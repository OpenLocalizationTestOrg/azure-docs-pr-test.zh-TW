---
title: "aaaAdd hello 預設 VM 映像 toohello Azure 堆疊 marketplace |Microsoft 文件"
description: "新增 hello Windows Server 2016 VM 預設映像 toohello 堆疊 Azure marketplace。"
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
ms.openlocfilehash: 9b5a6f4e4c73c706b059e3c3622a968b5eef9a27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-hello-windows-server-2016-vm-image-toohello-azure-stack-marketplace"></a><span data-ttu-id="68cc3-103">新增 hello Windows Server 2016 VM 映像 toohello 堆疊 Azure marketplace</span><span class="sxs-lookup"><span data-stu-id="68cc3-103">Add hello Windows Server 2016 VM image toohello Azure Stack marketplace</span></span>

<span data-ttu-id="68cc3-104">根據預設，沒有任何虛擬機器映像 hello Azure 堆疊 marketplace 中。</span><span class="sxs-lookup"><span data-stu-id="68cc3-104">By default, there aren’t any virtual machine images available in hello Azure Stack marketplace.</span></span> <span data-ttu-id="68cc3-105">hello Azure 堆疊雲端管理員必須將映像 toohello marketplace，使用者才能使用它們。</span><span class="sxs-lookup"><span data-stu-id="68cc3-105">hello Azure Stack cloud administrator must add an image toohello marketplace before users can use them.</span></span> <span data-ttu-id="68cc3-106">您可以加入 hello Windows Server 2016 映像 toohello 堆疊 Azure marketplace 使用其中一種 hello 下列兩種方法：</span><span class="sxs-lookup"><span data-stu-id="68cc3-106">You can add hello Windows Server 2016 image toohello Azure Stack marketplace by using one of hello following two methods:</span></span>

