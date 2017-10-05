---
title: "使用 Azure CLI 1.0 在 Linux VM 上安裝 MongoDB | Microsoft Docs"
description: "了解如何使用 Resource Manager 部署模型在 Azure 中的 Linux 虛擬機器上安裝及設定 MongoDB。"
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
ms.openlocfilehash: c97ade0a3d95824f723aad55776de861fe49441f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-install-and-configure-mongodb-on-a-linux-vm-using-the-azure-cli-10"></a><span data-ttu-id="6f9b5-103">如何使用 Azure CLI 1.0 在 Linux VM 上安裝及設定 MongoDB</span><span class="sxs-lookup"><span data-stu-id="6f9b5-103">How to install and configure MongoDB on a Linux VM using the Azure CLI 1.0</span></span>
<span data-ttu-id="6f9b5-104">[MongoDB](http://www.mongodb.org) 是受歡迎的高效能開放原始碼 NoSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="6f9b5-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="6f9b5-105">本文說明如何使用 Resource Manager 部署模型在 Azure 中的 Linux VM 上安裝及設定 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="6f9b5-105">This article shows you how to install and configure MongoDB on a Linux VM in Azure using the Resource Manager deployment model.</span></span> <span data-ttu-id="6f9b5-106">範例會詳細說明如何︰</span><span class="sxs-lookup"><span data-stu-id="6f9b5-106">Examples are shown that detail how to:</span></span>

* [<span data-ttu-id="6f9b5-107">手動安裝及設定基本 MongoDB 執行個體</span><span class="sxs-lookup"><span data-stu-id="6f9b5-107">Manually install and configure a basic MongoDB instance</span></span>](#manually-install-and-configure-mongodb-on-a-vm)
* [<span data-ttu-id="6f9b5-108">使用 Resource Manager 範本建立基本 MongoDB 執行個體</span><span class="sxs-lookup"><span data-stu-id="6f9b5-108">Create a basic MongoDB instance using a Resource Manager template</span></span>](#create-basic-mongodb-instance-on-centos-using-a-template)
* [<span data-ttu-id="6f9b5-109">使用 Resource Manager 範本建立複雜的 MongoDB 分區化叢集與複本集</span><span class="sxs-lookup"><span data-stu-id="6f9b5-109">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span></span>](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="6f9b5-110">用以完成工作的 CLI 版本</span><span class="sxs-lookup"><span data-stu-id="6f9b5-110">CLI versions to complete the task</span></span>
<span data-ttu-id="6f9b5-111">您可以使用下列其中一個 CLI 版本來完成工作︰</span><span class="sxs-lookup"><span data-stu-id="6f9b5-111">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="6f9b5-112">Azure CLI 1.0 - 適用於傳統和資源管理部署模型 (本文) 的 CLI</span><span class="sxs-lookup"><span data-stu-id="6f9b5-112">Azure CLI 1.0 – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="6f9b5-113">[Azure CLI 2.0](create-cli-complete-nodejs.md) - 適用於資源管理部署模型的新一代 CLI</span><span class="sxs-lookup"><span data-stu-id="6f9b5-113">[Azure CLI 2.0](create-cli-complete-nodejs.md) - our next generation CLI for the resource management deployment model</span></span>


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="6f9b5-114">在 VM 上手動安裝及設定 MongoDB</span><span class="sxs-lookup"><span data-stu-id="6f9b5-114">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="6f9b5-115">MongoDB [提供 Linux 散發版本的安裝指示](https://docs.mongodb.com/manual/administration/install-on-linux/)，包括 Red Hat / CentOS、SUSE、Ubuntu 和 Debian。</span><span class="sxs-lookup"><span data-stu-id="6f9b5-115">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="6f9b5-116">下列範例使用儲存在 ~/.ssh/id_rsa.pub 的 SSH 金鑰建立 CentOS VM。</span><span class="sxs-lookup"><span data-stu-id="6f9b5-116">The following example creates a *CentOS* VM using an SSH key stored at *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="6f9b5-117">回答儲存體帳戶名稱、DNS 名稱和系統管理員認證的提示︰</span><span class="sxs-lookup"><span data-stu-id="6f9b5-117">Answer the prompts for storage account name, DNS name, and admin credentials:</span></span>

```azurecli
azure vm quick-create \
    --image-urn CentOS \
    --ssh-publickey-file ~/.ssh/id_rsa.pub 
```

<span data-ttu-id="6f9b5-118">使用前一個 VM 建立步驟結尾所顯示的公用 IP 位址登入 VM︰</span><span class="sxs-lookup"><span data-stu-id="6f9b5-118">Log on to the VM using the public IP address displayed at the end of the preceding VM creation step:</span></span>

```bash
ssh azureuser@40.78.23.145
```

<span data-ttu-id="6f9b5-119">若要新增 MongoDB 的安裝來源，請建立 yum 存放庫檔案，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="6f9b5-119">To add the installation sources for MongoDB, create a **yum** repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

<span data-ttu-id="6f9b5-120">開啟 MongoDB 儲存機制檔案以進行編輯。</span><span class="sxs-lookup"><span data-stu-id="6f9b5-120">Open the MongoDB repo file for editing.</span></span> <span data-ttu-id="6f9b5-121">加入下列幾行：</span><span class="sxs-lookup"><span data-stu-id="6f9b5-121">Add the following lines:</span></span>

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

<span data-ttu-id="6f9b5-122">使用 yum 安裝 MongoDB，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6f9b5-122">Install MongoDB using **yum** as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="6f9b5-123">依預設，會在可防止您存取 MongoDB 的 CentOS 映像上強制採用 SELinux。</span><span class="sxs-lookup"><span data-stu-id="6f9b5-123">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="6f9b5-124">安裝原則管理工具及設定 SELinux，以允許 MongoDB 在其預設 TCP 連接埠 27017 上運作，如下所示。</span><span class="sxs-lookup"><span data-stu-id="6f9b5-124">Install policy management tools and configure SELinux to allow MongoDB to operate on its default TCP port 27017 as follows.</span></span> 

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="6f9b5-125">啟動 MongoDB 服務，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="6f9b5-125">Start the MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="6f9b5-126">藉由使用本機 `mongo` 用戶端連線來確認 MongoDB 安裝︰</span><span class="sxs-lookup"><span data-stu-id="6f9b5-126">Verify the MongoDB installation by connecting using the local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="6f9b5-127">現在，新增一些資料然後進行搜尋，以測試 MongoDB 執行個體︰</span><span class="sxs-lookup"><span data-stu-id="6f9b5-127">Now test the MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="6f9b5-128">如有需要，設定 MongoDB 以在系統重新開機期間自動啟動：</span><span class="sxs-lookup"><span data-stu-id="6f9b5-128">If desired, configure MongoDB to start automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="6f9b5-129">使用範本在 CentOS 上建立基本 MongoDB 執行個體</span><span class="sxs-lookup"><span data-stu-id="6f9b5-129">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="6f9b5-130">您可以使用下列來自 GitHub 的 Azure 快速入門範本，在單一 CentOS VM 上建立基本的 MongoDB 執行個體。</span><span class="sxs-lookup"><span data-stu-id="6f9b5-130">You can create a basic MongoDB instance on a single CentOS VM using the following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="6f9b5-131">這個範本會使用 Linux 適用的自訂指令碼延伸模組將 `yum` 儲存機制新增至您新建立的 CentOS VM，然後安裝 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="6f9b5-131">This template uses the Custom Script extension for Linux to add a `yum` repository to your newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="6f9b5-132">[CentOS 上的基本 MongoDB 執行個體](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="6f9b5-132">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="6f9b5-133">下列範例會在 `eastus` 區域建立名為 `myResourceGroup` 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="6f9b5-133">The following example creates a resource group with the name `myResourceGroup` in the `eastus` region.</span></span> <span data-ttu-id="6f9b5-134">輸入您自己的值，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="6f9b5-134">Enter your own values as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="6f9b5-135">Azure CLI 會在建立部署後幾秒鐘內讓您回到提示，但是安裝和設定需要幾分鐘才能完成。</span><span class="sxs-lookup"><span data-stu-id="6f9b5-135">The Azure CLI returns you to a prompt within a few seconds of creating the deployment, but the installation and configuration takes a few minutes to complete.</span></span> <span data-ttu-id="6f9b5-136">使用 `azure group deployment show myResourceGroup` 檢查部署狀態，據以輸入資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="6f9b5-136">Check the status of the deployment with `azure group deployment show myResourceGroup`, entering the name of your resource group accordingly.</span></span> <span data-ttu-id="6f9b5-137">等到 ProvisioningState 顯示 Succeeded 後，再嘗試將 SSH 連線到 VM。</span><span class="sxs-lookup"><span data-stu-id="6f9b5-137">Wait until the **ProvisioningState** shows *Succeeded* before trying to SSH to the VM.</span></span>

<span data-ttu-id="6f9b5-138">一旦部署完成時，SSH 連線到 VM。</span><span class="sxs-lookup"><span data-stu-id="6f9b5-138">Once the deployment is complete, SSH to the VM.</span></span> <span data-ttu-id="6f9b5-139">使用 `azure vm show` 命令取得 VM 的 IP 位址，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="6f9b5-139">Obtain the IP address of your VM using the `azure vm show` command as in the following example:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myLinuxVM
```

<span data-ttu-id="6f9b5-140">在輸出的結尾附近，會顯示公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6f9b5-140">Near the end of the output, the public IP address is displayed.</span></span> <span data-ttu-id="6f9b5-141">SSH 連線到您的 VM，包含您 VM 的 IP 位址︰</span><span class="sxs-lookup"><span data-stu-id="6f9b5-141">SSH to your VM with the IP address of your VM:</span></span>

```bash
ssh azureuser@138.91.149.74
```

<span data-ttu-id="6f9b5-142">藉由使用本機 `mongo` 用戶端連線來確認 MongoDB 安裝，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="6f9b5-142">Verify the MongoDB installation by connecting using the local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="6f9b5-143">現在，新增一些資料並進行搜尋來測試執行個體，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="6f9b5-143">Now test the instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="6f9b5-144">使用範本在 CentOS 上建立複雜的 MongoDB 分區化叢集</span><span class="sxs-lookup"><span data-stu-id="6f9b5-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="6f9b5-145">您可以使用下列來自 GitHub 的 Azure 快速入門範本，建立複雜的 MongoDB 分區化叢集。</span><span class="sxs-lookup"><span data-stu-id="6f9b5-145">You can create a complex MongoDB sharded cluster using the following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="6f9b5-146">此範本遵循 [MongoDB 分區化叢集最佳作法](https://docs.mongodb.com/manual/core/sharded-cluster-components/)提供備援和高可用性。</span><span class="sxs-lookup"><span data-stu-id="6f9b5-146">This template follows the [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) to provide redundancy and high availability.</span></span> <span data-ttu-id="6f9b5-147">範本會建立兩個分區，其中每個複本集中有三個節點。</span><span class="sxs-lookup"><span data-stu-id="6f9b5-147">The template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="6f9b5-148">還會建立具有三個節點的組態伺服器複本集，加上兩個 mongos 路由器伺服器，以提供跨分區應用程式的一致性。</span><span class="sxs-lookup"><span data-stu-id="6f9b5-148">One config server replica set with three nodes is also created, plus two **mongos** router servers to provide consistency to applications from across the shards.</span></span>

* <span data-ttu-id="6f9b5-149">[CentOS 上的 MongoDB 分區化叢集](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="6f9b5-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="6f9b5-150">部署這個複雜的 MongoDB 分區化叢集需要超過 20 個核心，通常是每個訂用帳戶區域的預設核心計數。</span><span class="sxs-lookup"><span data-stu-id="6f9b5-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically the default core count per region for a subscription.</span></span> <span data-ttu-id="6f9b5-151">開啟 Azure 支援要求，以增加核心計數。</span><span class="sxs-lookup"><span data-stu-id="6f9b5-151">Open an Azure support request to increase your core count.</span></span>

<span data-ttu-id="6f9b5-152">以下範例會在 eastus 區域建立名為 myResourceGroup 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="6f9b5-152">The following example creates a resource group with the name *myResourceGroup* in the *eastus* region.</span></span> <span data-ttu-id="6f9b5-153">輸入您自己的值，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="6f9b5-153">Enter your own values as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="6f9b5-154">Azure CLI 會在建立部署後幾秒鐘內讓您回到提示，但是安裝和設定需要一個小時以上才能完成。</span><span class="sxs-lookup"><span data-stu-id="6f9b5-154">The Azure CLI returns you to a prompt within a few seconds of creating the deployment, but the installation and configuration can take over an hour to complete.</span></span> <span data-ttu-id="6f9b5-155">使用 `azure group deployment show myResourceGroup` 檢查部署狀態，據以調整資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="6f9b5-155">Check the status of the deployment with `azure group deployment show myResourceGroup`, adjusting the name of your resource group accordingly.</span></span> <span data-ttu-id="6f9b5-156">等到 ProvisioningState 顯示 Succeeded 後，再連線到 VM。</span><span class="sxs-lookup"><span data-stu-id="6f9b5-156">Wait until the **ProvisioningState** shows *Succeeded* before connecting to the VMs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6f9b5-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6f9b5-157">Next steps</span></span>
<span data-ttu-id="6f9b5-158">在這些範例中，您會從 VM 本機連線到 MongoDB 執行個體。</span><span class="sxs-lookup"><span data-stu-id="6f9b5-158">In these examples, you connect to the MongoDB instance locally from the VM.</span></span> <span data-ttu-id="6f9b5-159">如果您想要從另一個 VM 或網路連線到 MongoDB 執行個體，請確定建立適當的[網路安全性群組規則](nsg-quickstart.md)。</span><span class="sxs-lookup"><span data-stu-id="6f9b5-159">If you want to connect to the MongoDB instance from another VM or network, ensure the appropriate [Network Security Group rules are created](nsg-quickstart.md).</span></span>

<span data-ttu-id="6f9b5-160">如需關於建立範本的詳細資訊，請參閱 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="6f9b5-160">For more information about creating using templates, see the [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="6f9b5-161">Azure Resource Manager 範本會使用自訂指令碼延伸模組，在您的 VM 上下載並執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="6f9b5-161">The Azure Resource Manager templates use the Custom Script Extension to download and execute scripts on your VMs.</span></span> <span data-ttu-id="6f9b5-162">如需詳細資訊，請參閱[搭配 Linux 虛擬機器使用 Azure 自訂指令碼擴充功能](extensions-customscript.md)。</span><span class="sxs-lookup"><span data-stu-id="6f9b5-162">For more information, see [Using the Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span></span>

