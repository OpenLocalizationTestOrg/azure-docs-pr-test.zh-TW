---
title: "aaaHow toocreate Linux Azure VM 映像與 Packer |Microsoft 文件"
description: "深入了解如何在 Azure 中 Linux 虛擬機器的 toouse Packer toocreate 映像"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/18/2017
ms.author: iainfou
ms.openlocfilehash: 5990598859e73efac477884bc8de5fd5138bf6e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-packer-toocreate-linux-virtual-machine-images-in-azure"></a><span data-ttu-id="2f7bd-103">Toouse Packer toocreate Linux 虛擬機器在 Azure 中的映像</span><span class="sxs-lookup"><span data-stu-id="2f7bd-103">How toouse Packer toocreate Linux virtual machine images in Azure</span></span>
<span data-ttu-id="2f7bd-104">在 Azure 中的每個虛擬機器 (VM) 是從定義 hello Linux 發行版本和作業系統版本的映像建立。</span><span class="sxs-lookup"><span data-stu-id="2f7bd-104">Each virtual machine (VM) in Azure is created from an image that defines hello Linux distribution and OS version.</span></span> <span data-ttu-id="2f7bd-105">映像中可包含預先安裝的應用程式與組態。</span><span class="sxs-lookup"><span data-stu-id="2f7bd-105">Images can include pre-installed applications and configurations.</span></span> <span data-ttu-id="2f7bd-106">hello Azure Marketplace 提供許多的第一個和第三方映像的最常見的分佈和應用程式環境，或您可以建立您自己的自訂映像，量身訂做 tooyour 需求。</span><span class="sxs-lookup"><span data-stu-id="2f7bd-106">hello Azure Marketplace provides many first and third-party images for most common distributions and application environments, or you can create your own custom images tailored tooyour needs.</span></span> <span data-ttu-id="2f7bd-107">這篇文章說明如何 toouse hello 開啟原始碼工具[Packer](https://www.packer.io/) toodefine 和建置在 Azure 中的自訂影像。</span><span class="sxs-lookup"><span data-stu-id="2f7bd-107">This article details how toouse hello open source tool [Packer](https://www.packer.io/) toodefine and build custom images in Azure.</span></span>


## <a name="create-azure-resource-group"></a><span data-ttu-id="2f7bd-108">建立 Azure 資源群組</span><span class="sxs-lookup"><span data-stu-id="2f7bd-108">Create Azure resource group</span></span>
<span data-ttu-id="2f7bd-109">在 hello 建置過程中，Packer 會建立暫存的 Azure 資源，當它建立 hello 來源 VM。</span><span class="sxs-lookup"><span data-stu-id="2f7bd-109">During hello build process, Packer creates temporary Azure resources as it builds hello source VM.</span></span> <span data-ttu-id="2f7bd-110">來源 VM 用作映像的 toocapture，您必須定義的資源群組。</span><span class="sxs-lookup"><span data-stu-id="2f7bd-110">toocapture that source VM for use as an image, you must define a resource group.</span></span> <span data-ttu-id="2f7bd-111">hello hello Packer 建置程序的輸出會儲存在此資源群組。</span><span class="sxs-lookup"><span data-stu-id="2f7bd-111">hello output from hello Packer build process is stored in this resource group.</span></span>

<span data-ttu-id="2f7bd-112">使用 [az group create](/cli/azure/group#create) 來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="2f7bd-112">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="2f7bd-113">hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置：</span><span class="sxs-lookup"><span data-stu-id="2f7bd-113">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create -n myResourceGroup -l eastus
```


## <a name="create-azure-credentials"></a><span data-ttu-id="2f7bd-114">建立 Azure 認證</span><span class="sxs-lookup"><span data-stu-id="2f7bd-114">Create Azure credentials</span></span>
<span data-ttu-id="2f7bd-115">Packer 會使用服務主體來向 Azure 驗證。</span><span class="sxs-lookup"><span data-stu-id="2f7bd-115">Packer authenticates with Azure using a service principal.</span></span> <span data-ttu-id="2f7bd-116">Azure 服務主體是安全性識別，可供您與應用程式、服務及諸如 Packer 等自動化工具搭配使用。</span><span class="sxs-lookup"><span data-stu-id="2f7bd-116">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Packer.</span></span> <span data-ttu-id="2f7bd-117">您可以控制和定義 hello 權限，如 toowhat 作業 hello 服務主體可以在 Azure 中執行。</span><span class="sxs-lookup"><span data-stu-id="2f7bd-117">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span>

<span data-ttu-id="2f7bd-118">建立服務主體與[az ad 預存程序建立-如-rbac](/cli/azure/ad/sp#create-for-rbac)和 Packer 需要輸出 hello 認證：</span><span class="sxs-lookup"><span data-stu-id="2f7bd-118">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output hello credentials that Packer needs:</span></span>

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

<span data-ttu-id="2f7bd-119">從上述命令 hello hello 輸出的範例如下所示：</span><span class="sxs-lookup"><span data-stu-id="2f7bd-119">An example of hello output from hello preceding commands is as follows:</span></span>

```azurecli
"f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
"0e760437-bf34-4aad-9f8d-870be799c55d",
"72f988bf-86f1-41af-91ab-2d7cd011db47"
```

<span data-ttu-id="2f7bd-120">tooauthenticate tooAzure，您也需要您的 Azure 訂用帳戶 ID 與 tooobtain [az 帳戶顯示](/cli/azure/account#show):</span><span class="sxs-lookup"><span data-stu-id="2f7bd-120">tooauthenticate tooAzure, you also need tooobtain your Azure subscription ID with [az account show](/cli/azure/account#show):</span></span>

```azurecli
az account show --query [id] --output tsv
```

<span data-ttu-id="2f7bd-121">您可以使用這兩個命令 hello 輸出 hello 下一個步驟中。</span><span class="sxs-lookup"><span data-stu-id="2f7bd-121">You use hello output from these two commands in hello next step.</span></span>


## <a name="define-packer-template"></a><span data-ttu-id="2f7bd-122">定義 Packer 範本</span><span class="sxs-lookup"><span data-stu-id="2f7bd-122">Define Packer template</span></span>
<span data-ttu-id="2f7bd-123">toobuild 映像，您會建立範本成為 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="2f7bd-123">toobuild images, you create a template as a JSON file.</span></span> <span data-ttu-id="2f7bd-124">Hello 範本中定義產生器和 provisioners hello 實際執行的建置程序。</span><span class="sxs-lookup"><span data-stu-id="2f7bd-124">In hello template, you define builders and provisioners that carry out hello actual build process.</span></span> <span data-ttu-id="2f7bd-125">具有 packer [provisioner azure](https://www.packer.io/docs/builders/azure.html) ，可讓您 toodefine Azure 資源，例如 hello 服務主體認證 hello 前面步驟中建立。</span><span class="sxs-lookup"><span data-stu-id="2f7bd-125">Packer has a [provisioner for Azure](https://www.packer.io/docs/builders/azure.html) that allows you toodefine Azure resources, such as hello service principal credentials created in hello preceding step.</span></span>

<span data-ttu-id="2f7bd-126">建立名為*ubuntu.json*和 hello 貼上下列內容。</span><span class="sxs-lookup"><span data-stu-id="2f7bd-126">Create a file named *ubuntu.json* and paste hello following content.</span></span> <span data-ttu-id="2f7bd-127">輸入您自己的值為 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="2f7bd-127">Enter your own values for hello following:</span></span>

| <span data-ttu-id="2f7bd-128">參數</span><span class="sxs-lookup"><span data-stu-id="2f7bd-128">Parameter</span></span>                           | <span data-ttu-id="2f7bd-129">其中 tooobtain</span><span class="sxs-lookup"><span data-stu-id="2f7bd-129">Where tooobtain</span></span> |
|-------------------------------------|----------------------------------------------------|
| <span data-ttu-id="2f7bd-130">client_id</span><span class="sxs-lookup"><span data-stu-id="2f7bd-130">*client_id*</span></span>                         | <span data-ttu-id="2f7bd-131">`az ad sp` 建立命令所產生之輸出的第一行 - appId</span><span class="sxs-lookup"><span data-stu-id="2f7bd-131">First line of output from `az ad sp` create command - *appId*</span></span> |
| <span data-ttu-id="2f7bd-132">client_secret</span><span class="sxs-lookup"><span data-stu-id="2f7bd-132">*client_secret*</span></span>                     | <span data-ttu-id="2f7bd-133">`az ad sp` 建立命令所產生之輸出的第二行 - password</span><span class="sxs-lookup"><span data-stu-id="2f7bd-133">Second line of output from `az ad sp` create command - *password*</span></span> |
| <span data-ttu-id="2f7bd-134">tenant_id</span><span class="sxs-lookup"><span data-stu-id="2f7bd-134">*tenant_id*</span></span>                         | <span data-ttu-id="2f7bd-135">`az ad sp` 建立命令所產生之輸出的第三行 - tenant</span><span class="sxs-lookup"><span data-stu-id="2f7bd-135">Third line of output from `az ad sp` create command - *tenant*</span></span> |
| <span data-ttu-id="2f7bd-136">subscription_id</span><span class="sxs-lookup"><span data-stu-id="2f7bd-136">*subscription_id*</span></span>                   | <span data-ttu-id="2f7bd-137">`az account show` 命令所產生的輸出</span><span class="sxs-lookup"><span data-stu-id="2f7bd-137">Output from `az account show` command</span></span> |
| <span data-ttu-id="2f7bd-138">managed_image_resource_group_name</span><span class="sxs-lookup"><span data-stu-id="2f7bd-138">*managed_image_resource_group_name*</span></span> | <span data-ttu-id="2f7bd-139">您在 hello 第一個步驟中建立的資源群組名稱</span><span class="sxs-lookup"><span data-stu-id="2f7bd-139">Name of resource group you created in hello first step</span></span> |
| <span data-ttu-id="2f7bd-140">managed_image_name</span><span class="sxs-lookup"><span data-stu-id="2f7bd-140">*managed_image_name*</span></span>                | <span data-ttu-id="2f7bd-141">建立 hello 受管理的磁碟映像的名稱</span><span class="sxs-lookup"><span data-stu-id="2f7bd-141">Name for hello managed disk image that is created</span></span> |


```json
{
  "builders": [{
    "type": "azure-arm",

    "client_id": "f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
    "client_secret": "0e760437-bf34-4aad-9f8d-870be799c55d",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "subscription_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx",

    "managed_image_resource_group_name": "myResourceGroup",
    "managed_image_name": "myPackerImage",

    "os_type": "Linux",
    "image_publisher": "Canonical",
    "image_offer": "UbuntuServer",
    "image_sku": "16.04-LTS",

    "azure_tags": {
        "dept": "Engineering",
        "task": "Image deployment"
    },

    "location": "East US",
    "vm_size": "Standard_DS2_v2"
  }],
  "provisioners": [{
    "execute_command": "chmod +x {{ .Path }}; {{ .Vars }} sudo -E sh '{{ .Path }}'",
    "inline": [
      "apt-get update",
      "apt-get upgrade -y",
      "apt-get -y install nginx",

      "/usr/sbin/waagent -force -deprovision+user && export HISTSIZE=0 && sync"
    ],
    "inline_shebang": "/bin/sh -x",
    "type": "shell"
  }]
}
```

<span data-ttu-id="2f7bd-142">此範本建置 Ubuntu 16.04 LTS 映像，請安裝 NGINX，然後 deprovisions hello VM。</span><span class="sxs-lookup"><span data-stu-id="2f7bd-142">This template builds an Ubuntu 16.04 LTS image, installs NGINX, then deprovisions hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="2f7bd-143">如果您展開此範本 tooprovision 使用者認證時，調整 hello provisioner 命令 deprovisions hello Azure 代理程式 tooread`-deprovision`而不是`deprovision+user`。</span><span class="sxs-lookup"><span data-stu-id="2f7bd-143">If you expand on this template tooprovision user credentials, adjust hello provisioner command that deprovisions hello Azure agent tooread `-deprovision` rather than `deprovision+user`.</span></span>
> <span data-ttu-id="2f7bd-144">hello`+user`旗標移除 hello 來源 VM 中的所有使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="2f7bd-144">hello `+user` flag removes all user accounts from hello source VM.</span></span>


## <a name="build-packer-image"></a><span data-ttu-id="2f7bd-145">建置 Packer 映像</span><span class="sxs-lookup"><span data-stu-id="2f7bd-145">Build Packer image</span></span>
<span data-ttu-id="2f7bd-146">如果您還沒有安裝在本機電腦上的 Packer[依照 hello Packer 安裝指示](https://www.packer.io/docs/install/index.html)。</span><span class="sxs-lookup"><span data-stu-id="2f7bd-146">If you don't already have Packer installed on your local machine, [follow hello Packer installation instructions](https://www.packer.io/docs/install/index.html).</span></span>

<span data-ttu-id="2f7bd-147">建立 hello 映像藉由指定您 Packer 範本檔案，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2f7bd-147">Build hello image by specifying your Packer template file as follows:</span></span>

```bash
./packer build ubuntu.json
```

<span data-ttu-id="2f7bd-148">從上述命令 hello hello 輸出的範例如下所示：</span><span class="sxs-lookup"><span data-stu-id="2f7bd-148">An example of hello output from hello preceding commands is as follows:</span></span>

```bash
azure-arm output will be in this color.

==> azure-arm: Running builder ...
    azure-arm: Creating Azure Resource Manager (ARM) client ...
==> azure-arm: Creating resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Location          : ‘East US’
==> azure-arm:  -> Tags              :
==> azure-arm:  ->> dept : Engineering
==> azure-arm:  ->> task : Image deployment
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Getting hello VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.218.147’
==> azure-arm: Waiting for SSH toobecome available...
==> azure-arm: Connected tooSSH!
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-shell868574263
    azure-arm: WARNING! hello waagent service will be stopped.
    azure-arm: WARNING! Cached DHCP leases will be deleted.
    azure-arm: WARNING! root password will be disabled. You will not be able toologin as root.
    azure-arm: WARNING! /etc/resolvconf/resolv.conf.d/tail and /etc/resolvconf/resolv.conf.d/original will be deleted.
    azure-arm: WARNING! packer account and entire home directory will be deleted.
==> azure-arm: Querying hello machine’s properties ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Managed OS Disk   : ‘/subscriptions/guid/resourceGroups/packer-Resource-Group-swtxmqm7ly/providers/Microsoft.Compute/disks/osdisk’
==> azure-arm: Powering off machine ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm: Capturing image ...
==> azure-arm:  -> Compute ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Compute Name              : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Compute Location          : ‘East US’
==> azure-arm:  -> Image ResourceGroupName   : ‘myResourceGroup’
==> azure-arm:  -> Image Name                : ‘myPackerImage’
==> azure-arm:  -> Image Location            : ‘eastus’
==> azure-arm: Deleting resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm: Deleting hello temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. hello artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```


## <a name="create-vm-from-azure-image"></a><span data-ttu-id="2f7bd-149">從 Azure 映像建立 VM</span><span class="sxs-lookup"><span data-stu-id="2f7bd-149">Create VM from Azure Image</span></span>
<span data-ttu-id="2f7bd-150">您現在可以使用 [az vm create](/cli/azure/vm#create) 從您的映像建立 VM。</span><span class="sxs-lookup"><span data-stu-id="2f7bd-150">You can now create a VM from your Image with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="2f7bd-151">指定您建立以 hello 映像 hello`--image`參數。</span><span class="sxs-lookup"><span data-stu-id="2f7bd-151">Specify hello Image you created with hello `--image` parameter.</span></span> <span data-ttu-id="2f7bd-152">hello 下列範例會建立名為的 VM *myVM*從*myPackerImage*並產生 SSH 金鑰，如果它們尚不存在：</span><span class="sxs-lookup"><span data-stu-id="2f7bd-152">hello following example creates a VM named *myVM* from *myPackerImage* and generates SSH keys if they do not already exist:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image myPackerImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="2f7bd-153">花幾分鐘的時間 toocreate hello VM。</span><span class="sxs-lookup"><span data-stu-id="2f7bd-153">It takes a few minutes toocreate hello VM.</span></span> <span data-ttu-id="2f7bd-154">一旦建立 hello VM 之後，記下 hello`publicIpAddress`顯示 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="2f7bd-154">Once hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="2f7bd-155">這個位址是透過 web 瀏覽器使用的 tooaccess hello NGINX 站台。</span><span class="sxs-lookup"><span data-stu-id="2f7bd-155">This address is used tooaccess hello NGINX site via a web browser.</span></span>

<span data-ttu-id="2f7bd-156">tooallow web 流量 tooreach VM，開啟的通訊埠 80 hello 網際網路從[az vm 開啟通訊埠](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="2f7bd-156">tooallow web traffic tooreach your VM, open port 80 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli
az vm open-port \
    --resource-group myResourceGroup \
    --name myVM \
    --port 80
```

## <a name="test-vm-and-nginx"></a><span data-ttu-id="2f7bd-157">測試 VM 和 NGINX</span><span class="sxs-lookup"><span data-stu-id="2f7bd-157">Test VM and NGINX</span></span>
<span data-ttu-id="2f7bd-158">現在您可以開啟網頁瀏覽器並輸入`http://publicIpAddress`hello 網址列中。</span><span class="sxs-lookup"><span data-stu-id="2f7bd-158">Now you can open a web browser and enter `http://publicIpAddress` in hello address bar.</span></span> <span data-ttu-id="2f7bd-159">提供自己的公用 IP 位址從 hello VM 建立處理程序。</span><span class="sxs-lookup"><span data-stu-id="2f7bd-159">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="2f7bd-160">hello 預設 NGINX 網頁會顯示如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="2f7bd-160">hello default NGINX page is displayed as in hello following example:</span></span>

![預設 NGINX 網站](./media/build-image-with-packer/nginx.png) 


## <a name="next-steps"></a><span data-ttu-id="2f7bd-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2f7bd-162">Next steps</span></span>
<span data-ttu-id="2f7bd-163">在此範例中，您搭配 Packer toocreate VM 映像 NGINX 已經安裝。</span><span class="sxs-lookup"><span data-stu-id="2f7bd-163">In this example, you used Packer toocreate a VM image with NGINX already installed.</span></span> <span data-ttu-id="2f7bd-164">您可以使用現有的部署工作流程，例如從 hello Ansible、 Chef 或 Puppet 的映像建立的應用程式 tooVMs toodeploy 連同此 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="2f7bd-164">You can use this VM image alongside existing deployment workflows, such as toodeploy your app tooVMs created from hello Image with Ansible, Chef, or Puppet.</span></span>

<span data-ttu-id="2f7bd-165">如需其他 Linux 散發套件的其他 Packer 範本範例，請參閱[這個 GitHub 存放庫](https://github.com/hashicorp/packer/tree/master/examples/azure)。</span><span class="sxs-lookup"><span data-stu-id="2f7bd-165">For additional example Packer templates for other Linux distros, see [this GitHub repo](https://github.com/hashicorp/packer/tree/master/examples/azure).</span></span>