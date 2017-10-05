---
title: "建立 StorSimple 支援封裝 | Microsoft Docs"
description: "了解如何建立、解密和編輯 StorSimple 裝置的支援封裝。"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: eac76f5f-5db1-4c92-af8c-54053b91e66c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 32d20e7a8adcfc646c592213fe7395b87a93c985
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-a-storsimple-support-package"></a><span data-ttu-id="bba46-103">建立及管理 StorSimple 支援封裝</span><span class="sxs-lookup"><span data-stu-id="bba46-103">Create and manage a StorSimple support package</span></span>
## <a name="overview"></a><span data-ttu-id="bba46-104">概觀</span><span class="sxs-lookup"><span data-stu-id="bba46-104">Overview</span></span>
<span data-ttu-id="bba46-105">StorSimple 支援封裝是一種簡便的機制，可收集所有相關的記錄以協助 Microsoft 支援服務針對任何 StorSimple 裝置問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="bba46-105">A StorSimple support package is an easy-to-use mechanism that collects all relevant logs to assist Microsoft Support with troubleshooting any StorSimple device issues.</span></span> <span data-ttu-id="bba46-106">收集的記錄都會經過加密並壓縮。</span><span class="sxs-lookup"><span data-stu-id="bba46-106">The collected logs are encrypted and compressed.</span></span>

<span data-ttu-id="bba46-107">本教學課程包含建立和管理支援封裝的逐步指示：</span><span class="sxs-lookup"><span data-stu-id="bba46-107">This tutorial includes step-by-step instructions to create and manage the support package.</span></span>

## <a name="create-and-upload-a-support-package-in-the-azure-classic-portal"></a><span data-ttu-id="bba46-108">在 Azure 傳統入口網站中建立與上傳支援封裝</span><span class="sxs-lookup"><span data-stu-id="bba46-108">Create and upload a support package in the Azure classic portal</span></span>
<span data-ttu-id="bba46-109">您可以在 Azure 傳統入口網站中透過此服務的 [維護]  頁面，建立支援封裝並上傳至 Microsoft 支援服務網站。</span><span class="sxs-lookup"><span data-stu-id="bba46-109">You can create and upload a support package to the Microsoft Support site through the **Maintenance** page of the service in the Azure classic portal.</span></span>

> [!NOTE]
> <span data-ttu-id="bba46-110">上傳需要支援密碼。</span><span class="sxs-lookup"><span data-stu-id="bba46-110">The upload requires a support passkey.</span></span> <span data-ttu-id="bba46-111">支援工程師應在電子郵件中提供此密碼給您。</span><span class="sxs-lookup"><span data-stu-id="bba46-111">Your support engineer should provide this to you in an email.</span></span>
> 
> 

<span data-ttu-id="bba46-112">建立加密和壓縮的支援封裝 (.cab 檔案) 並上傳至「支援服務」網站。</span><span class="sxs-lookup"><span data-stu-id="bba46-112">An encrypted and compressed support package (.cab file) is created and uploaded to the Support site.</span></span> <span data-ttu-id="bba46-113">支援工程師就能從支援服務網站擷取此封裝以針對此問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="bba46-113">The support engineer can then retrieve this package from the Support site for troubleshooting the issue.</span></span>

<span data-ttu-id="bba46-114">在 Azure 傳統入口網站中執行下列步驟，以建立支援封裝。</span><span class="sxs-lookup"><span data-stu-id="bba46-114">Perform the following steps in the classic portal to create a support package.</span></span>

