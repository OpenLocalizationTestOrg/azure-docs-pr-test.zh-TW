---
title: "從事件中樞與使用 Java 的 HDInsight 上的 Storm aaaProcess 事件 |Microsoft 文件"
description: "了解與 Maven tooprocess Java Storm 拓撲與事件中心資料的建立方式。"
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 453fa7b0-c8a6-413e-8747-3ac3b71bed86
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/13/2017
ms.author: larryfr
ms.openlocfilehash: 6506f5bc8f6ab0e29350c071a3f84433382038e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-java"></a><span data-ttu-id="08b80-103">使用 Storm on HDInsight 處理 Azure 事件中樞的事件 (Java)</span><span class="sxs-lookup"><span data-stu-id="08b80-103">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>

<span data-ttu-id="08b80-104">深入了解如何 toouse Storm HDInsight 上使用的 Azure 事件中心。</span><span class="sxs-lookup"><span data-stu-id="08b80-104">Learn how toouse Azure Event Hubs with Storm on HDInsight.</span></span> <span data-ttu-id="08b80-105">這個範例會使用在 Azure 事件中心 Java 為基礎的元件 tooread 及寫入資料。</span><span class="sxs-lookup"><span data-stu-id="08b80-105">This example uses Java-based components tooread and write data in Azure Event Hubs.</span></span>

<span data-ttu-id="08b80-106">Azure 事件中心可讓您 tooprocess 從網站、 應用程式和裝置的資料量很大。</span><span class="sxs-lookup"><span data-stu-id="08b80-106">Azure Event Hubs allows you tooprocess massive amounts of data from websites, apps, and devices.</span></span> <span data-ttu-id="08b80-107">hello spout 事件中心可讓您輕鬆 toouse Apache Storm HDInsight tooanalyze 上此即時資料。</span><span class="sxs-lookup"><span data-stu-id="08b80-107">hello Event Hub spout makes it easy toouse Apache Storm on HDInsight tooanalyze this data in real time.</span></span> <span data-ttu-id="08b80-108">您也可以撰寫從出現的資料 tooEvent 集線器使用事件中心閃電的 hello。</span><span class="sxs-lookup"><span data-stu-id="08b80-108">You can also write data tooEvent Hubs from Storm by using hello Event Hubs bolt.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08b80-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="08b80-109">Prerequisites</span></span>

