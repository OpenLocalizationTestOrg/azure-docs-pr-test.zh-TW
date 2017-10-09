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
# <a name="deploy-a-net-application-in-a-windows-container-tooazure-service-fabric"></a><span data-ttu-id="7d77b-104">部署 Windows 容器 tooAzure Service Fabric 中的.NET 應用程式</span><span class="sxs-lookup"><span data-stu-id="7d77b-104">Deploy a .NET application in a Windows container tooAzure Service Fabric</span></span>

<span data-ttu-id="7d77b-105">本教學課程示範如何 toodeploy 在 Azure 上的 Windows 容器中現有的 ASP.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d77b-105">This tutorial shows you how toodeploy an existing ASP.NET application in a Windows container on Azure.</span></span>

<span data-ttu-id="7d77b-106">在本教學課程中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="7d77b-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7d77b-107">在 Visual Studio 中建立 Docker 專案</span><span class="sxs-lookup"><span data-stu-id="7d77b-107">Create a Docker project in Visual Studio</span></span>
> * <span data-ttu-id="7d77b-108">將現有的應用程式容器化</span><span class="sxs-lookup"><span data-stu-id="7d77b-108">Containerize an existing application</span></span>
> * <span data-ttu-id="7d77b-109">使用 Visual Studio 和 VSTS 設定持續整合</span><span class="sxs-lookup"><span data-stu-id="7d77b-109">Setup continuous integration with Visual Studio and VSTS</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d77b-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="7d77b-110">Prerequisites</span></span>

1. <span data-ttu-id="7d77b-111">安裝 [Docker CE for Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description)，以便在 Windows 10 上執行容器。</span><span class="sxs-lookup"><span data-stu-id="7d77b-111">Install [Docker CE for Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) so that you can run containers on Windows 10.</span></span>
2. <span data-ttu-id="7d77b-112">熟悉 hello [Windows 10 容器快速入門][link-container-quickstart]。</span><span class="sxs-lookup"><span data-stu-id="7d77b-112">Familiarize yourself with hello [Windows 10 Containers quickstart][link-container-quickstart].</span></span>
3. <span data-ttu-id="7d77b-113">下載 hello [Fabrikam Fiber 撥接中心][ link-fabrikam-github]範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d77b-113">Download hello [Fabrikam Fiber CallCenter][link-fabrikam-github] sample application.</span></span>
4. <span data-ttu-id="7d77b-114">安裝 [Azure PowerShell][link-azure-powershell-install]</span><span class="sxs-lookup"><span data-stu-id="7d77b-114">Install [Azure PowerShell][link-azure-powershell-install]</span></span>
5. <span data-ttu-id="7d77b-115">安裝 hello [Visual Studio 2017 連續傳遞工具擴充功能][link-visualstudio-cd-extension]</span><span class="sxs-lookup"><span data-stu-id="7d77b-115">Install hello [Continuous Delivery Tools extension for Visual Studio 2017][link-visualstudio-cd-extension]</span></span>
6. <span data-ttu-id="7d77b-116">建立 [Azure 訂用帳戶][link-azure-subscription]和 [Visual Studio Team Services 帳戶][link-vsts-account]。</span><span class="sxs-lookup"><span data-stu-id="7d77b-116">Create an [Azure subscription][link-azure-subscription] and a [Visual Studio Team Services account][link-vsts-account].</span></span> 
7. [<span data-ttu-id="7d77b-117">在 Azure 上建立叢集</span><span class="sxs-lookup"><span data-stu-id="7d77b-117">Create a cluster on Azure</span></span>](service-fabric-tutorial-create-cluster-azure-ps.md)

## <a name="containerize-hello-application"></a><span data-ttu-id="7d77b-118">化 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="7d77b-118">Containerize hello application</span></span>

