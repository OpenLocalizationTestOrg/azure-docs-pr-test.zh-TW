---
title: "服務網狀架構獨立叢集部署準備 aaaAzure |Microsoft 文件"
description: "建立 hello 叢集設定時，toobe 考慮先前 toodeploying 叢集用於處理生產工作負載以及相關 toopreparing hello 環境的文件集。"
services: service-fabric
documentationcenter: .net
author: maburlik
manager: timlt
editor: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 1/17/2017
ms.author: maburlik;chackdan
ms.openlocfilehash: e503c61a64b408af3f22bd75ab02f1c34ac9f380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
<a id="preparemachines"></a>

## <a name="plan-and-prepare-your-service-fabric-standalone-cluster-deployment"></a>規劃和準備您的 Service Fabric 獨立叢集部署
執行下列步驟，建立您的叢集之前的 hello。

### <a name="step-1-plan-your-cluster-infrastructure"></a>步驟 1︰規劃叢集基礎結構
您即將 toocreate Service Fabric 叢集，您所擁有的電腦上讓您可以決定何種失敗想 hello 叢集 toosurvive。 例如，您需要不同的電源線或網際網路連線提供 toothese 機器？ 此外，請考慮 hello 這些機器的實體安全性。 Hello 機器位於何處，以及需要哪些人存取 toothem？ 進行這些決定之後，您可以以邏輯方式對應 hello 機器 toohello （請參閱步驟 4） 的不同容錯網域。 實際執行叢集規劃 hello 基礎結構會比測試叢集的更為複雜。

### <a name="step-2-prepare-hello-machines-toomeet-hello-prerequisites"></a>步驟 2： 準備 hello 機器 toomeet hello 必要條件
每一部電腦的必要條件，您會想 tooadd toohello 叢集：

