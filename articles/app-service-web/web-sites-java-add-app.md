---
title: "aaaAdd Java 應用程式 tooAzure App Service Web 應用程式"
description: "本教學課程會示範如何 tooadd 網頁或應用程式 tooyour 執行個體的 Azure App Service Web 應用程式已設定 toouse Java。"
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9b46528b-e2d0-4f26-b8d7-af94bd8c31ef
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 2feb464b2933921ad2887779a6b7589634e2e2f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-java-application-tooazure-app-service-web-apps"></a>新增 App Service Web 應用程式的 Java 應用程式 tooAzure
初始化中的 Java web 應用程式之後[Azure App Service] [ Azure App Service]述[Java web 應用程式建立 Azure App Service 中](web-sites-java-get-started.md)，您可以藉由放置上傳您的應用程式在 hello 戰爭**webapps**資料夾。

hello 導覽路徑 toohello **webapps**資料夾不同根據您如何設定您的 Web 應用程式執行個體。

* 如果您使用 Azure Marketplace hello 設定您的 web 應用程式，hello 路徑 toohello **webapps**資料夾位於 hello 表單**d:\home\site\wwwroot\bin\application\_server\webapps**，其中**應用程式\_伺服器**是 hello hello 應用程式伺服器的作用中您 Web 應用程式執行個體名稱。 
* 如果您使用 hello Azure 組態 UI 來設定您的 web 應用程式 hello 路徑 toohello **webapps**資料夾位於 hello 表單**d:\home\site\wwwroot\webapps**。 

請注意，您可以使用來源控制 tooupload 應用程式或網頁，包括[連續整合案例](app-service-continuous-deployment.md)。 FTP 您也可以上傳您的應用程式或 web 網頁。如需透過 FTP 部署您的應用程式的詳細資訊，請參閱[部署您的應用程式服務的應用程式 tooAzure]。

Tomcat web 應用程式的附註： 一旦您已上傳您的 WAR 檔案 toohello **webapps**資料夾，hello Tomcat 應用程式伺服器會偵測您已新增，並會自動載入。 請注意，是否您複製檔案 （非 WAR 檔） toohello 根目錄，hello 應用程式伺服器必須重新啟動後才能使用這些檔案的 toobe。 hello Tomcat Java web 應用程式在 Azure 上執行的 hello autoload 功能根據要加入新的 WAR 檔案或新檔案或目錄加入 toohello **webapps**資料夾。 

<a name="see-also"></a>

## <a name="see-also"></a>另請參閱
如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心]。

[application-insights-app-insights-java-get-started](../application-insights/app-insights-java-get-started.md)

<!-- URL List -->

[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[部署您的應用程式服務的應用程式 tooAzure]: ./web-sites-deploy.md
