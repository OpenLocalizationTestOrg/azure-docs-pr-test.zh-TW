---
title: "使用 Linux VM 上 MongoDB aaaInstall hello Azure CLI 1.0 |Microsoft 文件"
description: "深入了解如何 tooinstall 及使用 hello Resource Manager 部署模型在 Azure 中 Linux 虛擬機器上設定 MongoDB。"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 3f55b546-86df-4442-9ef4-8a25fae7b96e
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 4ce21a2c63da7d00a4422e0a6766e2103e7f12d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm-using-hello-azure-cli-10"></a>如何 tooinstall 及使用 Azure CLI 1.0 hello Linux VM 上設定 MongoDB
[MongoDB](http://www.mongodb.org) 是受歡迎的高效能開放原始碼 NoSQL 資料庫。 本文章將示範如何 tooinstall 及使用 hello Resource Manager 部署模型在 Azure 中 Linux VM 上設定 MongoDB。 範例會詳細說明如何︰

* [手動安裝及設定基本 MongoDB 執行個體](#manually-install-and-configure-mongodb-on-a-vm)
* [使用 Resource Manager 範本建立基本 MongoDB 執行個體](#create-basic-mongodb-instance-on-centos-using-a-template)
* [使用 Resource Manager 範本建立複雜的 MongoDB 分區化叢集與複本集](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="cli-versions-toocomplete-hello-task"></a>CLI 版本 toocomplete hello 工作
您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：

- Azure CLI 1.0 – 我們 CLI hello 傳統和資源管理部署模型 （此文件）
- [Azure CLI 2.0](create-cli-complete-nodejs.md) -hello 資源管理部署模型我們下一個層代 CLI


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a>在 VM 上手動安裝及設定 MongoDB
MongoDB [提供 Linux 散發版本的安裝指示](https://docs.mongodb.com/manual/administration/install-on-linux/)，包括 Red Hat / CentOS、SUSE、Ubuntu 和 Debian。 hello 下列範例會建立*CentOS* VM 使用 SSH 金鑰儲存在*~/.ssh/id_rsa.pub*。 回應 hello 提示您輸入儲存體帳戶名稱、 DNS 名稱和管理員認證：

```azurecli
azure vm quick-create \
    --image-urn CentOS \
    --ssh-publickey-file ~/.ssh/id_rsa.pub 
```

登入 toohello VM 使用 hello 結尾 hello hello 前面 VM 建立步驟顯示公用 IP 位址：

```bash
ssh azureuser@40.78.23.145
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

依預設，會在可防止您存取 MongoDB 的 CentOS 映像上強制採用 SELinux。 原則管理工具上安裝及設定 SELinux tooallow MongoDB toooperate 預設 TCP 通訊埠 27017，如下所示。 

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
您可以在單一的 CentOS vm 使用 hello GitHub 中的下列 Azure 快速入門範本建立基本的 MongoDB 執行個體。 此範本使用 hello 自訂指令碼擴充功能的 Linux tooadd`yum`儲存機制 tooyour 新建立的 CentOS VM，然後再安裝 MongoDB。

* [CentOS 上的基本 MongoDB 執行個體](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json

hello 下列範例會建立資源群組名稱 hello`myResourceGroup`在 hello`eastus`區域。 輸入您自己的值，如下所示︰

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

> [!NOTE]
> hello Azure CLI 傳回您 tooa 提示字元建立 hello 部署，但 hello 安裝在幾秒鐘內，並組態採用幾分鐘的時間 toocomplete。 檢查與 hello 部署的 hello 狀態`azure group deployment show myResourceGroup`，據此輸入 hello 的資源群組的名稱。 等候直到在 hello **ProvisioningState**顯示*Succeeded*之前嘗試 tooSSH toohello VM。

一旦 hello 部署完成，SSH toohello VM。 取得 hello IP 位址，您的 VM 使用 hello`azure vm show`命令如 hello 下列範例所示：

```azurecli
azure vm show --resource-group myResourceGroup --name myLinuxVM
```

接近 hello hello 輸出結尾，會顯示 hello 公用 IP 位址。 SSH tooyour VM hello IP 位址，為您的 VM:

```bash
ssh azureuser@138.91.149.74
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

hello 下列範例會建立資源群組名稱 hello *myResourceGroup*在 hello *eastus*區域。 輸入您自己的值，如下所示︰

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json
```

> [!NOTE]
> hello Azure CLI 傳回您 tooa 提示字元建立 hello 部署的幾秒內，但 hello 安裝和設定可能會花費小時 toocomplete。 檢查與 hello 部署的 hello 狀態`azure group deployment show myResourceGroup`，據此調整 hello 的資源群組的名稱。 等候直到在 hello **ProvisioningState**顯示*Succeeded*之前 toohello Vm 連線。


## <a name="next-steps"></a>後續步驟
在這些範例中，您連接 toohello MongoDB 執行個體在本機從 hello VM。 如果您想從其他 VM 或網路 tooconnect toohello MongoDB 執行個體，請確定適當的 hello[會建立網路安全性群組規則](nsg-quickstart.md)。

如需有關如何使用範本建立的詳細資訊，請參閱 hello [Azure 資源管理員概觀](../../azure-resource-manager/resource-group-overview.md)。

hello Azure Resource Manager 範本使用 hello 自訂指令碼擴充 toodownload，並在您的 Vm 上執行指令碼。 如需詳細資訊，請參閱[使用 hello Azure 自訂指令碼延伸與 Linux 虛擬機器](extensions-customscript.md)。

