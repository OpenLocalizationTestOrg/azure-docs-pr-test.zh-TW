---
title: "aaaUsers 標示風險安全性報告 hello Azure Active Directory 入口網站中為 |Microsoft 文件"
description: "深入了解 hello 使用者標示為在 hello Azure Active Directory 入口網站的風險安全性報告"
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
ms.openlocfilehash: 5077cd61d6119745a85ed712623904633a151331
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="users-flagged-for-risk-security-report-in-hello-azure-active-directory-portal"></a><span data-ttu-id="3bfc5-103">標示為進行風險安全性報告 hello Azure Active Directory 入口網站中的使用者</span><span class="sxs-lookup"><span data-stu-id="3bfc5-103">Users flagged for risk security report in hello Azure Active Directory portal</span></span>

<span data-ttu-id="3bfc5-104">與 hello Azure Active Directory (Azure AD) 中的 hello 安全性報表，您可以深入了 hello 機率盜用的使用者帳戶，您的環境中。</span><span class="sxs-lookup"><span data-stu-id="3bfc5-104">With hello security reports in hello Azure Active Directory (Azure AD), you can gain insights into hello probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="3bfc5-105">Azure Active Directory 偵測到可疑相關的 tooyour 使用者帳戶的動作。</span><span class="sxs-lookup"><span data-stu-id="3bfc5-105">Azure Active Directory detects suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="3bfc5-106">針對每個偵測到的動作，將會建立一筆稱為「風險事件」的記錄。</span><span class="sxs-lookup"><span data-stu-id="3bfc5-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="3bfc5-107">如需詳細資訊，請參閱 [Azure Active Directory 風險事件](active-directory-identity-protection-risk-events.md)。</span><span class="sxs-lookup"><span data-stu-id="3bfc5-107">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="3bfc5-108">hello 偵測到有使用的 toocalculate 風險事件：</span><span class="sxs-lookup"><span data-stu-id="3bfc5-108">hello detected risk events are used toocalculate:</span></span>

