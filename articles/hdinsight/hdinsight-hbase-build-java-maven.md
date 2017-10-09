---
title: "aaaBuild windows Azure HDInsight Java HBase 應用程式 |Microsoft 文件"
description: "深入了解如何 toouse Apache Maven Java 為基礎的 toobuild Apache HBase 應用程式，然後將它部署 tooa windows Azure HDInsight 叢集。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7f4a4e02-45ab-40dd-842b-3ec034f256c9
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 33c2f3d12cb6a17b5406817e8bcd3accff239517
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-maven-toobuild-java-applications-that-use-hbase-with-windows-based-hdinsight-hadoop"></a><span data-ttu-id="20fcf-103">使用 Maven toobuild Java 應用程式與 Windows 為基礎的 HDInsight (Hadoop) 使用 HBase</span><span class="sxs-lookup"><span data-stu-id="20fcf-103">Use Maven toobuild Java applications that use HBase with Windows-based HDInsight (Hadoop)</span></span>
<span data-ttu-id="20fcf-104">深入了解如何 toocreate 和建置[Apache HBase](http://hbase.apache.org/)使用 Apache Maven java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="20fcf-104">Learn how toocreate and build an [Apache HBase](http://hbase.apache.org/) application in Java by using Apache Maven.</span></span> <span data-ttu-id="20fcf-105">然後使用 hello 應用程式與 Azure HDInsight (Hadoop)。</span><span class="sxs-lookup"><span data-stu-id="20fcf-105">Then use hello application with Azure HDInsight (Hadoop).</span></span>

<span data-ttu-id="20fcf-106">[Maven](http://maven.apache.org/)是軟體專案管理和理解工具，可讓您 toobuild 軟體、 文件和 Java 專案的報表。</span><span class="sxs-lookup"><span data-stu-id="20fcf-106">[Maven](http://maven.apache.org/) is a software project management and comprehension tool that allows you toobuild software, documentation, and reports for Java projects.</span></span> <span data-ttu-id="20fcf-107">在本文中，您將學習如何 toouse 它 toocreate 的基本 Java 應用程式建立、 查詢和刪除 HBase 資料表的 Azure HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="20fcf-107">In this article, you learn how toouse it toocreate a basic Java application that that creates, queries, and deletes an HBase table on an Azure HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="20fcf-108">本文件中的 hello 步驟需要使用 Windows 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="20fcf-108">hello steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="20fcf-109">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="20fcf-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="20fcf-110">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="20fcf-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="requirements"></a><span data-ttu-id="20fcf-111">需求</span><span class="sxs-lookup"><span data-stu-id="20fcf-111">Requirements</span></span>
* <span data-ttu-id="20fcf-112">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 7 或更新版本</span><span class="sxs-lookup"><span data-stu-id="20fcf-112">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 7 or later</span></span>
* [<span data-ttu-id="20fcf-113">Maven</span><span class="sxs-lookup"><span data-stu-id="20fcf-113">Maven</span></span>](http://maven.apache.org/)
* <span data-ttu-id="20fcf-114">搭配使用 HBase 和以 Windows 為基礎的 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="20fcf-114">A Windows-based HDInsight cluster with HBase</span></span>

    > [!NOTE]
    > <span data-ttu-id="20fcf-115">與 HDInsight 叢集版本 3.2 和 3.3 過 hello 本文件中的步驟。</span><span class="sxs-lookup"><span data-stu-id="20fcf-115">hello steps in this document have been tested with HDInsight cluster versions 3.2 and 3.3.</span></span> <span data-ttu-id="20fcf-116">提供範例中的 hello 預設值是 HDInsight 3.3 叢集。</span><span class="sxs-lookup"><span data-stu-id="20fcf-116">hello default values provided in examples are for a HDInsight 3.3 cluster.</span></span>

## <a name="create-hello-project"></a><span data-ttu-id="20fcf-117">建立 hello 專案</span><span class="sxs-lookup"><span data-stu-id="20fcf-117">Create hello project</span></span>
1. <span data-ttu-id="20fcf-118">從開發環境中的 hello 命令列，變更目錄 toohello 所在的位置 toocreate hello 專案，例如`cd code\hdinsight`。</span><span class="sxs-lookup"><span data-stu-id="20fcf-118">From hello command line in your development environment, change directories toohello location where you want toocreate hello project, for example, `cd code\hdinsight`.</span></span>
2. <span data-ttu-id="20fcf-119">使用 hello **mvn**命令，它會隨 Maven，toogenerate hello scaffolding hello 專案。</span><span class="sxs-lookup"><span data-stu-id="20fcf-119">Use hello **mvn** command, which is installed with Maven, toogenerate hello scaffolding for hello project.</span></span>

        mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

    <span data-ttu-id="20fcf-120">此命令會建立一個目錄 hello 目前的位置，與 hello 所指定的 hello 名稱**artifactID**參數 (**hbaseapp**在此範例中。)此目錄包含下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="20fcf-120">This command creates a directory in hello current location, with hello name specified by hello **artifactID** parameter (**hbaseapp** in this example.) This directory contains hello following items:</span></span>

   * <span data-ttu-id="20fcf-121">**pom.xml**: hello Project 物件模型 ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) 包含資訊和設定詳細資料使用 toobuild hello 專案。</span><span class="sxs-lookup"><span data-stu-id="20fcf-121">**pom.xml**:  hello Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contains information and configuration details used toobuild hello project.</span></span>
   * <span data-ttu-id="20fcf-122">**src**: hello 目錄，包含 hello **main\java\com\microsoft\examples**目錄中，您將在其中撰寫 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="20fcf-122">**src**: hello directory that contains hello **main\java\com\microsoft\examples** directory, where you will author hello application.</span></span>
3. <span data-ttu-id="20fcf-123">刪除 hello **src\test\java\com\microsoft\examples\apptest.java**檔案，因為它不會在此範例中使用。</span><span class="sxs-lookup"><span data-stu-id="20fcf-123">Delete hello **src\test\java\com\microsoft\examples\apptest.java** file because it is not used in this example.</span></span>

## <a name="update-hello-project-object-model"></a><span data-ttu-id="20fcf-124">更新 hello Project 物件模型</span><span class="sxs-lookup"><span data-stu-id="20fcf-124">Update hello Project Object Model</span></span>
1. <span data-ttu-id="20fcf-125">編輯 hello **pom.xml**檔案，然後加入下列程式碼內 hello hello `<dependencies>` > 一節：</span><span class="sxs-lookup"><span data-stu-id="20fcf-125">Edit hello **pom.xml** file and add hello following code inside hello `<dependencies>` section:</span></span>

        <dependency>
          <groupId>org.apache.hbase</groupId>
          <artifactId>hbase-client</artifactId>
          <version>1.1.2</version>
        </dependency>

    <span data-ttu-id="20fcf-126">本節說明需要 hello 專案的 Maven **hbase 用戶端**版本**1.1.2**。</span><span class="sxs-lookup"><span data-stu-id="20fcf-126">This section tells Maven that hello project requires **hbase-client** version **1.1.2**.</span></span> <span data-ttu-id="20fcf-127">在編譯時期，從 hello 預設 Maven 儲存機制下載此相依性。</span><span class="sxs-lookup"><span data-stu-id="20fcf-127">At compile time, this dependency is downloaded from hello default Maven repository.</span></span> <span data-ttu-id="20fcf-128">您可以使用 hello [Maven 中央儲存機制搜尋](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar)toolearn 更多關於此相依性。</span><span class="sxs-lookup"><span data-stu-id="20fcf-128">You can use hello [Maven Central Repository Search](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn more about this dependency.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="20fcf-129">hello 版本號碼必須符合所提供的 HDInsight 叢集的 HBase hello 版本。</span><span class="sxs-lookup"><span data-stu-id="20fcf-129">hello version number must match hello version of HBase that is provided with your HDInsight cluster.</span></span> <span data-ttu-id="20fcf-130">使用下列資料表 toofind hello 正確的版本號碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="20fcf-130">Use hello following table toofind hello correct version number.</span></span>
   >
   >

   | <span data-ttu-id="20fcf-131">HDInsight 叢集版本</span><span class="sxs-lookup"><span data-stu-id="20fcf-131">HDInsight cluster version</span></span> | <span data-ttu-id="20fcf-132">對 HBase 版本 toouse</span><span class="sxs-lookup"><span data-stu-id="20fcf-132">HBase version toouse</span></span> |
   | --- | --- |
   | <span data-ttu-id="20fcf-133">3.2</span><span class="sxs-lookup"><span data-stu-id="20fcf-133">3.2</span></span> |<span data-ttu-id="20fcf-134">0.98.4-hadoop2</span><span class="sxs-lookup"><span data-stu-id="20fcf-134">0.98.4-hadoop2</span></span> |
   | <span data-ttu-id="20fcf-135">3.3</span><span class="sxs-lookup"><span data-stu-id="20fcf-135">3.3</span></span> |<span data-ttu-id="20fcf-136">1.1.2</span><span class="sxs-lookup"><span data-stu-id="20fcf-136">1.1.2</span></span> |

    <span data-ttu-id="20fcf-137">如需有關 HDInsight 版本和元件的詳細資訊，請參閱[為何 hello 不同 Hadoop 元件適用於 HDInsight](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="20fcf-137">For more information on HDInsight versions and components, see [What are hello different Hadoop components available with HDInsight](hdinsight-component-versioning.md).</span></span>
2. <span data-ttu-id="20fcf-138">如果您使用 HDInsight 3.3 叢集，您也必須加入下列 toohello hello `<dependencies>` > 一節：</span><span class="sxs-lookup"><span data-stu-id="20fcf-138">If you are using an HDInsight 3.3 cluster, you must also add hello following toohello `<dependencies>` section:</span></span>

        <dependency>
            <groupId>org.apache.phoenix</groupId>
            <artifactId>phoenix-core</artifactId>
            <version>4.4.0-HBase-1.1</version>
        </dependency>

    <span data-ttu-id="20fcf-139">此相依性會載入 hello in phoenix 核心元件，Hbase 版本所使用的 1.1.x。</span><span class="sxs-lookup"><span data-stu-id="20fcf-139">This dependency will load hello phoenix-core components, which are used by Hbase version 1.1.x.</span></span>
3. <span data-ttu-id="20fcf-140">新增下列程式碼 toohello hello **pom.xml**檔案。</span><span class="sxs-lookup"><span data-stu-id="20fcf-140">Add hello following code toohello **pom.xml** file.</span></span> <span data-ttu-id="20fcf-141">此區段必須是內部 hello `<project>...</project>` hello 中的標記檔案，例如之間`</dependencies>`和`</project>`。</span><span class="sxs-lookup"><span data-stu-id="20fcf-141">This section must be inside hello `<project>...</project>` tags in hello file, for example, between `</dependencies>` and `</project>`.</span></span>

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
                    <source>1.7</source>
                    <target>1.7</target>
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

    <span data-ttu-id="20fcf-142">hello`<resources>`區段設定資源 (**conf\hbase site.xml**)，其中包含 HBase 組態資訊。</span><span class="sxs-lookup"><span data-stu-id="20fcf-142">hello `<resources>` section configures a resource (**conf\hbase-site.xml**) that contains configuration information for HBase.</span></span>

   > [!NOTE]
   > <span data-ttu-id="20fcf-143">您也可以透過程式碼來設定組態值。</span><span class="sxs-lookup"><span data-stu-id="20fcf-143">You can also set configuration values via code.</span></span> <span data-ttu-id="20fcf-144">請參閱 hello 註解中 hello **CreateTable**範例所示的方式 toodo 這。</span><span class="sxs-lookup"><span data-stu-id="20fcf-144">See hello comments in hello **CreateTable** example that follows for how toodo this.</span></span>
   >
   >

    <span data-ttu-id="20fcf-145">這`<plugins>`區段設定 hello [Maven 編譯器外掛程式](http://maven.apache.org/plugins/maven-compiler-plugin/)和[Maven 陰影外掛程式](http://maven.apache.org/plugins/maven-shade-plugin/)。</span><span class="sxs-lookup"><span data-stu-id="20fcf-145">This `<plugins>` section configures hello [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) and [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span></span> <span data-ttu-id="20fcf-146">hello 編譯器外掛程式會使用的 toocompile hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="20fcf-146">hello compiler plug-in is used toocompile hello topology.</span></span> <span data-ttu-id="20fcf-147">hello 陰影外掛程式會使用的 tooprevent 授權重複，Maven 建置 hello JAR 封裝中。</span><span class="sxs-lookup"><span data-stu-id="20fcf-147">hello shade plug-in is used tooprevent license duplication in hello JAR package that is built by Maven.</span></span> <span data-ttu-id="20fcf-148">這用 hello 原因是 hello 重複的授權檔案會導致 hello HDInsight 叢集上的執行階段錯誤。</span><span class="sxs-lookup"><span data-stu-id="20fcf-148">hello reason this is used is that hello duplicate license files cause an error at run time on hello HDInsight cluster.</span></span> <span data-ttu-id="20fcf-149">使用 maven-網底-外掛程式以 hello`ApacheLicenseResourceTransformer`實作會避免這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="20fcf-149">Using maven-shade-plugin with hello `ApacheLicenseResourceTransformer` implementation prevents this error.</span></span>

    <span data-ttu-id="20fcf-150">hello maven-網底-外掛程式也會產生超級 jar （或 fat jar），其中包含所有 hello 應用程式所需的 hello 相依性。</span><span class="sxs-lookup"><span data-stu-id="20fcf-150">hello maven-shade-plugin also produces an uber jar (or fat jar) that contains all hello dependencies required by hello application.</span></span>
4. <span data-ttu-id="20fcf-151">儲存 hello **pom.xml**檔案。</span><span class="sxs-lookup"><span data-stu-id="20fcf-151">Save hello **pom.xml** file.</span></span>
5. <span data-ttu-id="20fcf-152">建立新的目錄名稱為**conf**在 hello **hbaseapp**目錄。</span><span class="sxs-lookup"><span data-stu-id="20fcf-152">Create a new directory named **conf** in hello **hbaseapp** directory.</span></span> <span data-ttu-id="20fcf-153">在 hello **conf**目錄中，建立名為**hbase-site.xml**。</span><span class="sxs-lookup"><span data-stu-id="20fcf-153">In hello **conf** directory, create a file named **hbase-site.xml**.</span></span> <span data-ttu-id="20fcf-154">使用下列 hello 做為 hello hello 檔案內容：</span><span class="sxs-lookup"><span data-stu-id="20fcf-154">Use hello following as hello contents of hello file:</span></span>

        <?xml version="1.0"?>
        <?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
        <!--
        /**
          * Copyright 2010 hello Apache Software Foundation
          *
          * Licensed toohello Apache Software Foundation (ASF) under one
          * or more contributor license agreements.  See hello NOTICE file
          * distributed with this work for additional information
          * regarding copyright ownership.  hello ASF licenses this file
          * tooyou under hello Apache License, Version 2.0 (the
          * "License"); you may not use this file except in compliance
          * with hello License.  You may obtain a copy of hello License at
          *
          *     http://www.apache.org/licenses/LICENSE-2.0
          *
          * Unless required by applicable law or agreed tooin writing, software
          * distributed under hello License is distributed on an "AS IS" BASIS,
          * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
          * See hello License for hello specific language governing permissions and
          * limitations under hello License.
          */
        -->
        <configuration>
          <property>
            <name>hbase.cluster.distributed</name>
            <value>true</value>
          </property>
          <property>
            <name>hbase.zookeeper.quorum</name>
            <value>zookeeper0,zookeeper1,zookeeper2</value>
          </property>
          <property>
            <name>hbase.zookeeper.property.clientPort</name>
            <value>2181</value>
          </property>
        </configuration>

    <span data-ttu-id="20fcf-155">這個檔案將會使用的 tooload hello HBase 組態的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="20fcf-155">This file will be used tooload hello HBase configuration for an HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="20fcf-156">這是最小 hbase-site.xml 檔案，而且包含 hello 裸機的最小設定 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="20fcf-156">This is a minimal hbase-site.xml file, and it contains hello bare minimum settings for hello HDInsight cluster.</span></span>

6. <span data-ttu-id="20fcf-157">儲存 hello **hbase-site.xml**檔案。</span><span class="sxs-lookup"><span data-stu-id="20fcf-157">Save hello **hbase-site.xml** file.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="20fcf-158">建立 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="20fcf-158">Create hello application</span></span>
1. <span data-ttu-id="20fcf-159">移 toohello **hbaseapp\src\main\java\com\microsoft\examples**目錄和重新命名 hello app.java 檔案太**CreateTable.java**。</span><span class="sxs-lookup"><span data-stu-id="20fcf-159">Go toohello **hbaseapp\src\main\java\com\microsoft\examples** directory and rename hello app.java file too**CreateTable.java**.</span></span>
2. <span data-ttu-id="20fcf-160">開啟 hello **CreateTable.java**檔案，然後以下列程式碼的 hello 取代 hello 現有內容：</span><span class="sxs-lookup"><span data-stu-id="20fcf-160">Open hello **CreateTable.java** file and replace hello existing contents with hello following code:</span></span>

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
            // hello following sets hello znode root for Linux-based HDInsight
            //config.set("zookeeper.znode.parent","/hbase-unsecure");

            // create an admin object using hello config
            HBaseAdmin admin = new HBaseAdmin(config);

            // create hello table...
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

            // Add each person toohello table
            //   Use hello `name` column family for hello name
            //   Use hello `contactinfo` column family for hello email
            for (int i = 0; i< people.length; i++) {
              Put person = new Put(Bytes.toBytes(people[i][0]));
              person.add(Bytes.toBytes("name"), Bytes.toBytes("first"), Bytes.toBytes(people[i][1]));
              person.add(Bytes.toBytes("name"), Bytes.toBytes("last"), Bytes.toBytes(people[i][2]));
              person.add(Bytes.toBytes("contactinfo"), Bytes.toBytes("email"), Bytes.toBytes(people[i][3]));
              table.put(person);
            }
            // flush commits and close hello table
            table.flushCommits();
            table.close();
          }
        }

    <span data-ttu-id="20fcf-161">這是 hello **CreateTable**類別，會建立資料表，名為**人員**並填入某些預先定義的使用者。</span><span class="sxs-lookup"><span data-stu-id="20fcf-161">This is hello **CreateTable** class, which will create a table named **people** and populate it with some predefined users.</span></span>
3. <span data-ttu-id="20fcf-162">儲存 hello **CreateTable.java**檔案。</span><span class="sxs-lookup"><span data-stu-id="20fcf-162">Save hello **CreateTable.java** file.</span></span>
4. <span data-ttu-id="20fcf-163">在 hello **hbaseapp\src\main\java\com\microsoft\examples**目錄中，建立新的檔案命名為**SearchByEmail.java**。</span><span class="sxs-lookup"><span data-stu-id="20fcf-163">In hello **hbaseapp\src\main\java\com\microsoft\examples** directory, create a new file named **SearchByEmail.java**.</span></span> <span data-ttu-id="20fcf-164">使用下列程式碼做為此檔案的 hello 內容 hello:</span><span class="sxs-lookup"><span data-stu-id="20fcf-164">Use hello following code as hello contents of this file:</span></span>

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

            // Use GenericOptionsParser tooget only hello parameters toohello class
            // and not all hello parameters passed (when using WebHCat for example)
            String[] otherArgs = new GenericOptionsParser(config, args).getRemainingArgs();
            if (otherArgs.length != 1) {
              System.out.println("usage: [regular expression]");
              System.exit(-1);
            }

            // Open hello table
            HTable table = new HTable(config, "people");

            // Define hello family and qualifiers toobe used
            byte[] contactFamily = Bytes.toBytes("contactinfo");
            byte[] emailQualifier = Bytes.toBytes("email");
            byte[] nameFamily = Bytes.toBytes("name");
            byte[] firstNameQualifier = Bytes.toBytes("first");
            byte[] lastNameQualifier = Bytes.toBytes("last");

            // Create a new regex filter
            RegexStringComparator emailFilter = new RegexStringComparator(otherArgs[0]);
            // Attach hello regex filter tooa filter
            //   for hello email column
            SingleColumnValueFilter filter = new SingleColumnValueFilter(
              contactFamily,
              emailQualifier,
              CompareOp.EQUAL,
              emailFilter
            );

            // Create a scan and set hello filter
            Scan scan = new Scan();
            scan.setFilter(filter);

            // Get hello results
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

    <span data-ttu-id="20fcf-165">hello **SearchByEmail**類別可以使用的 tooquery 由電子郵件地址的資料列。</span><span class="sxs-lookup"><span data-stu-id="20fcf-165">hello **SearchByEmail** class can be used tooquery for rows by email address.</span></span> <span data-ttu-id="20fcf-166">因為它使用規則運算式篩選時，可以在使用 hello 類別時，提供字串或規則運算式。</span><span class="sxs-lookup"><span data-stu-id="20fcf-166">Because it uses a regular expression filter, you can provide either a string or a regular expression when using hello class.</span></span>
5. <span data-ttu-id="20fcf-167">儲存 hello **SearchByEmail.java**檔案。</span><span class="sxs-lookup"><span data-stu-id="20fcf-167">Save hello **SearchByEmail.java** file.</span></span>
6. <span data-ttu-id="20fcf-168">在 hello **hbaseapp\src\main\hava\com\microsoft\examples**目錄中，建立新的檔案命名為**DeleteTable.java**。</span><span class="sxs-lookup"><span data-stu-id="20fcf-168">In hello **hbaseapp\src\main\hava\com\microsoft\examples** directory, create a new file named **DeleteTable.java**.</span></span> <span data-ttu-id="20fcf-169">使用下列程式碼做為此檔案的 hello 內容 hello:</span><span class="sxs-lookup"><span data-stu-id="20fcf-169">Use hello following code as hello contents of this file:</span></span>

        package com.microsoft.examples;
        import java.io.IOException;

        import org.apache.hadoop.conf.Configuration;
        import org.apache.hadoop.hbase.HBaseConfiguration;
        import org.apache.hadoop.hbase.client.HBaseAdmin;

        public class DeleteTable {
          public static void main(String[] args) throws IOException {
            Configuration config = HBaseConfiguration.create();

            // Create an admin object using hello config
            HBaseAdmin admin = new HBaseAdmin(config);

            // Disable, and then delete hello table
            admin.disableTable("people");
            admin.deleteTable("people");
          }
        }

    <span data-ttu-id="20fcf-170">這個類別是清除此範例中，停用和卸除 hello 資料表建立 hello **CreateTable**類別。</span><span class="sxs-lookup"><span data-stu-id="20fcf-170">This class is for cleaning up this example by disabling and dropping hello table created by hello **CreateTable** class.</span></span>
7. <span data-ttu-id="20fcf-171">儲存 hello **DeleteTable.java**檔案。</span><span class="sxs-lookup"><span data-stu-id="20fcf-171">Save hello **DeleteTable.java** file.</span></span>

## <a name="build-and-package-hello-application"></a><span data-ttu-id="20fcf-172">建置和封裝 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="20fcf-172">Build and package hello application</span></span>
1. <span data-ttu-id="20fcf-173">開啟命令提示字元並變更目錄 toohello **hbaseapp**目錄。</span><span class="sxs-lookup"><span data-stu-id="20fcf-173">Open a command prompt and change directories toohello **hbaseapp** directory.</span></span>
2. <span data-ttu-id="20fcf-174">使用下列命令 toobuild JAR 檔案，其中包含 hello 應用程式的 hello:</span><span class="sxs-lookup"><span data-stu-id="20fcf-174">Use hello following command toobuild a JAR file that contains hello application:</span></span>

        mvn clean package

    <span data-ttu-id="20fcf-175">這會清除任何先前的組建成品、 下載尚未安裝任何相依性，然後建置並封裝 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="20fcf-175">This cleans any previous build artifacts, downloads any dependencies that have not already been installed, then builds and packages hello application.</span></span>
3. <span data-ttu-id="20fcf-176">Hello 命令完成時，hello **hbaseapp\target**目錄包含名為**hbaseapp-1.0-SNAPSHOT.jar**。</span><span class="sxs-lookup"><span data-stu-id="20fcf-176">When hello command completes, hello **hbaseapp\target** directory contains a file named **hbaseapp-1.0-SNAPSHOT.jar**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="20fcf-177">hello **hbaseapp-1.0-SNAPSHOT.jar**檔案是超級 jar （有時稱為 fat jar，） 包含所有 hello 相依性所需 toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="20fcf-177">hello **hbaseapp-1.0-SNAPSHOT.jar** file is an uber jar (sometimes called a fat jar,) which contains all hello dependencies required toorun hello application.</span></span>

## <a name="upload-hello-jar-file-and-start-a-job"></a><span data-ttu-id="20fcf-178">上傳 hello JAR 檔案，並啟動工作</span><span class="sxs-lookup"><span data-stu-id="20fcf-178">Upload hello JAR file and start a job</span></span>
<span data-ttu-id="20fcf-179">有許多方式 tooupload 檔案 tooyour HDInsight 叢集中所述[HDInsight 中的 Hadoop 工作的資料上傳](hdinsight-upload-data.md)。</span><span class="sxs-lookup"><span data-stu-id="20fcf-179">There are many ways tooupload a file tooyour HDInsight cluster, as described in [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span> <span data-ttu-id="20fcf-180">hello 下列步驟使用 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="20fcf-180">hello following steps use Azure PowerShell.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

1. <span data-ttu-id="20fcf-181">安裝並設定 Azure PowerShell 之後，建立名為 **hbase-runner.psm1** 的新檔案。</span><span class="sxs-lookup"><span data-stu-id="20fcf-181">After installing and configuring Azure PowerShell, create a new file named **hbase-runner.psm1**.</span></span> <span data-ttu-id="20fcf-182">使用此檔案的 hello 內容 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="20fcf-182">Use hello following as hello contents of this file:</span></span>

        <#
        .SYNOPSIS
        Copies a file toohello primary storage of an HDInsight cluster.
        .DESCRIPTION
        Copies a file from a local directory toohello blob container for
        hello HDInsight cluster.
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
        #hello class toorun
        [Parameter(Mandatory = $true)]
        [String]$className,

        #hello name of hello HDInsight cluster
        [Parameter(Mandatory = $true)]
        [String]$clusterName,

        #Only used when using SearchByEmail
        [Parameter(Mandatory = $false)]
        [String]$emailRegex,

        #Use if you want toosee stderr output
        [Parameter(Mandatory = $false)]
        [Switch]$showErr
        )

        Set-StrictMode -Version 3

        # Is hello Azure module installed?
        FindAzure

        # Get hello login for hello HDInsight cluster
        $creds=Get-Credential -Message "Enter hello login for hello cluster" -UserName "admin"

        # hello JAR
        $jarFile = "wasb:///example/jars/hbaseapp-1.0-SNAPSHOT.jar"

        # hello job definition
        $jobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
            -JarFile $jarFile `
            -ClassName $className `
            -Arguments $emailRegex

        # Get hello job output
        $job = Start-AzureRmHDInsightJob `
            -ClusterName $clusterName `
            -JobDefinition $jobDefinition `
            -HttpCredential $creds
        Write-Host "Wait for hello job toocomplete ..." -ForegroundColor Green
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
        Write-Host "Display hello standard output ..." -ForegroundColor Green
        Get-AzureRmHDInsightJobOutput `
                    -Clustername $clusterName `
                    -JobId $job.JobId `
                    -HttpCredential $creds
        }

        <#
        .SYNOPSIS
        Copies a file toohello primary storage of an HDInsight cluster.
        .DESCRIPTION
        Copies a file from a local directory toohello blob container for
        hello HDInsight cluster.
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
                #hello path toohello local file.
                [Parameter(Mandatory = $true)]
                [String]$localPath,

                #hello destination path and file name, relative toohello root of hello container.
                [Parameter(Mandatory = $true)]
                [String]$destinationPath,

                #hello name of hello HDInsight cluster
                [Parameter(Mandatory = $true)]
                [String]$clusterName,

                #If specified, overwrites existing files without prompting
                [Parameter(Mandatory = $false)]
                [Switch]$force
            )

            Set-StrictMode -Version 3

            # Is hello Azure module installed?
            FindAzure

            # Get authentication for hello cluster
            $creds=Get-Credential

            # Does hello local path exist?
            if (-not (Test-Path $localPath))
            {
                throw "Source path '$localPath' does not exist."
            }

            # Get hello primary storage container
            $storage = GetStorage -clusterName $clusterName

            # Upload file toostorage, overwriting existing files if -force was used.
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
                throw "No active Azure subscription found! If you have a subscription, use hello Login-AzureRmAccount cmdlet toologin tooyour subscription."
            }
        }

        function GetStorage {
            param(
                [Parameter(Mandatory = $true)]
                [String]$clusterName
            )
            $hdi = Get-AzureRmHDInsightCluster -ClusterName $clusterName
            # Does hello cluster exist?
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
            # Get hello resource group, in case we need that
            $return.resourceGroup = $resourceGroup
            # Get hello storage context, as we can't depend
            # on using hello default storage context
            $return.context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
            # Get hello container, so we know where to
            # find/store blobs
            $return.container = $container
            # Return storage accounts toosupport finding all accounts for
            # a cluster
            $return.storageAccount = $storageAccountName
            $return.storageAccountKey = $storageAccountKey

            return $return
        }
        # Only export hello verb-phrase things
        export-modulemember *-*

    <span data-ttu-id="20fcf-183">此檔案包含兩個模組：</span><span class="sxs-lookup"><span data-stu-id="20fcf-183">This file contains two modules:</span></span>

   * <span data-ttu-id="20fcf-184">**新增 HDInsightFile** -使用 tooupload 檔案 tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="20fcf-184">**Add-HDInsightFile** - used tooupload files tooHDInsight</span></span>
   * <span data-ttu-id="20fcf-185">**開始 HBaseExample** -使用稍早建立的 toorun hello 類別</span><span class="sxs-lookup"><span data-stu-id="20fcf-185">**Start-HBaseExample** - used toorun hello classes created earlier</span></span>
