---
title: "hello Service Fabric 可靠服務程式設計模型 aaaOverview |Microsoft 文件"
description: "深入了解 Service Fabric 可靠的服務的程式設計模型，並開始撰寫自己的服務。"
services: Service-Fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: vturecek; mani-ramaswamy
ms.assetid: 0c88a533-73f8-4ae1-a939-67d17456ac06
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: masnider;
ms.openlocfilehash: 41d1826df902b1f1845c4702bf2567e6b9ca1f1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-overview"></a>Reliable Services 概觀
Azure Service Fabric 可簡化撰寫和管理無狀態與具狀態的 Reliable Services。 本主題涵蓋︰

* hello 可靠的服務之程式設計模型無狀態與可設定狀態服務。
* hello 選項時，您有 toomake 撰寫可靠的服務。
* 某些情況和時機的範例 toouse Reliable Services 和寫入的方式。

可靠的服務是一個 hello 程式設計模型服務網狀架構上可用。 其他 hello 是 hello Reliable Actor 的程式設計模型，提供虛擬執行者程式設計模型 hello 可靠的服務模型之上。 如需有關 hello Reliable Actors 程式設計模型的詳細資訊，請參閱[簡介 tooService 網狀架構 Reliable Actors](service-fabric-reliable-actors-introduction.md)。

Service Fabric 管理服務的佈建和部署升級和刪除，透過 hello 存留期間透過[Service Fabric 應用程式管理](service-fabric-deploy-remove-applications.md)。

## <a name="what-are-reliable-services"></a>什麼是 Reliable Services？
可靠的服務會提供簡單、 強大、 最上層的程式設計模型 toohelp 你什麼是重要的 tooyour 應用程式。 透過 hello 可靠服務程式設計模型，您可以取得：

* 存取 toohello 其餘的 hello Service Fabric 程式設計應用程式開發介面。 不同於 Service Fabric 服務模型化為[客體可執行檔](service-fabric-deploy-existing-app.md)，可靠的服務會直接取得 toouse hello 其餘的 hello Service Fabric 應用程式開發介面。 如此可讓服務︰
  * 查詢 hello 系統
  * 回報關於 hello 叢集中的實體的健全狀況
  * 接收有關設定和程式碼變更的通知
  * 尋找其他服務而與之通訊，
  * （選擇性） 使用 hello[可靠的集合](service-fabric-reliable-services-reliable-collections.md)
  * … 並提供他們存取 toomany 其他功能，全部從第一個類別的程式設計模型，以數種程式設計語言。
* 類似您所習慣使用之程式設計模型的簡單模型，以便執行您自己的程式碼。 您的程式碼會具有定義完善的切入點和容易管理的生命週期。
* 隨插即用的通訊模型。 使用您的選擇，例如使用 HTTP 的 hello 傳輸[Web API](service-fabric-reliable-services-communication-webapi.md)，WebSockets，自訂 TCP 通訊協定，或任何其他項目。 Reliable Services 提供一些很棒的現成選項供您使用，或者您可以提供您自己的選項。
* 可設定狀態服務，hello 可靠服務程式設計模型可讓您 tooconsistently 可靠地使用和儲存您位於您的服務狀態[可靠集合](service-fabric-reliable-services-reliable-collections.md)。 可靠的集合是一組簡單的高度可用且可靠的集合類別，將會是很熟悉 tooanyone 已使用 C# 集合。 傳統上，服務需要外部系統來進行可靠狀態管理。 與可靠的集合，您可以儲存您的狀態下一步 tooyour 的運算以 hello 相同的高可用性和可靠性您返回 tooexpect 從高可用性的外部存放區。 此模型也可以改善延遲，因為您會共置 hello 運算和它需要 toofunction 的狀態。

觀看此 Microsoft Virtual Academy 影片以取得 Reliable Services 概觀︰<center>
<a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=HhD9566yC_4106218965">
<img src="./media/service-fabric-reliable-services-introduction/ReliableServicesVid.png" WIDTH="360" HEIGHT="244" />
</a>
</center>

## <a name="what-makes-reliable-services-different"></a>Reliable Services 有什麼不同之處？
Service Fabric 中的可靠的服務與您之前撰寫的服務不同。 Service Fabric 提供可靠性、可用性、一致性和延展性。

