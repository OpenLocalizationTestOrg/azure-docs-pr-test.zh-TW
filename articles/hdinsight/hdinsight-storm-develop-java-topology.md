---
title: "aaaApache Storm 範例 Java 拓樸-Azure HDInsight |Microsoft 文件"
description: "了解如何在 Java 中建立範例文字的 toocreate Apache Storm 拓撲計數拓撲。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: "apache storm,apache storm 範例,storm java,storm 拓撲範例"
ms.assetid: a8838f29-9c08-4fd9-99ef-26655d1bf6d7
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: 54fa9dc3c93ddad83ac861f3101f50f80117d804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-storm-topology-in-java"></a>在 Java 中建立 Apache Storm 拓撲

深入了解如何 toocreate Apache Storm 的 Java 為基礎的拓撲。 您會建立可實作字數統計應用程式的 Storm 拓撲。 您使用 Maven toobuild 和套件 hello 專案。 然後，您可以了解如何 toodefine hello 拓撲使用 hello 變動架構。

> [!NOTE]
> hello 變動架構是用於 Storm 0.10.0 或更新版本。 Storm 0.10.0 則可在 HDInsight 3.3 及 3.4 中使用。

完成這份文件中的 hello 步驟之後，您可以部署 hello 拓撲 tooApache HDInsight 上出現。

> [!NOTE]
> 在這份文件中建立 hello Storm 拓樸範例的完整的版本將會位於[https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount)。

## <a name="prerequisites"></a>必要條件

* [Java Developer Kit (JDK) 第 7 版](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)

* [Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi)：Maven 是適用於 Java 專案的專案建置系統。

* 文字編輯器或整合式開發環境 (IDE)。

## <a name="configure-environment-variables"></a>設定環境變數

hello 下列環境變數設定 Java 和 hello JDK 安裝時。 不過，您應該檢查其存在且包含您系統的 hello 正確值。

* **JAVA_HOME** -應該指向 toohello hello Java runtime environment (JRE) 安裝所在的目錄。 例如，在 Unix 或 Linux 的分佈，它應該有一個值類似太`/usr/lib/jvm/java-7-oracle`。 在 Windows 中，就會類似的值太`c:\Program Files (x86)\Java\jre1.7`

* **路徑**-應該包含下列路徑的 hello:

  * **JAVA_HOME** （或 hello 相等路徑）

  * **JAVA_HOME\bin** （或 hello 相等路徑）

  * hello Maven 安裝所在的目錄

## <a name="create-a-maven-project"></a>建立 Maven 專案

從 hello 命令列使用 hello 下列命令 toocreate 名為的 Maven 專案**WordCount**:

```bash
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart -DgroupId=com.microsoft.example -DartifactId=WordCount -DinteractiveMode=false
```

> [!NOTE]
> 如果您使用 PowerShell，則必須將 `-D` 參數放置在雙引號內。
>
> `mvn archetype:generate "-DarchetypeArtifactId=maven-archetype-quickstart" "-DgroupId=com.microsoft.example" "-DartifactId=WordCount" "-DinteractiveMode=false"`

此命令會建立一個名為目錄`WordCount`hello 目前位置，其中包含基本的 Maven 專案。 hello`WordCount`目錄包含下列項目 hello:

* `pom.xml`： 包含 hello Maven 專案的設定。
* `src\main\java\com\microsoft\example`︰包含應用程式的程式碼。
* `src\test\java\com\microsoft\example`︰包含應用程式的測試。 

### <a name="remove-hello-generated-example-code"></a>移除 hello 產生範例程式碼

刪除 hello 產生測試和 hello 應用程式檔案：

* **src\test\java\com\microsoft\example\AppTest.java**
* **src\main\java\com\microsoft\example\App.java**

## <a name="add-maven-repositories"></a>新增 Maven 存放庫

HDInsight 根據 hello Hortonworks Data Platform (HDP)，因此我們建議您針對您的 Apache Storm 專案使用 hello Hortonworks 儲存機制 toodownload 相依性。 在 hello __pom.xml__檔案中加入下列 XML 之後 hello hello`<url>http://maven.apache.org</url>`行：

