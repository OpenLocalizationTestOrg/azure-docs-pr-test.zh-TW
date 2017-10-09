---
title: "透過 Azure 資源健全狀況的資源類型 aaaSupported |Microsoft 文件"
description: "透過 Azure 資源健康狀態支援的資源類型"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: resource-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 03/19/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: a37d5c33f6ef6fdfbce0daf392bc7fa57853c7d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="resource-types-and-health-checks-in-azure-resource-health"></a><span data-ttu-id="d263e-103">Azure 資源健康狀態中的資源類型和健康情況檢查</span><span class="sxs-lookup"><span data-stu-id="d263e-103">Resource types and health checks in Azure resource health</span></span>
<span data-ttu-id="d263e-104">以下是所有的 hello 檢查透過資源健全狀況執行的資源類型的完整清單。</span><span class="sxs-lookup"><span data-stu-id="d263e-104">Below is a complete list of all hello checks executed through resource health by resource types.</span></span>

## <a name="microsoftcacheredisredis"></a><span data-ttu-id="d263e-105">Microsoft.CacheRedis/Redis</span><span class="sxs-lookup"><span data-stu-id="d263e-105">Microsoft.CacheRedis/Redis</span></span>
|<span data-ttu-id="d263e-106">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="d263e-106">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="d263e-107">Hello 快取的所有節點都都已啟動並執行？</span><span class="sxs-lookup"><span data-stu-id="d263e-107">Are all hello Cache nodes up and running?</span></span></li><li><span data-ttu-id="d263e-108">可以快取 hello 從聯繫 hello 資料中心內？</span><span class="sxs-lookup"><span data-stu-id="d263e-108">Can hello Cache be reached from within hello datacenter?</span></span></li><li><span data-ttu-id="d263e-109">已快取達到 hello 的連線數目上限的 hello？</span><span class="sxs-lookup"><span data-stu-id="d263e-109">Has hello Cache reached hello maximum number of connections?</span></span></li><li> <span data-ttu-id="d263e-110">Hello 快取已達可用的記憶體？</span><span class="sxs-lookup"><span data-stu-id="d263e-110">Has hello cache exhausted its available memory?</span></span> </li><li><span data-ttu-id="d263e-111">Hello 快取發生分頁錯誤數目？</span><span class="sxs-lookup"><span data-stu-id="d263e-111">Is hello Cache experiencing a high number of page faults?</span></span></li><li><span data-ttu-id="d263e-112">是在負載過重 hello 快取嗎？</span><span class="sxs-lookup"><span data-stu-id="d263e-112">Is hello Cache under heavy load?</span></span></li></ul>|

## <a name="microsoftcdnprofile"></a><span data-ttu-id="d263e-113">Microsoft.CDN/profile</span><span class="sxs-lookup"><span data-stu-id="d263e-113">Microsoft.CDN/profile</span></span>
|<span data-ttu-id="d263e-114">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="d263e-114">Executed Checks</span></span>|
|---|
|<ul> <li><span data-ttu-id="d263e-115">任何 hello 端點已停止，已移除，或設定錯誤？</span><span class="sxs-lookup"><span data-stu-id="d263e-115">Has any of hello endpoints been stopped, removed, or misconfigured?</span></span></li><li><span data-ttu-id="d263e-116">是 hello 補充入口網站存取 CDN 組態作業？</span><span class="sxs-lookup"><span data-stu-id="d263e-116">Is hello supplemental portal accessible for CDN configuration operations?</span></span></li><li><span data-ttu-id="d263e-117">有進行中傳遞問題以 hello CDN 端點嗎？</span><span class="sxs-lookup"><span data-stu-id="d263e-117">Are there ongoing delivery issues with hello CDN endpoints?</span></span></li><li><span data-ttu-id="d263e-118">使用者可以變更其 CDN 資源的 hello 組態嗎？</span><span class="sxs-lookup"><span data-stu-id="d263e-118">Can users change hello configuration of their CDN resources?</span></span></li><li><span data-ttu-id="d263e-119">組態變更會傳播 hello 預期速率嗎？</span><span class="sxs-lookup"><span data-stu-id="d263e-119">Are configuration changes propagating at hello expected rate?</span></span></li><li><span data-ttu-id="d263e-120">使用者可以管理使用 hello Azure 入口網站、 PowerShell 或 hello API hello CDN 組態嗎？</span><span class="sxs-lookup"><span data-stu-id="d263e-120">Can users manage hello CDN configuration using hello Azure portal, PowerShell, or hello API?</span></span></li> </ul>|

