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
# <a name="upgrade-your-standalone-azure-service-fabric-on-windows-server-cluster"></a>在 Windows Server 叢集上升級獨立的 Azure Service Fabric
> [!div class="op_single_selector"]
> * [Azure 叢集](service-fabric-cluster-upgrade.md)
> * [獨立叢集](service-fabric-cluster-upgrade-windows-server.md)
>
>

針對任何現代系統 hello 能力 tooupgrade 是產品金鑰 toohello 長期成功。 Azure Service Fabric 叢集是您擁有的資源。 本文將告訴您如何可確保該 hello 叢集中一定會執行支援的版本的 Service Fabric 程式碼和組態。

## <a name="control-hello-service-fabric-version-that-runs-on-your-cluster"></a>在您的叢集執行的控制 hello Service Fabric 版本
tooset 叢集 toodownload 更新的 Service Fabric 當 Microsoft 發行新的版本，組 hello **fabricClusterAutoupgradeEnabled**叢集組態 tootrue。 Service Fabric 支援版本，您想在組 hello 您叢集 toobe tooselect **fabricClusterAutoupgradeEnabled**叢集組態 toofalse。

> [!NOTE]
> 請確定您的叢集一律執行支援的 Service Fabric 版本。 當 Microsoft 宣佈 hello 發行新版的 Service Fabric 時，hello 舊版標示為的支援即將結束之後從 hello 公告 hello 日期 60 天的最小值。 新的版本上經過宣布[hello Service Fabric 小組部落格上](https://blogs.msdn.microsoft.com/azureservicefabric/)。 hello 新版此時是使用 toochoose。
>
>

只有當您使用生產樣式節點設定後，每個 Service Fabric 節點的個別實體或虛擬機器上的配置位置，您可以升級叢集 toohello 的新版本。 如果您有開發叢集，其中多部 Service Fabric 節點都是單一實體或虛擬機器，您必須重新建立 hello 叢集 hello 新版本。

兩個不同的工作流程可以升級叢集 toohello 的最新版本或 Service Fabric 的支援的版本。 一個工作流程是在連線 toodownload hello 最新版本時自動的叢集。 hello 其他工作流程是沒有連線 toodownload hello 最新 Service Fabric 版本的叢集。

### <a name="upgrade-clusters-that-have-connectivity-toodownload-hello-latest-code-and-configuration"></a>升級叢集具有連線 toodownload hello 最新程式碼和組態
使用這些步驟 tooupgrade 您叢集 tooa 支援版本，如果您的叢集節點具有網際網路連線能力過[http://download.microsoft.com](http://download.microsoft.com)。

也有連線的叢集[http://download.microsoft.com](http://download.microsoft.com)，Microsoft 會定期檢查新的 Service Fabric 版本 hello 可用性。

新的 Service Fabric 版本可用時，要 toohello 叢集在本機下載 hello 封裝和升級的佈建。 此外，這個新版本的 tooinform hello 客戶，hello 系統顯示會類似下列的 toohello 明確叢集健全狀況警告：

"hello 目前叢集版本 [版本 #] 支援將結束 [Date]"。

Hello 叢集正在執行 hello 最新版本之後，會隨即消失 hello 警告。

#### <a name="cluster-upgrade-workflow"></a>叢集升級工作流程
您會看到 hello 叢集健全狀況警告之後，請勿 hello 遵循：

1. 從具有系統管理員存取 tooall hello 機器列為 hello 叢集中節點的任何電腦連接 toohello 叢集。 hello 機器上執行此指令碼並沒有 toobe hello 叢集的一部分。

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

2. 取得您可以升級到 Service Fabric 版本 hello 清單。

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Get-ServiceFabricRegisteredClusterCodeVersion
    ```

    您應該取得輸出類似 toothis:

    ![取得網狀架構版本][getfabversions]
3. 開始使用的叢集升級 tooan 可用版本[開始 ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) PowerShell cmd.

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   toomonitor hello hello 升級進度，您可以使用 Service Fabric 總管或執行下列 Windows PowerShell 命令的 hello。

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    如果不符合 hello 叢集健全狀況原則，會回復 hello 升級。 hello toospecify 自訂的健康情況原則**開始 ServiceFabricClusterUpgrade**命令，請參閱文件[開始 ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx)。

修正導致 hello 復原 hello 問題之後，相同的步驟如先前所述的下列 hello 起始 hello 升級一次。

### <a name="upgrade-clusters-that-have-uno-connectivityu-toodownload-hello-latest-code-and-configuration"></a>升級具有叢集<U>沒有連線</u>toodownload hello 最新的程式碼和組態
使用這些步驟 tooupgrade 您叢集 tooa 支援版本，如果您的叢集節點不太需要網際網路連線[http://download.microsoft.com](http://download.microsoft.com)。

> [!NOTE]
> 如果您正在執行不是連接的 toohello 網際網路的叢集，您必須 toomonitor hello Service Fabric 小組部落格 toolearn 有關新的版本。 hello 系統不會顯示叢集健全狀況警告 tooalert 您新的版本。  
>
>

#### <a name="auto-provisioning-vs-manual-provisioning"></a>自動佈建與手動佈建
tooenable 自動下載和註冊的 hello 最新的程式碼版本，設定網狀架構更新服務。 參考內 hello toohello Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt[獨立封裝](service-fabric-cluster-standalone-package-contents.md)如需相關指示。
手動程序，請遵循下列的 hello 指示。

修改下列屬性 toofalse 開始組態升級之前您叢集組態 tooset hello。

        "fabricClusterAutoupgradeEnabled": false,

請參閱太[開始 ServiceFabricClusterConfigurationUpgrade PS cmd](https://msdn.microsoft.com/en-us/library/mt788302.aspx)的使用方式詳細資料。 開始 hello 組態升級之前，請確定 tooupdate 'clusterConfigurationVersion' 在您的 JSON。

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

#### <a name="cluster-upgrade-workflow"></a>叢集升級工作流程

1. 執行 Get ServiceFabricClusterUpgrade 從其中一個 hello hello 叢集中的節點，並記下 hello TargetCodeVersion。
2. 從網際網路連線的機器 toolist 執行的 hello 下列所有升級與 hello 目前版本的相容版本，並下載 hello 對應從 hello 相關的下載連結的封裝。

    ```powershell

    ###### Get list of all upgrade compatible packages  
    Get-ServiceFabricRuntimeUpgradeVersion -BaseVersion <TargetCodeVersion as noted in Step 1> 
    ```

3. 從具有系統管理員存取 tooall hello 機器列為 hello 叢集中節點的任何電腦連接 toohello 叢集。 hello 電腦上執行此指令碼並沒有 toobe hello 叢集的一部分

    ```powershell

   ###### Get hello list of available Service Fabric versions
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file including hello path tooit> -ImageStoreConnectionString "fabric:ImageStore"

   ###### Here is a filled-out example
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath .\MicrosoftAzureServiceFabric.5.3.301.9590.cab -ImageStoreConnectionString "fabric:ImageStore"

    ```
4. 將下載的 hello 封裝複製到 hello 叢集映像存放區。

5. 註冊 hello 複製封裝。

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Register-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file>

    ###### Here is a filled-out example
    Register-ServiceFabricClusterPackage -Code -CodePackagePath MicrosoftAzureServiceFabric.5.3.301.9590.cab

     ```
6. 啟動叢集升級 tooan 可用版本。

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example
    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   您可以監視 hello 的 Service Fabric 總管，在 hello 升級的進度，或者您可以執行下列 PowerShell 命令的 hello。

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    如果不符合 hello 叢集健全狀況原則，會回復 hello 升級。 hello toospecify 自訂的健康情況原則**開始 ServiceFabricClusterUpgrade**命令，請參閱 hello 文件[開始 ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx)。

修正導致 hello 復原 hello 問題之後，相同的步驟如先前所述的下列 hello 起始 hello 升級一次。


## <a name="upgrade-hello-cluster-configuration"></a>升級 hello 叢集設定
起始 hello 組態升級之前，您可以測試您的新叢集組態 json hello 獨立封裝中執行 hello powershell 指令碼。

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File>

```
或

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File> -FabricRuntimePackagePath <Path toohello .cab file which you want tootest hello configuration against>

```

某些組態無法升級，例如端點、叢集名稱、節點 IP 等。這將會測試 hello 新叢集組態 json 針對 hello 舊的密碼，並擲回錯誤 hello Powershell 視窗中，如果有任何問題。

tooupgrade hello 叢集組態升級時，執行**開始 ServiceFabricClusterConfigurationUpgrade**。 hello 組態升級已處理的升級網域的升級網域。

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

### <a name="cluster-certificate-config-upgrade"></a>叢集憑證組態升級  
叢集的憑證會用於叢集節點之間的驗證，因此 hello 憑證變換執行時應該格外小心因為失敗將會封鎖 hello 的叢集節點之間的通訊。  
從技術角度來看，支援三個選項：  

1. 單一憑證升級： hello 的升級路徑是 ' 憑證 （主要）]-> [憑證 B （主要）]-> [憑證 C （主要）->...'。   
2. Double 憑證升級： hello 的升級路徑是 ' 憑證 （主要）]-> [憑證 （主要） 與 （次要） 的 B-憑證 B （主要）-> 憑證 B （主要） 與 C （次要）-憑證 C （主要）->...'。
3. 憑證類型升級：指紋型憑證設定 <-> CommonName 型憑證設定。 例如，憑證指紋 A (主要) 和指紋 B (次要) -> 憑證 CommonName C。


## <a name="next-steps"></a>後續步驟
* 深入了解如何 toocustomize 某些[Service Fabric 叢集設定](service-fabric-cluster-fabric-settings.md)。
* 了解如何太[叢集及相應放大](service-fabric-cluster-scale-up-down.md)。
* 了解[應用程式升級](service-fabric-application-upgrade.md)。

<!--Image references-->
[getfabversions]: ./media/service-fabric-cluster-upgrade-windows-server/getfabversions.PNG
