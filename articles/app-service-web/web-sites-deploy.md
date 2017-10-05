---
title: "將您的應用程式部署至 Azure App Service | Microsoft Docs"
description: "了解如何將您的應用程式部署至 Azure App Service。"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: f1464f71-2624-400e-86a2-e687e385804f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2017
ms.author: cephalin
ms.openlocfilehash: f41be4e00a9250b07ca260c2858e5fc45143f746
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-your-app-to-azure-app-service"></a><span data-ttu-id="07db5-103">將您的應用程式部署至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="07db5-103">Deploy your app to Azure App Service</span></span>
<span data-ttu-id="07db5-104">這篇文章可協助您判斷將 Web 應用程式、行動應用程式後端或 API 應用程式檔案部署至 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)的最佳選項，並針對您的慣用選項，引導您參考含適當指示的資源。</span><span class="sxs-lookup"><span data-stu-id="07db5-104">This article helps you determine the best option to deploy the files for your web app, mobile app backend, or API app to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), and then guides you to appropriate resources with instructions specific to your preferred option.</span></span>

## <span data-ttu-id="07db5-105"><a name="overview"></a>Azure App Service 部署概觀</span><span class="sxs-lookup"><span data-stu-id="07db5-105"><a name="overview"></a>Azure App Service deployment overview</span></span>
<span data-ttu-id="07db5-106">Azure App Service 會維護您的應用程式架構 (ASP.NET、PHP、Node.js 等等)。</span><span class="sxs-lookup"><span data-stu-id="07db5-106">Azure App Service maintains the application framework for you (ASP.NET, PHP, Node.js, etc).</span></span> <span data-ttu-id="07db5-107">有些架構會依預設啟用，而其他架構 (如 Java 和 Python) 則需要簡單的核取記號組態資訊才能啟用。</span><span class="sxs-lookup"><span data-stu-id="07db5-107">Some frameworks are enabled by default while others, like Java and Python, may need a simple checkmark configuration to enable it.</span></span> <span data-ttu-id="07db5-108">此外，您可以自訂您的應用程式架構，例如 PHP 版本或執行階段位元。</span><span class="sxs-lookup"><span data-stu-id="07db5-108">In addition, you can customize your application framework, such as the PHP version or the bitness of your runtime.</span></span> <span data-ttu-id="07db5-109">如需詳細資訊，請參閱 [在 Azure App Service 中設定您的應用程式](web-sites-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="07db5-109">For more information, see [Configure your app in Azure App Service](web-sites-configure.md).</span></span>

<span data-ttu-id="07db5-110">由於您不需要擔心 Web 伺服器或應用程式架構，因此若要將您的應用程式部署至 App Service，只要將程式碼、二進位檔、內容檔案和其個別的目錄結構部署至 Azure 的 [**/site/wwwroot** 目錄](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure)即可 (或 WebJobs 的 **/site/wwwroot/App_Data/Jobs/** 目錄)。</span><span class="sxs-lookup"><span data-stu-id="07db5-110">Since you don't have to worry about the web server or application framework, deploying your app to App Service is a matter of deploying your code, binaries, content files, and their respective directory structure, to the [**/site/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (or the **/site/wwwroot/App_Data/Jobs/** directory for WebJobs).</span></span> <span data-ttu-id="07db5-111">App Service 支援三種不同的部署程序。</span><span class="sxs-lookup"><span data-stu-id="07db5-111">App Service supports three different deployment processes.</span></span> <span data-ttu-id="07db5-112">本文中的所有部署方法皆使用下列其中一種程序：</span><span class="sxs-lookup"><span data-stu-id="07db5-112">All the deployment methods in this article use one of the following processes:</span></span> 

* <span data-ttu-id="07db5-113">[FTP 或 FTPS](https://en.wikipedia.org/wiki/File_Transfer_Protocol)：使用您最喜愛的 FTP 或 FTPS 啟用工具將您的檔案移至 Azure，從 [FileZilla](https://filezilla-project.org) 到功能完整的整合式開發環境 (IDE) (例如 [NetBeans](https://netbeans.org))。</span><span class="sxs-lookup"><span data-stu-id="07db5-113">[FTP or FTPS](https://en.wikipedia.org/wiki/File_Transfer_Protocol): Use your favorite FTP or FTPS enabled tool to move your files to Azure, from [FileZilla](https://filezilla-project.org) to full-featured IDEs like [NetBeans](https://netbeans.org).</span></span> <span data-ttu-id="07db5-114">這完全是檔案上傳程序。</span><span class="sxs-lookup"><span data-stu-id="07db5-114">This is strictly a file upload process.</span></span> <span data-ttu-id="07db5-115">App Service 不會提供其他服務，例如版本控制、檔案結構管理等等。</span><span class="sxs-lookup"><span data-stu-id="07db5-115">No additional services are provided by App Service, such as version control, file structure management, etc.</span></span> 
* <span data-ttu-id="07db5-116">[Kudu (Git/Mercurial 或 OneDrive/Dropbox)](https://github.com/projectkudu/kudu/wiki/Deployment)：Kudu 是 App Service 中的[部署引擎](https://github.com/projectkudu/kudu/wiki)。</span><span class="sxs-lookup"><span data-stu-id="07db5-116">[Kudu (Git/Mercurial or OneDrive/Dropbox)](https://github.com/projectkudu/kudu/wiki/Deployment): Kudu is the [deployment engine](https://github.com/projectkudu/kudu/wiki) in App Service.</span></span> <span data-ttu-id="07db5-117">將您的程式碼直接從任何儲存機制推送到 Kudu。</span><span class="sxs-lookup"><span data-stu-id="07db5-117">Push your code to Kudu directly from any repository.</span></span> <span data-ttu-id="07db5-118">Kudu 也會在程式碼推入時提供新增的服務，包括版本控制、封裝還原、MSBuild 和 [Web 勾點](https://github.com/projectkudu/kudu/wiki/Web-hooks) 以連續部署和其他自動化工作。</span><span class="sxs-lookup"><span data-stu-id="07db5-118">Kudu also provides added services whenever code is pushed to it, including version control, package restore, MSBuild, and [web hooks](https://github.com/projectkudu/kudu/wiki/Web-hooks) for continuous deployment and other automation tasks.</span></span> <span data-ttu-id="07db5-119">Kudu 部署引擎支援 3 種不同類型的部署來源：</span><span class="sxs-lookup"><span data-stu-id="07db5-119">The Kudu deployment engine supports 3 different types of deployment sources:</span></span>   
  
  * <span data-ttu-id="07db5-120">OneDrive 和 Dropbox 的內容同步處理</span><span class="sxs-lookup"><span data-stu-id="07db5-120">Content sync from OneDrive and Dropbox</span></span>   
  * <span data-ttu-id="07db5-121">以儲存機制為基礎的持續部署，其使用 GitHub、Bitbucket 和 Visual Studio Team Services 的自動同步處理</span><span class="sxs-lookup"><span data-stu-id="07db5-121">Repository-based continuous deployment with auto-sync from GitHub, Bitbucket, and Visual Studio Team Services</span></span>  
  * <span data-ttu-id="07db5-122">以儲存機制為基礎的部署，其使用本機 Git 手動同步處理</span><span class="sxs-lookup"><span data-stu-id="07db5-122">Repository-based deployment with manual sync from local Git</span></span>  
* <span data-ttu-id="07db5-123">[Web Deploy](http://www.iis.net/learn/publish/using-web-deploy/introduction-to-web-deploy)：可讓您使用自動部署至 IIS 伺服器的相同工具，直接從最愛的 Microsoft 工具 (例如 Visual Studio)，將程式碼部署至 App Service。</span><span class="sxs-lookup"><span data-stu-id="07db5-123">[Web Deploy](http://www.iis.net/learn/publish/using-web-deploy/introduction-to-web-deploy): Deploy code to App Service directly from your favorite Microsoft tools such as Visual Studio using the same tooling that automates deployment to IIS servers.</span></span> <span data-ttu-id="07db5-124">這項工具支援僅限差異比對的部署、資料庫建立、連接字串等的轉換等等。Web 部署不同於 Kudu 的地方，在於將應用程式二進位檔部署至 Azure 之前，會先進行建置。</span><span class="sxs-lookup"><span data-stu-id="07db5-124">This tool supports diff-only deployment, database creation, transforms of connection strings, etc. Web Deploy differs from Kudu in that application binaries are built before they are deployed to Azure.</span></span> <span data-ttu-id="07db5-125">類似於 FTP，App Service 不會提供其他服務。</span><span class="sxs-lookup"><span data-stu-id="07db5-125">Similar to FTP, no additional services are provided by App Service.</span></span>

<span data-ttu-id="07db5-126">熱門的 Web 開發工具支援一或多個這些部署程序。</span><span class="sxs-lookup"><span data-stu-id="07db5-126">Popular web development tools support one or more of these deployment processes.</span></span> <span data-ttu-id="07db5-127">雖然您選擇的工具會決定可以利用的部署程序，但可供您使用的實際 DevOps 功能取決於部署程序的組合以及且您選擇的特定工具。</span><span class="sxs-lookup"><span data-stu-id="07db5-127">While the tool you choose determines the deployment processes you can leverage, the actual DevOps functionality at your disposal depends on the combination of the deployment process and the specific tools you choose.</span></span> <span data-ttu-id="07db5-128">例如，如果您從 [Visual Studio 搭配 Azure SDK](#vspros)執行 Web Deploy，即使您未從 Kudu 獲得自動化，仍可在 Visual Studio 中獲得套件還原和 MSBuild 自動化。</span><span class="sxs-lookup"><span data-stu-id="07db5-128">For example, if you perform Web Deploy from [Visual Studio with Azure SDK](#vspros), even though you don't get automation from Kudu, you do get package restore and MSBuild automation in Visual Studio.</span></span> 

> [!NOTE]
> <span data-ttu-id="07db5-129">這些部署程序並不會實際 [佈建 Azure 資源](../azure-resource-manager/resource-group-template-deploy-portal.md) ，但這些資源可能是您的應用程式需要的。</span><span class="sxs-lookup"><span data-stu-id="07db5-129">These deployment processes don't actually [provision the Azure resources](../azure-resource-manager/resource-group-template-deploy-portal.md) that your app may need.</span></span> <span data-ttu-id="07db5-130">然而，大部分連結的作法文章會說明如何以端對端的方式佈建應用程式及將程式碼部署到應用程式。</span><span class="sxs-lookup"><span data-stu-id="07db5-130">However, most of the linked how-to articles show you how to provision the app AND deploy your code to it end-to-end.</span></span> <span data-ttu-id="07db5-131">您也可以在 [使用命令列工具自動化部署](#automate) 一節中找到佈建 Azure 資源的其他選項。</span><span class="sxs-lookup"><span data-stu-id="07db5-131">You can also find additional options for provisioning Azure resources in the [Automate deployment by using command-line tools](#automate) section.</span></span>
> 
> 

## <span data-ttu-id="07db5-132"><a name="ftp"></a>透過 FTP 上傳檔案來手動部署</span><span class="sxs-lookup"><span data-stu-id="07db5-132"><a name="ftp"></a>Deploy manually by uploading files with FTP</span></span>
<span data-ttu-id="07db5-133">如果您習慣以手動方式將網站內容複製到 Web 伺服器，則可以使用 [FTP](http://en.wikipedia.org/wiki/File_Transfer_Protocol) 公用程式來複製檔案，例如 Windows 檔案總管或 [FileZilla](https://filezilla-project.org/)。</span><span class="sxs-lookup"><span data-stu-id="07db5-133">If you are used to manually copying your web content to a web server, you can use an [FTP](http://en.wikipedia.org/wiki/File_Transfer_Protocol) utility to copy files, such as Windows Explorer or [FileZilla](https://filezilla-project.org/).</span></span>

<span data-ttu-id="07db5-134">手動複製檔案的優點如下：</span><span class="sxs-lookup"><span data-stu-id="07db5-134">The pros of copying files manually are:</span></span>

* <span data-ttu-id="07db5-135">FTP 工具易於上手且複雜性最小。</span><span class="sxs-lookup"><span data-stu-id="07db5-135">Familiarity and minimal complexity for FTP tooling.</span></span> 
* <span data-ttu-id="07db5-136">可明確掌握檔案的走向。</span><span class="sxs-lookup"><span data-stu-id="07db5-136">Knowing exactly where your files are going.</span></span>
* <span data-ttu-id="07db5-137">FTPS 的高安全性。</span><span class="sxs-lookup"><span data-stu-id="07db5-137">Added security with FTPS.</span></span>

<span data-ttu-id="07db5-138">手動複製檔案的缺點如下：</span><span class="sxs-lookup"><span data-stu-id="07db5-138">The cons of copying files manually are:</span></span>

* <span data-ttu-id="07db5-139">必須知道如何將檔案部署至 App Service 中正確的目錄。</span><span class="sxs-lookup"><span data-stu-id="07db5-139">Having to know how to deploy files to the correct directories in App Service.</span></span> 
* <span data-ttu-id="07db5-140">當發生失敗時沒有回復的版本控制。</span><span class="sxs-lookup"><span data-stu-id="07db5-140">No version control for rollback when failures occur.</span></span>
* <span data-ttu-id="07db5-141">沒有內建的部署歷程記錄可針對部署問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="07db5-141">No built-in deployment history for troubleshooting deployment issues.</span></span>
* <span data-ttu-id="07db5-142">部署時間可能會較長，因為有許多 FTP 工具不提供僅限差異比對的複製，而會複製所有檔案。</span><span class="sxs-lookup"><span data-stu-id="07db5-142">Potential long deployment times because many FTP tools don't provide diff-only copying and simply copy all the files.</span></span>  

### <span data-ttu-id="07db5-143"><a name="howtoftp"></a>如何透過 FTP 上傳檔案</span><span class="sxs-lookup"><span data-stu-id="07db5-143"><a name="howtoftp"></a>How to upload files with FTP</span></span>
<span data-ttu-id="07db5-144">[Azure 入口網站](https://portal.azure.com)會提供您使用 FTP 或 FTPS 來連接到應用程式目錄時所需的一切資訊。</span><span class="sxs-lookup"><span data-stu-id="07db5-144">The [Azure Portal](https://portal.azure.com) gives you all the information you need to connect to your app's directories using FTP or FTPS.</span></span>

* [<span data-ttu-id="07db5-145">使用 FTP 將您的應用程式部署至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="07db5-145">Deploy your app to Azure App Service using FTP</span></span>](app-service-deploy-ftp.md)

## <span data-ttu-id="07db5-146"><a name="dropbox"></a>與雲端資料夾同步處理以進行部署</span><span class="sxs-lookup"><span data-stu-id="07db5-146"><a name="dropbox"></a>Deploy by syncing with a cloud folder</span></span>
<span data-ttu-id="07db5-147">如果不想 [手動複製檔案](#ftp) ，理想替代方法是從雲端儲存空間 (例如 OneDrive 和 Dropbox)，將檔案和資料夾同步處理到 App Service。</span><span class="sxs-lookup"><span data-stu-id="07db5-147">A good alternative to [copying files manually](#ftp) is syncing files and folders to App Service from a cloud storage service like OneDrive and Dropbox.</span></span> <span data-ttu-id="07db5-148">與雲端資料夾同步處理時，會利用 Kudu 程序來進行部署 (請參閱 [部署程序概觀](#overview))。</span><span class="sxs-lookup"><span data-stu-id="07db5-148">Syncing with a cloud folder utilizes the Kudu process for deployment (see [Overview of deployment processes](#overview)).</span></span>

<span data-ttu-id="07db5-149">與雲端資料夾同步處理的優點如下：</span><span class="sxs-lookup"><span data-stu-id="07db5-149">The pros of syncing with a cloud folder are:</span></span>

* <span data-ttu-id="07db5-150">部署的簡潔性。</span><span class="sxs-lookup"><span data-stu-id="07db5-150">Simplicity of deployment.</span></span> <span data-ttu-id="07db5-151">部分服務 (例如 OneDrive 和 Dropbox) 提供桌面同步處理用戶端，使您的本機工作目錄也是部署目錄。</span><span class="sxs-lookup"><span data-stu-id="07db5-151">Services like OneDrive and Dropbox provide desktop sync clients, so your local working directory is also your deployment directory.</span></span>
* <span data-ttu-id="07db5-152">單鍵部署。</span><span class="sxs-lookup"><span data-stu-id="07db5-152">One-click deployment.</span></span>
* <span data-ttu-id="07db5-153">可使用 Kudu 部署引擎中的所有功能 (例如封裝還原和自動化)。</span><span class="sxs-lookup"><span data-stu-id="07db5-153">All functionality in the Kudu deployment engine is available (e.g. package restore, automation).</span></span>

<span data-ttu-id="07db5-154">與雲端資料夾同步處理的缺點如下：</span><span class="sxs-lookup"><span data-stu-id="07db5-154">The cons of syncing with a cloud folder are:</span></span>

* <span data-ttu-id="07db5-155">當發生失敗時沒有回復的版本控制。</span><span class="sxs-lookup"><span data-stu-id="07db5-155">No version control for rollback when failures occur.</span></span>
* <span data-ttu-id="07db5-156">沒有自動化的部署，需要手動同步處理。</span><span class="sxs-lookup"><span data-stu-id="07db5-156">No automated deployment, manual sync is required.</span></span>

### <span data-ttu-id="07db5-157"><a name="howtodropbox"></a>如何與雲端資料夾同步處理以進行部署</span><span class="sxs-lookup"><span data-stu-id="07db5-157"><a name="howtodropbox"></a>How to deploy by syncing with a cloud folder</span></span>
<span data-ttu-id="07db5-158">在 [Azure 入口網站](https://portal.azure.com)中，您可以在 OneDrive 或 Dropbox 雲端儲存空間中指定要同步內容的資料夾、在該資料夾中處理您的應用程式程式碼和內容，並按一下按鈕以同步至 App Service。</span><span class="sxs-lookup"><span data-stu-id="07db5-158">In the [Azure Portal](https://portal.azure.com), you can designate a folder for content sync in your OneDrive or Dropbox cloud storage, work with your app code and content in that folder, and sync to App Service with the click of a button.</span></span>

* <span data-ttu-id="07db5-159">[將雲端資料夾的內容同步處理到 Azure App Service](app-service-deploy-content-sync.md)。</span><span class="sxs-lookup"><span data-stu-id="07db5-159">[Sync content from a cloud folder to Azure App Service](app-service-deploy-content-sync.md).</span></span> 

## <span data-ttu-id="07db5-160"><a name="continuousdeployment"></a>從雲端型原始檔控制服務進行持續部署</span><span class="sxs-lookup"><span data-stu-id="07db5-160"><a name="continuousdeployment"></a>Deploy continuously from a cloud-based source control service</span></span>
<span data-ttu-id="07db5-161">如果您的開發團隊使用雲端型原始程式碼管理 (SCM) 服務，例如 [Visual Studio Team Services](http://www.visualstudio.com/)[GitHub](https://www.github.com)或 [BitBucket](https://bitbucket.org/)，您可以設定 App Service 與儲存機制整合，並持續部署。</span><span class="sxs-lookup"><span data-stu-id="07db5-161">If your development team uses a cloud-based source code management (SCM) service like [Visual Studio Team Services](http://www.visualstudio.com/), [GitHub](https://www.github.com), or [BitBucket](https://bitbucket.org/), you can configure App Service to integrate with your repository and deploy continuously.</span></span> 

<span data-ttu-id="07db5-162">從雲端型原始檔控制服務進行部署的優點如下：</span><span class="sxs-lookup"><span data-stu-id="07db5-162">The pros of deploying from a cloud-based source control service are:</span></span>

* <span data-ttu-id="07db5-163">版本控制可進行回復。</span><span class="sxs-lookup"><span data-stu-id="07db5-163">Version control to enable rollback.</span></span>
* <span data-ttu-id="07db5-164">可設定適用於 Git 儲存機制 (若適用的話也含 Mercurial) 的持續部署。</span><span class="sxs-lookup"><span data-stu-id="07db5-164">Ability to configure continuous deployment for Git (and Mercurial where applicable) repositories.</span></span> 
* <span data-ttu-id="07db5-165">分支專屬的部署，可以將不同的分支部署至不同的 [位置](web-sites-staged-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="07db5-165">Branch-specific deployment, can deploy different branches to different [slots](web-sites-staged-publishing.md).</span></span>
* <span data-ttu-id="07db5-166">可使用 Kudu 部署引擎中的所有功能 (例如部署版本控制、回復、封裝還原和自動化)。</span><span class="sxs-lookup"><span data-stu-id="07db5-166">All functionality in the Kudu deployment engine is available (e.g. deployment versioning, rollback, package restore, automation).</span></span>

<span data-ttu-id="07db5-167">從雲端型原始檔控制服務進行部署的缺點如下：</span><span class="sxs-lookup"><span data-stu-id="07db5-167">The con of deploying from a cloud-based source control service is:</span></span>

* <span data-ttu-id="07db5-168">需對個別 SCM 服務有一定程度的了解。</span><span class="sxs-lookup"><span data-stu-id="07db5-168">Some knowledge of the respective SCM service required.</span></span>

### <span data-ttu-id="07db5-169"><a name="vsts"></a>如何從雲端型原始檔控制服務進行持續部署</span><span class="sxs-lookup"><span data-stu-id="07db5-169"><a name="vsts"></a>How to deploy continuously from a cloud-based source control service</span></span>
<span data-ttu-id="07db5-170">在 [Azure 入口網站](https://portal.azure.com)中，您可以透過 GitHub、Bitbucket 和 Visual Studio Team Services 設定持續部署。</span><span class="sxs-lookup"><span data-stu-id="07db5-170">In the [Azure Portal](https://portal.azure.com), you can configure continuous deployment from GitHub, Bitbucket, and Visual Studio Team Services.</span></span>

* <span data-ttu-id="07db5-171">[持續部署至 Azure App Service](app-service-continuous-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="07db5-171">[Continous Deployment to Azure App Service](app-service-continuous-deployment.md).</span></span> 

<span data-ttu-id="07db5-172">若要了解如何從 Azure 入口網站未列出的雲端存放庫中手動設定連續部署 (例如 [GitLab](https://gitlab.com/))，請參閱[使用手動步驟設定連續部署](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps)。</span><span class="sxs-lookup"><span data-stu-id="07db5-172">To find out how to configure continuous deployment manually from a cloud repository not listed by the Azure Portal (such as [GitLab](https://gitlab.com/)), see [Setting up continuous deployment using manual steps](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).</span></span>

## <span data-ttu-id="07db5-173"><a name="localgitdeployment"></a>從本機 Git 進行部署</span><span class="sxs-lookup"><span data-stu-id="07db5-173"><a name="localgitdeployment"></a>Deploy from local Git</span></span>
<span data-ttu-id="07db5-174">如果開發團隊使用以 Git 為基礎的內部部署本機原始程式碼管理 (SCM) 服務，則您可將其設為 App Service 的部署來源。</span><span class="sxs-lookup"><span data-stu-id="07db5-174">If your development team uses an on-premises local source code management (SCM) service based on Git, you can configure this as a deployment source to App Service.</span></span> 

<span data-ttu-id="07db5-175">從本機 Git 進行部署的優點如下：</span><span class="sxs-lookup"><span data-stu-id="07db5-175">Pros of deploying from local Git are:</span></span>

* <span data-ttu-id="07db5-176">版本控制可進行回復。</span><span class="sxs-lookup"><span data-stu-id="07db5-176">Version control to enable rollback.</span></span>
* <span data-ttu-id="07db5-177">分支專屬的部署，可以將不同的分支部署至不同的 [位置](web-sites-staged-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="07db5-177">Branch-specific deployment, can deploy different branches to different [slots](web-sites-staged-publishing.md).</span></span>
* <span data-ttu-id="07db5-178">可使用 Kudu 部署引擎中的所有功能 (例如部署版本控制、回復、封裝還原和自動化)。</span><span class="sxs-lookup"><span data-stu-id="07db5-178">All functionality in the Kudu deployment engine is available (e.g. deployment versioning, rollback, package restore, automation).</span></span>

<span data-ttu-id="07db5-179">從本機 Git 進行部署的缺點如下：</span><span class="sxs-lookup"><span data-stu-id="07db5-179">Cons of deploying from local Git is:</span></span>

* <span data-ttu-id="07db5-180">需對個別 SCM 系統有一定程度的了解。</span><span class="sxs-lookup"><span data-stu-id="07db5-180">Some knowledge of the respective SCM system required.</span></span>
* <span data-ttu-id="07db5-181">沒有任何持續部署的現成解決方案。</span><span class="sxs-lookup"><span data-stu-id="07db5-181">No turn-key solutions for continuous deployment.</span></span> 

### <span data-ttu-id="07db5-182"><a name="vsts"></a>如何從本機 Git 進行部署</span><span class="sxs-lookup"><span data-stu-id="07db5-182"><a name="vsts"></a>How to deploy from local Git</span></span>
<span data-ttu-id="07db5-183">在 [Azure 入口網站](https://portal.azure.com)中，您可以設定本機 Git 部署。</span><span class="sxs-lookup"><span data-stu-id="07db5-183">In the [Azure Portal](https://portal.azure.com), you can configure local Git deployment.</span></span>

* <span data-ttu-id="07db5-184">[本機 Git 部署至 Azure App Service](app-service-deploy-local-git.md)。</span><span class="sxs-lookup"><span data-stu-id="07db5-184">[Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span> 
* <span data-ttu-id="07db5-185">[從任何 git/hg 儲存機制發行至 Web Apps](http://blog.davidebbo.com/2013/04/publishing-to-azure-web-sites-from-any.html)。</span><span class="sxs-lookup"><span data-stu-id="07db5-185">[Publishing to Web Apps from any git/hg repo](http://blog.davidebbo.com/2013/04/publishing-to-azure-web-sites-from-any.html).</span></span>  

## <a name="deploy-using-an-ide"></a><span data-ttu-id="07db5-186">使用整合式開發環境 (IDE) 部署</span><span class="sxs-lookup"><span data-stu-id="07db5-186">Deploy using an IDE</span></span>
<span data-ttu-id="07db5-187">如果您已經將 [Visual Studio](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) 與 [Azure SDK](https://azure.microsoft.com/downloads/) 或其他整合式開發環境 (IDE) 套件 (例如 [Xcode](https://developer.apple.com/xcode/)[Eclipse](https://www.eclipse.org)和 [IntelliJ IDEA](https://www.jetbrains.com/idea/)) 搭配使用，您就可以直接從您的整合式開發環境 (IDE) 內部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="07db5-187">If you are already using [Visual Studio](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) with an [Azure SDK](https://azure.microsoft.com/downloads/), or other IDE suites like [Xcode](https://developer.apple.com/xcode/), [Eclipse](https://www.eclipse.org), and [IntelliJ IDEA](https://www.jetbrains.com/idea/), you can deploy to Azure directly from within your IDE.</span></span> <span data-ttu-id="07db5-188">此選項適用於個別的開發人員。</span><span class="sxs-lookup"><span data-stu-id="07db5-188">This option is ideal for an individual developer.</span></span>

<span data-ttu-id="07db5-189">視您的喜好設定而定，Visual Studio 支援所有三種部署程序 (FTP、Git 及 Web Deploy)，而其他 IDE 若有 FTP 或 Git 整合，便可以部署至 App Service (請參閱 [部署程序概觀](#overview))。</span><span class="sxs-lookup"><span data-stu-id="07db5-189">Visual Studio supports all three deployment processes (FTP, Git, and Web Deploy), depending on your preference, while other IDEs can deploy to App Service if they have FTP or Git integration (see [Overview of deployment processes](#overview)).</span></span>

<span data-ttu-id="07db5-190">使用整合式開發環境 (IDE) 部署的優點如下：</span><span class="sxs-lookup"><span data-stu-id="07db5-190">The pros of deploying using an IDE are:</span></span>

* <span data-ttu-id="07db5-191">可能會減少您端對端應用程式生命週期的工具。</span><span class="sxs-lookup"><span data-stu-id="07db5-191">Potentially minimize the tooling for your end-to-end application life-cycle.</span></span> <span data-ttu-id="07db5-192">開發、偵錯、追蹤和部署應用程式至 Azure 而不會移動到您的整合式開發環境 (IDE) 之外。</span><span class="sxs-lookup"><span data-stu-id="07db5-192">Develop, debug, track, and deploy your app to Azure all without moving outside of your IDE.</span></span> 

<span data-ttu-id="07db5-193">使用整合式開發環境 (IDE) 部署的缺點如下：</span><span class="sxs-lookup"><span data-stu-id="07db5-193">The cons of deploying using an IDE are:</span></span>

* <span data-ttu-id="07db5-194">工具的複雜度增加。</span><span class="sxs-lookup"><span data-stu-id="07db5-194">Added complexity in tooling.</span></span>
* <span data-ttu-id="07db5-195">仍然需要團隊專案的原始檔控制系統。</span><span class="sxs-lookup"><span data-stu-id="07db5-195">Still requires a source control system for a team project.</span></span>

<span data-ttu-id="07db5-196"><a name="vspros"></a> 使用 Visual Studio 搭配 Azure SDK 進行部署的其他優點包括：</span><span class="sxs-lookup"><span data-stu-id="07db5-196"><a name="vspros"></a> Additional pros of deploying using Visual Studio with Azure SDK are:</span></span>

* <span data-ttu-id="07db5-197">Azure SDK 會優先使用 Visual Studio 中的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="07db5-197">Azure SDK makes Azure resources first-class citizens in Visual Studio.</span></span> <span data-ttu-id="07db5-198">建立、刪除、編輯、啟動和停止應用程式、查詢後端 SQL Database、即時偵錯 Azure 應用程式，以及更多。</span><span class="sxs-lookup"><span data-stu-id="07db5-198">Create, delete, edit, start, and stop apps, query the backend SQL database, live-debug the Azure app, and much more.</span></span> 
* <span data-ttu-id="07db5-199">即時編輯在 Azure 上的程式碼檔案。</span><span class="sxs-lookup"><span data-stu-id="07db5-199">Live editing of code files on Azure.</span></span>
* <span data-ttu-id="07db5-200">即時偵錯在 Azure 上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="07db5-200">Live debugging of apps on Azure.</span></span>
* <span data-ttu-id="07db5-201">整合式 Azure Explorer。</span><span class="sxs-lookup"><span data-stu-id="07db5-201">Integrated Azure explorer.</span></span>
* <span data-ttu-id="07db5-202">僅限差異比對的部署。</span><span class="sxs-lookup"><span data-stu-id="07db5-202">Diff-only deployment.</span></span> 

### <span data-ttu-id="07db5-203"><a name="vs"></a>如何直接從 Visual Studio 進行部署</span><span class="sxs-lookup"><span data-stu-id="07db5-203"><a name="vs"></a>How to deploy from Visual Studio directly</span></span>
* <span data-ttu-id="07db5-204">[開始使用 Azure 和 ASP.NET](app-service-web-get-started-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="07db5-204">[Get started with Azure and ASP.NET](app-service-web-get-started-dotnet.md).</span></span> <span data-ttu-id="07db5-205">說明如何使用 Visual Studio 和 Web Deploy 建立及部署簡易的 ASP.NET MVC Web 專案。</span><span class="sxs-lookup"><span data-stu-id="07db5-205">How to create and deploy a simple ASP.NET MVC web project by using Visual Studio and Web Deploy.</span></span>
* <span data-ttu-id="07db5-206">[如何使用 Visual Studio 部署 Azure WebJob](websites-dotnet-deploy-webjobs.md)。</span><span class="sxs-lookup"><span data-stu-id="07db5-206">[How to Deploy Azure WebJobs using Visual Studio](websites-dotnet-deploy-webjobs.md).</span></span> <span data-ttu-id="07db5-207">如何設定主控台應用程式專案，使其部署為 WebJob。</span><span class="sxs-lookup"><span data-stu-id="07db5-207">How to configure Console Application projects so that they deploy as WebJobs.</span></span>  
* <span data-ttu-id="07db5-208">[使用 Visual Studio 的 ASP.NET Web 部署](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/introduction)。</span><span class="sxs-lookup"><span data-stu-id="07db5-208">[ASP.NET Web Deployment using Visual Studio](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/introduction).</span></span> <span data-ttu-id="07db5-209">這是分成 12 個單元的教學課程系列，其中討論的部署工作比此處所列的其他資源更為詳盡。</span><span class="sxs-lookup"><span data-stu-id="07db5-209">A 12-part tutorial series that covers a more complete range of deployment tasks than the others in this list.</span></span> <span data-ttu-id="07db5-210">本教學課程撰寫後已新增某些 Azure 部署功能，但稍後的附註會說明遺漏的功能。</span><span class="sxs-lookup"><span data-stu-id="07db5-210">Some Azure deployment features have been added since the tutorial was written, but notes added later explain what's missing.</span></span>
* <span data-ttu-id="07db5-211">[在 Visual Studio 2012 中直接從 Git 儲存機制將 ASP.NET 網站部署至 Azure](http://www.dotnetcurry.com/ShowArticle.aspx?ID=881)。</span><span class="sxs-lookup"><span data-stu-id="07db5-211">[Deploying an ASP.NET Website to Azure in Visual Studio 2012 from a Git Repository directly](http://www.dotnetcurry.com/ShowArticle.aspx?ID=881).</span></span> <span data-ttu-id="07db5-212">說明如何使用 Git 外掛程式將程式碼認可至 Git，以及將 Azure 連接到 Git 儲存機制，以在 Visual Studio 中部署 ASP.NET Web 專案。</span><span class="sxs-lookup"><span data-stu-id="07db5-212">Explains how to deploy an ASP.NET web project in Visual Studio, using the Git plug-in to commit the code to Git and connecting Azure to the Git repository.</span></span> <span data-ttu-id="07db5-213">自 Visual Studio 2013 起，Git 支援已是內建的功能，不需安裝外掛程式。</span><span class="sxs-lookup"><span data-stu-id="07db5-213">Starting in Visual Studio 2013, Git support is built-in and doesn't require installation of a plug-in.</span></span>

### <span data-ttu-id="07db5-214"><a name="aztk"></a>如何使用適用於 Eclipse 和 IntelliJ IDEA 的 Azure 工具組來進行部署</span><span class="sxs-lookup"><span data-stu-id="07db5-214"><a name="aztk"></a>How to deploy using the Azure Toolkits for Eclipse and IntelliJ IDEA</span></span>
<span data-ttu-id="07db5-215">Microsoft 可讓您透過[適用於 Eclipse 的 Azure 工具組](../azure-toolkit-for-eclipse.md)和[適用於 IntelliJ 的 Azure 工具組](../azure-toolkit-for-intellij.md)，將 Web Apps 直接從 Eclipse 和 IntelliJ 部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="07db5-215">Microsoft makes it possible to deploy Web Apps to Azure directly from Eclipse and IntelliJ via the [Azure Toolkit for Eclipse](../azure-toolkit-for-eclipse.md) and [Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij.md).</span></span> <span data-ttu-id="07db5-216">下列教學課程說明使用上述任一整合式開發環境 (IDE)，將簡單的 "Hello" World Web 應用程式部署到 Azure 所涉及的步驟：</span><span class="sxs-lookup"><span data-stu-id="07db5-216">The following tutorials illustrate the steps that are involved in deploying simple a "Hello" world Web App to Azure using either IDE:</span></span>

* <span data-ttu-id="07db5-217">[Create a Hello World Web App for Azure in Eclipse (在 Eclipse 中建立 Azure Hello World Web 應用程式)](app-service-web-eclipse-create-hello-world-web-app.md)。</span><span class="sxs-lookup"><span data-stu-id="07db5-217">[Create a Hello World Web App for Azure in Eclipse](app-service-web-eclipse-create-hello-world-web-app.md).</span></span> <span data-ttu-id="07db5-218">本教學課程示範如何使用「適用於 Eclipse 的 Azure 工具組」來建立與部署 Azure 的 Hello World Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="07db5-218">This tutorial shows you how to use the Azure Toolkit for Eclipse to create and deploy a Hello World Web App for Azure.</span></span>
* <span data-ttu-id="07db5-219">[在 IntelliJ 中建立 Azure Hello World Web 應用程式](app-service-web-intellij-create-hello-world-web-app.md)。</span><span class="sxs-lookup"><span data-stu-id="07db5-219">[Create a Hello World Web App for Azure in IntelliJ](app-service-web-intellij-create-hello-world-web-app.md).</span></span> <span data-ttu-id="07db5-220">本教學課程示範如何使用「適用於 IntelliJ 的 Azure 工具組」來建立與部署 Azure 的 Hello World Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="07db5-220">This tutorial shows you how to use the Azure Toolkit for IntelliJ to create and deploy a Hello World Web App for Azure.</span></span>

## <span data-ttu-id="07db5-221"><a name="automate"></a>使用命令列工具進行自動化部署</span><span class="sxs-lookup"><span data-stu-id="07db5-221"><a name="automate"></a>Automate deployment by using command-line tools</span></span>
<span data-ttu-id="07db5-222">如果您偏好使用命令列終端機作為選擇的開發環境，您可以使用命令列工具為 App Service 應用程式編寫部署工作指令碼。</span><span class="sxs-lookup"><span data-stu-id="07db5-222">If you prefer the command-line terminal as the development environment of choice, you can script deployment tasks for your App Service app using command-line tools.</span></span> 

<span data-ttu-id="07db5-223">使用命令列工具進行部署的優點如下：</span><span class="sxs-lookup"><span data-stu-id="07db5-223">Pros of deploying by using command-line tools are:</span></span>

* <span data-ttu-id="07db5-224">啟用指令碼式部署案例。</span><span class="sxs-lookup"><span data-stu-id="07db5-224">Enables scripted deployment scenarios.</span></span>
* <span data-ttu-id="07db5-225">整合 Azure 資源與程式碼部署的佈建。</span><span class="sxs-lookup"><span data-stu-id="07db5-225">Integrate provisioning of Azure resources and code deployment.</span></span>
* <span data-ttu-id="07db5-226">將 Azure 部署整合至現有的連續整合指令碼。</span><span class="sxs-lookup"><span data-stu-id="07db5-226">Integrate Azure deployment into existing continous integration scripts.</span></span>

<span data-ttu-id="07db5-227">使用命令列工具進行部署的缺點如下：</span><span class="sxs-lookup"><span data-stu-id="07db5-227">Cons of deploying by using command-line tools are:</span></span>

* <span data-ttu-id="07db5-228">不適用於偏好 GUI 的開發人員。</span><span class="sxs-lookup"><span data-stu-id="07db5-228">Not for GUI-preferring developers.</span></span>

### <span data-ttu-id="07db5-229"><a name="automatehow"></a>如何使用命令列工具進行自動化部署</span><span class="sxs-lookup"><span data-stu-id="07db5-229"><a name="automatehow"></a>How to automate deployment with command-line tools</span></span>

<span data-ttu-id="07db5-230">如需命令列工具清單和教學課程連結，請參閱[使用命令列工具來自動部署 Azure 應用程式](app-service-deploy-command-line.md)。</span><span class="sxs-lookup"><span data-stu-id="07db5-230">See [Automate deployment of your Azure app with command-line tools](app-service-deploy-command-line.md) for a list of command-line tools and links to tutorials.</span></span> 

## <span data-ttu-id="07db5-231"><a name="nextsteps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="07db5-231"><a name="nextsteps"></a>Next Steps</span></span>
<span data-ttu-id="07db5-232">在某些情況中，您可能想要輕鬆地在預備版本和生產版本的應用程式之間來回切換。</span><span class="sxs-lookup"><span data-stu-id="07db5-232">In some scenarios you might want to be able to easily switch back and forth between a staging and a production version of your app.</span></span> <span data-ttu-id="07db5-233">[如需詳細資訊，請參閱 Web Apps 上的預備部署](web-sites-staged-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="07db5-233">For more information, see [Staged Deployment on Web Apps](web-sites-staged-publishing.md).</span></span>

<span data-ttu-id="07db5-234">具有備份及還原計劃是部署工作流程中相當重要的環節。</span><span class="sxs-lookup"><span data-stu-id="07db5-234">Having a backup and restore plan in place is an important part of any deployment workflow.</span></span> <span data-ttu-id="07db5-235">如需有關 App Service 備份和還原功能的資訊，請參閱 [Web Apps 備份](web-sites-backup.md)。</span><span class="sxs-lookup"><span data-stu-id="07db5-235">For information about the App Service backup and restore feature, see [Web Apps Backups](web-sites-backup.md).</span></span>  

<span data-ttu-id="07db5-236">如需了解如何使用 Azure「角色型存取控制」來管理對 App Service 部署的存取，請參閱 [RBAC 和 Web 應用程式發行](https://azure.microsoft.com/blog/2015/01/05/rbac-and-azure-websites-publishing/)。</span><span class="sxs-lookup"><span data-stu-id="07db5-236">For information about how to use Azure's Role-Based Access Control to manage access to App Service deployment, see [RBAC and Web App Publishing](https://azure.microsoft.com/blog/2015/01/05/rbac-and-azure-websites-publishing/).</span></span>