2. <span data-ttu-id="20fcf-186">儲存 hello **hbase runner.psm1**檔案。</span><span class="sxs-lookup"><span data-stu-id="20fcf-186">Save hello **hbase-runner.psm1** file.</span></span>
3. <span data-ttu-id="20fcf-187">開啟新的 Azure PowerShell 視窗，將變更目錄 toohello **hbaseapp**目錄，然後執行的 hello 遵從命令。</span><span class="sxs-lookup"><span data-stu-id="20fcf-187">Open a new Azure PowerShell window, change directories toohello **hbaseapp** directory, and then run hello following command.</span></span>

        PS C:\ Import-Module c:\path\to\hbase-runner.psm1

    <span data-ttu-id="20fcf-188">變更 hello hello 路徑 toohello 位置**hbase runner.psm1**稍早建立的檔案。</span><span class="sxs-lookup"><span data-stu-id="20fcf-188">Change hello path toohello location of hello **hbase-runner.psm1** file created earlier.</span></span> <span data-ttu-id="20fcf-189">這會註冊此 Azure PowerShell 工作階段的 hello 模組。</span><span class="sxs-lookup"><span data-stu-id="20fcf-189">This registers hello module for this Azure PowerShell session.</span></span>
4. <span data-ttu-id="20fcf-190">使用 hello 下列命令 tooupload hello **hbaseapp-1.0-SNAPSHOT.jar** tooyour HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="20fcf-190">Use hello following command tooupload hello **hbaseapp-1.0-SNAPSHOT.jar** tooyour HDInsight cluster.</span></span>

        Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername

    <span data-ttu-id="20fcf-191">取代**hdinsightclustername** hello 名稱，為您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="20fcf-191">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span> <span data-ttu-id="20fcf-192">hello 命令會將上傳 hello **hbaseapp-1.0-SNAPSHOT.jar** toohello **（範例/每瓶)** hello 您的 HDInsight 叢集的主要儲存體中的位置。</span><span class="sxs-lookup"><span data-stu-id="20fcf-192">hello command uploads hello **hbaseapp-1.0-SNAPSHOT.jar** toohello **example/jars** location in hello primary storage for your HDInsight cluster.</span></span>
