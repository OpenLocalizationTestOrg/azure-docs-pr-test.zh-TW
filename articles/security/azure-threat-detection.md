---
title: "Azure 進階威脅偵測 | Microsoft Docs"
description: "了解 Identity Protection 及其功能。"
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: TomSh
ms.openlocfilehash: 7db677614c23a3447e3e40ae867711a754b06d0d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-advanced-threat-detection"></a><span data-ttu-id="0e92a-103">Azure 進階威脅偵測</span><span class="sxs-lookup"><span data-stu-id="0e92a-103">Azure Advanced Threat Detection</span></span>
## <a name="introduction"></a><span data-ttu-id="0e92a-104">簡介</span><span class="sxs-lookup"><span data-stu-id="0e92a-104">Introduction</span></span>

### <a name="overview"></a><span data-ttu-id="0e92a-105">概觀</span><span class="sxs-lookup"><span data-stu-id="0e92a-105">Overview</span></span>

<span data-ttu-id="0e92a-106">Microsoft 開發了一系列的技術白皮書、安全性概觀、最佳作法及檢查清單，來協助 Azure 客戶了解可在 Azure 平台上和周圍取得的各種安全性相關功能。</span><span class="sxs-lookup"><span data-stu-id="0e92a-106">Microsoft has developed a series of White Papers, Security Overviews, Best Practices, and Checklists to assist Azure customers about the various security-related capabilities available in and surrounding the Azure Platform.</span></span> <span data-ttu-id="0e92a-107">主題範圍兼具廣度與深度，並會定期更新。</span><span class="sxs-lookup"><span data-stu-id="0e92a-107">The topics range in terms of breadth and depth and are updated periodically.</span></span> <span data-ttu-id="0e92a-108">本文件是該系列的一部分，以下的＜摘要＞一節將會摘要說明。</span><span class="sxs-lookup"><span data-stu-id="0e92a-108">This document is part of that series as summarized in the following abstract section.</span></span>

### <a name="azure-platform"></a><span data-ttu-id="0e92a-109">Azure 平台</span><span class="sxs-lookup"><span data-stu-id="0e92a-109">Azure Platform</span></span>

<span data-ttu-id="0e92a-110">Azure 是一個公用雲端服務平台，支援最廣泛的作業系統、程式設計語言、架構、工具、資料庫及裝置等選擇。</span><span class="sxs-lookup"><span data-stu-id="0e92a-110">Azure is a public cloud service platform that supports the broadest selection of operating systems, programming languages, frameworks, tools, databases, and devices.</span></span>
<span data-ttu-id="0e92a-111">它支援下列程式設計語言：</span><span class="sxs-lookup"><span data-stu-id="0e92a-111">It supports the following programming languages:</span></span>
-   <span data-ttu-id="0e92a-112">透過 Docker 整合執行 Linux 容器。</span><span class="sxs-lookup"><span data-stu-id="0e92a-112">Run Linux containers with Docker integration.</span></span>
-   <span data-ttu-id="0e92a-113">使用 JavaScript、Python、.NET、PHP、Java 和 Node.js 建置應用程式。</span><span class="sxs-lookup"><span data-stu-id="0e92a-113">Build apps with JavaScript, Python, .NET, PHP, Java, and Node.js</span></span>
-   <span data-ttu-id="0e92a-114">建置 iOS、Android 和 Windows 裝置的後端。</span><span class="sxs-lookup"><span data-stu-id="0e92a-114">Build back-ends for iOS, Android, and Windows devices.</span></span>

<span data-ttu-id="0e92a-115">Azure 公用雲端服務支援數百萬名開發人員和 IT 專家早已仰賴和信任的相同技術。</span><span class="sxs-lookup"><span data-stu-id="0e92a-115">Azure public cloud services support the same technologies millions of developers and IT professionals already rely on and trust.</span></span>

<span data-ttu-id="0e92a-116">當您透過某個組織移轉至公用雲端時，該組織會負責保護您的資料，並提供系統周圍的安全性和控管。</span><span class="sxs-lookup"><span data-stu-id="0e92a-116">When you are migrating to a public cloud with an organization, that organization is responsible to protect your data and provide security and governance around the system.</span></span>

<span data-ttu-id="0e92a-117">Azure 的基礎結構設計涵蓋設備與應用程式，可同時裝載數以百萬計的客戶，並提供可靠的基礎供企業符合其安全性需求。</span><span class="sxs-lookup"><span data-stu-id="0e92a-117">Azure’s infrastructure is designed from the facility to applications for hosting millions of customers simultaneously, and it provides a trustworthy foundation upon which businesses can meet their security needs.</span></span> <span data-ttu-id="0e92a-118">Azure 提供各種選項來設定和自訂安全性，以符合您應用程式部署的需求。</span><span class="sxs-lookup"><span data-stu-id="0e92a-118">Azure provides a wide array of options to configure and customize security to meet the requirements of your app deployments.</span></span> <span data-ttu-id="0e92a-119">本文件可協助您符合這些需求。</span><span class="sxs-lookup"><span data-stu-id="0e92a-119">This document helps you meet these requirements.</span></span>

### <a name="abstract"></a><span data-ttu-id="0e92a-120">摘要</span><span class="sxs-lookup"><span data-stu-id="0e92a-120">Abstract</span></span>

<span data-ttu-id="0e92a-121">Microsoft Azure 透過 Azure Active Directory、Azure Operations Management Suite (OMS) 及 Azure 資訊安全中心等服務，來提供內建的進階威脅偵測功能。</span><span class="sxs-lookup"><span data-stu-id="0e92a-121">Microsoft Azure offers built in advanced threat detection functionality through services like Azure Active Directory, Azure Operations Management Suite (OMS), and Azure Security Center.</span></span> <span data-ttu-id="0e92a-122">這個安全性服務和功能集合提供簡單且快速的方式，來了解您 Azure 部署內的一舉一動。</span><span class="sxs-lookup"><span data-stu-id="0e92a-122">This collection of security services and capabilities provides a simple and fast way to understand what is happening within your Azure deployments.</span></span>

<span data-ttu-id="0e92a-123">本技術白皮書將引導您針對威脅弱點診斷使用「Microsoft Azure 方法」，並針對以伺服器和其他 Azure 資源為目標的惡意活動，分析相關的風險。</span><span class="sxs-lookup"><span data-stu-id="0e92a-123">This white paper will guide you the “Microsoft Azure approaches” towards threat vulnerability diagnostic and analysing the risk associated with the malicious activities targeted against servers and other Azure resources.</span></span> <span data-ttu-id="0e92a-124">這可協助您利用 Azure 平台最佳化的解決方案和客戶面向的安全性服務和技術，來識別身分識別和弱點管理的方法。</span><span class="sxs-lookup"><span data-stu-id="0e92a-124">This helps you to identify the methods of identification and vulnerability management with optimized solutions by the Azure platform and customer-facing security services and technologies.</span></span>

<span data-ttu-id="0e92a-125">本技術白皮書著重於 Azure 平台和客戶面向之控制的技術，不會嘗試處理 SLA、計價模式和 DevOps 作法考量。</span><span class="sxs-lookup"><span data-stu-id="0e92a-125">This white paper focuses on the technology of Azure platform and customer-facing controls, and does not attempt to address SLAs, pricing models, and DevOps practice considerations.</span></span>

## <a name="azure-active-directory-identity-protection"></a><span data-ttu-id="0e92a-126">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="0e92a-126">Azure Active Directory Identity Protection</span></span>

![Azure Active Directory Identity Protection](./media/azure-threat-detection/azure-threat-detection-fig1.png)


