---
title: "aaaCluster 資源管理員叢集描述 |Microsoft 文件"
description: "藉由指定容錯網域、 升級 」 網域，節點屬性，以及節點容量 hello 叢集資源管理員說明 Service Fabric 叢集。"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 55f8ab37-9399-4c9a-9e6c-d2d859de6766
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: f2822075976bd54402af5ad56991b5b360dfb1d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="describing-a-service-fabric-cluster"></a>描述 Service Fabric 叢集
hello Service Fabric 叢集資源管理員會提供數種機制，用來描述叢集。 在執行階段 hello 叢集資源管理員會使用此資訊 tooensure 高可用性的 hello 服務 hello 叢集中執行。 同時強制執行這些重要的規則，它也會嘗試 hello 叢集內的 toooptimize hello 資源耗用量。

## <a name="key-concepts"></a>重要概念
hello 叢集資源管理員支援數個特徵來描述叢集：

* 容錯網域
* 升級網域
* 節點屬性
* 節點容量

## <a name="fault-domains"></a>容錯網域
容錯網域是任何連鎖故障區域。 一部電腦是 「 故障 」 網域，（因為它可能無法在它自己的各種理由，從電源供應器失敗 toodrive 失敗 toobad NIC 韌體）。 機器相同的乙太網路交換器是能力的中的連接的 toohello hello 做為相同容錯網域，是能力的共用單一來源，或在單一位置的機器。 因為這是理所當然的硬體錯誤 toooverlap，容錯網域是原本就是以階層方式和它們以服務的網狀架構中的 Uri。

請務必確認容錯網域中正確設定了因為服務網狀架構會使用此資訊 toosafely 位置服務。 Service Fabric 不希望 tooplace 服務，例如 hello 遺失的 「 故障 」 網域 （某個元件的 hello 失敗所造成） 會導致服務 toogo 向下。 在 hello Azure Service Fabric 會使用所提供的 hello 環境 toocorrectly hello 容錯網域資訊的環境設定 hello hello 叢集中的節點代表您。 服務網狀架構獨立的容錯網域會定義在 hello 階段設定該 hello 叢集 