5. <span data-ttu-id="20fcf-193">Hello 檔案上傳之後，使用 hello 下列程式碼 toocreate 資料表使用 hello **hbaseapp**:</span><span class="sxs-lookup"><span data-stu-id="20fcf-193">After hello files are uploaded, use hello following code toocreate a table using hello **hbaseapp**:</span></span>

        Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername

    <span data-ttu-id="20fcf-194">取代**hdinsightclustername** hello 名稱，為您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="20fcf-194">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="20fcf-195">此命令會在 HDInsight 叢集中建立名為 **people** 的新資料表。</span><span class="sxs-lookup"><span data-stu-id="20fcf-195">This command creates a new table named **people** in your HDInsight cluster.</span></span> <span data-ttu-id="20fcf-196">此命令不會顯示 hello 主控台視窗中的任何輸出。</span><span class="sxs-lookup"><span data-stu-id="20fcf-196">This command does not show any output in hello console window.</span></span>
6. <span data-ttu-id="20fcf-197">項目在 hello 資料表中，下列命令使用 hello toosearch:</span><span class="sxs-lookup"><span data-stu-id="20fcf-197">toosearch for entries in hello table, use hello following command:</span></span>

        Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com

    <span data-ttu-id="20fcf-198">取代**hdinsightclustername** hello 名稱，為您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="20fcf-198">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="20fcf-199">此命令會使用 hello **SearchByEmail**類別 toosearch 任何資料列，其中 hello **contactinformation**資料欄系列和 hello**電子郵件**資料行，包含 hello 字串**contoso.com**。您應該會收到 hello 下列結果：</span><span class="sxs-lookup"><span data-stu-id="20fcf-199">This command uses hello **SearchByEmail** class toosearch for any rows where hello **contactinformation** column family and hello **email** column, contains hello string **contoso.com**. You should receive hello following results:</span></span>

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    <span data-ttu-id="20fcf-200">使用**fabrikam.com** hello`-emailRegex`值會傳回具有 hello 使用者**fabrikam.com** hello 電子郵件欄位中。</span><span class="sxs-lookup"><span data-stu-id="20fcf-200">Using **fabrikam.com** for hello `-emailRegex` value returns hello users that have **fabrikam.com** in hello email field.</span></span> <span data-ttu-id="20fcf-201">因為這個搜尋藉由使用規則運算式為基礎的篩選，您也可以輸入規則運算式，例如**^ r**，hello 電子郵件會開頭 hello 字母 'r' 的傳回項目。</span><span class="sxs-lookup"><span data-stu-id="20fcf-201">Since this search is implemented by using a regular expression-based filter, you can also enter regular expressions, such as **^r**, which returns entries where hello email begins with hello letter 'r'.</span></span>