#### <a name="to-create-a-support-package-in-the-azure-classic-portal"></a><span data-ttu-id="bba46-115">在 Azure 傳統入口網站中建立支援封裝</span><span class="sxs-lookup"><span data-stu-id="bba46-115">To create a support package in the Azure classic portal</span></span>
1. <span data-ttu-id="bba46-116">選取 [裝置] > [維護]。</span><span class="sxs-lookup"><span data-stu-id="bba46-116">Select **Devices** > **Maintenance**.</span></span>
2. <span data-ttu-id="bba46-117">在 [支援封裝] 區段中，選取 [建立及上傳支援封裝]。</span><span class="sxs-lookup"><span data-stu-id="bba46-117">In the **Support package** section, select **Create and upload support package**.</span></span>
3. <span data-ttu-id="bba46-118">在 [ **建立及上傳支援封裝** ] 對話方塊中，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="bba46-118">In the **Create and upload support package** dialog box, do the following:</span></span>
   
    ![建立支援封裝](./media/storsimple-create-manage-support-package/IC740923.png)
   
   * <span data-ttu-id="bba46-120">在 [支援密碼]  文字方塊中，輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="bba46-120">In the **Support Passkey** text box, enter the passkey.</span></span> <span data-ttu-id="bba46-121">Microsoft 支援工程師應在電子郵件中將此密碼傳送給您。</span><span class="sxs-lookup"><span data-stu-id="bba46-121">Your Microsoft support engineer should send this passkey to you in email.</span></span>
   * <span data-ttu-id="bba46-122">選取此核取方塊以同意自動上傳支援封裝至 Microsoft 支援服務網站。</span><span class="sxs-lookup"><span data-stu-id="bba46-122">Select the check box to provide consent to automatically upload the support package to the Microsoft Support site.</span></span>
   * <span data-ttu-id="bba46-123">按一下核取圖示 </span><span class="sxs-lookup"><span data-stu-id="bba46-123">Click the check icon</span></span> ![核取圖示](./media/storsimple-create-manage-support-package/IC740895.png)<span data-ttu-id="bba46-125">。</span><span class="sxs-lookup"><span data-stu-id="bba46-125">.</span></span>

## <a name="manually-create-a-support-package"></a><span data-ttu-id="bba46-126">手動建立支援封裝</span><span class="sxs-lookup"><span data-stu-id="bba46-126">Manually create a support package</span></span>
<span data-ttu-id="bba46-127">在某些情況下，您必須透過 Windows PowerShell for StorSimple 手動建立支援封裝。</span><span class="sxs-lookup"><span data-stu-id="bba46-127">In some cases, you'll need to manually create the support package through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="bba46-128">例如：</span><span class="sxs-lookup"><span data-stu-id="bba46-128">For example:</span></span>

* <span data-ttu-id="bba46-129">如果您在與 Microsoft 支援服務共用您的記錄檔之前，必須從其中移除機密資訊。</span><span class="sxs-lookup"><span data-stu-id="bba46-129">If you need to remove sensitive information from your log files prior to sharing with Microsoft Support.</span></span>
* <span data-ttu-id="bba46-130">如果您在上傳封裝時，因為連線能力問題而遇到困難。</span><span class="sxs-lookup"><span data-stu-id="bba46-130">If you are having difficulty uploading the package due to connectivity issues.</span></span>

<span data-ttu-id="bba46-131">您可以透過電子郵件與 Microsoft 支援服務共用手動產生的支援封裝。</span><span class="sxs-lookup"><span data-stu-id="bba46-131">You can share your manually generated support package with Microsoft Support over email.</span></span> <span data-ttu-id="bba46-132">執行下列步驟在 Windows PowerShell for StorSimple 中建立支援封裝。</span><span class="sxs-lookup"><span data-stu-id="bba46-132">Perform the following steps to create a support package in Windows PowerShell for StorSimple.</span></span>

#### <a name="to-create-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="bba46-133">在 Windows PowerShell for StorSimple 中建立支援封裝</span><span class="sxs-lookup"><span data-stu-id="bba46-133">To create a support package in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="bba46-134">若要在用來連接至 StorSimple 裝置的遠端電腦上，以系統管理員身分啟動 Windows PowerShell 工作階段，請輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="bba46-134">To start a Windows PowerShell session as an administrator on the remote computer that's used to connect to your StorSimple device, enter the following command:</span></span>
   
    `Start PowerShell`
