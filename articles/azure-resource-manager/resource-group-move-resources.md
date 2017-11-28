---
title: "aaaMove Azure 資源 toonew 訂用帳戶或資源群組 |Microsoft 文件"
description: "使用 Azure Resource Manager toomove 資源 tooa 新資源群組或訂用帳戶。"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ab7d42bd-8434-4026-a892-df4a97b60a9b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: tomfitz
ms.openlocfilehash: 09d35f0afbbcdc0c66779f98a982d878f0807497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-resources-toonew-resource-group-or-subscription"></a><span data-ttu-id="e4e94-103">移動資源 toonew 資源群組或訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e4e94-103">Move resources toonew resource group or subscription</span></span>
<span data-ttu-id="e4e94-104">本主題說明您如何 toomove 資源 tooeither 新訂用帳戶或新的資源群組中 hello 相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e4e94-104">This topic shows you how toomove resources tooeither a new subscription or a new resource group in hello same subscription.</span></span> <span data-ttu-id="e4e94-105">您可以使用 hello 入口網站、 PowerShell、 Azure CLI 或 hello REST API toomove 資源。</span><span class="sxs-lookup"><span data-stu-id="e4e94-105">You can use hello portal, PowerShell, Azure CLI, or hello REST API toomove resource.</span></span> <span data-ttu-id="e4e94-106">本主題中的 hello 移動作業是使用 tooyou 不需要任何協助從 Azure 支援。</span><span class="sxs-lookup"><span data-stu-id="e4e94-106">hello move operations in this topic are available tooyou without any assistance from Azure support.</span></span>

<span data-ttu-id="e4e94-107">當您移動資源，也會 hello 作業期間鎖定 hello 來源群組和 hello 目標群組。</span><span class="sxs-lookup"><span data-stu-id="e4e94-107">When moving resources, both hello source group and hello target group are locked during hello operation.</span></span> <span data-ttu-id="e4e94-108">寫入和刪除作業 hello 移動作業完成之前被封鎖於 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="e4e94-108">Write and delete operations are blocked on hello resource groups until hello move completes.</span></span> <span data-ttu-id="e4e94-109">這個鎖定表示您無法加入、 更新或刪除資源在 hello 資源群組中，但它並不表示已遭到凍結 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="e4e94-109">This lock means you cannot add, update, or delete resources in hello resource groups, but it does not mean hello resources are frozen.</span></span> <span data-ttu-id="e4e94-110">比方說，如果您移動 SQL Server 和資料庫 tooa 新資源群組，使用 hello 資料庫的應用程式就會發生任何停機時間。</span><span class="sxs-lookup"><span data-stu-id="e4e94-110">For example, if you move a SQL Server and its database tooa new resource group, an application that uses hello database experiences no downtime.</span></span> <span data-ttu-id="e4e94-111">仍可讀取並寫入 toohello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="e4e94-111">It can still read and write toohello database.</span></span>

<span data-ttu-id="e4e94-112">您無法變更 hello 資源的 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="e4e94-112">You cannot change hello location of hello resource.</span></span> <span data-ttu-id="e4e94-113">移動資源只會移動它 tooa 新資源群組。</span><span class="sxs-lookup"><span data-stu-id="e4e94-113">Moving a resource only moves it tooa new resource group.</span></span> <span data-ttu-id="e4e94-114">hello 新資源群組可能會有不同的位置，但不會變更 hello 資源的 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="e4e94-114">hello new resource group may have a different location, but that does not change hello location of hello resource.</span></span>

> [!NOTE]
> <span data-ttu-id="e4e94-115">本文說明如何在現有的 Azure toomove 資源帳戶提供項目。</span><span class="sxs-lookup"><span data-stu-id="e4e94-115">This article describes how toomove resources within an existing Azure account offering.</span></span> <span data-ttu-id="e4e94-116">如果您真的想要 toochange 為您的 Azure 帳戶 （例如從隨用隨付 toopre 付費升級） 產品，同時繼續 toowork 與您現有的資源，請參閱[切換您的 Azure 訂用帳戶 tooanother 優惠](../billing/billing-how-to-switch-azure-offer.md)。</span><span class="sxs-lookup"><span data-stu-id="e4e94-116">If you actually want toochange your Azure account offering (such as upgrading from pay-as-you-go toopre-pay) while continuing toowork with your existing resources, see [Switch your Azure subscription tooanother offer](../billing/billing-how-to-switch-azure-offer.md).</span></span>
>
>

## <a name="checklist-before-moving-resources"></a><span data-ttu-id="e4e94-117">移動資源前的檢查清單</span><span class="sxs-lookup"><span data-stu-id="e4e94-117">Checklist before moving resources</span></span>
<span data-ttu-id="e4e94-118">移動資源之前有一些重要步驟 tooperform。</span><span class="sxs-lookup"><span data-stu-id="e4e94-118">There are some important steps tooperform before moving a resource.</span></span> <span data-ttu-id="e4e94-119">藉由驗證這些條件，您可以避免錯誤。</span><span class="sxs-lookup"><span data-stu-id="e4e94-119">By verifying these conditions, you can avoid errors.</span></span>

