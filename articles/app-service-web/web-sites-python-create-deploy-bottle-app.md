---
title: "在 Azure 中的 Bottle aaaPython web 應用程式"
description: "此教學課程為您介紹 toorunning Python web 應用程式在 Azure App Service Web 應用程式。"
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 84f043b8-9d05-479f-a9d0-d0d9a32a0bb9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2016
ms.author: huvalo
ms.openlocfilehash: 98acd7d8fcdbba326625121c20f9237d2663ea1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-bottle-in-azure"></a><span data-ttu-id="32c2e-103">在 Azure 中使用 Bottle 建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="32c2e-103">Creating web apps with Bottle in Azure</span></span>
<span data-ttu-id="32c2e-104">本教學課程描述 tooget 啟動 Azure App Service Web 應用程式中執行 Python 的方式。</span><span class="sxs-lookup"><span data-stu-id="32c2e-104">This tutorial describes how tooget started running Python in Azure App Service Web Apps.</span></span> <span data-ttu-id="32c2e-105">Web Apps 提供有限的免費裝載和快速部署，而您可以使用 Python！</span><span class="sxs-lookup"><span data-stu-id="32c2e-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="32c2e-106">當您的應用程式成長，您可以切換 toopaid 裝載，您也可以與所有的整合 hello 其他 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="32c2e-106">As your app grows, you can switch toopaid hosting, and you can also integrate with all of hello other Azure services.</span></span>

