---
title: "aaaHow toocreate Windows Azure VM 映像 Packer |Microsoft 文件"
description: "深入了解如何 toouse Packer toocreate 映像的 Windows Azure 中的虛擬機器"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/18/2017
ms.author: iainfou
ms.openlocfilehash: d310fae3becb453b52d21281cb8ac53fa14a3fc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-packer-toocreate-windows-virtual-machine-images-in-azure"></a><span data-ttu-id="2e53e-103">Toouse Packer toocreate Windows 虛擬機器在 Azure 中的映像</span><span class="sxs-lookup"><span data-stu-id="2e53e-103">How toouse Packer toocreate Windows virtual machine images in Azure</span></span>
<span data-ttu-id="2e53e-104">在 Azure 中的每個虛擬機器 (VM) 是從定義 hello Windows 發佈和作業系統版本的映像建立。</span><span class="sxs-lookup"><span data-stu-id="2e53e-104">Each virtual machine (VM) in Azure is created from an image that defines hello Windows distribution and OS version.</span></span> <span data-ttu-id="2e53e-105">映像中可包含預先安裝的應用程式與組態。</span><span class="sxs-lookup"><span data-stu-id="2e53e-105">Images can include pre-installed applications and configurations.</span></span> <span data-ttu-id="2e53e-106">hello Azure Marketplace 提供許多的第一個和第三方映像的最常見的作業系統和應用程式環境中，或者您可以建立您自己的自訂映像，量身訂做 tooyour 需求。</span><span class="sxs-lookup"><span data-stu-id="2e53e-106">hello Azure Marketplace provides many first and third-party images for most common OS' and application environments, or you can create your own custom images tailored tooyour needs.</span></span> <span data-ttu-id="2e53e-107">這篇文章說明如何 toouse hello 開啟原始碼工具[Packer](https://www.packer.io/) toodefine 和建置在 Azure 中的自訂影像。</span><span class="sxs-lookup"><span data-stu-id="2e53e-107">This article details how toouse hello open source tool [Packer](https://www.packer.io/) toodefine and build custom images in Azure.</span></span>


## <a name="create-azure-resource-group"></a><span data-ttu-id="2e53e-108">建立 Azure 資源群組</span><span class="sxs-lookup"><span data-stu-id="2e53e-108">Create Azure resource group</span></span>
<span data-ttu-id="2e53e-109">在 hello 建置過程中，Packer 會建立暫存的 Azure 資源，當它建立 hello 來源 VM。</span><span class="sxs-lookup"><span data-stu-id="2e53e-109">During hello build process, Packer creates temporary Azure resources as it builds hello source VM.</span></span> <span data-ttu-id="2e53e-110">來源 VM 用作映像的 toocapture，您必須定義的資源群組。</span><span class="sxs-lookup"><span data-stu-id="2e53e-110">toocapture that source VM for use as an image, you must define a resource group.</span></span> <span data-ttu-id="2e53e-111">hello hello Packer 建置程序的輸出會儲存在此資源群組。</span><span class="sxs-lookup"><span data-stu-id="2e53e-111">hello output from hello Packer build process is stored in this resource group.</span></span>

<span data-ttu-id="2e53e-112">使用 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="2e53e-112">Create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="2e53e-113">hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置：</span><span class="sxs-lookup"><span data-stu-id="2e53e-113">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```powershell
$rgName = "myResourceGroup"
$location = "East US"
New-AzureRmResourceGroup -Name $rgName -Location $location
```

## <a name="create-azure-credentials"></a><span data-ttu-id="2e53e-114">建立 Azure 認證</span><span class="sxs-lookup"><span data-stu-id="2e53e-114">Create Azure credentials</span></span>
<span data-ttu-id="2e53e-115">Packer 會使用服務主體來向 Azure 驗證。</span><span class="sxs-lookup"><span data-stu-id="2e53e-115">Packer authenticates with Azure using a service principal.</span></span> <span data-ttu-id="2e53e-116">Azure 服務主體是安全性識別，可供您與應用程式、服務及諸如 Packer 等自動化工具搭配使用。</span><span class="sxs-lookup"><span data-stu-id="2e53e-116">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Packer.</span></span> <span data-ttu-id="2e53e-117">您可以控制和定義 hello 權限，如 toowhat 作業 hello 服務主體可以在 Azure 中執行。</span><span class="sxs-lookup"><span data-stu-id="2e53e-117">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span>

