---
title: "Linux 上的 Azure App Service Web 應用程式常見問題集 | Microsoft Docs"
description: "Linux 上的 Azure App Service Web 應用程式常見問題集。"
keywords: "azure app service, web 應用程式, 常見問題集, linux, oss"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: 6122f28b35d143ec26a379ae9aa8aee9bdaaff9e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-app-service-web-app-on-linux-faq"></a><span data-ttu-id="9f5fc-104">Linux 上的 Azure App Service Web 應用程式常見問題集</span><span class="sxs-lookup"><span data-stu-id="9f5fc-104">Azure App Service Web App on Linux FAQ</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="9f5fc-105">隨著 Linux 上的 Web 應用程式推出，我們正著手在我們的平台上新增功能和進行改善。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-105">With the release of Web App on Linux, we're working on adding features and making improvements to our platform.</span></span> <span data-ttu-id="9f5fc-106">以下是過去幾個月以來，我們的客戶一直詢問的一些常見問題 (FAQ)。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-106">Here are some frequently asked questions (FAQ) that our customers have been asking us over the last months.</span></span>
<span data-ttu-id="9f5fc-107">如果您有問題，請對文章發表評論，我們會盡速回答。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-107">If you have a question, comment on the article and we'll answer it as soon as possible.</span></span>

## <a name="built-in-images"></a><span data-ttu-id="9f5fc-108">內建映像</span><span class="sxs-lookup"><span data-stu-id="9f5fc-108">Built-in images</span></span>

<span data-ttu-id="9f5fc-109">**問︰**我想要將平台所提供的內建 Docker 容器進行分岔。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-109">**Q:** I want to fork the built-in Docker containers that the platform provides.</span></span> <span data-ttu-id="9f5fc-110">哪裡可以找到這些檔案？</span><span class="sxs-lookup"><span data-stu-id="9f5fc-110">Where can I find those files?</span></span>

