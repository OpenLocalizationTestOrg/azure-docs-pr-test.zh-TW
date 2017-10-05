---
title: "在 Azure 中使用 Django 建立 Web 應用程式"
description: "介紹在 Azure App Service Web Apps 中執行 Python Web 應用程式的教學課程。"
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 9be1a05a-9460-49ae-94fb-9798f82c11cf
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2016
ms.author: huvalo
ms.openlocfilehash: 388a2db21dd1669b48b3204aaa322d7915905506
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="creating-web-apps-with-django-in-azure"></a><span data-ttu-id="05fa4-103">在 Azure 中使用 Django 建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="05fa4-103">Creating web apps with Django in Azure</span></span>
<span data-ttu-id="05fa4-104">本教學課程說明如何在 [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714)上開始執行 Python。</span><span class="sxs-lookup"><span data-stu-id="05fa4-104">This tutorial describes how to get started running Python on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="05fa4-105">Web Apps 提供有限的免費裝載和快速部署，而您可以使用 Python！</span><span class="sxs-lookup"><span data-stu-id="05fa4-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="05fa4-106">隨著應用程式規模增加，您可以切換為付費主控，也可以與其他所有 Azure 服務整合。</span><span class="sxs-lookup"><span data-stu-id="05fa4-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span></span>

