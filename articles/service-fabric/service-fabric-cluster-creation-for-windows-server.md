---
title: "aaaCreate 獨立 Azure Service Fabric 叢集 |Microsoft 文件"
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
ms.openlocfilehash: 444970816290a0448d88a8b2082c75eb7a64cb44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-standalone-cluster-running-on-windows-server"></a><span data-ttu-id="7ff57-103">建立在 Windows Server 上執行的獨立叢集</span><span class="sxs-lookup"><span data-stu-id="7ff57-103">Create a standalone cluster running on Windows Server</span></span>
<span data-ttu-id="7ff57-104">您可以在任何虛擬機器或執行 Windows Server 的電腦上使用 Azure Service Fabric toocreate Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="7ff57-104">You can use Azure Service Fabric toocreate Service Fabric clusters on any virtual machines or computers running Windows Server.</span></span> <span data-ttu-id="7ff57-105">這表示您能夠在包含一組互連式 Windows Server 電腦的任何環境中部署和執行 Service Fabric 應用程式，不論該環境是內部部署或是透過任何雲端提供者來提供。</span><span class="sxs-lookup"><span data-stu-id="7ff57-105">This means you can deploy and run Service Fabric applications in any environment that contains a set of interconnected Windows Server computers, be it on premises or with any cloud provider.</span></span> <span data-ttu-id="7ff57-106">Service Fabric 提供 Service Fabric 叢集安裝程式封裝 toocreate 稱為 hello 獨立 Windows 伺服器封裝。</span><span class="sxs-lookup"><span data-stu-id="7ff57-106">Service Fabric provides a setup package toocreate Service Fabric clusters called hello standalone Windows Server package.</span></span>