```xml
<repositories>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPReleases</id>
        <name>HDP Releases</name>
        <url>http://repo.hortonworks.com/content/repositories/releases/</url>
        <layout>default</layout>
    </repository>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPJetty</id>
        <name>Hadoop Jetty</name>
        <url>http://repo.hortonworks.com/content/repositories/jetty-hadoop/</url>
        <layout>default</layout>
    </repository>
</repositories>
```

## <a name="add-properties"></a>加入屬性

Maven 可讓您呼叫的內容 toodefine 專案層級值。 在 hello __pom.xml__，加入下列文字之後 hello hello`</repositories>`列：

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--
    This is a version of Storm from hello Hortonworks repository that is compatible with HDInsight.
    -->
    <storm.version>1.0.1.2.5.3.0-37</storm.version>
</properties>
```

您現在可以使用此值 hello 的其他章節`pom.xml`。 例如，在指定 hello Storm 元件版本，您可以使用`${storm.version}`而不是硬式編碼值。

## <a name="add-dependencies"></a>新增相依性

新增 Storm 元件的相依性。 開啟 hello`pom.xml`檔案，然後加入下列程式碼中 hello hello `<dependencies>` > 一節：

```xml
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-core</artifactId>
    <version>${storm.version}</version>
    <!-- keep storm out of hello jar-with-dependencies -->
    <scope>provided</scope>
</dependency>
```

在編譯時期 Maven 能利用此資訊 toolook `storm-core` hello Maven 儲存機制中。 它會先尋找 hello 在本機電腦上的儲存機制中。 如果 hello 檔案不存在，Maven 將其從 hello 公用 Maven 儲存機制下載，並將它們儲存在 hello 本機儲存機制中。

> [!NOTE]
> 請注意 hello`<scope>provided</scope>`本節中的行。 此設定會告知 Maven tooexclude **storm 核心**的 JAR 檔案所建立，因為它 hello 系統所提供。

## <a name="build-configuration"></a>建置組態

Maven 外掛程式可讓您 hello 專案 toocustomize hello 組建階段。 例如，如何 hello 專案會編譯或如何 toopackage 到 JAR 檔案。 開啟 hello`pom.xml`檔案，然後加入下列程式碼正上方 hello hello`</project>`列。

```xml
<build>
    <plugins>
    </plugins>
    <resources>
    </resources>
</build>
```

此區段是使用的 tooadd 外掛程式、 資源和其他組建組態選項。 如需完整的參考的 hello **pom.xml**檔案，請參閱[http://maven.apache.org/pom.html](http://maven.apache.org/pom.html)。

### <a name="add-plug-ins"></a>新增外掛程式

如需在 Java 中實作 Apache Storm 拓撲，hello [Exec Maven 外掛程式](http://www.mojohaus.org/exec-maven-plugin/)很有用，因為它可讓您在本機開發環境中執行 hello 拓撲 tooeasily。 新增下列 toohello hello`<plugins>`區段 hello`pom.xml`檔案 tooinclude hello Exec Maven 外掛程式：

```xml
<plugin>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>exec-maven-plugin</artifactId>
    <version>1.4.0</version>
    <executions>
    <execution>
    <goals>
        <goal>exec</goal>
    </goals>
    </execution>
    </executions>
    <configuration>
    <executable>java</executable>
    <includeProjectDependencies>true</includeProjectDependencies>
    <includePluginDependencies>false</includePluginDependencies>
    <classpathScope>compile</classpathScope>
    <mainClass>${storm.topology}</mainClass>
    <cleanupDaemonThreads>false</cleanupDaemonThreads> 
    </configuration>
</plugin>
```

另一個有用外掛程式為 hello [Apache Maven 編譯器外掛程式](http://maven.apache.org/plugins/maven-compiler-plugin/)，它會使用的 toochange 編譯選項。 hello 變更 hello Maven 用於 hello 來源和目標應用程式的 Java 版本。

* Hdinsight __3.4 或更早版本__、 設定 hello 來源和目標 Java 版本 too__1.7__。

* Hdinsight __3.5__、 設定 hello 來源和目標 Java 版本 too__1.8__。

加入下列文字放 hello hello`<plugins>`區段 hello`pom.xml`檔案 tooinclude hello Apache Maven 編譯器外掛程式。 這個範例會指定 1.8，因此 hello 目標 HDInsight 版本 3.5。

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>3.3</version>
    <configuration>
    <source>1.8</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

### <a name="configure-resources"></a>Configure resources

hello 資源區段可讓您 tooinclude 非程式碼資源例如 hello 拓撲中的元件所需的組態檔。 此範例中，加入下列文字放 hello hello `<resources>` hello 區段 ' pom.xml 檔案。

```xml
<resource>
    <directory>${basedir}/resources</directory>
    <filtering>false</filtering>
    <includes>
        <include>log4j2.xml</include>
    </includes>
