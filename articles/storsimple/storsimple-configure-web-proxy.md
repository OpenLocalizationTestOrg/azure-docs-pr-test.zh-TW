---
title: "StorSimple 裝置的 web proxy aaaSet |Microsoft 文件"
description: "深入了解如何 toouse Windows PowerShell for StorSimple tooconfigure web proxy 設定您的 StorSimple 裝置。"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 6c2ca351-a7c6-4da6-ab5e-c081e6d08261
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: c0213eb2a1902ff994147bb16593f0ff300eb70c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-proxy-for-your-storsimple-device"></a>為 StorSimple 裝置設定 Web Proxy
## <a name="overview"></a>概觀
這個教學課程描述如何 toouse Windows PowerShell for StorSimple tooconfigure，以及檢視 web proxy 設定您的 StorSimple 裝置。 與 hello 雲端通訊時，會使用所 hello StorSimple 裝置 hello web proxy 設定。 Web proxy 伺服器是使用的 tooadd 另一層安全性，篩選內容、 快取 tooease 頻寬需求或甚至協助進行分析。

Web Proxy 是 StorSimple 裝置的選用設定。 您只能透過 Windows PowerShell for StorSimple 來設定 Web Proxy。 hello 設定兩步驟程序如下所示：

1. 您先設定 web proxy 設定，透過 hello 安裝精靈或 Windows PowerShell for StorSimple cmdlet。
2. 接著，您會啟用 hello 設定 web proxy 設定透過 Windows PowerShell for StorSimple cmdlet。

Hello web proxy 組態完成之後，您可以檢視在 hello Microsoft Azure StorSimple Manager 服務和 hello Windows PowerShell 中的 hello 設定 web proxy 設定 for StorSimple。 

閱讀本教學課程之後，您將能夠：

* 使用安裝精靈和 Cmdlet 來設定 Web Proxy
* 使用 Cmdlet 來啟用 Web Proxy
* 在 hello Azure 傳統入口網站中檢視 web proxy 設定
* 對 Web Proxy 設定期間的錯誤進行疑難排解

## <a name="configure-web-proxy-via-windows-powershell-for-storsimple"></a>透過 Windows PowerShell for StorSimple 來設定 Web Proxy
您可以使用其中一個 hello 遵循 tooconfigure web proxy 設定：

* 安裝程式精靈 tooguide 您完成 hello 組態步驟。
* Windows PowerShell for StorSimple 中的 Cmdlet。

每一種方法在 hello 下列各節討論。

## <a name="configure-web-proxy-via-hello-setup-wizard"></a>透過 hello 安裝精靈設定 web proxy
您可以使用您透過 hello 步驟 hello 安裝程式精靈 tooguide 進行 web proxy 組態。 執行下列步驟 tooconfigure web proxy，您的裝置上的 hello。

#### <a name="tooconfigure-web-proxy-via-hello-setup-wizard"></a>透過 hello 安裝精靈的 tooconfigure web proxy
1. 在 hello 序列主控台功能表中，選擇選項 1，**登入的完整存取**並提供 hello**裝置系統管理員密碼**。 輸入 hello 下列命令安裝精靈的工作階段的 toostart:
   
    `Invoke-HcsSetupWizard`
2. 如果這是 hello 您已註冊的裝置使用 hello 安裝精靈的第一次，您將需要 tooconfigure hello 所需的所有網路設定直到您到達 hello web proxy 組態。 如果您的裝置已經註冊，您可以接受所有 hello 設定網路設定，直到您到達 hello web proxy 設定。 在 hello 安裝精靈 提示的 tooconfigure web proxy 設定，當輸入**是**。
3. Hello **Web Proxy URL**、 指定 hello IP 位址或 hello 您 web proxy 伺服器與 hello TCP 通訊埠編號，您想裝置 toouse 與 hello 雲端通訊時的完整的網域名稱 (FQDN)。 使用下列格式的 hello:
   
    `http://<IP address or FQDN of hello web proxy server>:<TCP port number>`
   
    預設會指定 TCP 連接埠號碼 8080。
