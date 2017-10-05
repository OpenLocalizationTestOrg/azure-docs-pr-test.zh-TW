---
title: "開始使用 Azure 監視器的角色、權限和安全性 | Microsoft Docs"
description: "了解如何使用 Azure 監視器的內建角色和權限來限制存取監視資源。"
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
ms.openlocfilehash: a28f971ae898ffdd1168550a909f2a48e1b3b652
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-roles-permissions-and-security-with-azure-monitor"></a><span data-ttu-id="3aa91-103">開始使用 Azure 監視器的角色、權限和安全性</span><span class="sxs-lookup"><span data-stu-id="3aa91-103">Get started with roles, permissions, and security with Azure Monitor</span></span>
<span data-ttu-id="3aa91-104">許多團隊需要嚴格規範對監視資料及設定的存取。</span><span class="sxs-lookup"><span data-stu-id="3aa91-104">Many teams need to strictly regulate access to monitoring data and settings.</span></span> <span data-ttu-id="3aa91-105">例如，如果您擁有專門從事監視 (技術支援工程師、devops 工程師) 的團隊成員，或如果您使用受管理的服務提供者，則您可能只要授與他們監視資料的存取權，同時限制他們建立、修改或刪除資源的能力。</span><span class="sxs-lookup"><span data-stu-id="3aa91-105">For example, if you have team members who work exclusively on monitoring (support engineers, devops engineers) or if you use a managed service provider, you may want to grant them access to only monitoring data while restricting their ability to create, modify, or delete resources.</span></span> <span data-ttu-id="3aa91-106">本文說明如何在 Azure 中快速將內建的監視 RBAC 角色套用到使用者，或針對需要有限監視權限的使用者建置您自己的自訂角色。</span><span class="sxs-lookup"><span data-stu-id="3aa91-106">This article shows how to quickly apply a built-in monitoring RBAC role to a user in Azure or build your own custom role for a user who needs limited monitoring permissions.</span></span> <span data-ttu-id="3aa91-107">接著會討論 Azure 監視器相關資源的安全性考量，以及如何限制對這些資源所包含的資料進行存取。</span><span class="sxs-lookup"><span data-stu-id="3aa91-107">It then discusses security considerations for your Azure Monitor-related resources and how you can limit access to the data they contain.</span></span>

## <a name="built-in-monitoring-roles"></a><span data-ttu-id="3aa91-108">內建的監視角色</span><span class="sxs-lookup"><span data-stu-id="3aa91-108">Built-in monitoring roles</span></span>
<span data-ttu-id="3aa91-109">Azure 監視器的內建角色是專為協助限制存取訂用帳戶中的資源所設計，同時仍可讓負責監視基礎結構的人員取得及設定他們所需的資料。</span><span class="sxs-lookup"><span data-stu-id="3aa91-109">Azure Monitor’s built-in roles are designed to help limit access to resources in a subscription while still enabling those responsible for monitoring infrastructure to obtain and configure the data they need.</span></span> <span data-ttu-id="3aa91-110">Azure 監視器提供兩個現成的角色︰監視讀取器和監視參與者。</span><span class="sxs-lookup"><span data-stu-id="3aa91-110">Azure Monitor provides two out-of-the-box roles: A Monitoring Reader and a Monitoring Contributor.</span></span>

### <a name="monitoring-reader"></a><span data-ttu-id="3aa91-111">監視讀取器</span><span class="sxs-lookup"><span data-stu-id="3aa91-111">Monitoring Reader</span></span>
<span data-ttu-id="3aa91-112">受指派監視讀取器角色的人員可以檢視訂用帳戶中所有的監視資料，但無法修改任何資源或編輯與監視資源相關的任何設定。</span><span class="sxs-lookup"><span data-stu-id="3aa91-112">People assigned the Monitoring Reader role can view all monitoring data in a subscription but cannot modify any resource or edit any settings related to monitoring resources.</span></span> <span data-ttu-id="3aa91-113">這個角色適用於組織中的使用者，例如支援或作業工程師，這些人員必須能夠︰</span><span class="sxs-lookup"><span data-stu-id="3aa91-113">This role is appropriate for users in an organization, such as support or operations engineers, who need to be able to:</span></span>

