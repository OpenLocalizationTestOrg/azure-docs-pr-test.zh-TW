---
title: "aaaCreate 表格式模型使用 hello Azure Analysis Services Web 設計工具 |Microsoft 文件"
description: "了解如何 toocreate Azure Analysis Services 表格式模型使用 hello Azure 入口網站中的 Web 設計工具。"
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
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: a37b326b76c84fc3a4300827bc1c8706b0584701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-model-in-azure-portal"></a><span data-ttu-id="c0cdb-103">在 Azure 入口網站中建立模型</span><span class="sxs-lookup"><span data-stu-id="c0cdb-103">Create a model in Azure portal</span></span>

<span data-ttu-id="c0cdb-104">提供快速簡便方式 toocreate hello Azure Analysis Services web 設計工具 （預覽） 功能在 Azure 入口網站，並編輯表格式模型和查詢模型資料直接在您的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="c0cdb-104">hello Azure Analysis Services web designer (preview) feature in Azure portal provides a quick and easy way toocreate and edit tabular models and query model data right in your browser.</span></span> 

<span data-ttu-id="c0cdb-105">請記住，hello web 設計工具是**預覽**。</span><span class="sxs-lookup"><span data-stu-id="c0cdb-105">Keep in mind, hello web designer is **preview**.</span></span> <span data-ttu-id="c0cdb-106">正在加入新的功能在預覽中，所有 hello 時間時功能會受到限制。</span><span class="sxs-lookup"><span data-stu-id="c0cdb-106">While new functionality is being added all hello time, in preview, functionality is limited.</span></span> <span data-ttu-id="c0cdb-107">如需進階模型開發和測試，是最佳 toouse Visual Studio (SSDT) 和 SQL Server Management Studio (SSMS)。</span><span class="sxs-lookup"><span data-stu-id="c0cdb-107">For more advanced model development and testing, it's best toouse Visual Studio (SSDT) and SQL Server Management Studio (SSMS).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0cdb-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="c0cdb-108">Prerequisites</span></span>

- <span data-ttu-id="c0cdb-109">Azure Analysis Services 伺服器在 hello 標準或開發人員層。</span><span class="sxs-lookup"><span data-stu-id="c0cdb-109">An Azure Analysis Services server at hello Standard or Developer tier.</span></span> <span data-ttu-id="c0cdb-110">使用 hello Web 設計工具所建立的新模型是 DirectQuery，只有支援這些層。</span><span class="sxs-lookup"><span data-stu-id="c0cdb-110">New models created by using hello Web designer are DirectQuery, supported only by these tiers.</span></span>
- <span data-ttu-id="c0cdb-111">作為資料來源的 Azure SQL Database、Azure SQL 資料倉儲或 Power BI Desktop (.pbix) 檔案。</span><span class="sxs-lookup"><span data-stu-id="c0cdb-111">An Azure SQL Database, Azure SQL Data Warehouse, or Power BI Desktop (.pbix) file as a datasource.</span></span> <span data-ttu-id="c0cdb-112">從 Power BI Desktop 檔案建立的新模型支援 Azure SQL Database、Azure SQL 資料倉儲、Oracle 和 Teradata 資料來源。</span><span class="sxs-lookup"><span data-stu-id="c0cdb-112">New models created from Power BI Desktop files support Azure SQL Database, Azure SQL Data Warehouse, Oracle, and Teradata data sources.</span></span>
- <span data-ttu-id="c0cdb-113">SQL Server 帳戶和密碼來連接 tooAzure SQL Database 或 Azure SQL 資料倉儲資料來源。</span><span class="sxs-lookup"><span data-stu-id="c0cdb-113">A SQL Server account and password for connecting tooAzure SQL Database or Azure SQL Data Warehouse data sources.</span></span>

## <a name="toocreate-a-new-tabular-model"></a><span data-ttu-id="c0cdb-114">toocreate 新的表格式模型</span><span class="sxs-lookup"><span data-stu-id="c0cdb-114">toocreate a new tabular model</span></span>

1. <span data-ttu-id="c0cdb-115">在您的伺服器 [概觀] 刀鋒視窗 > [Web 設計工具] 中，按一下 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="c0cdb-115">In your server's **Overview** blade > **Web designer**, click **Open**.</span></span>

    ![在 Azure 入口網站中建立模型](./media/analysis-services-create-model-portal/aas-create-portal-overview-wd.png)

