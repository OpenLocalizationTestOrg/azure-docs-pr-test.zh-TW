---
title: "透過 hello JDBC 驅動程式的 Azure HDInsight 的 Hive aaaQuery |Microsoft 文件"
description: "HDInsight 上使用從 Java 應用程式 toosubmit Hive 查詢 tooHadoop hello JDBC 驅動程式。 以程式設計的方式和從 hello 松鼠 SQL 用戶端連接。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 928f8d2a-684d-48cb-894c-11c59a5599ae
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 93178da3b8d497faa4c788e91dba89c4e45d3fff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="query-hive-through-hello-jdbc-driver-in-hdinsight"></a>Hive 查詢透過 HDInsight 中的 hello JDBC 驅動程式

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

了解如何從 Java 應用程式 toosubmit Hive toouse hello JDBC 驅動程式查詢 Azure HDInsight 中的 tooHadoop。 本文件中的 hello 資訊會示範如何 tooconnect 以程式設計的方式與 hello 松鼠 SQL 用戶端。

如需有關 hello Hive JDBC 介面的詳細資訊，請參閱[HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface)。

## <a name="prerequisites"></a>必要條件

* HDInsight 叢集上的 Hadoop。 以 Linux 或 Windows 為基礎的叢集都可運作。

  > [!IMPORTANT]
  > Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [HDInsight 3.3 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

* [SQuirreL SQL](http://squirrel-sql.sourceforge.net/)。 SQuirreL 是 JDBC 用戶端應用程式。

* hello [Java Developer Kit (JDK) 第 7 版](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)或更高版本。

* [Apache Maven](https://maven.apache.org)。 Maven 是專案建立 Java 專案由與此發行項相關聯的 hello 專案的系統。

## <a name="jdbc-connection-string"></a>JDBC 連接字串

JDBC 連接 tooan HDInsight 叢集在 Azure 上的超過 443，會使用 SSL 來保護 hello 流量。 hello 後面坐 hello 叢集的公用閘道重新導向 hello 流量 toohello 接聽連接埠 HiveServer2 是實際。 hello 以下是範例連接字串：

    jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

取代`CLUSTERNAME`hello 名稱，為您的 HDInsight 叢集。

## <a name="authentication"></a>驗證

在建立 hello 連接時，您必須使用 hello HDInsight 叢集系統管理員名稱和密碼 tooauthenticate toohello 叢集閘道。 當從例如松鼠 SQL JDBC 用戶端連線，您必須輸入用戶端設定中的 hello 管理員名稱和密碼。

從 Java 應用程式，您必須使用 hello 名稱和密碼建立的連接時。 例如，hello 下列 Java 程式碼會開啟新的連接使用 hello 連接字串、 管理員名稱和密碼：

```java
DriverManager.getConnection(connectionString,clusterAdmin,clusterPassword);
```

## <a name="connect-with-squirrel-sql-client"></a>使用 SQuirreL SQL 用戶端連接

松鼠 SQL 是 JDBC 用戶端可以使用的 tooremotely 執行 Hive 查詢與您的 HDInsight 叢集。 hello 下列步驟假設您已安裝松鼠 SQL。

1. Hello Hive JDBC 驅動程式複製您的 HDInsight 叢集。

    * 如**以 Linux 為基礎的 HDInsight**，使用 hello 下列步驟 toodownload 所需的 hello jar 檔案。

        1. 建立包含 hello 檔案的目錄。 例如： `mkdir hivedriver`。

        2. 從命令列使用 hello 下列命令從 hello HDInsight 叢集 toocopy hello 檔案：

            ```bash
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/hive-jdbc*standalone.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-common.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-auth.jar .
            ```

            取代`USERNAME`hello 叢集 hello SSH 使用者帳戶名稱。 取代`CLUSTERNAME`與 hello HDInsight 叢集名稱。

    * 如**Windows 為基礎的 HDInsight**，使用 hello 下列步驟 toodownload hello jar 檔案。

        1. 從 hello Azure 入口網站，選取您的 HDInsight 叢集，然後選取 hello**遠端桌面**圖示。

            ![遠端桌面圖示](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopicon.png)

        2. Hello 遠端桌面 刀鋒視窗中，使用 hello**連接**按鈕 tooconnect toohello 叢集。 如果未啟用 hello 遠端桌面，使用 hello 表單 tooprovide 使用者名稱和密碼，然後選取 **啟用**hello 叢集 tooenable 遠端桌面。

            ![遠端桌面刀鋒視窗](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopblade.png)

            選取 [連線] 後，系統會下載 .rdp 檔案。 使用此檔案 toolaunch hello 遠端桌面用戶端。 出現提示時，使用您輸入的遠端桌面存取 hello 使用者名稱和密碼。

        3. 一旦連接之後，複製下列檔案從 hello 遠端桌面工作階段 tooyour 本機電腦的 hello。 把它們放在名為 `hivedriver` 的本機目錄中。

            * C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar
            * C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar
            * C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar

            > [!NOTE]
            > hello hello 路徑和檔案名稱中包含的數字可能會為您的叢集不同的版本。

        4. 中斷連線 hello 遠端桌面工作階段一旦完成複製 hello 檔案。

2. 啟動 hello 松鼠 SQL 應用程式。 從 hello hello 視窗左邊，選取**驅動程式**。

    ![驅動程式 索引標籤上 hello 視窗左邊的 hello](./media/hdinsight-connect-hive-jdbc-driver/squirreldrivers.png)

3. 從頂端的 hello hello hello 圖示**驅動程式**對話方塊中，選取 hello  **+** 圖示 toocreate 驅動程式。

    ![[驅動程式] 圖示](./media/hdinsight-connect-hive-jdbc-driver/driversicons.png)

4. 在 [hello] 新增驅動程式對話方塊新增 hello 下列資訊：

    * **名稱**：Hive
    * **範例 URL**：`jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`
    * **額外的類別路徑**： 之前使用 hello 新增按鈕 tooadd hello jar 檔案下載
    * **類別名稱**：org.apache.hive.jdbc.HiveDriver

   ![新增驅動程式對話方塊](./media/hdinsight-connect-hive-jdbc-driver/adddriver.png)

   按一下**確定**toosave 這些設定。

5. 在 hello hello 松鼠 SQL 視窗左邊，選取 **別名**。 然後按一下 hello  **+** 圖示 toocreate 連接別名。

    ![新增別名](./media/hdinsight-connect-hive-jdbc-driver/aliases.png)

6. 使用 hello 下列值 hello**新增別名**對話方塊。

    * **名稱**：HDInsight 上的 Hive

    * **驅動程式**： 使用 hello 下拉式 tooselect hello **Hive**驅動程式

    * **URL**： jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

        取代**CLUSTERNAME** hello 名稱，為您的 HDInsight 叢集。

    * **使用者名稱**: hello 您的 HDInsight 叢集的叢集登入帳戶名稱。 hello 預設值是`admin`。

    * **密碼**: hello hello 叢集登入帳戶的密碼。

 ![[新增別名] 對話方塊](./media/hdinsight-connect-hive-jdbc-driver/addalias.png)

    使用 hello**測試**hello 連線可運作的按鈕 tooverify。 當**連接到： Hive HDInsight 上**對話方塊出現，請選取**連接**tooperform hello 測試。 如果 hello 測試成功，您會看到**連線成功**對話方塊。

    toosave hello 連接別名，使用 hello**確定**在 hello hello 底部的按鈕**新增別名**對話方塊。

7. 從 hello**連接到**松鼠 SQL 的 hello 頂端的下拉式清單中選取**Hive HDInsight 上**。 出現提示時，請選取 [連接]。

    ![連接對話方塊](./media/hdinsight-connect-hive-jdbc-driver/connect.png)

8. 一旦連接之後，輸入下列查詢 hello SQL 查詢] 對話方塊，然後選取 [hello hello**執行**圖示。 hello 結果區域應該會顯示 hello hello 查詢結果。

        select * from hivesampletable limit 10;

    ![sql 查詢對話方塊，包括結果](./media/hdinsight-connect-hive-jdbc-driver/sqlquery.png)

## <a name="connect-from-an-example-java-application"></a>從範例 Java 應用程式連接

使用 Java 用戶端 tooquery Hive HDInsight 上的範例將會位於[https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc)。 依照 hello 儲存機制 toobuild 中的 hello 指示，並執行 hello 範例。

## <a name="troubleshooting"></a>疑難排解

### <a name="unexpected-error-occurred-attempting-tooopen-an-sql-connection"></a>發生意外的錯誤嘗試 tooopen SQL 連線

**徵兆**： 連接時 tooan HDInsight 叢集版本 3.3 或 3.4，您可能會收到未預期的錯誤發生的錯誤。 這項錯誤的 hello 堆疊追蹤為開頭 hello 下列行：

```java
java.util.concurrent.ExecutionException: java.lang.RuntimeException: java.lang.NoSuchMethodError: org.apache.commons.codec.binary.Base64.<init>(I)V
at java.util.concurrent.FutureTas...(FutureTask.java:122)
at java.util.concurrent.FutureTask.get(FutureTask.java:206)
```

**可能的原因**: hello hello commons codec.jar 檔案由松鼠和 hello hello hive 控制檔的 JDBC 元件所需的其中一個版本中不相符所造成這個錯誤。

**解析**: toofix 這個錯誤，請使用 hello 下列步驟：

1. 從您的 HDInsight 叢集下載 hello commons 轉碼器 jar 檔案。

        scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-codec*.jar ./commons-codec.jar

2. 結束松鼠，並前往 toohello 目錄松鼠系統上的安裝位置。 在 hello 松鼠目錄中，在 hello`lib`取代 hello 現有 commons-codec.jar 以其中一個從 hello HDInsight 叢集下載的 hello 的目錄。

3. 重新啟動 SQuirreL。 連接 tooHive HDInsight 上的時，應該不會再發生 hello 錯誤。

## <a name="next-steps"></a>後續步驟

既然您已經學會如何使用 Hive，使用下列的 hello toouse JDBC toowork 會連結 tooexplore Azure HDInsight 以其他方式 toowork。

* [上傳資料 tooHDInsight](hdinsight-upload-data.md)
* [搭配 HDInsight 使用 Hivet](hdinsight-use-hive.md)
* [搭配 HDInsight 使用 Pig](hdinsight-use-pig.md)
* [搭配 HDInsight 使用 MapReduce 工作](hdinsight-use-mapreduce.md)
