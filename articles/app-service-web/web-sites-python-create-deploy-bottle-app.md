---
title: "在 Azure 中使用 Bottle 建立 Python Web 應用程式"
description: "介紹在 Azure App Service Web Apps 中執行 Python Web 應用程式的教學課程。"
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
ms.openlocfilehash: de5831defc395cd8a4033be8c1fc5dc6cbc9d683
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="creating-web-apps-with-bottle-in-azure"></a><span data-ttu-id="05cde-103">在 Azure 中使用 Bottle 建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="05cde-103">Creating web apps with Bottle in Azure</span></span>
<span data-ttu-id="05cde-104">本教學課程說明如何在 Azure App Service Web Apps 上開始執行 Python。</span><span class="sxs-lookup"><span data-stu-id="05cde-104">This tutorial describes how to get started running Python in Azure App Service Web Apps.</span></span> <span data-ttu-id="05cde-105">Web Apps 提供有限的免費裝載和快速部署，而您可以使用 Python！</span><span class="sxs-lookup"><span data-stu-id="05cde-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="05cde-106">隨著應用程式規模增加，您可以切換為付費主控，也可以與其他所有 Azure 服務整合。</span><span class="sxs-lookup"><span data-stu-id="05cde-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span></span>

<span data-ttu-id="05cde-107">您將使用 Bottle Web 架構建立 Web 應用程式 (請參閱本教學課程的其他版本中有關 [Django](web-sites-python-create-deploy-django-app.md) 和 [Flask](web-sites-python-create-deploy-flask-app.md) 的說明)。</span><span class="sxs-lookup"><span data-stu-id="05cde-107">You will create a web app using the Bottle web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Flask](web-sites-python-create-deploy-flask-app.md)).</span></span> <span data-ttu-id="05cde-108">您會從 Azure Marketplace 建立 Web 應用程式、設定 Git 部署，並於本機複製儲存機制。</span><span class="sxs-lookup"><span data-stu-id="05cde-108">You will create the web app from the Azure Marketplace, set up Git deployment, and clone the repository locally.</span></span> <span data-ttu-id="05cde-109">接著您將在本機執行 Web 應用程式、進行變更、認可及推送至 [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714)。</span><span class="sxs-lookup"><span data-stu-id="05cde-109">Then you will run the web app locally, make changes, commit and push them to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="05cde-110">本教學課程示範如何從 Windows 或 Mac/Linux 執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="05cde-110">The tutorial shows how to do this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="05cde-111">如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service](https://azure.microsoft.com/try/app-service/)，即可在 App Service 中立即建立短期入門 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="05cde-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="05cde-112">不需要信用卡；無需承諾。</span><span class="sxs-lookup"><span data-stu-id="05cde-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="05cde-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="05cde-113">Prerequisites</span></span>
* <span data-ttu-id="05cde-114">Windows、Mac 或 Linux</span><span class="sxs-lookup"><span data-stu-id="05cde-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="05cde-115">Python 2.7 或 3.4</span><span class="sxs-lookup"><span data-stu-id="05cde-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="05cde-116">setuptools、pip、virtualenv (僅 Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="05cde-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="05cde-117">Git</span><span class="sxs-lookup"><span data-stu-id="05cde-117">Git</span></span>
* <span data-ttu-id="05cde-118">[Python Tools 2.2 for Visual Studio][Python Tools 2.2 for Visual Studio] (PTVS) - 注意：這是選擇性的</span><span class="sxs-lookup"><span data-stu-id="05cde-118">[Python Tools 2.2 for Visual Studio][Python Tools 2.2 for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="05cde-119">**注意**：Python 專案目前不支援 TFS 發佈。</span><span class="sxs-lookup"><span data-stu-id="05cde-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="05cde-120">Windows</span><span class="sxs-lookup"><span data-stu-id="05cde-120">Windows</span></span>
<span data-ttu-id="05cde-121">如果您還沒有安裝 Python 2.7 或 3.4 (32 位元)，建議您使用 Web Platform Installer 安裝 [Azure SDK for Python 2.7] 或 [Azure SDK for Python 3.4]。</span><span class="sxs-lookup"><span data-stu-id="05cde-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="05cde-122">這會安裝 32 位元版本的 Python、setuptools、pip、virtualenv 等 (32 位元 Python 安裝於 Azure 主機電腦上)。</span><span class="sxs-lookup"><span data-stu-id="05cde-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span></span> <span data-ttu-id="05cde-123">或者，您可以從 [python.org]取得 Python。</span><span class="sxs-lookup"><span data-stu-id="05cde-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="05cde-124">針對 Git，建議您安裝 [Git for Windows] 或 [GitHub for Windows]。</span><span class="sxs-lookup"><span data-stu-id="05cde-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="05cde-125">如果您使用 Visual Studio，您可以使用整合式的 Git 支援。</span><span class="sxs-lookup"><span data-stu-id="05cde-125">If you use Visual Studio, you can use the integrated Git support.</span></span>

<span data-ttu-id="05cde-126">我們也建議您安裝 [Python Tools 2.2 for Visual Studio]。</span><span class="sxs-lookup"><span data-stu-id="05cde-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="05cde-127">這是選擇性的，但如果您有 [Visual Studio](包含免費的 Visual Studio Community 2013 或 Visual Studio Express 2013 for Web)，它會提供您絕佳的 Python IDE。</span><span class="sxs-lookup"><span data-stu-id="05cde-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="05cde-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="05cde-128">Mac/Linux</span></span>
<span data-ttu-id="05cde-129">您應該已經安裝 Python 與 Git，但請確定您擁有的是 Python 2.7 或 3.4。</span><span class="sxs-lookup"><span data-stu-id="05cde-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-the-azure-portal"></a><span data-ttu-id="05cde-130">在 Azure 入口網站上建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="05cde-130">Web app creation on the Azure Portal</span></span>
<span data-ttu-id="05cde-131">建立應用程式的第一步是透過 [Azure 入口網站](https://portal.azure.com)建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="05cde-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span></span>  

1. <span data-ttu-id="05cde-132">登入 Azure 入口網站中，並按一下左下角的 [新增]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="05cde-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span></span> 
2. <span data-ttu-id="05cde-133">在搜尋方塊中，輸入 "python"。</span><span class="sxs-lookup"><span data-stu-id="05cde-133">In the search box, type "python".</span></span>
3. <span data-ttu-id="05cde-134">在搜尋結果中，選取 [Bottle]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="05cde-134">In the search results, select **Bottle**, then click **Create**.</span></span>
4. <span data-ttu-id="05cde-135">設定新的 Bottle 應用程式，例如為其建立新的 App Service 方案和新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="05cde-135">Configure the new Bottle app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="05cde-136">然後按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="05cde-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="05cde-137">依照 [本機 Git 部署至 Azure App Service](app-service-deploy-local-git.md)的指示，為您新建立的 Web 應用程式設定 Git 發佈功能。</span><span class="sxs-lookup"><span data-stu-id="05cde-137">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="05cde-138">應用程式概觀</span><span class="sxs-lookup"><span data-stu-id="05cde-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="05cde-139">Git 儲存機制內容</span><span class="sxs-lookup"><span data-stu-id="05cde-139">Git repository contents</span></span>
<span data-ttu-id="05cde-140">以下是您會在初始的 Git 儲存機制中找到的檔案概觀，我們將在下一節中複製。</span><span class="sxs-lookup"><span data-stu-id="05cde-140">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span></span>

    \routes.py
    \static\content\
    \static\fonts\
    \static\scripts\
    \views\about.tpl
    \views\contact.tpl
    \views\index.tpl
    \views\layout.tpl

<span data-ttu-id="05cde-141">應用程式的主要來源。</span><span class="sxs-lookup"><span data-stu-id="05cde-141">Main sources for the application.</span></span> <span data-ttu-id="05cde-142">包含 3 個主要的版面配置頁面 (index、about、contact)。</span><span class="sxs-lookup"><span data-stu-id="05cde-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="05cde-143">靜態內容和指令碼，包含啟動程序、jquery、modernizr 和回應。</span><span class="sxs-lookup"><span data-stu-id="05cde-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \app.py

<span data-ttu-id="05cde-144">本機開發伺服器支援。</span><span class="sxs-lookup"><span data-stu-id="05cde-144">Local development server support.</span></span> <span data-ttu-id="05cde-145">使用此項在本機執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="05cde-145">Use this to run the application locally.</span></span>

    \BottleWebProject.pyproj
    \BottleWebProject.sln

<span data-ttu-id="05cde-146">搭配 [Python Tools for Visual Studio]使用的專案檔。</span><span class="sxs-lookup"><span data-stu-id="05cde-146">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="05cde-147">虛擬環境和 PTVS 遠端偵錯支援的 IIS Proxy。</span><span class="sxs-lookup"><span data-stu-id="05cde-147">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="05cde-148">此應用程式所需的外部封裝。</span><span class="sxs-lookup"><span data-stu-id="05cde-148">External packages needed by this application.</span></span> <span data-ttu-id="05cde-149">部署指令碼將 pip 安裝在這個檔案中所列的封裝。</span><span class="sxs-lookup"><span data-stu-id="05cde-149">The deployment script will pip install the packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="05cde-150">IIS 組態檔。</span><span class="sxs-lookup"><span data-stu-id="05cde-150">IIS configuration files.</span></span> <span data-ttu-id="05cde-151">部署指令碼會使用適當的 web.x.y.config，並將它複製為 web.config。</span><span class="sxs-lookup"><span data-stu-id="05cde-151">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="05cde-152">選用的檔案 - 自訂部署</span><span class="sxs-lookup"><span data-stu-id="05cde-152">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="05cde-153">選用的檔案 - Python 執行階段</span><span class="sxs-lookup"><span data-stu-id="05cde-153">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="05cde-154">在伺服器上的其他檔案</span><span class="sxs-lookup"><span data-stu-id="05cde-154">Additional files on server</span></span>
<span data-ttu-id="05cde-155">某些檔案存在於伺服器上，但未加入至 Git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="05cde-155">Some files exist on the server but are not added to the git repository.</span></span> <span data-ttu-id="05cde-156">這些檔案由部署指令碼建立。</span><span class="sxs-lookup"><span data-stu-id="05cde-156">These are created by the deployment script.</span></span>

    \web.config

<span data-ttu-id="05cde-157">IIS 組態檔。</span><span class="sxs-lookup"><span data-stu-id="05cde-157">IIS configuration file.</span></span> <span data-ttu-id="05cde-158">從 web.x.y.config 建立於每個部署上。</span><span class="sxs-lookup"><span data-stu-id="05cde-158">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="05cde-159">Python 虛擬環境。</span><span class="sxs-lookup"><span data-stu-id="05cde-159">Python virtual environment.</span></span> <span data-ttu-id="05cde-160">如果 Web 應用程式上不存在相容的虛擬環境，會於部署期間建立。</span><span class="sxs-lookup"><span data-stu-id="05cde-160">Created during deployment if a compatible virtual environment doesn't already exist on the web app.</span></span>  <span data-ttu-id="05cde-161">requirements.txt 中所列封裝為 pip 安裝，但是如果封裝已安裝，pip 會跳過安裝。</span><span class="sxs-lookup"><span data-stu-id="05cde-161">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span></span>

<span data-ttu-id="05cde-162">接下來的 3 小節會說明如何在 3 個不同環境中繼續進行 Web 應用程式開發：</span><span class="sxs-lookup"><span data-stu-id="05cde-162">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span></span>

* <span data-ttu-id="05cde-163">Windows，使用 Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="05cde-163">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="05cde-164">Windows，使用命令列</span><span class="sxs-lookup"><span data-stu-id="05cde-164">Windows, with command line</span></span>
* <span data-ttu-id="05cde-165">Mac/Linux，使用命令列</span><span class="sxs-lookup"><span data-stu-id="05cde-165">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="05cde-166">Web 應用程式開發 - Windows - 適用於 Visual Studio 的 Python 工具</span><span class="sxs-lookup"><span data-stu-id="05cde-166">Web App development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="05cde-167">複製儲存機制</span><span class="sxs-lookup"><span data-stu-id="05cde-167">Clone the repository</span></span>
<span data-ttu-id="05cde-168">首先，使用 Azure 入口網站上提供的 URL 複製儲存機制。</span><span class="sxs-lookup"><span data-stu-id="05cde-168">First, clone the repository using the url provided on the Azure Portal.</span></span> <span data-ttu-id="05cde-169">如需詳細資訊，請參閱 [本機 Git 部署至 Azure App Service](app-service-deploy-local-git.md)。</span><span class="sxs-lookup"><span data-stu-id="05cde-169">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="05cde-170">開啟包含在儲存機制根目錄中的方案檔 (.sln)。</span><span class="sxs-lookup"><span data-stu-id="05cde-170">Open the solution file (.sln) that is included in the root of the repository.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-solution-bottle.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="05cde-171">建立虛擬環境</span><span class="sxs-lookup"><span data-stu-id="05cde-171">Create virtual environment</span></span>
<span data-ttu-id="05cde-172">現在我們要建立本機開發的虛擬環境。</span><span class="sxs-lookup"><span data-stu-id="05cde-172">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="05cde-173">以滑鼠右鍵按一下 [Python 環境]，選取 [新增虛擬環境...]。</span><span class="sxs-lookup"><span data-stu-id="05cde-173">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="05cde-174">請確定環境的名稱是 `env`。</span><span class="sxs-lookup"><span data-stu-id="05cde-174">Make sure the name of the environment is `env`.</span></span>
* <span data-ttu-id="05cde-175">選取基礎解譯器。</span><span class="sxs-lookup"><span data-stu-id="05cde-175">Select the base interpreter.</span></span> <span data-ttu-id="05cde-176">確認使用針對您 Web 應用程式選取的 Python 版本 (在 runtime.txt 中，或在 Azure 入口網站中您的 Web 應用程式的 [應用程式設定]  分頁中) 相同的版本。</span><span class="sxs-lookup"><span data-stu-id="05cde-176">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>
* <span data-ttu-id="05cde-177">確定已勾選下載並安裝封裝的選項。</span><span class="sxs-lookup"><span data-stu-id="05cde-177">Make sure the option to download and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="05cde-178">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="05cde-178">Click **Create**.</span></span> <span data-ttu-id="05cde-179">這會建立虛擬環境，並安裝 requirements.txt 中列出的相依性。</span><span class="sxs-lookup"><span data-stu-id="05cde-179">This will create the virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="05cde-180">使用開發伺服器來執行</span><span class="sxs-lookup"><span data-stu-id="05cde-180">Run using development server</span></span>
<span data-ttu-id="05cde-181">按 F5 開始偵錯，並且網頁瀏覽器會自動開啟在本機執行的頁面。</span><span class="sxs-lookup"><span data-stu-id="05cde-181">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

<span data-ttu-id="05cde-182">您可以在來源中設定中斷點、使用監看式視窗等等。如需各種功能的詳細資訊，請參閱 [Python Tools for Visual Studio 文件]。</span><span class="sxs-lookup"><span data-stu-id="05cde-182">You can set breakpoints in the sources, use the watch windows, etc. See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="05cde-183">進行變更</span><span class="sxs-lookup"><span data-stu-id="05cde-183">Make changes</span></span>
<span data-ttu-id="05cde-184">現在您可以嘗試對應用程式來源和/或範本進行變更。</span><span class="sxs-lookup"><span data-stu-id="05cde-184">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="05cde-185">測試過您的變更之後，請將它們認可至 Git 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="05cde-185">After you've tested your changes, commit them to the Git repository:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-commit-bottle.png)

### <a name="install-more-packages"></a><span data-ttu-id="05cde-186">安裝更多封裝</span><span class="sxs-lookup"><span data-stu-id="05cde-186">Install more packages</span></span>
<span data-ttu-id="05cde-187">您的應用程式可能會擁有 Python 和 Bottle 之外的相依性。</span><span class="sxs-lookup"><span data-stu-id="05cde-187">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="05cde-188">您可以使用 pip 安裝其他封裝。</span><span class="sxs-lookup"><span data-stu-id="05cde-188">You can install additional packages using pip.</span></span> <span data-ttu-id="05cde-189">若要安裝封裝，以滑鼠右鍵按一下虛擬環境，然後選取 [安裝 Python 封裝] 。</span><span class="sxs-lookup"><span data-stu-id="05cde-189">To install a package, right-click on the virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="05cde-190">例如，若要安裝 Azure SDK for Python，讓您可存取 Azure 儲存體、服務匯流排和其他 Azure 服務，請輸入 `azure`：</span><span class="sxs-lookup"><span data-stu-id="05cde-190">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-install-package-dialog.png)

<span data-ttu-id="05cde-191">以滑鼠右鍵按一下虛擬環境，然後選取 [產生 requirements.txt]  更新 requirements.txt。</span><span class="sxs-lookup"><span data-stu-id="05cde-191">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span></span>

<span data-ttu-id="05cde-192">然後，將變更認可到 Git 儲存機制的 requirements.txt。</span><span class="sxs-lookup"><span data-stu-id="05cde-192">Then, commit the changes to requirements.txt to the Git repository.</span></span>

### <a name="deploy-to-azure"></a><span data-ttu-id="05cde-193">部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="05cde-193">Deploy to Azure</span></span>
<span data-ttu-id="05cde-194">若要觸發部署，按一下 [同步] 或 [推送]。</span><span class="sxs-lookup"><span data-stu-id="05cde-194">To trigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="05cde-195">同步處理會推送和提取。</span><span class="sxs-lookup"><span data-stu-id="05cde-195">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-git-push.png)

<span data-ttu-id="05cde-196">第一次部署將需要一些時間，因為它會建立虛擬環境、安裝封裝等。</span><span class="sxs-lookup"><span data-stu-id="05cde-196">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="05cde-197">Visual Studio 不會顯示部署進度。</span><span class="sxs-lookup"><span data-stu-id="05cde-197">Visual Studio doesn't show the progress of the deployment.</span></span> <span data-ttu-id="05cde-198">如果您想要檢閱輸出，請參閱 [疑難排解 - 部署](#troubleshooting-deployment)一節。</span><span class="sxs-lookup"><span data-stu-id="05cde-198">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="05cde-199">瀏覽至 Azure URL，以檢視您的變更。</span><span class="sxs-lookup"><span data-stu-id="05cde-199">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="05cde-200">Web 應用程式開發 - Windows - 命令列</span><span class="sxs-lookup"><span data-stu-id="05cde-200">Web app development - Windows - Command Line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="05cde-201">複製儲存機制</span><span class="sxs-lookup"><span data-stu-id="05cde-201">Clone the repository</span></span>
<span data-ttu-id="05cde-202">首先，使用 Azure 入口網站上提供的 URL 複製儲存機制，並將 Azure 儲存機制加入為遠端。</span><span class="sxs-lookup"><span data-stu-id="05cde-202">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="05cde-203">如需詳細資訊，請參閱 [本機 Git 部署至 Azure App Service](app-service-deploy-local-git.md)。</span><span class="sxs-lookup"><span data-stu-id="05cde-203">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="05cde-204">建立虛擬環境</span><span class="sxs-lookup"><span data-stu-id="05cde-204">Create virtual environment</span></span>
<span data-ttu-id="05cde-205">我們要建立開發用途的新虛擬環境 (不加入至儲存機制)。</span><span class="sxs-lookup"><span data-stu-id="05cde-205">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="05cde-206">Python 虛擬環境不可重置，因此每位使用該應用程式的開發人員都會在本機建立。</span><span class="sxs-lookup"><span data-stu-id="05cde-206">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="05cde-207">務必使用正確的 Python 版本；應與您為 Web 應用程式所選取的版本相同 (在 runtime.txt 中，或在 Azure 入口網站中您的 Web 應用程式的 [應用程式設定] 刀鋒視窗中) 相同的版本</span><span class="sxs-lookup"><span data-stu-id="05cde-207">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade for your web app in the Azure Portal)</span></span>

<span data-ttu-id="05cde-208">針對 Python 2.7：</span><span class="sxs-lookup"><span data-stu-id="05cde-208">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="05cde-209">針對 Python 3.4：</span><span class="sxs-lookup"><span data-stu-id="05cde-209">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="05cde-210">安裝應用程式所需的任何外部封裝。</span><span class="sxs-lookup"><span data-stu-id="05cde-210">Install any external packages required by your application.</span></span> <span data-ttu-id="05cde-211">您可以在儲存機制的根目錄使用 requirements.txt 檔案，在虛擬環境中安裝封裝：</span><span class="sxs-lookup"><span data-stu-id="05cde-211">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="05cde-212">使用開發伺服器來執行</span><span class="sxs-lookup"><span data-stu-id="05cde-212">Run using development server</span></span>
<span data-ttu-id="05cde-213">您可以使用下列命令，在開發伺服器下啟動應用程式：</span><span class="sxs-lookup"><span data-stu-id="05cde-213">You can launch the application under a development server with the following command:</span></span>

    env\scripts\python app.py

<span data-ttu-id="05cde-214">主控台會顯示 URL，以及伺服器接聽的通訊埠：</span><span class="sxs-lookup"><span data-stu-id="05cde-214">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-run-local-bottle.png)

