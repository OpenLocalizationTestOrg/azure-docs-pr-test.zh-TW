---
title: "aaaCreate Azure web 應用程式在 Linux 上執行 |Microsoft 文件"
description: "針對 Linux 上的 Azure Web 應用程式建立 Web 應用程式工作流程。"
keywords: "azure app service, web 應用程式, linux, oss"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: 3a71d10a-a0fe-4d28-af95-03b2860057d5
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: de1bd030345d5e2a8024012067b5bcaa2cca09dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-web-app-running-on-linux"></a>建立在 Linux 上執行的 Azure Web 應用程式

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


## <a name="use-hello-azure-portal-toocreate-your-web-app"></a>使用 Azure 入口網站 toocreate hello 您 web 應用程式
您可以開始在 Linux 上建立 web 應用程式，從 hello [Azure 入口網站](https://portal.azure.com)hello 下列影像所示：

![開始在 hello Azure 入口網站上建立 web 應用程式][1]

接下來，hello**刀鋒視窗中建立**會開啟 hello 下列影像所示：

![刀鋒視窗中建立 hello][2]

1. 命名您的 Web 應用程式。
2. 選擇現有的資源群組或建立新群組。 (請參閱 hello 中的可用區域[限制 > 一節](app-service-linux-intro.md)。)
3. 選擇現有的 Azure App Service 方案或建立新方案。 (請參閱應用程式服務計劃在 hello[限制 > 一節](app-service-linux-intro.md)。)
4. 選擇 hello 應用程式，您還要 toouse 堆疊。 您可以從 Node.js、PHP、.Net Core、 Ruby 數種版本中選擇。

當您建立 hello 應用程式之後時，您可以變更 hello 應用程式堆疊 hello 應用程式設定 hello 下列影像所示：

![應用程式設定][3]

## <a name="deploy-your-web-app"></a>部署 Web 應用程式
選擇**部署選項**從 hello management 入口網站可讓您 hello 選項 toouse 本機 Git 或 GitHub 儲存機制 toodeploy 您的應用程式。 hello 指示 hello 其餘部分是類似 toothose，非 Linux web 應用程式。 您可以依照中的 hello 指示[本機 Git 部署](app-service-deploy-local-git.md)或[連續部署](app-service-continuous-deployment.md)toodeploy 您的應用程式。

您也可以使用 FTP tooupload 應用程式的 tooyour 站台。 您可以取得 hello FTP 端點 web 應用程式從 hello 診斷記錄 區段中 hello 下列影像所示：

![診斷記錄檔][4]

## <a name="next-steps"></a>後續步驟
* [什麼是 Linux 上的 Azure Web 應用程式？](app-service-linux-intro.md)
* [在 Linux 上的 Azure Web 應用程式中使用適用於 Node.js 的 PM2 組態](app-service-linux-using-nodejs-pm2.md)
* [在 Linux 上的 Azure App Service Web 應用程式中使用 Ruby](app-service-linux-ruby-get-started.md)
* [Linux 上的 Azure App Service Web 應用程式常見問題集](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-how-to-create-a-web-app/top-level-create.png
[2]: ./media/app-service-linux-how-to-create-a-web-app/create-blade.png
[3]: ./media/app-service-linux-how-to-create-a-web-app/application-settings-change-stack.png
[4]: ./media/app-service-linux-how-to-create-a-web-app/diagnostic-logs-ftp.png
