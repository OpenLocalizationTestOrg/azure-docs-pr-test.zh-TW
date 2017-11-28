---
title: "在 Azure 中的酒瓶 aaaCreating web 應用程式"
description: "此教學課程為您介紹 toorunning Python web 應用程式在 Azure 上。"
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: b7f4ca3a-0b52-4108-90a7-f7e07ac73da0
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/20/2016
ms.author: huvalo
ms.openlocfilehash: 3362047b3106b4380b5971e47cbd8042d38a792b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-flask-in-azure"></a><span data-ttu-id="000e4-103">在 Azure 中使用 Flask 建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="000e4-103">Creating web apps with Flask in Azure</span></span>
<span data-ttu-id="000e4-104">這個教學課程描述如何 tooget 啟動中執行 Python [Azure App Service Web 應用程式](http://go.microsoft.com/fwlink/?LinkId=529714)。</span><span class="sxs-lookup"><span data-stu-id="000e4-104">This tutorial describes how tooget started running Python in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>  <span data-ttu-id="000e4-105">Web Apps 提供有限的免費裝載和快速部署，而您可以使用 Python！</span><span class="sxs-lookup"><span data-stu-id="000e4-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span>  <span data-ttu-id="000e4-106">當您的應用程式成長，您可以切換 toopaid 裝載，您也可以與所有的整合 hello 其他 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="000e4-106">As your app grows, you can switch toopaid hosting, and you can also integrate with all of hello other Azure services.</span></span>

<span data-ttu-id="000e4-107">您將建立使用 hello 酒瓶 web 架構的應用程式 (請參閱本教學課程中的替代版本[Django](web-sites-python-create-deploy-django-app.md)和[Bottle](web-sites-python-create-deploy-bottle-app.md))。</span><span class="sxs-lookup"><span data-stu-id="000e4-107">You will create an application using hello Flask web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span>  <span data-ttu-id="000e4-108">您將會從 hello Azure 組件庫中建立 hello 網站、 設定 Git 部署和複製本機 hello 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="000e4-108">You will create hello website from hello Azure gallery, set up Git deployment, and clone hello repository locally.</span></span>  <span data-ttu-id="000e4-109">然後，您會在本機執行 hello 應用程式、 進行變更、 認可並推送它們 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="000e4-109">Then you will run hello application locally, make changes, commit and push them tooAzure.</span></span>  <span data-ttu-id="000e4-110">hello 教學課程顯示如何 toodo 於 Windows 或 Mac/Linux。</span><span class="sxs-lookup"><span data-stu-id="000e4-110">hello tutorial shows how toodo this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="000e4-111">如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="000e4-111">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="000e4-112">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="000e4-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="000e4-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="000e4-113">Prerequisites</span></span>
* <span data-ttu-id="000e4-114">Windows、Mac 或 Linux</span><span class="sxs-lookup"><span data-stu-id="000e4-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="000e4-115">Python 2.7 或 3.4</span><span class="sxs-lookup"><span data-stu-id="000e4-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="000e4-116">setuptools、pip、virtualenv (僅 Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="000e4-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="000e4-117">Git</span><span class="sxs-lookup"><span data-stu-id="000e4-117">Git</span></span>
* <span data-ttu-id="000e4-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - 注意：這是選擇性的</span><span class="sxs-lookup"><span data-stu-id="000e4-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="000e4-119">**注意**：Python 專案目前不支援 TFS 發佈。</span><span class="sxs-lookup"><span data-stu-id="000e4-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="000e4-120">Windows</span><span class="sxs-lookup"><span data-stu-id="000e4-120">Windows</span></span>
<span data-ttu-id="000e4-121">如果您還沒有安裝 Python 2.7 或 3.4 (32 位元)，建議您使用 Web Platform Installer 安裝 [Azure SDK for Python 2.7] 或 [Azure SDK for Python 3.4]。</span><span class="sxs-lookup"><span data-stu-id="000e4-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span>  <span data-ttu-id="000e4-122">這會安裝 hello 32 位元版本的 Python、 setuptools、 pip、 virtualenv 等 （32 位元 Python 是 hello Azure 主機機器上安裝的內容）。</span><span class="sxs-lookup"><span data-stu-id="000e4-122">This installs hello 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on hello Azure host machines).</span></span>  <span data-ttu-id="000e4-123">或者，您可以從 [python.org]取得 Python。</span><span class="sxs-lookup"><span data-stu-id="000e4-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="000e4-124">針對 Git，建議您安裝 [Git for Windows] 或 [GitHub for Windows]。</span><span class="sxs-lookup"><span data-stu-id="000e4-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span>  <span data-ttu-id="000e4-125">如果您使用 Visual Studio，您可以使用整合的 hello Git 支援。</span><span class="sxs-lookup"><span data-stu-id="000e4-125">If you use Visual Studio, you can use hello integrated Git support.</span></span>

<span data-ttu-id="000e4-126">我們也建議您安裝 [Python Tools 2.2 for Visual Studio]。</span><span class="sxs-lookup"><span data-stu-id="000e4-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span>  <span data-ttu-id="000e4-127">這是選擇性的但如果您有[Visual Studio]，包括 hello 釋放 Visual Studio Community 2013 或 Visual Studio Express 2013 for Web，則這會提供絕佳的 Python IDE。</span><span class="sxs-lookup"><span data-stu-id="000e4-127">This is optional, but if you have [Visual Studio], including hello free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="000e4-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="000e4-128">Mac/Linux</span></span>
<span data-ttu-id="000e4-129">您應該已經安裝 Python 與 Git，但請確定您擁有的是 Python 2.7 或 3.4。</span><span class="sxs-lookup"><span data-stu-id="000e4-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-create-on-hello-azure-portal"></a><span data-ttu-id="000e4-130">在 hello Azure 入口網站上建立 web 應用程式</span><span class="sxs-lookup"><span data-stu-id="000e4-130">Web app create on hello Azure Portal</span></span>
<span data-ttu-id="000e4-131">hello 第一個步驟中建立您的應用程式是 toocreate hello web 應用程式，透過 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="000e4-131">hello first step in creating your app is toocreate hello web app via hello [Azure Portal](https://portal.azure.com).</span></span> 

1. <span data-ttu-id="000e4-132">登入 hello Azure 入口網站並按一下 hello**新增**hello 左下角中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="000e4-132">Log into hello Azure Portal and click hello **NEW** button in hello bottom left corner.</span></span> 
2. <span data-ttu-id="000e4-133">按一下 [Web + 行動] 。</span><span class="sxs-lookup"><span data-stu-id="000e4-133">Click **Web + Mobile**.</span></span>
3. <span data-ttu-id="000e4-134">在 hello 搜尋方塊中輸入"python"。</span><span class="sxs-lookup"><span data-stu-id="000e4-134">In hello search box, type "python".</span></span>
4. <span data-ttu-id="000e4-135">在 hello 搜尋結果中，選取 **酒瓶**，然後按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="000e4-135">In hello search results, select **Flask**, then click **Create**.</span></span>
5. <span data-ttu-id="000e4-136">設定 hello 新酒瓶應用程式，例如為它建立新的應用程式服務方案和新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="000e4-136">Configure hello new Flask app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="000e4-137">然後按一下 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="000e4-137">Then, click **Create**.</span></span>
6. <span data-ttu-id="000e4-138">設定 Git 發行功能，新建立的 web 應用程式在 hello 指示[應用程式服務的本機 Git 部署 tooAzure](app-service-deploy-local-git.md)。</span><span class="sxs-lookup"><span data-stu-id="000e4-138">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="000e4-139">應用程式概觀</span><span class="sxs-lookup"><span data-stu-id="000e4-139">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="000e4-140">Git 儲存機制內容</span><span class="sxs-lookup"><span data-stu-id="000e4-140">Git repository contents</span></span>
<span data-ttu-id="000e4-141">以下是您會發現在 hello 初始 Git 儲存機制，我們將複製 hello 下一節中的 hello 檔案的概觀。</span><span class="sxs-lookup"><span data-stu-id="000e4-141">Here's an overview of hello files you'll find in hello initial Git repository, which we'll clone in hello next section.</span></span>

    \FlaskWebProject\__init__.py
    \FlaskWebProject\views.py
    \FlaskWebProject\static\content\
    \FlaskWebProject\static\fonts\
    \FlaskWebProject\static\scripts\
    \FlaskWebProject\templates\about.html
    \FlaskWebProject\templates\contact.html
    \FlaskWebProject\templates\index.html
    \FlaskWebProject\templates\layout.html

<span data-ttu-id="000e4-142">Hello 應用程式的主要來源。</span><span class="sxs-lookup"><span data-stu-id="000e4-142">Main sources for hello application.</span></span>  <span data-ttu-id="000e4-143">包含 3 個主要的版面配置頁面 (index、about、contact)。</span><span class="sxs-lookup"><span data-stu-id="000e4-143">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="000e4-144">靜態內容和指令碼，包含啟動程序、jquery、modernizr 和回應。</span><span class="sxs-lookup"><span data-stu-id="000e4-144">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \runserver.py

<span data-ttu-id="000e4-145">本機開發伺服器支援。</span><span class="sxs-lookup"><span data-stu-id="000e4-145">Local development server support.</span></span> <span data-ttu-id="000e4-146">在本機上使用此 toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="000e4-146">Use this toorun hello application locally.</span></span>

    \FlaskWebProject.pyproj
    \FlaskWebProject.sln

<span data-ttu-id="000e4-147">搭配 [Python Tools for Visual Studio]使用的專案檔。</span><span class="sxs-lookup"><span data-stu-id="000e4-147">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="000e4-148">虛擬環境和 PTVS 遠端偵錯支援的 IIS Proxy。</span><span class="sxs-lookup"><span data-stu-id="000e4-148">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="000e4-149">此應用程式所需的外部封裝。</span><span class="sxs-lookup"><span data-stu-id="000e4-149">External packages needed by this application.</span></span> <span data-ttu-id="000e4-150">hello 部署指令碼將 pip 安裝 hello 封裝這個檔案中列出。</span><span class="sxs-lookup"><span data-stu-id="000e4-150">hello deployment script will pip install hello packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="000e4-151">IIS 組態檔。</span><span class="sxs-lookup"><span data-stu-id="000e4-151">IIS configuration files.</span></span>  <span data-ttu-id="000e4-152">將使用 hello 適當 web.x.y.config hello 部署指令碼，並將它複製為 web.config。</span><span class="sxs-lookup"><span data-stu-id="000e4-152">hello deployment script will use hello appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="000e4-153">選用的檔案 - 自訂部署</span><span class="sxs-lookup"><span data-stu-id="000e4-153">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="000e4-154">選用的檔案 - Python 執行階段</span><span class="sxs-lookup"><span data-stu-id="000e4-154">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="000e4-155">在伺服器上的其他檔案</span><span class="sxs-lookup"><span data-stu-id="000e4-155">Additional files on server</span></span>
<span data-ttu-id="000e4-156">某些檔案存在於 hello 伺服器，但不是會新增 toohello git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="000e4-156">Some files exist on hello server but are not added toohello git repository.</span></span>  <span data-ttu-id="000e4-157">這些被建立 hello 部署指令碼。</span><span class="sxs-lookup"><span data-stu-id="000e4-157">These are created by hello deployment script.</span></span>

    \web.config

<span data-ttu-id="000e4-158">IIS 組態檔。</span><span class="sxs-lookup"><span data-stu-id="000e4-158">IIS configuration file.</span></span>  <span data-ttu-id="000e4-159">從 web.x.y.config 建立於每個部署上。</span><span class="sxs-lookup"><span data-stu-id="000e4-159">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="000e4-160">Python 虛擬環境。</span><span class="sxs-lookup"><span data-stu-id="000e4-160">Python virtual environment.</span></span>  <span data-ttu-id="000e4-161">如果相容的虛擬環境不存在 hello 應用程式上，在部署期間建立。</span><span class="sxs-lookup"><span data-stu-id="000e4-161">Created during deployment if a compatible virtual environment doesn't already exist on hello app.</span></span>  <span data-ttu-id="000e4-162">封裝中 requirements.txt 列出 pip 安裝，但 pip 會略過安裝，如果已安裝 hello 封裝。</span><span class="sxs-lookup"><span data-stu-id="000e4-162">Packages listed in requirements.txt are pip installed, but pip will skip installation if hello packages are already installed.</span></span>

<span data-ttu-id="000e4-163">hello 接下來的 3 各節說明如何以 hello tooproceed web 3 不同環境下的應用程式開發：</span><span class="sxs-lookup"><span data-stu-id="000e4-163">hello next 3 sections describe how tooproceed with hello web app development under 3 different environments:</span></span>

* <span data-ttu-id="000e4-164">Windows，使用 Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="000e4-164">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="000e4-165">Windows，使用命令列</span><span class="sxs-lookup"><span data-stu-id="000e4-165">Windows, with command line</span></span>
* <span data-ttu-id="000e4-166">Mac/Linux，使用命令列</span><span class="sxs-lookup"><span data-stu-id="000e4-166">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="000e4-167">Web 應用程式開發 - Windows - 適用於 Visual Studio 的 Python 工具</span><span class="sxs-lookup"><span data-stu-id="000e4-167">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="000e4-168">複製 hello 儲存機制</span><span class="sxs-lookup"><span data-stu-id="000e4-168">Clone hello repository</span></span>
<span data-ttu-id="000e4-169">首先，複製 hello 儲存機制使用 hello hello Azure 入口網站上所提供的 URL。</span><span class="sxs-lookup"><span data-stu-id="000e4-169">First, clone hello repository using hello URL provided on hello Azure Portal.</span></span> <span data-ttu-id="000e4-170">如需詳細資訊，請參閱[應用程式服務的本機 Git 部署 tooAzure](app-service-deploy-local-git.md)。</span><span class="sxs-lookup"><span data-stu-id="000e4-170">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="000e4-171">開啟包含 hello hello 儲存機制的根目錄中的 hello 方案檔 (.sln)。</span><span class="sxs-lookup"><span data-stu-id="000e4-171">Open hello solution file (.sln) that is included in hello root of hello repository.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-solution-flask.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="000e4-172">建立虛擬環境</span><span class="sxs-lookup"><span data-stu-id="000e4-172">Create virtual environment</span></span>
<span data-ttu-id="000e4-173">現在我們要建立本機開發的虛擬環境。</span><span class="sxs-lookup"><span data-stu-id="000e4-173">Now we'll create a virtual environment for local development.</span></span>  <span data-ttu-id="000e4-174">以滑鼠右鍵按一下 [Python 環境]，選取 [新增虛擬環境...]。</span><span class="sxs-lookup"><span data-stu-id="000e4-174">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="000e4-175">請確定 hello 環境的 hello 名稱`env`。</span><span class="sxs-lookup"><span data-stu-id="000e4-175">Make sure hello name of hello environment is `env`.</span></span>
* <span data-ttu-id="000e4-176">選取 hello 基底直譯器。</span><span class="sxs-lookup"><span data-stu-id="000e4-176">Select hello base interpreter.</span></span>  <span data-ttu-id="000e4-177">請確定 toouse hello 相同版本的 web 應用程式的已選取的 Python (runtime.txt 或 hello**應用程式設定**刀鋒視窗中的 hello Azure 入口網站中的 web 應用程式)。</span><span class="sxs-lookup"><span data-stu-id="000e4-177">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>
* <span data-ttu-id="000e4-178">請確定已核取 hello 選項 toodownload 和安裝封裝。</span><span class="sxs-lookup"><span data-stu-id="000e4-178">Make sure hello option toodownload and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="000e4-179">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="000e4-179">Click **Create**.</span></span>  <span data-ttu-id="000e4-180">將建立 hello 虛擬環境中，並安裝相依項目 requirements.txt 中列出。</span><span class="sxs-lookup"><span data-stu-id="000e4-180">This will create hello virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="000e4-181">使用開發伺服器來執行</span><span class="sxs-lookup"><span data-stu-id="000e4-181">Run using development server</span></span>
<span data-ttu-id="000e4-182">偵錯，請按 F5 toostart 和網頁瀏覽器會開啟自動在本機執行的 toohello 頁面。</span><span class="sxs-lookup"><span data-stu-id="000e4-182">Press F5 toostart debugging, and your web browser will open automatically toohello page running locally.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

<span data-ttu-id="000e4-183">您可以在 hello 來源、 使用 hello 監看式視窗和其他內容中設定中斷點。請參閱 hello [Python Tools for Visual Studio 文件]如需有關 hello 各種功能。</span><span class="sxs-lookup"><span data-stu-id="000e4-183">You can set breakpoints in hello sources, use hello watch windows, etc.  See hello [Python Tools for Visual Studio Documentation] for more information on hello various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="000e4-184">進行變更</span><span class="sxs-lookup"><span data-stu-id="000e4-184">Make changes</span></span>
<span data-ttu-id="000e4-185">現在您可以嘗試藉由變更 toohello 應用程式來源及/或範本。</span><span class="sxs-lookup"><span data-stu-id="000e4-185">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="000e4-186">測試過您的變更之後，認可這些 toohello Git 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="000e4-186">After you've tested your changes, commit them toohello Git repository:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-commit-flask.png)

### <a name="install-more-packages"></a><span data-ttu-id="000e4-187">安裝更多封裝</span><span class="sxs-lookup"><span data-stu-id="000e4-187">Install more packages</span></span>
<span data-ttu-id="000e4-188">您的應用程式可能會擁有 Python 和 Flask 之外的相依性。</span><span class="sxs-lookup"><span data-stu-id="000e4-188">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="000e4-189">您可以使用 pip 安裝其他封裝。</span><span class="sxs-lookup"><span data-stu-id="000e4-189">You can install additional packages using pip.</span></span>  <span data-ttu-id="000e4-190">tooinstall 封裝時，以滑鼠右鍵按一下 hello 虛擬環境，並選取**安裝 Python 封裝**。</span><span class="sxs-lookup"><span data-stu-id="000e4-190">tooinstall a package, right-click on hello virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="000e4-191">例如，tooinstall hello Azure SDK for Python 可讓您存取 tooAzure 儲存體、 服務匯流排和其他 Azure 服務，輸入`azure`:</span><span class="sxs-lookup"><span data-stu-id="000e4-191">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-install-package-dialog.png)

<span data-ttu-id="000e4-192">以滑鼠右鍵按一下 hello 虛擬環境，然後選取**產生 requirements.txt** tooupdate requirements.txt。</span><span class="sxs-lookup"><span data-stu-id="000e4-192">Right-click on hello virtual environment and select **Generate requirements.txt** tooupdate requirements.txt.</span></span>

<span data-ttu-id="000e4-193">然後，認可 hello 變更 toorequirements.txt toohello Git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="000e4-193">Then, commit hello changes toorequirements.txt toohello Git repository.</span></span>

### <a name="deploy-tooazure"></a><span data-ttu-id="000e4-194">部署 tooAzure</span><span class="sxs-lookup"><span data-stu-id="000e4-194">Deploy tooAzure</span></span>
<span data-ttu-id="000e4-195">tootrigger 部署中，按一下 **同步**或**推送**。</span><span class="sxs-lookup"><span data-stu-id="000e4-195">tootrigger a deployment, click on **Sync** or **Push**.</span></span>  <span data-ttu-id="000e4-196">同步處理會推送和提取。</span><span class="sxs-lookup"><span data-stu-id="000e4-196">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-git-push.png)

<span data-ttu-id="000e4-197">hello 第一次部署將需要一些時間，因為它會建立虛擬環境、 安裝套件和其他內容。</span><span class="sxs-lookup"><span data-stu-id="000e4-197">hello first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="000e4-198">Visual Studio 不會顯示 hello 部署的 hello 進度。</span><span class="sxs-lookup"><span data-stu-id="000e4-198">Visual Studio doesn't show hello progress of hello deployment.</span></span>  <span data-ttu-id="000e4-199">如果您想要 tooreview hello 輸出，請參閱 hello 章節[疑難排解-部署](#troubleshooting-deployment)。</span><span class="sxs-lookup"><span data-stu-id="000e4-199">If you'd like tooreview hello output, see hello section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="000e4-200">瀏覽 toohello Azure URL tooview 您的變更。</span><span class="sxs-lookup"><span data-stu-id="000e4-200">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="000e4-201">Web 應用程式開發 - Windows - 命令列</span><span class="sxs-lookup"><span data-stu-id="000e4-201">Web app development - Windows - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="000e4-202">複製 hello 儲存機制</span><span class="sxs-lookup"><span data-stu-id="000e4-202">Clone hello repository</span></span>
<span data-ttu-id="000e4-203">首先，複製 hello 儲存機制使用 hello hello Azure 網站上所提供的 URL，並新增與遠端的 hello Azure 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="000e4-203">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="000e4-204">如需詳細資訊，請參閱[應用程式服務的本機 Git 部署 tooAzure](app-service-deploy-local-git.md)。</span><span class="sxs-lookup"><span data-stu-id="000e4-204">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="000e4-205">建立虛擬環境</span><span class="sxs-lookup"><span data-stu-id="000e4-205">Create virtual environment</span></span>
<span data-ttu-id="000e4-206">我們將建立新的虛擬環境，供開發應用程式 （不要將它 toohello 儲存機制）。</span><span class="sxs-lookup"><span data-stu-id="000e4-206">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span>  <span data-ttu-id="000e4-207">Python 中的虛擬環境並不是可重置，因此處理 hello 應用程式開發人員會建立自己在本機。</span><span class="sxs-lookup"><span data-stu-id="000e4-207">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="000e4-208">請確定 toouse hello 相同版本的 web 應用程式的已選取的 Python (runtime.txt 或 hello**應用程式設定**刀鋒視窗中的 hello Azure 入口網站中的 web 應用程式)。</span><span class="sxs-lookup"><span data-stu-id="000e4-208">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="000e4-209">針對 Python 2.7：</span><span class="sxs-lookup"><span data-stu-id="000e4-209">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="000e4-210">針對 Python 3.4：</span><span class="sxs-lookup"><span data-stu-id="000e4-210">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="000e4-211">安裝應用程式所需的任何外部封裝。</span><span class="sxs-lookup"><span data-stu-id="000e4-211">Install any external packages required by your application.</span></span> <span data-ttu-id="000e4-212">您可以在虛擬環境中，根目錄 hello hello 儲存機制 tooinstall hello 封裝使用 hello requirements.txt 檔案：</span><span class="sxs-lookup"><span data-stu-id="000e4-212">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="000e4-213">使用開發伺服器來執行</span><span class="sxs-lookup"><span data-stu-id="000e4-213">Run using development server</span></span>
<span data-ttu-id="000e4-214">您可以啟動 hello 應用程式開發伺服器底下，以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="000e4-214">You can launch hello application under a development server with hello following command:</span></span>

    env\scripts\python runserver.py

<span data-ttu-id="000e4-215">hello 主控台就會顯示 hello URL，而且會接聽通訊埠 hello 伺服器：</span><span class="sxs-lookup"><span data-stu-id="000e4-215">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-run-local-flask.png)