2. <span data-ttu-id="bba46-135">在 Windows PowerShell 工作階段中，連接到裝置的 SSAdmin 主控台：</span><span class="sxs-lookup"><span data-stu-id="bba46-135">In the Windows PowerShell session, connect to the SSAdmin Console of your device:</span></span>
   
   * <span data-ttu-id="bba46-136">在命令提示字元中，輸入：</span><span class="sxs-lookup"><span data-stu-id="bba46-136">At the command prompt, enter:</span></span>
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   * <span data-ttu-id="bba46-137">在開啟的對話方塊中，輸入您的裝置系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="bba46-137">In the dialog box that opens, enter your device administrator password.</span></span> <span data-ttu-id="bba46-138">預設密碼為：</span><span class="sxs-lookup"><span data-stu-id="bba46-138">The default password is:</span></span>
     
      `Password1`
     
      ![[PowerShell 認證] 對話方塊](./media/storsimple-create-manage-support-package/IC740962.png)
   * <span data-ttu-id="bba46-140">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="bba46-140">Select **OK**.</span></span>
   * <span data-ttu-id="bba46-141">在命令提示字元中，輸入：</span><span class="sxs-lookup"><span data-stu-id="bba46-141">At the command prompt, enter:</span></span>
     
      `Enter-PSSession $MS`
3. <span data-ttu-id="bba46-142">在開啟的工作階段中，輸入適當的命令。</span><span class="sxs-lookup"><span data-stu-id="bba46-142">In the session that opens, enter the appropriate command.</span></span>
   
   * <span data-ttu-id="bba46-143">對於受密碼保護的網路共用，請輸入：</span><span class="sxs-lookup"><span data-stu-id="bba46-143">For network shares that are password protected, enter:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       <span data-ttu-id="bba46-144">系統會提示您輸入密碼、網路共用的資料夾路徑及加密複雜密碼 (因為支援封裝已加密)。</span><span class="sxs-lookup"><span data-stu-id="bba46-144">You'll be prompted for a password, a path to the network shared folder, and an encryption passphrase (because the support package is encrypted).</span></span> <span data-ttu-id="bba46-145">然後會在指定的資料夾中建立支援封裝。</span><span class="sxs-lookup"><span data-stu-id="bba46-145">A support package is then created in the specified folder.</span></span>
   * <span data-ttu-id="bba46-146">對於不受密碼保護的共用內容，您不需要 `-Credential` 參數。</span><span class="sxs-lookup"><span data-stu-id="bba46-146">For shares that are not password protected, you do not need the `-Credential` parameter.</span></span> <span data-ttu-id="bba46-147">輸入以下資訊：</span><span class="sxs-lookup"><span data-stu-id="bba46-147">Enter the following:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       <span data-ttu-id="bba46-148">在指定的網路共用資料夾中，同時為兩個控制器建立支援封裝。</span><span class="sxs-lookup"><span data-stu-id="bba46-148">The support package is created for both controllers in the specified network shared folder.</span></span> <span data-ttu-id="bba46-149">這是加密的壓縮檔案，可傳送給 Microsoft 支援服務進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="bba46-149">It's an encrypted, compressed file that can be sent to Microsoft Support for troubleshooting.</span></span> <span data-ttu-id="bba46-150">如需詳細資訊，請參閱 [連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)。</span><span class="sxs-lookup"><span data-stu-id="bba46-150">For more information, see [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

### <a name="the-export-hcssupportpackage-cmdlet-parameters"></a><span data-ttu-id="bba46-151">The Export-HcsSupportPackage cmdlet 參數</span><span class="sxs-lookup"><span data-stu-id="bba46-151">The Export-HcsSupportPackage cmdlet parameters</span></span>
<span data-ttu-id="bba46-152">您可以使用下列參數搭配 Export-HcsSupportPackage cmdlet。</span><span class="sxs-lookup"><span data-stu-id="bba46-152">You can use the following parameters with the Export-HcsSupportPackage cmdlet.</span></span>

