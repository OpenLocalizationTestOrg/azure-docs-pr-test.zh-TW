---
title: "在虛擬機器擴展集上部署應用程式"
description: "使用延伸模組在 Azure 虛擬機器擴展集上部署應用程式。"
services: virtual-machine-scale-sets
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8892199-f2e2-4b82-988a-28ca8a7fd1eb
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: fa7d9d3bef4cb326844ede76171e8c566e87116b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-your-application-on-virtual-machine-scale-sets"></a><span data-ttu-id="a5293-103">在虛擬機器擴展集上部署您的應用程式</span><span class="sxs-lookup"><span data-stu-id="a5293-103">Deploy your application on virtual machine scale sets</span></span>

<span data-ttu-id="a5293-104">本文說明在佈建擴展集時安裝軟體的各種不同方式。</span><span class="sxs-lookup"><span data-stu-id="a5293-104">This article describes different ways of how to install software at the time the scale set is provisioned.</span></span>

<span data-ttu-id="a5293-105">您可能需要檢閱[擴展集設計概觀](virtual-machine-scale-sets-design-overview.md)一文，其描述虛擬機器擴展集合所加諸的一些限制。</span><span class="sxs-lookup"><span data-stu-id="a5293-105">You may want to review the [Scale Set Design Overview](virtual-machine-scale-sets-design-overview.md) article, which describes some of the limits imposed by virtual machine scale sets.</span></span>

## <a name="capture-and-reuse-an-image"></a><span data-ttu-id="a5293-106">擷取並重複使用映像</span><span class="sxs-lookup"><span data-stu-id="a5293-106">Capture and reuse an image</span></span>

<span data-ttu-id="a5293-107">您可以使用 Azure 中現有的虛擬機器來準備擴展集的基礎映像。</span><span class="sxs-lookup"><span data-stu-id="a5293-107">You can use a virtual machine you have in Azure to prepare a base-image for your scale set.</span></span> <span data-ttu-id="a5293-108">此程序會在您的儲存體帳戶中建立受控磁碟，您可以參考作為擴展集的基礎映像。</span><span class="sxs-lookup"><span data-stu-id="a5293-108">This process creates a managed disk in your storage account, which you can reference as the base image for your scale set.</span></span> 

<span data-ttu-id="a5293-109">請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a5293-109">Do the following steps:</span></span>

1. <span data-ttu-id="a5293-110">建立 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a5293-110">Create an Azure Virtual Machine</span></span>
   * <span data-ttu-id="a5293-111">[Linux][linux-vm-create]</span><span class="sxs-lookup"><span data-stu-id="a5293-111">[Linux][linux-vm-create]</span></span>
   * <span data-ttu-id="a5293-112">[Windows][windows-vm-create]</span><span class="sxs-lookup"><span data-stu-id="a5293-112">[Windows][windows-vm-create]</span></span>

2. <span data-ttu-id="a5293-113">遠端登入虛擬機器，並視喜好自訂系統。</span><span class="sxs-lookup"><span data-stu-id="a5293-113">Remote into the virtual machine and customize the system to your liking.</span></span>

   <span data-ttu-id="a5293-114">如果想要，您可以立即安裝應用程式。</span><span class="sxs-lookup"><span data-stu-id="a5293-114">If you want, you can install your application now.</span></span> <span data-ttu-id="a5293-115">不過，請了解若立即安裝應用程式，您可能會使升級應用程式更複雜，因為您可能必須先將它移除。</span><span class="sxs-lookup"><span data-stu-id="a5293-115">However, know that by installing your application now, you may make upgrading your application more complicated because you may need to remove it first.</span></span> <span data-ttu-id="a5293-116">您可以改用此步驟來安裝應用程式可能需要的任何必要條件，例如特定執行階段或作業系統功能。</span><span class="sxs-lookup"><span data-stu-id="a5293-116">Instead, you can use this step to install any prerequisites your application may need, like a specific runtime or operating system feature.</span></span>

