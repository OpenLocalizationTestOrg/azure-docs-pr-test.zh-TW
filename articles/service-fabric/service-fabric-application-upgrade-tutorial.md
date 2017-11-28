---
title: "Service Fabric 應用程式升級教學課程 | Microsoft Docs"
description: "本文章會逐步解說使用 Visual Studio 部署 Service Fabric 應用程式、變更程式碼及執行升級的體驗。"
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
ms.openlocfilehash: 940440688ec770a4aeb932b574bd6be173f494d4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="service-fabric-application-upgrade-tutorial-using-visual-studio"></a><span data-ttu-id="597ec-103">使用 Visual Studio 進行 Service Fabric 應用程式升級的教學課程</span><span class="sxs-lookup"><span data-stu-id="597ec-103">Service Fabric application upgrade tutorial using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="597ec-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="597ec-104">PowerShell</span></span>](service-fabric-application-upgrade-tutorial-powershell.md)
> * [<span data-ttu-id="597ec-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="597ec-105">Visual Studio</span></span>](service-fabric-application-upgrade-tutorial.md)
> 
> 

<br/>

<span data-ttu-id="597ec-106">Azure Service Fabric 藉由確保只升級已變更的服務，並且在整個升級程序中監視應用程式健康狀態，簡化雲端應用程式的升級程序。</span><span class="sxs-lookup"><span data-stu-id="597ec-106">Azure Service Fabric simplifies the process of upgrading cloud applications by ensuring that only changed services are upgraded, and that application health is monitored throughout the upgrade process.</span></span> <span data-ttu-id="597ec-107">它也會在應用程式發生問題時自動回復到舊版。</span><span class="sxs-lookup"><span data-stu-id="597ec-107">It also automatically rolls back the application to the previous version upon encountering issues.</span></span> <span data-ttu-id="597ec-108">Service Fabric 應用程式升級並「不需要停機」 ，因為可以在不停機的情況下升級應用程式。</span><span class="sxs-lookup"><span data-stu-id="597ec-108">Service Fabric application upgrades are *Zero Downtime*, since the application can be upgraded with no downtime.</span></span> <span data-ttu-id="597ec-109">本教學課程涵蓋如何從 Visual Studio 完成輪流升級。</span><span class="sxs-lookup"><span data-stu-id="597ec-109">This tutorial covers how to complete a rolling upgrade from Visual Studio.</span></span>

## <a name="step-1-build-and-publish-the-visual-objects-sample"></a><span data-ttu-id="597ec-110">步驟 1：建置和發佈視覺物件範例</span><span class="sxs-lookup"><span data-stu-id="597ec-110">Step 1: Build and publish the Visual Objects sample</span></span>
<span data-ttu-id="597ec-111">首先從 GitHub 下載 [Visual Objects](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Actors/VisualObjects) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="597ec-111">First, download the [Visual Objects](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Actors/VisualObjects) application from GitHub.</span></span> <span data-ttu-id="597ec-112">然後在應用程式專案 **VisualObjects** 上按一下滑鼠右鍵，選取 Service Fabric 功能表項目中的 [發佈] 命令來建置和發佈應用程式。</span><span class="sxs-lookup"><span data-stu-id="597ec-112">Then, build and publish the application by right-clicking on the application project, **VisualObjects**, and selecting the **Publish** command in the Service Fabric menu item.</span></span>

![Service Fabric 應用程式的操作功能表][image1]

<span data-ttu-id="597ec-114">選取 [發佈] 會顯示另一個快顯視窗，您可以將 [目標設定檔] 設定成 [PublishProfiles\Local.xml]。</span><span class="sxs-lookup"><span data-stu-id="597ec-114">Selecting **Publish** brings up a popup, and you can set the **Target profile** to **PublishProfiles\Local.xml**.</span></span> <span data-ttu-id="597ec-115">在您按一下 [發佈] 之前，視窗應該看起來如下。</span><span class="sxs-lookup"><span data-stu-id="597ec-115">The window should look like the following before you click **Publish**.</span></span>

![發佈 Service Fabric 應用程式][image2]

<span data-ttu-id="597ec-117">現在，您可以按一下對話方塊中的 [發佈]  。</span><span class="sxs-lookup"><span data-stu-id="597ec-117">Now you can click **Publish** in the dialog box.</span></span> <span data-ttu-id="597ec-118">您可以使用 [Service Fabric 總管來檢視叢集與應用程式](service-fabric-visualizing-your-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="597ec-118">You can use [Service Fabric Explorer to view the cluster and the application](service-fabric-visualizing-your-cluster.md).</span></span> <span data-ttu-id="597ec-119">Visual Objects 應用程式有一個 Web 服務，您可在瀏覽器的網址列中輸入 [http://localhost:8081/visualobjects/](http://localhost:8081/visualobjects/)，以移至該服務。</span><span class="sxs-lookup"><span data-stu-id="597ec-119">The Visual Objects application has a web service that you can go to by typing [http://localhost:8081/visualobjects/](http://localhost:8081/visualobjects/) in the address bar of your browser.</span></span>  <span data-ttu-id="597ec-120">您應該會看到 10 個浮動的視覺物件在畫面中四處移動。</span><span class="sxs-lookup"><span data-stu-id="597ec-120">You should see 10 floating visual objects moving around on the screen.</span></span>

<span data-ttu-id="597ec-121">**注意︰**如果部署至 `Cloud.xml` 設定檔 (Azure Service Fabric)，則應該可在 **http://{ServiceFabricName}.{Region}.cloudapp.azure.com:8081/visualobjects/** 上取得應用程式。</span><span class="sxs-lookup"><span data-stu-id="597ec-121">**NOTE:** If deploying to `Cloud.xml` profile (Azure Service Fabric), the application should then be available at **http://{ServiceFabricName}.{Region}.cloudapp.azure.com:8081/visualobjects/**.</span></span> <span data-ttu-id="597ec-122">請確定您確實已在負載平衡器 (在與 Service Fabric 執行個體相同的資源群組中尋找負載平衡器) 中設定 `8081/TCP`。</span><span class="sxs-lookup"><span data-stu-id="597ec-122">Make sure you do have `8081/TCP` configured in the Load Balancer (find the Load Balancer in the same resource group as the Service Fabric instance).</span></span>

## <a name="step-2-update-the-visual-objects-sample"></a><span data-ttu-id="597ec-123">步驟 2：更新視覺物件範例</span><span class="sxs-lookup"><span data-stu-id="597ec-123">Step 2: Update the Visual Objects sample</span></span>
<span data-ttu-id="597ec-124">您可能會注意到使用步驟 1 中部署的版本，視覺物件不會旋轉。</span><span class="sxs-lookup"><span data-stu-id="597ec-124">You might notice that with the version that was deployed in step 1, the visual objects do not rotate.</span></span> <span data-ttu-id="597ec-125">讓我們將這個應用程式升級到其中的視覺物件也會旋轉的版本。</span><span class="sxs-lookup"><span data-stu-id="597ec-125">Let's upgrade this application to one where the visual objects also rotate.</span></span>

<span data-ttu-id="597ec-126">選取 VisualObjects 方案內的 VisualObjects.ActorService 專案，然後開啟 **VisualObjectActor.cs** 檔案。</span><span class="sxs-lookup"><span data-stu-id="597ec-126">Select the VisualObjects.ActorService project within the VisualObjects solution, and open the **VisualObjectActor.cs** file.</span></span> <span data-ttu-id="597ec-127">在該檔案內，移至 `MoveObject` 方法，將 `visualObject.Move(false)` 標記為註解，並將 `visualObject.Move(true)` 取消註解。</span><span class="sxs-lookup"><span data-stu-id="597ec-127">Within that file, go to the method `MoveObject`, comment out `visualObject.Move(false)`, and uncomment `visualObject.Move(true)`.</span></span> <span data-ttu-id="597ec-128">這項程式碼變更會在服務升級後旋轉物件。</span><span class="sxs-lookup"><span data-stu-id="597ec-128">This code change rotates the objects after the service is upgraded.</span></span>  <span data-ttu-id="597ec-129">**現在您可以建置 (而非重建) 方案**，這會建置修改過的專案。</span><span class="sxs-lookup"><span data-stu-id="597ec-129">**Now you can build (not rebuild) the solution**, which builds the modified projects.</span></span> <span data-ttu-id="597ec-130">如果您選取 [全部重建] ，則必須更新所有專案的版本。</span><span class="sxs-lookup"><span data-stu-id="597ec-130">If you select *Rebuild all*, you have to update the versions for all the projects.</span></span>

<span data-ttu-id="597ec-131">我們也需要設定應用程式的版本。</span><span class="sxs-lookup"><span data-stu-id="597ec-131">We also need to version our application.</span></span> <span data-ttu-id="597ec-132">若要進行版本變更，請在 [VisualObjects] 專案上按一下滑鼠右鍵，使用 Visual Studio 的 [編輯資訊清單版本] 選項。</span><span class="sxs-lookup"><span data-stu-id="597ec-132">To make the version changes after you right-click on the **VisualObjects** project, you can use the Visual Studio **Edit Manifest Versions** option.</span></span> <span data-ttu-id="597ec-133">選取此選項會帶出對話方塊供您編輯版本，如以下所示：</span><span class="sxs-lookup"><span data-stu-id="597ec-133">Selecting this option brings up the dialog box for edition versions as follows:</span></span>

![版本設定對話方塊][image3]

<span data-ttu-id="597ec-135">將已修改之專案及其程式碼封裝連同應用程式的版本一起更新成 2.0.0 版。</span><span class="sxs-lookup"><span data-stu-id="597ec-135">Update the versions for the modified projects and their code packages, along with the application to version 2.0.0.</span></span> <span data-ttu-id="597ec-136">進行變更之後，資訊清單應該會看起來如下 (粗體部分即為所做的變更)：</span><span class="sxs-lookup"><span data-stu-id="597ec-136">After the changes are made, the manifest should look like the following (bold portions show the changes):</span></span>

![更新版本][image4]

<span data-ttu-id="597ec-138">選取 [自動更新應用程式與服務版本] 之後，Visual Studio 工具便可自動彙總版本。</span><span class="sxs-lookup"><span data-stu-id="597ec-138">The Visual Studio tools can do automatic rollups of versions upon selecting **Automatically update application and service versions**.</span></span> <span data-ttu-id="597ec-139">如果您使用 [SemVer](http://www.semver.org)，當您選取以上選項時，則必須單獨更新程式碼和 (或) 組態封裝版本。</span><span class="sxs-lookup"><span data-stu-id="597ec-139">If you use [SemVer](http://www.semver.org), you need to update the code and/or configuration package version alone if that option is selected.</span></span>

<span data-ttu-id="597ec-140">儲存變更，然後立即核取 [升級應用程式]  方塊。</span><span class="sxs-lookup"><span data-stu-id="597ec-140">Save the changes, and now check the **Upgrade the Application** box.</span></span>

## <a name="step-3--upgrade-your-application"></a><span data-ttu-id="597ec-141">步驟 3：升級應用程式</span><span class="sxs-lookup"><span data-stu-id="597ec-141">Step 3:  Upgrade your application</span></span>
<span data-ttu-id="597ec-142">請您熟悉[應用程式升級參數](service-fabric-application-upgrade-parameters.md)和[升級程序](service-fabric-application-upgrade.md)，以了解可以套用的各種升級參數、逾時和健康狀態準則。</span><span class="sxs-lookup"><span data-stu-id="597ec-142">Familiarize yourself with the [application upgrade parameters](service-fabric-application-upgrade-parameters.md) and the [upgrade process](service-fabric-application-upgrade.md) to get a good understanding of the various upgrade parameters, time-outs, and health criterion that can be applied.</span></span> <span data-ttu-id="597ec-143">針對此逐步解說，服務健康狀態評估準則會設定為預設值 (未受監視的模式)。</span><span class="sxs-lookup"><span data-stu-id="597ec-143">For this walkthrough, the service health evaluation criterion is set to the default (unmonitored mode).</span></span> <span data-ttu-id="597ec-144">您可以選取 [設定升級設定]  ，然後視需要修改參數，來設定這些設定。</span><span class="sxs-lookup"><span data-stu-id="597ec-144">You can configure these settings by selecting **Configure Upgrade Settings** and then modifying the parameters as desired.</span></span>

<span data-ttu-id="597ec-145">現在，我們已經準備好選取 [發佈] 來啟動應用程式升級。</span><span class="sxs-lookup"><span data-stu-id="597ec-145">Now we are all set to start the application upgrade by selecting **Publish**.</span></span> <span data-ttu-id="597ec-146">此選項會將您的應用程式升級到其中物件會旋轉的版本 2.0.0。</span><span class="sxs-lookup"><span data-stu-id="597ec-146">This option upgrades your application to version 2.0.0, in which the objects rotate.</span></span> <span data-ttu-id="597ec-147">Service Fabric 會一次升級一個更新網域 (某些物件會先更新，其他物件再接著更新)，在升級期間仍可存取服務。</span><span class="sxs-lookup"><span data-stu-id="597ec-147">Service Fabric upgrades one update domain at a time (some objects are updated first, followed by others), and the service remains accessible during the upgrade.</span></span> <span data-ttu-id="597ec-148">透過您的用戶端 (瀏覽器) 可檢查服務的存取權。</span><span class="sxs-lookup"><span data-stu-id="597ec-148">Access to the service can be checked through your client (browser).</span></span>  

<span data-ttu-id="597ec-149">現在，隨著應用程式繼續進行升級，您可以利用 Service Fabric Explorer (使用應用程式底下的 [Upgrades in Progress (正在進行升級)]  索引標籤) 來監視應用程式。</span><span class="sxs-lookup"><span data-stu-id="597ec-149">Now, as the application upgrade proceeds, you can monitor it with Service Fabric Explorer, by using the **Upgrades in Progress** tab under the applications.</span></span>

<span data-ttu-id="597ec-150">幾分鐘後，應該就已升級 (完成) 所有更新網域，而 Visual Studio 的輸出視窗應該也會指出升級已完成。</span><span class="sxs-lookup"><span data-stu-id="597ec-150">In a few minutes, all update domains should be upgraded (completed), and the Visual Studio output window should also state that the upgrade is completed.</span></span> <span data-ttu-id="597ec-151">而且，您應該會發現瀏覽器視窗中的「所有」  視覺物件現在都在旋轉！</span><span class="sxs-lookup"><span data-stu-id="597ec-151">And you should find that *all* the visual objects in your browser window are now rotating!</span></span>

<span data-ttu-id="597ec-152">您可能會想要嘗試變更版本，從版本 2.0.0 移到版本 3.0.0 來做為練習，或甚至是從版本 2.0.0 變回版本 1.0.0。</span><span class="sxs-lookup"><span data-stu-id="597ec-152">You may want to try changing the versions, and moving from version 2.0.0 to version 3.0.0 as an exercise, or even from version 2.0.0 back to version 1.0.0.</span></span> <span data-ttu-id="597ec-153">練習逾時和健康狀態原則，讓自己更熟練。</span><span class="sxs-lookup"><span data-stu-id="597ec-153">Play with time-outs and health policies to make yourself familiar with them.</span></span> <span data-ttu-id="597ec-154">在部署至 Azure 叢集而不是本機叢集時，所使用的參數可能不同。</span><span class="sxs-lookup"><span data-stu-id="597ec-154">When deploying to an Azure cluster as opposed to a local cluster, the parameters used may have to differ.</span></span> <span data-ttu-id="597ec-155">我們建議您保守地設定逾時。</span><span class="sxs-lookup"><span data-stu-id="597ec-155">We recommend that you set the time-outs conservatively.</span></span>

## <a name="next-steps"></a><span data-ttu-id="597ec-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="597ec-156">Next steps</span></span>
<span data-ttu-id="597ec-157">[使用 PowerShell 升級您的應用程式](service-fabric-application-upgrade-tutorial-powershell.md) 將引導您完成使用 PowerShell 進行應用程式升級的步驟。</span><span class="sxs-lookup"><span data-stu-id="597ec-157">[Upgrading your application using PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="597ec-158">使用 [升級參數](service-fabric-application-upgrade-parameters.md)來控制您應用程式的升級方式。</span><span class="sxs-lookup"><span data-stu-id="597ec-158">Control how your application is upgraded by using [upgrade parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="597ec-159">了解如何使用 [資料序列化](service-fabric-application-upgrade-data-serialization.md)，以讓您的應用程式升級相容。</span><span class="sxs-lookup"><span data-stu-id="597ec-159">Make your application upgrades compatible by learning how to use [data serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="597ec-160">參考 [進階主題](service-fabric-application-upgrade-advanced.md)，以了解如何在升級您的應用程式時使用進階功能。</span><span class="sxs-lookup"><span data-stu-id="597ec-160">Learn how to use advanced functionality while upgrading your application by referring to [Advanced topics](service-fabric-application-upgrade-advanced.md).</span></span>

<span data-ttu-id="597ec-161">參考 [疑難排解應用程式升級](service-fabric-application-upgrade-troubleshooting.md)中的步驟，以修正應用程式升級中常見的問題。</span><span class="sxs-lookup"><span data-stu-id="597ec-161">Fix common problems in application upgrades by referring to the steps in [Troubleshooting application upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>

[image1]: media/service-fabric-application-upgrade-tutorial/upgrade7.png
[image2]: media/service-fabric-application-upgrade-tutorial/upgrade1.png
[image3]: media/service-fabric-application-upgrade-tutorial/upgrade5.png
[image4]: media/service-fabric-application-upgrade-tutorial/upgrade6.png