2. <span data-ttu-id="c0cdb-117">在 [Web 設計工具]  >  [模型] 中，按一下 [+ 新增]。</span><span class="sxs-lookup"><span data-stu-id="c0cdb-117">In **Web designer** > **Models**, click **+ Add**.</span></span>

    ![在 Azure 入口網站中建立模型](./media/analysis-services-create-model-portal/aas-create-portal-models.png)

3. <span data-ttu-id="c0cdb-119">在 [新增模型] 中輸入模型名稱，然後選取資料來源。</span><span class="sxs-lookup"><span data-stu-id="c0cdb-119">In **New model**, type a model name, and then select a data source.</span></span>

    ![在 Azure 入口網站中的新增模型對話方塊](./media/analysis-services-create-model-portal/aas-create-portal-new-model.png)

4. <span data-ttu-id="c0cdb-121">在**連接**，輸入 hello 連接屬性。</span><span class="sxs-lookup"><span data-stu-id="c0cdb-121">In **Connect**, enter hello connection properties.</span></span> <span data-ttu-id="c0cdb-122">使用者名稱和密碼必須是 SQL Server 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c0cdb-122">Username and password must be a SQL Server account.</span></span>

     ![在 Azure 入口網站中的連線對話方塊](./media/analysis-services-create-model-portal/aas-create-portal-connect.png)

5. <span data-ttu-id="c0cdb-124">在**資料表和檢視表**hello 資料表 tooinclude 選取在模型中，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="c0cdb-124">In **Tables and views**, select hello tables tooinclude in your model, and then click **Create**.</span></span> <span data-ttu-id="c0cdb-125">會使用金鑰組自動建立資料表之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="c0cdb-125">Relationships are created automatically between tables with a key pair.</span></span>

     ![選取資料表和檢視](./media/analysis-services-create-model-portal/aas-create-portal-tables.png)

<span data-ttu-id="c0cdb-127">新的模型會出現在您的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="c0cdb-127">Your new model appears in your browser.</span></span> <span data-ttu-id="c0cdb-128">您可以在這裡執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="c0cdb-128">From here, you can:</span></span>   

- <span data-ttu-id="c0cdb-129">拖曳欄位 toohello 查詢設計工具，以及加入篩選來查詢模型資料。</span><span class="sxs-lookup"><span data-stu-id="c0cdb-129">Query model data by dragging fields toohello query designer and adding filters.</span></span>
- <span data-ttu-id="c0cdb-130">在資料表中建立新的量值。</span><span class="sxs-lookup"><span data-stu-id="c0cdb-130">Create new measures in tables.</span></span>
- <span data-ttu-id="c0cdb-131">使用 hello json 編輯器來編輯模型中繼資料。</span><span class="sxs-lookup"><span data-stu-id="c0cdb-131">Edit model metadata by using hello json editor.</span></span>
- <span data-ttu-id="c0cdb-132">在 Visual Studio (SSDT) 中，Power BI Desktop 或 Excel 中開啟 hello 模型。</span><span class="sxs-lookup"><span data-stu-id="c0cdb-132">Open hello model in Visual Studio (SSDT), Power BI Desktop, or Excel.</span></span>

![選取資料表和檢視](./media/analysis-services-create-model-portal/aas-create-portal-query.png)

> [!NOTE]
> <span data-ttu-id="c0cdb-134">當您編輯模型中繼資料，或在您的瀏覽器中建立新的量值時，您要在 Azure 中儲存這些變更 tooyour 模型。</span><span class="sxs-lookup"><span data-stu-id="c0cdb-134">When you edit model metadata or create new measures in your browser, you're saving those changes tooyour model in Azure.</span></span> <span data-ttu-id="c0cdb-135">如果您正在 SSDT、Power BI Desktop 或 Excel 中使用模型，您的模型可以不同步。</span><span class="sxs-lookup"><span data-stu-id="c0cdb-135">If you're also working on your model in SSDT, Power BI Desktop, or Excel, your model can get out of sync.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c0cdb-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c0cdb-136">Next steps</span></span> 
[<span data-ttu-id="c0cdb-137">管理資料庫角色和使用者</span><span class="sxs-lookup"><span data-stu-id="c0cdb-137">Manage database roles and users</span></span>](analysis-services-database-users.md)  
[<span data-ttu-id="c0cdb-138">與 Excel 連線</span><span class="sxs-lookup"><span data-stu-id="c0cdb-138">Connect with Excel</span></span>](analysis-services-connect-excel.md)  