* **可靠性**-您註冊服務會保持，甚至是在您的電腦失敗或叫用的網路問題的位置不可靠的環境或在其中 hello 服務本身的情況下會遇到的錯誤和損毀或失敗。 可設定狀態服務，您的狀態會保留即使在 hello 存在網路或其他失敗。
* **可用性** - 您的服務可供存取且有回應。 Service Fabric 會維護您所需的執行中複本數目。
* **延展性**-服務彼此分離時特定的硬體，以及他們可以擴張或縮小，視需要透過 hello 新增或移除硬體或其他資源。 服務已輕鬆地分割 （特別是在 hello 可設定狀態的情況下） tooensure hello 服務可調整且控制代碼部分失敗。 服務可以建立和刪除以動態方式透過程式碼，讓多個執行個體 toobe 調整大小如有必要，說出回應 toocustomer 要求。 最後，Service Fabric 鼓勵服務 toobe 輕量型。 服務網狀架構可讓數以千計的服務 toobe 佈建內單一處理序，而不需要或專用整個作業系統執行個體或處理程序 tooa 單一執行個體的服務。
* **一致性**-此服務中儲存的任何資訊才能保證 toobe 一致。 即使在服務內跨越多個可靠的集合也一樣。 利用交易不可部分完成的方式，即可在服務內跨集合進行變更。

## <a name="service-lifecycle"></a>服務生命週期
無論您的服務是具狀態還是無狀態，Reliable Services 會提供簡單的生命週期，可讓您快速插入您的程式碼，並開始著手。  有只有一個或兩個方法，您需要 tooimplement tooget 您的服務啟動並執行。

* **CreateServiceReplicaListeners/CreateServiceInstanceListeners** -這個方法是 hello 服務而定義，它想 toouse hello 通訊 stack(s)。 hello 通訊堆疊，例如[Web API](service-fabric-reliable-services-communication-webapi.md)、 是所定義的 hello 接聽端點或端點 hello （如何用戶端連線 hello 服務） 的服務。 它也會定義所顯示的 hello 訊息與 hello 其餘的 hello 服務程式碼之間的互動方式。
* **RunAsync** -此方法，而且您的服務執行其商務邏輯，它會開始進行關閉 hello hello 服務存留期間應該執行的任何背景工作。 hello 取消語彙基元提供是當該工作應該停止的信號。 例如，如果 hello 服務需要可靠的佇列 toopull 訊息並進行處理，這是該工作的發生位置。

如果您所學習的 hello 可靠服務第一次，閱讀 ！ 如果您要尋找的可靠的服務的 hello 生命週期的詳細逐步解說，您可以向透過太[本文](service-fabric-reliable-services-lifecycle.md)。

## <a name="example-services"></a>範例服務
了解這個程式設計模型，讓我們快速查看兩個不同的服務 toosee 這些部分配合。

### <a name="stateless-reliable-services"></a>無狀態的可靠的服務
無狀態服務是一個 where 沒有呼叫之間保留 hello 服務內的狀態。 任何已存在的狀態完全可丟棄，不需要同步處理、複寫、持續性或高可用性。

例如，請考慮沒有記憶體，一次接收所有的詞彙和作業 tooperform 計算機。

