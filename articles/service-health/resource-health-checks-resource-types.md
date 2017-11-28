---
title: "透過 Azure 資源健全狀況的資源類型 aaaSupported |Microsoft 文件"
description: "透過 Azure 資源健康狀態支援的資源類型"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 03/19/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: fc7bef214702f8ba6954b5aca62236b38023d27a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="resource-types-and-health-checks-in-azure-resource-health"></a><span data-ttu-id="4c5f1-103">Azure 資源健康狀態中的資源類型和健康情況檢查</span><span class="sxs-lookup"><span data-stu-id="4c5f1-103">Resource types and health checks in Azure resource health</span></span>
<span data-ttu-id="4c5f1-104">以下是所有的 hello 檢查透過資源健全狀況執行的資源類型的完整清單。</span><span class="sxs-lookup"><span data-stu-id="4c5f1-104">Below is a complete list of all hello checks executed through resource health by resource types.</span></span>

## <a name="microsoftcacheredisredis"></a><span data-ttu-id="4c5f1-105">Microsoft.CacheRedis/Redis</span><span class="sxs-lookup"><span data-stu-id="4c5f1-105">Microsoft.CacheRedis/Redis</span></span>
|<span data-ttu-id="4c5f1-106">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="4c5f1-106">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="4c5f1-107">Hello 快取的所有節點都都已啟動並執行？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-107">Are all hello Cache nodes up and running?</span></span></li><li><span data-ttu-id="4c5f1-108">可以快取 hello 從聯繫 hello 資料中心內？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-108">Can hello Cache be reached from within hello datacenter?</span></span></li><li><span data-ttu-id="4c5f1-109">已快取達到 hello 的連線數目上限的 hello？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-109">Has hello Cache reached hello maximum number of connections?</span></span></li><li> <span data-ttu-id="4c5f1-110">Hello 快取已達可用的記憶體？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-110">Has hello cache exhausted its available memory?</span></span> </li><li><span data-ttu-id="4c5f1-111">Hello 快取發生分頁錯誤數目？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-111">Is hello Cache experiencing a high number of page faults?</span></span></li><li><span data-ttu-id="4c5f1-112">是在負載過重 hello 快取嗎？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-112">Is hello Cache under heavy load?</span></span></li></ul>|

## <a name="microsoftcdnprofile"></a><span data-ttu-id="4c5f1-113">Microsoft.CDN/profile</span><span class="sxs-lookup"><span data-stu-id="4c5f1-113">Microsoft.CDN/profile</span></span>
|<span data-ttu-id="4c5f1-114">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="4c5f1-114">Executed Checks</span></span>|
|---|
|<ul> <li><span data-ttu-id="4c5f1-115">任何 hello 端點已停止，已移除，或設定錯誤？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-115">Has any of hello endpoints been stopped, removed, or misconfigured?</span></span></li><li><span data-ttu-id="4c5f1-116">是 hello 補充入口網站存取 CDN 組態作業？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-116">Is hello supplemental portal accessible for CDN configuration operations?</span></span></li><li><span data-ttu-id="4c5f1-117">有進行中傳遞問題以 hello CDN 端點嗎？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-117">Are there ongoing delivery issues with hello CDN endpoints?</span></span></li><li><span data-ttu-id="4c5f1-118">使用者可以變更其 CDN 資源的 hello 組態嗎？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-118">Can users change hello configuration of their CDN resources?</span></span></li><li><span data-ttu-id="4c5f1-119">組態變更會傳播 hello 預期速率嗎？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-119">Are configuration changes propagating at hello expected rate?</span></span></li><li><span data-ttu-id="4c5f1-120">使用者可以管理使用 hello Azure 入口網站、 PowerShell 或 hello API hello CDN 組態嗎？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-120">Can users manage hello CDN configuration using hello Azure portal, PowerShell, or hello API?</span></span></li> </ul>|

