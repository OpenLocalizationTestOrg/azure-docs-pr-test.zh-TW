---
title: "aaaAzure 計費企業應用程式開發介面 |Microsoft 文件"
description: "深入了解 hello 報告 Api 以程式設計的方式讓企業 Azure 客戶 toopull 耗用量資料。"
services: 
documentationcenter: 
author: aedwin
manager: aedwin
editor: 
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/25/2017
ms.author: aedwin
ms.openlocfilehash: 017cecc57ad6bdeb402b5d9d57fc95df9b033a42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-reporting-apis-for-enterprise-customers"></a><span data-ttu-id="a421d-103">適用於企業客戶的報告 API 概觀</span><span class="sxs-lookup"><span data-stu-id="a421d-103">Overview of Reporting APIs for Enterprise customers</span></span>
<span data-ttu-id="a421d-104">hello 報告 Api 可讓企業 Azure 客戶 tooprogrammatically 提取耗用量和計費資料到慣用的資料分析工具。</span><span class="sxs-lookup"><span data-stu-id="a421d-104">hello Reporting APIs enable Enterprise Azure customers tooprogrammatically pull consumption and billing data into preferred data analysis tools.</span></span> 

## <a name="enabling-data-access-toohello-api"></a><span data-ttu-id="a421d-105">啟用資料存取 toohello API</span><span class="sxs-lookup"><span data-stu-id="a421d-105">Enabling data access toohello API</span></span>
* <span data-ttu-id="a421d-106">**產生或擷取 hello API 金鑰**-toohello 企業入口網站，然後遵循 hello 教學課程中說明的記錄檔-Reporting Api。</span><span class="sxs-lookup"><span data-stu-id="a421d-106">**Generate or retrieve hello API key** - Log in toohello Enterprise portal and follow hello tutorial under Help - Reporting APIs.</span></span> <span data-ttu-id="a421d-107">在此說明文章的 hello 第一節說明 hello toogenerate 或擷取 hello API 金鑰指定註冊的方式。</span><span class="sxs-lookup"><span data-stu-id="a421d-107">hello first section under this help article explains how toogenerate or retrieve hello API key for hello specified enrollment.</span></span>
* <span data-ttu-id="a421d-108">**傳入 hello API 金鑰**-hello API 金鑰需要 toobe 傳遞每個呼叫進行驗證和授權。</span><span class="sxs-lookup"><span data-stu-id="a421d-108">**Passing keys in hello API** - hello API key needs toobe passed for each call for Authentication and Authorization.</span></span> <span data-ttu-id="a421d-109">hello 下列屬性需要 toobe toohello HTTP 標頭</span><span class="sxs-lookup"><span data-stu-id="a421d-109">hello following property needs toobe toohello HTTP headers</span></span>

|<span data-ttu-id="a421d-110">要求標頭金鑰</span><span class="sxs-lookup"><span data-stu-id="a421d-110">Request Header Key</span></span> | <span data-ttu-id="a421d-111">值</span><span class="sxs-lookup"><span data-stu-id="a421d-111">Value</span></span>|
|-|-|
|<span data-ttu-id="a421d-112">Authorization</span><span class="sxs-lookup"><span data-stu-id="a421d-112">Authorization</span></span>| <span data-ttu-id="a421d-113">以此格式指定 hello 值： **bearer {API_KEY}**</span><span class="sxs-lookup"><span data-stu-id="a421d-113">Specify hello value in this format: **bearer {API_KEY}**</span></span> <br/> <span data-ttu-id="a421d-114">範例：bearer eyr....09</span><span class="sxs-lookup"><span data-stu-id="a421d-114">Example: bearer eyr....09</span></span>|

