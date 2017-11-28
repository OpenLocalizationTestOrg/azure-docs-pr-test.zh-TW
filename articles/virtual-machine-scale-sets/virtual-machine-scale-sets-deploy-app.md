---
title: "aaaDeploy 上虛擬機器規模的應用程式設定"
description: "使用 Azure 虛擬機器擴展集延伸模組 toodepoy 應用程式。"
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
ms.openlocfilehash: 5f3988b9511d80370a8be1fc042c21fee212506e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-application-on-virtual-machine-scale-sets"></a><span data-ttu-id="aa4a2-103">在虛擬機器擴展集上部署您的應用程式</span><span class="sxs-lookup"><span data-stu-id="aa4a2-103">Deploy your application on virtual machine scale sets</span></span>

<span data-ttu-id="aa4a2-104">本文說明如何在 hello 時段 hello tooinstall 軟體設定不同的方式已佈建。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-104">This article describes different ways of how tooinstall software at hello time hello scale set is provisioned.</span></span>

<span data-ttu-id="aa4a2-105">您可能會想 tooreview hello[小數位數設定的設計概觀](virtual-machine-scale-sets-design-overview.md)文件，其中描述一些 hello 虛擬機器擴展集所加諸的限制。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-105">You may want tooreview hello [Scale Set Design Overview](virtual-machine-scale-sets-design-overview.md) article, which describes some of hello limits imposed by virtual machine scale sets.</span></span>

## <a name="capture-and-reuse-an-image"></a><span data-ttu-id="aa4a2-106">擷取並重複使用映像</span><span class="sxs-lookup"><span data-stu-id="aa4a2-106">Capture and reuse an image</span></span>

<span data-ttu-id="aa4a2-107">您可以使用您已為您的標尺的 Azure tooprepare 基底映像中設定虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-107">You can use a virtual machine you have in Azure tooprepare a base-image for your scale set.</span></span> <span data-ttu-id="aa4a2-108">此程序會在您可以在擴展集做為 hello 基底映像參考的儲存體帳戶中建立受管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-108">This process creates a managed disk in your storage account, which you can reference as hello base image for your scale set.</span></span> 

<span data-ttu-id="aa4a2-109">下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="aa4a2-109">Do hello following steps:</span></span>

1. <span data-ttu-id="aa4a2-110">建立 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="aa4a2-110">Create an Azure Virtual Machine</span></span>
   * <span data-ttu-id="aa4a2-111">[Linux][linux-vm-create]</span><span class="sxs-lookup"><span data-stu-id="aa4a2-111">[Linux][linux-vm-create]</span></span>
   * <span data-ttu-id="aa4a2-112">[Windows][windows-vm-create]</span><span class="sxs-lookup"><span data-stu-id="aa4a2-112">[Windows][windows-vm-create]</span></span>

2. <span data-ttu-id="aa4a2-113">遠端至 hello 虛擬機器，並自訂 hello 系統 tooyour 喜好。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-113">Remote into hello virtual machine and customize hello system tooyour liking.</span></span>

   <span data-ttu-id="aa4a2-114">如果想要，您可以立即安裝應用程式。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-114">If you want, you can install your application now.</span></span> <span data-ttu-id="aa4a2-115">不過，知道安裝您的應用程式現在，您可能會進行升級您的應用程式更複雜，因為您可能需要 tooremove 它第一次。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-115">However, know that by installing your application now, you may make upgrading your application more complicated because you may need tooremove it first.</span></span> <span data-ttu-id="aa4a2-116">相反地，您可以使用此步驟 tooinstall 任何可能需要您的應用程式，例如特定執行階段或作業系統功能的必要條件。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-116">Instead, you can use this step tooinstall any prerequisites your application may need, like a specific runtime or operating system feature.</span></span>

3. <span data-ttu-id="aa4a2-117">請遵循 hello 」 擷取機器 」 教學課程的[Linux] [ linux-vm-capture]或[Windows][windows-vm-capture]。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-117">Follow hello "capture a machine" tutorial for either [Linux][linux-vm-capture] or [Windows][windows-vm-capture].</span></span>