## <a name="microsoftclassiccomputevirtualmachines"></a><span data-ttu-id="d263e-121">Microsoft.classiccompute/virtualmachines</span><span class="sxs-lookup"><span data-stu-id="d263e-121">Microsoft.classiccompute/virtualmachines</span></span>
|<span data-ttu-id="d263e-122">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="d263e-122">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="d263e-123">Hello 主機伺服器已啟動並執行？</span><span class="sxs-lookup"><span data-stu-id="d263e-123">Is hello host server up and running?</span></span></li><li><span data-ttu-id="d263e-124">已完成 hello 主機 OS 開機嗎？</span><span class="sxs-lookup"><span data-stu-id="d263e-124">Has hello host OS booting completed?</span></span></li><li><span data-ttu-id="d263e-125">佈建並開啟電源 hello 虛擬機器容器？</span><span class="sxs-lookup"><span data-stu-id="d263e-125">Is hello virtual machine container provisioned and powered up?</span></span></li><li><span data-ttu-id="d263e-126">有 hello 主機與 hello 儲存體帳戶之間的網路連線嗎？</span><span class="sxs-lookup"><span data-stu-id="d263e-126">Is there network connectivity between hello host and hello storage account?</span></span></li><li><span data-ttu-id="d263e-127">已完成 hello 開機的 hello 客體作業系統？</span><span class="sxs-lookup"><span data-stu-id="d263e-127">Has hello booting of hello guest OS completed?</span></span></li><li><span data-ttu-id="d263e-128">是否有持續性的規劃維護？</span><span class="sxs-lookup"><span data-stu-id="d263e-128">Is there ongoing planned maintenance?</span></span></li></ul>|

## <a name="microsoftcognitiveservicesaccounts"></a><span data-ttu-id="d263e-129">Microsoft.cognitiveservices/accounts</span><span class="sxs-lookup"><span data-stu-id="d263e-129">Microsoft.cognitiveservices/accounts</span></span>
|<span data-ttu-id="d263e-130">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="d263e-130">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="d263e-131">可以 hello 帳戶從聯繫 hello 資料中心內？</span><span class="sxs-lookup"><span data-stu-id="d263e-131">Can hello account be reached from within hello datacenter?</span></span></li><li><span data-ttu-id="d263e-132">是 hello 認知服務資源提供者可用？</span><span class="sxs-lookup"><span data-stu-id="d263e-132">Is hello Cognitive Services Resource Provider available?</span></span></li><li><span data-ttu-id="d263e-133">是 hello 認知可用的服務在 hello 適當區域？</span><span class="sxs-lookup"><span data-stu-id="d263e-133">Is hello Cognitive Service available in hello appropriate region?</span></span></li><li><span data-ttu-id="d263e-134">可以讀取作業 hello 保存 hello 資源的中繼資料的儲存體帳戶上執行？</span><span class="sxs-lookup"><span data-stu-id="d263e-134">Can read operations be performed on hello storage account holding hello resource metadata?</span></span></li><li><span data-ttu-id="d263e-135">已達到 hello API 呼叫配額？</span><span class="sxs-lookup"><span data-stu-id="d263e-135">Has hello API call quota been reached?</span></span></li><li><span data-ttu-id="d263e-136">已達到 hello API 呼叫讀取限制？</span><span class="sxs-lookup"><span data-stu-id="d263e-136">Has hello API call read-limit been reached?</span></span></li></ul>|

