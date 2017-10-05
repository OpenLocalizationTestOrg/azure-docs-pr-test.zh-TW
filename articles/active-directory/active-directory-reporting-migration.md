---
title: "在 Azure 入口網站中尋找活動報告 | Microsoft Docs"
description: "了解如何在 Azure 入口網站中尋找 Azure Active Directory 活動報告。"
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
ms.openlocfilehash: f1875582476c3817b9eb0082b6548cc15043cb98
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="find-activity-reports-in-the-azure-portal"></a><span data-ttu-id="f10ea-103">在 Azure 入口網站中尋找活動報告</span><span class="sxs-lookup"><span data-stu-id="f10ea-103">Find activity reports in the Azure portal</span></span>

<span data-ttu-id="f10ea-104">如果您從 Azure 傳統入口網站移轉到 Azure 入口網站，您可看到新的 Azure Active Directory 活動記錄風貌。</span><span class="sxs-lookup"><span data-stu-id="f10ea-104">If you are moving from the Azure classic portal to the Azure portal, you get a new look at Azure Active Directory (Azure AD) activity logs.</span></span> <span data-ttu-id="f10ea-105">在一篇近期的[部落格文章](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/)中，我們說明如何在 Azure 入口網站中您正在處理的資源內容中查看活動記錄。</span><span class="sxs-lookup"><span data-stu-id="f10ea-105">In a recent [blog post](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), we explain how you can see activity logs in the context of the resource you are working on in the Azure portal.</span></span> <span data-ttu-id="f10ea-106">在本文中，我們會說明如何在 Azure 入口網站中尋找您使用於 Azure 傳統入口網站的報告。</span><span class="sxs-lookup"><span data-stu-id="f10ea-106">In this article, we describe how to find reports that you used in the Azure classic portal in the Azure portal.</span></span>

## <a name="whats-new"></a><span data-ttu-id="f10ea-107">新功能</span><span class="sxs-lookup"><span data-stu-id="f10ea-107">What's new</span></span>

<span data-ttu-id="f10ea-108">Azure 傳統入口網站中的報告分為下列幾類：</span><span class="sxs-lookup"><span data-stu-id="f10ea-108">Reports in the Azure classic portal are separated into categories:</span></span>

1.  <span data-ttu-id="f10ea-109">安全性報告</span><span class="sxs-lookup"><span data-stu-id="f10ea-109">Security reports</span></span>
2.  <span data-ttu-id="f10ea-110">活動報告</span><span class="sxs-lookup"><span data-stu-id="f10ea-110">Activity reports</span></span>
3.  <span data-ttu-id="f10ea-111">整合式應用程式報告</span><span class="sxs-lookup"><span data-stu-id="f10ea-111">Integrated app reports</span></span>

### <a name="activity-and-integrated-app-reports"></a><span data-ttu-id="f10ea-112">活動和整合式應用程式報告</span><span class="sxs-lookup"><span data-stu-id="f10ea-112">Activity and integrated app reports</span></span>

<span data-ttu-id="f10ea-113">為了在 Azure 入口網站中進行以內容為基礎的報告，現有的報告會合併成單一檢視。</span><span class="sxs-lookup"><span data-stu-id="f10ea-113">For context-based reporting in the Azure portal, existing reports are merged into a single view.</span></span> <span data-ttu-id="f10ea-114">單一基礎 API 可提供此檢視的資料。</span><span class="sxs-lookup"><span data-stu-id="f10ea-114">A single, underlying API provides the data to the view.</span></span>

<span data-ttu-id="f10ea-115">若要查看這個檢視，請在 [Azure Active Directory] 刀鋒視窗的 [活動] 之下，選取 [稽核記錄]。</span><span class="sxs-lookup"><span data-stu-id="f10ea-115">To see this view, on the **Azure Active Directory** blade, under **ACTIVITY**, select **Audit logs**.</span></span>

<span data-ttu-id="f10ea-116">![稽核記錄](./media/active-directory-reporting-migration/482.png "稽核記錄")</span><span class="sxs-lookup"><span data-stu-id="f10ea-116">![Audit logs](./media/active-directory-reporting-migration/482.png "Audit logs")</span></span>

<span data-ttu-id="f10ea-117">下列報告會整合在此檢視中：</span><span class="sxs-lookup"><span data-stu-id="f10ea-117">The following reports are consolidated in this view:</span></span>

