---
title: ".NET 應用程式中的容器 tooAzure Service Fabric aaaDeploy |Microsoft 文件"
description: "將教導您如何 toopackage Docker 容器中的 Visual Studio 中的.NET 應用程式。 這個新的\"container\"應用程式接著會部署 tooa Service Fabric 叢集。"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: mikhegn
ms.openlocfilehash: 094b0e71d76b2e56ffb9b23638dd8154b3aff5fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-net-application-in-a-windows-container-tooazure-service-fabric"></a>部署 Windows 容器 tooAzure Service Fabric 中的.NET 應用程式

本教學課程示範如何 toodeploy 在 Azure 上的 Windows 容器中現有的 ASP.NET 應用程式。

在本教學課程中，您將了解如何：

> [!div class="checklist"]
> * 在 Visual Studio 中建立 Docker 專案
> * 將現有的應用程式容器化
> * 使用 Visual Studio 和 VSTS 設定持續整合

## <a name="prerequisites"></a>必要條件

1. 安裝 [Docker CE for Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description)，以便在 Windows 10 上執行容器。
2. 熟悉 hello [Windows 10 容器快速入門][link-container-quickstart]。
3. 下載 hello [Fabrikam Fiber 撥接中心][ link-fabrikam-github]範例應用程式。
4. 安裝 [Azure PowerShell][link-azure-powershell-install]
5. 安裝 hello [Visual Studio 2017 連續傳遞工具擴充功能][link-visualstudio-cd-extension]
6. 建立 [Azure 訂用帳戶][link-azure-subscription]和 [Visual Studio Team Services 帳戶][link-vsts-account]。 
7. [在 Azure 上建立叢集](service-fabric-tutorial-create-cluster-azure-ps.md)

## <a name="containerize-hello-application"></a>化 hello 應用程式

您現在已具備[Service Fabric 叢集正在 Azure 中執行](service-fabric-tutorial-create-cluster-azure-ps.md)您已準備好 toocreate 和部署進行容器化應用程式。 toostart 執行我們的應用程式在容器中，我們需要 tooadd **Docker 支援**toohello Visual Studio 專案中的。 當您將加入**Docker 支援**toohello 應用程式中，會發生兩件事。 首先， _Dockerfile_加入 toohello 專案。 這個新的檔案描述 hello 容器映像 toobe 建置。 然後第二個、 一個新_docker 撰寫_專案會加入 toohello 方案。 hello 新的專案包含了一些 docker 撰寫的檔案。 Docker 撰寫檔案可以使用的 toodescribe hello 容器的執行方式。

深入了解如何使用 [Visual Studio 容器工具][link-visualstudio-container-tools]。

>[!NOTE]
>如果您正在 Windows 容器映像電腦的第一次是 hello，Docker CE 必須提取 hello 您容器的基底映像。 在本教學課程中使用的 hello 映像與 14 GB。 請繼續進行，然後執行下列終端機的命令 toopull hello 基底映像的 hello:
>```cmd
>docker pull microsoft/mssql-server-windows-developer
>docker pull microsoft/aspnet:4.6.2
>```

### <a name="add-docker-support"></a>新增 Docker 支援

開啟 hello [FabrikamFiber.CallCenter.sln] [ link-fabrikam-github] Visual Studio 中的檔案。

以滑鼠右鍵按一下 hello **FabrikamFiber.Web**專案 >**新增** > **Docker 支援**。

### <a name="add-support-for-sql"></a>新增對 SQL 的支援

此應用程式使用 SQL hello 資料提供者，因此 SQL server 是必要的 toorun hello 應用程式。 請參考 docker-compose.override.yml 檔案中的 SQL Server 容器映像。

在 Visual Studio 中開啟**方案總管 中**，尋找**docker 撰寫**，和開啟 hello 檔案**docker compose.override.yml**。

瀏覽 toohello `services:`  節點，加入名為的節點`db:`定義 hello hello 容器的 SQL Server 項目。

```yml
  db:
    image: microsoft/mssql-server-windows-developer
    environment:
      sa_password: "Password1"
      ACCEPT_EULA: "Y"
    ports:
      - "1433"
    healthcheck:
      test: [ "CMD", "sqlcmd", "-U", "sa", "-P", "Password1", "-Q", "select 1" ]
      interval: 1s
      retries: 20
```

>[!NOTE]
>您可以使用任何慣用的 SQL Server 來進行本機偵錯，只要能夠從您的主機連線到該 SQL Server 即可。 不過，**localdb** 不支援 `container -> host` 通訊。

