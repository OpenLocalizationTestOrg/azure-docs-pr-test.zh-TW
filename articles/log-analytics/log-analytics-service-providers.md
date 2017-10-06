---
title: "aaaLog 服務提供者的分析功能 |Microsoft 文件"
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
ms.openlocfilehash: 3c0a93232293f90385c6c724be436cee1cf855f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-features-for-service-providers"></a><span data-ttu-id="03b37-103">服務提供者的 Log Analytics 功能</span><span class="sxs-lookup"><span data-stu-id="03b37-103">Log Analytics features for Service Providers</span></span>
<span data-ttu-id="03b37-104">Log Analytics 可協助管理服務提供者 (MSP)、大型企業、獨立軟體廠商 (ISV) 和主機服務提供者管理和監視客戶的內部部署或雲端基礎結構中的伺服器。</span><span class="sxs-lookup"><span data-stu-id="03b37-104">Log Analytics can help managed service providers (MSPs), large enterprises, independent software vendors (ISVs), and hosting service providers manage and monitor servers in customer's on-premises or cloud infrastructure.</span></span> 

<span data-ttu-id="03b37-105">大型企業與服務提供者有許多相似之處，特別是當有集中式的 IT 團隊負責管理許多不同業務單位的 IT 時。</span><span class="sxs-lookup"><span data-stu-id="03b37-105">Large enterprises share many similarities with service providers, particularly when there is a centralized IT team that is responsible for managing IT for many different business units.</span></span> <span data-ttu-id="03b37-106">為了簡單起見，本文件會使用 hello 詞彙*服務提供者*但 hello 相同的功能也適用於企業和其他客戶。</span><span class="sxs-lookup"><span data-stu-id="03b37-106">For simplicity, this document uses hello term *service provider* but hello same functionality is also available for enterprises and other customers.</span></span>