-   <span data-ttu-id="f10ea-118">稽核報告</span><span class="sxs-lookup"><span data-stu-id="f10ea-118">Audit report</span></span>
-   <span data-ttu-id="f10ea-119">密碼重設活動</span><span class="sxs-lookup"><span data-stu-id="f10ea-119">Password reset activity</span></span>
-   <span data-ttu-id="f10ea-120">密碼重設註冊活動</span><span class="sxs-lookup"><span data-stu-id="f10ea-120">Password reset registration activity</span></span>
-   <span data-ttu-id="f10ea-121">自助式群組活動</span><span class="sxs-lookup"><span data-stu-id="f10ea-121">Self-service groups activity</span></span>
-   <span data-ttu-id="f10ea-122">Office365 群組名稱變更</span><span class="sxs-lookup"><span data-stu-id="f10ea-122">Office365 Group Name Changes</span></span>
-   <span data-ttu-id="f10ea-123">帳戶佈建活動</span><span class="sxs-lookup"><span data-stu-id="f10ea-123">Account provisioning activity</span></span>
-   <span data-ttu-id="f10ea-124">密碼變換狀態</span><span class="sxs-lookup"><span data-stu-id="f10ea-124">Password rollover status</span></span>
-   <span data-ttu-id="f10ea-125">帳戶佈建錯誤</span><span class="sxs-lookup"><span data-stu-id="f10ea-125">Account provisioning errors</span></span>


<span data-ttu-id="f10ea-126">[應用程式使用量] 報告已增強並包含於 [登入] 檢視中。</span><span class="sxs-lookup"><span data-stu-id="f10ea-126">The Application Usage report has been enhanced and is included in the **Sign-ins** view.</span></span> <span data-ttu-id="f10ea-127">若要查看這個檢視，請在 [Azure Active Directory] 刀鋒視窗的 [活動] 之下，選取 [登入]。</span><span class="sxs-lookup"><span data-stu-id="f10ea-127">To see this view, on the **Azure Active Directory** blade, under **ACTIVITY**, select **Sign-ins**.</span></span>

<span data-ttu-id="f10ea-128">![登入檢視](./media/active-directory-reporting-migration/483.png "登入檢視")</span><span class="sxs-lookup"><span data-stu-id="f10ea-128">![Sign-ins view](./media/active-directory-reporting-migration/483.png "Sign-ins view")</span></span>

<span data-ttu-id="f10ea-129">[登入] 檢視包含所有使用者登入。</span><span class="sxs-lookup"><span data-stu-id="f10ea-129">The **Sign-ins** view includes all user sign-ins.</span></span> <span data-ttu-id="f10ea-130">您可以利用這項資訊來取得應用程式使用量資訊。</span><span class="sxs-lookup"><span data-stu-id="f10ea-130">You can use this information to get application usage information.</span></span> <span data-ttu-id="f10ea-131">您也可以在 [企業應用程式] 概觀的 [管理] 區段中檢視應用程式使用量資訊。</span><span class="sxs-lookup"><span data-stu-id="f10ea-131">You also can view application usage information in the **Enterprise applications** overview, in the **MANAGE** section.</span></span>

<span data-ttu-id="f10ea-132">![企業應用程式](./media/active-directory-reporting-migration/484.png "企業應用程式")</span><span class="sxs-lookup"><span data-stu-id="f10ea-132">![Enterprise applications](./media/active-directory-reporting-migration/484.png "Enterprise applications")</span></span>

## <a name="access-a-specific-report"></a><span data-ttu-id="f10ea-133">存取特定報告</span><span class="sxs-lookup"><span data-stu-id="f10ea-133">Access a specific report</span></span>

<span data-ttu-id="f10ea-134">雖然 Azure 入口網站提供了單一檢視，但您也可以查看特定報告。</span><span class="sxs-lookup"><span data-stu-id="f10ea-134">Although the Azure portal offers a single view, you also can look at specific reports.</span></span>

### <a name="audit-logs"></a><span data-ttu-id="f10ea-135">稽核記錄</span><span class="sxs-lookup"><span data-stu-id="f10ea-135">Audit logs</span></span>

