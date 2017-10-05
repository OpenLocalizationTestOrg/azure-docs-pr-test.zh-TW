---
title: "在 Windows Server 上升級獨立的 Azure Service Fabric 叢集 | Microsoft Docs"
description: "升級執行獨立 Azure Service Fabric 叢集的 Service Fabric 程式碼和/或組態，包括設定叢集更新模式。"
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
ms.openlocfilehash: ac40775ca62362a32184207857a0b965a798e135
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="upgrade-your-standalone-azure-service-fabric-on-windows-server-cluster"></a><span data-ttu-id="6bdab-103">在 Windows Server 叢集上升級獨立的 Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6bdab-103">Upgrade your standalone Azure Service Fabric on Windows Server cluster</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6bdab-104">Azure 叢集</span><span class="sxs-lookup"><span data-stu-id="6bdab-104">Azure Cluster</span></span>](service-fabric-cluster-upgrade.md)
> * [<span data-ttu-id="6bdab-105">獨立叢集</span><span class="sxs-lookup"><span data-stu-id="6bdab-105">Standalone Cluster</span></span>](service-fabric-cluster-upgrade-windows-server.md)
>
>

<span data-ttu-id="6bdab-106">對於現代化系統來說，升級能力攸關產品是否能長期成功。</span><span class="sxs-lookup"><span data-stu-id="6bdab-106">For any modern system, the ability to upgrade is a key to the long-term success of your product.</span></span> <span data-ttu-id="6bdab-107">Azure Service Fabric 叢集是您擁有的資源。</span><span class="sxs-lookup"><span data-stu-id="6bdab-107">An Azure Service Fabric cluster is a resource that you own.</span></span> <span data-ttu-id="6bdab-108">本文說明如何確定叢集一律會執行支援版本的 Service Fabric 程式碼和組態的方法。</span><span class="sxs-lookup"><span data-stu-id="6bdab-108">This article describes how you can make sure that the cluster always runs supported versions of Service Fabric code and configurations.</span></span>

## <a name="control-the-service-fabric-version-that-runs-on-your-cluster"></a><span data-ttu-id="6bdab-109">控制叢集上執行的 Service Fabric 版本</span><span class="sxs-lookup"><span data-stu-id="6bdab-109">Control the Service Fabric version that runs on your cluster</span></span>
<span data-ttu-id="6bdab-110">若要設定叢集，讓其在 Microsoft 發行新版本時下載 Service Fabric 更新，請將 **fabricClusterAutoupgradeEnabled** 叢集組態設定為 true。</span><span class="sxs-lookup"><span data-stu-id="6bdab-110">To set your cluster to download updates of Service Fabric when Microsoft releases a new version, set the **fabricClusterAutoupgradeEnabled** cluster configuration to true.</span></span> <span data-ttu-id="6bdab-111">若要選取要讓叢集執行的受支援 Service Fabric 版本，請將 **fabricClusterAutoupgradeEnabled** 叢集組態設定為 false。</span><span class="sxs-lookup"><span data-stu-id="6bdab-111">To select a supported version of Service Fabric that you want your cluster to be on, set the **fabricClusterAutoupgradeEnabled** cluster configuration to false.</span></span>

