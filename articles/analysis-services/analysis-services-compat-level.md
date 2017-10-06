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
# <a name="compatibility-level-for-analysis-services-tabular-models"></a>Analysis Services 表格式模型的相容性層級

*相容性層級*是指在 hello Analysis Services 引擎 toorelease 特定行為。 與 SQL server 的主要版本通常一致變更 toohello 相容性層級。 這些變更也會實作兩個平台之間的 Azure Analysis Services toomaintain 同位檢查。 相容性層級變更也會影響您的表格式模型中的可用功能。 例如，DirectQuery 和表格式物件中繼資料，請在根據 hello 相容性層級有不同的實作。 

Azure Analysis Services 支援 hello 1200 和 1400年相容性層級的表格式模型。

hello 最新相容性層級是 1400年。 此層級與 SQL Server 2017 Analysis Services 一致。 Hello 1400 相容性層級中的主要功能包括：

*  資料連線的新基礎結構，以及匯入表格式模型，且支援 TOM API 和 TMSL 指令碼。 這項新功能可支援其他資料來源，例如 Azure Blob 儲存體。
*  使用 Get Data 與 M 運算式的資料轉換和資料混搭功能。
*  量值支援使用 DAX 運算式的詳細資料列屬性。 此屬性可讓用戶端工具，像是 Microsoft Excel toodrill 向 toodetailed 資料，從彙總的報表。 例如，當使用者檢視區域和月份的總銷售額，則可以檢視相關聯的 hello 訂單詳細資料。 
*  物件層級安全性的資料表和資料行名稱，此外 toohello 中的資料。
*  不完全階層的增強支援。
*  效能和監控改善。
  
## <a name="set-compatibility-level"></a>設定相容性層級 
 當在 SSDT 中建立新的表格式模型專案，您可以指定 hello 相容性層級上 hello**表格式模型設計師**對話方塊。 
  
 ![ssas_tabularproject_compat1200](./media/analysis-services-compat-level/aas-tabularproject-compat.png)  
  
 如果您選取 hello**不要再顯示此訊息**選項時，所有後續專案都使用您指定為 hello 預設 hello 相容性層級。 您可以變更在 SSDT 中的 hello 預設相容性層級**工具** > **選項**。  
  
 將現有的表格式模型專案，在 SSDT 中，設定 hello tooupgrade**相容性層級**hello 模型中的屬性**屬性**視窗。 請記住，升級 hello 相容性層級是無法復原。
  
## <a name="check-compatibility-level-for-a-tabular-model-database-in-sql-server-management-studio"></a>檢查 SQL Server Management Studio 中表格式模型資料庫的相容性層級 
 在 SSMS 中，以滑鼠右鍵按一下 hello 資料庫名稱 >**屬性** > **相容性層級**。  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a>檢查 SSMS 中的伺服器支援的相容性層級  
 在 SSMS 中，以滑鼠右鍵按一下 hello 伺服器名稱 >**屬性** > **支援的相容性層級**。  
  
 此屬性指定 hello 最高相容性層級將在 hello （不含預覽） 的伺服器執行的資料庫。 無法變更 hello 支援相容性層級。  

## <a name="next-steps"></a>後續步驟
  [在 Azure 入口網站中建立模型](analysis-services-create-model-portal.md)   
  [ Analysis Services](analysis-services-manage.md)  
