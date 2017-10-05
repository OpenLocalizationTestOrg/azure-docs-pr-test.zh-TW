---
title: "使用 Azure 報告工具記載個人資料的保護 | Microsoft Docs"
description: "如何使用 Azure 報告服務和技術來協助保護個人資料的隱私權。"
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
ms.openlocfilehash: bd9d94f13a304f4bf9818df50541894bdbb4f379
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="document-protection-of-personal-data-with-azure-reporting-tools"></a><span data-ttu-id="55585-103">使用 Azure 報告工具記載個人資料的保護</span><span class="sxs-lookup"><span data-stu-id="55585-103">Document protection of personal data with Azure reporting tools</span></span>

<span data-ttu-id="55585-104">本文探討如何使用 Azure 報告服務和技術來協助保護個人資料的隱私權。</span><span class="sxs-lookup"><span data-stu-id="55585-104">This article will discuss how to use Azure reporting services and technologies to help protect privacy of personal data.</span></span>

## <a name="scenario"></a><span data-ttu-id="55585-105">案例</span><span class="sxs-lookup"><span data-stu-id="55585-105">Scenario</span></span>

<span data-ttu-id="55585-106">總部設於美國的大型郵輪公司將擴展其營運，以提供地中海、亞得里亞海、波羅的海和不列顛群島的行程。</span><span class="sxs-lookup"><span data-stu-id="55585-106">A large cruise company, headquartered in the United States, is expanding its operations to offer itineraries in the Mediterranean, Adriatic, and Baltic seas, as well as the British Isles.</span></span> <span data-ttu-id="55585-107">為了協助這些工作，它收購了以義大利、德國、丹麥和英國為據點的數個較小型郵輪公司。</span><span class="sxs-lookup"><span data-stu-id="55585-107">To help these efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and the U.K.</span></span>

<span data-ttu-id="55585-108">此公司使用 Microsoft Azure 來處理和儲存公司資料。</span><span class="sxs-lookup"><span data-stu-id="55585-108">The company uses Microsoft Azure for processing and storage of corporate data.</span></span> <span data-ttu-id="55585-109">其中包含其全球客戶群的名稱、地址、電話號碼和信用卡資訊等個人識別資訊。</span><span class="sxs-lookup"><span data-stu-id="55585-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="55585-110">它也會包含在所有位置的傳統的人力資源資訊，例如地址、 電話號碼、 稅務識別碼和醫療公司員工的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="55585-110">It also includes traditional Human Resources information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="55585-111">此郵輪公司也會維護獎勵和忠誠度方案會員的大型資料庫，其中包含的個人資訊可追蹤與目前和過去客戶的關係。</span><span class="sxs-lookup"><span data-stu-id="55585-111">The cruise line also maintains a large database of reward and loyalty program members that includes personal information to track relationships with current and past customers.</span></span>

<span data-ttu-id="55585-112">公司員工會從公司的遠端辦公室存取網路，而位於全球的旅行社會存取某些公司資源。</span><span class="sxs-lookup"><span data-stu-id="55585-112">Corporate employees access the network from the company’s remote offices and travel agents located around the world have access to some company resources.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="55585-113">問題陳述</span><span class="sxs-lookup"><span data-stu-id="55585-113">Problem statement</span></span>

<span data-ttu-id="55585-114">公司必須保護透過多層式的安全性策略可使用 Azure 的管理和安全性功能來對進行嚴格控制存取和處理的個人資料，而且必須能夠員工和客戶的個人資料的隱私權示範其保護措施，為內部和外部的稽核員。</span><span class="sxs-lookup"><span data-stu-id="55585-114">The company must protect the privacy of employees’ and customers’ personal data through a multi-layered security strategy that uses Azure management and security features to impose strict controls on access to and processing of personal data, and must be able to demonstrate its protective measures to internal and external auditors.</span></span>

## <a name="company-goal"></a><span data-ttu-id="55585-115">公司目標</span><span class="sxs-lookup"><span data-stu-id="55585-115">Company goal</span></span>

<span data-ttu-id="55585-116">在其深度防禦的安全性策略中，公司目標在於追蹤個人資料的所有存取和處理，並確保個人資料的適當隱私權保護已到位並有作用。</span><span class="sxs-lookup"><span data-stu-id="55585-116">As part of its defense-in-depth security strategy, it is a company goal to track all access to and processing of personal data, and ensure that documentation of adequate privacy protections for personal data are in place and working.</span></span>

## <a name="solutions"></a><span data-ttu-id="55585-117">解決方案</span><span class="sxs-lookup"><span data-stu-id="55585-117">Solutions</span></span>

<span data-ttu-id="55585-118">Microsoft Azure 提供全方位的監視、記錄和診斷工具，協助追蹤及記錄與個人資料存取和處理、資料的地理流程，以及個人資料之第三方存取相關聯的活動和事件。</span><span class="sxs-lookup"><span data-stu-id="55585-118">Microsoft Azure provides comprehensive monitoring, logging, and diagnostics tools to help track and record activities and events associated with accessing and processing personal data, geographic flow of data, and third-party access to personal data.</span></span> <span data-ttu-id="55585-119">因為雲端中個人資料的安全性是共同的責任，所以 Microsoft 也會提供給客戶：</span><span class="sxs-lookup"><span data-stu-id="55585-119">Because security of personal data in the cloud is a shared responsibility, Microsoft also provides customers with:</span></span>

- <span data-ttu-id="55585-120">其自己處理客戶資料的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="55585-120">Detailed information about its own processing of customers’ data</span></span>

- <span data-ttu-id="55585-121">由 Microsoft 管理的安全性措施</span><span class="sxs-lookup"><span data-stu-id="55585-121">Security measures administered by Microsoft</span></span>

- <span data-ttu-id="55585-122">其傳送客戶資料的位置和方式</span><span class="sxs-lookup"><span data-stu-id="55585-122">Where and how it sends customers’ data</span></span>

- <span data-ttu-id="55585-123">Microsoft 自有隱私權檢閱程序的詳細資料</span><span class="sxs-lookup"><span data-stu-id="55585-123">Details of Microsoft’s own privacy reviews process</span></span>