在此情況下，hello `RunAsync()` (C#) 或`runAsync()`(Java) 的 hello 服務可以是空白，因為沒有任何背景工作處理 hello 服務需要 toodo。 建立 hello 計算機服務時，它會傳回`ICommunicationListener`(C#) 或`CommunicationListener`(Java) (例如[Web API](service-fabric-reliable-services-communication-webapi.md))，會開啟某些連接埠上接聽端點。 這個接聽端點連結 toohello 不同的計算方法 (範例: 「 新增 （n1、 n2） 」)，定義 [小算盤] hello 公用 API。

從用戶端呼叫時，hello 適當的方法會叫用，並 hello 計算機服務 hello 上執行作業提供資料，並傳回 hello 結果的 hello。 它不會儲存任何狀態。

不儲存任何內部狀態會讓此範例計算機變得較簡單。 不過大多數服務並不是真正無狀態。 相反地，它們外部化其狀態 toosome 其他存放區。 (例如，任何依賴在備份存放區或快取中保留工作階段狀態的 Web 應用程式便不是無狀態)。

如何在無狀態服務的常見範例用於 Service Fabric 是做為前端公開 hello 公開 API 的 web 應用程式。 hello 前端服務然後交談 toostateful 服務 toocomplete 使用者要求。 在此情況下，用戶端的呼叫會導向的 tooa 已知連接埠 80，例如 hello 無狀態服務接聽的位置。 此無狀態服務收到 hello 呼叫，並判斷是否 hello 呼叫是來自受信任的合作對象和它的服務以為目的端。  然後，hello 無狀態服務轉送 hello 呼叫 toohello 正確的資料分割的 hello 具狀態服務，並等候回應。 當 hello 無狀態服務收到回應時，它會回覆 toohello 原始用戶端。 我們的 [C#](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started) / [Java](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Actors/VisualObjectActor/VisualObjectWebService) 範例中有這類服務的例子。 這是只有一個 hello 範例在這個模式的範例，還有其他在以及其他範例。

### <a name="stateful-reliable-services"></a>具狀態可靠的服務
必須有狀態保持一致且 hello 服務 toofunction 存在的某些部分的其中一個可設定狀態的服務。 假設有一個服務不斷地根據某個值收到的更新，計算它的滾動平均。 toodo，它必須有 hello 的連入要求需要 tooprocess 目前資料集和 hello 目前的平均。 擷取、處理並將資訊儲存在外部存放區 (例如現在的 Azure Blob 或資料表存放區) 的任何服務都是具狀態。 它只會 hello 外部狀態存放區中保存其狀態。

大部分服務今天儲存在外部，其狀態，因為 hello 外部存放區是什麼，為該狀態提供可靠性、 可用性、 延展性和一致性。 在 Service Fabric 服務不需要的 toostore 其狀態儲存在外部。 Service Fabric 會負責 hello 服務程式碼和 hello 服務狀態的需求。

> [!NOTE]
> Linux 上尚不支援 Stateful Reliable Services (針對 C# 或 Java)。
>

例如，假設我們想要 toowrite 處理影像的服務。 toodo 此映像和 hello 轉換 tooperform 該映像上的數列中的 hello 服務採用。 此服務會傳回一個通訊接聽程式 (假設是 WebAPI)，其中公開一個像 `ConvertImage(Image i, IList<Conversion> conversions)` 的 API。 當它收到要求時，hello 服務會儲存在`IReliableQueue`，並傳回某些識別碼 toohello 用戶端，讓它能夠追蹤 hello 要求。

在這個服務中，`RunAsync()` 可能較為複雜。 hello 服務有迴圈中的其`RunAsync()`的提取要求出`IReliableQueue`並執行要求的 hello 轉換。 hello 結果取得儲存在`IReliableDictionary`以便當 hello 用戶端重新上線時，就可以取得其已轉換的映像。 tooensure，即使發生失敗 hello 映像不會遺失，可靠的服務會從 hello 佇列提取、 執行 hello 轉換和 hello 結果儲存在單一交易中所有。 在此情況下，從 hello 佇列中移除 hello 訊息，並只 hello 轉換完成時，將會儲存在 hello 結果字典的 hello 結果。 或者，hello 服務無法提取從 hello 佇列 hello 映像，並立即將它儲存在遠端存放區。 這會減少 hello 狀態 hello 服務數量有 toomanage，但是會增加複雜性，因為 hello 服務有 tookeep hello 必要的中繼資料 toomanage hello 遠端存放區。 使用其中一個方法時，如果項目無法在 hello 中間 hello 要求會保持 hello 佇列等候 toobe 處理。

關於這項服務的一件事 toonote 為聽起來正常的.NET 服務 ！ hello 唯一的差別在於 hello 資料結構所使用 (`IReliableQueue`和`IReliableDictionary`) 所提供的服務的網狀架構，而且高度可靠、 可用，且一致。

## <a name="when-toouse-reliable-services-apis"></a>當 toouse 可靠的服務應用程式開發介面
如果 hello 下列任何一項描述應用程式服務的需求，您應該考慮可靠的服務 Api:

* 您想要您的服務程式碼 （和選擇性狀態） toobe 高度可用且可靠
* 您需要跨多個狀態單位 (例如，訂單和訂單明細項目) 的交易式保證。
* 您的應用程式狀態可以自然地模型化，做為可靠的字典和佇列。
* 您的應用程式程式碼或狀態需要 toobe 高可用性與低度延遲讀取和寫入。
* 您的應用程式需要 toocontrol hello 並行或資料粒度的交易作業，跨一或多個可靠的集合。
* 您想 toomanage hello 通訊或資料分割配置為您的服務控制 hello。
* 您的程式碼需要無限制執行緒的執行階段環境。
* 您的應用程式需要 toodynamically 建立或終結可靠字典或佇列或整個服務在執行階段。
* Tooprogrammatically 控制 Service Fabric 提供備份和還原功能所需的服務的狀態。
* 應用程式就需要其狀態的單位 toomaintain 變更歷程記錄。
* 您想要 toodevelop，或使用協力廠商開發的自訂狀態提供者。

## <a name="next-steps"></a>後續步驟
* [Reliable Services 快速入門](service-fabric-reliable-services-quick-start.md)
* [Reliable Services 的進階用法](service-fabric-reliable-services-advanced-usage.md)
* [hello Reliable Actors 程式設計模型](service-fabric-reliable-actors-introduction.md)
