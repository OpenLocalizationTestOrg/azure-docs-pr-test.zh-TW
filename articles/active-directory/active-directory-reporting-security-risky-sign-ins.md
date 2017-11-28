---
title: "aaaRisky hello Azure Active Directory 入口網站中的登入報表 |Microsoft 文件"
description: "深入了解 hello Azure Active Directory 入口網站中的 hello 危險的登入報表"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: 7728fcd7-3dd5-4b99-a0e4-949c69788c0f
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d8df5cafea6b38f3e364c24a6aff599abe088e88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="risky-sign-ins-report-in-hello-azure-active-directory-portal"></a><span data-ttu-id="2dcdb-103">Hello Azure Active Directory 入口網站中的高風險的登入報表</span><span class="sxs-lookup"><span data-stu-id="2dcdb-103">Risky sign-ins report in hello Azure Active Directory portal</span></span>

<span data-ttu-id="2dcdb-104">使用 Azure Active Directory (Azure AD) 中的 hello 安全性報告中，您可以取得 hello 機率盜用的使用者帳戶的深入了解您的環境中。</span><span class="sxs-lookup"><span data-stu-id="2dcdb-104">With hello security reports in Azure Active Directory (Azure AD) you can gain insights into hello probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="2dcdb-105">Azure AD 會偵測到可疑相關的 tooyour 使用者帳戶的動作。</span><span class="sxs-lookup"><span data-stu-id="2dcdb-105">Azure AD detects suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="2dcdb-106">針對每個偵測到的動作，將會建立一筆稱為「風險事件」的記錄。</span><span class="sxs-lookup"><span data-stu-id="2dcdb-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="2dcdb-107">如需詳細資訊，請參閱 [Azure Active 風險事件](active-directory-identity-protection-risk-events.md)。</span><span class="sxs-lookup"><span data-stu-id="2dcdb-107">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="2dcdb-108">hello 偵測到有使用的 toocalculate 風險事件：</span><span class="sxs-lookup"><span data-stu-id="2dcdb-108">hello detected risk events are used toocalculate:</span></span>

