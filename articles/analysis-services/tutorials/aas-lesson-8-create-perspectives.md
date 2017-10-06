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
# <a name="lesson-8-create-perspectives"></a>第 8 課：建立檢視方塊

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

在這堂課中，您可以建立「網際網路銷售」檢視方塊。 檢視方塊會定義可檢視的模型子集，以提供聚焦、商務特有或應用程式特有的觀點。 當使用者使用檢視方塊 tooa 模型，它們只會看到這些模型物件 （資料表、 資料行、 量值、 階層和 Kpi） 做為該檢視方塊中所定義的欄位。 詳細資訊，請參閱 toolearn[檢視方塊](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular)。
  
hello 您在這一課中建立的網際網路銷售檢視方塊排除 hello DimCustomer 資料表物件。 當您建立從檢視中排除特定物件的檢視方塊時，該物件仍然存在 hello 模型中。 不過，不會顯示在報告用戶端欄位清單中。 計算結果欄和量值不管是否包含在檢視方塊中，仍然可以從排除的物件資料計算。  
  
hello 本課程的目的是 toodescribe 如何 toocreate 檢視方塊並熟悉 hello 表格式模型撰寫工具。 如果您之後展開此模型 tooinclude 其他資料表，您可以建立其他檢視方塊 toodefine 不同觀點的 hello 模型，例如存貨和銷售。  
  
本課程的估計時間 toocomplete:**五分鐘**  
  
## <a name="prerequisites"></a>必要條件  
本主題是表格式模型教學課程的一部分，請依序完成。 在執行之前 hello 工作在這一課，您應已完成上一課 hello:[第 7 課： 建立關鍵效能指標](../tutorials/aas-lesson-7-create-key-performance-indicators.md)。  
  
## <a name="create-perspectives"></a>建立檢視方塊  
  
#### <a name="toocreate-an-internet-sales-perspective"></a>toocreate 網際網路銷售檢視方塊  
  
1.  按一下 hello**模型**功能表 >**檢視方塊** > **建立和管理**。  
  
2.  在 hello**檢視方塊**對話方塊中，按一下 **新檢視方塊**。  
  
3.  按兩下 hello**新檢視方塊**欄標題，並將其重新命名**Internet Sales**。  
  
4.  選取 hello 所有都 hello 資料表*除了* **DimCustomer**。  
  
    ![aas-lesson8-perspectives](../tutorials/media/aas-lesson8-perspectives.png)
  
    在後面的課程，您使用在 Excel 功能 tootest hello 分析此檢視方塊。 hello Excel 樞紐分析表欄位清單包含每個資料表除了 hello DimCustomer 資料表。  

## <a name="whats-next"></a>後續步驟
[第 9 課：建立階層](../tutorials/aas-lesson-9-create-hierarchies.md)。
  
  
  
  
