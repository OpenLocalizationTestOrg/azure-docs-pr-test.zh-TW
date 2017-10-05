---
title: "使用 SQL 資料倉儲建置整合式解決方案 | Microsoft Docs"
description: "工具以及提供可與 SQL 資料倉儲整合之解決方案的合作夥伴。 "
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: e2dc8f3f-10e3-4589-a4e2-50c67dfcf67f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: d407c29f99fd7537590ec787febd84a9e3f4f353
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="leverage-other-services-with-sql-data-warehouse"></a><span data-ttu-id="37bdc-103">以 SQL 資料倉儲來搭配運用其他服務</span><span class="sxs-lookup"><span data-stu-id="37bdc-103">Leverage other services with SQL Data Warehouse</span></span>
<span data-ttu-id="37bdc-104">除了其核心功能，SQL 資料倉儲可讓使用者搭配運用許多其他 Azure 中的服務。</span><span class="sxs-lookup"><span data-stu-id="37bdc-104">In addition to its core functionality, SQL Data Warehouse enables users to leverage many of the other services in Azure alongside it.</span></span>  <span data-ttu-id="37bdc-105">具體而言，我們目前已經採取步驟來深入整合下列項目：</span><span class="sxs-lookup"><span data-stu-id="37bdc-105">Specifically, we have currently taken steps to deeply integrate with the following:</span></span>

* <span data-ttu-id="37bdc-106">Power BI</span><span class="sxs-lookup"><span data-stu-id="37bdc-106">Power BI</span></span>
* <span data-ttu-id="37bdc-107">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="37bdc-107">Azure Data Factory</span></span>
* <span data-ttu-id="37bdc-108">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="37bdc-108">Azure Machine Learning</span></span>
* <span data-ttu-id="37bdc-109">Azure 串流分析</span><span class="sxs-lookup"><span data-stu-id="37bdc-109">Azure Stream Analytics</span></span>

<span data-ttu-id="37bdc-110">我們正努力連接多個跨 Azure 生態系統的服務。</span><span class="sxs-lookup"><span data-stu-id="37bdc-110">We are working to connect with more services across the Azure ecosystem.</span></span>

## <a name="power-bi"></a><span data-ttu-id="37bdc-111">Power BI</span><span class="sxs-lookup"><span data-stu-id="37bdc-111">Power BI</span></span>
<span data-ttu-id="37bdc-112">Power BI 整合可讓您運用 SQL 資料倉儲的計算能力以及 Power BI 的動態報告和視覺效果。</span><span class="sxs-lookup"><span data-stu-id="37bdc-112">Power BI integration allows you to leverage the compute power of SQL Data Warehouse with the dynamic reporting and visualization of Power BI.</span></span> <span data-ttu-id="37bdc-113">目前 Power BI 整合包括：</span><span class="sxs-lookup"><span data-stu-id="37bdc-113">Power BI integration currently includes:</span></span>

* <span data-ttu-id="37bdc-114">**直接連接**：針對 SQL 資料倉儲進行之邏輯下推的更進階連接。</span><span class="sxs-lookup"><span data-stu-id="37bdc-114">**Direct Connect**: A more advanced connection with logical pushdown against SQL Data Warehouse.</span></span>  <span data-ttu-id="37bdc-115">可提供更快速且更大規模的分析。</span><span class="sxs-lookup"><span data-stu-id="37bdc-115">This provides faster analysis on a larger scale.</span></span>
* <span data-ttu-id="37bdc-116">**在 Power BI 中開啟**：[在 Power BI 中開啟] 按鈕會傳遞執行個體資訊給 Power BI，允許更順暢的連接。</span><span class="sxs-lookup"><span data-stu-id="37bdc-116">**Open in Power BI**: The 'Open in Power BI' button passes instance information to Power BI, allowing for a more seamless connection.</span></span>

<span data-ttu-id="37bdc-117">如需詳細資訊，請參閱[整合 Power BI](sql-data-warehouse-integrate-power-bi.md) 或 [Power BI 文件](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx)。</span><span class="sxs-lookup"><span data-stu-id="37bdc-117">See [Integrate with Power BI](sql-data-warehouse-integrate-power-bi.md) or the [Power BI documentation](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) for more information.</span></span>

## <a name="azure-data-factory"></a><span data-ttu-id="37bdc-118">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="37bdc-118">Azure Data Factory</span></span>
<span data-ttu-id="37bdc-119">Azure Data Factory 提供使用者一個受管理的平台，以建立複雜的擷取-載入管線。</span><span class="sxs-lookup"><span data-stu-id="37bdc-119">Azure Data Factory gives users a managed platform to create complex Extract-Load pipelines.</span></span>  <span data-ttu-id="37bdc-120">SQL 資料倉儲與 Azure Data Factory 的整合包含下列內容：</span><span class="sxs-lookup"><span data-stu-id="37bdc-120">SQL Data Warehouse's integration with Azure Data Factory includes the following:</span></span>

