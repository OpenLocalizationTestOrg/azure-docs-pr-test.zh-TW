---
title: "Windows 伺服器的獨立 Azure Service Fabric 叢集的 aaaUpgrade |Microsoft 文件"
description: "升級 hello Azure Service Fabric 程式碼和/或執行獨立 Service Fabric 叢集，包括設定 hello 叢集更新模式的組態。"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 66296cc6-9524-4c6a-b0a6-57c253bdf67e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 5132795e544b6f0185accedbf5092dcaafd66df0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-standalone-azure-service-fabric-on-windows-server-cluster"></a><span data-ttu-id="b80cc-103">在 Windows Server 叢集上升級獨立的 Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b80cc-103">Upgrade your standalone Azure Service Fabric on Windows Server cluster</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b80cc-104">Azure 叢集</span><span class="sxs-lookup"><span data-stu-id="b80cc-104">Azure Cluster</span></span>](service-fabric-cluster-upgrade.md)
> * [<span data-ttu-id="b80cc-105">獨立叢集</span><span class="sxs-lookup"><span data-stu-id="b80cc-105">Standalone Cluster</span></span>](service-fabric-cluster-upgrade-windows-server.md)
>
>

<span data-ttu-id="b80cc-106">針對任何現代系統 hello 能力 tooupgrade 是產品金鑰 toohello 長期成功。</span><span class="sxs-lookup"><span data-stu-id="b80cc-106">For any modern system, hello ability tooupgrade is a key toohello long-term success of your product.</span></span> <span data-ttu-id="b80cc-107">Azure Service Fabric 叢集是您擁有的資源。</span><span class="sxs-lookup"><span data-stu-id="b80cc-107">An Azure Service Fabric cluster is a resource that you own.</span></span> <span data-ttu-id="b80cc-108">本文將告訴您如何可確保該 hello 叢集中一定會執行支援的版本的 Service Fabric 程式碼和組態。</span><span class="sxs-lookup"><span data-stu-id="b80cc-108">This article describes how you can make sure that hello cluster always runs supported versions of Service Fabric code and configurations.</span></span>

## <a name="control-hello-service-fabric-version-that-runs-on-your-cluster"></a><span data-ttu-id="b80cc-109">在您的叢集執行的控制 hello Service Fabric 版本</span><span class="sxs-lookup"><span data-stu-id="b80cc-109">Control hello Service Fabric version that runs on your cluster</span></span>
<span data-ttu-id="b80cc-110">tooset 叢集 toodownload 更新的 Service Fabric 當 Microsoft 發行新的版本，組 hello **fabricClusterAutoupgradeEnabled**叢集組態 tootrue。</span><span class="sxs-lookup"><span data-stu-id="b80cc-110">tooset your cluster toodownload updates of Service Fabric when Microsoft releases a new version, set hello **fabricClusterAutoupgradeEnabled** cluster configuration tootrue.</span></span> <span data-ttu-id="b80cc-111">Service Fabric 支援版本，您想在組 hello 您叢集 toobe tooselect **fabricClusterAutoupgradeEnabled**叢集組態 toofalse。</span><span class="sxs-lookup"><span data-stu-id="b80cc-111">tooselect a supported version of Service Fabric that you want your cluster toobe on, set hello **fabricClusterAutoupgradeEnabled** cluster configuration toofalse.</span></span>