> [!WARNING]
> 請務必該 hello 容錯網域資訊提供 tooService 網狀架構的精確度。 例如，假設 Service Fabric 叢集是在 10 部虛擬機器上執行，這些虛擬機器是在五個實體主機上執行。 在此情況下，即使有 10 部虛擬機器，也只有 5 個不同的 (最上層) 容錯網域。 共用相同的實體主機造成的 hello Vm tooshare hello 相同的根容錯網域，因為 Vm 經驗 hello 協調失敗，其實體主機失敗時。  
>
> 因為 Service Fabric 需要 hello 不 toochange 節點的容錯網域。 確保高可用性的 hello 的 Vm，這類的其他機制[HA Vm](https://technet.microsoft.com/en-us/library/cc967323.aspx)，使用從一部主機 tooanother 透明移轉 Vm。 這些機制不要重新設定或通知 hello 執行 hello VM 內的程式碼。 因此，它們**不支援**作為執行中 Service Fabric 叢集的環境。 Service Fabric 應該採用的 hello 僅高可用性技術。 不需要像是即時 VM 移轉、SAN 或其他項目的機制。 如果與 Service Fabric 搭配使用，這些機制會_減少_應用程式可用性和可靠性，因為它們會導致額外的複雜性、新增集中式失敗來源，並且使用與 Service Fabric 衝突的可靠性和可用性策略。 
>
>

在 hello 圖所示我們色彩所有 hello 實體構成 tooFault 網域及清單所有 hello 所產生的不同容錯網域。 在此範例中，我們有資料中心 ("DC")、機架 ("R") 和刀鋒伺服器 ("B")。 理論上，如果每個刀鋒視窗會保留多個虛擬機器，可能有另一個圖層 hello 容錯網域階層中。

<center>
![透過容錯網域組織的節點][Image1]
</center>

在執行階段 hello Service Fabric 叢集資源管理員會考慮 hello hello 叢集中的容錯網域，並計劃配置。 hello 可設定狀態的複本或無狀態的執行個體指定服務的已發佈，讓它們位於不同的容錯網域。 容錯網域之間分散 hello 服務可確保在 hello 階層的任何層級的容錯網域失敗時，不會洩露 hello hello 服務可用性。

Service Fabric 叢集資源管理員不在意 hello 容錯網域階層中有多少層級。 不過，它會嘗試 hello 遺失 hello 階層中任何一個部分不會影響執行中服務的 tooensure。 

建議您最好有 hello 深度 hello 容錯網域階層中的每個層級的節點數目相同。 如果 hello 「 樹 」 的容錯網域是在叢集中不平衡，難 hello 叢集資源管理員 toofigure 出 hello 的服務的最佳配置。 不平衡的容錯網域配置表示的某些網域 hello 損失影響 hello 可用性的服務，比其他網域。 如此一來，兩個目標之間損毀 hello 叢集資源管理員： 它想要將服務放在他們的 toouse 「 大量 」 網域中的 hello 機器和其想 tooplace 其他網域中的服務，讓網域中的 hello 遺失並不會造成問題。 

不平衡網域外觀為何？ Hello 在圖中，我們會示範兩個不同的叢集配置。 在 hello 第一個範例中，hello 節點平均分佈在 hello 容錯網域。 Hello 第二個範例中，在一個 「 故障 」 網域會有許多節點 hello 超過其他容錯網域。 

<center>
![兩個不同的叢集配置][Image2]
</center>

在 Azure 中，為您管理的容錯網域包含節點的 hello 選擇。 不過，根據 hello 您佈建的節點數目您可以仍然得到容錯網域與它們比其他的多個節點。 例如，假設您有五個 hello 叢集中的容錯網域，但會以給定的 NodeType 佈建七個節點。 在此情況下，hello 前兩個容錯網域得到更多的節點。 如果您只有幾個執行個體與多個 NodeTypes 繼續 toodeploy，hello 問題取得較差。 基於這個理由，建議您該 hello 中每個節點類型的節點數目是 hello 容錯網域數目的倍數。

## <a name="upgrade-domains"></a>升級網域
升級網域是另一項功能，可協助 hello Service Fabric 叢集資源管理員了解 hello 叢集的 hello 版面配置。 升級網域會定義在 hello 升級的節點集相同的時間。 升級的網域說明 hello 叢集資源管理員了解，以及協調管理作業，例如升級。

升級網域非常類似容錯網域，但是有幾個主要的差異。 首先，協調硬體失敗的區域會定義容錯網域。 升級網域、 在 hello 相反，由原則所定義。 您取得 toodecide 多少想，而不是它聽寫 hello 環境。 您可能會有與節點一樣多的升級網域。 容錯網域和升級網域的另一個差異在於升級網域不是階層式。 相反地，它們更像是簡單的標記。 

hello 下列圖表顯示三個升級網域會等量分散於三個容錯網域。 其中也顯示不具狀態服務的三個不同複本有一個可能的位置，而每一個最後都在不同的容錯網域和升級網域。 這個位置可讓 「 故障 」 網域中的服務升級的 hello 中間時的 hello 遺失，並且仍然擁有一份 hello 程式碼和資料。  

<center>
容錯網域和升級網域的位置![][Image3]
</center>

有優缺點 toohaving 大量的升級網域。 多個升級網域代表 hello 升級的每個步驟是更精細，因此會影響較少的節點或服務。 如此一來，較少的服務有 toomove 一次引入 hello 系統較少變換。 這通常會 tooimprove 可靠性，因為小於 hello 服務在 hello 升級過程中引用的任何問題所致。 多個升級網域也表示您需要較少的 hello 其他節點 toohandle hello 影響上的可用緩衝區升級。 例如，如果您有五個升級網域，hello 節點中每個處理大約 20%的流量。 如果您需要關閉該升級網域 tootake 升級時，該負載通常需要 toogo 某處。 因為您有四個剩餘的升級網域，每一個都必須有 hello 總流量的大約 5%的空間。 多個升級網域會表示您需要較少的緩衝區 hello hello 叢集中節點上。 例如，請考慮如果您擁有 10 個升級網域。 在此情況下，每個 UD 會只處理 hello 總流量的大約 10%。 當透過 hello 叢集升級步驟時，每個網域只需要 toohave hello 總流量的大約 1.1%的空間。 多個升級網域通常可讓您 toorun 您在高使用率，因為您需要較低的保留容量的節點。 hello 也適用於容錯網域。  

有許多的 「 升級 」 網域 hello 缺點是升級傾向 tootake 長。 Service Fabric 等候一段時間之後升級網域會完成，而且會執行啟動 tooupgrade hello 之前檢查下一個。 這些延遲啟用偵測 hello 升級所導入，才會繼續執行 hello 升級的問題。 hello 代價是可接受的因為它會防止不正確的變更會影響到太多的 hello 服務一次。

升級網域太少有許多負面的副作用 - 當個別升級網域關閉來升級時，整體容量會有一大部分無法使用。 例如，若您只有三個升級網域，則一次就關閉大約 1/3 的整體服務或叢集容量。 因為您在叢集 toohandle hello 工作負載的 hello 其餘部分有 toohave 足夠的容量，一次向下有非常多的服務不需要這樣做。 維護該緩衝區表示這些節點在一般作業期間的負載比其他期間少。 這會增加執行您的服務中的 hello 成本。

沒有任何實際限制 toohello 總數錯誤 」 或 「 升級 」 網域環境中，或條件約束上重疊的方式。 話雖如此，有幾個常見模式：

- 1:1 對應的容錯網域和升級網域
- 每個節點 (實體或虛擬作業系統執行個體) 一個升級網域
- 其中 hello 容錯網域和升級網域形成矩陣與機器通常會執行下 hello 對角線"等量 」 或 「 矩陣 」 模型

<center>
![容錯網域和升級網域配置][Image4]
</center>

有沒有最佳回答哪些配置 toochoose，各有一些優點和缺點。 例如，hello 1FD:1UD 模型會是簡單 tooset 最多。 hello 1 的升級網域，每個節點的模型是最接近哪些人只是要使用。 在升級期間每個節點會獨立更新。 這是類似 toohow 少量的機器已在過去的 hello 手動升級。 

hello FD/UD 矩陣，其中 hello Fd 和 Ud 形成資料表，而節點都放置啟動沿著 hello 對角線 hello 最常見的模型。 這是預設會在 Azure 中的 Service Fabric 叢集所使用的 hello 模型。 對具有許多節點的叢集的所有項目最後會看起來就像是上述的 hello 密集矩陣模式。

## <a name="fault-and-upgrade-domain-constraints-and-resulting-behavior"></a>容錯網域和升級網域的條件約束和導致的行為
hello 叢集資源管理員會將 hello desire tookeep 服務平衡故障 」 和 「 升級 」 網域做為條件約束。 您可以在 [這篇文章](service-fabric-cluster-resource-manager-management-integration.md)中深入了解條件約束。 hello 容錯和升級網域的條件約束狀態: 「 指定的服務資料分割應該不會在發現差異*大於一*在 hello 的服務物件 （無狀態服務執行個體或可設定狀態的服務複本）兩個網域。 」 這可防止違反這個條件約束的特定移動或排列方式。

讓我們來看看一個範例。 假設我們的叢集有六個節點，且已設定五個容錯網域和五個升級網域。

|  | FD0 | FD1 | FD2 | FD3 | FD4 |
| --- |:---:|:---:|:---:|:---:|:---:|
| **UD0** |N1 | | | | |
| **UD1** |N6 |N2 | | | |
| **UD2** | | |N3 | | |
| **UD3** | | | |N4 | |
| **UD4** | | | | |N5 |

現在假設我們建立 TargetReplicaSetSize (或者對於無狀態服務是 InstanceCount) 為五的服務。 N1 N5 進入 hello 複本。 事實上，不論建立多少像這樣的服務，都不會用到 N6。 原因為何？ 讓我們看看 hello 目前的配置和選擇 N6，則會發生什麼事的 hello 差異。

以下是我們了及 hello 複本，每個容錯和升級網域總數的 hello 版面配置：

|  | FD0 | FD1 | FD2 | FD3 | FD4 | UDTotal |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| **UD0** |R1 | | | | |1 |
| **UD1** | |R2 | | | |1 |
| **UD2** | | |R3 | | |1 |
| **UD3** | | | |R4 | |1 |
| **UD4** | | | | |R5 |1 |
| **FDTotal** |1 |1 |1 |1 |1 |- |

就每個容錯網域和升級網域的節點數而論，在此配置達到平衡。 它也是由平衡 hello 數的每個容錯和升級網域的複本。 每個網域有節點數目相同的 hello 和 hello 相同數目的複本。

現在，讓我們看看改用 N6 而不使用 N2 的情況。 會 hello 複本要如何散發然後？

|  | FD0 | FD1 | FD2 | FD3 | FD4 | UDTotal |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| **UD0** |R1 | | | | |1 |
| **UD1** |R5 | | | | |1 |
| **UD2** | | |R2 | | |1 |
| **UD3** | | | |R3 | |1 |
| **UD4** | | | | |R4 |1 |
| **FDTotal** |2 |0 |1 |1 |1 |- |

此配置命名為違反我們 hello 容錯網域條件約束的定義。 FD0 具有兩個複本，而 FD1 零，讓 hello FD0 和差異 FD1 總共有兩個。 hello 叢集資源管理員不允許這種排列方式。 同樣地，如果挑選 N2 和 N6 (而不是 N1 和 N2)，則會得到：

|  | FD0 | FD1 | FD2 | FD3 | FD4 | UDTotal |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| **UD0** | | | | | |0 |
| **UD1** |R5 |R1 | | | |2 |
| **UD2** | | |R2 | | |1 |
| **UD3** | | | |R3 | |1 |
| **UD4** | | | | |R4 |1 |
| **FDTotal** |1 |1 |1 |1 |1 |- |

此配置就容錯網域而言是平衡的。 不過，現在它會違反 hello 升級網域條件約束。 這是因為 UD0 有零個複本，而 UD1 有兩個複本。 因此，此配置命名為也不正確，而且不會挑選 hello 叢集資源管理員所。 

## <a name="configuring-fault-and-upgrade-domains"></a>設定容錯網域和升級網域
Azure 託管的 Service Fabric 部署中會自動定義容錯網域和升級網域。 Service Fabric 拾取，並使用從 Azure 的 hello 環境資訊。

如果您正在建立您自己的叢集 （或想 toorun 特定拓撲中開發），您可以自行提供 hello 容錯網域和升級網域的資訊。 在此範例中，我們定義本機開發叢集，具有九個節點，且跨越三個「資料中心」(各有三個機架)。 此叢集也有三個升級網域等量分散於這些三個資料中心。 Hello 組態的範例如下： 

ClusterManifest.xml

```xml
  <Infrastructure>
    <!-- IsScaleMin indicates that this cluster runs on one-box /one single server -->
    <WindowsServer IsScaleMin="true">
      <NodeList>
        <Node NodeName="Node01" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType01" FaultDomain="fd:/DC01/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node02" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType02" FaultDomain="fd:/DC01/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node03" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType03" FaultDomain="fd:/DC01/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
        <Node NodeName="Node04" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType04" FaultDomain="fd:/DC02/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node05" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType05" FaultDomain="fd:/DC02/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node06" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType06" FaultDomain="fd:/DC02/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
        <Node NodeName="Node07" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType07" FaultDomain="fd:/DC03/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node08" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType08" FaultDomain="fd:/DC03/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node09" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType09" FaultDomain="fd:/DC03/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
      </NodeList>
    </WindowsServer>
  </Infrastructure>
```

獨立部署透過 ClusterConfig.json

```json
"nodes": [
  {
    "nodeName": "vm1",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm2",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm3",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD3"
  },
  {
    "nodeName": "vm4",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm5",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm6",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD3"
  },
  {
    "nodeName": "vm7",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm8",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm9",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD3"
  }
],
```

> [!NOTE]
> 透過 Azure Resource Manager 定義叢集時，容錯網域和升級網域會由 Azure 指派。 因此，Azure Resource Manager 範本中的 hello 定義的節點型別和虛擬機器規模集不包含容錯網域 」 或 「 升級 」 網域資訊。
>

## <a name="node-properties-and-placement-constraints"></a>節點屬性和放置條件約束
您有時 （事實上，大部分的 hello 時間） 將只在特定類型的 hello 叢集中的節點執行某些工作負載的 toowant tooensure。 例如，某些工作負載可能需要 GPU 或 SSD，而有些則不用。 目標硬體 tooparticular 工作負載的絕佳範例是有幾乎每個多層式架構。 特定電腦做為 hello 前端或 API 伺服端 hello 應用程式和公開的 toohello 用戶端或 hello 網際網路。 不同的電腦，通常會使用不同的硬體資源，且處理 hello 運算或儲存層的 hello 工作。 這些通常是_不_直接公開 tooclients 或 hello 網際網路。 Service Fabric 需要有特定的工作負載需要特定硬體組態上的 toorun 情況。 例如：

* 現有的多層式架構應用程式已「提升並移轉」到 Service Fabric 環境
* 工作負載需要 toorun 於特定硬體的效能、 小數位數或隔離的理由
* 基於原則或資源耗用量的理由，工作負載應該彼此隔離

toosupport 組態，這類服務網狀架構有可以套用的 toonodes 標記的第一個類別的概念。 這些標記稱為**節點屬性**。 **位置條件約束**是 hello 陳述式附加 tooindividual 服務選取一或多個節點的屬性。 放置條件約束會定義應該執行服務的位置。 hello 一組條件約束可延伸-任何索引鍵/值組可以運作。 

<center>
![叢集配置不同工作負載][Image5]
</center>

### <a name="built-in-node-properties"></a>內建節點屬性
服務網狀架構定義可以自動使用不含 hello 使用者具有 toodefine 某些預設節點屬性它們。 hello 預設屬性，定義每個節點是 hello **NodeType**和 hello **NodeName**。 例如，您可以將放置條件約束撰寫成 `"(NodeType == NodeType03)"`。 通常我們找到了 NodeType toobe hello 最常使用的屬性之一。 因為它與機器類型的對應是 1:1，所以很有用。 機器的每個型別對應 tooa 傳統的多層式架構應用程式中的工作負載類型。

<center>
![放置條件約束和節點屬性][Image6]
</center>

## <a name="placement-constraint-and-node-property-syntax"></a>放置條件約束和節點屬性語法 
hello hello 節點屬性中指定的值可以是字串，bool，或帶正負號長時間。 在 hello 服務的 hello 陳述式會呼叫放置*條件約束*因為它會限制 hello 服務可讓 hello 叢集中執行。 hello 條件約束可以是任何 hello hello 叢集中的另一個節點屬性運作的布林陳述式。 這些布林值的陳述式中的 hello 有效選取器為：

1) 建立特定陳述式的條件式檢查

