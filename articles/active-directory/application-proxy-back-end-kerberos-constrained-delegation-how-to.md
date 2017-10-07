---
title: "aaaHow tooconfigure 應用程式 Proxy 應用程式 toouse Kerberos 限制委派 |Microsoft 文件"
description: "如何針對 Azure AD Application Proxy 應用程式的 tooconfigure Kerberos 限制委派。"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 93dac264ff1d3b99dead1d9c759c37c59373cbd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application-toouse-kerberos-constrained-delegation"></a>如何 tooconfigure 應用程式 Proxy 應用程式 toouse Kerberos 限制委派

hello 達成 SSO toopublished 應用程式可以稍微不同應用程式 tooapplication 和 Azure 應用程式 Proxy 提供現成 hello 右邊 hello 選項的其中一個可用的方法是 Kerberos 限制委派 (KCD)。 這是連接器主機是限制的設定的 tooperform kerberos 驗證 toobackend 應用程式，代表使用者的位置。

hello 啟用 KCD 的實際程序較為簡單，而且通常需要有基本認識的 hello 以內，各種元件和可加速 SSO 執行的驗證流程。 尋找良好來源的資訊 toohelp 疑難排解的案例 where KCD SSO 未如預期般函式，可以為疏鬆。

因此，這篇文章會嘗試 tooprovide 的參考，這樣應該有助於疑難排解和自我補救 hello 最常見的問題，我們會看到單一點。 在 hello 相同時間提供其他指導方針診斷 hello 越複雜，雖然實作。

請注意，這篇文章會使 hello 下列假設：

-   為每個已部署 azure 應用程式 Proxy 我們[文件](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable)與一般存取 toonon KCD 應用程式是否正常運作。

-   hello 已發行的目標應用程式為基礎的 kerberos IIS 和 Microsoft 的實作。

