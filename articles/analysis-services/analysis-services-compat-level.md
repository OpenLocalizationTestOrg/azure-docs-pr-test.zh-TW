---
title: "Azure Analysis Services 中的資料模型相容性層級 | Microsoft Docs"
description: "了解表格式資料模型的相容性層級。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/16/2017
ms.author: owend
ms.openlocfilehash: b11ba54c2cdc2675ec535368e7076613a5290212
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a><span data-ttu-id="b39ad-103">Analysis Services 表格式模型的相容性層級</span><span class="sxs-lookup"><span data-stu-id="b39ad-103">Compatibility level for Analysis Services tabular models</span></span>

<span data-ttu-id="b39ad-104">*相容性層級*是指 Analysis Services 引擎中特定版本的表現方式。</span><span class="sxs-lookup"><span data-stu-id="b39ad-104">*Compatibility level* refers to release-specific behaviors in the Analysis Services engine.</span></span> <span data-ttu-id="b39ad-105">相容性層級的變更通常與 SQL Server 的主要版本相符。</span><span class="sxs-lookup"><span data-stu-id="b39ad-105">Changes to the compatibility level typically coincide with major releases of SQL Server.</span></span> <span data-ttu-id="b39ad-106">這些變更也會在 Azure Analysis Services 中實作，以維護兩個平台之間的同位。</span><span class="sxs-lookup"><span data-stu-id="b39ad-106">These changes are also implemented in Azure Analysis Services to maintain parity between both platforms.</span></span> <span data-ttu-id="b39ad-107">相容性層級變更也會影響您的表格式模型中的可用功能。</span><span class="sxs-lookup"><span data-stu-id="b39ad-107">Compatibility level changes also affect features available in your tabular models.</span></span> <span data-ttu-id="b39ad-108">例如，DirectQuery 和表格式物件中繼資料根據相容性層級而有不同的實作方式。</span><span class="sxs-lookup"><span data-stu-id="b39ad-108">For example, DirectQuery and tabular object metadata have different implementations depending on the compatibility level.</span></span> 

<span data-ttu-id="b39ad-109">Azure Analysis Services 支援 1200 和 1400 相容性層級的表格式模型。</span><span class="sxs-lookup"><span data-stu-id="b39ad-109">Azure Analysis Services supports tabular models at the 1200 and 1400 compatibility levels.</span></span>

<span data-ttu-id="b39ad-110">最新的相容性層級是 1400。</span><span class="sxs-lookup"><span data-stu-id="b39ad-110">The latest compatibility level is 1400.</span></span> <span data-ttu-id="b39ad-111">此層級與 SQL Server 2017 Analysis Services 一致。</span><span class="sxs-lookup"><span data-stu-id="b39ad-111">This level coincides with SQL Server 2017 Analysis Services.</span></span> <span data-ttu-id="b39ad-112">1400 相容性層級中的主要功能包括：</span><span class="sxs-lookup"><span data-stu-id="b39ad-112">Major features in the 1400 compatibility level include:</span></span>

*  <span data-ttu-id="b39ad-113">資料連線的新基礎結構，以及匯入表格式模型，且支援 TOM API 和 TMSL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="b39ad-113">New infrastructure for data connectivity and import into tabular models with support for TOM APIs and TMSL scripting.</span></span> <span data-ttu-id="b39ad-114">這項新功能可支援其他資料來源，例如 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="b39ad-114">This new feature enables support for additional data sources such as Azure Blob storage.</span></span>
*  <span data-ttu-id="b39ad-115">使用 Get Data 與 M 運算式的資料轉換和資料混搭功能。</span><span class="sxs-lookup"><span data-stu-id="b39ad-115">Data transformation and data mashup capabilities by using Get Data and M expressions.</span></span>
*  <span data-ttu-id="b39ad-116">量值支援使用 DAX 運算式的詳細資料列屬性。</span><span class="sxs-lookup"><span data-stu-id="b39ad-116">Measures support a Detail Rows property with a DAX expression.</span></span> <span data-ttu-id="b39ad-117">此屬性可讓用戶端工具 (例如 Microsoft Excel) 從彙總的報表向下鑽研到詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b39ad-117">This property enables client tools like Microsoft Excel to drill down to detailed data from an aggregated report.</span></span> <span data-ttu-id="b39ad-118">例如，當使用者依區域和月份檢視總銷售額，他們可以檢視相關的訂單詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b39ad-118">For example, when users view total sales for a region and month, they can view the associated order details.</span></span> 
*  <span data-ttu-id="b39ad-119">除了資料表和資料行名稱中的資料以外，還有其物件層級安全性。</span><span class="sxs-lookup"><span data-stu-id="b39ad-119">Object-level security for table and column names, in addition to the data within them.</span></span>
*  <span data-ttu-id="b39ad-120">不完全階層的增強支援。</span><span class="sxs-lookup"><span data-stu-id="b39ad-120">Enhanced support for ragged hierarchies.</span></span>
*  <span data-ttu-id="b39ad-121">效能和監控改善。</span><span class="sxs-lookup"><span data-stu-id="b39ad-121">Performance and monitoring improvements.</span></span>
  