> [!NOTE]
> <span data-ttu-id="6bdab-112">請確定您的叢集一律執行支援的 Service Fabric 版本。</span><span class="sxs-lookup"><span data-stu-id="6bdab-112">Make sure that your cluster always runs a supported Service Fabric version.</span></span> <span data-ttu-id="6bdab-113">當 Microsoft 宣布發行新版本的 Service Fabric 時，從宣布當日起至少 60 天後，舊版就會標示為結束支援。</span><span class="sxs-lookup"><span data-stu-id="6bdab-113">When Microsoft announces the release of a new version of Service Fabric, the previous version is marked for end of support after a minimum of 60 days from the date of the announcement.</span></span> <span data-ttu-id="6bdab-114">新的版本會於 [Service Fabric 小組部落格上](https://blogs.msdn.microsoft.com/azureservicefabric/)發佈。</span><span class="sxs-lookup"><span data-stu-id="6bdab-114">New releases are announced [on the Service Fabric team blog](https://blogs.msdn.microsoft.com/azureservicefabric/).</span></span> <span data-ttu-id="6bdab-115">那時就有新的版本可選擇。</span><span class="sxs-lookup"><span data-stu-id="6bdab-115">The new release is available to choose at that point.</span></span>
>
>

<span data-ttu-id="6bdab-116">只有當您使用生產樣式節點組態，其中每個 Service Fabric 節點是配置在不同實體或虛擬機器時，您才可以將叢集升級到新的版本。</span><span class="sxs-lookup"><span data-stu-id="6bdab-116">You can upgrade your cluster to the new version only if you are using a production-style node configuration, where each Service Fabric node is allocated on a separate physical or virtual machine.</span></span> <span data-ttu-id="6bdab-117">如果您擁有的開發叢集在單一的實體或虛擬機器上有多個 Service Fabric 節點，您必須以新版本重新建立叢集。</span><span class="sxs-lookup"><span data-stu-id="6bdab-117">If you have a development cluster, where more than one Service Fabric node is on a single physical or virtual machine, you must re-create the cluster with the new version.</span></span>

<span data-ttu-id="6bdab-118">兩個不同的工作流程可以將您的叢集升級至最新版本或支援的 Service Fabric 版本。</span><span class="sxs-lookup"><span data-stu-id="6bdab-118">Two distinct workflows can upgrade your cluster to the latest version or a supported Service Fabric version.</span></span> <span data-ttu-id="6bdab-119">一個工作流程適用於具備連線能力而可自動下載最新版本的叢集。</span><span class="sxs-lookup"><span data-stu-id="6bdab-119">One workflow is for clusters that have connectivity to download the latest version automatically.</span></span> <span data-ttu-id="6bdab-120">另一個工作流程則適用於不具備連線能力因而無法下載最新 Service Fabric 版本的叢集。</span><span class="sxs-lookup"><span data-stu-id="6bdab-120">The other workflow is for clusters that do not have connectivity to download the latest Service Fabric version.</span></span>

### <a name="upgrade-clusters-that-have-connectivity-to-download-the-latest-code-and-configuration"></a><span data-ttu-id="6bdab-121">升級具有連線能力而可下載最新程式碼和組態的叢集</span><span class="sxs-lookup"><span data-stu-id="6bdab-121">Upgrade clusters that have connectivity to download the latest code and configuration</span></span>
<span data-ttu-id="6bdab-122">如果您的叢集節點具有與 [http://download.microsoft.com](http://download.microsoft.com) 進行網際網路連線的能力，請使用這些步驟將您的叢集升級至支援的版本。</span><span class="sxs-lookup"><span data-stu-id="6bdab-122">Use these steps to upgrade your cluster to a supported version if your cluster nodes have Internet connectivity to [http://download.microsoft.com](http://download.microsoft.com).</span></span>

<span data-ttu-id="6bdab-123">對於可以連線至 [http://download.microsoft.com](http://download.microsoft.com) 的叢集，Microsoft 會定期檢查是否有新的 Service Fabric 版本。</span><span class="sxs-lookup"><span data-stu-id="6bdab-123">For clusters that have connectivity to [http://download.microsoft.com](http://download.microsoft.com), Microsoft periodically checks for the availability of new Service Fabric versions.</span></span>

<span data-ttu-id="6bdab-124">當新的 Service Fabric 版本可用時，系統會將套件下載至本機叢集並佈建以進行升級。</span><span class="sxs-lookup"><span data-stu-id="6bdab-124">When a new Service Fabric version is available, the package is downloaded locally to the cluster and provisioned for upgrade.</span></span> <span data-ttu-id="6bdab-125">除了通知客戶這個新版本之外，系統會顯示明確的叢集健全狀況警告，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6bdab-125">Additionally, to inform the customer of this new version, the system shows an explicit cluster health warning that's similar to the following:</span></span>

<span data-ttu-id="6bdab-126">「目前的叢集版本 [version#] 支援結束 [Date]。」</span><span class="sxs-lookup"><span data-stu-id="6bdab-126">“The current cluster version [version#] support ends [Date]."</span></span>

<span data-ttu-id="6bdab-127">叢集執行最新版本後，警告就會消失。</span><span class="sxs-lookup"><span data-stu-id="6bdab-127">After the cluster is running the latest version, the warning goes away.</span></span>

#### <a name="cluster-upgrade-workflow"></a><span data-ttu-id="6bdab-128">叢集升級工作流程</span><span class="sxs-lookup"><span data-stu-id="6bdab-128">Cluster upgrade workflow</span></span>
<span data-ttu-id="6bdab-129">您看到叢集健全狀況警告之後，請執行下列操作︰</span><span class="sxs-lookup"><span data-stu-id="6bdab-129">After you see the cluster health warning, do the following:</span></span>

1. <span data-ttu-id="6bdab-130">從具有系統管理員存取權的任何電腦，將叢集連接至列為叢集中節點的所有電腦。</span><span class="sxs-lookup"><span data-stu-id="6bdab-130">Connect to the cluster from any machine that has administrator access to all the machines that are listed as nodes in the cluster.</span></span> <span data-ttu-id="6bdab-131">執行此指令碼所在的電腦不一定是叢集的一部分。</span><span class="sxs-lookup"><span data-stu-id="6bdab-131">The machine that this script is run on does not have to be part of the cluster.</span></span>

    ```powershell

    ###### connect to the secure cluster using certs
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

2. <span data-ttu-id="6bdab-132">取得您可以升級的 Service Fabric 版本清單。</span><span class="sxs-lookup"><span data-stu-id="6bdab-132">Get the list of Service Fabric versions that you can upgrade to.</span></span>

    ```powershell

    ###### Get the list of available Service Fabric versions
    Get-ServiceFabricRegisteredClusterCodeVersion
    ```

    <span data-ttu-id="6bdab-133">您應該會看到如下的輸出：</span><span class="sxs-lookup"><span data-stu-id="6bdab-133">You should get an output similar to this:</span></span>

    ![取得網狀架構版本][getfabversions]
3. <span data-ttu-id="6bdab-135">使用 [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) PowerShell 命令開始將叢集升級為可用版本。</span><span class="sxs-lookup"><span data-stu-id="6bdab-135">Start a cluster upgrade to an available version by using the [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) PowerShell cmd.</span></span>

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   <span data-ttu-id="6bdab-136">若要監視升級的進度，您可以使用 Service Fabric Explorer 或執行下列 Windows PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="6bdab-136">To monitor the progress of the upgrade, you can use Service Fabric Explorer or run the following Windows PowerShell command.</span></span>

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    <span data-ttu-id="6bdab-137">如果不符合叢集健康狀態原則，則會回復升級。</span><span class="sxs-lookup"><span data-stu-id="6bdab-137">If the cluster health policies are not met, the upgrade is rolled back.</span></span> <span data-ttu-id="6bdab-138">若要為 **Start-ServiceFabricClusterUpgrade** 命令指定自訂的健康狀態原則，請參閱 [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) 的文件。</span><span class="sxs-lookup"><span data-stu-id="6bdab-138">To specify custom health policies for the **Start-ServiceFabricClusterUpgrade** command, see documentation for [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span></span>

<span data-ttu-id="6bdab-139">在解決導致復原的問題後，請依照先前所述的相同步驟再次起始升級。</span><span class="sxs-lookup"><span data-stu-id="6bdab-139">After you fix the issues that resulted in the rollback, initiate the upgrade again by following the same steps as previously described.</span></span>

### <a name="upgrade-clusters-that-have-uno-connectivityu-to-download-the-latest-code-and-configuration"></a><span data-ttu-id="6bdab-140">升級<U>沒有連線能力</u>因而無法下載最新程式碼和組態的叢集</span><span class="sxs-lookup"><span data-stu-id="6bdab-140">Upgrade clusters that have <U>no connectivity</u> to download the latest code and configuration</span></span>
<span data-ttu-id="6bdab-141">如果您的叢集節點沒有與 [http://download.microsoft.com](http://download.microsoft.com) 進行網際網路連線的能力，請使用這些步驟將您的叢集升級至支援的版本。</span><span class="sxs-lookup"><span data-stu-id="6bdab-141">Use these steps to upgrade your cluster to a supported version if your cluster nodes do not have Internet connectivity to [http://download.microsoft.com](http://download.microsoft.com).</span></span>

> [!NOTE]
> <span data-ttu-id="6bdab-142">如果您正在執行的叢集未連線至網際網路，您必須關注 Service Fabric 小組部落格，以便得知新版本的消息。</span><span class="sxs-lookup"><span data-stu-id="6bdab-142">If you are running a cluster that is not connected to the Internet, you will have to monitor the Service Fabric team blog to learn about a new release.</span></span> <span data-ttu-id="6bdab-143">系統不會顯示叢集健康狀態警告來提醒您有新版本。</span><span class="sxs-lookup"><span data-stu-id="6bdab-143">The system does not show a cluster health warning to alert you of a new release.</span></span>  
>
>

#### <a name="auto-provisioning-vs-manual-provisioning"></a><span data-ttu-id="6bdab-144">自動佈建與手動佈建</span><span class="sxs-lookup"><span data-stu-id="6bdab-144">Auto Provisioning vs Manual Provisioning</span></span>
<span data-ttu-id="6bdab-145">若要啟用自動下載與註冊最新版程式碼的功能，請設定 Service Fabric 更新服務。</span><span class="sxs-lookup"><span data-stu-id="6bdab-145">To enable automatic downloading and registration for the latest code version, set up Service Fabric Update Service.</span></span> <span data-ttu-id="6bdab-146">請參閱[獨立封裝](service-fabric-cluster-standalone-package-contents.md)中的 Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt，以取得相關指示。</span><span class="sxs-lookup"><span data-stu-id="6bdab-146">Refer to the Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt inside the [Standalone Package](service-fabric-cluster-standalone-package-contents.md) for instructions.</span></span>
<span data-ttu-id="6bdab-147">如需進行手動程序，請遵循以下指示。</span><span class="sxs-lookup"><span data-stu-id="6bdab-147">For manual process, follow the instructions below.</span></span>

<span data-ttu-id="6bdab-148">請修改叢集組態以將下列屬性設定為 false，再開始進行組態升級。</span><span class="sxs-lookup"><span data-stu-id="6bdab-148">Modify your cluster configuration to set the following property to false before you start a configuration upgrade.</span></span>

        "fabricClusterAutoupgradeEnabled": false,

<span data-ttu-id="6bdab-149">請參閱 [Start-ServiceFabricClusterConfigurationUpgrade PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) 以取得使用方式詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6bdab-149">Refer to [Start-ServiceFabricClusterConfigurationUpgrade PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) for usage details.</span></span> <span data-ttu-id="6bdab-150">在您開始組態升級之前，請確實更新 JSON 中的 'clusterConfigurationVersion'。</span><span class="sxs-lookup"><span data-stu-id="6bdab-150">Make sure to update 'clusterConfigurationVersion' in your JSON before you start the configuration upgrade.</span></span>

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>

```

#### <a name="cluster-upgrade-workflow"></a><span data-ttu-id="6bdab-151">叢集升級工作流程</span><span class="sxs-lookup"><span data-stu-id="6bdab-151">Cluster upgrade workflow</span></span>

1. <span data-ttu-id="6bdab-152">從叢集中的其中一個節點執行 Get-ServiceFabricClusterUpgrade，並記下 TargetCodeVersion。</span><span class="sxs-lookup"><span data-stu-id="6bdab-152">Run Get-ServiceFabricClusterUpgrade from one of the nodes in the cluster and note the TargetCodeVersion.</span></span>
2. <span data-ttu-id="6bdab-153">從與網際網路連線的電腦執行下列程式碼，以根據目前版本列出所有升級相容版本 ，並從相關聯的下載連結下載對應封裝。</span><span class="sxs-lookup"><span data-stu-id="6bdab-153">Run the following from an internet connected machine to list all upgrade compatible versions with the current version and download the corresponding package from the associated download links.</span></span>

    ```powershell

    ###### Get list of all upgrade compatible packages  
    Get-ServiceFabricRuntimeUpgradeVersion -BaseVersion <TargetCodeVersion as noted in Step 1> 
    ```

3. <span data-ttu-id="6bdab-154">從具有系統管理員存取權的任何電腦，將叢集連接至列為叢集中節點的所有電腦。</span><span class="sxs-lookup"><span data-stu-id="6bdab-154">Connect to the cluster from any machine that has administrator access to all the machines that are listed as nodes in the cluster.</span></span> <span data-ttu-id="6bdab-155">執行此指令碼所在的電腦不一定是叢集的一部分</span><span class="sxs-lookup"><span data-stu-id="6bdab-155">The machine that this script is run on does not have to be part of the cluster</span></span>

    ```powershell

   ###### Get the list of available Service Fabric versions
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath <name of the .cab file including the path to it> -ImageStoreConnectionString "fabric:ImageStore"

   ###### Here is a filled-out example
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath .\MicrosoftAzureServiceFabric.5.3.301.9590.cab -ImageStoreConnectionString "fabric:ImageStore"

    ```
4. <span data-ttu-id="6bdab-156">將下載的套件複製到叢集映像存放區。</span><span class="sxs-lookup"><span data-stu-id="6bdab-156">Copy the downloaded package into the cluster image store.</span></span>

5. <span data-ttu-id="6bdab-157">註冊所複製的套件。</span><span class="sxs-lookup"><span data-stu-id="6bdab-157">Register the copied package.</span></span>

    ```powershell

    ###### Get the list of available Service Fabric versions
    Register-ServiceFabricClusterPackage -Code -CodePackagePath <name of the .cab file>

    ###### Here is a filled-out example
    Register-ServiceFabricClusterPackage -Code -CodePackagePath MicrosoftAzureServiceFabric.5.3.301.9590.cab

     ```
6. <span data-ttu-id="6bdab-158">開始將叢集升級為可用版本。</span><span class="sxs-lookup"><span data-stu-id="6bdab-158">Start a cluster upgrade to an available version.</span></span>

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example
    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   <span data-ttu-id="6bdab-159">您可以在 Service Fabric Explorer 上或執行下列 Power Shell 命令來監視升級進度。</span><span class="sxs-lookup"><span data-stu-id="6bdab-159">You can monitor the progress of the upgrade on Service Fabric Explorer, or you can run the following PowerShell command.</span></span>

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    <span data-ttu-id="6bdab-160">如果不符合叢集健康狀態原則，則會回復升級。</span><span class="sxs-lookup"><span data-stu-id="6bdab-160">If the cluster health policies are not met, the upgrade is rolled back.</span></span> <span data-ttu-id="6bdab-161">若要為 **Start-ServiceFabricClusterUpgrade** 命令指定自訂的健康狀態原則，請參閱 [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) 的文件。</span><span class="sxs-lookup"><span data-stu-id="6bdab-161">To specify custom health policies for the **Start-ServiceFabricClusterUpgrade** command, see the documentation for [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span></span>

<span data-ttu-id="6bdab-162">在解決導致復原的問題後，請依照先前所述的相同步驟再次起始升級。</span><span class="sxs-lookup"><span data-stu-id="6bdab-162">After you fix the issues that resulted in the rollback, initiate the upgrade again by following the same steps as previously described.</span></span>


## <a name="upgrade-the-cluster-configuration"></a><span data-ttu-id="6bdab-163">升級叢集組態</span><span class="sxs-lookup"><span data-stu-id="6bdab-163">Upgrade the cluster configuration</span></span>
<span data-ttu-id="6bdab-164">起始組態升級之前，您可以執行獨立封裝中的 powershell 指令碼來對新叢集組態 json 進行測試。</span><span class="sxs-lookup"><span data-stu-id="6bdab-164">Before you initiate the configuration upgrade, you can test your new cluster configuration json by running the powershell script in the standalone package.</span></span>

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path to the new Configuration File> -OldClusterConfigFilePath <Path to the old Configuration File>

```
<span data-ttu-id="6bdab-165">或</span><span class="sxs-lookup"><span data-stu-id="6bdab-165">or</span></span>

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path to the new Configuration File> -OldClusterConfigFilePath <Path to the old Configuration File> -FabricRuntimePackagePath <Path to the .cab file which you want to test the configuration against>

```

<span data-ttu-id="6bdab-166">某些組態無法升級，例如端點、叢集名稱、節點 IP 等。這將會對照舊的叢集組態 json 測試新的叢集組態 json，如有任何問題，會在 Powershell 視窗中擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="6bdab-166">Some configurations can't be upgraded, such as endpoints, cluster name, node IP, etc. This will test the new cluster configuration json against the old one and throw errors in the Powershell window if there is any issue.</span></span>

<span data-ttu-id="6bdab-167">若要升級叢集組態升級，請執行 **Start-ServiceFabricClusterConfigurationUpgrade**。</span><span class="sxs-lookup"><span data-stu-id="6bdab-167">To upgrade the cluster configuration upgrade, run **Start-ServiceFabricClusterConfigurationUpgrade**.</span></span> <span data-ttu-id="6bdab-168">組態升級是按升級網域逐一處理。</span><span class="sxs-lookup"><span data-stu-id="6bdab-168">The configuration upgrade is processed upgrade domain by upgrade domain.</span></span>

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>

```

### <a name="cluster-certificate-config-upgrade"></a><span data-ttu-id="6bdab-169">叢集憑證組態升級</span><span class="sxs-lookup"><span data-stu-id="6bdab-169">Cluster certificate config upgrade</span></span>  
<span data-ttu-id="6bdab-170">叢集憑證是用來在叢集節點之間進行驗證，所以執行憑證變換應更加謹慎，因為失敗將會封鎖叢集節點之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="6bdab-170">Cluster certificate is used for authentication between cluster nodes, so the certificate roll over should be performed with extra caution because failure will block the communication among cluster nodes.</span></span>  
<span data-ttu-id="6bdab-171">從技術角度來看，支援三個選項：</span><span class="sxs-lookup"><span data-stu-id="6bdab-171">Technically, three options are supported:</span></span>  

1. <span data-ttu-id="6bdab-172">單一憑證升級：升級路徑為「憑證 A (主要) -> 憑證 B (主要) -> 憑證 C (主要) -> ...」。</span><span class="sxs-lookup"><span data-stu-id="6bdab-172">Single certificate upgrade: The upgrade path is 'Certificate A (Primary) -> Certificate B (Primary) -> Certificate C (Primary) -> ...'.</span></span>   
2. <span data-ttu-id="6bdab-173">雙重憑證升級：升級路徑為「憑證 A (主要) -> 憑證 A (主要) 和 B (次要) -> 憑證 B (主要) -> 憑證 B (主要) 和 C (次要) -> 憑證 C (主要) -> ...」。</span><span class="sxs-lookup"><span data-stu-id="6bdab-173">Double certificate upgrade: The upgrade path is 'Certificate A (Primary) -> Certificate A (Primary) and B (Secondary) -> Certificate B (Primary) -> Certificate B (Primary) and C (Secondary) -> Certificate C (Primary) -> ...'.</span></span>
3. <span data-ttu-id="6bdab-174">憑證類型升級：指紋型憑證設定 <-> CommonName 型憑證設定。</span><span class="sxs-lookup"><span data-stu-id="6bdab-174">Certificate type upgrade: Thumbprint-based certificate configuration <-> CommonName-based certificate configuration.</span></span> <span data-ttu-id="6bdab-175">例如，憑證指紋 A (主要) 和指紋 B (次要) -> 憑證 CommonName C。</span><span class="sxs-lookup"><span data-stu-id="6bdab-175">For example, Certificate Thumbprint A (Primary) and Thumbprint B (Secondary) -> Certificate CommonName C.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6bdab-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6bdab-176">Next steps</span></span>
* <span data-ttu-id="6bdab-177">了解如何自訂一些 [Service Fabric 叢集設定](service-fabric-cluster-fabric-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="6bdab-177">Learn how to customize some [Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>
* <span data-ttu-id="6bdab-178">了解如何[相應放大和相應縮小叢集](service-fabric-cluster-scale-up-down.md)。</span><span class="sxs-lookup"><span data-stu-id="6bdab-178">Learn how to [scale your cluster in and out](service-fabric-cluster-scale-up-down.md).</span></span>
* <span data-ttu-id="6bdab-179">了解[應用程式升級](service-fabric-application-upgrade.md)。</span><span class="sxs-lookup"><span data-stu-id="6bdab-179">Learn about [application upgrades](service-fabric-application-upgrade.md).</span></span>

<!--Image references-->
[getfabversions]: ./media/service-fabric-cluster-upgrade-windows-server/getfabversions.PNG
