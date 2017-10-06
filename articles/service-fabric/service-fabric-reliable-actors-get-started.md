---
title: "aaaCreate 您第一次行動為基礎 Azure 微服務在 C# |Microsoft 文件"
description: "本教學課程將引導您完成建立、 偵錯和部署簡單動作項目為基礎的服務使用服務網狀架構 Reliable Actors hello 步驟。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d4aebe72-1551-4062-b1eb-54d83297f139
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ab4f75bef0adb6e70f0ead587475b3fb51e6e6a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a>開始使用 Reliable Actors
> [!div class="op_single_selector"]
> * [Windows 上的 C# ](service-fabric-reliable-actors-get-started.md)
> * [在 Linux 上使用 Java](service-fabric-reliable-actors-get-started-java.md)
> 
> 

本文章說明 Azure Service Fabric Reliable Actors hello 基本概念，並將引導您建立、 偵錯和部署 Visual Studio 中的簡單 Reliable Actor 應用程式。

## <a name="installation-and-setup"></a>安裝與設定
在開始之前，請確定您已擁有 hello Service Fabric 開發環境設定您的電腦上。
如果您需要 tooset 它，請參閱詳細的指示[如何 hello 開發環境 tooset](service-fabric-get-started.md)。

## <a name="basic-concepts"></a>基本概念
tooget 入門 Reliable Actors，您只需要 toounderstand 某些基本概念：

* **動作項目服務**。 Reliable Actors 被封裝在可靠的服務，可以部署在 hello 服務網狀架構基礎結構。 動作項目執行個體會在指定的服務執行個體中啟動。
* **動作項目註冊**。 為使用可靠的服務，Reliable Actor 服務需要 toobe 向 hello Service Fabric 執行階段。 此外，hello 動作項目類型必須 toobe 向 hello 動作項目執行階段。
* **動作項目介面**。 hello 執行者介面是使用的 toodefine 執行者的強型別的公用介面。 在 hello Reliable Actor 模型術語，hello 執行者介面會定義的 hello hello 執行者的訊息類型可以了解並處理。 hello 執行者介面由其他的動作，用戶端應用程式太 「 傳送 」 （非同步） 訊息 toohello 動作項目。 Reliable Actors 可實作多個介面。
* **ActorProxy 類別**。 hello ActorProxy 類別由用戶端應用程式 tooinvoke hello hello 執行者介面透過公開的方法。 hello ActorProxy 類別提供兩個重要功能：
  
  * 名稱解析： 它是無法 toolocate hello hello 叢集 （尋找 hello hello 叢集節點的裝載位置） 中的動作項目。
  * 錯誤處理： 它可以重試方法引動過程，和重新解析 hello 動作項目位置之後、 需要 hello 執行者 toobe 失敗，例如重新定位 tooanother hello 叢集中的節點。

下列規則的相關 tooactor 介面 hello 是值得一提的是：

* 動作項目介面方法無法多載。
* 動作項目介面方法不能有 out、ref 或選擇性參數。
* 不支援泛型介面。

## <a name="create-a-new-project-in-visual-studio"></a>在 Visual Studio 中建立新專案
以管理員身分啟動 Visual Studio 2015 或 Visual Studio 2017，並建立新的 Service Fabric 應用程式專案：

![適用於 Visual Studio 的 Service Fabric 工具 - 新專案][1]

在 hello 下一步 對話方塊中，您可以選擇 hello 類型的專案，您會想 toocreate。

![Service Fabric 專案範本][5]

Hello HelloWorld 專案，讓我們使用 hello 服務網狀架構 Reliable Actors 服務。

建立 hello 方案之後，您應該會看到下列結構的 hello:

![Service Fabric 專案結構][2]

## <a name="reliable-actors-basic-building-blocks"></a>Reliable Actors 項目基本建置組塊
典型的 Reliable Actors 方案是由 3 個專案組成：

* **hello 應用程式專案 (MyActorApplication)**。 這是封裝所有 hello 服務一起部署的 hello 專案。 它包含 hello *ApplicationManifest.xml*和 PowerShell 指令碼，以管理 hello 應用程式。
* **hello 介面專案 (MyActor.Interfaces)**。 這是包含 hello 執行者的 hello 介面定義的 hello 專案。 在 hello MyActor.Interfaces 專案中，您可以定義將由 hello 執行者 hello 方案中的 hello 介面。 動作項目介面可以定義任何專案中使用任何名稱，不過 hello 介面定義 hello 動作項目實作和呼叫 hello 動作項目，因此它通常會建立有意義 toodefine hello 用戶端共用的 hello 執行者合約中的組件分隔與 hello 動作項目實作，並且可由多個其他專案共用。

```csharp
public interface IMyActor : IActor
{
    Task<string> HelloWorld();
}
```

* **hello 行動服務專案 (MyActor)**。 這是 hello 專案使用 toodefine hello Service Fabric 服務進行 toohost hello 動作項目。 它包含 hello 執行者 hello 實作。 動作項目實作是類別，衍生自基底型別 hello`Actor`和實作 hello hello MyActor.Interfaces 專案中所定義的介面。 動作項目類別也必須實作的建構函式可接受`ActorService`執行個體和`ActorId`並將其傳遞 toohello 基底`Actor`類別。 這可允許平台相依性的建構函式相依性插入。

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<string> HelloWorld()
    {
        return Task.FromResult("Hello world!");
    }
}
```

hello actor 服務必須向 hello Service Fabric 執行階段中的服務類型。 在順序 hello Actor 服務 toorun 您的動作項目執行個體，動作項目類型也必須向 hello 動作項目服務。 hello`ActorRuntime`註冊方法為執行者執行這項工作。

```csharp
internal static class Program
{
    private static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<MyActor>(
                (context, actorType) => new ActorService(context, actorType, () => new MyActor())).GetAwaiter().GetResult();

            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ActorEventSource.Current.ActorHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

如果您從新的專案，Visual Studio 中啟動，您只能有一個動作項目定義 hello 註冊預設隨附在 Visual Studio 會產生的 hello 程式碼中。 如果您在 hello 服務中定義其他的動作，您會需要使用 tooadd hello 執行者註冊：

```csharp
 ActorRuntime.RegisterActorAsync<MyOtherActor>();

```

> [!TIP]
> hello Service Fabric 動作項目執行階段發出某些[事件和效能計數器相關 tooactor 方法](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters)。 這些項目對於診斷與效能監視很有幫助。
> 
> 

## <a name="debugging"></a>Debugging
Visual Studio 的 hello Service Fabric 工具支援偵錯在本機電腦上。 您可以叫用 hello F5 鍵啟動偵錯工作階段。 Visual Studio 會建置封裝 (如有必要)。 它也將 hello hello 本機 Service Fabric 叢集上的應用程式部署，並附加 hello 偵錯工具。

在 hello 部署過程中，您可以看到 hello hello 正在**輸出**視窗。

![Service Fabric 偵錯輸出視窗][3]

## <a name="next-steps"></a>後續步驟
深入了解[Reliable Actors 使用 hello Service Fabric 平台的方式](service-fabric-reliable-actors-platform.md)。

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject.PNG
[2]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-projectstructure.PNG
[3]: ./media/service-fabric-reliable-actors-get-started/debugging-output.PNG
[4]: ./media/service-fabric-reliable-actors-get-started/vs-context-menu.png
[5]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject1.PNG
