---
title: "aaaCreate StorSimple 支援封裝 |Microsoft 文件"
description: "了解如何 toocreate，解密，以及編輯您的 StorSimple 裝置的支援封裝。"
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
ms.openlocfilehash: 209aeee50e823fd2ca96ababd1d0cf3ea9cdad53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-storsimple-support-package"></a>建立及管理 StorSimple 支援封裝
## <a name="overview"></a>概觀
StorSimple 支援封裝是一種方便使用的機制，會收集任何 StorSimple 裝置的問題進行疑難排解的所有相關記錄 tooassist Microsoft 支援服務。 hello 收集記錄檔會加密和壓縮。

本教學課程包含逐步指示 toocreate 和管理 hello 支援封裝。

## <a name="create-and-upload-a-support-package-in-hello-azure-classic-portal"></a>建立及上傳支援套件 hello Azure 傳統入口網站中
您可以建立及上傳支援套件 toohello Microsoft 支援 」 網站，透過 hello**維護**hello Azure 傳統入口網站中的 hello 服務頁面。

> [!NOTE]
> hello 上傳需要的支援密碼金鑰。 支援工程師應提供此 tooyou 以電子郵件。
> 
> 

加密和壓縮的支援封裝 （.cab 檔案） 是建立及上傳 toohello 支援站台。 hello 支援工程師然後可以擷取此套件 hello 協助疑難排解 hello 問題的技術支援服務網站。

執行下列步驟在 hello 傳統入口網站 toocreate 支援封裝中的 hello。

#### <a name="toocreate-a-support-package-in-hello-azure-classic-portal"></a>toocreate hello Azure 傳統入口網站中的支援套件
1. 選取 [裝置] > [維護]。
2. 在 hello**支援封裝**區段中，選取**建立並上傳支援套件**。
3. 在 hello**建立並上傳支援套件**對話方塊方塊中，執行下列 hello:
   
    ![建立支援封裝](./media/storsimple-create-manage-support-package/IC740923.png)
   
   * 在 hello**支援密碼**文字方塊中，輸入 hello 密碼金鑰。 Microsoft 支援工程師應該將此密碼金鑰 tooyou 傳送電子郵件中。
   * 選取 hello 核取方塊 tooprovide 同意 tooautomatically 上載 hello 支援封裝 toohello Microsoft 支援服務網站。
   * 按一下 [hello] 核取圖示 ![核取圖示](./media/storsimple-create-manage-support-package/IC740895.png)。

## <a name="manually-create-a-support-package"></a>手動建立支援封裝
在某些情況下，您將需要 toomanually 建立 hello 支援封裝，透過 Windows PowerShell for StorSimple。 例如：

* 如果您需要 tooremove 機密資訊從您的記錄檔先前 toosharing 向 Microsoft 支援。
* 如果您無法上傳 hello 封裝，因為 tooconnectivity 問題。

您可以透過電子郵件與 Microsoft 支援服務共用手動產生的支援封裝。 執行下列步驟 toocreate 支援封裝中 Windows PowerShell for StorSimple 的 hello。

#### <a name="toocreate-a-support-package-in-windows-powershell-for-storsimple"></a>toocreate Windows PowerShell for StorSimple 中的支援套件
1. toostart hello 已使用 tooconnect tooyour StorSimple 裝置的遠端電腦上系統管理員身分的 Windows PowerShell 工作階段輸入 hello 下列命令：
   
    `Start PowerShell`
2. Hello Windows PowerShell 工作階段中，連接 toohello SSAdmin 主控台，您的裝置：
   
   * 在 hello 命令提示字元中輸入：
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   * 在 hello 開啟對話方塊，輸入您的裝置系統管理員密碼。 hello 預設密碼為：
     
      `Password1`
     
      ![[PowerShell 認證] 對話方塊](./media/storsimple-create-manage-support-package/IC740962.png)
   * 選取 [確定] 。
   * 在 hello 命令提示字元中輸入：
     
      `Enter-PSSession $MS`
3. 在開啟的 hello 工作階段，輸入 hello 適當的命令。
   
   * 對於受密碼保護的網路共用，請輸入：
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       （因為加密 hello 支援封裝），將會提示您輸入密碼、 路徑 toohello 網路共用的資料夾，以及加密複雜密碼。 Hello 指定資料夾中，然後會建立支援封裝。
   * 對於不受密碼保護的共用，您不需要 hello`-Credential`參數。 輸入 hello 下列：
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       hello 支援封裝會建立兩個控制器 hello 指定的網路共用資料夾中。 這是可以用於疑難排解傳送 tooMicrosoft 支援加密、 壓縮檔案。 如需詳細資訊，請參閱 [連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)。

