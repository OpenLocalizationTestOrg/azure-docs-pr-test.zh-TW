---
title: "Azure Active Directory 報告：開始使用 | Microsoft Docs"
description: "在 Azure Active Directory 報告列出各種可用的報告"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 7ac99919-8df5-4424-9298-fc7c025ba949
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 5cd1ae6196d9cd63f97dc9d302442280ece23e40
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-active-directory-reporting"></a><span data-ttu-id="d2704-103">開始使用 Azure Active Directory 報告</span><span class="sxs-lookup"><span data-stu-id="d2704-103">Getting started with Azure Active Directory Reporting</span></span>
## <a name="what-it-is"></a><span data-ttu-id="d2704-104">內容</span><span class="sxs-lookup"><span data-stu-id="d2704-104">What it is</span></span>
<span data-ttu-id="d2704-105">Azure Active Directory (Azure AD) 包括您的目錄的安全性、活動和稽核報告。</span><span class="sxs-lookup"><span data-stu-id="d2704-105">Azure Active Directory (Azure AD) includes security, activity, and audit reports for your directory.</span></span> <span data-ttu-id="d2704-106">以下是包含的報告清單：</span><span class="sxs-lookup"><span data-stu-id="d2704-106">Here's a list of the reports included:</span></span>

### <a name="security-reports"></a><span data-ttu-id="d2704-107">安全性報告</span><span class="sxs-lookup"><span data-stu-id="d2704-107">Security reports</span></span>
* <span data-ttu-id="d2704-108">從不明來源登入</span><span class="sxs-lookup"><span data-stu-id="d2704-108">Sign-ins from unknown sources</span></span>
* <span data-ttu-id="d2704-109">在多次失敗後登入</span><span class="sxs-lookup"><span data-stu-id="d2704-109">Sign-ins after multiple failures</span></span>
* <span data-ttu-id="d2704-110">從多個地理區域登入</span><span class="sxs-lookup"><span data-stu-id="d2704-110">Sign-ins from multiple geographies</span></span>
* <span data-ttu-id="d2704-111">從具有可疑活動的 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="d2704-111">Sign-ins from IP addresses with suspicious activity</span></span>
* <span data-ttu-id="d2704-112">異常的登入活動</span><span class="sxs-lookup"><span data-stu-id="d2704-112">Irregular sign-in activity</span></span>
* <span data-ttu-id="d2704-113">從可能受感染的裝置登入</span><span class="sxs-lookup"><span data-stu-id="d2704-113">Sign-ins from possibly infected devices</span></span>
* <span data-ttu-id="d2704-114">具有異常登入活動的使用者</span><span class="sxs-lookup"><span data-stu-id="d2704-114">Users with anomalous sign-in activity</span></span>

### <a name="activity-reports"></a><span data-ttu-id="d2704-115">活動報告</span><span class="sxs-lookup"><span data-stu-id="d2704-115">Activity reports</span></span>
* <span data-ttu-id="d2704-116">應用程式使用情況：摘要</span><span class="sxs-lookup"><span data-stu-id="d2704-116">Application usage: summary</span></span>
* <span data-ttu-id="d2704-117">應用程式使用情況：詳細</span><span class="sxs-lookup"><span data-stu-id="d2704-117">Application usage: detailed</span></span>
* <span data-ttu-id="d2704-118">應用程式儀表板</span><span class="sxs-lookup"><span data-stu-id="d2704-118">Application dashboard</span></span>
* <span data-ttu-id="d2704-119">帳戶佈建錯誤</span><span class="sxs-lookup"><span data-stu-id="d2704-119">Account provisioning errors</span></span>
* <span data-ttu-id="d2704-120">個別使用者裝置</span><span class="sxs-lookup"><span data-stu-id="d2704-120">Individual user devices</span></span>
* <span data-ttu-id="d2704-121">個別使用者活動</span><span class="sxs-lookup"><span data-stu-id="d2704-121">Individual user Activity</span></span>
* <span data-ttu-id="d2704-122">群組活動報告</span><span class="sxs-lookup"><span data-stu-id="d2704-122">Groups activity report</span></span>
* <span data-ttu-id="d2704-123">密碼重設登錄活動報告</span><span class="sxs-lookup"><span data-stu-id="d2704-123">Password Reset Registration Activity Report</span></span>
* <span data-ttu-id="d2704-124">密碼重設活動</span><span class="sxs-lookup"><span data-stu-id="d2704-124">Password reset activity</span></span>

