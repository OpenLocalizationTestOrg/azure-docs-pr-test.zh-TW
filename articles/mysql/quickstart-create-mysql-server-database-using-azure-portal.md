---
title: "快速入門：建立 Azure Database for MySQL 伺服器 - Azure 入口網站 | Microsoft Docs"
description: "您透過使用 hello Azure 入口網站 tooquickly 此發行項步驟會建立在五分鐘內的範例 Azure 資料庫的 MySQL 伺服器。"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.date: 08/15/2017
ms.openlocfilehash: d5754fe7a6f0f0f4b3fa19d456c4e15e64ca396c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-portal"></a>使用 Azure 入口網站建立 Azure Database for MySQL 伺服器
Azure MySQL 資料庫是受管理的服務，可讓您 toorun、 管理及調整 hello 雲端中的高可用性 MySQL 資料庫。 本快速入門示範如何 toocreate Azure 資料庫使用 hello Azure 入口網站在五分鐘內的 MySQL 伺服器。 

如果您沒有 Azure 訂用帳戶，請在開始前建立[免費帳戶](https://azure.microsoft.com/free/) 。

## <a name="log-in-tooazure"></a>登入 tooAzure
開啟網頁瀏覽器，並瀏覽 toohello [Microsoft Azure 入口網站](https://portal.azure.com/)。 輸入認證 toosign toohello 入口網站中。 hello 預設檢視是服務儀表板。

## <a name="create-azure-database-for-mysql-server"></a>建立 Azure Database for MySQL 伺服器
建立的「適用於 MySQL 的 Azure 資料庫」伺服器會有一組已定義的[計算和儲存體](./concepts-compute-unit-and-storage.md)資源。 hello 伺服器內建立[Azure 資源群組](../azure-resource-manager/resource-group-overview.md)。

請遵循這些步驟 toocreate Azure 資料庫的 MySQL 伺服器：

1. 按一下 hello**新增**hello 的左上角 hello Azure 入口網站上找到的按鈕 （+）。

2. 選取**資料庫**從 hello**新增**頁面上，並選取**Azure 資料庫的 MySQL**從 hello**資料庫**頁面。 您也可以輸入**MySQL** hello 新頁面的搜尋方塊 toofind hello 服務中。
![Azure 入口網站 - 新增 - 資料庫 - MySQL](./media/quickstart-create-mysql-server-database-using-azure-portal/2_navigate-to-mysql.png)

3. 填寫 hello 新伺服器詳細資料表單以下列資訊，hello hello 前面影像所示：

    **設定** | **建議的值** | **欄位描述** 
    ---|---|---
    伺服器名稱 | myserver4demo | 選擇可識別 Azure Database for MySQL 伺服器的唯一名稱。 hello 網域名稱*mysql.database.azure.com*是您提供的應用程式 tooconnect 來附加的 toohello 伺服器名稱。 hello 伺服器名稱只能包含小寫字母、 數字和 hello 連字號 （-） 字元，而且它必須包含 3 到 63 個字元。
    訂用帳戶 | 您的訂用帳戶 | hello toouse 需您伺服器的 Azure 訂用帳戶。 如果您有多個訂閱，請選擇所在 hello 資源支付 hello 適當訂用帳戶。
    資源群組 | myresourcegroup | 您可以產生新的資源群組名稱，或使用您訂用帳戶中現有的資源群組名稱。
    伺服器管理員登入 | myadmin | 連接 toohello 伺服器時，請您自己的登入帳戶 toouse。 hello 系統管理員登入名稱不可為 'azure_superuser'、 'admin'、 'administrator'、 'root'、 'guest' public'。
    密碼 | 您的選擇 | 建立 hello 伺服器系統管理員帳戶的新密碼。 必須包含 8 too128 個字元。 您的密碼必須包含下列類別目錄的 hello 其中三種字元-英文大寫字母、 英文小寫字母、 數字 (0-9) 和非英數字元 (！、 $、 #、 %等。)。
    確認密碼 | 您的選擇| 確認 hello 管理帳戶的密碼。
    位置 | *hello 區域最接近 tooyour 使用者*| 選擇最接近 tooyour 使用者或其他 Azure 應用程式的 hello 位置。
    版本 | *選擇 hello 最新版本*| 除非您有特定需求，請選擇 hello 最新版本。
    定價層 | [基本]、[50 個計算單位]、[50 GB] | 按一下**定價層**toospecify hello 服務層和效能層級的新資料庫。 選擇**基本層**hello hello 頂端的索引標籤中。 按一下左邊 hello hello**計算單位**滑桿 tooadjust hello 值 toohello 最低金額可用的本快速入門。 按一下**確定**toosave hello 定價層選擇。 請參閱下列螢幕擷取畫面的 hello。
    Pin toodashboard | 勾選 | 檢查 hello **Pin toodashboard**選項 tooallow 輕鬆追蹤您的伺服器在 hello 前端儀表板 頁面上的 Azure 入口網站。

    > [!IMPORTANT]
    > hello 伺服器系統管理員登入和您在此處指定的密碼是必要的 toolog toohello 伺服器和它的資料庫，稍後在本快速入門。 請記住或記錄此資訊，以供稍後使用。
    > 

    ![Azure 入口網站-藉由提供所需的 hello 表單輸入建立 MySQL](./media/quickstart-create-mysql-server-database-using-azure-portal/3_create-server.png)

4.  按一下**建立**tooprovision hello 伺服器。 佈建需要幾分鐘，向上 too20 分鐘的時間上限。
   
5.  在 [hello] 工具列上按一下**通知**（鈴鐺圖示） toomonitor hello 部署程序。

## <a name="configure-a-server-level-firewall-rule"></a>設定伺服器層級防火牆規則

hello Azure 資料庫的 MySQL 服務會在 hello 伺服器層級建立防火牆。 此防火牆會阻止外部應用程式和工具連接 toohello 伺服器和任何伺服器上的資料庫 hello，除非針對特定的 IP 位址的 tooopen hello 防火牆就會建立防火牆規則。 

1.  Hello 部署完成之後，請找出您的伺服器。 如有需要，您可以搜尋它。 例如，按一下**所有資源**從 hello 左側功能表和 hello 伺服器名稱 中的型別 (例如 hello 範例*myserver4demo*) toosearch 您新建立的伺服器。 按一下您 hello 搜尋結果中所列的伺服器名稱。 hello**概觀**頁面會針對您的伺服器會開啟，並提供進一步組態的選項。

2. 在 hello 伺服器頁面上，選取 **連線安全性**。

3.  在 hello**防火牆規則**hello 空白文字方塊中 hello 標題之下，按一下**規則名稱**建立 hello 防火牆規則的資料行 toobegin。 

    如本快速入門中，讓我們來允許所有 IP 位址 hello 伺服器填入 hello 文字方塊中，每個資料行中，以下列值的 hello:

    規則名稱 | 起始 IP | 結束 IP 
    ---|---|---
    AllowAllIps |  0.0.0.0 | 255.255.255.255

4. Hello 上方工具列上的 hello**連線安全性**頁面上，按一下**儲存**。 請等候幾分鐘的時間，顯示 更新連接安全性已成功完成的繼續之前請注意 hello 通知。

    > [!NOTE]
    > 透過連接埠 3306 通訊連線 tooAzure MySQL 資料庫。 如果您嘗試 tooconnect 從公司網路內，透過連接埠 3306 輸出流量可能不允許您的網路防火牆。 如果是的話，就能 tooconnect tooyour 伺服器除非您的 IT 部門會開啟連接埠 3306。
    > 

## <a name="get-hello-connection-information"></a>取得 hello 的連接資訊
tooconnect tooyour 資料庫伺服器時，您需要 tooremember hello 完整的伺服器名稱和系統管理員登入認證。 您可能已記下這些 hello 快速入門文件中稍早的值。 如果您沒有這樣做，您可以輕鬆找到 hello 伺服器 hello 伺服器的名稱和登入資訊**概觀**頁面或 hello**屬性**hello Azure 入口網站中的頁面。

1. 開啟伺服器的 [概觀] 頁面。 請記下 hello**伺服器名稱**和**伺服器系統管理員登入名稱**。 
    您的游標停留在每個欄位，和 hello 複製圖示會出現 toohello 右邊的 hello 文字。 按一下 hello 複製圖示，做為所需的 toocopy hello 值。

    在此範例中，hello 伺服器名稱是*myserver4demo.mysql.database.azure.com*，hello server 系統管理員登入，且 *myadmin@myserver4demo* 。

## <a name="connect-toomysql-using-mysql-command-line-tool"></a>連接 tooMySQL 使用 mysql 命令列工具
有許多應用程式可以使用 tooconnect tooyour Azure 資料庫的 MySQL 伺服器。 讓我們先使用 hello [mysql](https://dev.mysql.com/doc/refman/5.7/en/mysql.html)命令列工具 tooillustrate 如何 tooconnect toohello 伺服器。  您可以使用網頁瀏覽器和 hello Azure 雲端殼層與這裡所述但 hello 不需要 tooinstall 任何額外的軟體。 如果您擁有 hello mysql 公用程式的電腦上本機安裝，您可以從該處進行連線。

1. 啟動 hello Azure 雲端殼層透過 hello 終端機圖示 (> _) 上 hello hello Azure 入口網站 web 頁面的右上方。

2. hello Azure 雲端殼層會開啟瀏覽器中，讓您 tootype bash 殼層命令。

    ![命令提示字元 - mysql 命令列範例](./media/quickstart-create-mysql-server-database-using-azure-portal/7_connect-to-server.png)

3. 在 hello 雲端殼層提示字元中，會在 hello 綠色提示字元中輸入 hello mysql 命令列連接 tooyour Azure 資料庫的 MySQL 伺服器。

    hello 遵循格式是使用的 tooconnect tooan Azure 資料庫的 MySQL 伺服器 hello mysql 公用程式：
    ```bash
    mysql --host <yourserver> --user <server admin login> --password
    ```

    例如，下列命令的 hello 連接 tooour 範例伺服器：
    ```azurecli-interactive
    mysql --host myserver4demo.mysql.database.azure.com --user myadmin@myserver4demo --password
    ```

    mysql 參數 |建議的值|說明
    ---|---|---
    --host | 伺服器名稱 | 指定您 hello Azure 資料庫的 MySQL 稍早建立時所用的 hello 的伺服器名稱值。 顯示的範例伺服器是 myserver4demo.mysql.database.azure.com。使用 hello 完整的網域名稱 (\*。 mysql.database.azure.com) hello 範例所示。 如果您不記得您的伺服器名稱，請遵循 hello 前一個區段 tooget hello 連接資訊中的 hello 步驟。 
    --user | 伺服器管理員登入名稱 |輸入的 hello 伺服器系統管理員登入密碼時您建立 hello Azure 資料庫的 MySQL 稍早所提供。 如果您不記得 hello 使用者名稱，請遵循 hello 前一個區段 tooget hello 連接資訊中的 hello 步驟。  hello 格式是 *username@servername* 。
    --password | 等到出現提示為止 | 系統將提示您太之後的 [輸入密碼] 輸入 hello 命令。 出現提示時，輸入 hello 相同時建立 hello 伺服器所提供的密碼。  請注意 hello 輸入字元不會顯示 hello bash 提示您輸入時的密碼。 按 enter 鍵之後，您輸入的所有 hello 字元 tooauthenticate 並連接。

   一旦連接之後，會顯示 hello mysql 公用程式`mysql>`提示您 tootype 命令。 

    mysql 輸出範例：
    ```bash
    Welcome toohello MySQL monitor.  Commands end with ; or \g.
    Your MySQL connection id is 65505
    Server version: 5.6.26.0 MySQL Community Server (GPL)
    
    Copyright (c) 2000, 2017, Oracle and/or its affiliates. All rights reserved.
    
    Oracle is a registered trademark of Oracle Corporation and/or its
    affiliates. Other names may be trademarks of their respective
    owners.

    Type 'help;' or '\h' for help. Type '\c' tooclear hello current input statement.
    
    mysql>
    ```
    > [!TIP]
    > 如果不是 hello 防火牆設定 tooallow hello IP 位址的 hello Azure 雲端殼層，hello 會發生下列錯誤：
    >
    > 錯誤 2003 (28000): 123.456.789.0 的 IP 位址不是允許用戶端 tooaccess hello 伺服器。
    >
    > tooresolve hello 錯誤，請確定 hello 伺服器組態相符項目中 hello 步驟 hello*設定伺服器層級防火牆規則*hello 文章一節。

4. 檢視伺服器狀態 tooensure hello 連接可運作。 型別`status`在 hello mysql > 一旦它所連接的提示。
    ```sql
    status
    ```

   > [!TIP]
   > 如需其他命令，請參閱 [MySQL 5.7 參考手冊 - 第 4.5.1 章](https://dev.mysql.com/doc/refman/5.7/en/mysql.html)。

5.  在 hello mysql 建立空白資料庫 > 提示輸入下列命令的 hello:
    ```sql
    CREATE DATABASE quickstartdb;
    ```
    hello 命令可能需要幾分鐘的時間 toocomplete。 

    在適用於 MySQL Server 的 Azure 資料庫內，您可以建立一個或多個資料庫。 您可以選擇單一資料庫，每個伺服器 tooutilize toocreate 所有 hello 資源，或建立多個資料庫 tooshare hello 資源。 沒有可以建立的資料庫沒有限制 toohello 數目，但多個資料庫共用 hello 相同的伺服器資源。 

6. 列出在 hello mysql hello 資料庫 > 提示輸入下列命令的 hello:

    ```sql
    SHOW DATABASES;
    ```

7.  型別`\q`，然後按 ENTER tooquit hello mysql 工具。 您在完成之後，您可以關閉 hello Azure 雲端殼層。

現在您已連接 MySQL toohello Azure 資料庫，而且建立空白的使用者資料庫。 繼續下一個區段 toorepeat toohello 類似的練習 tooconnect toohello 使用其他常見的工具，MySQL 工作臺的同一部伺服器。

## <a name="connect-toohello-server-using-hello-mysql-workbench-gui-tool"></a>使用 hello MySQL Workbench GUI 工具 toohello 伺服器連接
使用 hello GUI 工具 MySQL Workbench tooconnect tooAzure MySQL 伺服器：

1.  啟動 hello MySQL Workbench 用戶端電腦上的應用程式。 您可以從[這裡](https://dev.mysql.com/downloads/workbench/)下載並安裝 MySQL Workbench。

2.  在**設定新連線**對話方塊方塊中，輸入下列資訊 hello**參數** 索引標籤：

    ![設定新連線](./media/quickstart-create-mysql-server-database-using-azure-portal/setup-new-connection.png)

    | **設定** | **建議的值** | **欄位描述** |
    |---|---|---|
    |   連線名稱 | 示範連線 | 指定此連線的標籤。 |
    | 連線方式 | 標準 (TCP/IP) | 標準 (TCP/IP) 就足夠了。 |
    | 主機名稱 | 伺服器名稱 | 指定您 hello Azure 資料庫的 MySQL 稍早建立時所用的 hello 的伺服器名稱值。 顯示的範例伺服器是 myserver4demo.mysql.database.azure.com。使用 hello 完整的網域名稱 (\*。 mysql.database.azure.com) hello 範例所示。 如果您不記得您的伺服器名稱，請遵循 hello 前一個區段 tooget hello 連接資訊中的 hello 步驟。  |
    | Port | 3306 | 一律使用連接埠 3306 的 MySQL 連接 tooAzure 資料庫時。 |
    | 使用者名稱 |  伺服器管理員登入名稱 | 輸入的 hello 伺服器系統管理員登入密碼時您建立 hello Azure 資料庫的 MySQL 稍早所提供。 我們的範例使用者名稱為 myadmin@myserver4demo。 如果您不記得 hello 使用者名稱，請遵循 hello 前一個區段 tooget hello 連接資訊中的 hello 步驟。 hello 格式是 *username@servername* 。
    | 密碼 | 您的密碼 | 按一下 [儲存在保存庫...] 按鈕 toosave hello 密碼。 |

    按一下**測試連接**tootest 如果已正確設定所有參數。 按一下 [確定] toosave hello 連線。 

    > [!NOTE]
    > SSL 會強制執行預設會在您的伺服器，並需要額外的設定，在訂單 tooconnect 成功。 請參閱[設定 SSL 連接，您的應用程式 toosecurely 所連接的 MySQL tooAzure 資料庫](./howto-configure-ssl.md)。  如果您想要這個快速入門 toodisable SSL，請瀏覽 hello Azure 入口網站，然後按一下 hello 連線安全性頁面 toodisable hello 強制的 SSL 連接切換按鈕。

## <a name="clean-up-resources"></a>清除資源
清除您建立 hello 快速入門中的 hello 資源藉由刪除 hello [Azure 資源群組](../azure-resource-manager/resource-group-overview.md)、 hello 資源群組中，包括所有 hello 資源，或藉由刪除 hello 一部伺服器的資源，如果您想 tookeep hello其他資源保持不變。

> [!TIP]
> 此集合中的其他快速入門會以本快速入門為基礎。 如果您計劃與後續 toowork toocontinue 快速入門，無法清除不要 hello 建立本快速入門的資源。 如果您不打算 toocontinue，使用 hello 本快速入門 hello Azure 入口網站中的下列步驟 toodelete 建立所有資源。
>

toodelete hello 整個資源群組包括 hello 新建立的伺服器：
1.  Hello Azure 入口網站中，找出您的資源群組。 Hello Azure 入口網站中的 hello 左側功能表中按一下**資源群組**，然後按一下您的資源群組，例如我們的範例中的 hello 名稱**myresourcegroup**。
2.  在資源群組頁面上，按一下 [刪除]。 然後類型 hello 的資源群組名稱，例如我們的範例**myresourcegroup**，在 hello 文字方塊 tooconfirm 刪除、，然後按一下**刪除**。

或者，相反地，toodelete hello 新建伺服器：
1.  如果您沒有開啟，請在 hello Azure 入口網站中尋找您的伺服器。 在 Azure 入口網站中的 hello 左側功能表中按一下**所有資源**，然後搜尋您所建立的 hello 伺服器。
2.  在 hello**概觀**頁面上，按一下 hello**刪除**hello 上方窗格上的按鈕。
![Azure Database for MySQL - 刪除伺服器](./media/quickstart-create-mysql-server-database-using-azure-portal/delete-server.png)
3.  確認您想 toodelete，並顯示其下的 hello 資料庫受影響的 hello 的伺服器名稱。 您的伺服器名稱方塊中輸入 hello 文字，例如我們的範例**myserver4demo**，然後按一下**刪除**。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [設計您的第一個 Azure Database for MySQL 資料庫](./tutorial-design-database-using-portal.md)