* <span data-ttu-id="37bdc-121">**預存程序**：協調 SQL 資料倉儲上的預存程序的執行。</span><span class="sxs-lookup"><span data-stu-id="37bdc-121">**Stored Procedures**: Orchestrate the execution of stored procedures on SQL Data Warehouse.</span></span>
* <span data-ttu-id="37bdc-122">**複製**：使用 ADF 將資料移到「SQL 資料倉儲」中。</span><span class="sxs-lookup"><span data-stu-id="37bdc-122">**Copy**: Use ADF to move data into SQL Data Warehouse.</span></span>  <span data-ttu-id="37bdc-123">這項作業可以在幕後使用 ADF 的標準資料移動機制或 PolyBase。</span><span class="sxs-lookup"><span data-stu-id="37bdc-123">This operation can use ADF's standard data movement mechanism or PolyBase under the covers.</span></span> 

<span data-ttu-id="37bdc-124">如需詳細資訊，請參閱[與 Azure Data Factory 整合](sql-data-warehouse-integrate-azure-data-factory.md)或 [Azure Data Factory 文件](https://azure.microsoft.com/documentation/services/data-factory/)。</span><span class="sxs-lookup"><span data-stu-id="37bdc-124">See [Integrate with Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) or the [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/) for more information.</span></span>

## <a name="azure-machine-learning"></a><span data-ttu-id="37bdc-125">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="37bdc-125">Azure Machine Learning</span></span>
<span data-ttu-id="37bdc-126">Azure Machine Learning 是完全受管理的分析服務，可讓使用者建立運用一組大型預測工具的複雜模型。</span><span class="sxs-lookup"><span data-stu-id="37bdc-126">Azure Machine Learning is a fully managed analytics service which allows users to create intricate models leveraging a large set of predictive tools.</span></span>  <span data-ttu-id="37bdc-127">SQL 資料倉儲可支援做為模型的來源和目的地，具備下列功能：</span><span class="sxs-lookup"><span data-stu-id="37bdc-127">SQL Data Warehouse is supported as both a source and destination for these models with the following functionality:</span></span>

* <span data-ttu-id="37bdc-128">**讀取資料：** 針對 SQL 資料倉儲透過 T-SQL 大規模驅動模型。</span><span class="sxs-lookup"><span data-stu-id="37bdc-128">**Read Data:** Drive models at scale using T-SQL against SQL Data Warehouse.</span></span>
* <span data-ttu-id="37bdc-129">**寫入資料：** 認可從任何模型回到 SQL 資料倉儲的變更。</span><span class="sxs-lookup"><span data-stu-id="37bdc-129">**Write Data:** Commit changes from any model back to SQL Data Warehouse.</span></span>

<span data-ttu-id="37bdc-130">如需詳細資訊，請參閱[與 Azure Machine Learning 整合](sql-data-warehouse-integrate-azure-machine-learning.md)或 [Azure 機器學習文件](https://azure.microsoft.com/services/machine-learning/)。</span><span class="sxs-lookup"><span data-stu-id="37bdc-130">See [Integrate with Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) or the [Azure Machine Learning documentation](https://azure.microsoft.com/services/machine-learning/) for more information.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="37bdc-131">Azure 串流分析</span><span class="sxs-lookup"><span data-stu-id="37bdc-131">Azure Stream Analytics</span></span>
<span data-ttu-id="37bdc-132">Azure 串流分析是複雜、完全受管理的基礎結構，可處理和取用產生自 Azure 事件中樞的事件資料。</span><span class="sxs-lookup"><span data-stu-id="37bdc-132">Azure Stream Analytics is a complex, fully managed infrastructure for processing and consuming event data generated from Azure Event Hub.</span></span>  <span data-ttu-id="37bdc-133">與 SQL 資料倉儲的整合可讓串流資料有效地處理並與相關資料一起儲存以啟用更深入、更進階的分析。</span><span class="sxs-lookup"><span data-stu-id="37bdc-133">Integration with SQL Data Warehouse allows for streaming data to be effectively processed and stored alongside relational data enabling deeper, more advanced analysis.</span></span>  

* <span data-ttu-id="37bdc-134">**工作輸出：** 將來自資料流分析工作的輸出直接傳送到 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="37bdc-134">**Job Output:** Send output from Stream Analytics jobs directly to SQL Data Warehouse.</span></span>

<span data-ttu-id="37bdc-135">如需詳細資訊，請參閱[與 Azure 串流分析整合](sql-data-warehouse-integrate-azure-stream-analytics.md)或 [Azure y 串流分析文件](https://azure.microsoft.com/documentation/services/stream-analytics/)。</span><span class="sxs-lookup"><span data-stu-id="37bdc-135">See [Integrate with Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) or the [Azure Stream Analytics documentation](https://azure.microsoft.com/documentation/services/stream-analytics/) for more information.</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop/

[Azure Data Factory]: sql-data-warehouse-integrate-azure-data-factory.md
[Azure Machine Learning]: sql-data-warehouse-integrate-azure-machine-learning.md
[Azure Stream Analytics]: sql-data-warehouse-integrate-azure-stream-analytics.md
[Power BI]: sql-data-warehouse-integrate-power-bi.md
[Partners]: sql-data-warehouse-partner-business-intelligence.md

<!--MSDN references-->

<!--Other Web references-->
