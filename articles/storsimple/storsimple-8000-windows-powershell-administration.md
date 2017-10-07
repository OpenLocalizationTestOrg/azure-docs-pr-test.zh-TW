---
title: "管理 StorSimple 裝置 aaaPowerShell |Microsoft 文件"
description: "深入了解如何 toouse Windows PowerShell for StorSimple toomanage StorSimple 裝置。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/03/2017
ms.author: alkohli@microsoft.com
ms.openlocfilehash: e9e4bd025933cdef68b861d93749a107d1689536
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-powershell-for-storsimple-tooadminister-your-device"></a>使用 Windows PowerShell for StorSimple tooadminister 您的裝置

## <a name="overview"></a>概觀

Windows PowerShell for StorSimple 提供命令列介面，您可以使用 toomanage Microsoft Azure StorSimple 裝置。 如 hello 名稱所示，它是 Windows PowerShell 為基礎的命令列介面，建置在受限 runspace。 Hello hello 使用者在 hello 命令列的觀點而言，受限的 runspace 就像是功能受限的 Windows PowerShell。 保留一些 hello 的 Windows PowerShell 的基本功能，這個介面具有專為管理您的 Microsoft Azure StorSimple 裝置的其他專用的 cmdlet。

這篇文章描述 hello Windows PowerShell for StorSimple 的功能，包括如何連接 toothis 介面，並包含連結 toostep 個步驟程序或工作流程，您可以使用此介面來執行。 hello 工作流程包括如何 tooregister 您的裝置，hello 網路介面在裝置上設定，安裝更新，需要在維護模式中的 hello 裝置 toobe，變更 hello 裝置狀態，以及您可能會遇到任何問題進行疑難排解。

閱讀本文之後，您將能夠：

* 使用 Windows PowerShell for StorSimple tooyour StorSimple 裝置連線。
* 使用 Windows PowerShell for StorSimple 管理 StorSimple 裝置。
* 在 Windows PowerShell for StorSimple 中取得說明。

