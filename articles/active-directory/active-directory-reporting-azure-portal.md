---
title: "Azure Active Directory 報告 | Microsoft Docs"
description: "提供 Azure Active Directory 報告的一般概觀。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 6141a333-38db-478a-927e-526f1e7614f4
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 738c8f4a56586b87f03973ec258b0a3023affa60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-reporting"></a><span data-ttu-id="3a1d4-103">Azure Active Directory 報告</span><span class="sxs-lookup"><span data-stu-id="3a1d4-103">Azure Active Directory reporting</span></span>

<span data-ttu-id="3a1d4-104">透過 Azure Active Directory 報告，您可以深入了解環境的運作情況。</span><span class="sxs-lookup"><span data-stu-id="3a1d4-104">With Azure Active Directory reporting, you can gain insights into how your environment is doing.</span></span>  
<span data-ttu-id="3a1d4-105">提供的資料可讓您：</span><span class="sxs-lookup"><span data-stu-id="3a1d4-105">The provided data enables you to:</span></span>

- <span data-ttu-id="3a1d4-106">判斷使用者如何利用您的應用程式和服務</span><span class="sxs-lookup"><span data-stu-id="3a1d4-106">Determine how your apps and services are utilized by your users</span></span>
- <span data-ttu-id="3a1d4-107">偵測會影響環境健康情況的潛在風險</span><span class="sxs-lookup"><span data-stu-id="3a1d4-107">Detect potential risks affecting the health of your environment</span></span>
- <span data-ttu-id="3a1d4-108">針對會阻止使用者完成其工作的問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="3a1d4-108">Troubleshoot issues preventing your users from getting their work done</span></span>  

<span data-ttu-id="3a1d4-109">報告架構依賴兩大主要支柱：</span><span class="sxs-lookup"><span data-stu-id="3a1d4-109">The reporting architecture relies on two main pillars:</span></span>

- <span data-ttu-id="3a1d4-110">安全性報告</span><span class="sxs-lookup"><span data-stu-id="3a1d4-110">Security reports</span></span>
- <span data-ttu-id="3a1d4-111">活動報告</span><span class="sxs-lookup"><span data-stu-id="3a1d4-111">Activity reports</span></span>

![報告](./media/active-directory-reporting-azure-portal/01.png)



## <a name="security-reports"></a><span data-ttu-id="3a1d4-113">安全性報告</span><span class="sxs-lookup"><span data-stu-id="3a1d4-113">Security reports</span></span>

<span data-ttu-id="3a1d4-114">Azure Active Directory 中的安全性報告可協助您保護貴組織的身分識別。</span><span class="sxs-lookup"><span data-stu-id="3a1d4-114">The security reports in Azure Active Directory help you to protect your organization's identities.</span></span>  
<span data-ttu-id="3a1d4-115">Azure Active Directory 中有兩種安全性報告：</span><span class="sxs-lookup"><span data-stu-id="3a1d4-115">There are two types of security reports in Azure Active Directory:</span></span>

- <span data-ttu-id="3a1d4-116">**標幟為有風險的使用者** - 從[有風險的使用者安全性報告](active-directory-reporting-security-user-at-risk.md)，取得可能受危害之使用者帳戶的概觀。</span><span class="sxs-lookup"><span data-stu-id="3a1d4-116">**Users flagged for risk** - From the [users flagged for risk security report](active-directory-reporting-security-user-at-risk.md), you get an overview of user accounts that might have been compromised.</span></span>

- <span data-ttu-id="3a1d4-117">**有風險的登入** - 透過[有風險的登入安全性報告](active-directory-reporting-security-risky-sign-ins.md)，取得非使用者帳戶合法擁有者的某人嘗試登入的指示器。</span><span class="sxs-lookup"><span data-stu-id="3a1d4-117">**Risky sign-ins** - With the [risky sign-in security report](active-directory-reporting-security-risky-sign-ins.md), you get an indicator for sign-in attempts that might have been performed by someone who is not the legitimate owner of a user account.</span></span> 

<span data-ttu-id="3a1d4-118">**您需要哪項 Azure AD 授權才能存取安全性報告？**</span><span class="sxs-lookup"><span data-stu-id="3a1d4-118">**What Azure AD license do you need to access a security report?**</span></span>  
<span data-ttu-id="3a1d4-119">所有 Azure Active Directory 版本都可提供標幟為有風險的使用者和有風險的登入報告。</span><span class="sxs-lookup"><span data-stu-id="3a1d4-119">All editions of Azure Active Directory provide you with users flagged for risk and risky sign-ins reports.</span></span>  
<span data-ttu-id="3a1d4-120">不過，報告細微性層級因版本而異：</span><span class="sxs-lookup"><span data-stu-id="3a1d4-120">However, the level of report granularity varies between the editions:</span></span> 

