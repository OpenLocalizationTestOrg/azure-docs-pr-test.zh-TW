---
title: "aaaCreate 和管理適用於使用 Azure 入口網站的 MySQL 伺服器的 Azure 資料庫 |Microsoft 文件"
description: "本文說明如何快速建立新的 Azure 資料庫的 MySQL server 和管理使用 hello Azure 入口網站的 hello 伺服器。"
services: mysql
author: v-chenyh
ms.author: nolanwu
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: c532df43b3d2124d7bd34875b32d52357f162af8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-server-using-azure-portal"></a>使用 Azure 入口網站建立和管理適用於 MySQL 的 Azure 資料庫伺服器
本文說明如何快速建立新的 Azure 資料庫的 MySQL server 和管理使用 hello Azure 入口網站的 hello 伺服器。 伺服器管理包括檢視伺服器詳細資料 （& s） 資料庫、 重設密碼和刪除 hello 伺服器。

## <a name="log-in-toohello-azure-portal"></a>登入 toohello Azure 入口網站
登入 toohello [Azure 入口網站](https://portal.azure.com)。

## <a name="create-an-azure-database-for-mysql-server"></a>建立適用於 MySQL 的 Azure 資料庫伺服器
請遵循這些步驟 toocreate 名為"mysqlserver4demo"MySQL 伺服器的 Azure 資料庫

1-按一下**新增**hello 的左上角 hello Azure 入口網站上找到的按鈕。

2-選取**資料庫**hello 新頁面上，然後選取從**Azure 資料庫的 MySQL**從 hello 資料庫頁面。

> 建立的「適用於 MySQL 的 Azure 資料庫」伺服器會有一組已定義的[計算和儲存體](./concepts-compute-unit-and-storage.md)資源。 hello 資料庫會建立在 Azure 資源群組和 Azure 資料庫的 MySQL 伺服器。

![建立新的伺服器](./media/howto-create-manage-server-portal/create-new-server.png)

3-填寫 hello Azure 資料庫的 MySQL 表單以 hello 下列資訊：

| **表單欄位** | **欄位描述** |
|----------------|-----------------------|
| *伺服器名稱* | azure-mysql (伺服器名稱是全域唯一的) |
| *訂用帳戶* | MySQLaaS (從下拉式清單選取) |
| *資源群組* | myresource (建立新的資源群組，或使用現有的資源群組) |
| 伺服器管理員登入 | myadmin (設定管理帳戶名稱) |
| *密碼* | 設定管理帳戶密碼 |
| *確認密碼* | 確認管理帳戶密碼 |
| *位置* | 北歐 (選取北歐或美國西部) |
| *版本* | 5.6 (選擇適用於 MySQL 的 Azure 資料庫伺服器版本) |

4 按一下**定價層**toospecify hello 服務層和效能層級為您新的伺服器。 在基本層，計算單位可以設定在 50 到 100 之間，而在標準層，則可以設定在 100 到 200 之間，還可根據加入的數量來新增儲存體。 在本作法指南中，我們選擇 50 計算單位和 50GB。 按一下**確定**toosave 選取項目。
![建立伺服器定價層](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)

5 按一下**建立**tooprovision hello 伺服器。 佈建需要幾分鐘的時間。

> 檢查 hello **Pin toodashboard**選項 tooallow 輕鬆追蹤您的部署。
> [!NOTE]
> 雖然在基本層 too1000GB 和 10000 GB 標準層將會支援存放裝置，對於公開預覽，hello 最大儲存體是暫時仍會限制的 too1000GB。 
</Include>

## <a name="update-an-azure-database-for-mysql-server"></a>更新適用於 MySQL 的 Azure 資料庫伺服器
新的伺服器已佈建之後，使用者會有 2 選項 tooedit 現有的伺服器： 重設管理員密碼或小數位數向上/向下 hello 伺服器變更 hello 計算單位。

### <a name="change-hello-administrator-user-password"></a>變更 hello 系統管理員使用者密碼
1-hello 伺服器上**概觀**刀鋒視窗中，按一下 **重設密碼**toopopulate 密碼輸入和確認視窗。

2-輸入新密碼並確認 hello 密碼在 hello 視窗中，如下所示：![重設密碼](./media/howto-create-manage-server-portal/reset-password.png)

3-按一下**確定**toosave hello 新密碼。

### <a name="scale-updown-by-changing-compute-units"></a>變更計算單位以相應增加/減少

1-在 hello 伺服器刀鋒視窗中，在**設定**，按一下 **定價層**tooopen hello 定價層刀鋒視窗中的 hello Azure 資料庫的 MySQL 伺服器。

2 後續步驟 4 中的**建立 MySQL 伺服器的 Azure 資料庫**toochange 計算單位 hello 相同定價層。

## <a name="delete-an-azure-database-for-mysql-server"></a>刪除適用於 MySQL 的 Azure 資料庫伺服器

1-hello 伺服器上**概觀**刀鋒視窗中，按一下 **刪除**命令按鈕 tooopen hello 刪除確認刀鋒視窗。

Double 確認 hello 刀鋒視窗的輸入方塊中的 2 類型 hello 正確的伺服器名稱。

3-按一下**刪除**按鈕再次 tooconfirm 刪除動作，然後等候 hello 通知列的 「 刪除成功 」 的快顯視窗。

## <a name="list-hello-azure-database-for-mysql-databases"></a>清單 hello Azure 資料庫的 MySQL 資料庫
Hello 伺服器上**概觀**刀鋒視窗中，向下捲動直到您看到 hello 資料庫並排顯示 hello 下方。 所有的 hello 資料庫將列在 hello 資料表中。 按一下**刪除**命令按鈕 tooopen hello 刪除確認刀鋒視窗。

![顯示資料庫](./media/howto-create-manage-server-portal/show-databases.png)

## <a name="show-details-of-an-azure-database-for-mysql-server"></a>顯示「適用於 MySQL 的 Azure 資料庫」伺服器的詳細資料
按一下**屬性**下**設定**hello 伺服器刀鋒視窗會開啟 hello**屬性**刀鋒視窗。 然後您可以檢視有關 hello 伺服器的所有詳細的資訊。

## <a name="next-steps"></a>後續步驟

[快速入門：使用 Azure 入口網站建立適用於 MySQL 的 Azure 資料庫伺服器](./quickstart-create-mysql-server-database-using-azure-portal.md)
