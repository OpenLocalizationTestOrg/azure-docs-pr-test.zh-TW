---
title: "採用 Python 元件的 Apache Storm - Azure HDInsight | Microsoft Docs"
description: "了解如何建立使用 Python 元件的 Apache Storm 拓撲。"
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
ms.openlocfilehash: 305c4060ad81458b254e66a4bad6dfd7bf69b28d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="develop-apache-storm-topologies-using-python-on-hdinsight"></a><span data-ttu-id="4e4a3-104">在 HDInsight 上使用 Python 開發 Apache Storm 拓撲</span><span class="sxs-lookup"><span data-stu-id="4e4a3-104">Develop Apache Storm topologies using Python on HDInsight</span></span>

<span data-ttu-id="4e4a3-105">了解如何建立使用 Python 元件的 Apache Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-105">Learn how to create an Apache Storm topology that uses Python components.</span></span> <span data-ttu-id="4e4a3-106">Apache Storm 支援多種語言，甚至可讓您將數種語言的元件結合成一個拓撲。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-106">Apache Storm supports multiple languages, even allowing you to combine components from several languages in one topology.</span></span> <span data-ttu-id="4e4a3-107">Flux 架構 (隨 Storm 0.10.0 一起引進) 可讓您輕鬆建立使用 Python 元件的解決方案。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-107">The Flux framework (introduced with Storm 0.10.0) allows you to easily create solutions that use Python components.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4e4a3-108">本文件中的資訊已使用 Storm on HDInsight 3.6 進行測試。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-108">The information in this document was tested using Storm on HDInsight 3.6.</span></span> <span data-ttu-id="4e4a3-109">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4e4a3-110">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="4e4a3-111">此專案的程式碼可於 [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount)取得。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-111">The code for this project is available at [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e4a3-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="4e4a3-112">Prerequisites</span></span>

* <span data-ttu-id="4e4a3-113">Python 2.7 或更新版本</span><span class="sxs-lookup"><span data-stu-id="4e4a3-113">Python 2.7 or higher</span></span>

* <span data-ttu-id="4e4a3-114">Java JDK 1.8 或更新版本</span><span class="sxs-lookup"><span data-stu-id="4e4a3-114">Java JDK 1.8 or higher</span></span>

* <span data-ttu-id="4e4a3-115">Maven 3</span><span class="sxs-lookup"><span data-stu-id="4e4a3-115">Maven 3</span></span>

