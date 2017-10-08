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
# <a name="how-tooview-related-data-assets-in-azure-data-catalog"></a>Tooview 關聯在 Azure 資料目錄中的資料資產的方式？
Azure 資料目錄可讓您 tooview 資料資產相關的 tooa 選取資料資產和檢視之間的關聯性。 

## <a name="supported-data-sources"></a>支援的資料來源 
當您註冊從 hello 下列資料來源的資料資產時，Azure 資料目錄將會自動註冊選取的 hello 資料資產之間的聯結關聯性的相關中繼資料。 

- SQL Server
- Azure SQL Database
- MySQL
- Oracle

## <a name="view-related-data-assets"></a>檢視相關的資料資產
tooview 資料資產的相關的 tooa 選取資料集，使用 hello**關聯性**索引標籤中 hello 下列影像所示： 

![Azure 資料目錄 - 檢視相關的資料資產](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

在此範例中，有兩個關聯性選取的 hello **ProductSubcategory**資料資產： 

- ProductSubcategoryID hello 產品資料表資料行有 ProductSubcategoryID hello 選取 ProductSubcategory 資料表資料行的外部索引鍵關聯性。 
- Production.productcategory hello ProductSubCategory 資料表資料行有 Production.productcategory hello 選取 ProductCategory 資料表資料行的外部索引鍵關聯性。

> [!NOTE]
> 請注意 hello hello 關聯性樹狀結構檢視中的 hello 箭頭方向。  

toosee 更多詳細資料，例如 hello 完整 hello 資料行名稱移 hello 滑鼠，而且您看見快顯視窗類似 toohello，下列影像： 

![Azure 資料目錄 - 關聯性快顯訊息](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

tooinclude 已註冊的資產之間的關聯性重新註冊這些資產。

## <a name="next-steps"></a>後續步驟
- [如何 toomanage 資料資產](data-catalog-how-to-manage.md)
