---
title: "aaa\"Azure Analysis Services 教學課程第 8 課建立的檢視方塊 |Microsoft 文件 」"
description: "描述如何 toocreate 中的檢視方塊 hello Azure Analysis Services 教學課程專案。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: 25391813e1969ecb22af4d6f9c1ccd8358d812fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="lesson-8-create-perspectives"></a><span data-ttu-id="e68db-103">第 8 課：建立檢視方塊</span><span class="sxs-lookup"><span data-stu-id="e68db-103">Lesson 8: Create perspectives</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="e68db-104">在這堂課中，您可以建立「網際網路銷售」檢視方塊。</span><span class="sxs-lookup"><span data-stu-id="e68db-104">In this lesson, you create an Internet Sales perspective.</span></span> <span data-ttu-id="e68db-105">檢視方塊會定義可檢視的模型子集，以提供聚焦、商務特有或應用程式特有的觀點。</span><span class="sxs-lookup"><span data-stu-id="e68db-105">A perspective defines a viewable subset of a model that provides focused, business-specific, or application-specific viewpoints.</span></span> <span data-ttu-id="e68db-106">當使用者使用檢視方塊 tooa 模型，它們只會看到這些模型物件 （資料表、 資料行、 量值、 階層和 Kpi） 做為該檢視方塊中所定義的欄位。</span><span class="sxs-lookup"><span data-stu-id="e68db-106">When a user connects tooa model by using a perspective, they see only those model objects (tables, columns, measures, hierarchies, and KPIs) as fields defined in that perspective.</span></span> <span data-ttu-id="e68db-107">詳細資訊，請參閱 toolearn[檢視方塊](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular)。</span><span class="sxs-lookup"><span data-stu-id="e68db-107">toolearn more, see [Perspectives](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span></span>
  
<span data-ttu-id="e68db-108">hello 您在這一課中建立的網際網路銷售檢視方塊排除 hello DimCustomer 資料表物件。</span><span class="sxs-lookup"><span data-stu-id="e68db-108">hello Internet Sales perspective you create in this lesson excludes hello DimCustomer table object.</span></span> <span data-ttu-id="e68db-109">當您建立從檢視中排除特定物件的檢視方塊時，該物件仍然存在 hello 模型中。</span><span class="sxs-lookup"><span data-stu-id="e68db-109">When you create a perspective that excludes certain objects from view, that object still exists in hello model.</span></span> <span data-ttu-id="e68db-110">不過，不會顯示在報告用戶端欄位清單中。</span><span class="sxs-lookup"><span data-stu-id="e68db-110">However, it is not visible in a reporting client field list.</span></span> <span data-ttu-id="e68db-111">計算結果欄和量值不管是否包含在檢視方塊中，仍然可以從排除的物件資料計算。</span><span class="sxs-lookup"><span data-stu-id="e68db-111">Calculated columns and measures either included in a perspective or not can still calculate from object data that is excluded.</span></span>  
  
<span data-ttu-id="e68db-112">hello 本課程的目的是 toodescribe 如何 toocreate 檢視方塊並熟悉 hello 表格式模型撰寫工具。</span><span class="sxs-lookup"><span data-stu-id="e68db-112">hello purpose of this lesson is toodescribe how toocreate perspectives and become familiar with hello tabular model authoring tools.</span></span> <span data-ttu-id="e68db-113">如果您之後展開此模型 tooinclude 其他資料表，您可以建立其他檢視方塊 toodefine 不同觀點的 hello 模型，例如存貨和銷售。</span><span class="sxs-lookup"><span data-stu-id="e68db-113">If you later expand this model tooinclude additional tables, you can create additional perspectives toodefine different viewpoints of hello model, for example, Inventory and Sales.</span></span>  
  
<span data-ttu-id="e68db-114">本課程的估計時間 toocomplete:**五分鐘**</span><span class="sxs-lookup"><span data-stu-id="e68db-114">Estimated time toocomplete this lesson: **Five minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="e68db-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="e68db-115">Prerequisites</span></span>  
<span data-ttu-id="e68db-116">本主題是表格式模型教學課程的一部分，請依序完成。</span><span class="sxs-lookup"><span data-stu-id="e68db-116">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="e68db-117">在執行之前 hello 工作在這一課，您應已完成上一課 hello:[第 7 課： 建立關鍵效能指標](../tutorials/aas-lesson-7-create-key-performance-indicators.md)。</span><span class="sxs-lookup"><span data-stu-id="e68db-117">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  
  
## <a name="create-perspectives"></a><span data-ttu-id="e68db-118">建立檢視方塊</span><span class="sxs-lookup"><span data-stu-id="e68db-118">Create perspectives</span></span>  
  
#### <a name="toocreate-an-internet-sales-perspective"></a><span data-ttu-id="e68db-119">toocreate 網際網路銷售檢視方塊</span><span class="sxs-lookup"><span data-stu-id="e68db-119">toocreate an Internet Sales perspective</span></span>  
  
1.  <span data-ttu-id="e68db-120">按一下 hello**模型**功能表 >**檢視方塊** > **建立和管理**。</span><span class="sxs-lookup"><span data-stu-id="e68db-120">Click hello **Model** menu > **Perspectives** > **Create and Manage**.</span></span>  
  
2.  <span data-ttu-id="e68db-121">在 hello**檢視方塊**對話方塊中，按一下 **新檢視方塊**。</span><span class="sxs-lookup"><span data-stu-id="e68db-121">In hello **Perspectives** dialog box, click **New Perspective**.</span></span>  
  
3.  <span data-ttu-id="e68db-122">按兩下 hello**新檢視方塊**欄標題，並將其重新命名**Internet Sales**。</span><span class="sxs-lookup"><span data-stu-id="e68db-122">Double-click hello **New Perspective** column heading, and then rename **Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="e68db-123">選取 hello 所有都 hello 資料表*除了* **DimCustomer**。</span><span class="sxs-lookup"><span data-stu-id="e68db-123">Select hello all hello tables *except* **DimCustomer**.</span></span>  
  
    ![aas-lesson8-perspectives](../tutorials/media/aas-lesson8-perspectives.png)
  
    <span data-ttu-id="e68db-125">在後面的課程，您使用在 Excel 功能 tootest hello 分析此檢視方塊。</span><span class="sxs-lookup"><span data-stu-id="e68db-125">In a later lesson, you use hello Analyze in Excel feature tootest this perspective.</span></span> <span data-ttu-id="e68db-126">hello Excel 樞紐分析表欄位清單包含每個資料表除了 hello DimCustomer 資料表。</span><span class="sxs-lookup"><span data-stu-id="e68db-126">hello Excel PivotTable Fields List includes each table except hello DimCustomer table.</span></span>  

## <a name="whats-next"></a><span data-ttu-id="e68db-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e68db-127">What's next?</span></span>
<span data-ttu-id="e68db-128">[第 9 課：建立階層](../tutorials/aas-lesson-9-create-hierarchies.md)。</span><span class="sxs-lookup"><span data-stu-id="e68db-128">[Lesson 9: Create hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>
  
  
  
  
