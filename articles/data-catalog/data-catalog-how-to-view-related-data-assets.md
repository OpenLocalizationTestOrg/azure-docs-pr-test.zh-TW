---
title: "aaaHow tooview 相關 Azure 資料目錄中的資料資產 |Microsoft 文件"
description: "本文說明如何 tooview 相關資料的 Azure 資料目錄中選取的資料資產的資產。"
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: b69686737070ac563a0318f48e693215c605f90b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooview-related-data-assets-in-azure-data-catalog"></a><span data-ttu-id="d63e0-103">Tooview 關聯在 Azure 資料目錄中的資料資產的方式？</span><span class="sxs-lookup"><span data-stu-id="d63e0-103">How tooview related data assets in Azure Data Catalog?</span></span>
<span data-ttu-id="d63e0-104">Azure 資料目錄可讓您 tooview 資料資產相關的 tooa 選取資料資產和檢視之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="d63e0-104">Azure Data Catalog allows you tooview data assets related tooa selected data asset and view relationships between them.</span></span> 

## <a name="supported-data-sources"></a><span data-ttu-id="d63e0-105">支援的資料來源</span><span class="sxs-lookup"><span data-stu-id="d63e0-105">Supported data sources</span></span> 
<span data-ttu-id="d63e0-106">當您註冊從 hello 下列資料來源的資料資產時，Azure 資料目錄將會自動註冊選取的 hello 資料資產之間的聯結關聯性的相關中繼資料。</span><span class="sxs-lookup"><span data-stu-id="d63e0-106">When you register data assets from hello following data sources, Azure Data Catalog automatically registers metadata about join relationships between hello selected data assets.</span></span> 

- <span data-ttu-id="d63e0-107">SQL Server</span><span class="sxs-lookup"><span data-stu-id="d63e0-107">SQL Server</span></span>
- <span data-ttu-id="d63e0-108">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="d63e0-108">Azure SQL Database</span></span>
- <span data-ttu-id="d63e0-109">MySQL</span><span class="sxs-lookup"><span data-stu-id="d63e0-109">MySQL</span></span>
- <span data-ttu-id="d63e0-110">Oracle</span><span class="sxs-lookup"><span data-stu-id="d63e0-110">Oracle</span></span>

## <a name="view-related-data-assets"></a><span data-ttu-id="d63e0-111">檢視相關的資料資產</span><span class="sxs-lookup"><span data-stu-id="d63e0-111">View related data assets</span></span>
<span data-ttu-id="d63e0-112">tooview 資料資產的相關的 tooa 選取資料集，使用 hello**關聯性**索引標籤中 hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="d63e0-112">tooview data assets that are related tooa selected dataset, use hello **Relationships** tab as shown in hello following image:</span></span> 

![Azure 資料目錄 - 檢視相關的資料資產](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

<span data-ttu-id="d63e0-114">在此範例中，有兩個關聯性選取的 hello **ProductSubcategory**資料資產：</span><span class="sxs-lookup"><span data-stu-id="d63e0-114">In this example, there are two relationships for hello selected **ProductSubcategory** data asset:</span></span> 

- <span data-ttu-id="d63e0-115">ProductSubcategoryID hello 產品資料表資料行有 ProductSubcategoryID hello 選取 ProductSubcategory 資料表資料行的外部索引鍵關聯性。</span><span class="sxs-lookup"><span data-stu-id="d63e0-115">ProductSubcategoryID column of hello Product table has a foreign key relationship with ProductSubcategoryID column of hello selected ProductSubcategory table.</span></span> 
- <span data-ttu-id="d63e0-116">Production.productcategory hello ProductSubCategory 資料表資料行有 Production.productcategory hello 選取 ProductCategory 資料表資料行的外部索引鍵關聯性。</span><span class="sxs-lookup"><span data-stu-id="d63e0-116">ProductCategoryID column of hello ProductSubCategory table has a foreign key relationship with ProductCategoryID column of hello selected ProductCategory table.</span></span>

> [!NOTE]
> <span data-ttu-id="d63e0-117">請注意 hello hello 關聯性樹狀結構檢視中的 hello 箭頭方向。</span><span class="sxs-lookup"><span data-stu-id="d63e0-117">Notice hello direction of hello arrow in hello relationships tree view.</span></span>  

<span data-ttu-id="d63e0-118">toosee 更多詳細資料，例如 hello 完整 hello 資料行名稱移 hello 滑鼠，而且您看見快顯視窗類似 toohello，下列影像：</span><span class="sxs-lookup"><span data-stu-id="d63e0-118">toosee more details such as hello fully qualified name of hello column, move hello mouse over and you see a popup similar toohello following image:</span></span> 

![Azure 資料目錄 - 關聯性快顯訊息](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

<span data-ttu-id="d63e0-120">tooinclude 已註冊的資產之間的關聯性重新註冊這些資產。</span><span class="sxs-lookup"><span data-stu-id="d63e0-120">tooinclude relationships between assets that have already been registered, re-register those assets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d63e0-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d63e0-121">Next steps</span></span>
- [<span data-ttu-id="d63e0-122">如何 toomanage 資料資產</span><span class="sxs-lookup"><span data-stu-id="d63e0-122">How toomanage data assets</span></span>](data-catalog-how-to-manage.md)