<span data-ttu-id="000e4-216">然後，開啟您的 web 瀏覽器 toothat URL。</span><span class="sxs-lookup"><span data-stu-id="000e4-216">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="000e4-217">進行變更</span><span class="sxs-lookup"><span data-stu-id="000e4-217">Make changes</span></span>
<span data-ttu-id="000e4-218">現在您可以嘗試藉由變更 toohello 應用程式來源及/或範本。</span><span class="sxs-lookup"><span data-stu-id="000e4-218">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="000e4-219">測試過您的變更之後，認可這些 toohello Git 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="000e4-219">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="000e4-220">安裝更多封裝</span><span class="sxs-lookup"><span data-stu-id="000e4-220">Install more packages</span></span>
<span data-ttu-id="000e4-221">您的應用程式可能會擁有 Python 和 Flask 之外的相依性。</span><span class="sxs-lookup"><span data-stu-id="000e4-221">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="000e4-222">您可以使用 pip 安裝其他封裝。</span><span class="sxs-lookup"><span data-stu-id="000e4-222">You can install additional packages using pip.</span></span>  <span data-ttu-id="000e4-223">例如，tooinstall hello Azure SDK for Python 可讓您存取 tooAzure 儲存體、 服務匯流排和其他 Azure 服務類型：</span><span class="sxs-lookup"><span data-stu-id="000e4-223">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="000e4-224">請確定 tooupdate requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="000e4-224">Make sure tooupdate requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="000e4-225">認可 hello 變更：</span><span class="sxs-lookup"><span data-stu-id="000e4-225">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="000e4-226">部署 tooAzure</span><span class="sxs-lookup"><span data-stu-id="000e4-226">Deploy tooAzure</span></span>
<span data-ttu-id="000e4-227">tootrigger 部署，推入 hello 變更 tooAzure:</span><span class="sxs-lookup"><span data-stu-id="000e4-227">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="000e4-228">您會看到 hello 輸出 hello 部署指令碼，包括建立虛擬環境安裝封裝，建立 web.config。</span><span class="sxs-lookup"><span data-stu-id="000e4-228">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="000e4-229">瀏覽 toohello Azure URL tooview 您的變更。</span><span class="sxs-lookup"><span data-stu-id="000e4-229">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="000e4-230">Web 應用程式開發 - Mac/Linux - 命令列</span><span class="sxs-lookup"><span data-stu-id="000e4-230">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="000e4-231">複製 hello 儲存機制</span><span class="sxs-lookup"><span data-stu-id="000e4-231">Clone hello repository</span></span>
<span data-ttu-id="000e4-232">首先，複製 hello 儲存機制使用 hello hello Azure 網站上所提供的 URL，並新增與遠端的 hello Azure 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="000e4-232">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="000e4-233">如需詳細資訊，請參閱[應用程式服務的本機 Git 部署 tooAzure](app-service-deploy-local-git.md)。</span><span class="sxs-lookup"><span data-stu-id="000e4-233">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="000e4-234">建立虛擬環境</span><span class="sxs-lookup"><span data-stu-id="000e4-234">Create virtual environment</span></span>
<span data-ttu-id="000e4-235">我們將建立新的虛擬環境，供開發應用程式 （不要將它 toohello 儲存機制）。</span><span class="sxs-lookup"><span data-stu-id="000e4-235">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span>  <span data-ttu-id="000e4-236">Python 中的虛擬環境並不是可重置，因此處理 hello 應用程式開發人員會建立自己在本機。</span><span class="sxs-lookup"><span data-stu-id="000e4-236">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="000e4-237">請確定 toouse hello 相同版本的 web 應用程式的已選取的 Python (runtime.txt 或 hello**應用程式設定**刀鋒視窗中的 hello Azure 入口網站中的 web 應用程式)。</span><span class="sxs-lookup"><span data-stu-id="000e4-237">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="000e4-238">針對 Python 2.7：</span><span class="sxs-lookup"><span data-stu-id="000e4-238">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="000e4-239">針對 Python 3.4：</span><span class="sxs-lookup"><span data-stu-id="000e4-239">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="000e4-240">或 pyvenv env</span><span class="sxs-lookup"><span data-stu-id="000e4-240">or pyvenv env</span></span>

