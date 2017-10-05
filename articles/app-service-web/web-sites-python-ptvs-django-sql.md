---
title: "Azure 上使用 Python Tools 2.2 for Visual Studio 的 Django 和 SQL Database"
description: "了解如何使用 Python Tools for Visual Studio 建立 Django Web 應用程式，藉此將資料儲存在 SQL Database 執行個體中，並部署到 Azure App Service Web Apps。"
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
ms.openlocfilehash: 65b59dee2b7bddca77d31c692dab713c68d67e24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="24a61-103">Azure 上使用 Python Tools 2.2 for Visual Studio 的 Django 和 SQL Database</span><span class="sxs-lookup"><span data-stu-id="24a61-103">Django and SQL Database on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="24a61-104">在此教學課程中，我們將使用 [Python Tools for Visual Studio] ，並使用其中一個 PTVS 範例範本來建立簡單的民調 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="24a61-104">In this tutorial, we'll use [Python Tools for Visual Studio] to create a simple polls web app using one of the PTVS sample templates.</span></span> <span data-ttu-id="24a61-105">本教學課程也提供 [教學影片](https://www.youtube.com/watch?v=ZwcoGcIeHF4)。</span><span class="sxs-lookup"><span data-stu-id="24a61-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span></span>

<span data-ttu-id="24a61-106">我們將學習如何使用 Azure 上裝載的 SQL Database、如何設定 Web 應用程式來使用 SQL Database，以及如何將 Web 應用程式發佈至 [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714)。</span><span class="sxs-lookup"><span data-stu-id="24a61-106">We'll learn how to use a SQL database hosted on Azure, how to configure the web app to use a SQL database, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="24a61-107">如需更多相關文章 (說明透過使用 Bottle、Flask 和 Django 架構的 PTVS、透過 Azure 資料表儲存體、MySQL 和 SQL Database 服務進行 Azure App Service Web Apps 開發)，請參閱 [Python 開發人員中心] 。</span><span class="sxs-lookup"><span data-stu-id="24a61-107">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="24a61-108">雖然本文著重於 App Service，但其開發步驟類似於開發 [Azure 雲端服務]。</span><span class="sxs-lookup"><span data-stu-id="24a61-108">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24a61-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="24a61-109">Prerequisites</span></span>
* <span data-ttu-id="24a61-110">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="24a61-110">Visual Studio 2015</span></span>
* <span data-ttu-id="24a61-111">[Python 2.7 (32 位元)]</span><span class="sxs-lookup"><span data-stu-id="24a61-111">[Python 2.7 32-bit]</span></span>
* <span data-ttu-id="24a61-112">[Python Tools 2.2 for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="24a61-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="24a61-113">[Python Tools 2.2 for Visual Studio 範例 VSIX]</span><span class="sxs-lookup"><span data-stu-id="24a61-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="24a61-114">[Azure SDK Tools for VS 2015]</span><span class="sxs-lookup"><span data-stu-id="24a61-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="24a61-115">Django 1.9 或更新版本</span><span class="sxs-lookup"><span data-stu-id="24a61-115">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="24a61-116">如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service](https://azure.microsoft.com/try/app-service/)，即可在 App Service 中立即建立短期入門 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="24a61-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="24a61-117">不需要信用卡；無需承諾。</span><span class="sxs-lookup"><span data-stu-id="24a61-117">No credit cards required; no commitments.</span></span>
>
>

## <a name="create-the-project"></a><span data-ttu-id="24a61-118">建立專案</span><span class="sxs-lookup"><span data-stu-id="24a61-118">Create the Project</span></span>
<span data-ttu-id="24a61-119">在這一節中，我們將使用範例範本建立 Visual Studio 專案。</span><span class="sxs-lookup"><span data-stu-id="24a61-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="24a61-120">我們將建立虛擬環境並安裝必要的套件。</span><span class="sxs-lookup"><span data-stu-id="24a61-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="24a61-121">我們將使用 sqlite 建立本機資料庫。</span><span class="sxs-lookup"><span data-stu-id="24a61-121">We'll create a local database using sqlite.</span></span> <span data-ttu-id="24a61-122">接著，在本機執行 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="24a61-122">Then we'll run the web app locally.</span></span>

1. <span data-ttu-id="24a61-123">在 Visual Studio 中，選取 [檔案]、[新增專案]。</span><span class="sxs-lookup"><span data-stu-id="24a61-123">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="24a61-124">在 [Python]、[範例] 之下可取得 [Python Tools 2.2 for Visual Studio 範例 VSIX] 中的專案範本。</span><span class="sxs-lookup"><span data-stu-id="24a61-124">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="24a61-125">選取 [Polls Django Web Project]  ，然後按一下 [確定] 以建立專案。</span><span class="sxs-lookup"><span data-stu-id="24a61-125">Select **Polls Django Web Project** and click OK to create the project.</span></span>

     ![New Project Dialog](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. <span data-ttu-id="24a61-127">系統會提示您安裝外部套件。</span><span class="sxs-lookup"><span data-stu-id="24a61-127">You will be prompted to install external packages.</span></span> <span data-ttu-id="24a61-128">選取 [安裝到虛擬環境] 。</span><span class="sxs-lookup"><span data-stu-id="24a61-128">Select **Install into a virtual environment**.</span></span>

     ![外部套件對話方塊](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="24a61-130">選取 **Python 2.7** 作為基礎解譯器。</span><span class="sxs-lookup"><span data-stu-id="24a61-130">Select **Python 2.7** as the base interpreter.</span></span>

     ![新增虛擬環境對話方塊](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="24a61-132">在 [方案總管] 中，以滑鼠右鍵按一下專案節點並選取 [Python]，然後選取 [Django 移轉]。</span><span class="sxs-lookup"><span data-stu-id="24a61-132">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="24a61-133">然後選取 [Django 建立超級使用者] 。</span><span class="sxs-lookup"><span data-stu-id="24a61-133">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="24a61-134">這樣會開啟 Django 管理主控台，並在專案資料夾中建立 sqlite 資料庫。</span><span class="sxs-lookup"><span data-stu-id="24a61-134">This will open a Django Management Console and create a sqlite database in the project folder.</span></span> <span data-ttu-id="24a61-135">依照提示建立使用者。</span><span class="sxs-lookup"><span data-stu-id="24a61-135">Follow the prompts to create a user.</span></span>
7. <span data-ttu-id="24a61-136">按 <kbd>F5</kbd> 確認應用程式可運作。</span><span class="sxs-lookup"><span data-stu-id="24a61-136">Confirm that the application works by pressing <kbd>F5</kbd>.</span></span>
8. <span data-ttu-id="24a61-137">按一下頂端導覽列中的 [登入]  。</span><span class="sxs-lookup"><span data-stu-id="24a61-137">Click **Log in** from the navigation bar at the top.</span></span>

     ![Web Browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="24a61-139">為您在同步處理資料庫時建立的使用者輸入認證。</span><span class="sxs-lookup"><span data-stu-id="24a61-139">Enter the credentials for the user you created when you synchronized the database.</span></span>

     ![Web Browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="24a61-141">按一下 [Create Sample Polls] 。</span><span class="sxs-lookup"><span data-stu-id="24a61-141">Click **Create Sample Polls**.</span></span>

      ![Web Browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="24a61-143">按一下民調並進行投票。</span><span class="sxs-lookup"><span data-stu-id="24a61-143">Click on a poll and vote.</span></span>

      ![Web Browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a><span data-ttu-id="24a61-145">建立 SQL Database</span><span class="sxs-lookup"><span data-stu-id="24a61-145">Create a SQL Database</span></span>
<span data-ttu-id="24a61-146">對於資料庫，我們將建立 Azure SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="24a61-146">For the database, we'll create an Azure SQL database.</span></span>

<span data-ttu-id="24a61-147">您可以依照下列步驟來建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="24a61-147">You can create a database by following these steps.</span></span>

1. <span data-ttu-id="24a61-148">登入 [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="24a61-148">Log into the [Azure Portal].</span></span>
2. <span data-ttu-id="24a61-149">在導覽窗格的底端，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="24a61-149">At the bottom of the navigation pane, click **NEW**.</span></span> <span data-ttu-id="24a61-150">接著，按一下 [資料 + 儲存體] > [Azure Marketplace]。</span><span class="sxs-lookup"><span data-stu-id="24a61-150">, click **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="24a61-151">設定新的 SQL Database，做法是建立新的資源群組，然後為其選取一個適當的位置。</span><span class="sxs-lookup"><span data-stu-id="24a61-151">Configure the new SQL Database by creating a new resource group and select the appropriate location for it.</span></span>
4. <span data-ttu-id="24a61-152">建立 SQL Database 後，請按一下資料庫刀鋒視窗中的 [在 Visual Studio 中開啟]  。</span><span class="sxs-lookup"><span data-stu-id="24a61-152">Once the SQL Database is created, click **Open in Visual Studio** in the database blade.</span></span>
5. <span data-ttu-id="24a61-153">按一下 [設定防火牆] 。</span><span class="sxs-lookup"><span data-stu-id="24a61-153">Click **Configure your firewall**.</span></span>
6. <span data-ttu-id="24a61-154">在 [防火牆設定] 刀鋒視窗中新增下列防火牆規則：**START IP** 與 **END IP** 設為您開發電腦上的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="24a61-154">In the **Firewall Settings** blade, add a firewall rule with **START IP** and **END IP** set to the public IP address of your development machine.</span></span> <span data-ttu-id="24a61-155">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="24a61-155">Click **Save**.</span></span>

   <span data-ttu-id="24a61-156">這樣可讓您從開發電腦連線至資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="24a61-156">This will allow connections to the database server from your development machine.</span></span>
7. <span data-ttu-id="24a61-157">在資料庫刀鋒視窗中，按一下 [屬性]，然後按一下 [顯示資料庫連接字串]。</span><span class="sxs-lookup"><span data-stu-id="24a61-157">Back in the database blade, click **Properties**, then click **Show database connection strings**.</span></span>
8. <span data-ttu-id="24a61-158">使用 [複製] 按鈕將 **ADO.NET** 的值複製到剪貼簿上。</span><span class="sxs-lookup"><span data-stu-id="24a61-158">Use the copy button to put the value of **ADO.NET** on the clipboard.</span></span>

## <a name="configure-the-project"></a><span data-ttu-id="24a61-159">設定專案</span><span class="sxs-lookup"><span data-stu-id="24a61-159">Configure the Project</span></span>
<span data-ttu-id="24a61-160">在這一節中，我們會將 Web 應用程式設定為使用我們剛才建立的 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="24a61-160">In this section, we'll configure our web app to use the SQL database we just created.</span></span> <span data-ttu-id="24a61-161">我們也將安裝搭配使用 SQL 資料庫與 Django 所需的其他 Python 套件。</span><span class="sxs-lookup"><span data-stu-id="24a61-161">We'll also install additional Python packages required to use SQL databases with Django.</span></span> <span data-ttu-id="24a61-162">接著，在本機執行 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="24a61-162">Then we'll run the web app locally.</span></span>

1. <span data-ttu-id="24a61-163">在 Visual Studio 中，從 **ProjectName**資料夾開啟 *settings.py* 。</span><span class="sxs-lookup"><span data-stu-id="24a61-163">In Visual Studio, open **settings.py**, from the *ProjectName* folder.</span></span> <span data-ttu-id="24a61-164">暫時在編輯器中貼上連接字串。</span><span class="sxs-lookup"><span data-stu-id="24a61-164">Temporarily paste the connection string in the editor.</span></span> <span data-ttu-id="24a61-165">連接字串的格式如下：</span><span class="sxs-lookup"><span data-stu-id="24a61-165">The connection string is in this format:</span></span>

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

<span data-ttu-id="24a61-166">使用上述值編輯 `DATABASES` 的定義。</span><span class="sxs-lookup"><span data-stu-id="24a61-166">Edit the definition of `DATABASES` to use the values above.</span></span>

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

1. <span data-ttu-id="24a61-167">在 [方案總管] 的 [Python 環境] 之下，在虛擬環境上按一下滑鼠右鍵並選取 [安裝 Python 封裝]。</span><span class="sxs-lookup"><span data-stu-id="24a61-167">In Solution Explorer, under **Python Environments**, right-click on the virtual environment and select **Install Python Package**.</span></span>
2. <span data-ttu-id="24a61-168">使用 **pip** 安裝 `pyodbc` 封裝。</span><span class="sxs-lookup"><span data-stu-id="24a61-168">Install the package `pyodbc` using **pip**.</span></span>

     ![安裝 Python 封裝對話方塊](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. <span data-ttu-id="24a61-170">使用 **pip** 安裝 `django-pyodbc-azure` 封裝。</span><span class="sxs-lookup"><span data-stu-id="24a61-170">Install the package `django-pyodbc-azure` using **pip**.</span></span>

     ![安裝 Python 封裝對話方塊](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. <span data-ttu-id="24a61-172">在 [方案總管] 中，以滑鼠右鍵按一下專案節點並選取 [Python]，然後選取 [Django 移轉]。</span><span class="sxs-lookup"><span data-stu-id="24a61-172">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="24a61-173">然後選取 [Django 建立超級使用者] 。</span><span class="sxs-lookup"><span data-stu-id="24a61-173">Then select **Django Create Superuser**.</span></span>

   <span data-ttu-id="24a61-174">此舉會為我們在上一節中建立的 SQL Database 建立資料表。</span><span class="sxs-lookup"><span data-stu-id="24a61-174">This will create the tables for the SQL database we created in the previous section.</span></span> <span data-ttu-id="24a61-175">依照提示建立使用者，該使用者不需符合在第一節中建立之 sqlite 資料庫中的使用者。</span><span class="sxs-lookup"><span data-stu-id="24a61-175">Follow the prompts to create a user, which doesn't have to match the user in the sqlite database created in the first section.</span></span>
5. <span data-ttu-id="24a61-176">使用 `F5`執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="24a61-176">Run the application with `F5`.</span></span> <span data-ttu-id="24a61-177">使用 [Create Sample Polls]  建立的民調以及投票所提交的資料將會在 SQL Database 中序列化。</span><span class="sxs-lookup"><span data-stu-id="24a61-177">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in the SQL database.</span></span>

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="24a61-178">將 Web 應用程式發佈至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="24a61-178">Publish the web app to Azure App Service</span></span>
<span data-ttu-id="24a61-179">Azure .NET SDK 提供簡單的方法將 Web 應用程式部署至 Azure App Service Web Apps。</span><span class="sxs-lookup"><span data-stu-id="24a61-179">The Azure .NET SDK provides an easy way to deploy your web web app to Azure App Service Web Apps.</span></span>

1. <span data-ttu-id="24a61-180">在 [方案總管] 中，以滑鼠右鍵按一下專案節點並選取 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="24a61-180">In **Solution Explorer**, right-click on the project node and select **Publish**.</span></span>

     ![發行 Web 對話方塊](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="24a61-182">按一下 [Microsoft Azure Web Apps] 。</span><span class="sxs-lookup"><span data-stu-id="24a61-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="24a61-183">按一下 [新增]  以建立新的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="24a61-183">Click on **New** to create a new web app.</span></span>
4. <span data-ttu-id="24a61-184">填寫下列欄位，然後按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="24a61-184">Fill in the following fields and click **Create**.</span></span>

   * <span data-ttu-id="24a61-185">**Web 應用程式名稱**</span><span class="sxs-lookup"><span data-stu-id="24a61-185">**Web App name**</span></span>
   * <span data-ttu-id="24a61-186">**App Service 計劃**</span><span class="sxs-lookup"><span data-stu-id="24a61-186">**App Service plan**</span></span>
   * <span data-ttu-id="24a61-187">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="24a61-187">**Resource group**</span></span>
   * <span data-ttu-id="24a61-188">**區域**</span><span class="sxs-lookup"><span data-stu-id="24a61-188">**Region**</span></span>
   * <span data-ttu-id="24a61-189">讓「資料庫伺服器」維持設定為「沒有資料庫」</span><span class="sxs-lookup"><span data-stu-id="24a61-189">Leave **Database server** set to **No database**</span></span>
5. <span data-ttu-id="24a61-190">接受所有其他預設值並按一下 [發佈] 。</span><span class="sxs-lookup"><span data-stu-id="24a61-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="24a61-191">您的 Web 瀏覽器將會自動開啟到已發佈的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="24a61-191">Your web browser will open automatically to the published web app.</span></span> <span data-ttu-id="24a61-192">您應該會看到 Web 應用程式如預期般運作，並使用 Azure 上裝載的 **SQL** 資料庫。</span><span class="sxs-lookup"><span data-stu-id="24a61-192">You should see the web app working as expected, using the **SQL** database hosted on Azure.</span></span>

   <span data-ttu-id="24a61-193">恭喜！</span><span class="sxs-lookup"><span data-stu-id="24a61-193">Congratulations!</span></span>

     ![Web Browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="24a61-195">後續步驟</span><span class="sxs-lookup"><span data-stu-id="24a61-195">Next steps</span></span>
<span data-ttu-id="24a61-196">請遵循下列連結以深入了解 Python Tools for Visual Studio、Django 和 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="24a61-196">Follow these links to learn more about Python Tools for Visual Studio, Django and SQL Database.</span></span>

* <span data-ttu-id="24a61-197">[Python Tools for Visual Studio 說明文件]</span><span class="sxs-lookup"><span data-stu-id="24a61-197">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="24a61-198">[Web 專案]</span><span class="sxs-lookup"><span data-stu-id="24a61-198">[Web Projects]</span></span>
  * <span data-ttu-id="24a61-199">[雲端服務專案]</span><span class="sxs-lookup"><span data-stu-id="24a61-199">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="24a61-200">[在 Microsoft Azure 上進行遠端偵錯]</span><span class="sxs-lookup"><span data-stu-id="24a61-200">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="24a61-201">[Django 說明文件]</span><span class="sxs-lookup"><span data-stu-id="24a61-201">[Django Documentation]</span></span>
* <span data-ttu-id="24a61-202">[SQL Database]</span><span class="sxs-lookup"><span data-stu-id="24a61-202">[SQL Database]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="24a61-203">變更的項目</span><span class="sxs-lookup"><span data-stu-id="24a61-203">What's changed</span></span>
* <span data-ttu-id="24a61-204">如需從網站變更為 App Service 的指南，請參閱： [Azure App Service 及其對現有 Azure 服務的影響](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="24a61-204">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
<span data-ttu-id="24a61-205">[Python 開發人員中心]: /develop/python/</span><span class="sxs-lookup"><span data-stu-id="24a61-205">[Python Developer Center]: /develop/python/</span></span>
<span data-ttu-id="24a61-206">[Azure 雲端服務]: ../cloud-services/cloud-services-python-ptvs.md</span><span class="sxs-lookup"><span data-stu-id="24a61-206">[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md</span></span>

<!--External Link references-->
<span data-ttu-id="24a61-207">[Azure 入口網站]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="24a61-207">[Azure Portal]: https://portal.azure.com</span></span>
<span data-ttu-id="24a61-208">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span><span class="sxs-lookup"><span data-stu-id="24a61-208">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span></span>
<span data-ttu-id="24a61-209">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="24a61-209">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="24a61-210">[Python Tools 2.2 for Visual Studio 範例 VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="24a61-210">[Python Tools 2.2 for Visual Studio Samples VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="24a61-211">[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003</span><span class="sxs-lookup"><span data-stu-id="24a61-211">[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003</span></span>
<span data-ttu-id="24a61-212">[Python 2.7 (32 位元)]: http://go.microsoft.com/fwlink/?LinkId=517190</span><span class="sxs-lookup"><span data-stu-id="24a61-212">[Python 2.7 32-bit]: http://go.microsoft.com/fwlink/?LinkId=517190</span></span>
<span data-ttu-id="24a61-213">[Python Tools for Visual Studio 說明文件]: http://aka.ms/ptvsdocs</span><span class="sxs-lookup"><span data-stu-id="24a61-213">[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs</span></span>
<span data-ttu-id="24a61-214">[在 Microsoft Azure 上進行遠端偵錯]: http://go.microsoft.com/fwlink/?LinkId=624026</span><span class="sxs-lookup"><span data-stu-id="24a61-214">[Remote Debugging on Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026</span></span>
<span data-ttu-id="24a61-215">[Web 專案]: http://go.microsoft.com/fwlink/?LinkId=624027</span><span class="sxs-lookup"><span data-stu-id="24a61-215">[Web Projects]: http://go.microsoft.com/fwlink/?LinkId=624027</span></span>
<span data-ttu-id="24a61-216">[雲端服務專案]: http://go.microsoft.com/fwlink/?LinkId=624028</span><span class="sxs-lookup"><span data-stu-id="24a61-216">[Cloud Service Projects]: http://go.microsoft.com/fwlink/?LinkId=624028</span></span>
<span data-ttu-id="24a61-217">[Django 說明文件]: https://www.djangoproject.com/</span><span class="sxs-lookup"><span data-stu-id="24a61-217">[Django Documentation]: https://www.djangoproject.com/</span></span>
<span data-ttu-id="24a61-218">[SQL Database]: /documentation/services/sql-database/</span><span class="sxs-lookup"><span data-stu-id="24a61-218">[SQL Database]: /documentation/services/sql-database/</span></span>