<span data-ttu-id="32c2e-107">您將建立使用 hello Bottle web 架構的 web 應用程式 (請參閱本教學課程中的替代版本[Django](web-sites-python-create-deploy-django-app.md)和[酒瓶](web-sites-python-create-deploy-flask-app.md))。</span><span class="sxs-lookup"><span data-stu-id="32c2e-107">You will create a web app using hello Bottle web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Flask](web-sites-python-create-deploy-flask-app.md)).</span></span> <span data-ttu-id="32c2e-108">您會建立從 hello Azure Marketplace 的 hello web 應用程式、 設定 Git 部署和複製本機 hello 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="32c2e-108">You will create hello web app from hello Azure Marketplace, set up Git deployment, and clone hello repository locally.</span></span> <span data-ttu-id="32c2e-109">然後您會在本機執行 hello web 應用程式、 進行變更、 認可並推送它們太[Azure App Service Web 應用程式](http://go.microsoft.com/fwlink/?LinkId=529714)。</span><span class="sxs-lookup"><span data-stu-id="32c2e-109">Then you will run hello web app locally, make changes, commit and push them too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="32c2e-110">hello 教學課程顯示如何 toodo 於 Windows 或 Mac/Linux。</span><span class="sxs-lookup"><span data-stu-id="32c2e-110">hello tutorial shows how toodo this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="32c2e-111">如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="32c2e-111">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="32c2e-112">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="32c2e-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="32c2e-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="32c2e-113">Prerequisites</span></span>
* <span data-ttu-id="32c2e-114">Windows、Mac 或 Linux</span><span class="sxs-lookup"><span data-stu-id="32c2e-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="32c2e-115">Python 2.7 或 3.4</span><span class="sxs-lookup"><span data-stu-id="32c2e-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="32c2e-116">setuptools、pip、virtualenv (僅 Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="32c2e-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="32c2e-117">Git</span><span class="sxs-lookup"><span data-stu-id="32c2e-117">Git</span></span>
* <span data-ttu-id="32c2e-118">[Python Tools 2.2 for Visual Studio][Python Tools 2.2 for Visual Studio] (PTVS) - 注意：這是選擇性的</span><span class="sxs-lookup"><span data-stu-id="32c2e-118">[Python Tools 2.2 for Visual Studio][Python Tools 2.2 for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="32c2e-119">**注意**：Python 專案目前不支援 TFS 發佈。</span><span class="sxs-lookup"><span data-stu-id="32c2e-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="32c2e-120">Windows</span><span class="sxs-lookup"><span data-stu-id="32c2e-120">Windows</span></span>
<span data-ttu-id="32c2e-121">如果您還沒有安裝 Python 2.7 或 3.4 (32 位元)，建議您使用 Web Platform Installer 安裝 [Azure SDK for Python 2.7] 或 [Azure SDK for Python 3.4]。</span><span class="sxs-lookup"><span data-stu-id="32c2e-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="32c2e-122">這會安裝 hello 32 位元版本的 Python、 setuptools、 pip、 virtualenv 等 （32 位元 Python 是 hello Azure 主機機器上安裝的內容）。</span><span class="sxs-lookup"><span data-stu-id="32c2e-122">This installs hello 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on hello Azure host machines).</span></span> <span data-ttu-id="32c2e-123">或者，您可以從 [python.org]取得 Python。</span><span class="sxs-lookup"><span data-stu-id="32c2e-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="32c2e-124">針對 Git，建議您安裝 [Git for Windows] 或 [GitHub for Windows]。</span><span class="sxs-lookup"><span data-stu-id="32c2e-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="32c2e-125">如果您使用 Visual Studio，您可以使用整合的 hello Git 支援。</span><span class="sxs-lookup"><span data-stu-id="32c2e-125">If you use Visual Studio, you can use hello integrated Git support.</span></span>

<span data-ttu-id="32c2e-126">我們也建議您安裝 [Python Tools 2.2 for Visual Studio]。</span><span class="sxs-lookup"><span data-stu-id="32c2e-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="32c2e-127">這是選擇性的但如果您有[Visual Studio]，包括 hello 釋放 Visual Studio Community 2013 或 Visual Studio Express 2013 for Web，則這會提供絕佳的 Python IDE。</span><span class="sxs-lookup"><span data-stu-id="32c2e-127">This is optional, but if you have [Visual Studio], including hello free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="32c2e-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="32c2e-128">Mac/Linux</span></span>
<span data-ttu-id="32c2e-129">您應該已經安裝 Python 與 Git，但請確定您擁有的是 Python 2.7 或 3.4。</span><span class="sxs-lookup"><span data-stu-id="32c2e-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-hello-azure-portal"></a><span data-ttu-id="32c2e-130">在 hello Azure 入口網站上建立 web 應用程式</span><span class="sxs-lookup"><span data-stu-id="32c2e-130">Web app creation on hello Azure Portal</span></span>
<span data-ttu-id="32c2e-131">hello 第一個步驟中建立您的應用程式是 toocreate hello web 應用程式，透過 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="32c2e-131">hello first step in creating your app is toocreate hello web app via hello [Azure Portal](https://portal.azure.com).</span></span>  

1. <span data-ttu-id="32c2e-132">登入 hello Azure 入口網站並按一下 hello**新增**hello 左下角中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="32c2e-132">Log into hello Azure Portal and click hello **NEW** button in hello bottom left corner.</span></span> 
2. <span data-ttu-id="32c2e-133">在 hello 搜尋方塊中輸入"python"。</span><span class="sxs-lookup"><span data-stu-id="32c2e-133">In hello search box, type "python".</span></span>
3. <span data-ttu-id="32c2e-134">在 hello 搜尋結果中，選取  **Bottle**，然後按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="32c2e-134">In hello search results, select **Bottle**, then click **Create**.</span></span>
4. <span data-ttu-id="32c2e-135">設定 hello 新 Bottle 應用程式，例如為它建立新的應用程式服務方案和新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="32c2e-135">Configure hello new Bottle app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="32c2e-136">然後按一下 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="32c2e-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="32c2e-137">設定 Git 發行功能，新建立的 web 應用程式在 hello 指示[應用程式服務的本機 Git 部署 tooAzure](app-service-deploy-local-git.md)。</span><span class="sxs-lookup"><span data-stu-id="32c2e-137">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="32c2e-138">應用程式概觀</span><span class="sxs-lookup"><span data-stu-id="32c2e-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="32c2e-139">Git 儲存機制內容</span><span class="sxs-lookup"><span data-stu-id="32c2e-139">Git repository contents</span></span>
<span data-ttu-id="32c2e-140">以下是您會發現在 hello 初始 Git 儲存機制，我們將複製 hello 下一節中的 hello 檔案的概觀。</span><span class="sxs-lookup"><span data-stu-id="32c2e-140">Here's an overview of hello files you'll find in hello initial Git repository, which we'll clone in hello next section.</span></span>

    \routes.py
    \static\content\
    \static\fonts\
    \static\scripts\
    \views\about.tpl
    \views\contact.tpl
    \views\index.tpl
    \views\layout.tpl

<span data-ttu-id="32c2e-141">Hello 應用程式的主要來源。</span><span class="sxs-lookup"><span data-stu-id="32c2e-141">Main sources for hello application.</span></span> <span data-ttu-id="32c2e-142">包含 3 個主要的版面配置頁面 (index、about、contact)。</span><span class="sxs-lookup"><span data-stu-id="32c2e-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="32c2e-143">靜態內容和指令碼，包含啟動程序、jquery、modernizr 和回應。</span><span class="sxs-lookup"><span data-stu-id="32c2e-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \app.py

<span data-ttu-id="32c2e-144">本機開發伺服器支援。</span><span class="sxs-lookup"><span data-stu-id="32c2e-144">Local development server support.</span></span> <span data-ttu-id="32c2e-145">在本機上使用此 toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="32c2e-145">Use this toorun hello application locally.</span></span>

    \BottleWebProject.pyproj
    \BottleWebProject.sln

<span data-ttu-id="32c2e-146">搭配 [Python Tools for Visual Studio]使用的專案檔。</span><span class="sxs-lookup"><span data-stu-id="32c2e-146">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="32c2e-147">虛擬環境和 PTVS 遠端偵錯支援的 IIS Proxy。</span><span class="sxs-lookup"><span data-stu-id="32c2e-147">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="32c2e-148">此應用程式所需的外部封裝。</span><span class="sxs-lookup"><span data-stu-id="32c2e-148">External packages needed by this application.</span></span> <span data-ttu-id="32c2e-149">hello 部署指令碼將 pip 安裝 hello 封裝這個檔案中列出。</span><span class="sxs-lookup"><span data-stu-id="32c2e-149">hello deployment script will pip install hello packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="32c2e-150">IIS 組態檔。</span><span class="sxs-lookup"><span data-stu-id="32c2e-150">IIS configuration files.</span></span> <span data-ttu-id="32c2e-151">將使用 hello 適當 web.x.y.config hello 部署指令碼，並將它複製為 web.config。</span><span class="sxs-lookup"><span data-stu-id="32c2e-151">hello deployment script will use hello appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="32c2e-152">選用的檔案 - 自訂部署</span><span class="sxs-lookup"><span data-stu-id="32c2e-152">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="32c2e-153">選用的檔案 - Python 執行階段</span><span class="sxs-lookup"><span data-stu-id="32c2e-153">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="32c2e-154">在伺服器上的其他檔案</span><span class="sxs-lookup"><span data-stu-id="32c2e-154">Additional files on server</span></span>
<span data-ttu-id="32c2e-155">某些檔案存在於 hello 伺服器，但不是會新增 toohello git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="32c2e-155">Some files exist on hello server but are not added toohello git repository.</span></span> <span data-ttu-id="32c2e-156">這些被建立 hello 部署指令碼。</span><span class="sxs-lookup"><span data-stu-id="32c2e-156">These are created by hello deployment script.</span></span>

    \web.config

<span data-ttu-id="32c2e-157">IIS 組態檔。</span><span class="sxs-lookup"><span data-stu-id="32c2e-157">IIS configuration file.</span></span> <span data-ttu-id="32c2e-158">從 web.x.y.config 建立於每個部署上。</span><span class="sxs-lookup"><span data-stu-id="32c2e-158">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="32c2e-159">Python 虛擬環境。</span><span class="sxs-lookup"><span data-stu-id="32c2e-159">Python virtual environment.</span></span> <span data-ttu-id="32c2e-160">如果相容的虛擬環境不存在 hello web 應用程式上，在部署期間建立。</span><span class="sxs-lookup"><span data-stu-id="32c2e-160">Created during deployment if a compatible virtual environment doesn't already exist on hello web app.</span></span>  <span data-ttu-id="32c2e-161">封裝中 requirements.txt 列出 pip 安裝，但 pip 會略過安裝，如果已安裝 hello 封裝。</span><span class="sxs-lookup"><span data-stu-id="32c2e-161">Packages listed in requirements.txt are pip installed, but pip will skip installation if hello packages are already installed.</span></span>

<span data-ttu-id="32c2e-162">hello 接下來的 3 各節說明如何以 hello tooproceed web 3 不同環境下的應用程式開發：</span><span class="sxs-lookup"><span data-stu-id="32c2e-162">hello next 3 sections describe how tooproceed with hello web app development under 3 different environments:</span></span>

* <span data-ttu-id="32c2e-163">Windows，使用 Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="32c2e-163">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="32c2e-164">Windows，使用命令列</span><span class="sxs-lookup"><span data-stu-id="32c2e-164">Windows, with command line</span></span>
* <span data-ttu-id="32c2e-165">Mac/Linux，使用命令列</span><span class="sxs-lookup"><span data-stu-id="32c2e-165">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="32c2e-166">Web 應用程式開發 - Windows - 適用於 Visual Studio 的 Python 工具</span><span class="sxs-lookup"><span data-stu-id="32c2e-166">Web App development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="32c2e-167">複製 hello 儲存機制</span><span class="sxs-lookup"><span data-stu-id="32c2e-167">Clone hello repository</span></span>
<span data-ttu-id="32c2e-168">首先，複製 hello 儲存機制使用 hello hello Azure 入口網站上所提供的 url。</span><span class="sxs-lookup"><span data-stu-id="32c2e-168">First, clone hello repository using hello url provided on hello Azure Portal.</span></span> <span data-ttu-id="32c2e-169">如需詳細資訊，請參閱[應用程式服務的本機 Git 部署 tooAzure](app-service-deploy-local-git.md)。</span><span class="sxs-lookup"><span data-stu-id="32c2e-169">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="32c2e-170">開啟包含 hello hello 儲存機制的根目錄中的 hello 方案檔 (.sln)。</span><span class="sxs-lookup"><span data-stu-id="32c2e-170">Open hello solution file (.sln) that is included in hello root of hello repository.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-solution-bottle.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="32c2e-171">建立虛擬環境</span><span class="sxs-lookup"><span data-stu-id="32c2e-171">Create virtual environment</span></span>
<span data-ttu-id="32c2e-172">現在我們要建立本機開發的虛擬環境。</span><span class="sxs-lookup"><span data-stu-id="32c2e-172">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="32c2e-173">以滑鼠右鍵按一下 [Python 環境]，選取 [新增虛擬環境...]。</span><span class="sxs-lookup"><span data-stu-id="32c2e-173">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="32c2e-174">請確定 hello 環境的 hello 名稱`env`。</span><span class="sxs-lookup"><span data-stu-id="32c2e-174">Make sure hello name of hello environment is `env`.</span></span>
* <span data-ttu-id="32c2e-175">選取 hello 基底直譯器。</span><span class="sxs-lookup"><span data-stu-id="32c2e-175">Select hello base interpreter.</span></span> <span data-ttu-id="32c2e-176">請確定 toouse hello 相同版本的 web 應用程式的已選取的 Python (runtime.txt 或 hello**應用程式設定**刀鋒視窗中的 hello Azure 入口網站中的 web 應用程式)。</span><span class="sxs-lookup"><span data-stu-id="32c2e-176">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>
* <span data-ttu-id="32c2e-177">請確定已核取 hello 選項 toodownload 和安裝封裝。</span><span class="sxs-lookup"><span data-stu-id="32c2e-177">Make sure hello option toodownload and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="32c2e-178">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="32c2e-178">Click **Create**.</span></span> <span data-ttu-id="32c2e-179">將建立 hello 虛擬環境中，並安裝相依項目 requirements.txt 中列出。</span><span class="sxs-lookup"><span data-stu-id="32c2e-179">This will create hello virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="32c2e-180">使用開發伺服器來執行</span><span class="sxs-lookup"><span data-stu-id="32c2e-180">Run using development server</span></span>
<span data-ttu-id="32c2e-181">偵錯，請按 F5 toostart 和網頁瀏覽器會開啟自動在本機執行的 toohello 頁面。</span><span class="sxs-lookup"><span data-stu-id="32c2e-181">Press F5 toostart debugging, and your web browser will open automatically toohello page running locally.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

<span data-ttu-id="32c2e-182">您可以在 hello 來源、 使用 hello 監看式視窗和其他內容中設定中斷點。請參閱 hello [Python Tools for Visual Studio 文件]如需有關 hello 各種功能。</span><span class="sxs-lookup"><span data-stu-id="32c2e-182">You can set breakpoints in hello sources, use hello watch windows, etc. See hello [Python Tools for Visual Studio Documentation] for more information on hello various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="32c2e-183">進行變更</span><span class="sxs-lookup"><span data-stu-id="32c2e-183">Make changes</span></span>
<span data-ttu-id="32c2e-184">現在您可以嘗試藉由變更 toohello 應用程式來源及/或範本。</span><span class="sxs-lookup"><span data-stu-id="32c2e-184">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="32c2e-185">測試過您的變更之後，認可這些 toohello Git 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="32c2e-185">After you've tested your changes, commit them toohello Git repository:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-commit-bottle.png)

### <a name="install-more-packages"></a><span data-ttu-id="32c2e-186">安裝更多封裝</span><span class="sxs-lookup"><span data-stu-id="32c2e-186">Install more packages</span></span>
<span data-ttu-id="32c2e-187">您的應用程式可能會擁有 Python 和 Bottle 之外的相依性。</span><span class="sxs-lookup"><span data-stu-id="32c2e-187">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="32c2e-188">您可以使用 pip 安裝其他封裝。</span><span class="sxs-lookup"><span data-stu-id="32c2e-188">You can install additional packages using pip.</span></span> <span data-ttu-id="32c2e-189">tooinstall 封裝時，以滑鼠右鍵按一下 hello 虛擬環境，並選取**安裝 Python 封裝**。</span><span class="sxs-lookup"><span data-stu-id="32c2e-189">tooinstall a package, right-click on hello virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="32c2e-190">例如，tooinstall hello Azure SDK for Python 可讓您存取 tooAzure 儲存體、 服務匯流排和其他 Azure 服務，輸入`azure`:</span><span class="sxs-lookup"><span data-stu-id="32c2e-190">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-install-package-dialog.png)

<span data-ttu-id="32c2e-191">以滑鼠右鍵按一下 hello 虛擬環境，然後選取**產生 requirements.txt** tooupdate requirements.txt。</span><span class="sxs-lookup"><span data-stu-id="32c2e-191">Right-click on hello virtual environment and select **Generate requirements.txt** tooupdate requirements.txt.</span></span>

<span data-ttu-id="32c2e-192">然後，認可 hello 變更 toorequirements.txt toohello Git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="32c2e-192">Then, commit hello changes toorequirements.txt toohello Git repository.</span></span>

### <a name="deploy-tooazure"></a><span data-ttu-id="32c2e-193">部署 tooAzure</span><span class="sxs-lookup"><span data-stu-id="32c2e-193">Deploy tooAzure</span></span>
<span data-ttu-id="32c2e-194">tootrigger 部署中，按一下 **同步**或**推送**。</span><span class="sxs-lookup"><span data-stu-id="32c2e-194">tootrigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="32c2e-195">同步處理會推送和提取。</span><span class="sxs-lookup"><span data-stu-id="32c2e-195">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-git-push.png)

<span data-ttu-id="32c2e-196">hello 第一次部署將需要一些時間，因為它會建立虛擬環境、 安裝套件和其他內容。</span><span class="sxs-lookup"><span data-stu-id="32c2e-196">hello first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="32c2e-197">Visual Studio 不會顯示 hello 部署的 hello 進度。</span><span class="sxs-lookup"><span data-stu-id="32c2e-197">Visual Studio doesn't show hello progress of hello deployment.</span></span> <span data-ttu-id="32c2e-198">如果您想要 tooreview hello 輸出，請參閱 hello 章節[疑難排解-部署](#troubleshooting-deployment)。</span><span class="sxs-lookup"><span data-stu-id="32c2e-198">If you'd like tooreview hello output, see hello section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="32c2e-199">瀏覽 toohello Azure URL tooview 您的變更。</span><span class="sxs-lookup"><span data-stu-id="32c2e-199">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="32c2e-200">Web 應用程式開發 - Windows - 命令列</span><span class="sxs-lookup"><span data-stu-id="32c2e-200">Web app development - Windows - Command Line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="32c2e-201">複製 hello 儲存機制</span><span class="sxs-lookup"><span data-stu-id="32c2e-201">Clone hello repository</span></span>
<span data-ttu-id="32c2e-202">首先，複製 hello 儲存機制使用 hello hello Azure 網站上所提供的 URL，並新增與遠端的 hello Azure 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="32c2e-202">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="32c2e-203">如需詳細資訊，請參閱[應用程式服務的本機 Git 部署 tooAzure](app-service-deploy-local-git.md)。</span><span class="sxs-lookup"><span data-stu-id="32c2e-203">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="32c2e-204">建立虛擬環境</span><span class="sxs-lookup"><span data-stu-id="32c2e-204">Create virtual environment</span></span>
<span data-ttu-id="32c2e-205">我們將建立新的虛擬環境，供開發應用程式 （不要將它 toohello 儲存機制）。</span><span class="sxs-lookup"><span data-stu-id="32c2e-205">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="32c2e-206">Python 中的虛擬環境並不是可重置，因此處理 hello 應用程式開發人員會建立自己在本機。</span><span class="sxs-lookup"><span data-stu-id="32c2e-206">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="32c2e-207">請確定 toouse hello 相同的 web 應用程式 （在 runtime.txt 或 hello 應用程式設定 刀鋒視窗中 hello Azure 入口網站 web 應用程式） 選取的 Python 版本</span><span class="sxs-lookup"><span data-stu-id="32c2e-207">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade for your web app in hello Azure Portal)</span></span>

<span data-ttu-id="32c2e-208">針對 Python 2.7：</span><span class="sxs-lookup"><span data-stu-id="32c2e-208">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="32c2e-209">針對 Python 3.4：</span><span class="sxs-lookup"><span data-stu-id="32c2e-209">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="32c2e-210">安裝應用程式所需的任何外部封裝。</span><span class="sxs-lookup"><span data-stu-id="32c2e-210">Install any external packages required by your application.</span></span> <span data-ttu-id="32c2e-211">您可以在虛擬環境中，根目錄 hello hello 儲存機制 tooinstall hello 封裝使用 hello requirements.txt 檔案：</span><span class="sxs-lookup"><span data-stu-id="32c2e-211">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="32c2e-212">使用開發伺服器來執行</span><span class="sxs-lookup"><span data-stu-id="32c2e-212">Run using development server</span></span>
<span data-ttu-id="32c2e-213">您可以啟動 hello 應用程式開發伺服器底下，以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="32c2e-213">You can launch hello application under a development server with hello following command:</span></span>

    env\scripts\python app.py

<span data-ttu-id="32c2e-214">hello 主控台就會顯示 hello URL，而且會接聽通訊埠 hello 伺服器：</span><span class="sxs-lookup"><span data-stu-id="32c2e-214">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-run-local-bottle.png)

