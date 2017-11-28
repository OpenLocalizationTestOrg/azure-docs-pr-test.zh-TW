---
title: "使用 Java 在事件中樞內透過 Storm on HDInsight 處理事件 | Microsoft Docs"
description: "了解如何使用 Maven 建立的 Java Storm 拓撲處理事件中樞資料。"
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
ms.openlocfilehash: 2e8ebbdab2be7bed224a67facec798820615bb22
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-java"></a><span data-ttu-id="3bb15-103">使用 Storm on HDInsight 處理 Azure 事件中樞的事件 (Java)</span><span class="sxs-lookup"><span data-stu-id="3bb15-103">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>

<span data-ttu-id="3bb15-104">了解如何透過 Storm on HDInsight 使用 Azure 事件中樞。</span><span class="sxs-lookup"><span data-stu-id="3bb15-104">Learn how to use Azure Event Hubs with Storm on HDInsight.</span></span> <span data-ttu-id="3bb15-105">此範例使用 Java 架構的元件，在 Azure 事件中樞讀取和寫入資料。</span><span class="sxs-lookup"><span data-stu-id="3bb15-105">This example uses Java-based components to read and write data in Azure Event Hubs.</span></span>

<span data-ttu-id="3bb15-106">Azure 事件中樞可讓您從網站、應用程式和裝置處理巨量資料。</span><span class="sxs-lookup"><span data-stu-id="3bb15-106">Azure Event Hubs allows you to process massive amounts of data from websites, apps, and devices.</span></span> <span data-ttu-id="3bb15-107">事件中樞 Spout 可讓您輕鬆地使用 Apache Storm on HDInsight 進行即時分析資料。</span><span class="sxs-lookup"><span data-stu-id="3bb15-107">The Event Hub spout makes it easy to use Apache Storm on HDInsight to analyze this data in real time.</span></span> <span data-ttu-id="3bb15-108">您也可以使用事件中樞 Bolt 將資料從 Storm 寫入事件中樞。</span><span class="sxs-lookup"><span data-stu-id="3bb15-108">You can also write data to Event Hubs from Storm by using the Event Hubs bolt.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3bb15-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="3bb15-109">Prerequisites</span></span>