- <span data-ttu-id="3a1d4-121">在 [Azure Active Directory Free 和 Basic 版本] 中，您已取得標幟為有風險的使用者和有風險的登入清單。</span><span class="sxs-lookup"><span data-stu-id="3a1d4-121">In the **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk and risky sign-ins.</span></span> 

- <span data-ttu-id="3a1d4-122">**Azure Active Directory Premium 1** 版本也可讓您檢查每份報告部分已偵測到的基礎風險事件，藉此擴充此模型。</span><span class="sxs-lookup"><span data-stu-id="3a1d4-122">The **Azure Active Directory Premium 1** edition extends this model by also enabling you to examine some of the underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="3a1d4-123">**Azure Active Directory Premium 2** 版本可提供有關基礎風險事件的最詳細資訊，也可讓您設定安全性原則，自動回應已設定的風險層級。</span><span class="sxs-lookup"><span data-stu-id="3a1d4-123">The **Azure Active Directory Premium 2** edition provides you with the most detailed information about the underlying risk events and it also enables you to configure security policies that automatically respond to configured risk levels.</span></span>


## <a name="activity-reports"></a><span data-ttu-id="3a1d4-124">活動報告</span><span class="sxs-lookup"><span data-stu-id="3a1d4-124">Activity reports</span></span>

<span data-ttu-id="3a1d4-125">Azure Active Directory 中有兩種活動報告：</span><span class="sxs-lookup"><span data-stu-id="3a1d4-125">There are two types of activity reports in Azure Active Directory:</span></span>

- <span data-ttu-id="3a1d4-126">**稽核記錄** - [稽核記錄活動報告](active-directory-reporting-activity-audit-logs.md)可供您存取在租用戶中執行之每個工作的歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="3a1d4-126">**Audit logs** - The [audit logs activity report](active-directory-reporting-activity-audit-logs.md) provides you with access to the history of every task performed in your tenant.</span></span>

- <span data-ttu-id="3a1d4-127">**登入** - 透過[登入活動報告](active-directory-reporting-activity-sign-ins.md)，您可以判斷已執行稽核記錄報告所報告之工作的人員。</span><span class="sxs-lookup"><span data-stu-id="3a1d4-127">**Sign-ins** -  With the [sign-ins activity report](active-directory-reporting-activity-sign-ins.md), you can determine, who has performed the tasks reported by the audit logs report.</span></span>



<span data-ttu-id="3a1d4-128">**稽核記錄報告**會提供系統活動記錄以達到合規性。</span><span class="sxs-lookup"><span data-stu-id="3a1d4-128">The **audit logs report** provides you with records of system activities for compliance.</span></span>
<span data-ttu-id="3a1d4-129">此外，所提供的資料可讓您解決常見的案例，例如：</span><span class="sxs-lookup"><span data-stu-id="3a1d4-129">Amongst others, the provided data enables you to address common scenarios such as:</span></span>

- <span data-ttu-id="3a1d4-130">我的租用戶中有人已取得系統管理員群組的存取權。</span><span class="sxs-lookup"><span data-stu-id="3a1d4-130">Someone in my tenant got access to an admin group.</span></span> <span data-ttu-id="3a1d4-131">誰提供存取權給他們？</span><span class="sxs-lookup"><span data-stu-id="3a1d4-131">Who gave them access?</span></span> 

- <span data-ttu-id="3a1d4-132">我想要知道登入特定應用程式的使用者清單，因為我最近將應用程式上架而且想知道其運作情況</span><span class="sxs-lookup"><span data-stu-id="3a1d4-132">I want to know the list of users signing into a specific app since I recently onboarded the app and want to know if it’s doing well</span></span>

- <span data-ttu-id="3a1d4-133">我想要知道我的租用戶中發生多少次密碼重設</span><span class="sxs-lookup"><span data-stu-id="3a1d4-133">I want to know how many password resets are happening in my tenant</span></span>


<span data-ttu-id="3a1d4-134">**您需要哪項 Azure AD 授權才能存取稽核記錄報告？**</span><span class="sxs-lookup"><span data-stu-id="3a1d4-134">**What Azure AD license do you need to access the audit logs report?**</span></span>  
<span data-ttu-id="3a1d4-135">稽核記錄報告可用於您擁有授權的功能。</span><span class="sxs-lookup"><span data-stu-id="3a1d4-135">The audit logs report is available for features for which you have licenses.</span></span> <span data-ttu-id="3a1d4-136">如果您有特定功能的授權，也可以存取其稽核記錄資訊。</span><span class="sxs-lookup"><span data-stu-id="3a1d4-136">If you have a license for a specific feature, you also have access to the audit log information for it.</span></span>

