---
title: "在本機部署和升級 Azure 微服務 | Microsoft Docs"
description: "了解如何設定本機 Service Fabric 叢集、將現有的應用程式部署至該叢集，然後升級該應用程式。"
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
ms.openlocfilehash: 359677972c7e1fa3f7435052021ddfae5b1ed85e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-deploying-and-upgrading-applications-on-your-local-cluster"></a><span data-ttu-id="71a8f-103">在您的本機叢集上開始部署和升級應用程式</span><span class="sxs-lookup"><span data-stu-id="71a8f-103">Get started with deploying and upgrading applications on your local cluster</span></span>
<span data-ttu-id="71a8f-104">Azure Service Fabric SDK 包含完整的本機開發環境，可讓您快速地在本機叢集上開始部署和管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="71a8f-104">The Azure Service Fabric SDK includes a full local development environment that you can use to quickly get started with deploying and managing applications on a local cluster.</span></span> <span data-ttu-id="71a8f-105">在本文中，您會從 Windows PowerShell 建立本機叢集、將現有的應用程式部署至該叢集，然後將應用程式升級為新版本。</span><span class="sxs-lookup"><span data-stu-id="71a8f-105">In this article, you create a local cluster, deploy an existing application to it, and then upgrade that application to a new version, all from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="71a8f-106">本文假設您已經 [設定開發環境](service-fabric-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="71a8f-106">This article assumes that you already [set up your development environment](service-fabric-get-started.md).</span></span>
> 
> 

## <a name="create-a-local-cluster"></a><span data-ttu-id="71a8f-107">建立本機叢集</span><span class="sxs-lookup"><span data-stu-id="71a8f-107">Create a local cluster</span></span>
<span data-ttu-id="71a8f-108">Service Fabric 叢集代表一組您可以部署應用程式的硬體資源。</span><span class="sxs-lookup"><span data-stu-id="71a8f-108">A Service Fabric cluster represents a set of hardware resources that you can deploy applications to.</span></span> <span data-ttu-id="71a8f-109">通常，叢集是由任意數量的電腦 (從 5 部到數千部) 所組成。</span><span class="sxs-lookup"><span data-stu-id="71a8f-109">Typically, a cluster is made up of anywhere from five to many thousands of machines.</span></span> <span data-ttu-id="71a8f-110">不過，Service Fabric SDK 包含可在一部電腦上執行的叢集組態。</span><span class="sxs-lookup"><span data-stu-id="71a8f-110">However, the Service Fabric SDK includes a cluster configuration that can run on a single machine.</span></span>

<span data-ttu-id="71a8f-111">請務必了解 Service Fabric 本機叢集不是模擬器。</span><span class="sxs-lookup"><span data-stu-id="71a8f-111">It is important to understand that the Service Fabric local cluster is not an emulator or simulator.</span></span> <span data-ttu-id="71a8f-112">它會執行在多部電腦的叢集上找到的相同平台程式碼。</span><span class="sxs-lookup"><span data-stu-id="71a8f-112">It runs the same platform code that is found on multi-machine clusters.</span></span> <span data-ttu-id="71a8f-113">唯一的差別在於它會在一部電腦上執行通常分散於五部電腦的平台程序。</span><span class="sxs-lookup"><span data-stu-id="71a8f-113">The only difference is that it runs the platform processes that are normally spread across five machines on one machine.</span></span>

<span data-ttu-id="71a8f-114">SDK 提供兩種方式來設定本機叢集：Windows PowerShell 指令碼和 [本機叢集管理員] 系統匣應用程式。</span><span class="sxs-lookup"><span data-stu-id="71a8f-114">The SDK provides two ways to set up a local cluster: a Windows PowerShell script and the Local Cluster Manager system tray app.</span></span> <span data-ttu-id="71a8f-115">在本教學課程中，我們會使用 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="71a8f-115">In this tutorial, we use the PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="71a8f-116">如果您已藉由從 Visual Studio 部署應用程式來建立本機叢集，您可以略過本節。</span><span class="sxs-lookup"><span data-stu-id="71a8f-116">If you have already created a local cluster by deploying an application from Visual Studio, you can skip this section.</span></span>
> 
> 

1. <span data-ttu-id="71a8f-117">以系統管理員身分啟動新的 PowerShell 視窗。</span><span class="sxs-lookup"><span data-stu-id="71a8f-117">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="71a8f-118">從 SDK 資料夾執行叢集設定指令碼：</span><span class="sxs-lookup"><span data-stu-id="71a8f-118">Run the cluster setup script from the SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"
    ```
   
    <span data-ttu-id="71a8f-119">叢集設定需要一些時間。</span><span class="sxs-lookup"><span data-stu-id="71a8f-119">Cluster setup takes a few moments.</span></span> <span data-ttu-id="71a8f-120">設定完成後，您應該會看到輸出類似於：</span><span class="sxs-lookup"><span data-stu-id="71a8f-120">After setup is finished, you should see output similar to:</span></span>
   
    ![叢集設定輸出][cluster-setup-success]
   
    <span data-ttu-id="71a8f-122">您現在已準備好將應用程式部署至您的叢集。</span><span class="sxs-lookup"><span data-stu-id="71a8f-122">You are now ready to try deploying an application to your cluster.</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="71a8f-123">部署應用程式</span><span class="sxs-lookup"><span data-stu-id="71a8f-123">Deploy an application</span></span>
<span data-ttu-id="71a8f-124">Service Fabric SDK 包含一組豐富的架構以及用來建立應用程式的開發人員工具。</span><span class="sxs-lookup"><span data-stu-id="71a8f-124">The Service Fabric SDK includes a rich set of frameworks and developer tooling for creating applications.</span></span> <span data-ttu-id="71a8f-125">如果您有興趣學習如何在 Visual Studio 中建立應用程式，請參閱 [在 Visual Studio 中建立第一個 Service Fabric 應用程式](service-fabric-create-your-first-application-in-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="71a8f-125">If you are interested in learning how to create applications in Visual Studio, see [Create your first Service Fabric application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span>

<span data-ttu-id="71a8f-126">在本教學課程中，您會使用現有的範例應用程式 (稱為 WordCount)，如此您即可專注於平台的管理層面：部署、監視及升級。</span><span class="sxs-lookup"><span data-stu-id="71a8f-126">In this tutorial, you use an existing sample application (called WordCount) so that you can focus on the management aspects of the platform: deployment, monitoring, and upgrade.</span></span>

1. <span data-ttu-id="71a8f-127">以系統管理員身分啟動新的 PowerShell 視窗。</span><span class="sxs-lookup"><span data-stu-id="71a8f-127">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="71a8f-128">匯入 Service Fabric SDK PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="71a8f-128">Import the Service Fabric SDK PowerShell module.</span></span>
   
    ```powershell
    Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
    ```
3. <span data-ttu-id="71a8f-129">建立目錄以儲存您下載和部署的應用程式，例如 C:\ServiceFabric。</span><span class="sxs-lookup"><span data-stu-id="71a8f-129">Create a directory to store the application that you download and deploy, such as C:\ServiceFabric.</span></span>
   
    ```powershell
    mkdir c:\ServiceFabric\
    cd c:\ServiceFabric\
    ```
4. <span data-ttu-id="71a8f-130">[將 WordCount 應用程式下載](http://aka.ms/servicefabric-wordcountapp) 至您建立的位置。</span><span class="sxs-lookup"><span data-stu-id="71a8f-130">[Download the WordCount application](http://aka.ms/servicefabric-wordcountapp) to the location you created.</span></span>  <span data-ttu-id="71a8f-131">注意︰Microsoft Edge 瀏覽器會使用 .zip  副檔名來儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="71a8f-131">Note: the Microsoft Edge browser saves the file with a *.zip* extension.</span></span>  <span data-ttu-id="71a8f-132">請將副檔名變更為 .sfpkg 。</span><span class="sxs-lookup"><span data-stu-id="71a8f-132">Change the file extension to *.sfpkg*.</span></span>
5. <span data-ttu-id="71a8f-133">連接到本機叢集：</span><span class="sxs-lookup"><span data-stu-id="71a8f-133">Connect to the local cluster:</span></span>
   
    ```powershell
    Connect-ServiceFabricCluster localhost:19000
    ```
6. <span data-ttu-id="71a8f-134">使用 SDK 的部署命令來建立新的應用程式，並提供應用程式套件的名稱和路徑。</span><span class="sxs-lookup"><span data-stu-id="71a8f-134">Create a new application using the SDK's deployment command with a name and a path to the application package.</span></span>
   
    ```powershell  
   Publish-NewServiceFabricApplication -ApplicationPackagePath c:\ServiceFabric\WordCountV1.sfpkg -ApplicationName "fabric:/WordCount"
    ```
   
    <span data-ttu-id="71a8f-135">如果順利執行，您應該會看到如下的輸出：</span><span class="sxs-lookup"><span data-stu-id="71a8f-135">If all goes well, you should see the following output:</span></span>
   
    ![將應用程式部署至本機叢集][deploy-app-to-local-cluster]
7. <span data-ttu-id="71a8f-137">若要查看動作中的應用程式，請啟動瀏覽器並瀏覽至 [http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html)。</span><span class="sxs-lookup"><span data-stu-id="71a8f-137">To see the application in action, launch the browser and navigate to [http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html).</span></span> <span data-ttu-id="71a8f-138">您應該會看到：</span><span class="sxs-lookup"><span data-stu-id="71a8f-138">You should see:</span></span>
   
    ![部署應用程式 UI][deployed-app-ui]
   
    <span data-ttu-id="71a8f-140">WordCount 應用程式很簡單。</span><span class="sxs-lookup"><span data-stu-id="71a8f-140">The WordCount application is simple.</span></span> <span data-ttu-id="71a8f-141">它包含的用戶端 JavaScript 程式碼可產生隨機五個字元的「單字」，這些字接著會透過 ASP.NET Web API 轉送至應用程式。</span><span class="sxs-lookup"><span data-stu-id="71a8f-141">It includes client-side JavaScript code to generate random five-character "words", which are then relayed to the application via ASP.NET Web API.</span></span> <span data-ttu-id="71a8f-142">具狀態服務會追蹤已計算的字數。</span><span class="sxs-lookup"><span data-stu-id="71a8f-142">A stateful service tracks the number of words counted.</span></span> <span data-ttu-id="71a8f-143">這些單字會根據單字的第一個字元進行分割。</span><span class="sxs-lookup"><span data-stu-id="71a8f-143">They are partitioned based on the first character of the word.</span></span> <span data-ttu-id="71a8f-144">您可以在[傳統快速入門範例](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount)中找到 WordCount 應用程式的原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="71a8f-144">You can find the source code for the WordCount app in the [classic getting started samples](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).</span></span>
   
    <span data-ttu-id="71a8f-145">我們所部署的應用程式包含四個資料分割。</span><span class="sxs-lookup"><span data-stu-id="71a8f-145">The application that we deployed contains four partitions.</span></span> <span data-ttu-id="71a8f-146">所以開頭為 A 到 G 的單字會儲存在第一個磁碟分割中，而開頭為 N 到 H 的單字會儲存在第二個資料分割中，依此類推。</span><span class="sxs-lookup"><span data-stu-id="71a8f-146">So words beginning with A through G are stored in the first partition, words beginning with H through N are stored in the second partition, and so on.</span></span>

## <a name="view-application-details-and-status"></a><span data-ttu-id="71a8f-147">檢視應用程式詳細資料和狀態</span><span class="sxs-lookup"><span data-stu-id="71a8f-147">View application details and status</span></span>
<span data-ttu-id="71a8f-148">我們現已部署應用程式，讓我們在 PowerShell 中看看一些應用程式詳細資料。</span><span class="sxs-lookup"><span data-stu-id="71a8f-148">Now that we have deployed the application, let's look at some of the app details in PowerShell.</span></span>

1. <span data-ttu-id="71a8f-149">查詢叢集上所有已部署的應用程式：</span><span class="sxs-lookup"><span data-stu-id="71a8f-149">Query all deployed applications on the cluster:</span></span>
   
    ```powershell
    Get-ServiceFabricApplication
    ```
   
    <span data-ttu-id="71a8f-150">假設您只部署 WordCount 應用程式，您會看到類似下面的內容：</span><span class="sxs-lookup"><span data-stu-id="71a8f-150">Assuming that you have only deployed the WordCount app, you see something similar to:</span></span>
   
    ![在 PowerShell 中查詢所有已部署的應用程式][ps-getsfapp]
2. <span data-ttu-id="71a8f-152">查詢 WordCount 應用程式中包含的服務集合，進而移至下一個層級。</span><span class="sxs-lookup"><span data-stu-id="71a8f-152">Go to the next level by querying the set of services that are included in the WordCount application.</span></span>
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![在 PowerShell 中列出應用程式的服務][ps-getsfsvc]
   
    <span data-ttu-id="71a8f-154">此應用程式是由兩個服務所組成：Web 前端服務以及可管理文字的具狀態服務。</span><span class="sxs-lookup"><span data-stu-id="71a8f-154">The application is made up of two services, the web front end, and the stateful service that manages the words.</span></span>
3. <span data-ttu-id="71a8f-155">最後，看看 WordCountService 的資料分割清單：</span><span class="sxs-lookup"><span data-stu-id="71a8f-155">Finally, look at the list of partitions for WordCountService:</span></span>
   
    ```powershell
    Get-ServiceFabricPartition 'fabric:/WordCount/WordCountService'
    ```
   
    ![在 PowerShell 中檢視服務資料分割][ps-getsfpartitions]
   
    <span data-ttu-id="71a8f-157">您所使用的命令集 (例如所有的 Service Fabric PowerShell 命令) 適用於任何您可能連接的叢集 (本機或遠端)。</span><span class="sxs-lookup"><span data-stu-id="71a8f-157">The set of commands that you used, like all Service Fabric PowerShell commands, are available for any cluster that you might connect to, local or remote.</span></span>
   
    <span data-ttu-id="71a8f-158">若要以更具視覺效果的方式來與叢集互動，您可以在瀏覽器中瀏覽至 [http://localhost:19080/Explorer](http://localhost:19080/Explorer) ，以使用 Web 型 Service Fabric 總管工具。</span><span class="sxs-lookup"><span data-stu-id="71a8f-158">For a more visual way to interact with the cluster, you can use the web-based Service Fabric Explorer tool by navigating to [http://localhost:19080/Explorer](http://localhost:19080/Explorer) in the browser.</span></span>
   
    ![在 Service Fabric 總管中檢視應用程式詳細資料][sfx-service-overview]
   
   > [!NOTE]
   > <span data-ttu-id="71a8f-160">若要深入了解 Service Fabric Explorer，請參閱 [使用 Service Fabric Explorer 視覺化叢集](service-fabric-visualizing-your-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="71a8f-160">To learn more about Service Fabric Explorer, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
   > 
   > 

## <a name="upgrade-an-application"></a><span data-ttu-id="71a8f-161">升級應用程式</span><span class="sxs-lookup"><span data-stu-id="71a8f-161">Upgrade an application</span></span>
<span data-ttu-id="71a8f-162">Service Fabric 會在應用程式推展於叢集時監視其健康狀態，進而提供不需停機的升級。</span><span class="sxs-lookup"><span data-stu-id="71a8f-162">Service Fabric provides no-downtime upgrades by monitoring the health of the application as it rolls out across the cluster.</span></span> <span data-ttu-id="71a8f-163">執行 WordCount 應用程式的升級。</span><span class="sxs-lookup"><span data-stu-id="71a8f-163">Perform an upgrade of the WordCount application.</span></span>

<span data-ttu-id="71a8f-164">新版的應用程式現在只會計算以母音開頭的單字。</span><span class="sxs-lookup"><span data-stu-id="71a8f-164">The new version of the application now counts only words that begin with a vowel.</span></span> <span data-ttu-id="71a8f-165">進行升級時，我們會看到應用程式的行為出現兩項變更。</span><span class="sxs-lookup"><span data-stu-id="71a8f-165">As the upgrade rolls out, we see two changes in the application's behavior.</span></span> <span data-ttu-id="71a8f-166">第一，計數成長的速率應該變慢，因為計算的單字比較少。</span><span class="sxs-lookup"><span data-stu-id="71a8f-166">First, the rate at which the count grows should slow, since fewer words are being counted.</span></span> <span data-ttu-id="71a8f-167">第二，由於第一個資料分割有兩個母音 (A 和 E)，而其他每個資料分割只包含一個母音，其計數最後應該會開始超越其他資料分割。</span><span class="sxs-lookup"><span data-stu-id="71a8f-167">Second, since the first partition has two vowels (A and E) and all other partitions contain only one each, its count should eventually start to outpace the others.</span></span>

1. <span data-ttu-id="71a8f-168">[將 WordCount 第 2 版套件下載](http://aka.ms/servicefabric-wordcountappv2) 到您下載第 1 版套件的相同位置。</span><span class="sxs-lookup"><span data-stu-id="71a8f-168">[Download the WordCount version 2 package](http://aka.ms/servicefabric-wordcountappv2) to the same location where you downloaded the version 1 package.</span></span>
2. <span data-ttu-id="71a8f-169">返回 PowerShell 視窗並使用 SDK 的升級命令在叢集中註冊新版本。</span><span class="sxs-lookup"><span data-stu-id="71a8f-169">Return to your PowerShell window and use the SDK's upgrade command to register the new version in the cluster.</span></span> <span data-ttu-id="71a8f-170">然後開始升級 fabric:/WordCount 應用程式。</span><span class="sxs-lookup"><span data-stu-id="71a8f-170">Then begin upgrading the fabric:/WordCount application.</span></span>
   
    ```powershell
    Publish-UpgradedServiceFabricApplication -ApplicationPackagePath C:\ServiceFabric\WordCountV2.sfpkg -ApplicationName "fabric:/WordCount" -UpgradeParameters @{"FailureAction"="Rollback"; "UpgradeReplicaSetCheckTimeout"=1; "Monitored"=$true; "Force"=$true}
    ```
   
    <span data-ttu-id="71a8f-171">開始升級時，您應該會在 PowerShell 中看到下列輸出。</span><span class="sxs-lookup"><span data-stu-id="71a8f-171">You should see the following output in PowerShell as the upgrade begins.</span></span>
   
    ![在 PowerShell 中的升級進度][ps-appupgradeprogress]
3. <span data-ttu-id="71a8f-173">當升級正在進行時，您可能會發現從 Service Fabric 總管監視其狀態更加輕鬆。</span><span class="sxs-lookup"><span data-stu-id="71a8f-173">While the upgrade is proceeding, you may find it easier to monitor its status from Service Fabric Explorer.</span></span> <span data-ttu-id="71a8f-174">啟動瀏覽器視窗並瀏覽至 [http://localhost:19080/Explorer](http://localhost:19080/Explorer)。</span><span class="sxs-lookup"><span data-stu-id="71a8f-174">Launch a browser window and navigate to [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="71a8f-175">展開左邊樹狀目錄中的 [應用程式]，然後選擇 [WordCount]，最後選擇 [fabric:/WordCount]。</span><span class="sxs-lookup"><span data-stu-id="71a8f-175">Expand **Applications** in the tree on the left, then choose **WordCount**, and finally **fabric:/WordCount**.</span></span> <span data-ttu-id="71a8f-176">在 [基本功能] 索引標籤中，您會在升級繼續進行叢集的升級網域時的狀態。</span><span class="sxs-lookup"><span data-stu-id="71a8f-176">In the essentials tab, you see the status of the upgrade as it proceeds through the cluster's upgrade domains.</span></span>
   
    ![在 Service Fabric 總管中的升級進度][sfx-upgradeprogress]
   
    <span data-ttu-id="71a8f-178">透過每個網域繼續升級時，系統會執行健康狀態檢查，以確保應用程式運作正常。</span><span class="sxs-lookup"><span data-stu-id="71a8f-178">As the upgrade proceeds through each domain, health checks are performed to ensure that the application is behaving properly.</span></span>
4. <span data-ttu-id="71a8f-179">如果您對 fabric:/WordCount 應用程式中的服務集合重新執行先前的查詢，請注意，雖然 WordCountService 版本已變更，但 WordCountWebService 版本維持不變：</span><span class="sxs-lookup"><span data-stu-id="71a8f-179">If you rerun the earlier query for the set of services in the fabric:/WordCount application, notice that the WordCountService version changed but the WordCountWebService version did not:</span></span>
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![在升級後查詢應用程式服務][ps-getsfsvc-postupgrade]
   
    <span data-ttu-id="71a8f-181">此範例強調 Service Fabric 如何管理應用程式升級。</span><span class="sxs-lookup"><span data-stu-id="71a8f-181">This example highlights how Service Fabric manages application upgrades.</span></span> <span data-ttu-id="71a8f-182">只會影響已變更的服務 (或這些服務中的程式碼/組態套件) 集合，讓升級程序變得更快速且更可靠。</span><span class="sxs-lookup"><span data-stu-id="71a8f-182">It touches only the set of services (or code/configuration packages within those services) that have changed, which makes the process of upgrading faster and more reliable.</span></span>
5. <span data-ttu-id="71a8f-183">最後，返回瀏覽器來觀察新應用程式版本的行為。</span><span class="sxs-lookup"><span data-stu-id="71a8f-183">Finally, return to the browser to observe the behavior of the new application version.</span></span> <span data-ttu-id="71a8f-184">如同預期，計數進度比較緩慢，而第一個磁碟分割最後會有稍微多一些的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="71a8f-184">As expected, the count progresses more slowly, and the first partition ends up with slightly more of the volume.</span></span>
   
    ![在瀏覽器中檢視新版的應用程式][deployed-app-ui-v2]

## <a name="cleaning-up"></a><span data-ttu-id="71a8f-186">清除</span><span class="sxs-lookup"><span data-stu-id="71a8f-186">Cleaning up</span></span>
<span data-ttu-id="71a8f-187">在我們做結論之前，請務必記得本機叢集是真實的。</span><span class="sxs-lookup"><span data-stu-id="71a8f-187">Before wrapping up, it's important to remember that the local cluster is real.</span></span> <span data-ttu-id="71a8f-188">應用程式會繼續在背景中執行，直到您將它們移除。</span><span class="sxs-lookup"><span data-stu-id="71a8f-188">Applications continue to run in the background until you remove them.</span></span>  <span data-ttu-id="71a8f-189">視應用程式的本質而定，執行中應用程式可能會佔用您電腦上的大量資源。</span><span class="sxs-lookup"><span data-stu-id="71a8f-189">Depending on the nature of your apps, a running app can take up significant resources on your machine.</span></span> <span data-ttu-id="71a8f-190">您有數個選項可管理應用程式和叢集：</span><span class="sxs-lookup"><span data-stu-id="71a8f-190">You have several options to manage applications and the cluster:</span></span>

1. <span data-ttu-id="71a8f-191">若要移除個別應用程式及其所有資料，請執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="71a8f-191">To remove an individual application and all it's data, run the following command:</span></span>
   
    ```powershell
    Unpublish-ServiceFabricApplication -ApplicationName "fabric:/WordCount"
    ```
   
    <span data-ttu-id="71a8f-192">或者，從 Service Fabric Explorer 的 [動作] 功能表或左窗格中應用程式清單檢視的內容功能表來刪除應用程式。</span><span class="sxs-lookup"><span data-stu-id="71a8f-192">Or, delete the application from the Service Fabric Explorer **ACTIONS** menu or the context menu in the left-hand application list view.</span></span>
   
    ![在 Service Fabric 總管中刪除應用程式][sfe-delete-application]
2. <span data-ttu-id="71a8f-194">在叢集中刪除應用程式之後，將 WordCount 應用程式類型的 1.0.0 和 2.0.0 版取消註冊。</span><span class="sxs-lookup"><span data-stu-id="71a8f-194">After deleting the application from the cluster, unregister versions 1.0.0 and 2.0.0 of the WordCount application type.</span></span> <span data-ttu-id="71a8f-195">刪除作業會從叢集的映像存放區中移除應用程式套件，包括程式碼和設定。</span><span class="sxs-lookup"><span data-stu-id="71a8f-195">Deletion removes the application packages, including the code and configuration, from the cluster's image store.</span></span>
   
    ```powershell
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 2.0.0
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 1.0.0
    ```
   
    <span data-ttu-id="71a8f-196">或者，在 Service Fabric Explorer 中為應用程式選擇 [解除佈建類型]  。</span><span class="sxs-lookup"><span data-stu-id="71a8f-196">Or, in Service Fabric Explorer, choose **Unprovision Type** for the application.</span></span>
3. <span data-ttu-id="71a8f-197">若要關閉叢集，但保留應用程式資料及追蹤，請按一下系統匣應用程式中的 [停止本機叢集]  。</span><span class="sxs-lookup"><span data-stu-id="71a8f-197">To shut down the cluster but keep the application data and traces, click **Stop Local Cluster** in the system tray app.</span></span>
4. <span data-ttu-id="71a8f-198">若要完全刪除叢集，請按一下系統匣應用程式中的 [移除本機叢集]  。</span><span class="sxs-lookup"><span data-stu-id="71a8f-198">To delete the cluster entirely, click **Remove Local Cluster** in the system tray app.</span></span> <span data-ttu-id="71a8f-199">此選項會導致下次您在 Visual Studio 中按 F5 鍵時發生其他緩慢部署。</span><span class="sxs-lookup"><span data-stu-id="71a8f-199">This option will result in another slow deployment the next time you press F5 in Visual Studio.</span></span> <span data-ttu-id="71a8f-200">只有在您計劃一陣子不使用本機叢集或者需要回收資源時，才將本機叢集移除。</span><span class="sxs-lookup"><span data-stu-id="71a8f-200">Remove the local cluster only if you don't intend to use it for some time or if you need to reclaim resources.</span></span>

## <a name="one-node-and-five-node-cluster-mode"></a><span data-ttu-id="71a8f-201">1 個節點和 5 個節點叢集模式</span><span class="sxs-lookup"><span data-stu-id="71a8f-201">One-node and five-node cluster mode</span></span>
<span data-ttu-id="71a8f-202">開發應用程式時，您常會發現自己快速反覆撰寫程式碼、偵錯、變更程式碼和偵錯。</span><span class="sxs-lookup"><span data-stu-id="71a8f-202">When developing applications, you often find yourself doing quick iterations of writing code, debugging, changing code, and debugging.</span></span> <span data-ttu-id="71a8f-203">為了協助最佳化這個程序，本機叢集可以用兩種模式執行︰1 個節點或 5 節點。</span><span class="sxs-lookup"><span data-stu-id="71a8f-203">To help optimize this process, the local cluster can run in two modes: one-node or five-node.</span></span> <span data-ttu-id="71a8f-204">這兩個叢集模式各有優點。</span><span class="sxs-lookup"><span data-stu-id="71a8f-204">Both cluster modes have their benefits.</span></span> <span data-ttu-id="71a8f-205">5 個節點叢集模式可讓您使用實際的叢集。</span><span class="sxs-lookup"><span data-stu-id="71a8f-205">Five-node cluster mode enables you to work with a real cluster.</span></span> <span data-ttu-id="71a8f-206">您可以測試容錯移轉案例，使用更多您的服務的執行個體和複本。</span><span class="sxs-lookup"><span data-stu-id="71a8f-206">You can test failover scenarios, work with more instances and replicas of your services.</span></span> <span data-ttu-id="71a8f-207">1 個節點叢集模式已最佳化，可進行服務的快速部署和註冊，進而協助您使用 Service Fabric 執行階段快速驗證程式碼。</span><span class="sxs-lookup"><span data-stu-id="71a8f-207">One-node cluster mode is optimized to do quick deployment and registration of services, to help you quickly validate code using the Service Fabric runtime.</span></span>

<span data-ttu-id="71a8f-208">1 個節點叢集或 5 個節點叢集模式皆不是模擬器。</span><span class="sxs-lookup"><span data-stu-id="71a8f-208">Neither one-node cluster or five-node cluster modes are an emulator or simulator.</span></span> <span data-ttu-id="71a8f-209">本機開發叢集會執行在多部電腦的叢集上找到的相同平台程式碼。</span><span class="sxs-lookup"><span data-stu-id="71a8f-209">The local development cluster runs the same platform code that is found on multi-machine clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="71a8f-210">變更叢集模式時，目前的叢集會從您的系統移除，而建立新的叢集。</span><span class="sxs-lookup"><span data-stu-id="71a8f-210">When you change the cluster mode, the current cluster is removed from your system and a new cluster is created.</span></span> <span data-ttu-id="71a8f-211">當您變更叢集模式時，在叢集中儲存的資料會遭到刪除。</span><span class="sxs-lookup"><span data-stu-id="71a8f-211">The data stored in the cluster is deleted when you change cluster mode.</span></span>
> 
> 

<span data-ttu-id="71a8f-212">若要將模式變更為 1 個節點叢集，請選取 Service Fabric 本機叢集管理員中的**交換器叢集模式**。</span><span class="sxs-lookup"><span data-stu-id="71a8f-212">To change the mode to one-node cluster, select **Switch Cluster Mode** in the Service Fabric Local Cluster Manager.</span></span>

![切換叢集模式][switch-cluster-mode]

<span data-ttu-id="71a8f-214">或者，您也可以使用 PowerShell 變更叢集模式︰</span><span class="sxs-lookup"><span data-stu-id="71a8f-214">Or, change the cluster mode using PowerShell:</span></span>

1. <span data-ttu-id="71a8f-215">以系統管理員身分啟動新的 PowerShell 視窗。</span><span class="sxs-lookup"><span data-stu-id="71a8f-215">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="71a8f-216">從 SDK 資料夾執行叢集設定指令碼：</span><span class="sxs-lookup"><span data-stu-id="71a8f-216">Run the cluster setup script from the SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1" -CreateOneNodeCluster
    ```
   
    <span data-ttu-id="71a8f-217">叢集設定需要一些時間。</span><span class="sxs-lookup"><span data-stu-id="71a8f-217">Cluster setup takes a few moments.</span></span> <span data-ttu-id="71a8f-218">設定完成後，您應該會看到輸出類似於：</span><span class="sxs-lookup"><span data-stu-id="71a8f-218">After setup is finished, you should see output similar to:</span></span>
   
    ![叢集設定輸出][cluster-setup-success-1-node]

## <a name="next-steps"></a><span data-ttu-id="71a8f-220">後續步驟</span><span class="sxs-lookup"><span data-stu-id="71a8f-220">Next steps</span></span>
* <span data-ttu-id="71a8f-221">您現在已部署並升級某些預先建置的應用程式，您可以 [嘗試在 Visual Studio 中建立自己的應用程式](service-fabric-create-your-first-application-in-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="71a8f-221">Now that you have deployed and upgraded some pre-built applications, you can [try building your own in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span>
* <span data-ttu-id="71a8f-222">本文中在本機叢集上執行的所有動作也可以在 [Azure 叢集](service-fabric-cluster-creation-via-portal.md) 上執行。</span><span class="sxs-lookup"><span data-stu-id="71a8f-222">All the actions performed on the local cluster in this article can be performed on an [Azure cluster](service-fabric-cluster-creation-via-portal.md) as well.</span></span>
* <span data-ttu-id="71a8f-223">本文中執行的是基本升級。</span><span class="sxs-lookup"><span data-stu-id="71a8f-223">The upgrade that we performed in this article was basic.</span></span> <span data-ttu-id="71a8f-224">若要深入了解 Service Fabric 升級的功用和彈性，請參閱 [升級文件](service-fabric-application-upgrade.md) 。</span><span class="sxs-lookup"><span data-stu-id="71a8f-224">See the [upgrade documentation](service-fabric-application-upgrade.md) to learn more about the power and flexibility of Service Fabric upgrades.</span></span>

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
