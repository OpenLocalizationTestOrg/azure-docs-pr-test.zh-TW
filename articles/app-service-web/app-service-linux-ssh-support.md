---
title: "Azure App Service Web 應用程式在 Linux 上的 aaaSSH 支援 |Microsoft 文件"
description: "了解如何使用 SSH 搭配 Linux 上的 Azure Web 應用程式。"
keywords: "azure app service, web 應用程式, linux, oss"
services: app-service
documentationcenter: 
author: wesmc7777
manager: erikre
editor: 
ms.assetid: 66f9988f-8ffa-414a-9137-3a9b15a5573c
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: wesmc
ms.openlocfilehash: e00be6d4631e8936a2a8bc106da1fc06237a4b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="ssh-support-for-azure-web-app-on-linux"></a><span data-ttu-id="e5c87-104">Linux 上的 Azure Web 應用程式 SSH 支援</span><span class="sxs-lookup"><span data-stu-id="e5c87-104">SSH support for Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="e5c87-105">概觀</span><span class="sxs-lookup"><span data-stu-id="e5c87-105">Overview</span></span>

<span data-ttu-id="e5c87-106">[安全殼層 (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) 是密碼編譯網路通訊協定，可保護網絡服務的使用安全。</span><span class="sxs-lookup"><span data-stu-id="e5c87-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) is a cryptographic network protocol for using network services securely.</span></span> <span data-ttu-id="e5c87-107">它是最常使用系統 toolog 遠端安全地從命令列，從遠端執行系統管理命令。</span><span class="sxs-lookup"><span data-stu-id="e5c87-107">It is most commonly used toolog into a system remotely securely from a command-line and execute administrative commands remotely.</span></span>

<span data-ttu-id="e5c87-108">Web 應用程式，在 Linux 上支援 SSH 至 hello 應用程式容器中與每個 hello 內建的 Docker 映像用於 hello 新的 web 應用程式的執行階段堆疊。</span><span class="sxs-lookup"><span data-stu-id="e5c87-108">Web App on Linux provides SSH support into hello app container with each of hello built-in Docker images used for hello Runtime Stack of new web apps.</span></span> 

![執行階段堆疊](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

<span data-ttu-id="e5c87-110">您也可以使用自訂的 Docker 映像的 SSH 包括 hello SSH 伺服器 hello 映像的一部分，並設定它，本主題中所述。</span><span class="sxs-lookup"><span data-stu-id="e5c87-110">You can also use SSH with your custom Docker images by including hello SSH server as part of hello image and configuring it as described in this topic.</span></span>



## <a name="making-a-client-connection"></a><span data-ttu-id="e5c87-111">建立用戶端連線</span><span class="sxs-lookup"><span data-stu-id="e5c87-111">Making a client connection</span></span>

<span data-ttu-id="e5c87-112">必須啟動 toomake SSH 用戶端連線，hello 主要站台。</span><span class="sxs-lookup"><span data-stu-id="e5c87-112">toomake an SSH client connection, hello main site must be started.</span></span> 

<span data-ttu-id="e5c87-113">貼入您的瀏覽器使用下列格式的 hello hello web 應用程式的原始檔控制管理 (SCM) 端點：</span><span class="sxs-lookup"><span data-stu-id="e5c87-113">Paste hello Source Control Management (SCM) endpoint for your web app into your browser using hello following form:</span></span>

        https://<your sitename>.scm.azurewebsites.net/webssh/host

<span data-ttu-id="e5c87-114">如果您尚未經過驗證，則需要的 tooauthenticate 與 Azure 訂用帳戶 tooconnect。</span><span class="sxs-lookup"><span data-stu-id="e5c87-114">If you are not already authenticated, you are required tooauthenticate with your Azure subscription tooconnect.</span></span>

![SSH 連線](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a><span data-ttu-id="e5c87-116">SSH 支援自訂 Docker 映像</span><span class="sxs-lookup"><span data-stu-id="e5c87-116">SSH support with custom Docker images</span></span>

<span data-ttu-id="e5c87-117">為了讓自訂 Docker 映像 toosupport SSH 通訊 hello 容器與 hello Azure 入口網站中的 hello 用戶端之間，執行 hello Docker 映像的步驟。</span><span class="sxs-lookup"><span data-stu-id="e5c87-117">In order for a custom Docker image toosupport SSH communication between hello container and hello client in hello Azure portal, perform hello following steps for your Docker image.</span></span> 

<span data-ttu-id="e5c87-118">這些步驟如下所示 hello Azure 應用程式服務儲存機制，例如[這裡](https://github.com/Azure-App-Service/node/blob/master/6.9.3/)。</span><span class="sxs-lookup"><span data-stu-id="e5c87-118">These steps are are shown in hello Azure App Service repository as an example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).</span></span>

1. <span data-ttu-id="e5c87-119">包含 hello`openssh-server`安裝[`RUN`指令](https://docs.docker.com/engine/reference/builder/#run)在 hello Dockerfile 為映像，並設定 hello hello 根帳號的密碼太`"Docker!"`。</span><span class="sxs-lookup"><span data-stu-id="e5c87-119">Include hello `openssh-server` installation in [`RUN` instruction](https://docs.docker.com/engine/reference/builder/#run) in hello Dockerfile for your image and set hello password for hello root account too`"Docker!"`.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="e5c87-120">此設定不允許外部連接 toohello 容器。</span><span class="sxs-lookup"><span data-stu-id="e5c87-120">This configuration does not allow external connections toohello container.</span></span> <span data-ttu-id="e5c87-121">SSH 只能存取透過 hello Kudu / SCM 站台，使用驗證 hello 發行認證。</span><span class="sxs-lookup"><span data-stu-id="e5c87-121">SSH can only be accessed via hello Kudu / SCM Site, which is authenticated using hello publishing credentials.</span></span>

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. <span data-ttu-id="e5c87-122">新增[`COPY`指令](https://docs.docker.com/engine/reference/builder/#copy)toohello Dockerfile toocopy [sshd_config](http://man.openbsd.org/sshd_config)檔案 toohello */等等/ssh/*目錄。</span><span class="sxs-lookup"><span data-stu-id="e5c87-122">Add a [`COPY` instruction](https://docs.docker.com/engine/reference/builder/#copy) toohello Dockerfile toocopy a [sshd_config](http://man.openbsd.org/sshd_config) file toohello */etc/ssh/* directory.</span></span> <span data-ttu-id="e5c87-123">您的組態檔應該根據 hello Azure App Service GitHub 儲存機制中我們 sshd_config 檔案[這裡](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config)。</span><span class="sxs-lookup"><span data-stu-id="e5c87-123">Your configuration file should be based on our sshd_config file in hello Azure-App-Service GitHub repository [here](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e5c87-124">hello *sshd_config* hello 連線失敗或檔案中必須包含下列 hello:</span><span class="sxs-lookup"><span data-stu-id="e5c87-124">hello *sshd_config* file must include hello following or hello connection fails:</span></span> 
    > * <span data-ttu-id="e5c87-125">`Ciphers`必須包含至少一個 hello 下列： `aes128-cbc,3des-cbc,aes256-cbc`。</span><span class="sxs-lookup"><span data-stu-id="e5c87-125">`Ciphers` must include at least one of hello following: `aes128-cbc,3des-cbc,aes256-cbc`.</span></span>
    > * <span data-ttu-id="e5c87-126">`MACs`必須包含至少一個 hello 下列： `hmac-sha1,hmac-sha1-96`。</span><span class="sxs-lookup"><span data-stu-id="e5c87-126">`MACs` must include at least one of hello following: `hmac-sha1,hmac-sha1-96`.</span></span>

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. <span data-ttu-id="e5c87-127">連接埠 2222年納入 hello [ `EXPOSE`指令](https://docs.docker.com/engine/reference/builder/#expose)hello Dockerfile。</span><span class="sxs-lookup"><span data-stu-id="e5c87-127">Include port 2222 in hello [`EXPOSE` instruction](https://docs.docker.com/engine/reference/builder/#expose) for hello Dockerfile.</span></span> <span data-ttu-id="e5c87-128">連接埠 2222年雖然已知 hello 根密碼，但不能從 hello 存取網際網路。</span><span class="sxs-lookup"><span data-stu-id="e5c87-128">Although hello root password is known, port 2222 cannot be accessed from hello internet.</span></span> <span data-ttu-id="e5c87-129">它是內部唯一連接埠存取只能由 hello 橋接網路的私人虛擬網路內的容器。</span><span class="sxs-lookup"><span data-stu-id="e5c87-129">It is an internal only port accessible only by containers within hello bridge network of a private virtual network.</span></span>

    ```docker
    EXPOSE 2222 80
    ```

4. <span data-ttu-id="e5c87-130">請確定 toostart hello ssh 服務。</span><span class="sxs-lookup"><span data-stu-id="e5c87-130">Make sure toostart hello ssh service.</span></span> <span data-ttu-id="e5c87-131">hello 範例[這裡](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh)使用殼層指令碼中的*/bin*目錄。</span><span class="sxs-lookup"><span data-stu-id="e5c87-131">hello example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) uses a shell script in */bin* directory.</span></span>

    ```bash
    #!/bin/bash
    service ssh start
    ```

    <span data-ttu-id="e5c87-132">hello Dockerfile 使用 hello [ `CMD`指令](https://docs.docker.com/engine/reference/builder/#cmd)toorun hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="e5c87-132">hello Dockerfile uses hello [`CMD` instruction](https://docs.docker.com/engine/reference/builder/#cmd) toorun hello script.</span></span>

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a><span data-ttu-id="e5c87-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e5c87-133">Next steps</span></span>
<span data-ttu-id="e5c87-134">請參閱下列連結以取得更多關於 Web 應用程式在 Linux 上的 hello。</span><span class="sxs-lookup"><span data-stu-id="e5c87-134">See hello following links for more information regarding Web App on Linux.</span></span> <span data-ttu-id="e5c87-135">您可以在[我們的論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview)張貼問題和疑難。</span><span class="sxs-lookup"><span data-stu-id="e5c87-135">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="e5c87-136">Toouse 自訂的 Docker 的 Linux 上的 Azure Web 應用程式的映像</span><span class="sxs-lookup"><span data-stu-id="e5c87-136">How toouse a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="e5c87-137">在 Linux 上的 Azure Web 應用程式中使用適用於 Node.js 的 PM2 組態</span><span class="sxs-lookup"><span data-stu-id="e5c87-137">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="e5c87-138">在 Linux 上的 Azure Web 應用程式中使用 .NET Core</span><span class="sxs-lookup"><span data-stu-id="e5c87-138">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="e5c87-139">在 Linux 上的 Azure Web 應用程式中使用 Ruby</span><span class="sxs-lookup"><span data-stu-id="e5c87-139">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="e5c87-140">Linux 上的 Azure App Service Web 應用程式常見問題集</span><span class="sxs-lookup"><span data-stu-id="e5c87-140">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

