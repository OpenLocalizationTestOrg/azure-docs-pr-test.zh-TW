---
title: "aaaAzure App Service Web 應用程式，在 Linux 常見問題集 |Microsoft 文件"
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
ms.openlocfilehash: c7798d9144d936eecdc0e191fc870b0ee0b220c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-web-app-on-linux-faq"></a><span data-ttu-id="739b9-104">Linux 上的 Azure App Service Web 應用程式常見問題集</span><span class="sxs-lookup"><span data-stu-id="739b9-104">Azure App Service Web App on Linux FAQ</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="739b9-105">Hello 版本在 Linux 上的 Web 應用程式中，我們正努力加入功能，並進行改善 tooour 平台。</span><span class="sxs-lookup"><span data-stu-id="739b9-105">With hello release of Web App on Linux, we're working on adding features and making improvements tooour platform.</span></span> <span data-ttu-id="739b9-106">以下是一些常見問題集 (FAQ)，我們的客戶有已要求我們透過 hello 最後幾個月。</span><span class="sxs-lookup"><span data-stu-id="739b9-106">Here are some frequently asked questions (FAQ) that our customers have been asking us over hello last months.</span></span>
<span data-ttu-id="739b9-107">如果您有問題，hello 發行項上的註解，我們會儘速回答。</span><span class="sxs-lookup"><span data-stu-id="739b9-107">If you have a question, comment on hello article and we'll answer it as soon as possible.</span></span>

## <a name="built-in-images"></a><span data-ttu-id="739b9-108">內建映像</span><span class="sxs-lookup"><span data-stu-id="739b9-108">Built-in images</span></span>

<span data-ttu-id="739b9-109">**問：**我想 toofork hello 內建 Docker 容器 hello 平台所提供。</span><span class="sxs-lookup"><span data-stu-id="739b9-109">**Q:** I want toofork hello built-in Docker containers that hello platform provides.</span></span> <span data-ttu-id="739b9-110">哪裡可以找到這些檔案？</span><span class="sxs-lookup"><span data-stu-id="739b9-110">Where can I find those files?</span></span>

