---
title: "aaaDocument 保護個人資料與 Azure 報告工具 |Microsoft 文件"
description: "如何 toouse Azure 的 reporting services 與技術 toohelp 保護隱私權的個人資料。"
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.openlocfilehash: 3230d26ed308a8a0e72421c001793be06334a7c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="document-protection-of-personal-data-with-azure-reporting-tools"></a><span data-ttu-id="037dd-103">使用 Azure 報告工具記載個人資料的保護</span><span class="sxs-lookup"><span data-stu-id="037dd-103">Document protection of personal data with Azure reporting tools</span></span>

<span data-ttu-id="037dd-104">本文將討論如何 toouse Azure reporting services，技術 toohelp 保護隱私權的個人資料。</span><span class="sxs-lookup"><span data-stu-id="037dd-104">This article will discuss how toouse Azure reporting services and technologies toohelp protect privacy of personal data.</span></span>

## <a name="scenario"></a><span data-ttu-id="037dd-105">案例</span><span class="sxs-lookup"><span data-stu-id="037dd-105">Scenario</span></span>

<span data-ttu-id="037dd-106">大型出航公司搬遷後 hello 美國，展開在 hello 地中海、 Adriatic，與波羅的海文海，以及 hello 不列顛群島其作業 toooffer 行程。</span><span class="sxs-lookup"><span data-stu-id="037dd-106">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="037dd-107">toohelp 這些工作，它所取得數個較小的出航行位於義大利，德國、 丹麥和 hello 英國</span><span class="sxs-lookup"><span data-stu-id="037dd-107">toohelp these efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span>

<span data-ttu-id="037dd-108">hello 公司使用 Microsoft Azure 的處理和儲存的公司資料。</span><span class="sxs-lookup"><span data-stu-id="037dd-108">hello company uses Microsoft Azure for processing and storage of corporate data.</span></span> <span data-ttu-id="037dd-109">其中包含其全球客戶群的名稱、地址、電話號碼和信用卡資訊等個人識別資訊。</span><span class="sxs-lookup"><span data-stu-id="037dd-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="037dd-110">它也會包含在所有位置的傳統的人力資源資訊，例如地址、 電話號碼、 稅務識別碼和醫療公司員工的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="037dd-110">It also includes traditional Human Resources information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="037dd-111">hello 出航列也會維護報酬和忠誠度計劃成員大型資料庫，其中包含與目前和過去的客戶的個人資訊 tootrack 關聯性。</span><span class="sxs-lookup"><span data-stu-id="037dd-111">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

<span data-ttu-id="037dd-112">位於 hello 世界各地的公司員工存取 hello 網路從 hello 公司遠端辦公室和旅行代理程式已存取 toosome 公司資源。</span><span class="sxs-lookup"><span data-stu-id="037dd-112">Corporate employees access hello network from hello company’s remote offices and travel agents located around hello world have access toosome company resources.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="037dd-113">問題陳述</span><span class="sxs-lookup"><span data-stu-id="037dd-113">Problem statement</span></span>

<span data-ttu-id="037dd-114">hello 公司必須保護員工和客戶的個人資料的多層式的安全性策略，使用 Azure 管理和安全性功能 tooimpose 嚴格的控制存取 tooand 處理的個人資料，而必須透過 hello 的隱私權無法 toodemonstrate 其保護測量 toointernal 和外部的稽核員。</span><span class="sxs-lookup"><span data-stu-id="037dd-114">hello company must protect hello privacy of employees’ and customers’ personal data through a multi-layered security strategy that uses Azure management and security features tooimpose strict controls on access tooand processing of personal data, and must be able toodemonstrate its protective measures toointernal and external auditors.</span></span>

## <a name="company-goal"></a><span data-ttu-id="037dd-115">公司目標</span><span class="sxs-lookup"><span data-stu-id="037dd-115">Company goal</span></span>

<span data-ttu-id="037dd-116">其深度防禦的安全性策略的一部分，它是公司目標 tootrack 的個人資料，所有存取 tooand 處理，並確保的個人資料的適當的隱私權保護的文件中的位置以及如何使用。</span><span class="sxs-lookup"><span data-stu-id="037dd-116">As part of its defense-in-depth security strategy, it is a company goal tootrack all access tooand processing of personal data, and ensure that documentation of adequate privacy protections for personal data are in place and working.</span></span>

## <a name="solutions"></a><span data-ttu-id="037dd-117">解決方案</span><span class="sxs-lookup"><span data-stu-id="037dd-117">Solutions</span></span>

<span data-ttu-id="037dd-118">Microsoft Azure 提供完整的監視、 記錄和診斷工具 toohelp 追蹤和記錄活動以及存取和處理個人資料、 地理資料流程的資料，以及第三方存取 toopersonal 資料相關聯的事件。</span><span class="sxs-lookup"><span data-stu-id="037dd-118">Microsoft Azure provides comprehensive monitoring, logging, and diagnostics tools toohelp track and record activities and events associated with accessing and processing personal data, geographic flow of data, and third-party access toopersonal data.</span></span> <span data-ttu-id="037dd-119">由於 hello 雲端中的個人資料的安全性是共同的責任，Microsoft 也有提供客戶：</span><span class="sxs-lookup"><span data-stu-id="037dd-119">Because security of personal data in hello cloud is a shared responsibility, Microsoft also provides customers with:</span></span>

- <span data-ttu-id="037dd-120">其自己處理客戶資料的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="037dd-120">Detailed information about its own processing of customers’ data</span></span>

- <span data-ttu-id="037dd-121">由 Microsoft 管理的安全性措施</span><span class="sxs-lookup"><span data-stu-id="037dd-121">Security measures administered by Microsoft</span></span>

- <span data-ttu-id="037dd-122">其傳送客戶資料的位置和方式</span><span class="sxs-lookup"><span data-stu-id="037dd-122">Where and how it sends customers’ data</span></span>

- <span data-ttu-id="037dd-123">Microsoft 自有隱私權檢閱程序的詳細資料</span><span class="sxs-lookup"><span data-stu-id="037dd-123">Details of Microsoft’s own privacy reviews process</span></span>

### <a name="azure-active-directory"></a><span data-ttu-id="037dd-124">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="037dd-124">Azure Active Directory</span></span>

