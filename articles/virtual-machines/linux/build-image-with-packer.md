---
title: "如何使用 Packer 來建立 Linux Azure VM 映像 | Microsoft Docs"
description: "了解如何在 Azure 中使用 Packer 建立 Linux 虛擬機器的映像"
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
ms.openlocfilehash: 49a74648bd3953647d581c4e7c548985c5000f17
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-packer-to-create-linux-virtual-machine-images-in-azure"></a><span data-ttu-id="1a371-103">如何在 Azure 中使用 Packer 來建立 Linux 虛擬機器映像</span><span class="sxs-lookup"><span data-stu-id="1a371-103">How to use Packer to create Linux virtual machine images in Azure</span></span>
<span data-ttu-id="1a371-104">Azure 中的每個虛擬機器 (VM) 都是透過映像所建立，而映像則會定義 Linux 散發套件和作業系統版本。</span><span class="sxs-lookup"><span data-stu-id="1a371-104">Each virtual machine (VM) in Azure is created from an image that defines the Linux distribution and OS version.</span></span> <span data-ttu-id="1a371-105">映像中可包含預先安裝的應用程式與組態。</span><span class="sxs-lookup"><span data-stu-id="1a371-105">Images can include pre-installed applications and configurations.</span></span> <span data-ttu-id="1a371-106">Azure Marketplace 提供了許多第一方和第三方映像，這些映像適用於最常見的散發套件和應用程式環境，而您也可以建立自己自訂的映像，以符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="1a371-106">The Azure Marketplace provides many first and third-party images for most common distributions and application environments, or you can create your own custom images tailored to your needs.</span></span> <span data-ttu-id="1a371-107">本文詳述如何使用開放原始碼工具 [Packer](https://www.packer.io/)，在 Azure 中定義並建置自訂映像。</span><span class="sxs-lookup"><span data-stu-id="1a371-107">This article details how to use the open source tool [Packer](https://www.packer.io/) to define and build custom images in Azure.</span></span>


## <a name="create-azure-resource-group"></a><span data-ttu-id="1a371-108">建立 Azure 資源群組</span><span class="sxs-lookup"><span data-stu-id="1a371-108">Create Azure resource group</span></span>
<span data-ttu-id="1a371-109">建置程序進行期間，Packer 會在建置來源 VM 時建立暫存的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="1a371-109">During the build process, Packer creates temporary Azure resources as it builds the source VM.</span></span> <span data-ttu-id="1a371-110">若要擷取該來源 VM 以作為映像，您必須定義資源群組。</span><span class="sxs-lookup"><span data-stu-id="1a371-110">To capture that source VM for use as an image, you must define a resource group.</span></span> <span data-ttu-id="1a371-111">Packer 建置程序所產生的輸出會儲存在此資源群組中。</span><span class="sxs-lookup"><span data-stu-id="1a371-111">The output from the Packer build process is stored in this resource group.</span></span>

<span data-ttu-id="1a371-112">使用 [az group create](/cli/azure/group#create) 來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="1a371-112">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="1a371-113">下列範例會在 eastus 位置建立名為 myResourceGroup 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="1a371-113">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create -n myResourceGroup -l eastus
```


## <a name="create-azure-credentials"></a><span data-ttu-id="1a371-114">建立 Azure 認證</span><span class="sxs-lookup"><span data-stu-id="1a371-114">Create Azure credentials</span></span>
<span data-ttu-id="1a371-115">Packer 會使用服務主體來向 Azure 驗證。</span><span class="sxs-lookup"><span data-stu-id="1a371-115">Packer authenticates with Azure using a service principal.</span></span> <span data-ttu-id="1a371-116">Azure 服務主體是安全性識別，可供您與應用程式、服務及諸如 Packer 等自動化工具搭配使用。</span><span class="sxs-lookup"><span data-stu-id="1a371-116">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Packer.</span></span> <span data-ttu-id="1a371-117">您可以控制和定義對於服務主體可以在 Azure 中執行哪些作業的權限。</span><span class="sxs-lookup"><span data-stu-id="1a371-117">You control and define the permissions as to what operations the service principal can perform in Azure.</span></span>

<span data-ttu-id="1a371-118">使用 [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) 建立服務主體，並將 Packer 所需的認證輸出：</span><span class="sxs-lookup"><span data-stu-id="1a371-118">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output the credentials that Packer needs:</span></span>

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

<span data-ttu-id="1a371-119">上述命令的輸出範例如下所示：</span><span class="sxs-lookup"><span data-stu-id="1a371-119">An example of the output from the preceding commands is as follows:</span></span>

```azurecli
"f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
"0e760437-bf34-4aad-9f8d-870be799c55d",
"72f988bf-86f1-41af-91ab-2d7cd011db47"
```

<span data-ttu-id="1a371-120">若要向 Azure 驗證，您也需要使用 [az account show](/cli/azure/account#show) 取得 Azure 訂用帳戶識別碼：</span><span class="sxs-lookup"><span data-stu-id="1a371-120">To authenticate to Azure, you also need to obtain your Azure subscription ID with [az account show](/cli/azure/account#show):</span></span>

```azurecli
az account show --query [id] --output tsv
```

<span data-ttu-id="1a371-121">您將在下一個步驟中使用這兩個命令的輸出。</span><span class="sxs-lookup"><span data-stu-id="1a371-121">You use the output from these two commands in the next step.</span></span>


## <a name="define-packer-template"></a><span data-ttu-id="1a371-122">定義 Packer 範本</span><span class="sxs-lookup"><span data-stu-id="1a371-122">Define Packer template</span></span>
<span data-ttu-id="1a371-123">若要建置映像，您可以將範本建立為 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="1a371-123">To build images, you create a template as a JSON file.</span></span> <span data-ttu-id="1a371-124">在此範本中，您必須定義產生器和佈建程式，由它們執行實際的建置程序。</span><span class="sxs-lookup"><span data-stu-id="1a371-124">In the template, you define builders and provisioners that carry out the actual build process.</span></span> <span data-ttu-id="1a371-125">Packer 具有[適用於 Azure 的佈建程式](https://www.packer.io/docs/builders/azure.html)，以供您定義 Azure 資源，例如上述步驟所建立的服務主體認證。</span><span class="sxs-lookup"><span data-stu-id="1a371-125">Packer has a [provisioner for Azure](https://www.packer.io/docs/builders/azure.html) that allows you to define Azure resources, such as the service principal credentials created in the preceding step.</span></span>

<span data-ttu-id="1a371-126">建立名為 ubuntu.json 的檔案，並貼入下列內容。</span><span class="sxs-lookup"><span data-stu-id="1a371-126">Create a file named *ubuntu.json* and paste the following content.</span></span> <span data-ttu-id="1a371-127">針對下列參數輸入您自己的值︰</span><span class="sxs-lookup"><span data-stu-id="1a371-127">Enter your own values for the following:</span></span>

| <span data-ttu-id="1a371-128">參數</span><span class="sxs-lookup"><span data-stu-id="1a371-128">Parameter</span></span>                           | <span data-ttu-id="1a371-129">取得位置</span><span class="sxs-lookup"><span data-stu-id="1a371-129">Where to obtain</span></span> |
|-------------------------------------|----------------------------------------------------|
| <span data-ttu-id="1a371-130">client_id</span><span class="sxs-lookup"><span data-stu-id="1a371-130">*client_id*</span></span>                         | <span data-ttu-id="1a371-131">`az ad sp` 建立命令所產生之輸出的第一行 - appId</span><span class="sxs-lookup"><span data-stu-id="1a371-131">First line of output from `az ad sp` create command - *appId*</span></span> |
| <span data-ttu-id="1a371-132">client_secret</span><span class="sxs-lookup"><span data-stu-id="1a371-132">*client_secret*</span></span>                     | <span data-ttu-id="1a371-133">`az ad sp` 建立命令所產生之輸出的第二行 - password</span><span class="sxs-lookup"><span data-stu-id="1a371-133">Second line of output from `az ad sp` create command - *password*</span></span> |
| <span data-ttu-id="1a371-134">tenant_id</span><span class="sxs-lookup"><span data-stu-id="1a371-134">*tenant_id*</span></span>                         | <span data-ttu-id="1a371-135">`az ad sp` 建立命令所產生之輸出的第三行 - tenant</span><span class="sxs-lookup"><span data-stu-id="1a371-135">Third line of output from `az ad sp` create command - *tenant*</span></span> |
| <span data-ttu-id="1a371-136">subscription_id</span><span class="sxs-lookup"><span data-stu-id="1a371-136">*subscription_id*</span></span>                   | <span data-ttu-id="1a371-137">`az account show` 命令所產生的輸出</span><span class="sxs-lookup"><span data-stu-id="1a371-137">Output from `az account show` command</span></span> |
| <span data-ttu-id="1a371-138">managed_image_resource_group_name</span><span class="sxs-lookup"><span data-stu-id="1a371-138">*managed_image_resource_group_name*</span></span> | <span data-ttu-id="1a371-139">您在第一個步驟中建立的資源群組名稱</span><span class="sxs-lookup"><span data-stu-id="1a371-139">Name of resource group you created in the first step</span></span> |
| <span data-ttu-id="1a371-140">managed_image_name</span><span class="sxs-lookup"><span data-stu-id="1a371-140">*managed_image_name*</span></span>                | <span data-ttu-id="1a371-141">所建立之受控磁碟映像的名稱</span><span class="sxs-lookup"><span data-stu-id="1a371-141">Name for the managed disk image that is created</span></span> |


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

<span data-ttu-id="1a371-142">此範本會建置 Ubuntu 16.04 LTS 映像、安裝 NGINX，然後取消佈建 VM。</span><span class="sxs-lookup"><span data-stu-id="1a371-142">This template builds an Ubuntu 16.04 LTS image, installs NGINX, then deprovisions the VM.</span></span>

> [!NOTE]
> <span data-ttu-id="1a371-143">如果您擴充此範本來佈建使用者認證，請將取消佈建 Azure 代理程式的佈建程式命令調整為讀取 `-deprovision` 而不是 `deprovision+user`。</span><span class="sxs-lookup"><span data-stu-id="1a371-143">If you expand on this template to provision user credentials, adjust the provisioner command that deprovisions the Azure agent to read `-deprovision` rather than `deprovision+user`.</span></span>
> <span data-ttu-id="1a371-144">`+user` 旗標會從來源 VM 中移除所有使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="1a371-144">The `+user` flag removes all user accounts from the source VM.</span></span>


## <a name="build-packer-image"></a><span data-ttu-id="1a371-145">建置 Packer 映像</span><span class="sxs-lookup"><span data-stu-id="1a371-145">Build Packer image</span></span>
<span data-ttu-id="1a371-146">如果您尚未在本機電腦上安裝 Packer，請[遵循 Packer 安裝指示](https://www.packer.io/docs/install/index.html)。</span><span class="sxs-lookup"><span data-stu-id="1a371-146">If you don't already have Packer installed on your local machine, [follow the Packer installation instructions](https://www.packer.io/docs/install/index.html).</span></span>

<span data-ttu-id="1a371-147">請指定 Packer 範本檔案來建置映像，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1a371-147">Build the image by specifying your Packer template file as follows:</span></span>

```bash
./packer build ubuntu.json
```

<span data-ttu-id="1a371-148">上述命令的輸出範例如下所示：</span><span class="sxs-lookup"><span data-stu-id="1a371-148">An example of the output from the preceding commands is as follows:</span></span>

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
==> azure-arm: Getting the VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.218.147’
==> azure-arm: Waiting for SSH to become available...
==> azure-arm: Connected to SSH!
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-shell868574263
    azure-arm: WARNING! The waagent service will be stopped.
    azure-arm: WARNING! Cached DHCP leases will be deleted.
    azure-arm: WARNING! root password will be disabled. You will not be able to login as root.
    azure-arm: WARNING! /etc/resolvconf/resolv.conf.d/tail and /etc/resolvconf/resolv.conf.d/original will be deleted.
    azure-arm: WARNING! packer account and entire home directory will be deleted.
==> azure-arm: Querying the machine’s properties ...
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
==> azure-arm: Deleting the temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. The artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```


## <a name="create-vm-from-azure-image"></a><span data-ttu-id="1a371-149">從 Azure 映像建立 VM</span><span class="sxs-lookup"><span data-stu-id="1a371-149">Create VM from Azure Image</span></span>
<span data-ttu-id="1a371-150">您現在可以使用 [az vm create](/cli/azure/vm#create) 從您的映像建立 VM。</span><span class="sxs-lookup"><span data-stu-id="1a371-150">You can now create a VM from your Image with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="1a371-151">指定您使用 `--image` 參數所建立的映像。</span><span class="sxs-lookup"><span data-stu-id="1a371-151">Specify the Image you created with the `--image` parameter.</span></span> <span data-ttu-id="1a371-152">下列範例會從 myPackerImage 建立名為 myVM 的 VM，並產生 SSH 金鑰 (如果您還未擁有這些金鑰的話)︰</span><span class="sxs-lookup"><span data-stu-id="1a371-152">The following example creates a VM named *myVM* from *myPackerImage* and generates SSH keys if they do not already exist:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image myPackerImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="1a371-153">建立 VM 需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="1a371-153">It takes a few minutes to create the VM.</span></span> <span data-ttu-id="1a371-154">在 VM 建立好之後，請記下 Azure CLI 所顯示的 `publicIpAddress`。</span><span class="sxs-lookup"><span data-stu-id="1a371-154">Once the VM has been created, take note of the `publicIpAddress` displayed by the Azure CLI.</span></span> <span data-ttu-id="1a371-155">此位址可用來透過 Web 瀏覽器存取 NGINX 網站。</span><span class="sxs-lookup"><span data-stu-id="1a371-155">This address is used to access the NGINX site via a web browser.</span></span>

<span data-ttu-id="1a371-156">若要讓 Web 流量到達您的 VM，請使用 [az vm open-port](/cli/azure/vm#open-port) 從網際網路開啟通訊埠 80：</span><span class="sxs-lookup"><span data-stu-id="1a371-156">To allow web traffic to reach your VM, open port 80 from the Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli
az vm open-port \
    --resource-group myResourceGroup \
    --name myVM \
    --port 80
```

## <a name="test-vm-and-nginx"></a><span data-ttu-id="1a371-157">測試 VM 和 NGINX</span><span class="sxs-lookup"><span data-stu-id="1a371-157">Test VM and NGINX</span></span>
<span data-ttu-id="1a371-158">現在，您可以開啟 Web 瀏覽器，並在網址列輸入 `http://publicIpAddress`。</span><span class="sxs-lookup"><span data-stu-id="1a371-158">Now you can open a web browser and enter `http://publicIpAddress` in the address bar.</span></span> <span data-ttu-id="1a371-159">提供您自己從 VM 建立程序中取得的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="1a371-159">Provide your own public IP address from the VM create process.</span></span> <span data-ttu-id="1a371-160">預設 NGINX 網頁即會顯示，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="1a371-160">The default NGINX page is displayed as in the following example:</span></span>

![預設 NGINX 網站](./media/build-image-with-packer/nginx.png) 


## <a name="next-steps"></a><span data-ttu-id="1a371-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1a371-162">Next steps</span></span>
<span data-ttu-id="1a371-163">在此範例中，您已使用 Packer 來建立已安裝 NGINX 的 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="1a371-163">In this example, you used Packer to create a VM image with NGINX already installed.</span></span> <span data-ttu-id="1a371-164">您可以使用這個 VM 映像以及現有的部署工作流程，來進行「將應用程式部署至使用 Ansible、Chef 或 Puppet 從映像所建立的 VM」之類的作業。</span><span class="sxs-lookup"><span data-stu-id="1a371-164">You can use this VM image alongside existing deployment workflows, such as to deploy your app to VMs created from the Image with Ansible, Chef, or Puppet.</span></span>

<span data-ttu-id="1a371-165">如需其他 Linux 散發套件的其他 Packer 範本範例，請參閱[這個 GitHub 存放庫](https://github.com/hashicorp/packer/tree/master/examples/azure)。</span><span class="sxs-lookup"><span data-stu-id="1a371-165">For additional example Packer templates for other Linux distros, see [this GitHub repo](https://github.com/hashicorp/packer/tree/master/examples/azure).</span></span>