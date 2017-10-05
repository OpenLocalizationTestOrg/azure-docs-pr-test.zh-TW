---
title: "Linux 上的 Azure Web 應用程式簡介 | Microsoft Docs"
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
ms.openlocfilehash: 0870f811845ec7c705da13f08abdfa762d25b209
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-azure-web-app-on-linux"></a>Linux 上的 Azure Web 應用程式簡介

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a>概觀
針對支援的應用程式堆疊，客戶可以使用 Linux 上的 Web 應用程式，以原生方式將 Web Apps 裝載於 Linux。 下節列出目前支援的應用程式堆疊。 

## <a name="features"></a>特性
Linux 上的 Web 應用程式目前支援下列應用程式堆疊︰

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

* 客戶可以變更 App Service 方案中的階層，即可相應增加和減少 Web 應用程式的規模
* 客戶可以將應用程式相應放大，在其 SKU 的範圍內執行多個應用程式執行個體

針對 Kudu，有一些基本功能︰

* 環境
* 部署
* 基本主控台
* SSH

針對 DevOps：

* 預備環境
* ACR 和 DockerHub CI/CD

## <a name="limitations"></a>限制
Azure 入口網站只會顯示 Linux 上的 Web 應用程式目前可用的功能，並隱藏其餘部分。 隨著我們啟用更多功能，您會在入口網站中看到它們。

某些功能尚無法使用，例如虛擬網路整合、Azure Active Directory/第三方驗證或 Kudu 網站擴充功能。 一旦這些功能提供使用後，我們將會在文件和部落格中更新關於變更的消息。

目前只在下列區域提供此公開預覽版本：

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

Linux 上的 Web Apps 只在「專用」App Service 方案中才支援，而且沒有「免費」或「共用」層。 此外，一般和 Linux Web 應用程式的 App Service 方案互斥，因此，您無法在非 Linux App Service 方案中建立 Linux Web 應用程式。

只有同一區域沒有非 Linux Web Apps 的資源群組中，才能建立 Linux 上的 Web Apps。

## <a name="troubleshooting"></a>疑難排解 ##

當您的應用程式無法啟動或您想要檢查應用程式的記錄時，請檢查 LogFiles 目錄中的 Docker 記錄。 您可以透過 SCM 網站或 FTP 來存取此目錄。
若要從您的容器記錄 `stdout` 和 `stderr`，您必須啟用 [診斷記錄] 下的 [Docker 容器記錄]。

![啟用記錄][2]

![Using Kudu to view Docker logs][1]

您可以在 [開發工具] 功能表中從 [進階工具] 存取 SCM 網站。

## <a name="next-steps"></a>後續步驟
請參閱下列連結以開始使用 Linux 上的 App Service。 您可以在[我們的論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview)張貼問題和疑難。

* [如何針對 Linux 上的 Azure Web 應用程式使用自訂 Docker 映像](app-service-linux-using-custom-docker-image.md)
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