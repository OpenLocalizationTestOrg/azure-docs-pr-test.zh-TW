---
title: "SQL 資料倉儲與 Azure Stream Analytics aaaUse |Microsoft 文件"
description: "搭配使用 Azure 串流分析與 SQL 資料倉儲以便開發解決方案的秘訣。"
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 8aeb2247-20c5-4a29-b327-30a8ce09dfdc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 1278197a6764864124fd92fc672de00b83ec343f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-with-sql-data-warehouse"></a>搭配使用 Azure 串流分析與 SQL 資料倉儲
Azure Stream Analytics 是完全受管理的服務，透過 hello 雲端中的資料流提供低延遲、 高可用性、 可擴充的複雜事件處理。 您可以藉由讀取了解 hello 基本概念[簡介 tooAzure Stream Analytics][Introduction tooAzure Stream Analytics]。 您接著可以學 toocreate 依照資料流分析的端對端解決方案如何 hello[開始使用 Azure Stream Analytics] [ Get started using Azure Stream Analytics]教學課程。

在本文中，您將學習如何 toouse Azure SQL 資料倉儲資料庫做為您的資料流分析工作的輸出來源。

## <a name="prerequisites"></a>必要條件
首先，執行透過下列步驟在 hello hello[開始使用 Azure Stream Analytics] [ Get started using Azure Stream Analytics]教學課程。  

1. 建立事件中樞輸入
2. 設定並啟動事件產生器應用程式
3. 佈建資料流分析工作
4. 指定工作輸入和查詢

接著，建立 Azure SQL 資料倉儲資料庫

## <a name="specify-job-output-azure-sql-data-warehouse-database"></a>指定工作輸出：Azure SQL 資料倉儲資料庫
### <a name="step-1"></a>步驟 1
在資料流分析工作按一下**輸出**hello 頁面上，然後再按一下 hello 由上至下**加入輸出**。

### <a name="step-2"></a>步驟 2
選取 SQL Database，然後按一下 [下一步]。

![][add-output]

### <a name="step-3"></a>步驟 3
輸入下列值 hello 下一個頁面上的 hello:

* *輸出別名*：輸入此工作輸出的易記名稱。
* 訂用帳戶：
  * 如果您的 SQL 資料倉儲資料庫在 hello 相同訂用帳戶 hello 資料流分析工作，從目前的訂用帳戶中選取 使用 SQL 資料庫。
  * 如果您的資料庫是在不同的訂用帳戶中，請選取 [使用其他訂用帳戶的 SQL Database]。
* *資料庫*： 指定 hello 目的地資料庫名稱。
* *伺服器名稱*： 指定 hello hello 您剛才指定的資料庫伺服器名稱。 您可以使用 hello Azure 傳統入口網站 toofind 這個。

![][server-name]

* *使用者名稱*： 指定 hello 擁有 hello 資料庫的寫入權限的帳戶使用者名稱。
* *密碼*： 提供 hello hello 密碼指定使用者帳戶。
* *資料表*： 指定 hello 資料庫中的 hello hello 目標資料表名稱。

![][add-database]

### <a name="step-4"></a>步驟 4
此工作輸出和 tooverify 資料流分析可以成功連線 toohello 資料庫，請按一下 hello 核取按鈕 tooadd。

![][test-connection]

Hello 連線 toohello 資料庫成功時，您會看到在 hello hello 入口網站底部的通知。 在 hello 底部 tootest hello 連線 toohello 資料庫，您可以按一下測試連接。

## <a name="next-steps"></a>後續步驟
如需整合概觀，請參閱 [SQL 資料倉儲整合概觀][SQL Data Warehouse integration overview]。

如需更多開發秘訣，請參閱 [SQL 資料倉儲開發概觀][SQL Data Warehouse development overview]。

<!--Image references-->

[add-output]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-output.png
[server-name]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/dw-server-name.png
[add-database]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-database.png
[test-connection]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/test-connection.png

<!--Article references-->

[Introduction tooAzure Stream Analytics]: ../stream-analytics/stream-analytics-introduction.md
[Get started using Azure Stream Analytics]: ../stream-analytics/stream-analytics-real-time-fraud-detection.md
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Stream Analytics documentation]: http://azure.microsoft.com/documentation/services/stream-analytics/