### <a name="audit-reports"></a><span data-ttu-id="d2704-125">稽核報告</span><span class="sxs-lookup"><span data-stu-id="d2704-125">Audit reports</span></span>
* <span data-ttu-id="d2704-126">目錄稽核報告</span><span class="sxs-lookup"><span data-stu-id="d2704-126">Directory audit report</span></span>

> [!TIP]
> <span data-ttu-id="d2704-127">如需有關 Azure AD 報告的更多文件，請參閱 [檢視存取和使用情況報告](active-directory-view-access-usage-reports.md)。</span><span class="sxs-lookup"><span data-stu-id="d2704-127">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="how-it-works"></a><span data-ttu-id="d2704-128">運作方式</span><span class="sxs-lookup"><span data-stu-id="d2704-128">How it works</span></span>
### <a name="reporting-pipeline"></a><span data-ttu-id="d2704-129">報告管線</span><span class="sxs-lookup"><span data-stu-id="d2704-129">Reporting pipeline</span></span>
<span data-ttu-id="d2704-130">報告管線包含三個主要步驟。</span><span class="sxs-lookup"><span data-stu-id="d2704-130">The reporting pipeline consists of three main steps.</span></span> <span data-ttu-id="d2704-131">每次使用者登入或進行驗證時，就會發生以下狀況：</span><span class="sxs-lookup"><span data-stu-id="d2704-131">Every time a user signs in, or an authentication is made, the following happens:</span></span>

* <span data-ttu-id="d2704-132">首先，使用者會經過驗證 (成功或失敗)，結果會儲存在 Azure Active Directory 服務資料庫。</span><span class="sxs-lookup"><span data-stu-id="d2704-132">First, the user is authenticated (successfully or unsuccessfully), and the result is stored in the Azure Active Directory service databases.</span></span>
* <span data-ttu-id="d2704-133">每隔一段固定時間，就會處理所有最近的登入。</span><span class="sxs-lookup"><span data-stu-id="d2704-133">At regular intervals, all recent sign ins are processed.</span></span> <span data-ttu-id="d2704-134">此時，我們的安全性和異常活動演算法會搜尋所有最近的登入找出是否有可疑的活動。</span><span class="sxs-lookup"><span data-stu-id="d2704-134">At this point, our security and anomalous activity algorithms are searching all recent sign ins for suspicious activity.</span></span>
* <span data-ttu-id="d2704-135">處理之後，就會寫入報告、快取報告，然後在 Azure 傳統入口網站中提供報告。</span><span class="sxs-lookup"><span data-stu-id="d2704-135">After processing, the reports are written, cached, and served in the Azure classic portal.</span></span>

### <a name="report-generation-times"></a><span data-ttu-id="d2704-136">報告產生時間</span><span class="sxs-lookup"><span data-stu-id="d2704-136">Report generation times</span></span>
<span data-ttu-id="d2704-137">由於 Azure AD 平台需處理大量的驗證和登入，所處理的最近登入平均而言為過去一小時。</span><span class="sxs-lookup"><span data-stu-id="d2704-137">Due to the large volume of authentications and sign ins processed by the Azure AD platform, the most recent sign-ins processed are, on average, one hour old.</span></span> <span data-ttu-id="d2704-138">在罕見的情況下，可能需要花費多達 8 小時處理最近的登入。</span><span class="sxs-lookup"><span data-stu-id="d2704-138">In rare cases, it may take up to 8 hours to process the most recent sign-ins.</span></span>

<span data-ttu-id="d2704-139">您可以查看每個報告頂端的說明文字，找到最近處理的登入。</span><span class="sxs-lookup"><span data-stu-id="d2704-139">You can find the most recent processed sign-in by examining the help text at the top of each report.</span></span>

![每個報告頂端的說明文字](./media/active-directory-reporting-getting-started/reportingWatermark.PNG)