## <a name="microsoftcomputevirtualmachines"></a><span data-ttu-id="d263e-137">Microsoft.compute/virtualmachines</span><span class="sxs-lookup"><span data-stu-id="d263e-137">Microsoft.compute/virtualmachines</span></span>
|<span data-ttu-id="d263e-138">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="d263e-138">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="d263e-139">Hello 伺服器上裝載此虛擬機器，且執行？</span><span class="sxs-lookup"><span data-stu-id="d263e-139">Is hello server hosting this virtual machine up and running?</span></span></li><li><span data-ttu-id="d263e-140">已完成 hello 主機 OS 開機嗎？</span><span class="sxs-lookup"><span data-stu-id="d263e-140">Has hello host OS booting completed?</span></span></li><li><span data-ttu-id="d263e-141">佈建並開啟電源 hello 虛擬機器容器？</span><span class="sxs-lookup"><span data-stu-id="d263e-141">Is hello virtual machine container provisioned and powered up?</span></span></li><li><span data-ttu-id="d263e-142">有 hello 主機與 hello 儲存體帳戶之間的網路連線嗎？</span><span class="sxs-lookup"><span data-stu-id="d263e-142">Is there network connectivity between hello host and hello storage account?</span></span></li><li><span data-ttu-id="d263e-143">已完成 hello 開機的 hello 客體作業系統？</span><span class="sxs-lookup"><span data-stu-id="d263e-143">Has hello booting of hello guest OS completed?</span></span></li><li><span data-ttu-id="d263e-144">是否有持續性的規劃維護？</span><span class="sxs-lookup"><span data-stu-id="d263e-144">Is there ongoing planned maintenance?</span></span></li></ul>|

## <a name="microsoftdatalakeanalyticsaccounts"></a><span data-ttu-id="d263e-145">Microsoft.datalakeanalytics/accounts</span><span class="sxs-lookup"><span data-stu-id="d263e-145">Microsoft.datalakeanalytics/accounts</span></span>
|<span data-ttu-id="d263e-146">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="d263e-146">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="d263e-147">使用者送出作業中的 tooData Lake Analytics 可以 hello 區域？</span><span class="sxs-lookup"><span data-stu-id="d263e-147">Can users submit jobs tooData Lake Analytics in hello region?</span></span></li><li><span data-ttu-id="d263e-148">執行基本工作執行並完成成功地在 hello 區域？</span><span class="sxs-lookup"><span data-stu-id="d263e-148">Do basic jobs run and complete successfully in hello region?</span></span></li><li><span data-ttu-id="d263e-149">使用者可以列出 hello 區域中的類別目錄項目嗎？</span><span class="sxs-lookup"><span data-stu-id="d263e-149">Can users list catalog items in hello region?</span></span></li>|


## <a name="microsoftdatalakestoreaccounts"></a><span data-ttu-id="d263e-150">Microsoft.datalakestore/accounts</span><span class="sxs-lookup"><span data-stu-id="d263e-150">Microsoft.datalakestore/accounts</span></span>
|<span data-ttu-id="d263e-151">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="d263e-151">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="d263e-152">使用者可以上傳資料區內 hello tooData 湖存放區嗎？</span><span class="sxs-lookup"><span data-stu-id="d263e-152">Can users upload data tooData Lake Store in hello region?</span></span></li><li><span data-ttu-id="d263e-153">使用者可以從 Data Lake Store hello 區域中下載資料嗎？</span><span class="sxs-lookup"><span data-stu-id="d263e-153">Can users download data from Data Lake Store in hello region?</span></span></li></ul>|

