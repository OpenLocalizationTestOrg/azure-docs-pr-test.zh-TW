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
# <a name="use-a-java-udf-with-hive-in-hdinsight"></a>在 HDInsight 中搭配使用 Java UDF 和 Hive

了解如何 toocreate Java 為基礎使用者定義函數 (UDF) 可搭配 Hive。 在此範例中的 hello Java UDF 將轉換的文字字串 tooall 小寫字元。

## <a name="requirements"></a>需求

* HDInsight 叢集 

    > [!IMPORTANT]
    > Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

    本文件中的大部分步驟適用於以 Windows 和 Linux 為基礎的叢集。 不過，hello 步驟 tooupload hello 所編譯的 UDF toohello 叢集並執行它是特定 tooLinux 為基礎的叢集。 可以搭配 windows 叢集的 tooinformation 時，會提供連結。

* [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 或更新版本 (或同等功能版本，例如 OpenJDK)

* [Apache Maven](http://maven.apache.org/)

* 文字編輯器或 Java IDE

    > [!IMPORTANT]
    > 如果您建立 hello Python Windows 用戶端上的檔案，您必須使用 LF 做尾結束編輯器。 如果您不確定您的編輯器是使用 LF 或 CRLF，請參閱 hello[疑難排解](#troubleshooting)區段中針對步驟移除 hello CR 字元。

## <a name="create-an-example-java-udf"></a>建立範例 Java UDF 

1. 從命令列使用下列新的 Maven 專案 toocreate hello:

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=ExampleUDF -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

   > [!NOTE]
   > 如果您使用 PowerShell，您必須前後放置引號 hello 參數。 例如： `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`。

    此命令會建立一個名為目錄**exampleudf**，其中包含 hello Maven 專案。

2. 一旦建立 hello 專案之後，刪除 hello **exampleudf/src/test** hello 專案中建立的目錄。

3. 開啟 hello **exampleudf/pom.xml**，並取代現有的 hello `<dependencies>` hello 下列 XML 項目：

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

    這些項目指定 Hadoop 和 Hive HDInsight 3.5 所隨附的 hello 的版本。 您可以找到有關 hello 版本 Hadoop 和 Hive 與 HDInsight 提供從 hello [HDInsight 的元件版本控制](hdinsight-component-versioning.md)文件。

    新增`<build>`區段之前 hello `</project>` hello hello 檔結尾行。 這個區段應該包含下列 XML 的 hello:

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

    這些項目會定義如何 toobuild hello 專案。 具體來說，hello 專案使用的 Java hello 版本以及如何 toobuild uberjar 部署 toohello 叢集。

    一旦 hello 已變更，請儲存 hello 檔案。

4. 重新命名**exampleudf/src/main/java/com/microsoft/examples/App.java**太**ExampleUDF.java**，然後開啟您在編輯器中的 hello 檔案。

5. 取代 hello hello 內容**ExampleUDF.java** hello 下列檔案，然後儲存 hello 檔案。

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

    此程式碼會實作接受字串值，並傳回 hello 字串的小寫版本的 UDF。

## <a name="build-and-install-hello-udf"></a>建置和安裝 hello UDF

1. 使用下列命令 toocompile hello 和封裝 hello UDF:

    ```bash
    mvn compile package
    ```

    此命令會建置並封裝成 hello hello UDF`exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar`檔案。

2. 使用 hello`scp`命令 toocopy hello 檔案 toohello HDInsight 叢集。

    ```bash
    scp ./target/ExampleUDF-1.0-SNAPSHOT.jar myuser@mycluster-ssh.azurehdinsight
    ```

    取代`myuser`以 hello SSH 使用者帳戶，供您的叢集。 取代`mycluster`與 hello 叢集名稱。 如果您使用密碼 toosecure hello SSH 帳戶時，您必須提示的 tooenter hello 密碼。 如果您使用憑證，您可能需要 toouse hello`-i`參數 toospecify hello 私密金鑰檔案。

3. Toohello 叢集使用 SSH 連線。

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

    如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

4. 從 hello SSH 工作階段，將複製 hello jar 檔案 tooHDInsight 存放裝置。

    ```bash
    hdfs dfs -put ExampleUDF-1.0-SNAPSHOT.jar /example/jars
    ```

## <a name="use-hello-udf-from-hive"></a>使用 Hive hello UDF

1. 使用下列 toostart hello Beeline 用戶端 hello SSH 工作階段的 hello。

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    此命令假設您使用 hello 預設值是**admin** hello 登入帳戶，供您的叢集。

2. 一旦您到達 hello`jdbc:hive2://localhost:10001/>`提示，然後輸入 hello 遵循 tooadd hello UDF tooHive 並將它公開為函式。

    ```hiveql
    ADD JAR wasb:///example/jars/ExampleUDF-1.0-SNAPSHOT.jar;
    CREATE TEMPORARY FUNCTION tolower as 'com.microsoft.examples.ExampleUDF';
    ```

    > [!NOTE]
    > 這個範例假設 Azure 儲存體是 hello 叢集的預設儲存體。 如果您的叢集會改為使用資料湖存放區，變更 hello`wasb:///`值太`adl:///`。

3. 使用擷取自資料表 toolower 大小寫字串 hello UDF tooconvert 值。

    ```hiveql
    SELECT tolower(deviceplatform) FROM hivesampletable LIMIT 10;
    ```

    選取 hello 裝置平台 （Android、 Windows、 iOS、 等等） 從 hello 資料表中，此查詢轉換 hello 字串 toolower 情況下，，，然後將它們顯示。 會出現下列文字類似 toohello hello 輸出：

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

## <a name="next-steps"></a>後續步驟

Hive 以其他方式 toowork，請參閱[使用 Hive 與 HDInsight](hdinsight-use-hive.md)。

如需有關 Hive User-Defined 函式的詳細資訊，請參閱[hive 控制檔的運算子和使用者定義函數](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF)hello Hive wiki apache.org 在區段。