</resource>
```

這個範例會將 hello hello 專案根目錄中的 hello 資源目錄 (`${basedir}`) 做為位置，其中包含資源，並包含名為 「 hello 檔案`log4j2.xml`。 這個檔案是使用的 tooconfigure hello 拓撲記錄哪些資訊。

## <a name="create-hello-topology"></a>建立 hello 拓樸

Java 型 Apache Storm 拓撲包含三個您必須編寫 (或參考) 為相依性的元件。

* **Spouts**： 讀取來自外部資料來源，並發出的資料流到 hello 拓撲。

* **Bolt**：執行 Spout 或其他 Bolt 所發出資料流的處理，並發出一或多個資料流。

* **拓樸**： 定義如何 hello spouts 和發射排列，並提供 hello 拓撲 hello 進入點。

### <a name="create-hello-spout"></a>建立 hello spout

設定外部資料來源的 tooreduce 需求 hello 遵循 spout 只發出隨機的句子。 它會提供以 hello spout 的修改的版本[Storm 入門範例](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter)。

> [!NOTE]
> 如需從外部資料來源讀取 spout 的範例，請參閱 hello 遵循範例：
>
> * [TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java)：從 Twitter 讀取的 Spout 範例
> * [Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka)：從 Kafka 讀取的 Spout

建立名為檔案，hello spout `RandomSentenceSpout.java` hello 中`src\main\java\com\microsoft\example`下列 Java 程式碼做為 hello 內容的目錄，並使用 hello:

```java
package com.microsoft.example;

import org.apache.storm.spout.SpoutOutputCollector;
import org.apache.storm.task.TopologyContext;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseRichSpout;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Values;
import org.apache.storm.utils.Utils;

import java.util.Map;
import java.util.Random;

//This spout randomly emits sentences
public class RandomSentenceSpout extends BaseRichSpout {
  //Collector used tooemit output
  SpoutOutputCollector _collector;
  //Used toogenerate a random number
  Random _rand;

  //Open is called when an instance of hello class is created
  @Override
  public void open(Map conf, TopologyContext context, SpoutOutputCollector collector) {
  //Set hello instance collector toohello one passed in
    _collector = collector;
    //For randomness
    _rand = new Random();
  }

  //Emit data toohello stream
  @Override
  public void nextTuple() {
  //Sleep for a bit
    Utils.sleep(100);
    //hello sentences that are randomly emitted
    String[] sentences = new String[]{ "hello cow jumped over hello moon", "an apple a day keeps hello doctor away",
        "four score and seven years ago", "snow white and hello seven dwarfs", "i am at two with nature" };
    //Randomly pick a sentence
    String sentence = sentences[_rand.nextInt(sentences.length)];
    //Emit hello sentence
    _collector.emit(new Values(sentence));
  }

  //Ack is not implemented since this is a basic example
  @Override
  public void ack(Object id) {
  }

  //Fail is not implemented since this is a basic example
  @Override
  public void fail(Object id) {
  }

  //Declare hello output fields. In this case, an sentence
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("sentence"));
  }
}
```

> [!NOTE]
> 雖然此拓撲會使用只有一個 spout，其他人有許多不同來源的資料送入 hello 拓撲。

### <a name="create-hello-bolts"></a>建立 hello 攻擊

發射處理 hello 資料處理。 此拓撲會使用兩個 Bolt：

* **SplitSentence**： 分割所發出的 hello 句子**RandomSentenceSpout**成單字。

* **WordCount**：計算每個單字的出現次數。

> [!NOTE]
> 發射可以執行任何動作，例如，計算、 持續性，或說 tooexternal 元件。

建立兩個新的檔案，`SplitSentence.java`和`WordCount.java`在 hello`src\main\java\com\microsoft\example`目錄。 使用 hello hello hello 檔案的內容為下列文字：

#### <a name="splitsentence"></a>SplitSentence

```java
package com.microsoft.example;

