---
title: "透過 Azure 資源健康狀態支援的資源類型 | Microsoft Docs"
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
ms.openlocfilehash: ed9c955096a5427e8184bb6c542ad85ff4c302be
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="resource-types-and-health-checks-in-azure-resource-health"></a><span data-ttu-id="52df1-103">Azure 資源健康狀態中的資源類型和健康情況檢查</span><span class="sxs-lookup"><span data-stu-id="52df1-103">Resource types and health checks in Azure resource health</span></span>
<span data-ttu-id="52df1-104">以下是依資源類型透過資源健康狀態執行之所有檢查的完整清單。</span><span class="sxs-lookup"><span data-stu-id="52df1-104">Below is a complete list of all the checks executed through resource health by resource types.</span></span>

## <a name="microsoftcacheredisredis"></a><span data-ttu-id="52df1-105">Microsoft.CacheRedis/Redis</span><span class="sxs-lookup"><span data-stu-id="52df1-105">Microsoft.CacheRedis/Redis</span></span>
|<span data-ttu-id="52df1-106">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="52df1-106">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="52df1-107">所有快取節點是否已啟動且執行中？</span><span class="sxs-lookup"><span data-stu-id="52df1-107">Are all the Cache nodes up and running?</span></span></li><li><span data-ttu-id="52df1-108">可以從資料中心內觸達快取嗎？</span><span class="sxs-lookup"><span data-stu-id="52df1-108">Can the Cache be reached from within the datacenter?</span></span></li><li><span data-ttu-id="52df1-109">快取是否已觸達連線數目上限？</span><span class="sxs-lookup"><span data-stu-id="52df1-109">Has the Cache reached the maximum number of connections?</span></span></li><li> <span data-ttu-id="52df1-110">快取是否已用盡其可用的記憶體？</span><span class="sxs-lookup"><span data-stu-id="52df1-110">Has the cache exhausted its available memory?</span></span> </li><li><span data-ttu-id="52df1-111">快取是否發生大量頁面錯誤？</span><span class="sxs-lookup"><span data-stu-id="52df1-111">Is the Cache experiencing a high number of page faults?</span></span></li><li><span data-ttu-id="52df1-112">快取是否負載過重？</span><span class="sxs-lookup"><span data-stu-id="52df1-112">Is the Cache under heavy load?</span></span></li></ul>|

## <a name="microsoftcdnprofile"></a><span data-ttu-id="52df1-113">Microsoft.CDN/profile</span><span class="sxs-lookup"><span data-stu-id="52df1-113">Microsoft.CDN/profile</span></span>
|<span data-ttu-id="52df1-114">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="52df1-114">Executed Checks</span></span>|
|---|
|<ul> <li><span data-ttu-id="52df1-115">是否已將任何端點停止、移除或設定錯誤？</span><span class="sxs-lookup"><span data-stu-id="52df1-115">Has any of the endpoints been stopped, removed, or misconfigured?</span></span></li><li><span data-ttu-id="52df1-116">是否可存取補充入口網站進行 CDN 組態作業？</span><span class="sxs-lookup"><span data-stu-id="52df1-116">Is the supplemental portal accessible for CDN configuration operations?</span></span></li><li><span data-ttu-id="52df1-117">CDN 端點有進行中的傳遞問題嗎？</span><span class="sxs-lookup"><span data-stu-id="52df1-117">Are there ongoing delivery issues with the CDN endpoints?</span></span></li><li><span data-ttu-id="52df1-118">使用者可以將其 CDN 資源的組態進行變更嗎？</span><span class="sxs-lookup"><span data-stu-id="52df1-118">Can users change the configuration of their CDN resources?</span></span></li><li><span data-ttu-id="52df1-119">組態變更是否會以預期的速度進行傳播？</span><span class="sxs-lookup"><span data-stu-id="52df1-119">Are configuration changes propagating at the expected rate?</span></span></li><li><span data-ttu-id="52df1-120">使用者可以使用 Azure 入口網站、PowerShell 或 API 管理 CDN 組態嗎？</span><span class="sxs-lookup"><span data-stu-id="52df1-120">Can users manage the CDN configuration using the Azure portal, PowerShell, or the API?</span></span></li> </ul>|

