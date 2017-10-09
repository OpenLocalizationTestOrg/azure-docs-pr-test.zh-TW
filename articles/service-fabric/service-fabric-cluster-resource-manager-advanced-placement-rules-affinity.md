---
title: "aaaService 網狀架構叢集資源管理員的親和性 |Microsoft 文件"
description: "Service Fabric 服務的設定同質性概觀"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 678073e1-d08d-46c4-a811-826e70aba6c4
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 7dc9b6d9c18d9d615d39cff7de9d7cba1c040474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-and-using-service-affinity-in-service-fabric"></a>在 Service Fabric 中設定並使用服務同質性
親和性會提供主要 toohelp 輕鬆 hello 轉換成 hello 雲端和 microservices 世界大型整合應用程式的控制項。 它也會當做使用最佳化來改善 hello 效能的服務，雖然這樣做可能有副作用。

例如，假設您要讓較大的應用程式，或只未設計 microservices 注意、 tooService 網狀架構 （或任何分散式的環境） 中的其中一個。 這種轉換很常見。 您啟動提升到 hello 環境的 hello 整個應用程式、 封裝，並確定它可以順利執行。 然後啟動其分解成較小不同，所有交談 tooeach 其他的服務。

最後您可能會發現 hello 應用程式發生一些問題。 hello 問題通常可分成下列其中一種：

1. Hello 整合應用程式中的某些元件 X Y 元件上有未記載的相依性和您剛開啟這些元件到個別的服務。 因為這些服務現在 hello 叢集中不同節點上執行，變更就會中斷。
2. 透過這些元件進行通訊 (本機具名管道 | 共用記憶體 | 磁碟上的檔案) 和它們真正需要 toobe 無法 toowrite tooa 共用本機資源的效能立即。 您稍後或許會移除該硬式相依性。
3. 一切都沒問題，但事實上，這兩個元件具有很多對話/效能敏感的內容。 當我將它們移到個別服務時，整體應用程式效能會遭到重挫或導致延遲增加。 如此一來，hello 整體應用程式不符合預期。

在這些情況下，我們不要 toolose 重構的工作中，而且不想 toogo 後 toohello monolith。 hello 最後一個條件，甚至可能想要為純文字的最佳化。 不過，我們可以重新 hello 元件 toowork 設計為服務的自然 （或之前我們可以解決 hello 效能期望其他方式） 我們 tooneed 某種意義上的位置。

哪些 toodo？ 嗯，您可以嘗試開啟同質性。

## <a name="how-tooconfigure-affinity"></a>如何 tooconfigure 親和性
tooset 向上親和性，您會定義兩個不同的服務之間的親和性關聯性。 您可以將此同質性想像成在一個服務上「指向」另一個服務，並假設「此服務只有在該服務執行所在的地方才能執行」。 有時候我們 tooaffinity 父子式關聯性 （其中您指向 hello 子 hello 父）。 確定 hello 複本或一個服務的執行個體位於上 hello 相同親和性可確保與其他服務的節點。

