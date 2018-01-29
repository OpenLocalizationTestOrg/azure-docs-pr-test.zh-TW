---
title: "適用於 MySQL 的 Azure 資料庫中的限制 | Microsoft Docs"
description: "描述適用於 MySQL 的 Azure 資料庫中的預覽限制。"
services: mysql
author: jasonh
ms.author: kamathsun
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 01/11/2018
ms.openlocfilehash: f0f9a10f987f19d8ae77a07038cffe23446856fd
ms.sourcegitcommit: 562a537ed9b96c9116c504738414e5d8c0fd53b1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/12/2018
---
# <a name="limitations-in-azure-database-for-mysql"></a>「適用於 MySQL 的 Azure 資料庫」中的限制
適用於 MySQL 的 Azure 資料庫服務目前為公開預覽狀態。 下列各節說明資料庫服務中的容量、儲存引擎支援、權限支援、資料操作陳述式支援，以及功能限制。 另請參閱適用於 MySQL 資料庫引擎的[一般限制](https://dev.mysql.com/doc/mysql-reslimits-excerpt/5.6/en/limits.html) \(英文\)。

## <a name="service-tier-maximums"></a>服務層上限
適用於 MySQL 的 Azure 資料庫具有多個可在建立伺服器時從中選擇的服務層。 如需詳細資訊，請參閱[了解每個服務層中可用的項目](concepts-service-tiers.md)。  

在預覽期間，每個服務層中具有連線、計算單位及儲存體的數目上限，如下： 

|                            |                   |
| :------------------------- | :---------------- |
| **連接數目上限**        |                   |
| 基本的 50 個計算單位     | 50 個連接    |
| 基本的 100 個計算單位    | 100 個連接   |
| 標準的 100 個計算單位 | 200 個連接   |
| 標準的 200 個計算單位 | 400 個連接   |
| 標準的 400 個計算單位 | 800 個連線   |
| 標準的 800 個計算單位 | 1600 個連線  |
| **計算單位數目上限**      |                   |
| 基本服務層         | 100 個計算單位 |
| 標準服務層      | 800 個計算單位 |
| **儲存體上限**            |                   |
| 基本服務層         | 1 TB              |
| 標準服務層      | 1 TB              |

到達太多連接時，您可能會收到下列錯誤：
> 錯誤 1040 (08004)：太多的連接

## <a name="storage-engine-support"></a>儲存引擎支援

### <a name="supported"></a>支援
- [InnoDB](https://dev.mysql.com/doc/refman/5.7/en/innodb-introduction.html) \(英文\)
- [MEMORY](https://dev.mysql.com/doc/refman/5.7/en/memory-storage-engine.html) \(英文\)

### <a name="unsupported"></a>不支援
- [MyISAM](https://dev.mysql.com/doc/refman/5.7/en/myisam-storage-engine.html) \(英文\)
- [BLACKHOLE](https://dev.mysql.com/doc/refman/5.7/en/blackhole-storage-engine.html) \(英文\)
- [ARCHIVE](https://dev.mysql.com/doc/refman/5.7/en/archive-storage-engine.html) \(英文\)
- [FEDERATED](https://dev.mysql.com/doc/refman/5.7/en/federated-storage-engine.html) \(英文\)

## <a name="privilege-support"></a>權限支援

### <a name="unsupported"></a>不支援
- DBA 角色：許多伺服器參數與設定可能會在無意中造成伺服器效能降級，或是取消 DBMS 的 ACID 屬性。 因此，為了維護產品層級的服務完整性與 SLA，我們不會對客戶公開 DBA 角色。 於建立新資料庫行個體時所建構的預設使用者帳戶，可讓客戶在受管理的資料庫執行個體中執行大部分的 DDL 與 DML 陳述式。 
- SUPER 權限：同樣地，[SUPER 權限](https://dev.mysql.com/doc/refman/5.7/en/privileges-provided.html#priv_super) \(英文\) 也受到限制。

## <a name="data-manipulation-statement-support"></a>資料操作陳述式支援

### <a name="supported"></a>支援
- LOAD DATA INFILE：支援，但必須指定導向 UNC 路徑 (透過 XSMB 裝載的 Azure 儲存體) 的 [LOCAL] 參數。

### <a name="unsupported"></a>不支援
- SELECT ...INTO OUTFILE

## <a name="preview-functional-limitations"></a>預覽功能限制

### <a name="scale-operations"></a>調整作業
- 目前不支援跨服務層動態調整伺服器。 也就是在基本和標準服務層之間切換。
- 目前不支援依需求在預先建立的伺服器上動態增加儲存體。
- 不支援減少伺服器儲存體大小。

### <a name="server-version-upgrades"></a>伺服器版本升級
- 目前不支援在主要資料庫引擎版本之間進行自動轉換。

### <a name="point-in-time-restore"></a>還原時間點
- 不允許還原到不同服務層和/或計算單位與儲存體大小。
- 不支援還原已刪除的伺服器。

## <a name="functional-limitations"></a>功能限制：

### <a name="subscription-management"></a>訂用帳戶管理
- 目前不支援跨訂用帳戶和資源群組動態移動預先建立的伺服器。

## <a name="current-known-issues"></a>目前已知問題
- MySQL 伺服器執行個體於建立連線後會顯示錯誤的伺服器版本。 若要取得正確的伺服器執行個體版本，請在 MySQL 命令提示字元中使用 select version(); 命令。

## <a name="next-steps"></a>後續步驟
- [每個服務層中可用的項目](concepts-service-tiers.md)
- [支援的 MySQL 資料庫版本](concepts-supported-versions.md)