## <a name="microsoftclassiccomputevirtualmachines"></a><span data-ttu-id="52df1-121">Microsoft.classiccompute/virtualmachines</span><span class="sxs-lookup"><span data-stu-id="52df1-121">Microsoft.classiccompute/virtualmachines</span></span>
|<span data-ttu-id="52df1-122">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="52df1-122">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="52df1-123">主機伺服器是否已啟動且執行中？</span><span class="sxs-lookup"><span data-stu-id="52df1-123">Is the host server up and running?</span></span></li><li><span data-ttu-id="52df1-124">主機 OS 是否已開機完成？</span><span class="sxs-lookup"><span data-stu-id="52df1-124">Has the host OS booting completed?</span></span></li><li><span data-ttu-id="52df1-125">虛擬機器容器是否已佈建和啟動？</span><span class="sxs-lookup"><span data-stu-id="52df1-125">Is the virtual machine container provisioned and powered up?</span></span></li><li><span data-ttu-id="52df1-126">主機和儲存體帳戶之間是否有網路連線能力？</span><span class="sxs-lookup"><span data-stu-id="52df1-126">Is there network connectivity between the host and the storage account?</span></span></li><li><span data-ttu-id="52df1-127">客體 OS 是否已完成開機？</span><span class="sxs-lookup"><span data-stu-id="52df1-127">Has the booting of the guest OS completed?</span></span></li><li><span data-ttu-id="52df1-128">是否有持續性的規劃維護？</span><span class="sxs-lookup"><span data-stu-id="52df1-128">Is there ongoing planned maintenance?</span></span></li></ul>|

## <a name="microsoftcognitiveservicesaccounts"></a><span data-ttu-id="52df1-129">Microsoft.cognitiveservices/accounts</span><span class="sxs-lookup"><span data-stu-id="52df1-129">Microsoft.cognitiveservices/accounts</span></span>
|<span data-ttu-id="52df1-130">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="52df1-130">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="52df1-131">可以從資料中心內觸達帳戶嗎？</span><span class="sxs-lookup"><span data-stu-id="52df1-131">Can the account be reached from within the datacenter?</span></span></li><li><span data-ttu-id="52df1-132">是否有可用的辨識服務資源提供者？</span><span class="sxs-lookup"><span data-stu-id="52df1-132">Is the Cognitive Services Resource Provider available?</span></span></li><li><span data-ttu-id="52df1-133">適當區域中是否有可用的辨識服務？</span><span class="sxs-lookup"><span data-stu-id="52df1-133">Is the Cognitive Service available in the appropriate region?</span></span></li><li><span data-ttu-id="52df1-134">可以在保存資源中繼資料的儲存體帳戶上執行讀取作業嗎？</span><span class="sxs-lookup"><span data-stu-id="52df1-134">Can read operations be performed on the storage account holding the resource metadata?</span></span></li><li><span data-ttu-id="52df1-135">是否已觸達 API 呼叫配額？</span><span class="sxs-lookup"><span data-stu-id="52df1-135">Has the API call quota been reached?</span></span></li><li><span data-ttu-id="52df1-136">是否已觸達 API 呼叫讀取上限？</span><span class="sxs-lookup"><span data-stu-id="52df1-136">Has the API call read-limit been reached?</span></span></li></ul>|

