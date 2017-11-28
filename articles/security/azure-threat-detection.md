---
title: "aaaAzure 進階威脅偵測 |Microsoft 文件"
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
ms.openlocfilehash: 63e2c541fd4ce2c571af9d5845c9a9bd4b03b2a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-advanced-threat-detection"></a><span data-ttu-id="34f92-103">Azure 進階威脅偵測</span><span class="sxs-lookup"><span data-stu-id="34f92-103">Azure Advanced Threat Detection</span></span>
## <a name="introduction"></a><span data-ttu-id="34f92-104">簡介</span><span class="sxs-lookup"><span data-stu-id="34f92-104">Introduction</span></span>

### <a name="overview"></a><span data-ttu-id="34f92-105">概觀</span><span class="sxs-lookup"><span data-stu-id="34f92-105">Overview</span></span>

<span data-ttu-id="34f92-106">Microsoft 開發了一系列的技術白皮書、 安全性概觀、 最佳做法和檢查清單 tooassist Azure 客戶關於 hello 各種可用的安全性相關功能與周圍的 hello Azure 平台。</span><span class="sxs-lookup"><span data-stu-id="34f92-106">Microsoft has developed a series of White Papers, Security Overviews, Best Practices, and Checklists tooassist Azure customers about hello various security-related capabilities available in and surrounding hello Azure Platform.</span></span> <span data-ttu-id="34f92-107">hello 廣度及深度方面的主題範圍，並定期更新。</span><span class="sxs-lookup"><span data-stu-id="34f92-107">hello topics range in terms of breadth and depth and are updated periodically.</span></span> <span data-ttu-id="34f92-108">這份文件摘要 hello 遵循抽象 > 一節中為該系列的一部分。</span><span class="sxs-lookup"><span data-stu-id="34f92-108">This document is part of that series as summarized in hello following abstract section.</span></span>

### <a name="azure-platform"></a><span data-ttu-id="34f92-109">Azure 平台</span><span class="sxs-lookup"><span data-stu-id="34f92-109">Azure Platform</span></span>

<span data-ttu-id="34f92-110">Azure 是作業系統的公用雲端服務平台支援的程式設計語言、 架構、 工具、 資料庫和裝置 hello 最大範圍的選取範圍。</span><span class="sxs-lookup"><span data-stu-id="34f92-110">Azure is a public cloud service platform that supports hello broadest selection of operating systems, programming languages, frameworks, tools, databases, and devices.</span></span>
<span data-ttu-id="34f92-111">它支援下列程式設計語言的 hello:</span><span class="sxs-lookup"><span data-stu-id="34f92-111">It supports hello following programming languages:</span></span>
-   <span data-ttu-id="34f92-112">透過 Docker 整合執行 Linux 容器。</span><span class="sxs-lookup"><span data-stu-id="34f92-112">Run Linux containers with Docker integration.</span></span>
-   <span data-ttu-id="34f92-113">使用 JavaScript、Python、.NET、PHP、Java 和 Node.js 建置應用程式。</span><span class="sxs-lookup"><span data-stu-id="34f92-113">Build apps with JavaScript, Python, .NET, PHP, Java, and Node.js</span></span>
-   <span data-ttu-id="34f92-114">建置 iOS、Android 和 Windows 裝置的後端。</span><span class="sxs-lookup"><span data-stu-id="34f92-114">Build back-ends for iOS, Android, and Windows devices.</span></span>

<span data-ttu-id="34f92-115">Azure 公用雲端服務支援相同的技術數百萬的開發人員和 IT 專業人員已經依賴和信任的 hello。</span><span class="sxs-lookup"><span data-stu-id="34f92-115">Azure public cloud services support hello same technologies millions of developers and IT professionals already rely on and trust.</span></span>

<span data-ttu-id="34f92-116">當您移轉 tooa 與組織的公用雲端時，該組織是負責 tooprotect 您的資料，並提供安全性和 hello 系統周圍的控管。</span><span class="sxs-lookup"><span data-stu-id="34f92-116">When you are migrating tooa public cloud with an organization, that organization is responsible tooprotect your data and provide security and governance around hello system.</span></span>

<span data-ttu-id="34f92-117">從裝載吸引數百萬的客戶同時 hello 設備 tooapplications 設計 azure 的基礎結構，並提供的企業符合安全性需求的可信任基礎。</span><span class="sxs-lookup"><span data-stu-id="34f92-117">Azure’s infrastructure is designed from hello facility tooapplications for hosting millions of customers simultaneously, and it provides a trustworthy foundation upon which businesses can meet their security needs.</span></span> <span data-ttu-id="34f92-118">Azure 提供廣泛的選項 tooconfigure 與自訂安全性 toomeet hello 需求的應用程式部署。</span><span class="sxs-lookup"><span data-stu-id="34f92-118">Azure provides a wide array of options tooconfigure and customize security toomeet hello requirements of your app deployments.</span></span> <span data-ttu-id="34f92-119">本文件可協助您符合這些需求。</span><span class="sxs-lookup"><span data-stu-id="34f92-119">This document helps you meet these requirements.</span></span>

### <a name="abstract"></a><span data-ttu-id="34f92-120">摘要</span><span class="sxs-lookup"><span data-stu-id="34f92-120">Abstract</span></span>

<span data-ttu-id="34f92-121">Microsoft Azure 透過 Azure Active Directory、Azure Operations Management Suite (OMS) 及 Azure 資訊安全中心等服務，來提供內建的進階威脅偵測功能。</span><span class="sxs-lookup"><span data-stu-id="34f92-121">Microsoft Azure offers built in advanced threat detection functionality through services like Azure Active Directory, Azure Operations Management Suite (OMS), and Azure Security Center.</span></span> <span data-ttu-id="34f92-122">安全性服務和功能，這個集合會提供簡單又快速的方式 toounderstand 為什麼您的 Azure 部署中。</span><span class="sxs-lookup"><span data-stu-id="34f92-122">This collection of security services and capabilities provides a simple and fast way toounderstand what is happening within your Azure deployments.</span></span>

<span data-ttu-id="34f92-123">這份技術白皮書將引導您 hello 「 Microsoft Azure 方法 」 向潛在威脅的弱點可能會診斷和分析 hello 風險與 hello 惡意活動為目標的伺服器和其他 Azure 資源相關聯。</span><span class="sxs-lookup"><span data-stu-id="34f92-123">This white paper will guide you hello “Microsoft Azure approaches” towards threat vulnerability diagnostic and analysing hello risk associated with hello malicious activities targeted against servers and other Azure resources.</span></span> <span data-ttu-id="34f92-124">這可協助您識別 tooidentify hello 方法，而且的弱點可能會管理與最佳化方案 hello Azure 平台及客戶對向安全性服務和技術。</span><span class="sxs-lookup"><span data-stu-id="34f92-124">This helps you tooidentify hello methods of identification and vulnerability management with optimized solutions by hello Azure platform and customer-facing security services and technologies.</span></span>

<span data-ttu-id="34f92-125">這份技術白皮書著重在 Azure 平台和客戶對向控制項 hello 技術，並不會嘗試 tooaddress Sla 定價模型和 DevOps 作法的考量。</span><span class="sxs-lookup"><span data-stu-id="34f92-125">This white paper focuses on hello technology of Azure platform and customer-facing controls, and does not attempt tooaddress SLAs, pricing models, and DevOps practice considerations.</span></span>

## <a name="azure-active-directory-identity-protection"></a><span data-ttu-id="34f92-126">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="34f92-126">Azure Active Directory Identity Protection</span></span>

![Azure Active Directory Identity Protection](./media/azure-threat-detection/azure-threat-detection-fig1.png)


