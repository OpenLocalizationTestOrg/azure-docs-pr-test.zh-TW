---
title: "在 Azure 中使用 Flask 建立 Web 應用程式"
description: "介紹在 Azure 上執行 Python Web 應用程式的教學課程。"
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
ms.openlocfilehash: 29457a39ee3df0bbdbc9869cdce0e14bd85b7302
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="creating-web-apps-with-flask-in-azure"></a><span data-ttu-id="ade3e-103">在 Azure 中使用 Flask 建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="ade3e-103">Creating web apps with Flask in Azure</span></span>
<span data-ttu-id="ade3e-104">本教學課程說明如何在 [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714)上開始執行 Python。</span><span class="sxs-lookup"><span data-stu-id="ade3e-104">This tutorial describes how to get started running Python in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>  <span data-ttu-id="ade3e-105">Web Apps 提供有限的免費裝載和快速部署，而您可以使用 Python！</span><span class="sxs-lookup"><span data-stu-id="ade3e-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span>  <span data-ttu-id="ade3e-106">隨著應用程式規模增加，您可以切換為付費主控，也可以與其他所有 Azure 服務整合。</span><span class="sxs-lookup"><span data-stu-id="ade3e-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span></span>

<span data-ttu-id="ade3e-107">您將使用 Flask Web 架構建立應用程式 (請參閱本教學課程的其他版本 [Django](web-sites-python-create-deploy-django-app.md) 和 [Bottle](web-sites-python-create-deploy-bottle-app.md))。</span><span class="sxs-lookup"><span data-stu-id="ade3e-107">You will create an application using the Flask web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span>  <span data-ttu-id="ade3e-108">您會從 Azure 組件庫建立網站、設定 Git 部署，並於本機複製儲存機制。</span><span class="sxs-lookup"><span data-stu-id="ade3e-108">You will create the website from the Azure gallery, set up Git deployment, and clone the repository locally.</span></span>  <span data-ttu-id="ade3e-109">然後您會在本機執行應用程式、進行變更、認可和推送至 Azure。</span><span class="sxs-lookup"><span data-stu-id="ade3e-109">Then you will run the application locally, make changes, commit and push them to Azure.</span></span>  <span data-ttu-id="ade3e-110">本教學課程示範如何從 Windows 或 Mac/Linux 執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="ade3e-110">The tutorial shows how to do this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="ade3e-111">如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service](https://azure.microsoft.com/try/app-service/)，即可在 App Service 中立即建立短期入門 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ade3e-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="ade3e-112">不需要信用卡；無需承諾。</span><span class="sxs-lookup"><span data-stu-id="ade3e-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="ade3e-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="ade3e-113">Prerequisites</span></span>
* <span data-ttu-id="ade3e-114">Windows、Mac 或 Linux</span><span class="sxs-lookup"><span data-stu-id="ade3e-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="ade3e-115">Python 2.7 或 3.4</span><span class="sxs-lookup"><span data-stu-id="ade3e-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="ade3e-116">setuptools、pip、virtualenv (僅 Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="ade3e-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="ade3e-117">Git</span><span class="sxs-lookup"><span data-stu-id="ade3e-117">Git</span></span>
* <span data-ttu-id="ade3e-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - 注意：這是選擇性的</span><span class="sxs-lookup"><span data-stu-id="ade3e-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="ade3e-119">**注意**：Python 專案目前不支援 TFS 發佈。</span><span class="sxs-lookup"><span data-stu-id="ade3e-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="ade3e-120">Windows</span><span class="sxs-lookup"><span data-stu-id="ade3e-120">Windows</span></span>
<span data-ttu-id="ade3e-121">如果您還沒有安裝 Python 2.7 或 3.4 (32 位元)，建議您使用 Web Platform Installer 安裝 [Azure SDK for Python 2.7] 或 [Azure SDK for Python 3.4]。</span><span class="sxs-lookup"><span data-stu-id="ade3e-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span>  <span data-ttu-id="ade3e-122">這會安裝 32 位元版本的 Python、setuptools、pip、virtualenv 等 (32 位元 Python 安裝於 Azure 主機電腦上)。</span><span class="sxs-lookup"><span data-stu-id="ade3e-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span></span>  <span data-ttu-id="ade3e-123">或者，您可以從 [python.org]取得 Python。</span><span class="sxs-lookup"><span data-stu-id="ade3e-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="ade3e-124">針對 Git，建議您安裝 [Git for Windows] 或 [GitHub for Windows]。</span><span class="sxs-lookup"><span data-stu-id="ade3e-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span>  <span data-ttu-id="ade3e-125">如果您使用 Visual Studio，您可以使用整合式的 Git 支援。</span><span class="sxs-lookup"><span data-stu-id="ade3e-125">If you use Visual Studio, you can use the integrated Git support.</span></span>

<span data-ttu-id="ade3e-126">我們也建議您安裝 [Python Tools 2.2 for Visual Studio]。</span><span class="sxs-lookup"><span data-stu-id="ade3e-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span>  <span data-ttu-id="ade3e-127">這是選擇性的，但如果您有 [Visual Studio](包含免費的 Visual Studio Community 2013 或 Visual Studio Express 2013 for Web)，它會提供您絕佳的 Python IDE。</span><span class="sxs-lookup"><span data-stu-id="ade3e-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="ade3e-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="ade3e-128">Mac/Linux</span></span>
<span data-ttu-id="ade3e-129">您應該已經安裝 Python 與 Git，但請確定您擁有的是 Python 2.7 或 3.4。</span><span class="sxs-lookup"><span data-stu-id="ade3e-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-create-on-the-azure-portal"></a><span data-ttu-id="ade3e-130">在 Azure 入口網站上建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="ade3e-130">Web app create on the Azure Portal</span></span>
<span data-ttu-id="ade3e-131">建立應用程式的第一步是透過 [Azure 入口網站](https://portal.azure.com)建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ade3e-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span></span> 

1. <span data-ttu-id="ade3e-132">登入 Azure 入口網站中，並按一下左下角的 [新增]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="ade3e-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span></span> 
2. <span data-ttu-id="ade3e-133">按一下 [Web + 行動] 。</span><span class="sxs-lookup"><span data-stu-id="ade3e-133">Click **Web + Mobile**.</span></span>
3. <span data-ttu-id="ade3e-134">在搜尋方塊中，輸入 "python"。</span><span class="sxs-lookup"><span data-stu-id="ade3e-134">In the search box, type "python".</span></span>
4. <span data-ttu-id="ade3e-135">在搜尋結果中，選取 [Flask]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="ade3e-135">In the search results, select **Flask**, then click **Create**.</span></span>
5. <span data-ttu-id="ade3e-136">設定新的 Flask 應用程式，例如為它建立新的 App Service 計劃和新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="ade3e-136">Configure the new Flask app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="ade3e-137">然後按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="ade3e-137">Then, click **Create**.</span></span>
6. <span data-ttu-id="ade3e-138">依照 [本機 Git 部署至 Azure App Service](app-service-deploy-local-git.md)的指示，為您新建立的 Web 應用程式設定 Git 發佈功能。</span><span class="sxs-lookup"><span data-stu-id="ade3e-138">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="ade3e-139">應用程式概觀</span><span class="sxs-lookup"><span data-stu-id="ade3e-139">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="ade3e-140">Git 儲存機制內容</span><span class="sxs-lookup"><span data-stu-id="ade3e-140">Git repository contents</span></span>
<span data-ttu-id="ade3e-141">以下是您會在初始的 Git 儲存機制中找到的檔案概觀，我們將在下一節中複製。</span><span class="sxs-lookup"><span data-stu-id="ade3e-141">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span></span>

    \FlaskWebProject\__init__.py
    \FlaskWebProject\views.py
    \FlaskWebProject\static\content\
    \FlaskWebProject\static\fonts\
    \FlaskWebProject\static\scripts\
    \FlaskWebProject\templates\about.html
    \FlaskWebProject\templates\contact.html
    \FlaskWebProject\templates\index.html
    \FlaskWebProject\templates\layout.html

<span data-ttu-id="ade3e-142">應用程式的主要來源。</span><span class="sxs-lookup"><span data-stu-id="ade3e-142">Main sources for the application.</span></span>  <span data-ttu-id="ade3e-143">包含 3 個主要的版面配置頁面 (index、about、contact)。</span><span class="sxs-lookup"><span data-stu-id="ade3e-143">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="ade3e-144">靜態內容和指令碼，包含啟動程序、jquery、modernizr 和回應。</span><span class="sxs-lookup"><span data-stu-id="ade3e-144">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \runserver.py

<span data-ttu-id="ade3e-145">本機開發伺服器支援。</span><span class="sxs-lookup"><span data-stu-id="ade3e-145">Local development server support.</span></span> <span data-ttu-id="ade3e-146">使用此項在本機執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="ade3e-146">Use this to run the application locally.</span></span>

    \FlaskWebProject.pyproj
    \FlaskWebProject.sln

<span data-ttu-id="ade3e-147">搭配 [Python Tools for Visual Studio]使用的專案檔。</span><span class="sxs-lookup"><span data-stu-id="ade3e-147">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="ade3e-148">虛擬環境和 PTVS 遠端偵錯支援的 IIS Proxy。</span><span class="sxs-lookup"><span data-stu-id="ade3e-148">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="ade3e-149">此應用程式所需的外部封裝。</span><span class="sxs-lookup"><span data-stu-id="ade3e-149">External packages needed by this application.</span></span> <span data-ttu-id="ade3e-150">部署指令碼將 pip 安裝在這個檔案中所列的封裝。</span><span class="sxs-lookup"><span data-stu-id="ade3e-150">The deployment script will pip install the packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="ade3e-151">IIS 組態檔。</span><span class="sxs-lookup"><span data-stu-id="ade3e-151">IIS configuration files.</span></span>  <span data-ttu-id="ade3e-152">部署指令碼會使用適當的 web.x.y.config，並將它複製為 web.config。</span><span class="sxs-lookup"><span data-stu-id="ade3e-152">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="ade3e-153">選用的檔案 - 自訂部署</span><span class="sxs-lookup"><span data-stu-id="ade3e-153">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="ade3e-154">選用的檔案 - Python 執行階段</span><span class="sxs-lookup"><span data-stu-id="ade3e-154">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="ade3e-155">在伺服器上的其他檔案</span><span class="sxs-lookup"><span data-stu-id="ade3e-155">Additional files on server</span></span>
<span data-ttu-id="ade3e-156">某些檔案存在於伺服器上，但未加入至 Git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="ade3e-156">Some files exist on the server but are not added to the git repository.</span></span>  <span data-ttu-id="ade3e-157">這些檔案由部署指令碼建立。</span><span class="sxs-lookup"><span data-stu-id="ade3e-157">These are created by the deployment script.</span></span>

    \web.config

<span data-ttu-id="ade3e-158">IIS 組態檔。</span><span class="sxs-lookup"><span data-stu-id="ade3e-158">IIS configuration file.</span></span>  <span data-ttu-id="ade3e-159">從 web.x.y.config 建立於每個部署上。</span><span class="sxs-lookup"><span data-stu-id="ade3e-159">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="ade3e-160">Python 虛擬環境。</span><span class="sxs-lookup"><span data-stu-id="ade3e-160">Python virtual environment.</span></span>  <span data-ttu-id="ade3e-161">如果應用程式上不存在相容的虛擬環境，會於部署期間建立。</span><span class="sxs-lookup"><span data-stu-id="ade3e-161">Created during deployment if a compatible virtual environment doesn't already exist on the app.</span></span>  <span data-ttu-id="ade3e-162">requirements.txt 中所列封裝為 pip 安裝，但是如果封裝已安裝，pip 會跳過安裝。</span><span class="sxs-lookup"><span data-stu-id="ade3e-162">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span></span>

<span data-ttu-id="ade3e-163">接下來的 3 小節會說明如何在 3 個不同環境中繼續進行 Web 應用程式開發：</span><span class="sxs-lookup"><span data-stu-id="ade3e-163">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span></span>

* <span data-ttu-id="ade3e-164">Windows，使用 Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ade3e-164">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="ade3e-165">Windows，使用命令列</span><span class="sxs-lookup"><span data-stu-id="ade3e-165">Windows, with command line</span></span>
* <span data-ttu-id="ade3e-166">Mac/Linux，使用命令列</span><span class="sxs-lookup"><span data-stu-id="ade3e-166">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="ade3e-167">Web 應用程式開發 - Windows - 適用於 Visual Studio 的 Python 工具</span><span class="sxs-lookup"><span data-stu-id="ade3e-167">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="ade3e-168">複製儲存機制</span><span class="sxs-lookup"><span data-stu-id="ade3e-168">Clone the repository</span></span>
<span data-ttu-id="ade3e-169">首先，使用 Azure 入口網站上提供的 URL 複製儲存機制。</span><span class="sxs-lookup"><span data-stu-id="ade3e-169">First, clone the repository using the URL provided on the Azure Portal.</span></span> <span data-ttu-id="ade3e-170">如需詳細資訊，請參閱 [本機 Git 部署至 Azure App Service](app-service-deploy-local-git.md)。</span><span class="sxs-lookup"><span data-stu-id="ade3e-170">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="ade3e-171">開啟包含在儲存機制根目錄中的方案檔 (.sln)。</span><span class="sxs-lookup"><span data-stu-id="ade3e-171">Open the solution file (.sln) that is included in the root of the repository.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-solution-flask.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="ade3e-172">建立虛擬環境</span><span class="sxs-lookup"><span data-stu-id="ade3e-172">Create virtual environment</span></span>
<span data-ttu-id="ade3e-173">現在我們要建立本機開發的虛擬環境。</span><span class="sxs-lookup"><span data-stu-id="ade3e-173">Now we'll create a virtual environment for local development.</span></span>  <span data-ttu-id="ade3e-174">以滑鼠右鍵按一下 [Python 環境]，選取 [新增虛擬環境...]。</span><span class="sxs-lookup"><span data-stu-id="ade3e-174">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="ade3e-175">請確定環境的名稱是 `env`。</span><span class="sxs-lookup"><span data-stu-id="ade3e-175">Make sure the name of the environment is `env`.</span></span>
* <span data-ttu-id="ade3e-176">選取基礎解譯器。</span><span class="sxs-lookup"><span data-stu-id="ade3e-176">Select the base interpreter.</span></span>  <span data-ttu-id="ade3e-177">確認使用針對您 Web 應用程式選取的 Python 版本 (在 runtime.txt 中，或在 Azure 入口網站中您的 Web 應用程式的 [應用程式設定]  分頁中) 相同的版本。</span><span class="sxs-lookup"><span data-stu-id="ade3e-177">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>
* <span data-ttu-id="ade3e-178">確定已勾選下載並安裝封裝的選項。</span><span class="sxs-lookup"><span data-stu-id="ade3e-178">Make sure the option to download and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="ade3e-179">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="ade3e-179">Click **Create**.</span></span>  <span data-ttu-id="ade3e-180">這會建立虛擬環境，並安裝 requirements.txt 中列出的相依性。</span><span class="sxs-lookup"><span data-stu-id="ade3e-180">This will create the virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="ade3e-181">使用開發伺服器來執行</span><span class="sxs-lookup"><span data-stu-id="ade3e-181">Run using development server</span></span>
<span data-ttu-id="ade3e-182">按 F5 開始偵錯，並且網頁瀏覽器會自動開啟在本機執行的頁面。</span><span class="sxs-lookup"><span data-stu-id="ade3e-182">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

<span data-ttu-id="ade3e-183">您可以在來源中設定中斷點、使用監看式視窗等等。如需各種功能的詳細資訊，請參閱 [Python Tools for Visual Studio 文件]。</span><span class="sxs-lookup"><span data-stu-id="ade3e-183">You can set breakpoints in the sources, use the watch windows, etc.  See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="ade3e-184">進行變更</span><span class="sxs-lookup"><span data-stu-id="ade3e-184">Make changes</span></span>
<span data-ttu-id="ade3e-185">現在您可以嘗試對應用程式來源和/或範本進行變更。</span><span class="sxs-lookup"><span data-stu-id="ade3e-185">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="ade3e-186">測試過您的變更之後，請將它們認可至 Git 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="ade3e-186">After you've tested your changes, commit them to the Git repository:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-commit-flask.png)

### <a name="install-more-packages"></a><span data-ttu-id="ade3e-187">安裝更多封裝</span><span class="sxs-lookup"><span data-stu-id="ade3e-187">Install more packages</span></span>
<span data-ttu-id="ade3e-188">您的應用程式可能會擁有 Python 和 Flask 之外的相依性。</span><span class="sxs-lookup"><span data-stu-id="ade3e-188">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="ade3e-189">您可以使用 pip 安裝其他封裝。</span><span class="sxs-lookup"><span data-stu-id="ade3e-189">You can install additional packages using pip.</span></span>  <span data-ttu-id="ade3e-190">若要安裝封裝，以滑鼠右鍵按一下虛擬環境，然後選取 [安裝 Python 封裝] 。</span><span class="sxs-lookup"><span data-stu-id="ade3e-190">To install a package, right-click on the virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="ade3e-191">例如，若要安裝 Azure SDK for Python，讓您可存取 Azure 儲存體、服務匯流排和其他 Azure 服務，請輸入 `azure`：</span><span class="sxs-lookup"><span data-stu-id="ade3e-191">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-install-package-dialog.png)

<span data-ttu-id="ade3e-192">以滑鼠右鍵按一下虛擬環境，然後選取 [產生 requirements.txt]  更新 requirements.txt。</span><span class="sxs-lookup"><span data-stu-id="ade3e-192">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span></span>

<span data-ttu-id="ade3e-193">然後，將變更認可到 Git 儲存機制的 requirements.txt。</span><span class="sxs-lookup"><span data-stu-id="ade3e-193">Then, commit the changes to requirements.txt to the Git repository.</span></span>

### <a name="deploy-to-azure"></a><span data-ttu-id="ade3e-194">部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="ade3e-194">Deploy to Azure</span></span>
<span data-ttu-id="ade3e-195">若要觸發部署，按一下 [同步] 或 [推送]。</span><span class="sxs-lookup"><span data-stu-id="ade3e-195">To trigger a deployment, click on **Sync** or **Push**.</span></span>  <span data-ttu-id="ade3e-196">同步處理會推送和提取。</span><span class="sxs-lookup"><span data-stu-id="ade3e-196">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-git-push.png)

<span data-ttu-id="ade3e-197">第一次部署將需要一些時間，因為它會建立虛擬環境、安裝封裝等。</span><span class="sxs-lookup"><span data-stu-id="ade3e-197">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="ade3e-198">Visual Studio 不會顯示部署進度。</span><span class="sxs-lookup"><span data-stu-id="ade3e-198">Visual Studio doesn't show the progress of the deployment.</span></span>  <span data-ttu-id="ade3e-199">如果您想要檢閱輸出，請參閱 [疑難排解 - 部署](#troubleshooting-deployment)一節。</span><span class="sxs-lookup"><span data-stu-id="ade3e-199">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="ade3e-200">瀏覽至 Azure URL，以檢視您的變更。</span><span class="sxs-lookup"><span data-stu-id="ade3e-200">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="ade3e-201">Web 應用程式開發 - Windows - 命令列</span><span class="sxs-lookup"><span data-stu-id="ade3e-201">Web app development - Windows - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="ade3e-202">複製儲存機制</span><span class="sxs-lookup"><span data-stu-id="ade3e-202">Clone the repository</span></span>
<span data-ttu-id="ade3e-203">首先，使用 Azure 入口網站上提供的 URL 複製儲存機制，並將 Azure 儲存機制加入為遠端。</span><span class="sxs-lookup"><span data-stu-id="ade3e-203">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="ade3e-204">如需詳細資訊，請參閱 [本機 Git 部署至 Azure App Service](app-service-deploy-local-git.md)。</span><span class="sxs-lookup"><span data-stu-id="ade3e-204">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="ade3e-205">建立虛擬環境</span><span class="sxs-lookup"><span data-stu-id="ade3e-205">Create virtual environment</span></span>
<span data-ttu-id="ade3e-206">我們要建立開發用途的新虛擬環境 (不加入至儲存機制)。</span><span class="sxs-lookup"><span data-stu-id="ade3e-206">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span>  <span data-ttu-id="ade3e-207">Python 虛擬環境不可重置，因此每位使用該應用程式的開發人員都會在本機建立。</span><span class="sxs-lookup"><span data-stu-id="ade3e-207">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="ade3e-208">確認使用針對您 Web 應用程式選取的 Python 版本 (在 runtime.txt 中，或在 Azure 入口網站中您的 Web 應用程式的 [應用程式設定]  分頁中) 相同的版本。</span><span class="sxs-lookup"><span data-stu-id="ade3e-208">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="ade3e-209">針對 Python 2.7：</span><span class="sxs-lookup"><span data-stu-id="ade3e-209">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="ade3e-210">針對 Python 3.4：</span><span class="sxs-lookup"><span data-stu-id="ade3e-210">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="ade3e-211">安裝應用程式所需的任何外部封裝。</span><span class="sxs-lookup"><span data-stu-id="ade3e-211">Install any external packages required by your application.</span></span> <span data-ttu-id="ade3e-212">您可以在儲存機制的根目錄使用 requirements.txt 檔案，在虛擬環境中安裝封裝：</span><span class="sxs-lookup"><span data-stu-id="ade3e-212">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="ade3e-213">使用開發伺服器來執行</span><span class="sxs-lookup"><span data-stu-id="ade3e-213">Run using development server</span></span>
<span data-ttu-id="ade3e-214">您可以使用下列命令，在開發伺服器下啟動應用程式：</span><span class="sxs-lookup"><span data-stu-id="ade3e-214">You can launch the application under a development server with the following command:</span></span>

    env\scripts\python runserver.py

<span data-ttu-id="ade3e-215">主控台會顯示 URL，以及伺服器接聽的通訊埠：</span><span class="sxs-lookup"><span data-stu-id="ade3e-215">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-run-local-flask.png)