## <a name="microsoftcomputevirtualmachines"></a><span data-ttu-id="52df1-137">Microsoft.compute/virtualmachines</span><span class="sxs-lookup"><span data-stu-id="52df1-137">Microsoft.compute/virtualmachines</span></span>
|<span data-ttu-id="52df1-138">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="52df1-138">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="52df1-139">裝載此虛擬機器的伺服器是否已啟動且執行中？</span><span class="sxs-lookup"><span data-stu-id="52df1-139">Is the server hosting this virtual machine up and running?</span></span></li><li><span data-ttu-id="52df1-140">主機 OS 是否已開機完成？</span><span class="sxs-lookup"><span data-stu-id="52df1-140">Has the host OS booting completed?</span></span></li><li><span data-ttu-id="52df1-141">虛擬機器容器是否已佈建和啟動？</span><span class="sxs-lookup"><span data-stu-id="52df1-141">Is the virtual machine container provisioned and powered up?</span></span></li><li><span data-ttu-id="52df1-142">主機和儲存體帳戶之間是否有網路連線能力？</span><span class="sxs-lookup"><span data-stu-id="52df1-142">Is there network connectivity between the host and the storage account?</span></span></li><li><span data-ttu-id="52df1-143">客體 OS 是否已完成開機？</span><span class="sxs-lookup"><span data-stu-id="52df1-143">Has the booting of the guest OS completed?</span></span></li><li><span data-ttu-id="52df1-144">是否有持續性的規劃維護？</span><span class="sxs-lookup"><span data-stu-id="52df1-144">Is there ongoing planned maintenance?</span></span></li></ul>|

## <a name="microsoftdatalakeanalyticsaccounts"></a><span data-ttu-id="52df1-145">Microsoft.datalakeanalytics/accounts</span><span class="sxs-lookup"><span data-stu-id="52df1-145">Microsoft.datalakeanalytics/accounts</span></span>
|<span data-ttu-id="52df1-146">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="52df1-146">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="52df1-147">使用者可以將作業提交至區域中的 Data Lake Analytics 嗎？</span><span class="sxs-lookup"><span data-stu-id="52df1-147">Can users submit jobs to Data Lake Analytics in the region?</span></span></li><li><span data-ttu-id="52df1-148">是否會在區域中執行且順利完成基本作業？</span><span class="sxs-lookup"><span data-stu-id="52df1-148">Do basic jobs run and complete successfully in the region?</span></span></li><li><span data-ttu-id="52df1-149">使用者可以列出區域中的目錄項目嗎？</span><span class="sxs-lookup"><span data-stu-id="52df1-149">Can users list catalog items in the region?</span></span></li>|


## <a name="microsoftdatalakestoreaccounts"></a><span data-ttu-id="52df1-150">Microsoft.datalakestore/accounts</span><span class="sxs-lookup"><span data-stu-id="52df1-150">Microsoft.datalakestore/accounts</span></span>
|<span data-ttu-id="52df1-151">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="52df1-151">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="52df1-152">使用者可以將資料上傳至區域中的 Data Lake Store 嗎？</span><span class="sxs-lookup"><span data-stu-id="52df1-152">Can users upload data to Data Lake Store in the region?</span></span></li><li><span data-ttu-id="52df1-153">使用者可以從區域中的 Data Lake Store 下載資料嗎？</span><span class="sxs-lookup"><span data-stu-id="52df1-153">Can users download data from Data Lake Store in the region?</span></span></li></ul>|

## <a name="microsoftdocumentdbdatabaseaccounts"></a><span data-ttu-id="52df1-154">Microsoft.documentdb/databaseAccounts</span><span class="sxs-lookup"><span data-stu-id="52df1-154">Microsoft.documentdb/databaseAccounts</span></span>
|<span data-ttu-id="52df1-155">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="52df1-155">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="52df1-156">是否有因 DocumentDB 服務無法使用而不提供的任何資料庫或集合要求？</span><span class="sxs-lookup"><span data-stu-id="52df1-156">Have there been any database or collection requests not served due to a DocumentDB service unavailability?</span></span></li><li><span data-ttu-id="52df1-157">是否有因 DocumentDB 服務無法使用而不提供的任何文件要求？</span><span class="sxs-lookup"><span data-stu-id="52df1-157">Have there been any document requests not served due to a DocumentDB service unavailability?</span></span></li></ul>|

