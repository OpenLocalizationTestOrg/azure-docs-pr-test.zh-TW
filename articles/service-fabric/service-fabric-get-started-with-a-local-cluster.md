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
# <a name="get-started-with-deploying-and-upgrading-applications-on-your-local-cluster"></a>在您的本機叢集上開始部署和升級應用程式
hello Azure Service Fabric SDK 包含的完整本機開發環境，您可以使用 tooquickly 開始部署及管理本機叢集上的應用程式。 本文中，您可以建立本機叢集，部署現有的應用程式 tooit，然後再升級應用程式 tooa 新的版本，所有從 Windows PowerShell。

> [!NOTE]
> 本文假設您已經 [設定開發環境](service-fabric-get-started.md)。
> 
> 

## <a name="create-a-local-cluster"></a>建立本機叢集
Service Fabric 叢集代表一組您可以部署應用程式的硬體資源。 一般而言，叢集所組成的任何位置從五個 toomany 數以千計的機器。 不過，hello Service Fabric SDK 包含可以在單一電腦執行的叢集設定。

請務必 toounderstand hello Service Fabric 本機叢集，並不是模擬器。 它執行 hello 多電腦叢集找到的相同平台程式碼。 hello 唯一的差異在於，它會執行 hello 平台的處理程序通常會分散到一部電腦上的五個機器。

hello SDK 提供本機叢集的兩個方式 tooset: Windows PowerShell 指令碼和 hello 本機叢集管理員 系統匣應用程式。 在此教學課程中，我們會使用 hello PowerShell 指令碼。

> [!NOTE]
> 如果您已藉由從 Visual Studio 部署應用程式來建立本機叢集，您可以略過本節。
> 
> 