* <span data-ttu-id="3bb15-110">Apache Storm on HDInsight 叢集 3.6 版。</span><span class="sxs-lookup"><span data-stu-id="3bb15-110">An Apache Storm on HDInsight cluster version 3.6.</span></span> <span data-ttu-id="3bb15-111">如需詳細資訊，請參閱[開始使用 Storm on HDInsight cluster](hdinsight-apache-storm-tutorial-get-started-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="3bb15-111">For more information, see [Get started with Storm on HDInsight cluster](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="3bb15-112">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="3bb15-112">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3bb15-113">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="3bb15-113">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="3bb15-114">[Azure 事件中樞](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)。</span><span class="sxs-lookup"><span data-stu-id="3bb15-114">An [Azure Event Hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="3bb15-115">[Oracle Java Developer Kit (JDK) 第 8 版](http://www.oracle.com/technetwork/java/javase/downloads/index.html)或同等版本，例如 [OpenJDK](http://openjdk.java.net/)。</span><span class="sxs-lookup"><span data-stu-id="3bb15-115">[Oracle Java Developer Kit (JDK) version 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or equivalent, such as [OpenJDK](http://openjdk.java.net/).</span></span>

* <span data-ttu-id="3bb15-116">[Maven](https://maven.apache.org/download.cgi)：Maven 是 Java 專案的專案建置系統。</span><span class="sxs-lookup"><span data-stu-id="3bb15-116">[Maven](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="3bb15-117">文字編輯器或整合開發環境 (IDE)。</span><span class="sxs-lookup"><span data-stu-id="3bb15-117">A text editor or integrated development environment (IDE).</span></span>

    > [!NOTE]
    > <span data-ttu-id="3bb15-118">您的編輯器或 IDE 可能具有處理 Maven 的特定功能，但未記載在這份文件中。</span><span class="sxs-lookup"><span data-stu-id="3bb15-118">Your editor or IDE may have specific functionality for working with Maven that is not addressed in this document.</span></span> <span data-ttu-id="3bb15-119">如需編輯環境功能的詳細資訊，請參閱所使用產品的文件。</span><span class="sxs-lookup"><span data-stu-id="3bb15-119">For information about the capabilities of your editing environment, see the documentation for the product you are using.</span></span>

    * <span data-ttu-id="3bb15-120">SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="3bb15-120">An SSH client.</span></span> <span data-ttu-id="3bb15-121">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="3bb15-121">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="3bb15-122">`ssh` 和 `scp` 命令。</span><span class="sxs-lookup"><span data-stu-id="3bb15-122">The `ssh` and `scp` commands.</span></span> <span data-ttu-id="3bb15-123">這些命令用來將檔案複製到 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="3bb15-123">These are used to copy files to the HDInsight cluster.</span></span> <span data-ttu-id="3bb15-124">在 Windows 上，您可以透過 Windows 10 的 Bash 執行這些命令。</span><span class="sxs-lookup"><span data-stu-id="3bb15-124">On Windows, you can get these through Bash on Windows 10.</span></span>

## <a name="understanding-the-example"></a><span data-ttu-id="3bb15-125">了解範例</span><span class="sxs-lookup"><span data-stu-id="3bb15-125">Understanding the example</span></span>

<span data-ttu-id="3bb15-126">[hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) 範例包含兩個拓撲：</span><span class="sxs-lookup"><span data-stu-id="3bb15-126">The [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) example contains two topologies:</span></span>

<span data-ttu-id="3bb15-127">`resources/writer.yaml` 拓撲會將隨機資料寫入 Azure 事件中樞。</span><span class="sxs-lookup"><span data-stu-id="3bb15-127">The `resources/writer.yaml` topology writes random data to an Azure Event Hub.</span></span> <span data-ttu-id="3bb15-128">資料由 `DeviceSpout` 產生，而且是隨機裝置識別碼和裝置值。</span><span class="sxs-lookup"><span data-stu-id="3bb15-128">The data is generated by the `DeviceSpout` component, and is a random device ID and device value.</span></span> <span data-ttu-id="3bb15-129">所以它是模擬會發出字串識別碼和數值的部分硬體。</span><span class="sxs-lookup"><span data-stu-id="3bb15-129">So it's simulating some hardware that emits a string ID and a numeric value.</span></span>

<span data-ttu-id="3bb15-130">有三個 `resources/reader.yaml` 拓撲會從事件中樞讀取資料 (由 EventHubWriter 寫入的資料)、剖析 JSON 資料，然後記錄 `deviceId` 和 `deviceValue` 資料。</span><span class="sxs-lookup"><span data-stu-id="3bb15-130">Thee `resources/reader.yaml` topology reads data from Event Hub (the data written by EventHubWriter,) parses the JSON data, and then logs the `deviceId` and `deviceValue` data.</span></span>

<span data-ttu-id="3bb15-131">資料會在寫入事件中樞之前格式化為 JSON 文件，當讀取器讀取時會從 JSON 剖析，並且進入 Tuple。</span><span class="sxs-lookup"><span data-stu-id="3bb15-131">The data is formatted as a JSON document before it is written to Event Hub, and when read by the reader it is parsed out of JSON and into tuples.</span></span> <span data-ttu-id="3bb15-132">JSON 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="3bb15-132">The JSON format is as follows:</span></span>

    { "deviceId": "unique identifier", "deviceValue": some value }

### <a name="project-configuration"></a><span data-ttu-id="3bb15-133">專案組態</span><span class="sxs-lookup"><span data-stu-id="3bb15-133">Project configuration</span></span>

<span data-ttu-id="3bb15-134">`POM.xml` 檔案包含此 Maven 專案的組態資訊。</span><span class="sxs-lookup"><span data-stu-id="3bb15-134">The `POM.xml` file contains configuration information for this Maven project.</span></span> <span data-ttu-id="3bb15-135">有趣的部分是：</span><span class="sxs-lookup"><span data-stu-id="3bb15-135">The interesting pieces are:</span></span>

#### <a name="event-hub-components"></a><span data-ttu-id="3bb15-136">事件中樞元件</span><span class="sxs-lookup"><span data-stu-id="3bb15-136">Event Hub components</span></span>

<span data-ttu-id="3bb15-137">讀取和寫入至 Azure 事件中樞的元件位於 [HDInsight 儲存機制](https://github.com/hdinsight/mvn-rep)。</span><span class="sxs-lookup"><span data-stu-id="3bb15-137">The component that reads and writes to Azure Event Hubs is located in the [HDInsight repository](https://github.com/hdinsight/mvn-rep).</span></span> <span data-ttu-id="3bb15-138">`POM.xml` 檔案的下列各區段可從這個儲存機制載入元件</span><span class="sxs-lookup"><span data-stu-id="3bb15-138">The following sections in the `POM.xml` file load the components from this repository</span></span>

```xml
<repositories>
    <repository>
        <id>hdinsight-examples</id>
        <url>http://raw.github.com/hdinsight/mvn-repo/master</url>
    </repository>
</repositories>
```

#### <a name="the-eventhubs-storm-spout-dependency"></a><span data-ttu-id="3bb15-139">EventHubs Storm Spout 相依性</span><span class="sxs-lookup"><span data-stu-id="3bb15-139">The EventHubs Storm Spout dependency</span></span>

```xml
<dependency>
    <groupId>com.microsoft</groupId>
    <artifactId>eventhubs</artifactId>
    <version>${storm.eventhub.version}</version>
</dependency>
```

<span data-ttu-id="3bb15-140">這個 xml 會定義 eventhubs 套件的相依性，當中包含用以從「事件中樞」讀取的 Spout 和寫入「事件中樞」的 Bolt。</span><span class="sxs-lookup"><span data-stu-id="3bb15-140">This xml defines a dependency for the eventhubs package, which contains both a spout for reading from Event Hubs, and a bolt for writing to it.</span></span>

```xml
</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

<span data-ttu-id="3bb15-141">這個 XML 會將專案設定為產生 Java 8 的輸出，而輸出將由 HDInsight 3.5 或更新版本使用。</span><span class="sxs-lookup"><span data-stu-id="3bb15-141">This xml configures the project to generate output for Java 8, which is used by HDInsight 3.5 or higher.</span></span>

#### <a name="the-maven-shade-plugin"></a><span data-ttu-id="3bb15-142">maven-shade-plugin</span><span class="sxs-lookup"><span data-stu-id="3bb15-142">The maven-shade-plugin</span></span>

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

<span data-ttu-id="3bb15-143">這個 XML 會將解決方案設定為把輸出封裝成 uber jar 。</span><span class="sxs-lookup"><span data-stu-id="3bb15-143">This xml configures the solution to package the output into an uber jar.</span></span> <span data-ttu-id="3bb15-144">jar 包含專案程式碼和必要的相依性。</span><span class="sxs-lookup"><span data-stu-id="3bb15-144">The jar contains both the project code and required dependencies.</span></span> <span data-ttu-id="3bb15-145">它也用來：</span><span class="sxs-lookup"><span data-stu-id="3bb15-145">It is also used to:</span></span>

* <span data-ttu-id="3bb15-146">重新命名相依性的授權檔案。</span><span class="sxs-lookup"><span data-stu-id="3bb15-146">Rename license files for the dependencies.</span></span>
* <span data-ttu-id="3bb15-147">排除安全性/簽章。</span><span class="sxs-lookup"><span data-stu-id="3bb15-147">Exclude security/signatures.</span></span>
* <span data-ttu-id="3bb15-148">請確定介面相同的多個實作會合併成一個項目。</span><span class="sxs-lookup"><span data-stu-id="3bb15-148">Ensure that multiple implementations of the same interface are merged into one entry.</span></span>

<span data-ttu-id="3bb15-149">這些組態設定可防止執行階段錯誤。</span><span class="sxs-lookup"><span data-stu-id="3bb15-149">These configuration settings prevent errors at runtime.</span></span>

#### <a name="topology-definitions"></a><span data-ttu-id="3bb15-150">拓撲定義</span><span class="sxs-lookup"><span data-stu-id="3bb15-150">Topology definitions</span></span>

<span data-ttu-id="3bb15-151">這個範例會使用 [Flux](https://storm.apache.org/releases/1.1.0/flux.html) 架構。</span><span class="sxs-lookup"><span data-stu-id="3bb15-151">This example uses the [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework.</span></span> <span data-ttu-id="3bb15-152">此架構則使用 YAML 來定義拓撲。</span><span class="sxs-lookup"><span data-stu-id="3bb15-152">This framework uses YAML to define the topologies.</span></span> <span data-ttu-id="3bb15-153">主要優點為您不是將拓撲寫入 Java 程式碼。</span><span class="sxs-lookup"><span data-stu-id="3bb15-153">The primary benefit is that you aren't hard coding the topology in Java code.</span></span> <span data-ttu-id="3bb15-154">由於定義是 YAML，因此您可以在提交拓撲之前變更它，而不必重新編譯所有項目。</span><span class="sxs-lookup"><span data-stu-id="3bb15-154">Since the definition is YAML, you can change it before submitting the topology, without having to recompile everything.</span></span>

<span data-ttu-id="3bb15-155">__writer.yaml__：</span><span class="sxs-lookup"><span data-stu-id="3bb15-155">__writer.yaml__:</span></span>

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubwriter"

components:
  # Configure the Event Hub spout
  - id: "eventhubbolt-config"
    className: "org.apache.storm.eventhubs.bolt.EventHubBoltConfig"
    constructorArgs:
      # These are populated from the .properties file when the topology is started
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
    # parallelism hint. This should be the same as the number of partitions for your Event Hub, so we read it from the dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

# How data flows through the components
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

<span data-ttu-id="3bb15-156">__reader.yaml__：</span><span class="sxs-lookup"><span data-stu-id="3bb15-156">__reader.yaml__:</span></span>

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubreader"

components:
  # Configure the Event Hub spout
  - id: "eventhubspout-config"
    className: "org.apache.storm.eventhubs.spout.EventHubSpoutConfig"
    constructorArgs:
      # These are populated from the .properties file when the topology is started
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
    # parallelism hint. This should be the same as the number of partitions for your Event Hub, so we read it from the dev.properties file passed at run time.
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

# How data flows through the components
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

#### <a name="tell-the-topology-about-event-hub"></a><span data-ttu-id="3bb15-157">分辨事件中樞的相關拓撲</span><span class="sxs-lookup"><span data-stu-id="3bb15-157">Tell the topology about Event Hub</span></span>

<span data-ttu-id="3bb15-158">在執行階段，`dev.properties` 檔案用來將事件中樞設定傳遞至拓撲。</span><span class="sxs-lookup"><span data-stu-id="3bb15-158">At run time, the `dev.properties` file is used to pass the Event Hub configuration to the topology.</span></span> <span data-ttu-id="3bb15-159">下列範例是檔案的預設內容：</span><span class="sxs-lookup"><span data-stu-id="3bb15-159">The following example is the default contents of the file:</span></span>

```yaml
eventhub.write.policy.name: writer
eventhub.write.policy.key: your_key_here
eventhub.read.policy.name: reader
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: storm
eventhub.partitions: 2
```

## <a name="configure-environment-variables"></a><span data-ttu-id="3bb15-160">設定環境變數</span><span class="sxs-lookup"><span data-stu-id="3bb15-160">Configure environment variables</span></span>

<span data-ttu-id="3bb15-161">當您在開發工作站上安裝 Java 和 JDK 時可能會設定下列環境變數。</span><span class="sxs-lookup"><span data-stu-id="3bb15-161">The following environment variables may be set when you install Java and the JDK on your development workstation.</span></span> <span data-ttu-id="3bb15-162">不過，您應該檢查它們是否存在，以及它們是否包含您系統的正確值。</span><span class="sxs-lookup"><span data-stu-id="3bb15-162">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="3bb15-163">**JAVA_HOME** - 應該指向已安裝 Java 執行階段環境 (JRE) 的目錄。</span><span class="sxs-lookup"><span data-stu-id="3bb15-163">**JAVA_HOME** - should point to the directory where the Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="3bb15-164">例如，在 Unix 或 Linux 散發套件上，它的值應該類似 `/usr/lib/jvm/java-7-oracle`</span><span class="sxs-lookup"><span data-stu-id="3bb15-164">For example, in a Unix or Linux distribution, it should have a value similar to `/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="3bb15-165">在 Windows 中，它的值應該類似 `c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="3bb15-165">In Windows, it would have a value similar to `c:\Program Files (x86)\Java\jre1.7`</span></span>
* <span data-ttu-id="3bb15-166">**PATH** - 應該包含下列路徑：</span><span class="sxs-lookup"><span data-stu-id="3bb15-166">**PATH** - should contain the following paths:</span></span>

  * <span data-ttu-id="3bb15-167">**JAVA_HOME** (或對等的路徑)</span><span class="sxs-lookup"><span data-stu-id="3bb15-167">**JAVA_HOME** (or the equivalent path)</span></span>
  * <span data-ttu-id="3bb15-168">**JAVA_HOME\bin** (或對等的路徑)</span><span class="sxs-lookup"><span data-stu-id="3bb15-168">**JAVA_HOME\bin** (or the equivalent path)</span></span>
  * <span data-ttu-id="3bb15-169">已安裝 Maven 的目錄</span><span class="sxs-lookup"><span data-stu-id="3bb15-169">The directory where Maven is installed</span></span>

## <a name="configure-event-hub"></a><span data-ttu-id="3bb15-170">設定事件中樞</span><span class="sxs-lookup"><span data-stu-id="3bb15-170">Configure Event Hub</span></span>

<span data-ttu-id="3bb15-171">事件中樞是此範例的資料來源。</span><span class="sxs-lookup"><span data-stu-id="3bb15-171">Event Hubs is the data source for this example.</span></span> <span data-ttu-id="3bb15-172">使用下列步驟建立事件中樞。</span><span class="sxs-lookup"><span data-stu-id="3bb15-172">Use the following steps to create a Event Hub.</span></span>

1. <span data-ttu-id="3bb15-173">從 [Azure 傳統入口網站](https://manage.windowsazure.com)選取 [新增]  >  [服務匯流排]  >  [事件中樞]  > [自訂建立]。</span><span class="sxs-lookup"><span data-stu-id="3bb15-173">From the [Azure Classic Portal](https://manage.windowsazure.com), select **NEW** > **Service Bus** > **Event Hub** > **Custom Create**.</span></span>

2. <span data-ttu-id="3bb15-174">在 [新增事件中樞] 畫面上，輸入 [事件中樞名稱]。</span><span class="sxs-lookup"><span data-stu-id="3bb15-174">On the **Add a new Event Hub** screen, enter an **Event Hub Name**.</span></span> <span data-ttu-id="3bb15-175">選取要建立中樞的 [區域]，然後建立新的命名空間或選取現有的命名空間。</span><span class="sxs-lookup"><span data-stu-id="3bb15-175">Select the **Region** to create the hub in, and then create a namespace or select an existing one.</span></span> <span data-ttu-id="3bb15-176">最後，按一下**箭頭**進行下一步。</span><span class="sxs-lookup"><span data-stu-id="3bb15-176">Finally, click the **Arrow** to continue.</span></span>

    ![精靈頁面 1](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz1.png)

   > [!NOTE]
   > <span data-ttu-id="3bb15-178">選取與 Storm on HDInsight 伺服器相同的 [位置]，可降低延遲和成本。</span><span class="sxs-lookup"><span data-stu-id="3bb15-178">Select the same **Location** as your Storm on HDInsight server to reduce latency and costs.</span></span>

3. <span data-ttu-id="3bb15-179">在 [設定事件中樞] 畫面中，輸入 [資料分割計數] 及 [訊息保留] 值。</span><span class="sxs-lookup"><span data-stu-id="3bb15-179">On the **Configure Event Hub** screen, enter the **Partition count** and **Message Retention** values.</span></span> <span data-ttu-id="3bb15-180">在此範例中，資料分割計數使用 10，訊息保留使用 1。</span><span class="sxs-lookup"><span data-stu-id="3bb15-180">For this example, use a partition count of 10 and a message retention of 1.</span></span> <span data-ttu-id="3bb15-181">請記下資料分割計數，因為您稍後會用到這個值。</span><span class="sxs-lookup"><span data-stu-id="3bb15-181">Note the partition count because you need this value later.</span></span>

    ![精靈頁面 2](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz2.png)

4. <span data-ttu-id="3bb15-183">建立事件中樞之後，依序選取命名空間、[事件中樞] ，然後選取您先前建立的事件中樞。</span><span class="sxs-lookup"><span data-stu-id="3bb15-183">After the event hub has been created, select the namespace, select **Event Hubs**, and then select the event hub that you created earlier.</span></span>
5. <span data-ttu-id="3bb15-184">選取 [設定]，然後使用下列資訊建立兩個新的存取原則：</span><span class="sxs-lookup"><span data-stu-id="3bb15-184">Select **Configure**, then create two new access policies by using the following information:</span></span>

    <table>
    <tr><th><span data-ttu-id="3bb15-185">名稱</span><span class="sxs-lookup"><span data-stu-id="3bb15-185">Name</span></span></th><th><span data-ttu-id="3bb15-186">權限</span><span class="sxs-lookup"><span data-stu-id="3bb15-186">Permissions</span></span></th></tr>
    <tr><td><span data-ttu-id="3bb15-187">寫入器</span><span class="sxs-lookup"><span data-stu-id="3bb15-187">Writer</span></span></td><td><span data-ttu-id="3bb15-188">傳送</span><span class="sxs-lookup"><span data-stu-id="3bb15-188">Send</span></span></td></tr>
    <tr><td><span data-ttu-id="3bb15-189">讀取者</span><span class="sxs-lookup"><span data-stu-id="3bb15-189">Reader</span></span></td><td><span data-ttu-id="3bb15-190">接聽</span><span class="sxs-lookup"><span data-stu-id="3bb15-190">Listen</span></span></td></tr>
    </table>

    <span data-ttu-id="3bb15-191">建立權限之後，在頁面底部選取 **儲存** 圖示。</span><span class="sxs-lookup"><span data-stu-id="3bb15-191">After You create the permissions, select the **Save** icon at the bottom of the page.</span></span> <span data-ttu-id="3bb15-192">這些共用的存取原則是用來讀取和寫入事件中樞。</span><span class="sxs-lookup"><span data-stu-id="3bb15-192">These shared access policies are used to read and write to Event Hub.</span></span>

    ![原則](./media/hdinsight-storm-develop-csharp-event-hub-topology/policy.png)

6. <span data-ttu-id="3bb15-194">儲存原則之後，請使用頁面底部的 [共用存取金鑰產生器] 來擷取 [寫入器] 和 [讀取器] 原則的金鑰。</span><span class="sxs-lookup"><span data-stu-id="3bb15-194">After you save the policies, use the **Shared access key generator** at the bottom of the page to retrieve the key for the **writer** and **reader** policies.</span></span> <span data-ttu-id="3bb15-195">儲存這些金鑰。</span><span class="sxs-lookup"><span data-stu-id="3bb15-195">Save these keys.</span></span>

## <a name="download-and-build-the-project"></a><span data-ttu-id="3bb15-196">下載和建置專案</span><span class="sxs-lookup"><span data-stu-id="3bb15-196">Download and build the project</span></span>

1. <span data-ttu-id="3bb15-197">從 GitHub 下載專案： [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub)。</span><span class="sxs-lookup"><span data-stu-id="3bb15-197">Download the project from GitHub: [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span></span> <span data-ttu-id="3bb15-198">您可以將封裝下載為 zip 封存，或使用 [git](https://git-scm.com/) 以在本機複製專案。</span><span class="sxs-lookup"><span data-stu-id="3bb15-198">You can either download the package as a zip archive, or use [git](https://git-scm.com/) to clone the project locally.</span></span>

2. <span data-ttu-id="3bb15-199">使用事件中樞設定修改 `dev.properties` 檔案。</span><span class="sxs-lookup"><span data-stu-id="3bb15-199">Modify the `dev.properties` file with the configuration for your Event Hub.</span></span>

3. <span data-ttu-id="3bb15-200">使用下列項目建置和封裝專案：</span><span class="sxs-lookup"><span data-stu-id="3bb15-200">Use the following to build and package the project:</span></span>

        mvn package

    <span data-ttu-id="3bb15-201">這個命令會下載必要的相依性、進行建置，然後封裝專案。</span><span class="sxs-lookup"><span data-stu-id="3bb15-201">This command downloads required dependencies, builds, and then packages the project.</span></span> <span data-ttu-id="3bb15-202">輸出會在 **/target** 目錄儲存為 **EventHubExample-1.0-SNAPSHOT.jar**。</span><span class="sxs-lookup"><span data-stu-id="3bb15-202">The output is stored in the **/target** directory as **EventHubExample-1.0-SNAPSHOT.jar**.</span></span>

## <a name="test-locally"></a><span data-ttu-id="3bb15-203">本機測試</span><span class="sxs-lookup"><span data-stu-id="3bb15-203">Test locally</span></span>

<span data-ttu-id="3bb15-204">由於這些拓撲中只會讀取和寫入至事件中樞，因此如果您有 [Storm 開發環境](http://storm.apache.org/releases/current/Setting-up-development-environment.html)，則可以在本機測試它們。</span><span class="sxs-lookup"><span data-stu-id="3bb15-204">Since these topologies just read and write to Event Hubs, you can test them locally if you have a [Storm development environment](http://storm.apache.org/releases/current/Setting-up-development-environment.html).</span></span> <span data-ttu-id="3bb15-205">使用下列步驟，以在開發環境的本機中執行：</span><span class="sxs-lookup"><span data-stu-id="3bb15-205">Use the following steps to run locally in the dev environment:</span></span>

1. <span data-ttu-id="3bb15-206">執行寫入器：</span><span class="sxs-lookup"><span data-stu-id="3bb15-206">Run the writer:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /writer.yaml --filter dev.properties

2. <span data-ttu-id="3bb15-207">執行讀取器：</span><span class="sxs-lookup"><span data-stu-id="3bb15-207">Run the reader:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /reader.yaml --filter dev.properties

> [!TIP]
> * <span data-ttu-id="3bb15-208">`--local`：以本機模式執行拓撲 (非分散式)。</span><span class="sxs-lookup"><span data-stu-id="3bb15-208">`--local`: Run the topology in local mode (non-distributed).</span></span>
> * <span data-ttu-id="3bb15-209">`-R /writer.yaml`：從封裝在 Jar 中的 `resources` 載入拓撲定義。</span><span class="sxs-lookup"><span data-stu-id="3bb15-209">`-R /writer.yaml`: Load the topology definition from the `resources` packaged in the jar.</span></span> <span data-ttu-id="3bb15-210">如果拓撲為本機檔案系統上的檔案，請改為指定其路徑作為最後一個參數。</span><span class="sxs-lookup"><span data-stu-id="3bb15-210">If the topology is a file on the local file system, specify the path to it as the last parameter instead.</span></span>
> * <span data-ttu-id="3bb15-211">`--filter dev.properties`：使用 `dev.properties` 的內容在拓撲定義中填入值。</span><span class="sxs-lookup"><span data-stu-id="3bb15-211">`--filter dev.properties`: Use the contents of `dev.properties` to fill in the values in the topology definitions.</span></span> <span data-ttu-id="3bb15-212">例如， `${eventhub.read.policy.name}`。</span><span class="sxs-lookup"><span data-stu-id="3bb15-212">For example, `${eventhub.read.policy.name}`.</span></span>

<span data-ttu-id="3bb15-213">在本機執行時，輸出會記錄至主控台。</span><span class="sxs-lookup"><span data-stu-id="3bb15-213">Output is logged to the console when running locally.</span></span> <span data-ttu-id="3bb15-214">使用 __Ctrl+C__ 來停止拓撲。</span><span class="sxs-lookup"><span data-stu-id="3bb15-214">Use __Ctrl+C__ to stop the topology.</span></span>

## <a name="deploy-the-topologies"></a><span data-ttu-id="3bb15-215">部署拓撲</span><span class="sxs-lookup"><span data-stu-id="3bb15-215">Deploy the topologies</span></span>

1. <span data-ttu-id="3bb15-216">使用 SCP 將 jar 封裝複製到您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="3bb15-216">Use SCP to copy the jar package to your HDInsight cluster.</span></span> <span data-ttu-id="3bb15-217">將 USERNAME 取代為用於您的叢集的 SSH 使用者。</span><span class="sxs-lookup"><span data-stu-id="3bb15-217">Replace USERNAME with the SSH user for your cluster.</span></span> <span data-ttu-id="3bb15-218">將 CLUSTERNAME 取代為 HDInsight 叢集的名稱：</span><span class="sxs-lookup"><span data-stu-id="3bb15-218">Replace CLUSTERNAME with the name of your HDInsight cluster:</span></span>

        scp ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.

    <span data-ttu-id="3bb15-219">如果您針對 SSH 帳戶使用密碼，系統會提示您輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="3bb15-219">If you used a password for your SSH account, you are prompted to enter the password.</span></span> <span data-ttu-id="3bb15-220">如果您搭配帳戶使用 SSH 金鑰，可能需要使用 `-i` 參數來指定金鑰檔的路徑。</span><span class="sxs-lookup"><span data-stu-id="3bb15-220">If you used an SSH key with the account, you may need to use the `-i` parameter to specify the path to the key file.</span></span> <span data-ttu-id="3bb15-221">例如， `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span><span class="sxs-lookup"><span data-stu-id="3bb15-221">For example, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span></span>

    <span data-ttu-id="3bb15-222">此命令會將檔案複製到叢集上 SSH 使用者的主目錄中。</span><span class="sxs-lookup"><span data-stu-id="3bb15-222">This command copies the file to the home directory of your SSH user on the cluster.</span></span>

2. <span data-ttu-id="3bb15-223">完成上傳檔案之後，使用 SSH 以連接到 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="3bb15-223">Once the file has finished uploading, use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="3bb15-224">將 **USERNAME** 取代為您的 SSH 登入名稱。</span><span class="sxs-lookup"><span data-stu-id="3bb15-224">Replace **USERNAME** the name of your SSH login.</span></span> <span data-ttu-id="3bb15-225">將 **CLUSTERNAME** 取代為 HDInsight 叢集名稱：</span><span class="sxs-lookup"><span data-stu-id="3bb15-225">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    > [!NOTE]
    > <span data-ttu-id="3bb15-226">如果您針對 SSH 帳戶使用密碼，系統會提示您輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="3bb15-226">If you used a password for your SSH account, you are prompted to enter the password.</span></span> <span data-ttu-id="3bb15-227">如果您搭配帳戶使用 SSH 金鑰，可能需要使用 `-i` 參數來指定金鑰檔的路徑。</span><span class="sxs-lookup"><span data-stu-id="3bb15-227">If you used an SSH key with the account, you may need to use the `-i` parameter to specify the path to the key file.</span></span> <span data-ttu-id="3bb15-228">下列範例會從 `~/.ssh/id_rsa` 載入私密金鑰：</span><span class="sxs-lookup"><span data-stu-id="3bb15-228">The following example loads the private key from `~/.ssh/id_rsa`:</span></span>
    >
    > `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`

3. <span data-ttu-id="3bb15-229">使用下列命令以啟動拓撲：</span><span class="sxs-lookup"><span data-stu-id="3bb15-229">Use the following command to start the topologies:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties

    > [!TIP]
    > * <span data-ttu-id="3bb15-230">`--remote`：將拓撲提交到 Nimbus 服務，該服務會在叢集中的背景工作節點上啟動拓撲。</span><span class="sxs-lookup"><span data-stu-id="3bb15-230">`--remote`: Submits the topology to the Nimbus service, which starts it on the worker nodes in the cluster.</span></span>

4. <span data-ttu-id="3bb15-231">若要檢視記錄的資料，請移至 https://CLUSTERNAME.azurehdinsight.net/stormui，其中 __CLUSTERNAME__ 是 HDInsight 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="3bb15-231">To view the logged data, go to https://CLUSTERNAME.azurehdinsight.net/stormui, where __CLUSTERNAME__ is the name of your HDInsight cluster.</span></span> <span data-ttu-id="3bb15-232">選取拓撲，然後向下切入至元件。</span><span class="sxs-lookup"><span data-stu-id="3bb15-232">Select the topologies and drill down to the components.</span></span> <span data-ttu-id="3bb15-233">選取元件執行個體的 __port__ 項目來檢視記錄的資訊。</span><span class="sxs-lookup"><span data-stu-id="3bb15-233">Select the __port__ entry for an instance of a component to view logged information.</span></span>

5. <span data-ttu-id="3bb15-234">使用下列命令以停止拓撲：</span><span class="sxs-lookup"><span data-stu-id="3bb15-234">Use the following commands to stop the topologies:</span></span>

        storm kill reader
        storm kill writer

## <a name="delete-your-cluster"></a><span data-ttu-id="3bb15-235">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="3bb15-235">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="3bb15-236">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3bb15-236">Next steps</span></span>

* [<span data-ttu-id="3bb15-237">Storm on HDInsight 的範例拓撲</span><span class="sxs-lookup"><span data-stu-id="3bb15-237">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
