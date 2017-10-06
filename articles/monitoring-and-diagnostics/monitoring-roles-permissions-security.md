---
title: "角色、 權限和安全性的 Azure 監視入門 aaaGet |Microsoft 文件"
description: "了解 toouse Azure 監視的內建的角色和權限 toorestrict 存取 toomonitoring 資源的方式。"
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 2686e53b-72f0-4312-bcd3-3dc1b4a9b912
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: johnkem
ms.openlocfilehash: 44fdf2a697050309480dfc164ebab51445b19bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-roles-permissions-and-security-with-azure-monitor"></a><span data-ttu-id="8a6d9-103">開始使用 Azure 監視器的角色、權限和安全性</span><span class="sxs-lookup"><span data-stu-id="8a6d9-103">Get started with roles, permissions, and security with Azure Monitor</span></span>
<span data-ttu-id="8a6d9-104">許多小組需要 toostrictly 規範存取 toomonitoring 資料和設定。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-104">Many teams need toostrictly regulate access toomonitoring data and settings.</span></span> <span data-ttu-id="8a6d9-105">例如，如果您有只在監視 （技術支援工程師，devops 工程師） 上之小組成員，或如果您使用受管理的服務提供者，您可能會想 toogrant 這些使用者存取監視資料，同時限制他們能夠 toocreate tooonly，修改，或刪除資源。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-105">For example, if you have team members who work exclusively on monitoring (support engineers, devops engineers) or if you use a managed service provider, you may want toogrant them access tooonly monitoring data while restricting their ability toocreate, modify, or delete resources.</span></span> <span data-ttu-id="8a6d9-106">本文示範如何 tooquickly 套用內建監視 RBAC 角色 tooa 使用者在 Azure 中的或建立您自己自訂的角色需要有限的監視權限的使用者。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-106">This article shows how tooquickly apply a built-in monitoring RBAC role tooa user in Azure or build your own custom role for a user who needs limited monitoring permissions.</span></span> <span data-ttu-id="8a6d9-107">接著討論您的 Azure 監視相關資源的安全性考量，而且包含您可以限制存取 toohello 資料的方式。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-107">It then discusses security considerations for your Azure Monitor-related resources and how you can limit access toohello data they contain.</span></span>

## <a name="built-in-monitoring-roles"></a><span data-ttu-id="8a6d9-108">內建的監視角色</span><span class="sxs-lookup"><span data-stu-id="8a6d9-108">Built-in monitoring roles</span></span>
<span data-ttu-id="8a6d9-109">Azure 監視的內建角色設計的 toohelp 限制存取 tooresources，同時仍可讓這些訂用帳戶中負責監視基礎結構 tooobtain 並設定所需的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-109">Azure Monitor’s built-in roles are designed toohelp limit access tooresources in a subscription while still enabling those responsible for monitoring infrastructure tooobtain and configure hello data they need.</span></span> <span data-ttu-id="8a6d9-110">Azure 監視器提供兩個現成的角色︰監視讀取器和監視參與者。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-110">Azure Monitor provides two out-of-the-box roles: A Monitoring Reader and a Monitoring Contributor.</span></span>

### <a name="monitoring-reader"></a><span data-ttu-id="8a6d9-111">監視讀取器</span><span class="sxs-lookup"><span data-stu-id="8a6d9-111">Monitoring Reader</span></span>
<span data-ttu-id="8a6d9-112">指派 hello 監視讀取者角色的人員可以將檢視訂用帳戶中的所有監視的資料，但無法修改任何資源或編輯任何設定的相關的 toomonitoring 資源。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-112">People assigned hello Monitoring Reader role can view all monitoring data in a subscription but cannot modify any resource or edit any settings related toomonitoring resources.</span></span> <span data-ttu-id="8a6d9-113">這個角色是適用於組織，例如支援或作業工程師，需要能夠 toobe 中的使用者：</span><span class="sxs-lookup"><span data-stu-id="8a6d9-113">This role is appropriate for users in an organization, such as support or operations engineers, who need toobe able to:</span></span>

