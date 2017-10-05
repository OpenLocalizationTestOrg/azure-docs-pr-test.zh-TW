---
title: "Java HBase 用戶端 - Azure HDInsight | Microsoft Docs"
description: "了解如何使用 Apache Maven 建置以 Java 為基礎的 Apache HBase 應用程式，然後將它部署至 Azure HDInsight 上的 HBase。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: 
ms.assetid: 1d1ed180-e0f4-4d1c-b5ea-72e0eda643bc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 03c88397e36c0fc7f19410e49f6b6f1a607659f8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="build-java-applications-for-apache-hbase"></a><span data-ttu-id="238be-103">建置 Apache HBase 的 Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="238be-103">Build Java applications for Apache HBase</span></span>

<span data-ttu-id="238be-104">了解如何在 Java 中建立 [Apache HBase](http://hbase.apache.org/) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="238be-104">Learn how to create an [Apache HBase](http://hbase.apache.org/) application in Java.</span></span> <span data-ttu-id="238be-105">然後使用此應用程式搭配 Azure HDInsight 上的 HBase。</span><span class="sxs-lookup"><span data-stu-id="238be-105">Then use the application with HBase on Azure HDInsight.</span></span>

<span data-ttu-id="238be-106">本文件中的步驟使用 [Maven](http://maven.apache.org/) 來建立專案。</span><span class="sxs-lookup"><span data-stu-id="238be-106">The steps in this document use [Maven](http://maven.apache.org/) to create and build the project.</span></span> <span data-ttu-id="238be-107">Maven是軟體專案管理和理解工具，可讓您建置 Java 專案的軟體、文件及報告。</span><span class="sxs-lookup"><span data-stu-id="238be-107">Maven is a software project management and comprehension tool that allows you to build software, documentation, and reports for Java projects.</span></span>

> [!NOTE]
> <span data-ttu-id="238be-108">此文件中的步驟最近已在 HDInsight 3.6 中測試過。</span><span class="sxs-lookup"><span data-stu-id="238be-108">The steps in this document were most recently tested with HDInsight 3.6.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="238be-109">此文件中的步驟需要使用 Linux 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="238be-109">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="238be-110">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="238be-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="238be-111">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="238be-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="requirements"></a><span data-ttu-id="238be-112">需求</span><span class="sxs-lookup"><span data-stu-id="238be-112">Requirements</span></span>

* <span data-ttu-id="238be-113">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="238be-113">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 or later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="238be-114">HDInsight 3.5 和更新版本需要 Java 8。</span><span class="sxs-lookup"><span data-stu-id="238be-114">HDInsight 3.5 and greater requires Java 8.</span></span> <span data-ttu-id="238be-115">舊版的 HDInsight 需要 Java 7。</span><span class="sxs-lookup"><span data-stu-id="238be-115">Earlier versions of HDInsight require Java 7.</span></span>

* [<span data-ttu-id="238be-116">Maven</span><span class="sxs-lookup"><span data-stu-id="238be-116">Maven</span></span>](http://maven.apache.org/)

* [<span data-ttu-id="238be-117">具有 HBase 的 Linux 型 Azure HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="238be-117">A Linux-based Azure HDInsight cluster with HBase</span></span>](hdinsight-hbase-tutorial-get-started-linux.md#create-hbase-cluster)

  > [!NOTE]
  > <span data-ttu-id="238be-118">此文件中的步驟已經過 HDInsight 叢集 3.4 和 3.5 版的測試。</span><span class="sxs-lookup"><span data-stu-id="238be-118">The steps in this document have been tested with HDInsight cluster versions 3.4 and 3.5.</span></span> <span data-ttu-id="238be-119">範例中提供的預設值適用於 HDInsight 3.5 叢集。</span><span class="sxs-lookup"><span data-stu-id="238be-119">The default values provided in examples are for a HDInsight 3.5 cluster.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="238be-120">建立專案</span><span class="sxs-lookup"><span data-stu-id="238be-120">Create the project</span></span>

1. <span data-ttu-id="238be-121">從開發環境的命令列中，將目錄變更至您想要建立專案的位置，例如 `cd code\hbase`。</span><span class="sxs-lookup"><span data-stu-id="238be-121">From the command line in your development environment, change directories to the location where you want to create the project, for example, `cd code\hbase`.</span></span>

2. <span data-ttu-id="238be-122">使用隨 Maven 一起安裝的 **mvn** 命令來產生專案的結構。</span><span class="sxs-lookup"><span data-stu-id="238be-122">Use the **mvn** command, which is installed with Maven, to generate the scaffolding for the project.</span></span>

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

    > [!NOTE]
    > <span data-ttu-id="238be-123">如果您使用 PowerShell，則必須將 `-D` 參數放置在雙引號內。</span><span class="sxs-lookup"><span data-stu-id="238be-123">If you are using PowerShell, you must enclose the `-D` parameters in double quotes.</span></span>
    >
    > `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=hbaseapp" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    <span data-ttu-id="238be-124">此命令會利用與 **artifactID** 參數 (此範例中為 **hbaseapp**) 相同的名稱來建立目錄。此目錄包含下列項目：</span><span class="sxs-lookup"><span data-stu-id="238be-124">This command creates a directory with the same name as the **artifactID** parameter (**hbaseapp** in this example.) This directory contains the following items:</span></span>

   * <span data-ttu-id="238be-125">**pom.xml**：專案物件模型 ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) 包含用來建置專案之資訊和組態的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="238be-125">**pom.xml**:  The Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contains information and configuration details used to build the project.</span></span>
   * <span data-ttu-id="238be-126">**src**：包含 **main/java/com/microsoft/examples** 目錄的目錄，您將在此處撰寫應用程式。</span><span class="sxs-lookup"><span data-stu-id="238be-126">**src**: The directory that contains the **main/java/com/microsoft/examples** directory, where you author the application.</span></span>

3. <span data-ttu-id="238be-127">刪除 `src/test/java/com/microsoft/examples/apptest.java` 檔案。</span><span class="sxs-lookup"><span data-stu-id="238be-127">Delete the `src/test/java/com/microsoft/examples/apptest.java` file.</span></span> <span data-ttu-id="238be-128">此範例不會使用此方法。</span><span class="sxs-lookup"><span data-stu-id="238be-128">It is not be used in this example.</span></span>

## <a name="update-the-project-object-model"></a><span data-ttu-id="238be-129">更新專案物件模型</span><span class="sxs-lookup"><span data-stu-id="238be-129">Update the Project Object Model</span></span>

1. <span data-ttu-id="238be-130">編輯 `pom.xml` 檔案，並在 `<dependencies>` 區段內新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="238be-130">Edit the `pom.xml` file and add the following code inside the `<dependencies>` section:</span></span>

   ```xml
    <dependency>
        <groupId>org.apache.hbase</groupId>
        <artifactId>hbase-client</artifactId>
        <version>1.1.2</version>
    </dependency>
    <dependency>
        <groupId>org.apache.phoenix</groupId>
        <artifactId>phoenix-core</artifactId>
        <version>4.4.0-HBase-1.1</version>
    </dependency>
   ```

    <span data-ttu-id="238be-131">此區段指出專案需要 **hbase-client** 和 **phoenix-core** 元件。</span><span class="sxs-lookup"><span data-stu-id="238be-131">This section indicates that the project needs **hbase-client** and **phoenix-core** components.</span></span> <span data-ttu-id="238be-132">在編譯期間，會從預設的 Maven 儲存機制下載這些相依性。</span><span class="sxs-lookup"><span data-stu-id="238be-132">At compile time, these dependencies are downloaded from the default Maven repository.</span></span> <span data-ttu-id="238be-133">您可以使用 [Maven 中央儲存機制搜尋](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) ，進一步了解此相依性的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="238be-133">You can use the [Maven Central Repository Search](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) to learn more about this dependency.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="238be-134">hbase-client 的版本號碼必須符合隨附於 HDInsight 叢集的 HBase 版本。</span><span class="sxs-lookup"><span data-stu-id="238be-134">The version number of the hbase-client must match the version of HBase that is provided with your HDInsight cluster.</span></span> <span data-ttu-id="238be-135">您可以使用下表來尋找正確的版本號碼。</span><span class="sxs-lookup"><span data-stu-id="238be-135">Use the following table to find the correct version number.</span></span>

   | <span data-ttu-id="238be-136">HDInsight 叢集版本</span><span class="sxs-lookup"><span data-stu-id="238be-136">HDInsight cluster version</span></span> | <span data-ttu-id="238be-137">要使用的 HBase 版本</span><span class="sxs-lookup"><span data-stu-id="238be-137">HBase version to use</span></span> |
   | --- | --- |
   | <span data-ttu-id="238be-138">3.2</span><span class="sxs-lookup"><span data-stu-id="238be-138">3.2</span></span> |<span data-ttu-id="238be-139">0.98.4-hadoop2</span><span class="sxs-lookup"><span data-stu-id="238be-139">0.98.4-hadoop2</span></span> |
   | <span data-ttu-id="238be-140">3.3、3.4、3.5 和 3.6</span><span class="sxs-lookup"><span data-stu-id="238be-140">3.3, 3.4, 3.5, and 3.6</span></span> |<span data-ttu-id="238be-141">1.1.2</span><span class="sxs-lookup"><span data-stu-id="238be-141">1.1.2</span></span> |

    <span data-ttu-id="238be-142">如需 HDInsight 版本和元件的詳細資訊，請參閱 [HDInsight 提供的 Hadoop 元件有什麼不同](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="238be-142">For more information on HDInsight versions and components, see [What are the different Hadoop components available with HDInsight](hdinsight-component-versioning.md).</span></span>

3. <span data-ttu-id="238be-143">將下列程式碼加入 **pom.xml** 檔案。</span><span class="sxs-lookup"><span data-stu-id="238be-143">Add the following code to the **pom.xml** file.</span></span> <span data-ttu-id="238be-144">此文字必須位在檔案中的 `<project>...</project>` 標籤內，例如在 `</dependencies>` 和 `</project>` 之間。</span><span class="sxs-lookup"><span data-stu-id="238be-144">This text must be inside the `<project>...</project>` tags in the file, for example, between `</dependencies>` and `</project>`.</span></span>

   ```xml
    <build>
        <sourceDirectory>src</sourceDirectory>
        <resources>
        <resource>
            <directory>${basedir}/conf</directory>
            <filtering>false</filtering>
            <includes>
            <include>hbase-site.xml</include>
            </includes>
        </resource>
        </resources>
        <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
                    <version>3.3</version>
            <configuration>
                <source>1.8</source>
                <target>1.8</target>
            </configuration>
            </plugin>
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
        </plugins>
    </build>
   ```

    <span data-ttu-id="238be-145">此區段會設定包含 HBase 組態資訊的資源(`conf/hbase-site.xml`)。</span><span class="sxs-lookup"><span data-stu-id="238be-145">This section configures a resource (`conf/hbase-site.xml`) that contains configuration information for HBase.</span></span>

   > [!NOTE]
   > <span data-ttu-id="238be-146">您也可以透過程式碼來設定組態值。</span><span class="sxs-lookup"><span data-stu-id="238be-146">You can also set configuration values via code.</span></span> <span data-ttu-id="238be-147">請參閱 `CreateTable` 範例中的註解。</span><span class="sxs-lookup"><span data-stu-id="238be-147">See the comments in the `CreateTable` example.</span></span>

    <span data-ttu-id="238be-148">此區段也會設定 [Maven Compiler 外掛程式](http://maven.apache.org/plugins/maven-compiler-plugin/)與 [Maven Shade 外掛程式](http://maven.apache.org/plugins/maven-shade-plugin/)。</span><span class="sxs-lookup"><span data-stu-id="238be-148">This section also configures the [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) and [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span></span> <span data-ttu-id="238be-149">Compiler 外掛程式用來編譯拓撲。</span><span class="sxs-lookup"><span data-stu-id="238be-149">The compiler plug-in is used to compile the topology.</span></span> <span data-ttu-id="238be-150">Shade 外掛程式用來防止以 Maven 所建置的 JAR 封裝發生授權重複。</span><span class="sxs-lookup"><span data-stu-id="238be-150">The shade plug-in is used to prevent license duplication in the JAR package that is built by Maven.</span></span> <span data-ttu-id="238be-151">此外掛程式是用於防止 HDInsight 叢集在執行階段發生「重複的授權檔案」錯誤。</span><span class="sxs-lookup"><span data-stu-id="238be-151">This plugin is used to prevent a "duplicate license files" error at run time on the HDInsight cluster.</span></span> <span data-ttu-id="238be-152">使用 maven-shade-plugin 搭配 `ApacheLicenseResourceTransformer` 實作可防止此錯誤。</span><span class="sxs-lookup"><span data-stu-id="238be-152">Using maven-shade-plugin with the `ApacheLicenseResourceTransformer` implementation prevents the error.</span></span>

    <span data-ttu-id="238be-153">maven-shade-plugin 也會產生 uber jar，其中含有應用程式需要的所有相依性。</span><span class="sxs-lookup"><span data-stu-id="238be-153">The maven-shade-plugin also produces an uber jar that contains all the dependencies required by the application.</span></span>

4. <span data-ttu-id="238be-154">儲存 `pom.xml` 檔案。</span><span class="sxs-lookup"><span data-stu-id="238be-154">Save the `pom.xml` file.</span></span>

5. <span data-ttu-id="238be-155">在 `hbaseapp` 目錄中建立名為 `conf` 的目錄。</span><span class="sxs-lookup"><span data-stu-id="238be-155">Create a directory named `conf` in the `hbaseapp` directory.</span></span> <span data-ttu-id="238be-156">此目錄會用來保存連接至 HBase 的組態資訊。</span><span class="sxs-lookup"><span data-stu-id="238be-156">This directory is used to hold configuration information for connecting to HBase.</span></span>

6. <span data-ttu-id="238be-157">使用下列命令將 HBase 組態，從 HBase 叢集複製到 `conf` 目錄。</span><span class="sxs-lookup"><span data-stu-id="238be-157">Use the following command to copy the HBase configuration from the HBase cluster to the `conf` directory.</span></span> <span data-ttu-id="238be-158">將 `USERNAME` 取代為您的 SSH 登入名稱。</span><span class="sxs-lookup"><span data-stu-id="238be-158">Replace `USERNAME` with the name of your SSH login.</span></span> <span data-ttu-id="238be-159">將 `CLUSTERNAME` 取代為 HDInsight 叢集名稱：</span><span class="sxs-lookup"><span data-stu-id="238be-159">Replace `CLUSTERNAME` with your HDInsight cluster name:</span></span>

    ```bash
    scp USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:/etc/hbase/conf/hbase-site.xml ./conf/hbase-site.xml
    ```

   <span data-ttu-id="238be-160">如需使用 `ssh` 和 `scp` 的詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="238be-160">For more information on using `ssh` and `scp`, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-the-application"></a><span data-ttu-id="238be-161">建立應用程式</span><span class="sxs-lookup"><span data-stu-id="238be-161">Create the application</span></span>

1. <span data-ttu-id="238be-162">移至 `hbaseapp/src/main/java/com/microsoft/examples` 目錄，並將 app.java 檔案重新命名為 `CreateTable.java`。</span><span class="sxs-lookup"><span data-stu-id="238be-162">Go to the `hbaseapp/src/main/java/com/microsoft/examples` directory and rename the app.java file to `CreateTable.java`.</span></span>

2. <span data-ttu-id="238be-163">開啟 `CreateTable.java` 檔案，並以下列文字取代現有的內容：</span><span class="sxs-lookup"><span data-stu-id="238be-163">Open the `CreateTable.java` file and replace the existing contents with the following text:</span></span>

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HBaseAdmin;
    import org.apache.hadoop.hbase.HTableDescriptor;
    import org.apache.hadoop.hbase.TableName;
    import org.apache.hadoop.hbase.HColumnDescriptor;
    import org.apache.hadoop.hbase.client.HTable;
    import org.apache.hadoop.hbase.client.Put;
    import org.apache.hadoop.hbase.util.Bytes;

    public class CreateTable {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Example of setting zookeeper values for HDInsight
        // in code instead of an hbase-site.xml file
        //
        // config.set("hbase.zookeeper.quorum",
        //            "zookeepernode0,zookeepernode1,zookeepernode2");
        //config.set("hbase.zookeeper.property.clientPort", "2181");
        //config.set("hbase.cluster.distributed", "true");
        //
        //NOTE: Actual zookeeper host names can be found using Ambari:
        //curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/hosts"

        //Linux-based HDInsight clusters use /hbase-unsecure as the znode parent
        config.set("zookeeper.znode.parent","/hbase-unsecure");

        // create an admin object using the config
        HBaseAdmin admin = new HBaseAdmin(config);

        // create the table...
        HTableDescriptor tableDescriptor = new HTableDescriptor(TableName.valueOf("people"));
        // ... with two column families
        tableDescriptor.addFamily(new HColumnDescriptor("name"));
        tableDescriptor.addFamily(new HColumnDescriptor("contactinfo"));
        admin.createTable(tableDescriptor);

        // define some people
        String[][] people = {
            { "1", "Marcel", "Haddad", "marcel@fabrikam.com"},
            { "2", "Franklin", "Holtz", "franklin@contoso.com" },
            { "3", "Dwayne", "McKee", "dwayne@fabrikam.com" },
            { "4", "Rae", "Schroeder", "rae@contoso.com" },
            { "5", "Rosalie", "burton", "rosalie@fabrikam.com"},
            { "6", "Gabriela", "Ingram", "gabriela@contoso.com"} };

        HTable table = new HTable(config, "people");

        // Add each person to the table
        //   Use the `name` column family for the name
        //   Use the `contactinfo` column family for the email
        for (int i = 0; i< people.length; i++) {
            Put person = new Put(Bytes.toBytes(people[i][0]));
            person.add(Bytes.toBytes("name"), Bytes.toBytes("first"), Bytes.toBytes(people[i][1]));
            person.add(Bytes.toBytes("name"), Bytes.toBytes("last"), Bytes.toBytes(people[i][2]));
            person.add(Bytes.toBytes("contactinfo"), Bytes.toBytes("email"), Bytes.toBytes(people[i][3]));
            table.put(person);
        }
        // flush commits and close the table
        table.flushCommits();
        table.close();
        }
    }
   ```

    <span data-ttu-id="238be-164">此程式碼是 **CreateTable** 類別，將會建立名為 **people** 的資料表，並填入一些預先定義的使用者。</span><span class="sxs-lookup"><span data-stu-id="238be-164">This code is the **CreateTable** class, which creates a table named **people** and populate it with some predefined users.</span></span>

3. <span data-ttu-id="238be-165">儲存 `CreateTable.java` 檔案。</span><span class="sxs-lookup"><span data-stu-id="238be-165">Save the `CreateTable.java` file.</span></span>

4. <span data-ttu-id="238be-166">在 `hbaseapp/src/main/java/com/microsoft/examples` 目錄中，建立名稱為 `SearchByEmail.java` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="238be-166">In the `hbaseapp/src/main/java/com/microsoft/examples` directory, create a file named `SearchByEmail.java`.</span></span> <span data-ttu-id="238be-167">使用下列文字做為此檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="238be-167">Use the following text as the contents of this file:</span></span>

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HTable;
    import org.apache.hadoop.hbase.client.Scan;
    import org.apache.hadoop.hbase.client.ResultScanner;
    import org.apache.hadoop.hbase.client.Result;
    import org.apache.hadoop.hbase.filter.RegexStringComparator;
    import org.apache.hadoop.hbase.filter.SingleColumnValueFilter;
    import org.apache.hadoop.hbase.filter.CompareFilter.CompareOp;
    import org.apache.hadoop.hbase.util.Bytes;
    import org.apache.hadoop.util.GenericOptionsParser;

    public class SearchByEmail {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Use GenericOptionsParser to get only the parameters to the class
        // and not all the parameters passed (when using WebHCat for example)
        String[] otherArgs = new GenericOptionsParser(config, args).getRemainingArgs();
        if (otherArgs.length != 1) {
            System.out.println("usage: [regular expression]");
            System.exit(-1);
        }

        // Open the table
        HTable table = new HTable(config, "people");

        // Define the family and qualifiers to be used
        byte[] contactFamily = Bytes.toBytes("contactinfo");
        byte[] emailQualifier = Bytes.toBytes("email");
        byte[] nameFamily = Bytes.toBytes("name");
        byte[] firstNameQualifier = Bytes.toBytes("first");
        byte[] lastNameQualifier = Bytes.toBytes("last");

        // Create a regex filter
        RegexStringComparator emailFilter = new RegexStringComparator(otherArgs[0]);
        // Attach the regex filter to a filter
        //   for the email column
        SingleColumnValueFilter filter = new SingleColumnValueFilter(
            contactFamily,
            emailQualifier,
            CompareOp.EQUAL,
            emailFilter
        );

        // Create a scan and set the filter
        Scan scan = new Scan();
        scan.setFilter(filter);

        // Get the results
        ResultScanner results = table.getScanner(scan);
        // Iterate over results and print  values
        for (Result result : results ) {
            String id = new String(result.getRow());
            byte[] firstNameObj = result.getValue(nameFamily, firstNameQualifier);
            String firstName = new String(firstNameObj);
            byte[] lastNameObj = result.getValue(nameFamily, lastNameQualifier);
            String lastName = new String(lastNameObj);
            System.out.println(firstName + " " + lastName + " - ID: " + id);
            byte[] emailObj = result.getValue(contactFamily, emailQualifier);
            String email = new String(emailObj);
            System.out.println(firstName + " " + lastName + " - " + email + " - ID: " + id);
        }
        results.close();
        table.close();
        }
    }
   ```

    <span data-ttu-id="238be-168">**SearchByEmail** 類別可用來依電子郵件地址查詢資料列。</span><span class="sxs-lookup"><span data-stu-id="238be-168">The **SearchByEmail** class can be used to query for rows by email address.</span></span> <span data-ttu-id="238be-169">因為此類別使用規則運算式篩選器，您可以在使用此類別時提供字串或規則運算式。</span><span class="sxs-lookup"><span data-stu-id="238be-169">Because it uses a regular expression filter, you can provide either a string or a regular expression when using the class.</span></span>

5. <span data-ttu-id="238be-170">儲存 `SearchByEmail.java` 檔案。</span><span class="sxs-lookup"><span data-stu-id="238be-170">Save the `SearchByEmail.java` file.</span></span>

6. <span data-ttu-id="238be-171">在 `hbaseapp/src/main/hava/com/microsoft/examples` 目錄中，建立名稱為 `DeleteTable.java` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="238be-171">In the `hbaseapp/src/main/hava/com/microsoft/examples` directory, create a file named `DeleteTable.java`.</span></span> <span data-ttu-id="238be-172">使用下列文字做為此檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="238be-172">Use the following text as the contents of this file:</span></span>

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HBaseAdmin;

    public class DeleteTable {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Create an admin object using the config
        HBaseAdmin admin = new HBaseAdmin(config);

        // Disable, and then delete the table
        admin.disableTable("people");
        admin.deleteTable("people");
        }
    }
   ```

    <span data-ttu-id="238be-173">此類別會清理此範例中建立的 HBase 資料表，方法是停用並卸除 `CreateTable` 類別所建立的資料表。</span><span class="sxs-lookup"><span data-stu-id="238be-173">This class cleans up the HBase tables created in this example by disabling and dropping the table created by the `CreateTable` class.</span></span>

7. <span data-ttu-id="238be-174">儲存 `DeleteTable.java` 檔案。</span><span class="sxs-lookup"><span data-stu-id="238be-174">Save the `DeleteTable.java` file.</span></span>

## <a name="build-and-package-the-application"></a><span data-ttu-id="238be-175">建置和封裝應用程式</span><span class="sxs-lookup"><span data-stu-id="238be-175">Build and package the application</span></span>

1. <span data-ttu-id="238be-176">從 `hbaseapp` 目錄，使用下列命令來建置含有應用程式的 JAR 檔案：</span><span class="sxs-lookup"><span data-stu-id="238be-176">From the `hbaseapp` directory, use the following command to build a JAR file that contains the application:</span></span>

    ```bash
    mvn clean package
    ```

    <span data-ttu-id="238be-177">此命令會建置應用程式並封裝到 .jar 檔案中。</span><span class="sxs-lookup"><span data-stu-id="238be-177">This command builds and packages the application into a .jar file.</span></span>

2. <span data-ttu-id="238be-178">命令完成時，`hbaseapp/target` 目錄就會包含名為 `hbaseapp-1.0-SNAPSHOT.jar` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="238be-178">When the command completes, the `hbaseapp/target` directory contains a file named `hbaseapp-1.0-SNAPSHOT.jar`.</span></span>

   > [!NOTE]
   > <span data-ttu-id="238be-179">`hbaseapp-1.0-SNAPSHOT.jar` 檔案是 uber jar。</span><span class="sxs-lookup"><span data-stu-id="238be-179">The `hbaseapp-1.0-SNAPSHOT.jar` file is an uber jar.</span></span> <span data-ttu-id="238be-180">它包含執行應用程式需要的所有相依性。</span><span class="sxs-lookup"><span data-stu-id="238be-180">It contains all the dependencies required to run the application.</span></span>


## <a name="upload-the-jar-and-run-jobs-ssh"></a><span data-ttu-id="238be-181">上傳 JAR 並執行作業 (SSH)</span><span class="sxs-lookup"><span data-stu-id="238be-181">Upload the JAR and run jobs (SSH)</span></span>

<span data-ttu-id="238be-182">下列步驟使用 `scp` 將 JAR 複製到 HBase on HDInsight 叢集的主要前端節點。</span><span class="sxs-lookup"><span data-stu-id="238be-182">The following steps use `scp` to copy the JAR to the primary head node of your HBase on HDInsight cluster.</span></span> <span data-ttu-id="238be-183">接著，會使用 `ssh` 命令連接到該叢集並直接在前端節點上執行範例。</span><span class="sxs-lookup"><span data-stu-id="238be-183">The `ssh` command is then used to connect to the cluster and run the example directly on the head node.</span></span>

1. <span data-ttu-id="238be-184">若要將 jar 上傳到叢集，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="238be-184">To upload the jar to the cluster, use the following command:</span></span>

    ```bash
    scp ./target/hbaseapp-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:hbaseapp-1.0-SNAPSHOT.jar
    ```

    <span data-ttu-id="238be-185">將 `USERNAME` 取代為您的 SSH 登入名稱。</span><span class="sxs-lookup"><span data-stu-id="238be-185">Replace `USERNAME` with the name of your SSH login.</span></span> <span data-ttu-id="238be-186">將 `CLUSTERNAME` 取代為 HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="238be-186">Replace `CLUSTERNAME` with your HDInsight cluster name.</span></span>

2. <span data-ttu-id="238be-187">若要連線到 HBase 叢集，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="238be-187">To connect to the HBase cluster, use the following command:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="238be-188">將 `USERNAME` 取代為您的 SSH 登入名稱。</span><span class="sxs-lookup"><span data-stu-id="238be-188">Replace `USERNAME` the name of your SSH login.</span></span> <span data-ttu-id="238be-189">將 `CLUSTERNAME` 取代為 HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="238be-189">Replace `CLUSTERNAME` with your HDInsight cluster name.</span></span>

3. <span data-ttu-id="238be-190">若要使用 Java 應用程式來建立 HBase 資料表，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="238be-190">To create an HBase table using the Java application, use the following command:</span></span>

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.CreateTable
    ```

    <span data-ttu-id="238be-191">此命令會建立名為 **people** 的 HBase 資料表，並填入資料。</span><span class="sxs-lookup"><span data-stu-id="238be-191">This command creates a HBase table named **people**, and populates it with data.</span></span>

4. <span data-ttu-id="238be-192">若要搜尋資料表中儲存的電子郵件地址，請使用以下命令：</span><span class="sxs-lookup"><span data-stu-id="238be-192">To search for email addresses stored in the table, use the following command:</span></span>

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.SearchByEmail contoso.com
    ```

    <span data-ttu-id="238be-193">您會收到下列結果：</span><span class="sxs-lookup"><span data-stu-id="238be-193">You receive the following results:</span></span>

        Franklin Holtz - ID: 2
        Franklin Holtz - franklin@contoso.com - ID: 2
        Rae Schroeder - ID: 4
        Rae Schroeder - rae@contoso.com - ID: 4
        Gabriela Ingram - ID: 6
        Gabriela Ingram - gabriela@contoso.com - ID: 6

5. <span data-ttu-id="238be-194">若要刪除資料表，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="238be-194">To delete the table, use the following command:</span></span>

    

## <a name="upload-the-jar-and-run-jobs-powershell"></a><span data-ttu-id="238be-195">上傳 JAR 並執行作業 (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="238be-195">Upload the JAR and run jobs (PowerShell)</span></span>

<span data-ttu-id="238be-196">下列步驟使用 Azure PowerShell 將 JAR 上傳到您 HBase 叢集的預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="238be-196">The following steps use Azure PowerShell to upload the JAR to the default storage for your HBase cluster.</span></span> <span data-ttu-id="238be-197">接著，會使用 HDInsight Cmdlet 從遠端執行範例。</span><span class="sxs-lookup"><span data-stu-id="238be-197">HDInsight cmdlets are then used to run the examples remotely.</span></span>

1. <span data-ttu-id="238be-198">安裝並設定 Azure PowerShell 之後，請建立名為 `hbase-runner.psm1` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="238be-198">After installing and configuring Azure PowerShell, create a file named `hbase-runner.psm1`.</span></span> <span data-ttu-id="238be-199">使用下列文字做為此檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="238be-199">Use the following text as the contents of this file:</span></span>

   ```powershell
    <#
    .SYNOPSIS
    Copies a file to the primary storage of an HDInsight cluster.
    .DESCRIPTION
    Copies a file from a local directory to the blob container for
    the HDInsight cluster.
    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.CreateTable"
    -clusterName "MyHDInsightCluster"

    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.SearchByEmail"
    -clusterName "MyHDInsightCluster"
    -emailRegex "contoso.com"

    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.SearchByEmail"
    -clusterName "MyHDInsightCluster"
    -emailRegex "^r" -showErr
    #>

    function Start-HBaseExample {
    [CmdletBinding(SupportsShouldProcess = $true)]
    param(
    #The class to run
    [Parameter(Mandatory = $true)]
    [String]$className,

    #The name of the HDInsight cluster
    [Parameter(Mandatory = $true)]
    [String]$clusterName,

    #Only used when using SearchByEmail
    [Parameter(Mandatory = $false)]
    [String]$emailRegex,

    #Use if you want to see stderr output
    [Parameter(Mandatory = $false)]
    [Switch]$showErr
    )

    Set-StrictMode -Version 3

    # Is the Azure module installed?
    FindAzure

    # Get the login for the HDInsight cluster
    $creds=Get-Credential -Message "Enter the login for the cluster" -UserName "admin"

    # The JAR
    $jarFile = "wasb:///example/jars/hbaseapp-1.0-SNAPSHOT.jar"

    # The job definition
    $jobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
        -JarFile $jarFile `
        -ClassName $className `
        -Arguments $emailRegex

    # Get the job output
    $job = Start-AzureRmHDInsightJob `
        -ClusterName $clusterName `
        -JobDefinition $jobDefinition `
        -HttpCredential $creds
    Write-Host "Wait for the job to complete ..." -ForegroundColor Green
    Wait-AzureRmHDInsightJob `
        -ClusterName $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds
    if($showErr)
    {
    Write-Host "STDERR"
    Get-AzureRmHDInsightJobOutput `
                -Clustername $clusterName `
                -JobId $job.JobId `
                -HttpCredential $creds `
                -DisplayOutputType StandardError
    }
    Write-Host "Display the standard output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
                -Clustername $clusterName `
                -JobId $job.JobId `
                -HttpCredential $creds
    }

    <#
    .SYNOPSIS
    Copies a file to the primary storage of an HDInsight cluster.
    .DESCRIPTION
    Copies a file from a local directory to the blob container for
    the HDInsight cluster.
    .EXAMPLE
    Add-HDInsightFile -localPath "C:\temp\data.txt"
    -destinationPath "example/data/data.txt"
    -ClusterName "MyHDInsightCluster"
    .EXAMPLE
    Add-HDInsightFile -localPath "C:\temp\data.txt"
    -destinationPath "example/data/data.txt"
    -ClusterName "MyHDInsightCluster"
    -Container "MyContainer"
    #>

    function Add-HDInsightFile {
        [CmdletBinding(SupportsShouldProcess = $true)]
        param(
            #The path to the local file.
            [Parameter(Mandatory = $true)]
            [String]$localPath,

            #The destination path and file name, relative to the root of the container.
            [Parameter(Mandatory = $true)]
            [String]$destinationPath,

            #The name of the HDInsight cluster
            [Parameter(Mandatory = $true)]
            [String]$clusterName,

            #If specified, overwrites existing files without prompting
            [Parameter(Mandatory = $false)]
            [Switch]$force
        )

        Set-StrictMode -Version 3

        # Is the Azure module installed?
        FindAzure

        # Get authentication for the cluster
        $creds=Get-Credential

        # Does the local path exist?
        if (-not (Test-Path $localPath))
        {
            throw "Source path '$localPath' does not exist."
        }

        # Get the primary storage container
        $storage = GetStorage -clusterName $clusterName

        # Upload file to storage, overwriting existing files if -force was used.
        Set-AzureStorageBlobContent -File $localPath `
            -Blob $destinationPath `
            -force:$force `
            -Container $storage.container `
            -Context $storage.context
    }

    function FindAzure {
        # Is there an active Azure subscription?
        $sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
        if(-not($sub))
        {
            throw "No active Azure subscription found! If you have a subscription, use the Login-AzureRmAccount cmdlet to login to your subscription."
        }
    }

    function GetStorage {
        param(
            [Parameter(Mandatory = $true)]
            [String]$clusterName
        )
        $hdi = Get-AzureRmHDInsightCluster -ClusterName $clusterName
        # Does the cluster exist?
        if (!$hdi)
        {
            throw "HDInsight cluster '$clusterName' does not exist."
        }
        # Create a return object for context & container
        $return = @{}
        $storageAccounts = @{}

        # Get storage information
        $resourceGroup = $hdi.ResourceGroup
        $storageAccountName=$hdi.DefaultStorageAccount.split('.')[0]
        $container=$hdi.DefaultStorageContainer
        $storageAccountKey=(Get-AzureRmStorageAccountKey `
            -Name $storageAccountName `
        -ResourceGroupName $resourceGroup)[0].Value
        # Get the resource group, in case we need that
        $return.resourceGroup = $resourceGroup
        # Get the storage context, as we can't depend
        # on using the default storage context
        $return.context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        # Get the container, so we know where to
        # find/store blobs
        $return.container = $container
        # Return storage accounts to support finding all accounts for
        # a cluster
        $return.storageAccount = $storageAccountName
        $return.storageAccountKey = $storageAccountKey

        return $return
    }
    # Only export the verb-phrase things
    export-modulemember *-*
   ```

    <span data-ttu-id="238be-200">此檔案包含兩個模組：</span><span class="sxs-lookup"><span data-stu-id="238be-200">This file contains two modules:</span></span>

   * <span data-ttu-id="238be-201">**Add-HDInsightFile** - 用來將檔案上傳到叢集</span><span class="sxs-lookup"><span data-stu-id="238be-201">**Add-HDInsightFile** - used to upload files to the cluster</span></span>
   * <span data-ttu-id="238be-202">**Start-HBaseExample** - 用來執行稍早建立的類別</span><span class="sxs-lookup"><span data-stu-id="238be-202">**Start-HBaseExample** - used to run the classes created earlier</span></span>

2. <span data-ttu-id="238be-203">儲存 `hbase-runner.psm1` 檔案。</span><span class="sxs-lookup"><span data-stu-id="238be-203">Save the `hbase-runner.psm1` file.</span></span>

3. <span data-ttu-id="238be-204">開啟新的 Azure PowerShell 視窗，切換至 `hbaseapp` 目錄，然後執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="238be-204">Open a new Azure PowerShell window, change directories to the `hbaseapp` directory, and then run the following command:</span></span>

    ```powershell
    PS C:\ Import-Module c:\path\to\hbase-runner.psm1
    ```

    <span data-ttu-id="238be-205">將路徑變更為稍早建立之 `hbase-runner.psm1` 檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="238be-205">Change the path to the location of the `hbase-runner.psm1` file created earlier.</span></span> <span data-ttu-id="238be-206">此命令會使用 Azure PowerShell 註冊該模組。</span><span class="sxs-lookup"><span data-stu-id="238be-206">This command registers the module with Azure PowerShell.</span></span>

4. <span data-ttu-id="238be-207">使用下列命令將 `hbaseapp-1.0-SNAPSHOT.jar` 上傳到您的叢集。</span><span class="sxs-lookup"><span data-stu-id="238be-207">Use the following command to upload the `hbaseapp-1.0-SNAPSHOT.jar` to your cluster.</span></span>

    ```powershell
    Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername
    ```

    <span data-ttu-id="238be-208">將 `hdinsightclustername` 取代為您的叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="238be-208">Replace `hdinsightclustername` with the name of your cluster.</span></span> <span data-ttu-id="238be-209">此命令會將 `hbaseapp-1.0-SNAPSHOT.jar` 上傳至您叢集的主要儲存體中的 `example/jars` 位置。</span><span class="sxs-lookup"><span data-stu-id="238be-209">The command uploads the `hbaseapp-1.0-SNAPSHOT.jar` to the `example/jars` location in the primary storage for your cluster.</span></span>

5. <span data-ttu-id="238be-210">若要使用 `hbaseapp` 建立資料表，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="238be-210">To create a table using the `hbaseapp`, use the following command:</span></span>

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername
    ```

    <span data-ttu-id="238be-211">將 `hdinsightclustername` 取代為您的叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="238be-211">Replace `hdinsightclustername` with the name of your cluster.</span></span>

    <span data-ttu-id="238be-212">此命令會在您 HDInsight 叢集上的 HBase 中建立名為 **people** 的資料表。</span><span class="sxs-lookup"><span data-stu-id="238be-212">This command creates a table named **people** in HBase on your HDInsight cluster.</span></span> <span data-ttu-id="238be-213">此命令不會在主控台視窗中顯示任何輸出。</span><span class="sxs-lookup"><span data-stu-id="238be-213">This command does not show any output in the console window.</span></span>

6. <span data-ttu-id="238be-214">若要在資料表中搜尋項目，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="238be-214">To search for entries in the table, use the following command:</span></span>

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com
    ```

    <span data-ttu-id="238be-215">將 `hdinsightclustername` 取代為您的叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="238be-215">Replace `hdinsightclustername` with the name of your cluster.</span></span>

    <span data-ttu-id="238be-216">此命令會使用 `SearchByEmail` 類別來搜尋 `contactinformation` 資料行系列和 `email` 資料行包含字串 `contoso.com` 的任何資料列。</span><span class="sxs-lookup"><span data-stu-id="238be-216">This command uses the `SearchByEmail` class to search for any rows where the `contactinformation` column family and the `email` column, contains the string `contoso.com`.</span></span> <span data-ttu-id="238be-217">您應該會得到下列結果：</span><span class="sxs-lookup"><span data-stu-id="238be-217">You should receive the following results:</span></span>

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    <span data-ttu-id="238be-218">使用 **fabrikam.com** 做為 `-emailRegex` 值會傳回電子郵件欄位中含有 **fabrikam.com** 的使用者。</span><span class="sxs-lookup"><span data-stu-id="238be-218">Using **fabrikam.com** for the `-emailRegex` value returns the users that have **fabrikam.com** in the email field.</span></span> <span data-ttu-id="238be-219">您也可以使用規則運算式作為搜尋字詞。</span><span class="sxs-lookup"><span data-stu-id="238be-219">You can also use regular expressions as the search term.</span></span> <span data-ttu-id="238be-220">例如，**^r** 會傳回開頭為字母 'r' 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="238be-220">For example, **^r** returns email addresses that begin with the letter 'r'.</span></span>

### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a><span data-ttu-id="238be-221">使用 Start-HBaseExample 時沒有結果或傳回非預期的結果</span><span class="sxs-lookup"><span data-stu-id="238be-221">No results or unexpected results when using Start-HBaseExample</span></span>

<span data-ttu-id="238be-222">請使用 `-showErr` 參數，以檢視執行工作時所產生的標準錯誤 (STDERR)。</span><span class="sxs-lookup"><span data-stu-id="238be-222">Use the `-showErr` parameter to view the standard error (STDERR) that is produced while running the job.</span></span>

## <a name="delete-the-table"></a><span data-ttu-id="238be-223">刪除資料表</span><span class="sxs-lookup"><span data-stu-id="238be-223">Delete the table</span></span>

<span data-ttu-id="238be-224">練習完範例之後，請使用下列命令來刪除在此範例中使用的 **people** 資料表：</span><span class="sxs-lookup"><span data-stu-id="238be-224">When you are done with the example, use the following to delete the **people** table used in this example:</span></span>

<span data-ttu-id="238be-225">__從 `ssh` 工作階段__：</span><span class="sxs-lookup"><span data-stu-id="238be-225">__From an `ssh` session__:</span></span>

`yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.DeleteTable`

<span data-ttu-id="238be-226">__從 Azure PowerShell__：</span><span class="sxs-lookup"><span data-stu-id="238be-226">__From Azure PowerShell__:</span></span>

`Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername`

## <a name="next-steps"></a><span data-ttu-id="238be-227">後續步驟</span><span class="sxs-lookup"><span data-stu-id="238be-227">Next steps</span></span>

[<span data-ttu-id="238be-228">了解如何使用 SQuirreL SQL 搭配 HBase</span><span class="sxs-lookup"><span data-stu-id="238be-228">Learn how to use SQuirreL SQL with HBase</span></span>](hdinsight-hbase-phoenix-squirrel-linux.md)
