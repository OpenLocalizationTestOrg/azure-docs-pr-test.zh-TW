---
title: "建立 StorSimple 8000 系列支援封裝 | Microsoft Docs"
description: "了解如何建立、解密和編輯 StorSimple 8000 系列裝置的支援封裝。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 92abbb96b2117e10800de61b5c405a784453265b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-a-support-package-for-storsimple-8000-series"></a><span data-ttu-id="00e97-103">建立及管理 StorSimple 8000 系列的支援封裝</span><span class="sxs-lookup"><span data-stu-id="00e97-103">Create and manage a support package for StorSimple 8000 series</span></span>

## <a name="overview"></a><span data-ttu-id="00e97-104">概觀</span><span class="sxs-lookup"><span data-stu-id="00e97-104">Overview</span></span>

<span data-ttu-id="00e97-105">StorSimple 支援封裝是一種簡便的機制，可收集所有相關的記錄以協助 Microsoft 支援服務針對任何 StorSimple 裝置問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="00e97-105">A StorSimple support package is an easy-to-use mechanism that collects all relevant logs to assist Microsoft Support with troubleshooting any StorSimple device issues.</span></span> <span data-ttu-id="00e97-106">收集的記錄都會經過加密並壓縮。</span><span class="sxs-lookup"><span data-stu-id="00e97-106">The collected logs are encrypted and compressed.</span></span>

