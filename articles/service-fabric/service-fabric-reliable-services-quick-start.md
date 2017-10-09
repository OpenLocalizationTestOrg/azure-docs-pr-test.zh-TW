---
title: "aaaCreate C# 中的第一個 Service Fabric 應用程式 |Microsoft 文件"
description: "簡介 toocreating 無狀態與可設定狀態服務的 Microsoft Azure Service Fabric 應用程式。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d9b44d75-e905-468e-b867-2190ce97379a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/06/2017
ms.author: vturecek
ms.openlocfilehash: e95e67cc84be1b83c936b250cae9112ddc77b963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a>開始使用 Reliable Service
> [!div class="op_single_selector"]
> * [Windows 上的 C# ](service-fabric-reliable-services-quick-start.md)
> * [Linux 上的 Java](service-fabric-reliable-services-quick-start-java.md)
> 
> 

Azure Service Fabric 應用程式包含一個或多個執行您的程式碼的服務。 本指南也說明如何 toocreate 無狀態與可設定狀態的 Service Fabric 應用程式與[可靠服務](service-fabric-reliable-services-introduction.md)。  Microsoft Virtual Academy 影片也將示範如何 toocreate 無狀態 Reliable service:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965">  
<img src="./media/service-fabric-reliable-services-quick-start/ReliableServicesVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="basic-concepts"></a>基本概念
tooget 開始使用可靠的服務，您只需要 toounderstand 某些基本概念：

* **服務類型**：這是您的服務實作。 它由您撰寫可擴充 hello 類別所定義`StatelessService`和任何其他程式碼或使用另有規定，以及名稱和版本號碼的相依性。
* **名為服務執行個體**: toorun 您的服務，您建立您的服務類型的具名執行個體更像建立的類別類型的物件執行個體。 服務執行個體已使用 hello URI 的 hello 表單中的名稱 「 網狀架構: /"配置，例如"fabric: / MyApp/MyService"。
* **服務主機**: hello 名為您建立需要 toorun 主機處理序內的服務執行個體。 只要您的服務執行個體可以在上面執行的處理序 hello 服務主機。
* **服務註冊**：註冊可將所有項目結合在一起。 hello 服務類型必須註冊以 hello Service Fabric 服務中的執行階段裝載 tooallow Service Fabric toocreate 的執行個體，toorun。  

## <a name="create-a-stateless-service"></a>建立無狀態服務
無狀態服務是一種服務正在為雲端應用程式中的 hello 範數。 因為 hello 服務本身不包含需要 toobe 可靠地儲存，或成為高可用性的資料，則會視為無狀態。 如果無狀態服務的執行個體關閉，其所有內部狀態都會遺失。 在這種服務，狀態必須是永續性的 tooan 外部存放區，例如 Azure 資料表或 SQL 資料庫中，為其 toobe 會進行高度可用且可靠。

以管理員身分啟動 Visual Studio 2015 或 Visual Studio 2017，並建立新的 Service Fabric 應用程式專案，命名為 HelloWorld：

![使用 hello 新增專案 對話方塊的方塊 toocreate 新的 Service Fabric 應用程式](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject.png)

然後建立名為 *HelloWorldStateless*的無狀態服務專案：

![在 hello 第二個對話方塊中，建立無狀態服務專案](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject2.png)

您的方案現在包含兩個專案：

* *HelloWorld*。 這是 hello*應用程式*專案，其中包含您*服務*。 它也包含說明 hello 應用程式，以及一些可協助您 toodeploy PowerShell 指令碼應用程式的 hello 應用程式資訊清單。
* *HelloWorldStateless*。 這是 hello 服務專案。 它包含 hello 無狀態服務實作。

## <a name="implement-hello-service"></a>實作 hello 服務
開啟 hello **HelloWorldStateless.cs** hello 服務專案中的檔案。 在 Service Fabric 中，服務可以執行任何商務邏輯。 hello 服務 API 提供兩個進入點的程式碼：

* 開放式的進入點方法，稱為 *RunAsync*，您可以在這裡開始執行任何工作負載，包括長時間執行的計算工作負載。

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    ...
}
```

* 通訊進入點，您可以在這裡插入選擇的通訊堆疊，例如 ASP.NET Core。 這就是您可以開始接收來自使用者和其他服務要求的地方。

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}
```

在本教學課程中，我們將著重在 hello`RunAsync()`進入點方法。 這就是您可以立即開始執行程式碼的地方。
hello 專案範本包含的範例實作`RunAsync()`增量循環計數。

> [!NOTE]
> 如需如何 toowork 通訊堆疊的詳細資訊，請參閱[與 OWIN 自我主控的服務網狀架構 Web API 服務](service-fabric-reliable-services-communication-webapi.md)
> 
> 

### <a name="runasync"></a>RunAsync
```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    long iterations = 0;

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        ServiceEventSource.Current.ServiceMessage(this, "Working-{0}", ++iterations);

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
}
```

