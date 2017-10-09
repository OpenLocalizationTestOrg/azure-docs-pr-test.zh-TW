---
title: "aaaCreate StorSimple 8000 系列的支援封裝 |Microsoft 文件"
description: "了解如何 toocreate，解密，以及編輯您的 StorSimple 8000 系列裝置的支援封裝。"
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
ms.openlocfilehash: 857555b6ba31b1527f8f00d19818ebbec6005d0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-support-package-for-storsimple-8000-series"></a><span data-ttu-id="38644-103">建立及管理 StorSimple 8000 系列的支援封裝</span><span class="sxs-lookup"><span data-stu-id="38644-103">Create and manage a support package for StorSimple 8000 series</span></span>

## <a name="overview"></a><span data-ttu-id="38644-104">概觀</span><span class="sxs-lookup"><span data-stu-id="38644-104">Overview</span></span>

<span data-ttu-id="38644-105">StorSimple 支援封裝是一種方便使用的機制，會收集任何 StorSimple 裝置的問題進行疑難排解的所有相關記錄 tooassist Microsoft 支援服務。</span><span class="sxs-lookup"><span data-stu-id="38644-105">A StorSimple support package is an easy-to-use mechanism that collects all relevant logs tooassist Microsoft Support with troubleshooting any StorSimple device issues.</span></span> <span data-ttu-id="38644-106">hello 收集記錄檔會加密和壓縮。</span><span class="sxs-lookup"><span data-stu-id="38644-106">hello collected logs are encrypted and compressed.</span></span>