<span data-ttu-id="05fa4-107">您將建立使用 Django Web 架構的應用程式 (請參閱本教學課程適用於 [Flask](web-sites-python-create-deploy-flask-app.md) 和 [Bottle](web-sites-python-create-deploy-bottle-app.md) 的替代版本)。</span><span class="sxs-lookup"><span data-stu-id="05fa4-107">You will create an application using the Django web framework (see alternate versions of this tutorial for [Flask](web-sites-python-create-deploy-flask-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span> <span data-ttu-id="05fa4-108">您會從 Azure Marketplace 建立 Web 應用程式、設定 Git 部署，並於本機複製儲存機制。</span><span class="sxs-lookup"><span data-stu-id="05fa4-108">You will create the web app from the Azure Marketplace, set up Git deployment, and clone the repository locally.</span></span> <span data-ttu-id="05fa4-109">然後您會在本機執行應用程式、進行變更、認可和推送至 Azure。</span><span class="sxs-lookup"><span data-stu-id="05fa4-109">Then you will run the application locally, make changes, commit and push them to Azure.</span></span> <span data-ttu-id="05fa4-110">本教學課程示範如何從 Windows 或 Mac/Linux 執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="05fa4-110">The tutorial shows how to do this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="05fa4-111">如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service](https://azure.microsoft.com/try/app-service/)，即可在 App Service 中立即建立短期入門 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="05fa4-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="05fa4-112">不需要信用卡；無需承諾。</span><span class="sxs-lookup"><span data-stu-id="05fa4-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="05fa4-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="05fa4-113">Prerequisites</span></span>
* <span data-ttu-id="05fa4-114">Windows、Mac 或 Linux</span><span class="sxs-lookup"><span data-stu-id="05fa4-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="05fa4-115">Python 2.7 或 3.4</span><span class="sxs-lookup"><span data-stu-id="05fa4-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="05fa4-116">setuptools、pip、virtualenv (僅 Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="05fa4-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="05fa4-117">Git</span><span class="sxs-lookup"><span data-stu-id="05fa4-117">Git</span></span>
* <span data-ttu-id="05fa4-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - 注意：這是選擇性的</span><span class="sxs-lookup"><span data-stu-id="05fa4-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="05fa4-119">**注意**：Python 專案目前不支援 TFS 發佈。</span><span class="sxs-lookup"><span data-stu-id="05fa4-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="05fa4-120">Windows</span><span class="sxs-lookup"><span data-stu-id="05fa4-120">Windows</span></span>
<span data-ttu-id="05fa4-121">如果您還沒有安裝 Python 2.7 或 3.4 (32 位元)，建議您使用 Web Platform Installer 安裝 [Azure SDK for Python 2.7] 或 [Azure SDK for Python 3.4]。</span><span class="sxs-lookup"><span data-stu-id="05fa4-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="05fa4-122">這會安裝 32 位元版本的 Python、setuptools、pip、virtualenv 等 (32 位元 Python 安裝於 Azure 主機電腦上)。</span><span class="sxs-lookup"><span data-stu-id="05fa4-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span></span> <span data-ttu-id="05fa4-123">或者，您可以從 [python.org]取得 Python。</span><span class="sxs-lookup"><span data-stu-id="05fa4-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="05fa4-124">針對 Git，建議您安裝 [Git for Windows] 或 [GitHub for Windows]。</span><span class="sxs-lookup"><span data-stu-id="05fa4-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="05fa4-125">如果您使用 Visual Studio，您可以使用整合式的 Git 支援。</span><span class="sxs-lookup"><span data-stu-id="05fa4-125">If you use Visual Studio, you can use the integrated Git support.</span></span>

<span data-ttu-id="05fa4-126">我們也建議您安裝 [Python Tools 2.2 for Visual Studio]。</span><span class="sxs-lookup"><span data-stu-id="05fa4-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="05fa4-127">這是選擇性的，但如果您有 [Visual Studio](包含免費的 Visual Studio Community 2013 或 Visual Studio Express 2013 for Web)，它會提供您絕佳的 Python IDE。</span><span class="sxs-lookup"><span data-stu-id="05fa4-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="05fa4-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="05fa4-128">Mac/Linux</span></span>
<span data-ttu-id="05fa4-129">您應該已經安裝 Python 與 Git，但請確定您擁有的是 Python 2.7 或 3.4。</span><span class="sxs-lookup"><span data-stu-id="05fa4-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-portal"></a><span data-ttu-id="05fa4-130">在入口網站中建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="05fa4-130">Web App Creation on Portal</span></span>
<span data-ttu-id="05fa4-131">建立應用程式的第一步是透過 [Azure 入口網站](https://portal.azure.com)建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="05fa4-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="05fa4-132">登入 Azure 入口網站中，並按一下左下角的 [新增]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="05fa4-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span></span>
2. <span data-ttu-id="05fa4-133">在搜尋方塊中，輸入 "python"。</span><span class="sxs-lookup"><span data-stu-id="05fa4-133">In the search box, type "python".</span></span>
3. <span data-ttu-id="05fa4-134">在搜尋結果中，選取 [Django (由 PTVS 發佈)]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="05fa4-134">In the search results, select **Django** (published by PTVS), then click **Create**.</span></span>
4. <span data-ttu-id="05fa4-135">設定新的 Django 應用程式，例如為它建立新的應用程式服務方案和新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="05fa4-135">Configure the new Django app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="05fa4-136">然後按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="05fa4-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="05fa4-137">依照 [本機 Git 部署至 Azure App Service](app-service-deploy-local-git.md)的指示，為您新建立的 Web 應用程式設定 Git 發佈功能。</span><span class="sxs-lookup"><span data-stu-id="05fa4-137">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="05fa4-138">應用程式概觀</span><span class="sxs-lookup"><span data-stu-id="05fa4-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="05fa4-139">Git 儲存機制內容</span><span class="sxs-lookup"><span data-stu-id="05fa4-139">Git repository contents</span></span>
<span data-ttu-id="05fa4-140">以下是您會在初始的 Git 儲存機制中找到的檔案概觀，我們將在下一節中複製。</span><span class="sxs-lookup"><span data-stu-id="05fa4-140">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span></span>

    \app\__init__.py
    \app\forms.py
    \app\models.py
    \app\tests.py
    \app\views.py
    \app\static\content\
    \app\static\fonts\
    \app\static\scripts\
    \app\templates\about.html
    \app\templates\contact.html
    \app\templates\index.html
    \app\templates\layout.html
    \app\templates\login.html
    \app\templates\loginpartial.html
    \DjangoWebProject\__init__.py
    \DjangoWebProject\settings.py
    \DjangoWebProject\urls.py
    \DjangoWebProject\wsgi.py

<span data-ttu-id="05fa4-141">應用程式的主要來源。</span><span class="sxs-lookup"><span data-stu-id="05fa4-141">Main sources for the application.</span></span> <span data-ttu-id="05fa4-142">包含 3 個主要的版面配置頁面 (index、about、contact)。</span><span class="sxs-lookup"><span data-stu-id="05fa4-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span> <span data-ttu-id="05fa4-143">靜態內容和指令碼，包含啟動程序、jquery、modernizr 和回應。</span><span class="sxs-lookup"><span data-stu-id="05fa4-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \manage.py

<span data-ttu-id="05fa4-144">本機管理和開發伺服器支援。</span><span class="sxs-lookup"><span data-stu-id="05fa4-144">Local management and development server support.</span></span> <span data-ttu-id="05fa4-145">使用這個選項在本機執行應用程式、同步處理資料庫等等。</span><span class="sxs-lookup"><span data-stu-id="05fa4-145">Use this to run the application locally, synchronize the database, etc.</span></span>

    \db.sqlite3

<span data-ttu-id="05fa4-146">預設資料庫。</span><span class="sxs-lookup"><span data-stu-id="05fa4-146">Default database.</span></span> <span data-ttu-id="05fa4-147">包含所需的資料表，應用程式才能執行，但不包含任何使用者 (同步處理資料庫來建立使用者)。</span><span class="sxs-lookup"><span data-stu-id="05fa4-147">Includes the necessary tables for the application to run, but does not contain any users (synchronize the database to create a user).</span></span>

    \DjangoWebProject.pyproj
    \DjangoWebProject.sln

<span data-ttu-id="05fa4-148">搭配 [Python Tools for Visual Studio]使用的專案檔。</span><span class="sxs-lookup"><span data-stu-id="05fa4-148">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="05fa4-149">虛擬環境和 PTVS 遠端偵錯支援的 IIS Proxy。</span><span class="sxs-lookup"><span data-stu-id="05fa4-149">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="05fa4-150">此應用程式所需的外部封裝。</span><span class="sxs-lookup"><span data-stu-id="05fa4-150">External packages needed by this application.</span></span> <span data-ttu-id="05fa4-151">部署指令碼將 pip 安裝在這個檔案中所列的封裝。</span><span class="sxs-lookup"><span data-stu-id="05fa4-151">The deployment script will pip install the packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="05fa4-152">IIS 組態檔。</span><span class="sxs-lookup"><span data-stu-id="05fa4-152">IIS configuration files.</span></span> <span data-ttu-id="05fa4-153">部署指令碼會使用適當的 web.x.y.config，並將它複製為 web.config。</span><span class="sxs-lookup"><span data-stu-id="05fa4-153">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="05fa4-154">選用的檔案 - 自訂部署</span><span class="sxs-lookup"><span data-stu-id="05fa4-154">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-django-customizing-deployment](../../includes/web-sites-python-django-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="05fa4-155">選用的檔案 - Python 執行階段</span><span class="sxs-lookup"><span data-stu-id="05fa4-155">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="05fa4-156">在伺服器上的其他檔案</span><span class="sxs-lookup"><span data-stu-id="05fa4-156">Additional files on server</span></span>
<span data-ttu-id="05fa4-157">某些檔案存在於伺服器上，但未加入至 Git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="05fa4-157">Some files exist on the server but are not added to the git repository.</span></span> <span data-ttu-id="05fa4-158">這些檔案由部署指令碼建立。</span><span class="sxs-lookup"><span data-stu-id="05fa4-158">These are created by the deployment script.</span></span>

    \web.config

<span data-ttu-id="05fa4-159">IIS 組態檔。</span><span class="sxs-lookup"><span data-stu-id="05fa4-159">IIS configuration file.</span></span> <span data-ttu-id="05fa4-160">從 web.x.y.config 建立於每個部署上。</span><span class="sxs-lookup"><span data-stu-id="05fa4-160">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="05fa4-161">Python 虛擬環境。</span><span class="sxs-lookup"><span data-stu-id="05fa4-161">Python virtual environment.</span></span> <span data-ttu-id="05fa4-162">如果 Web 應用程式上不存在相容的虛擬環境，會於部署期間建立。</span><span class="sxs-lookup"><span data-stu-id="05fa4-162">Created during deployment if a compatible virtual environment doesn't already exist on the web app.</span></span> <span data-ttu-id="05fa4-163">requirements.txt 中所列封裝為 pip 安裝，但是如果封裝已安裝，pip 會跳過安裝。</span><span class="sxs-lookup"><span data-stu-id="05fa4-163">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span></span>

<span data-ttu-id="05fa4-164">接下來的 3 小節會說明如何在 3 個不同環境中繼續進行 Web 應用程式開發：</span><span class="sxs-lookup"><span data-stu-id="05fa4-164">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span></span>

* <span data-ttu-id="05fa4-165">Windows，使用 Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="05fa4-165">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="05fa4-166">Windows，使用命令列</span><span class="sxs-lookup"><span data-stu-id="05fa4-166">Windows, with command line</span></span>
* <span data-ttu-id="05fa4-167">Mac/Linux，使用命令列</span><span class="sxs-lookup"><span data-stu-id="05fa4-167">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="05fa4-168">Web 應用程式開發 - Windows - 適用於 Visual Studio 的 Python 工具</span><span class="sxs-lookup"><span data-stu-id="05fa4-168">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="05fa4-169">複製儲存機制</span><span class="sxs-lookup"><span data-stu-id="05fa4-169">Clone the repository</span></span>
<span data-ttu-id="05fa4-170">首先，使用 Azure 入口網站上提供的 URL 複製儲存機制。</span><span class="sxs-lookup"><span data-stu-id="05fa4-170">First, clone the repository using the URL provided on the Azure Portal.</span></span> <span data-ttu-id="05fa4-171">如需詳細資訊，請參閱 [本機 Git 部署至 Azure App Service](app-service-deploy-local-git.md)。</span><span class="sxs-lookup"><span data-stu-id="05fa4-171">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="05fa4-172">開啟包含在儲存機制根目錄中的方案檔 (.sln)。</span><span class="sxs-lookup"><span data-stu-id="05fa4-172">Open the solution file (.sln) that is included in the root of the repository.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-solution-django.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="05fa4-173">建立虛擬環境</span><span class="sxs-lookup"><span data-stu-id="05fa4-173">Create virtual environment</span></span>
<span data-ttu-id="05fa4-174">現在我們要建立本機開發的虛擬環境。</span><span class="sxs-lookup"><span data-stu-id="05fa4-174">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="05fa4-175">以滑鼠右鍵按一下 [Python 環境]，選取 [新增虛擬環境...]。</span><span class="sxs-lookup"><span data-stu-id="05fa4-175">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="05fa4-176">請確定環境的名稱是 `env`。</span><span class="sxs-lookup"><span data-stu-id="05fa4-176">Make sure the name of the environment is `env`.</span></span>
* <span data-ttu-id="05fa4-177">選取基礎解譯器。</span><span class="sxs-lookup"><span data-stu-id="05fa4-177">Select the base interpreter.</span></span> <span data-ttu-id="05fa4-178">確認使用針對您 Web 應用程式選取的 Python 版本 (在 runtime.txt 中，或在 Azure 入口網站中您的 Web 應用程式的 [應用程式設定]  分頁中) 相同的版本。</span><span class="sxs-lookup"><span data-stu-id="05fa4-178">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>
* <span data-ttu-id="05fa4-179">確定已勾選下載並安裝封裝的選項。</span><span class="sxs-lookup"><span data-stu-id="05fa4-179">Make sure the option to download and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="05fa4-180">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="05fa4-180">Click **Create**.</span></span> <span data-ttu-id="05fa4-181">這會建立虛擬環境，並安裝 requirements.txt 中列出的相依性。</span><span class="sxs-lookup"><span data-stu-id="05fa4-181">This will create the virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="create-a-superuser"></a><span data-ttu-id="05fa4-182">建立超級使用者</span><span class="sxs-lookup"><span data-stu-id="05fa4-182">Create a superuser</span></span>
<span data-ttu-id="05fa4-183">應用程式包含的資料庫並沒有定義任何超級使用者。</span><span class="sxs-lookup"><span data-stu-id="05fa4-183">The database included with the application does not have any superuser defined.</span></span> <span data-ttu-id="05fa4-184">若要使用應用程式登入功能或 Django 管理介面 (如果您決定要啟用它)，您必須建立超級使用者。</span><span class="sxs-lookup"><span data-stu-id="05fa4-184">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span></span>

<span data-ttu-id="05fa4-185">從您專案資料夾的命令列執行：</span><span class="sxs-lookup"><span data-stu-id="05fa4-185">Run this from the command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="05fa4-186">請依照下列提示來設定使用者名稱、密碼等等。</span><span class="sxs-lookup"><span data-stu-id="05fa4-186">Follow the prompts to set the user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="05fa4-187">使用開發伺服器來執行</span><span class="sxs-lookup"><span data-stu-id="05fa4-187">Run using development server</span></span>
<span data-ttu-id="05fa4-188">按 F5 開始偵錯，並且網頁瀏覽器會自動開啟在本機執行的頁面。</span><span class="sxs-lookup"><span data-stu-id="05fa4-188">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

<span data-ttu-id="05fa4-189">您可以在來源中設定中斷點、使用監看式視窗等等。如需各種功能的詳細資訊，請參閱 [Python Tools for Visual Studio 文件]。</span><span class="sxs-lookup"><span data-stu-id="05fa4-189">You can set breakpoints in the sources, use the watch windows, etc. See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="05fa4-190">進行變更</span><span class="sxs-lookup"><span data-stu-id="05fa4-190">Make changes</span></span>
<span data-ttu-id="05fa4-191">現在您可以嘗試對應用程式來源和/或範本進行變更。</span><span class="sxs-lookup"><span data-stu-id="05fa4-191">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="05fa4-192">測試過您的變更之後，請將它們認可至 Git 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="05fa4-192">After you've tested your changes, commit them to the Git repository:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-commit-django.png)

### <a name="install-more-packages"></a><span data-ttu-id="05fa4-193">安裝更多封裝</span><span class="sxs-lookup"><span data-stu-id="05fa4-193">Install more packages</span></span>
<span data-ttu-id="05fa4-194">您的應用程式可能會擁有 Python 和 Django 之外的相依性。</span><span class="sxs-lookup"><span data-stu-id="05fa4-194">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="05fa4-195">您可以使用 pip 安裝其他封裝。</span><span class="sxs-lookup"><span data-stu-id="05fa4-195">You can install additional packages using pip.</span></span> <span data-ttu-id="05fa4-196">若要安裝封裝，以滑鼠右鍵按一下虛擬環境，然後選取 [安裝 Python 封裝] 。</span><span class="sxs-lookup"><span data-stu-id="05fa4-196">To install a package, right-click on the virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="05fa4-197">例如，若要安裝 Azure SDK for Python，讓您可存取 Azure 儲存體、服務匯流排和其他 Azure 服務，請輸入 `azure`：</span><span class="sxs-lookup"><span data-stu-id="05fa4-197">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-install-package-dialog.png)

<span data-ttu-id="05fa4-198">以滑鼠右鍵按一下虛擬環境，然後選取 [產生 requirements.txt]  更新 requirements.txt。</span><span class="sxs-lookup"><span data-stu-id="05fa4-198">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span></span>

<span data-ttu-id="05fa4-199">然後，將變更認可到 Git 儲存機制的 requirements.txt。</span><span class="sxs-lookup"><span data-stu-id="05fa4-199">Then, commit the changes to requirements.txt to the Git repository.</span></span>

### <a name="deploy-to-azure"></a><span data-ttu-id="05fa4-200">部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="05fa4-200">Deploy to Azure</span></span>
<span data-ttu-id="05fa4-201">若要觸發部署，按一下 [同步] 或 [推送]。</span><span class="sxs-lookup"><span data-stu-id="05fa4-201">To trigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="05fa4-202">同步處理會推送和提取。</span><span class="sxs-lookup"><span data-stu-id="05fa4-202">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-git-push.png)

<span data-ttu-id="05fa4-203">第一次部署將需要一些時間，因為它會建立虛擬環境、安裝封裝等。</span><span class="sxs-lookup"><span data-stu-id="05fa4-203">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="05fa4-204">Visual Studio 不會顯示部署進度。</span><span class="sxs-lookup"><span data-stu-id="05fa4-204">Visual Studio doesn't show the progress of the deployment.</span></span> <span data-ttu-id="05fa4-205">如果您想要檢閱輸出，請參閱 [疑難排解 - 部署](#troubleshooting-deployment)一節。</span><span class="sxs-lookup"><span data-stu-id="05fa4-205">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="05fa4-206">瀏覽至 Azure URL，以檢視您的變更。</span><span class="sxs-lookup"><span data-stu-id="05fa4-206">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="05fa4-207">Web 應用程式開發 - Windows - 命令列</span><span class="sxs-lookup"><span data-stu-id="05fa4-207">Web app development - Windows - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="05fa4-208">複製儲存機制</span><span class="sxs-lookup"><span data-stu-id="05fa4-208">Clone the repository</span></span>
<span data-ttu-id="05fa4-209">首先，使用 Azure 入口網站上提供的 URL 複製儲存機制，並將 Azure 儲存機制加入為遠端。</span><span class="sxs-lookup"><span data-stu-id="05fa4-209">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="05fa4-210">如需詳細資訊，請參閱 [本機 Git 部署至 Azure App Service](app-service-deploy-local-git.md)。</span><span class="sxs-lookup"><span data-stu-id="05fa4-210">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="05fa4-211">建立虛擬環境</span><span class="sxs-lookup"><span data-stu-id="05fa4-211">Create virtual environment</span></span>
<span data-ttu-id="05fa4-212">我們要建立開發用途的新虛擬環境 (不加入至儲存機制)。</span><span class="sxs-lookup"><span data-stu-id="05fa4-212">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="05fa4-213">Python 虛擬環境不可重置，因此每位使用該應用程式的開發人員都會在本機建立。</span><span class="sxs-lookup"><span data-stu-id="05fa4-213">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="05fa4-214">務必使用正確的 Python 版本；應與您為 Web 應用程式所選取的版本相同 (在 runtime.txt 中，或在 Azure 入口網站中您的 Web 應用程式的 [應用程式設定] 刀鋒視窗中) 相同的版本。</span><span class="sxs-lookup"><span data-stu-id="05fa4-214">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="05fa4-215">針對 Python 2.7：</span><span class="sxs-lookup"><span data-stu-id="05fa4-215">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="05fa4-216">針對 Python 3.4：</span><span class="sxs-lookup"><span data-stu-id="05fa4-216">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="05fa4-217">安裝應用程式所需的任何外部封裝。</span><span class="sxs-lookup"><span data-stu-id="05fa4-217">Install any external packages required by your application.</span></span> <span data-ttu-id="05fa4-218">您可以在儲存機制的根目錄使用 requirements.txt 檔案，在虛擬環境中安裝封裝：</span><span class="sxs-lookup"><span data-stu-id="05fa4-218">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="05fa4-219">建立超級使用者</span><span class="sxs-lookup"><span data-stu-id="05fa4-219">Create a superuser</span></span>
<span data-ttu-id="05fa4-220">應用程式包含的資料庫並沒有定義任何超級使用者。</span><span class="sxs-lookup"><span data-stu-id="05fa4-220">The database included with the application does not have any superuser defined.</span></span> <span data-ttu-id="05fa4-221">若要使用應用程式登入功能或 Django 管理介面 (如果您決定要啟用它)，您必須建立超級使用者。</span><span class="sxs-lookup"><span data-stu-id="05fa4-221">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span></span>

<span data-ttu-id="05fa4-222">從您專案資料夾的命令列執行：</span><span class="sxs-lookup"><span data-stu-id="05fa4-222">Run this from the command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="05fa4-223">請依照下列提示來設定使用者名稱、密碼等等。</span><span class="sxs-lookup"><span data-stu-id="05fa4-223">Follow the prompts to set the user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="05fa4-224">使用開發伺服器來執行</span><span class="sxs-lookup"><span data-stu-id="05fa4-224">Run using development server</span></span>
<span data-ttu-id="05fa4-225">您可以使用下列命令，在開發伺服器下啟動應用程式：</span><span class="sxs-lookup"><span data-stu-id="05fa4-225">You can launch the application under a development server with the following command:</span></span>

    env\scripts\python manage.py runserver

<span data-ttu-id="05fa4-226">主控台會顯示 URL，以及伺服器接聽的通訊埠：</span><span class="sxs-lookup"><span data-stu-id="05fa4-226">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-run-local-django.png)

<span data-ttu-id="05fa4-227">然後，開啟網頁瀏覽器指向該 URL。</span><span class="sxs-lookup"><span data-stu-id="05fa4-227">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="05fa4-228">進行變更</span><span class="sxs-lookup"><span data-stu-id="05fa4-228">Make changes</span></span>
<span data-ttu-id="05fa4-229">現在您可以嘗試對應用程式來源和/或範本進行變更。</span><span class="sxs-lookup"><span data-stu-id="05fa4-229">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="05fa4-230">測試過您的變更之後，請將它們認可至 Git 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="05fa4-230">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="05fa4-231">安裝更多封裝</span><span class="sxs-lookup"><span data-stu-id="05fa4-231">Install more packages</span></span>
<span data-ttu-id="05fa4-232">您的應用程式可能會擁有 Python 和 Django 之外的相依性。</span><span class="sxs-lookup"><span data-stu-id="05fa4-232">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="05fa4-233">您可以使用 pip 安裝其他封裝。</span><span class="sxs-lookup"><span data-stu-id="05fa4-233">You can install additional packages using pip.</span></span> <span data-ttu-id="05fa4-234">例如，若要安裝 Azure SDK for Python，讓您可存取 Azure 儲存體、服務匯流排和其他 Azure 服務，請輸入：</span><span class="sxs-lookup"><span data-stu-id="05fa4-234">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="05fa4-235">請務必更新 requirements.txt：</span><span class="sxs-lookup"><span data-stu-id="05fa4-235">Make sure to update requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="05fa4-236">認可變更：</span><span class="sxs-lookup"><span data-stu-id="05fa4-236">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="05fa4-237">部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="05fa4-237">Deploy to Azure</span></span>
<span data-ttu-id="05fa4-238">若要觸發部署，將變更推送至 Azure：</span><span class="sxs-lookup"><span data-stu-id="05fa4-238">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="05fa4-239">您會看到部署指令碼的輸出，包括虛擬環境建立、安裝封裝、建立 web.config。</span><span class="sxs-lookup"><span data-stu-id="05fa4-239">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="05fa4-240">瀏覽至 Azure URL，以檢視您的變更。</span><span class="sxs-lookup"><span data-stu-id="05fa4-240">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="05fa4-241">Web 應用程式開發 - Mac/Linux - 命令列</span><span class="sxs-lookup"><span data-stu-id="05fa4-241">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="05fa4-242">複製儲存機制</span><span class="sxs-lookup"><span data-stu-id="05fa4-242">Clone the repository</span></span>
<span data-ttu-id="05fa4-243">首先，使用 Azure 入口網站上提供的 URL 複製儲存機制，並將 Azure 儲存機制加入為遠端。</span><span class="sxs-lookup"><span data-stu-id="05fa4-243">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="05fa4-244">如需詳細資訊，請參閱 [本機 Git 部署至 Azure App Service](app-service-deploy-local-git.md)。</span><span class="sxs-lookup"><span data-stu-id="05fa4-244">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="05fa4-245">建立虛擬環境</span><span class="sxs-lookup"><span data-stu-id="05fa4-245">Create virtual environment</span></span>
<span data-ttu-id="05fa4-246">我們要建立開發用途的新虛擬環境 (不加入至儲存機制)。</span><span class="sxs-lookup"><span data-stu-id="05fa4-246">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="05fa4-247">Python 虛擬環境不可重置，因此每位使用該應用程式的開發人員都會在本機建立。</span><span class="sxs-lookup"><span data-stu-id="05fa4-247">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="05fa4-248">務必使用正確的 Python 版本；應與您為 Web 應用程式所選取的版本相同 (在 runtime.txt 中，或在 Azure 入口網站中您的 Web 應用程式的 [應用程式設定] 刀鋒視窗中) 相同的版本。</span><span class="sxs-lookup"><span data-stu-id="05fa4-248">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="05fa4-249">針對 Python 2.7：</span><span class="sxs-lookup"><span data-stu-id="05fa4-249">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="05fa4-250">針對 Python 3.4：</span><span class="sxs-lookup"><span data-stu-id="05fa4-250">For Python 3.4:</span></span>

    python -m venv env

<span data-ttu-id="05fa4-251">或</span><span class="sxs-lookup"><span data-stu-id="05fa4-251">or</span></span>

    pyvenv env

<span data-ttu-id="05fa4-252">安裝應用程式所需的任何外部封裝。</span><span class="sxs-lookup"><span data-stu-id="05fa4-252">Install any external packages required by your application.</span></span> <span data-ttu-id="05fa4-253">您可以在儲存機制的根目錄使用 requirements.txt 檔案，在虛擬環境中安裝封裝：</span><span class="sxs-lookup"><span data-stu-id="05fa4-253">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="05fa4-254">建立超級使用者</span><span class="sxs-lookup"><span data-stu-id="05fa4-254">Create a superuser</span></span>
<span data-ttu-id="05fa4-255">應用程式包含的資料庫並沒有定義任何超級使用者。</span><span class="sxs-lookup"><span data-stu-id="05fa4-255">The database included with the application does not have any superuser defined.</span></span> <span data-ttu-id="05fa4-256">若要使用應用程式登入功能或 Django 管理介面 (如果您決定要啟用它)，您必須建立超級使用者。</span><span class="sxs-lookup"><span data-stu-id="05fa4-256">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span></span>

<span data-ttu-id="05fa4-257">從您專案資料夾的命令列執行：</span><span class="sxs-lookup"><span data-stu-id="05fa4-257">Run this from the command-line from your project folder:</span></span>

    env/bin/python manage.py createsuperuser

<span data-ttu-id="05fa4-258">請依照下列提示來設定使用者名稱、密碼等等。</span><span class="sxs-lookup"><span data-stu-id="05fa4-258">Follow the prompts to set the user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="05fa4-259">使用開發伺服器來執行</span><span class="sxs-lookup"><span data-stu-id="05fa4-259">Run using development server</span></span>
<span data-ttu-id="05fa4-260">您可以使用下列命令，在開發伺服器下啟動應用程式：</span><span class="sxs-lookup"><span data-stu-id="05fa4-260">You can launch the application under a development server with the following command:</span></span>

    env/bin/python manage.py runserver

<span data-ttu-id="05fa4-261">主控台會顯示 URL，以及伺服器接聽的通訊埠：</span><span class="sxs-lookup"><span data-stu-id="05fa4-261">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-run-local-django.png)