4. Hello 驗證類型選擇為**NTLM**，**基本**，或**無**。 基本是 hello hello proxy 伺服器設定最不安全的驗證。 NT LAN Manager (NTLM) 是一種高度安全且複雜的驗證通訊協定使用三向傳訊系統 （有時四是否需要額外完整性） tooauthenticate 使用者。 hello 預設驗證為 NTLM。 如需詳細資訊，請參閱[基本](http://hc.apache.org/httpclient-3.x/authentication.html)和 [NTLM 驗證](http://hc.apache.org/httpclient-3.x/authentication.html)。 
   
   > [!IMPORTANT]
   > **在 hello StorSimple Manager 服務，hello 裝置監控圖表不會運作時基本或 NTLM 驗證已啟用 hello 裝置 hello proxy 伺服器組態中。監控圖表 toowork hello，您將需要 tooensure tooNONE 驗證設定。**
   > 
   > 
5. 如果您使用驗證，請提供 [Web Proxy 使用者名稱] 和 [Web Proxy 密碼]。 您也需要 tooconfirm hello 密碼。
   
    ![在 StorSimple 裝置 1 設定 Web Proxy](./media/storsimple-configure-web-proxy/IC751830.png)

如果您要註冊您的裝置 hello 第一次，繼續進行 hello 註冊。 如果您的裝置已經註冊，就會結束 hello 精靈。 將儲存設定的 hello 設定。

現在也會啟用 Web Proxy。 您可以略過 hello[啟用 web proxy](#enable-web-proxy)步驟，並直接移過[hello Azure 傳統入口網站中檢視 web proxy 設定](#view-web-proxy-settings-in-the-azure-classic-portal)。

## <a name="configure-web-proxy-via-windows-powershell-for-storsimple-cmdlets"></a>透過 Windows PowerShell for StorSimple Cmdlet 來設定 Web Proxy
替代方式 tooconfigure web proxy 設定是透過 hello Windows PowerShell for StorSimple cmdlet。 執行下列步驟 tooconfigure web proxy 的 hello。

#### <a name="tooconfigure-web-proxy-via-cmdlets"></a>透過 cmdlet tooconfigure web proxy
1. 在 hello 序列主控台功能表中，選擇選項 1，**登入的完整存取**。 出現提示時，提供 hello**裝置系統管理員密碼**。 hello 預設密碼為`Password1`。
2. 在 hello 命令提示字元中輸入：
   
    `Set-HcsWebProxy -Authentication NTLM -ConnectionURI "<http://<IP address or FQDN of web proxy server>:<TCP port number>" -Username "<Username for web proxy server>"`
   
    提供並確認 hello 密碼出現提示時，如下所示。
   
    ![在 StorSimple 裝置 3 設定 Web Proxy](./media/storsimple-configure-web-proxy/IC751831.png)

hello web proxy 現在已設定，並需要 toobe 啟用。

## <a name="enable-web-proxy"></a>啟用 Web Proxy
預設會停用 Web Proxy。 StorSimple 裝置上設定 hello web proxy 設定之後，您需要 toouse hello Windows PowerShell for StorSimple tooenable hello web proxy 設定。

> [!NOTE]
> **如果您使用 hello 安裝程式精靈 tooconfigure web proxy，將不需要此步驟。依預設，安裝精靈工作階段之後會自動啟用 Web Proxy。**
> 
> 

執行下列步驟在 Windows PowerShell 中的適用於 StorSimple tooenable web proxy 在裝置上的 hello:

#### <a name="tooenable-web-proxy"></a>tooenable web proxy
1. 在 hello 序列主控台功能表中，選擇選項 1，**登入的完整存取**。 出現提示時，提供 hello**裝置系統管理員密碼**。 hello 預設密碼為`Password1`。
2. 在 hello 命令提示字元中輸入：
   
    `Enable-HcsWebProxy`
   
    您現在已經在您的 StorSimple 裝置上啟用 hello web proxy 設定。
   
    ![在 StorSimple 裝置 4 設定 Web Proxy](./media/storsimple-configure-web-proxy/IC751832.png)

## <a name="view-web-proxy-settings-in-hello-azure-classic-portal"></a>在 hello Azure 傳統入口網站中檢視 web proxy 設定
hello web proxy 設定透過 hello Windows PowerShell 介面設定，而且不能在 hello 傳統入口網站中變更。 您不過，可以 hello 傳統入口網站中檢視這些設定的設定。 執行下列步驟 tooview web proxy 的 hello。

#### <a name="tooview-web-proxy-settings"></a>tooview web proxy 設定
1. 瀏覽過**StorSimple Manager 服務 > 裝置**。 選取並按一下裝置，然後移過**設定**。
2. 向下捲動 hello**設定**頁面太**Web proxy 設定**> 一節。 您可以在 StorSimple 裝置上檢視 hello 設定 web proxy 設定，如下所示。
   
    ![在管理入口網站中檢視 Web Proxy](./media/storsimple-configure-web-proxy/ViewWebProxyPortal_M.png)

## <a name="errors-during-web-proxy-configuration"></a>在 Web Proxy 設定期間發生錯誤
如果未正確設定 hello web proxy 設定，錯誤訊息將會顯示的 toohello 使用者在 Windows PowerShell for StorSimple 中。 hello 下表說明一些這些錯誤訊息、 可能原因和建議的動作。

| 序號 | HRESULT 錯誤碼 | 可能的根本原因 | 建議的動作 |
|:--- |:--- |:--- |:--- |
| 1. |0x80070001 |從 hello 被動控制站執行命令，而且不能 toocommunicate 與 hello 作用中控制器。 |Hello 作用中控制器上執行 hello 命令。 從被動控制站 hello toorun hello 命令，您將需要 toofix hello tooactive 被動控制站的連線。 如果此連接已中斷，您將需要 tooengage Microsoft 支援服務。 |
| 2. |0x800710dd-hello 作業識別碼無效 |StorSimple 虛擬裝置不支援 Proxy 設定。 |StorSimple 虛擬裝置不支援 Proxy 設定。 這些設定只能在 StorSimple 實體裝置上設定。 |
| 3. |0x80070057 - 無效的參數 |其中一個 hello 參數提供給 hello proxy 設定不正確。 |hello URI 未提供正確格式。 使用下列格式的 hello:`http://<IP address or FQDN of hello web proxy server>:<TCP port number>` |
| 4. |0x800706ba - RPC 伺服器無法使用 |hello 根本原因是 hello 下列其中一種：</br></br>叢集未啟動。</br></br>資料路徑服務不在執行中。</br></br>從被動控制站執行 hello 命令，並不能 toocommunicate 與 hello 作用中控制器。 |請進行 hello 叢集的 Microsoft 支援服務 tooensure 已啟動，而且資料路徑服務正在執行。</br></br>從 hello 作用中控制器執行 hello 命令。 如果您想從被動控制站 hello toorun hello 命令時，您將需要 tooensure hello 被動控制站可以與 hello active 控制器通訊。 如果此連接已中斷，您將需要 tooengage Microsoft 支援服務。 |
| 5. |0x800706be - RPC 呼叫失敗 |叢集已關閉。 |請連絡 Microsoft 支援服務 hello 叢集的 tooensure 已啟動。 |
| 6. |0x8007138f - 找不到叢集資源 |找不到平台服務叢集資源。 當 hello 安裝不正確，也可能會發生。 |您可能需要 tooperform 原廠重設您的裝置。 您可能需要 toocreate 平台資源。 請連絡 Microsoft 支援服務來請示後續步驟。 |
| 7. |0x8007138c - 叢集資源不在線上 |平台或資料路徑叢集資源不在線上。 |請連絡 Microsoft 支援服務 toohelp 確認 hello 和平台服務資源都已上線。 |

> [!NOTE]
> * hello 上述錯誤訊息清單未全部列出。 
> * Hello StorSimple Manager 服務在 Azure 傳統入口網站中，將不會顯示錯誤相關的 tooweb proxy 設定。 如果發生問題時透過 web proxy hello 組態完成後，hello 裝置狀態會變更太**離線**hello 傳統入口網站中。 |
> 
> 

## <a name="next-steps"></a>後續步驟
* 如果您在部署您的裝置，或設定 web proxy 設定時遇到任何問題，請參閱太[疑難排解您的 StorSimple 裝置部署](storsimple-troubleshoot-deployment.md)。
* toolearn toouse hello StorSimple Manager 服務如何太移[使用 hello StorSimple Manager 服務 tooadminister StorSimple 裝置](storsimple-manager-service-administration.md)。

