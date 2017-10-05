---
title: "建立獨立 Azure Service Fabric 叢集 | Microsoft Docs"
description: "在執行 Windows Server (無論是在內部部署或任何雲端) 的任何電腦 (實體或虛擬) 上建立 Azure Service Fabric 叢集。"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 31349169-de19-4be6-8742-ca20ac41eb9e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/10/2017
ms.author: chackdan;maburlik;dekapur
ms.openlocfilehash: 6aa2905a97ec6b8c125f2ab9572a8e40bf525b27
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-standalone-cluster-running-on-windows-server"></a><span data-ttu-id="c6c4b-103">建立在 Windows Server 上執行的獨立叢集</span><span class="sxs-lookup"><span data-stu-id="c6c4b-103">Create a standalone cluster running on Windows Server</span></span>
<span data-ttu-id="c6c4b-104">您可以使用 Azure Service Fabric 在執行 Windows Server 的任何虛擬機器或電腦上建立 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-104">You can use Azure Service Fabric to create Service Fabric clusters on any virtual machines or computers running Windows Server.</span></span> <span data-ttu-id="c6c4b-105">這表示您能夠在包含一組互連式 Windows Server 電腦的任何環境中部署和執行 Service Fabric 應用程式，不論該環境是內部部署或是透過任何雲端提供者來提供。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-105">This means you can deploy and run Service Fabric applications in any environment that contains a set of interconnected Windows Server computers, be it on premises or with any cloud provider.</span></span> <span data-ttu-id="c6c4b-106">Service Fabric 會提供一個安裝封裝來建立稱為獨立 Windows Server 封裝的 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-106">Service Fabric provides a setup package to create Service Fabric clusters called the standalone Windows Server package.</span></span>

