---
title: "Azure Active Directory 報告：開始使用 | Microsoft Docs"
description: "列出 hello 各種可用的報表，在 Azure Active Directory 報告"
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
ms.openlocfilehash: f47875708398391dd7f3efdc56a741fdba273b76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-reporting"></a><span data-ttu-id="f64ec-103">開始使用 Azure Active Directory 報告</span><span class="sxs-lookup"><span data-stu-id="f64ec-103">Getting started with Azure Active Directory Reporting</span></span>
## <a name="what-it-is"></a><span data-ttu-id="f64ec-104">內容</span><span class="sxs-lookup"><span data-stu-id="f64ec-104">What it is</span></span>
<span data-ttu-id="f64ec-105">Azure Active Directory (Azure AD) 包括您的目錄的安全性、活動和稽核報告。</span><span class="sxs-lookup"><span data-stu-id="f64ec-105">Azure Active Directory (Azure AD) includes security, activity, and audit reports for your directory.</span></span> <span data-ttu-id="f64ec-106">以下是一份包含 hello 報表：</span><span class="sxs-lookup"><span data-stu-id="f64ec-106">Here's a list of hello reports included:</span></span>

### <a name="security-reports"></a><span data-ttu-id="f64ec-107">安全性報告</span><span class="sxs-lookup"><span data-stu-id="f64ec-107">Security reports</span></span>
* <span data-ttu-id="f64ec-108">從不明來源登入</span><span class="sxs-lookup"><span data-stu-id="f64ec-108">Sign-ins from unknown sources</span></span>
* <span data-ttu-id="f64ec-109">在多次失敗後登入</span><span class="sxs-lookup"><span data-stu-id="f64ec-109">Sign-ins after multiple failures</span></span>
* <span data-ttu-id="f64ec-110">從多個地理區域登入</span><span class="sxs-lookup"><span data-stu-id="f64ec-110">Sign-ins from multiple geographies</span></span>
* <span data-ttu-id="f64ec-111">從具有可疑活動的 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="f64ec-111">Sign-ins from IP addresses with suspicious activity</span></span>
* <span data-ttu-id="f64ec-112">異常的登入活動</span><span class="sxs-lookup"><span data-stu-id="f64ec-112">Irregular sign-in activity</span></span>
* <span data-ttu-id="f64ec-113">從可能受感染的裝置登入</span><span class="sxs-lookup"><span data-stu-id="f64ec-113">Sign-ins from possibly infected devices</span></span>
* <span data-ttu-id="f64ec-114">具有異常登入活動的使用者</span><span class="sxs-lookup"><span data-stu-id="f64ec-114">Users with anomalous sign-in activity</span></span>

### <a name="activity-reports"></a><span data-ttu-id="f64ec-115">活動報告</span><span class="sxs-lookup"><span data-stu-id="f64ec-115">Activity reports</span></span>
* <span data-ttu-id="f64ec-116">應用程式使用情況：摘要</span><span class="sxs-lookup"><span data-stu-id="f64ec-116">Application usage: summary</span></span>
* <span data-ttu-id="f64ec-117">應用程式使用情況：詳細</span><span class="sxs-lookup"><span data-stu-id="f64ec-117">Application usage: detailed</span></span>
* <span data-ttu-id="f64ec-118">應用程式儀表板</span><span class="sxs-lookup"><span data-stu-id="f64ec-118">Application dashboard</span></span>
* <span data-ttu-id="f64ec-119">帳戶佈建錯誤</span><span class="sxs-lookup"><span data-stu-id="f64ec-119">Account provisioning errors</span></span>
* <span data-ttu-id="f64ec-120">個別使用者裝置</span><span class="sxs-lookup"><span data-stu-id="f64ec-120">Individual user devices</span></span>
* <span data-ttu-id="f64ec-121">個別使用者活動</span><span class="sxs-lookup"><span data-stu-id="f64ec-121">Individual user Activity</span></span>
* <span data-ttu-id="f64ec-122">群組活動報告</span><span class="sxs-lookup"><span data-stu-id="f64ec-122">Groups activity report</span></span>
* <span data-ttu-id="f64ec-123">密碼重設登錄活動報告</span><span class="sxs-lookup"><span data-stu-id="f64ec-123">Password Reset Registration Activity Report</span></span>
* <span data-ttu-id="f64ec-124">密碼重設活動</span><span class="sxs-lookup"><span data-stu-id="f64ec-124">Password reset activity</span></span>