服務的執行個體時放置並準備好 tooexecute hello 平台會呼叫這個方法。 無狀態的服務，這只是表示開啟 hello 服務執行個體時。 取消語彙基元提供 toocoordinate 您服務執行個體需要 toobe 關閉時。 在 Service Fabric 服務執行個體的此開啟/關閉週期可以發生多次存留 hello hello 服務的整個。 發生這種情形的原因有很多，包括：

* hello 系統移動資源平衡服務執行的個體。
* 在您的程式碼中發生錯誤。
* hello 應用程式或系統也會升級。
* hello 基礎硬體發生中斷。

此協調流程由 hello 系統 tookeep 管理您的服務高可用性且正確平衡。

`RunAsync()` 不應該同步封鎖。 RunAsync 的實作應該傳回的工作，或等待任何長時間執行或封鎖作業 tooallow hello 執行階段 toocontinue 上。 請注意，在 hello `while(true)` hello 前一個範例中，傳回工作的迴圈`await Task.Delay()`用。 如果您的工作負載必須同步封鎖，您應該使用 `Task.Run()` 在您的 `RunAsync` 實作中排定一個新的工作。

取消您的工作負載是由提供取消語彙基元的 hello 協調合作式工作。 hello 系統將會等到工作 tooend （由成功完成、 取消作業或錯誤） 之間移動之前。 它是重要的 toohonor hello 取消語彙基元，完成任何工作，並結束`RunAsync()`hello 系統要求取消盡快。

無狀態服務在本例中，hello 計數會儲存在本機變數。 但 hello 儲存的值，這是無狀態服務，因為存在只會針對目前 hello 其服務執行個體生命週期。 當 hello 服務移動或重新啟動時，將會遺失 hello 值。

## <a name="create-a-stateful-service"></a>建立具狀態服務
Service Fabric 導入了一種可設定狀態的新服務。 可設定狀態的服務可以維護可靠地 hello 服務本身，共 hello 正在使用它的程式碼中的狀態。 狀態進行高可用性服務網狀架構不含 hello 需要 toopersist 狀態 tooan 外部存放區。

tooconvert 無狀態 toohighly 可用且持續性的計數器值，即使 hello 服務移動或重新啟動時，您需要具狀態的服務。

在 hello 相同*HelloWorld*應用程式，可以加入新的服務，以滑鼠右鍵按一下在 hello 應用程式專案，並選取 hello uddi 服務參照**新增-> 新增 Service Fabric 服務**。

![新增服務 tooyour Service Fabric 應用程式](media/service-fabric-reliable-services-quick-start/hello-stateful-NewService.png)

選取 [具狀態服務]  並將它命名為 *HelloWorldStateful*。 按一下 [確定] 。

![使用 hello 新增專案 對話方塊的方塊 toocreate 新的 Service Fabric 具狀態服務](media/service-fabric-reliable-services-quick-start/hello-stateful-NewProject.png)

您的應用程式現在應該會有兩個服務： hello 無狀態服務*HelloWorldStateless*和 hello 可設定狀態服務*HelloWorldStateful*。

可設定狀態的服務具有 hello 為無狀態服務的同一個進入點。 hello 主要差異在於 hello 可用性*狀態提供者*可以可靠地儲存狀態。 Service Fabric 隨附呼叫狀態提供者實作[可靠集合](service-fabric-reliable-services-reliable-collections.md)，可讓您建立可靠的狀態管理員的 hello 透過複寫的資料結構。 具狀態可靠服務預設會使用此狀態供應器。

