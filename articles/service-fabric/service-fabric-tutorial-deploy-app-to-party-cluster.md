---
title: "aaaDeploy Azure Service Fabric 應用程式 tooa 合作對象叢集 |Microsoft 文件"
description: "深入了解如何 toodeploy 應用程式 tooa 合作對象叢集。"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: msfussell
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: mikhegn
ms.openlocfilehash: db16b6418fa2533ed915c8b6e612b7a8e7311bed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-party-cluster-in-azure"></a><span data-ttu-id="ee449-103">部署應用程式 tooa Azure 中的合作對象叢集</span><span class="sxs-lookup"><span data-stu-id="ee449-103">Deploy an application tooa Party Cluster in Azure</span></span>
<span data-ttu-id="ee449-104">本教學課程是兩個一系列的一部分，並為您示範如何在 Azure 中的合作對象叢集 Azure Service Fabric 應用程式 tooa toodeploy。</span><span class="sxs-lookup"><span data-stu-id="ee449-104">This tutorial is part two of a series and shows you how toodeploy an Azure Service Fabric application tooa Party Cluster in Azure.</span></span>

<span data-ttu-id="ee449-105">在 hello 教學課程系列的第二個部分，您將學習如何：</span><span class="sxs-lookup"><span data-stu-id="ee449-105">In part two of hello tutorial series, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="ee449-106">部署使用 Visual Studio 應用程式的 tooa 遠端叢集</span><span class="sxs-lookup"><span data-stu-id="ee449-106">Deploy an application tooa remote cluster using Visual Studio</span></span>
> * <span data-ttu-id="ee449-107">使用 Service Fabric Explorer 從叢集移除應用程式</span><span class="sxs-lookup"><span data-stu-id="ee449-107">Remove an application from a cluster using Service Fabric Explorer</span></span>