1. 以系統管理員身分啟動新的 PowerShell 視窗。
2. 從 hello SDK 資料夾中執行 hello 叢集安裝指令碼：
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"
    ```
   
    叢集設定需要一些時間。 設定完成後，您應該會看到輸出類似於：
   
    ![叢集設定輸出][cluster-setup-success]
   
    現在您已經準備就緒 tootry 部署應用程式 tooyour 叢集。

## <a name="deploy-an-application"></a>部署應用程式
hello Service Fabric SDK 包含一組豐富的架構和開發人員工具建立應用程式。 如果您想要了解如何 toocreate 應用程式，在 Visual Studio 中，請參閱[Visual Studio 中建立 Service Fabric 應用程式第一次](service-fabric-create-your-first-application-in-visual-studio.md)。

在此教學課程中，您使用現有的範例應用程式 （稱為 WordCount），讓您可以專注於 hello 管理方面 hello 平台： 部署、 監視及升級。

1. 以系統管理員身分啟動新的 PowerShell 視窗。
2. 匯入 hello Service Fabric SDK PowerShell 模組。
   
    ```powershell
    Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
    ```
3. 建立會在下載及部署，例如 C:\ServiceFabric 目錄 toostore hello 應用程式。
   
    ```powershell
    mkdir c:\ServiceFabric\
    cd c:\ServiceFabric\
    ```
4. [下載 hello WordCount 應用程式](http://aka.ms/servicefabric-wordcountapp)toohello 您所建立的位置。  注意： hello Microsoft Edge 瀏覽器 hello 會將檔案儲存與*.zip*延伸模組。  也變更 hello 副檔名*.sfpkg*。
5. 連接 toohello 本機叢集：
   
    ```powershell
    Connect-ServiceFabricCluster localhost:19000
    ```
6. 建立新的應用程式使用的名稱和路徑 toohello 應用程式套件的 hello SDK 的部署命令。
   
    ```powershell  
   Publish-NewServiceFabricApplication -ApplicationPackagePath c:\ServiceFabric\WordCountV1.sfpkg -ApplicationName "fabric:/WordCount"
    ```
   
    如果一切順利，您應該會看到下列輸出的 hello:
   
    ![部署應用程式 toohello 本機叢集][deploy-app-to-local-cluster]
7. toosee hello 應用程式的動作，啟動 hello 瀏覽器，並瀏覽過[http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html)。 您應該會看到：
   
    ![部署應用程式 UI][deployed-app-ui]
   
    hello WordCount 應用程式很簡單。 它包含用戶端 JavaScript 程式碼 toogenerate 隨機五個字元"字組 」，然後是轉送 toohello 透過 ASP.NET Web API 的應用程式。 可設定狀態的服務會追蹤 hello 計算的字組的數目。 它們會分割 hello 的 hello word 的第一個字元為基礎。 您可以在 hello hello WordCount 應用程式找到 hello 原始程式碼[傳統使用者入門範例](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount)。
   
    我們所部署的 hello 應用程式包含四個資料分割。 以 A 到 G 開頭的單字會儲存在 hello 第一個資料分割，因此與透過 N H 開頭的單字會儲存在 hello 第二個資料分割，依此類推。

## <a name="view-application-details-and-status"></a>檢視應用程式詳細資料和狀態
既然我們已部署的 hello 應用程式，讓我們看看一些在 PowerShell 中的 hello 應用程式詳細資料。

1. 查詢 hello 叢集上的所有已部署應用程式：
   
    ```powershell
    Get-ServiceFabricApplication
    ```
   
    假設您只有部署 hello WordCount 應用程式，您會看到類似的項目：
   
    ![在 PowerShell 中查詢所有已部署的應用程式][ps-getsfapp]
2. 藉由查詢 hello 組包含在 hello WordCount 應用程式的服務移 toohello 下一個層級。
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![在 PowerShell 中的 hello 應用程式的清單服務][ps-getsfsvc]
   
    hello 應用程式是由兩個服務、 hello web 前端，hello 可設定狀態服務，可管理 hello 文字所組成。
3. 最後，查看 hello 清單的資料分割的 WordCountService:
   
    ```powershell
    Get-ServiceFabricPartition 'fabric:/WordCount/WordCountService'
    ```
   
    ![在 PowerShell 中檢視 hello 服務分割][ps-getsfpartitions]
   
    hello 的使用，例如所有 Service Fabric PowerShell 命令的命令集，您可能會連線至本機或遠端任何叢集無法進行。
   
    對於與 hello 叢集更視覺化的方式 toointeract，您可以使用 hello web 為基礎的 Service Fabric 總管工具瀏覽過[http://localhost:19080/總管](http://localhost:19080/Explorer)hello 瀏覽器中。
   
    ![在 Service Fabric 總管中檢視應用程式詳細資料][sfx-service-overview]
   
   > [!NOTE]
   > toolearn 進一步了解 Service Fabric 總管，請參閱[視覺化您的叢集，利用 Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)。
   > 
   > 

## <a name="upgrade-an-application"></a>升級應用程式
Service Fabric 提供無停機時間升級，藉由監視便會復原整個 hello 叢集 hello hello 應用程式的健全狀況。 執行 hello WordCount 應用程式的升級。

hello 新版 hello 應用程式現在會計算某個母音以開頭的單字。 因為 hello 升級中推出，我們會看到兩個 hello 應用程式的行為變更。 首先，hello 速率 hello 計數成長速率應該變慢，因為較少的字詞會被計算。 第二，由於 hello 第一個資料分割都有兩個母音 （A 和 E） 及所有其他資料分割只包含一個每個，計數應該最後開始 toooutpace hello 其他人。

1. [下載 hello WordCount 第 2 版封裝](http://aka.ms/servicefabric-wordcountappv2)toohello 下載 hello 第 1 版套件的相同位置。
2. 傳回 tooyour PowerShell 視窗，並使用 hello SDK tooregister hello hello 叢集中的新版本升級 命令。 然後開始升級 hello fabric: / WordCount 應用程式。
   
    ```powershell
    Publish-UpgradedServiceFabricApplication -ApplicationPackagePath C:\ServiceFabric\WordCountV2.sfpkg -ApplicationName "fabric:/WordCount" -UpgradeParameters @{"FailureAction"="Rollback"; "UpgradeReplicaSetCheckTimeout"=1; "Monitored"=$true; "Force"=$true}
    ```
   
    您應該會看到如 hello 升級輸出在 PowerShell 中的 hello 下列開始。
   
    ![在 PowerShell 中的升級進度][ps-appupgradeprogress]
3. 繼續 hello 升級時，您可能會發現它更容易 toomonitor 其狀態從 Service Fabric 總管。 啟動瀏覽器視窗並瀏覽過[http://localhost:19080/總管](http://localhost:19080/Explorer)。 展開**應用程式**在 hello 左側 hello 樹狀目錄，然後選擇  **WordCount**，最後再**fabric: / WordCount**。 Hello essentials 索引標籤中，您會看到 hello hello 升級狀態，透過 hello 叢集的升級網域進行時。
   
    ![在 Service Fabric 總管中的升級進度][sfx-upgradeprogress]
   
    Hello 升級繼續進行到每個網域，是執行的 hello 應用程式運作不正確的 tooensure 健康情況檢查。
4. 如果您重新執行 hello 先前查詢的 hello 組 hello 網狀架構中的服務: / WordCount 應用程式，請注意，hello WordCountService 版本已變更，但 hello WordCountWebService 版本不提供支援：
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![在升級後查詢應用程式服務][ps-getsfsvc-postupgrade]
   
    此範例強調 Service Fabric 如何管理應用程式升級。 它所接觸只有 hello 的一組服務 （或在這些服務的程式碼/組態套件） 已變更，會使升級更快速且更可靠的 hello 程序。
5. 最後，傳回 toohello hello 新版應用程式的瀏覽器 tooobserve hello 行為。 如預期般，速度變慢，hello 計數進展和 hello 第一個分割區最後會有稍微多個 hello 磁碟區。
   
    ![檢視 hello 新版本的 hello hello 瀏覽器中的應用程式][deployed-app-ui-v2]

## <a name="cleaning-up"></a>清除
包裝之前，這是很重要 hello 本機叢集的 tooremember 真實。 應用程式繼續 toorun hello 背景中，直到您將它們移除。  根據您的應用程式的 hello 本質，執行中應用程式可能佔用大量的資源，您的電腦上。 您有數個選項 toomanage 應用程式和 hello 叢集：

1. tooremove 個別的應用程式及其所有的資料，執行下列命令的 hello:
   
    ```powershell
    Unpublish-ServiceFabricApplication -ApplicationName "fabric:/WordCount"
    ```
   
    或者，您也可以從 hello Service Fabric 總管刪除 hello 應用程式**動作**功能表或 hello hello 左側的應用程式清單檢視中的內容功能表。
   
    ![在 Service Fabric 總管中刪除應用程式][sfe-delete-application]
2. 刪除之後 hello 應用程式從 hello 叢集中，移除註冊 1.0.0 和 2.0.0 的 hello WordCount 應用程式類型版本。 刪除作業會移除 hello 應用程式封裝，包括 hello 程式碼和組態，從 hello 叢集映像存放區。
   
    ```powershell
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 2.0.0
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 1.0.0
    ```
   
    或者，您也可以在 Service Fabric 總管] 中，選擇 [**解除佈建類型**hello 應用程式。
3. 按一下 向下 hello 叢集但保留 hello 應用程式資料，然後追蹤、 tooshut**停止本機叢集**hello 系統匣應用程式中。
4. 完全，按一下 toodelete hello 叢集**移除本機叢集**hello 系統匣應用程式中。 此選項將會導致其他慢速部署 hello 下次您在 Visual Studio 中按下 F5。 只有當您不想在 toouse 這段時間，或如果您需要 tooreclaim 資源，移除 hello 本機叢集。

## <a name="one-node-and-five-node-cluster-mode"></a>1 個節點和 5 個節點叢集模式
開發應用程式時，您常會發現自己快速反覆撰寫程式碼、偵錯、變更程式碼和偵錯。 toohelp 最佳化這個程序，hello 本機叢集可以執行兩種模式： 其中一個節點或五個節點。 這兩個叢集模式各有優點。 五個節點的叢集模式可讓您 toowork 與實際的叢集。 您可以測試容錯移轉案例，使用更多您的服務的執行個體和複本。 最佳化的 toodo 快速部署和註冊服務，toohelp 您快速驗證程式碼使用 hello Service Fabric 執行階段的單一節點叢集模式。

1 個節點叢集或 5 個節點叢集模式皆不是模擬器。 hello 本機開發叢集執行 hello 多電腦叢集找到的相同平台程式碼。

> [!WARNING]
> 當您變更 hello 叢集模式時，從系統移除 hello 目前叢集，並建立新的叢集。 當您變更叢集模式時，會刪除 hello hello 叢集中儲存的資料。
> 
> 

toochange hello 模式 tooone 節點的叢集，選取**切換叢集模式**hello 服務網狀架構本機叢集管理員中。

![切換叢集模式][switch-cluster-mode]

或者，使用 PowerShell 變更 hello 叢集模式：

1. 以系統管理員身分啟動新的 PowerShell 視窗。
2. 從 hello SDK 資料夾中執行 hello 叢集安裝指令碼：
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1" -CreateOneNodeCluster
    ```
   
    叢集設定需要一些時間。 設定完成後，您應該會看到輸出類似於：
   
    ![叢集設定輸出][cluster-setup-success-1-node]

## <a name="next-steps"></a>後續步驟
* 您現在已部署並升級某些預先建置的應用程式，您可以 [嘗試在 Visual Studio 中建立自己的應用程式](service-fabric-create-your-first-application-in-visual-studio.md)。
* 本文章中的 hello 本機叢集上執行的所有 hello 動作可都對[Azure 叢集概略](service-fabric-cluster-creation-via-portal.md)以及。
* 我們執行本文中的 hello 升級為基本。 請參閱 hello[升級文件](service-fabric-application-upgrade.md)toolearn 更多關於 hello 功能及彈性的 Service Fabric 升級。

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
