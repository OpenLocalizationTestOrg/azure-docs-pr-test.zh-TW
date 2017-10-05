---
title: "將 Azure 資源移至新的訂用帳戶或資源群組 | Microsoft Docs"
description: "使用 Azure Resource Manager 將資源移到新的資源群組或訂用帳戶。"
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
ms.openlocfilehash: e138f80e808968ab4bf5c11cfd5fd46fe4a1bcce
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="move-resources-to-new-resource-group-or-subscription"></a><span data-ttu-id="afc1c-103">將資源移動到新的資源群組或訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="afc1c-103">Move resources to new resource group or subscription</span></span>
<span data-ttu-id="afc1c-104">本主題說明如何將資源移至新的訂用帳戶或相同訂用帳戶中新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="afc1c-104">This topic shows you how to move resources to either a new subscription or a new resource group in the same subscription.</span></span> <span data-ttu-id="afc1c-105">您可以使用入口網站、PowerShell、Azure CLI 或 REST API 來移動資源。</span><span class="sxs-lookup"><span data-stu-id="afc1c-105">You can use the portal, PowerShell, Azure CLI, or the REST API to move resource.</span></span> <span data-ttu-id="afc1c-106">本主題中的移動作業可供您使用而不需要任何 Azure 支援的協助。</span><span class="sxs-lookup"><span data-stu-id="afc1c-106">The move operations in this topic are available to you without any assistance from Azure support.</span></span>

<span data-ttu-id="afc1c-107">移動資源時，在此作業期間會同時鎖定來源群組和目標群組。</span><span class="sxs-lookup"><span data-stu-id="afc1c-107">When moving resources, both the source group and the target group are locked during the operation.</span></span> <span data-ttu-id="afc1c-108">資源群組上的寫入和刪除作業將會封鎖，直到移動完成。</span><span class="sxs-lookup"><span data-stu-id="afc1c-108">Write and delete operations are blocked on the resource groups until the move completes.</span></span> <span data-ttu-id="afc1c-109">此鎖定表示您無法新增、更新或刪除資源群組中的資源，但不表示資源已遭到凍結。</span><span class="sxs-lookup"><span data-stu-id="afc1c-109">This lock means you cannot add, update, or delete resources in the resource groups, but it does not mean the resources are frozen.</span></span> <span data-ttu-id="afc1c-110">例如，如果您將 SQL Server 和其資料庫移至新的資源群組，使用該資料庫的應用程式不會發生停機時間。</span><span class="sxs-lookup"><span data-stu-id="afc1c-110">For example, if you move a SQL Server and its database to a new resource group, an application that uses the database experiences no downtime.</span></span> <span data-ttu-id="afc1c-111">它仍可對資料庫讀取和寫入。</span><span class="sxs-lookup"><span data-stu-id="afc1c-111">It can still read and write to the database.</span></span>

<span data-ttu-id="afc1c-112">您無法變更資源的位置。</span><span class="sxs-lookup"><span data-stu-id="afc1c-112">You cannot change the location of the resource.</span></span> <span data-ttu-id="afc1c-113">移動資源只會將它移動到新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="afc1c-113">Moving a resource only moves it to a new resource group.</span></span> <span data-ttu-id="afc1c-114">新的資源群組可能會有不同的位置，但那樣不會變更資源的位置。</span><span class="sxs-lookup"><span data-stu-id="afc1c-114">The new resource group may have a different location, but that does not change the location of the resource.</span></span>

> [!NOTE]
> <span data-ttu-id="afc1c-115">本文說明如何在現有的 Azure 帳戶提供項目內移動資源。</span><span class="sxs-lookup"><span data-stu-id="afc1c-115">This article describes how to move resources within an existing Azure account offering.</span></span> <span data-ttu-id="afc1c-116">如果您真的想要變更 Azure 帳戶提供項目 (例如，從隨用隨付升級為預付)，同時繼續使用現有的資源，請參閱 [切換至不同的 Azure 訂用帳戶優惠](../billing/billing-how-to-switch-azure-offer.md)。</span><span class="sxs-lookup"><span data-stu-id="afc1c-116">If you actually want to change your Azure account offering (such as upgrading from pay-as-you-go to pre-pay) while continuing to work with your existing resources, see [Switch your Azure subscription to another offer](../billing/billing-how-to-switch-azure-offer.md).</span></span>
>
>

## <a name="checklist-before-moving-resources"></a><span data-ttu-id="afc1c-117">移動資源前的檢查清單</span><span class="sxs-lookup"><span data-stu-id="afc1c-117">Checklist before moving resources</span></span>
<span data-ttu-id="afc1c-118">在移動資源之前，要執行的重要步驟如下︰</span><span class="sxs-lookup"><span data-stu-id="afc1c-118">There are some important steps to perform before moving a resource.</span></span> <span data-ttu-id="afc1c-119">藉由驗證這些條件，您可以避免錯誤。</span><span class="sxs-lookup"><span data-stu-id="afc1c-119">By verifying these conditions, you can avoid errors.</span></span>

