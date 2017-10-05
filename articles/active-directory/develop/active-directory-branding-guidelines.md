---
title: "應用程式的商標指導方針 | Microsoft Docs"
description: "Azure Active Directory 開發人員導向資源的完整指南"
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
ms.openlocfilehash: 4f6806cde52ce965a8f78a5cce8a24c3d1248594
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="branding-guidelines-for-applications"></a><span data-ttu-id="6a939-103">應用程式的商標指導方針</span><span class="sxs-lookup"><span data-stu-id="6a939-103">Branding Guidelines for Applications</span></span>
<span data-ttu-id="6a939-104">本主題討論使用 Azure Active Directory (Azure AD) 開發應用程式時，您應該使用的商標指導方針。</span><span class="sxs-lookup"><span data-stu-id="6a939-104">This topic discusses the branding guidelines you should use when developing applications with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="6a939-105">當客戶想要使用其工作或學校帳戶 (在 Azure AD 中管理) 或其個人帳戶來註冊和登入您的應用程式時，這些指導方針可協助引導客戶。</span><span class="sxs-lookup"><span data-stu-id="6a939-105">These guidelines will help direct your customers when they want to use their work or school account, managed in Azure AD, or their personal account for sign-up and sign-in to your application.</span></span>

## <a name="personal-accounts-vs-work-or-school-accounts-from-microsoft"></a><span data-ttu-id="6a939-106">個人帳戶與 Microsoft 提供的工作或學校帳戶的比較</span><span class="sxs-lookup"><span data-stu-id="6a939-106">Personal accounts vs. work or school accounts from Microsoft</span></span>
<span data-ttu-id="6a939-107">Microsoft 管理兩種類型的使用者帳戶：</span><span class="sxs-lookup"><span data-stu-id="6a939-107">Microsoft manages two kinds of user accounts:</span></span>

* <span data-ttu-id="6a939-108">**個人帳戶** (之前稱為 Windows Live ID)。</span><span class="sxs-lookup"><span data-stu-id="6a939-108">**Personal accounts** (formerly known as Windows Live ID).</span></span> <span data-ttu-id="6a939-109">這些帳戶代表 *個別* 使用者和 Microsoft 之間的關聯性，用於存取來自 Microsoft 的消費型裝置和服務。</span><span class="sxs-lookup"><span data-stu-id="6a939-109">These accounts represent the relationship between *individual* users and Microsoft, and are used to access consumer devices and services from Microsoft.</span></span> <span data-ttu-id="6a939-110">這些帳戶主要供個人使用。</span><span class="sxs-lookup"><span data-stu-id="6a939-110">These accounts are intended for personal use.</span></span>
* <span data-ttu-id="6a939-111">**工作或學校帳戶。**</span><span class="sxs-lookup"><span data-stu-id="6a939-111">**Work or school accounts.**</span></span> <span data-ttu-id="6a939-112">這些是使用 Azure Active Directory 的組織交由 Microsoft 代為管理的帳戶。</span><span class="sxs-lookup"><span data-stu-id="6a939-112">These accounts are managed by Microsoft on behalf of organizations that use Azure Active Directory.</span></span> <span data-ttu-id="6a939-113">這些帳戶用來從 Microsoft 登入 Office 365 和其他商務服務。</span><span class="sxs-lookup"><span data-stu-id="6a939-113">These accounts are used to sign in to Office 365 and other business services from Microsoft.</span></span>

<span data-ttu-id="6a939-114">Microsoft 工作或學校帳戶通常由其組織 (公司、 學校、政府機構) 指派給使用者 (員工、學生、聯邦員工)。</span><span class="sxs-lookup"><span data-stu-id="6a939-114">Microsoft work or school accounts are typically assigned to end users (employees, students, federal employees) by their organizations (company, school, government agency).</span></span> <span data-ttu-id="6a939-115">這些帳戶可能直接在雲端中管理 (在 Azure AD 平台)，或從內部部署目錄 (例如 Windows Server Active Directory) 同步處理到 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="6a939-115">These accounts are either mastered directly in the cloud, in the Azure AD platform, or synced to Azure AD from an on-premises directory, such as Windows Server Active Directory.</span></span> <span data-ttu-id="6a939-116">Microsoft 是工作或學校帳戶的 *保管者* ，但這些帳戶由組織擁有和控制。</span><span class="sxs-lookup"><span data-stu-id="6a939-116">Microsoft is the *custodian* of the work or school accounts, but the accounts are owned and controlled by the organization.</span></span>

