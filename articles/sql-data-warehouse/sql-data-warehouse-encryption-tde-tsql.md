---
title: "SQL 資料倉儲 (T-SQL) 中的資料加密 aaaTransparent |Microsoft 文件"
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
ms.openlocfilehash: 3894431c76f14b217f3a6b9a42dbf2f4d216bad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-transparent-data-encryption-tde"></a><span data-ttu-id="b235d-103">開始使用透明資料加密 (TDE)</span><span class="sxs-lookup"><span data-stu-id="b235d-103">Get started with Transparent Data Encryption (TDE)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b235d-104">安全性概觀</span><span class="sxs-lookup"><span data-stu-id="b235d-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="b235d-105">驗證</span><span class="sxs-lookup"><span data-stu-id="b235d-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="b235d-106">加密 (入口網站)</span><span class="sxs-lookup"><span data-stu-id="b235d-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="b235d-107">加密 (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="b235d-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="b235d-108">需要的權限</span><span class="sxs-lookup"><span data-stu-id="b235d-108">Required Permssions</span></span>
<span data-ttu-id="b235d-109">tooenable 透明資料加密 (TDE)，您必須是系統管理員或 hello dbmanager 角色的成員。</span><span class="sxs-lookup"><span data-stu-id="b235d-109">tooenable Transparent Data Encryption (TDE), you must be an administrator or a member of hello dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="b235d-110">啟用加密</span><span class="sxs-lookup"><span data-stu-id="b235d-110">Enabling Encryption</span></span>
<span data-ttu-id="b235d-111">SQL 資料倉儲，請遵循這些步驟 tooenable TDE:</span><span class="sxs-lookup"><span data-stu-id="b235d-111">Follow these steps tooenable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="b235d-112">連接 toohello*主要*裝載 hello 資料庫使用的登入是系統管理員或成員的 hello 的 hello 伺服器上的資料庫**dbmanager** hello master 資料庫中的角色</span><span class="sxs-lookup"><span data-stu-id="b235d-112">Connect toohello *master* database on hello server hosting hello database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="b235d-113">執行下列陳述式 tooencrypt hello 資料庫 hello。</span><span class="sxs-lookup"><span data-stu-id="b235d-113">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="b235d-114">停用加密</span><span class="sxs-lookup"><span data-stu-id="b235d-114">Disabling Encryption</span></span>
<span data-ttu-id="b235d-115">SQL 資料倉儲，請遵循這些步驟 toodisable TDE:</span><span class="sxs-lookup"><span data-stu-id="b235d-115">Follow these steps toodisable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="b235d-116">連接 toohello*主要*資料庫使用的登入是系統管理員或成員的 hello **dbmanager** hello master 資料庫中的角色</span><span class="sxs-lookup"><span data-stu-id="b235d-116">Connect toohello *master* database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="b235d-117">執行下列陳述式 tooencrypt hello 資料庫 hello。</span><span class="sxs-lookup"><span data-stu-id="b235d-117">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;
```

> [!NOTE]
> <span data-ttu-id="b235d-118">Toohello TDE 設定進行變更之前，必須繼續暫停的 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="b235d-118">A paused SQL Data Warehouse must be resumed before making changes toohello TDE settings.</span></span>
> 
> 

## <a name="verifying-encryption"></a><span data-ttu-id="b235d-119">確認加密</span><span class="sxs-lookup"><span data-stu-id="b235d-119">Verifying Encryption</span></span>
<span data-ttu-id="b235d-120">SQL 資料倉儲，tooverify 加密的狀態，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="b235d-120">tooverify encryption status for a SQL Data Warehouse, follow hello steps below:</span></span>

1. <span data-ttu-id="b235d-121">連接 toohello*主要*或執行個體資料庫使用的登入是系統管理員或成員的 hello **dbmanager** hello master 資料庫中的角色</span><span class="sxs-lookup"><span data-stu-id="b235d-121">Connect toohello *master* or instance database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="b235d-122">執行下列陳述式 tooencrypt hello 資料庫 hello。</span><span class="sxs-lookup"><span data-stu-id="b235d-122">Execute hello following statement tooencrypt hello database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="b235d-123">```1``` 的結果表示加密的資料庫，```0``` 表示未加密的資料庫。</span><span class="sxs-lookup"><span data-stu-id="b235d-123">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

## <a name="encryption-dmvs"></a><span data-ttu-id="b235d-124">加密 DMV</span><span class="sxs-lookup"><span data-stu-id="b235d-124">Encryption DMVs</span></span>
* <span data-ttu-id="b235d-125">[sys.databases][sys.databases]</span><span class="sxs-lookup"><span data-stu-id="b235d-125">[sys.databases][sys.databases]</span></span> 
* <span data-ttu-id="b235d-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="b235d-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx  
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx  

<!--Image references-->

<!--Link references-->
