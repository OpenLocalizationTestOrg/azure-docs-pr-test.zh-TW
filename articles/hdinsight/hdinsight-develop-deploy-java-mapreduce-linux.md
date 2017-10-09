---
title: "aaaCreate Hadoop-Azure HDInsight 的 Java MapReduce |Microsoft 文件"
description: "深入了解如何 toouse Apache Maven Java 為基礎的 toocreate MapReduce 應用程式，然後加以執行的 Hadoop Azure HDInsight 上。"
services: hdinsight
editor: cgronlun
manager: jhubbard
author: Blackmist
documentationcenter: 
tags: azure-portal
ms.assetid: 9ee6384c-cb61-4087-8273-fb53fa27c1c3
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 903a57a482395f7da79002188399a4d6288ff0af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="develop-java-mapreduce-programs-for-hadoop-on-hdinsight"></a>在 HDInsight 上開發 Hadoop 的 Java MapReduce 程式

深入了解如何 toouse Apache Maven Java 為基礎的 toocreate MapReduce 應用程式，然後加以執行的 Hadoop Azure HDInsight 上。

> [!NOTE]
> 此範例最近已在 HDInsight 3.6 上測試過。

## <a name="prerequisites"></a>必要條件

* [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 或更新版本 (或同等功能版本，例如 OpenJDK)。
    
    > [!NOTE]
    > HDInsight 版本 3.4 和先前版本會使用 Java 7。 HDInsight 3.5 和更新版本會使用 Java 8。

* [Apache Maven](http://maven.apache.org/)

## <a name="configure-development-environment"></a>設定開發環境

hello 下列環境變數設定 Java 和 hello JDK 安裝時。 不過，您應該檢查其存在且包含您系統的 hello 正確值。

* `JAVA_HOME`-應該指向 toohello hello Java runtime environment (JRE) 安裝所在的目錄。 例如，在 OS X、 Unix 或 Linux 系統上，就不應有類似的值太`/usr/lib/jvm/java-7-oracle`。 在 Windows 中，就會類似的值太`c:\Program Files (x86)\Java\jre1.7`

* `PATH`-應包含下列路徑的 hello:
  
  * `JAVA_HOME`（或 hello 相等路徑）

  * `JAVA_HOME\bin`（或 hello 相等路徑）

  * hello Maven 安裝所在的目錄

## <a name="create-a-maven-project"></a>建立 Maven 專案

1. 從終端機工作階段或開發環境中的命令列中，變更您想要 toostore 這個專案的目錄 toohello 位置。

2. 使用 hello`mvn`命令，它會隨 Maven，toogenerate hello scaffolding hello 專案。

   ```bash
   mvn archetype:generate -DgroupId=org.apache.hadoop.examples -DartifactId=wordcountjava -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```

    > [!NOTE]
    > 如果您使用 PowerShell，您必須將 hello`-D`雙引號括住的參數。
    >
    > `mvn archetype:generate "-DgroupId=org.apache.hadoop.examples" "-DartifactId=wordcountjava" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    此命令會指定 hello hello 名稱建立目錄`artifactID`參數 (**wordcountjava**在此範例中。)此目錄包含下列項目 hello:

   * `pom.xml`-hello[專案物件模型 (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) ，其中包含的資訊和使用 toobuild hello 專案組態詳細資料。

   * `src`-包含 hello 應用程式的 hello 目錄。

3. 刪除 hello`src/test/java/org/apache/hadoop/examples/apptest.java`檔案。 此範例不會使用此方法。

## <a name="add-dependencies"></a>新增相依性

1. 編輯 hello`pom.xml`檔案，然後加入下列 hello 內文字的 hello `<dependencies>` > 一節：
   
   ```xml
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-mapreduce-examples</artifactId>
        <version>2.7.3</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-mapreduce-client-common</artifactId>
        <version>2.7.3</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-common</artifactId>
        <version>2.7.3</version>
        <scope>provided</scope>
    </dependency>
   ```

    這會定義含有特定版本 (列於&lt;version\> 內) 的必要程式庫 (列於 &lt;artifactId\> 內)。 在編譯時期，這些相依性下載 hello 預設 Maven 儲存機制。 您可以使用 hello [Maven 儲存機制搜尋](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar)tooview 更多。
   
    hello`<scope>provided</scope>`告訴 Maven 這些相依性不應封裝 hello 應用程式時，依照 hello HDInsight 叢集，在執行階段所提供。

    > [!IMPORTANT]
    > 使用 hello 版本應與 Hadoop 叢集上有 hello 版本相符。 如需有關版本的詳細資訊，請參閱 hello [HDInsight 的元件版本控制](hdinsight-component-versioning.md)文件。

2. 新增下列 toohello hello`pom.xml`檔案。 此文字必須在 hello 內`<project>...</project>`標記 hello 檔案中，例如之間`</dependencies>`和`</project>`。

   ```xml
    <build>
        <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
            <transformers>
                <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer">
                </transformer>
            </transformers>
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
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.6.1</version>
            <configuration>
            <source>1.8</source>
            <target>1.8</target>
            </configuration>
        </plugin>
        </plugins>
    </build>
   ```

    hello 第一個外掛程式會設定 hello [Maven 陰影外掛程式](http://maven.apache.org/plugins/maven-shade-plugin/)，它會使用的 toobuild uberjar （有時稱為 fatjar），其中包含 hello 應用程式所需的相依性。 它也可以避免重複的 hello jar 封裝中可能會造成問題，在某些系統上的授權。

    hello 第二個外掛程式會設定 hello 目標 Java 版本。

    > [!NOTE]
    > HDInsight 3.4 和先前版本會使用 Java 7。 HDInsight 3.5 和更新版本會使用 Java 8。

3. 儲存 hello`pom.xml`檔案。

## <a name="create-hello-mapreduce-application"></a>建立 hello MapReduce 應用程式

1. 移 toohello`wordcountjava/src/main/java/org/apache/hadoop/examples`目錄和重新命名的 hello`App.java`檔案太`WordCount.java`。

2. 開啟 hello`WordCount.java`檔案文字編輯器中，然後以下列文字的 hello 取代 hello 內容：
   
    ```java
    package org.apache.hadoop.examples;

    import java.io.IOException;
    import java.util.StringTokenizer;
    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.fs.Path;
    import org.apache.hadoop.io.IntWritable;
    import org.apache.hadoop.io.Text;
    import org.apache.hadoop.mapreduce.Job;
    import org.apache.hadoop.mapreduce.Mapper;
    import org.apache.hadoop.mapreduce.Reducer;
    import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
    import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
    import org.apache.hadoop.util.GenericOptionsParser;

    public class WordCount {

        public static class TokenizerMapper
            extends Mapper<Object, Text, Text, IntWritable>{

        private final static IntWritable one = new IntWritable(1);
        private Text word = new Text();

        public void map(Object key, Text value, Context context
                        ) throws IOException, InterruptedException {
            StringTokenizer itr = new StringTokenizer(value.toString());
            while (itr.hasMoreTokens()) {
            word.set(itr.nextToken());
            context.write(word, one);
            }
        }
    }

    public static class IntSumReducer
            extends Reducer<Text,IntWritable,Text,IntWritable> {
        private IntWritable result = new IntWritable();

        public void reduce(Text key, Iterable<IntWritable> values,
                            Context context
                            ) throws IOException, InterruptedException {
            int sum = 0;
            for (IntWritable val : values) {
            sum += val.get();
            }
            result.set(sum);
            context.write(key, result);
        }
    }

    public static void main(String[] args) throws Exception {
        Configuration conf = new Configuration();
        String[] otherArgs = new GenericOptionsParser(conf, args).getRemainingArgs();
        if (otherArgs.length != 2) {
            System.err.println("Usage: wordcount <in> <out>");
            System.exit(2);
        }
        Job job = new Job(conf, "word count");
        job.setJarByClass(WordCount.class);
        job.setMapperClass(TokenizerMapper.class);
        job.setCombinerClass(IntSumReducer.class);
        job.setReducerClass(IntSumReducer.class);
        job.setOutputKeyClass(Text.class);
        job.setOutputValueClass(IntWritable.class);
        FileInputFormat.addInputPath(job, new Path(otherArgs[0]));
        FileOutputFormat.setOutputPath(job, new Path(otherArgs[1]));
        System.exit(job.waitForCompletion(true) ? 0 : 1);
        }
    }
    ```
   
    請注意 hello package name 是`org.apache.hadoop.examples`hello 類別名稱，且`WordCount`。 當您送出 hello MapReduce 工作，您可以使用這些名稱。

3. 儲存 hello 檔案。

## <a name="build-hello-application"></a>建置 hello 應用程式

1. 變更 toohello`wordcountjava`目錄中，如果您已不存在。

2. 使用下列命令 toobuild JAR 檔案包含 hello 應用程式的 hello:

   ```
   mvn clean package
   ```

    此命令會清除任何先前的組建成品，會下載任何相依性，有尚未安裝，然後建置和封裝 hello 應用程式。

3. 一旦 hello 命令完成時，hello`wordcountjava/target`目錄包含名為`wordcountjava-1.0-SNAPSHOT.jar`。
   
   > [!NOTE]
   > hello`wordcountjava-1.0-SNAPSHOT.jar`檔案 uberjar，其中包含不只 hello WordCount 作業，但是 hello 工作的相依性也需要在執行階段。

## <a id="upload"></a>上傳 hello jar

使用下列命令 tooupload hello jar 檔案 toohello HDInsight 叢集前端節點的 hello:

   ```bash
   scp target/wordcountjava-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
   ```

    Replace __USERNAME__ with your SSH user name for hello cluster. Replace __CLUSTERNAME__ with hello HDInsight cluster name.

此命令會將 hello 檔案從 hello 本機系統 toohello 前端節點。 如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

## <a name="run"></a>在 Hadoop 上執行 hello MapReduce 工作

1. 連接使用 SSH tooHDInsight。 如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

2. 從 hello SSH 工作階段，使用下列命令 toorun hello MapReduce 應用程式的 hello:
   
   ```bash
   yarn jar wordcountjava-1.0-SNAPSHOT.jar org.apache.hadoop.examples.WordCount /example/data/gutenberg/davinci.txt /example/data/wordcountout
   ```
   
    此命令啟動 hello WordCount MapReduce 應用程式。 hello 輸入的檔是`/example/data/gutenberg/davinci.txt`，hello 輸出目錄，且`/example/data/wordcountout`。 Hello 輸入的檔和輸出是預存的 toohello hello 叢集的預設儲存體。

3. Hello 作業完成之後，請使用下列命令 tooview hello 結果 hello:
   
   ```bash
   hdfs dfs -cat /example/data/wordcountout/*
   ```

    您應該與下列文字值類似 toohello 會收到一份單字的計數：
   
        zeal    1
        zelus   1
        zenith  2

## <a id="nextsteps"></a>接續步驟

在本文件中，您已經學會如何 toodevelop Java MapReduce 工作。 請參閱下列文件與 HDInsight 其他方式 toowork hello。

* [搭配 HDInsight 使用 Hivet][hdinsight-use-hive]
* [搭配 HDInsight 使用 Pig][hdinsight-use-pig]
* [〈搭配 HDInsight 使用 MapReduce〉](hdinsight-use-mapreduce.md)

如需詳細資訊，請參閱 hello [Java 開發人員中心](https://azure.microsoft.com/develop/java/)。

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-ODBC]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md

[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md

[powershell-PSCredential]: http://social.technet.microsoft.com/wiki/contents/articles/4546.working-with-passwords-secure-strings-and-credentials-in-windows-powershell.aspx