<span data-ttu-id="c6c4b-107">本文將逐步引導您完成建立 Service Fabric 獨立叢集的步驟。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-107">This article walks you through the steps for creating a Service Fabric standalone cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="c6c4b-108">此獨立 Windows Server 套件已正式上市，可使用於生產部署。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-108">This standalone Windows Server package is commercially available and may be used for production deployments.</span></span> <span data-ttu-id="c6c4b-109">此套件包含處於「預覽」狀態的新 Service Fabric 功能。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-109">This package may contain new Service Fabric features that are in "Preview".</span></span> <span data-ttu-id="c6c4b-110">捲動至「[此封裝包含的預覽功能](#previewfeatures_anchor)」。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-110">Scroll down to "[Preview features included in this package](#previewfeatures_anchor)."</span></span> <span data-ttu-id="c6c4b-111">區段，以取得預覽功能的清單。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-111">section for the list of the preview features.</span></span> <span data-ttu-id="c6c4b-112">您可以立即[下載一份 EULA](http://go.microsoft.com/fwlink/?LinkID=733084)。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-112">You can [download a copy of the EULA](http://go.microsoft.com/fwlink/?LinkID=733084) now.</span></span>
> 
> 

<a id="getsupport"></a>

## <a name="get-support-for-the-service-fabric-for-windows-server-package"></a><span data-ttu-id="c6c4b-113">取得 Windows Server 套件的 Service Fabric 支援</span><span class="sxs-lookup"><span data-stu-id="c6c4b-113">Get support for the Service Fabric for Windows Server package</span></span>
* <span data-ttu-id="c6c4b-114">請至 [Azure Service Fabric 論壇](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?)，向社群發問有關 Windows Server 的 Service Fabric 獨立封裝。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-114">Ask the community about the Service Fabric standalone package for Windows Server in the [Azure Service Fabric forum](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span></span>
* <span data-ttu-id="c6c4b-115">向 [Service Fabric 的專業支援](http://support.microsoft.com/oas/default.aspx?prid=16146)開立票證。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-115">Open a ticket for [Professional Support for Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).</span></span>  <span data-ttu-id="c6c4b-116">[在這裡](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0)深入了解 Microsoft 的專業支援。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-116">Learn more about Professional Support from Microsoft [here](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span></span>
* <span data-ttu-id="c6c4b-117">您也可以取得此封裝的支援做為 [Microsoft 頂級支援](https://support.microsoft.com/en-us/premier)的一部分。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-117">You can also get support for this package as a part of [Microsoft Premier Support](https://support.microsoft.com/en-us/premier).</span></span>
* <span data-ttu-id="c6c4b-118">如需詳細資訊，請參閱 [Azure Service Fabric 支援選項](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support)。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-118">For more details, please see [Azure Service Fabric support options](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span></span>
* <span data-ttu-id="c6c4b-119">若要針對支援用途收集記錄，請執行 [Service Fabric 獨立記錄收集器](service-fabric-cluster-standalone-package-contents.md)。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-119">To collect logs for support purposes, run the [Service Fabric Standalone Log collector](service-fabric-cluster-standalone-package-contents.md).</span></span>

<a id="downloadpackage"></a>

## <a name="download-the-service-fabric-for-windows-server-package"></a><span data-ttu-id="c6c4b-120">下載 Windows Server 套件的 Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c6c4b-120">Download the Service Fabric for Windows Server package</span></span>
<span data-ttu-id="c6c4b-121">若要建立叢集，請使用適用於 Windows Server 套件 (Windows Server 2012 R2 及更新版本) 的 Service Fabric，可在這裡找到︰</span><span class="sxs-lookup"><span data-stu-id="c6c4b-121">To create the cluster, use the Service Fabric for Windows Server package (Windows Server 2012 R2 and newer) found here:</span></span> <br><span data-ttu-id="c6c4b-122">
[下載連結 - Service Fabric 獨立封裝 - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)</span><span class="sxs-lookup"><span data-stu-id="c6c4b-122">
[Download Link - Service Fabric Standalone Package - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)</span></span>

<span data-ttu-id="c6c4b-123">可在[這裡](service-fabric-cluster-standalone-package-contents.md)找到封裝內容的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-123">Find details on contents of the package [here](service-fabric-cluster-standalone-package-contents.md).</span></span>

<span data-ttu-id="c6c4b-124">叢集建立時會自動下載 Service Fabric 執行階段封裝。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-124">The Service Fabric runtime package is automatically downloaded at time of cluster creation.</span></span> <span data-ttu-id="c6c4b-125">如果從未連線到網際網路的機器部署，請從這裡下載頻外執行階段封裝︰</span><span class="sxs-lookup"><span data-stu-id="c6c4b-125">If deploying from a machine not connected to the internet, please download the runtime package out of band from here:</span></span> <br><span data-ttu-id="c6c4b-126">
[下載連結 - Service Fabric 執行階段 - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)</span><span class="sxs-lookup"><span data-stu-id="c6c4b-126">
[Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)</span></span>

<span data-ttu-id="c6c4b-127">獨立叢集組態範例在此︰</span><span class="sxs-lookup"><span data-stu-id="c6c4b-127">Find Standalone Cluster Configuration samples at:</span></span> <br><span data-ttu-id="c6c4b-128">
[獨立叢集組態範例](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span><span class="sxs-lookup"><span data-stu-id="c6c4b-128">
[Standalone Cluster Configuration Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span></span>

<a id="createcluster"></a>

## <a name="create-the-cluster"></a><span data-ttu-id="c6c4b-129">建立叢集</span><span class="sxs-lookup"><span data-stu-id="c6c4b-129">Create the cluster</span></span>
<span data-ttu-id="c6c4b-130">Service Fabric 可以使用[範例](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)中所含的 *ClusterConfig.Unsecure.DevCluster.json* 檔案，部署到一個電腦開發叢集。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-130">Service Fabric can be deployed to a one-machine development cluster by using the *ClusterConfig.Unsecure.DevCluster.json* file included in [Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span></span>

<span data-ttu-id="c6c4b-131">將獨立封裝解除封裝到電腦，將範例組態檔複製到本機電腦，然後從獨立套件資料夾，透過系統管理員 PowerShell 工作階段，執行 *CreateServiceFabricCluster.ps1* 指令碼︰</span><span class="sxs-lookup"><span data-stu-id="c6c4b-131">Unpack the standalone package to your machine, copy the sample config file to the local machine, then run the *CreateServiceFabricCluster.ps1* script through an administrator PowerShell session, from the standalone package folder:</span></span>
### <a name="step-1a-create-an-unsecured-local-development-cluster"></a><span data-ttu-id="c6c4b-132">步驟 1A：建立不安全的本機開發叢集</span><span class="sxs-lookup"><span data-stu-id="c6c4b-132">Step 1A: Create an unsecured local development cluster</span></span>
```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

<span data-ttu-id="c6c4b-133">如需疑難排解的詳細資料，請參閱[規劃及準備叢集部署](service-fabric-cluster-standalone-deployment-preparation.md)的「環境設定」一節。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-133">See the Environment Setup section at [Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md) for troubleshooting details.</span></span>

<span data-ttu-id="c6c4b-134">如果您完成執行開發案例，您可以參閱「[移除叢集](#removecluster_anchor)」一節中的步驟，從電腦中移除 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-134">If you're finished running development scenarios, you can remove the Service Fabric cluster from the machine by referring to steps in section "[Remove a cluster](#removecluster_anchor)".</span></span> 

### <a name="step-1b-create-a-multi-machine-cluster"></a><span data-ttu-id="c6c4b-135">步驟 1B︰ 建立多部電腦的叢集</span><span class="sxs-lookup"><span data-stu-id="c6c4b-135">Step 1B: Create a multi-machine cluster</span></span>
<span data-ttu-id="c6c4b-136">在您完成規劃和準備下面連結詳細列出的步驟之後，就可以開始使用您的叢集組態檔，建立生產叢集。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-136">After you have gone through the planning and preparation steps detailed at the below link, you are ready to create your production cluster using your cluster configuration file.</span></span> <br><span data-ttu-id="c6c4b-137">
[規劃及準備叢集部署](service-fabric-cluster-standalone-deployment-preparation.md)</span><span class="sxs-lookup"><span data-stu-id="c6c4b-137">
[Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md)</span></span>

1. <span data-ttu-id="c6c4b-138">從獨立封裝資料夾執行 *TestConfiguration.ps1* 指令碼，驗證您所撰寫的組態檔︰</span><span class="sxs-lookup"><span data-stu-id="c6c4b-138">Validate the configuration file you have written by running the *TestConfiguration.ps1* script from the standalone package folder:</span></span>  

    ```powershell
    .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.json
    ```

    <span data-ttu-id="c6c4b-139">您應該會看到如下的輸出：</span><span class="sxs-lookup"><span data-stu-id="c6c4b-139">You should see output like below.</span></span> <span data-ttu-id="c6c4b-140">如果底層欄位 "Passed" 傳回為 "True"，表示已通過例行性檢查，並可根據輸入組態來部署該叢集。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-140">If the bottom field "Passed" is returned as "True", sanity checks have passed and the cluster looks to be deployable based on the input configuration.</span></span>

    ```
    Trace folder already exists. Traces will be written to existing trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
    Running Best Practices Analyzer...
    Best Practices Analyzer completed successfully.
    
    LocalAdminPrivilege        : True
    IsJsonValid                : True
    IsCabValid                 : True
    RequiredPortsOpen          : True
    RemoteRegistryAvailable    : True
    FirewallAvailable          : True
    RpcCheckPassed             : True
    NoConflictingInstallations : True
    FabricInstallable          : True
    Passed                     : True
    ```

2. <span data-ttu-id="c6c4b-141">建立叢集︰執行 *CreateServiceFabricCluster.ps1* 指令碼，以跨組態中的每一部機器部署 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-141">Create the cluster:  Run the *CreateServiceFabricCluster.ps1* script to deploy the Service Fabric cluster across each machine in the configuration.</span></span> 
    ```powershell
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -AcceptEULA
    ```

> [!NOTE]
> <span data-ttu-id="c6c4b-142">部署追蹤會寫入您可以執行 CreateServiceFabricCluster.ps1 PowerShell 指令碼的 VM/電腦。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-142">Deployment traces are written to the VM/machine on which you ran the CreateServiceFabricCluster.ps1 PowerShell script.</span></span> <span data-ttu-id="c6c4b-143">這些可以根據指令碼執行的目錄，在其子資料夾 DeploymentTraces 中找到。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-143">These can be found in the subfolder DeploymentTraces, based in the directory from which the script was run.</span></span> <span data-ttu-id="c6c4b-144">若要查看是否已正確將 Service Fabric 部署到電腦，請在 FabricDataRoot 目錄中找到安裝的檔案，如叢集組態檔的 FabricSettings 區段 (預設為 c:\ProgramData\SF) 中所述。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-144">To see if Service Fabric was deployed correctly to a machine, find the installed files in the FabricDataRoot directory, as detailed in the cluster configuration file FabricSettings section (by default c:\ProgramData\SF).</span></span> <span data-ttu-id="c6c4b-145">同時，也要能在 [工作管理員] 看到 FabricHost.exe 和 Fabric.exe 處理序正在執行中。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-145">As well, FabricHost.exe and Fabric.exe processes can be seen running in Task Manager.</span></span>
> 
> 

### <a name="step-1c-create-an-offline-internet-disconnected-cluster"></a><span data-ttu-id="c6c4b-146">步驟 1 C：建立離線 (網際網路中斷連線的) 叢集</span><span class="sxs-lookup"><span data-stu-id="c6c4b-146">Step 1C: Create an offline (internet-disconnected) cluster</span></span>
<span data-ttu-id="c6c4b-147">叢集建立時會自動下載 Service Fabric 執行階段套件。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-147">The Service Fabric runtime package is automatically downloaded at cluster creation.</span></span> <span data-ttu-id="c6c4b-148">將叢集部署到未連線到網際網路的電腦時，您必須另外下載 Service Fabric 執行階段套件，並在建立叢集時提供指向它的路徑。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-148">When deploying a cluster to machines not connected to the internet, you will need to download the Service Fabric runtime package separately, and provide the path to it at cluster creation.</span></span>
<span data-ttu-id="c6c4b-149">可以從另一部有連線到網際網路電腦，到[下載連結 - Service Fabric 執行階段 - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354) 另外下載執行階段套件。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-149">The runtime package can be downloaded separately, from another machine connected to the internet, at [Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span></span> <span data-ttu-id="c6c4b-150">將執行階段套件複製到您要部署離線叢集之處，然後執行 `CreateServiceFabricCluster.ps1` 搭配 `-FabricRuntimePackagePath` 參數建立叢集，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c6c4b-150">Copy the runtime package to where you are deploying the offline cluster from, and create the cluster by running `CreateServiceFabricCluster.ps1` with the `-FabricRuntimePackagePath` parameter included, as shown below:</span></span> 

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -FabricRuntimePackagePath .\MicrosoftAzureServiceFabric.cab
```
<span data-ttu-id="c6c4b-151">其中 `.\ClusterConfig.json` 和 `.\MicrosoftAzureServiceFabric.cab` 分別為叢集設定與執行階段 .cab 檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-151">where `.\ClusterConfig.json` and `.\MicrosoftAzureServiceFabric.cab` are the paths to the cluster configuration and the runtime .cab file respectively.</span></span>


### <a name="step-2-connect-to-the-cluster"></a><span data-ttu-id="c6c4b-152">步驟 2：連接到叢集</span><span class="sxs-lookup"><span data-stu-id="c6c4b-152">Step 2: Connect to the cluster</span></span>
<span data-ttu-id="c6c4b-153">若要連接至安全的叢集，請參閱 [Service Fabric 連線到安全的叢集](service-fabric-connect-to-secure-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-153">To connect to a secure cluster, see [Service fabric connect to secure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="c6c4b-154">若要連線到不安全的叢集，請執行下列 PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="c6c4b-154">To connect to an unsecure cluster, run the following PowerShell command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <*IPAddressofaMachine*>:<Client connection end point port>
```
<span data-ttu-id="c6c4b-155">範例：</span><span class="sxs-lookup"><span data-stu-id="c6c4b-155">Example:</span></span>
```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint 192.13.123.2345:19000
```
### <a name="step-3-bring-up-service-fabric-explorer"></a><span data-ttu-id="c6c4b-156">步驟 3：啟動 Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="c6c4b-156">Step 3: Bring up Service Fabric Explorer</span></span>
<span data-ttu-id="c6c4b-157">現在，您可以使用 http://localhost:19080/Explorer/index.html 直接從其中一部電腦或使用 http://<*IPAddressofaMachine*>:19080/Explorer/index.html 從遠端利用 Service Fabric Explorer 連接到叢集。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-157">Now you can connect to the cluster with Service Fabric Explorer either directly from one of the machines with http://localhost:19080/Explorer/index.html or remotely with http://<*IPAddressofaMachine*>:19080/Explorer/index.html.</span></span>

## <a name="add-and-remove-nodes"></a><span data-ttu-id="c6c4b-158">新增和移除節點</span><span class="sxs-lookup"><span data-stu-id="c6c4b-158">Add and remove nodes</span></span>
<span data-ttu-id="c6c4b-159">當您的商務需求改變時，您可以在獨立 Service Fabric 叢集中新增或移除節點。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-159">You can add or remove nodes to your standalone Service Fabric cluster as your business needs change.</span></span> <span data-ttu-id="c6c4b-160">如需詳細步驟，請參閱[在 Service Fabric 獨立叢集中新增或移除節點](service-fabric-cluster-windows-server-add-remove-nodes.md)。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-160">See [Add or Remove nodes to a Service Fabric standalone cluster](service-fabric-cluster-windows-server-add-remove-nodes.md) for detailed steps.</span></span>

<a id="removecluster" name="removecluster_anchor"></a>
## <a name="remove-a-cluster"></a><span data-ttu-id="c6c4b-161">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="c6c4b-161">Remove a cluster</span></span>
<span data-ttu-id="c6c4b-162">若要移除叢集，請從封裝資料夾執行 *RemoveServiceFabricCluster.ps1* PowerShell 指令碼，然後傳入 JSON 組態檔的路徑。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-162">To remove a cluster, run the *RemoveServiceFabricCluster.ps1* PowerShell script from the package folder and pass in the path to the JSON configuration file.</span></span> <span data-ttu-id="c6c4b-163">您可以選擇指定刪除作業的記錄檔位置。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-163">You can optionally specify a location for the log of the deletion.</span></span>

<span data-ttu-id="c6c4b-164">此指令碼可以在以系統管理員身分存取叢集組態檔中列為節點的所有電腦的任何電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-164">This script can be run on any machine that has administrator access to all the machines that are listed as nodes in the cluster configuration file.</span></span> <span data-ttu-id="c6c4b-165">執行此指令碼所在的電腦不一定是叢集的一部分。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-165">The machine that this script is run on does not have to be part of the cluster.</span></span>

```
# Removes Service Fabric from each machine in the configuration
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -Force
```

```
# Removes Service Fabric from the current machine
.\CleanFabric.ps1
```

<a id="telemetry"></a>

## <a name="telemetry-data-collected-and-how-to-opt-out-of-it"></a><span data-ttu-id="c6c4b-166">收集的遙測資料及如何選擇退出</span><span class="sxs-lookup"><span data-stu-id="c6c4b-166">Telemetry data collected and how to opt out of it</span></span>
<span data-ttu-id="c6c4b-167">根據預設，產品會收集 Service Fabric 使用情形的遙測來改善產品。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-167">As a default, the product collects telemetry on the Service Fabric usage to improve the product.</span></span> <span data-ttu-id="c6c4b-168">安裝過程執行的最佳做法分析會檢查能否連線到 [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1)。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-168">The Best Practice Analyzer that runs as a part of the setup checks for connectivity to [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span></span> <span data-ttu-id="c6c4b-169">如果無法連線，則安裝會失敗，除非您選擇退出遙測。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-169">If it is not reachable, the setup fails unless you opt out of telemetry.</span></span>

1. <span data-ttu-id="c6c4b-170">遙測管線會嘗試將下列資料每天上傳一次到 [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1)。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-170">The telemetry pipeline tries to upload the following data to [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) once every day.</span></span> <span data-ttu-id="c6c4b-171">這只是儘可能上傳，不會影響叢集功能。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-171">It is a best-effort upload and has no impact on the cluster functionality.</span></span> <span data-ttu-id="c6c4b-172">只有執行主要容錯移轉管理員的節點才會傳送遙測。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-172">The telemetry is only sent from the node that runs the failover manager primary.</span></span> <span data-ttu-id="c6c4b-173">沒有其他節點會傳送遙測。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-173">No other nodes send out telemetry.</span></span>
2. <span data-ttu-id="c6c4b-174">遙測是由下列項目所組成：</span><span class="sxs-lookup"><span data-stu-id="c6c4b-174">The telemetry consists of the following:</span></span>

* <span data-ttu-id="c6c4b-175">服務數</span><span class="sxs-lookup"><span data-stu-id="c6c4b-175">Number of services</span></span>
* <span data-ttu-id="c6c4b-176">ServiceTypes 數目</span><span class="sxs-lookup"><span data-stu-id="c6c4b-176">Number of ServiceTypes</span></span>
* <span data-ttu-id="c6c4b-177">Applications 的數目</span><span class="sxs-lookup"><span data-stu-id="c6c4b-177">Number of Applications</span></span>
* <span data-ttu-id="c6c4b-178">ApplicationUpgrades 的數目</span><span class="sxs-lookup"><span data-stu-id="c6c4b-178">Number of ApplicationUpgrades</span></span>
* <span data-ttu-id="c6c4b-179">FailoverUnits 的數目</span><span class="sxs-lookup"><span data-stu-id="c6c4b-179">Number of FailoverUnits</span></span>
* <span data-ttu-id="c6c4b-180">InBuildFailoverUnits 的數目</span><span class="sxs-lookup"><span data-stu-id="c6c4b-180">Number of InBuildFailoverUnits</span></span>
* <span data-ttu-id="c6c4b-181">UnhealthyFailoverUnits 的數目</span><span class="sxs-lookup"><span data-stu-id="c6c4b-181">Number of UnhealthyFailoverUnits</span></span>
* <span data-ttu-id="c6c4b-182">Replicas 的數目</span><span class="sxs-lookup"><span data-stu-id="c6c4b-182">Number of Replicas</span></span>
* <span data-ttu-id="c6c4b-183">InBuildReplicas 的數目</span><span class="sxs-lookup"><span data-stu-id="c6c4b-183">Number of InBuildReplicas</span></span>
* <span data-ttu-id="c6c4b-184">StandByReplicas 的數目</span><span class="sxs-lookup"><span data-stu-id="c6c4b-184">Number of StandByReplicas</span></span>
* <span data-ttu-id="c6c4b-185">OfflineReplicas 的數目</span><span class="sxs-lookup"><span data-stu-id="c6c4b-185">Number of OfflineReplicas</span></span>
* <span data-ttu-id="c6c4b-186">CommonQueueLength</span><span class="sxs-lookup"><span data-stu-id="c6c4b-186">CommonQueueLength</span></span>
* <span data-ttu-id="c6c4b-187">QueryQueueLength</span><span class="sxs-lookup"><span data-stu-id="c6c4b-187">QueryQueueLength</span></span>
* <span data-ttu-id="c6c4b-188">FailoverUnitQueueLength</span><span class="sxs-lookup"><span data-stu-id="c6c4b-188">FailoverUnitQueueLength</span></span>
* <span data-ttu-id="c6c4b-189">CommitQueueLength</span><span class="sxs-lookup"><span data-stu-id="c6c4b-189">CommitQueueLength</span></span>
* <span data-ttu-id="c6c4b-190">Nodes 的數目</span><span class="sxs-lookup"><span data-stu-id="c6c4b-190">Number of Nodes</span></span>
* <span data-ttu-id="c6c4b-191">IsContextComplete: True/False</span><span class="sxs-lookup"><span data-stu-id="c6c4b-191">IsContextComplete: True/False</span></span>
* <span data-ttu-id="c6c4b-192">ClusterId︰這是針對每個叢集隨機產生的 GUID。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-192">ClusterId: This is a GUID randomly generated for each cluster</span></span>
* <span data-ttu-id="c6c4b-193">ServiceFabricVersion</span><span class="sxs-lookup"><span data-stu-id="c6c4b-193">ServiceFabricVersion</span></span>
* <span data-ttu-id="c6c4b-194">遙測上傳來源虛擬機器的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="c6c4b-194">IP address of the virtual machine or machine from which the telemetry is uploaded</span></span>

<span data-ttu-id="c6c4b-195">若要停用遙測，請將下列命令新增至叢集組態中的 *properties*：*enableTelemetry: false*。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-195">To disable telemetry, add the following to *properties* in your cluster config: *enableTelemetry: false*.</span></span>

<a id="previewfeatures" name="previewfeatures_anchor"></a>

## <a name="preview-features-included-in-this-package"></a><span data-ttu-id="c6c4b-196">此封裝包含的預覽功能</span><span class="sxs-lookup"><span data-stu-id="c6c4b-196">Preview features included in this package</span></span>
<span data-ttu-id="c6c4b-197">無。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-197">None.</span></span>


> [!NOTE]
> <span data-ttu-id="c6c4b-198">從[適用於 Windows Server 的獨立叢集 GA 新版本 (5.3.204.x 版)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/)著手，您可以手動或自動將叢集升級至未來的版本。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-198">Starting with the new [GA version of the standalone cluster for Windows Server (version 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), you can upgrade your cluster to future releases, manually or automatically.</span></span> <span data-ttu-id="c6c4b-199">請參閱[獨立 Service Fabric 叢集版本升級](service-fabric-cluster-upgrade-windows-server.md)文件，以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="c6c4b-199">Refer to [Upgrade a standalone Service Fabric cluster version](service-fabric-cluster-upgrade-windows-server.md) document for details.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="c6c4b-200">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c6c4b-200">Next steps</span></span>
* [<span data-ttu-id="c6c4b-201">使用 PowerShell 部署與移除應用程式</span><span class="sxs-lookup"><span data-stu-id="c6c4b-201">Deploy and remove applications using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="c6c4b-202">獨立 Windows 叢集的組態設定</span><span class="sxs-lookup"><span data-stu-id="c6c4b-202">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="c6c4b-203">在獨立 Service Fabric 叢集中新增或移除節點</span><span class="sxs-lookup"><span data-stu-id="c6c4b-203">Add or remove nodes to a standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="c6c4b-204">獨立 Service Fabric 叢集版本升級</span><span class="sxs-lookup"><span data-stu-id="c6c4b-204">Upgrade a standalone Service Fabric cluster version</span></span>](service-fabric-cluster-upgrade-windows-server.md)
* [<span data-ttu-id="c6c4b-205">建立具有執行 Windows 之 Azure VM 的獨立 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="c6c4b-205">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)
* [<span data-ttu-id="c6c4b-206">使用 Windows 安全性保護 Windows 上的獨立叢集</span><span class="sxs-lookup"><span data-stu-id="c6c4b-206">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="c6c4b-207">使用 X509 憑證保護 Windows 上的獨立叢集</span><span class="sxs-lookup"><span data-stu-id="c6c4b-207">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

<!--Image references-->
[Trusted Zone]: ./media/service-fabric-cluster-creation-for-windows-server/TrustedZone.png