> [!NOTE]
> <span data-ttu-id="b80cc-112">請確定您的叢集一律執行支援的 Service Fabric 版本。</span><span class="sxs-lookup"><span data-stu-id="b80cc-112">Make sure that your cluster always runs a supported Service Fabric version.</span></span> <span data-ttu-id="b80cc-113">當 Microsoft 宣佈 hello 發行新版的 Service Fabric 時，hello 舊版標示為的支援即將結束之後從 hello 公告 hello 日期 60 天的最小值。</span><span class="sxs-lookup"><span data-stu-id="b80cc-113">When Microsoft announces hello release of a new version of Service Fabric, hello previous version is marked for end of support after a minimum of 60 days from hello date of hello announcement.</span></span> <span data-ttu-id="b80cc-114">新的版本上經過宣布[hello Service Fabric 小組部落格上](https://blogs.msdn.microsoft.com/azureservicefabric/)。</span><span class="sxs-lookup"><span data-stu-id="b80cc-114">New releases are announced [on hello Service Fabric team blog](https://blogs.msdn.microsoft.com/azureservicefabric/).</span></span> <span data-ttu-id="b80cc-115">hello 新版此時是使用 toochoose。</span><span class="sxs-lookup"><span data-stu-id="b80cc-115">hello new release is available toochoose at that point.</span></span>
>
>

<span data-ttu-id="b80cc-116">只有當您使用生產樣式節點設定後，每個 Service Fabric 節點的個別實體或虛擬機器上的配置位置，您可以升級叢集 toohello 的新版本。</span><span class="sxs-lookup"><span data-stu-id="b80cc-116">You can upgrade your cluster toohello new version only if you are using a production-style node configuration, where each Service Fabric node is allocated on a separate physical or virtual machine.</span></span> <span data-ttu-id="b80cc-117">如果您有開發叢集，其中多部 Service Fabric 節點都是單一實體或虛擬機器，您必須重新建立 hello 叢集 hello 新版本。</span><span class="sxs-lookup"><span data-stu-id="b80cc-117">If you have a development cluster, where more than one Service Fabric node is on a single physical or virtual machine, you must re-create hello cluster with hello new version.</span></span>

<span data-ttu-id="b80cc-118">兩個不同的工作流程可以升級叢集 toohello 的最新版本或 Service Fabric 的支援的版本。</span><span class="sxs-lookup"><span data-stu-id="b80cc-118">Two distinct workflows can upgrade your cluster toohello latest version or a supported Service Fabric version.</span></span> <span data-ttu-id="b80cc-119">一個工作流程是在連線 toodownload hello 最新版本時自動的叢集。</span><span class="sxs-lookup"><span data-stu-id="b80cc-119">One workflow is for clusters that have connectivity toodownload hello latest version automatically.</span></span> <span data-ttu-id="b80cc-120">hello 其他工作流程是沒有連線 toodownload hello 最新 Service Fabric 版本的叢集。</span><span class="sxs-lookup"><span data-stu-id="b80cc-120">hello other workflow is for clusters that do not have connectivity toodownload hello latest Service Fabric version.</span></span>

### <a name="upgrade-clusters-that-have-connectivity-toodownload-hello-latest-code-and-configuration"></a><span data-ttu-id="b80cc-121">升級叢集具有連線 toodownload hello 最新程式碼和組態</span><span class="sxs-lookup"><span data-stu-id="b80cc-121">Upgrade clusters that have connectivity toodownload hello latest code and configuration</span></span>
<span data-ttu-id="b80cc-122">使用這些步驟 tooupgrade 您叢集 tooa 支援版本，如果您的叢集節點具有網際網路連線能力過[http://download.microsoft.com](http://download.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="b80cc-122">Use these steps tooupgrade your cluster tooa supported version if your cluster nodes have Internet connectivity too[http://download.microsoft.com](http://download.microsoft.com).</span></span>

<span data-ttu-id="b80cc-123">也有連線的叢集[http://download.microsoft.com](http://download.microsoft.com)，Microsoft 會定期檢查新的 Service Fabric 版本 hello 可用性。</span><span class="sxs-lookup"><span data-stu-id="b80cc-123">For clusters that have connectivity too[http://download.microsoft.com](http://download.microsoft.com), Microsoft periodically checks for hello availability of new Service Fabric versions.</span></span>

<span data-ttu-id="b80cc-124">新的 Service Fabric 版本可用時，要 toohello 叢集在本機下載 hello 封裝和升級的佈建。</span><span class="sxs-lookup"><span data-stu-id="b80cc-124">When a new Service Fabric version is available, hello package is downloaded locally toohello cluster and provisioned for upgrade.</span></span> <span data-ttu-id="b80cc-125">此外，這個新版本的 tooinform hello 客戶，hello 系統顯示會類似下列的 toohello 明確叢集健全狀況警告：</span><span class="sxs-lookup"><span data-stu-id="b80cc-125">Additionally, tooinform hello customer of this new version, hello system shows an explicit cluster health warning that's similar toohello following:</span></span>

<span data-ttu-id="b80cc-126">"hello 目前叢集版本 [版本 #] 支援將結束 [Date]"。</span><span class="sxs-lookup"><span data-stu-id="b80cc-126">“hello current cluster version [version#] support ends [Date]."</span></span>

<span data-ttu-id="b80cc-127">Hello 叢集正在執行 hello 最新版本之後，會隨即消失 hello 警告。</span><span class="sxs-lookup"><span data-stu-id="b80cc-127">After hello cluster is running hello latest version, hello warning goes away.</span></span>

#### <a name="cluster-upgrade-workflow"></a><span data-ttu-id="b80cc-128">叢集升級工作流程</span><span class="sxs-lookup"><span data-stu-id="b80cc-128">Cluster upgrade workflow</span></span>
<span data-ttu-id="b80cc-129">您會看到 hello 叢集健全狀況警告之後，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="b80cc-129">After you see hello cluster health warning, do hello following:</span></span>

1. <span data-ttu-id="b80cc-130">從具有系統管理員存取 tooall hello 機器列為 hello 叢集中節點的任何電腦連接 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="b80cc-130">Connect toohello cluster from any machine that has administrator access tooall hello machines that are listed as nodes in hello cluster.</span></span> <span data-ttu-id="b80cc-131">hello 機器上執行此指令碼並沒有 toobe hello 叢集的一部分。</span><span class="sxs-lookup"><span data-stu-id="b80cc-131">hello machine that this script is run on does not have toobe part of hello cluster.</span></span>

    ```powershell

    ###### connect toohello secure cluster using certs
    $ClusterName= "mysecurecluster.something.com:19000"
    $CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7FG2D630F8F3"
    Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
        -X509Credential `
        -ServerCertThumbprint $CertThumbprint  `
        -FindType FindByThumbprint `
        -FindValue $CertThumbprint `
        -StoreLocation CurrentUser `
        -StoreName My
    ```

2. <span data-ttu-id="b80cc-132">取得您可以升級到 Service Fabric 版本 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="b80cc-132">Get hello list of Service Fabric versions that you can upgrade to.</span></span>

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Get-ServiceFabricRegisteredClusterCodeVersion
    ```

    <span data-ttu-id="b80cc-133">您應該取得輸出類似 toothis:</span><span class="sxs-lookup"><span data-stu-id="b80cc-133">You should get an output similar toothis:</span></span>

    ![取得網狀架構版本][getfabversions]
3. <span data-ttu-id="b80cc-135">開始使用的叢集升級 tooan 可用版本[開始 ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) PowerShell cmd.</span><span class="sxs-lookup"><span data-stu-id="b80cc-135">Start a cluster upgrade tooan available version by using the [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) PowerShell cmd.</span></span>

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   <span data-ttu-id="b80cc-136">toomonitor hello hello 升級進度，您可以使用 Service Fabric 總管或執行下列 Windows PowerShell 命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="b80cc-136">toomonitor hello progress of hello upgrade, you can use Service Fabric Explorer or run hello following Windows PowerShell command.</span></span>

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    <span data-ttu-id="b80cc-137">如果不符合 hello 叢集健全狀況原則，會回復 hello 升級。</span><span class="sxs-lookup"><span data-stu-id="b80cc-137">If hello cluster health policies are not met, hello upgrade is rolled back.</span></span> <span data-ttu-id="b80cc-138">hello toospecify 自訂的健康情況原則**開始 ServiceFabricClusterUpgrade**命令，請參閱文件[開始 ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b80cc-138">toospecify custom health policies for hello **Start-ServiceFabricClusterUpgrade** command, see documentation for [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span></span>

<span data-ttu-id="b80cc-139">修正導致 hello 復原 hello 問題之後，相同的步驟如先前所述的下列 hello 起始 hello 升級一次。</span><span class="sxs-lookup"><span data-stu-id="b80cc-139">After you fix hello issues that resulted in hello rollback, initiate hello upgrade again by following hello same steps as previously described.</span></span>

### <a name="upgrade-clusters-that-have-uno-connectivityu-toodownload-hello-latest-code-and-configuration"></a><span data-ttu-id="b80cc-140">升級具有叢集<U>沒有連線</u>toodownload hello 最新的程式碼和組態</span><span class="sxs-lookup"><span data-stu-id="b80cc-140">Upgrade clusters that have <U>no connectivity</u> toodownload hello latest code and configuration</span></span>
<span data-ttu-id="b80cc-141">使用這些步驟 tooupgrade 您叢集 tooa 支援版本，如果您的叢集節點不太需要網際網路連線[http://download.microsoft.com](http://download.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="b80cc-141">Use these steps tooupgrade your cluster tooa supported version if your cluster nodes do not have Internet connectivity too[http://download.microsoft.com](http://download.microsoft.com).</span></span>

> [!NOTE]
> <span data-ttu-id="b80cc-142">如果您正在執行不是連接的 toohello 網際網路的叢集，您必須 toomonitor hello Service Fabric 小組部落格 toolearn 有關新的版本。</span><span class="sxs-lookup"><span data-stu-id="b80cc-142">If you are running a cluster that is not connected toohello Internet, you will have toomonitor hello Service Fabric team blog toolearn about a new release.</span></span> <span data-ttu-id="b80cc-143">hello 系統不會顯示叢集健全狀況警告 tooalert 您新的版本。</span><span class="sxs-lookup"><span data-stu-id="b80cc-143">hello system does not show a cluster health warning tooalert you of a new release.</span></span>  
>
>

#### <a name="auto-provisioning-vs-manual-provisioning"></a><span data-ttu-id="b80cc-144">自動佈建與手動佈建</span><span class="sxs-lookup"><span data-stu-id="b80cc-144">Auto Provisioning vs Manual Provisioning</span></span>
<span data-ttu-id="b80cc-145">tooenable 自動下載和註冊的 hello 最新的程式碼版本，設定網狀架構更新服務。</span><span class="sxs-lookup"><span data-stu-id="b80cc-145">tooenable automatic downloading and registration for hello latest code version, set up Service Fabric Update Service.</span></span> <span data-ttu-id="b80cc-146">參考內 hello toohello Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt[獨立封裝](service-fabric-cluster-standalone-package-contents.md)如需相關指示。</span><span class="sxs-lookup"><span data-stu-id="b80cc-146">Refer toohello Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt inside hello [Standalone Package](service-fabric-cluster-standalone-package-contents.md) for instructions.</span></span>
<span data-ttu-id="b80cc-147">手動程序，請遵循下列的 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="b80cc-147">For manual process, follow hello instructions below.</span></span>

<span data-ttu-id="b80cc-148">修改下列屬性 toofalse 開始組態升級之前您叢集組態 tooset hello。</span><span class="sxs-lookup"><span data-stu-id="b80cc-148">Modify your cluster configuration tooset hello following property toofalse before you start a configuration upgrade.</span></span>

        "fabricClusterAutoupgradeEnabled": false,

<span data-ttu-id="b80cc-149">請參閱太[開始 ServiceFabricClusterConfigurationUpgrade PS cmd](https://msdn.microsoft.com/en-us/library/mt788302.aspx)的使用方式詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b80cc-149">Refer too[Start-ServiceFabricClusterConfigurationUpgrade PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) for usage details.</span></span> <span data-ttu-id="b80cc-150">開始 hello 組態升級之前，請確定 tooupdate 'clusterConfigurationVersion' 在您的 JSON。</span><span class="sxs-lookup"><span data-stu-id="b80cc-150">Make sure tooupdate 'clusterConfigurationVersion' in your JSON before you start hello configuration upgrade.</span></span>

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

#### <a name="cluster-upgrade-workflow"></a><span data-ttu-id="b80cc-151">叢集升級工作流程</span><span class="sxs-lookup"><span data-stu-id="b80cc-151">Cluster upgrade workflow</span></span>

1. <span data-ttu-id="b80cc-152">執行 Get ServiceFabricClusterUpgrade 從其中一個 hello hello 叢集中的節點，並記下 hello TargetCodeVersion。</span><span class="sxs-lookup"><span data-stu-id="b80cc-152">Run Get-ServiceFabricClusterUpgrade from one of hello nodes in hello cluster and note hello TargetCodeVersion.</span></span>
2. <span data-ttu-id="b80cc-153">從網際網路連線的機器 toolist 執行的 hello 下列所有升級與 hello 目前版本的相容版本，並下載 hello 對應從 hello 相關的下載連結的封裝。</span><span class="sxs-lookup"><span data-stu-id="b80cc-153">Run hello following from an internet connected machine toolist all upgrade compatible versions with hello current version and download hello corresponding package from hello associated download links.</span></span>

    ```powershell

    ###### Get list of all upgrade compatible packages  
    Get-ServiceFabricRuntimeUpgradeVersion -BaseVersion <TargetCodeVersion as noted in Step 1> 
    ```

3. <span data-ttu-id="b80cc-154">從具有系統管理員存取 tooall hello 機器列為 hello 叢集中節點的任何電腦連接 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="b80cc-154">Connect toohello cluster from any machine that has administrator access tooall hello machines that are listed as nodes in hello cluster.</span></span> <span data-ttu-id="b80cc-155">hello 電腦上執行此指令碼並沒有 toobe hello 叢集的一部分</span><span class="sxs-lookup"><span data-stu-id="b80cc-155">hello machine that this script is run on does not have toobe part of hello cluster</span></span>

    ```powershell

   ###### Get hello list of available Service Fabric versions
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file including hello path tooit> -ImageStoreConnectionString "fabric:ImageStore"

   ###### Here is a filled-out example
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath .\MicrosoftAzureServiceFabric.5.3.301.9590.cab -ImageStoreConnectionString "fabric:ImageStore"

    ```
4. <span data-ttu-id="b80cc-156">將下載的 hello 封裝複製到 hello 叢集映像存放區。</span><span class="sxs-lookup"><span data-stu-id="b80cc-156">Copy hello downloaded package into hello cluster image store.</span></span>

5. <span data-ttu-id="b80cc-157">註冊 hello 複製封裝。</span><span class="sxs-lookup"><span data-stu-id="b80cc-157">Register hello copied package.</span></span>

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Register-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file>

    ###### Here is a filled-out example
    Register-ServiceFabricClusterPackage -Code -CodePackagePath MicrosoftAzureServiceFabric.5.3.301.9590.cab

     ```
6. <span data-ttu-id="b80cc-158">啟動叢集升級 tooan 可用版本。</span><span class="sxs-lookup"><span data-stu-id="b80cc-158">Start a cluster upgrade tooan available version.</span></span>

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example
    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   <span data-ttu-id="b80cc-159">您可以監視 hello 的 Service Fabric 總管，在 hello 升級的進度，或者您可以執行下列 PowerShell 命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="b80cc-159">You can monitor hello progress of hello upgrade on Service Fabric Explorer, or you can run hello following PowerShell command.</span></span>

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    <span data-ttu-id="b80cc-160">如果不符合 hello 叢集健全狀況原則，會回復 hello 升級。</span><span class="sxs-lookup"><span data-stu-id="b80cc-160">If hello cluster health policies are not met, hello upgrade is rolled back.</span></span> <span data-ttu-id="b80cc-161">hello toospecify 自訂的健康情況原則**開始 ServiceFabricClusterUpgrade**命令，請參閱 hello 文件[開始 ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b80cc-161">toospecify custom health policies for hello **Start-ServiceFabricClusterUpgrade** command, see hello documentation for [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span></span>

<span data-ttu-id="b80cc-162">修正導致 hello 復原 hello 問題之後，相同的步驟如先前所述的下列 hello 起始 hello 升級一次。</span><span class="sxs-lookup"><span data-stu-id="b80cc-162">After you fix hello issues that resulted in hello rollback, initiate hello upgrade again by following hello same steps as previously described.</span></span>


## <a name="upgrade-hello-cluster-configuration"></a><span data-ttu-id="b80cc-163">升級 hello 叢集設定</span><span class="sxs-lookup"><span data-stu-id="b80cc-163">Upgrade hello cluster configuration</span></span>
<span data-ttu-id="b80cc-164">起始 hello 組態升級之前，您可以測試您的新叢集組態 json hello 獨立封裝中執行 hello powershell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="b80cc-164">Before you initiate hello configuration upgrade, you can test your new cluster configuration json by running hello powershell script in hello standalone package.</span></span>

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File>

```
<span data-ttu-id="b80cc-165">或</span><span class="sxs-lookup"><span data-stu-id="b80cc-165">or</span></span>

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File> -FabricRuntimePackagePath <Path toohello .cab file which you want tootest hello configuration against>

```

<span data-ttu-id="b80cc-166">某些組態無法升級，例如端點、叢集名稱、節點 IP 等。這將會測試 hello 新叢集組態 json 針對 hello 舊的密碼，並擲回錯誤 hello Powershell 視窗中，如果有任何問題。</span><span class="sxs-lookup"><span data-stu-id="b80cc-166">Some configurations can't be upgraded, such as endpoints, cluster name, node IP, etc. This will test hello new cluster configuration json against hello old one and throw errors in hello Powershell window if there is any issue.</span></span>

<span data-ttu-id="b80cc-167">tooupgrade hello 叢集組態升級時，執行**開始 ServiceFabricClusterConfigurationUpgrade**。</span><span class="sxs-lookup"><span data-stu-id="b80cc-167">tooupgrade hello cluster configuration upgrade, run **Start-ServiceFabricClusterConfigurationUpgrade**.</span></span> <span data-ttu-id="b80cc-168">hello 組態升級已處理的升級網域的升級網域。</span><span class="sxs-lookup"><span data-stu-id="b80cc-168">hello configuration upgrade is processed upgrade domain by upgrade domain.</span></span>

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

### <a name="cluster-certificate-config-upgrade"></a><span data-ttu-id="b80cc-169">叢集憑證組態升級</span><span class="sxs-lookup"><span data-stu-id="b80cc-169">Cluster certificate config upgrade</span></span>  
<span data-ttu-id="b80cc-170">叢集的憑證會用於叢集節點之間的驗證，因此 hello 憑證變換執行時應該格外小心因為失敗將會封鎖 hello 的叢集節點之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="b80cc-170">Cluster certificate is used for authentication between cluster nodes, so hello certificate roll over should be performed with extra caution because failure will block hello communication among cluster nodes.</span></span>  
<span data-ttu-id="b80cc-171">從技術角度來看，支援三個選項：</span><span class="sxs-lookup"><span data-stu-id="b80cc-171">Technically, three options are supported:</span></span>  

1. <span data-ttu-id="b80cc-172">單一憑證升級： hello 的升級路徑是 ' 憑證 （主要）]-> [憑證 B （主要）]-> [憑證 C （主要）->...'。</span><span class="sxs-lookup"><span data-stu-id="b80cc-172">Single certificate upgrade: hello upgrade path is 'Certificate A (Primary) -> Certificate B (Primary) -> Certificate C (Primary) -> ...'.</span></span>   
2. <span data-ttu-id="b80cc-173">Double 憑證升級： hello 的升級路徑是 ' 憑證 （主要）]-> [憑證 （主要） 與 （次要） 的 B-憑證 B （主要）-> 憑證 B （主要） 與 C （次要）-憑證 C （主要）->...'。</span><span class="sxs-lookup"><span data-stu-id="b80cc-173">Double certificate upgrade: hello upgrade path is 'Certificate A (Primary) -> Certificate A (Primary) and B (Secondary) -> Certificate B (Primary) -> Certificate B (Primary) and C (Secondary) -> Certificate C (Primary) -> ...'.</span></span>
3. <span data-ttu-id="b80cc-174">憑證類型升級：指紋型憑證設定 <-> CommonName 型憑證設定。</span><span class="sxs-lookup"><span data-stu-id="b80cc-174">Certificate type upgrade: Thumbprint-based certificate configuration <-> CommonName-based certificate configuration.</span></span> <span data-ttu-id="b80cc-175">例如，憑證指紋 A (主要) 和指紋 B (次要) -> 憑證 CommonName C。</span><span class="sxs-lookup"><span data-stu-id="b80cc-175">For example, Certificate Thumbprint A (Primary) and Thumbprint B (Secondary) -> Certificate CommonName C.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b80cc-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b80cc-176">Next steps</span></span>
* <span data-ttu-id="b80cc-177">深入了解如何 toocustomize 某些[Service Fabric 叢集設定](service-fabric-cluster-fabric-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="b80cc-177">Learn how toocustomize some [Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>
* <span data-ttu-id="b80cc-178">了解如何太[叢集及相應放大](service-fabric-cluster-scale-up-down.md)。</span><span class="sxs-lookup"><span data-stu-id="b80cc-178">Learn how too[scale your cluster in and out](service-fabric-cluster-scale-up-down.md).</span></span>
* <span data-ttu-id="b80cc-179">了解[應用程式升級](service-fabric-application-upgrade.md)。</span><span class="sxs-lookup"><span data-stu-id="b80cc-179">Learn about [application upgrades](service-fabric-application-upgrade.md).</span></span>

<!--Image references-->
[getfabversions]: ./media/service-fabric-cluster-upgrade-windows-server/getfabversions.PNG
