---
title: "從 Java SDK tooMaven-aaaMigrate 更新舊的 Azure 服務網狀架構 Java 應用程式 toouse Maven |Microsoft 文件"
description: "更新 hello 舊版 Java 應用程式使用 toouse hello Service Fabric Java SDK，從 Maven toofetch 服務網狀架構 Java 相依性。 完成此安裝後，舊版的 Java 應用程式將無法 toobuild。"
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: saysa
ms.openlocfilehash: 11b979facd7b3865141a6d3a035a6021dd06ca0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-previous-java-service-fabric-application-toofetch-java-libraries-from-maven"></a><span data-ttu-id="3869b-104">更新您先前 Java Service Fabric 應用程式 toofetch Java 文件庫從 Maven</span><span class="sxs-lookup"><span data-stu-id="3869b-104">Update your previous Java Service Fabric application toofetch Java libraries from Maven</span></span>
<span data-ttu-id="3869b-105">我們最近已從 hello Service Fabric Java SDK tooMaven 裝載移服務網狀架構 Java 二進位檔。</span><span class="sxs-lookup"><span data-stu-id="3869b-105">We have recently moved Service Fabric Java binaries from hello Service Fabric Java SDK tooMaven hosting.</span></span> <span data-ttu-id="3869b-106">現在您可以使用**mavencentral** toofetch hello 最新 Service Fabric Java 相依性。</span><span class="sxs-lookup"><span data-stu-id="3869b-106">Now you can use **mavencentral** toofetch hello latest Service Fabric Java dependencies.</span></span> <span data-ttu-id="3869b-107">此快速入門可協助您更新現有的 Java 應用程式，您稍早建立 toobe 搭配 Service Fabric Java SDK，使用任一 Yeoman 範本或 Eclipse toobe 與 hello 基礎 Maven 組建相容。</span><span class="sxs-lookup"><span data-stu-id="3869b-107">This quick-start helps you update your existing Java applications, which you earlier created toobe used with Service Fabric Java SDK, using either Yeoman template or Eclipse, toobe compatible with hello Maven based build.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3869b-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="3869b-108">Prerequisites</span></span>
1. <span data-ttu-id="3869b-109">首先，您必須 toouninstall hello 現有 Java SDK。</span><span class="sxs-lookup"><span data-stu-id="3869b-109">First you need toouninstall hello existing Java SDK.</span></span>

  ```bash
  sudo dpkg -r servicefabricsdkjava
  ```