4. <span data-ttu-id="aa4a2-118">建立[虛擬機器擴展集][ vmss-create] hello 與映像 hello 上一個步驟中所擷取的 URI。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-118">Create a [Virtual Machine Scale Set][vmss-create] with hello image URI you captured in hello previous step.</span></span>

<span data-ttu-id="aa4a2-119">如需磁碟的詳細資訊，請參閱[受控磁碟概觀](../virtual-machines/windows/managed-disks-overview.md)和[使用連結的資料磁碟](virtual-machine-scale-sets-attached-disks.md)。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-119">For more information about disks, see [Managed Disks Overview](../virtual-machines/windows/managed-disks-overview.md) and [Use Attached Data Disks](virtual-machine-scale-sets-attached-disks.md).</span></span>

## <a name="install-when-hello-scale-set-is-provisioned"></a><span data-ttu-id="aa4a2-120">Hello 規模調整集合已佈建時，安裝</span><span class="sxs-lookup"><span data-stu-id="aa4a2-120">Install when hello scale set is provisioned</span></span>

<span data-ttu-id="aa4a2-121">虛擬機器延伸模組就會套用 tooa 虛擬機器規模集。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-121">Virtual machine extensions can be applied tooa virtual machine scale set.</span></span> <span data-ttu-id="aa4a2-122">透過虛擬機器擴充功能，您可以自訂 hello 虛擬機器擴展集做為整個群組內。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-122">With a virtual machine extension, you can customize hello virtual machines in a scale set as a whole group.</span></span> <span data-ttu-id="aa4a2-123">如需擴充功能的詳細資訊，請參閱[虛擬機器擴充功能](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-123">For more information about extensions, see [Virtual Machine Extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="aa4a2-124">視您的作業系統為 Linux 或 Windows 而定，有三個主要延伸模組可供您使用。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-124">There are three main extensions you can use, depending on if your operating system is Linux-based or Windows-based.</span></span>

### <a name="windows"></a><span data-ttu-id="aa4a2-125">Windows</span><span class="sxs-lookup"><span data-stu-id="aa4a2-125">Windows</span></span>

<span data-ttu-id="aa4a2-126">Windows 作業系統，請使用其中一個 hello**自訂指令碼 v1.8**擴充功能或 hello **PowerShell DSC**延伸模組。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-126">For a Windows-based operating system, use either hello **Custom Script v1.8** extension, or hello **PowerShell DSC** extension.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="aa4a2-127">Custom Script</span><span class="sxs-lookup"><span data-stu-id="aa4a2-127">Custom Script</span></span>

<span data-ttu-id="aa4a2-128">hello 自訂指令碼延伸執行指令碼 hello 規模集中的每個虛擬機器執行個體。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-128">hello Custom Script extension runs a script on each virtual machine instance in hello scale set.</span></span> <span data-ttu-id="aa4a2-129">組態檔或變數，指出哪些檔案會下載的 toohello 虛擬機器，然後再執行哪些命令。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-129">A config file or variable indicates which files are downloaded toohello virtual machine, and then what command runs.</span></span> <span data-ttu-id="aa4a2-130">如需範例可以使用這個 toorun 安裝程式、 指令碼、 批次檔，任何可執行檔。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-130">You could use this toorun an installer, a script, a batch file, any executable for example.</span></span>

<span data-ttu-id="aa4a2-131">PowerShell 會基於 hello 設定使用雜湊表。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-131">PowerShell uses a hashtable for hello settings.</span></span> <span data-ttu-id="aa4a2-132">這個範例會設定 hello 自訂指令碼延伸 toorun 安裝 IIS 的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-132">This example configures hello custom script extension toorun a PowerShell script that installs IIS.</span></span>

```powershell
# Setup extension configuration hashtable variable
$customConfig = @{
  "fileUris" = @("https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1");
  "commandToExecute" = "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> `"%TEMP%\StartupLog.txt`" 2>&1";
};

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Compute -Type CustomScriptExtension -TypeHandlerVersion 1.8 -Name "customscript1" -Setting $customConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "MyVmssTest143"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="aa4a2-133">使用 hello`-ProtectedSetting`切換可能包含機密資訊的任何設定。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-133">Use hello `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

---------