| 陳述式 | 語法 |
| --- |:---:|
| 「等於」 | "==" |
| 「不等於」 | "!=" |
| 「大於」 | ">" |
| 「大於或等於」 | ">=" |
| 「小於」 | "<" |
| 「小於或等於」 | "<=" |

2) 分組和邏輯運算的布林值陳述式

| 陳述式 | 語法 |
| --- |:---:|
| 「和」 | "&&" |
| 「或」 | "&#124;&#124;" |
| 「否」 | "!" |
| 「組成單一陳述式」 | "()" |

以下是基本條件約束陳述式的一些範例。

  * `"Value >= 5"`
  * `"NodeColor != green"`
  * `"((OneProperty < 100) || ((AnotherProperty == false) && (OneProperty >= 100)))"`

只有其中 hello 整體放置 constraint 陳述式會評估太"，則為 True 」 的節點可以有 hello 置於其上的服務。 未定義屬性的節點不符合包含該屬性的任何放置條件約束。

假設該屬性定義指定的節點類型的節點的後的 hello:

ClusterManifest.xml

```xml
    <NodeType Name="NodeType01">
      <PlacementProperties>
        <Property Name="HasSSD" Value="true"/>
        <Property Name="NodeColor" Value="green"/>
        <Property Name="SomeProperty" Value="5"/>
      </PlacementProperties>
    </NodeType>
```

