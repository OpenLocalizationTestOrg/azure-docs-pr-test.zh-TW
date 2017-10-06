---
title: "Azure Active Directory B2C：開始使用自訂原則 | Microsoft Docs"
description: "Tooget 如何開始使用 Azure Active Directory B2C 的自訂原則"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja;parahk;gsacavdm
ms.openlocfilehash: 5ee133806395cddf18682769a6cad149889d82d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-get-started-with-custom-policies"></a>Azure Active Directory B2C：開始使用自訂原則

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

完成本文中的 hello 步驟之後，您的自訂原則將會支援 「 本機帳戶 」 註冊或登入透過電子郵件地址和密碼。 您也會準備環境以新增識別提供者 (例如 Facebook 或 Azure Active Directory)。 我們鼓勵您 toocomplete 有關其他讀取之前，先依照使用的 hello Azure Active Directory (Azure AD) B2C 身分識別體驗架構。

## <a name="prerequisites"></a>必要條件

繼續之前，請確定具有 Azure AD B2C 租用戶。此租用戶是存放您的所有使用者、應用程式、原則等的容器。 如果您還沒有已經，您需要太[建立 Azure AD B2C 租用戶](active-directory-b2c-get-started.md)。 我們強烈建議所有開發人員 toocomplete hello Azure AD B2C 內建原則逐步解說，並使用內建原則，才能繼續設定其應用程式。 一旦您進行微幅變更 toohello 原則名稱 tooinvoke hello 自訂原則，您的應用程式將會使用這兩種原則類型。

>[!NOTE]
>編輯 tooaccess 自訂原則，您需要有效的 Azure 訂用帳戶連結的 tooyour 租用戶。 如果還沒有[連結您 Azure 訂用帳戶的 Azure AD B2C 租用戶 tooan](active-directory-b2c-how-to-enable-billing.md)或您的 Azure 訂用帳戶已停用，hello 身分識別體驗架構按鈕將無法使用。

## <a name="add-signing-and-encryption-keys-tooyour-b2c-tenant-for-use-by-custom-policies"></a>新增簽章和加密金鑰 tooyour B2C 租用戶使用的自訂原則

1. 開啟 hello**身分識別體驗架構**刀鋒視窗，在您的 Azure AD B2C 租用戶設定。
2. 選取**原則機碼**tooview hello 金鑰用於您的租用戶。
3. 如果 B2C_1A_TokenSigningKeyContainer 不存在，請加以建立：<br>
    a. 選取 [新增] 。 <br>
    b.這是另一個 C# 主控台應用程式。 選取 [產生]。<br>
    c. 針對 [名稱] 使用 `TokenSigningKeyContainer`。 <br> 
    hello 前置詞`B2C_1A_`可能會自動加入。<br>
    d. 針對 [金鑰類型] 使用 [RSA]。<br>
    e. 如**日期**，使用 hello 預設值。 <br>
    f. 針對 [金鑰使用方法] 使用 [簽章]。<br>
    g. 選取 [ **建立**]。<br>
4. 如果 B2C_1A_TokenEncryptionKeyContainer 不存在，請加以建立：<br>
 a. 選取 [新增] 。<br>
 b.這是另一個 C# 主控台應用程式。 選取 [產生]。<br>
 c. 針對 [名稱] 使用 `TokenEncryptionKeyContainer`。 <br>
   hello 前置詞`B2C_1A`_ 可能會自動加入。<br>
 d. 針對 [金鑰類型] 使用 [RSA]。<br>
 e. 如**日期**，使用 hello 預設值。<br>
 f. 針對 [金鑰使用方法] 使用 [加密]。<br>
 g. 選取 [ **建立**]。<br>
