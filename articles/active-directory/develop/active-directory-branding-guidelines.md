---
title: "應用程式的指導方針 aaaBranding |Microsoft 文件"
description: "完整的 Azure Active Directory 引導 toodeveloper 導向資源"
services: active-directory
documentationcenter: dev-center-name
author: skwan
manager: mbaldwin
editor: 
ms.assetid: 72f4e464-1352-4a49-a18f-c37f58e7d5c4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: skwan
ms.custom: aaddev
ms.openlocfilehash: e43f884c736a0dcb2e6e51293962ef1e2636ad70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="branding-guidelines-for-applications"></a>應用程式的商標指導方針
本主題討論 hello 的商標的指導開發與 Azure Active Directory (Azure AD) 的應用程式時，您應該使用。 這些指導方針可協助您的客戶時想要 toouse 其工作或學校帳戶，在 Azure AD 中管理或個人帳戶的註冊和登入 tooyour 應用程式。

## <a name="personal-accounts-vs-work-or-school-accounts-from-microsoft"></a>個人帳戶與 Microsoft 提供的工作或學校帳戶的比較
Microsoft 管理兩種類型的使用者帳戶：

* **個人帳戶** (之前稱為 Windows Live ID)。 這些帳戶代表 hello 之間的關聯性*個別*使用者和 Microsoft，並使用 tooaccess 消費者裝置與 Microsoft 服務。 這些帳戶主要供個人使用。
* **工作或學校帳戶。** 這些是使用 Azure Active Directory 的組織交由 Microsoft 代為管理的帳戶。 這些帳戶設定為使用的 toosign tooOffice 365 和 Microsoft 其他商務服務中。

Microsoft 工作或學校帳戶通常是由組織 （公司、 學校、 政府機關） 指派 tooend 使用者 （員工、 學生、 聯邦員工）。 這些帳戶設定為直接在 hello Azure AD 的平台或從內部部署目錄，例如 Windows Server Active Directory 的同步處理的 tooAzure AD 中的 hello 雲端中是主要屬性。 Microsoft 為 hello*保管者*hello 工作或學校帳戶，但 hello 擁有和控制 hello 組織帳戶。

## <a name="referring-tooazure-ad-accounts-in-your-application"></a>在您的應用程式的轉介 tooAzure AD 帳戶
Microsoft 不會公開使用者 toohello Azure hello Active Directory 商標名稱，或兩者都不應該您。

* 一旦使用者登入，您應該使用 hello 組織的名稱和最大的標誌。 這比使用「您的組織」之類的通稱更好。
* 當使用者未登入時，您應該參閱 tootheir 帳戶做為 「 工作或學校帳戶 」 和使用 hello Microsoft 標誌 tooconvey 這些帳戶由 Microsoft 管理。 請勿使用「企業帳戶」、「商務帳戶」或「公司帳戶」之類的詞彙，這會造成使用者混淆。

## <a name="user-account-pictogram"></a>使用者帳戶象形圖
在這些指導方針的較早版本中，我們建議使用「藍色徽章」象形圖。 根據使用者和開發人員的意見反應，現在建議 hello 使用 hello Microsoft 標誌。 這可協助使用者瞭解他們可以重複使用他們用於 Office 365 或其他 Microsoft 商業服務 toosign 的 tooyour 應用程式中的 hello 帳戶。

## <a name="signing-up-and-signing-in-with-azure-ad"></a>使用 Azure AD 來註冊和登入
您的應用程式可能會呈現不同的路徑，來註冊和登入，並 hello 下列各節提供這兩種案例的視覺化導引。

**如果您的應用程式支援 （例如免費 tootrial 或 freemium 模型） 的終端使用者註冊**： 您可以顯示**登入**按鈕可讓使用者 tooaccess 應用程式與自己的工作帳戶或個人帳戶。 Azure AD 將會顯示同意提示 hello 他們存取您的應用程式的第一次。

