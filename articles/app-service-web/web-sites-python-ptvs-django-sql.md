---
title: "aaaDjango 和使用 Python Tools 2.2 for Visual Studio 在 Azure 上的 SQL Database"
description: "了解如何 toouse hello Python Tools for Visual Studio toocreate Django web 應用程式將資料儲存在 SQL 資料庫執行個體中，並將其部署 tooAzure App Service Web 應用程式。"
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 3a677e64-b5a9-4d43-b9c0-66246368b483
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: b5b2ef4f3292e7df85007465c5394c8660a7d231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="5e27d-103">Azure 上使用 Python Tools 2.2 for Visual Studio 的 Django 和 SQL Database</span><span class="sxs-lookup"><span data-stu-id="5e27d-103">Django and SQL Database on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="5e27d-104">在此教學課程中，我們將使用[Python Tools for Visual Studio] toocreate 簡單輪詢 web 應用程式使用其中一個 hello PTVS 範例範本。</span><span class="sxs-lookup"><span data-stu-id="5e27d-104">In this tutorial, we'll use [Python Tools for Visual Studio] toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="5e27d-105">本教學課程也提供 [教學影片](https://www.youtube.com/watch?v=ZwcoGcIeHF4)。</span><span class="sxs-lookup"><span data-stu-id="5e27d-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span></span>

