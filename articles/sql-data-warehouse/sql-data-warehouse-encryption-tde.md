---
title: "SQL 資料倉儲中的透明資料加密 (入口網站) | Microsoft Docs"
description: "SQL 資料倉儲中的透明資料加密 (TDE)"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: fabf75d3-9bbf-4e0d-9b31-8b5a8713f08d
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: b1db3bdfdfb54bda325c9b971cfcb4dd5efa333a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-transparent-data-encryption-tde-in-sql-data-warehouse"></a><span data-ttu-id="93e02-103">開始使用 SQL 資料倉儲中的透明資料加密 (TDE)</span><span class="sxs-lookup"><span data-stu-id="93e02-103">Get started with Transparent Data Encryption (TDE) in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="93e02-104">安全性概觀</span><span class="sxs-lookup"><span data-stu-id="93e02-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="93e02-105">驗證</span><span class="sxs-lookup"><span data-stu-id="93e02-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="93e02-106">加密 (入口網站)</span><span class="sxs-lookup"><span data-stu-id="93e02-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="93e02-107">加密 (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="93e02-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="93e02-108">需要的權限</span><span class="sxs-lookup"><span data-stu-id="93e02-108">Required Permssions</span></span>
<span data-ttu-id="93e02-109">您必須是系統管理員或 dbmanager 角色的成員，才能啟用透明資料加密 (TDE)。</span><span class="sxs-lookup"><span data-stu-id="93e02-109">To enable Transparent Data Encryption (TDE), you must be an administrator or a member of the dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="93e02-110">啟用加密</span><span class="sxs-lookup"><span data-stu-id="93e02-110">Enabling Encryption</span></span>
<span data-ttu-id="93e02-111">若要啟用 SQL 資料倉儲的 TDE，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="93e02-111">To enable TDE for a SQL Data Warehouse, follow the steps below:</span></span>

1. <span data-ttu-id="93e02-112">在 [Azure 入口網站](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="93e02-112">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="93e02-113">在資料庫刀鋒視窗中，按一下 [設定]  按鈕</span><span class="sxs-lookup"><span data-stu-id="93e02-113">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="93e02-114">選取 [透明資料加密]  選項 ![][1]</span><span class="sxs-lookup"><span data-stu-id="93e02-114">Select the **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="93e02-115">選取 [開啟] 設定 ![][2]</span><span class="sxs-lookup"><span data-stu-id="93e02-115">Select the **On** setting ![][2]</span></span>
5. <span data-ttu-id="93e02-116">選取 [儲存]
   ![][3]</span><span class="sxs-lookup"><span data-stu-id="93e02-116">Select **Save**
![][3]</span></span>  

## <a name="disabling-encryption"></a><span data-ttu-id="93e02-117">停用加密</span><span class="sxs-lookup"><span data-stu-id="93e02-117">Disabling Encryption</span></span>
<span data-ttu-id="93e02-118">若要停用 SQL 資料倉儲的 TDE，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="93e02-118">To disable TDE for a SQL Data Warehouse, follow the steps below:</span></span>

1. <span data-ttu-id="93e02-119">在 [Azure 入口網站](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="93e02-119">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="93e02-120">在資料庫刀鋒視窗中，按一下 [設定]  按鈕</span><span class="sxs-lookup"><span data-stu-id="93e02-120">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="93e02-121">選取 [透明資料加密]  選項 ![][1]</span><span class="sxs-lookup"><span data-stu-id="93e02-121">Select the **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="93e02-122">選取 [關閉] 設定 ![][4]</span><span class="sxs-lookup"><span data-stu-id="93e02-122">Select the **Off** setting ![][4]</span></span>
5. <span data-ttu-id="93e02-123">選取 [儲存]
   ![][5]</span><span class="sxs-lookup"><span data-stu-id="93e02-123">Select **Save**
![][5]</span></span>  

## <a name="encryption-dmvs"></a><span data-ttu-id="93e02-124">加密 DMV</span><span class="sxs-lookup"><span data-stu-id="93e02-124">Encryption DMVs</span></span>
<span data-ttu-id="93e02-125">可以使用下列 DMW 來確認加密：</span><span class="sxs-lookup"><span data-stu-id="93e02-125">Encryption can be confirmed with the following DMVs:</span></span>

* <span data-ttu-id="93e02-126">[sys.databases]</span><span class="sxs-lookup"><span data-stu-id="93e02-126">[sys.databases]</span></span>
* <span data-ttu-id="93e02-127">[sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="93e02-127">[sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--MSDN references-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
<span data-ttu-id="93e02-128">[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx</span><span class="sxs-lookup"><span data-stu-id="93e02-128">[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx</span></span>
<span data-ttu-id="93e02-129">[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx</span><span class="sxs-lookup"><span data-stu-id="93e02-129">[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx</span></span>

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings.png
[2]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-on.png
[3]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save.png
[4]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-off.png
[5]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save2.png

<!--Link references-->