* 建議至少 16 GB RAM。
* 建議至少 40 GB 的可用磁碟空間。
* 建議 4 核心或以上的 CPU。
* 連線 tooa 安全的網路或網路上的所有機器。
* Windows Server 2012 R2 或 Windows Server 2016。 
* [.NET Framework 4.5.1 或更高版本](https://www.microsoft.com/download/details.aspx?id=40773)，完整安裝。
* [Windows PowerShell 3.0](https://msdn.microsoft.com/powershell/scripting/setup/installing-windows-powershell)。
* hello[遠端登錄服務](https://technet.microsoft.com/library/cc754820)應該 hello 的所有電腦上執行。

hello 叢集系統管理員部署和設定 hello 叢集必須有[系統管理員權限](https://social.technet.microsoft.com/wiki/contents/articles/13436.windows-server-2012-how-to-add-an-account-to-a-local-administrator-group.aspx)每部 hello 電腦上。 您無法在網域控制站上安裝 Service Fabric。

### <a name="step-3-determine-hello-initial-cluster-size"></a>步驟 3： 決定 hello 最初的叢集大小
獨立 Service Fabric 叢集中的每個節點都 hello Service Fabric 執行階段部署，hello 叢集的成員。 在一般生產部署中，每個作業系統執行個體 (實體或虛擬) 都有一個節點。 hello 叢集大小取決於您的業務需求。 不過，您必須有三個節點 (電腦或虛擬機器) 的最小叢集大小。
基於開發目的，在一部指定的電腦上可以有多個節點。 在生產環境中，對於每個實體或虛擬機器，Service Fabric 只支援一個節點。

### <a name="step-4-determine-hello-number-of-fault-domains-and-upgrade-domains"></a>步驟 4： 決定 hello 數目容錯網域和升級網域
A*容錯網域*(FD) 失敗的實體單位，而直接相關的 toohello hello 資料中心內實體基礎結構。 容錯網域是由共用單一失敗點的硬體元件 (電腦、交換器、網路等) 所組成。 雖然容錯網域和機架之間沒有 1:1 對應，但是大致上來說，可以將每個機架視為一個容錯網域。 在考慮 hello 叢集中的節點時，我們強烈建議 hello 節點會散佈到至少三個容錯網域。

當您指定 Fd 如此時，您可以選擇每個 FD hello 名稱。 Service Fabric 支援階層式 FD，因此，您可以在 FD 中反映您的基礎結構拓撲。  例如，下列 Fd hello 是有效的：

* "faultDomain": "fd:/Room1/Rack1/Machine1"
* "faultDomain": "fd:/FD1"
* "faultDomain": "fd:/Room1/Rack1/PDU1/M1"

*升級網域* (UD) 是節點的邏輯單元。 Service Fabric 協調在升級期間 （應用程式升級或叢集升級），UD 中的所有節點會都被降 tooperform hello 升級，但在其他 Ud 節點仍保持可用 tooserve 要求。 hello 您執行您的電腦的韌體升級不接受 Ud，因此您必須執行這些其中一個電腦一次。

hello 最簡單方式 toothink 有關這些概念是 tooconsider Fd hello 未計劃的失敗和單位 Ud 當做 hello 的計劃性維護的單位。

當您指定 Ud 如此時，您可以選擇每個 UD hello 名稱。 例如，下列名稱的 hello 是有效的：

* "upgradeDomain": "UD0"
* "upgradeDomain": "UD1A"
* "upgradeDomain": "DomainRed"
* "upgradeDomain": "Blue"

如需升級網域和容錯網域的詳細資訊，請參閱[描述 Service Fabric 叢集](service-fabric-cluster-resource-manager-cluster-description.md)。

### <a name="step-5-download-hello-service-fabric-standalone-package-for-windows-server"></a>步驟 5： 下載適用於 Windows Server hello Service Fabric 獨立封裝
[下載連結的 Service Fabric 獨立封裝的 Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)並解壓縮 hello 封裝，任一 tooa 部署機器也就不是屬於 hello 叢集或 tooone 的 hello 機器將成為叢集的一部分。

### <a name="step-6-modify-cluster-configuration"></a>步驟 6︰修改叢集組態
toocreate 您擁有 toocreate 獨立叢集設定追蹤檔案，其中描述 hello 規格 hello 叢集的獨立叢集。 您可以根據 hello 範本，請參閱下面的連結 hello hello 設定檔。 <br>
[獨立叢集組態](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)

如需這個檔案中的 hello 區段的詳細資訊，請參閱[獨立 Windows 叢集的組態設定](service-fabric-cluster-manifest.md)。

開啟其中一個 hello 追蹤檔案從您下載的 hello 封裝，並修改下列設定的 hello:
| **組態設定** | **說明** |
| --- | --- |
| **NodeTypes** |節點型別可讓您 tooseparate 成不同群組的叢集節點。 一個叢集至少必須有一個節點類型。 在群組中的所有節點都有 hello 遵循共同的特性： <br> **名稱**-這是 hello 節點類型名稱。 <br>**Endpoint Ports** - 這些是與這個節點類型相關聯的各種具名端點 (連接埠)。 您可以使用任何您想，只要未與此資訊清單中的其他任何項目發生衝突，並不存在於任何 hello 機器/VM 上執行的應用程式所使用的通訊埠編號。 <br> **放置屬性**-其中說明您用於作為位置限制 hello 系統服務或您的服務此節點類型的屬性。 這些屬性是使用者定義的索引鍵/值組，可針對指定節點提供額外的中繼資料。 節點屬性的範例是 hello 節點是否有硬碟機或圖形卡、 hello 的磁針數中的硬碟機、 核心和其他實體的屬性。 <br> **容量**-節點容量定義 hello 名稱和特定資源數量確認特定的節點都有可供取用。 例如，節點可能會定義它具有名為 "MemoryInMb" 的度量容量，而且預設有 2048 MB 的可用記憶體。 這些容量會用在執行階段 tooensure，需要特定的大量資源的服務節點上的位置 hello，具有這些 hello 中可用的資源需要金額。<br>**IsPrimary** -如果您有多個定義的 NodeType 確定只有一個已設定 hello 值 tooprimary *true*，也就是 services hello 系統執行。 所有其他節點型別應該設定 toohello 值*false* |
| **Nodes** |這些是 hello 的每個屬於 hello 叢集 （節點型別、 節點名稱、 IP 位址、 容錯網域和升級網域的 hello 節點） 的 hello 節點的詳細資料。 hello 機器想 hello 叢集 toobe 需要 toobe 此處列出其 IP 位址上建立。 <br> 如果您使用的 hello 建立所有 hello 節點，則其中一個方塊叢集相同的 IP 位址時，您可以基於測試目的使用。 不要使用一整體叢集部署生產工作負載。 |

Hello 叢集組態中有了所有設定 toohello 環境後，可以針對 hello （步驟 7） 的叢集環境進行測試。

<a id="environmentsetup"></a>

### <a name="step-7-environment-setup"></a>步驟 7. 環境設定

在叢集系統管理員設定獨立 Service Fabric 叢集，hello 環境時需要 toobe 設置 hello 下列準則： <br>
1. 建立 hello 叢集的 hello 使用者必須具備系統管理員層級的安全性權限 tooall 機器列為 hello 叢集組態檔中的節點。
2. 電腦中的 hello 建立叢集，以及每個叢集節點電腦必須：
* 已將 Service Fabric SDK 解除安裝
* 已將 Service Fabric 執行階段解除安裝 
* Hello Windows 防火牆服務 (mpssvc) 啟用
* 已啟用的 hello 遠端登錄服務 (remoteregistry)
* 已啟用檔案共用 (SMB)
* 已根據叢集組態的連接埠，開啟必要的連接埠
* 已經開啟 Windows SMB 和遠端登錄服務的必要通訊埠︰135、137、138、139 和 445
* 具有網路連線 tooone 另一個
3. 無 hello 叢集節點電腦應該是網域控制站。
4. 如果部署的 hello 叢集 toobe 是安全的叢集，驗證 hello 必要條件已位置，以及針對 hello 組態已正確設定必要的安全性。
5. Hello 叢集機器並不是可存取網際網路時，如果在 hello 組 hello 下列叢集設定：
* 停用遙測：在 *properties* 下設定 *"enableTelemetry": false*
* 停用自動網狀架構版本下載該 hello 目前叢集版本即將結束支援的通知： 下*屬性*設定*"fabricClusterAutoupgradeEnabled": false*
* 或者如果有限的 toowhite 列出網域網路存取網際網路，以下的 hello 網域所需的自動升級： go.microsoft.com download.microsoft.com

6. 設定適當的 Service Fabric 防毒排除項目︰

| **防毒排除目錄** |
| --- |
| Program Files\Microsoft Service Fabric |
| FabricDataRoot (從叢集組態) |
| FabricLogRoot (從叢集組態) |

| **防毒排除處理序** |
| --- |
| Fabric.exe |
| FabricHost.exe |
| FabricInstallerService.exe |
| FabricSetup.exe |
| FabricDeployer.exe |
| ImageBuilder.exe |
| FabricGateway.exe |
| FabricDCA.exe |
| FabricFAS.exe |
| FabricUOS.exe |
| FabricRM.exe |
| FileStoreService.exe |

### <a name="step-8-validate-environment-using-testconfiguration-script"></a>步驟 8。 使用 TestConfiguration 指令碼驗證環境
hello 獨立封裝中可以找到 hello TestConfiguration.ps1 指令碼。 它是做為最佳做法分析程式 toovalidate 上述 hello 條件部分，應該用於為例行性檢查 toovalidate 是否可供指定的環境上部署叢集。 如果有任何失敗，請參閱底下 toohello 清單[環境設定](service-fabric-cluster-standalone-deployment-preparation.md)進行疑難排解。 

此指令碼可以在任何電腦具有系統管理員存取 tooall hello 機器列為 hello 叢集組態檔中的節點上執行。 hello 機器上執行此指令碼並沒有 toobe hello 叢集的一部分。

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
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

目前此組態的測試模組並不會驗證 hello 安全性設定，因此這會有 toobe 獨立完成。  

> [!NOTE]
> 我們會持續改良 toomake 此模組來說更為完整，因此如果沒有錯誤或遺漏案例您認為這不目前攔截 TestConfiguration，請讓我們知道透過我們[支援通道](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support)。   
> 
> 

## <a name="next-steps"></a>後續步驟
* [建立在 Windows Server 上執行的獨立叢集](service-fabric-cluster-creation-for-windows-server.md)
