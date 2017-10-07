---
title: "aaaAzure Active Directory 報告 |Microsoft 文件"
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
ms.openlocfilehash: c91813acbdc4b0bfcd164169b0b575accac227d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting"></a><span data-ttu-id="8dc77-103">Azure Active Directory 報告</span><span class="sxs-lookup"><span data-stu-id="8dc77-103">Azure Active Directory reporting</span></span>

<span data-ttu-id="8dc77-104">透過 Azure Active Directory 報告，您可以深入了解環境的運作情況。</span><span class="sxs-lookup"><span data-stu-id="8dc77-104">With Azure Active Directory reporting, you can gain insights into how your environment is doing.</span></span>  
<span data-ttu-id="8dc77-105">提供的 hello 資料可讓您：</span><span class="sxs-lookup"><span data-stu-id="8dc77-105">hello provided data enables you to:</span></span>

- <span data-ttu-id="8dc77-106">判斷使用者如何利用您的應用程式和服務</span><span class="sxs-lookup"><span data-stu-id="8dc77-106">Determine how your apps and services are utilized by your users</span></span>
- <span data-ttu-id="8dc77-107">偵測潛在的風險會影響您環境的 hello 健全狀況</span><span class="sxs-lookup"><span data-stu-id="8dc77-107">Detect potential risks affecting hello health of your environment</span></span>
- <span data-ttu-id="8dc77-108">針對會阻止使用者完成其工作的問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="8dc77-108">Troubleshoot issues preventing your users from getting their work done</span></span>  

<span data-ttu-id="8dc77-109">hello 報告的架構會依賴兩個主要功能：</span><span class="sxs-lookup"><span data-stu-id="8dc77-109">hello reporting architecture relies on two main pillars:</span></span>

- <span data-ttu-id="8dc77-110">安全性報告</span><span class="sxs-lookup"><span data-stu-id="8dc77-110">Security reports</span></span>
- <span data-ttu-id="8dc77-111">活動報告</span><span class="sxs-lookup"><span data-stu-id="8dc77-111">Activity reports</span></span>

![報告](./media/active-directory-reporting-azure-portal/01.png)



## <a name="security-reports"></a><span data-ttu-id="8dc77-113">安全性報告</span><span class="sxs-lookup"><span data-stu-id="8dc77-113">Security reports</span></span>

<span data-ttu-id="8dc77-114">Azure Active Directory 中的 hello 安全性報表可協助您 tooprotect 貴組織的身分識別。</span><span class="sxs-lookup"><span data-stu-id="8dc77-114">hello security reports in Azure Active Directory help you tooprotect your organization's identities.</span></span>  
<span data-ttu-id="8dc77-115">Azure Active Directory 中有兩種安全性報告：</span><span class="sxs-lookup"><span data-stu-id="8dc77-115">There are two types of security reports in Azure Active Directory:</span></span>

- <span data-ttu-id="8dc77-116">**使用者加上旗標的風險**-從 hello[使用者加上旗標的風險安全性報告](active-directory-reporting-security-user-at-risk.md)，取得可能已受到危害的使用者帳戶的概觀。</span><span class="sxs-lookup"><span data-stu-id="8dc77-116">**Users flagged for risk** - From hello [users flagged for risk security report](active-directory-reporting-security-user-at-risk.md), you get an overview of user accounts that might have been compromised.</span></span>

- <span data-ttu-id="8dc77-117">**高風險的登入**-以 hello[危險的登入安全性報告](active-directory-reporting-security-risky-sign-ins.md)，您會取得指標登入嘗試可能會向其他人要求執行不 hello 合法的使用者帳戶的擁有者。</span><span class="sxs-lookup"><span data-stu-id="8dc77-117">**Risky sign-ins** - With hello [risky sign-in security report](active-directory-reporting-security-risky-sign-ins.md), you get an indicator for sign-in attempts that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> 

<span data-ttu-id="8dc77-118">**Azure AD 授權您需要 tooaccess 安全性報表嗎？**</span><span class="sxs-lookup"><span data-stu-id="8dc77-118">**What Azure AD license do you need tooaccess a security report?**</span></span>  
<span data-ttu-id="8dc77-119">所有 Azure Active Directory 版本都可提供標幟為有風險的使用者和有風險的登入報告。</span><span class="sxs-lookup"><span data-stu-id="8dc77-119">All editions of Azure Active Directory provide you with users flagged for risk and risky sign-ins reports.</span></span>  
<span data-ttu-id="8dc77-120">不過，報表資料粒度層級 hello hello 版本而異：</span><span class="sxs-lookup"><span data-stu-id="8dc77-120">However, hello level of report granularity varies between hello editions:</span></span> 

