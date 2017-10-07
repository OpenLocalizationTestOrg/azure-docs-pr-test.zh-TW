---
title: "aaaEnable hello 傳統入口網站中的 Azure AD Application Proxy |Microsoft 文件"
description: "開啟應用程式 Proxy 在 hello Azure 傳統入口網站，並安裝 hello hello 反向 proxy 連接器。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: c7186f98-dd80-4910-92a4-a7b8ff6272b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/02/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 8be9416a61993e1b46a20152e172c5133e54c0a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-application-proxy-in-hello-classic-portal-and-download-connectors"></a>Hello 傳統入口網站中啟用應用程式 Proxy 並下載連接器
本文將告訴您透過 hello 步驟 tooenable Microsoft Azure AD 應用程式 Proxy 為您的雲端目錄，在 Azure AD 中。

如果您不熟悉哪些應用程式 Proxy 可協助您執行，深入了解[如何 tooprovide 安全的遠端存取 tooon 內部部署應用程式](active-directory-application-proxy-get-started.md)。

## <a name="application-proxy-prerequisites"></a>應用程式 Proxy 先決條件
您可以啟用及使用應用程式 Proxy 服務之前，您會需要 toohave:

* Microsoft Azure AD [基本或進階訂用帳戶](active-directory-editions.md) 以及您是全域管理員的 Azure AD 目錄。
* 執行 Windows Server 2012 R2 或 2016，您可以安裝 hello 應用程式 Proxy 連接器的伺服器。 hello 伺服器要求 toohello 應用程式 Proxy 會將服務傳送 hello 雲端中，需要 HTTP 或 HTTPS 連線 toohello 應用程式，您要發行。
  * 單一登入 tooyour 已發佈的應用程式，這部電腦應該是網域的 hello 相同的 AD 網域中做為您要發行的 hello 應用程式。 如需詳細資訊，請參閱[使用應用程式 Proxy 進行單一登入](active-directory-application-proxy-sso-using-kcd.md)
* 如果您的組織使用 proxy 伺服器 tooconnect toohello 網際網路，讀取[使用現有的內部 proxy 伺服器](application-proxy-working-with-proxy-servers.md)的詳細資料 tooconfigure 它們。

## <a name="open-your-ports"></a>開啟您的連接埠

tooprepare 環境針對 Azure AD Application Proxy，您必須先 tooenable 通訊 tooAzure 資料中心。 如果 hello 路徑中有防火牆，請確認它已開啟，因此該連接器可以進行 HTTPS (TCP) 的 hello 要求 toohello 應用程式 Proxy。