<span data-ttu-id="f10ea-136">為了回應客戶的意見反應，您可以在 Azure 入口網站中使用進階篩選來存取想要的資料。</span><span class="sxs-lookup"><span data-stu-id="f10ea-136">In response to customer feedback, in the Azure portal, you can use advanced filtering to access the data you want.</span></span> <span data-ttu-id="f10ea-137">您可以使用的其中一個篩選是「活動類別」，它會列出 Azure AD 中的各種活動記錄。</span><span class="sxs-lookup"><span data-stu-id="f10ea-137">One filter you can use is an *activity category*, which lists the different types of activity logs in Azure AD.</span></span> <span data-ttu-id="f10ea-138">若要縮小您要尋找的結果範圍，您可以選取一個類別。</span><span class="sxs-lookup"><span data-stu-id="f10ea-138">To narrow results to what you are looking for, you can select a category.</span></span>

<span data-ttu-id="f10ea-139">例如，如果您只對取得自助式密碼重設相關活動感興趣，您可以選擇 [自助式密碼管理] 類別。</span><span class="sxs-lookup"><span data-stu-id="f10ea-139">For example, if you are interested only in activities related to self-service password resets, you can choose the **Self-service Password Management** category.</span></span> <span data-ttu-id="f10ea-140">您可看見的類別取決於您正在處理的資源。</span><span class="sxs-lookup"><span data-stu-id="f10ea-140">The categories you see are based on the resource you are working in.</span></span>  

<span data-ttu-id="f10ea-141">![[篩選稽核記錄] 頁面上的類別選項](./media/active-directory-reporting-migration/06.png "[篩選稽核記錄] 頁面上的類別選項")</span><span class="sxs-lookup"><span data-stu-id="f10ea-141">![Category options on the Filter Audit Logs page](./media/active-directory-reporting-migration/06.png "Category options on the Filter Audit Logs page")</span></span>

<span data-ttu-id="f10ea-142">活動類別包括︰</span><span class="sxs-lookup"><span data-stu-id="f10ea-142">Activity categories include:</span></span>

- <span data-ttu-id="f10ea-143">核心目錄</span><span class="sxs-lookup"><span data-stu-id="f10ea-143">Core Directory</span></span>
- <span data-ttu-id="f10ea-144">自助式密碼管理</span><span class="sxs-lookup"><span data-stu-id="f10ea-144">Self-service Password Management</span></span>
- <span data-ttu-id="f10ea-145">自助式群組管理</span><span class="sxs-lookup"><span data-stu-id="f10ea-145">Self-service Group Management</span></span>
- <span data-ttu-id="f10ea-146">帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="f10ea-146">Account Provisioning</span></span>

### <a name="application-usage"></a><span data-ttu-id="f10ea-147">應用程式使用情況</span><span class="sxs-lookup"><span data-stu-id="f10ea-147">Application usage</span></span>

<span data-ttu-id="f10ea-148">若要檢視所有應用程式或單一應用程式的應用程式使用量詳細資料，請在 [活動] 之下選取 [登入]。</span><span class="sxs-lookup"><span data-stu-id="f10ea-148">To view details about application usage for all apps or for a single app, under **ACTIVITY**, select **Sign-ins**.</span></span> <span data-ttu-id="f10ea-149">若要縮小結果範圍，您可以依據使用者名稱或應用程式名稱進行篩選。</span><span class="sxs-lookup"><span data-stu-id="f10ea-149">To narrow the results, you can filter on user name or application name.</span></span>

<span data-ttu-id="f10ea-150">![[篩選登入事件] 頁面](./media/active-directory-reporting-migration/07.png "[篩選登入事件] 頁面")</span><span class="sxs-lookup"><span data-stu-id="f10ea-150">![Filter Sign-In Events page](./media/active-directory-reporting-migration/07.png "Filter Sign-In Events page")</span></span>

### <a name="security-reports"></a><span data-ttu-id="f10ea-151">安全性報告</span><span class="sxs-lookup"><span data-stu-id="f10ea-151">Security reports</span></span>

#### <a name="azure-ad-anomalous-activity-reports"></a><span data-ttu-id="f10ea-152">Azure AD 異常活動報告</span><span class="sxs-lookup"><span data-stu-id="f10ea-152">Azure AD anomalous activity reports</span></span>

<span data-ttu-id="f10ea-153">來自 Azure 傳統入口網站的 Azure AD 異常活動安全性報告已經合併，可為您提供一個集中檢視。</span><span class="sxs-lookup"><span data-stu-id="f10ea-153">Azure AD anomalous activity security reports from the Azure classic portal have been consolidated to provide you with one, central view.</span></span> <span data-ttu-id="f10ea-154">此檢視顯示 Azure AD 可以偵測及作為報告依據的所有安全性相關風險事件。</span><span class="sxs-lookup"><span data-stu-id="f10ea-154">This view shows all security-related risk events that Azure AD can detect and report on.</span></span>