* <span data-ttu-id="68cc3-107">[從 hello Azure Marketplace 下載並新增 hello 映像](#add-the-image-by-downloading-it-from-the-Azure-marketplace)-如果您正在連線的案例中，而且您 Azure 堆疊的執行個體向 Azure 使用此選項。</span><span class="sxs-lookup"><span data-stu-id="68cc3-107">[Add hello image by downloading it from hello Azure Marketplace](#add-the-image-by-downloading-it-from-the-Azure-marketplace) - Use this option if you are operating in a connected scenario and if you have registered your Azure Stack instance with Azure.</span></span>

* <span data-ttu-id="68cc3-108">[使用 PowerShell 新增 hello 映像](#add-the-image-by-using-powershell)-使用此選項，如果您部署了 Azure 堆疊在中斷連接案例或案例中具有有限的連線。</span><span class="sxs-lookup"><span data-stu-id="68cc3-108">[Add hello image by using PowerShell](#add-the-image-by-using-powershell) - Use this option if you have deployed Azure Stack in a disconnected scenario or in scenarios with limited connectivity.</span></span>

## <a name="add-hello-image-by-downloading-it-from-hello-azure-marketplace"></a><span data-ttu-id="68cc3-109">從 hello Azure Marketplace 下載並新增 hello 映像</span><span class="sxs-lookup"><span data-stu-id="68cc3-109">Add hello image by downloading it from hello Azure Marketplace</span></span>

1. <span data-ttu-id="68cc3-110">部署之後 Azure 堆疊，請登入 tooyour Azure 堆疊開發套件。</span><span class="sxs-lookup"><span data-stu-id="68cc3-110">After deploying Azure Stack, sign in tooyour Azure Stack Development Kit.</span></span>

2. <span data-ttu-id="68cc3-111">按一下 [更多服務] > [市集管理] > [從 Azure 新增]</span><span class="sxs-lookup"><span data-stu-id="68cc3-111">click **More services** > **Marketplace Management** > **Add from Azure**</span></span> 

3. <span data-ttu-id="68cc3-112">尋找或搜尋 hello **Windows Server 2016 Datacenter Eval**影像 > 按一下**下載**</span><span class="sxs-lookup"><span data-stu-id="68cc3-112">Find or search for hello **Windows Server 2016 Datacenter – Eval** image > click **Download**</span></span>

   ![從 Azure 下載映像](media/azure-stack-add-default-image/download-image.png)

<span data-ttu-id="68cc3-114">Hello 影像 hello 下載完成之後，會新增 toohello **Marketplace 管理**刀鋒視窗，它也可從 hello**虛擬機器**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="68cc3-114">After hello download completes, hello image is added toohello **Marketplace Management** blade and it is also made available from hello **Virtual Machines** blade.</span></span>

## <a name="add-hello-image-by-using-powershell"></a><span data-ttu-id="68cc3-115">使用 PowerShell 新增 hello 映像</span><span class="sxs-lookup"><span data-stu-id="68cc3-115">Add hello image by using PowerShell</span></span>

### <a name="prerequisites"></a><span data-ttu-id="68cc3-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="68cc3-116">Prerequisites</span></span> 

<span data-ttu-id="68cc3-117">執行下列必要條件 hello 從 hello[開發套件](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop)，或從 Windows 的外部用戶端如果您是[透過 VPN 連線](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span><span class="sxs-lookup"><span data-stu-id="68cc3-117">Run hello following prerequisites either from hello [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span></span>

* <span data-ttu-id="68cc3-118">安裝 [Azure Stack 相容的 Azure PowerShell 模組](azure-stack-powershell-install.md)。</span><span class="sxs-lookup"><span data-stu-id="68cc3-118">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  

* <span data-ttu-id="68cc3-119">下載 hello [Azure 堆疊的工具需要的 toowork](azure-stack-powershell-download.md)。</span><span class="sxs-lookup"><span data-stu-id="68cc3-119">Download hello [tools required toowork with Azure Stack](azure-stack-powershell-download.md).</span></span>  

* <span data-ttu-id="68cc3-120">Toohttps://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016，並下載 Windows Server 2016 hello 評估。</span><span class="sxs-lookup"><span data-stu-id="68cc3-120">Go toohttps://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016 and download hello Windows Server 2016 evaluation.</span></span> <span data-ttu-id="68cc3-121">出現提示時，選取 hello **ISO** hello 下載的版本。</span><span class="sxs-lookup"><span data-stu-id="68cc3-121">When prompted, select hello **ISO** version of hello download.</span></span> <span data-ttu-id="68cc3-122">資料錄 hello 路徑 toohello 下載位置，使用稍後的步驟執行。</span><span class="sxs-lookup"><span data-stu-id="68cc3-122">Record hello path toohello download location, which is used later in these steps.</span></span> <span data-ttu-id="68cc3-123">此步驟需要網際網路連線能力。</span><span class="sxs-lookup"><span data-stu-id="68cc3-123">This step requires internet connectivity.</span></span>  

<span data-ttu-id="68cc3-124">現在，執行下列步驟 tooadd hello 映像 toohello 堆疊 Azure marketplace 的 hello:</span><span class="sxs-lookup"><span data-stu-id="68cc3-124">Now run hello following steps tooadd hello image toohello Azure Stack marketplace:</span></span>
   
1. <span data-ttu-id="68cc3-125">使用下列命令的 hello 匯入 hello Azure 堆疊 Connect 和 ComputeAdmin 模組：</span><span class="sxs-lookup"><span data-stu-id="68cc3-125">Import hello Azure Stack Connect and ComputeAdmin modules by using hello following commands:</span></span>

   ```powershell
   Set-ExecutionPolicy RemoteSigned

   # import hello Connect and ComputeAdmin modules   
   Import-Module .\Connect\AzureStack.Connect.psm1
   Import-Module .\ComputeAdmin\AzureStack.ComputeAdmin.psm1

   ```

2. <span data-ttu-id="68cc3-126">登入 tooyour Azure 堆疊環境。</span><span class="sxs-lookup"><span data-stu-id="68cc3-126">Sign in tooyour Azure Stack environment.</span></span> <span data-ttu-id="68cc3-127">如果您的 Azure 堆疊環境部署使用 AAD 或 AD FS （請確定 tooreplace hello AAD 租用戶名稱），取決於指令碼執行的 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="68cc3-127">Run hello following script depending on if your Azure Stack environment is deployed by using AAD or AD FS (Make sure tooreplace hello AAD tenant name):</span></span>  

   <span data-ttu-id="68cc3-128">a.</span><span class="sxs-lookup"><span data-stu-id="68cc3-128">a.</span></span> <span data-ttu-id="68cc3-129">**Azure Active Directory**，使用下列 cmdlet 的 hello:</span><span class="sxs-lookup"><span data-stu-id="68cc3-129">**Azure Active Directory**, use hello following cmdlet:</span></span>

   ```PowerShell
   # Create hello Azure Stack cloud administrator's AzureRM environment by using hello following cmdlet:
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

   <span data-ttu-id="68cc3-130">b.</span><span class="sxs-lookup"><span data-stu-id="68cc3-130">b.</span></span> <span data-ttu-id="68cc3-131">**Active Directory Federation Services**，使用下列 cmdlet 的 hello:</span><span class="sxs-lookup"><span data-stu-id="68cc3-131">**Active Directory Federation Services**, use hello following cmdlet:</span></span>
    
   ```PowerShell
   # Create hello Azure Stack cloud administrator's AzureRM environment by using hello following cmdlet:
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
   
3. <span data-ttu-id="68cc3-132">新增 Windows Server 2016 hello 映像 toohello 堆疊 Azure marketplace (請確定 tooreplace hello *Path_to_ISO*與 hello 路徑 toohello WS2016 您下載的 ISO):</span><span class="sxs-lookup"><span data-stu-id="68cc3-132">Add hello Windows Server 2016 image toohello Azure Stack marketplace (Make sure tooreplace hello *Path_to_ISO* with hello path toohello WS2016 ISO you downloaded):</span></span>

   ```PowerShell
   $ISOPath = "<Fully_Qualified_Path_to_ISO>"

   # Add a Windows Server 2016 Evaluation VM Image.
   New-AzsServer2016VMImage `
     -ISOPath $ISOPath

   ```

<span data-ttu-id="68cc3-133">hello Windows Server 2016 VM 映像的 tooensure 具有 hello 最新累積更新，包括 hello`IncludeLatestCU`參數執行 hello 時`New-AzsServer2016VMImage`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="68cc3-133">tooensure that hello Windows Server 2016 VM image has hello latest cumulative update, include hello `IncludeLatestCU` parameter when running hello `New-AzsServer2016VMImage` cmdlet.</span></span> <span data-ttu-id="68cc3-134">請參閱 hello[參數](#parameters)> 一節有關如何允許參數 hello `New-AzsServer2016VMImage` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="68cc3-134">See hello [Parameters](#parameters) section for information about allowed parameters for hello `New-AzsServer2016VMImage` cmdlet.</span></span> <span data-ttu-id="68cc3-135">它採用有關小時 toopublish hello 映像 toohello 堆疊 Azure marketplace。</span><span class="sxs-lookup"><span data-stu-id="68cc3-135">It takes about an hour toopublish hello image toohello Azure Stack marketplace.</span></span> 

## <a name="parameters"></a><span data-ttu-id="68cc3-136">參數</span><span class="sxs-lookup"><span data-stu-id="68cc3-136">Parameters</span></span>

|<span data-ttu-id="68cc3-137">New-AzsServer2016VMImage 參數</span><span class="sxs-lookup"><span data-stu-id="68cc3-137">New-AzsServer2016VMImage parameters</span></span>|<span data-ttu-id="68cc3-138">必要？</span><span class="sxs-lookup"><span data-stu-id="68cc3-138">Required?</span></span>|<span data-ttu-id="68cc3-139">說明</span><span class="sxs-lookup"><span data-stu-id="68cc3-139">Description</span></span>|
|-----|-----|------|
|<span data-ttu-id="68cc3-140">ISOPath</span><span class="sxs-lookup"><span data-stu-id="68cc3-140">ISOPath</span></span>|<span data-ttu-id="68cc3-141">是</span><span class="sxs-lookup"><span data-stu-id="68cc3-141">Yes</span></span>|<span data-ttu-id="68cc3-142">hello 的完整的路徑 toohello 下載 Windows Server 2016 ISO。</span><span class="sxs-lookup"><span data-stu-id="68cc3-142">hello fully qualified path toohello downloaded Windows Server 2016 ISO.</span></span>|
|<span data-ttu-id="68cc3-143">Net35</span><span class="sxs-lookup"><span data-stu-id="68cc3-143">Net35</span></span>|<span data-ttu-id="68cc3-144">否</span><span class="sxs-lookup"><span data-stu-id="68cc3-144">No</span></span>|<span data-ttu-id="68cc3-145">這個參數可讓您 tooinstall hello.NET 3.5 執行階段 hello Windows Server 2016 映像上。</span><span class="sxs-lookup"><span data-stu-id="68cc3-145">This parameter allows you tooinstall hello .NET 3.5 runtime on hello Windows Server 2016 image.</span></span> <span data-ttu-id="68cc3-146">根據預設，這個值會設定 tootrue。</span><span class="sxs-lookup"><span data-stu-id="68cc3-146">By default, this value is set tootrue.</span></span> <span data-ttu-id="68cc3-147">它是強制該 hello 映像包含.NET 3.5 hello 執行階段 tooinstall hello SQL 和 MYSQL 資源提供者。</span><span class="sxs-lookup"><span data-stu-id="68cc3-147">It is mandatory that hello image contains hello .NET 3.5 runtime tooinstall hello SQL and MYSQL resource providers.</span></span> |
|<span data-ttu-id="68cc3-148">版本</span><span class="sxs-lookup"><span data-stu-id="68cc3-148">Version</span></span>|<span data-ttu-id="68cc3-149">否</span><span class="sxs-lookup"><span data-stu-id="68cc3-149">No</span></span>|<span data-ttu-id="68cc3-150">此參數可讓您 toochoose 是否 tooadd**核心**或**完整**或**兩者**Windows Server 2016 映像。</span><span class="sxs-lookup"><span data-stu-id="68cc3-150">This parameter allows you toochoose whether tooadd a **Core** or **Full** or **Both** Windows Server 2016 images.</span></span> <span data-ttu-id="68cc3-151">根據預設，這個值會設定過 「 完整。 」</span><span class="sxs-lookup"><span data-stu-id="68cc3-151">By default, this value is set too"Full."</span></span>|
|<span data-ttu-id="68cc3-152">VHDSizeInMB</span><span class="sxs-lookup"><span data-stu-id="68cc3-152">VHDSizeInMB</span></span>|<span data-ttu-id="68cc3-153">否</span><span class="sxs-lookup"><span data-stu-id="68cc3-153">No</span></span>|<span data-ttu-id="68cc3-154">設定 hello 大小 （以 mb 為單位） 的 hello VHD 映像 toobe 加入 tooyour Azure 堆疊環境。</span><span class="sxs-lookup"><span data-stu-id="68cc3-154">Sets hello size (in MB) of hello VHD image toobe added tooyour Azure Stack environment.</span></span> <span data-ttu-id="68cc3-155">根據預設，這個值會設定 too40960 MB。</span><span class="sxs-lookup"><span data-stu-id="68cc3-155">By default, this value is set too40960 MB.</span></span>|
|<span data-ttu-id="68cc3-156">CreateGalleryItem</span><span class="sxs-lookup"><span data-stu-id="68cc3-156">CreateGalleryItem</span></span>|<span data-ttu-id="68cc3-157">否</span><span class="sxs-lookup"><span data-stu-id="68cc3-157">No</span></span>|<span data-ttu-id="68cc3-158">指定是否應建立 hello Windows Server 2016 映像的 Marketplace 項目。</span><span class="sxs-lookup"><span data-stu-id="68cc3-158">Specifies if a Marketplace item should be created for hello Windows Server 2016 image.</span></span> <span data-ttu-id="68cc3-159">根據預設，這個值會設定 tootrue。</span><span class="sxs-lookup"><span data-stu-id="68cc3-159">By default, this value is set tootrue.</span></span>|
|<span data-ttu-id="68cc3-160">location</span><span class="sxs-lookup"><span data-stu-id="68cc3-160">location</span></span> |<span data-ttu-id="68cc3-161">否</span><span class="sxs-lookup"><span data-stu-id="68cc3-161">No</span></span> |<span data-ttu-id="68cc3-162">指定應該發行 hello 位置 toowhich hello Windows Server 2016 映像。</span><span class="sxs-lookup"><span data-stu-id="68cc3-162">Specifies hello location toowhich hello Windows Server 2016 image should be published.</span></span>|
|<span data-ttu-id="68cc3-163">IncludeLatestCU</span><span class="sxs-lookup"><span data-stu-id="68cc3-163">IncludeLatestCU</span></span>|<span data-ttu-id="68cc3-164">否</span><span class="sxs-lookup"><span data-stu-id="68cc3-164">No</span></span>|<span data-ttu-id="68cc3-165">設定此參數 tooapply hello 最新 Windows Server 2016 累計更新 toohello 新的 VHD。</span><span class="sxs-lookup"><span data-stu-id="68cc3-165">Set this switch tooapply hello latest Windows Server 2016 cumulative update toohello new VHD.</span></span>|
|<span data-ttu-id="68cc3-166">CUUri</span><span class="sxs-lookup"><span data-stu-id="68cc3-166">CUUri</span></span> |<span data-ttu-id="68cc3-167">否</span><span class="sxs-lookup"><span data-stu-id="68cc3-167">No</span></span> |<span data-ttu-id="68cc3-168">從特定的 URI 設定此值 toochoose hello Windows Server 2016 累計更新。</span><span class="sxs-lookup"><span data-stu-id="68cc3-168">Set this value toochoose hello Windows Server 2016 cumulative update from a specific URI.</span></span> |
|<span data-ttu-id="68cc3-169">CUPath</span><span class="sxs-lookup"><span data-stu-id="68cc3-169">CUPath</span></span> |<span data-ttu-id="68cc3-170">否</span><span class="sxs-lookup"><span data-stu-id="68cc3-170">No</span></span> |<span data-ttu-id="68cc3-171">設定此值 toochoose hello Windows Server 2016 累積更新從本機路徑。</span><span class="sxs-lookup"><span data-stu-id="68cc3-171">Set this value toochoose hello Windows Server 2016 cumulative update from a local path.</span></span> <span data-ttu-id="68cc3-172">這個選項很有用，如果您已部署的 hello Azure 堆疊的執行個體中斷連線的環境中。</span><span class="sxs-lookup"><span data-stu-id="68cc3-172">This option is helpful if you have deployed hello Azure Stack instance in a disconnected environment.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="68cc3-173">後續步驟</span><span class="sxs-lookup"><span data-stu-id="68cc3-173">Next steps</span></span>

[<span data-ttu-id="68cc3-174">佈建虛擬機器</span><span class="sxs-lookup"><span data-stu-id="68cc3-174">Provision a virtual machine</span></span>](azure-stack-provision-vm.md)