<span data-ttu-id="aa4a2-134">Azure CLI hello 設定使用的 json 檔案。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-134">Azure CLI uses a json file for hello settings.</span></span> <span data-ttu-id="aa4a2-135">這個範例會設定 hello 自訂指令碼延伸 toorun 安裝 IIS 的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-135">This example configures hello custom script extension toorun a PowerShell script that installs IIS.</span></span> <span data-ttu-id="aa4a2-136">儲存下列 json 檔案儲存為 hello _settings.json_。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-136">Save hello following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1"
  ],
  "commandToExecute": "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> \"%TEMP%\StartupLog.txt\" 2>&1"
}
```

<span data-ttu-id="aa4a2-137">然後，執行下列 Azure CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-137">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Compute --version 1.8 --name CustomScriptExtension --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="aa4a2-138">使用 hello`--protected-settings`切換可能包含機密資訊的任何設定。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-138">Use hello `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="powershell-dsc"></a><span data-ttu-id="aa4a2-139">PowerShell DSC</span><span class="sxs-lookup"><span data-stu-id="aa4a2-139">PowerShell DSC</span></span>

<span data-ttu-id="aa4a2-140">您可以使用 PowerShell DSC toocustomize hello 小數位數組 vm 執行個體。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-140">You can use PowerShell DSC toocustomize hello scale set vm instances.</span></span> <span data-ttu-id="aa4a2-141">hello **DSC**延伸模組所發行**Microsoft.Powershell**部署，並在每個虛擬機器執行個體上執行提供的 hello DSC 設定。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-141">hello **DSC** extension published by **Microsoft.Powershell** deploys and runs hello provided DSC configuration on each virtual machine instance.</span></span> <span data-ttu-id="aa4a2-142">組態檔或變數會告知 hello 延伸其中*.zip*是封裝，以及哪些_指令碼函式_組合 toorun。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-142">A config file or variable tells hello extension where *.zip* package is, and which _script-function_ combination toorun.</span></span>

<span data-ttu-id="aa4a2-143">PowerShell 會基於 hello 設定使用雜湊表。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-143">PowerShell uses a hashtable for hello settings.</span></span> <span data-ttu-id="aa4a2-144">下列範例會部署 DSC 封裝以安裝 IIS。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-144">This example deploys a DSC package that installs IIS.</span></span>

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

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Powershell -Type DSC -TypeHandlerVersion 2.24 -Name "dsc1" -Setting $dscConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "myscaleset1"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="aa4a2-145">使用 hello`-ProtectedSetting`切換可能包含機密資訊的任何設定。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-145">Use hello `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

-----------

<span data-ttu-id="aa4a2-146">Azure CLI 會使用 json hello 設定。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-146">Azure CLI uses a json for hello settings.</span></span> <span data-ttu-id="aa4a2-147">下列範例會部署 DSC 封裝以安裝 IIS。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-147">This example deploys a DSC package that installs IIS.</span></span> <span data-ttu-id="aa4a2-148">儲存下列 json 檔案儲存為 hello _settings.json_。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-148">Save hello following json file as _settings.json_.</span></span>

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

<span data-ttu-id="aa4a2-149">然後，執行下列 Azure CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-149">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Powershell --version 2.24 --name DSC --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="aa4a2-150">使用 hello`--protected-settings`切換可能包含機密資訊的任何設定。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-150">Use hello `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="linux"></a><span data-ttu-id="aa4a2-151">Linux</span><span class="sxs-lookup"><span data-stu-id="aa4a2-151">Linux</span></span>

<span data-ttu-id="aa4a2-152">Linux 可以使用任一 hello**自訂指令碼 v2.0**擴充功能或使用**雲端 init**期間建立。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-152">Linux can use either hello **Custom Script v2.0** extension or use **cloud-init** during creation.</span></span>

<span data-ttu-id="aa4a2-153">自訂指令碼是一種簡單的延伸，下載檔案 toohello 虛擬機器執行個體，並在執行命令。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-153">Custom script is a simple extension that downloads files toohello virtual machine instances, and runs a command.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="aa4a2-154">Custom Script</span><span class="sxs-lookup"><span data-stu-id="aa4a2-154">Custom Script</span></span>

<span data-ttu-id="aa4a2-155">儲存下列 json 檔案儲存為 hello _settings.json_。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-155">Save hello following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
  ],
  "commandToExecute": "bash installserver.sh"
}
```