3. <span data-ttu-id="a5293-117">遵循 [Linux][linux-vm-capture] 或 [Windows][windows-vm-capture] 的「擷取機器」教學課程。</span><span class="sxs-lookup"><span data-stu-id="a5293-117">Follow the "capture a machine" tutorial for either [Linux][linux-vm-capture] or [Windows][windows-vm-capture].</span></span>

4. <span data-ttu-id="a5293-118">使用您在上一個步驟中擷取的映像 URI 建立[虛擬機器擴展集][vmss-create]。</span><span class="sxs-lookup"><span data-stu-id="a5293-118">Create a [Virtual Machine Scale Set][vmss-create] with the image URI you captured in the previous step.</span></span>

<span data-ttu-id="a5293-119">如需磁碟的詳細資訊，請參閱[受控磁碟概觀](../virtual-machines/windows/managed-disks-overview.md)和[使用連結的資料磁碟](virtual-machine-scale-sets-attached-disks.md)。</span><span class="sxs-lookup"><span data-stu-id="a5293-119">For more information about disks, see [Managed Disks Overview](../virtual-machines/windows/managed-disks-overview.md) and [Use Attached Data Disks](virtual-machine-scale-sets-attached-disks.md).</span></span>

## <a name="install-when-the-scale-set-is-provisioned"></a><span data-ttu-id="a5293-120">佈建擴展集時安裝</span><span class="sxs-lookup"><span data-stu-id="a5293-120">Install when the scale set is provisioned</span></span>

<span data-ttu-id="a5293-121">虛擬機器延伸模組可以套用至虛擬機器擴展集。</span><span class="sxs-lookup"><span data-stu-id="a5293-121">Virtual machine extensions can be applied to a virtual machine scale set.</span></span> <span data-ttu-id="a5293-122">透過虛擬機器擴充功能，您可以將擴展集中的虛擬機器當做整個群組來自訂。</span><span class="sxs-lookup"><span data-stu-id="a5293-122">With a virtual machine extension, you can customize the virtual machines in a scale set as a whole group.</span></span> <span data-ttu-id="a5293-123">如需擴充功能的詳細資訊，請參閱[虛擬機器擴充功能](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a5293-123">For more information about extensions, see [Virtual Machine Extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="a5293-124">視您的作業系統為 Linux 或 Windows 而定，有三個主要延伸模組可供您使用。</span><span class="sxs-lookup"><span data-stu-id="a5293-124">There are three main extensions you can use, depending on if your operating system is Linux-based or Windows-based.</span></span>

### <a name="windows"></a><span data-ttu-id="a5293-125">Windows</span><span class="sxs-lookup"><span data-stu-id="a5293-125">Windows</span></span>

<span data-ttu-id="a5293-126">若是 Windows 作業系統，請使用**自訂指令碼 v1.8** 延伸模組或 **PowerShell DSC** 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="a5293-126">For a Windows-based operating system, use either the **Custom Script v1.8** extension, or the **PowerShell DSC** extension.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="a5293-127">Custom Script</span><span class="sxs-lookup"><span data-stu-id="a5293-127">Custom Script</span></span>

<span data-ttu-id="a5293-128">自訂指令碼延伸模組會在擴展集的每部虛擬機器上執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="a5293-128">The Custom Script extension runs a script on each virtual machine instance in the scale set.</span></span> <span data-ttu-id="a5293-129">設定檔或變數會指出下載到虛擬機器的檔案，再指出執行的命令。</span><span class="sxs-lookup"><span data-stu-id="a5293-129">A config file or variable indicates which files are downloaded to the virtual machine, and then what command runs.</span></span> <span data-ttu-id="a5293-130">例如，您可以使用此延伸模組來執行安裝程式、指令碼、批次檔和任何可執行檔。</span><span class="sxs-lookup"><span data-stu-id="a5293-130">You could use this to run an installer, a script, a batch file, any executable for example.</span></span>

<span data-ttu-id="a5293-131">PowerShell 針對設定使用雜湊表。</span><span class="sxs-lookup"><span data-stu-id="a5293-131">PowerShell uses a hashtable for the settings.</span></span> <span data-ttu-id="a5293-132">下列範例會設定自訂指令碼延伸模組，以執行安裝 IIS 的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="a5293-132">This example configures the custom script extension to run a PowerShell script that installs IIS.</span></span>

```powershell
# Setup extension configuration hashtable variable
$customConfig = @{
  "fileUris" = @("https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1");
  "commandToExecute" = "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> `"%TEMP%\StartupLog.txt`" 2>&1";
};