## <a name="microsoftclassiccomputevirtualmachines"></a><span data-ttu-id="4c5f1-121">Microsoft.classiccompute/virtualmachines</span><span class="sxs-lookup"><span data-stu-id="4c5f1-121">Microsoft.classiccompute/virtualmachines</span></span>
|<span data-ttu-id="4c5f1-122">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="4c5f1-122">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="4c5f1-123">Hello 主機伺服器已啟動並執行？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-123">Is hello host server up and running?</span></span></li><li><span data-ttu-id="4c5f1-124">已完成 hello 主機 OS 開機嗎？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-124">Has hello host OS booting completed?</span></span></li><li><span data-ttu-id="4c5f1-125">佈建並開啟電源 hello 虛擬機器容器？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-125">Is hello virtual machine container provisioned and powered up?</span></span></li><li><span data-ttu-id="4c5f1-126">有 hello 主機與 hello 儲存體帳戶之間的網路連線嗎？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-126">Is there network connectivity between hello host and hello storage account?</span></span></li><li><span data-ttu-id="4c5f1-127">已完成 hello 開機的 hello 客體作業系統？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-127">Has hello booting of hello guest OS completed?</span></span></li><li><span data-ttu-id="4c5f1-128">是否有持續性的規劃維護？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-128">Is there ongoing planned maintenance?</span></span></li></ul>|

## <a name="microsoftcognitiveservicesaccounts"></a><span data-ttu-id="4c5f1-129">Microsoft.cognitiveservices/accounts</span><span class="sxs-lookup"><span data-stu-id="4c5f1-129">Microsoft.cognitiveservices/accounts</span></span>
|<span data-ttu-id="4c5f1-130">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="4c5f1-130">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="4c5f1-131">可以 hello 帳戶從聯繫 hello 資料中心內？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-131">Can hello account be reached from within hello datacenter?</span></span></li><li><span data-ttu-id="4c5f1-132">是 hello 認知服務資源提供者可用？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-132">Is hello Cognitive Services Resource Provider available?</span></span></li><li><span data-ttu-id="4c5f1-133">是 hello 認知可用的服務在 hello 適當區域？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-133">Is hello Cognitive Service available in hello appropriate region?</span></span></li><li><span data-ttu-id="4c5f1-134">可以讀取作業 hello 保存 hello 資源的中繼資料的儲存體帳戶上執行？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-134">Can read operations be performed on hello storage account holding hello resource metadata?</span></span></li><li><span data-ttu-id="4c5f1-135">已達到 hello API 呼叫配額？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-135">Has hello API call quota been reached?</span></span></li><li><span data-ttu-id="4c5f1-136">已達到 hello API 呼叫讀取限制？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-136">Has hello API call read-limit been reached?</span></span></li></ul>|

## <a name="microsoftcomputevirtualmachines"></a><span data-ttu-id="4c5f1-137">Microsoft.compute/virtualmachines</span><span class="sxs-lookup"><span data-stu-id="4c5f1-137">Microsoft.compute/virtualmachines</span></span>
|<span data-ttu-id="4c5f1-138">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="4c5f1-138">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="4c5f1-139">Hello 伺服器上裝載此虛擬機器，且執行？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-139">Is hello server hosting this virtual machine up and running?</span></span></li><li><span data-ttu-id="4c5f1-140">已完成 hello 主機 OS 開機嗎？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-140">Has hello host OS booting completed?</span></span></li><li><span data-ttu-id="4c5f1-141">佈建並開啟電源 hello 虛擬機器容器？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-141">Is hello virtual machine container provisioned and powered up?</span></span></li><li><span data-ttu-id="4c5f1-142">有 hello 主機與 hello 儲存體帳戶之間的網路連線嗎？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-142">Is there network connectivity between hello host and hello storage account?</span></span></li><li><span data-ttu-id="4c5f1-143">已完成 hello 開機的 hello 客體作業系統？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-143">Has hello booting of hello guest OS completed?</span></span></li><li><span data-ttu-id="4c5f1-144">是否有持續性的規劃維護？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-144">Is there ongoing planned maintenance?</span></span></li></ul>|