<span data-ttu-id="f10ea-155">下表列出 Azure 入口網站中的 Azure AD 異常活動安全性報告，以及對應的風險事件類型。</span><span class="sxs-lookup"><span data-stu-id="f10ea-155">The following table lists the Azure AD anomalous activity security reports, and corresponding risk event types in the Azure portal.</span></span>

| <span data-ttu-id="f10ea-156">Azure AD 異常活動報告</span><span class="sxs-lookup"><span data-stu-id="f10ea-156">Azure AD anomalous activity report</span></span> |  <span data-ttu-id="f10ea-157">Identity Protection 風險事件類型</span><span class="sxs-lookup"><span data-stu-id="f10ea-157">Identity protection risk event type</span></span>|
| :--- | :--- |
| <span data-ttu-id="f10ea-158">認證外洩的使用者</span><span class="sxs-lookup"><span data-stu-id="f10ea-158">Users with leaked credentials</span></span> | <span data-ttu-id="f10ea-159">認證外洩</span><span class="sxs-lookup"><span data-stu-id="f10ea-159">Leaked credentials</span></span> |
| <span data-ttu-id="f10ea-160">異常的登入活動</span><span class="sxs-lookup"><span data-stu-id="f10ea-160">Irregular sign-in activity</span></span> | <span data-ttu-id="f10ea-161">不可能到達非典型位置的移動</span><span class="sxs-lookup"><span data-stu-id="f10ea-161">Impossible travel to atypical locations</span></span> |
| <span data-ttu-id="f10ea-162">從可能受感染的裝置登入</span><span class="sxs-lookup"><span data-stu-id="f10ea-162">Sign-ins from possibly infected devices</span></span> | <span data-ttu-id="f10ea-163">從受感染的裝置登入</span><span class="sxs-lookup"><span data-stu-id="f10ea-163">Sign-ins from infected devices</span></span>|
| <span data-ttu-id="f10ea-164">從不明來源登入</span><span class="sxs-lookup"><span data-stu-id="f10ea-164">Sign-ins from unknown sources</span></span> | <span data-ttu-id="f10ea-165">從匿名 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="f10ea-165">Sign-ins from anonymous IP addresses</span></span> |
| <span data-ttu-id="f10ea-166">從具有可疑活動的 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="f10ea-166">Sign-ins from IP addresses with suspicious activity</span></span> | <span data-ttu-id="f10ea-167">從具有可疑活動的 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="f10ea-167">Sign-ins from IP addresses with suspicious activity</span></span> |
| - | <span data-ttu-id="f10ea-168">從不熟悉的位置登入</span><span class="sxs-lookup"><span data-stu-id="f10ea-168">Sign-ins from unfamiliar locations</span></span> |

<span data-ttu-id="f10ea-169">下列 Azure AD 異常活動安全性報告並未包含在 Azure 入口網站的風險事件中：</span><span class="sxs-lookup"><span data-stu-id="f10ea-169">The following Azure AD anomalous activity security reports are not included as risk events in the Azure portal:</span></span>

* <span data-ttu-id="f10ea-170">在多次失敗後登入</span><span class="sxs-lookup"><span data-stu-id="f10ea-170">Sign-ins after multiple failures</span></span>
* <span data-ttu-id="f10ea-171">從多個地理區域登入</span><span class="sxs-lookup"><span data-stu-id="f10ea-171">Sign-ins from multiple geographies</span></span>

<span data-ttu-id="f10ea-172">這些報告仍可在 Azure 傳統入口網站中取得，但是將會在未來某個時候淘汰。</span><span class="sxs-lookup"><span data-stu-id="f10ea-172">These reports are still available in the Azure classic portal, but they will be deprecated at some time in the future.</span></span>

<span data-ttu-id="f10ea-173">如需詳細資訊，請參閱 [Azure Active Directory 風險事件](active-directory-identity-protection-risk-events.md)。</span><span class="sxs-lookup"><span data-stu-id="f10ea-173">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>  


#### <a name="detected-risk-events"></a><span data-ttu-id="f10ea-174">偵測到的風險事件</span><span class="sxs-lookup"><span data-stu-id="f10ea-174">Detected risk events</span></span>

