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
# <a name="ssh-support-for-azure-web-app-on-linux"></a>Linux 上的 Azure Web 應用程式 SSH 支援

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a>概觀

[安全殼層 (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) 是密碼編譯網路通訊協定，可保護網絡服務的使用安全。 它是最常使用系統 toolog 遠端安全地從命令列，從遠端執行系統管理命令。

Web 應用程式，在 Linux 上支援 SSH 至 hello 應用程式容器中與每個 hello 內建的 Docker 映像用於 hello 新的 web 應用程式的執行階段堆疊。 

![執行階段堆疊](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

您也可以使用自訂的 Docker 映像的 SSH 包括 hello SSH 伺服器 hello 映像的一部分，並設定它，本主題中所述。



## <a name="making-a-client-connection"></a>建立用戶端連線

必須啟動 toomake SSH 用戶端連線，hello 主要站台。 

貼入您的瀏覽器使用下列格式的 hello hello web 應用程式的原始檔控制管理 (SCM) 端點：

        https://<your sitename>.scm.azurewebsites.net/webssh/host

如果您尚未經過驗證，則需要的 tooauthenticate 與 Azure 訂用帳戶 tooconnect。

![SSH 連線](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a>SSH 支援自訂 Docker 映像

為了讓自訂 Docker 映像 toosupport SSH 通訊 hello 容器與 hello Azure 入口網站中的 hello 用戶端之間，執行 hello Docker 映像的步驟。 

這些步驟如下所示 hello Azure 應用程式服務儲存機制，例如[這裡](https://github.com/Azure-App-Service/node/blob/master/6.9.3/)。

1. 包含 hello`openssh-server`安裝[`RUN`指令](https://docs.docker.com/engine/reference/builder/#run)在 hello Dockerfile 為映像，並設定 hello hello 根帳號的密碼太`"Docker!"`。 

    > [!NOTE] 
    > 此設定不允許外部連接 toohello 容器。 SSH 只能存取透過 hello Kudu / SCM 站台，使用驗證 hello 發行認證。

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. 新增[`COPY`指令](https://docs.docker.com/engine/reference/builder/#copy)toohello Dockerfile toocopy [sshd_config](http://man.openbsd.org/sshd_config)檔案 toohello */等等/ssh/*目錄。 您的組態檔應該根據 hello Azure App Service GitHub 儲存機制中我們 sshd_config 檔案[這裡](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config)。

    > [!NOTE] 
    > hello *sshd_config* hello 連線失敗或檔案中必須包含下列 hello: 
    > * `Ciphers`必須包含至少一個 hello 下列： `aes128-cbc,3des-cbc,aes256-cbc`。
    > * `MACs`必須包含至少一個 hello 下列： `hmac-sha1,hmac-sha1-96`。

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. 連接埠 2222年納入 hello [ `EXPOSE`指令](https://docs.docker.com/engine/reference/builder/#expose)hello Dockerfile。 連接埠 2222年雖然已知 hello 根密碼，但不能從 hello 存取網際網路。 它是內部唯一連接埠存取只能由 hello 橋接網路的私人虛擬網路內的容器。

    ```docker
    EXPOSE 2222 80
    ```

4. 請確定 toostart hello ssh 服務。 hello 範例[這裡](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh)使用殼層指令碼中的*/bin*目錄。

    ```bash
    #!/bin/bash
    service ssh start
    ```

    hello Dockerfile 使用 hello [ `CMD`指令](https://docs.docker.com/engine/reference/builder/#cmd)toorun hello 指令碼。

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a>後續步驟
請參閱下列連結以取得更多關於 Web 應用程式在 Linux 上的 hello。 您可以在[我們的論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview)張貼問題和疑難。

* [Toouse 自訂的 Docker 的 Linux 上的 Azure Web 應用程式的映像](app-service-linux-using-custom-docker-image.md)
* [在 Linux 上的 Azure Web 應用程式中使用適用於 Node.js 的 PM2 組態](app-service-linux-using-nodejs-pm2.md)
* [在 Linux 上的 Azure Web 應用程式中使用 .NET Core](app-service-linux-using-dotnetcore.md)
* [在 Linux 上的 Azure Web 應用程式中使用 Ruby](app-service-linux-ruby-get-started.md)
* [Linux 上的 Azure App Service Web 應用程式常見問題集](app-service-linux-faq.md)

