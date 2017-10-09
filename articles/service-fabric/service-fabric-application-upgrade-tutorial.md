---
title: "aaaService 網狀架構應用程式升級教學課程 |Microsoft 文件"
description: "本文逐步部署 Service Fabric 應用程式、 變更 hello 程式碼，以及使用 Visual Studio 推出升級 hello 體驗。"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a3181a7a-9ab1-4216-b07a-05b79bd826a4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: d069ff0b291018dbac846e65cddff1e9d73d156c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-tutorial-using-visual-studio"></a><span data-ttu-id="c86de-103">使用 Visual Studio 進行 Service Fabric 應用程式升級的教學課程</span><span class="sxs-lookup"><span data-stu-id="c86de-103">Service Fabric application upgrade tutorial using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c86de-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c86de-104">PowerShell</span></span>](service-fabric-application-upgrade-tutorial-powershell.md)
> * [<span data-ttu-id="c86de-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c86de-105">Visual Studio</span></span>](service-fabric-application-upgrade-tutorial.md)
> 
> 

<br/>

<span data-ttu-id="c86de-106">Azure Service Fabric 會簡化 hello 的雲端應用程式升級，升級後已變更的服務，同時應用程式健全狀況會監視整個 hello 升級程序的程序。</span><span class="sxs-lookup"><span data-stu-id="c86de-106">Azure Service Fabric simplifies hello process of upgrading cloud applications by ensuring that only changed services are upgraded, and that application health is monitored throughout hello upgrade process.</span></span> <span data-ttu-id="c86de-107">它也會自動回復在遇到問題時的 hello 應用程式 toohello 先前版本。</span><span class="sxs-lookup"><span data-stu-id="c86de-107">It also automatically rolls back hello application toohello previous version upon encountering issues.</span></span> <span data-ttu-id="c86de-108">Service Fabric 應用程式升級*零停機時間*，因為可以升級 hello 應用程式，而不需要停機時間。</span><span class="sxs-lookup"><span data-stu-id="c86de-108">Service Fabric application upgrades are *Zero Downtime*, since hello application can be upgraded with no downtime.</span></span> <span data-ttu-id="c86de-109">本教學課程涵蓋如何 toocomplete 從 Visual Studio 的輪流升級。</span><span class="sxs-lookup"><span data-stu-id="c86de-109">This tutorial covers how toocomplete a rolling upgrade from Visual Studio.</span></span>

## <a name="step-1-build-and-publish-hello-visual-objects-sample"></a><span data-ttu-id="c86de-110">步驟 1： 建立和發行 hello 視覺物件範例</span><span class="sxs-lookup"><span data-stu-id="c86de-110">Step 1: Build and publish hello Visual Objects sample</span></span>
<span data-ttu-id="c86de-111">首先，下載 hello[視覺物件](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Actors/VisualObjects)從 GitHub 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c86de-111">First, download hello [Visual Objects](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Actors/VisualObjects) application from GitHub.</span></span> <span data-ttu-id="c86de-112">然後，建置並發行 hello 應用程式，以滑鼠右鍵按一下 hello 應用程式專案， **VisualObjects**，然後選取 hello**發行**hello Service Fabric 功能表項目中的命令。</span><span class="sxs-lookup"><span data-stu-id="c86de-112">Then, build and publish hello application by right-clicking on hello application project, **VisualObjects**, and selecting hello **Publish** command in hello Service Fabric menu item.</span></span>

![Service Fabric 應用程式的操作功能表][image1]

<span data-ttu-id="c86de-114">選取**發行**會開啟快顯視窗，因此您可以設定 hello **profile 當做目標**太**PublishProfiles\Local.xml**。</span><span class="sxs-lookup"><span data-stu-id="c86de-114">Selecting **Publish** brings up a popup, and you can set hello **Target profile** too**PublishProfiles\Local.xml**.</span></span> <span data-ttu-id="c86de-115">hello 視窗看起來應該像 hello 之後，再按一下 **發行**。</span><span class="sxs-lookup"><span data-stu-id="c86de-115">hello window should look like hello following before you click **Publish**.</span></span>

![發佈 Service Fabric 應用程式][image2]

