---
title: "Azure Active Directory B2C︰權杖、工作階段及單一登入設定 | Microsoft Docs"
description: "Azure Active Directory B2C 中的權杖、工作階段及單一登入組態"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: e78e6344-0089-49bf-8c7b-5f634326f58c
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: swkrish
ms.openlocfilehash: 63325ed97a7363723c97ee3a992046ebb5592662
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-token-session-and-single-sign-on-configuration"></a>Azure Active Directory B2C：權杖、工作階段及單一登入設定
這項功能可讓您以 [每個原則為基礎](active-directory-b2c-reference-policies.md)，針對以下項目進行精細控制︰

1. Azure Active Directory (Azure AD) B2C 所發出之安全性權杖的存留期。
2. 由 Azure AD B2C 管理之 Web 應用程式工作階段的存留期。
3. 重要 hello Azure AD B2C 所發出的安全性權杖中宣告的格式。
4. B2C 租用戶中跨越多個應用程式和原則的單一登入 (SSO) 行為。

您可以在 B2C 租用戶中使用這項功能，如下所示︰

1. 請遵循下列步驟太[瀏覽 toohello B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)hello Azure 入口網站上。
2. 按一下 [登入原則] 。 *附註︰這項功能適用於任何原則類型，並不限於**登入原則***。
3. 按一下原則以予以開啟。 例如，按一下 [B2C_1_SiIn]。
4. 按一下**編輯**在 hello hello 刀鋒視窗最上方。
5. 按一下 [權杖、工作階段及單一登入設定]。
6. 變更需要的項目。 了解後續章節中的可用屬性。
7. 按一下 [確定] 。
8. 按一下**儲存**hello 頂端 hello 刀鋒視窗上。

## <a name="token-lifetimes-configuration"></a>權杖存留期組態
Azure AD B2C 支援 hello [OAuth 2.0 授權通訊協定](active-directory-b2c-reference-protocols.md)啟用存取 tooprotected 保護資源的安全。 tooimplement 各種就會發出這項支援，Azure AD B2C[安全性語彙基元](active-directory-b2c-reference-tokens.md)。 這些是您可以使用 Azure AD B2C 所發出的安全性權杖的 toomanage 存留期的 hello 屬性：

* **存取與 ID 權杖存留期 （分鐘）**: hello OAuth 2.0 承載權杖使用的 toogain 存取 tooa hello 存留期間受保護資源。 Azure AD B2C 目前只能發出識別碼權杖。 這個值會套用 tooaccess 語彙基元，當我們將支援加以新增。
  * 預設值 = 60 分鐘。
  * 最小值 (含) = 5 分鐘。
  * 最大值 (含) = 1440 分鐘。
* **重新整理權杖存留期 （天數）**: hello 之前重新整理語彙基元可以用的 tooacquire 的最大的時間期間，新的存取或 ID 語彙基元 (並選擇性地新重新整理權杖，如果您的應用程式已被授與 hello`offline_access`範圍)。
  * 預設值 = 14 天。
  * 最小值 (含) = 1 天。
  * 最大值 (含) = 90 天。
* **重新整理權杖的滑動視窗存留期 （天數）**： 這個時間期間過後 hello 使用者強制的 toore 後的驗證，不論 hello hello hello 應用程式來取得最新重新整理權杖的有效期間。 它可以只提供已設定太 hello 參數，如果**已繫結**。 需要 toobe 大於或等於 toohello**重新整理權杖的存留期 （天數）**值。 如果設定太 hello 參數**Unbounded**，您不能提供精確的值。
  * 預設值 = 90 天。
  * 最小值 (含) = 1 天。
  * 最大值 (含) = 365 天。

以下是幾個可以透過這些屬性實現的使用案例︰

* 只要他或她會持續作用中 hello 應用程式可讓使用者 toostay 無限期地登入行動應用程式。 您可以透過設定 hello**重新整理權杖滑動視窗存留期 （天數）**太切換**Unbounded**在您登入的原則。
* 藉由設定 hello 適當的存取權杖存留期符合您的業界安全性與相容性需求。

    > [!NOTE]
    > 這些設定不適用於密碼重設原則。
    > 
    > 

## <a name="token-compatibility-settings"></a>權杖相容性設定
我們在 Azure AD B2C 所發出的安全性權杖進行格式化變更 tooimportant 宣告。 這是完成 tooimprove 我們的標準通訊協定支援和更佳的互通性與協力廠商身分識別的程式庫。 不過，tooavoid 中斷現有的應用程式，我們會建立下列屬性 tooallow 客戶 tooopt-視 hello:

* **簽發者 (iss) 宣告**： 這會識別發出權杖 hello hello Azure AD B2C 租用戶。
  * `https://login.microsoftonline.com/{B2C tenant GUID}/v2.0/`： 這是 hello 預設值。
  * `https://login.microsoftonline.com/tfp/{B2C tenant GUID}/{Policy ID}/v2.0/`： 這個值會包含識別碼 hello B2C 租用戶和 hello 原則 hello 權杖要求中使用。 如果您的應用程式庫需要 Azure AD B2C toobe 符合 hello [OpenID Connect 探索 1.0 規格](http://openid.net/specs/openid-connect-discovery-1_0.html)，使用此值。
* **主體 (sub) 宣告**： 這會識別 hello 實體，也就是 hello 使用者，哪些 hello 權杖判斷提示資訊。
  * **ObjectID**： 這是 hello 預設值。 Hello 物件識別碼 hello 目錄中的 hello 使用者填入 hello `sub` hello 權杖中宣告。
  * **不支援**： 這只會提供回溯相容性，並建議您改用太**ObjectID**只要能夠。
* **宣告表示原則識別碼**： 這會識別 hello 到哪一個 hello hello 權杖要求中所用的原則識別碼已填入的宣告類型。
  * **tfp**： 這是 hello 預設值。
  * **acr**： 這只會提供回溯相容性，並建議您改用太`tfp`只要能夠。

## <a name="session-behavior"></a>工作階段行為
Azure AD B2C 支援 hello [OpenID Connect 的驗證通訊協定](active-directory-b2c-reference-oidc.md)用於啟用安全登入 tooweb 應用程式。 這些是您可以使用 toomanage web 應用程式工作階段的 hello 屬性：

* **Web 應用程式工作階段存留期 （分鐘）**: hello 存留期的 Azure AD B2C 的工作階段 cookie 儲存在驗證成功後的 hello 使用者的瀏覽器上。
  * 預設值 = 1440 分鐘。
  * 最小值 (含) = 15 分鐘。
  * 最大值 (含) = 1440 分鐘。
* **Web 應用程式工作階段逾時**： 如果此參數設定太**絕對**，hello 使用者是強制的 toore-hello 所指定的時間週期之後驗證**Web 應用程式工作階段存留期 （分鐘）**經過。 如果這個參數設定得**循環**(hello 預設設定)，hello 使用者仍登入，只要 hello 使用者為 web 應用程式中持續作用中。

以下是幾個可以透過這些屬性實現的使用案例︰

* 符合產業的安全性與相容性需求設定 hello 適當的 web 應用程式工作階段存留期。
* 當使用者與 Web 應用程式之高度安全組件的互動達到設定期間後，請強制他們重新驗證。 

    > [!NOTE]
    > 這些設定不適用於密碼重設原則。
    > 
    > 

## <a name="single-sign-on-sso-configuration"></a>單一登入組態
如果您有多個應用程式和原則 B2C 租用戶中，您可以在它們之間管理使用者互動使用 hello**單一登入組態**屬性。 您可以設定下列設定的 hello 的 hello 屬性 tooone:

* **租用戶**： 這是 hello 預設值。 使用此設定可讓多個應用程式和原則 B2C 租用戶中 tooshare hello 相同的使用者工作階段。 例如，一旦使用者登入應用程式 Contoso Shopping 後，他或她就可以在存取另一個應用程式 Contoso Pharmacy 時順暢地登入。
* **應用程式**： 這可讓您 toomaintain 專用的應用程式中，獨立於其他應用程式的使用者工作階段。 例如，如果您想要在 tooContoso 藥局 hello 使用者 toosign (hello 與相同的認證)，即使他或她會登入 Contoso 購物，另一個應用程式上 hello 相同 B2C 租用戶。 
* **原則**： 這可讓您 toomaintain 專用的原則，獨立於 hello 應用程式使用的使用者工作階段。 例如，如果 hello 使用者已登入並完成多重要素驗證 (MFA) 步驟，他或她可以獲得 access toohigher 安全性組件的多個應用程式，只要 hello 繫結工作階段 toohello 原則不會過期。
* **已停用**： 這會透過 hello 整個使用者之旅 hello 使用者 toorun 強制在每次執行 hello 原則。 比方說，這可讓多個使用者 toosign tooyour 應用程式 （在中共用桌面的案例），甚至在單一使用者仍為 hello 整個期間已登入。

    > [!NOTE]
    > 這些設定不適用於密碼重設原則。
    > 
    > 