獨立部署透過 ClusterConfig.json，Azure 託管叢集透過 Template.json。 

> [!NOTE]
> 在您的 Azure Resource Manager 範本 hello 節點型別通常已參數化。 它看起來會是 "[parameters('vmNodeType1Name')]"，而不是 "NodeType01"。
>

```json
"nodeTypes": [
    {
        "name": "NodeType01",
        "placementProperties": {
            "HasSSD": "true",
            "NodeColor": "green",
            "SomeProperty": "5"
        },
    }
],
```

您可以針對服務建立服務放置「條件約束」，如下所示︰

C#

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
serviceDescription.PlacementConstraints = "(HasSSD == true && SomeProperty >= 4)";
// add other required servicedescription fields
//...
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

PowerShell：

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceType -Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementConstraint "HasSSD == true && SomeProperty >= 4"
```

如果 NodeType01 的所有節點都是有效的您也可以選取該節點型別中的 hello 條件約束"(NodeType == NodeType01)"。

其中一個 hello 酷事情，關於服務的位置限制式是可以進行更新以動態方式在執行階段。 因此如果需要您可以在 hello 叢集移動服務、 加入和移除需求等。Service Fabric 會負責確保，hello 服務停留和可用即使當這類的變更進行。

C#：

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.PlacementConstraints = "NodeType == NodeType01";
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/app/service"), updateDescription);
```

