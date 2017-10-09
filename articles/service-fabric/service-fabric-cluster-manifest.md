---
title: "aaaConfigure 獨立 Azure Service Fabric 叢集 |Microsoft 文件"
description: "深入了解如何 tooconfigure 獨立] 或 [私用的 Service Fabric 叢集。"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 0c5ec720-8f70-40bd-9f86-cd07b84a219d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dekapur
ms.openlocfilehash: ce2ad387162a05668bbd3a271c754776fe471850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-settings-for-standalone-windows-cluster"></a>獨立 Windows 叢集的組態設定
本文說明如何 tooconfigure 獨立 Service Fabric 叢集使用 hello***追蹤***檔案。 您可以使用此檔案 toospecify 資訊如 hello Service Fabric 節點和其 IP 位址、 不同類型的節點上 hello 叢集、 hello 安全性組態，以及根據錯誤/升級網域的 hello 網路拓樸您獨立叢集。

當您[下載 hello 獨立 Service Fabric 封裝](service-fabric-cluster-creation-for-windows-server.md#downloadpackage)，hello 追蹤檔案的一些範例僅適用於下載的 tooyour 工作電腦。 具有 hello 範例*DevCluster*名稱中將協助您建立具有 hello 相同機器類似邏輯的節點上的所有三個節點的叢集。 在這三個節點中，至少必須將一個節點標示為主要節點。 此叢集可用於開發或測試環境，但不支援做為生產叢集。 具有 hello 範例*MultiMachine*在其名稱中，將協助您建立生產環境品質的叢集中，每個節點在不同電腦上。

1. *ClusterConfig.Unsecure.DevCluster.JSON*和*ClusterConfig.Unsecure.MultiMachine.JSON*顯示如何 toocreate 不安全的測試或實際執行分別的叢集。 
2. *ClusterConfig.Windows.DevCluster.JSON*和*ClusterConfig.Windows.MultiMachine.JSON*顯示 toocreate 測試或實際執行叢集如何保護使用[Windows 安全性](service-fabric-windows-cluster-windows-security.md)。
3. *ClusterConfig.X509.DevCluster.JSON*和*ClusterConfig.X509.MultiMachine.JSON*顯示 toocreate 測試或實際執行叢集如何保護使用[X509 憑證為基礎的安全性](service-fabric-windows-cluster-x509-security.md). 

現在我們將檢驗 hello 的各個不同區段***追蹤***檔案，如下所示。

## <a name="general-cluster-configurations"></a>一般叢集組態
這涵蓋 hello 廣泛叢集特定組態中，如以下的 hello JSON 片段所示。

    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "01-2017",

您可以藉由將其指派 toohello 授予任何易記名稱 tooyour Service Fabric 叢集**名稱**變數。 hello **clusterConfigurationVersion**是 hello 版本號碼的叢集，您應該增加每次您將 Service Fabric 叢集升級。 不過，您應該保留 hello **Microsoft.authorization** toohello 預設值。

<a id="clusternodes"></a>

## <a name="nodes-on-hello-cluster"></a>Hello 叢集上的節點
您也可以使用 hello Service Fabric 叢集上設定 hello 節點**節點**區段中的，為下列程式碼片段說明 hello。

    "nodes": [{
        "nodeName": "vm0",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType1",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType2",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],

Service Fabric 叢集至少必須包含 3 個節點。 根據您的設定，您可以加入多個節點 toothis 一節。 hello 下表說明每個節點的 hello 組態設定。

| **節點組態** | **說明** |
| --- | --- |
| nodeName |您可以提供易記名稱 toohello 的任何節點。 |
| iPAddress |找出您節點 hello IP 位址，以開啟命令視窗並鍵入`ipconfig`。 請注意 hello IPV4 位址，並將它指派 toohello **iPAddress**變數。 |
| nodeTypeRef |每個節點都可以指派不同的節點類型。 hello[節點型別](#nodetypes)hello 一節中所定義。 |
| faultDomain |容錯網域啟用叢集系統管理員 toodefine hello 實體節點可能會在 hello 失敗的相同時間到期，tooshared 實體的相依性。 |
| upgradeDomain |升級網域描述都已關閉的 Service Fabric 升級在 hello 關於相同的節點集的時間。 您可以選擇哪些節點 tooassign toowhich 升級網域，如未受到任何實體的需求。 |

## <a name="cluster-properties"></a>叢集屬性
hello**屬性**hello 追蹤 > 一節中是使用的 tooconfigure hello 叢集，如下所示。

<a id="reliability"></a>

### <a name="reliability"></a>可靠性
hello 概念**reliabilityLevel**定義 hello 複本的數目或 hello Service Fabric 系統服務可以在 hello 主要 hello 叢集節點上執行的執行個體。 它會決定這些服務的 hello 可靠性，並因此 hello 叢集。 hello 值為 hello 系統計算在叢集建立和升級時間。

### <a name="diagnostics"></a>診斷
hello **diagnosticsStore**區段可讓您 tooconfigure 參數 tooenable 診斷和疑難排解的節點或叢集失敗中 hello 下列程式碼片段所示。 

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
    }

hello**中繼資料**叢集診斷的描述，且可以根據您的安裝設定。 這些變數有助於收集 ETW 追蹤記錄檔、損毀傾印，以及效能計數器。 如需 ETW 追蹤記錄檔的詳細資訊，請參閱 [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) 和 [ETW 追蹤](https://msdn.microsoft.com/library/ms751538.aspx)。 包括的所有記錄檔[損毀傾印](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/)和[效能計數器](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx)可以導向的 toohello **connectionString**您的電腦上的資料夾。 您也可以使用 *AzureStorage* 儲存診斷。 請參閱下面的範例程式碼片段。

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "AzureStorage",
        "IsEncrypted": "false",
        "connectionstring": "xstore:DefaultEndpointsProtocol=https;AccountName=[AzureAccountName];AccountKey=[AzureAccountKey]"
    }

### <a name="security"></a>安全性
hello**安全性**區段是安全的獨立 Service Fabric 叢集所需。 hello 下列程式碼片段示範此區段的一部分。

    "security": {
        "metadata": "This cluster is secured using X509 certificates.",
        "ClusterCredentialType": "X509",
        "ServerCredentialType": "X509",
        . . .
    }

hello**中繼資料**安全叢集的描述，且可以根據您的安裝設定。 hello **ClusterCredentialType**和**ServerCredentialType**決定 hello hello 叢集和 hello 節點將實作的安全性類型。 您可以設定 tooeither *X509*憑證為基礎的安全性，或*Windows* Azure Active Directory 架構的安全性。 hello hello 的其餘部分**安全性**> 一節將根據 hello hello 安全性類型。 讀取[憑證為基礎的安全性，在獨立叢集中](service-fabric-windows-cluster-x509-security.md)或[獨立叢集中的 Windows 安全性](service-fabric-windows-cluster-windows-security.md)如需有關如何出 hello toofill 其餘部分的 hello 詳細**安全性**> 一節。

<a id="nodetypes"></a>

### <a name="node-types"></a>節點類型
hello **nodeTypes**章節描述您的叢集有的 hello 節點 hello 類型。 至少一個節點型別必須指定叢集，hello 以下程式碼片段所示。 

    "nodeTypes": [{
        "name": "NodeType0",
        "clientConnectionEndpointPort": "19000",
        "clusterConnectionEndpointPort": "19001",
        "leaseDriverEndpointPort": "19002"
        "serviceConnectionEndpointPort": "19003",
        "httpGatewayEndpointPort": "19080",
        "reverseProxyEndpointPort": "19081",
        "applicationPorts": {
            "startPort": "20575",
            "endPort": "20605"
        },
        "ephemeralPorts": {
            "startPort": "20606",
            "endPort": "20861"
        },
        "isPrimary": true
    }]

hello**名稱**是 hello 此特定節點類型的易記名稱。 toocreate 此節點類型節點，將指派其好記名稱 toohello **nodeTypeRef**變數對於該節點，如所述[上方](#clusternodes)。 每個節點類型，定義將用於 hello 連接端點。 您可以為這些連接端點選擇任意的連接埠號碼，只要它們不會與此叢集中的任何其他端點發生衝突即可。 在多節點叢集中，會有一或多個主要節點 (也就是**isPrimary**設定得*true*)，端視 hello [ **reliabilityLevel** ](#reliability). 讀取[Service Fabric 叢集的容量規劃考量](service-fabric-cluster-capacity.md)有關**nodeTypes**和**reliabilityLevel**，和 tooknow 哪些主要或 hello非主要節點類型。 

#### <a name="endpoints-used-tooconfigure-hello-node-types"></a>使用端點 tooconfigure hello 節點型別
* *clientConnectionEndpointPort*是 hello 使用 hello 用戶端應用程式開發介面時，hello 用戶端 tooconnect toohello 叢集所使用的連接埠。 
* *clusterConnectionEndpointPort* hello hello 節點彼此通訊的通訊埠。
* *leaseDriverEndpointPort*是使用 hello 叢集租用驅動程式 toofind 出 hello 節點是否仍在作用中的 hello 通訊埠。 
* *serviceConnectionEndpointPort* hello hello 應用程式所使用的連接埠及 toocommunicate hello Service Fabric 用戶端上該特定節點的節點上部署的服務。
* *httpGatewayEndpointPort*是 hello hello Service Fabric 總管 tooconnect toohello 叢集所使用的連接埠。
* *ephemeralPorts*覆寫 hello [hello 作業系統所使用的動態連接埠](https://support.microsoft.com/kb/929851)。 Service Fabric 將使用這些應用程式連接埠的一部分，而且可供 hello OS hello 剩餘。 它也會對應此範圍 toohello 現有範圍中 hello OS，因此所有進行中，您可以使用已知 hello 範例 JSON 檔案中的 hello 範圍。 您必須確定 hello 開始與 hello 端通訊埠的 hello 差異至少 255 toomake。 如果這項差異太低，因為與 hello 作業系統共用此範圍，則可能會發生衝突。 請參閱 hello 設定動態連接埠範圍，藉由執行`netsh int ipv4 show dynamicport tcp`。
* *applicationPorts* hello hello Service Fabric 應用程式將使用的連接埠。 hello 應用程式連接埠範圍應夠大 toocover hello 端點需求的應用程式。 此範圍應 hello 在電腦上，也就是 hello hello 動態連接埠範圍排除*ephemeralPorts* hello 組態中所設定的範圍。  服務網狀架構會使用這些新的連接埠為必要欄位，以及負責開啟這些連接埠的 hello 防火牆時。 
* reverseProxyEndpointPort 是選擇性的反向 Proxy 端點。 如需詳細資訊，請參閱 [Service Fabric 反向 Proxy](service-fabric-reverseproxy.md)。 

### <a name="log-settings"></a>記錄設定
hello **fabricSettings**區段可讓您 tooset hello 根 hello Service Fabric 資料與記錄檔目錄。 您可以自訂這些只在 hello 最初的叢集建立期間。 如需這個區段的範例程式碼片段，請參閱下列內容。

    "fabricSettings": [{
        "name": "Setup",
        "parameters": [{
            "name": "FabricDataRoot",
            "value": "C:\\ProgramData\\SF"
        }, {
            "name": "FabricLogRoot",
            "value": "C:\\ProgramData\\SF\\Log"
    }]

我們建議使用 hello FabricDataRoot 非作業系統磁碟機和 Clusterconfig.json，因為它提供更多的可靠性，對作業系統當機。 請注意，是否您自訂 hello 資料根目錄，然後 hello 記錄根將放置 hello 資料根目錄下的一個層級。

### <a name="stateful-reliable-service-settings"></a>具狀態可靠服務設定
hello **KtlLogger**區段可讓您的可靠服務 tooset hello 全域組態設定。 如需這些設定的詳細資訊，請參閱[設定具狀態可靠服務](service-fabric-reliable-services-configuration.md)。
hello 以下範例顯示如何 toochange hello hello 共用的交易記錄檔，取得會建立 tooback 可設定狀態服務的任何可靠的集合。

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="add-on-features"></a>附加元件功能
tooconfigure 附加元件的功能，hello api 版本應該是設定為 ' 04-2017' 或更高版本，而且 addonFeatures 需要 toobe 設定：

    "apiVersion": "04-2017",
    "properties": {
      "addOnFeatures": [
          "DnsService",
          "RepairManager"
      ]
    }

### <a name="container-support"></a>容器支援
windows server 容器和 hyper-v 容器的獨立式叢集 tooenable 容器支援，必須啟用 toobe hello 'DnsService' 附加元件功能。


## <a name="next-steps"></a>後續步驟
一旦您擁有完整的追蹤檔案，根據獨立的叢集安裝程式設定，您可以部署下列 hello 發行項所叢集[建立獨立 Service Fabric 叢集](service-fabric-cluster-creation-for-windows-server.md)，然後再繼續太[視覺化您的叢集，利用 Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)。