* <span data-ttu-id="3aa91-114">在入口網站中檢視監視儀表板，並建立自己的私人監視儀表板。</span><span class="sxs-lookup"><span data-stu-id="3aa91-114">View monitoring dashboards in the portal and create their own private monitoring dashboards.</span></span>
* <span data-ttu-id="3aa91-115">使用 [Azure 監視器 REST API](https://msdn.microsoft.com/library/azure/dn931930.aspx)、[PowerShell cmdlets](insights-powershell-samples.md) 或[跨平台 CLI](insights-cli-samples.md) 查詢度量。</span><span class="sxs-lookup"><span data-stu-id="3aa91-115">Query for metrics using the [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931930.aspx), [PowerShell cmdlets](insights-powershell-samples.md), or [cross-platform CLI](insights-cli-samples.md).</span></span>
* <span data-ttu-id="3aa91-116">使用入口網站、Azure 監視器 REST API、PowerShell Cmdlets 或跨平台 CLI 查詢活動記錄檔。</span><span class="sxs-lookup"><span data-stu-id="3aa91-116">Query the Activity Log using the portal, Azure Monitor REST API, PowerShell cmdlets, or cross-platform CLI.</span></span>
* <span data-ttu-id="3aa91-117">檢視用於資源的 [診斷設定](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) 。</span><span class="sxs-lookup"><span data-stu-id="3aa91-117">View the [diagnostic settings](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) for a resource.</span></span>
* <span data-ttu-id="3aa91-118">檢視用於訂用帳戶的 [記錄檔設定檔](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) 。</span><span class="sxs-lookup"><span data-stu-id="3aa91-118">View the [log profile](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) for a subscription.</span></span>
* <span data-ttu-id="3aa91-119">檢視自動調整設定。</span><span class="sxs-lookup"><span data-stu-id="3aa91-119">View autoscale settings.</span></span>
* <span data-ttu-id="3aa91-120">檢視警示活動和設定。</span><span class="sxs-lookup"><span data-stu-id="3aa91-120">View alert activity and settings.</span></span>
* <span data-ttu-id="3aa91-121">存取 Application Insights 資料，並檢視 AI 分析中的資料。</span><span class="sxs-lookup"><span data-stu-id="3aa91-121">Access Application Insights data and view data in AI Analytics.</span></span>
* <span data-ttu-id="3aa91-122">搜尋 Log Analytics (OMS) 工作區資料，包括工作區的使用狀況資料。</span><span class="sxs-lookup"><span data-stu-id="3aa91-122">Search Log Analytics (OMS) workspace data including usage data for the workspace.</span></span>
* <span data-ttu-id="3aa91-123">檢視 Log Analytics (OMS) 管理群組。</span><span class="sxs-lookup"><span data-stu-id="3aa91-123">View Log Analytics (OMS) management groups.</span></span>
* <span data-ttu-id="3aa91-124">擷取 Log Analytics (OMS) 搜尋結構描述。</span><span class="sxs-lookup"><span data-stu-id="3aa91-124">Retrieve the Log Analytics (OMS) search schema.</span></span>
* <span data-ttu-id="3aa91-125">列出 Log Analytics (OMS) 智慧套件。</span><span class="sxs-lookup"><span data-stu-id="3aa91-125">List Log Analytics (OMS) intelligence packs.</span></span>
* <span data-ttu-id="3aa91-126">擷取並執行 Log Analytics (OMS) 已儲存的搜尋。</span><span class="sxs-lookup"><span data-stu-id="3aa91-126">Retrieve and execute Log Analytics (OMS) saved searches.</span></span>
* <span data-ttu-id="3aa91-127">擷取 Log Analytics (OMS) 儲存體組態。</span><span class="sxs-lookup"><span data-stu-id="3aa91-127">Retrieve the Log Analytics (OMS) storage configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="3aa91-128">此角色不會對已串流至事件中樞或儲存在儲存體帳戶中的記錄檔資料授予讀取權限。</span><span class="sxs-lookup"><span data-stu-id="3aa91-128">This role does not give read access to log data that has been streamed to an event hub or stored in a storage account.</span></span> <span data-ttu-id="3aa91-129">[請參閱下方](#security-considerations-for-monitoring-data) 以取得設定存取這些資源的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="3aa91-129">[See below](#security-considerations-for-monitoring-data) for information on configuring access to these resources.</span></span>
> 
> 

### <a name="monitoring-contributor"></a><span data-ttu-id="3aa91-130">監視參與者</span><span class="sxs-lookup"><span data-stu-id="3aa91-130">Monitoring Contributor</span></span>
<span data-ttu-id="3aa91-131">受指派監視參與者角色的人員可以檢視訂用帳戶中所有的監視資料，並建立或修改監視設定，但無法修改任何其他資源。</span><span class="sxs-lookup"><span data-stu-id="3aa91-131">People assigned the Monitoring Contributor role can view all monitoring data in a subscription and create or modify monitoring settings, but cannot modify any other resources.</span></span> <span data-ttu-id="3aa91-132">此角色是監視讀取者角色的超集，且適用於組織的監視團隊成員或受管理的服務提供者，這些服務提供者除了上述的權限之外，也必須能夠︰</span><span class="sxs-lookup"><span data-stu-id="3aa91-132">This role is a superset of the Monitoring Reader role, and is appropriate for members of an organization’s monitoring team or managed service providers who, in addition to the permissions above, also need to be able to:</span></span>

* <span data-ttu-id="3aa91-133">將監視儀表板發佈為共用儀表板。</span><span class="sxs-lookup"><span data-stu-id="3aa91-133">Publish monitoring dashboards as a shared dashboard.</span></span>
* <span data-ttu-id="3aa91-134">設定用於資源的[診斷設定](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings)。*</span><span class="sxs-lookup"><span data-stu-id="3aa91-134">Set [diagnostic settings](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) for a resource.*</span></span>
* <span data-ttu-id="3aa91-135">設定用於訂用帳戶的[記錄檔設定檔](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile)。*</span><span class="sxs-lookup"><span data-stu-id="3aa91-135">Set the [log profile](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) for a subscription.*</span></span>
* <span data-ttu-id="3aa91-136">設定警示活動和設定。</span><span class="sxs-lookup"><span data-stu-id="3aa91-136">Set alert activity and settings.</span></span>
* <span data-ttu-id="3aa91-137">建立 Application Insights web 測試和元件。</span><span class="sxs-lookup"><span data-stu-id="3aa91-137">Create Application Insights web tests and components.</span></span>
* <span data-ttu-id="3aa91-138">列出 Log Analytics (OMS) 工作區共用金鑰。</span><span class="sxs-lookup"><span data-stu-id="3aa91-138">List Log Analytics (OMS) workspace shared keys.</span></span>
* <span data-ttu-id="3aa91-139">啟用或停用 Log Analytics (OMS) 智慧套件。</span><span class="sxs-lookup"><span data-stu-id="3aa91-139">Enable or disable Log Analytics (OMS) intelligence packs.</span></span>
* <span data-ttu-id="3aa91-140">建立及刪除及執行 Log Analytics (OMS) 已儲存的搜尋。</span><span class="sxs-lookup"><span data-stu-id="3aa91-140">Create and delete and execute Log Analytics (OMS) saved searches.</span></span>
* <span data-ttu-id="3aa91-141">建立及刪除 Log Analytics (OMS) 儲存體組態。</span><span class="sxs-lookup"><span data-stu-id="3aa91-141">Create and delete the Log Analytics (OMS) storage configuration.</span></span>

<span data-ttu-id="3aa91-142">*使用者也必須在目標資源上個別授與 ListKeys 權限 (儲存體帳戶或事件中樞命名空間)，以設定記錄檔設定檔或診斷設定。</span><span class="sxs-lookup"><span data-stu-id="3aa91-142">*user must also separately be granted ListKeys permission on the target resource (storage account or event hub namespace) to set a log profile or diagnostic setting.</span></span>

> [!NOTE]
> <span data-ttu-id="3aa91-143">此角色不會對已串流至事件中樞或儲存在儲存體帳戶中的記錄檔資料授予讀取權限。</span><span class="sxs-lookup"><span data-stu-id="3aa91-143">This role does not give read access to log data that has been streamed to an event hub or stored in a storage account.</span></span> <span data-ttu-id="3aa91-144">[請參閱下方](#security-considerations-for-monitoring-data) 以取得設定存取這些資源的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="3aa91-144">[See below](#security-considerations-for-monitoring-data) for information on configuring access to these resources.</span></span>
> 
> 

## <a name="monitoring-permissions-and-custom-rbac-roles"></a><span data-ttu-id="3aa91-145">監視權限和自訂的 RBAC 角色</span><span class="sxs-lookup"><span data-stu-id="3aa91-145">Monitoring permissions and custom RBAC roles</span></span>
<span data-ttu-id="3aa91-146">如果上述的內建角色不符合您團隊的確切需求，您可以使用更精確的權限 [建立自訂的 RBAC 角色](../active-directory/role-based-access-control-custom-roles.md) 。</span><span class="sxs-lookup"><span data-stu-id="3aa91-146">If the above built-in roles don’t meet the exact needs of your team, you can [create a custom RBAC role](../active-directory/role-based-access-control-custom-roles.md) with more granular permissions.</span></span> <span data-ttu-id="3aa91-147">以下是一般 Azure 監視器 RBAC 作業及其說明。</span><span class="sxs-lookup"><span data-stu-id="3aa91-147">Below are the common Azure Monitor RBAC operations with their descriptions.</span></span>

| <span data-ttu-id="3aa91-148">作業</span><span class="sxs-lookup"><span data-stu-id="3aa91-148">Operation</span></span> | <span data-ttu-id="3aa91-149">說明</span><span class="sxs-lookup"><span data-stu-id="3aa91-149">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3aa91-150">Microsoft.Insights/AlertRules/[讀取、寫入、刪除]</span><span class="sxs-lookup"><span data-stu-id="3aa91-150">Microsoft.Insights/AlertRules/[Read, Write, Delete]</span></span> |<span data-ttu-id="3aa91-151">讀取/寫入/刪除警示規則。</span><span class="sxs-lookup"><span data-stu-id="3aa91-151">Read/write/delete alert rules.</span></span> |
| <span data-ttu-id="3aa91-152">Microsoft.Insights/AlertRules/Incidents/Read</span><span class="sxs-lookup"><span data-stu-id="3aa91-152">Microsoft.Insights/AlertRules/Incidents/Read</span></span> |<span data-ttu-id="3aa91-153">列出警示規則的事件 (觸發的警示規則歷程記錄)。</span><span class="sxs-lookup"><span data-stu-id="3aa91-153">List incidents (history of the alert rule being triggered) for alert rules.</span></span> <span data-ttu-id="3aa91-154">這僅適用於入口網站。</span><span class="sxs-lookup"><span data-stu-id="3aa91-154">This only applies to the portal.</span></span> |
| <span data-ttu-id="3aa91-155">Microsoft.Insights/AutoscaleSettings/[讀取、寫入、刪除]</span><span class="sxs-lookup"><span data-stu-id="3aa91-155">Microsoft.Insights/AutoscaleSettings/[Read, Write, Delete]</span></span> |<span data-ttu-id="3aa91-156">讀取/寫入/刪除自動調整設定。</span><span class="sxs-lookup"><span data-stu-id="3aa91-156">Read/write/delete autoscale settings.</span></span> |
| <span data-ttu-id="3aa91-157">Microsoft.Insights/DiagnosticSettings/[讀取、寫入、刪除]</span><span class="sxs-lookup"><span data-stu-id="3aa91-157">Microsoft.Insights/DiagnosticSettings/[Read, Write, Delete]</span></span> |<span data-ttu-id="3aa91-158">讀取/寫入/刪除診斷設定。</span><span class="sxs-lookup"><span data-stu-id="3aa91-158">Read/write/delete diagnostic settings.</span></span> |
| <span data-ttu-id="3aa91-159">Microsoft.Insights/eventtypes/digestevents/Read</span><span class="sxs-lookup"><span data-stu-id="3aa91-159">Microsoft.Insights/eventtypes/digestevents/Read</span></span> |<span data-ttu-id="3aa91-160">此為使用者需要透過入口網站存取活動記錄檔時所需的權限。</span><span class="sxs-lookup"><span data-stu-id="3aa91-160">This permission is necessary for users who need access to Activity Logs via the portal.</span></span> |
| <span data-ttu-id="3aa91-161">Microsoft.Insights/eventtypes/values/Read</span><span class="sxs-lookup"><span data-stu-id="3aa91-161">Microsoft.Insights/eventtypes/values/Read</span></span> |<span data-ttu-id="3aa91-162">列出訂用帳戶中的活動記錄檔事件 (管理事件)。</span><span class="sxs-lookup"><span data-stu-id="3aa91-162">List Activity Log events (management events) in a subscription.</span></span> <span data-ttu-id="3aa91-163">此權限適用於以程式設計方式存取和入口網站存取活動記錄檔。</span><span class="sxs-lookup"><span data-stu-id="3aa91-163">This permission is applicable to both programmatic and portal access to the Activity Log.</span></span> |
| <span data-ttu-id="3aa91-164">Microsoft.Insights/LogDefinitions/Read</span><span class="sxs-lookup"><span data-stu-id="3aa91-164">Microsoft.Insights/LogDefinitions/Read</span></span> |<span data-ttu-id="3aa91-165">此為使用者需要透過入口網站存取活動記錄檔時所需的權限。</span><span class="sxs-lookup"><span data-stu-id="3aa91-165">This permission is necessary for users who need access to Activity Logs via the portal.</span></span> |
| <span data-ttu-id="3aa91-166">Microsoft.Insights/MetricDefinitions/Read</span><span class="sxs-lookup"><span data-stu-id="3aa91-166">Microsoft.Insights/MetricDefinitions/Read</span></span> |<span data-ttu-id="3aa91-167">讀取度量定義 (可用資源的度量類型清單)。</span><span class="sxs-lookup"><span data-stu-id="3aa91-167">Read metric definitions (list of available metric types for a resource).</span></span> |
| <span data-ttu-id="3aa91-168">Microsoft.Insights/Metrics/Read</span><span class="sxs-lookup"><span data-stu-id="3aa91-168">Microsoft.Insights/Metrics/Read</span></span> |<span data-ttu-id="3aa91-169">讀取資源的度量。</span><span class="sxs-lookup"><span data-stu-id="3aa91-169">Read metrics for a resource.</span></span> |

> [!NOTE]
> <span data-ttu-id="3aa91-170">存取警示、診斷設定和資源的度量需要使用者具有資源類型和該資源範圍的讀取權限。</span><span class="sxs-lookup"><span data-stu-id="3aa91-170">Access to alerts, diagnostic settings, and metrics for a resource requires that the user has Read access to the resource type and scope of that resource.</span></span> <span data-ttu-id="3aa91-171">建立 (「寫入」) 封存至儲存體帳戶或串流至事件中樞的診斷設定或記錄檔設定檔的使用者也需要在目標資源上擁有 ListKeys 權限。</span><span class="sxs-lookup"><span data-stu-id="3aa91-171">Creating (“write”) a diagnostic setting or log profile that archives to a storage account or streams to event hubs requires the user to also have ListKeys permission on the target resource.</span></span>
> 
> 

<span data-ttu-id="3aa91-172">例如，您可以使用上述資料表針對「活動記錄檔讀取器」建立如下的自訂 RBAC 角色︰</span><span class="sxs-lookup"><span data-stu-id="3aa91-172">For example, using the above table you could create a custom RBAC role for an “Activity Log Reader” like this:</span></span>

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

## <a name="security-considerations-for-monitoring-data"></a><span data-ttu-id="3aa91-173">監視資料的安全性考量</span><span class="sxs-lookup"><span data-stu-id="3aa91-173">Security considerations for monitoring data</span></span>
<span data-ttu-id="3aa91-174">監視資料 (尤其是記錄檔)，可以包含機密資訊，例如 IP 位址或使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="3aa91-174">Monitoring data—particularly log files—can contain sensitive information, such as IP addresses or user names.</span></span> <span data-ttu-id="3aa91-175">來自 Azure 的監視資料有三種基本形式︰</span><span class="sxs-lookup"><span data-stu-id="3aa91-175">Monitoring data from Azure comes in three basic forms:</span></span>

1. <span data-ttu-id="3aa91-176">活動記錄檔，會描述您 Azure 訂用帳戶上所有的控制層面動作。</span><span class="sxs-lookup"><span data-stu-id="3aa91-176">The Activity Log, which describes all control-plane actions on your Azure subscription.</span></span>
2. <span data-ttu-id="3aa91-177">診斷記錄檔，是由資源發出的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="3aa91-177">Diagnostic Logs, which are logs emitted by a resource.</span></span>
3. <span data-ttu-id="3aa91-178">度量，是由資源發出。</span><span class="sxs-lookup"><span data-stu-id="3aa91-178">Metrics, which are emitted by resources.</span></span>

<span data-ttu-id="3aa91-179">這三種資料類型都可以儲存在儲存體帳戶或串流到事件中樞，兩者都是一般用途的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="3aa91-179">All three of these data types can be stored in a storage account or streamed to Event Hub, both of which are general-purpose Azure resources.</span></span> <span data-ttu-id="3aa91-180">由於這些是一般用途的資源，因此對其進行建立、刪除及存取通常是保留給系統管理員的特殊權限作業。</span><span class="sxs-lookup"><span data-stu-id="3aa91-180">Because these are general-purpose resources, creating, deleting, and accessing them is a privileged operation usually reserved for an administrator.</span></span> <span data-ttu-id="3aa91-181">我們建議您對監視相關的資源使用下列作法以防止誤用︰</span><span class="sxs-lookup"><span data-stu-id="3aa91-181">We suggest that you use the following practices for monitoring-related resources to prevent misuse:</span></span>

* <span data-ttu-id="3aa91-182">針對監視資料使用單一、專用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3aa91-182">Use a single, dedicated storage account for monitoring data.</span></span> <span data-ttu-id="3aa91-183">如果您需要將監視資料分成多個儲存體帳戶，切勿將儲存體帳戶的監視及非監視資料使用情況進行共用，因為這可能會不小心讓只需要存取監視資料 (例如，</span><span class="sxs-lookup"><span data-stu-id="3aa91-183">If you need to separate monitoring data into multiple storage accounts, never share usage of a storage account between monitoring and non-monitoring data, as this may inadvertently give those who only need access to monitoring data (eg.</span></span> <span data-ttu-id="3aa91-184">第三方 SIEM) 的使用者得以存取非監視資料。</span><span class="sxs-lookup"><span data-stu-id="3aa91-184">a third-party SIEM) access to non-monitoring data.</span></span>
* <span data-ttu-id="3aa91-185">以上述相同的原因在所有的診斷設定中使用單一、專用的服務匯流排或事件中樞命名空間。</span><span class="sxs-lookup"><span data-stu-id="3aa91-185">Use a single, dedicated Service Bus or Event Hub namespace across all diagnostic settings for the same reason as above.</span></span>
* <span data-ttu-id="3aa91-186">將存取監視相關的儲存體帳戶或事件中樞保存在不同的資源群組中，以限制存取它們，並在監視角色上 [使用範圍](../active-directory/role-based-access-control-what-is.md#basics-of-access-management-in-azure) 來限制只能存取該資源群組。</span><span class="sxs-lookup"><span data-stu-id="3aa91-186">Limit access to monitoring-related storage accounts or event hubs by keeping them in a separate resource group, and [use scope](../active-directory/role-based-access-control-what-is.md#basics-of-access-management-in-azure) on your monitoring roles to limit access to only that resource group.</span></span>
* <span data-ttu-id="3aa91-187">當使用者只需要存取監視資料時，切勿針對訂用帳戶範圍內的儲存體帳戶或事件中樞授與 ListKeys 權限。</span><span class="sxs-lookup"><span data-stu-id="3aa91-187">Never grant the ListKeys permission for either storage accounts or event hubs at subscription scope when a user only needs access to monitoring data.</span></span> <span data-ttu-id="3aa91-188">反之，對資源或資源群組 (如果您有專用的監視資源群組) 範圍內的使用者授與這些權限。</span><span class="sxs-lookup"><span data-stu-id="3aa91-188">Instead, give these permissions to the user at a resource or resource group (if you have a dedicated monitoring resource group) scope.</span></span>

### <a name="limiting-access-to-monitoring-related-storage-accounts"></a><span data-ttu-id="3aa91-189">限制存取監控相關的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="3aa91-189">Limiting access to monitoring-related storage accounts</span></span>
<span data-ttu-id="3aa91-190">當使用者或應用程式需要存取儲存體帳戶中的監視資料時，您應該在包含具有 Blob 儲存體服務層級唯讀存取權的監視資料儲存體帳戶上 [產生帳戶 SAS](https://msdn.microsoft.com/library/azure/mt584140.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="3aa91-190">When a user or application needs access to monitoring data in a storage account, you should [generate an Account SAS](https://msdn.microsoft.com/library/azure/mt584140.aspx) on the storage account that contains monitoring data with service-level read-only access to blob storage.</span></span> <span data-ttu-id="3aa91-191">在 PowerShell 中，它看起來應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="3aa91-191">In PowerShell, this might look like:</span></span>

```powershell
$context = New-AzureStorageContext -ConnectionString "[connection string for your monitoring Storage Account]"
$token = New-AzureStorageAccountSASToken -ResourceType Service -Service Blob -Permission "rl" -Context $context
```

<span data-ttu-id="3aa91-192">接著，您可將權杖提供給需要從該儲存體帳戶進行讀取的實體，且它可以從該儲存體帳戶中的所有 blob 進行列出並讀取。</span><span class="sxs-lookup"><span data-stu-id="3aa91-192">You can then give the token to the entity that needs to read from that storage account, and it can list and read from all blobs in that storage account.</span></span>

<span data-ttu-id="3aa91-193">或者，如果您需要使用 RBAC 控制此權限，可以在該特定儲存體帳戶上對該實體授與 Microsoft.Storage/storageAccounts/listkeys/action 權限。</span><span class="sxs-lookup"><span data-stu-id="3aa91-193">Alternatively, if you need to control this permission with RBAC, you can grant that entity the Microsoft.Storage/storageAccounts/listkeys/action permission on that particular storage account.</span></span> <span data-ttu-id="3aa91-194">對於需要設定診斷設定或記錄檔設定檔以封存至儲存體帳戶的使用者而言，這是必要的。</span><span class="sxs-lookup"><span data-stu-id="3aa91-194">This is necessary for users who need to be able to set a diagnostic setting or log profile to archive to a storage account.</span></span> <span data-ttu-id="3aa91-195">例如，針對只需要從一個儲存體帳戶進行讀取的使用者或應用程式，您可以建立下列自訂 RBAC 角色︰</span><span class="sxs-lookup"><span data-stu-id="3aa91-195">For example, you could create the following custom RBAC role for a user or application that only needs to read from one storage account:</span></span>

```powershell
$role = Get-AzureRmRoleDefinition "Reader"
$role.Id = $null
$role.Name = "Monitoring Storage Account Reader"
$role.Description = "Can get the storage account keys for a monitoring storage account."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Storage/storageAccounts/listkeys/action")
$role.Actions.Add("Microsoft.Storage/storageAccounts/Read")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/mySubscription/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/myMonitoringStorageAccount")
New-AzureRmRoleDefinition -Role $role 
```

> [!WARNING]
> <span data-ttu-id="3aa91-196">ListKeys 權限可讓使用者列出主要和次要的儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="3aa91-196">The ListKeys permission enables the user to list the primary and secondary storage account keys.</span></span> <span data-ttu-id="3aa91-197">在該儲存體帳戶中所有已簽署的服務 (blob、佇列、資料表、檔案) 中，這些金鑰會對使用者授與所有已簽署的權限 (讀取、寫入、建立 blob、刪除 blob 等)。</span><span class="sxs-lookup"><span data-stu-id="3aa91-197">These keys grant the user all signed permissions (read, write, create blobs, delete blobs, etc.) across all signed services (blob, queue, table, file) in that storage account.</span></span> <span data-ttu-id="3aa91-198">我們建議盡可能使用上述的帳戶 SAS。</span><span class="sxs-lookup"><span data-stu-id="3aa91-198">We recommend using an Account SAS described above when possible.</span></span>
> 
> 

### <a name="limiting-access-to-monitoring-related-event-hubs"></a><span data-ttu-id="3aa91-199">限制存取監控相關的事件中樞</span><span class="sxs-lookup"><span data-stu-id="3aa91-199">Limiting access to monitoring-related event hubs</span></span>
<span data-ttu-id="3aa91-200">可以使用事件中樞採用類似的模式，但您必須先建立專用的接聽授權規則。</span><span class="sxs-lookup"><span data-stu-id="3aa91-200">A similar pattern can be followed with event hubs, but first you need to create a dedicated Listen authorization rule.</span></span> <span data-ttu-id="3aa91-201">如果您要對僅需要接聽監視相關事件中樞的應用程式授與存取權，請執行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="3aa91-201">If you want to grant access to an application that only needs to listen to monitoring-related event hubs, do the following:</span></span>

1. <span data-ttu-id="3aa91-202">在針對只有接聽宣告的串流監視資料所建立的事件中樞上建立共用存取原則。</span><span class="sxs-lookup"><span data-stu-id="3aa91-202">Create a shared access policy on the event hub(s) that were created for streaming monitoring data with only Listen claims.</span></span> <span data-ttu-id="3aa91-203">這可以在入口網站中完成。</span><span class="sxs-lookup"><span data-stu-id="3aa91-203">This can be done in the portal.</span></span> <span data-ttu-id="3aa91-204">例如，您可能會將它稱為 “monitoringReadOnly”。</span><span class="sxs-lookup"><span data-stu-id="3aa91-204">For example, you might call it “monitoringReadOnly.”</span></span> <span data-ttu-id="3aa91-205">可能的話，您會直接將該金鑰提供給取用者，並略過下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="3aa91-205">If possible, you will want to give that key directly to the consumer and skip the next step.</span></span>
2. <span data-ttu-id="3aa91-206">如果取用者必須能夠取得金鑰臨機操作，則對使用者授與該事件中樞的 ListKeys 動作。</span><span class="sxs-lookup"><span data-stu-id="3aa91-206">If the consumer needs to be able to get the key ad-hoc, grant the user the ListKeys action for that event hub.</span></span> <span data-ttu-id="3aa91-207">對於需要設定診斷設定或記錄檔設定檔以串流至事件中樞的使用者而言，這也是必要的。</span><span class="sxs-lookup"><span data-stu-id="3aa91-207">This is also necessary for users who need to be able to set a diagnostic setting or log profile to stream to event hubs.</span></span> <span data-ttu-id="3aa91-208">例如，您可能會建立 RBAC 規則︰</span><span class="sxs-lookup"><span data-stu-id="3aa91-208">For example, you might create an RBAC rule:</span></span>
   
   ```powershell
   $role = Get-AzureRmRoleDefinition "Reader"
   $role.Id = $null
   $role.Name = "Monitoring Event Hub Listener"
   $role.Description = "Can get the key to listen to an event hub streaming monitoring data."
   $role.Actions.Clear()
   $role.Actions.Add("Microsoft.ServiceBus/namespaces/authorizationrules/listkeys/action")
   $role.Actions.Add("Microsoft.ServiceBus/namespaces/Read")
   $role.AssignableScopes.Clear()
   $role.AssignableScopes.Add("/subscriptions/mySubscription/resourceGroups/myResourceGroup/providers/Microsoft.ServiceBus/namespaces/mySBNameSpace")
   New-AzureRmRoleDefinition -Role $role 
   ```

## <a name="next-steps"></a><span data-ttu-id="3aa91-209">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3aa91-209">Next steps</span></span>
* [<span data-ttu-id="3aa91-210">深入了解 RBAC 和 Resource Manager 中的權限</span><span class="sxs-lookup"><span data-stu-id="3aa91-210">Read about RBAC and permissions in Resource Manager</span></span>](../active-directory/role-based-access-control-what-is.md)
* [<span data-ttu-id="3aa91-211">閱讀 Azure 中的監視概觀</span><span class="sxs-lookup"><span data-stu-id="3aa91-211">Read the overview of monitoring in Azure</span></span>](monitoring-overview.md)

