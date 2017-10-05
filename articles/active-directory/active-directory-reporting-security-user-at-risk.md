---
title: "Azure Active Directory 入口網站中標幟為有風險的使用者安全性報告 | Microsoft Docs"
description: "了解 Azure Active Directory 入口網站中標幟為有風險的使用者安全性報告"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 04f15384a7cd0fa03300acdf159d371569ecf9fc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="users-flagged-for-risk-security-report-in-the-azure-active-directory-portal"></a><span data-ttu-id="f0eba-103">Azure Active Directory 入口網站中標幟為有風險的使用者安全性報告</span><span class="sxs-lookup"><span data-stu-id="f0eba-103">Users flagged for risk security report in the Azure Active Directory portal</span></span>

<span data-ttu-id="f0eba-104">利用 Azure Active Directory (Azure AD) 中的安全性報告，您可以深入了解環境中使用者帳戶被盜用的可能性。</span><span class="sxs-lookup"><span data-stu-id="f0eba-104">With the security reports in the Azure Active Directory (Azure AD), you can gain insights into the probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="f0eba-105">Azure Active Directory 會偵測使用者帳戶相關的可疑動作。</span><span class="sxs-lookup"><span data-stu-id="f0eba-105">Azure Active Directory detects suspicious actions that are related to your user accounts.</span></span> <span data-ttu-id="f0eba-106">針對每個偵測到的動作，將會建立一筆稱為「風險事件」的記錄。</span><span class="sxs-lookup"><span data-stu-id="f0eba-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="f0eba-107">如需詳細資訊，請參閱 [Azure Active Directory 風險事件](active-directory-identity-protection-risk-events.md)。</span><span class="sxs-lookup"><span data-stu-id="f0eba-107">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="f0eba-108">偵測到的風險事件用來計算︰</span><span class="sxs-lookup"><span data-stu-id="f0eba-108">The detected risk events are used to calculate:</span></span>

