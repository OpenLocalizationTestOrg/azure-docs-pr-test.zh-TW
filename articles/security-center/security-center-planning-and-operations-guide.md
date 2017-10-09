---
title: "aaaSecurity Center 計劃與作業指南 |Microsoft 文件"
description: "這份文件可協助您 tooplan 之前採用 Azure 資訊安全中心和每日作業考量。"
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: f984e4a2-ac97-40bf-b281-2f7f473494c4
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: yurid
ms.openlocfilehash: b0a0a6f5fd56fbd46f7736928c99e3bcd0b1e140
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-planning-and-operations-guide"></a><span data-ttu-id="85a48-103">Azure 資訊安全中心規劃和操作指南</span><span class="sxs-lookup"><span data-stu-id="85a48-103">Azure Security Center planning and operations guide</span></span>
<span data-ttu-id="85a48-104">此指南適用於資訊技術 (IT) 專業人員、 IT 架構設計人員、 資訊安全性分析師和其組織打算 toouse Azure 資訊安全中心的雲端系統管理員。</span><span class="sxs-lookup"><span data-stu-id="85a48-104">This guide is for information technology (IT) professionals, IT architects, information security analysts, and cloud administrators whose organizations are planning toouse Azure Security Center.</span></span>

>[!NOTE] 
><span data-ttu-id="85a48-105">從開始早期年 6 月 2017年，資訊安全中心將會使用 hello Microsoft Monitoring Agent toocollect 及儲存資料。</span><span class="sxs-lookup"><span data-stu-id="85a48-105">Beginning in early June 2017, Security Center will use hello Microsoft Monitoring Agent toocollect and store data.</span></span> <span data-ttu-id="85a48-106">請參閱[Azure 安全性 Center 平台移轉](security-center-platform-migration.md)toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="85a48-106">See [Azure Security Center Platform Migration](security-center-platform-migration.md) toolearn more.</span></span> <span data-ttu-id="85a48-107">本文章中的 hello 資訊表示資訊安全中心功能之後轉換 toohello Microsoft Monitoring Agent。</span><span class="sxs-lookup"><span data-stu-id="85a48-107">hello information in this article represents Security Center functionality after transition toohello Microsoft Monitoring Agent.</span></span>
>

## <a name="planning-guide"></a><span data-ttu-id="85a48-108">規劃指南</span><span class="sxs-lookup"><span data-stu-id="85a48-108">Planning guide</span></span>
<span data-ttu-id="85a48-109">本指南涵蓋了一組步驟和工作，您可以依照的 toooptimize 貴用戶使用的資訊安全中心會根據您組織的安全性需求和雲端管理模型。</span><span class="sxs-lookup"><span data-stu-id="85a48-109">This guide covers a set of steps and tasks that you can follow toooptimize your use of Security Center based on your organization’s security requirements and cloud management model.</span></span> <span data-ttu-id="85a48-110">資訊安全中心 tootake 充分利用，是重要 toounderstand 方式不同的個人或小組在您的組織使用 hello 服務 toomeet 安全開發和作業、 監視、 控管，和事件回應需求。</span><span class="sxs-lookup"><span data-stu-id="85a48-110">tootake full advantage of Security Center, it is important toounderstand how different individuals or teams in your organization use hello service toomeet secure development and operations, monitoring, governance, and incident response needs.</span></span> <span data-ttu-id="85a48-111">hello 主要區域 tooconsider 規劃 toouse 資訊安全中心時如下：</span><span class="sxs-lookup"><span data-stu-id="85a48-111">hello key areas tooconsider when planning toouse Security Center are:</span></span>

* <span data-ttu-id="85a48-112">安全性角色和存取控制</span><span class="sxs-lookup"><span data-stu-id="85a48-112">Security Roles and Access Controls</span></span>
* <span data-ttu-id="85a48-113">安全性原則和建議</span><span class="sxs-lookup"><span data-stu-id="85a48-113">Security Policies and Recommendations</span></span>
* <span data-ttu-id="85a48-114">資料收集和儲存</span><span class="sxs-lookup"><span data-stu-id="85a48-114">Data Collection and Storage</span></span>
* <span data-ttu-id="85a48-115">持續安全性監視</span><span class="sxs-lookup"><span data-stu-id="85a48-115">Ongoing Security Monitoring</span></span>
* <span data-ttu-id="85a48-116">事件回應</span><span class="sxs-lookup"><span data-stu-id="85a48-116">Incident Response</span></span>

<span data-ttu-id="85a48-117">在 hello 下一步 區段中，您將學習如何 tooplan 這些區域的每個及套用這些建議，根據您的需求。</span><span class="sxs-lookup"><span data-stu-id="85a48-117">In hello next section, you will learn how tooplan for each one of those areas and apply those recommendations based on your requirements.</span></span>

> [!NOTE]
> <span data-ttu-id="85a48-118">讀取[常見問題集 (FAQ) 的 Azure 資訊安全中心](security-center-faq.md)的 hello 設計和規劃階段期間也很有用的常見問題清單。</span><span class="sxs-lookup"><span data-stu-id="85a48-118">Read [Azure Security Center frequently asked questions (FAQ)](security-center-faq.md) for a list of common questions that can also be useful during hello designing and planning phase.</span></span>
> 

## <a name="security-roles-and-access-controls"></a><span data-ttu-id="85a48-119">安全性角色和存取控制</span><span class="sxs-lookup"><span data-stu-id="85a48-119">Security roles and access controls</span></span>
<span data-ttu-id="85a48-120">根據 hello 大小和您組織的結構，多個個人和小組可以使用資訊安全中心 tooperform 不同安全性相關的工作。</span><span class="sxs-lookup"><span data-stu-id="85a48-120">Depending on hello size and structure of your organization, multiple individuals and teams may use Security Center tooperform different security-related tasks.</span></span> <span data-ttu-id="85a48-121">在下列圖表中的 hello 有虛構人物代表其個別角色和安全性責任的範例：</span><span class="sxs-lookup"><span data-stu-id="85a48-121">In hello following diagram you have an example of fictitious personas and their respective roles and security responsibilities:</span></span>

![角色](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig01-new.png)

<span data-ttu-id="85a48-123">資訊安全中心可讓這些人員 toomeet 這些不同的責任。</span><span class="sxs-lookup"><span data-stu-id="85a48-123">Security Center enables these individuals toomeet these various responsibilities.</span></span> <span data-ttu-id="85a48-124">例如：</span><span class="sxs-lookup"><span data-stu-id="85a48-124">For example:</span></span>