<span data-ttu-id="9f5fc-111">**答：**您可以在 [GitHub](https://github.com/azure-app-service) 上找到所有 Docker 檔案。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-111">**A:** You can find all Docker files on [GitHub](https://github.com/azure-app-service).</span></span> <span data-ttu-id="9f5fc-112">您可以在 [Docker Hub](https://hub.docker.com/u/appsvc/) 上找到所有 Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-112">You can find all Docker containers on [Docker Hub](https://hub.docker.com/u/appsvc/).</span></span>

<span data-ttu-id="9f5fc-113">**問︰**設定執行階段堆疊時，在 [啟動檔案] 區段應該使用哪些值？</span><span class="sxs-lookup"><span data-stu-id="9f5fc-113">**Q:** What are the expected values for the Startup File section when I configure the runtime stack?</span></span>

<span data-ttu-id="9f5fc-114">**答︰**針對 Node.Js，您需指定 PM2 組態檔或指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-114">**A:** For Node.Js, you specify the PM2 configuration file or your script file.</span></span> <span data-ttu-id="9f5fc-115">針對 .Net Core，請指定已編譯的 DLL 名稱。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-115">For .NET Core, specify your compiled DLL name.</span></span> <span data-ttu-id="9f5fc-116">針對 Ruby，您可以指定要用來將應用程式初始化的 Ruby 指令碼。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-116">For Ruby, you can specify the Ruby script that you want to initialize your app with.</span></span>

## <a name="management"></a><span data-ttu-id="9f5fc-117">管理</span><span class="sxs-lookup"><span data-stu-id="9f5fc-117">Management</span></span>

<span data-ttu-id="9f5fc-118">**問︰**當我按下 Azure 入口網站中的 [重新啟動] 按鈕時，會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="9f5fc-118">**Q:** What happens when I press the restart button in the Azure portal?</span></span>

<span data-ttu-id="9f5fc-119">**答︰**這相當於 Docker 的重新啟動。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-119">**A:** This is the equivalent of Docker restart.</span></span>

<span data-ttu-id="9f5fc-120">**問：**我是否可以使用「安全殼層」(SSH) 來連線到應用程式容器虛擬機器 (VM)？</span><span class="sxs-lookup"><span data-stu-id="9f5fc-120">**Q:** Can I use Secure Shell (SSH) to connect to the app container virtual machine (VM)?</span></span>

<span data-ttu-id="9f5fc-121">**答︰**是，您可以透過 SCM 網站來這樣做，如需詳細資訊，請查看下列文件：[Linux 上的 Web 應用程式 SSH 支援](./app-service-linux-ssh-support.md)</span><span class="sxs-lookup"><span data-stu-id="9f5fc-121">**A:** Yes, you can do that through the SCM site, check the following article for more information [SSH support for Web App on Linux](./app-service-linux-ssh-support.md)</span></span>

<span data-ttu-id="9f5fc-122">**問：**要如何才能夠透過 SDK 或 ARM 範本來建立 Linux App Service 方案？</span><span class="sxs-lookup"><span data-stu-id="9f5fc-122">**Q:** I want to create a Linux App Service plane through SDK or an ARM template, how can I achieve this?</span></span>

<span data-ttu-id="9f5fc-123">**答：**您必須將 App Service 的 `reserved` 欄位設定為 `true`。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-123">**A:** You need to set the `reserved` field of the app service to `true`.</span></span>

## <a name="continuous-integrationdeployment"></a><span data-ttu-id="9f5fc-124">連續整合/部署</span><span class="sxs-lookup"><span data-stu-id="9f5fc-124">Continuous integration/deployment</span></span>

<span data-ttu-id="9f5fc-125">**問︰**我的 Web 應用程式在我已更新 Docker Hub 上的映像之後，仍然使用舊的 Docker 容器映像。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-125">**Q:** My web app still uses an old Docker container image after I've updated the image on Docker Hub.</span></span> <span data-ttu-id="9f5fc-126">您是否支援自訂容器的連續整合/部署？</span><span class="sxs-lookup"><span data-stu-id="9f5fc-126">Do you support continuous integration/deployment of custom containers?</span></span>

<span data-ttu-id="9f5fc-127">**答︰**如需設定 Azure Container Registry 或 DockerHub 映像的持續整合/部署，請查看下列文件：[在 Linux 上使用 Azure Web 應用程式持續部署](./app-service-linux-ci-cd.md)。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-127">**A:** To set up continuous integration/deployment for Azure Container Registry or DockerHub images by check the following article [Continuous Deployment with Azure Web App on Linux](./app-service-linux-ci-cd.md).</span></span> <span data-ttu-id="9f5fc-128">針對私人登錄，您可以將 Web 應用程式先停止再啟動，來重新整理容器。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-128">For private registries, you can refresh the container by stopping and then starting your web app.</span></span> <span data-ttu-id="9f5fc-129">您也可以變更或新增虛擬應用程式設定，來強制重新整理您的容器。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-129">Or you can change or add a dummy application setting to force a refresh of your container.</span></span>

<span data-ttu-id="9f5fc-130">**問︰**是否支援預備環境？</span><span class="sxs-lookup"><span data-stu-id="9f5fc-130">**Q:** Do you support staging environments?</span></span>

<span data-ttu-id="9f5fc-131">**答：** 是。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-131">**A:** Yes.</span></span>

<span data-ttu-id="9f5fc-132">**問：**我可以使用 **Web 部署**來部署我的 Web 應用程式嗎？</span><span class="sxs-lookup"><span data-stu-id="9f5fc-132">**Q:** Can I use **web deploy** to deploy my web app?</span></span>

<span data-ttu-id="9f5fc-133">**答：**是，您需要將稱為 `WEBSITE_WEBDEPLOY_USE_SCM` 的應用程式設定設定為 `false`。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-133">**A:** Yes, you need to set an app setting called `WEBSITE_WEBDEPLOY_USE_SCM` to `false`.</span></span>

## <a name="language-support"></a><span data-ttu-id="9f5fc-134">語言支援</span><span class="sxs-lookup"><span data-stu-id="9f5fc-134">Language support</span></span>

<span data-ttu-id="9f5fc-135">**問︰**是否支援未編譯的 .NET Core 應用程式？</span><span class="sxs-lookup"><span data-stu-id="9f5fc-135">**Q:** Do you support uncompiled .NET Core apps?</span></span>

<span data-ttu-id="9f5fc-136">**答：** 是。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-136">**A:** Yes.</span></span>

<span data-ttu-id="9f5fc-137">**問︰**您是否支援以 Composer 做為 PHP 應用程式的相依性管理程式？</span><span class="sxs-lookup"><span data-stu-id="9f5fc-137">**Q:** Do you support Composer as a dependency manager for PHP apps?</span></span>

<span data-ttu-id="9f5fc-138">**答：** 是。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-138">**A:** Yes.</span></span> <span data-ttu-id="9f5fc-139">在 Git 部署期間，Kudu 應該會偵測到您要部署 PHP 應用程式 (這點受惠於 composer.json 檔案)，並且會為您觸發編輯器安裝。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-139">During a Git deployment, Kudu should detect that you are deploying a PHP application (thanks to the presence of a composer.json file) and will trigger a composer install for you.</span></span>

## <a name="custom-containers"></a><span data-ttu-id="9f5fc-140">自訂容器</span><span class="sxs-lookup"><span data-stu-id="9f5fc-140">Custom containers</span></span>

<span data-ttu-id="9f5fc-141">**問︰**我使用自己的自訂容器。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-141">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="9f5fc-142">我的應用程式位於 `\home\` 目錄中，但是我使用 [SCM 網站](https://github.com/projectkudu/kudu)或 FTP 用戶端來瀏覽內容時卻找不到檔案。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-142">My app resides in the `\home\` directory, but I can't find my files when I browse the content by using the [SCM site](https://github.com/projectkudu/kudu) or an FTP client.</span></span> <span data-ttu-id="9f5fc-143">我的檔案在哪裡？</span><span class="sxs-lookup"><span data-stu-id="9f5fc-143">Where are my files?</span></span>

<span data-ttu-id="9f5fc-144">**答︰**我們在 `\home\` 目錄掛接了 SMB 共用。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-144">**A:** We mount an SMB share to the `\home\` directory.</span></span> <span data-ttu-id="9f5fc-145">這會覆寫該處的所有內容。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-145">This will override any content that's there.</span></span>

<span data-ttu-id="9f5fc-146">**問︰**我使用自己的自訂容器。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-146">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="9f5fc-147">我不需要平台將 SMB 共用掛接至 `\home\`。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-147">I don't want the platform to mount an SMB share to the `\home\`.</span></span>

<span data-ttu-id="9f5fc-148">**答：**您可以將 `WEBSITES_ENABLE_APP_SERVICE_STORAGE` 應用程式設定設為 `false` 來執行此動作。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-148">**A:** You can do that by setting the `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting to `false`.</span></span>

<span data-ttu-id="9f5fc-149">**問：**我的自訂容器需要很長時間才能啟動，而平台會在它完成啟動之前將容器重新啟動。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-149">**Q:** My custom container takes a long time to start, and the platform restart the container before it finishes starting up.</span></span>

<span data-ttu-id="9f5fc-150">**答：**您可以設定在重新啟動容器之前，平台所要等待的時間。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-150">**A:** You can configure the time the platform will wait before restarting your container.</span></span> <span data-ttu-id="9f5fc-151">可藉由將 `WEBSITES_CONTAINER_START_TIME_LIMIT` 應用程式設定設為所需的值 (以秒為單位) 來執行此動作。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-151">This can be done by setting the `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting to the desired value in seconds.</span></span> <span data-ttu-id="9f5fc-152">預設為 230 秒，最大值為 600 秒。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-152">The default is 230 seconds, and the max is 600 seconds.</span></span>

<span data-ttu-id="9f5fc-153">**問︰**私人登錄伺服器 URL 的格式為何？</span><span class="sxs-lookup"><span data-stu-id="9f5fc-153">**Q:** What is the format for private registry server url?</span></span>

<span data-ttu-id="9f5fc-154">**答︰**您需要提供包括 `http://` 或 `https://` 的完整登錄 URL。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-154">**A:** You need to provide the full registry url including `http://` or `https://`.</span></span>

<span data-ttu-id="9f5fc-155">**問︰**私人登錄選項中的映像名稱格式為何？</span><span class="sxs-lookup"><span data-stu-id="9f5fc-155">**Q:** What is the format for the image name in private registry option?</span></span>

<span data-ttu-id="9f5fc-156">**答︰**您需要新增包括私人登錄 URL 的完整映像名稱 (例如</span><span class="sxs-lookup"><span data-stu-id="9f5fc-156">**A:** You need to add the full image name including the private registry url (eg.</span></span> <span data-ttu-id="9f5fc-157">myacr.azurecr.io/dotnet:latest)</span><span class="sxs-lookup"><span data-stu-id="9f5fc-157">myacr.azurecr.io/dotnet:latest)</span></span>

<span data-ttu-id="9f5fc-158">**問︰**我想要在我的自訂容器映像上公開多個連接埠。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-158">**Q:** I want to expose more than one port on my custom container image.</span></span> <span data-ttu-id="9f5fc-159">是否可行？</span><span class="sxs-lookup"><span data-stu-id="9f5fc-159">Is that possible?</span></span>

<span data-ttu-id="9f5fc-160">**答：**目前不支援此做法。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-160">**A:** Currently, that isn't supported.</span></span>

<span data-ttu-id="9f5fc-161">**問︰**我可以攜帶自己的儲存體嗎？</span><span class="sxs-lookup"><span data-stu-id="9f5fc-161">**Q:** Can I bring my own storage?</span></span>

<span data-ttu-id="9f5fc-162">**答：**目前不支援此做法。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-162">**A:** Currently that isn't supported.</span></span>

<span data-ttu-id="9f5fc-163">**問︰**我無法從 SCM 網站瀏覽自訂容器的檔案系統或執行中處理序。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-163">**Q:** I can't browse my custom container's file system or running processes from the SCM site.</span></span> <span data-ttu-id="9f5fc-164">這是為什麼？</span><span class="sxs-lookup"><span data-stu-id="9f5fc-164">Why is that?</span></span>

<span data-ttu-id="9f5fc-165">**答︰**SCM 網站是在個別的容器中執行。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-165">**A:** The SCM site runs in a separate container.</span></span> <span data-ttu-id="9f5fc-166">您無法檢查應用程式容器的檔案系統或執行中的處理程序。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-166">You can't check the file system or running processes of the app container.</span></span>

<span data-ttu-id="9f5fc-167">**問︰**我的自訂容器接聽連接埠 80 以外的連接埠。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-167">**Q:** My custom container listens to a port other than port 80.</span></span> <span data-ttu-id="9f5fc-168">如何設定我的應用程式將要求路由至該連接埠？</span><span class="sxs-lookup"><span data-stu-id="9f5fc-168">How can I configure my app to route the requests to that port?</span></span>

<span data-ttu-id="9f5fc-169">**答︰**我們會自動偵測連接埠，您也可以指定一個名為 [WEBSITES_PORT] 的應用程式設定，為它提供一個預期的連接埠號碼值。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-169">**A:** We have auto port detection, also you can specify an application setting called **WEBSITES_PORT**, and give it the value of the expected port number.</span></span> <span data-ttu-id="9f5fc-170">先前平台使用 `PORT` 應用程式設定，我們計劃取代此應用程式設定的使用，並改為專門使用 `WEBSITES_PORT`。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-170">Previously the platform was using `PORT` app setting, we are planning to deprecate the use this app setting and move to using `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="9f5fc-171">**問︰**我是否需要在我的自訂容器中實作 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-171">**Q:** Do I need to implement HTTPS in my custom container.</span></span>

<span data-ttu-id="9f5fc-172">**答︰**不需要，平台會在共用的前端處理 HTTPS 終止。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-172">**A:** No, the platform handles HTTPS termination at the shared frontends.</span></span>

## <a name="pricing-and-sla"></a><span data-ttu-id="9f5fc-173">價格和 SLA</span><span class="sxs-lookup"><span data-stu-id="9f5fc-173">Pricing and SLA</span></span>

<span data-ttu-id="9f5fc-174">**問︰**使用公開預覽版時是價格是多少？</span><span class="sxs-lookup"><span data-stu-id="9f5fc-174">**Q:** What's the pricing while you're using the public preview?</span></span>

<span data-ttu-id="9f5fc-175">**答︰**我們會以標準 Azure App Service 定價，向您收取應用程式執行時數一半的費用。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-175">**A:** You are charged half the number of hours that your app runs, with the normal Azure App Service pricing.</span></span> <span data-ttu-id="9f5fc-176">這表示您會獲得標準 Azure App Service 定價的五折優惠。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-176">This means that you get a 50 percent discount on normal Azure App Service pricing.</span></span>

## <a name="other"></a><span data-ttu-id="9f5fc-177">其他</span><span class="sxs-lookup"><span data-stu-id="9f5fc-177">Other</span></span>

<span data-ttu-id="9f5fc-178">**問︰**應用程式設定名稱所支援的字元為何？</span><span class="sxs-lookup"><span data-stu-id="9f5fc-178">**Q:** What are the supported characters in application settings names?</span></span>

<span data-ttu-id="9f5fc-179">**答︰**針對應用程式設定，您只能使用 A-Z、a-z、0-9 以及底線。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-179">**A:** You can only use A-Z, a-z, 0-9, and the underscore for application settings.</span></span>

<span data-ttu-id="9f5fc-180">**問︰**我可以在何處提出新功能的要求？</span><span class="sxs-lookup"><span data-stu-id="9f5fc-180">**Q:** Where can I request new features?</span></span>

<span data-ttu-id="9f5fc-181">**答︰**您可以在 [Web Apps 意見反應論壇 (英文)](https://aka.ms/webapps-uservoice) 提交您的想法。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-181">**A:** You can submit your idea at the [Web Apps feedback forum](https://aka.ms/webapps-uservoice).</span></span> <span data-ttu-id="9f5fc-182">將 "[Linux]" 新增至您想法的標題。</span><span class="sxs-lookup"><span data-stu-id="9f5fc-182">Add "[Linux]" to the title of your idea.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f5fc-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9f5fc-183">Next steps</span></span>
* [<span data-ttu-id="9f5fc-184">什麼是 Linux 上的 Azure Web 應用程式？</span><span class="sxs-lookup"><span data-stu-id="9f5fc-184">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="9f5fc-185">Linux 上的 Azure Web 應用程式 SSH 支援</span><span class="sxs-lookup"><span data-stu-id="9f5fc-185">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="9f5fc-186">在 Azure App Service 中設定預備環境</span><span class="sxs-lookup"><span data-stu-id="9f5fc-186">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="9f5fc-187">在 Linux 上使用 Azure Web 應用程式持續部署</span><span class="sxs-lookup"><span data-stu-id="9f5fc-187">Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)