### <a name="hello-export-hcssupportpackage-cmdlet-parameters"></a>hello Export-hcssupportpackage cmdlet 參數
您可以使用下列參數使用 hello Export-hcssupportpackage cmdlet 的 hello。

| 參數 | 必要/選用 | 說明 |
| --- | --- | --- |
| `-Path` |必要 |使用 tooprovide hello hello 網路共用資料夾中的 hello 放置支援封裝位置。 |
| `-EncryptionPassphrase` |必要 |使用 tooprovide 複雜密碼 toohelp 加密 hello 支援封裝。 |
| `-Credential` |選用 |使用 hello 網路共用資料夾 toosupply 存取認證。 |
| `-Force` |選用 |使用 tooskip hello 加密複雜密碼確認步驟。 |
| `-PackageTag` |選用 |使用 toospecify 下的目錄*路徑*的 hello 支援放置封裝。 hello 預設值為 [裝置名稱]-[目前的日期和 time: yyyy-mm-dd-hh-mm-ss]。 |
| `-Scope` |選用 |指定為**叢集**（預設值） toocreate 兩個控制器的支援封裝。 如果您想要 toocreate 封裝只 hello 目前的控制器，指定**控制器**。 |

## <a name="edit-a-support-package"></a>編輯支援封裝
產生支援套件後，您可能需要 tooedit hello 封裝 tooremove 機密資訊。 這可以包括磁碟區名稱、 裝置 IP 位址，以及從 hello 記錄檔的備份名稱。

> [!IMPORTANT]
> 您只能編輯透過 Windows PowerShell for StorSimple 產生的支援封裝。 您無法編輯 hello 與 StorSimple Manager 服務的 Azure 傳統入口網站中建立的封裝。
> 
> 

tooedit 之前將其 hello Microsoft 支援服務網站上, 傳支援封裝會先解密 hello 支援封裝、 編輯 hello 檔案，然後重新加密。 執行下列步驟的 hello。

#### <a name="tooedit-a-support-package-in-windows-powershell-for-storsimple"></a>tooedit Windows PowerShell for StorSimple 中的支援套件
1. 產生支援封裝中稍早所述[toocreate 支援套件，Windows PowerShell for StorSimple 中](#to-create-a-support-package-in-windows-powershell-for-storsimple)。
2. [下載 hello 指令碼](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65)在您的用戶端的本機上。
3. 匯入 hello Windows PowerShell 模組。 指定 hello 路徑 toohello 本機資料夾下載 hello 指令碼。 tooimport hello 模組中，輸入：
   
    `Import-module <Path toohello folder that contains hello Windows PowerShell script>`
4. 所有的 hello 檔案都*.aes*經過壓縮並加密的檔案。 toodecompress 和解密檔案中，輸入：
   
    `Open-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    請注意 hello 的所有檔案現在會顯示 hello 實際的檔案副檔名。
   
    ![編輯支援封裝](./media/storsimple-create-manage-support-package/IC750706.png)
5. 當系統提示您輸入 hello 加密複雜密碼，請輸入 hello 建立 hello 支援封裝時所使用的複雜密碼。
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for hello following parameters:EncryptionPassphrase: ****
6. 瀏覽 toohello 包含 hello 記錄檔的資料夾。 Hello 記錄檔現在會解壓縮並解密，因為它們會有原始副檔名。 修改這些檔案 tooremove 任何客戶特定資訊，例如磁碟區名稱和裝置的 IP 位址，然後儲存 hello 檔案。
7. 關閉 hello 檔案 toocompress 以 gzip 它們，並以 aes-256 加密它們。 這適用於速度和透過網路傳送嗨支援封裝中的安全性。 toocompress 和加密的檔案中，輸入 hello 下列：
   
    `Close-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    ![編輯支援封裝](./media/storsimple-create-manage-support-package/IC750707.png)
8. 出現提示時，提供 hello 已修改之支援封裝加密複雜密碼。
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for hello following parameters:EncryptionPassphrase: ****
9. 記下 hello 新的複雜密碼，讓您與 Microsoft 支援服務要求時可以共用。

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a>範例：在受密碼保護的共用中編輯支援封裝中的檔案
hello 下列範例顯示如何 toodecrypt、 編輯和重新加密支援封裝。

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

## <a name="next-steps"></a>後續步驟
* 了解如何太[使用支援封裝和裝置記錄 tootroubleshoot 裝置部署](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting)。
* 了解如何太[使用 hello StorSimple Manager 服務 tooadminister StorSimple 裝置](storsimple-manager-service-administration.md)。

