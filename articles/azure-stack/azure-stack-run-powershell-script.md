---
title: "部署 Azure Stack 開發套件 | Microsoft Docs"
description: "了解如何準備 Azure Stack 開發套件，以及執行 PowerShell 指令碼來加以部署。"
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
ms.openlocfilehash: b8497f0331e9b7d19eed2e1c254849a1619f496a
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2017
---
# <a name="deploy-the-azure-stack-development-kit"></a><span data-ttu-id="2de1d-103">部署 Azure Stack 開發套件</span><span class="sxs-lookup"><span data-stu-id="2de1d-103">Deploy the Azure Stack Development Kit</span></span>

<span data-ttu-id="2de1d-104">適用於：Azure Stack 開發套件</span><span class="sxs-lookup"><span data-stu-id="2de1d-104">*Applies to: Azure Stack Development Kit*</span></span>

<span data-ttu-id="2de1d-105">若要部署 [Azure Stack 開發套件](azure-stack-poc.md)，您必須完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="2de1d-105">To deploy the [Azure Stack Development Kit](azure-stack-poc.md), you must complete the following steps:</span></span>

1. <span data-ttu-id="2de1d-106">[下載部署封裝](https://azure.microsoft.com/overview/azure-stack/try/?v=try)以取得 Cloudbuilder.vhdx。</span><span class="sxs-lookup"><span data-stu-id="2de1d-106">[Download the deployment package](https://azure.microsoft.com/overview/azure-stack/try/?v=try) to get the Cloudbuilder.vhdx.</span></span>
2. <span data-ttu-id="2de1d-107">執行 asdk-installer.ps1 指令碼來設定安裝開發套件所在的電腦 (開發套件主機)，以[準備 cloudbuilder.vhdx](#prepare-the-development-kit-host)。</span><span class="sxs-lookup"><span data-stu-id="2de1d-107">[Prepare the cloudbuilder.vhdx](#prepare-the-development-kit-host) by running the asdk-installer.ps1 script to configure the computer (the development kit host) on which you want to install development kit.</span></span> <span data-ttu-id="2de1d-108">在這個步驟之後，開發套件主機將會開機進入 Cloudbuilder.vhdx。</span><span class="sxs-lookup"><span data-stu-id="2de1d-108">After this step, the development kit host will boot to the Cloudbuilder.vhdx.</span></span>
3. <span data-ttu-id="2de1d-109">在開發套件主機上，[部署開發套件](#deploy-the-development-kit)。</span><span class="sxs-lookup"><span data-stu-id="2de1d-109">[Deploy the development kit](#deploy-the-development-kit) on the development kit host.</span></span>

> [!NOTE]
> <span data-ttu-id="2de1d-110">為獲得最佳結果，即使您想要使用已中斷連線的 Azure Stack 環境，最好是在已連線到網際網路時部署。</span><span class="sxs-lookup"><span data-stu-id="2de1d-110">For best results, even if you want to use a disconnected Azure Stack environment, it is best to deploy while connected to the internet.</span></span> <span data-ttu-id="2de1d-111">如此一來，就可以在部署期間啟動 Windows Server 2016 評估版。</span><span class="sxs-lookup"><span data-stu-id="2de1d-111">That way, the Windows Server 2016 evaluation version can be activated at deployment time.</span></span> <span data-ttu-id="2de1d-112">如果在 10 天內未啟動 Windows Server 2016 評估版，它就會關閉。</span><span class="sxs-lookup"><span data-stu-id="2de1d-112">If the Windows Server 2016 evaluation version is not activated within 10 days, it shuts down.</span></span>
> 
> 

## <a name="download-and-extract-the-development-kit"></a><span data-ttu-id="2de1d-113">下載並將開發套件解壓縮</span><span class="sxs-lookup"><span data-stu-id="2de1d-113">Download and extract the development kit</span></span>
1. <span data-ttu-id="2de1d-114">開始下載之前，請確定您的電腦符合下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="2de1d-114">Before you start the download, make sure that your computer meets the following prerequisites:</span></span>

   * <span data-ttu-id="2de1d-115">電腦必須至少有 60 GB 的可用磁碟空間。</span><span class="sxs-lookup"><span data-stu-id="2de1d-115">The computer must have at least 60 GB of free disk space.</span></span>
   * <span data-ttu-id="2de1d-116">必須安裝 [.NET framework 4.6 (或更新版本)](https://aka.ms/r6mkiy)。</span><span class="sxs-lookup"><span data-stu-id="2de1d-116">[.NET Framework 4.6 (or a later version)](https://aka.ms/r6mkiy) must be installed.</span></span>

2. <span data-ttu-id="2de1d-117">[移至開始使用頁面](https://azure.microsoft.com/overview/azure-stack/try/?v=try)、提供您的詳細資料，然後按一下 [提交]。</span><span class="sxs-lookup"><span data-stu-id="2de1d-117">[Go to the Get Started page](https://azure.microsoft.com/overview/azure-stack/try/?v=try), provide your details, and click **Submit**.</span></span>
3. <span data-ttu-id="2de1d-118">在 [下載軟體] 底下，按一下 [Azure Stack 開發套件]。</span><span class="sxs-lookup"><span data-stu-id="2de1d-118">Under **Download the software**, click **Azure Stack Development Kit**.</span></span>
4. <span data-ttu-id="2de1d-119">執行下載的 AzureStackDownloader.exe 檔案。</span><span class="sxs-lookup"><span data-stu-id="2de1d-119">Run the downloaded AzureStackDownloader.exe file.</span></span>
5. <span data-ttu-id="2de1d-120">在 [Azure Stack 開發套件下載程式] 視窗中，遵循步驟 1 至 5 進行。</span><span class="sxs-lookup"><span data-stu-id="2de1d-120">In the **Azure Stack Development Kit Downloader** window, follow steps 1 through 5.</span></span>
6. <span data-ttu-id="2de1d-121">下載完成之後，請按一下 [執行]，以啟動 MicrosoftAzureStackPOC.exe。</span><span class="sxs-lookup"><span data-stu-id="2de1d-121">After the download completes, click **Run** to launch the MicrosoftAzureStackPOC.exe.</span></span>
7. <span data-ttu-id="2de1d-122">檢閱 自我解壓縮程式精靈 的 授權合約 畫面和資訊，然後按一下下一步。</span><span class="sxs-lookup"><span data-stu-id="2de1d-122">Review the License Agreement screen and information of the Self-Extractor Wizard and then click **Next**.</span></span>
8. <span data-ttu-id="2de1d-123">檢閱 自我解壓縮程式精靈 的 隱私權聲明 畫面和資訊，然後按一下下一步。</span><span class="sxs-lookup"><span data-stu-id="2de1d-123">Review the Privacy Statement screen and information of the Self-Extractor Wizard and then click **Next**.</span></span>
9. <span data-ttu-id="2de1d-124">選取要用來將檔案解壓縮的目的地，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="2de1d-124">Select the Destination for the files to be extracted, click **Next**.</span></span>
   * <span data-ttu-id="2de1d-125">預設值是：<drive letter>:\<目前資料夾>\Microsoft Azure Stack</span><span class="sxs-lookup"><span data-stu-id="2de1d-125">The default is: <drive letter>:\<current folder>\Microsoft Azure Stack</span></span>
10. <span data-ttu-id="2de1d-126">檢閱 自我解壓縮程式精靈 的 目的地位置 畫面和資訊，然後按一下解壓縮 來解壓縮 CloudBuilder.vhdx (~ 25 GB) 和 ThirdPartyLicenses.rtf 檔案。</span><span class="sxs-lookup"><span data-stu-id="2de1d-126">Review the Destination location screen and information of the Self-Extractor Wizard, and then click **Extract** to extract the CloudBuilder.vhdx (~25 GB) and ThirdPartyLicenses.rtf files.</span></span> <span data-ttu-id="2de1d-127">這個程序需要一些時間才會完成。</span><span class="sxs-lookup"><span data-stu-id="2de1d-127">This process will take some time to complete.</span></span>

> [!NOTE]
> <span data-ttu-id="2de1d-128">將檔案解壓縮之後，您可以刪除 exe 和 bin 檔案來恢復電腦上的空間。</span><span class="sxs-lookup"><span data-stu-id="2de1d-128">After you extract the files, you can delete the exe and bin files to recover space on the machine.</span></span> <span data-ttu-id="2de1d-129">或者，您可以將這些檔案移到其他位置。如此一來，如果您需要重新部署，就不必重新下載這些檔案。</span><span class="sxs-lookup"><span data-stu-id="2de1d-129">Or, you can move these files to another location so that if you need to redeploy you don’t need to download the files again.</span></span>
> 
> 

## <a name="prepare-the-development-kit-host"></a><span data-ttu-id="2de1d-130">準備開發套件主機</span><span class="sxs-lookup"><span data-stu-id="2de1d-130">Prepare the development kit host</span></span>
1. <span data-ttu-id="2de1d-131">請確定您可以實際連線到開發套件主機，或者可以存取實體主控台 (例如 KVM)。</span><span class="sxs-lookup"><span data-stu-id="2de1d-131">Make sure that you can physically connect to the development kit host, or have physical console access (such as KVM).</span></span> <span data-ttu-id="2de1d-132">在下面的步驟 13 中重新啟動開發套件主機之後，您必須以這類方式來存取。</span><span class="sxs-lookup"><span data-stu-id="2de1d-132">You must have such access after you reboot the development kit host in step 13 below.</span></span>
2. <span data-ttu-id="2de1d-133">請確定開發套件主機符合[最低需求](azure-stack-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="2de1d-133">Make sure the development kit host meets the [minimum requirements](azure-stack-deploy.md).</span></span> <span data-ttu-id="2de1d-134">您可以使用 [Azure Stack 適用的部署檢查程式](https://gallery.technet.microsoft.com/Deployment-Checker-for-50e0f51b)來確認您的需求。</span><span class="sxs-lookup"><span data-stu-id="2de1d-134">You can use the [Deployment Checker for Azure Stack](https://gallery.technet.microsoft.com/Deployment-Checker-for-50e0f51b) to confirm your requirements.</span></span>
3. <span data-ttu-id="2de1d-135">以本機系統管理員的身分來登入開發套件主機。</span><span class="sxs-lookup"><span data-stu-id="2de1d-135">Sign in as the Local Administrator to your development kit host.</span></span>
4. <span data-ttu-id="2de1d-136">將 CloudBuilder.vhdx 檔案複製或移動至 C:\ 磁碟機的根目錄 (C:\CloudBuilder.vhdx)。</span><span class="sxs-lookup"><span data-stu-id="2de1d-136">Copy or move the CloudBuilder.vhdx file to the root of the C:\ drive (C:\CloudBuilder.vhdx).</span></span>
5. <span data-ttu-id="2de1d-137">執行下列指令碼，將開發套件安裝程式檔案 (asdk-installer.ps1) 下載至開發套件主機上的 c:\AzureStack_Installer 資料夾。</span><span class="sxs-lookup"><span data-stu-id="2de1d-137">Run the following script to download the development kit installer file (asdk-installer.ps1) to the c:\AzureStack_Installer folder on your development kit host.</span></span>
    ```powershell
    # Variables
    $Uri = 'https://raw.githubusercontent.com/Azure/AzureStack-Tools/master/Deployment/asdk-installer.ps1'
    $LocalPath = 'c:\AzureStack_Installer'

    # Create folder
    New-Item $LocalPath -Type directory

    # Download file
    Invoke-WebRequest $uri -OutFile ($LocalPath + '\' + 'asdk-installer.ps1')
    ```
6. <span data-ttu-id="2de1d-138">開啟提升權限的 PowerShell 主控台 > 執行 C:\AzureStack_Installer\asdk-installer.ps1 指令碼 > 按一下**準備環境**。</span><span class="sxs-lookup"><span data-stu-id="2de1d-138">Open an elevated PowerShell console > run the C:\AzureStack_Installer\asdk-installer.ps1 script > click **Prepare Environment**.</span></span>
7. <span data-ttu-id="2de1d-139">在安裝程式的 [選取 Cloudbuilder vhdx] 頁面上，瀏覽至您在先前步驟中下載的 cloudbuilder.vhdx 檔案並加以選取。</span><span class="sxs-lookup"><span data-stu-id="2de1d-139">On the **Select Cloudbuilder vhdx** page of the installer, browse to and select the cloudbuilder.vhdx file that you downloaded in the previous steps.</span></span>
8. <span data-ttu-id="2de1d-140">選擇性：選取 [新增驅動程式] 方塊，以指定包含主機上所要其他驅動程式的資料夾。</span><span class="sxs-lookup"><span data-stu-id="2de1d-140">Optional: Check the **Add drivers** box to specify a folder containing additional drivers that you want on the host.</span></span>
9. <span data-ttu-id="2de1d-141">在 [選擇性設定] 頁面上，提供開發套件主機的本機系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="2de1d-141">On the **Optional settings** page, provide the local administrator account for the development kit host.</span></span> <span data-ttu-id="2de1d-142">如果沒有提供這些認證，則在下方的安裝程序期間，您必須能夠以 KVM 來存取主機。</span><span class="sxs-lookup"><span data-stu-id="2de1d-142">If you don't provide these credentials, you'll need KVM access to the host during the install process below.</span></span>
10. <span data-ttu-id="2de1d-143">此外，在 [選擇性設定] 頁面上，您可以選擇設定下列項目：</span><span class="sxs-lookup"><span data-stu-id="2de1d-143">Also on the **Optional settings** page, you have the option to set the following:</span></span>
    - <span data-ttu-id="2de1d-144">**電腦名稱**：此選項會設定開發套件主機的名稱。</span><span class="sxs-lookup"><span data-stu-id="2de1d-144">**Computername**: This option sets the name for the development kit host.</span></span> <span data-ttu-id="2de1d-145">名稱必須符合 FQDN 需求，且長度必須等於或少於 15 個字元。</span><span class="sxs-lookup"><span data-stu-id="2de1d-145">The name must comply with FQDN requirements and must be 15 characters or less in length.</span></span> <span data-ttu-id="2de1d-146">預設值是由 Windows 產生的隨機電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="2de1d-146">The default is a random computer name generated by Windows.</span></span>
    - <span data-ttu-id="2de1d-147">**時區**：設定開發套件主機的時區。</span><span class="sxs-lookup"><span data-stu-id="2de1d-147">**Time zone**: Sets the time zone for the development kit host.</span></span> <span data-ttu-id="2de1d-148">預設值是 (UTC-8:00) 太平洋時間 (美國和加拿大)。</span><span class="sxs-lookup"><span data-stu-id="2de1d-148">The default is (UTC-8:00) Pacific Time (US & Canada).</span></span>
    - <span data-ttu-id="2de1d-149">**靜態 IP 組態**：將您的部署設定為使用靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2de1d-149">**Static IP configuration**: Sets your deployment to use a static IP address.</span></span> <span data-ttu-id="2de1d-150">否則，當安裝程式重新開機進入 cloudbuilder.vhx 時，會使用 DHCP 來設定網路介面。</span><span class="sxs-lookup"><span data-stu-id="2de1d-150">Otherwise, when the installer reboots into the cloudbuilder.vhx, the network interfaces are configured with DHCP.</span></span>
11. <span data-ttu-id="2de1d-151">按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="2de1d-151">Click **Next**.</span></span>
12. <span data-ttu-id="2de1d-152">如果您在上一個步驟中選擇靜態 IP 組態，您現在必須：</span><span class="sxs-lookup"><span data-stu-id="2de1d-152">If you chose a static IP configuration in the previous step, you must now:</span></span>
    - <span data-ttu-id="2de1d-153">選取網路介面卡。</span><span class="sxs-lookup"><span data-stu-id="2de1d-153">Select a network adapter.</span></span> <span data-ttu-id="2de1d-154">請先確定您可以連線到介面卡，然後再按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="2de1d-154">Make sure you can connect to the adapter before you click **Next**.</span></span>
    - <span data-ttu-id="2de1d-155">請確定 IP 位址、閘道 和 DNS 值正確無誤，然後按一下下一步。</span><span class="sxs-lookup"><span data-stu-id="2de1d-155">Make sure that the **IP address**, **Gateway**, and **DNS** values are correct and then click **Next**.</span></span>
13. <span data-ttu-id="2de1d-156">按一下 [下一步]，以開始準備程序。</span><span class="sxs-lookup"><span data-stu-id="2de1d-156">Click **Next** to start the preparation process.</span></span>
14. <span data-ttu-id="2de1d-157">當準備指出 [已完成] 時，按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="2de1d-157">When the preparation indicates **Completed**, click **Next**.</span></span>
15. <span data-ttu-id="2de1d-158">按一下 [立即重新開機]，以開機進入 cloudbuilder.vhdx 並繼續部署程序。</span><span class="sxs-lookup"><span data-stu-id="2de1d-158">Click **Reboot now** to boot into the cloudbuilder.vhdx and continue the deployment process.</span></span>

## <a name="deploy-the-development-kit"></a><span data-ttu-id="2de1d-159">部署開發套件</span><span class="sxs-lookup"><span data-stu-id="2de1d-159">Deploy the development kit</span></span>
1. <span data-ttu-id="2de1d-160">以本機系統管理員的身分來登入開發套件主機。</span><span class="sxs-lookup"><span data-stu-id="2de1d-160">Sign in as the Local Administrator to the development kit host.</span></span> <span data-ttu-id="2de1d-161">使用在先前步驟中指定的認證。</span><span class="sxs-lookup"><span data-stu-id="2de1d-161">Use the credentials specified in the previous steps.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="2de1d-162">若是 Azure Active Directory 部署，Azure Stack 需要能夠直接或透過 Transparent Proxy 來存取網際網路。</span><span class="sxs-lookup"><span data-stu-id="2de1d-162">For Azure Active Directory deployments, Azure Stack requires access to the Internet, either directly or through a transparent proxy.</span></span> <span data-ttu-id="2de1d-163">部署僅支援一個 NIC，以供網路功能使用。</span><span class="sxs-lookup"><span data-stu-id="2de1d-163">The deployment supports exactly one NIC for networking.</span></span> <span data-ttu-id="2de1d-164">如果您有多個 NIC，請確定僅啟用一個 NIC (且停用其他所有 NIC)，再執行下一節中的部署指令碼。</span><span class="sxs-lookup"><span data-stu-id="2de1d-164">If you have multiple NICs, make sure that only one is enabled (and all others are disabled) before running the deployment script in the next section.</span></span>
    
2. <span data-ttu-id="2de1d-165">開啟提升權限的 PowerShell 主控台 > 執行 \AzureStack_Installer\asdk-installer.ps1 指令碼 (這可能是在 Cloudbuilder.vhdx 中的其他磁碟機上) > 按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="2de1d-165">Open an elevated PowerShell console > run the \AzureStack_Installer\asdk-installer.ps1 script (which may be on a different drive in the Cloudbuilder.vhdx) > click **Install**.</span></span>
3. <span data-ttu-id="2de1d-166">在 [類型] 方塊中，選取 [Azure 雲端] 或 [ADFS]。</span><span class="sxs-lookup"><span data-stu-id="2de1d-166">In the **Type** box, select **Azure Cloud** or **ADFS**.</span></span>
    - <span data-ttu-id="2de1d-167">**Azure 雲端**：Azure Active Directory 為識別提供者。</span><span class="sxs-lookup"><span data-stu-id="2de1d-167">**Azure Cloud**: Azure Active Directory is the identity provider.</span></span> <span data-ttu-id="2de1d-168">使用此參數可指定 AAD 帳戶具有全域系統管理員權限的特定目錄。</span><span class="sxs-lookup"><span data-stu-id="2de1d-168">Use this parameter to specify a specific directory where the AAD account has global admin permissions.</span></span> <span data-ttu-id="2de1d-169">AAD 目錄租用戶的完整名稱，格式為 .onmicrosoft.com。</span><span class="sxs-lookup"><span data-stu-id="2de1d-169">Full name of an AAD Directory tenant in the format of .onmicrosoft.com.</span></span> 
    - <span data-ttu-id="2de1d-170">**ADFS**：預設戳記目錄服務為識別提供者、登入身分的預設帳戶是 azurestackadmin@azurestack.local，且要使用的密碼是您在安裝時所提供的密碼。</span><span class="sxs-lookup"><span data-stu-id="2de1d-170">**ADFS**: The default stamp Directory Service is the identity provider, the default account to sign in with is azurestackadmin@azurestack.local, and the password to use is the one you provided as part of the setup.</span></span>
4. <span data-ttu-id="2de1d-171">在 本機系統管理員密碼 底下的 密碼 方塊中，輸入本機系統管理員密碼 (必須符合目前設定的本機系統管理員密碼)，然後按一下下一步。</span><span class="sxs-lookup"><span data-stu-id="2de1d-171">Under **Local administrator password**, in the **Password** box, type the local administrator password (which must match the current configured local administrator password), and then click **Next**.</span></span>
5. <span data-ttu-id="2de1d-172">選取要用於開發套件的網路介面卡，然後按一下下一步。</span><span class="sxs-lookup"><span data-stu-id="2de1d-172">Select a network adapter to use for the development kit and then click **Next**.</span></span>
6. <span data-ttu-id="2de1d-173">為 BGPNAT01 虛擬機器選取 DHCP 或靜態網路組態。</span><span class="sxs-lookup"><span data-stu-id="2de1d-173">Select DHCP or static network configuration for the BGPNAT01 virtual machine.</span></span>
    - <span data-ttu-id="2de1d-174">**DHCP** (預設值)：虛擬機器會從 DHCP 伺服器取得 IP 網路組態。</span><span class="sxs-lookup"><span data-stu-id="2de1d-174">**DHCP** (default): The virtual machine gets the IP network configuration from the DHCP server.</span></span>
    - <span data-ttu-id="2de1d-175">**靜態**：只有當 DHCP 無法為 Azure Stack 指派有效的 IP 位址來存取網際網路時，才使用此選項。</span><span class="sxs-lookup"><span data-stu-id="2de1d-175">**Static**: Only use this option if DHCP can’t assign a valid IP address for Azure Stack to access the Internet.</span></span> <span data-ttu-id="2de1d-176">指定靜態 IP 位址 時，必須一併指定子網路遮罩長度 (例如，10.0.0.5/24)。</span><span class="sxs-lookup"><span data-stu-id="2de1d-176">A static IP address must be specified with the subnetmask length (for example, 10.0.0.5/24).</span></span>
7. <span data-ttu-id="2de1d-177">或者，設定下列值：</span><span class="sxs-lookup"><span data-stu-id="2de1d-177">Optionally, set the following values:</span></span>
    - <span data-ttu-id="2de1d-178">**VLAN 識別碼**：設定 VLAN 識別碼。</span><span class="sxs-lookup"><span data-stu-id="2de1d-178">**VLAN ID**: Sets the VLAN ID.</span></span> <span data-ttu-id="2de1d-179">只有當主機與 AzS-BGPNAT01 必須設定 VLAN 識別碼來存取實體網路 (以及網際網路) 時，才使用此選項。</span><span class="sxs-lookup"><span data-stu-id="2de1d-179">Only use this option if the host and AzS-BGPNAT01 must configure VLAN ID to access the physical network (and Internet).</span></span> 
    - <span data-ttu-id="2de1d-180">**DNS 轉寄站**：DNS 伺服器會在 Azure Stack 部署期間建立。</span><span class="sxs-lookup"><span data-stu-id="2de1d-180">**DNS forwarder**: A DNS server is created as part of the Azure Stack deployment.</span></span> <span data-ttu-id="2de1d-181">若要允許解決方案內的電腦解析戳記以外的名稱，請提供您現有架構 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="2de1d-181">To allow computers inside the solution to resolve names outside of the stamp, provide your existing infrastructure DNS server.</span></span> <span data-ttu-id="2de1d-182">戳記內的 DNS 伺服器會將未知的名稱解析要求轉送至這部伺服器。</span><span class="sxs-lookup"><span data-stu-id="2de1d-182">The in-stamp DNS server forwards unknown name resolution requests to this server.</span></span>
    - <span data-ttu-id="2de1d-183">**時間伺服器**： 這個必要的欄位設定時間伺服器，而必須是 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2de1d-183">**Time server**: This required field sets the time server and must be an IP address.</span></span> <span data-ttu-id="2de1d-184">若要尋找時間伺服器的 IP 位址，請造訪[pool.ntp.org](http:\\pool.ntp.org)或偵測 time.windows.com。</span><span class="sxs-lookup"><span data-stu-id="2de1d-184">To find a time server IP address, visit [pool.ntp.org](http:\\pool.ntp.org) or ping time.windows.com.</span></span> 
8. <span data-ttu-id="2de1d-185">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="2de1d-185">Click **Next**.</span></span> 
9. <span data-ttu-id="2de1d-186">在 [驗證網路介面卡內容] 頁面上，您將會看到一個進度列。</span><span class="sxs-lookup"><span data-stu-id="2de1d-186">On the **Verifying network interface card properties** page, you'll see a progress bar.</span></span> 
    - <span data-ttu-id="2de1d-187">如果顯示 [無法下載更新]，請遵循頁面上的指示執行。</span><span class="sxs-lookup"><span data-stu-id="2de1d-187">If it says **An update cannot be downloaded**, follow the instructions on the page.</span></span>
    - <span data-ttu-id="2de1d-188">顯示 [已完成] 時，按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="2de1d-188">When it says **Completed**, click **Next**.</span></span>
10. <span data-ttu-id="2de1d-189">在 [摘要] 頁面上，按一下 [部署]。</span><span class="sxs-lookup"><span data-stu-id="2de1d-189">On **Summary** page, click **Deploy**.</span></span>
11. <span data-ttu-id="2de1d-190">如果您使用的是 Azure Active Directory 部署，系統會要求您輸入 Azure Active Directory 全域系統管理員帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="2de1d-190">If you're using an Azure Active Directory deployment, you'll be asked to enter your Azure Active Directory global administrator account credentials.</span></span>
12. <span data-ttu-id="2de1d-191">部署程序可能需要幾小時的時間，在這段期間內，系統會自動重新開機一次。</span><span class="sxs-lookup"><span data-stu-id="2de1d-191">The deployment process can take a few hours, during which the system automatically reboots once.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="2de1d-192">如果您想要監視部署進度，請以 azurestack\AzureStackAdmin 的身分登入。</span><span class="sxs-lookup"><span data-stu-id="2de1d-192">If you want to monitor the deployment progress, sign in as azurestack\AzureStackAdmin.</span></span> <span data-ttu-id="2de1d-193">如果您在電腦加入網域之後，以本機系統管理員的身分登入，將不會看到部署進度。</span><span class="sxs-lookup"><span data-stu-id="2de1d-193">If you sign in as a local admin after the machine is joined to the domain, you won't see the deployment progress.</span></span> <span data-ttu-id="2de1d-194">請勿重新執行部署，而是以 azurestack\AzureStackAdmin 的身分登入，以驗證執行狀態。</span><span class="sxs-lookup"><span data-stu-id="2de1d-194">Do not rerun deployment, instead sign in as azurestack\AzureStackAdmin to validate that it's running.</span></span>
   > 
   > 
   
    <span data-ttu-id="2de1d-195">當部署成功時，PowerShell 主控台會顯示：**COMPLETE: Action ‘Deployment’**。</span><span class="sxs-lookup"><span data-stu-id="2de1d-195">When the deployment succeeds, the PowerShell console displays: **COMPLETE: Action ‘Deployment’**.</span></span>
   
<span data-ttu-id="2de1d-196">如果部署失敗，您可以使用下列 PowerShell，從相同提升權限的 PowerShell 視窗重新執行指令碼：</span><span class="sxs-lookup"><span data-stu-id="2de1d-196">If the deployment fails, you can use the following PowerShell rerun script from the same elevated PowerShell window:</span></span>

```powershell
cd c:\CloudDeployment\Setup
.\InstallAzureStackPOC.ps1 -Rerun
```

<span data-ttu-id="2de1d-197">此指令碼將會從最後一個成功的步驟重新開始部署。</span><span class="sxs-lookup"><span data-stu-id="2de1d-197">This script will restart the deployment from the last step that succeeded.</span></span>

<span data-ttu-id="2de1d-198">或者，您可以從頭開始[重新部署](azure-stack-redeploy.md)。</span><span class="sxs-lookup"><span data-stu-id="2de1d-198">Or, you can [redeploy](azure-stack-redeploy.md) from scratch.</span></span>


## <a name="reset-the-password-expiration-to-180-days"></a><span data-ttu-id="2de1d-199">將密碼到期日重設為 180 天</span><span class="sxs-lookup"><span data-stu-id="2de1d-199">Reset the password expiration to 180 days</span></span>

<span data-ttu-id="2de1d-200">為確定開發套件主機的密碼不會太快到期，請在部署之後遵循下列步驟進行：</span><span class="sxs-lookup"><span data-stu-id="2de1d-200">To make sure that the password for the development kit host doesn't expire too soon, follow these steps after you deploy:</span></span>

1. <span data-ttu-id="2de1d-201">在開發套件主機上，開啟 [群組原則管理]，並瀏覽至 [群組原則管理] – [樹系：azurestack.local] – [網域] – [azurestack.local]。</span><span class="sxs-lookup"><span data-stu-id="2de1d-201">On the development kit host, open **Group Policy Management** and navigate to **Group Policy Management** – **Forest: azurestack.local** – **Domains** – **azurestack.local**.</span></span>
2. <span data-ttu-id="2de1d-202">以滑鼠右鍵按一下**預設網域原則**按一下**編輯**。</span><span class="sxs-lookup"><span data-stu-id="2de1d-202">Right click **Default Domain Policy** and click **Edit**.</span></span>
3. <span data-ttu-id="2de1d-203">在 [群組原則管理編輯器] 中，瀏覽至 [電腦設定] – [原則] – [Windows 設定] – [安全性設定] – [帳戶原則] – [密碼原則]。</span><span class="sxs-lookup"><span data-stu-id="2de1d-203">In the Group Policy Management Editor, navigate to **Computer Configuration** – **Policies** – **Windows Settings** – **Security Settings** – **Account Policies** – **Password Policy**.</span></span>
4. <span data-ttu-id="2de1d-204">在右窗格中，按兩下**密碼最長有效期**。</span><span class="sxs-lookup"><span data-stu-id="2de1d-204">In the right pane, double-click **Maximum password age**.</span></span>
5. <span data-ttu-id="2de1d-205">在**密碼最長有效期屬性**對話方塊中，變更**密碼即將於**值設定為 180，然後按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="2de1d-205">In the **Maximum password age Properties** dialog box, change the **Password will expire in** value to 180, then click **OK**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="2de1d-206">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2de1d-206">Next steps</span></span>

[<span data-ttu-id="2de1d-207">安裝 PowerShell</span><span class="sxs-lookup"><span data-stu-id="2de1d-207">Install PowerShell</span></span>](azure-stack-powershell-configure-quickstart.md)

[<span data-ttu-id="2de1d-208">使用您的 Azure 訂用帳戶註冊 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="2de1d-208">Register Azure Stack with your Azure subscription</span></span>](azure-stack-register.md)

[<span data-ttu-id="2de1d-209">連接至 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="2de1d-209">Connect to Azure Stack</span></span>](azure-stack-connect-azure-stack.md)

