---
title: "應用程式 Proxy aaaTroubleshoot |Microsoft 文件"
description: "涵蓋如何在 Azure AD Application Proxy tootroubleshoot 錯誤。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 970caafb-40b8-483c-bb46-c8b032a4fb74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: d426708a2ee32da6674987b5794602ed984b06b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-application-proxy-problems-and-error-messages"></a>針對應用程式 Proxy 問題和錯誤訊息進行疑難排解
如果在存取發行的應用程式，或在發行應用程式，就會發生錯誤，檢查下列選項 toosee，如果 Microsoft Azure AD 應用程式 Proxy 正常運作的 hello:

* 開啟 hello Windows 服務主控台並確認該 hello **Microsoft AAD 應用程式 Proxy 連接器**服務已啟用且正在執行。 您也可以在 hello 應用程式 Proxy 服務屬性頁面 toolook hello 下列影像所示：  
  ![[Microsoft AAD 應用程式 Proxy 連接器屬性] 視窗螢幕擷取畫面](./media/active-directory-application-proxy-troubleshoot/connectorproperties.png)
* 開啟 [事件檢視器]，然後在 [應用程式及服務記錄檔] > [Microsoft] > [AadApplicationProxy] > [Connector] > [Admin] 中尋找「應用程式 Proxy」連接器事件。
* 如有需要更詳細的記錄檔可用的[開啟 hello 應用程式 Proxy 連接器工作階段記錄](application-proxy-understand-connectors.md#under-the-hood)。

如需 hello Azure AD 疑難排解工具的詳細資訊，請參閱[疑難排解工具 toovalidate 連接器網路必要條件](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/03/troubleshooting-tool-to-validate-connector-networking-prerequisites)。

## <a name="hello-page-is-not-rendered-correctly"></a>無法正確呈現 hello 頁面
您可能會遇到應用程式轉譯有問題或運作不正確，但沒有收到特定錯誤訊息的情況。 如果您發行 hello 文件路徑，但卻 hello 應用程式需要存在於該路徑的外部的內容，也可能會發生。

比方說，如果您發行 hello 路徑 https://yourapp/app 但 hello 應用程式會呼叫 https://yourapp/media 映像，它們將不會呈現。 請確定您發行使用 hello 最高的層級路徑相關的所有內容都需要 tooinclude hello 應用程式。 在此範例中，它會是 http://yourapp/。

如果您變更您的路徑 tooinclude 參考內容，但仍然需要使用者 tooland hello 路徑中的更深層連結，請參閱 hello 部落格文章[hello Azure AD 存取面板和 Office 365 應用程式中的應用程式 Proxy 應用程式的設定 hello 右邊連結啟動器](https://blogs.technet.microsoft.com/applicationproxyblog/2016/04/06/setting-the-right-link-for-application-proxy-applications-in-the-azure-ad-access-panel-and-office-365-app-launcher/)。

## <a name="connector-errors"></a>連接器錯誤

使用 hello [Azure AD 應用程式 Proxy 連接器連接埠測試工具](https://aadap-portcheck.connectorporttest.msappproxy.net/)tooverify 連接器可達到 hello 應用程式 Proxy 服務。 最少，請確定 hello 美國中部地區和 hello 區域最接近 tooyou 具有所有綠色的核取記號。 除此之外，綠色勾選記號越多代表恢復能力越佳。 

如果登錄失敗 hello 連接器精靈安裝期間，有兩種方式 tooview hello hello 失敗原因。 請查看下 hello 事件記錄檔**應用程式和服務 Logs\Microsoft\AadApplicationProxy\Connector\Admin**，或執行的 hello 下列 Windows PowerShell 命令：

    Get-EventLog application –source “Microsoft AAD Application Proxy Connector” –EntryType “Error” –Newest 1

一旦您找到 hello Connector 錯誤 hello 事件記錄檔中的，使用此表格的常見錯誤 tooresolve hello 問題：

| 錯誤 | 建議的步驟 |
| ----- | ----------------- |
| 連接器註冊失敗： 請確定您啟用應用程式 Proxy hello Azure 管理入口網站中，而且您輸入您的 Active Directory 使用者名稱和密碼正確。 錯誤︰「發生一或多個錯誤。」 | 如果您關閉 hello 註冊視窗而不用登入 tooAzure AD，請再次執行 hello 連接器精靈，並註冊 hello 連接器。 <br><br> 如果 hello 註冊視窗隨即開啟，並立即關閉但不允許您 toolog 中的，您可能會收到這個錯誤。 您的系統有網路錯誤時，就會發生此錯誤。 請確定它是從瀏覽器 tooa 公用網站可能 tooconnect 和 hello 通訊埠已開啟中所指定[應用程式 Proxy 必要條件](active-directory-application-proxy-enable.md)。 |
| 清除錯誤 hello 註冊視窗中顯示。 無法繼續 | 如果您看到此錯誤，然後 hello 視窗關閉時，您可以輸入 hello 錯誤的使用者名稱或密碼。 請再試一次。 |
| 連接器註冊失敗： 請確定您啟用應用程式 Proxy hello Azure 管理入口網站中，而且您輸入您的 Active Directory 使用者名稱和密碼正確。 錯誤: ' AADSTS50059: hello 要求中找到沒有租用戶識別資訊，或隱含任何所提供的認證和服務以進行搜尋失敗主體的 URI。 | 您嘗試 toosign 中使用 Microsoft 帳戶與非網域屬於 hello 目錄 hello 組織識別碼嘗試 tooaccess。 請確定該 hello 管理員屬於 hello 相同的網域名稱為 hello 租用戶網域，例如，如果 hello Azure AD 網域為 contoso.com，hello admin 應該是admin@contoso.com。 |
| 無法 tooretrieve hello 目前的執行原則執行 PowerShell 指令碼。 | 如果 hello 連接器安裝失敗，請檢查 toomake 確定未停用 PowerShell 執行原則。 <br><br>1.開啟 hello 群組原則編輯器。<br>2.跳過**電腦設定** > **系統管理範本** > **Windows 元件** >  **Windows PowerShell**按兩下**Turn on Script Execution**。<br>3.hello 執行原則可以設定 tooeither**未設定**或**啟用**。 如果設定太**啟用**，請確定在 選項，hello 執行原則設定 tooeither**允許本機指令碼和遠端簽署指令碼**或太**允許所有指令碼**。 |
| 連接器無法 toodownload hello 組態。 | hello 連接器的用戶端憑證，用來驗證，過期。 如果您擁有的 hello 連接器安裝在 proxy 背景時，這也可能發生。 在此情況下，hello Connector 無法存取網際網路 hello 而且不會無法 tooprovide 應用程式 tooremote 使用者。 更新信任手動使用 hello`Register-AppProxyConnector`中 Windows PowerShell cmdlet。 如果您的連接器位於 proxy 後方，則必要 toogrant 網際網路存取 toohello 連接器帳戶 「 網路服務 」 和 「 本機系統 」。 這可藉由授與它們存取 toohello Proxy 或藉由設定這些 toobypass hello proxy。 |
| 連接器註冊失敗： 請確定您是全域管理員的您 Active Directory tooregister hello 連接器。 錯誤: ' hello 註冊要求遭到拒絕。 」 | 您正嘗試在與 toolog hello 別名不是此網域的系統管理員。 您的連接器一律會安裝 hello 目錄擁有 hello 使用者的網域。 請確定您嘗試在與 toosign hello 系統管理員帳戶具有通用權限 toohello Azure AD 租用戶。 |

## <a name="kerberos-errors"></a>Kerberos 錯誤

下表涵蓋常見的 hello 來自 Kerberos 安裝和組態，而且有建議的解決方式的錯誤。

| 錯誤 | 建議的步驟 |
| ----- | ----------------- |
| 無法 tooretrieve hello 目前的執行原則執行 PowerShell 指令碼。 | 如果 hello 連接器安裝失敗，請檢查 toomake 確定未停用 PowerShell 執行原則。<br><br>1.開啟 hello 群組原則編輯器。<br>2.跳過**電腦設定** > **系統管理範本** > **Windows 元件** >  **Windows PowerShell**按兩下**Turn on Script Execution**。<br>3.hello 執行原則可以設定 tooeither**未設定**或**啟用**。 如果設定太**啟用**，請確定在 選項，hello 執行原則設定 tooeither**允許本機指令碼和遠端簽署指令碼**或太**允許所有指令碼**。 |
| 12008-azure AD 超過 hello 允許 Kerberos 驗證的次數上限 toohello 後端伺服器。 | 此錯誤可能表示 Azure AD 之間設定不正確，hello 後端應用程式伺服器或兩台電腦上的日期和時間設定問題。 hello 後端伺服器拒絕 Azure AD 所建立的 hello Kerberos 票證。 驗證 Azure AD 和 hello 後端應用程式伺服器設定正確。 請確定 hello 日期和時間設定在 hello Azure AD 和 hello 後端應用程式伺服器會同步處理。 |
| 13016-azure AD 無法擷取 Kerberos 票證代表 hello 使用者，因為沒有任何 UPN 的 hello edge 權杖或 hello 存取 cookie 中。 | 沒有 hello STS 組態有問題。 在 hello STS 修正的 hello UPN 宣告組態。 |
| 13019-azure AD 無法擷取 Kerberos 票證代表 hello 使用者，因為發生下列一般 API 錯誤的 hello。 | 這個事件可能表示 Azure AD 之間設定不正確和 hello 網域控制站伺服器或兩台電腦上的日期和時間設定問題。 hello 網域控制站拒絕 Azure AD 所建立的 hello Kerberos 票證。 驗證 Azure AD 和 hello 後端應用程式伺服器設定正確，尤其是 hello SPN 組態。 請確定 hello Azure AD 網域 toohello 相同的網域為 hello hello 網域控制站的網域控制站 tooensure 建立與 Azure AD 的信任關係。 請確定 hello 日期和時間設定在 hello Azure AD 和 hello 網域控制站會同步處理。 |
| 13020-azure AD 無法擷取 Kerberos 票證代表 hello 使用者，因為並未定義 hello 後端伺服器 SPN。 | 這個事件可能表示 Azure AD 之間設定不正確和 hello 網域控制站伺服器或兩台電腦上的日期和時間設定問題。 hello 網域控制站拒絕 Azure AD 所建立的 hello Kerberos 票證。 驗證 Azure AD 和 hello 後端應用程式伺服器設定正確，尤其是 hello SPN 組態。 請確定 hello Azure AD 網域 toohello 相同的網域為 hello hello 網域控制站的網域控制站 tooensure 建立與 Azure AD 的信任關係。 請確定 hello 日期和時間設定在 hello Azure AD 和 hello 網域控制站會同步處理。 |
| 13022-azure AD 無法驗證 hello 使用者，因為 hello 後端伺服器會回應與 HTTP 401 錯誤 tooKerberos 驗證嘗試。 | 此事件可能表示 Azure AD 之間設定不正確，而且 hello 後端應用程式伺服器或兩台電腦上的日期和時間設定問題。 hello 後端伺服器拒絕 Azure AD 所建立的 hello Kerberos 票證。 驗證 Azure AD 和 hello 後端應用程式伺服器設定正確。 請確定 hello 日期和時間設定在 hello Azure AD 和 hello 後端應用程式伺服器會同步處理。 |

## <a name="end-user-errors"></a>使用者錯誤

這份清單包含試 tooaccess hello 應用程式及失敗時，您的使用者可能會遇到的錯誤。 

| 錯誤 | 建議的步驟 |
| ----- | ----------------- |
| hello 網站無法顯示 hello 頁面。 | 如果 hello 應用程式是 IWA 應用程式，您發行的 tooaccess hello 應用程式時，使用者可能會收到這個錯誤。 hello 定義此應用程式可能不正確的 SPN。 對於 IWA 應用程式，請確定該 hello 為此應用程式設定的 SPN 正確。 |
| hello 網站無法顯示 hello 頁面。 | 如果 hello 應用程式是 OWA 應用程式，您發行的 tooaccess hello 應用程式時，使用者可能會收到這個錯誤。 這可能被因 hello 下列其中一種：<br><li>hello 定義此應用程式不正確的 SPN。 請確定該 hello 為此應用程式設定的 SPN 正確。</li><li>hello，使用者嘗試 tooaccess hello 應用程式使用 Microsoft 帳戶，而不是 hello 中，適當的公司帳戶 toosign 或 hello 使用者是 guest 使用者。 請確定 hello 使用者登入時使用公司帳戶相符項目 hello 網域的 hello 發行應用程式。 Microsoft 帳戶使用者和來賓無法存取 IWA 應用程式。</li><li>此應用程式在 hello 由內部部署端未正確定義 hello 使用者嘗試 tooaccess hello 應用程式。 請確定此使用者擁有 hello 適當的權限，為這個 hello 由內部部署電腦上的後端應用程式所定義。 |
| 無法存取此公司應用程式。 您為未獲授權的 tooaccess 此應用程式。 授權失敗。 請確定 tooassign hello 使用者具有存取 toothis 應用程式。 | 嘗試您發行，則他們使用 Microsoft 帳戶而不是在其公司帳戶 toosign tooaccess hello 應用程式時，您的使用者可能會收到這個錯誤。 來賓使用者也可能會發生此錯誤。 Microsoft 帳戶使用者和來賓無法存取 IWA 應用程式。 請確定 hello 使用者登入時使用公司帳戶相符項目 hello 網域的 hello 發行應用程式。<br><br>您可能未指派 hello 這個應用程式的使用者。 移 toohello**應用程式** 索引標籤，然後在**使用者和群組**，指派給此使用者或使用者群組 toothis 應用程式。 |
| 無法立即存取此公司應用程式。 請稍後再試一次...hello 連接器已逾時。 | 嘗試 tooaccess hello 應用程式，您發行，則為此應用程式在 hello 由內部部署端未正確定義時，您的使用者可能會收到這個錯誤。 請確定您的使用者具有這個 hello 由內部部署電腦上的後端應用程式定義 hello 適當的權限。 |
| 無法存取此公司應用程式。 您為未獲授權的 tooaccess 此應用程式。 授權失敗。 請確定該 hello 使用者具有 Azure Active Directory Premium 或 Basic 授權。 | 嘗試 tooaccess hello 應用程式，如果未明確指派給這些 Premium/Basic 授權 hello 訂閱者的系統管理員，您發行時，您的使用者可能會收到這個錯誤。 移 toohello 訂閱者的 Active Directory**授權**索引標籤，請確定此使用者或使用者群組已指派 Premium 或 Basic 授權。 |

## <a name="my-error-wasnt-listed-here"></a>此處未列出我的錯誤

如果您遇到錯誤或是此疑難排解指南中未列出的 Azure AD Application Proxy 問題，我們希望 toohear 資訊，請參閱。 傳送電子郵件 tooour[意見反應小組](mailto:aadapfeedback@microsoft.com)與 hello hello 您遇到的錯誤詳細資料。

## <a name="see-also"></a>另請參閱
* [啟用 Azure Active Directory 的應用程式 Proxy](active-directory-application-proxy-enable.md)
* [使用應用程式 Proxy 發行應用程式](active-directory-application-proxy-publish.md)
* [啟用單一登入](active-directory-application-proxy-sso-using-kcd.md)
* [啟用條件式存取](active-directory-application-proxy-conditional-access.md)


<!--Image references-->
[1]: ./media/active-directory-application-proxy-troubleshoot/connectorproperties.png
[2]: ./media/active-directory-application-proxy-troubleshoot/sessionlog.png
