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
# <a name="branding-guidelines-for-applications"></a><span data-ttu-id="049a5-103">應用程式的商標指導方針</span><span class="sxs-lookup"><span data-stu-id="049a5-103">Branding Guidelines for Applications</span></span>
<span data-ttu-id="049a5-104">本主題討論 hello 的商標的指導開發與 Azure Active Directory (Azure AD) 的應用程式時，您應該使用。</span><span class="sxs-lookup"><span data-stu-id="049a5-104">This topic discusses hello branding guidelines you should use when developing applications with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="049a5-105">這些指導方針可協助您的客戶時想要 toouse 其工作或學校帳戶，在 Azure AD 中管理或個人帳戶的註冊和登入 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="049a5-105">These guidelines will help direct your customers when they want toouse their work or school account, managed in Azure AD, or their personal account for sign-up and sign-in tooyour application.</span></span>

## <a name="personal-accounts-vs-work-or-school-accounts-from-microsoft"></a><span data-ttu-id="049a5-106">個人帳戶與 Microsoft 提供的工作或學校帳戶的比較</span><span class="sxs-lookup"><span data-stu-id="049a5-106">Personal accounts vs. work or school accounts from Microsoft</span></span>
<span data-ttu-id="049a5-107">Microsoft 管理兩種類型的使用者帳戶：</span><span class="sxs-lookup"><span data-stu-id="049a5-107">Microsoft manages two kinds of user accounts:</span></span>

* <span data-ttu-id="049a5-108">**個人帳戶** (之前稱為 Windows Live ID)。</span><span class="sxs-lookup"><span data-stu-id="049a5-108">**Personal accounts** (formerly known as Windows Live ID).</span></span> <span data-ttu-id="049a5-109">這些帳戶代表 hello 之間的關聯性*個別*使用者和 Microsoft，並使用 tooaccess 消費者裝置與 Microsoft 服務。</span><span class="sxs-lookup"><span data-stu-id="049a5-109">These accounts represent hello relationship between *individual* users and Microsoft, and are used tooaccess consumer devices and services from Microsoft.</span></span> <span data-ttu-id="049a5-110">這些帳戶主要供個人使用。</span><span class="sxs-lookup"><span data-stu-id="049a5-110">These accounts are intended for personal use.</span></span>
* <span data-ttu-id="049a5-111">**工作或學校帳戶。**</span><span class="sxs-lookup"><span data-stu-id="049a5-111">**Work or school accounts.**</span></span> <span data-ttu-id="049a5-112">這些是使用 Azure Active Directory 的組織交由 Microsoft 代為管理的帳戶。</span><span class="sxs-lookup"><span data-stu-id="049a5-112">These accounts are managed by Microsoft on behalf of organizations that use Azure Active Directory.</span></span> <span data-ttu-id="049a5-113">這些帳戶設定為使用的 toosign tooOffice 365 和 Microsoft 其他商務服務中。</span><span class="sxs-lookup"><span data-stu-id="049a5-113">These accounts are used toosign in tooOffice 365 and other business services from Microsoft.</span></span>

<span data-ttu-id="049a5-114">Microsoft 工作或學校帳戶通常是由組織 （公司、 學校、 政府機關） 指派 tooend 使用者 （員工、 學生、 聯邦員工）。</span><span class="sxs-lookup"><span data-stu-id="049a5-114">Microsoft work or school accounts are typically assigned tooend users (employees, students, federal employees) by their organizations (company, school, government agency).</span></span> <span data-ttu-id="049a5-115">這些帳戶設定為直接在 hello Azure AD 的平台或從內部部署目錄，例如 Windows Server Active Directory 的同步處理的 tooAzure AD 中的 hello 雲端中是主要屬性。</span><span class="sxs-lookup"><span data-stu-id="049a5-115">These accounts are either mastered directly in hello cloud, in hello Azure AD platform, or synced tooAzure AD from an on-premises directory, such as Windows Server Active Directory.</span></span> <span data-ttu-id="049a5-116">Microsoft 為 hello*保管者*hello 工作或學校帳戶，但 hello 擁有和控制 hello 組織帳戶。</span><span class="sxs-lookup"><span data-stu-id="049a5-116">Microsoft is hello *custodian* of hello work or school accounts, but hello accounts are owned and controlled by hello organization.</span></span>

## <a name="referring-tooazure-ad-accounts-in-your-application"></a><span data-ttu-id="049a5-117">在您的應用程式的轉介 tooAzure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="049a5-117">Referring tooAzure AD accounts in your application</span></span>
<span data-ttu-id="049a5-118">Microsoft 不會公開使用者 toohello Azure hello Active Directory 商標名稱，或兩者都不應該您。</span><span class="sxs-lookup"><span data-stu-id="049a5-118">Microsoft doesn’t expose end-users toohello Azure or hello Active Directory brand names, and neither should you.</span></span>

