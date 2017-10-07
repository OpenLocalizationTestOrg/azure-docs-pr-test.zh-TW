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
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a><span data-ttu-id="f1c56-103">在 Azure App Service 中建立 PHP-MySQL Web 應用程式並使用 FTP 部署</span><span class="sxs-lookup"><span data-stu-id="f1c56-103">Create a PHP-MySQL web app in Azure App Service and deploy using FTP</span></span>
<span data-ttu-id="f1c56-104">本教學課程告訴您如何 toocreate PHP MySQL web 應用程式以及如何 toodeploy 使用 FTP。</span><span class="sxs-lookup"><span data-stu-id="f1c56-104">This tutorial shows you how toocreate a PHP-MySQL web app and how toodeploy it using FTP.</span></span> <span data-ttu-id="f1c56-105">本教學課程假定您的電腦已經安裝 [PHP][install-php]、[MySQL][install-mysql]、一台 Web 伺服器，以及一個 FTP 用戶端。</span><span class="sxs-lookup"><span data-stu-id="f1c56-105">This tutorial assumes you have [PHP][install-php], [MySQL][install-mysql], a web server, and an FTP client installed on your computer.</span></span> <span data-ttu-id="f1c56-106">可在任何作業系統，包括 Windows、 Mac 和 Linux 上遵循本教學課程中的 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="f1c56-106">hello instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="f1c56-107">看完本指南後，您將擁有可在 Azure 上執行的 PHP/MySQL Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1c56-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="f1c56-108">您將了解：</span><span class="sxs-lookup"><span data-stu-id="f1c56-108">You will learn:</span></span>

* <span data-ttu-id="f1c56-109">如何 toocreate web 應用程式和 MySQL 資料庫使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="f1c56-109">How toocreate a web app and a MySQL database using hello Azure Portal.</span></span> <span data-ttu-id="f1c56-110">因為預設 PHP 啟用 Web 應用程式中，沒有特別的是需要的 toorun 您 PHP 程式碼。</span><span class="sxs-lookup"><span data-stu-id="f1c56-110">Because PHP is enabled in Web Apps by default, nothing special is required toorun your PHP code.</span></span>
* <span data-ttu-id="f1c56-111">如何 toopublish 您應用程式 tooAzure 使用 FTP。</span><span class="sxs-lookup"><span data-stu-id="f1c56-111">How toopublish your application tooAzure using FTP.</span></span>

<span data-ttu-id="f1c56-112">依照本教學課程進行，您將使用 PHP 建置一個簡易的註冊 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1c56-112">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="f1c56-113">hello 應用程式將會裝載在 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1c56-113">hello application will be hosted in a Web App.</span></span> <span data-ttu-id="f1c56-114">底下是完成 hello 應用程式的螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="f1c56-114">A screenshot of hello completed application is below:</span></span>

![Azure PHP Web Site][running-app]

> [!NOTE]
> <span data-ttu-id="f1c56-116">如果您想 tooget 開始使用 Azure App Service 的帳戶註冊前，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="f1c56-116">If you want tooget started with Azure App Service before signing up for an account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="f1c56-117">不需要信用卡，無需承諾。</span><span class="sxs-lookup"><span data-stu-id="f1c56-117">No credit cards required, no commitments.</span></span> 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a><span data-ttu-id="f1c56-118">建立 Web 應用程式並設定 FTP 發行</span><span class="sxs-lookup"><span data-stu-id="f1c56-118">Create a web app and set up FTP publishing</span></span>
<span data-ttu-id="f1c56-119">Web 應用程式和 MySQL 資料庫，請遵循這些步驟 toocreate:</span><span class="sxs-lookup"><span data-stu-id="f1c56-119">Follow these steps toocreate a web app and a MySQL database:</span></span>

