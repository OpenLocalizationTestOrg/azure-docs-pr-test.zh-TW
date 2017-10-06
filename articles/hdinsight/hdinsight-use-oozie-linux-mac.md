---
title: "aaaUse Hadoop Oozie 工作流程中以 Linux 為基礎的 HDInsight |Microsoft 文件"
description: "在 Linux 型 HDInsight 上使用 Hadoop Oozie。 深入了解如何 toodefine Oozie 工作流程，並提交 Oozie 作業。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d7603471-5076-43d1-8b9a-dbc4e366ce5d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: larryfr
ms.openlocfilehash: cb5682837543312621e3424b7a9341b5d2a00bf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-oozie-with-hadoop-toodefine-and-run-a-workflow-on-linux-based-hdinsight"></a>使用 Hadoop toodefine Oozie 和 Linux 為基礎的 HDInsight 上執行的工作流程

[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

深入了解如何 toouse Apache Oozie Hadoop HDInsight 上使用。 Apache Oozie 是可管理 Hadoop 工作的工作流程/協調系統。 Oozie hello Hadoop 堆疊，與整合並支援下列作業的 hello:

* Apache MapReduce
* Apache Pig
* Apache Hive
* Apache Sqoop

Oozie 也可以使用的 tooschedule 作業的特定 tooa 系統，例如 Java 程式或殼層指令碼

> [!NOTE]
> 還有另一個選項可以定義與 HDInsight 搭配的工作流程，那就是 Azure Data Factory。 toolearn 深入了解 Azure Data Factory，請參閱[搭配使用 Pig 和 Hive 與 Data Factory][azure-data-factory-pig-hive]。

> [!IMPORTANT]
> Oozie 未在已加入網域的 HDInsight 上啟用。

## <a name="prerequisites"></a>必要條件

* **HDInsight 叢集**：請參閱 [開始使用 Linux 上的 HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)

  > [!IMPORTANT]
  > 本文件中的 hello 步驟需要使用 Linux 的 HDInsight 叢集。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

## <a name="example-workflow"></a>範例工作流程

使用這份文件中的 hello 工作流程包含兩個動作。 動作就是工作的定義，例如執行 Hive、Sqoop、MapReduce 或其他處理序：

![Workflow diagram][img-workflow-diagram]

1. 登錄區動作會在執行下列 HiveQL 指令碼 tooextract 記錄從 hello **hivesampletable**隨附 HDInsight。 每個資料列均代表來自特定行動裝置的瀏覽。 hello 記錄格式會顯示下列文字類似 toohello:

        8       18:54:20        en-US   Android Samsung SCH-i500        California     United States    13.9204007      0       0
        23      19:19:44        en-US   Android HTC     Incredible      Pennsylvania   United States    NULL    0       0
        23      19:19:46        en-US   Android HTC     Incredible      Pennsylvania   United States    1.4757422       0       1

    hello 本文件中使用的 Hive 指令碼計算 hello 總造訪每個平台 （例如 Android 或 iPhone），並會儲存 hello 計數 tooa 新 Hive 資料表。

    如需 Hive 的詳細資訊，請參閱[在 HDInsight 上使用 Hive][hdinsight-use-hive]。

2. Sqoop 動作會將匯出 hello 新 Hive 資料表 tooa 資料表中 Azure SQL database 的 hello 的內容。 如需 Sqoop 的詳細資訊，請參閱[搭配 HDInsight 使用 Hadoop Sqoop][hdinsight-use-sqoop]。

> [!NOTE]
> HDInsight 叢集上支援 Oozie 版本，請參閱[hello HDInsight 所提供的 Hadoop 叢集版本的新][hdinsight-versions]。

## <a name="create-hello-working-directory"></a>建立 hello 工作目錄

Oozie 必須要有資源所需作業 toobe 儲存在 hello 相同目錄。 這個範例會使用 **wasb:///tutorials/useoozie**。 此目錄和 hello 保存 hello 由此工作流程建立新 Hive 資料表的資料目錄，請使用下列命令 toocreate hello:

```
hdfs dfs -mkdir -p /tutorials/useoozie/data
```

> [!NOTE]
> hello`-p`參數會導致 hello 路徑 toobe 建立所有目錄。 hello**資料**目錄是使用的 toohold 資料供 hello **useooziewf.hql**指令碼。

也請執行下列命令，可確保 Oozie 可以模擬使用者帳戶時執行的 Hive 和 Sqoop 工作 hello。 將 **USERNAME** 取代為您的登入名稱：

```
sudo adduser USERNAME users
```

> [!NOTE]
> 您可以忽略錯誤 hello 使用者已屬於 hello`users`群組。

## <a name="add-a-database-driver"></a>新增資料庫驅動程式

由於此工作流程使用 Sqoop tooexport 資料 tooSQL 資料庫，您必須提供一份 hello JDBC 驅動程式使用 tootalk tooSQL 資料庫。 使用 hello 下列命令 toocopy 它 toohello 工作目錄：

```
hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc*.jar /tutorials/useoozie/
```

如果您的工作流程會使用其他資源，例如 jar，包含 MapReduce 應用程式，您需要 tooadd 以及這些資源。

## <a name="define-hello-hive-query"></a>定義 hello Hive 查詢

使用下列步驟 toocreate 下列 HiveQL 指令碼會定義的查詢，在本文件稍後的 Oozie 工作流程中使用的 hello。

1. Toohello 叢集使用 SSH 連線。 hello 下列命令會示範如何使用 hello`ssh`命令。 取代__USERNAME__與 hello SSH 使用者 hello 叢集。 取代__CLUSTERNAME__ hello hello HDInsight 叢集名稱。

    ```
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

2. 從 hello SSH 連線，使用下列命令 toocreate 檔案 hello:

    ```
    nano useooziewf.hql
    ```

3. 一旦 hello nano 編輯器隨即開啟，請使用 hello hello hello 檔案內容為下列查詢：

    ```hiveql
    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(deviceplatform string, count string) ROW FORMAT DELIMITED
    FIELDS TERMINATED BY '\t' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE TABLE ${hiveTableName} SELECT deviceplatform, COUNT(*) as count FROM hivesampletable GROUP BY deviceplatform;
    ```

    有兩個 hello 指令碼中使用的變數：

    * **${hiveTableName}**： 包含建立 hello 資料表 toobe hello 名稱

    * **${hiveDataFolder}**： 包含 hello toostore hello 資料檔案位置 hello 資料表

    hello 工作流程定義檔 (在本教學課程 workflow.xml) 傳遞這些值 toothis 下列 HiveQL 指令碼在執行階段

4. tooexit hello 編輯器 中，按下 Ctrl X。 出現提示時，選取**Y** toosave hello 檔案，然後使用**Enter** toouse hello **useooziewf.hql**檔案名稱。

5. 使用 hello 下列命令 toocopy **useooziewf.hql**太**wasb:///tutorials/useoozie/useooziewf.hql**:

    ```
    hdfs dfs -put useooziewf.hql /tutorials/useoozie/useooziewf.hql
    ```

    這些命令儲存 hello **useooziewf.hql** hello 叢集 hello HDFS 相容存放裝置上的檔案。

## <a name="define-hello-workflow"></a>定義 hello 工作流程

Oozie 工作流程定義是以 hPDL 撰寫 (一種 XML 程序定義語言)。 使用下列步驟 toodefine hello 工作流程的 hello:

1. 使用下列陳述式 toocreate hello 和編輯新檔案：

    ```
    nano workflow.xml
    ```

2. 一旦 hello nano 編輯器隨即開啟，請輸入 hello hello 檔案內容為下列 XML:

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start too= "RunHiveScript"/>
        <action name="RunHiveScript">
        <hive xmlns="uri:oozie:hive-action:0.2">
            <job-tracker>${jobTracker}</job-tracker>
            <name-node>${nameNode}</name-node>
            <configuration>
            <property>
                <name>mapred.job.queue.name</name>
                <value>${queueName}</value>
            </property>
            </configuration>
            <script>${hiveScript}</script>
            <param>hiveTableName=${hiveTableName}</param>
            <param>hiveDataFolder=${hiveDataFolder}</param>
        </hive>
        <ok to="RunSqoopExport"/>
        <error to="fail"/>
        </action>
        <action name="RunSqoopExport">
        <sqoop xmlns="uri:oozie:sqoop-action:0.2">
            <job-tracker>${jobTracker}</job-tracker>
            <name-node>${nameNode}</name-node>
            <configuration>
            <property>
                <name>mapred.compress.map.output</name>
                <value>true</value>
            </property>
            </configuration>
            <arg>export</arg>
            <arg>--connect</arg>
            <arg>${sqlDatabaseConnectionString}</arg>
            <arg>--table</arg>
            <arg>${sqlDatabaseTableName}</arg>
            <arg>--export-dir</arg>
            <arg>${hiveDataFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\t"</arg>
            <archive>sqljdbc41.jar</archive>
            </sqoop>
        <ok to="end"/>
        <error to="fail"/>
        </action>
        <kill name="fail">
        <message>Job failed, error message[${wf:errorMessage(wf:lastErrorNode())}] </message>
        </kill>
        <end name="end"/>
    </workflow-app>
    ```

    有兩個 hello 工作流程中定義的動作：

   * **RunHiveScript**: hello 開始的動作，此動作，並執行 hello **useooziewf.hql** Hive 指令碼

   * **RunSqoopExport**： 這個動作將匯出的 hello 資料所建立的 hello Hive 指令碼 tooSQL Sqoop 資料庫。 這個動作才會執行 hello **RunHiveScript**動作是否成功。

     hello 工作流程中有數個項目，例如`${jobTracker}`。 這些項目會以您在 hello 工作定義中使用的值取代。 在本文件稍後建立 hello 工作定義。

     也請注意 hello `<archive>sqljdbc4.jar</arcive>` hello Sqoop > 一節中的項目。 此項目執行此動作時，指示 Oozie toomake Sqoop 可用在此封存。

3. 然後使用 Ctrl-X **Y**和**Enter** toosave hello 檔案。

4. 使用 hello 下列命令 toocopy hello **workflow.xml**檔案太**/tutorials/useoozie/workflow.xml**:

    ```
    hdfs dfs -put workflow.xml /tutorials/useoozie/workflow.xml
    ```

## <a name="create-hello-database"></a>建立 hello 資料庫

Azure SQL Database，toocreate hello 中步驟 hello[建立 SQL Database](../sql-database/sql-database-get-started.md)文件。 建立 hello 資料庫時，使用`oozietest`與 hello 資料庫名稱。 也請記下 hello hello 資料庫伺服器名稱。

### <a name="create-hello-table"></a>建立 hello 資料表

> [!NOTE]
> 有許多方式 tooconnect tooSQL 資料庫 toocreate 資料表。 hello 下列步驟使用[freetds 才能使用](http://www.freetds.org/)從 hello HDInsight 叢集。


1. 使用下列命令 tooinstall freetds 才能使用 hello HDInsight 叢集上的 hello:

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

2. 一旦安裝 freetds 才能使用之後，使用下列命令 tooconnect toohello SQL Database 伺服器您先前建立的 hello:

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <sqlLogin> -P <sqlPassword> -p 1433 -D oozietest
    ```

    您收到的輸出類似 toohello 下列文字：

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toooozietest
        1>

3. 在 hello`1>`提示字元中，輸入下列行 hello:

    ```
    CREATE TABLE [dbo].[mobiledata](
    [deviceplatform] [nvarchar](50),
    [count] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(deviceplatform)
    GO
    ```

    當 hello`GO`輸入陳述式、 評估 hello 前一個陳述式。 這些陳述式建立了名為**mobiledata** ，會由 hello 工作流程。

    已建立下列 hello 資料表的 tooverify 使用 hello:

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    您會看到下列文字的輸出類似 toohello:

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    oozietest       dbo     mobiledata      BASE TABLE
    ```

4. 輸入`exit`在 hello`1>`提示 tooexit hello tsql 公用程式。

## <a name="create-hello-job-definition"></a>建立 hello 工作定義

hello 工作定義描述 toofind hello workflow.xml 的位置。 它也會描述 where toofind hello 工作流程 （例如 useooziewf.hql。) 所使用的其他檔案它也會定義 hello 值的屬性 hello 工作流程中使用，而且相關聯的檔案。

1. 使用下列命令 tooget hello 完整位址 hello 預設儲存體的 hello。 Hello 設定檔中會使用此位址，在不久後：

    ```
    sed -n '/<name>fs.default/,/<\/value>/p' /etc/hadoop/conf/core-site.xml
    ```

    此命令會傳回下列 XML 的資訊類似 toohello:

    ```xml
    <name>fs.defaultFS</name>
    <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
    ```

    > [!NOTE]
    > 如果 hello HDInsight 叢集會使用 Azure 儲存體為 hello 預設儲存體，hello`<value>`項目內容的開頭`wasb://`。 若改為使用 Azure Data Lake Store，則其開頭將會是 `adl://`。

    儲存 hello hello 內容`<value>`元素，因為它用於 hello 接下來的步驟。

2. 使用下列命令 tooget hello 叢集前端節點的 FQDN 的 hello。 這項資訊可用於 hello JobTracker hello 叢集位址：

    ```
    hostname -f
    ```

    這會傳回資訊的類似 toohello 下列文字：

    ```hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net```

    hello 使用連接埠 hello JobTracker 是 8050，因此 hello 完整位址 toouse hello JobTracker `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`。

3. 使用下列 toocreate hello Oozie 工作定義組態 hello:

    ```
    nano job.xml
    ```

4. 一旦 hello nano 編輯器隨即開啟，請使用 hello hello hello 檔案內容為下列 XML:

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

        <property>
        <name>nameNode</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
        </property>

        <property>
        <name>jobTracker</name>
        <value>JOBTRACKERADDRESS</value>
        </property>

        <property>
        <name>queueName</name>
        <value>default</value>
        </property>

        <property>
        <name>oozie.use.system.libpath</name>
        <value>true</value>
        </property>

        <property>
        <name>hiveScript</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/useooziewf.hql</value>
        </property>

        <property>
        <name>hiveTableName</name>
        <value>mobilecount</value>
        </property>

        <property>
        <name>hiveDataFolder</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/data</value>
        </property>

        <property>
        <name>sqlDatabaseConnectionString</name>
        <value>"jdbc:sqlserver://serverName.database.windows.net;user=adminLogin;password=adminPassword;database=oozietest"</value>
        </property>

        <property>
        <name>sqlDatabaseTableName</name>
        <value>mobiledata</value>
        </property>

        <property>
        <name>user.name</name>
        <value>YourName</value>
        </property>

        <property>
        <name>oozie.wf.application.path</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
    </configuration>
    ```

   * 所有執行個體 **wasb://mycontainer@mystorageaccount.blob.core.windows.net** 預設儲存體之前收到 hello 值。

     > [!WARNING]
     > 如果 hello 路徑`wasb`路徑，您必須使用 hello 完整路徑。 請勿它縮短 toojust `wasb:///`。

   * 取代**JOBTRACKERADDRESS**以 hello 您稍早收到 JobTracker/ResourceManager 位址。
   * 取代**YourName**與 hello HDInsight 叢集的登入名稱。
   * 取代**serverName**， **adminLogin**，和**adminPassword** hello Azure SQL database 的資訊。

     大部分的此檔案中的 hello 資訊是使用的 toopopulate hello 值用於 hello workflow.xml 或 ooziewf.hql 檔 （例如 ${nameNode}。）

     > [!NOTE]
     > hello **oozie.wf.application.path**項目會定義 where toofind hello workflow.xml 檔案，其中包含 hello 工作流程執行此作業。

5. 然後使用 Ctrl-X **Y**和**Enter** toosave hello 檔案。

## <a name="submit-and-manage-hello-job"></a>送出並管理 hello 工作

hello 下列步驟使用 hello Oozie 命令 toosubmit 和管理 Oozie hello 叢集上的工作流程。 hello Oozie 命令是容易使用的介面，透過 hello [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html)。

> [!IMPORTANT]
> 當使用 hello Oozie 命令時，您必須使用 hello FQDN 的 hello HDInsight 叢集前端節點。 這個 FQDN 只能存取從 hello 叢集或 hello 叢集是否在 Azure 虛擬網路上，從 hello 上的其他機器相同網路。


1. 使用下列 tooobtain hello URL toohello Oozie service hello:

    ```
    sed -n '/<name>oozie.base.url/,/<\/value>/p' /etc/oozie/conf/oozie-site.xml
    ```

    這會傳回下列 XML 的資訊類似 toohello:

    ```xml
    <name>oozie.base.url</name>
    <value>http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie</value>
    ```

    hello`http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie`部分是 hello URL toouse 以 hello Oozie 命令。

2. 使用 hello hello url 遵循 toocreate 環境變數，所以您不需 tootype 會針對每個命令：

    ```
    export OOZIE_URL=http://HOSTNAMEt:11000/oozie
    ```

    取代為您稍早收到 hello hello URL。
3. 使用下列 toosubmit hello 作業 hello:

    ```
    oozie job -config job.xml -submit
    ```

    這個命令載入 hello 作業資訊從**job.xml**並將它提交 tooOozie，但無法執行它。

    Hello 命令完成之後，它應該傳回 hello hello 作業識別碼。 例如： `0000005-150622124850154-oozie-oozi-W`。 這個識別碼是使用的 toomanage hello 作業。

4. 使用下列命令的 hello hello 工作檢視 hello 狀態：

    ```
    oozie job -info <JOBID>
    ```

    > [!NOTE]
    > 取代`<JOBID>`hello 上一個步驟中傳回以 hello 識別碼。

    這會傳回資訊的類似 toohello 下列文字：

    ```
    Job ID : 0000005-150622124850154-oozie-oozi-W
    ------------------------------------------------------------------------------------------------------------------------------------
    Workflow Name : useooziewf
    App Path      : wasb:///tutorials/useoozie
    Status        : PREP
    Run           : 0
    User          : USERNAME
    Group         : -
    Created       : 2015-06-22 15:06 GMT
    Started       : -
    Last Modified : 2015-06-22 15:06 GMT
    Ended         : -
    CoordAction ID: -
    ------------------------------------------------------------------------------------------------------------------------------------
    ```

    這項工作的狀態為 `PREP`。 這個狀態表示該 hello 作業所建立，但不是會啟動。

5. 使用下列命令 toostart hello 作業 hello:

    ```
    oozie job -start JOBID
    ```

    > [!NOTE]
    > 取代`<JOBID>`以 hello 識別碼傳回前面。

    如果您檢查 hello 狀態這個命令之後，它處於執行狀態，並傳回 hello 作業中的 hello 動作的資訊。

6. 一旦 hello 工作順利完成，您可以確認 hello 資料產生 toohello SQL 資料庫資料表使用匯出的 hello 下列命令：

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D oozietest
    ```

    在 hello`1>`提示字元中，輸入下列查詢的 hello:

    ```
    SELECT * FROM mobiledata
    GO
    ```

    傳回的 hello 資訊是類似 toohello 下列文字：

        deviceplatform  count
        Android 31591
        iPhone OS       22731
        proprietary development 3
        RIM OS  3464
        Unknown 213
        Windows Phone   1791
        (6 rows affected)

如需有關 hello Oozie 命令的詳細資訊，請參閱[Oozie 命令列工具](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html)。

## <a name="oozie-rest-api"></a>Oozie REST API

hello Oozie REST API 可讓您 toobuild 自己 Oozie 所使用的工具。 hello 下面是有關使用 hello Oozie REST API 的 HDInsight 特定資訊：

* **URI**: hello 可從外部 hello 叢集存取 REST API`https://CLUSTERNAME.azurehdinsight.net/oozie`

* **驗證**: toohello API 使用 hello 叢集 HTTP 帳戶 （管理員） 和密碼進行驗證。 例如：

    ```
    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/oozie/versions
    ```

如需有關使用 hello Oozie REST API 的詳細資訊，請參閱[Oozie Web 服務 API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html)。

## <a name="oozie-web-ui"></a>Oozie Web UI

hello Oozie Web UI hello 叢集上提供網頁 hello Oozie 工作狀態檢視。 hello web UI 可讓您 tooview hello 下列資訊：

* 工作狀態
* 工作定義
* 組態
* Hello 作業中的 hello 動作的圖形
* 記錄檔中的 hello 工作

您也可以檢視工作內的動作詳細資料。

tooaccess hello Oozie Web UI，請使用下列步驟的 hello:

1. 建立 SSH 通道 toohello HDInsight 叢集。 如需資訊，請參閱 hello[使用 SSH 通道，與 HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)文件。

2. 一旦建立通道之後，請 web 瀏覽器中開啟 hello Ambari web UI。 hello URI hello Ambari 站台是**https://CLUSTERNAME.azurehdinsight.net**。 取代**CLUSTERNAME** hello 以 Linux 為基礎的 HDInsight 叢集名稱。

3. 從 hello hello 頁面的左側，選取**Oozie**，然後**快速連結**，最後再**Oozie Web UI**。

    ![hello 功能表的影像](./media/hdinsight-use-oozie-linux-mac/ooziewebuisteps.png)

4. hello Oozie Web UI 的預設值 toodisplaying 執行工作流程工作。 所有的工作流程工作，選取 toosee**所有工作**。

    ![顯示的所有工作](./media/hdinsight-use-oozie-linux-mac/ooziejobs.png)

5. 選取作業 tooview hello 工作的詳細資訊。

    ![工作資訊](./media/hdinsight-use-oozie-linux-mac/jobinfo.png)

6. 從 hello 工作資訊 索引標籤，您可以查看基本作業資訊和 hello hello 作業內的個別動作。 使用 hello 索引標籤頂端 hello 您可以檢視 hello 工作定義，作業設定存取 hello 作業記錄，或檢視導向非循環圖 (DAG) 的 hello 作業。

   * **作業記錄**： 選取 hello **GetLogs**按鈕 tooget hello 作業的所有記錄檔，或使用 hello**輸入的搜尋篩選器**欄位 toofilter 記錄檔

       ![工作記錄](./media/hdinsight-use-oozie-linux-mac/joblog.png)

   * **JobDAG**: hello DAG 是 hello 資料路徑，引導他們完成 hello 工作流程的圖形化概觀

       ![工作 DAG](./media/hdinsight-use-oozie-linux-mac/jobdag.png)

7. 選取其中一個 hello 動作從 hello**作業資訊** 索引標籤會顯示 hello 動作的資訊。 例如，選取 hello **RunHiveScript**動作。

    ![動作資訊](./media/hdinsight-use-oozie-linux-mac/action.png)

8. 您可以看到 hello 動作，例如連結 toohello 詳細資料**主控台 URL**。 這個連結可以在使用的 tooview JobTracker hello 工作資訊。

## <a name="scheduling-jobs"></a>排程工作

hello 協調器可讓您 toospecify 工作的開始、 結束和出現頻率。 toodefine hello 工作流程中，使用下列步驟的 hello 的排程：

1. 遵循 toocreate 名為的檔案使用 hello **coordinator.xml**:

    ```
    nano coordinator.xml
    ```

    使用下列 XML 當做 hello hello 檔案內容的 hello:

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
        <workflow>
            <app-path>${workflowPath}</app-path>
        </workflow>
        </action>
    </coordinator-app>
    ```

    > [!NOTE]
    > hello`${...}`以 hello 工作定義，在執行階段中的值取代變數。 hello 變數包括：
    >
    > * `${coordFrequency}`： 執行 hello 工作的執行個體之間的時間。
    > ** `${coordStart}`: hello 工作開始時間。
    > * `${coordEnd}`: hello 工作結束時間。
    > * `${coordTimezone}`：協調器工作位在固定時區，不受日光節約時間影響 (通常使用 UTC 表示)。 這個時區稱為 hello"Oozie 處理 timezone。 」
    > * `${wfPath}`: hello 路徑 toohello workflow.xml。

2. toosave hello 檔案，請使用 Ctrl-X **Y**，和**Enter**。

3. 使用下列命令 toocopy hello 檔案 toohello 工作目錄為此工作的 hello:

    ```
    hadoop fs -put coordinator.xml /tutorials/useoozie/coordinator.xml
    ```

4. 使用 hello 遵循 toomodify hello **job.xml**檔案：

    ```
    nano job.xml
    ```

    進行下列變更 hello:

   * tooinstruct oozie toorun hello 協調器檔案而不是 hello 工作流程中，變更`<name>oozie.wf.application.path</name>`太`<name>oozie.coord.application.path</name>`。

   * tooset hello `workflowPath` hello 協調器 中，所使用的變數加入下列 XML 的 hello:

        ```xml
        <property>
            <name>workflowPath</name>
            <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
        ```

       取代 hello `wasb://mycontainer@mystorageaccount.blob.core.windows` hello job.xml 檔案中的其他項目中所使用的 hello 值的文字。

   * toodefine hello 開始、 結束和頻率 hello 協調器 中，加入下列 XML 的 hello:

        ```xml
        <property>
            <name>coordStart</name>
            <value>2017-05-10T12:00Z</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>2017-05-12T12:00Z</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>1440</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>UTC</value>
        </property>
        ```

       這些值來設定 hello 開始時間 too12: 00 PM 2017 年 10 hello 的結束時間 tooMay 12，2017年。 hello 間隔為每日執行此作業。 hello 頻率是以分鐘為單位，因此 24 小時 x 60 分鐘 = 1440年分鐘。 最後，hello 時區會設定 tooUTC。

5. 然後使用 Ctrl-X **Y**和**Enter** toosave hello 檔案。

6. 下列命令使用 hello toorun hello 工作：

    ```
    oozie job -config job.xml -run
    ```

    此命令送出，並開始 hello 作業。

7. 如果您瀏覽 hello Oozie Web UI，並選取 hello**協調者作業**索引標籤上，您會看到下列映像的資訊類似 toohello:

    ![協調器工作索引標籤](./media/hdinsight-use-oozie-linux-mac/coordinatorjob.png)

    hello**下一步具體化**項目包含 hello hello 工作執行的下一次。

8. 類似 toohello 舊版工作流程工作，在 hello web UI 中選取 hello 工作項目會顯示 hello 作業有關的資訊：

    ![協調器工作資訊](./media/hdinsight-use-oozie-linux-mac/coordinatorjobinfo.png)

    > [!NOTE]
    > 此映像只會顯示成功執行 hello 作業不是個別 hello 排定的工作流程內的動作。 選取其中一個 hello toosee**動作**項目。

    ![動作資訊](./media/hdinsight-use-oozie-linux-mac/coordinatoractionjob.png)

## <a name="troubleshooting"></a>疑難排解

hello Oozie UI 可讓您 tooview Oozie 記錄檔。 它也包含連結 tooJobTracker 記錄檔中的 hello 工作流程啟動 MapReduce 工作。 如需疑難排解的 hello 模式應該是：

1. 檢視 hello Oozie Web UI 中的工作。

2. 如果沒有錯誤或特定的動作失敗，選取如果 hello hello 動作 toosee**錯誤訊息**欄位提供有關 hello 失敗的詳細資訊。

3. 如果有的話，使用 hello URL hello 動作 tooview 從更多詳細資料 （例如 JobTracker 記錄） hello 動作。

hello 以下是您可能會遇到的特定錯誤及如何 tooresolve 它們。

### <a name="ja009-cannot-initialize-cluster"></a>JA009：無法初始化叢集

**徵兆**: hello 作業狀態變更太**SUSPENDED**。 Hello 工作的詳細資料顯示 hello RunHiveScript 狀態為**START_MANUAL**。 選取 hello 動作會顯示下列錯誤訊息的 hello:

    JA009: Cannot initialize Cluster. Please check your configuration for map

**可能的原因**: hello WASB 位址用於 hello **job.xml**檔案不包含 hello 儲存體容器或儲存體帳戶名稱。 hello WASB 位址格式必須為`wasb://containername@storageaccountname.blob.core.windows.net`。

**解析**： 變更 hello 作業所使用的 hello WASB 位址。

### <a name="ja002-oozie-is-not-allowed-tooimpersonate-ltuser"></a>JA002: Oozie 不允許 tooimpersonate&lt;使用者 >

**徵兆**: hello 作業狀態變更太**SUSPENDED**。 Hello 工作的詳細資料顯示 hello RunHiveScript 狀態為**START_MANUAL**。 選取 hello 動作會顯示下列錯誤訊息的 hello:

    JA002: User: oozie is not allowed tooimpersonate <USER>

**可能的原因**： 目前的權限設定不允許 Oozie tooimpersonate hello 指定使用者帳戶。

**解析**: Oozie hello 中允許 tooimpersonate 使用者**使用者**群組。 使用 hello `groups USERNAME` hello 使用者帳戶的 toosee hello 群組是的成員。 如果 hello 使用者不屬於 hello**使用者**群組中，使用下列命令 tooadd hello 使用者 toohello 群組 hello:

    sudo adduser USERNAME users

> [!NOTE]
> 可能需要幾分鐘的時間才能 HDInsight 辨識該 hello 使用者已新增 toohello 群組。

### <a name="launcher-error-sqoop"></a>啟動器錯誤 (Sqoop)

**徵兆**: hello 作業狀態變更太**KILLED**。 Hello 工作的詳細資料顯示 hello RunSqoopExport 狀態為**錯誤**。 選取 hello 動作會顯示下列錯誤訊息的 hello:

    Launcher ERROR, reason: Main class [org.apache.oozie.action.hadoop.SqoopMain], exit code [1]

**可能的原因**: Sqoop 是無法 tooload hello 資料庫驅動程式需要的 tooaccess hello 資料庫。

**解析**： 當使用 Sqoop 從 Oozie 作業，您必須包含以 hello hello 資料庫驅動程式 hello 作業所使用其他資源 （例如 hello workflow.xml)。 也會參考包含 hello 資料庫驅動程式從 hello hello 封存`<sqoop>...</sqoop>`hello workflow.xml 一節。

比方說，這份文件中的 hello 作業，您會使用 hello 下列步驟：

1. 複製 hello sqljdbc4.1.jar 檔案 toohello /tutorials/useoozie 目錄：

    ```
    hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc41.jar /tutorials/useoozie/sqljdbc41.jar
    ```

2. 修改下列新的一行上述 XML hello workflow.xml tooadd hello `</sqoop>`:

    ```xml
    <archive>sqljdbc41.jar</archive>
    ```

## <a name="next-steps"></a>後續步驟

在本教學課程中，您學到如何 toodefine Oozie 工作流程以及 toorun Oozie 作業。 toolearn 進一步了解使用 HDInsight，請參閱下列文章的 hello:

* [搭配 HDInsight 使用以時間為基礎的 Hadoop Oozie 協調器][hdinsight-oozie-coordinator-time]
* [在 HDInsight 中上傳 Hadoop 作業的資料][hdinsight-upload-data]
* [搭配使用 Sqoop 與 HDInsight 中的 Hadoop][hdinsight-use-sqoop]
* [搭配使用 Hive 與 HDInsight 上的 Hadoop][hdinsight-use-hive]
* [搭配使用 Pig 與 HDInsight 上的 Hadoop][hdinsight-use-pig]
* [開發 HDInsight 的 Java MapReduce 程式][hdinsight-develop-mapreduce]

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563
[azure-data-factory-pig-hive]: ../data-factory/data-factory-data-transformation-activities.md
[hdinsight-oozie-coordinator-time]: hdinsight-use-oozie-coordinator-time.md
[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-use-blob-storage.md
[hdinsight-get-started]: hdinsight-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop-mac-linux.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-use-blob-storage.md
[hdinsight-get-started-emulator]: hdinsight-get-started-emulator.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[sqldatabase-create-configue]: sql-database-create-configure.md
[sqldatabase-get-started]: sql-database-get-started.md

[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: https://technet.microsoft.com/en-us/library/ee176961.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: ./media/hdinsight-use-oozie/HDI.UseOozie.RunWF.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
