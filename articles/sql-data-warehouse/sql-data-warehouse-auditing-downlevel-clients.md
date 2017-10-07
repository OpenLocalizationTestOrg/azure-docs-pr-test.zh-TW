---
title: "aaaSQL 資料倉儲下層用戶端支援針對資料稽核 |Microsoft 文件"
description: "了解 SQL 資料倉儲下層用戶端對資料稽核的支援"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: dfe29ff3-dfeb-4309-83c0-c1a300f4f44e
ms.service: sql-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 377488680eb297c3e9b1dc754c003c5b19b47996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse----downlevel-clients-support-for-auditing-and-dynamic-data-masking"></a>SQL 資料倉儲 -  下層用戶端對稽核和動態資料遮罩的支援
[稽核](sql-data-warehouse-auditing-overview.md) 可與支援 TDS 重新導向的 SQL 用戶端搭配使用。

實作 TDS 7.4 的任何用戶端應該也支援重新導向。 例外狀況 toothis 納入 JDBC 4.0 的 hello 重新導向功能不完全支援和 Tedious for Node.JS 不會實作重新導向時。

「 下層用戶端 」，也就是它支援 TDS 版本 7.3，且以下-hello hello 連接字串中的伺服器 FQDN 應修改：

原始伺服器 FQDN hello 連接字串中： <*伺服器名稱*>。.database.windows.net

已修改的伺服器 FQDN hello 連接字串中： <*伺服器名稱*>.database。**安全**。 windows.net

「舊版用戶端」的部分清單包括：

* .NET 4.0 和以下版本，
* ODBC 10.0 和以下版本。
* JDBC （雖然 JDBC 可支援 TDS 7.4，hello TDS 重新導向功能不完全支援）
* Tedious (適用於 Node.JS)

**備註：** hello 上述伺服器 FDQN 修改可能會有所助益也沒有需要的設定步驟 （暫存緩和） 每個資料庫中套用 SQL Server 層級稽核原則。     