# Add the extension to the config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Compute -Type CustomScriptExtension -TypeHandlerVersion 1.8 -Name "customscript1" -Setting $customConfig

# Send the new config to Azure
Update-AzureRmVmss -ResourceGroupName $rg -Name "MyVmssTest143"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="a5293-133">針對可能包含敏感性資訊的任何設定，請使用 `-ProtectedSetting` 參數。</span><span class="sxs-lookup"><span data-stu-id="a5293-133">Use the `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

---------


<span data-ttu-id="a5293-134">Azure CLI 針對設定使用 json 檔案。</span><span class="sxs-lookup"><span data-stu-id="a5293-134">Azure CLI uses a json file for the settings.</span></span> <span data-ttu-id="a5293-135">下列範例會設定自訂指令碼延伸模組，以執行安裝 IIS 的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="a5293-135">This example configures the custom script extension to run a PowerShell script that installs IIS.</span></span> <span data-ttu-id="a5293-136">請將下列 json 檔案儲存為 _settings.json_。</span><span class="sxs-lookup"><span data-stu-id="a5293-136">Save the following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1"
  ],
  "commandToExecute": "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> \"%TEMP%\StartupLog.txt\" 2>&1"
}
```

<span data-ttu-id="a5293-137">然後，執行下列 Azure CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="a5293-137">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Compute --version 1.8 --name CustomScriptExtension --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="a5293-138">針對可能包含敏感性資訊的任何設定，請使用 `--protected-settings` 參數。</span><span class="sxs-lookup"><span data-stu-id="a5293-138">Use the `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="powershell-dsc"></a><span data-ttu-id="a5293-139">PowerShell DSC</span><span class="sxs-lookup"><span data-stu-id="a5293-139">PowerShell DSC</span></span>

<span data-ttu-id="a5293-140">您可以使用 PowerShell DSC 來自訂擴展集的 VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="a5293-140">You can use PowerShell DSC to customize the scale set vm instances.</span></span> <span data-ttu-id="a5293-141">**Microsoft.Powershell** 所發行的 **DSC** 延伸模組會在每個虛擬機器執行個體上部署及執行所提供的 DSC 設定。</span><span class="sxs-lookup"><span data-stu-id="a5293-141">The **DSC** extension published by **Microsoft.Powershell** deploys and runs the provided DSC configuration on each virtual machine instance.</span></span> <span data-ttu-id="a5293-142">設定檔或變數會告訴延伸模組 *.zip* 封裝的位置，以及要執行的_指令碼函式_組合。</span><span class="sxs-lookup"><span data-stu-id="a5293-142">A config file or variable tells the extension where *.zip* package is, and which _script-function_ combination to run.</span></span>

<span data-ttu-id="a5293-143">PowerShell 針對設定使用雜湊表。</span><span class="sxs-lookup"><span data-stu-id="a5293-143">PowerShell uses a hashtable for the settings.</span></span> <span data-ttu-id="a5293-144">下列範例會部署 DSC 封裝以安裝 IIS。</span><span class="sxs-lookup"><span data-stu-id="a5293-144">This example deploys a DSC package that installs IIS.</span></span>

```powershell
# Setup extension configuration hashtable variable
$dscConfig = @{
  "wmfVersion" = "latest";
  "configuration" = @{
    "url" = "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip";
    "script" = "configure-http.ps1";
    "function" = "WebsiteTest";
  };
}

