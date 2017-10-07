---
title: "在 Azure 中的 Django aaaCreating web 應用程式"
description: "此教學課程為您介紹 toorunning Python web 應用程式在 Azure App Service Web 應用程式。"
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
ms.openlocfilehash: 26a131da358748bd6fe4ee5c114d0a8f91b83cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-django-in-azure"></a><span data-ttu-id="c77fb-103">在 Azure 中使用 Django 建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="c77fb-103">Creating web apps with Django in Azure</span></span>
<span data-ttu-id="c77fb-104">這個教學課程描述如何 tooget 啟動上執行 Python [Azure App Service Web 應用程式](http://go.microsoft.com/fwlink/?LinkId=529714)。</span><span class="sxs-lookup"><span data-stu-id="c77fb-104">This tutorial describes how tooget started running Python on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="c77fb-105">Web Apps 提供有限的免費裝載和快速部署，而您可以使用 Python！</span><span class="sxs-lookup"><span data-stu-id="c77fb-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="c77fb-106">當您的應用程式成長，您可以切換 toopaid 裝載，您也可以與所有的整合 hello 其他 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="c77fb-106">As your app grows, you can switch toopaid hosting, and you can also integrate with all of hello other Azure services.</span></span>

<span data-ttu-id="c77fb-107">您將建立使用 hello Django web 架構的應用程式 (請參閱本教學課程中的替代版本[酒瓶](web-sites-python-create-deploy-flask-app.md)和[Bottle](web-sites-python-create-deploy-bottle-app.md))。</span><span class="sxs-lookup"><span data-stu-id="c77fb-107">You will create an application using hello Django web framework (see alternate versions of this tutorial for [Flask](web-sites-python-create-deploy-flask-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span> <span data-ttu-id="c77fb-108">您會建立從 hello Azure Marketplace 的 hello web 應用程式、 設定 Git 部署和複製本機 hello 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="c77fb-108">You will create hello web app from hello Azure Marketplace, set up Git deployment, and clone hello repository locally.</span></span> <span data-ttu-id="c77fb-109">然後，您會在本機執行 hello 應用程式、 進行變更、 認可並推送它們 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="c77fb-109">Then you will run hello application locally, make changes, commit and push them tooAzure.</span></span> <span data-ttu-id="c77fb-110">hello 教學課程顯示如何 toodo 於 Windows 或 Mac/Linux。</span><span class="sxs-lookup"><span data-stu-id="c77fb-110">hello tutorial shows how toodo this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="c77fb-111">如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="c77fb-111">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="c77fb-112">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="c77fb-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="c77fb-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="c77fb-113">Prerequisites</span></span>
* <span data-ttu-id="c77fb-114">Windows、Mac 或 Linux</span><span class="sxs-lookup"><span data-stu-id="c77fb-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="c77fb-115">Python 2.7 或 3.4</span><span class="sxs-lookup"><span data-stu-id="c77fb-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="c77fb-116">setuptools、pip、virtualenv (僅 Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="c77fb-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="c77fb-117">Git</span><span class="sxs-lookup"><span data-stu-id="c77fb-117">Git</span></span>
* <span data-ttu-id="c77fb-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - 注意：這是選擇性的</span><span class="sxs-lookup"><span data-stu-id="c77fb-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="c77fb-119">**注意**：Python 專案目前不支援 TFS 發佈。</span><span class="sxs-lookup"><span data-stu-id="c77fb-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="c77fb-120">Windows</span><span class="sxs-lookup"><span data-stu-id="c77fb-120">Windows</span></span>
<span data-ttu-id="c77fb-121">如果您還沒有安裝 Python 2.7 或 3.4 (32 位元)，建議您使用 Web Platform Installer 安裝 [Azure SDK for Python 2.7] 或 [Azure SDK for Python 3.4]。</span><span class="sxs-lookup"><span data-stu-id="c77fb-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="c77fb-122">這會安裝 hello 32 位元版本的 Python、 setuptools、 pip、 virtualenv 等 （32 位元 Python 是 hello Azure 主機機器上安裝的內容）。</span><span class="sxs-lookup"><span data-stu-id="c77fb-122">This installs hello 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on hello Azure host machines).</span></span> <span data-ttu-id="c77fb-123">或者，您可以從 [python.org]取得 Python。</span><span class="sxs-lookup"><span data-stu-id="c77fb-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="c77fb-124">針對 Git，建議您安裝 [Git for Windows] 或 [GitHub for Windows]。</span><span class="sxs-lookup"><span data-stu-id="c77fb-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="c77fb-125">如果您使用 Visual Studio，您可以使用整合的 hello Git 支援。</span><span class="sxs-lookup"><span data-stu-id="c77fb-125">If you use Visual Studio, you can use hello integrated Git support.</span></span>

<span data-ttu-id="c77fb-126">我們也建議您安裝 [Python Tools 2.2 for Visual Studio]。</span><span class="sxs-lookup"><span data-stu-id="c77fb-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="c77fb-127">這是選擇性的但如果您有[Visual Studio]，包括 hello 釋放 Visual Studio Community 2013 或 Visual Studio Express 2013 for Web，則這會提供絕佳的 Python IDE。</span><span class="sxs-lookup"><span data-stu-id="c77fb-127">This is optional, but if you have [Visual Studio], including hello free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="c77fb-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="c77fb-128">Mac/Linux</span></span>
<span data-ttu-id="c77fb-129">您應該已經安裝 Python 與 Git，但請確定您擁有的是 Python 2.7 或 3.4。</span><span class="sxs-lookup"><span data-stu-id="c77fb-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-portal"></a><span data-ttu-id="c77fb-130">在入口網站中建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="c77fb-130">Web App Creation on Portal</span></span>
<span data-ttu-id="c77fb-131">hello 第一個步驟中建立您的應用程式是 toocreate hello web 應用程式，透過 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="c77fb-131">hello first step in creating your app is toocreate hello web app via hello [Azure Portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="c77fb-132">登入 hello Azure 入口網站並按一下 hello**新增**hello 左下角中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="c77fb-132">Log into hello Azure Portal and click hello **NEW** button in hello bottom left corner.</span></span>
2. <span data-ttu-id="c77fb-133">在 hello 搜尋方塊中輸入"python"。</span><span class="sxs-lookup"><span data-stu-id="c77fb-133">In hello search box, type "python".</span></span>
3. <span data-ttu-id="c77fb-134">在 hello 搜尋結果中，選取  **Django** （發行 PTVS），然後按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="c77fb-134">In hello search results, select **Django** (published by PTVS), then click **Create**.</span></span>
4. <span data-ttu-id="c77fb-135">設定 hello 新 Django 應用程式，例如為它建立新的應用程式服務方案和新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="c77fb-135">Configure hello new Django app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="c77fb-136">然後按一下 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="c77fb-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="c77fb-137">設定 Git 發行功能，新建立的 web 應用程式在 hello 指示[應用程式服務的本機 Git 部署 tooAzure](app-service-deploy-local-git.md)。</span><span class="sxs-lookup"><span data-stu-id="c77fb-137">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="c77fb-138">應用程式概觀</span><span class="sxs-lookup"><span data-stu-id="c77fb-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="c77fb-139">Git 儲存機制內容</span><span class="sxs-lookup"><span data-stu-id="c77fb-139">Git repository contents</span></span>
<span data-ttu-id="c77fb-140">以下是您會發現在 hello 初始 Git 儲存機制，我們將複製 hello 下一節中的 hello 檔案的概觀。</span><span class="sxs-lookup"><span data-stu-id="c77fb-140">Here's an overview of hello files you'll find in hello initial Git repository, which we'll clone in hello next section.</span></span>

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

<span data-ttu-id="c77fb-141">Hello 應用程式的主要來源。</span><span class="sxs-lookup"><span data-stu-id="c77fb-141">Main sources for hello application.</span></span> <span data-ttu-id="c77fb-142">包含 3 個主要的版面配置頁面 (index、about、contact)。</span><span class="sxs-lookup"><span data-stu-id="c77fb-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span> <span data-ttu-id="c77fb-143">靜態內容和指令碼，包含啟動程序、jquery、modernizr 和回應。</span><span class="sxs-lookup"><span data-stu-id="c77fb-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \manage.py

<span data-ttu-id="c77fb-144">本機管理和開發伺服器支援。</span><span class="sxs-lookup"><span data-stu-id="c77fb-144">Local management and development server support.</span></span> <span data-ttu-id="c77fb-145">在本機上使用此 toorun hello 應用程式，同步處理 hello 資料庫等等。</span><span class="sxs-lookup"><span data-stu-id="c77fb-145">Use this toorun hello application locally, synchronize hello database, etc.</span></span>

    \db.sqlite3

<span data-ttu-id="c77fb-146">預設資料庫。</span><span class="sxs-lookup"><span data-stu-id="c77fb-146">Default database.</span></span> <span data-ttu-id="c77fb-147">包含 hello hello 應用程式 toorun，針對必要的資料表，但不包含任何使用者 （同步處理 hello 資料庫 toocreate 使用者）。</span><span class="sxs-lookup"><span data-stu-id="c77fb-147">Includes hello necessary tables for hello application toorun, but does not contain any users (synchronize hello database toocreate a user).</span></span>

    \DjangoWebProject.pyproj
    \DjangoWebProject.sln

<span data-ttu-id="c77fb-148">搭配 [Python Tools for Visual Studio]使用的專案檔。</span><span class="sxs-lookup"><span data-stu-id="c77fb-148">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="c77fb-149">虛擬環境和 PTVS 遠端偵錯支援的 IIS Proxy。</span><span class="sxs-lookup"><span data-stu-id="c77fb-149">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="c77fb-150">此應用程式所需的外部封裝。</span><span class="sxs-lookup"><span data-stu-id="c77fb-150">External packages needed by this application.</span></span> <span data-ttu-id="c77fb-151">hello 部署指令碼將 pip 安裝 hello 封裝這個檔案中列出。</span><span class="sxs-lookup"><span data-stu-id="c77fb-151">hello deployment script will pip install hello packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="c77fb-152">IIS 組態檔。</span><span class="sxs-lookup"><span data-stu-id="c77fb-152">IIS configuration files.</span></span> <span data-ttu-id="c77fb-153">將使用 hello 適當 web.x.y.config hello 部署指令碼，並將它複製為 web.config。</span><span class="sxs-lookup"><span data-stu-id="c77fb-153">hello deployment script will use hello appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="c77fb-154">選用的檔案 - 自訂部署</span><span class="sxs-lookup"><span data-stu-id="c77fb-154">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-django-customizing-deployment](../../includes/web-sites-python-django-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="c77fb-155">選用的檔案 - Python 執行階段</span><span class="sxs-lookup"><span data-stu-id="c77fb-155">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="c77fb-156">在伺服器上的其他檔案</span><span class="sxs-lookup"><span data-stu-id="c77fb-156">Additional files on server</span></span>
<span data-ttu-id="c77fb-157">某些檔案存在於 hello 伺服器，但不是會新增 toohello git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="c77fb-157">Some files exist on hello server but are not added toohello git repository.</span></span> <span data-ttu-id="c77fb-158">這些被建立 hello 部署指令碼。</span><span class="sxs-lookup"><span data-stu-id="c77fb-158">These are created by hello deployment script.</span></span>

    \web.config

<span data-ttu-id="c77fb-159">IIS 組態檔。</span><span class="sxs-lookup"><span data-stu-id="c77fb-159">IIS configuration file.</span></span> <span data-ttu-id="c77fb-160">從 web.x.y.config 建立於每個部署上。</span><span class="sxs-lookup"><span data-stu-id="c77fb-160">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="c77fb-161">Python 虛擬環境。</span><span class="sxs-lookup"><span data-stu-id="c77fb-161">Python virtual environment.</span></span> <span data-ttu-id="c77fb-162">如果相容的虛擬環境不存在 hello web 應用程式上，在部署期間建立。</span><span class="sxs-lookup"><span data-stu-id="c77fb-162">Created during deployment if a compatible virtual environment doesn't already exist on hello web app.</span></span> <span data-ttu-id="c77fb-163">封裝中 requirements.txt 列出 pip 安裝，但 pip 會略過安裝，如果已安裝 hello 封裝。</span><span class="sxs-lookup"><span data-stu-id="c77fb-163">Packages listed in requirements.txt are pip installed, but pip will skip installation if hello packages are already installed.</span></span>

<span data-ttu-id="c77fb-164">hello 接下來的 3 各節說明如何以 hello tooproceed web 3 不同環境下的應用程式開發：</span><span class="sxs-lookup"><span data-stu-id="c77fb-164">hello next 3 sections describe how tooproceed with hello web app development under 3 different environments:</span></span>

* <span data-ttu-id="c77fb-165">Windows，使用 Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c77fb-165">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="c77fb-166">Windows，使用命令列</span><span class="sxs-lookup"><span data-stu-id="c77fb-166">Windows, with command line</span></span>
* <span data-ttu-id="c77fb-167">Mac/Linux，使用命令列</span><span class="sxs-lookup"><span data-stu-id="c77fb-167">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="c77fb-168">Web 應用程式開發 - Windows - 適用於 Visual Studio 的 Python 工具</span><span class="sxs-lookup"><span data-stu-id="c77fb-168">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="c77fb-169">複製 hello 儲存機制</span><span class="sxs-lookup"><span data-stu-id="c77fb-169">Clone hello repository</span></span>
<span data-ttu-id="c77fb-170">首先，複製 hello 儲存機制使用 hello hello Azure 入口網站上所提供的 URL。</span><span class="sxs-lookup"><span data-stu-id="c77fb-170">First, clone hello repository using hello URL provided on hello Azure Portal.</span></span> <span data-ttu-id="c77fb-171">如需詳細資訊，請參閱[應用程式服務的本機 Git 部署 tooAzure](app-service-deploy-local-git.md)。</span><span class="sxs-lookup"><span data-stu-id="c77fb-171">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="c77fb-172">開啟包含 hello hello 儲存機制的根目錄中的 hello 方案檔 (.sln)。</span><span class="sxs-lookup"><span data-stu-id="c77fb-172">Open hello solution file (.sln) that is included in hello root of hello repository.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-solution-django.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="c77fb-173">建立虛擬環境</span><span class="sxs-lookup"><span data-stu-id="c77fb-173">Create virtual environment</span></span>
<span data-ttu-id="c77fb-174">現在我們要建立本機開發的虛擬環境。</span><span class="sxs-lookup"><span data-stu-id="c77fb-174">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="c77fb-175">以滑鼠右鍵按一下 [Python 環境]，選取 [新增虛擬環境...]。</span><span class="sxs-lookup"><span data-stu-id="c77fb-175">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="c77fb-176">請確定 hello 環境的 hello 名稱`env`。</span><span class="sxs-lookup"><span data-stu-id="c77fb-176">Make sure hello name of hello environment is `env`.</span></span>
* <span data-ttu-id="c77fb-177">選取 hello 基底直譯器。</span><span class="sxs-lookup"><span data-stu-id="c77fb-177">Select hello base interpreter.</span></span> <span data-ttu-id="c77fb-178">請確定 toouse hello 相同版本的 web 應用程式的已選取的 Python (runtime.txt 或 hello**應用程式設定**刀鋒視窗中的 hello Azure 入口網站中的 web 應用程式)。</span><span class="sxs-lookup"><span data-stu-id="c77fb-178">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>
* <span data-ttu-id="c77fb-179">請確定已核取 hello 選項 toodownload 和安裝封裝。</span><span class="sxs-lookup"><span data-stu-id="c77fb-179">Make sure hello option toodownload and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="c77fb-180">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="c77fb-180">Click **Create**.</span></span> <span data-ttu-id="c77fb-181">將建立 hello 虛擬環境中，並安裝相依項目 requirements.txt 中列出。</span><span class="sxs-lookup"><span data-stu-id="c77fb-181">This will create hello virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="create-a-superuser"></a><span data-ttu-id="c77fb-182">建立超級使用者</span><span class="sxs-lookup"><span data-stu-id="c77fb-182">Create a superuser</span></span>
<span data-ttu-id="c77fb-183">hello hello 應用程式所包含的資料庫並沒有定義任何超級使用者。</span><span class="sxs-lookup"><span data-stu-id="c77fb-183">hello database included with hello application does not have any superuser defined.</span></span> <span data-ttu-id="c77fb-184">在訂單 toouse hello 登入功能 hello 應用程式或 hello Django 管理介面中 (如果您決定 tooenable 它)，您將需要 toocreate 超級使用者。</span><span class="sxs-lookup"><span data-stu-id="c77fb-184">In order toouse hello sign-in functionality in hello application, or hello Django admin interface (if you decide tooenable it), you'll need toocreate a superuser.</span></span>

<span data-ttu-id="c77fb-185">這個 hello 從命令列從執行您的專案資料夾：</span><span class="sxs-lookup"><span data-stu-id="c77fb-185">Run this from hello command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="c77fb-186">請遵循 hello 提示 tooset hello 使用者名稱、 密碼等。</span><span class="sxs-lookup"><span data-stu-id="c77fb-186">Follow hello prompts tooset hello user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="c77fb-187">使用開發伺服器來執行</span><span class="sxs-lookup"><span data-stu-id="c77fb-187">Run using development server</span></span>
<span data-ttu-id="c77fb-188">偵錯，請按 F5 toostart 和網頁瀏覽器會開啟自動在本機執行的 toohello 頁面。</span><span class="sxs-lookup"><span data-stu-id="c77fb-188">Press F5 toostart debugging, and your web browser will open automatically toohello page running locally.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

<span data-ttu-id="c77fb-189">您可以在 hello 來源、 使用 hello 監看式視窗和其他內容中設定中斷點。請參閱 hello [Python Tools for Visual Studio 文件]如需有關 hello 各種功能。</span><span class="sxs-lookup"><span data-stu-id="c77fb-189">You can set breakpoints in hello sources, use hello watch windows, etc. See hello [Python Tools for Visual Studio Documentation] for more information on hello various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="c77fb-190">進行變更</span><span class="sxs-lookup"><span data-stu-id="c77fb-190">Make changes</span></span>
<span data-ttu-id="c77fb-191">現在您可以嘗試藉由變更 toohello 應用程式來源及/或範本。</span><span class="sxs-lookup"><span data-stu-id="c77fb-191">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="c77fb-192">測試過您的變更之後，認可這些 toohello Git 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="c77fb-192">After you've tested your changes, commit them toohello Git repository:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-commit-django.png)

### <a name="install-more-packages"></a><span data-ttu-id="c77fb-193">安裝更多封裝</span><span class="sxs-lookup"><span data-stu-id="c77fb-193">Install more packages</span></span>
<span data-ttu-id="c77fb-194">您的應用程式可能會擁有 Python 和 Django 之外的相依性。</span><span class="sxs-lookup"><span data-stu-id="c77fb-194">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="c77fb-195">您可以使用 pip 安裝其他封裝。</span><span class="sxs-lookup"><span data-stu-id="c77fb-195">You can install additional packages using pip.</span></span> <span data-ttu-id="c77fb-196">tooinstall 封裝時，以滑鼠右鍵按一下 hello 虛擬環境，並選取**安裝 Python 封裝**。</span><span class="sxs-lookup"><span data-stu-id="c77fb-196">tooinstall a package, right-click on hello virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="c77fb-197">例如，tooinstall hello Azure SDK for Python 可讓您存取 tooAzure 儲存體、 服務匯流排和其他 Azure 服務，輸入`azure`:</span><span class="sxs-lookup"><span data-stu-id="c77fb-197">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-install-package-dialog.png)

<span data-ttu-id="c77fb-198">以滑鼠右鍵按一下 hello 虛擬環境，然後選取**產生 requirements.txt** tooupdate requirements.txt。</span><span class="sxs-lookup"><span data-stu-id="c77fb-198">Right-click on hello virtual environment and select **Generate requirements.txt** tooupdate requirements.txt.</span></span>

<span data-ttu-id="c77fb-199">然後，認可 hello 變更 toorequirements.txt toohello Git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="c77fb-199">Then, commit hello changes toorequirements.txt toohello Git repository.</span></span>

### <a name="deploy-tooazure"></a><span data-ttu-id="c77fb-200">部署 tooAzure</span><span class="sxs-lookup"><span data-stu-id="c77fb-200">Deploy tooAzure</span></span>
<span data-ttu-id="c77fb-201">tootrigger 部署中，按一下 **同步**或**推送**。</span><span class="sxs-lookup"><span data-stu-id="c77fb-201">tootrigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="c77fb-202">同步處理會推送和提取。</span><span class="sxs-lookup"><span data-stu-id="c77fb-202">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-git-push.png)

<span data-ttu-id="c77fb-203">hello 第一次部署將需要一些時間，因為它會建立虛擬環境、 安裝套件和其他內容。</span><span class="sxs-lookup"><span data-stu-id="c77fb-203">hello first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="c77fb-204">Visual Studio 不會顯示 hello 部署的 hello 進度。</span><span class="sxs-lookup"><span data-stu-id="c77fb-204">Visual Studio doesn't show hello progress of hello deployment.</span></span> <span data-ttu-id="c77fb-205">如果您想要 tooreview hello 輸出，請參閱 hello 章節[疑難排解-部署](#troubleshooting-deployment)。</span><span class="sxs-lookup"><span data-stu-id="c77fb-205">If you'd like tooreview hello output, see hello section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="c77fb-206">瀏覽 toohello Azure URL tooview 您的變更。</span><span class="sxs-lookup"><span data-stu-id="c77fb-206">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="c77fb-207">Web 應用程式開發 - Windows - 命令列</span><span class="sxs-lookup"><span data-stu-id="c77fb-207">Web app development - Windows - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="c77fb-208">複製 hello 儲存機制</span><span class="sxs-lookup"><span data-stu-id="c77fb-208">Clone hello repository</span></span>
<span data-ttu-id="c77fb-209">首先，複製 hello 儲存機制使用 hello hello Azure 網站上所提供的 URL，並新增與遠端的 hello Azure 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="c77fb-209">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="c77fb-210">如需詳細資訊，請參閱[應用程式服務的本機 Git 部署 tooAzure](app-service-deploy-local-git.md)。</span><span class="sxs-lookup"><span data-stu-id="c77fb-210">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="c77fb-211">建立虛擬環境</span><span class="sxs-lookup"><span data-stu-id="c77fb-211">Create virtual environment</span></span>
<span data-ttu-id="c77fb-212">我們將建立新的虛擬環境，供開發應用程式 （不要將它 toohello 儲存機制）。</span><span class="sxs-lookup"><span data-stu-id="c77fb-212">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="c77fb-213">Python 中的虛擬環境並不是可重置，因此處理 hello 應用程式開發人員會建立自己在本機。</span><span class="sxs-lookup"><span data-stu-id="c77fb-213">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="c77fb-214">請確定 toouse hello 相同版本的 Python 選取 web 應用程式 （在 runtime.txt 或 hello 應用程式設定 刀鋒視窗的 hello Azure 入口網站中的 web 應用程式）。</span><span class="sxs-lookup"><span data-stu-id="c77fb-214">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="c77fb-215">針對 Python 2.7：</span><span class="sxs-lookup"><span data-stu-id="c77fb-215">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="c77fb-216">針對 Python 3.4：</span><span class="sxs-lookup"><span data-stu-id="c77fb-216">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="c77fb-217">安裝應用程式所需的任何外部封裝。</span><span class="sxs-lookup"><span data-stu-id="c77fb-217">Install any external packages required by your application.</span></span> <span data-ttu-id="c77fb-218">您可以在虛擬環境中，根目錄 hello hello 儲存機制 tooinstall hello 封裝使用 hello requirements.txt 檔案：</span><span class="sxs-lookup"><span data-stu-id="c77fb-218">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="c77fb-219">建立超級使用者</span><span class="sxs-lookup"><span data-stu-id="c77fb-219">Create a superuser</span></span>
<span data-ttu-id="c77fb-220">hello hello 應用程式所包含的資料庫並沒有定義任何超級使用者。</span><span class="sxs-lookup"><span data-stu-id="c77fb-220">hello database included with hello application does not have any superuser defined.</span></span> <span data-ttu-id="c77fb-221">在訂單 toouse hello 登入功能 hello 應用程式或 hello Django 管理介面中 (如果您決定 tooenable 它)，您將需要 toocreate 超級使用者。</span><span class="sxs-lookup"><span data-stu-id="c77fb-221">In order toouse hello sign-in functionality in hello application, or hello Django admin interface (if you decide tooenable it), you'll need toocreate a superuser.</span></span>

<span data-ttu-id="c77fb-222">這個 hello 從命令列從執行您的專案資料夾：</span><span class="sxs-lookup"><span data-stu-id="c77fb-222">Run this from hello command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="c77fb-223">請遵循 hello 提示 tooset hello 使用者名稱、 密碼等。</span><span class="sxs-lookup"><span data-stu-id="c77fb-223">Follow hello prompts tooset hello user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="c77fb-224">使用開發伺服器來執行</span><span class="sxs-lookup"><span data-stu-id="c77fb-224">Run using development server</span></span>
<span data-ttu-id="c77fb-225">您可以啟動 hello 應用程式開發伺服器底下，以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="c77fb-225">You can launch hello application under a development server with hello following command:</span></span>

    env\scripts\python manage.py runserver

<span data-ttu-id="c77fb-226">hello 主控台就會顯示 hello URL，而且會接聽通訊埠 hello 伺服器：</span><span class="sxs-lookup"><span data-stu-id="c77fb-226">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-run-local-django.png)

<span data-ttu-id="c77fb-227">然後，開啟您的 web 瀏覽器 toothat URL。</span><span class="sxs-lookup"><span data-stu-id="c77fb-227">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="c77fb-228">進行變更</span><span class="sxs-lookup"><span data-stu-id="c77fb-228">Make changes</span></span>
<span data-ttu-id="c77fb-229">現在您可以嘗試藉由變更 toohello 應用程式來源及/或範本。</span><span class="sxs-lookup"><span data-stu-id="c77fb-229">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="c77fb-230">測試過您的變更之後，認可這些 toohello Git 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="c77fb-230">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="c77fb-231">安裝更多封裝</span><span class="sxs-lookup"><span data-stu-id="c77fb-231">Install more packages</span></span>
<span data-ttu-id="c77fb-232">您的應用程式可能會擁有 Python 和 Django 之外的相依性。</span><span class="sxs-lookup"><span data-stu-id="c77fb-232">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="c77fb-233">您可以使用 pip 安裝其他封裝。</span><span class="sxs-lookup"><span data-stu-id="c77fb-233">You can install additional packages using pip.</span></span> <span data-ttu-id="c77fb-234">例如，tooinstall hello Azure SDK for Python 可讓您存取 tooAzure 儲存體、 服務匯流排和其他 Azure 服務類型：</span><span class="sxs-lookup"><span data-stu-id="c77fb-234">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="c77fb-235">請確定 tooupdate requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="c77fb-235">Make sure tooupdate requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="c77fb-236">認可 hello 變更：</span><span class="sxs-lookup"><span data-stu-id="c77fb-236">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="c77fb-237">部署 tooAzure</span><span class="sxs-lookup"><span data-stu-id="c77fb-237">Deploy tooAzure</span></span>
<span data-ttu-id="c77fb-238">tootrigger 部署，推入 hello 變更 tooAzure:</span><span class="sxs-lookup"><span data-stu-id="c77fb-238">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="c77fb-239">您會看到 hello 輸出 hello 部署指令碼，包括建立虛擬環境安裝封裝，建立 web.config。</span><span class="sxs-lookup"><span data-stu-id="c77fb-239">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="c77fb-240">瀏覽 toohello Azure URL tooview 您的變更。</span><span class="sxs-lookup"><span data-stu-id="c77fb-240">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="c77fb-241">Web 應用程式開發 - Mac/Linux - 命令列</span><span class="sxs-lookup"><span data-stu-id="c77fb-241">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="c77fb-242">複製 hello 儲存機制</span><span class="sxs-lookup"><span data-stu-id="c77fb-242">Clone hello repository</span></span>
<span data-ttu-id="c77fb-243">首先，複製 hello 儲存機制使用 hello hello Azure 網站上所提供的 URL，並新增與遠端的 hello Azure 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="c77fb-243">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="c77fb-244">如需詳細資訊，請參閱[應用程式服務的本機 Git 部署 tooAzure](app-service-deploy-local-git.md)。</span><span class="sxs-lookup"><span data-stu-id="c77fb-244">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="c77fb-245">建立虛擬環境</span><span class="sxs-lookup"><span data-stu-id="c77fb-245">Create virtual environment</span></span>
<span data-ttu-id="c77fb-246">我們將建立新的虛擬環境，供開發應用程式 （不要將它 toohello 儲存機制）。</span><span class="sxs-lookup"><span data-stu-id="c77fb-246">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="c77fb-247">Python 中的虛擬環境並不是可重置，因此處理 hello 應用程式開發人員會建立自己在本機。</span><span class="sxs-lookup"><span data-stu-id="c77fb-247">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="c77fb-248">請確定 toouse hello 相同版本的 Python 選取 web 應用程式 （在 runtime.txt 或 hello 應用程式設定 刀鋒視窗的 hello Azure 入口網站中的 web 應用程式）。</span><span class="sxs-lookup"><span data-stu-id="c77fb-248">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="c77fb-249">針對 Python 2.7：</span><span class="sxs-lookup"><span data-stu-id="c77fb-249">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="c77fb-250">針對 Python 3.4：</span><span class="sxs-lookup"><span data-stu-id="c77fb-250">For Python 3.4:</span></span>

    python -m venv env

<span data-ttu-id="c77fb-251">或</span><span class="sxs-lookup"><span data-stu-id="c77fb-251">or</span></span>

    pyvenv env

<span data-ttu-id="c77fb-252">安裝應用程式所需的任何外部封裝。</span><span class="sxs-lookup"><span data-stu-id="c77fb-252">Install any external packages required by your application.</span></span> <span data-ttu-id="c77fb-253">您可以在虛擬環境中，根目錄 hello hello 儲存機制 tooinstall hello 封裝使用 hello requirements.txt 檔案：</span><span class="sxs-lookup"><span data-stu-id="c77fb-253">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="c77fb-254">建立超級使用者</span><span class="sxs-lookup"><span data-stu-id="c77fb-254">Create a superuser</span></span>
<span data-ttu-id="c77fb-255">hello hello 應用程式所包含的資料庫並沒有定義任何超級使用者。</span><span class="sxs-lookup"><span data-stu-id="c77fb-255">hello database included with hello application does not have any superuser defined.</span></span> <span data-ttu-id="c77fb-256">在訂單 toouse hello 登入功能 hello 應用程式或 hello Django 管理介面中 (如果您決定 tooenable 它)，您將需要 toocreate 超級使用者。</span><span class="sxs-lookup"><span data-stu-id="c77fb-256">In order toouse hello sign-in functionality in hello application, or hello Django admin interface (if you decide tooenable it), you'll need toocreate a superuser.</span></span>

<span data-ttu-id="c77fb-257">這個 hello 從命令列從執行您的專案資料夾：</span><span class="sxs-lookup"><span data-stu-id="c77fb-257">Run this from hello command-line from your project folder:</span></span>

    env/bin/python manage.py createsuperuser

<span data-ttu-id="c77fb-258">請遵循 hello 提示 tooset hello 使用者名稱、 密碼等。</span><span class="sxs-lookup"><span data-stu-id="c77fb-258">Follow hello prompts tooset hello user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="c77fb-259">使用開發伺服器來執行</span><span class="sxs-lookup"><span data-stu-id="c77fb-259">Run using development server</span></span>
<span data-ttu-id="c77fb-260">您可以啟動 hello 應用程式開發伺服器底下，以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="c77fb-260">You can launch hello application under a development server with hello following command:</span></span>

    env/bin/python manage.py runserver

<span data-ttu-id="c77fb-261">hello 主控台就會顯示 hello URL，而且會接聽通訊埠 hello 伺服器：</span><span class="sxs-lookup"><span data-stu-id="c77fb-261">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-run-local-django.png)

<span data-ttu-id="c77fb-262">然後，開啟您的 web 瀏覽器 toothat URL。</span><span class="sxs-lookup"><span data-stu-id="c77fb-262">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="c77fb-263">進行變更</span><span class="sxs-lookup"><span data-stu-id="c77fb-263">Make changes</span></span>
<span data-ttu-id="c77fb-264">現在您可以嘗試藉由變更 toohello 應用程式來源及/或範本。</span><span class="sxs-lookup"><span data-stu-id="c77fb-264">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="c77fb-265">測試過您的變更之後，認可這些 toohello Git 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="c77fb-265">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="c77fb-266">安裝更多封裝</span><span class="sxs-lookup"><span data-stu-id="c77fb-266">Install more packages</span></span>
<span data-ttu-id="c77fb-267">您的應用程式可能會擁有 Python 和 Django 之外的相依性。</span><span class="sxs-lookup"><span data-stu-id="c77fb-267">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="c77fb-268">您可以使用 pip 安裝其他封裝。</span><span class="sxs-lookup"><span data-stu-id="c77fb-268">You can install additional packages using pip.</span></span> <span data-ttu-id="c77fb-269">例如，tooinstall hello Azure SDK for Python 可讓您存取 tooAzure 儲存體、 服務匯流排和其他 Azure 服務類型：</span><span class="sxs-lookup"><span data-stu-id="c77fb-269">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="c77fb-270">請確定 tooupdate requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="c77fb-270">Make sure tooupdate requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="c77fb-271">認可 hello 變更：</span><span class="sxs-lookup"><span data-stu-id="c77fb-271">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="c77fb-272">部署 tooAzure</span><span class="sxs-lookup"><span data-stu-id="c77fb-272">Deploy tooAzure</span></span>
<span data-ttu-id="c77fb-273">tootrigger 部署，推入 hello 變更 tooAzure:</span><span class="sxs-lookup"><span data-stu-id="c77fb-273">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="c77fb-274">您會看到 hello 輸出 hello 部署指令碼，包括建立虛擬環境安裝封裝，建立 web.config。</span><span class="sxs-lookup"><span data-stu-id="c77fb-274">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="c77fb-275">瀏覽 toohello Azure URL tooview 您的變更。</span><span class="sxs-lookup"><span data-stu-id="c77fb-275">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="c77fb-276">疑難排解 - 封裝安裝</span><span class="sxs-lookup"><span data-stu-id="c77fb-276">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="c77fb-277">疑難排解 - 虛擬環境</span><span class="sxs-lookup"><span data-stu-id="c77fb-277">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="troubleshooting---static-files"></a><span data-ttu-id="c77fb-278">疑難排解 - 靜態檔案</span><span class="sxs-lookup"><span data-stu-id="c77fb-278">Troubleshooting - Static Files</span></span>
<span data-ttu-id="c77fb-279">Django 並收集靜態檔案的 hello 概念。</span><span class="sxs-lookup"><span data-stu-id="c77fb-279">Django has hello concept of collecting static files.</span></span> <span data-ttu-id="c77fb-280">這會從其原始位置中取得所有 hello 靜態檔案，並將其複製 tooa 單一資料夾。</span><span class="sxs-lookup"><span data-stu-id="c77fb-280">This takes all hello static files from their original location and copies them tooa single folder.</span></span> <span data-ttu-id="c77fb-281">此應用程式，將它們複製太`/static`。</span><span class="sxs-lookup"><span data-stu-id="c77fb-281">For this application, they are copied too`/static`.</span></span>

<span data-ttu-id="c77fb-282">這是因為靜態檔案可能來自不同的 Django「應用程式」。</span><span class="sxs-lookup"><span data-stu-id="c77fb-282">This is done because static files may come from different Django 'apps'.</span></span> <span data-ttu-id="c77fb-283">比方說，hello Django 管理介面中的 hello 靜態檔案位於 hello 虛擬環境中如 Django 程式庫的子資料夾中。</span><span class="sxs-lookup"><span data-stu-id="c77fb-283">For example, hello static files from hello Django admin interfaces are located in a Django library subfolder in hello virtual environment.</span></span> <span data-ttu-id="c77fb-284">此應用程式所定義的靜態檔案位於 `/app/static`。</span><span class="sxs-lookup"><span data-stu-id="c77fb-284">Static files defined by this application are located in `/app/static`.</span></span> <span data-ttu-id="c77fb-285">當您使用多個 Django「應用程式」時 ，您必須擁有位於多個位置中的靜態檔案。</span><span class="sxs-lookup"><span data-stu-id="c77fb-285">As you use more Django 'apps', you'll have static files located in multiple places.</span></span>

<span data-ttu-id="c77fb-286">當偵錯模式執行 hello 應用程式，hello 應用程式服務的 hello 靜態檔案從其原始位置。</span><span class="sxs-lookup"><span data-stu-id="c77fb-286">When running hello application in debug mode, hello application serves hello static files from their original location.</span></span>

<span data-ttu-id="c77fb-287">在發行模式中執行 hello 應用程式，hello 應用程式會執行**不**做 hello 靜態檔案。</span><span class="sxs-lookup"><span data-stu-id="c77fb-287">When running hello application in release mode, hello application does **not** serve hello static files.</span></span> <span data-ttu-id="c77fb-288">負責 hello hello web 伺服器 tooserve hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="c77fb-288">It is hello responsibility of hello web server tooserve hello files.</span></span> <span data-ttu-id="c77fb-289">此應用程式中，IIS 會提供 hello 靜態檔`/static`。</span><span class="sxs-lookup"><span data-stu-id="c77fb-289">For this application, IIS will serve hello static files from `/static`.</span></span>

<span data-ttu-id="c77fb-290">hello 靜態檔案的集合做為組件的 hello 部署指令碼中，清除先前收集的檔案會自動完成的。</span><span class="sxs-lookup"><span data-stu-id="c77fb-290">hello collection of static files is done automatically as part of hello deployment script, clearing previously collected files.</span></span> <span data-ttu-id="c77fb-291">這表示 hello 回收會針對每個部署，一個位元速度減緩部署，但是它確保過時的檔案，將無法使用，避免潛在的安全性問題。</span><span class="sxs-lookup"><span data-stu-id="c77fb-291">This means hello collection occurs on every deployment, slowing down deployment a bit, but it ensures that obsolete files won't be available, avoiding a potential security issue.</span></span>

<span data-ttu-id="c77fb-292">如果您想 tooskip 靜態檔案的集合，如 Django 應用程式：</span><span class="sxs-lookup"><span data-stu-id="c77fb-292">If you want tooskip collection of static files for your Django application:</span></span>

    \.skipDjango

<span data-ttu-id="c77fb-293">然後您將在本機電腦上手動需要 toodo hello 集合：</span><span class="sxs-lookup"><span data-stu-id="c77fb-293">Then you'll need toodo hello collection manually on your local machine:</span></span>

    env\scripts\python manage.py collectstatic

<span data-ttu-id="c77fb-294">然後移除 hello`\static`資料夾從`.gitignore`並將它加入 toohello Git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="c77fb-294">Then remove hello `\static` folder from `.gitignore` and add it toohello Git repository.</span></span>

## <a name="troubleshooting---settings"></a><span data-ttu-id="c77fb-295">疑難排解 - 設定</span><span class="sxs-lookup"><span data-stu-id="c77fb-295">Troubleshooting - Settings</span></span>
<span data-ttu-id="c77fb-296">Hello 應用程式的各種設定可以變更在`DjangoWebProject/settings.py`。</span><span class="sxs-lookup"><span data-stu-id="c77fb-296">Various settings for hello application can be changed in `DjangoWebProject/settings.py`.</span></span>

<span data-ttu-id="c77fb-297">為了開發人員方便起見，已啟用偵錯模式。</span><span class="sxs-lookup"><span data-stu-id="c77fb-297">For developer convenience, debug mode is enabled.</span></span> <span data-ttu-id="c77fb-298">一個好所造成的副作用，是您在本機執行，而不需要 toocollect 靜態檔案時將會無法 toosee 映像，而且其他靜態內容。</span><span class="sxs-lookup"><span data-stu-id="c77fb-298">One nice side effect of that is you'll be able toosee images and other static content when running locally, without having toocollect static files.</span></span>

<span data-ttu-id="c77fb-299">toodisable 偵錯模式：</span><span class="sxs-lookup"><span data-stu-id="c77fb-299">toodisable debug mode:</span></span>

    DEBUG = False

<span data-ttu-id="c77fb-300">停用偵錯時，hello 值`ALLOWED_HOSTS`需求 toobe 更新 tooinclude hello Azure 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="c77fb-300">When debug is disabled, hello value for `ALLOWED_HOSTS` needs toobe updated tooinclude hello Azure host name.</span></span> <span data-ttu-id="c77fb-301">例如：</span><span class="sxs-lookup"><span data-stu-id="c77fb-301">For example:</span></span>

    ALLOWED_HOSTS = (
        'pythonapp.azurewebsites.net',
    )

<span data-ttu-id="c77fb-302">或 tooenable 任何：</span><span class="sxs-lookup"><span data-stu-id="c77fb-302">or tooenable any:</span></span>

    ALLOWED_HOSTS = (
        '*',
    )

<span data-ttu-id="c77fb-303">在實務上，您可能想 toodo 更複雜的 toodeal 之間切換偵錯與發行模式中，並取得 hello 主機名稱的項目。</span><span class="sxs-lookup"><span data-stu-id="c77fb-303">In practice, you may want toodo something more complex toodeal with switching between debug and release mode, and getting hello host name.</span></span>

<span data-ttu-id="c77fb-304">您可以設定環境變數，透過 Azure 入口網站 hello**設定** 頁面的 hello**應用程式設定**> 一節。</span><span class="sxs-lookup"><span data-stu-id="c77fb-304">You can set environment variables through hello Azure portal **CONFIGURE** page, in hello **app settings** section.</span></span>  <span data-ttu-id="c77fb-305">這可用於設定值，您可能不想 tooappear hello 來源 （連接字串、 密碼等），或您想 tooset Azure 與您的本機電腦之間的不同。</span><span class="sxs-lookup"><span data-stu-id="c77fb-305">This can be useful for setting values that you may not want tooappear in hello sources (connection strings, passwords, etc), or that you want tooset differently between Azure and your local machine.</span></span> <span data-ttu-id="c77fb-306">在`settings.py`，您可以查詢 hello 環境變數使用`os.getenv`。</span><span class="sxs-lookup"><span data-stu-id="c77fb-306">In `settings.py`, you can query hello environment variables using `os.getenv`.</span></span>

## <a name="using-a-database"></a><span data-ttu-id="c77fb-307">使用資料庫</span><span class="sxs-lookup"><span data-stu-id="c77fb-307">Using a Database</span></span>
<span data-ttu-id="c77fb-308">sqlite 資料庫 hello 資料庫所包含的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c77fb-308">hello database that is included with hello application is a sqlite database.</span></span> <span data-ttu-id="c77fb-309">這是方便且實用的預設資料庫 toouse 進行開發，因為它不需要的幾乎任何設定。</span><span class="sxs-lookup"><span data-stu-id="c77fb-309">This is a convenient and useful default database toouse for development, as it requires almost no setup.</span></span> <span data-ttu-id="c77fb-310">hello 資料庫會儲存在 hello 專案資料夾中的 hello db.sqlite3 檔案。</span><span class="sxs-lookup"><span data-stu-id="c77fb-310">hello database is stored in hello db.sqlite3 file in hello project folder.</span></span>

<span data-ttu-id="c77fb-311">Azure 會提供資料庫服務，而這是簡單 toouse 從 Django 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c77fb-311">Azure provides database services which are easy toouse from a Django application.</span></span> <span data-ttu-id="c77fb-312">教學課程使用[SQL Database]和[MySQL]從 Django 應用程式顯示 hello 步驟需要 toocreate hello 資料庫服務，變更中的 hello 資料庫設定`DjangoWebProject/settings.py`，和 hello程式庫需要 tooinstall。</span><span class="sxs-lookup"><span data-stu-id="c77fb-312">Tutorials for using [SQL Database] and [MySQL] from a Django application show hello steps necessary toocreate hello database service, change hello database settings in `DjangoWebProject/settings.py`, and hello libraries required tooinstall.</span></span>

<span data-ttu-id="c77fb-313">當然，如果您偏好 toomanage 您自己的資料庫伺服器，您可以使用在 Azure 上執行的 Windows 或 Linux 的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="c77fb-313">Of course, if you prefer toomanage your own database servers, you can do so using Windows or Linux virtual machines running on Azure.</span></span>

## <a name="django-admin-interface"></a><span data-ttu-id="c77fb-314">Django 管理介面</span><span class="sxs-lookup"><span data-stu-id="c77fb-314">Django Admin Interface</span></span>
<span data-ttu-id="c77fb-315">一旦您開始建置您的模型，您會想 toopopulate hello 資料庫，某些資料。</span><span class="sxs-lookup"><span data-stu-id="c77fb-315">Once you start building your models, you'll want toopopulate hello database with some data.</span></span> <span data-ttu-id="c77fb-316">Toodo 加入，以互動方式編輯內容的簡單方法是 toouse hello Django 管理介面。</span><span class="sxs-lookup"><span data-stu-id="c77fb-316">An easy way toodo add and edit content interactively is toouse hello Django administration interface.</span></span>

<span data-ttu-id="c77fb-317">hello hello 管理介面的程式碼會標記為註解中 hello 應用程式的來源，但明確標示讓您輕鬆地啟用它 （搜尋 'admin'）。</span><span class="sxs-lookup"><span data-stu-id="c77fb-317">hello code for hello admin interface is commented out in hello application sources, but it's clearly marked so you can easily enable it (search for 'admin').</span></span>

<span data-ttu-id="c77fb-318">啟用之後，同步處理 hello 資料庫、 執行 hello 應用程式並瀏覽過`/admin`。</span><span class="sxs-lookup"><span data-stu-id="c77fb-318">After it's enabled, synchronize hello database, run hello application and navigate too`/admin`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c77fb-319">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c77fb-319">Next Steps</span></span>
<span data-ttu-id="c77fb-320">請遵循這些連結 toolearn 更多關於如 Django 和 Python Tools for Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="c77fb-320">Follow these links toolearn more about Django and Python Tools for Visual Studio:</span></span>

* <span data-ttu-id="c77fb-321">[Django 說明文件]</span><span class="sxs-lookup"><span data-stu-id="c77fb-321">[Django Documentation]</span></span>
* <span data-ttu-id="c77fb-322">[Python Tools for Visual Studio 文件]</span><span class="sxs-lookup"><span data-stu-id="c77fb-322">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="c77fb-323">如需使用 SQL Database 和 MySQL 的資訊：</span><span class="sxs-lookup"><span data-stu-id="c77fb-323">For information on using SQL Database and MySQL:</span></span>

* <span data-ttu-id="c77fb-324">[Azure 上使用 Python Tools for Visual Studio 的 Django 和 MySQL]</span><span class="sxs-lookup"><span data-stu-id="c77fb-324">[Django and MySQL on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="c77fb-325">[Azure 上使用 Python Tools for Visual Studio 的 Django 和 SQL Database]</span><span class="sxs-lookup"><span data-stu-id="c77fb-325">[Django and SQL Database on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="c77fb-326">如需詳細資訊，請參閱 hello [Python 開發人員中心](/develop/python/)。</span><span class="sxs-lookup"><span data-stu-id="c77fb-326">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="c77fb-327">變更的項目</span><span class="sxs-lookup"><span data-stu-id="c77fb-327">What's changed</span></span>
* <span data-ttu-id="c77fb-328">從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="c77fb-328">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

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
