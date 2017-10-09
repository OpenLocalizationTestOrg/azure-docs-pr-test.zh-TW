---
title: "aaaBuild SQL 資料倉儲與整合解決方案 |Microsoft 文件"
description: "工具以及提供可與 SQL 資料倉儲整合之解決方案的合作夥伴。 "
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: e2dc8f3f-10e3-4589-a4e2-50c67dfcf67f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: c8a4202dd84305bea4e4c2faf0e4791d026e794f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="leverage-other-services-with-sql-data-warehouse"></a>以 SQL 資料倉儲來搭配運用其他服務
此外 tooits 核心功能，SQL 資料倉儲可讓使用者 tooleverage 許多 hello 中 Azure 旁邊的其他服務。  具體來說，我們目前採取 toodeeply 整合與 hello 下列步驟：

* Power BI
* Azure Data Factory
* Azure Machine Learning
* Azure 串流分析

我們正與更多服務 tooconnect 跨 hello Azure 生態系統。

## <a name="power-bi"></a>Power BI
Power BI 整合可讓您 tooleverage hello 選計算能力的 SQL 資料倉儲與 hello 動態報告和 Power BI 視覺效果。 目前 Power BI 整合包括：

* **直接連接**：針對 SQL 資料倉儲進行之邏輯下推的更進階連接。  可提供更快速且更大規模的分析。
* **在 Power BI 中開啟**: hello 'Power BI 中開啟' 按鈕傳遞執行個體資訊 tooPower BI，以便更順暢的連線。

請參閱[與 Power BI 整合](sql-data-warehouse-integrate-power-bi.md)或 hello [Power BI 文件](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx)如需詳細資訊。

## <a name="azure-data-factory"></a>Azure Data Factory
Azure Data Factory 可讓使用者的受管理的平台 toocreate 複雜擷取載入管線。  與 Azure Data Factory 的 SQL 資料倉儲的整合包含 hello 下列：

* **預存程序**： 協調 hello 執行 SQL 資料倉儲上的預存程序。
* **複製**： 使用 ADF toomove 資料到 SQL 資料倉儲。  這項作業可以使用 ADF 的標準資料移動機制，或在 hello PolyBase 涵蓋。 

請參閱[與 Azure Data Factory 整合](sql-data-warehouse-integrate-azure-data-factory.md)或 hello [Azure Data Factory 文件](https://azure.microsoft.com/documentation/services/data-factory/)如需詳細資訊。

## <a name="azure-machine-learning"></a>Azure Machine Learning
Azure Machine Learning 是完全受管理的分析服務，可讓使用者利用大量預測工具 toocreate 複雜模型。  SQL 資料倉儲做為來源和目的地，這些模型以支援下列功能的 hello:

* **讀取資料：** 針對 SQL 資料倉儲透過 T-SQL 大規模驅動模型。
* **將資料寫入：**認可變更，從任何模型傳回 tooSQL 資料倉儲。

請參閱[整合與 Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md)或 hello [Azure Machine Learning 文](https://azure.microsoft.com/services/machine-learning/)如需詳細資訊。

## <a name="azure-stream-analytics"></a>Azure 串流分析
Azure 串流分析是複雜、完全受管理的基礎結構，可處理和取用產生自 Azure 事件中樞的事件資料。  SQL 資料倉儲與整合可讓資料流資料 toobe 有效地處理並啟用更深入的關聯式資料一起儲存，多個進階分析。  

* **工作輸出：**傳送輸出資料流分析工作直接 tooSQL 資料倉儲。

請參閱[與 Azure Stream Analytics 整合](sql-data-warehouse-integrate-azure-stream-analytics.md)或 hello [Azure Stream Analytics 文件](https://azure.microsoft.com/documentation/services/stream-analytics/)如需詳細資訊。

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop/

[Azure Data Factory]: sql-data-warehouse-integrate-azure-data-factory.md
[Azure Machine Learning]: sql-data-warehouse-integrate-azure-machine-learning.md
[Azure Stream Analytics]: sql-data-warehouse-integrate-azure-stream-analytics.md
[Power BI]: sql-data-warehouse-integrate-power-bi.md
[Partners]: sql-data-warehouse-partner-business-intelligence.md

<!--MSDN references-->

<!--Other Web references-->
