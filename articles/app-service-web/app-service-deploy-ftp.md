---
title: "使用 FTP/S 將您的應用程式部署至 Azure App Service | Microsoft Docs"
description: "了解如何使用 FTP 或 FTPS 將您的應用程式部署至 Azure App Service。"
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
ms.openlocfilehash: 9078abbc4ed7eff6975201443992f7bbb84bf57c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-your-app-to-azure-app-service-using-ftps"></a><span data-ttu-id="cd086-103">使用 FTP/S 將您的應用程式部署至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="cd086-103">Deploy your app to Azure App Service using FTP/S</span></span>

<span data-ttu-id="cd086-104">這篇文章說明如何使用 FTP 或 FTPS 將您的 Web 應用程式、行動裝置應用程式後端或 API 應用程式部署到 [Azure App Service (英文)](http://go.microsoft.com/fwlink/?LinkId=529714)。</span><span class="sxs-lookup"><span data-stu-id="cd086-104">This article shows you how to use FTP or FTPS to deploy your web app, mobile app backend, or API app to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="cd086-105">您應用程式的 FTP/S 端點已經啟動。</span><span class="sxs-lookup"><span data-stu-id="cd086-105">The FTP/S endpoint for your app is already active.</span></span> <span data-ttu-id="cd086-106">啟用 FTP/S 部署不需要任何組態。</span><span class="sxs-lookup"><span data-stu-id="cd086-106">No configuration is necessary to enable FTP/S deployment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cd086-107">我們將持續逐步改善 Microsoft Azure 平台安全性。</span><span class="sxs-lookup"><span data-stu-id="cd086-107">We are continuously taking steps to improve Microsoft Azure Platform security.</span></span> <span data-ttu-id="cd086-108">在此持續努力的過程中，我們規劃升級德國中部和德國東北部地區的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cd086-108">As part of this ongoing effort an upgrade of Web Applications is planned for Germany Central and Germany Northeast regions.</span></span> <span data-ttu-id="cd086-109">在此 Web Apps 期間，將會停止使用純文字 FTP 通訊協定進行部署。</span><span class="sxs-lookup"><span data-stu-id="cd086-109">During this Web Apps will be disabling the use of plain text FTP protocol for deployments.</span></span> <span data-ttu-id="cd086-110">建議客戶切換至 FTPS 進行部署。</span><span class="sxs-lookup"><span data-stu-id="cd086-110">Our recommendation to our customers is to switch to FTPS for deployments.</span></span> <span data-ttu-id="cd086-111">此升級預定在 9/5 進行，在這段期間預期不會對您的服務造成任何中斷。</span><span class="sxs-lookup"><span data-stu-id="cd086-111">We do not expect any disruption to your service during this upgrade which is planned for 9/5.</span></span> <span data-ttu-id="cd086-112">感謝您支援這項工作。</span><span class="sxs-lookup"><span data-stu-id="cd086-112">We appreciate you support in this effort.</span></span>

<a name="step1"></a>
## <a name="step-1-set-deployment-credentials"></a><span data-ttu-id="cd086-113">步驟 1：設定部署認證</span><span class="sxs-lookup"><span data-stu-id="cd086-113">Step 1: Set deployment credentials</span></span>

<span data-ttu-id="cd086-114">若要存取您應用程式的 FTP 伺服器，您必須先部署認證。</span><span class="sxs-lookup"><span data-stu-id="cd086-114">To access the FTP server for your app, you first need deployment credentials.</span></span> 

<span data-ttu-id="cd086-115">若要設定或重設部署認證，請參閱 [Azure App Service 部署認證](app-service-deployment-credentials.md)。</span><span class="sxs-lookup"><span data-stu-id="cd086-115">To set or reset your deployment credentials, see [Azure App Service Deployment Credentials](app-service-deployment-credentials.md).</span></span> <span data-ttu-id="cd086-116">本教學課程示範如何使用使用者層級的認證。</span><span class="sxs-lookup"><span data-stu-id="cd086-116">This tutorial demonstrates the use of user-level credentials.</span></span>

## <a name="step-2-get-ftp-connection-information"></a><span data-ttu-id="cd086-117">步驟 2：取得 FTP 連線資訊</span><span class="sxs-lookup"><span data-stu-id="cd086-117">Step 2: Get FTP connection information</span></span>

1. <span data-ttu-id="cd086-118">在 [Azure 入口網站](https://portal.azure.com)中，開啟應用程式的[資源刀鋒視窗](../azure-resource-manager/resource-group-portal.md#manage-resources)。</span><span class="sxs-lookup"><span data-stu-id="cd086-118">In the [Azure portal](https://portal.azure.com), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="cd086-119">在左側功能表中選取 [概觀]，然後記下 [FTP/部署使用者]、[FTP 主機名稱] 和 [FTPS 主機名稱] 的值。</span><span class="sxs-lookup"><span data-stu-id="cd086-119">Select **Overview** in the left menu, then note the values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span> 

    ![FTP 連線資訊](./media/web-sites-deploy/FTP-Connection-Info.PNG)

    > [!NOTE]
    > <span data-ttu-id="cd086-121">Azure 入口網站顯示的 **FTP/部署使用者** 的使用者值，包括應用程式名稱，以針對 FTP 伺服器提供適當的內容。</span><span class="sxs-lookup"><span data-stu-id="cd086-121">The **FTP/Deployment User** user value as displayed by the Azure Portal including the app name in order to provide proper context for the FTP server.</span></span>
    > <span data-ttu-id="cd086-122">當您在左側功能表中選取 [屬性] 時，可以找到相同資訊。</span><span class="sxs-lookup"><span data-stu-id="cd086-122">You can find the same information when you select **Properties** in the left menu.</span></span> 
    >
    > <span data-ttu-id="cd086-123">此外，絕對不會顯示部署密碼。</span><span class="sxs-lookup"><span data-stu-id="cd086-123">Also, the deployment password is never shown.</span></span> <span data-ttu-id="cd086-124">如果您忘記您的部署密碼，請回到[步驟 1](#step1) 並重設您的部署密碼。</span><span class="sxs-lookup"><span data-stu-id="cd086-124">If you forget your deployment password, go back to [step 1](#step1) and reset your deployment password.</span></span>
    >
    >

## <a name="step-3-deploy-files-to-azure"></a><span data-ttu-id="cd086-125">步驟 3︰將檔案部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="cd086-125">Step 3: Deploy files to Azure</span></span>

1. <span data-ttu-id="cd086-126">從您的 FTP 用戶端 ([Visual Studio](https://www.visualstudio.com/vs/community/)、[FileZilla](https://filezilla-project.org/download.php?type=client) 等等)，使用您所蒐集的連接資訊以連接到您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="cd086-126">From your FTP client ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), etc), use the connection information you gathered to connect to your app.</span></span>
3. <span data-ttu-id="cd086-127">將您的檔案和其個別的目錄結構複製到 Azure 中的 [**/site/wwwroot** 目錄](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) (或 WebJobs 的 **/site/wwwroot/App_Data/Jobs/** 目錄)。</span><span class="sxs-lookup"><span data-stu-id="cd086-127">Copy your files and their respective directory structure to the [**/site/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (or the **/site/wwwroot/App_Data/Jobs/** directory for WebJobs).</span></span>
4. <span data-ttu-id="cd086-128">瀏覽至您的應用程式 URL，以確認應用程式運作正常。</span><span class="sxs-lookup"><span data-stu-id="cd086-128">Browse to your app's URL to verify the app is running properly.</span></span> 

> [!NOTE] 
> <span data-ttu-id="cd086-129">與 [Git 型部署](app-service-deploy-local-git.md)不同，FTP 部署不支援下列的部署自動化︰</span><span class="sxs-lookup"><span data-stu-id="cd086-129">Unlike [Git-based deployments](app-service-deploy-local-git.md), FTP deployment doesn't support the following deployment automations:</span></span> 
>
> - <span data-ttu-id="cd086-130">相依性還原 (例如 NuGet、NPM、PIP 和編輯器自動化)</span><span class="sxs-lookup"><span data-stu-id="cd086-130">dependency restore (such as NuGet, NPM, PIP, and Composer automations)</span></span>
> - <span data-ttu-id="cd086-131">.NET 二進位檔的編譯</span><span class="sxs-lookup"><span data-stu-id="cd086-131">compilation of .NET binaries</span></span>
> - <span data-ttu-id="cd086-132">web.config 的產生 (此處是 [Node.js 範例](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span><span class="sxs-lookup"><span data-stu-id="cd086-132">generation of web.config (here is a [Node.js example](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span></span>
> 
> <span data-ttu-id="cd086-133">您必須在您的本機電腦上手動還原、建置及產生這些必要的檔案，並與您的應用程式一起部署它們。</span><span class="sxs-lookup"><span data-stu-id="cd086-133">You must restore, build, and generate these necessary files manually on your local machine and deploy them together with your app.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="cd086-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cd086-134">Next steps</span></span>

<span data-ttu-id="cd086-135">如需更多的進階部署案例，請嘗試[使用 Git 部署至 Azure ](app-service-deploy-local-git.md)。</span><span class="sxs-lookup"><span data-stu-id="cd086-135">For more advanced deployment scenarios, try [deploying to Azure with Git](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="cd086-136">Git 型部署至 Azure 可啟用版本控制、封裝還原、MSBuild 等等。</span><span class="sxs-lookup"><span data-stu-id="cd086-136">Git-based deployment to Azure enables version control, package restore, MSBuild, and more.</span></span>

## <a name="more-resources"></a><span data-ttu-id="cd086-137">其他資源</span><span class="sxs-lookup"><span data-stu-id="cd086-137">More Resources</span></span>

* <span data-ttu-id="cd086-138">[建立 PHP-MySQL Web 應用程式並使用 FTP 部署](web-sites-php-mysql-deploy-use-ftp.md)。</span><span class="sxs-lookup"><span data-stu-id="cd086-138">[Create a PHP-MySQL web app and deploy using FTP](web-sites-php-mysql-deploy-use-ftp.md).</span></span>
* [<span data-ttu-id="cd086-139">Azure App Service 部署認證</span><span class="sxs-lookup"><span data-stu-id="cd086-139">Azure App Service Deployment Credentials</span></span>](app-service-deploy-ftp.md)