<span data-ttu-id="85a48-125">**Jeff (雲端工作負載擁有者)**</span><span class="sxs-lookup"><span data-stu-id="85a48-125">**Jeff (Cloud Workload Owner)**</span></span>

* <span data-ttu-id="85a48-126">管理雲端工作負載和其相關的資源</span><span class="sxs-lookup"><span data-stu-id="85a48-126">Manage a cloud workload and its related resources</span></span>
* <span data-ttu-id="85a48-127">負責根據公司的安全性原則來實作和維護保護</span><span class="sxs-lookup"><span data-stu-id="85a48-127">Responsible for implementing and maintaining protections in accordance with company security policy</span></span>

<span data-ttu-id="85a48-128">**Ellen (CISO/CIO)**</span><span class="sxs-lookup"><span data-stu-id="85a48-128">**Ellen (CISO/CIO)**</span></span>

* <span data-ttu-id="85a48-129">負責所有 hello 公司的安全性課題</span><span class="sxs-lookup"><span data-stu-id="85a48-129">Responsible for all aspects of security for hello company</span></span>
* <span data-ttu-id="85a48-130">在雲端工作負載間想 toounderstand hello 公司的安全性狀態</span><span class="sxs-lookup"><span data-stu-id="85a48-130">Wants toounderstand hello company's security posture across cloud workloads</span></span>
* <span data-ttu-id="85a48-131">需要 toobe 主要攻擊和風險的通知</span><span class="sxs-lookup"><span data-stu-id="85a48-131">Needs toobe informed of major attacks and risks</span></span>

<span data-ttu-id="85a48-132">**David (IT 安全性)**</span><span class="sxs-lookup"><span data-stu-id="85a48-132">**David (IT Security)**</span></span>

* <span data-ttu-id="85a48-133">設定公司安全性原則 tooensure hello 適當保護就定位</span><span class="sxs-lookup"><span data-stu-id="85a48-133">Sets company security policies tooensure hello appropriate protections are in place</span></span>
* <span data-ttu-id="85a48-134">監控安全性原則的遵循狀態</span><span class="sxs-lookup"><span data-stu-id="85a48-134">Monitors compliance with policies</span></span>
* <span data-ttu-id="85a48-135">產生報告以供主管或稽核人員使用</span><span class="sxs-lookup"><span data-stu-id="85a48-135">Generates reports for leadership or auditors</span></span>

<span data-ttu-id="85a48-136">**Judy (安全性作業)**</span><span class="sxs-lookup"><span data-stu-id="85a48-136">**Judy (Security Operations)**</span></span>

* <span data-ttu-id="85a48-137">監視及回應 toosecurity 警示 24/7</span><span class="sxs-lookup"><span data-stu-id="85a48-137">Monitors and responds toosecurity alerts 24/7</span></span>
* <span data-ttu-id="85a48-138">呈報 tooCloud 工作負載擁有人或 IT 安全性分析師</span><span class="sxs-lookup"><span data-stu-id="85a48-138">Escalates tooCloud Workload Owner or IT Security Analyst</span></span>

<span data-ttu-id="85a48-139">**Sam (安全性分析師)**</span><span class="sxs-lookup"><span data-stu-id="85a48-139">**Sam (Security Analyst)**</span></span>

* <span data-ttu-id="85a48-140">調查攻擊</span><span class="sxs-lookup"><span data-stu-id="85a48-140">Investigate attacks</span></span>
* <span data-ttu-id="85a48-141">使用雲端工作負載擁有者 tooapply 補救</span><span class="sxs-lookup"><span data-stu-id="85a48-141">Work with Cloud Workload Owner tooapply remediation</span></span> 

<span data-ttu-id="85a48-142">資訊安全中心使用[角色型存取控制 (RBAC)](../active-directory/role-based-access-control-configure.md)，這樣會提供[內建角色](../active-directory/role-based-access-built-in-roles.md)toousers、 群組和服務在 Azure 中的可獲指派。</span><span class="sxs-lookup"><span data-stu-id="85a48-142">Security Center uses [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md), which provides [built-in roles](../active-directory/role-based-access-built-in-roles.md) that can be assigned toousers, groups, and services in Azure.</span></span> <span data-ttu-id="85a48-143">當使用者開啟資訊安全中心時，只看到資訊相關的 tooresources 他們擁有存取權。</span><span class="sxs-lookup"><span data-stu-id="85a48-143">When a user opens Security Center, they only see information related tooresources they have access to.</span></span> <span data-ttu-id="85a48-144">這表示 hello 使用者獲指派擁有者、 參與者或讀取器 toohello 訂用帳戶或資源群組的資源屬於 hello 角色。</span><span class="sxs-lookup"><span data-stu-id="85a48-144">Which means hello user is assigned hello role of Owner, Contributor, or Reader toohello subscription or resource group that a resource belongs to.</span></span> <span data-ttu-id="85a48-145">在加法 toothese 角色中，有兩個特定的資訊安全中心角色：</span><span class="sxs-lookup"><span data-stu-id="85a48-145">In addition toothese roles, there are two specific Security Center roles:</span></span>

- <span data-ttu-id="85a48-146">**安全性讀取器**： 所屬 toothis 角色的使用者是無法 tooview 權限 tooSecurity 中心，其包含建議、 警示、 原則和健全狀況，不過它無法 toomake 無法變更。</span><span class="sxs-lookup"><span data-stu-id="85a48-146">**Security reader**: user that belongs toothis role is be able tooview rights tooSecurity Center, which includes recommendations, alerts, policy, and health, but it won't be able toomake changes.</span></span>
- <span data-ttu-id="85a48-147">**安全性管理員**： 相同安全性讀取器，但它也可以更新 hello 安全性原則，關閉建議和警示。</span><span class="sxs-lookup"><span data-stu-id="85a48-147">**Security admin**: same as security reader but it can also update hello security policy, dismiss recommendations and alerts.</span></span>

<span data-ttu-id="85a48-148">hello 上面所述的資訊安全中心角色不需要存取 Azure 儲存體、 Web 和行動裝置、 或物聯網等的 tooother 服務區域。</span><span class="sxs-lookup"><span data-stu-id="85a48-148">hello Security Center roles described above do not have access tooother service areas of Azure such as Storage, Web & Mobile, or Internet of Things.</span></span>  