import java.text.BreakIterator;

import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class SplitSentence extends BaseBasicBolt {

  //Execute is called tooprocess tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //Get hello sentence content from hello tuple
    String sentence = tuple.getString(0);
    //An iterator tooget each word
    BreakIterator boundary=BreakIterator.getWordInstance();
    //Give hello iterator hello sentence
    boundary.setText(sentence);
    //Find hello beginning first word
    int start=boundary.first();
    //Iterate over each word and emit it toohello output stream
    for (int end=boundary.next(); end != BreakIterator.DONE; start=end, end=boundary.next()) {
      //get hello word
      String word=sentence.substring(start,end);
      //If a word is whitespace characters, replace it with empty
      word=word.replaceAll("\\s+","");
      //if it's an actual word, emit it
      if (!word.equals("")) {
        collector.emit(new Values(word));
      }
    }
  }

  //Declare that emitted tuples contain a word field
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word"));
  }
}
```

#### <a name="wordcount"></a>WordCount

```java
package com.microsoft.example;

import java.util.HashMap;
import java.util.Map;
import java.util.Iterator;

import org.apache.storm.Constants;
import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;
import org.apache.storm.Config;

// For logging
import org.apache.logging.log4j.Logger;
import org.apache.logging.log4j.LogManager;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class WordCount extends BaseBasicBolt {
  //Create logger for this class
  private static final Logger logger = LogManager.getLogger(WordCount.class);
  //For holding words and counts
  Map<String, Integer> counts = new HashMap<String, Integer>();
  //How often tooemit a count of words
  private Integer emitFrequency;

  // Default constructor
  public WordCount() {
      emitFrequency=5; // Default too60 seconds
  }

  // Constructor that sets emit frequency
  public WordCount(Integer frequency) {
      emitFrequency=frequency;
  }

  //Configure frequency of tick tuples for this bolt
  //This delivers a 'tick' tuple on a specific interval,
  //which is used tootrigger certain actions
  @Override
  public Map<String, Object> getComponentConfiguration() {
      Config conf = new Config();
      conf.put(Config.TOPOLOGY_TICK_TUPLE_FREQ_SECS, emitFrequency);
      return conf;
  }

  //execute is called tooprocess tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //If it's a tick tuple, emit all words and counts
    if(tuple.getSourceComponent().equals(Constants.SYSTEM_COMPONENT_ID)
            && tuple.getSourceStreamId().equals(Constants.SYSTEM_TICK_STREAM_ID)) {
      for(String word : counts.keySet()) {
        Integer count = counts.get(word);
        collector.emit(new Values(word, count));
        logger.info("Emitting a count of " + count + " for word " + word);
      }
    } else {
      //Get hello word contents from hello tuple
      String word = tuple.getString(0);
      //Have we counted any already?
      Integer count = counts.get(word);
      if (count == null)
        count = 0;
      //Increment hello count and store it
      count++;
      counts.put(word, count);
    }
  }

  //Declare that this emits a tuple containing two fields; word and count
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word", "count"));
  }
}
```

### <a name="define-hello-topology"></a>定義 hello 拓撲

hello 拓撲繫結合作對 hello spouts 並一起釘到圖形定義 hello 元件之間資料流動的方式。 它也會提供出現在建立 hello 叢集內的 hello 元件的執行個體時所使用的平行處理原則提示。

hello 以下影像是基本的 hello 圖形的元件，針對此拓撲圖表。

![圖表顯示 hello spouts 和釘排列方式](./media/hdinsight-storm-develop-java-topology/wordcount-topology.png)

tooimplement hello 拓撲中，建立名為`WordCountTopology.java`在 hello`src\main\java\com\microsoft\example`目錄。 使用下列 Java 程式碼為 hello hello 檔案內容的 hello:

```java
package com.microsoft.example;

import org.apache.storm.Config;
import org.apache.storm.LocalCluster;
import org.apache.storm.StormSubmitter;
import org.apache.storm.topology.TopologyBuilder;
import org.apache.storm.tuple.Fields;

