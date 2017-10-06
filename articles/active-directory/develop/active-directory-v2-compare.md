---
title: "aaaWhat 是 hello Azure AD v2.0 端點中不同的嗎？ | Microsoft Docs"
description: "Hello 原始的 Azure AD 與 hello v2.0 端點之間的比較。"
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5060da46-b091-4e25-9fa8-af4ae4359b6c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: e7ed196f9053fc21db799cd6bc513ba5c2b92885
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="whats-different-about-hello-v20-endpoint"></a>何謂不同有關 hello v2.0 端點？
如果您是熟悉使用 Azure Active Directory 或已與 hello 過去在 Azure AD 整合的應用程式，可能無法如預期般 hello v2.0 端點中的一些差異。  本文件集結了這些差異，讓您得以瞭解。

> [!NOTE]
> 並非所有的 Azure Active Directory 案例和功能都受到 hello v2.0 端點。  toodetermine 如果應該使用 hello v2.0 端點，閱讀有關[v2.0 限制](active-directory-v2-limitations.md)。
>

## <a name="microsoft-accounts-and-azure-ad-accounts"></a>Microsoft 帳戶和 Azure AD 帳戶
hello v2.0 端點可讓開發人員 toowrite 登入來自 Microsoft 帳戶和 Azure AD 的帳戶，使用單一授權端點所接受的應用程式。  這讓您的應用程式完全帳戶無關; hello 能力 toowrite它可以是帳戶的不知道 hello hello 使用者登入類型。  當然，您*可以*讓您的應用程式知道 hello 中特定的工作階段中，使用的帳戶類型，但您不需要。

