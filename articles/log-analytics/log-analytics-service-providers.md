---
title: "服務提供者的 Log Analytics 功能 | Microsoft Docs"
description: "Log Analytics 可協助管理服務提供者 (MSP)、大型企業、獨立軟體廠商 (ISV) 和主機服務提供者管理和監視客戶的內部部署或雲端基礎結構中的伺服器。"
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: c07f0b9f-ec37-480d-91ec-d9bcf6786464
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: richrund
ms.openlocfilehash: 8a67d9a9d345682e9e6c8f5c7779204a038f5f6a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="log-analytics-features-for-service-providers"></a><span data-ttu-id="f7cbf-103">服務提供者的 Log Analytics 功能</span><span class="sxs-lookup"><span data-stu-id="f7cbf-103">Log Analytics features for Service Providers</span></span>
<span data-ttu-id="f7cbf-104">Log Analytics 可協助管理服務提供者 (MSP)、大型企業、獨立軟體廠商 (ISV) 和主機服務提供者管理和監視客戶的內部部署或雲端基礎結構中的伺服器。</span><span class="sxs-lookup"><span data-stu-id="f7cbf-104">Log Analytics can help managed service providers (MSPs), large enterprises, independent software vendors (ISVs), and hosting service providers manage and monitor servers in customer's on-premises or cloud infrastructure.</span></span> 

<span data-ttu-id="f7cbf-105">大型企業與服務提供者有許多相似之處，特別是當有集中式的 IT 團隊負責管理許多不同業務單位的 IT 時。</span><span class="sxs-lookup"><span data-stu-id="f7cbf-105">Large enterprises share many similarities with service providers, particularly when there is a centralized IT team that is responsible for managing IT for many different business units.</span></span> <span data-ttu-id="f7cbf-106">為了簡單起見，本文件會使用「服務提供者」這個詞彙，但是相同的功能也適用於企業或其他客戶。</span><span class="sxs-lookup"><span data-stu-id="f7cbf-106">For simplicity, this document uses the term *service provider* but the same functionality is also available for enterprises and other customers.</span></span>