* <span data-ttu-id="4e4a3-116">(選擇性) 本機 Storm 開發環境。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-116">(Optional) A local Storm development environment.</span></span> <span data-ttu-id="4e4a3-117">只有當您想要在本機執行拓撲時，才需要本機 Storm 環境。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-117">A local Storm environment is only needed if you want to run the topology locally.</span></span> <span data-ttu-id="4e4a3-118">如需詳細資訊，請參閱[設定開發環境](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-118">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).</span></span>

## <a name="storm-multi-language-support"></a><span data-ttu-id="4e4a3-119">Storm 多語言支援</span><span class="sxs-lookup"><span data-stu-id="4e4a3-119">Storm multi-language support</span></span>

<span data-ttu-id="4e4a3-120">Apache Storm 專門用來搭配以任何程式設計語言撰寫的元件。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-120">Apache Storm was designed to work with components written using any programming language.</span></span> <span data-ttu-id="4e4a3-121">這些元件必須了解如何使用 [Storm 的 Thrift 定義](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift)。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-121">The components must understand how to work with the [Thrift definition for Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span></span> <span data-ttu-id="4e4a3-122">在 Python 中，Apache Storm 專案隨附一個模組，可讓您輕鬆地與 Strom 互動。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-122">For Python, a module is provided as part of the Apache Storm project that allows you to easily interface with Storm.</span></span> <span data-ttu-id="4e4a3-123">您可以在 [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py)找到此模組。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-123">You can find this module at [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span></span>

<span data-ttu-id="4e4a3-124">Storm 是在 Java 虛擬機器 (JVM) 上執行的 Java 程序。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-124">Storm is a Java process that runs on the Java Virtual Machine (JVM).</span></span> <span data-ttu-id="4e4a3-125">以其他語言撰寫的元件會以子流程執行。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-125">Components written in other languages are executed as subprocesses.</span></span> <span data-ttu-id="4e4a3-126">Storm 會使用透過 stdin/stdout 傳送的 JSON 訊息，與這些子流程進行通訊。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-126">The Storm communicates with these subprocesses using JSON messages sent over stdin/stdout.</span></span> <span data-ttu-id="4e4a3-127">如需各元件之間通訊的詳細資訊，請參閱 [多語言通訊協定](https://storm.apache.org/documentation/Multilang-protocol.html) 文件。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-127">More details on communication between components can be found in the [Multi-lang Protocol](https://storm.apache.org/documentation/Multilang-protocol.html) documentation.</span></span>

## <a name="python-with-the-flux-framework"></a><span data-ttu-id="4e4a3-128">採用 Flux 架構的 Python</span><span class="sxs-lookup"><span data-stu-id="4e4a3-128">Python with the Flux framework</span></span>

<span data-ttu-id="4e4a3-129">Flux 架構可讓您獨立於元件之外定義 Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-129">The Flux framework allows you to define Storm topologies separately from the components.</span></span> <span data-ttu-id="4e4a3-130">Flux 架構會使用 YAML 來定義 Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-130">The Flux framework uses YAML to define the Storm topology.</span></span> <span data-ttu-id="4e4a3-131">下列文字是如何在 YAML 文件中參考 Python 元件的範例：</span><span class="sxs-lookup"><span data-stu-id="4e4a3-131">The following text is an example of how to reference a Python component in the YAML document:</span></span>

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

<span data-ttu-id="4e4a3-132">類別 `FluxShellSpout` 用來啟動實作 Spout 的 `sentencespout.py` 指令碼。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-132">The class `FluxShellSpout` is used to start the `sentencespout.py` script that implements the spout.</span></span>

<span data-ttu-id="4e4a3-133">Flux 要求 Python 指令碼位於拓撲所在之 jar 檔案內的 `/resources` 目錄。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-133">Flux expects the Python scripts to be in the `/resources` directory inside the jar file that contains the topology.</span></span> <span data-ttu-id="4e4a3-134">因此，這個範例會將 Python 指令碼儲存在 `/multilang/resources` 目錄。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-134">So this example stores the Python scripts in the `/multilang/resources` directory.</span></span> <span data-ttu-id="4e4a3-135">`pom.xml` 使用下列 XML 來包含此檔案：</span><span class="sxs-lookup"><span data-stu-id="4e4a3-135">The `pom.xml` includes this file using the following XML:</span></span>

```xml
<!-- include the Python components -->
<resource>
    <directory>${basedir}/multilang</directory>
    <filtering>false</filtering>
</resource>
```

<span data-ttu-id="4e4a3-136">如先前所述，有一個 `storm.py` 檔案實作 Storm 的 Thrift 定義。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-136">As mentioned earlier, there is a `storm.py` file that implements the Thrift definition for Storm.</span></span> <span data-ttu-id="4e4a3-137">建置專案時，Flux 架構會自動包含 `storm.py`，因此您不必擔心要包含它。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-137">The Flux framework includes `storm.py` automatically when the project is built, so you don't have to worry about including it.</span></span>

## <a name="build-the-project"></a><span data-ttu-id="4e4a3-138">建置專案</span><span class="sxs-lookup"><span data-stu-id="4e4a3-138">Build the project</span></span>

<span data-ttu-id="4e4a3-139">從專案根目錄中，使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="4e4a3-139">From the root of the project, use the following command:</span></span>

```bash
mvn clean compile package
```

<span data-ttu-id="4e4a3-140">此命令會建立 `target/WordCount-1.0-SNAPSHOT.jar` 檔案，其中包含已編譯的拓撲。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-140">This command creates a `target/WordCount-1.0-SNAPSHOT.jar` file that contains the compiled topology.</span></span>

## <a name="run-the-topology-locally"></a><span data-ttu-id="4e4a3-141">在本機測試拓撲</span><span class="sxs-lookup"><span data-stu-id="4e4a3-141">Run the topology locally</span></span>

<span data-ttu-id="4e4a3-142">若要在本機執行拓撲，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="4e4a3-142">To run the topology locally, use the following command:</span></span>

```bash
storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -l -R /topology.yaml
```

> [!NOTE]
> <span data-ttu-id="4e4a3-143">此命令需要本機 Storm 開發環境。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-143">This command requires a local Storm development environment.</span></span> <span data-ttu-id="4e4a3-144">如需詳細資訊，請參閱[設定開發環境](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-144">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)</span></span>

<span data-ttu-id="4e4a3-145">拓撲啟動之後，就會將類似下列文字的資訊發出至本機主控台︰</span><span class="sxs-lookup"><span data-stu-id="4e4a3-145">Once the topology starts, it emits information to the local console similar to the following text:</span></span>


    24302 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting the cow jumped over the moon
    24302 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting the
    24302 [Thread-28] INFO  o.a.s.t.ShellBolt - ShellLog pid:2437, name:counter-bolt Emitting years:160
    24302 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=the, count=599}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=seven, count=302}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=dwarfs, count=143}
    24303 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting the cow jumped over the moon
    24303 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting cow
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=four, count=160}