## <a name="microsoftdocumentdbdatabaseaccounts"></a><span data-ttu-id="d263e-154">Microsoft.documentdb/databaseAccounts</span><span class="sxs-lookup"><span data-stu-id="d263e-154">Microsoft.documentdb/databaseAccounts</span></span>
|<span data-ttu-id="d263e-155">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="d263e-155">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="d263e-156">已有任何資料庫或集合的要求不因為 tooa DocumentDB 服務無法使用服務？</span><span class="sxs-lookup"><span data-stu-id="d263e-156">Have there been any database or collection requests not served due tooa DocumentDB service unavailability?</span></span></li><li><span data-ttu-id="d263e-157">已有未處理因為 tooa DocumentDB 服務無法使用任何文件要求嗎？</span><span class="sxs-lookup"><span data-stu-id="d263e-157">Have there been any document requests not served due tooa DocumentDB service unavailability?</span></span></li></ul>|

## <a name="microsoftnetworkconnections"></a><span data-ttu-id="d263e-158">Microsoft.network/connections</span><span class="sxs-lookup"><span data-stu-id="d263e-158">Microsoft.network/connections</span></span>
|<span data-ttu-id="d263e-159">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="d263e-159">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="d263e-160">Hello VPN 通道連線？</span><span class="sxs-lookup"><span data-stu-id="d263e-160">Is hello VPN tunnel connected?</span></span></li><li><span data-ttu-id="d263e-161">Hello 連線中是否有設定衝突？</span><span class="sxs-lookup"><span data-stu-id="d263e-161">Are there configuration conflicts in hello connection?</span></span></li><li><span data-ttu-id="d263e-162">Hello 預先共用的金鑰正確設定嗎？</span><span class="sxs-lookup"><span data-stu-id="d263e-162">Are hello pre-shared keys properly configured?</span></span></li><li><span data-ttu-id="d263e-163">是 hello VPN 在內部部署裝置的連線嗎？</span><span class="sxs-lookup"><span data-stu-id="d263e-163">Is hello VPN on-premise device reachable?</span></span></li><li><span data-ttu-id="d263e-164">Hello IPSec/IKE 安全性原則中是否有不相符？</span><span class="sxs-lookup"><span data-stu-id="d263e-164">Are there mismatches in hello IPSec/IKE security policy?</span></span></li><li><span data-ttu-id="d263e-165">是 hello S2S VPN 連線正確佈建或處於失敗狀態？</span><span class="sxs-lookup"><span data-stu-id="d263e-165">Is hello S2S VPN connection properly provisioned or in a failed state?</span></span></li><li><span data-ttu-id="d263e-166">是 hello VNET 對 VNET 連線正確佈建或處於失敗狀態？</span><span class="sxs-lookup"><span data-stu-id="d263e-166">Is hello VNET-to-VNET connection properly provisioned or in a failed state?</span></span></li></ul>|

## <a name="microsoftnetworkvirtualnetworkgateways"></a><span data-ttu-id="d263e-167">Microsoft.network/virtualNetworkGateways</span><span class="sxs-lookup"><span data-stu-id="d263e-167">Microsoft.network/virtualNetworkGateways</span></span>
|<span data-ttu-id="d263e-168">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="d263e-168">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="d263e-169">是從 hello VPN 閘道 hello 網際網路嗎？</span><span class="sxs-lookup"><span data-stu-id="d263e-169">Is hello VPN gateway reachable from hello internet?</span></span></li><li><span data-ttu-id="d263e-170">會在待命模式 hello VPN 閘道嗎？</span><span class="sxs-lookup"><span data-stu-id="d263e-170">Is hello VPN Gateway in standby mode?</span></span></li><li><span data-ttu-id="d263e-171">Hello VPN 服務是否執行 hello 閘道？</span><span class="sxs-lookup"><span data-stu-id="d263e-171">Is hello VPN service running on hello gateway?</span></span></li></ul>|

## <a name="microsoftnotificationhubsnamespace"></a><span data-ttu-id="d263e-172">Microsoft.NotificationHubs/namespace</span><span class="sxs-lookup"><span data-stu-id="d263e-172">Microsoft.NotificationHubs/namespace</span></span>
|<span data-ttu-id="d263e-173">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="d263e-173">Executed Checks</span></span>|
|---|
|<ul><li> <span data-ttu-id="d263e-174">可以在 hello 命名空間上執行執行階段作業，例如註冊、 安裝或傳送？</span><span class="sxs-lookup"><span data-stu-id="d263e-174">Can runtime operations like registration, installation, or send be performed on hello namespace?</span></span></li></ul>|

