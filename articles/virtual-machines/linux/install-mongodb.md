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
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm"></a><span data-ttu-id="485b7-103">如何 tooinstall 及 Linux VM 上設定 MongoDB</span><span class="sxs-lookup"><span data-stu-id="485b7-103">How tooinstall and configure MongoDB on a Linux VM</span></span>
<span data-ttu-id="485b7-104">[MongoDB](http://www.mongodb.org) 是受歡迎的高效能開放原始碼 NoSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="485b7-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="485b7-105">本文章將示範如何 tooinstall 和以 hello Azure CLI 2.0 Linux VM 上設定 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="485b7-105">This article shows you how tooinstall and configure MongoDB on a Linux VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="485b7-106">您也可以執行下列步驟以 hello [Azure CLI 1.0](install-mongodb-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="485b7-106">You can also perform these steps with hello [Azure CLI 1.0](install-mongodb-nodejs.md).</span></span> <span data-ttu-id="485b7-107">範例會詳細說明如何︰</span><span class="sxs-lookup"><span data-stu-id="485b7-107">Examples are shown that detail how to:</span></span>

* [<span data-ttu-id="485b7-108">手動安裝及設定基本 MongoDB 執行個體</span><span class="sxs-lookup"><span data-stu-id="485b7-108">Manually install and configure a basic MongoDB instance</span></span>](#manually-install-and-configure-mongodb-on-a-vm)
* [<span data-ttu-id="485b7-109">使用 Resource Manager 範本建立基本 MongoDB 執行個體</span><span class="sxs-lookup"><span data-stu-id="485b7-109">Create a basic MongoDB instance using a Resource Manager template</span></span>](#create-basic-mongodb-instance-on-centos-using-a-template)
* [<span data-ttu-id="485b7-110">使用 Resource Manager 範本建立複雜的 MongoDB 分區化叢集與複本集</span><span class="sxs-lookup"><span data-stu-id="485b7-110">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span></span>](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="485b7-111">在 VM 上手動安裝及設定 MongoDB</span><span class="sxs-lookup"><span data-stu-id="485b7-111">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="485b7-112">MongoDB [提供 Linux 散發版本的安裝指示](https://docs.mongodb.com/manual/administration/install-on-linux/)，包括 Red Hat / CentOS、SUSE、Ubuntu 和 Debian。</span><span class="sxs-lookup"><span data-stu-id="485b7-112">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="485b7-113">hello 下列範例會建立*CentOS* VM。</span><span class="sxs-lookup"><span data-stu-id="485b7-113">hello following example creates a *CentOS* VM.</span></span> <span data-ttu-id="485b7-114">toocreate 此環境中，您需要最新的 hello [Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。</span><span class="sxs-lookup"><span data-stu-id="485b7-114">toocreate this environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="485b7-115">使用 [az group create](/cli/azure/group#create) 來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="485b7-115">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="485b7-116">hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置：</span><span class="sxs-lookup"><span data-stu-id="485b7-116">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="485b7-117">使用 [az vm create](/cli/azure/vm#create) 來建立 VM。</span><span class="sxs-lookup"><span data-stu-id="485b7-117">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="485b7-118">hello 下列範例會建立名為的 VM *myVM*與名為使用者*azureuser*使用 SSH 公開金鑰驗證</span><span class="sxs-lookup"><span data-stu-id="485b7-118">hello following example creates a VM named *myVM* with a user named *azureuser* using SSH public key authentication</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="485b7-119">SSH toohello VM 使用您自己的使用者名稱和 hello `publicIpAddress` hello 輸出 hello 上一個步驟中所列：</span><span class="sxs-lookup"><span data-stu-id="485b7-119">SSH toohello VM using your own username and hello `publicIpAddress` listed in hello output from hello previous step:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="485b7-120">tooadd hello 安裝來源的 MongoDB，建立**yum**儲存機制檔案，如下所示：</span><span class="sxs-lookup"><span data-stu-id="485b7-120">tooadd hello installation sources for MongoDB, create a **yum** repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

<span data-ttu-id="485b7-121">開啟 hello MongoDB 儲存機制檔案進行編輯。</span><span class="sxs-lookup"><span data-stu-id="485b7-121">Open hello MongoDB repo file for editing.</span></span> <span data-ttu-id="485b7-122">加入下列行 hello:</span><span class="sxs-lookup"><span data-stu-id="485b7-122">Add hello following lines:</span></span>

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

<span data-ttu-id="485b7-123">使用 yum 安裝 MongoDB，如下所示：</span><span class="sxs-lookup"><span data-stu-id="485b7-123">Install MongoDB using **yum** as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="485b7-124">依預設，會在可防止您存取 MongoDB 的 CentOS 映像上強制採用 SELinux。</span><span class="sxs-lookup"><span data-stu-id="485b7-124">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="485b7-125">原則管理工具在安裝及設定 SELinux tooallow MongoDB toooperate 預設 TCP 通訊埠 27017，如下所示：</span><span class="sxs-lookup"><span data-stu-id="485b7-125">Install policy management tools and configure SELinux tooallow MongoDB toooperate on its default TCP port 27017 as follows:</span></span>

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="485b7-126">啟動 hello MongoDB 服務，如下所示：</span><span class="sxs-lookup"><span data-stu-id="485b7-126">Start hello MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="485b7-127">藉由連接使用 hello 本機驗證 hello MongoDB 安裝`mongo`用戶端：</span><span class="sxs-lookup"><span data-stu-id="485b7-127">Verify hello MongoDB installation by connecting using hello local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="485b7-128">現在加入一些資料，及搜尋測試 hello MongoDB 執行個體：</span><span class="sxs-lookup"><span data-stu-id="485b7-128">Now test hello MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="485b7-129">如有需要，MongoDB toostart 自動設定系統重新開機期間：</span><span class="sxs-lookup"><span data-stu-id="485b7-129">If desired, configure MongoDB toostart automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="485b7-130">使用範本在 CentOS 上建立基本 MongoDB 執行個體</span><span class="sxs-lookup"><span data-stu-id="485b7-130">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="485b7-131">您可以在單一的 CentOS vm 使用 hello GitHub 中的下列 Azure 快速入門範本建立基本的 MongoDB 執行個體。</span><span class="sxs-lookup"><span data-stu-id="485b7-131">You can create a basic MongoDB instance on a single CentOS VM using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="485b7-132">此範本使用 hello 自訂指令碼擴充功能的 Linux tooadd **yum**儲存機制 tooyour 新建立的 CentOS VM，然後再安裝 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="485b7-132">This template uses hello Custom Script extension for Linux tooadd a **yum** repository tooyour newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="485b7-133">[CentOS 上的基本 MongoDB 執行個體](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="485b7-133">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="485b7-134">toocreate 此環境中，您需要最新的 hello [Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。</span><span class="sxs-lookup"><span data-stu-id="485b7-134">toocreate this environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="485b7-135">首先，使用 [az group create](/cli/azure/group#create) 建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="485b7-135">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="485b7-136">hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置：</span><span class="sxs-lookup"><span data-stu-id="485b7-136">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="485b7-137">接下來，部署具有 hello MongoDB 範本[az 群組部署建立](/cli/azure/group/deployment#create)。</span><span class="sxs-lookup"><span data-stu-id="485b7-137">Next, deploy hello MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="485b7-138">定義您自己的資源名稱和大小，例如，有需要*newStorageAccountName*， *virtualNetworkName*，和*vmSize*:</span><span class="sxs-lookup"><span data-stu-id="485b7-138">Define your own resource names and sizes where needed such as for *newStorageAccountName*, *virtualNetworkName*, and *vmSize*:</span></span>

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

<span data-ttu-id="485b7-139">登入 toohello VM 使用您的 VM hello 公用 DNS 位址。</span><span class="sxs-lookup"><span data-stu-id="485b7-139">Log on toohello VM using hello public DNS address of your VM.</span></span> <span data-ttu-id="485b7-140">您可以檢視與 hello 公用 DNS 位址[az vm 顯示](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="485b7-140">You can view hello public DNS address with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show -g myResourceGroup -n myVM -d --query [fqdns] -o tsv
```

<span data-ttu-id="485b7-141">SSH tooyour VM 使用您自己的使用者名稱和公用 DNS 位址：</span><span class="sxs-lookup"><span data-stu-id="485b7-141">SSH tooyour VM using your own username and public DNS address:</span></span>

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

<span data-ttu-id="485b7-142">藉由連接使用 hello 本機驗證 hello MongoDB 安裝`mongo`用戶端，如下所示：</span><span class="sxs-lookup"><span data-stu-id="485b7-142">Verify hello MongoDB installation by connecting using hello local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="485b7-143">現在測試 hello 執行個體加入一些資料，並搜尋，如下所示：</span><span class="sxs-lookup"><span data-stu-id="485b7-143">Now test hello instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="485b7-144">使用範本在 CentOS 上建立複雜的 MongoDB 分區化叢集</span><span class="sxs-lookup"><span data-stu-id="485b7-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="485b7-145">您可以建立複雜的 MongoDB 分區化叢集中，並使用 hello GitHub 中的下列 Azure 快速入門範本。</span><span class="sxs-lookup"><span data-stu-id="485b7-145">You can create a complex MongoDB sharded cluster using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="485b7-146">此範本會遵循 hello [MongoDB 分區化叢集的最佳作法](https://docs.mongodb.com/manual/core/sharded-cluster-components/)tooprovide 備援性和高可用性。</span><span class="sxs-lookup"><span data-stu-id="485b7-146">This template follows hello [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide redundancy and high availability.</span></span> <span data-ttu-id="485b7-147">hello 範本會建立兩個分區，其中每個複本組中的三個節點。</span><span class="sxs-lookup"><span data-stu-id="485b7-147">hello template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="485b7-148">一個具有三個節點設定的組態伺服器複本也會建立，再加上兩個**mongos**路由器伺服器 tooprovide 一致性 tooapplications 從跨 hello 分區。</span><span class="sxs-lookup"><span data-stu-id="485b7-148">One config server replica set with three nodes is also created, plus two **mongos** router servers tooprovide consistency tooapplications from across hello shards.</span></span>

* <span data-ttu-id="485b7-149">[CentOS 上的 MongoDB 分區化叢集](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="485b7-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="485b7-150">部署這個複雜的 MongoDB 分區化的叢集需要超過 20 個核心，通常是每個訂用帳戶的區域 hello 預設核心計數。</span><span class="sxs-lookup"><span data-stu-id="485b7-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically hello default core count per region for a subscription.</span></span> <span data-ttu-id="485b7-151">開啟 Azure 支援人員要求 tooincrease 核心計數。</span><span class="sxs-lookup"><span data-stu-id="485b7-151">Open an Azure support request tooincrease your core count.</span></span>

<span data-ttu-id="485b7-152">toocreate 此環境中，您需要最新的 hello [Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。</span><span class="sxs-lookup"><span data-stu-id="485b7-152">toocreate this environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="485b7-153">首先，使用 [az group create](/cli/azure/group#create) 建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="485b7-153">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="485b7-154">hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置：</span><span class="sxs-lookup"><span data-stu-id="485b7-154">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="485b7-155">接下來，部署具有 hello MongoDB 範本[az 群組部署建立](/cli/azure/group/deployment#create)。</span><span class="sxs-lookup"><span data-stu-id="485b7-155">Next, deploy hello MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="485b7-156">在需要的地方定義您自己的資源名稱與大小，例如 mongoAdminUsername、sizeOfDataDiskInGB 和 configNodeVmSize：</span><span class="sxs-lookup"><span data-stu-id="485b7-156">Define your own resource names and sizes where needed such as for *mongoAdminUsername*, *sizeOfDataDiskInGB*, and *configNodeVmSize*:</span></span>

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

<span data-ttu-id="485b7-157">此部署可以接管小時 toodeploy，並設定所有 hello VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="485b7-157">This deployment can take over an hour toodeploy and configure all hello VM instances.</span></span> <span data-ttu-id="485b7-158">hello`--no-wait`旗標用在 hello hello 前面命令 tooreturn 控制項 toohello 命令提示字元，一旦 hello 範本部署已由 hello Azure 平台的結尾。</span><span class="sxs-lookup"><span data-stu-id="485b7-158">hello `--no-wait` flag is used at hello end of hello preceding command tooreturn control toohello command prompt once hello template deployment has been accepted by hello Azure platform.</span></span> <span data-ttu-id="485b7-159">然後，您可以檢視與 hello 部署狀態[az 群組部署顯示](/cli/azure/group/deployment#show)。</span><span class="sxs-lookup"><span data-stu-id="485b7-159">You can then view hello deployment status with [az group deployment show](/cli/azure/group/deployment#show).</span></span> <span data-ttu-id="485b7-160">hello 下列範例檢視 hello 狀態 hello *myMongoDBCluster* hello 中的部署*myResourceGroup*資源群組：</span><span class="sxs-lookup"><span data-stu-id="485b7-160">hello following example views hello status for hello *myMongoDBCluster* deployment in hello *myResourceGroup* resource group:</span></span>

```azurecli
az group deployment show \
    --resource-group myResourceGroup \
    --name myMongoDBCluster \
    --query [properties.provisioningState] \
    --output tsv
```

## <a name="next-steps"></a><span data-ttu-id="485b7-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="485b7-161">Next steps</span></span>
<span data-ttu-id="485b7-162">在這些範例中，您連接 toohello MongoDB 執行個體在本機從 hello VM。</span><span class="sxs-lookup"><span data-stu-id="485b7-162">In these examples, you connect toohello MongoDB instance locally from hello VM.</span></span> <span data-ttu-id="485b7-163">如果您想從其他 VM 或網路 tooconnect toohello MongoDB 執行個體，請確定適當的 hello[會建立網路安全性群組規則](nsg-quickstart.md)。</span><span class="sxs-lookup"><span data-stu-id="485b7-163">If you want tooconnect toohello MongoDB instance from another VM or network, ensure hello appropriate [Network Security Group rules are created](nsg-quickstart.md).</span></span>

<span data-ttu-id="485b7-164">這些範例部署 hello 核心 MongoDB 環境為開發用途。</span><span class="sxs-lookup"><span data-stu-id="485b7-164">These examples deploy hello core MongoDB environment for development purposes.</span></span> <span data-ttu-id="485b7-165">適用於您的環境所需的 hello 安全性組態選項。</span><span class="sxs-lookup"><span data-stu-id="485b7-165">Apply hello required security configuration options for your environment.</span></span> <span data-ttu-id="485b7-166">如需詳細資訊，請參閱 hello [MongoDB 安全性文件](https://docs.mongodb.com/manual/security/)。</span><span class="sxs-lookup"><span data-stu-id="485b7-166">For more information, see hello [MongoDB security docs](https://docs.mongodb.com/manual/security/).</span></span>

<span data-ttu-id="485b7-167">如需有關如何使用範本建立的詳細資訊，請參閱 hello [Azure 資源管理員概觀](../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="485b7-167">For more information about creating using templates, see hello [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="485b7-168">hello Azure Resource Manager 範本使用 hello 自訂指令碼擴充 toodownload，並在您的 Vm 上執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="485b7-168">hello Azure Resource Manager templates use hello Custom Script Extension toodownload and execute scripts on your VMs.</span></span> <span data-ttu-id="485b7-169">如需詳細資訊，請參閱[使用 hello Azure 自訂指令碼延伸與 Linux 虛擬機器](extensions-customscript.md)。</span><span class="sxs-lookup"><span data-stu-id="485b7-169">For more information, see [Using hello Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span></span>