<span data-ttu-id="739b9-111">**答：**您可以在 [GitHub](https://github.com/azure-app-service) 上找到所有 Docker 檔案。</span><span class="sxs-lookup"><span data-stu-id="739b9-111">**A:** You can find all Docker files on [GitHub](https://github.com/azure-app-service).</span></span> <span data-ttu-id="739b9-112">您可以在 [Docker Hub](https://hub.docker.com/u/appsvc/) 上找到所有 Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="739b9-112">You can find all Docker containers on [Docker Hub](https://hub.docker.com/u/appsvc/).</span></span>

<span data-ttu-id="739b9-113">**問：**為何 hello 預期 hello 啟動檔案區段的值時設定執行階段堆疊時會 hello？</span><span class="sxs-lookup"><span data-stu-id="739b9-113">**Q:** What are hello expected values for hello Startup File section when I configure hello runtime stack?</span></span>

<span data-ttu-id="739b9-114">**答：** For Node.Js 您指定 hello PM2 組態檔或指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="739b9-114">**A:** For Node.Js, you specify hello PM2 configuration file or your script file.</span></span> <span data-ttu-id="739b9-115">針對 .Net Core，請指定已編譯的 DLL 名稱。</span><span class="sxs-lookup"><span data-stu-id="739b9-115">For .NET Core, specify your compiled DLL name.</span></span> <span data-ttu-id="739b9-116">Ruby，您可以指定 hello 拼音指令碼的 tooinitialize 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="739b9-116">For Ruby, you can specify hello Ruby script that you want tooinitialize your app with.</span></span>

## <a name="management"></a><span data-ttu-id="739b9-117">管理</span><span class="sxs-lookup"><span data-stu-id="739b9-117">Management</span></span>

<span data-ttu-id="739b9-118">**問：**當我按 hello Azure 入口網站中的 hello 重新啟動 按鈕時，會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="739b9-118">**Q:** What happens when I press hello restart button in hello Azure portal?</span></span>

<span data-ttu-id="739b9-119">**答：**這是 hello Docker 重新啟動的對等。</span><span class="sxs-lookup"><span data-stu-id="739b9-119">**A:** This is hello equivalent of Docker restart.</span></span>

<span data-ttu-id="739b9-120">**問：**我可以使用安全殼層 (SSH) tooconnect toohello 應用程式容器虛擬機器 (VM)？</span><span class="sxs-lookup"><span data-stu-id="739b9-120">**Q:** Can I use Secure Shell (SSH) tooconnect toohello app container virtual machine (VM)?</span></span>

<span data-ttu-id="739b9-121">**答：**是，您可以透過 hello SCM 網站，文件如需詳細資訊核取 hello 下列[Web 應用程式，在 Linux 上的 SSH 支援](./app-service-linux-ssh-support.md)</span><span class="sxs-lookup"><span data-stu-id="739b9-121">**A:** Yes, you can do that through hello SCM site, check hello following article for more information [SSH support for Web App on Linux](./app-service-linux-ssh-support.md)</span></span>

<span data-ttu-id="739b9-122">**問：**我想 toocreate Linux 應用程式服務平面上，透過 SDK 或 ARM 範本、 如何達成這嗎？</span><span class="sxs-lookup"><span data-stu-id="739b9-122">**Q:** I want toocreate a Linux App Service plane through SDK or an ARM template, how can I achieve this?</span></span>

<span data-ttu-id="739b9-123">**答：**需要 tooset hello `reserved` hello 應用程式的欄位太服務`true`。</span><span class="sxs-lookup"><span data-stu-id="739b9-123">**A:** You need tooset hello `reserved` field of hello app service too`true`.</span></span>

## <a name="continuous-integrationdeployment"></a><span data-ttu-id="739b9-124">連續整合/部署</span><span class="sxs-lookup"><span data-stu-id="739b9-124">Continuous integration/deployment</span></span>

<span data-ttu-id="739b9-125">**問：**我的 web 應用程式仍會使用舊的 Docker 容器映像之後我已更新 hello 銜接站集線器上的映像。</span><span class="sxs-lookup"><span data-stu-id="739b9-125">**Q:** My web app still uses an old Docker container image after I've updated hello image on Docker Hub.</span></span> <span data-ttu-id="739b9-126">您是否支援自訂容器的連續整合/部署？</span><span class="sxs-lookup"><span data-stu-id="739b9-126">Do you support continuous integration/deployment of custom containers?</span></span>

<span data-ttu-id="739b9-127">**答：**連續整合/部署 Azure 容器登錄或 DockerHub 映像的下列文章的核取 hello tooset [on Linux 的 Azure Web 應用程式與連續部署](./app-service-linux-ci-cd.md)。</span><span class="sxs-lookup"><span data-stu-id="739b9-127">**A:** tooset up continuous integration/deployment for Azure Container Registry or DockerHub images by check hello following article [Continuous Deployment with Azure Web App on Linux](./app-service-linux-ci-cd.md).</span></span> <span data-ttu-id="739b9-128">針對私人登錄中，您可以重新整理 hello 容器停止然後啟動您的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="739b9-128">For private registries, you can refresh hello container by stopping and then starting your web app.</span></span> <span data-ttu-id="739b9-129">或者，您可以變更或新增虛擬應用程式設定 tooforce 重新整理您的容器。</span><span class="sxs-lookup"><span data-stu-id="739b9-129">Or you can change or add a dummy application setting tooforce a refresh of your container.</span></span>

<span data-ttu-id="739b9-130">**問︰**是否支援預備環境？</span><span class="sxs-lookup"><span data-stu-id="739b9-130">**Q:** Do you support staging environments?</span></span>

<span data-ttu-id="739b9-131">**答：** 是。</span><span class="sxs-lookup"><span data-stu-id="739b9-131">**A:** Yes.</span></span>

<span data-ttu-id="739b9-132">**問：**我可以使用**web 部署**toodeploy 我的 web 應用程式嗎？</span><span class="sxs-lookup"><span data-stu-id="739b9-132">**Q:** Can I use **web deploy** toodeploy my web app?</span></span>

<span data-ttu-id="739b9-133">**答：**是，您需要 tooset 應用程式稱為`WEBSITE_WEBDEPLOY_USE_SCM`太`false`。</span><span class="sxs-lookup"><span data-stu-id="739b9-133">**A:** Yes, you need tooset an app setting called `WEBSITE_WEBDEPLOY_USE_SCM` too`false`.</span></span>

## <a name="language-support"></a><span data-ttu-id="739b9-134">語言支援</span><span class="sxs-lookup"><span data-stu-id="739b9-134">Language support</span></span>

<span data-ttu-id="739b9-135">**問︰**是否支援未編譯的 .NET Core 應用程式？</span><span class="sxs-lookup"><span data-stu-id="739b9-135">**Q:** Do you support uncompiled .NET Core apps?</span></span>

<span data-ttu-id="739b9-136">**答：** 是。</span><span class="sxs-lookup"><span data-stu-id="739b9-136">**A:** Yes.</span></span>

<span data-ttu-id="739b9-137">**問︰**您是否支援以 Composer 做為 PHP 應用程式的相依性管理程式？</span><span class="sxs-lookup"><span data-stu-id="739b9-137">**Q:** Do you support Composer as a dependency manager for PHP apps?</span></span>

<span data-ttu-id="739b9-138">**答：** 是。</span><span class="sxs-lookup"><span data-stu-id="739b9-138">**A:** Yes.</span></span> <span data-ttu-id="739b9-139">Git 在部署期間，Kudu 應該會偵測到您要部署的 PHP 應用程式 （感謝您 toohello composer.json 檔案存在），並將觸發程序為您的編輯器 」 安裝。</span><span class="sxs-lookup"><span data-stu-id="739b9-139">During a Git deployment, Kudu should detect that you are deploying a PHP application (thanks toohello presence of a composer.json file) and will trigger a composer install for you.</span></span>

## <a name="custom-containers"></a><span data-ttu-id="739b9-140">自訂容器</span><span class="sxs-lookup"><span data-stu-id="739b9-140">Custom containers</span></span>

<span data-ttu-id="739b9-141">**問︰**我使用自己的自訂容器。</span><span class="sxs-lookup"><span data-stu-id="739b9-141">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="739b9-142">我的應用程式位於 hello`\home\`目錄，但我找不到我的檔案時使用 hello 瀏覽 hello 內容[SCM 網站](https://github.com/projectkudu/kudu)或 FTP 用戶端。</span><span class="sxs-lookup"><span data-stu-id="739b9-142">My app resides in hello `\home\` directory, but I can't find my files when I browse hello content by using hello [SCM site](https://github.com/projectkudu/kudu) or an FTP client.</span></span> <span data-ttu-id="739b9-143">我的檔案在哪裡？</span><span class="sxs-lookup"><span data-stu-id="739b9-143">Where are my files?</span></span>

<span data-ttu-id="739b9-144">**答：**掛接 SMB 共用 toohello`\home\`目錄。</span><span class="sxs-lookup"><span data-stu-id="739b9-144">**A:** We mount an SMB share toohello `\home\` directory.</span></span> <span data-ttu-id="739b9-145">這會覆寫該處的所有內容。</span><span class="sxs-lookup"><span data-stu-id="739b9-145">This will override any content that's there.</span></span>

<span data-ttu-id="739b9-146">**問︰**我使用自己的自訂容器。</span><span class="sxs-lookup"><span data-stu-id="739b9-146">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="739b9-147">我不想 hello 平台 toomount SMB 共用 toohello `\home\`。</span><span class="sxs-lookup"><span data-stu-id="739b9-147">I don't want hello platform toomount an SMB share toohello `\home\`.</span></span>

<span data-ttu-id="739b9-148">**答：**您可以執行此動作設定 hello`WEBSITES_ENABLE_APP_SERVICE_STORAGE`應用程式設定過`false`。</span><span class="sxs-lookup"><span data-stu-id="739b9-148">**A:** You can do that by setting hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting too`false`.</span></span>

<span data-ttu-id="739b9-149">**問：**我自訂容器會很長的時間 toostart，和 hello 平台重新啟動之前的 hello 容器完成啟動。</span><span class="sxs-lookup"><span data-stu-id="739b9-149">**Q:** My custom container takes a long time toostart, and hello platform restart hello container before it finishes starting up.</span></span>

<span data-ttu-id="739b9-150">**答：**您可以設定 hello hello 平台會重新啟動您的容器之前等候的時間。</span><span class="sxs-lookup"><span data-stu-id="739b9-150">**A:** You can configure hello time hello platform will wait before restarting your container.</span></span> <span data-ttu-id="739b9-151">這可藉由設定 hello`WEBSITES_CONTAINER_START_TIME_LIMIT`應用程式設定 toohello 所需值，以秒為單位。</span><span class="sxs-lookup"><span data-stu-id="739b9-151">This can be done by setting hello `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting toohello desired value in seconds.</span></span> <span data-ttu-id="739b9-152">hello 預設 230 秒，而且 hello 最大值為 600 秒。</span><span class="sxs-lookup"><span data-stu-id="739b9-152">hello default is 230 seconds, and hello max is 600 seconds.</span></span>

<span data-ttu-id="739b9-153">**問：** hello 私人登錄伺服器 url 的格式是什麼？</span><span class="sxs-lookup"><span data-stu-id="739b9-153">**Q:** What is hello format for private registry server url?</span></span>

<span data-ttu-id="739b9-154">**答：**您需要 tooprovide hello 完整登錄 url 包括`http://`或`https://`。</span><span class="sxs-lookup"><span data-stu-id="739b9-154">**A:** You need tooprovide hello full registry url including `http://` or `https://`.</span></span>

<span data-ttu-id="739b9-155">**問：** hello 私人登錄選項中的 hello 映像名稱格式是什麼？</span><span class="sxs-lookup"><span data-stu-id="739b9-155">**Q:** What is hello format for hello image name in private registry option?</span></span>

<span data-ttu-id="739b9-156">**答：**需要 tooadd hello 完整的映像名稱包括 hello 私人登錄 url （例如。</span><span class="sxs-lookup"><span data-stu-id="739b9-156">**A:** You need tooadd hello full image name including hello private registry url (eg.</span></span> <span data-ttu-id="739b9-157">myacr.azurecr.io/dotnet:latest)</span><span class="sxs-lookup"><span data-stu-id="739b9-157">myacr.azurecr.io/dotnet:latest)</span></span>

