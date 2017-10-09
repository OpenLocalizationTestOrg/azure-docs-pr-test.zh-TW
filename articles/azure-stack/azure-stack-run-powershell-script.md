---
title: "aaaDeploy hello Azure 堆疊開發套件 |Microsoft 文件"
description: "了解如何在 tooprepare hello Azure 堆疊開發套件及執行的 hello PowerShell 指令碼 toodeploy 它。"
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 0ad02941-ed14-4888-8695-b82ad6e43c66
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/17/2017
ms.author: erikje
ms.openlocfilehash: a96879fb91000f6b3d3aac3089861e8a573ebead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-azure-stack-development-kit"></a><span data-ttu-id="91858-103">部署 hello Azure 堆疊開發套件</span><span class="sxs-lookup"><span data-stu-id="91858-103">Deploy hello Azure Stack Development Kit</span></span>
<span data-ttu-id="91858-104">toodeploy hello 開發套件，您必須完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="91858-104">toodeploy hello development kit, you must complete hello following steps:</span></span>

1. <span data-ttu-id="91858-105">[下載 hello 部署套件](https://azure.microsoft.com/overview/azure-stack/try/?v=try)tooget hello Cloudbuilder.vhdx。</span><span class="sxs-lookup"><span data-stu-id="91858-105">[Download hello deployment package](https://azure.microsoft.com/overview/azure-stack/try/?v=try) tooget hello Cloudbuilder.vhdx.</span></span>
2. <span data-ttu-id="91858-106">[準備 hello cloudbuilder.vhdx](#prepare-the-development-kit-host)執行 hello asdk installer.ps1 指令碼 tooconfigure hello 電腦 （hello 開發套件主機），您會想 tooinstall 開發套件。</span><span class="sxs-lookup"><span data-stu-id="91858-106">[Prepare hello cloudbuilder.vhdx](#prepare-the-development-kit-host) by running hello asdk-installer.ps1 script tooconfigure hello computer (hello development kit host) on which you want tooinstall development kit.</span></span> <span data-ttu-id="91858-107">這個步驟之後，hello 開發套件主機將會開機 toohello Cloudbuilder.vhdx。</span><span class="sxs-lookup"><span data-stu-id="91858-107">After this step, hello development kit host will boot toohello Cloudbuilder.vhdx.</span></span>
3. <span data-ttu-id="91858-108">[部署 hello 開發套件](#deploy-the-development-kit)hello 開發套件主機上。</span><span class="sxs-lookup"><span data-stu-id="91858-108">[Deploy hello development kit](#deploy-the-development-kit) on hello development kit host.</span></span>

> [!NOTE]
> <span data-ttu-id="91858-109">獲得最佳結果，即使您希望 toouse 中斷連線的 Azure 堆疊環境，它是連接 toohello 時的最佳 toodeploy 網際網路。</span><span class="sxs-lookup"><span data-stu-id="91858-109">For best results, even if you want toouse a disconnected Azure Stack environment, it is best toodeploy while connected toohello internet.</span></span> <span data-ttu-id="91858-110">這樣一來，您可以在部署期間啟動 hello Windows Server 2016 評估版。</span><span class="sxs-lookup"><span data-stu-id="91858-110">That way, hello Windows Server 2016 evaluation version can be activated at deployment time.</span></span> <span data-ttu-id="91858-111">如果在 10 天內未啟動 hello Windows Server 2016 評估版，它會關閉。</span><span class="sxs-lookup"><span data-stu-id="91858-111">If hello Windows Server 2016 evaluation version is not activated within 10 days, it shuts down.</span></span>
> 
> 

## <a name="download-and-extract-hello-development-kit"></a><span data-ttu-id="91858-112">下載並解壓縮 hello 開發套件</span><span class="sxs-lookup"><span data-stu-id="91858-112">Download and extract hello development kit</span></span>
1. <span data-ttu-id="91858-113">Hello 下載開始之前，請確定您的電腦符合下列必要條件 hello:</span><span class="sxs-lookup"><span data-stu-id="91858-113">Before you start hello download, make sure that your computer meets hello following prerequisites:</span></span>

   * <span data-ttu-id="91858-114">hello 電腦必須至少為 60 GB 的可用磁碟空間。</span><span class="sxs-lookup"><span data-stu-id="91858-114">hello computer must have at least 60 GB of free disk space.</span></span>
   * <span data-ttu-id="91858-115">必須安裝 [.NET framework 4.6 (或更新版本)](https://aka.ms/r6mkiy)。</span><span class="sxs-lookup"><span data-stu-id="91858-115">[.NET Framework 4.6 (or a later version)](https://aka.ms/r6mkiy) must be installed.</span></span>

2. <span data-ttu-id="91858-116">[移 toohello 開始頁面](https://azure.microsoft.com/overview/azure-stack/try/?v=try)，提供您詳細資料，然後按一下**送出**。</span><span class="sxs-lookup"><span data-stu-id="91858-116">[Go toohello Get Started page](https://azure.microsoft.com/overview/azure-stack/try/?v=try), provide your details, and click **Submit**.</span></span>
3. <span data-ttu-id="91858-117">在下**下載 hello 軟體**，按一下  **Azure 堆疊開發套件**。</span><span class="sxs-lookup"><span data-stu-id="91858-117">Under **Download hello software**, click **Azure Stack Development Kit**.</span></span>
4. <span data-ttu-id="91858-118">執行下載的 hello AzureStackDownloader.exe 檔案。</span><span class="sxs-lookup"><span data-stu-id="91858-118">Run hello downloaded AzureStackDownloader.exe file.</span></span>
5. <span data-ttu-id="91858-119">在 [hello **Azure 堆疊開發套件程式下載程式**] 視窗中，遵循步驟 1 至 5。</span><span class="sxs-lookup"><span data-stu-id="91858-119">In hello **Azure Stack Development Kit Downloader** window, follow steps 1 through 5.</span></span>
6. <span data-ttu-id="91858-120">Hello 下載完成之後，請按一下**執行**toolaunch hello MicrosoftAzureStackPOC.exe。</span><span class="sxs-lookup"><span data-stu-id="91858-120">After hello download completes, click **Run** toolaunch hello MicrosoftAzureStackPOC.exe.</span></span>
7. <span data-ttu-id="91858-121">檢閱 hello 授權合約 畫面和 hello 自我解壓縮程式精靈的資訊，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="91858-121">Review hello License Agreement screen and information of hello Self-Extractor Wizard and then click **Next**.</span></span>
8. <span data-ttu-id="91858-122">檢閱 hello 隱私權聲明螢幕和 hello 自我解壓縮程式精靈的資訊，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="91858-122">Review hello Privacy Statement screen and information of hello Self-Extractor Wizard and then click **Next**.</span></span>
9. <span data-ttu-id="91858-123">選取 hello hello 的目的地檔案 toobe 解壓縮，請按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="91858-123">Select hello Destination for hello files toobe extracted, click **Next**.</span></span>
   * <span data-ttu-id="91858-124">hello 預設值是： <drive letter>:\<目前資料夾 > \Microsoft Azure 堆疊</span><span class="sxs-lookup"><span data-stu-id="91858-124">hello default is: <drive letter>:\<current folder>\Microsoft Azure Stack</span></span>
10. <span data-ttu-id="91858-125">檢閱 hello 目的地位置 畫面和 hello 自我解壓縮程式精靈的資訊，然後按一下**擷取**tooextract hello CloudBuilder.vhdx (~ 25 GB) 及 ThirdPartyLicenses.rtf 檔案。</span><span class="sxs-lookup"><span data-stu-id="91858-125">Review hello Destination location screen and information of hello Self-Extractor Wizard, and then click **Extract** tooextract hello CloudBuilder.vhdx (~25 GB) and ThirdPartyLicenses.rtf files.</span></span> <span data-ttu-id="91858-126">此程序將需要一些時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="91858-126">This process will take some time toocomplete.</span></span>

> [!NOTE]
> <span data-ttu-id="91858-127">Hello 檔案解壓縮之後，您可以刪除 hello 機器上的 hello exe 和分類收納檔案 toorecover 空間。</span><span class="sxs-lookup"><span data-stu-id="91858-127">After you extract hello files, you can delete hello exe and bin files toorecover space on hello machine.</span></span> <span data-ttu-id="91858-128">或者，您可以移動這些檔案 tooanother 位置，如果您需要 tooredeploy 您就不需要 toodownload hello 檔案一次。</span><span class="sxs-lookup"><span data-stu-id="91858-128">Or, you can move these files tooanother location so that if you need tooredeploy you don’t need toodownload hello files again.</span></span>
> 
> 

## <a name="prepare-hello-development-kit-host"></a><span data-ttu-id="91858-129">準備 hello 開發套件主應用程式</span><span class="sxs-lookup"><span data-stu-id="91858-129">Prepare hello development kit host</span></span>
1. <span data-ttu-id="91858-130">請確定您可以實際連接 toohello 開發套件的主機，或存取實體主控台 （例如 KVM)。</span><span class="sxs-lookup"><span data-stu-id="91858-130">Make sure that you can physically connect toohello development kit host, or have physical console access (such as KVM).</span></span> <span data-ttu-id="91858-131">當您重新開機 hello 開發套件主應用程式在下面步驟 13，必須有這類存取。</span><span class="sxs-lookup"><span data-stu-id="91858-131">You must have such access after you reboot hello development kit host in step 13 below.</span></span>
2. <span data-ttu-id="91858-132">請確定 hello 開發套件主機符合 hello[最低需求](azure-stack-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="91858-132">Make sure hello development kit host meets hello [minimum requirements](azure-stack-deploy.md).</span></span> <span data-ttu-id="91858-133">您可以使用 hello[部署適用於 Azure 堆疊檢查程式](https://gallery.technet.microsoft.com/Deployment-Checker-for-50e0f51b)tooconfirm 您的需求。</span><span class="sxs-lookup"><span data-stu-id="91858-133">You can use hello [Deployment Checker for Azure Stack](https://gallery.technet.microsoft.com/Deployment-Checker-for-50e0f51b) tooconfirm your requirements.</span></span>
3. <span data-ttu-id="91858-134">以本機系統管理員 tooyour 開發套件主機 hello 登入。</span><span class="sxs-lookup"><span data-stu-id="91858-134">Sign in as hello Local Administrator tooyour development kit host.</span></span>
4. <span data-ttu-id="91858-135">複製或移動 hello CloudBuilder.vhdx 檔案 toohello 根目錄的 hello C:\ 磁碟機 (C:\CloudBuilder.vhdx)。</span><span class="sxs-lookup"><span data-stu-id="91858-135">Copy or move hello CloudBuilder.vhdx file toohello root of hello C:\ drive (C:\CloudBuilder.vhdx).</span></span>
5. <span data-ttu-id="91858-136">執行下列指令碼 toodownload hello 開發套件安裝程式檔案 (asdk installer.ps1) toohello c:\AzureStack_Installer 資料夾，您的開發套件主機上的 hello。</span><span class="sxs-lookup"><span data-stu-id="91858-136">Run hello following script toodownload hello development kit installer file (asdk-installer.ps1) toohello c:\AzureStack_Installer folder on your development kit host.</span></span>
    ```powershell
    # Variables
    $Uri = 'https://raw.githubusercontent.com/Azure/AzureStack-Tools/master/Deployment/asdk-installer.ps1'
    $LocalPath = 'c:\AzureStack_Installer'

    # Create folder
    New-Item $LocalPath -Type directory

    # Download file
    Invoke-WebRequest $uri -OutFile ($LocalPath + '\' + 'asdk-installer.ps1')
    ```
6. <span data-ttu-id="91858-137">開啟提升權限的 PowerShell 主控台 > 執行 hello C:\AzureStack_Installer\asdk-installer.ps1 指令碼 > 按一下**準備 vhdx**。</span><span class="sxs-lookup"><span data-stu-id="91858-137">Open an elevated PowerShell console > run hello C:\AzureStack_Installer\asdk-installer.ps1 script > click **Prepare vhdx**.</span></span>
7. <span data-ttu-id="91858-138">在 hello**選取 Cloudbuilder vhdx** hello 安裝程式中，瀏覽 tooand 選取 hello cloudbuilder.vhdx 下載檔案，在 hello 先前步驟中的頁面。</span><span class="sxs-lookup"><span data-stu-id="91858-138">On hello **Select Cloudbuilder vhdx** page of hello installer, browse tooand select hello cloudbuilder.vhdx file that you downloaded in hello previous steps.</span></span>
8. <span data-ttu-id="91858-139">選擇性： 核取 hello**新增驅動程式**方塊 toospecify 包含您想 hello 主機的其他驅動程式的資料夾。</span><span class="sxs-lookup"><span data-stu-id="91858-139">Optional: Check hello **Add drivers** box toospecify a folder containing additional drivers that you want on hello host.</span></span>
9. <span data-ttu-id="91858-140">在 hello**選擇性設定**頁面上，提供 hello hello 開發套件主機的本機系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="91858-140">On hello **Optional settings** page, provide hello local administrator account for hello development kit host.</span></span> <span data-ttu-id="91858-141">如果您沒有提供這些認證，您將在下方的 hello 安裝程序期間需要 KVM 存取 toohello 主機。</span><span class="sxs-lookup"><span data-stu-id="91858-141">If you don't provide these credentials, you'll need KVM access toohello host during hello install process below.</span></span>
10. <span data-ttu-id="91858-142">也在 hello**選擇性設定**頁面上，您可以遵循 hello 選項 tooset hello:</span><span class="sxs-lookup"><span data-stu-id="91858-142">Also on hello **Optional settings** page, you have hello option tooset hello following:</span></span>
    - <span data-ttu-id="91858-143">**Computername**： 這個選項會設定 hello hello 開發套件主機名稱。</span><span class="sxs-lookup"><span data-stu-id="91858-143">**Computername**: This option sets hello name for hello development kit host.</span></span> <span data-ttu-id="91858-144">hello 名稱必須符合 FQDN 需求，而且必須是 15 個字元長度等於或小於。</span><span class="sxs-lookup"><span data-stu-id="91858-144">hello name must comply with FQDN requirements and must be 15 characters or less in length.</span></span> <span data-ttu-id="91858-145">hello 預設是由 Windows 產生隨機的電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="91858-145">hello default is a random computer name generated by Windows.</span></span>
    - <span data-ttu-id="91858-146">**時區**： 集 hello hello 開發套件主機的時區。</span><span class="sxs-lookup"><span data-stu-id="91858-146">**Time zone**: Sets hello time zone for hello development kit host.</span></span> <span data-ttu-id="91858-147">hello 預設值是 (UTC-8:00) 太平洋時間 （美國和加拿大）。</span><span class="sxs-lookup"><span data-stu-id="91858-147">hello default is (UTC-8:00) Pacific Time (US & Canada).</span></span>
    - <span data-ttu-id="91858-148">**靜態 IP 組態**： 設定部署 toouse 靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="91858-148">**Static IP configuration**: Sets your deployment toouse a static IP address.</span></span> <span data-ttu-id="91858-149">否則，當 hello installer hello cloudbuilder.vhx 重新開機，hello 網路介面設定的 DHCP。</span><span class="sxs-lookup"><span data-stu-id="91858-149">Otherwise, when hello installer reboots into hello cloudbuilder.vhx, hello network interfaces are configured with DHCP.</span></span>
11. <span data-ttu-id="91858-150">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="91858-150">Click **Next**.</span></span>
12. <span data-ttu-id="91858-151">如果您選擇靜態 IP 組態 hello 上一個步驟中，您必須立即：</span><span class="sxs-lookup"><span data-stu-id="91858-151">If you chose a static IP configuration in hello previous step, you must now:</span></span>
    - <span data-ttu-id="91858-152">選取網路介面卡。</span><span class="sxs-lookup"><span data-stu-id="91858-152">Select a network adapter.</span></span> <span data-ttu-id="91858-153">請確定您可以連接 toohello 配接器，再按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="91858-153">Make sure you can connect toohello adapter before you click **Next**.</span></span>
    - <span data-ttu-id="91858-154">請確定該 hello **IP 位址**，**閘道**，和**DNS**值正確無誤，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="91858-154">Make sure that hello **IP address**, **Gateway**, and **DNS** values are correct and then click **Next**.</span></span>
13. <span data-ttu-id="91858-155">按一下**下一步**toostart hello 準備程序。</span><span class="sxs-lookup"><span data-stu-id="91858-155">Click **Next** toostart hello preparation process.</span></span>
14. <span data-ttu-id="91858-156">當 hello 準備表示**已完成**，按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="91858-156">When hello preparation indicates **Completed**, click **Next**.</span></span>
15. <span data-ttu-id="91858-157">按一下**立即重新開機**到 hello cloudbuilder.vhdx tooboot 並繼續 hello 部署程序。</span><span class="sxs-lookup"><span data-stu-id="91858-157">Click **Reboot now** tooboot into hello cloudbuilder.vhdx and continue hello deployment process.</span></span>

## <a name="deploy-hello-development-kit"></a><span data-ttu-id="91858-158">部署 hello 開發套件</span><span class="sxs-lookup"><span data-stu-id="91858-158">Deploy hello development kit</span></span>
1. <span data-ttu-id="91858-159">以本機系統管理員 toohello 開發套件主機 hello 登入。</span><span class="sxs-lookup"><span data-stu-id="91858-159">Sign in as hello Local Administrator toohello development kit host.</span></span> <span data-ttu-id="91858-160">使用 hello hello 先前步驟中指定的認證。</span><span class="sxs-lookup"><span data-stu-id="91858-160">Use hello credentials specified in hello previous steps.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="91858-161">Azure Active Directory 部署中，Azure 堆疊需要存取 toohello 網際網路，直接或透過 transparent proxy。</span><span class="sxs-lookup"><span data-stu-id="91858-161">For Azure Active Directory deployments, Azure Stack requires access toohello Internet, either directly or through a transparent proxy.</span></span> <span data-ttu-id="91858-162">hello 部署支援只有一個 NIC 的網路功能。</span><span class="sxs-lookup"><span data-stu-id="91858-162">hello deployment supports exactly one NIC for networking.</span></span> <span data-ttu-id="91858-163">如果您有多個 Nic 時，請確定只有一個已啟用 （，其他所有項目已停用） 才能執行 hello 下一節中的 hello 部署指令碼。</span><span class="sxs-lookup"><span data-stu-id="91858-163">If you have multiple NICs, make sure that only one is enabled (and all others are disabled) before running hello deployment script in hello next section.</span></span>
    
2. <span data-ttu-id="91858-164">開啟提升權限的 PowerShell 主控台 > 執行 hello \AzureStack_Installer\asdk-installer.ps1 指令碼 （這可能是在 hello Cloudbuilder.vhdx 中的不同磁碟機上） > 按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="91858-164">Open an elevated PowerShell console > run hello \AzureStack_Installer\asdk-installer.ps1 script (which may be on a different drive in hello Cloudbuilder.vhdx) > click **Install**.</span></span>
3. <span data-ttu-id="91858-165">在 hello**類型**方塊中，選取**Azure 雲端**或**ADFS**。</span><span class="sxs-lookup"><span data-stu-id="91858-165">In hello **Type** box, select **Azure Cloud** or **ADFS**.</span></span>
    - <span data-ttu-id="91858-166">**Azure 雲端**: Azure Active Directory 是 hello 身分識別提供者。</span><span class="sxs-lookup"><span data-stu-id="91858-166">**Azure Cloud**: Azure Active Directory is hello identity provider.</span></span> <span data-ttu-id="91858-167">使用此參數 toospecify 特定目錄 hello AAD 帳戶具有全域系統管理員權限的位置。</span><span class="sxs-lookup"><span data-stu-id="91858-167">Use this parameter toospecify a specific directory where hello AAD account has global admin permissions.</span></span> <span data-ttu-id="91858-168">AAD 目錄租用戶中的 hello 格式的完整名稱。.onmicrosoft.com。</span><span class="sxs-lookup"><span data-stu-id="91858-168">Full name of an AAD Directory tenant in hello format of .onmicrosoft.com.</span></span> 
    - <span data-ttu-id="91858-169">**ADFS**: hello 預設戳記目錄服務是 hello 身分識別提供者，在與 hello 預設帳戶 toosign azurestackadmin@azurestack.local，而且 hello 密碼 toouse hello 您提供 hello 安裝程序。</span><span class="sxs-lookup"><span data-stu-id="91858-169">**ADFS**: hello default stamp Directory Service is hello identity provider, hello default account toosign in with is azurestackadmin@azurestack.local, and hello password toouse is hello one you provided as part of hello setup.</span></span>
4. <span data-ttu-id="91858-170">在下**本機系統管理員密碼**，在 hello**密碼** 方塊中，輸入 hello 本機系統管理員密碼 （它必須符合 hello 目前設定的本機系統管理員密碼），然後按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="91858-170">Under **Local administrator password**, in hello **Password** box, type hello local administrator password (which must match hello current configured local administrator password), and then click **Next**.</span></span>
5. <span data-ttu-id="91858-171">選取網路介面卡 toouse hello 開發套件，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="91858-171">Select a network adapter toouse for hello development kit and then click **Next**.</span></span>
6. <span data-ttu-id="91858-172">選取的 DHCP 或靜態的網路組態 hello BGPNAT01 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="91858-172">Select DHCP or static network configuration for hello BGPNAT01 virtual machine.</span></span>
    - <span data-ttu-id="91858-173">**DHCP** （預設值）： hello 虛擬機器從 hello DHCP 伺服器取得 hello IP 網路設定。</span><span class="sxs-lookup"><span data-stu-id="91858-173">**DHCP** (default): hello virtual machine gets hello IP network configuration from hello DHCP server.</span></span>
    - <span data-ttu-id="91858-174">**靜態**： 只有當 DHCP 無法指定有效的 IP 位址，如 Azure 堆疊 tooaccess hello 網際網路使用此選項。</span><span class="sxs-lookup"><span data-stu-id="91858-174">**Static**: Only use this option if DHCP can’t assign a valid IP address for Azure Stack tooaccess hello Internet.</span></span> <span data-ttu-id="91858-175">必須指定靜態 IP 位址與 hello 子網路遮罩長度 (例如，10.0.0.5/24)。</span><span class="sxs-lookup"><span data-stu-id="91858-175">A static IP address must be specified with hello subnetmask length (for example, 10.0.0.5/24).</span></span>
7. <span data-ttu-id="91858-176">選擇性地設定下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="91858-176">Optionally, set hello following values:</span></span>
    - <span data-ttu-id="91858-177">**VLAN ID**： 集 hello VLAN id。</span><span class="sxs-lookup"><span data-stu-id="91858-177">**VLAN ID**: Sets hello VLAN ID.</span></span> <span data-ttu-id="91858-178">只有當 hello 主機以及 AzS BGPNAT01 必須設定 VLAN ID tooaccess hello 實體網路 （與網際網路） 時，才能使用此選項。</span><span class="sxs-lookup"><span data-stu-id="91858-178">Only use this option if hello host and AzS-BGPNAT01 must configure VLAN ID tooaccess hello physical network (and Internet).</span></span> 
    - <span data-ttu-id="91858-179">**DNS 轉寄站**: hello Azure 堆疊部署的一部分建立的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="91858-179">**DNS forwarder**: A DNS server is created as part of hello Azure Stack deployment.</span></span> <span data-ttu-id="91858-180">tooallow hello 戳記 hello 方案 tooresolve 名稱內的電腦提供您現有基礎結構的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="91858-180">tooallow computers inside hello solution tooresolve names outside of hello stamp, provide your existing infrastructure DNS server.</span></span> <span data-ttu-id="91858-181">hello 戳記中 DNS 伺服器將轉寄無法辨識的名稱解析要求 toothis 伺服器。</span><span class="sxs-lookup"><span data-stu-id="91858-181">hello in-stamp DNS server forwards unknown name resolution requests toothis server.</span></span>
    - <span data-ttu-id="91858-182">**時間伺服器**：設定特定的時間伺服器。</span><span class="sxs-lookup"><span data-stu-id="91858-182">**Time server**: Sets a specific time server.</span></span> 
8. <span data-ttu-id="91858-183">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="91858-183">Click **Next**.</span></span> 
9. <span data-ttu-id="91858-184">在 [hello**驗證網路介面卡內容**] 頁面上，您會看到進度列。</span><span class="sxs-lookup"><span data-stu-id="91858-184">On hello **Verifying network interface card properties** page, you'll see a progress bar.</span></span> 
    - <span data-ttu-id="91858-185">如果，該處會指示**無法下載更新**，依照 hello 頁面上 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="91858-185">If it says **An update cannot be downloaded**, follow hello instructions on hello page.</span></span>
    - <span data-ttu-id="91858-186">顯示 [已完成] 時，按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="91858-186">When it says **Completed**, click **Next**.</span></span>
10. <span data-ttu-id="91858-187">在 [摘要] 頁面上，按一下 [部署]。</span><span class="sxs-lookup"><span data-stu-id="91858-187">On **Summary** page, click **Deploy**.</span></span>
11. <span data-ttu-id="91858-188">如果您使用 Azure Active Directory 部署，您將會詢問 tooenter 您 Azure Active Directory 的全域管理員帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="91858-188">If you're using an Azure Active Directory deployment, you'll be asked tooenter your Azure Active Directory global administrator account credentials.</span></span>
12. <span data-ttu-id="91858-189">hello 部署程序可能需要幾小時，期間 hello 系統會自動重新開機一次。</span><span class="sxs-lookup"><span data-stu-id="91858-189">hello deployment process can take a few hours, during which hello system automatically reboots once.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="91858-190">如果您想 toomonitor hello 部署進度，azurestack\AzureStackAdmin 身分登入。</span><span class="sxs-lookup"><span data-stu-id="91858-190">If you want toomonitor hello deployment progress, sign in as azurestack\AzureStackAdmin.</span></span> <span data-ttu-id="91858-191">如果您登入本機系統管理員 hello 機器之後加入 toohello 網域時，就看 hello 部署進度。</span><span class="sxs-lookup"><span data-stu-id="91858-191">If you sign in as a local admin after hello machine is joined toohello domain, you won't see hello deployment progress.</span></span> <span data-ttu-id="91858-192">請勿重新部署，而是登入為 azurestack\AzureStackAdmin toovalidate 它正在執行。</span><span class="sxs-lookup"><span data-stu-id="91858-192">Do not rerun deployment, instead sign in as azurestack\AzureStackAdmin toovalidate that it's running.</span></span>
   > 
   > 
   
    <span data-ttu-id="91858-193">Hello 部署成功時，會顯示 hello PowerShell 主控台：**完成： 動作 '部署'**。</span><span class="sxs-lookup"><span data-stu-id="91858-193">When hello deployment succeeds, hello PowerShell console displays: **COMPLETE: Action ‘Deployment’**.</span></span>
   
<span data-ttu-id="91858-194">如果 hello 部署失敗，您可以使用中的 hello 下列重新執行的 PowerShell 指令碼的 hello 相同提升權限的 PowerShell 視窗：</span><span class="sxs-lookup"><span data-stu-id="91858-194">If hello deployment fails, you can use hello following PowerShell rerun script from hello same elevated PowerShell window:</span></span>

```powershell
cd c:\CloudDeployment\Setup
.\InstallAzureStackPOC.ps1 -Rerun
```

<span data-ttu-id="91858-195">此指令碼會重新啟動 hello 成功的最後一個步驟中的 hello 部署。</span><span class="sxs-lookup"><span data-stu-id="91858-195">This script will restart hello deployment from hello last step that succeeded.</span></span>

<span data-ttu-id="91858-196">或者，您可以從頭開始[重新部署](azure-stack-redeploy.md)。</span><span class="sxs-lookup"><span data-stu-id="91858-196">Or, you can [redeploy](azure-stack-redeploy.md) from scratch.</span></span>


## <a name="reset-hello-password-expiration-too180-days"></a><span data-ttu-id="91858-197">重設 hello 密碼到期 too180 天數</span><span class="sxs-lookup"><span data-stu-id="91858-197">Reset hello password expiration too180 days</span></span>

<span data-ttu-id="91858-198">toomake 確定 hello 密碼到期的 hello 開發套件主應用程式不會太快，請遵循下列步驟部署之後：</span><span class="sxs-lookup"><span data-stu-id="91858-198">toomake sure that hello password for hello development kit host doesn't expire too soon, follow these steps after you deploy:</span></span>

1. <span data-ttu-id="91858-199">Hello 開發套件在主機上，開啟**群組原則管理**並瀏覽過**群組原則管理**–**樹系： azurestack.local** –**網域** – **azurestack.local**。</span><span class="sxs-lookup"><span data-stu-id="91858-199">On hello development kit host, open **Group Policy Management** and navigate too**Group Policy Management** – **Forest: azurestack.local** – **Domains** – **azurestack.local**.</span></span>
2. <span data-ttu-id="91858-200">以滑鼠右鍵按一下 [MemberServer]，然後按一下 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="91858-200">Right click on **MemberServer** and click **Edit**.</span></span>
3. <span data-ttu-id="91858-201">Hello 群組原則管理編輯器，在瀏覽過**電腦設定**–**原則**– **Windows 設定**–**安全性設定**–**帳戶原則**–**密碼原則**。</span><span class="sxs-lookup"><span data-stu-id="91858-201">In hello Group Policy Management Editor, navigate too**Computer Configuration** – **Policies** – **Windows Settings** – **Security Settings** – **Account Policies** – **Password Policy**.</span></span>
4. <span data-ttu-id="91858-202">在 hello 右窗格中，按兩下**密碼最長有效期**。</span><span class="sxs-lookup"><span data-stu-id="91858-202">In hello right pane, double-click on **Maximum password age**.</span></span>
5. <span data-ttu-id="91858-203">在 hello**密碼最長有效期屬性**對話方塊中，變更 hello**密碼即將於**值 too180，然後按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="91858-203">In hello **Maximum password age Properties** dialog box, change hello **Password will expire in** value too180, then Click **OK**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="91858-204">後續步驟</span><span class="sxs-lookup"><span data-stu-id="91858-204">Next steps</span></span>
[<span data-ttu-id="91858-205">使用您的 Azure 訂用帳戶註冊 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="91858-205">Register Azure Stack with your Azure subscription</span></span>](azure-stack-register.md)

[<span data-ttu-id="91858-206">連接 tooAzure 堆疊</span><span class="sxs-lookup"><span data-stu-id="91858-206">Connect tooAzure Stack</span></span>](azure-stack-connect-azure-stack.md)