1. <span data-ttu-id="afc1c-120">來源和目的地的訂用帳戶必須存在於相同的 [Azure Active Directory 租用戶](../active-directory/active-directory-howto-tenant.md)內。</span><span class="sxs-lookup"><span data-stu-id="afc1c-120">The source and destination subscriptions must exist within the same [Azure Active Directory tenant](../active-directory/active-directory-howto-tenant.md).</span></span> <span data-ttu-id="afc1c-121">若要檢查這兩個訂用帳戶都有相同的租用戶識別碼，請使用 Azure PowerShell 或 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="afc1c-121">To check that both subscriptions have the same tenant ID, use Azure PowerShell or Azure CLI.</span></span>

  <span data-ttu-id="afc1c-122">如果是 Azure PowerShell，請使用：</span><span class="sxs-lookup"><span data-stu-id="afc1c-122">For Azure PowerShell, use:</span></span>

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  <span data-ttu-id="afc1c-123">如果是 Azure CLI 2.0，請使用：</span><span class="sxs-lookup"><span data-stu-id="afc1c-123">For Azure CLI 2.0, use:</span></span>

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  <span data-ttu-id="afc1c-124">如果來源和目的地訂用帳戶的租用戶識別碼不相同，您可以嘗試變更訂用帳戶的目錄。</span><span class="sxs-lookup"><span data-stu-id="afc1c-124">If the tenant IDs for the source and destination subscriptions are not the same, you can attempt to change the directory for the subscription.</span></span> <span data-ttu-id="afc1c-125">不過，此選項僅提供給使用 Microsoft 帳戶 (非組織帳戶) 登入的服務系統管理員。</span><span class="sxs-lookup"><span data-stu-id="afc1c-125">However, this option is only available to Service Administrators who are signed in with a Microsoft account (not an organizational account).</span></span> <span data-ttu-id="afc1c-126">若要嘗試變更目錄，登入到[傳統入口網站](https://manage.windowsazure.com/)，然後選取 [設定]，再選取訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="afc1c-126">To attempt changing the directory, log in to the [classic portal](https://manage.windowsazure.com/), and select **Settings**, and select the subscription.</span></span> <span data-ttu-id="afc1c-127">如果 [編輯目錄] 圖示可用，請選取它來變更相關聯的 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="afc1c-127">If the **Edit Directory** icon is available, select it to change the associated Azure Active Directory.</span></span>

  ![編輯目錄](./media/resource-group-move-resources/edit-directory.png)

  <span data-ttu-id="afc1c-129">如果該圖示不可用，您必須連絡支援人員將資源移動到新的租用戶。</span><span class="sxs-lookup"><span data-stu-id="afc1c-129">If that icon is not available, you must contact support to move the resources to a new tenant.</span></span>

2. <span data-ttu-id="afc1c-130">服務必須啟用移動資源的功能。</span><span class="sxs-lookup"><span data-stu-id="afc1c-130">The service must enable the ability to move resources.</span></span> <span data-ttu-id="afc1c-131">本主題列出哪些服務可實現移動資源，哪些服務無法實現移動資源。</span><span class="sxs-lookup"><span data-stu-id="afc1c-131">This topic lists which services enable moving resources and which services do not enable moving resources.</span></span>
3. <span data-ttu-id="afc1c-132">必須針對要移動之資源的資源提供者註冊其目的地訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="afc1c-132">The destination subscription must be registered for the resource provider of the resource being moved.</span></span> <span data-ttu-id="afc1c-133">否則，您會收到錯誤，指出 **未針對資源類型註冊訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="afc1c-133">If not, you receive an error stating that the **subscription is not registered for a resource type**.</span></span> <span data-ttu-id="afc1c-134">將資源移至新的訂用帳戶時，可能會因為該訂用帳戶不曾以指定的資源類型使用過而遇到問題。</span><span class="sxs-lookup"><span data-stu-id="afc1c-134">You might encounter this problem when moving a resource to a new subscription, but that subscription has never been used with that resource type.</span></span> <span data-ttu-id="afc1c-135">若要了解如何檢查註冊狀態及註冊資源提供者，請參閱 [資源提供者和類型](resource-manager-supported-services.md)。</span><span class="sxs-lookup"><span data-stu-id="afc1c-135">To learn how to check the registration status and register resource providers, see [Resource providers and types](resource-manager-supported-services.md).</span></span>

## <a name="when-to-call-support"></a><span data-ttu-id="afc1c-136">呼叫支援的時機</span><span class="sxs-lookup"><span data-stu-id="afc1c-136">When to call support</span></span>
<span data-ttu-id="afc1c-137">您可以透過本主題顯示的自助式作業，移動大部分資源。</span><span class="sxs-lookup"><span data-stu-id="afc1c-137">You can move most resources through the self-service operations shown in this topic.</span></span> <span data-ttu-id="afc1c-138">使用自助式作業︰</span><span class="sxs-lookup"><span data-stu-id="afc1c-138">Use the self-service operations to:</span></span>

* <span data-ttu-id="afc1c-139">移動 Resource Manager 資源。</span><span class="sxs-lookup"><span data-stu-id="afc1c-139">Move Resource Manager resources.</span></span>
* <span data-ttu-id="afc1c-140">根據[傳統部署限制](#classic-deployment-limitations)移動傳統資源。</span><span class="sxs-lookup"><span data-stu-id="afc1c-140">Move classic resources according to the [classic deployment limitations](#classic-deployment-limitations).</span></span>

<span data-ttu-id="afc1c-141">當您需要進行下列作業時，請連絡支援人員︰</span><span class="sxs-lookup"><span data-stu-id="afc1c-141">Call support when you need to:</span></span>

* <span data-ttu-id="afc1c-142">將資源移至新的 Azure 帳戶 (與 Azure Active Directory 租用戶)。</span><span class="sxs-lookup"><span data-stu-id="afc1c-142">Move your resources to a new Azure account (and Azure Active Directory tenant).</span></span>
* <span data-ttu-id="afc1c-143">移動傳統資源，但有限制的問題。</span><span class="sxs-lookup"><span data-stu-id="afc1c-143">Move classic resources but are having trouble with the limitations.</span></span>

## <a name="services-that-enable-move"></a><span data-ttu-id="afc1c-144">啟用移動的服務</span><span class="sxs-lookup"><span data-stu-id="afc1c-144">Services that enable move</span></span>
<span data-ttu-id="afc1c-145">目前啟用移動到新資源群組與訂用帳戶的服務有：</span><span class="sxs-lookup"><span data-stu-id="afc1c-145">For now, the services that enable moving to both a new resource group and subscription are:</span></span>

* <span data-ttu-id="afc1c-146">API 管理</span><span class="sxs-lookup"><span data-stu-id="afc1c-146">API Management</span></span>
* <span data-ttu-id="afc1c-147">App Service 應用程式 (Web 應用程式) - 請參閱 [App Service 限制](#app-service-limitations)</span><span class="sxs-lookup"><span data-stu-id="afc1c-147">App Service apps (web apps) - see [App Service limitations](#app-service-limitations)</span></span>
* <span data-ttu-id="afc1c-148">Application Insights</span><span class="sxs-lookup"><span data-stu-id="afc1c-148">Application Insights</span></span>
* <span data-ttu-id="afc1c-149">自動化</span><span class="sxs-lookup"><span data-stu-id="afc1c-149">Automation</span></span>
* <span data-ttu-id="afc1c-150">Batch</span><span class="sxs-lookup"><span data-stu-id="afc1c-150">Batch</span></span>
* <span data-ttu-id="afc1c-151">Bing 地圖</span><span class="sxs-lookup"><span data-stu-id="afc1c-151">Bing Maps</span></span>
* <span data-ttu-id="afc1c-152">CDN</span><span class="sxs-lookup"><span data-stu-id="afc1c-152">CDN</span></span>
* <span data-ttu-id="afc1c-153">雲端服務 - 請參閱 [傳統部署限制](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="afc1c-153">Cloud Services - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="afc1c-154">辨識服務</span><span class="sxs-lookup"><span data-stu-id="afc1c-154">Cognitive Services</span></span>
* <span data-ttu-id="afc1c-155">內容仲裁</span><span class="sxs-lookup"><span data-stu-id="afc1c-155">Content Moderator</span></span>
* <span data-ttu-id="afc1c-156">資料目錄</span><span class="sxs-lookup"><span data-stu-id="afc1c-156">Data Catalog</span></span>
* <span data-ttu-id="afc1c-157">Data Factory</span><span class="sxs-lookup"><span data-stu-id="afc1c-157">Data Factory</span></span>
* <span data-ttu-id="afc1c-158">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="afc1c-158">Data Lake Analytics</span></span>
* <span data-ttu-id="afc1c-159">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="afc1c-159">Data Lake Store</span></span>
* <span data-ttu-id="afc1c-160">DNS</span><span class="sxs-lookup"><span data-stu-id="afc1c-160">DNS</span></span>
* <span data-ttu-id="afc1c-161">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="afc1c-161">Azure Cosmos DB</span></span>
* <span data-ttu-id="afc1c-162">事件中樞</span><span class="sxs-lookup"><span data-stu-id="afc1c-162">Event Hubs</span></span>
* <span data-ttu-id="afc1c-163">HDInsight 叢集 - 請參閱 [HDInsight 限制](#hdinsight-limitations)</span><span class="sxs-lookup"><span data-stu-id="afc1c-163">HDInsight clusters - see [HDInsight limitations](#hdinsight-limitations)</span></span>
* <span data-ttu-id="afc1c-164">IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="afc1c-164">IoT Hubs</span></span>
* <span data-ttu-id="afc1c-165">Key Vault</span><span class="sxs-lookup"><span data-stu-id="afc1c-165">Key Vault</span></span>
* <span data-ttu-id="afc1c-166">負載平衡器</span><span class="sxs-lookup"><span data-stu-id="afc1c-166">Load Balancers</span></span>
* <span data-ttu-id="afc1c-167">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="afc1c-167">Logic Apps</span></span>
* <span data-ttu-id="afc1c-168">機器學習服務</span><span class="sxs-lookup"><span data-stu-id="afc1c-168">Machine Learning</span></span>
* <span data-ttu-id="afc1c-169">媒體服務</span><span class="sxs-lookup"><span data-stu-id="afc1c-169">Media Services</span></span>
* <span data-ttu-id="afc1c-170">Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="afc1c-170">Mobile Engagement</span></span>
* <span data-ttu-id="afc1c-171">通知中樞</span><span class="sxs-lookup"><span data-stu-id="afc1c-171">Notification Hubs</span></span>
* <span data-ttu-id="afc1c-172">Operational Insights</span><span class="sxs-lookup"><span data-stu-id="afc1c-172">Operational Insights</span></span>
* <span data-ttu-id="afc1c-173">Operations Management</span><span class="sxs-lookup"><span data-stu-id="afc1c-173">Operations Management</span></span>
* <span data-ttu-id="afc1c-174">Power BI</span><span class="sxs-lookup"><span data-stu-id="afc1c-174">Power BI</span></span>
* <span data-ttu-id="afc1c-175">Redis 快取</span><span class="sxs-lookup"><span data-stu-id="afc1c-175">Redis Cache</span></span>
* <span data-ttu-id="afc1c-176">排程器</span><span class="sxs-lookup"><span data-stu-id="afc1c-176">Scheduler</span></span>
* <span data-ttu-id="afc1c-177">搜尋</span><span class="sxs-lookup"><span data-stu-id="afc1c-177">Search</span></span>
* <span data-ttu-id="afc1c-178">伺服器管理</span><span class="sxs-lookup"><span data-stu-id="afc1c-178">Server Management</span></span>
* <span data-ttu-id="afc1c-179">服務匯流排</span><span class="sxs-lookup"><span data-stu-id="afc1c-179">Service Bus</span></span>
* <span data-ttu-id="afc1c-180">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="afc1c-180">Service Fabric</span></span>
* <span data-ttu-id="afc1c-181">儲存體</span><span class="sxs-lookup"><span data-stu-id="afc1c-181">Storage</span></span>
* <span data-ttu-id="afc1c-182">儲存體 (傳統) - 請參閱 [傳統部署限制](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="afc1c-182">Storage (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="afc1c-183">串流分析 - 無法移動執行中狀態的串流分析作業。</span><span class="sxs-lookup"><span data-stu-id="afc1c-183">Stream Analytics - Stream Analytics jobs cannot be moved when in running state.</span></span>
* <span data-ttu-id="afc1c-184">SQL Database 伺服器 - 資料庫和伺服器必須位於相同的資源群組。</span><span class="sxs-lookup"><span data-stu-id="afc1c-184">SQL Database server - The database and server must reside in the same resource group.</span></span> <span data-ttu-id="afc1c-185">當您移動 SQL 伺服器時，其所有資料庫也會跟著移動。</span><span class="sxs-lookup"><span data-stu-id="afc1c-185">When you move a SQL server, all its databases are also moved.</span></span>
* <span data-ttu-id="afc1c-186">流量管理員</span><span class="sxs-lookup"><span data-stu-id="afc1c-186">Traffic Manager</span></span>
* <span data-ttu-id="afc1c-187">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="afc1c-187">Virtual Machines</span></span>
* <span data-ttu-id="afc1c-188">憑證儲存在 Key Vault 中的虛擬機器 - 已啟用移動至相同訂用帳戶中新資源群組的功能，但未啟用跨訂用帳戶之間的移動。</span><span class="sxs-lookup"><span data-stu-id="afc1c-188">Virtual Machines with certificate stored in Key Vault - Move to new resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="afc1c-189">虛擬機器 (傳統) - 請參閱 [傳統部署限制](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="afc1c-189">Virtual Machines (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="afc1c-190">虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="afc1c-190">Virtual Machine Scale Sets</span></span>
* <span data-ttu-id="afc1c-191">虛擬網路 - 目前，在停用 VNet 對等互連之前，將無法移動對等的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="afc1c-191">Virtual Networks - Currently, a peered Virtual Network cannot be moved until VNet peering has been disabled.</span></span> <span data-ttu-id="afc1c-192">一旦停用之後，就能成功移動虛擬網路，並接著啟用 VNet 對等互連。</span><span class="sxs-lookup"><span data-stu-id="afc1c-192">Once disabled, the Virtual Network can be moved successfully and the VNet peering can be enabled.</span></span> <span data-ttu-id="afc1c-193">此外，如果虛擬網路包含任何有資源導覽連結的子網路，則無法將虛擬網路移動到其他訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="afc1c-193">In addition, a Virtual Network cannot be moved to a different subscription if the Virtual Network contains any subnet with resource navigation links.</span></span> <span data-ttu-id="afc1c-194">例如，當 Microsoft.Cache Redis 資源部署到虛擬網路子網路時，該子網路便具有資源導覽連結。</span><span class="sxs-lookup"><span data-stu-id="afc1c-194">For example, a Virtual Network subnet has a resource navigation link when a Microsoft.Cache redis resource is deployed into this subnet.</span></span>
* <span data-ttu-id="afc1c-195">VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="afc1c-195">VPN Gateway</span></span>


## <a name="services-that-do-not-enable-move"></a><span data-ttu-id="afc1c-196">不啟用移動的服務</span><span class="sxs-lookup"><span data-stu-id="afc1c-196">Services that do not enable move</span></span>
<span data-ttu-id="afc1c-197">目前不啟用移動資源的服務有：</span><span class="sxs-lookup"><span data-stu-id="afc1c-197">The services that currently do not enable moving a resource are:</span></span>

* <span data-ttu-id="afc1c-198">AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="afc1c-198">AD Domain Services</span></span>
* <span data-ttu-id="afc1c-199">AD 混合式健康狀態服務</span><span class="sxs-lookup"><span data-stu-id="afc1c-199">AD Hybrid Health Service</span></span>
* <span data-ttu-id="afc1c-200">應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="afc1c-200">Application Gateway</span></span>
* <span data-ttu-id="afc1c-201">具有使用受控磁碟之虛擬機器的可用性設定組</span><span class="sxs-lookup"><span data-stu-id="afc1c-201">Availability sets with Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="afc1c-202">BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="afc1c-202">BizTalk Services</span></span>
* <span data-ttu-id="afc1c-203">容器服務</span><span class="sxs-lookup"><span data-stu-id="afc1c-203">Container Service</span></span>
* <span data-ttu-id="afc1c-204">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="afc1c-204">Express Route</span></span>
* <span data-ttu-id="afc1c-205">DevTest Labs - 已啟用移動至相同訂用帳戶中新資源群組的功能，但未啟用跨訂用帳戶之間的移動。</span><span class="sxs-lookup"><span data-stu-id="afc1c-205">DevTest Labs - Move to new resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="afc1c-206">Dynamics LCS</span><span class="sxs-lookup"><span data-stu-id="afc1c-206">Dynamics LCS</span></span>
* <span data-ttu-id="afc1c-207">從受控磁碟建立的映像</span><span class="sxs-lookup"><span data-stu-id="afc1c-207">Images created from Managed Disks</span></span>
* <span data-ttu-id="afc1c-208">受控磁碟</span><span class="sxs-lookup"><span data-stu-id="afc1c-208">Managed Disks</span></span>
* <span data-ttu-id="afc1c-209">受管理的應用程式</span><span class="sxs-lookup"><span data-stu-id="afc1c-209">Managed Applications</span></span>
* <span data-ttu-id="afc1c-210">復原服務保存庫 - 也不會移動與「復原服務」保存庫關聯的「計算」、「網路」及「儲存體」資源，請參閱 [復原服務限制](#recovery-services-limitations)。</span><span class="sxs-lookup"><span data-stu-id="afc1c-210">Recovery Services vault - also do not move the Compute, Network, and Storage resources associated with the Recovery Services vault, see [Recovery Services limitations](#recovery-services-limitations).</span></span>
* <span data-ttu-id="afc1c-211">安全性</span><span class="sxs-lookup"><span data-stu-id="afc1c-211">Security</span></span>
* <span data-ttu-id="afc1c-212">從受控磁碟建立的快照集</span><span class="sxs-lookup"><span data-stu-id="afc1c-212">Snapshots created from Managed Disks</span></span>
* <span data-ttu-id="afc1c-213">StorSimple 裝置管理員</span><span class="sxs-lookup"><span data-stu-id="afc1c-213">StorSimple Device Manager</span></span>
* <span data-ttu-id="afc1c-214">使用受控磁碟的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="afc1c-214">Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="afc1c-215">虛擬網路 (傳統) - 請參閱 [傳統部署限制](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="afc1c-215">Virtual Networks (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="afc1c-216">從 Marketplace 資源建立的虛擬機器 - 無法在訂用帳戶之間移動。</span><span class="sxs-lookup"><span data-stu-id="afc1c-216">Virtual Machines created from Marketplace resources - cannot be moved across subscriptions.</span></span> <span data-ttu-id="afc1c-217">資源必須先在目前的訂用帳戶中取消佈建，並於新訂用帳戶中再次部署</span><span class="sxs-lookup"><span data-stu-id="afc1c-217">Resource needs to be deprovisioned in the current subscription and deployed again in the new subscription</span></span>

## <a name="app-service-limitations"></a><span data-ttu-id="afc1c-218">App Service 限制</span><span class="sxs-lookup"><span data-stu-id="afc1c-218">App Service limitations</span></span>
<span data-ttu-id="afc1c-219">使用 App Service 應用程式時，您無法只移動 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="afc1c-219">When working with App Service apps, you cannot move only an App Service plan.</span></span> <span data-ttu-id="afc1c-220">若要移動 App Service 應用程式，您的選項如下：</span><span class="sxs-lookup"><span data-stu-id="afc1c-220">To move App Service apps, your options are:</span></span>

* <span data-ttu-id="afc1c-221">將該資源群組中的 App Service 方案和所有其他 App Service 資源，都移到還沒有 App Service 資源的新資源群組。</span><span class="sxs-lookup"><span data-stu-id="afc1c-221">Move the App Service plan and all other App Service resources in that resource group to a new resource group that does not already have App Service resources.</span></span> <span data-ttu-id="afc1c-222">這項需求意謂著您甚至必須移動與 App Service 方案沒有關聯的 App Service 資源。</span><span class="sxs-lookup"><span data-stu-id="afc1c-222">This requirement means you must move even the App Service resources that are not associated with the App Service plan.</span></span>
* <span data-ttu-id="afc1c-223">將應用程式移到不同的資源群組，但在原始資源群組中保留所有 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="afc1c-223">Move the apps to a different resource group, but keep all App Service plans in the original resource group.</span></span>

<span data-ttu-id="afc1c-224">App Service 方案不需要與應用程式位於相同的資源群組，應用程式就能正確運作。</span><span class="sxs-lookup"><span data-stu-id="afc1c-224">The App Service plan does not need to reside in the same resource group as the app for the app to function correctly.</span></span>

<span data-ttu-id="afc1c-225">例如，如果您的資源群組包含︰</span><span class="sxs-lookup"><span data-stu-id="afc1c-225">For example, if your resource group contains:</span></span>

* <span data-ttu-id="afc1c-226">與 **plan-a** 關聯的 **web-a**</span><span class="sxs-lookup"><span data-stu-id="afc1c-226">**web-a** which is associated with **plan-a**</span></span>
* <span data-ttu-id="afc1c-227">與 **plan-b** 關聯的 **web-b**</span><span class="sxs-lookup"><span data-stu-id="afc1c-227">**web-b** which is associated with **plan-b**</span></span>

<span data-ttu-id="afc1c-228">您的選項如下：</span><span class="sxs-lookup"><span data-stu-id="afc1c-228">Your options are:</span></span>

* <span data-ttu-id="afc1c-229">移動 **web-a**、**plan-a**、**web-b** 及 **plan-b**</span><span class="sxs-lookup"><span data-stu-id="afc1c-229">Move **web-a**, **plan-a**, **web-b**, and **plan-b**</span></span>
* <span data-ttu-id="afc1c-230">移動 **web-a** 和 **web-b**</span><span class="sxs-lookup"><span data-stu-id="afc1c-230">Move **web-a** and **web-b**</span></span>
* <span data-ttu-id="afc1c-231">移動 **web-a**</span><span class="sxs-lookup"><span data-stu-id="afc1c-231">Move **web-a**</span></span>
* <span data-ttu-id="afc1c-232">移動 **web-b**</span><span class="sxs-lookup"><span data-stu-id="afc1c-232">Move **web-b**</span></span>

<span data-ttu-id="afc1c-233">所有其他組合都會留下移動 App Service 方案時無法留下的資源類型 (任何類型的 App Service 資源)。</span><span class="sxs-lookup"><span data-stu-id="afc1c-233">All other combinations involve leaving behind a resource type that can't be left behind when moving an App Service plan (any type of App Service resource).</span></span>

<span data-ttu-id="afc1c-234">如果 Web 應用程式與其 App Service 方案位於不同的資源群組，但您想要將兩者移到新的資源群組，則必須使用兩個步驟來執行移動。</span><span class="sxs-lookup"><span data-stu-id="afc1c-234">If your web app resides in a different resource group than its App Service plan but you want to move both to a new resource group, you must perform the move in two steps.</span></span> <span data-ttu-id="afc1c-235">例如：</span><span class="sxs-lookup"><span data-stu-id="afc1c-235">For example:</span></span>

* <span data-ttu-id="afc1c-236">**web-a** 位於 **web-group** 中</span><span class="sxs-lookup"><span data-stu-id="afc1c-236">**web-a** resides in **web-group**</span></span>
* <span data-ttu-id="afc1c-237">**plan-a** 位於 **plan-group** 中</span><span class="sxs-lookup"><span data-stu-id="afc1c-237">**plan-a** resides in **plan-group**</span></span>
* <span data-ttu-id="afc1c-238">您想要讓 **web-a** 和 **plan-a** 位於 **combined-group** 中</span><span class="sxs-lookup"><span data-stu-id="afc1c-238">You want **web-a** and **plan-a** to reside in **combined-group**</span></span>

<span data-ttu-id="afc1c-239">若要完成這項移動，請依下列序列執行兩個不同的移動作業︰</span><span class="sxs-lookup"><span data-stu-id="afc1c-239">To accomplish this move, perform two separate move operations in the following sequence:</span></span>

1. <span data-ttu-id="afc1c-240">將 **web-a** 移到 **plan-group**</span><span class="sxs-lookup"><span data-stu-id="afc1c-240">Move the **web-a** to **plan-group**</span></span>
2. <span data-ttu-id="afc1c-241">將 **web-a** 和 **plan-a** 移到 **combined-group**。</span><span class="sxs-lookup"><span data-stu-id="afc1c-241">Move **web-a** and **plan-a** to **combined-group**.</span></span>

<span data-ttu-id="afc1c-242">您可以將 App Service 憑證移至新資源群組或訂用帳戶，而不會發生任何問題。</span><span class="sxs-lookup"><span data-stu-id="afc1c-242">You can move an App Service Certificate to a new resource group or subscription without any issues.</span></span> <span data-ttu-id="afc1c-243">不過，如果您的 Web 應用程式包含在外部購買，並上傳至應用程式的 SSL 憑證，您必須在移動 Web 應用程式之前刪除憑證。</span><span class="sxs-lookup"><span data-stu-id="afc1c-243">However, if your web app includes an SSL certificate that you purchased externally and uploaded to the app, you must delete the certificate before moving the web app.</span></span> <span data-ttu-id="afc1c-244">例如，您可以執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="afc1c-244">For example, you can perform the following steps:</span></span>

1. <span data-ttu-id="afc1c-245">刪除從 Web 應用程式上傳的憑證</span><span class="sxs-lookup"><span data-stu-id="afc1c-245">Delete the uploaded certificate from the web app</span></span>
2. <span data-ttu-id="afc1c-246">移動 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="afc1c-246">Move the web app</span></span>
3. <span data-ttu-id="afc1c-247">將憑證上傳至 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="afc1c-247">Upload the certificate to the web app</span></span>

## <a name="recovery-services-limitations"></a><span data-ttu-id="afc1c-248">復原服務限制</span><span class="sxs-lookup"><span data-stu-id="afc1c-248">Recovery Services limitations</span></span>
<span data-ttu-id="afc1c-249">無法移動用來設定 Azure Site Recovery 相關災害復原的「儲存體」、「網路」或「計算」資源。</span><span class="sxs-lookup"><span data-stu-id="afc1c-249">Move is not enabled for Storage, Network, or Compute resources used to set up disaster recovery with Azure Site Recovery.</span></span>

<span data-ttu-id="afc1c-250">舉例來說，假設您已設定將內部部署機器複寫到某個儲存體帳戶 (Storage1)，而想要讓受保護的機器在容錯移轉到 Azure 之後，以連接到虛擬網路 (Network1) 的虛擬機器 (VM1) 身分上線。</span><span class="sxs-lookup"><span data-stu-id="afc1c-250">For example, suppose you have set up replication of your on-premises machines to a storage account (Storage1) and want the protected machine to come up after failover to Azure as a virtual machine (VM1) attached to a virtual network (Network1).</span></span> <span data-ttu-id="afc1c-251">您無法跨相同訂用帳戶內的資源群組或跨訂用帳戶來移動任何這些 Azure 資源 - Storage1、VM1 及 Network1。</span><span class="sxs-lookup"><span data-stu-id="afc1c-251">You cannot move any of these Azure resources - Storage1, VM1, and Network1 - across resource groups within the same subscription or across subscriptions.</span></span>

## <a name="hdinsight-limitations"></a><span data-ttu-id="afc1c-252">HDInsight 限制</span><span class="sxs-lookup"><span data-stu-id="afc1c-252">HDInsight limitations</span></span>

<span data-ttu-id="afc1c-253">您可以將 HDInsight 叢集移至新的訂用帳戶或資源群組。</span><span class="sxs-lookup"><span data-stu-id="afc1c-253">You can move HDInsight clusters to a new subscription or resource group.</span></span> <span data-ttu-id="afc1c-254">不過，您無法跨訂用帳戶來移動連結至 HDInsight 叢集的網路資源 (例如虛擬網路、NIC 或負載平衡器)。</span><span class="sxs-lookup"><span data-stu-id="afc1c-254">However, you cannot move across subscriptions the networking resources linked to the HDInsight cluster (such as the virtual network, NIC, or load balancer).</span></span> <span data-ttu-id="afc1c-255">此外，您無法將已連接至叢集虛擬機器的 NIC 移至新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="afc1c-255">In addition, you cannot move to a new resource group a NIC that is attached to a virtual machine for the cluster.</span></span>

<span data-ttu-id="afc1c-256">將 HDInsight 叢集移至新的訂用帳戶時，請先移動其他資源 (例如儲存體帳戶)。</span><span class="sxs-lookup"><span data-stu-id="afc1c-256">When moving an HDInsight cluster to a new subscription, first move other resources (like the storage account).</span></span> <span data-ttu-id="afc1c-257">然後，移動 HDInsight 叢集本身。</span><span class="sxs-lookup"><span data-stu-id="afc1c-257">Then, move the HDInsight cluster by itself.</span></span>

## <a name="classic-deployment-limitations"></a><span data-ttu-id="afc1c-258">傳統部署限制</span><span class="sxs-lookup"><span data-stu-id="afc1c-258">Classic deployment limitations</span></span>
<span data-ttu-id="afc1c-259">移動透過傳統模型所部署之資源的選項，會根據移動訂用帳戶內的資源還是將資源移到新的訂用帳戶而有所不同。</span><span class="sxs-lookup"><span data-stu-id="afc1c-259">The options for moving resources deployed through the classic model differ based on whether you are moving the resources within a subscription or to a new subscription.</span></span>

### <a name="same-subscription"></a><span data-ttu-id="afc1c-260">相同訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="afc1c-260">Same subscription</span></span>
<span data-ttu-id="afc1c-261">將資源從一個資源群組移到相同訂用帳戶內的另一個資源群組時，適用下列限制︰</span><span class="sxs-lookup"><span data-stu-id="afc1c-261">When moving resources from one resource group to another resource group within the same subscription, the following restrictions apply:</span></span>

* <span data-ttu-id="afc1c-262">無法移動虛擬網路 (傳統)。</span><span class="sxs-lookup"><span data-stu-id="afc1c-262">Virtual networks (classic) cannot be moved.</span></span>
* <span data-ttu-id="afc1c-263">虛擬機器 (傳統) 必須與雲端服務一起移動。</span><span class="sxs-lookup"><span data-stu-id="afc1c-263">Virtual machines (classic) must be moved with the cloud service.</span></span>
* <span data-ttu-id="afc1c-264">只有當移動作業包含雲端服務的所有虛擬機器時，才能移動雲端服務。</span><span class="sxs-lookup"><span data-stu-id="afc1c-264">Cloud service can only be moved when the move includes all its virtual machines.</span></span>
* <span data-ttu-id="afc1c-265">一次只能移動一個雲端服務。</span><span class="sxs-lookup"><span data-stu-id="afc1c-265">Only one cloud service can be moved at a time.</span></span>
* <span data-ttu-id="afc1c-266">一次只能移動一個儲存體帳戶 (傳統)。</span><span class="sxs-lookup"><span data-stu-id="afc1c-266">Only one storage account (classic) can be moved at a time.</span></span>
* <span data-ttu-id="afc1c-267">透過相同的作業，儲存體帳戶 (傳統) 不能與虛擬機器或雲端服務一起移動。</span><span class="sxs-lookup"><span data-stu-id="afc1c-267">Storage account (classic) cannot be moved in the same operation with a virtual machine or a cloud service.</span></span>

<span data-ttu-id="afc1c-268">若要將傳統資源移到相同訂用帳戶內的新資源群組，請透過[入口網站](#use-portal)、[Azure PowerShell](#use-powershell)、[Azure CLI](#use-azure-cli) 或 [REST API](#use-rest-api)，使用標準移動作業。</span><span class="sxs-lookup"><span data-stu-id="afc1c-268">To move classic resources to a new resource group within the same subscription, use the standard move operations through the [portal](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), or [REST API](#use-rest-api).</span></span> <span data-ttu-id="afc1c-269">當您移動 Resource Manager 資源時，您會使用相同的作業。</span><span class="sxs-lookup"><span data-stu-id="afc1c-269">You use the same operations as you use for moving Resource Manager resources.</span></span>

### <a name="new-subscription"></a><span data-ttu-id="afc1c-270">新的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="afc1c-270">New subscription</span></span>
<span data-ttu-id="afc1c-271">將資源移到新訂用帳戶時，適用下列限制︰</span><span class="sxs-lookup"><span data-stu-id="afc1c-271">When moving resources to a new subscription, the following restrictions apply:</span></span>

* <span data-ttu-id="afc1c-272">必須透過相同的作業移動訂用帳戶中的所有傳統資源。</span><span class="sxs-lookup"><span data-stu-id="afc1c-272">All classic resources in the subscription must be moved in the same operation.</span></span>
* <span data-ttu-id="afc1c-273">目標訂用帳戶不得包含任何其他傳統資源。</span><span class="sxs-lookup"><span data-stu-id="afc1c-273">The target subscription must not contain any other classic resources.</span></span>
* <span data-ttu-id="afc1c-274">只能透過適用於傳統移動的個別 REST API 來要求移動。</span><span class="sxs-lookup"><span data-stu-id="afc1c-274">The move can only be requested through a separate REST API for classic moves.</span></span> <span data-ttu-id="afc1c-275">將傳統資源移到新的訂用帳戶時，標準 Resource Manager 移動命令無法運作。</span><span class="sxs-lookup"><span data-stu-id="afc1c-275">The standard Resource Manager move commands do not work when moving classic resources to a new subscription.</span></span>

<span data-ttu-id="afc1c-276">若要將傳統資源移到新的訂用帳戶，請使用傳統資源特定的 REST 作業。</span><span class="sxs-lookup"><span data-stu-id="afc1c-276">To move classic resources to a new subscription, use the REST operations that are specific to classic resources.</span></span> <span data-ttu-id="afc1c-277">若要使用 REST，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="afc1c-277">To use REST, perform the following steps:</span></span>

1. <span data-ttu-id="afc1c-278">請檢查來源訂用帳戶是否可以參與跨訂用帳戶移動。</span><span class="sxs-lookup"><span data-stu-id="afc1c-278">Check if the source subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="afc1c-279">請使用下列作業：</span><span class="sxs-lookup"><span data-stu-id="afc1c-279">Use the following operation:</span></span>

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="afc1c-280">在要求本文中包含：</span><span class="sxs-lookup"><span data-stu-id="afc1c-280">In the request body, include:</span></span>

  ```json
  {
    "role": "source"
  }
  ```

     <span data-ttu-id="afc1c-281">驗證作業的回應格式如下︰</span><span class="sxs-lookup"><span data-stu-id="afc1c-281">The response for the validation operation is in the following format:</span></span>

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. <span data-ttu-id="afc1c-282">請檢查目的地訂用帳戶是否可以參與跨訂用帳戶移動。</span><span class="sxs-lookup"><span data-stu-id="afc1c-282">Check if the destination subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="afc1c-283">請使用下列作業：</span><span class="sxs-lookup"><span data-stu-id="afc1c-283">Use the following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="afc1c-284">在要求本文中包含：</span><span class="sxs-lookup"><span data-stu-id="afc1c-284">In the request body, include:</span></span>

  ```json
  {
    "role": "target"
  }
  ```

     <span data-ttu-id="afc1c-285">回應的格式與來源訂用帳戶驗證的格式相同。</span><span class="sxs-lookup"><span data-stu-id="afc1c-285">The response is in the same format as the source subscription validation.</span></span>
3. <span data-ttu-id="afc1c-286">如果兩個訂用帳戶都通過驗證，使用下列作業將所有傳統資源從某個訂用帳戶移到另一個訂用帳戶︰</span><span class="sxs-lookup"><span data-stu-id="afc1c-286">If both subscriptions pass validation, move all classic resources from one subscription to another subscription with the following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    <span data-ttu-id="afc1c-287">在要求本文中包含：</span><span class="sxs-lookup"><span data-stu-id="afc1c-287">In the request body, include:</span></span>

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

<span data-ttu-id="afc1c-288">這項作業可能需要幾分鐘的時間執行。</span><span class="sxs-lookup"><span data-stu-id="afc1c-288">The operation may run for several minutes.</span></span>

## <a name="use-portal"></a><span data-ttu-id="afc1c-289">使用入口網站</span><span class="sxs-lookup"><span data-stu-id="afc1c-289">Use portal</span></span>
<span data-ttu-id="afc1c-290">若要移動資源，請選取包含這些資源的資源群組，然後選取 [移動] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="afc1c-290">To move resources, select the resource group containing those resources, and then select the **Move** button.</span></span>

![移動資源](./media/resource-group-move-resources/select-move.png)

<span data-ttu-id="afc1c-292">選擇將資源移動到新的資源群組或新的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="afc1c-292">Select whether you are moving the resources to a new resource group or a new subscription.</span></span>

<span data-ttu-id="afc1c-293">選取要移動的資源和目的地資源群組。</span><span class="sxs-lookup"><span data-stu-id="afc1c-293">Select the resources to move and the destination resource group.</span></span> <span data-ttu-id="afc1c-294">認可您需要更新這些資源的指令碼，然後選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="afc1c-294">Acknowledge that you need to update scripts for these resources and select **OK**.</span></span> <span data-ttu-id="afc1c-295">如果您在上一個步驟中選取了 [編輯訂用帳戶] 圖示，則也必須選取目的地訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="afc1c-295">If you selected the edit subscription icon in the previous step, you must also select the destination subscription.</span></span>

![選取目的地](./media/resource-group-move-resources/select-destination.png)

<span data-ttu-id="afc1c-297">在 [通知] 中，您會看到移動作業正在執行。</span><span class="sxs-lookup"><span data-stu-id="afc1c-297">In **Notifications**, you see that the move operation is running.</span></span>

![顯示移動狀態](./media/resource-group-move-resources/show-status.png)

<span data-ttu-id="afc1c-299">完成後，您會收到結果的通知。</span><span class="sxs-lookup"><span data-stu-id="afc1c-299">When it has completed, you are notified of the result.</span></span>

![顯示移動結果](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a><span data-ttu-id="afc1c-301">使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="afc1c-301">Use PowerShell</span></span>
<span data-ttu-id="afc1c-302">若要將現有的資源移動到另一個資源群組或訂用帳戶，請使用 `Move-AzureRmResource` 命令。</span><span class="sxs-lookup"><span data-stu-id="afc1c-302">To move existing resources to another resource group or subscription, use the `Move-AzureRmResource` command.</span></span>

<span data-ttu-id="afc1c-303">第一個範例顯示如何將某個資源移動到新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="afc1c-303">The first example shows how to move one resource to a new resource group.</span></span>

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

<span data-ttu-id="afc1c-304">第二個範例顯示如何將多個資源移動到新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="afc1c-304">The second example shows how to move multiple resources to a new resource group.</span></span>

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

<span data-ttu-id="afc1c-305">若要移動到新的訂用帳戶，請包含 `DestinationSubscriptionId`參數的值。</span><span class="sxs-lookup"><span data-stu-id="afc1c-305">To move to a new subscription, include a value for the `DestinationSubscriptionId` parameter.</span></span>

<span data-ttu-id="afc1c-306">系統會要求您確認您想要移動指定的資源。</span><span class="sxs-lookup"><span data-stu-id="afc1c-306">You are asked to confirm that you want to move the specified resources.</span></span>

```powershell
Confirm
Are you sure you want to move these resources to the resource group
'/subscriptions/{guid}/resourceGroups/newRG' the resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a><span data-ttu-id="afc1c-307">使用 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="afc1c-307">Use Azure CLI 2.0</span></span>
<span data-ttu-id="afc1c-308">若要將現有的資源移動到另一個資源群組或訂用帳戶，請使用 `az resource move` 命令。</span><span class="sxs-lookup"><span data-stu-id="afc1c-308">To move existing resources to another resource group or subscription, use the `az resource move` command.</span></span> <span data-ttu-id="afc1c-309">提供要移動之資源的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="afc1c-309">Provide the resource IDs of the resources to move.</span></span> <span data-ttu-id="afc1c-310">您可以使用下列命令取得資源識別碼︰</span><span class="sxs-lookup"><span data-stu-id="afc1c-310">You can get resource IDs with the following command:</span></span>

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

<span data-ttu-id="afc1c-311">下列範例說明如何將儲存體帳戶移動到新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="afc1c-311">The following example shows how to move a storage account to a new resource group.</span></span> <span data-ttu-id="afc1c-312">請在 `--ids` 參數中，為要移動的資源識別碼提供以空格分隔的清單。</span><span class="sxs-lookup"><span data-stu-id="afc1c-312">In the `--ids` parameter, provide a space-separated list of the resource IDs to move.</span></span>

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

<span data-ttu-id="afc1c-313">若要移動到新的訂用帳戶，請提供 `--destination-subscription-id` 參數。</span><span class="sxs-lookup"><span data-stu-id="afc1c-313">To move to a new subscription, provide the `--destination-subscription-id` parameter.</span></span>

## <a name="use-azure-cli-10"></a><span data-ttu-id="afc1c-314">使用 Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="afc1c-314">Use Azure CLI 1.0</span></span>
<span data-ttu-id="afc1c-315">若要將現有的資源移動到另一個資源群組或訂用帳戶，請使用 `azure resource move` 命令。</span><span class="sxs-lookup"><span data-stu-id="afc1c-315">To move existing resources to another resource group or subscription, use the `azure resource move` command.</span></span> <span data-ttu-id="afc1c-316">提供要移動之資源的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="afc1c-316">Provide the resource IDs of the resources to move.</span></span> <span data-ttu-id="afc1c-317">您可以使用下列命令取得資源識別碼︰</span><span class="sxs-lookup"><span data-stu-id="afc1c-317">You can get resource IDs with the following command:</span></span>

```azurecli
azure resource list -g sourceGroup --json
```

<span data-ttu-id="afc1c-318">它會傳回下列格式︰</span><span class="sxs-lookup"><span data-stu-id="afc1c-318">Which returns the following format:</span></span>

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

<span data-ttu-id="afc1c-319">下列範例說明如何將儲存體帳戶移動到新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="afc1c-319">The following example shows how to move a storage account to a new resource group.</span></span> <span data-ttu-id="afc1c-320">請在 `-i` 參數中，為要移動的資源識別碼提供以逗號分隔的清單。</span><span class="sxs-lookup"><span data-stu-id="afc1c-320">In the `-i` parameter, provide a comma-separated list of the resource IDs to move.</span></span>

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

<span data-ttu-id="afc1c-321">系統會要求您確認您想要移動指定的資源。</span><span class="sxs-lookup"><span data-stu-id="afc1c-321">You are asked to confirm that you want to move the specified resource.</span></span>

## <a name="use-rest-api"></a><span data-ttu-id="afc1c-322">使用 REST API</span><span class="sxs-lookup"><span data-stu-id="afc1c-322">Use REST API</span></span>
<span data-ttu-id="afc1c-323">若要將現有的資源移動到另一個資源群組或訂用帳戶，請執行：</span><span class="sxs-lookup"><span data-stu-id="afc1c-323">To move existing resources to another resource group or subscription, run:</span></span>

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

<span data-ttu-id="afc1c-324">在要求主體中，您可以指定目標資源群組以及要移動的資源。</span><span class="sxs-lookup"><span data-stu-id="afc1c-324">In the request body, you specify the target resource group and the resources to move.</span></span> <span data-ttu-id="afc1c-325">如需有關 REST 移動作業的詳細資訊，請參閱 [移動資源](https://msdn.microsoft.com/library/azure/mt218710.aspx)。</span><span class="sxs-lookup"><span data-stu-id="afc1c-325">For more information about the move REST operation, see [Move resources](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="afc1c-326">後續步驟</span><span class="sxs-lookup"><span data-stu-id="afc1c-326">Next steps</span></span>
* <span data-ttu-id="afc1c-327">若要了解用於管理訂用帳戶的 PowerShell Cmdlet，請參閱 [搭配使用 Azure PowerShell 與 Azure Resource Manager](powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="afc1c-327">To learn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="afc1c-328">若要了解用於管理訂用帳戶的 Azure CLI 命令，請參閱 [搭配使用 Azure CLI 與 Azure Resource Manager](xplat-cli-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="afc1c-328">To learn about Azure CLI commands for managing your subscription, see [Using the Azure CLI with Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="afc1c-329">若要了解用於管理訂用帳戶的入口網站功能，請參閱 [使用 Azure 入口網站來管理資源](resource-group-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="afc1c-329">To learn about portal features for managing your subscription, see [Using the Azure portal to manage resources](resource-group-portal.md).</span></span>
* <span data-ttu-id="afc1c-330">若要了解如何將邏輯組織套用到您的資源，請參閱 [使用標記來組織您的資源](resource-group-using-tags.md)。</span><span class="sxs-lookup"><span data-stu-id="afc1c-330">To learn about applying a logical organization to your resources, see [Using tags to organize your resources](resource-group-using-tags.md).</span></span>