<span data-ttu-id="739b9-158">**問：**我想要 tooexpose 多個連接埠上我的自訂容器映像。</span><span class="sxs-lookup"><span data-stu-id="739b9-158">**Q:** I want tooexpose more than one port on my custom container image.</span></span> <span data-ttu-id="739b9-159">是否可行？</span><span class="sxs-lookup"><span data-stu-id="739b9-159">Is that possible?</span></span>

<span data-ttu-id="739b9-160">**答：**目前不支援此做法。</span><span class="sxs-lookup"><span data-stu-id="739b9-160">**A:** Currently, that isn't supported.</span></span>

<span data-ttu-id="739b9-161">**問︰**我可以攜帶自己的儲存體嗎？</span><span class="sxs-lookup"><span data-stu-id="739b9-161">**Q:** Can I bring my own storage?</span></span>

<span data-ttu-id="739b9-162">**答：**目前不支援此做法。</span><span class="sxs-lookup"><span data-stu-id="739b9-162">**A:** Currently that isn't supported.</span></span>

<span data-ttu-id="739b9-163">**問：**無法瀏覽我的自訂容器檔案系統 」 或 「 執行處理序從 hello SCM 站台。</span><span class="sxs-lookup"><span data-stu-id="739b9-163">**Q:** I can't browse my custom container's file system or running processes from hello SCM site.</span></span> <span data-ttu-id="739b9-164">這是為什麼？</span><span class="sxs-lookup"><span data-stu-id="739b9-164">Why is that?</span></span>

