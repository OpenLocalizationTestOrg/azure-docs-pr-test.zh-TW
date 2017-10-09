---
title: "aaaUse 上 Azure HDInsight Spark Caffe 分散式深層的了解 |Microsoft 文件"
description: "在 Azure HDInsight Spark 上使用 Caffe 進行分散式深入學習"
services: hdinsight
documentationcenter: 
author: xiaoyongzhu
manager: asadk
editor: cgronlun
tags: azure-portal
ms.assetid: 71dcd1ad-4cad-47ad-8a9d-dcb7fa3c2ff9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: xiaoyzhu
ms.openlocfilehash: d6476a7ed3a0df38538e845d7d5404067b01113c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-caffe-on-azure-hdinsight-spark-for-distributed-deep-learning"></a>在 Azure HDInsight Spark 上使用 Caffe 進行分散式深入學習


## <a name="introduction"></a>簡介

醫療保健 tootransportation toomanufacturing 從所有項目以及其他影響到深入學習。 公司將 toodeep 學習 toosolve 艱難問題，例如在開啟[影像分類](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/)，[語音辨識](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html)、 物件辨識和機器轉譯。 

有[許多受歡迎的架構](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software)，包括 [Microsoft 認知工具組](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/)、[Tensorflow](https://www.tensorflow.org/)MXNet、Theano 等等。Caffe 是其中一個 hello 最知名的非符號 （命令式） 類神經網路架構，而且也廣泛使用在許多方面，包括電腦視覺。 此外，[CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) 結合 Caffe 與 Apache Spark，在此情況下，深入學習可輕鬆地用於現有的 Hadoop 叢集結合 Spark ETL 管線，以減少系統複雜度和端對端學習的延遲。

[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/)只有完全受管理的雲端 Hadoop 供應項目可提供開放原始碼分析叢集針對 Spark、 Hive、 MapReduce、 HBase、 Storm、 Kafka 和最佳化 99.9 %sla 所支援的 R 伺服器為 hello。 每個巨量資料技術及 ISV 應用程式都可輕鬆部署為受管理的叢集，以提供企業級安全性和監視功能。

有些使用者會詢問我們如何 toouse 深入了解 HDInsight 是 Microsoft 的 PaaS Hadoop 產品上。 我們將會在多個 tooshare 在 hello 未來，但我們需要 toosummarize 如何技術部落格的今天 toouse Caffe HDInsight Spark 上。

如果您之前已安裝過 Caffe，您會發現安裝此架構有點困難。 在這篇部落格，我們會先說明如何 tooinstall[上的 Spark Caffe](https://github.com/yahoo/CaffeOnSpark) HDInsight 叢集，然後使用內建 MNIST 示範 toodemostrate hello 如何 toouse 分散式深入學習使用 Cpu 上的 HDInsight Spark。

有四個主要步驟 tooget 它在 HDInsight 使用。

1. Hello 的所有節點上安裝所需的 hello 相依項目
2. Spark HDInsight Caffe 根據 hello 前端節點上
3. 發佈 hello 所需的程式庫 tooall hello 背景工作節點
4. 撰寫 Caffe 模型，並以分散方式執行它

HDInsight 是 PaaS 解決方案，因為它提供絕佳的平台功能-因此相當簡單 tooperform 某些工作。 我們會大量使用此部落格文章中的 hello 功能在呼叫其中一個[指令碼動作](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)，與您可以執行殼層命令 toocustomize 叢集節點 （前端節點、 背景工作節點或邊緣節點）。

## <a name="step-1--install-hello-required-dependencies-on-all-hello-nodes"></a>步驟 1: Hello 的所有節點上安裝所需的 hello 相依項目

啟動 tooget，我們需要我們需要 tooinstall hello 相依性。 hello Caffe 站台和[CaffeOnSpark 網站](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn)提供一些很有幫助 wiki 安裝 hello 相依性的 Spark，YARN 模式 （這是 HDInsight Spark hello 模式），但我們需要 tooadd 少數的多個相依性的 HDInsight 平台。 我們將使用 hello 指令碼動作，如下所示，所有 hello 前端節點和背景工作節點上執行它。 此指令碼動作將需要大約 20 分鐘，因為這些相依性也取決於其他封裝。 您應該將它放在某些位置，存取 tooyour HDInsight 叢集，例如 GitHub 位置或 hello 預設 BLOB 儲存體帳戶。

    #!/bin/bash
    #Please be aware that installing hello below will add additional 20 mins toocluster creation because of hello dependencies
    #installing all dependencies, including hello ones mentioned in http://caffe.berkeleyvision.org/install_apt.html, as well a few packages that are not included in HDInsight, such as gflags, glog, lmdb, numpy
    #It seems numpy will only needed during compilation time, but for safety purpose we install them on all hello nodes

    sudo apt-get install -y libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler maven libatlas-base-dev libgflags-dev libgoogle-glog-dev liblmdb-dev build-essential  libboost-all-dev python-numpy python-scipy python-matplotlib ipython ipython-notebook python-pandas python-sympy python-nose

    #install protobuf
    wget https://github.com/google/protobuf/releases/download/v2.5.0/protobuf-2.5.0.tar.gz
    sudo tar xzvf protobuf-2.5.0.tar.gz -C /tmp/
    cd /tmp/protobuf-2.5.0/
    sudo ./configure
    sudo make
    sudo make check
    sudo make install
    sudo ldconfig
    echo "protobuf installation done"


上述的 hello 指令碼動作有兩個步驟。 hello 第一個步驟是 tooinstall 所有 hello 必要程式庫。 這些程式庫包含編譯 Caffe （例如 gflags glog) 和執行 （例如 numpy) Caffe hello 必要的程式庫。 我們使用 libatlas CPU 最佳化，但您永遠可以依照 hello CaffeOnSpark wiki 需安裝其他最佳化程式庫，例如 MKL 或 CUDA （適用於 GPU)。