```csharp
ServiceCorrelationDescription affinityDescription = new ServiceCorrelationDescription();
affinityDescription.Scheme = ServiceCorrelationScheme.Affinity;
affinityDescription.ServiceName = new Uri("fabric:/otherApplication/parentService");
serviceDescription.Correlations.Add(affinityDescription);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

> [!NOTE]
> 子服務只能參與一個同質關聯性。 如果您想 hello 子 toobe 相似化 tootwo 父服務一次您會有幾個選項：
> - 反向 hello 關聯性 （具有 parentService1 和 parentService2 指向 hello 目前子服務），或
> - 指定其中一種 hello 父系的集線器，依照慣例，而且有指向該服務的所有服務。 
>
> hello 產生 hello 叢集中的放置方式應該 hello 相同。
>

## <a name="different-affinity-options"></a>各種同質性選項
同質性是透過數種相互關聯的結構描述之一來表示，而且有兩種不同的模式。 hello 親和性的最常見的模式是我們呼叫 NonAlignedAffinity。 在 NonAlignedAffinity，hello 複本或 hello 不同服務的執行個體上放置 hello 相同節點。 hello 其他模式為 AlignedAffinity。 對齊的同質性只有在與具狀態服務搭配使用時才有用。 設定兩個可設定狀態服務 toohave 對齊親和性可確保這些服務的 hello 混雜會置於 hello 相同節點每個其他。 它也會讓次要資料庫的每一對這些服務 toobe 置於 hello 相同的節點。 此外，也可以 （但較不常見，） tooconfigure NonAlignedAffinity 可設定狀態的服務。 NonAlignedAffinity，hello 不同複本的兩個可設定狀態的服務會在執行的 hello hello 相同節點，但其主要複本會最後可能會在不同節點上。

<center>
![同質性模式及其效果][Image1]
</center>

### <a name="best-effort-desired-state"></a>盡力而為的期望狀態
同質關聯性是盡力而為模式。 它不提供 hello 共置或可靠性的 hello 中執行相同的可執行程序會執行相同的保證。 親和性關聯性中的 hello 服務都可能會失敗，而且獨立移動的本質上不同實體。 同質關聯性也可能會中斷，不過這些中斷只是暫時的。 例如，容量限制可能表示只有部分 hello hello 親和性關聯性中的服務物件可容納指定節點上。 在這些情況下即使有親和性關聯性的位置，則無法強制執行到期 toohello 其他條件約束。 如果可能 toodo 因此，會自動稍後更正 hello 違規。

### <a name="chains-vs-stars"></a>鏈結與星形的比較
現今 hello 叢集資源管理員不能 toomodel 親和性關聯性的鏈結。 這表示是，如果有一個服務是某一個同質關聯性中的子系，則該服務不能是另一個同質關聯性中的父系。 如果您想 toomodel 這種類型的關聯性，您可以實際獲得 toomodel 它為星號，而不是鏈結。 toomove 從鏈結 tooa 星形，hello 最底層子會是父代的 toohello 第一個子系的父系。 根據您的服務的 hello 排列方式，您可能 toodo 多次。 如果沒有自然父系服務，您可能 toocreate 一個用來作為預留位置。 根據您的需求，您可能也想成 toolook[應用程式群組](service-fabric-cluster-resource-manager-application-groups.md)。

<center>
![同質關聯性內容中的鏈結與Hello 內容的親和性關聯性中顆星][Image2]
</center>

有關親和性關聯性的另一件事 toonote 現今是具有方向性。 這表示該 hello 親和性規則只會強制 hello 子放置 hello 父代。 它無法確保該 hello 父系位於使用 hello 子系。 它也很重要 hello 親和性關聯性的 toonote 無法最佳或立即強制因為不同的服務可以有不同的生命週期，和可以失敗，並且單獨移動。 例如，假設 hello 父突然失敗 tooanother 節點上發生當機。 hello 叢集資源管理員和容錯移轉管理員控制代碼 hello 容錯移轉，因為保持 hello 服務、 一致且可用 hello 優先順序。 Hello 容錯移轉完成之後，請 hello 親和性關聯中斷，但 hello 叢集資源管理員認為服務的所有項目是正常的直到它通知 hello 子不是位於 hello 父代。 系統會定期執行這類檢查。 上如何 hello 叢集資源管理員會評估條件約束的詳細資訊可用於[本文](service-fabric-cluster-resource-manager-management-integration.md#constraint-types)，和[這一個](service-fabric-cluster-resource-manager-balancing.md)深入 tooconfigure hello 的韻律這些條件約束會在其的方式評估。   


### <a name="partitioning-support"></a>支援分割
hello 最後一件事 toonotice 有關親和性是不支援在資料分割 hello 父親和性關聯性。 我們最終可能會支援分割的父服務，但目前尚未允許這麼做。

## <a name="next-steps"></a>後續步驟
- 如需服務設定的詳細資訊，請[深入了解設定服務](service-fabric-cluster-resource-manager-configure-services.md)
- toolimit 服務 tooa 的一組小型機器或服務，使用的彙總 hello 負載[應用程式群組](service-fabric-cluster-resource-manager-application-groups.md)

[Image1]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-affinity/cluster-resrouce-manager-affinity-modes.png
[Image2]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-affinity/cluster-resource-manager-chains-vs-stars.png