<span data-ttu-id="2e53e-118">建立服務主體與[新增 AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal)為 hello 服務主體 toocreate 指派權限和管理資源[新增 AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment):</span><span class="sxs-lookup"><span data-stu-id="2e53e-118">Create a service principal with [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) and assign permissions for hello service principal toocreate and manage resources with [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment):</span></span>

```powershell
$sp = New-AzureRmADServicePrincipal -DisplayName "Azure Packer IKF" -Password "P@ssw0rd!"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="2e53e-119">tooauthenticate tooAzure，您也需要 tooobtain 與您 Azure 租用戶和訂用帳戶 Id [Get AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription):</span><span class="sxs-lookup"><span data-stu-id="2e53e-119">tooauthenticate tooAzure, you also need tooobtain your Azure tenant and subscription IDs with [Get-AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription):</span></span>

```powershell
$sub = Get-AzureRmSubscription
$sub.TenantId
$sub.SubscriptionId
```

<span data-ttu-id="2e53e-120">您可以使用下列兩個識別碼 hello 下一個步驟中。</span><span class="sxs-lookup"><span data-stu-id="2e53e-120">You use these two IDs in hello next step.</span></span>


## <a name="define-packer-template"></a><span data-ttu-id="2e53e-121">定義 Packer 範本</span><span class="sxs-lookup"><span data-stu-id="2e53e-121">Define Packer template</span></span>
<span data-ttu-id="2e53e-122">toobuild 映像，您會建立範本成為 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="2e53e-122">toobuild images, you create a template as a JSON file.</span></span> <span data-ttu-id="2e53e-123">Hello 範本中定義產生器和 provisioners hello 實際執行的建置程序。</span><span class="sxs-lookup"><span data-stu-id="2e53e-123">In hello template, you define builders and provisioners that carry out hello actual build process.</span></span> <span data-ttu-id="2e53e-124">具有 packer [provisioner azure](https://www.packer.io/docs/builders/azure.html) ，可讓您 toodefine Azure 資源，例如 hello 服務主體認證 hello 前面步驟中建立。</span><span class="sxs-lookup"><span data-stu-id="2e53e-124">Packer has a [provisioner for Azure](https://www.packer.io/docs/builders/azure.html) that allows you toodefine Azure resources, such as hello service principal credentials created in hello preceding step.</span></span>

<span data-ttu-id="2e53e-125">建立名為*windows.json*和 hello 貼上下列內容。</span><span class="sxs-lookup"><span data-stu-id="2e53e-125">Create a file named *windows.json* and paste hello following content.</span></span> <span data-ttu-id="2e53e-126">輸入您自己的值為 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="2e53e-126">Enter your own values for hello following:</span></span>

| <span data-ttu-id="2e53e-127">參數</span><span class="sxs-lookup"><span data-stu-id="2e53e-127">Parameter</span></span>                           | <span data-ttu-id="2e53e-128">其中 tooobtain</span><span class="sxs-lookup"><span data-stu-id="2e53e-128">Where tooobtain</span></span> |
|-------------------------------------|----------------------------------------------------|
| <span data-ttu-id="2e53e-129">client_id</span><span class="sxs-lookup"><span data-stu-id="2e53e-129">*client_id*</span></span>                         | <span data-ttu-id="2e53e-130">檢視具有 `$sp.applicationId` 的服務主體識別碼</span><span class="sxs-lookup"><span data-stu-id="2e53e-130">View service principal ID with `$sp.applicationId`</span></span> |
| <span data-ttu-id="2e53e-131">client_secret</span><span class="sxs-lookup"><span data-stu-id="2e53e-131">*client_secret*</span></span>                     | <span data-ttu-id="2e53e-132">您在 `$securePassword` 中指定的密碼</span><span class="sxs-lookup"><span data-stu-id="2e53e-132">Password you specified in `$securePassword`</span></span> |
| <span data-ttu-id="2e53e-133">tenant_id</span><span class="sxs-lookup"><span data-stu-id="2e53e-133">*tenant_id*</span></span>                         | <span data-ttu-id="2e53e-134">`$sub.TenantId` 命令所產生的輸出</span><span class="sxs-lookup"><span data-stu-id="2e53e-134">Output from `$sub.TenantId` command</span></span> |
| <span data-ttu-id="2e53e-135">subscription_id</span><span class="sxs-lookup"><span data-stu-id="2e53e-135">*subscription_id*</span></span>                   | <span data-ttu-id="2e53e-136">`$sub.SubscriptionId` 命令所產生的輸出</span><span class="sxs-lookup"><span data-stu-id="2e53e-136">Output from `$sub.SubscriptionId` command</span></span> |
| <span data-ttu-id="2e53e-137">object_id</span><span class="sxs-lookup"><span data-stu-id="2e53e-137">*object_id*</span></span>                         | <span data-ttu-id="2e53e-138">檢視具有 `$sp.Id` 的服務主體物件識別碼</span><span class="sxs-lookup"><span data-stu-id="2e53e-138">View service principal object ID with `$sp.Id`</span></span> |
| <span data-ttu-id="2e53e-139">managed_image_resource_group_name</span><span class="sxs-lookup"><span data-stu-id="2e53e-139">*managed_image_resource_group_name*</span></span> | <span data-ttu-id="2e53e-140">您在 hello 第一個步驟中建立的資源群組名稱</span><span class="sxs-lookup"><span data-stu-id="2e53e-140">Name of resource group you created in hello first step</span></span> |
| <span data-ttu-id="2e53e-141">managed_image_name</span><span class="sxs-lookup"><span data-stu-id="2e53e-141">*managed_image_name*</span></span>                | <span data-ttu-id="2e53e-142">建立 hello 受管理的磁碟映像的名稱</span><span class="sxs-lookup"><span data-stu-id="2e53e-142">Name for hello managed disk image that is created</span></span> |

```json
{
  "builders": [{
    "type": "azure-arm",

    "client_id": "0831b578-8ab6-40b9-a581-9a880a94aab1",
    "client_secret": "P@ssw0rd!",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "subscription_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx",
    "object_id": "a7dfb070-0d5b-47ac-b9a5-cf214fff0ae2",

    "managed_image_resource_group_name": "myResourceGroup",
    "managed_image_name": "myPackerImage",

    "os_type": "Windows",
    "image_publisher": "MicrosoftWindowsServer",
    "image_offer": "WindowsServer",
    "image_sku": "2016-Datacenter",

    "communicator": "winrm",
    "winrm_use_ssl": "true",
    "winrm_insecure": "true",
    "winrm_timeout": "3m",
    "winrm_username": "packer",

    "azure_tags": {
        "dept": "Engineering",
        "task": "Image deployment"
    },

    "location": "East US",
    "vm_size": "Standard_DS2_v2"
  }],
  "provisioners": [{
    "type": "powershell",
    "inline": [
      "Add-WindowsFeature Web-Server",
      "if( Test-Path $Env:SystemRoot\\windows\\system32\\Sysprep\\unattend.xml ){ rm $Env:SystemRoot\\windows\\system32\\Sysprep\\unattend.xml -Force}",
      "& $Env:SystemRoot\\System32\\Sysprep\\Sysprep.exe /oobe /generalize /shutdown /quiet"
    ]
  }]
}
```

<span data-ttu-id="2e53e-143">此範本建立 Windows Server 2016 VM，會安裝 IIS，然後 hello VM 使用 Sysprep 來一般化。</span><span class="sxs-lookup"><span data-stu-id="2e53e-143">This template builds a Windows Server 2016 VM, installs IIS, then generalizes hello VM with Sysprep.</span></span>


## <a name="build-packer-image"></a><span data-ttu-id="2e53e-144">建置 Packer 映像</span><span class="sxs-lookup"><span data-stu-id="2e53e-144">Build Packer image</span></span>
<span data-ttu-id="2e53e-145">如果您還沒有安裝在本機電腦上的 Packer[依照 hello Packer 安裝指示](https://www.packer.io/docs/install/index.html)。</span><span class="sxs-lookup"><span data-stu-id="2e53e-145">If you don't already have Packer installed on your local machine, [follow hello Packer installation instructions](https://www.packer.io/docs/install/index.html).</span></span>

<span data-ttu-id="2e53e-146">建立 hello 映像藉由指定您 Packer 範本檔案，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2e53e-146">Build hello image by specifying your Packer template file as follows:</span></span>

```bash
./packer build windows.json
```

<span data-ttu-id="2e53e-147">從上述命令 hello hello 輸出的範例如下所示：</span><span class="sxs-lookup"><span data-stu-id="2e53e-147">An example of hello output from hello preceding commands is as follows:</span></span>

```bash
azure-arm output will be in this color.

