---
title: "aaaCreate PHP MySQL web Azure App Service 中的應用程式，並使用 FTP 部署"
description: "示範如何 toocreate PHP web 應用程式，將資料儲存在 MySQL 並使用 FTP 部署 tooAzure 的教學課程。"
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6d9d1de5-5868-48fd-8bad-decb4979cd65
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 4d3b56a8ac63d0eba0dc0aec1b62e6d12f601bf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a>在 Azure App Service 中建立 PHP-MySQL Web 應用程式並使用 FTP 部署
本教學課程告訴您如何 toocreate PHP MySQL web 應用程式以及如何 toodeploy 使用 FTP。 本教學課程假定您的電腦已經安裝 [PHP][install-php]、[MySQL][install-mysql]、一台 Web 伺服器，以及一個 FTP 用戶端。 可在任何作業系統，包括 Windows、 Mac 和 Linux 上遵循本教學課程中的 hello 指示。 看完本指南後，您將擁有可在 Azure 上執行的 PHP/MySQL Web 應用程式。

您將了解：

* 如何 toocreate web 應用程式和 MySQL 資料庫使用 hello Azure 入口網站。 因為預設 PHP 啟用 Web 應用程式中，沒有特別的是需要的 toorun 您 PHP 程式碼。
* 如何 toopublish 您應用程式 tooAzure 使用 FTP。

依照本教學課程進行，您將使用 PHP 建置一個簡易的註冊 Web 應用程式。 hello 應用程式將會裝載在 Web 應用程式。 底下是完成 hello 應用程式的螢幕擷取畫面：

![Azure PHP Web Site][running-app]

> [!NOTE]
> 如果您想 tooget 開始使用 Azure App Service 的帳戶註冊前，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡，無需承諾。 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a>建立 Web 應用程式並設定 FTP 發行
Web 應用程式和 MySQL 資料庫，請遵循這些步驟 toocreate:

1. 登入 toohello [Azure 入口網站][management-portal]。
2. 按一下 hello **+ 新增**hello Azure 入口網站的左 hello 上方的圖示。
   
    ![Create New Azure Web Site][new-website]
3. 在 hello 搜尋輸入**Web 應用程式 + MySQL** ，然後按一下  **Web 應用程式 + MySQL**。
   
    ![Custom Create a new Web Site][custom-create]
4. 按一下 [建立] 。 請輸入唯一的應用程式服務名稱、 有效 hello 資源群組的名稱和新的服務方案。
   
    ![設定資源群組名稱][resource-group]
5. 輸入新資料庫，包括同意值 toohello 法律條款。
   
    ![建立新的 MySQL 資料庫][new-mysql-db]
6. Hello web 應用程式建立後，您會看到 hello 新應用程式服務刀鋒視窗。
7. 按一下 [設定] > [部署認證]。 
   
    ![設定部署認證][set-deployment-credentials]
