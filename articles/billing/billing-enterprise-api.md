---
title: "Azure 計費企業版 API | Microsoft Docs"
description: "了解可讓企業 Azure 客戶以程式設計方式提取使用情況資料的報告 API。"
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
ms.openlocfilehash: e3a5f9bcd6b54a51c29df649f1ae8ac185b153a1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="overview-of-reporting-apis-for-enterprise-customers"></a><span data-ttu-id="894db-103">適用於企業客戶的報告 API 概觀</span><span class="sxs-lookup"><span data-stu-id="894db-103">Overview of Reporting APIs for Enterprise customers</span></span>
<span data-ttu-id="894db-104">報告 API 可讓企業 Azure 客戶以程式設計方式提取使用情況和帳單資料，以使用慣用的資料分析工具進行分析。</span><span class="sxs-lookup"><span data-stu-id="894db-104">The Reporting APIs enable Enterprise Azure customers to programmatically pull consumption and billing data into preferred data analysis tools.</span></span> 

## <a name="enabling-data-access-to-the-api"></a><span data-ttu-id="894db-105">啟用對 API 的資料存取</span><span class="sxs-lookup"><span data-stu-id="894db-105">Enabling data access to the API</span></span>
* <span data-ttu-id="894db-106">**產生或擷取 API 金鑰** - 登入企業入口網站，並遵循 [說明] - [報告 API] 底下的教學課程。</span><span class="sxs-lookup"><span data-stu-id="894db-106">**Generate or retrieve the API key** - Log in to the Enterprise portal and follow the tutorial under Help - Reporting APIs.</span></span> <span data-ttu-id="894db-107">此說明文章的第一節說明如何針對指定的註冊產生或擷取 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="894db-107">The first section under this help article explains how to generate or retrieve the API key for the specified enrollment.</span></span>
* <span data-ttu-id="894db-108">**在 API 中傳遞金鑰** - 必須針對每個驗證和授權呼叫傳遞 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="894db-108">**Passing keys in the API** - The API key needs to be passed for each call for Authentication and Authorization.</span></span> <span data-ttu-id="894db-109">下列屬性必須是針對 HTTP 標頭</span><span class="sxs-lookup"><span data-stu-id="894db-109">The following property needs to be to the HTTP headers</span></span>

|<span data-ttu-id="894db-110">要求標頭金鑰</span><span class="sxs-lookup"><span data-stu-id="894db-110">Request Header Key</span></span> | <span data-ttu-id="894db-111">值</span><span class="sxs-lookup"><span data-stu-id="894db-111">Value</span></span>|
|-|-|
|<span data-ttu-id="894db-112">Authorization</span><span class="sxs-lookup"><span data-stu-id="894db-112">Authorization</span></span>| <span data-ttu-id="894db-113">以此格式指定值：**bearer {API_KEY}**</span><span class="sxs-lookup"><span data-stu-id="894db-113">Specify the value in this format: **bearer {API_KEY}**</span></span> <br/> <span data-ttu-id="894db-114">範例：bearer eyr....09</span><span class="sxs-lookup"><span data-stu-id="894db-114">Example: bearer eyr....09</span></span>|