hello 第二步是 toodownload、 編譯和執行階段期間安裝 protobuf 2.5.0 Caffe 的。 Protobuf 2.5.0[無須](https://github.com/yahoo/CaffeOnSpark/issues/87)，但是這個版本並非為 Ubuntu 16 上的封裝可使用，因此我們需要 toocompile 從 hello 原始程式碼。 另外還有幾個資源上如何 hello 網際網路 toocompile，例如[這](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)

toosimply 開始，您可以只執行此指令碼動作對叢集 tooall hello 背景工作節點和前端節點 （適用於 HDInsight 3.5)。 您可以執行 hello 指令碼動作執行的叢集，或者您也可以執行 hello 指令碼動作在 hello 叢集佈建時間。 如需有關 hello 指令碼動作的詳細資訊，請參閱 hello 文件[這裡](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)

![指令碼動作 tooInstall 相依性](./media/hdinsight-deep-learning-caffe-spark/Script-Action-1.png)


## <a name="step-2-build-caffe-on-spark-for-hdinsight-on-hello-head-node"></a>步驟 2： 根據 Caffe Spark HDInsight hello 前端節點上

hello 第二個步驟是 toobuild Caffe hello 叢集前端節點，在然後將發佈 hello 編譯的程式庫 tooall hello 背景工作節點。 在此步驟中，您將需要太[ssh 到您的叢集前端節點](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix)，只要遵循 hello [CaffeOnSpark 建置程序](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn)下面是 hello 指令碼，您可以使用 toobuild CaffeOnSpark 搭配一些額外的步驟。 

    #!/bin/bash
    git clone https://github.com/yahoo/CaffeOnSpark.git --recursive
    export CAFFE_ON_SPARK=$(pwd)/CaffeOnSpark

    pushd ${CAFFE_ON_SPARK}/caffe-public/
    cp Makefile.config.example Makefile.config
    echo "INCLUDE_DIRS += ${JAVA_HOME}/include" >> Makefile.config
    #Below configurations might need toobe updated based on actual cases. For example, if you are using GPU, or using a different BLAS library, you may want tooupdate those settings accordingly.
    echo "CPU_ONLY := 1" >> Makefile.config
    echo "BLAS := atlas" >> Makefile.config
    echo "INCLUDE_DIRS += /usr/include/hdf5/serial/" >> Makefile.config
    echo "LIBRARY_DIRS += /usr/lib/x86_64-linux-gnu/hdf5/serial/" >> Makefile.config
    popd

    #compile CaffeOnSpark
    pushd ${CAFFE_ON_SPARK}
    #always clean up hello environment before building (especially when rebuiding), or there will be errors such as "failed tooexecute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2"
    make clean 
    #hello build step usually takes 20~30 mins, since it has a lot maven dependencies
    make build 
    popd
    export LD_LIBRARY_PATH=${CAFFE_ON_SPARK}/caffe-public/distribute/lib:${CAFFE_ON_SPARK}/caffe-distri/distribute/lib

    hadoop fs -mkdir -p wasb:///projects/machine_learning/image_dataset

    ${CAFFE_ON_SPARK}/scripts/setup-mnist.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/mnist_*_lmdb wasb:///projects/machine_learning/image_dataset/

    ${CAFFE_ON_SPARK}/scripts/setup-cifar10.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/cifar10_*_lmdb wasb:///projects/machine_learning/image_dataset/

    #put hello already compiled CaffeOnSpark libraries toowasb storage, then read back tooeach node using script actions. This is because CaffeOnSpark requires all hello nodes have hello libarries
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-public/distribute/lib/
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-distri/distribute/lib/* /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-public/distribute/lib/* /CaffeOnSpark/caffe-public/distribute/lib/

您可能需要 toodo 超過 CaffeOnSpark 哪些 hello 文件，該處會指示。 hello 變更如下：
- 變更只 tooCPU 並針對此特定用途使用 libatlas。
- Put 的 hello 資料集 toohello BLOB 儲存體，這是可存取 tooall 背景工作節點，以供稍後使用的共用的位置。
- Put 的 hello 編譯 Caffe 文件庫 tooBLOB 儲存體，稍後您將會複製使用指令碼動作 tooavoid 其他的編譯時間這些程式庫 tooall hello 節點。


### <a name="troubleshooting-an-ant-buildexception-has-occured-exec-returned-2"></a>疑難排解︰發生 Ant BuildException︰exec 傳回︰2

當第一次嘗試 toobuild CaffeOnSpark，有時它會顯示

    failed tooexecute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2

由 「 請清除 「 只是全新的 hello 程式碼儲存機制，然後執行 「 請建置 「 即可解決此問題，只要您持有 hello 正確的依存性。

### <a name="troubleshooting-maven-repository-connection-time-out"></a>疑難排解︰Maven 儲存機制連線逾時

有時 maven 讓我 hello 連接逾時錯誤，類似 toobelow:

    Retry:
    [INFO] Downloading: https://repo.maven.apache.org/maven2/com/twitter/chill_2.11/0.8.0/chill_2.11-0.8.0.jar
    Feb 01, 2017 5:14:49 AM org.apache.maven.wagon.providers.http.httpclient.impl.execchain.RetryExec execute
    INFO: I/O exception (java.net.SocketException) caught when processing request too{s}->https://repo.maven.apache.org:443: Connection timed out (Read failed)

它將會是 OK 之後等候幾分鐘的時間，並再試 toorebuild hello 程式碼，因此它可能 Maven 由於某種原因而限制 hello 從給定的 IP 位址的流量。


### <a name="troubleshooting-test-failure-for-caffe"></a>疑難排解︰Caffe 測試失敗

您可能會看到測試失敗時的 CaffeOnSpark，與下面類似的 hello 最終檢查。 這是 prabably 相關以 utf-8 編碼方式，但應該不會影響 Caffe hello 使用量

    Run completed in 32 seconds, 78 milliseconds.
    Total number of tests run: 7
    Suites: completed 5, aborted 0
    Tests: succeeded 6, failed 1, canceled 0, ignored 0, pending 0
    *** 1 TEST FAILED ***

## <a name="step-3-distribute-hello-required-libraries-tooall-hello-worker-nodes"></a>步驟 3： 散佈 hello 所需的程式庫 tooall hello 背景工作節點

hello 下一個步驟是 toodistribute hello 程式庫 (基本上 hello 文件庫中 CaffeOnSpark/caffe 公用/發佈/lib/和 CaffeOnSpark/caffe-distri/發佈/lib /) tooall hello 節點。 在步驟 2 中，將這些程式庫在 BLOB 儲存體，並在此步驟中，我們將使用指令碼動作 toocopy 它 tooall hello 前端節點和背景工作節點。

toodo 執行指令碼動作，如下所示，簡單 （您需要 toopoint toohello 正確的位置特定 tooyour 叢集）：

    #!/bin/bash
    hadoop fs -get wasb:///CaffeOnSpark /home/changetoyourusername/

在步驟 2 中，我們將它放在 hello BLOB 儲存體，這是可存取 tooall hello 節點，因為在此步驟中我們只將它複製 tooall hello 節點。

## <a name="step-4-compose-a-caffe-model-and-run-it-distributely"></a>步驟 4︰撰寫 Caffe 模型，並以分散方式執行它

執行上述步驟 hello 之後, Caffe hello 叢集前端節點上安裝完成後，我們很好的 toogo。 hello 下一個步驟是 toowrite Caffe 模型。 

Caffe 正在使用"易懂 architecture"，在撰寫模型，您只需要 toodefine 組態檔，而不完全 （在大部分情況下） 撰寫程式碼。 現在讓我們來看看那裡。 

hello 今天，我們將定型的模型是 MNIST 訓練範例模型。 手寫的數字的 hello MNIST 資料庫有個 60,000 範例中，定型集和測試集的 10,000 的範例。 它是一組可從 NIST 提供之較大集的子集。 hello 數字已大小正規化和固定大小的映像中置中。 CaffeOnSpark 有某些指令碼 toodownload hello 資料集，並將它轉換成 hello 正確的格式。

CaffeOnSpark 針對 MNIST 訓練提供一些網路拓樸範例。 它有 nice 設計的分割 hello 網路架構 （hello 網路中的 hello 拓撲） 和最佳化。 在此情況下，需要兩個檔案︰ 

hello"規劃求解 」 檔案 （${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt） 用於愈加 hello 最佳化，並產生參數更新。 比方說，它會定義是否 CPU 或 GPU 將用於，什麼是 hello 動量會多少反覆項目，等等。它也會定義哪些神經網路拓樸應該 hello （這是我們需要 hello 第二個檔案） 的程式使用。 如需有關規劃求解的詳細資訊，請參閱太[Caffe 文件](http://caffe.berkeleyvision.org/tutorial/solver.html)。

例如，因為我們使用 CPU，而不是 GPU，我們應該變更 hello 最後一行以：

    # solver mode: CPU or GPU
    solver_mode: CPU

![Caffe 組態](./media/hdinsight-deep-learning-caffe-spark/Caffe-1.png)

您可以視需要變更其他行。

hello 第二個檔案 （${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt） 會定義如何 hello 神經網路看起來，hello 相關輸入和輸出檔。 我們也需要 tooupdate hello 檔案 tooreflect hello 定型資料的位置。 變更下列的 lenet_memory_train_test.prototxt （您需要 toopoint toohello 正確的位置特定 tooyour 叢集） 中組件的 hello:

- 也變更 hello"file:/Users/mridul/bigml/demodl/mnist_train_lmdb""wasb: / 專案/machine_learning/image_dataset/mnist_train_lmdb"
- 變更 「 file:/Users/mridul/bigml/demodl/mnist_test_lmdb/ 」 太"wasb: / 專案/machine_learning/image_dataset/mnist_test_lmdb"

![Caffe 組態](./media/hdinsight-deep-learning-caffe-spark/Caffe-2.png)

如需有關如何 toodefine hello 網路的詳細資訊，請檢查 hello [Caffe MNIST 資料集上的文件](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)

為了 hello 這篇部落格，我們只會使用這個簡單的 MNIST 範例。 您應該從 hello 前端節點執行下面的 hello 命令：

    spark-submit --master yarn --deploy-mode cluster --num-executors 8 --files ${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt,${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt --conf spark.driver.extraLibraryPath="${LD_LIBRARY_PATH}" --conf spark.executorEnv.LD_LIBRARY_PATH="${LD_LIBRARY_PATH}" --class com.yahoo.ml.caffe.CaffeOnSpark ${CAFFE_ON_SPARK}/caffe-grid/target/caffe-grid-0.1-SNAPSHOT-jar-with-dependencies.jar -train -features accuracy,loss -label label -conf lenet_memory_solver.prototxt -devices 1 -connection ethernet -model wasb:///mnist.model -output wasb:///mnist_features_result

基本上它能將散發所需的 hello 檔案 （lenet_memory_solver.prototxt 和 lenet_memory_train_test.prototxt） tooeach YARN 容器，而且也設 hello 相關的每個 Spark 執行程式的驅動程式/tooLD_LIBRARY_PATH，hello 中定義的路徑前一個程式碼片段和點 toohello 位置具有 CaffeOnSpark 文件庫。 

## <a name="monitoring-and-troubleshooting"></a>監視與疑難排解

因為我們使用 YARN 叢集模式，在此情況下 hello Spark 驅動程式將會排定的 tooan 任意容器 （和任意的背景工作節點） 只能中應該會出現類似 hello 主控台輸出：

    17/02/01 23:22:16 INFO Client: Application report for application_1485916338528_0015 (state: RUNNING)

如果您想 tooknow 發生了什麼事，您通常需要 tooget hello Spark 驅動程式的記錄檔，其中有詳細資訊。 在此情況下，您需要 toogo toohello YARN UI toofind hello 相關 YARN 記錄。 您可以取得此 url 的 YARN UI hello: 

    https://yourclustername.azurehdinsight.net/yarnui
   
![YARN UI](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-1.png)

您可以看看此特定應用程式配置了多少資源。 您可以按一下 hello 」 排程器 」 連結，然後您會看到這個應用程式中，有 9 執行的容器。 我們要求 YARN tooprovide 8 執行程式，而另一個容器是驅動程式處理序。 

![YARN 排程器](./media/hdinsight-deep-learning-caffe-spark/YARN-Scheduler.png)

如果發生失敗，您可能想 toocheck hello 驅動程式記錄檔或容器的記錄檔。 驅動程式記錄檔，您可以按一下 hello YARN UI 中的應用程式識別碼，然後按一下 hello 」 記錄檔 」 按鈕。 hello 驅動程式記錄檔會寫入至 stderr。

![YARN UI 2](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-2.png)

例如，您會看到一些 hello 驅動程式記錄檔，從下方的 hello 錯誤指出配置太多的執行程式。

    17/02/01 07:26:06 ERROR ApplicationMaster: User class threw exception: java.lang.IllegalStateException: Insufficient training data. Please adjust hyperparameters or increase dataset.
    java.lang.IllegalStateException: Insufficient training data. Please adjust hyperparameters or increase dataset.
        at com.yahoo.ml.caffe.CaffeOnSpark.trainWithValidation(CaffeOnSpark.scala:261)
        at com.yahoo.ml.caffe.CaffeOnSpark$.main(CaffeOnSpark.scala:42)
        at com.yahoo.ml.caffe.CaffeOnSpark.main(CaffeOnSpark.scala)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:498)
        at org.apache.spark.deploy.yarn.ApplicationMaster$$anon$2.run(ApplicationMaster.scala:627)

某些情況下，執行程式，而不是驅動程式中的 hello 問題可能會發生。 在此情況下，您需要 toocheck hello 容器的記錄檔。 您可以一律取得 hello 容器記錄檔，然後 hello 失敗的容器。 例如，您在執行 Caffe 時可能會遇到此失敗。

    17/02/01 07:12:05 WARN YarnAllocator: Container marked as failed: container_1485916338528_0008_05_000005 on host: 10.0.0.14. Exit status: 134. Diagnostics: Exception from container-launch.
    Container id: container_1485916338528_0008_05_000005
    Exit code: 134
    Exception message: /bin/bash: line 1: 12230 Aborted                 (core dumped) LD_LIBRARY_PATH=/usr/hdp/current/hadoop-client/lib/native:/usr/hdp/current/hadoop-client/lib/native/Linux-amd64-64:/home/xiaoyzhu/CaffeOnSpark/caffe-public/distribute/lib:/home/xiaoyzhu/CaffeOnSpark/caffe-distri/distribute/lib /usr/lib/jvm/java-8-openjdk-amd64/bin/java -server -Xmx4608m '-Dhdp.version=' '-Detwlogger.component=sparkexecutor' '-DlogFilter.filename=SparkLogFilters.xml' '-DpatternGroup.filename=SparkPatternGroups.xml' '-Dlog4jspark.root.logger=INFO,console,RFA,ETW,Anonymizer' '-Dlog4jspark.log.dir=/var/log/sparkapp/${user.name}' '-Dlog4jspark.log.file=sparkexecutor.log' '-Dlog4j.configuration=file:/usr/hdp/current/spark2-client/conf/log4j.properties' '-Djavax.xml.parsers.SAXParserFactory=com.sun.org.apache.xerces.internal.jaxp.SAXParserFactoryImpl' -Djava.io.tmpdir=/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/tmp '-Dspark.driver.port=43942' '-Dspark.history.ui.port=18080' '-Dspark.ui.port=0' -Dspark.yarn.app.container.log.dir=/mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005 -XX:OnOutOfMemoryError='kill %p' org.apache.spark.executor.CoarseGrainedExecutorBackend --driver-url spark://CoarseGrainedScheduler@10.0.0.13:43942 --executor-id 4 --hostname 10.0.0.14 --cores 3 --app-id application_1485916338528_0008 --user-class-path file:/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/__app__.jar > /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stdout 2> /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stderr

    Stack trace: ExitCodeException exitCode=134: /bin/bash: line 1: 12230 Aborted                 (core dumped) LD_LIBRARY_PATH=/usr/hdp/current/hadoop-client/lib/native:/usr/hdp/current/hadoop-client/lib/native/Linux-amd64-64:/home/xiaoyzhu/CaffeOnSpark/caffe-public/distribute/lib:/home/xiaoyzhu/CaffeOnSpark/caffe-distri/distribute/lib /usr/lib/jvm/java-8-openjdk-amd64/bin/java -server -Xmx4608m '-Dhdp.version=' '-Detwlogger.component=sparkexecutor' '-DlogFilter.filename=SparkLogFilters.xml' '-DpatternGroup.filename=SparkPatternGroups.xml' '-Dlog4jspark.root.logger=INFO,console,RFA,ETW,Anonymizer' '-Dlog4jspark.log.dir=/var/log/sparkapp/${user.name}' '-Dlog4jspark.log.file=sparkexecutor.log' '-Dlog4j.configuration=file:/usr/hdp/current/spark2-client/conf/log4j.properties' '-Djavax.xml.parsers.SAXParserFactory=com.sun.org.apache.xerces.internal.jaxp.SAXParserFactoryImpl' -Djava.io.tmpdir=/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/tmp '-Dspark.driver.port=43942' '-Dspark.history.ui.port=18080' '-Dspark.ui.port=0' -Dspark.yarn.app.container.log.dir=/mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005 -XX:OnOutOfMemoryError='kill %p' org.apache.spark.executor.CoarseGrainedExecutorBackend --driver-url spark://CoarseGrainedScheduler@10.0.0.13:43942 --executor-id 4 --hostname 10.0.0.14 --cores 3 --app-id application_1485916338528_0008 --user-class-path file:/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/__app__.jar > /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stdout 2> /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stderr

        at org.apache.hadoop.util.Shell.runCommand(Shell.java:933)
        at org.apache.hadoop.util.Shell.run(Shell.java:844)
        at org.apache.hadoop.util.Shell$ShellCommandExecutor.execute(Shell.java:1123)
        at org.apache.hadoop.yarn.server.nodemanager.DefaultContainerExecutor.launchContainer(DefaultContainerExecutor.java:225)
        at org.apache.hadoop.yarn.server.nodemanager.containermanager.launcher.ContainerLaunch.call(ContainerLaunch.java:317)
        at org.apache.hadoop.yarn.server.nodemanager.containermanager.launcher.ContainerLaunch.call(ContainerLaunch.java:83)
        at java.util.concurrent.FutureTask.run(FutureTask.java:266)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617)
        at java.lang.Thread.run(Thread.java:745)


    Container exited with a non-zero exit code 134

在此情況下，您需要 tooget hello 失敗容器識別碼 （在上述案例 hello，它是 container_1485916338528_0008_05_000005）。 您需要 toorun 

    yarn logs -containerId container_1485916338528_0008_03_000005

從 hello 叢集前端節點。 在檢查容器失敗之後，它是由使用 lenet_memory_solver.prototxt 中的 GPU 模式 (您應該改用 CPU 模式) 所引起。

    17/02/01 07:10:48 INFO LMDB: Batch size:100
    WARNING: Logging before InitGoogleLogging() is written tooSTDERR
    F0201 07:10:48.309725 11624 common.cpp:79] Cannot use GPU in CPU-only Caffe: check mode.


## <a name="getting-results"></a>取得結果

因為我們會配置 8 執行程式，而且 hello 網路拓撲很簡單，它應該只採用大約 30 分鐘 toorun hello 結果。 從 hello 命令列中，您可以看到我們放 hello 模型 toowasb:///mnist.model，並將名為 wasb hello 結果 tooa 資料夾: / / mnist_features_result。

您可以透過執行取得 hello 結果

    hadoop fs -cat hdfs:///mnist_features_result/*

和 hello 結果如下所示：

    {"SampleID":"00009597","accuracy":[1.0],"loss":[0.028171852],"label":[2.0]}
    {"SampleID":"00009598","accuracy":[1.0],"loss":[0.028171852],"label":[6.0]}
    {"SampleID":"00009599","accuracy":[1.0],"loss":[0.028171852],"label":[1.0]}
    {"SampleID":"00009600","accuracy":[0.97],"loss":[0.0677709],"label":[5.0]}
    {"SampleID":"00009601","accuracy":[0.97],"loss":[0.0677709],"label":[0.0]}
    {"SampleID":"00009602","accuracy":[0.97],"loss":[0.0677709],"label":[1.0]}
    {"SampleID":"00009603","accuracy":[0.97],"loss":[0.0677709],"label":[2.0]}
    {"SampleID":"00009604","accuracy":[0.97],"loss":[0.0677709],"label":[3.0]}
    {"SampleID":"00009605","accuracy":[0.97],"loss":[0.0677709],"label":[4.0]}

hello SampleID 代表 hello 識別碼 hello MNIST 資料集中，且 hello 標籤 hello hello 模型的數字識別。


## <a name="conclusion"></a>結論

這份文件，在您嘗試 tooinstall CaffeOnSpark 執行簡單的範例。 HDInsight 是完整受管理的雲端分散式的運算平台，而 hello 大型的資料集上執行機器學習和進階的分析工作負載的最佳位置和分散式深層的了解，您可以使用 Caffe HDInsight Spark tooperform 深入學習工作。


## <a name="seealso"></a>另請參閱
* [概觀：Azure HDInsight 上的 Apache Spark](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>案例
* [Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [機器學習的 Spark： 使用 HDInsight toopredict 食物檢查結果中的 Spark](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

### <a name="manage-resources"></a>管理資源
* [管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源](hdinsight-apache-spark-resource-manager.md)