### <a name="azure-active-directory"></a><span data-ttu-id="55585-124">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="55585-124">Azure Active Directory</span></span>

<span data-ttu-id="55585-125">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) 是 Microsoft 的雲端式、多租用戶目錄和身分識別管理服務。</span><span class="sxs-lookup"><span data-stu-id="55585-125">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) is Microsoft’s cloud-based, multi-tenant directory and identity management service.</span></span> <span data-ttu-id="55585-126">服務的登入和稽核報告功能提供您詳細的登入和應用程式使用活動資訊，以協助您監視及確保客戶和員工個人資料的適當存取。</span><span class="sxs-lookup"><span data-stu-id="55585-126">The service’s sign-in and audit reporting capabilities provide you with detailed sign-in and application usage activity information to help you monitor and ensure proper access to customers’ and employees’ personal data.</span></span>

<span data-ttu-id="55585-127">活動報告類型有兩種︰</span><span class="sxs-lookup"><span data-stu-id="55585-127">There are two types of activity reports:</span></span>

- <span data-ttu-id="55585-128">[稽核活動報告/記錄](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs)提供系統活動/工作的詳細記錄</span><span class="sxs-lookup"><span data-stu-id="55585-128">The [audit activity reports/logs](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) provide a detailed record of system activities/tasks</span></span>

- <span data-ttu-id="55585-129">[登入活動報告/記錄](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins)顯示執行稽核報告中所列之每個活動的人員</span><span class="sxs-lookup"><span data-stu-id="55585-129">The [sign-ins activity report/log](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins) shows you who has performed each activity listed in the audit report</span></span>

<span data-ttu-id="55585-130">兩者併用，可以追蹤每項已執行工作及其執行人員的歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="55585-130">Using the two together, you can track the history of every task performed and who performed each.</span></span> <span data-ttu-id="55585-131">這兩種報告均可自訂和篩選。</span><span class="sxs-lookup"><span data-stu-id="55585-131">Both types of reports are customizable and can be filtered.</span></span>

#### <a name="how-do-i-access-the-audit-and-security-logs"></a><span data-ttu-id="55585-132">如何存取稽核和安全性記錄？</span><span class="sxs-lookup"><span data-stu-id="55585-132">How do I access the audit and security logs?</span></span>

<span data-ttu-id="55585-133">您可以用三種不同的方式從 Active Directory 入口網站存取稽核和安全性記錄：透過 [活動] 區段 (選取 [稽核記錄] 或 [登入])，或在 Active Directory 中從 [管理] 之下的 [使用者和群組] 或 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="55585-133">The audit and security logs can be accessed from the Active Directory portal in three different ways: through the **Activity** section (select either **Audit logs** or **Sign-ins**), or from **Users and groups** or **Enterprise applications** under **Manage** in Active Directory.</span></span> <span data-ttu-id="55585-134">透過 Azure Active Directory 報告 API 也可以存取報告。</span><span class="sxs-lookup"><span data-stu-id="55585-134">Reports can also be accessed through the Azure Active Directory reporting API.</span></span> 

1. <span data-ttu-id="55585-135">在 Azure 入口網站中，選取 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="55585-135">In the Azure portal, select **Azure Active Directory.**</span></span>

2. <span data-ttu-id="55585-136">在 [活動] 區段中，選取 [稽核警示]。</span><span class="sxs-lookup"><span data-stu-id="55585-136">In the **Activity** section, select **Audit logs.**</span></span>

    ![](media/protection-personal-data-azure-reporting-tools/image001.png)

3. <span data-ttu-id="55585-137">按一下工具列中的 [資料行] 來自訂清單檢視。</span><span class="sxs-lookup"><span data-stu-id="55585-137">Customize the list view by clicking **Columns** in the toolbar.</span></span>

4.  <span data-ttu-id="55585-138">選取清單檢視中的項目，即可查看所有可用的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="55585-138">Select an item in the list view to see all available details about it.</span></span>

    ![](media/protection-personal-data-azure-reporting-tools/image003.png)

<span data-ttu-id="55585-139">Azure Active Directory 報告還包含兩種類型的安全性報告：[標幟為有風險的使用者]和 [有風險的登入]，這可協助您監視 Azure 環境中的潛在風險。</span><span class="sxs-lookup"><span data-stu-id="55585-139">Azure Active Directory reporting also includes two types of security reports, **users flagged for risk** and **risky sign-ins**, which can help you monitor potential risks in your Azure environment.</span></span>

<span data-ttu-id="55585-140">如需報告服務的詳細資訊，請參閱 [Azure Active Directory 報告](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal)</span><span class="sxs-lookup"><span data-stu-id="55585-140">For more information about the reporting service, see [Azure Active Directory reporting](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal)</span></span>