<span data-ttu-id="c86de-117">現在您可以按一下**發行**hello 對話方塊中。</span><span class="sxs-lookup"><span data-stu-id="c86de-117">Now you can click **Publish** in hello dialog box.</span></span> <span data-ttu-id="c86de-118">您可以使用[Service Fabric 總管 tooview hello 叢集和 hello 應用程式](service-fabric-visualizing-your-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="c86de-118">You can use [Service Fabric Explorer tooview hello cluster and hello application](service-fabric-visualizing-your-cluster.md).</span></span> <span data-ttu-id="c86de-119">hello 視覺物件的應用程式有 web 服務，您可以移 tooby 輸入[http://localhost:8081/visualobjects/](http://localhost:8081/visualobjects/) hello 瀏覽器的網址列中。</span><span class="sxs-lookup"><span data-stu-id="c86de-119">hello Visual Objects application has a web service that you can go tooby typing [http://localhost:8081/visualobjects/](http://localhost:8081/visualobjects/) in hello address bar of your browser.</span></span>  <span data-ttu-id="c86de-120">您應該會看到 hello 螢幕上移動的 10 個浮動的視覺物件。</span><span class="sxs-lookup"><span data-stu-id="c86de-120">You should see 10 floating visual objects moving around on hello screen.</span></span>

<span data-ttu-id="c86de-121">**注意：**如果太部署`Cloud.xml`設定檔 (Azure Service Fabric) hello 應用程式應該可以在**http://{ServiceFabricName}。 {Region}.cloudapp.azure.com:8081/visualobjects/**。</span><span class="sxs-lookup"><span data-stu-id="c86de-121">**NOTE:** If deploying too`Cloud.xml` profile (Azure Service Fabric), hello application should then be available at **http://{ServiceFabricName}.{Region}.cloudapp.azure.com:8081/visualobjects/**.</span></span> <span data-ttu-id="c86de-122">請確定您沒有`8081/TCP`中 hello 負載平衡器設定 (hello 負載平衡器中尋找在 hello 與 hello Service Fabric 執行個體相同的資源群組)。</span><span class="sxs-lookup"><span data-stu-id="c86de-122">Make sure you do have `8081/TCP` configured in hello Load Balancer (find hello Load Balancer in hello same resource group as hello Service Fabric instance).</span></span>

## <a name="step-2-update-hello-visual-objects-sample"></a><span data-ttu-id="c86de-123">步驟 2： 更新 hello 視覺物件範例</span><span class="sxs-lookup"><span data-stu-id="c86de-123">Step 2: Update hello Visual Objects sample</span></span>
<span data-ttu-id="c86de-124">您可能會注意到，在步驟 1 中已部署的 hello 版本，hello 視覺物件不旋轉。</span><span class="sxs-lookup"><span data-stu-id="c86de-124">You might notice that with hello version that was deployed in step 1, hello visual objects do not rotate.</span></span> <span data-ttu-id="c86de-125">讓我們來升級此應用程式 tooone，也旋轉 hello 視覺物件。</span><span class="sxs-lookup"><span data-stu-id="c86de-125">Let's upgrade this application tooone where hello visual objects also rotate.</span></span>

<span data-ttu-id="c86de-126">選取 hello VisualObjects 方案中的 hello VisualObjects.ActorService 專案並開啟 hello **VisualObjectActor.cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="c86de-126">Select hello VisualObjects.ActorService project within hello VisualObjects solution, and open hello **VisualObjectActor.cs** file.</span></span> <span data-ttu-id="c86de-127">在該檔案中，移 toohello 方法`MoveObject`，標記為註解`visualObject.Move(false)`，並取消註解`visualObject.Move(true)`。</span><span class="sxs-lookup"><span data-stu-id="c86de-127">Within that file, go toohello method `MoveObject`, comment out `visualObject.Move(false)`, and uncomment `visualObject.Move(true)`.</span></span> <span data-ttu-id="c86de-128">Hello 服務升級後，此程式碼變更旋轉 hello 物件。</span><span class="sxs-lookup"><span data-stu-id="c86de-128">This code change rotates hello objects after hello service is upgraded.</span></span>  <span data-ttu-id="c86de-129">**現在您可以建置 （不重建） hello 方案**，哪些組建 hello 修改專案。</span><span class="sxs-lookup"><span data-stu-id="c86de-129">**Now you can build (not rebuild) hello solution**, which builds hello modified projects.</span></span> <span data-ttu-id="c86de-130">如果您選取*全部重建*，針對所有 hello 專案有 tooupdate hello 版本。</span><span class="sxs-lookup"><span data-stu-id="c86de-130">If you select *Rebuild all*, you have tooupdate hello versions for all hello projects.</span></span>

<span data-ttu-id="c86de-131">我們也需要 tooversion 我們的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c86de-131">We also need tooversion our application.</span></span> <span data-ttu-id="c86de-132">toomake hello 版本變更之後您以滑鼠右鍵按一下 hello, **VisualObjects**專案中，您可以使用 Visual Studio hello**編輯資訊清單版本**選項。</span><span class="sxs-lookup"><span data-stu-id="c86de-132">toomake hello version changes after you right-click on hello **VisualObjects** project, you can use hello Visual Studio **Edit Manifest Versions** option.</span></span> <span data-ttu-id="c86de-133">選取此選項會顯示 hello 對話方塊 edition 版本，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c86de-133">Selecting this option brings up hello dialog box for edition versions as follows:</span></span>

![版本設定對話方塊][image3]

<span data-ttu-id="c86de-135">更新 hello 版本 hello 修改專案和其程式碼封裝，以及 hello 應用程式 tooversion 2.0.0。</span><span class="sxs-lookup"><span data-stu-id="c86de-135">Update hello versions for hello modified projects and their code packages, along with hello application tooversion 2.0.0.</span></span> <span data-ttu-id="c86de-136">Hello 變更之後，hello 資訊清單看起來應該像 hello 下列 （粗體部分會顯示 hello 變更）：</span><span class="sxs-lookup"><span data-stu-id="c86de-136">After hello changes are made, hello manifest should look like hello following (bold portions show hello changes):</span></span>

![更新版本][image4]

<span data-ttu-id="c86de-138">hello Visual Studio 工具可以執行自動彙總套件的版本時選取**自動更新應用程式和服務版本**。</span><span class="sxs-lookup"><span data-stu-id="c86de-138">hello Visual Studio tools can do automatic rollups of versions upon selecting **Automatically update application and service versions**.</span></span> <span data-ttu-id="c86de-139">如果您使用[SemVer](http://www.semver.org)、 需要 tooupdate hello 程式碼和/或設定封裝版本如果該選項已選取。</span><span class="sxs-lookup"><span data-stu-id="c86de-139">If you use [SemVer](http://www.semver.org), you need tooupdate hello code and/or configuration package version alone if that option is selected.</span></span>

<span data-ttu-id="c86de-140">儲存 hello 的變更，並立即檢查 hello**升級 hello 應用程式**方塊。</span><span class="sxs-lookup"><span data-stu-id="c86de-140">Save hello changes, and now check hello **Upgrade hello Application** box.</span></span>

## <a name="step-3--upgrade-your-application"></a><span data-ttu-id="c86de-141">步驟 3：升級應用程式</span><span class="sxs-lookup"><span data-stu-id="c86de-141">Step 3:  Upgrade your application</span></span>
<span data-ttu-id="c86de-142">熟悉 hello[應用程式升級參數](service-fabric-application-upgrade-parameters.md)和 hello[升級程序](service-fabric-application-upgrade.md)tooget hello 各種需要升級參數、 逾時、 和健全狀況條件，可以充分了解套用。</span><span class="sxs-lookup"><span data-stu-id="c86de-142">Familiarize yourself with hello [application upgrade parameters](service-fabric-application-upgrade-parameters.md) and hello [upgrade process](service-fabric-application-upgrade.md) tooget a good understanding of hello various upgrade parameters, time-outs, and health criterion that can be applied.</span></span> <span data-ttu-id="c86de-143">這個逐步解說中，針對 hello 服務健全狀況評估準則設定 toohello 預設 （無人監控的模式）。</span><span class="sxs-lookup"><span data-stu-id="c86de-143">For this walkthrough, hello service health evaluation criterion is set toohello default (unmonitored mode).</span></span> <span data-ttu-id="c86de-144">您可以設定這些設定，藉由選取**設定升級設定**然後修改視 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="c86de-144">You can configure these settings by selecting **Configure Upgrade Settings** and then modifying hello parameters as desired.</span></span>

<span data-ttu-id="c86de-145">現在我們已全部設定 toostart hello 應用程式升級選取**發行**。</span><span class="sxs-lookup"><span data-stu-id="c86de-145">Now we are all set toostart hello application upgrade by selecting **Publish**.</span></span> <span data-ttu-id="c86de-146">此選項升級您的應用程式 tooversion 2.0.0，hello 物件將旋轉。</span><span class="sxs-lookup"><span data-stu-id="c86de-146">This option upgrades your application tooversion 2.0.0, in which hello objects rotate.</span></span> <span data-ttu-id="c86de-147">Service Fabric 升級一個更新網域一次 （某些物件會更新第一次，後面接著其他人），而且 hello 服務 hello 升級期間仍然可以存取。</span><span class="sxs-lookup"><span data-stu-id="c86de-147">Service Fabric upgrades one update domain at a time (some objects are updated first, followed by others), and hello service remains accessible during hello upgrade.</span></span> <span data-ttu-id="c86de-148">存取 toohello 服務可透過您的用戶端 （瀏覽器） 來檢查。</span><span class="sxs-lookup"><span data-stu-id="c86de-148">Access toohello service can be checked through your client (browser).</span></span>  

<span data-ttu-id="c86de-149">現在，hello 應用程式會繼續進行升級，您可以監視它與服務網狀架構總管 中，使用 hello**升級正在進行中的** 索引標籤下 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c86de-149">Now, as hello application upgrade proceeds, you can monitor it with Service Fabric Explorer, by using hello **Upgrades in Progress** tab under hello applications.</span></span>

<span data-ttu-id="c86de-150">在幾分鐘內，所有更新網域應該都升級 （完成），而且 hello Visual Studio 輸出 視窗也應該清楚該 hello 升級完成。</span><span class="sxs-lookup"><span data-stu-id="c86de-150">In a few minutes, all update domains should be upgraded (completed), and hello Visual Studio output window should also state that hello upgrade is completed.</span></span> <span data-ttu-id="c86de-151">您應該會發現與*所有*現在輪替 hello 瀏覽器視窗中的視覺物件 ！</span><span class="sxs-lookup"><span data-stu-id="c86de-151">And you should find that *all* hello visual objects in your browser window are now rotating!</span></span>

<span data-ttu-id="c86de-152">您可能想 tootry 變更 hello 的版本中，並從 2.0.0 版 tooversion 3.0.0，當做練習移動，或甚至是從 2.0.0 版回 tooversion 1.0.0。</span><span class="sxs-lookup"><span data-stu-id="c86de-152">You may want tootry changing hello versions, and moving from version 2.0.0 tooversion 3.0.0 as an exercise, or even from version 2.0.0 back tooversion 1.0.0.</span></span> <span data-ttu-id="c86de-153">玩逾時和健全狀況原則 toomake 自己熟悉它們。</span><span class="sxs-lookup"><span data-stu-id="c86de-153">Play with time-outs and health policies toomake yourself familiar with them.</span></span> <span data-ttu-id="c86de-154">當部署的 tooan Azure 叢集做為相對於 tooa 本機叢集時，所使用的 hello 參數可能擁有 toodiffer。</span><span class="sxs-lookup"><span data-stu-id="c86de-154">When deploying tooan Azure cluster as opposed tooa local cluster, hello parameters used may have toodiffer.</span></span> <span data-ttu-id="c86de-155">我們建議您以穩當的方式設定 hello 逾時。</span><span class="sxs-lookup"><span data-stu-id="c86de-155">We recommend that you set hello time-outs conservatively.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c86de-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c86de-156">Next steps</span></span>
<span data-ttu-id="c86de-157">[使用 PowerShell 升級您的應用程式](service-fabric-application-upgrade-tutorial-powershell.md) 將引導您完成使用 PowerShell 進行應用程式升級的步驟。</span><span class="sxs-lookup"><span data-stu-id="c86de-157">[Upgrading your application using PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="c86de-158">使用 [升級參數](service-fabric-application-upgrade-parameters.md)來控制您應用程式的升級方式。</span><span class="sxs-lookup"><span data-stu-id="c86de-158">Control how your application is upgraded by using [upgrade parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="c86de-159">讓應用程式升級相容所學習如何 toouse[資料序列化](service-fabric-application-upgrade-data-serialization.md)。</span><span class="sxs-lookup"><span data-stu-id="c86de-159">Make your application upgrades compatible by learning how toouse [data serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="c86de-160">了解 toouse 把太升級您的應用程式時所進階的功能[進階主題](service-fabric-application-upgrade-advanced.md)。</span><span class="sxs-lookup"><span data-stu-id="c86de-160">Learn how toouse advanced functionality while upgrading your application by referring too[Advanced topics](service-fabric-application-upgrade-advanced.md).</span></span>

<span data-ttu-id="c86de-161">藉由參考 toohello 步驟中的修正應用程式升級的一般問題[疑難排解應用程式升級](service-fabric-application-upgrade-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="c86de-161">Fix common problems in application upgrades by referring toohello steps in [Troubleshooting application upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>

[image1]: media/service-fabric-application-upgrade-tutorial/upgrade7.png
[image2]: media/service-fabric-application-upgrade-tutorial/upgrade1.png
[image3]: media/service-fabric-application-upgrade-tutorial/upgrade5.png
[image4]: media/service-fabric-application-upgrade-tutorial/upgrade6.png
