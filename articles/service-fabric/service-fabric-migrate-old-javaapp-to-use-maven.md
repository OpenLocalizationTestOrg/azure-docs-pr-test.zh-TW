---
title: "從 Java SDK 移轉至 Maven - 更新舊版 Azure Service Fabric Java 應用程式以使用 Maven | Microsoft Docs"
description: "更新用於使用 Service Fabric Java SDK 的舊版 Java 應用程式，以從 Maven 擷取 Service Fabric Java 相依性。 完成此設定之後，就能夠建置舊版 Java 應用程式。"
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
ms.openlocfilehash: 2123c5f26d77045bd22af56a844fdbf222930e7b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="update-your-previous-java-service-fabric-application-to-fetch-java-libraries-from-maven"></a><span data-ttu-id="d43e7-104">更新先前的 Java Service Fabric 應用程式，以從 Maven 擷取 Java 程式庫</span><span class="sxs-lookup"><span data-stu-id="d43e7-104">Update your previous Java Service Fabric application to fetch Java libraries from Maven</span></span>
<span data-ttu-id="d43e7-105">我們最近已將 Service Fabric Java 二進位檔從 Service Fabric Java SDK 移至 Maven 主機。</span><span class="sxs-lookup"><span data-stu-id="d43e7-105">We have recently moved Service Fabric Java binaries from the Service Fabric Java SDK to Maven hosting.</span></span> <span data-ttu-id="d43e7-106">您現在可以使用 **mavencentral** 擷取最新的 Service Fabric Java 相依性。</span><span class="sxs-lookup"><span data-stu-id="d43e7-106">Now you can use **mavencentral** to fetch the latest Service Fabric Java dependencies.</span></span> <span data-ttu-id="d43e7-107">本快速入門可協助您更新要與以 Maven 為基礎的組建相容的現有 Java 應用程式，您稍早使用 Yeoman 範本或 Eclipse 建立這些應用程式，以便搭配 Service Fabric Java SDK 使用。</span><span class="sxs-lookup"><span data-stu-id="d43e7-107">This quick-start helps you update your existing Java applications, which you earlier created to be used with Service Fabric Java SDK, using either Yeoman template or Eclipse, to be compatible with the Maven based build.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d43e7-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="d43e7-108">Prerequisites</span></span>
1. <span data-ttu-id="d43e7-109">首先，您必須解除安裝現有的 Java SDK。</span><span class="sxs-lookup"><span data-stu-id="d43e7-109">First you need to uninstall the existing Java SDK.</span></span>

  ```bash
  sudo dpkg -r servicefabricsdkjava
  ```
2. <span data-ttu-id="d43e7-110">依照[這裡](service-fabric-cli.md)所述的步驟，安裝最新的 Service Fabric CLI。</span><span class="sxs-lookup"><span data-stu-id="d43e7-110">Install the latest Service Fabric CLI following the steps mentioned [here](service-fabric-cli.md).</span></span>

3. <span data-ttu-id="d43e7-111">若要建置和處理 Service Fabric Java 應用程式，您必須確定已安裝 JDK 1.8 和 Gradle。</span><span class="sxs-lookup"><span data-stu-id="d43e7-111">To build and work on the Service Fabric Java applications, you need to ensure that you have JDK 1.8 and Gradle installed.</span></span> <span data-ttu-id="d43e7-112">如果尚未安裝，您可以執行下列命令來安裝 JDK 1.8 (openjdk-8-jdk) 和 Gradle -</span><span class="sxs-lookup"><span data-stu-id="d43e7-112">If not yet installed, you can run the following to install JDK 1.8 (openjdk-8-jdk) and Gradle -</span></span>

 ```bash
 sudo apt-get install openjdk-8-jdk-headless
 sudo apt-get install gradle
 ```