<span data-ttu-id="000e4-241">安裝應用程式所需的任何外部封裝。</span><span class="sxs-lookup"><span data-stu-id="000e4-241">Install any external packages required by your application.</span></span> <span data-ttu-id="000e4-242">您可以在虛擬環境中，根目錄 hello hello 儲存機制 tooinstall hello 封裝使用 hello requirements.txt 檔案：</span><span class="sxs-lookup"><span data-stu-id="000e4-242">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="000e4-243">使用開發伺服器來執行</span><span class="sxs-lookup"><span data-stu-id="000e4-243">Run using development server</span></span>
<span data-ttu-id="000e4-244">您可以啟動 hello 應用程式開發伺服器底下，以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="000e4-244">You can launch hello application under a development server with hello following command:</span></span>

    env/bin/python runserver.py

<span data-ttu-id="000e4-245">hello 主控台就會顯示 hello URL，而且會接聽通訊埠 hello 伺服器：</span><span class="sxs-lookup"><span data-stu-id="000e4-245">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-run-local-flask.png)

<span data-ttu-id="000e4-246">然後，開啟您的 web 瀏覽器 toothat URL。</span><span class="sxs-lookup"><span data-stu-id="000e4-246">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="000e4-247">進行變更</span><span class="sxs-lookup"><span data-stu-id="000e4-247">Make changes</span></span>
<span data-ttu-id="000e4-248">現在您可以嘗試藉由變更 toohello 應用程式來源及/或範本。</span><span class="sxs-lookup"><span data-stu-id="000e4-248">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="000e4-249">測試過您的變更之後，認可這些 toohello Git 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="000e4-249">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="000e4-250">安裝更多封裝</span><span class="sxs-lookup"><span data-stu-id="000e4-250">Install more packages</span></span>
<span data-ttu-id="000e4-251">您的應用程式可能會擁有 Python 和 Flask 之外的相依性。</span><span class="sxs-lookup"><span data-stu-id="000e4-251">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="000e4-252">您可以使用 pip 安裝其他封裝。</span><span class="sxs-lookup"><span data-stu-id="000e4-252">You can install additional packages using pip.</span></span>  <span data-ttu-id="000e4-253">例如，tooinstall hello Azure SDK for Python 可讓您存取 tooAzure 儲存體、 服務匯流排和其他 Azure 服務類型：</span><span class="sxs-lookup"><span data-stu-id="000e4-253">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="000e4-254">請確定 tooupdate requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="000e4-254">Make sure tooupdate requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="000e4-255">認可 hello 變更：</span><span class="sxs-lookup"><span data-stu-id="000e4-255">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="000e4-256">部署 tooAzure</span><span class="sxs-lookup"><span data-stu-id="000e4-256">Deploy tooAzure</span></span>
<span data-ttu-id="000e4-257">tootrigger 部署，推入 hello 變更 tooAzure:</span><span class="sxs-lookup"><span data-stu-id="000e4-257">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="000e4-258">您會看到 hello 輸出 hello 部署指令碼，包括建立虛擬環境安裝封裝，建立 web.config。</span><span class="sxs-lookup"><span data-stu-id="000e4-258">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="000e4-259">瀏覽 toohello Azure URL tooview 您的變更。</span><span class="sxs-lookup"><span data-stu-id="000e4-259">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="000e4-260">疑難排解 - 封裝安裝</span><span class="sxs-lookup"><span data-stu-id="000e4-260">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="000e4-261">疑難排解 - 虛擬環境</span><span class="sxs-lookup"><span data-stu-id="000e4-261">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="000e4-262">後續步驟</span><span class="sxs-lookup"><span data-stu-id="000e4-262">Next Steps</span></span>
<span data-ttu-id="000e4-263">請遵循這些連結 toolearn 更多關於酒瓶和 Python Tools for Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="000e4-263">Follow these links toolearn more about Flask and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="000e4-264">[Flask 說明文件 英文]</span><span class="sxs-lookup"><span data-stu-id="000e4-264">[Flask Documentation]</span></span>
* <span data-ttu-id="000e4-265">[Python Tools for Visual Studio 文件]</span><span class="sxs-lookup"><span data-stu-id="000e4-265">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="000e4-266">如需有關使用 Azure 資料表儲存體和 MongoDB 的資訊：</span><span class="sxs-lookup"><span data-stu-id="000e4-266">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="000e4-267">[Azure 上使用 Python Tools for Visual Studio 的 Flask 和 MongoDB]</span><span class="sxs-lookup"><span data-stu-id="000e4-267">[Flask and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="000e4-268">[Azure 上使用 Python Tools for Visual Studio 的 Flask 和 Azure 資料表儲存體]</span><span class="sxs-lookup"><span data-stu-id="000e4-268">[Flask and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="000e4-269">如需詳細資訊，請參閱 hello [Python 開發人員中心](/develop/python/)。</span><span class="sxs-lookup"><span data-stu-id="000e4-269">For more information, see also hello [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="000e4-270">變更的項目</span><span class="sxs-lookup"><span data-stu-id="000e4-270">What's changed</span></span>
* <span data-ttu-id="000e4-271">從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="000e4-271">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Azure 上使用 Python Tools for Visual Studio 的 Flask 和 MongoDB]: https://github.com/microsoft/ptvs/wiki/Flask-and-MongoDB-on-Azure
[Azure 上使用 Python Tools for Visual Studio 的 Flask 和 Azure 資料表儲存體]: web-sites-python-ptvs-flask-table-storage.md

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
[Flask 說明文件 英文]: http://flask.pocoo.org/ 