* <span data-ttu-id="8a6d9-114">Hello 入口網站中檢視監視儀表板，並建立其自己私用的監視儀表板。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-114">View monitoring dashboards in hello portal and create their own private monitoring dashboards.</span></span>
* <span data-ttu-id="8a6d9-115">查詢度量使用 hello [Azure 監視 REST API](https://msdn.microsoft.com/library/azure/dn931930.aspx)， [PowerShell cmdlet](insights-powershell-samples.md)，或[跨平台 CLI](insights-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-115">Query for metrics using hello [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931930.aspx), [PowerShell cmdlets](insights-powershell-samples.md), or [cross-platform CLI](insights-cli-samples.md).</span></span>
* <span data-ttu-id="8a6d9-116">查詢 hello 使用 hello 入口網站、 Azure 監視 REST API、 PowerShell 指令程式或跨平台 CLI 活動記錄檔。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-116">Query hello Activity Log using hello portal, Azure Monitor REST API, PowerShell cmdlets, or cross-platform CLI.</span></span>
* <span data-ttu-id="8a6d9-117">檢視 hello[診斷設定](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings)資源。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-117">View hello [diagnostic settings](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) for a resource.</span></span>
* <span data-ttu-id="8a6d9-118">檢視 hello[記錄設定檔](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile)訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-118">View hello [log profile](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) for a subscription.</span></span>
* <span data-ttu-id="8a6d9-119">檢視自動調整設定。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-119">View autoscale settings.</span></span>
* <span data-ttu-id="8a6d9-120">檢視警示活動和設定。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-120">View alert activity and settings.</span></span>
* <span data-ttu-id="8a6d9-121">存取 Application Insights 資料，並檢視 AI 分析中的資料。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-121">Access Application Insights data and view data in AI Analytics.</span></span>
* <span data-ttu-id="8a6d9-122">搜尋包括 hello 工作區的使用量資料記錄分析 (OMS) 工作區的資料。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-122">Search Log Analytics (OMS) workspace data including usage data for hello workspace.</span></span>
* <span data-ttu-id="8a6d9-123">檢視 Log Analytics (OMS) 管理群組。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-123">View Log Analytics (OMS) management groups.</span></span>
* <span data-ttu-id="8a6d9-124">擷取 hello 記錄分析 (OMS) 的搜尋結構描述。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-124">Retrieve hello Log Analytics (OMS) search schema.</span></span>
* <span data-ttu-id="8a6d9-125">列出 Log Analytics (OMS) 智慧套件。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-125">List Log Analytics (OMS) intelligence packs.</span></span>
* <span data-ttu-id="8a6d9-126">擷取並執行 Log Analytics (OMS) 已儲存的搜尋。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-126">Retrieve and execute Log Analytics (OMS) saved searches.</span></span>
* <span data-ttu-id="8a6d9-127">擷取 hello 記錄分析 (OMS) 存放裝置設定。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-127">Retrieve hello Log Analytics (OMS) storage configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="8a6d9-128">此角色沒有提供經過資料流處理的 tooan 事件中心或儲存在儲存體帳戶的讀取權限 toolog 資料。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-128">This role does not give read access toolog data that has been streamed tooan event hub or stored in a storage account.</span></span> <span data-ttu-id="8a6d9-129">[請參閱下文](#security-considerations-for-monitoring-data)如需設定存取 toothese 資源資訊。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-129">[See below](#security-considerations-for-monitoring-data) for information on configuring access toothese resources.</span></span>
> 
> 

### <a name="monitoring-contributor"></a><span data-ttu-id="8a6d9-130">監視參與者</span><span class="sxs-lookup"><span data-stu-id="8a6d9-130">Monitoring Contributor</span></span>
<span data-ttu-id="8a6d9-131">指定人員 hello 監視參與者角色可以在訂用帳戶中檢視監視的所有資料並建立或修改的監視設定，但無法修改任何其他資源。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-131">People assigned hello Monitoring Contributor role can view all monitoring data in a subscription and create or modify monitoring settings, but cannot modify any other resources.</span></span> <span data-ttu-id="8a6d9-132">這個角色是 hello 監視讀取器角色中的超集，而且是適當的成員組織監視小組或受管理的服務提供者，此外 toohello 權限以上版本，也需要 toobe 能夠：</span><span class="sxs-lookup"><span data-stu-id="8a6d9-132">This role is a superset of hello Monitoring Reader role, and is appropriate for members of an organization’s monitoring team or managed service providers who, in addition toohello permissions above, also need toobe able to:</span></span>

* <span data-ttu-id="8a6d9-133">將監視儀表板發佈為共用儀表板。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-133">Publish monitoring dashboards as a shared dashboard.</span></span>
* <span data-ttu-id="8a6d9-134">設定用於資源的[診斷設定](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings)。*</span><span class="sxs-lookup"><span data-stu-id="8a6d9-134">Set [diagnostic settings](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) for a resource.*</span></span>
* <span data-ttu-id="8a6d9-135">設定 hello[記錄設定檔](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile)subscription.* 的</span><span class="sxs-lookup"><span data-stu-id="8a6d9-135">Set hello [log profile](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) for a subscription.*</span></span>
* <span data-ttu-id="8a6d9-136">設定警示活動和設定。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-136">Set alert activity and settings.</span></span>
* <span data-ttu-id="8a6d9-137">建立 Application Insights web 測試和元件。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-137">Create Application Insights web tests and components.</span></span>
* <span data-ttu-id="8a6d9-138">列出 Log Analytics (OMS) 工作區共用金鑰。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-138">List Log Analytics (OMS) workspace shared keys.</span></span>
* <span data-ttu-id="8a6d9-139">啟用或停用 Log Analytics (OMS) 智慧套件。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-139">Enable or disable Log Analytics (OMS) intelligence packs.</span></span>
* <span data-ttu-id="8a6d9-140">建立及刪除及執行 Log Analytics (OMS) 已儲存的搜尋。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-140">Create and delete and execute Log Analytics (OMS) saved searches.</span></span>
* <span data-ttu-id="8a6d9-141">建立及刪除 hello 記錄分析 (OMS) 存放裝置設定。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-141">Create and delete hello Log Analytics (OMS) storage configuration.</span></span>

<span data-ttu-id="8a6d9-142">* 使用者必須另外也有權 Listkey hello 目標資源 （儲存體帳戶或事件中樞命名空間） tooset 記錄檔的設定檔或診斷設定。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-142">*user must also separately be granted ListKeys permission on hello target resource (storage account or event hub namespace) tooset a log profile or diagnostic setting.</span></span>

> [!NOTE]
> <span data-ttu-id="8a6d9-143">此角色沒有提供經過資料流處理的 tooan 事件中心或儲存在儲存體帳戶的讀取權限 toolog 資料。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-143">This role does not give read access toolog data that has been streamed tooan event hub or stored in a storage account.</span></span> <span data-ttu-id="8a6d9-144">[請參閱下文](#security-considerations-for-monitoring-data)如需設定存取 toothese 資源資訊。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-144">[See below](#security-considerations-for-monitoring-data) for information on configuring access toothese resources.</span></span>
> 
> 

## <a name="monitoring-permissions-and-custom-rbac-roles"></a><span data-ttu-id="8a6d9-145">監視權限和自訂的 RBAC 角色</span><span class="sxs-lookup"><span data-stu-id="8a6d9-145">Monitoring permissions and custom RBAC roles</span></span>
<span data-ttu-id="8a6d9-146">如果 hello 上方內建的角色不符合您的小組的 hello 確切需求，您可以[建立自訂的 RBAC 角色](../active-directory/role-based-access-control-custom-roles.md)具有更細微的權限。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-146">If hello above built-in roles don’t meet hello exact needs of your team, you can [create a custom RBAC role](../active-directory/role-based-access-control-custom-roles.md) with more granular permissions.</span></span> <span data-ttu-id="8a6d9-147">以下是一般的 Azure 監視 RBAC 作業，其描述 hello。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-147">Below are hello common Azure Monitor RBAC operations with their descriptions.</span></span>

| <span data-ttu-id="8a6d9-148">作業</span><span class="sxs-lookup"><span data-stu-id="8a6d9-148">Operation</span></span> | <span data-ttu-id="8a6d9-149">說明</span><span class="sxs-lookup"><span data-stu-id="8a6d9-149">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8a6d9-150">Microsoft.Insights/AlertRules/[讀取、寫入、刪除]</span><span class="sxs-lookup"><span data-stu-id="8a6d9-150">Microsoft.Insights/AlertRules/[Read, Write, Delete]</span></span> |<span data-ttu-id="8a6d9-151">讀取/寫入/刪除警示規則。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-151">Read/write/delete alert rules.</span></span> |
| <span data-ttu-id="8a6d9-152">Microsoft.Insights/AlertRules/Incidents/Read</span><span class="sxs-lookup"><span data-stu-id="8a6d9-152">Microsoft.Insights/AlertRules/Incidents/Read</span></span> |<span data-ttu-id="8a6d9-153">列出警示規則事件 （hello 觸發的警示規則的記錄）。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-153">List incidents (history of hello alert rule being triggered) for alert rules.</span></span> <span data-ttu-id="8a6d9-154">這只適用於 toohello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-154">This only applies toohello portal.</span></span> |
| <span data-ttu-id="8a6d9-155">Microsoft.Insights/AutoscaleSettings/[讀取、寫入、刪除]</span><span class="sxs-lookup"><span data-stu-id="8a6d9-155">Microsoft.Insights/AutoscaleSettings/[Read, Write, Delete]</span></span> |<span data-ttu-id="8a6d9-156">讀取/寫入/刪除自動調整設定。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-156">Read/write/delete autoscale settings.</span></span> |
| <span data-ttu-id="8a6d9-157">Microsoft.Insights/DiagnosticSettings/[讀取、寫入、刪除]</span><span class="sxs-lookup"><span data-stu-id="8a6d9-157">Microsoft.Insights/DiagnosticSettings/[Read, Write, Delete]</span></span> |<span data-ttu-id="8a6d9-158">讀取/寫入/刪除診斷設定。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-158">Read/write/delete diagnostic settings.</span></span> |
| <span data-ttu-id="8a6d9-159">Microsoft.Insights/eventtypes/digestevents/Read</span><span class="sxs-lookup"><span data-stu-id="8a6d9-159">Microsoft.Insights/eventtypes/digestevents/Read</span></span> |<span data-ttu-id="8a6d9-160">此權限是必要的使用者需要存取 tooActivity 透過 hello 入口網站的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-160">This permission is necessary for users who need access tooActivity Logs via hello portal.</span></span> |
| <span data-ttu-id="8a6d9-161">Microsoft.Insights/eventtypes/values/Read</span><span class="sxs-lookup"><span data-stu-id="8a6d9-161">Microsoft.Insights/eventtypes/values/Read</span></span> |<span data-ttu-id="8a6d9-162">列出訂用帳戶中的活動記錄檔事件 (管理事件)。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-162">List Activity Log events (management events) in a subscription.</span></span> <span data-ttu-id="8a6d9-163">此權限是適用的 tooboth 程式設計和入口網站存取 toohello 活動記錄檔。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-163">This permission is applicable tooboth programmatic and portal access toohello Activity Log.</span></span> |
| <span data-ttu-id="8a6d9-164">Microsoft.Insights/LogDefinitions/Read</span><span class="sxs-lookup"><span data-stu-id="8a6d9-164">Microsoft.Insights/LogDefinitions/Read</span></span> |<span data-ttu-id="8a6d9-165">此權限是必要的使用者需要存取 tooActivity 透過 hello 入口網站的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-165">This permission is necessary for users who need access tooActivity Logs via hello portal.</span></span> |
| <span data-ttu-id="8a6d9-166">Microsoft.Insights/MetricDefinitions/Read</span><span class="sxs-lookup"><span data-stu-id="8a6d9-166">Microsoft.Insights/MetricDefinitions/Read</span></span> |<span data-ttu-id="8a6d9-167">讀取度量定義 (可用資源的度量類型清單)。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-167">Read metric definitions (list of available metric types for a resource).</span></span> |
| <span data-ttu-id="8a6d9-168">Microsoft.Insights/Metrics/Read</span><span class="sxs-lookup"><span data-stu-id="8a6d9-168">Microsoft.Insights/Metrics/Read</span></span> |<span data-ttu-id="8a6d9-169">讀取資源的度量。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-169">Read metrics for a resource.</span></span> |

> [!NOTE]
> <span data-ttu-id="8a6d9-170">存取 tooalerts、 診斷的設定和度量的資源需要該 hello 使用者具有讀取權限 toohello 資源類型和該資源的範圍。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-170">Access tooalerts, diagnostic settings, and metrics for a resource requires that hello user has Read access toohello resource type and scope of that resource.</span></span> <span data-ttu-id="8a6d9-171">診斷的設定或記錄檔的設定檔，封存 tooa 儲存體帳戶或資料流 tooevent 中心需要 hello 使用者 tooalso hello 目標資源具有 Listkey 權限建立 （「 寫入 」）。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-171">Creating (“write”) a diagnostic setting or log profile that archives tooa storage account or streams tooevent hubs requires hello user tooalso have ListKeys permission on hello target resource.</span></span>
> 
> 

<span data-ttu-id="8a6d9-172">比方說，透過使用資料表上方的 hello 您可以為 「 活動記錄讀取器 」 就像這樣建立自訂的 RBAC 角色：</span><span class="sxs-lookup"><span data-stu-id="8a6d9-172">For example, using hello above table you could create a custom RBAC role for an “Activity Log Reader” like this:</span></span>

```powershell
$role = Get-AzureRmRoleDefinition "Reader"
$role.Id = $null
$role.Name = "Activity Log Reader"
$role.Description = "Can view activity logs."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Insights/eventtypes/*")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/mySubscription")
New-AzureRmRoleDefinition -Role $role 
```

## <a name="security-considerations-for-monitoring-data"></a><span data-ttu-id="8a6d9-173">監視資料的安全性考量</span><span class="sxs-lookup"><span data-stu-id="8a6d9-173">Security considerations for monitoring data</span></span>
<span data-ttu-id="8a6d9-174">監視資料 (尤其是記錄檔)，可以包含機密資訊，例如 IP 位址或使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-174">Monitoring data—particularly log files—can contain sensitive information, such as IP addresses or user names.</span></span> <span data-ttu-id="8a6d9-175">來自 Azure 的監視資料有三種基本形式︰</span><span class="sxs-lookup"><span data-stu-id="8a6d9-175">Monitoring data from Azure comes in three basic forms:</span></span>

1. <span data-ttu-id="8a6d9-176">hello 活動記錄檔，其中描述 Azure 訂用帳戶的控制平面的所有動作。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-176">hello Activity Log, which describes all control-plane actions on your Azure subscription.</span></span>
2. <span data-ttu-id="8a6d9-177">診斷記錄檔，是由資源發出的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-177">Diagnostic Logs, which are logs emitted by a resource.</span></span>
3. <span data-ttu-id="8a6d9-178">度量，是由資源發出。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-178">Metrics, which are emitted by resources.</span></span>

<span data-ttu-id="8a6d9-179">這三種資料型別可以儲存在儲存體帳戶，或資料流處理 tooEvent 集線器，兩者都是一般用途的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-179">All three of these data types can be stored in a storage account or streamed tooEvent Hub, both of which are general-purpose Azure resources.</span></span> <span data-ttu-id="8a6d9-180">由於這些是一般用途的資源，因此對其進行建立、刪除及存取通常是保留給系統管理員的特殊權限作業。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-180">Because these are general-purpose resources, creating, deleting, and accessing them is a privileged operation usually reserved for an administrator.</span></span> <span data-ttu-id="8a6d9-181">我們建議您使用下列做法監視相關資源的 tooprevent 誤用 hello:</span><span class="sxs-lookup"><span data-stu-id="8a6d9-181">We suggest that you use hello following practices for monitoring-related resources tooprevent misuse:</span></span>

* <span data-ttu-id="8a6d9-182">針對監視資料使用單一、專用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-182">Use a single, dedicated storage account for monitoring data.</span></span> <span data-ttu-id="8a6d9-183">如果您需要 tooseparate 監視資料到多個儲存體帳戶時，絕對不會共用儲存體帳戶之間監視的使用方式和非監視資料，因為這樣可能會不小心讓只需要存取 （例如 toomonitoring 資料的使用者</span><span class="sxs-lookup"><span data-stu-id="8a6d9-183">If you need tooseparate monitoring data into multiple storage accounts, never share usage of a storage account between monitoring and non-monitoring data, as this may inadvertently give those who only need access toomonitoring data (eg.</span></span> <span data-ttu-id="8a6d9-184">第三方 SIEM) 存取 toonon 監視資料。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-184">a third-party SIEM) access toonon-monitoring data.</span></span>
* <span data-ttu-id="8a6d9-185">理由與上面相同的 hello 跨所有診斷設定使用單一的專用或 服務匯流排事件中樞命名空間。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-185">Use a single, dedicated Service Bus or Event Hub namespace across all diagnostic settings for hello same reason as above.</span></span>
* <span data-ttu-id="8a6d9-186">由將其保存在個別的資源群組中，會限制存取 toomonitoring 相關的儲存體帳戶或事件中心和[使用範圍](../active-directory/role-based-access-control-what-is.md#basics-of-access-management-in-azure)您監視角色 toolimit 存取 tooonly 資源群組。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-186">Limit access toomonitoring-related storage accounts or event hubs by keeping them in a separate resource group, and [use scope](../active-directory/role-based-access-control-what-is.md#basics-of-access-management-in-azure) on your monitoring roles toolimit access tooonly that resource group.</span></span>
* <span data-ttu-id="8a6d9-187">當使用者只需要存取 toomonitoring 資料永遠不會授與 hello Listkey 權限的儲存體帳戶或事件中心在訂用帳戶範圍。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-187">Never grant hello ListKeys permission for either storage accounts or event hubs at subscription scope when a user only needs access toomonitoring data.</span></span> <span data-ttu-id="8a6d9-188">相反地，授與這些權限 toohello 使用者在資源或資源群組 （如果您有專用的監視資源群組） 範圍。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-188">Instead, give these permissions toohello user at a resource or resource group (if you have a dedicated monitoring resource group) scope.</span></span>

### <a name="limiting-access-toomonitoring-related-storage-accounts"></a><span data-ttu-id="8a6d9-189">限制存取 toomonitoring 相關的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="8a6d9-189">Limiting access toomonitoring-related storage accounts</span></span>
<span data-ttu-id="8a6d9-190">當使用者或應用程式需要存取 toomonitoring 資料儲存體帳戶中的時，您應該[產生帳戶 SAS](https://msdn.microsoft.com/library/azure/mt584140.aspx) hello 包含具有唯讀存取的服務層級 tooblob 存放裝置的監視資料的儲存體帳戶上。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-190">When a user or application needs access toomonitoring data in a storage account, you should [generate an Account SAS](https://msdn.microsoft.com/library/azure/mt584140.aspx) on hello storage account that contains monitoring data with service-level read-only access tooblob storage.</span></span> <span data-ttu-id="8a6d9-191">在 PowerShell 中，它看起來應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="8a6d9-191">In PowerShell, this might look like:</span></span>

```powershell
$context = New-AzureStorageContext -ConnectionString "[connection string for your monitoring Storage Account]"
$token = New-AzureStorageAccountSASToken -ResourceType Service -Service Blob -Permission "rl" -Context $context
```

<span data-ttu-id="8a6d9-192">然後，您可以將需要從該儲存體帳戶，tooread hello 語彙基元 toohello 實體，其可以清單，並從該儲存體帳戶中的所有 blob 讀取。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-192">You can then give hello token toohello entity that needs tooread from that storage account, and it can list and read from all blobs in that storage account.</span></span>

<span data-ttu-id="8a6d9-193">或者，如果您需要 toocontrol RBAC 具有此權限，您可以授與該實體 hello Microsoft.Storage/storageAccounts/listkeys/action 該特定的儲存體帳戶的權限。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-193">Alternatively, if you need toocontrol this permission with RBAC, you can grant that entity hello Microsoft.Storage/storageAccounts/listkeys/action permission on that particular storage account.</span></span> <span data-ttu-id="8a6d9-194">這是必要的使用者需要 toobe 無法 tooset 診斷設定或記錄檔的設定檔 tooarchive tooa 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-194">This is necessary for users who need toobe able tooset a diagnostic setting or log profile tooarchive tooa storage account.</span></span> <span data-ttu-id="8a6d9-195">例如，您可以建立遵循自訂的 RBAC 角色的使用者或應用程式只需要從一個儲存體帳戶的 tooread hello:</span><span class="sxs-lookup"><span data-stu-id="8a6d9-195">For example, you could create hello following custom RBAC role for a user or application that only needs tooread from one storage account:</span></span>

```powershell
$role = Get-AzureRmRoleDefinition "Reader"
$role.Id = $null
$role.Name = "Monitoring Storage Account Reader"
$role.Description = "Can get hello storage account keys for a monitoring storage account."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Storage/storageAccounts/listkeys/action")
$role.Actions.Add("Microsoft.Storage/storageAccounts/Read")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/mySubscription/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/myMonitoringStorageAccount")
New-AzureRmRoleDefinition -Role $role 
```

> [!WARNING]
> <span data-ttu-id="8a6d9-196">hello Listkey 權限可讓 hello 使用者 toolist hello 主要和次要儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-196">hello ListKeys permission enables hello user toolist hello primary and secondary storage account keys.</span></span> <span data-ttu-id="8a6d9-197">這些金鑰授與 hello 使用者所有已簽署的權限 （讀取、 寫入、 建立 blob、 刪除 blob 等等） 在所有已簽署該儲存體帳戶中的服務 （blob、 佇列、 表格及檔案）。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-197">These keys grant hello user all signed permissions (read, write, create blobs, delete blobs, etc.) across all signed services (blob, queue, table, file) in that storage account.</span></span> <span data-ttu-id="8a6d9-198">我們建議盡可能使用上述的帳戶 SAS。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-198">We recommend using an Account SAS described above when possible.</span></span>
> 
> 

### <a name="limiting-access-toomonitoring-related-event-hubs"></a><span data-ttu-id="8a6d9-199">限制存取 toomonitoring 相關的事件中心</span><span class="sxs-lookup"><span data-stu-id="8a6d9-199">Limiting access toomonitoring-related event hubs</span></span>
<span data-ttu-id="8a6d9-200">使用事件中心可依照類似的模式，但首先您需要 toocreate 專用的接聽授權規則。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-200">A similar pattern can be followed with event hubs, but first you need toocreate a dedicated Listen authorization rule.</span></span> <span data-ttu-id="8a6d9-201">如果您想 toogrant 存取 tooan 應用程式只需要 toolisten toomonitoring 相關的事件中樞時，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="8a6d9-201">If you want toogrant access tooan application that only needs toolisten toomonitoring-related event hubs, do hello following:</span></span>

1. <span data-ttu-id="8a6d9-202">為資料流只接聽宣告的監視資料所建立的 hello 事件中樞上建立共用的存取原則。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-202">Create a shared access policy on hello event hub(s) that were created for streaming monitoring data with only Listen claims.</span></span> <span data-ttu-id="8a6d9-203">這可以在 hello 入口網站中完成。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-203">This can be done in hello portal.</span></span> <span data-ttu-id="8a6d9-204">例如，您可能會將它稱為 “monitoringReadOnly”。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-204">For example, you might call it “monitoringReadOnly.”</span></span> <span data-ttu-id="8a6d9-205">可能的話，您會想 toogive 金鑰直接 toohello 取用者，並略過 hello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-205">If possible, you will want toogive that key directly toohello consumer and skip hello next step.</span></span>
2. <span data-ttu-id="8a6d9-206">如果 hello 取用者需要 toobe 無法 tooget hello 金鑰特定，授與該事件中心 hello 使用者 hello Listkey 動作。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-206">If hello consumer needs toobe able tooget hello key ad-hoc, grant hello user hello ListKeys action for that event hub.</span></span> <span data-ttu-id="8a6d9-207">這也是必要的使用者需要 toobe 無法 tooset 診斷設定，或記錄設定檔 toostream tooevent 集線器。</span><span class="sxs-lookup"><span data-stu-id="8a6d9-207">This is also necessary for users who need toobe able tooset a diagnostic setting or log profile toostream tooevent hubs.</span></span> <span data-ttu-id="8a6d9-208">例如，您可能會建立 RBAC 規則︰</span><span class="sxs-lookup"><span data-stu-id="8a6d9-208">For example, you might create an RBAC rule:</span></span>
   
   ```powershell
   $role = Get-AzureRmRoleDefinition "Reader"
   $role.Id = $null
   $role.Name = "Monitoring Event Hub Listener"
   $role.Description = "Can get hello key toolisten tooan event hub streaming monitoring data."
   $role.Actions.Clear()
   $role.Actions.Add("Microsoft.ServiceBus/namespaces/authorizationrules/listkeys/action")
   $role.Actions.Add("Microsoft.ServiceBus/namespaces/Read")
   $role.AssignableScopes.Clear()
   $role.AssignableScopes.Add("/subscriptions/mySubscription/resourceGroups/myResourceGroup/providers/Microsoft.ServiceBus/namespaces/mySBNameSpace")
   New-AzureRmRoleDefinition -Role $role 
   ```

## <a name="next-steps"></a><span data-ttu-id="8a6d9-209">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8a6d9-209">Next steps</span></span>
* [<span data-ttu-id="8a6d9-210">深入了解 RBAC 和 Resource Manager 中的權限</span><span class="sxs-lookup"><span data-stu-id="8a6d9-210">Read about RBAC and permissions in Resource Manager</span></span>](../active-directory/role-based-access-control-what-is.md)
* [<span data-ttu-id="8a6d9-211">讀取的監視在 Azure 中的 hello 概觀</span><span class="sxs-lookup"><span data-stu-id="8a6d9-211">Read hello overview of monitoring in Azure</span></span>](monitoring-overview.md)

