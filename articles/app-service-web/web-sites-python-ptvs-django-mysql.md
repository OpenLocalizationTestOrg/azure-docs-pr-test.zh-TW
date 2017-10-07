---
title: "aaaDjango 和使用 Python Tools 2.2 for Visual Studio 在 Azure 上的 MySQL"
description: "了解如何 toouse hello Python Tools for Visual Studio toocreate Django web 應用程式的 MySQL 資料庫執行個體中儲存資料，並將其部署 tooAzure App Service Web 應用程式。"
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
ms.openlocfilehash: 1597c391d20c8e8ef629b4e4d05c9eb64c83bffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-mysql-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="bd839-103">Azure 上使用 Python Tools 2.2 for Visual Studio 的 Django 和 MySQL</span><span class="sxs-lookup"><span data-stu-id="bd839-103">Django and MySQL on Azure with Python Tools 2.2 for Visual Studio</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="bd839-104">在此教學課程中，您將使用[Python Tools for Visual Studio](https://www.visualstudio.com/vs/python) toocreate 簡單輪詢 web 應用程式使用其中一個 hello PTVS 範例範本。</span><span class="sxs-lookup"><span data-stu-id="bd839-104">In this tutorial, you'll use [Python Tools for Visual Studio](https://www.visualstudio.com/vs/python) toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="bd839-105">您將學習如何 toouse MySQL 服務裝載在 Azure 上、 如何 tooconfigure hello web 應用程式 toouse MySQL，以及如何 toopublish hello web 應用程式太[Azure App Service Web 應用程式](http://go.microsoft.com/fwlink/?LinkId=529714)。</span><span class="sxs-lookup"><span data-stu-id="bd839-105">You'll learn how toouse a MySQL service hosted on Azure, how tooconfigure hello web app toouse MySQL, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

> [!NOTE]
> <span data-ttu-id="bd839-106">在本教學課程所包含的 hello 資訊也會提供下列視訊 hello:</span><span class="sxs-lookup"><span data-stu-id="bd839-106">hello information contained in this tutorial is also available in hello following video:</span></span>
> 
> <span data-ttu-id="bd839-107">[PTVS 2.1：Django 應用程式與 MySQL][video]</span><span class="sxs-lookup"><span data-stu-id="bd839-107">[PTVS 2.1: Django app with MySQL][video]</span></span>
> 
> 

<span data-ttu-id="bd839-108">請參閱 hello [Python 開發人員中心]涵蓋 Azure App Service Web 應用程式與使用 Bottle PTVS 開發的多個發行項，酒瓶和 Django web 架構，來使用 Azure 資料表儲存體、 MySQL 及 SQL Database 服務。</span><span class="sxs-lookup"><span data-stu-id="bd839-108">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL, and SQL Database services.</span></span> <span data-ttu-id="bd839-109">本文著重在應用程式服務，而開發時 hello 步驟均相似[Azure 雲端服務]。</span><span class="sxs-lookup"><span data-stu-id="bd839-109">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd839-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="bd839-110">Prerequisites</span></span>
* <span data-ttu-id="bd839-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="bd839-111">Visual Studio 2015</span></span>
* <span data-ttu-id="bd839-112">[Python 2.7 32 位元]或 [Python 3.4 32 位元]</span><span class="sxs-lookup"><span data-stu-id="bd839-112">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>
* <span data-ttu-id="bd839-113">[Python Tools 2.2 for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="bd839-113">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="bd839-114">[Python Tools 2.2 for Visual Studio 範例 VSIX]</span><span class="sxs-lookup"><span data-stu-id="bd839-114">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="bd839-115">[Azure SDK Tools for VS 2015]</span><span class="sxs-lookup"><span data-stu-id="bd839-115">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="bd839-116">Django 1.9 或更新版本</span><span class="sxs-lookup"><span data-stu-id="bd839-116">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<!-- This note should not render as part of hello hello previous include. -->

> [!NOTE]
> <span data-ttu-id="bd839-117">如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="bd839-117">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="bd839-118">不需要信用卡，無需承諾。</span><span class="sxs-lookup"><span data-stu-id="bd839-118">No credit card is required, and no commitments are necessary.</span></span>
> 
> 

## <a name="create-hello-project"></a><span data-ttu-id="bd839-119">建立 hello 專案</span><span class="sxs-lookup"><span data-stu-id="bd839-119">Create hello Project</span></span>
<span data-ttu-id="bd839-120">在這一節中，您將使用範例範本建立 Visual Studio 專案。</span><span class="sxs-lookup"><span data-stu-id="bd839-120">In this section, you'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="bd839-121">您將建立虛擬環境並安裝必要的套件。</span><span class="sxs-lookup"><span data-stu-id="bd839-121">You'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="bd839-122">您將使用 sqlite 建立本機資料庫。</span><span class="sxs-lookup"><span data-stu-id="bd839-122">You'll create a local database using sqlite.</span></span> <span data-ttu-id="bd839-123">然後您將在本機執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bd839-123">Then you'll run hello application locally.</span></span>

1. <span data-ttu-id="bd839-124">在 Visual Studio 中，選取 [檔案]、[新增專案]。</span><span class="sxs-lookup"><span data-stu-id="bd839-124">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="bd839-125">hello 專案範本從 hello [Python Tools 2.2 for Visual Studio 範例 VSIX]底下可使用**Python**，**範例**。</span><span class="sxs-lookup"><span data-stu-id="bd839-125">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="bd839-126">選取**輪詢 Django Web 專案**然後按一下 [確定] toocreate hello 專案。</span><span class="sxs-lookup"><span data-stu-id="bd839-126">Select **Polls Django Web Project** and click OK toocreate hello project.</span></span>
   
    ![New Project Dialog](./media/web-sites-python-ptvs-django-mysql/PollsDjangoNewProject.png)
3. <span data-ttu-id="bd839-128">系統會提示的 tooinstall 外部的封裝。</span><span class="sxs-lookup"><span data-stu-id="bd839-128">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="bd839-129">選取 [安裝到虛擬環境] 。</span><span class="sxs-lookup"><span data-stu-id="bd839-129">Select **Install into a virtual environment**.</span></span>
   
    ![外部套件對話方塊](./media/web-sites-python-ptvs-django-mysql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="bd839-131">選取**Python 2.7**或**Python 3.4**為 hello 基底直譯器。</span><span class="sxs-lookup"><span data-stu-id="bd839-131">Select **Python 2.7** or **Python 3.4** as hello base interpreter.</span></span>
   
    ![新增虛擬環境對話方塊](./media/web-sites-python-ptvs-django-mysql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="bd839-133">在**方案總管 中**，hello 專案節點上按一下滑鼠右鍵，然後選取**Python**，然後選取**Django 移轉**。</span><span class="sxs-lookup"><span data-stu-id="bd839-133">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="bd839-134">然後選取 [Django 建立超級使用者] 。</span><span class="sxs-lookup"><span data-stu-id="bd839-134">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="bd839-135">這會開啟 Django 管理主控台，並在 hello 專案資料夾中建立 sqlite 資料庫。</span><span class="sxs-lookup"><span data-stu-id="bd839-135">This will open a Django Management Console and create a sqlite database in hello project folder.</span></span> <span data-ttu-id="bd839-136">請遵循 hello 提示 toocreate 使用者。</span><span class="sxs-lookup"><span data-stu-id="bd839-136">Follow hello prompts toocreate a user.</span></span>
7. <span data-ttu-id="bd839-137">確認 hello 應用程式運作方式是按`F5`。</span><span class="sxs-lookup"><span data-stu-id="bd839-137">Confirm that hello application works by pressing `F5`.</span></span>
8. <span data-ttu-id="bd839-138">按一下**登入**hello 導覽列頂端 hello。</span><span class="sxs-lookup"><span data-stu-id="bd839-138">Click **Log in** from hello navigation bar at hello top.</span></span>
   
    ![Django 導覽列](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="bd839-140">Hello hello 資料庫進行同步處理時所建立的使用者輸入 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="bd839-140">Enter hello credentials for hello user you created when you synchronized hello database.</span></span>
   
    ![登入表單](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="bd839-142">按一下 [Create Sample Polls] 。</span><span class="sxs-lookup"><span data-stu-id="bd839-142">Click **Create Sample Polls**.</span></span>
    
     ![建立範例投票](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="bd839-144">按一下民調並進行投票。</span><span class="sxs-lookup"><span data-stu-id="bd839-144">Click on a poll and vote.</span></span>
    
     ![在範例投票中進行投票](./media/web-sites-python-ptvs-django-mysql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-mysql-database"></a><span data-ttu-id="bd839-146">建立 MySQL Database</span><span class="sxs-lookup"><span data-stu-id="bd839-146">Create a MySQL Database</span></span>
<span data-ttu-id="bd839-147">Hello 資料庫，您將在 Azure 上建立 ClearDB MySQL 裝載的資料庫。</span><span class="sxs-lookup"><span data-stu-id="bd839-147">For hello database, you'll create a ClearDB MySQL hosted database on Azure.</span></span>

<span data-ttu-id="bd839-148">或者，您可以為自己建立在 Azure 中執行的虛擬機器，然後自行安裝和管理 MySQL。</span><span class="sxs-lookup"><span data-stu-id="bd839-148">As an alternative, you can create your own Virtual Machine running in Azure, then install and administer MySQL yourself.</span></span>

<span data-ttu-id="bd839-149">您可以依照下列步驟，透過免費計畫建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="bd839-149">You can create a database with a free plan by following these steps.</span></span>

1. <span data-ttu-id="bd839-150">登入 toohello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="bd839-150">Log in toohello [Azure Portal].</span></span>
2. <span data-ttu-id="bd839-151">在 hello hello 瀏覽窗格的頂端，按一下**新增**，然後按一下**資料 + 儲存體**，然後按一下 **MySQL 資料庫**。</span><span class="sxs-lookup"><span data-stu-id="bd839-151">At hello Top of hello navigation pane, click **NEW**, then click **Data + Storage**, and then click **MySQL Database**.</span></span>
3. <span data-ttu-id="bd839-152">藉由建立新的資源群組設定 hello 新的 MySQL 資料庫並選取 hello 為它的適當位置。</span><span class="sxs-lookup"><span data-stu-id="bd839-152">Configure hello new MySQL database by creating a new resource group and select hello appropriate location for it.</span></span>
4. <span data-ttu-id="bd839-153">一旦建立 hello MySQL 資料庫時，按一下 **屬性**hello 資料庫刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="bd839-153">Once hello MySQL database is created, click **Properties** in hello database blade.</span></span>
5. <span data-ttu-id="bd839-154">使用 hello 複製按鈕 tooput hello 值**連接字串**hello 剪貼簿上。</span><span class="sxs-lookup"><span data-stu-id="bd839-154">Use hello copy button tooput hello value of **CONNECTION STRING** on hello clipboard.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="bd839-155">設定 hello 專案</span><span class="sxs-lookup"><span data-stu-id="bd839-155">Configure hello Project</span></span>
<span data-ttu-id="bd839-156">在本節中，您需要設定 web 應用程式 toouse hello MySQL 資料庫剛剛建立。</span><span class="sxs-lookup"><span data-stu-id="bd839-156">In this section, you'll configure our web app toouse hello MySQL database you just created.</span></span> <span data-ttu-id="bd839-157">您也會使用如 Django 安裝其他的 Python 封裝需要的 toouse MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="bd839-157">You'll also install additional Python packages required toouse MySQL databases with Django.</span></span> <span data-ttu-id="bd839-158">然後您將在本機執行 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bd839-158">Then you'll run hello web app locally.</span></span>

1. <span data-ttu-id="bd839-159">在 Visual Studio 中開啟**settings.py**，從 hello *ProjectName*資料夾。</span><span class="sxs-lookup"><span data-stu-id="bd839-159">In Visual Studio, open **settings.py**, from hello *ProjectName* folder.</span></span> <span data-ttu-id="bd839-160">暫時貼上 hello 編輯器中的 hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="bd839-160">Temporarily paste hello connection string in hello editor.</span></span> <span data-ttu-id="bd839-161">hello 連接字串是以下列格式：</span><span class="sxs-lookup"><span data-stu-id="bd839-161">hello connection string is in this format:</span></span>
   
        Database=<NAME>;Data Source=<HOST>;User Id=<USER>;Password=<PASSWORD>
   
    <span data-ttu-id="bd839-162">變更 hello 預設資料庫**引擎**toouse MySQL，以及組 hello 值**名稱**，**使用者**，**密碼**和**主機**從 hello **CONNECTIONSTRING**。</span><span class="sxs-lookup"><span data-stu-id="bd839-162">Change hello default database **ENGINE** toouse MySQL, and set hello values for **NAME**, **USER**, **PASSWORD** and **HOST** from hello **CONNECTIONSTRING**.</span></span>
   
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
2. <span data-ttu-id="bd839-163">在 方案總管下**Python 環境**，以滑鼠右鍵按一下 hello 虛擬環境，然後選取**安裝 Python 封裝**。</span><span class="sxs-lookup"><span data-stu-id="bd839-163">In Solution Explorer, under **Python Environments**, right-click on hello virtual environment and select **Install Python Package**.</span></span>
3. <span data-ttu-id="bd839-164">安裝套件 hello`mysqlclient`使用**pip**。</span><span class="sxs-lookup"><span data-stu-id="bd839-164">Install hello package `mysqlclient` using **pip**.</span></span>
   
    ![安裝套件對話方塊](./media/web-sites-python-ptvs-django-mysql/PollsDjangoMySQLInstallPackage.png)
4. <span data-ttu-id="bd839-166">在**方案總管 中**，hello 專案節點上按一下滑鼠右鍵，然後選取**Python**，然後選取**Django 移轉**。</span><span class="sxs-lookup"><span data-stu-id="bd839-166">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="bd839-167">然後選取 [Django 建立超級使用者] 。</span><span class="sxs-lookup"><span data-stu-id="bd839-167">Then select **Django Create Superuser**.</span></span>
   
    <span data-ttu-id="bd839-168">這會建立 hello hello 您 hello 前一節中所建立的 MySQL 資料庫的資料表。</span><span class="sxs-lookup"><span data-stu-id="bd839-168">This will create hello tables for hello MySQL database you created in hello previous section.</span></span> <span data-ttu-id="bd839-169">請遵循 hello 提示 toocreate hello 的這篇文章的第一個區段中建立的 hello sqlite 資料庫中沒有 toomatch hello 使用者的使用者。</span><span class="sxs-lookup"><span data-stu-id="bd839-169">Follow hello prompts toocreate a user, which doesn't have toomatch hello user in hello sqlite database created in hello first section of this article.</span></span>
5. <span data-ttu-id="bd839-170">執行與 hello 應用程式`F5`。</span><span class="sxs-lookup"><span data-stu-id="bd839-170">Run hello application with `F5`.</span></span> <span data-ttu-id="bd839-171">利用所建立的輪詢**建立範例輪詢**和送出的投票 hello 資料會序列化 hello MySQL 資料庫中。</span><span class="sxs-lookup"><span data-stu-id="bd839-171">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in hello MySQL database.</span></span>

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="bd839-172">發行 hello web 應用程式 tooAzure 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="bd839-172">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="bd839-173">hello Azure.NET SDK 提供簡單的方式 toodeploy 您 web 應用程式 tooAzure 應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="bd839-173">hello Azure .NET SDK provides an easy way toodeploy your web app tooAzure App Service.</span></span>

1. <span data-ttu-id="bd839-174">在**方案總管 中**，hello 專案節點上按一下滑鼠右鍵，然後選取**發行**。</span><span class="sxs-lookup"><span data-stu-id="bd839-174">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>
   
    ![發行 Web 對話方塊](./media/web-sites-python-ptvs-django-mysql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="bd839-176">按一下 [Microsoft Azure App Service] 。</span><span class="sxs-lookup"><span data-stu-id="bd839-176">Click on **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="bd839-177">按一下**新增**toocreate 新的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bd839-177">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="bd839-178">填寫下列欄位的 hello，並按一下**建立**:</span><span class="sxs-lookup"><span data-stu-id="bd839-178">Fill in hello following fields and click **Create**:</span></span>
   
   * <span data-ttu-id="bd839-179">**Web 應用程式名稱**</span><span class="sxs-lookup"><span data-stu-id="bd839-179">**Web App name**</span></span>
   * <span data-ttu-id="bd839-180">**App Service 計劃**</span><span class="sxs-lookup"><span data-stu-id="bd839-180">**App Service plan**</span></span>
   * <span data-ttu-id="bd839-181">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="bd839-181">**Resource group**</span></span>
   * <span data-ttu-id="bd839-182">**區域**</span><span class="sxs-lookup"><span data-stu-id="bd839-182">**Region**</span></span>
   * <span data-ttu-id="bd839-183">保留**資料庫伺服器**設定得**沒有資料庫**</span><span class="sxs-lookup"><span data-stu-id="bd839-183">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="bd839-184">接受所有其他預設值並按一下 [發佈] 。</span><span class="sxs-lookup"><span data-stu-id="bd839-184">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="bd839-185">網頁瀏覽器會自動開啟 toohello 已發佈的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bd839-185">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="bd839-186">您應該看到 hello web 應用程式工作，如預期般，使用 hello **MySQL**裝載於 Azure 的資料庫。</span><span class="sxs-lookup"><span data-stu-id="bd839-186">You should see hello web app working as expected, using hello **MySQL** database hosted on Azure.</span></span>
   
    ![Web Browser](./media/web-sites-python-ptvs-django-mysql/PollsDjangoAzureBrowser.png)
   
    <span data-ttu-id="bd839-188">恭喜！</span><span class="sxs-lookup"><span data-stu-id="bd839-188">Congratulations!</span></span> <span data-ttu-id="bd839-189">您已成功發行您的 MySQL 為基礎的 web 應用程式 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="bd839-189">You have successfully published your MySQL-based web app tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd839-190">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bd839-190">Next steps</span></span>
<span data-ttu-id="bd839-191">請遵循這些連結 toolearn 更多關於 Python Tools for Visual Studio，如 Django 和 MySQL。</span><span class="sxs-lookup"><span data-stu-id="bd839-191">Follow these links toolearn more about Python Tools for Visual Studio, Django and MySQL.</span></span>

* <span data-ttu-id="bd839-192">[Python Tools for Visual Studio 說明文件]</span><span class="sxs-lookup"><span data-stu-id="bd839-192">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="bd839-193">[Web 專案]</span><span class="sxs-lookup"><span data-stu-id="bd839-193">[Web Projects]</span></span>
  * <span data-ttu-id="bd839-194">[雲端服務專案]</span><span class="sxs-lookup"><span data-stu-id="bd839-194">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="bd839-195">[在 Microsoft Azure 上進行遠端偵錯]</span><span class="sxs-lookup"><span data-stu-id="bd839-195">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="bd839-196">[Django 說明文件]</span><span class="sxs-lookup"><span data-stu-id="bd839-196">[Django Documentation]</span></span>
* <span data-ttu-id="bd839-197">[MySQL]</span><span class="sxs-lookup"><span data-stu-id="bd839-197">[MySQL]</span></span>

<span data-ttu-id="bd839-198">如需詳細資訊，請參閱 hello [Python 開發人員中心](/develop/python/)。</span><span class="sxs-lookup"><span data-stu-id="bd839-198">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

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