<span data-ttu-id="05fa4-262">然後，開啟網頁瀏覽器指向該 URL。</span><span class="sxs-lookup"><span data-stu-id="05fa4-262">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="05fa4-263">進行變更</span><span class="sxs-lookup"><span data-stu-id="05fa4-263">Make changes</span></span>
<span data-ttu-id="05fa4-264">現在您可以嘗試對應用程式來源和/或範本進行變更。</span><span class="sxs-lookup"><span data-stu-id="05fa4-264">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="05fa4-265">測試過您的變更之後，請將它們認可至 Git 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="05fa4-265">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="05fa4-266">安裝更多封裝</span><span class="sxs-lookup"><span data-stu-id="05fa4-266">Install more packages</span></span>
<span data-ttu-id="05fa4-267">您的應用程式可能會擁有 Python 和 Django 之外的相依性。</span><span class="sxs-lookup"><span data-stu-id="05fa4-267">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="05fa4-268">您可以使用 pip 安裝其他封裝。</span><span class="sxs-lookup"><span data-stu-id="05fa4-268">You can install additional packages using pip.</span></span> <span data-ttu-id="05fa4-269">例如，若要安裝 Azure SDK for Python，讓您可存取 Azure 儲存體、服務匯流排和其他 Azure 服務，請輸入：</span><span class="sxs-lookup"><span data-stu-id="05fa4-269">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="05fa4-270">請務必更新 requirements.txt：</span><span class="sxs-lookup"><span data-stu-id="05fa4-270">Make sure to update requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="05fa4-271">認可變更：</span><span class="sxs-lookup"><span data-stu-id="05fa4-271">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="05fa4-272">部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="05fa4-272">Deploy to Azure</span></span>
<span data-ttu-id="05fa4-273">若要觸發部署，將變更推送至 Azure：</span><span class="sxs-lookup"><span data-stu-id="05fa4-273">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="05fa4-274">您會看到部署指令碼的輸出，包括虛擬環境建立、安裝封裝、建立 web.config。</span><span class="sxs-lookup"><span data-stu-id="05fa4-274">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="05fa4-275">瀏覽至 Azure URL，以檢視您的變更。</span><span class="sxs-lookup"><span data-stu-id="05fa4-275">Browse to the Azure URL to view your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="05fa4-276">疑難排解 - 封裝安裝</span><span class="sxs-lookup"><span data-stu-id="05fa4-276">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="05fa4-277">疑難排解 - 虛擬環境</span><span class="sxs-lookup"><span data-stu-id="05fa4-277">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="troubleshooting---static-files"></a><span data-ttu-id="05fa4-278">疑難排解 - 靜態檔案</span><span class="sxs-lookup"><span data-stu-id="05fa4-278">Troubleshooting - Static Files</span></span>
<span data-ttu-id="05fa4-279">Django 具有收集靜態檔案的概念。</span><span class="sxs-lookup"><span data-stu-id="05fa4-279">Django has the concept of collecting static files.</span></span> <span data-ttu-id="05fa4-280">這會從原始位置取得所有靜態檔案，並將它們複製到單一資料夾。</span><span class="sxs-lookup"><span data-stu-id="05fa4-280">This takes all the static files from their original location and copies them to a single folder.</span></span> <span data-ttu-id="05fa4-281">針對此應用程式，它們會複製到 `/static`。</span><span class="sxs-lookup"><span data-stu-id="05fa4-281">For this application, they are copied to `/static`.</span></span>

