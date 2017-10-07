---
title: "服務網狀架構監視 aaaHealth |Microsoft 文件"
description: "簡介 toohello Azure Service Fabric 健康監視提供監視 hello 叢集與應用程式及服務的模型。"
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 1d979210-b1eb-4022-be24-799fd9d8e003
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: oanapl
ms.openlocfilehash: 904f36374ca6ca7e4caa1d43c92584e7e4c50087
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooservice-fabric-health-monitoring"></a>簡介 tooService 網狀架構健全狀況監視
Azure Service Fabric 導入了健康狀態模型，提供豐富、彈性且可延伸的健康狀態評估與報告。 hello 模型允許接近即時監視 hello hello 叢集和執行中的 hello 服務的狀態。 您可以輕鬆地取得健康狀態資訊，並在潛在問題引起連鎖反應和造成大規模中斷之前，予以更正。 在 hello 一般模型中，服務會傳送其本機檢視中，為基礎的報表，資訊都會彙總以及 tooprovide 整體叢集層級檢視。

Service Fabric 元件會使用這個豐富的健全狀況模型 tooreport 及其目前狀態。 您可以使用 hello 從您的應用程式的相同機制 tooreport 健全狀況。 只要投入時間規劃高品質的健康狀態報告來擷取您的自訂條件，就能更輕鬆地偵測並修正執行中應用程式的問題。

下列 Microsoft Virtual Academy 視訊也會描述 hello 服務網狀架構健全狀況模型，以及如何使用 hello:<center><a target="_blank" href="https://mva.microsoft.com/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tevZw56yC_1906218965">
<img src="./media/service-fabric-health-introduction/HealthIntroVid.png" WIDTH="360" HEIGHT="244">
</a></center>

> [!NOTE]
> 我們已開始 hello 健全狀況子系統 tooaddress 受監視的升級需求。 Service Fabric 提供受監視應用程式和叢集的升級，可確保完整的可用性、 沒有停機時間及 toono 最少使用者介入。 這些目標，hello 升級檢查健全狀況根據的 tooachieve 設定升級的原則。 只有在健康情況達到所需的臨界值時，才可繼續進行升級。 否則，hello 升級可能會自動回復或暫停 toogive 系統管理員有機會 toofix hello 問題。 toolearn 深入了解應用程式升級，請參閱[本文](service-fabric-application-upgrade.md)。
> 
> 

## <a name="health-store"></a>健康狀態資料存放區
hello 健全狀況存放區會保留實體健全狀況相關資訊，以方便擷取和評估 hello 叢集中。 它被實作 Service Fabric 保存具狀態服務 tooensure 高可用性和延展性。 hello 健全狀況存放區屬於 hello **fabric: / System**應用程式，而且這是可用時 hello 叢集已啟動且正在執行。

## <a name="health-entities-and-hierarchy"></a>健康狀態實體和階層
hello 健康實體被按照邏輯階層架構中擷取的互動和不同實體之間的相依性。 健康實體和階層，根據從 Service Fabric 元件所收到的報表，自動建置 hello 健全狀況存放區。

hello 健康實體鏡像 hello Service Fabric 實體。 (比方說，**健全狀況應用程式的實體**符合應用程式執行個體 hello 叢集中部署，而**健全狀況節點實體**符合 Service Fabric 叢集節點。) 擷取 hello 健全狀況階層hello 與之間的互動 hello 系統實體，它是進階的健全狀況評估 hello 基礎。 您可以在 [Service Fabric 技術概觀](service-fabric-technical-overview.md)中了解重要的 Service Fabric 概念。 如需應用程式的詳細資訊，請參閱 [Service Fabric 應用程式模型](service-fabric-application-model.md)。

hello 健康實體和階層可讓 hello 叢集和應用程式 toobe 有效報告、 偵錯和監視。 hello 健全狀況模型會提供正確的*細微*hello 健全狀況的表示法 hello hello 叢集中的許多移動片段。

![健康狀態實體][1]。
hello 健全狀況的實體，組織中的父子式關聯性為基礎的階層。

[1]: ./media/service-fabric-health-introduction/servicefabric-health-hierarchy.png

hello 健康實體包括：

