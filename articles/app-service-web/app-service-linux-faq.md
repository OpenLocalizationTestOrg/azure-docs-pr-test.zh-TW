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
# <a name="azure-app-service-web-app-on-linux-faq"></a>Linux 上的 Azure App Service Web 應用程式常見問題集

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


Hello 版本在 Linux 上的 Web 應用程式中，我們正努力加入功能，並進行改善 tooour 平台。 以下是一些常見問題集 (FAQ)，我們的客戶有已要求我們透過 hello 最後幾個月。
如果您有問題，hello 發行項上的註解，我們會儘速回答。

## <a name="built-in-images"></a>內建映像

**問：**我想 toofork hello 內建 Docker 容器 hello 平台所提供。 哪裡可以找到這些檔案？

**答：**您可以在 [GitHub](https://github.com/azure-app-service) 上找到所有 Docker 檔案。 您可以在 [Docker Hub](https://hub.docker.com/u/appsvc/) 上找到所有 Docker 容器。

**問：**為何 hello 預期 hello 啟動檔案區段的值時設定執行階段堆疊時會 hello？

**答：** For Node.Js 您指定 hello PM2 組態檔或指令碼檔案。 針對 .Net Core，請指定已編譯的 DLL 名稱。 Ruby，您可以指定 hello 拼音指令碼的 tooinitialize 您的應用程式。

## <a name="management"></a>管理

**問：**當我按 hello Azure 入口網站中的 hello 重新啟動 按鈕時，會發生什麼事？

**答：**這是 hello Docker 重新啟動的對等。

**問：**我可以使用安全殼層 (SSH) tooconnect toohello 應用程式容器虛擬機器 (VM)？

**答：**是，您可以透過 hello SCM 網站，文件如需詳細資訊核取 hello 下列[Web 應用程式，在 Linux 上的 SSH 支援](./app-service-linux-ssh-support.md)

**問：**我想 toocreate Linux 應用程式服務平面上，透過 SDK 或 ARM 範本、 如何達成這嗎？

**答：**需要 tooset hello `reserved` hello 應用程式的欄位太服務`true`。

## <a name="continuous-integrationdeployment"></a>連續整合/部署

**問：**我的 web 應用程式仍會使用舊的 Docker 容器映像之後我已更新 hello 銜接站集線器上的映像。 您是否支援自訂容器的連續整合/部署？

**答：**連續整合/部署 Azure 容器登錄或 DockerHub 映像的下列文章的核取 hello tooset [on Linux 的 Azure Web 應用程式與連續部署](./app-service-linux-ci-cd.md)。 針對私人登錄中，您可以重新整理 hello 容器停止然後啟動您的 web 應用程式。 或者，您可以變更或新增虛擬應用程式設定 tooforce 重新整理您的容器。

**問︰**是否支援預備環境？

**答：** 是。

**問：**我可以使用**web 部署**toodeploy 我的 web 應用程式嗎？

**答：**是，您需要 tooset 應用程式稱為`WEBSITE_WEBDEPLOY_USE_SCM`太`false`。

## <a name="language-support"></a>語言支援

**問︰**是否支援未編譯的 .NET Core 應用程式？

**答：** 是。

**問︰**您是否支援以 Composer 做為 PHP 應用程式的相依性管理程式？

**答：** 是。 Git 在部署期間，Kudu 應該會偵測到您要部署的 PHP 應用程式 （感謝您 toohello composer.json 檔案存在），並將觸發程序為您的編輯器 」 安裝。

## <a name="custom-containers"></a>自訂容器

**問︰**我使用自己的自訂容器。 我的應用程式位於 hello`\home\`目錄，但我找不到我的檔案時使用 hello 瀏覽 hello 內容[SCM 網站](https://github.com/projectkudu/kudu)或 FTP 用戶端。 我的檔案在哪裡？

**答：**掛接 SMB 共用 toohello`\home\`目錄。 這會覆寫該處的所有內容。

**問︰**我使用自己的自訂容器。 我不想 hello 平台 toomount SMB 共用 toohello `\home\`。

**答：**您可以執行此動作設定 hello`WEBSITES_ENABLE_APP_SERVICE_STORAGE`應用程式設定過`false`。

**問：**我自訂容器會很長的時間 toostart，和 hello 平台重新啟動之前的 hello 容器完成啟動。

**答：**您可以設定 hello hello 平台會重新啟動您的容器之前等候的時間。 這可藉由設定 hello`WEBSITES_CONTAINER_START_TIME_LIMIT`應用程式設定 toohello 所需值，以秒為單位。 hello 預設 230 秒，而且 hello 最大值為 600 秒。

**問：** hello 私人登錄伺服器 url 的格式是什麼？

**答：**您需要 tooprovide hello 完整登錄 url 包括`http://`或`https://`。

**問：** hello 私人登錄選項中的 hello 映像名稱格式是什麼？

**答：**需要 tooadd hello 完整的映像名稱包括 hello 私人登錄 url （例如。 myacr.azurecr.io/dotnet:latest)

**問：**我想要 tooexpose 多個連接埠上我的自訂容器映像。 是否可行？

**答：**目前不支援此做法。

**問︰**我可以攜帶自己的儲存體嗎？

**答：**目前不支援此做法。

**問：**無法瀏覽我的自訂容器檔案系統 」 或 「 執行處理序從 hello SCM 站台。 這是為什麼？

**答：** hello SCM 站台執行不同的容器中。 您無法檢查 hello 檔案系統或執行中的 hello 應用程式容器的處理序。

**問：**我自訂容器會接聽通訊埠 80 以外的 tooa 連接埠。 如何設定我的應用程式 tooroute hello 要求 toothat 的連接埠？

**答：**我們有自動偵測連接埠，而且您可以指定應用程式稱為**WEBSITES_PORT**，並給定 hello hello 預期的連接埠號碼的值。 Hello 平台使用先前`PORT`應用程式設定，我們要規劃 toodeprecate hello 使用此設定的應用程式和移動 toousing`WEBSITES_PORT`獨佔。

**問：**就需要 tooimplement HTTPS 我自訂容器中。

**答：** hello 平台不可以，會處理在共用的 hello 前端的 HTTPS 終止。

## <a name="pricing-and-sla"></a>價格和 SLA

**問：**什麼 hello 定價使用 hello 公用預覽？

**答：**負責半 hello 的小時數 hello 一般的 Azure 應用程式服務定價與您的應用程式執行。 這表示您會獲得標準 Azure App Service 定價的五折優惠。

## <a name="other"></a>其他

**問：** hello 支援應用程式設定名稱中的字元是什麼？

**答：**只能使用 A-Z、 a-z、 0-9 和 hello 應用程式設定的底線。

**問︰**我可以在何處提出新功能的要求？

**答：**可以送出您的想法在 hello [Web 應用程式的意見反應論壇](https://aka.ms/webapps-uservoice)。 加入您的想法的"[Linux]"toohello 標題。

## <a name="next-steps"></a>後續步驟
* [什麼是 Linux 上的 Azure Web 應用程式？](app-service-linux-intro.md)
* [Linux 上的 Azure Web 應用程式 SSH 支援](./app-service-linux-ssh-support.md)
* [在 Azure App Service 中設定預備環境](./web-sites-staged-publishing.md)
* [在 Linux 上使用 Azure Web 應用程式持續部署](./app-service-linux-ci-cd.md)