> [!NOTE]
> <span data-ttu-id="85a48-149">使用者需要 toobe 至少一個訂用帳戶、 資源群組擁有者或參與者 toobe 無法 toosee 在 Azure 中的資訊安全中心。</span><span class="sxs-lookup"><span data-stu-id="85a48-149">A user needs toobe at least a subscription, resource group owner, or contributor toobe able toosee Security Center in Azure.</span></span> 
> 
> 

<span data-ttu-id="85a48-150">使用 hello 人物代表 hello 上圖中，會需要下列的 RBAC hello 中說明：</span><span class="sxs-lookup"><span data-stu-id="85a48-150">Using hello personas explained in hello previous diagram, hello following RBAC would be needed:</span></span>

<span data-ttu-id="85a48-151">**Jeff (雲端工作負載擁有者)**</span><span class="sxs-lookup"><span data-stu-id="85a48-151">**Jeff (Cloud Workload Owner)**</span></span>

* <span data-ttu-id="85a48-152">資源群組擁有者/共同作業者</span><span class="sxs-lookup"><span data-stu-id="85a48-152">Resource Group Owner/Collaborator</span></span>

<span data-ttu-id="85a48-153">**David (IT 安全性)**</span><span class="sxs-lookup"><span data-stu-id="85a48-153">**David (IT Security)**</span></span>

* <span data-ttu-id="85a48-154">訂用帳戶擁有者/共同作業者或安全性管理員</span><span class="sxs-lookup"><span data-stu-id="85a48-154">Subscription Owner/Collaborator or Security Admin</span></span>

<span data-ttu-id="85a48-155">**Judy (安全性作業)**</span><span class="sxs-lookup"><span data-stu-id="85a48-155">**Judy (Security Operations)**</span></span>

* <span data-ttu-id="85a48-156">訂用帳戶的讀取器或安全性讀取器 tooview 警示</span><span class="sxs-lookup"><span data-stu-id="85a48-156">Subscription Reader or Security Reader tooview Alerts</span></span>
* <span data-ttu-id="85a48-157">訂用帳戶擁有者/共同作業者或安全性系統管理員需要 toodismiss 警示</span><span class="sxs-lookup"><span data-stu-id="85a48-157">Subscription Owner/Collaborator or Security Admin required toodismiss Alerts</span></span>

<span data-ttu-id="85a48-158">**Sam (安全性分析師)**</span><span class="sxs-lookup"><span data-stu-id="85a48-158">**Sam (Security Analyst)**</span></span>

* <span data-ttu-id="85a48-159">訂用帳戶的讀取器 tooview 警示</span><span class="sxs-lookup"><span data-stu-id="85a48-159">Subscription Reader tooview Alerts</span></span>
* <span data-ttu-id="85a48-160">訂用帳戶擁有者/共同作業者需要 toodismiss 警示</span><span class="sxs-lookup"><span data-stu-id="85a48-160">Subscription Owner/Collaborator required toodismiss Alerts</span></span>
* <span data-ttu-id="85a48-161">可能需要存取 toohello 工作區</span><span class="sxs-lookup"><span data-stu-id="85a48-161">Access toohello workspace may be required</span></span>

<span data-ttu-id="85a48-162">其他一些重要資訊 tooconsider:</span><span class="sxs-lookup"><span data-stu-id="85a48-162">Some other important information tooconsider:</span></span>

* <span data-ttu-id="85a48-163">只有訂用帳戶擁有者/參與者和安全性管理員可以編輯安全性原則</span><span class="sxs-lookup"><span data-stu-id="85a48-163">Only subscription Owners/Contributors and Security Admins can edit a security policy</span></span>
* <span data-ttu-id="85a48-164">只有訂用帳戶和資源群組擁有者和參與者可以套用資源的安全性建議</span><span class="sxs-lookup"><span data-stu-id="85a48-164">Only subscription and resource group Owners and Contributors can apply security recommendations for a resource</span></span>

<span data-ttu-id="85a48-165">在規劃使用 RBAC 資訊安全中心的存取控制，是確定 toounderstand 者組織中使用資訊安全中心。</span><span class="sxs-lookup"><span data-stu-id="85a48-165">When planning access control using RBAC for Security Center, be sure toounderstand who in your organization will be using Security Center.</span></span> <span data-ttu-id="85a48-166">以及他們會執行的工作，然後據此設定 RBAC。</span><span class="sxs-lookup"><span data-stu-id="85a48-166">Also, what types of tasks they will be performing and then configure RBAC accordingly.</span></span>

> [!NOTE]
> <span data-ttu-id="85a48-167">我們建議您將指派 hello 最寬鬆的角色所需的使用者 toocomplete 其工作。</span><span class="sxs-lookup"><span data-stu-id="85a48-167">We recommend that you assign hello least permissive role needed for users toocomplete their tasks.</span></span> <span data-ttu-id="85a48-168">例如，只需要 tooview hello 資源的安全性狀態的資訊，但未採取任何動作，例如套用建議，或編輯原則，使用者應該指派 hello 讀取者角色。</span><span class="sxs-lookup"><span data-stu-id="85a48-168">For example, users who only need tooview information about hello security state of resources but not take action, such as applying recommendations or editing policies, should be assigned hello Reader role.</span></span>
> 
> 

## <a name="security-policies-and-recommendations"></a><span data-ttu-id="85a48-169">安全性原則和建議</span><span class="sxs-lookup"><span data-stu-id="85a48-169">Security policies and recommendations</span></span>
<span data-ttu-id="85a48-170">安全性原則定義中指定的 hello 資源的建議使用的控制項 hello 組訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="85a48-170">A security policy defines hello set of controls, which are recommended for resources within hello specified subscription.</span></span> <span data-ttu-id="85a48-171">資訊安全中心，您定義原則根據 tooyour 公司的安全性需求與 hello 類型的應用程式或 hello 資料的機密性。</span><span class="sxs-lookup"><span data-stu-id="85a48-171">In Security Center, you define policies according tooyour company's security requirements and hello type of applications or sensitivity of hello data.</span></span>

<span data-ttu-id="85a48-172">會自動啟用 hello 訂用帳戶層級中的原則傳播 tooall hello 訂用帳戶內的資源群組中 hello 下列圖表所示：</span><span class="sxs-lookup"><span data-stu-id="85a48-172">Policies that are enabled in hello subscription level automatically propagate tooall resources groups within hello subscription as shown in hello following diagram:</span></span>

