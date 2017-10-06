---
title: "aaaCreate 您第一次可靠 Azure 微服務在 Java 中的 |Microsoft 文件"
description: "簡介 toocreating 無狀態與可設定狀態服務的 Microsoft Azure Service Fabric 應用程式。"
services: service-fabric
documentationcenter: java
author: vturecek
manager: timlt
editor: 
ms.assetid: 7831886f-7ec4-4aef-95c5-b2469a5b7b5d
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 577d96591797bbfe6be5c1094426b5f1435cca0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a>開始使用 Reliable Service
> [!div class="op_single_selector"]
> * [Windows 上的 C# ](service-fabric-reliable-services-quick-start.md)
> * [在 Linux 上使用 Java](service-fabric-reliable-services-quick-start-java.md)
>
>

本文章說明 hello Azure Service Fabric 可靠服務基本概念，並將告訴您如何建立及部署在 Java 中撰寫的簡單可靠的服務應用程式。 Microsoft Virtual Academy 影片也將示範如何 toocreate 無狀態 Reliable service:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965">  
<img src="./media/service-fabric-reliable-services-quick-start-java/ReliableServicesJavaVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="installation-and-setup"></a>安裝與設定
開始之前，請確定您擁有 hello Service Fabric 開發環境設定您的電腦上。
如果您需要 tooset 總太移[Mac 上開始使用](service-fabric-get-started-mac.md)或[開始使用 Linux](service-fabric-get-started-linux.md)。

## <a name="basic-concepts"></a>基本概念
tooget 開始使用可靠的服務，您只需要 toounderstand 某些基本概念：

* **服務類型**：這是您的服務實作。 它由您撰寫可擴充 hello 類別所定義`StatelessService`和任何其他程式碼或使用另有規定，以及名稱和版本號碼的相依性。
* **名為服務執行個體**: toorun 您的服務，您建立您的服務類型的具名執行個體更像建立的類別類型的物件執行個體。 服務執行個體實際上就是您所撰寫服務類型的物件具現化。
* **服務主機**: hello 名為您建立需要 toorun 主機內部的服務執行個體。 只要您的服務執行個體可以在上面執行的處理序 hello 服務主機。
* **服務註冊**：註冊可將所有項目結合在一起。 hello 服務類型必須註冊以 hello Service Fabric 服務中的執行階段裝載 tooallow Service Fabric toocreate 的執行個體，toorun。  

## <a name="create-a-stateless-service"></a>建立無狀態服務
從建立 Service Fabric 應用程式開始著手。 hello Service Fabric SDK for Linux 包含 Yeoman Service Fabric 應用程式與無狀態服務的產生器 tooprovide hello scaffolding。 開始執行 hello Yeoman 下列命令：

```bash
$ yo azuresfjava
```

請遵循 hello 指示 toocreate**可靠的無狀態服務**。 此教學課程中，名稱 hello 應用程式"HelloWorldApplication 」 和 hello 服務"HelloWorld"。 hello 結果包含目錄 hello`HelloWorldApplication`和`HelloWorld`。

```bash
HelloWorldApplication/
├── build.gradle
├── HelloWorld
│   ├── build.gradle
│   └── src
│       └── statelessservice
│           ├── HelloWorldServiceHost.java
│           └── HelloWorldService.java
├── HelloWorldApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   └── _readme.txt
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="implement-hello-service"></a>實作 hello 服務
開啟 **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**。 這個類別定義 hello 服務型別，而且可以執行任何程式碼。 hello 服務 API 提供兩個進入點的程式碼：

* 開放式的進入點方法 (稱為 `runAsync()`)，您可以在這裡開始執行任何工作負載，包括長時間執行的計算工作負載。

```java
@Override
protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {
    ...
}
```

* 通訊進入點，您可以在這裡插入選擇的通訊堆疊。 這就是您可以開始接收來自使用者和其他服務要求的地方。

```java
@Override
protected List<ServiceInstanceListener> createServiceInstanceListeners() {
    ...
}
```

在本教學課程中，我們將重點放在 hello`runAsync()`進入點方法。 這就是您可以立即開始執行程式碼的地方。

### <a name="runasync"></a>RunAsync
服務的執行個體時放置並準備好 tooexecute hello 平台會呼叫這個方法。 無狀態的服務，這只是表示開啟 hello 服務執行個體時。 取消語彙基元提供 toocoordinate 您服務執行個體需要 toobe 關閉時。 在 Service Fabric 服務執行個體的此開啟/關閉週期可以發生多次存留 hello hello 服務的整個。 發生這種情形的原因有很多，包括：

* hello 系統移動資源平衡服務執行的個體。
* 在您的程式碼中發生錯誤。
* hello 應用程式或系統也會升級。
* hello 基礎硬體發生中斷。

此協調流程由 Service Fabric tookeep 管理您的服務高可用性且正確平衡。

`runAsync()` 不應該同步封鎖。 RunAsync 的實作應該傳回 CompletableFuture tooallow hello 執行階段 toocontinue。 如果您的工作負載需要 tooimplement 長時間執行的工作應該在 hello CompletableFuture。

#### <a name="cancellation"></a>取消
取消您的工作負載是由提供取消語彙基元的 hello 協調合作式工作。 hello 系統會等到工作 tooend （由成功完成、 取消作業或錯誤） 之間移動之前。 它是重要的 toohonor hello 取消語彙基元，完成任何工作，並結束`runAsync()`hello 系統要求取消盡快。 hello 下列範例會示範如何 toohandle 取消事件：

```java
    @Override
    protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {

        // TODO: Replace hello following sample code with your own logic
        // or remove this runAsync override if it's not needed in your service.

        CompletableFuture.runAsync(() -> {
          long iterations = 0;
          while(true)
          {
            cancellationToken.throwIfCancellationRequested();
            logger.log(Level.INFO, "Working-{0}", ++iterations);

            try
            {
              Thread.sleep(1000);
            }
            catch (IOException ex) {}
          }
        });
    }
```

### <a name="service-registration"></a>服務註冊
服務類型必須向 hello Service Fabric 執行階段。 hello 服務類型定義於 hello`ServiceManifest.xml`和您的服務類別可實作`StatelessService`。 服務登錄是在 hello 程序的主要進入點執行。 在此範例中，hello 程序的主要進入點是`HelloWorldServiceHost.java`:

```java
public static void main(String[] args) throws Exception {
    try {
        ServiceRuntime.registerStatelessServiceAsync("HelloWorldType", (context) -> new HelloWorldService(), Duration.ofSeconds(10));
        logger.log(Level.INFO, "Registered stateless service type HelloWorldType.");
        Thread.sleep(Long.MAX_VALUE);
    }
    catch (Exception ex) {
        logger.log(Level.SEVERE, "Exception in registration:", ex);
        throw ex;
    }
}
```

## <a name="run-hello-application"></a>執行 hello 應用程式

hello Yeoman scaffolding 包含 gradle 指令碼 toobuild hello 應用程式和 bash 指令碼 toodeploy 和移除應用程式。 toorun hello 應用程式，第一個使用 gradle 的組建 hello 應用程式：

```bash
$ gradle
```

這會產生可使用 Service Fabric CLI 來部署的 Service Fabric 應用程式套件。

### <a name="deploy-with-service-fabric-cli"></a>使用 Service Fabric CLI 部署

hello 為 install.sh 指令碼包含 hello 所需服務網狀架構 CLI 命令 toodeploy hello 應用程式套件。 執行為 install.sh 的指令碼 toodeploy hello 應用程式。

```bash
$ ./install.sh
```

## <a name="next-steps"></a>後續步驟

* [開始使用 Service Fabric CLI](service-fabric-cli.md)
