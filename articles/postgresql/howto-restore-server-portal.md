---
title: "如何在適用於 PostgreSQL 的 Azure 資料庫中還原伺服器 | Microsoft Docs"
description: "本文說明如何使用 Azure 入口網站，在適用於 PostgreSQL 的 Azure 資料庫中還原伺服器。"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 11/03/2017
ms.openlocfilehash: 903fd2ff446e1963ab5cfcec745766188b74efcf
ms.sourcegitcommit: 38c9176c0c967dd641d3a87d1f9ae53636cf8260
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/06/2017
---
# <a name="how-to-backup-and-restore-a-server-in-azure-database-for-postgresql-using-the-azure-portal"></a>如何使用 Azure 入口網站，在適用於 PostgreSQL 的 Azure 資料庫中備份和還原伺服器

## <a name="backup-happens-automatically"></a>備份會自動進行
使用適用於 PostgreSQL 的 Azure 資料庫時，資料庫服務每隔 5 分鐘會自動備份一次伺服器。 

使用基本層時，備份會保留 7 天，而使用標準層時會保留 35 天。 如需詳細資訊，請參閱[適用於 PostgreSQL 的 Azure 資料庫服務層](concepts-service-tiers.md)

透過這個自動備份功能，您可以將伺服器和其所有資料庫還原至新的伺服器，而且還原至更早的時間點。

## <a name="restore-in-the-azure-portal"></a>在 Azure 入口網站中還原
適用於 PostgreSQL 的 Azure 資料庫可讓您將伺服器還原至過去的時間點，並還原至新的伺服器複本。 您可以使用這個新的伺服器復原資料。 

比方說，如果今天中午不小心卸除資料表，您可以還原至中午之前的時刻，然後從該新的伺服器複本擷取遺漏的資料表和資料。

下列步驟會將範例伺服器還原至某個時間點︰
1. 登入 [Azure 入口網站](https://portal.azure.com/)
2. 找出您的「適用於 PostgreSQL 的 Azure 資料庫」伺服器。 在 Azure 入口網站中，從左側功能表按一下 [所有資源]，然後輸入伺服器的名稱搜尋現有的伺服器，例如 **mypgserver-20170401**。 按一下搜尋結果中列出的伺服器名稱。 伺服器的 [概觀] 頁面隨即開啟，並提供可進一步設定的選項。

   ![Azure 入口網站 - 搜尋找出您的伺服器](media/postgresql-howto-restore-server-portal/1-locate.png)

3. 在伺服器概觀分頁的工具列上，按一下 [還原]。 [還原] 頁面隨即開啟。

   ![適用於 PostgreSQL 的 Azure 資料庫 - 概觀 - 還原按鈕](./media/postgresql-howto-restore-server-portal/2_server.png)

4. 在 [還原] 表單中填入必要資訊︰

   ![適用於 PostgreSQL 的 Azure 資料庫 - 還原資訊 ](./media/postgresql-howto-restore-server-portal/3_restore.png)
  - **還原點**：選取在變更伺服器之前的時間點。
  - **目標伺服器**︰提供要作為還原目的地的新伺服器名稱。
  - **位置**：您無法選取區域。 它預設與來源伺服器相同。
  - **定價層**︰還原伺服器時，您無法變更此值。 它與來源伺服器相同。 

5. 按一下 [確定] 將伺服器還原至某個時間點。 

6. 完成還原時，找出已建立的新伺服器，確認資料如預期般還原。

## <a name="next-steps"></a>後續步驟
- [「適用於 PostgreSQL 的 Azure 資料庫」的連線庫](concepts-connection-libraries.md)