# Add the extension to the config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Powershell -Type DSC -TypeHandlerVersion 2.24 -Name "dsc1" -Setting $dscConfig

# Send the new config to Azure
Update-AzureRmVmss -ResourceGroupName $rg -Name "myscaleset1"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="a5293-145">針對可能包含敏感性資訊的任何設定，請使用 `-ProtectedSetting` 參數。</span><span class="sxs-lookup"><span data-stu-id="a5293-145">Use the `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

-----------

<span data-ttu-id="a5293-146">Azure CLI 針對設定使用 json。</span><span class="sxs-lookup"><span data-stu-id="a5293-146">Azure CLI uses a json for the settings.</span></span> <span data-ttu-id="a5293-147">下列範例會部署 DSC 封裝以安裝 IIS。</span><span class="sxs-lookup"><span data-stu-id="a5293-147">This example deploys a DSC package that installs IIS.</span></span> <span data-ttu-id="a5293-148">請將下列 json 檔案儲存為 _settings.json_。</span><span class="sxs-lookup"><span data-stu-id="a5293-148">Save the following json file as _settings.json_.</span></span>

```json
{
  "wmfVersion": "latest",
  "configuration": {
    "url": "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip",
    "script": "configure-http.ps1",
    "function": "WebsiteTest"
  }
}
```

<span data-ttu-id="a5293-149">然後，執行下列 Azure CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="a5293-149">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Powershell --version 2.24 --name DSC --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="a5293-150">針對可能包含敏感性資訊的任何設定，請使用 `--protected-settings` 參數。</span><span class="sxs-lookup"><span data-stu-id="a5293-150">Use the `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="linux"></a><span data-ttu-id="a5293-151">Linux</span><span class="sxs-lookup"><span data-stu-id="a5293-151">Linux</span></span>

<span data-ttu-id="a5293-152">Linux 可以使用**自訂指令碼 v2.0** 延伸模組，或在建立期間使用 **cloud-init**。</span><span class="sxs-lookup"><span data-stu-id="a5293-152">Linux can use either the **Custom Script v2.0** extension or use **cloud-init** during creation.</span></span>

<span data-ttu-id="a5293-153">自訂指令碼是簡單的延伸模組，可將檔案下載到虛擬機器執行個體，以及執行命令。</span><span class="sxs-lookup"><span data-stu-id="a5293-153">Custom script is a simple extension that downloads files to the virtual machine instances, and runs a command.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="a5293-154">Custom Script</span><span class="sxs-lookup"><span data-stu-id="a5293-154">Custom Script</span></span>

<span data-ttu-id="a5293-155">請將下列 json 檔案儲存為 _settings.json_。</span><span class="sxs-lookup"><span data-stu-id="a5293-155">Save the following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
  ],
  "commandToExecute": "bash installserver.sh"
}
```

<span data-ttu-id="a5293-156">使用 Azure CLI 將此延伸模組新增至現有的虛擬機器擴展集。</span><span class="sxs-lookup"><span data-stu-id="a5293-156">Use the Azure CLI to add this extension to an existing virtual machine scale set.</span></span> <span data-ttu-id="a5293-157">擴展集中的每部虛擬機器都會自動執行此延伸模組。</span><span class="sxs-lookup"><span data-stu-id="a5293-157">Each virtual machine in the scale set automatically runs the extension.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="a5293-158">針對可能包含敏感性資訊的任何設定，請使用 `--protected-settings` 參數。</span><span class="sxs-lookup"><span data-stu-id="a5293-158">Use the `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

#### <a name="cloud-init"></a><span data-ttu-id="a5293-159">Cloud-Init</span><span class="sxs-lookup"><span data-stu-id="a5293-159">Cloud-Init</span></span>

