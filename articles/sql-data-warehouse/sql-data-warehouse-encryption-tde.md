---
title: "SQL 資料倉儲 （入口網站） 中的資料加密 aaaTransparent |Microsoft 文件"
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
ms.openlocfilehash: 8233886ecf170844104e0d1459e2a829cafa9b8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-transparent-data-encryption-tde-in-sql-data-warehouse"></a><span data-ttu-id="dbcde-103">開始使用 SQL 資料倉儲中的透明資料加密 (TDE)</span><span class="sxs-lookup"><span data-stu-id="dbcde-103">Get started with Transparent Data Encryption (TDE) in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dbcde-104">安全性概觀</span><span class="sxs-lookup"><span data-stu-id="dbcde-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="dbcde-105">驗證</span><span class="sxs-lookup"><span data-stu-id="dbcde-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="dbcde-106">加密 (入口網站)</span><span class="sxs-lookup"><span data-stu-id="dbcde-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="dbcde-107">加密 (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="dbcde-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="dbcde-108">需要的權限</span><span class="sxs-lookup"><span data-stu-id="dbcde-108">Required Permssions</span></span>
<span data-ttu-id="dbcde-109">tooenable 透明資料加密 (TDE)，您必須是系統管理員或 hello dbmanager 角色的成員。</span><span class="sxs-lookup"><span data-stu-id="dbcde-109">tooenable Transparent Data Encryption (TDE), you must be an administrator or a member of hello dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="dbcde-110">啟用加密</span><span class="sxs-lookup"><span data-stu-id="dbcde-110">Enabling Encryption</span></span>
<span data-ttu-id="dbcde-111">tooenable TDE SQL 資料倉儲，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="dbcde-111">tooenable TDE for a SQL Data Warehouse, follow hello steps below:</span></span>

1. <span data-ttu-id="dbcde-112">開啟 hello 資料庫在 hello [Azure 入口網站](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="dbcde-112">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="dbcde-113">在 hello 資料庫刀鋒視窗中，按一下 hello**設定**按鈕</span><span class="sxs-lookup"><span data-stu-id="dbcde-113">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="dbcde-114">選取 hello**透明資料加密**選項![][1]</span><span class="sxs-lookup"><span data-stu-id="dbcde-114">Select hello **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="dbcde-115">選取 hello**上**設定![][2]</span><span class="sxs-lookup"><span data-stu-id="dbcde-115">Select hello **On** setting ![][2]</span></span>
5. <span data-ttu-id="dbcde-116">選取 [儲存]
   ![][3]</span><span class="sxs-lookup"><span data-stu-id="dbcde-116">Select **Save**
![][3]</span></span>  

## <a name="disabling-encryption"></a><span data-ttu-id="dbcde-117">停用加密</span><span class="sxs-lookup"><span data-stu-id="dbcde-117">Disabling Encryption</span></span>
<span data-ttu-id="dbcde-118">toodisable TDE SQL 資料倉儲，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="dbcde-118">toodisable TDE for a SQL Data Warehouse, follow hello steps below:</span></span>

1. <span data-ttu-id="dbcde-119">開啟 hello 資料庫在 hello [Azure 入口網站](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="dbcde-119">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="dbcde-120">在 hello 資料庫刀鋒視窗中，按一下 hello**設定**按鈕</span><span class="sxs-lookup"><span data-stu-id="dbcde-120">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="dbcde-121">選取 hello**透明資料加密**選項![][1]</span><span class="sxs-lookup"><span data-stu-id="dbcde-121">Select hello **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="dbcde-122">選取 hello**關閉**設定![][4]</span><span class="sxs-lookup"><span data-stu-id="dbcde-122">Select hello **Off** setting ![][4]</span></span>
5. <span data-ttu-id="dbcde-123">選取 [儲存]
   ![][5]</span><span class="sxs-lookup"><span data-stu-id="dbcde-123">Select **Save**
![][5]</span></span>  

## <a name="encryption-dmvs"></a><span data-ttu-id="dbcde-124">加密 DMV</span><span class="sxs-lookup"><span data-stu-id="dbcde-124">Encryption DMVs</span></span>
<span data-ttu-id="dbcde-125">確認加密時，可以使用下列 Dmv 的 hello:</span><span class="sxs-lookup"><span data-stu-id="dbcde-125">Encryption can be confirmed with hello following DMVs:</span></span>

* <span data-ttu-id="dbcde-126">[sys.databases]</span><span class="sxs-lookup"><span data-stu-id="dbcde-126">[sys.databases]</span></span>
* <span data-ttu-id="dbcde-127">[sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="dbcde-127">[sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--MSDN references-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings.png
[2]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-on.png
[3]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save.png
[4]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-off.png
[5]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save2.png

<!--Link references-->
