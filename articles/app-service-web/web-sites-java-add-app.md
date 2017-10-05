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
ms.openlocfilehash: c28e7c499ed02b759df580f4b14a971b6aec5b67
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-java-application-to-azure-app-service-web-apps"></a><span data-ttu-id="b9586-103">將 Java 應用程式新增至 Azure App Service Web Apps</span><span class="sxs-lookup"><span data-stu-id="b9586-103">Add a Java application to Azure App Service Web Apps</span></span>
<span data-ttu-id="b9586-104">在您已依照[在 Azure App Service 中建立 Java Web 應用程式](web-sites-java-get-started.md)所述，在 [Azure App Service][Azure App Service] 中將 Java Web 應用程式初始化之後，就可以將 WAR 放在 [webapps] 資料夾中來上傳您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b9586-104">Once you have initialized your Java web app in [Azure App Service][Azure App Service] as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md), you can upload your application by placing your WAR in the **webapps** folder.</span></span>

<span data-ttu-id="b9586-105">**webapps** 資料夾的導覽路徑會根據 Web Apps 執行個體的設定方式而有所不同。</span><span class="sxs-lookup"><span data-stu-id="b9586-105">The navigation path to the **webapps** folder differs based on how you set up your Web Apps instance.</span></span>

* <span data-ttu-id="b9586-106">如果您使用 Azure Marketplace 來設定 Web Apps，則 **webapps** 資料夾的路徑會是 **d:\home\site\wwwroot\bin\application\_server\webapps** 的格式，其中 **application\_server** 是您 Web Apps 執行個體中生效的應用程式伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="b9586-106">If you set up your web app by using the Azure Marketplace, the path to the **webapps** folder is in the form **d:\home\site\wwwroot\bin\application\_server\webapps**, where **application\_server** is the name of the application server in effect for your Web Apps instance.</span></span> 
* <span data-ttu-id="b9586-107">如果您使用 Azure 組態 UI 來設定 Web 應用程式，則 **webapps** 資料夾的路徑會是 **d:\home\site\wwwroot\webapps** 的格式。</span><span class="sxs-lookup"><span data-stu-id="b9586-107">If you set up your web app by using the Azure configuration UI, the path to the **webapps** folder is in the form **d:\home\site\wwwroot\webapps**.</span></span> 

<span data-ttu-id="b9586-108">請注意，您可以使用原始檔控制來上傳應用程式或網頁，包括 [連續整合案例](app-service-continuous-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="b9586-108">Note that you can use source control to upload your application or web pages, including [continuous integration scenarios](app-service-continuous-deployment.md).</span></span> <span data-ttu-id="b9586-109">FTP 也是上傳您的應用程式或網頁的選項，如需透過 FTP 部署您應用程式的詳細資訊，請參閱 [將應用程式部署至 Azure App Service]。</span><span class="sxs-lookup"><span data-stu-id="b9586-109">FTP is also an option for uploading your application or web pages; for more information about deploying your applications over FTP, see [Deploy your app to Azure App Service].</span></span>

<span data-ttu-id="b9586-110">Tomcat Web 應用程式注意事項：將 WAR 檔案上傳至 **webapps** 資料夾之後，Tomcat 應用程式伺服器便會偵測到您已新增該檔案，並會將其自動載入。</span><span class="sxs-lookup"><span data-stu-id="b9586-110">Note for Tomcat web apps: Once you've uploaded your WAR file to the **webapps** folder, the Tomcat application server will detect that you've added it and will automatically load it.</span></span> <span data-ttu-id="b9586-111">請注意，如果您將檔案 (WAR 檔案除外) 複製到根目錄，則在使用這些檔案之前，必須重新啟動應用程式伺服器。</span><span class="sxs-lookup"><span data-stu-id="b9586-111">Note that if you copy files (other than WAR files) to the ROOT directory, the application server will need to be restarted before those files are used.</span></span> <span data-ttu-id="b9586-112">在 Azure 上執行的 Tomcat Java Web 應用程式，其自動載入功能會視新增的 WAR 檔案或新增至 **webapps** 資料夾的新檔案或目錄而定。</span><span class="sxs-lookup"><span data-stu-id="b9586-112">The autoload functionality for the Tomcat Java web apps running on Azure is based on a new WAR file being added, or new files or directories added to the **webapps** folder.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="b9586-113">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b9586-113">See Also</span></span>
<span data-ttu-id="b9586-114">如需如何搭配使用 Azure 與 Java 的詳細資訊，請參閱 [Azure Java 開發人員中心]。</span><span class="sxs-lookup"><span data-stu-id="b9586-114">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

[<span data-ttu-id="b9586-115">application-insights-app-insights-java-get-started</span><span class="sxs-lookup"><span data-stu-id="b9586-115">application-insights-app-insights-java-get-started</span></span>](../application-insights/app-insights-java-get-started.md)

<!-- URL List -->

<span data-ttu-id="b9586-116">[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="b9586-116">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
<span data-ttu-id="b9586-117">[將應用程式部署至 Azure App Service]: ./web-sites-deploy.md</span><span class="sxs-lookup"><span data-stu-id="b9586-117">[Deploy your app to Azure App Service]: ./web-sites-deploy.md</span></span>
