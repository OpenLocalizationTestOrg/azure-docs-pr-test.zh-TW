---
title: "aaaAzure AD 應用程式 Proxy-快速入門安裝連接器 |Microsoft 文件"
description: "Hello Azure 入口網站中開啟應用程式 Proxy，並安裝 hello hello 反向 proxy 連接器。"
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
ms.date: 08/02/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ea79ffa92fa223584be04f49019fd31a0bfd8358
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-proxy-and-install-hello-connector"></a>開始使用應用程式 Proxy 並安裝 hello 連接器
本文將告訴您透過 hello 步驟 tooenable Microsoft Azure AD 應用程式 Proxy 為您的雲端目錄，在 Azure AD 中。

如果您不知道 hello 安全性和產能優勢的應用程式 Proxy 將 tooyour 組織，請深入了解[如何 tooprovide 安全的遠端存取 tooon 內部部署應用程式](active-directory-application-proxy-get-started.md)。

## <a name="application-proxy-prerequisites"></a>應用程式 Proxy 先決條件
您可以啟用及使用應用程式 Proxy 服務之前，您會需要 toohave:

* Microsoft Azure AD [基本或進階訂用帳戶](active-directory-editions.md) 以及您是全域管理員的 Azure AD 目錄。
* 執行 Windows Server 2012 R2 或 2016，您可以安裝 hello 應用程式 Proxy 連接器的伺服器。 hello 伺服器需要 toobe 無法 tooconnect toohello hello 雲端中的應用程式 Proxy 服務而 hello 內部部署您發行的應用程式。
  * 針對單一登入 tooyour 已發行的應用程式使用 Kerberos 限制委派，這部電腦應該被網域的 hello 相同的 AD 網域中做為您要發行的 hello 應用程式。 如需詳細資訊，請參閱[使用應用程式 Proxy 進行單一登入的 KCD](active-directory-application-proxy-sso-using-kcd.md)。

如果您的組織使用 proxy 伺服器 tooconnect toohello 網際網路，讀取[使用現有的內部 proxy 伺服器](application-proxy-working-with-proxy-servers.md)如需詳細資訊如何 tooconfigure 它們才能取得啟動應用程式 proxy。

## <a name="open-your-ports"></a>開啟您的連接埠

tooprepare 環境針對 Azure AD Application Proxy，您必須先 tooenable 通訊 tooAzure 資料中心。 如果 hello 路徑中有防火牆，請確認它已開啟，因此該連接器可以進行 HTTPS (TCP) 的 hello 要求 toohello 應用程式 Proxy。

