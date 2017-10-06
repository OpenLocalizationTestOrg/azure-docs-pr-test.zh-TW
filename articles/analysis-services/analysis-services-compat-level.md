---
title: "Azure Analysis Services 中的 aaaData 模型相容性層級 |Microsoft 文件"
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
ms.openlocfilehash: bfaf0c60666729d1e6e0baf082c046ea9faa4e86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a><span data-ttu-id="5288c-103">Analysis Services 表格式模型的相容性層級</span><span class="sxs-lookup"><span data-stu-id="5288c-103">Compatibility level for Analysis Services tabular models</span></span>

<span data-ttu-id="5288c-104">*相容性層級*是指在 hello Analysis Services 引擎 toorelease 特定行為。</span><span class="sxs-lookup"><span data-stu-id="5288c-104">*Compatibility level* refers toorelease-specific behaviors in hello Analysis Services engine.</span></span> <span data-ttu-id="5288c-105">與 SQL server 的主要版本通常一致變更 toohello 相容性層級。</span><span class="sxs-lookup"><span data-stu-id="5288c-105">Changes toohello compatibility level typically coincide with major releases of SQL Server.</span></span> <span data-ttu-id="5288c-106">這些變更也會實作兩個平台之間的 Azure Analysis Services toomaintain 同位檢查。</span><span class="sxs-lookup"><span data-stu-id="5288c-106">These changes are also implemented in Azure Analysis Services toomaintain parity between both platforms.</span></span> <span data-ttu-id="5288c-107">相容性層級變更也會影響您的表格式模型中的可用功能。</span><span class="sxs-lookup"><span data-stu-id="5288c-107">Compatibility level changes also affect features available in your tabular models.</span></span> <span data-ttu-id="5288c-108">例如，DirectQuery 和表格式物件中繼資料，請在根據 hello 相容性層級有不同的實作。</span><span class="sxs-lookup"><span data-stu-id="5288c-108">For example, DirectQuery and tabular object metadata have different implementations depending on hello compatibility level.</span></span> 

<span data-ttu-id="5288c-109">Azure Analysis Services 支援 hello 1200 和 1400年相容性層級的表格式模型。</span><span class="sxs-lookup"><span data-stu-id="5288c-109">Azure Analysis Services supports tabular models at hello 1200 and 1400 compatibility levels.</span></span>

<span data-ttu-id="5288c-110">hello 最新相容性層級是 1400年。</span><span class="sxs-lookup"><span data-stu-id="5288c-110">hello latest compatibility level is 1400.</span></span> <span data-ttu-id="5288c-111">此層級與 SQL Server 2017 Analysis Services 一致。</span><span class="sxs-lookup"><span data-stu-id="5288c-111">This level coincides with SQL Server 2017 Analysis Services.</span></span> <span data-ttu-id="5288c-112">Hello 1400 相容性層級中的主要功能包括：</span><span class="sxs-lookup"><span data-stu-id="5288c-112">Major features in hello 1400 compatibility level include:</span></span>

*  <span data-ttu-id="5288c-113">資料連線的新基礎結構，以及匯入表格式模型，且支援 TOM API 和 TMSL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="5288c-113">New infrastructure for data connectivity and import into tabular models with support for TOM APIs and TMSL scripting.</span></span> <span data-ttu-id="5288c-114">這項新功能可支援其他資料來源，例如 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="5288c-114">This new feature enables support for additional data sources such as Azure Blob storage.</span></span>
*  <span data-ttu-id="5288c-115">使用 Get Data 與 M 運算式的資料轉換和資料混搭功能。</span><span class="sxs-lookup"><span data-stu-id="5288c-115">Data transformation and data mashup capabilities by using Get Data and M expressions.</span></span>
*  <span data-ttu-id="5288c-116">量值支援使用 DAX 運算式的詳細資料列屬性。</span><span class="sxs-lookup"><span data-stu-id="5288c-116">Measures support a Detail Rows property with a DAX expression.</span></span> <span data-ttu-id="5288c-117">此屬性可讓用戶端工具，像是 Microsoft Excel toodrill 向 toodetailed 資料，從彙總的報表。</span><span class="sxs-lookup"><span data-stu-id="5288c-117">This property enables client tools like Microsoft Excel toodrill down toodetailed data from an aggregated report.</span></span> <span data-ttu-id="5288c-118">例如，當使用者檢視區域和月份的總銷售額，則可以檢視相關聯的 hello 訂單詳細資料。</span><span class="sxs-lookup"><span data-stu-id="5288c-118">For example, when users view total sales for a region and month, they can view hello associated order details.</span></span> 
*  <span data-ttu-id="5288c-119">物件層級安全性的資料表和資料行名稱，此外 toohello 中的資料。</span><span class="sxs-lookup"><span data-stu-id="5288c-119">Object-level security for table and column names, in addition toohello data within them.</span></span>
*  <span data-ttu-id="5288c-120">不完全階層的增強支援。</span><span class="sxs-lookup"><span data-stu-id="5288c-120">Enhanced support for ragged hierarchies.</span></span>
*  <span data-ttu-id="5288c-121">效能和監控改善。</span><span class="sxs-lookup"><span data-stu-id="5288c-121">Performance and monitoring improvements.</span></span>
  