## <a name="microsoftnetworkconnections"></a><span data-ttu-id="52df1-158">Microsoft.network/connections</span><span class="sxs-lookup"><span data-stu-id="52df1-158">Microsoft.network/connections</span></span>
|<span data-ttu-id="52df1-159">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="52df1-159">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="52df1-160">VPN 通道是否已連線？</span><span class="sxs-lookup"><span data-stu-id="52df1-160">Is the VPN tunnel connected?</span></span></li><li><span data-ttu-id="52df1-161">連線中有設定衝突嗎？</span><span class="sxs-lookup"><span data-stu-id="52df1-161">Are there configuration conflicts in the connection?</span></span></li><li><span data-ttu-id="52df1-162">是否正確設定預先共用的金鑰？</span><span class="sxs-lookup"><span data-stu-id="52df1-162">Are the pre-shared keys properly configured?</span></span></li><li><span data-ttu-id="52df1-163">VPN 內部部署裝置是否可觸達？</span><span class="sxs-lookup"><span data-stu-id="52df1-163">Is the VPN on-premise device reachable?</span></span></li><li><span data-ttu-id="52df1-164">IPSec/IKE 安全性原則中是否有不相符之處？</span><span class="sxs-lookup"><span data-stu-id="52df1-164">Are there mismatches in the IPSec/IKE security policy?</span></span></li><li><span data-ttu-id="52df1-165">S2S VPN 連線是否正確佈建，還是處於失敗狀態？</span><span class="sxs-lookup"><span data-stu-id="52df1-165">Is the S2S VPN connection properly provisioned or in a failed state?</span></span></li><li><span data-ttu-id="52df1-166">VNET 對 VNET 連線是否正確佈建，還是處於失敗狀態？</span><span class="sxs-lookup"><span data-stu-id="52df1-166">Is the VNET-to-VNET connection properly provisioned or in a failed state?</span></span></li></ul>|

## <a name="microsoftnetworkvirtualnetworkgateways"></a><span data-ttu-id="52df1-167">Microsoft.network/virtualNetworkGateways</span><span class="sxs-lookup"><span data-stu-id="52df1-167">Microsoft.network/virtualNetworkGateways</span></span>
|<span data-ttu-id="52df1-168">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="52df1-168">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="52df1-169">是否可從網際網路觸達 VPN 閘道？</span><span class="sxs-lookup"><span data-stu-id="52df1-169">Is the VPN gateway reachable from the internet?</span></span></li><li><span data-ttu-id="52df1-170">VPN 閘道是否處於待命模式？</span><span class="sxs-lookup"><span data-stu-id="52df1-170">Is the VPN Gateway in standby mode?</span></span></li><li><span data-ttu-id="52df1-171">VPN 服務是否在閘道上執行？</span><span class="sxs-lookup"><span data-stu-id="52df1-171">Is the VPN service running on the gateway?</span></span></li></ul>|

## <a name="microsoftnotificationhubsnamespace"></a><span data-ttu-id="52df1-172">Microsoft.NotificationHubs/namespace</span><span class="sxs-lookup"><span data-stu-id="52df1-172">Microsoft.NotificationHubs/namespace</span></span>
|<span data-ttu-id="52df1-173">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="52df1-173">Executed Checks</span></span>|
|---|
|<ul><li> <span data-ttu-id="52df1-174">可以在命名空間上執行註冊、安裝或傳送等執行階段作業嗎？</span><span class="sxs-lookup"><span data-stu-id="52df1-174">Can runtime operations like registration, installation, or send be performed on the namespace?</span></span></li></ul>|