<span data-ttu-id="34f92-128">[Azure Active Directory 識別身分保護](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection)是一項功能的 hello [Azure AD Premium P2](https://docs.microsoft.com/azure/active-directory/active-directory-editions) hello 風險事件和潛在的弱點可能會影響您的組織的概觀會提供您的版本身分識別。</span><span class="sxs-lookup"><span data-stu-id="34f92-128">[Azure Active Directory Identity Protection](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection) is a feature of hello [Azure AD Premium P2](https://docs.microsoft.com/azure/active-directory/active-directory-editions) edition that provides you an overview of hello risk events and potential vulnerabilities affecting your organization’s identities.</span></span> <span data-ttu-id="34f92-129">Microsoft 有已保護的雲端式身分識別以來，和與 Azure AD Identity Protection Microsoft 提供這些相同的保護系統可用 tooenterprise 客戶。</span><span class="sxs-lookup"><span data-stu-id="34f92-129">Microsoft has been securing cloud-based identities for over a decade, and with Azure AD Identity Protection, Microsoft is making these same protection systems available tooenterprise customers.</span></span> <span data-ttu-id="34f92-130">Identity Protection 使用現有 Azure AD 的異常偵測功能 (可透過 [Azure AD 的異常活動報告](https://docs.microsoft.com/azure/active-directory/active-directory-view-access-usage-reports#anomalous-activity-reports)取得)，並引進可即時偵測異常的新風險事件類型。</span><span class="sxs-lookup"><span data-stu-id="34f92-130">Identity Protection uses existing Azure AD’s anomaly detection capabilities available through [Azure AD’s Anomalous Activity Reports](https://docs.microsoft.com/azure/active-directory/active-directory-view-access-usage-reports#anomalous-activity-reports), and introduces new risk event types that can detect real time anomalies.</span></span>

<span data-ttu-id="34f92-131">自動調整的機器學習演算法和啟發學習法 toodetect 異常可能表示身分識別已遭洩漏的風險事件，則會使用識別身分保護。</span><span class="sxs-lookup"><span data-stu-id="34f92-131">Identity Protection uses adaptive machine learning algorithms and heuristics toodetect anomalies and risk events that may indicate that an identity has been compromised.</span></span> <span data-ttu-id="34f92-132">使用這項資料，識別身分保護會產生報表和警示可讓您 tooinvestigate 這些風險事件，並採取適當的補救或補救動作。</span><span class="sxs-lookup"><span data-stu-id="34f92-132">Using this data, Identity Protection generates reports and alerts that enable you tooinvestigate these risk events and take appropriate remediation or mitigation action.</span></span>

<span data-ttu-id="34f92-133">但是，Azure Active Directory Identity Protection 不只是監視和報告工具而已。</span><span class="sxs-lookup"><span data-stu-id="34f92-133">But Azure Active Directory Identity Protection is more than a monitoring and reporting tool.</span></span> <span data-ttu-id="34f92-134">根據風險事件，Identity Protection 會計算每位使用者的使用者風險層級，讓您 tooconfigure 風險為基礎的原則保護 tooautomatically hello 您組織的身分識別。</span><span class="sxs-lookup"><span data-stu-id="34f92-134">Based on risk events, Identity Protection calculates a user risk level for each user, enabling you tooconfigure risk-based policies tooautomatically protect hello identities of your organization.</span></span>

<span data-ttu-id="34f92-135">這些風險型原則，請在加法 tooother[條件式存取控制](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access)提供由 Azure Active Directory 和[EMS](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access)、 可以自動封鎖或提供彈性的修復動作，包括密碼重設以及強制多因素驗證。</span><span class="sxs-lookup"><span data-stu-id="34f92-135">These risk-based policies, in addition tooother [conditional access controls](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) provided by Azure Active Directory and [EMS](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access), can automatically block or offer adaptive remediation actions that include password resets and multi-factor authentication enforcement.</span></span>

### <a name="identity-protections-capabilities"></a><span data-ttu-id="34f92-136">Identity Protection 的功能</span><span class="sxs-lookup"><span data-stu-id="34f92-136">Identity Protection's capabilities</span></span>

<span data-ttu-id="34f92-137">Azure Active Directory Identity Protection 不只是監視和報告工具而已。</span><span class="sxs-lookup"><span data-stu-id="34f92-137">Azure Active Directory Identity Protection is more than a monitoring and reporting tool.</span></span> <span data-ttu-id="34f92-138">tooprotect 貴組織的身分識別，您可以設定在達到指定的風險層級時，自動回應 toodetected 問題的風險為基礎原則。</span><span class="sxs-lookup"><span data-stu-id="34f92-138">tooprotect your organization's identities, you can configure risk-based policies that automatically respond toodetected issues when a specified risk level has been reached.</span></span> <span data-ttu-id="34f92-139">這些原則，除了 tooother 條件式存取 Azure Active Directory 和 EMS 所提供的控制項，可以自動封鎖或起始自動調整的修復動作，包括密碼重設以及強制多因素驗證。</span><span class="sxs-lookup"><span data-stu-id="34f92-139">These policies, in addition tooother conditional access controls provided by Azure Active Directory and EMS, can either automatically block or initiate adaptive remediation actions including password resets and multi-factor authentication enforcement.</span></span>

<span data-ttu-id="34f92-140">Hello 方式 Azure 識別身分保護可幫助的一些範例保護您的帳戶，並識別包括：</span><span class="sxs-lookup"><span data-stu-id="34f92-140">Examples of some of hello ways that Azure Identity Protection can help secure your accounts and identities include:</span></span>

[<span data-ttu-id="34f92-141">偵測風險事件和有風險的帳戶：</span><span class="sxs-lookup"><span data-stu-id="34f92-141">Detecting risk events and risky accounts:</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#detection)
-   <span data-ttu-id="34f92-142">使用機器學習服務和啟發式規則偵測六種風險事件類型</span><span class="sxs-lookup"><span data-stu-id="34f92-142">Detecting six risk event types using machine learning and heuristic rules</span></span>
-   <span data-ttu-id="34f92-143">計算使用者風險層級</span><span class="sxs-lookup"><span data-stu-id="34f92-143">Calculating user risk levels</span></span>
-   <span data-ttu-id="34f92-144">提供自訂的建議 tooimprove 透過的弱點可能會反白顯示整體的安全性狀態</span><span class="sxs-lookup"><span data-stu-id="34f92-144">Providing custom recommendations tooimprove overall security posture by highlighting vulnerabilities</span></span>

[<span data-ttu-id="34f92-145">調查風險事件：</span><span class="sxs-lookup"><span data-stu-id="34f92-145">Investigating risk events:</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#investigation)
-   <span data-ttu-id="34f92-146">傳送風險事件的通知</span><span class="sxs-lookup"><span data-stu-id="34f92-146">Sending notifications for risk events</span></span>
-   <span data-ttu-id="34f92-147">使用相關和內容資訊來調查風險事件</span><span class="sxs-lookup"><span data-stu-id="34f92-147">Investigating risk events using relevant and contextual information</span></span>
-   <span data-ttu-id="34f92-148">提供基本工作流程 tootrack 調查</span><span class="sxs-lookup"><span data-stu-id="34f92-148">Providing basic workflows tootrack investigations</span></span>
-   <span data-ttu-id="34f92-149">讓您輕鬆存取 tooremediation 動作，例如密碼重設</span><span class="sxs-lookup"><span data-stu-id="34f92-149">Providing easy access tooremediation actions such as password reset</span></span>

[<span data-ttu-id="34f92-150">以風險為基礎的條件式存取原則：</span><span class="sxs-lookup"><span data-stu-id="34f92-150">Risk-based conditional access policies:</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#risky-sign-ins)
-   <span data-ttu-id="34f92-151">原則 toomitigate 風險登入所封鎖登入，或要求多重要素驗證挑戰。</span><span class="sxs-lookup"><span data-stu-id="34f92-151">Policy toomitigate risky sign-ins by blocking sign-ins or requiring multi-factor authentication challenges.</span></span>
-   <span data-ttu-id="34f92-152">原則 tooblock 或安全風險的使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="34f92-152">Policy tooblock or secure risky user accounts</span></span>
-   <span data-ttu-id="34f92-153">原則 toorequire 使用者 tooregister 的多重要素驗證</span><span class="sxs-lookup"><span data-stu-id="34f92-153">Policy toorequire users tooregister for multi-factor authentication</span></span>

### <a name="azure-ad-privileged-identity-management-pim"></a><span data-ttu-id="34f92-154">Azure AD Privileged Identity Management (PIM)</span><span class="sxs-lookup"><span data-stu-id="34f92-154">Azure AD Privileged Identity Management (PIM)</span></span>

<span data-ttu-id="34f92-155">利用 [Azure Active Directory (AD) Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure)，</span><span class="sxs-lookup"><span data-stu-id="34f92-155">With [Azure Active Directory (AD) Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure),</span></span>

![Azure AD 特殊權限身分識別管理](./media/azure-threat-detection/azure-threat-detection-fig2.png)

<span data-ttu-id="34f92-157">您可以管理、控制及監視組織內的存取。</span><span class="sxs-lookup"><span data-stu-id="34f92-157">you can manage, control, and monitor access within your organization.</span></span> <span data-ttu-id="34f92-158">這包括存取 tooresources 在 Azure AD 和 Office 365 或 Microsoft Intune 等其他 Microsoft online services。</span><span class="sxs-lookup"><span data-stu-id="34f92-158">This includes access tooresources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="34f92-159">Azure AD Privileged Identity Management 可協助您：</span><span class="sxs-lookup"><span data-stu-id="34f92-159">Azure AD Privileged Identity Management helps you:</span></span>

-   <span data-ttu-id="34f92-160">取得警示和報告 Azure AD 系統管理員和"just-in-time"系統管理存取權 tooMicrosoft 線上服務，例如 Office 365 和 Intune</span><span class="sxs-lookup"><span data-stu-id="34f92-160">Get an alert and report on Azure AD administrators and "just in time" administrative access tooMicrosoft Online Services like Office 365 and Intune</span></span>

-   <span data-ttu-id="34f92-161">取得有關系統管理員存取記錄與系統管理員指派變更的報告</span><span class="sxs-lookup"><span data-stu-id="34f92-161">Get reports about administrator access history and changes in administrator assignments</span></span>

-   <span data-ttu-id="34f92-162">取得警示存取 tooa 特殊權限角色</span><span class="sxs-lookup"><span data-stu-id="34f92-162">Get alerts about access tooa privileged role</span></span>

## <a name="microsoft-operations-management-suite-oms"></a><span data-ttu-id="34f92-163">Microsoft Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="34f92-163">Microsoft Operations Management Suite (OMS)</span></span>

<span data-ttu-id="34f92-164">[Microsoft Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) 是 Microsoft 的雲端型 IT 管理解決方案，可協助您管理並保護內部部署和雲端基礎結構。</span><span class="sxs-lookup"><span data-stu-id="34f92-164">[Microsoft Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="34f92-165">因為 OMS 實作為雲端型服務，所以您對基礎結構服務進行最小的投資就可以快速啟動並執行它。</span><span class="sxs-lookup"><span data-stu-id="34f92-165">Since OMS is implemented as a cloud-based service, you can have it up and running quickly with minimal investment in infrastructure services.</span></span> <span data-ttu-id="34f92-166">新的安全性功能會自動提供，以節省持續維護和升級成本。</span><span class="sxs-lookup"><span data-stu-id="34f92-166">New security features are delivered automatically, saving your ongoing maintenance and upgrade costs.</span></span>

<span data-ttu-id="34f92-167">此外 tooproviding 重要服務在其本身，OMS 可以整合 System Center 元件這類[System Center Operations Manager](https://blogs.technet.microsoft.com/cbernier/2013/10/23/monitoring-windows-azure-with-system-center-operations-manager-2012-get-me-started/) tooextend 現有的安全性管理投資 hello 到雲端。</span><span class="sxs-lookup"><span data-stu-id="34f92-167">In addition tooproviding valuable services on its own, OMS can integrate with System Center components such as [System Center Operations Manager](https://blogs.technet.microsoft.com/cbernier/2013/10/23/monitoring-windows-azure-with-system-center-operations-manager-2012-get-me-started/) tooextend your existing security management investments into hello cloud.</span></span> <span data-ttu-id="34f92-168">System Center 和 OMS 可一起運作的 tooprovide 完整的混合式管理體驗。</span><span class="sxs-lookup"><span data-stu-id="34f92-168">System Center and OMS can work together tooprovide a full hybrid management experience.</span></span>

### <a name="holistic-security-and-compliance-posture"></a><span data-ttu-id="34f92-169">整體安全性與合規性狀態</span><span class="sxs-lookup"><span data-stu-id="34f92-169">Holistic Security and Compliance Posture</span></span>

<span data-ttu-id="34f92-170">hello [OMS 安全性和稽核儀表板](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started)讓您完整檢視您組織的 IT 安全性狀況，針對值得您注意的問題使用內建的搜尋查詢。</span><span class="sxs-lookup"><span data-stu-id="34f92-170">hello [OMS Security and Audit dashboard](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) provides a comprehensive view into your organization’s IT security posture with built-in search queries for notable issues that require your attention.</span></span> <span data-ttu-id="34f92-171">hello 安全性和稽核儀表板是所有項目 hello 主畫面相關 toosecurity 在 OMS 中。</span><span class="sxs-lookup"><span data-stu-id="34f92-171">hello Security and Audit dashboard is hello home screen for everything related toosecurity in OMS.</span></span> <span data-ttu-id="34f92-172">會提供在電腦的 hello 安全性狀態的高層級深入。</span><span class="sxs-lookup"><span data-stu-id="34f92-172">It provides high-level insight into hello security state of your computers.</span></span> <span data-ttu-id="34f92-173">它也包含 hello 能力 tooview hello 過去 24 小時、 7 天的所有事件或任何其他自訂的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="34f92-173">It also includes hello ability tooview all events from hello past 24 hours, 7 days, or any other custom time frame.</span></span>

<span data-ttu-id="34f92-174">OMS 儀表板幫助您快速且輕鬆地了解 hello 全部都在 IT 作業，包括 hello 內容內的所有環境的整體安全性狀況： 軟體更新評估、 反惡意程式碼評估和設定基準。</span><span class="sxs-lookup"><span data-stu-id="34f92-174">OMS dashboards help you quickly and easily understand hello overall security posture of any environment, all within hello context of IT Operations, including: software update assessment, antimalware assessment, and configuration baselines.</span></span> <span data-ttu-id="34f92-175">此外，安全性記錄檔資料會立即存取 toostreamline hello 安全性與相容性稽核程序。</span><span class="sxs-lookup"><span data-stu-id="34f92-175">Furthermore, security log data is readily accessible toostreamline hello security and compliance audit processes.</span></span>

<span data-ttu-id="34f92-176">hello OMS 安全性和稽核儀表板分為四個主要類別：</span><span class="sxs-lookup"><span data-stu-id="34f92-176">hello OMS Security and Audit dashboard is organized in four major categories:</span></span>

![OMS 安全性和稽核儀表板](./media/azure-threat-detection/azure-threat-detection-fig3.jpg)

-   <span data-ttu-id="34f92-178">**安全性網域：**在這個區域中，您將無法 toofurther 探索安全性記錄一段時間，存取惡意程式碼評估、 更新評估、 網路安全性、 身分識別和存取資訊、 電腦與安全性事件並能快速地存取 tooAzure 資訊安全中心儀表板。</span><span class="sxs-lookup"><span data-stu-id="34f92-178">**Security Domains:** in this area, you will be able toofurther explore security records over time, access malware assessment, update assessment, network security, identity and access information, computers with security events and quickly have access tooAzure Security Center dashboard.</span></span>

-   <span data-ttu-id="34f92-179">**值得注意的問題：**此選項可讓您 tooquickly 識別作用中問題的 hello 數目和 hello 這些問題的嚴重性。</span><span class="sxs-lookup"><span data-stu-id="34f92-179">**Notable Issues:** this option allows you tooquickly identify hello number of active issues and hello severity of these issues.</span></span>

-   <span data-ttu-id="34f92-180">**偵測 （預覽）：**可讓您透過視覺化安全性警示，因為它們對您的資源進行的 tooidentify 攻擊的模式。</span><span class="sxs-lookup"><span data-stu-id="34f92-180">**Detections (Preview):** enables you tooidentify attack patterns by visualizing security alerts as they take place against your resources.</span></span>

-   <span data-ttu-id="34f92-181">**威脅情報：**可讓您所視覺化的具有惡意連出 IP 流量、 hello 惡意之威脅類型，以及顯示這些 Ip 所在的對應伺服器 hello 總數的 tooidentify 攻擊的模式。</span><span class="sxs-lookup"><span data-stu-id="34f92-181">**Threat Intelligence:** enables you tooidentify attack patterns by visualizing hello total number of servers with outbound malicious IP traffic, hello malicious threat type, and a map that shows where these IPs are coming from.</span></span>

-   <span data-ttu-id="34f92-182">**常見安全性查詢：**這個選項提供您一份 hello 最常見安全性查詢，您可以使用 toomonitor 您的環境。</span><span class="sxs-lookup"><span data-stu-id="34f92-182">**Common security queries:** this option provides you a list of hello most common security queries that you can use toomonitor your environment.</span></span> <span data-ttu-id="34f92-183">當您按一下其中一個這些查詢中時，它會開啟刀鋒視窗中搜尋 hello 與 hello 該查詢的結果。</span><span class="sxs-lookup"><span data-stu-id="34f92-183">When you click in one of those queries, it opens hello Search blade with hello results for that query.</span></span>

### <a name="insight-and-analytics"></a><span data-ttu-id="34f92-184">深入解析與分析</span><span class="sxs-lookup"><span data-stu-id="34f92-184">Insight and Analytics</span></span>
<span data-ttu-id="34f92-185">Hello 中央的[記錄分析](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)是 hello OMS 儲存機制裝載在 hello Azure 雲端。</span><span class="sxs-lookup"><span data-stu-id="34f92-185">At hello center of [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) is hello OMS repository, which is hosted in hello Azure cloud.</span></span>

![深入解析與分析](./media/azure-threat-detection/azure-threat-detection-fig4.png)

<span data-ttu-id="34f92-187">到 hello 儲存機制從所設定的資料來源和加入解決方案 tooyour 訂用帳戶連線來源收集資料。</span><span class="sxs-lookup"><span data-stu-id="34f92-187">Data is collected into hello repository from connected sources by configuring data sources and adding solutions tooyour subscription.</span></span>

![訂用帳戶](./media/azure-threat-detection/azure-threat-detection-fig5.png)

<span data-ttu-id="34f92-189">資料來源和解決方案將每個建立自己的屬性集，但可能仍然會分析一起查詢 toohello 儲存機制中不同的記錄類型。</span><span class="sxs-lookup"><span data-stu-id="34f92-189">Data sources and solutions will each create different record types that have their own set of properties but may still be analyzed together in queries toohello repository.</span></span> <span data-ttu-id="34f92-190">這可讓您 toouse hello 與不同類型的資料相同的工具和方法 toowork 收集不同的來源。</span><span class="sxs-lookup"><span data-stu-id="34f92-190">This allows you toouse hello same tools and methods toowork with different kinds of data collected by different sources.</span></span>


<span data-ttu-id="34f92-191">大部分的記錄分析與您互動都是透過 hello OMS 入口網站，它會在任何瀏覽器中執行，並提供您存取 tooconfiguration 設定和與多個工具 tooanalyze 在收集的資料上運作。</span><span class="sxs-lookup"><span data-stu-id="34f92-191">Most of your interaction with Log Analytics is through hello OMS portal, which runs in any browser and provides you with access tooconfiguration settings and multiple tools tooanalyze and act on collected data.</span></span> <span data-ttu-id="34f92-192">從 hello 入口網站，您可以使用[記錄搜尋](https://docs.microsoft.com/azure/log-analytics/log-analytics-log-searches)建構查詢 tooanalyze 收集資料，其中[儀表板](https://docs.microsoft.com/azure/log-analytics/log-analytics-dashboards)，您可利用圖形檢視最有價值的搜尋，以及自訂[解決方案](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions)，這兩個提供額外的功能和分析工具。</span><span class="sxs-lookup"><span data-stu-id="34f92-192">From hello portal, you can use [log searches](https://docs.microsoft.com/azure/log-analytics/log-analytics-log-searches) where you construct queries tooanalyze collected data, [dashboards](https://docs.microsoft.com/azure/log-analytics/log-analytics-dashboards), which you can customize with graphical views of your most valuable searches, and [solutions](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions), which provide additional functionality and analysis tools.</span></span>

![分析工具](./media/azure-threat-detection/azure-threat-detection-fig6.png)

<span data-ttu-id="34f92-194">解決方案會將功能 tooLog 分析。</span><span class="sxs-lookup"><span data-stu-id="34f92-194">Solutions add functionality tooLog Analytics.</span></span> <span data-ttu-id="34f92-195">這些主要在 hello 雲端中執行，並且提供 hello OMS 儲存機制所收集的資料分析。</span><span class="sxs-lookup"><span data-stu-id="34f92-195">They primarily run in hello cloud and provide analysis of data collected in hello OMS repository.</span></span> <span data-ttu-id="34f92-196">它們也必須定義新記錄類型 toobe 收集可分析記錄搜尋而 hello OMS 儀表板中的 hello 方案所提供的其他使用者介面。</span><span class="sxs-lookup"><span data-stu-id="34f92-196">They may also define new record types toobe collected that can be analyzed with Log Searches or by additional user interface provided by hello solution in hello OMS dashboard.</span></span>
<span data-ttu-id="34f92-197">hello 安全性和稽核是這類解決方案的範例。</span><span class="sxs-lookup"><span data-stu-id="34f92-197">hello Security and Audit is an example of these types of solutions.</span></span>



### <a name="automation--control-alert-on-security-configuration-drifts"></a><span data-ttu-id="34f92-198">自動化與控制︰有關安全性設定漂移的警示</span><span class="sxs-lookup"><span data-stu-id="34f92-198">Automation & Control: Alert on security configuration drifts</span></span>

<span data-ttu-id="34f92-199">Azure 自動化可自動化管理程序，使用 PowerShell 為基礎且在 hello Azure 雲端中執行的 runbook。</span><span class="sxs-lookup"><span data-stu-id="34f92-199">Azure Automation automates administrative processes with runbooks that are based on PowerShell and run in hello Azure cloud.</span></span> <span data-ttu-id="34f92-200">也可以在您本機資料中心 toomanage 本機資源的伺服器上，執行 Runbook。</span><span class="sxs-lookup"><span data-stu-id="34f92-200">Runbooks can also be executed on a server in your local data center toomanage local resources.</span></span> <span data-ttu-id="34f92-201">Azure 自動化會使用 PowerShell DSC (Desired State Configuration) 來提供設定管理。</span><span class="sxs-lookup"><span data-stu-id="34f92-201">Azure Automation provides configuration management with PowerShell DSC (Desired State Configuration).</span></span>

![Azure 自動化](./media/azure-threat-detection/azure-threat-detection-fig7.png)

<span data-ttu-id="34f92-203">您可以建立和管理裝載於 Azure 的 DSC 資源並將其套用 toocloud 和內部系統 toodefine 和自動強制執行其設定或取得報表漂移時即 toohelp 確保安全性設定保留原則內。</span><span class="sxs-lookup"><span data-stu-id="34f92-203">You can create and manage DSC resources hosted in Azure and apply them toocloud and on-premises systems toodefine and automatically enforce their configuration or get reports on drift toohelp insure that security configurations remain within policy.</span></span>

## <a name="azure-security-center"></a><span data-ttu-id="34f92-204">Azure 資訊安全中心</span><span class="sxs-lookup"><span data-stu-id="34f92-204">Azure Security Center</span></span>

<span data-ttu-id="34f92-205">Azure 資訊安全中心可協助保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="34f92-205">Azure Security Center helps protect your Azure resources.</span></span> <span data-ttu-id="34f92-206">它提供您 Azure 訂用帳戶之間的整合式安全性監視和原則管理。</span><span class="sxs-lookup"><span data-stu-id="34f92-206">It provides integrated security monitoring and policy management across your Azure subscriptions.</span></span> <span data-ttu-id="34f92-207">Hello 在服務內，您就可以 toodefine 原則不只是針對您 Azure 訂用帳戶，同時也針對[資源群組](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal)，使您能夠更細微。</span><span class="sxs-lookup"><span data-stu-id="34f92-207">Within hello service, you are able toodefine polices not only against your Azure subscriptions, but also against [Resource Groups](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal), so you can be more granular.</span></span>

![Azure 資訊安全中心](./media/azure-threat-detection/azure-threat-detection-fig8.png)

<span data-ttu-id="34f92-209">Microsoft 安全性研究人員經常位於 hello lookout 的威脅。</span><span class="sxs-lookup"><span data-stu-id="34f92-209">Microsoft security researchers are constantly on hello lookout for threats.</span></span> <span data-ttu-id="34f92-210">他們有存取 tooan 以免受到擴充獲得 Microsoft 的全域存在 hello 雲端和內部部署中的遙測。</span><span class="sxs-lookup"><span data-stu-id="34f92-210">They have access tooan expansive set of telemetry gained from Microsoft’s global presence in hello cloud and on-premises.</span></span> <span data-ttu-id="34f92-211">這個寬到達的各種集合的資料集可讓 Microsoft toodiscover 新的攻擊模式和趨勢跨越其內部消費者和企業產品，以及其線上服務。</span><span class="sxs-lookup"><span data-stu-id="34f92-211">This wide-reaching and diverse collection of datasets enables Microsoft toodiscover new attack patterns and trends across its on-premises consumer and enterprise products, as well as its online services.</span></span>

<span data-ttu-id="34f92-212">因此，資訊安全中心可以在攻擊者發行新的和日益複雜的攻擊時，快速地更新其偵測演算法。</span><span class="sxs-lookup"><span data-stu-id="34f92-212">Thus, Security Center can rapidly update its detection algorithms as attackers release new and increasingly sophisticated exploits.</span></span> <span data-ttu-id="34f92-213">這種方法可協助您跟上瞬息萬變的威脅環境。</span><span class="sxs-lookup"><span data-stu-id="34f92-213">This approach helps you keep pace with a fast-moving threat environment.</span></span>

![資訊安全中心](./media/azure-threat-detection/azure-threat-detection-fig9.jpg)

<span data-ttu-id="34f92-215">資訊安全中心威脅偵測的運作方式自動收集您的 Azure 資源、 hello 網路和連線的交易夥伴方案中的 安全性資訊。</span><span class="sxs-lookup"><span data-stu-id="34f92-215">Security Center threat detection works by automatically collecting security information from your Azure resources, hello network, and connected partner solutions.</span></span>  <span data-ttu-id="34f92-216">它會分析這項資訊相互關聯多個來源，tooidentify 威脅的資訊。</span><span class="sxs-lookup"><span data-stu-id="34f92-216">It analyzes this information, correlating information from multiple sources, tooidentify threats.</span></span>
<span data-ttu-id="34f92-217">安全性警示的優先順序資訊安全中心以及如何 tooremediate hello 威脅的建議。</span><span class="sxs-lookup"><span data-stu-id="34f92-217">Security alerts are prioritized in Security Center along with recommendations on how tooremediate hello threat.</span></span>

<span data-ttu-id="34f92-218">資訊安全中心會運用進階安全性分析，其遠勝於以簽章為基礎的方法。</span><span class="sxs-lookup"><span data-stu-id="34f92-218">Security Center employs advanced security analytics, which go far beyond signature-based approaches.</span></span> <span data-ttu-id="34f92-219">巨量資料中的突破和[機器學習](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/)技術都使用的 tooevaluate 事件 hello 整個雲端網狀架構 – 偵測會是不可能 tooidentify 使用手動方法，並預測 hello 的威脅演進而來的攻擊。</span><span class="sxs-lookup"><span data-stu-id="34f92-219">Breakthroughs in big data and [machine learning](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/) technologies are used tooevaluate events across hello entire cloud fabric – detecting threats that would be impossible tooidentify using manual approaches and predicting hello evolution of attacks.</span></span> <span data-ttu-id="34f92-220">這些安全性分析包含下列 hello。</span><span class="sxs-lookup"><span data-stu-id="34f92-220">These security analytics includes hello following.</span></span>

### <a name="threat-intelligence"></a><span data-ttu-id="34f92-221">威脅情報</span><span class="sxs-lookup"><span data-stu-id="34f92-221">Threat Intelligence</span></span>

<span data-ttu-id="34f92-222">Microsoft 有大量全域威脅情報。</span><span class="sxs-lookup"><span data-stu-id="34f92-222">Microsoft has an immense amount of global threat intelligence.</span></span>
<span data-ttu-id="34f92-223">遙測中傳送多個來源，例如 Azure、 Office 365、 Microsoft CRM online、 Microsoft Dynamics AX、 outlook.com、 MSN.com、 hello Microsoft 數位犯罪單元 (DCU)，以及 Microsoft Security Response Center (MSRC)。</span><span class="sxs-lookup"><span data-stu-id="34f92-223">Telemetry flows in from multiple sources, such as Azure, Office 365, Microsoft CRM online, Microsoft Dynamics AX, outlook.com, MSN.com, hello Microsoft Digital Crimes Unit (DCU), and Microsoft Security Response Center (MSRC).</span></span>

![威脅情報](./media/azure-threat-detection/azure-threat-detection-fig10.jpg)

<span data-ttu-id="34f92-225">研究人員也會收到威脅情報資訊主要雲端服務提供者之間共用，並從第三方訂閱 toothreat intelligence 摘要。</span><span class="sxs-lookup"><span data-stu-id="34f92-225">Researchers also receive threat intelligence information that is shared among major cloud service providers and subscribes toothreat intelligence feeds from third parties.</span></span> <span data-ttu-id="34f92-226">Azure 資訊安全中心可以使用此資訊 tooalert 您 toothreats 從已知不良執行者。</span><span class="sxs-lookup"><span data-stu-id="34f92-226">Azure Security Center can use this information tooalert you toothreats from known bad actors.</span></span> <span data-ttu-id="34f92-227">部分範例包括：</span><span class="sxs-lookup"><span data-stu-id="34f92-227">Some examples include:</span></span>

-   <span data-ttu-id="34f92-228">**另外 hello 電源 Machine Learning-** Azure 資訊安全中心具有存取 tooa 大量資料的相關雲端網路活動，它可以是使用目標 Azure 部署 toodetect 威脅。</span><span class="sxs-lookup"><span data-stu-id="34f92-228">**Harnessing hello Power of Machine Learning -** Azure Security Center has access tooa vast amount of data about cloud network activity, which can be used toodetect threats targeting your Azure deployments.</span></span> <span data-ttu-id="34f92-229">例如：</span><span class="sxs-lookup"><span data-stu-id="34f92-229">For example:</span></span>

-   <span data-ttu-id="34f92-230">**破解強制偵測-**機器學習服務使用的 toocreate 歷程記錄模式的遠端存取嘗試，好讓它 toodetect 暴力攻擊針對 SSH、 RDP 和 SQL 連接埠。</span><span class="sxs-lookup"><span data-stu-id="34f92-230">**Brute Force Detections -** Machine learning is used toocreate a historical pattern of remote access attempts, which allows it toodetect brute force attacks against SSH, RDP, and SQL ports.</span></span>

-   <span data-ttu-id="34f92-231">**傳出 DDoS 和殭屍網路偵測**-目標雲端資源的攻擊的常見目標是 toouse hello 選計算能力的這些資源 tooexecute 其他攻擊。</span><span class="sxs-lookup"><span data-stu-id="34f92-231">**Outbound DDoS and Botnet Detection** - A common objective of attacks targeting cloud resources is toouse hello compute power of these resources tooexecute other attacks.</span></span>

-   <span data-ttu-id="34f92-232">**新的行為分析伺服器和 Vm-**一旦伺服器或虛擬機器遭到入侵，攻擊者時避免偵測，確保持續性，因此不可以用各種不同的技術 tooexecute 惡意程式碼在該系統上安全性控制。</span><span class="sxs-lookup"><span data-stu-id="34f92-232">**New Behavioral Analytics Servers and VMs -** Once a server or virtual machine is compromised, attackers employ a wide variety of techniques tooexecute malicious code on that system while avoiding detection, ensuring persistence, and obviating security controls.</span></span>

-   <span data-ttu-id="34f92-233">**Azure SQL Database 威脅偵測-** for Azure SQL Database，識別異常資料庫活動異常和潛在危險的威脅偵測嘗試 tooaccess 或利用資料庫。</span><span class="sxs-lookup"><span data-stu-id="34f92-233">**Azure SQL Database Threat Detection -** Threat Detection for Azure SQL Database, which identifies anomalous database activities indicating unusual and potentially harmful attempts tooaccess or exploit databases.</span></span>

### <a name="behavioral-analytics"></a><span data-ttu-id="34f92-234">行為分析</span><span class="sxs-lookup"><span data-stu-id="34f92-234">Behavioral analytics</span></span>

<span data-ttu-id="34f92-235">行為分析是一種技術，分析和比較資料 tooa 收集的已知的模式。</span><span class="sxs-lookup"><span data-stu-id="34f92-235">Behavioral analytics is a technique that analyzes and compares data tooa collection of known patterns.</span></span> <span data-ttu-id="34f92-236">不過，這些模式並非簡單的簽章。</span><span class="sxs-lookup"><span data-stu-id="34f92-236">However, these patterns are not simple signatures.</span></span> <span data-ttu-id="34f92-237">它們是透過套用的 toomassive 資料集的複雜的機器學習演算法決定。</span><span class="sxs-lookup"><span data-stu-id="34f92-237">They are determined through complex machine learning algorithms that are applied toomassive datasets.</span></span>

![行為分析](./media/azure-threat-detection/azure-threat-detection-fig11.jpg)


<span data-ttu-id="34f92-239">它們也能透過專業分析師仔細分析惡意行為來判定。</span><span class="sxs-lookup"><span data-stu-id="34f92-239">They are also determined through careful analysis of malicious behaviors by expert analysts.</span></span> <span data-ttu-id="34f92-240">Azure 資訊安全中心可以使用行為分析 tooidentify 洩漏資源，根據分析的虛擬機器記錄檔、 虛擬網路裝置記錄檔、 網狀架構的記錄檔、 損毀傾印和其他來源。</span><span class="sxs-lookup"><span data-stu-id="34f92-240">Azure Security Center can use behavioral analytics tooidentify compromised resources based on analysis of virtual machine logs, virtual network device logs, fabric logs, crash dumps, and other sources.</span></span>

<span data-ttu-id="34f92-241">此外，沒有與其他支援廣泛的行銷活動的辨識項的訊號 toocheck 相互關聯。</span><span class="sxs-lookup"><span data-stu-id="34f92-241">In addition, there is correlation with other signals toocheck for supporting evidence of a widespread campaign.</span></span> <span data-ttu-id="34f92-242">此相互關聯可協助建立洩露的指標與一致的 tooidentify 事件。</span><span class="sxs-lookup"><span data-stu-id="34f92-242">This correlation helps tooidentify events that are consistent with established indicators of compromise.</span></span>

<span data-ttu-id="34f92-243">部分範例包括：</span><span class="sxs-lookup"><span data-stu-id="34f92-243">Some examples include:</span></span>
-   <span data-ttu-id="34f92-244">**可疑的處理序執行：**攻擊者可以用數種技術 tooexecute 惡意軟體偵測。</span><span class="sxs-lookup"><span data-stu-id="34f92-244">**Suspicious process execution:** Attackers employ several techniques tooexecute malicious software without detection.</span></span> <span data-ttu-id="34f92-245">比方說，攻擊者可能會讓惡意程式碼 hello 合法的系統檔案相同的名稱，但將這些檔案放在替代位置，使用名稱，非常類似良性的檔案或遮罩 hello 的則為 true 的副檔名。</span><span class="sxs-lookup"><span data-stu-id="34f92-245">For example, an attacker might give malware hello same names as legitimate system files but place these files in an alternate location, use a name that is very like a benign file, or mask hello file’s true extension.</span></span> <span data-ttu-id="34f92-246">資訊安全中心模型的處理序行為 」 和 「 監視處理這類執行 toodetect 極端值。</span><span class="sxs-lookup"><span data-stu-id="34f92-246">Security Center models processes behaviors and monitors process executions toodetect outliers such as these.</span></span>

-   <span data-ttu-id="34f92-247">**隱藏惡意程式碼和入侵嘗試：**複雜的惡意程式碼可以避開傳統的反惡意程式碼產品永遠不會寫入 toodisk 或加密儲存在磁碟上的軟體元件。</span><span class="sxs-lookup"><span data-stu-id="34f92-247">**Hidden malware and exploitation attempts:** Sophisticated malware can evade traditional antimalware products by either never writing toodisk or encrypting software components stored on disk.</span></span> <span data-ttu-id="34f92-248">不過，這類惡意程式碼可以時偵測到使用記憶體分析 hello 惡意程式碼必須保留記憶體 toofunction 追蹤。</span><span class="sxs-lookup"><span data-stu-id="34f92-248">However, such malware can be detected using memory analysis, as hello malware must leave traces in memory toofunction.</span></span> <span data-ttu-id="34f92-249">軟體損毀，損毀傾印會擷取 hello hello 損毀時的記憶體部分。</span><span class="sxs-lookup"><span data-stu-id="34f92-249">When software crashes, a crash dump captures a portion of memory at hello time of hello crash.</span></span> <span data-ttu-id="34f92-250">藉由分析 hello 記憶體 hello 損毀傾印中的，Azure 資訊安全中心可以偵測技術軟體中使用 tooexploit 弱點，存取機密資料，並暗中保存內遭入侵的電腦而不會影響 hello 效能您的電腦。</span><span class="sxs-lookup"><span data-stu-id="34f92-250">By analyzing hello memory in hello crash dump, Azure Security Center can detect techniques used tooexploit vulnerabilities in software, access confidential data, and surreptitiously persist within a compromised machine without impacting hello performance of your machine.</span></span>

-   <span data-ttu-id="34f92-251">**橫向移動和內部探察：** toopersist 遭盜用的網路和找出/蒐集寶貴資料中，攻擊者通常會嘗試從入侵的 hello 此舉 toomove 內機器 tooothers hello 相同的網路。</span><span class="sxs-lookup"><span data-stu-id="34f92-251">**Lateral movement and internal reconnaissance:** toopersist in a compromised network and locate/harvest valuable data, attackers often attempt toomove laterally from hello compromised machine tooothers within hello same network.</span></span> <span data-ttu-id="34f92-252">資訊安全中心會監視程序，並登入活動 toodiscover 嘗試 tooexpand hello 在網路內，例如遠端命令執行、 網路探查和帳戶列舉的攻擊者的一席之地。</span><span class="sxs-lookup"><span data-stu-id="34f92-252">Security Center monitors process and login activities toodiscover attempts tooexpand an attacker’s foothold within hello network, such as remote command execution, network probing, and account enumeration.</span></span>

-   <span data-ttu-id="34f92-253">**惡意的 PowerShell 指令碼：** PowerShell 可以由攻擊者 tooexecute 惡意程式碼在目標虛擬機器上用於各種用途。</span><span class="sxs-lookup"><span data-stu-id="34f92-253">**Malicious PowerShell Scripts:** PowerShell can be used by attackers tooexecute malicious code on target virtual machines for a various purposes.</span></span> <span data-ttu-id="34f92-254">資訊安全中心會檢查 PowerShell 活動，以找到可疑活動的證明。</span><span class="sxs-lookup"><span data-stu-id="34f92-254">Security Center inspects PowerShell activity for evidence of suspicious activity.</span></span>

-   <span data-ttu-id="34f92-255">**傳出攻擊：**攻擊者通常目標雲端資源，以 hello 目標使用那些資源 toomount 其他攻擊。</span><span class="sxs-lookup"><span data-stu-id="34f92-255">**Outgoing attacks:** Attackers often target cloud resources with hello goal of using those resources toomount additional attacks.</span></span> <span data-ttu-id="34f92-256">遭盜用的虛擬機器，例如，可能使用的 toolaunch 暴力攻擊其他虛擬機器、 傳送垃圾郵件，或掃描開啟的連接埠與 hello 網際網路上的其他裝置。</span><span class="sxs-lookup"><span data-stu-id="34f92-256">Compromised virtual machines, for example, might be used toolaunch brute force attacks against other virtual machines, send SPAM, or scan open ports and other devices on hello Internet.</span></span> <span data-ttu-id="34f92-257">藉由套用機器學習 toonetwork 流量，資訊安全中心可以偵測何時輸出網路通訊超過 hello 範數。</span><span class="sxs-lookup"><span data-stu-id="34f92-257">By applying machine learning toonetwork traffic, Security Center can detect when outbound network communications exceed hello norm.</span></span> <span data-ttu-id="34f92-258">當 垃圾郵件、 資訊安全中心也與相互關聯不尋常的電子郵件流量從 Office 365 toodetermine 智慧 hello 郵件是否可能讓或 hello 的合法電子郵件行銷活動的結果。</span><span class="sxs-lookup"><span data-stu-id="34f92-258">When SPAM, Security Center also correlates unusual email traffic with intelligence from Office 365 toodetermine whether hello mail is likely nefarious or hello result of a legitimate email campaign.</span></span>

### <a name="anomaly-detection"></a><span data-ttu-id="34f92-259">異常偵測</span><span class="sxs-lookup"><span data-stu-id="34f92-259">Anomaly Detection</span></span>

<span data-ttu-id="34f92-260">Azure 資訊安全中心也會使用異常偵測 tooidentify 威脅。</span><span class="sxs-lookup"><span data-stu-id="34f92-260">Azure Security Center also uses anomaly detection tooidentify threats.</span></span> <span data-ttu-id="34f92-261">在對比 toobehavioral analytics 中 （這取決於衍生自大型資料集的已知模式），異常偵測更 」 個人化 」，將著重於特定 tooyour 部署的基準。</span><span class="sxs-lookup"><span data-stu-id="34f92-261">In contrast toobehavioral analytics (which depends on known patterns derived from large data sets), anomaly detection is more “personalized” and focuses on baselines that are specific tooyour deployments.</span></span> <span data-ttu-id="34f92-262">機器學習服務是套用的 toodetermine 一般活動，為您的部署，然後再規則便會產生的 toodefine 極端值條件可代表安全性事件。</span><span class="sxs-lookup"><span data-stu-id="34f92-262">Machine learning is applied toodetermine normal activity for your deployments and then rules are generated toodefine outlier conditions that could represent a security event.</span></span> <span data-ttu-id="34f92-263">範例如下：</span><span class="sxs-lookup"><span data-stu-id="34f92-263">Here’s an example:</span></span>

-   <span data-ttu-id="34f92-264">**輸入 RDP/SSH 暴力密碼破解攻擊**︰您的部署中可能包含每天都有許多登入的繁忙虛擬機器，以及有少量或任何登入的其他虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="34f92-264">**Inbound RDP/SSH brute force attacks:** Your deployments may have busy virtual machines with many logins each day and other virtual machines that have few or any logins.</span></span> <span data-ttu-id="34f92-265">Azure 資訊安全中心可以判斷這些虛擬機器的基準登入活動，並使用機器學習 toodefine 周圍 hello 正常的登入活動。</span><span class="sxs-lookup"><span data-stu-id="34f92-265">Azure Security Center can determine baseline login activity for these virtual machines and use machine learning toodefine around hello normal login activities.</span></span> <span data-ttu-id="34f92-266">如果沒有任何差異，與 hello 基準定義登入相關的特性，則可能會產生警示的。</span><span class="sxs-lookup"><span data-stu-id="34f92-266">If there is any discrepancy with hello baseline defined for login related characteristics, then an alert may be generated.</span></span> <span data-ttu-id="34f92-267">同樣地，機器學習服務會判斷何者值得關注。</span><span class="sxs-lookup"><span data-stu-id="34f92-267">Again, machine learning determines what is significant.</span></span>

### <a name="continuous-threat-intelligence-monitoring"></a><span data-ttu-id="34f92-268">連續威脅情報監視</span><span class="sxs-lookup"><span data-stu-id="34f92-268">Continuous Threat Intelligence Monitoring</span></span>

<span data-ttu-id="34f92-269">Azure 資訊安全中心的運作方式與安全性研究與資料科學團隊整個 hello world hello 威脅大環境中的變更持續監視。</span><span class="sxs-lookup"><span data-stu-id="34f92-269">Azure Security Center operates with security research and data science teams throughout hello world that continuously monitor for changes in hello threat landscape.</span></span> <span data-ttu-id="34f92-270">這包括下列 initiatives hello:</span><span class="sxs-lookup"><span data-stu-id="34f92-270">This includes hello following initiatives:</span></span>

-   <span data-ttu-id="34f92-271">**威脅情報監視**︰威脅情報包含關於現有或新興威脅的機制、指標、影響和可採取動作的建議。</span><span class="sxs-lookup"><span data-stu-id="34f92-271">**Threat intelligence monitoring:** Threat intelligence includes mechanisms, indicators, implications, and actionable advice about existing or emerging threats.</span></span> <span data-ttu-id="34f92-272">這項資訊會共用 hello 安全性社群中，而且 Microsoft 會持續監視 threat intelligence 摘要內部和外部來源。</span><span class="sxs-lookup"><span data-stu-id="34f92-272">This information is shared in hello security community and Microsoft continuously monitors threat intelligence feeds from internal and external sources.</span></span>

-   <span data-ttu-id="34f92-273">**訊號共用**︰共用和分析 Microsoft 的資訊安全小組對於各種雲端和內部部署服務、伺服器及用戶端端點裝置組合所提供的深入見解。</span><span class="sxs-lookup"><span data-stu-id="34f92-273">**Signal sharing:** Insights from security teams across Microsoft’s broad portfolio of cloud and on-premises services, servers, and client endpoint devices are shared and analyzed.</span></span>

-   <span data-ttu-id="34f92-274">**Microsoft 資訊安全專家**︰持續與擅長特殊資訊安全領域 (例如鑑識與 Web 攻擊偵測) 的 Microsoft 團隊攜手合作。</span><span class="sxs-lookup"><span data-stu-id="34f92-274">**Microsoft security specialists:** Ongoing engagement with teams across Microsoft that work in specialized security fields, like forensics and web attack detection.</span></span>

-   <span data-ttu-id="34f92-275">**偵測微調：**演算法會針對實際的客戶資料集來執行和安全性研究人員會使用客戶 toovalidate hello 結果。</span><span class="sxs-lookup"><span data-stu-id="34f92-275">**Detection tuning:** Algorithms are run against real customer data sets and security researchers work with customers toovalidate hello results.</span></span> <span data-ttu-id="34f92-276">True 和 false 肯定是使用的 toorefine 機器學習演算法。</span><span class="sxs-lookup"><span data-stu-id="34f92-276">True and false positives are used toorefine machine learning algorithms.</span></span>

<span data-ttu-id="34f92-277">這些合併的工作做為目標，在全新且改善了偵測，您可以立即獲益於-您 tootake 的任何動作。</span><span class="sxs-lookup"><span data-stu-id="34f92-277">These combined efforts culminate in new and improved detections, which you can benefit from instantly – there’s no action for you tootake.</span></span>

## <a name="advanced-threat-detection-features---other-azure-services"></a><span data-ttu-id="34f92-278">進階威脅偵測功能：其他 Azure 服務</span><span class="sxs-lookup"><span data-stu-id="34f92-278">Advanced Threat Detection Features - Other Azure Services</span></span>

### <a name="virtual-machine-microsoft-antimalware"></a><span data-ttu-id="34f92-279">虛擬機器︰Microsoft Antimalware</span><span class="sxs-lookup"><span data-stu-id="34f92-279">Virtual Machine: Microsoft Antimalware</span></span>

<span data-ttu-id="34f92-280">[Microsoft 反惡意程式碼](https://docs.microsoft.com/azure/security/azure-security-antimalware)Azure 為應用程式和租用戶環境的單一代理程式解決方案，設計 toorun hello 背景需要人為介入。</span><span class="sxs-lookup"><span data-stu-id="34f92-280">[Microsoft Antimalware](https://docs.microsoft.com/azure/security/azure-security-antimalware) for Azure is a single-agent solution for applications and tenant environments, designed toorun in hello background without human intervention.</span></span> <span data-ttu-id="34f92-281">您可以部署根據您的應用程式工作負載，與其中一個基本安全依預設的 hello 需求或進階自訂組態，包括監視反惡意程式碼的保護。</span><span class="sxs-lookup"><span data-stu-id="34f92-281">You can deploy protection based on hello needs of your application workloads, with either basic secure-by-default or advanced custom configuration, including antimalware monitoring.</span></span> <span data-ttu-id="34f92-282">Azure 的反惡意程式碼是適用於 Azure 虛擬機器的安全性選項，而且會自動安裝在所有的 Azure PaaS 虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="34f92-282">Azure antimalware is a security option for Azure Virtual Machines and is automatically installed on all Azure PaaS virtual machines.</span></span>

<span data-ttu-id="34f92-283">**Azure toodeploy 和啟用 Microsoft 反惡意程式碼應用程式的功能**</span><span class="sxs-lookup"><span data-stu-id="34f92-283">**Features of Azure toodeploy and enable Microsoft Antimalware for your applications**</span></span>

#### <a name="microsoft-antimalware-core-features"></a><span data-ttu-id="34f92-284">Microsoft Antimalware 核心功能</span><span class="sxs-lookup"><span data-stu-id="34f92-284">Microsoft Antimalware Core Features</span></span>

-   <span data-ttu-id="34f92-285">**即時保護-**監視雲端服務和虛擬機器 toodetect 和封鎖惡意程式碼執行的活動。</span><span class="sxs-lookup"><span data-stu-id="34f92-285">**Real-time protection -** monitors activity in Cloud Services and on Virtual Machines toodetect and block malware execution.</span></span>

-   <span data-ttu-id="34f92-286">**排程掃描-**目標掃描 toodetect 惡意程式碼，包括正在執行的程式會定期執行。</span><span class="sxs-lookup"><span data-stu-id="34f92-286">**Scheduled scanning -** periodically performs targeted scanning toodetect malware, including actively running programs.</span></span>

-   <span data-ttu-id="34f92-287">**惡意程式碼補救**：自動針對偵測到的惡意程式碼採取行動，例如，刪除或隔離惡意檔案，以及清除惡意的登錄項目。</span><span class="sxs-lookup"><span data-stu-id="34f92-287">**Malware remediation -** automatically takes action on detected malware, such as deleting or quarantining malicious files and cleaning up malicious registry entries.</span></span>

-   <span data-ttu-id="34f92-288">**簽章更新-**自動安裝 hello 最新保護 （防毒定義） 的簽章 tooensure 保護是最新的預先決定的頻率。</span><span class="sxs-lookup"><span data-stu-id="34f92-288">**Signature updates -** automatically installs hello latest protection signatures (virus definitions) tooensure protection is up-to-date on a pre-determined frequency.</span></span>

-   <span data-ttu-id="34f92-289">**反惡意程式碼引擎的更新-**自動更新 hello Microsoft 反惡意程式碼引擎。</span><span class="sxs-lookup"><span data-stu-id="34f92-289">**Antimalware Engine updates -** automatically updates hello Microsoft Antimalware engine.</span></span>

-   <span data-ttu-id="34f92-290">**反惡意程式碼的平台更新 –**自動更新 hello Microsoft 反惡意程式碼的平台。</span><span class="sxs-lookup"><span data-stu-id="34f92-290">**Antimalware Platform updates –** automatically updates hello Microsoft Antimalware platform.</span></span>

-   <span data-ttu-id="34f92-291">**作用中保護-**遙測中繼資料會報告有關偵測到的威脅和可疑資源 tooMicrosoft Azure tooensure 快速回應 toohello 進化的威脅架構之下，以及啟用透過即時同步的簽章傳遞hello Microsoft Active Protection 系統 (MAPS)。</span><span class="sxs-lookup"><span data-stu-id="34f92-291">**Active protection -** reports telemetry metadata about detected threats and suspicious resources tooMicrosoft Azure tooensure rapid response toohello evolving threat landscape, and enabling real-time synchronous signature delivery through hello Microsoft Active Protection System (MAPS).</span></span>

-   <span data-ttu-id="34f92-292">**範例報表-**提供和報表範例 toohello Microsoft 反惡意程式碼服務 toohelp 精簡 hello 服務和啟用疑難排解。</span><span class="sxs-lookup"><span data-stu-id="34f92-292">**Samples reporting -** provides and reports samples toohello Microsoft Antimalware service toohelp refine hello service and enable troubleshooting.</span></span>

-   <span data-ttu-id="34f92-293">**排除項目 –**可讓應用程式和服務系統管理員 tooconfigure 某些檔案時，處理程序，以及磁碟機 tooexclude，其保護和效能及/或其他原因而進行掃描。</span><span class="sxs-lookup"><span data-stu-id="34f92-293">**Exclusions –** allows application and service administrators tooconfigure certain files, processes, and drives tooexclude them from protection and scanning for performance and/or other reasons.</span></span>

-   <span data-ttu-id="34f92-294">**反惡意程式碼的事件集合-** hello 反惡意程式碼服務健全狀況、 可疑活動，以及在 hello 作業系統事件記錄檔中所採取的修復動作記錄，並會加以收集到 hello 客戶的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="34f92-294">**Antimalware event collection -** records hello antimalware service health, suspicious activities, and remediation actions taken in hello operating system event log and collects them into hello customer’s Azure Storage account.</span></span>

### <a name="azure-sql-database-threat-detection"></a><span data-ttu-id="34f92-295">Azure SQL Database 威脅偵測</span><span class="sxs-lookup"><span data-stu-id="34f92-295">Azure SQL Database Threat Detection</span></span>

<span data-ttu-id="34f92-296">[Azure SQL Database 威脅偵測](https://azure.microsoft.com/blog/azure-sql-database-threat-detection-your-built-in-security-expert/)是 hello Azure SQL Database 服務內建的新安全性智慧功能。</span><span class="sxs-lookup"><span data-stu-id="34f92-296">[Azure SQL Database Threat Detection](https://azure.microsoft.com/blog/azure-sql-database-threat-detection-your-built-in-security-expert/) is a new security intelligence feature built into hello Azure SQL Database service.</span></span> <span data-ttu-id="34f92-297">解決 hello 時鐘 toolearn，設定檔，並偵測的異常資料庫活動、 Azure SQL Database 威脅偵測識別潛在的威脅 toohello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="34f92-297">Working around hello clock toolearn, profile and detect anomalous database activities, Azure SQL Database Threat Detection identifies potential threats toohello database.</span></span>

<span data-ttu-id="34f92-298">資訊安全人員或其他指定的系統管理員可以在發生可疑的資料庫活動時立即取得通知。</span><span class="sxs-lookup"><span data-stu-id="34f92-298">Security officers or other designated administrators can get an immediate notification about suspicious database activities as they occur.</span></span> <span data-ttu-id="34f92-299">每個通知提供 hello 可疑活動的詳細資料，並建議 toofurther 調查並降低 hello 威脅的方式。</span><span class="sxs-lookup"><span data-stu-id="34f92-299">Each notification provides details of hello suspicious activity and recommends how toofurther investigate and mitigate hello threat.</span></span>

<span data-ttu-id="34f92-300">目前，Azure SQL Database 威脅偵測會偵測潛在的弱點與 SQL 插入式攻擊，以及異常的資料庫存取模式。</span><span class="sxs-lookup"><span data-stu-id="34f92-300">Currently, Azure SQL Database Threat Detection detects potential vulnerabilities and SQL injection attacks, and anomalous database access patterns.</span></span>

<span data-ttu-id="34f92-301">在收到威脅偵測電子郵件通知時，使用者即無法 toonavigate 和檢視 hello 相關的稽核記錄 hello mail 開啟稽核檢視器和/或預先設定顯示 hello 相關的稽核的稽核 Excel 範本中使用 hello 深層連結周圍 hello 事件時間的 hello 可疑根據 toohello 下列記錄：</span><span class="sxs-lookup"><span data-stu-id="34f92-301">Upon receiving threat detection email notification, users are able toonavigate and view hello relevant audit records using hello deep link in hello mail that opens an audit viewer and/or preconfigured auditing Excel template that shows hello relevant audit records around hello time of hello suspicious event according toohello following:</span></span>
-   <span data-ttu-id="34f92-302">Hello/具有資料庫伺服器 hello 的異常資料庫活動的稽核儲存體</span><span class="sxs-lookup"><span data-stu-id="34f92-302">Audit storage for hello database/server with hello anomalous database activities</span></span>

-   <span data-ttu-id="34f92-303">相關的稽核儲存體資料表所使用的 hello 時間 hello 事件 toowrite 稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="34f92-303">Relevant audit storage table that was used at hello time of hello event toowrite audit log</span></span>

-   <span data-ttu-id="34f92-304">稽核記錄的 hello hello 事件，就會發生因為下列小時。</span><span class="sxs-lookup"><span data-stu-id="34f92-304">Audit records of hello following hour since hello event occurs.</span></span>

-   <span data-ttu-id="34f92-305">Hello 事件時間的 hello （某些偵測選擇性） 在稽核記錄類似的事件識別碼</span><span class="sxs-lookup"><span data-stu-id="34f92-305">Audit records with similar event ID at hello time of hello event (optional for some detectors)</span></span>

<span data-ttu-id="34f92-306">SQL Database 威脅偵測器會使用 hello 遵循偵測方法的其中一個：</span><span class="sxs-lookup"><span data-stu-id="34f92-306">SQL Database Threat Detectors use one of hello following detection methodologies:</span></span>

-   <span data-ttu-id="34f92-307">**決定性偵測 –** hello SQL 用戶端查詢，以符合已知的攻擊中偵測到可疑的模式 （規則為基礎）。</span><span class="sxs-lookup"><span data-stu-id="34f92-307">**Deterministic Detection –** detects suspicious patterns (rules based) in hello SQL client queries that match known attacks.</span></span> <span data-ttu-id="34f92-308">這種方法具有高偵測和低誤判，不過受限於涵蓋範圍，因為它的 「 不可部分完成的偵測 「 hello 類別目錄內。</span><span class="sxs-lookup"><span data-stu-id="34f92-308">This methodology has high detection and low false positive, however limited coverage because it falls within hello category of “atomic detections”.</span></span>

-   <span data-ttu-id="34f92-309">**Behavioural 偵測 –**瑕疵異常的活動，也就是找不到在 hello 過去 30 天的 hello 資料庫異常行為。</span><span class="sxs-lookup"><span data-stu-id="34f92-309">**Behavioural Detection –** defects anomalous activity, which is abnormal behavior for hello database that was not seen during hello last 30 days.</span></span>  <span data-ttu-id="34f92-310">SQL 用戶端異常活動的範例可以是失敗的登入查詢及大量解壓縮的資料，不尋常的標準查詢不熟悉的 IP 位址使用 tooaccess hello 資料庫的增量</span><span class="sxs-lookup"><span data-stu-id="34f92-310">An example for SQL client anomalous activity can be a spike of failed logins/queries, high volume of data being extracted, unusual canonical queries, and unfamiliar IP addresses used tooaccess hello database</span></span>

### <a name="application-gateway-web-application-firewall"></a><span data-ttu-id="34f92-311">應用程式閘道 Web 應用程式防火牆</span><span class="sxs-lookup"><span data-stu-id="34f92-311">Application Gateway Web Application Firewall</span></span>

<span data-ttu-id="34f92-312">[Web 應用程式防火牆](https://docs.microsoft.com/azure/app-service-web/app-service-app-service-environment-web-application-firewall)是一項功能[Azure 應用程式閘道](https://docs.microsoft.com/azure/application-gateway/application-gateway-webapplicationfirewall-overview)tooweb 應用程式使用標準的應用程式閘道提供保護[應用程式傳遞控制](https://kemptechnologies.com/in/application-delivery-controllers)函式。</span><span class="sxs-lookup"><span data-stu-id="34f92-312">[Web Application Firewall](https://docs.microsoft.com/azure/app-service-web/app-service-app-service-environment-web-application-firewall) is a feature of [Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-webapplicationfirewall-overview) that provides protection tooweb applications that use application gateway for standard [Application Delivery Control](https://kemptechnologies.com/in/application-delivery-controllers) functions.</span></span> <span data-ttu-id="34f92-313">Web 應用程式防火牆會保護它們對大部分的 hello [OWASP 前 10 個常見的 web 弱點](https://www.owasp.org/index.php/Top_10_2010-Main)</span><span class="sxs-lookup"><span data-stu-id="34f92-313">Web application firewall does this by protecting them against most of hello [OWASP top 10 common web vulnerabilities](https://www.owasp.org/index.php/Top_10_2010-Main)</span></span>

![應用程式閘道 Web 應用程式防火牆](./media/azure-threat-detection/azure-threat-detection-fig13.png)

-   <span data-ttu-id="34f92-315">SQL 插入式攻擊保護</span><span class="sxs-lookup"><span data-stu-id="34f92-315">SQL injection protection</span></span>

-   <span data-ttu-id="34f92-316">跨網站指令碼保護</span><span class="sxs-lookup"><span data-stu-id="34f92-316">Cross site scripting protection</span></span>

-   <span data-ttu-id="34f92-317">常見 Web 攻擊保護，例如命令插入式攻擊、HTTP 要求走私、HTTP 回應分割和遠端檔案包含攻擊</span><span class="sxs-lookup"><span data-stu-id="34f92-317">Common Web Attacks Protection such as command injection, HTTP request smuggling, HTTP response splitting, and remote file inclusion attack</span></span>

-   <span data-ttu-id="34f92-318">防範 HTTP 通訊協定違規</span><span class="sxs-lookup"><span data-stu-id="34f92-318">Protection against HTTP protocol violations</span></span>

-   <span data-ttu-id="34f92-319">防範 HTTP 通訊協定異常行為，例如遺漏主機使用者代理程式和接受標頭</span><span class="sxs-lookup"><span data-stu-id="34f92-319">Protection against HTTP protocol anomalies such as missing host user-agent and accept headers</span></span>

-   <span data-ttu-id="34f92-320">防範 Bot、編目程式和掃描器</span><span class="sxs-lookup"><span data-stu-id="34f92-320">Prevention against bots, crawlers, and scanners</span></span>

-   <span data-ttu-id="34f92-321">偵測一般應用程式錯誤組態 (也就是 Apache、IIS 等)</span><span class="sxs-lookup"><span data-stu-id="34f92-321">Detection of common application misconfigurations (that is, Apache, IIS, etc.)</span></span>

<span data-ttu-id="34f92-322">在應用程式閘道設定 WAF 提供下列好處 tooyou hello:</span><span class="sxs-lookup"><span data-stu-id="34f92-322">Configuring WAF at Application Gateway provides hello following benefit tooyou:</span></span>

-   <span data-ttu-id="34f92-323">保護您的 web 應用程式 web 的弱點可能會與沒有修改 toobackend 程式碼的攻擊。</span><span class="sxs-lookup"><span data-stu-id="34f92-323">Protect your web application from web vulnerabilities and attacks without modification toobackend code.</span></span>

-   <span data-ttu-id="34f92-324">保護多個 web 應用程式閘道後方相同時間 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="34f92-324">Protect multiple web applications at hello same time behind an application gateway.</span></span> <span data-ttu-id="34f92-325">應用程式閘道支援所有會保護 web 攻擊，單一閘道後方 too20 網站上裝載。</span><span class="sxs-lookup"><span data-stu-id="34f92-325">Application gateway supports hosting up too20 websites behind a single gateway that could all be protected against web attacks.</span></span>

-   <span data-ttu-id="34f92-326">使用應用程式閘道 WAF 記錄所產生的即時報告，監視 Web 應用程式對抗攻擊。</span><span class="sxs-lookup"><span data-stu-id="34f92-326">Monitor your web application against attacks using real-time report generated by application gateway WAF logs.</span></span>

-   <span data-ttu-id="34f92-327">特定相容性的控制項需要所有的網際網路對向結束點 toobe 受 WAF 方案。</span><span class="sxs-lookup"><span data-stu-id="34f92-327">Certain compliance controls require all internet facing end points toobe protected by a WAF solution.</span></span> <span data-ttu-id="34f92-328">使用已啟用 WAF 的應用程式閘道，您就可以符合這些法務遵循需求。</span><span class="sxs-lookup"><span data-stu-id="34f92-328">By using application gateway with WAF enabled, you can meet these compliance requirements.</span></span>

### <a name="anomaly-detection--an-api-built-with-azure-machine-learning"></a><span data-ttu-id="34f92-329">異常偵測：使用 Azure Machine Learning 建置的 API</span><span class="sxs-lookup"><span data-stu-id="34f92-329">Anomaly Detection – an API built with Azure Machine Learning</span></span>

<span data-ttu-id="34f92-330">異常偵測是使用 Azure Machine Learning 建置的 API，在時間序列資料中偵測不同類型的異常模式時非常有用。</span><span class="sxs-lookup"><span data-stu-id="34f92-330">Anomaly Detection is an API built with Azure Machine Learning that is useful for detecting different types of anomalous patterns in your time series data.</span></span> <span data-ttu-id="34f92-331">hello API 指派分數 tooeach 資料點 hello 時間序列，它可以用來產生警示，異常監視透過儀表板，或使用票證系統進行連接。</span><span class="sxs-lookup"><span data-stu-id="34f92-331">hello API assigns an anomaly score tooeach data point in hello time series, which can be used for generating alerts, monitoring through dashboards or connecting with your ticketing systems.</span></span>

<span data-ttu-id="34f92-332">hello[異常偵測 API](https://docs.microsoft.com/azure/machine-learning/machine-learning-apps-anomaly-detection-api)可以偵測到下列的異常類型對時間序列資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="34f92-332">hello [Anomaly Detection API](https://docs.microsoft.com/azure/machine-learning/machine-learning-apps-anomaly-detection-api) can detect hello following types of anomalies on time series data:</span></span>

-   <span data-ttu-id="34f92-333">**升高和畫 Dip:**比方說，監視 hello 登入失敗 tooa 服務數目或簽出的電子商務網站中的數字、 不尋常的尖峰或 dip 無法指出安全性攻擊或服務中斷的情況。</span><span class="sxs-lookup"><span data-stu-id="34f92-333">**Spikes and Dips:** For example, when monitoring hello number of login failures tooa service or number of checkouts in an e-commerce site, unusual spikes or dips could indicate security attacks or service disruptions.</span></span>

-   <span data-ttu-id="34f92-334">**上升和下滑趨勢**：例如，監視計算期間的記憶體使用量時，縮小可用的記憶體大小表示可能發生記憶體流失；監視服務佇列長度時，持續上升的趨勢可能代表發生基本的軟體問題。</span><span class="sxs-lookup"><span data-stu-id="34f92-334">**Positive and negative trends:** When monitoring memory usage in computing, for instance, shrinking free memory size is indicative of a potential memory leak; when monitoring service queue length, a persistent upward trend may indicate an underlying software issue.</span></span>

-   <span data-ttu-id="34f92-335">**層級變更，以及動態值的範圍中的變更：**比方說，層級中服務的延遲之後變更的服務升級或之後升級會有趣 toomonitor 較低層級的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="34f92-335">**Level changes and changes in dynamic range of values:** For example, level changes in latencies of a service after a service upgrade or lower levels of exceptions after upgrade can be interesting toomonitor.</span></span>

<span data-ttu-id="34f92-336">hello 機器學習型應用程式開發介面可讓：</span><span class="sxs-lookup"><span data-stu-id="34f92-336">hello machine learning based API enables:</span></span>

-   <span data-ttu-id="34f92-337">**彈性和強大偵測：** hello 異常偵測模型讓使用者 tooconfigure 敏感度設定，並偵測異常行為在季節性和非季節性的資料集之間。</span><span class="sxs-lookup"><span data-stu-id="34f92-337">**Flexible and robust detection:** hello anomaly detection models allow users tooconfigure sensitivity settings and detect anomalies among seasonal and non-seasonal data sets.</span></span> <span data-ttu-id="34f92-338">使用者可以較不調整 hello 異常偵測模型 toomake hello 偵測應用程式開發介面，或更為敏感的相應 tootheir 需求。</span><span class="sxs-lookup"><span data-stu-id="34f92-338">Users can adjust hello anomaly detection model toomake hello detection API less or more sensitive according tootheir needs.</span></span> <span data-ttu-id="34f92-339">這表示偵測 hello 資料與不季節性模式中的較少或多個顯示異常狀況。</span><span class="sxs-lookup"><span data-stu-id="34f92-339">This would mean detecting hello less or more visible anomalies in data with and without seasonal patterns.</span></span>

-   <span data-ttu-id="34f92-340">**可擴充且適時偵測：** hello 傳統方式使用存在專家定義域知識所設定的閾值監視會以動態方式變更資料集的成本高同時不可擴充 toomillions。</span><span class="sxs-lookup"><span data-stu-id="34f92-340">**Scalable and timely detection:** hello traditional way of monitoring with present thresholds set by experts' domain knowledge are costly and not scalable toomillions of dynamically changing data sets.</span></span> <span data-ttu-id="34f92-341">學到此應用程式開發介面中的 hello 異常偵測模型，模型將自動調整歷程記錄和即時資料。</span><span class="sxs-lookup"><span data-stu-id="34f92-341">hello anomaly detection models in this API are learned and models are tuned automatically from both historical and real-time data.</span></span>

-   <span data-ttu-id="34f92-342">**主動且可採取動作的偵測**：緩慢的趨勢和層級變更偵測可應用於早期異常偵測。</span><span class="sxs-lookup"><span data-stu-id="34f92-342">**Proactive and actionable detection:** Slow trend and level change detection can be applied for early anomaly detection.</span></span> <span data-ttu-id="34f92-343">早期 hello 偵測到異常訊號可以使用的 toodirect 人類 tooinvestigate 和處理 hello 問題區域。</span><span class="sxs-lookup"><span data-stu-id="34f92-343">hello early abnormal signals detected can be used toodirect humans tooinvestigate and act on hello problem areas.</span></span>  <span data-ttu-id="34f92-344">此外，還可以在此異常偵測 API 服務之上，開發根本原因分析模型和警示工具。</span><span class="sxs-lookup"><span data-stu-id="34f92-344">In addition, root cause analysis models and alerting tools can be developed on top of this anomaly detection API service.</span></span>

<span data-ttu-id="34f92-345">hello 異常偵測應用程式開發介面是各種不同的案例，就如同服務健全狀況和 KPI 監視 IoT、 效能監視和網路流量監視效能和效率解決方案。</span><span class="sxs-lookup"><span data-stu-id="34f92-345">hello anomaly detection API is an effective and efficient solution for a wide range of scenarios like service health & KPI monitoring, IoT, performance monitoring, and network traffic monitoring.</span></span> <span data-ttu-id="34f92-346">以下提供一些常見案例，此 API 在這類案例中非常實用：</span><span class="sxs-lookup"><span data-stu-id="34f92-346">Here are some popular scenarios where this API can be useful:</span></span>
- <span data-ttu-id="34f92-347">IT 部門需要及時的工具 tootrack 事件、 錯誤代碼、 使用量記錄和效能 （CPU、 記憶體等）。</span><span class="sxs-lookup"><span data-stu-id="34f92-347">IT departments need tools tootrack events, error code, usage log, and performance (CPU, Memory and so on) in a timely manner.</span></span>

-   <span data-ttu-id="34f92-348">線上商務網站想 tootrack 客戶活動、 網頁檢視中，按一下、 等等。</span><span class="sxs-lookup"><span data-stu-id="34f92-348">Online commerce sites want tootrack customer activities, page views, clicks, and so on.</span></span>

-   <span data-ttu-id="34f92-349">公用程式的公司都想 tootrack 耗用量上限、 汽油、 電力，以及其他資源。</span><span class="sxs-lookup"><span data-stu-id="34f92-349">Utility companies want tootrack consumption of water, gas, electricity, and other resources.</span></span>

-   <span data-ttu-id="34f92-350">設備/建置管理服務想 toomonitor 溫度、 溼氣、 流量，等等。</span><span class="sxs-lookup"><span data-stu-id="34f92-350">Facility/Building management services want toomonitor temperature, moisture, traffic, and so on.</span></span>

-   <span data-ttu-id="34f92-351">IoT/製造商想要在時間序列 toomonitor toouse 感應器資料工作流程、 品質，等等。</span><span class="sxs-lookup"><span data-stu-id="34f92-351">IoT/manufacturers want toouse sensor data in time series toomonitor work flow, quality, and so on.</span></span>

-   <span data-ttu-id="34f92-352">服務提供者，例如撥接中心需要 toomonitor 服務要求趨勢，事件的磁碟區，等候佇列長度，依此類推。</span><span class="sxs-lookup"><span data-stu-id="34f92-352">Service providers, such as call centers need toomonitor service demand trend, incident volume, wait queue length and so on.</span></span>

-   <span data-ttu-id="34f92-353">商務分析群組想 toomonitor 商務 Kpi （例如銷售的磁碟區，客戶 sentiments，定價） 即時異常移動。</span><span class="sxs-lookup"><span data-stu-id="34f92-353">Business analytics groups want toomonitor business KPIs' (such as sales volume, customer sentiments, pricing) abnormal movement in real time.</span></span>

### <a name="cloud-app-security"></a><span data-ttu-id="34f92-354">Cloud App Security</span><span class="sxs-lookup"><span data-stu-id="34f92-354">Cloud App Security</span></span>

<span data-ttu-id="34f92-355">[Cloud App Security](https://docs.microsoft.com/cloud-app-security/what-is-cloud-app-security)是 hello Microsoft Cloud Security 堆疊的重要元件。</span><span class="sxs-lookup"><span data-stu-id="34f92-355">[Cloud App Security](https://docs.microsoft.com/cloud-app-security/what-is-cloud-app-security) is a critical component of hello Microsoft Cloud Security stack.</span></span> <span data-ttu-id="34f92-356">它是全方位的解決方案，可協助您的組織，當您移動 tootake 充分善用 hello 承諾的雲端應用程式，但讓您控制，透過改良的活動可見度。</span><span class="sxs-lookup"><span data-stu-id="34f92-356">It's a comprehensive solution that can help your organization as you move tootake full advantage of hello promise of cloud applications, but keep you in control, through improved visibility into activity.</span></span> <span data-ttu-id="34f92-357">此外，它也有助於提高 hello 保護重要資料的所有雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="34f92-357">It also helps increase hello protection of critical data across cloud applications.</span></span>

<span data-ttu-id="34f92-358">使用工具，協助找出陰影 IT、 評估風險、 強制執行原則、 調查活動，並停止威脅，您的組織更安全地移 toohello 雲端同時保有重要資料的控制項。</span><span class="sxs-lookup"><span data-stu-id="34f92-358">With tools that help uncover shadow IT, assess risk, enforce policies, investigate activities, and stop threats, your organization can more safely move toohello cloud while maintaining control of critical data.</span></span>

<table style="width:100%">
 <tr>
   <td><span data-ttu-id="34f92-359">探索</span><span class="sxs-lookup"><span data-stu-id="34f92-359">Discover</span></span></td>
   <td><span data-ttu-id="34f92-360">利用 Cloud App Security 來揭露影子 IT。</span><span class="sxs-lookup"><span data-stu-id="34f92-360">Uncover shadow IT with Cloud App Security.</span></span> <span data-ttu-id="34f92-361">藉由探索雲端環境中的應用程式、活動、使用者、資料和檔案，來取得可見度。</span><span class="sxs-lookup"><span data-stu-id="34f92-361">Gain visibility by discovering apps, activities, users, data, and files in your cloud environment.</span></span> <span data-ttu-id="34f92-362">探索已連接的第三方應用程式 tooyour 雲端。</span><span class="sxs-lookup"><span data-stu-id="34f92-362">Discover third-party apps that are connected tooyour cloud.</span></span></td>
 </tr>
 <tr>
   <td><span data-ttu-id="34f92-363">調查</span><span class="sxs-lookup"><span data-stu-id="34f92-363">Investigate</span></span></td>
   <td><span data-ttu-id="34f92-364">調查雲端應用程式使用雲端鑑識調查工具 toodeep 探討至有風險的應用程式、 特定的使用者及網路中的檔案。</span><span class="sxs-lookup"><span data-stu-id="34f92-364">Investigate your cloud apps by using cloud forensics tools toodeep-dive into risky apps, specific users, and files in your network.</span></span> <span data-ttu-id="34f92-365">找 hello 資料從雲端收集模式。</span><span class="sxs-lookup"><span data-stu-id="34f92-365">Find patterns in hello data collected from your cloud.</span></span> <span data-ttu-id="34f92-366">產生報表 toomonitor 您的雲端。</span><span class="sxs-lookup"><span data-stu-id="34f92-366">Generate reports toomonitor your cloud.</span></span></td>

 </tr>
 <tr>
   <td><span data-ttu-id="34f92-367">控制</span><span class="sxs-lookup"><span data-stu-id="34f92-367">Control</span></span></td>
   <td><span data-ttu-id="34f92-368">Tooachieve 充分控制網路雲端流量設定原則和警示來降低風險。</span><span class="sxs-lookup"><span data-stu-id="34f92-368">Mitigate risk by setting policies and alerts tooachieve maximum control over network cloud traffic.</span></span> <span data-ttu-id="34f92-369">使用 Cloud App Security toomigrate 您使用者 toosafe，保障的雲端應用程式的替代方案。</span><span class="sxs-lookup"><span data-stu-id="34f92-369">Use Cloud App Security toomigrate your users toosafe, sanctioned cloud app alternatives.</span></span></td>

 </tr>
 <tr>
   <td><span data-ttu-id="34f92-370">Protect</span><span class="sxs-lookup"><span data-stu-id="34f92-370">Protect</span></span></td>
   <td><span data-ttu-id="34f92-371">使用 Cloud App Security toosanction 或禁止的應用程式、 強制執行資料外洩防護、 控制 」 權限和共用，並產生自訂報告和警示。</span><span class="sxs-lookup"><span data-stu-id="34f92-371">Use Cloud App Security toosanction or prohibit applications, enforce data loss prevention, control permissions and sharing, and generate custom reports and alerts.</span></span></td>

 </tr>
 <tr>
   <td><span data-ttu-id="34f92-372">控制</span><span class="sxs-lookup"><span data-stu-id="34f92-372">Control</span></span></td>
   <td><span data-ttu-id="34f92-373">Tooachieve 充分控制網路雲端流量設定原則和警示來降低風險。</span><span class="sxs-lookup"><span data-stu-id="34f92-373">Mitigate risk by setting policies and alerts tooachieve maximum control over network cloud traffic.</span></span> <span data-ttu-id="34f92-374">使用 Cloud App Security toomigrate 您使用者 toosafe，保障的雲端應用程式的替代方案。</span><span class="sxs-lookup"><span data-stu-id="34f92-374">Use Cloud App Security toomigrate your users toosafe, sanctioned cloud app alternatives.</span></span></td>

 </tr>
</table>


![Cloud App Security](./media/azure-threat-detection/azure-threat-detection-fig14.png)

<span data-ttu-id="34f92-376">Cloud App Security 會透過下列方式來整合您雲端的可見性</span><span class="sxs-lookup"><span data-stu-id="34f92-376">Cloud App Security integrates visibility with your cloud by</span></span>

-   <span data-ttu-id="34f92-377">使用 Cloud Discovery toomap、 找出您的雲端環境並 hello 您的組織使用的雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="34f92-377">Using Cloud Discovery toomap and identify your cloud environment and hello cloud apps your organization is using.</span></span>


-   <span data-ttu-id="34f92-378">批准和禁止您雲端中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="34f92-378">Sanctioning and prohibiting apps in your cloud.</span></span>



-   <span data-ttu-id="34f92-379">使用易於部署的應用程式連接器，利用提供者 API 來取得您所連接之應用程式的可見度和控管。</span><span class="sxs-lookup"><span data-stu-id="34f92-379">Using easy-to-deploy app connectors that take advantage of provider APIs, for visibility and governance of apps that you connect to.</span></span>

-   <span data-ttu-id="34f92-380">透過設定，接著持續微調原則，協助您持續進行控制。</span><span class="sxs-lookup"><span data-stu-id="34f92-380">Helping you have continuous control by setting, and then continually fine-tuning, policies.</span></span>

<span data-ttu-id="34f92-381">在從這些來源收集資料，Cloud App Security 會在 hello 資料中執行複雜的分析。</span><span class="sxs-lookup"><span data-stu-id="34f92-381">On collecting data from these sources, Cloud App Security runs sophisticated analysis on hello data.</span></span> <span data-ttu-id="34f92-382">立即 tooanomalous 活動會提醒您，並讓您深入掌握雲端環境。</span><span class="sxs-lookup"><span data-stu-id="34f92-382">It immediately alerts you tooanomalous activities, and gives you deep visibility into your cloud environment.</span></span> <span data-ttu-id="34f92-383">您可以在 Cloud App Security 中設定的原則，並使用它 tooprotect 雲端環境中的所有項目。</span><span class="sxs-lookup"><span data-stu-id="34f92-383">You can configure a policy in Cloud App Security and use it tooprotect everything in your cloud environment.</span></span>

## <a name="third-party-atd-capabilities-through-azure-marketplace"></a><span data-ttu-id="34f92-384">透過 Azure Marketplace 提供的協力廠商 ATD 功能</span><span class="sxs-lookup"><span data-stu-id="34f92-384">Third-party ATD capabilities through Azure Marketplace</span></span>

### <a name="web-application-firewall"></a><span data-ttu-id="34f92-385">Web 應用程式防火牆</span><span class="sxs-lookup"><span data-stu-id="34f92-385">Web Application Firewall</span></span>

<span data-ttu-id="34f92-386">Web 應用程式防火牆會檢查輸入的 Web 流量和並封鎖 SQL 插入、跨網站指令碼、惡意程式碼上傳和應用程式 DDoS，以及目標為您 Web 應用程式的其他攻擊。</span><span class="sxs-lookup"><span data-stu-id="34f92-386">Web Application Firewall inspects inbound web traffic and blocks SQL injections, Cross-Site Scripting, malware uploads & application DDoS and other attacks targeted at your web applications.</span></span> <span data-ttu-id="34f92-387">它也會檢驗 hello 回應 hello 後端 web 伺服器中的資料遺失防護 (DLP)。</span><span class="sxs-lookup"><span data-stu-id="34f92-387">It also inspects hello responses from hello back-end web servers for Data Loss Prevention (DLP).</span></span> <span data-ttu-id="34f92-388">hello 整合式的存取控制引擎可讓系統管理員 toocreate 細微的存取控制原則驗證、 授權和帳戶處理 (AAA)，提供增強式驗證的組織和使用者控制項。</span><span class="sxs-lookup"><span data-stu-id="34f92-388">hello integrated access control engine enables administrators toocreate granular access control policies for Authentication, Authorization & Accounting (AAA), which gives organizations strong authentication and user control.</span></span>

<span data-ttu-id="34f92-389">**重點摘要：**</span><span class="sxs-lookup"><span data-stu-id="34f92-389">**Highlights:**</span></span>
-   <span data-ttu-id="34f92-390">偵測並封鎖 SQL 插入、跨網站指令碼、惡意程式碼上傳、應用程式 DDoS 或針對您應用程式的任何其他攻擊。</span><span class="sxs-lookup"><span data-stu-id="34f92-390">Detects and blocks SQL injections, Cross-Site Scripting, malware uploads, application DDoS, or any other attacks against your application.</span></span>

-   <span data-ttu-id="34f92-391">驗證和存取控制。</span><span class="sxs-lookup"><span data-stu-id="34f92-391">Authentication and access control.</span></span>

-   <span data-ttu-id="34f92-392">掃描傳出流量 toodetect 敏感性資料，並可以加上遮罩或封鎖 hello 資訊外洩。</span><span class="sxs-lookup"><span data-stu-id="34f92-392">Scans outbound traffic toodetect sensitive data and can mask or block hello information from being leaked out.</span></span>

-   <span data-ttu-id="34f92-393">加速使用功能，例如快取、 壓縮和其他流量最佳化的 web 應用程式內容的 hello 傳遞。</span><span class="sxs-lookup"><span data-stu-id="34f92-393">Accelerates hello delivery of web application contents, using capabilities such as caching, compression, and other traffic optimizations.</span></span>

<span data-ttu-id="34f92-394">以下是 Azure Market Place 中可用的 Web 應用程式防火牆範例：</span><span class="sxs-lookup"><span data-stu-id="34f92-394">Following are example of Web Application firewalls available in Azure Market Place:</span></span>

[<span data-ttu-id="34f92-395">Barracuda Web 應用程式防火牆、 虛擬 Web 應用程式防火牆 Brocade (Brocade vWAF)、 Imperva SecureSphere 和 hello ThreatSTOP IP 防火牆。</span><span class="sxs-lookup"><span data-stu-id="34f92-395">Barracuda Web Application Firewall, Brocade Virtual Web Application Firewall (Brocade vWAF), Imperva SecureSphere & hello ThreatSTOP IP Firewall.</span></span>](https://azure.microsoft.com/marketplace/partners/brocade_communications/brocade-virtual-web-application-firewall-templatevtmcluster/)

## <a name="next-steps"></a><span data-ttu-id="34f92-396">後續步驟</span><span class="sxs-lookup"><span data-stu-id="34f92-396">Next Steps</span></span>

- [<span data-ttu-id="34f92-397">Azure 資訊安全中心的偵測功能</span><span class="sxs-lookup"><span data-stu-id="34f92-397">Azure Security Center detection capabilities</span></span>](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities)

<span data-ttu-id="34f92-398">Azure 資訊安全中心的進階的偵測功能可協助 tooidentify 目標 Microsoft Azure 資源的作用中威脅，並提供您使用 hello insights 需要 toorespond 快速。</span><span class="sxs-lookup"><span data-stu-id="34f92-398">Azure Security Center’s advanced detection capabilities helps tooidentify active threats targeting your Microsoft Azure resources and provides you with hello insights needed toorespond quickly.</span></span>

- [<span data-ttu-id="34f92-399">Azure SQL Database 威脅偵測 (英文)</span><span class="sxs-lookup"><span data-stu-id="34f92-399">Azure SQL Database Threat Detection</span></span>](https://azure.microsoft.com/blog/azure-sql-database-threat-detection-your-built-in-security-expert/)

<span data-ttu-id="34f92-400">Azure SQL Database 威脅偵測協助處理潛在威脅 tootheir 資料庫相關的考量。</span><span class="sxs-lookup"><span data-stu-id="34f92-400">Azure SQL Database Threat Detection helped address their concerns about potential threats tootheir database.</span></span>
