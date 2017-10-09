---
title: "aaaInstall 以 hello Azure CLI Linux VM 上 MongoDB |Microsoft 文件"
description: "深入了解如何 tooinstall 上及設定 MongoDB Linux 虛擬機器 iusing hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 3f55b546-86df-4442-9ef4-8a25fae7b96e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 97a4d9913f0eeaf7b8bf15d7fc81befe538cdc8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm"></a>如何 tooinstall 及 Linux VM 上設定 MongoDB
[MongoDB](http://www.mongodb.org) 是受歡迎的高效能開放原始碼 NoSQL 資料庫。 本文章將示範如何 tooinstall 和以 hello Azure CLI 2.0 Linux VM 上設定 MongoDB。 您也可以執行下列步驟以 hello [Azure CLI 1.0](install-mongodb-nodejs.md)。 範例會詳細說明如何︰

* [手動安裝及設定基本 MongoDB 執行個體](#manually-install-and-configure-mongodb-on-a-vm)
* [使用 Resource Manager 範本建立基本 MongoDB 執行個體](#create-basic-mongodb-instance-on-centos-using-a-template)
* [使用 Resource Manager 範本建立複雜的 MongoDB 分區化叢集與複本集](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a>在 VM 上手動安裝及設定 MongoDB
MongoDB [提供 Linux 散發版本的安裝指示](https://docs.mongodb.com/manual/administration/install-on-linux/)，包括 Red Hat / CentOS、SUSE、Ubuntu 和 Debian。 hello 下列範例會建立*CentOS* VM。 toocreate 此環境中，您需要最新的 hello [Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。

使用 [az group create](/cli/azure/group#create) 來建立資源群組。 hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置：

```azurecli
az group create --name myResourceGroup --location eastus
```

使用 [az vm create](/cli/azure/vm#create) 來建立 VM。 hello 下列範例會建立名為的 VM *myVM*與名為使用者*azureuser*使用 SSH 公開金鑰驗證

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH toohello VM 使用您自己的使用者名稱和 hello `publicIpAddress` hello 輸出 hello 上一個步驟中所列：

```bash
ssh azureuser@<publicIpAddress>
```

tooadd hello 安裝來源的 MongoDB，建立**yum**儲存機制檔案，如下所示：

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

開啟 hello MongoDB 儲存機制檔案進行編輯。 加入下列行 hello:

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

使用 yum 安裝 MongoDB，如下所示：

```bash
sudo yum install -y mongodb-org
```

依預設，會在可防止您存取 MongoDB 的 CentOS 映像上強制採用 SELinux。 原則管理工具在安裝及設定 SELinux tooallow MongoDB toooperate 預設 TCP 通訊埠 27017，如下所示：

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

啟動 hello MongoDB 服務，如下所示：

```bash
sudo service mongod start
```

藉由連接使用 hello 本機驗證 hello MongoDB 安裝`mongo`用戶端：

```bash
mongo
```

現在加入一些資料，及搜尋測試 hello MongoDB 執行個體：

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

如有需要，MongoDB toostart 自動設定系統重新開機期間：

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a>使用範本在 CentOS 上建立基本 MongoDB 執行個體
您可以在單一的 CentOS vm 使用 hello GitHub 中的下列 Azure 快速入門範本建立基本的 MongoDB 執行個體。 此範本使用 hello 自訂指令碼擴充功能的 Linux tooadd **yum**儲存機制 tooyour 新建立的 CentOS VM，然後再安裝 MongoDB。

* [CentOS 上的基本 MongoDB 執行個體](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json

toocreate 此環境中，您需要最新的 hello [Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。 首先，使用 [az group create](/cli/azure/group#create) 建立資源群組。 hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置：

```azurecli
az group create --name myResourceGroup --location eastus
```

接下來，部署具有 hello MongoDB 範本[az 群組部署建立](/cli/azure/group/deployment#create)。 定義您自己的資源名稱和大小，例如，有需要*newStorageAccountName*， *virtualNetworkName*，和*vmSize*:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"},
    "virtualNetworkName": {"value": "myVnet"},
    "vmSize": {"value": "Standard_DS2_v2"},
    "vmName": {"value": "myVM"},
    "publicIPAddressName": {"value": "myPublicIP"},
    "nicName": {"value": "myNic"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

登入 toohello VM 使用您的 VM hello 公用 DNS 位址。 您可以檢視與 hello 公用 DNS 位址[az vm 顯示](/cli/azure/vm#show):

```azurecli
az vm show -g myResourceGroup -n myVM -d --query [fqdns] -o tsv
```

SSH tooyour VM 使用您自己的使用者名稱和公用 DNS 位址：

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

藉由連接使用 hello 本機驗證 hello MongoDB 安裝`mongo`用戶端，如下所示：

```bash
mongo
```

現在測試 hello 執行個體加入一些資料，並搜尋，如下所示：

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a>使用範本在 CentOS 上建立複雜的 MongoDB 分區化叢集
您可以建立複雜的 MongoDB 分區化叢集中，並使用 hello GitHub 中的下列 Azure 快速入門範本。 此範本會遵循 hello [MongoDB 分區化叢集的最佳作法](https://docs.mongodb.com/manual/core/sharded-cluster-components/)tooprovide 備援性和高可用性。 hello 範本會建立兩個分區，其中每個複本組中的三個節點。 一個具有三個節點設定的組態伺服器複本也會建立，再加上兩個**mongos**路由器伺服器 tooprovide 一致性 tooapplications 從跨 hello 分區。

* [CentOS 上的 MongoDB 分區化叢集](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json

> [!WARNING]
> 部署這個複雜的 MongoDB 分區化的叢集需要超過 20 個核心，通常是每個訂用帳戶的區域 hello 預設核心計數。 開啟 Azure 支援人員要求 tooincrease 核心計數。

toocreate 此環境中，您需要最新的 hello [Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。 首先，使用 [az group create](/cli/azure/group#create) 建立資源群組。 hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置：

```azurecli
az group create --name myResourceGroup --location eastus
```

接下來，部署具有 hello MongoDB 範本[az 群組部署建立](/cli/azure/group/deployment#create)。 在需要的地方定義您自己的資源名稱與大小，例如 mongoAdminUsername、sizeOfDataDiskInGB 和 configNodeVmSize：

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "mongoAdminUsername": {"value": "mongoadmin"},
    "mongoAdminPassword": {"value": "P@ssw0rd!"},
    "dnsNamePrefix": {"value": "mypublicdns"},
    "environment": {"value": "AzureCloud"},
    "numDataDisks": {"value": "4"},
    "sizeOfDataDiskInGB": {"value": 20},
    "centOsVersion": {"value": "7.0"},
    "routerNodeVmSize": {"value": "Standard_DS3_v2"},
    "configNodeVmSize": {"value": "Standard_DS3_v2"},
    "replicaNodeVmSize": {"value": "Standard_DS3_v2"},
    "zabbixServerIPAddress": {"value": "Null"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json \
  --name myMongoDBCluster \
  --no-wait
```

此部署可以接管小時 toodeploy，並設定所有 hello VM 執行個體。 hello`--no-wait`旗標用在 hello hello 前面命令 tooreturn 控制項 toohello 命令提示字元，一旦 hello 範本部署已由 hello Azure 平台的結尾。 然後，您可以檢視與 hello 部署狀態[az 群組部署顯示](/cli/azure/group/deployment#show)。 hello 下列範例檢視 hello 狀態 hello *myMongoDBCluster* hello 中的部署*myResourceGroup*資源群組：

```azurecli
az group deployment show \
    --resource-group myResourceGroup \
    --name myMongoDBCluster \
    --query [properties.provisioningState] \
    --output tsv
```

## <a name="next-steps"></a>後續步驟
在這些範例中，您連接 toohello MongoDB 執行個體在本機從 hello VM。 如果您想從其他 VM 或網路 tooconnect toohello MongoDB 執行個體，請確定適當的 hello[會建立網路安全性群組規則](nsg-quickstart.md)。

這些範例部署 hello 核心 MongoDB 環境為開發用途。 適用於您的環境所需的 hello 安全性組態選項。 如需詳細資訊，請參閱 hello [MongoDB 安全性文件](https://docs.mongodb.com/manual/security/)。

如需有關如何使用範本建立的詳細資訊，請參閱 hello [Azure 資源管理員概觀](../../azure-resource-manager/resource-group-overview.md)。

hello Azure Resource Manager 範本使用 hello 自訂指令碼擴充 toodownload，並在您的 Vm 上執行指令碼。 如需詳細資訊，請參閱[使用 hello Azure 自訂指令碼延伸與 Linux 虛擬機器](extensions-customscript.md)。