## <a name="consumption-apis"></a><span data-ttu-id="a421d-115">使用情況 API</span><span class="sxs-lookup"><span data-stu-id="a421d-115">Consumption APIs</span></span>
<span data-ttu-id="a421d-116">有可用 Swagger 端點[這裡](https://consumption.azure.com/swagger/ui/index)hello Api 低於此應該啟用簡單自我 hello API 和 hello 能力 toogenerate 用戶端 Sdk 的使用說明[AutoRest](https://github.com/Azure/AutoRest)或[Swagger CodeGen](http://swagger.io/swagger-codegen/)。</span><span class="sxs-lookup"><span data-stu-id="a421d-116">A Swagger endpoint is available [here](https://consumption.azure.com/swagger/ui/index) for hello APIs described below which should enable easy introspection of hello API and hello ability toogenerate client SDKs using [AutoRest](https://github.com/Azure/AutoRest) or [Swagger CodeGen](http://swagger.io/swagger-codegen/).</span></span> <span data-ttu-id="a421d-117">自 2014 年 5 月 1 日起的資料可透過此 API 取得。</span><span class="sxs-lookup"><span data-stu-id="a421d-117">Data beginning May 1, 2014 is available through this API.</span></span> 

* <span data-ttu-id="a421d-118">**平衡和摘要**-hello[平衡和摘要的應用程式開發介面](billing-enterprise-api-balance-summary.md)提供每月餘額、 購買、 Azure Marketplace 服務的費用、 調整及 overage 費用的詳細資訊的摘要。</span><span class="sxs-lookup"><span data-stu-id="a421d-118">**Balance and Summary** - hello [Balance and Summary API](billing-enterprise-api-balance-summary.md) offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments and overage charges.</span></span>

* <span data-ttu-id="a421d-119">**使用方式詳細資料**-hello[使用量詳細資料 API](billing-enterprise-api-usage-detail.md)提供已使用的數量和所註冊的估計的費用的每日明細。</span><span class="sxs-lookup"><span data-stu-id="a421d-119">**Usage Details** - hello [Usage Detail API](billing-enterprise-api-usage-detail.md) offers a daily breakdown of consumed quantities and estimated charges by an Enrollment.</span></span> <span data-ttu-id="a421d-120">hello 結果也會包含有關執行個體、 公尺和部門。</span><span class="sxs-lookup"><span data-stu-id="a421d-120">hello result also includes information on instances, meters and departments.</span></span> <span data-ttu-id="a421d-121">您可以查詢 hello API，計費週期或指定的開始和結束日期。</span><span class="sxs-lookup"><span data-stu-id="a421d-121">hello API can be queried by Billing period or by a specified start and end date.</span></span> 

* <span data-ttu-id="a421d-122">**Marketplace 商店電量**-hello [Marketplace 商店電量 API](billing-enterprise-api-marketplace-storecharge.md)傳回依日排列的 hello 基於使用方式的 marketplace 費用明細 hello 指定計費期間或開始和結束日期 （一次費用不包含）.</span><span class="sxs-lookup"><span data-stu-id="a421d-122">**Marketplace Store Charge** - hello [Marketplace Store Charge API](billing-enterprise-api-marketplace-storecharge.md) returns hello usage-based marketplace charges breakdown by day for hello specified Billing Period or start and end dates (one time fees are not included).</span></span>

* <span data-ttu-id="a421d-123">**價位表**-hello[價位表 API](billing-enterprise-api-pricesheet.md)提供每個計量器 hello 註冊和帳單週期 hello 適用的速率。</span><span class="sxs-lookup"><span data-stu-id="a421d-123">**Price Sheet** - hello [Price Sheet API](billing-enterprise-api-pricesheet.md) provides hello applicable rate for each Meter for hello given Enrollment and Billing Period.</span></span> 

## <a name="helper-apis"></a><span data-ttu-id="a421d-124">協助程式 API</span><span class="sxs-lookup"><span data-stu-id="a421d-124">Helper APIs</span></span>
 <span data-ttu-id="a421d-125">**列出計費週期**-hello[計費週期 API](billing-enterprise-api-billing-periods.md)會傳回一份計費週期 hello 依反向時間順序指定註冊都耗用量資料。</span><span class="sxs-lookup"><span data-stu-id="a421d-125">**List Billing Periods** - hello [Billing Periods API](billing-enterprise-api-billing-periods.md) returns a list of billing periods that have consumption data for hello specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="a421d-126">每個週期包含指向 hello 四組資料-BalanceSummary、 UsageDetails、 Marketplace 費用及價位表的 toohello API 路由的屬性。</span><span class="sxs-lookup"><span data-stu-id="a421d-126">Each Period contains a property pointing toohello API route for hello four sets of data - BalanceSummary, UsageDetails, Marketplace Charges, and Price Sheet.</span></span>


## <a name="api-response-codes"></a><span data-ttu-id="a421d-127">API 回應碼</span><span class="sxs-lookup"><span data-stu-id="a421d-127">API Response Codes</span></span>  
|<span data-ttu-id="a421d-128">回應狀態碼</span><span class="sxs-lookup"><span data-stu-id="a421d-128">Response Status Code</span></span>|<span data-ttu-id="a421d-129">訊息</span><span class="sxs-lookup"><span data-stu-id="a421d-129">Message</span></span>|<span data-ttu-id="a421d-130">描述</span><span class="sxs-lookup"><span data-stu-id="a421d-130">Description</span></span>|
|-|-|-|
|<span data-ttu-id="a421d-131">200</span><span class="sxs-lookup"><span data-stu-id="a421d-131">200</span></span>| <span data-ttu-id="a421d-132">OK</span><span class="sxs-lookup"><span data-stu-id="a421d-132">OK</span></span>|<span data-ttu-id="a421d-133">沒有錯誤</span><span class="sxs-lookup"><span data-stu-id="a421d-133">No error</span></span>|
|<span data-ttu-id="a421d-134">401</span><span class="sxs-lookup"><span data-stu-id="a421d-134">401</span></span>| <span data-ttu-id="a421d-135">未經授權</span><span class="sxs-lookup"><span data-stu-id="a421d-135">Unauthorized</span></span>| <span data-ttu-id="a421d-136">API 金鑰找不到、無效或過期等。</span><span class="sxs-lookup"><span data-stu-id="a421d-136">API Key not found, Invalid, Expired etc.</span></span>|
|<span data-ttu-id="a421d-137">404</span><span class="sxs-lookup"><span data-stu-id="a421d-137">404</span></span>| <span data-ttu-id="a421d-138">無法使用</span><span class="sxs-lookup"><span data-stu-id="a421d-138">Unavailable</span></span>| <span data-ttu-id="a421d-139">找不到報告端點</span><span class="sxs-lookup"><span data-stu-id="a421d-139">Report endpoint not found</span></span>|
|<span data-ttu-id="a421d-140">400</span><span class="sxs-lookup"><span data-stu-id="a421d-140">400</span></span>| <span data-ttu-id="a421d-141">不正確的要求</span><span class="sxs-lookup"><span data-stu-id="a421d-141">Bad Request</span></span>| <span data-ttu-id="a421d-142">無效的參數 - 資料範圍、EA 編號等。</span><span class="sxs-lookup"><span data-stu-id="a421d-142">Invalid params – Date ranges, EA numbers etc.</span></span>|
|<span data-ttu-id="a421d-143">500</span><span class="sxs-lookup"><span data-stu-id="a421d-143">500</span></span>| <span data-ttu-id="a421d-144">伺服器錯誤</span><span class="sxs-lookup"><span data-stu-id="a421d-144">Server Error</span></span>| <span data-ttu-id="a421d-145">處理要求時發生未預期的錯誤</span><span class="sxs-lookup"><span data-stu-id="a421d-145">Unexoected error processing request</span></span>| 









