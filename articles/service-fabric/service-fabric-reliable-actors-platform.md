---
title: "aaaReliable 上 Service Fabric 動作項目 |Microsoft 文件"
description: "描述如何 Reliable Actors 的分層上可靠的服務，並使用 hello hello Service Fabric 平台功能。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: 45839a7f-0536-46f1-ae2b-8ba3556407fb
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: vturecek
ms.openlocfilehash: ecffb54139f1171c7839b77fed0be60950881198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-reliable-actors-use-hello-service-fabric-platform"></a>Reliable Actors 使用 hello Service Fabric 平台的方式
本文說明 Reliable Actors hello Azure Service Fabric 平台上的運作方式。 位於呼叫 hello 可設定狀態可靠的服務實作的架構中執行 reliable Actors *actor 服務*。 hello actor 服務包含所有 hello 元件所需的 toomanage hello 生命週期和訊息發送您的動作項目：

* hello 動作項目執行階段生命週期，記憶體回收，並強制執行單一執行緒存取。
* 動作項目服務遠端接聽程式接受遠端存取呼叫 tooactors，並將它們傳送 tooa 發送器 tooroute toohello 適當的動作項目執行個體。
* hello 動作項目狀態提供者會包裝狀態提供者 （例如 hello 可靠集合狀態提供者），並提供動作項目狀態管理的介面卡。

這些元件一起表單 hello Reliable Actor 架構。

## <a name="service-layering"></a>將服務分層
Hello actor 服務本身是可靠的服務，因為所有 hello[應用程式模型](service-fabric-application-model.md)，生命週期，[封裝](service-fabric-package-apps.md)，[部署](service-fabric-deploy-remove-applications.md)、 升級和縮放比例的概念可靠的服務套用 hello tooactor 服務相同方式。 

![將動作項目服務分層][1]

hello 上圖顯示 hello hello Service Fabric 應用程式架構和使用者程式碼之間的關聯性。 藍色項目代表 hello 可靠的服務應用程式架構、 橙色代表 hello Reliable Actor 架構，而綠色代表使用者程式碼。

可靠的服務，在您的服務會繼承 hello`StatefulService`類別。 這個類別本身是衍生自 `StatefulServiceBase` (或無狀態服務的 `StatelessService`)。 中可靠的動作項目，您可以使用 hello 動作項目服務。 hello actor 服務是 hello 的不同實作`StatefulServiceBase`類別實作 hello actor 模式執行您的動作項目。 因為 hello actor 服務本身是實作的`StatefulServiceBase`，您可以撰寫您自己的服務衍生自`ActorService`和實作服務層級功能 hello 相同的方式進行繼承時`StatefulService`，例如：

* 服務備份與還原。
* 適用於所有動作項目的共用功能，例如斷路器。
* Hello actor 服務本身和每個個別的動作項目上的遠端程序呼叫。

> [!NOTE]
> Java/Linux 上目前不支援具狀態服務。

### <a name="using-hello-actor-service"></a>使用 hello 行動服務
動作項目執行個體具有存取 toohello 行動服務執行所在。 透過 hello 行動服務，動作項目執行個體可以透過程式設計方式取得 hello 服務內容。 hello 服務內容具有 hello 分割區識別碼、 服務名稱、 應用程式名稱和其他 Service Fabric 平台特定的資訊：

```csharp
Task MyActorMethod()
{
    Guid partitionId = this.ActorService.Context.PartitionId;
    string serviceTypeName = this.ActorService.Context.ServiceTypeName;
    Uri serviceInstanceName = this.ActorService.Context.ServiceName;
    string applicationInstanceName = this.ActorService.Context.CodePackageActivationContext.ApplicationName;
}
```
```Java
CompletableFuture<?> MyActorMethod()
{
    UUID partitionId = this.getActorService().getServiceContext().getPartitionId();
    String serviceTypeName = this.getActorService().getServiceContext().getServiceTypeName();
    URI serviceInstanceName = this.getActorService().getServiceContext().getServiceName();
    String applicationInstanceName = this.getActorService().getServiceContext().getCodePackageActivationContext().getApplicationName();
}
```