開啟**HelloWorldStateful.cs**中*HelloWorldStateful*，其中包含下列 RunAsync 方法 hello:

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        using (var tx = this.StateManager.CreateTransaction())
        {
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");

            ServiceEventSource.Current.ServiceMessage(this, "Current Counter Value: {0}",
                result.HasValue ? result.Value.ToString() : "Value does not exist.");

            await myDictionary.AddOrUpdateAsync(tx, "Counter", 0, (key, value) => ++value);

            // If an exception is thrown before calling CommitAsync, hello transaction aborts, all changes are
            // discarded, and nothing is saved toohello secondary replicas.
            await tx.CommitAsync();
        }

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
```

### <a name="runasync"></a>RunAsync
`RunAsync()` 在具狀態和無狀態服務中的運作方式類似。 不過，在可設定狀態的服務中，hello 平台執行額外工作代替您執行前先`RunAsync()`。 這項工作可確保該 hello 可靠狀態管理員和可靠的集合是準備 toouse。

### <a name="reliable-collections-and-hello-reliable-state-manager"></a>可靠的集合和 hello 可靠狀態管理員
```csharp
var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
```

[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx)是字典實作，您可以使用 tooreliably hello 服務中的存放區狀態。 Service Fabric 和可靠的集合，您可以直接在您的服務而 hello 需要在外部的持續性存放區中儲存資料。 可靠的集合可讓您的資料具備高可用性。 Service Fabric 會藉由為您建立與管理服務的多個複本  來完成此作業。 它也提供 API，以區隔離開 hello 變得複雜，管理這些複本和其狀態轉換。

可靠的集合可以儲存任何 .NET 類型 (包括您的自訂類型)，不過有幾個需要注意的事項：

* Service Fabric 讓高可用性，您的狀態*複寫*跨節點和可靠的集合狀態儲存資料 toolocal 磁碟上每個複本。 這表示所有儲存在可靠的集合中的項目必須可序列化 。 根據預設，使用可靠集合[DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx)進行序列化，因此，確定您的型別是重要 toomake [hello 資料合約序列化程式所支援](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx)當您使用 hello 預設序列化程式。
* 當您在可靠的集合上認可交易時，物件會複寫以獲得高可用性。 儲存在可靠集合中的物件會保留在服務中的本機記憶體。 這表示您有本機參考 toohello 物件。
  
   請務必您不要變更這些物件的本機執行個體不在交易中執行 hello 可靠集合上的更新作業。 這是因為不會自動複寫的物件變更 toolocal 執行個體。 您必須重新 hello 物件插入回 hello 字典，或使用其中一種 hello*更新*hello 字典上的方法。

hello 可靠狀態管理員會為您管理可靠的集合。 您可以只要求 hello 可靠狀態管理員可靠的集合名稱在任何時候，而且在任何地方在您的服務。 hello 可靠狀態管理員可確保重新取得的參考。 我們不建議您儲存參考 tooreliable 集合執行個體中的類別成員變數或屬性。 特別注意，必須進行設定 hello 參考的 tooensure tooan 執行個體隨時 hello 服務生命週期中。 hello 可靠狀態管理員處理這項工作，並針對重複的瀏覽進行最佳化。

### <a name="transactional-and-asynchronous-operations"></a>交易式和非同步作業
```C#
using (ITransaction tx = this.StateManager.CreateTransaction())
{
    var result = await myDictionary.TryGetValueAsync(tx, "Counter-1");

    await myDictionary.AddOrUpdateAsync(tx, "Counter-1", 0, (k, v) => ++v);

    await tx.CommitAsync();
}
```

可靠的集合都具有許多 hello 相同的作業，其`System.Collections.Generic`和`System.Collections.Concurrent`對應項目，除非 LINQ。 可靠的集合上的作業是非同步的。 這是因為與可靠的集合寫入作業執行 I/O 作業 tooreplicate 和保存資料 toodisk。

可靠的集合作業為「交易式」 作業，因此您可以在多個可靠的集合和作業之間維持狀態的一致。 比方說，您可能會清除佇列工作項目從可靠的佇列、 上，執行作業和可靠的字典，全部都在單一交易中儲存 hello 結果。 這會被視為不可部分完成的作業，而且它不保證是 hello 整個作業會成功，或 hello 整個作業會回復。 如果您清除佇列 hello 項目之後，就會發生錯誤，但儲存 hello 結果前，回復 hello 整個交易，並 hello 項目保持開啟 hello 佇列中進行處理。

## <a name="run-hello-application"></a>執行 hello 應用程式
我們現在傳回 toohello *HelloWorld*應用程式。 您現在可以建置並部署您的服務。 當您按**F5**，您的應用程式將會建置及部署 tooyour 本機叢集。

Hello 服務開始執行之後，您可以檢視中的 hello 產生事件的 Windows 追蹤 (ETW) 事件**診斷事件**視窗。 請注意，顯示 hello 事件從 hello 無狀態服務和 hello hello 應用程式中可設定狀態的服務。 您可以暫停 hello 資料流，依序按一下 hello**暫停** 按鈕。 接著，您可以檢查 hello 訊息詳細資料的方法是展開該訊息。

> [!NOTE]
> 執行 hello 應用程式之前，請確定您已執行的本機開發叢集。 簽出 hello[入門指南](service-fabric-get-started.md)如需有關設定本機環境資訊。
> 
> 

![在 Visual Studio 中檢視診斷事件](media/service-fabric-reliable-services-quick-start/hello-stateful-Output.png)

## <a name="next-steps"></a>後續步驟
[在 Visual Studio 中偵錯 Service Fabric 應用程式](service-fabric-debugging-your-application.md)

[開始使用：Service Fabric Web API 服務與 OWIN 自我裝載 | Microsoft Azure](service-fabric-reliable-services-communication-webapi.md)

[深入了解可靠的集合](service-fabric-reliable-services-reliable-collections.md)

[部署應用程式](service-fabric-deploy-remove-applications.md)

[應用程式升級](service-fabric-application-upgrade.md)

[Reliable Services 的開發人員參考資料](https://msdn.microsoft.com/library/azure/dn706529.aspx)

