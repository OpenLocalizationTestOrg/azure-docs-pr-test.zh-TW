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
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm-using-hello-azure-cli-10"></a><span data-ttu-id="74873-103">如何 tooinstall 及使用 Azure CLI 1.0 hello Linux VM 上設定 MongoDB</span><span class="sxs-lookup"><span data-stu-id="74873-103">How tooinstall and configure MongoDB on a Linux VM using hello Azure CLI 1.0</span></span>
<span data-ttu-id="74873-104">[MongoDB](http://www.mongodb.org) 是受歡迎的高效能開放原始碼 NoSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="74873-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="74873-105">本文章將示範如何 tooinstall 及使用 hello Resource Manager 部署模型在 Azure 中 Linux VM 上設定 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="74873-105">This article shows you how tooinstall and configure MongoDB on a Linux VM in Azure using hello Resource Manager deployment model.</span></span> <span data-ttu-id="74873-106">範例會詳細說明如何︰</span><span class="sxs-lookup"><span data-stu-id="74873-106">Examples are shown that detail how to:</span></span>

* [<span data-ttu-id="74873-107">手動安裝及設定基本 MongoDB 執行個體</span><span class="sxs-lookup"><span data-stu-id="74873-107">Manually install and configure a basic MongoDB instance</span></span>](#manually-install-and-configure-mongodb-on-a-vm)
* [<span data-ttu-id="74873-108">使用 Resource Manager 範本建立基本 MongoDB 執行個體</span><span class="sxs-lookup"><span data-stu-id="74873-108">Create a basic MongoDB instance using a Resource Manager template</span></span>](#create-basic-mongodb-instance-on-centos-using-a-template)
* [<span data-ttu-id="74873-109">使用 Resource Manager 範本建立複雜的 MongoDB 分區化叢集與複本集</span><span class="sxs-lookup"><span data-stu-id="74873-109">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span></span>](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="74873-110">CLI 版本 toocomplete hello 工作</span><span class="sxs-lookup"><span data-stu-id="74873-110">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="74873-111">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：</span><span class="sxs-lookup"><span data-stu-id="74873-111">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="74873-112">Azure CLI 1.0 – 我們 CLI hello 傳統和資源管理部署模型 （此文件）</span><span class="sxs-lookup"><span data-stu-id="74873-112">Azure CLI 1.0 – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="74873-113">[Azure CLI 2.0](create-cli-complete-nodejs.md) -hello 資源管理部署模型我們下一個層代 CLI</span><span class="sxs-lookup"><span data-stu-id="74873-113">[Azure CLI 2.0](create-cli-complete-nodejs.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="74873-114">在 VM 上手動安裝及設定 MongoDB</span><span class="sxs-lookup"><span data-stu-id="74873-114">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="74873-115">MongoDB [提供 Linux 散發版本的安裝指示](https://docs.mongodb.com/manual/administration/install-on-linux/)，包括 Red Hat / CentOS、SUSE、Ubuntu 和 Debian。</span><span class="sxs-lookup"><span data-stu-id="74873-115">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="74873-116">hello 下列範例會建立*CentOS* VM 使用 SSH 金鑰儲存在*~/.ssh/id_rsa.pub*。</span><span class="sxs-lookup"><span data-stu-id="74873-116">hello following example creates a *CentOS* VM using an SSH key stored at *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="74873-117">回應 hello 提示您輸入儲存體帳戶名稱、 DNS 名稱和管理員認證：</span><span class="sxs-lookup"><span data-stu-id="74873-117">Answer hello prompts for storage account name, DNS name, and admin credentials:</span></span>

```azurecli
azure vm quick-create \
    --image-urn CentOS \
    --ssh-publickey-file ~/.ssh/id_rsa.pub 
```

<span data-ttu-id="74873-118">登入 toohello VM 使用 hello 結尾 hello hello 前面 VM 建立步驟顯示公用 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="74873-118">Log on toohello VM using hello public IP address displayed at hello end of hello preceding VM creation step:</span></span>

```bash
ssh azureuser@40.78.23.145
```

<span data-ttu-id="74873-119">tooadd hello 安裝來源的 MongoDB，建立**yum**儲存機制檔案，如下所示：</span><span class="sxs-lookup"><span data-stu-id="74873-119">tooadd hello installation sources for MongoDB, create a **yum** repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

<span data-ttu-id="74873-120">開啟 hello MongoDB 儲存機制檔案進行編輯。</span><span class="sxs-lookup"><span data-stu-id="74873-120">Open hello MongoDB repo file for editing.</span></span> <span data-ttu-id="74873-121">加入下列行 hello:</span><span class="sxs-lookup"><span data-stu-id="74873-121">Add hello following lines:</span></span>

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

<span data-ttu-id="74873-122">使用 yum 安裝 MongoDB，如下所示：</span><span class="sxs-lookup"><span data-stu-id="74873-122">Install MongoDB using **yum** as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="74873-123">依預設，會在可防止您存取 MongoDB 的 CentOS 映像上強制採用 SELinux。</span><span class="sxs-lookup"><span data-stu-id="74873-123">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="74873-124">原則管理工具上安裝及設定 SELinux tooallow MongoDB toooperate 預設 TCP 通訊埠 27017，如下所示。</span><span class="sxs-lookup"><span data-stu-id="74873-124">Install policy management tools and configure SELinux tooallow MongoDB toooperate on its default TCP port 27017 as follows.</span></span> 

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="74873-125">啟動 hello MongoDB 服務，如下所示：</span><span class="sxs-lookup"><span data-stu-id="74873-125">Start hello MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="74873-126">藉由連接使用 hello 本機驗證 hello MongoDB 安裝`mongo`用戶端：</span><span class="sxs-lookup"><span data-stu-id="74873-126">Verify hello MongoDB installation by connecting using hello local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="74873-127">現在加入一些資料，及搜尋測試 hello MongoDB 執行個體：</span><span class="sxs-lookup"><span data-stu-id="74873-127">Now test hello MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="74873-128">如有需要，MongoDB toostart 自動設定系統重新開機期間：</span><span class="sxs-lookup"><span data-stu-id="74873-128">If desired, configure MongoDB toostart automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="74873-129">使用範本在 CentOS 上建立基本 MongoDB 執行個體</span><span class="sxs-lookup"><span data-stu-id="74873-129">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="74873-130">您可以在單一的 CentOS vm 使用 hello GitHub 中的下列 Azure 快速入門範本建立基本的 MongoDB 執行個體。</span><span class="sxs-lookup"><span data-stu-id="74873-130">You can create a basic MongoDB instance on a single CentOS VM using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="74873-131">此範本使用 hello 自訂指令碼擴充功能的 Linux tooadd`yum`儲存機制 tooyour 新建立的 CentOS VM，然後再安裝 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="74873-131">This template uses hello Custom Script extension for Linux tooadd a `yum` repository tooyour newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="74873-132">[CentOS 上的基本 MongoDB 執行個體](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="74873-132">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="74873-133">hello 下列範例會建立資源群組名稱 hello`myResourceGroup`在 hello`eastus`區域。</span><span class="sxs-lookup"><span data-stu-id="74873-133">hello following example creates a resource group with hello name `myResourceGroup` in hello `eastus` region.</span></span> <span data-ttu-id="74873-134">輸入您自己的值，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="74873-134">Enter your own values as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="74873-135">hello Azure CLI 傳回您 tooa 提示字元建立 hello 部署，但 hello 安裝在幾秒鐘內，並組態採用幾分鐘的時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="74873-135">hello Azure CLI returns you tooa prompt within a few seconds of creating hello deployment, but hello installation and configuration takes a few minutes toocomplete.</span></span> <span data-ttu-id="74873-136">檢查與 hello 部署的 hello 狀態`azure group deployment show myResourceGroup`，據此輸入 hello 的資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="74873-136">Check hello status of hello deployment with `azure group deployment show myResourceGroup`, entering hello name of your resource group accordingly.</span></span> <span data-ttu-id="74873-137">等候直到在 hello **ProvisioningState**顯示*Succeeded*之前嘗試 tooSSH toohello VM。</span><span class="sxs-lookup"><span data-stu-id="74873-137">Wait until hello **ProvisioningState** shows *Succeeded* before trying tooSSH toohello VM.</span></span>

<span data-ttu-id="74873-138">一旦 hello 部署完成，SSH toohello VM。</span><span class="sxs-lookup"><span data-stu-id="74873-138">Once hello deployment is complete, SSH toohello VM.</span></span> <span data-ttu-id="74873-139">取得 hello IP 位址，您的 VM 使用 hello`azure vm show`命令如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="74873-139">Obtain hello IP address of your VM using hello `azure vm show` command as in hello following example:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myLinuxVM
```

<span data-ttu-id="74873-140">接近 hello hello 輸出結尾，會顯示 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="74873-140">Near hello end of hello output, hello public IP address is displayed.</span></span> <span data-ttu-id="74873-141">SSH tooyour VM hello IP 位址，為您的 VM:</span><span class="sxs-lookup"><span data-stu-id="74873-141">SSH tooyour VM with hello IP address of your VM:</span></span>

```bash
ssh azureuser@138.91.149.74
```

<span data-ttu-id="74873-142">藉由連接使用 hello 本機驗證 hello MongoDB 安裝`mongo`用戶端，如下所示：</span><span class="sxs-lookup"><span data-stu-id="74873-142">Verify hello MongoDB installation by connecting using hello local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="74873-143">現在測試 hello 執行個體加入一些資料，並搜尋，如下所示：</span><span class="sxs-lookup"><span data-stu-id="74873-143">Now test hello instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="74873-144">使用範本在 CentOS 上建立複雜的 MongoDB 分區化叢集</span><span class="sxs-lookup"><span data-stu-id="74873-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="74873-145">您可以建立複雜的 MongoDB 分區化叢集中，並使用 hello GitHub 中的下列 Azure 快速入門範本。</span><span class="sxs-lookup"><span data-stu-id="74873-145">You can create a complex MongoDB sharded cluster using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="74873-146">此範本會遵循 hello [MongoDB 分區化叢集的最佳作法](https://docs.mongodb.com/manual/core/sharded-cluster-components/)tooprovide 備援性和高可用性。</span><span class="sxs-lookup"><span data-stu-id="74873-146">This template follows hello [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide redundancy and high availability.</span></span> <span data-ttu-id="74873-147">hello 範本會建立兩個分區，其中每個複本組中的三個節點。</span><span class="sxs-lookup"><span data-stu-id="74873-147">hello template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="74873-148">一個具有三個節點設定的組態伺服器複本也會建立，再加上兩個**mongos**路由器伺服器 tooprovide 一致性 tooapplications 從跨 hello 分區。</span><span class="sxs-lookup"><span data-stu-id="74873-148">One config server replica set with three nodes is also created, plus two **mongos** router servers tooprovide consistency tooapplications from across hello shards.</span></span>

* <span data-ttu-id="74873-149">[CentOS 上的 MongoDB 分區化叢集](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="74873-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="74873-150">部署這個複雜的 MongoDB 分區化的叢集需要超過 20 個核心，通常是每個訂用帳戶的區域 hello 預設核心計數。</span><span class="sxs-lookup"><span data-stu-id="74873-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically hello default core count per region for a subscription.</span></span> <span data-ttu-id="74873-151">開啟 Azure 支援人員要求 tooincrease 核心計數。</span><span class="sxs-lookup"><span data-stu-id="74873-151">Open an Azure support request tooincrease your core count.</span></span>

<span data-ttu-id="74873-152">hello 下列範例會建立資源群組名稱 hello *myResourceGroup*在 hello *eastus*區域。</span><span class="sxs-lookup"><span data-stu-id="74873-152">hello following example creates a resource group with hello name *myResourceGroup* in hello *eastus* region.</span></span> <span data-ttu-id="74873-153">輸入您自己的值，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="74873-153">Enter your own values as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="74873-154">hello Azure CLI 傳回您 tooa 提示字元建立 hello 部署的幾秒內，但 hello 安裝和設定可能會花費小時 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="74873-154">hello Azure CLI returns you tooa prompt within a few seconds of creating hello deployment, but hello installation and configuration can take over an hour toocomplete.</span></span> <span data-ttu-id="74873-155">檢查與 hello 部署的 hello 狀態`azure group deployment show myResourceGroup`，據此調整 hello 的資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="74873-155">Check hello status of hello deployment with `azure group deployment show myResourceGroup`, adjusting hello name of your resource group accordingly.</span></span> <span data-ttu-id="74873-156">等候直到在 hello **ProvisioningState**顯示*Succeeded*之前 toohello Vm 連線。</span><span class="sxs-lookup"><span data-stu-id="74873-156">Wait until hello **ProvisioningState** shows *Succeeded* before connecting toohello VMs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="74873-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="74873-157">Next steps</span></span>
<span data-ttu-id="74873-158">在這些範例中，您連接 toohello MongoDB 執行個體在本機從 hello VM。</span><span class="sxs-lookup"><span data-stu-id="74873-158">In these examples, you connect toohello MongoDB instance locally from hello VM.</span></span> <span data-ttu-id="74873-159">如果您想從其他 VM 或網路 tooconnect toohello MongoDB 執行個體，請確定適當的 hello[會建立網路安全性群組規則](nsg-quickstart.md)。</span><span class="sxs-lookup"><span data-stu-id="74873-159">If you want tooconnect toohello MongoDB instance from another VM or network, ensure hello appropriate [Network Security Group rules are created](nsg-quickstart.md).</span></span>

<span data-ttu-id="74873-160">如需有關如何使用範本建立的詳細資訊，請參閱 hello [Azure 資源管理員概觀](../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="74873-160">For more information about creating using templates, see hello [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="74873-161">hello Azure Resource Manager 範本使用 hello 自訂指令碼擴充 toodownload，並在您的 Vm 上執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="74873-161">hello Azure Resource Manager templates use hello Custom Script Extension toodownload and execute scripts on your VMs.</span></span> <span data-ttu-id="74873-162">如需詳細資訊，請參閱[使用 hello Azure 自訂指令碼延伸與 Linux 虛擬機器](extensions-customscript.md)。</span><span class="sxs-lookup"><span data-stu-id="74873-162">For more information, see [Using hello Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span></span>