<span data-ttu-id="32c2e-215">然後，開啟您的 web 瀏覽器 toothat URL。</span><span class="sxs-lookup"><span data-stu-id="32c2e-215">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="32c2e-216">進行變更</span><span class="sxs-lookup"><span data-stu-id="32c2e-216">Make changes</span></span>
<span data-ttu-id="32c2e-217">現在您可以嘗試藉由變更 toohello 應用程式來源及/或範本。</span><span class="sxs-lookup"><span data-stu-id="32c2e-217">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="32c2e-218">測試過您的變更之後，認可這些 toohello Git 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="32c2e-218">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="32c2e-219">安裝更多封裝</span><span class="sxs-lookup"><span data-stu-id="32c2e-219">Install more packages</span></span>
<span data-ttu-id="32c2e-220">您的應用程式可能會擁有 Python 和 Bottle 之外的相依性。</span><span class="sxs-lookup"><span data-stu-id="32c2e-220">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="32c2e-221">您可以使用 pip 安裝其他封裝。</span><span class="sxs-lookup"><span data-stu-id="32c2e-221">You can install additional packages using pip.</span></span> <span data-ttu-id="32c2e-222">例如，tooinstall hello Azure SDK for Python 可讓您存取 tooAzure 儲存體、 服務匯流排和其他 Azure 服務類型：</span><span class="sxs-lookup"><span data-stu-id="32c2e-222">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="32c2e-223">請確定 tooupdate requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="32c2e-223">Make sure tooupdate requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="32c2e-224">認可 hello 變更：</span><span class="sxs-lookup"><span data-stu-id="32c2e-224">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="32c2e-225">部署 tooAzure</span><span class="sxs-lookup"><span data-stu-id="32c2e-225">Deploy tooAzure</span></span>
<span data-ttu-id="32c2e-226">tootrigger 部署，推入 hello 變更 tooAzure:</span><span class="sxs-lookup"><span data-stu-id="32c2e-226">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="32c2e-227">您會看到 hello 輸出 hello 部署指令碼，包括建立虛擬環境安裝封裝，建立 web.config。</span><span class="sxs-lookup"><span data-stu-id="32c2e-227">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="32c2e-228">瀏覽 toohello Azure URL tooview 您的變更。</span><span class="sxs-lookup"><span data-stu-id="32c2e-228">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="32c2e-229">Web 應用程式開發 - Mac/Linux - 命令列</span><span class="sxs-lookup"><span data-stu-id="32c2e-229">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="32c2e-230">複製 hello 儲存機制</span><span class="sxs-lookup"><span data-stu-id="32c2e-230">Clone hello repository</span></span>
<span data-ttu-id="32c2e-231">首先，複製 hello 儲存機制使用 hello hello Azure 網站上所提供的 URL，並新增與遠端的 hello Azure 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="32c2e-231">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="32c2e-232">如需詳細資訊，請參閱[應用程式服務的本機 Git 部署 tooAzure](app-service-deploy-local-git.md)。</span><span class="sxs-lookup"><span data-stu-id="32c2e-232">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="32c2e-233">建立虛擬環境</span><span class="sxs-lookup"><span data-stu-id="32c2e-233">Create virtual environment</span></span>
<span data-ttu-id="32c2e-234">我們將建立新的虛擬環境，供開發應用程式 （不要將它 toohello 儲存機制）。</span><span class="sxs-lookup"><span data-stu-id="32c2e-234">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="32c2e-235">Python 中的虛擬環境並不是可重置，因此處理 hello 應用程式開發人員會建立自己在本機。</span><span class="sxs-lookup"><span data-stu-id="32c2e-235">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="32c2e-236">請確定 toouse hello 相同版本的 Python 選取 web 應用程式 （在 runtime.txt 或 hello 應用程式設定 刀鋒視窗的 hello Azure 入口網站中的 web 應用程式）。</span><span class="sxs-lookup"><span data-stu-id="32c2e-236">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="32c2e-237">針對 Python 2.7：</span><span class="sxs-lookup"><span data-stu-id="32c2e-237">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="32c2e-238">針對 Python 3.4：</span><span class="sxs-lookup"><span data-stu-id="32c2e-238">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="32c2e-239">或 pyvenv env</span><span class="sxs-lookup"><span data-stu-id="32c2e-239">or pyvenv env</span></span>