<span data-ttu-id="4e4a3-146">若要停止拓撲，請使用 __Ctrl+C__。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-146">To stop the topology, use __Ctrl + C__.</span></span>

## <a name="run-the-storm-topology-on-hdinsight"></a><span data-ttu-id="4e4a3-147">在 HDInsight 上執行 Storm 拓撲</span><span class="sxs-lookup"><span data-stu-id="4e4a3-147">Run the Storm topology on HDInsight</span></span>

1. <span data-ttu-id="4e4a3-148">使用下列命令將 `WordCount-1.0-SNAPSHOT.jar`檔案複製到 Storm on HDInsight 叢集：</span><span class="sxs-lookup"><span data-stu-id="4e4a3-148">Use the following command to copy the `WordCount-1.0-SNAPSHOT.jar` file to your Storm on HDInsight cluster:</span></span>

    ```bash
    scp target\WordCount-1.0-SNAPSHOT.jar sshuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="4e4a3-149">將 `sshuser` 取代為叢集的 SSH 使用者。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-149">Replace `sshuser` with the SSH user for your cluster.</span></span> <span data-ttu-id="4e4a3-150">將 `mycluster` 取代為叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-150">Replace `mycluster` with the cluster name.</span></span> <span data-ttu-id="4e4a3-151">系統可能會提示您輸入 SSH 使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-151">You may be prompted to enter the password for the SSH user.</span></span>

    <span data-ttu-id="4e4a3-152">如需有關使用 SSH 和 SCP 的詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-152">For more information on using SSH and SCP, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="4e4a3-153">上傳檔案後，使用 SSH 連線至叢集：</span><span class="sxs-lookup"><span data-stu-id="4e4a3-153">Once the file has been uploaded, connect to the cluster using SSH:</span></span>

    ```bash
    ssh sshuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="4e4a3-154">從 SSH 工作階段中，使用下列命令啟動叢集上的拓撲：</span><span class="sxs-lookup"><span data-stu-id="4e4a3-154">From the SSH session, use the following command to start the topology on the cluster:</span></span>

    ```bash
    storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -r -R /topology.yaml
    ```

3. <span data-ttu-id="4e4a3-155">您可以使用 Storm UI 來檢視叢集上的拓撲。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-155">You can use the Storm UI to view the topology on the cluster.</span></span> <span data-ttu-id="4e4a3-156">Storm UI 位於 https://mycluster.azurehdinsight.net/stormui。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-156">The Storm UI is located at https://mycluster.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="4e4a3-157">將 `mycluster` 取代為您的叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-157">Replace `mycluster` with your cluster name.</span></span>

> [!NOTE]
> <span data-ttu-id="4e4a3-158">Storm 拓撲啟動之後會一直執行到停止為止。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-158">Once started, a Storm topology runs until stopped.</span></span> <span data-ttu-id="4e4a3-159">若要停止拓撲，請使用下列其中一種方法：</span><span class="sxs-lookup"><span data-stu-id="4e4a3-159">To stop the topology, use one of the following methods:</span></span>
>
> * <span data-ttu-id="4e4a3-160">從命令列執行 `storm kill TOPOLOGYNAME` 命令</span><span class="sxs-lookup"><span data-stu-id="4e4a3-160">The `storm kill TOPOLOGYNAME` command from the command line</span></span>
> * <span data-ttu-id="4e4a3-161">Storm UI 中的 [終止] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-161">The **Kill** button in the Storm UI.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4e4a3-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4e4a3-162">Next steps</span></span>

<span data-ttu-id="4e4a3-163">請參閱下列文件，了解搭配使用 Python 與 HDInsight 的其他方式。</span><span class="sxs-lookup"><span data-stu-id="4e4a3-163">See the following documents for other ways to use Python with HDInsight:</span></span>

* [<span data-ttu-id="4e4a3-164">如何使用 Python 串流處理 MapReduce 工作</span><span class="sxs-lookup"><span data-stu-id="4e4a3-164">How to use Python for streaming MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)
* [<span data-ttu-id="4e4a3-165">如何在 Pig 和 Hive 中使用 Python 使用者定義函數 (UDF)</span><span class="sxs-lookup"><span data-stu-id="4e4a3-165">How to use Python User Defined Functions (UDF) in Pig and Hive</span></span>](hdinsight-python.md)