-   hello 伺服器和應用程式的主機位於單一 Active Directory 網域中。 如需有關跨網域和樹系案例的詳細資訊，請參閱 [KCD 白皮書 (英文)](http://aka.ms/KCDPaper)。

-   hello 主旨發行應用程式在 Azure 中使用預先驗證已啟用，租用戶和使用者應 tooauthenticate tooAzure 透過表單型驗證。 豐富型用戶端驗證案例未涵蓋的本文中，但加入 hello 未來某些時候。

## <a name="prerequisites"></a>必要條件

Azure 應用程式 Proxy 可以部署到幾乎任何類型的基礎結構，或環境和 hello 毫無疑問架構，從組織 tooorganization。 KCD hello 最常見原因之一相關的問題不是 hello 環境本身，但相當簡單的錯誤組態或一般監督。

基於這個理由，我們建議是一律 toostart 藉由確定您已符合所有 hello 先決條件配置在我們的主要[與 hello 應用程式 Proxy 發行項使用 KCD SSO](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd)之前開始疑難排解。

在設定 KCD 2012R2，因為這會採用舊版的 Windows，但同時會記住的數個其他考量，在本質上不同的方法 tooconfiguring KCD 的特別 hello 區段：

-   不是網域成員伺服器 tooopen 含有特定網域控制站的安全通道對話罕見狀況。 然後將 tooanother 對話方塊在任何時候，這樣連接器主機通常不應該限制的 toobeing 無法 toocommunicate 只在特定的本機站台的 dc。

-   類似上述點 toohello，跨網域案例依賴直接可能位於 hello 本機網路周邊外部連接器主機 tooDCs 的轉介。 在此案例中是同樣重要 toomake 確定您也允許將流量起 tooDCs 代表其他個別的網域，或是委派失敗。

-   您應該盡可能避免在連接器主機和 DC 之間放置任何作用中的 IPS/IDS 裝置，因為這些裝置有時候會侵入及干擾核心 RPC 流量

一樣，我們都希望 tooresolve 問題快速並有效地，它可能需要的時間，因此可能您應該再次嘗試並測試委派 hello 最簡單的案例中。 hello 您引入的多個變數，hello 多則可能需要與 toocontend。 例如，限制測試 tooa 單一連接器，可以節省寶貴的時間，而 hello 問題解決之後，就可以加入其他連接器。

某些環境因素，可能也造成 tooan 問題，所以再次如果可能再試一次，並盡可能縮短 hello 架構 tooa 最低限度的測試。 例如，內部防火牆的設定不正確的 Acl 並不常見，因此如果可能的話從連接器，可直接通過 toohello Dc 和後端應用程式的所有流量。 

實際上 hello 絕對最佳地方 tooposition 連接器是接近 tootheir 目標都可以。 在測試同時設置內嵌的防火牆，只會增加不必要的複雜性，而且可能會延長您的調查時間。

所以，KCD 問題到底是由什麼構成？ 也那里數個傳統的指示 KCD SSO 失敗，且 hello 第一個問題徵兆通常是資訊清單本身中的 hello 瀏覽器。

   ![不正確的 KCD 組態錯誤](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic1.png)

   ![授權失敗，因為 toomissing 權限](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic2.png)

所有都帶有 hello 相同徵狀失敗 tooperform SSO，因此拒絕哪些 hello 使用者存取 toohello 應用程式。

## <a name="troubleshooting"></a>疑難排解

然後解決方式取決於 hello 問題及觀察到的徵兆。 將任何之前進一步會建議 hello 下列連結，因為它們可能會不尚未已有的實用資訊：

-   [針對應用程式 Proxy 問題和錯誤訊息進行疑難排解](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot)

-   [Kerberos 錯誤與徵狀](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#kerberos-errors)

-   [在內部部署和雲端身分識別不相同時使用 SSO](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd#working-with-sso-when-on-premises-and-cloud-identities-are-not-identical)

如果您已有此到目前為止，然後 hello 主要問題確實存在。 您需要 toodig 更深入，因此啟動分隔 hello 流入進行疑難排解的三個階段。

**用戶端預先驗證**-驗證透過瀏覽器 tooAzure hello 外部使用者。

要能 toopre-驗證 KCD SSO toofunction tooAzure 務必。 如果有發生任何問題，便應該先測試並解決這項問題。 請注意，hello 預先驗證階段的任何關聯 tooKCD 或 hello 發行應用程式。 它應該是相當簡單 toocorrect 任何不一致的例行性檢查 hello 主體帳戶存在於 Azure，而不是已停用/遭到封鎖。 hello hello 瀏覽器中的錯誤回應是描述性通常足以 toounderstand hello 原因。 如果您不確定，您也可以查看我們其他疑難排解文件 tooverify。

**委派服務**-hello 代表使用者取得 kerberos 服務票證 KDC （Kerberos 配送中心），從 Azure Proxy 連接器。

hello hello 用戶端與 hello Azure 前端之間的外部通訊上至少應有並無任何影響 KCD 恕不另行通知，而不是確保正常運作。 這是使 hello Azure Proxy 服務能夠提供有效的使用者識別碼，會使用的 tooobtain kerberos 票證。 如果不這麼做，就無法使用 KCD 並且會失敗。

如先前所述，hello 瀏覽器的錯誤訊息通常會提供一些很好的線索上作業失敗的原因。 請確定 toonote 下 hello 活動識別碼和時間戳記 hello 回應，因為這可讓您 toocorrelate hello 行為 tooactual 事件 hello Azure Proxy 事件記錄檔中。

   ![不正確的 KCD 組態錯誤](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic3.png)

和 hello 看到的 hello 事件記錄檔會被視為 13019 或 12027 事件對應項目。 您可以找到 hello 連接器中的事件記錄檔**Applications and Services Logs** &gt; **Microsoft** &gt; **AadApplicationProxy** &gt;**連接器**&gt;**Admin**。

   ![應用程式 Proxy 事件記錄檔中的事件 13019](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic4.png)

   ![應用程式 Proxy 事件記錄檔中的事件 12027](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic5.png)

-   在您的內部 DNS 使用 A 記錄 hello 應用程式的位址，以及不 CName

-   重新確認 hello 連接器裝載授與 hello 目標帳戶的 SPN，及所指定的權限 toodelegate toohello**使用任何驗證通訊協定**已選取。 這部分涵蓋於我們主要的 [SSO 組態文章](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd)

-   請確認有 hello SPN 是否存在，在 AD 中的單一執行個體發出**setspn-x**從任何網域的成員主機的 cmd 命令提示字元

-   檢查 toosee 如果網域原則強制執行 toolimit hello[發出的 kerberos 權杖的大小上限](https://blogs.technet.microsoft.com/askds/2012/09/12/maxtokensize-and-windows-8-and-windows-server-2012/)，如這個防止 hello 連接器從取得權杖，如果找到 toobe 過多

網路追蹤擷取 hello hello 連接器主機與 KDC 的網域之間的交換將 hello 下一個最佳的步驟中取得更低層級詳細資料在 hello 問題。 您可以在[深入探討疑難排解文件 (英文)](https://aka.ms/proxytshootpaper) 中找到此資訊。

如果票證看來正常，您應該會看到指出該驗證失敗，因為傳回 401 toohello 應用程式的 hello 記錄檔中的事件。 這通常表示拒絕您的票證該 hello 目標應用程式，因此進行 hello 遵循下一個階段。

**目標應用程式**-hello hello 連接器所提供的 kerberos 票證的 hello 取用者

在此階段 hello 連接器會預期的 toohave kerberos 服務票證 toohello 後端，以傳送 hello 第一個應用程式要求中的標頭。

-   使用 hello 應用程式驗證 hello 應用程式是可從 hello hello 連接器主機上的瀏覽器直接存取內部定義在 hello 入口網站的 URL。 然後您就可以成功登入。 Hello 連接器疑難排解頁面上，就可以找到有關執行此操作的詳細資料。

-   仍在 hello 連接器主機上，確認該 hello 之間驗證 hello 瀏覽器和 hello 應用程式使用 kerberos，hello 下列其中一項動作：

1.  執行開發人員工具 (**F12**) 在 Internet Explorer 中或使用[Fiddler](https://blogs.msdn.microsoft.com/crminthefield/2012/10/10/using-fiddler-to-check-for-kerberos-auth/)從 hello 連接器主機。 移 toohello 應用程式使用 hello 內部 URL，並檢查提供 WWW 授權標頭傳回 hello 回應 hello 應用程式中的 hello、 tooensure 交涉或 kerberos 存在於。 後續 kerberos blob 傳回 hello 回應 hello 瀏覽器 toohello 從應用程式通常會以開頭**YII**，因此這是正在播放的 kerberos 有助於。 NTLM 上 hello 另一方面一律以啟動**TlRMTVNTUAAB**，讀取 NTLMSSP 時從 Base64 解碼。 如果您看到**TlRMTVNTUAAB**在 hello blob hello 開頭，這表示 Kerberos 是**不**可用。 如果您沒有看到它，則應該可以使用 Kerberos。

  * 請注意，如果使用 Fiddler，這個方法可能必須暫時停用在 IIS 中的 hello 應用程式組態上的擴充的保護。

     ![瀏覽器網路檢查視窗](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic6.png)

    *圖：*由於這個開頭不是 TIRMTVNTUAAB，所以 Kerberos 在此範例中可以使用。 這是 Kerberos Blob 開頭不是 YII 的範例。

2.  暫時移除 hello 的提供者清單上 IIS 站台及存取應用程式直接從 IE 連接器主機上的 NTLM。 Ntlm 不會再在 hello 的提供者清單中，您應該只使用 Kerberos 無法 tooaccess hello 應用程式。 如果這個作業失敗，然後建議是 hello 應用程式的組態有問題，Kerberos 驗證無法正常運作。

如果 Kerberos 無法使用，核取 hello 應用程式的驗證設定，確定 IIS toomake 中的交涉會列出最上層，NTLM 下方直接使用。 (不是 Negotiate:kerberos 或 Negotiate:PKU2U)。 只有在 Kerberos 能正常運作的情況下才繼續。

   ![Windows 驗證提供者](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic7.png)
   
-   Kerberos 和 NTLM 備妥，可讓現在會暫時停用 hello hello 入口網站中的應用程式的預先驗證。 請參閱是否可以存取它 hello 從網際網路使用 hello 外部 URL。 您應該是提示的 tooauthenticate，並且應該能夠 toodo，因此 hello 與使用相同帳戶中使用的 hello 上一個步驟。 如果沒有的話，這表示根本問題 hello 後端應用程式及不 KCD。

-   現在重新啟用 hello 入口網站中的預先驗證，並嘗試 tooconnect toohello 應用程式，透過它的外部 URL，透過 Azure 進行驗證。 如果 SSO 失敗時，您應該看到 hello 瀏覽器中，加上事件 13022 hello 記錄檔中的 「 禁止 」 錯誤訊息：

    *Microsoft AAD 應用程式 Proxy 連接器無法驗證 hello 使用者，因為 hello 後端伺服器會回應與 HTTP 401 錯誤 tooKerberos 驗證嘗試。*

    ![HTTP 401 禁止錯誤](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic8.png)

-   請檢查 hello IIS 應用程式 tooensure hello 設定應用程式集區已設定的 toouse hello 相同 hello SPN 的帳戶已針對在 AD 中，如下所示，在 IIS 中瀏覽

    ![IIS 應用程式組態視窗](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic9.png)

    一旦您知道 hello 身分識別時，發出下列確定明確設定此帳戶以 hello SPN 有問題的 cmd 提示 toomake hello。 例如，**setspn – q http/spn.wacketywack.com**

    ![SetSPN 命令視窗](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic10.png)

-   請檢查該 hello hello 入口網站中的 hello 應用程式設定中定義的 SPN 是 hello 相同設定針對 hello 應用程式的應用程式集區的使用中的 hello 目標 AD 帳戶的 SPN

   ![Azure 入口網站中的 SPN 組態](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic11.png)
   
-   切換至 IIS 和選取 hello**組態編輯器**選項 hello 應用程式，並瀏覽過**system.webServer/security/authentication/windowsAuthentication** toomake 確定該**UseAppPoolCredentials**設定 tootrue

   ![IIS 設定應用程式集區認證選項](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic12.png)

同時會用於改善 hello 的 Kerberos 作業的效能，離開啟用核心模式也會導致 hello hello 票證要求服務 toobe 解密使用電腦帳戶。 這也稱為 hello 本機系統，因此需要這組 tootrue 中斷 KCD hello 應用程式裝載在伺服器陣列中的多部伺服器時。

-   額外的檢查，您可能也想 toodisable hello**擴充**保護太。 已有這已經在此證明 toobreak KCD 非常特定的組態中啟用時的情況下遇到應用程式發行為 hello 預設的網站的子資料夾的位置。 此本身設定為匿名驗證，離開 hello 整個對話灰色建議子物件就不會繼承目前使用的設定。 但其中一律建議需要啟用，這可能因此由所有是測試，但不要忘記此 tooenabled toorestore。

這些額外的檢查應該出您追蹤 toostart 使用已發行應用程式上。 您可以繼續，還有其他連接器向上微調設定 toodelegate，但如果沒有其他進一步的事情就會接著會建議我們更深入技術的逐步解說的讀取[hello 疑難排解 Azure AD 應用程式的完整指南Proxy](https://aka.ms/proxytshootpaper)

如果您仍然無法 tooprogress 您的問題，支援會超過高興 tooassist，且繼續從這裡。 建立支援票證，直接在 hello 入口網站中的，我們的工程師會聯繫 tooyou。

## <a name="other-scenarios"></a>其他案例

-   Azure 應用程式 Proxy 將要求傳送其要求 tooan 應用程式之前，先 Kerberos 票證。 某些第 3 個合作對象應用程式，例如 Tableau Server 不喜歡的驗證，這個方法並而不是預期的 hello 傳統交涉 tootake 地點。 hello 第一個要求是匿名的允許 hello 應用程式 toorespond 與 hello 401 透過支援的驗證類型。

-   雙躍點驗證：常用於應用程式已分層並具有後端與前端，且兩者皆需要驗證的案例 (例如 SQL Reporting Services)。

## <a name="next-steps"></a>後續步驟
[在受管理的網域上設定 Kerberos 限制委派 (KCD)](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-enable-kcd)