<span data-ttu-id="05cde-215">然後，開啟網頁瀏覽器指向該 URL。</span><span class="sxs-lookup"><span data-stu-id="05cde-215">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="05cde-216">進行變更</span><span class="sxs-lookup"><span data-stu-id="05cde-216">Make changes</span></span>
<span data-ttu-id="05cde-217">現在您可以嘗試對應用程式來源和/或範本進行變更。</span><span class="sxs-lookup"><span data-stu-id="05cde-217">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="05cde-218">測試過您的變更之後，請將它們認可至 Git 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="05cde-218">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="05cde-219">安裝更多封裝</span><span class="sxs-lookup"><span data-stu-id="05cde-219">Install more packages</span></span>
<span data-ttu-id="05cde-220">您的應用程式可能會擁有 Python 和 Bottle 之外的相依性。</span><span class="sxs-lookup"><span data-stu-id="05cde-220">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="05cde-221">您可以使用 pip 安裝其他封裝。</span><span class="sxs-lookup"><span data-stu-id="05cde-221">You can install additional packages using pip.</span></span> <span data-ttu-id="05cde-222">例如，若要安裝 Azure SDK for Python，讓您可存取 Azure 儲存體、服務匯流排和其他 Azure 服務，請輸入：</span><span class="sxs-lookup"><span data-stu-id="05cde-222">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="05cde-223">請務必更新 requirements.txt：</span><span class="sxs-lookup"><span data-stu-id="05cde-223">Make sure to update requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="05cde-224">認可變更：</span><span class="sxs-lookup"><span data-stu-id="05cde-224">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="05cde-225">部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="05cde-225">Deploy to Azure</span></span>
<span data-ttu-id="05cde-226">若要觸發部署，將變更推送至 Azure：</span><span class="sxs-lookup"><span data-stu-id="05cde-226">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="05cde-227">您會看到部署指令碼的輸出，包括虛擬環境建立、安裝封裝、建立 web.config。</span><span class="sxs-lookup"><span data-stu-id="05cde-227">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="05cde-228">瀏覽至 Azure URL，以檢視您的變更。</span><span class="sxs-lookup"><span data-stu-id="05cde-228">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="05cde-229">Web 應用程式開發 - Mac/Linux - 命令列</span><span class="sxs-lookup"><span data-stu-id="05cde-229">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="05cde-230">複製儲存機制</span><span class="sxs-lookup"><span data-stu-id="05cde-230">Clone the repository</span></span>
<span data-ttu-id="05cde-231">首先，使用 Azure 入口網站上提供的 URL 複製儲存機制，並將 Azure 儲存機制加入為遠端。</span><span class="sxs-lookup"><span data-stu-id="05cde-231">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="05cde-232">如需詳細資訊，請參閱 [本機 Git 部署至 Azure App Service](app-service-deploy-local-git.md)。</span><span class="sxs-lookup"><span data-stu-id="05cde-232">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="05cde-233">建立虛擬環境</span><span class="sxs-lookup"><span data-stu-id="05cde-233">Create virtual environment</span></span>
<span data-ttu-id="05cde-234">我們要建立開發用途的新虛擬環境 (不加入至儲存機制)。</span><span class="sxs-lookup"><span data-stu-id="05cde-234">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="05cde-235">Python 虛擬環境不可重置，因此每位使用該應用程式的開發人員都會在本機建立。</span><span class="sxs-lookup"><span data-stu-id="05cde-235">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="05cde-236">務必使用正確的 Python 版本；應與您為 Web 應用程式所選取的版本相同 (在 runtime.txt 中，或在 Azure 入口網站中您的 Web 應用程式的 [應用程式設定] 刀鋒視窗中) 相同的版本。</span><span class="sxs-lookup"><span data-stu-id="05cde-236">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="05cde-237">針對 Python 2.7：</span><span class="sxs-lookup"><span data-stu-id="05cde-237">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="05cde-238">針對 Python 3.4：</span><span class="sxs-lookup"><span data-stu-id="05cde-238">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="05cde-239">或 pyvenv env</span><span class="sxs-lookup"><span data-stu-id="05cde-239">or pyvenv env</span></span>

