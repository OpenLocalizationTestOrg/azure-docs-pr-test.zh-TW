---
title: "Azure 上使用 Python Tools 2.2 for Visual Studio 的 Django 和 MySQL"
description: "了解如何使用 Python Tools for Visual Studio 建立 Django Web 應用程式，藉此將資料儲存在 MySQL 資料庫執行個體中，並部署到 Azure App Service Web Apps。"
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: c60a50b5-8b5e-4818-a442-16362273dabb
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: fd85337ecdc638a4c18065a0ce94f697da8197f1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="django-and-mysql-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="25129-103">Azure 上使用 Python Tools 2.2 for Visual Studio 的 Django 和 MySQL</span><span class="sxs-lookup"><span data-stu-id="25129-103">Django and MySQL on Azure with Python Tools 2.2 for Visual Studio</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="25129-104">在此教學課程中，您將使用 [Python Tools for Visual Studio](https://www.visualstudio.com/vs/python)，並使用其中一個 PTVS 範例範本來建立簡單的民調 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="25129-104">In this tutorial, you'll use [Python Tools for Visual Studio](https://www.visualstudio.com/vs/python) to create a simple polls web app using one of the PTVS sample templates.</span></span> <span data-ttu-id="25129-105">您將學習如何使用在 Azure 上裝載的 MySQL 服務、如何設定 Web 應用程式使用 MySQL，以及如何將 Web 應用程式發佈至 [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714)。</span><span class="sxs-lookup"><span data-stu-id="25129-105">You'll learn how to use a MySQL service hosted on Azure, how to configure the web app to use MySQL, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

> [!NOTE]
> <span data-ttu-id="25129-106">本教學課程中所包含的資訊也可在下列影片中取得︰</span><span class="sxs-lookup"><span data-stu-id="25129-106">The information contained in this tutorial is also available in the following video:</span></span>
> 
> <span data-ttu-id="25129-107">[PTVS 2.1：Django 應用程式與 MySQL][video]</span><span class="sxs-lookup"><span data-stu-id="25129-107">[PTVS 2.1: Django app with MySQL][video]</span></span>
> 
> 

