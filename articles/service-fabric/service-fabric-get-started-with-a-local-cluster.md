---
title: "aaaDeploy 和升級在本機執行 Azure microservices |Microsoft 文件"
description: "了解本機的 Service Fabric 叢集，tooset 部署現有的應用程式 tooit，和再升級該應用程式的方式。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 60a1f6a5-5478-46c0-80a8-18fe62da17a8
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi;mikhegn
ms.openlocfilehash: e5f5adc9edb71433b2a7635e9d661ff92a4b18ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-deploying-and-upgrading-applications-on-your-local-cluster"></a><span data-ttu-id="75fa5-103">在您的本機叢集上開始部署和升級應用程式</span><span class="sxs-lookup"><span data-stu-id="75fa5-103">Get started with deploying and upgrading applications on your local cluster</span></span>
<span data-ttu-id="75fa5-104">hello Azure Service Fabric SDK 包含的完整本機開發環境，您可以使用 tooquickly 開始部署及管理本機叢集上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="75fa5-104">hello Azure Service Fabric SDK includes a full local development environment that you can use tooquickly get started with deploying and managing applications on a local cluster.</span></span> <span data-ttu-id="75fa5-105">本文中，您可以建立本機叢集，部署現有的應用程式 tooit，然後再升級應用程式 tooa 新的版本，所有從 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="75fa5-105">In this article, you create a local cluster, deploy an existing application tooit, and then upgrade that application tooa new version, all from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="75fa5-106">本文假設您已經 [設定開發環境](service-fabric-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="75fa5-106">This article assumes that you already [set up your development environment](service-fabric-get-started.md).</span></span>
> 
> 

## <a name="create-a-local-cluster"></a><span data-ttu-id="75fa5-107">建立本機叢集</span><span class="sxs-lookup"><span data-stu-id="75fa5-107">Create a local cluster</span></span>
<span data-ttu-id="75fa5-108">Service Fabric 叢集代表一組您可以部署應用程式的硬體資源。</span><span class="sxs-lookup"><span data-stu-id="75fa5-108">A Service Fabric cluster represents a set of hardware resources that you can deploy applications to.</span></span> <span data-ttu-id="75fa5-109">一般而言，叢集所組成的任何位置從五個 toomany 數以千計的機器。</span><span class="sxs-lookup"><span data-stu-id="75fa5-109">Typically, a cluster is made up of anywhere from five toomany thousands of machines.</span></span> <span data-ttu-id="75fa5-110">不過，hello Service Fabric SDK 包含可以在單一電腦執行的叢集設定。</span><span class="sxs-lookup"><span data-stu-id="75fa5-110">However, hello Service Fabric SDK includes a cluster configuration that can run on a single machine.</span></span>

<span data-ttu-id="75fa5-111">請務必 toounderstand hello Service Fabric 本機叢集，並不是模擬器。</span><span class="sxs-lookup"><span data-stu-id="75fa5-111">It is important toounderstand that hello Service Fabric local cluster is not an emulator or simulator.</span></span> <span data-ttu-id="75fa5-112">它執行 hello 多電腦叢集找到的相同平台程式碼。</span><span class="sxs-lookup"><span data-stu-id="75fa5-112">It runs hello same platform code that is found on multi-machine clusters.</span></span> <span data-ttu-id="75fa5-113">hello 唯一的差異在於，它會執行 hello 平台的處理程序通常會分散到一部電腦上的五個機器。</span><span class="sxs-lookup"><span data-stu-id="75fa5-113">hello only difference is that it runs hello platform processes that are normally spread across five machines on one machine.</span></span>

<span data-ttu-id="75fa5-114">hello SDK 提供本機叢集的兩個方式 tooset: Windows PowerShell 指令碼和 hello 本機叢集管理員 系統匣應用程式。</span><span class="sxs-lookup"><span data-stu-id="75fa5-114">hello SDK provides two ways tooset up a local cluster: a Windows PowerShell script and hello Local Cluster Manager system tray app.</span></span> <span data-ttu-id="75fa5-115">在此教學課程中，我們會使用 hello PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="75fa5-115">In this tutorial, we use hello PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="75fa5-116">如果您已藉由從 Visual Studio 部署應用程式來建立本機叢集，您可以略過本節。</span><span class="sxs-lookup"><span data-stu-id="75fa5-116">If you have already created a local cluster by deploying an application from Visual Studio, you can skip this section.</span></span>
> 
> 

1. <span data-ttu-id="75fa5-117">以系統管理員身分啟動新的 PowerShell 視窗。</span><span class="sxs-lookup"><span data-stu-id="75fa5-117">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="75fa5-118">從 hello SDK 資料夾中執行 hello 叢集安裝指令碼：</span><span class="sxs-lookup"><span data-stu-id="75fa5-118">Run hello cluster setup script from hello SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"
    ```
   
    <span data-ttu-id="75fa5-119">叢集設定需要一些時間。</span><span class="sxs-lookup"><span data-stu-id="75fa5-119">Cluster setup takes a few moments.</span></span> <span data-ttu-id="75fa5-120">設定完成後，您應該會看到輸出類似於：</span><span class="sxs-lookup"><span data-stu-id="75fa5-120">After setup is finished, you should see output similar to:</span></span>
   
    ![叢集設定輸出][cluster-setup-success]
   
    <span data-ttu-id="75fa5-122">現在您已經準備就緒 tootry 部署應用程式 tooyour 叢集。</span><span class="sxs-lookup"><span data-stu-id="75fa5-122">You are now ready tootry deploying an application tooyour cluster.</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="75fa5-123">部署應用程式</span><span class="sxs-lookup"><span data-stu-id="75fa5-123">Deploy an application</span></span>
<span data-ttu-id="75fa5-124">hello Service Fabric SDK 包含一組豐富的架構和開發人員工具建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="75fa5-124">hello Service Fabric SDK includes a rich set of frameworks and developer tooling for creating applications.</span></span> <span data-ttu-id="75fa5-125">如果您想要了解如何 toocreate 應用程式，在 Visual Studio 中，請參閱[Visual Studio 中建立 Service Fabric 應用程式第一次](service-fabric-create-your-first-application-in-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="75fa5-125">If you are interested in learning how toocreate applications in Visual Studio, see [Create your first Service Fabric application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span>

<span data-ttu-id="75fa5-126">在此教學課程中，您使用現有的範例應用程式 （稱為 WordCount），讓您可以專注於 hello 管理方面 hello 平台： 部署、 監視及升級。</span><span class="sxs-lookup"><span data-stu-id="75fa5-126">In this tutorial, you use an existing sample application (called WordCount) so that you can focus on hello management aspects of hello platform: deployment, monitoring, and upgrade.</span></span>

1. <span data-ttu-id="75fa5-127">以系統管理員身分啟動新的 PowerShell 視窗。</span><span class="sxs-lookup"><span data-stu-id="75fa5-127">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="75fa5-128">匯入 hello Service Fabric SDK PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="75fa5-128">Import hello Service Fabric SDK PowerShell module.</span></span>
   
    ```powershell
    Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
    ```
3. <span data-ttu-id="75fa5-129">建立會在下載及部署，例如 C:\ServiceFabric 目錄 toostore hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="75fa5-129">Create a directory toostore hello application that you download and deploy, such as C:\ServiceFabric.</span></span>
   
    ```powershell
    mkdir c:\ServiceFabric\
    cd c:\ServiceFabric\
    ```
4. <span data-ttu-id="75fa5-130">[下載 hello WordCount 應用程式](http://aka.ms/servicefabric-wordcountapp)toohello 您所建立的位置。</span><span class="sxs-lookup"><span data-stu-id="75fa5-130">[Download hello WordCount application](http://aka.ms/servicefabric-wordcountapp) toohello location you created.</span></span>  <span data-ttu-id="75fa5-131">注意： hello Microsoft Edge 瀏覽器 hello 會將檔案儲存與*.zip*延伸模組。</span><span class="sxs-lookup"><span data-stu-id="75fa5-131">Note: hello Microsoft Edge browser saves hello file with a *.zip* extension.</span></span>  <span data-ttu-id="75fa5-132">也變更 hello 副檔名*.sfpkg*。</span><span class="sxs-lookup"><span data-stu-id="75fa5-132">Change hello file extension too*.sfpkg*.</span></span>
5. <span data-ttu-id="75fa5-133">連接 toohello 本機叢集：</span><span class="sxs-lookup"><span data-stu-id="75fa5-133">Connect toohello local cluster:</span></span>
   
    ```powershell
    Connect-ServiceFabricCluster localhost:19000
    ```
6. <span data-ttu-id="75fa5-134">建立新的應用程式使用的名稱和路徑 toohello 應用程式套件的 hello SDK 的部署命令。</span><span class="sxs-lookup"><span data-stu-id="75fa5-134">Create a new application using hello SDK's deployment command with a name and a path toohello application package.</span></span>
   
    ```powershell  
   Publish-NewServiceFabricApplication -ApplicationPackagePath c:\ServiceFabric\WordCountV1.sfpkg -ApplicationName "fabric:/WordCount"
    ```
   
    <span data-ttu-id="75fa5-135">如果一切順利，您應該會看到下列輸出的 hello:</span><span class="sxs-lookup"><span data-stu-id="75fa5-135">If all goes well, you should see hello following output:</span></span>
   
    ![部署應用程式 toohello 本機叢集][deploy-app-to-local-cluster]
7. <span data-ttu-id="75fa5-137">toosee hello 應用程式的動作，啟動 hello 瀏覽器，並瀏覽過[http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html)。</span><span class="sxs-lookup"><span data-stu-id="75fa5-137">toosee hello application in action, launch hello browser and navigate too[http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html).</span></span> <span data-ttu-id="75fa5-138">您應該會看到：</span><span class="sxs-lookup"><span data-stu-id="75fa5-138">You should see:</span></span>
   
    ![部署應用程式 UI][deployed-app-ui]
   
    <span data-ttu-id="75fa5-140">hello WordCount 應用程式很簡單。</span><span class="sxs-lookup"><span data-stu-id="75fa5-140">hello WordCount application is simple.</span></span> <span data-ttu-id="75fa5-141">它包含用戶端 JavaScript 程式碼 toogenerate 隨機五個字元"字組 」，然後是轉送 toohello 透過 ASP.NET Web API 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="75fa5-141">It includes client-side JavaScript code toogenerate random five-character "words", which are then relayed toohello application via ASP.NET Web API.</span></span> <span data-ttu-id="75fa5-142">可設定狀態的服務會追蹤 hello 計算的字組的數目。</span><span class="sxs-lookup"><span data-stu-id="75fa5-142">A stateful service tracks hello number of words counted.</span></span> <span data-ttu-id="75fa5-143">它們會分割 hello 的 hello word 的第一個字元為基礎。</span><span class="sxs-lookup"><span data-stu-id="75fa5-143">They are partitioned based on hello first character of hello word.</span></span> <span data-ttu-id="75fa5-144">您可以在 hello hello WordCount 應用程式找到 hello 原始程式碼[傳統使用者入門範例](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount)。</span><span class="sxs-lookup"><span data-stu-id="75fa5-144">You can find hello source code for hello WordCount app in hello [classic getting started samples](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).</span></span>
   
    <span data-ttu-id="75fa5-145">我們所部署的 hello 應用程式包含四個資料分割。</span><span class="sxs-lookup"><span data-stu-id="75fa5-145">hello application that we deployed contains four partitions.</span></span> <span data-ttu-id="75fa5-146">以 A 到 G 開頭的單字會儲存在 hello 第一個資料分割，因此與透過 N H 開頭的單字會儲存在 hello 第二個資料分割，依此類推。</span><span class="sxs-lookup"><span data-stu-id="75fa5-146">So words beginning with A through G are stored in hello first partition, words beginning with H through N are stored in hello second partition, and so on.</span></span>

## <a name="view-application-details-and-status"></a><span data-ttu-id="75fa5-147">檢視應用程式詳細資料和狀態</span><span class="sxs-lookup"><span data-stu-id="75fa5-147">View application details and status</span></span>
<span data-ttu-id="75fa5-148">既然我們已部署的 hello 應用程式，讓我們看看一些在 PowerShell 中的 hello 應用程式詳細資料。</span><span class="sxs-lookup"><span data-stu-id="75fa5-148">Now that we have deployed hello application, let's look at some of hello app details in PowerShell.</span></span>

1. <span data-ttu-id="75fa5-149">查詢 hello 叢集上的所有已部署應用程式：</span><span class="sxs-lookup"><span data-stu-id="75fa5-149">Query all deployed applications on hello cluster:</span></span>
   
    ```powershell
    Get-ServiceFabricApplication
    ```
   
    <span data-ttu-id="75fa5-150">假設您只有部署 hello WordCount 應用程式，您會看到類似的項目：</span><span class="sxs-lookup"><span data-stu-id="75fa5-150">Assuming that you have only deployed hello WordCount app, you see something similar to:</span></span>
   
    ![在 PowerShell 中查詢所有已部署的應用程式][ps-getsfapp]
2. <span data-ttu-id="75fa5-152">藉由查詢 hello 組包含在 hello WordCount 應用程式的服務移 toohello 下一個層級。</span><span class="sxs-lookup"><span data-stu-id="75fa5-152">Go toohello next level by querying hello set of services that are included in hello WordCount application.</span></span>
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![在 PowerShell 中的 hello 應用程式的清單服務][ps-getsfsvc]
   
    <span data-ttu-id="75fa5-154">hello 應用程式是由兩個服務、 hello web 前端，hello 可設定狀態服務，可管理 hello 文字所組成。</span><span class="sxs-lookup"><span data-stu-id="75fa5-154">hello application is made up of two services, hello web front end, and hello stateful service that manages hello words.</span></span>
3. <span data-ttu-id="75fa5-155">最後，查看 hello 清單的資料分割的 WordCountService:</span><span class="sxs-lookup"><span data-stu-id="75fa5-155">Finally, look at hello list of partitions for WordCountService:</span></span>
   
    ```powershell
    Get-ServiceFabricPartition 'fabric:/WordCount/WordCountService'
    ```
   
    ![在 PowerShell 中檢視 hello 服務分割][ps-getsfpartitions]
   
    <span data-ttu-id="75fa5-157">hello 的使用，例如所有 Service Fabric PowerShell 命令的命令集，您可能會連線至本機或遠端任何叢集無法進行。</span><span class="sxs-lookup"><span data-stu-id="75fa5-157">hello set of commands that you used, like all Service Fabric PowerShell commands, are available for any cluster that you might connect to, local or remote.</span></span>
   
    <span data-ttu-id="75fa5-158">對於與 hello 叢集更視覺化的方式 toointeract，您可以使用 hello web 為基礎的 Service Fabric 總管工具瀏覽過[http://localhost:19080/總管](http://localhost:19080/Explorer)hello 瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="75fa5-158">For a more visual way toointeract with hello cluster, you can use hello web-based Service Fabric Explorer tool by navigating too[http://localhost:19080/Explorer](http://localhost:19080/Explorer) in hello browser.</span></span>
   
    ![在 Service Fabric 總管中檢視應用程式詳細資料][sfx-service-overview]
   
   > [!NOTE]
   > <span data-ttu-id="75fa5-160">toolearn 進一步了解 Service Fabric 總管，請參閱[視覺化您的叢集，利用 Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="75fa5-160">toolearn more about Service Fabric Explorer, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
   > 
   > 

## <a name="upgrade-an-application"></a><span data-ttu-id="75fa5-161">升級應用程式</span><span class="sxs-lookup"><span data-stu-id="75fa5-161">Upgrade an application</span></span>
<span data-ttu-id="75fa5-162">Service Fabric 提供無停機時間升級，藉由監視便會復原整個 hello 叢集 hello hello 應用程式的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="75fa5-162">Service Fabric provides no-downtime upgrades by monitoring hello health of hello application as it rolls out across hello cluster.</span></span> <span data-ttu-id="75fa5-163">執行 hello WordCount 應用程式的升級。</span><span class="sxs-lookup"><span data-stu-id="75fa5-163">Perform an upgrade of hello WordCount application.</span></span>

<span data-ttu-id="75fa5-164">hello 新版 hello 應用程式現在會計算某個母音以開頭的單字。</span><span class="sxs-lookup"><span data-stu-id="75fa5-164">hello new version of hello application now counts only words that begin with a vowel.</span></span> <span data-ttu-id="75fa5-165">因為 hello 升級中推出，我們會看到兩個 hello 應用程式的行為變更。</span><span class="sxs-lookup"><span data-stu-id="75fa5-165">As hello upgrade rolls out, we see two changes in hello application's behavior.</span></span> <span data-ttu-id="75fa5-166">首先，hello 速率 hello 計數成長速率應該變慢，因為較少的字詞會被計算。</span><span class="sxs-lookup"><span data-stu-id="75fa5-166">First, hello rate at which hello count grows should slow, since fewer words are being counted.</span></span> <span data-ttu-id="75fa5-167">第二，由於 hello 第一個資料分割都有兩個母音 （A 和 E） 及所有其他資料分割只包含一個每個，計數應該最後開始 toooutpace hello 其他人。</span><span class="sxs-lookup"><span data-stu-id="75fa5-167">Second, since hello first partition has two vowels (A and E) and all other partitions contain only one each, its count should eventually start toooutpace hello others.</span></span>

1. <span data-ttu-id="75fa5-168">[下載 hello WordCount 第 2 版封裝](http://aka.ms/servicefabric-wordcountappv2)toohello 下載 hello 第 1 版套件的相同位置。</span><span class="sxs-lookup"><span data-stu-id="75fa5-168">[Download hello WordCount version 2 package](http://aka.ms/servicefabric-wordcountappv2) toohello same location where you downloaded hello version 1 package.</span></span>
2. <span data-ttu-id="75fa5-169">傳回 tooyour PowerShell 視窗，並使用 hello SDK tooregister hello hello 叢集中的新版本升級 命令。</span><span class="sxs-lookup"><span data-stu-id="75fa5-169">Return tooyour PowerShell window and use hello SDK's upgrade command tooregister hello new version in hello cluster.</span></span> <span data-ttu-id="75fa5-170">然後開始升級 hello fabric: / WordCount 應用程式。</span><span class="sxs-lookup"><span data-stu-id="75fa5-170">Then begin upgrading hello fabric:/WordCount application.</span></span>
   
    ```powershell
    Publish-UpgradedServiceFabricApplication -ApplicationPackagePath C:\ServiceFabric\WordCountV2.sfpkg -ApplicationName "fabric:/WordCount" -UpgradeParameters @{"FailureAction"="Rollback"; "UpgradeReplicaSetCheckTimeout"=1; "Monitored"=$true; "Force"=$true}
    ```
   
    <span data-ttu-id="75fa5-171">您應該會看到如 hello 升級輸出在 PowerShell 中的 hello 下列開始。</span><span class="sxs-lookup"><span data-stu-id="75fa5-171">You should see hello following output in PowerShell as hello upgrade begins.</span></span>
   
    ![在 PowerShell 中的升級進度][ps-appupgradeprogress]
3. <span data-ttu-id="75fa5-173">繼續 hello 升級時，您可能會發現它更容易 toomonitor 其狀態從 Service Fabric 總管。</span><span class="sxs-lookup"><span data-stu-id="75fa5-173">While hello upgrade is proceeding, you may find it easier toomonitor its status from Service Fabric Explorer.</span></span> <span data-ttu-id="75fa5-174">啟動瀏覽器視窗並瀏覽過[http://localhost:19080/總管](http://localhost:19080/Explorer)。</span><span class="sxs-lookup"><span data-stu-id="75fa5-174">Launch a browser window and navigate too[http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="75fa5-175">展開**應用程式**在 hello 左側 hello 樹狀目錄，然後選擇  **WordCount**，最後再**fabric: / WordCount**。</span><span class="sxs-lookup"><span data-stu-id="75fa5-175">Expand **Applications** in hello tree on hello left, then choose **WordCount**, and finally **fabric:/WordCount**.</span></span> <span data-ttu-id="75fa5-176">Hello essentials 索引標籤中，您會看到 hello hello 升級狀態，透過 hello 叢集的升級網域進行時。</span><span class="sxs-lookup"><span data-stu-id="75fa5-176">In hello essentials tab, you see hello status of hello upgrade as it proceeds through hello cluster's upgrade domains.</span></span>
   
    ![在 Service Fabric 總管中的升級進度][sfx-upgradeprogress]
   
    <span data-ttu-id="75fa5-178">Hello 升級繼續進行到每個網域，是執行的 hello 應用程式運作不正確的 tooensure 健康情況檢查。</span><span class="sxs-lookup"><span data-stu-id="75fa5-178">As hello upgrade proceeds through each domain, health checks are performed tooensure that hello application is behaving properly.</span></span>
4. <span data-ttu-id="75fa5-179">如果您重新執行 hello 先前查詢的 hello 組 hello 網狀架構中的服務: / WordCount 應用程式，請注意，hello WordCountService 版本已變更，但 hello WordCountWebService 版本不提供支援：</span><span class="sxs-lookup"><span data-stu-id="75fa5-179">If you rerun hello earlier query for hello set of services in hello fabric:/WordCount application, notice that hello WordCountService version changed but hello WordCountWebService version did not:</span></span>
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![在升級後查詢應用程式服務][ps-getsfsvc-postupgrade]
   
    <span data-ttu-id="75fa5-181">此範例強調 Service Fabric 如何管理應用程式升級。</span><span class="sxs-lookup"><span data-stu-id="75fa5-181">This example highlights how Service Fabric manages application upgrades.</span></span> <span data-ttu-id="75fa5-182">它所接觸只有 hello 的一組服務 （或在這些服務的程式碼/組態套件） 已變更，會使升級更快速且更可靠的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="75fa5-182">It touches only hello set of services (or code/configuration packages within those services) that have changed, which makes hello process of upgrading faster and more reliable.</span></span>
5. <span data-ttu-id="75fa5-183">最後，傳回 toohello hello 新版應用程式的瀏覽器 tooobserve hello 行為。</span><span class="sxs-lookup"><span data-stu-id="75fa5-183">Finally, return toohello browser tooobserve hello behavior of hello new application version.</span></span> <span data-ttu-id="75fa5-184">如預期般，速度變慢，hello 計數進展和 hello 第一個分割區最後會有稍微多個 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="75fa5-184">As expected, hello count progresses more slowly, and hello first partition ends up with slightly more of hello volume.</span></span>
   
    ![檢視 hello 新版本的 hello hello 瀏覽器中的應用程式][deployed-app-ui-v2]

## <a name="cleaning-up"></a><span data-ttu-id="75fa5-186">清除</span><span class="sxs-lookup"><span data-stu-id="75fa5-186">Cleaning up</span></span>
<span data-ttu-id="75fa5-187">包裝之前，這是很重要 hello 本機叢集的 tooremember 真實。</span><span class="sxs-lookup"><span data-stu-id="75fa5-187">Before wrapping up, it's important tooremember that hello local cluster is real.</span></span> <span data-ttu-id="75fa5-188">應用程式繼續 toorun hello 背景中，直到您將它們移除。</span><span class="sxs-lookup"><span data-stu-id="75fa5-188">Applications continue toorun in hello background until you remove them.</span></span>  <span data-ttu-id="75fa5-189">根據您的應用程式的 hello 本質，執行中應用程式可能佔用大量的資源，您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="75fa5-189">Depending on hello nature of your apps, a running app can take up significant resources on your machine.</span></span> <span data-ttu-id="75fa5-190">您有數個選項 toomanage 應用程式和 hello 叢集：</span><span class="sxs-lookup"><span data-stu-id="75fa5-190">You have several options toomanage applications and hello cluster:</span></span>

1. <span data-ttu-id="75fa5-191">tooremove 個別的應用程式及其所有的資料，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="75fa5-191">tooremove an individual application and all it's data, run hello following command:</span></span>
   
    ```powershell
    Unpublish-ServiceFabricApplication -ApplicationName "fabric:/WordCount"
    ```
   
    <span data-ttu-id="75fa5-192">或者，您也可以從 hello Service Fabric 總管刪除 hello 應用程式**動作**功能表或 hello hello 左側的應用程式清單檢視中的內容功能表。</span><span class="sxs-lookup"><span data-stu-id="75fa5-192">Or, delete hello application from hello Service Fabric Explorer **ACTIONS** menu or hello context menu in hello left-hand application list view.</span></span>
   
    ![在 Service Fabric 總管中刪除應用程式][sfe-delete-application]
2. <span data-ttu-id="75fa5-194">刪除之後 hello 應用程式從 hello 叢集中，移除註冊 1.0.0 和 2.0.0 的 hello WordCount 應用程式類型版本。</span><span class="sxs-lookup"><span data-stu-id="75fa5-194">After deleting hello application from hello cluster, unregister versions 1.0.0 and 2.0.0 of hello WordCount application type.</span></span> <span data-ttu-id="75fa5-195">刪除作業會移除 hello 應用程式封裝，包括 hello 程式碼和組態，從 hello 叢集映像存放區。</span><span class="sxs-lookup"><span data-stu-id="75fa5-195">Deletion removes hello application packages, including hello code and configuration, from hello cluster's image store.</span></span>
   
    ```powershell
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 2.0.0
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 1.0.0
    ```
   
    <span data-ttu-id="75fa5-196">或者，您也可以在 Service Fabric 總管] 中，選擇 [**解除佈建類型**hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="75fa5-196">Or, in Service Fabric Explorer, choose **Unprovision Type** for hello application.</span></span>
3. <span data-ttu-id="75fa5-197">按一下 向下 hello 叢集但保留 hello 應用程式資料，然後追蹤、 tooshut**停止本機叢集**hello 系統匣應用程式中。</span><span class="sxs-lookup"><span data-stu-id="75fa5-197">tooshut down hello cluster but keep hello application data and traces, click **Stop Local Cluster** in hello system tray app.</span></span>
4. <span data-ttu-id="75fa5-198">完全，按一下 toodelete hello 叢集**移除本機叢集**hello 系統匣應用程式中。</span><span class="sxs-lookup"><span data-stu-id="75fa5-198">toodelete hello cluster entirely, click **Remove Local Cluster** in hello system tray app.</span></span> <span data-ttu-id="75fa5-199">此選項將會導致其他慢速部署 hello 下次您在 Visual Studio 中按下 F5。</span><span class="sxs-lookup"><span data-stu-id="75fa5-199">This option will result in another slow deployment hello next time you press F5 in Visual Studio.</span></span> <span data-ttu-id="75fa5-200">只有當您不想在 toouse 這段時間，或如果您需要 tooreclaim 資源，移除 hello 本機叢集。</span><span class="sxs-lookup"><span data-stu-id="75fa5-200">Remove hello local cluster only if you don't intend toouse it for some time or if you need tooreclaim resources.</span></span>

## <a name="one-node-and-five-node-cluster-mode"></a><span data-ttu-id="75fa5-201">1 個節點和 5 個節點叢集模式</span><span class="sxs-lookup"><span data-stu-id="75fa5-201">One-node and five-node cluster mode</span></span>
<span data-ttu-id="75fa5-202">開發應用程式時，您常會發現自己快速反覆撰寫程式碼、偵錯、變更程式碼和偵錯。</span><span class="sxs-lookup"><span data-stu-id="75fa5-202">When developing applications, you often find yourself doing quick iterations of writing code, debugging, changing code, and debugging.</span></span> <span data-ttu-id="75fa5-203">toohelp 最佳化這個程序，hello 本機叢集可以執行兩種模式： 其中一個節點或五個節點。</span><span class="sxs-lookup"><span data-stu-id="75fa5-203">toohelp optimize this process, hello local cluster can run in two modes: one-node or five-node.</span></span> <span data-ttu-id="75fa5-204">這兩個叢集模式各有優點。</span><span class="sxs-lookup"><span data-stu-id="75fa5-204">Both cluster modes have their benefits.</span></span> <span data-ttu-id="75fa5-205">五個節點的叢集模式可讓您 toowork 與實際的叢集。</span><span class="sxs-lookup"><span data-stu-id="75fa5-205">Five-node cluster mode enables you toowork with a real cluster.</span></span> <span data-ttu-id="75fa5-206">您可以測試容錯移轉案例，使用更多您的服務的執行個體和複本。</span><span class="sxs-lookup"><span data-stu-id="75fa5-206">You can test failover scenarios, work with more instances and replicas of your services.</span></span> <span data-ttu-id="75fa5-207">最佳化的 toodo 快速部署和註冊服務，toohelp 您快速驗證程式碼使用 hello Service Fabric 執行階段的單一節點叢集模式。</span><span class="sxs-lookup"><span data-stu-id="75fa5-207">One-node cluster mode is optimized toodo quick deployment and registration of services, toohelp you quickly validate code using hello Service Fabric runtime.</span></span>

<span data-ttu-id="75fa5-208">1 個節點叢集或 5 個節點叢集模式皆不是模擬器。</span><span class="sxs-lookup"><span data-stu-id="75fa5-208">Neither one-node cluster or five-node cluster modes are an emulator or simulator.</span></span> <span data-ttu-id="75fa5-209">hello 本機開發叢集執行 hello 多電腦叢集找到的相同平台程式碼。</span><span class="sxs-lookup"><span data-stu-id="75fa5-209">hello local development cluster runs hello same platform code that is found on multi-machine clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="75fa5-210">當您變更 hello 叢集模式時，從系統移除 hello 目前叢集，並建立新的叢集。</span><span class="sxs-lookup"><span data-stu-id="75fa5-210">When you change hello cluster mode, hello current cluster is removed from your system and a new cluster is created.</span></span> <span data-ttu-id="75fa5-211">當您變更叢集模式時，會刪除 hello hello 叢集中儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="75fa5-211">hello data stored in hello cluster is deleted when you change cluster mode.</span></span>
> 
> 

<span data-ttu-id="75fa5-212">toochange hello 模式 tooone 節點的叢集，選取**切換叢集模式**hello 服務網狀架構本機叢集管理員中。</span><span class="sxs-lookup"><span data-stu-id="75fa5-212">toochange hello mode tooone-node cluster, select **Switch Cluster Mode** in hello Service Fabric Local Cluster Manager.</span></span>

![切換叢集模式][switch-cluster-mode]

<span data-ttu-id="75fa5-214">或者，使用 PowerShell 變更 hello 叢集模式：</span><span class="sxs-lookup"><span data-stu-id="75fa5-214">Or, change hello cluster mode using PowerShell:</span></span>

1. <span data-ttu-id="75fa5-215">以系統管理員身分啟動新的 PowerShell 視窗。</span><span class="sxs-lookup"><span data-stu-id="75fa5-215">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="75fa5-216">從 hello SDK 資料夾中執行 hello 叢集安裝指令碼：</span><span class="sxs-lookup"><span data-stu-id="75fa5-216">Run hello cluster setup script from hello SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1" -CreateOneNodeCluster
    ```
   
    <span data-ttu-id="75fa5-217">叢集設定需要一些時間。</span><span class="sxs-lookup"><span data-stu-id="75fa5-217">Cluster setup takes a few moments.</span></span> <span data-ttu-id="75fa5-218">設定完成後，您應該會看到輸出類似於：</span><span class="sxs-lookup"><span data-stu-id="75fa5-218">After setup is finished, you should see output similar to:</span></span>
   
    ![叢集設定輸出][cluster-setup-success-1-node]

## <a name="next-steps"></a><span data-ttu-id="75fa5-220">後續步驟</span><span class="sxs-lookup"><span data-stu-id="75fa5-220">Next steps</span></span>
* <span data-ttu-id="75fa5-221">您現在已部署並升級某些預先建置的應用程式，您可以 [嘗試在 Visual Studio 中建立自己的應用程式](service-fabric-create-your-first-application-in-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="75fa5-221">Now that you have deployed and upgraded some pre-built applications, you can [try building your own in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span>
* <span data-ttu-id="75fa5-222">本文章中的 hello 本機叢集上執行的所有 hello 動作可都對[Azure 叢集概略](service-fabric-cluster-creation-via-portal.md)以及。</span><span class="sxs-lookup"><span data-stu-id="75fa5-222">All hello actions performed on hello local cluster in this article can be performed on an [Azure cluster](service-fabric-cluster-creation-via-portal.md) as well.</span></span>
* <span data-ttu-id="75fa5-223">我們執行本文中的 hello 升級為基本。</span><span class="sxs-lookup"><span data-stu-id="75fa5-223">hello upgrade that we performed in this article was basic.</span></span> <span data-ttu-id="75fa5-224">請參閱 hello[升級文件](service-fabric-application-upgrade.md)toolearn 更多關於 hello 功能及彈性的 Service Fabric 升級。</span><span class="sxs-lookup"><span data-stu-id="75fa5-224">See hello [upgrade documentation](service-fabric-application-upgrade.md) toolearn more about hello power and flexibility of Service Fabric upgrades.</span></span>

<!-- Images -->

[cluster-setup-success]: ./media/service-fabric-get-started-with-a-local-cluster/LocalClusterSetup.png
[extracted-app-package]: ./media/service-fabric-get-started-with-a-local-cluster/ExtractedAppPackage.png
[deploy-app-to-local-cluster]: ./media/service-fabric-get-started-with-a-local-cluster/DeployAppToLocalCluster.png
[deployed-app-ui]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-v1.png
[deployed-app-ui-v2]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-PostUpgrade.png
[sfx-app-instance]: ./media/service-fabric-get-started-with-a-local-cluster/SfxAppInstance.png
[sfx-two-app-instances-different-partitions]: ./media/service-fabric-get-started-with-a-local-cluster/SfxTwoAppInstances-DifferentPartitionCount.png
[ps-getsfapp]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFApp.png
[ps-getsfsvc]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc.png
[ps-getsfpartitions]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFPartitions.png
[ps-appupgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/PS-AppUpgradeProgress.png
[ps-getsfsvc-postupgrade]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc-PostUpgrade.png
[sfx-upgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/SfxUpgradeOverview.png
[sfx-service-overview]: ./media/service-fabric-get-started-with-a-local-cluster/sfx-service-overview.png
[sfe-delete-application]: ./media/service-fabric-get-started-with-a-local-cluster/sfe-delete-application.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
[switch-cluster-mode]: ./media/service-fabric-get-started-with-a-local-cluster/switch-cluster-mode.png