如同所有可靠的服務，hello actor 服務必須向 hello Service Fabric 執行階段中的服務類型。 Hello actor 服務 toorun 您的動作項目執行個體，也必須註冊動作項目類型與 hello 動作項目服務。 hello`ActorRuntime`註冊方法為執行者執行這項工作。 在 hello 最簡單的情況下，您就可以註冊您的動作項目類型和 hello actor 服務以預設設定將會隱含使用：

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>().GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```

或者，您可以使用服務所提供的 hello 註冊方法 tooconstruct hello 執行者自行 lambda。 您可以再設定 hello 行動服務，並明確建構您的動作項目執行個體，您可以在其中插入透過其建構函式的相依性 tooyour 動作項目：

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>(
            (context, actorType) => new ActorService(context, actorType, () => new MyActor()))
            .GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```
```Java
static class Program
{
    private static void Main()
    {
      ActorRuntime.registerActorAsync(
              MyActor.class,
              (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
              timeout);

        Thread.sleep(Long.MAX_VALUE);
    }
}
```

### <a name="actor-service-methods"></a>動作項目服務方法
hello 行動服務會實作`IActorService`(C#) 或`ActorService`(Java)，它接著會實作`IService`(C#) 或`Service`(Java)。 這是可靠的服務遠端處理，可讓服務方法的遠端程序呼叫所使用的 hello 介面。 它包含的服務層級方法可使用服務遠端處理功能從遠端呼叫。

#### <a name="enumerating-actors"></a>列舉動作項目
hello 行動服務可讓用戶端 hello 執行者 hello 服務裝載 tooenumerate 中繼資料。 因為 hello 行動服務資料分割的可設定狀態服務，執行列舉作業每個資料分割。 因為每個資料分割可能包含許多參與者，以一組分頁式結果傳回 hello 列舉型別。 hello 頁面被迴圈，直到讀取所有頁面。 下列範例會示範如何 hello toocreate 行動服務的一個資料分割中的所有作用中執行者的清單：

```csharp
IActorService actorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), partitionKey);

ContinuationToken continuationToken = null;
List<ActorInformation> activeActors = new List<ActorInformation>();

do
{
    PagedResult<ActorInformation> page = await actorServiceProxy.GetActorsAsync(continuationToken, cancellationToken);

    activeActors.AddRange(page.Items.Where(x => x.IsActive));

    continuationToken = page.ContinuationToken;
}
while (continuationToken != null);
```

```Java
ActorService actorServiceProxy = ActorServiceProxy.create(
    new URI("fabric:/MyApp/MyService"), partitionKey);

ContinuationToken continuationToken = null;
List<ActorInformation> activeActors = new ArrayList<ActorInformation>();

do
{
    PagedResult<ActorInformation> page = actorServiceProxy.getActorsAsync(continuationToken);

    while(ActorInformation x: page.getItems())
    {
         if(x.isActive()){
              activeActors.add(x);
         }
    }

    continuationToken = page.getContinuationToken();
}
while (continuationToken != null);
```

#### <a name="deleting-actors"></a>刪除動作項目
hello actor 服務也提供函式刪除動作項目：

```csharp
ActorId actorToDelete = new ActorId(id);

IActorService myActorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

await myActorServiceProxy.DeleteActorAsync(actorToDelete, cancellationToken)
```
```Java
ActorId actorToDelete = new ActorId(id);

ActorService myActorServiceProxy = ActorServiceProxy.create(
    new URI("fabric:/MyApp/MyService"), actorToDelete);

myActorServiceProxy.deleteActorAsync(actorToDelete);
```

如需有關刪除動作項目和其狀態的詳細資訊，請參閱 hello[執行者生命週期的文件](service-fabric-reliable-actors-lifecycle.md)。

### <a name="custom-actor-service"></a>自訂動作項目服務
您可以藉由使用 hello 執行者註冊 lambda，註冊您自己的自訂動作項目服務衍生自`ActorService`(C#) 和`FabricActorService`(Java)。 在此自訂動作項目服務中，您可以撰寫繼承 `ActorService` (C#) 或 `FabricActorService` (Java) 的服務，以實作自己的服務層級功能。 自訂動作項目服務繼承所有 hello 動作項目執行階段功能，從`ActorService`(C#) 或`FabricActorService`(Java) 而且可以使用的 tooimplement 您自己的服務方法。

```csharp
class MyActorService : ActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<ActorBase> newActor)
        : base(context, typeInfo, newActor)
    { }
}
```
```Java
class MyActorService extends FabricActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, BiFunction<FabricActorService, ActorId, ActorBase> newActor)
    {
         super(context, typeInfo, newActor);
    }
}
```

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>(
            (context, actorType) => new MyActorService(context, actorType, () => new MyActor()))
            .GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```
```Java
public class Program
{
    public static void main(String[] args)
    {
        ActorRuntime.registerActorAsync(
                MyActor.class,
                (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
                timeout);
        Thread.sleep(Long.MAX_VALUE);
    }
}
```

#### <a name="implementing-actor-backup-and-restore"></a>實作動作項目備份與還原
 在下列範例的 hello，hello 自訂動作項目服務所公開執行者資料備份方法 tooback 透過 hello 遠端接聽程式中已有運用`ActorService`:

```csharp
public interface IMyActorService : IService
{
    Task BackupActorsAsync();
}

class MyActorService : ActorService, IMyActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<ActorBase> newActor)
        : base(context, typeInfo, newActor)
    { }

    public Task BackupActorsAsync()
    {
        return this.BackupAsync(new BackupDescription(PerformBackupAsync));
    }

    private async Task<bool> PerformBackupAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
    {
        try
        {
           // store hello contents of backupInfo.Directory
           return true;
        }
        finally
        {
           Directory.Delete(backupInfo.Directory, recursive: true);
        }
    }
}
```
```Java
public interface MyActorService extends Service
{
    CompletableFuture<?> backupActorsAsync();
}

class MyActorServiceImpl extends ActorService implements MyActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<FabricActorService, ActorId, ActorBase> newActor)
    {
       super(context, typeInfo, newActor);
    }

    public CompletableFuture backupActorsAsync()
    {
        return this.backupAsync(new BackupDescription((backupInfo, cancellationToken) -> performBackupAsync(backupInfo, cancellationToken)));
    }

    private CompletableFuture<Boolean> performBackupAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
    {
        try
        {
           // store hello contents of backupInfo.Directory
           return true;
        }
        finally
        {
           deleteDirectory(backupInfo.Directory)
        }
    }

    void deleteDirectory(File file) {
        File[] contents = file.listFiles();
        if (contents != null) {
            for (File f : contents) {
               deleteDirectory(f);
             }
        }
        file.delete();
    }
}
```


在此範例中，`IMyActorService` 是遠端處理協定，它會實作 `IService` (C#) 與 `Service` (Java)，然後透過 `MyActorService` 來實作。 加上這個遠端服務合約，而方法`IMyActorService`現在也是可用 tooa 用戶端藉由建立透過遠端 proxy `ActorServiceProxy`:

```csharp
IMyActorService myActorServiceProxy = ActorServiceProxy.Create<IMyActorService>(
    new Uri("fabric:/MyApp/MyService"), ActorId.CreateRandom());

