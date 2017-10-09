---
title: "aaaJava HBase 用戶端-Azure HDInsight |Microsoft 文件"
description: "深入了解如何 toouse Apache Maven Java 為基礎的 toobuild Apache HBase 應用程式，然後將它部署在 Azure HDInsight 上的 tooHBase。"
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
ms.openlocfilehash: 41ef92b2900280dd59089c4fa40686c44133b337
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="build-java-applications-for-apache-hbase"></a>建置 Apache HBase 的 Java 應用程式

深入了解如何 toocreate [Apache HBase](http://hbase.apache.org/) java 應用程式。 然後使用 Azure HDInsight 上的 HBase hello 應用程式。

此文件的使用中的 hello 步驟[Maven](http://maven.apache.org/) toocreate 與建置 hello 專案。 Maven 是軟體專案管理和理解的工具，可讓您 toobuild 軟體、 文件和 Java 專案的報表。

> [!NOTE]
> hello 本文件中的步驟執行最新測試與 HDInsight 3.6。

> [!IMPORTANT]
> 本文件中的 hello 步驟需要使用 Linux 的 HDInsight 叢集。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

## <a name="requirements"></a>需求

* [Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 或更新版本。

    > [!NOTE]
    > HDInsight 3.5 和更新版本需要 Java 8。 舊版的 HDInsight 需要 Java 7。

* [Maven](http://maven.apache.org/)

* [具有 HBase 的 Linux 型 Azure HDInsight 叢集](hdinsight-hbase-tutorial-get-started-linux.md#create-hbase-cluster)

  > [!NOTE]
  > 本文件中的 hello 步驟已經過測試與 HDInsight 叢集版本 3.4 和 3.5。 提供範例中的 hello 預設值為 HDInsight 3.5 叢集。

## <a name="create-hello-project"></a>建立 hello 專案

1. 從開發環境中的 hello 命令列，變更目錄 toohello 所在的位置 toocreate hello 專案，例如`cd code\hbase`。

2. 使用 hello **mvn**命令，它會隨 Maven，toogenerate hello scaffolding hello 專案。

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

    > [!NOTE]
    > 如果您使用 PowerShell，您必須將 hello`-D`雙引號括住的參數。
    >
    > `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=hbaseapp" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    此命令會建立名稱為 hello 相同的 hello 目錄**artifactID**參數 (**hbaseapp**在此範例中。)此目錄包含下列項目 hello:

   * **pom.xml**: hello Project 物件模型 ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) 包含資訊和設定詳細資料使用 toobuild hello 專案。
   * **src**: hello 目錄，包含 hello **main/java/com/microsoft/範例**目錄中，您用來撰寫 hello 應用程式。

3. 刪除 hello`src/test/java/com/microsoft/examples/apptest.java`檔案。 此範例不會使用此方法。

## <a name="update-hello-project-object-model"></a>更新 hello Project 物件模型

1. 編輯 hello`pom.xml`檔案，然後加入下列程式碼內 hello hello `<dependencies>` > 一節：

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

    本節指出該 hello 專案需要**hbase 用戶端**和**in phoenix 核心**元件。 在編譯時期，這些相依性下載 hello 預設 Maven 儲存機制。 您可以使用 hello [Maven 中央儲存機制搜尋](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar)toolearn 更多關於此相依性。

   > [!IMPORTANT]
   > hello hbase-用戶端 hello 版本號碼必須符合所提供的 HDInsight 叢集的 HBase hello 版本。 使用下列資料表 toofind hello 正確的版本號碼的 hello。

   | HDInsight 叢集版本 | 對 HBase 版本 toouse |
   | --- | --- |
   | 3.2 |0.98.4-hadoop2 |
   | 3.3、3.4、3.5 和 3.6 |1.1.2 |

    如需有關 HDInsight 版本和元件的詳細資訊，請參閱[為何 hello 不同 Hadoop 元件適用於 HDInsight](hdinsight-component-versioning.md)。

3. 新增下列程式碼 toohello hello **pom.xml**檔案。 此文字必須在 hello 內`<project>...</project>`hello 中的標記檔案，例如之間`</dependencies>`和`</project>`。

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

    此區段會設定包含 HBase 組態資訊的資源(`conf/hbase-site.xml`)。

   > [!NOTE]
   > 您也可以透過程式碼來設定組態值。 請參閱 hello 註解中 hello`CreateTable`範例。

    本章節也會設定 hello [Maven 編譯器外掛程式](http://maven.apache.org/plugins/maven-compiler-plugin/)和[Maven 陰影外掛程式](http://maven.apache.org/plugins/maven-shade-plugin/)。 hello 編譯器外掛程式會使用的 toocompile hello 拓撲。 hello 陰影外掛程式會使用的 tooprevent 授權重複，Maven 建置 hello JAR 封裝中。 此外掛程式 hello HDInsight 叢集上的執行階段會使用的 tooprevent"重複授權檔案 」 錯誤。 使用 maven-網底-外掛程式以 hello`ApacheLicenseResourceTransformer`實作會避免 hello 錯誤。

    hello maven 陰影外掛程式也會產生包含所有 hello 應用程式所需的 hello 相依性超級 jar。

4. 儲存 hello`pom.xml`檔案。

5. 建立名為目錄`conf`在 hello`hbaseapp`目錄。 這個目錄是連接 tooHBase 使用的 toohold 組態資訊。

6. 使用 hello 下列命令從 hello HBase 叢集 toohello toocopy hello HBase 組態`conf`目錄。 取代`USERNAME`hello SSH 登入名稱。 將 `CLUSTERNAME` 取代為 HDInsight 叢集名稱：

    ```bash
    scp USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:/etc/hbase/conf/hbase-site.xml ./conf/hbase-site.xml
    ```

   如需使用 `ssh` 和 `scp` 的詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

## <a name="create-hello-application"></a>建立 hello 應用程式

1. 移 toohello`hbaseapp/src/main/java/com/microsoft/examples`目錄和重新命名 hello app.java 檔案太`CreateTable.java`。

2. 開啟 hello`CreateTable.java`檔案，然後以下列文字的 hello 取代 hello 現有內容：

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

        //Linux-based HDInsight clusters use /hbase-unsecure as hello znode parent
        config.set("zookeeper.znode.parent","/hbase-unsecure");

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
   ```

    此程式碼為 hello **CreateTable**類別，會建立名為**人員**並填入某些預先定義的使用者。

3. 儲存 hello`CreateTable.java`檔案。

4. 在 hello`hbaseapp/src/main/java/com/microsoft/examples`目錄中，建立名為`SearchByEmail.java`。 使用 hello hello 這個檔案的內容為下列文字：

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

        // Create a regex filter
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
   ```

    hello **SearchByEmail**類別可以使用的 tooquery 由電子郵件地址的資料列。 因為它使用規則運算式篩選時，可以在使用 hello 類別時，提供字串或規則運算式。

5. 儲存 hello`SearchByEmail.java`檔案。

6. 在 hello`hbaseapp/src/main/hava/com/microsoft/examples`目錄中，建立名為`DeleteTable.java`。 使用 hello hello 這個檔案的內容為下列文字：

   ```java
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
   ```

    這個類別會清除 hello HBase 資料表建立在此範例中，停用和卸除 hello 資料表建立 hello`CreateTable`類別。

7. 儲存 hello`DeleteTable.java`檔案。

## <a name="build-and-package-hello-application"></a>建置和封裝 hello 應用程式

1. 從 hello`hbaseapp`目錄下，使用 hello 下列命令 toobuild 包含 hello 應用程式的 JAR 檔案：

    ```bash
    mvn clean package
    ```

    此命令會建立和封裝 hello 應用程式到檔案。

2. Hello 命令完成時，hello`hbaseapp/target`目錄包含名為`hbaseapp-1.0-SNAPSHOT.jar`。

   > [!NOTE]
   > hello`hbaseapp-1.0-SNAPSHOT.jar`檔案是超級 jar。 它包含所有 hello 相依性需要的 toorun hello 應用程式。


## <a name="upload-hello-jar-and-run-jobs-ssh"></a>上傳 hello JAR，並執行工作 (SSH)

hello 下列步驟使用`scp`toocopy hello JAR toohello 主要前端節點的 HDInsight 叢集上您 HBase。 hello`ssh`命令則使用 tooconnect toohello 叢集並直接在 hello 前端節點上執行 hello 範例。

1. tooupload hello jar toohello 叢集中，下列命令使用 hello:

    ```bash
    scp ./target/hbaseapp-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:hbaseapp-1.0-SNAPSHOT.jar
    ```

    取代`USERNAME`hello SSH 登入名稱。 將 `CLUSTERNAME` 取代為 HDInsight 叢集名稱。

2. tooconnect toohello HBase 叢集使用 hello 下列命令：

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    取代`USERNAME`hello SSH 登入名稱。 將 `CLUSTERNAME` 取代為 HDInsight 叢集名稱。

3. toocreate HBase 資料表使用 hello Java 應用程式，下列命令使用 hello:

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.CreateTable
    ```

    此命令會建立名為 **people** 的 HBase 資料表，並填入資料。

4. 電子郵件地址儲存在 hello 資料表中，下列命令使用 hello toosearch:

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.SearchByEmail contoso.com
    ```

    您會收到 hello 下列結果：

        Franklin Holtz - ID: 2
        Franklin Holtz - franklin@contoso.com - ID: 2
        Rae Schroeder - ID: 4
        Rae Schroeder - rae@contoso.com - ID: 4
        Gabriela Ingram - ID: 6
        Gabriela Ingram - gabriela@contoso.com - ID: 6

5. 下列命令使用 hello toodelete hello 資料表：

    

## <a name="upload-hello-jar-and-run-jobs-powershell"></a>上傳 hello JAR，並執行工作 (PowerShell)

hello 步驟會使用 Azure PowerShell tooupload hello JAR toohello 預設儲存體 HBase 叢集。 HDInsight cmdlet 都使用的 toorun 遠端 hello 範例。

1. 安裝並設定 Azure PowerShell 之後，請建立名為 `hbase-runner.psm1` 的檔案。 使用 hello hello 這個檔案的內容為下列文字：

   ```powershell
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
   ```

    此檔案包含兩個模組：

   * **新增 HDInsightFile** -用 tooupload 檔案 toohello 叢集
   * **開始 HBaseExample** -使用稍早建立的 toorun hello 類別

2. 儲存 hello`hbase-runner.psm1`檔案。

3. 開啟新的 Azure PowerShell 視窗，將變更目錄 toohello`hbaseapp`目錄，然後執行的 hello 遵從命令：

    ```powershell
    PS C:\ Import-Module c:\path\to\hbase-runner.psm1
    ```

    變更 hello hello 路徑 toohello 位置`hbase-runner.psm1`稍早建立的檔案。 此命令會註冊使用 Azure PowerShell hello 模組。

4. 使用 hello 下列命令 tooupload hello `hbaseapp-1.0-SNAPSHOT.jar` tooyour 叢集。

    ```powershell
    Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername
    ```

    取代`hdinsightclustername`與 hello 叢集的名稱。 hello 命令會將上傳 hello `hbaseapp-1.0-SNAPSHOT.jar` toohello `example/jars` hello 您叢集的主要儲存體中的位置。

5. 資料表使用 toocreate hello `hbaseapp`，使用下列命令的 hello:

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername
    ```

    取代`hdinsightclustername`與 hello 叢集的名稱。

    此命令會在您 HDInsight 叢集上的 HBase 中建立名為 **people** 的資料表。 此命令不會顯示 hello 主控台視窗中的任何輸出。

6. 項目在 hello 資料表中，下列命令使用 hello toosearch:

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com
    ```

    取代`hdinsightclustername`與 hello 叢集的名稱。

    此命令會使用 hello`SearchByEmail`類別 toosearch 任何資料列，其中 hello`contactinformation`資料欄系列和 hello`email`資料行，包含字串 hello `contoso.com`。 您應該會收到 hello 下列結果：

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    使用**fabrikam.com** hello`-emailRegex`值會傳回具有 hello 使用者**fabrikam.com** hello 電子郵件欄位中。 您也可以使用規則運算式做為 hello 搜尋詞彙。 例如， **^ r**傳回電子郵件地址開頭 hello 字母 'r'。

### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a>使用 Start-HBaseExample 時沒有結果或傳回非預期的結果

使用 hello`-showErr`參數 tooview hello 標準錯誤 (STDERR) 在執行中的 hello 作業時所產生之。

## <a name="delete-hello-table"></a>刪除 hello 資料表

當您完成 hello 範例之後時，使用下列 toodelete hello hello**人員**此範例中使用的資料表：

__從 `ssh` 工作階段__：

`yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.DeleteTable`

__從 Azure PowerShell__：

`Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername`

## <a name="next-steps"></a>後續步驟

[深入了解如何使用 HBase 松鼠 SQL toouse](hdinsight-hbase-phoenix-squirrel-linux.md)