1. 開啟 hello siguientes puertos 太**輸出**流量：

   | 連接埠號碼 | 使用方式 |
   | --- | --- |
   | 80 | 下載憑證撤銷清單 (Crl) 時驗證 hello SSL 憑證 |
   | 443 | 所有的連出通訊以 hello 應用程式 Proxy 服務 |

   如果您的防火牆，強制執行根據 toooriginating 使用者流量，開啟 estos puertos para el 與執行以網路服務的 Windows 服務的流量。

   > [!IMPORTANT]
   > hello 反映出 hello 連接器版本 1.5.132.0 的連接埠需求及更新版本。 如果仍有舊版的連接器，您也需要下列連接埠 tooenable hello: 5671、 8080、 9090、 9091、 9350、 9352，和 10100 – 10120。
   >
   >如需更新連接器 toohello 的最新版本的相關資訊，請參閱[了解 Azure AD 應用程式 Proxy 連接器](application-proxy-understand-connectors.md#automatic-updates)。

2. 如果您的防火牆或 proxy 可讓 DNS 允許清單，您可以允許清單連接 toomsappproxy.net 和.servicebus.windows.net 的支援。 如果沒有，您需要 tooallow 存取 toohello [Azure 資料中心 IP 範圍](https://www.microsoft.com/download/details.aspx?id=41653)，這會更新每週。

3. 使用 hello [Azure AD 應用程式 Proxy 連接器連接埠測試工具](https://aadap-portcheck.connectorporttest.msappproxy.net/)tooverify 連接器可達到 hello 應用程式 Proxy 服務。 最少，請確定 hello 美國中部地區和 hello 區域最接近 tooyou 具有所有綠色的核取記號。 除此之外，綠色勾選記號越多代表恢復能力越佳。

## <a name="enable-application-proxy-in-azure-ad"></a>Azure AD 中啟用應用程式 Proxy
1. Hello 中的系統管理員身分登入[Azure 傳統入口網站](https://manage.windowsazure.com/)。
2. 請 tooActive 目錄並選取您想在其中 tooenable 應用程式 Proxy 的 hello 目錄。

    ![Active Directory - 圖示](./media/active-directory-application-proxy-enable/ad_icon.png)
3. 選取**設定**從 hello 目錄 頁面上，向下捲動太**應用程式 Proxy**。
4. 切換**此目錄啟用應用程式 Proxy 服務**太**啟用**。

    ![啟用應用程式 Proxy](./media/active-directory-application-proxy-enable/app_proxy_enable.png)
5. 選取 [立即下載] 。 hello **Azure 的 AD 應用程式 Proxy 連接器下載**隨即開啟。 閱讀並接受 hello 授權條款，然後按一下**下載**toosave hello Windows Installer 檔案 (.exe) hello 連接器。

## <a name="install-and-register-hello-connector"></a>安裝並註冊 hello 連接器
1. 執行**AADApplicationProxyConnectorInstaller.exe** hello 伺服器上您備妥相應 toohello 必要條件。
2. 遵循 hello 精靈 tooinstall hello 指示進行。
3. 在安裝期間，您必須提示的 tooregister hello hello 的 Azure AD 租用戶的應用程式 Proxy 連接器。

   * 提供您的 Azure AD 全域管理員認證。 您的全域管理員租用戶可能與您的 Microsoft Azure 認證不同。
   * 請確定暫存器 hello 連接器處於 hello 相同的目錄已啟用 hello 管理員 hello 應用程式 Proxy 服務。 例如，如果 hello 租用戶網域為 contoso.com，hello admin 應該是admin@contoso.com或在該網域上的任何其他別名。
   * 如果**IE 增強式安全性設定**設定得**上**hello 註冊畫面可能會封鎖 hello 伺服器上。 tooallow 存取權，遵循 hello hello 錯誤訊息中的指示。 請確定已停用 [Internet Explorer 增強式安全性]。
   * 如果連接器註冊不成功，請參閱 [針對應用程式 Proxy 進行疑難排解](active-directory-application-proxy-troubleshoot.md)。  
4. Hello 安裝完成時，兩個 se agregan dos nuevos tooyour 伺服器：

   * **Microsoft AAD 應用程式 Proxy 連接器** 可啟用連線

     * **Microsoft AAD 應用程式 Proxy 連接器更新程式**是自動更新服務。 定期檢查有新版本的 hello 連接器，並視需要更新 hello 連接器。

     ![應用程式 Proxy 連接器服務 - 螢幕擷取畫面](./media/active-directory-application-proxy-enable/app_proxy_services.png)
5. 按一下**完成**hello 安裝視窗中。

如需連接器的相關資訊，請參閱[了解 Azure AD 應用程式 Proxy 連接器](application-proxy-understand-connectors.md)。

為了實現高可用性，您應該至少部署兩個連接器。 toodeploy 多個連接器，重複步驟 2 和 3。 每個連接器都必須分別進行註冊。

如果您想 toouninstall hello 連接器，請解除安裝 hello 連接器服務和 hello Updater 服務。 重新啟動電腦 toofully 移除 hello 服務。

## <a name="next-steps"></a>後續步驟
現在您已經準備就緒太[發行應用程式 Proxy](active-directory-application-proxy-publish.md)。

如果您有個別的網路或不同的位置上的應用程式，您可以使用連接器群組 tooorganize hello 不同連接器成邏輯單元。 深入了解 [使用應用程式 Proxy 連接器](active-directory-application-proxy-connectors.md)。