- <span data-ttu-id="2dcdb-109">**高風險的登入**-有風險的登入是可能執行的人不是合法 hello 的使用者帳戶擁有者的登入嘗試的指標。</span><span class="sxs-lookup"><span data-stu-id="2dcdb-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="2dcdb-110">如需詳細資訊，請參閱[有風險的登入](active-directory-identityprotection.md#risky-sign-ins)。</span><span class="sxs-lookup"><span data-stu-id="2dcdb-110">For more details, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="2dcdb-111">**標幟為有風險的使用者** - 有風險的使用者表示可能被盜用的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="2dcdb-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="2dcdb-112">如需詳細資訊，請參閱[標幟為有風險的使用者](active-directory-identityprotection.md#users-flagged-for-risk)。</span><span class="sxs-lookup"><span data-stu-id="2dcdb-112">For more details, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="2dcdb-113">在[hello Azure 入口網站](https://portal.azure.com)，您可以找到 hello 安全性報告 hello **Azure Active Directory**刀鋒視窗中 hello**安全性**> 一節。</span><span class="sxs-lookup"><span data-stu-id="2dcdb-113">In [hello Azure portal](https://portal.azure.com), you can find hello security reports on hello **Azure Active Directory** blade in hello **Security** section.</span></span> 

![有風險的登入](./media/active-directory-reporting-security-risky-sign-ins/10.png)


## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a><span data-ttu-id="2dcdb-115">Azure AD 授權您需要 tooaccess 安全性報表嗎？</span><span class="sxs-lookup"><span data-stu-id="2dcdb-115">What Azure AD license do you need tooaccess a security report?</span></span>  

<span data-ttu-id="2dcdb-116">所有 Azure Active Directory 版本都會為您提供有風險的登入報告。</span><span class="sxs-lookup"><span data-stu-id="2dcdb-116">All editions of Azure Active Directory provide you with risky sign-ins reports.</span></span>  
<span data-ttu-id="2dcdb-117">不過，報表資料粒度層級 hello hello 版本而異：</span><span class="sxs-lookup"><span data-stu-id="2dcdb-117">However, hello level of report granularity varies between hello editions:</span></span> 

- <span data-ttu-id="2dcdb-118">在 hello **Azure Active Directory Free 和 Basic 版本**，您已取得高風險的登入的清單。</span><span class="sxs-lookup"><span data-stu-id="2dcdb-118">In hello **Azure Active Directory Free and Basic editions**, you already get a list of risky sign-ins.</span></span> 

- <span data-ttu-id="2dcdb-119">hello **Azure Active Directory Premium 1**版本擴充這個模型也啟用 tooexamine hello 已偵測到每個報表的風險事件的基礎部分。</span><span class="sxs-lookup"><span data-stu-id="2dcdb-119">hello **Azure Active Directory Premium 1** edition extends this model by also enabling you tooexamine some of hello underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="2dcdb-120">hello **Azure Active Directory Premium 2**版本會提供您以 hello 最詳盡的所有基礎的風險事件的相關資訊，而且它也可讓您自動回應 tooconfigured tooconfigure 安全性原則風險層級。</span><span class="sxs-lookup"><span data-stu-id="2dcdb-120">hello **Azure Active Directory Premium 2** edition provides you with hello most detailed information about all underlying risk events and it also enables you tooconfigure security policies that automatically respond tooconfigured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="2dcdb-121">Azure Active Directory 免費和基本版本</span><span class="sxs-lookup"><span data-stu-id="2dcdb-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="2dcdb-122">hello Azure Active Directory free 和 basic 版提供您有風險的登入偵測到的清單為您的使用者。</span><span class="sxs-lookup"><span data-stu-id="2dcdb-122">hello Azure Active Directory free and basic editions provide you with a list of risky sign-ins that have been detected for your users.</span></span> <span data-ttu-id="2dcdb-123">此報告會列出：</span><span class="sxs-lookup"><span data-stu-id="2dcdb-123">This report lists:</span></span>

- <span data-ttu-id="2dcdb-124">**使用者**-hello hello 使用者 hello 登入作業期間，所使用的名稱</span><span class="sxs-lookup"><span data-stu-id="2dcdb-124">**User** - hello name of hello user that was used during hello sign-in operation</span></span>
- <span data-ttu-id="2dcdb-125">**IP** -hello 已使用的 tooconnect tooAzure Active Directory 的 hello 裝置的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="2dcdb-125">**IP** - hello IP address of hello device that was used tooconnect tooAzure Active Directory</span></span>
- <span data-ttu-id="2dcdb-126">**位置**-使用 tooconnect tooAzure Active Directory hello 位置。</span><span class="sxs-lookup"><span data-stu-id="2dcdb-126">**Location** - hello location used tooconnect tooAzure Active Directory</span></span>
- <span data-ttu-id="2dcdb-127">**登入時間**-hello hello 登入執行時的時間</span><span class="sxs-lookup"><span data-stu-id="2dcdb-127">**Sign-in time** - hello time when hello sign-in was performed</span></span>
- <span data-ttu-id="2dcdb-128">**狀態**-hello hello 登入的狀態</span><span class="sxs-lookup"><span data-stu-id="2dcdb-128">**Status** - hello status of hello sign-in</span></span>


![有風險的登入](./media/active-directory-reporting-security-risky-sign-ins/01.png)

<span data-ttu-id="2dcdb-130">根據您調查 hello 風險登入，您可以提供意見反應 tooAzure Active Directory 中的下列動作的 hello 形式：</span><span class="sxs-lookup"><span data-stu-id="2dcdb-130">Based on your investigation of hello risky sign-in, you can provide feedback tooAzure Active Directory in form of hello following actions:</span></span>

- <span data-ttu-id="2dcdb-131">解決</span><span class="sxs-lookup"><span data-stu-id="2dcdb-131">Resolve</span></span>
- <span data-ttu-id="2dcdb-132">標記為誤判</span><span class="sxs-lookup"><span data-stu-id="2dcdb-132">Mark as false positive</span></span>
- <span data-ttu-id="2dcdb-133">略過</span><span class="sxs-lookup"><span data-stu-id="2dcdb-133">Ignore</span></span>
- <span data-ttu-id="2dcdb-134">重新啟動</span><span class="sxs-lookup"><span data-stu-id="2dcdb-134">Reactivate</span></span>

![有風險的登入](./media/active-directory-reporting-security-risky-sign-ins/21.png)

<span data-ttu-id="2dcdb-136">如需詳細資訊，請參閱[手動關閉風險事件](active-directory-identityprotection.md#closing-risk-events-manually)。</span><span class="sxs-lookup"><span data-stu-id="2dcdb-136">For more details, see [Closing risk events manually](active-directory-identityprotection.md#closing-risk-events-manually).</span></span>

<span data-ttu-id="2dcdb-137">此報告會提供選項以便：</span><span class="sxs-lookup"><span data-stu-id="2dcdb-137">This report provides you with an option to:</span></span>

- <span data-ttu-id="2dcdb-138">搜尋資源</span><span class="sxs-lookup"><span data-stu-id="2dcdb-138">Searh resources</span></span>
- <span data-ttu-id="2dcdb-139">下載 hello 報表資料</span><span class="sxs-lookup"><span data-stu-id="2dcdb-139">Download hello report data</span></span>


![有風險的登入](./media/active-directory-reporting-security-risky-sign-ins/93.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="2dcdb-141">Azure Active Directory Premium Edition</span><span class="sxs-lookup"><span data-stu-id="2dcdb-141">Azure Active Directory premium editions</span></span>

<span data-ttu-id="2dcdb-142">hello Azure Active Directory premium edition 中的 hello 危險的登入報告可讓您使用：</span><span class="sxs-lookup"><span data-stu-id="2dcdb-142">hello risky sign-ins report in hello Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="2dcdb-143">彙總資訊 hello[風險事件類型](active-directory-identity-protection-risk-events.md)偵測到的</span><span class="sxs-lookup"><span data-stu-id="2dcdb-143">Aggregated information about hello [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="2dcdb-144">選項 toodownload hello 報表</span><span class="sxs-lookup"><span data-stu-id="2dcdb-144">An option toodownload hello report</span></span>


![有風險的登入](./media/active-directory-reporting-security-risky-sign-ins/456.png)


<span data-ttu-id="2dcdb-146">當您選取風險事件時，即會取得這個風險事件的詳細報告檢視，讓您能夠：</span><span class="sxs-lookup"><span data-stu-id="2dcdb-146">When you select a risk event, you get a detailed report view for this risk event that enables you to:</span></span>

- <span data-ttu-id="2dcdb-147">選項 tooconfigure[使用者風險補救原則](active-directory-identityprotection.md#user-risk-security-policy)</span><span class="sxs-lookup"><span data-stu-id="2dcdb-147">An option tooconfigure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  

- <span data-ttu-id="2dcdb-148">檢閱 hello hello 風險事件的偵測時間軸</span><span class="sxs-lookup"><span data-stu-id="2dcdb-148">Review hello detection timeline for hello risk event</span></span>  

- <span data-ttu-id="2dcdb-149">檢閱已偵測到此風險事件的使用者清單</span><span class="sxs-lookup"><span data-stu-id="2dcdb-149">Review a list of users for which this risk event has been detected</span></span>

- <span data-ttu-id="2dcdb-150">[手動關閉風險事件](active-directory-identityprotection.md#closing-risk-events-manually)或重新啟動已手動關閉的風險事件。</span><span class="sxs-lookup"><span data-stu-id="2dcdb-150">[Manually close risk events](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![有風險的登入](./media/active-directory-reporting-security-risky-sign-ins/457.png)

<span data-ttu-id="2dcdb-152">當您選取使用者時，即會取得這位使用者的詳細報告檢視，讓您能夠：</span><span class="sxs-lookup"><span data-stu-id="2dcdb-152">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="2dcdb-153">開啟 檢視所有登入的 hello</span><span class="sxs-lookup"><span data-stu-id="2dcdb-153">Open hello All sign-ins view</span></span>

- <span data-ttu-id="2dcdb-154">重設 hello 使用者密碼</span><span class="sxs-lookup"><span data-stu-id="2dcdb-154">Reset hello user's password</span></span>

- <span data-ttu-id="2dcdb-155">關閉所有事件</span><span class="sxs-lookup"><span data-stu-id="2dcdb-155">Dismiss all events</span></span>

- <span data-ttu-id="2dcdb-156">調查 hello 使用者報告的風險事件。</span><span class="sxs-lookup"><span data-stu-id="2dcdb-156">Investigate reported risk events for hello user.</span></span> 


![有風險的登入](./media/active-directory-reporting-security-risky-sign-ins/324.png)


<span data-ttu-id="2dcdb-158">tooinvestigate 風險事件，從清單選取一個 hello。</span><span class="sxs-lookup"><span data-stu-id="2dcdb-158">tooinvestigate a risk event, select one from hello list.</span></span>  
<span data-ttu-id="2dcdb-159">這會開啟 hello**詳細資料**這個風險事件刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2dcdb-159">This opens hello **Details** blade for this risk event.</span></span> <span data-ttu-id="2dcdb-160">在 hello**詳細資料**刀鋒視窗中，您已擁有 hello 選項 tooeither[手動關閉風險事件](active-directory-identityprotection.md#closing-risk-events-manually)或重新啟動已手動關閉的風險事件。</span><span class="sxs-lookup"><span data-stu-id="2dcdb-160">On hello **Details** blade, you have hello option tooeither [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![有風險的登入](./media/active-directory-reporting-security-risky-sign-ins/325.png)





## <a name="next-steps"></a><span data-ttu-id="2dcdb-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2dcdb-162">Next steps</span></span>

- <span data-ttu-id="2dcdb-163">如需 Azure Active Directory Identity Protection 的詳細資訊，請參閱 [Azure Active Directory Identity Protection](active-directory-identityprotection.md)。</span><span class="sxs-lookup"><span data-stu-id="2dcdb-163">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

