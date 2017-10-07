---
title: "Azure Active Directory B2C：自訂原則 | Microsoft Docs"
description: "Azure Active Directory B2C 自訂原則的主題"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 1ff398a4-2079-4615-94f1-57de22c0aad6
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: parakhj
ms.openlocfilehash: bada9cf5f1a86f3dd047536f6fd9359c0231a384
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-custom-policies"></a>Azure Active Directory B2C：自訂原則

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

## <a name="what-are-custom-policies"></a>何謂自訂原則？

自訂的原則是定義您的 Azure AD B2C 租用戶的 hello 行為的組態檔。 而**內建原則**hello 最常見的身分工作，自訂原則可在 Azure AD B2C hello 入口網站中預先定義完全由身分識別開發人員 toocomplete 編輯附近的無限制的工作數目。 如果自訂原則的最適合您和您的身分識別案例，請閱讀 toodetermine 上。

**編輯自訂原則並不適合每個人。** hello 學習曲線要求 (demand)，hello 啟動的時間較長，並且未來變更 toocustom 原則需要類似的專業知識 toomaintain。 使用自訂原則之前，應該謹慎考量優先在您的案例中使用內建原則。

## <a name="comparing-built-in-policies-and-custom-policies"></a>比較內建原則和自訂原則

| | 內建原則 | 自訂原則 |
|-|-------------------|-----------------|
|目標使用者 | 所有具備或不具備身分識別專業知識的應用程式開發人員 | 身分識別專業人員︰系統整合人員、顧問和內部身分識別小組。 他們熟悉 OpenIDConnect 流程，也了解身分識別提供者和宣告型驗證 |
|設定方法 | 有 UI 方便使用的 Azure 入口網站 | 直接編輯 XML 檔案，然後上傳 toohello Azure 入口網站 |
|UI 自訂 | 完整的 UI 自訂，包括 HTML、CSS 和 jscript 支援 (需要自訂網域)<br><br>使用自訂字串支援多語言 | 相同 |
| 屬性自訂 | 標準和自訂屬性 | 相同 |
|權杖和工作階段管理 | 自訂權杖和多個工作階段選項 | 相同 |
|識別提供者| **目前**︰預先定義的本機、社交提供者<br><br>**未來**︰標準式 OIDC、SAML、OAuth | **目前**：標準式 OIDC、OAUTH、SAML<br><br>**未來**：WsFed |
|身分識別工作 (範例) | 使用本機和許多社交帳戶註冊或登入<br><br>自助式密碼重設<br><br>設定檔編輯<br><br>Multi-Factor Auth 案例<br><br>自訂權杖和工作階段<br><br>存取權杖流程 | 完成相同工作做為內建原則，使用自訂身分識別提供者的 hello 或使用自訂的範圍<br><br>在 hello 階段的另一個系統的登錄中的佈建使用者<br><br>使用您自己的電子郵件服務提供者傳送歡迎電子郵件<br><br>使用 B2C 外部的使用者存放區<br><br>透過 API 向受信任的系統驗證使用者所提供的資訊 |

## <a name="policy-files"></a>原則檔

自訂的原則被以一或多個 XML 格式的檔案而是會參照 tooeach 其他階層式鏈結中。 hello XML 項目定義： 宣告結構描述中，宣告轉換、 內容定義、 宣告提供者/技術設定檔和其他項目之間的 Userjourney 協調流程步驟。

我們建議 hello 使用三種類型的原則檔：

- **基底檔案**，其中包含大部分的 hello 定義以及 Azure 提供完整的範例。  我們建議您讓 toothis 檔案 toohelp 疑難排解之後，變更最小的數目和長期維護您的原則
- **擴充檔**保存 hello 唯一的組態變更為您的租用戶
- **信賴憑證者的合作對象 (RP) 檔案**即 hello 單一工作為主的檔案直接所 hello 應用程式或服務 （也稱為信賴憑證者合作對象） 叫用。  如需詳細資訊的原則檔案定義上的讀取 hello 文章。  每個唯一的工作需要自己 RP 並根據商標需求 hello 數目可能是"x 使用案例的總數的應用程式的總計 」。


內建原則，在 Azure AD B2C 遵循僅 hello 入口網站在 hello 背景 toohello EXTenstions 檔案進行的變更時，所看到 hello 信賴憑證者的合作對象 (RP) 檔案，但 hello 開發人員描述上述的 hello 3 檔案模式。

## <a name="core-concepts-you-should-know-when-using-custom-policies"></a>使用自訂原則時應該知道的核心概念

### <a name="azure-active-directory-b2c"></a>Azure Active Directory B2C

Azure 的客戶身分識別和存取管理 (CIAM) 服務。 hello 服務包括：

1. Hello 形式特殊用途 Azure Active Directory 可透過 Microsoft Graph 和其中保留本機帳戶和同盟的帳戶的使用者資料存取使用者目錄 
2. 存取 toohello**身分識別體驗架構**其中協調使用者與實體之間的信任，並將宣告傳遞它們之間 toocomplete 識別/存取管理工作 
3. 安全性權杖服務 (STS) 發行識別碼語彙基元、 重新整理權杖和存取語彙基元 （及對等的 SAML 判斷提示），並驗證其 tooprotect 資源。