## <a name="microsoftdatalakeanalyticsaccounts"></a><span data-ttu-id="4c5f1-145">Microsoft.datalakeanalytics/accounts</span><span class="sxs-lookup"><span data-stu-id="4c5f1-145">Microsoft.datalakeanalytics/accounts</span></span>
|<span data-ttu-id="4c5f1-146">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="4c5f1-146">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="4c5f1-147">使用者送出作業中的 tooData Lake Analytics 可以 hello 區域？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-147">Can users submit jobs tooData Lake Analytics in hello region?</span></span></li><li><span data-ttu-id="4c5f1-148">執行基本工作執行並完成成功地在 hello 區域？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-148">Do basic jobs run and complete successfully in hello region?</span></span></li><li><span data-ttu-id="4c5f1-149">使用者可以列出 hello 區域中的類別目錄項目嗎？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-149">Can users list catalog items in hello region?</span></span></li>|


## <a name="microsoftdatalakestoreaccounts"></a><span data-ttu-id="4c5f1-150">Microsoft.datalakestore/accounts</span><span class="sxs-lookup"><span data-stu-id="4c5f1-150">Microsoft.datalakestore/accounts</span></span>
|<span data-ttu-id="4c5f1-151">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="4c5f1-151">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="4c5f1-152">使用者可以上傳資料區內 hello tooData 湖存放區嗎？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-152">Can users upload data tooData Lake Store in hello region?</span></span></li><li><span data-ttu-id="4c5f1-153">使用者可以從 Data Lake Store hello 區域中下載資料嗎？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-153">Can users download data from Data Lake Store in hello region?</span></span></li></ul>|

## <a name="microsoftdocumentdbdatabaseaccounts"></a><span data-ttu-id="4c5f1-154">Microsoft.documentdb/databaseAccounts</span><span class="sxs-lookup"><span data-stu-id="4c5f1-154">Microsoft.documentdb/databaseAccounts</span></span>
|<span data-ttu-id="4c5f1-155">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="4c5f1-155">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="4c5f1-156">已有任何資料庫或集合的要求不因為 tooa DocumentDB 服務無法使用服務？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-156">Have there been any database or collection requests not served due tooa DocumentDB service unavailability?</span></span></li><li><span data-ttu-id="4c5f1-157">已有未處理因為 tooa DocumentDB 服務無法使用任何文件要求嗎？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-157">Have there been any document requests not served due tooa DocumentDB service unavailability?</span></span></li></ul>|

## <a name="microsoftnetworkconnections"></a><span data-ttu-id="4c5f1-158">Microsoft.network/connections</span><span class="sxs-lookup"><span data-stu-id="4c5f1-158">Microsoft.network/connections</span></span>
|<span data-ttu-id="4c5f1-159">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="4c5f1-159">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="4c5f1-160">Hello VPN 通道連線？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-160">Is hello VPN tunnel connected?</span></span></li><li><span data-ttu-id="4c5f1-161">Hello 連線中是否有設定衝突？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-161">Are there configuration conflicts in hello connection?</span></span></li><li><span data-ttu-id="4c5f1-162">Hello 預先共用的金鑰正確設定嗎？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-162">Are hello pre-shared keys properly configured?</span></span></li><li><span data-ttu-id="4c5f1-163">是 hello VPN 在內部部署裝置的連線嗎？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-163">Is hello VPN on-premise device reachable?</span></span></li><li><span data-ttu-id="4c5f1-164">Hello IPSec/IKE 安全性原則中是否有不相符？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-164">Are there mismatches in hello IPSec/IKE security policy?</span></span></li><li><span data-ttu-id="4c5f1-165">是 hello S2S VPN 連線正確佈建或處於失敗狀態？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-165">Is hello S2S VPN connection properly provisioned or in a failed state?</span></span></li><li><span data-ttu-id="4c5f1-166">是 hello VNET 對 VNET 連線正確佈建或處於失敗狀態？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-166">Is hello VNET-to-VNET connection properly provisioned or in a failed state?</span></span></li></ul>|

## <a name="microsoftnetworkvirtualnetworkgateways"></a><span data-ttu-id="4c5f1-167">Microsoft.network/virtualNetworkGateways</span><span class="sxs-lookup"><span data-stu-id="4c5f1-167">Microsoft.network/virtualNetworkGateways</span></span>
|<span data-ttu-id="4c5f1-168">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="4c5f1-168">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="4c5f1-169">是從 hello VPN 閘道 hello 網際網路嗎？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-169">Is hello VPN gateway reachable from hello internet?</span></span></li><li><span data-ttu-id="4c5f1-170">會在待命模式 hello VPN 閘道嗎？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-170">Is hello VPN Gateway in standby mode?</span></span></li><li><span data-ttu-id="4c5f1-171">Hello VPN 服務是否執行 hello 閘道？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-171">Is hello VPN service running on hello gateway?</span></span></li></ul>|

