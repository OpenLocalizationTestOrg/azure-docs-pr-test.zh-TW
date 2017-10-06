---
title: "aaaCreate PHP SQL web 應用程式和部署 tooAzure 應用程式服務使用 Git"
description: "此教學課程會示範如何 toocreate PHP web 應用程式將資料儲存在 Azure SQL Database 中，並使用 Git 部署 tooAzure 應用程式服務。"
services: app-service\web, sql-database
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6b090bf6-31d8-4b74-81eb-050ef95929ca
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: aaacb2fe0787bbcdafa72871912e8d08792be29d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-sql-web-app-and-deploy-tooazure-app-service-using-git"></a>建立 PHP SQL web 應用程式和部署 tooAzure 應用程式服務使用 Git
本教學課程告訴您如何 toocreate PHP web 應用程式中的[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)連接 tooAzure SQL Database 以及如何 toodeploy 使用 Git。 本教學課程假設您有[PHP][install-php]， [SQL Server Express][install-SQLExpress]，hello [Microsoft Drivers for for PHP SQL Server](http://www.microsoft.com/download/en/details.aspx?id=20098)，和[Git] [ install-git]安裝在電腦上。 完成本指南的步驟後，您將擁有在 Azure 上運作的 PHP-SQL Web 應用程式。

> [!NOTE]
> 您可以安裝和設定 PHP、 SQL Server Express 和 hello Microsoft Drivers for SQL Server 使用 hello PHP [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx)。
> 
> 

您將了解：

* Toocreate Azure web 應用程式和 SQL 資料庫使用 hello [Azure 入口網站](http://go.microsoft.com/fwlink/?LinkId=529715)。 因為預設 PHP 啟用 App Service Web 應用程式中，沒有特別的是需要的 toorun 您 PHP 程式碼。
* 如何 toopublish 並重新發行您的應用程式 tooAzure 使用 Git。

依照本教學課程進行，您將以 PHP 語法建構一個簡單的註冊網頁應用程式。 hello 應用程式將會裝載於 Azure 網站中。 底下是完成 hello 應用程式的螢幕擷取畫面：

![Azure PHP Web Site](./media/web-sites-php-sql-database-deploy-use-git/running_app_3.png)

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡；沒有承諾。
> 
> 

## <a name="create-an-azure-web-app-and-set-up-git-publishing"></a>建立 Azure Web 應用程式並設定 Git 發行功能
請遵循這些步驟 toocreate Azure web 應用程式和 SQL 資料庫：

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. Hello，即可開啟 hello Azure Marketplace**新增**hello 上方的圖示左邊 hello 儀表板上，按一下**全選**下一步 tooMarketplace 並選取**Web + 行動**。
3. 在 hello Marketplace，選取  **Web + 行動**。
4. 按一下 hello **Web 應用程式 + SQL**圖示。
5. 閱讀後 hello hello Web 應用程式 + SQL 應用程式的描述，選取**建立**。
6. 按一下 在每個部分 (**資源群組**， **Web 應用程式**，**資料庫**，和**訂用帳戶**) 然後輸入或選取所需的 hello 的值欄位：
   
   * 輸入您選擇的 URL 名稱    
   * 設定資料庫伺服器認證
   * 選取 hello 區域最接近 tooyou
     
     ![configure your app](./media/web-sites-php-sql-database-deploy-use-git/configure-db-settings.png)
7. 完成定義 hello web 應用程式，請按一下**建立**。
   
    Hello web 應用程式建立後，hello**通知** 按鈕會閃爍綠色**成功**和 hello 資源群組刀鋒視窗中開啟 tooshow 這兩個 hello web 應用程式和 hello SQL database hello 群組中的。
8. 按一下 hello 資源群組 刀鋒視窗 tooopen hello web 應用程式的刀鋒視窗中的 hello web 應用程式的圖示。
   
    ![Web 應用程式的資源群組](./media/web-sites-php-sql-database-deploy-use-git/resource-group-blade.png)
9. 在 [設定] 中按一下 [繼續部署] > [設定必要設定]。 選取 [本機 Git 儲存機制]，按一下 [確定]。
   
    ![where is your source code](./media/web-sites-php-sql-database-deploy-use-git/setup-local-git.png)
   
    如果您從未設定 Git 儲存機制，則必須提供使用者名稱和密碼。 toodo 此，依序按一下**設定** > **部署認證**hello web 應用程式的刀鋒視窗中。
   
    ![](./media/web-sites-php-sql-database-deploy-use-git/deployment-credentials.png)
10. 在**設定**按一下**屬性**toosee hello Git 遠端 URL 您於稍後 toouse toodeploy PHP 應用程式。

## <a name="get-sql-database-connection-information"></a>取得 SQL Database 連線資訊
tooconnect toohello SQL Database 執行個體的連結 tooyour web 應用程式，您將需要 hello hello 資料庫的建立時指定的連接資訊。 tooget hello SQL 資料庫連接資訊，請遵循下列步驟：

1. 在 hello 資源群組的刀鋒視窗中，按一下 hello SQL 資料庫的圖示。
2. 在 hello SQL database 的刀鋒視窗中，按一下 **設定** > **屬性**，然後按一下 **顯示資料庫的連接字串**。 
   
    ![檢視資料庫屬性](./media/web-sites-php-sql-database-deploy-use-git/view-database-properties.png)
3. 從 hello **PHP** > 一節的 hello 產生 對話方塊中，記下的 hello 值`Server`， `SQL Database`，和`User Name`。 您將使用這些值稍後當發行您的 PHP web 應用程式 tooAzure 應用程式服務。

## <a name="build-and-test-your-application-locally"></a>在本機建置與測試您的應用程式
hello 註冊應用程式是簡單的 PHP 應用程式，可讓您藉由提供您的名稱和電子郵件地址的 tooregister 事件。 先前的註冊者相關資訊會顯示在資料表中。 註冊資訊會儲存在 SQL Database 執行個體中。 hello 應用程式包含兩個檔案 （如下所示複製/貼上程式碼）：

* **index.php**：顯示註冊表單，以及內含註冊者資訊的資料表。
* **createtable.php**: hello SQL 資料庫的建立資料表 hello 應用程式。 只會使用一次此檔案。

toorun hello 應用程式在本機，請遵循下列 hello 步驟。 請注意，這些步驟假設您有 PHP 和 SQL Server Express 設定在本機電腦，並已啟用 hello [PDO 擴充功能，適用於 SQL Server][pdo-sqlsrv]。

1. 建立名為 `registration`的 SQL Server 資料庫。 您可以從 hello`sqlcmd`命令提示字元使用這些命令：
   
        >sqlcmd -S localhost\sqlexpress -U <local user name> -P <local password>
        1> create database registration
        2> GO    
2. 在應用程式根目錄中建立兩個檔案，一個名為 `createtable.php`，另一個名為 `index.php`。
3. 開啟 hello`createtable.php`在文字編輯器或 IDE 檔案，然後加入下列程式碼 hello。 此程式碼將會使用的 toocreate hello `registration_tbl` hello 中的資料表`registration`資料庫。
   
        <?php
        // DB connection info
        $host = "localhost\sqlexpress";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        try{
            $conn = new PDO( "sqlsrv:Server= $host ; Database = $db ", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            $sql = "CREATE TABLE registration_tbl(
            id INT NOT NULL IDENTITY(1,1) 
            PRIMARY KEY(id),
            name VARCHAR(30),
            email VARCHAR(30),
            date DATE)";
            $conn->query($sql);
        }
        catch(Exception $e){
            die(print_r($e));
        }
        echo "<h3>Table created.</h3>";
        ?>
   
    請注意，您將需要 tooupdate hello 值<code>$user</code>和<code>$pwd</code>使用您的本機 SQL Server 使用者名稱和密碼。
4. 在下列命令 hello 應用程式類型 hello hello 根目錄在終止：
   
        php -S localhost:8000
5. 開啟網頁瀏覽器並瀏覽過**http://localhost:8000/createtable.php**。 這會建立 hello `registration_tbl` hello 資料庫資料表中的。
6. 開啟 hello**為 index.php**檔案文字編輯器或 IDE 中，然後加入 hello 基本 HTML 和 CSS 程式碼 hello 頁面 （hello PHP 程式碼會在稍後步驟中新增）。
   
        <html>
        <head>
        <Title>Registration Form</Title>
        <style type="text/css">
            body { background-color: #fff; border-top: solid 10px #000;
                color: #333; font-size: .85em; margin: 20; padding: 20;
                font-family: "Segoe UI", Verdana, Helvetica, Sans-Serif;
            }
            h1, h2, h3,{ color: #000; margin-bottom: 0; padding-bottom: 0; }
            h1 { font-size: 2em; }
            h2 { font-size: 1.75em; }
            h3 { font-size: 1.2em; }
            table { margin-top: 0.75em; }
            th { font-size: 1.2em; text-align: left; border: none; padding-left: 0; }
            td { padding: 0.25em 2em 0.25em 0em; border: 0 none; }
        </style>
        </head>
        <body>
        <h1>Register here!</h1>
        <p>Fill in your name and email address, then click <strong>Submit</strong> tooregister.</p>
        <form method="post" action="index.php" enctype="multipart/form-data" >
              Name  <input type="text" name="name" id="name"/></br>
              Email <input type="text" name="email" id="email"/></br>
              <input type="submit" name="submit" value="Submit" />
        </form>
        <?php
   
        ?>
        </body>
        </html>
7. Hello PHP 標記內加入連接 toohello 資料庫 PHP 程式碼。
   
        // DB connection info
        $host = "localhost\sqlexpress";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect toodatabase.
        try {
            $conn = new PDO( "sqlsrv:Server= $host ; Database = $db ", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
    同樣地，您將需要 tooupdate hello 值<code>$user</code>和<code>$pwd</code>本機 MySQL 使用者名稱與密碼。
8. 下列程式碼 hello 資料庫連接，加入程式碼插入 hello 資料庫的註冊資訊。
   
        if(!empty($_POST)) {
        try {
            $name = $_POST['name'];
            $email = $_POST['email'];
            $date = date("Y-m-d");
            // Insert data
            $sql_insert = "INSERT INTO registration_tbl (name, email, date) 
                           VALUES (?,?,?)";
            $stmt = $conn->prepare($sql_insert);
            $stmt->bindValue(1, $name);
            $stmt->bindValue(2, $email);
            $stmt->bindValue(3, $date);
            $stmt->execute();
        }
        catch(Exception $e) {
            die(var_dump($e));
        }
        echo "<h3>Your're registered!</h3>";
        }
9. 最後，遵循上述的 hello 程式碼，加入程式碼從 hello 資料庫擷取資料。
   
        $sql_select = "SELECT * FROM registration_tbl";
        $stmt = $conn->query($sql_select);
        $registrants = $stmt->fetchAll(); 
        if(count($registrants) > 0) {
            echo "<h2>People who are registered:</h2>";
            echo "<table>";
            echo "<tr><th>Name</th>";
            echo "<th>Email</th>";
            echo "<th>Date</th></tr>";
            foreach($registrants as $registrant) {
                echo "<tr><td>".$registrant['name']."</td>";
                echo "<td>".$registrant['email']."</td>";
                echo "<td>".$registrant['date']."</td></tr>";
            }
             echo "</table>";
        } else {
            echo "<h3>No one is currently registered.</h3>";
        }

您現在可以瀏覽過**http://localhost:8000/index.php** tootest hello 應用程式。

## <a name="publish-your-application"></a>發佈您的應用程式
您已經測試過您的應用程式在本機上之後，您可以發行該 tooApp Service Web 應用程式使用 Git。 不過，您必須先 tooupdate hello 資料庫 hello 應用程式中的連接資訊。 使用您稍早取得的 hello 資料庫連接資訊 (在 hello**取得 SQL 資料庫連接資訊**> 一節)，下列中的資訊更新 hello**兩者**hello`createdatabase.php`和`index.php`檔案以 hello 適當值：

    // DB connection info
    $host = "tcp:<value of Server>";
    $user = "<value of User Name>";
    $pwd = "<your password>";
    $db = "<value of SQL Database>";

> [!NOTE]
> 在 hello <code>$host</code>，伺服器 hello 值必須在前面加上與<code>tcp:</code>。
> 
> 

現在，您已準備好 tooset 設定 Git 發行功能，並發佈 hello 應用程式。

> [!NOTE]
> 這些都是相同的步驟記下在 hello 結尾 hello hello**建立 Azure web 應用程式，並設定 Git 發行功能**上一節。
> 
> 

1. 開啟 GitBash (或終端機，如果 Git 位於您`PATH`)，變更目錄 toohello 根目錄，您的應用程式 (hello**註冊**目錄)，並執行的 hello 遵循命令：
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    安裝程式將會提示您稍早建立的 hello 密碼。
2. 瀏覽過**http://[web 應用程式 name].azurewebsites.net/createtable.php** toocreate hello SQL 資料庫資料表 hello 應用程式。
3. 瀏覽過**http://[web 應用程式 name].azurewebsites.net/index.php** toobegin 使用 hello 應用程式。

在發行您的應用程式之後，您可以開始製作變更 tooit，並使用 Git toopublish 它們。 

## <a name="publish-changes-tooyour-application"></a>發行變更 tooyour 應用程式
toopublish 變更 tooapplication，請遵循下列步驟：

1. 變更本機 tooyour 應用程式。
2. 開啟 GitBash (或終端機中，it Git 是在您`PATH`)，變更目錄 toohello 根目錄，應用程式，並執行 hello 下列命令：
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    安裝程式將會提示您稍早建立的 hello 密碼。
3. 瀏覽過**http://[web 應用程式 name].azurewebsites.net/index.php** toosee 您的變更。

## <a name="whats-changed"></a>變更的項目
* 從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[pdo-sqlsrv]: http://php.net/pdo_sqlsrv