PowerShell：

```posh
Update-ServiceFabricService -Stateful -ServiceName $serviceName -PlacementConstraints "NodeType == NodeType01"
```

放置條件約束會針對每個不同的具名服務執行個體指定。 更新一定要進行 hello 取代 （覆寫） 先前指定什麼。

hello 叢集定義定義 hello 屬性節點上。 變更節點的屬性需要叢集設定升級。 升級的節點屬性需要每個受影響的節點 toorestart tooreport 其新的屬性。 這些輪流升級是由 Service Fabric 管理。

## <a name="describing-and-managing-cluster-resources"></a>描述與管理叢集資源
其中一個最重要的任何 orchestrator 工作是 toohelp hello 管理 hello 叢集中的資源耗用量。 管理叢集資源可以表示幾個不同的項目。 首先，確保電腦不會多載。 這表示確定電腦不會執行比它們能夠處理還多的服務。 第二，也無需平衡即重大 toorunning 服務有效率地最佳化。 符合成本的效益或效能的敏感服務供應項目不允許某些節點 toobe 熱有些則是陌生。 Tooresource 競爭與效能不佳，和冷節點代表浪費資源並增加的成本，會導致最忙碌的節點。 

Service Fabric 以 `Metrics` 表示資源。 度量資訊是您想 toodescribe tooService 網狀架構的任何邏輯或實體資源。 度量的範例是例如「WorkQueueDepth」或「MemoryInMb」的項目。 在節點上 hello Service Fabric 可以管理的實體資源的相關資訊，請參閱[資源控管](service-fabric-resource-governance.md)。 如需設定自訂計量及其用法的相關資訊，請參閱[這篇文章](service-fabric-cluster-resource-manager-metrics.md)

