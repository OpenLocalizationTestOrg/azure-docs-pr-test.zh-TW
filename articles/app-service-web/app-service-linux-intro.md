---
title: "aaaIntroduction tooAzure Linux 上的 Web 應用程式 |Microsoft 文件"
description: "深入了解 Linux 上的 Azure Web 應用程式。"
keywords: azure app service, linux, oss
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: bc85eff6-bbdf-410a-93dc-0f1222796676
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 43b9865ade251909a77429eb3e18fe0bcaac3bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-web-app-on-linux"></a>簡介 tooAzure Linux 上的 Web 應用程式

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a>概觀
客戶可以使用 Web 應用程式原生 Linux 上的 Linux toohost web 應用程式支援的應用程式堆疊。 hello 下節列出 hello 目前支援的應用程式堆疊。 

## <a name="features"></a>特性
Web 應用程式，在 Linux 上目前支援下列應用程式堆疊的 hello:

* Node.js
    * 4.4
    * 4.5
    * 6.2
    * 6.6
    * 6.9
    * 6.10
    * 6.11
    * 8.0
    * 8.1
* PHP
    * 5.6
    * 7.0
* .Net Core
    * 1.0
    * 1.1
* Ruby
    * 2.3

客戶可以使用下列工具來部署應用程式︰

* FTP
* 本機 Git
* GitHub
* Bitbucket

調整應用程式大小︰

* 客戶可以向上和向下調整 web 應用程式，藉由變更其 App Service 方案的 hello 層
* 客戶可以擴充應用程式及執行多個應用程式的執行個體 hello 範圍內的 SKU

如 Kudu hello 基本功能：

* 環境
* 部署
* 基本主控台
* SSH

針對 DevOps：

* 預備環境
* ACR 和 DockerHub CI/CD

## <a name="limitations"></a>限制
hello Azure 入口網站會顯示目前在 Linux 上的 Web 應用程式適用的唯一功能，並隱藏 hello rest。 因為我們啟用更多的功能，就會看見 hello 入口網站上。

某些功能尚無法使用，例如虛擬網路整合、Azure Active Directory/第三方驗證或 Kudu 網站擴充功能。 一旦這些功能可供使用，我們將會更新我們的文件和部落格有關 hello 變更。

這個公用預覽了目前僅限用於 hello 下列區域：

* 美國西部
* 美國東部
* 西歐
* 北歐
* 美國中南部
* 美國中北部
* 東南亞
* 東亞
* 澳洲東部
* 日本東部
* 巴西南部
* 印度南部

Web 應用程式，在 Linux 上 hello 專用的 app service 方案中才支援，而且沒有免費或共用層。 此外，一般和 Linux Web 應用程式的 App Service 方案互斥，因此，您無法在非 Linux App Service 方案中建立 Linux Web 應用程式。

Web 應用程式，在 Linux 上必須建立資源群組不包含非 Linux hello 的 web 應用程式中相同的區域。

## <a name="troubleshooting"></a>疑難排解 ##

當您的應用程式失敗 toostart 或您想 toocheck hello 記錄從您的應用程式時，請檢查的 hello Docker 記錄 hello LogFiles 目錄中。 您可以透過 SCM 網站或 FTP 來存取此目錄。
toolog hello`stdout`和`stderr`從您的容器，您需要 tooenable **Docker 容器記錄**下**診斷記錄檔**。

![啟用記錄][2]

![使用 Kudu tooview Docker 記錄檔][1]

您可以存取 hello SCM 站台從**進階工具**在 hello**開發工具**功能表。

## <a name="next-steps"></a>後續步驟
請參閱下列連結 tooget 開始使用 Linux 上的應用程式服務的 hello。 您可以在[我們的論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview)張貼問題和疑難。

* [Toouse 自訂的 Docker 的 Linux 上的 Azure Web 應用程式的映像](app-service-linux-using-custom-docker-image.md)
* [在 Linux 上的 Azure Web 應用程式中使用適用於 Node.js 的 PM2 組態](app-service-linux-using-nodejs-pm2.md)
* [在 Linux 上的 Azure App Service Web 應用程式中使用 .NET Core](app-service-linux-using-dotnetcore.md)
* [在 Linux 上的 Azure App Service Web 應用程式中使用 Ruby](app-service-linux-ruby-get-started.md)
* [Linux 上的 Azure App Service Web 應用程式常見問題集](app-service-linux-faq.md)
* [Linux 上的 Azure Web 應用程式 SSH 支援](./app-service-linux-ssh-support.md)
* [在 Azure App Service 中設定預備環境](./web-sites-staged-publishing.md)
* [在 Linux 上使用 Azure Web 應用程式連續部署 Docker 中樞](./app-service-linux-ci-cd.md)

<!--Image references-->
[1]: ./media/app-service-linux-intro/kudu-docker-logs.png
[2]: ./media/app-service-linux-intro/logging.png