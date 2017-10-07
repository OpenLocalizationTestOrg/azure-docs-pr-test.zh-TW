---
title: "aaaCreate 您第一次行動為基礎 Azure 微服務在 Java 中的 |Microsoft 文件"
description: "本教學課程將引導您完成建立、 偵錯和部署簡單動作項目為基礎的服務使用服務網狀架構 Reliable Actors hello 步驟。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d31dc8ab-9760-4619-a641-facb8324c759
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/04/2017
ms.author: vturecek
ms.openlocfilehash: 24718a8d7034360c53597f139169580f1a6ce732
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

本文章說明 Azure Service Fabric Reliable Actors hello 基本概念，並將告訴您如何建立和部署簡單的 Reliable Actor 應用程式在 Java 中。

## <a name="installation-and-setup"></a>安裝與設定
開始之前，請確定您擁有 hello Service Fabric 開發環境設定您的電腦上。
如果您需要 tooset 總太移[Mac 上開始使用](service-fabric-get-started-mac.md)或[開始使用 Linux](service-fabric-get-started-linux.md)。

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

## <a name="create-an-actor-service"></a>建立動作項目服務
以建立新 Service Fabric 應用程式的方式開始。 hello Service Fabric SDK for Linux 包含 Yeoman Service Fabric 應用程式與無狀態服務的產生器 tooprovide hello scaffolding。 開始執行 hello Yeoman 下列命令：

```bash
$ yo azuresfjava
```

請遵循 hello 指示 toocreate **Reliable Actor Service**。 本教學課程中，命名 hello 應用程式"HelloWorldActorApplication 」 和 hello 執行者 」 HelloWorldActor。 」 將建立下列 scaffolding hello:

```bash
HelloWorldActorApplication/
├── build.gradle
├── HelloWorldActor
│   ├── build.gradle
│   ├── settings.gradle
│   └── src
│       └── reliableactor
│           ├── HelloWorldActorHost.java
│           └── HelloWorldActorImpl.java
├── HelloWorldActorApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldActorPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   ├── _readme.txt
│       │   └── Settings.xml
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── HelloWorldActorInterface
│   ├── build.gradle
│   └── src
│       └── reliableactor
│           └── HelloWorldActor.java
├── HelloWorldActorTestClient
│   ├── build.gradle
│   ├── settings.gradle
│   ├── src
│   │   └── reliableactor
│   │       └── test
│   │           └── HelloWorldActorTestClient.java
│   └── testclient.sh
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="reliable-actors-basic-building-blocks"></a>Reliable Actors 項目基本建置組塊
hello 稍早所述的基本概念會轉譯為 hello 基本建置組塊 Reliable Actor 服務。

### <a name="actor-interface"></a>動作項目介面
這包含 hello 執行者的 hello 介面定義。 這個介面會定義 hello 動作項目實作和呼叫 hello 動作項目，因此它通常會建立它的位置中分隔與 hello 動作項目實作，並且可由多個其他共用的意義上 toodefine hello 用戶端共用的 hello 執行者合約服務或用戶端應用程式。

`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`：

```java
public interface HelloWorldActor extends Actor {
    @Readonly   
    CompletableFuture<Integer> getCountAsync();

    CompletableFuture<?> setCountAsync(int count);
}
```

### <a name="actor-service"></a>動作項目服務
這包含您的動作項目實作和動作項目註冊碼。 hello 動作項目類別實作 hello 動作項目介面。 這是您的動作項目工作之處。

`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`：

```java
@ActorServiceAttribute(name = "HelloWorldActor.HelloWorldActorService")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class HelloWorldActorImpl extends ReliableActor implements HelloWorldActor {
    Logger logger = Logger.getLogger(this.getClass().getName());

    protected CompletableFuture<?> onActivateAsync() {
        logger.log(Level.INFO, "onActivateAsync");

        return this.stateManager().tryAddStateAsync("count", 0);
    }

    @Override
    public CompletableFuture<Integer> getCountAsync() {
        logger.log(Level.INFO, "Getting current count value");
        return this.stateManager().getStateAsync("count");
    }

    @Override
    public CompletableFuture<?> setCountAsync(int count) {
        logger.log(Level.INFO, "Setting current count value {0}", count);
        return this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value);
    }
}
```

### <a name="actor-registration"></a>動作項目註冊
hello actor 服務必須向 hello Service Fabric 執行階段中的服務類型。 在順序 hello Actor 服務 toorun 您的動作項目執行個體，動作項目類型也必須向 hello 動作項目服務。 hello`ActorRuntime`註冊方法為執行者執行這項工作。

`HelloWorldActor/src/reliableactor/HelloWorldActorHost`：

```java
public class HelloWorldActorHost {

    public static void main(String[] args) throws Exception {

        try {
            ActorRuntime.registerActorAsync(HelloWorldActorImpl.class, (context, actorType) -> new ActorServiceImpl(context, actorType, ()-> new HelloWorldActorImpl()), Duration.ofSeconds(10));

            Thread.sleep(Long.MAX_VALUE);

        } catch (Exception e) {
            e.printStackTrace();
            throw e;
        }
    }
}
```

### <a name="test-client"></a>Test client
這是簡單的測試用戶端應用程式，您可以分開執行 hello Service Fabric 應用程式 tootest 動作項目服務。 這是範例的位置 hello ActorProxy 可以使用的 tooactivate 和動作項目執行個體進行通訊。 它不會與您的服務一同部署。

### <a name="hello-application"></a>hello 應用程式
最後，hello 應用程式套件 hello 動作項目服務和任何其他您可能會在未來一起部署的 hello 新增的服務。 它包含 hello *ApplicationManifest.xml*和 hello actor 服務封裝的預留位置。

## <a name="run-hello-application"></a>執行 hello 應用程式

hello Yeoman scaffolding 包含 gradle 指令碼 toobuild hello 應用程式和 bash 指令碼 toodeploy 和移除應用程式。 toodeploy hello 應用程式，第一個使用 gradle 的組建 hello 應用程式：

```bash
$ gradle
```

這會產生可以使用 Service Fabric Azure CLI 工具來部署的 Service Fabric 應用程式套件。

### <a name="deploy-service-fabric-cli"></a>部署 Service Fabric CLI

hello 為 install.sh 指令碼包含 hello 所需服務網狀架構 CLI (sfctl) 命令 toodeploy hello 應用程式套件。
執行 hello 為 install.sh 指令碼 toodeploy hello 應用程式。

```bash
$ ./install.sh
```

## <a name="next-steps"></a>後續步驟

* [開始使用 Service Fabric CLI](service-fabric-cli.md)
