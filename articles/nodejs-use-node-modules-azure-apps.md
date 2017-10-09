---
title: "aaaWorking Node.js 模組"
description: "深入了解如何 toowork Node.js 模組，使用 Azure 應用程式服務或雲端服務時使用。"
services: 
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: c0e6cd3d-932d-433e-b72d-e513e23b4eb6
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 926358b7eb80a659dbc1015686b06a30d8c9b8f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-nodejs-modules-with-azure-applications"></a><span data-ttu-id="4ad88-103">使用 Node.js 模組與 Azure 應用程式搭配</span><span class="sxs-lookup"><span data-stu-id="4ad88-103">Using Node.js Modules with Azure applications</span></span>
<span data-ttu-id="4ad88-104">本文提供有關使用 Node.js 模組與 Azure 上代管之應用程式搭配的指引。</span><span class="sxs-lookup"><span data-stu-id="4ad88-104">This document provides guidance on using Node.js modules with applications hosted on Azure.</span></span> <span data-ttu-id="4ad88-105">它提供有關確保應用程式使用模組特定版本，以及搭配原生模組與 Azure 使用的指引。</span><span class="sxs-lookup"><span data-stu-id="4ad88-105">It provides guidance on ensuring that your application uses a specific version of module as well as using native modules with Azure.</span></span>

<span data-ttu-id="4ad88-106">如果您已經熟悉如何使用 Node.js 模組**package.json**和**npm shrinkwrap.json**檔案 hello 下列資訊提供快速摘要的本文中所討論的內容：</span><span class="sxs-lookup"><span data-stu-id="4ad88-106">If you are already familiar with using Node.js modules, **package.json** and **npm-shrinkwrap.json** files, hello following information provides a quick summary of what is discussed in this article:</span></span>

* <span data-ttu-id="4ad88-107">Azure App Service 熟悉 **package.json** 和 **npm-shrinkwrap.json** 檔案，並可根據這些檔案中的項目安裝模組。</span><span class="sxs-lookup"><span data-stu-id="4ad88-107">Azure App Service understands **package.json** and **npm-shrinkwrap.json** files and can install modules based on entries in these files.</span></span>