<span data-ttu-id="ee449-108">在本教學課程系列中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="ee449-108">In this tutorial series you learn how to:</span></span>
> [!div class="checklist"]
> * [<span data-ttu-id="ee449-109">建置 .NET Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="ee449-109">Build a .NET Service Fabric application</span></span>](service-fabric-tutorial-create-dotnet-app.md)
> * <span data-ttu-id="ee449-110">部署 hello 應用程式 tooa 遠端叢集</span><span class="sxs-lookup"><span data-stu-id="ee449-110">Deploy hello application tooa remote cluster</span></span>
> * [<span data-ttu-id="ee449-111">使用 Visual Studio Team Services 設定 CI/CD</span><span class="sxs-lookup"><span data-stu-id="ee449-111">Configure CI/CD using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a><span data-ttu-id="ee449-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="ee449-112">Prerequisites</span></span>
<span data-ttu-id="ee449-113">開始進行本教學課程之前：</span><span class="sxs-lookup"><span data-stu-id="ee449-113">Before you begin this tutorial:</span></span>
- <span data-ttu-id="ee449-114">如果您沒有 Azure 訂用帳戶，請建立[免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="ee449-114">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="ee449-115">[安裝 Visual Studio 2017](https://www.visualstudio.com/)並安裝 hello **Azure 開發**和**ASP.NET 及 web 開發**工作負載。</span><span class="sxs-lookup"><span data-stu-id="ee449-115">[Install Visual Studio 2017](https://www.visualstudio.com/) and install hello **Azure development** and **ASP.NET and web development** workloads.</span></span>
- [<span data-ttu-id="ee449-116">安裝 hello Service Fabric SDK</span><span class="sxs-lookup"><span data-stu-id="ee449-116">Install hello Service Fabric SDK</span></span>](service-fabric-get-started.md)

## <a name="download-hello-voting-sample-application"></a><span data-ttu-id="ee449-117">下載 hello 投票範例應用程式</span><span class="sxs-lookup"><span data-stu-id="ee449-117">Download hello Voting sample application</span></span>
<span data-ttu-id="ee449-118">如果您未建立 hello 投票範例應用程式[第一部此教學課程系列的](service-fabric-tutorial-create-dotnet-app.md)，您可以下載它。</span><span class="sxs-lookup"><span data-stu-id="ee449-118">If you did not build hello Voting sample application in [part one of this tutorial series](service-fabric-tutorial-create-dotnet-app.md), you can download it.</span></span> <span data-ttu-id="ee449-119">在命令視窗中，執行下列命令 tooclone hello 範例應用程式儲存機制 tooyour 本機電腦的 hello。</span><span class="sxs-lookup"><span data-stu-id="ee449-119">In a command window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="set-up-a-party-cluster"></a><span data-ttu-id="ee449-120">設定合作對象叢集</span><span class="sxs-lookup"><span data-stu-id="ee449-120">Set up a Party Cluster</span></span>
<span data-ttu-id="ee449-121">合作對象的叢集是免費的限時 Service Fabric 叢集裝載於 Azure，並執行 hello Service Fabric 小組的任何人都可以在此部署的應用程式，並了解 hello 平台。</span><span class="sxs-lookup"><span data-stu-id="ee449-121">Party clusters are free, limited-time Service Fabric clusters hosted on Azure and run by hello Service Fabric team where anyone can deploy applications and learn about hello platform.</span></span> <span data-ttu-id="ee449-122">免費！</span><span class="sxs-lookup"><span data-stu-id="ee449-122">For free!</span></span>

<span data-ttu-id="ee449-123">tooget 存取 tooa 合作對象叢集中，瀏覽 toothis 網站： http://aka.ms/tryservicefabric 然後遵循 hello 指示 tooget 存取 tooa 叢集。</span><span class="sxs-lookup"><span data-stu-id="ee449-123">tooget access tooa Party Cluster, browse toothis site: http://aka.ms/tryservicefabric and follow hello instructions tooget access tooa cluster.</span></span> <span data-ttu-id="ee449-124">您需要 Facebook 或 GitHub 帳戶 tooget 存取 tooa 合作對象叢集。</span><span class="sxs-lookup"><span data-stu-id="ee449-124">You need a Facebook or GitHub account tooget access tooa Party Cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="ee449-125">合作對象叢集也不安全，因此應用程式，且您將放在它們的任何資料可能會看見 tooothers。</span><span class="sxs-lookup"><span data-stu-id="ee449-125">Party clusters are not secured, so your applications and any data you put in them may be visible tooothers.</span></span> <span data-ttu-id="ee449-126">不會部署任何您不希望其他人 toosee。</span><span class="sxs-lookup"><span data-stu-id="ee449-126">Don't deploy anything you don't want others toosee.</span></span> <span data-ttu-id="ee449-127">確定 tooread 透過我們的使用規定的所有 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ee449-127">Be sure tooread over our Terms of Use for all hello details.</span></span>

## <a name="configure-hello-listening-port"></a><span data-ttu-id="ee449-128">設定 hello 接聽連接埠</span><span class="sxs-lookup"><span data-stu-id="ee449-128">Configure hello listening port</span></span>
<span data-ttu-id="ee449-129">建立 hello VotingWeb 前端服務時，Visual Studio 會隨機選擇 hello 服務 toolisten 的連接埠上。</span><span class="sxs-lookup"><span data-stu-id="ee449-129">When hello VotingWeb front-end service is created, Visual Studio randomly selects a port for hello service toolisten on.</span></span>  <span data-ttu-id="ee449-130">hello VotingWeb 服務做為此應用程式前端的 hello 和接受外部流量，因此讓我們先繫結修正該服務 tooa 並也知道連接埠。</span><span class="sxs-lookup"><span data-stu-id="ee449-130">hello VotingWeb service acts as hello front-end for this application and accepts external traffic, so let's bind that service tooa fixed and well-know port.</span></span> <span data-ttu-id="ee449-131">在 [方案總管] 中，開啟 VotingWeb/PackageRoot/ServiceManifest.xml。</span><span class="sxs-lookup"><span data-stu-id="ee449-131">In Solution Explorer, open  *VotingWeb/PackageRoot/ServiceManifest.xml*.</span></span>  <span data-ttu-id="ee449-132">尋找 hello**端點**hello 中的資源**資源**區段，並變更 hello**連接埠**值 too80。</span><span class="sxs-lookup"><span data-stu-id="ee449-132">Find hello **Endpoint** resource in hello **Resources** section and change hello **Port** value too80.</span></span>

```xml
<Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" Port="80" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="ee449-133">讓網頁瀏覽器開啟 toohello 正確的連接埠，當您偵錯使用 'F5' 時，也更新 hello 投票專案中的 hello 應用程式 URL 屬性值。</span><span class="sxs-lookup"><span data-stu-id="ee449-133">Also update hello Application URL property value in hello Voting project so a web browser opens toohello correct port when you debug using 'F5'.</span></span>  <span data-ttu-id="ee449-134">在 方案總管 中，選取 hello**投票**專案和更新的 hello**應用程式 URL**屬性。</span><span class="sxs-lookup"><span data-stu-id="ee449-134">In Solution Explorer, select hello **Voting** project and update hello **Application URL** property.</span></span>

![應用程式 URL](./media/service-fabric-tutorial-deploy-app-to-party-cluster/application-url.png)

## <a name="deploy-hello-app-toohello-azure"></a><span data-ttu-id="ee449-136">部署 hello 應用程式 toohello Azure</span><span class="sxs-lookup"><span data-stu-id="ee449-136">Deploy hello app toohello Azure</span></span>
<span data-ttu-id="ee449-137">現在已準備好 hello 應用程式，您可以部署它 toohello 直接從 Visual Studio 的合作對象叢集。</span><span class="sxs-lookup"><span data-stu-id="ee449-137">Now that hello application is ready, you can deploy it toohello Party Cluster direct from Visual Studio.</span></span>

1. <span data-ttu-id="ee449-138">以滑鼠右鍵按一下**投票**hello 中的 方案總管，然後選擇 **發行**。</span><span class="sxs-lookup"><span data-stu-id="ee449-138">Right-click **Voting** in hello Solution Explorer and choose **Publish**.</span></span>

    ![[發佈] 對話方塊](./media/service-fabric-tutorial-deploy-app-to-party-cluster/publish-app.png)

2. <span data-ttu-id="ee449-140">輸入 hello 連接端點之 hello 合作對象叢集在 hello**連接端點**欄位，然後按一下**發行**。</span><span class="sxs-lookup"><span data-stu-id="ee449-140">Type in hello Connection Endpoint of hello Party Cluster in hello **Connection Endpoint** field and click **Publish**.</span></span>

    <span data-ttu-id="ee449-141">一旦 hello 發佈已完成之後，您應該要能夠 toosend 透過瀏覽器要求 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ee449-141">Once hello publish has finished, you should be able toosend a request toohello application via a browser.</span></span>

3. <span data-ttu-id="ee449-142">開啟您偏好的瀏覽器然後輸入 hello 叢集位址 （不含 hello 連接埠資訊，例如 win1kw5649s.westus.cloudapp.azure.com hello 連接端點）。</span><span class="sxs-lookup"><span data-stu-id="ee449-142">Open you preferred browser and type in hello cluster address (hello connection endpoint without hello port information - for example, win1kw5649s.westus.cloudapp.azure.com).</span></span>

    <span data-ttu-id="ee449-143">您現在應該會看到結果如同在本機執行 hello 應用程式時相同的 hello。</span><span class="sxs-lookup"><span data-stu-id="ee449-143">You should now see hello same result as you saw when running hello application locally.</span></span>

    ![叢集的 API 回應](./media/service-fabric-tutorial-deploy-app-to-party-cluster/response-from-cluster.png)

## <a name="remove-hello-application-from-a-cluster-using-service-fabric-explorer"></a><span data-ttu-id="ee449-145">使用 Service Fabric 總管叢集中移除 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="ee449-145">Remove hello application from a cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="ee449-146">Service Fabric 總管是圖形化使用者介面 tooexplore 和管理 Service Fabric 叢集中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ee449-146">Service Fabric Explorer is a graphical user interface tooexplore and manage applications in a Service Fabric cluster.</span></span>

<span data-ttu-id="ee449-147">從合作對象叢集 hello tooremove hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="ee449-147">tooremove hello application from hello Party Cluster:</span></span>

1. <span data-ttu-id="ee449-148">瀏覽 toohello Service Fabric 總管 中，使用 hello hello 合作對象叢集註冊頁面所提供的連結。</span><span class="sxs-lookup"><span data-stu-id="ee449-148">Browse toohello Service Fabric Explorer, using hello link provided by hello Party Cluster sign-up page.</span></span> <span data-ttu-id="ee449-149">例如，http://win1kw5649s.westus.cloudapp.azure.com:19080/Explorer/index.html。</span><span class="sxs-lookup"><span data-stu-id="ee449-149">For example, http://win1kw5649s.westus.cloudapp.azure.com:19080/Explorer/index.html.</span></span>

2. <span data-ttu-id="ee449-150">在 Service Fabric 總管，瀏覽 toohello **fabric://Voting** hello 上 hello 左側的樹狀檢視中的節點。</span><span class="sxs-lookup"><span data-stu-id="ee449-150">In Service Fabric Explorer, navigate toohello **fabric://Voting** node in hello treeview on hello left-hand side.</span></span>

3. <span data-ttu-id="ee449-151">按一下 hello**動作**按鈕在右手邊的 hello **Essentials** ] 窗格中，選擇 [**刪除應用程式**。</span><span class="sxs-lookup"><span data-stu-id="ee449-151">Click hello **Action** button in hello right-hand **Essentials** pane, and choose **Delete Application**.</span></span> <span data-ttu-id="ee449-152">確認刪除 hello 應用程式執行個體，代表要移除 hello 我們 hello 叢集中執行的應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="ee449-152">Confirm deleting hello application instance, which removes hello instance of our application running in hello cluster.</span></span>

![刪除 Service Fabric Explorer 中的應用程式](./media/service-fabric-tutorial-deploy-app-to-party-cluster/delete-application.png)

## <a name="remove-hello-application-type-from-a-cluster-using-service-fabric-explorer"></a><span data-ttu-id="ee449-154">使用 Service Fabric 總管叢集中移除 hello 應用程式類型</span><span class="sxs-lookup"><span data-stu-id="ee449-154">Remove hello application type from a cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="ee449-155">應用程式會部署為在多個執行個體和 hello hello 叢集內執行的應用程式的版本，可讓您 toohave Service Fabric 叢集中的應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="ee449-155">Applications are deployed as application types in a Service Fabric cluster, which enables you toohave multiple instances and versions of hello application running within hello cluster.</span></span> <span data-ttu-id="ee449-156">之後移除 hello 執行我們的應用程式的執行個體之後，我們也可以移除 hello toocomplete hello 清除 hello 部署的型別。</span><span class="sxs-lookup"><span data-stu-id="ee449-156">After having removed hello running instance of our application, we can also remove hello type, toocomplete hello cleanup of hello deployment.</span></span>

<span data-ttu-id="ee449-157">如需服務網狀架構中的 hello 應用程式模型的詳細資訊，請參閱[模型的應用程式在 Service Fabric](service-fabric-application-model.md)。</span><span class="sxs-lookup"><span data-stu-id="ee449-157">For more information about hello application model in Service Fabric, see [Model an application in Service Fabric](service-fabric-application-model.md).</span></span>

1. <span data-ttu-id="ee449-158">瀏覽 toohello **VotingType** hello 樹狀檢視中的節點。</span><span class="sxs-lookup"><span data-stu-id="ee449-158">Navigate toohello **VotingType** node in hello treeview.</span></span>

2. <span data-ttu-id="ee449-159">按一下 hello**動作**按鈕在右手邊的 hello **Essentials** ] 窗格中，選擇 [**解除佈建類型**。</span><span class="sxs-lookup"><span data-stu-id="ee449-159">Click hello **Action** button in hello right-hand **Essentials** pane, and choose **Unprovision Type**.</span></span> <span data-ttu-id="ee449-160">確認解除佈建 hello 應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="ee449-160">Confirm unprovisioning hello application type.</span></span>

![在 Service Fabric Explorer 中解除佈建應用程式類型](./media/service-fabric-tutorial-deploy-app-to-party-cluster/unprovision-type.png)

<span data-ttu-id="ee449-162">以上總結 hello 教學課程。</span><span class="sxs-lookup"><span data-stu-id="ee449-162">This concludes hello tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee449-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ee449-163">Next steps</span></span>
<span data-ttu-id="ee449-164">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="ee449-164">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ee449-165">部署使用 Visual Studio 應用程式的 tooa 遠端叢集</span><span class="sxs-lookup"><span data-stu-id="ee449-165">Deploy an application tooa remote cluster using Visual Studio</span></span>
> * <span data-ttu-id="ee449-166">使用 Service Fabric Explorer 從叢集移除應用程式</span><span class="sxs-lookup"><span data-stu-id="ee449-166">Remove an application from a cluster using Service Fabric Explorer</span></span>

<span data-ttu-id="ee449-167">進階 toohello 下一個教學課程：</span><span class="sxs-lookup"><span data-stu-id="ee449-167">Advance toohello next tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="ee449-168">使用 Visual Studio Team Services 設定持續整合</span><span class="sxs-lookup"><span data-stu-id="ee449-168">Set up continuous integration using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)