import com.microsoft.example.RandomSentenceSpout;

public class WordCountTopology {

  //Entry point for hello topology
  public static void main(String[] args) throws Exception {
  //Used toobuild hello topology
    TopologyBuilder builder = new TopologyBuilder();
    //Add hello spout, with a name of 'spout'
    //and parallelism hint of 5 executors
    builder.setSpout("spout", new RandomSentenceSpout(), 5);
    //Add hello SplitSentence bolt, with a name of 'split'
    //and parallelism hint of 8 executors
    //shufflegrouping subscribes toohello spout, and equally distributes
    //tuples (sentences) across instances of hello SplitSentence bolt
    builder.setBolt("split", new SplitSentence(), 8).shuffleGrouping("spout");
    //Add hello counter, with a name of 'count'
    //and parallelism hint of 12 executors
    //fieldsgrouping subscribes toohello split bolt, and
    //ensures that hello same word is sent toohello same instance (group by field 'word')
    builder.setBolt("count", new WordCount(), 12).fieldsGrouping("split", new Fields("word"));

    //new configuration
    Config conf = new Config();
    //Set toofalse toodisable debug information when
    // running in production on a cluster
    conf.setDebug(false);

    //If there are arguments, we are running on a cluster
    if (args != null && args.length > 0) {
      //parallelism hint tooset hello number of workers
      conf.setNumWorkers(3);
      //submit hello topology
      StormSubmitter.submitTopology(args[0], conf, builder.createTopology());
    }
    //Otherwise, we are running locally
    else {
      //Cap hello maximum number of executors that can be spawned
      //for a component too3
      conf.setMaxTaskParallelism(3);
      //LocalCluster is used toorun locally
      LocalCluster cluster = new LocalCluster();
      //submit hello topology
      cluster.submitTopology("word-count", conf, builder.createTopology());
      //sleep
      Thread.sleep(10000);
      //shut down hello cluster
      cluster.shutdown();
    }
  }
}
```

### <a name="configure-logging"></a>設定記錄

Storm 使用 Apache Log4j toolog 資訊。 如果您未設定記錄，hello 拓撲會發出診斷資訊。 toocontrol 記錄，建立名為`log4j2.xml`在 hello`resources`目錄。 使用下列 XML 當做 hello hello 檔案內容的 hello。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration>
<Appenders>
    <Console name="STDOUT" target="SYSTEM_OUT">
        <PatternLayout pattern="%d{HH:mm:ss} [%t] %-5level %logger{36} - %msg%n"/>
    </Console>
</Appenders>
<Loggers>
    <Logger name="com.microsoft.example" level="trace" additivity="false">
        <AppenderRef ref="STDOUT"/>
    </Logger>
    <Root level="error">
        <Appender-Ref ref="STDOUT"/>
    </Root>
</Loggers>
</Configuration>
```

這段 XML 會設定新的記錄器 hello`com.microsoft.example`類別，其中包含在此範例拓撲中的 hello 元件。 hello 層級設定 tootrace 針對這個記錄器，這會擷取此拓撲中的元件所發出的任何記錄資訊。

hello`<Root level="error">`區段設定 hello 根層級的記錄 (所有項目不能在`com.microsoft.example`) tooonly 記錄資訊時發生錯誤。

如需針對 Log4j 設定記錄的詳細資訊，請參閱 [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html)(英文)。

> [!NOTE]
> Storm 0.10.0 和更新版本是使用 Log4j 2.x。 舊版的 Storm 使用 Log4j 1.x，它們使用不同格式的記錄設定。 如需 hello 舊組態資訊，請參閱[http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat)。

## <a name="test-hello-topology-locally"></a>在本機測試 hello 拓樸

儲存 hello 檔案之後，使用下列命令 tootest hello 拓撲在本機的 hello。

```bash
mvn compile exec:java -Dstorm.topology=com.microsoft.example.WordCountTopology
```

當它執行時，hello 拓撲會顯示啟動資訊。 hello 下列文字是 hello word 計數輸出的範例：

    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
    17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word snow

此範例記錄檔指出該 hello 單字 '和' 已經發出 113 次。 hello 計數若持續 toogo 向上只要 hello 拓撲會執行，因為 hello spout 持續發出 hello 相同的句子。

