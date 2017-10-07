---
title: "aaaAdd 或移除節點 tooa 獨立 Service Fabric 叢集 |Microsoft 文件"
description: "了解 tooadd 或移除節點 tooan Azure Service Fabric 叢集化的實體或虛擬機器執行 Windows Server，可能是在內部部署上，或在任何雲端中。"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: bc6b8fc0-d2af-42f8-a164-58538be38d02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 2/02/2017
ms.author: dekapur
ms.openlocfilehash: 1da908ad9840faa052e0b4021bc2d4ce732b02bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-nodes-tooa-standalone-service-fabric-cluster-running-on-windows-server"></a>新增或移除 Windows Server 上執行的節點 tooa 獨立 Service Fabric 叢集
之後[Windows Server 機器上建立獨立 Service Fabric 叢集](service-fabric-cluster-creation-for-windows-server.md)可能會變更您的業務需求，您可能需要 tooadd 或移除節點 tooyour 叢集。 本文章提供詳細的步驟 tooachieve 這。 請注意，在本機開發叢集中，不支援新增/移除節點功能。

## <a name="add-nodes-tooyour-cluster"></a>新增節點 tooyour 叢集
1. 準備 hello 想依照 hello hello 中所述的步驟 tooadd tooyour 叢集的 VM/機器[準備 hello 的電腦上的叢集部署的 toomeet hello 必要條件](service-fabric-cluster-creation-for-windows-server.md)區段
2. 識別哪些容錯網域和升級網域會持續 tooadd 此 VM/機器
3. 遠端桌面 (RDP) 至 hello 您想 tooadd toohello 叢集的 VM/電腦
4. 複製或[下載適用於 Windows Server 服務網狀架構 hello 獨立套件](http://go.microsoft.com/fwlink/?LinkId=730690)toohello VM/機器並將它解壓縮 hello 封裝
5. 執行 Powershell，使用提高的權限，並瀏覽 toohello hello 解壓縮封裝位置
6. 執行 hello *AddNode.ps1* hello 參數所描述新節點 tooadd hello 與指令碼。 hello 下面範例會將新的節點稱為 VM5，與類型 NodeType0 和 IP 位址 182.17.34.52，成 UD1 和 fd: / dc1/r0。 hello *ExistingClusterConnectionEndPoint*節點連接端點已在 hello 現有叢集中，它可以是 IP 位址 hello*任何*hello 叢集中的節點。

    ```
    .\AddNode.ps1 -NodeName VM5 -NodeType NodeType0 -NodeIPAddressorFQDN 182.17.34.52 -ExistingClientConnectionEndpoint 182.17.34.50:19000 -UpgradeDomain UD1 -FaultDomain fd:/dc1/r0 -AcceptEULA
    ```
    一旦 hello 指令碼完成執行時，您可以檢查是否已新增 hello 新節點執行 hello [Get ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet。

7. tooensure hello 叢集中不同節點之間的一致性，您必須起始組態升級。 執行[Get ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello 最新的組態檔，並加入 hello 新加入的節點太 「 節點 」 一節。 也建議 tooalways 具有 hello 最新叢集組態可用在 hello 情況下，您需要 tooredploy hello 與叢集相同的設定。

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
8. 執行[開始 ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello 升級。

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    您可以監視 hello Service Fabric 總管 hello 升級進度。 或者，您也可以執行 [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)

### <a name="add-nodes-tooclusters-configured-with-windows-security-using-gmsa"></a>新增節點 tooclusters 設定與使用 gMSA 的 Windows 安全性
針對已設定「群組受管理的服務帳戶」(gMSA)(https://technet.microsoft.com/library/hh831782.aspx) 的叢集，可以使用組態升級來新增新的節點：
1. 執行[Get ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps)上任何 hello 現有節點 tooget hello 最新的組態檔，並加入詳細資料 hello 一新節點中，您想 tooadd hello 「 節點 」 一節。 請確定 hello 新節點屬於相同的 hello 群組 「 受管理的帳戶。 此帳戶應該是所有機器上的「系統管理員」。

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
2. 執行[開始 ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello 升級。

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>
    ```
    您可以監視 hello Service Fabric 總管 hello 升級進度。 或者，您也可以執行 [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)

### <a name="add-node-types-tooyour-cluster"></a>新增節點型別 tooyour 叢集
在排序 tooadd 新的節點類型、 修改組態 tooinclude hello 新節點類型 「 屬性 」 底下的"NodeTypes 」 一節中並開始設定升級使用[開始 ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps)。 Hello 升級完成之後，您可以加入新的節點 tooyour 叢集與此節點類型。

## <a name="remove-nodes-from-your-cluster"></a>從叢集移除節點
可以從組態升級時，使用下列方式 hello 中的叢集移除節點：

1. 執行[Get ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello 最新的組態檔和*移除*hello 節點，從 「 節點 」 一節。
新增 「 NodesToBeRemoved"hello 參數太 「 安裝 」"FabricSettings 」 區段中的區段。 hello"value"應該是需要 toobe 移除的節點的節點名稱的逗號分隔清單。

    ```
         "fabricSettings": [
            {
            "name": "Setup",
            "parameters": [
                {
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
                },
                {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
                },
                {
                "name": "NodesToBeRemoved",
                "value": "vm0, vm1"
                }
            ]
            }
        ]
    ```
2. 執行[開始 ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello 升級。

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    您可以監視 hello Service Fabric 總管 hello 升級進度。 或者，您也可以執行 [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)

> [!NOTE]
> 移除節點可能會起始多個升級作業。 某些節點會標示`IsSeedNode=”true”`標記，並且可以由查詢 hello 叢集資訊清單使用`Get-ServiceFabricClusterManifest`。 因為 hello 種子節點必須在這種情況中移動 toobe，可能會超過其他這類節點移除。 hello 叢集必須維護 3 個主要節點類型節點的最小的值。
> 
> 

### <a name="remove-node-types-from-your-cluster"></a>從叢集移除節點類型
然後再移除節點型別，請檢查是否有任何參考 hello 節點類型的節點。 移除這些節點，然後再移除 hello 對應的節點類型。 一旦移除所有對應的節點，您可以從 hello 叢集組態移除 hello NodeType 並開始設定升級使用[開始 ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps)。


### <a name="replace-primary-nodes-of-your-cluster"></a>取代您叢集的主要節點
hello 取代主要節點應該在另一個，而不是移除，然後將加入批次之後執行的一個節點。


## <a name="next-steps"></a>後續步驟
* [獨立 Windows 叢集的組態設定](service-fabric-cluster-manifest.md)
* [使用 X509 憑證保護 Windows 上的獨立叢集](service-fabric-windows-cluster-x509-security.md)
* [建立具有執行 Windows 之 Azure VM 的獨立 Service Fabric 叢集](service-fabric-cluster-creation-with-windows-azure-vms.md)