<span data-ttu-id="7ff57-107">這篇文章會引導您建立獨立 Service Fabric 叢集 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="7ff57-107">This article walks you through hello steps for creating a Service Fabric standalone cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="7ff57-108">此獨立 Windows Server 套件已正式上市，可使用於生產部署。</span><span class="sxs-lookup"><span data-stu-id="7ff57-108">This standalone Windows Server package is commercially available and may be used for production deployments.</span></span> <span data-ttu-id="7ff57-109">此套件包含處於「預覽」狀態的新 Service Fabric 功能。</span><span class="sxs-lookup"><span data-stu-id="7ff57-109">This package may contain new Service Fabric features that are in "Preview".</span></span> <span data-ttu-id="7ff57-110">向下捲動太"[預覽功能，此封裝中包含](#previewfeatures_anchor)。 」</span><span class="sxs-lookup"><span data-stu-id="7ff57-110">Scroll down too"[Preview features included in this package](#previewfeatures_anchor)."</span></span> <span data-ttu-id="7ff57-111">一節，以 hello 清單 hello 預覽功能。</span><span class="sxs-lookup"><span data-stu-id="7ff57-111">section for hello list of hello preview features.</span></span> <span data-ttu-id="7ff57-112">您可以[下載一份 hello EULA](http://go.microsoft.com/fwlink/?LinkID=733084)現在。</span><span class="sxs-lookup"><span data-stu-id="7ff57-112">You can [download a copy of hello EULA](http://go.microsoft.com/fwlink/?LinkID=733084) now.</span></span>
> 
> 

<a id="getsupport"></a>

## <a name="get-support-for-hello-service-fabric-for-windows-server-package"></a><span data-ttu-id="7ff57-113">取得 hello 網狀架構的 Windows Server 的服務封裝的支援</span><span class="sxs-lookup"><span data-stu-id="7ff57-113">Get support for hello Service Fabric for Windows Server package</span></span>
* <span data-ttu-id="7ff57-114">詢問 hello 社群 hello Service Fabric 獨立封裝適用於 Windows Server 中 hello [Azure Service Fabric 論壇](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?)。</span><span class="sxs-lookup"><span data-stu-id="7ff57-114">Ask hello community about hello Service Fabric standalone package for Windows Server in hello [Azure Service Fabric forum](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span></span>
* <span data-ttu-id="7ff57-115">向 [Service Fabric 的專業支援](http://support.microsoft.com/oas/default.aspx?prid=16146)開立票證。</span><span class="sxs-lookup"><span data-stu-id="7ff57-115">Open a ticket for [Professional Support for Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).</span></span>  <span data-ttu-id="7ff57-116">[在這裡](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0)深入了解 Microsoft 的專業支援。</span><span class="sxs-lookup"><span data-stu-id="7ff57-116">Learn more about Professional Support from Microsoft [here](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span></span>
* <span data-ttu-id="7ff57-117">您也可以取得此封裝的支援做為 [Microsoft 頂級支援](https://support.microsoft.com/en-us/premier)的一部分。</span><span class="sxs-lookup"><span data-stu-id="7ff57-117">You can also get support for this package as a part of [Microsoft Premier Support](https://support.microsoft.com/en-us/premier).</span></span>
* <span data-ttu-id="7ff57-118">如需詳細資訊，請參閱 [Azure Service Fabric 支援選項](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support)。</span><span class="sxs-lookup"><span data-stu-id="7ff57-118">For more details, please see [Azure Service Fabric support options](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span></span>
* <span data-ttu-id="7ff57-119">toocollect 記錄檔以取得支援的目的，執行 hello[服務網狀架構獨立記錄檔收集器](service-fabric-cluster-standalone-package-contents.md)。</span><span class="sxs-lookup"><span data-stu-id="7ff57-119">toocollect logs for support purposes, run hello [Service Fabric Standalone Log collector](service-fabric-cluster-standalone-package-contents.md).</span></span>

<a id="downloadpackage"></a>

## <a name="download-hello-service-fabric-for-windows-server-package"></a><span data-ttu-id="7ff57-120">下載 hello 適用於 Windows Server Service Fabric 封裝</span><span class="sxs-lookup"><span data-stu-id="7ff57-120">Download hello Service Fabric for Windows Server package</span></span>
<span data-ttu-id="7ff57-121">toocreate hello 叢集中，使用 hello 網狀架構的 Windows Server 的服務套件 (Windows Server 2012 R2 及更新版本)，請參閱：</span><span class="sxs-lookup"><span data-stu-id="7ff57-121">toocreate hello cluster, use hello Service Fabric for Windows Server package (Windows Server 2012 R2 and newer) found here:</span></span> <br><span data-ttu-id="7ff57-122">
[下載連結 - Service Fabric 獨立封裝 - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)</span><span class="sxs-lookup"><span data-stu-id="7ff57-122">
[Download Link - Service Fabric Standalone Package - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)</span></span>

<span data-ttu-id="7ff57-123">找到 hello 套件內容的詳細資訊[這裡](service-fabric-cluster-standalone-package-contents.md)。</span><span class="sxs-lookup"><span data-stu-id="7ff57-123">Find details on contents of hello package [here](service-fabric-cluster-standalone-package-contents.md).</span></span>

<span data-ttu-id="7ff57-124">在叢集建立時，會自動下載 hello Service Fabric 執行階段封裝。</span><span class="sxs-lookup"><span data-stu-id="7ff57-124">hello Service Fabric runtime package is automatically downloaded at time of cluster creation.</span></span> <span data-ttu-id="7ff57-125">如果部署從機器未連接 toohello 網際網路，請從這裡下載 hello 超出訊號範圍的執行階段封裝：</span><span class="sxs-lookup"><span data-stu-id="7ff57-125">If deploying from a machine not connected toohello internet, please download hello runtime package out of band from here:</span></span> <br><span data-ttu-id="7ff57-126">
[下載連結 - Service Fabric 執行階段 - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)</span><span class="sxs-lookup"><span data-stu-id="7ff57-126">
[Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)</span></span>

<span data-ttu-id="7ff57-127">獨立叢集組態範例在此︰</span><span class="sxs-lookup"><span data-stu-id="7ff57-127">Find Standalone Cluster Configuration samples at:</span></span> <br><span data-ttu-id="7ff57-128">
[獨立叢集組態範例](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span><span class="sxs-lookup"><span data-stu-id="7ff57-128">
[Standalone Cluster Configuration Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span></span>

<a id="createcluster"></a>

## <a name="create-hello-cluster"></a><span data-ttu-id="7ff57-129">建立 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="7ff57-129">Create hello cluster</span></span>
<span data-ttu-id="7ff57-130">Service Fabric 可以部署的 tooa 一個機器開發叢集使用 hello *ClusterConfig.Unsecure.DevCluster.json*檔案中包含[範例](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)。</span><span class="sxs-lookup"><span data-stu-id="7ff57-130">Service Fabric can be deployed tooa one-machine development cluster by using hello *ClusterConfig.Unsecure.DevCluster.json* file included in [Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span></span>

<span data-ttu-id="7ff57-131">解除封裝 hello 獨立封裝 tooyour 機器，請複製 hello 範例組態檔 toohello 本機電腦，然後執行的 hello *CreateServiceFabricCluster.ps1*透過從 hello 獨立的系統管理員 PowerShell 工作階段的指令碼封裝的資料夾：</span><span class="sxs-lookup"><span data-stu-id="7ff57-131">Unpack hello standalone package tooyour machine, copy hello sample config file toohello local machine, then run hello *CreateServiceFabricCluster.ps1* script through an administrator PowerShell session, from hello standalone package folder:</span></span>
### <a name="step-1a-create-an-unsecured-local-development-cluster"></a><span data-ttu-id="7ff57-132">步驟 1A：建立不安全的本機開發叢集</span><span class="sxs-lookup"><span data-stu-id="7ff57-132">Step 1A: Create an unsecured local development cluster</span></span>
```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

<span data-ttu-id="7ff57-133">請參閱 hello 環境設定 > 一節[規劃並準備您的叢集部署](service-fabric-cluster-standalone-deployment-preparation.md)的疑難排解詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7ff57-133">See hello Environment Setup section at [Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md) for troubleshooting details.</span></span>

<span data-ttu-id="7ff57-134">如果您完成執行的開發案例，您可以藉由參考 toosteps 區段中的從 hello 機器移除 hello Service Fabric 叢集 」[移除叢集](#removecluster_anchor)"。</span><span class="sxs-lookup"><span data-stu-id="7ff57-134">If you're finished running development scenarios, you can remove hello Service Fabric cluster from hello machine by referring toosteps in section "[Remove a cluster](#removecluster_anchor)".</span></span> 

### <a name="step-1b-create-a-multi-machine-cluster"></a><span data-ttu-id="7ff57-135">步驟 1B︰ 建立多部電腦的叢集</span><span class="sxs-lookup"><span data-stu-id="7ff57-135">Step 1B: Create a multi-machine cluster</span></span>
<span data-ttu-id="7ff57-136">您已經完成 hello 規劃並準備步驟詳細資料在 hello 下面的連結，您之後可以準備 toocreate 您使用您的叢集設定檔的實際執行叢集。</span><span class="sxs-lookup"><span data-stu-id="7ff57-136">After you have gone through hello planning and preparation steps detailed at hello below link, you are ready toocreate your production cluster using your cluster configuration file.</span></span> <br><span data-ttu-id="7ff57-137">
[規劃及準備叢集部署](service-fabric-cluster-standalone-deployment-preparation.md)</span><span class="sxs-lookup"><span data-stu-id="7ff57-137">
[Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md)</span></span>

1. <span data-ttu-id="7ff57-138">您已經撰寫執行 hello hello 組態檔進行驗證*TestConfiguration.ps1* hello 獨立套件資料夾的指令碼：</span><span class="sxs-lookup"><span data-stu-id="7ff57-138">Validate hello configuration file you have written by running hello *TestConfiguration.ps1* script from hello standalone package folder:</span></span>  

    ```powershell
    .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.json
    ```

    <span data-ttu-id="7ff57-139">您應該會看到如下的輸出：</span><span class="sxs-lookup"><span data-stu-id="7ff57-139">You should see output like below.</span></span> <span data-ttu-id="7ff57-140">如果傳回 hello 場"Passed"是"True"，例行性檢查已通過，並 hello 叢集尋找 toobe 可部署的 hello 輸入組態為基礎。</span><span class="sxs-lookup"><span data-stu-id="7ff57-140">If hello bottom field "Passed" is returned as "True", sanity checks have passed and hello cluster looks toobe deployable based on hello input configuration.</span></span>

    ```
    Trace folder already exists. Traces will be written tooexisting trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
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

2. <span data-ttu-id="7ff57-141">建立 hello 叢集： 執行 hello *CreateServiceFabricCluster.ps1*指令碼 toodeploy hello hello 組態中的每部電腦上的 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="7ff57-141">Create hello cluster:  Run hello *CreateServiceFabricCluster.ps1* script toodeploy hello Service Fabric cluster across each machine in hello configuration.</span></span> 
    ```powershell
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -AcceptEULA
    ```

> [!NOTE]
> <span data-ttu-id="7ff57-142">部署追蹤會寫入 toohello VM/電腦已執行 hello CreateServiceFabricCluster.ps1 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="7ff57-142">Deployment traces are written toohello VM/machine on which you ran hello CreateServiceFabricCluster.ps1 PowerShell script.</span></span> <span data-ttu-id="7ff57-143">可以找到這些 hello 子資料夾 DeploymentTraces，以執行指令碼中的 hello hello 目錄為基礎。</span><span class="sxs-lookup"><span data-stu-id="7ff57-143">These can be found in hello subfolder DeploymentTraces, based in hello directory from which hello script was run.</span></span> <span data-ttu-id="7ff57-144">toosee Service Fabric 是否正確部署 tooa 機器，尋找 hello FabricDataRoot 目錄中所述 hello 叢集組態檔 FabricSettings 區段 （依預設 c:\ProgramData\SF) 中的 hello 安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="7ff57-144">toosee if Service Fabric was deployed correctly tooa machine, find hello installed files in hello FabricDataRoot directory, as detailed in hello cluster configuration file FabricSettings section (by default c:\ProgramData\SF).</span></span> <span data-ttu-id="7ff57-145">同時，也要能在 [工作管理員] 看到 FabricHost.exe 和 Fabric.exe 處理序正在執行中。</span><span class="sxs-lookup"><span data-stu-id="7ff57-145">As well, FabricHost.exe and Fabric.exe processes can be seen running in Task Manager.</span></span>
> 
> 

### <a name="step-1c-create-an-offline-internet-disconnected-cluster"></a><span data-ttu-id="7ff57-146">步驟 1 C：建立離線 (網際網路中斷連線的) 叢集</span><span class="sxs-lookup"><span data-stu-id="7ff57-146">Step 1C: Create an offline (internet-disconnected) cluster</span></span>
<span data-ttu-id="7ff57-147">在叢集建立時，會自動下載 hello Service Fabric 執行階段封裝。</span><span class="sxs-lookup"><span data-stu-id="7ff57-147">hello Service Fabric runtime package is automatically downloaded at cluster creation.</span></span> <span data-ttu-id="7ff57-148">連接時，不部署叢集 toomachines toohello 網際網路，您將需要 toodownload hello Service Fabric 執行階段分別封裝並提供在叢集建立 hello 路徑 tooit。</span><span class="sxs-lookup"><span data-stu-id="7ff57-148">When deploying a cluster toomachines not connected toohello internet, you will need toodownload hello Service Fabric runtime package separately, and provide hello path tooit at cluster creation.</span></span>
<span data-ttu-id="7ff57-149">hello 執行階段封裝可以分別下載，從另一部電腦連接 toohello 網際網路，在[下載連結的 Service Fabric 執行階段的 Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)。</span><span class="sxs-lookup"><span data-stu-id="7ff57-149">hello runtime package can be downloaded separately, from another machine connected toohello internet, at [Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span></span> <span data-ttu-id="7ff57-150">複製您要部署的 hello 離線的叢集，並執行建立 hello 叢集 hello 執行階段封裝 toowhere`CreateServiceFabricCluster.ps1`以 hello`-FabricRuntimePackagePath`參數包含如下所示：</span><span class="sxs-lookup"><span data-stu-id="7ff57-150">Copy hello runtime package toowhere you are deploying hello offline cluster from, and create hello cluster by running `CreateServiceFabricCluster.ps1` with hello `-FabricRuntimePackagePath` parameter included, as shown below:</span></span> 

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -FabricRuntimePackagePath .\MicrosoftAzureServiceFabric.cab
```
<span data-ttu-id="7ff57-151">其中`.\ClusterConfig.json`和`.\MicrosoftAzureServiceFabric.cab`分別為 hello 路徑 toohello 叢集組態和 hello 執行階段.cab 檔案。</span><span class="sxs-lookup"><span data-stu-id="7ff57-151">where `.\ClusterConfig.json` and `.\MicrosoftAzureServiceFabric.cab` are hello paths toohello cluster configuration and hello runtime .cab file respectively.</span></span>


### <a name="step-2-connect-toohello-cluster"></a><span data-ttu-id="7ff57-152">步驟 2: Toohello 叢集連線</span><span class="sxs-lookup"><span data-stu-id="7ff57-152">Step 2: Connect toohello cluster</span></span>
<span data-ttu-id="7ff57-153">tooconnect tooa 安全叢集，請參閱[Service fabric toosecure 叢集連線](service-fabric-connect-to-secure-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="7ff57-153">tooconnect tooa secure cluster, see [Service fabric connect toosecure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="7ff57-154">tooconnect tooan 不安全叢集，請執行下列 PowerShell 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="7ff57-154">tooconnect tooan unsecure cluster, run hello following PowerShell command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <*IPAddressofaMachine*>:<Client connection end point port>
```
<span data-ttu-id="7ff57-155">範例：</span><span class="sxs-lookup"><span data-stu-id="7ff57-155">Example:</span></span>
```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint 192.13.123.2345:19000
```
### <a name="step-3-bring-up-service-fabric-explorer"></a><span data-ttu-id="7ff57-156">步驟 3：啟動 Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="7ff57-156">Step 3: Bring up Service Fabric Explorer</span></span>
<span data-ttu-id="7ff57-157">現在您可以利用 Service Fabric Explorer 直接向其中一個 hello 機器 http://localhost:19080/Explorer/index.html 或從遠端 http://&lt 連接 toohello 叢集*IPAddressofaMachine*>: 19080 /Explorer/index.html。</span><span class="sxs-lookup"><span data-stu-id="7ff57-157">Now you can connect toohello cluster with Service Fabric Explorer either directly from one of hello machines with http://localhost:19080/Explorer/index.html or remotely with http://<*IPAddressofaMachine*>:19080/Explorer/index.html.</span></span>

## <a name="add-and-remove-nodes"></a><span data-ttu-id="7ff57-158">新增和移除節點</span><span class="sxs-lookup"><span data-stu-id="7ff57-158">Add and remove nodes</span></span>
<span data-ttu-id="7ff57-159">您可以新增或移除節點 tooyour 獨立 Service Fabric 叢集，因為您的商務需求變更。</span><span class="sxs-lookup"><span data-stu-id="7ff57-159">You can add or remove nodes tooyour standalone Service Fabric cluster as your business needs change.</span></span> <span data-ttu-id="7ff57-160">請參閱[新增或移除節點 tooa Service Fabric 獨立叢集](service-fabric-cluster-windows-server-add-remove-nodes.md)如需詳細步驟。</span><span class="sxs-lookup"><span data-stu-id="7ff57-160">See [Add or Remove nodes tooa Service Fabric standalone cluster](service-fabric-cluster-windows-server-add-remove-nodes.md) for detailed steps.</span></span>

<a id="removecluster" name="removecluster_anchor"></a>
## <a name="remove-a-cluster"></a><span data-ttu-id="7ff57-161">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="7ff57-161">Remove a cluster</span></span>
<span data-ttu-id="7ff57-162">tooremove 叢集中，執行 hello *RemoveServiceFabricCluster.ps1* hello 套件資料夾並傳入 hello 路徑 toohello JSON 組態檔中的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="7ff57-162">tooremove a cluster, run hello *RemoveServiceFabricCluster.ps1* PowerShell script from hello package folder and pass in hello path toohello JSON configuration file.</span></span> <span data-ttu-id="7ff57-163">您可以選擇性地指定 hello 刪除 hello 記錄檔的位置。</span><span class="sxs-lookup"><span data-stu-id="7ff57-163">You can optionally specify a location for hello log of hello deletion.</span></span>

<span data-ttu-id="7ff57-164">此指令碼可以在任何電腦具有系統管理員存取 tooall hello 機器列為 hello 叢集組態檔中的節點上執行。</span><span class="sxs-lookup"><span data-stu-id="7ff57-164">This script can be run on any machine that has administrator access tooall hello machines that are listed as nodes in hello cluster configuration file.</span></span> <span data-ttu-id="7ff57-165">hello 機器上執行此指令碼並沒有 toobe hello 叢集的一部分。</span><span class="sxs-lookup"><span data-stu-id="7ff57-165">hello machine that this script is run on does not have toobe part of hello cluster.</span></span>

```
# Removes Service Fabric from each machine in hello configuration
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -Force
```

```
# Removes Service Fabric from hello current machine
.\CleanFabric.ps1
```

<a id="telemetry"></a>

## <a name="telemetry-data-collected-and-how-tooopt-out-of-it"></a><span data-ttu-id="7ff57-166">收集的遙測資料以及如何不使用 tooopt</span><span class="sxs-lookup"><span data-stu-id="7ff57-166">Telemetry data collected and how tooopt out of it</span></span>
<span data-ttu-id="7ff57-167">預設為 hello 產品會收集 hello Service Fabric 使用量 tooimprove hello 產品遙測。</span><span class="sxs-lookup"><span data-stu-id="7ff57-167">As a default, hello product collects telemetry on hello Service Fabric usage tooimprove hello product.</span></span> <span data-ttu-id="7ff57-168">hello hello 安裝程式的一部分太檢查連線時才執行最佳做法分析程式[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1)。</span><span class="sxs-lookup"><span data-stu-id="7ff57-168">hello Best Practice Analyzer that runs as a part of hello setup checks for connectivity too[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span></span> <span data-ttu-id="7ff57-169">如果它找不到，hello 安裝會失敗，除非您退出遙測。</span><span class="sxs-lookup"><span data-stu-id="7ff57-169">If it is not reachable, hello setup fails unless you opt out of telemetry.</span></span>

1. <span data-ttu-id="7ff57-170">hello 遙測管線會嘗試遵循資料太 tooupload hello[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1)每天一次。</span><span class="sxs-lookup"><span data-stu-id="7ff57-170">hello telemetry pipeline tries tooupload hello following data too[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) once every day.</span></span> <span data-ttu-id="7ff57-171">它是最佳方式上傳並 hello 叢集 」 功能沒有任何影響。</span><span class="sxs-lookup"><span data-stu-id="7ff57-171">It is a best-effort upload and has no impact on hello cluster functionality.</span></span> <span data-ttu-id="7ff57-172">hello 遙測才會傳送 hello 節點執行 hello 容錯移轉管理員主要。</span><span class="sxs-lookup"><span data-stu-id="7ff57-172">hello telemetry is only sent from hello node that runs hello failover manager primary.</span></span> <span data-ttu-id="7ff57-173">沒有其他節點會傳送遙測。</span><span class="sxs-lookup"><span data-stu-id="7ff57-173">No other nodes send out telemetry.</span></span>
2. <span data-ttu-id="7ff57-174">hello 遙測組成 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="7ff57-174">hello telemetry consists of hello following:</span></span>

* <span data-ttu-id="7ff57-175">服務數</span><span class="sxs-lookup"><span data-stu-id="7ff57-175">Number of services</span></span>
* <span data-ttu-id="7ff57-176">ServiceTypes 數目</span><span class="sxs-lookup"><span data-stu-id="7ff57-176">Number of ServiceTypes</span></span>
* <span data-ttu-id="7ff57-177">Applications 的數目</span><span class="sxs-lookup"><span data-stu-id="7ff57-177">Number of Applications</span></span>
* <span data-ttu-id="7ff57-178">ApplicationUpgrades 的數目</span><span class="sxs-lookup"><span data-stu-id="7ff57-178">Number of ApplicationUpgrades</span></span>
* <span data-ttu-id="7ff57-179">FailoverUnits 的數目</span><span class="sxs-lookup"><span data-stu-id="7ff57-179">Number of FailoverUnits</span></span>
* <span data-ttu-id="7ff57-180">InBuildFailoverUnits 的數目</span><span class="sxs-lookup"><span data-stu-id="7ff57-180">Number of InBuildFailoverUnits</span></span>
* <span data-ttu-id="7ff57-181">UnhealthyFailoverUnits 的數目</span><span class="sxs-lookup"><span data-stu-id="7ff57-181">Number of UnhealthyFailoverUnits</span></span>
* <span data-ttu-id="7ff57-182">Replicas 的數目</span><span class="sxs-lookup"><span data-stu-id="7ff57-182">Number of Replicas</span></span>
* <span data-ttu-id="7ff57-183">InBuildReplicas 的數目</span><span class="sxs-lookup"><span data-stu-id="7ff57-183">Number of InBuildReplicas</span></span>
* <span data-ttu-id="7ff57-184">StandByReplicas 的數目</span><span class="sxs-lookup"><span data-stu-id="7ff57-184">Number of StandByReplicas</span></span>
* <span data-ttu-id="7ff57-185">OfflineReplicas 的數目</span><span class="sxs-lookup"><span data-stu-id="7ff57-185">Number of OfflineReplicas</span></span>
* <span data-ttu-id="7ff57-186">CommonQueueLength</span><span class="sxs-lookup"><span data-stu-id="7ff57-186">CommonQueueLength</span></span>
* <span data-ttu-id="7ff57-187">QueryQueueLength</span><span class="sxs-lookup"><span data-stu-id="7ff57-187">QueryQueueLength</span></span>
* <span data-ttu-id="7ff57-188">FailoverUnitQueueLength</span><span class="sxs-lookup"><span data-stu-id="7ff57-188">FailoverUnitQueueLength</span></span>
* <span data-ttu-id="7ff57-189">CommitQueueLength</span><span class="sxs-lookup"><span data-stu-id="7ff57-189">CommitQueueLength</span></span>
* <span data-ttu-id="7ff57-190">Nodes 的數目</span><span class="sxs-lookup"><span data-stu-id="7ff57-190">Number of Nodes</span></span>
* <span data-ttu-id="7ff57-191">IsContextComplete: True/False</span><span class="sxs-lookup"><span data-stu-id="7ff57-191">IsContextComplete: True/False</span></span>
* <span data-ttu-id="7ff57-192">ClusterId︰這是針對每個叢集隨機產生的 GUID。</span><span class="sxs-lookup"><span data-stu-id="7ff57-192">ClusterId: This is a GUID randomly generated for each cluster</span></span>
* <span data-ttu-id="7ff57-193">ServiceFabricVersion</span><span class="sxs-lookup"><span data-stu-id="7ff57-193">ServiceFabricVersion</span></span>
* <span data-ttu-id="7ff57-194">Hello 虛擬機器或從哪些 hello 上傳遙測的機器的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="7ff57-194">IP address of hello virtual machine or machine from which hello telemetry is uploaded</span></span>

<span data-ttu-id="7ff57-195">toodisable 遙測 hello 太之後加入*屬性*在叢集組態中： *enableTelemetry: false*。</span><span class="sxs-lookup"><span data-stu-id="7ff57-195">toodisable telemetry, add hello following too*properties* in your cluster config: *enableTelemetry: false*.</span></span>

<a id="previewfeatures" name="previewfeatures_anchor"></a>

## <a name="preview-features-included-in-this-package"></a><span data-ttu-id="7ff57-196">此封裝包含的預覽功能</span><span class="sxs-lookup"><span data-stu-id="7ff57-196">Preview features included in this package</span></span>
<span data-ttu-id="7ff57-197">無。</span><span class="sxs-lookup"><span data-stu-id="7ff57-197">None.</span></span>


> [!NOTE]
> <span data-ttu-id="7ff57-198">從新的 hello [GA 版的 Windows Server 的 hello 獨立叢集 (版本 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/)，您可以手動或自動升級叢集 toofuture 發行版本。</span><span class="sxs-lookup"><span data-stu-id="7ff57-198">Starting with hello new [GA version of hello standalone cluster for Windows Server (version 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), you can upgrade your cluster toofuture releases, manually or automatically.</span></span> <span data-ttu-id="7ff57-199">請參閱太[升級獨立 Service Fabric 叢集版本](service-fabric-cluster-upgrade-windows-server.md)文件以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7ff57-199">Refer too[Upgrade a standalone Service Fabric cluster version](service-fabric-cluster-upgrade-windows-server.md) document for details.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="7ff57-200">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7ff57-200">Next steps</span></span>
* [<span data-ttu-id="7ff57-201">使用 PowerShell 部署與移除應用程式</span><span class="sxs-lookup"><span data-stu-id="7ff57-201">Deploy and remove applications using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="7ff57-202">獨立 Windows 叢集的組態設定</span><span class="sxs-lookup"><span data-stu-id="7ff57-202">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="7ff57-203">新增或移除節點 tooa 獨立 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="7ff57-203">Add or remove nodes tooa standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="7ff57-204">獨立 Service Fabric 叢集版本升級</span><span class="sxs-lookup"><span data-stu-id="7ff57-204">Upgrade a standalone Service Fabric cluster version</span></span>](service-fabric-cluster-upgrade-windows-server.md)
* [<span data-ttu-id="7ff57-205">建立具有執行 Windows 之 Azure VM 的獨立 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="7ff57-205">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)
* [<span data-ttu-id="7ff57-206">使用 Windows 安全性保護 Windows 上的獨立叢集</span><span class="sxs-lookup"><span data-stu-id="7ff57-206">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="7ff57-207">使用 X509 憑證保護 Windows 上的獨立叢集</span><span class="sxs-lookup"><span data-stu-id="7ff57-207">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

<!--Image references-->
[Trusted Zone]: ./media/service-fabric-cluster-creation-for-windows-server/TrustedZone.png
