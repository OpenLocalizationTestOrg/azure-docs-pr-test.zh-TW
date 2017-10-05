---
title: "Azure Active Directory 條件式存取常見問題集 | Microsoft Docs"
description: "取得 Azure Active Directory 條件式存取常見問題集的解答。"
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
ms.openlocfilehash: e9a5af41b08b593e4d97475f29da4e5fe8df7042
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-conditional-access-faqs"></a><span data-ttu-id="63309-103">Azure Active Directory 條件式存取常見問題集</span><span class="sxs-lookup"><span data-stu-id="63309-103">Azure Active Directory conditional access FAQs</span></span>

## <a name="which-applications-work-with-conditional-access-policies"></a><span data-ttu-id="63309-104">哪些應用程式會使用條件式存取原則？</span><span class="sxs-lookup"><span data-stu-id="63309-104">Which applications work with conditional access policies?</span></span>

<span data-ttu-id="63309-105">如需有關使用條件式存取原則之應用程式的資訊，請參閱[在 Azure Active Directory 中使用條件式存取規則的應用程式和瀏覽器](active-directory-conditional-access-supported-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="63309-105">For information about applications that work with conditional access policies, see [Applications and browsers that use conditional access rules in Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span></span>

## <a name="are-conditional-access-policies-enforced-for-b2b-collaboration-and-guest-users"></a><span data-ttu-id="63309-106">是否會針對 B2B 共同作業與來賓使用者強制套用條件式存取原則？</span><span class="sxs-lookup"><span data-stu-id="63309-106">Are conditional access policies enforced for B2B collaboration and guest users?</span></span>

<span data-ttu-id="63309-107">系統會針對企業對企業 (B2B) 共同作業使用者強制執行原則。</span><span class="sxs-lookup"><span data-stu-id="63309-107">Policies are enforced for business-to-business (B2B) collaboration users.</span></span> <span data-ttu-id="63309-108">不過，在某些情況下，使用者可能無法符合原則需求。</span><span class="sxs-lookup"><span data-stu-id="63309-108">However, in some cases, a user might not be able to satisfy the policy requirements.</span></span> <span data-ttu-id="63309-109">例如，來賓使用者的組織可能不支援多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="63309-109">For example, a guest user's organization might not support multi-factor authentication.</span></span> 



## <a name="does-a-sharepoint-online-policy-also-apply-to-onedrive-for-business"></a><span data-ttu-id="63309-110">SharePoint Online 原則也適用於商務用 OneDrive 嗎？</span><span class="sxs-lookup"><span data-stu-id="63309-110">Does a SharePoint Online policy also apply to OneDrive for Business?</span></span>

<span data-ttu-id="63309-111">是。</span><span class="sxs-lookup"><span data-stu-id="63309-111">Yes.</span></span> <span data-ttu-id="63309-112">SharePoint Online 原則也會套用至商務用 OneDrive。</span><span class="sxs-lookup"><span data-stu-id="63309-112">A SharePoint Online policy also applies to OneDrive for Business.</span></span>


## <a name="why-cant-i-set-a-policy-on-client-apps-like-word-or-outlook"></a><span data-ttu-id="63309-113">為什麼我無法在用戶端應用程式 (例如 Word 或 Outlook) 上設定原則？</span><span class="sxs-lookup"><span data-stu-id="63309-113">Why can’t I set a policy on client apps, like Word or Outlook?</span></span>

<span data-ttu-id="63309-114">條件式存取原則會設定服務的存取需求。</span><span class="sxs-lookup"><span data-stu-id="63309-114">A conditional access policy sets requirements for accessing a service.</span></span> <span data-ttu-id="63309-115">在向該服務進行驗證時會強制執行。</span><span class="sxs-lookup"><span data-stu-id="63309-115">It's enforced when authentication to that service occurs.</span></span> <span data-ttu-id="63309-116">原則並不直接在用戶端應用程式上設定，</span><span class="sxs-lookup"><span data-stu-id="63309-116">The policy is not set directly on a client application.</span></span> <span data-ttu-id="63309-117">而是在用戶端呼叫服務時套用。</span><span class="sxs-lookup"><span data-stu-id="63309-117">Instead, it is applied when a client calls a service.</span></span> <span data-ttu-id="63309-118">例如，在 SharePoint 上設定的原則會套用至呼叫 SharePoint 的用戶端。</span><span class="sxs-lookup"><span data-stu-id="63309-118">For example, a policy set on SharePoint applies to clients calling SharePoint.</span></span> <span data-ttu-id="63309-119">在 Exchange 上設定的原則會套用至 Outlook。</span><span class="sxs-lookup"><span data-stu-id="63309-119">A policy set on Exchange applies to Outlook.</span></span>

## <a name="does-a-conditional-access-policy-apply-to-service-accounts"></a><span data-ttu-id="63309-120">是否會對服務帳戶套用條件式存取原則？</span><span class="sxs-lookup"><span data-stu-id="63309-120">Does a conditional access policy apply to service accounts?</span></span>

<span data-ttu-id="63309-121">條件式存取原則會套用至所有使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="63309-121">Conditional access policies apply to all user accounts.</span></span> <span data-ttu-id="63309-122">這包括作為服務帳戶的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="63309-122">This includes user accounts that are used as service accounts.</span></span> <span data-ttu-id="63309-123">通常，自動執行的服務帳戶無法滿足條件式存取原則的需求。</span><span class="sxs-lookup"><span data-stu-id="63309-123">Often, a service account that runs unattended can't satisfy the requirements of a conditional access policy.</span></span> <span data-ttu-id="63309-124">例如，可能需要多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="63309-124">For example, multi-factor authentication might be required.</span></span> <span data-ttu-id="63309-125">您可以利用條件式存取原則管理設定，將服務帳戶排除在原則之外。</span><span class="sxs-lookup"><span data-stu-id="63309-125">Service accounts can be excluded from a policy by using conditional access policy management settings.</span></span> 

## <a name="are-graph-apis-available-for-configuring-conditional-access-policies"></a><span data-ttu-id="63309-126">是否有提供「圖形 API」來設定條件式存取原則？</span><span class="sxs-lookup"><span data-stu-id="63309-126">Are Graph APIs available for configuring conditional access policies?</span></span>

<span data-ttu-id="63309-127">目前沒有。</span><span class="sxs-lookup"><span data-stu-id="63309-127">Currently, no.</span></span> 

## <a name="what-is-the-default-exclusion-policy-for-unsupported-device-platforms"></a><span data-ttu-id="63309-128">對於不支援的裝置平台，預設的排除原則是什麼？</span><span class="sxs-lookup"><span data-stu-id="63309-128">What is the default exclusion policy for unsupported device platforms?</span></span>

<span data-ttu-id="63309-129">目前，只會對 iOS 和 Android 裝置的使用者強制執行條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="63309-129">Currently, conditional access policies are selectively enforced on users of iOS and Android devices.</span></span> <span data-ttu-id="63309-130">根據預設，iOS 和 Android 裝置的條件式存取原則不會影響其他裝置平台上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="63309-130">Applications on other device platforms are, by default, not affected by the conditional access policy for iOS and Android devices.</span></span> <span data-ttu-id="63309-131">租用戶管理員可選擇覆寫全域原則，以禁止不受支援平台上的使用者存取。</span><span class="sxs-lookup"><span data-stu-id="63309-131">A tenant admin can choose to override the global policy to disallow access to users on platforms that are not supported.</span></span>


## <a name="how-do-conditional-access-policies-work-for-microsoft-teams"></a><span data-ttu-id="63309-132">條件式存取原則對 Microsoft Teams 有何用途？</span><span class="sxs-lookup"><span data-stu-id="63309-132">How do conditional access policies work for Microsoft Teams?</span></span>  

<span data-ttu-id="63309-133">Microsoft Teams 在核心產能情節中非常依賴 Exchange Online 和 SharePoint Online，例如會議、行事曆和檔案共用。</span><span class="sxs-lookup"><span data-stu-id="63309-133">Microsoft Teams relies heavily on Exchange Online and SharePoint Online for core productivity scenarios, like meetings, calendars, and file sharing.</span></span> <span data-ttu-id="63309-134">當使用者登入時，對這些雲端應用程式設定的條件式存取原則會套用至 Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="63309-134">Conditional access policies that are set for these cloud apps apply to Microsoft Teams when a user signs in.</span></span>

<span data-ttu-id="63309-135">在 Azure Active Directory 條件式存取原則中，也支援將 Microsoft Teams 當作個別的雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="63309-135">Microsoft Teams also is supported separately as a cloud app in Azure Active Directory conditional access policies.</span></span> <span data-ttu-id="63309-136">當使用者登入時，對雲端應用程式設定的憑證授權單位原則會套用至 Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="63309-136">Certificate authority policies that are set for a cloud app apply to Microsoft Teams when a user signs in.</span></span>

<span data-ttu-id="63309-137">適用於 Windows 和 Mac 的 Microsoft Teams 桌面用戶端支援新式驗證。</span><span class="sxs-lookup"><span data-stu-id="63309-137">Microsoft Teams desktop clients for Windows and Mac support modern authentication.</span></span> <span data-ttu-id="63309-138">新式驗證以 Azure Active Directory 驗證程式庫 (ADAL) 為基礎，支援 Microsoft Office 用戶端應用程式跨平台登入。</span><span class="sxs-lookup"><span data-stu-id="63309-138">Modern authentication brings sign-in based on the Azure Active Directory Authentication Library (ADAL) to Microsoft Office client applications across platforms.</span></span> 