## <a name="microsoftnotificationhubsnamespace"></a><span data-ttu-id="4c5f1-172">Microsoft.NotificationHubs/namespace</span><span class="sxs-lookup"><span data-stu-id="4c5f1-172">Microsoft.NotificationHubs/namespace</span></span>
|<span data-ttu-id="4c5f1-173">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="4c5f1-173">Executed Checks</span></span>|
|---|
|<ul><li> <span data-ttu-id="4c5f1-174">可以在 hello 命名空間上執行執行階段作業，例如註冊、 安裝或傳送？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-174">Can runtime operations like registration, installation, or send be performed on hello namespace?</span></span></li></ul>|

## <a name="microsoftpowerbiworkspacecollections"></a><span data-ttu-id="4c5f1-175">Microsoft.PowerBI/workspaceCollections</span><span class="sxs-lookup"><span data-stu-id="4c5f1-175">Microsoft.PowerBI/workspaceCollections</span></span>
|<span data-ttu-id="4c5f1-176">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="4c5f1-176">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="4c5f1-177">Hello 主機 OS 已啟動並執行？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-177">Is hello host OS up and running?</span></span></li><li><span data-ttu-id="4c5f1-178">是從 hello 資料中心外部連到 hello workspaceCollection？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-178">Is hello workspaceCollection reachable from outside hello datacenter?</span></span></li><li><span data-ttu-id="4c5f1-179">是 hello PowerBI 資源提供者可用？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-179">Is hello PowerBI Resource Provider available?</span></span></li><li><span data-ttu-id="4c5f1-180">是 hello PowerBI hello 適當區域中可用的服務嗎？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-180">Is hello PowerBI Service available in hello appropriate region?</span></span></li></ul>|

## <a name="microsoftsearchsearchservices"></a><span data-ttu-id="4c5f1-181">Microsoft.search/searchServices</span><span class="sxs-lookup"><span data-stu-id="4c5f1-181">Microsoft.search/searchServices</span></span>
|<span data-ttu-id="4c5f1-182">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="4c5f1-182">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="4c5f1-183">可以在 hello 叢集上執行診斷操作嗎？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-183">Can diagnostics operations be performed on hello cluster?</span></span></li></ul>|

## <a name="microsoftsqlserverdatabase"></a><span data-ttu-id="4c5f1-184">Microsoft.SQL/Server/database</span><span class="sxs-lookup"><span data-stu-id="4c5f1-184">Microsoft.SQL/Server/database</span></span>
|<span data-ttu-id="4c5f1-185">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="4c5f1-185">Executed Checks</span></span>|
|---|
|<ul><li> <span data-ttu-id="4c5f1-186">已有登入 toohello 資料庫嗎？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-186">Have there been logins toohello database?</span></span></li></ul>|

## <a name="microsoftstreamanalyticsstreamingjobs"></a><span data-ttu-id="4c5f1-187">Microsoft.StreamAnalytics/streamingjobs</span><span class="sxs-lookup"><span data-stu-id="4c5f1-187">Microsoft.StreamAnalytics/streamingjobs</span></span>
|<span data-ttu-id="4c5f1-188">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="4c5f1-188">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="4c5f1-189">是所有的 hello 主機是執行向上而執行 hello 作業嗎？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-189">Are all hello hosts where hello job is executing up and running?</span></span></li><li><span data-ttu-id="4c5f1-190">已 hello 工作無法 toostart 嗎？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-190">Was hello job unable toostart?</span></span></li><li><span data-ttu-id="4c5f1-191">有進行中的執行階段升級嗎？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-191">Are there ongoing runtime upgrades?</span></span></li><li><span data-ttu-id="4c5f1-192">是預期的狀態 （例如執行或停止的客戶） 中的 hello 工作嗎？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-192">Is hello job in an expected state (for example running or stopped by customer)?</span></span></li><li><span data-ttu-id="4c5f1-193">Hello 作業發現外的記憶體例外狀況？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-193">Has hello job encountered out of memory exceptions?</span></span></li><li><span data-ttu-id="4c5f1-194">是否有進行中的排程計算更新？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-194">Are there ongoing scheduled compute updates?</span></span></li><li><span data-ttu-id="4c5f1-195">是 hello 執行管理員 （控制計畫） 可用？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-195">Is hello Execution Manager (control plan) available?</span></span></li></ul>|