<span data-ttu-id="037dd-125">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) 是 Microsoft 的雲端式、多租用戶目錄和身分識別管理服務。</span><span class="sxs-lookup"><span data-stu-id="037dd-125">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) is Microsoft’s cloud-based, multi-tenant directory and identity management service.</span></span> <span data-ttu-id="037dd-126">服務的登入 hello 和稽核報告功能提供您詳細的登入和應用程式使用方式活動資訊 toohelp 監視，並確保適當的存取權 toocustomers 和員工的個人資料。</span><span class="sxs-lookup"><span data-stu-id="037dd-126">hello service’s sign-in and audit reporting capabilities provide you with detailed sign-in and application usage activity information toohelp you monitor and ensure proper access toocustomers’ and employees’ personal data.</span></span>

<span data-ttu-id="037dd-127">活動報告類型有兩種︰</span><span class="sxs-lookup"><span data-stu-id="037dd-127">There are two types of activity reports:</span></span>

- <span data-ttu-id="037dd-128">hello[稽核活動報告記錄檔](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs)提供系統活動/工作的詳細的記錄</span><span class="sxs-lookup"><span data-stu-id="037dd-128">hello [audit activity reports/logs](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) provide a detailed record of system activities/tasks</span></span>

- <span data-ttu-id="037dd-129">hello[登入活動報表/記錄檔](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins)顯示您已執行 hello 稽核報表中列出的每個活動的人員</span><span class="sxs-lookup"><span data-stu-id="037dd-129">hello [sign-ins activity report/log](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins) shows you who has performed each activity listed in hello audit report</span></span>

<span data-ttu-id="037dd-130">您可以同時使用兩個 hello，追蹤 hello 歷程記錄的每個已執行的工作，以及每個執行之人員。</span><span class="sxs-lookup"><span data-stu-id="037dd-130">Using hello two together, you can track hello history of every task performed and who performed each.</span></span> <span data-ttu-id="037dd-131">這兩種報告均可自訂和篩選。</span><span class="sxs-lookup"><span data-stu-id="037dd-131">Both types of reports are customizable and can be filtered.</span></span>

#### <a name="how-do-i-access-hello-audit-and-security-logs"></a><span data-ttu-id="037dd-132">如何存取 hello 稽核和安全性記錄檔？</span><span class="sxs-lookup"><span data-stu-id="037dd-132">How do I access hello audit and security logs?</span></span>

<span data-ttu-id="037dd-133">hello 稽核及安全性記錄檔可以存取從 hello Active Directory 入口網站以三個不同的方式： 透過 hello**活動**> 一節 (選取**稽核記錄檔**或**登入**)，或從**使用者和群組**或**企業應用程式**下**管理**Active Directory 中。</span><span class="sxs-lookup"><span data-stu-id="037dd-133">hello audit and security logs can be accessed from hello Active Directory portal in three different ways: through hello **Activity** section (select either **Audit logs** or **Sign-ins**), or from **Users and groups** or **Enterprise applications** under **Manage** in Active Directory.</span></span> <span data-ttu-id="037dd-134">報表也可以存取透過 hello Azure Active Directory 報告 API。</span><span class="sxs-lookup"><span data-stu-id="037dd-134">Reports can also be accessed through hello Azure Active Directory reporting API.</span></span> 

1. <span data-ttu-id="037dd-135">在 hello Azure 入口網站，選取  **Azure Active Directory。**</span><span class="sxs-lookup"><span data-stu-id="037dd-135">In hello Azure portal, select **Azure Active Directory.**</span></span>

2. <span data-ttu-id="037dd-136">在 hello**活動**區段中，選取**稽核記錄檔。**</span><span class="sxs-lookup"><span data-stu-id="037dd-136">In hello **Activity** section, select **Audit logs.**</span></span>

    ![](media/protection-personal-data-azure-reporting-tools/image001.png)

3. <span data-ttu-id="037dd-137">藉由按一下自訂 hello 清單檢視**資料行**hello 工具列中。</span><span class="sxs-lookup"><span data-stu-id="037dd-137">Customize hello list view by clicking **Columns** in hello toolbar.</span></span>

4.  <span data-ttu-id="037dd-138">選取的項目 hello 清單檢視 toosee 中所有可用的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="037dd-138">Select an item in hello list view toosee all available details about it.</span></span>

    ![](media/protection-personal-data-azure-reporting-tools/image003.png)

<span data-ttu-id="037dd-139">Azure Active Directory 報告還包含兩種類型的安全性報告：[標幟為有風險的使用者]和 [有風險的登入]，這可協助您監視 Azure 環境中的潛在風險。</span><span class="sxs-lookup"><span data-stu-id="037dd-139">Azure Active Directory reporting also includes two types of security reports, **users flagged for risk** and **risky sign-ins**, which can help you monitor potential risks in your Azure environment.</span></span>

<span data-ttu-id="037dd-140">如需 hello 報告服務的詳細資訊，請參閱[Azure Active Directory 報告](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal)</span><span class="sxs-lookup"><span data-stu-id="037dd-140">For more information about hello reporting service, see [Azure Active Directory reporting](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal)</span></span>