<span data-ttu-id="05fa4-282">這是因為靜態檔案可能來自不同的 Django「應用程式」。</span><span class="sxs-lookup"><span data-stu-id="05fa4-282">This is done because static files may come from different Django 'apps'.</span></span> <span data-ttu-id="05fa4-283">例如，Django 管理介面的靜態檔案位於虛擬環境中的 Django 程式庫子資料夾。</span><span class="sxs-lookup"><span data-stu-id="05fa4-283">For example, the static files from the Django admin interfaces are located in a Django library subfolder in the virtual environment.</span></span> <span data-ttu-id="05fa4-284">此應用程式所定義的靜態檔案位於 `/app/static`。</span><span class="sxs-lookup"><span data-stu-id="05fa4-284">Static files defined by this application are located in `/app/static`.</span></span> <span data-ttu-id="05fa4-285">當您使用多個 Django「應用程式」時 ，您必須擁有位於多個位置中的靜態檔案。</span><span class="sxs-lookup"><span data-stu-id="05fa4-285">As you use more Django 'apps', you'll have static files located in multiple places.</span></span>

<span data-ttu-id="05fa4-286">當在偵錯模式中執行應用程式，應用程式會從其原始位置提供靜態檔案。</span><span class="sxs-lookup"><span data-stu-id="05fa4-286">When running the application in debug mode, the application serves the static files from their original location.</span></span>