| <span data-ttu-id="bba46-153">參數</span><span class="sxs-lookup"><span data-stu-id="bba46-153">Parameter</span></span> | <span data-ttu-id="bba46-154">必要/選用</span><span class="sxs-lookup"><span data-stu-id="bba46-154">Required/Optional</span></span> | <span data-ttu-id="bba46-155">說明</span><span class="sxs-lookup"><span data-stu-id="bba46-155">Description</span></span> |
| --- | --- | --- |
| `-Path` |<span data-ttu-id="bba46-156">必要</span><span class="sxs-lookup"><span data-stu-id="bba46-156">Required</span></span> |<span data-ttu-id="bba46-157">用來提供存放支援封裝的網路共用資料夾位置。</span><span class="sxs-lookup"><span data-stu-id="bba46-157">Use to provide the location of the network shared folder in which the support package is placed.</span></span> |
| `-EncryptionPassphrase` |<span data-ttu-id="bba46-158">必要</span><span class="sxs-lookup"><span data-stu-id="bba46-158">Required</span></span> |<span data-ttu-id="bba46-159">用來提供複雜密碼，以協助加密支援封裝。</span><span class="sxs-lookup"><span data-stu-id="bba46-159">Use to provide a passphrase to help encrypt the support package.</span></span> |
| `-Credential` |<span data-ttu-id="bba46-160">選用</span><span class="sxs-lookup"><span data-stu-id="bba46-160">Optional</span></span> |<span data-ttu-id="bba46-161">用來提供網路共用資料夾的存取認證。</span><span class="sxs-lookup"><span data-stu-id="bba46-161">Use to supply access credentials for the network shared folder.</span></span> |
| `-Force` |<span data-ttu-id="bba46-162">選用</span><span class="sxs-lookup"><span data-stu-id="bba46-162">Optional</span></span> |<span data-ttu-id="bba46-163">用來略過加密複雜密碼確認步驟。</span><span class="sxs-lookup"><span data-stu-id="bba46-163">Use to skip the encryption passphrase confirmation step.</span></span> |
| `-PackageTag` |<span data-ttu-id="bba46-164">選用</span><span class="sxs-lookup"><span data-stu-id="bba46-164">Optional</span></span> |<span data-ttu-id="bba46-165">用來指定 *Path* 下存放支援封裝的目錄。</span><span class="sxs-lookup"><span data-stu-id="bba46-165">Use to specify a directory under *Path* in which the support package is placed.</span></span> <span data-ttu-id="bba46-166">預設值是 [裝置名稱]-[目前日期和時間：yyyy-MM-dd-HH-mm-ss]。</span><span class="sxs-lookup"><span data-stu-id="bba46-166">The default is [device name]-[current date and time:yyyy-MM-dd-HH-mm-ss].</span></span> |
| `-Scope` |<span data-ttu-id="bba46-167">選用</span><span class="sxs-lookup"><span data-stu-id="bba46-167">Optional</span></span> |<span data-ttu-id="bba46-168">指定為 **Cluster** (預設值) 可以為兩個控制器建立支援封裝。</span><span class="sxs-lookup"><span data-stu-id="bba46-168">Specify as **Cluster** (default) to create a support package for both controllers.</span></span> <span data-ttu-id="bba46-169">如果您只想針對目前的控制器建立封裝，請指定 **Controller**。</span><span class="sxs-lookup"><span data-stu-id="bba46-169">If you want to create a package only for the current controller, specify **Controller**.</span></span> |