<span data-ttu-id="f10ea-175">在 Azure 入口網站中，您可以在 [Azure Active Directory] 刀鋒視窗的 [安全性] 之下，存取所偵測到之風險事件的相關報告。</span><span class="sxs-lookup"><span data-stu-id="f10ea-175">In the Azure portal, you can access reports about detected risk events on the **Azure Active Directory** blade, under **SECURITY**.</span></span> <span data-ttu-id="f10ea-176">偵測到的風險事件會在下列報告中進行追蹤︰</span><span class="sxs-lookup"><span data-stu-id="f10ea-176">Detected risk events are tracked in the following reports:</span></span>   

- <span data-ttu-id="f10ea-177">有風險的使用者</span><span class="sxs-lookup"><span data-stu-id="f10ea-177">Users at Risk</span></span>
- <span data-ttu-id="f10ea-178">有風險的登入</span><span class="sxs-lookup"><span data-stu-id="f10ea-178">Risky Sign-ins</span></span>

<span data-ttu-id="f10ea-179">![安全性報告](./media/active-directory-reporting-migration/04.png "安全性報告")</span><span class="sxs-lookup"><span data-stu-id="f10ea-179">![Security reports](./media/active-directory-reporting-migration/04.png "Security reports")</span></span>

<span data-ttu-id="f10ea-180">如需安全性報告的詳細資訊，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="f10ea-180">For more information about security reports, see:</span></span>

- [<span data-ttu-id="f10ea-181">Azure Active Directory 入口網站中有風險使用者的安全性報告</span><span class="sxs-lookup"><span data-stu-id="f10ea-181">Users at Risk security report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="f10ea-182">Azure Active Directory 入口網站中有風險的登入報告</span><span class="sxs-lookup"><span data-stu-id="f10ea-182">Risky Sign-ins report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)


## <a name="activity-reports-in-the-azure-classic-portal-vs-the-azure-portal"></a><span data-ttu-id="f10ea-183">Azure 傳統入口網站與 Azure 入口網站中活動報告的比較</span><span class="sxs-lookup"><span data-stu-id="f10ea-183">Activity reports in the Azure classic portal vs. the Azure portal</span></span>

<span data-ttu-id="f10ea-184">本節中的表格會列出 Azure 傳統入口網站的現有報表。</span><span class="sxs-lookup"><span data-stu-id="f10ea-184">The table in this section lists existing reports in the Azure classic portal.</span></span> <span data-ttu-id="f10ea-185">此外也說明如何在 Azure 入口網站中取得相同的資訊。</span><span class="sxs-lookup"><span data-stu-id="f10ea-185">It also describes how you can get the same information in the Azure portal.</span></span>

<span data-ttu-id="f10ea-186">若要檢視所有稽核資料，請在 [Azure Active Directory] 刀鋒視窗的 [活動] 之下，移至 [稽核記錄]。</span><span class="sxs-lookup"><span data-stu-id="f10ea-186">To view all auditing data, on the **Azure Active Directory** blade, under **ACTIVITY**, go to **Audit logs**.</span></span>

<span data-ttu-id="f10ea-187">![稽核記錄](./media/active-directory-reporting-migration/61.png "稽核記錄")</span><span class="sxs-lookup"><span data-stu-id="f10ea-187">![Audit logs](./media/active-directory-reporting-migration/61.png "Audit logs")</span></span>