計量不同於放置條件約束和節點屬性。 節點屬性都是靜態的描述元的 hello 節點本身。 計量說明節點所擁有的資源，以及在節點上執行時取用的服務。 節點屬性可以是"HasSSD 」，而且無法將設定 tootrue 或 false。 hello 數量的可用空間的 SSD 和多少由服務上是類似"DriveSpaceInMb 」 的度量。 

如同位置條件約束和節點屬性 hello Service Fabric 叢集資源管理員不了解哪些 hello 的名稱 hello 度量的平均值的重要 toonote 它。 計量名稱只是字串。 它是很好的作法 toodeclare 單位可能是模稜兩可時，您建立的 hello 度量名稱的一部分。

## <a name="capacity"></a>容量
如果您關閉所有資源「平衡」，Service Fabric 的叢集資源管理員仍會確保節點不超出其容量。 管理容量溢位是可能的除非 hello 叢集已滿或 hello 工作負載大於任何節點。 容量是另一個*條件約束*該 hello 叢集資源管理員會使用 toounderstand 有多少節點的資源。 剩餘容量也會追蹤 hello 叢集的整體。 度量都以表示 hello 容量和 hello hello 服務層級的耗用量。 例如，hello 度量可能"ClientConnections 」，而且在指定的節點可能有 「 ClientConnections"32768 的容量。 其他節點可以有一些服務，可以為節點上執行假設它目前耗用 32256 hello 標準 「 ClientConnections 」 的其他限制。

