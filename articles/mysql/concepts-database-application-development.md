---
title: "Azure 資料庫的 MySQL aaaDatabase 應用程式開發概觀 |Microsoft 文件"
description: "引進了用於 MySQL 撰寫應用程式程式碼 tooconnect tooAzure 資料庫時，開發人員應該遵循的設計考量"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: f08df605eba21b4ba4b43565c0a7ded95779a171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-development-overview-for-azure-database-for-mysql"></a>適用於 MySQL 的 Azure 資料庫的應用程式開發概觀 
這篇文章討論的 MySQL 撰寫應用程式程式碼 tooconnect tooAzure 資料庫時，開發人員應該遵循的設計考量 

> [!TIP]
> 教學課程顯示如何 toocreate 伺服器，建立伺服器型防火牆，檢視伺服器屬性、 建立資料庫、 連線，並使用 workbench 和 mysql.exe 查詢，請參閱[設計您的第一個 Azure MySQL 資料庫](tutorial-design-database-using-portal.md)

## <a name="language-and-platform"></a>語言和平台
有一些程式碼範例可供各種程式設計語言和平台使用。 您可以找到連結 toohello 程式碼範例：[連接程式庫用於 MySQL 的 tooconnect tooAzure 資料庫](concepts-connection-libraries.md)

## <a name="tools"></a>工具
Azure 的 MySQL 資料庫使用 hello MySQL community 版本，與 MySQL 常見的管理工具 Workbench 或 MySQL 公用程式，例如 mysql.exe，例如相容[phpMyAdmin](https://www.phpmyadmin.net/)， [Navicat](https://www.navicat.com/products/navicat-for-mysql)，和其他人。 您也可以使用 hello Azure 入口網站、 Azure CLI 和 REST Api toointeract 與 hello 資料庫服務。

## <a name="resource-limitations"></a>資源限制
Azure 的 MySQL 資料庫管理 hello 資源可用 tooa 伺服器使用兩個不同的機制： 
- 資源管理 
- 強制執行限制。

## <a name="security"></a>安全性
Azure MySQL 資料庫提供資源，以便在 MySQL 資料庫上限制存取、保護資料、設定使用者和角色，以及監視活動。

## <a name="authentication"></a>驗證
Azure MySQL 資料庫支援適用於使用者與登入的伺服器驗證。

## <a name="resiliency"></a>復原功能
當連線 tooMySQL 資料庫時，就會發生暫時性的錯誤時，您的程式碼應該重試 hello 呼叫。 我們建議您使用 hello 重試邏輯使用邏輯、 功能，讓它不會不會使不勝負荷 hello SQL Database 與多個用戶端重試一次同時。

- 程式碼範例： 取得程式碼範例將示範中，然後重試邏輯，請參閱您選擇在 hello 語言的範例：[連接程式庫用於 MySQL 的 tooconnect tooAzure 資料庫](concepts-connection-libraries.md)

## <a name="managing-connections"></a>管理連接
資料庫連線是有限的資源，因此我們建議您合理使用的連接存取您的 MySQL 資料庫時 tooachieve 更佳的效能。
- 存取 hello 資料庫使用連接共用或持續連線。
- 使用簡短的連接生命週期的 access hello 資料庫。 
- Hello hello 連線嘗試、 toocatch 失敗，因為 tooconcurrent 連接點的應用程式中使用重試邏輯已達到允許的 hello 最大值。 在 [hello 重試邏輯、 設定短暫的延遲，，然後等待 hello 其他連接嘗試之前的隨機時間點。
