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
# <a name="create-a-php-sql-web-app-and-deploy-tooazure-app-service-using-git"></a><span data-ttu-id="b7fd1-103">建立 PHP SQL web 應用程式和部署 tooAzure 應用程式服務使用 Git</span><span class="sxs-lookup"><span data-stu-id="b7fd1-103">Create a PHP-SQL web app and deploy tooAzure App Service using Git</span></span>
<span data-ttu-id="b7fd1-104">本教學課程告訴您如何 toocreate PHP web 應用程式中的[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)連接 tooAzure SQL Database 以及如何 toodeploy 使用 Git。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-104">This tutorial shows you how toocreate a PHP web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) that connects tooAzure SQL Database and how toodeploy it using Git.</span></span> <span data-ttu-id="b7fd1-105">本教學課程假設您有[PHP][install-php]， [SQL Server Express][install-SQLExpress]，hello [Microsoft Drivers for for PHP SQL Server](http://www.microsoft.com/download/en/details.aspx?id=20098)，和[Git] [ install-git]安裝在電腦上。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-105">This tutorial assumes you have [PHP][install-php], [SQL Server Express][install-SQLExpress], hello [Microsoft Drivers for SQL Server for PHP](http://www.microsoft.com/download/en/details.aspx?id=20098), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="b7fd1-106">完成本指南的步驟後，您將擁有在 Azure 上運作的 PHP-SQL Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-106">Upon completing this guide, you will have a PHP-SQL web app running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="b7fd1-107">您可以安裝和設定 PHP、 SQL Server Express 和 hello Microsoft Drivers for SQL Server 使用 hello PHP [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-107">You can install and configure PHP, SQL Server Express, and hello Microsoft Drivers for SQL Server for PHP using hello [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> 
> 

<span data-ttu-id="b7fd1-108">您將了解：</span><span class="sxs-lookup"><span data-stu-id="b7fd1-108">You will learn:</span></span>

* <span data-ttu-id="b7fd1-109">Toocreate Azure web 應用程式和 SQL 資料庫使用 hello [Azure 入口網站](http://go.microsoft.com/fwlink/?LinkId=529715)。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-109">How toocreate an Azure web app and a SQL Database using hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="b7fd1-110">因為預設 PHP 啟用 App Service Web 應用程式中，沒有特別的是需要的 toorun 您 PHP 程式碼。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-110">Because PHP is enabled in App Service Web Apps by default, nothing special is required toorun your PHP code.</span></span>
* <span data-ttu-id="b7fd1-111">如何 toopublish 並重新發行您的應用程式 tooAzure 使用 Git。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-111">How toopublish and re-publish your application tooAzure using Git.</span></span>

<span data-ttu-id="b7fd1-112">依照本教學課程進行，您將以 PHP 語法建構一個簡單的註冊網頁應用程式。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-112">By following this tutorial, you will build a simple registration web application in PHP.</span></span> <span data-ttu-id="b7fd1-113">hello 應用程式將會裝載於 Azure 網站中。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-113">hello application will be hosted in an Azure Website.</span></span> <span data-ttu-id="b7fd1-114">底下是完成 hello 應用程式的螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="b7fd1-114">A screenshot of hello completed application is below:</span></span>

![Azure PHP Web Site](./media/web-sites-php-sql-database-deploy-use-git/running_app_3.png)

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="b7fd1-116">如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="b7fd1-117">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-an-azure-web-app-and-set-up-git-publishing"></a><span data-ttu-id="b7fd1-118">建立 Azure Web 應用程式並設定 Git 發行功能</span><span class="sxs-lookup"><span data-stu-id="b7fd1-118">Create an Azure web app and set up Git publishing</span></span>
<span data-ttu-id="b7fd1-119">請遵循這些步驟 toocreate Azure web 應用程式和 SQL 資料庫：</span><span class="sxs-lookup"><span data-stu-id="b7fd1-119">Follow these steps toocreate an Azure web app and a SQL Database:</span></span>

1. <span data-ttu-id="b7fd1-120">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-120">Log in toohello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b7fd1-121">Hello，即可開啟 hello Azure Marketplace**新增**hello 上方的圖示左邊 hello 儀表板上，按一下**全選**下一步 tooMarketplace 並選取**Web + 行動**。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-121">Open hello Azure Marketplace by clicking hello **New** icon on hello top left of hello dashboard, click on **Select All** next tooMarketplace and selecting **Web + Mobile**.</span></span>
3. <span data-ttu-id="b7fd1-122">在 hello Marketplace，選取  **Web + 行動**。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-122">In hello Marketplace, select **Web + Mobile**.</span></span>
4. <span data-ttu-id="b7fd1-123">按一下 hello **Web 應用程式 + SQL**圖示。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-123">Click hello **Web app + SQL** icon.</span></span>
5. <span data-ttu-id="b7fd1-124">閱讀後 hello hello Web 應用程式 + SQL 應用程式的描述，選取**建立**。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-124">After reading hello description of hello Web app + SQL app, select **Create**.</span></span>
6. <span data-ttu-id="b7fd1-125">按一下 在每個部分 (**資源群組**， **Web 應用程式**，**資料庫**，和**訂用帳戶**) 然後輸入或選取所需的 hello 的值欄位：</span><span class="sxs-lookup"><span data-stu-id="b7fd1-125">Click on each part (**Resource Group**, **Web App**, **Database**, and **Subscription**) and enter or select values for hello required fields:</span></span>
   
   * <span data-ttu-id="b7fd1-126">輸入您選擇的 URL 名稱</span><span class="sxs-lookup"><span data-stu-id="b7fd1-126">Enter a URL name of your choice</span></span>    
   * <span data-ttu-id="b7fd1-127">設定資料庫伺服器認證</span><span class="sxs-lookup"><span data-stu-id="b7fd1-127">Configure database server credentials</span></span>
   * <span data-ttu-id="b7fd1-128">選取 hello 區域最接近 tooyou</span><span class="sxs-lookup"><span data-stu-id="b7fd1-128">Select hello region closest tooyou</span></span>
     
     ![configure your app](./media/web-sites-php-sql-database-deploy-use-git/configure-db-settings.png)
7. <span data-ttu-id="b7fd1-130">完成定義 hello web 應用程式，請按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-130">When finished defining hello web app, click **Create**.</span></span>
   
    <span data-ttu-id="b7fd1-131">Hello web 應用程式建立後，hello**通知** 按鈕會閃爍綠色**成功**和 hello 資源群組刀鋒視窗中開啟 tooshow 這兩個 hello web 應用程式和 hello SQL database hello 群組中的。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-131">When hello web app has been created, hello **Notifications** button will flash a green **SUCCESS** and hello resource group blade open tooshow both hello web app and hello SQL database in hello group.</span></span>
8. <span data-ttu-id="b7fd1-132">按一下 hello 資源群組 刀鋒視窗 tooopen hello web 應用程式的刀鋒視窗中的 hello web 應用程式的圖示。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-132">Click hello web app's icon in hello resource group blade tooopen hello web app's blade.</span></span>
   
    ![Web 應用程式的資源群組](./media/web-sites-php-sql-database-deploy-use-git/resource-group-blade.png)
9. <span data-ttu-id="b7fd1-134">在 [設定] 中按一下 [繼續部署] > [設定必要設定]。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-134">In **Settings** click **Continuous deployment** > **Configure required settings**.</span></span> <span data-ttu-id="b7fd1-135">選取 [本機 Git 儲存機制]，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-135">Select **Local Git Repository** and click **OK**.</span></span>
   
    ![where is your source code](./media/web-sites-php-sql-database-deploy-use-git/setup-local-git.png)
   
    <span data-ttu-id="b7fd1-137">如果您從未設定 Git 儲存機制，則必須提供使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-137">If you have not set up a Git repository before, you must provide a user name and password.</span></span> <span data-ttu-id="b7fd1-138">toodo 此，依序按一下**設定** > **部署認證**hello web 應用程式的刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-138">toodo this, click **Settings** > **Deployment credentials** in hello web app's blade.</span></span>
   
    ![](./media/web-sites-php-sql-database-deploy-use-git/deployment-credentials.png)
10. <span data-ttu-id="b7fd1-139">在**設定**按一下**屬性**toosee hello Git 遠端 URL 您於稍後 toouse toodeploy PHP 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-139">In **Settings** click on **Properties** toosee hello Git remote URL you need toouse toodeploy your PHP app later.</span></span>

## <a name="get-sql-database-connection-information"></a><span data-ttu-id="b7fd1-140">取得 SQL Database 連線資訊</span><span class="sxs-lookup"><span data-stu-id="b7fd1-140">Get SQL Database connection information</span></span>
<span data-ttu-id="b7fd1-141">tooconnect toohello SQL Database 執行個體的連結 tooyour web 應用程式，您將需要 hello hello 資料庫的建立時指定的連接資訊。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-141">tooconnect toohello SQL Database instance that is linked tooyour web app, your will need hello connection information, which you specified when you created hello database.</span></span> <span data-ttu-id="b7fd1-142">tooget hello SQL 資料庫連接資訊，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b7fd1-142">tooget hello SQL Database connection information, follow these steps:</span></span>

1. <span data-ttu-id="b7fd1-143">在 hello 資源群組的刀鋒視窗中，按一下 hello SQL 資料庫的圖示。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-143">Back in hello resource group's blade, click hello SQL database's icon.</span></span>
2. <span data-ttu-id="b7fd1-144">在 hello SQL database 的刀鋒視窗中，按一下 **設定** > **屬性**，然後按一下 **顯示資料庫的連接字串**。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-144">In hello SQL database's blade, click **Settings** > **Properties**, then click **Show database connection strings**.</span></span> 
   
    ![檢視資料庫屬性](./media/web-sites-php-sql-database-deploy-use-git/view-database-properties.png)
3. <span data-ttu-id="b7fd1-146">從 hello **PHP** > 一節的 hello 產生 對話方塊中，記下的 hello 值`Server`， `SQL Database`，和`User Name`。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-146">From hello **PHP** section of hello resulting dialog, make note of hello values for `Server`, `SQL Database`, and `User Name`.</span></span> <span data-ttu-id="b7fd1-147">您將使用這些值稍後當發行您的 PHP web 應用程式 tooAzure 應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-147">You will use these values later when publishing your PHP web app tooAzure App Service.</span></span>

## <a name="build-and-test-your-application-locally"></a><span data-ttu-id="b7fd1-148">在本機建置與測試您的應用程式</span><span class="sxs-lookup"><span data-stu-id="b7fd1-148">Build and test your application locally</span></span>
<span data-ttu-id="b7fd1-149">hello 註冊應用程式是簡單的 PHP 應用程式，可讓您藉由提供您的名稱和電子郵件地址的 tooregister 事件。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-149">hello Registration application is a simple PHP application that allows you tooregister for an event by providing your name and email address.</span></span> <span data-ttu-id="b7fd1-150">先前的註冊者相關資訊會顯示在資料表中。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-150">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="b7fd1-151">註冊資訊會儲存在 SQL Database 執行個體中。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-151">Registration information is stored in a SQL Database instance.</span></span> <span data-ttu-id="b7fd1-152">hello 應用程式包含兩個檔案 （如下所示複製/貼上程式碼）：</span><span class="sxs-lookup"><span data-stu-id="b7fd1-152">hello application consists of two files (copy/paste code available below):</span></span>

* <span data-ttu-id="b7fd1-153">**index.php**：顯示註冊表單，以及內含註冊者資訊的資料表。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-153">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="b7fd1-154">**createtable.php**: hello SQL 資料庫的建立資料表 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-154">**createtable.php**: Creates hello SQL Database table for hello application.</span></span> <span data-ttu-id="b7fd1-155">只會使用一次此檔案。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-155">This file will only be used once.</span></span>

<span data-ttu-id="b7fd1-156">toorun hello 應用程式在本機，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-156">toorun hello application locally, follow hello steps below.</span></span> <span data-ttu-id="b7fd1-157">請注意，這些步驟假設您有 PHP 和 SQL Server Express 設定在本機電腦，並已啟用 hello [PDO 擴充功能，適用於 SQL Server][pdo-sqlsrv]。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-157">Note that these steps assume you have PHP and SQL Server Express set up on your local machine, and that you have enabled hello [PDO extension for SQL Server][pdo-sqlsrv].</span></span>

1. <span data-ttu-id="b7fd1-158">建立名為 `registration`的 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-158">Create a SQL Server database called `registration`.</span></span> <span data-ttu-id="b7fd1-159">您可以從 hello`sqlcmd`命令提示字元使用這些命令：</span><span class="sxs-lookup"><span data-stu-id="b7fd1-159">You can do this from hello `sqlcmd` command prompt with these commands:</span></span>
   
        >sqlcmd -S localhost\sqlexpress -U <local user name> -P <local password>
        1> create database registration
        2> GO    
2. <span data-ttu-id="b7fd1-160">在應用程式根目錄中建立兩個檔案，一個名為 `createtable.php`，另一個名為 `index.php`。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-160">In your application root directory, create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="b7fd1-161">開啟 hello`createtable.php`在文字編輯器或 IDE 檔案，然後加入下列程式碼 hello。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-161">Open hello `createtable.php` file in a text editor or IDE and add hello code below.</span></span> <span data-ttu-id="b7fd1-162">此程式碼將會使用的 toocreate hello `registration_tbl` hello 中的資料表`registration`資料庫。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-162">This code will be used toocreate hello `registration_tbl` table in hello `registration` database.</span></span>
   
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
   
    <span data-ttu-id="b7fd1-163">請注意，您將需要 tooupdate hello 值<code>$user</code>和<code>$pwd</code>使用您的本機 SQL Server 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-163">Note that you will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local SQL Server user name and password.</span></span>
4. <span data-ttu-id="b7fd1-164">在下列命令 hello 應用程式類型 hello hello 根目錄在終止：</span><span class="sxs-lookup"><span data-stu-id="b7fd1-164">In a terminal at hello root directory of hello application type hello following command:</span></span>
   
        php -S localhost:8000
5. <span data-ttu-id="b7fd1-165">開啟網頁瀏覽器並瀏覽過**http://localhost:8000/createtable.php**。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-165">Open a web browser and browse too**http://localhost:8000/createtable.php**.</span></span> <span data-ttu-id="b7fd1-166">這會建立 hello `registration_tbl` hello 資料庫資料表中的。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-166">This will create hello `registration_tbl` table in hello database.</span></span>
6. <span data-ttu-id="b7fd1-167">開啟 hello**為 index.php**檔案文字編輯器或 IDE 中，然後加入 hello 基本 HTML 和 CSS 程式碼 hello 頁面 （hello PHP 程式碼會在稍後步驟中新增）。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-167">Open hello **index.php** file in a text editor or IDE and add hello basic HTML and CSS code for hello page (hello PHP code will be added in later steps).</span></span>
   
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
7. <span data-ttu-id="b7fd1-168">Hello PHP 標記內加入連接 toohello 資料庫 PHP 程式碼。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-168">Within hello PHP tags, add PHP code for connecting toohello database.</span></span>
   
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
   
    <span data-ttu-id="b7fd1-169">同樣地，您將需要 tooupdate hello 值<code>$user</code>和<code>$pwd</code>本機 MySQL 使用者名稱與密碼。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-169">Again, you will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
8. <span data-ttu-id="b7fd1-170">下列程式碼 hello 資料庫連接，加入程式碼插入 hello 資料庫的註冊資訊。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-170">Following hello database connection code, add code for inserting registration information into hello database.</span></span>
   
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
9. <span data-ttu-id="b7fd1-171">最後，遵循上述的 hello 程式碼，加入程式碼從 hello 資料庫擷取資料。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-171">Finally, following hello code above, add code for retrieving data from hello database.</span></span>
   
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

<span data-ttu-id="b7fd1-172">您現在可以瀏覽過**http://localhost:8000/index.php** tootest hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-172">You can now browse too**http://localhost:8000/index.php** tootest hello application.</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="b7fd1-173">發佈您的應用程式</span><span class="sxs-lookup"><span data-stu-id="b7fd1-173">Publish your application</span></span>
<span data-ttu-id="b7fd1-174">您已經測試過您的應用程式在本機上之後，您可以發行該 tooApp Service Web 應用程式使用 Git。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-174">After you have tested your application locally, you can publish it tooApp Service Web Apps using Git.</span></span> <span data-ttu-id="b7fd1-175">不過，您必須先 tooupdate hello 資料庫 hello 應用程式中的連接資訊。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-175">However, you first need tooupdate hello database connection information in hello application.</span></span> <span data-ttu-id="b7fd1-176">使用您稍早取得的 hello 資料庫連接資訊 (在 hello**取得 SQL 資料庫連接資訊**> 一節)，下列中的資訊更新 hello**兩者**hello`createdatabase.php`和`index.php`檔案以 hello 適當值：</span><span class="sxs-lookup"><span data-stu-id="b7fd1-176">Using hello database connection information you obtained earlier (in hello **Get SQL Database connection information** section), update hello following information in **both** hello `createdatabase.php` and `index.php` files with hello appropriate values:</span></span>

    // DB connection info
    $host = "tcp:<value of Server>";
    $user = "<value of User Name>";
    $pwd = "<your password>";
    $db = "<value of SQL Database>";

> [!NOTE]
> <span data-ttu-id="b7fd1-177">在 hello <code>$host</code>，伺服器 hello 值必須在前面加上與<code>tcp:</code>。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-177">In hello <code>$host</code>, hello value of Server must be prepended with <code>tcp:</code>.</span></span>
> 
> 

<span data-ttu-id="b7fd1-178">現在，您已準備好 tooset 設定 Git 發行功能，並發佈 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-178">Now, you are ready tooset up Git publishing and publish hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="b7fd1-179">這些都是相同的步驟記下在 hello 結尾 hello hello**建立 Azure web 應用程式，並設定 Git 發行功能**上一節。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-179">These are hello same steps noted at hello end of hello **Create an Azure web app and set up Git publishing** section above.</span></span>
> 
> 

1. <span data-ttu-id="b7fd1-180">開啟 GitBash (或終端機，如果 Git 位於您`PATH`)，變更目錄 toohello 根目錄，您的應用程式 (hello**註冊**目錄)，並執行的 hello 遵循命令：</span><span class="sxs-lookup"><span data-stu-id="b7fd1-180">Open GitBash (or a terminal, if Git is in your `PATH`), change directories toohello root directory of your application (hello **registration** directory), and run hello following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="b7fd1-181">安裝程式將會提示您稍早建立的 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-181">You will be prompted for hello password you created earlier.</span></span>
2. <span data-ttu-id="b7fd1-182">瀏覽過**http://[web 應用程式 name].azurewebsites.net/createtable.php** toocreate hello SQL 資料庫資料表 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-182">Browse too**http://[web app name].azurewebsites.net/createtable.php** toocreate hello SQL database table for hello application.</span></span>
3. <span data-ttu-id="b7fd1-183">瀏覽過**http://[web 應用程式 name].azurewebsites.net/index.php** toobegin 使用 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-183">Browse too**http://[web app name].azurewebsites.net/index.php** toobegin using hello application.</span></span>

<span data-ttu-id="b7fd1-184">在發行您的應用程式之後，您可以開始製作變更 tooit，並使用 Git toopublish 它們。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-184">After you have published your application, you can begin making changes tooit and use Git toopublish them.</span></span> 

## <a name="publish-changes-tooyour-application"></a><span data-ttu-id="b7fd1-185">發行變更 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="b7fd1-185">Publish changes tooyour application</span></span>
<span data-ttu-id="b7fd1-186">toopublish 變更 tooapplication，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b7fd1-186">toopublish changes tooapplication, follow these steps:</span></span>

1. <span data-ttu-id="b7fd1-187">變更本機 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-187">Make changes tooyour application locally.</span></span>
2. <span data-ttu-id="b7fd1-188">開啟 GitBash (或終端機中，it Git 是在您`PATH`)，變更目錄 toohello 根目錄，應用程式，並執行 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="b7fd1-188">Open GitBash (or a terminal, it Git is in your `PATH`), change directories toohello root directory of your application, and run hello following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="b7fd1-189">安裝程式將會提示您稍早建立的 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-189">You will be prompted for hello password you created earlier.</span></span>
3. <span data-ttu-id="b7fd1-190">瀏覽過**http://[web 應用程式 name].azurewebsites.net/index.php** toosee 您的變更。</span><span class="sxs-lookup"><span data-stu-id="b7fd1-190">Browse too**http://[web app name].azurewebsites.net/index.php** toosee your changes.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="b7fd1-191">變更的項目</span><span class="sxs-lookup"><span data-stu-id="b7fd1-191">What's changed</span></span>
* <span data-ttu-id="b7fd1-192">從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="b7fd1-192">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[pdo-sqlsrv]: http://php.net/pdo_sqlsrv