==> azure-arm: Running builder ...
    azure-arm: Creating Azure Resource Manager (ARM) client ...
==> azure-arm: Creating resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> Location          : ‘East US’
==> azure-arm:  -> Tags              :
==> azure-arm:  ->> task : Image deployment
==> azure-arm:  ->> dept : Engineering
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Getting hello certificate’s URL ...
==> azure-arm:  -> Key Vault Name        : ‘pkrkvpq0mthtbtt’
==> azure-arm:  -> Key Vault Secret Name : ‘packerKeyVaultSecret’
==> azure-arm:  -> Certificate URL       : ‘https://pkrkvpq0mthtbtt.vault.azure.net/secrets/packerKeyVaultSecret/8c7bd823e4fa44e1abb747636128adbb'
==> azure-arm: Setting hello certificate’s URL ...
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Getting hello VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.55.35’
==> azure-arm: Waiting for WinRM toobecome available...
==> azure-arm: Connected tooWinRM!
==> azure-arm: Provisioning with Powershell...
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-powershell-provisioner902510110
    azure-arm: #< CLIXML
    azure-arm:
    azure-arm: Success Restart Needed Exit Code      Feature Result
    azure-arm: ------- -------------- ---------      --------------
    azure-arm: True    No             Success        {Common HTTP Features, Default Document, D...
    azure-arm: <Objs Version=“1.1.0.1” xmlns=“http://schemas.microsoft.com/powershell/2004/04"><Obj S=“progress” RefId=“0"><TN RefId=“0”><T>System.Management.Automation.PSCustomObject</T><T>System.Object</T></TN><MS><I64 N=“SourceId”>1</I64><PR N=“Record”><AV>Preparing modules for first use.</AV><AI>0</AI><Nil /><PI>-1</PI><PC>-1</PC><T>Completed</T><SR>-1</SR><SD> </SD></PR></MS></Obj></Objs>
==> azure-arm: Querying hello machine’s properties ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> ComputeName       : ‘pkrvmpq0mthtbtt’
==> azure-arm:  -> Managed OS Disk   : ‘/subscriptions/guid/resourceGroups/packer-Resource-Group-pq0mthtbtt/providers/Microsoft.Compute/disks/osdisk’
==> azure-arm: Powering off machine ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> ComputeName       : ‘pkrvmpq0mthtbtt’
==> azure-arm: Capturing image ...
==> azure-arm:  -> Compute ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> Compute Name              : ‘pkrvmpq0mthtbtt’
==> azure-arm:  -> Compute Location          : ‘East US’
==> azure-arm:  -> Image ResourceGroupName   : ‘myResourceGroup’
==> azure-arm:  -> Image Name                : ‘myPackerImage’
==> azure-arm:  -> Image Location            : ‘eastus’
==> azure-arm: Deleting resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm: Deleting hello temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. hello artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```

<span data-ttu-id="2e53e-148">花幾分鐘的時間執行 hello provisioners Packer toobuild hello VM，並清除 hello 部署。</span><span class="sxs-lookup"><span data-stu-id="2e53e-148">It takes a few minutes for Packer toobuild hello VM, run hello provisioners, and clean up hello deployment.</span></span>


## <a name="create-vm-from-azure-image"></a><span data-ttu-id="2e53e-149">從 Azure 映像建立 VM</span><span class="sxs-lookup"><span data-stu-id="2e53e-149">Create VM from Azure Image</span></span>
<span data-ttu-id="2e53e-150">設定系統管理員使用者名稱和密碼具有 hello Vm [Get-credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential)。</span><span class="sxs-lookup"><span data-stu-id="2e53e-150">Set an administrator username and password for hello VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential).</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="2e53e-151">您現在可以使用 [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) 從您的映像建立 VM。</span><span class="sxs-lookup"><span data-stu-id="2e53e-151">You can now create a VM from your Image with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="2e53e-152">hello 下列範例會建立名為的 VM *myVM*從*myPackerImage*。</span><span class="sxs-lookup"><span data-stu-id="2e53e-152">hello following example creates a VM named *myVM* from *myPackerImage*.</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $rgName `
    -Location $location `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName $rgName `
    -Location $location `
    -AllocationMethod "Static" `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleWWW  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $rgName `
    -Location $location `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName $rgName `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Define hello image created by Packer
$image = Get-AzureRMImage -ImageName myPackerImage -ResourceGroupName $rgName

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -Id $image.Id | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```

<span data-ttu-id="2e53e-153">花幾分鐘的時間 toocreate hello VM。</span><span class="sxs-lookup"><span data-stu-id="2e53e-153">It takes a few minutes toocreate hello VM.</span></span>


## <a name="test-vm-and-iis"></a><span data-ttu-id="2e53e-154">測試 VM 和 IIS</span><span class="sxs-lookup"><span data-stu-id="2e53e-154">Test VM and IIS</span></span>
<span data-ttu-id="2e53e-155">取得具有您 VM 的 hello 公用 IP 位址[Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress)。</span><span class="sxs-lookup"><span data-stu-id="2e53e-155">Obtain hello public IP address of your VM with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="2e53e-156">hello 下列範例會取得 IP 位址 hello *myPublicIP*稍早建立：</span><span class="sxs-lookup"><span data-stu-id="2e53e-156">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName $rgName `
    -Name "myPublicIP" | select "IpAddress"
```

<span data-ttu-id="2e53e-157">然後，您就可以 tooa 網頁瀏覽器中輸入 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2e53e-157">You can then enter hello public IP address in tooa web browser.</span></span>

![IIS 預設網站](./media/build-image-with-packer/iis.png) 


## <a name="next-steps"></a><span data-ttu-id="2e53e-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2e53e-159">Next steps</span></span>
<span data-ttu-id="2e53e-160">在此範例中，您可以使用 Packer toocreate VM 映像已安裝 iis。</span><span class="sxs-lookup"><span data-stu-id="2e53e-160">In this example, you used Packer toocreate a VM image with IIS already installed.</span></span> <span data-ttu-id="2e53e-161">您可以使用現有的部署工作流程，例如從 hello Team Services、 Ansible、 Chef 或 Puppet 的映像建立的應用程式 tooVMs toodeploy 連同此 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="2e53e-161">You can use this VM image alongside existing deployment workflows, such as toodeploy your app tooVMs created from hello Image with Team Services, Ansible, Chef, or Puppet.</span></span>

<span data-ttu-id="2e53e-162">如需其他 Windows 散發套件的其他 Packer 範本範例，請參閱[這個 GitHub 存放庫](https://github.com/hashicorp/packer/tree/master/examples/azure)。</span><span class="sxs-lookup"><span data-stu-id="2e53e-162">For additional example Packer templates for other Windows distros, see [this GitHub repo](https://github.com/hashicorp/packer/tree/master/examples/azure).</span></span>