<span data-ttu-id="7d77b-119">您現在已具備[Service Fabric 叢集正在 Azure 中執行](service-fabric-tutorial-create-cluster-azure-ps.md)您已準備好 toocreate 和部署進行容器化應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d77b-119">Now that you have a [Service Fabric cluster is running in Azure](service-fabric-tutorial-create-cluster-azure-ps.md) you are ready toocreate and deploy a containerized application.</span></span> <span data-ttu-id="7d77b-120">toostart 執行我們的應用程式在容器中，我們需要 tooadd **Docker 支援**toohello Visual Studio 專案中的。</span><span class="sxs-lookup"><span data-stu-id="7d77b-120">toostart running our application in a container, we need tooadd **Docker Support** toohello project in Visual Studio.</span></span> <span data-ttu-id="7d77b-121">當您將加入**Docker 支援**toohello 應用程式中，會發生兩件事。</span><span class="sxs-lookup"><span data-stu-id="7d77b-121">When you add **Docker support** toohello application, two things happen.</span></span> <span data-ttu-id="7d77b-122">首先， _Dockerfile_加入 toohello 專案。</span><span class="sxs-lookup"><span data-stu-id="7d77b-122">First, a _Dockerfile_ is added toohello project.</span></span> <span data-ttu-id="7d77b-123">這個新的檔案描述 hello 容器映像 toobe 建置。</span><span class="sxs-lookup"><span data-stu-id="7d77b-123">This new file describes how hello container image is toobe built.</span></span> <span data-ttu-id="7d77b-124">然後第二個、 一個新_docker 撰寫_專案會加入 toohello 方案。</span><span class="sxs-lookup"><span data-stu-id="7d77b-124">Then second, a new _docker-compose_ project is added toohello solution.</span></span> <span data-ttu-id="7d77b-125">hello 新的專案包含了一些 docker 撰寫的檔案。</span><span class="sxs-lookup"><span data-stu-id="7d77b-125">hello new project contains a few docker-compose files.</span></span> <span data-ttu-id="7d77b-126">Docker 撰寫檔案可以使用的 toodescribe hello 容器的執行方式。</span><span class="sxs-lookup"><span data-stu-id="7d77b-126">Docker-compose files can be used toodescribe how hello container is run.</span></span>

<span data-ttu-id="7d77b-127">深入了解如何使用 [Visual Studio 容器工具][link-visualstudio-container-tools]。</span><span class="sxs-lookup"><span data-stu-id="7d77b-127">More info on working with [Visual Studio Container Tools][link-visualstudio-container-tools].</span></span>

>[!NOTE]
><span data-ttu-id="7d77b-128">如果您正在 Windows 容器映像電腦的第一次是 hello，Docker CE 必須提取 hello 您容器的基底映像。</span><span class="sxs-lookup"><span data-stu-id="7d77b-128">If it is hello first time you are running Windows container images on your computer, Docker CE must pull down hello base images for your containers.</span></span> <span data-ttu-id="7d77b-129">在本教學課程中使用的 hello 映像與 14 GB。</span><span class="sxs-lookup"><span data-stu-id="7d77b-129">hello images used in this tutorial are 14 GB.</span></span> <span data-ttu-id="7d77b-130">請繼續進行，然後執行下列終端機的命令 toopull hello 基底映像的 hello:</span><span class="sxs-lookup"><span data-stu-id="7d77b-130">Go ahead and run hello following terminal command toopull hello base images:</span></span>
>```cmd
>docker pull microsoft/mssql-server-windows-developer
>docker pull microsoft/aspnet:4.6.2
>```

### <a name="add-docker-support"></a><span data-ttu-id="7d77b-131">新增 Docker 支援</span><span class="sxs-lookup"><span data-stu-id="7d77b-131">Add Docker support</span></span>

<span data-ttu-id="7d77b-132">開啟 hello [FabrikamFiber.CallCenter.sln] [ link-fabrikam-github] Visual Studio 中的檔案。</span><span class="sxs-lookup"><span data-stu-id="7d77b-132">Open hello [FabrikamFiber.CallCenter.sln][link-fabrikam-github] file in Visual Studio.</span></span>