<span data-ttu-id="739b9-165">**答：** hello SCM 站台執行不同的容器中。</span><span class="sxs-lookup"><span data-stu-id="739b9-165">**A:** hello SCM site runs in a separate container.</span></span> <span data-ttu-id="739b9-166">您無法檢查 hello 檔案系統或執行中的 hello 應用程式容器的處理序。</span><span class="sxs-lookup"><span data-stu-id="739b9-166">You can't check hello file system or running processes of hello app container.</span></span>

<span data-ttu-id="739b9-167">**問：**我自訂容器會接聽通訊埠 80 以外的 tooa 連接埠。</span><span class="sxs-lookup"><span data-stu-id="739b9-167">**Q:** My custom container listens tooa port other than port 80.</span></span> <span data-ttu-id="739b9-168">如何設定我的應用程式 tooroute hello 要求 toothat 的連接埠？</span><span class="sxs-lookup"><span data-stu-id="739b9-168">How can I configure my app tooroute hello requests toothat port?</span></span>

<span data-ttu-id="739b9-169">**答：**我們有自動偵測連接埠，而且您可以指定應用程式稱為**WEBSITES_PORT**，並給定 hello hello 預期的連接埠號碼的值。</span><span class="sxs-lookup"><span data-stu-id="739b9-169">**A:** We have auto port detection, also you can specify an application setting called **WEBSITES_PORT**, and give it hello value of hello expected port number.</span></span> <span data-ttu-id="739b9-170">Hello 平台使用先前`PORT`應用程式設定，我們要規劃 toodeprecate hello 使用此設定的應用程式和移動 toousing`WEBSITES_PORT`獨佔。</span><span class="sxs-lookup"><span data-stu-id="739b9-170">Previously hello platform was using `PORT` app setting, we are planning toodeprecate hello use this app setting and move toousing `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="739b9-171">**問：**就需要 tooimplement HTTPS 我自訂容器中。</span><span class="sxs-lookup"><span data-stu-id="739b9-171">**Q:** Do I need tooimplement HTTPS in my custom container.</span></span>

<span data-ttu-id="739b9-172">**答：** hello 平台不可以，會處理在共用的 hello 前端的 HTTPS 終止。</span><span class="sxs-lookup"><span data-stu-id="739b9-172">**A:** No, hello platform handles HTTPS termination at hello shared frontends.</span></span>

## <a name="pricing-and-sla"></a><span data-ttu-id="739b9-173">價格和 SLA</span><span class="sxs-lookup"><span data-stu-id="739b9-173">Pricing and SLA</span></span>

<span data-ttu-id="739b9-174">**問：**什麼 hello 定價使用 hello 公用預覽？</span><span class="sxs-lookup"><span data-stu-id="739b9-174">**Q:** What's hello pricing while you're using hello public preview?</span></span>

<span data-ttu-id="739b9-175">**答：**負責半 hello 的小時數 hello 一般的 Azure 應用程式服務定價與您的應用程式執行。</span><span class="sxs-lookup"><span data-stu-id="739b9-175">**A:** You are charged half hello number of hours that your app runs, with hello normal Azure App Service pricing.</span></span> <span data-ttu-id="739b9-176">這表示您會獲得標準 Azure App Service 定價的五折優惠。</span><span class="sxs-lookup"><span data-stu-id="739b9-176">This means that you get a 50 percent discount on normal Azure App Service pricing.</span></span>

## <a name="other"></a><span data-ttu-id="739b9-177">其他</span><span class="sxs-lookup"><span data-stu-id="739b9-177">Other</span></span>

<span data-ttu-id="739b9-178">**問：** hello 支援應用程式設定名稱中的字元是什麼？</span><span class="sxs-lookup"><span data-stu-id="739b9-178">**Q:** What are hello supported characters in application settings names?</span></span>

<span data-ttu-id="739b9-179">**答：**只能使用 A-Z、 a-z、 0-9 和 hello 應用程式設定的底線。</span><span class="sxs-lookup"><span data-stu-id="739b9-179">**A:** You can only use A-Z, a-z, 0-9, and hello underscore for application settings.</span></span>

<span data-ttu-id="739b9-180">**問︰**我可以在何處提出新功能的要求？</span><span class="sxs-lookup"><span data-stu-id="739b9-180">**Q:** Where can I request new features?</span></span>

<span data-ttu-id="739b9-181">**答：**可以送出您的想法在 hello [Web 應用程式的意見反應論壇](https://aka.ms/webapps-uservoice)。</span><span class="sxs-lookup"><span data-stu-id="739b9-181">**A:** You can submit your idea at hello [Web Apps feedback forum](https://aka.ms/webapps-uservoice).</span></span> <span data-ttu-id="739b9-182">加入您的想法的"[Linux]"toohello 標題。</span><span class="sxs-lookup"><span data-stu-id="739b9-182">Add "[Linux]" toohello title of your idea.</span></span>

## <a name="next-steps"></a><span data-ttu-id="739b9-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="739b9-183">Next steps</span></span>
* [<span data-ttu-id="739b9-184">什麼是 Linux 上的 Azure Web 應用程式？</span><span class="sxs-lookup"><span data-stu-id="739b9-184">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="739b9-185">Linux 上的 Azure Web 應用程式 SSH 支援</span><span class="sxs-lookup"><span data-stu-id="739b9-185">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="739b9-186">在 Azure App Service 中設定預備環境</span><span class="sxs-lookup"><span data-stu-id="739b9-186">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="739b9-187">在 Linux 上使用 Azure Web 應用程式持續部署</span><span class="sxs-lookup"><span data-stu-id="739b9-187">Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)