<span data-ttu-id="32c2e-240">安裝應用程式所需的任何外部封裝。</span><span class="sxs-lookup"><span data-stu-id="32c2e-240">Install any external packages required by your application.</span></span> <span data-ttu-id="32c2e-241">您可以在虛擬環境中，根目錄 hello hello 儲存機制 tooinstall hello 封裝使用 hello requirements.txt 檔案：</span><span class="sxs-lookup"><span data-stu-id="32c2e-241">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="32c2e-242">使用開發伺服器來執行</span><span class="sxs-lookup"><span data-stu-id="32c2e-242">Run using development server</span></span>
<span data-ttu-id="32c2e-243">您可以啟動 hello 應用程式開發伺服器底下，以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="32c2e-243">You can launch hello application under a development server with hello following command:</span></span>

    env/bin/python app.py

<span data-ttu-id="32c2e-244">hello 主控台就會顯示 hello URL，而且會接聽通訊埠 hello 伺服器：</span><span class="sxs-lookup"><span data-stu-id="32c2e-244">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-run-local-bottle.png)

<span data-ttu-id="32c2e-245">然後，開啟您的 web 瀏覽器 toothat URL。</span><span class="sxs-lookup"><span data-stu-id="32c2e-245">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="32c2e-246">進行變更</span><span class="sxs-lookup"><span data-stu-id="32c2e-246">Make changes</span></span>
<span data-ttu-id="32c2e-247">現在您可以嘗試藉由變更 toohello 應用程式來源及/或範本。</span><span class="sxs-lookup"><span data-stu-id="32c2e-247">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="32c2e-248">測試過您的變更之後，認可這些 toohello Git 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="32c2e-248">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="32c2e-249">安裝更多封裝</span><span class="sxs-lookup"><span data-stu-id="32c2e-249">Install more packages</span></span>
<span data-ttu-id="32c2e-250">您的應用程式可能會擁有 Python 和 Bottle 之外的相依性。</span><span class="sxs-lookup"><span data-stu-id="32c2e-250">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="32c2e-251">您可以使用 pip 安裝其他封裝。</span><span class="sxs-lookup"><span data-stu-id="32c2e-251">You can install additional packages using pip.</span></span> <span data-ttu-id="32c2e-252">例如，tooinstall hello Azure SDK for Python 可讓您存取 tooAzure 儲存體、 服務匯流排和其他 Azure 服務類型：</span><span class="sxs-lookup"><span data-stu-id="32c2e-252">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="32c2e-253">請確定 tooupdate requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="32c2e-253">Make sure tooupdate requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="32c2e-254">認可 hello 變更：</span><span class="sxs-lookup"><span data-stu-id="32c2e-254">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="32c2e-255">部署 tooAzure</span><span class="sxs-lookup"><span data-stu-id="32c2e-255">Deploy tooAzure</span></span>
<span data-ttu-id="32c2e-256">tootrigger 部署，推入 hello 變更 tooAzure:</span><span class="sxs-lookup"><span data-stu-id="32c2e-256">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="32c2e-257">您會看到 hello 輸出 hello 部署指令碼，包括建立虛擬環境安裝封裝，建立 web.config。</span><span class="sxs-lookup"><span data-stu-id="32c2e-257">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="32c2e-258">瀏覽 toohello Azure URL tooview 您的變更。</span><span class="sxs-lookup"><span data-stu-id="32c2e-258">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="32c2e-259">疑難排解 - 封裝安裝</span><span class="sxs-lookup"><span data-stu-id="32c2e-259">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="32c2e-260">疑難排解 - 虛擬環境</span><span class="sxs-lookup"><span data-stu-id="32c2e-260">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="32c2e-261">後續步驟</span><span class="sxs-lookup"><span data-stu-id="32c2e-261">Next Steps</span></span>
<span data-ttu-id="32c2e-262">請遵循這些連結 toolearn 更多關於 Bottle 和 Python Tools for Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="32c2e-262">Follow these links toolearn more about Bottle and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="32c2e-263">[Bottle 說明文件]</span><span class="sxs-lookup"><span data-stu-id="32c2e-263">[Bottle Documentation]</span></span>
* <span data-ttu-id="32c2e-264">[Python Tools for Visual Studio 文件]</span><span class="sxs-lookup"><span data-stu-id="32c2e-264">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="32c2e-265">如需有關使用 Azure 資料表儲存體和 MongoDB 的資訊：</span><span class="sxs-lookup"><span data-stu-id="32c2e-265">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="32c2e-266">[Azure 上使用 Python Tools for Visual Studio 的 Bottle 和 MongoDB]</span><span class="sxs-lookup"><span data-stu-id="32c2e-266">[Bottle and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="32c2e-267">[Azure 上使用 Python Tools for Visual Studio 的 Bottle 和 Azure 資料表儲存體]</span><span class="sxs-lookup"><span data-stu-id="32c2e-267">[Bottle and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="32c2e-268">變更的項目</span><span class="sxs-lookup"><span data-stu-id="32c2e-268">What's changed</span></span>
* <span data-ttu-id="32c2e-269">從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="32c2e-269">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Azure 上使用 Python Tools for Visual Studio 的 Bottle 和 MongoDB]: web-sites-python-ptvs-bottle-table-storage.md
[Azure 上使用 Python Tools for Visual Studio 的 Bottle 和 Azure 資料表儲存體]: web-sites-python-ptvs-bottle-table-storage.md

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
[Bottle 說明文件]: http://bottlepy.org/docs/dev/index.html