* **叢集**。 代表 hello Service Fabric 叢集健全狀況。 叢集健全狀況報表描述影響 hello 整個叢集的條件。 這些條件會影響 hello 叢集或本身 hello 叢集中的多個實體。 根據 hello 條件，hello 報告無法縮小 hello 問題向下 tooone 或多個狀況不良的子系。 範例包括 hello 叢集分割到期 toonetwork 分割或通訊問題的 hello 大腦。
* **節點**。 代表 hello Service Fabric 節點健全狀況。 節點健全狀況報告說明影響 hello 節點 」 功能的條件。 它們通常會影響在其上執行的所有部署的 hello 實體。 範例包括節點的磁碟空間不足 (或其他電腦全域屬性，例如記憶體、連線) 以及節點已關閉時。 hello 節點實體識別 hello 節點名稱 （字串）。
* **應用程式**。 代表 hello hello 叢集中執行的應用程式執行個體健全狀況。 應用程式健康情況報告的描述會影響 hello 的條件 hello 應用程式的整體健全狀況。 它們無法縮小 tooindividual 子系 （服務或部署的應用程式）。 範例包括 hello 應用程式中的 hello 在不同的服務之間的端對端互動。 hello 應用程式名稱 (URI) 來識別 hello 應用程式的實體。
* **服務**。 代表 hello hello 叢集中執行之服務的健全狀況。 服務健全狀況報告描述影響 hello 的條件 hello 服務的整體健全狀況。 hello 報告無法縮小 hello 問題 tooan 狀況不良資料分割或複本。 範例包括造成所有分割區發生問題的服務組態 (例如，連接埠或外部檔案共用)。 hello 服務實體識別 hello 服務名稱 (URI)。
* **資料分割**。 代表 hello 健全狀況服務資料分割。 資料分割健全狀況報表描述影響 hello 整個複本集的條件。 範例包括 hello 複本數目低於目標計數時，以及資料分割是在仲裁遺失。 hello 磁碟分割實體識別 hello 資料分割識別碼 (GUID)。
* **複本**。 代表 hello 健全狀況狀態的服務複本或無狀態服務執行個體。 hello 複本是 hello watchdogs 與系統元件可報告的應用程式的最小單位。 可設定狀態的服務的範例包括作業 toosecondaries 和速度緩慢的複寫無法複寫的主要複本。 此外，若無狀態的執行個體在執行時資源不足或發生連線問題，則其會進行報告。 hello 複本實體識別 hello 分割區識別碼 (GUID) 和 hello 複本或執行個體識別碼 （長整數）。
* **已部署應用程式**。 代表 hello 的健全狀況*節點上執行的應用程式*。 部署的應用程式健康情況報告描述條件特定 toohello 應用程式上無法縮小 tooservice 套件 hello 上部署的 hello 節點相同的節點。 範例包括錯誤時無法在該節點上下載應用程式套件和應用程式的安全性主體 hello 節點上所設定的問題。 部署的 hello 應用程式識別應用程式名稱 (URI) 和節點名稱 （字串）。
* **已部署服務封裝**。 代表 hello hello 叢集中的節點上執行的服務封裝健全狀況。 它描述條件特定 tooa 服務封裝不會影響 hello 其他服務封裝上 hello hello 的相同節點相同的應用程式。 範例包括 hello 無法啟動的服務封裝和組態的封裝無法讀取程式碼封裝。 識別部署的 hello 服務封裝應用程式名稱 (URI)、 節點名稱 （字串）、 服務資訊清單的名稱 （字串） 和服務套件啟用識別碼 （字串）。

hello 資料粒度的 hello 健全狀況模型可讓您輕鬆 toodetect 和修正問題。 例如，如果服務沒有回應，它是可行 hello 應用程式執行個體的 tooreport 會處於狀況不良。 報告在層級不理想的做法，不過，因為 hello 問題可能不會影響所有 hello 服務該應用程式中。 hello 報表應該在套用的 toohello 狀況不良的服務或 tooa 特定的子資料分割，如果更多資訊點 toothat 磁碟分割。 hello 自動透過 hello 階層的介面和狀況不良的資料分割也會看到資料服務和應用程式層級。 此彙總有助於 toopinpoint，並更快速地解決 hello hello 問題根本原因。