<span data-ttu-id="25129-108">如需更多相關文章 (說明透過使用 Bottle、Flask 和 Django 架構的 PTVS、透過 Azure 資料表儲存體、MySQL 和 SQL Database 服務進行 Azure App Service Web Apps 開發)，請參閱 [Python 開發人員中心] 。</span><span class="sxs-lookup"><span data-stu-id="25129-108">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL, and SQL Database services.</span></span> <span data-ttu-id="25129-109">雖然本文著重於 App Service，但其開發步驟類似於開發 [Azure 雲端服務]。</span><span class="sxs-lookup"><span data-stu-id="25129-109">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25129-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="25129-110">Prerequisites</span></span>
* <span data-ttu-id="25129-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="25129-111">Visual Studio 2015</span></span>
* <span data-ttu-id="25129-112">[Python 2.7 32 位元]或 [Python 3.4 32 位元]</span><span class="sxs-lookup"><span data-stu-id="25129-112">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>
* <span data-ttu-id="25129-113">[Python Tools 2.2 for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="25129-113">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="25129-114">[Python Tools 2.2 for Visual Studio 範例 VSIX]</span><span class="sxs-lookup"><span data-stu-id="25129-114">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="25129-115">[Azure SDK Tools for VS 2015]</span><span class="sxs-lookup"><span data-stu-id="25129-115">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="25129-116">Django 1.9 或更新版本</span><span class="sxs-lookup"><span data-stu-id="25129-116">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<!-- This note should not render as part of the the previous include. -->

> [!NOTE]
> <span data-ttu-id="25129-117">如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service](https://azure.microsoft.com/try/app-service/)，即可在 App Service 中立即建立短期入門 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="25129-117">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="25129-118">不需要信用卡，無需承諾。</span><span class="sxs-lookup"><span data-stu-id="25129-118">No credit card is required, and no commitments are necessary.</span></span>
> 
> 

## <a name="create-the-project"></a><span data-ttu-id="25129-119">建立專案</span><span class="sxs-lookup"><span data-stu-id="25129-119">Create the Project</span></span>
<span data-ttu-id="25129-120">在這一節中，您將使用範例範本建立 Visual Studio 專案。</span><span class="sxs-lookup"><span data-stu-id="25129-120">In this section, you'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="25129-121">您將建立虛擬環境並安裝必要的套件。</span><span class="sxs-lookup"><span data-stu-id="25129-121">You'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="25129-122">您將使用 sqlite 建立本機資料庫。</span><span class="sxs-lookup"><span data-stu-id="25129-122">You'll create a local database using sqlite.</span></span> <span data-ttu-id="25129-123">然後會在本機執行此應用程式。</span><span class="sxs-lookup"><span data-stu-id="25129-123">Then you'll run the application locally.</span></span>

1. <span data-ttu-id="25129-124">在 Visual Studio 中，選取 [檔案]、[新增專案]。</span><span class="sxs-lookup"><span data-stu-id="25129-124">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="25129-125">在 [Python]、[範例] 之下可取得 [Python Tools 2.2 for Visual Studio 範例 VSIX] 中的專案範本。</span><span class="sxs-lookup"><span data-stu-id="25129-125">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="25129-126">選取 [Polls Django Web Project]  ，然後按一下 [確定] 以建立專案。</span><span class="sxs-lookup"><span data-stu-id="25129-126">Select **Polls Django Web Project** and click OK to create the project.</span></span>
   
    ![New Project Dialog](./media/web-sites-python-ptvs-django-mysql/PollsDjangoNewProject.png)
3. <span data-ttu-id="25129-128">系統會提示您安裝外部套件。</span><span class="sxs-lookup"><span data-stu-id="25129-128">You will be prompted to install external packages.</span></span> <span data-ttu-id="25129-129">選取 [安裝到虛擬環境] 。</span><span class="sxs-lookup"><span data-stu-id="25129-129">Select **Install into a virtual environment**.</span></span>
   
    ![外部套件對話方塊](./media/web-sites-python-ptvs-django-mysql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="25129-131">選取 [Python 2.7] 或 [Python 3.4] 作為基礎解譯器。</span><span class="sxs-lookup"><span data-stu-id="25129-131">Select **Python 2.7** or **Python 3.4** as the base interpreter.</span></span>
   
    ![新增虛擬環境對話方塊](./media/web-sites-python-ptvs-django-mysql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="25129-133">在 [方案總管] 中，以滑鼠右鍵按一下專案節點並選取 [Python]，然後選取 [Django 移轉]。</span><span class="sxs-lookup"><span data-stu-id="25129-133">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="25129-134">然後選取 [Django 建立超級使用者] 。</span><span class="sxs-lookup"><span data-stu-id="25129-134">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="25129-135">這樣會開啟 Django 管理主控台，並在專案資料夾中建立 sqlite 資料庫。</span><span class="sxs-lookup"><span data-stu-id="25129-135">This will open a Django Management Console and create a sqlite database in the project folder.</span></span> <span data-ttu-id="25129-136">依照提示建立使用者。</span><span class="sxs-lookup"><span data-stu-id="25129-136">Follow the prompts to create a user.</span></span>
7. <span data-ttu-id="25129-137">按 `F5`確認應用程式可運作。</span><span class="sxs-lookup"><span data-stu-id="25129-137">Confirm that the application works by pressing `F5`.</span></span>
8. <span data-ttu-id="25129-138">按一下頂端導覽列中的 [登入]  。</span><span class="sxs-lookup"><span data-stu-id="25129-138">Click **Log in** from the navigation bar at the top.</span></span>
   
    ![Django 導覽列](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="25129-140">為您在同步處理資料庫時建立的使用者輸入認證。</span><span class="sxs-lookup"><span data-stu-id="25129-140">Enter the credentials for the user you created when you synchronized the database.</span></span>
   
    ![登入表單](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="25129-142">按一下 [Create Sample Polls] 。</span><span class="sxs-lookup"><span data-stu-id="25129-142">Click **Create Sample Polls**.</span></span>
    
     ![建立範例投票](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="25129-144">按一下民調並進行投票。</span><span class="sxs-lookup"><span data-stu-id="25129-144">Click on a poll and vote.</span></span>
    
     ![在範例投票中進行投票](./media/web-sites-python-ptvs-django-mysql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-mysql-database"></a><span data-ttu-id="25129-146">建立 MySQL Database</span><span class="sxs-lookup"><span data-stu-id="25129-146">Create a MySQL Database</span></span>
<span data-ttu-id="25129-147">對於資料庫，您將在 Azure 上建立 ClearDB MySQL 主控的資料庫。</span><span class="sxs-lookup"><span data-stu-id="25129-147">For the database, you'll create a ClearDB MySQL hosted database on Azure.</span></span>

<span data-ttu-id="25129-148">或者，您可以為自己建立在 Azure 中執行的虛擬機器，然後自行安裝和管理 MySQL。</span><span class="sxs-lookup"><span data-stu-id="25129-148">As an alternative, you can create your own Virtual Machine running in Azure, then install and administer MySQL yourself.</span></span>

<span data-ttu-id="25129-149">您可以依照下列步驟，透過免費計畫建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="25129-149">You can create a database with a free plan by following these steps.</span></span>

1. <span data-ttu-id="25129-150">登入 [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="25129-150">Log in to the [Azure Portal].</span></span>
2. <span data-ttu-id="25129-151">在導覽窗格的頂端，依序按一下 [新增]、[資料 + 儲存體] 和 [MySQL 資料庫]。</span><span class="sxs-lookup"><span data-stu-id="25129-151">At the Top of the navigation pane, click **NEW**, then click **Data + Storage**, and then click **MySQL Database**.</span></span>
3. <span data-ttu-id="25129-152">設定新的 MySQL 資料庫，做法是建立新的資源群組，然後為其選取一個適當的位置。</span><span class="sxs-lookup"><span data-stu-id="25129-152">Configure the new MySQL database by creating a new resource group and select the appropriate location for it.</span></span>
4. <span data-ttu-id="25129-153">建立 MySQL 資料庫後，請按一下資料庫刀鋒視窗中的 [屬性]  。</span><span class="sxs-lookup"><span data-stu-id="25129-153">Once the MySQL database is created, click **Properties** in the database blade.</span></span>
5. <span data-ttu-id="25129-154">使用 [複製] 按鈕將 **CONNECTION STRING** 的值複製到剪貼簿上。</span><span class="sxs-lookup"><span data-stu-id="25129-154">Use the copy button to put the value of **CONNECTION STRING** on the clipboard.</span></span>

## <a name="configure-the-project"></a><span data-ttu-id="25129-155">設定專案</span><span class="sxs-lookup"><span data-stu-id="25129-155">Configure the Project</span></span>
<span data-ttu-id="25129-156">在這一節中，您會將 Web 應用程式設定為使用剛才建立的 MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="25129-156">In this section, you'll configure our web app to use the MySQL database you just created.</span></span> <span data-ttu-id="25129-157">您也將安裝搭配使用 MySQL 資料庫與 Django 所需的其他 Python 套件。</span><span class="sxs-lookup"><span data-stu-id="25129-157">You'll also install additional Python packages required to use MySQL databases with Django.</span></span> <span data-ttu-id="25129-158">接著，在本機執行 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="25129-158">Then you'll run the web app locally.</span></span>

1. <span data-ttu-id="25129-159">在 Visual Studio 中，從 **ProjectName**資料夾開啟 *settings.py* 。</span><span class="sxs-lookup"><span data-stu-id="25129-159">In Visual Studio, open **settings.py**, from the *ProjectName* folder.</span></span> <span data-ttu-id="25129-160">暫時在編輯器中貼上連接字串。</span><span class="sxs-lookup"><span data-stu-id="25129-160">Temporarily paste the connection string in the editor.</span></span> <span data-ttu-id="25129-161">連接字串的格式如下：</span><span class="sxs-lookup"><span data-stu-id="25129-161">The connection string is in this format:</span></span>
   
        Database=<NAME>;Data Source=<HOST>;User Id=<USER>;Password=<PASSWORD>
   
    <span data-ttu-id="25129-162">變更預設資料庫 **ENGINE** 以使用 MySQL，並設定 **CONNECTIONSTRING** 中 **NAME**、**USER**、**PASSWORD** 和 **HOST** 的值。</span><span class="sxs-lookup"><span data-stu-id="25129-162">Change the default database **ENGINE** to use MySQL, and set the values for **NAME**, **USER**, **PASSWORD** and **HOST** from the **CONNECTIONSTRING**.</span></span>
   
        DATABASES = {
            'default': {
                'ENGINE': 'django.db.backends.mysql',
                'NAME': '<Database>',
                'USER': '<User Id>',
                'PASSWORD': '<Password>',
                'HOST': '<Data Source>',
                'PORT': '',
            }
        }
2. <span data-ttu-id="25129-163">在 [方案總管] 的 [Python 環境] 之下，在虛擬環境上按一下滑鼠右鍵並選取 [安裝 Python 封裝]。</span><span class="sxs-lookup"><span data-stu-id="25129-163">In Solution Explorer, under **Python Environments**, right-click on the virtual environment and select **Install Python Package**.</span></span>
3. <span data-ttu-id="25129-164">使用 **pip** 安裝 `mysqlclient` 封裝。</span><span class="sxs-lookup"><span data-stu-id="25129-164">Install the package `mysqlclient` using **pip**.</span></span>
   
    ![安裝套件對話方塊](./media/web-sites-python-ptvs-django-mysql/PollsDjangoMySQLInstallPackage.png)
4. <span data-ttu-id="25129-166">在 [方案總管] 中，以滑鼠右鍵按一下專案節點並選取 [Python]，然後選取 [Django 移轉]。</span><span class="sxs-lookup"><span data-stu-id="25129-166">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="25129-167">然後選取 [Django 建立超級使用者] 。</span><span class="sxs-lookup"><span data-stu-id="25129-167">Then select **Django Create Superuser**.</span></span>
   
    <span data-ttu-id="25129-168">此舉會為您在上一節中建立的 MySQL 資料庫建立資料表。</span><span class="sxs-lookup"><span data-stu-id="25129-168">This will create the tables for the MySQL database you created in the previous section.</span></span> <span data-ttu-id="25129-169">依照提示建立使用者，該使用者不需符合在本文第一節中建立之 sqlite 資料庫中的使用者。</span><span class="sxs-lookup"><span data-stu-id="25129-169">Follow the prompts to create a user, which doesn't have to match the user in the sqlite database created in the first section of this article.</span></span>
5. <span data-ttu-id="25129-170">使用 `F5`執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="25129-170">Run the application with `F5`.</span></span> <span data-ttu-id="25129-171">使用 [Create Sample Polls]  建立的民調以及投票所提交的資料將會在 MySQL 資料庫中序列化。</span><span class="sxs-lookup"><span data-stu-id="25129-171">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in the MySQL database.</span></span>

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="25129-172">將 Web 應用程式發佈至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="25129-172">Publish the web app to Azure App Service</span></span>
<span data-ttu-id="25129-173">Azure .NET SDK 提供簡單的方法將 Web 應用程式部署至 Azure App Service。</span><span class="sxs-lookup"><span data-stu-id="25129-173">The Azure .NET SDK provides an easy way to deploy your web app to Azure App Service.</span></span>

1. <span data-ttu-id="25129-174">在 [方案總管] 中，以滑鼠右鍵按一下專案節點並選取 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="25129-174">In **Solution Explorer**, right-click on the project node and select **Publish**.</span></span>
   
    ![發行 Web 對話方塊](./media/web-sites-python-ptvs-django-mysql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="25129-176">按一下 [Microsoft Azure App Service] 。</span><span class="sxs-lookup"><span data-stu-id="25129-176">Click on **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="25129-177">按一下 [新增]  以建立新的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="25129-177">Click on **New** to create a new web app.</span></span>
4. <span data-ttu-id="25129-178">填寫下列欄位，然後按一下 [建立] ：</span><span class="sxs-lookup"><span data-stu-id="25129-178">Fill in the following fields and click **Create**:</span></span>
   
   * <span data-ttu-id="25129-179">**Web 應用程式名稱**</span><span class="sxs-lookup"><span data-stu-id="25129-179">**Web App name**</span></span>
   * <span data-ttu-id="25129-180">**App Service 計劃**</span><span class="sxs-lookup"><span data-stu-id="25129-180">**App Service plan**</span></span>
   * <span data-ttu-id="25129-181">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="25129-181">**Resource group**</span></span>
   * <span data-ttu-id="25129-182">**區域**</span><span class="sxs-lookup"><span data-stu-id="25129-182">**Region**</span></span>
   * <span data-ttu-id="25129-183">讓「資料庫伺服器」維持設定為「沒有資料庫」</span><span class="sxs-lookup"><span data-stu-id="25129-183">Leave **Database server** set to **No database**</span></span>
5. <span data-ttu-id="25129-184">接受所有其他預設值並按一下 [發佈] 。</span><span class="sxs-lookup"><span data-stu-id="25129-184">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="25129-185">您的 Web 瀏覽器將會自動開啟到已發佈的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="25129-185">Your web browser will open automatically to the published web app.</span></span> <span data-ttu-id="25129-186">您應該會看到 Web 應用程式如預期般運作，並使用 Azure 上裝載的 **MySQL** 資料庫。</span><span class="sxs-lookup"><span data-stu-id="25129-186">You should see the web app working as expected, using the **MySQL** database hosted on Azure.</span></span>
   
    ![Web Browser](./media/web-sites-python-ptvs-django-mysql/PollsDjangoAzureBrowser.png)
   
    <span data-ttu-id="25129-188">恭喜！</span><span class="sxs-lookup"><span data-stu-id="25129-188">Congratulations!</span></span> <span data-ttu-id="25129-189">您已成功將以 MySQL 為基礎的 Web 應用程式發佈至 Azure。</span><span class="sxs-lookup"><span data-stu-id="25129-189">You have successfully published your MySQL-based web app to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="25129-190">後續步驟</span><span class="sxs-lookup"><span data-stu-id="25129-190">Next steps</span></span>
<span data-ttu-id="25129-191">請遵循下列連結以深入了解 Python Tools for Visual Studio、Django 和 MySQL。</span><span class="sxs-lookup"><span data-stu-id="25129-191">Follow these links to learn more about Python Tools for Visual Studio, Django and MySQL.</span></span>

* <span data-ttu-id="25129-192">[Python Tools for Visual Studio 說明文件]</span><span class="sxs-lookup"><span data-stu-id="25129-192">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="25129-193">[Web 專案]</span><span class="sxs-lookup"><span data-stu-id="25129-193">[Web Projects]</span></span>
  * <span data-ttu-id="25129-194">[雲端服務專案]</span><span class="sxs-lookup"><span data-stu-id="25129-194">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="25129-195">[在 Microsoft Azure 上進行遠端偵錯]</span><span class="sxs-lookup"><span data-stu-id="25129-195">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="25129-196">[Django 說明文件]</span><span class="sxs-lookup"><span data-stu-id="25129-196">[Django Documentation]</span></span>
* <span data-ttu-id="25129-197">[MySQL]</span><span class="sxs-lookup"><span data-stu-id="25129-197">[MySQL]</span></span>

<span data-ttu-id="25129-198">如需詳細資訊，請參閱 [Python 開發人員中心](/develop/python/)。</span><span class="sxs-lookup"><span data-stu-id="25129-198">For more information, see the [Python Developer Center](/develop/python/).</span></span>

<!--Link references-->

[Python 開發人員中心]: /develop/python/
[Azure 雲端服務]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->

[Azure 入口網站]: https://portal.azure.com
[Python Tools for Visual Studio]: https://www.visualstudio.com/vs/python/
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python Tools 2.2 for Visual Studio 範例 VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 32 位元]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 32 位元]: http://go.microsoft.com/fwlink/?LinkId=517191
[Python Tools for Visual Studio 說明文件]: http://aka.ms/ptvsdocs
[在 Microsoft Azure 上進行遠端偵錯]: http://go.microsoft.com/fwlink/?LinkId=624026
[Web 專案]: http://go.microsoft.com/fwlink/?LinkId=624027
[雲端服務專案]: http://go.microsoft.com/fwlink/?LinkId=624028
[Django 說明文件]: https://www.djangoproject.com/
[MySQL]: http://www.mysql.com/
[video]: http://youtu.be/oKCApIrS0Lo