<span data-ttu-id="a5293-160">您可以在建立擴展集時使用 Cloud-Init。</span><span class="sxs-lookup"><span data-stu-id="a5293-160">Cloud-Init is used when the scale set is created.</span></span> <span data-ttu-id="a5293-161">首先，建立名為 _cloud-init.txt_ 的本機檔案並加入您的設定。</span><span class="sxs-lookup"><span data-stu-id="a5293-161">First, create a local file named _cloud-init.txt_ and add your configuration to it.</span></span> <span data-ttu-id="a5293-162">例如，請參閱[此 gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)</span><span class="sxs-lookup"><span data-stu-id="a5293-162">For example, see [this gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)</span></span>

<span data-ttu-id="a5293-163">使用 Azure CLI 建立擴展集。</span><span class="sxs-lookup"><span data-stu-id="a5293-163">Use the Azure CLI to create a scale set.</span></span> <span data-ttu-id="a5293-164">`--custom-data` 欄位接受 cloud-init 指令碼的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="a5293-164">The `--custom-data` field accepts the file name of a cloud-init script.</span></span>

```azurecli
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image Canonical:UbuntuServer:14.04.4-LTS:latest \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

## <a name="how-do-i-manage-application-updates"></a><span data-ttu-id="a5293-165">如何管理應用程式更新？</span><span class="sxs-lookup"><span data-stu-id="a5293-165">How do I manage application updates?</span></span>

<span data-ttu-id="a5293-166">如果您透過延伸模組部署應用程式，請對延伸模組定義進行某些變更。</span><span class="sxs-lookup"><span data-stu-id="a5293-166">If you deployed your application through an extension, alter the extension definition in some way.</span></span> <span data-ttu-id="a5293-167">此變更會將延伸模組重新部署到所有虛擬機器執行個體。</span><span class="sxs-lookup"><span data-stu-id="a5293-167">This change causes the extension to be redeployed to all virtual machine instances.</span></span> <span data-ttu-id="a5293-168">您**必須**對延伸模組進行某些變更 (例如重新命名所參考的檔案)，否則 Azure 不會看到延伸模組已變更。</span><span class="sxs-lookup"><span data-stu-id="a5293-168">Something **must** be changed about the extension, such as renaming a referenced file, otherwise, Azure does not see that the extension has changed.</span></span>

<span data-ttu-id="a5293-169">如果您將應用程式內建到自己的作業系統映像中，請使用自動化部署管線進行應用程式更新。</span><span class="sxs-lookup"><span data-stu-id="a5293-169">If you baked the application into your own operating system image, use an automated deployment pipeline for application updates.</span></span> <span data-ttu-id="a5293-170">請設計您的架構以協助將分段擴展集快速切換到生產環境。</span><span class="sxs-lookup"><span data-stu-id="a5293-170">Design your architecture to facilitate rapid swapping of a staged scale set into production.</span></span> <span data-ttu-id="a5293-171">此方法的其中一個好例子就是 [Azure Spinnaker 驅動程式工作](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/)。</span><span class="sxs-lookup"><span data-stu-id="a5293-171">A good example of this approach is the [Azure Spinnaker driver work](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).</span></span>

<span data-ttu-id="a5293-172">[Packer](https://www.packer.io/) 和 [Terraform](https://www.terraform.io/) 支援 Azure Resource Manager，因此您也可以「以程式碼方式」定義您的映像並在 Azure 中建置它們，然後在您的擴展集內使用 VHD。</span><span class="sxs-lookup"><span data-stu-id="a5293-172">[Packer](https://www.packer.io/) and [Terraform](https://www.terraform.io/) support Azure Resource Manager, so you can also define your images "as code" and build them in Azure, then use the VHD in your scale set.</span></span> <span data-ttu-id="a5293-173">不過，這麼做對 Marketplace 映像會造成問題，其中延伸模組/自訂指令碼會變得更加重要，因為您不是直接從 Marketplace 操縱位元。</span><span class="sxs-lookup"><span data-stu-id="a5293-173">However, doing so would become problematic for marketplace images, where extensions/custom scripts become more important since you don’t directly manipulate bits from marketplace.</span></span>

## <a name="what-happens-when-a-scale-set-scales-out"></a><span data-ttu-id="a5293-174">當擴展集相應放大時，會發生什麼情況？</span><span class="sxs-lookup"><span data-stu-id="a5293-174">What happens when a scale set scales out?</span></span>
<span data-ttu-id="a5293-175">當您將一或多部虛擬機器新增至擴展集時，會自動安裝應用程式。</span><span class="sxs-lookup"><span data-stu-id="a5293-175">When you add one or more virtual machines to a scale set, the application is automatically installed.</span></span> <span data-ttu-id="a5293-176">例如，如果擴展集已定義延伸模組，則每次建立新的虛擬機器時，這些延伸模組都會在新的虛擬機器上執行。</span><span class="sxs-lookup"><span data-stu-id="a5293-176">For example if the scale set has extensions defined, they run on a new virtual machine each time it is created.</span></span> <span data-ttu-id="a5293-177">如果擴展集是以自訂映像為基礎，則所有新的虛擬機器都是來源自訂映像的複本。</span><span class="sxs-lookup"><span data-stu-id="a5293-177">If the scale set is based on a custom image, any new virtual machine is a copy of the source custom image.</span></span> <span data-ttu-id="a5293-178">如果擴展集的虛擬機器是容器主機，則您可以讓啟動程式碼載入自訂指令碼延伸模組中的容器。</span><span class="sxs-lookup"><span data-stu-id="a5293-178">If the scale set virtual machines are container hosts, then you might have startup code to load the containers in a Custom Script Extension.</span></span> <span data-ttu-id="a5293-179">或者，延伸模組可以安裝會向叢集 Orchestrator (例如 Azure Container Service) 註冊的代理程式。</span><span class="sxs-lookup"><span data-stu-id="a5293-179">Or, an extension might install an agent that registers with a cluster orchestrator, such as Azure Container Service.</span></span>


## <a name="how-do-you-roll-out-an-os-update-across-update-domains"></a><span data-ttu-id="a5293-180">如何在各個更新網域推出 OS 更新？</span><span class="sxs-lookup"><span data-stu-id="a5293-180">How do you roll out an OS update across update domains?</span></span>
<span data-ttu-id="a5293-181">假設您想要在更新 OS 映像的同時，又讓虛擬機器擴展集持續執行。</span><span class="sxs-lookup"><span data-stu-id="a5293-181">Suppose you want to update your OS image while keeping the virtual machine scale set running.</span></span> <span data-ttu-id="a5293-182">PowerShell 和 Azure CLI 可以更新虛擬機器映像，一次一部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a5293-182">PowerShell and the Azure CLI can update the virtual machine images, one virtual machine at a time.</span></span> <span data-ttu-id="a5293-183">[升級虛擬機器擴展集](./virtual-machine-scale-sets-upgrade-scale-set.md)一文也提供進一步的資訊，說明虛擬機器擴展集內執行作業系統升級的可用選項。</span><span class="sxs-lookup"><span data-stu-id="a5293-183">The [Upgrade a Virtual Machine Scale Set](./virtual-machine-scale-sets-upgrade-scale-set.md) article also provides further information on what options are available to perform an operating system upgrade across a virtual machine scale set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5293-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a5293-184">Next steps</span></span>

* [<span data-ttu-id="a5293-185">使用 PowerShell 管理您的擴展集。</span><span class="sxs-lookup"><span data-stu-id="a5293-185">Use PowerShell to manage your scale set.</span></span>](virtual-machine-scale-sets-windows-manage.md)
* [<span data-ttu-id="a5293-186">建立擴展集範本。</span><span class="sxs-lookup"><span data-stu-id="a5293-186">Create a scale set template.</span></span>](virtual-machine-scale-sets-mvss-start.md)


[linux-vm-create]: ../virtual-machines/linux/tutorial-manage-vm.md
[windows-vm-create]: ../virtual-machines/windows/tutorial-manage-vm.md
[linux-vm-capture]: ../virtual-machines/linux/capture-image.md
[windows-vm-capture]: ../virtual-machines/windows/capture-image.md 
[vmss-create]: virtual-machine-scale-sets-create.md

