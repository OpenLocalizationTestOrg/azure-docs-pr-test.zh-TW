---
title: "aaaDeploy 您應用程式 tooAzure 應用程式服務使用 FTP/S |Microsoft 文件"
description: "深入了解如何 toodeploy 您的應用程式 tooAzure 應用程式服務使用 FTP 或 FTPS。"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: ae78b410-1bc0-4d72-8fc4-ac69801247ae
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2016
ms.author: cephalin;dariac
ms.openlocfilehash: 318ae79d4fae269f853ea5c3ce28353b0864131e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-tooazure-app-service-using-ftps"></a><span data-ttu-id="a0d80-103">部署您的應用程式 tooAzure 使用 FTP/S 的應用程式服務</span><span class="sxs-lookup"><span data-stu-id="a0d80-103">Deploy your app tooAzure App Service using FTP/S</span></span>

<span data-ttu-id="a0d80-104">本文章將示範如何 toouse FTP 或 web 應用程式、 行動裝置應用程式後端或應用程式開發介面應用程式太 FTPS toodeploy[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)。</span><span class="sxs-lookup"><span data-stu-id="a0d80-104">This article shows you how toouse FTP or FTPS toodeploy your web app, mobile app backend, or API app too[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="a0d80-105">您的應用程式的 hello FTP/S 端點已在使用中。</span><span class="sxs-lookup"><span data-stu-id="a0d80-105">hello FTP/S endpoint for your app is already active.</span></span> <span data-ttu-id="a0d80-106">不不需要 tooenable FTP/S 部署的任何設定。</span><span class="sxs-lookup"><span data-stu-id="a0d80-106">No configuration is necessary tooenable FTP/S deployment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0d80-107">我們會持續執行步驟 tooimprove Microsoft Azure 平台安全性。</span><span class="sxs-lookup"><span data-stu-id="a0d80-107">We are continuously taking steps tooimprove Microsoft Azure Platform security.</span></span> <span data-ttu-id="a0d80-108">在此持續努力的過程中，我們規劃升級德國中部和德國東北部地區的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a0d80-108">As part of this ongoing effort an upgrade of Web Applications is planned for Germany Central and Germany Northeast regions.</span></span> <span data-ttu-id="a0d80-109">在此 Web 應用程式將會停用部署的 hello 使用純文字 FTP 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="a0d80-109">During this Web Apps will be disabling hello use of plain text FTP protocol for deployments.</span></span> <span data-ttu-id="a0d80-110">我們建議 tooour 客戶是 tooswitch tooFTPS 部署。</span><span class="sxs-lookup"><span data-stu-id="a0d80-110">Our recommendation tooour customers is tooswitch tooFTPS for deployments.</span></span> <span data-ttu-id="a0d80-111">我們不會在執行此升級的 9/5 計劃的任何中斷 tooyour 服務。</span><span class="sxs-lookup"><span data-stu-id="a0d80-111">We do not expect any disruption tooyour service during this upgrade which is planned for 9/5.</span></span> <span data-ttu-id="a0d80-112">感謝您支援這項工作。</span><span class="sxs-lookup"><span data-stu-id="a0d80-112">We appreciate you support in this effort.</span></span>

<a name="step1"></a>
## <a name="step-1-set-deployment-credentials"></a><span data-ttu-id="a0d80-113">步驟 1：設定部署認證</span><span class="sxs-lookup"><span data-stu-id="a0d80-113">Step 1: Set deployment credentials</span></span>

<span data-ttu-id="a0d80-114">tooaccess hello FTP 伺服器上您的應用程式，您必須先部署認證。</span><span class="sxs-lookup"><span data-stu-id="a0d80-114">tooaccess hello FTP server for your app, you first need deployment credentials.</span></span> 

<span data-ttu-id="a0d80-115">tooset 或重設您的部署認證，請參閱[Azure 應用程式服務的部署認證](app-service-deployment-credentials.md)。</span><span class="sxs-lookup"><span data-stu-id="a0d80-115">tooset or reset your deployment credentials, see [Azure App Service Deployment Credentials](app-service-deployment-credentials.md).</span></span> <span data-ttu-id="a0d80-116">本教學課程示範 hello 使用使用者層級的認證。</span><span class="sxs-lookup"><span data-stu-id="a0d80-116">This tutorial demonstrates hello use of user-level credentials.</span></span>

## <a name="step-2-get-ftp-connection-information"></a><span data-ttu-id="a0d80-117">步驟 2：取得 FTP 連線資訊</span><span class="sxs-lookup"><span data-stu-id="a0d80-117">Step 2: Get FTP connection information</span></span>

1. <span data-ttu-id="a0d80-118">在 hello [Azure 入口網站](https://portal.azure.com)，開啟您的應用程式[資源刀鋒視窗](../azure-resource-manager/resource-group-portal.md#manage-resources)。</span><span class="sxs-lookup"><span data-stu-id="a0d80-118">In hello [Azure portal](https://portal.azure.com), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="a0d80-119">選取**概觀**在 hello 左功能表中，然後記下 hello 值**FTP/部署使用者**， **FTP 主機名稱**，和**FTPS 主機名稱**。</span><span class="sxs-lookup"><span data-stu-id="a0d80-119">Select **Overview** in hello left menu, then note hello values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span> 

    ![FTP 連線資訊](./media/web-sites-deploy/FTP-Connection-Info.PNG)

    > [!NOTE]
    > <span data-ttu-id="a0d80-121">hello **FTP/部署使用者**使用者值顯示 hello hello 應用程式名稱包含在 hello FTP 伺服器的順序 tooprovide 適當內容的 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="a0d80-121">hello **FTP/Deployment User** user value as displayed by hello Azure Portal including hello app name in order tooprovide proper context for hello FTP server.</span></span>
    > <span data-ttu-id="a0d80-122">您可以找到 hello 相同的資訊，當您選取**屬性**hello 左功能表中。</span><span class="sxs-lookup"><span data-stu-id="a0d80-122">You can find hello same information when you select **Properties** in hello left menu.</span></span> 
    >
    > <span data-ttu-id="a0d80-123">此外，永遠不會顯示 hello 部署密碼。</span><span class="sxs-lookup"><span data-stu-id="a0d80-123">Also, hello deployment password is never shown.</span></span> <span data-ttu-id="a0d80-124">如果您忘記您部署的密碼，請回到太[步驟 1](#step1)和重設您部署的密碼。</span><span class="sxs-lookup"><span data-stu-id="a0d80-124">If you forget your deployment password, go back too[step 1](#step1) and reset your deployment password.</span></span>
    >
    >

## <a name="step-3-deploy-files-tooazure"></a><span data-ttu-id="a0d80-125">步驟 3： 部署檔案 tooAzure</span><span class="sxs-lookup"><span data-stu-id="a0d80-125">Step 3: Deploy files tooAzure</span></span>

1. <span data-ttu-id="a0d80-126">從您的 FTP 用戶端 ([Visual Studio](https://www.visualstudio.com/vs/community/)， [FileZilla](https://filezilla-project.org/download.php?type=client)等等)，使用您所蒐集 tooconnect tooyour 應用程式的 hello 連接資訊。</span><span class="sxs-lookup"><span data-stu-id="a0d80-126">From your FTP client ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), etc), use hello connection information you gathered tooconnect tooyour app.</span></span>
3. <span data-ttu-id="a0d80-127">複製您的檔案和其各自的目錄結構 toohello [ **/站台/wwwroot**目錄](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure)在 Azure 中 (或 hello **/站台/wwwroot/App_Data/工作/**目錄WebJobs)。</span><span class="sxs-lookup"><span data-stu-id="a0d80-127">Copy your files and their respective directory structure toohello [**/site/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (or hello **/site/wwwroot/App_Data/Jobs/** directory for WebJobs).</span></span>
4. <span data-ttu-id="a0d80-128">瀏覽 tooyour 應用程式的 URL tooverify hello 應用程式正常執行。</span><span class="sxs-lookup"><span data-stu-id="a0d80-128">Browse tooyour app's URL tooverify hello app is running properly.</span></span> 

> [!NOTE] 
> <span data-ttu-id="a0d80-129">不同於[Git 架構部署](app-service-deploy-local-git.md)，FTP 部署不支援下列部署不僅 hello:</span><span class="sxs-lookup"><span data-stu-id="a0d80-129">Unlike [Git-based deployments](app-service-deploy-local-git.md), FTP deployment doesn't support hello following deployment automations:</span></span> 
>
> - <span data-ttu-id="a0d80-130">相依性還原 (例如 NuGet、NPM、PIP 和編輯器自動化)</span><span class="sxs-lookup"><span data-stu-id="a0d80-130">dependency restore (such as NuGet, NPM, PIP, and Composer automations)</span></span>
> - <span data-ttu-id="a0d80-131">.NET 二進位檔的編譯</span><span class="sxs-lookup"><span data-stu-id="a0d80-131">compilation of .NET binaries</span></span>
> - <span data-ttu-id="a0d80-132">web.config 的產生 (此處是 [Node.js 範例](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span><span class="sxs-lookup"><span data-stu-id="a0d80-132">generation of web.config (here is a [Node.js example](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span></span>
> 
> <span data-ttu-id="a0d80-133">您必須在您的本機電腦上手動還原、建置及產生這些必要的檔案，並與您的應用程式一起部署它們。</span><span class="sxs-lookup"><span data-stu-id="a0d80-133">You must restore, build, and generate these necessary files manually on your local machine and deploy them together with your app.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="a0d80-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a0d80-134">Next steps</span></span>

<span data-ttu-id="a0d80-135">如需更多進階部署案例中，請嘗試[部署與 Git tooAzure](app-service-deploy-local-git.md)。</span><span class="sxs-lookup"><span data-stu-id="a0d80-135">For more advanced deployment scenarios, try [deploying tooAzure with Git](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="a0d80-136">Git 部署 tooAzure 啟用版本控制、 封裝還原，MSBuild，等等。</span><span class="sxs-lookup"><span data-stu-id="a0d80-136">Git-based deployment tooAzure enables version control, package restore, MSBuild, and more.</span></span>

## <a name="more-resources"></a><span data-ttu-id="a0d80-137">其他資源</span><span class="sxs-lookup"><span data-stu-id="a0d80-137">More Resources</span></span>

* <span data-ttu-id="a0d80-138">[建立 PHP-MySQL Web 應用程式並使用 FTP 部署](web-sites-php-mysql-deploy-use-ftp.md)。</span><span class="sxs-lookup"><span data-stu-id="a0d80-138">[Create a PHP-MySQL web app and deploy using FTP](web-sites-php-mysql-deploy-use-ftp.md).</span></span>
* [<span data-ttu-id="a0d80-139">Azure App Service 部署認證</span><span class="sxs-lookup"><span data-stu-id="a0d80-139">Azure App Service Deployment Credentials</span></span>](app-service-deploy-ftp.md)
