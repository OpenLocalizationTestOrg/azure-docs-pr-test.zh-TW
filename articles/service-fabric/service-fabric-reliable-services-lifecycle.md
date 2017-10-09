---
title: "Azure Service Fabric 可靠的服務的 hello 生命週期的 aaaOverview |Microsoft 文件"
description: "深入了解 Service Fabric 可靠的服務中的 hello 不同的生命週期事件"
services: Service-Fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: vturecek;
ms.assetid: 
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 0d75ed5ee7cda85ac9af6a02e160727277804a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-lifecycle-overview"></a>Reliable Services 生命週期概觀
> [!div class="op_single_selector"]
> * [Windows 上的 C# ](service-fabric-reliable-services-lifecycle.md)
> * [在 Linux 上使用 Java](service-fabric-reliable-services-lifecycle-java.md)
>
>

在思考 hello 生命週期的可靠的服務，hello 生命週期的 hello 基本概念是最重要的 hello。 一般而言：

- 在啟動期間
  - 建構服務
  - 它們有機會 tooconstruct 與傳回零個或多個接聽程式
  - 任何傳回的接聽程式會開啟，可讓與 hello 服務的通訊
  - hello 服務 RunAsync 呼叫方法時，允許 hello toodo 長時間執行的服務或背景工作
- 在關閉期間
  - hello 取消語彙基元傳遞的 tooRunAsync 會取消，且會關閉 hello 接聽程式
  - 完成後，hello 服務物件本身解構

沒有確切的這些事件排序的 hello 周圍的詳細資料。 特別是，事件 hello 順序有可能變更根據 hello 可靠的服務是無狀態或可設定狀態。 此外，可設定狀態服務，我們有 toodeal hello 主要交換案例。 在此順序，hello 主要角色是傳送的 tooanother 複本 （或恢復） 沒有 hello 服務正在關閉。 最後，我們有 toothink 相關錯誤或失敗的狀況。

## <a name="stateless-service-startup"></a>無狀態服務啟動
無狀態服務的 hello 生命週期是相當簡單。 以下是 hello 的事件順序：

1. hello 服務建構期間
2. 接著，兩件事平行發生︰
    - 叫用 `StatelessService.CreateServiceInstanceListeners()`，並「開啟」任何傳回的接聽程式。 在每個接聽程式上呼叫 `ICommunicationListener.OpenAsync()`
    - hello 服務的`StatelessService.RunAsync()`方法呼叫
3. 如果有的話，hello 服務的`StatelessService.OnOpenAsync()`方法呼叫。 這是不常用的覆寫，但可用。

很重要的 toonote 沒有 hello 呼叫 toocreate 與開啟的 hello 接聽程式和 RunAsync 之間沒有順序。 RunAsync 啟動之前，可能會開啟 hello 接聽程式。 同樣地，RunAsync 最後可能之前已開啟 hello 通訊接聽程式，或甚至建構叫用。 如果任何同步處理，它會保持為練習 toohello 實作者。 常見的解決方案︰

  - 有時，必須等到建立其他一些資訊或完成工作後，接聽程式才能運作。 運作的無狀態服務通常可在其他位置完成，例如： 
    - 在 hello 服務建構函式
    - 在 hello`CreateServiceInstanceListeners()`呼叫
    - hello 建構 hello 接聽程式本身的一部分
  - 有時 hello RunAsync 中的程式碼不想 toostart 直到 hello 接聽程式會開啟。 在此情況下，額外的協調有必要。 一個常見的解決方案是某些旗標，指出當他們完成時的 hello 接聽程式內。 RunAsync 再檢查此旗標才能繼續 tooactual 工作。

## <a name="stateless-service-shutdown"></a>無狀態服務關閉
當您關閉無狀態服務，遵循相同的模式，只是在反向 hello:

1. 平行
    - 任何開啟的接聽程式皆為關閉。 在每個接聽程式上呼叫 `ICommunicationListener.CloseAsync()`。
    - hello 取消語彙基元傳遞太`RunAsync()`已取消。 檢查 hello 取消語彙基元的`IsCancellationRequested`屬性會傳回 true，如果呼叫 hello 語彙基元和`ThrowIfCancellationRequested`方法會擲回`OperationCanceledException`。
2. 一次`CloseAsync()`完成每個接聽程式和`RunAsync()`也完成 hello 服務`StatelessService.OnCloseAsync()`呼叫方法時，如果有的話。 它是不常見 toooverride `StatelessService.OnCloseAsync()`。
3. 之後`StatelessService.OnCloseAsync()`完成時，解構 hello 服務物件

## <a name="stateful-service-startup"></a>具狀態服務啟動
可設定狀態的服務有類似的模式 toostateless 服務，進行一些變更。 當可設定狀態的服務啟動時，事件 hello 順序如下所示：

1. hello 服務建構期間
2. 呼叫 `StatefulServiceBase.OnOpenAsync()`。 這是在 hello 服務 uncommonly 覆寫。
3. hello 會發生下列情況以平行方式
    - 叫用 `StatefulServiceBase.CreateServiceReplicaListeners()` 
      - 如果 hello 服務是主要會開啟所有傳回的接聽程式。 在每個接聽程式上呼叫 `ICommunicationListener.OpenAsync()`。
      - 如果次要 hello 服務，這些接聽程式會標示為`ListenOnSecondary = true`已開啟。 在「次要」上開啟的接聽程式較不常見。
    - 如果 hello 服務目前是主要的 hello 服務 hello`StatefulServiceBase.RunAsync()`方法呼叫
4. 一旦所有 hello 複本接聽程式`OpenAsync()`呼叫完成和`RunAsync()`呼叫時，`StatefulServiceBase.OnChangeRoleAsync()`呼叫。 這是在 hello 服務 uncommonly 覆寫。

同樣地 toostateless 服務沒有 hello 順序中的 hello 接聽程式會建立並開啟之間沒有進行協調，且呼叫 RunAsync 的時機。 如果您需要協調，hello 解決方案會更 hello 相同。 還有一個額外的案例： 說出 hello 呼叫抵達 hello 通訊接聽程式需要保留一些內的資訊[可靠集合](service-fabric-reliable-services-reliable-collections.md)。 因為 hello 通訊接聽程式無法開啟之前 hello 可靠集合是可讀取或寫入的而且 RunAsync 無法開始之前，某些其他的協調是必要的。 hello 通訊接聽程式 tooreturn hello 用戶端會使用 tooknow tooretry hello 要求一些錯誤程式碼為 hello 最簡單且最常見的方案。

## <a name="stateful-service-shutdown"></a>具狀態服務關閉
同樣地 tooStateless 服務 hello 生命週期事件在關機期間會 hello 相同期間啟動，但相反。 當具狀態服務正在關閉時，hello 發生下列事件：

1. 平行
    - 任何開啟的接聽程式皆為關閉。 在每個接聽程式上呼叫 `ICommunicationListener.CloseAsync()`。
    - hello 取消語彙基元傳遞太`RunAsync()`已取消。 檢查 hello 取消語彙基元的`IsCancellationRequested`屬性會傳回 true，如果呼叫 hello 語彙基元和`ThrowIfCancellationRequested`方法會擲回`OperationCanceledException`。
2. 一次`CloseAsync()`完成每個接聽程式和`RunAsync()`也完成 hello 服務`StatefulServiceBase.OnChangeRoleAsync()`呼叫。 （這是 uncommonly 覆寫在 hello 服務）。
    - 等候 RunAsync toocomplete 時才需要這個服務複本是否為主要。
3. 一次 hello`StatefulServiceBase.OnChangeRoleAsync()`方法完成，hello`StatefulServiceBase.OnCloseAsync()`方法呼叫。 這是不常用的覆寫，但可用。
3. 之後`StatefulServiceBase.OnCloseAsync()`完成時，解構 hello 服務物件。

## <a name="stateful-service-primary-swaps"></a>具狀態服務主要複本互換
當具狀態服務正在執行時，hello，可設定狀態服務的主要複本只有開啟其通訊接聽程式和呼叫其 RunAsync 方法。 建構次要，但看不到進一步的呼叫。 但是執行可設定狀態的服務時，可以變更目前是 hello 主要的複本。 這代表什麼的 hello 生命週期事件，可以看到複本？hello 行為 hello 可設定狀態的複本所看到取決於它是否 hello 複本正在降級或升級 hello 交換期間。

### <a name="for-hello-primary-being-demoted"></a>正在降級 hello 主要
Service Fabric 需要此複本 toostop，處理訊息並結束任何正在進行的背景工作。 如此一來，此步驟會尋找類似 toowhen hello 服務正在關閉。 其中一種差異是該 hello 服務並不是解構或已關閉，因為它會保持為次要資料庫。 呼叫下列應用程式開發介面的 hello:

1. 平行
    - 任何開啟的接聽程式皆為關閉。 在每個接聽程式上呼叫 `ICommunicationListener.CloseAsync()`。
    - hello 取消語彙基元傳遞太`RunAsync()`已取消。 檢查 hello 取消語彙基元的`IsCancellationRequested`屬性會傳回 true，如果呼叫 hello 語彙基元和`ThrowIfCancellationRequested`方法會擲回`OperationCanceledException`。
2. 一次`CloseAsync()`完成每個接聽程式和`RunAsync()`也完成 hello 服務`StatefulServiceBase.OnChangeRoleAsync()`呼叫。 這是在 hello 服務 uncommonly 覆寫。

### <a name="for-hello-secondary-being-promoted"></a>正在升級的次要 hello
同樣地，Service Fabric 需要此複本 toostart，接聽 hello 網路上的訊息，並啟動任何它所關心的背景工作。 如此一來，建立類似 toowhen hello 服務時，此程序會尋找該 hello 複本除了本身已存在。 呼叫下列應用程式開發介面的 hello:

1. 平行
    - 叫用 `StatefulServiceBase.CreateServiceReplicaListeners()`，並「開啟」任何傳回的接聽程式。 在每個接聽程式上呼叫 `ICommunicationListener.OpenAsync()`。
    - hello 服務的`StatefulServiceBase.RunAsync()`方法呼叫
2. 一旦所有 hello 複本接聽程式`OpenAsync()`呼叫完成和`RunAsync()`呼叫之後`StatefulServiceBase.OnChangeRoleAsync()`呼叫。 這是在 hello 服務 uncommonly 覆寫。

### <a name="common-issues-during-stateful-service-shutdown-and-primary-demotion"></a>具狀態服務關閉和主要降級期間的常見問題
Service Fabric 變更 hello 各種原因而具狀態服務的主要圖像。 hello 最常是[叢集重新平衡](service-fabric-cluster-resource-manager-balancing.md)和[應用程式升級](service-fabric-application-upgrade.md)。 這些作業期間 （以及在標準服務關機，您會看到 hello 服務是否已刪除的一樣），很重要的 hello 服務一方面 hello `CancellationToken`。 未完全處理取消作業的服務將會遇到幾個問題。 特別是，這些作業可能會變慢因為 Service Fabric 等候 hello 服務 toostop 依正常程序。 這可以最終會導致 toofailed 升級時間，並回復。 失敗 toohonor hello 取消語彙基元也會造成不平衡的叢集節點取得熱，但由於 toomove 太長，無法重新平衡 hello 服務，因為它們在其他地方。 

由於 hello 服務是可設定狀態，也可能時，他們使用 hello[可靠集合](service-fabric-reliable-services-reliable-collections.md)。 Service Fabric 中主要降級，當所發生的 hello 第一件事是 toohello 基礎狀態時，寫入權被撤銷。 這會導致 tooa 問題，可能會影響 hello 服務生命週期的第二個集合。 傳回例外狀況為基礎 hello 時間控制，以及是否 hello 複本移 hello 集合或關機。 應該正確處理這些例外狀況。 Service Fabric 擲回的例外狀況可分為永久性 [(`FabricException`)](https://docs.microsoft.com/en-us/dotnet/api/system.fabric.fabricexception?view=azure-dotnet) 和暫時性[(`FabricTransientException`)](https://docs.microsoft.com/en-us/dotnet/api/system.fabric.fabrictransientexception?view=azure-dotnet) 類別。 永久例外狀況要記錄，而且擲回，而 hello 暫時性例外狀況可能會重試根據一些重試邏輯。

來自使用 hello 的 hello 例外狀況處理`ReliableCollections`搭配服務生命週期事件會測試及驗證可靠的服務很重要的一部分。 hello 建議一律為 toorun 您在負載下的服務執行升級時， [chaos 測試](service-fabric-controlled-chaos.md)tooproduction 曾經在部署之前。 下列基本步驟協助確保您的服務正確地實作，並正確地處理生命週期事件。


## <a name="notes-on-service-lifecycle"></a>服務生命週期的注意事項
  - 這兩個 hello`RunAsync()`方法和 hello`CreateServiceReplicaListeners/CreateServiceInstanceListeners`呼叫是選擇性的。 一個服務可能具有其中一個、兩者或都沒有。 例如，hello 服務沒有回應 toouser 呼叫其工作，是否有不需要 tooimplement `RunAsync()`。 只有 hello 通訊接聽程式和其相關聯的程式碼是必要的。 同樣地，建立和傳回通訊接聽程式是選擇性的因為 hello 服務可能會有背景工作 toodo，並因此只需要 tooimplement`RunAsync()`
  - 是有效的服務 toocomplete`RunAsync()`已成功從它傳回。 完成不是失敗情況。 完成`RunAsync()`表示 hello 服務的 hello 背景工作已完成。 可設定狀態的可靠服務`RunAsync()`hello 複本都已從主要 tooSecondary 降級，然後升級後 tooPrimary 如果再次呼叫。
  - 如果服務藉由擲回某些非預期的例外狀況退出 `RunAsync()`，則會構成失敗。 hello 服務物件會關閉，而且一個健全狀況報告錯誤。
  - 雖然在這些方法在傳回沒有沒有時間限制，您會立即失去 hello 能力 toowrite tooReliable 集合，因此無法完成任何實際工作。 建議您傳回為儘速收到 hello 取消要求。 如果您的服務沒有回應 toothese API 呼叫，在合理的時間服務網狀架構可能會強制終止您的服務。 這通常只發生在應用程式升級期間或刪除服務時。 此逾時預設為 15 分鐘。
  - Hello 失敗`OnCloseAsync()`path 結果中的`OnAbort()`被呼叫的是最後一個機會最佳效能的機會 hello 註冊服務 tooclean 和釋放它們宣告任何資源。

## <a name="next-steps"></a>後續步驟
- [簡介 tooReliable 服務](service-fabric-reliable-services-introduction.md)
- [Reliable Services 快速入門](service-fabric-reliable-services-quick-start.md)
- [Reliable Services 的進階用法](service-fabric-reliable-services-advanced-usage.md)
