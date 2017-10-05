---
title: "建立適用於 Hadoop 的 Java MapReduce - Azure HDInsight | Microsoft Docs"
description: "了解如何使用 Apache Maven 來建立以 Java 為基礎的 MapReduce 應用程式，然後在 Azure HDInsight 上使用 Hadoop 來加以執行。"
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
ms.openlocfilehash: 11d63f22204eb2acb530378f53ac72f16a35a4f2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="develop-java-mapreduce-programs-for-hadoop-on-hdinsight"></a><span data-ttu-id="21f86-103">在 HDInsight 上開發 Hadoop 的 Java MapReduce 程式</span><span class="sxs-lookup"><span data-stu-id="21f86-103">Develop Java MapReduce programs for Hadoop on HDInsight</span></span>

<span data-ttu-id="21f86-104">了解如何使用 Apache Maven 來建立以 Java 為基礎的 MapReduce 應用程式，然後在 Azure HDInsight 上使用 Hadoop 來加以執行。</span><span class="sxs-lookup"><span data-stu-id="21f86-104">Learn how to use Apache Maven to create a Java-based MapReduce application, then run it with Hadoop on Azure HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="21f86-105">此範例最近已在 HDInsight 3.6 上測試過。</span><span class="sxs-lookup"><span data-stu-id="21f86-105">This example was most recently tested on HDInsight 3.6.</span></span>

## <span data-ttu-id="21f86-106"><a name="prerequisites"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="21f86-106"><a name="prerequisites"></a>Prerequisites</span></span>

* <span data-ttu-id="21f86-107">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 或更新版本 (或同等功能版本，例如 OpenJDK)。</span><span class="sxs-lookup"><span data-stu-id="21f86-107">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="21f86-108">HDInsight 版本 3.4 和先前版本會使用 Java 7。</span><span class="sxs-lookup"><span data-stu-id="21f86-108">HDInsight versions 3.4 and earlier use Java 7.</span></span> <span data-ttu-id="21f86-109">HDInsight 3.5 和更新版本會使用 Java 8。</span><span class="sxs-lookup"><span data-stu-id="21f86-109">HDInsight 3.5 and greater uses Java 8.</span></span>