<span data-ttu-id="7d77b-133">以滑鼠右鍵按一下 hello **FabrikamFiber.Web**專案 >**新增** > **Docker 支援**。</span><span class="sxs-lookup"><span data-stu-id="7d77b-133">Right-click hello **FabrikamFiber.Web** project > **Add** > **Docker Support**.</span></span>

### <a name="add-support-for-sql"></a><span data-ttu-id="7d77b-134">新增對 SQL 的支援</span><span class="sxs-lookup"><span data-stu-id="7d77b-134">Add support for SQL</span></span>

<span data-ttu-id="7d77b-135">此應用程式使用 SQL hello 資料提供者，因此 SQL server 是必要的 toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d77b-135">This application uses SQL as hello data provider, so a SQL server is required toorun hello application.</span></span> <span data-ttu-id="7d77b-136">請參考 docker-compose.override.yml 檔案中的 SQL Server 容器映像。</span><span class="sxs-lookup"><span data-stu-id="7d77b-136">Reference a SQL Server container image in our docker-compose.override.yml file.</span></span>

<span data-ttu-id="7d77b-137">在 Visual Studio 中開啟**方案總管 中**，尋找**docker 撰寫**，和開啟 hello 檔案**docker compose.override.yml**。</span><span class="sxs-lookup"><span data-stu-id="7d77b-137">In Visual Studio, open **Solution Explorer**, find **docker-compose**, and open hello file **docker-compose.override.yml**.</span></span>

<span data-ttu-id="7d77b-138">瀏覽 toohello `services:`  節點，加入名為的節點`db:`定義 hello hello 容器的 SQL Server 項目。</span><span class="sxs-lookup"><span data-stu-id="7d77b-138">Navigate toohello `services:` node, add a node named `db:` that defines hello SQL Server entry for hello container.</span></span>

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
><span data-ttu-id="7d77b-139">您可以使用任何慣用的 SQL Server 來進行本機偵錯，只要能夠從您的主機連線到該 SQL Server 即可。</span><span class="sxs-lookup"><span data-stu-id="7d77b-139">You can use any SQL Server you prefer for local debugging, as long as it is reachable from your host.</span></span> <span data-ttu-id="7d77b-140">不過，**localdb** 不支援 `container -> host` 通訊。</span><span class="sxs-lookup"><span data-stu-id="7d77b-140">However, **localdb** does not support `container -> host` communication.</span></span>

>[!WARNING]
><span data-ttu-id="7d77b-141">執行容器中的 SQL Server 時，不支援保存資料。</span><span class="sxs-lookup"><span data-stu-id="7d77b-141">Running SQL Server in a container does not support persisting data.</span></span> <span data-ttu-id="7d77b-142">當 hello 容器停止時，會清除您的資料。</span><span class="sxs-lookup"><span data-stu-id="7d77b-142">When hello container stops, your data is erased.</span></span> <span data-ttu-id="7d77b-143">因此，請不要將這個設定用於生產環境。</span><span class="sxs-lookup"><span data-stu-id="7d77b-143">Do not use this configuration for production.</span></span>

<span data-ttu-id="7d77b-144">瀏覽 toohello`fabrikamfiber.web:`節點並新增名為的子節點`depends_on:`。</span><span class="sxs-lookup"><span data-stu-id="7d77b-144">Navigate toohello `fabrikamfiber.web:` node and add a child node named `depends_on:`.</span></span> <span data-ttu-id="7d77b-145">這可確保該 hello`db`我們的 web 應用程式 (fabrikamfiber.web) 之前啟動的服務 （SQL Server 容器 hello）。</span><span class="sxs-lookup"><span data-stu-id="7d77b-145">This ensures that hello `db` service (hello SQL Server container) starts before our web application (fabrikamfiber.web).</span></span>

```yml
  fabrikamfiber.web:
    depends_on:
      - db
```

### <a name="update-hello-web-config"></a><span data-ttu-id="7d77b-146">更新 hello 的 web 設定</span><span class="sxs-lookup"><span data-stu-id="7d77b-146">Update hello web config</span></span>