<span data-ttu-id="55585-141">如需 Azure Active Directory 中可用報告的特定資訊，請瀏覽 [Azure Active Directory 活動報告](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal#activity-reports)。</span><span class="sxs-lookup"><span data-stu-id="55585-141">Visit [Azure Active Directory activity reports](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal#activity-reports) for more specifics about the reports available in Azure Active Directory.</span></span> <span data-ttu-id="55585-142">這個網站包含如何在入口網站中存取及使用[稽核記錄活動報告](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs)和[登入活動報告](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins)的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="55585-142">This site includes more details about how to access and use [audit logs activity reports](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) and [sign-in activity reports](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins) in the portal.</span></span> <span data-ttu-id="55585-143">它也包含[標幟為有風險的使用者](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-user-at-risk)和[有風險的登入](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-risky-sign-ins)安全性報告的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="55585-143">It also includes information about [users flagged for risk](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-user-at-risk) and [risky sign-in](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-risky-sign-ins) security reports.</span></span>

<span data-ttu-id="55585-144">有關如何以程式設計方式連線到 Azure Active Directory 報告的詳細資訊，請瀏覽 [Azure Active Directory 稽核 API 參考](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-audit-reference)。</span><span class="sxs-lookup"><span data-stu-id="55585-144">Visit the [Azure Active Directory audit API reference](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-audit-reference) site for more information on how to connect to Azure Directory reporting programmatically.</span></span>

### <a name="log-analytics"></a><span data-ttu-id="55585-145">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="55585-145">Log Analytics</span></span>

<span data-ttu-id="55585-146">[Log Analytics](https://azure.microsoft.com/services/log-analytics/) 可以[從 Azure 監視器收集資料](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-storage)，使它與其他資料相互關聯並提供其他分析。</span><span class="sxs-lookup"><span data-stu-id="55585-146">[Log Analytics](https://azure.microsoft.com/services/log-analytics/) can [collect data from Azure Monitor](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-storage) to correlate it with other data and provide additional analysis.</span></span> <span data-ttu-id="55585-147">Azure 監視器可收集和分析 Azure 環境的監視資料。</span><span class="sxs-lookup"><span data-stu-id="55585-147">Azure Monitor collects and analyzes monitoring data for your Azure environment.</span></span> 

<span data-ttu-id="55585-148">Log Analytics 中的分析工具 (例如記錄搜尋、檢視和解決方案) 可處理所有收集的資料，進而為您提供整個環境的集中式分析。</span><span class="sxs-lookup"><span data-stu-id="55585-148">Analysis tools in Log Analytics such as log searches, views, and solutions work against all collected data, providing you with centralized analysis of your entire environment.</span></span> <span data-ttu-id="55585-149">Log Analytics 可彙總及分析 Windows 事件記錄、IIS 記錄和 Syslog，其有助於偵測可能會對未經授權的使用者公開個人資料的潛在個人資料缺口。</span><span class="sxs-lookup"><span data-stu-id="55585-149">Log Analytics can aggregate and analyze Windows Event logs, IIS logs, and Syslogs, which can help detect potential personal data breaches that could expose personal data to unauthorized users.</span></span>

#### <a name="how-do-i-use-log-analytics"></a><span data-ttu-id="55585-150">如何使用 Log Analytics？</span><span class="sxs-lookup"><span data-stu-id="55585-150">How do I use Log Analytics?</span></span>

<span data-ttu-id="55585-151">您可以透過 OMS 入口網站或 Azure 入口網站，從任何網頁瀏覽器存取 Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="55585-151">You can access Log Analytics through the OMS portal or the Azure portal, from any web browser.</span></span> <span data-ttu-id="55585-152">Log Analytics 包含可快速擷取及彙總存放庫中資料的查詢語言。</span><span class="sxs-lookup"><span data-stu-id="55585-152">Log Analytics includes a query language to quickly retrieve and consolidate data in the repository.</span></span> <span data-ttu-id="55585-153">您可以建立及儲存記錄搜尋，直接在入口網站中分析資料。</span><span class="sxs-lookup"><span data-stu-id="55585-153">You can create and save Log Searches to directly analyze data in the portal.</span></span>

<span data-ttu-id="55585-154">若要在 Azure 入口網站中建立 Log Analytics 工作區，請執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="55585-154">To create a Log Analytics workspace in the Azure portal, do the following:</span></span>

1. <span data-ttu-id="55585-155">從 Marketplace 中的服務清單選取 **Log Analytics**。</span><span class="sxs-lookup"><span data-stu-id="55585-155">Select **Log Analytics** from the list of services in the Marketplace.</span></span>

2. <span data-ttu-id="55585-156">選取 [建立]，然後指定 OMS 工作區的名稱、選取您的訂用帳戶、資源群組、位置和定價層。</span><span class="sxs-lookup"><span data-stu-id="55585-156">Select **Create,** then specify the name of your OMS workspace, select your subscription, resource group, location, and pricing tier.</span></span>

3. <span data-ttu-id="55585-157">按一下 [確定] 以顯示工作區清單。</span><span class="sxs-lookup"><span data-stu-id="55585-157">Click **OK** to display a list of your workspaces.</span></span>

4. <span data-ttu-id="55585-158">選取工作區以查看其詳細資料。</span><span class="sxs-lookup"><span data-stu-id="55585-158">Select a workspace to see its details.</span></span>

    ![](media/protection-personal-data-azure-reporting-tools/image004.png)

<span data-ttu-id="55585-159">若要深入了解這項服務，請瀏覽 [Log Analytics 文件](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)。</span><span class="sxs-lookup"><span data-stu-id="55585-159">Visit the [Log Analytics documentation](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) to learn more about the service.</span></span>

<span data-ttu-id="55585-160">瀏覽[開始使用 Log Analytics 工作區](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)教學課程，以建立評估工作區並了解如何使用此服務的基本概念。</span><span class="sxs-lookup"><span data-stu-id="55585-160">Visit the [Get started with a Log Analytics workspace](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started) tutorial to create an evaluation workspace and learn the basics of how to use the service.</span></span>

<span data-ttu-id="55585-161">有關如何連線以使用 Log Analytics 搭配上述記錄的特定資訊，請瀏覽下列網頁：</span><span class="sxs-lookup"><span data-stu-id="55585-161">Visit the following web pages for more specific information on how to connect to use Log Analytics with the logs described above:</span></span>

[<span data-ttu-id="55585-162">Log Analytics 中的 Windows 事件記錄資料來源</span><span class="sxs-lookup"><span data-stu-id="55585-162">Windows event logs data sources in Log Analytics</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events)

[<span data-ttu-id="55585-163">Log Analytics 中的 IIS 記錄</span><span class="sxs-lookup"><span data-stu-id="55585-163">IIS logs in Log Analytics</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-iis-logs)

[<span data-ttu-id="55585-164">Log Analytics 中的 Syslog 資料來源</span><span class="sxs-lookup"><span data-stu-id="55585-164">Syslog data sources in Log Analytics</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-syslog)

### <a name="azure-monitorazure-activity-log"></a><span data-ttu-id="55585-165">Azure 監視器/Azure 活動記錄</span><span class="sxs-lookup"><span data-stu-id="55585-165">Azure Monitor/Azure Activity Log</span></span> 

<span data-ttu-id="55585-166">[Azure 監視器](https://azure.microsoft.com/services/monitor/)可針對 Microsoft Azure 中的大多數服務提供基本等級的基礎結構計量與記錄。</span><span class="sxs-lookup"><span data-stu-id="55585-166">[Azure Monitor](https://azure.microsoft.com/services/monitor/) provides base level infrastructure metrics and logs for most services in Microsoft Azure.</span></span>
<span data-ttu-id="55585-167">監視功能可協助您取得 Azure 應用程式的深入解析。</span><span class="sxs-lookup"><span data-stu-id="55585-167">Monitoring can help you to gain deep insights about your Azure applications.</span></span> <span data-ttu-id="55585-168">Azure 監視器依賴 Azure 診斷擴充功能 (Windows 或 Linux) 來收集大多數應用程式等級的計量和記錄。</span><span class="sxs-lookup"><span data-stu-id="55585-168">Azure Monitor relies on the Azure diagnostics extension (Windows or Linux) to collect most application level metrics and logs.</span></span> <span data-ttu-id="55585-169">[Azure 活動記錄](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)是您可以使用 Azure 監視器檢視的其中一項資源。</span><span class="sxs-lookup"><span data-stu-id="55585-169">[The Azure Activity Log](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) is one of the resources you can view with Azure Monitor.</span></span> <span data-ttu-id="55585-170">它會追蹤每個 API 呼叫，並提供有關在 [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) 中發生之活動的豐富資訊。</span><span class="sxs-lookup"><span data-stu-id="55585-170">It tracks every API call, and provides a wealth of information about activities that occur in [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span></span>
<span data-ttu-id="55585-171">您可以搜尋活動記錄檔 (之前稱為「作業記錄」或「稽核記錄」)，以取得 Azure 基礎結構所見之資源的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="55585-171">You can search the Activity Log (previously called Operational or Audit Logs) for information about your resource as seen by the Azure infrastructure.</span></span> 

<span data-ttu-id="55585-172">雖然活動記錄中所記錄的大部分資訊與效能和服務健康情況有關，但也有與資料保護相關的資訊。</span><span class="sxs-lookup"><span data-stu-id="55585-172">Although much of the information recorded in the Activity log pertains to performance and service health, there is also information that is related to protection of data.</span></span> <span data-ttu-id="55585-173">您可以使用活動記錄來判斷 Azure 訂用帳戶中的資源上任何寫入作業 (PUT、POST、DELETE) 的「內容、對象和時間」。</span><span class="sxs-lookup"><span data-stu-id="55585-173">Using the Activity Log, you can determine the “what, who, and when” for any write operations (PUT, POST, DELETE) taken on the resources in your Azure subscription.</span></span>

<span data-ttu-id="55585-174">例如，當系統管理員刪除網路安全性群組 (這可能會影響個人資料的保護) 時，它會提供一筆記錄。</span><span class="sxs-lookup"><span data-stu-id="55585-174">For example, it provides a record when an administrator deletes a network security group, which could impact the protection of personal data.</span></span> <span data-ttu-id="55585-175">活動記錄項目會儲存在 Azure 監視器中長達 90 天。</span><span class="sxs-lookup"><span data-stu-id="55585-175">Activity log entries are stored in Azure Monitor for 90 days.</span></span>

#### <a name="how-do-i-use-the-data-collected-by-azure-monitor"></a><span data-ttu-id="55585-176">如何使用 Azure 監視器所收集的資料？</span><span class="sxs-lookup"><span data-stu-id="55585-176">How do I use the data collected by Azure Monitor?</span></span>

<span data-ttu-id="55585-177">有數種方式可使用活動記錄和其他 Azure 監視器資源中的資料。</span><span class="sxs-lookup"><span data-stu-id="55585-177">There are a number of ways to use the data in the Activity log and other Azure Monitor resources.</span></span>

- <span data-ttu-id="55585-178">您可以將資料即時串流到其他位置。</span><span class="sxs-lookup"><span data-stu-id="55585-178">You can stream the data to other locations in real line.</span></span>

- <span data-ttu-id="55585-179">使用 [Azure 儲存體帳戶](https://docs.microsoft.com/azure/storage/common/storage-introduction)及設定保留原則，即可讓資料的儲存期間超過預設值。</span><span class="sxs-lookup"><span data-stu-id="55585-179">You can store the data for longer time periods than the defaults, using an [Azure storage account](https://docs.microsoft.com/azure/storage/common/storage-introduction) and setting a retention policy.</span></span>

- <span data-ttu-id="55585-180">您可以使用 [Azure 入口網站](https://azure.microsoft.com/features/azure-portal/)、[Azure Application Insights](https://azure.microsoft.com/services/application-insights/)、[Microsoft PowerBI](https://powerbi.microsoft.com/) 或第三方視覺效果工具，將圖形和圖表中的資料視覺化。</span><span class="sxs-lookup"><span data-stu-id="55585-180">You can visual the data in graphics and charts, using the [Azure portal](https://azure.microsoft.com/features/azure-portal/), [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), [Microsoft PowerBI](https://powerbi.microsoft.com/), or third-party visualization tools.</span></span>

- <span data-ttu-id="55585-181">您可以使用 Azure 監視器 REST API、CLI 命令、[PowerShell](https://docs.microsoft.com/powershell/) cmdlet 或 .NET SDK 來查詢資料。</span><span class="sxs-lookup"><span data-stu-id="55585-181">You can query the data using the Azure Monitor REST API, CLI commands, [PowerShell](https://docs.microsoft.com/powershell/) cmdlets, or the .NET SDK.</span></span>

<span data-ttu-id="55585-182">若要開始使用 Azure 監視器，請在 Azure 入口網站中選取 [更多服務]。</span><span class="sxs-lookup"><span data-stu-id="55585-182">To get started with Azure Monitor, select **More Services** in the Azure portal.</span></span>

1. <span data-ttu-id="55585-183">向下捲動至 [監視與管理] 區段中的 [監視器]。</span><span class="sxs-lookup"><span data-stu-id="55585-183">Scroll down to **Monitor** in the **Monitoring and Managing** section.</span></span>

    ![](media/protection-personal-data-azure-reporting-tools/image005.png)

2.  <span data-ttu-id="55585-184">監視器會在 [活動記錄] 檢視中開啟。</span><span class="sxs-lookup"><span data-stu-id="55585-184">Monitor opens in the **Activity Log** view.</span></span>

    ![](media/protection-personal-data-azure-reporting-tools/image007.png)

<span data-ttu-id="55585-185">您可以建立並儲存一般篩選的查詢，然後將最重要的查詢釘選至入口網站儀表板，這樣只要發生符合您準則的事件時就會通知您。</span><span class="sxs-lookup"><span data-stu-id="55585-185">You can create and save queries for common filters, then pin the most important queries to a portal dashboard so you'll always know if events that meet your criteria have occurred.</span></span>

1. <span data-ttu-id="55585-186">您可以依照資源群組、時間範圍和事件類別來篩選檢視。</span><span class="sxs-lookup"><span data-stu-id="55585-186">You can filter the view by resource group, timespan, and event category.</span></span>

    ![](media/protection-personal-data-azure-reporting-tools/image008.png)

2. <span data-ttu-id="55585-187">然後按一下 [釘選] 按鈕，即可將查詢釘選到入口網站儀表板。</span><span class="sxs-lookup"><span data-stu-id="55585-187">You can then pin queries to a portal dashboard by clicking the **Pin** button.</span></span> <span data-ttu-id="55585-188">這可協助您在服務上建立作業資料的單一資訊來源。</span><span class="sxs-lookup"><span data-stu-id="55585-188">This helps you create a single source of information for operational  data on your services.</span></span> <span data-ttu-id="55585-189">儀表板上會顯示查詢名稱和結果筆數。</span><span class="sxs-lookup"><span data-stu-id="55585-189">The query name and number of results will be displayed on the dashboard.</span></span>

<span data-ttu-id="55585-190">您也可以使用監視器來檢視所有 Azure 資源的計量、設定診斷設定和警示，以及搜尋記錄。</span><span class="sxs-lookup"><span data-stu-id="55585-190">You can also use the Monitor to view metrics for all Azure resources, configure diagnostics settings and alerts, and search the log.</span></span> <span data-ttu-id="55585-191">有關如何使用 Azure 監視器和活動記錄的詳細資訊，請參閱[開始使用 Azure 監視器](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-get-started)。</span><span class="sxs-lookup"><span data-stu-id="55585-191">For more information on how to use the Azure Monitor and Activity Log, see [Get Started with Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-get-started).</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="55585-192">Azure 診斷</span><span class="sxs-lookup"><span data-stu-id="55585-192">Azure Diagnostics</span></span> 

<span data-ttu-id="55585-193">Azure 中的診斷功能可以從數個來源收集資料。</span><span class="sxs-lookup"><span data-stu-id="55585-193">The diagnostics capability in Azure enables collection of data from several sources.</span></span> <span data-ttu-id="55585-194">Windows 事件記錄 (其中包括安全性記錄) 在追蹤和記載個人資料的保護時特別有用。</span><span class="sxs-lookup"><span data-stu-id="55585-194">The Windows Event logs, which include the Security log, can be especially useful in tracking and documenting protection of personal data.</span></span> <span data-ttu-id="55585-195">安全性記錄可追蹤登入成功和失敗事件，以及權限變更、指出特定攻擊類型的偵測模式、安全性相關原則變更、安全性群組成員資格變更等等。</span><span class="sxs-lookup"><span data-stu-id="55585-195">The security log tracks logon success and failure events, as well as permissions changes, detection of patterns indicating certain types of attacks, changes to security-related policies, security group membership changes, and much more.</span></span>

<span data-ttu-id="55585-196">例如，事件識別碼 4695 會警示您，有人嘗試解除保護可稽核的受保護資料。</span><span class="sxs-lookup"><span data-stu-id="55585-196">For example, Event ID 4695 alerts you to the attempted unprotection of auditable protected data.</span></span> <span data-ttu-id="55585-197">這屬於資料保護 API (DPAPI)，其可協助您保護資料，例如私密金鑰、預存認證和其他機密資訊。</span><span class="sxs-lookup"><span data-stu-id="55585-197">This pertains to the Data Protection API (DPAPI), which helps to protect data such as private keys, stored credentials, and other confidential information.</span></span>

#### <a name="how-do-i-enable-the-diagnostics-extension-for-windows-vms"></a><span data-ttu-id="55585-198">如何啟用 Windows VM 的診斷擴充功能？</span><span class="sxs-lookup"><span data-stu-id="55585-198">How do I enable the diagnostics extension for Windows VMs?</span></span>

<span data-ttu-id="55585-199">您可以使用 PowerShell 來啟用 Windows VM 的診斷擴充功能，以便收集記錄資料。</span><span class="sxs-lookup"><span data-stu-id="55585-199">You can use PowerShell to enable the diagnostics extension for a Windows VM, so as to collect log data.</span></span> <span data-ttu-id="55585-200">這麼做的步驟取決於您使用的部署模型 (Resource Manager 或傳統)。</span><span class="sxs-lookup"><span data-stu-id="55585-200">The steps for doing so depend on which deployment model you use (Resource Manager or Classic).</span></span> <span data-ttu-id="55585-201">若要在透過 Resource Manager 部署模型所建立的現有 VM 上啟用診斷擴充功能，您可以使用 [Set-AzureRMVMDiagnosticsExtension PowerShell cmdlet](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension?view=azurermps-4.3.1)。</span><span class="sxs-lookup"><span data-stu-id="55585-201">To enable the diagnostics extension on an existing VM that was created through the Resource Manager deployment model, you can use the [Set-AzureRMVMDiagnosticsExtension PowerShell cmdlet](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension?view=azurermps-4.3.1).</span></span>

   ![](media/protection-personal-data-azure-reporting-tools/image009.png)

<span data-ttu-id="55585-202">*\$diagnosticsconfig_path* 是包含診斷組態之 XML 檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="55585-202">*\$diagnosticsconfig_path* is the path to the file that contains the diagnostics configuration in XML.</span></span> <span data-ttu-id="55585-203">如需在 VM 上啟用 Azure 診斷的詳細指示，請參閱[使用 PowerShell 在執行 Windows 的虛擬機器中啟用 Azure 診斷](https://docs.microsoft.com/azure/virtual-machines/windows/ps-extensions-diagnostics)。</span><span class="sxs-lookup"><span data-stu-id="55585-203">For more detailed instructions on enabling Azure Diagnostics on a VM, see [Use PowerShell to enable Azure Diagnostics in a virtual machine running Windows.](https://docs.microsoft.com/azure/virtual-machines/windows/ps-extensions-diagnostics)</span></span>

<span data-ttu-id="55585-204">Azure 診斷擴充功能可以將所收集的資料傳輸到 Azure 儲存體帳戶，或傳送到 Application Insights 之類的服務。</span><span class="sxs-lookup"><span data-stu-id="55585-204">The Azure diagnostics extension can transfer the collected data to an Azure storage account or send it to services such as Application Insights.</span></span> <span data-ttu-id="55585-205">您可以接著使用資料進行稽核。</span><span class="sxs-lookup"><span data-stu-id="55585-205">You can then use the data for auditing.</span></span>

#### <a name="how-do-i-store-and-view-diagnostic-data"></a><span data-ttu-id="55585-206">如何儲存和檢視診斷資料？</span><span class="sxs-lookup"><span data-stu-id="55585-206">How do I store and view diagnostic data?</span></span>

<span data-ttu-id="55585-207">請務必記住，除非您將診斷資料傳輸至 Microsoft Azure 儲存體模擬器或 Azure 儲存體，否則不會永久儲存診斷資料。</span><span class="sxs-lookup"><span data-stu-id="55585-207">It’s important to remember that diagnostic data is not permanently stored unless you transfer it to the Microsoft Azure storage emulator or to Azure storage.</span></span> <span data-ttu-id="55585-208">若要在 Azure 儲存體中儲存和檢視診斷資料，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="55585-208">To store and view diagnostic data in Azure Storage, follow these steps:</span></span>

1. <span data-ttu-id="55585-209">在 ServiceConfiguration.cscfg 檔案中指定儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="55585-209">Specify a storage account in the ServiceConfiguration.cscfg file.</span></span> <span data-ttu-id="55585-210">視資料類型而定，Azure 診斷可以使用 Blob 服務或資料表服務。</span><span class="sxs-lookup"><span data-stu-id="55585-210">Azure Diagnostics can use either the Blob service or the Table service, depending on the type of data.</span></span> <span data-ttu-id="55585-211">Windows 事件記錄會以資料表格式儲存。</span><span class="sxs-lookup"><span data-stu-id="55585-211">Windows Event logs are stored in Table format.</span></span>

2. <span data-ttu-id="55585-212">傳輸資料。</span><span class="sxs-lookup"><span data-stu-id="55585-212">Transfer the data.</span></span> <span data-ttu-id="55585-213">您可以透過組態檔要求傳輸診斷資料。</span><span class="sxs-lookup"><span data-stu-id="55585-213">You can request to transfer the diagnostic data through the configuration file.</span></span> <span data-ttu-id="55585-214">若為 SDK 2.4 和較舊版本，您也可以程式設計方式提出此要求。</span><span class="sxs-lookup"><span data-stu-id="55585-214">For SDK 2.4 and previous, you can also make the request programmatically.</span></span>

3. <span data-ttu-id="55585-215">在 Visual Studio 中使用 [Azure 儲存體總管](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer)、[伺服器總管](https://docs.microsoft.com/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage)，或在 Azure Management Studio 中使用 [Azure 診斷管理員](https://www.cerebrata.com/products/azure-diagnostics-manager)來檢視資料。</span><span class="sxs-lookup"><span data-stu-id="55585-215">View the data, using [Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer),  [Server Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage) in Visual Studio, or [Azure Diagnostics Manager](https://www.cerebrata.com/products/azure-diagnostics-manager) in Azure Management Studio.</span></span>

<span data-ttu-id="55585-216">有關如何執行上述每個步驟的詳細資訊，請參閱[在 Azure 儲存體中儲存和檢視診斷資料](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics-storage)。</span><span class="sxs-lookup"><span data-stu-id="55585-216">For more information on how to perform each of these steps, see [Store and view diagnostic data in Azure Storage.](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics-storage)</span></span>

### <a name="azure-storage-analytics"></a><span data-ttu-id="55585-217">Azure 儲存體分析</span><span class="sxs-lookup"><span data-stu-id="55585-217">Azure Storage Analytics</span></span> 

<span data-ttu-id="55585-218">儲存體分析會記錄對儲存體服務之成功和失敗要求的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="55585-218">Storage Analytics logs detailed information about successful and failed requests to a storage service.</span></span> <span data-ttu-id="55585-219">此資訊可用來監視個別要求，這有助於記載儲存在服務中的個人資料存取權。</span><span class="sxs-lookup"><span data-stu-id="55585-219">This information can be used to monitor individual requests, which can help in documenting access to personal data stored in the service.</span></span> <span data-ttu-id="55585-220">不過，根據預設，儲存體帳戶不會啟用儲存體分析記錄功能。</span><span class="sxs-lookup"><span data-stu-id="55585-220">However, Storage Analytics logging is not enabled by default for your storage account.</span></span> <span data-ttu-id="55585-221">您可以在 Azure 入口網站中將它啟用。</span><span class="sxs-lookup"><span data-stu-id="55585-221">You can enable it in the Azure portal.</span></span>

#### <a name="how-do-i-configure-monitoring-for-a-storage-account"></a><span data-ttu-id="55585-222">如何設定儲存體帳戶的監視？</span><span class="sxs-lookup"><span data-stu-id="55585-222">How do I configure monitoring for a storage account?</span></span>

<span data-ttu-id="55585-223">若要設定儲存體帳戶的監視，請執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="55585-223">To configure monitoring for a storage account, do the following:</span></span>

1. <span data-ttu-id="55585-224">在 Azure 入口網站中選取 [儲存體帳戶]，然後選取您要監視的帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="55585-224">Select **Storage accounts** in the Azure portal, then select the name of the account you want to monitor.</span></span>

    ![](media/protection-personal-data-azure-reporting-tools/image011.png)

2. <span data-ttu-id="55585-225">在 [監視] 區段中，選取 [診斷]。</span><span class="sxs-lookup"><span data-stu-id="55585-225">In the **Monitoring** section, select **Diagnostics.**</span></span>

3.  <span data-ttu-id="55585-226">選取您想為每項服務監視的計量資料**類型** (Blob、資料表、檔案)。</span><span class="sxs-lookup"><span data-stu-id="55585-226">Select the **type** of metrics data you want to monitor for each service (Blob, Table, File).</span></span> <span data-ttu-id="55585-227">若要指示 Azure 儲存體，將 Blob、資料表和佇列服務之讀取、寫入及刪除要求的診斷記錄儲存起來，請選取 [Blob 記錄、資料表記錄] 和 [佇列記錄]。</span><span class="sxs-lookup"><span data-stu-id="55585-227">To instruct Azure Storage to save diagnostics logs for read, write, and delete requests for the blob, table, and queue services, select **Blob logs, Table logs** and **Queue logs.**</span></span>

    ![](media/protection-personal-data-azure-reporting-tools/image013.png)

4. <span data-ttu-id="55585-228">使用底部的滑桿來設定 [保留] 原則 (1 – 365 的天數值)。</span><span class="sxs-lookup"><span data-stu-id="55585-228">Using the slider at the bottom, set the **retention** policy in days (value of 1 – 365).</span></span> <span data-ttu-id="55585-229">預設值為 7 天。</span><span class="sxs-lookup"><span data-stu-id="55585-229">Seven days is the default.</span></span>

5. <span data-ttu-id="55585-230">選取 [儲存] 以套用組態設定。</span><span class="sxs-lookup"><span data-stu-id="55585-230">Select **Save** to apply the configuration settings.</span></span>

<span data-ttu-id="55585-231">儲存體記錄的記錄項目包含個別要求的下列資訊：</span><span class="sxs-lookup"><span data-stu-id="55585-231">Storage Logging log entries contain the following information about individual requests:</span></span>

- <span data-ttu-id="55585-232">時間資訊，例如開始時間、端對端延遲和伺服器延遲。</span><span class="sxs-lookup"><span data-stu-id="55585-232">Timing information such as start time, end-to-end latency, and server latency.</span></span>

- <span data-ttu-id="55585-233">儲存體作業的詳細資料，例如作業類型、用戶端存取之儲存體物件的索引鍵、成功或失敗，以及傳回至用戶端的 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="55585-233">Details of the storage operation such as the operation type, the key of the storage object the client is accessing, success or failure, and the HTTP   status code returned to the client.</span></span>

- <span data-ttu-id="55585-234">驗證詳細資料，例如用戶端所使用的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="55585-234">Authentication details such as the type of authentication the client used.</span></span>

- <span data-ttu-id="55585-235">並行資訊，例如 ETag 值和上次修改的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="55585-235">Concurrency information such as the ETag value and last modified timestamp.</span></span>

- <span data-ttu-id="55585-236">要求和回應訊息的大小。</span><span class="sxs-lookup"><span data-stu-id="55585-236">The sizes of the request and response messages.</span></span>

<span data-ttu-id="55585-237">有關如何啟用儲存體分析記錄的詳細指示，請參閱[在 Azure 入口網站中監視儲存體帳戶](https://docs.microsoft.com/azure/storage/common/storage-monitor-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="55585-237">For more detailed instructions on how to enable Storage Analytics logging, see [Monitor a storage account in the Azure portal.](https://docs.microsoft.com/azure/storage/common/storage-monitor-storage-account)</span></span>

### <a name="azure-security-center"></a><span data-ttu-id="55585-238">Azure 資訊安全中心</span><span class="sxs-lookup"><span data-stu-id="55585-238">Azure Security Center</span></span> 

<span data-ttu-id="55585-239">[Azure 資訊安全中心](https://azure.microsoft.com/services/security-center/)會監視 Azure 資源的安全性狀態，以便防止和偵測威脅，並提供回應的建議。</span><span class="sxs-lookup"><span data-stu-id="55585-239">[Azure Security Center](https://azure.microsoft.com/services/security-center/) monitors the security state of your Azure resources in order to prevent and detect threats, and provide recommendations for responding.</span></span> <span data-ttu-id="55585-240">它會提供數種方式，協助記載保護個人資料隱私權的安全性措施。</span><span class="sxs-lookup"><span data-stu-id="55585-240">It provides several ways to help document your security measures that protect the privacy of personal data.</span></span>

<span data-ttu-id="55585-241">安全性健康情況監視可協助您確保符合安全性原則的規範。</span><span class="sxs-lookup"><span data-stu-id="55585-241">Security health monitoring helps you ensure compliance with your security policies.</span></span> <span data-ttu-id="55585-242">安全性監視是一個主動式策略，可稽核您的資源，以識別不符合組織標準或最佳做法的系統。</span><span class="sxs-lookup"><span data-stu-id="55585-242">Security monitoring is a proactive strategy that audits your resources to identify systems that do not meet organizational standards or best practices.</span></span> <span data-ttu-id="55585-243">您可以監視下列資源的安全性狀態：</span><span class="sxs-lookup"><span data-stu-id="55585-243">You can monitor the security state of the following resources:</span></span>

- <span data-ttu-id="55585-244">計算 (虛擬機器和雲端服務)</span><span class="sxs-lookup"><span data-stu-id="55585-244">Compute (virtual machines and cloud services)</span></span>

- <span data-ttu-id="55585-245">網路 (虛擬網路)</span><span class="sxs-lookup"><span data-stu-id="55585-245">Networking (virtual networks)</span></span>

- <span data-ttu-id="55585-246">儲存體和資料 (伺服器和資料庫稽核和威脅偵測、TDE、儲存體加密)</span><span class="sxs-lookup"><span data-stu-id="55585-246">Storage and data (server and database auditing and threat detection, TDE, storage encryption)</span></span>

- <span data-ttu-id="55585-247">應用程式 (潛在安全性問題)</span><span class="sxs-lookup"><span data-stu-id="55585-247">Applications (potential security issues)</span></span>

<span data-ttu-id="55585-248">任何兩個類別中的安全性問題可能會對個人資料的隱私權造成威脅。</span><span class="sxs-lookup"><span data-stu-id="55585-248">Security issues in any of these categories could pose a threat to the privacy of personal data.</span></span>

#### <a name="how-do-i-view-the-security-state-of-my-azure-resources"></a><span data-ttu-id="55585-249">如何檢視 Azure 資源的安全性狀態？</span><span class="sxs-lookup"><span data-stu-id="55585-249">How do I view the security state of my Azure resources?</span></span>

<span data-ttu-id="55585-250">資訊安全中心會定期分析 Azure 資源的安全性狀態。</span><span class="sxs-lookup"><span data-stu-id="55585-250">Security Center periodically analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="55585-251">您可以在儀表板的 [防護] 區段中，檢視它所識別的任何潛在安全性弱點。</span><span class="sxs-lookup"><span data-stu-id="55585-251">You can view any potential security vulnerabilities it identifies in the **Prevention** section of the dashboard.</span></span>

   ![](media/protection-personal-data-azure-reporting-tools/image014.png)

1. <span data-ttu-id="55585-252">在 [防護] 區段中，選取 [計算] 圖格。</span><span class="sxs-lookup"><span data-stu-id="55585-252">In the **Prevention** section, select the **Compute** tile.</span></span> <span data-ttu-id="55585-253">您會在這裡看到 [概觀]，以以及所有 VM 的 [虛擬機器] 狀態與其安全性狀態，還有由資訊安全中心監視之 Web 和背景工作角色的 [雲端服務] 清單。</span><span class="sxs-lookup"><span data-stu-id="55585-253">You’ll see here an **Overview,** along with the **Virtual machines** listing of all VMs and their security states, and the **Cloud services** list of web and worker roles monitored by Security Center.</span></span>

2. <span data-ttu-id="55585-254">在 [概觀] 索引標籤中，第二個建議可檢視更多資訊。</span><span class="sxs-lookup"><span data-stu-id="55585-254">On the **Overview** tab, second a recommendation to view more information.</span></span>

3. <span data-ttu-id="55585-255">在 [虛擬機器] 索引標籤中選取 VM，以檢視其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="55585-255">On the **Virtual machines** tab, select a VM to view additional details.</span></span>

<span data-ttu-id="55585-256">在 Azure 資訊安全中心啟用資料收集後，Microsoft Monitoring Agent 會自動佈建於已部署的所有現有和新的虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="55585-256">When data collection is enabled in Azure Security Center, the Microsoft Monitoring Agent is automatically provisioned on all existing and any new supported virtual machines that are deployed.</span></span> <span data-ttu-id="55585-257">從這個代理程式收集的資料會儲存在與您的訂用帳戶相關聯的現有 [Log Analytics](https://azure.microsoft.com/services/log-analytics/) 工作區或新的工作區中。</span><span class="sxs-lookup"><span data-stu-id="55585-257">Data collected from this agent is stored in either an existing [Log Analytics](https://azure.microsoft.com/services/log-analytics/) workspace associated with your subscription or a new workspace.</span></span>

<span data-ttu-id="55585-258">資訊安全中心所提供的[威脅情報報告](https://docs.microsoft.com/azure/security-center/security-center-threat-report)。</span><span class="sxs-lookup"><span data-stu-id="55585-258">[Threat Intelligence Reports](https://docs.microsoft.com/azure/security-center/security-center-threat-report) are provided by Security Center.</span></span> <span data-ttu-id="55585-259">這些報告會提供實用資訊給您，協助分辨攻擊者的身分識別、目標、目前和過去攻擊活動，以及所使用的策略、工具和程序。</span><span class="sxs-lookup"><span data-stu-id="55585-259">These give you useful information to help discern the attacker’s identity, objectives, current and historical attack campaigns, and tactics, tools and procedures used.</span></span> <span data-ttu-id="55585-260">還包含緩和與修復資訊。</span><span class="sxs-lookup"><span data-stu-id="55585-260">Mitigation and remediation information is also included.</span></span>

<span data-ttu-id="55585-261">這些威脅報告的主要目的在於協助您有效地回應立即的威脅，並協助您採取後續措施以緩和問題。</span><span class="sxs-lookup"><span data-stu-id="55585-261">The primary purpose of these threat reports is to help you to respond effectively to the immediate threat and help take measures afterward to mitigate the issue.</span></span> <span data-ttu-id="55585-262">當您為了報告和稽核目的而記載事件回應時，報告中的資訊也很實用。</span><span class="sxs-lookup"><span data-stu-id="55585-262">The information in the reports can also be useful when you document your incident response for reporting and auditing purposes.</span></span>

<span data-ttu-id="55585-263">威脅情報報告會以 .PDF 格式呈現，對於 Azure 資訊安全中心的每個安全性警示而言，其可透過 [已執行的可疑處理序] 刀鋒視窗的 [報告] 欄位中的連結存取。</span><span class="sxs-lookup"><span data-stu-id="55585-263">The Threat Intelligence Reports are presented in .PDF format, accessed via a link in the **Reports** field of the **Suspicious process executed** blade for each security alert in Azure Security Center.</span></span>

<span data-ttu-id="55585-264">如需如何檢視和使用威脅情報報告的詳細資訊，請參閱 [Azure 資訊安全中心威脅情報報告](https://docs.microsoft.com/azure/security-center/security-center-threat-report)。</span><span class="sxs-lookup"><span data-stu-id="55585-264">For more information on how to view and use the Threat Intelligence Report, see [Azure Security Center Threat Intelligence Report.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span></span>

## <a name="next-steps"></a><span data-ttu-id="55585-265">後續步驟：</span><span class="sxs-lookup"><span data-stu-id="55585-265">Next Steps:</span></span>

[<span data-ttu-id="55585-266">開始使用 Azure Active Directory 報告 API</span><span class="sxs-lookup"><span data-stu-id="55585-266">Getting Started with the Azure Active Directory reporting API</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started-azure-portal)

[<span data-ttu-id="55585-267">什麼是 Log Analytics？</span><span class="sxs-lookup"><span data-stu-id="55585-267">What is Log Analytics?</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)

[<span data-ttu-id="55585-268">Microsoft Azure 中的監視概觀</span><span class="sxs-lookup"><span data-stu-id="55585-268">Overview of Monitoring in Microsoft Azure</span></span>](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

[<span data-ttu-id="55585-269">Azure 活動記錄簡介 (影片)</span><span class="sxs-lookup"><span data-stu-id="55585-269">Introduction to the Azure Activity Log (video)</span></span>](https://azure.microsoft.com/resources/videos/intro-activity-log/)