1. 開啟 hello siguientes puertos 太**輸出**流量：

   | 連接埠號碼 | 使用方式 |
   | --- | --- |
   | 80 | 下載憑證撤銷清單 (Crl) 時驗證 hello SSL 憑證 |
   | 443 | 所有的連出通訊以 hello 應用程式 Proxy 服務 |

   如果您的防火牆，強制執行根據 toooriginating 使用者流量，開啟這些連接埠的流量從做為網路服務執行的 Windows 服務。

   > [!IMPORTANT]
   > hello 反映出 hello 連接器版本 1.5.132.0 的連接埠需求及更新版本。 如果仍有舊版的連接器，您也需要 tooenable hello 9350，下列連接埠在加法 too80 和 443: 5671、 8080，9090 9091，則為 9352 10100 – 10120。
   >
   >如需更新連接器 toohello 的最新版本的相關資訊，請參閱[了解 Azure AD 應用程式 Proxy 連接器](application-proxy-understand-connectors.md#automatic-updates)。

2. 如果您的防火牆或 proxy 可讓 DNS 允許清單，您可以允許清單連接 toomsappproxy.net 和.servicebus.windows.net 的支援。 如果沒有，您需要 tooallow 存取 toohello [Azure 資料中心 IP 範圍](https://www.microsoft.com/download/details.aspx?id=41653)，這會更新每週。

3. Microsoft 會使用四個位址 tooverify 憑證。 允許存取 toohello 如果您尚未這樣做其他產品的下列 Url:
   * mscrl.microsoft.com:80
   * crl.microsoft.com:80
   * ocsp.msocsp.com:80
   * www.microsoft.com:80

4. 您的連接器需要存取 toologin.windows.net 和 login.microsoftonline.net 的 hello 註冊程序。

5. 使用 hello [Azure AD 應用程式 Proxy 連接器連接埠測試工具](https://aadap-portcheck.connectorporttest.msappproxy.net/)tooverify 連接器可達到 hello 應用程式 Proxy 服務。 最少，請確定 hello 美國中部地區和 hello 區域最接近 tooyou 具有所有綠色的核取記號。 除此之外，綠色勾選記號越多代表恢復能力越佳。

## <a name="install-and-register-a-connector"></a>安裝並註冊連接器
1. Hello 中的系統管理員身分登入[Azure 入口網站](https://portal.azure.com/)。
2. 您目前的目錄會出現在 hello 右上角的 在您的使用者名稱。 如果您需要 toochange 目錄，請選取該圖示。
3. 跳過**Azure Active Directory** > **應用程式 Proxy**。

   ![瀏覽 tooApplication Proxy](./media/active-directory-application-proxy-enable/app_proxy_navigate.png)

4. 選取 [下載連接器]。

   ![下載連接器](./media/active-directory-application-proxy-enable/download_connector.png)

5. 執行**AADApplicationProxyConnectorInstaller.exe** hello 伺服器上您備妥相應 toohello 必要條件。
6. 遵循 hello 精靈 tooinstall hello 指示進行。 在安裝期間，您必須提示的 tooregister hello hello 的 Azure AD 租用戶的應用程式 Proxy 連接器。

   * 提供您的 Azure AD 全域管理員認證。 您的全域管理員租用戶可能與您的 Microsoft Azure 認證不同。
   * 請確定暫存器 hello 連接器處於 hello 相同的目錄已啟用 hello 管理員 hello 應用程式 Proxy 服務。 例如，如果 hello 租用戶網域為 contoso.com，hello admin 應該是admin@contoso.com或在該網域上的任何其他別名。
   * 如果**IE 增強式安全性設定**設定得**上**hello 在伺服器上安裝 hello 連接器，您可能無法看見 hello 註冊 畫面中。 tooget 存取權，遵循 hello hello 錯誤訊息中的指示。 請確定已停用 [Internet Explorer 增強式安全性]。

為了實現高可用性，您應該至少部署兩個連接器。 每個連接器都必須分別進行註冊。

## <a name="test-that-hello-connector-installed-correctly"></a>測試已正確安裝該 hello 連接器

您可以確認新的連接器，檢查它在任一個 hello Azure 入口網站或伺服器上正確安裝。 

在 hello Azure 入口網站、 登入 tooyour 租用戶和瀏覽過**Azure Active Directory** > **應用程式 Proxy**。 所有的連接器與連接器群組都會出現在此頁面上。 選取連接器 toosee 其詳細資料，或將它移至不同的連接器群組。 

在您的伺服器，請檢查 hello 清單 hello 連接器與 hello 連接器更新程式的作用中服務。 hello 兩個服務應該立即，開始執行，但如果沒有，請加以啟動： 

   * **Microsoft AAD 應用程式 Proxy 連接器** 可啟用連線

   * **Microsoft AAD 應用程式 Proxy 連接器更新程式**是自動更新服務。 hello updater 會檢查新版本的 hello 連接器，並且更新 hello 連接器，視需要。

   ![應用程式 Proxy 連接器服務 - 螢幕擷取畫面](./media/active-directory-application-proxy-enable/app_proxy_services.png)

如需連接器和方式，就會維持 toodate 註冊資訊，請參閱[了解 Azure AD 應用程式 Proxy 連接器](application-proxy-understand-connectors.md)。


## <a name="next-steps"></a>後續步驟
現在您已經準備就緒太[發行應用程式 Proxy](application-proxy-publish-azure-portal.md)。

如果您有個別的網路或不同的位置上的應用程式，使用連接器，將邏輯單元分 tooorganize hello 不同連接器。 深入了解 [使用應用程式 Proxy 連接器](active-directory-application-proxy-connectors-azure-portal.md)。