<span data-ttu-id="3a1d4-137">如需詳細資訊，請參閱 [Azure Active Directory 功能](https://www.microsoft.com/cloud-platform/azure-active-directory-features)中的**比較 Free、Basic 和 Premium 版本的正式推出功能**。</span><span class="sxs-lookup"><span data-stu-id="3a1d4-137">For more details, see **Comparing generally available features of the Free, Basic, and Premium editions** in [Azure Active Directory features and capabilities](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span></span>   



<span data-ttu-id="3a1d4-138">**登入活動報告**可讓您尋找以下問題的解答，例如：</span><span class="sxs-lookup"><span data-stu-id="3a1d4-138">The **sign-ins activity report** enables to to find answers to questions such as:</span></span>

- <span data-ttu-id="3a1d4-139">使用者的登入模式為何？</span><span class="sxs-lookup"><span data-stu-id="3a1d4-139">What is the sign-in pattern of a user?</span></span>
- <span data-ttu-id="3a1d4-140">一週內有多少使用者登入？</span><span class="sxs-lookup"><span data-stu-id="3a1d4-140">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="3a1d4-141">這些登入的狀態為何？</span><span class="sxs-lookup"><span data-stu-id="3a1d4-141">What’s the status of these sign-ins?</span></span>


<span data-ttu-id="3a1d4-142">**您需要哪項 Azure AD 授權才能存取登入活動報告？**</span><span class="sxs-lookup"><span data-stu-id="3a1d4-142">**What Azure AD license do you need to access the sign-ins activity report?**</span></span>  
<span data-ttu-id="3a1d4-143">若要存取登入活動報告，租用戶必須有相關聯的 Azure AD Premium 授權。</span><span class="sxs-lookup"><span data-stu-id="3a1d4-143">To access the sign-ins activity report, your tenant must have an Azure AD Premium license associated with it.</span></span>


## <a name="programmatic-access"></a><span data-ttu-id="3a1d4-144">以程式設計方式存取</span><span class="sxs-lookup"><span data-stu-id="3a1d4-144">Programmatic access</span></span>

<span data-ttu-id="3a1d4-145">除了使用者介面，Azure Active Directory 報告也提供[以程式設計方式存取](active-directory-reporting-api-getting-started-azure-portal.md)報告資料。</span><span class="sxs-lookup"><span data-stu-id="3a1d4-145">In addition to the user interface, Azure Active Directory reporting also provides you with [programmatic access](active-directory-reporting-api-getting-started-azure-portal.md) to the reporting data.</span></span> <span data-ttu-id="3a1d4-146">這些報告的資料對您的應用程式 (例如 SIEM 系統、稽核和商業智慧工具) 可能非常有用。</span><span class="sxs-lookup"><span data-stu-id="3a1d4-146">The data of these reports can be very useful to your applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="3a1d4-147">Azure AD 報告 API 透過一組以 REST 為基礎的 API 提供資料的程式設計方式存取。</span><span class="sxs-lookup"><span data-stu-id="3a1d4-147">The Azure AD reporting APIs provide programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="3a1d4-148">您可以從各種程式設計語言和工具呼叫這些 API。</span><span class="sxs-lookup"><span data-stu-id="3a1d4-148">You can call these APIs from a variety of programming languages and tools.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="3a1d4-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3a1d4-149">Next steps</span></span>

<span data-ttu-id="3a1d4-150">如果您想要深入了解 Azure Active Directory 中的各種報告類型，請參閱：</span><span class="sxs-lookup"><span data-stu-id="3a1d4-150">If you want to know more about the various report types in Azure Active Directory, see:</span></span>

- [<span data-ttu-id="3a1d4-151">標幟有風險的使用者報告</span><span class="sxs-lookup"><span data-stu-id="3a1d4-151">Users flagged for risk report</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="3a1d4-152">有風險的登入報告</span><span class="sxs-lookup"><span data-stu-id="3a1d4-152">Risky sign-ins report</span></span>](active-directory-reporting-security-risky-sign-ins.md)
- [<span data-ttu-id="3a1d4-153">稽核記錄報告</span><span class="sxs-lookup"><span data-stu-id="3a1d4-153">Audit logs report</span></span>](active-directory-reporting-activity-audit-logs.md)
- [<span data-ttu-id="3a1d4-154">登入記錄報告</span><span class="sxs-lookup"><span data-stu-id="3a1d4-154">Sign-ins logs report</span></span>](active-directory-reporting-activity-sign-ins.md)

<span data-ttu-id="3a1d4-155">如果您想要深入了解如何使用報告 API 存取報告資料，請參閱：</span><span class="sxs-lookup"><span data-stu-id="3a1d4-155">If you want to know more about accessing the the reporting data using the reporting API, see:</span></span> 

- [<span data-ttu-id="3a1d4-156">透過 Azure Active Directory 報告 API 開始入門</span><span class="sxs-lookup"><span data-stu-id="3a1d4-156">Getting started with the Azure Active Directory reporting API</span></span>](active-directory-reporting-api-getting-started-azure-portal.md)


<!--Image references-->
[1]: ./media/active-directory-reporting-azure-portal/ic195031.png