<span data-ttu-id="0e92a-128">[Azure Active Directory Identity Protection](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection) 是 [Azure AD Premium P2](https://docs.microsoft.com/azure/active-directory/active-directory-editions) Edition 的一項功能，可提供會影響組織身分識別之風險事件和潛在弱點的概觀。</span><span class="sxs-lookup"><span data-stu-id="0e92a-128">[Azure Active Directory Identity Protection](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection) is a feature of the [Azure AD Premium P2](https://docs.microsoft.com/azure/active-directory/active-directory-editions) edition that provides you an overview of the risk events and potential vulnerabilities affecting your organization’s identities.</span></span> <span data-ttu-id="0e92a-129">十多年來，Microsoft 一直保護雲端架構身分識別的安全，並透過 Azure AD Identity Protection 持續為企業客戶提供相同的保護系統。</span><span class="sxs-lookup"><span data-stu-id="0e92a-129">Microsoft has been securing cloud-based identities for over a decade, and with Azure AD Identity Protection, Microsoft is making these same protection systems available to enterprise customers.</span></span> <span data-ttu-id="0e92a-130">Identity Protection 使用現有 Azure AD 的異常偵測功能 (可透過 [Azure AD 的異常活動報告](https://docs.microsoft.com/azure/active-directory/active-directory-view-access-usage-reports#anomalous-activity-reports)取得)，並引進可即時偵測異常的新風險事件類型。</span><span class="sxs-lookup"><span data-stu-id="0e92a-130">Identity Protection uses existing Azure AD’s anomaly detection capabilities available through [Azure AD’s Anomalous Activity Reports](https://docs.microsoft.com/azure/active-directory/active-directory-view-access-usage-reports#anomalous-activity-reports), and introduces new risk event types that can detect real time anomalies.</span></span>

<span data-ttu-id="0e92a-131">Identity Protection 會使用調適性機器學習服務演算法和啟發學習法，來偵測異常以及可能表示身分識別已遭入侵的風險事件。</span><span class="sxs-lookup"><span data-stu-id="0e92a-131">Identity Protection uses adaptive machine learning algorithms and heuristics to detect anomalies and risk events that may indicate that an identity has been compromised.</span></span> <span data-ttu-id="0e92a-132">Identity Protection 會使用此資料來產生報告和警示，讓您能夠調查這些風險事件並採取適當的補救動作或緩和措施。</span><span class="sxs-lookup"><span data-stu-id="0e92a-132">Using this data, Identity Protection generates reports and alerts that enable you to investigate these risk events and take appropriate remediation or mitigation action.</span></span>

<span data-ttu-id="0e92a-133">但是，Azure Active Directory Identity Protection 不只是監視和報告工具而已。</span><span class="sxs-lookup"><span data-stu-id="0e92a-133">But Azure Active Directory Identity Protection is more than a monitoring and reporting tool.</span></span> <span data-ttu-id="0e92a-134">Identity Protection 會根據風險事件，計算每位使用者的使用者風險層級，讓您設定以風險為基礎的原則來自動保護您組織的身分識別。</span><span class="sxs-lookup"><span data-stu-id="0e92a-134">Based on risk events, Identity Protection calculates a user risk level for each user, enabling you to configure risk-based policies to automatically protect the identities of your organization.</span></span>

<span data-ttu-id="0e92a-135">除了 Azure Active Directory 與 [EMS](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) 所提供的其他[條件式存取控制](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access)以外，這些以風險為根據的原則可以自動封鎖或提供調適性補救動作，包括重設密碼，以及強制執行 Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="0e92a-135">These risk-based policies, in addition to other [conditional access controls](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) provided by Azure Active Directory and [EMS](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access), can automatically block or offer adaptive remediation actions that include password resets and multi-factor authentication enforcement.</span></span>

### <a name="identity-protections-capabilities"></a><span data-ttu-id="0e92a-136">Identity Protection 的功能</span><span class="sxs-lookup"><span data-stu-id="0e92a-136">Identity Protection's capabilities</span></span>

<span data-ttu-id="0e92a-137">Azure Active Directory Identity Protection 不只是監視和報告工具而已。</span><span class="sxs-lookup"><span data-stu-id="0e92a-137">Azure Active Directory Identity Protection is more than a monitoring and reporting tool.</span></span> <span data-ttu-id="0e92a-138">若要保護您組織的身分識別，您可以設定以風險為基礎的原則，當達到指定風險層級時自動回應偵測到的問題。</span><span class="sxs-lookup"><span data-stu-id="0e92a-138">To protect your organization's identities, you can configure risk-based policies that automatically respond to detected issues when a specified risk level has been reached.</span></span> <span data-ttu-id="0e92a-139">除了 Azure Active Directory 與 EMS 所提供的其他條件式存取控制以外，這些的原則可以自動封鎖或起始調適性補救動作，包括重設密碼以及強制 Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="0e92a-139">These policies, in addition to other conditional access controls provided by Azure Active Directory and EMS, can either automatically block or initiate adaptive remediation actions including password resets and multi-factor authentication enforcement.</span></span>

<span data-ttu-id="0e92a-140">Azure Identity Protection 可用以協助保護您的帳戶和身分識別的一些方法範例包括：</span><span class="sxs-lookup"><span data-stu-id="0e92a-140">Examples of some of the ways that Azure Identity Protection can help secure your accounts and identities include:</span></span>

[<span data-ttu-id="0e92a-141">偵測風險事件和有風險的帳戶：</span><span class="sxs-lookup"><span data-stu-id="0e92a-141">Detecting risk events and risky accounts:</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#detection)
-   <span data-ttu-id="0e92a-142">使用機器學習服務和啟發式規則偵測六種風險事件類型</span><span class="sxs-lookup"><span data-stu-id="0e92a-142">Detecting six risk event types using machine learning and heuristic rules</span></span>
-   <span data-ttu-id="0e92a-143">計算使用者風險層級</span><span class="sxs-lookup"><span data-stu-id="0e92a-143">Calculating user risk levels</span></span>
-   <span data-ttu-id="0e92a-144">提供自訂建議，藉由反白顯示弱點來改善整體安全性狀態</span><span class="sxs-lookup"><span data-stu-id="0e92a-144">Providing custom recommendations to improve overall security posture by highlighting vulnerabilities</span></span>

[<span data-ttu-id="0e92a-145">調查風險事件：</span><span class="sxs-lookup"><span data-stu-id="0e92a-145">Investigating risk events:</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#investigation)
-   <span data-ttu-id="0e92a-146">傳送風險事件的通知</span><span class="sxs-lookup"><span data-stu-id="0e92a-146">Sending notifications for risk events</span></span>
-   <span data-ttu-id="0e92a-147">使用相關和內容資訊來調查風險事件</span><span class="sxs-lookup"><span data-stu-id="0e92a-147">Investigating risk events using relevant and contextual information</span></span>
-   <span data-ttu-id="0e92a-148">提供基本工作流程來追蹤調查</span><span class="sxs-lookup"><span data-stu-id="0e92a-148">Providing basic workflows to track investigations</span></span>
-   <span data-ttu-id="0e92a-149">讓您輕鬆存取補救動作，例如重設密碼</span><span class="sxs-lookup"><span data-stu-id="0e92a-149">Providing easy access to remediation actions such as password reset</span></span>

[<span data-ttu-id="0e92a-150">以風險為基礎的條件式存取原則：</span><span class="sxs-lookup"><span data-stu-id="0e92a-150">Risk-based conditional access policies:</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#risky-sign-ins)
-   <span data-ttu-id="0e92a-151">此原則會藉由封鎖登入或要求 Multi-Factor Authentication 挑戰來緩和有風險的登入。</span><span class="sxs-lookup"><span data-stu-id="0e92a-151">Policy to mitigate risky sign-ins by blocking sign-ins or requiring multi-factor authentication challenges.</span></span>
-   <span data-ttu-id="0e92a-152">此原則會封鎖或保護有風險的使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="0e92a-152">Policy to block or secure risky user accounts</span></span>
-   <span data-ttu-id="0e92a-153">此原則會要求使用者註冊以便進行 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="0e92a-153">Policy to require users to register for multi-factor authentication</span></span>

### <a name="azure-ad-privileged-identity-management-pim"></a><span data-ttu-id="0e92a-154">Azure AD Privileged Identity Management (PIM)</span><span class="sxs-lookup"><span data-stu-id="0e92a-154">Azure AD Privileged Identity Management (PIM)</span></span>

<span data-ttu-id="0e92a-155">利用 [Azure Active Directory (AD) Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure)，</span><span class="sxs-lookup"><span data-stu-id="0e92a-155">With [Azure Active Directory (AD) Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure),</span></span>

![Azure AD 特殊權限身分識別管理](./media/azure-threat-detection/azure-threat-detection-fig2.png)

<span data-ttu-id="0e92a-157">您可以管理、控制及監視組織內的存取。</span><span class="sxs-lookup"><span data-stu-id="0e92a-157">you can manage, control, and monitor access within your organization.</span></span> <span data-ttu-id="0e92a-158">這包括存取 Azure AD 中的資源和其他 Microsoft 線上服務，例如 Office 365 或 Microsoft Intune。</span><span class="sxs-lookup"><span data-stu-id="0e92a-158">This includes access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="0e92a-159">Azure AD Privileged Identity Management 可協助您：</span><span class="sxs-lookup"><span data-stu-id="0e92a-159">Azure AD Privileged Identity Management helps you:</span></span>

-   <span data-ttu-id="0e92a-160">取得有關 Azure AD 系統管理員，以及對 Office 365 和 Intune 等 Microsoft Online Services 之 "just-in-time" 系統管理存取權限的警示和報告</span><span class="sxs-lookup"><span data-stu-id="0e92a-160">Get an alert and report on Azure AD administrators and "just in time" administrative access to Microsoft Online Services like Office 365 and Intune</span></span>

-   <span data-ttu-id="0e92a-161">取得有關系統管理員存取記錄與系統管理員指派變更的報告</span><span class="sxs-lookup"><span data-stu-id="0e92a-161">Get reports about administrator access history and changes in administrator assignments</span></span>

-   <span data-ttu-id="0e92a-162">取得有關特殊權限角色存取的警示</span><span class="sxs-lookup"><span data-stu-id="0e92a-162">Get alerts about access to a privileged role</span></span>

## <a name="microsoft-operations-management-suite-oms"></a><span data-ttu-id="0e92a-163">Microsoft Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="0e92a-163">Microsoft Operations Management Suite (OMS)</span></span>

<span data-ttu-id="0e92a-164">[Microsoft Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) 是 Microsoft 的雲端型 IT 管理解決方案，可協助您管理並保護內部部署和雲端基礎結構。</span><span class="sxs-lookup"><span data-stu-id="0e92a-164">[Microsoft Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="0e92a-165">因為 OMS 實作為雲端型服務，所以您對基礎結構服務進行最小的投資就可以快速啟動並執行它。</span><span class="sxs-lookup"><span data-stu-id="0e92a-165">Since OMS is implemented as a cloud-based service, you can have it up and running quickly with minimal investment in infrastructure services.</span></span> <span data-ttu-id="0e92a-166">新的安全性功能會自動提供，以節省持續維護和升級成本。</span><span class="sxs-lookup"><span data-stu-id="0e92a-166">New security features are delivered automatically, saving your ongoing maintenance and upgrade costs.</span></span>

<span data-ttu-id="0e92a-167">除了自行提供重要服務之外，OMS 還可以整合 System Center 元件 (例如 [System Center Operations Manager](https://blogs.technet.microsoft.com/cbernier/2013/10/23/monitoring-windows-azure-with-system-center-operations-manager-2012-get-me-started/))，以將現有的安全性管理投資擴充到雲端。</span><span class="sxs-lookup"><span data-stu-id="0e92a-167">In addition to providing valuable services on its own, OMS can integrate with System Center components such as [System Center Operations Manager](https://blogs.technet.microsoft.com/cbernier/2013/10/23/monitoring-windows-azure-with-system-center-operations-manager-2012-get-me-started/) to extend your existing security management investments into the cloud.</span></span> <span data-ttu-id="0e92a-168">System Center 和 OMS 可以搭配運作，來提供完整的混合式管理經驗。</span><span class="sxs-lookup"><span data-stu-id="0e92a-168">System Center and OMS can work together to provide a full hybrid management experience.</span></span>

### <a name="holistic-security-and-compliance-posture"></a><span data-ttu-id="0e92a-169">整體安全性與合規性狀態</span><span class="sxs-lookup"><span data-stu-id="0e92a-169">Holistic Security and Compliance Posture</span></span>

<span data-ttu-id="0e92a-170">[OMS 安全性和稽核儀表板](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started)針對值得您注意的問題，使用內建的搜尋查詢，為您組織的 IT 安全性狀態提供全面檢視。</span><span class="sxs-lookup"><span data-stu-id="0e92a-170">The [OMS Security and Audit dashboard](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) provides a comprehensive view into your organization’s IT security posture with built-in search queries for notable issues that require your attention.</span></span> <span data-ttu-id="0e92a-171">[安全性和稽核] 儀表板是 OMS 中所有安全性相關項目的主畫面。</span><span class="sxs-lookup"><span data-stu-id="0e92a-171">The Security and Audit dashboard is the home screen for everything related to security in OMS.</span></span> <span data-ttu-id="0e92a-172">它可讓您深入了解您的電腦的安全性狀態。</span><span class="sxs-lookup"><span data-stu-id="0e92a-172">It provides high-level insight into the security state of your computers.</span></span> <span data-ttu-id="0e92a-173">它還能夠檢視過去 24 小時、7 天或任何其他自訂時間範圍內的所有事件。</span><span class="sxs-lookup"><span data-stu-id="0e92a-173">It also includes the ability to view all events from the past 24 hours, 7 days, or any other custom time frame.</span></span>

<span data-ttu-id="0e92a-174">OMS 儀表板可協助您快速且輕鬆地了解任何環境的整體安全性狀態，全部都在 IT 作業的內容中，包括：軟體更新評估、反惡意程式碼評估和設定基準。</span><span class="sxs-lookup"><span data-stu-id="0e92a-174">OMS dashboards help you quickly and easily understand the overall security posture of any environment, all within the context of IT Operations, including: software update assessment, antimalware assessment, and configuration baselines.</span></span> <span data-ttu-id="0e92a-175">此外，可立即存取安全性記錄資料，以簡化安全性與合規性稽核程序。</span><span class="sxs-lookup"><span data-stu-id="0e92a-175">Furthermore, security log data is readily accessible to streamline the security and compliance audit processes.</span></span>

<span data-ttu-id="0e92a-176">OMS 安全性和稽核儀表板分為四個主要類別︰</span><span class="sxs-lookup"><span data-stu-id="0e92a-176">The OMS Security and Audit dashboard is organized in four major categories:</span></span>

![OMS 安全性和稽核儀表板](./media/azure-threat-detection/azure-threat-detection-fig3.jpg)

-   <span data-ttu-id="0e92a-178">**安全性網域**︰在此區域中，您將能夠進一步探索一段時間的安全性記錄、存取惡意程式碼評估、更新評估、網路安全性、身分識別和存取資訊、具有安全性事件的電腦，以及快速存取 Azure 資訊安全中心儀表板。</span><span class="sxs-lookup"><span data-stu-id="0e92a-178">**Security Domains:** in this area, you will be able to further explore security records over time, access malware assessment, update assessment, network security, identity and access information, computers with security events and quickly have access to Azure Security Center dashboard.</span></span>

-   <span data-ttu-id="0e92a-179">**值得注意的問題**︰此選項可讓您快速識別待處理的問題數目和這些問題的嚴重性。</span><span class="sxs-lookup"><span data-stu-id="0e92a-179">**Notable Issues:** this option allows you to quickly identify the number of active issues and the severity of these issues.</span></span>

-   <span data-ttu-id="0e92a-180">**偵測 (預覽)**︰可讓您立即將資源的安全性警示視覺化，進而識別攻擊模式。</span><span class="sxs-lookup"><span data-stu-id="0e92a-180">**Detections (Preview):** enables you to identify attack patterns by visualizing security alerts as they take place against your resources.</span></span>

-   <span data-ttu-id="0e92a-181">**威脅情報**：可讓您藉由下列方式來識別攻擊模式：視覺化呈現具有惡意輸出 IP 流量的伺服器總數、惡意威脅類型，以及顯示這些 IP 出處的地圖。</span><span class="sxs-lookup"><span data-stu-id="0e92a-181">**Threat Intelligence:** enables you to identify attack patterns by visualizing the total number of servers with outbound malicious IP traffic, the malicious threat type, and a map that shows where these IPs are coming from.</span></span>

-   <span data-ttu-id="0e92a-182">**常見安全性查詢**︰此選項提供最常見的安全性查詢清單，可用來監視您的環境。</span><span class="sxs-lookup"><span data-stu-id="0e92a-182">**Common security queries:** this option provides you a list of the most common security queries that you can use to monitor your environment.</span></span> <span data-ttu-id="0e92a-183">當您按一下上述其中一個查詢時，[搜尋] 刀鋒視窗即會開啟，其中包含該查詢的結果。</span><span class="sxs-lookup"><span data-stu-id="0e92a-183">When you click in one of those queries, it opens the Search blade with the results for that query.</span></span>

### <a name="insight-and-analytics"></a><span data-ttu-id="0e92a-184">深入解析與分析</span><span class="sxs-lookup"><span data-stu-id="0e92a-184">Insight and Analytics</span></span>
<span data-ttu-id="0e92a-185">[Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) 的中心是裝載在 Azure 雲端的 OMS 存放庫。</span><span class="sxs-lookup"><span data-stu-id="0e92a-185">At the center of [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) is the OMS repository, which is hosted in the Azure cloud.</span></span>

![深入解析與分析](./media/azure-threat-detection/azure-threat-detection-fig4.png)

<span data-ttu-id="0e92a-187">資料會藉由設定資料來源以及將方案新增至訂用帳戶中，而從連接的來源收集到存放庫。</span><span class="sxs-lookup"><span data-stu-id="0e92a-187">Data is collected into the repository from connected sources by configuring data sources and adding solutions to your subscription.</span></span>

![訂用帳戶](./media/azure-threat-detection/azure-threat-detection-fig5.png)

<span data-ttu-id="0e92a-189">資料來源和方案都會建立不同的記錄類型，它們具有自己的屬性集，但仍可以一起分析，以便查詢存放庫。</span><span class="sxs-lookup"><span data-stu-id="0e92a-189">Data sources and solutions will each create different record types that have their own set of properties but may still be analyzed together in queries to the repository.</span></span> <span data-ttu-id="0e92a-190">這可讓您使用相同的工具和方法，來處理由不同來源收集的不同類型的資料。</span><span class="sxs-lookup"><span data-stu-id="0e92a-190">This allows you to use the same tools and methods to work with different kinds of data collected by different sources.</span></span>


<span data-ttu-id="0e92a-191">與 Log Analytics 的大部分互動都會透過 OMS 入口網站，它可以在任何瀏覽器中執行，並讓您存取組態設定和多項工具來分析及處理所收集的資料。</span><span class="sxs-lookup"><span data-stu-id="0e92a-191">Most of your interaction with Log Analytics is through the OMS portal, which runs in any browser and provides you with access to configuration settings and multiple tools to analyze and act on collected data.</span></span> <span data-ttu-id="0e92a-192">從入口網站，您可以使用[記錄搜尋](https://docs.microsoft.com/azure/log-analytics/log-analytics-log-searches)來建構查詢以分析所收集的資料、您可以透過最有價值之搜尋的圖形檢視自訂的[儀表板](https://docs.microsoft.com/azure/log-analytics/log-analytics-dashboards)，以及提供額外功能和分析工具的[解決方案](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions)。</span><span class="sxs-lookup"><span data-stu-id="0e92a-192">From the portal, you can use [log searches](https://docs.microsoft.com/azure/log-analytics/log-analytics-log-searches) where you construct queries to analyze collected data, [dashboards](https://docs.microsoft.com/azure/log-analytics/log-analytics-dashboards), which you can customize with graphical views of your most valuable searches, and [solutions](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions), which provide additional functionality and analysis tools.</span></span>

![分析工具](./media/azure-threat-detection/azure-threat-detection-fig6.png)

<span data-ttu-id="0e92a-194">方案會將功能加入 Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="0e92a-194">Solutions add functionality to Log Analytics.</span></span> <span data-ttu-id="0e92a-195">它們主要是在雲端執行，並提供 OMS 儲存機制中所收集資料的分析。</span><span class="sxs-lookup"><span data-stu-id="0e92a-195">They primarily run in the cloud and provide analysis of data collected in the OMS repository.</span></span> <span data-ttu-id="0e92a-196">它們也可以定義要收集的新記錄類型，可以使用記錄搜尋進行分析，或是藉由 OMS 儀表板方案所提供的其他使用者介面進行分析。</span><span class="sxs-lookup"><span data-stu-id="0e92a-196">They may also define new record types to be collected that can be analyzed with Log Searches or by additional user interface provided by the solution in the OMS dashboard.</span></span>
<span data-ttu-id="0e92a-197">安全性和稽核是這類解決方案的範例。</span><span class="sxs-lookup"><span data-stu-id="0e92a-197">The Security and Audit is an example of these types of solutions.</span></span>



### <a name="automation--control-alert-on-security-configuration-drifts"></a><span data-ttu-id="0e92a-198">自動化與控制︰有關安全性設定漂移的警示</span><span class="sxs-lookup"><span data-stu-id="0e92a-198">Automation & Control: Alert on security configuration drifts</span></span>

<span data-ttu-id="0e92a-199">Azure 自動化會使用根據 PowerShell 在 Azure 雲端中執行的 Runbook，來自動化管理程序。</span><span class="sxs-lookup"><span data-stu-id="0e92a-199">Azure Automation automates administrative processes with runbooks that are based on PowerShell and run in the Azure cloud.</span></span> <span data-ttu-id="0e92a-200">Runbook 也可以在本機資料中心的伺服器上執行，以管理本機資源。</span><span class="sxs-lookup"><span data-stu-id="0e92a-200">Runbooks can also be executed on a server in your local data center to manage local resources.</span></span> <span data-ttu-id="0e92a-201">Azure 自動化會使用 PowerShell DSC (Desired State Configuration) 來提供設定管理。</span><span class="sxs-lookup"><span data-stu-id="0e92a-201">Azure Automation provides configuration management with PowerShell DSC (Desired State Configuration).</span></span>

![Azure 自動化](./media/azure-threat-detection/azure-threat-detection-fig7.png)

<span data-ttu-id="0e92a-203">您可以建立和管理裝載於 Azure 的 DSC 資源，並將它們套用到雲端和內部部署系統，來定義和自動強制執行其設定，或者取得有關漂移的報告來協助確保原則內仍保有安全性設定。</span><span class="sxs-lookup"><span data-stu-id="0e92a-203">You can create and manage DSC resources hosted in Azure and apply them to cloud and on-premises systems to define and automatically enforce their configuration or get reports on drift to help insure that security configurations remain within policy.</span></span>

## <a name="azure-security-center"></a><span data-ttu-id="0e92a-204">Azure 資訊安全中心</span><span class="sxs-lookup"><span data-stu-id="0e92a-204">Azure Security Center</span></span>

<span data-ttu-id="0e92a-205">Azure 資訊安全中心可協助保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="0e92a-205">Azure Security Center helps protect your Azure resources.</span></span> <span data-ttu-id="0e92a-206">它提供您 Azure 訂用帳戶之間的整合式安全性監視和原則管理。</span><span class="sxs-lookup"><span data-stu-id="0e92a-206">It provides integrated security monitoring and policy management across your Azure subscriptions.</span></span> <span data-ttu-id="0e92a-207">在服務中，您不只可針對 Azure 訂用帳戶定義原則，也能針對[資源群組](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal)加以定義，如此便能以更細微的方式進行。</span><span class="sxs-lookup"><span data-stu-id="0e92a-207">Within the service, you are able to define polices not only against your Azure subscriptions, but also against [Resource Groups](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal), so you can be more granular.</span></span>

![Azure 資訊安全中心](./media/azure-threat-detection/azure-threat-detection-fig8.png)

<span data-ttu-id="0e92a-209">Microsoft 資訊安全研究人員會持續監視威脅。</span><span class="sxs-lookup"><span data-stu-id="0e92a-209">Microsoft security researchers are constantly on the lookout for threats.</span></span> <span data-ttu-id="0e92a-210">他們可以存取從 Microsoft 在雲端和內部部署中的全域支援取得的一組廣泛遙測。</span><span class="sxs-lookup"><span data-stu-id="0e92a-210">They have access to an expansive set of telemetry gained from Microsoft’s global presence in the cloud and on-premises.</span></span> <span data-ttu-id="0e92a-211">這組包羅萬象的資料集，可讓 Microsoft 探索其內部部署消費性和企業產品及其線上服務的新攻擊模式和趨勢。</span><span class="sxs-lookup"><span data-stu-id="0e92a-211">This wide-reaching and diverse collection of datasets enables Microsoft to discover new attack patterns and trends across its on-premises consumer and enterprise products, as well as its online services.</span></span>

<span data-ttu-id="0e92a-212">因此，資訊安全中心可以在攻擊者發行新的和日益複雜的攻擊時，快速地更新其偵測演算法。</span><span class="sxs-lookup"><span data-stu-id="0e92a-212">Thus, Security Center can rapidly update its detection algorithms as attackers release new and increasingly sophisticated exploits.</span></span> <span data-ttu-id="0e92a-213">這種方法可協助您跟上瞬息萬變的威脅環境。</span><span class="sxs-lookup"><span data-stu-id="0e92a-213">This approach helps you keep pace with a fast-moving threat environment.</span></span>

![資訊安全中心](./media/azure-threat-detection/azure-threat-detection-fig9.jpg)

<span data-ttu-id="0e92a-215">資訊安全中心威脅偵測的運作方式如下：從您的 Azure 資源、網路及已連線的協力廠商解決方案自動收集安全性資訊。</span><span class="sxs-lookup"><span data-stu-id="0e92a-215">Security Center threat detection works by automatically collecting security information from your Azure resources, the network, and connected partner solutions.</span></span>  <span data-ttu-id="0e92a-216">它會分析這項資訊 (來自多個來源的相互關聯資訊) 以識別威脅。</span><span class="sxs-lookup"><span data-stu-id="0e92a-216">It analyzes this information, correlating information from multiple sources, to identify threats.</span></span>
<span data-ttu-id="0e92a-217">資訊安全中心的安全性警示會排定優先順序，並提供如何補救威脅的建議。</span><span class="sxs-lookup"><span data-stu-id="0e92a-217">Security alerts are prioritized in Security Center along with recommendations on how to remediate the threat.</span></span>

<span data-ttu-id="0e92a-218">資訊安全中心會運用進階安全性分析，其遠勝於以簽章為基礎的方法。</span><span class="sxs-lookup"><span data-stu-id="0e92a-218">Security Center employs advanced security analytics, which go far beyond signature-based approaches.</span></span> <span data-ttu-id="0e92a-219">對於巨量資料和[機器學習服務 (英文)](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/) 技術的突破適用於評估整個雲端網狀架構的事件：使用手動方式來偵測無法識別的威脅，以及預測攻擊的演化。</span><span class="sxs-lookup"><span data-stu-id="0e92a-219">Breakthroughs in big data and [machine learning](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/) technologies are used to evaluate events across the entire cloud fabric – detecting threats that would be impossible to identify using manual approaches and predicting the evolution of attacks.</span></span> <span data-ttu-id="0e92a-220">這些安全性分析包括下列各項。</span><span class="sxs-lookup"><span data-stu-id="0e92a-220">These security analytics includes the following.</span></span>

### <a name="threat-intelligence"></a><span data-ttu-id="0e92a-221">威脅情報</span><span class="sxs-lookup"><span data-stu-id="0e92a-221">Threat Intelligence</span></span>

<span data-ttu-id="0e92a-222">Microsoft 有大量全域威脅情報。</span><span class="sxs-lookup"><span data-stu-id="0e92a-222">Microsoft has an immense amount of global threat intelligence.</span></span>
<span data-ttu-id="0e92a-223">遙測會從多個來源流入，例如 Azure、Office 365、Microsoft CRM Online、Microsoft Dynamics AX、outlook.com、MSN.com、Microsoft 數位犯罪防治中心 (DCU) 和 Microsoft 安全性回應中心 (MSRC)。</span><span class="sxs-lookup"><span data-stu-id="0e92a-223">Telemetry flows in from multiple sources, such as Azure, Office 365, Microsoft CRM online, Microsoft Dynamics AX, outlook.com, MSN.com, the Microsoft Digital Crimes Unit (DCU), and Microsoft Security Response Center (MSRC).</span></span>

![威脅情報](./media/azure-threat-detection/azure-threat-detection-fig10.jpg)

<span data-ttu-id="0e92a-225">研究人員也會收到主要雲端服務提供者之間共用的威脅情報資訊，並訂閱來自協力廠商的威脅情報摘要。</span><span class="sxs-lookup"><span data-stu-id="0e92a-225">Researchers also receive threat intelligence information that is shared among major cloud service providers and subscribes to threat intelligence feeds from third parties.</span></span> <span data-ttu-id="0e92a-226">Azure 資訊安全中心可以使用這項資訊來警示您來自已知不良執行者的威脅。</span><span class="sxs-lookup"><span data-stu-id="0e92a-226">Azure Security Center can use this information to alert you to threats from known bad actors.</span></span> <span data-ttu-id="0e92a-227">部分範例包括：</span><span class="sxs-lookup"><span data-stu-id="0e92a-227">Some examples include:</span></span>

-   <span data-ttu-id="0e92a-228">**運用機器學習服務的力量**：Azure 資訊安全中心可以存取關於雲端網路活動的大量資料，可用來偵測目標為您 Azure 部署的潛在威脅。</span><span class="sxs-lookup"><span data-stu-id="0e92a-228">**Harnessing the Power of Machine Learning -** Azure Security Center has access to a vast amount of data about cloud network activity, which can be used to detect threats targeting your Azure deployments.</span></span> <span data-ttu-id="0e92a-229">例如：</span><span class="sxs-lookup"><span data-stu-id="0e92a-229">For example:</span></span>

-   <span data-ttu-id="0e92a-230">**暴力密碼破解偵測**：機器學習服務可用來建立嘗試遠端存取的歷程記錄模式，使其得以偵測到對於 SSH、RDP 和 SQL 連接埠的暴力密碼破解攻擊。</span><span class="sxs-lookup"><span data-stu-id="0e92a-230">**Brute Force Detections -** Machine learning is used to create a historical pattern of remote access attempts, which allows it to detect brute force attacks against SSH, RDP, and SQL ports.</span></span>

-   <span data-ttu-id="0e92a-231">**輸出 DDoS 和 Botnet 偵測**：目標為雲端資源之攻擊的常見目標之一是使用這些資源的計算能力來執行其他攻擊。</span><span class="sxs-lookup"><span data-stu-id="0e92a-231">**Outbound DDoS and Botnet Detection** - A common objective of attacks targeting cloud resources is to use the compute power of these resources to execute other attacks.</span></span>

-   <span data-ttu-id="0e92a-232">**新的行為分析伺服器和 VM**：一旦伺服器或虛擬機器遭到入侵之後，攻擊者就能用各種不同的技術，在該系統上執行惡意程式碼，同時避開偵測、確保持續性，並迴避安全性控制。</span><span class="sxs-lookup"><span data-stu-id="0e92a-232">**New Behavioral Analytics Servers and VMs -** Once a server or virtual machine is compromised, attackers employ a wide variety of techniques to execute malicious code on that system while avoiding detection, ensuring persistence, and obviating security controls.</span></span>

-   <span data-ttu-id="0e92a-233">**Azure SQL Database 威脅偵測**：適用於 Azure SQL Database 的威脅偵測，它會識別異常的資料庫活動，指出發生不尋常且可能有害的嘗試存取或惡意探索資料庫。</span><span class="sxs-lookup"><span data-stu-id="0e92a-233">**Azure SQL Database Threat Detection -** Threat Detection for Azure SQL Database, which identifies anomalous database activities indicating unusual and potentially harmful attempts to access or exploit databases.</span></span>

### <a name="behavioral-analytics"></a><span data-ttu-id="0e92a-234">行為分析</span><span class="sxs-lookup"><span data-stu-id="0e92a-234">Behavioral analytics</span></span>

<span data-ttu-id="0e92a-235">行為分析是一種可分析及比較資料與一組已知模式的技術。</span><span class="sxs-lookup"><span data-stu-id="0e92a-235">Behavioral analytics is a technique that analyzes and compares data to a collection of known patterns.</span></span> <span data-ttu-id="0e92a-236">不過，這些模式並非簡單的簽章。</span><span class="sxs-lookup"><span data-stu-id="0e92a-236">However, these patterns are not simple signatures.</span></span> <span data-ttu-id="0e92a-237">它們會透過已套用至大型資料集的複雜機器學習演算法來決定。</span><span class="sxs-lookup"><span data-stu-id="0e92a-237">They are determined through complex machine learning algorithms that are applied to massive datasets.</span></span>

![行為分析](./media/azure-threat-detection/azure-threat-detection-fig11.jpg)


<span data-ttu-id="0e92a-239">它們也能透過專業分析師仔細分析惡意行為來判定。</span><span class="sxs-lookup"><span data-stu-id="0e92a-239">They are also determined through careful analysis of malicious behaviors by expert analysts.</span></span> <span data-ttu-id="0e92a-240">Azure 資訊安全中心可以使用行為分析，根據虛擬機器記錄、虛擬網路裝置記錄、網狀架構記錄、毀損傾印和其他來源的分析，來識別遭到入侵的資源。</span><span class="sxs-lookup"><span data-stu-id="0e92a-240">Azure Security Center can use behavioral analytics to identify compromised resources based on analysis of virtual machine logs, virtual network device logs, fabric logs, crash dumps, and other sources.</span></span>

<span data-ttu-id="0e92a-241">此外，還與其他訊號相互關聯，以檢查廣泛行銷活動的支援證明。</span><span class="sxs-lookup"><span data-stu-id="0e92a-241">In addition, there is correlation with other signals to check for supporting evidence of a widespread campaign.</span></span> <span data-ttu-id="0e92a-242">此相互關聯有助於識別與已確立危害指標一致的事件。</span><span class="sxs-lookup"><span data-stu-id="0e92a-242">This correlation helps to identify events that are consistent with established indicators of compromise.</span></span>

<span data-ttu-id="0e92a-243">部分範例包括：</span><span class="sxs-lookup"><span data-stu-id="0e92a-243">Some examples include:</span></span>
-   <span data-ttu-id="0e92a-244">**可疑的處理序執行**︰攻擊者不需要偵測，即可運用數種技術來執行惡意軟體。</span><span class="sxs-lookup"><span data-stu-id="0e92a-244">**Suspicious process execution:** Attackers employ several techniques to execute malicious software without detection.</span></span> <span data-ttu-id="0e92a-245">例如，攻擊者可能會讓惡意程式碼具有與合法系統檔案相同的名稱，但會將這些檔案放在替代位置、使用非常類似良性檔案的名稱，或為檔案的真正副檔名加上遮罩。</span><span class="sxs-lookup"><span data-stu-id="0e92a-245">For example, an attacker might give malware the same names as legitimate system files but place these files in an alternate location, use a name that is very like a benign file, or mask the file’s true extension.</span></span> <span data-ttu-id="0e92a-246">資訊安全中心會塑造程序行為的模型，並監視處理序執行以偵測這類的極端值。</span><span class="sxs-lookup"><span data-stu-id="0e92a-246">Security Center models processes behaviors and monitors process executions to detect outliers such as these.</span></span>

-   <span data-ttu-id="0e92a-247">**隱藏的惡意程式碼和弱點攻擊嘗試**︰複雜的惡意程式碼可藉由永遠不要寫入至磁碟或加密磁碟上儲存的軟體元件，來避開傳統的反惡意程式碼產品。</span><span class="sxs-lookup"><span data-stu-id="0e92a-247">**Hidden malware and exploitation attempts:** Sophisticated malware can evade traditional antimalware products by either never writing to disk or encrypting software components stored on disk.</span></span> <span data-ttu-id="0e92a-248">不過，可以使用記憶體分析來偵測這類惡意程式碼，因為惡意程式碼必須在記憶體中留下蹤跡才能運作。</span><span class="sxs-lookup"><span data-stu-id="0e92a-248">However, such malware can be detected using memory analysis, as the malware must leave traces in memory to function.</span></span> <span data-ttu-id="0e92a-249">當軟體損毀時，損毀傾印會在損毀時擷取部分的記憶體。</span><span class="sxs-lookup"><span data-stu-id="0e92a-249">When software crashes, a crash dump captures a portion of memory at the time of the crash.</span></span> <span data-ttu-id="0e92a-250">藉由分析損毀傾印中的記憶體，Azure 資訊安全中心可以偵測到用來惡意探索軟體中的弱點、存取機密資料，以及暗中保存於遭入侵電腦的技術，而不會影響您電腦的效能。</span><span class="sxs-lookup"><span data-stu-id="0e92a-250">By analyzing the memory in the crash dump, Azure Security Center can detect techniques used to exploit vulnerabilities in software, access confidential data, and surreptitiously persist within a compromised machine without impacting the performance of your machine.</span></span>

-   <span data-ttu-id="0e92a-251">**橫向移動和內部偵察**︰為了保存於遭入侵的網路內並找出/獲取重要資料，攻擊者經常會試圖從遭入侵的電腦橫向移到相同網路內的其他電腦。</span><span class="sxs-lookup"><span data-stu-id="0e92a-251">**Lateral movement and internal reconnaissance:** To persist in a compromised network and locate/harvest valuable data, attackers often attempt to move laterally from the compromised machine to others within the same network.</span></span> <span data-ttu-id="0e92a-252">資訊安全中心會監視處理和登入活動，以探索在網路內展開攻擊者據點的嘗試，例如，遠端命令執行、網路探查和帳戶列舉。</span><span class="sxs-lookup"><span data-stu-id="0e92a-252">Security Center monitors process and login activities to discover attempts to expand an attacker’s foothold within the network, such as remote command execution, network probing, and account enumeration.</span></span>

-   <span data-ttu-id="0e92a-253">**惡意 PowerShell 指令碼**︰攻擊者會針對各種目的，使用 PowerShell 在目標虛擬機器上執行惡意程式碼。</span><span class="sxs-lookup"><span data-stu-id="0e92a-253">**Malicious PowerShell Scripts:** PowerShell can be used by attackers to execute malicious code on target virtual machines for a various purposes.</span></span> <span data-ttu-id="0e92a-254">資訊安全中心會檢查 PowerShell 活動，以找到可疑活動的證明。</span><span class="sxs-lookup"><span data-stu-id="0e92a-254">Security Center inspects PowerShell activity for evidence of suspicious activity.</span></span>

-   <span data-ttu-id="0e92a-255">**傳出攻擊**︰攻擊者通常會以雲端資源為目標，目的在於使用這些資源來掛載其他攻擊。</span><span class="sxs-lookup"><span data-stu-id="0e92a-255">**Outgoing attacks:** Attackers often target cloud resources with the goal of using those resources to mount additional attacks.</span></span> <span data-ttu-id="0e92a-256">例如，遭入侵的虛擬機器可用來對其他虛擬機器發動暴力密碼破解攻擊、傳送垃圾郵件，或掃描開啟的連接埠和網際網路上的其他裝置。</span><span class="sxs-lookup"><span data-stu-id="0e92a-256">Compromised virtual machines, for example, might be used to launch brute force attacks against other virtual machines, send SPAM, or scan open ports and other devices on the Internet.</span></span> <span data-ttu-id="0e92a-257">藉由將機器學習服務套用到網路流量，資訊安全中心可以偵測輸出網路通訊何時超出規範。</span><span class="sxs-lookup"><span data-stu-id="0e92a-257">By applying machine learning to network traffic, Security Center can detect when outbound network communications exceed the norm.</span></span> <span data-ttu-id="0e92a-258">如果是垃圾郵件，資訊安全中心也會讓不尋常的電子郵件流量與 Office 365 提供的情報相互關聯，以判斷郵件是否可能有惡意或合法電子郵件行銷活動的結果。</span><span class="sxs-lookup"><span data-stu-id="0e92a-258">When SPAM, Security Center also correlates unusual email traffic with intelligence from Office 365 to determine whether the mail is likely nefarious or the result of a legitimate email campaign.</span></span>

### <a name="anomaly-detection"></a><span data-ttu-id="0e92a-259">異常偵測</span><span class="sxs-lookup"><span data-stu-id="0e92a-259">Anomaly Detection</span></span>

<span data-ttu-id="0e92a-260">Azure 資訊安全中心也會使用異常偵測來識別威脅。</span><span class="sxs-lookup"><span data-stu-id="0e92a-260">Azure Security Center also uses anomaly detection to identify threats.</span></span> <span data-ttu-id="0e92a-261">相較於行為分析 (這取決於衍生自大型資料集的已知模式)，異常偵測更加「個人化」，且著重於您的部署專用的基準。</span><span class="sxs-lookup"><span data-stu-id="0e92a-261">In contrast to behavioral analytics (which depends on known patterns derived from large data sets), anomaly detection is more “personalized” and focuses on baselines that are specific to your deployments.</span></span> <span data-ttu-id="0e92a-262">機器學習服務適用於判斷您部署的正常活動，然後產生規則來定義可能代表安全性事件的極端狀況。</span><span class="sxs-lookup"><span data-stu-id="0e92a-262">Machine learning is applied to determine normal activity for your deployments and then rules are generated to define outlier conditions that could represent a security event.</span></span> <span data-ttu-id="0e92a-263">範例如下：</span><span class="sxs-lookup"><span data-stu-id="0e92a-263">Here’s an example:</span></span>

-   <span data-ttu-id="0e92a-264">**輸入 RDP/SSH 暴力密碼破解攻擊**︰您的部署中可能包含每天都有許多登入的繁忙虛擬機器，以及有少量或任何登入的其他虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0e92a-264">**Inbound RDP/SSH brute force attacks:** Your deployments may have busy virtual machines with many logins each day and other virtual machines that have few or any logins.</span></span> <span data-ttu-id="0e92a-265">Azure 資訊安全中心可以判斷這些虛擬機器的基準登入活動，並使用要定義於正常登入活動周圍的機器學習服務。</span><span class="sxs-lookup"><span data-stu-id="0e92a-265">Azure Security Center can determine baseline login activity for these virtual machines and use machine learning to define around the normal login activities.</span></span> <span data-ttu-id="0e92a-266">如果與針對登入相關特性所定義的基準有任何差異，則可能會產生警示。</span><span class="sxs-lookup"><span data-stu-id="0e92a-266">If there is any discrepancy with the baseline defined for login related characteristics, then an alert may be generated.</span></span> <span data-ttu-id="0e92a-267">同樣地，機器學習服務會判斷何者值得關注。</span><span class="sxs-lookup"><span data-stu-id="0e92a-267">Again, machine learning determines what is significant.</span></span>

### <a name="continuous-threat-intelligence-monitoring"></a><span data-ttu-id="0e92a-268">連續威脅情報監視</span><span class="sxs-lookup"><span data-stu-id="0e92a-268">Continuous Threat Intelligence Monitoring</span></span>

<span data-ttu-id="0e92a-269">Azure 資訊安全中心在世界各地設有資訊安全研究和資料科學小組，負責持續監視威脅態勢中的變化。</span><span class="sxs-lookup"><span data-stu-id="0e92a-269">Azure Security Center operates with security research and data science teams throughout the world that continuously monitor for changes in the threat landscape.</span></span> <span data-ttu-id="0e92a-270">這包括下列計劃︰</span><span class="sxs-lookup"><span data-stu-id="0e92a-270">This includes the following initiatives:</span></span>

-   <span data-ttu-id="0e92a-271">**威脅情報監視**︰威脅情報包含關於現有或新興威脅的機制、指標、影響和可採取動作的建議。</span><span class="sxs-lookup"><span data-stu-id="0e92a-271">**Threat intelligence monitoring:** Threat intelligence includes mechanisms, indicators, implications, and actionable advice about existing or emerging threats.</span></span> <span data-ttu-id="0e92a-272">安全性社群會共用此資訊，而 Microsoft 會持續監視來自內部和外部來源的威脅情報摘要。</span><span class="sxs-lookup"><span data-stu-id="0e92a-272">This information is shared in the security community and Microsoft continuously monitors threat intelligence feeds from internal and external sources.</span></span>

-   <span data-ttu-id="0e92a-273">**訊號共用**︰共用和分析 Microsoft 的資訊安全小組對於各種雲端和內部部署服務、伺服器及用戶端端點裝置組合所提供的深入見解。</span><span class="sxs-lookup"><span data-stu-id="0e92a-273">**Signal sharing:** Insights from security teams across Microsoft’s broad portfolio of cloud and on-premises services, servers, and client endpoint devices are shared and analyzed.</span></span>

-   <span data-ttu-id="0e92a-274">**Microsoft 資訊安全專家**︰持續與擅長特殊資訊安全領域 (例如鑑識與 Web 攻擊偵測) 的 Microsoft 團隊攜手合作。</span><span class="sxs-lookup"><span data-stu-id="0e92a-274">**Microsoft security specialists:** Ongoing engagement with teams across Microsoft that work in specialized security fields, like forensics and web attack detection.</span></span>

-   <span data-ttu-id="0e92a-275">**偵測微調**︰對真正的客戶資料集執行演算法，而資訊安全研究人員會與客戶一起驗證結果。</span><span class="sxs-lookup"><span data-stu-id="0e92a-275">**Detection tuning:** Algorithms are run against real customer data sets and security researchers work with customers to validate the results.</span></span> <span data-ttu-id="0e92a-276">真肯定和誤判可用來縮小機器學習演算法的範圍。</span><span class="sxs-lookup"><span data-stu-id="0e92a-276">True and false positives are used to refine machine learning algorithms.</span></span>

<span data-ttu-id="0e92a-277">結合上述努力終於獲得全新及改善的偵測功能，您因而立即受惠 – 不需採取任何的動作。</span><span class="sxs-lookup"><span data-stu-id="0e92a-277">These combined efforts culminate in new and improved detections, which you can benefit from instantly – there’s no action for you to take.</span></span>

## <a name="advanced-threat-detection-features---other-azure-services"></a><span data-ttu-id="0e92a-278">進階威脅偵測功能：其他 Azure 服務</span><span class="sxs-lookup"><span data-stu-id="0e92a-278">Advanced Threat Detection Features - Other Azure Services</span></span>

### <a name="virtual-machine-microsoft-antimalware"></a><span data-ttu-id="0e92a-279">虛擬機器︰Microsoft Antimalware</span><span class="sxs-lookup"><span data-stu-id="0e92a-279">Virtual Machine: Microsoft Antimalware</span></span>

<span data-ttu-id="0e92a-280">適用於 Azure 的 [Microsoft Antimalware](https://docs.microsoft.com/azure/security/azure-security-antimalware) 是針對應用程式和租用戶環境所提供的單一代理程式解決方案，其設計可於無人為介入的情況下在背景中執行。</span><span class="sxs-lookup"><span data-stu-id="0e92a-280">[Microsoft Antimalware](https://docs.microsoft.com/azure/security/azure-security-antimalware) for Azure is a single-agent solution for applications and tenant environments, designed to run in the background without human intervention.</span></span> <span data-ttu-id="0e92a-281">您可依據應用程式工作負載需求，選擇預設的基本安全性或進階的自訂組態 (包括反惡意程式碼監視) 來部署保護。</span><span class="sxs-lookup"><span data-stu-id="0e92a-281">You can deploy protection based on the needs of your application workloads, with either basic secure-by-default or advanced custom configuration, including antimalware monitoring.</span></span> <span data-ttu-id="0e92a-282">Azure 的反惡意程式碼是適用於 Azure 虛擬機器的安全性選項，而且會自動安裝在所有的 Azure PaaS 虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="0e92a-282">Azure antimalware is a security option for Azure Virtual Machines and is automatically installed on all Azure PaaS virtual machines.</span></span>

<span data-ttu-id="0e92a-283">**要部署的 Azure 功能以及為您的應用程式啟用 Microsoft Antimalware**</span><span class="sxs-lookup"><span data-stu-id="0e92a-283">**Features of Azure to deploy and enable Microsoft Antimalware for your applications**</span></span>

#### <a name="microsoft-antimalware-core-features"></a><span data-ttu-id="0e92a-284">Microsoft Antimalware 核心功能</span><span class="sxs-lookup"><span data-stu-id="0e92a-284">Microsoft Antimalware Core Features</span></span>

-   <span data-ttu-id="0e92a-285">**即時保護**：監視雲端服務和虛擬機器上的活動，以偵測和封鎖惡意程式碼執行。</span><span class="sxs-lookup"><span data-stu-id="0e92a-285">**Real-time protection -** monitors activity in Cloud Services and on Virtual Machines to detect and block malware execution.</span></span>

-   <span data-ttu-id="0e92a-286">**排程掃描**：定期執行目標掃描以偵測惡意程式碼，包括主動執行程式。</span><span class="sxs-lookup"><span data-stu-id="0e92a-286">**Scheduled scanning -** periodically performs targeted scanning to detect malware, including actively running programs.</span></span>

-   <span data-ttu-id="0e92a-287">**惡意程式碼補救**：自動針對偵測到的惡意程式碼採取行動，例如，刪除或隔離惡意檔案，以及清除惡意的登錄項目。</span><span class="sxs-lookup"><span data-stu-id="0e92a-287">**Malware remediation -** automatically takes action on detected malware, such as deleting or quarantining malicious files and cleaning up malicious registry entries.</span></span>

-   <span data-ttu-id="0e92a-288">**簽章更新**：自動安裝最新的保護簽章 (病毒定義)，以確保會依預定頻率維持最新的保護狀態。</span><span class="sxs-lookup"><span data-stu-id="0e92a-288">**Signature updates -** automatically installs the latest protection signatures (virus definitions) to ensure protection is up-to-date on a pre-determined frequency.</span></span>

-   <span data-ttu-id="0e92a-289">**Antimalware Engine 更新**：自動更新 Microsoft Antimalware 引擎。</span><span class="sxs-lookup"><span data-stu-id="0e92a-289">**Antimalware Engine updates -** automatically updates the Microsoft Antimalware engine.</span></span>

-   <span data-ttu-id="0e92a-290">**Antimalware 平台更新**：自動更新 Microsoft Antimalware 平台。</span><span class="sxs-lookup"><span data-stu-id="0e92a-290">**Antimalware Platform updates –** automatically updates the Microsoft Antimalware platform.</span></span>

-   <span data-ttu-id="0e92a-291">**主動保護**：向 Microsoft Azure 報告有關偵測到的威脅和可疑資源的遙測中繼資料，以確保能針對不斷演變的威脅型態做出快速的回應，並透過 Microsoft Active Protection System (MAPS) 啟用即時的同步簽章傳遞。</span><span class="sxs-lookup"><span data-stu-id="0e92a-291">**Active protection -** reports telemetry metadata about detected threats and suspicious resources to Microsoft Azure to ensure rapid response to the evolving threat landscape, and enabling real-time synchronous signature delivery through the Microsoft Active Protection System (MAPS).</span></span>

-   <span data-ttu-id="0e92a-292">**範例報告**：提供範例並向 Microsoftt Antimalware 服務報告，以協助改善服務並啟用疑難排解。</span><span class="sxs-lookup"><span data-stu-id="0e92a-292">**Samples reporting -** provides and reports samples to the Microsoft Antimalware service to help refine the service and enable troubleshooting.</span></span>

-   <span data-ttu-id="0e92a-293">**排除項目**：可讓應用程式和服務管理員設定特定的檔案、處理序及磁碟機，以因應效能及/或其他原因將其從保護和掃描中排除。</span><span class="sxs-lookup"><span data-stu-id="0e92a-293">**Exclusions –** allows application and service administrators to configure certain files, processes, and drives to exclude them from protection and scanning for performance and/or other reasons.</span></span>

-   <span data-ttu-id="0e92a-294">**Antimalware 事件收集**：在作業系統事件記錄中記錄反惡意程式碼服務的健康狀況、可疑的活動及所採取的補救動作，並將這些資料收集至客戶的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0e92a-294">**Antimalware event collection -** records the antimalware service health, suspicious activities, and remediation actions taken in the operating system event log and collects them into the customer’s Azure Storage account.</span></span>

### <a name="azure-sql-database-threat-detection"></a><span data-ttu-id="0e92a-295">Azure SQL Database 威脅偵測</span><span class="sxs-lookup"><span data-stu-id="0e92a-295">Azure SQL Database Threat Detection</span></span>

<span data-ttu-id="0e92a-296">[Azure SQL Database 威脅偵測](https://azure.microsoft.com/blog/azure-sql-database-threat-detection-your-built-in-security-expert/)是內建於 Azure SQL Database 服務的新安全性智慧型功能。</span><span class="sxs-lookup"><span data-stu-id="0e92a-296">[Azure SQL Database Threat Detection](https://azure.microsoft.com/blog/azure-sql-database-threat-detection-your-built-in-security-expert/) is a new security intelligence feature built into the Azure SQL Database service.</span></span> <span data-ttu-id="0e92a-297">Azure SQL Database 威脅偵測可藉由全天候學習、分析及偵測異常資料庫活動，來識別資料庫的潛在威脅。</span><span class="sxs-lookup"><span data-stu-id="0e92a-297">Working around the clock to learn, profile and detect anomalous database activities, Azure SQL Database Threat Detection identifies potential threats to the database.</span></span>

<span data-ttu-id="0e92a-298">資訊安全人員或其他指定的系統管理員可以在發生可疑的資料庫活動時立即取得通知。</span><span class="sxs-lookup"><span data-stu-id="0e92a-298">Security officers or other designated administrators can get an immediate notification about suspicious database activities as they occur.</span></span> <span data-ttu-id="0e92a-299">每個通知都會提供可疑活動的詳細資料，以及建議如何進一步調查並減輕威脅。</span><span class="sxs-lookup"><span data-stu-id="0e92a-299">Each notification provides details of the suspicious activity and recommends how to further investigate and mitigate the threat.</span></span>

<span data-ttu-id="0e92a-300">目前，Azure SQL Database 威脅偵測會偵測潛在的弱點與 SQL 插入式攻擊，以及異常的資料庫存取模式。</span><span class="sxs-lookup"><span data-stu-id="0e92a-300">Currently, Azure SQL Database Threat Detection detects potential vulnerabilities and SQL injection attacks, and anomalous database access patterns.</span></span>

<span data-ttu-id="0e92a-301">收到威脅偵測電子郵件通知之後，使用者可以使用郵件中的深層連結來瀏覽並檢視相關稽核記錄，該連結會開啟稽核檢視器和/或預先設定的稽核 Excel 範本，根據下列各項來顯示發生可疑事件前後時間的相關稽核記錄：</span><span class="sxs-lookup"><span data-stu-id="0e92a-301">Upon receiving threat detection email notification, users are able to navigate and view the relevant audit records using the deep link in the mail that opens an audit viewer and/or preconfigured auditing Excel template that shows the relevant audit records around the time of the suspicious event according to the following:</span></span>
-   <span data-ttu-id="0e92a-302">適用於具有資料庫異常活動之資料庫/伺服器的稽核儲存體</span><span class="sxs-lookup"><span data-stu-id="0e92a-302">Audit storage for the database/server with the anomalous database activities</span></span>

-   <span data-ttu-id="0e92a-303">將事件寫入稽核記錄時所使用的相關稽核儲存體資料表</span><span class="sxs-lookup"><span data-stu-id="0e92a-303">Relevant audit storage table that was used at the time of the event to write audit log</span></span>

-   <span data-ttu-id="0e92a-304">事件發生之後一個小時內的稽核記錄。</span><span class="sxs-lookup"><span data-stu-id="0e92a-304">Audit records of the following hour since the event occurs.</span></span>

-   <span data-ttu-id="0e92a-305">事件發生時具有類似事件識別碼的稽核記錄 (對於某些偵測器而言是選擇性的)</span><span class="sxs-lookup"><span data-stu-id="0e92a-305">Audit records with similar event ID at the time of the event (optional for some detectors)</span></span>

<span data-ttu-id="0e92a-306">SQL Database 威脅偵測器會使用下列其中一種偵測方法：</span><span class="sxs-lookup"><span data-stu-id="0e92a-306">SQL Database Threat Detectors use one of the following detection methodologies:</span></span>

-   <span data-ttu-id="0e92a-307">**具決定性的偵測**：偵測 SQL 用戶端查詢中符合已知攻擊的可疑模式 (以規則為基礎)。</span><span class="sxs-lookup"><span data-stu-id="0e92a-307">**Deterministic Detection –** detects suspicious patterns (rules based) in the SQL client queries that match known attacks.</span></span> <span data-ttu-id="0e92a-308">這種方法具有高偵測度和低誤判率，但其涵蓋範圍有限，因為它屬於「不可部分完成的偵測」分類。</span><span class="sxs-lookup"><span data-stu-id="0e92a-308">This methodology has high detection and low false positive, however limited coverage because it falls within the category of “atomic detections”.</span></span>

-   <span data-ttu-id="0e92a-309">**偵測**：偵測異常活動，此為資料庫中未曾在過去 30 天內見到的異常行為。</span><span class="sxs-lookup"><span data-stu-id="0e92a-309">**Behavioural Detection –** defects anomalous activity, which is abnormal behavior for the database that was not seen during the last 30 days.</span></span>  <span data-ttu-id="0e92a-310">SQL 用戶端異常活動的範例可以是失敗的登入和查詢數目突然增加、擷取了大量的資料、不尋常的標準查詢，以及用來存取資料庫的陌生 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0e92a-310">An example for SQL client anomalous activity can be a spike of failed logins/queries, high volume of data being extracted, unusual canonical queries, and unfamiliar IP addresses used to access the database</span></span>

### <a name="application-gateway-web-application-firewall"></a><span data-ttu-id="0e92a-311">應用程式閘道 Web 應用程式防火牆</span><span class="sxs-lookup"><span data-stu-id="0e92a-311">Application Gateway Web Application Firewall</span></span>

<span data-ttu-id="0e92a-312">[Web 應用程式防火牆](https://docs.microsoft.com/azure/app-service-web/app-service-app-service-environment-web-application-firewall)是 [Azure 應用程式閘道](https://docs.microsoft.com/azure/application-gateway/application-gateway-webapplicationfirewall-overview)的一項功能，可保護使用應用程式閘道執行標準[應用程式傳遞控制 (英文)](https://kemptechnologies.com/in/application-delivery-controllers) 功能的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0e92a-312">[Web Application Firewall](https://docs.microsoft.com/azure/app-service-web/app-service-app-service-environment-web-application-firewall) is a feature of [Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-webapplicationfirewall-overview) that provides protection to web applications that use application gateway for standard [Application Delivery Control](https://kemptechnologies.com/in/application-delivery-controllers) functions.</span></span> <span data-ttu-id="0e92a-313">Web 應用程式防火牆的做法是保護應用程式，以防範 [OWASP 前 10 個最常見的 Web 弱點 (英文)](https://www.owasp.org/index.php/Top_10_2010-Main)。</span><span class="sxs-lookup"><span data-stu-id="0e92a-313">Web application firewall does this by protecting them against most of the [OWASP top 10 common web vulnerabilities](https://www.owasp.org/index.php/Top_10_2010-Main)</span></span>

![應用程式閘道 Web 應用程式防火牆](./media/azure-threat-detection/azure-threat-detection-fig13.png)

-   <span data-ttu-id="0e92a-315">SQL 插入式攻擊保護</span><span class="sxs-lookup"><span data-stu-id="0e92a-315">SQL injection protection</span></span>

-   <span data-ttu-id="0e92a-316">跨網站指令碼保護</span><span class="sxs-lookup"><span data-stu-id="0e92a-316">Cross site scripting protection</span></span>

-   <span data-ttu-id="0e92a-317">常見 Web 攻擊保護，例如命令插入式攻擊、HTTP 要求走私、HTTP 回應分割和遠端檔案包含攻擊</span><span class="sxs-lookup"><span data-stu-id="0e92a-317">Common Web Attacks Protection such as command injection, HTTP request smuggling, HTTP response splitting, and remote file inclusion attack</span></span>

-   <span data-ttu-id="0e92a-318">防範 HTTP 通訊協定違規</span><span class="sxs-lookup"><span data-stu-id="0e92a-318">Protection against HTTP protocol violations</span></span>

-   <span data-ttu-id="0e92a-319">防範 HTTP 通訊協定異常行為，例如遺漏主機使用者代理程式和接受標頭</span><span class="sxs-lookup"><span data-stu-id="0e92a-319">Protection against HTTP protocol anomalies such as missing host user-agent and accept headers</span></span>

-   <span data-ttu-id="0e92a-320">防範 Bot、編目程式和掃描器</span><span class="sxs-lookup"><span data-stu-id="0e92a-320">Prevention against bots, crawlers, and scanners</span></span>

-   <span data-ttu-id="0e92a-321">偵測一般應用程式錯誤組態 (也就是 Apache、IIS 等)</span><span class="sxs-lookup"><span data-stu-id="0e92a-321">Detection of common application misconfigurations (that is, Apache, IIS, etc.)</span></span>

<span data-ttu-id="0e92a-322">在應用程式閘道上設定 WAF 可為您提供下列好處：</span><span class="sxs-lookup"><span data-stu-id="0e92a-322">Configuring WAF at Application Gateway provides the following benefit to you:</span></span>

-   <span data-ttu-id="0e92a-323">不需修改後端程式碼就能保護 Web 應用程式不受 Web 弱點和攻擊的威脅。</span><span class="sxs-lookup"><span data-stu-id="0e92a-323">Protect your web application from web vulnerabilities and attacks without modification to backend code.</span></span>

-   <span data-ttu-id="0e92a-324">在應用程式閘道背後同時保護多個 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0e92a-324">Protect multiple web applications at the same time behind an application gateway.</span></span> <span data-ttu-id="0e92a-325">應用程式閘道可在單一閘道背後支援裝載最多 20 個網站，並且全都受到免於 Web 攻擊的保護。</span><span class="sxs-lookup"><span data-stu-id="0e92a-325">Application gateway supports hosting up to 20 websites behind a single gateway that could all be protected against web attacks.</span></span>

-   <span data-ttu-id="0e92a-326">使用應用程式閘道 WAF 記錄所產生的即時報告，監視 Web 應用程式對抗攻擊。</span><span class="sxs-lookup"><span data-stu-id="0e92a-326">Monitor your web application against attacks using real-time report generated by application gateway WAF logs.</span></span>

-   <span data-ttu-id="0e92a-327">某些法務遵循控制需要由 WAF 方案保護所有網際網路對向端點。</span><span class="sxs-lookup"><span data-stu-id="0e92a-327">Certain compliance controls require all internet facing end points to be protected by a WAF solution.</span></span> <span data-ttu-id="0e92a-328">使用已啟用 WAF 的應用程式閘道，您就可以符合這些法務遵循需求。</span><span class="sxs-lookup"><span data-stu-id="0e92a-328">By using application gateway with WAF enabled, you can meet these compliance requirements.</span></span>

### <a name="anomaly-detection--an-api-built-with-azure-machine-learning"></a><span data-ttu-id="0e92a-329">異常偵測：使用 Azure Machine Learning 建置的 API</span><span class="sxs-lookup"><span data-stu-id="0e92a-329">Anomaly Detection – an API built with Azure Machine Learning</span></span>

<span data-ttu-id="0e92a-330">異常偵測是使用 Azure Machine Learning 建置的 API，在時間序列資料中偵測不同類型的異常模式時非常有用。</span><span class="sxs-lookup"><span data-stu-id="0e92a-330">Anomaly Detection is an API built with Azure Machine Learning that is useful for detecting different types of anomalous patterns in your time series data.</span></span> <span data-ttu-id="0e92a-331">API 會為時間序列中的每個資料點指派異常分數，可用來產生警示、透過儀表板監視或與您的票證系統連線。</span><span class="sxs-lookup"><span data-stu-id="0e92a-331">The API assigns an anomaly score to each data point in the time series, which can be used for generating alerts, monitoring through dashboards or connecting with your ticketing systems.</span></span>

<span data-ttu-id="0e92a-332">[異常偵測 API](https://docs.microsoft.com/azure/machine-learning/machine-learning-apps-anomaly-detection-api) 可在時間序列資料上偵測下列異常類型：</span><span class="sxs-lookup"><span data-stu-id="0e92a-332">The [Anomaly Detection API](https://docs.microsoft.com/azure/machine-learning/machine-learning-apps-anomaly-detection-api) can detect the following types of anomalies on time series data:</span></span>

-   <span data-ttu-id="0e92a-333">**尖峰和下降**：例如，在監視服務的登入失敗數目或電子商務網站的結帳數目時，不尋常的尖峰或下降可能表示遭到安全性攻擊或服務中斷。</span><span class="sxs-lookup"><span data-stu-id="0e92a-333">**Spikes and Dips:** For example, when monitoring the number of login failures to a service or number of checkouts in an e-commerce site, unusual spikes or dips could indicate security attacks or service disruptions.</span></span>

-   <span data-ttu-id="0e92a-334">**上升和下滑趨勢**：例如，監視計算期間的記憶體使用量時，縮小可用的記憶體大小表示可能發生記憶體流失；監視服務佇列長度時，持續上升的趨勢可能代表發生基本的軟體問題。</span><span class="sxs-lookup"><span data-stu-id="0e92a-334">**Positive and negative trends:** When monitoring memory usage in computing, for instance, shrinking free memory size is indicative of a potential memory leak; when monitoring service queue length, a persistent upward trend may indicate an underlying software issue.</span></span>

-   <span data-ttu-id="0e92a-335">**層級變更與動態範圍值中的變更**：例如，在服務升級之後服務延遲中的層級變更，或升級之後較低層級的例外狀況，會使人有興趣加以監視。</span><span class="sxs-lookup"><span data-stu-id="0e92a-335">**Level changes and changes in dynamic range of values:** For example, level changes in latencies of a service after a service upgrade or lower levels of exceptions after upgrade can be interesting to monitor.</span></span>

<span data-ttu-id="0e92a-336">機器學習服務架構的 API 能夠進行下列動作：</span><span class="sxs-lookup"><span data-stu-id="0e92a-336">The machine learning based API enables:</span></span>

-   <span data-ttu-id="0e92a-337">**具彈性且健全的偵測**：異常偵測模型允許使用者設定具敏感性的設定，並偵測季節性和非季節性資料集之間的異常行為。</span><span class="sxs-lookup"><span data-stu-id="0e92a-337">**Flexible and robust detection:** The anomaly detection models allow users to configure sensitivity settings and detect anomalies among seasonal and non-seasonal data sets.</span></span> <span data-ttu-id="0e92a-338">使用者可以根據自己的需求來調整異常偵測模型，以降低或提高偵測 API 的敏感度。</span><span class="sxs-lookup"><span data-stu-id="0e92a-338">Users can adjust the anomaly detection model to make the detection API less or more sensitive according to their needs.</span></span> <span data-ttu-id="0e92a-339">這表示會在包含和不含季節性模式的資料中偵測較不常見或較常見的異常。</span><span class="sxs-lookup"><span data-stu-id="0e92a-339">This would mean detecting the less or more visible anomalies in data with and without seasonal patterns.</span></span>

-   <span data-ttu-id="0e92a-340">**可調整的即時偵測**：使用透過專家網域知識所設定之現有閾值進行監視的傳統方式既昂貴，又無法調整為數百萬個動態變更的資料集。</span><span class="sxs-lookup"><span data-stu-id="0e92a-340">**Scalable and timely detection:** The traditional way of monitoring with present thresholds set by experts' domain knowledge are costly and not scalable to millions of dynamically changing data sets.</span></span> <span data-ttu-id="0e92a-341">此 API 中的異常偵測模型會被學習，而且會從歷程記錄和即時資料自動調整模型。</span><span class="sxs-lookup"><span data-stu-id="0e92a-341">The anomaly detection models in this API are learned and models are tuned automatically from both historical and real-time data.</span></span>

-   <span data-ttu-id="0e92a-342">**主動且可採取動作的偵測**：緩慢的趨勢和層級變更偵測可應用於早期異常偵測。</span><span class="sxs-lookup"><span data-stu-id="0e92a-342">**Proactive and actionable detection:** Slow trend and level change detection can be applied for early anomaly detection.</span></span> <span data-ttu-id="0e92a-343">偵測到的早期異常訊號可用來引導使用者調查及處理問題區域。</span><span class="sxs-lookup"><span data-stu-id="0e92a-343">The early abnormal signals detected can be used to direct humans to investigate and act on the problem areas.</span></span>  <span data-ttu-id="0e92a-344">此外，還可以在此異常偵測 API 服務之上，開發根本原因分析模型和警示工具。</span><span class="sxs-lookup"><span data-stu-id="0e92a-344">In addition, root cause analysis models and alerting tools can be developed on top of this anomaly detection API service.</span></span>

<span data-ttu-id="0e92a-345">異常偵測 API 是適用於各種案例之有效且有效率的解決方案，例如，服務健全狀況和 KPI 監視、IoT、效能監視及網路流量監視。</span><span class="sxs-lookup"><span data-stu-id="0e92a-345">The anomaly detection API is an effective and efficient solution for a wide range of scenarios like service health & KPI monitoring, IoT, performance monitoring, and network traffic monitoring.</span></span> <span data-ttu-id="0e92a-346">以下提供一些常見案例，此 API 在這類案例中非常實用：</span><span class="sxs-lookup"><span data-stu-id="0e92a-346">Here are some popular scenarios where this API can be useful:</span></span>
- <span data-ttu-id="0e92a-347">IT 部門需要工具來即時追蹤事件、錯誤碼、使用量記錄及效能 (CPU、記憶體等)。</span><span class="sxs-lookup"><span data-stu-id="0e92a-347">IT departments need tools to track events, error code, usage log, and performance (CPU, Memory and so on) in a timely manner.</span></span>

-   <span data-ttu-id="0e92a-348">線上電子商務網站想要追蹤客戶活動、頁面檢視、點擊次數等項目。</span><span class="sxs-lookup"><span data-stu-id="0e92a-348">Online commerce sites want to track customer activities, page views, clicks, and so on.</span></span>

-   <span data-ttu-id="0e92a-349">公用事業公司想要追蹤水、天然氣、電力和其他資源的耗用量。</span><span class="sxs-lookup"><span data-stu-id="0e92a-349">Utility companies want to track consumption of water, gas, electricity, and other resources.</span></span>

-   <span data-ttu-id="0e92a-350">設備/大樓管理服務想要監視溫度、濕度、流量等項目。</span><span class="sxs-lookup"><span data-stu-id="0e92a-350">Facility/Building management services want to monitor temperature, moisture, traffic, and so on.</span></span>

-   <span data-ttu-id="0e92a-351">IoT/製造商想要使用時間序列中的感應器資料來監視工作流程、品質等項目。</span><span class="sxs-lookup"><span data-stu-id="0e92a-351">IoT/manufacturers want to use sensor data in time series to monitor work flow, quality, and so on.</span></span>

-   <span data-ttu-id="0e92a-352">服務提供者 (例如話務中心) 需要監視服務需求趨勢、事件量、等候佇列長度等項目。</span><span class="sxs-lookup"><span data-stu-id="0e92a-352">Service providers, such as call centers need to monitor service demand trend, incident volume, wait queue length and so on.</span></span>

-   <span data-ttu-id="0e92a-353">商務分析群組想要即時監視商務 KPI (例如銷售量、客戶人氣、定價) 的異常移動。</span><span class="sxs-lookup"><span data-stu-id="0e92a-353">Business analytics groups want to monitor business KPIs' (such as sales volume, customer sentiments, pricing) abnormal movement in real time.</span></span>

### <a name="cloud-app-security"></a><span data-ttu-id="0e92a-354">Cloud App Security</span><span class="sxs-lookup"><span data-stu-id="0e92a-354">Cloud App Security</span></span>

<span data-ttu-id="0e92a-355">[Cloud App Security](https://docs.microsoft.com/cloud-app-security/what-is-cloud-app-security) 是 Microsoft Cloud 安全性堆疊的一個重要元件。</span><span class="sxs-lookup"><span data-stu-id="0e92a-355">[Cloud App Security](https://docs.microsoft.com/cloud-app-security/what-is-cloud-app-security) is a critical component of the Microsoft Cloud Security stack.</span></span> <span data-ttu-id="0e92a-356">它是全方位的解決方案，可協助您的組織在您移動時能夠充分運用雲端應用程式的承諾，但仍能透過提高對活動的可見度來保留您的控制。</span><span class="sxs-lookup"><span data-stu-id="0e92a-356">It's a comprehensive solution that can help your organization as you move to take full advantage of the promise of cloud applications, but keep you in control, through improved visibility into activity.</span></span> <span data-ttu-id="0e92a-357">它也有助於跨雲端應用程式提高對重要資料的保護。</span><span class="sxs-lookup"><span data-stu-id="0e92a-357">It also helps increase the protection of critical data across cloud applications.</span></span>

<span data-ttu-id="0e92a-358">利用有助於揭露影子 IT、評估風險、強制執行原則、調查活動及停止威脅的工具，您的組織可以更安全的移至雲端，同時仍能控制重要資料。</span><span class="sxs-lookup"><span data-stu-id="0e92a-358">With tools that help uncover shadow IT, assess risk, enforce policies, investigate activities, and stop threats, your organization can more safely move to the cloud while maintaining control of critical data.</span></span>

<table style="width:100%">
 <tr>
   <td><span data-ttu-id="0e92a-359">探索</span><span class="sxs-lookup"><span data-stu-id="0e92a-359">Discover</span></span></td>
   <td><span data-ttu-id="0e92a-360">利用 Cloud App Security 來揭露影子 IT。</span><span class="sxs-lookup"><span data-stu-id="0e92a-360">Uncover shadow IT with Cloud App Security.</span></span> <span data-ttu-id="0e92a-361">藉由探索雲端環境中的應用程式、活動、使用者、資料和檔案，來取得可見度。</span><span class="sxs-lookup"><span data-stu-id="0e92a-361">Gain visibility by discovering apps, activities, users, data, and files in your cloud environment.</span></span> <span data-ttu-id="0e92a-362">探索連接到您雲端的協力廠商應用程式。</span><span class="sxs-lookup"><span data-stu-id="0e92a-362">Discover third-party apps that are connected to your cloud.</span></span></td>
 </tr>
 <tr>
   <td><span data-ttu-id="0e92a-363">調查</span><span class="sxs-lookup"><span data-stu-id="0e92a-363">Investigate</span></span></td>
   <td><span data-ttu-id="0e92a-364">使用雲端鑑識工具深入探討有風險的應用程式、特定的使用者及您網路中的檔案，藉以調查您的雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="0e92a-364">Investigate your cloud apps by using cloud forensics tools to deep-dive into risky apps, specific users, and files in your network.</span></span> <span data-ttu-id="0e92a-365">在收集自您雲端的資料中尋找模式。</span><span class="sxs-lookup"><span data-stu-id="0e92a-365">Find patterns in the data collected from your cloud.</span></span> <span data-ttu-id="0e92a-366">產生報告來監視您的雲端。</span><span class="sxs-lookup"><span data-stu-id="0e92a-366">Generate reports to monitor your cloud.</span></span></td>

 </tr>
 <tr>
   <td><span data-ttu-id="0e92a-367">控制</span><span class="sxs-lookup"><span data-stu-id="0e92a-367">Control</span></span></td>
   <td><span data-ttu-id="0e92a-368">藉由設定原則和警示以便能充分控制網路雲端流量來降低風險。</span><span class="sxs-lookup"><span data-stu-id="0e92a-368">Mitigate risk by setting policies and alerts to achieve maximum control over network cloud traffic.</span></span> <span data-ttu-id="0e92a-369">使用 Cloud App Security，將您的使用者移轉至安全且獲批准的雲端應用程式替代項目。</span><span class="sxs-lookup"><span data-stu-id="0e92a-369">Use Cloud App Security to migrate your users to safe, sanctioned cloud app alternatives.</span></span></td>

 </tr>
 <tr>
   <td><span data-ttu-id="0e92a-370">Protect</span><span class="sxs-lookup"><span data-stu-id="0e92a-370">Protect</span></span></td>
   <td><span data-ttu-id="0e92a-371">使用 Cloud App Security 來批准或禁止應用程式、強制執行資料損失防範措施、控制權限和共用，並產生自訂報告和警示。</span><span class="sxs-lookup"><span data-stu-id="0e92a-371">Use Cloud App Security to sanction or prohibit applications, enforce data loss prevention, control permissions and sharing, and generate custom reports and alerts.</span></span></td>

 </tr>
 <tr>
   <td><span data-ttu-id="0e92a-372">控制</span><span class="sxs-lookup"><span data-stu-id="0e92a-372">Control</span></span></td>
   <td><span data-ttu-id="0e92a-373">藉由設定原則和警示以便能充分控制網路雲端流量來降低風險。</span><span class="sxs-lookup"><span data-stu-id="0e92a-373">Mitigate risk by setting policies and alerts to achieve maximum control over network cloud traffic.</span></span> <span data-ttu-id="0e92a-374">使用 Cloud App Security，將您的使用者移轉至安全且獲批准的雲端應用程式替代項目。</span><span class="sxs-lookup"><span data-stu-id="0e92a-374">Use Cloud App Security to migrate your users to safe, sanctioned cloud app alternatives.</span></span></td>

 </tr>
</table>


![Cloud App Security](./media/azure-threat-detection/azure-threat-detection-fig14.png)

<span data-ttu-id="0e92a-376">Cloud App Security 會透過下列方式來整合您雲端的可見性</span><span class="sxs-lookup"><span data-stu-id="0e92a-376">Cloud App Security integrates visibility with your cloud by</span></span>

-   <span data-ttu-id="0e92a-377">使用 Cloud Discovery 來對應和識別您的雲端環境，以及您組織所使用的雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="0e92a-377">Using Cloud Discovery to map and identify your cloud environment and the cloud apps your organization is using.</span></span>


-   <span data-ttu-id="0e92a-378">批准和禁止您雲端中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0e92a-378">Sanctioning and prohibiting apps in your cloud.</span></span>



-   <span data-ttu-id="0e92a-379">使用易於部署的應用程式連接器，利用提供者 API 來取得您所連接之應用程式的可見度和控管。</span><span class="sxs-lookup"><span data-stu-id="0e92a-379">Using easy-to-deploy app connectors that take advantage of provider APIs, for visibility and governance of apps that you connect to.</span></span>

-   <span data-ttu-id="0e92a-380">透過設定，接著持續微調原則，協助您持續進行控制。</span><span class="sxs-lookup"><span data-stu-id="0e92a-380">Helping you have continuous control by setting, and then continually fine-tuning, policies.</span></span>

<span data-ttu-id="0e92a-381">從這些來源收集資料時，Cloud App Security 會對資料執行複雜的分析。</span><span class="sxs-lookup"><span data-stu-id="0e92a-381">On collecting data from these sources, Cloud App Security runs sophisticated analysis on the data.</span></span> <span data-ttu-id="0e92a-382">它會在發生異常活動時立即警示您，並讓您能深入檢視您的雲端環境。</span><span class="sxs-lookup"><span data-stu-id="0e92a-382">It immediately alerts you to anomalous activities, and gives you deep visibility into your cloud environment.</span></span> <span data-ttu-id="0e92a-383">您可以在 Cloud App Security 中設定原則，並使用它來保護您雲端環境中的一切。</span><span class="sxs-lookup"><span data-stu-id="0e92a-383">You can configure a policy in Cloud App Security and use it to protect everything in your cloud environment.</span></span>

## <a name="third-party-atd-capabilities-through-azure-marketplace"></a><span data-ttu-id="0e92a-384">透過 Azure Marketplace 提供的協力廠商 ATD 功能</span><span class="sxs-lookup"><span data-stu-id="0e92a-384">Third-party ATD capabilities through Azure Marketplace</span></span>

### <a name="web-application-firewall"></a><span data-ttu-id="0e92a-385">Web 應用程式防火牆</span><span class="sxs-lookup"><span data-stu-id="0e92a-385">Web Application Firewall</span></span>

<span data-ttu-id="0e92a-386">Web 應用程式防火牆會檢查輸入的 Web 流量和並封鎖 SQL 插入、跨網站指令碼、惡意程式碼上傳和應用程式 DDoS，以及目標為您 Web 應用程式的其他攻擊。</span><span class="sxs-lookup"><span data-stu-id="0e92a-386">Web Application Firewall inspects inbound web traffic and blocks SQL injections, Cross-Site Scripting, malware uploads & application DDoS and other attacks targeted at your web applications.</span></span> <span data-ttu-id="0e92a-387">它也會針對資料外洩防護 (DLP) 檢查來自後端 Web 伺服器的回應。</span><span class="sxs-lookup"><span data-stu-id="0e92a-387">It also inspects the responses from the back-end web servers for Data Loss Prevention (DLP).</span></span> <span data-ttu-id="0e92a-388">整合式存取控制引擎讓系統管理員能夠建立細微的存取控制原則以用於驗證、授權和帳戶處理 (AAA)，其可為組織提供增強式驗證和使用者控制。</span><span class="sxs-lookup"><span data-stu-id="0e92a-388">The integrated access control engine enables administrators to create granular access control policies for Authentication, Authorization & Accounting (AAA), which gives organizations strong authentication and user control.</span></span>

<span data-ttu-id="0e92a-389">**重點摘要：**</span><span class="sxs-lookup"><span data-stu-id="0e92a-389">**Highlights:**</span></span>
-   <span data-ttu-id="0e92a-390">偵測並封鎖 SQL 插入、跨網站指令碼、惡意程式碼上傳、應用程式 DDoS 或針對您應用程式的任何其他攻擊。</span><span class="sxs-lookup"><span data-stu-id="0e92a-390">Detects and blocks SQL injections, Cross-Site Scripting, malware uploads, application DDoS, or any other attacks against your application.</span></span>

-   <span data-ttu-id="0e92a-391">驗證和存取控制。</span><span class="sxs-lookup"><span data-stu-id="0e92a-391">Authentication and access control.</span></span>

-   <span data-ttu-id="0e92a-392">掃描輸出流量以偵測敏感性資料，並且可為資訊加上遮罩或封鎖以防止外洩。</span><span class="sxs-lookup"><span data-stu-id="0e92a-392">Scans outbound traffic to detect sensitive data and can mask or block the information from being leaked out.</span></span>

-   <span data-ttu-id="0e92a-393">使用快取、壓縮及其他流量最佳化等功能，來加速 Web 應用程式內容的傳遞。</span><span class="sxs-lookup"><span data-stu-id="0e92a-393">Accelerates the delivery of web application contents, using capabilities such as caching, compression, and other traffic optimizations.</span></span>

<span data-ttu-id="0e92a-394">以下是 Azure Market Place 中可用的 Web 應用程式防火牆範例：</span><span class="sxs-lookup"><span data-stu-id="0e92a-394">Following are example of Web Application firewalls available in Azure Market Place:</span></span>

<span data-ttu-id="0e92a-395">[Barracuda Web 應用程式防火牆、Brocade 虛擬 Web 應用程式防火牆 (Brocade vWAF)、Imperva SecureSphere 和 ThreatSTOP IP 防火牆 (英文)](https://azure.microsoft.com/marketplace/partners/brocade_communications/brocade-virtual-web-application-firewall-templatevtmcluster/)。</span><span class="sxs-lookup"><span data-stu-id="0e92a-395">[Barracuda Web Application Firewall, Brocade Virtual Web Application Firewall (Brocade vWAF), Imperva SecureSphere & The ThreatSTOP IP Firewall.](https://azure.microsoft.com/marketplace/partners/brocade_communications/brocade-virtual-web-application-firewall-templatevtmcluster/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e92a-396">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0e92a-396">Next Steps</span></span>

- [<span data-ttu-id="0e92a-397">Azure 資訊安全中心的偵測功能</span><span class="sxs-lookup"><span data-stu-id="0e92a-397">Azure Security Center detection capabilities</span></span>](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities)

<span data-ttu-id="0e92a-398">Azure 資訊安全中心的進階偵測功能，可協助您識別以您的 Microsoft Azure 資源為目標的作用中威脅，並提供您快速回應所需的深入見解。</span><span class="sxs-lookup"><span data-stu-id="0e92a-398">Azure Security Center’s advanced detection capabilities helps to identify active threats targeting your Microsoft Azure resources and provides you with the insights needed to respond quickly.</span></span>

- [<span data-ttu-id="0e92a-399">Azure SQL Database 威脅偵測 (英文)</span><span class="sxs-lookup"><span data-stu-id="0e92a-399">Azure SQL Database Threat Detection</span></span>](https://azure.microsoft.com/blog/azure-sql-database-threat-detection-your-built-in-security-expert/)

<span data-ttu-id="0e92a-400">Azure SQL Database 威脅偵測有助於解決他們對於其資料庫之潛在威脅的疑慮。</span><span class="sxs-lookup"><span data-stu-id="0e92a-400">Azure SQL Database Threat Detection helped address their concerns about potential threats to their database.</span></span>
