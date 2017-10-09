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
# <a name="develop-java-mapreduce-programs-for-hadoop-on-hdinsight"></a><span data-ttu-id="c7dc4-103">在 HDInsight 上開發 Hadoop 的 Java MapReduce 程式</span><span class="sxs-lookup"><span data-stu-id="c7dc4-103">Develop Java MapReduce programs for Hadoop on HDInsight</span></span>

<span data-ttu-id="c7dc4-104">深入了解如何 toouse Apache Maven Java 為基礎的 toocreate MapReduce 應用程式，然後加以執行的 Hadoop Azure HDInsight 上。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-104">Learn how toouse Apache Maven toocreate a Java-based MapReduce application, then run it with Hadoop on Azure HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="c7dc4-105">此範例最近已在 HDInsight 3.6 上測試過。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-105">This example was most recently tested on HDInsight 3.6.</span></span>

## <span data-ttu-id="c7dc4-106"><a name="prerequisites"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="c7dc4-106"><a name="prerequisites"></a>Prerequisites</span></span>

* <span data-ttu-id="c7dc4-107">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 或更新版本 (或同等功能版本，例如 OpenJDK)。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-107">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="c7dc4-108">HDInsight 版本 3.4 和先前版本會使用 Java 7。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-108">HDInsight versions 3.4 and earlier use Java 7.</span></span> <span data-ttu-id="c7dc4-109">HDInsight 3.5 和更新版本會使用 Java 8。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-109">HDInsight 3.5 and greater uses Java 8.</span></span>