<span data-ttu-id="7d77b-147">在 hello **FabrikamFiber.Web**專案、 更新 hello 連接字串中 hello **web.config**檔案，toopoint toohello hello 容器中的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="7d77b-147">Back in hello **FabrikamFiber.Web** project, update hello connection string in hello **web.config** file, toopoint toohello SQL Server in hello container.</span></span>

```xml
<add name="FabrikamFiber-Express" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />

<add name="FabrikamFiber-DataWarehouse" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />
```

>[!NOTE]
><span data-ttu-id="7d77b-148">如果您想的 toouse web 應用程式建立不同的 SQL Server 建置發行版本時，，加入另一個連接字串 tooyour web.release.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="7d77b-148">If you want toouse a different SQL Server when building a release build of your web application, add another connection string tooyour web.release.config file.</span></span>

### <a name="test-your-container"></a><span data-ttu-id="7d77b-149">測試您的容器</span><span class="sxs-lookup"><span data-stu-id="7d77b-149">Test your container</span></span>

<span data-ttu-id="7d77b-150">按**F5** toorun 和偵錯 hello 應用程式在您的容器。</span><span class="sxs-lookup"><span data-stu-id="7d77b-150">Press **F5** toorun and debug hello application in your container.</span></span>

<span data-ttu-id="7d77b-151">邊緣會開啟您的應用程式定義的啟動頁面 hello 內部 NAT 網路 (通常 172.x.x.x) 上使用 hello 容器 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7d77b-151">Edge opens your application's defined launch page using hello IP address of hello container on hello internal NAT network (typically 172.x.x.x).</span></span> <span data-ttu-id="7d77b-152">toolearn 有關偵錯使用 Visual Studio 2017，容器中的應用程式的詳細資訊請參閱[本文][link-debug-container]。</span><span class="sxs-lookup"><span data-stu-id="7d77b-152">toolearn more about debugging applications in containers using Visual Studio 2017, see [this article][link-debug-container].</span></span>

![容器中 fabrikam 的範例][image-web-preview]

<span data-ttu-id="7d77b-154">hello 容器現在是準備 toobe 建置和封裝中的 Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d77b-154">hello container is now ready toobe built and packaged in a Service Fabric application.</span></span> <span data-ttu-id="7d77b-155">一旦您擁有 hello 建置您的電腦上的容器映像，您可以直接將其推 tooany 容器登錄中，並提取 tooany 主機 toorun。</span><span class="sxs-lookup"><span data-stu-id="7d77b-155">Once you have hello container image built on your machine, you can push it tooany container registry and pull it down tooany host toorun.</span></span>

## <a name="get-hello-application-ready-for-hello-cloud"></a><span data-ttu-id="7d77b-156">準備 hello 雲端 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="7d77b-156">Get hello application ready for hello cloud</span></span>

<span data-ttu-id="7d77b-157">tooget hello 應用程式準備好進行在 Azure 中的 Service Fabric 中執行，我們需要 toocomplete 兩個步驟：</span><span class="sxs-lookup"><span data-stu-id="7d77b-157">tooget hello application ready for running in Service Fabric in Azure, we need toocomplete two steps:</span></span>

1. <span data-ttu-id="7d77b-158">公開 hello 我們希望 toobe 無法 tooreach 我們 hello Service Fabric 叢集中的 web 應用程式的連接埠。</span><span class="sxs-lookup"><span data-stu-id="7d77b-158">Expose hello port where we want toobe able tooreach our web application in hello Service Fabric cluster.</span></span>
2. <span data-ttu-id="7d77b-159">提供適用於應用程式且準備好用於生產環境的 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="7d77b-159">Provide a production ready SQL database for our application.</span></span>