<span data-ttu-id="05fa4-287">在發行模式中執行應用程式，應用程式 **不會** 提供靜態檔案。</span><span class="sxs-lookup"><span data-stu-id="05fa4-287">When running the application in release mode, the application does **not** serve the static files.</span></span> <span data-ttu-id="05fa4-288">Web 伺服器的責任就是提供檔案。</span><span class="sxs-lookup"><span data-stu-id="05fa4-288">It is the responsibility of the web server to serve the files.</span></span> <span data-ttu-id="05fa4-289">針對此應用程式，IIS 將會從 `/static`提供靜態檔案。</span><span class="sxs-lookup"><span data-stu-id="05fa4-289">For this application, IIS will serve the static files from `/static`.</span></span>

<span data-ttu-id="05fa4-290">靜態檔案的集合會做為部署指令碼的一部分自動完成，清除先前收集的檔案。</span><span class="sxs-lookup"><span data-stu-id="05fa4-290">The collection of static files is done automatically as part of the deployment script, clearing previously collected files.</span></span> <span data-ttu-id="05fa4-291">這表示此集合會發生在每個部署上、稍微降低部署速度，但它可確保已過時的檔案無法使用，避免潛在的安全性問題。</span><span class="sxs-lookup"><span data-stu-id="05fa4-291">This means the collection occurs on every deployment, slowing down deployment a bit, but it ensures that obsolete files won't be available, avoiding a potential security issue.</span></span>