## <a name="consumption-apis"></a><span data-ttu-id="894db-115">使用情況 API</span><span class="sxs-lookup"><span data-stu-id="894db-115">Consumption APIs</span></span>
<span data-ttu-id="894db-116">下述 API 的 Swagger 端點可在[這裡](https://consumption.azure.com/swagger/ui/index)取得，它可讓使用者輕鬆進行 API 自我檢查，並且能使用 [AutoRest](https://github.com/Azure/AutoRest) 或 [Swagger CodeGen](http://swagger.io/swagger-codegen/) 產生用戶端 SDK。</span><span class="sxs-lookup"><span data-stu-id="894db-116">A Swagger endpoint is available [here](https://consumption.azure.com/swagger/ui/index) for the APIs described below which should enable easy introspection of the API and the ability to generate client SDKs using [AutoRest](https://github.com/Azure/AutoRest) or [Swagger CodeGen](http://swagger.io/swagger-codegen/).</span></span> <span data-ttu-id="894db-117">自 2014 年 5 月 1 日起的資料可透過此 API 取得。</span><span class="sxs-lookup"><span data-stu-id="894db-117">Data beginning May 1, 2014 is available through this API.</span></span> 

* <span data-ttu-id="894db-118">**餘額與摘要** - [餘額與摘要 API](billing-enterprise-api-balance-summary.md) 可提供餘額、新購買、Azure Marketplace 服務費用、調整，以及超額部分費用的每月摘要資訊。</span><span class="sxs-lookup"><span data-stu-id="894db-118">**Balance and Summary** - The [Balance and Summary API](billing-enterprise-api-balance-summary.md) offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments and overage charges.</span></span>

* <span data-ttu-id="894db-119">**使用量詳細資料** - [使用量詳細資料 API](billing-enterprise-api-usage-detail.md) 可提供註冊之使用量和預估費用的每日明細。</span><span class="sxs-lookup"><span data-stu-id="894db-119">**Usage Details** - The [Usage Detail API](billing-enterprise-api-usage-detail.md) offers a daily breakdown of consumed quantities and estimated charges by an Enrollment.</span></span> <span data-ttu-id="894db-120">結果也包含執行個體、計量和部門的資訊。</span><span class="sxs-lookup"><span data-stu-id="894db-120">The result also includes information on instances, meters and departments.</span></span> <span data-ttu-id="894db-121">API 可依計費週期或指定開始和結束日期來查詢。</span><span class="sxs-lookup"><span data-stu-id="894db-121">The API can be queried by Billing period or by a specified start and end date.</span></span> 

* <span data-ttu-id="894db-122">**Marketplace 市集費用** - [Marketplace 市集費用 API](billing-enterprise-api-marketplace-storecharge.md) 可針對指定的計費週期或開始和結束日期，傳回以使用量為基礎的 Marketplace 費用每日明細 (不含一次性費用)。</span><span class="sxs-lookup"><span data-stu-id="894db-122">**Marketplace Store Charge** - The [Marketplace Store Charge API](billing-enterprise-api-marketplace-storecharge.md) returns the usage-based marketplace charges breakdown by day for the specified Billing Period or start and end dates (one time fees are not included).</span></span>

* <span data-ttu-id="894db-123">**價位表** - [價位表 API](billing-enterprise-api-pricesheet.md) 可針對指定註冊和計費週期的每個計量提供適用的費率。</span><span class="sxs-lookup"><span data-stu-id="894db-123">**Price Sheet** - The [Price Sheet API](billing-enterprise-api-pricesheet.md) provides the applicable rate for each Meter for the given Enrollment and Billing Period.</span></span> 

## <a name="helper-apis"></a><span data-ttu-id="894db-124">協助程式 API</span><span class="sxs-lookup"><span data-stu-id="894db-124">Helper APIs</span></span>
 <span data-ttu-id="894db-125">**列出計費週期** - [計費週期 API](billing-enterprise-api-billing-periods.md) 會傳回計費週期清單，其中包含所指定註冊的使用情況資料 (以反向時間順序排列)。</span><span class="sxs-lookup"><span data-stu-id="894db-125">**List Billing Periods** - The [Billing Periods API](billing-enterprise-api-billing-periods.md) returns a list of billing periods that have consumption data for the specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="894db-126">每個週期包含指向四組資料 (BalanceSummary、UsageDetails、Marketplace 費用和價位表) 之 API 路由的屬性。</span><span class="sxs-lookup"><span data-stu-id="894db-126">Each Period contains a property pointing to the API route for the four sets of data - BalanceSummary, UsageDetails, Marketplace Charges, and Price Sheet.</span></span>


## <a name="api-response-codes"></a><span data-ttu-id="894db-127">API 回應碼</span><span class="sxs-lookup"><span data-stu-id="894db-127">API Response Codes</span></span>  
|<span data-ttu-id="894db-128">回應狀態碼</span><span class="sxs-lookup"><span data-stu-id="894db-128">Response Status Code</span></span>|<span data-ttu-id="894db-129">訊息</span><span class="sxs-lookup"><span data-stu-id="894db-129">Message</span></span>|<span data-ttu-id="894db-130">描述</span><span class="sxs-lookup"><span data-stu-id="894db-130">Description</span></span>|
|-|-|-|
|<span data-ttu-id="894db-131">200</span><span class="sxs-lookup"><span data-stu-id="894db-131">200</span></span>| <span data-ttu-id="894db-132">OK</span><span class="sxs-lookup"><span data-stu-id="894db-132">OK</span></span>|<span data-ttu-id="894db-133">沒有錯誤</span><span class="sxs-lookup"><span data-stu-id="894db-133">No error</span></span>|
|<span data-ttu-id="894db-134">401</span><span class="sxs-lookup"><span data-stu-id="894db-134">401</span></span>| <span data-ttu-id="894db-135">未經授權</span><span class="sxs-lookup"><span data-stu-id="894db-135">Unauthorized</span></span>| <span data-ttu-id="894db-136">API 金鑰找不到、無效或過期等。</span><span class="sxs-lookup"><span data-stu-id="894db-136">API Key not found, Invalid, Expired etc.</span></span>|
|<span data-ttu-id="894db-137">404</span><span class="sxs-lookup"><span data-stu-id="894db-137">404</span></span>| <span data-ttu-id="894db-138">無法使用</span><span class="sxs-lookup"><span data-stu-id="894db-138">Unavailable</span></span>| <span data-ttu-id="894db-139">找不到報告端點</span><span class="sxs-lookup"><span data-stu-id="894db-139">Report endpoint not found</span></span>|
|<span data-ttu-id="894db-140">400</span><span class="sxs-lookup"><span data-stu-id="894db-140">400</span></span>| <span data-ttu-id="894db-141">不正確的要求</span><span class="sxs-lookup"><span data-stu-id="894db-141">Bad Request</span></span>| <span data-ttu-id="894db-142">無效的參數 - 資料範圍、EA 編號等。</span><span class="sxs-lookup"><span data-stu-id="894db-142">Invalid params – Date ranges, EA numbers etc.</span></span>|
|<span data-ttu-id="894db-143">500</span><span class="sxs-lookup"><span data-stu-id="894db-143">500</span></span>| <span data-ttu-id="894db-144">伺服器錯誤</span><span class="sxs-lookup"><span data-stu-id="894db-144">Server Error</span></span>| <span data-ttu-id="894db-145">處理要求時發生未預期的錯誤</span><span class="sxs-lookup"><span data-stu-id="894db-145">Unexoected error processing request</span></span>| 









