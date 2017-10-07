---
title: "aaaHow toouse 自訂的 Docker 映像，在 Linux 上的 Azure Web 應用程式 |Microsoft 文件"
description: "如何在 Linux 上的 Azure Web 應用程式的映像 toouse 自訂的 Docker。"
keywords: "azure app service, web 應用程式, linux, docker, 容器"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: b97bd4e6-dff0-4976-ac20-d5c109a559a8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 8853095d0e1067cfea4297bbd23b622fe4a0d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-custom-docker-image-for-azure-web-app-on-linux"></a><span data-ttu-id="987e2-104">針對 Linux 上的 Azure Web 應用程式使用自訂 Docker 映像</span><span class="sxs-lookup"><span data-stu-id="987e2-104">Using a custom Docker image for Azure Web App on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="987e2-105">App Service 在 Linux 上提供預先定義的應用程式堆疊，且支援特定的版本，例如 PHP 7.0 和 Node.js 4.5。</span><span class="sxs-lookup"><span data-stu-id="987e2-105">App Service provides pre-defined application stacks on Linux with support for specific versions, such as PHP 7.0 and Node.js 4.5.</span></span> <span data-ttu-id="987e2-106">在 Linux 上的應用程式服務會使用 Docker 容器 toohost 這些預先建置的應用程式堆疊。</span><span class="sxs-lookup"><span data-stu-id="987e2-106">App Service on Linux uses Docker containers toohost these pre-built application stacks.</span></span> <span data-ttu-id="987e2-107">您也可以使用自訂的 Docker 映像 toodeploy 尚未定義 Azure 中您 web 應用程式 tooan 應用程式堆疊。</span><span class="sxs-lookup"><span data-stu-id="987e2-107">You can also use a custom Docker image toodeploy your web app tooan application stack that is not already defined in Azure.</span></span> <span data-ttu-id="987e2-108">自訂 Docker 映像可裝載於公用或私人 Docker 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="987e2-108">Custom Docker images can be hosted on either a public or private Docker repository.</span></span>


