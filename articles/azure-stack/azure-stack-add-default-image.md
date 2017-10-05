---
title: "將預設 VM 映像新增到 Azure Stack 市集 | Microsoft Docs"
description: "將 Windows Server 2016 VM 預設映像新增到 Azure Stack 市集。"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: 2953038d45b1bda4aa281ecad91c887dcde90bd0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="add-the-windows-server-2016-vm-image-to-the-azure-stack-marketplace"></a><span data-ttu-id="6a274-103">將 Windows Server 2016 VM 映像新增到 Azure Stack 市集</span><span class="sxs-lookup"><span data-stu-id="6a274-103">Add the Windows Server 2016 VM image to the Azure Stack marketplace</span></span>

<span data-ttu-id="6a274-104">Azure Stack 市集中預設沒有提供任何虛擬機器映像。</span><span class="sxs-lookup"><span data-stu-id="6a274-104">By default, there aren’t any virtual machine images available in the Azure Stack marketplace.</span></span> <span data-ttu-id="6a274-105">Azure 堆疊雲端系統管理員必須將映像新增至 marketplace，使用者才能使用它們。</span><span class="sxs-lookup"><span data-stu-id="6a274-105">The Azure Stack cloud administrator must add an image to the marketplace before users can use them.</span></span> <span data-ttu-id="6a274-106">您可以使用下列兩種方法其中之一，將 Windows Server 2016 映像新增到 Azure Stack 市集：</span><span class="sxs-lookup"><span data-stu-id="6a274-106">You can add the Windows Server 2016 image to the Azure Stack marketplace by using one of the following two methods:</span></span>