<span data-ttu-id="aa4a2-156">請使用現有的虛擬機器規模集的這個延伸模組 tooan hello Azure CLI tooadd。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-156">Use hello Azure CLI tooadd this extension tooan existing virtual machine scale set.</span></span> <span data-ttu-id="aa4a2-157">Hello 標尺每個虛擬機器設定自動執行 hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-157">Each virtual machine in hello scale set automatically runs hello extension.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="aa4a2-158">使用 hello`--protected-settings`切換可能包含機密資訊的任何設定。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-158">Use hello `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

#### <a name="cloud-init"></a><span data-ttu-id="aa4a2-159">Cloud-Init</span><span class="sxs-lookup"><span data-stu-id="aa4a2-159">Cloud-Init</span></span>

<span data-ttu-id="aa4a2-160">建立 hello 規模集時，會使用雲端 Init。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-160">Cloud-Init is used when hello scale set is created.</span></span> <span data-ttu-id="aa4a2-161">首先，建立名為本機檔案_雲端 init.txt_和加入組態 tooit。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-161">First, create a local file named _cloud-init.txt_ and add your configuration tooit.</span></span> <span data-ttu-id="aa4a2-162">例如，請參閱[此 gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)</span><span class="sxs-lookup"><span data-stu-id="aa4a2-162">For example, see [this gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)</span></span>

<span data-ttu-id="aa4a2-163">設定使用 hello Azure CLI toocreate 小數位數。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-163">Use hello Azure CLI toocreate a scale set.</span></span> <span data-ttu-id="aa4a2-164">hello`--custom-data`欄位可接受 hello 雲端初始化指令碼檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-164">hello `--custom-data` field accepts hello file name of a cloud-init script.</span></span>

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

## <a name="how-do-i-manage-application-updates"></a><span data-ttu-id="aa4a2-165">如何管理應用程式更新？</span><span class="sxs-lookup"><span data-stu-id="aa4a2-165">How do I manage application updates?</span></span>

<span data-ttu-id="aa4a2-166">如果您部署您的應用程式，透過擴充功能時，改變 hello 在某些方面的延伸模組定義。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-166">If you deployed your application through an extension, alter hello extension definition in some way.</span></span> <span data-ttu-id="aa4a2-167">這項變更會導致 hello 延伸 toobe 重新部署 tooall 虛擬機器執行個體。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-167">This change causes hello extension toobe redeployed tooall virtual machine instances.</span></span> <span data-ttu-id="aa4a2-168">項目**必須**變更有關 hello 擴充功能，例如重新命名參考的檔案，否則 Azure hello 延伸模組不再顯示已變更的作用。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-168">Something **must** be changed about hello extension, such as renaming a referenced file, otherwise, Azure does not see that hello extension has changed.</span></span>

<span data-ttu-id="aa4a2-169">如果您的作業系統映像到法式 hello 應用程式，使用自動的部署管線的應用程式更新。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-169">If you baked hello application into your own operating system image, use an automated deployment pipeline for application updates.</span></span> <span data-ttu-id="aa4a2-170">設計您的架構 toofacilitate 快速交換至生產環境中設定預備標尺。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-170">Design your architecture toofacilitate rapid swapping of a staged scale set into production.</span></span> <span data-ttu-id="aa4a2-171">這種方法的理想範例為 hello [Azure Spinnaker 驅動程式工作](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/)。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-171">A good example of this approach is hello [Azure Spinnaker driver work](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).</span></span>