| <span data-ttu-id="f10ea-188">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="f10ea-188">Azure classic portal</span></span>                 | <span data-ttu-id="f10ea-189">在 Azure 入口網站中尋找</span><span class="sxs-lookup"><span data-stu-id="f10ea-189">To find in the Azure portal</span></span>                                                         |
| ---                                  | ---                                                                        |
| <span data-ttu-id="f10ea-190">稽核記錄</span><span class="sxs-lookup"><span data-stu-id="f10ea-190">Audit logs</span></span>                           | <span data-ttu-id="f10ea-191">選取 [核心目錄] 做為 [活動類別]。</span><span class="sxs-lookup"><span data-stu-id="f10ea-191">For **Activity Category**, select **Core Directory**.</span></span>                       |
| <span data-ttu-id="f10ea-192">密碼重設活動</span><span class="sxs-lookup"><span data-stu-id="f10ea-192">Password reset activity</span></span>              | <span data-ttu-id="f10ea-193">選取 [自助式密碼管理] 做為 [活動分類]。</span><span class="sxs-lookup"><span data-stu-id="f10ea-193">For **Activity Category**, select **Self-service Password Management**.</span></span> |
| <span data-ttu-id="f10ea-194">密碼重設註冊活動</span><span class="sxs-lookup"><span data-stu-id="f10ea-194">Password reset registration activity</span></span> | <span data-ttu-id="f10ea-195">選取 [自助式密碼管理] 做為 [活動分類]。</span><span class="sxs-lookup"><span data-stu-id="f10ea-195">For **Activity Category**, select **Self-service Password Management**.</span></span>     |
| <span data-ttu-id="f10ea-196">自助式群組活動</span><span class="sxs-lookup"><span data-stu-id="f10ea-196">Self-service groups activity</span></span>         | <span data-ttu-id="f10ea-197">選取 [自助式群組管理] 做為 [活動類別]。</span><span class="sxs-lookup"><span data-stu-id="f10ea-197">For **Activity Category**, select **Self-service Group Management**.</span></span>        |
| <span data-ttu-id="f10ea-198">帳戶佈建活動</span><span class="sxs-lookup"><span data-stu-id="f10ea-198">Account provisioning activity</span></span>        | <span data-ttu-id="f10ea-199">選取 [帳戶使用者佈建] 做為 [活動類別]。</span><span class="sxs-lookup"><span data-stu-id="f10ea-199">For **Activity Category**, select **Account User Provisioning**.</span></span>         |
| <span data-ttu-id="f10ea-200">密碼變換狀態</span><span class="sxs-lookup"><span data-stu-id="f10ea-200">Password rollover status</span></span>             | <span data-ttu-id="f10ea-201">選取 [自動應用程式密碼變換] 做為 [活動類別]。</span><span class="sxs-lookup"><span data-stu-id="f10ea-201">For **Activity Category**, select **Automatic App Password Rollover**.</span></span>      |
| <span data-ttu-id="f10ea-202">帳戶佈建錯誤</span><span class="sxs-lookup"><span data-stu-id="f10ea-202">Account provisioning errors</span></span>          | <span data-ttu-id="f10ea-203">選取 [帳戶使用者佈建] 做為 [活動類別]。</span><span class="sxs-lookup"><span data-stu-id="f10ea-203">For **Activity Category**, select **Account User Provisioning**.</span></span>        |
| <span data-ttu-id="f10ea-204">Office365 群組名稱變更</span><span class="sxs-lookup"><span data-stu-id="f10ea-204">Office365 Group Name Changes</span></span>         | <span data-ttu-id="f10ea-205">選取 [自助式密碼管理] 做為 [活動分類]。</span><span class="sxs-lookup"><span data-stu-id="f10ea-205">For **Activity Category**, select **Self-service Password Management**.</span></span> <span data-ttu-id="f10ea-206">選取 [群組] 做為 [活動資源類型]。</span><span class="sxs-lookup"><span data-stu-id="f10ea-206">For **Activity Resource Type**, select **Group**.</span></span> <span data-ttu-id="f10ea-207">選取 [O365 群組] 做為 [活動來源]。</span><span class="sxs-lookup"><span data-stu-id="f10ea-207">For **Activity Source**, select **O365 groups**.</span></span>|

<span data-ttu-id="f10ea-208">若要檢視 [應用程式使用量] 報告，請在 [Azure Active Directory] 刀鋒視窗的 [管理] 之下，依序選取 [企業應用程式] 和 [登入]。</span><span class="sxs-lookup"><span data-stu-id="f10ea-208">To view the **Application Usage** report, on the **Azure Active Directory** blade, under **MANAGE**, select **Enterprise Applications**, and then select **Sign-ins**.</span></span>


<span data-ttu-id="f10ea-209">![企業應用程式登入報告](./media/active-directory-reporting-migration/199.png "企業應用程式登入報告")</span><span class="sxs-lookup"><span data-stu-id="f10ea-209">![Enterprise Applications Sign-Ins report](./media/active-directory-reporting-migration/199.png "Enterprise Applications Sign-Ins report")</span></span>

## <a name="next-steps"></a><span data-ttu-id="f10ea-210">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f10ea-210">Next steps</span></span>

<span data-ttu-id="f10ea-211">如需報告概觀，請參閱 [Azure Active Directory 報告](active-directory-reporting-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="f10ea-211">For an overview of reporting, see the [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>