<span data-ttu-id="38644-107">本教學課程包含逐步指示 toocreate 並管理您的 StorSimple 8000 系列裝置 hello 支援封裝。</span><span class="sxs-lookup"><span data-stu-id="38644-107">This tutorial includes step-by-step instructions toocreate and manage hello support package for your StorSimple 8000 series device.</span></span> <span data-ttu-id="38644-108">如果您正在使用 StorSimple Virtual Array，請移至太[產生記錄檔套件](storsimple-ova-web-ui-admin.md#generate-a-log-package)。</span><span class="sxs-lookup"><span data-stu-id="38644-108">If you are working with a StorSimple Virtual Array, go too[generate a log package](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span></span>

## <a name="create-a-support-package"></a><span data-ttu-id="38644-109">建立支援封裝</span><span class="sxs-lookup"><span data-stu-id="38644-109">Create a support package</span></span>

<span data-ttu-id="38644-110">在某些情況下，您將需要 toomanually 建立 hello 支援封裝，透過 Windows PowerShell for StorSimple。</span><span class="sxs-lookup"><span data-stu-id="38644-110">In some cases, you'll need toomanually create hello support package through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="38644-111">例如：</span><span class="sxs-lookup"><span data-stu-id="38644-111">For example:</span></span>

* <span data-ttu-id="38644-112">如果您需要 tooremove 機密資訊從您的記錄檔先前 toosharing 向 Microsoft 支援。</span><span class="sxs-lookup"><span data-stu-id="38644-112">If you need tooremove sensitive information from your log files prior toosharing with Microsoft Support.</span></span>
* <span data-ttu-id="38644-113">如果您無法上傳 hello 封裝，因為 tooconnectivity 問題。</span><span class="sxs-lookup"><span data-stu-id="38644-113">If you are having difficulty uploading hello package due tooconnectivity issues.</span></span>

<span data-ttu-id="38644-114">您可以透過電子郵件與 Microsoft 支援服務共用手動產生的支援封裝。</span><span class="sxs-lookup"><span data-stu-id="38644-114">You can share your manually generated support package with Microsoft Support over email.</span></span> <span data-ttu-id="38644-115">執行下列步驟 toocreate 支援封裝中 Windows PowerShell for StorSimple 的 hello。</span><span class="sxs-lookup"><span data-stu-id="38644-115">Perform hello following steps toocreate a support package in Windows PowerShell for StorSimple.</span></span>

#### <a name="toocreate-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="38644-116">toocreate Windows PowerShell for StorSimple 中的支援套件</span><span class="sxs-lookup"><span data-stu-id="38644-116">toocreate a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="38644-117">toostart hello 已使用 tooconnect tooyour StorSimple 裝置的遠端電腦上系統管理員身分的 Windows PowerShell 工作階段輸入 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="38644-117">toostart a Windows PowerShell session as an administrator on hello remote computer that's used tooconnect tooyour StorSimple device, enter hello following command:</span></span>
   
    `Start PowerShell`
2. <span data-ttu-id="38644-118">Hello Windows PowerShell 工作階段中，連接 toohello SSAdmin 主控台，您的裝置：</span><span class="sxs-lookup"><span data-stu-id="38644-118">In hello Windows PowerShell session, connect toohello SSAdmin Console of your device:</span></span>
   
   1. <span data-ttu-id="38644-119">在 hello 命令提示字元中輸入：</span><span class="sxs-lookup"><span data-stu-id="38644-119">At hello command prompt, enter:</span></span>
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   2. <span data-ttu-id="38644-120">在 hello 開啟對話方塊，輸入您的裝置系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="38644-120">In hello dialog box that opens, enter your device administrator password.</span></span> <span data-ttu-id="38644-121">hello 預設密碼為_Password1_。</span><span class="sxs-lookup"><span data-stu-id="38644-121">hello default password is _Password1_.</span></span>
     
      ![[PowerShell 認證] 對話方塊](./media/storsimple-8000-create-manage-support-package/IC740962.png)
   3. <span data-ttu-id="38644-123">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="38644-123">Select **OK**.</span></span>
   4. <span data-ttu-id="38644-124">在 hello 命令提示字元中輸入：</span><span class="sxs-lookup"><span data-stu-id="38644-124">At hello command prompt, enter:</span></span>
     
      `Enter-PSSession $MS`
3. <span data-ttu-id="38644-125">在開啟的 hello 工作階段，輸入 hello 適當的命令。</span><span class="sxs-lookup"><span data-stu-id="38644-125">In hello session that opens, enter hello appropriate command.</span></span>
   
   * <span data-ttu-id="38644-126">對於受密碼保護的網路共用，請輸入：</span><span class="sxs-lookup"><span data-stu-id="38644-126">For network shares that are password protected, enter:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       <span data-ttu-id="38644-127">（因為加密 hello 支援封裝），將會提示您輸入密碼、 路徑 toohello 網路共用的資料夾，以及加密複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="38644-127">You'll be prompted for a password, a path toohello network shared folder, and an encryption passphrase (because hello support package is encrypted).</span></span> <span data-ttu-id="38644-128">Hello 指定資料夾中，然後會建立支援封裝。</span><span class="sxs-lookup"><span data-stu-id="38644-128">A support package is then created in hello specified folder.</span></span>
   * <span data-ttu-id="38644-129">對於不受密碼保護的共用，您不需要 hello`-Credential`參數。</span><span class="sxs-lookup"><span data-stu-id="38644-129">For shares that are not password protected, you do not need hello `-Credential` parameter.</span></span> <span data-ttu-id="38644-130">輸入 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="38644-130">Enter hello following:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       <span data-ttu-id="38644-131">hello 支援封裝會建立兩個控制器 hello 指定的網路共用資料夾中。</span><span class="sxs-lookup"><span data-stu-id="38644-131">hello support package is created for both controllers in hello specified network shared folder.</span></span> <span data-ttu-id="38644-132">這是可以用於疑難排解傳送 tooMicrosoft 支援加密、 壓縮檔案。</span><span class="sxs-lookup"><span data-stu-id="38644-132">It's an encrypted, compressed file that can be sent tooMicrosoft Support for troubleshooting.</span></span> <span data-ttu-id="38644-133">如需詳細資訊，請參閱 [連絡 Microsoft 支援服務](storsimple-8000-contact-microsoft-support.md)。</span><span class="sxs-lookup"><span data-stu-id="38644-133">For more information, see [Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

### <a name="hello-export-hcssupportpackage-cmdlet-parameters"></a><span data-ttu-id="38644-134">hello Export-hcssupportpackage cmdlet 參數</span><span class="sxs-lookup"><span data-stu-id="38644-134">hello Export-HcsSupportPackage cmdlet parameters</span></span>

<span data-ttu-id="38644-135">您可以使用下列參數使用 hello Export-hcssupportpackage cmdlet 的 hello。</span><span class="sxs-lookup"><span data-stu-id="38644-135">You can use hello following parameters with hello Export-HcsSupportPackage cmdlet.</span></span>

| <span data-ttu-id="38644-136">參數</span><span class="sxs-lookup"><span data-stu-id="38644-136">Parameter</span></span> | <span data-ttu-id="38644-137">必要/選用</span><span class="sxs-lookup"><span data-stu-id="38644-137">Required/Optional</span></span> | <span data-ttu-id="38644-138">說明</span><span class="sxs-lookup"><span data-stu-id="38644-138">Description</span></span> |
| --- | --- | --- |
| `-Path` |<span data-ttu-id="38644-139">必要</span><span class="sxs-lookup"><span data-stu-id="38644-139">Required</span></span> |<span data-ttu-id="38644-140">使用 tooprovide hello hello 網路共用資料夾中的 hello 放置支援封裝位置。</span><span class="sxs-lookup"><span data-stu-id="38644-140">Use tooprovide hello location of hello network shared folder in which hello support package is placed.</span></span> |
| `-EncryptionPassphrase` |<span data-ttu-id="38644-141">必要</span><span class="sxs-lookup"><span data-stu-id="38644-141">Required</span></span> |<span data-ttu-id="38644-142">使用 tooprovide 複雜密碼 toohelp 加密 hello 支援封裝。</span><span class="sxs-lookup"><span data-stu-id="38644-142">Use tooprovide a passphrase toohelp encrypt hello support package.</span></span> |
| `-Credential` |<span data-ttu-id="38644-143">選用</span><span class="sxs-lookup"><span data-stu-id="38644-143">Optional</span></span> |<span data-ttu-id="38644-144">使用 hello 網路共用資料夾 toosupply 存取認證。</span><span class="sxs-lookup"><span data-stu-id="38644-144">Use toosupply access credentials for hello network shared folder.</span></span> |
| `-Force` |<span data-ttu-id="38644-145">選用</span><span class="sxs-lookup"><span data-stu-id="38644-145">Optional</span></span> |<span data-ttu-id="38644-146">使用 tooskip hello 加密複雜密碼確認步驟。</span><span class="sxs-lookup"><span data-stu-id="38644-146">Use tooskip hello encryption passphrase confirmation step.</span></span> |
| `-PackageTag` |<span data-ttu-id="38644-147">選用</span><span class="sxs-lookup"><span data-stu-id="38644-147">Optional</span></span> |<span data-ttu-id="38644-148">使用 toospecify 下的目錄*路徑*的 hello 支援放置封裝。</span><span class="sxs-lookup"><span data-stu-id="38644-148">Use toospecify a directory under *Path* in which hello support package is placed.</span></span> <span data-ttu-id="38644-149">hello 預設值為 [裝置名稱]-[目前的日期和 time: yyyy-mm-dd-hh-mm-ss]。</span><span class="sxs-lookup"><span data-stu-id="38644-149">hello default is [device name]-[current date and time:yyyy-MM-dd-HH-mm-ss].</span></span> |
| `-Scope` |<span data-ttu-id="38644-150">選用</span><span class="sxs-lookup"><span data-stu-id="38644-150">Optional</span></span> |<span data-ttu-id="38644-151">指定為**叢集**（預設值） toocreate 兩個控制器的支援封裝。</span><span class="sxs-lookup"><span data-stu-id="38644-151">Specify as **Cluster** (default) toocreate a support package for both controllers.</span></span> <span data-ttu-id="38644-152">如果您想要 toocreate 封裝只 hello 目前的控制器，指定**控制器**。</span><span class="sxs-lookup"><span data-stu-id="38644-152">If you want toocreate a package only for hello current controller, specify **Controller**.</span></span> |

## <a name="edit-a-support-package"></a><span data-ttu-id="38644-153">編輯支援封裝</span><span class="sxs-lookup"><span data-stu-id="38644-153">Edit a support package</span></span>

<span data-ttu-id="38644-154">產生支援套件後，您可能需要 tooedit hello 封裝 tooremove 機密資訊。</span><span class="sxs-lookup"><span data-stu-id="38644-154">After you have generated a support package, you might need tooedit hello package tooremove sensitive information.</span></span> <span data-ttu-id="38644-155">這可以包括磁碟區名稱、 裝置 IP 位址，以及從 hello 記錄檔的備份名稱。</span><span class="sxs-lookup"><span data-stu-id="38644-155">This can include volume names, device IP addresses, and backup names from hello log files.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="38644-156">您只能編輯透過 Windows PowerShell for StorSimple 產生的支援封裝。</span><span class="sxs-lookup"><span data-stu-id="38644-156">You can only edit a support package that was generated through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="38644-157">您無法編輯 hello 與 StorSimple 裝置管理員服務的 Azure 入口網站中建立的封裝。</span><span class="sxs-lookup"><span data-stu-id="38644-157">You can't edit a package created in hello Azure portal with StorSimple Device Manager service.</span></span>

<span data-ttu-id="38644-158">tooedit 之前將其 hello Microsoft 支援服務網站上, 傳支援封裝會先解密 hello 支援封裝、 編輯 hello 檔案，然後重新加密。</span><span class="sxs-lookup"><span data-stu-id="38644-158">tooedit a support package before uploading it on hello Microsoft Support site, first decrypt hello support package, edit hello files, and then re-encrypt it.</span></span> <span data-ttu-id="38644-159">執行下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="38644-159">Perform hello following steps.</span></span>

#### <a name="tooedit-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="38644-160">tooedit Windows PowerShell for StorSimple 中的支援套件</span><span class="sxs-lookup"><span data-stu-id="38644-160">tooedit a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="38644-161">產生支援封裝中稍早所述[toocreate 支援套件，Windows PowerShell for StorSimple 中](#to-create-a-support-package-in-windows-powershell-for-storsimple)。</span><span class="sxs-lookup"><span data-stu-id="38644-161">Generate a support package as described earlier, in [toocreate a support package in Windows PowerShell for StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span></span>
2. <span data-ttu-id="38644-162">[下載 hello 指令碼](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65)在您的用戶端的本機上。</span><span class="sxs-lookup"><span data-stu-id="38644-162">[Download hello script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) locally on your client.</span></span>
3. <span data-ttu-id="38644-163">匯入 hello Windows PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="38644-163">Import hello Windows PowerShell module.</span></span> <span data-ttu-id="38644-164">指定 hello 路徑 toohello 本機資料夾下載 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="38644-164">Specify hello path toohello local folder in which you downloaded hello script.</span></span> <span data-ttu-id="38644-165">tooimport hello 模組中，輸入：</span><span class="sxs-lookup"><span data-stu-id="38644-165">tooimport hello module, enter:</span></span>
   
    `Import-module <Path toohello folder that contains hello Windows PowerShell script>`
4. <span data-ttu-id="38644-166">所有的 hello 檔案都*.aes*經過壓縮並加密的檔案。</span><span class="sxs-lookup"><span data-stu-id="38644-166">All hello files are *.aes* files that are compressed and encrypted.</span></span> <span data-ttu-id="38644-167">toodecompress 和解密檔案中，輸入：</span><span class="sxs-lookup"><span data-stu-id="38644-167">toodecompress and decrypt files, enter:</span></span>
   
    `Open-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    <span data-ttu-id="38644-168">請注意 hello 的所有檔案現在會顯示 hello 實際的檔案副檔名。</span><span class="sxs-lookup"><span data-stu-id="38644-168">Note that hello actual file extensions are now displayed for all hello files.</span></span>
   
    ![編輯支援封裝](./media/storsimple-8000-create-manage-support-package/IC750706.png)
5. <span data-ttu-id="38644-170">當系統提示您輸入 hello 加密複雜密碼，請輸入 hello 建立 hello 支援封裝時所使用的複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="38644-170">When you're prompted for hello encryption passphrase, enter hello passphrase that you used when hello support package was created.</span></span>
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for hello following parameters:EncryptionPassphrase: ****
6. <span data-ttu-id="38644-171">瀏覽 toohello 包含 hello 記錄檔的資料夾。</span><span class="sxs-lookup"><span data-stu-id="38644-171">Browse toohello folder that contains hello log files.</span></span> <span data-ttu-id="38644-172">Hello 記錄檔現在會解壓縮並解密，因為它們會有原始副檔名。</span><span class="sxs-lookup"><span data-stu-id="38644-172">Because hello log files are now decompressed and decrypted, these will have original file extensions.</span></span> <span data-ttu-id="38644-173">修改這些檔案 tooremove 任何客戶特定資訊，例如磁碟區名稱和裝置的 IP 位址，然後儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="38644-173">Modify these files tooremove any customer-specific information, such as volume names and device IP addresses, and save hello files.</span></span>
7. <span data-ttu-id="38644-174">關閉 hello 檔案 toocompress 以 gzip 它們，並以 aes-256 加密它們。</span><span class="sxs-lookup"><span data-stu-id="38644-174">Close hello files toocompress them with gzip and encrypt them with AES-256.</span></span> <span data-ttu-id="38644-175">這適用於速度和透過網路傳送嗨支援封裝中的安全性。</span><span class="sxs-lookup"><span data-stu-id="38644-175">This is for speed and security in transferring hello support package over a network.</span></span> <span data-ttu-id="38644-176">toocompress 和加密的檔案中，輸入 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="38644-176">toocompress and encrypt files, enter hello following:</span></span>
   
    `Close-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    ![編輯支援封裝](./media/storsimple-8000-create-manage-support-package/IC750707.png)
8. <span data-ttu-id="38644-178">出現提示時，提供 hello 已修改之支援封裝加密複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="38644-178">When prompted, provide an encryption passphrase for hello modified support package.</span></span>
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for hello following parameters:EncryptionPassphrase: ****
9. <span data-ttu-id="38644-179">記下 hello 新的複雜密碼，讓您與 Microsoft 支援服務要求時可以共用。</span><span class="sxs-lookup"><span data-stu-id="38644-179">Write down hello new passphrase, so that you can share it with Microsoft Support when requested.</span></span>

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a><span data-ttu-id="38644-180">範例：在受密碼保護的共用中編輯支援封裝中的檔案</span><span class="sxs-lookup"><span data-stu-id="38644-180">Example: Editing files in a support package on a password-protected share</span></span>

<span data-ttu-id="38644-181">hello 下列範例顯示如何 toodecrypt、 編輯和重新加密支援封裝。</span><span class="sxs-lookup"><span data-stu-id="38644-181">hello following example shows how toodecrypt, edit, and re-encrypt a support package.</span></span>

        PS C:\WINDOWS\system32> Import-module C:\Users\Default\StorSimple\SupportPackage\HCSSupportPackageTools.psm1

        PS C:\WINDOWS\system32> Open-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Open-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32> Close-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Close-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32>

## <a name="next-steps"></a><span data-ttu-id="38644-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="38644-182">Next steps</span></span>

* <span data-ttu-id="38644-183">深入了解 hello [hello 支援封裝中收集的資訊](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)</span><span class="sxs-lookup"><span data-stu-id="38644-183">Learn about hello [information collected in hello Support package](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)</span></span>
* <span data-ttu-id="38644-184">了解如何太[使用支援封裝和裝置記錄 tootroubleshoot 裝置部署](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting)。</span><span class="sxs-lookup"><span data-stu-id="38644-184">Learn how too[use support packages and device logs tootroubleshoot your device deployment](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span></span>
* <span data-ttu-id="38644-185">了解如何太[使用 hello StorSimple 裝置管理員服務 tooadminister StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="38644-185">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