- <span data-ttu-id="8dc77-121">在 [hello **Azure Active Directory Free 和 Basic 版本**，您已取得的加上旗標的風險和風險的登入的使用者清單。</span><span class="sxs-lookup"><span data-stu-id="8dc77-121">In hello **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk and risky sign-ins.</span></span> 

- <span data-ttu-id="8dc77-122">hello **Azure Active Directory Premium 1**版本擴充這個模型也啟用 tooexamine hello 已偵測到每個報表的風險事件的基礎部分。</span><span class="sxs-lookup"><span data-stu-id="8dc77-122">hello **Azure Active Directory Premium 1** edition extends this model by also enabling you tooexamine some of hello underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="8dc77-123">hello **Azure Active Directory Premium 2**版本會提供您以 hello 最詳盡 hello 基礎風險事件的相關資訊，而且它也可讓您自動回應 tooconfigured tooconfigure 安全性原則風險層級。</span><span class="sxs-lookup"><span data-stu-id="8dc77-123">hello **Azure Active Directory Premium 2** edition provides you with hello most detailed information about hello underlying risk events and it also enables you tooconfigure security policies that automatically respond tooconfigured risk levels.</span></span>


## <a name="activity-reports"></a><span data-ttu-id="8dc77-124">活動報告</span><span class="sxs-lookup"><span data-stu-id="8dc77-124">Activity reports</span></span>

<span data-ttu-id="8dc77-125">Azure Active Directory 中有兩種活動報告：</span><span class="sxs-lookup"><span data-stu-id="8dc77-125">There are two types of activity reports in Azure Active Directory:</span></span>

- <span data-ttu-id="8dc77-126">**稽核記錄檔**-hello[稽核記錄活動報告](active-directory-reporting-activity-audit-logs.md)您提供的每個租用戶中已執行的工作存取 toohello 歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="8dc77-126">**Audit logs** - hello [audit logs activity report](active-directory-reporting-activity-audit-logs.md) provides you with access toohello history of every task performed in your tenant.</span></span>

- <span data-ttu-id="8dc77-127">**登入**-以 hello[登入活動報表](active-directory-reporting-activity-sign-ins.md)，您可以判斷，具有執行 hello 工作 hello 稽核記錄報告所報告的人員。</span><span class="sxs-lookup"><span data-stu-id="8dc77-127">**Sign-ins** -  With hello [sign-ins activity report](active-directory-reporting-activity-sign-ins.md), you can determine, who has performed hello tasks reported by hello audit logs report.</span></span>



<span data-ttu-id="8dc77-128">hello**稽核記錄報告**為您提供系統活動記錄的相容性。</span><span class="sxs-lookup"><span data-stu-id="8dc77-128">hello **audit logs report** provides you with records of system activities for compliance.</span></span>
<span data-ttu-id="8dc77-129">在其他的之間 hello 會提供資料可讓您 tooaddress 常見案例如：</span><span class="sxs-lookup"><span data-stu-id="8dc77-129">Amongst others, hello provided data enables you tooaddress common scenarios such as:</span></span>

- <span data-ttu-id="8dc77-130">我的租用戶中的某人收到存取 tooan admin 群組。</span><span class="sxs-lookup"><span data-stu-id="8dc77-130">Someone in my tenant got access tooan admin group.</span></span> <span data-ttu-id="8dc77-131">誰提供存取權給他們？</span><span class="sxs-lookup"><span data-stu-id="8dc77-131">Who gave them access?</span></span> 

- <span data-ttu-id="8dc77-132">我想 tooknow hello 登入特定的應用程式的使用者清單自我最近 onboarded hello 應用程式，而且想 tooknow 也執行</span><span class="sxs-lookup"><span data-stu-id="8dc77-132">I want tooknow hello list of users signing into a specific app since I recently onboarded hello app and want tooknow if it’s doing well</span></span>

- <span data-ttu-id="8dc77-133">我想要 tooknow 多少密碼重設發生在我的租用戶</span><span class="sxs-lookup"><span data-stu-id="8dc77-133">I want tooknow how many password resets are happening in my tenant</span></span>


<span data-ttu-id="8dc77-134">**Azure AD 授權需要 tooaccess hello 稽核記錄報告？**</span><span class="sxs-lookup"><span data-stu-id="8dc77-134">**What Azure AD license do you need tooaccess hello audit logs report?**</span></span>  
<span data-ttu-id="8dc77-135">hello 稽核記錄檔報表是可供您擁有授權的功能。</span><span class="sxs-lookup"><span data-stu-id="8dc77-135">hello audit logs report is available for features for which you have licenses.</span></span> <span data-ttu-id="8dc77-136">如果您有特定功能的授權，您也可以存取 toohello 稽核記錄檔的資訊。</span><span class="sxs-lookup"><span data-stu-id="8dc77-136">If you have a license for a specific feature, you also have access toohello audit log information for it.</span></span>

<span data-ttu-id="8dc77-137">如需詳細資訊，請參閱**比較正式推出的功能的 hello Free、 Basic 和 Premium edition**中[Azure Active Directory 功能](https://www.microsoft.com/cloud-platform/azure-active-directory-features)。</span><span class="sxs-lookup"><span data-stu-id="8dc77-137">For more details, see **Comparing generally available features of hello Free, Basic, and Premium editions** in [Azure Active Directory features and capabilities](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span></span>   



<span data-ttu-id="8dc77-138">hello**登入活動報表**啟用 tootoofind 回答 tooquestions 例如：</span><span class="sxs-lookup"><span data-stu-id="8dc77-138">hello **sign-ins activity report** enables tootoofind answers tooquestions such as:</span></span>

- <span data-ttu-id="8dc77-139">Hello 登入使用者的模式是什麼？</span><span class="sxs-lookup"><span data-stu-id="8dc77-139">What is hello sign-in pattern of a user?</span></span>
- <span data-ttu-id="8dc77-140">一週內有多少使用者登入？</span><span class="sxs-lookup"><span data-stu-id="8dc77-140">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="8dc77-141">這些登入的 hello 狀態為何？</span><span class="sxs-lookup"><span data-stu-id="8dc77-141">What’s hello status of these sign-ins?</span></span>


<span data-ttu-id="8dc77-142">**Azure AD 授權嗎需要 tooaccess hello 登入活動報表嗎？**</span><span class="sxs-lookup"><span data-stu-id="8dc77-142">**What Azure AD license do you need tooaccess hello sign-ins activity report?**</span></span>  
<span data-ttu-id="8dc77-143">tooaccess hello 登入活動報表，您的租用戶必須有與其相關聯的 Azure AD Premium 授權。</span><span class="sxs-lookup"><span data-stu-id="8dc77-143">tooaccess hello sign-ins activity report, your tenant must have an Azure AD Premium license associated with it.</span></span>


## <a name="programmatic-access"></a><span data-ttu-id="8dc77-144">以程式設計方式存取</span><span class="sxs-lookup"><span data-stu-id="8dc77-144">Programmatic access</span></span>

<span data-ttu-id="8dc77-145">加法 toohello 使用者介面、 Azure Active Directory 報告也會提供您與[以程式設計方式存取](active-directory-reporting-api-getting-started-azure-portal.md)toohello 報告資料。</span><span class="sxs-lookup"><span data-stu-id="8dc77-145">In addition toohello user interface, Azure Active Directory reporting also provides you with [programmatic access](active-directory-reporting-api-getting-started-azure-portal.md) toohello reporting data.</span></span> <span data-ttu-id="8dc77-146">這些報告的 hello 資料可以是很有幫助 tooyour 應用程式，例如 SIEM 系統、 稽核和商業智慧工具。</span><span class="sxs-lookup"><span data-stu-id="8dc77-146">hello data of these reports can be very useful tooyour applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="8dc77-147">hello Azure AD 報告 Api 提供以程式設計方式存取 toohello 資料透過一組 REST 架構應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="8dc77-147">hello Azure AD reporting APIs provide programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="8dc77-148">您可以從各種程式設計語言和工具呼叫這些 API。</span><span class="sxs-lookup"><span data-stu-id="8dc77-148">You can call these APIs from a variety of programming languages and tools.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="8dc77-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8dc77-149">Next steps</span></span>

<span data-ttu-id="8dc77-150">如果您想深入了解 hello tooknow Azure Active Directory 中的各種報表類型，請參閱：</span><span class="sxs-lookup"><span data-stu-id="8dc77-150">If you want tooknow more about hello various report types in Azure Active Directory, see:</span></span>

- [<span data-ttu-id="8dc77-151">標幟有風險的使用者報告</span><span class="sxs-lookup"><span data-stu-id="8dc77-151">Users flagged for risk report</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="8dc77-152">有風險的登入報告</span><span class="sxs-lookup"><span data-stu-id="8dc77-152">Risky sign-ins report</span></span>](active-directory-reporting-security-risky-sign-ins.md)
- [<span data-ttu-id="8dc77-153">稽核記錄報告</span><span class="sxs-lookup"><span data-stu-id="8dc77-153">Audit logs report</span></span>](active-directory-reporting-activity-audit-logs.md)
- [<span data-ttu-id="8dc77-154">登入記錄報告</span><span class="sxs-lookup"><span data-stu-id="8dc77-154">Sign-ins logs report</span></span>](active-directory-reporting-activity-sign-ins.md)

<span data-ttu-id="8dc77-155">如果您想深入了解存取報表資料使用 hello reporting API 的 hello hello tooknow，請參閱：</span><span class="sxs-lookup"><span data-stu-id="8dc77-155">If you want tooknow more about accessing hello hello reporting data using hello reporting API, see:</span></span> 

- [<span data-ttu-id="8dc77-156">開始使用 hello Azure Active Directory 報告 API</span><span class="sxs-lookup"><span data-stu-id="8dc77-156">Getting started with hello Azure Active Directory reporting API</span></span>](active-directory-reporting-api-getting-started-azure-portal.md)


<!--Image references-->
[1]: ./media/active-directory-reporting-azure-portal/ic195031.png