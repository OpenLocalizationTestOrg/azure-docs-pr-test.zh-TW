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
# <a name="develop-apache-storm-topologies-using-python-on-hdinsight"></a><span data-ttu-id="1d907-104">在 HDInsight 上使用 Python 開發 Apache Storm 拓撲</span><span class="sxs-lookup"><span data-stu-id="1d907-104">Develop Apache Storm topologies using Python on HDInsight</span></span>

<span data-ttu-id="1d907-105">深入了解如何 toocreate 使用 Python 元件 Apache Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="1d907-105">Learn how toocreate an Apache Storm topology that uses Python components.</span></span> <span data-ttu-id="1d907-106">Apache Storm 支援多種語言，甚至允許 toocombine 元件從一個拓撲中的數種語言。</span><span class="sxs-lookup"><span data-stu-id="1d907-106">Apache Storm supports multiple languages, even allowing you toocombine components from several languages in one topology.</span></span> <span data-ttu-id="1d907-107">hello 變動架構 （Storm 0.10.0 導入） 可讓您 tooeasily 建立使用 Python 元件的方案。</span><span class="sxs-lookup"><span data-stu-id="1d907-107">hello Flux framework (introduced with Storm 0.10.0) allows you tooeasily create solutions that use Python components.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1d907-108">本文件中的 hello 資訊已使用 Storm HDInsight 3.6 上進行測試。</span><span class="sxs-lookup"><span data-stu-id="1d907-108">hello information in this document was tested using Storm on HDInsight 3.6.</span></span> <span data-ttu-id="1d907-109">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="1d907-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1d907-110">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="1d907-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="1d907-111">hello 這個專案的程式碼將會位於[https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount)。</span><span class="sxs-lookup"><span data-stu-id="1d907-111">hello code for this project is available at [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d907-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="1d907-112">Prerequisites</span></span>

* <span data-ttu-id="1d907-113">Python 2.7 或更新版本</span><span class="sxs-lookup"><span data-stu-id="1d907-113">Python 2.7 or higher</span></span>

* <span data-ttu-id="1d907-114">Java JDK 1.8 或更新版本</span><span class="sxs-lookup"><span data-stu-id="1d907-114">Java JDK 1.8 or higher</span></span>

* <span data-ttu-id="1d907-115">Maven 3</span><span class="sxs-lookup"><span data-stu-id="1d907-115">Maven 3</span></span>

* <span data-ttu-id="1d907-116">(選擇性) 本機 Storm 開發環境。</span><span class="sxs-lookup"><span data-stu-id="1d907-116">(Optional) A local Storm development environment.</span></span> <span data-ttu-id="1d907-117">如果您想要在本機 toorun hello 拓樸，才需要在本機的 Storm 環境。</span><span class="sxs-lookup"><span data-stu-id="1d907-117">A local Storm environment is only needed if you want toorun hello topology locally.</span></span> <span data-ttu-id="1d907-118">如需詳細資訊，請參閱[設定開發環境](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)。</span><span class="sxs-lookup"><span data-stu-id="1d907-118">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).</span></span>

## <a name="storm-multi-language-support"></a><span data-ttu-id="1d907-119">Storm 多語言支援</span><span class="sxs-lookup"><span data-stu-id="1d907-119">Storm multi-language support</span></span>