比方說，如果您的應用程式呼叫 hello [Microsoft Graph](https://graph.microsoft.io)，某些額外的功能和資料將會使用 tooenterprise 的使用者，例如其 SharePoint 網站或目錄資料。  但對於許多動作，例如[讀取使用者的郵件](https://graph.microsoft.io/docs/api-reference/v1.0/resources/message)，hello 程式碼可以完全寫入 hello 相同的 Microsoft 帳戶和 Azure AD 的帳戶。  

整合應用程式與 Microsoft 帳戶和 Azure AD 帳戶現在是一個簡單的程序。  您可以使用一組端點、 單一程式庫和單一應用程式註冊 toogain 存取 tooboth hello 消費者和企業環境。  toolearn 深入了解 hello v2.0 端點，請簽出[hello 概觀](active-directory-appmodel-v2-overview.md)。

## <a name="new-app-registration-portal"></a>新的 App 註冊入口網站
tooregister 與 hello v2.0 端點的運作方式的應用程式，您必須使用新的應用程式註冊入口網站： [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)。這是 hello 入口網站，您可以在哪裡取得應用程式識別碼，來自訂您的應用程式登入頁面，以及其他 hello 外觀。  您只需要 tooaccess hello 入口網站是電源的 Microsoft 帳戶-個人或工作/學校帳戶。

## <a name="one-app-id-for-all-platforms"></a>所有平台使用一個應用程式識別碼
如果您已經使用 Azure Active Directory，您可能已針對單一專案註冊數個不同的應用程式。  例如，如果您建立網站和 iOS 應用程式，您必須 tooregister 它們分別使用兩個不同的應用程式識別碼。 hello Azure AD 應用程式註冊入口網站註冊期間，這樣的區別將強制您 toomake:

![舊版應用程式註冊 UI](../../media/active-directory-v2-flows/old_app_registration.PNG)

同樣地，如果您有網站和後端 Web API，您可能已在 Azure AD 中將它們註冊為個別的應用程式。  或者，如果您有 iOS 應用程式和 Android 應用程式，您也可能已註冊兩個不同的應用程式。  註冊應用程式的每個元件的 led toosome 非預期的行為，開發人員和他們的客戶：

* 每個元件顯示為每一位客戶的 hello Azure Active Directory 租用戶中的個別應用程式。
* 當租用戶系統管理員嘗試 tooapply 原則來管理存取權，或刪除應用程式時，他們必須 toodo 因此 hello 應用程式的每個元件。
* 當客戶同意 tooan 應用程式時，每個元件會出現在 hello 同意畫面，做為不同的應用程式。

與 hello v2.0 端點，現在可以為單一應用程式註冊，註冊您的專案的所有元件，並為整個專案中使用單一的應用程式識別碼。  您可以加入數個 「 平台 」 tooa 每個專案，並提供您加入每個平台 hello 適當的資料。  當然，您可以建立許多應用程式為您要根據您的需求，但在 hello 大多數情況下只有一個應用程式識別碼應該是必要。

我們的目標是，這將會導致 tooa 詳細簡化應用程式管理和開發體驗，並建立單一專案，您可能會使用更合併的檢視。

## <a name="scopes-not-resources"></a>範圍，而非資源
在 Azure Active Directory 中，應用程式能以「資源」，或是權杖收件者的方式運作。  資源可以定義多種**範圍**或**oAuth2Permissions**它了解，讓用戶端應用程式特定的一組範圍 toorequest 語彙基元 toothat 資源。  請考慮 hello Azure AD Graph API，做為資源的範例：

* 資源識別碼，或`AppID URI`：`https://graph.windows.net/`
* 範圍，或`OAuth2Permissions`：`Directory.Read`、`Directory.Write` 等。  

這些全部都保存 hello hello v2.0 端點，則為 true。  應用程式仍可做為資源、定義範圍並依據 URI 識別。  用戶端應用程式仍可以要求存取 toothose 領域。  不過，在其中用戶端會要求這些權限的 hello 方式已變更。  Hello 過去，在 OAuth 2.0 授權要求 tooAzure AD 可能有看起來像：

```
GET https://login.microsoftonline.com/common/oauth2/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&resource=https%3A%2F%2Fgraph.windows.net%2F
...
```

其中 hello**資源**參數指示哪些資源 hello 用戶端應用程式所要求的授權。  Azure AD 會計算 hello hello 應用程式根據 hello Azure 入口網站中的靜態設定，並據以發出的權杖所需的權限。  現在，hello 相同的 OAuth 2.0 授權要求看起來像是：

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&scope=https%3A%2F%2Fgraph.windows.net%2Fdirectory.read%20https%3A%2F%2Fgraph.windows.net%2Fdirectory.write
...
```

其中 hello**範圍**參數表示的資源和權限 hello 應用程式所要求的授權。 hello 所需的資源存在於仍然非常 hello 要求-它只包含在每個 hello hello 範圍參數值。  以這種方式使用 hello 範圍參數允許 hello v2.0 端點 toobe 更符合 OAuth 2.0 hello 規格，並會與通用的業界作法更密切地對應。  它也可讓應用程式 tooperform[累加同意](#incremental-and-dynamic-consent)，hello 下一節中所說明。

## <a name="incremental-and-dynamic-consent"></a>增量和動態同意
註冊 toospecify 先前所需的 Azure AD 中應用程式在應用程式建立時在 hello Azure 入口網站，其需要的 OAuth 2.0 權限：

![權限註冊 UI](../../media/active-directory-v2-flows/app_reg_permissions.PNG)

需要應用程式所設定的 hello 權限**靜態**。  雖然這 hello Azure 入口網站中允許的 hello 應用程式 tooexist 組態，並保留清晰且簡單的 hello 程式碼，它會呈現為開發人員的一些問題：

* 應用程式有 tooknow 所有 hello 會需要在應用程式建立時的權限。  隨著時間新增權限有所困難。
* 應用程式有 tooknow 所有它曾經存取事先 hello 資源。  您很難 toocreate 應用程式可以存取的任意數目的資源。
* 應用程式具有 toorequest 會需要在 hello 使用者首次登入的所有 hello 權限。  在某些情況下，這會導致 tooa 的權限，不建議使用從核准初始登入的 hello 應用程式的存取權的使用者很長的清單。

與 hello v2.0 端點，您可以指定 hello 權限的應用程式需求**動態**，在執行階段，在您的應用程式的一般使用。  toodo 因此，您可以指定 hello 您的應用程式需求，在任何給定時間點的時間範圍併入 hello`scope`授權要求參數：

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&scope=https%3A%2F%2Fgraph.windows.net%2Fdirectory.read%20https%3A%2F%2Fgraph.windows.net%2Fdirectory.write
...
```

hello 上述要求 hello 應用程式 tooread 權限，在 Azure AD 使用者的目錄資料，以及寫入資料 tootheir 目錄。  如果 hello 使用者已經同意 hello 過去 toothose 權限特定應用程式中，它們會直接輸入其認證和登入 hello 應用程式。  如果 hello 使用者不同意這些權限的 tooany，hello v2.0 端點會要求 hello 使用者同意 toothose 權限。  toolearn 更多，您可以閱讀[權限、 同意，以及範圍](active-directory-v2-scopes.md)。

允許應用程式 toorequest 權限，以動態方式透過 hello`scope`參數可讓您完整控制您的使用者體驗。  如果您希望，您可以選擇的 toofrontload 您的同意體驗，並且要求一項的初始授權要求中的所有權限。  或者，如果您的應用程式需要大量的權限，您可以選擇 toogather 這些權限從 hello 使用者以累加的方式，如它們經過一段時間嘗試 toouse 您的應用程式的特定功能。

## <a name="well-known-scopes"></a>知名的範圍
#### <a name="offline-access"></a>離線存取
使用 hello v2.0 端點的應用程式可能需要 hello 使用新的已知的權限的應用程式-hello`offline_access`範圍。  所有應用程式如果，則需要 toorequest 此權限的必要 tooaccess 資源上 hello 代表使用者執行很長一段時間，即使 hello 使用者可能不主動使用 hello 應用程式。  hello`offline_access`範圍將會出現 toohello 使用者同意對話方塊為 「 存取您的資料離線 」，hello 使用者必須同意。  要求的 hello`offline_access`權限可讓您的 web 應用程式 tooreceive OAuth 2.0 refresh_tokens 從 hello v2.0 端點。  Refresh_token 屬於長效權杖，可用來交換新的 OAuth 2.0 access_token 以延長存取期間。  

如果您的應用程式沒有要求 hello`offline_access`範圍，則不會接收 refresh_tokens。  這表示，當您兌換 authorization_code hello OAuth 2.0 授權碼流程中的，您只會接收回 access_token 從 hello`/token`端點。  該 access_token 會短時間維持有效 (通常是一小時)，但最後終將過期。  在該點的時間，您的應用程式需要 tooredirect hello 使用者回復 toohello`/authorize`端點 tooretrieve 新 authorization_code。  在此重新導向，hello 使用者可能或可能無法再次需要 tooenter 他們的認證或重新同意 toopermissions，根據 hello hello 類型的應用程式。

深入了解 hello 的 OAuth 2.0、 refresh_tokens 和 access_tokens，取出 toolearn [v2.0 通訊協定參考](active-directory-v2-protocols.md)。

#### <a name="openid-profile-and-email"></a>OpenID、設定檔和電子郵件
在過去，hello 最基本 OpenID Connect 登入流程與 Azure Active Directory 會提供豐富的 hello 產生 id_token 中的 hello 使用者的相關資訊。  在 id_token hello 宣告可以包含 hello 使用者名稱、 慣用的使用者名稱、 電子郵件地址、 物件識別碼、 等等。

我們正在該 hello 限制 hello 資訊`openid`範圍可以提供您的應用程式的存取權。  hello 'openid' 範圍將僅允許應用程式 toosign hello 使用者中，並收到 hello 使用者應用程式特定識別項。  如果您想 tooobtain 個人識別資訊 (PII) 有關 hello 使用者應用程式中，您的應用程式必須 toorequest hello 使用者從其他權限。  我們採用兩個新領域 – hello`email`和`profile`範圍 – 可讓您 toodo 因此。

hello`email`範圍是非常簡單，因為它可讓您的應用程式存取 toohello 使用者的主要電子郵件地址，透過 hello `email` hello id_token 中宣告。  hello`profile`範圍可以提供您的應用程式存取 tooall hello 使用者 – 其名稱、 慣用的使用者名稱，其他基本資訊的物件識別碼，等等。

這可讓您 toocode 您的應用程式，以最少洩漏的方式 – 您可以只要求 hello 使用者 hello 組的應用程式需要 toodo 其作業的資訊。  如需有關這些範圍的詳細資訊，請參閱太[hello v2.0 範圍參考](active-directory-v2-scopes.md)。

## <a name="token-claims"></a>權杖宣告
hello v2.0 端點所發出的權杖中的 hello 宣告不會發出 hello 正式推出的 Azure AD 端點的相同 tootokens-移轉 toohello 新服務的應用程式不應該假設的特定宣告會存在於 id_tokens 或 access_tokens。 toolearn 有關 hello v2.0 權杖中發出的特定宣告，請參閱 「 hello [v2.0 權杖參照](active-directory-v2-tokens.md)。

## <a name="limitations"></a>限制
有一些限制 toobe 時使用 hello v2.0 點。  請參閱 toohello [v2.0 限制文件](active-directory-v2-limitations.md)toosee 如果任何這些限制適用於 tooyour 特定案例。