<span data-ttu-id="aa4a2-172">[Packer](https://www.packer.io/)和[Terraform](https://www.terraform.io/)支援 Azure 資源管理員，讓您可以定義您的映像 」 做為程式碼 」，並建置在 Azure 中，然後使用您規模集中的 hello VHD。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-172">[Packer](https://www.packer.io/) and [Terraform](https://www.terraform.io/) support Azure Resource Manager, so you can also define your images "as code" and build them in Azure, then use hello VHD in your scale set.</span></span> <span data-ttu-id="aa4a2-173">不過，這麼做對 Marketplace 映像會造成問題，其中延伸模組/自訂指令碼會變得更加重要，因為您不是直接從 Marketplace 操縱位元。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-173">However, doing so would become problematic for marketplace images, where extensions/custom scripts become more important since you don’t directly manipulate bits from marketplace.</span></span>

## <a name="what-happens-when-a-scale-set-scales-out"></a><span data-ttu-id="aa4a2-174">當擴展集相應放大時，會發生什麼情況？</span><span class="sxs-lookup"><span data-stu-id="aa4a2-174">What happens when a scale set scales out?</span></span>
<span data-ttu-id="aa4a2-175">當您新增一或多個虛擬機器 tooa 規模集時，會自動安裝 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-175">When you add one or more virtual machines tooa scale set, hello application is automatically installed.</span></span> <span data-ttu-id="aa4a2-176">範例 hello 規模調整集合，如果有定義的擴充功能，它們執行新的虛擬機器上每次建立時。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-176">For example if hello scale set has extensions defined, they run on a new virtual machine each time it is created.</span></span> <span data-ttu-id="aa4a2-177">如果 hello 規模調整集合為基礎的自訂映像，任何新的虛擬機器是一份 hello 來源的自訂映像。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-177">If hello scale set is based on a custom image, any new virtual machine is a copy of hello source custom image.</span></span> <span data-ttu-id="aa4a2-178">如果 hello 小數位數組虛擬機器是容器主機，您可能在自訂指令碼延伸必須啟動程式碼 tooload hello 容器。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-178">If hello scale set virtual machines are container hosts, then you might have startup code tooload hello containers in a Custom Script Extension.</span></span> <span data-ttu-id="aa4a2-179">或者，延伸模組可以安裝會向叢集 Orchestrator (例如 Azure Container Service) 註冊的代理程式。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-179">Or, an extension might install an agent that registers with a cluster orchestrator, such as Azure Container Service.</span></span>


## <a name="how-do-you-roll-out-an-os-update-across-update-domains"></a><span data-ttu-id="aa4a2-180">如何在各個更新網域推出 OS 更新？</span><span class="sxs-lookup"><span data-stu-id="aa4a2-180">How do you roll out an OS update across update domains?</span></span>
<span data-ttu-id="aa4a2-181">假設您想要 tooupdate 作業系統映像，同時保留 hello 虛擬機器擴展集執行。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-181">Suppose you want tooupdate your OS image while keeping hello virtual machine scale set running.</span></span> <span data-ttu-id="aa4a2-182">PowerShell 和 hello Azure CLI 可以更新 hello 虛擬機器映像，一部虛擬機器一次。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-182">PowerShell and hello Azure CLI can update hello virtual machine images, one virtual machine at a time.</span></span> <span data-ttu-id="aa4a2-183">hello[升級虛擬機器擴展集](./virtual-machine-scale-sets-upgrade-scale-set.md)發行項也會提供進一步資訊的選擇有哪些可用 tooperform 作業系統升級各虛擬機器規模集。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-183">hello [Upgrade a Virtual Machine Scale Set](./virtual-machine-scale-sets-upgrade-scale-set.md) article also provides further information on what options are available tooperform an operating system upgrade across a virtual machine scale set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa4a2-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aa4a2-184">Next steps</span></span>

* [<span data-ttu-id="aa4a2-185">使用 PowerShell toomanage 規模集。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-185">Use PowerShell toomanage your scale set.</span></span>](virtual-machine-scale-sets-windows-manage.md)
* [<span data-ttu-id="aa4a2-186">建立擴展集範本。</span><span class="sxs-lookup"><span data-stu-id="aa4a2-186">Create a scale set template.</span></span>](virtual-machine-scale-sets-mvss-start.md)


[linux-vm-create]: ../virtual-machines/linux/tutorial-manage-vm.md
[windows-vm-create]: ../virtual-machines/windows/tutorial-manage-vm.md
[linux-vm-capture]: ../virtual-machines/linux/capture-image.md
[windows-vm-capture]: ../virtual-machines/windows/capture-image.md 
[vmss-create]: virtual-machine-scale-sets-create.md