## <a name="edit-a-support-package"></a><span data-ttu-id="bba46-170">編輯支援封裝</span><span class="sxs-lookup"><span data-stu-id="bba46-170">Edit a support package</span></span>
<span data-ttu-id="bba46-171">在您產生支援封裝之後，可能需要編輯封裝以移除機密資訊。</span><span class="sxs-lookup"><span data-stu-id="bba46-171">After you have generated a support package, you might need to edit the package to remove sensitive information.</span></span> <span data-ttu-id="bba46-172">這可能包括磁碟區名稱、裝置 IP 位址，以及記錄檔中的備份名稱。</span><span class="sxs-lookup"><span data-stu-id="bba46-172">This can include volume names, device IP addresses, and backup names from the log files.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bba46-173">您只能編輯透過 Windows PowerShell for StorSimple 產生的支援封裝。</span><span class="sxs-lookup"><span data-stu-id="bba46-173">You can only edit a support package that was generated through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="bba46-174">您無法編輯在 Azure 傳統入口網站中以 StorSimple Manager 服務建立的封裝。</span><span class="sxs-lookup"><span data-stu-id="bba46-174">You can't edit a package created in the Azure classic portal with StorSimple Manager service.</span></span>
> 
> 

<span data-ttu-id="bba46-175">在 Microsoft 支援網站上傳支援封裝之前，若要編輯支援封裝，請先解密支援封裝、編輯檔案，然後重新加密。</span><span class="sxs-lookup"><span data-stu-id="bba46-175">To edit a support package before uploading it on the Microsoft Support site, first decrypt the support package, edit the files, and then re-encrypt it.</span></span> <span data-ttu-id="bba46-176">請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="bba46-176">Perform the following steps.</span></span>

#### <a name="to-edit-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="bba46-177">在 Windows PowerShell for StorSimple 中編輯支援封裝</span><span class="sxs-lookup"><span data-stu-id="bba46-177">To edit a support package in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="bba46-178">產生支援封裝，如稍早的 [在 Windows PowerShell for StorSimple 中建立支援封裝](#to-create-a-support-package-in-windows-powershell-for-storsimple)中所述。</span><span class="sxs-lookup"><span data-stu-id="bba46-178">Generate a support package as described earlier, in [To create a support package in Windows PowerShell for StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span></span>
2. <span data-ttu-id="bba46-179">[下載指令碼](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) 。</span><span class="sxs-lookup"><span data-stu-id="bba46-179">[Download the script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) locally on your client.</span></span>
3. <span data-ttu-id="bba46-180">匯入 Windows PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="bba46-180">Import the Windows PowerShell module.</span></span> <span data-ttu-id="bba46-181">指定下載指令碼時的本機資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="bba46-181">Specify the path to the local folder in which you downloaded the script.</span></span> <span data-ttu-id="bba46-182">若要匯入模組，請輸入：</span><span class="sxs-lookup"><span data-stu-id="bba46-182">To import the module, enter:</span></span>
   
    `Import-module <Path to the folder that contains the Windows PowerShell script>`
4. <span data-ttu-id="bba46-183">所有檔案都是已壓縮和加密的 *.aes* 檔案。</span><span class="sxs-lookup"><span data-stu-id="bba46-183">All the files are *.aes* files that are compressed and encrypted.</span></span> <span data-ttu-id="bba46-184">若要解壓縮並解密檔案，請輸入︰</span><span class="sxs-lookup"><span data-stu-id="bba46-184">To decompress and decrypt files, enter:</span></span>
   
    `Open-HcsSupportPackage <Path to the folder that contains support package files>`
   
    <span data-ttu-id="bba46-185">請注意，所有檔案現在顯示實際的副檔名。</span><span class="sxs-lookup"><span data-stu-id="bba46-185">Note that the actual file extensions are now displayed for all the files.</span></span>
   
    ![編輯支援封裝](./media/storsimple-create-manage-support-package/IC750706.png)