* <span data-ttu-id="049a5-119">一旦使用者登入，您應該使用 hello 組織的名稱和最大的標誌。</span><span class="sxs-lookup"><span data-stu-id="049a5-119">Once users are signed in, you should use hello organization’s name and logo as much as possible.</span></span> <span data-ttu-id="049a5-120">這比使用「您的組織」之類的通稱更好。</span><span class="sxs-lookup"><span data-stu-id="049a5-120">This is better than using generic terms like “your organization”.</span></span>
* <span data-ttu-id="049a5-121">當使用者未登入時，您應該參閱 tootheir 帳戶做為 「 工作或學校帳戶 」 和使用 hello Microsoft 標誌 tooconvey 這些帳戶由 Microsoft 管理。</span><span class="sxs-lookup"><span data-stu-id="049a5-121">When users are not signed in, you should refer tootheir accounts as “Work or school accounts” and use hello Microsoft logo tooconvey that these accounts are managed by Microsoft.</span></span> <span data-ttu-id="049a5-122">請勿使用「企業帳戶」、「商務帳戶」或「公司帳戶」之類的詞彙，這會造成使用者混淆。</span><span class="sxs-lookup"><span data-stu-id="049a5-122">Don’t use terms like “enterprise account”, “business account” or “corporate account” which create user confusion.</span></span>

## <a name="user-account-pictogram"></a><span data-ttu-id="049a5-123">使用者帳戶象形圖</span><span class="sxs-lookup"><span data-stu-id="049a5-123">User account pictogram</span></span>
<span data-ttu-id="049a5-124">在這些指導方針的較早版本中，我們建議使用「藍色徽章」象形圖。</span><span class="sxs-lookup"><span data-stu-id="049a5-124">In an earlier version of these guidelines, we recommended using a “blue badge” pictogram.</span></span> <span data-ttu-id="049a5-125">根據使用者和開發人員的意見反應，現在建議 hello 使用 hello Microsoft 標誌。</span><span class="sxs-lookup"><span data-stu-id="049a5-125">Based on user and developer feedback, we now recommend hello use of hello Microsoft logo instead.</span></span> <span data-ttu-id="049a5-126">這可協助使用者瞭解他們可以重複使用他們用於 Office 365 或其他 Microsoft 商業服務 toosign 的 tooyour 應用程式中的 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="049a5-126">This will help users understand that they can reuse hello account they use with Office 365 or other Microsoft business services toosign in tooyour app.</span></span>

## <a name="signing-up-and-signing-in-with-azure-ad"></a><span data-ttu-id="049a5-127">使用 Azure AD 來註冊和登入</span><span class="sxs-lookup"><span data-stu-id="049a5-127">Signing up and signing in with Azure AD</span></span>
<span data-ttu-id="049a5-128">您的應用程式可能會呈現不同的路徑，來註冊和登入，並 hello 下列各節提供這兩種案例的視覺化導引。</span><span class="sxs-lookup"><span data-stu-id="049a5-128">Your app may present separate paths for sign-up and sign-in and hello following sections provide visual guidance for both scenarios.</span></span>

<span data-ttu-id="049a5-129">**如果您的應用程式支援 （例如免費 tootrial 或 freemium 模型） 的終端使用者註冊**： 您可以顯示**登入**按鈕可讓使用者 tooaccess 應用程式與自己的工作帳戶或個人帳戶。</span><span class="sxs-lookup"><span data-stu-id="049a5-129">**If your app supports end user sign up (e.g. free tootrial or freemium model)**: You can show a **sign-in** button that allows users tooaccess your app with their work account or their personal account.</span></span> <span data-ttu-id="049a5-130">Azure AD 將會顯示同意提示 hello 他們存取您的應用程式的第一次。</span><span class="sxs-lookup"><span data-stu-id="049a5-130">Azure AD will show a consent prompt hello first time they access your app.</span></span>

<span data-ttu-id="049a5-131">**如果您的應用程式需要唯有系統管理員才能同意的權限，或您的應用程式需要組織授權**：您應該將系統管理員擷取與使用者登入分開。</span><span class="sxs-lookup"><span data-stu-id="049a5-131">**If your app requires permissions that only admins can consent to, or if your app requires organizational licensing**: You should separate admin acquisition from user sign in.</span></span> <span data-ttu-id="049a5-132">hello **「 取得此應用程式 」 按鈕**會重新導向 admins toosign 中的並要求他們 toogrant 代表其組織中使用者的同意。</span><span class="sxs-lookup"><span data-stu-id="049a5-132">hello **“get this app” button** will redirect admins toosign in then ask them toogrant consent on behalf of users in their organization.</span></span> <span data-ttu-id="049a5-133">這有 hello 歸併終端使用者同意提示 tooyour 應用程式的好處。</span><span class="sxs-lookup"><span data-stu-id="049a5-133">This has hello added benefit of suppressing end users consent prompts tooyour app.</span></span>

