---
title: "Azure 入口網站中 Azure 搜尋服務的服務管理"
description: "使用 Azure 入口網站來管理 Azure 搜尋服務 (Microsoft Azure 上的雲端託管搜尋服務)。"
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: c87d1fdd-b3b8-4702-a753-6d7e29dbe0a2
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/18/2017
ms.author: heidist
ms.openlocfilehash: c293de5b43103c8cbec01f61a26b8b28ac7e9116
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="service-administration-for-azure-search-in-the-azure-portal"></a><span data-ttu-id="0d199-103">Azure 入口網站中 Azure 搜尋服務的服務管理</span><span class="sxs-lookup"><span data-stu-id="0d199-103">Service administration for Azure Search in the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0d199-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="0d199-104">Portal</span></span>](search-manage.md)
> * [<span data-ttu-id="0d199-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0d199-105">PowerShell</span></span>](search-manage-powershell.md)
> * [<span data-ttu-id="0d199-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="0d199-106">.NET SDK</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.management.search)
> * <span data-ttu-id="0d199-107">[Python (英文)](https://pypi.python.org/pypi/azure-mgmt-search/0.1.0)></span><span class="sxs-lookup"><span data-stu-id="0d199-107">[Python](https://pypi.python.org/pypi/azure-mgmt-search/0.1.0)></span></span> 

<span data-ttu-id="0d199-108">Azure 搜尋服務是完全受管理、以雲端為基礎的搜尋服務，用來在自訂應用程式內建置豐富的搜尋經驗。</span><span class="sxs-lookup"><span data-stu-id="0d199-108">Azure Search is a fully managed, cloud-based search service used for building a rich search experience into custom apps.</span></span> <span data-ttu-id="0d199-109">本文章涵蓋服務管理  工作，可供您在 [Azure 入口網站](https://portal.azure.com)中針對已佈建的搜尋服務執行。</span><span class="sxs-lookup"><span data-stu-id="0d199-109">This article covers the *service administration* tasks that you can perform in the [Azure portal](https://portal.azure.com) for a search service that you've already provisioned.</span></span> <span data-ttu-id="0d199-110">*Service administration* 原先的設計是輕量級的，限制為下列工作︰</span><span class="sxs-lookup"><span data-stu-id="0d199-110">*Service administration* is lightweight by design, limited to the following tasks:</span></span>

* <span data-ttu-id="0d199-111">管理及保護 API 金鑰  (用於讀取或寫入您的服務存取權) 的存取權。</span><span class="sxs-lookup"><span data-stu-id="0d199-111">Manage and secure access to the *api-keys* used for read or write access to your service.</span></span>
* <span data-ttu-id="0d199-112">變更資料分割和複本的配置來調整服務容量。</span><span class="sxs-lookup"><span data-stu-id="0d199-112">Adjust service capacity by changing the allocation of partitions and replicas.</span></span>
* <span data-ttu-id="0d199-113">監視資源使用量，相對於服務層的最大限制。</span><span class="sxs-lookup"><span data-stu-id="0d199-113">Monitor resource usage, relative to maximum limits of your service tier.</span></span>

<span data-ttu-id="0d199-114">**不在範圍中**</span><span class="sxs-lookup"><span data-stu-id="0d199-114">**Not in scope**</span></span> 

<span data-ttu-id="0d199-115"> (或索引管理) 是指搜尋流量分析以了解查詢磁碟區等作業、找出使用者所搜尋的詞彙，以及搜尋結果將客戶引導至您索引中特定文件的成功率。</span><span class="sxs-lookup"><span data-stu-id="0d199-115">*Content management* (or index management) refers to operations such as analyzing search traffic to understand query volume, discover which terms people search for, and how successful search results are in guiding customers to specific documents in your index.</span></span> <span data-ttu-id="0d199-116">如需此區域的說明，請參閱 [Azure 搜尋服務的搜尋流量分析](search-traffic-analytics.md)。</span><span class="sxs-lookup"><span data-stu-id="0d199-116">For help in this area, see [Search Traffic Analytics for Azure Search](search-traffic-analytics.md).</span></span>

<span data-ttu-id="0d199-117"> 也已超出本文的範圍。</span><span class="sxs-lookup"><span data-stu-id="0d199-117">*Query performance* is also beyond the scope of this article.</span></span> <span data-ttu-id="0d199-118">如需詳細資訊，請參閱[監視使用量和查詢度量](search-monitor-usage.md)和[效能和最佳化](search-performance-optimization.md)。</span><span class="sxs-lookup"><span data-stu-id="0d199-118">For more information, see [Monitor usage and query metrics](search-monitor-usage.md) and [Performance and optimization](search-performance-optimization.md).</span></span>

<span data-ttu-id="0d199-119">「升級」不是管理工作。</span><span class="sxs-lookup"><span data-stu-id="0d199-119">*Upgrade* is not an administrative task.</span></span> <span data-ttu-id="0d199-120">因為資源是在佈建服務時進行配置，所以移動到其他層需要新的服務。</span><span class="sxs-lookup"><span data-stu-id="0d199-120">Because resources are allocated when the service is provisioned, moving to a different tier requires a new service.</span></span> <span data-ttu-id="0d199-121">如需詳細資料，請參閱[建立 Azure 搜尋服務](search-create-service-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="0d199-121">For details, see [Create an Azure Search service](search-create-service-portal.md).</span></span>

<a id="admin-rights"></a>

## <a name="administrator-rights"></a><span data-ttu-id="0d199-122">系統管理員權限</span><span class="sxs-lookup"><span data-stu-id="0d199-122">Administrator rights</span></span>
<span data-ttu-id="0d199-123">Azure 訂用帳戶管理員或共同管理員可以佈建或解除委任服務本身。</span><span class="sxs-lookup"><span data-stu-id="0d199-123">Provisioning or decommissioning the service itself can be done by an Azure subscription administrator or co-administrator.</span></span>

<span data-ttu-id="0d199-124">在服務中，任何有服務 URL 和系統管理 API 金鑰存取權的人員，都有服務的讀寫存取權限。</span><span class="sxs-lookup"><span data-stu-id="0d199-124">Within a service, anyone with access to the service URL and an admin api-key has read-write access to the service.</span></span> <span data-ttu-id="0d199-125">讀寫存取權限提供新增、刪除或修改伺服器物件的能力，這些物件包含 API 金鑰、索引、索引子、資料來源、排程，以及透過 [RBAC 定義的角色](#rbac)實作的角色指派。</span><span class="sxs-lookup"><span data-stu-id="0d199-125">Read-write access provides the ability to add, delete, or modify server objects, including api-keys, indexes, indexers, data sources, schedules, and role assignments as implemented through [RBAC-defined roles](#rbac).</span></span>

<span data-ttu-id="0d199-126">與 Azure 搜尋服務互動的所有使用者皆屬於下列模式之一︰讀寫存取服務 (系統管理員權限) 或唯讀存取服務 (查詢權限)。</span><span class="sxs-lookup"><span data-stu-id="0d199-126">All user interaction with Azure Search falls within one of these modes: read-write access to the service (administrator rights), or read-only access to the service (query rights).</span></span> <span data-ttu-id="0d199-127">如需詳細資訊，請參閱[管理 API 金鑰](#manage-keys)。</span><span class="sxs-lookup"><span data-stu-id="0d199-127">For more information, see [Manage the api-keys](#manage-keys).</span></span>

<a id="sys-info"></a>

## <a name="set-rbac-roles-for-administrative-access"></a><span data-ttu-id="0d199-128">設定系統管理存取權的 RBAC 角色</span><span class="sxs-lookup"><span data-stu-id="0d199-128">Set RBAC roles for administrative access</span></span>
<span data-ttu-id="0d199-129">Azure 特別為透過入口網站或 Resource Manager API 管理的所有服務提供[全域角色型授權模型](../active-directory/role-based-access-control-configure.md) 。</span><span class="sxs-lookup"><span data-stu-id="0d199-129">Azure provides a [global role-based authorization model](../active-directory/role-based-access-control-configure.md) for all services managed through the portal or Resource Manager APIs.</span></span> <span data-ttu-id="0d199-130">「擁有者」、「參與者」和「讀取者」角色可針對指派給各角色的 Active Directory 使用者、群組和安全性主體，決定服務管理層級。</span><span class="sxs-lookup"><span data-stu-id="0d199-130">Owner, Contributor, and Reader roles determine the level of service administration for Active Directory users, groups, and security principals assigned to each role.</span></span> 

<span data-ttu-id="0d199-131">針對 Azure 搜尋服務，RBAC 權限會決定下列管理工作︰</span><span class="sxs-lookup"><span data-stu-id="0d199-131">For Azure Search, RBAC permissions determine the following administrative tasks:</span></span>

| <span data-ttu-id="0d199-132">角色</span><span class="sxs-lookup"><span data-stu-id="0d199-132">Role</span></span> | <span data-ttu-id="0d199-133">工作</span><span class="sxs-lookup"><span data-stu-id="0d199-133">Task</span></span> |
| --- | --- |
| <span data-ttu-id="0d199-134">擁有者</span><span class="sxs-lookup"><span data-stu-id="0d199-134">Owner</span></span> |<span data-ttu-id="0d199-135">建立或刪除服務或服務上的任何物件，包括 api 索引鍵、索引、索引子、索引子資料來源和索引子排程。</span><span class="sxs-lookup"><span data-stu-id="0d199-135">Create or delete the service or any object on the service, including api-keys, indexes, indexers, indexer data sources, and indexer schedules.</span></span><p><span data-ttu-id="0d199-136">檢視服務狀態，包括計數和儲存體大小。</span><span class="sxs-lookup"><span data-stu-id="0d199-136">View service status, including counts and storage size.</span></span><p><span data-ttu-id="0d199-137">新增或刪除角色成員資格 (只有「擁有者」可以管理角色成員資格)。</span><span class="sxs-lookup"><span data-stu-id="0d199-137">Add or delete role membership (only an Owner can manage role membership).</span></span><p><span data-ttu-id="0d199-138">訂用帳戶管理員和服務擁有者在擁有者角色具有自動成員資格。</span><span class="sxs-lookup"><span data-stu-id="0d199-138">Subscription administrators and service owners have automatic membership in the Owners role.</span></span> |
| <span data-ttu-id="0d199-139">參與者</span><span class="sxs-lookup"><span data-stu-id="0d199-139">Contributor</span></span> |<span data-ttu-id="0d199-140">與「擁有者」相同層級的存取權，減去 RBAC 角色管理。</span><span class="sxs-lookup"><span data-stu-id="0d199-140">Same level of access as Owner, minus RBAC role management.</span></span> <span data-ttu-id="0d199-141">例如，參與者可以檢視和重新產生 `api-key`，但不能修改角色成員資格。</span><span class="sxs-lookup"><span data-stu-id="0d199-141">For example, a Contributor can view and regenerate `api-key`, but cannot modify role memberships.</span></span> |
| <span data-ttu-id="0d199-142">讀取者</span><span class="sxs-lookup"><span data-stu-id="0d199-142">Reader</span></span> |<span data-ttu-id="0d199-143">檢視服務狀態及查詢金鑰。</span><span class="sxs-lookup"><span data-stu-id="0d199-143">View service status and query keys.</span></span> <span data-ttu-id="0d199-144">這個角色的成員無法變更服務組態，也無法檢視管理金鑰。</span><span class="sxs-lookup"><span data-stu-id="0d199-144">Members of this role cannot change service configuration, nor can they view admin keys.</span></span> |

<span data-ttu-id="0d199-145">角色不會授與服務端點的存取權限。</span><span class="sxs-lookup"><span data-stu-id="0d199-145">Roles do not grant access rights to the service endpoint.</span></span> <span data-ttu-id="0d199-146">搜尋服務作業 (例如索引管理、索引母體擴展，以及搜尋資料查詢) 可透過 api-key 而非角色來控制。</span><span class="sxs-lookup"><span data-stu-id="0d199-146">Search service operations, such as index management, index population, and queries on search data, are controlled through api-keys, not roles.</span></span> <span data-ttu-id="0d199-147">如需詳細資訊，請參閱[什麼是角色存取控制](../active-directory/role-based-access-control-what-is.md)中的「管理授權與資料作業」。</span><span class="sxs-lookup"><span data-stu-id="0d199-147">For more information, see "Authorization for management versus data operations" in [What is Role-based access control](../active-directory/role-based-access-control-what-is.md).</span></span>

<a id="secure-keys"></a>
## <a name="logging-and-system-information"></a><span data-ttu-id="0d199-148">記錄與系統資訊</span><span class="sxs-lookup"><span data-stu-id="0d199-148">Logging and system information</span></span>
<span data-ttu-id="0d199-149">Azure 搜尋服務不會透過入口網站或程式設計介面公開個別服務的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="0d199-149">Azure Search does not expose log files for an individual service either through the portal or programmatic interfaces.</span></span> <span data-ttu-id="0d199-150">在基本層以上，Microsoft 會監視所有 Azure 搜尋服務以達到服務等級協定 (SLA) 的 99.9%可用性。</span><span class="sxs-lookup"><span data-stu-id="0d199-150">At the Basic tier and above, Microsoft monitors all Azure Search services for 99.9% availability per service level agreements (SLA).</span></span> <span data-ttu-id="0d199-151">如果服務很慢或要求輸送量低於 SLA 閾值，支援團隊會檢閱他們可用的記錄檔並解決問題。</span><span class="sxs-lookup"><span data-stu-id="0d199-151">If the service is slow or request throughput falls below SLA thresholds, support teams review the log files available to them and address the issue.</span></span>

<span data-ttu-id="0d199-152">就關於您服務的一般資訊而言，您可以透過下列方式取得資訊︰</span><span class="sxs-lookup"><span data-stu-id="0d199-152">In terms of general information about your service, you can obtain information in the following ways:</span></span>

* <span data-ttu-id="0d199-153">在入口網站中、在服務儀表板上、透過通知、屬性和狀態訊息。</span><span class="sxs-lookup"><span data-stu-id="0d199-153">In the portal, on the service dashboard, through notifications, properties, and status messages.</span></span>
* <span data-ttu-id="0d199-154">使用 [PowerShell](search-manage-powershell.md) 或 [Management REST API](https://docs.microsoft.com/rest/api/searchmanagement/) 來[取得服務屬性](https://docs.microsoft.com/rest/api/searchmanagement/services)，或索引資源使用狀況的狀態。</span><span class="sxs-lookup"><span data-stu-id="0d199-154">Using [PowerShell](search-manage-powershell.md) or the [Management REST API](https://docs.microsoft.com/rest/api/searchmanagement/) to [get service properties](https://docs.microsoft.com/rest/api/searchmanagement/services), or status on index resource usage.</span></span>
* <span data-ttu-id="0d199-155">如先前所述，透過[搜尋流量分析](search-traffic-analytics.md)。</span><span class="sxs-lookup"><span data-stu-id="0d199-155">Via [search traffic analytics](search-traffic-analytics.md), as noted previously.</span></span>

<a id="manage-keys"></a>

## <a name="manage-api-keys"></a><span data-ttu-id="0d199-156">管理 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="0d199-156">Manage api-keys</span></span>
<span data-ttu-id="0d199-157">搜尋服務的所有要求需要專為您的服務而產生的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="0d199-157">All requests to a search service need an api-key that was generated specifically for your service.</span></span> <span data-ttu-id="0d199-158">此 API 金鑰是驗證存取您搜尋服務端點的唯一機制。</span><span class="sxs-lookup"><span data-stu-id="0d199-158">This api-key is the sole mechanism for authenticating access to your search service endpoint.</span></span> 

<span data-ttu-id="0d199-159">API 金鑰是由隨機產生的數字和字母所組成的字串。</span><span class="sxs-lookup"><span data-stu-id="0d199-159">An api-key is a string composed of randomly generated numbers and letters.</span></span> <span data-ttu-id="0d199-160">您可以透過 [RBAC 權限](#rbac)來刪除或讀取金鑰，但無法以使用者定義的密碼取代金鑰。</span><span class="sxs-lookup"><span data-stu-id="0d199-160">Through [RBAC permissions](#rbac), you can delete or read the keys, but you can't replace a key with a user-defined password.</span></span> 

<span data-ttu-id="0d199-161">存取搜尋服務的金鑰有兩種類型：</span><span class="sxs-lookup"><span data-stu-id="0d199-161">Two types of keys are used to access your search service:</span></span>

* <span data-ttu-id="0d199-162">管理員 (適用於服務的任何讀寫作業)</span><span class="sxs-lookup"><span data-stu-id="0d199-162">Admin (valid for any read-write operation against the service)</span></span>
* <span data-ttu-id="0d199-163">查詢 (適用於唯讀作業，例如針對索引的查詢)</span><span class="sxs-lookup"><span data-stu-id="0d199-163">Query (valid for read-only operations such as queries against an index)</span></span>

<span data-ttu-id="0d199-164">與當佈建服務時會建立管理員 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="0d199-164">An admin api-key is created when the service is provisioned.</span></span> <span data-ttu-id="0d199-165">有兩個管理員金鑰，指定為主要和次要以將它們保持在各自的位置，但事實上，它們是可互換。</span><span class="sxs-lookup"><span data-stu-id="0d199-165">There are two admin keys, designated as *primary* and *secondary* to keep them straight, but in fact they are interchangeable.</span></span> <span data-ttu-id="0d199-166">每個服務有兩個管理員金鑰，以便您在轉換其中一個時不會無法存取您的服務。</span><span class="sxs-lookup"><span data-stu-id="0d199-166">Each service has two admin keys so that you can roll one over without losing access to your service.</span></span> <span data-ttu-id="0d199-167">您可以重新產生任何一種管理員金鑰，但您無法增加管理員金鑰的總數量。</span><span class="sxs-lookup"><span data-stu-id="0d199-167">You can regenerate either admin key, but you cannot add to the total admin key count.</span></span> <span data-ttu-id="0d199-168">每個搜尋服務最多有 2 個管理員金鑰。</span><span class="sxs-lookup"><span data-stu-id="0d199-168">There is a maximum of two admin keys per search service.</span></span>

<span data-ttu-id="0d199-169">查詢金鑰是專為直接呼叫搜尋的用戶端應用程式所設計。</span><span class="sxs-lookup"><span data-stu-id="0d199-169">Query keys are designed for client applications that call Search directly.</span></span> <span data-ttu-id="0d199-170">您最多可以建立 50 個查詢金鑰。</span><span class="sxs-lookup"><span data-stu-id="0d199-170">You can create up to 50 query keys.</span></span> <span data-ttu-id="0d199-171">在應用程式程式碼中，您可以指定搜尋 URL 和查詢 API 金鑰以允許唯讀存取服務。</span><span class="sxs-lookup"><span data-stu-id="0d199-171">In application code, you specify the search URL and a query api-key to allow read-only access to the service.</span></span> <span data-ttu-id="0d199-172">應用程式程式碼也會指定應用程式所使用的索引。</span><span class="sxs-lookup"><span data-stu-id="0d199-172">Your application code also specifies the index used by your application.</span></span> <span data-ttu-id="0d199-173">端點、可供唯讀存取的 API 金鑰以及目標索引共同定義來自用戶端應用程式連接的範圍和存取層級。</span><span class="sxs-lookup"><span data-stu-id="0d199-173">Together, the endpoint, an api-key for read-only access, and a target index define the scope and access level of the connection from your client application.</span></span>

<span data-ttu-id="0d199-174">若要取得或重新產生 API 金鑰，請開啟服務儀表板。</span><span class="sxs-lookup"><span data-stu-id="0d199-174">To get or regenerate api-keys, open the service dashboard.</span></span> <span data-ttu-id="0d199-175">按一下 [金鑰] 以滑動開啟金鑰管理頁面。</span><span class="sxs-lookup"><span data-stu-id="0d199-175">Click **KEYS** to slide open the key management page.</span></span> <span data-ttu-id="0d199-176">重新產生或建立金鑰的命令位於頁面頂端。</span><span class="sxs-lookup"><span data-stu-id="0d199-176">Commands for regenerating or creating keys are at the top of the page.</span></span> <span data-ttu-id="0d199-177">依預設，只會建立管理員金鑰。</span><span class="sxs-lookup"><span data-stu-id="0d199-177">By default, only admin keys are created.</span></span> <span data-ttu-id="0d199-178">查詢 API 金鑰必須以手動方式建立。</span><span class="sxs-lookup"><span data-stu-id="0d199-178">Query api-keys must be created manually.</span></span>

 ![][9]

<a id="rbac"></a>

## <a name="secure-api-keys"></a><span data-ttu-id="0d199-179">保護 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="0d199-179">Secure api-keys</span></span>
<span data-ttu-id="0d199-180">藉由限制透過入口網站或 Resource Manager 介面 (PowerShell 或命令列介面) 的存取來確保金鑰安全性。</span><span class="sxs-lookup"><span data-stu-id="0d199-180">Key security is ensured by restricting access via the portal or Resource Manager interfaces (PowerShell or command-line interface).</span></span> <span data-ttu-id="0d199-181">如前所述，訂用帳戶系統管理員可以檢視及重新產生所有的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="0d199-181">As noted, subscription administrators can view and regenerate all api-keys.</span></span> <span data-ttu-id="0d199-182">為以防萬一，請檢閱角色指派以了解誰具有管理員金鑰存取權。</span><span class="sxs-lookup"><span data-stu-id="0d199-182">As a precaution, review role assignments to understand who has access to the admin keys.</span></span>

1. <span data-ttu-id="0d199-183">在服務儀表板中，按一下 [存取] 圖示以滑動開啟 [使用者] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="0d199-183">In the service dashboard, click the Access icon to slide open the Users blade.</span></span>
   ![][7]
2. <span data-ttu-id="0d199-184">在 [使用者] 中，檢閱現有的角色指派。</span><span class="sxs-lookup"><span data-stu-id="0d199-184">In Users, review existing role assignments.</span></span> <span data-ttu-id="0d199-185">如預期，訂用帳戶管理員已經透過擁有者角色具有服務的完整存取權。</span><span class="sxs-lookup"><span data-stu-id="0d199-185">As expected, Subscription admins already have full access to the service via the Owner role.</span></span>
3. <span data-ttu-id="0d199-186">若要進一步鑽研，按一下 [訂用帳戶管理員] ，然後展開角色指派清單以查看誰在您的搜尋服務上具有共同系統管理權限。</span><span class="sxs-lookup"><span data-stu-id="0d199-186">To drill further, click **Subscription admins** and then expand the role assignment list to see who has co-administration rights on your search service.</span></span>

<span data-ttu-id="0d199-187">檢視存取權限的另一個方法是按一下 [使用者] 刀鋒視窗上的 [角色]。</span><span class="sxs-lookup"><span data-stu-id="0d199-187">Another way to view access permissions is to click **Roles** on the Users blade.</span></span> <span data-ttu-id="0d199-188">這麼做會顯示可用的角色以及使用者數目或指派給每個角色的群組數目。</span><span class="sxs-lookup"><span data-stu-id="0d199-188">Doing so displays available roles and the number of users or groups assigned to each role.</span></span>

<a id="sub-5"></a>

## <a name="monitor-resource-usage"></a><span data-ttu-id="0d199-189">監視資源使用量</span><span class="sxs-lookup"><span data-stu-id="0d199-189">Monitor resource usage</span></span>
<span data-ttu-id="0d199-190">在儀表板中，僅能針對服務儀表板中顯示的資訊，以及一些透過查詢服務取得的度量進行資源監視。</span><span class="sxs-lookup"><span data-stu-id="0d199-190">In the dashboard, resource monitoring is limited to the information shown in the service dashboard and a few metrics that you can obtain by querying the service.</span></span> <span data-ttu-id="0d199-191">在服務儀表板上的使用量區段中，您可以快速判斷資料分割資源層級是否適合您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d199-191">On the service dashboard, in the Usage section, you can quickly determine whether partition resource levels are adequate for your application.</span></span>

<span data-ttu-id="0d199-192">使用搜尋服務 API 可取得文件和索引的計數。</span><span class="sxs-lookup"><span data-stu-id="0d199-192">Using the Search Service API, you can get a count on documents and indexes.</span></span> <span data-ttu-id="0d199-193">根據價格層不同，會有些與這些計數相關聯的固定限制。</span><span class="sxs-lookup"><span data-stu-id="0d199-193">There are hard limits associated with these counts based on the pricing tier.</span></span> <span data-ttu-id="0d199-194">如需詳細資訊，請參閱[搜尋服務限制](search-limits-quotas-capacity.md)。</span><span class="sxs-lookup"><span data-stu-id="0d199-194">For more information, see [Search service limits](search-limits-quotas-capacity.md).</span></span> 

* [<span data-ttu-id="0d199-195">取得索引統計資料</span><span class="sxs-lookup"><span data-stu-id="0d199-195">Get Index Statistics</span></span>](https://docs.microsoft.com/rest/api/searchservice/Get-Index-Statistics)
* [<span data-ttu-id="0d199-196">文件計數</span><span class="sxs-lookup"><span data-stu-id="0d199-196">Count Documents</span></span>](https://docs.microsoft.com/rest/api/searchservice/count-documents)

> [!NOTE]
> <span data-ttu-id="0d199-197">快取行為可暫時放寬限制。</span><span class="sxs-lookup"><span data-stu-id="0d199-197">Caching behaviors can temporarily overstate a limit.</span></span> <span data-ttu-id="0d199-198">例如，使用共用服務時，您可能會看到文件計數超過固定限制的 10,000 份文件。</span><span class="sxs-lookup"><span data-stu-id="0d199-198">For example, when using the shared service, you might see a document count over the hard limit of 10,000 documents.</span></span> <span data-ttu-id="0d199-199">這種「超出限制」是暫時的，並且將會在下一次的限制強制檢核中偵測出來。</span><span class="sxs-lookup"><span data-stu-id="0d199-199">The overstatement is temporary and will be detected on the next limit enforcement check.</span></span> 
> 
> 

## <a name="disaster-recovery-and-service-outages"></a><span data-ttu-id="0d199-200">災害復原和服務中斷</span><span class="sxs-lookup"><span data-stu-id="0d199-200">Disaster recovery and service outages</span></span>

<span data-ttu-id="0d199-201">雖然我們可以回收您的資料，但如果中斷發生在叢集或資料中心層級，Azure 搜尋服務將無法提供立即的服務容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="0d199-201">Although we can salvage your data, Azure Search does not provide instant failover of the service if there is an outage at the cluster or data center level.</span></span> <span data-ttu-id="0d199-202">如果叢集在資料中心內失敗，作業小組將會偵測並處理以還原服務。</span><span class="sxs-lookup"><span data-stu-id="0d199-202">If a cluster fails in the data center, the operations team will detect and work to restore service.</span></span> <span data-ttu-id="0d199-203">您會在服務還原期間經歷停機。</span><span class="sxs-lookup"><span data-stu-id="0d199-203">You will experience downtime during service restoration.</span></span> <span data-ttu-id="0d199-204">您可以根據[服務等級協定 (SLA)](https://azure.microsoft.com/support/legal/sla/search/v1_0/) 要求服務信用額度作為無法使用服務的補償。</span><span class="sxs-lookup"><span data-stu-id="0d199-204">You can request service credits to compensate for service unavailability per the [Service Level Agreement (SLA)](https://azure.microsoft.com/support/legal/sla/search/v1_0/).</span></span> 

<span data-ttu-id="0d199-205">如果在遇到 Microsoft 控制之外的災難性失敗時，需要持續的服務，您可以在不同區域[佈建額外的服務](search-create-service-portal.md)並實作異地複寫策略，以確保索引在所有服務之間皆具有完整備援。</span><span class="sxs-lookup"><span data-stu-id="0d199-205">If continuous service is required in the event of catastrophic failures outside of Microsoft’s control, you could [provision an additional service](search-create-service-portal.md) in a different region and implement a geo-replication strategy to ensure indexes are fully redundant across all services.</span></span>

<span data-ttu-id="0d199-206">使用[索引子](search-indexer-overview.md)來填入及重新整理索引的客戶，可以透過使用相同資料來源的地理特定索引子來處理災害復原。</span><span class="sxs-lookup"><span data-stu-id="0d199-206">Customers who use [indexers](search-indexer-overview.md) to populate and refresh indexes can handle disaster recovery through geo-specific indexers leveraging the same data source.</span></span> <span data-ttu-id="0d199-207">在不同區域中的兩個服務 (每個都執行一個索引子)，可以從相同相同的資料來源建立索引，以達到異地備援的目的。</span><span class="sxs-lookup"><span data-stu-id="0d199-207">Two services in different regions, each running an indexer, could index from the same data source to achieve geo-redundancy.</span></span> <span data-ttu-id="0d199-208">如果從同為異地備援的資料來源建立索引，請留意，Azure 搜尋服務索引子只能在主要複本執行遞增索引。</span><span class="sxs-lookup"><span data-stu-id="0d199-208">If you are indexing from data sources that are also geo-redundant, be aware that Azure Search indexers can only perform incremental indexing from primary replicas.</span></span> <span data-ttu-id="0d199-209">在容錯移轉事件中，請務必將索引子重新指向新的主要複本。</span><span class="sxs-lookup"><span data-stu-id="0d199-209">In a failover event, be sure to re-point the indexer to the new primary replica.</span></span> 

<span data-ttu-id="0d199-210">若不使用索引子，您可以使用應用程式程式碼將物件和資料平行推送到不同的搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="0d199-210">If you do not use indexers, you would use your application code to push objects and data to different search services in parallel.</span></span> <span data-ttu-id="0d199-211">如需詳細資訊，請參閱 [Azure 搜尋服務中的效能和最佳化](search-performance-optimization.md)。</span><span class="sxs-lookup"><span data-stu-id="0d199-211">For more information, see [Performance and optimization in Azure Search](search-performance-optimization.md).</span></span>

## <a name="backup-and-restore"></a><span data-ttu-id="0d199-212">備份與還原</span><span class="sxs-lookup"><span data-stu-id="0d199-212">Backup and restore</span></span>

<span data-ttu-id="0d199-213">因為 Azure 搜尋服務不是主要的資料儲存體解決方案，所以我們不提供自助備份及還原的正式機制。</span><span class="sxs-lookup"><span data-stu-id="0d199-213">Because Azure Search is not a primary data storage solution, we do not provide a formal mechanism for self-service backup and restore.</span></span> <span data-ttu-id="0d199-214">如果不小心刪除索引，您用於建立及填入索引的應用程式程式碼是現行的還原選項。</span><span class="sxs-lookup"><span data-stu-id="0d199-214">Your application code used for creating and populating an index is the de facto restore option if you delete an index by mistake.</span></span> 

<span data-ttu-id="0d199-215">若要重建索引，請先將索引刪除 (假設它存在)，在服務中重新建立索引，然後從您的主要資料存放區擷取資料以重新載入。</span><span class="sxs-lookup"><span data-stu-id="0d199-215">To rebuild an index, you would delete it (assuming it exists), recreate the index in the service, and reload by retrieving data from your primary data store.</span></span> <span data-ttu-id="0d199-216">此外，如果發生區域性中斷，您也可以連絡[客戶支援]()以回收索引。</span><span class="sxs-lookup"><span data-stu-id="0d199-216">Alternatively, you can reach out to [customer support]() to salvage indexes if there is a regional outage.</span></span>


<a id="scale"></a>

## <a name="scale-up-or-down"></a><span data-ttu-id="0d199-217">擴大或縮小規模</span><span class="sxs-lookup"><span data-stu-id="0d199-217">Scale up or down</span></span>
<span data-ttu-id="0d199-218">每個搜尋服務都會以一個複本和一個資料分割的最小值開始執行。</span><span class="sxs-lookup"><span data-stu-id="0d199-218">Every search service starts with a minimum of one replica and one partition.</span></span> <span data-ttu-id="0d199-219">如果您註冊的[層提供專用資源](search-limits-quotas-capacity.md)，請按一下服務儀表板中的 [級別] 圖格來調整資源使用量。</span><span class="sxs-lookup"><span data-stu-id="0d199-219">If you signed up for a [tier that provides dedicated resources](search-limits-quotas-capacity.md), click the **SCALE** tile in the service dashboard to adjust resource usage.</span></span>

<span data-ttu-id="0d199-220">當您透過任何資源加入處理能力時，服務即會自動使用這些資源。</span><span class="sxs-lookup"><span data-stu-id="0d199-220">When you add capacity through either resource, the service uses them automatically.</span></span> <span data-ttu-id="0d199-221">您無須再執行其他動作，但在新資源產生作用前，會有些許的延遲。</span><span class="sxs-lookup"><span data-stu-id="0d199-221">No further action is required on your part, but there is a slight delay before the impact of the new resource is realized.</span></span> <span data-ttu-id="0d199-222">佈建其他資源需要 15 分鐘或更久的時間。</span><span class="sxs-lookup"><span data-stu-id="0d199-222">It can take 15 minutes or more to provision additional resources.</span></span>

 ![][10]

### <a name="add-replicas"></a><span data-ttu-id="0d199-223">新增複本</span><span class="sxs-lookup"><span data-stu-id="0d199-223">Add replicas</span></span>
<span data-ttu-id="0d199-224">系統會藉由新增複本來增加每秒查詢 (QPS) 數量或達到高可用性。</span><span class="sxs-lookup"><span data-stu-id="0d199-224">Increasing queries per second (QPS) or achieving high availability is done by adding replicas.</span></span> <span data-ttu-id="0d199-225">每個複本都有一個索引的副本，因此再新增一個複本就會轉譯出可用來處理服務查詢要求的索引。</span><span class="sxs-lookup"><span data-stu-id="0d199-225">Each replica has one copy of an index, so adding one more replica translates to one more index available for handling service query requests.</span></span> <span data-ttu-id="0d199-226">高可用性至少需要 3 個複本 (如需詳細資訊，請參閱[容量規劃](search-capacity-planning.md) )。</span><span class="sxs-lookup"><span data-stu-id="0d199-226">A minimum of 3 replicas are required for high availability (see [Capacity Planning](search-capacity-planning.md) for details).</span></span>

<span data-ttu-id="0d199-227">有許多複本的搜尋服務可透過大量索引來達到查詢要求的負載平衡。</span><span class="sxs-lookup"><span data-stu-id="0d199-227">A search service having more replicas can load balance query requests over a larger number of indexes.</span></span> <span data-ttu-id="0d199-228">假設有一定等級的查詢量，當有愈多服務要求可用的索引副本時，查詢輸送量的速度就會愈快。</span><span class="sxs-lookup"><span data-stu-id="0d199-228">Given a level of query volume, query throughput is going to be faster when there are more copies of the index available to service the request.</span></span> <span data-ttu-id="0d199-229">如果您有查詢延遲的經驗，可以期待線上有其他複本時，對效能所造成的正面影響。</span><span class="sxs-lookup"><span data-stu-id="0d199-229">If you are experiencing query latency, you can expect a positive impact on performance once the additional replicas are online.</span></span>

<span data-ttu-id="0d199-230">雖然當您新增複本時會提高輸送量，但並不會以您新增至服務之複本的正好兩倍或三倍來計算提高程度。</span><span class="sxs-lookup"><span data-stu-id="0d199-230">Although query throughput goes up as you add replicas, it does not precisely double or triple as you add replicas to your service.</span></span> <span data-ttu-id="0d199-231">所有搜尋應用程式皆會因為影響查詢效能的外部因素而受影響。</span><span class="sxs-lookup"><span data-stu-id="0d199-231">All search applications are subject to external factors that can impinge on query performance.</span></span> <span data-ttu-id="0d199-232">複雜的查詢和網路延遲是造成查詢回應次數變化的兩個因素。</span><span class="sxs-lookup"><span data-stu-id="0d199-232">Complex queries and network latency are two factors that contribute to variations in query response times.</span></span>

### <a name="add-partitions"></a><span data-ttu-id="0d199-233">新增資料分割</span><span class="sxs-lookup"><span data-stu-id="0d199-233">Add partitions</span></span>
<span data-ttu-id="0d199-234">大部分的服務應用程式內建需要多個複本，而非資料分割。</span><span class="sxs-lookup"><span data-stu-id="0d199-234">Most service applications have a built-in need for more replicas rather than partitions.</span></span> <span data-ttu-id="0d199-235">如果您註冊的是標準服務，對於需要新增文件計數的案例，可以新增資料分割。</span><span class="sxs-lookup"><span data-stu-id="0d199-235">For those cases where an increased document count is required, you can add partitions if you signed up for Standard service.</span></span> <span data-ttu-id="0d199-236">基本層沒有提供額外的資料分割。</span><span class="sxs-lookup"><span data-stu-id="0d199-236">Basic tier does not provide for additional partitions.</span></span>

<span data-ttu-id="0d199-237">在標準層中，資料分割要以 12 的倍數新增 (準確來說是 1、2、3、4、6 或 12)。</span><span class="sxs-lookup"><span data-stu-id="0d199-237">At the Standard tier, partitions are added in multiples of 12 (specifically, 1, 2, 3, 4, 6, or 12).</span></span> <span data-ttu-id="0d199-238">這是分區化的構件。</span><span class="sxs-lookup"><span data-stu-id="0d199-238">This is an artifact of sharding.</span></span> <span data-ttu-id="0d199-239">索引會建立在 12 個分區中，並且可以全部儲存在 1 個資料分割中，或平均分配在 2、3、4、6 或 12 個資料分割中 (每個資料分割分配一個分區)。</span><span class="sxs-lookup"><span data-stu-id="0d199-239">An index is created in 12 shards, which can all be stored on 1 partition or equally divided into 2, 3, 4, 6, or 12 partitions (one shard per partition).</span></span>

### <a name="remove-replicas"></a><span data-ttu-id="0d199-240">移除複本</span><span class="sxs-lookup"><span data-stu-id="0d199-240">Remove replicas</span></span>
<span data-ttu-id="0d199-241">高查詢量期間過後，在搜尋的查詢負載量回到標準時 (例如，假日銷售結束後)，您可以減少複本。</span><span class="sxs-lookup"><span data-stu-id="0d199-241">After periods of high query volumes, you can reduce replicas after search query loads have normalized (for example, after holiday sales are over).</span></span>

<span data-ttu-id="0d199-242">若要這麼做，請將複本滑動軸移回到較低數目即可。</span><span class="sxs-lookup"><span data-stu-id="0d199-242">To do this, move the replica slider back to a lower number.</span></span> <span data-ttu-id="0d199-243">無須再執行其他步驟。</span><span class="sxs-lookup"><span data-stu-id="0d199-243">There are no further steps required on your part.</span></span> <span data-ttu-id="0d199-244">降低複本數量會讓出資料中心內的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0d199-244">Lowering the replica count relinquishes virtual machines in the data center.</span></span> <span data-ttu-id="0d199-245">相較於先前的情況，現在會在較少的 VM 上執行您的查詢和資料擷取作業。</span><span class="sxs-lookup"><span data-stu-id="0d199-245">Your query and data ingestion operations will now run on fewer VMs than before.</span></span> <span data-ttu-id="0d199-246">最小的限制為一個複本。</span><span class="sxs-lookup"><span data-stu-id="0d199-246">The minimum limit is one replica.</span></span>

### <a name="remove-partitions"></a><span data-ttu-id="0d199-247">移除資料分割</span><span class="sxs-lookup"><span data-stu-id="0d199-247">Remove partitions</span></span>
<span data-ttu-id="0d199-248">相較於您無須付出多餘動作就可移除複本，如果您使用的儲存體大於可減少的儲存體，您可能需要完成一些工作。</span><span class="sxs-lookup"><span data-stu-id="0d199-248">In contrast with removing replicas, which requires no extra effort on your part, you might have some work to do if you are using more storage than can be reduced.</span></span> <span data-ttu-id="0d199-249">例如，如果您的解決方案使用三個資料分割，則如果新的儲存空間小於所需，減少為一或兩個資料分割會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="0d199-249">For example, if your solution is using three partitions, downsizing to one or two partitions will generate an error if the new storage space is less than required.</span></span> <span data-ttu-id="0d199-250">如您可能預期的，您可以選擇刪除索引或相關索引內的文件來釋出空間，或保持目前設定。</span><span class="sxs-lookup"><span data-stu-id="0d199-250">As you might expect, your choices are to delete indexes or documents within an associated index to free up space, or keep the current configuration.</span></span>

<span data-ttu-id="0d199-251">沒有任何偵測方法可告訴您哪個索引分區儲存在哪個特定資料分割中。</span><span class="sxs-lookup"><span data-stu-id="0d199-251">There is no detection method that tells you which index shards are stored on specific partitions.</span></span> <span data-ttu-id="0d199-252">每個資料分割提供大約 25 GB 的儲存體，因此您需要將儲存體減少至可讓您擁有的資料分割數量所能容納的大小。</span><span class="sxs-lookup"><span data-stu-id="0d199-252">Each partition provides approximately 25 GB in storage, so you will need to reduce storage to a size that can be accommodated by the number of partitions you have.</span></span> <span data-ttu-id="0d199-253">如果您想還原成一個資料分割，所有 12 個分區皆要能符合。</span><span class="sxs-lookup"><span data-stu-id="0d199-253">If you want to revert to one partition, all 12 shards will need to fit.</span></span>

<span data-ttu-id="0d199-254">若要協助進行未來規劃，您可能需要檢查儲存體 (使用[取得索引統計資料](https://docs.microsoft.com/rest/api/searchservice/Get-Index-Statistics)) 以了解實際上您可以使用的空間大小。</span><span class="sxs-lookup"><span data-stu-id="0d199-254">To help with future planning, you might want to check storage (using [Get Index Statistics](https://docs.microsoft.com/rest/api/searchservice/Get-Index-Statistics)) to see how much you actually used.</span></span> 

<a id="advanced-deployment"></a>

## <a name="best-practices-on-scale-and-deployment"></a><span data-ttu-id="0d199-255">調整和部署的最佳作法</span><span class="sxs-lookup"><span data-stu-id="0d199-255">Best practices on scale and deployment</span></span>
<span data-ttu-id="0d199-256">在這段 30 分鐘的影片中，會檢閱進階部署案例的最佳作法，包括地理位置分散工作負載。</span><span class="sxs-lookup"><span data-stu-id="0d199-256">This 30-minute video reviews best practices for advanced deployment scenarios, including geo-distributed workloads.</span></span> <span data-ttu-id="0d199-257">您也可以查看 [Azure 搜尋服務中的效能和最佳化](search-performance-optimization.md) ，以取得涵蓋相同要點的說明頁面。</span><span class="sxs-lookup"><span data-stu-id="0d199-257">You can also see [Performance and optimization in Azure Search](search-performance-optimization.md) for help pages that cover the same points.</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON319/player]
> 
> 

<a id="next-steps"></a>

## <a name="next-steps"></a><span data-ttu-id="0d199-258">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0d199-258">Next steps</span></span>
<span data-ttu-id="0d199-259">當您了解服務管理背後的概念之後，請考慮使用 [PowerShell](search-manage-powershell.md) 來將工作自動化。</span><span class="sxs-lookup"><span data-stu-id="0d199-259">Once you understand the concepts behind service administration, consider using [PowerShell](search-manage-powershell.md) to automate tasks.</span></span>

<span data-ttu-id="0d199-260">也建議您檢視[效能與最佳化文章](search-performance-optimization.md)。</span><span class="sxs-lookup"><span data-stu-id="0d199-260">We also recommend reviewing the [performance and optimization article](search-performance-optimization.md).</span></span>

<span data-ttu-id="0d199-261">另一個建議是觀看先前小節所提及的影片。</span><span class="sxs-lookup"><span data-stu-id="0d199-261">Another recommendation is to watch the video noted in the previous section.</span></span> <span data-ttu-id="0d199-262">影片涵蓋在本節中所提及技術的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0d199-262">It provides deeper coverage of the techniques mentioned in this section.</span></span>

<!--Image references-->
[7]: ./media/search-manage/rbac-icon.png
[8]: ./media/search-manage/Azure-Search-Manage-1-URL.png
[9]: ./media/search-manage/Azure-Search-Manage-2-Keys.png
[10]: ./media/search-manage/Azure-Search-Manage-3-ScaleUp.png