<span data-ttu-id="ade3e-216">然後，開啟網頁瀏覽器指向該 URL。</span><span class="sxs-lookup"><span data-stu-id="ade3e-216">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="ade3e-217">進行變更</span><span class="sxs-lookup"><span data-stu-id="ade3e-217">Make changes</span></span>
<span data-ttu-id="ade3e-218">現在您可以嘗試對應用程式來源和/或範本進行變更。</span><span class="sxs-lookup"><span data-stu-id="ade3e-218">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="ade3e-219">測試過您的變更之後，請將它們認可至 Git 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="ade3e-219">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="ade3e-220">安裝更多封裝</span><span class="sxs-lookup"><span data-stu-id="ade3e-220">Install more packages</span></span>
<span data-ttu-id="ade3e-221">您的應用程式可能會擁有 Python 和 Flask 之外的相依性。</span><span class="sxs-lookup"><span data-stu-id="ade3e-221">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="ade3e-222">您可以使用 pip 安裝其他封裝。</span><span class="sxs-lookup"><span data-stu-id="ade3e-222">You can install additional packages using pip.</span></span>  <span data-ttu-id="ade3e-223">例如，若要安裝 Azure SDK for Python，讓您可存取 Azure 儲存體、服務匯流排和其他 Azure 服務，請輸入：</span><span class="sxs-lookup"><span data-stu-id="ade3e-223">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="ade3e-224">請務必更新 requirements.txt：</span><span class="sxs-lookup"><span data-stu-id="ade3e-224">Make sure to update requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="ade3e-225">認可變更：</span><span class="sxs-lookup"><span data-stu-id="ade3e-225">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="ade3e-226">部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="ade3e-226">Deploy to Azure</span></span>
<span data-ttu-id="ade3e-227">若要觸發部署，將變更推送至 Azure：</span><span class="sxs-lookup"><span data-stu-id="ade3e-227">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="ade3e-228">您會看到部署指令碼的輸出，包括虛擬環境建立、安裝封裝、建立 web.config。</span><span class="sxs-lookup"><span data-stu-id="ade3e-228">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="ade3e-229">瀏覽至 Azure URL，以檢視您的變更。</span><span class="sxs-lookup"><span data-stu-id="ade3e-229">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="ade3e-230">Web 應用程式開發 - Mac/Linux - 命令列</span><span class="sxs-lookup"><span data-stu-id="ade3e-230">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="ade3e-231">複製儲存機制</span><span class="sxs-lookup"><span data-stu-id="ade3e-231">Clone the repository</span></span>
<span data-ttu-id="ade3e-232">首先，使用 Azure 入口網站上提供的 URL 複製儲存機制，並將 Azure 儲存機制加入為遠端。</span><span class="sxs-lookup"><span data-stu-id="ade3e-232">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="ade3e-233">如需詳細資訊，請參閱 [本機 Git 部署至 Azure App Service](app-service-deploy-local-git.md)。</span><span class="sxs-lookup"><span data-stu-id="ade3e-233">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="ade3e-234">建立虛擬環境</span><span class="sxs-lookup"><span data-stu-id="ade3e-234">Create virtual environment</span></span>
<span data-ttu-id="ade3e-235">我們要建立開發用途的新虛擬環境 (不加入至儲存機制)。</span><span class="sxs-lookup"><span data-stu-id="ade3e-235">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span>  <span data-ttu-id="ade3e-236">Python 虛擬環境不可重置，因此每位使用該應用程式的開發人員都會在本機建立。</span><span class="sxs-lookup"><span data-stu-id="ade3e-236">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="ade3e-237">確認使用針對您 Web 應用程式選取的 Python 版本 (在 runtime.txt 中，或在 Azure 入口網站中您的 Web 應用程式的 [應用程式設定]  分頁中) 相同的版本。</span><span class="sxs-lookup"><span data-stu-id="ade3e-237">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="ade3e-238">針對 Python 2.7：</span><span class="sxs-lookup"><span data-stu-id="ade3e-238">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="ade3e-239">針對 Python 3.4：</span><span class="sxs-lookup"><span data-stu-id="ade3e-239">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="ade3e-240">或 pyvenv env</span><span class="sxs-lookup"><span data-stu-id="ade3e-240">or pyvenv env</span></span>