8. tooenable FTP 發行，您必須提供使用者名稱和密碼。 儲存 hello 認證，並記下 hello 使用者名稱和您所建立的密碼。
   
    ![建立發佈認證][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a>在本機建置及測試您的應用程式
hello 註冊應用程式是簡單的 PHP 應用程式，可讓您藉由提供您的名稱和電子郵件地址的 tooregister 事件。 先前的註冊者相關資訊會顯示在資料表中。 註冊資訊會存放在 MySQL 資料庫。 hello 應用程式包含兩個檔案：

* **index.php**：顯示註冊表單，以及內含註冊者資訊的資料表。
* **createtable.php**: hello MySQL 的建立資料表 hello 應用程式。 只會使用一次此檔案。

toobuild 和執行的 hello 應用程式在本機，請遵循下列 hello 步驟。 請注意，這些步驟假設您有 PHP、 MySQL 和您的本機電腦上設定 web 伺服器，而且您已啟用 hello [PDO MySQL 擴充功能][pdo-mysql]。

1. 建立名為 `registration`的 MySQL 資料庫。 您可以從 hello MySQL 命令提示字元使用下列命令：
   
        mysql> create database registration;
2. 在 Web 伺服器的根目錄中，建立名為 `registration` 的資料夾，並於其中建立兩個檔案，一個名為 `createtable.php`，另一個名為 `index.php`。
3. 開啟 hello`createtable.php`在文字編輯器或 IDE 檔案，然後加入下列程式碼 hello。 此程式碼將會使用的 toocreate hello `registration_tbl` hello 中的資料表`registration`資料庫。
   
        <?php
        // DB connection info
        $host = "localhost";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        try{
            $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            $sql = "CREATE TABLE registration_tbl(
                        id INT NOT NULL AUTO_INCREMENT, 
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
   
   > [!NOTE]
   > 您將需要針對 tooupdate hello 值<code>$user</code>和<code>$pwd</code>本機 MySQL 使用者名稱與密碼。
   > 
   > 
4. 開啟網頁瀏覽器並瀏覽過[http://localhost/registration/createtable.php][localhost-createtable]。 這會建立 hello `registration_tbl` hello 資料庫資料表中的。
5. 開啟 hello**為 index.php**檔案文字編輯器或 IDE 中，然後加入 hello 基本 HTML 和 CSS 程式碼 hello 頁面 （hello PHP 程式碼會在稍後步驟中新增）。
   
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
6. Hello PHP 標記內加入連接 toohello 資料庫 PHP 程式碼。
   
        // DB connection info
        $host = "localhost";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect toodatabase.
        try {
            $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
   > [!NOTE]
   > 同樣地，您將需要 tooupdate hello 值<code>$user</code>和<code>$pwd</code>本機 MySQL 使用者名稱與密碼。
   > 
   > 
7. 下列程式碼 hello 資料庫連接，加入程式碼插入 hello 資料庫的註冊資訊。
   
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
8. 最後，遵循上述的 hello 程式碼，加入程式碼從 hello 資料庫擷取資料。
   
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

您現在可以瀏覽過[http://localhost/registration/index.php] [ localhost-index] tootest hello 應用程式。

## <a name="get-mysql-and-ftp-connection-information"></a>取得 MySQL 與 FTP 連線資訊
在 Web 應用程式，您將執行的 tooconnect toohello MySQL 資料庫需要 hello 連接資訊。 tooget MySQL 連接資訊，請遵循下列步驟：

1. Hello 應用程式服務從 web 應用程式 刀鋒視窗按一下 hello 資源群組的連結：
   
    ![選取資源群組][select-resourcegroup]
2. 從資源群組中，按一下 hello 資料庫：
   
    ![選取資料庫][select-database]
3. Hello 資料庫摘要，從選取**設定** > **屬性**。
   
    ![選取屬性][select-properties]
4. 請記下的 hello 值`Database`， `Host`， `User Id`，和`Password`。
   
    ![注意屬性][note-properties]
5. 從您網頁應用程式中，按一下 hello**下載發行設定檔**底部 hello hello 頁面右下角的連結：
   
    ![Download publish profile][download-publish-profile]
6. 開啟 hello`.publishsettings`在 XML 編輯器中的檔案。 
7. 尋找 hello`<publishProfile >`具有項目`publishMethod="FTP"`這看起來類似 toothis:
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

請記下 hello `publishUrl`， `userName`，和`userPWD`屬性。

## <a name="publish-your-app"></a>發佈您的應用程式
您已經測試過您的應用程式在本機上之後，您可以發行該 tooyour web 應用程式使用 FTP。 不過，您必須先 tooupdate hello 資料庫 hello 應用程式中的連接資訊。 使用您稍早取得的 hello 資料庫連接資訊 (在 hello**取得 MySQL 和 FTP 連線資訊**> 一節)，下列中的資訊更新 hello**兩者**hello`createdatabase.php`和`index.php`檔案以 hello 適當值：

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

現在您已準備好 toopublish 使用 FTP 的應用程式。

1. 開啟您選擇的 FTP 用戶端。
2. 輸入 hello*主機名稱部分*從 hello`publishUrl`到您的 FTP 用戶端有上述的屬性。
3. 輸入 hello`userName`和`userPWD`您先前所述的屬性未變更到您的 FTP 用戶端。
4. 建立連線。

您連接之後您將會是無法 tooupload，並且視需要下載檔案。 確定您要上傳檔案 toohello 根目錄中，也就是`/site/wwwroot`。

同時上傳後`index.php`和`createtable.php`，瀏覽過**http://[site name].azurewebsites.net/createtable.php** toocreate hello MySQL 資料表 hello 應用程式，然後瀏覽過**http://[site 名稱].azurewebsites.net/index.php** toobegin 使用 hello 應用程式。

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱 hello [PHP 開發人員中心](/develop/php/)。

[install-php]: http://www.php.net/manual/en/install.php
[install-mysql]: http://dev.mysql.com/doc/refman/5.6/en/installing.html
[pdo-mysql]: http://www.php.net/manual/en/ref.pdo-mysql.php
[localhost-createtable]: http://localhost/tasklist/createtable.php
[localhost-index]: http://localhost/tasklist/index.php
[running-app]: ./media/web-sites-php-mysql-deploy-use-ftp/running_app_2.png
[new-website]: ./media/web-sites-php-mysql-deploy-use-ftp/new_website2.png
[custom-create]: ./media/web-sites-php-mysql-deploy-use-ftp/create_web_mysql.png
[website-details]: ./media/web-sites-php-web-site-mysql-deploy-use-ftp/website_details.jpg
[new-mysql-db]: ./media/web-sites-php-mysql-deploy-use-ftp/create_db.png
[go-to-webapp]: ./media/web-sites-php-mysql-deploy-use-ftp/select_webapp.png
[set-deployment-credentials]: ./media/web-sites-php-mysql-deploy-use-ftp/set_credentials.png
[portal-ftp-username-password]: ./media/web-sites-php-mysql-deploy-use-ftp/save_credentials.png
[resource-group]: ./media/web-sites-php-mysql-deploy-use-ftp/set_group.png
[new-web-app]: ./media/web-sites-php-mysql-deploy-use-ftp/create_wa.png
[select-database]: ./media/web-sites-php-mysql-deploy-use-ftp/select_database.png
[select-resourcegroup]: ./media/web-sites-php-mysql-deploy-use-ftp/select_resourcegroup.png
[select-properties]: ./media/web-sites-php-mysql-deploy-use-ftp/select_properties.png
[note-properties]: ./media/web-sites-php-mysql-deploy-use-ftp/note-properties.png

[connection-string-info]: ./media/web-sites-php-web-site-mysql-deploy-use-ftp/connection_string_info.png
[management-portal]: https://portal.azure.com
[download-publish-profile]: ./media/web-sites-php-mysql-deploy-use-ftp/download_publish_profile_3.png

