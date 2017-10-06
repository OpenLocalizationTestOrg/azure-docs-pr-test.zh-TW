---
title: "aaaAzure Active Directory 條件式存取常見問題集 |Microsoft 文件"
description: "取得 Azure Active Directory 中的條件式存取相關常見問題的解答 toofrequently。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 14f7fc83-f4bb-41bf-b6f1-a9bb97717c34
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: d23acbb01217d7e9717d1a43de1b46a929404118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-faqs"></a><span data-ttu-id="fa5d5-103">Azure Active Directory 條件式存取常見問題集</span><span class="sxs-lookup"><span data-stu-id="fa5d5-103">Azure Active Directory conditional access FAQs</span></span>

## <a name="which-applications-work-with-conditional-access-policies"></a><span data-ttu-id="fa5d5-104">哪些應用程式會使用條件式存取原則？</span><span class="sxs-lookup"><span data-stu-id="fa5d5-104">Which applications work with conditional access policies?</span></span>

<span data-ttu-id="fa5d5-105">如需有關使用條件式存取原則之應用程式的資訊，請參閱[在 Azure Active Directory 中使用條件式存取規則的應用程式和瀏覽器](active-directory-conditional-access-supported-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="fa5d5-105">For information about applications that work with conditional access policies, see [Applications and browsers that use conditional access rules in Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span></span>

## <a name="are-conditional-access-policies-enforced-for-b2b-collaboration-and-guest-users"></a><span data-ttu-id="fa5d5-106">是否會針對 B2B 共同作業與來賓使用者強制套用條件式存取原則？</span><span class="sxs-lookup"><span data-stu-id="fa5d5-106">Are conditional access policies enforced for B2B collaboration and guest users?</span></span>

<span data-ttu-id="fa5d5-107">系統會針對企業對企業 (B2B) 共同作業使用者強制執行原則。</span><span class="sxs-lookup"><span data-stu-id="fa5d5-107">Policies are enforced for business-to-business (B2B) collaboration users.</span></span> <span data-ttu-id="fa5d5-108">不過，在某些情況下，使用者可能不能 toosatisfy hello 原則需求。</span><span class="sxs-lookup"><span data-stu-id="fa5d5-108">However, in some cases, a user might not be able toosatisfy hello policy requirements.</span></span> <span data-ttu-id="fa5d5-109">例如，來賓使用者的組織可能不支援多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="fa5d5-109">For example, a guest user's organization might not support multi-factor authentication.</span></span> 



## <a name="does-a-sharepoint-online-policy-also-apply-tooonedrive-for-business"></a><span data-ttu-id="fa5d5-110">沒有 SharePoint Online 原則也適用於 tooOneDrive 商務嗎？</span><span class="sxs-lookup"><span data-stu-id="fa5d5-110">Does a SharePoint Online policy also apply tooOneDrive for Business?</span></span>

<span data-ttu-id="fa5d5-111">是。</span><span class="sxs-lookup"><span data-stu-id="fa5d5-111">Yes.</span></span> <span data-ttu-id="fa5d5-112">SharePoint Online 原則也適用於 tooOneDrive 商務。</span><span class="sxs-lookup"><span data-stu-id="fa5d5-112">A SharePoint Online policy also applies tooOneDrive for Business.</span></span>


## <a name="why-cant-i-set-a-policy-on-client-apps-like-word-or-outlook"></a><span data-ttu-id="fa5d5-113">為什麼我無法在用戶端應用程式 (例如 Word 或 Outlook) 上設定原則？</span><span class="sxs-lookup"><span data-stu-id="fa5d5-113">Why can’t I set a policy on client apps, like Word or Outlook?</span></span>

<span data-ttu-id="fa5d5-114">條件式存取原則會設定服務的存取需求。</span><span class="sxs-lookup"><span data-stu-id="fa5d5-114">A conditional access policy sets requirements for accessing a service.</span></span> <span data-ttu-id="fa5d5-115">驗證 toothat 服務時，它會強制執行。</span><span class="sxs-lookup"><span data-stu-id="fa5d5-115">It's enforced when authentication toothat service occurs.</span></span> <span data-ttu-id="fa5d5-116">hello 原則未直接在用戶端應用程式上設定。</span><span class="sxs-lookup"><span data-stu-id="fa5d5-116">hello policy is not set directly on a client application.</span></span> <span data-ttu-id="fa5d5-117">而是在用戶端呼叫服務時套用。</span><span class="sxs-lookup"><span data-stu-id="fa5d5-117">Instead, it is applied when a client calls a service.</span></span> <span data-ttu-id="fa5d5-118">例如，在 SharePoint 上設定的原則會套用 tooclients 呼叫 SharePoint。</span><span class="sxs-lookup"><span data-stu-id="fa5d5-118">For example, a policy set on SharePoint applies tooclients calling SharePoint.</span></span> <span data-ttu-id="fa5d5-119">在 Exchange 上設定的原則會套用 tooOutlook。</span><span class="sxs-lookup"><span data-stu-id="fa5d5-119">A policy set on Exchange applies tooOutlook.</span></span>

## <a name="does-a-conditional-access-policy-apply-tooservice-accounts"></a><span data-ttu-id="fa5d5-120">條件式存取原則是否套用 tooservice 帳戶？</span><span class="sxs-lookup"><span data-stu-id="fa5d5-120">Does a conditional access policy apply tooservice accounts?</span></span>

<span data-ttu-id="fa5d5-121">條件式存取原則會套用 tooall 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="fa5d5-121">Conditional access policies apply tooall user accounts.</span></span> <span data-ttu-id="fa5d5-122">這包括作為服務帳戶的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="fa5d5-122">This includes user accounts that are used as service accounts.</span></span> <span data-ttu-id="fa5d5-123">通常，自動執行的服務帳戶無法滿足條件式存取原則的 hello 的需求。</span><span class="sxs-lookup"><span data-stu-id="fa5d5-123">Often, a service account that runs unattended can't satisfy hello requirements of a conditional access policy.</span></span> <span data-ttu-id="fa5d5-124">例如，可能需要多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="fa5d5-124">For example, multi-factor authentication might be required.</span></span> <span data-ttu-id="fa5d5-125">您可以利用條件式存取原則管理設定，將服務帳戶排除在原則之外。</span><span class="sxs-lookup"><span data-stu-id="fa5d5-125">Service accounts can be excluded from a policy by using conditional access policy management settings.</span></span> 

## <a name="are-graph-apis-available-for-configuring-conditional-access-policies"></a><span data-ttu-id="fa5d5-126">是否有提供「圖形 API」來設定條件式存取原則？</span><span class="sxs-lookup"><span data-stu-id="fa5d5-126">Are Graph APIs available for configuring conditional access policies?</span></span>

<span data-ttu-id="fa5d5-127">目前沒有。</span><span class="sxs-lookup"><span data-stu-id="fa5d5-127">Currently, no.</span></span> 

## <a name="what-is-hello-default-exclusion-policy-for-unsupported-device-platforms"></a><span data-ttu-id="fa5d5-128">不支援的裝置平台的 hello 預設排除原則為何？</span><span class="sxs-lookup"><span data-stu-id="fa5d5-128">What is hello default exclusion policy for unsupported device platforms?</span></span>

<span data-ttu-id="fa5d5-129">目前，只會對 iOS 和 Android 裝置的使用者強制執行條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="fa5d5-129">Currently, conditional access policies are selectively enforced on users of iOS and Android devices.</span></span> <span data-ttu-id="fa5d5-130">其他裝置平台上的應用程式，根據預設，不會影響 hello 適用於 iOS 和 Android 裝置的條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="fa5d5-130">Applications on other device platforms are, by default, not affected by hello conditional access policy for iOS and Android devices.</span></span> <span data-ttu-id="fa5d5-131">租用戶系統管理員可以選擇 toooverride hello 全域原則 toodisallow 存取 toousers 不支援的平台上。</span><span class="sxs-lookup"><span data-stu-id="fa5d5-131">A tenant admin can choose toooverride hello global policy toodisallow access toousers on platforms that are not supported.</span></span>


## <a name="how-do-conditional-access-policies-work-for-microsoft-teams"></a><span data-ttu-id="fa5d5-132">條件式存取原則對 Microsoft Teams 有何用途？</span><span class="sxs-lookup"><span data-stu-id="fa5d5-132">How do conditional access policies work for Microsoft Teams?</span></span>  

<span data-ttu-id="fa5d5-133">Microsoft Teams 在核心產能情節中非常依賴 Exchange Online 和 SharePoint Online，例如會議、行事曆和檔案共用。</span><span class="sxs-lookup"><span data-stu-id="fa5d5-133">Microsoft Teams relies heavily on Exchange Online and SharePoint Online for core productivity scenarios, like meetings, calendars, and file sharing.</span></span> <span data-ttu-id="fa5d5-134">當使用者登入時，這些雲端應用程式設定的條件式存取原則會套用 tooMicrosoft 小組。</span><span class="sxs-lookup"><span data-stu-id="fa5d5-134">Conditional access policies that are set for these cloud apps apply tooMicrosoft Teams when a user signs in.</span></span>

<span data-ttu-id="fa5d5-135">在 Azure Active Directory 條件式存取原則中，也支援將 Microsoft Teams 當作個別的雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="fa5d5-135">Microsoft Teams also is supported separately as a cloud app in Azure Active Directory conditional access policies.</span></span> <span data-ttu-id="fa5d5-136">當使用者登入時，憑證授權單位設定原則的雲端應用程式會套用 tooMicrosoft 小組。</span><span class="sxs-lookup"><span data-stu-id="fa5d5-136">Certificate authority policies that are set for a cloud app apply tooMicrosoft Teams when a user signs in.</span></span>

<span data-ttu-id="fa5d5-137">適用於 Windows 和 Mac 的 Microsoft Teams 桌面用戶端支援新式驗證。</span><span class="sxs-lookup"><span data-stu-id="fa5d5-137">Microsoft Teams desktop clients for Windows and Mac support modern authentication.</span></span> <span data-ttu-id="fa5d5-138">新式驗證將登入跨平台根據 hello Azure Active Directory 驗證程式庫 (ADAL) tooMicrosoft Office 用戶端應用程式整合。</span><span class="sxs-lookup"><span data-stu-id="fa5d5-138">Modern authentication brings sign-in based on hello Azure Active Directory Authentication Library (ADAL) tooMicrosoft Office client applications across platforms.</span></span> 
