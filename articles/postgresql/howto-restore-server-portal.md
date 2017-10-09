---
title: "如何 tooRestore Azure PostgreSQL 資料庫中的伺服器 |Microsoft 文件"
description: "本文說明如何 toorestore Azure Database 中的伺服器使用 PostgreSQL hello Azure 入口網站。"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/20/2017
ms.openlocfilehash: bc7351f384607397806d837afd3e1d7a26575e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-postgresql-using-hello-azure-portal"></a>TooBackup 和還原 Azure 資料庫中的伺服器使用 PostgreSQL hello Azure 入口網站

## <a name="backup-happens-automatically"></a>備份會自動進行
當使用 Azure 資料庫的 PostgreSQL，hello 資料庫服務會自動將 hello 服務的備份每隔 5 分鐘。 

hello 備份時，可以使用 7 天內使用基本層次中，則為 35 天使用標準層時。 如需詳細資訊，請參閱[適用於 PostgreSQL 的 Azure 資料庫服務層](concepts-service-tiers.md)

使用這個自動備份功能您可能會到新伺服器 tooan 稍早的時間點還原 hello 伺服器及其所有資料庫。

## <a name="restore-in-hello-azure-portal"></a>將還原的 hello Azure 入口網站
Azure PostgreSQL 資料庫可讓您 toorestore hello 伺服器回復 tooa 點的時間，並置於 tooa hello 伺服器新複本。 您可以使用這個新的伺服器 toorecover 您的資料。 

比方說，如果資料表已意外卸除正午現在，您無法還原 toohello 正午之前的時間，擷取 hello 遺漏的資料表和資料從 hello 伺服器的新複本。

hello 下列的步驟還原 hello 範例伺服器 tooa 點時間：
1. 登入 hello [Azure 入口網站](https://portal.azure.com/)
2. 找出您的「適用於 PostgreSQL 的 Azure 資料庫」伺服器。 在 hello Azure 入口網站，按一下**所有資源**從 hello 左側功能表，然後輸入 hello 名稱，例如**mypgserver 20170401**，toosearch 您現有的伺服器。 按一下 hello hello 搜尋結果中所列的伺服器名稱。 hello**概觀**頁面會針對您的伺服器會開啟，並提供進一步組態的選項。

   ![Azure 入口網站-搜尋 toolocate 您的伺服器](media/postgresql-howto-restore-server-portal/1-locate.png)

3. 在 hello hello 伺服器概觀刀鋒視窗頂端，按一下 **還原**hello 工具列上。 hello 還原刀鋒視窗隨即開啟。

   ![適用於 PostgreSQL 的 Azure 資料庫 - 概觀 - 還原按鈕](./media/postgresql-howto-restore-server-portal/2_server.png)

4. 填寫 hello 還原表單 hello 所需的資訊：

   ![適用於 PostgreSQL 的 Azure 資料庫 - 還原資訊 ](./media/postgresql-howto-restore-server-portal/3_restore.png)
  - **還原點**： 選取在時間點所發生之前 hello 伺服器已變更
  - **目標伺服器**： 提供新的伺服器名稱，您想要 toorestore
  - **位置**： 您無法選取 hello 區域，依預設它是與 hello 來源伺服器相同
  - **定價層**︰還原伺服器時，您無法變更此值。 它是與 hello 來源伺服器相同。 

5. 按一下**確定**toorestore hello 伺服器 toorestore tooa 時間點。 

6. 一旦 hello 還原完成時，找出 hello 建立 tooverify hello 如預期般，已還原資料的新伺服器。

## <a name="next-steps"></a>後續步驟
- [「適用於 PostgreSQL 的 Azure 資料庫」的連線庫](concepts-connection-libraries.md)