## <a name="referring-to-azure-ad-accounts-in-your-application"></a><span data-ttu-id="6a939-117">在您的應用程式中提及 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="6a939-117">Referring to Azure AD accounts in your application</span></span>
<span data-ttu-id="6a939-118">Microsoft 不會在 Azure 或 Active Directory 品牌名稱上公開使用者，所以您也不應該如此。</span><span class="sxs-lookup"><span data-stu-id="6a939-118">Microsoft doesn’t expose end-users to the Azure or the Active Directory brand names, and neither should you.</span></span>

* <span data-ttu-id="6a939-119">使用者登入之後，您應該盡可能使用組織的名稱和標誌。</span><span class="sxs-lookup"><span data-stu-id="6a939-119">Once users are signed in, you should use the organization’s name and logo as much as possible.</span></span> <span data-ttu-id="6a939-120">這比使用「您的組織」之類的通稱更好。</span><span class="sxs-lookup"><span data-stu-id="6a939-120">This is better than using generic terms like “your organization”.</span></span>
* <span data-ttu-id="6a939-121">當使用者未登入時，您應該將他們的帳戶稱為「工作或學校帳戶」，並使用 Microsoft 標誌來表達這些帳戶由 Microsoft 管理。</span><span class="sxs-lookup"><span data-stu-id="6a939-121">When users are not signed in, you should refer to their accounts as “Work or school accounts” and use the Microsoft logo to convey that these accounts are managed by Microsoft.</span></span> <span data-ttu-id="6a939-122">請勿使用「企業帳戶」、「商務帳戶」或「公司帳戶」之類的詞彙，這會造成使用者混淆。</span><span class="sxs-lookup"><span data-stu-id="6a939-122">Don’t use terms like “enterprise account”, “business account” or “corporate account” which create user confusion.</span></span>

## <a name="user-account-pictogram"></a><span data-ttu-id="6a939-123">使用者帳戶象形圖</span><span class="sxs-lookup"><span data-stu-id="6a939-123">User account pictogram</span></span>
<span data-ttu-id="6a939-124">在這些指導方針的較早版本中，我們建議使用「藍色徽章」象形圖。</span><span class="sxs-lookup"><span data-stu-id="6a939-124">In an earlier version of these guidelines, we recommended using a “blue badge” pictogram.</span></span> <span data-ttu-id="6a939-125">根據使用者和開發人員的意見反應，我們現在建議改用 Microsoft 標誌。</span><span class="sxs-lookup"><span data-stu-id="6a939-125">Based on user and developer feedback, we now recommend the use of the Microsoft logo instead.</span></span> <span data-ttu-id="6a939-126">這有助於使用者了解，他們用於 Office 365 或其他 Microsoft 商務服務的帳戶，也可以重複用來登入您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6a939-126">This will help users understand that they can reuse the account they use with Office 365 or other Microsoft business services to sign in to your app.</span></span>

## <a name="signing-up-and-signing-in-with-azure-ad"></a><span data-ttu-id="6a939-127">使用 Azure AD 來註冊和登入</span><span class="sxs-lookup"><span data-stu-id="6a939-127">Signing up and signing in with Azure AD</span></span>
<span data-ttu-id="6a939-128">您的應用程式可能將註冊和登入劃分成不同的路徑，下列各節提供這兩個案例的視覺化導引。</span><span class="sxs-lookup"><span data-stu-id="6a939-128">Your app may present separate paths for sign-up and sign-in and the following sections provide visual guidance for both scenarios.</span></span>

<span data-ttu-id="6a939-129">**如果您的應用程式支援使用者註冊 (例如免費試用版或免費增值模式)**：您可以顯示 [登入] 按鈕，讓使用者利用其工作帳戶或個人帳戶來存取您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6a939-129">**If your app supports end user sign up (e.g. free to trial or freemium model)**: You can show a **sign-in** button that allows users to access your app with their work account or their personal account.</span></span> <span data-ttu-id="6a939-130">他們第一次存取您的應用程式時，Azure AD 會顯示同意提示。</span><span class="sxs-lookup"><span data-stu-id="6a939-130">Azure AD will show a consent prompt the first time they access your app.</span></span>

<span data-ttu-id="6a939-131">**如果您的應用程式需要唯有系統管理員才能同意的權限，或您的應用程式需要組織授權**：您應該將系統管理員擷取與使用者登入分開。</span><span class="sxs-lookup"><span data-stu-id="6a939-131">**If your app requires permissions that only admins can consent to, or if your app requires organizational licensing**: You should separate admin acquisition from user sign in.</span></span> <span data-ttu-id="6a939-132">**取得此應用程式 按鈕** 會將系統管理員重新導向登入，然後要求他們代表組織中使用者來表示同意。</span><span class="sxs-lookup"><span data-stu-id="6a939-132">The **“get this app” button** will redirect admins to sign in then ask them to grant consent on behalf of users in their organization.</span></span> <span data-ttu-id="6a939-133">額外的好處是避免您的應用程式顯示使用者同意提示。</span><span class="sxs-lookup"><span data-stu-id="6a939-133">This has the added benefit of suppressing end users consent prompts to your app.</span></span>