- <span data-ttu-id="f0eba-109">**有風險的登入** - 有風險的登入表示非使用者帳戶合法擁有者的某人嘗試登入。</span><span class="sxs-lookup"><span data-stu-id="f0eba-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> <span data-ttu-id="f0eba-110">如需詳細資訊，請參閱[有風險的登入](active-directory-identityprotection.md#risky-sign-ins)。</span><span class="sxs-lookup"><span data-stu-id="f0eba-110">For more information, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="f0eba-111">**標幟為有風險的使用者** - 有風險的使用者表示可能被盜用的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="f0eba-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="f0eba-112">如需詳細資訊，請參閱[標幟為有風險的使用者](active-directory-identityprotection.md#users-flagged-for-risk)。</span><span class="sxs-lookup"><span data-stu-id="f0eba-112">For more information, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="f0eba-113">在 Azure 入口網站中，您可以在 [Azure Active Directory] 刀鋒視窗的 [安全性] 區段中找到安全性報告。</span><span class="sxs-lookup"><span data-stu-id="f0eba-113">In the Azure portal, you can find the security reports on the **Azure Active Directory** blade in the **Security** section.</span></span>  

![有風險的登入](./media/active-directory-reporting-security-user-at-risk/10.png)



## <a name="what-azure-ad-license-do-you-need-to-access-a-security-report"></a><span data-ttu-id="f0eba-115">您需要哪項 Azure AD 授權才能存取安全性報告？</span><span class="sxs-lookup"><span data-stu-id="f0eba-115">What Azure AD license do you need to access a security report?</span></span>  

<span data-ttu-id="f0eba-116">所有 Azure Active Directory 版本都會為您提供標幟為有風險的使用者報告。</span><span class="sxs-lookup"><span data-stu-id="f0eba-116">All editions of Azure Active Directory provide you with users flagged for risk reports.</span></span>  
<span data-ttu-id="f0eba-117">不過，報告細微性層級因版本而異：</span><span class="sxs-lookup"><span data-stu-id="f0eba-117">However, the level of report granularity varies between the editions:</span></span> 

- <span data-ttu-id="f0eba-118">在 [Azure Active Directory Free 和 Basic 版本] 中，您已取得標幟為有風險的使用者清單。</span><span class="sxs-lookup"><span data-stu-id="f0eba-118">In the **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk.</span></span> 

- <span data-ttu-id="f0eba-119">**Azure Active Directory Premium 1** 版本也可讓您檢查每份報告部分已偵測到的基礎風險事件，藉此擴充此模型。</span><span class="sxs-lookup"><span data-stu-id="f0eba-119">The **Azure Active Directory Premium 1** edition extends this model by also enabling you to examine some of the underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="f0eba-120">**Azure Active Directory Premium 2** 版本可提供有關所有基礎風險事件的最詳細資訊，可讓您設定安全性原則，自動回應已設定的風險層級。</span><span class="sxs-lookup"><span data-stu-id="f0eba-120">The **Azure Active Directory Premium 2** edition provides you with the most detailed information about all underlying risk events and enables you to configure security policies that automatically respond to configured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="f0eba-121">Azure Active Directory 免費和基本版本</span><span class="sxs-lookup"><span data-stu-id="f0eba-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="f0eba-122">Azure Active Directory 免費和基本版本中標幟為有風險的使用者報告，會提供可能遭到盜用的使用者帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="f0eba-122">The users flagged for risk report in the Azure Active Directory free and basic editions provides you with a list of user accounts that may have been compromised.</span></span> 


![有風險的登入](./media/active-directory-reporting-security-user-at-risk/03.png)

<span data-ttu-id="f0eba-124">選取使用者，即會開啟相關的使用者資料刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f0eba-124">Selecting a user opens the related user data blade.</span></span>
<span data-ttu-id="f0eba-125">針對有風險的使用者，您可以檢閱使用者的登入記錄，如有必要，請重設密碼。</span><span class="sxs-lookup"><span data-stu-id="f0eba-125">For users that are at risk, you can review the user’s sign-in history and reset the password if necessary.</span></span>

![有風險的登入](./media/active-directory-reporting-security-user-at-risk/46.png)


<span data-ttu-id="f0eba-127">此對話方塊會提供選項以便：</span><span class="sxs-lookup"><span data-stu-id="f0eba-127">This dialog provides you with an option to:</span></span>

- <span data-ttu-id="f0eba-128">下載報告</span><span class="sxs-lookup"><span data-stu-id="f0eba-128">Download the report</span></span>

- <span data-ttu-id="f0eba-129">搜尋使用者</span><span class="sxs-lookup"><span data-stu-id="f0eba-129">Search users</span></span>

![有風險的登入](./media/active-directory-reporting-security-user-at-risk/16.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="f0eba-131">Azure Active Directory Premium Edition</span><span class="sxs-lookup"><span data-stu-id="f0eba-131">Azure Active Directory premium editions</span></span>

<span data-ttu-id="f0eba-132">Azure Active Directory Premium Edition 中標幟為有風險的使用者報告可提供：</span><span class="sxs-lookup"><span data-stu-id="f0eba-132">The users flagged for risk report in the Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="f0eba-133">可能已遭盜用的[使用者帳戶清單](active-directory-identityprotection.md#users-flagged-for-risk)</span><span class="sxs-lookup"><span data-stu-id="f0eba-133">A [list of user accounts](active-directory-identityprotection.md#users-flagged-for-risk) that may have been compromised</span></span> 

- <span data-ttu-id="f0eba-134">關於已偵測到之[風險事件類型](active-directory-identity-protection-risk-events.md)的彙總資訊</span><span class="sxs-lookup"><span data-stu-id="f0eba-134">Aggregated information about the [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="f0eba-135">下載報告的選項</span><span class="sxs-lookup"><span data-stu-id="f0eba-135">An option to download the report</span></span>

- <span data-ttu-id="f0eba-136">選擇設定[使用者風險補救原則](active-directory-identityprotection.md#user-risk-security-policy)</span><span class="sxs-lookup"><span data-stu-id="f0eba-136">An option to configure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  


![有風險的登入](./media/active-directory-reporting-security-user-at-risk/71.png)

<span data-ttu-id="f0eba-138">當您選取使用者時，即會取得這位使用者的詳細報告檢視，讓您能夠：</span><span class="sxs-lookup"><span data-stu-id="f0eba-138">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="f0eba-139">開啟 [所有登入] 檢視</span><span class="sxs-lookup"><span data-stu-id="f0eba-139">Open the All sign-ins view</span></span>

- <span data-ttu-id="f0eba-140">重設使用者的密碼</span><span class="sxs-lookup"><span data-stu-id="f0eba-140">Reset the user's password</span></span>

- <span data-ttu-id="f0eba-141">關閉所有事件</span><span class="sxs-lookup"><span data-stu-id="f0eba-141">Dismiss all events</span></span>

- <span data-ttu-id="f0eba-142">調查針對該使用者報告的風險事件。</span><span class="sxs-lookup"><span data-stu-id="f0eba-142">Investigate reported risk events for the user.</span></span> 


![有風險的登入](./media/active-directory-reporting-security-user-at-risk/324.png)


<span data-ttu-id="f0eba-144">若要調查風險事件，請從清單中選取一項，以開啟此風險事件的 [詳細資料] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f0eba-144">To investigate a risk event, select one from the list to open the **Details** blade for this risk event.</span></span> <span data-ttu-id="f0eba-145">在 [詳細資料] 刀鋒視窗中，您可以選擇[手動關閉風險事件](active-directory-identityprotection.md#closing-risk-events-manually)或重新啟動已手動關閉的風險事件。</span><span class="sxs-lookup"><span data-stu-id="f0eba-145">On the **Details** blade, you have the option to either [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![有風險的登入](./media/active-directory-reporting-security-user-at-risk/325.png)



## <a name="next-steps"></a><span data-ttu-id="f0eba-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f0eba-147">Next steps</span></span>

- <span data-ttu-id="f0eba-148">如需 Azure Active Directory Identity Protection 的詳細資訊，請參閱 [Azure Active Directory Identity Protection](active-directory-identityprotection.md)。</span><span class="sxs-lookup"><span data-stu-id="f0eba-148">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