2. <span data-ttu-id="3869b-110">安裝 hello 最新的 Service Fabric CLI 下列 hello 所述的步驟[這裡](service-fabric-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="3869b-110">Install hello latest Service Fabric CLI following hello steps mentioned [here](service-fabric-cli.md).</span></span>

3. <span data-ttu-id="3869b-111">toobuild 及 hello 服務網狀架構 Java 應用程式上的工作，您必須確認您有 JDK 1.8 且 Gradle 安裝 tooensure。</span><span class="sxs-lookup"><span data-stu-id="3869b-111">toobuild and work on hello Service Fabric Java applications, you need tooensure that you have JDK 1.8 and Gradle installed.</span></span> <span data-ttu-id="3869b-112">如果尚未安裝，您可以執行 JDK 1.8 (openjdk-8-jdk) 和 Gradle-下列 tooinstall hello</span><span class="sxs-lookup"><span data-stu-id="3869b-112">If not yet installed, you can run hello following tooinstall JDK 1.8 (openjdk-8-jdk) and Gradle -</span></span>

 ```bash
 sudo apt-get install openjdk-8-jdk-headless
 sudo apt-get install gradle
 ```
4. <span data-ttu-id="3869b-113">更新 hello 安裝/解除安裝指令碼的應用程式 toouse hello hello 步驟所述的新服務網狀架構 CLI[這裡](service-fabric-application-lifecycle-sfctl.md)。</span><span class="sxs-lookup"><span data-stu-id="3869b-113">Update hello install/uninstall scripts of your application toouse hello new Service Fabric CLI following hello steps mentioned [here](service-fabric-application-lifecycle-sfctl.md).</span></span> <span data-ttu-id="3869b-114">您可以使用參照 tooour 入門[範例](https://github.com/Azure-Samples/service-fabric-java-getting-started)供參考。</span><span class="sxs-lookup"><span data-stu-id="3869b-114">You can refer tooour getting-started [examples](https://github.com/Azure-Samples/service-fabric-java-getting-started) for reference.</span></span>

>[!TIP]
> <span data-ttu-id="3869b-115">解除安裝之後 hello Service Fabric Java SDK，Yeoman 將無法運作。</span><span class="sxs-lookup"><span data-stu-id="3869b-115">After uninstalling hello Service Fabric Java SDK, Yeoman will not work.</span></span> <span data-ttu-id="3869b-116">請依照下列所提及的 hello 必要條件[這裡](service-fabric-create-your-first-linux-application-with-java.md)toohave 服務網狀架構 Yeoman Java 向上範本產生器以及如何使用。</span><span class="sxs-lookup"><span data-stu-id="3869b-116">Follow hello Prerequisites mentioned [here](service-fabric-create-your-first-linux-application-with-java.md) toohave Service Fabric Yeoman Java template generator up and working.</span></span>

## <a name="service-fabric-java-libraries-on-maven"></a><span data-ttu-id="3869b-117">Maven 上的 Service Fabric Java 程式庫</span><span class="sxs-lookup"><span data-stu-id="3869b-117">Service Fabric Java libraries on Maven</span></span>
<span data-ttu-id="3869b-118">Service Fabric Java 程式庫已裝載於 Maven 中。</span><span class="sxs-lookup"><span data-stu-id="3869b-118">Service Fabric Java libraries have been hosted in Maven.</span></span> <span data-ttu-id="3869b-119">您可以在 hello 新增 hello 相依性``pom.xml``或``build.gradle``從您專案 toouse 服務網狀架構 Java 程式庫**mavenCentral**。</span><span class="sxs-lookup"><span data-stu-id="3869b-119">You can add hello dependencies in hello ``pom.xml`` or ``build.gradle`` of your projects toouse Service Fabric Java libraries from **mavenCentral**.</span></span>

### <a name="actors"></a><span data-ttu-id="3869b-120">動作項目</span><span class="sxs-lookup"><span data-stu-id="3869b-120">Actors</span></span>

<span data-ttu-id="3869b-121">您應用程式的 Service Fabric Reliable Actor 支援。</span><span class="sxs-lookup"><span data-stu-id="3869b-121">Service Fabric Reliable Actor support for your application.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-actors-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-actors-preview:0.10.0'
  }
  ```

### <a name="services"></a><span data-ttu-id="3869b-122">服務</span><span class="sxs-lookup"><span data-stu-id="3869b-122">Services</span></span>

<span data-ttu-id="3869b-123">您應用程式的 Service Fabric 無狀態服務支援。</span><span class="sxs-lookup"><span data-stu-id="3869b-123">Service Fabric Stateless Service support for your application.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-services-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-services-preview:0.10.0'
  }
  ```

### <a name="others"></a><span data-ttu-id="3869b-124">其他</span><span class="sxs-lookup"><span data-stu-id="3869b-124">Others</span></span>
#### <a name="transport"></a><span data-ttu-id="3869b-125">傳輸</span><span class="sxs-lookup"><span data-stu-id="3869b-125">Transport</span></span>

<span data-ttu-id="3869b-126">Service Fabric Java 應用程式的傳輸層支援。</span><span class="sxs-lookup"><span data-stu-id="3869b-126">Transport layer support for Service Fabric Java application.</span></span> <span data-ttu-id="3869b-127">您不需要 tooexplicitly 將此相依性 tooyour Reliable Actor 或服務應用程式，除非您在 hello 傳輸層級進行程式設計。</span><span class="sxs-lookup"><span data-stu-id="3869b-127">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications, unless you program at hello transport layer.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-transport-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-transport-preview:0.10.0'
  }
  ```

#### <a name="fabric-support"></a><span data-ttu-id="3869b-128">網狀架構支援</span><span class="sxs-lookup"><span data-stu-id="3869b-128">Fabric support</span></span>

<span data-ttu-id="3869b-129">系統層級支援適用於 Service Fabric，交談 toonative Service Fabric 執行階段。</span><span class="sxs-lookup"><span data-stu-id="3869b-129">System level support for Service Fabric, which talks toonative Service Fabric runtime.</span></span> <span data-ttu-id="3869b-130">您不需要 tooexplicitly 加入此相依性 tooyour Reliable Actor 或服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="3869b-130">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications.</span></span> <span data-ttu-id="3869b-131">從 Maven 自動擷取這取得，當您包含 hello 上述其他相依性。</span><span class="sxs-lookup"><span data-stu-id="3869b-131">This gets fetched automatically from Maven, when you include hello other dependencies above.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-preview:0.10.0'
  }
  ```


## <a name="migrating-service-fabric-stateless-service"></a><span data-ttu-id="3869b-132">移轉 Service Fabric 無狀態服務</span><span class="sxs-lookup"><span data-stu-id="3869b-132">Migrating Service Fabric Stateless Service</span></span>