在發出單字和計算次數之間有 5 秒的間隔。 hello **WordCount**元件設定 tooonly 刻度 tuple 抵達時，發出資訊。 它會要求計時 Tuple 每隔五秒才傳送。

## <a name="convert-hello-topology-tooflux"></a>轉換 hello 拓撲 tooFlux

變動是新的架構使用 Storm 0.10.0 及更新版本，可讓您實作 tooseparate 組態。 您的元件仍會定義在 Java 中，但 hello 拓撲使用 YAML 檔案所定義。 您可以使用您的專案，封裝的預設拓撲定義，或傳送 hello 拓撲時，請使用獨立檔案。 當送出 hello 拓撲 tooStorm，您可以使用環境變數或組態檔 toopopulate 值在 hello YAML 拓撲定義。

hello YAML 檔案會定義 hello 元件 toouse hello 拓樸和 hello 兩者之間的資料流。 您可以包含 YAML 檔案當做 hello jar 檔案的一部分，或者您可以使用外部 YAML 檔案。

如需 Flux 的詳細資訊，請參閱 [Flux 架構 (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html)。

> [!WARNING]
> 到期 tooa [bug (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055)風暴 1.0.1，您可能需要 tooinstall [Storm 開發環境](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)本機 toorun 變動的拓撲。

1. 移動 hello `WordCountTopology.java` hello 專案檔案。 先前，此檔案定義 hello 拓撲，但不需要使用變動。

2. 在 hello`resources`目錄中，建立名為`topology.yaml`。 使用 hello hello 這個檔案的內容為下列文字。

        name: "wordcount"       # friendly name for hello topology
        
        config:                 # Topology configuration
        topology.workers: 1     # Hint for hello number of workers toocreate
        
        spouts:                 # Spout definitions
        - id: "sentence-spout"
            className: "com.microsoft.example.RandomSentenceSpout"
            parallelism: 1      # parallelism hint
        
        bolts:                  # Bolt definitions
        - id: "splitter-bolt"
            className: "com.microsoft.example.SplitSentence"
            parallelism: 1
         
        - id: "counter-bolt"
            className: "com.microsoft.example.WordCount"
            constructorArgs:
                - 10
            parallelism: 1
        
        streams:                # Stream definitions
            - name: "Spout --> Splitter" # name isn't used (placeholder for logging, UI, etc.)
            from: "sentence-spout"       # hello stream emitter
            to: "splitter-bolt"          # hello stream consumer
            grouping:                    # Grouping type
                type: SHUFFLE
          
            - name: "Splitter -> Counter"
            from: "splitter-bolt"
            to: "counter-bolt"
            grouping:
            type: FIELDS
                args: ["word"]           # field(s) toogroup on

3. 進行下列變更 toohello hello`pom.xml`檔案。
   
   * 新增下列新的相依性中 hello hello `<dependencies>` > 一節：
     
        ```xml
        <!-- Add a dependency on hello Flux framework -->
        <dependency>
            <groupId>org.apache.storm</groupId>
            <artifactId>flux-core</artifactId>
            <version>${storm.version}</version>
        </dependency>
        ```
   * 新增下列外掛程式 toohello hello `<plugins>` > 一節。 此外掛程式負責處理 hello 專案 hello 建立的封裝 （jar 檔案），並建立 hello 套件時，適用於某些轉換特定 tooFlux。
     
        ```xml
        <!-- build an uber jar -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
                <transformers>
                    <!-- Keep us from getting a "can't overwrite file error" -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer" />
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer" />
                    <!-- We're using Flux, so refer tooit as main -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                        <mainClass>org.apache.storm.flux.Flux</mainClass>
                    </transformer>
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

   * 在 hello **exec-maven-外掛程式**`<configuration>`區段中，變更 hello 值`<mainClass>`太`org.apache.storm.flux.Flux`。 此設定可讓程式開發中的本機執行 hello 拓撲變動 toohandle。

   * 在 hello`<resources>`區段中，新增下列 toohello hello `<includes>`。 這段 XML 會包含 hello YAML 檔案 hello 拓樸中定義的 hello 專案的一部分。

        ```xml
        <include>topology.yaml</include>
        ```

## <a name="test-hello-flux-topology-locally"></a>測試本機 hello 變動拓樸

1. 使用下列 toocompile hello 和執行使用 Maven hello 變動拓撲：

    ```bash
    mvn compile exec:java -Dexec.args="--local -R /topology.yaml"
    ```

    如果您使用 PowerShell，使用下列命令的 hello:

    ```bash
    mvn compile exec:java "-Dexec.args=--local -R /topology.yaml"
    ```

    > [!WARNING]
    > 如果您的拓撲使用 Storm 1.0.1 位元，此命令就會失敗。 此失敗是由 [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055) 所造成。 相反地，[開發環境中安裝 Storm](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html)和使用 hello 下列資訊。

    如果您有[開發環境中安裝 Storm](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html)，您可以使用 hello 改用下列命令：

    ```bash
    mvn compile package
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /topology.yaml
    ```

    hello`--local`參數在本機模式中執行 hello 拓撲，在開發環境上。 hello`-R /topology.yaml`參數會使用 hello `topology.yaml` hello jar 檔案 toodefine hello 拓撲檔案資源。

    當它執行時，hello 拓撲會顯示啟動資訊。 下列文字的 hello 是 hello 輸出的範例：

        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
        17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs

    記錄資訊的批次之間有 10 秒的延遲時間。

2. 建立一份 hello `topology.yaml` hello 專案檔案。 新檔案的名稱 hello `newtopology.yaml`。 在 hello`newtopology.yaml`檔案中，尋找 hello 下列區段，並且變更 hello 值`10`太`5`。 從 10 秒 too5 計數此修改變更 hello 間隔發出批次的文字。

    ```yaml
    - id: "counter-bolt"
    className: "com.microsoft.example.WordCount"
    constructorArgs:
    - 5
    parallelism: 1
    ```yaml

3. toorun hello topology, use hello following command:

    ```bash
    mvn exec:java -Dexec.args="--local /path/to/newtopology.yaml"
    ```

    或者，如果您的開發環境上含有 Storm：

    ```bash
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local /path/to/newtopology.yaml
    ```

    變更 hello `/path/to/newtopology.yaml` toohello 路徑 toohello newtopology.yaml 檔案 hello 先前步驟中所建立。 此命令會使用 hello newtopology.yaml 與 hello 拓撲定義。 因為我們並未包含 hello`compile`參數，Maven 使用在先前步驟中建立專案時 hello hello 版本。

    一次 hello 拓樸開始，您應該注意到 hello 發出批次之間的時間已變更 newtopology.yaml tooreflect hello 值。 因此，您可以看到您可以變更您的設定透過 YAML 檔案而不需要 toorecompile hello 拓撲。

如需有關這些和其他功能的 hello 變動架構的詳細資訊，請參閱[變動 (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html)。

## <a name="trident"></a>Trident

Trident 是 Storm 提供的高層級抽象。 它支援具狀態的處理。 hello 戟主要優點是，它可以保證進入 hello 拓撲的每個訊息處理一次。 若未使用 Trident，您的拓撲只能保證至少處理一次訊息。 還有其他差異，例如可供使用的內建元件，而不是建立 Bolt。 事實上，較不一般的元件 (例如篩選、投影和函數) 會取代 Bolt。

可以使用 Maven 專案來建立 Trident 應用程式。 使用 hello 相同的基本步驟，如本文稍早提供 — 僅 hello 程式碼都不同。 戟也 （目前） 無法與 hello 變動架構使用。

如需戟的詳細資訊，請參閱 hello[戟 API 概觀](http://storm.apache.org/documentation/Trident-API-Overview.html)。

如需 Trident 應用程式的範例，請參閱 [Twitter 的趨勢主題與 Apache Storm on HDInsight](hdinsight-storm-twitter-trending.md)。

## <a name="next-steps"></a>後續步驟

您已經學會如何使用 Java 的 Storm 拓樸 toocreate。 現在要了解如何：

* [部署和管理 HDInsight 上的 Apache Storm 拓撲](hdinsight-storm-deploy-monitor-topology.md)

* [使用 Visual Studio 開發 Apache Storm on HDInsight 的 C# 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)

您可透過瀏覽 [Storm on HDInsight 的範例拓撲](hdinsight-storm-example-topology.md)找到更多範例 Storm 拓撲。