**如果您的應用程式需要唯有系統管理員才能同意的權限，或您的應用程式需要組織授權**：您應該將系統管理員擷取與使用者登入分開。 hello **「 取得此應用程式 」 按鈕**會重新導向 admins toosign 中的並要求他們 toogrant 代表其組織中使用者的同意。 這有 hello 歸併終端使用者同意提示 tooyour 應用程式的好處。

## <a name="visual-guidance-for-app-acquisition"></a>取得應用程式的視覺化導引
您 「 取得 hello 應用程式 」 的連結，必須重新導向 hello 使用者 toohello Azure AD 授與存取權 （授權） 頁面、 tooallow 組織的系統管理員 tooauthorize 應用程式 toohave 存取由 Microsoft 主控的 tootheir 組織的資料。 有關 toorequest 存取 hello 的會討論[整合應用程式與 Azure Active Directory](active-directory-integrating-applications.md)發行項。

系統管理員同意 tooyour 應用程式之後，他們可以選擇 tooadd 它 tootheir 使用者的 Office 365 應用程式啟動器體驗 (從 hello waffle 和可存取[https://portal.office.com/myapps](https://portal.office.com/myapps))。 如果您想 tooadvertise 這項功能，您可以使用詞彙的 「 新增此應用程式 tooyour 組織 」，然後再顯示類似的按鈕：

![應用程式類型和案例](./media/active-directory-branding-guidelines/add-to-my-org.png)

不過，我們建議您撰寫說明文字，而不要依賴按鈕。 例如：

> *如果您已經使用 Office 365 或 microsoft 其他商務服務，您可以只授與 < your_app_name > 存取 tooyour 組織的資料。這可讓您使用其現有的工作帳戶的使用者 tooaccess < your_app_name >。*
> 
> 

## <a name="visual-guidance-for-sign-in"></a>登入的視覺化導引
您的應用程式應該會顯示登在重新導向使用者 toohello 登入對應端點 toohello 通訊協定 toointegrate 搭配 Azure AD 的按鈕。 下列章節的 hello 提供該按鈕應該看起來詳細資料。

### <a name="pictogram-and-sign-in-with-microsoft"></a>象形圖和「使用 Microsoft 帳戶登入」
它的唯一代表 Azure AD 從您的應用程式可能支援其他身分識別提供者的 hello 關聯的 hello Microsoft 標誌和 hello"符號在 with Microsoft"詞彙。 如果您沒有足夠的空間的 「 登在 with Microsoft 」，則確定 tooshorten 它太 「 登入 」。

![應用程式類型和案例](./media/active-directory-branding-guidelines/sign-in-with-microsoft-light.png)

![應用程式類型和案例](./media/active-directory-branding-guidelines/sign-in-light.png)

您也可以使用深色色彩配置 hello 按鈕。

![應用程式類型和案例](./media/active-directory-branding-guidelines/sign-in-with-microsoft-dark.png)

![應用程式類型和案例](./media/active-directory-branding-guidelines/sign-in-dark.png)

## <a name="branding-dos-and-donts"></a>商標的建議與禁忌
**請勿**使用搭配 hello"符號在 with Microsoft"按鈕 tooprovide 附加說明 toohelp 使用者的 「 工作或學校帳戶 」 會辨識是否可以使用它。 **禁止** 使用「企業帳戶」、「商務帳戶」或「公司帳戶」之類的其他詞彙。

**禁止** 使用 "Office 365 ID" 或 "Azure ID"。 Office 365 也是 hello 取用者來自 Microsoft 不使用 Azure AD 進行驗證的供應項目名稱。

**不要**alter hello Microsoft 標誌。

**不要**公開使用者 toohello Azure 或 Active Directory 品牌。 然而 toouse 這些詞彙與開發人員、 IT 專業人員和系統管理員。

## <a name="navigation-dos-and-donts"></a>導覽的建議與禁忌
**請勿**提供一種使用者 toosign 出，並切換 tooanother 使用者帳戶。 雖然大部分的人只有一個 Microsoft/Facebook/Google/Twitter 個人帳戶，但往往與多個組織相關聯。 我們即將支援多重登入使用者。