> [!NOTE]
> * Windows PowerShell for StorSimple cmdlet 可讓您 toomanage StorSimple 裝置序列主控台或從遠端透過 Windows PowerShell 遠端功能。 如需每個可以使用這個介面中的 hello 個別 cmdlet 的詳細資訊，請移至太[適用於 Windows PowerShell for StorSimple cmdlet 參考](https://technet.microsoft.com/library/dn688168.aspx)。
> * hello Azure PowerShell StorSimple cmdlet 是 cmdlet 的不同可讓您 tooautomate StorSimple 服務層級和 hello 命令列移轉工作集合。 如 for StorSimple hello Azure PowerShell cmdlet 的相關資訊，請移至 toohello [Azure StorSimple cmdlet 參考](https://docs.microsoft.com/powershell/servicemanagement/azure.storsimple/v3.1.0/azure.storsimple)。


您可以存取 hello Windows PowerShell for StorSimple 使用其中一種 hello 下列方法：

* [TooStorSimple 裝置序列主控台連接](#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console)
* [從遠端連線 tooStorSimple 使用 Windows PowerShell](#connect-remotely-to-storsimple-using-windows-powershell-for-storsimple)

## <a name="connect-toowindows-powershell-for-storsimple-via-hello-device-serial-console"></a>TooWindows PowerShell for StorSimple 透過 hello 裝置序列主控台

您可以[下載 PuTTY](http://www.putty.org/)或類似的終端機模擬軟體 tooconnect tooWindows PowerShell for StorSimple。 您需要 tooconfigure PuTTY 特別 tooaccess hello Microsoft Azure StorSimple 裝置。 hello 下列主題包含有關的詳細的步驟 tooconfigure PuTTy 和連接 toohello 裝置。 同時也說明 hello 序列主控台中的各種功能表選項。

### <a name="putty-settings"></a>PuTTY 設定

請確定您使用 hello hello 序列主控台中的下列 PuTTY 設定 tooconnect toohello Windows PowerShell 介面。

#### <a name="tooconfigure-putty"></a>tooconfigure PuTTY

1. 在 hello PuTTY**重新設定**對話方塊中的，在 hello**類別**窗格中，選取**鍵盤**。
2. 請務必選取下列選項的 hello （當您啟動新的工作階段時，這些是 hello 預設設定）。
   
   | 鍵盤項目 | 選取 |
   | --- | --- |
   | 退格鍵 |Control-? (127) |
   | Home 和 End 按鍵 |標準 |
   | 功能鍵和數字鍵台 |ESC[n~ |
   | 方向鍵的初始狀態 |正常 |
   | 數字鍵台的初始狀態 |正常 |
   | 啟用額外的鍵盤功能 |Control-Alt 和 AltGr 不同 |
   
    ![支援的 PuTTY 設定](./media/storsimple-windows-powershell-administration/IC740877.png)
3. 按一下 [Apply (套用)] 。
4. 在 hello**類別**窗格中，選取**轉譯**。
5. 在 hello**遠端字元集**清單方塊中，選取**utf-8**。
6. 在 [線條繪圖字元的處理] 下，選取 [使用 Unicode 線條繪圖字碼指標]。 hello 下列螢幕擷取畫面顯示 hello 正確的 PuTTY 選取項目。
   
    ![UTF PuTTY 設定](./media/storsimple-windows-powershell-administration/IC740878.png)
7. 按一下 [Apply (套用)] 。

您現在可以使用 PuTTY tooconnect toohello 裝置序列主控台執行下列步驟的 hello。

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="about-hello-serial-console"></a>關於 hello 序列主控台

當您存取您的 StorSimple 裝置 hello Windows PowerShell 介面透過 hello 序列主控台時，橫幅訊息，依序出現的功能表選項。

hello 橫幅訊息包含基本 StorSimple 裝置資訊，例如 hello 模型、 名稱、 已安裝的軟體版本，以及您要存取的 hello 控制站的狀態。 hello 下列影像顯示橫幅訊息範例。

![序列橫幅訊息](./media/storsimple-windows-powershell-administration/IC741098.png)

> [!IMPORTANT]
> 無論您是 hello 控制站，您可以使用 hello 橫幅訊息 tooidentify 連接 toois _Active_或_被動_。

下列影像顯示 hello hello 各種 hello 序列主控台功能表中的可用 runspace 選項。

![註冊裝置 2](./media/storsimple-windows-powershell-administration/IC740906.png)

您可以選擇從 hello 下列設定：

1. **登入的完整存取**此選項可讓您 （具有適當的認證） hello tooconnect toohello **SSAdminConsole** hello 本機控制器的 runspace。 （hello 本機控制器是透過您的 StorSimple 裝置 hello 序列主控台目前正在存取您的 hello 控制站）。也可以使用此選項 tooallow Microsoft 支援服務 tooaccess 不受限制的 runspace （支援工作階段） tootroubleshoot 任何可能的裝置問題。 您使用選項 1 toolog 上之後，您可以允許 hello Microsoft 支援工程師 tooaccess 不受限制的 runspace 執行特定的 cmdlet。 如需詳細資訊，請參閱太[啟動支援工作階段](storsimple-8000-contact-microsoft-support.md#start-a-support-session-in-windows-powershell-for-storsimple)。
   
2. **登入具有完整存取權的 toopeer 控制器**時，此選項與選項 1，hello 相同之處在於您可以連接 （使用適當的認證） hello toohello **SSAdminConsole** hello 同儕節點控制器上的 runspace。 Hello StorSimple 裝置是具有主動-被動組態中的兩個控制器的高可用性裝置，因為對等是指 toohello 另一個控制器 hello 透過 hello 序列主控台存取您的裝置）。
   類似 toooption 1，此選項也可以使用的 tooallow Microsoft 支援服務 tooaccess 不受限制的 runspace 同儕節點控制器上。

3. **限制存取連接**這個選項為 limited 模式下使用的 tooaccess Windows PowerShell 介面。 系統不會提示您輸入存取認證。 此選項會連接 tooa 更多受限制 runspace 比較 toooptions 1 和 2。  一些 hello 工作可透過選項 1，**無法*在此 runspace 中執行會：
   
   * 重設 toohello 原廠設定
   * 變更 hello 密碼
   * 啟用或停用支援存取
   * 套用更新
   * 安裝 Hotfix

    > [!NOTE]
    > 如果您忘記 hello 裝置系統管理員密碼而無法透過選項 1 或 2 連線，這是慣用的 hello 選項。

4. **變更語言**此選項可讓您 toochange hello 顯示語言 hello Windows PowerShell 介面上的。 支援的 hello 語言是英文、 日文、 俄文、 法文、 韓文、 西班牙文、 義大利文、 德文、 中文和巴西葡萄牙文。

## <a name="connect-remotely-toostorsimple-using-windows-powershell-for-storsimple"></a>從遠端連線使用 Windows PowerShell for StorSimple 的 tooStorSimple

您可以使用 Windows PowerShell 遠端執行功能 tooconnect tooyour StorSimple 裝置。 當您以這種方式連線時，將不會看到功能表。 （只有當您使用 hello 序列主控台上 hello 裝置 tooconnect，您看到功能表。 從遠端連線會讓您直接 toohello 相當於 hello 序列主控台上的"選項 1 – 完整存取權限 」。)使用 Windows PowerShell 遠端功能，您可以連接 tooa 特定 runspace。 您也可以指定 hello 顯示語言。

hello 顯示語言這 hello 與語言無關，您將使用 hello**變更語言**hello 序列主控台功能表中的選項。 遠端 PowerShell 將會自動挑選 hello 地區設定的裝置 hello 您連線時如果未指定。

> [!NOTE]
> 如果您正在使用 Microsoft Azure 虛擬主機與 StorSimple 雲端應用程式，您可以使用 Windows PowerShell 遠端處理和 hello 虛擬主機 tooconnect toohello 雲端應用裝置。 如果您已設定的共用位置 hello 主機 toosave 資訊從 hello Windows PowerShell 工作階段，您應該注意該 hello _Everyone_主體僅包含已驗證使用者。 因此，如果您已設定 hello tooallow 存取共用所_Everyone_和您連接卻未指定認證，將使用 hello 未經驗證的匿名主體，而且您會看到錯誤。 toofix 這個問題，請在 hello 共用主機，您必須啟用 hello Guest 帳戶，然後將 hello 來賓帳戶的完整存取 toohello 共用或您必須指定有效的認證，以及 hello Windows PowerShell cmdlet。


您可以使用 HTTP 或 HTTPS tooconnect 透過 Windows PowerShell 遠端功能。 使用下列教學課程的 hello hello 指示：

* [使用 HTTP 遠端連線](storsimple-remote-connect.md#connect-through-http)
* [使用 HTTPS 遠端連線](storsimple-remote-connect.md#connect-through-https)

## <a name="connection-security-considerations"></a>連線安全性考量

當您在決定如何 tooconnect tooWindows PowerShell for StorSimple，請考量下列 hello:

* 直接連接 toohello 裝置序列主控台安全，但不是透過網路交換器連接 toohello 序列主控台。 請小心 hello 安全性風險的網路交換器透過連線 toodevice 序列時。
* 透過 HTTP 工作階段連線，可能會提供更高的安全性比透過網路連接透過 hello 序列主控台。 雖然這不是 hello 最安全的方法，它是受信任的網路接受。
* 透過 HTTPS 工作階段連接是最安全的 hello 與 hello 建議的選項。

## <a name="administer-your-storsimple-device-using-windows-powershell-for-storsimple"></a>使用 Windows PowerShell for StorSimple 管理 StorSimple 裝置

hello 下表顯示所有 hello 常見管理工作和複雜工作流程的可執行的摘要 hello 您的 StorSimple 裝置的 Windows PowerShell 介面中。 如需有關每個工作流程的詳細資訊，請按一下 hello hello 資料表中的適當項目。

#### <a name="windows-powershell-for-storsimple-workflows"></a>Windows PowerShell for StorSimple 的工作流程

| 如果您希望 toodo 如此... | 使用此程序。 |
| --- | --- |
| 登記裝置 |[設定和註冊使用 Windows PowerShell for StorSimple 的 hello 裝置](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |
| 設定 Web Proxy</br>檢視 Web Proxy 設定 |[為 StorSimple 裝置設定 Web Proxy](storsimple-8000-configure-web-proxy.md) |
| 修改裝置上的 DATA 0 網路介面設定 |[修改 StorSimple 裝置上的 DATA 0 網路介面](storsimple-8000-modify-data-0.md) |
| 停止控制器  </br> 重新啟動或關閉控制器 </br> 關閉裝置</br>重設 hello 裝置 toofactory 預設值 |[管理裝置控制器](storsimple-8000-manage-device-controller.md) |
| 安裝維護模式更新和 Hotfixe |[更新您的裝置](storsimple-update-device.md) |
| 進入維護模式  </br>結束維護模式 |[StorSimple 裝置模式](storsimple-8000-device-modes.md) |
| 建立支援封裝 </br>解密並編輯支援封裝 |[建立及管理支援封裝](storsimple-8000-create-manage-support-package.md) |
| 啟動支援工作階段</br> |[在 Windows PowerShell for StorSimple 中啟動支援工作階段](storsimple-8000-create-manage-support-package.md#create-a-support-package) |

## <a name="get-help-in-windows-powershell-for-storsimple"></a>在 Windows PowerShell for StorSimple 中取得說明

在 Windows PowerShell for StorSimple 中也有 Cmdlet 的說明。 此說明的線上、 最新版本也會提供，您可以使用 tooupdate hello 說明您的系統上。

這個介面中取得說明是類似 toothat Windows PowerShell 中的，大部分的 hello 與說明相關 cmdlet 運作。 您可以在 hello TechNet 文件庫中找到 Windows PowerShell 說明線上：[使用 Windows PowerShell 撰寫指令碼](http://go.microsoft.com/fwlink/?LinkID=108518)。

hello 以下是說明此 Windows PowerShell 介面，包括如何 tooupdate hello 說明 hello 類型的簡短描述。

### <a name="tooget-help-for-a-cmdlet"></a>tooget cmdlet 的說明

* 任何 cmdlet 或函式，下列命令使用 hello tooget 說明：`Get-Help <cmdlet-name>`
* tooget 任何 cmdlet 的線上說明使用 hello 前一個 cmdlet 以 hello`-Online`參數：`Get-Help <cmdlet-name> -Online`
* 如需完整說明，您可以使用 hello`–Full`參數，如需範例，請使用 hello`–Examples`參數。

### <a name="tooupdate-help"></a>tooupdate 說明

您可以輕鬆地更新 hello hello Windows PowerShell 介面中的說明。 執行下列步驟 tooupdate hello 說明您的系統上的 hello。

#### <a name="tooupdate-cmdlet-help"></a>tooupdate cmdlet 說明
1. 啟動 Windows PowerShell 以 hello**系統管理員身分執行**選項。
2. 在 hello 命令提示字元中輸入：`Update-Help`
3. hello 更新檔案將安裝的說明。
4. 安裝的 hello 說明檔案之後，請輸入： `Get-Help Get-Command`。 將會顯示可用說明的 Cmdlet 清單。

> [!NOTE]
> tooget 一份所有 hello 中可用的 cmdlet runspace 中，登入 toohello 對應的功能表選項，然後執行 hello `Get-Command` cmdlet。


## <a name="next-steps"></a>後續步驟

如果遇到任何問題與您的 StorSimple 裝置時執行一個以上的工作流程的 hello，請參閱太[工具，以疑難排解 StorSimple 部署](storsimple-troubleshoot-deployment.md#tools-for-troubleshooting-storsimple-deployments)。