## <a name="cloud-solution-provider"></a><span data-ttu-id="f7cbf-107">雲端解決方案提供者</span><span class="sxs-lookup"><span data-stu-id="f7cbf-107">Cloud Solution Provider</span></span>
<span data-ttu-id="f7cbf-108">對於身為[雲端解決方案提供者 (CSP)](https://partner.microsoft.com/Solutions/cloud-reseller-overview) 方案一部分的合作夥伴和服務提供者，Log Analytics 是 CSP 訂用帳戶上的其中一個可用 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="f7cbf-108">For partners and service providers who are part of the [Cloud Solution Provider (CSP)](https://partner.microsoft.com/Solutions/cloud-reseller-overview) program, Log Analytics is one of the Azure services available on a CSP subscription.</span></span> 

<span data-ttu-id="f7cbf-109">對於 Log Analytics，下列功能在「雲端解決方案提供者」訂用帳戶中啟用。</span><span class="sxs-lookup"><span data-stu-id="f7cbf-109">For Log Analytics, the following capabilities are enabled in *Cloud Solution Provider* subscriptions.</span></span>

<span data-ttu-id="f7cbf-110">身為「雲端解決方案提供者」，您可以：</span><span class="sxs-lookup"><span data-stu-id="f7cbf-110">As a *Cloud Solution Provider* you can:</span></span>

* <span data-ttu-id="f7cbf-111">在租用戶 (客戶) 訂用帳戶中建立 Log Analytics 工作區。</span><span class="sxs-lookup"><span data-stu-id="f7cbf-111">Create Log Analytics workspaces in a tenant (customer's) subscription.</span></span>
* <span data-ttu-id="f7cbf-112">存取租用戶建立的工作區。</span><span class="sxs-lookup"><span data-stu-id="f7cbf-112">Access workspaces created by tenants.</span></span> 
* <span data-ttu-id="f7cbf-113">使用 Azure 使用者管理，新增和移除使用者對工作區的存取權。</span><span class="sxs-lookup"><span data-stu-id="f7cbf-113">Add and remove user access to the workspace using Azure user management.</span></span> <span data-ttu-id="f7cbf-114">在 OMS 入口網站中租用戶的工作區時，[設定] 底下的使用者管理頁面無法使用</span><span class="sxs-lookup"><span data-stu-id="f7cbf-114">When in a tenant’s workspace in the OMS portal the user management page under Settings is not available</span></span>
  * <span data-ttu-id="f7cbf-115">Log Analytics 尚未支援以角色為基礎的存取 - 在 Azure 入口網站中授與使用者 `reader` 權限可讓他們在 OMS 入口網站中進行組態變更</span><span class="sxs-lookup"><span data-stu-id="f7cbf-115">Log Analytics does not support role-based access yet - giving a user `reader` permission in the Azure portal allows them to make configuration changes in the OMS portal</span></span>

<span data-ttu-id="f7cbf-116">若要登入租用戶的訂用帳戶，您需要指定租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="f7cbf-116">To log in to a tenant’s subscription, you need to specify the tenant identifier.</span></span> <span data-ttu-id="f7cbf-117">租用戶識別碼通常是您用來登入的電子郵件地址的最後一部分。</span><span class="sxs-lookup"><span data-stu-id="f7cbf-117">The tenant identifier is often that last part of the e-mail address used to sign in.</span></span>

* <span data-ttu-id="f7cbf-118">在 OMS 入口網站中，針對入口網站在 URL 新增 `?tenant=contoso.com`。</span><span class="sxs-lookup"><span data-stu-id="f7cbf-118">In the OMS portal, add `?tenant=contoso.com` in the URL for the portal.</span></span> <span data-ttu-id="f7cbf-119">例如，`mms.microsoft.com/?tenant=contoso.com`</span><span class="sxs-lookup"><span data-stu-id="f7cbf-119">For example, `mms.microsoft.com/?tenant=contoso.com`</span></span>
* <span data-ttu-id="f7cbf-120">在 PowerShell 中，使用 `Add-AzureRmAccount` Cmdlet 時使用 `-Tenant contoso.com` 參數</span><span class="sxs-lookup"><span data-stu-id="f7cbf-120">In PowerShell, use the `-Tenant contoso.com` parameter when using `Add-AzureRmAccount` cmdlet</span></span>
* <span data-ttu-id="f7cbf-121">當您從 Azure 入口網站使用 `OMS portal` 連結，來開啟並登入所選取工作區的 OMS 入口網站時，會自動新增租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="f7cbf-121">The tenant identifier is automatically added when you use the `OMS portal` link from the Azure portal to open and log in to the OMS portal for the selected workspace</span></span>

<span data-ttu-id="f7cbf-122">身為「雲端解決方案提供者」的「客戶」，您可以：</span><span class="sxs-lookup"><span data-stu-id="f7cbf-122">As a *customer* of a Cloud Solution Provider you can:</span></span>

* <span data-ttu-id="f7cbf-123">在 CSP 訂用帳戶中建立 Log Analytics 工作區</span><span class="sxs-lookup"><span data-stu-id="f7cbf-123">Create log analytics workspaces in a CSP subscription</span></span>
* <span data-ttu-id="f7cbf-124">存取 CSP 建立的工作區</span><span class="sxs-lookup"><span data-stu-id="f7cbf-124">Access workspaces created by the CSP</span></span>
  * <span data-ttu-id="f7cbf-125">從 Azure 入口網站使用 `OMS portal` 連結，來開啟並登入所選取工作區的 OMS 入口網站</span><span class="sxs-lookup"><span data-stu-id="f7cbf-125">Use the `OMS portal` link from the Azure portal to open and log in to the OMS portal for the selected workspace</span></span>
* <span data-ttu-id="f7cbf-126">檢視及使用 OMS 入口網站中 [設定] 底下的使用者管理頁面</span><span class="sxs-lookup"><span data-stu-id="f7cbf-126">View and use the user management page under Settings in the OMS portal</span></span>

> [!NOTE]
> <span data-ttu-id="f7cbf-127">Log Analytics 內含的備份和 Site Recovery 解決方案無法連接至復原服務保存庫，且無法在 CSP 訂用帳戶中設定。</span><span class="sxs-lookup"><span data-stu-id="f7cbf-127">The included Backup and Site Recovery solutions for Log Analytics are not able to connect to a Recovery Services vault and cannot be configured in a CSP subscription.</span></span> 
> 
> 

## <a name="managing-multiple-customers-using-log-analytics"></a><span data-ttu-id="f7cbf-128">使用 Log Analytics 管理多個客戶</span><span class="sxs-lookup"><span data-stu-id="f7cbf-128">Managing multiple customers using Log Analytics</span></span>
<span data-ttu-id="f7cbf-129">建議您為每個您管理的客戶建立 Log Analytics 工作區。</span><span class="sxs-lookup"><span data-stu-id="f7cbf-129">It is recommended that you create a Log Analytics workspace for each customer you manage.</span></span> <span data-ttu-id="f7cbf-130">Log Analytics 工作區提供：</span><span class="sxs-lookup"><span data-stu-id="f7cbf-130">A Log Analytics workspace provides:</span></span>

* <span data-ttu-id="f7cbf-131">儲存資料的地理位置。</span><span class="sxs-lookup"><span data-stu-id="f7cbf-131">A geographic location for data to be stored.</span></span> 
* <span data-ttu-id="f7cbf-132">計費的細微度</span><span class="sxs-lookup"><span data-stu-id="f7cbf-132">Granularity for billing</span></span> 
* <span data-ttu-id="f7cbf-133">資料隔離</span><span class="sxs-lookup"><span data-stu-id="f7cbf-133">Data isolation</span></span> 
* <span data-ttu-id="f7cbf-134">唯一的組態</span><span class="sxs-lookup"><span data-stu-id="f7cbf-134">Unique configuration</span></span>

<span data-ttu-id="f7cbf-135">藉由建立每個客戶的工作區，就能夠區隔每個客戶的資料，也可以追蹤每個客戶的使用方式。</span><span class="sxs-lookup"><span data-stu-id="f7cbf-135">By creating a workspace per customer, you are able to keep each customer’s data separate and also track the usage of each customer.</span></span>

<span data-ttu-id="f7cbf-136">[管理對 Log Analytics 的存取](log-analytics-manage-access.md#determine-the-number-of-workspaces-you-need)中會說明建立多個工作區之時機和原因的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f7cbf-136">More details on when and why to create multiple workspaces is described in [manage access to log analytics](log-analytics-manage-access.md#determine-the-number-of-workspaces-you-need).</span></span>

<span data-ttu-id="f7cbf-137">建立及設定客戶的工作區可以使用 [PowerShell](log-analytics-powershell-workspace-configuration.md)、[Resource Manager 範本](log-analytics-template-workspace-configuration.md)，或使用 [REST API](https://www.nuget.org/packages/Microsoft.Azure.Management.OperationalInsights/) 進行自動化。</span><span class="sxs-lookup"><span data-stu-id="f7cbf-137">Creation and configuration of customer workspaces can be automated using [PowerShell](log-analytics-powershell-workspace-configuration.md), [Resource Manager templates](log-analytics-template-workspace-configuration.md), or using the [REST API](https://www.nuget.org/packages/Microsoft.Azure.Management.OperationalInsights/).</span></span>

<span data-ttu-id="f7cbf-138">使用工作區組態的 Resource Manager 範本，可讓您具有主要組態，用來建立和設定工作區。</span><span class="sxs-lookup"><span data-stu-id="f7cbf-138">The use of Resource Manager templates for workspace configuration allows you to have a master configuration that can be used to create and configure workspaces.</span></span> <span data-ttu-id="f7cbf-139">您可以確信為客戶建立工作區時，會自動針對您的需求進行設定。</span><span class="sxs-lookup"><span data-stu-id="f7cbf-139">You can be confident that as workspaces are created for customers they are automatically configured to your requirements.</span></span> <span data-ttu-id="f7cbf-140">當您更新您的需求時，範本會更新，然後重新套用現有的工作區。</span><span class="sxs-lookup"><span data-stu-id="f7cbf-140">When you update your requirements, the template is updated and then reapplied the existing workspaces.</span></span> <span data-ttu-id="f7cbf-141">此程序可確保現有的工作區符合新的標準。</span><span class="sxs-lookup"><span data-stu-id="f7cbf-141">This process ensures that even existing workspaces meet your new standards.</span></span>    

<span data-ttu-id="f7cbf-142">在管理多個 Log Analytics 工作區時，我們建議使用[警示](log-analytics-alerts.md)功能，整合每個工作區與現有的票證系統/Operations 主控台。</span><span class="sxs-lookup"><span data-stu-id="f7cbf-142">When managing multiple Log Analytics workspaces, we recommend integrating each workspace with your existing ticketing system / operations console using the [Alerts](log-analytics-alerts.md) functionality.</span></span> <span data-ttu-id="f7cbf-143">藉由與您現有的系統整合，支援人員可以繼續依照其熟悉的程序。</span><span class="sxs-lookup"><span data-stu-id="f7cbf-143">By integrating with your existing systems, support staff can continue to follow their familiar processes.</span></span> <span data-ttu-id="f7cbf-144">Log Analytics 會定期針對您指定的警示準則檢查每個工作區，並且在需要採取動作時產生警示。</span><span class="sxs-lookup"><span data-stu-id="f7cbf-144">Log Analytics regularly checks each workspace against the alert criteria you specify and generates an alert when action is needed.</span></span>

<span data-ttu-id="f7cbf-145">若要建立個人化的資料檢視，請使用 Azure 入口網站中的[儀表板](../azure-portal/azure-portal-dashboards.md)功能。</span><span class="sxs-lookup"><span data-stu-id="f7cbf-145">For personalized views of data, use the [dashboard](../azure-portal/azure-portal-dashboards.md) capability in the Azure portal.</span></span>  

<span data-ttu-id="f7cbf-146">對於摘要跨工作區資料的執行層級報告，您可以使用 Log Analytics 與 [PowerBI](log-analytics-powerbi.md) 之間的整合。</span><span class="sxs-lookup"><span data-stu-id="f7cbf-146">For executive level reports that summarize data across workspaces you can use the integration between Log Analytics and [PowerBI](log-analytics-powerbi.md).</span></span> <span data-ttu-id="f7cbf-147">如果您需要與其他報告系統整合，您可以使用搜尋 API (透過 PowerShell 或 [REST](log-analytics-log-search-api.md)) 來執行查詢，並且匯出搜尋結果。</span><span class="sxs-lookup"><span data-stu-id="f7cbf-147">If you need to integrate with another reporting system, you can use the Search API (via PowerShell or [REST](log-analytics-log-search-api.md)) to run queries and export search results.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7cbf-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f7cbf-148">Next Steps</span></span>
* <span data-ttu-id="f7cbf-149">使用 [Resource Manager 範本](log-analytics-template-workspace-configuration.md)建立和設定工作區</span><span class="sxs-lookup"><span data-stu-id="f7cbf-149">Automate creation and configuration of workspaces using [Resource Manager templates](log-analytics-template-workspace-configuration.md)</span></span>
* <span data-ttu-id="f7cbf-150">使用 [PowerShell](log-analytics-powershell-workspace-configuration.md)自動建立工作區</span><span class="sxs-lookup"><span data-stu-id="f7cbf-150">Automate creation of workspaces using [PowerShell](log-analytics-powershell-workspace-configuration.md)</span></span> 
* <span data-ttu-id="f7cbf-151">使用[警示](log-analytics-alerts.md)與現有的系統整合</span><span class="sxs-lookup"><span data-stu-id="f7cbf-151">Use [Alerts](log-analytics-alerts.md) to integrate with existing systems</span></span>
* <span data-ttu-id="f7cbf-152">使用 [PowerBI](log-analytics-powerbi.md)產生摘要報告</span><span class="sxs-lookup"><span data-stu-id="f7cbf-152">Generate summary reports using [PowerBI](log-analytics-powerbi.md)</span></span>