## <a name="microsoftpowerbiworkspacecollections"></a><span data-ttu-id="52df1-175">Microsoft.PowerBI/workspaceCollections</span><span class="sxs-lookup"><span data-stu-id="52df1-175">Microsoft.PowerBI/workspaceCollections</span></span>
|<span data-ttu-id="52df1-176">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="52df1-176">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="52df1-177">主機作業系統是否已啟動且執行中？</span><span class="sxs-lookup"><span data-stu-id="52df1-177">Is the host OS up and running?</span></span></li><li><span data-ttu-id="52df1-178">是否可從資料中心外部觸達 workspaceCollection？</span><span class="sxs-lookup"><span data-stu-id="52df1-178">Is the workspaceCollection reachable from outside the datacenter?</span></span></li><li><span data-ttu-id="52df1-179">PowerBI 資源提供者是否可用？</span><span class="sxs-lookup"><span data-stu-id="52df1-179">Is the PowerBI Resource Provider available?</span></span></li><li><span data-ttu-id="52df1-180">適當區域中是否有可用的 PowerBI 服務？</span><span class="sxs-lookup"><span data-stu-id="52df1-180">Is the PowerBI Service available in the appropriate region?</span></span></li></ul>|

## <a name="microsoftsearchsearchservices"></a><span data-ttu-id="52df1-181">Microsoft.search/searchServices</span><span class="sxs-lookup"><span data-stu-id="52df1-181">Microsoft.search/searchServices</span></span>
|<span data-ttu-id="52df1-182">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="52df1-182">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="52df1-183">可以在叢集上執行診斷作業嗎？</span><span class="sxs-lookup"><span data-stu-id="52df1-183">Can diagnostics operations be performed on the cluster?</span></span></li></ul>|

## <a name="microsoftsqlserverdatabase"></a><span data-ttu-id="52df1-184">Microsoft.SQL/Server/database</span><span class="sxs-lookup"><span data-stu-id="52df1-184">Microsoft.SQL/Server/database</span></span>
|<span data-ttu-id="52df1-185">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="52df1-185">Executed Checks</span></span>|
|---|
|<ul><li> <span data-ttu-id="52df1-186">是否已經登入資料庫？</span><span class="sxs-lookup"><span data-stu-id="52df1-186">Have there been logins to the database?</span></span></li></ul>|

## <a name="microsoftstreamanalyticsstreamingjobs"></a><span data-ttu-id="52df1-187">Microsoft.StreamAnalytics/streamingjobs</span><span class="sxs-lookup"><span data-stu-id="52df1-187">Microsoft.StreamAnalytics/streamingjobs</span></span>
|<span data-ttu-id="52df1-188">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="52df1-188">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="52df1-189">作業執行中的所有主機是否已啟動且執行中？</span><span class="sxs-lookup"><span data-stu-id="52df1-189">Are all the hosts where the job is executing up and running?</span></span></li><li><span data-ttu-id="52df1-190">作業無法啟動嗎？</span><span class="sxs-lookup"><span data-stu-id="52df1-190">Was the job unable to start?</span></span></li><li><span data-ttu-id="52df1-191">有進行中的執行階段升級嗎？</span><span class="sxs-lookup"><span data-stu-id="52df1-191">Are there ongoing runtime upgrades?</span></span></li><li><span data-ttu-id="52df1-192">作業是否為預期的狀態 (例如執行中或由客戶停止)？</span><span class="sxs-lookup"><span data-stu-id="52df1-192">Is the job in an expected state (for example running or stopped by customer)?</span></span></li><li><span data-ttu-id="52df1-193">作業是否發生記憶體不足的例外狀況？</span><span class="sxs-lookup"><span data-stu-id="52df1-193">Has the job encountered out of memory exceptions?</span></span></li><li><span data-ttu-id="52df1-194">是否有進行中的排程計算更新？</span><span class="sxs-lookup"><span data-stu-id="52df1-194">Are there ongoing scheduled compute updates?</span></span></li><li><span data-ttu-id="52df1-195">執行管理員 (控制計畫) 是否可用？</span><span class="sxs-lookup"><span data-stu-id="52df1-195">Is the Execution Manager (control plan) available?</span></span></li></ul>|

