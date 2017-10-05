---
title: "在 Azure App Service 中建立 PHP-MySQL Web 應用程式並使用 FTP 部署"
description: "示範如何建立 PHP Web 應用程式，將資料儲存於 MySQL 中並對 Azure 使用 FTP 部署的教學課程。"
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
ms.openlocfilehash: d428dffc6b810a692be0ec39a5f9cca05f5439e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a><span data-ttu-id="33afe-103">在 Azure App Service 中建立 PHP-MySQL Web 應用程式並使用 FTP 部署</span><span class="sxs-lookup"><span data-stu-id="33afe-103">Create a PHP-MySQL web app in Azure App Service and deploy using FTP</span></span>
<span data-ttu-id="33afe-104">本教學課程說明如何建立 PHP-MySQL Web 應用程式，以及如何使用 FTP 部署該 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="33afe-104">This tutorial shows you how to create a PHP-MySQL web app and how to deploy it using FTP.</span></span> <span data-ttu-id="33afe-105">本教學課程假定您的電腦已經安裝 [PHP][install-php]、[MySQL][install-mysql]、一台 Web 伺服器，以及一個 FTP 用戶端。</span><span class="sxs-lookup"><span data-stu-id="33afe-105">This tutorial assumes you have [PHP][install-php], [MySQL][install-mysql], a web server, and an FTP client installed on your computer.</span></span> <span data-ttu-id="33afe-106">本教學課程裡的說明可運用在包括 Windows、Mac 與 Linux 的任何作業系統上。</span><span class="sxs-lookup"><span data-stu-id="33afe-106">The instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="33afe-107">看完本指南後，您將擁有可在 Azure 上執行的 PHP/MySQL Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="33afe-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="33afe-108">您將了解：</span><span class="sxs-lookup"><span data-stu-id="33afe-108">You will learn:</span></span>

* <span data-ttu-id="33afe-109">如何使用 Azure 入口網站建立 Web 應用程式和 MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="33afe-109">How to create a web app and a MySQL database using the Azure Portal.</span></span> <span data-ttu-id="33afe-110">由於預設會在 Web Apps 上啟用 PHP，因此您不需要執行任何特殊步驟就能執行 PHP 程式碼。</span><span class="sxs-lookup"><span data-stu-id="33afe-110">Because PHP is enabled in Web Apps by default, nothing special is required to run your PHP code.</span></span>
* <span data-ttu-id="33afe-111">如何使用 FTP 將應用程式發行到 Azure。</span><span class="sxs-lookup"><span data-stu-id="33afe-111">How to publish your application to Azure using FTP.</span></span>

<span data-ttu-id="33afe-112">依照本教學課程進行，您將使用 PHP 建置一個簡易的註冊 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="33afe-112">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="33afe-113">此應用程式將裝載於 Web 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="33afe-113">The application will be hosted in a Web App.</span></span> <span data-ttu-id="33afe-114">完成之應用程式的螢幕擷取畫面如下：</span><span class="sxs-lookup"><span data-stu-id="33afe-114">A screenshot of the completed application is below:</span></span>

![Azure PHP Web Site][running-app]

