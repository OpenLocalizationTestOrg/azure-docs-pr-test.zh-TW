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
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-git"></a><span data-ttu-id="8ded8-103">在 Azure 應用程式服務中建立 PHP-MySQL Web 應用程式並使用 Git 部署</span><span class="sxs-lookup"><span data-stu-id="8ded8-103">Create a PHP-MySQL web app in Azure App Service and deploy using Git</span></span>
<span data-ttu-id="8ded8-104">本教學課程告訴您如何 toocreate PHP MySQL web 應用程式以及如何 toodeploy 它太[App Service](http://go.microsoft.com/fwlink/?LinkId=529714)使用 Git。</span><span class="sxs-lookup"><span data-stu-id="8ded8-104">This tutorial shows you how toocreate a PHP-MySQL web app and how toodeploy it too[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) using Git.</span></span> <span data-ttu-id="8ded8-105">您將使用[PHP][install-php]，hello MySQL 命令列工具 (屬於[MySQL][install-mysql])，和[Git] [install-git]安裝在電腦上。</span><span class="sxs-lookup"><span data-stu-id="8ded8-105">You will use [PHP][install-php], hello MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="8ded8-106">可在任何作業系統，包括 Windows、 Mac 和 Linux 上遵循本教學課程中的 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="8ded8-106">hello instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="8ded8-107">看完本指南後，您將擁有可在 Azure 上執行的 PHP/MySQL Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8ded8-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="8ded8-108">您將了解：</span><span class="sxs-lookup"><span data-stu-id="8ded8-108">You will learn:</span></span>

* <span data-ttu-id="8ded8-109">如何 toocreate web 應用程式和 MySQL 資料庫使用 hello [Azure 入口網站][management-portal]。</span><span class="sxs-lookup"><span data-stu-id="8ded8-109">How toocreate a web app and a MySQL database using hello [Azure Portal][management-portal].</span></span> <span data-ttu-id="8ded8-110">因為在已啟用的 PHP [App Service Web 應用程式](http://go.microsoft.com/fwlink/?LinkId=529714)根據預設，沒有特別的是必要的 toorun 您 PHP 程式碼。</span><span class="sxs-lookup"><span data-stu-id="8ded8-110">Because PHP is enabled in [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) by default, nothing special is required toorun your PHP code.</span></span>
* <span data-ttu-id="8ded8-111">如何 toopublish 並重新發行您的應用程式 tooAzure 使用 Git。</span><span class="sxs-lookup"><span data-stu-id="8ded8-111">How toopublish and re-publish your application tooAzure using Git.</span></span>
* <span data-ttu-id="8ded8-112">影響 tooenable hello 編輯器延伸模組 tooautomate 作曲者工作在每個`git push`。</span><span class="sxs-lookup"><span data-stu-id="8ded8-112">How tooenable hello Composer extension tooautomate Composer tasks at every `git push`.</span></span>

<span data-ttu-id="8ded8-113">依照本教學課程進行，您將使用 PHP 建置一個簡易的註冊 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8ded8-113">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="8ded8-114">將 Web 應用程式中裝載 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8ded8-114">hello application will be hosted in Web Apps.</span></span> <span data-ttu-id="8ded8-115">底下是完成 hello 應用程式的螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="8ded8-115">A screenshot of hello completed application is below:</span></span>

![Azure PHP web site][running-app]

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="8ded8-117">設定 hello 開發環境</span><span class="sxs-lookup"><span data-stu-id="8ded8-117">Set up hello development environment</span></span>
<span data-ttu-id="8ded8-118">本教學課程假設您有[PHP][install-php]，hello MySQL 命令列工具 (屬於[MySQL][install-mysql])，和[Git] [ install-git]安裝在電腦上。</span><span class="sxs-lookup"><span data-stu-id="8ded8-118">This tutorial assumes you have [PHP][install-php], hello MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span>

<a id="create-web-site-and-set-up-git"></a>

## <a name="create-a-web-app-and-set-up-git-publishing"></a><span data-ttu-id="8ded8-119">建立 Web 應用程式並設定 Git 發行</span><span class="sxs-lookup"><span data-stu-id="8ded8-119">Create a web app and set up Git publishing</span></span>
<span data-ttu-id="8ded8-120">Web 應用程式和 MySQL 資料庫，請遵循這些步驟 toocreate:</span><span class="sxs-lookup"><span data-stu-id="8ded8-120">Follow these steps toocreate a web app and a MySQL database:</span></span>

1. <span data-ttu-id="8ded8-121">登入 toohello [Azure 入口網站][management-portal]。</span><span class="sxs-lookup"><span data-stu-id="8ded8-121">Login toohello [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="8ded8-122">按一下 hello**新增**圖示。</span><span class="sxs-lookup"><span data-stu-id="8ded8-122">Click hello **New** icon.</span></span>
3. <span data-ttu-id="8ded8-123">按一下**看到所有**下一步太**Marketplace**。</span><span class="sxs-lookup"><span data-stu-id="8ded8-123">Click **See All** next too**Marketplace**.</span></span> 
4. <span data-ttu-id="8ded8-124">依序按一下 [Web + 行動] 和 [Web 應用程式 + MySQL]。</span><span class="sxs-lookup"><span data-stu-id="8ded8-124">Click **Web + Mobile**, then **Web app + MySQL**.</span></span> <span data-ttu-id="8ded8-125">然後按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="8ded8-125">Then, click **Create**.</span></span>
5. <span data-ttu-id="8ded8-126">輸入資源群組的有效名稱。</span><span class="sxs-lookup"><span data-stu-id="8ded8-126">Enter a valid name for your resource group.</span></span>
   
    ![設定資源群組名稱][resource-group]
6. <span data-ttu-id="8ded8-128">輸入新 Web 應用程式的值。</span><span class="sxs-lookup"><span data-stu-id="8ded8-128">Enter values for your new web app.</span></span>
   
    ![建立 Web 應用程式][new-web-app]
7. <span data-ttu-id="8ded8-130">輸入新資料庫，包括同意值 toohello 法律條款。</span><span class="sxs-lookup"><span data-stu-id="8ded8-130">Enter values for your new database, including agreeing toohello legal terms.</span></span>
   
    ![建立新的 MySQL 資料庫][new-mysql-db]
8. <span data-ttu-id="8ded8-132">Hello web 應用程式建立後，您會看到 hello 新 web 應用程式 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="8ded8-132">When hello web app has been created, you will see hello new web app blade.</span></span>
9. <span data-ttu-id="8ded8-133">在 [設定] 中按一下 [繼續部署]，然後按一下 [設定必要設定]。</span><span class="sxs-lookup"><span data-stu-id="8ded8-133">In **Settings** click on **Continuous Deployment**, then click on *Configure required settings*.</span></span>
   
    ![設定 Git 發佈][setup-publishing]
10. <span data-ttu-id="8ded8-135">選取**本機 Git 儲存機制**hello 來源。</span><span class="sxs-lookup"><span data-stu-id="8ded8-135">Select **Local Git Repository** for hello source.</span></span>
    
     ![設定 Git 儲存機制][setup-repository]
11. <span data-ttu-id="8ded8-137">tooenable Git 發行，您必須提供使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="8ded8-137">tooenable Git publishing, you must provide a user name and password.</span></span> <span data-ttu-id="8ded8-138">記下的 hello 使用者名稱和您所建立的密碼。</span><span class="sxs-lookup"><span data-stu-id="8ded8-138">Make a note of hello user name and password you create.</span></span> <span data-ttu-id="8ded8-139">)</span><span class="sxs-lookup"><span data-stu-id="8ded8-139">(If you have set up a Git repository before, this step will be skipped.)</span></span>
    
     ![建立發佈認證][credentials]

## <a name="get-remote-mysql-connection-information"></a><span data-ttu-id="8ded8-141">取得遠端 MySQL 連線資訊</span><span class="sxs-lookup"><span data-stu-id="8ded8-141">Get remote MySQL connection information</span></span>
<span data-ttu-id="8ded8-142">在 Web 應用程式，您將執行的 tooconnect toohello MySQL 資料庫需要 hello 連接資訊。</span><span class="sxs-lookup"><span data-stu-id="8ded8-142">tooconnect toohello MySQL database that is running in Web Apps, your will need hello connection information.</span></span> <span data-ttu-id="8ded8-143">tooget MySQL 連接資訊，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8ded8-143">tooget MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="8ded8-144">從資源群組中，按一下 hello 資料庫：</span><span class="sxs-lookup"><span data-stu-id="8ded8-144">From your resource group, click hello database:</span></span>
   
    ![選取資料庫][select-database]
2. <span data-ttu-id="8ded8-146">從 hello 資料庫**設定**，選取**屬性**。</span><span class="sxs-lookup"><span data-stu-id="8ded8-146">From hello database **Settings**, select **Properties**.</span></span>
   
    ![選取屬性][select-properties]
3. <span data-ttu-id="8ded8-148">請記下的 hello 值`Database`， `Host`， `User Id`，和`Password`。</span><span class="sxs-lookup"><span data-stu-id="8ded8-148">Make note of hello values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![注意屬性][note-properties]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="8ded8-150">在本機建置及測試您的應用程式</span><span class="sxs-lookup"><span data-stu-id="8ded8-150">Build and test your app locally</span></span>
<span data-ttu-id="8ded8-151">現在您已經建立了 Web 應用程式，您可以在本機開發自己的應用程式，並在測試後進行部署。</span><span class="sxs-lookup"><span data-stu-id="8ded8-151">Now that you have created a web app, you can develop your application locally, then deploy it after testing.</span></span>

<span data-ttu-id="8ded8-152">hello 註冊應用程式是簡單的 PHP 應用程式，可讓您藉由提供您的名稱和電子郵件地址的 tooregister 事件。</span><span class="sxs-lookup"><span data-stu-id="8ded8-152">hello Registration application is a simple PHP application that allows you tooregister for an event by providing your name and email address.</span></span> <span data-ttu-id="8ded8-153">先前的註冊者相關資訊會顯示在資料表中。</span><span class="sxs-lookup"><span data-stu-id="8ded8-153">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="8ded8-154">註冊資訊會存放在 MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="8ded8-154">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="8ded8-155">hello 應用程式包含一個檔案 （如下所示複製/貼上程式碼）：</span><span class="sxs-lookup"><span data-stu-id="8ded8-155">hello application consists of one file (copy/paste code available below):</span></span>

* <span data-ttu-id="8ded8-156">**index.php**：顯示註冊表單，以及內含註冊者資訊的資料表。</span><span class="sxs-lookup"><span data-stu-id="8ded8-156">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>

<span data-ttu-id="8ded8-157">toobuild 和執行的 hello 應用程式在本機，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="8ded8-157">toobuild and run hello application locally, follow hello steps below.</span></span> <span data-ttu-id="8ded8-158">請注意，這些步驟假設您有 hello PHP 和 MySQL 命令列工具 （MySQL 的一部分） 設定在本機電腦，且您已啟用 hello [PDO MySQL 擴充功能][pdo-mysql]。</span><span class="sxs-lookup"><span data-stu-id="8ded8-158">Note that these steps assume you have hello PHP and MySQL Command-Line Tool (part of MySQL) set up on your local machine, and that you have enabled hello [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="8ded8-159">連接 toohello MySQL 使用遠端伺服器，hello 值`Data Source`， `User Id`， `Password`，和`Database`您稍早擷取：</span><span class="sxs-lookup"><span data-stu-id="8ded8-159">Connect toohello remote MySQL server, using hello value for `Data Source`, `User Id`, `Password`, and `Database` that you retrieved earlier:</span></span>
   
        mysql -h{Data Source] -u[User Id] -p[Password] -D[Database]
2. <span data-ttu-id="8ded8-160">hello MySQL 命令提示字元會出現：</span><span class="sxs-lookup"><span data-stu-id="8ded8-160">hello MySQL command prompt will appear:</span></span>
   
        mysql>
3. <span data-ttu-id="8ded8-161">貼上的 hello 下列`CREATE TABLE`命令 toocreate hello`registration_tbl`資料庫資料表中：</span><span class="sxs-lookup"><span data-stu-id="8ded8-161">Paste in hello following `CREATE TABLE` command toocreate hello `registration_tbl` table in your database:</span></span>
   
        CREATE TABLE registration_tbl(id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(id), name VARCHAR(30), email VARCHAR(30), date DATE);
4. <span data-ttu-id="8ded8-162">Hello 的本機應用程式資料夾的根目錄中建立**為 index.php**檔案。</span><span class="sxs-lookup"><span data-stu-id="8ded8-162">In hello root of your local application folder create **index.php** file.</span></span>
5. <span data-ttu-id="8ded8-163">開啟 hello**為 index.php**檔案文字編輯器或 IDE 中，然後加入 hello 下列程式碼，並且完成 hello 必要的變更標記為`//TODO:`註解。</span><span class="sxs-lookup"><span data-stu-id="8ded8-163">Open hello **index.php** file in a text editor or IDE and add hello following code, and complete hello necessary changes marked with `//TODO:` comments.</span></span>

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

1. <span data-ttu-id="8ded8-164">在終端機移 tooyour 應用程式資料夾，然後輸入 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="8ded8-164">In a terminal go tooyour application folder and type hello following command:</span></span>
   
       php -S localhost:8000

<span data-ttu-id="8ded8-165">您現在可以瀏覽過**: //localhost: 8000 /** tootest hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8ded8-165">You can now browse too**http://localhost:8000/** tootest hello application.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="8ded8-166">發佈您的應用程式</span><span class="sxs-lookup"><span data-stu-id="8ded8-166">Publish your app</span></span>
<span data-ttu-id="8ded8-167">您已經測試過您的應用程式在本機上之後，您可以使用 Git tooWeb 應用程式對它進行發佈。</span><span class="sxs-lookup"><span data-stu-id="8ded8-167">After you have tested your app locally, you can publish it tooWeb Apps using Git.</span></span> <span data-ttu-id="8ded8-168">您將會初始化您的本機 Git 儲存機制和發行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8ded8-168">You will initialize your local Git repository and publish hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="8ded8-169">這些是 hello 相同 hello 結尾 hello hello 建立 web 應用程式的 Azure 入口網站以及組設定 Git 發行上面所示的步驟。</span><span class="sxs-lookup"><span data-stu-id="8ded8-169">These are hello same steps shown in hello Azure Portal at hello end of hello Create a web app and Set up Git Publishing section above.</span></span>
> 
> 

1. <span data-ttu-id="8ded8-170">（選擇性） 如果您遺失或錯置 Git 遠端 repostitory URL，請瀏覽 hello Azure 入口網站上的 toohello web 應用程式屬性。</span><span class="sxs-lookup"><span data-stu-id="8ded8-170">(Optional)  If you've forgotten or misplaced your Git remote repostitory URL, navigate toohello web app properties on hello Azure Portal.</span></span>
2. <span data-ttu-id="8ded8-171">開啟 GitBash (或終端機，如果 Git 位於您`PATH`)，變更目錄 toohello 根目錄，應用程式，並執行 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="8ded8-171">Open GitBash (or a terminal, if Git is in your `PATH`), change directories toohello root directory of your application, and run hello following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="8ded8-172">安裝程式將會提示您稍早建立的 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="8ded8-172">You will be prompted for hello password you created earlier.</span></span>
   
    ![透過 Git 的初始發送 tooAzure][git-initial-push]
3. <span data-ttu-id="8ded8-174">瀏覽過**http://[site name].azurewebsites.net/index.php** toobegin 使用 hello 應用程式 （這項資訊會儲存帳戶儀表板）：</span><span class="sxs-lookup"><span data-stu-id="8ded8-174">Browse too**http://[site name].azurewebsites.net/index.php** toobegin using hello application (this information will be stored on your account dashboard):</span></span>
   
    ![Azure PHP web site][running-app]

<span data-ttu-id="8ded8-176">在發行您的應用程式之後，您可以開始製作變更 tooit，並使用 Git toopublish 它們。</span><span class="sxs-lookup"><span data-stu-id="8ded8-176">After you have published your app, you can begin making changes tooit and use Git toopublish them.</span></span>

## <a name="publish-changes-tooyour-app"></a><span data-ttu-id="8ded8-177">發行變更 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="8ded8-177">Publish changes tooyour app</span></span>
<span data-ttu-id="8ded8-178">toopublish 變更 tooyour 應用程式，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8ded8-178">toopublish changes tooyour app, follow these steps:</span></span>

1. <span data-ttu-id="8ded8-179">請在本機變更 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8ded8-179">Make changes tooyour app locally.</span></span>
2. <span data-ttu-id="8ded8-180">開啟 GitBash (或終端機中，it Git 是在您`PATH`)、 變更目錄 toohello 根目錄，應用程式，並執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="8ded8-180">Open GitBash (or a terminal, it Git is in your `PATH`), change directories toohello root directory of your app, and run hello following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="8ded8-181">安裝程式將會提示您稍早建立的 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="8ded8-181">You will be prompted for hello password you created earlier.</span></span>
   
    ![透過 Git 推送的站台變更 tooAzure][git-change-push]
3. <span data-ttu-id="8ded8-183">瀏覽過**http://[site name].azurewebsites.net/index.php** toosee 應用程式與您所做的變更：</span><span class="sxs-lookup"><span data-stu-id="8ded8-183">Browse too**http://[site name].azurewebsites.net/index.php** toosee your app and any changes you may have made:</span></span>
   
    ![Azure PHP web site][running-app]

> [!NOTE]
> <span data-ttu-id="8ded8-185">如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="8ded8-185">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="8ded8-186">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="8ded8-186">No credit cards required; no commitments.</span></span>
> 
> 

<a name="composer"></a>

## <a name="enable-composer-automation-with-hello-composer-extension"></a><span data-ttu-id="8ded8-187">啟用編輯器自動化以 hello 編輯器延伸模組</span><span class="sxs-lookup"><span data-stu-id="8ded8-187">Enable Composer automation with hello Composer extension</span></span>
<span data-ttu-id="8ded8-188">根據預設，App Service 中的 hello git 部署程序不執行任何動作與 composer.json，如果您有一個 PHP 專案中。</span><span class="sxs-lookup"><span data-stu-id="8ded8-188">By default, hello git deployment process in App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="8ded8-189">您可以啟用 composer.json 處理期間`git push`藉由啟用 hello 編輯器延伸模組。</span><span class="sxs-lookup"><span data-stu-id="8ded8-189">You can enable composer.json processing during `git push` by enabling hello Composer extension.</span></span>

1. <span data-ttu-id="8ded8-190">在您的 PHP web 應用程式的刀鋒視窗中 hello [Azure 入口網站][management-portal]，按一下 **工具** > **延伸**。</span><span class="sxs-lookup"><span data-stu-id="8ded8-190">In your PHP web app's blade in hello [Azure portal][management-portal], click **Tools** > **Extensions**.</span></span>
   
    ![編輯器擴充功能設定][composer-extension-settings]
2. <span data-ttu-id="8ded8-192">按一下 [新增]，然後按一下 [編輯器]。</span><span class="sxs-lookup"><span data-stu-id="8ded8-192">Click **Add**, then click **Composer**.</span></span>
   
    ![編輯器擴充功能新增][composer-extension-add]
3. <span data-ttu-id="8ded8-194">按一下**確定**tooaccept 法律條款。</span><span class="sxs-lookup"><span data-stu-id="8ded8-194">Click **OK** tooaccept legal terms.</span></span> <span data-ttu-id="8ded8-195">按一下**確定**再次 tooadd hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="8ded8-195">Click **OK** again tooadd hello extension.</span></span>
   
    <span data-ttu-id="8ded8-196">hello**擴充功能安裝**刀鋒視窗現在將會顯示 hello 編輯器延伸模組。</span><span class="sxs-lookup"><span data-stu-id="8ded8-196">hello **Installed extensions** blade will now show hello Composer extension.</span></span>  
    <span data-ttu-id="8ded8-197">![編輯器擴充功能檢視][composer-extension-view]</span><span class="sxs-lookup"><span data-stu-id="8ded8-197">![Composer Extension View][composer-extension-view]</span></span>
4. <span data-ttu-id="8ded8-198">現在，執行`git add`， `git commit`，和`git push`如同在 hello 上一節。</span><span class="sxs-lookup"><span data-stu-id="8ded8-198">Now, perform `git add`, `git commit`, and `git push` like in hello previous section.</span></span> <span data-ttu-id="8ded8-199">您就會立即看到編輯器正在安裝 composer.json 中定義的相依性。</span><span class="sxs-lookup"><span data-stu-id="8ded8-199">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![編輯器擴充功能成功][composer-extension-success]

## <a name="next-steps"></a><span data-ttu-id="8ded8-201">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8ded8-201">Next steps</span></span>
<span data-ttu-id="8ded8-202">如需詳細資訊，請參閱 hello [PHP 開發人員中心](/develop/php/)。</span><span class="sxs-lookup"><span data-stu-id="8ded8-202">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

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
