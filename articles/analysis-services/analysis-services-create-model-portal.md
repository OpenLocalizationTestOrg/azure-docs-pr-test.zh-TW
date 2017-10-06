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
# <a name="create-a-model-in-azure-portal"></a>在 Azure 入口網站中建立模型

提供快速簡便方式 toocreate hello Azure Analysis Services web 設計工具 （預覽） 功能在 Azure 入口網站，並編輯表格式模型和查詢模型資料直接在您的瀏覽器。 

請記住，hello web 設計工具是**預覽**。 正在加入新的功能在預覽中，所有 hello 時間時功能會受到限制。 如需進階模型開發和測試，是最佳 toouse Visual Studio (SSDT) 和 SQL Server Management Studio (SSMS)。

## <a name="prerequisites"></a>必要條件

- Azure Analysis Services 伺服器在 hello 標準或開發人員層。 使用 hello Web 設計工具所建立的新模型是 DirectQuery，只有支援這些層。
- 作為資料來源的 Azure SQL Database、Azure SQL 資料倉儲或 Power BI Desktop (.pbix) 檔案。 從 Power BI Desktop 檔案建立的新模型支援 Azure SQL Database、Azure SQL 資料倉儲、Oracle 和 Teradata 資料來源。
- SQL Server 帳戶和密碼來連接 tooAzure SQL Database 或 Azure SQL 資料倉儲資料來源。

## <a name="toocreate-a-new-tabular-model"></a>toocreate 新的表格式模型

1. 在您的伺服器 [概觀] 刀鋒視窗 > [Web 設計工具] 中，按一下 [開啟]。

    ![在 Azure 入口網站中建立模型](./media/analysis-services-create-model-portal/aas-create-portal-overview-wd.png)

2. 在 [Web 設計工具]  >  [模型] 中，按一下 [+ 新增]。

    ![在 Azure 入口網站中建立模型](./media/analysis-services-create-model-portal/aas-create-portal-models.png)

3. 在 [新增模型] 中輸入模型名稱，然後選取資料來源。

    ![在 Azure 入口網站中的新增模型對話方塊](./media/analysis-services-create-model-portal/aas-create-portal-new-model.png)

4. 在**連接**，輸入 hello 連接屬性。 使用者名稱和密碼必須是 SQL Server 帳戶。

     ![在 Azure 入口網站中的連線對話方塊](./media/analysis-services-create-model-portal/aas-create-portal-connect.png)

5. 在**資料表和檢視表**hello 資料表 tooinclude 選取在模型中，然後按一下**建立**。 會使用金鑰組自動建立資料表之間的關聯性。

     ![選取資料表和檢視](./media/analysis-services-create-model-portal/aas-create-portal-tables.png)

新的模型會出現在您的瀏覽器。 您可以在這裡執行下列動作：   

- 拖曳欄位 toohello 查詢設計工具，以及加入篩選來查詢模型資料。
- 在資料表中建立新的量值。
- 使用 hello json 編輯器來編輯模型中繼資料。
- 在 Visual Studio (SSDT) 中，Power BI Desktop 或 Excel 中開啟 hello 模型。

![選取資料表和檢視](./media/analysis-services-create-model-portal/aas-create-portal-query.png)

> [!NOTE]
> 當您編輯模型中繼資料，或在您的瀏覽器中建立新的量值時，您要在 Azure 中儲存這些變更 tooyour 模型。 如果您正在 SSDT、Power BI Desktop 或 Excel 中使用模型，您的模型可以不同步。


## <a name="next-steps"></a>後續步驟 
[管理資料庫角色和使用者](analysis-services-database-users.md)  
[與 Excel 連線](analysis-services-connect-excel.md)  