## <a name="cloud-solution-provider"></a><span data-ttu-id="03b37-107">雲端解決方案提供者</span><span class="sxs-lookup"><span data-stu-id="03b37-107">Cloud Solution Provider</span></span>
<span data-ttu-id="03b37-108">合作夥伴和服務提供者屬於 hello[雲端方案提供者 (CSP)](https://partner.microsoft.com/Solutions/cloud-reseller-overview)程式，記錄分析是其中一個 hello CSP 訂用帳戶可用的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="03b37-108">For partners and service providers who are part of hello [Cloud Solution Provider (CSP)](https://partner.microsoft.com/Solutions/cloud-reseller-overview) program, Log Analytics is one of hello Azure services available on a CSP subscription.</span></span> 

<span data-ttu-id="03b37-109">供記錄分析中啟用下列功能的 hello*雲端方案提供者*訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="03b37-109">For Log Analytics, hello following capabilities are enabled in *Cloud Solution Provider* subscriptions.</span></span>

<span data-ttu-id="03b37-110">身為「雲端解決方案提供者」，您可以：</span><span class="sxs-lookup"><span data-stu-id="03b37-110">As a *Cloud Solution Provider* you can:</span></span>

* <span data-ttu-id="03b37-111">在租用戶 (客戶) 訂用帳戶中建立 Log Analytics 工作區。</span><span class="sxs-lookup"><span data-stu-id="03b37-111">Create Log Analytics workspaces in a tenant (customer's) subscription.</span></span>
* <span data-ttu-id="03b37-112">存取租用戶建立的工作區。</span><span class="sxs-lookup"><span data-stu-id="03b37-112">Access workspaces created by tenants.</span></span> 
* <span data-ttu-id="03b37-113">加入和移除使用者存取 toohello 工作區中使用 Azure 的使用者管理。</span><span class="sxs-lookup"><span data-stu-id="03b37-113">Add and remove user access toohello workspace using Azure user management.</span></span> <span data-ttu-id="03b37-114">租用戶的工作區中 hello OMS 入口網站的 hello 使用者管理頁面，設定下無法使用時</span><span class="sxs-lookup"><span data-stu-id="03b37-114">When in a tenant’s workspace in hello OMS portal hello user management page under Settings is not available</span></span>
  * <span data-ttu-id="03b37-115">記錄分析不支援以角色為基礎的存取權但-讓使用者`reader`hello Azure 入口網站中的權限可讓它們 toomake 組態變更 hello OMS 入口網站中</span><span class="sxs-lookup"><span data-stu-id="03b37-115">Log Analytics does not support role-based access yet - giving a user `reader` permission in hello Azure portal allows them toomake configuration changes in hello OMS portal</span></span>

<span data-ttu-id="03b37-116">toolog tooa 租用戶的訂用帳戶中，您需要 toospecify hello 租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="03b37-116">toolog in tooa tenant’s subscription, you need toospecify hello tenant identifier.</span></span> <span data-ttu-id="03b37-117">hello 租用戶識別碼通常是 hello 電子郵件地址使用 toosign 中的最後一部分。</span><span class="sxs-lookup"><span data-stu-id="03b37-117">hello tenant identifier is often that last part of hello e-mail address used toosign in.</span></span>

* <span data-ttu-id="03b37-118">在 hello OMS 入口網站，加入`?tenant=contoso.com`hello hello 入口網站的 URL 中。</span><span class="sxs-lookup"><span data-stu-id="03b37-118">In hello OMS portal, add `?tenant=contoso.com` in hello URL for hello portal.</span></span> <span data-ttu-id="03b37-119">例如， `mms.microsoft.com/?tenant=contoso.com`</span><span class="sxs-lookup"><span data-stu-id="03b37-119">For example, `mms.microsoft.com/?tenant=contoso.com`</span></span>
* <span data-ttu-id="03b37-120">在 PowerShell 中，使用 hello`-Tenant contoso.com`參數使用時`Add-AzureRmAccount`cmdlet</span><span class="sxs-lookup"><span data-stu-id="03b37-120">In PowerShell, use hello `-Tenant contoso.com` parameter when using `Add-AzureRmAccount` cmdlet</span></span>
* <span data-ttu-id="03b37-121">當您使用 hello hello 租用戶識別碼會自動加入`OMS portal`從 hello Azure 入口網站 tooopen 連結並登入 toohello hello 選取工作區的 OMS 入口網站</span><span class="sxs-lookup"><span data-stu-id="03b37-121">hello tenant identifier is automatically added when you use hello `OMS portal` link from hello Azure portal tooopen and log in toohello OMS portal for hello selected workspace</span></span>

<span data-ttu-id="03b37-122">身為「雲端解決方案提供者」的「客戶」，您可以：</span><span class="sxs-lookup"><span data-stu-id="03b37-122">As a *customer* of a Cloud Solution Provider you can:</span></span>

* <span data-ttu-id="03b37-123">在 CSP 訂用帳戶中建立 Log Analytics 工作區</span><span class="sxs-lookup"><span data-stu-id="03b37-123">Create log analytics workspaces in a CSP subscription</span></span>
* <span data-ttu-id="03b37-124">存取工作區建立 hello CSP</span><span class="sxs-lookup"><span data-stu-id="03b37-124">Access workspaces created by hello CSP</span></span>
  * <span data-ttu-id="03b37-125">使用 hello`OMS portal`從 hello Azure 入口網站 tooopen 連結並登入 toohello hello 選取工作區的 OMS 入口網站</span><span class="sxs-lookup"><span data-stu-id="03b37-125">Use hello `OMS portal` link from hello Azure portal tooopen and log in toohello OMS portal for hello selected workspace</span></span>
* <span data-ttu-id="03b37-126">檢視及使用 hello 使用者管理頁面設定下 hello OMS 入口網站中</span><span class="sxs-lookup"><span data-stu-id="03b37-126">View and use hello user management page under Settings in hello OMS portal</span></span>

> [!NOTE]
> <span data-ttu-id="03b37-127">hello 包含備份和記錄分析的 Site Recovery 解決方案都不能 tooconnect tooa 復原服務保存庫無法設定 CSP 的訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="03b37-127">hello included Backup and Site Recovery solutions for Log Analytics are not able tooconnect tooa Recovery Services vault and cannot be configured in a CSP subscription.</span></span> 
> 
> 

## <a name="managing-multiple-customers-using-log-analytics"></a><span data-ttu-id="03b37-128">使用 Log Analytics 管理多個客戶</span><span class="sxs-lookup"><span data-stu-id="03b37-128">Managing multiple customers using Log Analytics</span></span>
<span data-ttu-id="03b37-129">建議您為每個您管理的客戶建立 Log Analytics 工作區。</span><span class="sxs-lookup"><span data-stu-id="03b37-129">It is recommended that you create a Log Analytics workspace for each customer you manage.</span></span> <span data-ttu-id="03b37-130">Log Analytics 工作區提供：</span><span class="sxs-lookup"><span data-stu-id="03b37-130">A Log Analytics workspace provides:</span></span>

* <span data-ttu-id="03b37-131">儲存資料 toobe 地理位置。</span><span class="sxs-lookup"><span data-stu-id="03b37-131">A geographic location for data toobe stored.</span></span> 
* <span data-ttu-id="03b37-132">計費的細微度</span><span class="sxs-lookup"><span data-stu-id="03b37-132">Granularity for billing</span></span> 
* <span data-ttu-id="03b37-133">資料隔離</span><span class="sxs-lookup"><span data-stu-id="03b37-133">Data isolation</span></span> 
* <span data-ttu-id="03b37-134">唯一的組態</span><span class="sxs-lookup"><span data-stu-id="03b37-134">Unique configuration</span></span>

<span data-ttu-id="03b37-135">藉由建立每個客戶的工作區，您可以 tookeep 個別的每個客戶的資料而且也追蹤 hello 每一位客戶的使用方式。</span><span class="sxs-lookup"><span data-stu-id="03b37-135">By creating a workspace per customer, you are able tookeep each customer’s data separate and also track hello usage of each customer.</span></span>

<span data-ttu-id="03b37-136">時間和原因 toocreate 多個工作區中描述的詳細[管理存取 toolog 分析](log-analytics-manage-access.md#determine-the-number-of-workspaces-you-need)。</span><span class="sxs-lookup"><span data-stu-id="03b37-136">More details on when and why toocreate multiple workspaces is described in [manage access toolog analytics](log-analytics-manage-access.md#determine-the-number-of-workspaces-you-need).</span></span>

<span data-ttu-id="03b37-137">建立及設定客戶工作區可以使用自動化[PowerShell](log-analytics-powershell-workspace-configuration.md)，[資源管理員範本](log-analytics-template-workspace-configuration.md)，或使用 hello [REST API](https://www.nuget.org/packages/Microsoft.Azure.Management.OperationalInsights/)。</span><span class="sxs-lookup"><span data-stu-id="03b37-137">Creation and configuration of customer workspaces can be automated using [PowerShell](log-analytics-powershell-workspace-configuration.md), [Resource Manager templates](log-analytics-template-workspace-configuration.md), or using hello [REST API](https://www.nuget.org/packages/Microsoft.Azure.Management.OperationalInsights/).</span></span>

<span data-ttu-id="03b37-138">hello 使用工作區中設定資源管理員範本可讓您 toohave 主要的設定，可以使用的 toocreate 並設定工作區。</span><span class="sxs-lookup"><span data-stu-id="03b37-138">hello use of Resource Manager templates for workspace configuration allows you toohave a master configuration that can be used toocreate and configure workspaces.</span></span> <span data-ttu-id="03b37-139">您可以放心工作區建立的客戶會自動設定 tooyour 需求。</span><span class="sxs-lookup"><span data-stu-id="03b37-139">You can be confident that as workspaces are created for customers they are automatically configured tooyour requirements.</span></span> <span data-ttu-id="03b37-140">當您更新您的需求時，hello 範本會更新，然後重新套用 hello 現有工作區。</span><span class="sxs-lookup"><span data-stu-id="03b37-140">When you update your requirements, hello template is updated and then reapplied hello existing workspaces.</span></span> <span data-ttu-id="03b37-141">此程序可確保現有的工作區符合新的標準。</span><span class="sxs-lookup"><span data-stu-id="03b37-141">This process ensures that even existing workspaces meet your new standards.</span></span>    

<span data-ttu-id="03b37-142">當管理多個記錄分析工作區，我們建議您與您現有的票證系統整合每個工作區 / operations 主控台使用 hello[警示](log-analytics-alerts.md)功能。</span><span class="sxs-lookup"><span data-stu-id="03b37-142">When managing multiple Log Analytics workspaces, we recommend integrating each workspace with your existing ticketing system / operations console using hello [Alerts](log-analytics-alerts.md) functionality.</span></span> <span data-ttu-id="03b37-143">藉由整合與您現有的系統，支援人員可以繼續 toofollow 其熟悉的程序。</span><span class="sxs-lookup"><span data-stu-id="03b37-143">By integrating with your existing systems, support staff can continue toofollow their familiar processes.</span></span> <span data-ttu-id="03b37-144">記錄分析會定期檢查 hello 警示的準則，您指定針對每個工作區，並不需要採取動作時產生警示。</span><span class="sxs-lookup"><span data-stu-id="03b37-144">Log Analytics regularly checks each workspace against hello alert criteria you specify and generates an alert when action is needed.</span></span>

<span data-ttu-id="03b37-145">個人化資料的檢視，使用 hello[儀表板](../azure-portal/azure-portal-dashboards.md)hello Azure 入口網站中的功能。</span><span class="sxs-lookup"><span data-stu-id="03b37-145">For personalized views of data, use hello [dashboard](../azure-portal/azure-portal-dashboards.md) capability in hello Azure portal.</span></span>  

<span data-ttu-id="03b37-146">執行層級報表來總結資料工作區，您可以使用跨 hello 之間記錄分析的整合和[PowerBI](log-analytics-powerbi.md)。</span><span class="sxs-lookup"><span data-stu-id="03b37-146">For executive level reports that summarize data across workspaces you can use hello integration between Log Analytics and [PowerBI](log-analytics-powerbi.md).</span></span> <span data-ttu-id="03b37-147">如果您需要 toointegrate 與另一個報告系統，您可以使用 hello 搜尋 API (透過 PowerShell 或[REST](log-analytics-log-search-api.md)) toorun 查詢和匯出搜尋結果。</span><span class="sxs-lookup"><span data-stu-id="03b37-147">If you need toointegrate with another reporting system, you can use hello Search API (via PowerShell or [REST](log-analytics-log-search-api.md)) toorun queries and export search results.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03b37-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="03b37-148">Next Steps</span></span>
* <span data-ttu-id="03b37-149">使用 [Resource Manager 範本](log-analytics-template-workspace-configuration.md)建立和設定工作區</span><span class="sxs-lookup"><span data-stu-id="03b37-149">Automate creation and configuration of workspaces using [Resource Manager templates](log-analytics-template-workspace-configuration.md)</span></span>
* <span data-ttu-id="03b37-150">使用 [PowerShell](log-analytics-powershell-workspace-configuration.md)自動建立工作區</span><span class="sxs-lookup"><span data-stu-id="03b37-150">Automate creation of workspaces using [PowerShell](log-analytics-powershell-workspace-configuration.md)</span></span> 
* <span data-ttu-id="03b37-151">使用[警示](log-analytics-alerts.md)toointegrate 與現有系統</span><span class="sxs-lookup"><span data-stu-id="03b37-151">Use [Alerts](log-analytics-alerts.md) toointegrate with existing systems</span></span>
* <span data-ttu-id="03b37-152">使用 [PowerBI](log-analytics-powerbi.md)產生摘要報告</span><span class="sxs-lookup"><span data-stu-id="03b37-152">Generate summary reports using [PowerBI](log-analytics-powerbi.md)</span></span>