### <a name="expose-hello-port-for-hello-app"></a><span data-ttu-id="7d77b-160">公開 hello hello 應用程式的連接埠</span><span class="sxs-lookup"><span data-stu-id="7d77b-160">Expose hello port for hello app</span></span>
<span data-ttu-id="7d77b-161">我們已設定，hello Service Fabric 叢集具有連接埠*80*開啟預設會在 hello Azure 負載平衡器，平衡連入流量 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="7d77b-161">hello Service Fabric cluster we have configured, has port *80* open by default in hello Azure Load Balancer, that balances incoming traffic toohello cluster.</span></span> <span data-ttu-id="7d77b-162">透過 docker-compose.yml 檔案，我們可以在此連接埠上公開容器。</span><span class="sxs-lookup"><span data-stu-id="7d77b-162">We can expose our container on this port via our docker-compose.yml file.</span></span>

<span data-ttu-id="7d77b-163">在 Visual Studio 中開啟**方案總管 中**，尋找**docker 撰寫**，和開啟 hello 檔案**docker compose.override.yml**。</span><span class="sxs-lookup"><span data-stu-id="7d77b-163">In Visual Studio, open **Solution Explorer**, find **docker-compose**, and open hello file **docker-compose.override.yml**.</span></span>

<span data-ttu-id="7d77b-164">修改 hello `fabrikamfiber.web:`  節點，加入名為的子節點`ports:`。</span><span class="sxs-lookup"><span data-stu-id="7d77b-164">Modify hello `fabrikamfiber.web:` node, add a child node named `ports:`.</span></span>

<span data-ttu-id="7d77b-165">新增字串項目 `- "80:80"`。</span><span class="sxs-lookup"><span data-stu-id="7d77b-165">Add a string entry `- "80:80"`.</span></span>

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

### <a name="use-a-production-sql-database"></a><span data-ttu-id="7d77b-166">使用生產環境 SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="7d77b-166">Use a production SQL database</span></span>
<span data-ttu-id="7d77b-167">在生產環境中執行時，我們需要將資料保存在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="7d77b-167">When running in production, we need our data persisted in our database.</span></span> <span data-ttu-id="7d77b-168">目前沒有任何方式 tooguarantee 永續性資料的容器中，因此您無法將實際執行資料儲存在容器中的 SQL Server 中。</span><span class="sxs-lookup"><span data-stu-id="7d77b-168">There is currently no way tooguarantee persistent data in a container, therefore you cannot store production data in SQL Server in a container.</span></span>

<span data-ttu-id="7d77b-169">建議您利用 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="7d77b-169">We recommend you utilize an Azure SQL Database.</span></span> <span data-ttu-id="7d77b-170">向上 tooset 以及執行受管理的 SQL Server 在 Azure 中，瀏覽 hello [Azure SQL Database 快速入門][ link-azure-sql]發行項。</span><span class="sxs-lookup"><span data-stu-id="7d77b-170">tooset up and run a managed SQL Server in Azure, visit hello [Azure SQL Database Quickstarts][link-azure-sql] article.</span></span>

>[!NOTE]
><span data-ttu-id="7d77b-171">請記住 toochange hello 連接字串 toohello 中的 SQL server hello **web.release.config**檔案在 hello **FabrikamFiber.Web**專案。</span><span class="sxs-lookup"><span data-stu-id="7d77b-171">Remember toochange hello connection strings toohello SQL server in hello **web.release.config** file in hello **FabrikamFiber.Web** project.</span></span>
>
><span data-ttu-id="7d77b-172">如果無法連線到任何 SQL 資料庫，此應用程式會依正常程序失敗。</span><span class="sxs-lookup"><span data-stu-id="7d77b-172">This application fails gracefully if no SQL database is reachable.</span></span> <span data-ttu-id="7d77b-173">您可以選擇繼續 toogo，然後部署 hello 與任何 SQL server 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d77b-173">You can choose toogo ahead and deploy hello application with no SQL server.</span></span>

## <a name="deploy-with-visual-studio-team-services"></a><span data-ttu-id="7d77b-174">使用 Visual Studio Team Services 進行部署</span><span class="sxs-lookup"><span data-stu-id="7d77b-174">Deploy with Visual Studio Team Services</span></span>