在執行階段 hello 叢集資源管理員會追蹤剩餘容量 hello 叢集中，並在節點上。 在順序 tootrack 容量 hello 叢集資源管理員會減去每個服務的使用方式從 hello 服務執行所在之節點的容量。 利用此資訊，hello Service Fabric 叢集資源管理員可找出哪裡 tooplace 或移動複本，讓節點不討論容量。

<center>
![叢集節點和容量][Image7]
</center>

C#：

```csharp
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
ServiceLoadMetricDescription metric = new ServiceLoadMetricDescription();
metric.Name = "ClientConnections";
metric.PrimaryDefaultLoad = 1024;
metric.SecondaryDefaultLoad = 0;
metric.Weight = ServiceLoadMetricWeight.High;
serviceDescription.Metrics.Add(metric);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

PowerShell：

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("ClientConnections,High,1024,0)
```

您可以看到 hello 叢集資訊清單中定義的容量：

ClusterManifest.xml

```xml
    <NodeType Name="NodeType03">
      <Capacities>
        <Capacity Name="ClientConnections" Value="65536"/>
      </Capacities>
    </NodeType>
```

獨立部署透過 ClusterConfig.json，Azure 託管叢集透過 Template.json。 

```json
"nodeTypes": [
    {
        "name": "NodeType03",
        "capacities": {
            "ClientConnections": "65536",
        }
    }
],
```

服務的負載通常會動態變更。 說出複本的負載"ClientConnections 」 的變更從 1024 too2048，但是它上執行，則只有該標準剩餘的 512 容量 hello 節點。 現在，該複本或執行個體的放置已無效，因為該節點上沒有足夠的空間。 hello 叢集資源管理員中有 tookick 和取得回下方容量 hello 節點。 它可減少從該節點 tooother 節點移動一或多個 hello 複本或執行個體是透過容量的 hello 節點上的負載。 當您移動複本，hello 叢集資源管理員會嘗試這些移動 toominimize hello 成本。 移動成本述[本文](service-fabric-cluster-resource-manager-movement-cost.md)更多有關 hello 叢集資源管理員的重新平衡策略和規則描述[這裡](service-fabric-cluster-resource-manager-metrics.md)。

## <a name="cluster-capacity"></a>叢集容量
如何沒有 hello Service Fabric 叢集資源管理員保留 hello 整體叢集不要太滿？ 使用動態負載的話，它並沒有太多可以執行的工作。 服務可以有獨立 hello 叢集資源管理員所採取的動作其負載突然增加。 因此，您的叢集今天有充足的空餘空間，明天就可能因為出名而後繼無力。 話雖如此，還有一些會燒 tooprevent 問題的控制項。 我們可以進行 hello 第一件事是防止 hello 建立新的工作負載，可能導致 hello 叢集 toobecome 完整。

假設您建立無狀態服務，而它有一些與它相關聯的負載。 讓我們假設 hello 服務重視 hello"DiskSpaceInMb"度量。 我們也假設它是 「 DiskSpaceInMb 「 每個執行個體的 hello 服務的持續 tooconsume 五個單位。 您想 toocreate hello 服務的三個執行個體。 太棒了！ 如此一來，表示我們需要 15 單位 」 DiskSpaceInMb"toobe hello 叢集中，為了讓我們 tooeven 是無法 toocreate 這些服務執行個體。 hello 叢集資源管理員持續計算 hello 容量和每個度量的耗用量，因此它可以判斷 hello hello 叢集中的剩餘容量。 如果沒有足夠的空間，叢集資源管理員拒絕 hello hello 建立服務呼叫。

由於 hello 需求，但是有可用 15 的單位，此空間無法配置許多不同的方式。 例如，15 個不同節點上可能剩餘一個單位的容量，或五個不同節點上剩餘三個單位的容量。 如果 hello 叢集資源管理員可以重新排列項目，讓三個節點上有可用的五個單位的就會將 hello 服務。 除非 hello 叢集幾乎已滿或無法合併 hello 現有服務，因為某些原因，是通常可以重新排列 hello 叢集。