* [<span data-ttu-id="21f86-110">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="21f86-110">Apache Maven</span></span>](http://maven.apache.org/)

## <a name="configure-development-environment"></a><span data-ttu-id="21f86-111">設定開發環境</span><span class="sxs-lookup"><span data-stu-id="21f86-111">Configure development environment</span></span>

<span data-ttu-id="21f86-112">當您安裝 Java 和 JDK 時可能會設定下列環境變數。</span><span class="sxs-lookup"><span data-stu-id="21f86-112">The following environment variables may be set when you install Java and the JDK.</span></span> <span data-ttu-id="21f86-113">不過，您應該檢查它們是否存在，以及它們是否包含您系統的正確值。</span><span class="sxs-lookup"><span data-stu-id="21f86-113">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="21f86-114">`JAVA_HOME` - 應該指向已安裝 Java 執行階段環境 (JRE) 的目錄。</span><span class="sxs-lookup"><span data-stu-id="21f86-114">`JAVA_HOME` - should point to the directory where the Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="21f86-115">例如，在 OS X、Unix 或 Linux 系統上，它的值應該類似 `/usr/lib/jvm/java-7-oracle`。</span><span class="sxs-lookup"><span data-stu-id="21f86-115">For example, on an OS X, Unix or Linux system, it should have a value similar to `/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="21f86-116">在 Windows 中，它的值應該類似 `c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="21f86-116">In Windows, it would have a value similar to `c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="21f86-117">`PATH` - 應該包含下列路徑：</span><span class="sxs-lookup"><span data-stu-id="21f86-117">`PATH` - should contain the following paths:</span></span>
  
  * <span data-ttu-id="21f86-118">`JAVA_HOME` (或對等的路徑)</span><span class="sxs-lookup"><span data-stu-id="21f86-118">`JAVA_HOME` (or the equivalent path)</span></span>

  * <span data-ttu-id="21f86-119">`JAVA_HOME\bin` (或對等的路徑)</span><span class="sxs-lookup"><span data-stu-id="21f86-119">`JAVA_HOME\bin` (or the equivalent path)</span></span>

  * <span data-ttu-id="21f86-120">已安裝 Maven 的目錄</span><span class="sxs-lookup"><span data-stu-id="21f86-120">The directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="21f86-121">建立 Maven 專案</span><span class="sxs-lookup"><span data-stu-id="21f86-121">Create a Maven project</span></span>

1. <span data-ttu-id="21f86-122">從終端機工作階段，或開發環境的命令列中，將目錄變更為您想要儲存此專案的位置。</span><span class="sxs-lookup"><span data-stu-id="21f86-122">From a terminal session, or command line in your development environment, change directories to the location you want to store this project.</span></span>

2. <span data-ttu-id="21f86-123">使用隨 Maven 一起安裝的 `mvn` 命令來產生專案的結構。</span><span class="sxs-lookup"><span data-stu-id="21f86-123">Use the `mvn` command, which is installed with Maven, to generate the scaffolding for the project.</span></span>

   ```bash
   mvn archetype:generate -DgroupId=org.apache.hadoop.examples -DartifactId=wordcountjava -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```

    > [!NOTE]
    > <span data-ttu-id="21f86-124">如果您使用 PowerShell，則必須將 `-D` 參數放置在雙引號內。</span><span class="sxs-lookup"><span data-stu-id="21f86-124">If you are using PowerShell, you must enclose the `-D` parameters in double quotes.</span></span>
    >
    > `mvn archetype:generate "-DgroupId=org.apache.hadoop.examples" "-DartifactId=wordcountjava" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    <span data-ttu-id="21f86-125">此命令會使用 `artifactID` 參數所指定的名稱 (此範例中為 **wordcountjava**) 來建立目錄。此目錄包含下列項目：</span><span class="sxs-lookup"><span data-stu-id="21f86-125">This command creates a directory with the name specified by the `artifactID` parameter (**wordcountjava** in this example.) This directory contains the following items:</span></span>

   * <span data-ttu-id="21f86-126">`pom.xml` - [專案物件模型 (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)，包含用來建置專案的資訊和組態詳細資料。</span><span class="sxs-lookup"><span data-stu-id="21f86-126">`pom.xml` - The [Project Object Model (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) that contains information and configuration details used to build the project.</span></span>

   * <span data-ttu-id="21f86-127">`src` - 包含應用程式的目錄。</span><span class="sxs-lookup"><span data-stu-id="21f86-127">`src` - The directory that contains the application.</span></span>

3. <span data-ttu-id="21f86-128">刪除 `src/test/java/org/apache/hadoop/examples/apptest.java` 檔案。</span><span class="sxs-lookup"><span data-stu-id="21f86-128">Delete the `src/test/java/org/apache/hadoop/examples/apptest.java` file.</span></span> <span data-ttu-id="21f86-129">此範例不會使用此方法。</span><span class="sxs-lookup"><span data-stu-id="21f86-129">It is not used in this example.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="21f86-130">新增相依性</span><span class="sxs-lookup"><span data-stu-id="21f86-130">Add dependencies</span></span>

1. <span data-ttu-id="21f86-131">編輯 `pom.xml` 檔案，並在 `<dependencies>` 區段內新增下列文字：</span><span class="sxs-lookup"><span data-stu-id="21f86-131">Edit the `pom.xml` file and add the following text inside the `<dependencies>` section:</span></span>
   
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

    <span data-ttu-id="21f86-132">這會定義含有特定版本 (列於&lt;version\> 內) 的必要程式庫 (列於 &lt;artifactId\> 內)。</span><span class="sxs-lookup"><span data-stu-id="21f86-132">This defines required libraries (listed within &lt;artifactId\>) with a specific version (listed within &lt;version\>).</span></span> <span data-ttu-id="21f86-133">在編譯期間，會從預設的 Maven 儲存機制下載這些相依性。</span><span class="sxs-lookup"><span data-stu-id="21f86-133">At compile time, these dependencies are downloaded from the default Maven repository.</span></span> <span data-ttu-id="21f86-134">您可以使用 [Maven 儲存機制搜尋](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) (英文) 檢視詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="21f86-134">You can use the [Maven repository search](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) to view more.</span></span>
   
    <span data-ttu-id="21f86-135">`<scope>provided</scope>` 會告訴 Maven 這些相依性不應該和應用程式一起封裝，因為 HDInsight 叢集會在執行階段提供這些相依性。</span><span class="sxs-lookup"><span data-stu-id="21f86-135">The `<scope>provided</scope>` tells Maven that these dependencies should not be packaged with the application, as they are provided by the HDInsight cluster at run-time.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="21f86-136">使用的版本應該符合您叢集上的 Hadoop 版本。</span><span class="sxs-lookup"><span data-stu-id="21f86-136">The version used should match the version of Hadoop present on your cluster.</span></span> <span data-ttu-id="21f86-137">如需有關版本的詳細資訊，請參閱 [HDInsight 元件版本設定](hdinsight-component-versioning.md)文件。</span><span class="sxs-lookup"><span data-stu-id="21f86-137">For more information on versions, see the [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

2. <span data-ttu-id="21f86-138">將下列項目新增至 `pom.xml` 檔案。</span><span class="sxs-lookup"><span data-stu-id="21f86-138">Add the following to the `pom.xml` file.</span></span> <span data-ttu-id="21f86-139">此文字必須位於檔案中的 `<project>...</project>` 標籤內，例如在 `</dependencies>` 和 `</project>` 之間。</span><span class="sxs-lookup"><span data-stu-id="21f86-139">This text must be inside the `<project>...</project>` tags in the file; for example, between `</dependencies>` and `</project>`.</span></span>

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

    <span data-ttu-id="21f86-140">第一個外掛程式會設定用於建置 uberjar (有時稱為 fatjar) 的 [Maven Shade 外掛程式](http://maven.apache.org/plugins/maven-shade-plugin/)，uberjar 內含應用程式需要的相依性。</span><span class="sxs-lookup"><span data-stu-id="21f86-140">The first plugin configures the [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/), which is used to build an uberjar (sometimes called a fatjar), which contains dependencies required by the application.</span></span> <span data-ttu-id="21f86-141">這麼做也可以防止 jar 封裝中具有重複的授權，以免在某些系統中造成問題。</span><span class="sxs-lookup"><span data-stu-id="21f86-141">It also prevents duplication of licenses within the jar package, which can cause problems on some systems.</span></span>

    <span data-ttu-id="21f86-142">第二個外掛程式會設定目標 Java 版本。</span><span class="sxs-lookup"><span data-stu-id="21f86-142">The second plugin configures the target Java version.</span></span>

    > [!NOTE]
    > <span data-ttu-id="21f86-143">HDInsight 3.4 和先前版本會使用 Java 7。</span><span class="sxs-lookup"><span data-stu-id="21f86-143">HDInsight 3.4 and earlier use Java 7.</span></span> <span data-ttu-id="21f86-144">HDInsight 3.5 和更新版本會使用 Java 8。</span><span class="sxs-lookup"><span data-stu-id="21f86-144">HDInsight 3.5 and greater uses Java 8.</span></span>

3. <span data-ttu-id="21f86-145">儲存 `pom.xml` 檔案。</span><span class="sxs-lookup"><span data-stu-id="21f86-145">Save the `pom.xml` file.</span></span>

## <a name="create-the-mapreduce-application"></a><span data-ttu-id="21f86-146">建立 MapReduce 應用程式</span><span class="sxs-lookup"><span data-stu-id="21f86-146">Create the MapReduce application</span></span>

1. <span data-ttu-id="21f86-147">移至 `wordcountjava/src/main/java/org/apache/hadoop/examples` 目錄，並將 `App.java` 檔案重新命名為 `WordCount.java`。</span><span class="sxs-lookup"><span data-stu-id="21f86-147">Go to the `wordcountjava/src/main/java/org/apache/hadoop/examples` directory and rename the `App.java` file to `WordCount.java`.</span></span>

2. <span data-ttu-id="21f86-148">在文字編輯器中開啟 `WordCount.java` 檔案，並使用下列文字來取代內容：</span><span class="sxs-lookup"><span data-stu-id="21f86-148">Open the `WordCount.java` file in a text editor and replace the contents with the following text:</span></span>
   
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
   
    <span data-ttu-id="21f86-149">請注意，封裝名稱是 `org.apache.hadoop.examples`，而類別名稱是 `WordCount`。</span><span class="sxs-lookup"><span data-stu-id="21f86-149">Notice the package name is `org.apache.hadoop.examples` and the class name is `WordCount`.</span></span> <span data-ttu-id="21f86-150">提交 MapReduce 作業時會用到這些名稱。</span><span class="sxs-lookup"><span data-stu-id="21f86-150">You use these names when you submit the MapReduce job.</span></span>

3. <span data-ttu-id="21f86-151">儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="21f86-151">Save the file.</span></span>

## <a name="build-the-application"></a><span data-ttu-id="21f86-152">建置應用程式</span><span class="sxs-lookup"><span data-stu-id="21f86-152">Build the application</span></span>

1. <span data-ttu-id="21f86-153">切換至 `wordcountjava` 目錄 (如果您尚未在該目錄中)。</span><span class="sxs-lookup"><span data-stu-id="21f86-153">Change to the `wordcountjava` directory, if you are not already there.</span></span>

2. <span data-ttu-id="21f86-154">使用下列命令來建置含有應用程式的 JAR 檔案：</span><span class="sxs-lookup"><span data-stu-id="21f86-154">Use the following command to build a JAR file containing the application:</span></span>

   ```
   mvn clean package
   ```

    <span data-ttu-id="21f86-155">此命令會清除任何先前的組建構件、下載任何尚未安裝的相依性，然後建置並封裝應用程式。</span><span class="sxs-lookup"><span data-stu-id="21f86-155">This command cleans any previous build artifacts, downloads any dependencies that have not already been installed, and then builds and package the application.</span></span>

3. <span data-ttu-id="21f86-156">一旦命令完成之後，`wordcountjava/target` 目錄就會包含名為 `wordcountjava-1.0-SNAPSHOT.jar` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="21f86-156">Once the command finishes, the `wordcountjava/target` directory contains a file named `wordcountjava-1.0-SNAPSHOT.jar`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="21f86-157">`wordcountjava-1.0-SNAPSHOT.jar` 檔案是一個 uberjar，其中不只含有 WordCount 作業，還有該作業在執行階段所需的相依性。</span><span class="sxs-lookup"><span data-stu-id="21f86-157">The `wordcountjava-1.0-SNAPSHOT.jar` file is an uberjar, which contains not only the WordCount job, but also dependencies that the job requires at runtime.</span></span>

## <span data-ttu-id="21f86-158"><a id="upload"></a>上傳 jar</span><span class="sxs-lookup"><span data-stu-id="21f86-158"><a id="upload"></a>Upload the jar</span></span>

<span data-ttu-id="21f86-159">使用以下命令將 jar 檔案上傳至 HDInsight 前端節點。</span><span class="sxs-lookup"><span data-stu-id="21f86-159">Use the following command to upload the jar file to the HDInsight headnode:</span></span>

   ```bash
   scp target/wordcountjava-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
   ```

    Replace __USERNAME__ with your SSH user name for the cluster. Replace __CLUSTERNAME__ with the HDInsight cluster name.

<span data-ttu-id="21f86-160">此命令會將檔案從本機系統複製到前端節點。</span><span class="sxs-lookup"><span data-stu-id="21f86-160">This command copies the files from the local system to the head node.</span></span> <span data-ttu-id="21f86-161">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="21f86-161">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="21f86-162"><a name="run"></a>在 Hadoop 上執行 MapReduce 作業</span><span class="sxs-lookup"><span data-stu-id="21f86-162"><a name="run"></a>Run the MapReduce job on Hadoop</span></span>

1. <span data-ttu-id="21f86-163">使用 SSH 連線到 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="21f86-163">Connect to HDInsight using SSH.</span></span> <span data-ttu-id="21f86-164">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="21f86-164">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="21f86-165">在 SSH 工作階段中，使用以下命令執行 MapReduce 應用程式：</span><span class="sxs-lookup"><span data-stu-id="21f86-165">From the SSH session, use the following command to run the MapReduce application:</span></span>
   
   ```bash
   yarn jar wordcountjava-1.0-SNAPSHOT.jar org.apache.hadoop.examples.WordCount /example/data/gutenberg/davinci.txt /example/data/wordcountout
   ```
   
    <span data-ttu-id="21f86-166">此命令會啟動 WordCount MapReduce 應用程式。</span><span class="sxs-lookup"><span data-stu-id="21f86-166">This command starts the WordCount MapReduce application.</span></span> <span data-ttu-id="21f86-167">輸入檔案為 `/example/data/gutenberg/davinci.txt`，輸出目錄則為 `/example/data/wordcountout`。</span><span class="sxs-lookup"><span data-stu-id="21f86-167">The input file is `/example/data/gutenberg/davinci.txt`, and the output directory is `/example/data/wordcountout`.</span></span> <span data-ttu-id="21f86-168">輸入檔和輸出都會儲存至叢集的預設儲存體中。</span><span class="sxs-lookup"><span data-stu-id="21f86-168">Both the input file and output are stored to the default storage for the cluster.</span></span>

3. <span data-ttu-id="21f86-169">作業完成之後，請使用以下命令來檢視結果：</span><span class="sxs-lookup"><span data-stu-id="21f86-169">Once the job completes, use the following command to view the results:</span></span>
   
   ```bash
   hdfs dfs -cat /example/data/wordcountout/*
   ```

    <span data-ttu-id="21f86-170">您應該會收到一份單字和計數的清單，其中含有類似下列文字的值：</span><span class="sxs-lookup"><span data-stu-id="21f86-170">You should receive a list of words and counts, with values similar to the following text:</span></span>
   
        zeal    1
        zelus   1
        zenith  2

## <span data-ttu-id="21f86-171"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="21f86-171"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="21f86-172">在本文件中，您已學到如何開發 Java MapReduce 工作。</span><span class="sxs-lookup"><span data-stu-id="21f86-172">In this document, you have learned how to develop a Java MapReduce job.</span></span> <span data-ttu-id="21f86-173">請參閱下列文件，了解其他的 HDInsight 使用方式。</span><span class="sxs-lookup"><span data-stu-id="21f86-173">See the following documents for other ways to work with HDInsight.</span></span>

* <span data-ttu-id="21f86-174">[搭配 HDInsight 使用 Hivet][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="21f86-174">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="21f86-175">[搭配 HDInsight 使用 Pig][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="21f86-175">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* [<span data-ttu-id="21f86-176">〈搭配 HDInsight 使用 MapReduce〉</span><span class="sxs-lookup"><span data-stu-id="21f86-176">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="21f86-177">如需詳細資訊，也請參閱 [Java 開發人員中心](https://azure.microsoft.com/develop/java/)。</span><span class="sxs-lookup"><span data-stu-id="21f86-177">For more information, see also the [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

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