<span data-ttu-id="3869b-133">現有 Service Fabric 無狀態 Java service 使用 Service Fabric 從 Maven 提取的相依性，您需要 tooupdate hello toobe 無法 toobuild ``build.gradle`` hello 服務內的檔案。</span><span class="sxs-lookup"><span data-stu-id="3869b-133">toobe able toobuild your existing Service Fabric stateless Java service using Service Fabric dependencies fetched from Maven, you need tooupdate hello ``build.gradle`` file inside hello Service.</span></span> <span data-ttu-id="3869b-134">先前使用它 toobe 類似如下-</span><span class="sxs-lookup"><span data-stu-id="3869b-134">Previously it used toobe like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
    compile project(':Interface')
}
.
.
.
jar {
    manifest {
    attributes(
                'Main-Class': 'statelessservice.MyStatelessServiceHost',
                "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
    baseName "MyStateless"
    destinationDir = file('./../MyStatelessApplication/MyStatelessPkg/Code')
}
.
.
.
task copyDeps <<{
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('*.jar')
    }
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('libj*.so')
    }
}
```
<span data-ttu-id="3869b-135">現在，從 Maven，toofetch hello 相依性 hello**更新**``build.gradle``必須 hello 對應組件，如下所示-</span><span class="sxs-lookup"><span data-stu-id="3869b-135">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
```
repositories {
        mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':Interface')
    azuresf ('com.microsoft.servicefabric:sf-services-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar {
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
        attributes(
                'Main-Class': 'statelessservice.MyStatelessServiceHost',
                "Class-Path": mpath)
    baseName "MyStateless"
    destinationDir = file('./../MyStatelessApplication/MyStatelessPkg/Code')
   }
}
.
.
.
task copyDeps <<{
    copy {
        from("lib/")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('*')
    }
}
```
<span data-ttu-id="3869b-136">一般情況下，tooget hello 如何建置指令碼的整體概念看起來會像 Service Fabric 無狀態 Java 服務，您可以從我們的快速入門範例會參考 tooany 範例。</span><span class="sxs-lookup"><span data-stu-id="3869b-136">In general, tooget an overall idea about how hello build script would look like for a Service Fabric stateless Java service, you can refer tooany sample from our getting-started examples.</span></span> <span data-ttu-id="3869b-137">以下是 hello [build.gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) hello EchoServer 範例。</span><span class="sxs-lookup"><span data-stu-id="3869b-137">Here is hello [build.gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) for hello EchoServer sample.</span></span>

## <a name="migrating-service-fabric-actor-service"></a><span data-ttu-id="3869b-138">移轉 Service Fabric 動作項目服務</span><span class="sxs-lookup"><span data-stu-id="3869b-138">Migrating Service Fabric Actor Service</span></span>

<span data-ttu-id="3869b-139">使用 Service Fabric 相依性從 Maven 提取您現有 Service Fabric 動作項目 Java 應用程式，您需要 tooupdate hello toobe 無法 toobuild ``build.gradle`` hello 介面封裝內和 hello 服務封裝中的檔案。</span><span class="sxs-lookup"><span data-stu-id="3869b-139">toobe able toobuild your existing Service Fabric Actor Java application using Service Fabric dependencies fetched from Maven, you need tooupdate hello ``build.gradle`` file inside hello interface package and in hello Service package.</span></span> <span data-ttu-id="3869b-140">如果您有 TestClient 封裝，您會需要 tooupdate 也一併。</span><span class="sxs-lookup"><span data-stu-id="3869b-140">If you have a TestClient package, you need tooupdate that as well.</span></span> <span data-ttu-id="3869b-141">因此，您的動作項目``Myactor``，hello 以下是需要 tooupdate-hello 地方</span><span class="sxs-lookup"><span data-stu-id="3869b-141">So, for your actor ``Myactor``, hello following would be hello places where you need tooupdate -</span></span>
```
./Myactor/build.gradle
./MyactorInterface/build.gradle
./MyactorTestClient/build.gradle
```

#### <a name="updating-build-script-for-hello-interface-project"></a><span data-ttu-id="3869b-142">更新 hello 介面專案的組建指令碼</span><span class="sxs-lookup"><span data-stu-id="3869b-142">Updating build script for hello interface project</span></span>

<span data-ttu-id="3869b-143">先前使用它 toobe 類似如下-</span><span class="sxs-lookup"><span data-stu-id="3869b-143">Previously it used toobe like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
}
.
.
```
<span data-ttu-id="3869b-144">現在，從 Maven，toofetch hello 相依性 hello**更新**``build.gradle``必須 hello 對應組件，如下所示-</span><span class="sxs-lookup"><span data-stu-id="3869b-144">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
```

#### <a name="updating-build-script-for-hello-actor-project"></a><span data-ttu-id="3869b-145">更新 hello 執行者專案的組建指令碼</span><span class="sxs-lookup"><span data-stu-id="3869b-145">Updating build script for hello actor project</span></span>

<span data-ttu-id="3869b-146">先前使用它 toobe 類似如下-</span><span class="sxs-lookup"><span data-stu-id="3869b-146">Previously it used toobe like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
    compile project(':MyactorInterface')
}
.
.
.
jar {
    manifest {
    attributes(
                'Main-Class': 'reliableactor.MyactorHost',
                "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
      baseName "myactor"
    destinationDir = file('./../myjavaapp/MyactorPkg/Code')
    }
}
.
.
.
task copyDeps<< {
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('*.jar')
    }
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('libj*.so')
    }
    copy {
        from("../MyactorInterface/out/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('*.jar')
    }
}
```
<span data-ttu-id="3869b-147">現在，從 Maven，toofetch hello 相依性 hello**更新**``build.gradle``必須 hello 對應組件，如下所示-</span><span class="sxs-lookup"><span data-stu-id="3869b-147">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':MyactorInterface')
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar {
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
        attributes(
                'Main-Class': 'reliableactor.MyactorHost',
                "Class-Path": mpath)
    baseName "myactor"
    destinationDir = file('../myjavaapp/MyactorPkg/Code')}
 }