### <a name="audit-reports"></a><span data-ttu-id="f64ec-125">稽核報告</span><span class="sxs-lookup"><span data-stu-id="f64ec-125">Audit reports</span></span>
* <span data-ttu-id="f64ec-126">目錄稽核報告</span><span class="sxs-lookup"><span data-stu-id="f64ec-126">Directory audit report</span></span>

> [!TIP]
> <span data-ttu-id="f64ec-127">如需有關 Azure AD 報告的更多文件，請參閱 [檢視存取和使用情況報告](active-directory-view-access-usage-reports.md)。</span><span class="sxs-lookup"><span data-stu-id="f64ec-127">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="how-it-works"></a><span data-ttu-id="f64ec-128">運作方式</span><span class="sxs-lookup"><span data-stu-id="f64ec-128">How it works</span></span>
### <a name="reporting-pipeline"></a><span data-ttu-id="f64ec-129">報告管線</span><span class="sxs-lookup"><span data-stu-id="f64ec-129">Reporting pipeline</span></span>
<span data-ttu-id="f64ec-130">hello 報告管線包含三個主要步驟。</span><span class="sxs-lookup"><span data-stu-id="f64ec-130">hello reporting pipeline consists of three main steps.</span></span> <span data-ttu-id="f64ec-131">每次使用者登入，或進行驗證，hello 會發生下列狀況：</span><span class="sxs-lookup"><span data-stu-id="f64ec-131">Every time a user signs in, or an authentication is made, hello following happens:</span></span>

* <span data-ttu-id="f64ec-132">首先，hello 使用者已驗證 （成功或失敗），並 hello 結果會儲存在 hello Azure Active Directory 服務資料庫。</span><span class="sxs-lookup"><span data-stu-id="f64ec-132">First, hello user is authenticated (successfully or unsuccessfully), and hello result is stored in hello Azure Active Directory service databases.</span></span>
* <span data-ttu-id="f64ec-133">每隔一段固定時間，就會處理所有最近的登入。</span><span class="sxs-lookup"><span data-stu-id="f64ec-133">At regular intervals, all recent sign ins are processed.</span></span> <span data-ttu-id="f64ec-134">此時，我們的安全性和異常活動演算法會搜尋所有最近的登入找出是否有可疑的活動。</span><span class="sxs-lookup"><span data-stu-id="f64ec-134">At this point, our security and anomalous activity algorithms are searching all recent sign ins for suspicious activity.</span></span>
* <span data-ttu-id="f64ec-135">經過處理後，hello 報表會寫入、 快取，而且在 hello Azure 傳統入口網站中提供。</span><span class="sxs-lookup"><span data-stu-id="f64ec-135">After processing, hello reports are written, cached, and served in hello Azure classic portal.</span></span>

### <a name="report-generation-times"></a><span data-ttu-id="f64ec-136">報告產生時間</span><span class="sxs-lookup"><span data-stu-id="f64ec-136">Report generation times</span></span>
<span data-ttu-id="f64ec-137">Toohello 大型磁碟區的驗證與登入處理 hello Azure AD 的平台，因為 hello 最近登入處理的平均，1 小時前。</span><span class="sxs-lookup"><span data-stu-id="f64ec-137">Due toohello large volume of authentications and sign ins processed by hello Azure AD platform, hello most recent sign-ins processed are, on average, one hour old.</span></span> <span data-ttu-id="f64ec-138">在罕見的情況下，它可能會佔用 too8 小時 tooprocess hello 最近登入。</span><span class="sxs-lookup"><span data-stu-id="f64ec-138">In rare cases, it may take up too8 hours tooprocess hello most recent sign-ins.</span></span>

<span data-ttu-id="f64ec-139">您可以藉由檢查 hello 說明文字，每個報表的 hello 頂端找到 hello 最近處理登入。</span><span class="sxs-lookup"><span data-stu-id="f64ec-139">You can find hello most recent processed sign-in by examining hello help text at hello top of each report.</span></span>

![在每個報表 hello 最上方的說明文字](./media/active-directory-reporting-getting-started/reportingWatermark.PNG)