## <a name="how-to-set-a-custom-docker-image-for-a-web-app"></a><span data-ttu-id="987e2-109">如何︰設定 Web 應用程式的自訂 Docker 映像</span><span class="sxs-lookup"><span data-stu-id="987e2-109">How to: set a custom Docker image for a web app</span></span>
<span data-ttu-id="987e2-110">您可以設定 hello 自訂 Docker 映像的新和現有的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="987e2-110">You can set hello custom Docker image for both new and existing webs apps.</span></span> <span data-ttu-id="987e2-111">當您建立 web 應用程式在 Linux 上在 hello [Azure 入口網站](https://portal.azure.com/#create/Microsoft.AppSvcLinux)，按一下 **設定容器**tooset 自訂的 Docker 映像：</span><span class="sxs-lookup"><span data-stu-id="987e2-111">When you create a web app on Linux in hello [Azure portal](https://portal.azure.com/#create/Microsoft.AppSvcLinux), click **Configure container** tooset a custom Docker image:</span></span>

![Linux 上新 Web 應用程式的自訂 Docker 映像][1]


## <a name="how-to-use-a-custom-docker-image-from-docker-hub"></a><span data-ttu-id="987e2-113">作法︰從 Docker 中樞使用自訂 Docker 映像</span><span class="sxs-lookup"><span data-stu-id="987e2-113">How to: use a custom Docker image from Docker Hub</span></span> ##
<span data-ttu-id="987e2-114">toouse 自訂的 Docker 映像從 Docker Hub:</span><span class="sxs-lookup"><span data-stu-id="987e2-114">toouse a custom Docker image from Docker Hub:</span></span>

1. <span data-ttu-id="987e2-115">在 hello [Azure 入口網站](https://portal.azure.com)，置於您在 Linux 上的 web 應用程式然後**設定**按一下**Docker 容器**。</span><span class="sxs-lookup"><span data-stu-id="987e2-115">In hello [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="987e2-116">選取**Docker Hub**為 hello**影像來源**，然後按一下 **公用**或**私人**和型別 hello**映像和選擇性的標記名稱**，例如`node:4.5`。</span><span class="sxs-lookup"><span data-stu-id="987e2-116">Select **Docker Hub** as hello **Image source**, then click either **Public** or **Private** and type hello **Image and optional tag name**, such as `node:4.5`.</span></span> <span data-ttu-id="987e2-117">hello**啟動命令**會自動根據集定義在 hello Docker 映像檔中，但是您可以設定您自己的命令。</span><span class="sxs-lookup"><span data-stu-id="987e2-117">hello **Startup command** is set automatically based on what is defined in hello Docker image file, but you can set your own commands.</span></span>  

    ![Configure Docker Hub public repository image][2]

    <span data-ttu-id="987e2-119">私用儲存機制從您的映像時，您也需要與 tooenter hello Docker Hub 認證 (**登入使用者名稱**和**密碼**) hello 私用 Docker Hub 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="987e2-119">When your image is from a private repository, you also need tooenter hello Docker Hub credentials as (**Login username** and **Password**) for hello private Docker Hub repository.</span></span>

    ![Configure Docker Hub private repository image][3]

3. <span data-ttu-id="987e2-121">您已設定 hello 容器之後，請按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="987e2-121">After you have configured hello container, click **Save**.</span></span>

## <a name="how-toouse-a-docker-image-from-a-private-image-registry"></a><span data-ttu-id="987e2-122">Toouse Docker 從私人映像登錄的映像</span><span class="sxs-lookup"><span data-stu-id="987e2-122">How toouse a Docker image from a private image registry</span></span> ##
<span data-ttu-id="987e2-123">toouse 自訂的 Docker 映像從私人映像登錄：</span><span class="sxs-lookup"><span data-stu-id="987e2-123">toouse a custom Docker image from a private image registry:</span></span>

1. <span data-ttu-id="987e2-124">在 hello [Azure 入口網站](https://portal.azure.com)，置於您在 Linux 上的 web 應用程式然後**設定**按一下**Docker 容器**。</span><span class="sxs-lookup"><span data-stu-id="987e2-124">In hello [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="987e2-125">按一下**私人登錄**為 hello**影像來源**。</span><span class="sxs-lookup"><span data-stu-id="987e2-125">Click **Private registry** as hello **Image source**.</span></span> <span data-ttu-id="987e2-126">輸入 hello**映像和選擇性的標記名稱**，**伺服器 URL** hello 私人登錄，以及 hello 認證 (**登入使用者名稱**和**密碼**).</span><span class="sxs-lookup"><span data-stu-id="987e2-126">Enter hello **Image and optional tag name**, **Server URL** for hello private registry, along with hello credentials (**Login username** and **Password**).</span></span> <span data-ttu-id="987e2-127">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="987e2-127">Click **Save**.</span></span>

    ![Configure Docker image from private registry][4]


## <a name="how-to-set-hello-port-used-by-your-docker-image"></a><span data-ttu-id="987e2-129">如何： 設定您的 Docker 映像所使用的 hello 通訊埠</span><span class="sxs-lookup"><span data-stu-id="987e2-129">How to: set hello port used by your Docker image</span></span> ##

<span data-ttu-id="987e2-130">當您使用自訂的 Docker 映像 web 應用程式時，您可以使用 hello`WEBSITES_PORT`您 Dockerfile，加入產生的 toohello 容器中的環境變數。</span><span class="sxs-lookup"><span data-stu-id="987e2-130">When you use a custom Docker image for your web app, you can use hello `WEBSITES_PORT` environment variable in your Dockerfile, which gets added toohello generated container.</span></span> <span data-ttu-id="987e2-131">請考慮下列範例的拼音的應用程式的 docker 檔案 hello:</span><span class="sxs-lookup"><span data-stu-id="987e2-131">Consider hello following example of a docker file for a Ruby application:</span></span>

    FROM ruby:2.2.0
    RUN mkdir /app
    WORKDIR /app
    ADD . /app
    RUN bundle install
    CMD bundle exec puma config.ru -p WEBSITES_PORT -e production

<span data-ttu-id="987e2-132">最後一行 hello 命令，您可以看到該 hello WEBSITES_PORT 環境變數在執行階段傳遞。</span><span class="sxs-lookup"><span data-stu-id="987e2-132">On last line of hello command, you can see that hello WEBSITES_PORT environment variable is passed at runtime.</span></span> <span data-ttu-id="987e2-133">請記住，命令中區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="987e2-133">Remember that casing matters in commands.</span></span>

<span data-ttu-id="987e2-134">Hello 平台使用先前`PORT`應用程式設定，我們要規劃 toodeprecate hello 使用此設定的應用程式和移動 toousing`WEBSITES_PORT`獨佔。</span><span class="sxs-lookup"><span data-stu-id="987e2-134">Previously hello platform was using `PORT` app setting, we are planning toodeprecate hello use this app setting and move toousing `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="987e2-135">當您使用現有的 Docker 映像建置的其他人時，您可能需要 toospecify 連接埠 80 以外的連接埠 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="987e2-135">When you use an existing Docker image built by someone else, you may need toospecify a port other than port 80 for hello application.</span></span> <span data-ttu-id="987e2-136">tooconfigure hello 連接埠、 新增應用程式設定，稱為`WEBSITES_PORT`hello 值如下所示：</span><span class="sxs-lookup"><span data-stu-id="987e2-136">tooconfigure hello port, add an application setting named `WEBSITES_PORT` with hello value as shown below:</span></span>

![Configure PORT app setting for custom Docker image][6]

## <a name="how-to-set-hello-startup-time-for-your-docker-image"></a><span data-ttu-id="987e2-138">如何： 設定您的 Docker 映像的 hello 啟動時間</span><span class="sxs-lookup"><span data-stu-id="987e2-138">How to: set hello startup time for your Docker image</span></span> ##

<span data-ttu-id="987e2-139">根據預設，如果您的容器未啟動之前 230 秒，則 hello 平台會重新啟動您的容器。</span><span class="sxs-lookup"><span data-stu-id="987e2-139">By default, if your container does not start before 230 seconds, hello platform will restart your container.</span></span> <span data-ttu-id="987e2-140">如果您自訂的 Docker 映像啟動以秒為單位 230 以上時，您可以使用 hello`WEBSITES_CONTAINER_START_TIME_LIMIT`應用程式設定，此設定的 hello 值是以秒為單位，這可讓 hello 平台保持您的容器執行才能重新啟動它。</span><span class="sxs-lookup"><span data-stu-id="987e2-140">If your custom Docker image starts in more than 230 seconds, you can use hello `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting, hello value for this setting is in seconds, this will allow hello platform keep your container running before restarting it.</span></span> <span data-ttu-id="987e2-141">hello 預設值為 230 秒，而且 hello 最大允許值為 600 秒。</span><span class="sxs-lookup"><span data-stu-id="987e2-141">hello default value is 230 seconds, and hello max allowed value is 600 seconds.</span></span>

## <a name="how-to-unmount-hello-platform-provided-storage"></a><span data-ttu-id="987e2-142">如何： 取消掛接 hello 平台提供的儲存體</span><span class="sxs-lookup"><span data-stu-id="987e2-142">How to: unmount hello platform provided storage</span></span> ##

<span data-ttu-id="987e2-143">根據預設，hello 平台將會裝載永續性儲存體共用 toohello`\home\`目錄。</span><span class="sxs-lookup"><span data-stu-id="987e2-143">By default, hello platform will mount a persistent storage share toohello `\home\` directory.</span></span> <span data-ttu-id="987e2-144">如果您的容器映像不需要持續的共用，您可以停用裝載該存放裝置所設定的 hello`WEBSITES_ENABLE_APP_SERVICE_STORAGE`應用程式設定過`false`。</span><span class="sxs-lookup"><span data-stu-id="987e2-144">If your container image does not need a persistent share, you can disable mounting that storage by setting hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting too`false`.</span></span> <span data-ttu-id="987e2-145">從 hello scm 站台，仍然會存取 toothat 儲存體和 toohello hello 平台所產生的記錄檔會寫入所有的 Docker 記錄檔 （如果啟用）。</span><span class="sxs-lookup"><span data-stu-id="987e2-145">You will still have access toothat storage from hello scm site, and all Docker logs (if enabled) will be written toohello log files generated by hello platform.</span></span>

## <a name="how-to-switch-back-toousing-a-built-in-image"></a><span data-ttu-id="987e2-146">如何： 切換回 toousing 內建影像</span><span class="sxs-lookup"><span data-stu-id="987e2-146">How to: Switch back toousing a built-in image</span></span> ##

<span data-ttu-id="987e2-147">使用自訂映像 toousing 內建影像 tooswitch:</span><span class="sxs-lookup"><span data-stu-id="987e2-147">tooswitch from using a custom image toousing a built-in image:</span></span>

1. <span data-ttu-id="987e2-148">在 hello [Azure 入口網站](https://portal.azure.com)，置於您在 Linux 上的 web 應用程式然後**設定**按一下**App Service**。</span><span class="sxs-lookup"><span data-stu-id="987e2-148">In hello [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **App Service**.</span></span>

2. <span data-ttu-id="987e2-149">選取您**執行階段堆疊**toouse hello 內建影像，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="987e2-149">Select your **Runtime Stack** toouse for hello built-in image, then click **Save**.</span></span> 

![Configure Built-In Docker image][5]


## <a name="troubleshooting"></a><span data-ttu-id="987e2-151">疑難排解</span><span class="sxs-lookup"><span data-stu-id="987e2-151">Troubleshooting</span></span> ##

<span data-ttu-id="987e2-152">當您的應用程式失敗時 toostart 使用自訂的 Docker 映像時，請檢查的 hello Docker 記錄 hello LogFiles 目錄中。</span><span class="sxs-lookup"><span data-stu-id="987e2-152">When your application fails toostart with your custom Docker image, check hello Docker logs in hello LogFiles directory.</span></span> <span data-ttu-id="987e2-153">您可以透過 SCM 網站或 FTP 來存取此目錄。</span><span class="sxs-lookup"><span data-stu-id="987e2-153">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="987e2-154">toolog hello`stdout`和`stderr`從您的容器，您需要 tooenable **Docker 容器記錄**下**診斷記錄檔**。</span><span class="sxs-lookup"><span data-stu-id="987e2-154">toolog hello `stdout` and `stderr` from your container, you need tooenable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![啟用記錄][8]

![使用 Kudu tooview Docker 記錄檔][7]

<span data-ttu-id="987e2-157">您可以存取 hello SCM 站台從**進階工具**在 hello**開發工具**功能表。</span><span class="sxs-lookup"><span data-stu-id="987e2-157">You can access hello SCM site from **Advanced Tools** in hello **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="987e2-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="987e2-158">Next Steps</span></span> ##

<span data-ttu-id="987e2-159">請遵循下列連結 tooget 與 Linux 上的 Web 應用程式啟動的 hello。</span><span class="sxs-lookup"><span data-stu-id="987e2-159">Follow hello following links tooget started with Web App on Linux.</span></span>   

* [<span data-ttu-id="987e2-160">簡介 tooAzure Linux 上的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="987e2-160">Introduction tooAzure Web App on Linux</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="987e2-161">在 Linux 上的 Azure Web 應用程式中使用適用於 Node.js 的 PM2 組態</span><span class="sxs-lookup"><span data-stu-id="987e2-161">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](./app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="987e2-162">Linux 上的 Azure App Service Web 應用程式常見問題集</span><span class="sxs-lookup"><span data-stu-id="987e2-162">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<span data-ttu-id="987e2-163">在[我們的論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview)張貼問題和關切事項。</span><span class="sxs-lookup"><span data-stu-id="987e2-163">Post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>


<!--Image references-->
[1]: ./media/app-service-linux-using-custom-docker-image/new-configure-container.png
[2]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-public.png
[3]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-private.png
[4]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-privateregistry.png
[5]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-builtin.png
[6]: ./media/app-service-linux-using-custom-docker-image/setting-port.png
[7]: ./media/app-service-linux-using-custom-docker-image/kudu-docker-logs.png
[8]: ./media/app-service-linux-using-custom-docker-image/logging.png