<span data-ttu-id="00e97-107">本教學課程包含建立和管理 StorSimple 8000 系列裝置之支援封裝的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="00e97-107">This tutorial includes step-by-step instructions to create and manage the support package for your StorSimple 8000 series device.</span></span> <span data-ttu-id="00e97-108">如果您使用 StorSimple Virtual Array，請移至[產生記錄檔封裝](storsimple-ova-web-ui-admin.md#generate-a-log-package)。</span><span class="sxs-lookup"><span data-stu-id="00e97-108">If you are working with a StorSimple Virtual Array, go to [generate a log package](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span></span>

## <a name="create-a-support-package"></a><span data-ttu-id="00e97-109">建立支援封裝</span><span class="sxs-lookup"><span data-stu-id="00e97-109">Create a support package</span></span>

<span data-ttu-id="00e97-110">在某些情況下，您必須透過 Windows PowerShell for StorSimple 手動建立支援封裝。</span><span class="sxs-lookup"><span data-stu-id="00e97-110">In some cases, you'll need to manually create the support package through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="00e97-111">例如：</span><span class="sxs-lookup"><span data-stu-id="00e97-111">For example:</span></span>

* <span data-ttu-id="00e97-112">如果您在與 Microsoft 支援服務共用您的記錄檔之前，必須從其中移除機密資訊。</span><span class="sxs-lookup"><span data-stu-id="00e97-112">If you need to remove sensitive information from your log files prior to sharing with Microsoft Support.</span></span>
* <span data-ttu-id="00e97-113">如果您在上傳封裝時，因為連線能力問題而遇到困難。</span><span class="sxs-lookup"><span data-stu-id="00e97-113">If you are having difficulty uploading the package due to connectivity issues.</span></span>

<span data-ttu-id="00e97-114">您可以透過電子郵件與 Microsoft 支援服務共用手動產生的支援封裝。</span><span class="sxs-lookup"><span data-stu-id="00e97-114">You can share your manually generated support package with Microsoft Support over email.</span></span> <span data-ttu-id="00e97-115">執行下列步驟在 Windows PowerShell for StorSimple 中建立支援封裝。</span><span class="sxs-lookup"><span data-stu-id="00e97-115">Perform the following steps to create a support package in Windows PowerShell for StorSimple.</span></span>

#### <a name="to-create-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="00e97-116">在 Windows PowerShell for StorSimple 中建立支援封裝</span><span class="sxs-lookup"><span data-stu-id="00e97-116">To create a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="00e97-117">若要在用來連接至 StorSimple 裝置的遠端電腦上，以系統管理員身分啟動 Windows PowerShell 工作階段，請輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="00e97-117">To start a Windows PowerShell session as an administrator on the remote computer that's used to connect to your StorSimple device, enter the following command:</span></span>
   
    `Start PowerShell`
2. <span data-ttu-id="00e97-118">在 Windows PowerShell 工作階段中，連接到裝置的 SSAdmin 主控台：</span><span class="sxs-lookup"><span data-stu-id="00e97-118">In the Windows PowerShell session, connect to the SSAdmin Console of your device:</span></span>
   
   1. <span data-ttu-id="00e97-119">在命令提示字元中，輸入：</span><span class="sxs-lookup"><span data-stu-id="00e97-119">At the command prompt, enter:</span></span>
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   2. <span data-ttu-id="00e97-120">在開啟的對話方塊中，輸入您的裝置系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="00e97-120">In the dialog box that opens, enter your device administrator password.</span></span> <span data-ttu-id="00e97-121">預設密碼為 _Password1_。</span><span class="sxs-lookup"><span data-stu-id="00e97-121">The default password is _Password1_.</span></span>
     
      ![[PowerShell 認證] 對話方塊](./media/storsimple-8000-create-manage-support-package/IC740962.png)
   3. <span data-ttu-id="00e97-123">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="00e97-123">Select **OK**.</span></span>
   4. <span data-ttu-id="00e97-124">在命令提示字元中，輸入：</span><span class="sxs-lookup"><span data-stu-id="00e97-124">At the command prompt, enter:</span></span>
     
      `Enter-PSSession $MS`
3. <span data-ttu-id="00e97-125">在開啟的工作階段中，輸入適當的命令。</span><span class="sxs-lookup"><span data-stu-id="00e97-125">In the session that opens, enter the appropriate command.</span></span>
   
   * <span data-ttu-id="00e97-126">對於受密碼保護的網路共用，請輸入：</span><span class="sxs-lookup"><span data-stu-id="00e97-126">For network shares that are password protected, enter:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       <span data-ttu-id="00e97-127">系統會提示您輸入密碼、網路共用的資料夾路徑及加密複雜密碼 (因為支援封裝已加密)。</span><span class="sxs-lookup"><span data-stu-id="00e97-127">You'll be prompted for a password, a path to the network shared folder, and an encryption passphrase (because the support package is encrypted).</span></span> <span data-ttu-id="00e97-128">然後會在指定的資料夾中建立支援封裝。</span><span class="sxs-lookup"><span data-stu-id="00e97-128">A support package is then created in the specified folder.</span></span>
   * <span data-ttu-id="00e97-129">對於不受密碼保護的共用內容，您不需要 `-Credential` 參數。</span><span class="sxs-lookup"><span data-stu-id="00e97-129">For shares that are not password protected, you do not need the `-Credential` parameter.</span></span> <span data-ttu-id="00e97-130">輸入以下資訊：</span><span class="sxs-lookup"><span data-stu-id="00e97-130">Enter the following:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       <span data-ttu-id="00e97-131">在指定的網路共用資料夾中，同時為兩個控制器建立支援封裝。</span><span class="sxs-lookup"><span data-stu-id="00e97-131">The support package is created for both controllers in the specified network shared folder.</span></span> <span data-ttu-id="00e97-132">這是加密的壓縮檔案，可傳送給 Microsoft 支援服務進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="00e97-132">It's an encrypted, compressed file that can be sent to Microsoft Support for troubleshooting.</span></span> <span data-ttu-id="00e97-133">如需詳細資訊，請參閱 [連絡 Microsoft 支援服務](storsimple-8000-contact-microsoft-support.md)。</span><span class="sxs-lookup"><span data-stu-id="00e97-133">For more information, see [Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

### <a name="the-export-hcssupportpackage-cmdlet-parameters"></a><span data-ttu-id="00e97-134">The Export-HcsSupportPackage cmdlet 參數</span><span class="sxs-lookup"><span data-stu-id="00e97-134">The Export-HcsSupportPackage cmdlet parameters</span></span>

<span data-ttu-id="00e97-135">您可以使用下列參數搭配 Export-HcsSupportPackage cmdlet。</span><span class="sxs-lookup"><span data-stu-id="00e97-135">You can use the following parameters with the Export-HcsSupportPackage cmdlet.</span></span>

| <span data-ttu-id="00e97-136">參數</span><span class="sxs-lookup"><span data-stu-id="00e97-136">Parameter</span></span> | <span data-ttu-id="00e97-137">必要/選用</span><span class="sxs-lookup"><span data-stu-id="00e97-137">Required/Optional</span></span> | <span data-ttu-id="00e97-138">說明</span><span class="sxs-lookup"><span data-stu-id="00e97-138">Description</span></span> |
| --- | --- | --- |
| `-Path` |<span data-ttu-id="00e97-139">必要</span><span class="sxs-lookup"><span data-stu-id="00e97-139">Required</span></span> |<span data-ttu-id="00e97-140">用來提供存放支援封裝的網路共用資料夾位置。</span><span class="sxs-lookup"><span data-stu-id="00e97-140">Use to provide the location of the network shared folder in which the support package is placed.</span></span> |
| `-EncryptionPassphrase` |<span data-ttu-id="00e97-141">必要</span><span class="sxs-lookup"><span data-stu-id="00e97-141">Required</span></span> |<span data-ttu-id="00e97-142">用來提供複雜密碼，以協助加密支援封裝。</span><span class="sxs-lookup"><span data-stu-id="00e97-142">Use to provide a passphrase to help encrypt the support package.</span></span> |
| `-Credential` |<span data-ttu-id="00e97-143">選用</span><span class="sxs-lookup"><span data-stu-id="00e97-143">Optional</span></span> |<span data-ttu-id="00e97-144">用來提供網路共用資料夾的存取認證。</span><span class="sxs-lookup"><span data-stu-id="00e97-144">Use to supply access credentials for the network shared folder.</span></span> |
| `-Force` |<span data-ttu-id="00e97-145">選用</span><span class="sxs-lookup"><span data-stu-id="00e97-145">Optional</span></span> |<span data-ttu-id="00e97-146">用來略過加密複雜密碼確認步驟。</span><span class="sxs-lookup"><span data-stu-id="00e97-146">Use to skip the encryption passphrase confirmation step.</span></span> |
| `-PackageTag` |<span data-ttu-id="00e97-147">選用</span><span class="sxs-lookup"><span data-stu-id="00e97-147">Optional</span></span> |<span data-ttu-id="00e97-148">用來指定 *Path* 下存放支援封裝的目錄。</span><span class="sxs-lookup"><span data-stu-id="00e97-148">Use to specify a directory under *Path* in which the support package is placed.</span></span> <span data-ttu-id="00e97-149">預設值是 [裝置名稱]-[目前日期和時間：yyyy-MM-dd-HH-mm-ss]。</span><span class="sxs-lookup"><span data-stu-id="00e97-149">The default is [device name]-[current date and time:yyyy-MM-dd-HH-mm-ss].</span></span> |
| `-Scope` |<span data-ttu-id="00e97-150">選用</span><span class="sxs-lookup"><span data-stu-id="00e97-150">Optional</span></span> |<span data-ttu-id="00e97-151">指定為 **Cluster** (預設值) 可以為兩個控制器建立支援封裝。</span><span class="sxs-lookup"><span data-stu-id="00e97-151">Specify as **Cluster** (default) to create a support package for both controllers.</span></span> <span data-ttu-id="00e97-152">如果您只想針對目前的控制器建立封裝，請指定 **Controller**。</span><span class="sxs-lookup"><span data-stu-id="00e97-152">If you want to create a package only for the current controller, specify **Controller**.</span></span> |

## <a name="edit-a-support-package"></a><span data-ttu-id="00e97-153">編輯支援封裝</span><span class="sxs-lookup"><span data-stu-id="00e97-153">Edit a support package</span></span>

<span data-ttu-id="00e97-154">在您產生支援封裝之後，可能需要編輯封裝以移除機密資訊。</span><span class="sxs-lookup"><span data-stu-id="00e97-154">After you have generated a support package, you might need to edit the package to remove sensitive information.</span></span> <span data-ttu-id="00e97-155">這可能包括磁碟區名稱、裝置 IP 位址，以及記錄檔中的備份名稱。</span><span class="sxs-lookup"><span data-stu-id="00e97-155">This can include volume names, device IP addresses, and backup names from the log files.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="00e97-156">您只能編輯透過 Windows PowerShell for StorSimple 產生的支援封裝。</span><span class="sxs-lookup"><span data-stu-id="00e97-156">You can only edit a support package that was generated through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="00e97-157">您無法編輯在 Azure 入口網站中以 StorSimple 裝置管理員服務建立的封裝。</span><span class="sxs-lookup"><span data-stu-id="00e97-157">You can't edit a package created in the Azure portal with StorSimple Device Manager service.</span></span>

<span data-ttu-id="00e97-158">在 Microsoft 支援網站上傳支援封裝之前，若要編輯支援封裝，請先解密支援封裝、編輯檔案，然後重新加密。</span><span class="sxs-lookup"><span data-stu-id="00e97-158">To edit a support package before uploading it on the Microsoft Support site, first decrypt the support package, edit the files, and then re-encrypt it.</span></span> <span data-ttu-id="00e97-159">請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="00e97-159">Perform the following steps.</span></span>

#### <a name="to-edit-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="00e97-160">在 Windows PowerShell for StorSimple 中編輯支援封裝</span><span class="sxs-lookup"><span data-stu-id="00e97-160">To edit a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="00e97-161">產生支援封裝，如稍早的 [在 Windows PowerShell for StorSimple 中建立支援封裝](#to-create-a-support-package-in-windows-powershell-for-storsimple)中所述。</span><span class="sxs-lookup"><span data-stu-id="00e97-161">Generate a support package as described earlier, in [To create a support package in Windows PowerShell for StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span></span>
2. <span data-ttu-id="00e97-162">[下載指令碼](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) 。</span><span class="sxs-lookup"><span data-stu-id="00e97-162">[Download the script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) locally on your client.</span></span>
3. <span data-ttu-id="00e97-163">匯入 Windows PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="00e97-163">Import the Windows PowerShell module.</span></span> <span data-ttu-id="00e97-164">指定下載指令碼時的本機資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="00e97-164">Specify the path to the local folder in which you downloaded the script.</span></span> <span data-ttu-id="00e97-165">若要匯入模組，請輸入：</span><span class="sxs-lookup"><span data-stu-id="00e97-165">To import the module, enter:</span></span>
   
    `Import-module <Path to the folder that contains the Windows PowerShell script>`
4. <span data-ttu-id="00e97-166">所有檔案都是已壓縮和加密的 *.aes* 檔案。</span><span class="sxs-lookup"><span data-stu-id="00e97-166">All the files are *.aes* files that are compressed and encrypted.</span></span> <span data-ttu-id="00e97-167">若要解壓縮並解密檔案，請輸入︰</span><span class="sxs-lookup"><span data-stu-id="00e97-167">To decompress and decrypt files, enter:</span></span>
   
    `Open-HcsSupportPackage <Path to the folder that contains support package files>`
   
    <span data-ttu-id="00e97-168">請注意，所有檔案現在顯示實際的副檔名。</span><span class="sxs-lookup"><span data-stu-id="00e97-168">Note that the actual file extensions are now displayed for all the files.</span></span>
   
    ![編輯支援封裝](./media/storsimple-8000-create-manage-support-package/IC750706.png)
5. <span data-ttu-id="00e97-170">當系統提示您輸入加密複雜密碼時，請輸入您在建立支援封裝時使用的複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="00e97-170">When you're prompted for the encryption passphrase, enter the passphrase that you used when the support package was created.</span></span>
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for the following parameters:EncryptionPassphrase: ****
6. <span data-ttu-id="00e97-171">瀏覽至包含記錄檔的資料夾。</span><span class="sxs-lookup"><span data-stu-id="00e97-171">Browse to the folder that contains the log files.</span></span> <span data-ttu-id="00e97-172">因為記錄檔現在已解壓縮並解密，所以會顯示原始的副檔名。</span><span class="sxs-lookup"><span data-stu-id="00e97-172">Because the log files are now decompressed and decrypted, these will have original file extensions.</span></span> <span data-ttu-id="00e97-173">修改這些檔案來移除客戶特定資訊，例如磁碟區名稱和裝置 IP 位址，然後儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="00e97-173">Modify these files to remove any customer-specific information, such as volume names and device IP addresses, and save the files.</span></span>
7. <span data-ttu-id="00e97-174">關閉檔案會使用 Gzip 壓縮檔案，並使用 AES-256 加密。</span><span class="sxs-lookup"><span data-stu-id="00e97-174">Close the files to compress them with gzip and encrypt them with AES-256.</span></span> <span data-ttu-id="00e97-175">這是為了透過網路傳輸支援封裝時提高速度和安全性。</span><span class="sxs-lookup"><span data-stu-id="00e97-175">This is for speed and security in transferring the support package over a network.</span></span> <span data-ttu-id="00e97-176">若要壓縮及加密檔案，請輸入下列內容︰</span><span class="sxs-lookup"><span data-stu-id="00e97-176">To compress and encrypt files, enter the following:</span></span>
   
    `Close-HcsSupportPackage <Path to the folder that contains support package files>`
   
    ![編輯支援封裝](./media/storsimple-8000-create-manage-support-package/IC750707.png)
8. <span data-ttu-id="00e97-178">出現提示時，提供加密複雜密碼給修改過的支援封裝。</span><span class="sxs-lookup"><span data-stu-id="00e97-178">When prompted, provide an encryption passphrase for the modified support package.</span></span>
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for the following parameters:EncryptionPassphrase: ****
9. <span data-ttu-id="00e97-179">記下新的複雜密碼，當接到要求時就能提供給 Microsoft 支援服務。</span><span class="sxs-lookup"><span data-stu-id="00e97-179">Write down the new passphrase, so that you can share it with Microsoft Support when requested.</span></span>

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a><span data-ttu-id="00e97-180">範例：在受密碼保護的共用中編輯支援封裝中的檔案</span><span class="sxs-lookup"><span data-stu-id="00e97-180">Example: Editing files in a support package on a password-protected share</span></span>

<span data-ttu-id="00e97-181">下列範例將示範如何解密、編輯和重新加密支援封裝。</span><span class="sxs-lookup"><span data-stu-id="00e97-181">The following example shows how to decrypt, edit, and re-encrypt a support package.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="00e97-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="00e97-182">Next steps</span></span>

* <span data-ttu-id="00e97-183">深入了解[支援封裝中收集的資訊](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)</span><span class="sxs-lookup"><span data-stu-id="00e97-183">Learn about the [information collected in the Support package](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)</span></span>
* <span data-ttu-id="00e97-184">了解如何 [使用支援封裝和裝置記錄對裝置部署進行疑難排解](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting)。</span><span class="sxs-lookup"><span data-stu-id="00e97-184">Learn how to [use support packages and device logs to troubleshoot your device deployment](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span></span>
* <span data-ttu-id="00e97-185">了解如何[使用 StorSimple 裝置管理員服務管理 StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="00e97-185">Learn how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

