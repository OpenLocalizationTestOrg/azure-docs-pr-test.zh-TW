---
title: "使用 Python 相符-Azure HDInsight aaaApache Storm |Microsoft 文件"
description: "深入了解如何 toocreate 使用 Python 元件 Apache Storm 拓撲。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
keywords: apache storm python
ms.assetid: edd0ec4f-664d-4266-910c-6ecc94172ad8
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/04/2017
ms.author: larryfr
ms.openlocfilehash: 143c639623f1992f913900a7c52d6e3f03c701e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="develop-apache-storm-topologies-using-python-on-hdinsight"></a>在 HDInsight 上使用 Python 開發 Apache Storm 拓撲

深入了解如何 toocreate 使用 Python 元件 Apache Storm 拓撲。 Apache Storm 支援多種語言，甚至允許 toocombine 元件從一個拓撲中的數種語言。 hello 變動架構 （Storm 0.10.0 導入） 可讓您 tooeasily 建立使用 Python 元件的方案。

> [!IMPORTANT]
> 本文件中的 hello 資訊已使用 Storm HDInsight 3.6 上進行測試。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

hello 這個專案的程式碼將會位於[https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount)。

## <a name="prerequisites"></a>必要條件

* Python 2.7 或更新版本

* Java JDK 1.8 或更新版本

* Maven 3

* (選擇性) 本機 Storm 開發環境。 如果您想要在本機 toorun hello 拓樸，才需要在本機的 Storm 環境。 如需詳細資訊，請參閱[設定開發環境](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)。

## <a name="storm-multi-language-support"></a>Storm 多語言支援

Apache Storm 已設計的 toowork 與使用任何程式設計語言撰寫的元件。 hello 元件必須了解如何以 hello toowork [Storm 的 Thrift 定義](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift)。 Python 模組提供為 hello Apache Storm 專案可讓您使用 Storm tooeasily 介面的一部分。 您可以在 [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py)找到此模組。

Storm 是 hello Java Virtual Machine (JVM) 執行的 Java 處理序。 以其他語言撰寫的元件會以子流程執行。 hello Storm 會與使用 JSON 訊息透過 stdin/stdout 傳送這些子處理序通訊。 在元件之間通訊的更多詳細資料位於 hello[多重 lang 通訊協定](https://storm.apache.org/documentation/Multilang-protocol.html)文件。

## <a name="python-with-hello-flux-framework"></a>Python hello 變動架構

hello 變動架構可讓您 toodefine Storm 拓撲 hello 元件分開。 hello 變動架構會使用 YAML toodefine hello Storm 拓撲。 hello 下列文字是如何的範例 tooreference hello YAML 文件中的 Python 元件：

```yaml
# Spout definitions
spouts:
  - id: "sentence-spout"
    className: "org.apache.storm.flux.wrappers.spouts.FluxShellSpout"
    constructorArgs:
      # Command line
      - ["python", "sentencespout.py"]
      # Output field(s)
      - ["sentence"]
    # parallelism hint
    parallelism: 1
```

hello 類別`FluxShellSpout`為使用的 toostart hello`sentencespout.py`實作 hello spout 指令碼。

變動預期 hello hello Python 指令碼 toobe`/resources`目錄內包含之 hello 拓撲 hello jar 檔案。 因此這個範例會將 hello Python 指令碼存放至 hello`/multilang/resources`目錄。 hello`pom.xml`包括此檔案使用下列 XML 的 hello:

```xml
<!-- include hello Python components -->
<resource>
    <directory>${basedir}/multilang</directory>
    <filtering>false</filtering>
</resource>
```

如先前所述，沒有`storm.py`實作 Storm 的 hello Thrift 定義檔案。 hello 變動 framework 包含`storm.py`自動當 hello 建置專案，所以您不需要考慮納入該 tooworry。

## <a name="build-hello-project"></a>建置 hello 專案

從 hello hello 專案根目錄，使用下列命令的 hello:

```bash
mvn clean compile package
```

此命令會建立`target/WordCount-1.0-SNAPSHOT.jar`檔案，其中包含 hello 編譯拓撲。

## <a name="run-hello-topology-locally"></a>在本機執行 hello 拓樸

在本機，toorun hello 拓撲使用 hello 下列命令：

```bash
storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -l -R /topology.yaml
```

> [!NOTE]
> 此命令需要本機 Storm 開發環境。 如需詳細資訊，請參閱[設定開發環境](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)。

一次 hello 拓撲啟動時，它會發出資訊 toohello 本機主控台類似 toohello 下列文字：


    24302 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24302 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting the
    24302 [Thread-28] INFO  o.a.s.t.ShellBolt - ShellLog pid:2437, name:counter-bolt Emitting years:160
    24302 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=the, count=599}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=seven, count=302}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=dwarfs, count=143}
    24303 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24303 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting cow
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=four, count=160}


toostop hello 拓撲中，使用__Ctrl + C__。

## <a name="run-hello-storm-topology-on-hdinsight"></a>在 HDInsight 上執行 hello Storm 拓樸

1. 使用 hello 下列命令 toocopy hello `WordCount-1.0-SNAPSHOT.jar` tooyour Storm HDInsight 叢集上的檔案：

    ```bash
    scp target\WordCount-1.0-SNAPSHOT.jar sshuser@mycluster-ssh.azurehdinsight.net
    ```

    取代`sshuser`與 hello SSH 使用者，供您的叢集。 取代`mycluster`與 hello 叢集名稱。 您可能會提示的 tooenter hello hello SSH 使用者的密碼。

    如需有關使用 SSH 和 SCP 的詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

2. Hello 檔案已上傳，一旦使用 SSH toohello 叢集的連線：

    ```bash
    ssh sshuser@mycluster-ssh.azurehdinsight.net
    ```

3. 從 hello SSH 工作階段，使用下列命令 toostart hello 拓撲 hello 叢集上的 hello:

    ```bash
    storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -r -R /topology.yaml
    ```

3. 您可以使用 hello Storm UI tooview hello 拓撲 hello 叢集上。 hello Storm UI 位於 https://mycluster.azurehdinsight.net/stormui。 將 `mycluster` 取代為您的叢集名稱。

> [!NOTE]
> Storm 拓撲啟動之後會一直執行到停止為止。 toostop hello 拓撲，請使用其中一個 hello 下列方法：
>
> * hello `storm kill TOPOLOGYNAME` hello 命令列命令
> * hello **Kill** hello Storm UI 中的按鈕。


## <a name="next-steps"></a>後續步驟

請參閱下列文件的其他方式 toouse Python 與 HDInsight hello:

* [如何 toouse Python 串流 MapReduce 工作](hdinsight-hadoop-streaming-python.md)
* [如何 toouse Python 使用者定義函數 (UDF) 在 Pig 和 Hive](hdinsight-python.md)