* [<span data-ttu-id="c7dc4-110">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="c7dc4-110">Apache Maven</span></span>](http://maven.apache.org/)

## <a name="configure-development-environment"></a><span data-ttu-id="c7dc4-111">設定開發環境</span><span class="sxs-lookup"><span data-stu-id="c7dc4-111">Configure development environment</span></span>

<span data-ttu-id="c7dc4-112">hello 下列環境變數設定 Java 和 hello JDK 安裝時。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-112">hello following environment variables may be set when you install Java and hello JDK.</span></span> <span data-ttu-id="c7dc4-113">不過，您應該檢查其存在且包含您系統的 hello 正確值。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-113">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="c7dc4-114">`JAVA_HOME`-應該指向 toohello hello Java runtime environment (JRE) 安裝所在的目錄。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-114">`JAVA_HOME` - should point toohello directory where hello Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="c7dc4-115">例如，在 OS X、 Unix 或 Linux 系統上，就不應有類似的值太`/usr/lib/jvm/java-7-oracle`。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-115">For example, on an OS X, Unix or Linux system, it should have a value similar too`/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="c7dc4-116">在 Windows 中，就會類似的值太`c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="c7dc4-116">In Windows, it would have a value similar too`c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="c7dc4-117">`PATH`-應包含下列路徑的 hello:</span><span class="sxs-lookup"><span data-stu-id="c7dc4-117">`PATH` - should contain hello following paths:</span></span>
  
  * <span data-ttu-id="c7dc4-118">`JAVA_HOME`（或 hello 相等路徑）</span><span class="sxs-lookup"><span data-stu-id="c7dc4-118">`JAVA_HOME` (or hello equivalent path)</span></span>

  * <span data-ttu-id="c7dc4-119">`JAVA_HOME\bin`（或 hello 相等路徑）</span><span class="sxs-lookup"><span data-stu-id="c7dc4-119">`JAVA_HOME\bin` (or hello equivalent path)</span></span>

  * <span data-ttu-id="c7dc4-120">hello Maven 安裝所在的目錄</span><span class="sxs-lookup"><span data-stu-id="c7dc4-120">hello directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="c7dc4-121">建立 Maven 專案</span><span class="sxs-lookup"><span data-stu-id="c7dc4-121">Create a Maven project</span></span>

1. <span data-ttu-id="c7dc4-122">從終端機工作階段或開發環境中的命令列中，變更您想要 toostore 這個專案的目錄 toohello 位置。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-122">From a terminal session, or command line in your development environment, change directories toohello location you want toostore this project.</span></span>

2. <span data-ttu-id="c7dc4-123">使用 hello`mvn`命令，它會隨 Maven，toogenerate hello scaffolding hello 專案。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-123">Use hello `mvn` command, which is installed with Maven, toogenerate hello scaffolding for hello project.</span></span>

   ```bash
   mvn archetype:generate -DgroupId=org.apache.hadoop.examples -DartifactId=wordcountjava -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```

    > [!NOTE]
    > <span data-ttu-id="c7dc4-124">如果您使用 PowerShell，您必須將 hello`-D`雙引號括住的參數。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-124">If you are using PowerShell, you must enclose hello `-D` parameters in double quotes.</span></span>
    >
    > `mvn archetype:generate "-DgroupId=org.apache.hadoop.examples" "-DartifactId=wordcountjava" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    <span data-ttu-id="c7dc4-125">此命令會指定 hello hello 名稱建立目錄`artifactID`參數 (**wordcountjava**在此範例中。)此目錄包含下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="c7dc4-125">This command creates a directory with hello name specified by hello `artifactID` parameter (**wordcountjava** in this example.) This directory contains hello following items:</span></span>

   * <span data-ttu-id="c7dc4-126">`pom.xml`-hello[專案物件模型 (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) ，其中包含的資訊和使用 toobuild hello 專案組態詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-126">`pom.xml` - hello [Project Object Model (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) that contains information and configuration details used toobuild hello project.</span></span>

   * <span data-ttu-id="c7dc4-127">`src`-包含 hello 應用程式的 hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-127">`src` - hello directory that contains hello application.</span></span>

3. <span data-ttu-id="c7dc4-128">刪除 hello`src/test/java/org/apache/hadoop/examples/apptest.java`檔案。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-128">Delete hello `src/test/java/org/apache/hadoop/examples/apptest.java` file.</span></span> <span data-ttu-id="c7dc4-129">此範例不會使用此方法。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-129">It is not used in this example.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="c7dc4-130">新增相依性</span><span class="sxs-lookup"><span data-stu-id="c7dc4-130">Add dependencies</span></span>

1. <span data-ttu-id="c7dc4-131">編輯 hello`pom.xml`檔案，然後加入下列 hello 內文字的 hello `<dependencies>` > 一節：</span><span class="sxs-lookup"><span data-stu-id="c7dc4-131">Edit hello `pom.xml` file and add hello following text inside hello `<dependencies>` section:</span></span>
   
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

    <span data-ttu-id="c7dc4-132">這會定義含有特定版本 (列於&lt;version\> 內) 的必要程式庫 (列於 &lt;artifactId\> 內)。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-132">This defines required libraries (listed within &lt;artifactId\>) with a specific version (listed within &lt;version\>).</span></span> <span data-ttu-id="c7dc4-133">在編譯時期，這些相依性下載 hello 預設 Maven 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-133">At compile time, these dependencies are downloaded from hello default Maven repository.</span></span> <span data-ttu-id="c7dc4-134">您可以使用 hello [Maven 儲存機制搜尋](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar)tooview 更多。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-134">You can use hello [Maven repository search](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) tooview more.</span></span>
   
    <span data-ttu-id="c7dc4-135">hello`<scope>provided</scope>`告訴 Maven 這些相依性不應封裝 hello 應用程式時，依照 hello HDInsight 叢集，在執行階段所提供。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-135">hello `<scope>provided</scope>` tells Maven that these dependencies should not be packaged with hello application, as they are provided by hello HDInsight cluster at run-time.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="c7dc4-136">使用 hello 版本應與 Hadoop 叢集上有 hello 版本相符。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-136">hello version used should match hello version of Hadoop present on your cluster.</span></span> <span data-ttu-id="c7dc4-137">如需有關版本的詳細資訊，請參閱 hello [HDInsight 的元件版本控制](hdinsight-component-versioning.md)文件。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-137">For more information on versions, see hello [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

2. <span data-ttu-id="c7dc4-138">新增下列 toohello hello`pom.xml`檔案。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-138">Add hello following toohello `pom.xml` file.</span></span> <span data-ttu-id="c7dc4-139">此文字必須在 hello 內`<project>...</project>`標記 hello 檔案中，例如之間`</dependencies>`和`</project>`。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-139">This text must be inside hello `<project>...</project>` tags in hello file; for example, between `</dependencies>` and `</project>`.</span></span>

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

    <span data-ttu-id="c7dc4-140">hello 第一個外掛程式會設定 hello [Maven 陰影外掛程式](http://maven.apache.org/plugins/maven-shade-plugin/)，它會使用的 toobuild uberjar （有時稱為 fatjar），其中包含 hello 應用程式所需的相依性。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-140">hello first plugin configures hello [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/), which is used toobuild an uberjar (sometimes called a fatjar), which contains dependencies required by hello application.</span></span> <span data-ttu-id="c7dc4-141">它也可以避免重複的 hello jar 封裝中可能會造成問題，在某些系統上的授權。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-141">It also prevents duplication of licenses within hello jar package, which can cause problems on some systems.</span></span>

    <span data-ttu-id="c7dc4-142">hello 第二個外掛程式會設定 hello 目標 Java 版本。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-142">hello second plugin configures hello target Java version.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c7dc4-143">HDInsight 3.4 和先前版本會使用 Java 7。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-143">HDInsight 3.4 and earlier use Java 7.</span></span> <span data-ttu-id="c7dc4-144">HDInsight 3.5 和更新版本會使用 Java 8。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-144">HDInsight 3.5 and greater uses Java 8.</span></span>

3. <span data-ttu-id="c7dc4-145">儲存 hello`pom.xml`檔案。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-145">Save hello `pom.xml` file.</span></span>

## <a name="create-hello-mapreduce-application"></a><span data-ttu-id="c7dc4-146">建立 hello MapReduce 應用程式</span><span class="sxs-lookup"><span data-stu-id="c7dc4-146">Create hello MapReduce application</span></span>

1. <span data-ttu-id="c7dc4-147">移 toohello`wordcountjava/src/main/java/org/apache/hadoop/examples`目錄和重新命名的 hello`App.java`檔案太`WordCount.java`。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-147">Go toohello `wordcountjava/src/main/java/org/apache/hadoop/examples` directory and rename hello `App.java` file too`WordCount.java`.</span></span>

2. <span data-ttu-id="c7dc4-148">開啟 hello`WordCount.java`檔案文字編輯器中，然後以下列文字的 hello 取代 hello 內容：</span><span class="sxs-lookup"><span data-stu-id="c7dc4-148">Open hello `WordCount.java` file in a text editor and replace hello contents with hello following text:</span></span>
   
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
   
    <span data-ttu-id="c7dc4-149">請注意 hello package name 是`org.apache.hadoop.examples`hello 類別名稱，且`WordCount`。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-149">Notice hello package name is `org.apache.hadoop.examples` and hello class name is `WordCount`.</span></span> <span data-ttu-id="c7dc4-150">當您送出 hello MapReduce 工作，您可以使用這些名稱。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-150">You use these names when you submit hello MapReduce job.</span></span>

3. <span data-ttu-id="c7dc4-151">儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-151">Save hello file.</span></span>

## <a name="build-hello-application"></a><span data-ttu-id="c7dc4-152">建置 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="c7dc4-152">Build hello application</span></span>

1. <span data-ttu-id="c7dc4-153">變更 toohello`wordcountjava`目錄中，如果您已不存在。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-153">Change toohello `wordcountjava` directory, if you are not already there.</span></span>

2. <span data-ttu-id="c7dc4-154">使用下列命令 toobuild JAR 檔案包含 hello 應用程式的 hello:</span><span class="sxs-lookup"><span data-stu-id="c7dc4-154">Use hello following command toobuild a JAR file containing hello application:</span></span>

   ```
   mvn clean package
   ```

    <span data-ttu-id="c7dc4-155">此命令會清除任何先前的組建成品，會下載任何相依性，有尚未安裝，然後建置和封裝 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-155">This command cleans any previous build artifacts, downloads any dependencies that have not already been installed, and then builds and package hello application.</span></span>

3. <span data-ttu-id="c7dc4-156">一旦 hello 命令完成時，hello`wordcountjava/target`目錄包含名為`wordcountjava-1.0-SNAPSHOT.jar`。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-156">Once hello command finishes, hello `wordcountjava/target` directory contains a file named `wordcountjava-1.0-SNAPSHOT.jar`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c7dc4-157">hello`wordcountjava-1.0-SNAPSHOT.jar`檔案 uberjar，其中包含不只 hello WordCount 作業，但是 hello 工作的相依性也需要在執行階段。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-157">hello `wordcountjava-1.0-SNAPSHOT.jar` file is an uberjar, which contains not only hello WordCount job, but also dependencies that hello job requires at runtime.</span></span>

## <span data-ttu-id="c7dc4-158"><a id="upload"></a>上傳 hello jar</span><span class="sxs-lookup"><span data-stu-id="c7dc4-158"><a id="upload"></a>Upload hello jar</span></span>

<span data-ttu-id="c7dc4-159">使用下列命令 tooupload hello jar 檔案 toohello HDInsight 叢集前端節點的 hello:</span><span class="sxs-lookup"><span data-stu-id="c7dc4-159">Use hello following command tooupload hello jar file toohello HDInsight headnode:</span></span>

   ```bash
   scp target/wordcountjava-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
   ```

    Replace __USERNAME__ with your SSH user name for hello cluster. Replace __CLUSTERNAME__ with hello HDInsight cluster name.

<span data-ttu-id="c7dc4-160">此命令會將 hello 檔案從 hello 本機系統 toohello 前端節點。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-160">This command copies hello files from hello local system toohello head node.</span></span> <span data-ttu-id="c7dc4-161">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-161">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="c7dc4-162"><a name="run"></a>在 Hadoop 上執行 hello MapReduce 工作</span><span class="sxs-lookup"><span data-stu-id="c7dc4-162"><a name="run"></a>Run hello MapReduce job on Hadoop</span></span>

1. <span data-ttu-id="c7dc4-163">連接使用 SSH tooHDInsight。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-163">Connect tooHDInsight using SSH.</span></span> <span data-ttu-id="c7dc4-164">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-164">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="c7dc4-165">從 hello SSH 工作階段，使用下列命令 toorun hello MapReduce 應用程式的 hello:</span><span class="sxs-lookup"><span data-stu-id="c7dc4-165">From hello SSH session, use hello following command toorun hello MapReduce application:</span></span>
   
   ```bash
   yarn jar wordcountjava-1.0-SNAPSHOT.jar org.apache.hadoop.examples.WordCount /example/data/gutenberg/davinci.txt /example/data/wordcountout
   ```
   
    <span data-ttu-id="c7dc4-166">此命令啟動 hello WordCount MapReduce 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-166">This command starts hello WordCount MapReduce application.</span></span> <span data-ttu-id="c7dc4-167">hello 輸入的檔是`/example/data/gutenberg/davinci.txt`，hello 輸出目錄，且`/example/data/wordcountout`。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-167">hello input file is `/example/data/gutenberg/davinci.txt`, and hello output directory is `/example/data/wordcountout`.</span></span> <span data-ttu-id="c7dc4-168">Hello 輸入的檔和輸出是預存的 toohello hello 叢集的預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-168">Both hello input file and output are stored toohello default storage for hello cluster.</span></span>

3. <span data-ttu-id="c7dc4-169">Hello 作業完成之後，請使用下列命令 tooview hello 結果 hello:</span><span class="sxs-lookup"><span data-stu-id="c7dc4-169">Once hello job completes, use hello following command tooview hello results:</span></span>
   
   ```bash
   hdfs dfs -cat /example/data/wordcountout/*
   ```

    <span data-ttu-id="c7dc4-170">您應該與下列文字值類似 toohello 會收到一份單字的計數：</span><span class="sxs-lookup"><span data-stu-id="c7dc4-170">You should receive a list of words and counts, with values similar toohello following text:</span></span>
   
        zeal    1
        zelus   1
        zenith  2

## <span data-ttu-id="c7dc4-171"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="c7dc4-171"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="c7dc4-172">在本文件中，您已經學會如何 toodevelop Java MapReduce 工作。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-172">In this document, you have learned how toodevelop a Java MapReduce job.</span></span> <span data-ttu-id="c7dc4-173">請參閱下列文件與 HDInsight 其他方式 toowork hello。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-173">See hello following documents for other ways toowork with HDInsight.</span></span>

* <span data-ttu-id="c7dc4-174">[搭配 HDInsight 使用 Hivet][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="c7dc4-174">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="c7dc4-175">[搭配 HDInsight 使用 Pig][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="c7dc4-175">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* [<span data-ttu-id="c7dc4-176">〈搭配 HDInsight 使用 MapReduce〉</span><span class="sxs-lookup"><span data-stu-id="c7dc4-176">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="c7dc4-177">如需詳細資訊，請參閱 hello [Java 開發人員中心](https://azure.microsoft.com/develop/java/)。</span><span class="sxs-lookup"><span data-stu-id="c7dc4-177">For more information, see also hello [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

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