hello 健全狀況階層是父子式關聯性所組成。 叢集是由節點和應用程式所組成。 應用程式包含服務和已部署的應用程式。 已部署的應用程式包含已部署的服務封裝。 服務包含資料分割，且每個資料分割包含一個或多個複本。 節點和已部署實體之間具有特殊關聯性。 狀況不良的節點回報其授權單位系統元件 hello Failover Manager service 會影響部署的 hello 應用程式、 服務套件，以及在其上部署的複本。

hello 健全狀況階層代表 hello hello 系統根據了 hello 最新的健康情況報告，幾乎即時的資訊最新狀態。
內部和外部 watchdogs 可以報告在 hello 相同的實體會根據特定應用程式邏輯或自訂受監視的狀況。 使用者報告共存 hello 系統報告。

規劃 tooinvest tooreport 和回應期間 hello toohealth 如何設計大型的雲端服務中。 此預付 investement 讓 hello 服務更容易 toodebug，監控和操作。

## <a name="health-states"></a>健康狀態
Service Fabric 實體是否狀況良好，或不會使用三種健全狀況狀態 toodescribe: [確定]，警告和錯誤。 所傳送的任何報告 toohello 健全狀況存放區都必須指定其中一種狀態。 hello 健全狀況評估結果為其中一種狀態。

