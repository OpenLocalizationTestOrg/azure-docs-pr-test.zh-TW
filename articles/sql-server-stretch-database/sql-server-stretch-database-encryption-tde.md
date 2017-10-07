---
title: "透明資料加密，以使用 Stretch Database-Azure aaaEnable |Microsoft 文件"
description: "為 Azure 上的 SQL Server Stretch Database 啟用透明資料加密 (TDE)"
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: barbkess
editor: 
ms.assetid: a44ed8f5-b416-4c41-9b1e-b7271f10bdc3
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2016
ms.author: douglasl
ms.openlocfilehash: 1d6bff455030ac8851b2184c1e8097afd61361d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a>為 Azure 上的 Stretch Database 啟用透明資料加密 (TDE)
> [!div class="op_single_selector"]
> * [Azure 入口網站](sql-server-stretch-database-encryption-tde.md)
> * [TSQL](sql-server-stretch-database-tde-tsql.md)
>
>

透明資料加密 (TDE) 可協助防範惡意活動的 hello 威脅，藉由執行 hello 資料庫、 相關聯的備份和靜止的交易記錄檔的即時加密與解密，而不需要變更 toohello應用程式。

TDE 會使用對稱金鑰的呼叫的 hello 資料庫加密金鑰將整個資料庫的 hello 儲存體。 hello 資料庫加密金鑰受到由內建的伺服器憑證。 hello 內建伺服器憑證是唯一的每個 Azure 伺服器。 Microsoft 至少每 90 天會自動替換這些憑證。 如需 TDE 的一般描述，請參閱 [透明資料加密 (TDE)]。

## <a name="enabling-encryption"></a>啟用加密
正在儲存從已啟用 Stretch 的 SQL Server 資料庫，移轉資料的 hello Azure 資料庫的 TDE tooenable hello 下列事項：

1. 開啟 hello 資料庫在 hello [Azure 入口網站](https://portal.azure.com)
2. 在 hello 資料庫刀鋒視窗中，按一下 hello**設定**按鈕
3. 選取 hello**透明資料加密**選項![][1]
4. 選取 hello**上**設定，然後再選取**儲存**
   ![][2]

## <a name="disabling-encryption"></a>停用加密
正在儲存從已啟用 Stretch 的 SQL Server 資料庫，移轉資料的 hello Azure 資料庫的 TDE toodisable hello 下列事項：

1. 開啟 hello 資料庫在 hello [Azure 入口網站](https://portal.azure.com)
2. 在 hello 資料庫刀鋒視窗中，按一下 hello**設定**按鈕
3. 選取 hello**透明資料加密**選項
4. 選取 hello**關閉**設定，然後再選取**儲存**

<!--Anchors-->
[透明資料加密 (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->
[1]: ./media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: ./media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->
