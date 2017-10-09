---
title: "aaaBuild SQL 資料倉儲與整合解決方案 |Microsoft 文件"
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
ms.openlocfilehash: c8a4202dd84305bea4e4c2faf0e4791d026e794f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="leverage-other-services-with-sql-data-warehouse"></a><span data-ttu-id="9650b-103">以 SQL 資料倉儲來搭配運用其他服務</span><span class="sxs-lookup"><span data-stu-id="9650b-103">Leverage other services with SQL Data Warehouse</span></span>
<span data-ttu-id="9650b-104">此外 tooits 核心功能，SQL 資料倉儲可讓使用者 tooleverage 許多 hello 中 Azure 旁邊的其他服務。</span><span class="sxs-lookup"><span data-stu-id="9650b-104">In addition tooits core functionality, SQL Data Warehouse enables users tooleverage many of hello other services in Azure alongside it.</span></span>  <span data-ttu-id="9650b-105">具體來說，我們目前採取 toodeeply 整合與 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9650b-105">Specifically, we have currently taken steps toodeeply integrate with hello following:</span></span>

* <span data-ttu-id="9650b-106">Power BI</span><span class="sxs-lookup"><span data-stu-id="9650b-106">Power BI</span></span>
* <span data-ttu-id="9650b-107">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9650b-107">Azure Data Factory</span></span>
* <span data-ttu-id="9650b-108">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9650b-108">Azure Machine Learning</span></span>
* <span data-ttu-id="9650b-109">Azure 串流分析</span><span class="sxs-lookup"><span data-stu-id="9650b-109">Azure Stream Analytics</span></span>

<span data-ttu-id="9650b-110">我們正與更多服務 tooconnect 跨 hello Azure 生態系統。</span><span class="sxs-lookup"><span data-stu-id="9650b-110">We are working tooconnect with more services across hello Azure ecosystem.</span></span>

## <a name="power-bi"></a><span data-ttu-id="9650b-111">Power BI</span><span class="sxs-lookup"><span data-stu-id="9650b-111">Power BI</span></span>
<span data-ttu-id="9650b-112">Power BI 整合可讓您 tooleverage hello 選計算能力的 SQL 資料倉儲與 hello 動態報告和 Power BI 視覺效果。</span><span class="sxs-lookup"><span data-stu-id="9650b-112">Power BI integration allows you tooleverage hello compute power of SQL Data Warehouse with hello dynamic reporting and visualization of Power BI.</span></span> <span data-ttu-id="9650b-113">目前 Power BI 整合包括：</span><span class="sxs-lookup"><span data-stu-id="9650b-113">Power BI integration currently includes:</span></span>

* <span data-ttu-id="9650b-114">**直接連接**：針對 SQL 資料倉儲進行之邏輯下推的更進階連接。</span><span class="sxs-lookup"><span data-stu-id="9650b-114">**Direct Connect**: A more advanced connection with logical pushdown against SQL Data Warehouse.</span></span>  <span data-ttu-id="9650b-115">可提供更快速且更大規模的分析。</span><span class="sxs-lookup"><span data-stu-id="9650b-115">This provides faster analysis on a larger scale.</span></span>
* <span data-ttu-id="9650b-116">**在 Power BI 中開啟**: hello 'Power BI 中開啟' 按鈕傳遞執行個體資訊 tooPower BI，以便更順暢的連線。</span><span class="sxs-lookup"><span data-stu-id="9650b-116">**Open in Power BI**: hello 'Open in Power BI' button passes instance information tooPower BI, allowing for a more seamless connection.</span></span>

