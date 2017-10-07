---
title: "aaaManage 的計算能力，在 Azure SQL 資料倉儲 （Azure 入口網站） |Microsoft 文件"
description: "Azure 入口網站工作 toomanage 運算能力。 透過調整 DWU 以調整計算資源。 或者，您也可以暫停和繼續計算資源 toosave 成本。"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 233b0da5-4abd-4d1d-9586-4ccc5f50b071
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: b2e84b3763e97ce88c190eecfb64b2d06f727229
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-azure-portal"></a>管理 Azure SQL 資料倉儲中的計算能力 (Azure 入口網站)
> [!div class="op_single_selector"]
> * [概觀](sql-data-warehouse-manage-compute-overview.md)
> * [入口網站](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>


## <a name="scale-compute-power"></a>調整計算能力
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

toochange 計算資源：

1. 開啟 hello [Azure 入口網站][Azure portal]，開啟您的資料庫，然後按一下**標尺**。

    ![按一下 [調整]][1]
2. 在 hello 小數位數 刀鋒視窗中，移動 hello 滑桿向左或向右 toochange hello DWU 設定。

    ![移動滑桿][2]
3. 按一下 [儲存] 。 確認訊息隨即出現。 按一下**是**tooconfirm 或**沒有**toocancel。

    ![按一下 [Save] \(儲存)。][3]

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a>暫停計算
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

toopause 資料庫：

1. 開啟 hello [Azure 入口網站][ Azure portal]並開啟您的資料庫。 請注意該狀態的 hello**線上**。

    ![線上狀態][6]
2. 按一下 toosuspend 運算和記憶體資源，**暫停**，和就會顯示確認訊息。 按一下**是**tooconfirm 或**沒有**toocancel。

    ![確認暫停][7]
3. SQL 資料倉儲啟動 hello 資料庫時，hello 狀態即**暫停**。
4. Hello 狀態時**暫停**hello 暫停作業完成，您無法再所負責的 Dwu。

    ![暫停狀態][4]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a>繼續計算
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

tooresume 資料庫：

1. 開啟 hello [Azure 入口網站][ Azure portal]並開啟您的資料庫。 請注意該狀態的 hello**暫停**。

    ![暫停資料庫][4]
2. tooresume hello 資料庫按一下**啟動**，並就會顯示確認訊息。 按一下**是**tooconfirm 或**沒有**toocancel。

    ![確認繼續][5]
3. SQL 資料倉儲啟動 hello 資料庫時，hello 狀態即 「 繼續 」。
4. Hello 狀態時**線上**，hello 資料庫就緒。

    ![線上狀態][6]

<a name="next-steps-bk"></a>

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱[管理概觀][Management overview]。

<!--Image references-->
[1]: ./media/sql-data-warehouse-manage-compute-portal/click-scale.png
[2]: ./media/sql-data-warehouse-manage-compute-portal/move-slider.png
[3]: ./media/sql-data-warehouse-manage-compute-portal/click-save.png
[4]: ./media/sql-data-warehouse-manage-compute-portal/resume-database.png
[5]: ./media/sql-data-warehouse-manage-compute-portal/resume-confirm.png
[6]: ./media/sql-data-warehouse-manage-compute-portal/pause-database.png
[7]: ./media/sql-data-warehouse-manage-compute-portal/pause-confirm.png

<!--Article references-->
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