<span data-ttu-id="05fa4-292">如果您想要跳過 Django 應用程式的靜態檔案收集：</span><span class="sxs-lookup"><span data-stu-id="05fa4-292">If you want to skip collection of static files for your Django application:</span></span>

    \.skipDjango

<span data-ttu-id="05fa4-293">那麼您必須要在本機電腦，手動執行收集：</span><span class="sxs-lookup"><span data-stu-id="05fa4-293">Then you'll need to do the collection manually on your local machine:</span></span>

    env\scripts\python manage.py collectstatic

<span data-ttu-id="05fa4-294">然後從 `.gitignore` 移除 `\static` 資料夾，並將它加入至 Git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="05fa4-294">Then remove the `\static` folder from `.gitignore` and add it to the Git repository.</span></span>

## <a name="troubleshooting---settings"></a><span data-ttu-id="05fa4-295">疑難排解 - 設定</span><span class="sxs-lookup"><span data-stu-id="05fa4-295">Troubleshooting - Settings</span></span>
<span data-ttu-id="05fa4-296">應用程式的各種設定可以在 `DjangoWebProject/settings.py`變更。</span><span class="sxs-lookup"><span data-stu-id="05fa4-296">Various settings for the application can be changed in `DjangoWebProject/settings.py`.</span></span>