hello 可能[健全狀況狀態](https://docs.microsoft.com/dotnet/api/system.fabric.health.healthstate)是：

* **OK**。 hello 實體是狀況良好。 報告實體本身或其子系 (適用時) 沒有已知問題。
* **Warning**。 hello 實體有一些問題，但它仍然可以正常運作。 例如，發生延遲，但尚未造成任何功能上的問題。 在某些情況下，hello 警告狀況可能可以解決本身不需要外部介入。 在這些情況下，健康情況報告會引起關注，並提供後續狀況的可見性。 在其他情況下，可能會降低不需要使用者介入的嚴重問題的 hello 警告狀況。
* **Error**。 hello 實體會處於狀況不良。 應採取動作 toofix hello 狀態 hello 實體，因為無法正確運作。
* **Unknown**。 hello 實體不存在 hello health store 中。 此結果可取得 hello 分散式查詢，使多個元件的結果合併。 比方說，hello 取得節點清單的查詢會太**FailoverManager**， **ClusterManager**，和**HealthManager**; 取得應用程式清單查詢會太**ClusterManager**和**HealthManager**。 這些查詢會合併來自多個系統元件的結果。 如果另一個系統元件傳回 health store 中所沒有的實體，hello 合併的結果具有未知健全狀況狀態。 實體不在存放區因為健康情況報告尚未處理或 hello 實體已被清除之後刪除。

## <a name="health-policies"></a>健康狀態原則
hello 健全狀況的儲存區適用於健全狀況原則 toodetermine，實體是否狀況良好的報表和子系為基礎。

> [!NOTE]
> Hello （適用於叢集和節點的健全狀況評估） 的叢集資訊清單中，或在 hello （適用於應用程式評估和任何子系） 的應用程式資訊清單中，可以指定健康情況原則。 健康情況評估要求也可傳入僅用於該評估的自訂健康情況評估原則。
> 
> 

根據預設，Service Fabric 適用於嚴格的規則 （所有項目必須是狀況良好） hello 父子式階層式關聯性。 如果即使其中一個 hello 系有一個狀況不良事件，hello 父系會被視為狀況不良。

### <a name="cluster-health-policy"></a>叢集健康狀態原則
hello[叢集健全狀況原則](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy)是使用的 tooevaluate hello 叢集健全狀況狀態和節點的健全狀況狀態。 hello 原則可以定義在 hello 叢集資訊清單。 如果不存在，則會使用 hello 預設原則 （零容許失敗）。
hello 叢集健全狀況原則包含：

* [ConsiderWarningAsError](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.considerwarningaserror)。 指定健康情況評估期間是否 tootreat 警告健康情況報告為錯誤。 預設：false。
* [MaxPercentUnhealthyApplications](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.maxpercentunhealthyapplications)。 指定 hello 的最大容許的百分比之前，會處於狀況不良 hello 叢集會被視為錯誤的應用程式。
* [MaxPercentUnhealthyNodes](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.maxpercentunhealthynodes)。 指定 hello 最大容許的百分比之前 hello 叢集會被視為錯誤則可以為狀況不良的節點。 在大型叢集，有些節點永遠都是向下或出修復，所以此百分比應該是設定的 tootolerate 的。
* [ApplicationTypeHealthPolicyMap](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.applicationtypehealthpolicymap)。 hello 應用程式類型的健全狀況原則對應可以用於叢集健全狀況評估 toodescribe 特殊應用程式類型。 根據預設，所有的應用程式都會放入集區，並使用 MaxPercentUnhealthyApplications 加以評估。 如果某些應用程式類型應該以不同的方式來處理，他們可以超出 hello 全域集區。 相反地，它們可以對其 hello 對應中的應用程式類型名稱與相關聯的 hello 百分比。 例如，在叢集中，有數千個不同類型的應用程式，以及某個特殊應用程式類型的數個控制應用程式執行個體。 hello 控制應用程式應該不會發生錯誤。 您可以指定全域 MaxPercentUnhealthyApplications too20 %tootolerate 某些失敗，但應用程式類型 」 ControlApplicationType"hello 設定 hello MaxPercentUnhealthyApplications too0。 如此一來，如果某些 hello 許多應用程式的狀況不良，但是低於 hello 全域的狀況不良百分比，就會產生 hello 叢集評估 tooWarning。 Warning 健康狀態並不會影響叢集升級或由 Error 健康狀態觸發的其他監視。 不過，即使一個控制應用程式中錯誤會使叢集狀況不良，觸發程序回復或暫停 hello 叢集升級時，視 hello 升級組態而定。
  Hello hello 對應中所定義的應用程式類型，所有的應用程式執行個體帶離 hello 全域集區的應用程式。 它們可以根據 hello 總數 hello 應用程式類型的應用程式，使用 hello hello 從特定 MaxPercentUnhealthyApplications 對應。 所有的 hello 其餘的 hello 應用程式仍會 hello 全域集區，並利用 MaxPercentUnhealthyApplications 來評估。

下列範例中的 hello 是摘錄自叢集資訊清單。 toodefine hello 應用程式中的項目型別對應，以 「 ApplicationTypeMaxPercentUnhealthyApplications-」，後面接著 hello 應用程式類型名稱的前置詞 hello 參數名稱。

```xml
<FabricSettings>
  <Section Name="HealthManager/ClusterHealthPolicy">
    <Parameter Name="ConsiderWarningAsError" Value="False" />
    <Parameter Name="MaxPercentUnhealthyApplications" Value="20" />
    <Parameter Name="MaxPercentUnhealthyNodes" Value="20" />
    <Parameter Name="ApplicationTypeMaxPercentUnhealthyApplications-ControlApplicationType" Value="0" />
  </Section>
</FabricSettings>
```

### <a name="application-health-policy"></a>應用程式健康狀態原則
hello[應用程式健全狀況原則](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy)描述的事件和子狀態的彙總的 hello 評估應用程式和其子系的進行方式。 它可以在 hello 應用程式資訊清單中定義**ApplicationManifest.xml**，hello 應用程式封裝中。 如果未不指定任何原則，Service Fabric 假設 hello 實體會處於狀況不良，如果它在 hello 警告或錯誤健全狀況狀態會有健全狀況報表或子系。
hello 可設定的原則包括：

* [ConsiderWarningAsError](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.considerwarningaserror.aspx)。 指定健康情況評估期間是否 tootreat 警告健康情況報告為錯誤。 預設：false。
* [MaxPercentUnhealthyDeployedApplications](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.maxpercentunhealthydeployedapplications)。 指定已部署的應用程式可能會處於狀況不良之前 hello 應用程式會被視為錯誤的 hello 所容許之最大百分比。 此百分比會計算除以 hello 數目狀況不良的已部署應用程式透過 hello hello 應用程式目前部署於 hello 叢集中的節點數目。 hello 計算進位 tootolerate 小的數字的節點上一次失敗。 預設百分比：零。
* [DefaultServiceTypeHealthPolicy](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.defaultservicetypehealthpolicy)。 指定 hello 預設服務類型健全狀況原則，可取代 hello hello 應用程式中的所有服務類型的預設健全狀況原則。
* [ServiceTypeHealthPolicyMap](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.servicetypehealthpolicymap)。 針對每個服務類型提供服務健康狀態原則的對應。 這些原則會取代 hello 預設服務類型健康原則的每個指定的服務類型。 例如，如果某個應用程式的無狀態的閘道服務型別和可設定狀態的引擎服務類型，您可以以不同的方式設定其評估 hello 健康情況原則。 當您指定每個服務類型的原則時，您可以更細微的控制權 hello hello 服務健全狀況。

### <a name="service-type-health-policy"></a>服務類型健康狀態原則
hello[服務類型的健全狀況原則](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy)指定如何 tooevaluate 和彙總 hello 服務以及 hello 服務的子系。 hello 原則包含：

* [MaxPercentUnhealthyPartitionsPerService](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy.maxpercentunhealthypartitionsperservice)。 服務視為狀況不良之前，請指定狀況不良的資料分割的 hello 所容許之最大的百分比。 預設百分比：零。
* [MaxPercentUnhealthyReplicasPerPartition](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy.maxpercentunhealthyreplicasperpartition)。 分割區視為狀況不良之前，請指定 hello 最大容許之百分比的狀況不良的複本。 預設百分比：零。
* [MaxPercentUnhealthyServices](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy.maxpercentunhealthyservices)。 Hello 應用程式視為狀況不良之前，請指定 hello 所容許之最大狀況不良服務百分比。 預設百分比：零。

下列範例中的 hello 是摘錄自應用程式資訊清單：

```xml
    <Policies>
        <HealthPolicy ConsiderWarningAsError="true" MaxPercentUnhealthyDeployedApplications="20">
            <DefaultServiceTypeHealthPolicy
                   MaxPercentUnhealthyServices="0"
                   MaxPercentUnhealthyPartitionsPerService="10"
                   MaxPercentUnhealthyReplicasPerPartition="0"/>
            <ServiceTypeHealthPolicy ServiceTypeName="FrontEndServiceType"
                   MaxPercentUnhealthyServices="0"
                   MaxPercentUnhealthyPartitionsPerService="20"
                   MaxPercentUnhealthyReplicasPerPartition="0"/>
            <ServiceTypeHealthPolicy ServiceTypeName="BackEndServiceType"
                   MaxPercentUnhealthyServices="20"
                   MaxPercentUnhealthyPartitionsPerService="0"
                   MaxPercentUnhealthyReplicasPerPartition="0">
            </ServiceTypeHealthPolicy>
        </HealthPolicy>
    </Policies>
```

## <a name="health-evaluation"></a>健康狀態評估
使用者和自動化服務可以隨時評估任何實體的健康狀態。 tooevaluate 實體健全狀況、 hello 健全狀況存放區的彙總所有健全狀況報告 hello 實體上，並評估所有子系 （如果適用的話）。 hello 健全狀況彙總演算法會使用健全狀況原則，以指定 tooevaluate 健全狀況的報告方式及如何 tooaggregate 子健全狀況狀態 （如果適用的話）。

### <a name="health-report-aggregation"></a>健康狀態報告彙總
一個實體可以具有由不同回報者針對不同屬性 (系統元件或看門狗) 所傳送的多個健康狀態報告。 hello 彙總使用 hello 關聯的健全狀況原則、 特別 hello ConsiderWarningAsError 成員的應用程式，或叢集健全狀況原則。 指定的 ConsiderWarningAsError 如何 tooevaluate 警告。

hello 彙總健全狀況狀態由觸發 hello*最差*hello 實體上的健康情況報告。 如果沒有至少一個錯誤健康情況報告，hello 彙總健全狀況狀態會發生錯誤。

![健康狀態報告彙總，包含「Error」報告。][2]

有一或多個錯誤健康狀態報告的健康狀態實體會評估為「錯誤」。 hello 也適用於已過期的健康情況報告，不論其健全狀況狀態。

[2]: ./media/service-fabric-health-introduction/servicefabric-health-report-eval-error.png

如果有任何錯誤報告和一或多個警告，hello 彙總健全狀況狀態是警告或錯誤時，根據 hello ConsiderWarningAsError 原則旗標。

![健康狀態報告彙總，包含「Warning」報告和已設為 false 的 ConsiderWarningAsError。][3]

健全狀況報表的彙總警告報表與 ConsiderWarningAsError 設定 toofalse （預設值）。

[3]: ./media/service-fabric-health-introduction/servicefabric-health-report-eval-warning.png

### <a name="child-health-aggregation"></a>子系健康狀態彙總
hello 實體的彙總健全狀況狀態反映 hello 子健全狀況狀態 （如果適用的話）。 彙總子健全狀況狀態的 hello 演算法使用 hello 健全狀況所適用的原則根據 hello 實體類型。

![子系實體健康狀態彙總。][4]

以健康狀態原則為基礎的子系彙總。

[4]: ./media/service-fabric-health-introduction/servicefabric-health-hierarchy-eval.png

Hello 健全狀況存放區評估 hello 的所有子系之後，它將彙總其健全狀況狀態，根據設定的 hello 的狀況不良的子系的最大百分比。 此百分比是取自 hello 原則根據 hello 實體和子類型。

* 如果所有子系的 [確定] 狀態，hello 子彙總健全狀況狀態是 [確定]。
* 如果子系 [確定] 和警告狀態，hello 子彙總健全狀況狀態為警告。
* 如果沒有子系不會採用 hello 允許的狀況不良的子系百分比的最大值的錯誤狀態，hello 彙總健全狀況狀態會發生錯誤。
* 如果以錯誤狀態尊重 hello 最大的 hello 子系所允許的狀況不良的子系的百分比 hello 彙總健全狀況狀態為警告。

## <a name="health-reporting"></a>健康狀態報告
系統元件、System Fabric 應用程式和內部/外部看門狗可以報告 Service Fabric 實體。 hello reporters 進行*本機*hello 根據 hello 條件所監視的受監視的 hello 實體健全狀況的決定。 它們不需要 toolook 任何全域狀態或彙總資料。 hello 所需的行為是 toohave 簡單正常值，並不複雜的生態需要在許多事情 tooinfer toolook 何種資訊 toosend。

toosend 健全狀況資料 toohello 健全狀況存放區，報告需要 tooidentify hello 影響實體並建立健康情況報告。 toosend hello 報表，請使用 hello [FabricClient.HealthClient.ReportHealth](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.reporthealth) API，應用程式開發介面公開在 hello 回報健全狀況`Partition`或`CodePackageActivationContext`物件、 PowerShell cmdlet 或 REST。

### <a name="health-reports"></a>健康狀態報告
hello[健康情況報告](https://docs.microsoft.com/dotnet/api/system.fabric.health.healthreport)hello 實體 hello 叢集中的每個包含 hello 下列資訊：

* **SourceId**。 可唯一識別 hello reporter hello 健全狀況事件的字串。
* **實體識別碼**。 識別 hello 實體套用 hello 報表的位置。 異 hello[實體類型](service-fabric-health-introduction.md#health-entities-and-hierarchy):
  
  * 叢集。 無。
  * 節點。 節點名稱 (字串)。
  * 應用程式。 應用程式名稱 (URI)。 代表 hello hello 叢集中部署的 hello 應用程式執行個體名稱。
  * 服務。 服務名稱 (URI)。 代表 hello hello 叢集中部署的 hello 服務執行個體名稱。
  * 分割區。 分割識別碼 (GUID)。 代表 hello 資料分割的唯一識別碼。
  * 複本。 hello 可設定狀態的服務複本識別碼或 hello 無狀態服務執行個體識別碼 (INT64)。
  * DeployedApplication。 應用程式名稱 (URI) 和節點名稱 (字串)。
  * DeployedServicePackage。 應用程式名稱 (URI)、節點名稱 (字串) 和服務資訊清單名稱 (字串)。
* **Property**。 A*字串*（不固定的列舉），可讓 hello reporter toocategorize hello 健全狀況事件的 hello 實體特定屬性。 例如，報告程式的可報告的 hello Node01"Storage"屬性的 hello 健全狀況，而且 reporter B 報告 hello Node01"連接性 」 屬性的 hello 健全狀況。 Hello 健全狀況存放區中，這些報表會被視為個別的健全狀況事件 hello Node01 實體。
* **Description**。 字串，可讓報告 tooprovide 詳細 hello 健全狀況事件的相關資訊。 **SourceId**，**屬性**，和**HealthState**應該完整描述 hello 報表。 hello 描述新增 hello 報表人類看得懂的資訊。 hello 文字，方便系統管理員和使用者 toounderstand hello 健康情況報告。
* **HealthState**。 [列舉](service-fabric-health-introduction.md#health-states)描述 hello 報表 hello 健全狀況狀態。 hello 接受的值為 [確定]、 警告和錯誤。
* **TimeToLive**。 表示多久 hello 健全狀況報表時間範圍無效。 搭配**RemoveWhenExpired**，它可讓知道如何 tooevaluate 過期事件 hello 健全狀況存放區。 根據預設，hello 值是無限的而且 hello 報表是永遠有效。
* **RemoveWhenExpired**。 布林值。 如果設定 tootrue，hello 過期的健全狀況報表會自動移除 hello 健全狀況存放區，並 hello 報表不會影響實體健全狀況評估。 Hello 報表有效期為一段指定時間，與 hello 報告時，使用不需要 tooexplicitly 清除它。它也使用從 hello health store toodelete 報表 （例如，可變更和停止傳送與先前的來源和屬性的報表監視）。 可傳送簡短 TimeToLive RemoveWhenExpired tooclear 以及具有報表從 hello health store 任何先前的狀態。 如果設定 hello 值 toofalse，hello 過期的報表會被視為 hello 健全狀況評估錯誤。 hello false 值表示 toohello 健全狀況存放區，該 hello 來源應該定期報告，這個屬性上。 如果沒有，則有必須 hello 監視問題。 考慮為錯誤的 hello 事件擷取 hello 監視健全狀況。
* **SequenceNumber**。 正整數，這個值需要 toobe 不斷增加，它代表 hello 報表 hello 順序。 它會使用 hello 健康狀態存放區 toodetect 過時報表晚期會收到是因為網路延遲或其他問題。 報表會拒絕 hello 序號是否小於或等於 toohello 最近套用號碼 hello 相同的實體、 來源和屬性。 如果未指定，會自動產生 hello 序號。 報告的狀態轉換時，才是必要 tooput hello 的序號。 在此情況下，hello 來源必須的 tooremember 哪些報表它傳送，並記下進行復原的 hello 資訊在容錯移轉。

每個健康狀態報告都需要四種資訊 (SourceId、實體識別碼、Property 和 HealthState)。 hello SourceId 字串不允許 toostart hello 前置詞"**系統**"，這保留供系統報告。 Hello 相同的實體沒有 hello 只能有一個報表相同的來源和屬性。 多個報表 hello 相同的來源和屬性覆寫彼此 hello 的健全狀況用戶端 （如果不批次處理） 或 hello 健全狀況存放區端。 hello 取代為基礎的序號。（具有更高的序號） 較新的報表會取代較舊的報表。

### <a name="health-events"></a>健康狀態事件
就內部而言，hello 健全狀況存放區會保留[健全狀況事件](https://docs.microsoft.com/dotnet/api/system.fabric.health.healthevent)，其中包含所有 hello 資訊 hello 報表和其他中繼資料。 hello 中繼資料包括 hello 報表有 toohello 健全狀況的用戶端 hello 時間和 hello 伺服器端修改它的 hello 時間。 hello 健全狀況事件都會傳回到由[健康狀態查詢](service-fabric-view-entities-aggregated-health.md#health-queries)。

hello 加入中繼資料包含：

* **SourceUtcTimestamp**。 hello hello 報表有 toohello 健全狀況用戶端 （國際標準時間）。
* **LastModifiedUtcTimestamp**。 hello hello 報表上次修改 hello 伺服器端 （國際標準時間）。
* **IsExpired**。 旗標 tooindicate 是否 hello 報表已過期時 hello 查詢由 hello 健全狀況存放區中執行。 只有當 RemoveWhenExpired 為 False，事件才會過期。 否則，hello 事件不會由查詢傳回，並移除從 hello 存放區。
* **LastOkTransitionAt**、**LastWarningTransitionAt**、**LastErrorTransitionAt**。 hello 最後一次 [確定] / 警告/錯誤轉換的時間。 這些欄位會提供 hello hello 健全狀況狀態轉換為 hello 事件的歷程記錄。

hello 狀態轉換欄位可用於更聰明的警示或 「 歷程記錄 」 的健全狀況事件的資訊。 所適用的案例如下：

* 當屬性處於「Warning/Error」狀態持續超過 X 分鐘時發出警示。 檢查一段時間的 hello 條件，可避免暫時狀況的警示。 例如，如果會在發出警告超過五分鐘 hello 健康狀態警示可以轉譯成 (HealthState = 警告和現在-LastWarningTransitionTime = > 5 分鐘)。
* 警示只在上次 X 分鐘 hello 中已經變更的條件。 如果報表已在錯誤發生時 hello 指定時間之前，它可以被忽略，因為它信號便已存在之前。
* 若屬性交叉出現警告和錯誤，請判斷狀況不良 (亦即不是 OK) 已持續多久。 比方說，如果 hello 屬性尚未不良的狀態已超過五分鐘警示可以轉譯成 (HealthState ！ = [確定] 並立即-LastOkTransitionTime > 5 分鐘)。

## <a name="example-report-and-evaluate-application-health"></a>範例：報告和評估應用程式健康狀態
hello 下列範例會傳送 hello 應用程式透過 PowerShell 健康情況報告**fabric: / WordCount** hello 來源**MyWatchdog**。 hello 健康情況報告包含 hello 健全狀況屬性中的錯誤健全狀況狀態，具有無限 TimeToLive 的 「 可用性 」 的相關資訊。 然後它會查詢 hello 應用程式健全狀況，並傳回彙總健全狀況狀態錯誤和 hello 回報的健全狀況事件的 hello 清單中的健全狀況事件。

```powershell
PS C:\> Send-ServiceFabricApplicationHealthReport –ApplicationName fabric:/WordCount –SourceId "MyWatchdog" –HealthProperty "Availability" –HealthState Error

PS C:\> Get-ServiceFabricApplicationHealth fabric:/WordCount -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            :
                                  Error event: SourceId='MyWatchdog', Property='Availability'.

ServiceHealthStates             :
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Error

                                  ServiceName           : fabric:/WordCount/WordCountWebService
                                  AggregatedHealthState : Ok

DeployedApplicationHealthStates :
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_0
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_2
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_3
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_4
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_1
                                  AggregatedHealthState : Ok

HealthEvents                    :
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 360
                                  SentAt                : 3/22/2016 7:56:53 PM
                                  ReceivedAt            : 3/22/2016 7:56:53 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 3/22/2016 7:56:53 PM, LastWarning = 1/1/0001 12:00:00 AM

                                  SourceId              : MyWatchdog
                                  Property              : Availability
                                  HealthState           : Error
                                  SequenceNumber        : 131032204762818013
                                  SentAt                : 3/23/2016 3:27:56 PM
                                  ReceivedAt            : 3/23/2016 3:27:56 PM
                                  TTL                   : Infinite
                                  Description           :
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Ok->Error = 3/23/2016 3:27:56 PM, LastWarning = 1/1/0001 12:00:00 AM
```

## <a name="health-model-usage"></a>健康狀態模型使用方式
hello 健全狀況模型可讓雲端服務和基礎 Service Fabric 平台 tooscale hello，因為監視與健全狀況判斷分散 hello hello 叢集內不同的監視器。
其他系統在剖析所有 hello hello 叢集層級有單一且集中式服務*潛在*服務所發出的有用資訊。 這個方法會防礙其延展性。 它也不允許它們 toocollect toohelp 識別為盡可能關閉 toohello 根本原因的問題以及潛在問題的特定資訊。

監視與診斷、 評估叢集和應用程式的健全狀況，以及受監視的升級，是大量使用 hello 健全狀況模型。 其他服務使用健全狀況資料 tooperform 自動修復，建置叢集健全狀況歷程記錄，並發出警示，在某些狀況。

## <a name="next-steps"></a>後續步驟
[檢視 Service Fabric 健康狀態報告](service-fabric-view-entities-aggregated-health.md)

[使用系統健康狀態報告進行疑難排解](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[Tooreport 並檢查服務健全狀況](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[新增自訂 Service Fabric 健康狀態報告](service-fabric-report-health.md)

[在本機上監視及診斷服務](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Service Fabric 應用程式升級](service-fabric-application-upgrade.md)

