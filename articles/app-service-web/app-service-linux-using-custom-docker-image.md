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
# <a name="using-a-custom-docker-image-for-azure-web-app-on-linux"></a>針對 Linux 上的 Azure Web 應用程式使用自訂 Docker 映像 #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


App Service 在 Linux 上提供預先定義的應用程式堆疊，且支援特定的版本，例如 PHP 7.0 和 Node.js 4.5。 在 Linux 上的應用程式服務會使用 Docker 容器 toohost 這些預先建置的應用程式堆疊。 您也可以使用自訂的 Docker 映像 toodeploy 尚未定義 Azure 中您 web 應用程式 tooan 應用程式堆疊。 自訂 Docker 映像可裝載於公用或私人 Docker 儲存機制。


## <a name="how-to-set-a-custom-docker-image-for-a-web-app"></a>如何︰設定 Web 應用程式的自訂 Docker 映像
您可以設定 hello 自訂 Docker 映像的新和現有的 web 應用程式。 當您建立 web 應用程式在 Linux 上在 hello [Azure 入口網站](https://portal.azure.com/#create/Microsoft.AppSvcLinux)，按一下 **設定容器**tooset 自訂的 Docker 映像：

![Linux 上新 Web 應用程式的自訂 Docker 映像][1]


## <a name="how-to-use-a-custom-docker-image-from-docker-hub"></a>作法︰從 Docker 中樞使用自訂 Docker 映像 ##
toouse 自訂的 Docker 映像從 Docker Hub:

1. 在 hello [Azure 入口網站](https://portal.azure.com)，置於您在 Linux 上的 web 應用程式然後**設定**按一下**Docker 容器**。

2.  選取**Docker Hub**為 hello**影像來源**，然後按一下 **公用**或**私人**和型別 hello**映像和選擇性的標記名稱**，例如`node:4.5`。 hello**啟動命令**會自動根據集定義在 hello Docker 映像檔中，但是您可以設定您自己的命令。  

    ![Configure Docker Hub public repository image][2]

    私用儲存機制從您的映像時，您也需要與 tooenter hello Docker Hub 認證 (**登入使用者名稱**和**密碼**) hello 私用 Docker Hub 儲存機制。

    ![Configure Docker Hub private repository image][3]

3. 您已設定 hello 容器之後，請按一下**儲存**。

## <a name="how-toouse-a-docker-image-from-a-private-image-registry"></a>Toouse Docker 從私人映像登錄的映像 ##
toouse 自訂的 Docker 映像從私人映像登錄：

1. 在 hello [Azure 入口網站](https://portal.azure.com)，置於您在 Linux 上的 web 應用程式然後**設定**按一下**Docker 容器**。

2.  按一下**私人登錄**為 hello**影像來源**。 輸入 hello**映像和選擇性的標記名稱**，**伺服器 URL** hello 私人登錄，以及 hello 認證 (**登入使用者名稱**和**密碼**). 按一下 [儲存] 。

    ![Configure Docker image from private registry][4]


## <a name="how-to-set-hello-port-used-by-your-docker-image"></a>如何： 設定您的 Docker 映像所使用的 hello 通訊埠 ##

當您使用自訂的 Docker 映像 web 應用程式時，您可以使用 hello`WEBSITES_PORT`您 Dockerfile，加入產生的 toohello 容器中的環境變數。 請考慮下列範例的拼音的應用程式的 docker 檔案 hello:

    FROM ruby:2.2.0
    RUN mkdir /app
    WORKDIR /app
    ADD . /app
    RUN bundle install
    CMD bundle exec puma config.ru -p WEBSITES_PORT -e production

最後一行 hello 命令，您可以看到該 hello WEBSITES_PORT 環境變數在執行階段傳遞。 請記住，命令中區分大小寫。

Hello 平台使用先前`PORT`應用程式設定，我們要規劃 toodeprecate hello 使用此設定的應用程式和移動 toousing`WEBSITES_PORT`獨佔。

當您使用現有的 Docker 映像建置的其他人時，您可能需要 toospecify 連接埠 80 以外的連接埠 hello 應用程式。 tooconfigure hello 連接埠、 新增應用程式設定，稱為`WEBSITES_PORT`hello 值如下所示：

![Configure PORT app setting for custom Docker image][6]

## <a name="how-to-set-hello-startup-time-for-your-docker-image"></a>如何： 設定您的 Docker 映像的 hello 啟動時間 ##

根據預設，如果您的容器未啟動之前 230 秒，則 hello 平台會重新啟動您的容器。 如果您自訂的 Docker 映像啟動以秒為單位 230 以上時，您可以使用 hello`WEBSITES_CONTAINER_START_TIME_LIMIT`應用程式設定，此設定的 hello 值是以秒為單位，這可讓 hello 平台保持您的容器執行才能重新啟動它。 hello 預設值為 230 秒，而且 hello 最大允許值為 600 秒。

## <a name="how-to-unmount-hello-platform-provided-storage"></a>如何： 取消掛接 hello 平台提供的儲存體 ##

根據預設，hello 平台將會裝載永續性儲存體共用 toohello`\home\`目錄。 如果您的容器映像不需要持續的共用，您可以停用裝載該存放裝置所設定的 hello`WEBSITES_ENABLE_APP_SERVICE_STORAGE`應用程式設定過`false`。 從 hello scm 站台，仍然會存取 toothat 儲存體和 toohello hello 平台所產生的記錄檔會寫入所有的 Docker 記錄檔 （如果啟用）。

## <a name="how-to-switch-back-toousing-a-built-in-image"></a>如何： 切換回 toousing 內建影像 ##

使用自訂映像 toousing 內建影像 tooswitch:

1. 在 hello [Azure 入口網站](https://portal.azure.com)，置於您在 Linux 上的 web 應用程式然後**設定**按一下**App Service**。

2. 選取您**執行階段堆疊**toouse hello 內建影像，然後按一下**儲存**。 

![Configure Built-In Docker image][5]


## <a name="troubleshooting"></a>疑難排解 ##

當您的應用程式失敗時 toostart 使用自訂的 Docker 映像時，請檢查的 hello Docker 記錄 hello LogFiles 目錄中。 您可以透過 SCM 網站或 FTP 來存取此目錄。
toolog hello`stdout`和`stderr`從您的容器，您需要 tooenable **Docker 容器記錄**下**診斷記錄檔**。

![啟用記錄][8]

![使用 Kudu tooview Docker 記錄檔][7]

您可以存取 hello SCM 站台從**進階工具**在 hello**開發工具**功能表。

## <a name="next-steps"></a>後續步驟 ##

請遵循下列連結 tooget 與 Linux 上的 Web 應用程式啟動的 hello。   

* [簡介 tooAzure Linux 上的 Web 應用程式](./app-service-linux-intro.md)
* [在 Linux 上的 Azure Web 應用程式中使用適用於 Node.js 的 PM2 組態](./app-service-linux-using-nodejs-pm2.md)
* [Linux 上的 Azure App Service Web 應用程式常見問題集](app-service-linux-faq.md)

在[我們的論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview)張貼問題和關切事項。


<!--Image references-->
[1]: ./media/app-service-linux-using-custom-docker-image/new-configure-container.png
[2]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-public.png
[3]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-private.png
[4]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-privateregistry.png
[5]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-builtin.png
[6]: ./media/app-service-linux-using-custom-docker-image/setting-port.png
[7]: ./media/app-service-linux-using-custom-docker-image/kudu-docker-logs.png
[8]: ./media/app-service-linux-using-custom-docker-image/logging.png
