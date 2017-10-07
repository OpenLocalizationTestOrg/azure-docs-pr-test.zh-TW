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
# <a name="add-a-java-application-tooazure-app-service-web-apps"></a><span data-ttu-id="f48fc-103">新增 App Service Web 應用程式的 Java 應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="f48fc-103">Add a Java application tooAzure App Service Web Apps</span></span>
<span data-ttu-id="f48fc-104">初始化中的 Java web 應用程式之後[Azure App Service] [ Azure App Service]述[Java web 應用程式建立 Azure App Service 中](web-sites-java-get-started.md)，您可以藉由放置上傳您的應用程式在 hello 戰爭**webapps**資料夾。</span><span class="sxs-lookup"><span data-stu-id="f48fc-104">Once you have initialized your Java web app in [Azure App Service][Azure App Service] as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md), you can upload your application by placing your WAR in hello **webapps** folder.</span></span>

<span data-ttu-id="f48fc-105">hello 導覽路徑 toohello **webapps**資料夾不同根據您如何設定您的 Web 應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="f48fc-105">hello navigation path toohello **webapps** folder differs based on how you set up your Web Apps instance.</span></span>

* <span data-ttu-id="f48fc-106">如果您使用 Azure Marketplace hello 設定您的 web 應用程式，hello 路徑 toohello **webapps**資料夾位於 hello 表單**d:\home\site\wwwroot\bin\application\_server\webapps**，其中**應用程式\_伺服器**是 hello hello 應用程式伺服器的作用中您 Web 應用程式執行個體名稱。</span><span class="sxs-lookup"><span data-stu-id="f48fc-106">If you set up your web app by using hello Azure Marketplace, hello path toohello **webapps** folder is in hello form **d:\home\site\wwwroot\bin\application\_server\webapps**, where **application\_server** is hello name of hello application server in effect for your Web Apps instance.</span></span> 
* <span data-ttu-id="f48fc-107">如果您使用 hello Azure 組態 UI 來設定您的 web 應用程式 hello 路徑 toohello **webapps**資料夾位於 hello 表單**d:\home\site\wwwroot\webapps**。</span><span class="sxs-lookup"><span data-stu-id="f48fc-107">If you set up your web app by using hello Azure configuration UI, hello path toohello **webapps** folder is in hello form **d:\home\site\wwwroot\webapps**.</span></span> 

<span data-ttu-id="f48fc-108">請注意，您可以使用來源控制 tooupload 應用程式或網頁，包括[連續整合案例](app-service-continuous-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="f48fc-108">Note that you can use source control tooupload your application or web pages, including [continuous integration scenarios](app-service-continuous-deployment.md).</span></span> <span data-ttu-id="f48fc-109">FTP 您也可以上傳您的應用程式或 web 網頁。如需透過 FTP 部署您的應用程式的詳細資訊，請參閱[部署您的應用程式服務的應用程式 tooAzure]。</span><span class="sxs-lookup"><span data-stu-id="f48fc-109">FTP is also an option for uploading your application or web pages; for more information about deploying your applications over FTP, see [Deploy your app tooAzure App Service].</span></span>

<span data-ttu-id="f48fc-110">Tomcat web 應用程式的附註： 一旦您已上傳您的 WAR 檔案 toohello **webapps**資料夾，hello Tomcat 應用程式伺服器會偵測您已新增，並會自動載入。</span><span class="sxs-lookup"><span data-stu-id="f48fc-110">Note for Tomcat web apps: Once you've uploaded your WAR file toohello **webapps** folder, hello Tomcat application server will detect that you've added it and will automatically load it.</span></span> <span data-ttu-id="f48fc-111">請注意，是否您複製檔案 （非 WAR 檔） toohello 根目錄，hello 應用程式伺服器必須重新啟動後才能使用這些檔案的 toobe。</span><span class="sxs-lookup"><span data-stu-id="f48fc-111">Note that if you copy files (other than WAR files) toohello ROOT directory, hello application server will need toobe restarted before those files are used.</span></span> <span data-ttu-id="f48fc-112">hello Tomcat Java web 應用程式在 Azure 上執行的 hello autoload 功能根據要加入新的 WAR 檔案或新檔案或目錄加入 toohello **webapps**資料夾。</span><span class="sxs-lookup"><span data-stu-id="f48fc-112">hello autoload functionality for hello Tomcat Java web apps running on Azure is based on a new WAR file being added, or new files or directories added toohello **webapps** folder.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="f48fc-113">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f48fc-113">See Also</span></span>
<span data-ttu-id="f48fc-114">如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心]。</span><span class="sxs-lookup"><span data-stu-id="f48fc-114">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

[<span data-ttu-id="f48fc-115">application-insights-app-insights-java-get-started</span><span class="sxs-lookup"><span data-stu-id="f48fc-115">application-insights-app-insights-java-get-started</span></span>](../application-insights/app-insights-java-get-started.md)

<!-- URL List -->

[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[部署您的應用程式服務的應用程式 tooAzure]: ./web-sites-deploy.md