<span data-ttu-id="5e27d-106">我們會了解如何 toouse SQL 資料庫裝載在 Azure 上、 如何 tooconfigure 會 hello web 應用程式 toouse SQL 資料庫，以及如何 toopublish hello web 應用程式太[Azure App Service Web 應用程式](http://go.microsoft.com/fwlink/?LinkId=529714)。</span><span class="sxs-lookup"><span data-stu-id="5e27d-106">We'll learn how toouse a SQL database hosted on Azure, how tooconfigure hello web app toouse a SQL database, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="5e27d-107">請參閱 hello [Python 開發人員中心]涵蓋 Azure App Service Web 應用程式與使用 Bottle PTVS 開發的多個發行項，酒瓶和 Django web 架構，來使用 Azure 資料表儲存體、 MySQL 及 SQL Database 服務。</span><span class="sxs-lookup"><span data-stu-id="5e27d-107">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="5e27d-108">本文著重在應用程式服務，而開發時 hello 步驟均相似[Azure 雲端服務]。</span><span class="sxs-lookup"><span data-stu-id="5e27d-108">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e27d-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="5e27d-109">Prerequisites</span></span>
* <span data-ttu-id="5e27d-110">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="5e27d-110">Visual Studio 2015</span></span>
* <span data-ttu-id="5e27d-111">[Python 2.7 (32 位元)]</span><span class="sxs-lookup"><span data-stu-id="5e27d-111">[Python 2.7 32-bit]</span></span>
* <span data-ttu-id="5e27d-112">[Python Tools 2.2 for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="5e27d-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="5e27d-113">[Python Tools 2.2 for Visual Studio 範例 VSIX]</span><span class="sxs-lookup"><span data-stu-id="5e27d-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="5e27d-114">[Azure SDK Tools for VS 2015]</span><span class="sxs-lookup"><span data-stu-id="5e27d-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="5e27d-115">Django 1.9 或更新版本</span><span class="sxs-lookup"><span data-stu-id="5e27d-115">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="5e27d-116">如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="5e27d-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="5e27d-117">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="5e27d-117">No credit cards required; no commitments.</span></span>
>
>

## <a name="create-hello-project"></a><span data-ttu-id="5e27d-118">建立 hello 專案</span><span class="sxs-lookup"><span data-stu-id="5e27d-118">Create hello Project</span></span>
<span data-ttu-id="5e27d-119">在這一節中，我們將使用範例範本建立 Visual Studio 專案。</span><span class="sxs-lookup"><span data-stu-id="5e27d-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="5e27d-120">我們將建立虛擬環境並安裝必要的套件。</span><span class="sxs-lookup"><span data-stu-id="5e27d-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="5e27d-121">我們將使用 sqlite 建立本機資料庫。</span><span class="sxs-lookup"><span data-stu-id="5e27d-121">We'll create a local database using sqlite.</span></span> <span data-ttu-id="5e27d-122">然後我們將在本機執行 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e27d-122">Then we'll run hello web app locally.</span></span>

1. <span data-ttu-id="5e27d-123">在 Visual Studio 中，選取 [檔案]、[新增專案]。</span><span class="sxs-lookup"><span data-stu-id="5e27d-123">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="5e27d-124">hello 專案範本從 hello [Python Tools 2.2 for Visual Studio 範例 VSIX]底下可使用**Python**，**範例**。</span><span class="sxs-lookup"><span data-stu-id="5e27d-124">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="5e27d-125">選取**輪詢 Django Web 專案**然後按一下 [確定] toocreate hello 專案。</span><span class="sxs-lookup"><span data-stu-id="5e27d-125">Select **Polls Django Web Project** and click OK toocreate hello project.</span></span>

     ![New Project Dialog](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. <span data-ttu-id="5e27d-127">系統會提示的 tooinstall 外部的封裝。</span><span class="sxs-lookup"><span data-stu-id="5e27d-127">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="5e27d-128">選取 [安裝到虛擬環境] 。</span><span class="sxs-lookup"><span data-stu-id="5e27d-128">Select **Install into a virtual environment**.</span></span>

     ![外部套件對話方塊](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="5e27d-130">選取**Python 2.7**為 hello 基底直譯器。</span><span class="sxs-lookup"><span data-stu-id="5e27d-130">Select **Python 2.7** as hello base interpreter.</span></span>

     ![新增虛擬環境對話方塊](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="5e27d-132">在**方案總管 中**，hello 專案節點上按一下滑鼠右鍵，然後選取**Python**，然後選取**Django 移轉**。</span><span class="sxs-lookup"><span data-stu-id="5e27d-132">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="5e27d-133">然後選取 [Django 建立超級使用者] 。</span><span class="sxs-lookup"><span data-stu-id="5e27d-133">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="5e27d-134">這會開啟 Django 管理主控台，並在 hello 專案資料夾中建立 sqlite 資料庫。</span><span class="sxs-lookup"><span data-stu-id="5e27d-134">This will open a Django Management Console and create a sqlite database in hello project folder.</span></span> <span data-ttu-id="5e27d-135">請遵循 hello 提示 toocreate 使用者。</span><span class="sxs-lookup"><span data-stu-id="5e27d-135">Follow hello prompts toocreate a user.</span></span>
7. <span data-ttu-id="5e27d-136">確認 hello 應用程式運作方式是按<kbd>F5</kbd>。</span><span class="sxs-lookup"><span data-stu-id="5e27d-136">Confirm that hello application works by pressing <kbd>F5</kbd>.</span></span>
8. <span data-ttu-id="5e27d-137">按一下**登入**hello 導覽列頂端 hello。</span><span class="sxs-lookup"><span data-stu-id="5e27d-137">Click **Log in** from hello navigation bar at hello top.</span></span>

     ![Web Browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="5e27d-139">Hello hello 資料庫進行同步處理時所建立的使用者輸入 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="5e27d-139">Enter hello credentials for hello user you created when you synchronized hello database.</span></span>

     ![Web Browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="5e27d-141">按一下 [Create Sample Polls] 。</span><span class="sxs-lookup"><span data-stu-id="5e27d-141">Click **Create Sample Polls**.</span></span>

      ![Web Browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="5e27d-143">按一下民調並進行投票。</span><span class="sxs-lookup"><span data-stu-id="5e27d-143">Click on a poll and vote.</span></span>

      ![Web Browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a><span data-ttu-id="5e27d-145">建立 SQL Database</span><span class="sxs-lookup"><span data-stu-id="5e27d-145">Create a SQL Database</span></span>
<span data-ttu-id="5e27d-146">Hello 資料庫，我們將建立 Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="5e27d-146">For hello database, we'll create an Azure SQL database.</span></span>

<span data-ttu-id="5e27d-147">您可以依照下列步驟來建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="5e27d-147">You can create a database by following these steps.</span></span>

1. <span data-ttu-id="5e27d-148">登入 hello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="5e27d-148">Log into hello [Azure Portal].</span></span>
2. <span data-ttu-id="5e27d-149">在 hello hello 瀏覽窗格底部，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="5e27d-149">At hello bottom of hello navigation pane, click **NEW**.</span></span> <span data-ttu-id="5e27d-150">接著，按一下 [資料 + 儲存體] > [Azure Marketplace]。</span><span class="sxs-lookup"><span data-stu-id="5e27d-150">, click **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="5e27d-151">設定新的 SQL Database hello 藉由建立新的資源群組和選取 hello 為它的適當位置。</span><span class="sxs-lookup"><span data-stu-id="5e27d-151">Configure hello new SQL Database by creating a new resource group and select hello appropriate location for it.</span></span>
4. <span data-ttu-id="5e27d-152">Hello SQL 資料庫建立之後，按一下**Visual Studio 中開啟**hello 資料庫刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="5e27d-152">Once hello SQL Database is created, click **Open in Visual Studio** in hello database blade.</span></span>
5. <span data-ttu-id="5e27d-153">按一下 [設定防火牆] 。</span><span class="sxs-lookup"><span data-stu-id="5e27d-153">Click **Configure your firewall**.</span></span>
6. <span data-ttu-id="5e27d-154">在 hello**防火牆設定**刀鋒視窗中，新增的防火牆規則**起始 IP**和**結束 IP** toohello 公用 IP 位址在開發電腦的設定。</span><span class="sxs-lookup"><span data-stu-id="5e27d-154">In hello **Firewall Settings** blade, add a firewall rule with **START IP** and **END IP** set toohello public IP address of your development machine.</span></span> <span data-ttu-id="5e27d-155">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="5e27d-155">Click **Save**.</span></span>

   <span data-ttu-id="5e27d-156">這可讓您在開發電腦的連線 toohello 資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="5e27d-156">This will allow connections toohello database server from your development machine.</span></span>
7. <span data-ttu-id="5e27d-157">在 hello 資料庫刀鋒視窗中，按一下 **屬性**，然後按一下 **顯示資料庫的連接字串**。</span><span class="sxs-lookup"><span data-stu-id="5e27d-157">Back in hello database blade, click **Properties**, then click **Show database connection strings**.</span></span>
8. <span data-ttu-id="5e27d-158">使用 hello 複製按鈕 tooput hello 值**ADO.NET** hello 剪貼簿上。</span><span class="sxs-lookup"><span data-stu-id="5e27d-158">Use hello copy button tooput hello value of **ADO.NET** on hello clipboard.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="5e27d-159">設定 hello 專案</span><span class="sxs-lookup"><span data-stu-id="5e27d-159">Configure hello Project</span></span>
<span data-ttu-id="5e27d-160">在本節中，我們會將設定我們 web 應用程式 toouse hello SQL database 剛才所建立。</span><span class="sxs-lookup"><span data-stu-id="5e27d-160">In this section, we'll configure our web app toouse hello SQL database we just created.</span></span> <span data-ttu-id="5e27d-161">我們也會使用如 Django 安裝其他的 Python 封裝需要的 toouse SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="5e27d-161">We'll also install additional Python packages required toouse SQL databases with Django.</span></span> <span data-ttu-id="5e27d-162">然後我們將在本機執行 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e27d-162">Then we'll run hello web app locally.</span></span>

1. <span data-ttu-id="5e27d-163">在 Visual Studio 中開啟**settings.py**，從 hello *ProjectName*資料夾。</span><span class="sxs-lookup"><span data-stu-id="5e27d-163">In Visual Studio, open **settings.py**, from hello *ProjectName* folder.</span></span> <span data-ttu-id="5e27d-164">暫時貼上 hello 編輯器中的 hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="5e27d-164">Temporarily paste hello connection string in hello editor.</span></span> <span data-ttu-id="5e27d-165">hello 連接字串是以下列格式：</span><span class="sxs-lookup"><span data-stu-id="5e27d-165">hello connection string is in this format:</span></span>

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

<span data-ttu-id="5e27d-166">編輯的 hello 定義`DATABASES`toouse hello 上述的值。</span><span class="sxs-lookup"><span data-stu-id="5e27d-166">Edit hello definition of `DATABASES` toouse hello values above.</span></span>

        DATABASES = {
            'default': {
                'ENGINE': 'sql_server.pyodbc',
                'NAME': '<DatabaseName>',
                'USER': '<UserName>',
                'PASSWORD': '{your_password_here}',
                'HOST': '<ServerName>',
                'PORT': '<ServerPort>',
                'OPTIONS': {
                    'driver': 'SQL Server Native Client 11.0',
                    'MARS_Connection': 'True',
                }
            }
        }

1. <span data-ttu-id="5e27d-167">在 方案總管下**Python 環境**，以滑鼠右鍵按一下 hello 虛擬環境，然後選取**安裝 Python 封裝**。</span><span class="sxs-lookup"><span data-stu-id="5e27d-167">In Solution Explorer, under **Python Environments**, right-click on hello virtual environment and select **Install Python Package**.</span></span>
2. <span data-ttu-id="5e27d-168">安裝套件 hello`pyodbc`使用**pip**。</span><span class="sxs-lookup"><span data-stu-id="5e27d-168">Install hello package `pyodbc` using **pip**.</span></span>

     ![安裝 Python 封裝對話方塊](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. <span data-ttu-id="5e27d-170">安裝套件 hello`django-pyodbc-azure`使用**pip**。</span><span class="sxs-lookup"><span data-stu-id="5e27d-170">Install hello package `django-pyodbc-azure` using **pip**.</span></span>

     ![安裝 Python 封裝對話方塊](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. <span data-ttu-id="5e27d-172">在**方案總管 中**，hello 專案節點上按一下滑鼠右鍵，然後選取**Python**，然後選取**Django 移轉**。</span><span class="sxs-lookup"><span data-stu-id="5e27d-172">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="5e27d-173">然後選取 [Django 建立超級使用者] 。</span><span class="sxs-lookup"><span data-stu-id="5e27d-173">Then select **Django Create Superuser**.</span></span>

   <span data-ttu-id="5e27d-174">這會建立 hello hello hello 上一節中建立的 SQL database 的資料表。</span><span class="sxs-lookup"><span data-stu-id="5e27d-174">This will create hello tables for hello SQL database we created in hello previous section.</span></span> <span data-ttu-id="5e27d-175">請遵循 hello 提示 toocreate 建立 hello 第一個區段中的 hello sqlite 資料庫中沒有 toomatch hello 使用者的使用者。</span><span class="sxs-lookup"><span data-stu-id="5e27d-175">Follow hello prompts toocreate a user, which doesn't have toomatch hello user in hello sqlite database created in hello first section.</span></span>
5. <span data-ttu-id="5e27d-176">執行與 hello 應用程式`F5`。</span><span class="sxs-lookup"><span data-stu-id="5e27d-176">Run hello application with `F5`.</span></span> <span data-ttu-id="5e27d-177">利用所建立的輪詢**建立範例輪詢**和送出的投票 hello 資料會序列化 hello SQL 資料庫中。</span><span class="sxs-lookup"><span data-stu-id="5e27d-177">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in hello SQL database.</span></span>

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="5e27d-178">發行 hello web 應用程式 tooAzure 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="5e27d-178">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="5e27d-179">hello Azure.NET SDK 提供簡單的方式 toodeploy 您 web web 應用程式 tooAzure App Service Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e27d-179">hello Azure .NET SDK provides an easy way toodeploy your web web app tooAzure App Service Web Apps.</span></span>

1. <span data-ttu-id="5e27d-180">在**方案總管 中**，hello 專案節點上按一下滑鼠右鍵，然後選取**發行**。</span><span class="sxs-lookup"><span data-stu-id="5e27d-180">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>

     ![發行 Web 對話方塊](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="5e27d-182">按一下 [Microsoft Azure Web Apps] 。</span><span class="sxs-lookup"><span data-stu-id="5e27d-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="5e27d-183">按一下**新增**toocreate 新的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e27d-183">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="5e27d-184">填寫下列欄位的 hello，並按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="5e27d-184">Fill in hello following fields and click **Create**.</span></span>

   * <span data-ttu-id="5e27d-185">**Web 應用程式名稱**</span><span class="sxs-lookup"><span data-stu-id="5e27d-185">**Web App name**</span></span>
   * <span data-ttu-id="5e27d-186">**App Service 計劃**</span><span class="sxs-lookup"><span data-stu-id="5e27d-186">**App Service plan**</span></span>
   * <span data-ttu-id="5e27d-187">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="5e27d-187">**Resource group**</span></span>
   * <span data-ttu-id="5e27d-188">**區域**</span><span class="sxs-lookup"><span data-stu-id="5e27d-188">**Region**</span></span>
   * <span data-ttu-id="5e27d-189">保留**資料庫伺服器**設定得**沒有資料庫**</span><span class="sxs-lookup"><span data-stu-id="5e27d-189">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="5e27d-190">接受所有其他預設值並按一下 [發佈] 。</span><span class="sxs-lookup"><span data-stu-id="5e27d-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="5e27d-191">網頁瀏覽器會自動開啟 toohello 已發佈的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e27d-191">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="5e27d-192">您應該看到 hello web 應用程式工作，如預期般，使用 hello **SQL**裝載於 Azure 的資料庫。</span><span class="sxs-lookup"><span data-stu-id="5e27d-192">You should see hello web app working as expected, using hello **SQL** database hosted on Azure.</span></span>

   <span data-ttu-id="5e27d-193">恭喜！</span><span class="sxs-lookup"><span data-stu-id="5e27d-193">Congratulations!</span></span>

     ![Web Browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="5e27d-195">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5e27d-195">Next steps</span></span>
<span data-ttu-id="5e27d-196">遵循這些連結 toolearn 更多關於 Python Tools for Visual Studio，如 Django 和 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="5e27d-196">Follow these links toolearn more about Python Tools for Visual Studio, Django and SQL Database.</span></span>

* <span data-ttu-id="5e27d-197">[Python Tools for Visual Studio 說明文件]</span><span class="sxs-lookup"><span data-stu-id="5e27d-197">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="5e27d-198">[Web 專案]</span><span class="sxs-lookup"><span data-stu-id="5e27d-198">[Web Projects]</span></span>
  * <span data-ttu-id="5e27d-199">[雲端服務專案]</span><span class="sxs-lookup"><span data-stu-id="5e27d-199">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="5e27d-200">[在 Microsoft Azure 上進行遠端偵錯]</span><span class="sxs-lookup"><span data-stu-id="5e27d-200">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="5e27d-201">[Django 說明文件]</span><span class="sxs-lookup"><span data-stu-id="5e27d-201">[Django Documentation]</span></span>
* <span data-ttu-id="5e27d-202">[SQL Database]</span><span class="sxs-lookup"><span data-stu-id="5e27d-202">[SQL Database]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="5e27d-203">變更的項目</span><span class="sxs-lookup"><span data-stu-id="5e27d-203">What's changed</span></span>
* <span data-ttu-id="5e27d-204">從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="5e27d-204">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Python 開發人員中心]: /develop/python/
[Azure 雲端服務]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->
[Azure 入口網站]: https://portal.azure.com
[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python Tools 2.2 for Visual Studio 範例 VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 (32 位元)]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python Tools for Visual Studio 說明文件]: http://aka.ms/ptvsdocs
[在 Microsoft Azure 上進行遠端偵錯]: http://go.microsoft.com/fwlink/?LinkId=624026
[Web 專案]: http://go.microsoft.com/fwlink/?LinkId=624027
[雲端服務專案]: http://go.microsoft.com/fwlink/?LinkId=624028
[Django 說明文件]: https://www.djangoproject.com/
[SQL Database]: /documentation/services/sql-database/