<span data-ttu-id="9650b-117">請參閱[與 Power BI 整合](sql-data-warehouse-integrate-power-bi.md)或 hello [Power BI 文件](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="9650b-117">See [Integrate with Power BI](sql-data-warehouse-integrate-power-bi.md) or hello [Power BI documentation](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) for more information.</span></span>

## <a name="azure-data-factory"></a><span data-ttu-id="9650b-118">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9650b-118">Azure Data Factory</span></span>
<span data-ttu-id="9650b-119">Azure Data Factory 可讓使用者的受管理的平台 toocreate 複雜擷取載入管線。</span><span class="sxs-lookup"><span data-stu-id="9650b-119">Azure Data Factory gives users a managed platform toocreate complex Extract-Load pipelines.</span></span>  <span data-ttu-id="9650b-120">與 Azure Data Factory 的 SQL 資料倉儲的整合包含 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="9650b-120">SQL Data Warehouse's integration with Azure Data Factory includes hello following:</span></span>

* <span data-ttu-id="9650b-121">**預存程序**： 協調 hello 執行 SQL 資料倉儲上的預存程序。</span><span class="sxs-lookup"><span data-stu-id="9650b-121">**Stored Procedures**: Orchestrate hello execution of stored procedures on SQL Data Warehouse.</span></span>
* <span data-ttu-id="9650b-122">**複製**： 使用 ADF toomove 資料到 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="9650b-122">**Copy**: Use ADF toomove data into SQL Data Warehouse.</span></span>  <span data-ttu-id="9650b-123">這項作業可以使用 ADF 的標準資料移動機制，或在 hello PolyBase 涵蓋。</span><span class="sxs-lookup"><span data-stu-id="9650b-123">This operation can use ADF's standard data movement mechanism or PolyBase under hello covers.</span></span> 

<span data-ttu-id="9650b-124">請參閱[與 Azure Data Factory 整合](sql-data-warehouse-integrate-azure-data-factory.md)或 hello [Azure Data Factory 文件](https://azure.microsoft.com/documentation/services/data-factory/)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="9650b-124">See [Integrate with Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) or hello [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/) for more information.</span></span>

## <a name="azure-machine-learning"></a><span data-ttu-id="9650b-125">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9650b-125">Azure Machine Learning</span></span>
<span data-ttu-id="9650b-126">Azure Machine Learning 是完全受管理的分析服務，可讓使用者利用大量預測工具 toocreate 複雜模型。</span><span class="sxs-lookup"><span data-stu-id="9650b-126">Azure Machine Learning is a fully managed analytics service which allows users toocreate intricate models leveraging a large set of predictive tools.</span></span>  <span data-ttu-id="9650b-127">SQL 資料倉儲做為來源和目的地，這些模型以支援下列功能的 hello:</span><span class="sxs-lookup"><span data-stu-id="9650b-127">SQL Data Warehouse is supported as both a source and destination for these models with hello following functionality:</span></span>

* <span data-ttu-id="9650b-128">**讀取資料：** 針對 SQL 資料倉儲透過 T-SQL 大規模驅動模型。</span><span class="sxs-lookup"><span data-stu-id="9650b-128">**Read Data:** Drive models at scale using T-SQL against SQL Data Warehouse.</span></span>
* <span data-ttu-id="9650b-129">**將資料寫入：**認可變更，從任何模型傳回 tooSQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="9650b-129">**Write Data:** Commit changes from any model back tooSQL Data Warehouse.</span></span>

<span data-ttu-id="9650b-130">請參閱[整合與 Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md)或 hello [Azure Machine Learning 文](https://azure.microsoft.com/services/machine-learning/)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="9650b-130">See [Integrate with Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) or hello [Azure Machine Learning documentation](https://azure.microsoft.com/services/machine-learning/) for more information.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="9650b-131">Azure 串流分析</span><span class="sxs-lookup"><span data-stu-id="9650b-131">Azure Stream Analytics</span></span>
<span data-ttu-id="9650b-132">Azure 串流分析是複雜、完全受管理的基礎結構，可處理和取用產生自 Azure 事件中樞的事件資料。</span><span class="sxs-lookup"><span data-stu-id="9650b-132">Azure Stream Analytics is a complex, fully managed infrastructure for processing and consuming event data generated from Azure Event Hub.</span></span>  <span data-ttu-id="9650b-133">SQL 資料倉儲與整合可讓資料流資料 toobe 有效地處理並啟用更深入的關聯式資料一起儲存，多個進階分析。</span><span class="sxs-lookup"><span data-stu-id="9650b-133">Integration with SQL Data Warehouse allows for streaming data toobe effectively processed and stored alongside relational data enabling deeper, more advanced analysis.</span></span>  

* <span data-ttu-id="9650b-134">**工作輸出：**傳送輸出資料流分析工作直接 tooSQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="9650b-134">**Job Output:** Send output from Stream Analytics jobs directly tooSQL Data Warehouse.</span></span>

<span data-ttu-id="9650b-135">請參閱[與 Azure Stream Analytics 整合](sql-data-warehouse-integrate-azure-stream-analytics.md)或 hello [Azure Stream Analytics 文件](https://azure.microsoft.com/documentation/services/stream-analytics/)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="9650b-135">See [Integrate with Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) or hello [Azure Stream Analytics documentation](https://azure.microsoft.com/documentation/services/stream-analytics/) for more information.</span></span>

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
