---
title: "使用 Azure CLI 在 Linux VM 上安裝 MongoDB | Microsoft Docs"
description: "了解如何使用 Azure CLI 2.0 在 Linux 虛擬機器上安裝及設定 MongoDB"
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
ms.openlocfilehash: e19c09558285497f29eb78b4f4ae5b15d7f1a191
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-install-and-configure-mongodb-on-a-linux-vm"></a><span data-ttu-id="f7ca8-103">如何在 Linux VM 上安裝及設定 MongoDB</span><span class="sxs-lookup"><span data-stu-id="f7ca8-103">How to install and configure MongoDB on a Linux VM</span></span>
<span data-ttu-id="f7ca8-104">[MongoDB](http://www.mongodb.org) 是受歡迎的高效能開放原始碼 NoSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="f7ca8-105">本文說明如何使用 Azure CLI 2.0 在 Linux VM 上安裝及設定 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-105">This article shows you how to install and configure MongoDB on a Linux VM with the Azure CLI 2.0.</span></span> <span data-ttu-id="f7ca8-106">您也可以使用 [Azure CLI 1.0](install-mongodb-nodejs.md) 來執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-106">You can also perform these steps with the [Azure CLI 1.0](install-mongodb-nodejs.md).</span></span> <span data-ttu-id="f7ca8-107">範例會詳細說明如何︰</span><span class="sxs-lookup"><span data-stu-id="f7ca8-107">Examples are shown that detail how to:</span></span>

* [<span data-ttu-id="f7ca8-108">手動安裝及設定基本 MongoDB 執行個體</span><span class="sxs-lookup"><span data-stu-id="f7ca8-108">Manually install and configure a basic MongoDB instance</span></span>](#manually-install-and-configure-mongodb-on-a-vm)
* [<span data-ttu-id="f7ca8-109">使用 Resource Manager 範本建立基本 MongoDB 執行個體</span><span class="sxs-lookup"><span data-stu-id="f7ca8-109">Create a basic MongoDB instance using a Resource Manager template</span></span>](#create-basic-mongodb-instance-on-centos-using-a-template)
* [<span data-ttu-id="f7ca8-110">使用 Resource Manager 範本建立複雜的 MongoDB 分區化叢集與複本集</span><span class="sxs-lookup"><span data-stu-id="f7ca8-110">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span></span>](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="f7ca8-111">在 VM 上手動安裝及設定 MongoDB</span><span class="sxs-lookup"><span data-stu-id="f7ca8-111">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="f7ca8-112">MongoDB [提供 Linux 散發版本的安裝指示](https://docs.mongodb.com/manual/administration/install-on-linux/)，包括 Red Hat / CentOS、SUSE、Ubuntu 和 Debian。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-112">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="f7ca8-113">下列範例會建立名為 CentOS 的 VM。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-113">The following example creates a *CentOS* VM.</span></span> <span data-ttu-id="f7ca8-114">若要建立此環境，您需要安裝最新的 [Azure CLI 2.0](/cli/azure/install-az-cli2)，並使用 [az login](/cli/azure/#login) 來登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-114">To create this environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="f7ca8-115">使用 [az group create](/cli/azure/group#create) 來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-115">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="f7ca8-116">下列範例會在 eastus 位置建立名為 myResourceGroup 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="f7ca8-116">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="f7ca8-117">使用 [az vm create](/cli/azure/vm#create) 建立 VM。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-117">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="f7ca8-118">下列範例會建立名為 *myVM* 的 VM，其中具有使用 SSH 公開金鑰驗證、名為 *azureuser* 的使用者</span><span class="sxs-lookup"><span data-stu-id="f7ca8-118">The following example creates a VM named *myVM* with a user named *azureuser* using SSH public key authentication</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="f7ca8-119">使用您自己的使用者名稱和上一個步驟輸出中列出的 `publicIpAddress`，透過 SSH 連接到 VM：</span><span class="sxs-lookup"><span data-stu-id="f7ca8-119">SSH to the VM using your own username and the `publicIpAddress` listed in the output from the previous step:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="f7ca8-120">若要新增 MongoDB 的安裝來源，請建立 yum 存放庫檔案，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="f7ca8-120">To add the installation sources for MongoDB, create a **yum** repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

<span data-ttu-id="f7ca8-121">開啟 MongoDB 儲存機制檔案以進行編輯。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-121">Open the MongoDB repo file for editing.</span></span> <span data-ttu-id="f7ca8-122">加入下列幾行：</span><span class="sxs-lookup"><span data-stu-id="f7ca8-122">Add the following lines:</span></span>

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

<span data-ttu-id="f7ca8-123">使用 yum 安裝 MongoDB，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f7ca8-123">Install MongoDB using **yum** as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="f7ca8-124">依預設，會在可防止您存取 MongoDB 的 CentOS 映像上強制採用 SELinux。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-124">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="f7ca8-125">安裝原則管理工具及設定 SELinux，以允許 MongoDB 在其預設 TCP 通訊埠 27017 上運作，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f7ca8-125">Install policy management tools and configure SELinux to allow MongoDB to operate on its default TCP port 27017 as follows:</span></span>

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="f7ca8-126">啟動 MongoDB 服務，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="f7ca8-126">Start the MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="f7ca8-127">藉由使用本機 `mongo` 用戶端連線來確認 MongoDB 安裝︰</span><span class="sxs-lookup"><span data-stu-id="f7ca8-127">Verify the MongoDB installation by connecting using the local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="f7ca8-128">現在，新增一些資料然後進行搜尋，以測試 MongoDB 執行個體︰</span><span class="sxs-lookup"><span data-stu-id="f7ca8-128">Now test the MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="f7ca8-129">如有需要，設定 MongoDB 以在系統重新開機期間自動啟動：</span><span class="sxs-lookup"><span data-stu-id="f7ca8-129">If desired, configure MongoDB to start automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="f7ca8-130">使用範本在 CentOS 上建立基本 MongoDB 執行個體</span><span class="sxs-lookup"><span data-stu-id="f7ca8-130">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="f7ca8-131">您可以使用下列來自 GitHub 的 Azure 快速入門範本，在單一 CentOS VM 上建立基本的 MongoDB 執行個體。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-131">You can create a basic MongoDB instance on a single CentOS VM using the following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="f7ca8-132">這個範本會使用 Linux 適用的自訂指令碼延伸模組將 yum 存放庫新增至您新建立的 CentOS VM，然後安裝 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-132">This template uses the Custom Script extension for Linux to add a **yum** repository to your newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="f7ca8-133">[CentOS 上的基本 MongoDB 執行個體](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="f7ca8-133">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="f7ca8-134">若要建立此環境，您需要安裝最新的 [Azure CLI 2.0](/cli/azure/install-az-cli2)，並使用 [az login](/cli/azure/#login) 來登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-134">To create this environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="f7ca8-135">首先，使用 [az group create](/cli/azure/group#create) 建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-135">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="f7ca8-136">下列範例會在 eastus 位置建立名為 myResourceGroup 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="f7ca8-136">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="f7ca8-137">接著，使用 [az group deployment create](/cli/azure/group/deployment#create) 來佈建 MongoDB 範本。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-137">Next, deploy the MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="f7ca8-138">定義您自己的資源名稱和大小，例如，有需要*newStorageAccountName*， *virtualNetworkName*，和*vmSize*:</span><span class="sxs-lookup"><span data-stu-id="f7ca8-138">Define your own resource names and sizes where needed such as for *newStorageAccountName*, *virtualNetworkName*, and *vmSize*:</span></span>

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

<span data-ttu-id="f7ca8-139">使用您 VM 的公用 DNS 位址來登入 VM。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-139">Log on to the VM using the public DNS address of your VM.</span></span> <span data-ttu-id="f7ca8-140">您可以使用 [az vm show](/cli/azure/vm#show) 來檢視公用 DNS 位址：</span><span class="sxs-lookup"><span data-stu-id="f7ca8-140">You can view the public DNS address with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show -g myResourceGroup -n myVM -d --query [fqdns] -o tsv
```

<span data-ttu-id="f7ca8-141">使用您自己的使用者名稱和公用 DNS 位址來透過 SSH 連線到 VM：</span><span class="sxs-lookup"><span data-stu-id="f7ca8-141">SSH to your VM using your own username and public DNS address:</span></span>

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

<span data-ttu-id="f7ca8-142">藉由使用本機 `mongo` 用戶端連線來確認 MongoDB 安裝，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="f7ca8-142">Verify the MongoDB installation by connecting using the local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="f7ca8-143">現在，新增一些資料並進行搜尋來測試執行個體，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="f7ca8-143">Now test the instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="f7ca8-144">使用範本在 CentOS 上建立複雜的 MongoDB 分區化叢集</span><span class="sxs-lookup"><span data-stu-id="f7ca8-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="f7ca8-145">您可以使用下列來自 GitHub 的 Azure 快速入門範本，建立複雜的 MongoDB 分區化叢集。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-145">You can create a complex MongoDB sharded cluster using the following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="f7ca8-146">此範本遵循 [MongoDB 分區化叢集最佳作法](https://docs.mongodb.com/manual/core/sharded-cluster-components/)提供備援和高可用性。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-146">This template follows the [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) to provide redundancy and high availability.</span></span> <span data-ttu-id="f7ca8-147">範本會建立兩個分區，其中每個複本集中有三個節點。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-147">The template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="f7ca8-148">還會建立具有三個節點的組態伺服器複本集，加上兩個 mongos 路由器伺服器，以提供跨分區應用程式的一致性。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-148">One config server replica set with three nodes is also created, plus two **mongos** router servers to provide consistency to applications from across the shards.</span></span>

* <span data-ttu-id="f7ca8-149">[CentOS 上的 MongoDB 分區化叢集](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="f7ca8-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="f7ca8-150">部署這個複雜的 MongoDB 分區化叢集需要超過 20 個核心，通常是每個訂用帳戶區域的預設核心計數。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically the default core count per region for a subscription.</span></span> <span data-ttu-id="f7ca8-151">開啟 Azure 支援要求，以增加核心計數。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-151">Open an Azure support request to increase your core count.</span></span>

<span data-ttu-id="f7ca8-152">若要建立此環境，您需要安裝最新的 [Azure CLI 2.0](/cli/azure/install-az-cli2)，並使用 [az login](/cli/azure/#login) 來登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-152">To create this environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="f7ca8-153">首先，使用 [az group create](/cli/azure/group#create) 建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-153">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="f7ca8-154">下列範例會在 eastus 位置建立名為 myResourceGroup 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="f7ca8-154">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="f7ca8-155">接著，使用 [az group deployment create](/cli/azure/group/deployment#create) 來佈建 MongoDB 範本。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-155">Next, deploy the MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="f7ca8-156">在需要的地方定義您自己的資源名稱與大小，例如 mongoAdminUsername、sizeOfDataDiskInGB 和 configNodeVmSize：</span><span class="sxs-lookup"><span data-stu-id="f7ca8-156">Define your own resource names and sizes where needed such as for *mongoAdminUsername*, *sizeOfDataDiskInGB*, and *configNodeVmSize*:</span></span>

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

<span data-ttu-id="f7ca8-157">這項部署可能需要超過一小時的時間來部署及設定所有 VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-157">This deployment can take over an hour to deploy and configure all the VM instances.</span></span> <span data-ttu-id="f7ca8-158">`--no-wait` 旗標是用在上述命令的結尾，可在 Azure 平台接受範本部署之後，將控制權交回給命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-158">The `--no-wait` flag is used at the end of the preceding command to return control to the command prompt once the template deployment has been accepted by the Azure platform.</span></span> <span data-ttu-id="f7ca8-159">您可以接著使用 [az group deployment show](/cli/azure/group/deployment#show) 來檢視部署狀態。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-159">You can then view the deployment status with [az group deployment show](/cli/azure/group/deployment#show).</span></span> <span data-ttu-id="f7ca8-160">下列範例會檢視 myResourceGroup 資源群組中 myMongoDBCluster 部署的狀態：</span><span class="sxs-lookup"><span data-stu-id="f7ca8-160">The following example views the status for the *myMongoDBCluster* deployment in the *myResourceGroup* resource group:</span></span>

```azurecli
az group deployment show \
    --resource-group myResourceGroup \
    --name myMongoDBCluster \
    --query [properties.provisioningState] \
    --output tsv
```

## <a name="next-steps"></a><span data-ttu-id="f7ca8-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f7ca8-161">Next steps</span></span>
<span data-ttu-id="f7ca8-162">在這些範例中，您會從 VM 本機連線到 MongoDB 執行個體。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-162">In these examples, you connect to the MongoDB instance locally from the VM.</span></span> <span data-ttu-id="f7ca8-163">如果您想要從另一個 VM 或網路連線到 MongoDB 執行個體，請確定建立適當的[網路安全性群組規則](nsg-quickstart.md)。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-163">If you want to connect to the MongoDB instance from another VM or network, ensure the appropriate [Network Security Group rules are created](nsg-quickstart.md).</span></span>

<span data-ttu-id="f7ca8-164">這些範例會部署核心 MongoDB 環境以用於開發用途。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-164">These examples deploy the core MongoDB environment for development purposes.</span></span> <span data-ttu-id="f7ca8-165">請為您的環境套用必要的安全性設定選項。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-165">Apply the required security configuration options for your environment.</span></span> <span data-ttu-id="f7ca8-166">如需詳細資訊，請參閱 [MongoDB 安全性文件](https://docs.mongodb.com/manual/security/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-166">For more information, see the [MongoDB security docs](https://docs.mongodb.com/manual/security/).</span></span>

<span data-ttu-id="f7ca8-167">如需關於建立範本的詳細資訊，請參閱 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-167">For more information about creating using templates, see the [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="f7ca8-168">Azure Resource Manager 範本會使用自訂指令碼延伸模組，在您的 VM 上下載並執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-168">The Azure Resource Manager templates use the Custom Script Extension to download and execute scripts on your VMs.</span></span> <span data-ttu-id="f7ca8-169">如需詳細資訊，請參閱[搭配 Linux 虛擬機器使用 Azure 自訂指令碼擴充功能](extensions-customscript.md)。</span><span class="sxs-lookup"><span data-stu-id="f7ca8-169">For more information, see [Using the Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span></span>