.
.
.
task copyDeps<< {
      copy {
              from("lib/")
              into("../myjavaapp/MyactorPkg/Code/lib")
              include('*')
      }
      copy {
              from("../MyactorInterface/out/lib")
              into("../myjavaapp/MyactorPkg/Code/lib")
              include('*.jar')
      }
}
```

#### <a name="updating-build-script-for-hello-test-client-project"></a><span data-ttu-id="3869b-148">更新 hello 測試用戶端專案的組建指令碼</span><span class="sxs-lookup"><span data-stu-id="3869b-148">Updating build script for hello test client project</span></span>

<span data-ttu-id="3869b-149">以下變更是上一節，也就是 hello 執行者專案中所討論的類似 toohello 對。</span><span class="sxs-lookup"><span data-stu-id="3869b-149">Changes here are similar toohello changes discussed in previous section, that is, hello actor project.</span></span> <span data-ttu-id="3869b-150">先前 hello 的 Gradle toobe 用指令碼，如下所示-喜歡</span><span class="sxs-lookup"><span data-stu-id="3869b-150">Previously hello Gradle script used toobe like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
      compile project(':MyactorInterface')
}
.
.
.
jar
{
    manifest {
    attributes(
        'Main-Class': 'reliableactor.test.MyactorTestClient',
        "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
    }
    baseName "myactor-test"
  destinationDir = file('out/lib')
}
.
.
.
task copyDeps<< {
        copy {
                from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
        copy {
                from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
                into("./out/lib/lib")
                include('libj*.so')
        }
        copy {
                from("../MyactorInterface/out/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
}
```
<span data-ttu-id="3869b-151">現在，從 Maven，toofetch hello 相依性 hello**更新**``build.gradle``必須 hello 對應組件，如下所示-</span><span class="sxs-lookup"><span data-stu-id="3869b-151">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':MyactorInterface')
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar
{
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
    attributes(
                'Main-Class': 'reliableactor.test.MyactorTestClient',
                "Class-Path": mpath)
    baseName "myactor-test"
    destinationDir = file('./out/lib')
        }
}
.
.
.
task copyDeps<< {
        copy {
                from("lib/")
                into("./out/lib/lib")
                include('*')
        }
        copy {
                from("../MyactorInterface/out/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
}
```

## <a name="next-steps"></a><span data-ttu-id="3869b-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3869b-152">Next steps</span></span>

* [<span data-ttu-id="3869b-153">使用 Yeoman 在 Linux 上建立和部署第一個 Service Fabric Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="3869b-153">Create and deploy your first Service Fabric Java application on Linux by using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="3869b-154">在 Linux 上使用適用於 Eclipse 的 Service Fabric 外掛程式建立和部署第一個 Service Fabric Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="3869b-154">Create and deploy your first Service Fabric Java application on Linux by using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="3869b-155">互動使用 hello 服務網狀架構 CLI Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="3869b-155">Interact with Service Fabric clusters using hello Service Fabric CLI</span></span>](service-fabric-cli.md)