## <a name="delete-hello-table"></a><span data-ttu-id="20fcf-202">刪除 hello 資料表</span><span class="sxs-lookup"><span data-stu-id="20fcf-202">Delete hello table</span></span>
<span data-ttu-id="20fcf-203">當您完成 hello 範例之後時，使用 hello 下列命令從 hello Azure PowerShell 工作階段 toodelete hello**人員**此範例中使用的資料表：</span><span class="sxs-lookup"><span data-stu-id="20fcf-203">When you are done with hello example, use hello following command from hello Azure PowerShell session toodelete hello **people** table used in this example:</span></span>

    Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername

<span data-ttu-id="20fcf-204">取代**hdinsightclustername** hello 名稱，為您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="20fcf-204">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="20fcf-205">疑難排解</span><span class="sxs-lookup"><span data-stu-id="20fcf-205">Troubleshooting</span></span>
### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a><span data-ttu-id="20fcf-206">使用 Start-HBaseExample 時沒有結果或傳回非預期的結果</span><span class="sxs-lookup"><span data-stu-id="20fcf-206">No results or unexpected results when using Start-HBaseExample</span></span>
<span data-ttu-id="20fcf-207">使用 hello`-showErr`參數 tooview hello 標準錯誤 (STDERR) 在執行中的 hello 作業時所產生之。</span><span class="sxs-lookup"><span data-stu-id="20fcf-207">Use hello `-showErr` parameter tooview hello standard error (STDERR) that is produced while running hello job.</span></span>
