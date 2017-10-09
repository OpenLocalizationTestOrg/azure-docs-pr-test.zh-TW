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
# <a name="get-started-with-transparent-data-encryption-tde-in-sql-data-warehouse"></a>開始使用 SQL 資料倉儲中的透明資料加密 (TDE)
> [!div class="op_single_selector"]
> * [安全性概觀](sql-data-warehouse-overview-manage-security.md)
> * [驗證](sql-data-warehouse-authentication.md)
> * [加密 (入口網站)](sql-data-warehouse-encryption-tde.md)
> * [加密 (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a>需要的權限
tooenable 透明資料加密 (TDE)，您必須是系統管理員或 hello dbmanager 角色的成員。

## <a name="enabling-encryption"></a>啟用加密
tooenable TDE SQL 資料倉儲，請遵循下列 hello 步驟：

1. 開啟 hello 資料庫在 hello [Azure 入口網站](https://portal.azure.com)
2. 在 hello 資料庫刀鋒視窗中，按一下 hello**設定**按鈕
3. 選取 hello**透明資料加密**選項![][1]
4. 選取 hello**上**設定![][2]
5. 選取 [儲存]
   ![][3]  

## <a name="disabling-encryption"></a>停用加密
toodisable TDE SQL 資料倉儲，請遵循下列 hello 步驟：

1. 開啟 hello 資料庫在 hello [Azure 入口網站](https://portal.azure.com)
2. 在 hello 資料庫刀鋒視窗中，按一下 hello**設定**按鈕
3. 選取 hello**透明資料加密**選項![][1]
4. 選取 hello**關閉**設定![][4]
5. 選取 [儲存]
   ![][5]  

## <a name="encryption-dmvs"></a>加密 DMV
確認加密時，可以使用下列 Dmv 的 hello:

* [sys.databases]
* [sys.dm_pdw_nodes_database_encryption_keys]

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