## <a name="microsoftpowerbiworkspacecollections"></a><span data-ttu-id="d263e-175">Microsoft.PowerBI/workspaceCollections</span><span class="sxs-lookup"><span data-stu-id="d263e-175">Microsoft.PowerBI/workspaceCollections</span></span>
|<span data-ttu-id="d263e-176">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="d263e-176">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="d263e-177">Hello 主機 OS 已啟動並執行？</span><span class="sxs-lookup"><span data-stu-id="d263e-177">Is hello host OS up and running?</span></span></li><li><span data-ttu-id="d263e-178">是從 hello 資料中心外部連到 hello workspaceCollection？</span><span class="sxs-lookup"><span data-stu-id="d263e-178">Is hello workspaceCollection reachable from outside hello datacenter?</span></span></li><li><span data-ttu-id="d263e-179">是 hello PowerBI 資源提供者可用？</span><span class="sxs-lookup"><span data-stu-id="d263e-179">Is hello PowerBI Resource Provider available?</span></span></li><li><span data-ttu-id="d263e-180">是 hello PowerBI hello 適當區域中可用的服務嗎？</span><span class="sxs-lookup"><span data-stu-id="d263e-180">Is hello PowerBI Service available in hello appropriate region?</span></span></li></ul>|

## <a name="microsoftsearchsearchservices"></a><span data-ttu-id="d263e-181">Microsoft.search/searchServices</span><span class="sxs-lookup"><span data-stu-id="d263e-181">Microsoft.search/searchServices</span></span>
|<span data-ttu-id="d263e-182">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="d263e-182">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="d263e-183">可以在 hello 叢集上執行診斷操作嗎？</span><span class="sxs-lookup"><span data-stu-id="d263e-183">Can diagnostics operations be performed on hello cluster?</span></span></li></ul>|

## <a name="microsoftsqlserverdatabase"></a><span data-ttu-id="d263e-184">Microsoft.SQL/Server/database</span><span class="sxs-lookup"><span data-stu-id="d263e-184">Microsoft.SQL/Server/database</span></span>
|<span data-ttu-id="d263e-185">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="d263e-185">Executed Checks</span></span>|
|---|
|<ul><li> <span data-ttu-id="d263e-186">已有登入 toohello 資料庫嗎？</span><span class="sxs-lookup"><span data-stu-id="d263e-186">Have there been logins toohello database?</span></span></li></ul>|

## <a name="microsoftstreamanalyticsstreamingjobs"></a><span data-ttu-id="d263e-187">Microsoft.StreamAnalytics/streamingjobs</span><span class="sxs-lookup"><span data-stu-id="d263e-187">Microsoft.StreamAnalytics/streamingjobs</span></span>
|<span data-ttu-id="d263e-188">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="d263e-188">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="d263e-189">是所有的 hello 主機是執行向上而執行 hello 作業嗎？</span><span class="sxs-lookup"><span data-stu-id="d263e-189">Are all hello hosts where hello job is executing up and running?</span></span></li><li><span data-ttu-id="d263e-190">已 hello 工作無法 toostart 嗎？</span><span class="sxs-lookup"><span data-stu-id="d263e-190">Was hello job unable toostart?</span></span></li><li><span data-ttu-id="d263e-191">有進行中的執行階段升級嗎？</span><span class="sxs-lookup"><span data-stu-id="d263e-191">Are there ongoing runtime upgrades?</span></span></li><li><span data-ttu-id="d263e-192">是預期的狀態 （例如執行或停止的客戶） 中的 hello 工作嗎？</span><span class="sxs-lookup"><span data-stu-id="d263e-192">Is hello job in an expected state (for example running or stopped by customer)?</span></span></li><li><span data-ttu-id="d263e-193">Hello 作業發現外的記憶體例外狀況？</span><span class="sxs-lookup"><span data-stu-id="d263e-193">Has hello job encountered out of memory exceptions?</span></span></li><li><span data-ttu-id="d263e-194">是否有進行中的排程計算更新？</span><span class="sxs-lookup"><span data-stu-id="d263e-194">Are there ongoing scheduled compute updates?</span></span></li><li><span data-ttu-id="d263e-195">是 hello 執行管理員 （控制計畫） 可用？</span><span class="sxs-lookup"><span data-stu-id="d263e-195">Is hello Execution Manager (control plan) available?</span></span></li></ul>|