<span data-ttu-id="1d907-120">Apache Storm 已設計的 toowork 與使用任何程式設計語言撰寫的元件。</span><span class="sxs-lookup"><span data-stu-id="1d907-120">Apache Storm was designed toowork with components written using any programming language.</span></span> <span data-ttu-id="1d907-121">hello 元件必須了解如何以 hello toowork [Storm 的 Thrift 定義](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift)。</span><span class="sxs-lookup"><span data-stu-id="1d907-121">hello components must understand how toowork with hello [Thrift definition for Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span></span> <span data-ttu-id="1d907-122">Python 模組提供為 hello Apache Storm 專案可讓您使用 Storm tooeasily 介面的一部分。</span><span class="sxs-lookup"><span data-stu-id="1d907-122">For Python, a module is provided as part of hello Apache Storm project that allows you tooeasily interface with Storm.</span></span> <span data-ttu-id="1d907-123">您可以在 [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py)找到此模組。</span><span class="sxs-lookup"><span data-stu-id="1d907-123">You can find this module at [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span></span>

<span data-ttu-id="1d907-124">Storm 是 hello Java Virtual Machine (JVM) 執行的 Java 處理序。</span><span class="sxs-lookup"><span data-stu-id="1d907-124">Storm is a Java process that runs on hello Java Virtual Machine (JVM).</span></span> <span data-ttu-id="1d907-125">以其他語言撰寫的元件會以子流程執行。</span><span class="sxs-lookup"><span data-stu-id="1d907-125">Components written in other languages are executed as subprocesses.</span></span> <span data-ttu-id="1d907-126">hello Storm 會與使用 JSON 訊息透過 stdin/stdout 傳送這些子處理序通訊。</span><span class="sxs-lookup"><span data-stu-id="1d907-126">hello Storm communicates with these subprocesses using JSON messages sent over stdin/stdout.</span></span> <span data-ttu-id="1d907-127">在元件之間通訊的更多詳細資料位於 hello[多重 lang 通訊協定](https://storm.apache.org/documentation/Multilang-protocol.html)文件。</span><span class="sxs-lookup"><span data-stu-id="1d907-127">More details on communication between components can be found in hello [Multi-lang Protocol](https://storm.apache.org/documentation/Multilang-protocol.html) documentation.</span></span>

## <a name="python-with-hello-flux-framework"></a><span data-ttu-id="1d907-128">Python hello 變動架構</span><span class="sxs-lookup"><span data-stu-id="1d907-128">Python with hello Flux framework</span></span>

<span data-ttu-id="1d907-129">hello 變動架構可讓您 toodefine Storm 拓撲 hello 元件分開。</span><span class="sxs-lookup"><span data-stu-id="1d907-129">hello Flux framework allows you toodefine Storm topologies separately from hello components.</span></span> <span data-ttu-id="1d907-130">hello 變動架構會使用 YAML toodefine hello Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="1d907-130">hello Flux framework uses YAML toodefine hello Storm topology.</span></span> <span data-ttu-id="1d907-131">hello 下列文字是如何的範例 tooreference hello YAML 文件中的 Python 元件：</span><span class="sxs-lookup"><span data-stu-id="1d907-131">hello following text is an example of how tooreference a Python component in hello YAML document:</span></span>

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

<span data-ttu-id="1d907-132">hello 類別`FluxShellSpout`為使用的 toostart hello`sentencespout.py`實作 hello spout 指令碼。</span><span class="sxs-lookup"><span data-stu-id="1d907-132">hello class `FluxShellSpout` is used toostart hello `sentencespout.py` script that implements hello spout.</span></span>

<span data-ttu-id="1d907-133">變動預期 hello hello Python 指令碼 toobe`/resources`目錄內包含之 hello 拓撲 hello jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="1d907-133">Flux expects hello Python scripts toobe in hello `/resources` directory inside hello jar file that contains hello topology.</span></span> <span data-ttu-id="1d907-134">因此這個範例會將 hello Python 指令碼存放至 hello`/multilang/resources`目錄。</span><span class="sxs-lookup"><span data-stu-id="1d907-134">So this example stores hello Python scripts in hello `/multilang/resources` directory.</span></span> <span data-ttu-id="1d907-135">hello`pom.xml`包括此檔案使用下列 XML 的 hello:</span><span class="sxs-lookup"><span data-stu-id="1d907-135">hello `pom.xml` includes this file using hello following XML:</span></span>

```xml
<!-- include hello Python components -->
<resource>
    <directory>${basedir}/multilang</directory>
    <filtering>false</filtering>
</resource>
```

<span data-ttu-id="1d907-136">如先前所述，沒有`storm.py`實作 Storm 的 hello Thrift 定義檔案。</span><span class="sxs-lookup"><span data-stu-id="1d907-136">As mentioned earlier, there is a `storm.py` file that implements hello Thrift definition for Storm.</span></span> <span data-ttu-id="1d907-137">hello 變動 framework 包含`storm.py`自動當 hello 建置專案，所以您不需要考慮納入該 tooworry。</span><span class="sxs-lookup"><span data-stu-id="1d907-137">hello Flux framework includes `storm.py` automatically when hello project is built, so you don't have tooworry about including it.</span></span>

## <a name="build-hello-project"></a><span data-ttu-id="1d907-138">建置 hello 專案</span><span class="sxs-lookup"><span data-stu-id="1d907-138">Build hello project</span></span>

<span data-ttu-id="1d907-139">從 hello hello 專案根目錄，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="1d907-139">From hello root of hello project, use hello following command:</span></span>

```bash
mvn clean compile package
```

<span data-ttu-id="1d907-140">此命令會建立`target/WordCount-1.0-SNAPSHOT.jar`檔案，其中包含 hello 編譯拓撲。</span><span class="sxs-lookup"><span data-stu-id="1d907-140">This command creates a `target/WordCount-1.0-SNAPSHOT.jar` file that contains hello compiled topology.</span></span>

## <a name="run-hello-topology-locally"></a><span data-ttu-id="1d907-141">在本機執行 hello 拓樸</span><span class="sxs-lookup"><span data-stu-id="1d907-141">Run hello topology locally</span></span>

<span data-ttu-id="1d907-142">在本機，toorun hello 拓撲使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="1d907-142">toorun hello topology locally, use hello following command:</span></span>

```bash
storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -l -R /topology.yaml
```

> [!NOTE]
> <span data-ttu-id="1d907-143">此命令需要本機 Storm 開發環境。</span><span class="sxs-lookup"><span data-stu-id="1d907-143">This command requires a local Storm development environment.</span></span> <span data-ttu-id="1d907-144">如需詳細資訊，請參閱[設定開發環境](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)。</span><span class="sxs-lookup"><span data-stu-id="1d907-144">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)</span></span>

<span data-ttu-id="1d907-145">一次 hello 拓撲啟動時，它會發出資訊 toohello 本機主控台類似 toohello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="1d907-145">Once hello topology starts, it emits information toohello local console similar toohello following text:</span></span>


    24302 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24302 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting the
    24302 [Thread-28] INFO  o.a.s.t.ShellBolt - ShellLog pid:2437, name:counter-bolt Emitting years:160
    24302 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=the, count=599}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=seven, count=302}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=dwarfs, count=143}
    24303 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24303 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting cow
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=four, count=160}