5. <span data-ttu-id="bba46-187">當系統提示您輸入加密複雜密碼時，請輸入您在建立支援封裝時使用的複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="bba46-187">When you're prompted for the encryption passphrase, enter the passphrase that you used when the support package was created.</span></span>
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for the following parameters:EncryptionPassphrase: ****
6. <span data-ttu-id="bba46-188">瀏覽至包含記錄檔的資料夾。</span><span class="sxs-lookup"><span data-stu-id="bba46-188">Browse to the folder that contains the log files.</span></span> <span data-ttu-id="bba46-189">因為記錄檔現在已解壓縮並解密，所以會顯示原始的副檔名。</span><span class="sxs-lookup"><span data-stu-id="bba46-189">Because the log files are now decompressed and decrypted, these will have original file extensions.</span></span> <span data-ttu-id="bba46-190">修改這些檔案來移除客戶特定資訊，例如磁碟區名稱和裝置 IP 位址，然後儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="bba46-190">Modify these files to remove any customer-specific information, such as volume names and device IP addresses, and save the files.</span></span>
7. <span data-ttu-id="bba46-191">關閉檔案會使用 Gzip 壓縮檔案，並使用 AES-256 加密。</span><span class="sxs-lookup"><span data-stu-id="bba46-191">Close the files to compress them with gzip and encrypt them with AES-256.</span></span> <span data-ttu-id="bba46-192">這是為了透過網路傳輸支援封裝時提高速度和安全性。</span><span class="sxs-lookup"><span data-stu-id="bba46-192">This is for speed and security in transferring the support package over a network.</span></span> <span data-ttu-id="bba46-193">若要壓縮及加密檔案，請輸入下列內容︰</span><span class="sxs-lookup"><span data-stu-id="bba46-193">To compress and encrypt files, enter the following:</span></span>
   
    `Close-HcsSupportPackage <Path to the folder that contains support package files>`
   
    ![編輯支援封裝](./media/storsimple-create-manage-support-package/IC750707.png)
8. <span data-ttu-id="bba46-195">出現提示時，提供加密複雜密碼給修改過的支援封裝。</span><span class="sxs-lookup"><span data-stu-id="bba46-195">When prompted, provide an encryption passphrase for the modified support package.</span></span>
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for the following parameters:EncryptionPassphrase: ****
9. <span data-ttu-id="bba46-196">記下新的複雜密碼，當接到要求時就能提供給 Microsoft 支援服務。</span><span class="sxs-lookup"><span data-stu-id="bba46-196">Write down the new passphrase, so that you can share it with Microsoft Support when requested.</span></span>

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a><span data-ttu-id="bba46-197">範例：在受密碼保護的共用中編輯支援封裝中的檔案</span><span class="sxs-lookup"><span data-stu-id="bba46-197">Example: Editing files in a support package on a password-protected share</span></span>
<span data-ttu-id="bba46-198">下列範例將示範如何解密、編輯和重新加密支援封裝。</span><span class="sxs-lookup"><span data-stu-id="bba46-198">The following example shows how to decrypt, edit, and re-encrypt a support package.</span></span>

        PS C:\WINDOWS\system32> Import-module C:\Users\Default\StorSimple\SupportPackage\HCSSupportPackageTools.psm1

        PS C:\WINDOWS\system32> Open-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Open-HcsSupportPackage at command pipeline position 1

        Supply values for the following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32> Close-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Close-HcsSupportPackage at command pipeline position 1

        Supply values for the following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32>

## <a name="next-steps"></a><span data-ttu-id="bba46-199">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bba46-199">Next steps</span></span>
* <span data-ttu-id="bba46-200">了解如何 [使用支援封裝和裝置記錄對裝置部署進行疑難排解](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting)。</span><span class="sxs-lookup"><span data-stu-id="bba46-200">Learn how to [use support packages and device logs to troubleshoot your device deployment](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span></span>
* <span data-ttu-id="bba46-201">了解如何 [使用 StorSimple Manager 服務管理 StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="bba46-201">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