<span data-ttu-id="ade3e-241">安裝應用程式所需的任何外部封裝。</span><span class="sxs-lookup"><span data-stu-id="ade3e-241">Install any external packages required by your application.</span></span> <span data-ttu-id="ade3e-242">您可以在儲存機制的根目錄使用 requirements.txt 檔案，在虛擬環境中安裝封裝：</span><span class="sxs-lookup"><span data-stu-id="ade3e-242">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="ade3e-243">使用開發伺服器來執行</span><span class="sxs-lookup"><span data-stu-id="ade3e-243">Run using development server</span></span>
<span data-ttu-id="ade3e-244">您可以使用下列命令，在開發伺服器下啟動應用程式：</span><span class="sxs-lookup"><span data-stu-id="ade3e-244">You can launch the application under a development server with the following command:</span></span>

    env/bin/python runserver.py

<span data-ttu-id="ade3e-245">主控台會顯示 URL，以及伺服器接聽的通訊埠：</span><span class="sxs-lookup"><span data-stu-id="ade3e-245">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-run-local-flask.png)

<span data-ttu-id="ade3e-246">然後，開啟網頁瀏覽器指向該 URL。</span><span class="sxs-lookup"><span data-stu-id="ade3e-246">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="ade3e-247">進行變更</span><span class="sxs-lookup"><span data-stu-id="ade3e-247">Make changes</span></span>
<span data-ttu-id="ade3e-248">現在您可以嘗試對應用程式來源和/或範本進行變更。</span><span class="sxs-lookup"><span data-stu-id="ade3e-248">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="ade3e-249">測試過您的變更之後，請將它們認可至 Git 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="ade3e-249">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="ade3e-250">安裝更多封裝</span><span class="sxs-lookup"><span data-stu-id="ade3e-250">Install more packages</span></span>
<span data-ttu-id="ade3e-251">您的應用程式可能會擁有 Python 和 Flask 之外的相依性。</span><span class="sxs-lookup"><span data-stu-id="ade3e-251">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="ade3e-252">您可以使用 pip 安裝其他封裝。</span><span class="sxs-lookup"><span data-stu-id="ade3e-252">You can install additional packages using pip.</span></span>  <span data-ttu-id="ade3e-253">例如，若要安裝 Azure SDK for Python，讓您可存取 Azure 儲存體、服務匯流排和其他 Azure 服務，請輸入：</span><span class="sxs-lookup"><span data-stu-id="ade3e-253">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="ade3e-254">請務必更新 requirements.txt：</span><span class="sxs-lookup"><span data-stu-id="ade3e-254">Make sure to update requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="ade3e-255">認可變更：</span><span class="sxs-lookup"><span data-stu-id="ade3e-255">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="ade3e-256">部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="ade3e-256">Deploy to Azure</span></span>
<span data-ttu-id="ade3e-257">若要觸發部署，將變更推送至 Azure：</span><span class="sxs-lookup"><span data-stu-id="ade3e-257">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="ade3e-258">您會看到部署指令碼的輸出，包括虛擬環境建立、安裝封裝、建立 web.config。</span><span class="sxs-lookup"><span data-stu-id="ade3e-258">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="ade3e-259">瀏覽至 Azure URL，以檢視您的變更。</span><span class="sxs-lookup"><span data-stu-id="ade3e-259">Browse to the Azure URL to view your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="ade3e-260">疑難排解 - 封裝安裝</span><span class="sxs-lookup"><span data-stu-id="ade3e-260">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="ade3e-261">疑難排解 - 虛擬環境</span><span class="sxs-lookup"><span data-stu-id="ade3e-261">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="ade3e-262">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ade3e-262">Next Steps</span></span>
<span data-ttu-id="ade3e-263">請遵循下列連結以深入了解 Flask 和 Python Tools for Visual Studio：</span><span class="sxs-lookup"><span data-stu-id="ade3e-263">Follow these links to learn more about Flask and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="ade3e-264">[Flask 說明文件 英文]</span><span class="sxs-lookup"><span data-stu-id="ade3e-264">[Flask Documentation]</span></span>
* <span data-ttu-id="ade3e-265">[Python Tools for Visual Studio 文件]</span><span class="sxs-lookup"><span data-stu-id="ade3e-265">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="ade3e-266">如需有關使用 Azure 資料表儲存體和 MongoDB 的資訊：</span><span class="sxs-lookup"><span data-stu-id="ade3e-266">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="ade3e-267">[Azure 上使用 Python Tools for Visual Studio 的 Flask 和 MongoDB]</span><span class="sxs-lookup"><span data-stu-id="ade3e-267">[Flask and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="ade3e-268">[Azure 上使用 Python Tools for Visual Studio 的 Flask 和 Azure 資料表儲存體]</span><span class="sxs-lookup"><span data-stu-id="ade3e-268">[Flask and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="ade3e-269">如需詳細資訊，另請參閱 [Python 開發人員中心](/develop/python/)。</span><span class="sxs-lookup"><span data-stu-id="ade3e-269">For more information, see also the [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="ade3e-270">變更的項目</span><span class="sxs-lookup"><span data-stu-id="ade3e-270">What's changed</span></span>
* <span data-ttu-id="ade3e-271">如需從網站變更為 App Service 的指南，請參閱： [Azure App Service 及其對現有 Azure 服務的影響](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="ade3e-271">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
<span data-ttu-id="ade3e-272">[Azure 上使用 Python Tools for Visual Studio 的 Flask 和 MongoDB]: https://github.com/microsoft/ptvs/wiki/Flask-and-MongoDB-on-Azure</span><span class="sxs-lookup"><span data-stu-id="ade3e-272">[Flask and MongoDB on Azure with Python Tools for Visual Studio]: https://github.com/microsoft/ptvs/wiki/Flask-and-MongoDB-on-Azure</span></span>
<span data-ttu-id="ade3e-273">[Azure 上使用 Python Tools for Visual Studio 的 Flask 和 Azure 資料表儲存體]: web-sites-python-ptvs-flask-table-storage.md</span><span class="sxs-lookup"><span data-stu-id="ade3e-273">[Flask and Azure Table Storage on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-flask-table-storage.md</span></span>

<!--External Link references-->
<span data-ttu-id="ade3e-274">[Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span><span class="sxs-lookup"><span data-stu-id="ade3e-274">[Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span></span>
<span data-ttu-id="ade3e-275">[Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span><span class="sxs-lookup"><span data-stu-id="ade3e-275">[Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span></span>
<span data-ttu-id="ade3e-276">[python.org]: http://www.python.org/</span><span class="sxs-lookup"><span data-stu-id="ade3e-276">[python.org]: http://www.python.org/</span></span>
<span data-ttu-id="ade3e-277">[Git for Windows]: http://msysgit.github.io/</span><span class="sxs-lookup"><span data-stu-id="ade3e-277">[Git for Windows]: http://msysgit.github.io/</span></span>
<span data-ttu-id="ade3e-278">[GitHub for Windows]: https://windows.github.com/</span><span class="sxs-lookup"><span data-stu-id="ade3e-278">[GitHub for Windows]: https://windows.github.com/</span></span>
<span data-ttu-id="ade3e-279">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span><span class="sxs-lookup"><span data-stu-id="ade3e-279">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span></span>
<span data-ttu-id="ade3e-280">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="ade3e-280">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="ade3e-281">[Visual Studio]: http://www.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="ade3e-281">[Visual Studio]: http://www.visualstudio.com/</span></span>
<span data-ttu-id="ade3e-282">[Python Tools for Visual Studio 文件]: http://aka.ms/ptvsdocs</span><span class="sxs-lookup"><span data-stu-id="ade3e-282">[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs</span></span>
<span data-ttu-id="ade3e-283">[Flask 說明文件 英文]: http://flask.pocoo.org/</span><span class="sxs-lookup"><span data-stu-id="ade3e-283">[Flask Documentation]: http://flask.pocoo.org/</span></span> 

