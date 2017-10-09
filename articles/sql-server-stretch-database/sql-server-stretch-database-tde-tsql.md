---
title: "透明資料加密，為 Stretch Database TSQL Azure aaaEnable |Microsoft 文件"
description: "為 Azure TSQL 上的 SQL Server Stretch Database 啟用透明資料加密 (TDE)"
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: jhubbard
editor: 
ms.assetid: 27753d91-9ca2-4d47-b34d-b5e2c2f029bb
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: anvang
ms.openlocfilehash: a9ba23649656fb344480d79438a1115f0eb353bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure-transact-sql"></a><span data-ttu-id="82ee6-103">為 Azure 上的 Stretch Database 啟用透明資料加密 (TDE) (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="82ee6-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure (Transact-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="82ee6-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="82ee6-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="82ee6-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="82ee6-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="82ee6-106">透明資料加密 (TDE) 可協助防範惡意活動的 hello 威脅，藉由執行 hello 資料庫、 相關聯的備份和靜止的交易記錄檔的即時加密與解密，而不需要變更 toohello應用程式。</span><span class="sxs-lookup"><span data-stu-id="82ee6-106">Transparent Data Encryption (TDE) helps protect against hello threat of malicious activity by performing real-time encryption and decryption of hello database, associated backups, and transaction log files at rest without requiring changes toohello application.</span></span>

<span data-ttu-id="82ee6-107">TDE 會使用對稱金鑰的呼叫的 hello 資料庫加密金鑰將整個資料庫的 hello 儲存體。</span><span class="sxs-lookup"><span data-stu-id="82ee6-107">TDE encrypts hello storage of an entire database by using a symmetric key called hello database encryption key.</span></span> <span data-ttu-id="82ee6-108">hello 資料庫加密金鑰受到由內建的伺服器憑證。</span><span class="sxs-lookup"><span data-stu-id="82ee6-108">hello database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="82ee6-109">hello 內建伺服器憑證是唯一的每個 Azure 伺服器。</span><span class="sxs-lookup"><span data-stu-id="82ee6-109">hello built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="82ee6-110">Microsoft 至少每 90 天會自動替換這些憑證。</span><span class="sxs-lookup"><span data-stu-id="82ee6-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="82ee6-111">如需 TDE 的一般描述，請參閱 [透明資料加密 (TDE)]。</span><span class="sxs-lookup"><span data-stu-id="82ee6-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="82ee6-112">啟用加密</span><span class="sxs-lookup"><span data-stu-id="82ee6-112">Enabling Encryption</span></span>
<span data-ttu-id="82ee6-113">正在儲存從已啟用 Stretch 的 SQL Server 資料庫，移轉資料的 hello Azure 資料庫的 TDE tooenable hello 下列事項：</span><span class="sxs-lookup"><span data-stu-id="82ee6-113">tooenable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="82ee6-114">連接 toohello*主要*hello Azure 伺服器主控 hello 資料庫上使用的登入是系統管理員或成員的 hello 資料庫**dbmanager** hello master 資料庫中的角色</span><span class="sxs-lookup"><span data-stu-id="82ee6-114">Connect toohello *master* database on hello Azure server hosting hello database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="82ee6-115">執行下列陳述式 tooencrypt hello 資料庫 hello。</span><span class="sxs-lookup"><span data-stu-id="82ee6-115">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="82ee6-116">停用加密</span><span class="sxs-lookup"><span data-stu-id="82ee6-116">Disabling Encryption</span></span>
<span data-ttu-id="82ee6-117">正在儲存從已啟用 Stretch 的 SQL Server 資料庫，移轉資料的 hello Azure 資料庫的 TDE toodisable hello 下列事項：</span><span class="sxs-lookup"><span data-stu-id="82ee6-117">toodisable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="82ee6-118">連接 toohello*主要*資料庫使用的登入是系統管理員或成員的 hello **dbmanager** hello master 資料庫中的角色</span><span class="sxs-lookup"><span data-stu-id="82ee6-118">Connect toohello *master* database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="82ee6-119">執行下列陳述式 tooencrypt hello 資料庫 hello。</span><span class="sxs-lookup"><span data-stu-id="82ee6-119">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION OFF;
```

## <a name="verifying-encryption"></a><span data-ttu-id="82ee6-120">確認加密</span><span class="sxs-lookup"><span data-stu-id="82ee6-120">Verifying Encryption</span></span>
<span data-ttu-id="82ee6-121">正在儲存從已啟用 Stretch 的 SQL Server 資料庫，移轉資料的 hello Azure 資料庫 tooverify 加密的狀態 hello 下列事項：</span><span class="sxs-lookup"><span data-stu-id="82ee6-121">tooverify encryption status for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="82ee6-122">連接 toohello*主要*或執行個體資料庫使用的登入是系統管理員或成員的 hello **dbmanager** hello master 資料庫中的角色</span><span class="sxs-lookup"><span data-stu-id="82ee6-122">Connect toohello *master* or instance database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="82ee6-123">執行下列陳述式 tooencrypt hello 資料庫 hello。</span><span class="sxs-lookup"><span data-stu-id="82ee6-123">Execute hello following statement tooencrypt hello database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="82ee6-124">```1``` 的結果表示加密的資料庫，```0``` 表示未加密的資料庫。</span><span class="sxs-lookup"><span data-stu-id="82ee6-124">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

<!--Anchors-->
[透明資料加密 (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->

<!--Link references-->
