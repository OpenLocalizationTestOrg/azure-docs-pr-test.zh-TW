---
title: "Azure 入口網站：建立適用於 PostgreSQL 的 Azure 資料庫 | Microsoft Docs"
description: "快速啟動指南 toocreate 並管理 PostgreSQL 伺服器使用 Azure 入口網站使用者介面的 Azure 資料庫。"
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.topic: quickstart
ms.date: 08/10/2017
ms.openlocfilehash: 61753268147d6ea283d1aa5d6baf269d2756d25a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-postgresql-in-hello-azure-portal"></a>Hello Azure 入口網站中建立 PostgreSQL Azure 資料庫

Azure PostgreSQL 資料庫是受管理的服務，可讓您 toorun、 管理及調整 hello 雲端中的高可用性 PostgreSQL 資料庫。 本快速入門示範如何 toocreate Azure 資料庫 PostgreSQL hello Azure 入口網站使用在五分鐘內的伺服器。

如果您沒有 Azure 訂用帳戶，請在開始前建立[免費帳戶](https://azure.microsoft.com/free/) 。

## <a name="log-in-toohello-azure-portal"></a>登入 toohello Azure 入口網站
開啟網頁瀏覽器，並瀏覽 toohello [Microsoft Azure 入口網站](https://portal.azure.com/)。 輸入認證 toosign toohello 入口網站中。 hello 預設檢視是服務儀表板。

## <a name="create-an-azure-database-for-postgresql"></a>建立適用於 PostgreSQL 的 Azure 資料庫

「適用於 PostgreSQL 的 Azure 資料庫」伺服器是以一組已定義的[計算和儲存體資源](./concepts-compute-unit-and-storage.md)所建立。 hello 伺服器內建立[Azure 資源群組](../azure-resource-manager/resource-group-overview.md)。

請遵循這些步驟 toocreate PostgreSQL server Azure 資料庫：
1.  按一下 hello**新增**hello 的左上角 hello Azure 入口網站上找到的按鈕 （+）。
2.  選取**資料庫**從 hello**新增**頁面上，並選取**Azure PostgreSQL 資料庫**從 hello**資料庫**頁面。
 ![Azure 資料庫 PostgreSQL-建立 hello 資料庫](./media/quickstart-create-database-portal/1-create-database.png)

3.  填寫 hello 新伺服器詳細資料表單以下列資訊，hello hello 前面影像所示：

    設定|建議的值|說明
    ---|---|---
    伺服器名稱 |*mypgserver-20170401*|選擇可識別 Azure Database for PostgreSQL 伺服器的唯一名稱。 hello 網域名稱*postgres.database.azure.com*是您提供的應用程式 tooconnect 來附加的 toohello 伺服器名稱。 hello 伺服器名稱只能包含小寫字母、 數字和 hello 連字號 （-） 字元，而且它必須包含 3 到 63 個字元。
    訂用帳戶|*您的訂用帳戶*|hello toouse 需您伺服器的 Azure 訂用帳戶。 如果您有多個訂閱，請選擇所在 hello 資源支付 hello 適當訂用帳戶。
    資源群組|*myresourcegroup*| 您可以產生新的資源群組名稱，或使用您訂用帳戶中現有的資源群組名稱。
    伺服器管理員登入 |*mylogin*| 連接 toohello 伺服器時，請您自己的登入帳戶 toouse。 hello 管理員登入名稱不能 'azure_superuser'、 'azure_pg_admin'、 'admin'、 'administrator'、 'root'、 'guest' public'，而且不能以 'pg_' 開頭。
    密碼 |您的選擇 | 建立 hello 伺服器系統管理員帳戶的新密碼。 必須包含 8 too128 個字元。 您的密碼必須包含下列類別目錄的 hello 其中三種字元-英文大寫字母、 英文小寫字母、 數字 (0-9) 和非英數字元 (！、 $、 #、 %等。)。
    位置|*hello 區域最接近 tooyour 使用者*| 選擇最接近 tooyour 使用者 hello 位置。
    PostgreSQL 版本|*選擇 hello 最新版本*| 除非您有特定需求，請選擇 hello 最新版本。
    定價層 | [基本]、[50 個計算單位]、[50 GB] | 按一下**定價層**toospecify hello 服務層和效能層級的新資料庫。 選擇基本層 hello hello 頂端的索引標籤中。 按一下左邊 hello 計算單位滑桿 tooadjust hello 值 toohello hello 供本快速入門的最少。 按一下**確定**toosave hello 定價層選擇。 請參閱下列螢幕擷取畫面的 hello。
    | Pin toodashboard | 勾選 | 檢查 hello **Pin toodashboard**選項 tooallow 輕鬆追蹤您的伺服器在 hello 前端儀表板 頁面上的 Azure 入口網站。

  > [!IMPORTANT]
  > hello 伺服器系統管理員登入和密碼，您在此處指定為 toohello server 中的必要的 toolog 和其資料庫，稍後在這個快速入門。 請記住或記錄此資訊，以供稍後使用。

    ![Azure 資料庫 PostgreSQL-挑選 hello 定價層](./media/quickstart-create-database-portal/2-service-tier.png)

4.  按一下**建立**tooprovision hello 伺服器。 佈建需要幾分鐘，向上 too20 分鐘的時間上限。

5.  在 [hello] 工具列上按一下**通知**toomonitor hello 部署程序。
 ![適用於 PostgreSQL 的 Azure 資料庫 - 查看通知](./media/quickstart-create-database-portal/3-notifications.png)
   
  根據預設，**postgres** 資料庫會建立在您的伺服器底下。 hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html)資料庫是適用於由使用者、 公用程式及協力廠商應用程式的預設資料庫。 

## <a name="configure-a-server-level-firewall-rule"></a>設定伺服器層級防火牆規則

PostgreSQL 服務的 hello Azure 資料庫建立 hello 伺服器層級的防火牆。 此防火牆會阻止外部應用程式和工具連接 toohello 伺服器和任何伺服器上的資料庫 hello，除非針對特定的 IP 位址的 tooopen hello 防火牆就會建立防火牆規則。 

1.  Hello 部署完成之後，請找出您的伺服器。 如有需要，您可以搜尋它。 例如，按一下**所有資源**從 hello 左側功能表和 hello 伺服器名稱 中的型別 (例如 hello 範例*mypgserver 20170401*) toosearch 您新建立的伺服器。 按一下您 hello 搜尋結果中所列的伺服器名稱。 hello**概觀**頁面會針對您的伺服器會開啟，並提供進一步組態的選項。
 
    ![Azure Database for PostgreSQL - 搜尋伺服器名稱](./media/quickstart-create-database-portal/4-locate.png)

2.  在 hello 伺服器頁面上，選取 **連線安全性**。 
    ![Azure Database for PostgreSQL - 建立防火牆規則](./media/quickstart-create-database-portal/5-firewall-2.png)

3.  在 hello**防火牆規則**hello 空白文字方塊中 hello 標題之下，按一下**規則名稱**建立 hello 防火牆規則的資料行 toobegin。 

    針對這個快速入門中，我們允許所有 IP 位址 hello 伺服器填入 hello 文字方塊中，每個資料行中，在以 hello 下列值：

    規則名稱 | 起始 IP | 結束 IP 
    ---|---|---
    AllowAllIps |  0.0.0.0 | 255.255.255.255

4. 在 hello hello 連線安全性頁面的上方工具列上，按一下 **儲存**。 請等候幾分鐘的時間，顯示 更新連接安全性已成功完成的繼續之前請注意 hello 通知。

    > [!NOTE]
    > 透過連接埠 5432 通訊 PostgreSQL 伺服器的連線 tooyour Azure 資料庫。 如果您嘗試 tooconnect 從公司網路內，透過連接埠 5432 輸出流量可能不允許您的網路防火牆。 如果是的話，就能 tooconnect tooyour 伺服器除非您的 IT 部門會開啟連接埠 5432。
    >

## <a name="get-hello-connection-information"></a>取得 hello 的連接資訊

當我們建立 Azure Database for PostgreSQL 伺服器時，系統會建立名為 **postgres** 的預設資料庫。 tooconnect tooyour 資料庫伺服器時，您需要 tooremember hello 完整的伺服器名稱和系統管理員登入認證。 您可能已記下這些 hello 快速入門文件中稍早的值。 如果您沒有這樣做，您可以輕鬆找到 hello 伺服器名稱和登入資訊從 hello 伺服器概觀 頁面中 hello Azure 入口網站。

1. 開啟伺服器的 [概觀] 頁面。 請記下 hello**伺服器名稱**和**伺服器系統管理員登入名稱**。
    您的游標停留在每個欄位，和 hello 複製圖示會出現 toohello 右邊的 hello 文字。 按一下 hello 複製圖示，做為所需的 toocopy hello 值。

 ![適用於 PostgreSQL 的 Azure 資料庫 - 伺服器管理員登入](./media/quickstart-create-database-portal/6-server-name.png)

## <a name="connect-toopostgresql-database-using-psql-in-cloud-shell"></a>連接雲端殼層中使用 psql tooPostgreSQL 資料庫

有許多應用程式可以使用 tooconnect tooyour Azure Database PostgreSQL 伺服器。 讓我們先使用如何 hello psql 命令列公用程式 tooillustrate tooconnect toohello 伺服器。  您可以使用網頁瀏覽器和 hello Azure 雲端殼層與這裡所述但 hello 不需要 tooinstall 任何額外的軟體。 如果您擁有 hello psql 公用程式的電腦上本機安裝，您可以從該處進行連線。

1. 啟動 hello Azure 雲端殼層透過 hello hello 上方瀏覽窗格上的終端機 圖示。

   ![適用於 PostgreSQL 的 Azure 資料庫 - Azure Cloud Shell 終端機圖示](./media/quickstart-create-database-portal/7-cloud-console.png)

2. hello Azure 雲端殼層會開啟瀏覽器中，讓您 tootype bash 殼層命令。

   ![適用於 PostgreSQL 的 Azure 資料庫 - Azure Shell Bash 提示字元](./media/quickstart-create-database-portal/8-bash.png)

3. 在 hello 雲端殼層提示字元中，會在 hello 綠色提示字元中輸入 hello psql 命令列連接 tooa PostgreSQL 伺服器的 Azure 資料庫中的資料庫。

    hello 下列格式是使用的 tooconnect tooan Azure Database PostgreSQL 伺服器 hello [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html)公用程式：
    ```bash
    psql --host=<yourserver> --port=<port> --username=<server admin login> --dbname=<database name>
    ```

    例如，下列命令的 hello 連接 tooan 範例伺服器：

    ```bash
    psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
    ```

    psql 參數 |建議的值|說明
    ---|---|---
    --host | 伺服器名稱 | 指定您 hello Azure Database PostgreSQL 如稍早建立時所用的 hello 的伺服器名稱值。 顯示的範例伺服器是 mypgserver-20170401.postgres.database.azure.com。使用 hello 完整的網域名稱 (\*。 postgres.database.azure.com) hello 範例所示。 如果您不記得您的伺服器名稱，請遵循 hello 前一個區段 tooget hello 連接資訊中的 hello 步驟。 
    --port | **5432** | 一律使用連接埠 5432 tooAzure 資料庫連接的 PostgreSQL 時。 
    --username | 伺服器管理員登入名稱 |輸入的 hello 伺服器系統管理員登入密碼時建立 hello Azure Database PostgreSQL 稍早所提供。 如果您不記得 hello 使用者名稱，請遵循 hello 前一個區段 tooget hello 連接資訊中的 hello 步驟。  hello 格式是 *username@servername* 。
    --dbname | **postgres** | 使用 hello 預設系統產生的資料庫名稱*postgres* hello 第一個連接。 您稍後會建立自己的資料庫。

    執行 hello psql 命令之後, 您自己的參數值，您在提示的 tootype hello 伺服器系統管理員密碼。 此密碼是 hello 相同時建立 hello 伺服器提供。 

    psql 參數 |建議的值|說明
    ---|---|---
    password | *您的系統管理員密碼* | 請注意，hello 字元不會顯示 hello bash 提示輸入的密碼。 按 enter 鍵之後，您輸入的所有 hello 字元 tooauthenticate 並連接。

    一旦連接之後，hello psql 公用程式會顯示 postgres 提示您輸入 sql 命令。 在 hello 初始連線輸出中，因為在 hello Azure 雲端殼層中的 hello psql 可能是針對 PostgreSQL 伺服器版本的 hello Azure 資料庫的版本不同，可能會顯示警告。 
    
    psql 輸出範例：
    ```bash
    psql (9.5.7, server 9.6.2)
    WARNING: psql major version 9.5, server major version 9.6.
        Some psql features might not work.
    SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-SHA384, bits: 256, compression: off)
    Type "help" for help.
   
    postgres=> 
    ```

    > [!TIP]
    > 如果不是 hello 防火牆設定 tooallow hello IP 位址的 hello Azure 雲端殼層，hello 會發生下列錯誤：
    > 
    > "psql: FATAL:  no pg_hba.conf entry for host "138.91.195.82", user "mylogin", database "postgres", SSL on FATAL：需要 SSL 連線。 請指定 SSL 選項，然後再試一次。
    > 
    > tooresolve hello 錯誤，請確定 hello 伺服器組態相符項目中 hello 步驟 hello*設定伺服器層級防火牆規則*hello 文章一節。

4.  建立空白資料庫在 hello 提示輸入下列命令的 hello:
    ```bash
    CREATE DATABASE mypgsqldb;
    ```
    hello 命令可能需要幾分鐘的時間 toocomplete。 

5.  在 hello 提示字元中執行下列命令 tooswitch 連線 toohello 新建資料庫的 hello **mypgsqldb**。
    ```bash
    \c mypgsqldb
    ```

6.  輸入 \q，然後按 ENTER tooquit psql。 您在完成之後，您可以關閉 hello Azure 雲端殼層。

現在您已連接 PostgreSQL toohello Azure 資料庫，而且建立空白的使用者資料庫。 繼續 toohello 使用其他常見的工具，pgAdmin 下一個區段 tooconnect。

## <a name="connect-toopostgresql-database-using-pgadmin"></a>連接使用 pgAdmin tooPostgreSQL 資料庫

使用 hello GUI 工具 tooconnect tooAzure PostgreSQL 伺服器_pgAdmin_
1.  啟動 hello _pgAdmin_應用程式用戶端電腦上。 您可以從 http://www.pgadmin.org/ 安裝 _pgAdmin_。
2.  按一下 hello**新增伺服器**圖示從 hello**快速連結**hello 中心中的 hello 儀表板頁面區段。
3.  在 hello**建立-伺服器**對話方塊**一般**索引標籤上，輸入 hello 伺服器的唯一易記名稱，例如**Azure PostgreSQL Server**。
![pgAdmin 工具 - 建立 - 伺服器](./media/quickstart-create-database-portal/9-pgadmin-create-server.png)
4.  在 hello**建立-伺服器**對話方塊中，**連接**索引標籤上，使用指定的 hello 設定，然後按一下**儲存**。
   ![pgAdmin - 建立 - 伺服器](./media/quickstart-create-database-portal/10-pgadmin-create-server.png)

    pgAdmin 參數 |建議的值|說明
    ---|---|---
    主機名稱/位址 | 伺服器名稱 | 指定您 hello Azure Database PostgreSQL 如稍早建立時所用的 hello 的伺服器名稱值。 顯示的範例伺服器是 mypgserver-20170401.postgres.database.azure.com。使用 hello 完整的網域名稱 (\*。 postgres.database.azure.com) hello 範例所示。 如果您不記得您的伺服器名稱，請遵循 hello 前一個區段 tooget hello 連接資訊中的 hello 步驟。 
    Port | **5432** | 一律使用連接埠 5432 tooAzure 資料庫連接的 PostgreSQL 時。  
    維護資料庫 | **postgres** | 使用 hello 預設系統產生的資料庫名稱*postgres*。
    使用者名稱 | 伺服器管理員登入名稱 | 輸入的 hello 伺服器系統管理員登入密碼時建立 hello Azure Database PostgreSQL 稍早所提供。 如果您不記得 hello 使用者名稱，請遵循 hello 前一個區段 tooget hello 連接資訊中的 hello 步驟。 hello 格式是 *username@servername* 。
    密碼 | *您的系統管理員密碼* |  hello 密碼稍早在本快速入門中建立 hello 伺服器時所選擇。
    角色 | 保留空白 | 不需要 tooprovide 角色名稱此時。 將 hello 欄位保留空白。
    SSL 模式 | 必要 | 根據預設，所有的 Azure PostgreSQL 伺服器建立時都會開啟強制使用 SSL。 tooturn 關閉 SSL 強制執行，請參閱詳細資料中的[強制 SSL](./concepts-ssl-connection-security.md)。
    
5.  按一下 [儲存] 。
6.  Hello 瀏覽器左窗格中，展開 hello**伺服器**節點。 選擇您的伺服器，例如**Azure PostgreSQL Server**按一下 tooconnect tooit。
7. 展開 hello 伺服器節點，然後再展開**資料庫**其下。 hello 清單應該包括現有*postgres*資料庫以及任何新建的使用者資料庫，例如*mypgsqldb*，我們建立 hello 前一節。 請注意，您可以使用 Azure Database for PostgreSQL，為每一部伺服器建立多個資料庫。
8. 以滑鼠右鍵按一下**資料庫**，選擇 hello**建立**功能表，然後按一下**資料庫**。
9.  輸入您選擇的資料庫名稱在 hello**資料庫**欄位，例如*mypgsqldb* hello 範例所示。 
10. 選取 hello**擁有者**hello hello 下拉式清單方塊中的資料庫。 選擇您的伺服器系統管理員登入名稱，例如 mylogin。
10. 按一下**儲存**toocreate 新的空白資料庫。
11. 在 [hello**瀏覽器**] 窗格中，請參閱 hello 您在建立的資料庫的資料庫 hello 清單下您的伺服器名稱。
 ![pgAdmin - 建立 - 資料庫](./media/quickstart-create-database-portal/11-pgadmin-database.png)


## <a name="clean-up-resources"></a>清除資源
清除您建立 hello 快速入門中的 hello 資源藉由刪除 hello [Azure 資源群組](../azure-resource-manager/resource-group-overview.md)、 hello 資源群組中，包括所有 hello 資源，或藉由刪除 hello 一部伺服器的資源，如果您想 tookeep hello其他資源保持不變。

> [!TIP]
> 此集合中的其他快速入門會以本快速入門為基礎。 如果您計劃與後續 toowork toocontinue 快速入門，無法清除不要 hello 建立本快速入門的資源。 如果您不打算 toocontinue，使用下列步驟 toodelete 資源本快速入門 hello Azure 入口網站中所建立的 hello。

toodelete hello 整個資源群組包括 hello 新建立的伺服器：
1.  Hello Azure 入口網站中，找出您的資源群組。 Hello Azure 入口網站中的 hello 左側功能表中按一下**資源群組**，然後按一下您的資源群組，例如我們的範例中的 hello 名稱**myresourcegroup**。
2.  在資源群組頁面上，按一下 [刪除]。 然後類型 hello 的資源群組名稱，例如我們的範例**myresourcegroup**，在 hello 文字方塊 tooconfirm 刪除、，然後按一下**刪除**。

或者，相反地，toodelete hello 新建伺服器：
1.  如果您沒有開啟，請在 hello Azure 入口網站中尋找您的伺服器。 在 Azure 入口網站中的 hello 左側功能表中按一下**所有資源**，然後搜尋您所建立的 hello 伺服器。
2.  在 hello**概觀**頁面上，按一下 hello**刪除**hello 上方窗格上的按鈕。
![Azure Database for PostgreSQL - 刪除伺服器](./media/quickstart-create-database-portal/12-delete.png)
3.  確認您想 toodelete，並顯示其下的 hello 資料庫受影響的 hello 的伺服器名稱。 您的伺服器名稱方塊中輸入 hello 文字，例如我們的範例**mypgserver 20170401**，然後按一下**刪除**。

## <a name="next-steps"></a>後續步驟
> [!div class="nextstepaction"]
> [使用匯出和匯入來移轉資料庫](./howto-migrate-using-export-and-import.md)