5. 建立 B2C_1A_FacebookSecret。 <br>
如果您已經有 Facebook 應用程式密碼，請將它加入做為原則金鑰 tooyour 租用戶。 否則，您必須建立 hello 金鑰預留位置值，讓您的原則通過驗證。<br>
 a. 選取 [新增] 。<br>
 b.這是另一個 C# 主控台應用程式。 針對 [選項] 使用 [手動]。<br>
 c. 針對 [名稱] 使用 `FacebookSecret`。 <br>
 hello 前置詞`B2C_1A_`可能會自動加入。<br>
 d. 在 [hello**密碼**方塊中，輸入您 FacebookSecret 從 developers.facebook.com 或`0`做為預留位置。 這不是您的 Facebook 應用程式識別碼。 <br>
 e. 針對 [金鑰使用方法] 使用 [簽章]。 <br>
 f. 選取 [建立] 並確認建立。

## <a name="register-identity-experience-framework-applications"></a>註冊身分識別體驗架構應用程式

Azure AD B2C 需要 tooregister 兩個額外的應用程式所使用的總 hello 引擎 toosign 並登入使用者。

>[!NOTE]
>您必須建立兩個應用程式的啟用登入使用本機帳戶： IdentityExperienceFramework （web 應用程式） 和 ProxyIdentityExperienceFramework （原生應用程式） 與委派 hello IdentityExperienceFramework 應用程式的權限。 本機帳戶只存在於您的租用戶。 您的使用者註冊使用唯一的電子郵件地址/密碼組合 tooaccess 您租用戶註冊的應用程式。

### <a name="create-hello-identityexperienceframework-application"></a>建立 hello IdentityExperienceFramework 應用程式

1. 在 [hello [Azure 入口網站](https://portal.azure.com)，切換至 hello[內容，您的 Azure AD B2C 租用戶](active-directory-b2c-navigate-to-b2c-context.md)。
2. 開啟 hello **Azure Active Directory**刀鋒視窗 (不 hello **Azure AD B2C**刀鋒視窗)。 您可能需要 tooselect**更服務**toofind 它。
3. 選取 [應用程式註冊]。
4. 選取 [新增應用程式註冊]。
   * 針對 [名稱] 使用 `IdentityExperienceFramework`。
   * 針對 [應用程式類型] 使用 [Web 應用程式/API]。
   * 針對 [登入 URL] 使用 `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`，其中 `yourtenant` 是您的 Azure AD B2C 租用戶網域名稱。
5. 選取 [ **建立**]。
6. 一旦建立之後，選取新建立的 hello 應用程式**IdentityExperienceFramework**。<br>
   * 選取 [屬性] 。<br>
   * 複製 hello 應用程式識別碼，並將它儲存為更新版本。

### <a name="create-hello-proxyidentityexperienceframework-application"></a>建立 hello ProxyIdentityExperienceFramework 應用程式

1. 選取 [應用程式註冊]。
1. 選取 [新增應用程式註冊]。
   * 針對 [名稱] 使用 `ProxyIdentityExperienceFramework`。
   * 針對 [應用程式類型] 使用 [原生]。
   * 針對 [重新導向 URI] 使用 `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`，其中 `yourtenant` 是您的 Azure AD B2C 租用戶。
1. 選取 [ **建立**]。
1. 一旦建立它，選取 hello 應用程式**ProxyIdentityExperienceFramework**。<br>
   * 選取 [屬性] 。 <br>
   * 複製 hello 應用程式識別碼，並將它儲存為更新版本。
1. 選取 [必要權限]。
1. 選取 [新增] 。
1. 選取 [選取 API]。
1. 搜尋 hello 名稱 IdentityExperienceFramework。 選取**IdentityExperienceFramework**在 hello 結果，然後按一下 [**選取**。
1. 選取 [hello] 核取方塊旁太**存取 IdentityExperienceFramework**，然後按一下 [**選取**。
1. 選取 [完成] 。
1. 選取 [授與權限]，然後選取 [是] 加以確認。

## <a name="download-starter-pack-and-modify-policies"></a>下載入門套件和修改原則

自訂的原則是一組需要上傳 toobe tooyour Azure AD B2C 租用戶的 XML 檔案。 我們提供入門套件 tooget 您快速地移。 Hello 下列清單中的每個入門套件包含 hello 的技術的設定檔的最小數目，而且使用者皆需要 tooachieve hello 案例所述：
 * LocalAccounts。 可讓您使用本機帳戶只 hello。
 * SocialAccounts。 可讓您使用 hello 社交 （或同盟） 帳戶。
 * **SocialAndLocalAccounts**。 我們 hello 逐步解說使用這個檔案。
 * SocialAndLocalAccountsWithMFA。 此處包含社交、本機及 Multi-Factor Authentication 選項。

每個入門套件均包含：

* hello[基底檔案](active-directory-b2c-overview-custom.md#policy-files)的 hello 原則。 一些修改，就需要的 toohello 基底。
* hello[延伸模組檔案](active-directory-b2c-overview-custom.md#policy-files)的 hello 原則。  大部分的設定變更都在這個檔案中完成。
* [信賴憑證者檔案](active-directory-b2c-overview-custom.md#policy-files)是工作特定檔案，由應用程式呼叫。

>[!NOTE]
>如果您的 XML 編輯器支援驗證，驗證位於 hello 入門套件 hello 根目錄中的 hello TrustFrameworkPolicy_0.3.0.0.xsd XML 結構描述中的 hello 檔案。 在上載之前，XML 結構描述驗證會識別錯誤。

 現在就開始吧！

1. 從 GitHub 下載 active-directory-b2c-custom-policy-starterpack。 [下載 hello.zip 檔案](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip)或執行

    ```console
    git clone https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack
    ```
2. 開啟 hello SocialAndLocalAccounts 資料夾。  hello 基底檔案 (TrustFrameworkBase.xml)，此資料夾中的包含所需的本機和公司身分證/帳戶內容。 hello 社交內容不會干擾 hello 快速安裝的本機帳戶和執行的步驟。
3. 開啟 TrustFrameworkBase.xml。 如果您需要 XML 編輯器，請[試用 Visual Studio 程式碼](https://code.visualstudio.com/download)，這是一個輕巧的跨平台編輯器。
4. Hello 根目錄中`TrustFrameworkPolicy`元素中，更新 hello`TenantId`和`PublicPolicyUri`屬性、 取代`yourtenant.onmicrosoft.com`hello 網域名稱，您的 Azure AD B2C 租用戶：
   ```xml
    <TrustFrameworkPolicy
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:xsd="http://www.w3.org/2001/XMLSchema"
    xmlns="http://schemas.microsoft.com/online/cpim/schemas/2013/06"
    PolicySchemaVersion="0.3.0.0"
    TenantId="yourtenant.onmicrosoft.com"
    PolicyId="B2C_1A_TrustFrameworkBase"
    PublicPolicyUri="http://yourtenant.onmicrosoft.com">
    ```
   >[!NOTE]
   >`PolicyId`是您在 hello 入口網站中看到的 hello 原則名稱和 hello 用這個原則檔正由其他原則檔案的名稱。

5. 儲存 hello 檔案。
6. 開啟 TrustFrameworkExtensions.xml。 進行相同的兩個變更 hello 取代`yourtenant.onmicrosoft.com`與 Azure AD B2C 租用戶。 請 hello 相同 hello 中的取代`<TenantId>`總共有三個變更的項目。 儲存 hello 檔案。
7. 開啟 SignUpOrSignIn.xml。 進行相同變更 hello 取代`yourtenant.onmicrosoft.com`與 Azure AD B2C 租用戶在三個位置。 儲存 hello 檔案。
8. 開啟 hello 密碼重設和設定檔編輯檔案。 進行相同變更 hello 取代`yourtenant.onmicrosoft.com`與 Azure AD B2C 租用戶的每個檔案中的三個位置。 儲存 hello 檔案。

### <a name="add-hello-application-ids-tooyour-custom-policy"></a>新增 hello 應用程式識別碼 tooyour 自訂原則
加入 hello 應用程式識別碼 toohello 延伸模組檔案 (`TrustFrameworkExtensions.xml`):

1. 在 hello 延伸模組檔案 (TrustFrameworkExtensions.xml)，尋找 [hello 元素`<TechnicalProfile Id="login-NonInteractive">`。
2. 取代的兩個執行個體`IdentityExperienceFrameworkAppId`hello 的 hello 您稍早建立的身分識別體驗架構應用程式的應用程式識別碼。 下列是一個範例：

   ```xml
   <Item Key="client_id">8322dedc-cbf4-43bc-8bb6-141d16f0f489</Item>
   ```
3. 取代的兩個執行個體`ProxyIdentityExperienceFrameworkAppId`hello 的 hello 您稍早建立的 Proxy 識別體驗架構應用程式的應用程式識別碼。
4. 儲存擴充檔案。

## <a name="upload-hello-policies-tooyour-tenant"></a>上傳 hello 原則 tooyour 租用戶

1. 在 hello [Azure 入口網站](https://portal.azure.com)，切換至 hello[內容，您的 Azure AD B2C 租用戶](active-directory-b2c-navigate-to-b2c-context.md)，並開啟 hello **Azure AD B2C**刀鋒視窗。
2. 選取 [識別體驗架構]。
3. 選取 [上傳原則]。

    >[!WARNING]
    >hello 自訂原則檔案必須上傳中順序的 hello:

1. 上傳 TrustFrameworkBase.xml。
2. 上傳 TrustFrameworkExtensions.xml。
3. 上傳 SignUpOrSignin.xml。
4. 上傳其他原則檔案。

上傳檔案時，hello hello 原則檔案名稱前面會加上`B2C_1A_`。

## <a name="test-hello-custom-policy-by-using-run-now"></a>使用 [立即執行測試 hello 自訂原則

1. 開啟**Azure AD B2C 設定**並移過**身分識別體驗架構**。

   >[!NOTE]
   >**現在就執行**需要至少一個應用程式 toobe 預先 hello 租用戶上。 應用程式必須使用 hello hello B2C 租用戶中註冊**應用程式**功能表選取項目在 Azure AD B2C 或使用 hello 身分識別體驗架構 tooinvoke 內建和自訂原則。 每個應用程式只需要一個註冊。<br><br>
   如何 tooregister 應用程式，請參閱的 toolearn hello Azure AD B2C[開始](active-directory-b2c-get-started.md)文章或 hello[應用程式註冊](active-directory-b2c-app-registration.md)發行項。  

2. 開啟 B2C_1A_signup_signin、 hello 上載的信賴憑證者 (rp) 自訂原則。 選取 [立即執行]。

3. 您應該能夠 toosign 使用電子郵件地址。

4. 使用登入 hello tooconfirm，您必須使用相同帳戶 hello 正確的組態。

>[!NOTE]
>登入失敗的常見原因是 IdentityExperienceFramework 應用程式設定不正確。


## <a name="next-steps"></a>後續步驟

### <a name="add-facebook-as-an-identity-provider"></a>將 Facebook 新增為識別提供者
註冊 Facebook tooset:
1. [在 developers.facebook.com 中設定 Facebook 應用程式](active-directory-b2c-setup-fb-app.md)。
2. [新增 hello Facebook 應用程式密碼 tooyour Azure AD B2C 租用戶](#add-signing-and-encryption-keys-to-your-b2c-tenant-for-use-by-custom-policies)。
3. 在 hello TrustFrameworkExtensions 原則檔案中，以取代 hello 值`client_id`hello Facebook 應用程式識別碼：

   ```xml
   <TechnicalProfile Id="Facebook-OAUTH">
     <Metadata>
     <!--Replace hello value of client_id in this technical profile with hello Facebook app ID"-->
       <Item Key="client_id">00000000000000</Item>
   ```
4. 上傳 hello TrustFrameworkExtensions.xml 原則檔案 tooyour 租用戶。
5. 使用測試**立即執行**或叫用 hello 原則直接從您已註冊的應用程式。

### <a name="add-azure-active-directory-as-an-identity-provider"></a>將 Azure Active Directory 新增為識別提供者
hello 已經用於這個使用者入門指南的基底檔案可包含一些您需要新增其他身分識別提供者的 hello 內容。 如需設定登入資訊，請參閱 hello [Azure Active Directory B2C： 使用 Azure AD 帳戶登入](active-directory-b2c-setup-aad-custom.md)發行項。

如需在 Azure AD B2C 使用 hello 身分識別體驗架構的自訂原則的概觀，請參閱 hello [Azure Active Directory B2C： 自訂原則](active-directory-b2c-overview-custom.md)發行項。 
