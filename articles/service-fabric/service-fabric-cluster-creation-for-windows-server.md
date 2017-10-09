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
# <a name="create-a-standalone-cluster-running-on-windows-server"></a>建立在 Windows Server 上執行的獨立叢集
您可以在任何虛擬機器或執行 Windows Server 的電腦上使用 Azure Service Fabric toocreate Service Fabric 叢集。 這表示您能夠在包含一組互連式 Windows Server 電腦的任何環境中部署和執行 Service Fabric 應用程式，不論該環境是內部部署或是透過任何雲端提供者來提供。 Service Fabric 提供 Service Fabric 叢集安裝程式封裝 toocreate 稱為 hello 獨立 Windows 伺服器封裝。

這篇文章會引導您建立獨立 Service Fabric 叢集 hello 步驟。

> [!NOTE]
> 此獨立 Windows Server 套件已正式上市，可使用於生產部署。 此套件包含處於「預覽」狀態的新 Service Fabric 功能。 向下捲動太"[預覽功能，此封裝中包含](#previewfeatures_anchor)。 」 一節，以 hello 清單 hello 預覽功能。 您可以[下載一份 hello EULA](http://go.microsoft.com/fwlink/?LinkID=733084)現在。
> 
> 

<a id="getsupport"></a>

## <a name="get-support-for-hello-service-fabric-for-windows-server-package"></a>取得 hello 網狀架構的 Windows Server 的服務封裝的支援
* 詢問 hello 社群 hello Service Fabric 獨立封裝適用於 Windows Server 中 hello [Azure Service Fabric 論壇](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?)。
* 向 [Service Fabric 的專業支援](http://support.microsoft.com/oas/default.aspx?prid=16146)開立票證。  [在這裡](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0)深入了解 Microsoft 的專業支援。
* 您也可以取得此封裝的支援做為 [Microsoft 頂級支援](https://support.microsoft.com/en-us/premier)的一部分。
* 如需詳細資訊，請參閱 [Azure Service Fabric 支援選項](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support)。
* toocollect 記錄檔以取得支援的目的，執行 hello[服務網狀架構獨立記錄檔收集器](service-fabric-cluster-standalone-package-contents.md)。

<a id="downloadpackage"></a>

## <a name="download-hello-service-fabric-for-windows-server-package"></a>下載 hello 適用於 Windows Server Service Fabric 封裝
toocreate hello 叢集中，使用 hello 網狀架構的 Windows Server 的服務套件 (Windows Server 2012 R2 及更新版本)，請參閱： <br>
[下載連結 - Service Fabric 獨立封裝 - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)

找到 hello 套件內容的詳細資訊[這裡](service-fabric-cluster-standalone-package-contents.md)。

在叢集建立時，會自動下載 hello Service Fabric 執行階段封裝。 如果部署從機器未連接 toohello 網際網路，請從這裡下載 hello 超出訊號範圍的執行階段封裝： <br>
[下載連結 - Service Fabric 執行階段 - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)

獨立叢集組態範例在此︰ <br>
[獨立叢集組態範例](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)

<a id="createcluster"></a>

## <a name="create-hello-cluster"></a>建立 hello 叢集
Service Fabric 可以部署的 tooa 一個機器開發叢集使用 hello *ClusterConfig.Unsecure.DevCluster.json*檔案中包含[範例](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)。

解除封裝 hello 獨立封裝 tooyour 機器，請複製 hello 範例組態檔 toohello 本機電腦，然後執行的 hello *CreateServiceFabricCluster.ps1*透過從 hello 獨立的系統管理員 PowerShell 工作階段的指令碼封裝的資料夾：
### <a name="step-1a-create-an-unsecured-local-development-cluster"></a>步驟 1A：建立不安全的本機開發叢集
```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

請參閱 hello 環境設定 > 一節[規劃並準備您的叢集部署](service-fabric-cluster-standalone-deployment-preparation.md)的疑難排解詳細資料。

如果您完成執行的開發案例，您可以藉由參考 toosteps 區段中的從 hello 機器移除 hello Service Fabric 叢集 」[移除叢集](#removecluster_anchor)"。 

### <a name="step-1b-create-a-multi-machine-cluster"></a>步驟 1B︰ 建立多部電腦的叢集
您已經完成 hello 規劃並準備步驟詳細資料在 hello 下面的連結，您之後可以準備 toocreate 您使用您的叢集設定檔的實際執行叢集。 <br>
[規劃及準備叢集部署](service-fabric-cluster-standalone-deployment-preparation.md)

1. 您已經撰寫執行 hello hello 組態檔進行驗證*TestConfiguration.ps1* hello 獨立套件資料夾的指令碼：  

    ```powershell
    .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.json
    ```

    您應該會看到如下的輸出： 如果傳回 hello 場"Passed"是"True"，例行性檢查已通過，並 hello 叢集尋找 toobe 可部署的 hello 輸入組態為基礎。

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

2. 建立 hello 叢集： 執行 hello *CreateServiceFabricCluster.ps1*指令碼 toodeploy hello hello 組態中的每部電腦上的 Service Fabric 叢集。 
    ```powershell
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -AcceptEULA
    ```

> [!NOTE]
> 部署追蹤會寫入 toohello VM/電腦已執行 hello CreateServiceFabricCluster.ps1 PowerShell 指令碼。 可以找到這些 hello 子資料夾 DeploymentTraces，以執行指令碼中的 hello hello 目錄為基礎。 toosee Service Fabric 是否正確部署 tooa 機器，尋找 hello FabricDataRoot 目錄中所述 hello 叢集組態檔 FabricSettings 區段 （依預設 c:\ProgramData\SF) 中的 hello 安裝檔案。 同時，也要能在 [工作管理員] 看到 FabricHost.exe 和 Fabric.exe 處理序正在執行中。
> 
> 

### <a name="step-1c-create-an-offline-internet-disconnected-cluster"></a>步驟 1 C：建立離線 (網際網路中斷連線的) 叢集
在叢集建立時，會自動下載 hello Service Fabric 執行階段封裝。 連接時，不部署叢集 toomachines toohello 網際網路，您將需要 toodownload hello Service Fabric 執行階段分別封裝並提供在叢集建立 hello 路徑 tooit。
hello 執行階段封裝可以分別下載，從另一部電腦連接 toohello 網際網路，在[下載連結的 Service Fabric 執行階段的 Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)。 複製您要部署的 hello 離線的叢集，並執行建立 hello 叢集 hello 執行階段封裝 toowhere`CreateServiceFabricCluster.ps1`以 hello`-FabricRuntimePackagePath`參數包含如下所示： 

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -FabricRuntimePackagePath .\MicrosoftAzureServiceFabric.cab
```
其中`.\ClusterConfig.json`和`.\MicrosoftAzureServiceFabric.cab`分別為 hello 路徑 toohello 叢集組態和 hello 執行階段.cab 檔案。


### <a name="step-2-connect-toohello-cluster"></a>步驟 2: Toohello 叢集連線
tooconnect tooa 安全叢集，請參閱[Service fabric toosecure 叢集連線](service-fabric-connect-to-secure-cluster.md)。

tooconnect tooan 不安全叢集，請執行下列 PowerShell 命令的 hello:

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <*IPAddressofaMachine*>:<Client connection end point port>
```
範例：
```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint 192.13.123.2345:19000
```
### <a name="step-3-bring-up-service-fabric-explorer"></a>步驟 3：啟動 Service Fabric Explorer
現在您可以利用 Service Fabric Explorer 直接向其中一個 hello 機器 http://localhost:19080/Explorer/index.html 或從遠端 http://&lt 連接 toohello 叢集*IPAddressofaMachine*>: 19080 /Explorer/index.html。

## <a name="add-and-remove-nodes"></a>新增和移除節點
您可以新增或移除節點 tooyour 獨立 Service Fabric 叢集，因為您的商務需求變更。 請參閱[新增或移除節點 tooa Service Fabric 獨立叢集](service-fabric-cluster-windows-server-add-remove-nodes.md)如需詳細步驟。

<a id="removecluster" name="removecluster_anchor"></a>
## <a name="remove-a-cluster"></a>刪除叢集
tooremove 叢集中，執行 hello *RemoveServiceFabricCluster.ps1* hello 套件資料夾並傳入 hello 路徑 toohello JSON 組態檔中的 PowerShell 指令碼。 您可以選擇性地指定 hello 刪除 hello 記錄檔的位置。

此指令碼可以在任何電腦具有系統管理員存取 tooall hello 機器列為 hello 叢集組態檔中的節點上執行。 hello 機器上執行此指令碼並沒有 toobe hello 叢集的一部分。

```
# Removes Service Fabric from each machine in hello configuration
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -Force
```

```
# Removes Service Fabric from hello current machine
.\CleanFabric.ps1
```

<a id="telemetry"></a>

## <a name="telemetry-data-collected-and-how-tooopt-out-of-it"></a>收集的遙測資料以及如何不使用 tooopt
預設為 hello 產品會收集 hello Service Fabric 使用量 tooimprove hello 產品遙測。 hello hello 安裝程式的一部分太檢查連線時才執行最佳做法分析程式[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1)。 如果它找不到，hello 安裝會失敗，除非您退出遙測。

1. hello 遙測管線會嘗試遵循資料太 tooupload hello[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1)每天一次。 它是最佳方式上傳並 hello 叢集 」 功能沒有任何影響。 hello 遙測才會傳送 hello 節點執行 hello 容錯移轉管理員主要。 沒有其他節點會傳送遙測。
2. hello 遙測組成 hello 下列：

* 服務數
* ServiceTypes 數目
* Applications 的數目
* ApplicationUpgrades 的數目
* FailoverUnits 的數目
* InBuildFailoverUnits 的數目
* UnhealthyFailoverUnits 的數目
* Replicas 的數目
* InBuildReplicas 的數目
* StandByReplicas 的數目
* OfflineReplicas 的數目
* CommonQueueLength
* QueryQueueLength
* FailoverUnitQueueLength
* CommitQueueLength
* Nodes 的數目
* IsContextComplete: True/False
* ClusterId︰這是針對每個叢集隨機產生的 GUID。
* ServiceFabricVersion
* Hello 虛擬機器或從哪些 hello 上傳遙測的機器的 IP 位址

toodisable 遙測 hello 太之後加入*屬性*在叢集組態中： *enableTelemetry: false*。

<a id="previewfeatures" name="previewfeatures_anchor"></a>

## <a name="preview-features-included-in-this-package"></a>此封裝包含的預覽功能
無。


> [!NOTE]
> 從新的 hello [GA 版的 Windows Server 的 hello 獨立叢集 (版本 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/)，您可以手動或自動升級叢集 toofuture 發行版本。 請參閱太[升級獨立 Service Fabric 叢集版本](service-fabric-cluster-upgrade-windows-server.md)文件以取得詳細資料。
> 
> 

## <a name="next-steps"></a>後續步驟
* [使用 PowerShell 部署與移除應用程式](service-fabric-deploy-remove-applications.md)
* [獨立 Windows 叢集的組態設定](service-fabric-cluster-manifest.md)
* [新增或移除節點 tooa 獨立 Service Fabric 叢集](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [獨立 Service Fabric 叢集版本升級](service-fabric-cluster-upgrade-windows-server.md)
* [建立具有執行 Windows 之 Azure VM 的獨立 Service Fabric 叢集](service-fabric-cluster-creation-with-windows-azure-vms.md)
* [使用 Windows 安全性保護 Windows 上的獨立叢集](service-fabric-windows-cluster-windows-security.md)
* [使用 X509 憑證保護 Windows 上的獨立叢集](service-fabric-windows-cluster-x509-security.md)

<!--Image references-->
[Trusted Zone]: ./media/service-fabric-cluster-creation-for-windows-server/TrustedZone.png