## <a name="buffered-capacity"></a>緩衝處理的容量
緩衝的容量是 hello 的另一項功能叢集資源管理員。 它可讓 hello 的某些部分的保留整體節點容量。 這個容量緩衝區是唯一使用的 tooplace services 升級和節點失敗時。 緩衝處理的容量是針對所有節點的每個計量進行全域指定。 您挑選 hello 保留容量的 hello 值為 hello 容錯和您擁有 hello 叢集中的升級網域數目的函式。 容錯網域和升級網域越多，表示您可以挑選較小的緩衝容量。 如果您有多個網域，您可以升級與失敗時，預期較少量的叢集 toobe 無法使用。 指定緩衝處理的容量才有意義如果您另有指定的 hello 節點容量標準。

以下是如何 toospecify 緩衝處理容量的範例：

ClusterManifest.xml

```xml
        <Section Name="NodeBufferPercentage">
            <Parameter Name="SomeMetric" Value="0.15" />
            <Parameter Name="SomeOtherMetric" Value="0.20" />
        </Section>
```

獨立部署透過 ClusterConfig.json，Azure 託管叢集透過 Template.json：

```json
"fabricSettings": [
  {
    "name": "NodeBufferPercentage",
    "parameters": [
      {
          "name": "SomeMetric",
          "value": "0.15"
      },
      {
          "name": "SomeOtherMetric",
          "value": "0.20"
      }
    ]
  }
]
```

hello 叢集超出標準緩衝容量時，就會失敗 hello 建立新的服務。 防止 hello 建立新的服務 toopreserve hello 緩衝區，可確保的升級和失敗不會使節點 toogo 低於產能。 緩衝容量是選擇性，但建議用在已定義計量容量的任何叢集。

hello 叢集資源管理員會公開此載入資訊。 對於每個計量，這項資訊包括： 
  - hello 緩衝處理的容量設定
  - hello 總容量
  - hello 目前的耗用量
  - 每個計量是否被視為平衡
  - hello 標準差的相關統計資料
  - 具有大部分和最少負載 hello hello 節點  
  
我們可以看到該輸出的範例如下︰

```posh
PS C:\Users\user> Get-ServiceFabricClusterLoadInformation
LastBalancingStartTimeUtc : 9/1/2016 12:54:59 AM
LastBalancingEndTimeUtc   : 9/1/2016 12:54:59 AM
LoadMetricInformation     :
                            LoadMetricName        : Metric1
                            IsBalancedBefore      : False
                            IsBalancedAfter       : False
                            DeviationBefore       : 0.192450089729875
                            DeviationAfter        : 0.192450089729875
                            BalancingThreshold    : 1
                            Action                : NoActionNeeded
                            ActivityThreshold     : 0
                            ClusterCapacity       : 189
                            ClusterLoad           : 45
                            ClusterRemainingCapacity : 144
                            NodeBufferPercentage  : 10
                            ClusterBufferedCapacity : 170
                            ClusterRemainingBufferedCapacity : 125
                            ClusterCapacityViolation : False
                            MinNodeLoadValue      : 0
                            MinNodeLoadNodeId     : 3ea71e8e01f4b0999b121abcbf27d74d
                            MaxNodeLoadValue      : 15
                            MaxNodeLoadNodeId     : 2cc648b6770be1bc9824fa995d5b68b1
```

## <a name="next-steps"></a>後續步驟
* 如 hello 叢集資源管理員中的 hello 架構和資訊流程的相關資訊，請參閱[這篇文章](service-fabric-cluster-resource-manager-architecture.md)
* 定義磁碟重組度量資訊是其中一種方式 tooconsolidate 負載，而不是分配的節點上。toolearn 如何 tooconfigure 磁碟重組，請參閱太[這篇文章](service-fabric-cluster-resource-manager-defragmentation-metrics.md)
* Hello 從頭開始並[取得簡介 toohello Service Fabric 叢集資源管理員](service-fabric-cluster-resource-manager-introduction.md)
* toofind 出 hello 叢集資源管理員如何管理和 hello 叢集中的負載平衡簽出 hello 發行項上[平衡負載](service-fabric-cluster-resource-manager-balancing.md)

[Image1]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-domains.png
[Image2]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-uneven-fault-domain-layout.png
[Image3]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-and-upgrade-domains-with-placement.png
[Image4]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-and-upgrade-domain-layout-strategies.png
[Image5]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-layout-different-workloads.png
[Image6]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-placement-constraints-node-properties.png
[Image7]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-nodes-and-capacity.png