* <span data-ttu-id="08b80-110">Apache Storm on HDInsight 叢集 3.6 版。</span><span class="sxs-lookup"><span data-stu-id="08b80-110">An Apache Storm on HDInsight cluster version 3.6.</span></span> <span data-ttu-id="08b80-111">如需詳細資訊，請參閱[開始使用 Storm on HDInsight cluster](hdinsight-apache-storm-tutorial-get-started-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="08b80-111">For more information, see [Get started with Storm on HDInsight cluster](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="08b80-112">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="08b80-112">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="08b80-113">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="08b80-113">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="08b80-114">[Azure 事件中樞](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)。</span><span class="sxs-lookup"><span data-stu-id="08b80-114">An [Azure Event Hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="08b80-115">[Oracle Java Developer Kit (JDK) 第 8 版](http://www.oracle.com/technetwork/java/javase/downloads/index.html)或同等版本，例如 [OpenJDK](http://openjdk.java.net/)。</span><span class="sxs-lookup"><span data-stu-id="08b80-115">[Oracle Java Developer Kit (JDK) version 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or equivalent, such as [OpenJDK](http://openjdk.java.net/).</span></span>

* <span data-ttu-id="08b80-116">[Maven](https://maven.apache.org/download.cgi)：Maven 是 Java 專案的專案建置系統。</span><span class="sxs-lookup"><span data-stu-id="08b80-116">[Maven](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="08b80-117">文字編輯器或整合開發環境 (IDE)。</span><span class="sxs-lookup"><span data-stu-id="08b80-117">A text editor or integrated development environment (IDE).</span></span>

    > [!NOTE]
    > <span data-ttu-id="08b80-118">您的編輯器或 IDE 可能具有處理 Maven 的特定功能，但未記載在這份文件中。</span><span class="sxs-lookup"><span data-stu-id="08b80-118">Your editor or IDE may have specific functionality for working with Maven that is not addressed in this document.</span></span> <span data-ttu-id="08b80-119">編輯環境的 hello 功能的相關資訊，請參閱您使用的 hello 產品的 hello 說明文件。</span><span class="sxs-lookup"><span data-stu-id="08b80-119">For information about hello capabilities of your editing environment, see hello documentation for hello product you are using.</span></span>

    * <span data-ttu-id="08b80-120">SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="08b80-120">An SSH client.</span></span> <span data-ttu-id="08b80-121">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="08b80-121">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="08b80-122">hello`ssh`和`scp`命令。</span><span class="sxs-lookup"><span data-stu-id="08b80-122">hello `ssh` and `scp` commands.</span></span> <span data-ttu-id="08b80-123">這些是使用的 toocopy 檔案 toohello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="08b80-123">These are used toocopy files toohello HDInsight cluster.</span></span> <span data-ttu-id="08b80-124">在 Windows 上，您可以透過 Windows 10 的 Bash 執行這些命令。</span><span class="sxs-lookup"><span data-stu-id="08b80-124">On Windows, you can get these through Bash on Windows 10.</span></span>

## <a name="understanding-hello-example"></a><span data-ttu-id="08b80-125">了解 hello 範例</span><span class="sxs-lookup"><span data-stu-id="08b80-125">Understanding hello example</span></span>

<span data-ttu-id="08b80-126">hello [hdinsight java storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub)範例包含兩種拓撲：</span><span class="sxs-lookup"><span data-stu-id="08b80-126">hello [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) example contains two topologies:</span></span>

<span data-ttu-id="08b80-127">hello`resources/writer.yaml`拓撲寫入隨機資料 tooan Azure 事件中心。</span><span class="sxs-lookup"><span data-stu-id="08b80-127">hello `resources/writer.yaml` topology writes random data tooan Azure Event Hub.</span></span> <span data-ttu-id="08b80-128">會產生 hello hello 資料`DeviceSpout`元件，且為隨機的裝置識別碼，裝置的值。</span><span class="sxs-lookup"><span data-stu-id="08b80-128">hello data is generated by hello `DeviceSpout` component, and is a random device ID and device value.</span></span> <span data-ttu-id="08b80-129">所以它是模擬會發出字串識別碼和數值的部分硬體。</span><span class="sxs-lookup"><span data-stu-id="08b80-129">So it's simulating some hardware that emits a string ID and a numeric value.</span></span>

<span data-ttu-id="08b80-130">關於`resources/reader.yaml`拓撲讀取自事件中心 （由 EventHubWriter，寫入 hello 資料） 的資料剖析 hello JSON 資料，並再記錄 hello`deviceId`和`deviceValue`資料。</span><span class="sxs-lookup"><span data-stu-id="08b80-130">Thee `resources/reader.yaml` topology reads data from Event Hub (hello data written by EventHubWriter,) parses hello JSON data, and then logs hello `deviceId` and `deviceValue` data.</span></span>

<span data-ttu-id="08b80-131">hello 資料會格式化為 JSON 文件它是撰寫 tooEvent 中樞，並由 hello 讀取器讀取時才能進行剖析從 JSON 移至 tuple。</span><span class="sxs-lookup"><span data-stu-id="08b80-131">hello data is formatted as a JSON document before it is written tooEvent Hub, and when read by hello reader it is parsed out of JSON and into tuples.</span></span> <span data-ttu-id="08b80-132">hello JSON 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="08b80-132">hello JSON format is as follows:</span></span>

    { "deviceId": "unique identifier", "deviceValue": some value }

### <a name="project-configuration"></a><span data-ttu-id="08b80-133">專案組態</span><span class="sxs-lookup"><span data-stu-id="08b80-133">Project configuration</span></span>

<span data-ttu-id="08b80-134">hello`POM.xml`檔案包含這個 Maven 專案的組態資訊。</span><span class="sxs-lookup"><span data-stu-id="08b80-134">hello `POM.xml` file contains configuration information for this Maven project.</span></span> <span data-ttu-id="08b80-135">hello 興趣︰</span><span class="sxs-lookup"><span data-stu-id="08b80-135">hello interesting pieces are:</span></span>

#### <a name="event-hub-components"></a><span data-ttu-id="08b80-136">事件中樞元件</span><span class="sxs-lookup"><span data-stu-id="08b80-136">Event Hub components</span></span>

<span data-ttu-id="08b80-137">可讀取和寫入 tooAzure 事件中心 hello 元件位於 hello [HDInsight 儲存機制](https://github.com/hdinsight/mvn-rep)。</span><span class="sxs-lookup"><span data-stu-id="08b80-137">hello component that reads and writes tooAzure Event Hubs is located in hello [HDInsight repository](https://github.com/hdinsight/mvn-rep).</span></span> <span data-ttu-id="08b80-138">下列各節 hello hello`POM.xml`這個儲存機制從檔案載入 hello 元件</span><span class="sxs-lookup"><span data-stu-id="08b80-138">hello following sections in hello `POM.xml` file load hello components from this repository</span></span>

```xml
<repositories>
    <repository>
        <id>hdinsight-examples</id>
        <url>http://raw.github.com/hdinsight/mvn-repo/master</url>
    </repository>
</repositories>
```

#### <a name="hello-eventhubs-storm-spout-dependency"></a><span data-ttu-id="08b80-139">hello EventHubs Storm Spout 相依性</span><span class="sxs-lookup"><span data-stu-id="08b80-139">hello EventHubs Storm Spout dependency</span></span>

```xml
<dependency>
    <groupId>com.microsoft</groupId>
    <artifactId>eventhubs</artifactId>
    <version>${storm.eventhub.version}</version>
</dependency>
```

<span data-ttu-id="08b80-140">這段 xml 會定義包含 spout 從事件中樞進行讀取和寫入 tooit 閃電 hello eventhubs 封裝的相依性。</span><span class="sxs-lookup"><span data-stu-id="08b80-140">This xml defines a dependency for hello eventhubs package, which contains both a spout for reading from Event Hubs, and a bolt for writing tooit.</span></span>

```xml
</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

<span data-ttu-id="08b80-141">這段 xml 會設定 hello 專案 toogenerate 輸出 for Java 8 中，會使用 HDInsight 3.5 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="08b80-141">This xml configures hello project toogenerate output for Java 8, which is used by HDInsight 3.5 or higher.</span></span>

#### <a name="hello-maven-shade-plugin"></a><span data-ttu-id="08b80-142">hello maven 陰影外掛程式</span><span class="sxs-lookup"><span data-stu-id="08b80-142">hello maven-shade-plugin</span></span>

```xml
<!-- build an uber jar -->
<plugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-shade-plugin</artifactId>
<version>2.3</version>
<configuration>
    <transformers>
    <!-- Keep us from getting a can't overwrite file error -->
    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer"/>
    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer"/>
    </transformers>
    <!-- Keep us from getting a bad signature error -->
    <filters>
    <filter>
        <artifact>*:*</artifact>
        <excludes>
            <exclude>META-INF/*.SF</exclude>
            <exclude>META-INF/*.DSA</exclude>
            <exclude>META-INF/*.RSA</exclude>
        </excludes>
    </filter>
    </filters>
</configuration>
<executions>
    <execution>
    <phase>package</phase>
    <goals>
        <goal>shade</goal>
    </goals>
    </execution>
</executions>
</plugin>
```

<span data-ttu-id="08b80-143">這段 xml 會設定成超級 jar hello 方案 toopackage hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="08b80-143">This xml configures hello solution toopackage hello output into an uber jar.</span></span> <span data-ttu-id="08b80-144">hello jar 包含 hello 專案程式碼和必要的相依性。</span><span class="sxs-lookup"><span data-stu-id="08b80-144">hello jar contains both hello project code and required dependencies.</span></span> <span data-ttu-id="08b80-145">它也用來：</span><span class="sxs-lookup"><span data-stu-id="08b80-145">It is also used to:</span></span>

* <span data-ttu-id="08b80-146">重新命名 hello 相依性的授權檔案。</span><span class="sxs-lookup"><span data-stu-id="08b80-146">Rename license files for hello dependencies.</span></span>
* <span data-ttu-id="08b80-147">排除安全性/簽章。</span><span class="sxs-lookup"><span data-stu-id="08b80-147">Exclude security/signatures.</span></span>
* <span data-ttu-id="08b80-148">請確定多個實作 hello 相同介面會合併成一個項目。</span><span class="sxs-lookup"><span data-stu-id="08b80-148">Ensure that multiple implementations of hello same interface are merged into one entry.</span></span>

<span data-ttu-id="08b80-149">這些組態設定可防止執行階段錯誤。</span><span class="sxs-lookup"><span data-stu-id="08b80-149">These configuration settings prevent errors at runtime.</span></span>

#### <a name="topology-definitions"></a><span data-ttu-id="08b80-150">拓撲定義</span><span class="sxs-lookup"><span data-stu-id="08b80-150">Topology definitions</span></span>

<span data-ttu-id="08b80-151">這個範例會使用 hello[變動](https://storm.apache.org/releases/1.1.0/flux.html)架構。</span><span class="sxs-lookup"><span data-stu-id="08b80-151">This example uses hello [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework.</span></span> <span data-ttu-id="08b80-152">此架構會使用 YAML toodefine hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="08b80-152">This framework uses YAML toodefine hello topologies.</span></span> <span data-ttu-id="08b80-153">hello 主要優點是您不是硬式編碼在 Java 程式碼中的 hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="08b80-153">hello primary benefit is that you aren't hard coding hello topology in Java code.</span></span> <span data-ttu-id="08b80-154">由於 hello 定義 YAML，您可以變更它提交 hello 拓撲，而不需要 toorecompile 的所有項目之前。</span><span class="sxs-lookup"><span data-stu-id="08b80-154">Since hello definition is YAML, you can change it before submitting hello topology, without having toorecompile everything.</span></span>

<span data-ttu-id="08b80-155">__writer.yaml__：</span><span class="sxs-lookup"><span data-stu-id="08b80-155">__writer.yaml__:</span></span>

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubwriter"

components:
  # Configure hello Event Hub spout
  - id: "eventhubbolt-config"
    className: "org.apache.storm.eventhubs.bolt.EventHubBoltConfig"
    constructorArgs:
      # These are populated from hello .properties file when hello topology is started
      - "${eventhub.write.policy.name}"
      - "${eventhub.write.policy.key}"
      - "${eventhub.namespace}"
      - "servicebus.windows.net"
      - "${eventhub.name}"

spouts:
  - id: "device-emulator-spout"
    className: "com.microsoft.example.DeviceSpout"
    parallelism: ${eventhub.partitions}

bolts:
  - id: "eventhub-bolt"
    className: "org.apache.storm.eventhubs.bolt.EventHubBolt"
    constructorArgs:
      - ref: "eventhubbolt-config" # config declared in components section
    # parallelism hint. This should be hello same as hello number of partitions for your Event Hub, so we read it from hello dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

# How data flows through hello components
streams:
  - name: "spout -> eventhub" # just a string used for logging
    from: "device-emulator-spout"
    to: "eventhub-bolt"
    grouping:
        type: SHUFFLE

  - name: "spout -> logger"
    from: "device-emulator-spout"
    to: "log-bolt"
    grouping:
        type: SHUFFLE
```

<span data-ttu-id="08b80-156">__reader.yaml__：</span><span class="sxs-lookup"><span data-stu-id="08b80-156">__reader.yaml__:</span></span>

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubreader"

components:
  # Configure hello Event Hub spout
  - id: "eventhubspout-config"
    className: "org.apache.storm.eventhubs.spout.EventHubSpoutConfig"
    constructorArgs:
      # These are populated from hello .properties file when hello topology is started
      - "${eventhub.read.policy.name}"
      - "${eventhub.read.policy.key}"
      - "${eventhub.namespace}"
      - "${eventhub.name}"
      - ${eventhub.partitions}

spouts:
  - id: "eventhub-spout"
    className: "org.apache.storm.eventhubs.spout.EventHubSpout"
    constructorArgs:
      - ref: "eventhubspout-config" # config declared in components section
    # parallelism hint. This should be hello same as hello number of partitions for your Event Hub, so we read it from hello dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

bolts:
  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

  # Parses from JSON into tuples
  - id: "parser-bolt"
    className: "com.microsoft.example.ParserBolt"
    parallelism: ${eventhub.partitions}

# How data flows through hello components
streams:
  - name: "spout -> parser" # just a string used for logging
    from: "eventhub-spout"
    to: "parser-bolt"
    grouping:
        type: SHUFFLE

  - name: "parser -> log-bolt"
    from: "parser-bolt"
    to: "log-bolt"
    grouping:
        type: SHUFFLE
```

#### <a name="tell-hello-topology-about-event-hub"></a><span data-ttu-id="08b80-157">事件中樞的相關分辨 hello 拓樸</span><span class="sxs-lookup"><span data-stu-id="08b80-157">Tell hello topology about Event Hub</span></span>

<span data-ttu-id="08b80-158">在執行階段，hello`dev.properties`檔案是使用的 toopass hello 事件中樞設定 toohello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="08b80-158">At run time, hello `dev.properties` file is used toopass hello Event Hub configuration toohello topology.</span></span> <span data-ttu-id="08b80-159">hello 下列範例是 hello 檔案 hello 預設內容：</span><span class="sxs-lookup"><span data-stu-id="08b80-159">hello following example is hello default contents of hello file:</span></span>

```yaml
eventhub.write.policy.name: writer
eventhub.write.policy.key: your_key_here
eventhub.read.policy.name: reader
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: storm
eventhub.partitions: 2
```

## <a name="configure-environment-variables"></a><span data-ttu-id="08b80-160">設定環境變數</span><span class="sxs-lookup"><span data-stu-id="08b80-160">Configure environment variables</span></span>

<span data-ttu-id="08b80-161">hello 下列環境變數設定當您在開發工作站上安裝 Java 和 hello JDK。</span><span class="sxs-lookup"><span data-stu-id="08b80-161">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="08b80-162">不過，您應該檢查其存在且包含您系統的 hello 正確值。</span><span class="sxs-lookup"><span data-stu-id="08b80-162">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="08b80-163">**JAVA_HOME** -應該指向 toohello hello Java runtime environment (JRE) 安裝所在的目錄。</span><span class="sxs-lookup"><span data-stu-id="08b80-163">**JAVA_HOME** - should point toohello directory where hello Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="08b80-164">例如，在 Unix 或 Linux 的分佈，它應該有一個值類似太`/usr/lib/jvm/java-7-oracle`。</span><span class="sxs-lookup"><span data-stu-id="08b80-164">For example, in a Unix or Linux distribution, it should have a value similar too`/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="08b80-165">在 Windows 中，就會類似的值太`c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="08b80-165">In Windows, it would have a value similar too`c:\Program Files (x86)\Java\jre1.7`</span></span>
* <span data-ttu-id="08b80-166">**路徑**-應該包含下列路徑的 hello:</span><span class="sxs-lookup"><span data-stu-id="08b80-166">**PATH** - should contain hello following paths:</span></span>

  * <span data-ttu-id="08b80-167">**JAVA_HOME** （或 hello 相等路徑）</span><span class="sxs-lookup"><span data-stu-id="08b80-167">**JAVA_HOME** (or hello equivalent path)</span></span>
  * <span data-ttu-id="08b80-168">**JAVA_HOME\bin** （或 hello 相等路徑）</span><span class="sxs-lookup"><span data-stu-id="08b80-168">**JAVA_HOME\bin** (or hello equivalent path)</span></span>
  * <span data-ttu-id="08b80-169">hello Maven 安裝所在的目錄</span><span class="sxs-lookup"><span data-stu-id="08b80-169">hello directory where Maven is installed</span></span>

## <a name="configure-event-hub"></a><span data-ttu-id="08b80-170">設定事件中樞</span><span class="sxs-lookup"><span data-stu-id="08b80-170">Configure Event Hub</span></span>

<span data-ttu-id="08b80-171">事件中心是此範例中的 hello 資料來源。</span><span class="sxs-lookup"><span data-stu-id="08b80-171">Event Hubs is hello data source for this example.</span></span> <span data-ttu-id="08b80-172">使用下列步驟 toocreate 事件中心的 hello。</span><span class="sxs-lookup"><span data-stu-id="08b80-172">Use hello following steps toocreate a Event Hub.</span></span>

1. <span data-ttu-id="08b80-173">從 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，選取**新增** > **Service Bus** > **事件中心** > **自訂建立**。</span><span class="sxs-lookup"><span data-stu-id="08b80-173">From hello [Azure Classic Portal](https://manage.windowsazure.com), select **NEW** > **Service Bus** > **Event Hub** > **Custom Create**.</span></span>

2. <span data-ttu-id="08b80-174">在 hello**新增新的事件中樞**畫面上，輸入**事件中樞名稱**。</span><span class="sxs-lookup"><span data-stu-id="08b80-174">On hello **Add a new Event Hub** screen, enter an **Event Hub Name**.</span></span> <span data-ttu-id="08b80-175">選取 hello**區域**toocreate hello 中樞中，然後再建立命名空間或選取現有的我的最愛。</span><span class="sxs-lookup"><span data-stu-id="08b80-175">Select hello **Region** toocreate hello hub in, and then create a namespace or select an existing one.</span></span> <span data-ttu-id="08b80-176">最後，按一下 hello**箭號**toocontinue。</span><span class="sxs-lookup"><span data-stu-id="08b80-176">Finally, click hello **Arrow** toocontinue.</span></span>

    ![精靈頁面 1](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz1.png)

   > [!NOTE]
   > <span data-ttu-id="08b80-178">選取 hello 相同**位置**為您 Storm HDInsight 伺服器 tooreduce 延遲和成本。</span><span class="sxs-lookup"><span data-stu-id="08b80-178">Select hello same **Location** as your Storm on HDInsight server tooreduce latency and costs.</span></span>

3. <span data-ttu-id="08b80-179">在 hello**設定事件中樞**畫面上，輸入 hello**分割計數**和**訊息保留**值。</span><span class="sxs-lookup"><span data-stu-id="08b80-179">On hello **Configure Event Hub** screen, enter hello **Partition count** and **Message Retention** values.</span></span> <span data-ttu-id="08b80-180">在此範例中，資料分割計數使用 10，訊息保留使用 1。</span><span class="sxs-lookup"><span data-stu-id="08b80-180">For this example, use a partition count of 10 and a message retention of 1.</span></span> <span data-ttu-id="08b80-181">請注意 hello 資料分割計數，因為您稍後需要這個值。</span><span class="sxs-lookup"><span data-stu-id="08b80-181">Note hello partition count because you need this value later.</span></span>

    ![精靈頁面 2](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz2.png)

4. <span data-ttu-id="08b80-183">Hello 事件中心已建立，請選取 hello 命名空間之後，請選取**事件中心**，然後選取您稍早建立的 hello 事件中心。</span><span class="sxs-lookup"><span data-stu-id="08b80-183">After hello event hub has been created, select hello namespace, select **Event Hubs**, and then select hello event hub that you created earlier.</span></span>
5. <span data-ttu-id="08b80-184">選取**設定**，然後使用下列資訊的 hello 建立兩個新的存取原則：</span><span class="sxs-lookup"><span data-stu-id="08b80-184">Select **Configure**, then create two new access policies by using hello following information:</span></span>

    <table>
    <tr><th><span data-ttu-id="08b80-185">名稱</span><span class="sxs-lookup"><span data-stu-id="08b80-185">Name</span></span></th><th><span data-ttu-id="08b80-186">權限</span><span class="sxs-lookup"><span data-stu-id="08b80-186">Permissions</span></span></th></tr>
    <tr><td><span data-ttu-id="08b80-187">寫入器</span><span class="sxs-lookup"><span data-stu-id="08b80-187">Writer</span></span></td><td><span data-ttu-id="08b80-188">傳送</span><span class="sxs-lookup"><span data-stu-id="08b80-188">Send</span></span></td></tr>
    <tr><td><span data-ttu-id="08b80-189">讀取者</span><span class="sxs-lookup"><span data-stu-id="08b80-189">Reader</span></span></td><td><span data-ttu-id="08b80-190">接聽</span><span class="sxs-lookup"><span data-stu-id="08b80-190">Listen</span></span></td></tr>
    </table>

    <span data-ttu-id="08b80-191">建立 hello 權限之後，請選取 hello**儲存**在 hello hello 頁面底部的圖示。</span><span class="sxs-lookup"><span data-stu-id="08b80-191">After You create hello permissions, select hello **Save** icon at hello bottom of hello page.</span></span> <span data-ttu-id="08b80-192">這些共用的存取原則使用的 tooread 並寫入 tooEvent 中樞。</span><span class="sxs-lookup"><span data-stu-id="08b80-192">These shared access policies are used tooread and write tooEvent Hub.</span></span>

    ![原則](./media/hdinsight-storm-develop-csharp-event-hub-topology/policy.png)

6. <span data-ttu-id="08b80-194">儲存 hello 原則之後，使用 hello**共用存取金鑰產生器**底部 hello hello 頁面 tooretrieve hello 金鑰 hello**寫入器**和**讀取器**原則。</span><span class="sxs-lookup"><span data-stu-id="08b80-194">After you save hello policies, use hello **Shared access key generator** at hello bottom of hello page tooretrieve hello key for hello **writer** and **reader** policies.</span></span> <span data-ttu-id="08b80-195">儲存這些金鑰。</span><span class="sxs-lookup"><span data-stu-id="08b80-195">Save these keys.</span></span>

## <a name="download-and-build-hello-project"></a><span data-ttu-id="08b80-196">下載並建置 hello 專案</span><span class="sxs-lookup"><span data-stu-id="08b80-196">Download and build hello project</span></span>

1. <span data-ttu-id="08b80-197">從 GitHub 下載 hello 專案： [hdinsight java storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub)。</span><span class="sxs-lookup"><span data-stu-id="08b80-197">Download hello project from GitHub: [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span></span> <span data-ttu-id="08b80-198">您可以下載為 zip 封存，hello 封裝，或使用[git](https://git-scm.com/) tooclone hello 專案在本機。</span><span class="sxs-lookup"><span data-stu-id="08b80-198">You can either download hello package as a zip archive, or use [git](https://git-scm.com/) tooclone hello project locally.</span></span>

2. <span data-ttu-id="08b80-199">修改 hello`dev.properties`包含事件中心的 hello 組態檔。</span><span class="sxs-lookup"><span data-stu-id="08b80-199">Modify hello `dev.properties` file with hello configuration for your Event Hub.</span></span>

3. <span data-ttu-id="08b80-200">使用下列 toobuild 和套件 hello 專案 hello:</span><span class="sxs-lookup"><span data-stu-id="08b80-200">Use hello following toobuild and package hello project:</span></span>

        mvn package

    <span data-ttu-id="08b80-201">這個命令會下載必要的相依性，建置並封裝然後 hello 專案。</span><span class="sxs-lookup"><span data-stu-id="08b80-201">This command downloads required dependencies, builds, and then packages hello project.</span></span> <span data-ttu-id="08b80-202">hello 輸出會儲存在 hello **/目標**目錄做為**EventHubExample-1.0-SNAPSHOT.jar**。</span><span class="sxs-lookup"><span data-stu-id="08b80-202">hello output is stored in hello **/target** directory as **EventHubExample-1.0-SNAPSHOT.jar**.</span></span>

## <a name="test-locally"></a><span data-ttu-id="08b80-203">本機測試</span><span class="sxs-lookup"><span data-stu-id="08b80-203">Test locally</span></span>

<span data-ttu-id="08b80-204">因為這些拓撲只讀取和寫入 tooEvent 中樞，您可以測試它們，如果您有[Storm 開發環境](http://storm.apache.org/releases/current/Setting-up-development-environment.html)。</span><span class="sxs-lookup"><span data-stu-id="08b80-204">Since these topologies just read and write tooEvent Hubs, you can test them locally if you have a [Storm development environment](http://storm.apache.org/releases/current/Setting-up-development-environment.html).</span></span> <span data-ttu-id="08b80-205">使用下列步驟 toorun hello 開發環境中的本機 hello:</span><span class="sxs-lookup"><span data-stu-id="08b80-205">Use hello following steps toorun locally in hello dev environment:</span></span>

1. <span data-ttu-id="08b80-206">執行 hello 寫入器：</span><span class="sxs-lookup"><span data-stu-id="08b80-206">Run hello writer:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /writer.yaml --filter dev.properties

2. <span data-ttu-id="08b80-207">執行 hello 讀取器：</span><span class="sxs-lookup"><span data-stu-id="08b80-207">Run hello reader:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /reader.yaml --filter dev.properties

> [!TIP]
> * <span data-ttu-id="08b80-208">`--local`: Hello 拓撲中執行本機模式 （非分散式）。</span><span class="sxs-lookup"><span data-stu-id="08b80-208">`--local`: Run hello topology in local mode (non-distributed).</span></span>
> * <span data-ttu-id="08b80-209">`-R /writer.yaml`： 從 hello 載入 hello 拓撲定義`resources`封裝在 hello jar。</span><span class="sxs-lookup"><span data-stu-id="08b80-209">`-R /writer.yaml`: Load hello topology definition from hello `resources` packaged in hello jar.</span></span> <span data-ttu-id="08b80-210">如果 hello 拓撲 hello 本機檔案系統上的檔案，請改為 hello 最後一個參數為指定 hello 路徑 tooit。</span><span class="sxs-lookup"><span data-stu-id="08b80-210">If hello topology is a file on hello local file system, specify hello path tooit as hello last parameter instead.</span></span>
> * <span data-ttu-id="08b80-211">`--filter dev.properties`： 使用 hello 內容`dev.properties`toofill hello hello 拓撲定義中的值。</span><span class="sxs-lookup"><span data-stu-id="08b80-211">`--filter dev.properties`: Use hello contents of `dev.properties` toofill in hello values in hello topology definitions.</span></span> <span data-ttu-id="08b80-212">例如： `${eventhub.read.policy.name}`。</span><span class="sxs-lookup"><span data-stu-id="08b80-212">For example, `${eventhub.read.policy.name}`.</span></span>

<span data-ttu-id="08b80-213">在本機執行時，輸出會是記錄的 toohello 主控台。</span><span class="sxs-lookup"><span data-stu-id="08b80-213">Output is logged toohello console when running locally.</span></span> <span data-ttu-id="08b80-214">使用__Ctrl + C__ toostop hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="08b80-214">Use __Ctrl+C__ toostop hello topology.</span></span>

## <a name="deploy-hello-topologies"></a><span data-ttu-id="08b80-215">部署 hello 拓撲</span><span class="sxs-lookup"><span data-stu-id="08b80-215">Deploy hello topologies</span></span>

1. <span data-ttu-id="08b80-216">使用 SCP toocopy hello jar 封裝 tooyour HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="08b80-216">Use SCP toocopy hello jar package tooyour HDInsight cluster.</span></span> <span data-ttu-id="08b80-217">取代為您的叢集 hello SSH 使用者使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="08b80-217">Replace USERNAME with hello SSH user for your cluster.</span></span> <span data-ttu-id="08b80-218">以您的 HDInsight 叢集 hello 名稱取代 CLUSTERNAME:</span><span class="sxs-lookup"><span data-stu-id="08b80-218">Replace CLUSTERNAME with hello name of your HDInsight cluster:</span></span>

        scp ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.

    <span data-ttu-id="08b80-219">如果您使用 SSH 帳戶密碼，則提示的 tooenter hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="08b80-219">If you used a password for your SSH account, you are prompted tooenter hello password.</span></span> <span data-ttu-id="08b80-220">如果您使用 SSH 金鑰與 hello 帳戶時，您可能需要 toouse hello`-i`參數 toospecify hello 路徑 toohello 金鑰檔。</span><span class="sxs-lookup"><span data-stu-id="08b80-220">If you used an SSH key with hello account, you may need toouse hello `-i` parameter toospecify hello path toohello key file.</span></span> <span data-ttu-id="08b80-221">例如， `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span><span class="sxs-lookup"><span data-stu-id="08b80-221">For example, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span></span>

    <span data-ttu-id="08b80-222">此命令會將複製 SSH 使用者 hello 叢集上的 hello 檔案 toohello 主的目錄。</span><span class="sxs-lookup"><span data-stu-id="08b80-222">This command copies hello file toohello home directory of your SSH user on hello cluster.</span></span>

2. <span data-ttu-id="08b80-223">Hello 檔案已完成上傳，一旦使用 SSH tooconnect toohello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="08b80-223">Once hello file has finished uploading, use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="08b80-224">取代**USERNAME** hello SSH 登入名稱。</span><span class="sxs-lookup"><span data-stu-id="08b80-224">Replace **USERNAME** hello name of your SSH login.</span></span> <span data-ttu-id="08b80-225">將 **CLUSTERNAME** 取代為 HDInsight 叢集名稱：</span><span class="sxs-lookup"><span data-stu-id="08b80-225">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    > [!NOTE]
    > <span data-ttu-id="08b80-226">如果您使用 SSH 帳戶密碼，則提示的 tooenter hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="08b80-226">If you used a password for your SSH account, you are prompted tooenter hello password.</span></span> <span data-ttu-id="08b80-227">如果您使用 SSH 金鑰與 hello 帳戶時，您可能需要 toouse hello`-i`參數 toospecify hello 路徑 toohello 金鑰檔。</span><span class="sxs-lookup"><span data-stu-id="08b80-227">If you used an SSH key with hello account, you may need toouse hello `-i` parameter toospecify hello path toohello key file.</span></span> <span data-ttu-id="08b80-228">hello 下列範例會載入 hello 私密金鑰`~/.ssh/id_rsa`:</span><span class="sxs-lookup"><span data-stu-id="08b80-228">hello following example loads hello private key from `~/.ssh/id_rsa`:</span></span>
    >
    > `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`

3. <span data-ttu-id="08b80-229">使用下列命令 toostart hello 拓撲 hello:</span><span class="sxs-lookup"><span data-stu-id="08b80-229">Use hello following command toostart hello topologies:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties

    > [!TIP]
    > * <span data-ttu-id="08b80-230">`--remote`： 送出 hello 拓撲 toohello Nimbus 服務，就會開始在 hello hello 叢集中的背景工作節點上。</span><span class="sxs-lookup"><span data-stu-id="08b80-230">`--remote`: Submits hello topology toohello Nimbus service, which starts it on hello worker nodes in hello cluster.</span></span>

4. <span data-ttu-id="08b80-231">tooview hello 記錄資料，請移 toohttps://CLUSTERNAME.azurehdinsight.net/stormui，其中__CLUSTERNAME__ hello 您的 HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="08b80-231">tooview hello logged data, go toohttps://CLUSTERNAME.azurehdinsight.net/stormui, where __CLUSTERNAME__ is hello name of your HDInsight cluster.</span></span> <span data-ttu-id="08b80-232">選取 hello 拓樸，然後向下切入 toohello 元件。</span><span class="sxs-lookup"><span data-stu-id="08b80-232">Select hello topologies and drill down toohello components.</span></span> <span data-ttu-id="08b80-233">選取 hello__連接埠__元件 tooview 的執行個體的項目會記錄資訊。</span><span class="sxs-lookup"><span data-stu-id="08b80-233">Select hello __port__ entry for an instance of a component tooview logged information.</span></span>

5. <span data-ttu-id="08b80-234">使用下列命令 toostop hello 拓撲 hello:</span><span class="sxs-lookup"><span data-stu-id="08b80-234">Use hello following commands toostop hello topologies:</span></span>

        storm kill reader
        storm kill writer

## <a name="delete-your-cluster"></a><span data-ttu-id="08b80-235">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="08b80-235">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="08b80-236">後續步驟</span><span class="sxs-lookup"><span data-stu-id="08b80-236">Next steps</span></span>

* [<span data-ttu-id="08b80-237">Storm on HDInsight 的範例拓撲</span><span class="sxs-lookup"><span data-stu-id="08b80-237">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