## <a name="visual-guidance-for-app-acquisition"></a><span data-ttu-id="6a939-134">取得應用程式的視覺化導引</span><span class="sxs-lookup"><span data-stu-id="6a939-134">Visual guidance for app acquisition</span></span>
<span data-ttu-id="6a939-135">[取得應用程式] 連結必須將使用者重新導向 Azure AD 授與存取權 (授權) 頁面，讓組織的系統管理員可授權您的應用程式來存取由 Microsoft 管理的組織資料。</span><span class="sxs-lookup"><span data-stu-id="6a939-135">Your “get the app” link must redirect the user to the Azure AD grant access (authorize) page, to allow an organization’s administrator to authorize your app to have access to their organization’s data that is hosted by Microsoft.</span></span> <span data-ttu-id="6a939-136">[整合應用程式與 Azure Active Directory](active-directory-integrating-applications.md) 一文中詳細討論存取權的要求方式。</span><span class="sxs-lookup"><span data-stu-id="6a939-136">Details on how to request access are discussed in the [Integrating Applications with Azure Active Directory](active-directory-integrating-applications.md) article.</span></span>

<span data-ttu-id="6a939-137">系統管理員同意您的應用程式之後，他們可以選擇將它加入使用者的 Office 365 應用程式啟動器體驗 (可從非正式管道和 [https://portal.office.com/myapps](https://portal.office.com/myapps)存取)。</span><span class="sxs-lookup"><span data-stu-id="6a939-137">After admins consent to your app, they can choose to add it to their users’ Office 365 app launcher experience (accessible from the waffle and from [https://portal.office.com/myapps](https://portal.office.com/myapps)).</span></span> <span data-ttu-id="6a939-138">如果您想要宣傳這項功能，您可以使用「將此應用程式加入至您的組織」之類的詞彙，並顯示如下的按鈕：</span><span class="sxs-lookup"><span data-stu-id="6a939-138">If you want to advertise this capability, you can use terms like “Add this app to your organization” and show a button like this:</span></span>

![應用程式類型和案例](./media/active-directory-branding-guidelines/add-to-my-org.png)

<span data-ttu-id="6a939-140">不過，我們建議您撰寫說明文字，而不要依賴按鈕。</span><span class="sxs-lookup"><span data-stu-id="6a939-140">However, we recommend that you write explanatory text instead of relying on buttons.</span></span> <span data-ttu-id="6a939-141">例如：</span><span class="sxs-lookup"><span data-stu-id="6a939-141">For example:</span></span>

> <span data-ttu-id="6a939-142">如果您已經使用 Office 365 或 Microsoft 的其他商務服務，您便可以直接授權 <your_app_name> 存取您的組織資料。這可讓使用者利用其現有的工作帳戶存取 <your_app_name>。</span><span class="sxs-lookup"><span data-stu-id="6a939-142">*If you already use Office 365 or other business service from Microsoft, you can simply grant <your_app_name> access to your organization’s data. This will allow your users to access <your_app_name> with their existing work accounts.*</span></span>
> 
> 

## <a name="visual-guidance-for-sign-in"></a><span data-ttu-id="6a939-143">登入的視覺化導引</span><span class="sxs-lookup"><span data-stu-id="6a939-143">Visual guidance for sign-in</span></span>
<span data-ttu-id="6a939-144">您的應用程式應該顯示登入按鈕，將使用者重新導向登入端點，此端點符合您用來與 Azure AD 整合的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="6a939-144">Your app should display a sign in button that redirects users to the sign-in endpoint that corresponds to the protocol you use to integrate with Azure AD.</span></span> <span data-ttu-id="6a939-145">下節提供該按鈕外觀的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6a939-145">The following section provides details on what that button should look like.</span></span>

### <a name="pictogram-and-sign-in-with-microsoft"></a><span data-ttu-id="6a939-146">象形圖和「使用 Microsoft 帳戶登入」</span><span class="sxs-lookup"><span data-stu-id="6a939-146">Pictogram and “Sign in with Microsoft”</span></span>
<span data-ttu-id="6a939-147">結合 Microsoft 標誌與「使用 Microsoft 帳戶登入」詞彙，才能在應用程式可能支援的其他身分識別提供者之中，彰顯 Azure AD 的獨特性。</span><span class="sxs-lookup"><span data-stu-id="6a939-147">It’s the association of the Microsoft logo and the “Sign in with Microsoft” terms that uniquely represents Azure AD amongst other identity providers your app may support.</span></span> <span data-ttu-id="6a939-148">如果沒有足夠的空間顯示「使用 Microsoft 帳戶登入」，可以縮短為「登入」。</span><span class="sxs-lookup"><span data-stu-id="6a939-148">If you don’t have enough space for “Sign in with Microsoft,” it’s ok to shorten it to “Sign in”.</span></span>

![應用程式類型和案例](./media/active-directory-branding-guidelines/sign-in-with-microsoft-light.png)

![應用程式類型和案例](./media/active-directory-branding-guidelines/sign-in-light.png)

<span data-ttu-id="6a939-151">按鈕也可以使用深色配置。</span><span class="sxs-lookup"><span data-stu-id="6a939-151">You can also use a dark color scheme for the buttons.</span></span>

![應用程式類型和案例](./media/active-directory-branding-guidelines/sign-in-with-microsoft-dark.png)

![應用程式類型和案例](./media/active-directory-branding-guidelines/sign-in-dark.png)

## <a name="branding-dos-and-donts"></a><span data-ttu-id="6a939-154">商標的建議與禁忌</span><span class="sxs-lookup"><span data-stu-id="6a939-154">Branding Do’s and Don’ts</span></span>
<span data-ttu-id="6a939-155">**建議** 將「工作或學校帳戶」與「使用 Microsoft 登入」按鈕結合使用，以提供更多說明協助使用者了解是否可使用它。</span><span class="sxs-lookup"><span data-stu-id="6a939-155">**DO** use “work or school account” in combination with the "Sign in with Microsoft" button to provide additional explanation to help end-users recognize whether they can use it.</span></span> <span data-ttu-id="6a939-156">**禁止** 使用「企業帳戶」、「商務帳戶」或「公司帳戶」之類的其他詞彙。</span><span class="sxs-lookup"><span data-stu-id="6a939-156">**DON’T** use other terms such as “enterprise account”, “business account” or “corporate account.”</span></span>

<span data-ttu-id="6a939-157">**禁止** 使用 "Office 365 ID" 或 "Azure ID"。</span><span class="sxs-lookup"><span data-stu-id="6a939-157">**DON’T** use “Office 365 ID” or “Azure ID”.</span></span> <span data-ttu-id="6a939-158">Office 365 也是 Microsoft 提供的消費型產品名稱，並不使用 Azure AD 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="6a939-158">Office 365 is also the name of a consumer offering from Microsoft which doesn’t use Azure AD for authentication.</span></span>

<span data-ttu-id="6a939-159">**禁止** 改變 Microsoft 標誌。</span><span class="sxs-lookup"><span data-stu-id="6a939-159">**DON’T** alter the Microsoft logo.</span></span>

<span data-ttu-id="6a939-160">**禁止** 在 Azure 或 Active Directory 品牌上公開使用者。</span><span class="sxs-lookup"><span data-stu-id="6a939-160">**DON’T** expose end-users to the Azure or Active Directory brands.</span></span> <span data-ttu-id="6a939-161">不過，對於開發人員、IT 專業人員和系統管理員，則可以使用這些詞彙。</span><span class="sxs-lookup"><span data-stu-id="6a939-161">It’s ok however to use these terms with developers, IT pros and admins.</span></span>

## <a name="navigation-dos-and-donts"></a><span data-ttu-id="6a939-162">導覽的建議與禁忌</span><span class="sxs-lookup"><span data-stu-id="6a939-162">Navigation Do’s and Don’ts</span></span>
<span data-ttu-id="6a939-163">**建議** 提供方法讓使用者登出並切換至另一個使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="6a939-163">**DO** provide a way for users to sign out and switch to another user account.</span></span> <span data-ttu-id="6a939-164">雖然大部分的人只有一個 Microsoft/Facebook/Google/Twitter 個人帳戶，但往往與多個組織相關聯。</span><span class="sxs-lookup"><span data-stu-id="6a939-164">While most people have a single personal account from Microsoft/Facebook/Google/Twitter, people are often associated with more than one organization.</span></span> <span data-ttu-id="6a939-165">我們即將支援多重登入使用者。</span><span class="sxs-lookup"><span data-stu-id="6a939-165">Support for multiple signed-in users is coming soon.</span></span>

