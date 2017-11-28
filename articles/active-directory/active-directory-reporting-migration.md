---
title: "aaaFind 活動報告的 hello Azure 入口網站 |Microsoft 文件"
description: "了解 Azure Active Directory 活動 toofind hello Azure 入口網站中的報告方式。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: d93521f8-dc21-4feb-aaff-4bb300f04812
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: f8d7a968403e10ccc5319f27fedad38b1553ded0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="find-activity-reports-in-hello-azure-portal"></a><span data-ttu-id="41e0d-103">在 [hello Azure 入口網站中尋找活動報告</span><span class="sxs-lookup"><span data-stu-id="41e0d-103">Find activity reports in hello Azure portal</span></span>

<span data-ttu-id="41e0d-104">如果您要從 Azure 傳統入口網站 toohello hello 移動 [Azure 入口網站，您會取得 Azure Active Directory (Azure AD) 活動記錄在新的外觀。</span><span class="sxs-lookup"><span data-stu-id="41e0d-104">If you are moving from hello Azure classic portal toohello Azure portal, you get a new look at Azure Active Directory (Azure AD) activity logs.</span></span> <span data-ttu-id="41e0d-105">中的最近[部落格文章](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/)，我們會說明如何查看活動記錄中的 hello 資源依據您進行 hello Azure 入口網站中的 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="41e0d-105">In a recent [blog post](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), we explain how you can see activity logs in hello context of hello resource you are working on in hello Azure portal.</span></span> <span data-ttu-id="41e0d-106">在本文中，我們說明 toofind 報告的方式，在 [hello hello Azure 入口網站中的 Azure 傳統入口網站中使用。</span><span class="sxs-lookup"><span data-stu-id="41e0d-106">In this article, we describe how toofind reports that you used in hello Azure classic portal in hello Azure portal.</span></span>

## <a name="whats-new"></a><span data-ttu-id="41e0d-107">新功能</span><span class="sxs-lookup"><span data-stu-id="41e0d-107">What's new</span></span>

<span data-ttu-id="41e0d-108">Hello Azure 傳統入口網站中的報表分為類別：</span><span class="sxs-lookup"><span data-stu-id="41e0d-108">Reports in hello Azure classic portal are separated into categories:</span></span>

1.  <span data-ttu-id="41e0d-109">安全性報告</span><span class="sxs-lookup"><span data-stu-id="41e0d-109">Security reports</span></span>
2.  <span data-ttu-id="41e0d-110">活動報告</span><span class="sxs-lookup"><span data-stu-id="41e0d-110">Activity reports</span></span>
3.  <span data-ttu-id="41e0d-111">整合式應用程式報告</span><span class="sxs-lookup"><span data-stu-id="41e0d-111">Integrated app reports</span></span>

### <a name="activity-and-integrated-app-reports"></a><span data-ttu-id="41e0d-112">活動和整合式應用程式報告</span><span class="sxs-lookup"><span data-stu-id="41e0d-112">Activity and integrated app reports</span></span>

<span data-ttu-id="41e0d-113">針對以內容為主 hello Azure 入口網站中的報表，現有的報表會合併到單一檢視。</span><span class="sxs-lookup"><span data-stu-id="41e0d-113">For context-based reporting in hello Azure portal, existing reports are merged into a single view.</span></span> <span data-ttu-id="41e0d-114">單一基礎的 API，可提供 hello 資料 toohello 檢視。</span><span class="sxs-lookup"><span data-stu-id="41e0d-114">A single, underlying API provides hello data toohello view.</span></span>

<span data-ttu-id="41e0d-115">此檢視 hello toosee **Azure Active Directory**刀鋒視窗底下**活動**，選取**稽核記錄檔**。</span><span class="sxs-lookup"><span data-stu-id="41e0d-115">toosee this view, on hello **Azure Active Directory** blade, under **ACTIVITY**, select **Audit logs**.</span></span>

<span data-ttu-id="41e0d-116">![稽核記錄](./media/active-directory-reporting-migration/482.png "稽核記錄")</span><span class="sxs-lookup"><span data-stu-id="41e0d-116">![Audit logs](./media/active-directory-reporting-migration/482.png "Audit logs")</span></span>

<span data-ttu-id="41e0d-117">在此檢視將會合併 hello 下列報表：</span><span class="sxs-lookup"><span data-stu-id="41e0d-117">hello following reports are consolidated in this view:</span></span>

-   <span data-ttu-id="41e0d-118">稽核報告</span><span class="sxs-lookup"><span data-stu-id="41e0d-118">Audit report</span></span>
-   <span data-ttu-id="41e0d-119">密碼重設活動</span><span class="sxs-lookup"><span data-stu-id="41e0d-119">Password reset activity</span></span>
-   <span data-ttu-id="41e0d-120">密碼重設註冊活動</span><span class="sxs-lookup"><span data-stu-id="41e0d-120">Password reset registration activity</span></span>
-   <span data-ttu-id="41e0d-121">自助式群組活動</span><span class="sxs-lookup"><span data-stu-id="41e0d-121">Self-service groups activity</span></span>
-   <span data-ttu-id="41e0d-122">Office365 群組名稱變更</span><span class="sxs-lookup"><span data-stu-id="41e0d-122">Office365 Group Name Changes</span></span>
-   <span data-ttu-id="41e0d-123">帳戶佈建活動</span><span class="sxs-lookup"><span data-stu-id="41e0d-123">Account provisioning activity</span></span>
-   <span data-ttu-id="41e0d-124">密碼變換狀態</span><span class="sxs-lookup"><span data-stu-id="41e0d-124">Password rollover status</span></span>
-   <span data-ttu-id="41e0d-125">帳戶佈建錯誤</span><span class="sxs-lookup"><span data-stu-id="41e0d-125">Account provisioning errors</span></span>


<span data-ttu-id="41e0d-126">hello 應用程式使用情況報表已經增強，而且會包含在 hello**登入**檢視。</span><span class="sxs-lookup"><span data-stu-id="41e0d-126">hello Application Usage report has been enhanced and is included in hello **Sign-ins** view.</span></span> <span data-ttu-id="41e0d-127">此檢視 hello toosee **Azure Active Directory**刀鋒視窗底下**活動**，選取**登入**。</span><span class="sxs-lookup"><span data-stu-id="41e0d-127">toosee this view, on hello **Azure Active Directory** blade, under **ACTIVITY**, select **Sign-ins**.</span></span>

<span data-ttu-id="41e0d-128">![登入檢視](./media/active-directory-reporting-migration/483.png "登入檢視")</span><span class="sxs-lookup"><span data-stu-id="41e0d-128">![Sign-ins view](./media/active-directory-reporting-migration/483.png "Sign-ins view")</span></span>

<span data-ttu-id="41e0d-129">hello**登入**檢視包含所有的使用者登入。您可以使用此資訊 tooget 應用程式使用方式資訊。</span><span class="sxs-lookup"><span data-stu-id="41e0d-129">hello **Sign-ins** view includes all user sign-ins. You can use this information tooget application usage information.</span></span> <span data-ttu-id="41e0d-130">您也可以檢視應用程式使用資訊在 hello**企業應用程式**概觀，請在 [hello**管理**> 一節。</span><span class="sxs-lookup"><span data-stu-id="41e0d-130">You also can view application usage information in hello **Enterprise applications** overview, in hello **MANAGE** section.</span></span>

<span data-ttu-id="41e0d-131">![企業應用程式](./media/active-directory-reporting-migration/484.png "企業應用程式")</span><span class="sxs-lookup"><span data-stu-id="41e0d-131">![Enterprise applications](./media/active-directory-reporting-migration/484.png "Enterprise applications")</span></span>

## <a name="access-a-specific-report"></a><span data-ttu-id="41e0d-132">存取特定報告</span><span class="sxs-lookup"><span data-stu-id="41e0d-132">Access a specific report</span></span>

<span data-ttu-id="41e0d-133">雖然 hello Azure 入口網站提供了單一檢視，您也可以查看特定報表。</span><span class="sxs-lookup"><span data-stu-id="41e0d-133">Although hello Azure portal offers a single view, you also can look at specific reports.</span></span>

### <a name="audit-logs"></a><span data-ttu-id="41e0d-134">稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="41e0d-134">Audit logs</span></span>

<span data-ttu-id="41e0d-135">在回應 toocustomer 意見反應，在 hello Azure 入口網站，您可以使用進階篩選 tooaccess hello 您想要的資料。</span><span class="sxs-lookup"><span data-stu-id="41e0d-135">In response toocustomer feedback, in hello Azure portal, you can use advanced filtering tooaccess hello data you want.</span></span> <span data-ttu-id="41e0d-136">您可以使用一個篩選條件*活動類別*，其中會列出 hello 不同類型的活動記錄在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="41e0d-136">One filter you can use is an *activity category*, which lists hello different types of activity logs in Azure AD.</span></span> <span data-ttu-id="41e0d-137">toonarrow 結果 toowhat 想要您可以選取類別。</span><span class="sxs-lookup"><span data-stu-id="41e0d-137">toonarrow results toowhat you are looking for, you can select a category.</span></span>

<span data-ttu-id="41e0d-138">例如，如果您想要只在活動相關的 tooself 服務密碼重設，您可以選擇 hello**自助密碼管理**類別目錄。</span><span class="sxs-lookup"><span data-stu-id="41e0d-138">For example, if you are interested only in activities related tooself-service password resets, you can choose hello **Self-service Password Management** category.</span></span> <span data-ttu-id="41e0d-139">您看到的 hello 類別取決於您工作所在的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="41e0d-139">hello categories you see are based on hello resource you are working in.</span></span>  

<span data-ttu-id="41e0d-140">![Hello 篩選稽核記錄檔] 頁面上的類別目錄選項](./media/active-directory-reporting-migration/06.png "hello 篩選稽核記錄檔] 頁面上的類別目錄選項")</span><span class="sxs-lookup"><span data-stu-id="41e0d-140">![Category options on hello Filter Audit Logs page](./media/active-directory-reporting-migration/06.png "Category options on hello Filter Audit Logs page")</span></span>

<span data-ttu-id="41e0d-141">活動類別包括︰</span><span class="sxs-lookup"><span data-stu-id="41e0d-141">Activity categories include:</span></span>

- <span data-ttu-id="41e0d-142">核心目錄</span><span class="sxs-lookup"><span data-stu-id="41e0d-142">Core Directory</span></span>
- <span data-ttu-id="41e0d-143">自助式密碼管理</span><span class="sxs-lookup"><span data-stu-id="41e0d-143">Self-service Password Management</span></span>
- <span data-ttu-id="41e0d-144">自助式群組管理</span><span class="sxs-lookup"><span data-stu-id="41e0d-144">Self-service Group Management</span></span>
- <span data-ttu-id="41e0d-145">帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="41e0d-145">Account Provisioning</span></span>

### <a name="application-usage"></a><span data-ttu-id="41e0d-146">應用程式使用情況</span><span class="sxs-lookup"><span data-stu-id="41e0d-146">Application usage</span></span>

<span data-ttu-id="41e0d-147">tooview 的相關詳細資料或單一應用程式中，所有應用程式的應用程式使用情形下**活動**，選取**登入**。 toonarrow hello 結果，您可以篩選使用者或應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="41e0d-147">tooview details about application usage for all apps or for a single app, under **ACTIVITY**, select **Sign-ins**. toonarrow hello results, you can filter on user name or application name.</span></span>

<span data-ttu-id="41e0d-148">![[篩選登入事件] 頁面](./media/active-directory-reporting-migration/07.png "[篩選登入事件] 頁面")</span><span class="sxs-lookup"><span data-stu-id="41e0d-148">![Filter Sign-In Events page](./media/active-directory-reporting-migration/07.png "Filter Sign-In Events page")</span></span>

### <a name="security-reports"></a><span data-ttu-id="41e0d-149">安全性報告</span><span class="sxs-lookup"><span data-stu-id="41e0d-149">Security reports</span></span>

#### <a name="azure-ad-anomalous-activity-reports"></a><span data-ttu-id="41e0d-150">Azure AD 異常活動報告</span><span class="sxs-lookup"><span data-stu-id="41e0d-150">Azure AD anomalous activity reports</span></span>

<span data-ttu-id="41e0d-151">Azure AD 異常活動的安全性已合併的 tooprovide hello Azure 傳統入口網站的報告。 您有一個中央檢視。</span><span class="sxs-lookup"><span data-stu-id="41e0d-151">Azure AD anomalous activity security reports from hello Azure classic portal have been consolidated tooprovide you with one, central view.</span></span> <span data-ttu-id="41e0d-152">此檢視顯示 Azure AD 可以偵測及作為報告依據的所有安全性相關風險事件。</span><span class="sxs-lookup"><span data-stu-id="41e0d-152">This view shows all security-related risk events that Azure AD can detect and report on.</span></span>

<span data-ttu-id="41e0d-153">hello 下表列出 hello Azure AD 異常活動安全性報表和 hello Azure 入口網站中的對應風險事件類型。</span><span class="sxs-lookup"><span data-stu-id="41e0d-153">hello following table lists hello Azure AD anomalous activity security reports, and corresponding risk event types in hello Azure portal.</span></span>

| <span data-ttu-id="41e0d-154">Azure AD 異常活動報告</span><span class="sxs-lookup"><span data-stu-id="41e0d-154">Azure AD anomalous activity report</span></span> |  <span data-ttu-id="41e0d-155">Identity Protection 風險事件類型</span><span class="sxs-lookup"><span data-stu-id="41e0d-155">Identity protection risk event type</span></span>|
| :--- | :--- |
| <span data-ttu-id="41e0d-156">認證外洩的使用者</span><span class="sxs-lookup"><span data-stu-id="41e0d-156">Users with leaked credentials</span></span> | <span data-ttu-id="41e0d-157">認證外洩</span><span class="sxs-lookup"><span data-stu-id="41e0d-157">Leaked credentials</span></span> |
| <span data-ttu-id="41e0d-158">異常的登入活動</span><span class="sxs-lookup"><span data-stu-id="41e0d-158">Irregular sign-in activity</span></span> | <span data-ttu-id="41e0d-159">不可能的旅遊 tooatypical 位置</span><span class="sxs-lookup"><span data-stu-id="41e0d-159">Impossible travel tooatypical locations</span></span> |
| <span data-ttu-id="41e0d-160">從可能受感染的裝置登入</span><span class="sxs-lookup"><span data-stu-id="41e0d-160">Sign-ins from possibly infected devices</span></span> | <span data-ttu-id="41e0d-161">從受感染的裝置登入</span><span class="sxs-lookup"><span data-stu-id="41e0d-161">Sign-ins from infected devices</span></span>|
| <span data-ttu-id="41e0d-162">從不明來源登入</span><span class="sxs-lookup"><span data-stu-id="41e0d-162">Sign-ins from unknown sources</span></span> | <span data-ttu-id="41e0d-163">從匿名 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="41e0d-163">Sign-ins from anonymous IP addresses</span></span> |
| <span data-ttu-id="41e0d-164">從具有可疑活動的 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="41e0d-164">Sign-ins from IP addresses with suspicious activity</span></span> | <span data-ttu-id="41e0d-165">從具有可疑活動的 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="41e0d-165">Sign-ins from IP addresses with suspicious activity</span></span> |
| - | <span data-ttu-id="41e0d-166">從不熟悉的位置登入</span><span class="sxs-lookup"><span data-stu-id="41e0d-166">Sign-ins from unfamiliar locations</span></span> |

<span data-ttu-id="41e0d-167">hello 下列 Azure AD 異常活動安全性報告不會包含為 hello Azure 入口網站中的風險事件：</span><span class="sxs-lookup"><span data-stu-id="41e0d-167">hello following Azure AD anomalous activity security reports are not included as risk events in hello Azure portal:</span></span>

* <span data-ttu-id="41e0d-168">在多次失敗後登入</span><span class="sxs-lookup"><span data-stu-id="41e0d-168">Sign-ins after multiple failures</span></span>
* <span data-ttu-id="41e0d-169">從多個地理區域登入</span><span class="sxs-lookup"><span data-stu-id="41e0d-169">Sign-ins from multiple geographies</span></span>

<span data-ttu-id="41e0d-170">這些報告就 hello Azure 傳統入口網站中仍然可用，但是將在未來的 hello 被取代。</span><span class="sxs-lookup"><span data-stu-id="41e0d-170">These reports are still available in hello Azure classic portal, but they will be deprecated at some time in hello future.</span></span>

<span data-ttu-id="41e0d-171">如需詳細資訊，請參閱 [Azure Active Directory 風險事件](active-directory-identity-protection-risk-events.md)。</span><span class="sxs-lookup"><span data-stu-id="41e0d-171">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>  


#### <a name="detected-risk-events"></a><span data-ttu-id="41e0d-172">偵測到的風險事件</span><span class="sxs-lookup"><span data-stu-id="41e0d-172">Detected risk events</span></span>

<span data-ttu-id="41e0d-173">在 hello Azure 入口網站，您可以存取有關偵測到的風險事件報告 hello **Azure Active Directory**刀鋒視窗底下**安全性**。</span><span class="sxs-lookup"><span data-stu-id="41e0d-173">In hello Azure portal, you can access reports about detected risk events on hello **Azure Active Directory** blade, under **SECURITY**.</span></span> <span data-ttu-id="41e0d-174">偵測到的風險事件會追蹤在 hello 下列報表：</span><span class="sxs-lookup"><span data-stu-id="41e0d-174">Detected risk events are tracked in hello following reports:</span></span>   

- <span data-ttu-id="41e0d-175">有風險的使用者</span><span class="sxs-lookup"><span data-stu-id="41e0d-175">Users at Risk</span></span>
- <span data-ttu-id="41e0d-176">有風險的登入</span><span class="sxs-lookup"><span data-stu-id="41e0d-176">Risky Sign-ins</span></span>

<span data-ttu-id="41e0d-177">![安全性報告](./media/active-directory-reporting-migration/04.png "安全性報告")</span><span class="sxs-lookup"><span data-stu-id="41e0d-177">![Security reports](./media/active-directory-reporting-migration/04.png "Security reports")</span></span>

<span data-ttu-id="41e0d-178">如需安全性報告的詳細資訊，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="41e0d-178">For more information about security reports, see:</span></span>

- [<span data-ttu-id="41e0d-179">使用者在風險中檢視 hello Azure Active Directory 入口網站的安全性報表</span><span class="sxs-lookup"><span data-stu-id="41e0d-179">Users at Risk security report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="41e0d-180">風險 hello Azure Active Directory 入口網站中的登入報表</span><span class="sxs-lookup"><span data-stu-id="41e0d-180">Risky Sign-ins report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)


## <a name="activity-reports-in-hello-azure-classic-portal-vs-hello-azure-portal"></a><span data-ttu-id="41e0d-181">在 [hello 與 hello Azure 入口網站的 Azure 傳統入口網站中的活動報告</span><span class="sxs-lookup"><span data-stu-id="41e0d-181">Activity reports in hello Azure classic portal vs. hello Azure portal</span></span>

<span data-ttu-id="41e0d-182">本節中的 hello 表格列出 hello Azure 傳統入口網站中的現有報表。</span><span class="sxs-lookup"><span data-stu-id="41e0d-182">hello table in this section lists existing reports in hello Azure classic portal.</span></span> <span data-ttu-id="41e0d-183">它也會說明如何取得 hello hello Azure 入口網站中的相同資訊。</span><span class="sxs-lookup"><span data-stu-id="41e0d-183">It also describes how you can get hello same information in hello Azure portal.</span></span>

<span data-ttu-id="41e0d-184">tooview 所有稽核資料，請在 [hello **Azure Active Directory**刀鋒視窗底下**活動**，跳過**稽核記錄檔**。</span><span class="sxs-lookup"><span data-stu-id="41e0d-184">tooview all auditing data, on hello **Azure Active Directory** blade, under **ACTIVITY**, go too**Audit logs**.</span></span>

<span data-ttu-id="41e0d-185">![稽核記錄](./media/active-directory-reporting-migration/61.png "稽核記錄")</span><span class="sxs-lookup"><span data-stu-id="41e0d-185">![Audit logs](./media/active-directory-reporting-migration/61.png "Audit logs")</span></span>

| <span data-ttu-id="41e0d-186">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="41e0d-186">Azure classic portal</span></span>                 | <span data-ttu-id="41e0d-187">toofind hello Azure 入口網站中</span><span class="sxs-lookup"><span data-stu-id="41e0d-187">toofind in hello Azure portal</span></span>                                                         |
| ---                                  | ---                                                                        |
| <span data-ttu-id="41e0d-188">稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="41e0d-188">Audit logs</span></span>                           | <span data-ttu-id="41e0d-189">選取 [核心目錄] 做為 [活動類別]。</span><span class="sxs-lookup"><span data-stu-id="41e0d-189">For **Activity Category**, select **Core Directory**.</span></span>                       |
| <span data-ttu-id="41e0d-190">密碼重設活動</span><span class="sxs-lookup"><span data-stu-id="41e0d-190">Password reset activity</span></span>              | <span data-ttu-id="41e0d-191">選取 [自助式密碼管理] 做為 [活動分類]。</span><span class="sxs-lookup"><span data-stu-id="41e0d-191">For **Activity Category**, select **Self-service Password Management**.</span></span> |
| <span data-ttu-id="41e0d-192">密碼重設註冊活動</span><span class="sxs-lookup"><span data-stu-id="41e0d-192">Password reset registration activity</span></span> | <span data-ttu-id="41e0d-193">選取 [自助式密碼管理] 做為 [活動分類]。</span><span class="sxs-lookup"><span data-stu-id="41e0d-193">For **Activity Category**, select **Self-service Password Management**.</span></span>     |
| <span data-ttu-id="41e0d-194">自助式群組活動</span><span class="sxs-lookup"><span data-stu-id="41e0d-194">Self-service groups activity</span></span>         | <span data-ttu-id="41e0d-195">選取 [自助式群組管理] 做為 [活動類別]。</span><span class="sxs-lookup"><span data-stu-id="41e0d-195">For **Activity Category**, select **Self-service Group Management**.</span></span>        |
| <span data-ttu-id="41e0d-196">帳戶佈建活動</span><span class="sxs-lookup"><span data-stu-id="41e0d-196">Account provisioning activity</span></span>        | <span data-ttu-id="41e0d-197">選取 [帳戶使用者佈建] 做為 [活動類別]。</span><span class="sxs-lookup"><span data-stu-id="41e0d-197">For **Activity Category**, select **Account User Provisioning**.</span></span>         |
| <span data-ttu-id="41e0d-198">密碼變換狀態</span><span class="sxs-lookup"><span data-stu-id="41e0d-198">Password rollover status</span></span>             | <span data-ttu-id="41e0d-199">選取 [自動應用程式密碼變換] 做為 [活動類別]。</span><span class="sxs-lookup"><span data-stu-id="41e0d-199">For **Activity Category**, select **Automatic App Password Rollover**.</span></span>      |
| <span data-ttu-id="41e0d-200">帳戶佈建錯誤</span><span class="sxs-lookup"><span data-stu-id="41e0d-200">Account provisioning errors</span></span>          | <span data-ttu-id="41e0d-201">選取 [帳戶使用者佈建] 做為 [活動類別]。</span><span class="sxs-lookup"><span data-stu-id="41e0d-201">For **Activity Category**, select **Account User Provisioning**.</span></span>        |
| <span data-ttu-id="41e0d-202">Office365 群組名稱變更</span><span class="sxs-lookup"><span data-stu-id="41e0d-202">Office365 Group Name Changes</span></span>         | <span data-ttu-id="41e0d-203">選取 [自助式密碼管理] 做為 [活動分類]。</span><span class="sxs-lookup"><span data-stu-id="41e0d-203">For **Activity Category**, select **Self-service Password Management**.</span></span> <span data-ttu-id="41e0d-204">選取 [群組] 做為 [活動資源類型]。</span><span class="sxs-lookup"><span data-stu-id="41e0d-204">For **Activity Resource Type**, select **Group**.</span></span> <span data-ttu-id="41e0d-205">選取 [O365 群組] 做為 [活動來源]。</span><span class="sxs-lookup"><span data-stu-id="41e0d-205">For **Activity Source**, select **O365 groups**.</span></span>|

<span data-ttu-id="41e0d-206">tooview hello**應用程式使用情形**報表，在 [hello **Azure Active Directory**刀鋒視窗底下**管理**，選取**企業應用程式**，然後選取**登入**。</span><span class="sxs-lookup"><span data-stu-id="41e0d-206">tooview hello **Application Usage** report, on hello **Azure Active Directory** blade, under **MANAGE**, select **Enterprise Applications**, and then select **Sign-ins**.</span></span>


<span data-ttu-id="41e0d-207">![企業應用程式登入報告](./media/active-directory-reporting-migration/199.png "企業應用程式登入報告")</span><span class="sxs-lookup"><span data-stu-id="41e0d-207">![Enterprise Applications Sign-Ins report](./media/active-directory-reporting-migration/199.png "Enterprise Applications Sign-Ins report")</span></span>

## <a name="next-steps"></a><span data-ttu-id="41e0d-208">後續步驟</span><span class="sxs-lookup"><span data-stu-id="41e0d-208">Next steps</span></span>

<span data-ttu-id="41e0d-209">如需報告的概觀，請參閱 hello [Azure Active Directory 報告](active-directory-reporting-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="41e0d-209">For an overview of reporting, see hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>
