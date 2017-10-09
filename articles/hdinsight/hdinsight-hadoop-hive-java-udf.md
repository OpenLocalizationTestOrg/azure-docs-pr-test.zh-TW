---
title: "aaaJava 使用者定義函數 (UDF 與 HDInsight 的 Azure 中的登錄區) |Microsoft 文件"
description: "了解如何 toocreate Java 為基礎使用者定義函數 (UDF) 可搭配 Hive。 此範例 UDF 將轉換文字字串 toolowercase 的資料表。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 8d4f8efe-2f01-4a61-8619-651e873c7982
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 392b4cfb73299d2f6c1e8e825a4201b48d501388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-java-udf-with-hive-in-hdinsight"></a><span data-ttu-id="cb69f-104">在 HDInsight 中搭配使用 Java UDF 和 Hive</span><span class="sxs-lookup"><span data-stu-id="cb69f-104">Use a Java UDF with Hive in HDInsight</span></span>

<span data-ttu-id="cb69f-105">了解如何 toocreate Java 為基礎使用者定義函數 (UDF) 可搭配 Hive。</span><span class="sxs-lookup"><span data-stu-id="cb69f-105">Learn how toocreate a Java-based user-defined function (UDF) that works with Hive.</span></span> <span data-ttu-id="cb69f-106">在此範例中的 hello Java UDF 將轉換的文字字串 tooall 小寫字元。</span><span class="sxs-lookup"><span data-stu-id="cb69f-106">hello Java UDF in this example converts a table of text strings tooall-lowercase characters.</span></span>

## <a name="requirements"></a><span data-ttu-id="cb69f-107">需求</span><span class="sxs-lookup"><span data-stu-id="cb69f-107">Requirements</span></span>

* <span data-ttu-id="cb69f-108">HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="cb69f-108">An HDInsight cluster</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="cb69f-109">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="cb69f-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="cb69f-110">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="cb69f-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

    <span data-ttu-id="cb69f-111">本文件中的大部分步驟適用於以 Windows 和 Linux 為基礎的叢集。</span><span class="sxs-lookup"><span data-stu-id="cb69f-111">Most steps in this document work on both Windows- and Linux-based clusters.</span></span> <span data-ttu-id="cb69f-112">不過，hello 步驟 tooupload hello 所編譯的 UDF toohello 叢集並執行它是特定 tooLinux 為基礎的叢集。</span><span class="sxs-lookup"><span data-stu-id="cb69f-112">However, hello steps used tooupload hello compiled UDF toohello cluster and run it are specific tooLinux-based clusters.</span></span> <span data-ttu-id="cb69f-113">可以搭配 windows 叢集的 tooinformation 時，會提供連結。</span><span class="sxs-lookup"><span data-stu-id="cb69f-113">Links are provided tooinformation that can be used with Windows-based clusters.</span></span>

* <span data-ttu-id="cb69f-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 或更新版本 (或同等功能版本，例如 OpenJDK)</span><span class="sxs-lookup"><span data-stu-id="cb69f-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK)</span></span>

