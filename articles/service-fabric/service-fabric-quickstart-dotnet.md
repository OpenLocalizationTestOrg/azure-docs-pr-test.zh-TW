---
title: "在 Azure 中的.NET Service Fabric 應用程式 aaaCreate |Microsoft 文件"
description: "Azure 使用 hello Service Fabric 快速入門範例建立.NET 應用程式。"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: msfussell
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: mikhegn
ms.openlocfilehash: 20ef88dbf9fb0def31234ef05679a19009b9b529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-net-service-fabric-application-in-azure"></a><span data-ttu-id="8a073-103">在 Azure 中建立 .NET Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="8a073-103">Create a .NET Service Fabric application in Azure</span></span>
<span data-ttu-id="8a073-104">Azure Service Fabric 是一個分散式系統平台，可讓您部署及管理可調整和可信賴的微服務與容器。</span><span class="sxs-lookup"><span data-stu-id="8a073-104">Azure Service Fabric is a distributed systems platform for deploying and managing scalable and reliable microservices and containers.</span></span> 

<span data-ttu-id="8a073-105">本快速入門示範如何 toodeploy 您第一次的.NET 應用程式 tooService 網狀架構。</span><span class="sxs-lookup"><span data-stu-id="8a073-105">This quickstart shows how toodeploy your first .NET application tooService Fabric.</span></span> <span data-ttu-id="8a073-106">當您完成時，必須具有 ASP.NET Core web 前端，將投票的結果儲存在可設定狀態的後端服務 hello 叢集中的投票應用程式。</span><span class="sxs-lookup"><span data-stu-id="8a073-106">When you're finished, you have a voting application with an ASP.NET Core web front-end that saves voting results in a stateful back-end service in hello cluster.</span></span>

![應用程式螢幕擷取畫面](./media/service-fabric-quickstart-dotnet/application-screenshot.png)

