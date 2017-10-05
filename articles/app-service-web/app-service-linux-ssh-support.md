---
title: "Linux 上的 Azure App Service Web 應用程式 SSH 支援 | Microsoft Docs"
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
ms.openlocfilehash: feee7a5c91d213a6b0bfdaf264a4da4d9e79cbe7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="ssh-support-for-azure-web-app-on-linux"></a><span data-ttu-id="cfe7f-104">Linux 上的 Azure Web 應用程式 SSH 支援</span><span class="sxs-lookup"><span data-stu-id="cfe7f-104">SSH support for Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="cfe7f-105">概觀</span><span class="sxs-lookup"><span data-stu-id="cfe7f-105">Overview</span></span>

<span data-ttu-id="cfe7f-106">[安全殼層 (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) 是密碼編譯網路通訊協定，可保護網絡服務的使用安全。</span><span class="sxs-lookup"><span data-stu-id="cfe7f-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) is a cryptographic network protocol for using network services securely.</span></span> <span data-ttu-id="cfe7f-107">它最常用於從命令列遠端安全地登入系統，以及從遠端執行系統管理命令。</span><span class="sxs-lookup"><span data-stu-id="cfe7f-107">It is most commonly used to log into a system remotely securely from a command-line and execute administrative commands remotely.</span></span>

<span data-ttu-id="cfe7f-108">Linux 上的 Web 應用程式會利用每個用於新 Web Apps 的「執行階段堆疊」的內建 Docker 映像來提供應用程式容器內的 SSH 支援。</span><span class="sxs-lookup"><span data-stu-id="cfe7f-108">Web App on Linux provides SSH support into the app container with each of the built-in Docker images used for the Runtime Stack of new web apps.</span></span> 

![執行階段堆疊](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

<span data-ttu-id="cfe7f-110">您也可以使用 SSH 搭配自訂 Docker 映像，方法是將 SSH 伺服器納入映像，並如本主題中所述將它進行設定。</span><span class="sxs-lookup"><span data-stu-id="cfe7f-110">You can also use SSH with your custom Docker images by including the SSH server as part of the image and configuring it as described in this topic.</span></span>



## <a name="making-a-client-connection"></a><span data-ttu-id="cfe7f-111">建立用戶端連線</span><span class="sxs-lookup"><span data-stu-id="cfe7f-111">Making a client connection</span></span>

<span data-ttu-id="cfe7f-112">若要建立 SSH 用戶端連線，必須先啟動主要網站。</span><span class="sxs-lookup"><span data-stu-id="cfe7f-112">To make an SSH client connection, the main site must be started.</span></span> 

<span data-ttu-id="cfe7f-113">使用下列格式，將 Web 應用程式的原始檔控制管理 (SCM) 端點貼到您的瀏覽器︰</span><span class="sxs-lookup"><span data-stu-id="cfe7f-113">Paste the Source Control Management (SCM) endpoint for your web app into your browser using the following form:</span></span>

        https://<your sitename>.scm.azurewebsites.net/webssh/host

<span data-ttu-id="cfe7f-114">如果您尚未經過驗證，必須向您的 Azure 訂用帳戶進行驗證才能連線。</span><span class="sxs-lookup"><span data-stu-id="cfe7f-114">If you are not already authenticated, you are required to authenticate with your Azure subscription to connect.</span></span>

![SSH 連線](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a><span data-ttu-id="cfe7f-116">SSH 支援自訂 Docker 映像</span><span class="sxs-lookup"><span data-stu-id="cfe7f-116">SSH support with custom Docker images</span></span>

<span data-ttu-id="cfe7f-117">為使自訂 Docker 映像支援容器與 Azure 入口網站之用戶端的 SSH 通訊，請針對 Docker 映像執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="cfe7f-117">In order for a custom Docker image to support SSH communication between the container and the client in the Azure portal, perform the following steps for your Docker image.</span></span> 

<span data-ttu-id="cfe7f-118">這些步驟會顯示在 Azure App Service 存放庫中，如[這裡](https://github.com/Azure-App-Service/node/blob/master/6.9.3/)的範例。</span><span class="sxs-lookup"><span data-stu-id="cfe7f-118">These steps are are shown in the Azure App Service repository as an example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).</span></span>

1. <span data-ttu-id="cfe7f-119">將 [`RUN`指示](https://docs.docker.com/engine/reference/builder/#run)中的 `openssh-server` 安裝納入映像的 Dockerfile，並將根帳戶的密碼設為 `"Docker!"`。</span><span class="sxs-lookup"><span data-stu-id="cfe7f-119">Include the `openssh-server` installation in [`RUN` instruction](https://docs.docker.com/engine/reference/builder/#run) in the Dockerfile for your image and set the password for the root account to `"Docker!"`.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="cfe7f-120">此設定不允許容器的外部連線。</span><span class="sxs-lookup"><span data-stu-id="cfe7f-120">This configuration does not allow external connections to the container.</span></span> <span data-ttu-id="cfe7f-121">只可透過使用發佈認證進行驗證的 Kudu / SCM 網站存取 SSH。</span><span class="sxs-lookup"><span data-stu-id="cfe7f-121">SSH can only be accessed via the Kudu / SCM Site, which is authenticated using the publishing credentials.</span></span>

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. <span data-ttu-id="cfe7f-122">將 [`COPY` 指示](https://docs.docker.com/engine/reference/builder/#copy)新增至 Dockerfile，以將 [sshd_config](http://man.openbsd.org/sshd_config) 檔案複製到 */etc/ssh/* 目錄。</span><span class="sxs-lookup"><span data-stu-id="cfe7f-122">Add a [`COPY` instruction](https://docs.docker.com/engine/reference/builder/#copy) to the Dockerfile to copy a [sshd_config](http://man.openbsd.org/sshd_config) file to the */etc/ssh/* directory.</span></span> <span data-ttu-id="cfe7f-123">組態檔需根據我們[這裡](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config)的 Azure-App-Service GitHub 存放庫中的 sshd_config 檔案。</span><span class="sxs-lookup"><span data-stu-id="cfe7f-123">Your configuration file should be based on our sshd_config file in the Azure-App-Service GitHub repository [here](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cfe7f-124">sshd_config 檔案必須包含下列項目，否則無法連線︰</span><span class="sxs-lookup"><span data-stu-id="cfe7f-124">The *sshd_config* file must include the following or the connection fails:</span></span> 
    > * <span data-ttu-id="cfe7f-125">`Ciphers` 必須至少包含下列其中一個：`aes128-cbc,3des-cbc,aes256-cbc`。</span><span class="sxs-lookup"><span data-stu-id="cfe7f-125">`Ciphers` must include at least one of the following: `aes128-cbc,3des-cbc,aes256-cbc`.</span></span>
    > * <span data-ttu-id="cfe7f-126">`MACs` 必須至少包含下列其中一個：`hmac-sha1,hmac-sha1-96`。</span><span class="sxs-lookup"><span data-stu-id="cfe7f-126">`MACs` must include at least one of the following: `hmac-sha1,hmac-sha1-96`.</span></span>

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. <span data-ttu-id="cfe7f-127">針對 Dockerfile，請納入 [`EXPOSE` 指示](https://docs.docker.com/engine/reference/builder/#expose) 中的連接埠 2222。</span><span class="sxs-lookup"><span data-stu-id="cfe7f-127">Include port 2222 in the [`EXPOSE` instruction](https://docs.docker.com/engine/reference/builder/#expose) for the Dockerfile.</span></span> <span data-ttu-id="cfe7f-128">雖然已知根密碼，但無法從網際網路存取連接埠 2222。</span><span class="sxs-lookup"><span data-stu-id="cfe7f-128">Although the root password is known, port 2222 cannot be accessed from the internet.</span></span> <span data-ttu-id="cfe7f-129">它是僅供內部使用的連接埠，只有私人虛擬網路之橋接網路內的容器可以存取。</span><span class="sxs-lookup"><span data-stu-id="cfe7f-129">It is an internal only port accessible only by containers within the bridge network of a private virtual network.</span></span>

    ```docker
    EXPOSE 2222 80
    ```

4. <span data-ttu-id="cfe7f-130">請確定啟動 SSH 服務。</span><span class="sxs-lookup"><span data-stu-id="cfe7f-130">Make sure to start the ssh service.</span></span> <span data-ttu-id="cfe7f-131">[這裡](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh)的範例會使用 /bin 目錄中的殼層指令碼。</span><span class="sxs-lookup"><span data-stu-id="cfe7f-131">The example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) uses a shell script in */bin* directory.</span></span>

    ```bash
    #!/bin/bash
    service ssh start
    ```

    <span data-ttu-id="cfe7f-132">Dockerfile 會使用 [`CMD` 指示](https://docs.docker.com/engine/reference/builder/#cmd)來執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="cfe7f-132">The Dockerfile uses the [`CMD` instruction](https://docs.docker.com/engine/reference/builder/#cmd) to run the script.</span></span>

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a><span data-ttu-id="cfe7f-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cfe7f-133">Next steps</span></span>
<span data-ttu-id="cfe7f-134">如需 Linux 上的 Web 應用程式相關資訊，請參閱下列連結。</span><span class="sxs-lookup"><span data-stu-id="cfe7f-134">See the following links for more information regarding Web App on Linux.</span></span> <span data-ttu-id="cfe7f-135">您可以在[我們的論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview)張貼問題和疑難。</span><span class="sxs-lookup"><span data-stu-id="cfe7f-135">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="cfe7f-136">如何針對 Linux 上的 Azure Web 應用程式使用自訂 Docker 映像</span><span class="sxs-lookup"><span data-stu-id="cfe7f-136">How to use a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="cfe7f-137">在 Linux 上的 Azure Web 應用程式中使用適用於 Node.js 的 PM2 組態</span><span class="sxs-lookup"><span data-stu-id="cfe7f-137">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="cfe7f-138">在 Linux 上的 Azure Web 應用程式中使用 .NET Core</span><span class="sxs-lookup"><span data-stu-id="cfe7f-138">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="cfe7f-139">在 Linux 上的 Azure Web 應用程式中使用 Ruby</span><span class="sxs-lookup"><span data-stu-id="cfe7f-139">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="cfe7f-140">Linux 上的 Azure App Service Web 應用程式常見問題集</span><span class="sxs-lookup"><span data-stu-id="cfe7f-140">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

