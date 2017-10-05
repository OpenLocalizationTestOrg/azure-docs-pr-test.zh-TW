---
title: "SQL 資料倉儲下層用戶端對資料稽核的支援 | Microsoft Docs"
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
ms.openlocfilehash: a7ea6141285a0098339f1e071af2592dd4535c12
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="sql-data-warehouse----downlevel-clients-support-for-auditing-and-dynamic-data-masking"></a><span data-ttu-id="0c1ae-103">SQL 資料倉儲 -  下層用戶端對稽核和動態資料遮罩的支援</span><span class="sxs-lookup"><span data-stu-id="0c1ae-103">SQL Data Warehouse -  Downlevel clients support for auditing and Dynamic Data Masking</span></span>
<span data-ttu-id="0c1ae-104">[稽核](sql-data-warehouse-auditing-overview.md) 可與支援 TDS 重新導向的 SQL 用戶端搭配使用。</span><span class="sxs-lookup"><span data-stu-id="0c1ae-104">[Auditing](sql-data-warehouse-auditing-overview.md) works with SQL clients that support TDS redirection.</span></span>

<span data-ttu-id="0c1ae-105">實作 TDS 7.4 的任何用戶端應該也支援重新導向。</span><span class="sxs-lookup"><span data-stu-id="0c1ae-105">Any client which implements TDS 7.4 should also support redirection.</span></span> <span data-ttu-id="0c1ae-106">例外包括其中未完全支援重新導向功能的 JDBC 4.0，和其中未實作重新導向的 Tedious for Node.JS。</span><span class="sxs-lookup"><span data-stu-id="0c1ae-106">Exceptions to this include JDBC 4.0 in which the redirection feature is not fully supported and Tedious for Node.JS in which redirection was not implemented.</span></span>

<span data-ttu-id="0c1ae-107">對於「舊版用戶端」，也就是支援 TDS 7.3 版和以下版本 - 應該修改連接字串中的伺服器 FQDN：</span><span class="sxs-lookup"><span data-stu-id="0c1ae-107">For "Downlevel clients", i.e. which support TDS version 7.3 and below - the server FQDN in the connection string should be modified:</span></span>

<span data-ttu-id="0c1ae-108">連接字串中的原始伺服器 FQDN：<*伺服器名稱*>.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="0c1ae-108">Original server FQDN in the connection string: <*server name*>.database.windows.net</span></span>

<span data-ttu-id="0c1ae-109">連接字串中已修改的伺服器 FQDN：<*伺服器名稱*>.database.**secure**.windows.net</span><span class="sxs-lookup"><span data-stu-id="0c1ae-109">Modified server FQDN in the connection string: <*server name*>.database.**secure**.windows.net</span></span>

<span data-ttu-id="0c1ae-110">「舊版用戶端」的部分清單包括：</span><span class="sxs-lookup"><span data-stu-id="0c1ae-110">A partial list of "Downlevel clients" includes:</span></span>

* <span data-ttu-id="0c1ae-111">.NET 4.0 和以下版本，</span><span class="sxs-lookup"><span data-stu-id="0c1ae-111">.NET 4.0 and below,</span></span>
* <span data-ttu-id="0c1ae-112">ODBC 10.0 和以下版本。</span><span class="sxs-lookup"><span data-stu-id="0c1ae-112">ODBC 10.0 and below.</span></span>
* <span data-ttu-id="0c1ae-113">JDBC (雖然 JDBC 支援 TDS 7.4，但並未完整支援 TDS 重新導向功能)</span><span class="sxs-lookup"><span data-stu-id="0c1ae-113">JDBC (while JDBC does support TDS 7.4, the TDS redirection feature is not fully supported)</span></span>
* <span data-ttu-id="0c1ae-114">Tedious (適用於 Node.JS)</span><span class="sxs-lookup"><span data-stu-id="0c1ae-114">Tedious (for Node.JS)</span></span>

<span data-ttu-id="0c1ae-115">**備註：** 上述伺服器 FDQN 修改可能會對於套用 SQL Server 層級稽核原則有所助益，不需要每個資料庫中的組態步驟 (暫存緩和)。</span><span class="sxs-lookup"><span data-stu-id="0c1ae-115">**Remark:** The above server FDQN modification may be useful also for applying a SQL Server Level Auditing policy without a need for a configuration step in each database (Temporary mitigation).</span></span>     