<span data-ttu-id="8a073-108">使用此應用程式，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="8a073-108">Using this application you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="8a073-109">建立使用 .NET 和 Service Fabric 的應用程式</span><span class="sxs-lookup"><span data-stu-id="8a073-109">Create an application using .NET and Service Fabric</span></span>
> * <span data-ttu-id="8a073-110">使用 ASP.NET Core 作為 Web 前端</span><span class="sxs-lookup"><span data-stu-id="8a073-110">Use ASP.NET core as a web front-end</span></span>
> * <span data-ttu-id="8a073-111">將應用程式資料儲存在具狀態服務中</span><span class="sxs-lookup"><span data-stu-id="8a073-111">Store application data in a stateful service</span></span>
> * <span data-ttu-id="8a073-112">在本機偵錯您的應用程式</span><span class="sxs-lookup"><span data-stu-id="8a073-112">Debug your application locally</span></span>
> * <span data-ttu-id="8a073-113">部署在 Azure 中的 hello 應用程式 tooa 叢集</span><span class="sxs-lookup"><span data-stu-id="8a073-113">Deploy hello application tooa cluster in Azure</span></span>
> * <span data-ttu-id="8a073-114">在多個節點的向外延展 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="8a073-114">Scale-out hello application across multiple nodes</span></span>
> * <span data-ttu-id="8a073-115">執行輪流應用程式升級</span><span class="sxs-lookup"><span data-stu-id="8a073-115">Perform a rolling application upgrade</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a073-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="8a073-116">Prerequisites</span></span>
<span data-ttu-id="8a073-117">toocomplete 本快速入門：</span><span class="sxs-lookup"><span data-stu-id="8a073-117">toocomplete this quickstart:</span></span>
1. <span data-ttu-id="8a073-118">[安裝 Visual Studio 2017](https://www.visualstudio.com/)以 hello **Azure 開發**和**ASP.NET 及 web 開發**工作負載。</span><span class="sxs-lookup"><span data-stu-id="8a073-118">[Install Visual Studio 2017](https://www.visualstudio.com/) with hello **Azure development** and **ASP.NET and web development** workloads.</span></span>
2. [<span data-ttu-id="8a073-119">安裝 Git</span><span class="sxs-lookup"><span data-stu-id="8a073-119">Install Git</span></span>](https://git-scm.com/)
3. [<span data-ttu-id="8a073-120">安裝 Microsoft Azure Service Fabric SDK hello</span><span class="sxs-lookup"><span data-stu-id="8a073-120">Install hello Microsoft Azure Service Fabric SDK</span></span>](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK)
4. <span data-ttu-id="8a073-121">執行下列命令 tooenable Visual Studio toodeploy toohello 本機 Service Fabric 叢集 hello:</span><span class="sxs-lookup"><span data-stu-id="8a073-121">Run hello following command tooenable Visual Studio toodeploy toohello local Service Fabric cluster:</span></span>
    ```powershell
    Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
    ```

## <a name="download-hello-sample"></a><span data-ttu-id="8a073-122">下載 hello 範例</span><span class="sxs-lookup"><span data-stu-id="8a073-122">Download hello sample</span></span>
<span data-ttu-id="8a073-123">在命令視窗中，執行下列命令 tooclone hello 範例應用程式儲存機制 tooyour 本機電腦的 hello。</span><span class="sxs-lookup"><span data-stu-id="8a073-123">In a command window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>
```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="run-hello-application-locally"></a><span data-ttu-id="8a073-124">在本機執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="8a073-124">Run hello application locally</span></span>
<span data-ttu-id="8a073-125">Hello hello 開始] 功能表中的 Visual Studio 圖示上按一下滑鼠右鍵，然後選擇 [**系統管理員身分執行**。</span><span class="sxs-lookup"><span data-stu-id="8a073-125">Right-click hello Visual Studio icon in hello Start Menu and choose **Run as administrator**.</span></span> <span data-ttu-id="8a073-126">在順序 tooattach hello 偵錯工具 tooyour services 中，您會需要 toorun Visual Studio 系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="8a073-126">In order tooattach hello debugger tooyour services, you need toorun Visual Studio as administrator.</span></span>

<span data-ttu-id="8a073-127">開啟 hello **Voting.sln** hello 您用於複製的儲存機制中的 Visual Studio 方案。</span><span class="sxs-lookup"><span data-stu-id="8a073-127">Open hello **Voting.sln** Visual Studio solution from hello repository you cloned.</span></span>

<span data-ttu-id="8a073-128">toodeploy hello 應用程式，請按**F5**。</span><span class="sxs-lookup"><span data-stu-id="8a073-128">toodeploy hello application, press **F5**.</span></span>

> [!NOTE]
> <span data-ttu-id="8a073-129">hello 第一次執行，並部署 hello 應用程式，Visual Studio 會建立偵錯的本機叢集。</span><span class="sxs-lookup"><span data-stu-id="8a073-129">hello first time you run and deploy hello application, Visual Studio creates a local cluster for debugging.</span></span> <span data-ttu-id="8a073-130">這項作業可能需要一些時間。</span><span class="sxs-lookup"><span data-stu-id="8a073-130">This operation may take some time.</span></span> <span data-ttu-id="8a073-131">hello Visual Studio 輸出 視窗中會顯示 hello 叢集建立狀態。</span><span class="sxs-lookup"><span data-stu-id="8a073-131">hello cluster creation status is displayed in hello Visual Studio output window.</span></span>

<span data-ttu-id="8a073-132">Hello 部署完成後，啟動瀏覽器，並開啟此頁面： `http://localhost:8080` -hello web 前端的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8a073-132">When hello deployment is complete, launch a browser and open this page: `http://localhost:8080` - hello web front-end of hello application.</span></span>

![應用程式前端](./media/service-fabric-quickstart-dotnet/application-screenshot-new.png)

<span data-ttu-id="8a073-134">您現在可以新增一組投票選項，並開始進行投票。</span><span class="sxs-lookup"><span data-stu-id="8a073-134">You can now add a set of voting options, and start taking votes.</span></span> <span data-ttu-id="8a073-135">hello 應用程式執行，並將所有資料都儲存在 Service Fabric 叢集中，而需要不同的資料庫在 hello。</span><span class="sxs-lookup"><span data-stu-id="8a073-135">hello application runs and stores all data in your Service Fabric cluster, without hello need for a separate database.</span></span>

## <a name="walk-through-hello-voting-sample-application"></a><span data-ttu-id="8a073-136">逐步解說 hello 投票範例應用程式</span><span class="sxs-lookup"><span data-stu-id="8a073-136">Walk through hello voting sample application</span></span>
<span data-ttu-id="8a073-137">hello 投票應用程式是由兩個服務所組成：</span><span class="sxs-lookup"><span data-stu-id="8a073-137">hello voting application consists of two services:</span></span>
- <span data-ttu-id="8a073-138">Web 前端服務 (VotingWeb)-ASP.NET Core web 前端服務，會做 hello 網頁，並公開 web Api toocommunicate 與 hello 後端服務。</span><span class="sxs-lookup"><span data-stu-id="8a073-138">Web front-end service (VotingWeb)- An ASP.NET Core web front-end service, which serves hello web page and exposes web APIs toocommunicate with hello backend service.</span></span>
- <span data-ttu-id="8a073-139">後端服務 (VotingData)-ASP.NET Core web 服務會公開 API toostore hello 投票結果可靠的字典中保存在磁碟。</span><span class="sxs-lookup"><span data-stu-id="8a073-139">Back-end service (VotingData)- An ASP.NET Core web service, which exposes an API toostore hello vote results in a reliable dictionary persisted on disk.</span></span>

![應用程式圖表](./media/service-fabric-quickstart-dotnet/application-diagram.png)

<span data-ttu-id="8a073-141">當您在下列的 hello 應用程式 hello 投票事件就會發生：</span><span class="sxs-lookup"><span data-stu-id="8a073-141">When you vote in hello application hello following events occur:</span></span>
1. <span data-ttu-id="8a073-142">JavaScript 會以 HTTP PUT 要求傳送 hello web 前端服務中的 hello 投票要求 toohello web API。</span><span class="sxs-lookup"><span data-stu-id="8a073-142">A JavaScript sends hello vote request toohello web API in hello web front-end service as an HTTP PUT request.</span></span>

2. <span data-ttu-id="8a073-143">hello web 前端服務會使用 proxy toolocate 及轉送 HTTP PUT 要求 toohello 後端服務。</span><span class="sxs-lookup"><span data-stu-id="8a073-143">hello web front-end service uses a proxy toolocate and forward an HTTP PUT request toohello back-end service.</span></span>

3. <span data-ttu-id="8a073-144">hello 後端服務大約需要 hello 傳入的要求，並儲存區 hello 更新在可靠字典中，取得複寫的 toomultiple hello 叢集中的節點，並保存在磁碟上的結果。</span><span class="sxs-lookup"><span data-stu-id="8a073-144">hello back-end service takes hello incoming request, and stores hello updated result in a reliable dictionary, which gets replicated toomultiple nodes within hello cluster and persisted on disk.</span></span> <span data-ttu-id="8a073-145">所有 hello 應用程式的資料儲存在 hello 叢集中，因此不需要任何資料庫。</span><span class="sxs-lookup"><span data-stu-id="8a073-145">All hello application's data is stored in hello cluster, so no database is needed.</span></span>

## <a name="debug-in-visual-studio"></a><span data-ttu-id="8a073-146">在 Visual Studio 中偵錯</span><span class="sxs-lookup"><span data-stu-id="8a073-146">Debug in Visual Studio</span></span>
<span data-ttu-id="8a073-147">在 Visual Studio 中偵錯應用程式時，您會使用本機 Service Fabric 開發叢集。</span><span class="sxs-lookup"><span data-stu-id="8a073-147">When debugging application in Visual Studio, you are using a local Service Fabric development cluster.</span></span> <span data-ttu-id="8a073-148">您擁有 hello 選項 tooadjust 您偵錯的體驗 tooyour 案例。</span><span class="sxs-lookup"><span data-stu-id="8a073-148">You have hello option tooadjust your debugging experience tooyour scenario.</span></span> <span data-ttu-id="8a073-149">在此應用程式中，我們將資料儲存在使用可靠字典的後端服務中。</span><span class="sxs-lookup"><span data-stu-id="8a073-149">In this application, we store data in our back-end service, using a reliable dictionary.</span></span> <span data-ttu-id="8a073-150">Visual Studio 移除 hello 應用程式，根據預設，當您停止 hello 偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="8a073-150">Visual Studio removes hello application per default when you stop hello debugger.</span></span> <span data-ttu-id="8a073-151">移除 hello 應用程式造成 hello 資料在 hello 後端服務 tooalso 被移除。</span><span class="sxs-lookup"><span data-stu-id="8a073-151">Removing hello application causes hello data in hello back-end service tooalso be removed.</span></span> <span data-ttu-id="8a073-152">toopersist hello 偵錯工作階段之間的資料，您可以變更 hello**應用程式偵錯模式**為 hello 屬性**投票**Visual Studio 專案中的。</span><span class="sxs-lookup"><span data-stu-id="8a073-152">toopersist hello data between debugging sessions, you can change hello **Application Debug Mode** as a property on hello **Voting** project in Visual Studio.</span></span>

<span data-ttu-id="8a073-153">在發生的事 hello 程式碼中，完成下列步驟的 hello toolook:</span><span class="sxs-lookup"><span data-stu-id="8a073-153">toolook at what happens in hello code, complete hello following steps:</span></span>
1. <span data-ttu-id="8a073-154">開啟 hello **VotesController.cs**檔案，並設定中斷點，在 hello web API 的**放**方法 （列 47）-您可以搜尋 hello Visual Studio 中的 [方案總管] 中的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="8a073-154">Open hello **VotesController.cs** file and set a breakpoint in hello web API's **Put** method (line 47) - You can search for hello file in hello Solution Explorer in Visual Studio.</span></span>

2. <span data-ttu-id="8a073-155">開啟 hello **VoteDataController.cs**檔案，並設定中斷點，在這個 web API**放**方法 （行 50）。</span><span class="sxs-lookup"><span data-stu-id="8a073-155">Open hello **VoteDataController.cs** file and set a breakpoint in this web API's **Put** method (line 50).</span></span>

3. <span data-ttu-id="8a073-156">返回 toohello 瀏覽器後，請按一下投票選項或加入新的投票選項。</span><span class="sxs-lookup"><span data-stu-id="8a073-156">Go back toohello browser and click a voting option or add a new voting option.</span></span> <span data-ttu-id="8a073-157">您已達到 hello hello web 前端端的 api 控制器中的第一個中斷點。</span><span class="sxs-lookup"><span data-stu-id="8a073-157">You hit hello first breakpoint in hello web front-end's api controller.</span></span>
    - <span data-ttu-id="8a073-158">這是其中 hello 瀏覽器中的 hello JavaScript 要求 toohello web API 控制器會以傳送 hello 前端服務。</span><span class="sxs-lookup"><span data-stu-id="8a073-158">This is where hello JavaScript in hello browser sends a request toohello web API controller in hello front-end service.</span></span>
    
    ![新增投票前端服務](./media/service-fabric-quickstart-dotnet/addvote-frontend.png)

    - <span data-ttu-id="8a073-160">我們第一次針對我們的後端服務建構 hello URL toohello ReverseProxy **(1)**。</span><span class="sxs-lookup"><span data-stu-id="8a073-160">First we construct hello URL toohello ReverseProxy for our back-end service **(1)**.</span></span>
    - <span data-ttu-id="8a073-161">接著，我們將傳送嗨 HTTP PUT 要求 toohello ReverseProxy **(2)**。</span><span class="sxs-lookup"><span data-stu-id="8a073-161">Then we send hello HTTP PUT Request toohello ReverseProxy **(2)**.</span></span>
    - <span data-ttu-id="8a073-162">最後 hello 我們決定傳回 hello 回應 hello 後端服務 toohello 用戶端從**(3)**。</span><span class="sxs-lookup"><span data-stu-id="8a073-162">Finally hello we return hello response from hello back-end service toohello client **(3)**.</span></span>

4. <span data-ttu-id="8a073-163">按**F5** toocontinue</span><span class="sxs-lookup"><span data-stu-id="8a073-163">Press **F5** toocontinue</span></span>
    - <span data-ttu-id="8a073-164">現在您已位於 hello 中斷點 hello 後端服務。</span><span class="sxs-lookup"><span data-stu-id="8a073-164">You are now at hello break point in hello back-end service.</span></span>
    
    ![新增投票後端服務](./media/service-fabric-quickstart-dotnet/addvote-backend.png)

    - <span data-ttu-id="8a073-166">Hello hello 方法中的第一行**(1)**我們使用 hello `StateManager` tooget 或可靠的字典，稱為`counts`。</span><span class="sxs-lookup"><span data-stu-id="8a073-166">In hello first line in hello method **(1)** we are using hello `StateManager` tooget or add a reliable dictionary called `counts`.</span></span>
    - <span data-ttu-id="8a073-167">與可靠字典中的值進行的所有互動，都需要交易，這會使用陳述式 **(2)** 建立該交易。</span><span class="sxs-lookup"><span data-stu-id="8a073-167">All interactions with values in a reliable dictionary require a transaction, this using statement **(2)** creates that transaction.</span></span>
    - <span data-ttu-id="8a073-168">在 hello 交易中，我們再更新 hello hello hello 投票選項的相關索引鍵的值，而且認可 hello 作業**(3)**。</span><span class="sxs-lookup"><span data-stu-id="8a073-168">In hello transaction, we then update hello value of hello relevant key for hello voting option and commits hello operation **(3)**.</span></span> <span data-ttu-id="8a073-169">一旦認可 hello 方法傳回時，hello 資料更新 hello 字典中，然後複寫 tooother hello 叢集中的節點。</span><span class="sxs-lookup"><span data-stu-id="8a073-169">Once hello commit method returns, hello data is updated in hello dictionary and replicated tooother nodes in hello cluster.</span></span> <span data-ttu-id="8a073-170">hello 現在會安全地儲存資料 hello 叢集中，hello 後端服務可以容錯移轉 tooother 節點，仍有可用的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="8a073-170">hello data is now safely stored in hello cluster, and hello back-end service can fail over tooother nodes, still having hello data available.</span></span>
5. <span data-ttu-id="8a073-171">按**F5** toocontinue</span><span class="sxs-lookup"><span data-stu-id="8a073-171">Press **F5** toocontinue</span></span>

<span data-ttu-id="8a073-172">偵錯工作階段，請按 toostop hello **Shift + F5**。</span><span class="sxs-lookup"><span data-stu-id="8a073-172">toostop hello debugging session, press **Shift+F5**.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="8a073-173">部署 hello 應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="8a073-173">Deploy hello application tooAzure</span></span>
<span data-ttu-id="8a073-174">toodeploy hello 應用程式 tooa 叢集在 Azure 中的，您可以選擇 toocreate 您自己的叢集或使用合作對象叢集。</span><span class="sxs-lookup"><span data-stu-id="8a073-174">toodeploy hello application tooa cluster in Azure, you can either choose toocreate your own cluster, or use a Party Cluster.</span></span>

<span data-ttu-id="8a073-175">合作對象的叢集是免費的限時 Service Fabric 叢集裝載於 Azure，並執行 hello Service Fabric 小組的任何人都可以在此部署的應用程式，並了解 hello 平台。</span><span class="sxs-lookup"><span data-stu-id="8a073-175">Party clusters are free, limited-time Service Fabric clusters hosted on Azure and run by hello Service Fabric team where anyone can deploy applications and learn about hello platform.</span></span> <span data-ttu-id="8a073-176">tooget 存取 tooa 合作對象叢集[遵循 hello](http://aka.ms/tryservicefabric)。</span><span class="sxs-lookup"><span data-stu-id="8a073-176">tooget access tooa Party Cluster, [follow hello instructions](http://aka.ms/tryservicefabric).</span></span> 

<span data-ttu-id="8a073-177">如需建立您自己叢集的資訊，請參閱[在 Azure 上建立您的第一個 Service Fabric 叢集](service-fabric-get-started-azure-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="8a073-177">For information about creating your own cluster, see [Create your first Service Fabric cluster on Azure](service-fabric-get-started-azure-cluster.md).</span></span>

> [!Note]
> <span data-ttu-id="8a073-178">設定連入流量的連接埠 8080 上 toolisten hello web 前端服務。</span><span class="sxs-lookup"><span data-stu-id="8a073-178">hello web front-end service is configured toolisten on port 8080 for incoming traffic.</span></span> <span data-ttu-id="8a073-179">請確定您的叢集中已開啟該連接埠。</span><span class="sxs-lookup"><span data-stu-id="8a073-179">Make sure that port is open in your cluster.</span></span> <span data-ttu-id="8a073-180">如果您使用 hello 合作對象叢集，此連接埠已開啟。</span><span class="sxs-lookup"><span data-stu-id="8a073-180">If you are using hello Party Cluster, this port is open.</span></span>
>

### <a name="deploy-hello-application-using-visual-studio"></a><span data-ttu-id="8a073-181">部署使用 Visual Studio 的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="8a073-181">Deploy hello application using Visual Studio</span></span>
<span data-ttu-id="8a073-182">現在已準備好 hello 應用程式，您可以直接從 Visual Studio tooa 叢集對它進行部署。</span><span class="sxs-lookup"><span data-stu-id="8a073-182">Now that hello application is ready, you can deploy it tooa cluster directly from Visual Studio.</span></span>

1. <span data-ttu-id="8a073-183">以滑鼠右鍵按一下**投票**hello 中的 方案總管，然後選擇 **發行**。</span><span class="sxs-lookup"><span data-stu-id="8a073-183">Right-click **Voting** in hello Solution Explorer and choose **Publish**.</span></span> <span data-ttu-id="8a073-184">hello 發行對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="8a073-184">hello Publish dialog appears.</span></span>

    ![[發佈] 對話方塊](./media/service-fabric-quickstart-dotnet/publish-app.png)

2. <span data-ttu-id="8a073-186">Hello 連接端點中的型別，hello 中的 hello 叢集**連接端點**欄位，然後按一下**發行**。</span><span class="sxs-lookup"><span data-stu-id="8a073-186">Type in hello Connection Endpoint of hello cluster in hello **Connection Endpoint** field and click **Publish**.</span></span> <span data-ttu-id="8a073-187">註冊 hello 合作對象叢集，請 hello 連接端點就會提供在 hello 瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="8a073-187">When signing up for hello Party Cluster, hello Connection Endpoint is provided in hello browser.</span></span> <span data-ttu-id="8a073-188">例如 `winh1x87d1d.westus.cloudapp.azure.com:19000`。</span><span class="sxs-lookup"><span data-stu-id="8a073-188">- for example, `winh1x87d1d.westus.cloudapp.azure.com:19000`.</span></span>

3. <span data-ttu-id="8a073-189">比方說，在 hello 叢集位址-開啟瀏覽器並輸入`http://winh1x87d1d.westus.cloudapp.azure.com`。</span><span class="sxs-lookup"><span data-stu-id="8a073-189">Open a browser and type in hello cluster address - for example, `http://winh1x87d1d.westus.cloudapp.azure.com`.</span></span> <span data-ttu-id="8a073-190">您現在應該會看到 hello Azure 中的 hello 叢集中執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8a073-190">You should now see hello application running in hello cluster in Azure.</span></span>

![應用程式前端](./media/service-fabric-quickstart-dotnet/application-screenshot-new-azure.png)

## <a name="scale-applications-and-services-in-a-cluster"></a><span data-ttu-id="8a073-192">調整叢集中的應用程式和服務</span><span class="sxs-lookup"><span data-stu-id="8a073-192">Scale applications and services in a cluster</span></span>
<span data-ttu-id="8a073-193">Service Fabric 服務輕鬆地跨越叢集 tooaccommodate hello 負載 hello 服務上的變更。</span><span class="sxs-lookup"><span data-stu-id="8a073-193">Service Fabric services can easily be scaled across a cluster tooaccommodate for a change in hello load on hello services.</span></span> <span data-ttu-id="8a073-194">您可以調整服務藉由變更 hello hello 叢集中執行的執行個體的數目。</span><span class="sxs-lookup"><span data-stu-id="8a073-194">You scale a service by changing hello number of instances running in hello cluster.</span></span> <span data-ttu-id="8a073-195">您有多種方法來調整您的服務，您可以使用 PowerShell 或 Service Fabric CLI (sfctl) 中的指令碼或命令。</span><span class="sxs-lookup"><span data-stu-id="8a073-195">You have multiple ways of scaling your services, you can use scripts or commands from PowerShell or Service Fabric CLI (sfctl).</span></span> <span data-ttu-id="8a073-196">在此範例中，我們使用 Service Fabric Explorer。</span><span class="sxs-lookup"><span data-stu-id="8a073-196">In this example, we are using Service Fabric Explorer.</span></span>

<span data-ttu-id="8a073-197">Service Fabric 總管執行所有的 Service Fabric 叢集中，並可以從瀏覽器，瀏覽 toohello 叢集 HTTP 管理連接埠 (19080)，例如，存取`http://winh1x87d1d.westus.cloudapp.azure.com:19080`。</span><span class="sxs-lookup"><span data-stu-id="8a073-197">Service Fabric Explorer runs in all Service Fabric clusters and can be accessed from a browser, by browsing toohello clusters HTTP management port (19080), for example, `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span></span>

<span data-ttu-id="8a073-198">tooscale hello web 前端服務，請執行下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="8a073-198">tooscale hello web front-end service, do hello following steps:</span></span>

1. <span data-ttu-id="8a073-199">在您的叢集中開啟 Service Fabric Explorer，例如 `http://winh1x87d1d.westus.cloudapp.azure.com:19080`。</span><span class="sxs-lookup"><span data-stu-id="8a073-199">Open Service Fabric Explorer in your cluster - for example,`http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span></span>
2. <span data-ttu-id="8a073-200">按一下 下一步 toohello 的 hello 省略符號 （三個點）**網狀架構： 投票/VotingWeb**節點在 hello 樹狀檢視，然後選擇 **縮放服務**。</span><span class="sxs-lookup"><span data-stu-id="8a073-200">Click on hello ellipsis (three dots) next toohello **fabric:/Voting/VotingWeb** node in hello treeview and choose **Scale Service**.</span></span>

    ![Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/service-fabric-explorer-scale.png)

    <span data-ttu-id="8a073-202">您現在可以選擇 tooscale hello 數目 hello web 前端服務的執行個體。</span><span class="sxs-lookup"><span data-stu-id="8a073-202">You can now choose tooscale hello number of instances of hello web front-end service.</span></span>

3. <span data-ttu-id="8a073-203">變更 hello 編號太**2**按一下**縮放服務**。</span><span class="sxs-lookup"><span data-stu-id="8a073-203">Change hello number too**2** and click **Scale Service**.</span></span>
4. <span data-ttu-id="8a073-204">按一下 hello **fabric: / 投票/VotingWeb** hello 樹狀檢視中的節點，並展開 hello 資料分割的節點 （以 GUID 表示）。</span><span class="sxs-lookup"><span data-stu-id="8a073-204">Click on hello **fabric:/Voting/VotingWeb** node in hello tree-view and expand hello partition node (represented by a GUID).</span></span>

    ![Service Fabric Explorer 的 [調整服務]](./media/service-fabric-quickstart-dotnet/service-fabric-explorer-scaled-service.png)

    <span data-ttu-id="8a073-206">您現在可以看到 hello 服務有兩個執行個體，和 hello 樹狀檢視中，您查看 hello 執行個體執行的節點。</span><span class="sxs-lookup"><span data-stu-id="8a073-206">You can now see that hello service has two instances, and in hello tree view you see which nodes hello instances run on.</span></span>

<span data-ttu-id="8a073-207">這項簡單的管理工作，我們的一倍 hello 資源可以使用我們的前端服務 tooprocess 使用者負載。</span><span class="sxs-lookup"><span data-stu-id="8a073-207">By this simple management task, we doubled hello resources available for our front-end service tooprocess user load.</span></span> <span data-ttu-id="8a073-208">您不需要它能夠可靠地執行服務 toohave 的多個執行個體的重要 toounderstand 它。</span><span class="sxs-lookup"><span data-stu-id="8a073-208">It's important toounderstand that you do not need multiple instances of a service toohave it run reliably.</span></span> <span data-ttu-id="8a073-209">如果服務失敗時，Service Fabric 可確保新的服務執行個體執行於 hello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="8a073-209">If a service fails, Service Fabric makes sure a new service instance runs in hello cluster.</span></span>

## <a name="perform-a-rolling-application-upgrade"></a><span data-ttu-id="8a073-210">執行輪流應用程式升級</span><span class="sxs-lookup"><span data-stu-id="8a073-210">Perform a rolling application upgrade</span></span>
<span data-ttu-id="8a073-211">在部署新的更新 tooyour 應用程式時，Service Fabric 中推出 hello 更新安全的方式。</span><span class="sxs-lookup"><span data-stu-id="8a073-211">When deploying new updates tooyour application, Service Fabric rolls out hello update in a safe way.</span></span> <span data-ttu-id="8a073-212">輪流升級可讓您在不需要停機的情況下進行升級，並在發生錯誤時自動復原。</span><span class="sxs-lookup"><span data-stu-id="8a073-212">Rolling upgrades gives you no downtime while upgrading as well as automated rollback should errors occur.</span></span>

<span data-ttu-id="8a073-213">tooupgrade hello 應用程式中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="8a073-213">tooupgrade hello application, do hello following:</span></span>

1. <span data-ttu-id="8a073-214">開啟 hello **Index.cshtml**檔案在 Visual Studio-您可以搜尋 hello Visual Studio 中的 [方案總管] 中的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="8a073-214">Open hello **Index.cshtml** file in Visual Studio - You can search for hello file in hello Solution Explorer in Visual Studio.</span></span>
2. <span data-ttu-id="8a073-215">加入一些文字-例如，變更 hello hello 頁面上的標題。</span><span class="sxs-lookup"><span data-stu-id="8a073-215">Change hello heading on hello page by adding some text - for example.</span></span>
    ```html
        <div class="col-xs-8 col-xs-offset-2 text-center">
            <h2>Service Fabric Voting Sample v2</h2>
        </div>
    ```
3. <span data-ttu-id="8a073-216">儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="8a073-216">Save hello file.</span></span>
4. <span data-ttu-id="8a073-217">以滑鼠右鍵按一下**投票**hello 中的 方案總管，然後選擇 **發行**。</span><span class="sxs-lookup"><span data-stu-id="8a073-217">Right-click **Voting** in hello Solution Explorer and choose **Publish**.</span></span> <span data-ttu-id="8a073-218">hello 發行對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="8a073-218">hello Publish dialog appears.</span></span>
5. <span data-ttu-id="8a073-219">按一下 hello**資訊清單版本**按鈕 toochange hello hello 服務版本與應用程式。</span><span class="sxs-lookup"><span data-stu-id="8a073-219">Click hello **Manifest Version** button toochange hello version of hello service and application.</span></span>
6. <span data-ttu-id="8a073-220">變更 hello 版的 hello**程式碼**項目底下**VotingWebPkg**太"2.0.0"，範例中，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="8a073-220">Change hello version of hello **Code** element under **VotingWebPkg** too"2.0.0", for example, and click **Save**.</span></span>

    ![變更版本對話方塊](./media/service-fabric-quickstart-dotnet/change-version.png)
7. <span data-ttu-id="8a073-222">在 hello**發行 Service Fabric 應用程式**對話方塊中，核取 hello 升級 hello 應用程式核取方塊，然後按一下**發行**。</span><span class="sxs-lookup"><span data-stu-id="8a073-222">In hello **Publish Service Fabric Application** dialog, check hello Upgrade hello Application checkbox, and click **Publish**.</span></span>

    ![發行對話方塊的升級設定](./media/service-fabric-quickstart-dotnet/upgrade-app.png)
8. <span data-ttu-id="8a073-224">開啟您的瀏覽器並瀏覽 toohello 19080-連接埠上的叢集位址，例如`http://winh1x87d1d.westus.cloudapp.azure.com:19080`。</span><span class="sxs-lookup"><span data-stu-id="8a073-224">Open your browser and browse toohello cluster address on port 19080 - for example, `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span></span>
9. <span data-ttu-id="8a073-225">按一下 hello**應用程式**hello 樹狀檢視中的節點，然後**升級正在進行中的**hello 右側窗格中。</span><span class="sxs-lookup"><span data-stu-id="8a073-225">Click on hello **Applications** node in hello tree view, and then **Upgrades in Progress** in hello right-hand pane.</span></span> <span data-ttu-id="8a073-226">您會看到如何 hello 升級彙透過 hello 升級網域中您的叢集，並確定每個網域是下一步之前繼續 toohello 狀況良好。</span><span class="sxs-lookup"><span data-stu-id="8a073-226">You see how hello upgrade rolls through hello upgrade domains in your cluster, making sure each domain is healthy before proceeding toohello next.</span></span>
    <span data-ttu-id="8a073-227">![Service Fabric Explorer 中的升級檢視](./media/service-fabric-quickstart-dotnet/upgrading.png)</span><span class="sxs-lookup"><span data-stu-id="8a073-227">![Upgrade View in Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/upgrading.png)</span></span>

    <span data-ttu-id="8a073-228">Service Fabric 可確保升級安全藉由等待兩分鐘後升級 hello hello 叢集中的每個節點上的服務。</span><span class="sxs-lookup"><span data-stu-id="8a073-228">Service Fabric makes upgrades safe by waiting two minutes after upgrading hello service on each node in hello cluster.</span></span> <span data-ttu-id="8a073-229">預期 hello 整個更新 tootake 約 8 分鐘。</span><span class="sxs-lookup"><span data-stu-id="8a073-229">Expect hello entire update tootake approximately eight minutes.</span></span>

10. <span data-ttu-id="8a073-230">當執行 hello 升級時，您仍然可以使用 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8a073-230">While hello upgrade is running, you can still use hello application.</span></span> <span data-ttu-id="8a073-231">由於您擁有 hello 叢集中執行的 hello 服務的兩個執行個體，部分您要求可能會收到已升級的版本的 hello 應用程式，而其他人可能仍會收到 hello 舊版本。</span><span class="sxs-lookup"><span data-stu-id="8a073-231">Because you have two instances of hello service running in hello cluster, some of your requests may get an upgraded version of hello application, while others may still get hello old version.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a073-232">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8a073-232">Next steps</span></span>
<span data-ttu-id="8a073-233">在此快速入門中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="8a073-233">In this quickstart, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8a073-234">建立使用 .NET 和 Service Fabric 的應用程式</span><span class="sxs-lookup"><span data-stu-id="8a073-234">Create an application using .NET and Service Fabric</span></span>
> * <span data-ttu-id="8a073-235">使用 ASP.NET Core 作為 Web 前端</span><span class="sxs-lookup"><span data-stu-id="8a073-235">Use ASP.NET core as a web front-end</span></span>
> * <span data-ttu-id="8a073-236">將應用程式資料儲存在具狀態服務中</span><span class="sxs-lookup"><span data-stu-id="8a073-236">Store application data in a stateful service</span></span>
> * <span data-ttu-id="8a073-237">在本機偵錯您的應用程式</span><span class="sxs-lookup"><span data-stu-id="8a073-237">Debug your application locally</span></span>
> * <span data-ttu-id="8a073-238">部署在 Azure 中的 hello 應用程式 tooa 叢集</span><span class="sxs-lookup"><span data-stu-id="8a073-238">Deploy hello application tooa cluster in Azure</span></span>
> * <span data-ttu-id="8a073-239">在多個節點的向外延展 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="8a073-239">Scale-out hello application across multiple nodes</span></span>
> * <span data-ttu-id="8a073-240">執行輪流應用程式升級</span><span class="sxs-lookup"><span data-stu-id="8a073-240">Perform a rolling application upgrade</span></span>

<span data-ttu-id="8a073-241">深入了解服務的網狀架構和.NET toolearn 看一下本教學課程：</span><span class="sxs-lookup"><span data-stu-id="8a073-241">toolearn more about Service Fabric and .NET, take a look at this tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="8a073-242">Service Fabric 上的 .NET 應用程式</span><span class="sxs-lookup"><span data-stu-id="8a073-242">.NET application on Service Fabric</span></span>](service-fabric-tutorial-create-dotnet-app.md)