## <a name="microsoftwebserverfarms"></a><span data-ttu-id="d263e-196">Microsoft.web/serverFarms</span><span class="sxs-lookup"><span data-stu-id="d263e-196">Microsoft.web/serverFarms</span></span>
|<span data-ttu-id="d263e-197">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="d263e-197">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="d263e-198">Hello 主機伺服器已啟動並執行？</span><span class="sxs-lookup"><span data-stu-id="d263e-198">Is hello host server up and running?</span></span></li><li><span data-ttu-id="d263e-199">網際網路資訊服務是否執行中？</span><span class="sxs-lookup"><span data-stu-id="d263e-199">Is Internet Information Services running?</span></span></li><li><span data-ttu-id="d263e-200">正在執行的 hello 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="d263e-200">Is hello Load balancer running?</span></span></li><li><span data-ttu-id="d263e-201">可以 hello Web 服務計劃從聯繫 hello 資料中心內？</span><span class="sxs-lookup"><span data-stu-id="d263e-201">Can hello Web Service Plan be reached from within hello datacenter?</span></span></li><li><span data-ttu-id="d263e-202">是 hello 儲存體帳戶裝載 hello 站台內容的 hello serverFarm 可用??</span><span class="sxs-lookup"><span data-stu-id="d263e-202">Is hello storage account hosting hello sites content for hello serverFarm  available??</span></span></li></ul>|

## <a name="microsoftwebsites"></a><span data-ttu-id="d263e-203">Microsoft.web/sites</span><span class="sxs-lookup"><span data-stu-id="d263e-203">Microsoft.web/sites</span></span>
|<span data-ttu-id="d263e-204">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="d263e-204">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="d263e-205">Hello 主機伺服器已啟動並執行？</span><span class="sxs-lookup"><span data-stu-id="d263e-205">Is hello host server up and running?</span></span></li><li><span data-ttu-id="d263e-206">網際網路資訊服務是否執行中？</span><span class="sxs-lookup"><span data-stu-id="d263e-206">Is Internet Information server running?</span></span></li><li><span data-ttu-id="d263e-207">正在執行的 hello 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="d263e-207">Is hello Load balancer running?</span></span></li><li><span data-ttu-id="d263e-208">可以 hello Web 應用程式從聯繫 hello 資料中心內？</span><span class="sxs-lookup"><span data-stu-id="d263e-208">Can hello Web App be reached from within hello datacenter?</span></span></li><li><span data-ttu-id="d263e-209">Hello 儲存體帳戶裝載 hello 站台的內容嗎？</span><span class="sxs-lookup"><span data-stu-id="d263e-209">Is hello storage account hosting hello site content available?</span></span></li></ul>|

<span data-ttu-id="d263e-210">請參閱這些資源 toolearn 深入了解資源健全狀況：</span><span class="sxs-lookup"><span data-stu-id="d263e-210">See these resources toolearn more about resource health:</span></span>
-  [<span data-ttu-id="d263e-211">簡介 tooAzure 資源健全狀況</span><span class="sxs-lookup"><span data-stu-id="d263e-211">Introduction tooAzure resource health</span></span>](Resource-health-overview.md)
-  [<span data-ttu-id="d263e-212">關於 Azure 資源健康狀態的常見問題集</span><span class="sxs-lookup"><span data-stu-id="d263e-212">Frequently asked questions about Azure resource health</span></span>](Resource-health-faq.md)

