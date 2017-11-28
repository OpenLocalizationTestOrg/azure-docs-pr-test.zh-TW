---
title: "SQL 資料倉儲中的透明資料加密 (T-SQL) | Microsoft Docs"
description: "SQL 資料倉儲中的透明資料加密 (TDE) (T-SQL)"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: barbkess
editor: 
ms.assetid: 8ccefef3-1308-41ee-b336-5e491d1098ae
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 74c9032aababdce91ed617cd7a4c628915b42504
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-transparent-data-encryption-tde"></a><span data-ttu-id="fe31d-103">開始使用透明資料加密 (TDE)</span><span class="sxs-lookup"><span data-stu-id="fe31d-103">Get started with Transparent Data Encryption (TDE)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fe31d-104">安全性概觀</span><span class="sxs-lookup"><span data-stu-id="fe31d-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="fe31d-105">驗證</span><span class="sxs-lookup"><span data-stu-id="fe31d-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="fe31d-106">加密 (入口網站)</span><span class="sxs-lookup"><span data-stu-id="fe31d-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="fe31d-107">加密 (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="fe31d-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="fe31d-108">需要的權限</span><span class="sxs-lookup"><span data-stu-id="fe31d-108">Required Permssions</span></span>
<span data-ttu-id="fe31d-109">您必須是系統管理員或 dbmanager 角色的成員，才能啟用透明資料加密 (TDE)。</span><span class="sxs-lookup"><span data-stu-id="fe31d-109">To enable Transparent Data Encryption (TDE), you must be an administrator or a member of the dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="fe31d-110">啟用加密</span><span class="sxs-lookup"><span data-stu-id="fe31d-110">Enabling Encryption</span></span>
<span data-ttu-id="fe31d-111">請遵循下列步驟來啟用 SQL 資料倉儲的 TDE：</span><span class="sxs-lookup"><span data-stu-id="fe31d-111">Follow these steps to enable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="fe31d-112">使用在 master 資料庫中做為系統管理員或 *dbmanager* 角色成員的登入，連接到裝載資料庫之伺服器上的 **master** 資料庫</span><span class="sxs-lookup"><span data-stu-id="fe31d-112">Connect to the *master* database on the server hosting the database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="fe31d-113">執行下列陳述式來加密資料庫。</span><span class="sxs-lookup"><span data-stu-id="fe31d-113">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="fe31d-114">停用加密</span><span class="sxs-lookup"><span data-stu-id="fe31d-114">Disabling Encryption</span></span>
<span data-ttu-id="fe31d-115">請遵循下列步驟來停用 SQL 資料倉儲的 TDE：</span><span class="sxs-lookup"><span data-stu-id="fe31d-115">Follow these steps to disable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="fe31d-116">使用在 master 資料庫中做為系統管理員或 *dbmanager* 角色成員的登入，連接到 **master** 資料庫</span><span class="sxs-lookup"><span data-stu-id="fe31d-116">Connect to the *master* database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="fe31d-117">執行下列陳述式來加密資料庫。</span><span class="sxs-lookup"><span data-stu-id="fe31d-117">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;
```

> [!NOTE]
> <span data-ttu-id="fe31d-118">變更 TDE 設定之前，必須先恢復暫停的 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="fe31d-118">A paused SQL Data Warehouse must be resumed before making changes to the TDE settings.</span></span>
> 
> 

## <a name="verifying-encryption"></a><span data-ttu-id="fe31d-119">確認加密</span><span class="sxs-lookup"><span data-stu-id="fe31d-119">Verifying Encryption</span></span>
<span data-ttu-id="fe31d-120">若要確認 SQL 資料倉儲的加密狀態，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="fe31d-120">To verify encryption status for a SQL Data Warehouse, follow the steps below:</span></span>

1. <span data-ttu-id="fe31d-121">使用在 master 資料庫中做為系統管理員或 *dbmanager* 角色成員的登入，連接到 **master** 或執行個體資料庫</span><span class="sxs-lookup"><span data-stu-id="fe31d-121">Connect to the *master* or instance database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="fe31d-122">執行下列陳述式來加密資料庫。</span><span class="sxs-lookup"><span data-stu-id="fe31d-122">Execute the following statement to encrypt the database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="fe31d-123">```1``` 的結果表示加密的資料庫，```0``` 表示未加密的資料庫。</span><span class="sxs-lookup"><span data-stu-id="fe31d-123">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

## <a name="encryption-dmvs"></a><span data-ttu-id="fe31d-124">加密 DMV</span><span class="sxs-lookup"><span data-stu-id="fe31d-124">Encryption DMVs</span></span>
* <span data-ttu-id="fe31d-125">[sys.databases][sys.databases]</span><span class="sxs-lookup"><span data-stu-id="fe31d-125">[sys.databases][sys.databases]</span></span> 
* <span data-ttu-id="fe31d-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="fe31d-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx  
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx  

<!--Image references-->

<!--Link references-->