<span data-ttu-id="1d907-146">toostop hello 拓撲中，使用__Ctrl + C__。</span><span class="sxs-lookup"><span data-stu-id="1d907-146">toostop hello topology, use __Ctrl + C__.</span></span>

## <a name="run-hello-storm-topology-on-hdinsight"></a><span data-ttu-id="1d907-147">在 HDInsight 上執行 hello Storm 拓樸</span><span class="sxs-lookup"><span data-stu-id="1d907-147">Run hello Storm topology on HDInsight</span></span>

1. <span data-ttu-id="1d907-148">使用 hello 下列命令 toocopy hello `WordCount-1.0-SNAPSHOT.jar` tooyour Storm HDInsight 叢集上的檔案：</span><span class="sxs-lookup"><span data-stu-id="1d907-148">Use hello following command toocopy hello `WordCount-1.0-SNAPSHOT.jar` file tooyour Storm on HDInsight cluster:</span></span>

    ```bash
    scp target\WordCount-1.0-SNAPSHOT.jar sshuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="1d907-149">取代`sshuser`與 hello SSH 使用者，供您的叢集。</span><span class="sxs-lookup"><span data-stu-id="1d907-149">Replace `sshuser` with hello SSH user for your cluster.</span></span> <span data-ttu-id="1d907-150">取代`mycluster`與 hello 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="1d907-150">Replace `mycluster` with hello cluster name.</span></span> <span data-ttu-id="1d907-151">您可能會提示的 tooenter hello hello SSH 使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="1d907-151">You may be prompted tooenter hello password for hello SSH user.</span></span>

    <span data-ttu-id="1d907-152">如需有關使用 SSH 和 SCP 的詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="1d907-152">For more information on using SSH and SCP, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="1d907-153">Hello 檔案已上傳，一旦使用 SSH toohello 叢集的連線：</span><span class="sxs-lookup"><span data-stu-id="1d907-153">Once hello file has been uploaded, connect toohello cluster using SSH:</span></span>

    ```bash
    ssh sshuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="1d907-154">從 hello SSH 工作階段，使用下列命令 toostart hello 拓撲 hello 叢集上的 hello:</span><span class="sxs-lookup"><span data-stu-id="1d907-154">From hello SSH session, use hello following command toostart hello topology on hello cluster:</span></span>

    ```bash
    storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -r -R /topology.yaml
    ```

3. <span data-ttu-id="1d907-155">您可以使用 hello Storm UI tooview hello 拓撲 hello 叢集上。</span><span class="sxs-lookup"><span data-stu-id="1d907-155">You can use hello Storm UI tooview hello topology on hello cluster.</span></span> <span data-ttu-id="1d907-156">hello Storm UI 位於 https://mycluster.azurehdinsight.net/stormui。</span><span class="sxs-lookup"><span data-stu-id="1d907-156">hello Storm UI is located at https://mycluster.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="1d907-157">將 `mycluster` 取代為您的叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="1d907-157">Replace `mycluster` with your cluster name.</span></span>

> [!NOTE]
> <span data-ttu-id="1d907-158">Storm 拓撲啟動之後會一直執行到停止為止。</span><span class="sxs-lookup"><span data-stu-id="1d907-158">Once started, a Storm topology runs until stopped.</span></span> <span data-ttu-id="1d907-159">toostop hello 拓撲，請使用其中一個 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="1d907-159">toostop hello topology, use one of hello following methods:</span></span>
>
> * <span data-ttu-id="1d907-160">hello `storm kill TOPOLOGYNAME` hello 命令列命令</span><span class="sxs-lookup"><span data-stu-id="1d907-160">hello `storm kill TOPOLOGYNAME` command from hello command line</span></span>
> * <span data-ttu-id="1d907-161">hello **Kill** hello Storm UI 中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="1d907-161">hello **Kill** button in hello Storm UI.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1d907-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1d907-162">Next steps</span></span>

<span data-ttu-id="1d907-163">請參閱下列文件的其他方式 toouse Python 與 HDInsight hello:</span><span class="sxs-lookup"><span data-stu-id="1d907-163">See hello following documents for other ways toouse Python with HDInsight:</span></span>

* [<span data-ttu-id="1d907-164">如何 toouse Python 串流 MapReduce 工作</span><span class="sxs-lookup"><span data-stu-id="1d907-164">How toouse Python for streaming MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)
* [<span data-ttu-id="1d907-165">如何 toouse Python 使用者定義函數 (UDF) 在 Pig 和 Hive</span><span class="sxs-lookup"><span data-stu-id="1d907-165">How toouse Python User Defined Functions (UDF) in Pig and Hive</span></span>](hdinsight-python.md)
