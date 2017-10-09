---
title: "aaaHow tooRestore MySQL 的 Azure 資料庫中的伺服器 |Microsoft 文件"
description: "本文說明如何 toorestore Azure Database 中的伺服器使用 MySQL hello Azure 入口網站。"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4b990d5b37c5d4924de9571192b923e3c81094ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-mysql-using-hello-azure-portal"></a>TooBackup 和還原 Azure 資料庫中的伺服器使用 MySQL hello Azure 入口網站

## <a name="backup-happens-automatically"></a>備份會自動進行
當使用 Azure 資料庫的 MySQL，hello 資料庫服務會自動將 hello 服務的備份每隔 5 分鐘。 

hello 備份時，可以使用 7 天內使用基本層次中，則為 35 天使用標準層時。 如需詳細資訊，請參閱[適用於 MySQL 的 Azure 資料庫服務層](concepts-service-tiers.md)

使用這個自動備份功能您可能會到新伺服器 tooan 稍早的時間點還原 hello 伺服器及其所有資料庫。

## <a name="restore-in-hello-azure-portal"></a>將還原的 hello Azure 入口網站
Azure 的 MySQL 資料庫可讓您 toorestore hello 伺服器回復 tooa 點的時間，並置於 tooa hello 伺服器新複本。 您可以使用這個新的伺服器 toorecover 您的資料。 

比方說，如果資料表已意外卸除正午現在，您無法還原 toohello 正午之前的時間，擷取 hello 遺漏的資料表和資料從 hello 伺服器的新複本。

hello 下列的步驟還原 hello 範例伺服器 tooa 點時間：

1. 登入 hello [Azure 入口網站](https://portal.azure.com/)

2. 找出適用於 MySQL 的 Azure 資料庫伺服器。 Hello 左窗格中，選取**所有資源**，然後從 hello 清單中選取您的伺服器。

3.  在 hello hello 伺服器概觀刀鋒視窗頂端，按一下 **還原**hello 工具列上。 hello 還原刀鋒視窗隨即開啟。
![按一下 [還原] 按鈕](./media/howto-restore-server-portal/click-restore-button.png)

4. 填寫 hello 還原表單 hello 所需的資訊：

- **還原點 (UTC)**： 使用 hello 日期選擇器和時間選擇器，選取時間點 toorestore 至。 指定的 hello 時間是 UTC 格式，因此您可能需要 tooconvert hello 本地時間到 UTC。
- **還原 toonew 伺服器**： 提供新的伺服器名稱 toorestore hello 現有伺服器。
- **位置**: hello 區域選擇自動填入 hello 來源伺服器的地區，而且無法變更。
- **定價層**: hello 定價層選擇自動填入的 hello 相同定價層為 hello 來源伺服器，並無法在此進行變更。 
![PITR 還原](./media/howto-restore-server-portal/pitr-restore.png)

5. 按一下**確定**toorestore hello 伺服器 toorestore tooa 時間點。 

6. Hello 還原完成後，找出已建立的資料庫已還原，如預期般 tooverify hello 的 hello 新伺服器。

## <a name="next-steps"></a>後續步驟
- [適用於 MySQL 的 Azure 資料庫的連線庫](concepts-connection-libraries.md)