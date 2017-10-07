---
title: "aaaCreate ASP.NET web 應用程式在 Azure 中的 |Microsoft 文件"
description: "了解如何 toorun web 應用程式在 Azure App Service 中部署的 hello 預設 ASP.NET web 應用程式。"
services: app-service\web
documentationcenter: 
author: cephalin
manager: wpickett
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 06/14/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: eec916b3c32b6c8b68083177938c5c822a9782b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-in-azure"></a>在 Azure 中建立 ASP.NET Web 應用程式

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) 提供可高度擴充、自我修復的 Web 主機服務。  本快速入門示範如何 toodeploy 您的第一個 ASP.NET web 應用程式 tooAzure Web 應用程式。 當您完成時，您會有已部署 Web 應用程式的資源群，其中包含 App Service 方案和 Azure Web 應用程式。

觀看 hello 視訊 toosee 本快速入門中的動作，然後依照 hello 步驟自行 toopublish.NET 應用程式第一次在 Azure 上。

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-NET-Developers/Create-a-NET-app-in-Azure-Quickstart/player]

## <a name="prerequisites"></a>必要條件

toocomplete 本教學課程：

* 安裝[Visual Studio 2017](https://www.visualstudio.com/downloads/)以下列工作負載的 hello:
    - **ASP.NET 和 Web 開發**
    - **Azure 開發**

    ![ASP.NET 和 Web 開發及 Azure 開發 (在 [Web 和雲端] 之下)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-an-aspnet-web-app"></a>建立 ASP.NET Web 應用程式

在 Visual Studio 中，選取 [檔案] > [新增] > [專案] 以建立專案。 

在 hello**新專案**對話方塊中，選取**Visual C# > Web > ASP.NET Web 應用程式 (.NET Framework)**。

Hello 應用程式命名_myFirstAzureWebApp_，然後選取**確定**。
   
![New Project dialog box](./media/app-service-web-get-started-dotnet/new-project.png)

您可以部署 ASP.NET web 應用程式 tooAzure 的任何型別。 針對本快速入門中，選取 hello **MVC**範本，並確定驗證設定得**非驗證**。
      
選取 [確定] 。

![[新增 ASP.NET 專案] 對話方塊](./media/app-service-web-get-started-dotnet/select-mvc-template.png)

從 [hello] 功能表中，選取**偵錯 > 啟動但不偵錯**toorun hello web 應用程式在本機。

![在本機執行應用程式](./media/app-service-web-get-started-dotnet/local-web-app.png)

## <a name="publish-tooazure"></a>發行 tooAzure

在 [hello**方案總管] 中**，以滑鼠右鍵按一下 hello **myFirstAzureWebApp**專案，然後選取**發行**。

![從方案總管發佈](./media/app-service-web-get-started-dotnet/solution-explorer-publish.png)

確定已選取 [Microsoft Azure App Service]，然後選取 [發佈]。

![從專案概觀頁面發佈](./media/app-service-web-get-started-dotnet/publish-to-app-service.png)

這會開啟 hello**建立 App Service**對話方塊，可協助您在 Azure 中建立所有 hello 所需的 Azure 資源 toorun hello ASP.NET web 應用程式。

## <a name="sign-in-tooazure"></a>登入 tooAzure

在 hello**建立 App Service**對話方塊中，選取**將帳戶加入**，並登入 tooyour Azure 訂用帳戶。 如果您已登入、 包含 hello 選取 hello 帳戶所需從 hello 下拉式清單中的訂用帳戶。

> [!NOTE]
> 如果您已經登入，請勿選取 [建立]。
>
>
   
![登入 tooAzure](./media/app-service-web-get-started-dotnet/sign-in-azure.png)

## <a name="create-a-resource-group"></a>建立資源群組

[!INCLUDE [resource group intro text](../../includes/resource-group.md)]

下一步太**資源群組**，選取**新增**。

名稱 hello 資源群組**myResourceGroup**選取**確定**。

## <a name="create-an-app-service-plan"></a>建立應用程式服務方案

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

下一步太**App Service 方案**，選取**新增**。 

在 [hello**設定 App Service 方案**] 對話方塊中，使用下列 hello 螢幕擷取畫面的 hello 資料表中的 hello 設定。

![建立 App Service 方案](./media/app-service-web-get-started-dotnet/configure-app-service-plan.png)

| 設定 | 建議的值 | 說明 |
|-|-|-|
|App Service 方案| myAppServicePlan | Hello 應用程式服務方案的名稱。 |
| 位置 | 西歐 | hello 資料中心裝載 hello web 應用程式的位置。 |
| 大小 | 免費 | [定價層](https://azure.microsoft.com/pricing/details/app-service/)可決定裝載功能。 |

選取 [確定] 。

## <a name="create-and-publish-hello-web-app"></a>建立及發行 hello web 應用程式

在**Web 應用程式名稱**，輸入唯一的應用程式名稱 (有效的字元是`a-z`， `0-9`，和`-`)，或接受 hello 自動產生的唯一名稱。 hello hello web 應用程式 URL 是`http://<app_name>.azurewebsites.net`，其中`<app_name>`是您的 web 應用程式名稱。

選取**建立**toostart 建立 hello Azure 資源。

![設定 Web 應用程式名稱](./media/app-service-web-get-started-dotnet/web-app-name.png)

Hello 精靈完成後，其所發行 hello ASP.NET web 應用程式 tooAzure，然後啟動 hello hello 預設瀏覽器中的應用程式。

![Azure 中已發佈的 ASP.NET Web 應用程式](./media/app-service-web-get-started-dotnet/published-azure-web-app.png)

hello hello 中指定的 web 應用程式名稱[建立及發行步驟](#create-and-publish-the-web-app)hello hello 格式的 URL 前置詞作為`http://<app_name>.azurewebsites.net`。

恭喜您，您的 ASP.NET Web 應用程式在 Azure App Service 中即時執行。

## <a name="update-hello-app-and-redeploy"></a>更新 hello 應用程式後再重新部署

從 hello**方案總管 中**，開啟_Views\Home\Index.cshtml_。

尋找 hello `<div class="jumbotron">` HTML 標記靠近 hello 頂端和 hello 整個項目取代為下列程式碼的 hello:

```HTML
<div class="jumbotron">
    <h1>ASP.NET in Azure!</h1>
    <p class="lead">This is a simple app that we’ve built that demonstrates how toodeploy a .NET app tooAzure App Service.</p>
</div>
```

tooredeploy tooAzure，以滑鼠右鍵按一下 hello **myFirstAzureWebApp**專案中**方案總管 中**選取**發行**。

在 hello、 發行頁選取**發行**。

當發行完成時，Visual Studio 會啟動瀏覽器 toohello hello web 應用程式的 URL。

![Azure 中已更新的 ASP.NET Web 應用程式](./media/app-service-web-get-started-dotnet/updated-azure-web-app.png)

## <a name="manage-hello-azure-web-app"></a>管理 hello Azure web 應用程式

移 toohello <a href="https://portal.azure.com" target="_blank">Azure 入口網站</a>toomanage hello web 應用程式。

從 hello 左窗格中，選取**應用程式服務**，然後選取 hello Azure web 應用程式名稱。

![入口網站瀏覽 tooAzure web 應用程式](./media/app-service-web-get-started-dotnet/access-portal.png)

您會看到 Web 應用程式的 [概觀] 頁面。 您可以在這裡執行基本管理工作，像是瀏覽、停止、啟動、重新啟動及刪除。 

![Azure 入口網站中的 App Service 刀鋒視窗](./media/app-service-web-get-started-dotnet/web-app-blade.png)

hello 左側的功能表提供不同頁面設定您的應用程式。 

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [ASP.NET 搭配 SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md)
