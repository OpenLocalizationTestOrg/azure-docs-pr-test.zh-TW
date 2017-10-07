---
title: "Azure Service Fabric 可靠的服務的 hello 生命週期的 aaaOverview |Microsoft 文件"
description: "深入了解 Service Fabric 可靠的服務中的 hello 不同的生命週期事件"
services: Service-Fabric
documentationcenter: java
author: PavanKunapareddyMSFT
manager: timlt
ms.assetid: 
ms.service: Service-Fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: pakunapa;
ms.openlocfilehash: 6d48c217d12bc5248c2da57b544aac747cecd872
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

* 在啟動期間
  * 建構服務
  * 它們有機會 tooconstruct 與傳回零個或多個接聽程式
  * 任何傳回的接聽程式會開啟，可讓與 hello 服務的通訊
  * 呼叫 hello 服務 runAsync 方法，允許 hello 長時間執行的服務 toodo 或背景工作
* 在關閉期間
  * hello 取消語彙基元傳遞的 toorunAsync 會取消，且會關閉 hello 接聽程式
  * 完成後，hello 服務物件本身解構

沒有確切的這些事件排序的 hello 周圍的詳細資料。 特別是，事件 hello 順序有可能變更根據 hello 可靠的服務是無狀態或可設定狀態。 此外，可設定狀態服務，我們有 toodeal hello 主要交換案例。 在此順序，hello 主要角色是傳送的 tooanother 複本 （或恢復） 沒有 hello 服務正在關閉。 最後，我們有 toothink 相關錯誤或失敗的狀況。

## <a name="stateless-service-startup"></a>無狀態服務啟動
無狀態服務的 hello 生命週期是相當簡單。 以下是 hello 的事件順序：

1. hello 服務建構期間
2. 接著，兩件事平行發生︰
    - 叫用 `StatelessService.createServiceInstanceListeners()`，並「開啟」任何傳回的接聽程式 (在每個接聽程式上呼叫 `CommunicationListener.openAsync()`)
    - hello 服務的 runAsync 方法 (`StatelessService.runAsync()`) 呼叫
3. 如果存在，會呼叫 hello 服務本身 onOpenAsync 方法 (特別是，`StatelessService.onOpenAsync()`呼叫。 這是不常用的覆寫，但可用)。

很重要的 toonote 沒有 hello 呼叫 toocreate 與開啟的 hello 接聽程式和 runAsync 之間沒有順序。 runAsync 啟動之前，可能會開啟 hello 接聽程式。 同樣地，runAsync 最後可能之前已開啟 hello 通訊接聽程式，或甚至建構叫用。 如果任何同步處理，它會保持為練習 toohello 實作者。 常見的解決方案︰

* 有時，必須等到建立其他一些資訊或完成工作後，接聽程式才能運作。 工作通常可依 hello 服務的建構函式，在 hello 期間的無狀態服務`createServiceInstanceListeners()`呼叫，或 hello 建構 hello 接聽程式本身的一部分。
* 有時 hello runAsync 中的程式碼不想 toostart 直到 hello 接聽程式會開啟。 在此情況下，額外的協調有必要。 一個常見的解決方案是某些旗標，指出它們都完成時，它才能繼續 tooactual 工作簽入 runAsync hello 接聽程式內。

## <a name="stateless-service-shutdown"></a>無狀態服務關閉
當您關閉無狀態服務，遵循相同的模式，只是在反向 hello:

1. 平行
    - 「關閉」任何開啟的接聽程式 (在每個接聽程式上呼叫 `CommunicationListener.closeAsync()`)
    - hello 取消語彙基元傳遞太`runAsync()`取消 (檢查 hello 取消語彙基元的`isCancelled`屬性會傳回 true，如果呼叫 hello 語彙基元和`throwIfCancellationRequested`方法會擲回`CancellationException`)
2. 一次`closeAsync()`完成每個接聽程式和`runAsync()`也完成 hello 服務`StatelessService.onCloseAsync()`呼叫方法時，如果存在的話 （一次這是不常見的覆寫）。
3. 之後`StatelessService.onCloseAsync()`完成時，解構 hello 服務物件

## <a name="notes-on-service-lifecycle"></a>服務生命週期的注意事項
* 這兩個 hello`runAsync()`方法和 hello`createServiceInstanceListeners`呼叫是選擇性的。 一個服務可能具有其中一個、兩者或都沒有。 例如，hello 服務沒有回應 toouser 呼叫其工作，是否有不需要 tooimplement `runAsync()`。 只有 hello 通訊接聽程式和其相關聯的程式碼是必要的。 同樣地，建立和傳回通訊接聽程式是選擇性的因為 hello 服務可能會有背景工作 toodo，並因此只需要 tooimplement`runAsync()`
* 是有效的服務 toocomplete`runAsync()`已成功從它傳回。 這不是失敗狀況，並會表示 hello 服務完成的 hello 背景工作。 可設定狀態的可靠服務`runAsync()`如果 hello 服務都已從主要降級，且再升級後 tooprimary 會再次呼叫。
* 如果服務結束`runAsync()`擲回某些非預期的例外狀況，這是失敗和 hello 服務物件會關閉並回報健全狀況錯誤。
* 雖然在這些方法在傳回沒有沒有時間限制，您會立即失去 hello 能力 toowrite，因此無法完成任何實際工作。 建議您傳回為儘速收到 hello 取消要求。 如果您的服務沒有回應 toothese API 呼叫，在合理的時間服務網狀架構可能會強制終止您的服務。 這通常只發生在應用程式升級期間或刪除服務時。 此逾時預設為 15 分鐘。
* Hello 失敗`onCloseAsync()`path 結果中的`onAbort()`被呼叫的是最後一個機會最佳效能的機會 hello 註冊服務 tooclean 和釋放它們宣告任何資源。

> [!NOTE]
> Java 中尚未支援具狀態 Reliable Services。
>
>

## <a name="next-steps"></a>後續步驟
* [簡介 tooReliable 服務](service-fabric-reliable-services-introduction.md)
* [Reliable Services 快速入門](service-fabric-reliable-services-quick-start.md)
* [Reliable Services 的進階用法](service-fabric-reliable-services-advanced-usage.md)