<span data-ttu-id="7d77b-175">使用 Visual Studio Team Services 部署 tooset，您需要 tooinstall hello[連續傳遞工具擴充功能的 Visual Studio 2017][link-visualstudio-cd-extension]。</span><span class="sxs-lookup"><span data-stu-id="7d77b-175">tooset up deployment using Visual Studio Team Services, you need tooinstall hello [Continuous Delivery Tools extension for Visual Studio 2017][link-visualstudio-cd-extension].</span></span> <span data-ttu-id="7d77b-176">此延伸模組可讓您輕鬆 toodeploy tooAzure 藉由設定 Visual Studio Team Services，並取得您的應用程式部署 tooyour Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="7d77b-176">This extension makes it easy toodeploy tooAzure by configuring Visual Studio Team Services and get your app deployed tooyour Service Fabric cluster.</span></span>

<span data-ttu-id="7d77b-177">tooget 啟動，您的程式碼必須裝載在原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="7d77b-177">tooget started, your code must be hosted in source control.</span></span> <span data-ttu-id="7d77b-178">本章節 hello 其餘部分會假設**git**正在使用。</span><span class="sxs-lookup"><span data-stu-id="7d77b-178">hello rest of this section assumes **git** is being used.</span></span>

### <a name="set-up-a-vsts-repo"></a><span data-ttu-id="7d77b-179">設定 VSTS 存放庫</span><span class="sxs-lookup"><span data-stu-id="7d77b-179">Set up a VSTS repo</span></span>
<span data-ttu-id="7d77b-180">在 Visual Studio hello 右下角，按一下**新增 tooSource 控制項** > **Git** （或您偏好的任何選項）。</span><span class="sxs-lookup"><span data-stu-id="7d77b-180">At hello bottom-right corner of Visual Studio, click **Add tooSource Control** > **Git** (or whichever option you prefer).</span></span>

![按下 hello 原始檔控制 按鈕][image-source-control]

<span data-ttu-id="7d77b-182">在 [hello _Team Explorer_ ] 窗格中，按下**發行 Git 儲存機制**。</span><span class="sxs-lookup"><span data-stu-id="7d77b-182">In hello _Team Explorer_ pane, press **Publish Git Repo**.</span></span>

<span data-ttu-id="7d77b-183">選取您的 VSTS 存放庫名稱，然後按 [存放庫]。</span><span class="sxs-lookup"><span data-stu-id="7d77b-183">Select your VSTS repository name and press **Repository**.</span></span>

![發佈儲存機制 tooVSTS][image-publish-repo]

<span data-ttu-id="7d77b-185">既然您的程式碼已與 VSTS 來源存放庫同步，現在您就可以設定持續整合和持續傳遞。</span><span class="sxs-lookup"><span data-stu-id="7d77b-185">Now that your code is synchronized with a VSTS source repository, you can configure continuous integration and continuous delivery.</span></span>

### <a name="setup-continuous-delivery"></a><span data-ttu-id="7d77b-186">設定持續傳遞</span><span class="sxs-lookup"><span data-stu-id="7d77b-186">Setup continuous delivery</span></span>

<span data-ttu-id="7d77b-187">在_方案總管 中_，以滑鼠右鍵按一下 hello**方案** > **設定持續傳遞**。</span><span class="sxs-lookup"><span data-stu-id="7d77b-187">In _Solution Explorer_, right-click hello **solution** > **Configure Continuous Delivery**.</span></span>

<span data-ttu-id="7d77b-188">選取 hello Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7d77b-188">Select hello Azure Subscription.</span></span>

<span data-ttu-id="7d77b-189">設定**主機類型**太**Service Fabric 叢集**。</span><span class="sxs-lookup"><span data-stu-id="7d77b-189">Set **Host Type** too**Service Fabric Cluster**.</span></span>

