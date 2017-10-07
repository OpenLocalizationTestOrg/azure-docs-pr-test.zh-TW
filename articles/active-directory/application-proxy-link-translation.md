---
title: "aaaTranslate 連結和 Url 的 Azure AD 應用程式 Proxy |Microsoft 文件"
description: "涵蓋有關 Azure AD 應用程式 Proxy 連接器 hello 基本概念。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7ec2b9fb01617067cf5d676037877bf72c19217b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="redirect-hardcoded-links-for-apps-published-with-azure-ad-application-proxy"></a>重新導向使用 Azure AD Application Proxy 發佈之應用程式的硬式編碼連結

Azure AD Application Proxy 可讓您在內部部署應用程式可用 toousers 遠端或在他們自己的裝置上。 不過，某些應用程式，所開發的內嵌在 hello HTML 中的本機連結。 從遠端使用 hello 應用程式時，這些連結無法正常運作。 當您有幾個內部部署應用程式點 tooeach 其他時，您的使用者預期 hello 連結 tookeep 運作時不是在 hello 辦公室。 

hello 最佳方式 toomake 確定連結工作 hello 相同這兩個內部公司網路外 tooconfigure hello 外部 Url 的應用程式 toobe hello 相同其內部的 url。 使用[自訂網域](active-directory-application-proxy-custom-domains.md)tooconfigure 您公司網域名稱，而不是 hello 預設應用程式 proxy 網域的外部 Url toohave。

如果您的租用戶中，您無法使用自訂網域，hello 的應用程式 Proxy 連結轉譯 」 功能會保留您不論您的使用者工作的連結。 當您指向直接 toointernal 端點或連接埠，您可以將對應的應用程式時這些內部 Url toohello 發行外部應用程式 Proxy Url。 若已啟用連結轉譯，應用程式 Proxy 會透過 HTML、CSS 搜尋，並選取已發佈內部連結的 JavaScript 標籤。 然後 hello 應用程式 Proxy 服務會轉譯它們，以便讓您的使用者取得不受干擾的體驗。

>[!NOTE]
>hello 連結轉譯功能是讓租用戶，無論原因，無法使用的自訂網域 toohave hello 自己的應用程式的相同內部和外部 Url。 在您啟用這項功能之前，請查看您是否適用 [Azure AD Application Proxy 中的自訂網域](active-directory-application-proxy-custom-domains.md)。
>
>或者，如果您需要與連結轉譯 tooconfigure hello 應用程式是 SharePoint，請參閱[設定適用於 SharePoint 2013 的備用存取對應](https://technet.microsoft.com/library/cc263208.aspx)的另一個方法 toomapping 連結。

## <a name="how-link-translation-works"></a>連結轉譯的運作方式

在驗證之後，當 hello proxy 伺服器傳遞 hello 應用程式資料 toohello 使用者應用程式 Proxy 掃描 hello 應用程式的硬式編碼的連結，然後將它們取代為其各自發行外部 Url。

應用程式 Proxy 假設應用程式是以 UTF-8 編碼。 如果不是 hello 案例，hello 編碼類型中指定 http 回應標頭，例如`Content-Type:text/html;charset=utf-8`。

### <a name="which-links-are-affected"></a>哪些連結會受影響？

hello 連結轉譯功能只會尋找 hello 主體的應用程式中的程式碼標記中的連結。 Application Proxy 有個別功能可轉譯標頭中的 cookie 或 URL。 

內部部署應用程式中有兩種常見的內部連結類型：

- **相對的內部連結**該點 tooa 共用類似的本機檔案結構中的資源`/claims/claims.html`。 這些連結會自動運作中應用程式，透過應用程式 Proxy 發佈，並繼續 toowork 不論連結轉譯。 
- **硬式編碼內部連結**tooother 內部部署應用程式，例如`http://expenses`或發行檔案，像是`http://expenses/logo.jpg`。 hello 連結轉譯功能適用於內部連結硬式編碼，，而且會將其變更 toopoint toohello 外部 Url 的遠端使用者需要透過 toogo。

### <a name="how-do-apps-link-tooeach-other"></a>應用程式如何連結其他 tooeach？

連結轉譯每個應用程式，啟用，所以您需要在 hello 個別應用程式層級的控制 hello 使用者經驗。 開啟連結轉譯為應用程式時想要讓 hello 連結*從*該應用程式 toobe 轉譯，不是連結*至*該應用程式。 

例如，假設您有三個透過所有連結 tooeach 其他的應用程式 Proxy 發行的應用程式： 效益、 費用和移動。 第四個應用程式 (Feedback) 不是透過 Application Proxy 發佈。

當您啟用 hello 優點的應用程式的連結轉譯時，hello 連結 tooExpenses 和旅行重新導向的 toohello 外部 Url，針對這些應用程式，但由於沒有外部 URL hello 連結 tooFeedback 不重新導向。 從費用及移動後 tooBenefits 沒有作用，因為尚未啟用連結轉譯這些兩個應用程式的連結。

![從啟用連結轉譯時的優點 tooother 應用程式的連結](./media/application-proxy-link-translation/one_app.png)

### <a name="which-links-arent-translated"></a>哪些連結並未轉譯？

某些連結 tooimprove 效能和安全性，無法轉譯：

- 不在程式碼標籤內的連結。 
- 不在 HTML、CSS 或 JavaScript 中的連結。 
- 從其他程式開啟的內部連結。 不會轉譯透過電子郵件或立即訊息傳送的連結，或包含在其他文件中的連結。 hello 使用者需要 tooknow toogo toohello 外部 URL。

如果您需要 toosupport 這些兩種情況下，使用 hello 相同內部和外部 Url，而不是連結轉譯。  

## <a name="enable-link-translation"></a>啟用連結轉譯

開始使用連結轉譯很簡單，按一下按鈕即可：

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)身為系統管理員。
2. 跳過**Azure Active Directory** > **企業應用程式** > **所有應用程式**> 選取 hello 應用程式想 toomanage >**應用程式 proxy**。
3. 開啟**應用程式主體中的 轉譯 Url**太**是**。

   ![應用程式主體中選取 [是] tootranslate Url](./media/application-proxy-link-translation/select_yes.png).
4. 選取**儲存**tooapply 您的變更。

現在，當您的使用者存取此應用程式，hello proxy 會自動掃描已透過應用程式 Proxy 發佈在租用戶的內部 Url。

## <a name="send-feedback"></a>傳送意見反應

我們想要說明 toomake 這項功能工作的所有應用程式。 我們以 HTML 和 CSS，搜尋超過 30 的標記，並考慮哪些 JavaScript 案例 toosupport。 如果您有不要翻譯的產生連結的範例，傳送程式碼片段太[應用程式 Proxy 的意見反應](mailto:aadapfeedback@microsoft.com)。 

## <a name="next-steps"></a>後續步驟
[自訂網域搭配 Azure AD Application Proxy](active-directory-application-proxy-custom-domains.md) toohave hello 相同的內部和外部 URL

[設定 SharePoint 2013 的備用存取對應](https://technet.microsoft.com/library/cc263208.aspx)