## <a name="set-compatibility-level"></a><span data-ttu-id="5288c-122">設定相容性層級</span><span class="sxs-lookup"><span data-stu-id="5288c-122">Set compatibility level</span></span> 
 <span data-ttu-id="5288c-123">當在 SSDT 中建立新的表格式模型專案，您可以指定 hello 相容性層級上 hello**表格式模型設計師**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5288c-123">When creating a new tabular model project in SSDT, you can specify hello compatibility level on hello **Tabular model designer** dialog.</span></span> 
  
 ![ssas_tabularproject_compat1200](./media/analysis-services-compat-level/aas-tabularproject-compat.png)  
  
 <span data-ttu-id="5288c-125">如果您選取 hello**不要再顯示此訊息**選項時，所有後續專案都使用您指定為 hello 預設 hello 相容性層級。</span><span class="sxs-lookup"><span data-stu-id="5288c-125">If you select hello **Do not show this message again** option, all subsequent projects use hello compatibility level you specified as hello default.</span></span> <span data-ttu-id="5288c-126">您可以變更在 SSDT 中的 hello 預設相容性層級**工具** > **選項**。</span><span class="sxs-lookup"><span data-stu-id="5288c-126">You can change hello default compatibility level in SSDT in **Tools** > **Options**.</span></span>  
  
 <span data-ttu-id="5288c-127">將現有的表格式模型專案，在 SSDT 中，設定 hello tooupgrade**相容性層級**hello 模型中的屬性**屬性**視窗。</span><span class="sxs-lookup"><span data-stu-id="5288c-127">tooupgrade an existing tabular model project in SSDT, set  hello **Compatibility Level** property in hello model **Properties** window.</span></span> <span data-ttu-id="5288c-128">請記住，升級 hello 相容性層級是無法復原。</span><span class="sxs-lookup"><span data-stu-id="5288c-128">Keep in-mind, upgrading hello compatibility level is irreversible.</span></span>
  
## <a name="check-compatibility-level-for-a-tabular-model-database-in-sql-server-management-studio"></a><span data-ttu-id="5288c-129">檢查 SQL Server Management Studio 中表格式模型資料庫的相容性層級</span><span class="sxs-lookup"><span data-stu-id="5288c-129">Check compatibility level for a tabular model database in SQL Server Management Studio</span></span> 
 <span data-ttu-id="5288c-130">在 SSMS 中，以滑鼠右鍵按一下 hello 資料庫名稱 >**屬性** > **相容性層級**。</span><span class="sxs-lookup"><span data-stu-id="5288c-130">In SSMS, right-click hello database name > **Properties** > **Compatibility Level**.</span></span>  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a><span data-ttu-id="5288c-131">檢查 SSMS 中的伺服器支援的相容性層級</span><span class="sxs-lookup"><span data-stu-id="5288c-131">Check supported compatibility level for a server in SSMS</span></span>  
 <span data-ttu-id="5288c-132">在 SSMS 中，以滑鼠右鍵按一下 hello 伺服器名稱 >**屬性** > **支援的相容性層級**。</span><span class="sxs-lookup"><span data-stu-id="5288c-132">In SSMS, right-click hello server name>  **Properties** > **Supported Compatibility Level**.</span></span>  
  
 <span data-ttu-id="5288c-133">此屬性指定 hello 最高相容性層級將在 hello （不含預覽） 的伺服器執行的資料庫。</span><span class="sxs-lookup"><span data-stu-id="5288c-133">This property specifies hello highest compatibility level of a database that will run on hello server (excluding preview).</span></span> <span data-ttu-id="5288c-134">無法變更 hello 支援相容性層級。</span><span class="sxs-lookup"><span data-stu-id="5288c-134">hello supported compatibility level cannot be changed.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="5288c-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5288c-135">Next steps</span></span>
  <span data-ttu-id="5288c-136">[在 Azure 入口網站中建立模型](analysis-services-create-model-portal.md) </span><span class="sxs-lookup"><span data-stu-id="5288c-136">[Create a model in Azure portal](analysis-services-create-model-portal.md) </span></span>  
  [<span data-ttu-id="5288c-137"> Analysis Services</span><span class="sxs-lookup"><span data-stu-id="5288c-137">Manage Analysis Services</span></span>](analysis-services-manage.md)  