<span data-ttu-id="7d77b-190">設定**目標主機**toohello hello 前一節中建立的 service fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="7d77b-190">Set **Target Host** toohello service fabric cluster you created in hello previous section.</span></span>

<span data-ttu-id="7d77b-191">選擇**容器登錄中**toopublish 至您的容器。</span><span class="sxs-lookup"><span data-stu-id="7d77b-191">Choose a **Container Registry** toopublish your container to.</span></span>

>[!TIP]
><span data-ttu-id="7d77b-192">使用 hello**編輯**按鈕 toocreate 容器登錄中。</span><span class="sxs-lookup"><span data-stu-id="7d77b-192">Use hello **Edit** button toocreate a container registry.</span></span>

<span data-ttu-id="7d77b-193">按 [確定]。</span><span class="sxs-lookup"><span data-stu-id="7d77b-193">Press **OK**.</span></span>

![設定 Service Fabric 持續整合][image-setup-ci]
   
   <span data-ttu-id="7d77b-195">Hello 組態完成後，您的容器是已部署的 tooService 網狀架構。</span><span class="sxs-lookup"><span data-stu-id="7d77b-195">Once hello configuration is completed, your container is deployed tooService Fabric.</span></span> <span data-ttu-id="7d77b-196">每當您推送更新 toohello 儲存機制會執行新組建和發行。</span><span class="sxs-lookup"><span data-stu-id="7d77b-196">Whenever you push updates toohello repository a new build and release is executed.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="7d77b-197">建置 hello 容器映像大約需要 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="7d77b-197">Building hello container images take approximately 15 minutes.</span></span>
   ><span data-ttu-id="7d77b-198">hello 第一個部署 toohello Service Fabric 叢集會造成 hello 基底 Windows Server Core 容器映像 toobe 下載。</span><span class="sxs-lookup"><span data-stu-id="7d77b-198">hello first deployment toohello Service Fabric cluster causes hello base Windows Server Core container images toobe downloaded.</span></span> <span data-ttu-id="7d77b-199">hello 下載會採用額外的 5-10 分鐘 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="7d77b-199">hello download takes additional 5-10 minutes toocomplete.</span></span>

<span data-ttu-id="7d77b-200">瀏覽 toohello Fabrikam 撥接中心的應用程式使用您的叢集 url hello： 例如， *http://mycluster.westeurope.cloudapp.azure.com*</span><span class="sxs-lookup"><span data-stu-id="7d77b-200">Browse toohello Fabrikam Call Center application using hello url of your cluster: for example, *http://mycluster.westeurope.cloudapp.azure.com*</span></span>

<span data-ttu-id="7d77b-201">既然您容器化並部署 hello Fabrikam 撥接中心的方案，您可以開啟 hello [Azure 入口網站][ link-azure-portal]並查看 hello Service Fabric 中執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d77b-201">Now that you have containerized and deployed hello Fabrikam Call Center solution, you can open hello [Azure portal][link-azure-portal] and see hello application running in Service Fabric.</span></span> <span data-ttu-id="7d77b-202">tootry hello 應用程式中，開啟網頁瀏覽器，並移 toohello Service Fabric 叢集 URL。</span><span class="sxs-lookup"><span data-stu-id="7d77b-202">tootry hello application, open a web browser and go toohello URL of your Service Fabric cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d77b-203">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7d77b-203">Next steps</span></span>

<span data-ttu-id="7d77b-204">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="7d77b-204">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7d77b-205">在 Visual Studio 中建立 Docker 專案</span><span class="sxs-lookup"><span data-stu-id="7d77b-205">Create a Docker project in Visual Studio</span></span>
> * <span data-ttu-id="7d77b-206">將現有的應用程式容器化</span><span class="sxs-lookup"><span data-stu-id="7d77b-206">Containerize an existing application</span></span>
> * <span data-ttu-id="7d77b-207">使用 Visual Studio 和 VSTS 設定持續整合</span><span class="sxs-lookup"><span data-stu-id="7d77b-207">Setup continuous integration with Visual Studio and VSTS</span></span>

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