* <span data-ttu-id="4ad88-108">Azure 雲端服務預期 hello 開發環境中和 hello 上安裝的所有模組 toobe**節點\_模組**目錄 toobe 納入 hello 部署套件的一部分。</span><span class="sxs-lookup"><span data-stu-id="4ad88-108">Azure Cloud Services expect all modules toobe installed on hello development environment, and hello **node\_modules** directory toobe included as part of hello deployment package.</span></span> <span data-ttu-id="4ad88-109">很可能 tooenable 支援安裝模組使用**package.json**或**npm shrinkwrap.json**檔案在雲端服務; 不過，此設定需要 hello 預設的自訂雲端服務專案所使用的指令碼。</span><span class="sxs-lookup"><span data-stu-id="4ad88-109">It is possible tooenable support for installing modules using **package.json** or **npm-shrinkwrap.json** files on Cloud Services; however, this configuration requires customization of hello default scripts used by Cloud Service projects.</span></span> <span data-ttu-id="4ad88-110">如需如何 tooconfigure 此環境中，請參閱[Azure 啟動工作 toorun npm 安裝 tooavoid 部署節點模組](https://github.com/woloski/nodeonazure-blog/blob/master/articles/startup-task-to-run-npm-in-azure.markdown)</span><span class="sxs-lookup"><span data-stu-id="4ad88-110">For an example of how tooconfigure this environment, see [Azure Startup task toorun npm install tooavoid deploying node modules](https://github.com/woloski/nodeonazure-blog/blob/master/articles/startup-task-to-run-npm-in-azure.markdown)</span></span>

> [!NOTE]
> <span data-ttu-id="4ad88-111">因為在 VM 中的 hello 部署經驗是相依於 hello 虛擬機器所裝載的 hello 作業系統本文中，不會討論 azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4ad88-111">Azure Virtual Machines are not discussed in this article, as hello deployment experience in a VM is dependent on hello operating system hosted by hello Virtual Machine.</span></span>
> 
> 

## <a name="nodejs-modules"></a><span data-ttu-id="4ad88-112">Node.js 模組</span><span class="sxs-lookup"><span data-stu-id="4ad88-112">Node.js Modules</span></span>
<span data-ttu-id="4ad88-113">模組是指可載入的 JavaScript 封裝，可為您的應用程式提供特定功能。</span><span class="sxs-lookup"><span data-stu-id="4ad88-113">Modules are loadable JavaScript packages that provide specific functionality for your application.</span></span> <span data-ttu-id="4ad88-114">模組通常會安裝使用 hello **npm**命令列工具，不過某些模組 （例如 hello http 模組） 會作為 hello 核心 Node.js 封裝的一部分。</span><span class="sxs-lookup"><span data-stu-id="4ad88-114">Modules are usually installed using hello **npm** command-line tool, however some modules (such as hello http module) are provided as part of hello core Node.js package.</span></span>

<span data-ttu-id="4ad88-115">安裝模組之後，它們儲存在 hello**節點\_模組**目錄在 hello 根目錄，您的應用程式目錄結構。</span><span class="sxs-lookup"><span data-stu-id="4ad88-115">When modules are installed, they are stored in hello **node\_modules** directory at hello root of your application directory structure.</span></span> <span data-ttu-id="4ad88-116">Hello 內每個模組**節點\_模組**目錄維護自己**節點\_模組**包含它相依於，而這種行為會重複任何模組的目錄每個模組 hello 相依性鏈結中向下的所有 hello 方式。</span><span class="sxs-lookup"><span data-stu-id="4ad88-116">Each module within hello **node\_modules** directory maintains its own **node\_modules** directory that contains any modules that it depends on, and this behavior repeats for every module all hello way down hello dependency chain.</span></span> <span data-ttu-id="4ad88-117">這個環境可讓每個安裝模組 toohave hello 模組自己版本需求而定，但是它可能會很大的目錄結構。</span><span class="sxs-lookup"><span data-stu-id="4ad88-117">This environment allows each module installed toohave its own version requirements for hello modules it depends on, however it can result in quite a large directory structure.</span></span>

<span data-ttu-id="4ad88-118">部署的 hello**節點\_模組**增加 hello 大小相較的 hello 部署的應用程式的一部分時，目錄 toousing **package.json**或**npm shrinkwrap.json**檔案; 不過，它並保證在生產環境中使用的 hello 模組 hello 版本是 hello 相同做為開發中使用的 hello 模組。</span><span class="sxs-lookup"><span data-stu-id="4ad88-118">Deploying hello **node\_modules** directory as part of your application increases hello size of hello deployment when compared toousing a **package.json** or **npm-shrinkwrap.json** file; however, it does guarantee that hello versions of hello modules used in production are hello same as hello modules used in development.</span></span>

### <a name="native-modules"></a><span data-ttu-id="4ad88-119">原生模組</span><span class="sxs-lookup"><span data-stu-id="4ad88-119">Native Modules</span></span>
<span data-ttu-id="4ad88-120">雖然大多數的模組是簡單的純文字 JavaScript 檔案，有些模組卻是平台特定的二進位影像。</span><span class="sxs-lookup"><span data-stu-id="4ad88-120">While most modules are simply plain-text JavaScript files, some modules are platform-specific binary images.</span></span> <span data-ttu-id="4ad88-121">這些模組會在安裝時編譯，通常是採用 Python 和 node-gyp。</span><span class="sxs-lookup"><span data-stu-id="4ad88-121">These modules are compiled at install time, usually by using Python and node-gyp.</span></span> <span data-ttu-id="4ad88-122">因為 Azure 雲端服務依賴 hello**節點\_模組**資料夾被部署為 hello 應用程式，包含在雲端服務中應該工作 hello 安裝模組的一部分時，只要它是任何原生模組的一部分安裝和編譯的 Windows 開發系統上。</span><span class="sxs-lookup"><span data-stu-id="4ad88-122">Since Azure Cloud Services rely on hello **node\_modules** folder being deployed as part of hello application, any native module included as part of hello installed modules should work in a cloud service as long as it was installed and compiled on a Windows development system.</span></span>

<span data-ttu-id="4ad88-123">Azure App Service 不支援所有的原生模組，而且在編譯具有特定必要元件的模組時，可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="4ad88-123">Azure App Service does not support all native modules, and might fail when compiling modules with specific prerequisites.</span></span> <span data-ttu-id="4ad88-124">雖然某些熱門模組 (如 MongoDB) 具有選擇性原生相依性，而且沒有這些相依性仍照常運作，但兩種因應措施成功證明目前幾乎可使用所有的原生模組：</span><span class="sxs-lookup"><span data-stu-id="4ad88-124">While some popular modules like MongoDB have optional native dependencies and work fine without them, two workarounds proved successful with almost all native modules available today:</span></span>

* <span data-ttu-id="4ad88-125">執行**npm 安裝**已安裝的所有 hello 原生模組的必要元件的 Windows 電腦上。</span><span class="sxs-lookup"><span data-stu-id="4ad88-125">Run **npm install** on a Windows machine that has all hello native module's prerequisites installed.</span></span> <span data-ttu-id="4ad88-126">接著，將部署建立 hello**節點\_模組**資料夾 hello 應用程式 tooAzure 應用程式服務的一部分。</span><span class="sxs-lookup"><span data-stu-id="4ad88-126">Then, deploy hello created **node\_modules** folder as part of hello application tooAzure App Service.</span></span>

  * <span data-ttu-id="4ad88-127">在編譯之前，檢查本機 Node.js 安裝具有相符結構，而且 hello 版本與 Azure 中使用的其中一個可能 toohello (hello 目前的值可以針對從屬性的執行階段檢查**process.arch**和**process.version**)。</span><span class="sxs-lookup"><span data-stu-id="4ad88-127">Before compiling, check that your local Node.js installation has matching architecture and hello version is as close as possible toohello one used in Azure (hello current values can be checked on runtime from properties **process.arch** and **process.version**).</span></span>

* <span data-ttu-id="4ad88-128">Azure App Service 可設定的 tooexecute 自訂 bash，或殼層指令碼，在部署期間，讓您 hello 機會 tooexecute 自訂命令和精確地設定 hello 方式**npm 安裝**正在執行。</span><span class="sxs-lookup"><span data-stu-id="4ad88-128">Azure App Service can be configured tooexecute custom bash or shell scripts during deployment, giving you hello opportunity tooexecute custom commands and precisely configure hello way **npm install** is being run.</span></span> <span data-ttu-id="4ad88-129">為視訊的顯示方式 tooconfigure 該環境中，請參閱[自訂 Kudu 與網站部署指令碼]。</span><span class="sxs-lookup"><span data-stu-id="4ad88-129">For a video showing how tooconfigure that environment, see [Custom Website Deployment Scripts with Kudu].</span></span>

### <a name="using-a-packagejson-file"></a><span data-ttu-id="4ad88-130">使用 package.json 檔案</span><span class="sxs-lookup"><span data-stu-id="4ad88-130">Using a package.json file</span></span>
<span data-ttu-id="4ad88-131">hello **package.json**檔案是方式 toospecify hello 最上層相依性應用程式需要，因此 hello 裝載平台可以安裝 hello 相依性，不需要您 tooinclude hello**節點\_封裝**資料夾 hello 部署的一部分。</span><span class="sxs-lookup"><span data-stu-id="4ad88-131">hello **package.json** file is a way toospecify hello top-level dependencies your application requires so that hello hosting platform can install hello dependencies, rather than requiring you tooinclude hello **node\_packages** folder as part of hello deployment.</span></span> <span data-ttu-id="4ad88-132">Hello 應用程式部署完成之後，hello **npm 安裝**命令是使用的 tooparse hello **package.json**檔案，並安裝所有列出的 hello 相依性。</span><span class="sxs-lookup"><span data-stu-id="4ad88-132">After hello application has been deployed, hello **npm install** command is used tooparse hello **package.json** file and install all hello dependencies listed.</span></span>

<span data-ttu-id="4ad88-133">在開發期間，您可以使用 hello **-儲存**， **-儲存開發人員**，或**-儲存選擇性**安裝模組 tooadd hello 模組 tooyour的項目時的參數**package.json**自動檔案。</span><span class="sxs-lookup"><span data-stu-id="4ad88-133">During development, you can use hello **--save**, **--save-dev**, or **--save-optional** parameters when installing modules tooadd an entry for hello module tooyour **package.json** file automatically.</span></span> <span data-ttu-id="4ad88-134">如需詳細資訊，請參閱 [npm-install](https://docs.npmjs.com/cli/install)(英文)。</span><span class="sxs-lookup"><span data-stu-id="4ad88-134">For more information, see [npm-install](https://docs.npmjs.com/cli/install).</span></span>

<span data-ttu-id="4ad88-135">一個潛在的問題，以 hello **package.json**檔案是只會指定最上層的相依性的 hello 版本。</span><span class="sxs-lookup"><span data-stu-id="4ad88-135">One potential problem with hello **package.json** file is that it only specifies hello version for top-level dependencies.</span></span> <span data-ttu-id="4ad88-136">安裝每個模組也不能指定 hello 版本而定，hello 模組，它是可能的您可能會以結束比 hello 其中一個在開發中使用不同的相依性鏈結。</span><span class="sxs-lookup"><span data-stu-id="4ad88-136">Each module installed may or may not specify hello version of hello modules it depends on, and so it is possible that you may end up with a different dependency chain than hello one used in development.</span></span>

> [!NOTE]
> <span data-ttu-id="4ad88-137">部署時 tooAzure 應用程式服務，如果您<b>package.json</b>檔案參考原生模組，您可能會看到錯誤類似 toohello hello 應用程式使用 Git 發行時，下列範例：</span><span class="sxs-lookup"><span data-stu-id="4ad88-137">When deploying tooAzure App Service, if your <b>package.json</b> file references a native module you might see an error similar toohello following example when publishing hello application using Git:</span></span>
> 
> <span data-ttu-id="4ad88-138">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="4ad88-138">npm ERR!</span></span> <span data-ttu-id="4ad88-139">module-name@0.6.0 install: 'node-gyp configure build'</span><span class="sxs-lookup"><span data-stu-id="4ad88-139">module-name@0.6.0 install: 'node-gyp configure build'</span></span>
> 
> <span data-ttu-id="4ad88-140">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="4ad88-140">npm ERR!</span></span> <span data-ttu-id="4ad88-141">'cmd "/c" "node-gyp configure build"' failed with 1</span><span class="sxs-lookup"><span data-stu-id="4ad88-141">'cmd "/c" "node-gyp configure build"' failed with 1</span></span>
> 
> 

### <a name="using-a-npm-shrinkwrapjson-file"></a><span data-ttu-id="4ad88-142">使用 npm-shrinkwrap.json 檔案</span><span class="sxs-lookup"><span data-stu-id="4ad88-142">Using a npm-shrinkwrap.json file</span></span>
<span data-ttu-id="4ad88-143">hello **npm shrinkwrap.json**檔案是嘗試 tooaddress hello 模組版本設定的限制 hello **package.json**檔案。</span><span class="sxs-lookup"><span data-stu-id="4ad88-143">hello **npm-shrinkwrap.json** file is an attempt tooaddress hello module versioning limitations of hello **package.json** file.</span></span> <span data-ttu-id="4ad88-144">Hello 時**package.json**檔案只包含最上層模組 hello，版本 hello **npm shrinkwrap.json**檔案包含 hello 完整模組相依性鏈結的 hello 版本需求。</span><span class="sxs-lookup"><span data-stu-id="4ad88-144">While hello **package.json** file only includes versions for hello top-level modules, hello **npm-shrinkwrap.json** file contains hello version requirements for hello full module dependency chain.</span></span>

<span data-ttu-id="4ad88-145">準備好實際執行應用程式時，您可以鎖定版本需求，並建立**npm shrinkwrap.json**檔案使用 hello **npm shrinkwrap**命令。</span><span class="sxs-lookup"><span data-stu-id="4ad88-145">When your application is ready for production, you can lock down version requirements and create an **npm-shrinkwrap.json** file by using hello **npm shrinkwrap** command.</span></span> <span data-ttu-id="4ad88-146">此命令會使用目前安裝在 hello hello 版本**節點\_模組**資料夾，並將記錄這些版本 toohello **npm shrinkwrap.json**檔案。</span><span class="sxs-lookup"><span data-stu-id="4ad88-146">This command will use hello versions currently installed in hello **node\_modules** folder, and record these versions toohello **npm-shrinkwrap.json** file.</span></span> <span data-ttu-id="4ad88-147">Hello 應用程式是否已部署的 toohello 裝載環境之後，hello **npm 安裝**命令是使用的 tooparse hello **npm shrinkwrap.json**檔案，並安裝所有列出的 hello 相依性。</span><span class="sxs-lookup"><span data-stu-id="4ad88-147">After hello application has been deployed toohello hosting environment, hello **npm install** command is used tooparse hello **npm-shrinkwrap.json** file and install all hello dependencies listed.</span></span> <span data-ttu-id="4ad88-148">如需詳細資訊，請參閱 [npm-shrinkwrap](https://docs.npmjs.com/cli/shrinkwrap)。</span><span class="sxs-lookup"><span data-stu-id="4ad88-148">For more information, see [npm-shrinkwrap](https://docs.npmjs.com/cli/shrinkwrap).</span></span>

> [!NOTE]
> <span data-ttu-id="4ad88-149">部署時 tooAzure 應用程式服務，如果您<b>npm shrinkwrap.json</b>檔案參考原生模組，您可能會看到錯誤類似 toohello hello 應用程式使用 Git 發行時，下列範例：</span><span class="sxs-lookup"><span data-stu-id="4ad88-149">When deploying tooAzure App Service, if your <b>npm-shrinkwrap.json</b> file references a native module you might see an error similar toohello following example when publishing hello application using Git:</span></span>
> 
> <span data-ttu-id="4ad88-150">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="4ad88-150">npm ERR!</span></span> <span data-ttu-id="4ad88-151">module-name@0.6.0 install: 'node-gyp configure build'</span><span class="sxs-lookup"><span data-stu-id="4ad88-151">module-name@0.6.0 install: 'node-gyp configure build'</span></span>
> 
> <span data-ttu-id="4ad88-152">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="4ad88-152">npm ERR!</span></span> <span data-ttu-id="4ad88-153">'cmd "/c" "node-gyp configure build"' failed with 1</span><span class="sxs-lookup"><span data-stu-id="4ad88-153">'cmd "/c" "node-gyp configure build"' failed with 1</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4ad88-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4ad88-154">Next steps</span></span>
<span data-ttu-id="4ad88-155">既然您了解如何 toouse Node.js 模組，透過 Azure，深入了解如何太[指定 hello Node.js 版本]，[建置和部署 Node.js web 應用程式](app-service-web/app-service-web-get-started-nodejs.md)，和[toouse hello Azure 命令列的方式介面，用於 Mac 和 Linux]。</span><span class="sxs-lookup"><span data-stu-id="4ad88-155">Now that you understand how toouse Node.js modules with Azure, learn how too[specify hello Node.js version], [build and deploy a Node.js web app](app-service-web/app-service-web-get-started-nodejs.md), and [How toouse hello Azure Command-Line Interface for Mac and Linux].</span></span>

<span data-ttu-id="4ad88-156">如需詳細資訊，請參閱 hello [Node.js 開發人員中心](/nodejs/azure/)。</span><span class="sxs-lookup"><span data-stu-id="4ad88-156">For more information, see hello [Node.js Developer Center](/nodejs/azure/).</span></span>

[指定 hello Node.js 版本]: nodejs-specify-node-version-azure-apps.md
[toouse hello Azure 命令列的方式介面，用於 Mac 和 Linux]:cli-install-nodejs.md
[自訂 Kudu 與網站部署指令碼]: https://channel9.msdn.com/Shows/Azure-Friday/Custom-Web-Site-Deployment-Scripts-with-Kudu-with-David-Ebbo