>[!WARNING]
>執行容器中的 SQL Server 時，不支援保存資料。 當 hello 容器停止時，會清除您的資料。 因此，請不要將這個設定用於生產環境。

瀏覽 toohello`fabrikamfiber.web:`節點並新增名為的子節點`depends_on:`。 這可確保該 hello`db`我們的 web 應用程式 (fabrikamfiber.web) 之前啟動的服務 （SQL Server 容器 hello）。

```yml
  fabrikamfiber.web:
    depends_on:
      - db
```

### <a name="update-hello-web-config"></a>更新 hello 的 web 設定

在 hello **FabrikamFiber.Web**專案、 更新 hello 連接字串中 hello **web.config**檔案，toopoint toohello hello 容器中的 SQL Server。

```xml
<add name="FabrikamFiber-Express" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />

<add name="FabrikamFiber-DataWarehouse" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />
```

>[!NOTE]
>如果您想的 toouse web 應用程式建立不同的 SQL Server 建置發行版本時，，加入另一個連接字串 tooyour web.release.config 檔案。

### <a name="test-your-container"></a>測試您的容器

按**F5** toorun 和偵錯 hello 應用程式在您的容器。

邊緣會開啟您的應用程式定義的啟動頁面 hello 內部 NAT 網路 (通常 172.x.x.x) 上使用 hello 容器 hello IP 位址。 toolearn 有關偵錯使用 Visual Studio 2017，容器中的應用程式的詳細資訊請參閱[本文][link-debug-container]。

![容器中 fabrikam 的範例][image-web-preview]

hello 容器現在是準備 toobe 建置和封裝中的 Service Fabric 應用程式。 一旦您擁有 hello 建置您的電腦上的容器映像，您可以直接將其推 tooany 容器登錄中，並提取 tooany 主機 toorun。

## <a name="get-hello-application-ready-for-hello-cloud"></a>準備 hello 雲端 hello 應用程式

tooget hello 應用程式準備好進行在 Azure 中的 Service Fabric 中執行，我們需要 toocomplete 兩個步驟：

1. 公開 hello 我們希望 toobe 無法 tooreach 我們 hello Service Fabric 叢集中的 web 應用程式的連接埠。
2. 提供適用於應用程式且準備好用於生產環境的 SQL 資料庫。

### <a name="expose-hello-port-for-hello-app"></a>公開 hello hello 應用程式的連接埠
我們已設定，hello Service Fabric 叢集具有連接埠*80*開啟預設會在 hello Azure 負載平衡器，平衡連入流量 toohello 叢集。 透過 docker-compose.yml 檔案，我們可以在此連接埠上公開容器。

在 Visual Studio 中開啟**方案總管 中**，尋找**docker 撰寫**，和開啟 hello 檔案**docker compose.override.yml**。

修改 hello `fabrikamfiber.web:`  節點，加入名為的子節點`ports:`。

新增字串項目 `- "80:80"`。

```yml
  version: '3'

  services:
    fabrikamfiber.web:
      image: fabrikamfiber.web
      build:
        context: .\FabrikamFiber.Web
        dockerfile: Dockerfile
      ports:
        - "80:80"
```

### <a name="use-a-production-sql-database"></a>使用生產環境 SQL 資料庫
在生產環境中執行時，我們需要將資料保存在資料庫中。 目前沒有任何方式 tooguarantee 永續性資料的容器中，因此您無法將實際執行資料儲存在容器中的 SQL Server 中。

建議您利用 Azure SQL Database。 向上 tooset 以及執行受管理的 SQL Server 在 Azure 中，瀏覽 hello [Azure SQL Database 快速入門][ link-azure-sql]發行項。

>[!NOTE]
>請記住 toochange hello 連接字串 toohello 中的 SQL server hello **web.release.config**檔案在 hello **FabrikamFiber.Web**專案。
>
>如果無法連線到任何 SQL 資料庫，此應用程式會依正常程序失敗。 您可以選擇繼續 toogo，然後部署 hello 與任何 SQL server 的應用程式。

## <a name="deploy-with-visual-studio-team-services"></a>使用 Visual Studio Team Services 進行部署

使用 Visual Studio Team Services 部署 tooset，您需要 tooinstall hello[連續傳遞工具擴充功能的 Visual Studio 2017][link-visualstudio-cd-extension]。 此延伸模組可讓您輕鬆 toodeploy tooAzure 藉由設定 Visual Studio Team Services，並取得您的應用程式部署 tooyour Service Fabric 叢集。