> [!NOTE]
> <span data-ttu-id="33afe-116">如果您想要在註冊 Azure 帳戶之前開始使用 Azure App Service，請移至 [試用 App Service](https://azure.microsoft.com/try/app-service/)，讓您能夠立即在應用程式服務中建立短期的入門 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="33afe-116">If you want to get started with Azure App Service before signing up for an account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="33afe-117">不需要信用卡，無需承諾。</span><span class="sxs-lookup"><span data-stu-id="33afe-117">No credit cards required, no commitments.</span></span> 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a><span data-ttu-id="33afe-118">建立 Web 應用程式並設定 FTP 發行</span><span class="sxs-lookup"><span data-stu-id="33afe-118">Create a web app and set up FTP publishing</span></span>
<span data-ttu-id="33afe-119">請遵循以下步驟來建立 Web 應用程式與 MySQL 資料庫：</span><span class="sxs-lookup"><span data-stu-id="33afe-119">Follow these steps to create a web app and a MySQL database:</span></span>

1. <span data-ttu-id="33afe-120">登入 [Azure 入口網站][management-portal]。</span><span class="sxs-lookup"><span data-stu-id="33afe-120">Login to the [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="33afe-121">按一下 Azure 入口網站左上方的 [+ 新增]  圖示。</span><span class="sxs-lookup"><span data-stu-id="33afe-121">Click the **+ New** icon on the top left of the Azure Portal.</span></span>
   
    ![Create New Azure Web Site][new-website]
3. <span data-ttu-id="33afe-123">在搜尋中輸入 **Web 應用程式 + MySQL** 並按一下 [Web 應用程式 + MySQL]。</span><span class="sxs-lookup"><span data-stu-id="33afe-123">In the search type **Web app + MySQL** and click on **Web app + MySQL**.</span></span>
   
    ![Custom Create a new Web Site][custom-create]
4. <span data-ttu-id="33afe-125">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="33afe-125">Click **Create**.</span></span> <span data-ttu-id="33afe-126">輸入唯一的應用程式服務名稱、資源群組的有效名稱及新的服務方案。</span><span class="sxs-lookup"><span data-stu-id="33afe-126">Enter a unique app service name, a valid name for the resource group and a new service plan.</span></span>
   
    ![設定資源群組名稱][resource-group]
5. <span data-ttu-id="33afe-128">輸入新資料庫的值，包括同意法律條款。</span><span class="sxs-lookup"><span data-stu-id="33afe-128">Enter values for your new database, including agreeing to the legal terms.</span></span>
   
    ![建立新的 MySQL 資料庫][new-mysql-db]
6. <span data-ttu-id="33afe-130">建立 Web 應用程式之後，您將會看到新的 Web 應用程式刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="33afe-130">When the web app has been created, you will see the new app service blade.</span></span>
7. <span data-ttu-id="33afe-131">按一下 [設定] > [部署認證]。</span><span class="sxs-lookup"><span data-stu-id="33afe-131">Click on **Settings** > **Deployment credentials**.</span></span> 
   
    ![設定部署認證][set-deployment-credentials]
8. <span data-ttu-id="33afe-133">若要啟用 FTP 發行，您必須提供使用者名稱與密碼。</span><span class="sxs-lookup"><span data-stu-id="33afe-133">To enable FTP publishing, you must provide a user name and password.</span></span> <span data-ttu-id="33afe-134">儲存認證，並記下您建立的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="33afe-134">Save the credentials and make a note of the user name and password you create.</span></span>
   
    ![建立發佈認證][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="33afe-136">在本機建置及測試您的應用程式</span><span class="sxs-lookup"><span data-stu-id="33afe-136">Build and test your app locally</span></span>
<span data-ttu-id="33afe-137">註冊應用程式是一項簡單的 PHP 應用程式，您只需提供名稱與電子郵件地址就能註冊活動。</span><span class="sxs-lookup"><span data-stu-id="33afe-137">The Registration application is a simple PHP application that allows you to register for an event by providing your name and email address.</span></span> <span data-ttu-id="33afe-138">先前的註冊者相關資訊會顯示在資料表中。</span><span class="sxs-lookup"><span data-stu-id="33afe-138">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="33afe-139">註冊資訊會存放在 MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="33afe-139">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="33afe-140">該應用程式包含兩個檔案：</span><span class="sxs-lookup"><span data-stu-id="33afe-140">The app consists of two files:</span></span>

* <span data-ttu-id="33afe-141">**index.php**：顯示註冊表單，以及內含註冊者資訊的資料表。</span><span class="sxs-lookup"><span data-stu-id="33afe-141">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="33afe-142">**createtable.php**：為應用程式建立 MySQL 資料表。</span><span class="sxs-lookup"><span data-stu-id="33afe-142">**createtable.php**: Creates the MySQL table for the application.</span></span> <span data-ttu-id="33afe-143">只會使用一次此檔案。</span><span class="sxs-lookup"><span data-stu-id="33afe-143">This file will only be used once.</span></span>

<span data-ttu-id="33afe-144">若要在本機建置與執行應用程式，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="33afe-144">To build and run the app locally, follow the steps below.</span></span> <span data-ttu-id="33afe-145">請注意，這些步驟假定您已在本機電腦上安裝 PHP、MySQL 以及 Web 伺服器，而且您已經啟用了[適用 MySQL 的 PDO 延伸功能][pdo-mysql]。</span><span class="sxs-lookup"><span data-stu-id="33afe-145">Note that these steps assume you have PHP, MySQL, and a web server set up on your local machine, and that you have enabled the [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="33afe-146">建立名為 `registration`的 MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="33afe-146">Create a MySQL database called `registration`.</span></span> <span data-ttu-id="33afe-147">您可以使用以下命令，從 MySQL 命令提示字元中完成此工作：</span><span class="sxs-lookup"><span data-stu-id="33afe-147">You can do this from the MySQL command prompt with this command:</span></span>
   
        mysql> create database registration;
2. <span data-ttu-id="33afe-148">在 Web 伺服器的根目錄中，建立名為 `registration` 的資料夾，並於其中建立兩個檔案，一個名為 `createtable.php`，另一個名為 `index.php`。</span><span class="sxs-lookup"><span data-stu-id="33afe-148">In your web server's root directory, create a folder called `registration` and create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="33afe-149">在文字編輯器或 IDE 中開啟 `createtable.php` 檔案，加入下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="33afe-149">Open the `createtable.php` file in a text editor or IDE and add the code below.</span></span> <span data-ttu-id="33afe-150">此程式碼將會在 `registration` 資料庫中用於建立 `registration_tbl` 資料表。</span><span class="sxs-lookup"><span data-stu-id="33afe-150">This code will be used to create the `registration_tbl` table in the `registration` database.</span></span>
   
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
   > <span data-ttu-id="33afe-151">您必須更新的值<code>$user</code>和<code>$pwd</code>本機 MySQL 使用者名稱與密碼。</span><span class="sxs-lookup"><span data-stu-id="33afe-151">You will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
4. <span data-ttu-id="33afe-152">開啟網頁瀏覽器並瀏覽至 [http://localhost/registration/createtable.php][localhost-createtable]。</span><span class="sxs-lookup"><span data-stu-id="33afe-152">Open a web browser and browse to [http://localhost/registration/createtable.php][localhost-createtable].</span></span> <span data-ttu-id="33afe-153">這會在資料庫中建立 `registration_tbl` 資料表。</span><span class="sxs-lookup"><span data-stu-id="33afe-153">This will create the `registration_tbl` table in the database.</span></span>
5. <span data-ttu-id="33afe-154">在文字編輯器或 IDE 中開啟 **index.php** 檔案，加入頁面的基本 HTML 和 CSS 程式碼 (稍後的步驟中將加入 PHP 程式碼)。</span><span class="sxs-lookup"><span data-stu-id="33afe-154">Open the **index.php** file in a text editor or IDE and add the basic HTML and CSS code for the page (the PHP code will be added in later steps).</span></span>
   
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
        <p>Fill in your name and email address, then click <strong>Submit</strong> to register.</p>
        <form method="post" action="index.php" enctype="multipart/form-data" >
              Name  <input type="text" name="name" id="name"/></br>
              Email <input type="text" name="email" id="email"/></br>
              <input type="submit" name="submit" value="Submit" />
        </form>
        <?php
   
        ?>
        </body>
        </html>
6. <span data-ttu-id="33afe-155">在 PHP 標籤內，加入用來連線至資料庫的 PHP 程式碼。</span><span class="sxs-lookup"><span data-stu-id="33afe-155">Within the PHP tags, add PHP code for connecting to the database.</span></span>
   
        // DB connection info
        $host = "localhost";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect to database.
        try {
            $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
   > [!NOTE]
   > <span data-ttu-id="33afe-156">同樣地，您將需要更新的值<code>$user</code>和<code>$pwd</code>本機 MySQL 使用者名稱與密碼。</span><span class="sxs-lookup"><span data-stu-id="33afe-156">Again, you will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
7. <span data-ttu-id="33afe-157">在資料庫連接程式碼後面，加入可將登錄資訊插入至資料庫的程式碼。</span><span class="sxs-lookup"><span data-stu-id="33afe-157">Following the database connection code, add code for inserting registration information into the database.</span></span>
   
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
8. <span data-ttu-id="33afe-158">最後，在上述程式碼後面，加入可從資料庫擷取資料的程式碼。</span><span class="sxs-lookup"><span data-stu-id="33afe-158">Finally, following the code above, add code for retrieving data from the database.</span></span>
   
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

<span data-ttu-id="33afe-159">您現在可以瀏覽至 [http://localhost/registration/index.php][localhost-index] 並測試應用程式。</span><span class="sxs-lookup"><span data-stu-id="33afe-159">You can now browse to [http://localhost/registration/index.php][localhost-index] to test the app.</span></span>

## <a name="get-mysql-and-ftp-connection-information"></a><span data-ttu-id="33afe-160">取得 MySQL 與 FTP 連線資訊</span><span class="sxs-lookup"><span data-stu-id="33afe-160">Get MySQL and FTP connection information</span></span>
<span data-ttu-id="33afe-161">若要連接至在 Web Apps 中執行的 MySQL 資料庫，您需要連線資訊。</span><span class="sxs-lookup"><span data-stu-id="33afe-161">To connect to the MySQL database that is running in Web Apps, your will need the connection information.</span></span> <span data-ttu-id="33afe-162">若要取得 MySQL 連線資訊，請依照以下步驟執行：</span><span class="sxs-lookup"><span data-stu-id="33afe-162">To get MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="33afe-163">在 [應用程式服務 Web 應用程式] 刀鋒視窗中，按一下資源群組連結：</span><span class="sxs-lookup"><span data-stu-id="33afe-163">From the app service web app blade click on the resource group link:</span></span>
   
    ![選取資源群組][select-resourcegroup]
2. <span data-ttu-id="33afe-165">從資源群組中，按一下資料庫：</span><span class="sxs-lookup"><span data-stu-id="33afe-165">From your resource group, click the database:</span></span>
   
    ![選取資料庫][select-database]
3. <span data-ttu-id="33afe-167">從資料庫摘要中，選取 [設定] > [屬性]。</span><span class="sxs-lookup"><span data-stu-id="33afe-167">From the database summary, select **Settings** > **Properties**.</span></span>
   
    ![選取屬性][select-properties]
4. <span data-ttu-id="33afe-169">記下 `Database`、`Host`、`User Id` 及 `Password` 的值。</span><span class="sxs-lookup"><span data-stu-id="33afe-169">Make note of the values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![注意屬性][note-properties]
5. <span data-ttu-id="33afe-171">從 Web 應用程式中，按一下頁面右下角的 [下載發行設定檔]  連結：</span><span class="sxs-lookup"><span data-stu-id="33afe-171">From your web app, click the **Download publish profile** link at the bottom right corner of the page:</span></span>
   
    ![Download publish profile][download-publish-profile]
6. <span data-ttu-id="33afe-173">在 XML 編輯器中開啟 `.publishsettings` 檔案。</span><span class="sxs-lookup"><span data-stu-id="33afe-173">Open the `.publishsettings` file in an XML editor.</span></span> 
7. <span data-ttu-id="33afe-174">尋找含 `<publishProfile >` 的 `publishMethod="FTP"` 元素，其看起來如下：</span><span class="sxs-lookup"><span data-stu-id="33afe-174">Find the `<publishProfile >` element with `publishMethod="FTP"` that looks similar to this:</span></span>
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

<span data-ttu-id="33afe-175">記下 `publishUrl`、`userName` 及 `userPWD` 屬性。</span><span class="sxs-lookup"><span data-stu-id="33afe-175">Make note of the `publishUrl`, `userName`, and `userPWD` attributes.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="33afe-176">發佈您的應用程式</span><span class="sxs-lookup"><span data-stu-id="33afe-176">Publish your app</span></span>
<span data-ttu-id="33afe-177">當您在本機完成應用程式測試之後，可以使用 FTP 將其發行至您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="33afe-177">After you have tested your app locally, you can publish it to your web app using FTP.</span></span> <span data-ttu-id="33afe-178">不過，首先您需要更新應用程式中的資料庫連線資訊。</span><span class="sxs-lookup"><span data-stu-id="33afe-178">However, you first need to update the database connection information in the application.</span></span> <span data-ttu-id="33afe-179">使用您稍早取得的資料庫連接資訊 (在＜**取得 MySQL 和 FTP 連線資訊**＞一節中），將 `createdatabase.php` 和 `index.php` **兩者**檔案中的下列資訊都更新為適當的值：</span><span class="sxs-lookup"><span data-stu-id="33afe-179">Using the database connection information you obtained earlier (in the **Get MySQL and FTP connection information** section), update the following information in **both** the `createdatabase.php` and `index.php` files with the appropriate values:</span></span>

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

<span data-ttu-id="33afe-180">現在您可以使用 FTP 來發佈應用程式。</span><span class="sxs-lookup"><span data-stu-id="33afe-180">Now you are ready to publish your app using FTP.</span></span>

1. <span data-ttu-id="33afe-181">開啟您選擇的 FTP 用戶端。</span><span class="sxs-lookup"><span data-stu-id="33afe-181">Open your FTP client of choice.</span></span>
2. <span data-ttu-id="33afe-182">將您在以上步驟中從 `publishUrl` 屬性記下的主機名稱部分輸入到您的 FTP 用戶端。</span><span class="sxs-lookup"><span data-stu-id="33afe-182">Enter the *host name portion* from the `publishUrl` attribute you noted above into your FTP client.</span></span>
3. <span data-ttu-id="33afe-183">將您在以上步驟中記下的 `userName` 與 `userPWD` 屬性，原封不動地輸入到您的 FTP 用戶端。</span><span class="sxs-lookup"><span data-stu-id="33afe-183">Enter the `userName` and `userPWD` attributes you noted above unchanged into your FTP client.</span></span>
4. <span data-ttu-id="33afe-184">建立連線。</span><span class="sxs-lookup"><span data-stu-id="33afe-184">Establish a connection.</span></span>

<span data-ttu-id="33afe-185">連線建立之後，您就能視需要上傳與下載檔案。</span><span class="sxs-lookup"><span data-stu-id="33afe-185">After you have connected you will be able to upload and download files as needed.</span></span> <span data-ttu-id="33afe-186">務必將檔案上傳至根目錄，亦即 `/site/wwwroot`。</span><span class="sxs-lookup"><span data-stu-id="33afe-186">Be sure that you are uploading files to the root directory, which is `/site/wwwroot`.</span></span>

<span data-ttu-id="33afe-187">同時將 `index.php` 與 `createtable.php` 上傳完畢後，瀏覽至 **http://[網站名稱].azurewebsites.net/createtable.php** 為應用程式建立 MySQL 資料表，然後瀏覽至 **http://[網站名稱].azurewebsites.net/index.php** 開始使用該應用程式。</span><span class="sxs-lookup"><span data-stu-id="33afe-187">After uploading both `index.php` and `createtable.php`, browse to **http://[site name].azurewebsites.net/createtable.php** to create the MySQL table for the application, then browse to **http://[site name].azurewebsites.net/index.php** to begin using the application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33afe-188">後續步驟</span><span class="sxs-lookup"><span data-stu-id="33afe-188">Next steps</span></span>
<span data-ttu-id="33afe-189">如需詳細資訊，請參閱 [PHP 開發人員中心](/develop/php/)。</span><span class="sxs-lookup"><span data-stu-id="33afe-189">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

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

