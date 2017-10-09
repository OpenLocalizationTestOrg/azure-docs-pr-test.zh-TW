---
title: "SQL 資料倉儲與 Azure Data Factory aaaUse |Microsoft 文件"
description: "搭配使用 Azure Data Factory (ADF) 與 SQL 資料倉儲以便開發解決方案的秘訣。"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 492de762-c7a2-4cdb-943f-3135230e94f1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: d40a547830f9681504253d39ae3066800a955c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-factory-with-sql-data-warehouse"></a>搭配使用 Azure Data Factory 與 SQL 資料倉儲
Azure Data Factory 提供完全受管理的方法，來協調 hello 傳輸資料及執行 SQL 資料倉儲上的預存程序。  這可讓您 toomore 輕鬆地設定和排程複雜擷取轉換和載入 (ETL) 程序到 SQL 資料倉儲。 如需更完整的 Azure Data Factory 概觀，請參閱 hello [Azure Data Factory 文件][Azure Data Factory documentation]。

## <a name="data-movement"></a>資料移動
Azure Data Factory 可讓資料在內部部署來源與不同的 Azure 服務之間移動。  目前的整體整合，使用 Azure Data Factory 支援的資料移動 tooand 從下列位置的 hello:

* Azure Blob 儲存體
* Azure SQL Database
* 內部部署 SQL Server
* IaaS 上的 SQL Server

資料備份 tooset 如何複製活動的詳細資訊請參閱[複製資料與 Azure Data Factory][Copy data with Azure Data Factory]

## <a name="stored-procedures"></a>預存程序
 在 hello 相同方式，會使用 tooschedule 資料傳輸，Azure Data Factory 可以也使用的 tooorchestrate hello 執行預存程序。  這允許更複雜的管線 toobe 建立，並擴充 Azure Data Factory 的能力 tooleverage hello 運算能力更佳的 SQL 資料倉儲。

## <a name="next-steps"></a>後續步驟
如需整合概觀，請參閱 [SQL 資料倉儲整合概觀][SQL Data Warehouse integration overview]。
如需更多開發秘訣，請參閱 [SQL 資料倉儲開發概觀][SQL Data Warehouse development overview]。

<!--Image references-->

<!--Article references-->

[Copy data with Azure Data Factory]: ../data-factory/data-factory-data-movement-activities.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]: ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory documentation]:https://azure.microsoft.com/documentation/services/data-factory/