> [!TIP]
> <span data-ttu-id="f64ec-141">如需有關 Azure AD 報告的更多文件，請參閱 [檢視存取和使用情況報告](active-directory-view-access-usage-reports.md)。</span><span class="sxs-lookup"><span data-stu-id="f64ec-141">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="getting-started"></a><span data-ttu-id="f64ec-142">開始使用</span><span class="sxs-lookup"><span data-stu-id="f64ec-142">Getting started</span></span>
### <a name="sign-into-hello-azure-classic-portal"></a><span data-ttu-id="f64ec-143">登入 hello Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="f64ec-143">Sign into hello Azure classic portal</span></span>
<span data-ttu-id="f64ec-144">首先，您將需要 toosign 到 hello [Azure 傳統入口網站](https://manage.windowsazure.com)身為全域或相容性的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="f64ec-144">First, you'll need toosign into hello [Azure classic portal](https://manage.windowsazure.com)  as a global or compliance administrator.</span></span> <span data-ttu-id="f64ec-145">您也必須有 Azure 訂用帳戶服務管理員或共同管理員，或使用 hello 」 存取 tooAzure AD"Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f64ec-145">You must also be an Azure subscription service administrator or co-administrator, or be using hello "Access tooAzure AD" Azure subscription.</span></span>

### <a name="navigate-tooreports"></a><span data-ttu-id="f64ec-146">瀏覽 tooReports</span><span class="sxs-lookup"><span data-stu-id="f64ec-146">Navigate tooReports</span></span>
<span data-ttu-id="f64ec-147">tooview 報表瀏覽 toohello 在 hello 頂端目錄的 [報告] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f64ec-147">tooview Reports, navigate toohello Reports tab at hello top of your directory.</span></span>

<span data-ttu-id="f64ec-148">如果這是您第一次檢視 hello 報表，您必須 tooagree tooa 對話方塊之前，您可以檢視 hello 報告。</span><span class="sxs-lookup"><span data-stu-id="f64ec-148">If this is your first time viewing hello reports, you'll need tooagree tooa dialog box before you can view hello reports.</span></span> <span data-ttu-id="f64ec-149">這是已接受您的組織 tooview 中的管理員 tooensure 這項資料可能會被視為一些國家/地區的私人資訊。</span><span class="sxs-lookup"><span data-stu-id="f64ec-149">This is tooensure that it's acceptable for admins in your organization tooview this data, which may be considered private information in some countries.</span></span>

![對話方塊](./media/active-directory-reporting-getting-started/dialogBox.png)

### <a name="explore-each-report"></a><span data-ttu-id="f64ec-151">瀏覽每個報告</span><span class="sxs-lookup"><span data-stu-id="f64ec-151">Explore each report</span></span>
<span data-ttu-id="f64ec-152">收集每個報表 toosee hello 資料瀏覽，再處理 hello 登入。</span><span class="sxs-lookup"><span data-stu-id="f64ec-152">Navigate into each report toosee hello data being collected and hello sign-ins processed.</span></span> <span data-ttu-id="f64ec-153">您可以找到[所有 hello 報告以下清單](active-directory-reporting-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="f64ec-153">You can find a [list of all hello reports here](active-directory-reporting-guide.md).</span></span>

![所有報告](./media/active-directory-reporting-getting-started/reportsMain.png)

### <a name="download-hello-reports-as-csv"></a><span data-ttu-id="f64ec-155">Hello 報表下載為 CSV</span><span class="sxs-lookup"><span data-stu-id="f64ec-155">Download hello reports as CSV</span></span>
<span data-ttu-id="f64ec-156">每個報告可以下載為 CSV (逗號分隔值) 檔案。</span><span class="sxs-lookup"><span data-stu-id="f64ec-156">Each report can be downloaded as a CSV (comma-separated value) file.</span></span> <span data-ttu-id="f64ec-157">您可以使用 Excel、 power Bi 或協力廠商架構分析程式 toofurther 分析資料中的這些檔案。</span><span class="sxs-lookup"><span data-stu-id="f64ec-157">You can use these files in Excel, PowerBI or third-party analysis programs toofurther analyze your data.</span></span>

<span data-ttu-id="f64ec-158">toodownload 任何報告以 csv 格式中，瀏覽 toohello 報表，然後按一下 [下載] 底部 hello。</span><span class="sxs-lookup"><span data-stu-id="f64ec-158">toodownload any report as a CSV, navigate toohello report and click "Download" at hello bottom.</span></span>

![[下載] 按鈕](./media/active-directory-reporting-getting-started/downloadButton.png)

> [!TIP]
> <span data-ttu-id="f64ec-160">如需有關 Azure AD 報告的更多文件，請參閱 [檢視存取和使用情況報告](active-directory-view-access-usage-reports.md)。</span><span class="sxs-lookup"><span data-stu-id="f64ec-160">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="f64ec-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f64ec-161">Next steps</span></span>
### <a name="customize-alerts-for-anomalous-sign-in-activity"></a><span data-ttu-id="f64ec-162">自訂異常登入活動的警示</span><span class="sxs-lookup"><span data-stu-id="f64ec-162">Customize alerts for anomalous sign in activity</span></span>
<span data-ttu-id="f64ec-163">瀏覽您的目錄 toohello 「 設定 」 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f64ec-163">Navigate toohello "Configure" tab of your directory.</span></span>

<span data-ttu-id="f64ec-164">捲動 toohello 「 通知 」 一節。</span><span class="sxs-lookup"><span data-stu-id="f64ec-164">Scroll toohello "Notifications" section.</span></span>

<span data-ttu-id="f64ec-165">啟用或停用 hello [異常的登入的電子郵件通知] 區段。</span><span class="sxs-lookup"><span data-stu-id="f64ec-165">Enable or disable hello "Email Notifications of Anomalous sign-ins" section.</span></span>

![hello 通知 區段](./media/active-directory-reporting-getting-started/notificationsSection.png)

### <a name="integrate-with-hello-azure-ad-reporting-api"></a><span data-ttu-id="f64ec-167">Hello 與整合 Azure AD 報告 API</span><span class="sxs-lookup"><span data-stu-id="f64ec-167">Integrate with hello Azure AD Reporting API</span></span>
<span data-ttu-id="f64ec-168">請參閱[入門 hello Reporting API](active-directory-reporting-api-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="f64ec-168">See [Getting started with hello Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

### <a name="engage-multi-factor-authentication-on-users"></a><span data-ttu-id="f64ec-169">對使用者採取 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="f64ec-169">Engage Multi-Factor Authentication on users</span></span>
<span data-ttu-id="f64ec-170">在報告中選取使用者。</span><span class="sxs-lookup"><span data-stu-id="f64ec-170">Select a user in a report.</span></span>

<span data-ttu-id="f64ec-171">按一下 在 hello 囉 」 畫面底部的 hello 」 啟用 MFA 」 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f64ec-171">Click hello "Enable MFA" button at hello bottom of hello screen.</span></span>

![在 hello 囉 」 畫面底部的 hello Multi-factor Authentication 按鈕](./media/active-directory-reporting-getting-started/mfaButton.png)

> [!TIP]
> <span data-ttu-id="f64ec-173">如需有關 Azure AD 報告的更多文件，請參閱 [檢視存取和使用情況報告](active-directory-view-access-usage-reports.md)。</span><span class="sxs-lookup"><span data-stu-id="f64ec-173">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="learn-more"></a><span data-ttu-id="f64ec-174">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="f64ec-174">Learn more</span></span>
### <a name="audit-events"></a><span data-ttu-id="f64ec-175">稽核事件</span><span class="sxs-lookup"><span data-stu-id="f64ec-175">Audit events</span></span>
<span data-ttu-id="f64ec-176">深入了解哪些事件稽核 hello 目錄中[Azure Active Directory 報告稽核事件](active-directory-reporting-audit-events.md)。</span><span class="sxs-lookup"><span data-stu-id="f64ec-176">Learn about what events are audited in hello directory in [Azure Active Directory Reporting Audit Events](active-directory-reporting-audit-events.md).</span></span>

### <a name="api-integration"></a><span data-ttu-id="f64ec-177">API 整合</span><span class="sxs-lookup"><span data-stu-id="f64ec-177">API Integration</span></span>
<span data-ttu-id="f64ec-178">請參閱[入門 hello Reporting API](active-directory-reporting-api-getting-started.md)和 hello [API 參考文件](https://msdn.microsoft.com/library/azure/mt126081.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f64ec-178">See [Getting started with hello Reporting API](active-directory-reporting-api-getting-started.md) and hello [API reference documentation](https://msdn.microsoft.com/library/azure/mt126081.aspx).</span></span>

### <a name="get-in-touch"></a><span data-ttu-id="f64ec-179">取得聯繫</span><span class="sxs-lookup"><span data-stu-id="f64ec-179">Get in touch</span></span>
<span data-ttu-id="f64ec-180">如有任何意見回饋、需要說明，或有任何問題，請寄送電子郵件到 [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com) 。</span><span class="sxs-lookup"><span data-stu-id="f64ec-180">Email [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com) for feedback, help, or any questions you might have.</span></span>

> [!TIP]
> <span data-ttu-id="f64ec-181">如需有關 Azure AD 報告的更多文件，請參閱 [檢視存取和使用情況報告](active-directory-view-access-usage-reports.md)。</span><span class="sxs-lookup"><span data-stu-id="f64ec-181">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

