---
title: "aaaCreate 和管理 Azure 資料庫的 MySQL 使用 hello Azure 入口網站的防火牆規則 |Microsoft 文件"
description: "建立和管理 Azure 資料庫的 MySQL 使用 hello Azure 入口網站的防火牆規則"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 30dbdde4299df564fbf6581419e908186fe3b823
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-hello-azure-portal"></a>建立和管理 Azure 資料庫的 MySQL 使用 hello Azure 入口網站的防火牆規則
伺服器層級防火牆規則可讓系統管理員 tooaccess Azure 資料庫的 MySQL 伺服器從指定的 IP 位址或 IP 位址範圍。 

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>在 hello Azure 入口網站中建立伺服器層級防火牆規則

1. Hello MySQL 伺服器 刀鋒視窗，設定下標題之下，按一下**連線安全性**tooopen hello 連線安全性刀鋒視窗中的 hello Azure MySQL 資料庫。

   ![Azure 入口網站 - 按一下 [連線安全性]](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. 按一下**加入我的 IP**上 hello 工具列 toocreate hello IP 位址的電腦，因為看得見 hello Azure 系統的規則。

   ![Azure 入口網站 - 按一下 [新增我的 IP]](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. 儲存 hello 組態之前，請確認您的 IP 位址。 在某些情況下，Azure 入口網站所觀察到的 hello IP 位址與 hello 所使用的 IP 位址時存取 hello 網際網路和 Azure 的伺服器。 因此，您可能需要 toochange hello 起始 IP 和結束 IP toomake hello 規則運作不如預期。

   使用搜尋引擎或其他線上工具 toocheck 您自己的 IP 位址 （例如，搜尋 「 什麼是我的 IP 位址 」）。

   ![使用 Bing 搜尋「我的 IP 位址是什麼」](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. 新增其他位址範圍。 在 hello hello Azure 資料庫的 MySQL 防火牆規則，您可以指定單一 IP 位址範圍。 如果您想 toolimit hello 規則 tooone 單一 IP 位址，相同的起始 IP 和結束 IP 位址 hello 欄位的型別 hello。 開啟 hello 防火牆可讓系統管理員和使用者 tooaccess hello MySQL server toowhich 它們具有有效的認證上任何資料庫。

   ![Azure 入口網站 - 防火牆規則 ](./media/howto-manage-firewall-using-portal/5-specify-addresses.png)


5. 按一下**儲存**上 hello 工具列 toosave 此伺服器層級防火牆規則。 等候 hello 確認 hello 更新 toohello 防火牆規則已順利完成。

   ![Azure 入口網站 - 按一下 [儲存]](./media/howto-manage-firewall-using-portal/4-save-firewall-rule.png)

## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a>管理現有的伺服器層級防火牆規則，透過 hello Azure 入口網站
重複 hello 步驟 toomanage hello 防火牆規則。
* tooadd hello 目前的電腦，按一下**+ 加入我的 IP**。
* tooadd 額外的 IP 位址，在 hello**規則名稱**，**起始 IP**，和**結束 IP**。
* toomodify 現有的規則，按一下任一個 hello hello 規則中的欄位，並修改。
* toodelete 現有規則，按一下 hello 省略符號 […]，然後按一下**刪除**。
* 按一下**儲存**toosave hello 變更。

## <a name="next-steps"></a>後續步驟
- 在連接 tooan Azure 資料庫的 MySQL 伺服器的說明，請參閱[MySQL 的 Azure 資料庫的連接程式庫](./concepts-connection-libraries.md)