- <span data-ttu-id="3bfc5-109">**高風險的登入**-有風險的登入是可能執行的人不是合法 hello 的使用者帳戶擁有者的登入嘗試的指標。</span><span class="sxs-lookup"><span data-stu-id="3bfc5-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="3bfc5-110">如需詳細資訊，請參閱[有風險的登入](active-directory-identityprotection.md#risky-sign-ins)。</span><span class="sxs-lookup"><span data-stu-id="3bfc5-110">For more information, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="3bfc5-111">**標幟為有風險的使用者** - 有風險的使用者表示可能被盜用的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="3bfc5-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="3bfc5-112">如需詳細資訊，請參閱[標幟為有風險的使用者](active-directory-identityprotection.md#users-flagged-for-risk)。</span><span class="sxs-lookup"><span data-stu-id="3bfc5-112">For more information, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="3bfc5-113">在 hello Azure 入口網站，您可以找到 hello 安全性報告 hello **Azure Active Directory**刀鋒視窗中 hello**安全性**> 一節。</span><span class="sxs-lookup"><span data-stu-id="3bfc5-113">In hello Azure portal, you can find hello security reports on hello **Azure Active Directory** blade in hello **Security** section.</span></span>  

![有風險的登入](./media/active-directory-reporting-security-user-at-risk/10.png)



## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a><span data-ttu-id="3bfc5-115">Azure AD 授權您需要 tooaccess 安全性報表嗎？</span><span class="sxs-lookup"><span data-stu-id="3bfc5-115">What Azure AD license do you need tooaccess a security report?</span></span>  

<span data-ttu-id="3bfc5-116">所有 Azure Active Directory 版本都會為您提供標幟為有風險的使用者報告。</span><span class="sxs-lookup"><span data-stu-id="3bfc5-116">All editions of Azure Active Directory provide you with users flagged for risk reports.</span></span>  
<span data-ttu-id="3bfc5-117">不過，報表資料粒度層級 hello hello 版本而異：</span><span class="sxs-lookup"><span data-stu-id="3bfc5-117">However, hello level of report granularity varies between hello editions:</span></span> 

- <span data-ttu-id="3bfc5-118">在 hello **Azure Active Directory Free 和 Basic 版本**，您已取得使用者針對風險加上旗標的清單。</span><span class="sxs-lookup"><span data-stu-id="3bfc5-118">In hello **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk.</span></span> 

- <span data-ttu-id="3bfc5-119">hello **Azure Active Directory Premium 1**版本擴充這個模型也啟用 tooexamine hello 已偵測到每個報表的風險事件的基礎部分。</span><span class="sxs-lookup"><span data-stu-id="3bfc5-119">hello **Azure Active Directory Premium 1** edition extends this model by also enabling you tooexamine some of hello underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="3bfc5-120">hello **Azure Active Directory Premium 2**版本會提供您與 hello 所有基礎的風險事件的最詳細的資訊，並可讓您 tooconfigure 自動回應 tooconfigured 風險的安全性原則層級。</span><span class="sxs-lookup"><span data-stu-id="3bfc5-120">hello **Azure Active Directory Premium 2** edition provides you with hello most detailed information about all underlying risk events and enables you tooconfigure security policies that automatically respond tooconfigured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="3bfc5-121">Azure Active Directory 免費和基本版本</span><span class="sxs-lookup"><span data-stu-id="3bfc5-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="3bfc5-122">hello 風險 hello Azure Active Directory free 和 basic 版本的報表加上旗標的使用者提供您可能已受到危害的使用者帳戶的清單。</span><span class="sxs-lookup"><span data-stu-id="3bfc5-122">hello users flagged for risk report in hello Azure Active Directory free and basic editions provides you with a list of user accounts that may have been compromised.</span></span> 


![有風險的登入](./media/active-directory-reporting-security-user-at-risk/03.png)

<span data-ttu-id="3bfc5-124">選取使用者開啟 hello 相關的使用者資料刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3bfc5-124">Selecting a user opens hello related user data blade.</span></span>
<span data-ttu-id="3bfc5-125">針對有風險的使用者，您可以檢閱 hello 使用者的登入歷程記錄，並且如有必要，請重設 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="3bfc5-125">For users that are at risk, you can review hello user’s sign-in history and reset hello password if necessary.</span></span>

![有風險的登入](./media/active-directory-reporting-security-user-at-risk/46.png)


<span data-ttu-id="3bfc5-127">此對話方塊會提供選項以便：</span><span class="sxs-lookup"><span data-stu-id="3bfc5-127">This dialog provides you with an option to:</span></span>

- <span data-ttu-id="3bfc5-128">下載 hello 報表</span><span class="sxs-lookup"><span data-stu-id="3bfc5-128">Download hello report</span></span>

- <span data-ttu-id="3bfc5-129">搜尋使用者</span><span class="sxs-lookup"><span data-stu-id="3bfc5-129">Search users</span></span>

![有風險的登入](./media/active-directory-reporting-security-user-at-risk/16.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="3bfc5-131">Azure Active Directory Premium Edition</span><span class="sxs-lookup"><span data-stu-id="3bfc5-131">Azure Active Directory premium editions</span></span>

<span data-ttu-id="3bfc5-132">hello hello Azure Active Directory premium edition 中，風險報表加上旗標的使用者提供讓您：</span><span class="sxs-lookup"><span data-stu-id="3bfc5-132">hello users flagged for risk report in hello Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="3bfc5-133">可能已遭盜用的[使用者帳戶清單](active-directory-identityprotection.md#users-flagged-for-risk)</span><span class="sxs-lookup"><span data-stu-id="3bfc5-133">A [list of user accounts](active-directory-identityprotection.md#users-flagged-for-risk) that may have been compromised</span></span> 

- <span data-ttu-id="3bfc5-134">彙總資訊 hello[風險事件類型](active-directory-identity-protection-risk-events.md)偵測到的</span><span class="sxs-lookup"><span data-stu-id="3bfc5-134">Aggregated information about hello [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="3bfc5-135">選項 toodownload hello 報表</span><span class="sxs-lookup"><span data-stu-id="3bfc5-135">An option toodownload hello report</span></span>

- <span data-ttu-id="3bfc5-136">選項 tooconfigure[使用者風險補救原則](active-directory-identityprotection.md#user-risk-security-policy)</span><span class="sxs-lookup"><span data-stu-id="3bfc5-136">An option tooconfigure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  


![有風險的登入](./media/active-directory-reporting-security-user-at-risk/71.png)

<span data-ttu-id="3bfc5-138">當您選取使用者時，即會取得這位使用者的詳細報告檢視，讓您能夠：</span><span class="sxs-lookup"><span data-stu-id="3bfc5-138">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="3bfc5-139">開啟 檢視所有登入的 hello</span><span class="sxs-lookup"><span data-stu-id="3bfc5-139">Open hello All sign-ins view</span></span>

- <span data-ttu-id="3bfc5-140">重設 hello 使用者密碼</span><span class="sxs-lookup"><span data-stu-id="3bfc5-140">Reset hello user's password</span></span>

- <span data-ttu-id="3bfc5-141">關閉所有事件</span><span class="sxs-lookup"><span data-stu-id="3bfc5-141">Dismiss all events</span></span>

- <span data-ttu-id="3bfc5-142">調查 hello 使用者報告的風險事件。</span><span class="sxs-lookup"><span data-stu-id="3bfc5-142">Investigate reported risk events for hello user.</span></span> 


![有風險的登入](./media/active-directory-reporting-security-user-at-risk/324.png)


<span data-ttu-id="3bfc5-144">tooinvestigate 風險事件，從選取一個 hello 清單 tooopen hello**詳細資料**這個風險事件刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3bfc5-144">tooinvestigate a risk event, select one from hello list tooopen hello **Details** blade for this risk event.</span></span> <span data-ttu-id="3bfc5-145">在 hello**詳細資料**刀鋒視窗中，您已擁有 hello 選項 tooeither[手動關閉風險事件](active-directory-identityprotection.md#closing-risk-events-manually)或重新啟動已手動關閉的風險事件。</span><span class="sxs-lookup"><span data-stu-id="3bfc5-145">On hello **Details** blade, you have hello option tooeither [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![有風險的登入](./media/active-directory-reporting-security-user-at-risk/325.png)



## <a name="next-steps"></a><span data-ttu-id="3bfc5-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3bfc5-147">Next steps</span></span>

- <span data-ttu-id="3bfc5-148">如需 Azure Active Directory Identity Protection 的詳細資訊，請參閱 [Azure Active Directory Identity Protection](active-directory-identityprotection.md)。</span><span class="sxs-lookup"><span data-stu-id="3bfc5-148">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