Azure AD B2C 與身分識別提供者、 使用者、 其他系統和互動 hello 本機使用者目錄中順序 tooachieve 識別工作 （例如登入使用者，註冊新的使用者、 重設密碼）。 hello 基礎的平台，可建立多個合作對象的信任關係並執行下列步驟稱為 hello 身分識別體驗架構和原則 （也稱為使用者之旅或信任架構原則） 明確地定義 hello 執行者，hello 動作 hello通訊協定，以及步驟 toocomplete hello 序列。

### <a name="identity-experience-framework"></a>身分識別體驗架構

完全可設定、原則導向、雲端式的 Azure 平台，協調標準通訊協定格式 (例如 OpenIDConnect、OAuth、SAML、WSFed) 實體 (大致上是宣告提供者) 和少數非標準格式 (例如以 REST API 為基礎的系統對系統宣告交換) 實體之間的信任。 hello I2E 建立使用者易記、 whitelabelled 發生時，支援 HTML、 CSS 和 jscript。  現在，hello 身分識別經驗架構只能在 hello hello Azure AD B2C 服務內容，並且工作相關 tooCIAM 優先。

### <a name="built-in-policies"></a>內建原則

預先定義的組態檔的 Azure AD B2C tooperform hello 最常使用的身分識別的直接 hello 行為工作 （也就是使用者註冊、 登入，密碼重設），以及與受信任的關係也預先定義在 Azure AD B2C （的合作對象互動例如 Facebook 身分識別提供者，LinkedIn，Microsoft 帳戶，Google 帳戶）。  在未來的 hello，也會提供內建原則，通常是在 hello 企業領域，例如 Azure Active Directory Premium、 Active Directory ADFS 等 Salesforce ID 提供者的身分識別提供者的自訂。


### <a name="custom-policies"></a>自訂原則

定義您的 Azure AD B2C 租用戶中的身分識別體驗架構 hello 行為的組態檔。 存取為一或多個 XML 檔案 （請參閱原則檔案定義） 的 hello 由信賴憑證者的合作對象 （例如應用程式） 叫用時，身分識別體驗架構所執行的自訂原則。 自訂的原則可以直接編輯身分識別開發人員 toocomplete 附近的無限制的工作數目。 開發人員必須定義設定的自訂原則 hello 小心詳細 tooinclude 中繼資料端點中的信任關聯性，確切的宣告交換定義，並根據每個身分識別提供者需要設定密碼、 金鑰和憑證。

## <a name="policy-file-definitions-for-identity-experience-framework-trustframeworks"></a>識別體驗架構 Trustframeworks 的原則檔案定義

### <a name="policy-files"></a>原則檔

自訂的原則被以一或多個 XML 格式的檔案而是會參照 tooeach 其他階層式鏈結中。 hello XML 項目定義： 宣告結構描述中，宣告轉換、 內容定義、 宣告提供者/技術設定檔和其他項目之間的 Userjourney 協調流程步驟。  我們建議 hello 使用三種類型的原則檔：

- **基底檔案**，其中包含大部分的 hello 定義以及 Azure 提供完整的範例。  我們建議您讓 toothis 檔案 toohelp 疑難排解之後，變更最小的數目和長期維護您的原則
- **擴充檔**保存 hello 唯一的組態變更為您的租用戶
- **信賴憑證者的合作對象 (RP) 檔案**即 hello 單一工作為主的檔案直接所 hello 應用程式或服務 （也稱為信賴憑證者合作對象） 叫用。  如需詳細資訊的原則檔案定義上的讀取 hello 文章。  每個唯一的工作需要自己 RP 並根據商標需求 hello 數目可能是"x 使用案例的總數的應用程式的總計 」。

![原則檔類型](media/active-directory-b2c-overview-custom/active-directory-b2c-overview-custom-policy-files.png)

| 原則檔類型 | 範例檔案名稱 | 建議使用 | 繼承自 |
|---------------------|--------------------|-----------------|---------------|
| 基底 |TrustFrameworkBase.xml<br><br>Mytenant.onmicrosoft.com-B2C-1A_BASE1.xml | 包含 hello 核心宣告結構描述、 宣告轉換，宣告提供者，以及 Microsoft 所設定的使用者皆<br><br>幾乎不需要變更 toothis 檔案 | None |
| 擴充 (EXT) | TrustFrameworkExtensions.xml<br><br>Mytenant.onmicrosoft.com-B2C-1A_EXT.xml | 合併您的變更 toohello 基底檔案，請前往<br><br>已修改的宣告提供者<br><br>已修改的使用者旅程圖<br><br>您自己的自訂結構描述定義 | 基底檔案 |
| 信賴憑證者 (RP) | B2C_1A_sign_up_sign_in.xml| 在此變更權杖圖形和工作階段設定| Extensions(EXT) 檔案 |

### <a name="inheritance-model"></a>繼承模型

當應用程式呼叫 hello RP 原則檔時，hello B2C 中的身分識別體驗架構就會從基底，然後在擴充功能，加入 hello 的所有項目，以及最後從 hello RP 原則檔案 tooassemble 中 hello 作用中 目前的原則。  Hello 相同類型和名稱 hello RP 檔案中的項目將會覆寫在 hello 擴充功能，並且延伸模組會覆寫基底。

**內建原則**在 Azure AD B2C 遵循 hello 3 檔案模式所描述之以上版本，但 hello 開發人員只看到 hello 信賴憑證者的合作對象 (RP) 檔案，而 hello 入口網站在 hello 背景 toohello EXTenstions 檔案進行的變更。  所有的 Azure AD B2C 共用控制權 hello Azure B2C 小組的 hello 且經常更新的基底原則檔案。
