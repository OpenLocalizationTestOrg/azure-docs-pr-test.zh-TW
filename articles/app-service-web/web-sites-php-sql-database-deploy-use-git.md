---
title: "建立 PHP-SQL Web 應用程式並使用 Git 部署至 Azure App Service"
description: "示範如何建立 PHP Web 應用程式將資料儲存於 Azure SQL Database 以及使用 Git 部署至 Azure App Service 的教學課程。"
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
ms.openlocfilehash: 0baa3eced3824fec0907ca937c594f127a2bdf8b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-php-sql-web-app-and-deploy-to-azure-app-service-using-git"></a><span data-ttu-id="b51ab-103">建立 PHP-SQL Web 應用程式並使用 Git 部署至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="b51ab-103">Create a PHP-SQL web app and deploy to Azure App Service using Git</span></span>
<span data-ttu-id="b51ab-104">本教學課程會示範如何在 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) 中建立連線到 Azure SQL Database 的 PHP Web 應用程式，以及如何使用 Git 來部署它。</span><span class="sxs-lookup"><span data-stu-id="b51ab-104">This tutorial shows you how to create a PHP web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) that connects to Azure SQL Database and how to deploy it using Git.</span></span> <span data-ttu-id="b51ab-105">本教學課程假設您的電腦上已安裝 [PHP][install-php]、[SQL Server Express][install-SQLExpress]、[Microsoft Drivers for SQL Server for PHP](http://www.microsoft.com/download/en/details.aspx?id=20098)，和 [Git][install-git]。</span><span class="sxs-lookup"><span data-stu-id="b51ab-105">This tutorial assumes you have [PHP][install-php], [SQL Server Express][install-SQLExpress], the [Microsoft Drivers for SQL Server for PHP](http://www.microsoft.com/download/en/details.aspx?id=20098), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="b51ab-106">完成本指南的步驟後，您將擁有在 Azure 上運作的 PHP-SQL Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b51ab-106">Upon completing this guide, you will have a PHP-SQL web app running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="b51ab-107">您可以使用 [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx)來安裝和設定 PHP、SQL Server Express，和 Microsoft Drivers for SQL Server for PHP。</span><span class="sxs-lookup"><span data-stu-id="b51ab-107">You can install and configure PHP, SQL Server Express, and the Microsoft Drivers for SQL Server for PHP using the [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> 
> 

<span data-ttu-id="b51ab-108">您將了解：</span><span class="sxs-lookup"><span data-stu-id="b51ab-108">You will learn:</span></span>

* <span data-ttu-id="b51ab-109">如何使用 [Azure 入口網站](http://go.microsoft.com/fwlink/?LinkId=529715)建立 Azure Web 應用程式和 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="b51ab-109">How to create an Azure web app and a SQL Database using the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="b51ab-110">由於預設會在 App Service Web Apps 上啟用 PHP，因此您不需要執行任何特殊步驟就能執行 PHP 程式碼。</span><span class="sxs-lookup"><span data-stu-id="b51ab-110">Because PHP is enabled in App Service Web Apps by default, nothing special is required to run your PHP code.</span></span>
* <span data-ttu-id="b51ab-111">如何使用 Git 來發行與重新發行應用程式到 Azure。</span><span class="sxs-lookup"><span data-stu-id="b51ab-111">How to publish and re-publish your application to Azure using Git.</span></span>

<span data-ttu-id="b51ab-112">依照本教學課程進行，您將以 PHP 語法建構一個簡單的註冊網頁應用程式。</span><span class="sxs-lookup"><span data-stu-id="b51ab-112">By following this tutorial, you will build a simple registration web application in PHP.</span></span> <span data-ttu-id="b51ab-113">該應用程式將在 Azure 網站中託管。</span><span class="sxs-lookup"><span data-stu-id="b51ab-113">The application will be hosted in an Azure Website.</span></span> <span data-ttu-id="b51ab-114">完成之應用程式的螢幕擷取畫面如下：</span><span class="sxs-lookup"><span data-stu-id="b51ab-114">A screenshot of the completed application is below:</span></span>

![Azure PHP Web Site](./media/web-sites-php-sql-database-deploy-use-git/running_app_3.png)

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="b51ab-116">如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service](https://azure.microsoft.com/try/app-service/)，即可在 App Service 中立即建立短期入門 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b51ab-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="b51ab-117">不需要信用卡；無需承諾。</span><span class="sxs-lookup"><span data-stu-id="b51ab-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-an-azure-web-app-and-set-up-git-publishing"></a><span data-ttu-id="b51ab-118">建立 Azure Web 應用程式並設定 Git 發行功能</span><span class="sxs-lookup"><span data-stu-id="b51ab-118">Create an Azure web app and set up Git publishing</span></span>
<span data-ttu-id="b51ab-119">請遵循以下步驟來建立 Azure Web 應用程式與 SQL Database：</span><span class="sxs-lookup"><span data-stu-id="b51ab-119">Follow these steps to create an Azure web app and a SQL Database:</span></span>

1. <span data-ttu-id="b51ab-120">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="b51ab-120">Log in to the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b51ab-121">按一下儀表板左上方的 [新增] 圖示開啟 Azure Marketplace，然後按一下 Marketplace 旁的 [全選] 並選取 [Web + 行動]。</span><span class="sxs-lookup"><span data-stu-id="b51ab-121">Open the Azure Marketplace by clicking the **New** icon on the top left of the dashboard, click on **Select All** next to Marketplace and selecting **Web + Mobile**.</span></span>
3. <span data-ttu-id="b51ab-122">在 Marketplace 中，選取 [Web + 行動] 。</span><span class="sxs-lookup"><span data-stu-id="b51ab-122">In the Marketplace, select **Web + Mobile**.</span></span>
4. <span data-ttu-id="b51ab-123">按一下 [Web 應用程式 + SQL]  圖示。</span><span class="sxs-lookup"><span data-stu-id="b51ab-123">Click the **Web app + SQL** icon.</span></span>
5. <span data-ttu-id="b51ab-124">讀取 Web 應用程式 + SQL 應用程式的描述之後，選取 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b51ab-124">After reading the description of the Web app + SQL app, select **Create**.</span></span>
6. <span data-ttu-id="b51ab-125">按一下每個部分 ([資源群組]、[Web 應用程式]、[資料庫] 以及 [訂用帳戶])，然後輸入或選取必填欄位的值：</span><span class="sxs-lookup"><span data-stu-id="b51ab-125">Click on each part (**Resource Group**, **Web App**, **Database**, and **Subscription**) and enter or select values for the required fields:</span></span>
   
   * <span data-ttu-id="b51ab-126">輸入您選擇的 URL 名稱</span><span class="sxs-lookup"><span data-stu-id="b51ab-126">Enter a URL name of your choice</span></span>    
   * <span data-ttu-id="b51ab-127">設定資料庫伺服器認證</span><span class="sxs-lookup"><span data-stu-id="b51ab-127">Configure database server credentials</span></span>
   * <span data-ttu-id="b51ab-128">選取最靠近您的區域</span><span class="sxs-lookup"><span data-stu-id="b51ab-128">Select the region closest to you</span></span>
     
     ![configure your app](./media/web-sites-php-sql-database-deploy-use-git/configure-db-settings.png)
7. <span data-ttu-id="b51ab-130">定義 Web 應用程式完成之後，按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b51ab-130">When finished defining the web app, click **Create**.</span></span>
   
    <span data-ttu-id="b51ab-131">建立 Web 應用程式後，[通知] 按鈕便會閃爍綠色**成功**並開啟資源群組刀鋒視窗，以顯示群組中的 Web 應用程式與 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="b51ab-131">When the web app has been created, the **Notifications** button will flash a green **SUCCESS** and the resource group blade open to show both the web app and the SQL database in the group.</span></span>
8. <span data-ttu-id="b51ab-132">按一下資源群組分頁中的 Web 應用程式圖示，開啟 Web 應用程式分頁。</span><span class="sxs-lookup"><span data-stu-id="b51ab-132">Click the web app's icon in the resource group blade to open the web app's blade.</span></span>
   
    ![Web 應用程式的資源群組](./media/web-sites-php-sql-database-deploy-use-git/resource-group-blade.png)
9. <span data-ttu-id="b51ab-134">在 [設定] 中按一下 [繼續部署] > [設定必要設定]。</span><span class="sxs-lookup"><span data-stu-id="b51ab-134">In **Settings** click **Continuous deployment** > **Configure required settings**.</span></span> <span data-ttu-id="b51ab-135">選取 [本機 Git 儲存機制]，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b51ab-135">Select **Local Git Repository** and click **OK**.</span></span>
   
    ![where is your source code](./media/web-sites-php-sql-database-deploy-use-git/setup-local-git.png)
   
    <span data-ttu-id="b51ab-137">如果您從未設定 Git 儲存機制，則必須提供使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="b51ab-137">If you have not set up a Git repository before, you must provide a user name and password.</span></span> <span data-ttu-id="b51ab-138">若要這樣做，請按一下 Web 應用程式刀鋒視窗中的 [設定] > [部署認證]。</span><span class="sxs-lookup"><span data-stu-id="b51ab-138">To do this, click **Settings** > **Deployment credentials** in the web app's blade.</span></span>
   
    ![](./media/web-sites-php-sql-database-deploy-use-git/deployment-credentials.png)
10. <span data-ttu-id="b51ab-139">在 [設定] 中按一下 [屬性] 以查看稍後部署 PHP 應用程式時需要使用的 Git 遠端 URL。</span><span class="sxs-lookup"><span data-stu-id="b51ab-139">In **Settings** click on **Properties** to see the Git remote URL you need to use to deploy your PHP app later.</span></span>

## <a name="get-sql-database-connection-information"></a><span data-ttu-id="b51ab-140">取得 SQL Database 連線資訊</span><span class="sxs-lookup"><span data-stu-id="b51ab-140">Get SQL Database connection information</span></span>
<span data-ttu-id="b51ab-141">若要連線到連結至 Web 應用程式的 SQL Database 執行個體，您將會需要在建立資料庫時所指定的連線資訊。</span><span class="sxs-lookup"><span data-stu-id="b51ab-141">To connect to the SQL Database instance that is linked to your web app, your will need the connection information, which you specified when you created the database.</span></span> <span data-ttu-id="b51ab-142">若要取得 SQL Database 連接資訊，請依照下列步驟進行：</span><span class="sxs-lookup"><span data-stu-id="b51ab-142">To get the SQL Database connection information, follow these steps:</span></span>

1. <span data-ttu-id="b51ab-143">回到資源群組分頁，按一下 SQL 資料庫的圖示。</span><span class="sxs-lookup"><span data-stu-id="b51ab-143">Back in the resource group's blade, click the SQL database's icon.</span></span>
2. <span data-ttu-id="b51ab-144">在 SQL 資料庫刀鋒視窗中，按一下 [設定] > [屬性]，然後按一下 [顯示資料庫連線字串]。</span><span class="sxs-lookup"><span data-stu-id="b51ab-144">In the SQL database's blade, click **Settings** > **Properties**, then click **Show database connection strings**.</span></span> 
   
    ![檢視資料庫屬性](./media/web-sites-php-sql-database-deploy-use-git/view-database-properties.png)
3. <span data-ttu-id="b51ab-146">從所產生對話方塊的 [PHP]**PHP** 區段中，請記下 `Server`、`SQL Database` 和 `User Name` 的值。</span><span class="sxs-lookup"><span data-stu-id="b51ab-146">From the **PHP** section of the resulting dialog, make note of the values for `Server`, `SQL Database`, and `User Name`.</span></span> <span data-ttu-id="b51ab-147">稍後將 PHP Web 應用程式發行至 Azure App Service 時，您將使用這些值。</span><span class="sxs-lookup"><span data-stu-id="b51ab-147">You will use these values later when publishing your PHP web app to Azure App Service.</span></span>

## <a name="build-and-test-your-application-locally"></a><span data-ttu-id="b51ab-148">在本機建置與測試您的應用程式</span><span class="sxs-lookup"><span data-stu-id="b51ab-148">Build and test your application locally</span></span>
<span data-ttu-id="b51ab-149">註冊應用程式是一項簡單的 PHP 應用程式，您只需提供名稱與電子郵件地址就能註冊活動。</span><span class="sxs-lookup"><span data-stu-id="b51ab-149">The Registration application is a simple PHP application that allows you to register for an event by providing your name and email address.</span></span> <span data-ttu-id="b51ab-150">先前的註冊者相關資訊會顯示在資料表中。</span><span class="sxs-lookup"><span data-stu-id="b51ab-150">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="b51ab-151">註冊資訊會儲存在 SQL Database 執行個體中。</span><span class="sxs-lookup"><span data-stu-id="b51ab-151">Registration information is stored in a SQL Database instance.</span></span> <span data-ttu-id="b51ab-152">該應用程式包含兩個檔案 (複製/貼上以下提供的程式碼)：</span><span class="sxs-lookup"><span data-stu-id="b51ab-152">The application consists of two files (copy/paste code available below):</span></span>

* <span data-ttu-id="b51ab-153">**index.php**：顯示註冊表單，以及內含註冊者資訊的資料表。</span><span class="sxs-lookup"><span data-stu-id="b51ab-153">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="b51ab-154">**createtable.php**：為應用程式建立 SQL 資料表。</span><span class="sxs-lookup"><span data-stu-id="b51ab-154">**createtable.php**: Creates the SQL Database table for the application.</span></span> <span data-ttu-id="b51ab-155">只會使用一次此檔案。</span><span class="sxs-lookup"><span data-stu-id="b51ab-155">This file will only be used once.</span></span>

<span data-ttu-id="b51ab-156">若要在本機執行應用程式，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="b51ab-156">To run the application locally, follow the steps below.</span></span> <span data-ttu-id="b51ab-157">請注意，這些步驟假設您的本機電腦上已設定 PHP、SQL Server Express，且您已啟用 [SQL Server 的 PDO 延伸模組][pdo-sqlsrv]。</span><span class="sxs-lookup"><span data-stu-id="b51ab-157">Note that these steps assume you have PHP and SQL Server Express set up on your local machine, and that you have enabled the [PDO extension for SQL Server][pdo-sqlsrv].</span></span>

1. <span data-ttu-id="b51ab-158">建立名為 `registration`的 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="b51ab-158">Create a SQL Server database called `registration`.</span></span> <span data-ttu-id="b51ab-159">您可以從 `sqlcmd` 命令提示字元中使用下列命令來建立此資料庫：</span><span class="sxs-lookup"><span data-stu-id="b51ab-159">You can do this from the `sqlcmd` command prompt with these commands:</span></span>
   
        >sqlcmd -S localhost\sqlexpress -U <local user name> -P <local password>
        1> create database registration
        2> GO    
2. <span data-ttu-id="b51ab-160">在應用程式根目錄中建立兩個檔案，一個名為 `createtable.php`，另一個名為 `index.php`。</span><span class="sxs-lookup"><span data-stu-id="b51ab-160">In your application root directory, create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="b51ab-161">在文字編輯器或 IDE 中開啟 `createtable.php` 檔案，加入下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="b51ab-161">Open the `createtable.php` file in a text editor or IDE and add the code below.</span></span> <span data-ttu-id="b51ab-162">此程式碼將會在 `registration` 資料庫中用於建立 `registration_tbl` 資料表。</span><span class="sxs-lookup"><span data-stu-id="b51ab-162">This code will be used to create the `registration_tbl` table in the `registration` database.</span></span>
   
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
   
    <span data-ttu-id="b51ab-163">請注意，您將需要更新的值<code>$user</code>和<code>$pwd</code>使用您的本機 SQL Server 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="b51ab-163">Note that you will need to update the values for <code>$user</code> and <code>$pwd</code> with your local SQL Server user name and password.</span></span>
4. <span data-ttu-id="b51ab-164">在終端機中，於應用程式的根目錄輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="b51ab-164">In a terminal at the root directory of the application type the following command:</span></span>
   
        php -S localhost:8000
5. <span data-ttu-id="b51ab-165">開啟網頁瀏覽器並瀏覽至 **http://localhost:8000/createtable.php**。</span><span class="sxs-lookup"><span data-stu-id="b51ab-165">Open a web browser and browse to **http://localhost:8000/createtable.php**.</span></span> <span data-ttu-id="b51ab-166">這會在資料庫中建立 `registration_tbl` 資料表。</span><span class="sxs-lookup"><span data-stu-id="b51ab-166">This will create the `registration_tbl` table in the database.</span></span>
6. <span data-ttu-id="b51ab-167">在文字編輯器或 IDE 中開啟 **index.php** 檔案，加入頁面的基本 HTML 和 CSS 程式碼 (稍後的步驟中將加入 PHP 程式碼)。</span><span class="sxs-lookup"><span data-stu-id="b51ab-167">Open the **index.php** file in a text editor or IDE and add the basic HTML and CSS code for the page (the PHP code will be added in later steps).</span></span>
   
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
7. <span data-ttu-id="b51ab-168">在 PHP 標籤內，加入用來連線至資料庫的 PHP 程式碼。</span><span class="sxs-lookup"><span data-stu-id="b51ab-168">Within the PHP tags, add PHP code for connecting to the database.</span></span>
   
        // DB connection info
        $host = "localhost\sqlexpress";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect to database.
        try {
            $conn = new PDO( "sqlsrv:Server= $host ; Database = $db ", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
    <span data-ttu-id="b51ab-169">同樣地，您將需要更新的值<code>$user</code>和<code>$pwd</code>本機 MySQL 使用者名稱與密碼。</span><span class="sxs-lookup"><span data-stu-id="b51ab-169">Again, you will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
8. <span data-ttu-id="b51ab-170">在資料庫連接程式碼後面，加入可將登錄資訊插入至資料庫的程式碼。</span><span class="sxs-lookup"><span data-stu-id="b51ab-170">Following the database connection code, add code for inserting registration information into the database.</span></span>
   
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
9. <span data-ttu-id="b51ab-171">最後，在上述程式碼後面，加入可從資料庫擷取資料的程式碼。</span><span class="sxs-lookup"><span data-stu-id="b51ab-171">Finally, following the code above, add code for retrieving data from the database.</span></span>
   
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

<span data-ttu-id="b51ab-172">您現在可以瀏覽至 **http://localhost:8000/index.php** 測試應用程式。</span><span class="sxs-lookup"><span data-stu-id="b51ab-172">You can now browse to **http://localhost:8000/index.php** to test the application.</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="b51ab-173">發行您的應用程式</span><span class="sxs-lookup"><span data-stu-id="b51ab-173">Publish your application</span></span>
<span data-ttu-id="b51ab-174">當您在本機完成應用程式測試之後，就可以使用 Git 將其發行至 App Service Web Apps。</span><span class="sxs-lookup"><span data-stu-id="b51ab-174">After you have tested your application locally, you can publish it to App Service Web Apps using Git.</span></span> <span data-ttu-id="b51ab-175">不過，首先您需要更新應用程式中的資料庫連線資訊。</span><span class="sxs-lookup"><span data-stu-id="b51ab-175">However, you first need to update the database connection information in the application.</span></span> <span data-ttu-id="b51ab-176">使用您稍早取得的資料庫連線資訊 (在＜**取得 SQL Database 連線資訊**＞一節中)，將 `createdatabase.php` 和 `index.php`**「兩者」**檔案中的下列資訊都更新為適當的值：</span><span class="sxs-lookup"><span data-stu-id="b51ab-176">Using the database connection information you obtained earlier (in the **Get SQL Database connection information** section), update the following information in **both** the `createdatabase.php` and `index.php` files with the appropriate values:</span></span>

    // DB connection info
    $host = "tcp:<value of Server>";
    $user = "<value of User Name>";
    $pwd = "<your password>";
    $db = "<value of SQL Database>";

> [!NOTE]
> <span data-ttu-id="b51ab-177">在<code>$host</code>，伺服器的值必須在前面加上與<code>tcp:</code>。</span><span class="sxs-lookup"><span data-stu-id="b51ab-177">In the <code>$host</code>, the value of Server must be prepended with <code>tcp:</code>.</span></span>
> 
> 

<span data-ttu-id="b51ab-178">現在，您可以準備設定 Git 發行，並發行應用程式。</span><span class="sxs-lookup"><span data-stu-id="b51ab-178">Now, you are ready to set up Git publishing and publish the application.</span></span>

> [!NOTE]
> <span data-ttu-id="b51ab-179">這些步驟與前述＜**建立 Azure Web 應用程式並設定 Git 發行功能**＞一節中最後面的步驟相同。</span><span class="sxs-lookup"><span data-stu-id="b51ab-179">These are the same steps noted at the end of the **Create an Azure web app and set up Git publishing** section above.</span></span>
> 
> 

1. <span data-ttu-id="b51ab-180">開啟 GitBash (如果 Git 位於您的 `PATH`，則為終端機)，將目錄變更為應用程式的根目錄 ( **registration** 目錄)，並執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="b51ab-180">Open GitBash (or a terminal, if Git is in your `PATH`), change directories to the root directory of your application (the **registration** directory), and run the following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="b51ab-181">系統會提示您輸入先前建立的密碼。</span><span class="sxs-lookup"><span data-stu-id="b51ab-181">You will be prompted for the password you created earlier.</span></span>
2. <span data-ttu-id="b51ab-182">瀏覽至 **http://[web 應用程式名稱].azurewebsites.net/createtable.php**，建立應用程式的 SQL 資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="b51ab-182">Browse to **http://[web app name].azurewebsites.net/createtable.php** to create the SQL database table for the application.</span></span>
3. <span data-ttu-id="b51ab-183">瀏覽至 **http://[web 應用程式名稱].azurewebsites.net/index.php**，開始使用應用程式。</span><span class="sxs-lookup"><span data-stu-id="b51ab-183">Browse to **http://[web app name].azurewebsites.net/index.php** to begin using the application.</span></span>

<span data-ttu-id="b51ab-184">發行應用程式之後，您可以開始對其進行變更，並使用 Git 來發行它們。</span><span class="sxs-lookup"><span data-stu-id="b51ab-184">After you have published your application, you can begin making changes to it and use Git to publish them.</span></span> 

## <a name="publish-changes-to-your-application"></a><span data-ttu-id="b51ab-185">將變更發行至您的應用程式</span><span class="sxs-lookup"><span data-stu-id="b51ab-185">Publish changes to your application</span></span>
<span data-ttu-id="b51ab-186">若要將變更發行至應用程式，請依照以下步驟進行：</span><span class="sxs-lookup"><span data-stu-id="b51ab-186">To publish changes to application, follow these steps:</span></span>

1. <span data-ttu-id="b51ab-187">在本機對您的應用程式進行變更。</span><span class="sxs-lookup"><span data-stu-id="b51ab-187">Make changes to your application locally.</span></span>
2. <span data-ttu-id="b51ab-188">開啟 GitBash (如果 Git 位於您的 `PATH`，則為終端機)，將目錄變更為應用程式的根目錄，並執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="b51ab-188">Open GitBash (or a terminal, it Git is in your `PATH`), change directories to the root directory of your application, and run the following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="b51ab-189">系統會提示您輸入先前建立的密碼。</span><span class="sxs-lookup"><span data-stu-id="b51ab-189">You will be prompted for the password you created earlier.</span></span>
3. <span data-ttu-id="b51ab-190">瀏覽至 **http://[web 應用程式名稱].azurewebsites.net/index.php** 以查看您的變更。</span><span class="sxs-lookup"><span data-stu-id="b51ab-190">Browse to **http://[web app name].azurewebsites.net/index.php** to see your changes.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="b51ab-191">變更的項目</span><span class="sxs-lookup"><span data-stu-id="b51ab-191">What's changed</span></span>
* <span data-ttu-id="b51ab-192">如需從網站變更為 App Service 的指南，請參閱： [Azure App Service 及其對現有 Azure 服務的影響](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="b51ab-192">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[pdo-sqlsrv]: http://php.net/pdo_sqlsrv