<span data-ttu-id="05cde-240">安裝應用程式所需的任何外部封裝。</span><span class="sxs-lookup"><span data-stu-id="05cde-240">Install any external packages required by your application.</span></span> <span data-ttu-id="05cde-241">您可以在儲存機制的根目錄使用 requirements.txt 檔案，在虛擬環境中安裝封裝：</span><span class="sxs-lookup"><span data-stu-id="05cde-241">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="05cde-242">使用開發伺服器來執行</span><span class="sxs-lookup"><span data-stu-id="05cde-242">Run using development server</span></span>
<span data-ttu-id="05cde-243">您可以使用下列命令，在開發伺服器下啟動應用程式：</span><span class="sxs-lookup"><span data-stu-id="05cde-243">You can launch the application under a development server with the following command:</span></span>

    env/bin/python app.py

<span data-ttu-id="05cde-244">主控台會顯示 URL，以及伺服器接聽的通訊埠：</span><span class="sxs-lookup"><span data-stu-id="05cde-244">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-run-local-bottle.png)

<span data-ttu-id="05cde-245">然後，開啟網頁瀏覽器指向該 URL。</span><span class="sxs-lookup"><span data-stu-id="05cde-245">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="05cde-246">進行變更</span><span class="sxs-lookup"><span data-stu-id="05cde-246">Make changes</span></span>
<span data-ttu-id="05cde-247">現在您可以嘗試對應用程式來源和/或範本進行變更。</span><span class="sxs-lookup"><span data-stu-id="05cde-247">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="05cde-248">測試過您的變更之後，請將它們認可至 Git 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="05cde-248">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="05cde-249">安裝更多封裝</span><span class="sxs-lookup"><span data-stu-id="05cde-249">Install more packages</span></span>
<span data-ttu-id="05cde-250">您的應用程式可能會擁有 Python 和 Bottle 之外的相依性。</span><span class="sxs-lookup"><span data-stu-id="05cde-250">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="05cde-251">您可以使用 pip 安裝其他封裝。</span><span class="sxs-lookup"><span data-stu-id="05cde-251">You can install additional packages using pip.</span></span> <span data-ttu-id="05cde-252">例如，若要安裝 Azure SDK for Python，讓您可存取 Azure 儲存體、服務匯流排和其他 Azure 服務，請輸入：</span><span class="sxs-lookup"><span data-stu-id="05cde-252">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="05cde-253">請務必更新 requirements.txt：</span><span class="sxs-lookup"><span data-stu-id="05cde-253">Make sure to update requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="05cde-254">認可變更：</span><span class="sxs-lookup"><span data-stu-id="05cde-254">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="05cde-255">部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="05cde-255">Deploy to Azure</span></span>
<span data-ttu-id="05cde-256">若要觸發部署，將變更推送至 Azure：</span><span class="sxs-lookup"><span data-stu-id="05cde-256">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="05cde-257">您會看到部署指令碼的輸出，包括虛擬環境建立、安裝封裝、建立 web.config。</span><span class="sxs-lookup"><span data-stu-id="05cde-257">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="05cde-258">瀏覽至 Azure URL，以檢視您的變更。</span><span class="sxs-lookup"><span data-stu-id="05cde-258">Browse to the Azure URL to view your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="05cde-259">疑難排解 - 封裝安裝</span><span class="sxs-lookup"><span data-stu-id="05cde-259">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="05cde-260">疑難排解 - 虛擬環境</span><span class="sxs-lookup"><span data-stu-id="05cde-260">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="05cde-261">後續步驟</span><span class="sxs-lookup"><span data-stu-id="05cde-261">Next Steps</span></span>
<span data-ttu-id="05cde-262">請遵循下列連結以深入了解 Bottle 和 Python Tools for Visual Studio：</span><span class="sxs-lookup"><span data-stu-id="05cde-262">Follow these links to learn more about Bottle and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="05cde-263">[Bottle 說明文件]</span><span class="sxs-lookup"><span data-stu-id="05cde-263">[Bottle Documentation]</span></span>
* <span data-ttu-id="05cde-264">[Python Tools for Visual Studio 文件]</span><span class="sxs-lookup"><span data-stu-id="05cde-264">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="05cde-265">如需有關使用 Azure 資料表儲存體和 MongoDB 的資訊：</span><span class="sxs-lookup"><span data-stu-id="05cde-265">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="05cde-266">[Azure 上使用 Python Tools for Visual Studio 的 Bottle 和 MongoDB]</span><span class="sxs-lookup"><span data-stu-id="05cde-266">[Bottle and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="05cde-267">[Azure 上使用 Python Tools for Visual Studio 的 Bottle 和 Azure 資料表儲存體]</span><span class="sxs-lookup"><span data-stu-id="05cde-267">[Bottle and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="05cde-268">變更的項目</span><span class="sxs-lookup"><span data-stu-id="05cde-268">What's changed</span></span>
* <span data-ttu-id="05cde-269">如需從網站變更為 App Service 的指南，請參閱： [Azure App Service 及其對現有 Azure 服務的影響](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="05cde-269">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
<span data-ttu-id="05cde-270">[Azure 上使用 Python Tools for Visual Studio 的 Bottle 和 MongoDB]: web-sites-python-ptvs-bottle-table-storage.md</span><span class="sxs-lookup"><span data-stu-id="05cde-270">[Bottle and MongoDB on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span></span>
<span data-ttu-id="05cde-271">[Azure 上使用 Python Tools for Visual Studio 的 Bottle 和 Azure 資料表儲存體]: web-sites-python-ptvs-bottle-table-storage.md</span><span class="sxs-lookup"><span data-stu-id="05cde-271">[Bottle and Azure Table Storage on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span></span>

<!--External Link references-->
<span data-ttu-id="05cde-272">[Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span><span class="sxs-lookup"><span data-stu-id="05cde-272">[Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span></span>
<span data-ttu-id="05cde-273">[Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span><span class="sxs-lookup"><span data-stu-id="05cde-273">[Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span></span>
<span data-ttu-id="05cde-274">[python.org]: http://www.python.org/</span><span class="sxs-lookup"><span data-stu-id="05cde-274">[python.org]: http://www.python.org/</span></span>
<span data-ttu-id="05cde-275">[Git for Windows]: http://msysgit.github.io/</span><span class="sxs-lookup"><span data-stu-id="05cde-275">[Git for Windows]: http://msysgit.github.io/</span></span>
<span data-ttu-id="05cde-276">[GitHub for Windows]: https://windows.github.com/</span><span class="sxs-lookup"><span data-stu-id="05cde-276">[GitHub for Windows]: https://windows.github.com/</span></span>
<span data-ttu-id="05cde-277">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span><span class="sxs-lookup"><span data-stu-id="05cde-277">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span></span>
<span data-ttu-id="05cde-278">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="05cde-278">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="05cde-279">[Visual Studio]: http://www.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="05cde-279">[Visual Studio]: http://www.visualstudio.com/</span></span>
<span data-ttu-id="05cde-280">[Python Tools for Visual Studio 文件]: http://aka.ms/ptvsdocs </span><span class="sxs-lookup"><span data-stu-id="05cde-280">[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs </span></span>
<span data-ttu-id="05cde-281">[Bottle 說明文件]: http://bottlepy.org/docs/dev/index.html</span><span class="sxs-lookup"><span data-stu-id="05cde-281">[Bottle Documentation]: http://bottlepy.org/docs/dev/index.html</span></span>

