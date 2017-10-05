---
title: "如何檢視 Azure 資料目錄中的相關資料資產 | Microsoft Docs"
description: "本文說明如何檢視「Azure 資料目錄」中所選資料資產的相關資料資產。"
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
ms.openlocfilehash: d45f2cabe712a7982f99a9d280fed4494fc4d377
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-view-related-data-assets-in-azure-data-catalog"></a><span data-ttu-id="60d1e-103">如何檢視 Azure 資料目錄中的相關資料資產？</span><span class="sxs-lookup"><span data-stu-id="60d1e-103">How to view related data assets in Azure Data Catalog?</span></span>
<span data-ttu-id="60d1e-104">「Azure 資料目錄」可讓您檢視與所選資料資產相關的資料資產，並檢視它們之間的關係。</span><span class="sxs-lookup"><span data-stu-id="60d1e-104">Azure Data Catalog allows you to view data assets related to a selected data asset and view relationships between them.</span></span> 

## <a name="supported-data-sources"></a><span data-ttu-id="60d1e-105">支援的資料來源</span><span class="sxs-lookup"><span data-stu-id="60d1e-105">Supported data sources</span></span> 
<span data-ttu-id="60d1e-106">當您從下列資料來源註冊資料資產時，「Azure 資料目錄」會自動註冊與所選資料資產之間聯結關聯性相關的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="60d1e-106">When you register data assets from the following data sources, Azure Data Catalog automatically registers metadata about join relationships between the selected data assets.</span></span> 

- <span data-ttu-id="60d1e-107">SQL Server</span><span class="sxs-lookup"><span data-stu-id="60d1e-107">SQL Server</span></span>
- <span data-ttu-id="60d1e-108">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="60d1e-108">Azure SQL Database</span></span>
- <span data-ttu-id="60d1e-109">MySQL</span><span class="sxs-lookup"><span data-stu-id="60d1e-109">MySQL</span></span>
- <span data-ttu-id="60d1e-110">Oracle</span><span class="sxs-lookup"><span data-stu-id="60d1e-110">Oracle</span></span>

## <a name="view-related-data-assets"></a><span data-ttu-id="60d1e-111">檢視相關的資料資產</span><span class="sxs-lookup"><span data-stu-id="60d1e-111">View related data assets</span></span>
<span data-ttu-id="60d1e-112">若要檢視與所選資料集相關的資料資產，請使用 [關聯性] 索引標籤，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="60d1e-112">To view data assets that are related to a selected dataset, use the **Relationships** tab as shown in the following image:</span></span> 

![Azure 資料目錄 - 檢視相關的資料資產](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

<span data-ttu-id="60d1e-114">在此範例中，所選取的 **ProductSubcategory** 資料資產有兩個關聯性：</span><span class="sxs-lookup"><span data-stu-id="60d1e-114">In this example, there are two relationships for the selected **ProductSubcategory** data asset:</span></span> 

- <span data-ttu-id="60d1e-115">[Product] 資料表的 [ProductSubcategoryID] 資料行與所選 [ProductSubcategory] 資料表的 [ProductSubcategoryID] 資料行之間具有外部索引鍵關聯性。</span><span class="sxs-lookup"><span data-stu-id="60d1e-115">ProductSubcategoryID column of the Product table has a foreign key relationship with ProductSubcategoryID column of the selected ProductSubcategory table.</span></span> 
- <span data-ttu-id="60d1e-116">[ProductSubCategory] 資料表的 [ProductCategoryID] 資料行與所選 [ProductCategory] 資料表的 [ProductCategoryID] 資料行之間具有外部索引鍵關聯性。</span><span class="sxs-lookup"><span data-stu-id="60d1e-116">ProductCategoryID column of the ProductSubCategory table has a foreign key relationship with ProductCategoryID column of the selected ProductCategory table.</span></span>

> [!NOTE]
> <span data-ttu-id="60d1e-117">請注意關聯性樹狀檢視中的箭頭方向。</span><span class="sxs-lookup"><span data-stu-id="60d1e-117">Notice the direction of the arrow in the relationships tree view.</span></span>  

<span data-ttu-id="60d1e-118">若要查看更多詳細資料 (例如資料行的完整名稱)，請將滑鼠游標移至其上方，您就會看到類似下圖的快顯訊息：</span><span class="sxs-lookup"><span data-stu-id="60d1e-118">To see more details such as the fully qualified name of the column, move the mouse over and you see a popup similar to the following image:</span></span> 

![Azure 資料目錄 - 關聯性快顯訊息](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

<span data-ttu-id="60d1e-120">若要包含已註冊之資產間的關聯性，請重新註冊這些資產。</span><span class="sxs-lookup"><span data-stu-id="60d1e-120">To include relationships between assets that have already been registered, re-register those assets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60d1e-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="60d1e-121">Next steps</span></span>
- [<span data-ttu-id="60d1e-122">如何管理資料資產</span><span class="sxs-lookup"><span data-stu-id="60d1e-122">How to manage data assets</span></span>](data-catalog-how-to-manage.md)