4. <span data-ttu-id="d43e7-113">依照[這裡](service-fabric-application-lifecycle-sfctl.md)所述的步驟，更新您應用程式的安裝/解除安裝指令碼，以使用新的 Service Fabric CLI。</span><span class="sxs-lookup"><span data-stu-id="d43e7-113">Update the install/uninstall scripts of your application to use the new Service Fabric CLI following the steps mentioned [here](service-fabric-application-lifecycle-sfctl.md).</span></span> <span data-ttu-id="d43e7-114">您可以參考我們的快速入門[範例](https://github.com/Azure-Samples/service-fabric-java-getting-started)以供參考。</span><span class="sxs-lookup"><span data-stu-id="d43e7-114">You can refer to our getting-started [examples](https://github.com/Azure-Samples/service-fabric-java-getting-started) for reference.</span></span>

>[!TIP]
> <span data-ttu-id="d43e7-115">解除安裝 Service Fabric Java SDK 之後，Yeoman 將無法運作。</span><span class="sxs-lookup"><span data-stu-id="d43e7-115">After uninstalling the Service Fabric Java SDK, Yeoman will not work.</span></span> <span data-ttu-id="d43e7-116">依照[這裡](service-fabric-create-your-first-linux-application-with-java.md)所提及的必要條件，啟動並執行 Service Fabric Yeoman Java 範本產生器。</span><span class="sxs-lookup"><span data-stu-id="d43e7-116">Follow the Prerequisites mentioned [here](service-fabric-create-your-first-linux-application-with-java.md) to have Service Fabric Yeoman Java template generator up and working.</span></span>

## <a name="service-fabric-java-libraries-on-maven"></a><span data-ttu-id="d43e7-117">Maven 上的 Service Fabric Java 程式庫</span><span class="sxs-lookup"><span data-stu-id="d43e7-117">Service Fabric Java libraries on Maven</span></span>
<span data-ttu-id="d43e7-118">Service Fabric Java 程式庫已裝載於 Maven 中。</span><span class="sxs-lookup"><span data-stu-id="d43e7-118">Service Fabric Java libraries have been hosted in Maven.</span></span> <span data-ttu-id="d43e7-119">您可以在專案的 ``pom.xml`` 或 ``build.gradle`` 中新增相依性，以從 **mavenCentral** 使用 Service Fabric Java 程式庫。</span><span class="sxs-lookup"><span data-stu-id="d43e7-119">You can add the dependencies in the ``pom.xml`` or ``build.gradle`` of your projects to use Service Fabric Java libraries from **mavenCentral**.</span></span>

### <a name="actors"></a><span data-ttu-id="d43e7-120">動作項目</span><span class="sxs-lookup"><span data-stu-id="d43e7-120">Actors</span></span>

<span data-ttu-id="d43e7-121">您應用程式的 Service Fabric Reliable Actor 支援。</span><span class="sxs-lookup"><span data-stu-id="d43e7-121">Service Fabric Reliable Actor support for your application.</span></span>

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

### <a name="services"></a><span data-ttu-id="d43e7-122">服務</span><span class="sxs-lookup"><span data-stu-id="d43e7-122">Services</span></span>

<span data-ttu-id="d43e7-123">您應用程式的 Service Fabric 無狀態服務支援。</span><span class="sxs-lookup"><span data-stu-id="d43e7-123">Service Fabric Stateless Service support for your application.</span></span>

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

### <a name="others"></a><span data-ttu-id="d43e7-124">其他</span><span class="sxs-lookup"><span data-stu-id="d43e7-124">Others</span></span>
#### <a name="transport"></a><span data-ttu-id="d43e7-125">傳輸</span><span class="sxs-lookup"><span data-stu-id="d43e7-125">Transport</span></span>

<span data-ttu-id="d43e7-126">Service Fabric Java 應用程式的傳輸層支援。</span><span class="sxs-lookup"><span data-stu-id="d43e7-126">Transport layer support for Service Fabric Java application.</span></span> <span data-ttu-id="d43e7-127">除非您在傳輸層進行程式設計，否則不需要明確地將此相依性新增至 Reliable Actor 或服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="d43e7-127">You do not need to explicitly add this dependency to your Reliable Actor or Service applications, unless you program at the transport layer.</span></span>

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

#### <a name="fabric-support"></a><span data-ttu-id="d43e7-128">網狀架構支援</span><span class="sxs-lookup"><span data-stu-id="d43e7-128">Fabric support</span></span>

<span data-ttu-id="d43e7-129">Service Fabric 的系統層級支援，其可與原生 Service Fabric 執行階段交談。</span><span class="sxs-lookup"><span data-stu-id="d43e7-129">System level support for Service Fabric, which talks to native Service Fabric runtime.</span></span> <span data-ttu-id="d43e7-130">您不需要明確地將此相依性新增至 Reliable Actor 或服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="d43e7-130">You do not need to explicitly add this dependency to your Reliable Actor or Service applications.</span></span> <span data-ttu-id="d43e7-131">當您納入上述其他相依性時，可從 Maven 自動提取此相依性。</span><span class="sxs-lookup"><span data-stu-id="d43e7-131">This gets fetched automatically from Maven, when you include the other dependencies above.</span></span>

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


## <a name="migrating-service-fabric-stateless-service"></a><span data-ttu-id="d43e7-132">移轉 Service Fabric 無狀態服務</span><span class="sxs-lookup"><span data-stu-id="d43e7-132">Migrating Service Fabric Stateless Service</span></span>

<span data-ttu-id="d43e7-133">若要能夠使用從 Maven 提取的 Service Fabric 相依性，建立現有的 Service Fabric 無狀態 Java 服務，您需要更新服務內的 ``build.gradle`` 檔案。</span><span class="sxs-lookup"><span data-stu-id="d43e7-133">To be able to build your existing Service Fabric stateless Java service using Service Fabric dependencies fetched from Maven, you need to update the ``build.gradle`` file inside the Service.</span></span> <span data-ttu-id="d43e7-134">它先前通常如下所示 -</span><span class="sxs-lookup"><span data-stu-id="d43e7-134">Previously it used to be like as follows -</span></span>
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
<span data-ttu-id="d43e7-135">現在，若要從 Maven 提取相依性，**已更新**的 ``build.gradle`` 會有對應的組件，如下所示 -</span><span class="sxs-lookup"><span data-stu-id="d43e7-135">Now, to fetch the dependencies from Maven, the **updated** ``build.gradle`` would have the corresponding parts as follows -</span></span>
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
<span data-ttu-id="d43e7-136">一般而言，若要取得有關如何組建指令碼看起來像 Service Fabric 無狀態 Java 服務的整體概念，您可以參考我們的快速入門範例中的任何範例。</span><span class="sxs-lookup"><span data-stu-id="d43e7-136">In general, to get an overall idea about how the build script would look like for a Service Fabric stateless Java service, you can refer to any sample from our getting-started examples.</span></span> <span data-ttu-id="d43e7-137">以下是 EchoServer 範例的 [build.gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle)。</span><span class="sxs-lookup"><span data-stu-id="d43e7-137">Here is the [build.gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) for the EchoServer sample.</span></span>

## <a name="migrating-service-fabric-actor-service"></a><span data-ttu-id="d43e7-138">移轉 Service Fabric 動作項目服務</span><span class="sxs-lookup"><span data-stu-id="d43e7-138">Migrating Service Fabric Actor Service</span></span>

<span data-ttu-id="d43e7-139">若要能夠使用從 Maven 提取的 Service Fabric 相依性，建立現有的 Service Fabric 動作項目 Java 應用程式，您需要更新介面套件和服務套件內的 ``build.gradle`` 檔案。</span><span class="sxs-lookup"><span data-stu-id="d43e7-139">To be able to build your existing Service Fabric Actor Java application using Service Fabric dependencies fetched from Maven, you need to update the ``build.gradle`` file inside the interface package and in the Service package.</span></span> <span data-ttu-id="d43e7-140">如果您有 TestClient 套件，您需要一併更新。</span><span class="sxs-lookup"><span data-stu-id="d43e7-140">If you have a TestClient package, you need to update that as well.</span></span> <span data-ttu-id="d43e7-141">因此，針對您的動作項目 ``Myactor``，以下是您需要更新的位置 -</span><span class="sxs-lookup"><span data-stu-id="d43e7-141">So, for your actor ``Myactor``, the following would be the places where you need to update -</span></span>
```
./Myactor/build.gradle
./MyactorInterface/build.gradle
./MyactorTestClient/build.gradle
```

#### <a name="updating-build-script-for-the-interface-project"></a><span data-ttu-id="d43e7-142">更新介面專案的組建指令碼</span><span class="sxs-lookup"><span data-stu-id="d43e7-142">Updating build script for the interface project</span></span>

<span data-ttu-id="d43e7-143">它先前通常如下所示 -</span><span class="sxs-lookup"><span data-stu-id="d43e7-143">Previously it used to be like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
}
.
.
```
<span data-ttu-id="d43e7-144">現在，若要從 Maven 提取相依性，**已更新**的 ``build.gradle`` 會有對應的組件，如下所示 -</span><span class="sxs-lookup"><span data-stu-id="d43e7-144">Now, to fetch the dependencies from Maven, the **updated** ``build.gradle`` would have the corresponding parts as follows -</span></span>
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

#### <a name="updating-build-script-for-the-actor-project"></a><span data-ttu-id="d43e7-145">更新動作項目專案的組建指令碼</span><span class="sxs-lookup"><span data-stu-id="d43e7-145">Updating build script for the actor project</span></span>

<span data-ttu-id="d43e7-146">它先前通常如下所示 -</span><span class="sxs-lookup"><span data-stu-id="d43e7-146">Previously it used to be like as follows -</span></span>
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
<span data-ttu-id="d43e7-147">現在，若要從 Maven 提取相依性，**已更新**的 ``build.gradle`` 會有對應的組件，如下所示 -</span><span class="sxs-lookup"><span data-stu-id="d43e7-147">Now, to fetch the dependencies from Maven, the **updated** ``build.gradle`` would have the corresponding parts as follows -</span></span>
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

#### <a name="updating-build-script-for-the-test-client-project"></a><span data-ttu-id="d43e7-148">更新測試用戶端專案的組建指令碼</span><span class="sxs-lookup"><span data-stu-id="d43e7-148">Updating build script for the test client project</span></span>

<span data-ttu-id="d43e7-149">此處的變更類似於上一節所討論的變更，也就是動作項目專案。</span><span class="sxs-lookup"><span data-stu-id="d43e7-149">Changes here are similar to the changes discussed in previous section, that is, the actor project.</span></span> <span data-ttu-id="d43e7-150">Gradle 指令碼先前通常如下所示 -</span><span class="sxs-lookup"><span data-stu-id="d43e7-150">Previously the Gradle script used to be like as follows -</span></span>
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
<span data-ttu-id="d43e7-151">現在，若要從 Maven 提取相依性，**已更新**的 ``build.gradle`` 會有對應的組件，如下所示 -</span><span class="sxs-lookup"><span data-stu-id="d43e7-151">Now, to fetch the dependencies from Maven, the **updated** ``build.gradle`` would have the corresponding parts as follows -</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="d43e7-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d43e7-152">Next steps</span></span>

* [<span data-ttu-id="d43e7-153">使用 Yeoman 在 Linux 上建立和部署第一個 Service Fabric Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="d43e7-153">Create and deploy your first Service Fabric Java application on Linux by using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="d43e7-154">在 Linux 上使用適用於 Eclipse 的 Service Fabric 外掛程式建立和部署第一個 Service Fabric Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="d43e7-154">Create and deploy your first Service Fabric Java application on Linux by using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="d43e7-155">使用 Service Fabric CLI 與 Service Fabric 叢集互動</span><span class="sxs-lookup"><span data-stu-id="d43e7-155">Interact with Service Fabric clusters using the Service Fabric CLI</span></span>](service-fabric-cli.md)