<span data-ttu-id="05fa4-297">為了開發人員方便起見，已啟用偵錯模式。</span><span class="sxs-lookup"><span data-stu-id="05fa4-297">For developer convenience, debug mode is enabled.</span></span> <span data-ttu-id="05fa4-298">其中一項不錯的副作用是，您能在本機執行時看見映像和其他靜態內容，而不需要收集靜態檔案。</span><span class="sxs-lookup"><span data-stu-id="05fa4-298">One nice side effect of that is you'll be able to see images and other static content when running locally, without having to collect static files.</span></span>

<span data-ttu-id="05fa4-299">若要停用偵錯模式：</span><span class="sxs-lookup"><span data-stu-id="05fa4-299">To disable debug mode:</span></span>

    DEBUG = False

<span data-ttu-id="05fa4-300">停用偵錯時，需要更新 `ALLOWED_HOSTS` 值以包含 Azure 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="05fa4-300">When debug is disabled, the value for `ALLOWED_HOSTS` needs to be updated to include the Azure host name.</span></span> <span data-ttu-id="05fa4-301">例如：</span><span class="sxs-lookup"><span data-stu-id="05fa4-301">For example:</span></span>

    ALLOWED_HOSTS = (
        'pythonapp.azurewebsites.net',
    )

<span data-ttu-id="05fa4-302">或啟用任何：</span><span class="sxs-lookup"><span data-stu-id="05fa4-302">or to enable any:</span></span>

    ALLOWED_HOSTS = (
        '*',
    )

<span data-ttu-id="05fa4-303">在實務上，您可能希望進行更複雜的操作，以應付在偵錯和發行模式之間切換，以及取得主機名稱。</span><span class="sxs-lookup"><span data-stu-id="05fa4-303">In practice, you may want to do something more complex to deal with switching between debug and release mode, and getting the host name.</span></span>

<span data-ttu-id="05fa4-304">您可以透過 Azure 入口網站中的 [設定] 頁面來設定環境變數 (在 [應用程式設定] 區段中)。</span><span class="sxs-lookup"><span data-stu-id="05fa4-304">You can set environment variables through the Azure portal **CONFIGURE** page, in the **app settings** section.</span></span>  <span data-ttu-id="05fa4-305">這對設定您不想要顯示於來源 (連接字串、密碼等等) 中的值，或是您想要 Azure 與本機電腦有不同設定時很有幫助。</span><span class="sxs-lookup"><span data-stu-id="05fa4-305">This can be useful for setting values that you may not want to appear in the sources (connection strings, passwords, etc), or that you want to set differently between Azure and your local machine.</span></span> <span data-ttu-id="05fa4-306">在 `settings.py` 中，您可以使用 `os.getenv` 查詢環境變數。</span><span class="sxs-lookup"><span data-stu-id="05fa4-306">In `settings.py`, you can query the environment variables using `os.getenv`.</span></span>

