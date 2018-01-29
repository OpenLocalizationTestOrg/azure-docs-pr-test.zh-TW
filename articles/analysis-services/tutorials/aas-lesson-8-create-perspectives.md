---
title: "Azure Analysis Services 教學課程第 8 課：建立檢視方塊 | Microsoft Docs"
description: "說明如何在 Azure Analysis Services 教學課程專案中建立檢視方塊。"
services: analysis-services
documentationcenter: 
author: Minewiskan
manager: kfile
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 01/08/2018
ms.author: owend
ms.openlocfilehash: 190a9c998bceb97f8446265809b8d2c3bdc76abc
ms.sourcegitcommit: 176c575aea7602682afd6214880aad0be6167c52
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2018
---
# <a name="create-perspectives"></a>建立檢視方塊

在這堂課中，您可以建立「網際網路銷售」檢視方塊。 檢視方塊會定義可檢視的模型子集，以提供聚焦、商務特有或應用程式特有的觀點。 當使用者使用檢視方塊連線至模型時，他們只會看到如該檢視方塊中所定義欄位的那些模型物件 (資料表、資料行、量值、階層及 KPI)。 若要深入了解，請參閱[檢視方塊](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular)。
  
您在這堂課中建立的「網際網路銷售」檢視方塊會排除 DimCustomer 資料表物件。 當您建立從檢視中排除某些物件的檢視方塊時，該物件仍然存在於模型中。 不過，不會顯示在報告用戶端欄位清單中。 計算結果欄和量值不管是否包含在檢視方塊中，仍然可以從排除的物件資料計算。  
  
本課程的目的在於說明如何建立檢視方塊，以及熟悉表格式模型撰寫工具。 如果您之後展開此模型以納入其他資料表，您可以建立其他檢視方塊來定義不同的模型觀點，例如，庫存與銷售。  
  
這堂課的預估完成時間：**5 分鐘**  
  
## <a name="prerequisites"></a>必要條件  
本主題是表格式模型教學課程的一部分，請依序完成。 在這堂課中執行工作之前，您必須已完成上一堂課︰[第 7 課︰建立關鍵效能指標](../tutorials/aas-lesson-7-create-key-performance-indicators.md)。  
  
## <a name="create-perspectives"></a>建立檢視方塊  
  
#### <a name="to-create-an-internet-sales-perspective"></a>建立網際網路銷售檢視方塊  
  
1.  按一下 [模型] 功能表 > [檢視方塊] > [建立和管理]。  
  
2.  在 [檢視方塊] 對話方塊中，按一下 [新增檢視方塊]。  
  
3.  按兩下 [新增檢視方塊] 資料行標題，並將其重新命名為 [網際網路銷售]。  
  
4.  選取除了 [DimCustomer] 以外的所有資料表。  
  
    ![aas-lesson8-perspectives](../tutorials/media/aas-lesson8-perspectives.png)
  
    在後面的課程中，您會使用 [使用 Excel 分析] 功能來測試此檢視方塊。 Excel PivotTable 欄位清單會包含除了 DimCustomer 資料表以外的每個資料表。  

## <a name="whats-next"></a>後續步驟
[第 9 課：建立階層](../tutorials/aas-lesson-9-create-hierarchies.md)。
  
  
  
  