## <a name="microsoftwebserverfarms"></a><span data-ttu-id="4c5f1-196">Microsoft.web/serverFarms</span><span class="sxs-lookup"><span data-stu-id="4c5f1-196">Microsoft.web/serverFarms</span></span>
|<span data-ttu-id="4c5f1-197">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="4c5f1-197">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="4c5f1-198">Hello 主機伺服器已啟動並執行？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-198">Is hello host server up and running?</span></span></li><li><span data-ttu-id="4c5f1-199">網際網路資訊服務是否執行中？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-199">Is Internet Information Services running?</span></span></li><li><span data-ttu-id="4c5f1-200">正在執行的 hello 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="4c5f1-200">Is hello Load balancer running?</span></span></li><li><span data-ttu-id="4c5f1-201">可以 hello Web 服務計劃從聯繫 hello 資料中心內？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-201">Can hello Web Service Plan be reached from within hello datacenter?</span></span></li><li><span data-ttu-id="4c5f1-202">是 hello 儲存體帳戶裝載 hello 站台內容的 hello serverFarm 可用??</span><span class="sxs-lookup"><span data-stu-id="4c5f1-202">Is hello storage account hosting hello sites content for hello serverFarm  available??</span></span></li></ul>|

## <a name="microsoftwebsites"></a><span data-ttu-id="4c5f1-203">Microsoft.web/sites</span><span class="sxs-lookup"><span data-stu-id="4c5f1-203">Microsoft.web/sites</span></span>
|<span data-ttu-id="4c5f1-204">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="4c5f1-204">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="4c5f1-205">Hello 主機伺服器已啟動並執行？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-205">Is hello host server up and running?</span></span></li><li><span data-ttu-id="4c5f1-206">網際網路資訊服務是否執行中？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-206">Is Internet Information server running?</span></span></li><li><span data-ttu-id="4c5f1-207">正在執行的 hello 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="4c5f1-207">Is hello Load balancer running?</span></span></li><li><span data-ttu-id="4c5f1-208">可以 hello Web 應用程式從聯繫 hello 資料中心內？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-208">Can hello Web App be reached from within hello datacenter?</span></span></li><li><span data-ttu-id="4c5f1-209">Hello 儲存體帳戶裝載 hello 站台的內容嗎？</span><span class="sxs-lookup"><span data-stu-id="4c5f1-209">Is hello storage account hosting hello site content available?</span></span></li></ul>|

# <a name="next-steps"></a><span data-ttu-id="4c5f1-210">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4c5f1-210">Next Steps</span></span>
-  <span data-ttu-id="4c5f1-211">請參閱[簡介 tooAzure 服務健全狀況](service-health-overview.md)和[簡介 tooAzure 資源健全狀況](resource-health-overview.md)toounderstand 深入了解它們。</span><span class="sxs-lookup"><span data-stu-id="4c5f1-211">See [Introduction tooAzure Service Health](service-health-overview.md) and [Introduction tooAzure Resource Health](resource-health-overview.md) toounderstand more about them.</span></span> 
-  [<span data-ttu-id="4c5f1-212">關於 Azure 資源健康狀態的常見問題集</span><span class="sxs-lookup"><span data-stu-id="4c5f1-212">Frequently asked questions about Azure Resource Health</span></span>](resource-health-faq.md)
- <span data-ttu-id="4c5f1-213">設定警示，如此就能收到健康狀態問題的通知。</span><span class="sxs-lookup"><span data-stu-id="4c5f1-213">Set up alerts so you are notified of health issues.</span></span> <span data-ttu-id="4c5f1-214">如需詳細資訊，請參閱[設定適用於服務健康情況的警示](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="4c5f1-214">For more information, see [Configure Alerts for Service Health](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md).</span></span> 