## <a name="visual-guidance-for-app-acquisition"></a><span data-ttu-id="049a5-134">取得應用程式的視覺化導引</span><span class="sxs-lookup"><span data-stu-id="049a5-134">Visual guidance for app acquisition</span></span>
<span data-ttu-id="049a5-135">您 「 取得 hello 應用程式 」 的連結，必須重新導向 hello 使用者 toohello Azure AD 授與存取權 （授權） 頁面、 tooallow 組織的系統管理員 tooauthorize 應用程式 toohave 存取由 Microsoft 主控的 tootheir 組織的資料。</span><span class="sxs-lookup"><span data-stu-id="049a5-135">Your “get hello app” link must redirect hello user toohello Azure AD grant access (authorize) page, tooallow an organization’s administrator tooauthorize your app toohave access tootheir organization’s data that is hosted by Microsoft.</span></span> <span data-ttu-id="049a5-136">有關 toorequest 存取 hello 的會討論[整合應用程式與 Azure Active Directory](active-directory-integrating-applications.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="049a5-136">Details on how toorequest access are discussed in hello [Integrating Applications with Azure Active Directory](active-directory-integrating-applications.md) article.</span></span>

<span data-ttu-id="049a5-137">系統管理員同意 tooyour 應用程式之後，他們可以選擇 tooadd 它 tootheir 使用者的 Office 365 應用程式啟動器體驗 (從 hello waffle 和可存取[https://portal.office.com/myapps](https://portal.office.com/myapps))。</span><span class="sxs-lookup"><span data-stu-id="049a5-137">After admins consent tooyour app, they can choose tooadd it tootheir users’ Office 365 app launcher experience (accessible from hello waffle and from [https://portal.office.com/myapps](https://portal.office.com/myapps)).</span></span> <span data-ttu-id="049a5-138">如果您想 tooadvertise 這項功能，您可以使用詞彙的 「 新增此應用程式 tooyour 組織 」，然後再顯示類似的按鈕：</span><span class="sxs-lookup"><span data-stu-id="049a5-138">If you want tooadvertise this capability, you can use terms like “Add this app tooyour organization” and show a button like this:</span></span>

![應用程式類型和案例](./media/active-directory-branding-guidelines/add-to-my-org.png)

<span data-ttu-id="049a5-140">不過，我們建議您撰寫說明文字，而不要依賴按鈕。</span><span class="sxs-lookup"><span data-stu-id="049a5-140">However, we recommend that you write explanatory text instead of relying on buttons.</span></span> <span data-ttu-id="049a5-141">例如：</span><span class="sxs-lookup"><span data-stu-id="049a5-141">For example:</span></span>

> <span data-ttu-id="049a5-142">*如果您已經使用 Office 365 或 microsoft 其他商務服務，您可以只授與 < your_app_name > 存取 tooyour 組織的資料。這可讓您使用其現有的工作帳戶的使用者 tooaccess < your_app_name >。*</span><span class="sxs-lookup"><span data-stu-id="049a5-142">*If you already use Office 365 or other business service from Microsoft, you can simply grant <your_app_name> access tooyour organization’s data. This will allow your users tooaccess <your_app_name> with their existing work accounts.*</span></span>
> 
> 

## <a name="visual-guidance-for-sign-in"></a><span data-ttu-id="049a5-143">登入的視覺化導引</span><span class="sxs-lookup"><span data-stu-id="049a5-143">Visual guidance for sign-in</span></span>
<span data-ttu-id="049a5-144">您的應用程式應該會顯示登在重新導向使用者 toohello 登入對應端點 toohello 通訊協定 toointegrate 搭配 Azure AD 的按鈕。</span><span class="sxs-lookup"><span data-stu-id="049a5-144">Your app should display a sign in button that redirects users toohello sign-in endpoint that corresponds toohello protocol you use toointegrate with Azure AD.</span></span> <span data-ttu-id="049a5-145">下列章節的 hello 提供該按鈕應該看起來詳細資料。</span><span class="sxs-lookup"><span data-stu-id="049a5-145">hello following section provides details on what that button should look like.</span></span>

### <a name="pictogram-and-sign-in-with-microsoft"></a><span data-ttu-id="049a5-146">象形圖和「使用 Microsoft 帳戶登入」</span><span class="sxs-lookup"><span data-stu-id="049a5-146">Pictogram and “Sign in with Microsoft”</span></span>
<span data-ttu-id="049a5-147">它的唯一代表 Azure AD 從您的應用程式可能支援其他身分識別提供者的 hello 關聯的 hello Microsoft 標誌和 hello"符號在 with Microsoft"詞彙。</span><span class="sxs-lookup"><span data-stu-id="049a5-147">It’s hello association of hello Microsoft logo and hello “Sign in with Microsoft” terms that uniquely represents Azure AD amongst other identity providers your app may support.</span></span> <span data-ttu-id="049a5-148">如果您沒有足夠的空間的 「 登在 with Microsoft 」，則確定 tooshorten 它太 「 登入 」。</span><span class="sxs-lookup"><span data-stu-id="049a5-148">If you don’t have enough space for “Sign in with Microsoft,” it’s ok tooshorten it too“Sign in”.</span></span>

![應用程式類型和案例](./media/active-directory-branding-guidelines/sign-in-with-microsoft-light.png)

![應用程式類型和案例](./media/active-directory-branding-guidelines/sign-in-light.png)

<span data-ttu-id="049a5-151">您也可以使用深色色彩配置 hello 按鈕。</span><span class="sxs-lookup"><span data-stu-id="049a5-151">You can also use a dark color scheme for hello buttons.</span></span>

![應用程式類型和案例](./media/active-directory-branding-guidelines/sign-in-with-microsoft-dark.png)

![應用程式類型和案例](./media/active-directory-branding-guidelines/sign-in-dark.png)

## <a name="branding-dos-and-donts"></a><span data-ttu-id="049a5-154">商標的建議與禁忌</span><span class="sxs-lookup"><span data-stu-id="049a5-154">Branding Do’s and Don’ts</span></span>
<span data-ttu-id="049a5-155">**請勿**使用搭配 hello"符號在 with Microsoft"按鈕 tooprovide 附加說明 toohelp 使用者的 「 工作或學校帳戶 」 會辨識是否可以使用它。</span><span class="sxs-lookup"><span data-stu-id="049a5-155">**DO** use “work or school account” in combination with hello "Sign in with Microsoft" button tooprovide additional explanation toohelp end-users recognize whether they can use it.</span></span> <span data-ttu-id="049a5-156">**禁止** 使用「企業帳戶」、「商務帳戶」或「公司帳戶」之類的其他詞彙。</span><span class="sxs-lookup"><span data-stu-id="049a5-156">**DON’T** use other terms such as “enterprise account”, “business account” or “corporate account.”</span></span>

<span data-ttu-id="049a5-157">**禁止** 使用 "Office 365 ID" 或 "Azure ID"。</span><span class="sxs-lookup"><span data-stu-id="049a5-157">**DON’T** use “Office 365 ID” or “Azure ID”.</span></span> <span data-ttu-id="049a5-158">Office 365 也是 hello 取用者來自 Microsoft 不使用 Azure AD 進行驗證的供應項目名稱。</span><span class="sxs-lookup"><span data-stu-id="049a5-158">Office 365 is also hello name of a consumer offering from Microsoft which doesn’t use Azure AD for authentication.</span></span>

<span data-ttu-id="049a5-159">**不要**alter hello Microsoft 標誌。</span><span class="sxs-lookup"><span data-stu-id="049a5-159">**DON’T** alter hello Microsoft logo.</span></span>

<span data-ttu-id="049a5-160">**不要**公開使用者 toohello Azure 或 Active Directory 品牌。</span><span class="sxs-lookup"><span data-stu-id="049a5-160">**DON’T** expose end-users toohello Azure or Active Directory brands.</span></span> <span data-ttu-id="049a5-161">然而 toouse 這些詞彙與開發人員、 IT 專業人員和系統管理員。</span><span class="sxs-lookup"><span data-stu-id="049a5-161">It’s ok however toouse these terms with developers, IT pros and admins.</span></span>

## <a name="navigation-dos-and-donts"></a><span data-ttu-id="049a5-162">導覽的建議與禁忌</span><span class="sxs-lookup"><span data-stu-id="049a5-162">Navigation Do’s and Don’ts</span></span>
<span data-ttu-id="049a5-163">**請勿**提供一種使用者 toosign 出，並切換 tooanother 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="049a5-163">**DO** provide a way for users toosign out and switch tooanother user account.</span></span> <span data-ttu-id="049a5-164">雖然大部分的人只有一個 Microsoft/Facebook/Google/Twitter 個人帳戶，但往往與多個組織相關聯。</span><span class="sxs-lookup"><span data-stu-id="049a5-164">While most people have a single personal account from Microsoft/Facebook/Google/Twitter, people are often associated with more than one organization.</span></span> <span data-ttu-id="049a5-165">我們即將支援多重登入使用者。</span><span class="sxs-lookup"><span data-stu-id="049a5-165">Support for multiple signed-in users is coming soon.</span></span>