1. <span data-ttu-id="e4e94-120">hello 來源和目的地訂用帳戶必須存在於 hello 相同[Azure Active Directory 租用戶](../active-directory/active-directory-howto-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="e4e94-120">hello source and destination subscriptions must exist within hello same [Azure Active Directory tenant](../active-directory/active-directory-howto-tenant.md).</span></span> <span data-ttu-id="e4e94-121">這兩個訂用帳戶擁有 hello 相同 toocheck 租用戶識別碼，請使用 Azure PowerShell 或 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="e4e94-121">toocheck that both subscriptions have hello same tenant ID, use Azure PowerShell or Azure CLI.</span></span>

  <span data-ttu-id="e4e94-122">如果是 Azure PowerShell，請使用：</span><span class="sxs-lookup"><span data-stu-id="e4e94-122">For Azure PowerShell, use:</span></span>

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  <span data-ttu-id="e4e94-123">如果是 Azure CLI 2.0，請使用：</span><span class="sxs-lookup"><span data-stu-id="e4e94-123">For Azure CLI 2.0, use:</span></span>

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  <span data-ttu-id="e4e94-124">如果 hello 租用戶的識別碼 hello 來源和目的地訂用帳戶不是 hello 相同，您可以嘗試 hello 訂用帳戶的 toochange hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="e4e94-124">If hello tenant IDs for hello source and destination subscriptions are not hello same, you can attempt toochange hello directory for hello subscription.</span></span> <span data-ttu-id="e4e94-125">不過，這個選項是使用 tooService Microsoft 帳戶 （非組織帳戶） 登入系統管理員。</span><span class="sxs-lookup"><span data-stu-id="e4e94-125">However, this option is only available tooService Administrators who are signed in with a Microsoft account (not an organizational account).</span></span> <span data-ttu-id="e4e94-126">變更 hello 目錄中，登入 toohello tooattempt[傳統入口網站](https://manage.windowsazure.com/)，然後選取**設定**，選取 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e4e94-126">tooattempt changing hello directory, log in toohello [classic portal](https://manage.windowsazure.com/), and select **Settings**, and select hello subscription.</span></span> <span data-ttu-id="e4e94-127">如果 hello**編輯目錄**圖示可用，請選取它 toochange hello 相關聯的 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="e4e94-127">If hello **Edit Directory** icon is available, select it toochange hello associated Azure Active Directory.</span></span>

  ![編輯目錄](./media/resource-group-move-resources/edit-directory.png)

  <span data-ttu-id="e4e94-129">如果找不到該圖示，您必須連絡支援 toomove hello 資源 tooa 新的租用戶。</span><span class="sxs-lookup"><span data-stu-id="e4e94-129">If that icon is not available, you must contact support toomove hello resources tooa new tenant.</span></span>

2. <span data-ttu-id="e4e94-130">hello 服務必須啟用 hello 能力 toomove 資源。</span><span class="sxs-lookup"><span data-stu-id="e4e94-130">hello service must enable hello ability toomove resources.</span></span> <span data-ttu-id="e4e94-131">本主題列出哪些服務可實現移動資源，哪些服務無法實現移動資源。</span><span class="sxs-lookup"><span data-stu-id="e4e94-131">This topic lists which services enable moving resources and which services do not enable moving resources.</span></span>
3. <span data-ttu-id="e4e94-132">正在移動的 hello 資源的 hello 資源提供者必須登錄 hello 目的地訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e4e94-132">hello destination subscription must be registered for hello resource provider of hello resource being moved.</span></span> <span data-ttu-id="e4e94-133">如果不是，您會收到錯誤，指出該 hello**訂用帳戶未註冊資源類型**。</span><span class="sxs-lookup"><span data-stu-id="e4e94-133">If not, you receive an error stating that hello **subscription is not registered for a resource type**.</span></span> <span data-ttu-id="e4e94-134">移動資源 tooa 新訂閱時，可能會遇到這個問題，但從未使用該訂用帳戶與該資源類型。</span><span class="sxs-lookup"><span data-stu-id="e4e94-134">You might encounter this problem when moving a resource tooa new subscription, but that subscription has never been used with that resource type.</span></span> <span data-ttu-id="e4e94-135">toolearn 如何 toocheck hello 登錄狀態，並註冊資源提供者，請參閱[資源提供者和類型](resource-manager-supported-services.md)。</span><span class="sxs-lookup"><span data-stu-id="e4e94-135">toolearn how toocheck hello registration status and register resource providers, see [Resource providers and types](resource-manager-supported-services.md).</span></span>

## <a name="when-toocall-support"></a><span data-ttu-id="e4e94-136">當 toocall 支援</span><span class="sxs-lookup"><span data-stu-id="e4e94-136">When toocall support</span></span>
<span data-ttu-id="e4e94-137">您可以移動透過本主題中的 hello 自助服務作業的最多資源。</span><span class="sxs-lookup"><span data-stu-id="e4e94-137">You can move most resources through hello self-service operations shown in this topic.</span></span> <span data-ttu-id="e4e94-138">使用 hello 自助服務作業：</span><span class="sxs-lookup"><span data-stu-id="e4e94-138">Use hello self-service operations to:</span></span>

* <span data-ttu-id="e4e94-139">移動 Resource Manager 資源。</span><span class="sxs-lookup"><span data-stu-id="e4e94-139">Move Resource Manager resources.</span></span>
* <span data-ttu-id="e4e94-140">將根據 toohello 傳統資源移動[傳統部署限制](#classic-deployment-limitations)。</span><span class="sxs-lookup"><span data-stu-id="e4e94-140">Move classic resources according toohello [classic deployment limitations](#classic-deployment-limitations).</span></span>

<span data-ttu-id="e4e94-141">當您需要進行下列作業時，請連絡支援人員︰</span><span class="sxs-lookup"><span data-stu-id="e4e94-141">Call support when you need to:</span></span>

* <span data-ttu-id="e4e94-142">移動資源 tooa 新的 Azure 帳戶 （與 Azure Active Directory 租用戶）。</span><span class="sxs-lookup"><span data-stu-id="e4e94-142">Move your resources tooa new Azure account (and Azure Active Directory tenant).</span></span>
* <span data-ttu-id="e4e94-143">將傳統資源移動，但發生問題 hello 限制。</span><span class="sxs-lookup"><span data-stu-id="e4e94-143">Move classic resources but are having trouble with hello limitations.</span></span>

## <a name="services-that-enable-move"></a><span data-ttu-id="e4e94-144">啟用移動的服務</span><span class="sxs-lookup"><span data-stu-id="e4e94-144">Services that enable move</span></span>
<span data-ttu-id="e4e94-145">現在，是啟用移動 tooboth 新的資源群組和訂用帳戶的 hello 服務：</span><span class="sxs-lookup"><span data-stu-id="e4e94-145">For now, hello services that enable moving tooboth a new resource group and subscription are:</span></span>

* <span data-ttu-id="e4e94-146">API 管理</span><span class="sxs-lookup"><span data-stu-id="e4e94-146">API Management</span></span>
* <span data-ttu-id="e4e94-147">App Service 應用程式 (Web 應用程式) - 請參閱 [App Service 限制](#app-service-limitations)</span><span class="sxs-lookup"><span data-stu-id="e4e94-147">App Service apps (web apps) - see [App Service limitations](#app-service-limitations)</span></span>
* <span data-ttu-id="e4e94-148">Application Insights</span><span class="sxs-lookup"><span data-stu-id="e4e94-148">Application Insights</span></span>
* <span data-ttu-id="e4e94-149">自動化</span><span class="sxs-lookup"><span data-stu-id="e4e94-149">Automation</span></span>
* <span data-ttu-id="e4e94-150">Batch</span><span class="sxs-lookup"><span data-stu-id="e4e94-150">Batch</span></span>
* <span data-ttu-id="e4e94-151">Bing 地圖</span><span class="sxs-lookup"><span data-stu-id="e4e94-151">Bing Maps</span></span>
* <span data-ttu-id="e4e94-152">CDN</span><span class="sxs-lookup"><span data-stu-id="e4e94-152">CDN</span></span>
* <span data-ttu-id="e4e94-153">雲端服務 - 請參閱 [傳統部署限制](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="e4e94-153">Cloud Services - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="e4e94-154">辨識服務</span><span class="sxs-lookup"><span data-stu-id="e4e94-154">Cognitive Services</span></span>
* <span data-ttu-id="e4e94-155">內容仲裁</span><span class="sxs-lookup"><span data-stu-id="e4e94-155">Content Moderator</span></span>
* <span data-ttu-id="e4e94-156">資料目錄</span><span class="sxs-lookup"><span data-stu-id="e4e94-156">Data Catalog</span></span>
* <span data-ttu-id="e4e94-157">Data Factory</span><span class="sxs-lookup"><span data-stu-id="e4e94-157">Data Factory</span></span>
* <span data-ttu-id="e4e94-158">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="e4e94-158">Data Lake Analytics</span></span>
* <span data-ttu-id="e4e94-159">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e4e94-159">Data Lake Store</span></span>
* <span data-ttu-id="e4e94-160">DNS</span><span class="sxs-lookup"><span data-stu-id="e4e94-160">DNS</span></span>
* <span data-ttu-id="e4e94-161">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e4e94-161">Azure Cosmos DB</span></span>
* <span data-ttu-id="e4e94-162">事件中樞</span><span class="sxs-lookup"><span data-stu-id="e4e94-162">Event Hubs</span></span>
* <span data-ttu-id="e4e94-163">HDInsight 叢集 - 請參閱 [HDInsight 限制](#hdinsight-limitations)</span><span class="sxs-lookup"><span data-stu-id="e4e94-163">HDInsight clusters - see [HDInsight limitations](#hdinsight-limitations)</span></span>
* <span data-ttu-id="e4e94-164">IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="e4e94-164">IoT Hubs</span></span>
* <span data-ttu-id="e4e94-165">Key Vault</span><span class="sxs-lookup"><span data-stu-id="e4e94-165">Key Vault</span></span>
* <span data-ttu-id="e4e94-166">負載平衡器</span><span class="sxs-lookup"><span data-stu-id="e4e94-166">Load Balancers</span></span>
* <span data-ttu-id="e4e94-167">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="e4e94-167">Logic Apps</span></span>
* <span data-ttu-id="e4e94-168">機器學習服務</span><span class="sxs-lookup"><span data-stu-id="e4e94-168">Machine Learning</span></span>
* <span data-ttu-id="e4e94-169">媒體服務</span><span class="sxs-lookup"><span data-stu-id="e4e94-169">Media Services</span></span>
* <span data-ttu-id="e4e94-170">Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="e4e94-170">Mobile Engagement</span></span>
* <span data-ttu-id="e4e94-171">通知中樞</span><span class="sxs-lookup"><span data-stu-id="e4e94-171">Notification Hubs</span></span>
* <span data-ttu-id="e4e94-172">Operational Insights</span><span class="sxs-lookup"><span data-stu-id="e4e94-172">Operational Insights</span></span>
* <span data-ttu-id="e4e94-173">Operations Management</span><span class="sxs-lookup"><span data-stu-id="e4e94-173">Operations Management</span></span>
* <span data-ttu-id="e4e94-174">Power BI</span><span class="sxs-lookup"><span data-stu-id="e4e94-174">Power BI</span></span>
* <span data-ttu-id="e4e94-175">Redis 快取</span><span class="sxs-lookup"><span data-stu-id="e4e94-175">Redis Cache</span></span>
* <span data-ttu-id="e4e94-176">排程器</span><span class="sxs-lookup"><span data-stu-id="e4e94-176">Scheduler</span></span>
* <span data-ttu-id="e4e94-177">搜尋</span><span class="sxs-lookup"><span data-stu-id="e4e94-177">Search</span></span>
* <span data-ttu-id="e4e94-178">伺服器管理</span><span class="sxs-lookup"><span data-stu-id="e4e94-178">Server Management</span></span>
* <span data-ttu-id="e4e94-179">服務匯流排</span><span class="sxs-lookup"><span data-stu-id="e4e94-179">Service Bus</span></span>
* <span data-ttu-id="e4e94-180">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e4e94-180">Service Fabric</span></span>
* <span data-ttu-id="e4e94-181">儲存體</span><span class="sxs-lookup"><span data-stu-id="e4e94-181">Storage</span></span>
* <span data-ttu-id="e4e94-182">儲存體 (傳統) - 請參閱 [傳統部署限制](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="e4e94-182">Storage (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="e4e94-183">串流分析 - 無法移動執行中狀態的串流分析作業。</span><span class="sxs-lookup"><span data-stu-id="e4e94-183">Stream Analytics - Stream Analytics jobs cannot be moved when in running state.</span></span>
* <span data-ttu-id="e4e94-184">SQL Database 伺服器-hello 資料庫和伺服器必須位於 hello 相同的資源群組。</span><span class="sxs-lookup"><span data-stu-id="e4e94-184">SQL Database server - hello database and server must reside in hello same resource group.</span></span> <span data-ttu-id="e4e94-185">當您移動 SQL 伺服器時，其所有資料庫也會跟著移動。</span><span class="sxs-lookup"><span data-stu-id="e4e94-185">When you move a SQL server, all its databases are also moved.</span></span>
* <span data-ttu-id="e4e94-186">流量管理員</span><span class="sxs-lookup"><span data-stu-id="e4e94-186">Traffic Manager</span></span>
* <span data-ttu-id="e4e94-187">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="e4e94-187">Virtual Machines</span></span>
* <span data-ttu-id="e4e94-188">使用憑證儲存在金鑰保存庫位在相同的訂用帳戶移動 toonew 資源群組中的虛擬機器已啟用，但未啟用跨訂用帳戶移動。</span><span class="sxs-lookup"><span data-stu-id="e4e94-188">Virtual Machines with certificate stored in Key Vault - Move toonew resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="e4e94-189">虛擬機器 (傳統) - 請參閱 [傳統部署限制](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="e4e94-189">Virtual Machines (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="e4e94-190">虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="e4e94-190">Virtual Machine Scale Sets</span></span>
* <span data-ttu-id="e4e94-191">虛擬網路 - 目前，在停用 VNet 對等互連之前，將無法移動對等的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="e4e94-191">Virtual Networks - Currently, a peered Virtual Network cannot be moved until VNet peering has been disabled.</span></span> <span data-ttu-id="e4e94-192">一旦停用的 hello 能夠順利移動虛擬網路，而且可以啟用 hello VNet 對等互連。</span><span class="sxs-lookup"><span data-stu-id="e4e94-192">Once disabled, hello Virtual Network can be moved successfully and hello VNet peering can be enabled.</span></span> <span data-ttu-id="e4e94-193">此外，虛擬網路不能移動的 tooa 不同訂用帳戶，如果 hello 虛擬網路包含資源瀏覽連結的任何子網路。</span><span class="sxs-lookup"><span data-stu-id="e4e94-193">In addition, a Virtual Network cannot be moved tooa different subscription if hello Virtual Network contains any subnet with resource navigation links.</span></span> <span data-ttu-id="e4e94-194">例如，當 Microsoft.Cache Redis 資源部署到虛擬網路子網路時，該子網路便具有資源導覽連結。</span><span class="sxs-lookup"><span data-stu-id="e4e94-194">For example, a Virtual Network subnet has a resource navigation link when a Microsoft.Cache redis resource is deployed into this subnet.</span></span>
* <span data-ttu-id="e4e94-195">VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="e4e94-195">VPN Gateway</span></span>


## <a name="services-that-do-not-enable-move"></a><span data-ttu-id="e4e94-196">不啟用移動的服務</span><span class="sxs-lookup"><span data-stu-id="e4e94-196">Services that do not enable move</span></span>
<span data-ttu-id="e4e94-197">目前未啟用移動資源的 hello 服務包括：</span><span class="sxs-lookup"><span data-stu-id="e4e94-197">hello services that currently do not enable moving a resource are:</span></span>

* <span data-ttu-id="e4e94-198">AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="e4e94-198">AD Domain Services</span></span>
* <span data-ttu-id="e4e94-199">AD 混合式健康狀態服務</span><span class="sxs-lookup"><span data-stu-id="e4e94-199">AD Hybrid Health Service</span></span>
* <span data-ttu-id="e4e94-200">應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="e4e94-200">Application Gateway</span></span>
* <span data-ttu-id="e4e94-201">具有使用受控磁碟之虛擬機器的可用性設定組</span><span class="sxs-lookup"><span data-stu-id="e4e94-201">Availability sets with Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="e4e94-202">BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="e4e94-202">BizTalk Services</span></span>
* <span data-ttu-id="e4e94-203">容器服務</span><span class="sxs-lookup"><span data-stu-id="e4e94-203">Container Service</span></span>
* <span data-ttu-id="e4e94-204">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="e4e94-204">Express Route</span></span>
* <span data-ttu-id="e4e94-205">DevTest Labs-移動 toonew 資源群組相同的訂用帳戶中已啟用，但不是會啟用跨訂用帳戶移動。</span><span class="sxs-lookup"><span data-stu-id="e4e94-205">DevTest Labs - Move toonew resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="e4e94-206">Dynamics LCS</span><span class="sxs-lookup"><span data-stu-id="e4e94-206">Dynamics LCS</span></span>
* <span data-ttu-id="e4e94-207">從受控磁碟建立的映像</span><span class="sxs-lookup"><span data-stu-id="e4e94-207">Images created from Managed Disks</span></span>
* <span data-ttu-id="e4e94-208">受控磁碟</span><span class="sxs-lookup"><span data-stu-id="e4e94-208">Managed Disks</span></span>
* <span data-ttu-id="e4e94-209">受管理的應用程式</span><span class="sxs-lookup"><span data-stu-id="e4e94-209">Managed Applications</span></span>
* <span data-ttu-id="e4e94-210">復原服務保存庫-不移動 hello 運算、 網路和儲存體資源相關聯也 hello 復原服務保存庫，請參閱[復原服務限制](#recovery-services-limitations)。</span><span class="sxs-lookup"><span data-stu-id="e4e94-210">Recovery Services vault - also do not move hello Compute, Network, and Storage resources associated with hello Recovery Services vault, see [Recovery Services limitations](#recovery-services-limitations).</span></span>
* <span data-ttu-id="e4e94-211">安全性</span><span class="sxs-lookup"><span data-stu-id="e4e94-211">Security</span></span>
* <span data-ttu-id="e4e94-212">從受控磁碟建立的快照集</span><span class="sxs-lookup"><span data-stu-id="e4e94-212">Snapshots created from Managed Disks</span></span>
* <span data-ttu-id="e4e94-213">StorSimple 裝置管理員</span><span class="sxs-lookup"><span data-stu-id="e4e94-213">StorSimple Device Manager</span></span>
* <span data-ttu-id="e4e94-214">使用受控磁碟的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="e4e94-214">Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="e4e94-215">虛擬網路 (傳統) - 請參閱 [傳統部署限制](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="e4e94-215">Virtual Networks (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="e4e94-216">從 Marketplace 資源建立的虛擬機器 - 無法在訂用帳戶之間移動。</span><span class="sxs-lookup"><span data-stu-id="e4e94-216">Virtual Machines created from Marketplace resources - cannot be moved across subscriptions.</span></span> <span data-ttu-id="e4e94-217">需要 toobe hello 目前訂用帳戶取消佈建和部署一次 hello 新訂用帳戶中的資源</span><span class="sxs-lookup"><span data-stu-id="e4e94-217">Resource needs toobe deprovisioned in hello current subscription and deployed again in hello new subscription</span></span>

## <a name="app-service-limitations"></a><span data-ttu-id="e4e94-218">App Service 限制</span><span class="sxs-lookup"><span data-stu-id="e4e94-218">App Service limitations</span></span>
<span data-ttu-id="e4e94-219">使用 App Service 應用程式時，您無法只移動 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="e4e94-219">When working with App Service apps, you cannot move only an App Service plan.</span></span> <span data-ttu-id="e4e94-220">toomove App Service 應用程式，您的選項如下：</span><span class="sxs-lookup"><span data-stu-id="e4e94-220">toomove App Service apps, your options are:</span></span>

* <span data-ttu-id="e4e94-221">該資源群組 tooa 新資源群組中已經沒有應用程式服務的資源移動 hello 應用程式服務方案和所有其他應用程式服務資源。</span><span class="sxs-lookup"><span data-stu-id="e4e94-221">Move hello App Service plan and all other App Service resources in that resource group tooa new resource group that does not already have App Service resources.</span></span> <span data-ttu-id="e4e94-222">甚至，您必須移動的方式 hello 應用程式服務資源的這項需求不是與 hello 應用程式服務方案相關聯。</span><span class="sxs-lookup"><span data-stu-id="e4e94-222">This requirement means you must move even hello App Service resources that are not associated with hello App Service plan.</span></span>
* <span data-ttu-id="e4e94-223">移動 hello 應用程式 tooa 不同的資源群組，但保留 hello 原始的資源群組中的所有應用程式服務方案。</span><span class="sxs-lookup"><span data-stu-id="e4e94-223">Move hello apps tooa different resource group, but keep all App Service plans in hello original resource group.</span></span>

<span data-ttu-id="e4e94-224">hello 應用程式服務計劃不需要在 tooreside hello 與 hello 應用程式 toofunction 的 hello 應用程式的相同資源群組正確。</span><span class="sxs-lookup"><span data-stu-id="e4e94-224">hello App Service plan does not need tooreside in hello same resource group as hello app for hello app toofunction correctly.</span></span>

<span data-ttu-id="e4e94-225">例如，如果您的資源群組包含︰</span><span class="sxs-lookup"><span data-stu-id="e4e94-225">For example, if your resource group contains:</span></span>

* <span data-ttu-id="e4e94-226">與 **plan-a** 關聯的 **web-a**</span><span class="sxs-lookup"><span data-stu-id="e4e94-226">**web-a** which is associated with **plan-a**</span></span>
* <span data-ttu-id="e4e94-227">與 **plan-b** 關聯的 **web-b**</span><span class="sxs-lookup"><span data-stu-id="e4e94-227">**web-b** which is associated with **plan-b**</span></span>

<span data-ttu-id="e4e94-228">您的選項如下：</span><span class="sxs-lookup"><span data-stu-id="e4e94-228">Your options are:</span></span>

* <span data-ttu-id="e4e94-229">移動 **web-a**、**plan-a**、**web-b** 及 **plan-b**</span><span class="sxs-lookup"><span data-stu-id="e4e94-229">Move **web-a**, **plan-a**, **web-b**, and **plan-b**</span></span>
* <span data-ttu-id="e4e94-230">移動 **web-a** 和 **web-b**</span><span class="sxs-lookup"><span data-stu-id="e4e94-230">Move **web-a** and **web-b**</span></span>
* <span data-ttu-id="e4e94-231">移動 **web-a**</span><span class="sxs-lookup"><span data-stu-id="e4e94-231">Move **web-a**</span></span>
* <span data-ttu-id="e4e94-232">移動 **web-b**</span><span class="sxs-lookup"><span data-stu-id="e4e94-232">Move **web-b**</span></span>

<span data-ttu-id="e4e94-233">所有其他組合都會留下移動 App Service 方案時無法留下的資源類型 (任何類型的 App Service 資源)。</span><span class="sxs-lookup"><span data-stu-id="e4e94-233">All other combinations involve leaving behind a resource type that can't be left behind when moving an App Service plan (any type of App Service resource).</span></span>

<span data-ttu-id="e4e94-234">如果您 web 應用程式位於不同的資源群組超過其應用程式服務方案，但您想 toomove 這兩個 tooa 新的資源群組，您必須執行兩個步驟中的 hello 移動。</span><span class="sxs-lookup"><span data-stu-id="e4e94-234">If your web app resides in a different resource group than its App Service plan but you want toomove both tooa new resource group, you must perform hello move in two steps.</span></span> <span data-ttu-id="e4e94-235">例如：</span><span class="sxs-lookup"><span data-stu-id="e4e94-235">For example:</span></span>

* <span data-ttu-id="e4e94-236">**web-a** 位於 **web-group** 中</span><span class="sxs-lookup"><span data-stu-id="e4e94-236">**web-a** resides in **web-group**</span></span>
* <span data-ttu-id="e4e94-237">**plan-a** 位於 **plan-group** 中</span><span class="sxs-lookup"><span data-stu-id="e4e94-237">**plan-a** resides in **plan-group**</span></span>
* <span data-ttu-id="e4e94-238">您想要**web 的**和**計劃的**中的 tooreside**結合群組**</span><span class="sxs-lookup"><span data-stu-id="e4e94-238">You want **web-a** and **plan-a** tooreside in **combined-group**</span></span>

<span data-ttu-id="e4e94-239">這將移動，在 hello 下列順序執行兩個不同的移動作業 tooaccomplish:</span><span class="sxs-lookup"><span data-stu-id="e4e94-239">tooaccomplish this move, perform two separate move operations in hello following sequence:</span></span>

1. <span data-ttu-id="e4e94-240">移動 hello **web 的**太**計劃群組**</span><span class="sxs-lookup"><span data-stu-id="e4e94-240">Move hello **web-a** too**plan-group**</span></span>
2. <span data-ttu-id="e4e94-241">移動**web 的**和**計劃的**太**結合群組**。</span><span class="sxs-lookup"><span data-stu-id="e4e94-241">Move **web-a** and **plan-a** too**combined-group**.</span></span>

<span data-ttu-id="e4e94-242">您可以移動應用程式的服務憑證 tooa 新資源群組或訂用帳戶沒有任何問題。</span><span class="sxs-lookup"><span data-stu-id="e4e94-242">You can move an App Service Certificate tooa new resource group or subscription without any issues.</span></span> <span data-ttu-id="e4e94-243">不過，如果您的 web 應用程式包含您購買外部並上傳 toohello 應用程式的 SSL 憑證，您必須刪除 hello 憑證，才能移動 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e4e94-243">However, if your web app includes an SSL certificate that you purchased externally and uploaded toohello app, you must delete hello certificate before moving hello web app.</span></span> <span data-ttu-id="e4e94-244">比方說，您可以執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e4e94-244">For example, you can perform hello following steps:</span></span>

1. <span data-ttu-id="e4e94-245">刪除 hello web 應用程式中的 hello 上傳憑證</span><span class="sxs-lookup"><span data-stu-id="e4e94-245">Delete hello uploaded certificate from hello web app</span></span>
2. <span data-ttu-id="e4e94-246">移動 hello web 應用程式</span><span class="sxs-lookup"><span data-stu-id="e4e94-246">Move hello web app</span></span>
3. <span data-ttu-id="e4e94-247">上傳 hello 憑證 toohello web 應用程式</span><span class="sxs-lookup"><span data-stu-id="e4e94-247">Upload hello certificate toohello web app</span></span>

## <a name="recovery-services-limitations"></a><span data-ttu-id="e4e94-248">復原服務限制</span><span class="sxs-lookup"><span data-stu-id="e4e94-248">Recovery Services limitations</span></span>
<span data-ttu-id="e4e94-249">移動 未啟用儲存體、 網路或計算與 Azure Site Recovery 使用 tooset 災害復原的資源。</span><span class="sxs-lookup"><span data-stu-id="e4e94-249">Move is not enabled for Storage, Network, or Compute resources used tooset up disaster recovery with Azure Site Recovery.</span></span>

<span data-ttu-id="e4e94-250">例如，假設您已設定複寫在內部部署機器 tooa 儲存體帳戶 (Storage1)，而且想 hello 受保護機器 toocome 向上，tooAzure 容錯移轉之後為虛擬機器 (VM1) 附加 tooa 虛擬網路 (Network1)。</span><span class="sxs-lookup"><span data-stu-id="e4e94-250">For example, suppose you have set up replication of your on-premises machines tooa storage account (Storage1) and want hello protected machine toocome up after failover tooAzure as a virtual machine (VM1) attached tooa virtual network (Network1).</span></span> <span data-ttu-id="e4e94-251">您無法移動下列任何 Azure 資源-Storage1，VM1，並 Network1-跨越資源群組內 hello 相同訂用帳戶或訂用帳戶之間。</span><span class="sxs-lookup"><span data-stu-id="e4e94-251">You cannot move any of these Azure resources - Storage1, VM1, and Network1 - across resource groups within hello same subscription or across subscriptions.</span></span>

## <a name="hdinsight-limitations"></a><span data-ttu-id="e4e94-252">HDInsight 限制</span><span class="sxs-lookup"><span data-stu-id="e4e94-252">HDInsight limitations</span></span>

<span data-ttu-id="e4e94-253">您可以移動 HDInsight 叢集 tooa 新訂用帳戶或資源群組。</span><span class="sxs-lookup"><span data-stu-id="e4e94-253">You can move HDInsight clusters tooa new subscription or resource group.</span></span> <span data-ttu-id="e4e94-254">不過，您無法跨訂閱 hello 網路功能 （例如 hello 虛擬網路、 NIC 或負載平衡器） 的資源連結的 toohello HDInsight 叢集移動。</span><span class="sxs-lookup"><span data-stu-id="e4e94-254">However, you cannot move across subscriptions hello networking resources linked toohello HDInsight cluster (such as hello virtual network, NIC, or load balancer).</span></span> <span data-ttu-id="e4e94-255">此外，您無法移動 tooa 新資源群組是附加的 tooa hello 叢集的虛擬機器的 NIC。</span><span class="sxs-lookup"><span data-stu-id="e4e94-255">In addition, you cannot move tooa new resource group a NIC that is attached tooa virtual machine for hello cluster.</span></span>

<span data-ttu-id="e4e94-256">當您移動 HDInsight 叢集 tooa 新訂閱，第一次移動其他資源 （例如 hello 儲存體帳戶）。</span><span class="sxs-lookup"><span data-stu-id="e4e94-256">When moving an HDInsight cluster tooa new subscription, first move other resources (like hello storage account).</span></span> <span data-ttu-id="e4e94-257">接著，單獨使用時移動 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="e4e94-257">Then, move hello HDInsight cluster by itself.</span></span>

## <a name="classic-deployment-limitations"></a><span data-ttu-id="e4e94-258">傳統部署限制</span><span class="sxs-lookup"><span data-stu-id="e4e94-258">Classic deployment limitations</span></span>
<span data-ttu-id="e4e94-259">hello 的選項移動透過 hello 傳統模型所部署的資源會因根據是否要移動訂用帳戶或 tooa 新訂用帳戶中的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="e4e94-259">hello options for moving resources deployed through hello classic model differ based on whether you are moving hello resources within a subscription or tooa new subscription.</span></span>

### <a name="same-subscription"></a><span data-ttu-id="e4e94-260">相同訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e4e94-260">Same subscription</span></span>
<span data-ttu-id="e4e94-261">當移動資源從一個資源群組 tooanother 資源群組內套用相同的訂用帳戶，下列限制的 hello hello:</span><span class="sxs-lookup"><span data-stu-id="e4e94-261">When moving resources from one resource group tooanother resource group within hello same subscription, hello following restrictions apply:</span></span>

* <span data-ttu-id="e4e94-262">無法移動虛擬網路 (傳統)。</span><span class="sxs-lookup"><span data-stu-id="e4e94-262">Virtual networks (classic) cannot be moved.</span></span>
* <span data-ttu-id="e4e94-263">必須移動虛擬機器 （傳統） 與 hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="e4e94-263">Virtual machines (classic) must be moved with hello cloud service.</span></span>
* <span data-ttu-id="e4e94-264">當 hello 移動包含其所有的虛擬機器時，就只能移動雲端服務。</span><span class="sxs-lookup"><span data-stu-id="e4e94-264">Cloud service can only be moved when hello move includes all its virtual machines.</span></span>
* <span data-ttu-id="e4e94-265">一次只能移動一個雲端服務。</span><span class="sxs-lookup"><span data-stu-id="e4e94-265">Only one cloud service can be moved at a time.</span></span>
* <span data-ttu-id="e4e94-266">一次只能移動一個儲存體帳戶 (傳統)。</span><span class="sxs-lookup"><span data-stu-id="e4e94-266">Only one storage account (classic) can be moved at a time.</span></span>
* <span data-ttu-id="e4e94-267">儲存體帳戶 （傳統） 無法在 hello 移動虛擬機器或雲端服務相同的作業。</span><span class="sxs-lookup"><span data-stu-id="e4e94-267">Storage account (classic) cannot be moved in hello same operation with a virtual machine or a cloud service.</span></span>

<span data-ttu-id="e4e94-268">toomove 傳統資源 tooa 新資源群組內 hello 相同訂用帳戶，請使用 hello 標準的移動作業透過 hello[入口網站](#use-portal)， [Azure PowerShell](#use-powershell)， [Azure CLI](#use-azure-cli)，或[REST API](#use-rest-api)。</span><span class="sxs-lookup"><span data-stu-id="e4e94-268">toomove classic resources tooa new resource group within hello same subscription, use hello standard move operations through hello [portal](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), or [REST API](#use-rest-api).</span></span> <span data-ttu-id="e4e94-269">您使用 hello 相同的作業，因為您用來移動資源管理員資源。</span><span class="sxs-lookup"><span data-stu-id="e4e94-269">You use hello same operations as you use for moving Resource Manager resources.</span></span>

### <a name="new-subscription"></a><span data-ttu-id="e4e94-270">新的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e4e94-270">New subscription</span></span>
<span data-ttu-id="e4e94-271">當您移動資源 tooa 新訂用帳戶，便會套用下列限制的 hello:</span><span class="sxs-lookup"><span data-stu-id="e4e94-271">When moving resources tooa new subscription, hello following restrictions apply:</span></span>

* <span data-ttu-id="e4e94-272">Hello 訂用帳戶中的所有傳統資源必須移動 hello 中相同的作業。</span><span class="sxs-lookup"><span data-stu-id="e4e94-272">All classic resources in hello subscription must be moved in hello same operation.</span></span>
* <span data-ttu-id="e4e94-273">hello 目標訂用帳戶不可以包含任何其他傳統資源。</span><span class="sxs-lookup"><span data-stu-id="e4e94-273">hello target subscription must not contain any other classic resources.</span></span>
* <span data-ttu-id="e4e94-274">只可以透過傳統移動個別的 REST API 要求 hello 移動。</span><span class="sxs-lookup"><span data-stu-id="e4e94-274">hello move can only be requested through a separate REST API for classic moves.</span></span> <span data-ttu-id="e4e94-275">hello 標準資源管理員移動命令無法運作時移動傳統資源 tooa 新訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e4e94-275">hello standard Resource Manager move commands do not work when moving classic resources tooa new subscription.</span></span>

<span data-ttu-id="e4e94-276">toomove 傳統資源 tooa 新訂用帳戶，都是特定 tooclassic 資源的使用 hello REST 作業。</span><span class="sxs-lookup"><span data-stu-id="e4e94-276">toomove classic resources tooa new subscription, use hello REST operations that are specific tooclassic resources.</span></span> <span data-ttu-id="e4e94-277">toouse 其餘部分，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e4e94-277">toouse REST, perform hello following steps:</span></span>

1. <span data-ttu-id="e4e94-278">檢查如果 hello 來源訂用帳戶可以參與跨訂用帳戶移動。</span><span class="sxs-lookup"><span data-stu-id="e4e94-278">Check if hello source subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="e4e94-279">使用 hello 下列操作：</span><span class="sxs-lookup"><span data-stu-id="e4e94-279">Use hello following operation:</span></span>

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="e4e94-280">在 hello 要求主體中，包括：</span><span class="sxs-lookup"><span data-stu-id="e4e94-280">In hello request body, include:</span></span>

  ```json
  {
    "role": "source"
  }
  ```

     <span data-ttu-id="e4e94-281">hello 回應 hello 驗證作業處於下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="e4e94-281">hello response for hello validation operation is in hello following format:</span></span>

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. <span data-ttu-id="e4e94-282">檢查如果 hello 目的地訂用帳戶可以參與跨訂用帳戶移動。</span><span class="sxs-lookup"><span data-stu-id="e4e94-282">Check if hello destination subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="e4e94-283">使用 hello 下列操作：</span><span class="sxs-lookup"><span data-stu-id="e4e94-283">Use hello following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="e4e94-284">在 hello 要求主體中，包括：</span><span class="sxs-lookup"><span data-stu-id="e4e94-284">In hello request body, include:</span></span>

  ```json
  {
    "role": "target"
  }
  ```

     <span data-ttu-id="e4e94-285">hello 回應 hello 相同 hello 來源訂用帳戶的驗證格式為。</span><span class="sxs-lookup"><span data-stu-id="e4e94-285">hello response is in hello same format as hello source subscription validation.</span></span>
3. <span data-ttu-id="e4e94-286">如果這兩個訂用帳戶通過驗證時，移動所有傳統資源從一個訂用帳戶 tooanother 訂用帳戶以 hello 下列操作：</span><span class="sxs-lookup"><span data-stu-id="e4e94-286">If both subscriptions pass validation, move all classic resources from one subscription tooanother subscription with hello following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    <span data-ttu-id="e4e94-287">在 hello 要求主體中，包括：</span><span class="sxs-lookup"><span data-stu-id="e4e94-287">In hello request body, include:</span></span>

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

<span data-ttu-id="e4e94-288">hello 作業可能會執行幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="e4e94-288">hello operation may run for several minutes.</span></span>

## <a name="use-portal"></a><span data-ttu-id="e4e94-289">使用入口網站</span><span class="sxs-lookup"><span data-stu-id="e4e94-289">Use portal</span></span>
<span data-ttu-id="e4e94-290">toomove 資源，選取包含這些資源，hello 資源群組，然後選取 [hello**移動**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e4e94-290">toomove resources, select hello resource group containing those resources, and then select hello **Move** button.</span></span>

![移動資源](./media/resource-group-move-resources/select-move.png)

<span data-ttu-id="e4e94-292">選取您要移動 hello 資源 tooa 新資源群組或新的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e4e94-292">Select whether you are moving hello resources tooa new resource group or a new subscription.</span></span>

<span data-ttu-id="e4e94-293">選取 hello 資源 toomove 與 hello 目的地資源群組。</span><span class="sxs-lookup"><span data-stu-id="e4e94-293">Select hello resources toomove and hello destination resource group.</span></span> <span data-ttu-id="e4e94-294">了解您需要 tooupdate 指令碼，這些資源並選取**確定**。</span><span class="sxs-lookup"><span data-stu-id="e4e94-294">Acknowledge that you need tooupdate scripts for these resources and select **OK**.</span></span> <span data-ttu-id="e4e94-295">如果您選取 hello 編輯訂用帳戶 圖示 hello 上一個步驟中，您也必須選取 hello 目的地訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e4e94-295">If you selected hello edit subscription icon in hello previous step, you must also select hello destination subscription.</span></span>

![選取目的地](./media/resource-group-move-resources/select-destination.png)

<span data-ttu-id="e4e94-297">在**通知**，您會看到該 hello 移動作業正在執行。</span><span class="sxs-lookup"><span data-stu-id="e4e94-297">In **Notifications**, you see that hello move operation is running.</span></span>

![顯示移動狀態](./media/resource-group-move-resources/show-status.png)

<span data-ttu-id="e4e94-299">完成後，就會通知的 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="e4e94-299">When it has completed, you are notified of hello result.</span></span>

![顯示移動結果](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a><span data-ttu-id="e4e94-301">使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="e4e94-301">Use PowerShell</span></span>
<span data-ttu-id="e4e94-302">toomove 現有資源 tooanother 資源群組或訂用帳戶，使用 hello`Move-AzureRmResource`命令。</span><span class="sxs-lookup"><span data-stu-id="e4e94-302">toomove existing resources tooanother resource group or subscription, use hello `Move-AzureRmResource` command.</span></span>

<span data-ttu-id="e4e94-303">hello 第一個範例顯示如何 toomove 一個資源 tooa 新資源群組。</span><span class="sxs-lookup"><span data-stu-id="e4e94-303">hello first example shows how toomove one resource tooa new resource group.</span></span>

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

<span data-ttu-id="e4e94-304">hello 第二個範例會示範如何 toomove 多個資源 tooa 新資源群組。</span><span class="sxs-lookup"><span data-stu-id="e4e94-304">hello second example shows how toomove multiple resources tooa new resource group.</span></span>

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

<span data-ttu-id="e4e94-305">toomove tooa 新訂用帳戶，包含的值 hello`DestinationSubscriptionId`參數。</span><span class="sxs-lookup"><span data-stu-id="e4e94-305">toomove tooa new subscription, include a value for hello `DestinationSubscriptionId` parameter.</span></span>

<span data-ttu-id="e4e94-306">系統會詢問您想 toomove hello tooconfirm 指定資源。</span><span class="sxs-lookup"><span data-stu-id="e4e94-306">You are asked tooconfirm that you want toomove hello specified resources.</span></span>

```powershell
Confirm
Are you sure you want toomove these resources toohello resource group
'/subscriptions/{guid}/resourceGroups/newRG' hello resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a><span data-ttu-id="e4e94-307">使用 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e4e94-307">Use Azure CLI 2.0</span></span>
<span data-ttu-id="e4e94-308">toomove 現有資源 tooanother 資源群組或訂用帳戶，使用 hello`az resource move`命令。</span><span class="sxs-lookup"><span data-stu-id="e4e94-308">toomove existing resources tooanother resource group or subscription, use hello `az resource move` command.</span></span> <span data-ttu-id="e4e94-309">提供 hello 資源 hello 資源 toomove Id。</span><span class="sxs-lookup"><span data-stu-id="e4e94-309">Provide hello resource IDs of hello resources toomove.</span></span> <span data-ttu-id="e4e94-310">您可以取得的資源識別碼與 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="e4e94-310">You can get resource IDs with hello following command:</span></span>

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

<span data-ttu-id="e4e94-311">hello 下列範例顯示如何 toomove 儲存體帳戶 tooa 新資源群組。</span><span class="sxs-lookup"><span data-stu-id="e4e94-311">hello following example shows how toomove a storage account tooa new resource group.</span></span> <span data-ttu-id="e4e94-312">在 hello`--ids`參數，提供的 hello 資源 Id toomove 以空格分隔清單。</span><span class="sxs-lookup"><span data-stu-id="e4e94-312">In hello `--ids` parameter, provide a space-separated list of hello resource IDs toomove.</span></span>

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

<span data-ttu-id="e4e94-313">toomove tooa 新訂用帳戶，提供 hello`--destination-subscription-id`參數。</span><span class="sxs-lookup"><span data-stu-id="e4e94-313">toomove tooa new subscription, provide hello `--destination-subscription-id` parameter.</span></span>

## <a name="use-azure-cli-10"></a><span data-ttu-id="e4e94-314">使用 Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e4e94-314">Use Azure CLI 1.0</span></span>
<span data-ttu-id="e4e94-315">toomove 現有資源 tooanother 資源群組或訂用帳戶，使用 hello`azure resource move`命令。</span><span class="sxs-lookup"><span data-stu-id="e4e94-315">toomove existing resources tooanother resource group or subscription, use hello `azure resource move` command.</span></span> <span data-ttu-id="e4e94-316">提供 hello 資源 hello 資源 toomove Id。</span><span class="sxs-lookup"><span data-stu-id="e4e94-316">Provide hello resource IDs of hello resources toomove.</span></span> <span data-ttu-id="e4e94-317">您可以取得的資源識別碼與 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="e4e94-317">You can get resource IDs with hello following command:</span></span>

```azurecli
azure resource list -g sourceGroup --json
```

<span data-ttu-id="e4e94-318">它會傳回下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="e4e94-318">Which returns hello following format:</span></span>

```azurecli
[
  {
    "id": "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo",
    "name": "storagedemo",
    "type": "Microsoft.Storage/storageAccounts",
    "location": "southcentralus",
    "tags": {},
    "kind": "Storage",
    "sku": {
      "name": "Standard_RAGRS",
      "tier": "Standard"
    }
  }
]
```

<span data-ttu-id="e4e94-319">hello 下列範例顯示如何 toomove 儲存體帳戶 tooa 新資源群組。</span><span class="sxs-lookup"><span data-stu-id="e4e94-319">hello following example shows how toomove a storage account tooa new resource group.</span></span> <span data-ttu-id="e4e94-320">在 hello`-i`參數，提供 hello 資源 Id toomove 的逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="e4e94-320">In hello `-i` parameter, provide a comma-separated list of hello resource IDs toomove.</span></span>

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

<span data-ttu-id="e4e94-321">系統會詢問您想 toomove hello tooconfirm 指定的資源。</span><span class="sxs-lookup"><span data-stu-id="e4e94-321">You are asked tooconfirm that you want toomove hello specified resource.</span></span>

## <a name="use-rest-api"></a><span data-ttu-id="e4e94-322">使用 REST API</span><span class="sxs-lookup"><span data-stu-id="e4e94-322">Use REST API</span></span>
<span data-ttu-id="e4e94-323">toomove 現有資源 tooanother 資源群組或訂用帳戶，執行：</span><span class="sxs-lookup"><span data-stu-id="e4e94-323">toomove existing resources tooanother resource group or subscription, run:</span></span>

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

<span data-ttu-id="e4e94-324">在 hello 要求主體中，您可以指定 hello 目標資源群組與 hello 資源 toomove。</span><span class="sxs-lookup"><span data-stu-id="e4e94-324">In hello request body, you specify hello target resource group and hello resources toomove.</span></span> <span data-ttu-id="e4e94-325">如需 hello 移動 REST 作業的詳細資訊，請參閱[資源移](https://msdn.microsoft.com/library/azure/mt218710.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e4e94-325">For more information about hello move REST operation, see [Move resources](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4e94-326">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e4e94-326">Next steps</span></span>
* <span data-ttu-id="e4e94-327">toolearn 相關 PowerShell cmdlet 來管理您的訂閱，請參閱[使用 Azure PowerShell 與資源管理員](powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="e4e94-327">toolearn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="e4e94-328">toolearn 有關 Azure CLI 命令可用於管理您的訂閱，請參閱[使用 hello Azure CLI 與資源管理員](xplat-cli-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="e4e94-328">toolearn about Azure CLI commands for managing your subscription, see [Using hello Azure CLI with Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="e4e94-329">toolearn 有關入口網站功能來管理您的訂閱，請參閱[使用 hello Azure 入口網站 toomanage 資源](resource-group-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="e4e94-329">toolearn about portal features for managing your subscription, see [Using hello Azure portal toomanage resources](resource-group-portal.md).</span></span>
* <span data-ttu-id="e4e94-330">toolearn 有關套用邏輯組織 tooyour 資源，請參閱[使用標記 tooorganize 資源](resource-group-using-tags.md)。</span><span class="sxs-lookup"><span data-stu-id="e4e94-330">toolearn about applying a logical organization tooyour resources, see [Using tags tooorganize your resources](resource-group-using-tags.md).</span></span>