<span data-ttu-id="037dd-141">請瀏覽[Azure Active Directory 活動報告](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal#activity-reports)針對更多有關使用 Azure Active Directory 中的 hello 報表的特性。</span><span class="sxs-lookup"><span data-stu-id="037dd-141">Visit [Azure Active Directory activity reports](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal#activity-reports) for more specifics about hello reports available in Azure Active Directory.</span></span> <span data-ttu-id="037dd-142">這個網站包含更多詳細瞭解 tooaccess 並用[稽核記錄活動報告](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs)和[登入活動報表](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins)hello 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="037dd-142">This site includes more details about how tooaccess and use [audit logs activity reports](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) and [sign-in activity reports](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins) in hello portal.</span></span> <span data-ttu-id="037dd-143">它也包含[標幟為有風險的使用者](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-user-at-risk)和[有風險的登入](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-risky-sign-ins)安全性報告的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="037dd-143">It also includes information about [users flagged for risk](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-user-at-risk) and [risky sign-in](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-risky-sign-ins) security reports.</span></span>

<span data-ttu-id="037dd-144">請瀏覽 hello [Azure Active Directory 稽核應用程式開發介面參考](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-audit-reference)站台，如需有關如何 tooconnect tooAzure 目錄以程式設計方式報告。</span><span class="sxs-lookup"><span data-stu-id="037dd-144">Visit hello [Azure Active Directory audit API reference](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-audit-reference) site for more information on how tooconnect tooAzure Directory reporting programmatically.</span></span>

### <a name="log-analytics"></a><span data-ttu-id="037dd-145">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="037dd-145">Log Analytics</span></span>

<span data-ttu-id="037dd-146">[記錄分析](https://azure.microsoft.com/services/log-analytics/)可以[收集資料，從 Azure 監視器](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-storage)toocorrelate 它與其他資料，並提供其他的分析。</span><span class="sxs-lookup"><span data-stu-id="037dd-146">[Log Analytics](https://azure.microsoft.com/services/log-analytics/) can [collect data from Azure Monitor](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-storage) toocorrelate it with other data and provide additional analysis.</span></span> <span data-ttu-id="037dd-147">Azure 監視器可收集和分析 Azure 環境的監視資料。</span><span class="sxs-lookup"><span data-stu-id="037dd-147">Azure Monitor collects and analyzes monitoring data for your Azure environment.</span></span> 

<span data-ttu-id="037dd-148">Log Analytics 中的分析工具 (例如記錄搜尋、檢視和解決方案) 可處理所有收集的資料，進而為您提供整個環境的集中式分析。</span><span class="sxs-lookup"><span data-stu-id="037dd-148">Analysis tools in Log Analytics such as log searches, views, and solutions work against all collected data, providing you with centralized analysis of your entire environment.</span></span> <span data-ttu-id="037dd-149">記錄分析可彙總並分析 Windows 事件記錄檔、 IIS 記錄檔，以及可協助偵測潛在可能會公開的個人資料 toounauthorized 使用者的個人資料缺口的 Syslog。</span><span class="sxs-lookup"><span data-stu-id="037dd-149">Log Analytics can aggregate and analyze Windows Event logs, IIS logs, and Syslogs, which can help detect potential personal data breaches that could expose personal data toounauthorized users.</span></span>

#### <a name="how-do-i-use-log-analytics"></a><span data-ttu-id="037dd-150">如何使用 Log Analytics？</span><span class="sxs-lookup"><span data-stu-id="037dd-150">How do I use Log Analytics?</span></span>

<span data-ttu-id="037dd-151">您可以透過 hello OMS 入口網站或 hello Azure 入口網站，從任何網頁瀏覽器存取記錄分析。</span><span class="sxs-lookup"><span data-stu-id="037dd-151">You can access Log Analytics through hello OMS portal or hello Azure portal, from any web browser.</span></span> <span data-ttu-id="037dd-152">記錄分析包含查詢語言 tooquickly 擷取和彙總 hello 儲存機制中的資料。</span><span class="sxs-lookup"><span data-stu-id="037dd-152">Log Analytics includes a query language tooquickly retrieve and consolidate data in hello repository.</span></span> <span data-ttu-id="037dd-153">您可以建立及儲存的記錄搜尋 toodirectly 分析 hello 入口網站中的資料。</span><span class="sxs-lookup"><span data-stu-id="037dd-153">You can create and save Log Searches toodirectly analyze data in hello portal.</span></span>

<span data-ttu-id="037dd-154">toocreate hello Azure 入口網站中的記錄分析工作區 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="037dd-154">toocreate a Log Analytics workspace in hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="037dd-155">選取**記錄分析**hello 清單中的 hello Marketplace 中的服務。</span><span class="sxs-lookup"><span data-stu-id="037dd-155">Select **Log Analytics** from hello list of services in hello Marketplace.</span></span>

2. <span data-ttu-id="037dd-156">選取**建立、**指定 hello 的 OMS 工作區的名稱、 您的訂用帳戶、 資源群組、 位置，然後在定價層。</span><span class="sxs-lookup"><span data-stu-id="037dd-156">Select **Create,** then specify hello name of your OMS workspace, select your subscription, resource group, location, and pricing tier.</span></span>

3. <span data-ttu-id="037dd-157">按一下**確定**toodisplay 的工作區清單。</span><span class="sxs-lookup"><span data-stu-id="037dd-157">Click **OK** toodisplay a list of your workspaces.</span></span>

4. <span data-ttu-id="037dd-158">選取工作區 toosee 其詳細資料。</span><span class="sxs-lookup"><span data-stu-id="037dd-158">Select a workspace toosee its details.</span></span>

    ![](media/protection-personal-data-azure-reporting-tools/image004.png)

<span data-ttu-id="037dd-159">請瀏覽 hello[記錄分析文件](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)toolearn 更多關於 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="037dd-159">Visit hello [Log Analytics documentation](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) toolearn more about hello service.</span></span>

<span data-ttu-id="037dd-160">瀏覽 hello[開始記錄分析工作區使用](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)教學課程 toocreate 評估工作區，並了解如何 toouse hello 服務 hello 基本概念。</span><span class="sxs-lookup"><span data-stu-id="037dd-160">Visit hello [Get started with a Log Analytics workspace](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started) tutorial toocreate an evaluation workspace and learn hello basics of how toouse hello service.</span></span>

<span data-ttu-id="037dd-161">請瀏覽下列如需特定資訊的網頁上以 hello tooconnect toouse 記錄分析的記錄檔的 hello 上面所述：</span><span class="sxs-lookup"><span data-stu-id="037dd-161">Visit hello following web pages for more specific information on how tooconnect toouse Log Analytics with hello logs described above:</span></span>

[<span data-ttu-id="037dd-162">Log Analytics 中的 Windows 事件記錄資料來源</span><span class="sxs-lookup"><span data-stu-id="037dd-162">Windows event logs data sources in Log Analytics</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events)

[<span data-ttu-id="037dd-163">Log Analytics 中的 IIS 記錄</span><span class="sxs-lookup"><span data-stu-id="037dd-163">IIS logs in Log Analytics</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-iis-logs)

[<span data-ttu-id="037dd-164">Log Analytics 中的 Syslog 資料來源</span><span class="sxs-lookup"><span data-stu-id="037dd-164">Syslog data sources in Log Analytics</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-syslog)

### <a name="azure-monitorazure-activity-log"></a><span data-ttu-id="037dd-165">Azure 監視器/Azure 活動記錄</span><span class="sxs-lookup"><span data-stu-id="037dd-165">Azure Monitor/Azure Activity Log</span></span> 

<span data-ttu-id="037dd-166">[Azure 監視器](https://azure.microsoft.com/services/monitor/)可針對 Microsoft Azure 中的大多數服務提供基本等級的基礎結構計量與記錄。</span><span class="sxs-lookup"><span data-stu-id="037dd-166">[Azure Monitor](https://azure.microsoft.com/services/monitor/) provides base level infrastructure metrics and logs for most services in Microsoft Azure.</span></span>
<span data-ttu-id="037dd-167">監視可協助您 toogain 深入了解有關 Azure 應用程式。</span><span class="sxs-lookup"><span data-stu-id="037dd-167">Monitoring can help you toogain deep insights about your Azure applications.</span></span> <span data-ttu-id="037dd-168">Azure 監視依賴 hello Azure 診斷延伸模組 （Windows 或 Linux） 來收集大部分的應用程式層級度量和記錄檔。</span><span class="sxs-lookup"><span data-stu-id="037dd-168">Azure Monitor relies on hello Azure diagnostics extension (Windows or Linux) to collect most application level metrics and logs.</span></span> <span data-ttu-id="037dd-169">[hello Azure 活動記錄檔](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)是 hello 資源，您可以檢視的 Azure 監視的其中一個。</span><span class="sxs-lookup"><span data-stu-id="037dd-169">[hello Azure Activity Log](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) is one of hello resources you can view with Azure Monitor.</span></span> <span data-ttu-id="037dd-170">它會追蹤每個 API 呼叫，並提供有關在 [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) 中發生之活動的豐富資訊。</span><span class="sxs-lookup"><span data-stu-id="037dd-170">It tracks every API call, and provides a wealth of information about activities that occur in [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span></span>
<span data-ttu-id="037dd-171">您可以在 hello Azure 基礎結構所偵測到您資源的相關資訊的搜尋 hello （先前稱為操作或稽核記錄檔） 的活動記錄檔。</span><span class="sxs-lookup"><span data-stu-id="037dd-171">You can search hello Activity Log (previously called Operational or Audit Logs) for information about your resource as seen by hello Azure infrastructure.</span></span> 

<span data-ttu-id="037dd-172">雖然許多 hello 資訊記錄在 hello 活動記錄檔與 tooperformance 和服務的健全狀況，也沒有為資料的相關的 tooprotection 的資訊。</span><span class="sxs-lookup"><span data-stu-id="037dd-172">Although much of hello information recorded in hello Activity log pertains tooperformance and service health, there is also information that is related tooprotection of data.</span></span> <span data-ttu-id="037dd-173">使用 hello 活動記錄檔，您可以決定 hello 」 功能，對象、 及何時"的任何寫入作業 (PUT、 POST、 DELETE) 在您的 Azure 訂用帳戶中的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="037dd-173">Using hello Activity Log, you can determine hello “what, who, and when” for any write operations (PUT, POST, DELETE) taken on hello resources in your Azure subscription.</span></span>

<span data-ttu-id="037dd-174">例如，它提供的記錄，當系統管理員刪除網路安全性群組，因而可能影響到 hello 保護個人資料。</span><span class="sxs-lookup"><span data-stu-id="037dd-174">For example, it provides a record when an administrator deletes a network security group, which could impact hello protection of personal data.</span></span> <span data-ttu-id="037dd-175">活動記錄項目會儲存在 Azure 監視器中長達 90 天。</span><span class="sxs-lookup"><span data-stu-id="037dd-175">Activity log entries are stored in Azure Monitor for 90 days.</span></span>

#### <a name="how-do-i-use-hello-data-collected-by-azure-monitor"></a><span data-ttu-id="037dd-176">如何使用 Azure 監視器所收集的 hello 資料？</span><span class="sxs-lookup"><span data-stu-id="037dd-176">How do I use hello data collected by Azure Monitor?</span></span>

<span data-ttu-id="037dd-177">有的方式 toouse hello 資料 hello 活動記錄檔中的數字和其他監視 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="037dd-177">There are a number of ways toouse hello data in hello Activity log and other Azure Monitor resources.</span></span>

- <span data-ttu-id="037dd-178">您可以串流處理實際的行中的 hello 資料 tooother 位置。</span><span class="sxs-lookup"><span data-stu-id="037dd-178">You can stream hello data tooother locations in real line.</span></span>

- <span data-ttu-id="037dd-179">您可以儲存 hello 資料較長的時間週期，比 hello 預設值，使用[Azure 儲存體帳戶](https://docs.microsoft.com/azure/storage/common/storage-introduction)和設定保留原則。</span><span class="sxs-lookup"><span data-stu-id="037dd-179">You can store hello data for longer time periods than hello defaults, using an [Azure storage account](https://docs.microsoft.com/azure/storage/common/storage-introduction) and setting a retention policy.</span></span>

- <span data-ttu-id="037dd-180">您可以視覺化 hello 圖形和圖表中的資料，使用 hello [Azure 入口網站](https://azure.microsoft.com/features/azure-portal/)， [Azure Application Insights](https://azure.microsoft.com/services/application-insights/)， [Microsoft PowerBI](https://powerbi.microsoft.com/)，或協力廠商視覺效果工具。</span><span class="sxs-lookup"><span data-stu-id="037dd-180">You can visual hello data in graphics and charts, using hello [Azure portal](https://azure.microsoft.com/features/azure-portal/), [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), [Microsoft PowerBI](https://powerbi.microsoft.com/), or third-party visualization tools.</span></span>

- <span data-ttu-id="037dd-181">您可以查詢使用 hello Azure 監視 REST API，CLI 命令的 hello 資料[PowerShell](https://docs.microsoft.com/powershell/) cmdlet，或 hello.NET SDK。</span><span class="sxs-lookup"><span data-stu-id="037dd-181">You can query hello data using hello Azure Monitor REST API, CLI commands, [PowerShell](https://docs.microsoft.com/powershell/) cmdlets, or hello .NET SDK.</span></span>

<span data-ttu-id="037dd-182">開始使用 Azure 監視器 tooget 選取**更服務**hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="037dd-182">tooget started with Azure Monitor, select **More Services** in hello Azure portal.</span></span>

1. <span data-ttu-id="037dd-183">向下捲動太**監視器**在 hello**監視及管理**> 一節。</span><span class="sxs-lookup"><span data-stu-id="037dd-183">Scroll down too**Monitor** in hello **Monitoring and Managing** section.</span></span>

    ![](media/protection-personal-data-azure-reporting-tools/image005.png)

2.  <span data-ttu-id="037dd-184">監視器開啟 hello**活動記錄檔**檢視。</span><span class="sxs-lookup"><span data-stu-id="037dd-184">Monitor opens in hello **Activity Log** view.</span></span>

    ![](media/protection-personal-data-azure-reporting-tools/image007.png)

<span data-ttu-id="037dd-185">您可以建立及儲存查詢的一般篩選器，然後 pin hello 最重要查詢 tooa 入口網站儀表板，就一定會知道是否發生符合您準則的事件。</span><span class="sxs-lookup"><span data-stu-id="037dd-185">You can create and save queries for common filters, then pin hello most important queries tooa portal dashboard so you'll always know if events that meet your criteria have occurred.</span></span>

1. <span data-ttu-id="037dd-186">您可以篩選 hello 檢視資源群組、 timespan 和事件類別目錄。</span><span class="sxs-lookup"><span data-stu-id="037dd-186">You can filter hello view by resource group, timespan, and event category.</span></span>

    ![](media/protection-personal-data-azure-reporting-tools/image008.png)

2. <span data-ttu-id="037dd-187">然後將依序按一下 hello 查詢 tooa 入口網站儀表板釘選**Pin**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="037dd-187">You can then pin queries tooa portal dashboard by clicking hello **Pin** button.</span></span> <span data-ttu-id="037dd-188">這可協助您在服務上建立作業資料的單一資訊來源。</span><span class="sxs-lookup"><span data-stu-id="037dd-188">This helps you create a single source of information for operational  data on your services.</span></span> <span data-ttu-id="037dd-189">hello 查詢的結果數目將會顯示名稱和 hello 儀表板上。</span><span class="sxs-lookup"><span data-stu-id="037dd-189">hello query name and number of results will be displayed on hello dashboard.</span></span>

<span data-ttu-id="037dd-190">您可以也使用 hello 監視器 tooview 標準所有 Azure 資源、 設定診斷設定和警示，並搜尋 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="037dd-190">You can also use hello Monitor tooview metrics for all Azure resources, configure diagnostics settings and alerts, and search hello log.</span></span> <span data-ttu-id="037dd-191">如需有關如何 toouse hello Azure 監視器和活動記錄檔，請參閱[開始使用 Azure 監視器](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-get-started)。</span><span class="sxs-lookup"><span data-stu-id="037dd-191">For more information on how toouse hello Azure Monitor and Activity Log, see [Get Started with Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-get-started).</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="037dd-192">Azure 診斷</span><span class="sxs-lookup"><span data-stu-id="037dd-192">Azure Diagnostics</span></span> 

<span data-ttu-id="037dd-193">在 Azure 中的 hello 診斷功能可讓來自多個來源的資料集合。</span><span class="sxs-lookup"><span data-stu-id="037dd-193">hello diagnostics capability in Azure enables collection of data from several sources.</span></span> <span data-ttu-id="037dd-194">hello Windows 事件記錄檔，其中包括 hello 安全性記錄檔，可以追蹤和記錄的個人資料的保護特別有用。</span><span class="sxs-lookup"><span data-stu-id="037dd-194">hello Windows Event logs, which include hello Security log, can be especially useful in tracking and documenting protection of personal data.</span></span> <span data-ttu-id="037dd-195">hello 安全性記錄檔會在登入成功和失敗事件，以及權限的變更、 偵測模式表示特定類型的攻擊、 安全性相關原則變更、 安全性群組成員資格變更，以及執行更多的追蹤。</span><span class="sxs-lookup"><span data-stu-id="037dd-195">hello security log tracks logon success and failure events, as well as permissions changes, detection of patterns indicating certain types of attacks, changes to security-related policies, security group membership changes, and much more.</span></span>

<span data-ttu-id="037dd-196">例如，事件識別碼 4695 提醒您嘗試 toohello unprotection 可稽核的受保護資料。</span><span class="sxs-lookup"><span data-stu-id="037dd-196">For example, Event ID 4695 alerts you toohello attempted unprotection of auditable protected data.</span></span> <span data-ttu-id="037dd-197">這與 toohello 資料保護 API (DPAPI)，它可以幫助 tooprotect 資料，例如私用的索引鍵、 預存的認證和其他機密資訊。</span><span class="sxs-lookup"><span data-stu-id="037dd-197">This pertains toohello Data Protection API (DPAPI), which helps tooprotect data such as private keys, stored credentials, and other confidential information.</span></span>

#### <a name="how-do-i-enable-hello-diagnostics-extension-for-windows-vms"></a><span data-ttu-id="037dd-198">如何啟用適用於 Windows Vm 的 hello 診斷延伸模組？</span><span class="sxs-lookup"><span data-stu-id="037dd-198">How do I enable hello diagnostics extension for Windows VMs?</span></span>

<span data-ttu-id="037dd-199">您可以針對 Windows VM，所以當 toocollect 記錄資料使用 PowerShell tooenable hello 診斷延伸模組。</span><span class="sxs-lookup"><span data-stu-id="037dd-199">You can use PowerShell tooenable hello diagnostics extension for a Windows VM, so as toocollect log data.</span></span> <span data-ttu-id="037dd-200">這麼做的 hello 步驟取決於您的部署模型上使用 （「 資源管理員 」 或 「 傳統 」）。</span><span class="sxs-lookup"><span data-stu-id="037dd-200">hello steps for doing so depend on which deployment model you use (Resource Manager or Classic).</span></span> <span data-ttu-id="037dd-201">tooenable hello 的診斷延伸模組透過 hello Resource Manager 部署模型所建立的現有 VM，您可以使用 hello[組 AzureRMVMDiagnosticsExtension PowerShell cmdlet](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension?view=azurermps-4.3.1)。</span><span class="sxs-lookup"><span data-stu-id="037dd-201">tooenable hello diagnostics extension on an existing VM that was created through hello Resource Manager deployment model, you can use hello [Set-AzureRMVMDiagnosticsExtension PowerShell cmdlet](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension?view=azurermps-4.3.1).</span></span>

   ![](media/protection-personal-data-azure-reporting-tools/image009.png)

<span data-ttu-id="037dd-202">*\$diagnosticsconfig_path* hello 路徑 toohello 檔案包含在 XML 中的 hello 診斷組態。</span><span class="sxs-lookup"><span data-stu-id="037dd-202">*\$diagnosticsconfig_path* is hello path toohello file that contains hello diagnostics configuration in XML.</span></span> <span data-ttu-id="037dd-203">如需詳細啟用 Azure 診斷 VM 上的指示，請參閱[執行 Windows 的虛擬機器中使用 PowerShell tooenable Azure 診斷。](https://docs.microsoft.com/azure/virtual-machines/windows/ps-extensions-diagnostics)</span><span class="sxs-lookup"><span data-stu-id="037dd-203">For more detailed instructions on enabling Azure Diagnostics on a VM, see [Use PowerShell tooenable Azure Diagnostics in a virtual machine running Windows.](https://docs.microsoft.com/azure/virtual-machines/windows/ps-extensions-diagnostics)</span></span>

<span data-ttu-id="037dd-204">hello Azure 診斷擴充功能可以傳送嗨收集資料 tooan Azure 儲存體帳戶，或傳送 tooservices 例如 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="037dd-204">hello Azure diagnostics extension can transfer hello collected data tooan Azure storage account or send it tooservices such as Application Insights.</span></span> <span data-ttu-id="037dd-205">然後您可以使用 hello 資料稽核。</span><span class="sxs-lookup"><span data-stu-id="037dd-205">You can then use hello data for auditing.</span></span>

#### <a name="how-do-i-store-and-view-diagnostic-data"></a><span data-ttu-id="037dd-206">如何儲存和檢視診斷資料？</span><span class="sxs-lookup"><span data-stu-id="037dd-206">How do I store and view diagnostic data?</span></span>

<span data-ttu-id="037dd-207">它是重要的 tooremember 的診斷資料不會永久儲存除非 toohello Microsoft Azure 儲存體模擬器] 或 [tooAzure 儲存體傳輸。</span><span class="sxs-lookup"><span data-stu-id="037dd-207">It’s important tooremember that diagnostic data is not permanently stored unless you transfer it toohello Microsoft Azure storage emulator or tooAzure storage.</span></span> <span data-ttu-id="037dd-208">toostore 和檢視診斷資料，在 Azure 儲存體，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="037dd-208">toostore and view diagnostic data in Azure Storage, follow these steps:</span></span>

1. <span data-ttu-id="037dd-209">Hello ServiceConfiguration.cscfg 檔案中指定的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="037dd-209">Specify a storage account in hello ServiceConfiguration.cscfg file.</span></span> <span data-ttu-id="037dd-210">Hello Blob 服務或 hello 表格服務，根據 hello 資料類型而定，可以使用 azure 診斷。</span><span class="sxs-lookup"><span data-stu-id="037dd-210">Azure Diagnostics can use either hello Blob service or hello Table service, depending on hello type of data.</span></span> <span data-ttu-id="037dd-211">Windows 事件記錄會以資料表格式儲存。</span><span class="sxs-lookup"><span data-stu-id="037dd-211">Windows Event logs are stored in Table format.</span></span>

2. <span data-ttu-id="037dd-212">傳送嗨資料。</span><span class="sxs-lookup"><span data-stu-id="037dd-212">Transfer hello data.</span></span> <span data-ttu-id="037dd-213">您可以透過 hello 設定檔要求 tootransfer hello 診斷資料。</span><span class="sxs-lookup"><span data-stu-id="037dd-213">You can request tootransfer hello diagnostic data through hello configuration file.</span></span> <span data-ttu-id="037dd-214">SDK 2.4 及之前，您也可以進行 hello 要求以程式設計的方式。</span><span class="sxs-lookup"><span data-stu-id="037dd-214">For SDK 2.4 and previous, you can also make hello request programmatically.</span></span>

3. <span data-ttu-id="037dd-215">檢視使用的 hello 資料[Azure 儲存體總管](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer)，[伺服器總管](https://docs.microsoft.com/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage)在 Visual Studio 中，或[Azure 診斷管理員](https://www.cerebrata.com/products/azure-diagnostics-manager)Azure Management Studio 中。</span><span class="sxs-lookup"><span data-stu-id="037dd-215">View hello data, using [Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer),  [Server Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage) in Visual Studio, or [Azure Diagnostics Manager](https://www.cerebrata.com/products/azure-diagnostics-manager) in Azure Management Studio.</span></span>

<span data-ttu-id="037dd-216">如需有關如何 tooperform 每個步驟執行，請參閱[Azure 儲存體中的儲存和檢視診斷資料。](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics-storage)</span><span class="sxs-lookup"><span data-stu-id="037dd-216">For more information on how tooperform each of these steps, see [Store and view diagnostic data in Azure Storage.](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics-storage)</span></span>

### <a name="azure-storage-analytics"></a><span data-ttu-id="037dd-217">Azure 儲存體分析</span><span class="sxs-lookup"><span data-stu-id="037dd-217">Azure Storage Analytics</span></span> 

<span data-ttu-id="037dd-218">儲存體分析記錄成功和失敗的要求 tooa 儲存體服務的詳細的資訊。</span><span class="sxs-lookup"><span data-stu-id="037dd-218">Storage Analytics logs detailed information about successful and failed requests tooa storage service.</span></span> <span data-ttu-id="037dd-219">這項資訊可以使用的 toomonitor 個別要求，可協助您撰寫存取 toopersonal 資料儲存在 hello 服務中。</span><span class="sxs-lookup"><span data-stu-id="037dd-219">This information can be used toomonitor individual requests, which can help in documenting access toopersonal data stored in hello service.</span></span> <span data-ttu-id="037dd-220">不過，根據預設，儲存體帳戶不會啟用儲存體分析記錄功能。</span><span class="sxs-lookup"><span data-stu-id="037dd-220">However, Storage Analytics logging is not enabled by default for your storage account.</span></span> <span data-ttu-id="037dd-221">您可以在 hello Azure 入口網站中加以啟用。</span><span class="sxs-lookup"><span data-stu-id="037dd-221">You can enable it in hello Azure portal.</span></span>

#### <a name="how-do-i-configure-monitoring-for-a-storage-account"></a><span data-ttu-id="037dd-222">如何設定儲存體帳戶的監視？</span><span class="sxs-lookup"><span data-stu-id="037dd-222">How do I configure monitoring for a storage account?</span></span>

<span data-ttu-id="037dd-223">tooconfigure 監視儲存體帳戶，下列 hello:</span><span class="sxs-lookup"><span data-stu-id="037dd-223">tooconfigure monitoring for a storage account, do hello following:</span></span>

1. <span data-ttu-id="037dd-224">選取**儲存體帳戶**hello Azure 入口網站，然後選取您想要 toomonitor hello 帳戶 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="037dd-224">Select **Storage accounts** in hello Azure portal, then select hello name of hello account you want toomonitor.</span></span>

    ![](media/protection-personal-data-azure-reporting-tools/image011.png)

2. <span data-ttu-id="037dd-225">在 hello**監視**區段中，選取**診斷。**</span><span class="sxs-lookup"><span data-stu-id="037dd-225">In hello **Monitoring** section, select **Diagnostics.**</span></span>

3.  <span data-ttu-id="037dd-226">選取 hello**類型**的度量資料想 toomonitor 為每個服務 （Blob、 資料表檔案）。</span><span class="sxs-lookup"><span data-stu-id="037dd-226">Select hello **type** of metrics data you want toomonitor for each service (Blob, Table, File).</span></span> <span data-ttu-id="037dd-227">tooinstruct Azure 儲存體 toosave 診斷記錄檔的讀取、 寫入和刪除要求 hello blob、 資料表和佇列服務，請選取**Blob 記錄檔時，資料表記錄**和**佇列記錄檔。**</span><span class="sxs-lookup"><span data-stu-id="037dd-227">tooinstruct Azure Storage toosave diagnostics logs for read, write, and delete requests for hello blob, table, and queue services, select **Blob logs, Table logs** and **Queue logs.**</span></span>

    ![](media/protection-personal-data-azure-reporting-tools/image013.png)

4. <span data-ttu-id="037dd-228">使用 hello 滑桿在 hello 下方，設定 hello**保留**原則天數 （1 – 365 值）。</span><span class="sxs-lookup"><span data-stu-id="037dd-228">Using hello slider at hello bottom, set hello **retention** policy in days (value of 1 – 365).</span></span> <span data-ttu-id="037dd-229">Hello 預設值是七天。</span><span class="sxs-lookup"><span data-stu-id="037dd-229">Seven days is hello default.</span></span>

5. <span data-ttu-id="037dd-230">選取**儲存**tooapply hello 組態設定。</span><span class="sxs-lookup"><span data-stu-id="037dd-230">Select **Save** tooapply hello configuration settings.</span></span>

<span data-ttu-id="037dd-231">儲存體記錄的記錄項目包含下列個別要求的相關資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="037dd-231">Storage Logging log entries contain hello following information about individual requests:</span></span>

- <span data-ttu-id="037dd-232">時間資訊，例如開始時間、端對端延遲和伺服器延遲。</span><span class="sxs-lookup"><span data-stu-id="037dd-232">Timing information such as start time, end-to-end latency, and server latency.</span></span>

- <span data-ttu-id="037dd-233">Hello 例如 hello 作業類型的儲存體作業的詳細資訊，儲存體物件 hello 用戶端 hello hello 索引鍵是存取、 成功或失敗，以及傳回 toohello 用戶端 hello HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="037dd-233">Details of hello storage operation such as hello operation type, hello key of hello storage object hello client is accessing, success or failure, and hello HTTP   status code returned toohello client.</span></span>

- <span data-ttu-id="037dd-234">例如 hello 類型驗證 hello 用戶端使用的驗證詳細資料。</span><span class="sxs-lookup"><span data-stu-id="037dd-234">Authentication details such as hello type of authentication hello client used.</span></span>

- <span data-ttu-id="037dd-235">並行存取資訊，例如 hello ETag 值和上次修改時間戳記。</span><span class="sxs-lookup"><span data-stu-id="037dd-235">Concurrency information such as hello ETag value and last modified timestamp.</span></span>

- <span data-ttu-id="037dd-236">hello 的 hello 要求和回應訊息的大小。</span><span class="sxs-lookup"><span data-stu-id="037dd-236">hello sizes of hello request and response messages.</span></span>

<span data-ttu-id="037dd-237">如需詳細指示 tooenable 儲存體分析記錄，請參閱[監視 hello Azure 入口網站的儲存體帳戶。](https://docs.microsoft.com/azure/storage/common/storage-monitor-storage-account)</span><span class="sxs-lookup"><span data-stu-id="037dd-237">For more detailed instructions on how tooenable Storage Analytics logging, see [Monitor a storage account in hello Azure portal.](https://docs.microsoft.com/azure/storage/common/storage-monitor-storage-account)</span></span>

### <a name="azure-security-center"></a><span data-ttu-id="037dd-238">Azure 資訊安全中心</span><span class="sxs-lookup"><span data-stu-id="037dd-238">Azure Security Center</span></span> 

<span data-ttu-id="037dd-239">[Azure 資訊安全中心](https://azure.microsoft.com/services/security-center/)監視器 hello 順序 tooprevent 在您的 Azure 資源的安全性狀態和偵測到威脅，並提供回應的建議。</span><span class="sxs-lookup"><span data-stu-id="037dd-239">[Azure Security Center](https://azure.microsoft.com/services/security-center/) monitors hello security state of your Azure resources in order tooprevent and detect threats, and provide recommendations for responding.</span></span> <span data-ttu-id="037dd-240">它會提供數種方式 toohelp 文件您保護 hello 隱私權的個人資料的安全措施。</span><span class="sxs-lookup"><span data-stu-id="037dd-240">It provides several ways toohelp document your security measures that protect hello privacy of personal data.</span></span>

<span data-ttu-id="037dd-241">安全性健康情況監視可協助您確保符合安全性原則的規範。</span><span class="sxs-lookup"><span data-stu-id="037dd-241">Security health monitoring helps you ensure compliance with your security policies.</span></span> <span data-ttu-id="037dd-242">安全性監視是稽核時，不符合組織的標準或最佳作法 tooidentify 系統資源的主動式策略。</span><span class="sxs-lookup"><span data-stu-id="037dd-242">Security monitoring is a proactive strategy that audits your resources tooidentify systems that do not meet organizational standards or best practices.</span></span> <span data-ttu-id="037dd-243">您可以監視下列資源的 hello hello 安全性狀態：</span><span class="sxs-lookup"><span data-stu-id="037dd-243">You can monitor hello security state of hello following resources:</span></span>

- <span data-ttu-id="037dd-244">計算 (虛擬機器和雲端服務)</span><span class="sxs-lookup"><span data-stu-id="037dd-244">Compute (virtual machines and cloud services)</span></span>

- <span data-ttu-id="037dd-245">網路 (虛擬網路)</span><span class="sxs-lookup"><span data-stu-id="037dd-245">Networking (virtual networks)</span></span>

- <span data-ttu-id="037dd-246">儲存體和資料 (伺服器和資料庫稽核和威脅偵測、TDE、儲存體加密)</span><span class="sxs-lookup"><span data-stu-id="037dd-246">Storage and data (server and database auditing and threat detection, TDE, storage encryption)</span></span>

- <span data-ttu-id="037dd-247">應用程式 (潛在安全性問題)</span><span class="sxs-lookup"><span data-stu-id="037dd-247">Applications (potential security issues)</span></span>

<span data-ttu-id="037dd-248">在任何兩個分類中的安全性問題，可能會造成威脅 toohello 隱私權的個人資料。</span><span class="sxs-lookup"><span data-stu-id="037dd-248">Security issues in any of these categories could pose a threat toohello privacy of personal data.</span></span>

#### <a name="how-do-i-view-hello-security-state-of-my-azure-resources"></a><span data-ttu-id="037dd-249">如何檢視我的 Azure 資源 hello 安全性狀態？</span><span class="sxs-lookup"><span data-stu-id="037dd-249">How do I view hello security state of my Azure resources?</span></span>

<span data-ttu-id="037dd-250">資訊安全中心定期分析您的 Azure 資源 hello 安全性狀態。</span><span class="sxs-lookup"><span data-stu-id="037dd-250">Security Center periodically analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="037dd-251">您可以檢視任何潛在的安全性漏洞，它會識別在 hello**防止**hello 儀表板的區段。</span><span class="sxs-lookup"><span data-stu-id="037dd-251">You can view any potential security vulnerabilities it identifies in hello **Prevention** section of hello dashboard.</span></span>

   ![](media/protection-personal-data-azure-reporting-tools/image014.png)

1. <span data-ttu-id="037dd-252">在 hello**防止**區段中，選取 hello**計算**磚。</span><span class="sxs-lookup"><span data-stu-id="037dd-252">In hello **Prevention** section, select hello **Compute** tile.</span></span> <span data-ttu-id="037dd-253">您會在這裡看到**概觀，**以及 hello**虛擬機器**列出的所有 Vm，而且其安全性狀態，並 hello**雲端服務**web 和背景工作角色的清單由資訊安全中心的監視。</span><span class="sxs-lookup"><span data-stu-id="037dd-253">You’ll see here an **Overview,** along with hello **Virtual machines** listing of all VMs and their security states, and hello **Cloud services** list of web and worker roles monitored by Security Center.</span></span>

2. <span data-ttu-id="037dd-254">在 hello**概觀**索引標籤中，第二個建議 tooview 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="037dd-254">On hello **Overview** tab, second a recommendation tooview more information.</span></span>

3. <span data-ttu-id="037dd-255">在 hello**虛擬機器**索引標籤上，選取 VM tooview 其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="037dd-255">On hello **Virtual machines** tab, select a VM tooview additional details.</span></span>

<span data-ttu-id="037dd-256">Azure 資訊安全中心中啟用資料收集時，hello Microsoft Monitoring Agent 會自動佈建所有現有和新的任何支援的已部署之虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="037dd-256">When data collection is enabled in Azure Security Center, hello Microsoft Monitoring Agent is automatically provisioned on all existing and any new supported virtual machines that are deployed.</span></span> <span data-ttu-id="037dd-257">從這個代理程式收集的資料會儲存在與您的訂用帳戶相關聯的現有 [Log Analytics](https://azure.microsoft.com/services/log-analytics/) 工作區或新的工作區中。</span><span class="sxs-lookup"><span data-stu-id="037dd-257">Data collected from this agent is stored in either an existing [Log Analytics](https://azure.microsoft.com/services/log-analytics/) workspace associated with your subscription or a new workspace.</span></span>

<span data-ttu-id="037dd-258">資訊安全中心所提供的[威脅情報報告](https://docs.microsoft.com/azure/security-center/security-center-threat-report)。</span><span class="sxs-lookup"><span data-stu-id="037dd-258">[Threat Intelligence Reports](https://docs.microsoft.com/azure/security-center/security-center-threat-report) are provided by Security Center.</span></span> <span data-ttu-id="037dd-259">這些可讓您 toohelp 分辨 hello 攻擊者的身分識別、 目標、 目前和歷史攻擊活動和的策略，工具和程序使用的有用資訊。</span><span class="sxs-lookup"><span data-stu-id="037dd-259">These give you useful information toohelp discern hello attacker’s identity, objectives, current and historical attack campaigns, and tactics, tools and procedures used.</span></span> <span data-ttu-id="037dd-260">還包含緩和與修復資訊。</span><span class="sxs-lookup"><span data-stu-id="037dd-260">Mitigation and remediation information is also included.</span></span>

<span data-ttu-id="037dd-261">這些威脅報告 hello 主要用途是 toohelp 您 toorespond 有效 toohello 立即威脅和說明 take 之後測量 toomitigate hello 問題。</span><span class="sxs-lookup"><span data-stu-id="037dd-261">hello primary purpose of these threat reports is toohelp you toorespond effectively toohello immediate threat and help take measures afterward toomitigate hello issue.</span></span> <span data-ttu-id="037dd-262">當您在文件您進行報告和稽核事件的回應，hello 報表中的 hello 資訊可以也很有用。</span><span class="sxs-lookup"><span data-stu-id="037dd-262">hello information in hello reports can also be useful when you document your incident response for reporting and auditing purposes.</span></span>

<span data-ttu-id="037dd-263">hello 威脅智慧報表會顯示。PDF 格式，透過 hello 中的連結存取**報表**欄位 hello**可疑的處理程序執行**刀鋒視窗中的每個 Azure 資訊安全中心中的安全性警示。</span><span class="sxs-lookup"><span data-stu-id="037dd-263">hello Threat Intelligence Reports are presented in .PDF format, accessed via a link in hello **Reports** field of hello **Suspicious process executed** blade for each security alert in Azure Security Center.</span></span>

<span data-ttu-id="037dd-264">如需有關並用 tooview hello Threat Intelligence 報告的詳細資訊，請參閱[Azure 安全性中心 Threat Intelligence 報告。](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span><span class="sxs-lookup"><span data-stu-id="037dd-264">For more information on how tooview and use hello Threat Intelligence Report, see [Azure Security Center Threat Intelligence Report.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span></span>

## <a name="next-steps"></a><span data-ttu-id="037dd-265">後續步驟：</span><span class="sxs-lookup"><span data-stu-id="037dd-265">Next Steps:</span></span>

[<span data-ttu-id="037dd-266">開始使用 hello Azure Active Directory 報告 API</span><span class="sxs-lookup"><span data-stu-id="037dd-266">Getting Started with hello Azure Active Directory reporting API</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started-azure-portal)

[<span data-ttu-id="037dd-267">什麼是 Log Analytics？</span><span class="sxs-lookup"><span data-stu-id="037dd-267">What is Log Analytics?</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)

[<span data-ttu-id="037dd-268">Microsoft Azure 中的監視概觀</span><span class="sxs-lookup"><span data-stu-id="037dd-268">Overview of Monitoring in Microsoft Azure</span></span>](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

[<span data-ttu-id="037dd-269">簡介 toohello Azure 活動記錄檔 （影片）</span><span class="sxs-lookup"><span data-stu-id="037dd-269">Introduction toohello Azure Activity Log (video)</span></span>](https://azure.microsoft.com/resources/videos/intro-activity-log/)