## <a name="microsoftwebserverfarms"></a><span data-ttu-id="52df1-196">Microsoft.web/serverFarms</span><span class="sxs-lookup"><span data-stu-id="52df1-196">Microsoft.web/serverFarms</span></span>
|<span data-ttu-id="52df1-197">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="52df1-197">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="52df1-198">主機伺服器是否已啟動且執行中？</span><span class="sxs-lookup"><span data-stu-id="52df1-198">Is the host server up and running?</span></span></li><li><span data-ttu-id="52df1-199">網際網路資訊服務是否執行中？</span><span class="sxs-lookup"><span data-stu-id="52df1-199">Is Internet Information Services running?</span></span></li><li><span data-ttu-id="52df1-200">負載平衡器是否執行中？</span><span class="sxs-lookup"><span data-stu-id="52df1-200">Is the Load balancer running?</span></span></li><li><span data-ttu-id="52df1-201">可以從資料中心內觸達 Web 服務方案嗎？</span><span class="sxs-lookup"><span data-stu-id="52df1-201">Can the Web Service Plan be reached from within the datacenter?</span></span></li><li><span data-ttu-id="52df1-202">裝載 serverFarm 網站內容的儲存體帳戶是否可用？</span><span class="sxs-lookup"><span data-stu-id="52df1-202">Is the storage account hosting the sites content for the serverFarm  available??</span></span></li></ul>|

## <a name="microsoftwebsites"></a><span data-ttu-id="52df1-203">Microsoft.web/sites</span><span class="sxs-lookup"><span data-stu-id="52df1-203">Microsoft.web/sites</span></span>
|<span data-ttu-id="52df1-204">執行的檢查</span><span class="sxs-lookup"><span data-stu-id="52df1-204">Executed Checks</span></span>|
|---|
|<ul><li><span data-ttu-id="52df1-205">主機伺服器是否已啟動且執行中？</span><span class="sxs-lookup"><span data-stu-id="52df1-205">Is the host server up and running?</span></span></li><li><span data-ttu-id="52df1-206">網際網路資訊服務是否執行中？</span><span class="sxs-lookup"><span data-stu-id="52df1-206">Is Internet Information server running?</span></span></li><li><span data-ttu-id="52df1-207">負載平衡器是否執行中？</span><span class="sxs-lookup"><span data-stu-id="52df1-207">Is the Load balancer running?</span></span></li><li><span data-ttu-id="52df1-208">可以從資料中心內觸達 Web 應用程式嗎？</span><span class="sxs-lookup"><span data-stu-id="52df1-208">Can the Web App be reached from within the datacenter?</span></span></li><li><span data-ttu-id="52df1-209">裝載網站內容的儲存體帳戶是否可用？</span><span class="sxs-lookup"><span data-stu-id="52df1-209">Is the storage account hosting the site content available?</span></span></li></ul>|

# <a name="next-steps"></a><span data-ttu-id="52df1-210">後續步驟</span><span class="sxs-lookup"><span data-stu-id="52df1-210">Next Steps</span></span>
-  <span data-ttu-id="52df1-211">請參閱 [Azure 服務健康狀態的簡介](service-health-overview.md)和 [Azure 資源健康狀態的簡介](resource-health-overview.md)來了解更多相關資訊。</span><span class="sxs-lookup"><span data-stu-id="52df1-211">See [Introduction to Azure Service Health](service-health-overview.md) and [Introduction to Azure Resource Health](resource-health-overview.md) to understand more about them.</span></span> 
-  [<span data-ttu-id="52df1-212">關於 Azure 資源健康狀態的常見問題集</span><span class="sxs-lookup"><span data-stu-id="52df1-212">Frequently asked questions about Azure Resource Health</span></span>](resource-health-faq.md)
- <span data-ttu-id="52df1-213">設定警示，如此就能收到健康狀態問題的通知。</span><span class="sxs-lookup"><span data-stu-id="52df1-213">Set up alerts so you are notified of health issues.</span></span> <span data-ttu-id="52df1-214">如需詳細資訊，請參閱[設定適用於服務健康情況的警示](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="52df1-214">For more information, see [Configure Alerts for Service Health](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md).</span></span> 