![安全性原則](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig2-newUI.png)

> [!NOTE]
> <span data-ttu-id="85a48-174">如果您需要的 tooreview 哪些原則已變更，您可以使用[Azure 稽核記錄檔](https://blogs.msdn.microsoft.com/cloud_solution_architect/2015/03/10/audit-logs-for-azure-events/)。</span><span class="sxs-lookup"><span data-stu-id="85a48-174">If you need tooreview which policies were changed, you can use [Azure Audit Logs](https://blogs.msdn.microsoft.com/cloud_solution_architect/2015/03/10/audit-logs-for-azure-events/).</span></span> <span data-ttu-id="85a48-175">原則變更一定都會記錄在 Azure 稽核記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="85a48-175">Policy changes are always logged in Azure Audit Logs.</span></span>
> 
> 

### <a name="security-recommendations"></a><span data-ttu-id="85a48-176">安全性建議</span><span class="sxs-lookup"><span data-stu-id="85a48-176">Security recommendations</span></span>
<span data-ttu-id="85a48-177">然後再設定安全性原則，請檢閱每個 hello[安全性建議](security-center-recommendations.md)，並判斷是否這些原則適用於各種不同的訂用帳戶和資源群組。</span><span class="sxs-lookup"><span data-stu-id="85a48-177">Before configuring security policies, review each of hello [security recommendations](security-center-recommendations.md), and determine whether these policies are appropriate for your various subscriptions and resource groups.</span></span> <span data-ttu-id="85a48-178">它也是重要的 toounderstand tooaddress 應該採取哪些動作[安全性建議](https://docs.microsoft.com/en-us/azure/security-center/security-center-recommendations)以及組織中負責監視新的建議和製作 hello 所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="85a48-178">It is also important toounderstand what action should be taken tooaddress [Security Recommendations](https://docs.microsoft.com/en-us/azure/security-center/security-center-recommendations) and who in your organization will be responsible for monitoring for new recommendations and taking hello needed steps.</span></span>

<span data-ttu-id="85a48-179">資訊安全中心會建議您針對您的 Azure 訂用帳戶提供安全性連絡人詳細資料。</span><span class="sxs-lookup"><span data-stu-id="85a48-179">Security Center will recommend that you provide security contact details for your Azure subscription.</span></span> <span data-ttu-id="85a48-180">這項資訊將供 Microsoft toocontact 您如果 hello Microsoft Security Response Center (MSRC) 探索非法或未經授權的合作對象已存取您的客戶資料。</span><span class="sxs-lookup"><span data-stu-id="85a48-180">This information will be used by Microsoft toocontact you if hello Microsoft Security Response Center (MSRC) discovers that your customer data has been accessed by an unlawful or unauthorized party.</span></span> <span data-ttu-id="85a48-181">讀取[提供安全性 Azure 資訊安全中心中的連絡人詳細資料](security-center-provide-security-contact-details.md)如需有關如何 tooenable 這項建議。</span><span class="sxs-lookup"><span data-stu-id="85a48-181">Read [Provide security contact details in Azure Security Center](security-center-provide-security-contact-details.md) for more information on how tooenable this recommendation.</span></span>

## <a name="data-collection-and-storage"></a><span data-ttu-id="85a48-182">資料收集和儲存</span><span class="sxs-lookup"><span data-stu-id="85a48-182">Data collection and storage</span></span>
<span data-ttu-id="85a48-183">Azure 資訊安全中心使用 hello Microsoft Monitoring Agent – 這是使用相同的代理程式的 hello Operations Management Suite，記錄分析服務 – toocollect 安全性資料，從您的虛擬機器的 hello。</span><span class="sxs-lookup"><span data-stu-id="85a48-183">Azure Security Center uses hello Microsoft Monitoring Agent – this is hello same agent used by hello Operations Management Suite and Log Analytics service – toocollect security data from your virtual machines.</span></span> <span data-ttu-id="85a48-184">從這個代理程式收集的資料會儲存在 Log Analytics 工作區中。</span><span class="sxs-lookup"><span data-stu-id="85a48-184">Data collected from this agent will be stored in your Log Analytics workspace(s).</span></span>

### <a name="agent"></a><span data-ttu-id="85a48-185">代理程式</span><span class="sxs-lookup"><span data-stu-id="85a48-185">Agent</span></span>

<span data-ttu-id="85a48-186">在 hello 安全性原則已啟用資料收集之後，hello Microsoft Monitoring Agent (如[Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-windows-agents)或[Linux](https://docs.microsoft.com/azure/log-analytics/log-analytics-linux-agents)) 已安裝在所有支援的 Azure Vm，然後建立任何新的。</span><span class="sxs-lookup"><span data-stu-id="85a48-186">After data collection is enabled in hello security policy, hello Microsoft Monitoring Agent (for [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-windows-agents) or [Linux](https://docs.microsoft.com/azure/log-analytics/log-analytics-linux-agents)) is installed on all supported Azure VMs and any new ones that are created.</span></span>  <span data-ttu-id="85a48-187">如果 VM 已經有 Microsoft Monitoring Agent 安裝，hello hello Azure 資訊安全中心會利用目前的 hello 安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="85a48-187">If hello VM already has hello Microsoft Monitoring Agent installed, Azure Security Center will leverage hello current installed agent.</span></span> <span data-ttu-id="85a48-188">hello 代理程式的程序是設計的 toobe 非侵入性功能，並對 VM 效能變得很小的影響。</span><span class="sxs-lookup"><span data-stu-id="85a48-188">hello agent’s process is designed toobe non-invasive and have very minimal impact on VM performance.</span></span>

<span data-ttu-id="85a48-189">Microsoft Monitoring Agent 的 Windows hello 需要使用 TCP 連接埠 443。</span><span class="sxs-lookup"><span data-stu-id="85a48-189">hello Microsoft Monitoring Agent for Windows requires use TCP port 443.</span></span> <span data-ttu-id="85a48-190">請參閱 hello[疑難排解文章](security-center-troubleshooting-guide.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="85a48-190">See hello [Troubleshooting article](security-center-troubleshooting-guide.md) for additional details.</span></span>

<span data-ttu-id="85a48-191">如果您想要有 toodisable 資料收集在某個時間點，可以在 hello 安全性原則中關閉它。</span><span class="sxs-lookup"><span data-stu-id="85a48-191">If at some point you want toodisable Data Collection, you can turn it off in hello security policy.</span></span> <span data-ttu-id="85a48-192">不過，hello Microsoft Monitoring Agent 可能會由其他 Azure 管理和監視服務，hello 代理程式將不會自動解除安裝，因為當您關閉資訊安全中心中的資料收集。</span><span class="sxs-lookup"><span data-stu-id="85a48-192">However, because hello Microsoft Monitoring Agent may be used by other Azure management and monitoring services, hello agent will not be uninstalled automatically when you turn off data collection in  Security Center.</span></span> <span data-ttu-id="85a48-193">您可以手動解除安裝 hello 代理程式所需。</span><span class="sxs-lookup"><span data-stu-id="85a48-193">You can manually uninstall hello agent if needed.</span></span>

> [!NOTE]
> <span data-ttu-id="85a48-194">一份支援的 Vm，讀取 hello toofind[常見問題集 (FAQ) 的 Azure 資訊安全中心](security-center-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="85a48-194">toofind a list of supported VMs, read hello [Azure Security Center frequently asked questions (FAQ)](security-center-faq.md).</span></span>
> 

### <a name="workspace"></a><span data-ttu-id="85a48-195">工作區</span><span class="sxs-lookup"><span data-stu-id="85a48-195">Workspace</span></span>

<span data-ttu-id="85a48-196">從 Microsoft Monitoring Agent （代表 Azure 資訊安全中心） 會儲存在現有記錄分析 workspace(s) hello 收集的資料與相關聯 Azure 訂用帳戶或新 workspace(s)，納入帳戶 hello hello VM 的地理。</span><span class="sxs-lookup"><span data-stu-id="85a48-196">Data collected from hello Microsoft Monitoring Agent (on behalf of Azure Security Center) will be stored in either an existing Log Analytics workspace(s) associated with your Azure subscription or a new workspace(s), taking into account hello Geo of hello VM.</span></span> 

<span data-ttu-id="85a48-197">在 hello Azure 入口網站，您可以瀏覽 toosee 記錄分析工作區，包括任何 Azure 資訊安全中心所建立的清單。</span><span class="sxs-lookup"><span data-stu-id="85a48-197">In hello Azure portal, you can browse toosee a list of your Log Analytics workspaces, including any created by Azure Security Center.</span></span> <span data-ttu-id="85a48-198">將會針對新的工作區建立相關的資源群組。</span><span class="sxs-lookup"><span data-stu-id="85a48-198">A related resource group will be created for new workspaces.</span></span> <span data-ttu-id="85a48-199">兩者都會遵照此命名慣例：</span><span class="sxs-lookup"><span data-stu-id="85a48-199">Both will follow this naming convention:</span></span> 

* <span data-ttu-id="85a48-200">工作區：*DefaultWorkspace-[subscription-ID]-[geo]*</span><span class="sxs-lookup"><span data-stu-id="85a48-200">Workspace: *DefaultWorkspace-[subscription-ID]-[geo]*</span></span>
* <span data-ttu-id="85a48-201">資源群組：*DefaultResouceGroup-[geo]*</span><span class="sxs-lookup"><span data-stu-id="85a48-201">Resource Group: *DefaultResouceGroup-[geo]*</span></span>

<span data-ttu-id="85a48-202">若為 Azure 資訊安全中心所建立的工作區，資料會保留 30 天。</span><span class="sxs-lookup"><span data-stu-id="85a48-202">For workspaces created by Azure Security Center, data is retained for 30 days.</span></span> <span data-ttu-id="85a48-203">結束工作區，保留根據 hello 工作區的定價層。</span><span class="sxs-lookup"><span data-stu-id="85a48-203">For exiting workspaces, retention is based on hello workspace pricing tier.</span></span>

> [!NOTE]
> <span data-ttu-id="85a48-204">Microsoft 會進行這項資料的強式承諾 tooprotect hello 隱私與安全性。</span><span class="sxs-lookup"><span data-stu-id="85a48-204">Microsoft make strong commitments tooprotect hello privacy and security of this data.</span></span> <span data-ttu-id="85a48-205">Microsoft 遵守 toostrict 相容性與安全性指導方針 — 從 toooperating 服務撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="85a48-205">Microsoft adheres toostrict compliance and security guidelines—from coding toooperating a service.</span></span> <span data-ttu-id="85a48-206">如需資料處理和隱私權的詳細資訊，請閱讀 [Azure 資訊安全中心資料安全性](security-center-data-security.md)。</span><span class="sxs-lookup"><span data-stu-id="85a48-206">For more information about data handling and privacy, read [Azure Security Center Data Security](security-center-data-security.md).</span></span>
> 

## <a name="ongoing-security-monitoring"></a><span data-ttu-id="85a48-207">持續安全性監視</span><span class="sxs-lookup"><span data-stu-id="85a48-207">Ongoing security monitoring</span></span>
<span data-ttu-id="85a48-208">初始設定和應用程式的資訊安全中心建議之後, hello 下一個步驟的考量資訊安全中心操作程序。</span><span class="sxs-lookup"><span data-stu-id="85a48-208">After initial configuration and application of Security Center recommendations, hello next step is considering Security Center operational processes.</span></span>

<span data-ttu-id="85a48-209">從 Azure 入口網站，您可以按一下 hello tooaccess 資訊安全中心**瀏覽**和型別**資訊安全中心**在 hello**篩選**欄位。</span><span class="sxs-lookup"><span data-stu-id="85a48-209">tooaccess Security Center from hello Azure portal you can click **Browse** and type **Security Center** in hello **Filter** field.</span></span> <span data-ttu-id="85a48-210">hello hello 使用者取得會根據 toothese 套用篩選的檢視，下方的 hello 範例顯示定址的許多問題 toobe 環境：</span><span class="sxs-lookup"><span data-stu-id="85a48-210">hello views that hello user gets are according toothese applied filters, hello example below shows an environment with many issues toobe addressed:</span></span>

![儀表板](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig6.png)

> [!NOTE]
> <span data-ttu-id="85a48-212">資訊安全中心不會干擾一般作業程序，則被動會監視您的部署，並提供您啟用 hello 安全性原則為基礎的建議。</span><span class="sxs-lookup"><span data-stu-id="85a48-212">Security Center will not interfere with your normal operational procedures, it will passively monitor your deployments and provide recommendations based on hello security policies you enabled.</span></span>

<span data-ttu-id="85a48-213">當您第一次選擇 toouse 資訊安全中心進行目前的 Azure 環境時，請確定您檢閱所有的建議，可依 hello**建議**磚或每個資源 (**計算****網路**，**儲存體與資料**，**應用程式**)。</span><span class="sxs-lookup"><span data-stu-id="85a48-213">When you first opt in toouse Security Center for your current Azure environment, make sure that you review all recommendations, which can be done in hello **Recommendations** tile or per resource (**Compute**, **Networking**, **Storage & data**, **Application**).</span></span>

<span data-ttu-id="85a48-214">一旦您解決所有建議，hello**防止**區段應為綠色的已解決的所有資源。</span><span class="sxs-lookup"><span data-stu-id="85a48-214">Once you address all recommendations, hello **Prevention** section should be green for all resources that were addressed.</span></span> <span data-ttu-id="85a48-215">持續不斷的監控此時可更輕鬆因為您將會僅依據採取動作 hello 資源安全性健康情況及建議磚中的變更。</span><span class="sxs-lookup"><span data-stu-id="85a48-215">Ongoing monitoring at this point becomes easier since you will only take actions based on changes in hello resource security health and recommendations tiles.</span></span>

<span data-ttu-id="85a48-216">hello**偵測**區段是更反應式，這些問題可能是發生現在，或發生在過去的 hello 所偵測的資訊安全中心控制項和第 3 個合作對象系統所發出的警示。</span><span class="sxs-lookup"><span data-stu-id="85a48-216">hello **Detection** section is more reactive, these are alerts regarding issues that are either taking place now, or occurred in hello past and were detected by Security Center controls and 3rd party systems.</span></span> <span data-ttu-id="85a48-217">hello 安全性警示磚會顯示代表每一天，以及其 hello 不同嚴重性分類 （低、 中高） 之間的分佈中找不到的威脅偵測警示的 hello 數目的長條圖。</span><span class="sxs-lookup"><span data-stu-id="85a48-217">hello Security Alerts tile will show bar graphs that represent hello number of threat detection alerts that were found in each day, and their distribution among hello different severity categories (low, medium, high).</span></span> <span data-ttu-id="85a48-218">如需有關安全性警示的詳細資訊，請閱讀[中 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="85a48-218">For more information about Security Alerts, read [Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md).</span></span>

> [!NOTE]
> <span data-ttu-id="85a48-219">您也可以利用 Microsoft Power BI toovisualize 資訊安全中心資料。</span><span class="sxs-lookup"><span data-stu-id="85a48-219">You can also leverage Microsoft Power BI toovisualize your Security Center data.</span></span> <span data-ttu-id="85a48-220">請閱讀 [使用 Power BI 從 Azure 資訊安全中心的資料取得見解](security-center-powerbi.md)。</span><span class="sxs-lookup"><span data-stu-id="85a48-220">Read [Get insights from Azure Security Center data with Power BI](security-center-powerbi.md).</span></span>
> 
> 

### <a name="monitoring-for-new-or-changed-resources"></a><span data-ttu-id="85a48-221">監視新的或已變更的資源</span><span class="sxs-lookup"><span data-stu-id="85a48-221">Monitoring for new or changed resources</span></span>
<span data-ttu-id="85a48-222">大多數 Azure 環境是動態的，包含定期上下波動的新資源、組態或變更等。資訊安全中心可協助確保您擁有 hello 安全性狀態，這些新的資源可視性。</span><span class="sxs-lookup"><span data-stu-id="85a48-222">Most Azure environments are dynamic, with new resources being spun up and down on a regular basis, configurations or changes, etc. Security Center helps ensure that you have visibility into hello security state of these new resources.</span></span>

<span data-ttu-id="85a48-223">當您新增新的資源 （Vm、 SQL 資料庫） tooyour Azure 環境時，資訊安全中心會自動探索這些資源，並開始 toomonitor 它們的安全性。</span><span class="sxs-lookup"><span data-stu-id="85a48-223">When you add new resources (VMs, SQL DBs) tooyour Azure Environment, Security Center will automatically discover these resources and begin toomonitor their security.</span></span> <span data-ttu-id="85a48-224">這也包括 PaaS Web 角色和背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="85a48-224">This also includes PaaS web roles and worker roles.</span></span> <span data-ttu-id="85a48-225">如果已啟用資料收集在 hello[安全性原則](security-center-policies.md)、 其他監視功能將會自動啟用您的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="85a48-225">If Data Collection is enabled in hello [Security Policy](security-center-policies.md), additional monitoring capabilities will be enabled automatically for your virtual machines.</span></span>

![主要領域](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig3-newUI.png)

1. <span data-ttu-id="85a48-227">針對虛擬機器，按一下 [預防] 區段下的 [計算]。</span><span class="sxs-lookup"><span data-stu-id="85a48-227">For virtual machines, click **Compute**, under **Prevention** section.</span></span> <span data-ttu-id="85a48-228">啟用資料或相關的建議的任何問題會發生在 hello**概觀** 索引標籤和**監視建議**> 一節。</span><span class="sxs-lookup"><span data-stu-id="85a48-228">Any issues with enabling data or related recommendations will be surfaced in hello **Overview** tab, and **Monitoring Recommendations** section.</span></span>
2. <span data-ttu-id="85a48-229">檢視 hello**建議**toosee 什麼，如果有的話，已辨識 hello 新資源的安全性風險。</span><span class="sxs-lookup"><span data-stu-id="85a48-229">View hello **Recommendations** toosee what, if any, security risks were identified for hello new resource.</span></span>
3. <span data-ttu-id="85a48-230">是非常普遍，當新的 Vm 加入 tooyour 環境時，只有 hello 一開始安裝作業系統。</span><span class="sxs-lookup"><span data-stu-id="85a48-230">It is very common that when new VMs are added tooyour environment, only hello operating system is initially installed.</span></span> <span data-ttu-id="85a48-231">hello 資源擁有者可能需要一些時間 toodeploy 將這些 Vm 所使用的其他應用程式。</span><span class="sxs-lookup"><span data-stu-id="85a48-231">hello resource owner might need some time toodeploy other apps that will be used by these VMs.</span></span>  <span data-ttu-id="85a48-232">在理想情況下，您應該知道此工作負載的 hello 最終的目的。</span><span class="sxs-lookup"><span data-stu-id="85a48-232">Ideally, you should know hello final intent of this workload.</span></span> <span data-ttu-id="85a48-233">它即將 toobe 應用程式伺服器嗎？</span><span class="sxs-lookup"><span data-stu-id="85a48-233">Is it going toobe an Application Server?</span></span> <span data-ttu-id="85a48-234">根據此新的工作負載會持續 toobe，您可以啟用適當的 hello**安全性原則**，這是此工作流程中的 hello 第三個步驟。</span><span class="sxs-lookup"><span data-stu-id="85a48-234">Based on what this new workload is going toobe, you can enable hello appropriate **Security Policy**, which is hello third step in this workflow.</span></span>
4. <span data-ttu-id="85a48-235">當新的資源加入 tooyour Azure 環境時，很可能在新的警示會顯示在 hello**安全性警示**磚。</span><span class="sxs-lookup"><span data-stu-id="85a48-235">As new resources are added tooyour Azure environment, it is possible that new alerts appear in hello **Security Alerts** tile.</span></span> <span data-ttu-id="85a48-236">一律驗證此磚中是否有新警示，並採取根據 tooSecurity 中心建議的動作。</span><span class="sxs-lookup"><span data-stu-id="85a48-236">Always verify if there are new alerts in this tile and take actions according tooSecurity Center recommendations.</span></span>

<span data-ttu-id="85a48-237">您也會想 tooregularly 監視 hello 狀態現有資源 tooidentify 的組態變更已建立的安全性風險，建議的基準，以及安全性警示從漂移。</span><span class="sxs-lookup"><span data-stu-id="85a48-237">You will also want tooregularly monitor hello state of existing resources tooidentify configuration changes that have created security risks, drift from recommended baselines, and security alerts.</span></span> <span data-ttu-id="85a48-238">在 hello 資訊安全中心儀表板開始。</span><span class="sxs-lookup"><span data-stu-id="85a48-238">Start at hello Security Center dashboard.</span></span> <span data-ttu-id="85a48-239">從該處，您會有三個主要區域 tooreview 持續。</span><span class="sxs-lookup"><span data-stu-id="85a48-239">From there you have three major areas tooreview on a consistent basis.</span></span>

![作業](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig4-newUI.png)

1. <span data-ttu-id="85a48-241">hello**防止**區段面板提供您快速存取 tooyour 重要資源。</span><span class="sxs-lookup"><span data-stu-id="85a48-241">hello **Prevention** section panel provides you quick access tooyour key resources.</span></span> <span data-ttu-id="85a48-242">使用此選項 toomonitor 計算、 網路、 儲存體及資料和應用程式。</span><span class="sxs-lookup"><span data-stu-id="85a48-242">Use this option toomonitor Compute, Networking, Storage & data and Applications.</span></span>
2. <span data-ttu-id="85a48-243">hello**建議**面板可讓您 tooreview 資訊安全中心建議。</span><span class="sxs-lookup"><span data-stu-id="85a48-243">hello **Recommendations** panel enables you tooreview Security Center recommendations.</span></span> <span data-ttu-id="85a48-244">持續監視期間可能會發現您不需要每日，這是正常現象，因為定址在 hello 初始資訊安全中心設定的所有建議的建議。</span><span class="sxs-lookup"><span data-stu-id="85a48-244">During your ongoing monitoring you may find that you don’t have recommendations on a daily basis, which is normal since you addressed all recommendations on hello initial Security Center setup.</span></span> <span data-ttu-id="85a48-245">基於這個理由，您可能沒有新的資訊在本節中每一天，只需要 tooaccess 視它。</span><span class="sxs-lookup"><span data-stu-id="85a48-245">For this reason, you may not have new information in this section every day and will just need tooaccess it as needed.</span></span>
3. <span data-ttu-id="85a48-246">hello**偵測**區段可能會非常頻繁或非常不頻繁的基礎上變更。</span><span class="sxs-lookup"><span data-stu-id="85a48-246">hello **Detection** section might change on either a very frequent or very infrequent basis.</span></span> <span data-ttu-id="85a48-247">請隨時檢閱安全性警示，並根據資訊安全中心的建議採取動作。</span><span class="sxs-lookup"><span data-stu-id="85a48-247">Always review your security alerts and take actions based on Security Center recommendations.</span></span>

## <a name="incident-response"></a><span data-ttu-id="85a48-248">事件回應</span><span class="sxs-lookup"><span data-stu-id="85a48-248">Incident response</span></span>
<span data-ttu-id="85a48-249">資訊安全中心會偵測並警示您 toothreats 發生。</span><span class="sxs-lookup"><span data-stu-id="85a48-249">Security Center detects and alerts you toothreats as they occur.</span></span> <span data-ttu-id="85a48-250">組織應該為新的安全性警示來監視和採取動作為所需 tooinvestigate 進一步或補救 hello 攻擊。</span><span class="sxs-lookup"><span data-stu-id="85a48-250">Organizations should monitor for new security alerts and take action as needed tooinvestigate further or remediate hello attack.</span></span> <span data-ttu-id="85a48-251">如需資訊安全中心威脅偵測運作方式的詳細資訊，請閱讀 [Azure 資訊安全中心的偵測功能](security-center-detection-capabilities.md)。</span><span class="sxs-lookup"><span data-stu-id="85a48-251">For more information on how Security Center threat detection works, read [Azure Security Center detection capabilities](security-center-detection-capabilities.md).</span></span>

<span data-ttu-id="85a48-252">雖然本文不會有 hello 意圖 tooassist 您建立自己的事件回應計劃，我們 toouse Microsoft Azure 安全性回應 hello 雲端生命週期中的為 hello 基礎事件回應階段。</span><span class="sxs-lookup"><span data-stu-id="85a48-252">While this article doesn’t have hello intent tooassist you creating your own Incident Response plan, we are going toouse Microsoft Azure Security Response in hello Cloud lifecycle as hello foundation for incident response stages.</span></span> <span data-ttu-id="85a48-253">hello 下列圖表顯示 hello 階段：</span><span class="sxs-lookup"><span data-stu-id="85a48-253">hello stages are shown in hello following diagram:</span></span>

![可疑的活動](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig5-1.png)

> [!NOTE]
> <span data-ttu-id="85a48-255">您可以使用 hello 美國國家標準與技術局 (NIST)[電腦安全性事件處理指南](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf)參考 tooassist 為您建置自己。</span><span class="sxs-lookup"><span data-stu-id="85a48-255">You can use hello National Institute of Standards and Technology (NIST) [Computer Security Incident Handling Guide](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf) as a reference tooassist you building your own.</span></span>
> 

<span data-ttu-id="85a48-256">您可以使用安全性中心警示期間 hello 下列階段：</span><span class="sxs-lookup"><span data-stu-id="85a48-256">You can use Security Center Alerts during hello following stages:</span></span>

* <span data-ttu-id="85a48-257">**偵測**︰識別一或多個資源中的可疑活動。</span><span class="sxs-lookup"><span data-stu-id="85a48-257">**Detect**: identify a suspicious activity in one or more resources.</span></span> 
* <span data-ttu-id="85a48-258">**評估**： 執行 hello 初始評估 tooobtain hello 可疑活動的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="85a48-258">**Assess**: perform hello initial assessment tooobtain more information about hello suspicious activity.</span></span>
* <span data-ttu-id="85a48-259">**診斷**： 使用 hello 補救步驟 tooconduct hello 技術的程序 tooaddress hello 問題。</span><span class="sxs-lookup"><span data-stu-id="85a48-259">**Diagnose**: use hello remediation steps tooconduct hello technical procedure tooaddress hello issue.</span></span>

<span data-ttu-id="85a48-260">每個安全性警示提供的資訊，可以用 toobetter 瞭解 hello 攻擊的 hello 本質，並建議可能的補救措施。</span><span class="sxs-lookup"><span data-stu-id="85a48-260">Each Security Alert provides information that can be used toobetter understand hello nature of hello attack and suggest possible mitigations.</span></span> <span data-ttu-id="85a48-261">某些警示也會提供連結 tooeither 更多的資訊或 tooother 來源 Azure 中的資訊。</span><span class="sxs-lookup"><span data-stu-id="85a48-261">Some alerts also provide links tooeither more information or tooother sources of information within Azure.</span></span> <span data-ttu-id="85a48-262">您可以使用 hello 做進一步研究和 toobegin 降低所提供的資訊，您也可以搜尋儲存在您的工作區的安全性相關資料。</span><span class="sxs-lookup"><span data-stu-id="85a48-262">You can use hello information provided for further research and toobegin mitigation, and you can also search security-related data that is stored in your workspace.</span></span>

<span data-ttu-id="85a48-263">hello 下例示範可疑的 RDP 活動正在進行中：</span><span class="sxs-lookup"><span data-stu-id="85a48-263">hello following example shows a suspicious RDP activity taking place:</span></span>

![可疑的活動](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig5-ga.png)

<span data-ttu-id="85a48-265">如您所見，此刀鋒視窗會顯示有關 hello 時間 hello 攻擊發生、 hello 來源主機名稱、 hello 目標 VM 和也會提供建議步驟。</span><span class="sxs-lookup"><span data-stu-id="85a48-265">As you can see, this blade shows details regarding hello time that hello attack took place, hello source hostname, hello target VM and also gives recommendation steps.</span></span> <span data-ttu-id="85a48-266">在某些情況下 hello hello 攻擊的來源資訊可能是空的。</span><span class="sxs-lookup"><span data-stu-id="85a48-266">In some circumstances hello source information of hello attack may be empty.</span></span> <span data-ttu-id="85a48-267">如需有關這類行為的詳細資訊，請閱讀 [Azure 資訊安全中心警示中的缺少來源資訊](https://blogs.msdn.microsoft.com/azuresecurity/2016/03/25/missing-source-information-in-azure-security-center-alerts/) 。</span><span class="sxs-lookup"><span data-stu-id="85a48-267">Read [Missing Source Information in Azure Security Center Alerts](https://blogs.msdn.microsoft.com/azuresecurity/2016/03/25/missing-source-information-in-azure-security-center-alerts/) for more information about this type of behavior.</span></span>

<span data-ttu-id="85a48-268">在 hello [tooLeverage 如何 hello Azure 資訊安全中心 & Microsoft Operations Management Suite 事件回應](https://channel9.msdn.com/Blogs/Taste-of-Premier/ToP1703)視訊可以看到可協助您 toounderstand 如何使用資訊安全中心，在每個部分示範其中的一個階段。</span><span class="sxs-lookup"><span data-stu-id="85a48-268">In hello [How tooLeverage hello Azure Security Center & Microsoft Operations Management Suite for an Incident Response](https://channel9.msdn.com/Blogs/Taste-of-Premier/ToP1703) video you can see some demonstrations that can help you toounderstand how Security Center can be used in each one of those stages.</span></span>

> [!NOTE]
> <span data-ttu-id="85a48-269">讀取[Leveraging Azure 資訊安全中心事件回應](security-center-incident-response.md)如需 toouse 資訊安全中心功能 tooassist 您期間事件回應程序的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="85a48-269">Read [Leveraging Azure Security Center for Incident Response](security-center-incident-response.md) for more information on how toouse Security Center capabilities tooassist you during your Incident Response process.</span></span> 
> 
> 

## <a name="see-also"></a><span data-ttu-id="85a48-270">另請參閱</span><span class="sxs-lookup"><span data-stu-id="85a48-270">See also</span></span>
<span data-ttu-id="85a48-271">在本文件中，您學到如何 tooplan 資訊安全中心採用。</span><span class="sxs-lookup"><span data-stu-id="85a48-271">In this document, you learned how tooplan for Security Center adoption.</span></span> <span data-ttu-id="85a48-272">toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="85a48-272">toolearn more about Security Center, see hello following:</span></span>

* [<span data-ttu-id="85a48-273">管理及回應 toosecurity Azure 資訊安全中心警示</span><span class="sxs-lookup"><span data-stu-id="85a48-273">Managing and responding toosecurity alerts in Azure Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* <span data-ttu-id="85a48-274">[在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)— 了解如何 toomonitor hello 您的 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="85a48-274">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="85a48-275">[監視與 Azure 資訊安全中心的協力廠商解決方案](security-center-partner-solutions.md)— 了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="85a48-275">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) — Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="85a48-276">[Azure 資訊安全中心常見問題集](security-center-faq.md)— 尋找使用 hello 服務相關的常見問題集。</span><span class="sxs-lookup"><span data-stu-id="85a48-276">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="85a48-277">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) — 尋找有關 Azure 安全性與相容性的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="85a48-277">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>