await myActorServiceProxy.BackupActorsAsync();
```
```Java
MyActorService myActorServiceProxy = ActorServiceProxy.create(MyActorService.class,
    new URI("fabric:/MyApp/MyService"), actorId);

myActorServiceProxy.backupActorsAsync();
```

## <a name="application-model"></a>應用程式模型
動作項目服務是可靠的服務，因此 hello 應用程式模型是 hello 相同。 不過，hello 執行者 framework 建置工具讓您有產生部分 hello 應用程式模型檔案。

### <a name="service-manifest"></a>服務資訊清單
hello 執行者 framework 建置工具自動產生 hello 行動服務的 ServiceManifest.xml 檔案內容。 此檔案包括：

* 動作項目服務類型。 hello 型別名稱會產生以動作項目的專案名稱為基礎。 根據您的動作項目上的 hello 持續性屬性，hello HasPersistedState 旗標會也隨之設定。
* 程式碼封裝。
* 組態封裝。
* 資源和端點。

### <a name="application-manifest"></a>應用程式資訊清單
hello 執行者 framework 建置工具自動建立您的行動服務的預設服務定義。 hello 建置工具填入 hello 預設服務屬性：

* 複本集計數取決於您的動作項目上的 hello 持續性屬性。 在您的動作項目上的每個時間 hello 持續性屬性變更時，會據以重設 hello 預設服務定義中的 hello 複本集計數。
* 資料分割配置和範圍會設定 tooUniform Int64 hello 完整 Int64 範圍。

## <a name="service-fabric-partition-concepts-for-actors"></a>動作項目的 Service Fabric 資料分割概念
動作項目服務是已資料分割的具狀態服務。 動作項目服務的每個分割區都包含一組動作項目。 服務分割區會自動散佈於 Service Fabric 中的多個節點上。 結果就是散佈動作項目執行個體。

![動作項目的資料分割和散佈][5]

您可以使用不同的分割區配置和分割區索引鍵範圍來建立 Reliable Services。 hello 行動服務會使用 hello 完整 Int64 關鍵範圍 toomap 執行者 toopartitions hello Int64 資料分割配置。

### <a name="actor-id"></a>動作項目識別碼
每個動作建立 hello 服務中的項目具有與它所 hello 表示相關聯的唯一識別碼`ActorId`類別。 `ActorId`是不透明的識別碼值，可用於執行者統一分佈在 hello 服務資料分割之間產生隨機識別碼：

```csharp
ActorProxy.Create<IMyActor>(ActorId.CreateRandom());
```
```Java
ActorProxyBase.create<MyActor>(MyActor.class, ActorId.newId());
```


每個`ActorId`是雜湊的 tooan Int64。 這就是為什麼 hello actor 服務必須使用 hello 完整 Int64 範圍的 Int64 資料分割配置。 不過，自訂識別碼值可用於 `ActorID`，包括 GUID/UUID、字串和 Int64。

```csharp
ActorProxy.Create<IMyActor>(new ActorId(Guid.NewGuid()));
ActorProxy.Create<IMyActor>(new ActorId("myActorId"));
ActorProxy.Create<IMyActor>(new ActorId(1234));
```
```Java
ActorProxyBase.create(MyActor.class, new ActorId(UUID.randomUUID()));
ActorProxyBase.create(MyActor.class, new ActorId("myActorId"));
ActorProxyBase.create(MyActor.class, new ActorId(1234));
```

當您使用的 Guid/Uuid 和字串 hello 值會是雜湊的 tooan Int64。 不過，當您明確地提供 Int64 tooan `ActorId`，hello Int64 會對應直接 tooa 資料分割而不進一步雜湊。 您可以使用這個技巧 toocontrol 分割 hello 執行者會放在其中。

## <a name="next-steps"></a>後續步驟
* [動作項目狀態管理](service-fabric-reliable-actors-state-management.md)
* [動作項目生命週期與記憶體回收](service-fabric-reliable-actors-lifecycle.md)
* [動作項目 API 參考文件](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [.NET 範例程式碼 (英文)](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Java 範例程式碼 (英文)](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-platform/actor-service.png
[2]: ./media/service-fabric-reliable-actors-platform/app-deployment-scripts.png
[3]: ./media/service-fabric-reliable-actors-platform/actor-partition-info.png
[4]: ./media/service-fabric-reliable-actors-platform/actor-replica-role.png
[5]: ./media/service-fabric-reliable-actors-introduction/distribution.png