tooget 啟動，您的程式碼必須裝載在原始檔控制。 本章節 hello 其餘部分會假設**git**正在使用。

### <a name="set-up-a-vsts-repo"></a>設定 VSTS 存放庫
在 Visual Studio hello 右下角，按一下**新增 tooSource 控制項** > **Git** （或您偏好的任何選項）。

![按下 hello 原始檔控制 按鈕][image-source-control]

在 [hello _Team Explorer_ ] 窗格中，按下**發行 Git 儲存機制**。

選取您的 VSTS 存放庫名稱，然後按 [存放庫]。

![發佈儲存機制 tooVSTS][image-publish-repo]

既然您的程式碼已與 VSTS 來源存放庫同步，現在您就可以設定持續整合和持續傳遞。

### <a name="setup-continuous-delivery"></a>設定持續傳遞

在_方案總管 中_，以滑鼠右鍵按一下 hello**方案** > **設定持續傳遞**。

選取 hello Azure 訂用帳戶。

設定**主機類型**太**Service Fabric 叢集**。

設定**目標主機**toohello hello 前一節中建立的 service fabric 叢集。

選擇**容器登錄中**toopublish 至您的容器。

>[!TIP]
>使用 hello**編輯**按鈕 toocreate 容器登錄中。

按 [確定]。

![設定 Service Fabric 持續整合][image-setup-ci]
   
   Hello 組態完成後，您的容器是已部署的 tooService 網狀架構。 每當您推送更新 toohello 儲存機制會執行新組建和發行。
   
   >[!NOTE]
   >建置 hello 容器映像大約需要 15 分鐘。
   >hello 第一個部署 toohello Service Fabric 叢集會造成 hello 基底 Windows Server Core 容器映像 toobe 下載。 hello 下載會採用額外的 5-10 分鐘 toocomplete。

瀏覽 toohello Fabrikam 撥接中心的應用程式使用您的叢集 url hello： 例如， *http://mycluster.westeurope.cloudapp.azure.com*

既然您容器化並部署 hello Fabrikam 撥接中心的方案，您可以開啟 hello [Azure 入口網站][ link-azure-portal]並查看 hello Service Fabric 中執行的應用程式。 tootry hello 應用程式中，開啟網頁瀏覽器，並移 toohello Service Fabric 叢集 URL。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何：

> [!div class="checklist"]
> * 在 Visual Studio 中建立 Docker 專案
> * 將現有的應用程式容器化
> * 使用 Visual Studio 和 VSTS 設定持續整合

<!--   NOTE SURE WHAT WE SHOULD DO YET HERE

Advance toohello next tutorial toolearn how toobind a custom SSL certificate tooit.

> [!div class="nextstepaction"]
> [Bind an existing custom SSL certificate tooAzure Web Apps](app-service-web-tutorial-custom-ssl.md)

## Next steps

- [Container Tooling in Visual Studio][link-visualstudio-container-tools]
- [Get started with containers in Service Fabric][link-servicefabric-containers]
- [Creating Service Fabric applications][link-servicefabric-createapp]
-->

[link-debug-container]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-fabrikam-github]: https://aka.ms/fabrikamcontainer
[link-container-quickstart]: /virtualization/windowscontainers/quick-start/quick-start-windows-10
[link-visualstudio-container-tools]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-azure-powershell-install]: /powershell/azure/install-azurerm-ps
[link-servicefabric-create-secure-clusters]: service-fabric-cluster-creation-via-arm.md
[link-visualstudio-cd-extension]: https://aka.ms/cd4vs
[link-servicefabric-containers]: service-fabric-get-started-containers.md
[link-servicefabric-createapp]: service-fabric-create-your-first-application-in-visual-studio.md
[link-azure-portal]: https://portal.azure.com
[link-sf-clustertemplate]: https://aka.ms/securepreviewonelineclustertemplate
[link-azure-pricing-calculator]: https://azure.microsoft.com/en-us/pricing/calculator/
[link-azure-subscription]: https://azure.microsoft.com/en-us/free/
[link-vsts-account]: https://www.visualstudio.com/team-services/pricing/
[link-azure-sql]: /azure/sql-database/

[image-web-preview]: media/service-fabric-host-app-in-a-container/fabrikam-web-sample.png
[image-source-control]: media/service-fabric-host-app-in-a-container/add-to-source-control.png
[image-publish-repo]: media/service-fabric-host-app-in-a-container/publish-repo.png
[image-setup-ci]: media/service-fabric-host-app-in-a-container/configure-continuous-integration.png
