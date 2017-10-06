---
title: "aaaDeploy 使用 Visual Studio 的 WebJobs"
description: "深入了解如何 toodeploy Azure WebJobs tooAzure App Service Web 應用程式使用 Visual Studio。"
services: app-service
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: a3a9d320-1201-4ac8-9398-b4c9535ba755
ms.service: app-service
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2016
ms.author: glenga
ms.openlocfilehash: 5fc5d9562e8836348f5ab6844fb6c23ff40a321c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-webjobs-using-visual-studio"></a>使用 Visual Studio 部署 WebJob
## <a name="overview"></a>概觀
本主題說明如何 toouse Visual Studio toodeploy 主控台應用程式專案中的 tooa web 應用程式[App Service](http://go.microsoft.com/fwlink/?LinkId=529714)為[Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226)。 如需如何使用 toodeploy WebJobs hello [Azure 入口網站](https://portal.azure.com)，請參閱[以 WebJobs 執行背景工作](web-sites-create-web-jobs.md)。

當 Visual Studio 部署具有 WebJobs 功能的主控台應用程式專案時，它會執行兩個工作：

* 複製執行階段檔案 toohello hello web 應用程式中適當的資料夾 (*App_Data/工作/連續*連續 web 工作，如*App_Data/工作/觸發*排程或隨選 Webjob 的)。
* 設定[Azure 排程器作業](#scheduler)個是在特定時間排程的 toorun 的 WebJobs。 (無需為連續 WebJobs 執行此動作。)

啟用 WebJobs 的專案具有下列項目加入的 tooit hello:

* hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet 封裝。
* 包含部署和排程器設定的 [webjob-publish-settings.json](#publishsettings) 檔案。 

![顯示項目會成為 WebJob tooa 主控台應用程式 tooenable 部署的圖表](./media/websites-dotnet-deploy-webjobs/convert.png)

您可以加入這些項目 tooan，現有的主控台應用程式專案，或使用範本 toocreate 新的 Webjob 功能的主控台應用程式專案。 

您可以部署專案 webjob 本身，或將其連結 tooa web 專案，讓它自動將部署時部署 hello web 專案。 toolink 專案，Visual Studio 包含 hello hello 啟用 WebJobs 的專案名稱[webjobs list.json](#webjobslist) hello web 專案中的檔案。

![顯示連結 tooweb 專案 WebJob 專案的圖表](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a>必要條件
當您安裝 hello Azure SDK for.NET 時，可提供 Visual Studio 中使用 WebJobs 部署功能：

* [Azure SDK for .NET (Visual Studio)](https://azure.microsoft.com/downloads/)。

## <a id="convert"></a>啟用現有主控台應用程式專案的 WebJobs 部署
您有兩個選擇：

* [透過 Web 專案啟用自動部署](#convertlink)。
  
    設定現有主控台應用程式專案，以便在您部署 Web 專案時，它會以 WebJob 的方式自動部署。 當您想 toorun 您在 hello 中的 WebJob，請使用此選項讓您執行 hello 的相同 web 應用程式相關的 web 應用程式。
* [不透過 Web 專案啟用部署](#convertnolink)。
  
    設定現有的主控台應用程式專案 toodeploy webjob 單獨使用時，與沒有連結 tooa web 專案。 當您單獨使用時，想 toorun web 應用程式中的 WebJob 與 hello web 應用程式中執行任何 web 應用程式時，請使用此選項。 您可能想要 toodo 這在順序 toobe 無法 tooscale WebJob 資源與您的 web 應用程式資源分開。

### <a id="convertlink"></a> 透過 Web 專案啟用自動 WebJobs 部署
1. 中的以滑鼠右鍵按一下 hello web 專案**方案總管 中**，然後按一下**新增** > **現有 Azure WebJob 專案**。
   
    ![Existing Project as Azure WebJob](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    hello[新增 Azure WebJob](#configure)  對話方塊隨即出現。
2. 在 hello**專案名稱**下拉式清單中，選取 hello 主控台應用程式專案 tooadd webjob。
   
    ![Selecting project in Add Azure WebJob dialog](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. 完整的 hello[新增 Azure WebJob](#configure)對話方塊，然後再按一下**確定**。 

### <a id="convertnolink"></a> 不透過 Web 專案啟用 WebJobs 部署
1. 以滑鼠右鍵按一下 hello 主控台應用程式專案中的**方案總管 中**，然後按一下**發行為 Azure WebJob...**. 
   
    ![發行為 Azure WebJob](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    hello[新增 Azure WebJob](#configure)  對話方塊隨即出現，並選取 hello 中的 hello 專案**專案名稱**方塊。
2. 完整的 hello[新增 Azure WebJob](#configure)對話方塊，然後按一下**確定**。
   
   hello**發行 Web**精靈 隨即出現。  如果您不立即想 toopublish，關閉 hello 精靈。 您輸入的 hello 設定會儲存的當您想太[部署 hello 專案](#deploy)。

## <a id="create"></a>建立具有 WebJobs 功能的新專案
toocreate 新的 Webjob 啟用專案，您可以使用 hello 主控台應用程式專案範本，並啟用 WebJobs 部署中所述[hello 上一節](#convert)。 或者，您可以使用 hello WebJobs 新專案範本：

* [使用獨立的 WebJob hello WebJobs 新專案範本](#createnolink)
  
    建立專案並且設定該 toodeploy 本身 webjob，與沒有連結 tooa web 專案。 當您單獨使用時，想 toorun web 應用程式中的 WebJob 與 hello web 應用程式中執行任何 web 應用程式時，請使用此選項。 您可能想要 toodo 這在順序 toobe 無法 tooscale WebJob 資源與您的 web 應用程式資源分開。
* [WebJob 連結的 tooa web 專案使用 hello WebJobs 新專案範本](#createlink)
  
    建立專案，會自動設定的 toodeploy webjob hello 部署相同方案中的 web 專案時。 當您想 toorun 您在 hello 中的 WebJob，請使用此選項讓您執行 hello 的相同 web 應用程式相關的 web 應用程式。

> [!NOTE]
> hello WebJobs 新專案範本自動安裝 NuGet 封裝，並包含程式碼中的*Program.cs* hello [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs)。 如果您不想 toouse hello WebJobs SDK，移除或變更 hello`host.RunAndBlock`陳述式中的*Program.cs*。
> 
> 

### <a id="createnolink"></a>使用獨立的 WebJob hello WebJobs 新專案範本
1. 按一下**檔案** > **新專案**，然後在 hello**新專案**對話方塊中，按一下**雲端** >  **Azure WebJob (.NET Framework)**。
   
    ![顯示 WebJob 範本的 [新增專案] 對話方塊](./media/websites-dotnet-deploy-webjobs/np.png)
2. 請依照稍早所示的 hello 指示太[進行獨立的 Webjob 專案 hello 主控台應用程式專案](#convertnolink)。

### <a id="createlink"></a>WebJob 連結的 tooa web 專案使用 hello WebJobs 新專案範本
1. 中的以滑鼠右鍵按一下 hello web 專案**方案總管 中**，然後按一下**新增** > **新增 Azure WebJob 專案**。
   
    ![New Azure WebJob Project menu entry](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    hello[新增 Azure WebJob](#configure)  對話方塊隨即出現。
2. 完整的 hello[新增 Azure WebJob](#configure)對話方塊，然後按一下**確定**。

## <a id="configure"></a>hello 新增 Azure WebJob 對話方塊
hello**新增 Azure WebJob**對話方塊可讓您輸入 hello web 工作名稱和執行您 web 工作的模式設定。 

![[加入 Azure WebJob] 對話方塊](./media/websites-dotnet-deploy-webjobs/aaw2.png)

在這個對話方塊中的 hello 欄位對應上 hello toofields**新工作**hello Azure 入口網站 對話方塊。 如需詳細資訊，請參閱[使用 WebJobs 執行背景工作](web-sites-create-web-jobs.md)。

> [!NOTE]
> * 如需命令列部署的詳細資訊，請參閱[啟用 Azure WebJobs 的命令列或連續傳遞](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/)。
> * 如果您部署 WebJob，然後決定您想 toochange hello 類型 WebJob 和重新部署時，您將需要 toodelete hello webjobs 發佈 settings.json 檔案。 這會讓 Visual Studio 顯示 hello 同樣地，發行選項，因此您可以變更 WebJob hello 型別。
> * 如果您部署 WebJob 和在之後變更 hello 執行的模式中從連續 toonon 連續或反之亦然，Visual Studio 會建立新的 WebJob 在 Azure 中重新部署時。 如果您變更排程的其他設定，但保留執行模式 hello 相同，或已排程和隨選之間切換，Visual Studio 更新 hello 現有的工作而非建立新的連線。
> 
> 

## <a id="publishsettings"></a>webjob-publish-settings.json
當您設定部署 WebJobs 的主控台應用程式時，Visual Studio 會安裝 hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet 封裝和排程資訊中的存放區*webjob 發行 settings.json* hello 專案檔案中的*屬性*hello Webjob 專案的資料夾。 以下是該檔案的範例：

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

您可以編輯此檔案目錄，而 Visual Studio 會提供 IntelliSense。 hello 檔案結構描述儲存在[http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json)而且可以那里檢視。  

## <a id="webjobslist"></a>webjobs-list.json
當您連結 WebJobs 啟用專案 tooa web 專案時，Visual Studio 會儲存 hello Webjob 專案的 hello 名稱*webjobs list.json* hello web 專案的檔案中*屬性*資料夾。 hello 清單可能包含多個 WebJobs 的專案，hello 下列範例所示：

        {
          "$schema": "http://schemastore.org/schemas/json/webjobs-list.json",
          "WebJobs": [
            {
              "filePath": "../ConsoleApplication1/ConsoleApplication1.csproj"
            },
            {
              "filePath": "../WebJob1/WebJob1.csproj"
            }
          ]
        }

您可以編輯此檔案目錄，而 Visual Studio 會提供 IntelliSense。 hello 檔案結構描述儲存在[http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json)而且可以那里檢視。

## <a id="deploy"></a>部署 WebJobs 專案
您已連結 tooa web 專案的 Webjob 專案會自動部署與 hello web 專案。 Web 專案部署的相關資訊，請參閱[如何 toodeploy tooWeb 應用程式](web-sites-deploy.md)。

toodeploy Webjob 專案本身，以滑鼠右鍵按一下中的 hello 專案**方案總管 中**按一下**發行為 Azure WebJob...**. 

![發行為 Azure WebJob](./media/websites-dotnet-deploy-webjobs/paw.png)

獨立的 web 工作，如 hello 相同**發行 Web**使用 web 專案會顯示，但使用較少的設定可用 toochange 精靈。

## <a id="nextsteps"></a>後續步驟
本文說明如何使用 Visual Studio toodeploy WebJobs。 如需有關如何 toodeploy Azure Webjob，請參閱[Azure WebJobs-資源-建議部署](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying)。