* <span data-ttu-id="6a274-107">[從 Azure Marketplace 下載映像來新增映像](#add-the-image-by-downloading-it-from-the-Azure-marketplace)：如果您是在已連線的情況下進行操作，並且已向 Azure 註冊 Azure Stack 執行個體，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="6a274-107">[Add the image by downloading it from the Azure Marketplace](#add-the-image-by-downloading-it-from-the-Azure-marketplace) - Use this option if you are operating in a connected scenario and if you have registered your Azure Stack instance with Azure.</span></span>

* <span data-ttu-id="6a274-108">[使用 PowerShell 來新增映像](#add-the-image-by-using-powershell)：如果您是在中斷連線或連線能力有限的情況下部署 Azure Stack，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="6a274-108">[Add the image by using PowerShell](#add-the-image-by-using-powershell) - Use this option if you have deployed Azure Stack in a disconnected scenario or in scenarios with limited connectivity.</span></span>

## <a name="add-the-image-by-downloading-it-from-the-azure-marketplace"></a><span data-ttu-id="6a274-109">從 Azure Marketplace 下載映像來新增映像</span><span class="sxs-lookup"><span data-stu-id="6a274-109">Add the image by downloading it from the Azure Marketplace</span></span>

1. <span data-ttu-id="6a274-110">部署 Azure Stack 之後，登入您的「Azure Stack 開發套件」。</span><span class="sxs-lookup"><span data-stu-id="6a274-110">After deploying Azure Stack, sign in to your Azure Stack Development Kit.</span></span>

2. <span data-ttu-id="6a274-111">按一下 [更多服務] > [市集管理] > [從 Azure 新增]</span><span class="sxs-lookup"><span data-stu-id="6a274-111">click **More services** > **Marketplace Management** > **Add from Azure**</span></span> 

3. <span data-ttu-id="6a274-112">尋找或搜尋 [Windows Server 2016 Datacenter – 評估版] 映像 > 按一下 [下載]</span><span class="sxs-lookup"><span data-stu-id="6a274-112">Find or search for the **Windows Server 2016 Datacenter – Eval** image > click **Download**</span></span>

   ![從 Azure 下載映像](media/azure-stack-add-default-image/download-image.png)

<span data-ttu-id="6a274-114">下載完成之後，映像會被新增到 [市集管理] 刀鋒視窗，而且從 [虛擬機器] 刀鋒視窗也可以使用此映像。</span><span class="sxs-lookup"><span data-stu-id="6a274-114">After the download completes, the image is added to the **Marketplace Management** blade and it is also made available from the **Virtual Machines** blade.</span></span>

## <a name="add-the-image-by-using-powershell"></a><span data-ttu-id="6a274-115">使用 PowerShell 來新增映像</span><span class="sxs-lookup"><span data-stu-id="6a274-115">Add the image by using PowerShell</span></span>

### <a name="prerequisites"></a><span data-ttu-id="6a274-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="6a274-116">Prerequisites</span></span> 

<span data-ttu-id="6a274-117">從[開發套件](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop)，或從 Windows 型外部用戶端 (如果您是[透過 VPN 連線](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn))，執行下列先決條件：</span><span class="sxs-lookup"><span data-stu-id="6a274-117">Run the following prerequisites either from the [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span></span>

* <span data-ttu-id="6a274-118">安裝 [Azure Stack 相容的 Azure PowerShell 模組](azure-stack-powershell-install.md)。</span><span class="sxs-lookup"><span data-stu-id="6a274-118">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  

* <span data-ttu-id="6a274-119">下載[與 Azure Stack 搭配運作所需的工具](azure-stack-powershell-download.md)。</span><span class="sxs-lookup"><span data-stu-id="6a274-119">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span>  

* <span data-ttu-id="6a274-120">移至 https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016 並下載 Windows Server 2016 評估版。</span><span class="sxs-lookup"><span data-stu-id="6a274-120">Go to https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016 and download the Windows Server 2016 evaluation.</span></span> <span data-ttu-id="6a274-121">出現提示時，選取下載項的 **ISO** 版本。</span><span class="sxs-lookup"><span data-stu-id="6a274-121">When prompted, select the **ISO** version of the download.</span></span> <span data-ttu-id="6a274-122">記錄下載位置的路徑，稍後在這些步驟中將會用到。</span><span class="sxs-lookup"><span data-stu-id="6a274-122">Record the path to the download location, which is used later in these steps.</span></span> <span data-ttu-id="6a274-123">此步驟需要網際網路連線能力。</span><span class="sxs-lookup"><span data-stu-id="6a274-123">This step requires internet connectivity.</span></span>  

<span data-ttu-id="6a274-124">現在，執行下列步驟以將映像新增到 Azure Stack 市集：</span><span class="sxs-lookup"><span data-stu-id="6a274-124">Now run the following steps to add the image to the Azure Stack marketplace:</span></span>
   
1. <span data-ttu-id="6a274-125">使用下列命令來匯入 Azure Stack 的 Connect 和 ComputeAdmin 模組：</span><span class="sxs-lookup"><span data-stu-id="6a274-125">Import the Azure Stack Connect and ComputeAdmin modules by using the following commands:</span></span>

   ```powershell
   Set-ExecutionPolicy RemoteSigned

   # import the Connect and ComputeAdmin modules   
   Import-Module .\Connect\AzureStack.Connect.psm1
   Import-Module .\ComputeAdmin\AzureStack.ComputeAdmin.psm1

   ```

2. <span data-ttu-id="6a274-126">登入您的 Azure Stack 環境。</span><span class="sxs-lookup"><span data-stu-id="6a274-126">Sign in to your Azure Stack environment.</span></span> <span data-ttu-id="6a274-127">根據部署您 Azure Stack 環境時使用的是 AAD 還是 AD FS (請務必取代 AAD 租用戶名稱) 而定，執行下列指令碼：</span><span class="sxs-lookup"><span data-stu-id="6a274-127">Run the following script depending on if your Azure Stack environment is deployed by using AAD or AD FS (Make sure to replace the AAD tenant name):</span></span>  

   <span data-ttu-id="6a274-128">a.</span><span class="sxs-lookup"><span data-stu-id="6a274-128">a.</span></span> <span data-ttu-id="6a274-129">**Azure Active Directory** - 使用下列 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="6a274-129">**Azure Active Directory**, use the following cmdlet:</span></span>

   ```PowerShell
   # Create the Azure Stack cloud administrator's AzureRM environment by using the following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint "https://adminmanagement.local.azurestack.external" 

   Set-AzureRmEnvironment `
    -Name "AzureStackAdmin" `
    -GraphAudience "https://graph.windows.net/"

   $TenantID = Get-AzsDirectoryTenantId `
     -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
     -EnvironmentName AzureStackAdmin

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```

   <span data-ttu-id="6a274-130">b.</span><span class="sxs-lookup"><span data-stu-id="6a274-130">b.</span></span> <span data-ttu-id="6a274-131">**Active Directory 同盟服務** - 使用下列 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="6a274-131">**Active Directory Federation Services**, use the following cmdlet:</span></span>
    
   ```PowerShell
   # Create the Azure Stack cloud administrator's AzureRM environment by using the following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint "https://adminmanagement.local.azurestack.external"

   Set-AzureRmEnvironment `
     -Name "AzureStackAdmin" `
     -GraphAudience "https://graph.local.azurestack.external/" `
     -EnableAdfsAuthentication:$true

   $TenantID = Get-AzsDirectoryTenantId `
     -ADFS 
     -EnvironmentName AzureStackAdmin 

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```
   
3. <span data-ttu-id="6a274-132">將 Windows Server 2016 映像新增到 Azure Stack 市集 (請務必以您所下載 WS2016 ISO 的路徑取代 *Path_to_ISO*)：</span><span class="sxs-lookup"><span data-stu-id="6a274-132">Add the Windows Server 2016 image to the Azure Stack marketplace (Make sure to replace the *Path_to_ISO* with the path to the WS2016 ISO you downloaded):</span></span>

   ```PowerShell
   $ISOPath = "<Fully_Qualified_Path_to_ISO>"

   # Add a Windows Server 2016 Evaluation VM Image.
   New-AzsServer2016VMImage `
     -ISOPath $ISOPath

   ```

<span data-ttu-id="6a274-133">若要確保 Windows Server 2016 VM 映像具有最新的累積更新，請在執行 `New-AzsServer2016VMImage` Cmdlet 時包含 `IncludeLatestCU` 參數。</span><span class="sxs-lookup"><span data-stu-id="6a274-133">To ensure that the Windows Server 2016 VM image has the latest cumulative update, include the `IncludeLatestCU` parameter when running the `New-AzsServer2016VMImage` cmdlet.</span></span> <span data-ttu-id="6a274-134">如需有關 `New-AzsServer2016VMImage` Cmdlet 所允許參數的資訊，請參閱[參數](#parameters)一節。</span><span class="sxs-lookup"><span data-stu-id="6a274-134">See the [Parameters](#parameters) section for information about allowed parameters for the `New-AzsServer2016VMImage` cmdlet.</span></span> <span data-ttu-id="6a274-135">將映像發行到 Azure Stack 市集需要大約一小時的時間。</span><span class="sxs-lookup"><span data-stu-id="6a274-135">It takes about an hour to publish the image to the Azure Stack marketplace.</span></span> 

## <a name="parameters"></a><span data-ttu-id="6a274-136">參數</span><span class="sxs-lookup"><span data-stu-id="6a274-136">Parameters</span></span>

|<span data-ttu-id="6a274-137">New-AzsServer2016VMImage 參數</span><span class="sxs-lookup"><span data-stu-id="6a274-137">New-AzsServer2016VMImage parameters</span></span>|<span data-ttu-id="6a274-138">必要？</span><span class="sxs-lookup"><span data-stu-id="6a274-138">Required?</span></span>|<span data-ttu-id="6a274-139">說明</span><span class="sxs-lookup"><span data-stu-id="6a274-139">Description</span></span>|
|-----|-----|------|
|<span data-ttu-id="6a274-140">ISOPath</span><span class="sxs-lookup"><span data-stu-id="6a274-140">ISOPath</span></span>|<span data-ttu-id="6a274-141">是</span><span class="sxs-lookup"><span data-stu-id="6a274-141">Yes</span></span>|<span data-ttu-id="6a274-142">所下載 Windows Server 2016 ISO 的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="6a274-142">The fully qualified path to the downloaded Windows Server 2016 ISO.</span></span>|
|<span data-ttu-id="6a274-143">Net35</span><span class="sxs-lookup"><span data-stu-id="6a274-143">Net35</span></span>|<span data-ttu-id="6a274-144">否</span><span class="sxs-lookup"><span data-stu-id="6a274-144">No</span></span>|<span data-ttu-id="6a274-145">此參數可讓您在 Windows Server 2016 映像上安裝 .NET 3.5 執行階段。</span><span class="sxs-lookup"><span data-stu-id="6a274-145">This parameter allows you to install the .NET 3.5 runtime on the Windows Server 2016 image.</span></span> <span data-ttu-id="6a274-146">此值預設會設定為 true。</span><span class="sxs-lookup"><span data-stu-id="6a274-146">By default, this value is set to true.</span></span> <span data-ttu-id="6a274-147">映像必須包含 .NET 3.5 執行階段，才能安裝 SQL 和 MYSQL 資源提供者。</span><span class="sxs-lookup"><span data-stu-id="6a274-147">It is mandatory that the image contains the .NET 3.5 runtime to install the SQL and MYSQL resource providers.</span></span> |
|<span data-ttu-id="6a274-148">版本</span><span class="sxs-lookup"><span data-stu-id="6a274-148">Version</span></span>|<span data-ttu-id="6a274-149">否</span><span class="sxs-lookup"><span data-stu-id="6a274-149">No</span></span>|<span data-ttu-id="6a274-150">此參數可讓您選擇是要新增 **Core** (核心)、**Full** (完整) Windows Server 2016 映像，還是 **Both** (兩者都新增)。</span><span class="sxs-lookup"><span data-stu-id="6a274-150">This parameter allows you to choose whether to add a **Core** or **Full** or **Both** Windows Server 2016 images.</span></span> <span data-ttu-id="6a274-151">此值預設會設定為 "Full"。</span><span class="sxs-lookup"><span data-stu-id="6a274-151">By default, this value is set to "Full."</span></span>|
|<span data-ttu-id="6a274-152">VHDSizeInMB</span><span class="sxs-lookup"><span data-stu-id="6a274-152">VHDSizeInMB</span></span>|<span data-ttu-id="6a274-153">否</span><span class="sxs-lookup"><span data-stu-id="6a274-153">No</span></span>|<span data-ttu-id="6a274-154">設定要新增到您 Azure Stack 環境之 VHD 映像的大小 (單位為 MB)。</span><span class="sxs-lookup"><span data-stu-id="6a274-154">Sets the size (in MB) of the VHD image to be added to your Azure Stack environment.</span></span> <span data-ttu-id="6a274-155">此值預設會設定為 40960 MB。</span><span class="sxs-lookup"><span data-stu-id="6a274-155">By default, this value is set to 40960 MB.</span></span>|
|<span data-ttu-id="6a274-156">CreateGalleryItem</span><span class="sxs-lookup"><span data-stu-id="6a274-156">CreateGalleryItem</span></span>|<span data-ttu-id="6a274-157">否</span><span class="sxs-lookup"><span data-stu-id="6a274-157">No</span></span>|<span data-ttu-id="6a274-158">指定是否應該為 Windows Server 2016 映像建立 Marketplace 項目。</span><span class="sxs-lookup"><span data-stu-id="6a274-158">Specifies if a Marketplace item should be created for the Windows Server 2016 image.</span></span> <span data-ttu-id="6a274-159">此值預設會設定為 true。</span><span class="sxs-lookup"><span data-stu-id="6a274-159">By default, this value is set to true.</span></span>|
|<span data-ttu-id="6a274-160">location</span><span class="sxs-lookup"><span data-stu-id="6a274-160">location</span></span> |<span data-ttu-id="6a274-161">否</span><span class="sxs-lookup"><span data-stu-id="6a274-161">No</span></span> |<span data-ttu-id="6a274-162">指定應作為 Windows Server 2016 映像發行目的地的位置。</span><span class="sxs-lookup"><span data-stu-id="6a274-162">Specifies the location to which the Windows Server 2016 image should be published.</span></span>|
|<span data-ttu-id="6a274-163">IncludeLatestCU</span><span class="sxs-lookup"><span data-stu-id="6a274-163">IncludeLatestCU</span></span>|<span data-ttu-id="6a274-164">否</span><span class="sxs-lookup"><span data-stu-id="6a274-164">No</span></span>|<span data-ttu-id="6a274-165">若要將最新的 Windows Server 2016 累積更新套用到新 VHD，請設定此參數。</span><span class="sxs-lookup"><span data-stu-id="6a274-165">Set this switch to apply the latest Windows Server 2016 cumulative update to the new VHD.</span></span>|
|<span data-ttu-id="6a274-166">CUUri</span><span class="sxs-lookup"><span data-stu-id="6a274-166">CUUri</span></span> |<span data-ttu-id="6a274-167">否</span><span class="sxs-lookup"><span data-stu-id="6a274-167">No</span></span> |<span data-ttu-id="6a274-168">若要從特定的 URI 選擇 Windows Server 2016 累積更新，請設定此值。</span><span class="sxs-lookup"><span data-stu-id="6a274-168">Set this value to choose the Windows Server 2016 cumulative update from a specific URI.</span></span> |
|<span data-ttu-id="6a274-169">CUPath</span><span class="sxs-lookup"><span data-stu-id="6a274-169">CUPath</span></span> |<span data-ttu-id="6a274-170">否</span><span class="sxs-lookup"><span data-stu-id="6a274-170">No</span></span> |<span data-ttu-id="6a274-171">若要從本機路徑選擇 Windows Server 2016 累積更新，請設定此值。</span><span class="sxs-lookup"><span data-stu-id="6a274-171">Set this value to choose the Windows Server 2016 cumulative update from a local path.</span></span> <span data-ttu-id="6a274-172">如果您是在已中斷連線的環境中部署 Azure Stack 執行個體，此選項會相當有用。</span><span class="sxs-lookup"><span data-stu-id="6a274-172">This option is helpful if you have deployed the Azure Stack instance in a disconnected environment.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="6a274-173">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6a274-173">Next steps</span></span>

[<span data-ttu-id="6a274-174">佈建虛擬機器</span><span class="sxs-lookup"><span data-stu-id="6a274-174">Provision a virtual machine</span></span>](azure-stack-provision-vm.md)