* [<span data-ttu-id="cb69f-115">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="cb69f-115">Apache Maven</span></span>](http://maven.apache.org/)

* <span data-ttu-id="cb69f-116">文字編輯器或 Java IDE</span><span class="sxs-lookup"><span data-stu-id="cb69f-116">A text editor or Java IDE</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="cb69f-117">如果您建立 hello Python Windows 用戶端上的檔案，您必須使用 LF 做尾結束編輯器。</span><span class="sxs-lookup"><span data-stu-id="cb69f-117">If you create hello Python files on a Windows client, you must use an editor that uses LF as a line ending.</span></span> <span data-ttu-id="cb69f-118">如果您不確定您的編輯器是使用 LF 或 CRLF，請參閱 hello[疑難排解](#troubleshooting)區段中針對步驟移除 hello CR 字元。</span><span class="sxs-lookup"><span data-stu-id="cb69f-118">If you are not sure whether your editor uses LF or CRLF, see hello [Troubleshooting](#troubleshooting) section for steps on removing hello CR character.</span></span>

## <a name="create-an-example-java-udf"></a><span data-ttu-id="cb69f-119">建立範例 Java UDF</span><span class="sxs-lookup"><span data-stu-id="cb69f-119">Create an example Java UDF</span></span> 

1. <span data-ttu-id="cb69f-120">從命令列使用下列新的 Maven 專案 toocreate hello:</span><span class="sxs-lookup"><span data-stu-id="cb69f-120">From a command line, use hello following toocreate a new Maven project:</span></span>

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=ExampleUDF -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

   > [!NOTE]
   > <span data-ttu-id="cb69f-121">如果您使用 PowerShell，您必須前後放置引號 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="cb69f-121">If you are using PowerShell, you must put quotes around hello parameters.</span></span> <span data-ttu-id="cb69f-122">例如： `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`。</span><span class="sxs-lookup"><span data-stu-id="cb69f-122">For example, `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.</span></span>

    <span data-ttu-id="cb69f-123">此命令會建立一個名為目錄**exampleudf**，其中包含 hello Maven 專案。</span><span class="sxs-lookup"><span data-stu-id="cb69f-123">This command creates a directory named **exampleudf**, which contains hello Maven project.</span></span>

2. <span data-ttu-id="cb69f-124">一旦建立 hello 專案之後，刪除 hello **exampleudf/src/test** hello 專案中建立的目錄。</span><span class="sxs-lookup"><span data-stu-id="cb69f-124">Once hello project has been created, delete hello **exampleudf/src/test** directory that was created as part of hello project.</span></span>

3. <span data-ttu-id="cb69f-125">開啟 hello **exampleudf/pom.xml**，並取代現有的 hello `<dependencies>` hello 下列 XML 項目：</span><span class="sxs-lookup"><span data-stu-id="cb69f-125">Open hello **exampleudf/pom.xml**, and replace hello existing `<dependencies>` entry with hello following XML:</span></span>

    ```xml
    <dependencies>
        <dependency>
            <groupId>org.apache.hadoop</groupId>
            <artifactId>hadoop-client</artifactId>
            <version>2.7.3</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.apache.hive</groupId>
            <artifactId>hive-exec</artifactId>
            <version>1.2.1</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>
    ```

    <span data-ttu-id="cb69f-126">這些項目指定 Hadoop 和 Hive HDInsight 3.5 所隨附的 hello 的版本。</span><span class="sxs-lookup"><span data-stu-id="cb69f-126">These entries specify hello version of Hadoop and Hive included with HDInsight 3.5.</span></span> <span data-ttu-id="cb69f-127">您可以找到有關 hello 版本 Hadoop 和 Hive 與 HDInsight 提供從 hello [HDInsight 的元件版本控制](hdinsight-component-versioning.md)文件。</span><span class="sxs-lookup"><span data-stu-id="cb69f-127">You can find information on hello versions of Hadoop and Hive provided with HDInsight from hello [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

    <span data-ttu-id="cb69f-128">新增`<build>`區段之前 hello `</project>` hello hello 檔結尾行。</span><span class="sxs-lookup"><span data-stu-id="cb69f-128">Add a `<build>` section before hello `</project>` line at hello end of hello file.</span></span> <span data-ttu-id="cb69f-129">這個區段應該包含下列 XML 的 hello:</span><span class="sxs-lookup"><span data-stu-id="cb69f-129">This section should contain hello following XML:</span></span>

    ```xml
    <build>
        <plugins>
            <!-- build for Java 1.8. This is required by HDInsight 3.5  -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.3</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
            </plugin>
            <!-- build an uber jar -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>2.3</version>
                <configuration>
                    <!-- Keep us from getting a can't overwrite file error -->
                    <transformers>
                        <transformer
                                implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer">
                        </transformer>
                        <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer">
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
        </plugins>
    </build>
    ```

    <span data-ttu-id="cb69f-130">這些項目會定義如何 toobuild hello 專案。</span><span class="sxs-lookup"><span data-stu-id="cb69f-130">These entries define how toobuild hello project.</span></span> <span data-ttu-id="cb69f-131">具體來說，hello 專案使用的 Java hello 版本以及如何 toobuild uberjar 部署 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="cb69f-131">Specifically, hello version of Java that hello project uses and how toobuild an uberjar for deployment toohello cluster.</span></span>

    <span data-ttu-id="cb69f-132">一旦 hello 已變更，請儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="cb69f-132">Save hello file once hello changes have been made.</span></span>

4. <span data-ttu-id="cb69f-133">重新命名**exampleudf/src/main/java/com/microsoft/examples/App.java**太**ExampleUDF.java**，然後開啟您在編輯器中的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="cb69f-133">Rename **exampleudf/src/main/java/com/microsoft/examples/App.java** too**ExampleUDF.java**, and then open hello file in your editor.</span></span>

5. <span data-ttu-id="cb69f-134">取代 hello hello 內容**ExampleUDF.java** hello 下列檔案，然後儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="cb69f-134">Replace hello contents of hello **ExampleUDF.java** file with hello following, then save hello file.</span></span>

    ```java
    package com.microsoft.examples;

    import org.apache.hadoop.hive.ql.exec.Description;
    import org.apache.hadoop.hive.ql.exec.UDF;
    import org.apache.hadoop.io.*;

    // Description of hello UDF
    @Description(
        name="ExampleUDF",
        value="returns a lower case version of hello input string.",
        extended="select ExampleUDF(deviceplatform) from hivesampletable limit 10;"
    )
    public class ExampleUDF extends UDF {
        // Accept a string input
        public String evaluate(String input) {
            // If hello value is null, return a null
            if(input == null)
                return null;
            // Lowercase hello input string and return it
            return input.toLowerCase();
        }
    }
    ```

    <span data-ttu-id="cb69f-135">此程式碼會實作接受字串值，並傳回 hello 字串的小寫版本的 UDF。</span><span class="sxs-lookup"><span data-stu-id="cb69f-135">This code implements a UDF that accepts a string value, and returns a lowercase version of hello string.</span></span>

## <a name="build-and-install-hello-udf"></a><span data-ttu-id="cb69f-136">建置和安裝 hello UDF</span><span class="sxs-lookup"><span data-stu-id="cb69f-136">Build and install hello UDF</span></span>

1. <span data-ttu-id="cb69f-137">使用下列命令 toocompile hello 和封裝 hello UDF:</span><span class="sxs-lookup"><span data-stu-id="cb69f-137">Use hello following command toocompile and package hello UDF:</span></span>

    ```bash
    mvn compile package
    ```

    <span data-ttu-id="cb69f-138">此命令會建置並封裝成 hello hello UDF`exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar`檔案。</span><span class="sxs-lookup"><span data-stu-id="cb69f-138">This command builds and packages hello UDF into hello `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` file.</span></span>

2. <span data-ttu-id="cb69f-139">使用 hello`scp`命令 toocopy hello 檔案 toohello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="cb69f-139">Use hello `scp` command toocopy hello file toohello HDInsight cluster.</span></span>

    ```bash
    scp ./target/ExampleUDF-1.0-SNAPSHOT.jar myuser@mycluster-ssh.azurehdinsight
    ```

    <span data-ttu-id="cb69f-140">取代`myuser`以 hello SSH 使用者帳戶，供您的叢集。</span><span class="sxs-lookup"><span data-stu-id="cb69f-140">Replace `myuser` with hello SSH user account for your cluster.</span></span> <span data-ttu-id="cb69f-141">取代`mycluster`與 hello 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="cb69f-141">Replace `mycluster` with hello cluster name.</span></span> <span data-ttu-id="cb69f-142">如果您使用密碼 toosecure hello SSH 帳戶時，您必須提示的 tooenter hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="cb69f-142">If you used a password toosecure hello SSH account, you are prompted tooenter hello password.</span></span> <span data-ttu-id="cb69f-143">如果您使用憑證，您可能需要 toouse hello`-i`參數 toospecify hello 私密金鑰檔案。</span><span class="sxs-lookup"><span data-stu-id="cb69f-143">If you used a certificate, you may need toouse hello `-i` parameter toospecify hello private key file.</span></span>

3. <span data-ttu-id="cb69f-144">Toohello 叢集使用 SSH 連線。</span><span class="sxs-lookup"><span data-stu-id="cb69f-144">Connect toohello cluster using SSH.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="cb69f-145">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="cb69f-145">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

4. <span data-ttu-id="cb69f-146">從 hello SSH 工作階段，將複製 hello jar 檔案 tooHDInsight 存放裝置。</span><span class="sxs-lookup"><span data-stu-id="cb69f-146">From hello SSH session, copy hello jar file tooHDInsight storage.</span></span>

    ```bash
    hdfs dfs -put ExampleUDF-1.0-SNAPSHOT.jar /example/jars
    ```

## <a name="use-hello-udf-from-hive"></a><span data-ttu-id="cb69f-147">使用 Hive hello UDF</span><span class="sxs-lookup"><span data-stu-id="cb69f-147">Use hello UDF from Hive</span></span>

1. <span data-ttu-id="cb69f-148">使用下列 toostart hello Beeline 用戶端 hello SSH 工作階段的 hello。</span><span class="sxs-lookup"><span data-stu-id="cb69f-148">Use hello following toostart hello Beeline client from hello SSH session.</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="cb69f-149">此命令假設您使用 hello 預設值是**admin** hello 登入帳戶，供您的叢集。</span><span class="sxs-lookup"><span data-stu-id="cb69f-149">This command assumes that you used hello default of **admin** for hello login account for your cluster.</span></span>

2. <span data-ttu-id="cb69f-150">一旦您到達 hello`jdbc:hive2://localhost:10001/>`提示，然後輸入 hello 遵循 tooadd hello UDF tooHive 並將它公開為函式。</span><span class="sxs-lookup"><span data-stu-id="cb69f-150">Once you arrive at hello `jdbc:hive2://localhost:10001/>` prompt, enter hello following tooadd hello UDF tooHive and expose it as a function.</span></span>

    ```hiveql
    ADD JAR wasb:///example/jars/ExampleUDF-1.0-SNAPSHOT.jar;
    CREATE TEMPORARY FUNCTION tolower as 'com.microsoft.examples.ExampleUDF';
    ```

    > [!NOTE]
    > <span data-ttu-id="cb69f-151">這個範例假設 Azure 儲存體是 hello 叢集的預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="cb69f-151">This example assumes that Azure Storage is default storage for hello cluster.</span></span> <span data-ttu-id="cb69f-152">如果您的叢集會改為使用資料湖存放區，變更 hello`wasb:///`值太`adl:///`。</span><span class="sxs-lookup"><span data-stu-id="cb69f-152">If your cluster uses Data Lake Store instead, change hello `wasb:///` value too`adl:///`.</span></span>

3. <span data-ttu-id="cb69f-153">使用擷取自資料表 toolower 大小寫字串 hello UDF tooconvert 值。</span><span class="sxs-lookup"><span data-stu-id="cb69f-153">Use hello UDF tooconvert values retrieved from a table toolower case strings.</span></span>

    ```hiveql
    SELECT tolower(deviceplatform) FROM hivesampletable LIMIT 10;
    ```

    <span data-ttu-id="cb69f-154">選取 hello 裝置平台 （Android、 Windows、 iOS、 等等） 從 hello 資料表中，此查詢轉換 hello 字串 toolower 情況下，，，然後將它們顯示。</span><span class="sxs-lookup"><span data-stu-id="cb69f-154">This query selects hello device platform (Android, Windows, iOS, etc.) from hello table, convert hello string toolower case, and then display them.</span></span> <span data-ttu-id="cb69f-155">會出現下列文字類似 toohello hello 輸出：</span><span class="sxs-lookup"><span data-stu-id="cb69f-155">hello output appears similar toohello following text:</span></span>

        +----------+--+
        |   _c0    |
        +----------+--+
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        +----------+--+

## <a name="next-steps"></a><span data-ttu-id="cb69f-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cb69f-156">Next steps</span></span>

<span data-ttu-id="cb69f-157">Hive 以其他方式 toowork，請參閱[使用 Hive 與 HDInsight](hdinsight-use-hive.md)。</span><span class="sxs-lookup"><span data-stu-id="cb69f-157">For other ways toowork with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="cb69f-158">如需有關 Hive User-Defined 函式的詳細資訊，請參閱[hive 控制檔的運算子和使用者定義函數](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF)hello Hive wiki apache.org 在區段。</span><span class="sxs-lookup"><span data-stu-id="cb69f-158">For more information on Hive User-Defined Functions, see [Hive Operators and User-Defined Functions](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) section of hello Hive wiki at apache.org.</span></span>