> [!TIP]
> <span data-ttu-id="d2704-141">如需有關 Azure AD 報告的更多文件，請參閱 [檢視存取和使用情況報告](active-directory-view-access-usage-reports.md)。</span><span class="sxs-lookup"><span data-stu-id="d2704-141">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="getting-started"></a><span data-ttu-id="d2704-142">開始使用</span><span class="sxs-lookup"><span data-stu-id="d2704-142">Getting started</span></span>
### <a name="sign-into-the-azure-classic-portal"></a><span data-ttu-id="d2704-143">登入 Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="d2704-143">Sign into the Azure classic portal</span></span>
<span data-ttu-id="d2704-144">首先，您必須以全域或相容性管理員身分登入 [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="d2704-144">First, you'll need to sign into the [Azure classic portal](https://manage.windowsazure.com)  as a global or compliance administrator.</span></span> <span data-ttu-id="d2704-145">您也必須是 Azure 訂用帳戶服務管理員或共同管理員，或使用「存取 Azure AD」的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d2704-145">You must also be an Azure subscription service administrator or co-administrator, or be using the "Access to Azure AD" Azure subscription.</span></span>

### <a name="navigate-to-reports"></a><span data-ttu-id="d2704-146">瀏覽至報告</span><span class="sxs-lookup"><span data-stu-id="d2704-146">Navigate to Reports</span></span>
<span data-ttu-id="d2704-147">若要檢視報告，請瀏覽至目錄頂端的 [報告] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="d2704-147">To view Reports, navigate to the Reports tab at the top of your directory.</span></span>

<span data-ttu-id="d2704-148">如果這是您第一次檢視報告，您必須先同意對話方塊，才能檢視報告。</span><span class="sxs-lookup"><span data-stu-id="d2704-148">If this is your first time viewing the reports, you'll need to agree to a dialog box before you can view the reports.</span></span> <span data-ttu-id="d2704-149">這是為了確保在您的組織中可接受讓管理員檢視這項資料，在某些國家/地區，這些資料可能會被視為隱私資訊。</span><span class="sxs-lookup"><span data-stu-id="d2704-149">This is to ensure that it's acceptable for admins in your organization to view this data, which may be considered private information in some countries.</span></span>

![對話方塊](./media/active-directory-reporting-getting-started/dialogBox.png)

### <a name="explore-each-report"></a><span data-ttu-id="d2704-151">瀏覽每個報告</span><span class="sxs-lookup"><span data-stu-id="d2704-151">Explore each report</span></span>
<span data-ttu-id="d2704-152">瀏覽每個報告以查看收集的資料，以及處理的登入。</span><span class="sxs-lookup"><span data-stu-id="d2704-152">Navigate into each report to see the data being collected and the sign-ins processed.</span></span> <span data-ttu-id="d2704-153">您可以 [在此找到所有報告的清單](active-directory-reporting-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="d2704-153">You can find a [list of all the reports here](active-directory-reporting-guide.md).</span></span>

![所有報告](./media/active-directory-reporting-getting-started/reportsMain.png)

### <a name="download-the-reports-as-csv"></a><span data-ttu-id="d2704-155">下載報告為 CSV</span><span class="sxs-lookup"><span data-stu-id="d2704-155">Download the reports as CSV</span></span>
<span data-ttu-id="d2704-156">每個報告可以下載為 CSV (逗號分隔值) 檔案。</span><span class="sxs-lookup"><span data-stu-id="d2704-156">Each report can be downloaded as a CSV (comma-separated value) file.</span></span> <span data-ttu-id="d2704-157">您可以在 Excel、PowerBI 或協力廠商分析程式中使用這些檔案，進一步分析您的資料。</span><span class="sxs-lookup"><span data-stu-id="d2704-157">You can use these files in Excel, PowerBI or third-party analysis programs to further analyze your data.</span></span>

<span data-ttu-id="d2704-158">若要下載任何報告為 CSV，請瀏覽至報告並按一下底部的 [下載]。</span><span class="sxs-lookup"><span data-stu-id="d2704-158">To download any report as a CSV, navigate to the report and click "Download" at the bottom.</span></span>

![[下載] 按鈕](./media/active-directory-reporting-getting-started/downloadButton.png)

> [!TIP]
> <span data-ttu-id="d2704-160">如需有關 Azure AD 報告的更多文件，請參閱 [檢視存取和使用情況報告](active-directory-view-access-usage-reports.md)。</span><span class="sxs-lookup"><span data-stu-id="d2704-160">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="d2704-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d2704-161">Next steps</span></span>
### <a name="customize-alerts-for-anomalous-sign-in-activity"></a><span data-ttu-id="d2704-162">自訂異常登入活動的警示</span><span class="sxs-lookup"><span data-stu-id="d2704-162">Customize alerts for anomalous sign in activity</span></span>
<span data-ttu-id="d2704-163">瀏覽至您目錄的 [設定] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="d2704-163">Navigate to the "Configure" tab of your directory.</span></span>

<span data-ttu-id="d2704-164">捲動到 [通知] 區段。</span><span class="sxs-lookup"><span data-stu-id="d2704-164">Scroll to the "Notifications" section.</span></span>

<span data-ttu-id="d2704-165">啟用或停用 [惡意登入的電子郵件通知] 區段。</span><span class="sxs-lookup"><span data-stu-id="d2704-165">Enable or disable the "Email Notifications of Anomalous sign-ins" section.</span></span>

![[通知] 區段](./media/active-directory-reporting-getting-started/notificationsSection.png)

### <a name="integrate-with-the-azure-ad-reporting-api"></a><span data-ttu-id="d2704-167">與 Azure AD 報告 API 整合</span><span class="sxs-lookup"><span data-stu-id="d2704-167">Integrate with the Azure AD Reporting API</span></span>
<span data-ttu-id="d2704-168">請參閱 [開始使用報告 API](active-directory-reporting-api-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="d2704-168">See [Getting started with the Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

### <a name="engage-multi-factor-authentication-on-users"></a><span data-ttu-id="d2704-169">對使用者採取 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="d2704-169">Engage Multi-Factor Authentication on users</span></span>
<span data-ttu-id="d2704-170">在報告中選取使用者。</span><span class="sxs-lookup"><span data-stu-id="d2704-170">Select a user in a report.</span></span>

<span data-ttu-id="d2704-171">按一下畫面底部的 [啟用 MFA] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d2704-171">Click the "Enable MFA" button at the bottom of the screen.</span></span>

![畫面底部的 [Multi-Factor Authentication] 按鈕](./media/active-directory-reporting-getting-started/mfaButton.png)

> [!TIP]
> <span data-ttu-id="d2704-173">如需有關 Azure AD 報告的更多文件，請參閱 [檢視存取和使用情況報告](active-directory-view-access-usage-reports.md)。</span><span class="sxs-lookup"><span data-stu-id="d2704-173">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="learn-more"></a><span data-ttu-id="d2704-174">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="d2704-174">Learn more</span></span>
### <a name="audit-events"></a><span data-ttu-id="d2704-175">稽核事件</span><span class="sxs-lookup"><span data-stu-id="d2704-175">Audit events</span></span>
<span data-ttu-id="d2704-176">如需了解目錄中的哪些事件會進行稽核，請參閱 [Azure Active Directory 報告稽核事件](active-directory-reporting-audit-events.md)。</span><span class="sxs-lookup"><span data-stu-id="d2704-176">Learn about what events are audited in the directory in [Azure Active Directory Reporting Audit Events](active-directory-reporting-audit-events.md).</span></span>

### <a name="api-integration"></a><span data-ttu-id="d2704-177">API 整合</span><span class="sxs-lookup"><span data-stu-id="d2704-177">API Integration</span></span>
<span data-ttu-id="d2704-178">請參閱[開始使用報告 API](active-directory-reporting-api-getting-started.md) 和 [API 參考文件](https://msdn.microsoft.com/library/azure/mt126081.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d2704-178">See [Getting started with the Reporting API](active-directory-reporting-api-getting-started.md) and the [API reference documentation](https://msdn.microsoft.com/library/azure/mt126081.aspx).</span></span>

### <a name="get-in-touch"></a><span data-ttu-id="d2704-179">取得聯繫</span><span class="sxs-lookup"><span data-stu-id="d2704-179">Get in touch</span></span>
<span data-ttu-id="d2704-180">如有任何意見回饋、需要說明，或有任何問題，請寄送電子郵件到 [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com) 。</span><span class="sxs-lookup"><span data-stu-id="d2704-180">Email [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com) for feedback, help, or any questions you might have.</span></span>

> [!TIP]
> <span data-ttu-id="d2704-181">如需有關 Azure AD 報告的更多文件，請參閱 [檢視存取和使用情況報告](active-directory-view-access-usage-reports.md)。</span><span class="sxs-lookup"><span data-stu-id="d2704-181">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

