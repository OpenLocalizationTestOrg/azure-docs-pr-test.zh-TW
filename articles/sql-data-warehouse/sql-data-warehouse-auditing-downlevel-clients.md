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
# <a name="sql-data-warehouse----downlevel-clients-support-for-auditing-and-dynamic-data-masking"></a><span data-ttu-id="fede5-103">SQL 資料倉儲 -  下層用戶端對稽核和動態資料遮罩的支援</span><span class="sxs-lookup"><span data-stu-id="fede5-103">SQL Data Warehouse -  Downlevel clients support for auditing and Dynamic Data Masking</span></span>
<span data-ttu-id="fede5-104">[稽核](sql-data-warehouse-auditing-overview.md) 可與支援 TDS 重新導向的 SQL 用戶端搭配使用。</span><span class="sxs-lookup"><span data-stu-id="fede5-104">[Auditing](sql-data-warehouse-auditing-overview.md) works with SQL clients that support TDS redirection.</span></span>

<span data-ttu-id="fede5-105">實作 TDS 7.4 的任何用戶端應該也支援重新導向。</span><span class="sxs-lookup"><span data-stu-id="fede5-105">Any client which implements TDS 7.4 should also support redirection.</span></span> <span data-ttu-id="fede5-106">例外狀況 toothis 納入 JDBC 4.0 的 hello 重新導向功能不完全支援和 Tedious for Node.JS 不會實作重新導向時。</span><span class="sxs-lookup"><span data-stu-id="fede5-106">Exceptions toothis include JDBC 4.0 in which hello redirection feature is not fully supported and Tedious for Node.JS in which redirection was not implemented.</span></span>

<span data-ttu-id="fede5-107">「 下層用戶端 」，也就是它支援 TDS 版本 7.3，且以下-hello hello 連接字串中的伺服器 FQDN 應修改：</span><span class="sxs-lookup"><span data-stu-id="fede5-107">For "Downlevel clients", i.e. which support TDS version 7.3 and below - hello server FQDN in hello connection string should be modified:</span></span>

<span data-ttu-id="fede5-108">原始伺服器 FQDN hello 連接字串中： <*伺服器名稱*>。.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="fede5-108">Original server FQDN in hello connection string: <*server name*>.database.windows.net</span></span>

<span data-ttu-id="fede5-109">已修改的伺服器 FQDN hello 連接字串中： <*伺服器名稱*>.database。**安全**。 windows.net</span><span class="sxs-lookup"><span data-stu-id="fede5-109">Modified server FQDN in hello connection string: <*server name*>.database.**secure**.windows.net</span></span>

<span data-ttu-id="fede5-110">「舊版用戶端」的部分清單包括：</span><span class="sxs-lookup"><span data-stu-id="fede5-110">A partial list of "Downlevel clients" includes:</span></span>

* <span data-ttu-id="fede5-111">.NET 4.0 和以下版本，</span><span class="sxs-lookup"><span data-stu-id="fede5-111">.NET 4.0 and below,</span></span>
* <span data-ttu-id="fede5-112">ODBC 10.0 和以下版本。</span><span class="sxs-lookup"><span data-stu-id="fede5-112">ODBC 10.0 and below.</span></span>
* <span data-ttu-id="fede5-113">JDBC （雖然 JDBC 可支援 TDS 7.4，hello TDS 重新導向功能不完全支援）</span><span class="sxs-lookup"><span data-stu-id="fede5-113">JDBC (while JDBC does support TDS 7.4, hello TDS redirection feature is not fully supported)</span></span>
* <span data-ttu-id="fede5-114">Tedious (適用於 Node.JS)</span><span class="sxs-lookup"><span data-stu-id="fede5-114">Tedious (for Node.JS)</span></span>

<span data-ttu-id="fede5-115">**備註：** hello 上述伺服器 FDQN 修改可能會有所助益也沒有需要的設定步驟 （暫存緩和） 每個資料庫中套用 SQL Server 層級稽核原則。</span><span class="sxs-lookup"><span data-stu-id="fede5-115">**Remark:** hello above server FDQN modification may be useful also for applying a SQL Server Level Auditing policy without a need for a configuration step in each database (Temporary mitigation).</span></span>     

