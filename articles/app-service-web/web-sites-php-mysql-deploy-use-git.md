---
title: "aaaCreate PHP MySQL web Azure App Service 中的應用程式，並使用 Git 部署"
description: "此教學課程會示範如何 toocreate PHP web 應用程式在 MySQL 中儲存資料，並使用 Git 部署 tooAzure。"
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
tags: mysql
ms.assetid: 7454475f-e275-4bc7-9f09-1ef07382e5da
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 9c22946777598cc973cd9dfc8d2a258bd08cc39a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-git"></a>在 Azure 應用程式服務中建立 PHP-MySQL Web 應用程式並使用 Git 部署
本教學課程告訴您如何 toocreate PHP MySQL web 應用程式以及如何 toodeploy 它太[App Service](http://go.microsoft.com/fwlink/?LinkId=529714)使用 Git。 您將使用[PHP][install-php]，hello MySQL 命令列工具 (屬於[MySQL][install-mysql])，和[Git] [install-git]安裝在電腦上。 可在任何作業系統，包括 Windows、 Mac 和 Linux 上遵循本教學課程中的 hello 指示。 看完本指南後，您將擁有可在 Azure 上執行的 PHP/MySQL Web 應用程式。

您將了解：

* 如何 toocreate web 應用程式和 MySQL 資料庫使用 hello [Azure 入口網站][management-portal]。 因為在已啟用的 PHP [App Service Web 應用程式](http://go.microsoft.com/fwlink/?LinkId=529714)根據預設，沒有特別的是必要的 toorun 您 PHP 程式碼。
* 如何 toopublish 並重新發行您的應用程式 tooAzure 使用 Git。
* 影響 tooenable hello 編輯器延伸模組 tooautomate 作曲者工作在每個`git push`。

依照本教學課程進行，您將使用 PHP 建置一個簡易的註冊 Web 應用程式。 將 Web 應用程式中裝載 hello 應用程式。 底下是完成 hello 應用程式的螢幕擷取畫面：

![Azure PHP web site][running-app]

## <a name="set-up-hello-development-environment"></a>設定 hello 開發環境
本教學課程假設您有[PHP][install-php]，hello MySQL 命令列工具 (屬於[MySQL][install-mysql])，和[Git] [ install-git]安裝在電腦上。

<a id="create-web-site-and-set-up-git"></a>

## <a name="create-a-web-app-and-set-up-git-publishing"></a>建立 Web 應用程式並設定 Git 發行
Web 應用程式和 MySQL 資料庫，請遵循這些步驟 toocreate:

1. 登入 toohello [Azure 入口網站][management-portal]。
2. 按一下 hello**新增**圖示。
3. 按一下**看到所有**下一步太**Marketplace**。 
4. 依序按一下 [Web + 行動] 和 [Web 應用程式 + MySQL]。 然後按一下 [建立] 。
5. 輸入資源群組的有效名稱。
   
    ![設定資源群組名稱][resource-group]
6. 輸入新 Web 應用程式的值。
   
    ![建立 Web 應用程式][new-web-app]
7. 輸入新資料庫，包括同意值 toohello 法律條款。
   
    ![建立新的 MySQL 資料庫][new-mysql-db]
8. Hello web 應用程式建立後，您會看到 hello 新 web 應用程式 刀鋒視窗。
9. 在 [設定] 中按一下 [繼續部署]，然後按一下 [設定必要設定]。
   
    ![設定 Git 發佈][setup-publishing]
10. 選取**本機 Git 儲存機制**hello 來源。
    
     ![設定 Git 儲存機制][setup-repository]
11. tooenable Git 發行，您必須提供使用者名稱和密碼。 記下的 hello 使用者名稱和您所建立的密碼。 )
    
     ![建立發佈認證][credentials]

## <a name="get-remote-mysql-connection-information"></a>取得遠端 MySQL 連線資訊
在 Web 應用程式，您將執行的 tooconnect toohello MySQL 資料庫需要 hello 連接資訊。 tooget MySQL 連接資訊，請遵循下列步驟：

1. 從資源群組中，按一下 hello 資料庫：
   
    ![選取資料庫][select-database]
2. 從 hello 資料庫**設定**，選取**屬性**。
   
    ![選取屬性][select-properties]
3. 請記下的 hello 值`Database`， `Host`， `User Id`，和`Password`。
   
    ![注意屬性][note-properties]

## <a name="build-and-test-your-app-locally"></a>在本機建置及測試您的應用程式
現在您已經建立了 Web 應用程式，您可以在本機開發自己的應用程式，並在測試後進行部署。

hello 註冊應用程式是簡單的 PHP 應用程式，可讓您藉由提供您的名稱和電子郵件地址的 tooregister 事件。 先前的註冊者相關資訊會顯示在資料表中。 註冊資訊會存放在 MySQL 資料庫。 hello 應用程式包含一個檔案 （如下所示複製/貼上程式碼）：

* **index.php**：顯示註冊表單，以及內含註冊者資訊的資料表。

toobuild 和執行的 hello 應用程式在本機，請遵循下列 hello 步驟。 請注意，這些步驟假設您有 hello PHP 和 MySQL 命令列工具 （MySQL 的一部分） 設定在本機電腦，且您已啟用 hello [PDO MySQL 擴充功能][pdo-mysql]。

1. 連接 toohello MySQL 使用遠端伺服器，hello 值`Data Source`， `User Id`， `Password`，和`Database`您稍早擷取：
   
        mysql -h{Data Source] -u[User Id] -p[Password] -D[Database]
2. hello MySQL 命令提示字元會出現：
   
        mysql>
3. 貼上的 hello 下列`CREATE TABLE`命令 toocreate hello`registration_tbl`資料庫資料表中：
   
        CREATE TABLE registration_tbl(id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(id), name VARCHAR(30), email VARCHAR(30), date DATE);
4. Hello 的本機應用程式資料夾的根目錄中建立**為 index.php**檔案。
5. 開啟 hello**為 index.php**檔案文字編輯器或 IDE 中，然後加入 hello 下列程式碼，並且完成 hello 必要的變更標記為`//TODO:`註解。

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
            // DB connection info
            //TODO: Update hello values for $host, $user, $pwd, and $db
            //using hello values you retrieved earlier from hello Azure Portal.
            $host = "value of Data Source";
            $user = "value of User Id";
            $pwd = "value of Password";
            $db = "value of Database";
            // Connect toodatabase.
            try {
                $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
                $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            }
            catch(Exception $e){
                die(var_dump($e));
            }
            // Insert registration info
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
            // Retrieve data
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
        ?>
        </body>
        </html>

1. 在終端機移 tooyour 應用程式資料夾，然後輸入 hello 下列命令：
   
       php -S localhost:8000

您現在可以瀏覽過**: //localhost: 8000 /** tootest hello 應用程式。

## <a name="publish-your-app"></a>發佈您的應用程式
您已經測試過您的應用程式在本機上之後，您可以使用 Git tooWeb 應用程式對它進行發佈。 您將會初始化您的本機 Git 儲存機制和發行 hello 應用程式。

> [!NOTE]
> 這些是 hello 相同 hello 結尾 hello hello 建立 web 應用程式的 Azure 入口網站以及組設定 Git 發行上面所示的步驟。
> 
> 

1. （選擇性） 如果您遺失或錯置 Git 遠端 repostitory URL，請瀏覽 hello Azure 入口網站上的 toohello web 應用程式屬性。
2. 開啟 GitBash (或終端機，如果 Git 位於您`PATH`)，變更目錄 toohello 根目錄，應用程式，並執行 hello 下列命令：
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    安裝程式將會提示您稍早建立的 hello 密碼。
   
    ![透過 Git 的初始發送 tooAzure][git-initial-push]
3. 瀏覽過**http://[site name].azurewebsites.net/index.php** toobegin 使用 hello 應用程式 （這項資訊會儲存帳戶儀表板）：
   
    ![Azure PHP web site][running-app]

在發行您的應用程式之後，您可以開始製作變更 tooit，並使用 Git toopublish 它們。

## <a name="publish-changes-tooyour-app"></a>發行變更 tooyour 應用程式
toopublish 變更 tooyour 應用程式，請遵循下列步驟：

1. 請在本機變更 tooyour 應用程式。
2. 開啟 GitBash (或終端機中，it Git 是在您`PATH`)、 變更目錄 toohello 根目錄，應用程式，並執行下列命令的 hello:
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    安裝程式將會提示您稍早建立的 hello 密碼。
   
    ![透過 Git 推送的站台變更 tooAzure][git-change-push]
3. 瀏覽過**http://[site name].azurewebsites.net/index.php** toosee 應用程式與您所做的變更：
   
    ![Azure PHP web site][running-app]

> [!NOTE]
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡；沒有承諾。
> 
> 

<a name="composer"></a>

## <a name="enable-composer-automation-with-hello-composer-extension"></a>啟用編輯器自動化以 hello 編輯器延伸模組
根據預設，App Service 中的 hello git 部署程序不執行任何動作與 composer.json，如果您有一個 PHP 專案中。 您可以啟用 composer.json 處理期間`git push`藉由啟用 hello 編輯器延伸模組。

1. 在您的 PHP web 應用程式的刀鋒視窗中 hello [Azure 入口網站][management-portal]，按一下 **工具** > **延伸**。
   
    ![編輯器擴充功能設定][composer-extension-settings]
2. 按一下 [新增]，然後按一下 [編輯器]。
   
    ![編輯器擴充功能新增][composer-extension-add]
3. 按一下**確定**tooaccept 法律條款。 按一下**確定**再次 tooadd hello 延伸模組。
   
    hello**擴充功能安裝**刀鋒視窗現在將會顯示 hello 編輯器延伸模組。  
    ![編輯器擴充功能檢視][composer-extension-view]
4. 現在，執行`git add`， `git commit`，和`git push`如同在 hello 上一節。 您就會立即看到編輯器正在安裝 composer.json 中定義的相依性。
   
    ![編輯器擴充功能成功][composer-extension-success]

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱 hello [PHP 開發人員中心](/develop/php/)。

<!-- URL List -->

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[install-mysql]: http://dev.mysql.com/downloads/mysql/
[pdo-mysql]: http://www.php.net/manual/en/ref.pdo-mysql.php
[management-portal]: https://portal.azure.com
[sql-database-editions]: http://msdn.microsoft.com/library/windowsazure/ee621788.aspx

<!-- IMG List -->

[running-app]: ./media/web-sites-php-mysql-deploy-use-git/running_app_2.png
[new-website]: ./media/web-sites-php-mysql-deploy-use-git/new_website2.png
[custom-create]: ./media/web-sites-php-mysql-deploy-use-git/create_web_mysql.png
[new-mysql-db]: ./media/web-sites-php-mysql-deploy-use-git/create_db.png
[go-to-webapp]: ./media/web-sites-php-mysql-deploy-use-git/select_webapp.png
[setup-git-publishing]: ./media/web-sites-php-mysql-deploy-use-git/setup_git_publishing.png
[credentials]: ./media/web-sites-php-mysql-deploy-use-git/save_credentials.png
[resource-group]: ./media/web-sites-php-mysql-deploy-use-git/set_group.png
[new-web-app]: ./media/web-sites-php-mysql-deploy-use-git/create_wa.png
[setup-publishing]: ./media/web-sites-php-mysql-deploy-use-git/setup_deploy.png
[setup-repository]: ./media/web-sites-php-mysql-deploy-use-git/select_local_git.png
[select-database]: ./media/web-sites-php-mysql-deploy-use-git/select_database.png
[select-properties]: ./media/web-sites-php-mysql-deploy-use-git/select_properties.png
[note-properties]: ./media/web-sites-php-mysql-deploy-use-git/note-properties.png

[git-instructions]: ./media/web-sites-php-mysql-deploy-use-git/git-instructions.png
[git-change-push]: ./media/web-sites-php-mysql-deploy-use-git/php-git-change-push.png
[git-initial-push]: ./media/web-sites-php-mysql-deploy-use-git/php-git-initial-push.png

[composer-extension-settings]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-settings.png
[composer-extension-add]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-add.png
[composer-extension-view]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-view.png
[composer-extension-success]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-success.png