1. <span data-ttu-id="f1c56-120">登入 toohello [Azure 入口網站][management-portal]。</span><span class="sxs-lookup"><span data-stu-id="f1c56-120">Login toohello [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="f1c56-121">按一下 hello **+ 新增**hello Azure 入口網站的左 hello 上方的圖示。</span><span class="sxs-lookup"><span data-stu-id="f1c56-121">Click hello **+ New** icon on hello top left of hello Azure Portal.</span></span>
   
    ![Create New Azure Web Site][new-website]
3. <span data-ttu-id="f1c56-123">在 hello 搜尋輸入**Web 應用程式 + MySQL** ，然後按一下  **Web 應用程式 + MySQL**。</span><span class="sxs-lookup"><span data-stu-id="f1c56-123">In hello search type **Web app + MySQL** and click on **Web app + MySQL**.</span></span>
   
    ![Custom Create a new Web Site][custom-create]
4. <span data-ttu-id="f1c56-125">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="f1c56-125">Click **Create**.</span></span> <span data-ttu-id="f1c56-126">請輸入唯一的應用程式服務名稱、 有效 hello 資源群組的名稱和新的服務方案。</span><span class="sxs-lookup"><span data-stu-id="f1c56-126">Enter a unique app service name, a valid name for hello resource group and a new service plan.</span></span>
   
    ![設定資源群組名稱][resource-group]
5. <span data-ttu-id="f1c56-128">輸入新資料庫，包括同意值 toohello 法律條款。</span><span class="sxs-lookup"><span data-stu-id="f1c56-128">Enter values for your new database, including agreeing toohello legal terms.</span></span>
   
    ![建立新的 MySQL 資料庫][new-mysql-db]
6. <span data-ttu-id="f1c56-130">Hello web 應用程式建立後，您會看到 hello 新應用程式服務刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f1c56-130">When hello web app has been created, you will see hello new app service blade.</span></span>
7. <span data-ttu-id="f1c56-131">按一下 [設定] > [部署認證]。</span><span class="sxs-lookup"><span data-stu-id="f1c56-131">Click on **Settings** > **Deployment credentials**.</span></span> 
   
    ![設定部署認證][set-deployment-credentials]
8. <span data-ttu-id="f1c56-133">tooenable FTP 發行，您必須提供使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="f1c56-133">tooenable FTP publishing, you must provide a user name and password.</span></span> <span data-ttu-id="f1c56-134">儲存 hello 認證，並記下 hello 使用者名稱和您所建立的密碼。</span><span class="sxs-lookup"><span data-stu-id="f1c56-134">Save hello credentials and make a note of hello user name and password you create.</span></span>
   
    ![建立發佈認證][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="f1c56-136">在本機建置及測試您的應用程式</span><span class="sxs-lookup"><span data-stu-id="f1c56-136">Build and test your app locally</span></span>
<span data-ttu-id="f1c56-137">hello 註冊應用程式是簡單的 PHP 應用程式，可讓您藉由提供您的名稱和電子郵件地址的 tooregister 事件。</span><span class="sxs-lookup"><span data-stu-id="f1c56-137">hello Registration application is a simple PHP application that allows you tooregister for an event by providing your name and email address.</span></span> <span data-ttu-id="f1c56-138">先前的註冊者相關資訊會顯示在資料表中。</span><span class="sxs-lookup"><span data-stu-id="f1c56-138">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="f1c56-139">註冊資訊會存放在 MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="f1c56-139">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="f1c56-140">hello 應用程式包含兩個檔案：</span><span class="sxs-lookup"><span data-stu-id="f1c56-140">hello app consists of two files:</span></span>

* <span data-ttu-id="f1c56-141">**index.php**：顯示註冊表單，以及內含註冊者資訊的資料表。</span><span class="sxs-lookup"><span data-stu-id="f1c56-141">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="f1c56-142">**createtable.php**: hello MySQL 的建立資料表 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1c56-142">**createtable.php**: Creates hello MySQL table for hello application.</span></span> <span data-ttu-id="f1c56-143">只會使用一次此檔案。</span><span class="sxs-lookup"><span data-stu-id="f1c56-143">This file will only be used once.</span></span>

<span data-ttu-id="f1c56-144">toobuild 和執行的 hello 應用程式在本機，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="f1c56-144">toobuild and run hello app locally, follow hello steps below.</span></span> <span data-ttu-id="f1c56-145">請注意，這些步驟假設您有 PHP、 MySQL 和您的本機電腦上設定 web 伺服器，而且您已啟用 hello [PDO MySQL 擴充功能][pdo-mysql]。</span><span class="sxs-lookup"><span data-stu-id="f1c56-145">Note that these steps assume you have PHP, MySQL, and a web server set up on your local machine, and that you have enabled hello [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="f1c56-146">建立名為 `registration`的 MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="f1c56-146">Create a MySQL database called `registration`.</span></span> <span data-ttu-id="f1c56-147">您可以從 hello MySQL 命令提示字元使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="f1c56-147">You can do this from hello MySQL command prompt with this command:</span></span>
   
        mysql> create database registration;
2. <span data-ttu-id="f1c56-148">在 Web 伺服器的根目錄中，建立名為 `registration` 的資料夾，並於其中建立兩個檔案，一個名為 `createtable.php`，另一個名為 `index.php`。</span><span class="sxs-lookup"><span data-stu-id="f1c56-148">In your web server's root directory, create a folder called `registration` and create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="f1c56-149">開啟 hello`createtable.php`在文字編輯器或 IDE 檔案，然後加入下列程式碼 hello。</span><span class="sxs-lookup"><span data-stu-id="f1c56-149">Open hello `createtable.php` file in a text editor or IDE and add hello code below.</span></span> <span data-ttu-id="f1c56-150">此程式碼將會使用的 toocreate hello `registration_tbl` hello 中的資料表`registration`資料庫。</span><span class="sxs-lookup"><span data-stu-id="f1c56-150">This code will be used toocreate hello `registration_tbl` table in hello `registration` database.</span></span>
   
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
   > <span data-ttu-id="f1c56-151">您將需要針對 tooupdate hello 值<code>$user</code>和<code>$pwd</code>本機 MySQL 使用者名稱與密碼。</span><span class="sxs-lookup"><span data-stu-id="f1c56-151">You will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
4. <span data-ttu-id="f1c56-152">開啟網頁瀏覽器並瀏覽過[http://localhost/registration/createtable.php][localhost-createtable]。</span><span class="sxs-lookup"><span data-stu-id="f1c56-152">Open a web browser and browse too[http://localhost/registration/createtable.php][localhost-createtable].</span></span> <span data-ttu-id="f1c56-153">這會建立 hello `registration_tbl` hello 資料庫資料表中的。</span><span class="sxs-lookup"><span data-stu-id="f1c56-153">This will create hello `registration_tbl` table in hello database.</span></span>
5. <span data-ttu-id="f1c56-154">開啟 hello**為 index.php**檔案文字編輯器或 IDE 中，然後加入 hello 基本 HTML 和 CSS 程式碼 hello 頁面 （hello PHP 程式碼會在稍後步驟中新增）。</span><span class="sxs-lookup"><span data-stu-id="f1c56-154">Open hello **index.php** file in a text editor or IDE and add hello basic HTML and CSS code for hello page (hello PHP code will be added in later steps).</span></span>
   
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
6. <span data-ttu-id="f1c56-155">Hello PHP 標記內加入連接 toohello 資料庫 PHP 程式碼。</span><span class="sxs-lookup"><span data-stu-id="f1c56-155">Within hello PHP tags, add PHP code for connecting toohello database.</span></span>
   
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
   > <span data-ttu-id="f1c56-156">同樣地，您將需要 tooupdate hello 值<code>$user</code>和<code>$pwd</code>本機 MySQL 使用者名稱與密碼。</span><span class="sxs-lookup"><span data-stu-id="f1c56-156">Again, you will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
7. <span data-ttu-id="f1c56-157">下列程式碼 hello 資料庫連接，加入程式碼插入 hello 資料庫的註冊資訊。</span><span class="sxs-lookup"><span data-stu-id="f1c56-157">Following hello database connection code, add code for inserting registration information into hello database.</span></span>
   
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
8. <span data-ttu-id="f1c56-158">最後，遵循上述的 hello 程式碼，加入程式碼從 hello 資料庫擷取資料。</span><span class="sxs-lookup"><span data-stu-id="f1c56-158">Finally, following hello code above, add code for retrieving data from hello database.</span></span>
   
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

<span data-ttu-id="f1c56-159">您現在可以瀏覽過[http://localhost/registration/index.php] [ localhost-index] tootest hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1c56-159">You can now browse too[http://localhost/registration/index.php][localhost-index] tootest hello app.</span></span>

## <a name="get-mysql-and-ftp-connection-information"></a><span data-ttu-id="f1c56-160">取得 MySQL 與 FTP 連線資訊</span><span class="sxs-lookup"><span data-stu-id="f1c56-160">Get MySQL and FTP connection information</span></span>
<span data-ttu-id="f1c56-161">在 Web 應用程式，您將執行的 tooconnect toohello MySQL 資料庫需要 hello 連接資訊。</span><span class="sxs-lookup"><span data-stu-id="f1c56-161">tooconnect toohello MySQL database that is running in Web Apps, your will need hello connection information.</span></span> <span data-ttu-id="f1c56-162">tooget MySQL 連接資訊，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f1c56-162">tooget MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="f1c56-163">Hello 應用程式服務從 web 應用程式 刀鋒視窗按一下 hello 資源群組的連結：</span><span class="sxs-lookup"><span data-stu-id="f1c56-163">From hello app service web app blade click on hello resource group link:</span></span>
   
    ![選取資源群組][select-resourcegroup]
2. <span data-ttu-id="f1c56-165">從資源群組中，按一下 hello 資料庫：</span><span class="sxs-lookup"><span data-stu-id="f1c56-165">From your resource group, click hello database:</span></span>
   
    ![選取資料庫][select-database]
3. <span data-ttu-id="f1c56-167">Hello 資料庫摘要，從選取**設定** > **屬性**。</span><span class="sxs-lookup"><span data-stu-id="f1c56-167">From hello database summary, select **Settings** > **Properties**.</span></span>
   
    ![選取屬性][select-properties]
4. <span data-ttu-id="f1c56-169">請記下的 hello 值`Database`， `Host`， `User Id`，和`Password`。</span><span class="sxs-lookup"><span data-stu-id="f1c56-169">Make note of hello values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![注意屬性][note-properties]
5. <span data-ttu-id="f1c56-171">從您網頁應用程式中，按一下 hello**下載發行設定檔**底部 hello hello 頁面右下角的連結：</span><span class="sxs-lookup"><span data-stu-id="f1c56-171">From your web app, click hello **Download publish profile** link at hello bottom right corner of hello page:</span></span>
   
    ![Download publish profile][download-publish-profile]
6. <span data-ttu-id="f1c56-173">開啟 hello`.publishsettings`在 XML 編輯器中的檔案。</span><span class="sxs-lookup"><span data-stu-id="f1c56-173">Open hello `.publishsettings` file in an XML editor.</span></span> 
7. <span data-ttu-id="f1c56-174">尋找 hello`<publishProfile >`具有項目`publishMethod="FTP"`這看起來類似 toothis:</span><span class="sxs-lookup"><span data-stu-id="f1c56-174">Find hello `<publishProfile >` element with `publishMethod="FTP"` that looks similar toothis:</span></span>
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

<span data-ttu-id="f1c56-175">請記下 hello `publishUrl`， `userName`，和`userPWD`屬性。</span><span class="sxs-lookup"><span data-stu-id="f1c56-175">Make note of hello `publishUrl`, `userName`, and `userPWD` attributes.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="f1c56-176">發佈您的應用程式</span><span class="sxs-lookup"><span data-stu-id="f1c56-176">Publish your app</span></span>
<span data-ttu-id="f1c56-177">您已經測試過您的應用程式在本機上之後，您可以發行該 tooyour web 應用程式使用 FTP。</span><span class="sxs-lookup"><span data-stu-id="f1c56-177">After you have tested your app locally, you can publish it tooyour web app using FTP.</span></span> <span data-ttu-id="f1c56-178">不過，您必須先 tooupdate hello 資料庫 hello 應用程式中的連接資訊。</span><span class="sxs-lookup"><span data-stu-id="f1c56-178">However, you first need tooupdate hello database connection information in hello application.</span></span> <span data-ttu-id="f1c56-179">使用您稍早取得的 hello 資料庫連接資訊 (在 hello**取得 MySQL 和 FTP 連線資訊**> 一節)，下列中的資訊更新 hello**兩者**hello`createdatabase.php`和`index.php`檔案以 hello 適當值：</span><span class="sxs-lookup"><span data-stu-id="f1c56-179">Using hello database connection information you obtained earlier (in hello **Get MySQL and FTP connection information** section), update hello following information in **both** hello `createdatabase.php` and `index.php` files with hello appropriate values:</span></span>

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

<span data-ttu-id="f1c56-180">現在您已準備好 toopublish 使用 FTP 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1c56-180">Now you are ready toopublish your app using FTP.</span></span>

1. <span data-ttu-id="f1c56-181">開啟您選擇的 FTP 用戶端。</span><span class="sxs-lookup"><span data-stu-id="f1c56-181">Open your FTP client of choice.</span></span>
2. <span data-ttu-id="f1c56-182">輸入 hello*主機名稱部分*從 hello`publishUrl`到您的 FTP 用戶端有上述的屬性。</span><span class="sxs-lookup"><span data-stu-id="f1c56-182">Enter hello *host name portion* from hello `publishUrl` attribute you noted above into your FTP client.</span></span>
3. <span data-ttu-id="f1c56-183">輸入 hello`userName`和`userPWD`您先前所述的屬性未變更到您的 FTP 用戶端。</span><span class="sxs-lookup"><span data-stu-id="f1c56-183">Enter hello `userName` and `userPWD` attributes you noted above unchanged into your FTP client.</span></span>
4. <span data-ttu-id="f1c56-184">建立連線。</span><span class="sxs-lookup"><span data-stu-id="f1c56-184">Establish a connection.</span></span>

<span data-ttu-id="f1c56-185">您連接之後您將會是無法 tooupload，並且視需要下載檔案。</span><span class="sxs-lookup"><span data-stu-id="f1c56-185">After you have connected you will be able tooupload and download files as needed.</span></span> <span data-ttu-id="f1c56-186">確定您要上傳檔案 toohello 根目錄中，也就是`/site/wwwroot`。</span><span class="sxs-lookup"><span data-stu-id="f1c56-186">Be sure that you are uploading files toohello root directory, which is `/site/wwwroot`.</span></span>

<span data-ttu-id="f1c56-187">同時上傳後`index.php`和`createtable.php`，瀏覽過**http://[site name].azurewebsites.net/createtable.php** toocreate hello MySQL 資料表 hello 應用程式，然後瀏覽過**http://[site 名稱].azurewebsites.net/index.php** toobegin 使用 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1c56-187">After uploading both `index.php` and `createtable.php`, browse too**http://[site name].azurewebsites.net/createtable.php** toocreate hello MySQL table for hello application, then browse too**http://[site name].azurewebsites.net/index.php** toobegin using hello application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1c56-188">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f1c56-188">Next steps</span></span>
<span data-ttu-id="f1c56-189">如需詳細資訊，請參閱 hello [PHP 開發人員中心](/develop/php/)。</span><span class="sxs-lookup"><span data-stu-id="f1c56-189">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

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