## <a name="using-a-database"></a><span data-ttu-id="05fa4-307">使用資料庫</span><span class="sxs-lookup"><span data-stu-id="05fa4-307">Using a Database</span></span>
<span data-ttu-id="05fa4-308">應用程式隨附的資料庫為 SQLite 資料庫</span><span class="sxs-lookup"><span data-stu-id="05fa4-308">The database that is included with the application is a sqlite database.</span></span> <span data-ttu-id="05fa4-309">這是用於開發、方便實用的預設資料庫，因為它幾乎不需要設定。</span><span class="sxs-lookup"><span data-stu-id="05fa4-309">This is a convenient and useful default database to use for development, as it requires almost no setup.</span></span> <span data-ttu-id="05fa4-310">資料庫會儲存在專案資料夾中的 db.sqlite3 檔案。</span><span class="sxs-lookup"><span data-stu-id="05fa4-310">The database is stored in the db.sqlite3 file in the project folder.</span></span>

<span data-ttu-id="05fa4-311">Azure 提供了資料庫服務，可從 Django 應用程式輕鬆使用。</span><span class="sxs-lookup"><span data-stu-id="05fa4-311">Azure provides database services which are easy to use from a Django application.</span></span> <span data-ttu-id="05fa4-312">從 Django 應用程式使用 [SQL Database] 和 [MySQL] 的教學課程，會示範建立資料庫服務、在 `DjangoWebProject/settings.py` 中變更資料庫設定，以及必須安裝組件庫的必要步驟。</span><span class="sxs-lookup"><span data-stu-id="05fa4-312">Tutorials for using [SQL Database] and [MySQL] from a Django application show the steps necessary to create the database service, change the database settings in `DjangoWebProject/settings.py`, and the libraries required to install.</span></span>

<span data-ttu-id="05fa4-313">當然，如果您偏好管理您自己的資料庫伺服器，您可以使用在 Azure 上執行的 Windows 或 Linux 的虛擬機器做到這點。</span><span class="sxs-lookup"><span data-stu-id="05fa4-313">Of course, if you prefer to manage your own database servers, you can do so using Windows or Linux virtual machines running on Azure.</span></span>

## <a name="django-admin-interface"></a><span data-ttu-id="05fa4-314">Django 管理介面</span><span class="sxs-lookup"><span data-stu-id="05fa4-314">Django Admin Interface</span></span>
<span data-ttu-id="05fa4-315">一旦您開始建置您的模型，您會想要在資料庫內填入一些資料。</span><span class="sxs-lookup"><span data-stu-id="05fa4-315">Once you start building your models, you'll want to populate the database with some data.</span></span> <span data-ttu-id="05fa4-316">使用 Django 管理介面可利用互動的方式，輕鬆新增並管理內容。</span><span class="sxs-lookup"><span data-stu-id="05fa4-316">An easy way to do add and edit content interactively is to use the Django administration interface.</span></span>

<span data-ttu-id="05fa4-317">已取消註解應用程式來源中的管理介面程式碼，但已清楚標示，您可以輕鬆啟用它 (搜尋 'admin')。</span><span class="sxs-lookup"><span data-stu-id="05fa4-317">The code for the admin interface is commented out in the application sources, but it's clearly marked so you can easily enable it (search for 'admin').</span></span>

<span data-ttu-id="05fa4-318">啟用後，同步處理資料庫、執行應用程式並瀏覽至 `/admin`。</span><span class="sxs-lookup"><span data-stu-id="05fa4-318">After it's enabled, synchronize the database, run the application and navigate to `/admin`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05fa4-319">後續步驟</span><span class="sxs-lookup"><span data-stu-id="05fa4-319">Next Steps</span></span>
<span data-ttu-id="05fa4-320">請遵循下列連結以深入了解 Django 和 Python Tools for Visual Studio：</span><span class="sxs-lookup"><span data-stu-id="05fa4-320">Follow these links to learn more about Django and Python Tools for Visual Studio:</span></span>

* <span data-ttu-id="05fa4-321">[Django 說明文件]</span><span class="sxs-lookup"><span data-stu-id="05fa4-321">[Django Documentation]</span></span>
* <span data-ttu-id="05fa4-322">[Python Tools for Visual Studio 文件]</span><span class="sxs-lookup"><span data-stu-id="05fa4-322">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="05fa4-323">如需使用 SQL Database 和 MySQL 的資訊：</span><span class="sxs-lookup"><span data-stu-id="05fa4-323">For information on using SQL Database and MySQL:</span></span>

* <span data-ttu-id="05fa4-324">[Azure 上使用 Python Tools for Visual Studio 的 Django 和 MySQL]</span><span class="sxs-lookup"><span data-stu-id="05fa4-324">[Django and MySQL on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="05fa4-325">[Azure 上使用 Python Tools for Visual Studio 的 Django 和 SQL Database]</span><span class="sxs-lookup"><span data-stu-id="05fa4-325">[Django and SQL Database on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="05fa4-326">如需詳細資訊，請參閱 [Python 開發人員中心](/develop/python/)。</span><span class="sxs-lookup"><span data-stu-id="05fa4-326">For more information, see the [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="05fa4-327">變更的項目</span><span class="sxs-lookup"><span data-stu-id="05fa4-327">What's changed</span></span>
* <span data-ttu-id="05fa4-328">如需從網站變更為 App Service 的指南，請參閱： [Azure App Service 及其對現有 Azure 服務的影響](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="05fa4-328">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Azure 上使用 Python Tools for Visual Studio 的 Django 和 MySQL]: web-sites-python-ptvs-django-mysql.md
[Azure 上使用 Python Tools for Visual Studio 的 Django 和 SQL Database]: web-sites-python-ptvs-django-sql.md
[SQL Database]: web-sites-python-ptvs-django-sql.md
[MySQL]: web-sites-python-ptvs-django-mysql.md

<!--External Link references-->
[Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281
[Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990
[python.org]: http://www.python.org/
[Git for Windows]: http://msysgit.github.io/
[GitHub for Windows]: https://windows.github.com/
[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Visual Studio]: http://www.visualstudio.com/
[Python Tools for Visual Studio 文件]: http://aka.ms/ptvsdocs
[Django 說明文件]: https://www.djangoproject.com/