## <a name="set-compatibility-level"></a><span data-ttu-id="b39ad-122">設定相容性層級</span><span class="sxs-lookup"><span data-stu-id="b39ad-122">Set compatibility level</span></span> 
 <span data-ttu-id="b39ad-123">在 SSDT 中建立新的表格式模型專案時，您可以在 [表格式模型設計工具] 對話方塊中指定相容性層級。</span><span class="sxs-lookup"><span data-stu-id="b39ad-123">When creating a new tabular model project in SSDT, you can specify the compatibility level on the **Tabular model designer** dialog.</span></span> 
  
 ![ssas_tabularproject_compat1200](./media/analysis-services-compat-level/aas-tabularproject-compat.png)  
  
 <span data-ttu-id="b39ad-125">如果您選取 [不要再顯示這則訊息] 選項，所有後續專案會使用您指定的相容性層級做為預設。</span><span class="sxs-lookup"><span data-stu-id="b39ad-125">If you select the **Do not show this message again** option, all subsequent projects use the compatibility level you specified as the default.</span></span> <span data-ttu-id="b39ad-126">您可以在 SSDT 中，利用 [工具] > [選項] 變更預設相容性層級。</span><span class="sxs-lookup"><span data-stu-id="b39ad-126">You can change the default compatibility level in SSDT in **Tools** > **Options**.</span></span>  
  
 <span data-ttu-id="b39ad-127">若要升級 SSDT 中現有的表格式模型專案，請在模型 [屬性] 視窗中，設定 [相容性層級] 屬性。</span><span class="sxs-lookup"><span data-stu-id="b39ad-127">To upgrade an existing tabular model project in SSDT, set  the **Compatibility Level** property in the model **Properties** window.</span></span> <span data-ttu-id="b39ad-128">請記住，升級相容性層級無法復原。</span><span class="sxs-lookup"><span data-stu-id="b39ad-128">Keep in-mind, upgrading the compatibility level is irreversible.</span></span>
  
## <a name="check-compatibility-level-for-a-tabular-model-database-in-sql-server-management-studio"></a><span data-ttu-id="b39ad-129">檢查 SQL Server Management Studio 中表格式模型資料庫的相容性層級</span><span class="sxs-lookup"><span data-stu-id="b39ad-129">Check compatibility level for a tabular model database in SQL Server Management Studio</span></span> 
 <span data-ttu-id="b39ad-130">在 SSMS 中，以滑鼠右鍵按一下資料庫名稱 > [屬性] > [相容性層級]。</span><span class="sxs-lookup"><span data-stu-id="b39ad-130">In SSMS, right-click the database name > **Properties** > **Compatibility Level**.</span></span>  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a><span data-ttu-id="b39ad-131">檢查 SSMS 中的伺服器支援的相容性層級</span><span class="sxs-lookup"><span data-stu-id="b39ad-131">Check supported compatibility level for a server in SSMS</span></span>  
 <span data-ttu-id="b39ad-132">在 SSMS 中，以滑鼠右鍵按一下伺服器名稱 > [屬性] > [支援的相容性層級]。</span><span class="sxs-lookup"><span data-stu-id="b39ad-132">In SSMS, right-click the server name>  **Properties** > **Supported Compatibility Level**.</span></span>  
  
 <span data-ttu-id="b39ad-133">此屬性會指定將在伺服器上執行之資料庫的最高相容性層級 (不包含預覽)。</span><span class="sxs-lookup"><span data-stu-id="b39ad-133">This property specifies the highest compatibility level of a database that will run on the server (excluding preview).</span></span> <span data-ttu-id="b39ad-134">支援的相容性層級不能變更。</span><span class="sxs-lookup"><span data-stu-id="b39ad-134">The supported compatibility level cannot be changed.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="b39ad-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b39ad-135">Next steps</span></span>
  <span data-ttu-id="b39ad-136">[在 Azure 入口網站中建立模型](analysis-services-create-model-portal.md) </span><span class="sxs-lookup"><span data-stu-id="b39ad-136">[Create a model in Azure portal](analysis-services-create-model-portal.md) </span></span>  
  [<span data-ttu-id="b39ad-137"> Analysis Services</span><span class="sxs-lookup"><span data-stu-id="b39ad-137">Manage Analysis Services</span></span>](analysis-services-manage.md)  
