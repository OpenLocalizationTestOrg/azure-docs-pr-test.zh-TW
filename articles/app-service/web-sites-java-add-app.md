---
title: "將 Java 應用程式新增至 Azure App Service Web Apps"
description: "本教學課程說明如何將頁面或應用程式新增至已設定為使用 Java 的 Azure App Service Web Apps 執行個體。"
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
ms.openlocfilehash: 1309985d7f1b93230b38ada2ee2687b1db10a791
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2017
---
# <a name="add-a-java-application-to-azure-app-service-web-apps"></a>將 Java 應用程式新增至 Azure App Service Web Apps
在您已依照[在 Azure App Service 中建立 Java Web 應用程式](app-service-web-get-started-java.md)所述，在 [Azure App Service][Azure App Service] 中將 Java Web 應用程式初始化之後，就可以將 WAR 放在 [webapps] 資料夾中來上傳您的應用程式。

**webapps** 資料夾的導覽路徑會根據 Web Apps 執行個體的設定方式而有所不同。

* 如果您使用 Azure Marketplace 來設定 Web Apps，則 **webapps** 資料夾的路徑會是 **d:\home\site\wwwroot\bin\application\_server\webapps** 的格式，其中 **application\_server** 是您 Web Apps 執行個體中生效的應用程式伺服器的名稱。 
* 如果您使用 Azure 組態 UI 來設定 Web 應用程式，則 **webapps** 資料夾的路徑會是 **d:\home\site\wwwroot\webapps** 的格式。 

請注意，您可以使用原始檔控制來上傳應用程式或網頁，包括 [連續整合案例](app-service-continuous-deployment.md)。 FTP 也是上傳您的應用程式或網頁的選項，如需透過 FTP 部署您應用程式的詳細資訊，請參閱[使用 FTP 部署應用程式](app-service-deploy-ftp.md)。

Tomcat Web 應用程式注意事項：將 WAR 檔案上傳至 **webapps** 資料夾之後，Tomcat 應用程式伺服器便會偵測到您已新增該檔案，並會將其自動載入。 請注意，如果您將檔案 (WAR 檔案除外) 複製到根目錄，則在使用這些檔案之前，必須重新啟動應用程式伺服器。 在 Azure 上執行的 Tomcat Java Web 應用程式，其自動載入功能會視新增的 WAR 檔案或新增至 **webapps** 資料夾的新檔案或目錄而定。 

<a name="see-also"></a>

## <a name="see-also"></a>另請參閱
如需如何搭配使用 Azure 與 Java 的詳細資訊，請參閱 [Azure Java 開發人員中心]。

[application-insights-app-insights-java-get-started](../application-insights/app-insights-java-get-started.md)

<!-- URL List -->

[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
