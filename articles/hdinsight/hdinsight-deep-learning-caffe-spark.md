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
# <a name="use-caffe-on-azure-hdinsight-spark-for-distributed-deep-learning"></a><span data-ttu-id="2c707-103">在 Azure HDInsight Spark 上使用 Caffe 進行分散式深入學習</span><span class="sxs-lookup"><span data-stu-id="2c707-103">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>


## <a name="introduction"></a><span data-ttu-id="2c707-104">簡介</span><span class="sxs-lookup"><span data-stu-id="2c707-104">Introduction</span></span>

<span data-ttu-id="2c707-105">醫療保健 tootransportation toomanufacturing 從所有項目以及其他影響到深入學習。</span><span class="sxs-lookup"><span data-stu-id="2c707-105">Deep learning is impacting everything from healthcare tootransportation toomanufacturing, and more.</span></span> <span data-ttu-id="2c707-106">公司將 toodeep 學習 toosolve 艱難問題，例如在開啟[影像分類](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/)，[語音辨識](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html)、 物件辨識和機器轉譯。</span><span class="sxs-lookup"><span data-stu-id="2c707-106">Companies are turning toodeep learning toosolve hard problems, like [image classification](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [speech recognition](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html), object recognition, and machine translation.</span></span> 

<span data-ttu-id="2c707-107">有[許多受歡迎的架構](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software)，包括 [Microsoft 認知工具組](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/)、[Tensorflow](https://www.tensorflow.org/)MXNet、Theano 等等。Caffe 是其中一個 hello 最知名的非符號 （命令式） 類神經網路架構，而且也廣泛使用在許多方面，包括電腦視覺。</span><span class="sxs-lookup"><span data-stu-id="2c707-107">There are [many popular frameworks](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), including [Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano, etc. Caffe is one of hello most famous non-symbolic (imperative) neural network frameworks, and widely used in many areas including computer vision.</span></span> <span data-ttu-id="2c707-108">此外，[CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) 結合 Caffe 與 Apache Spark，在此情況下，深入學習可輕鬆地用於現有的 Hadoop 叢集結合 Spark ETL 管線，以減少系統複雜度和端對端學習的延遲。</span><span class="sxs-lookup"><span data-stu-id="2c707-108">Furthermore, [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) combines Caffe with Apache Spark, in which case deep learning can be easily used on an existing Hadoop cluster together with Spark ETL pipelines, reducing system complexity and latency for end-to-end learning.</span></span>

<span data-ttu-id="2c707-109">[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/)只有完全受管理的雲端 Hadoop 供應項目可提供開放原始碼分析叢集針對 Spark、 Hive、 MapReduce、 HBase、 Storm、 Kafka 和最佳化 99.9 %sla 所支援的 R 伺服器為 hello。</span><span class="sxs-lookup"><span data-stu-id="2c707-109">[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) is hello only fully-managed cloud Hadoop offering that provides optimized open source analytic clusters for Spark, Hive, MapReduce, HBase, Storm, Kafka, and R Server backed by a 99.9% SLA.</span></span> <span data-ttu-id="2c707-110">每個巨量資料技術及 ISV 應用程式都可輕鬆部署為受管理的叢集，以提供企業級安全性和監視功能。</span><span class="sxs-lookup"><span data-stu-id="2c707-110">Each of these big data technologies and ISV applications are easily deployable as managed clusters with enterprise-level security and monitoring.</span></span>

<span data-ttu-id="2c707-111">有些使用者會詢問我們如何 toouse 深入了解 HDInsight 是 Microsoft 的 PaaS Hadoop 產品上。</span><span class="sxs-lookup"><span data-stu-id="2c707-111">Some users are asking us about how toouse deep learning on HDInsight, which is Microsoft's PaaS Hadoop product.</span></span> <span data-ttu-id="2c707-112">我們將會在多個 tooshare 在 hello 未來，但我們需要 toosummarize 如何技術部落格的今天 toouse Caffe HDInsight Spark 上。</span><span class="sxs-lookup"><span data-stu-id="2c707-112">We will have more tooshare in hello future, but today we want toosummarize a technical blog on how toouse Caffe on HDInsight Spark.</span></span>

<span data-ttu-id="2c707-113">如果您之前已安裝過 Caffe，您會發現安裝此架構有點困難。</span><span class="sxs-lookup"><span data-stu-id="2c707-113">If you have installed Caffe before, you will notice that installing this framework is a little bit challenging.</span></span> <span data-ttu-id="2c707-114">在這篇部落格，我們會先說明如何 tooinstall[上的 Spark Caffe](https://github.com/yahoo/CaffeOnSpark) HDInsight 叢集，然後使用內建 MNIST 示範 toodemostrate hello 如何 toouse 分散式深入學習使用 Cpu 上的 HDInsight Spark。</span><span class="sxs-lookup"><span data-stu-id="2c707-114">In this blog, we will first illustrate how tooinstall [Caffe on Spark](https://github.com/yahoo/CaffeOnSpark) for an HDInsight cluster, then use hello built-in MNIST demo toodemostrate how toouse Distributed Deep Learning using HDInsight Spark on CPUs.</span></span>

<span data-ttu-id="2c707-115">有四個主要步驟 tooget 它在 HDInsight 使用。</span><span class="sxs-lookup"><span data-stu-id="2c707-115">There are four major steps tooget it work on HDInsight.</span></span>

1. <span data-ttu-id="2c707-116">Hello 的所有節點上安裝所需的 hello 相依項目</span><span class="sxs-lookup"><span data-stu-id="2c707-116">Install hello required dependencies on all hello nodes</span></span>
2. <span data-ttu-id="2c707-117">Spark HDInsight Caffe 根據 hello 前端節點上</span><span class="sxs-lookup"><span data-stu-id="2c707-117">Build Caffe on Spark for HDInsight on hello head node</span></span>
3. <span data-ttu-id="2c707-118">發佈 hello 所需的程式庫 tooall hello 背景工作節點</span><span class="sxs-lookup"><span data-stu-id="2c707-118">Distribute hello required libraries tooall hello worker nodes</span></span>
4. <span data-ttu-id="2c707-119">撰寫 Caffe 模型，並以分散方式執行它</span><span class="sxs-lookup"><span data-stu-id="2c707-119">Compose a Caffe model and run it distributely</span></span>

<span data-ttu-id="2c707-120">HDInsight 是 PaaS 解決方案，因為它提供絕佳的平台功能-因此相當簡單 tooperform 某些工作。</span><span class="sxs-lookup"><span data-stu-id="2c707-120">Since HDInsight is a PaaS solution, it offers great platform features - so it is quite easy tooperform some tasks.</span></span> <span data-ttu-id="2c707-121">我們會大量使用此部落格文章中的 hello 功能在呼叫其中一個[指令碼動作](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)，與您可以執行殼層命令 toocustomize 叢集節點 （前端節點、 背景工作節點或邊緣節點）。</span><span class="sxs-lookup"><span data-stu-id="2c707-121">One of hello features that we heavily use in this blog post is called [Script Action](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), with which you can execute shell commands toocustomize cluster nodes (head node, worker node, or edge node).</span></span>

## <a name="step-1--install-hello-required-dependencies-on-all-hello-nodes"></a><span data-ttu-id="2c707-122">步驟 1: Hello 的所有節點上安裝所需的 hello 相依項目</span><span class="sxs-lookup"><span data-stu-id="2c707-122">Step 1:  Install hello required dependencies on all hello nodes</span></span>

<span data-ttu-id="2c707-123">啟動 tooget，我們需要我們需要 tooinstall hello 相依性。</span><span class="sxs-lookup"><span data-stu-id="2c707-123">tooget started, we need tooinstall hello dependencies we need.</span></span> <span data-ttu-id="2c707-124">hello Caffe 站台和[CaffeOnSpark 網站](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn)提供一些很有幫助 wiki 安裝 hello 相依性的 Spark，YARN 模式 （這是 HDInsight Spark hello 模式），但我們需要 tooadd 少數的多個相依性的 HDInsight 平台。</span><span class="sxs-lookup"><span data-stu-id="2c707-124">hello Caffe site and [CaffeOnSpark site](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) offers some very useful wiki for installing hello dependencies for Spark on YARN mode (which is hello mode for HDInsight Spark), but we need tooadd a few more dependencies for HDInsight platform.</span></span> <span data-ttu-id="2c707-125">我們將使用 hello 指令碼動作，如下所示，所有 hello 前端節點和背景工作節點上執行它。</span><span class="sxs-lookup"><span data-stu-id="2c707-125">We will use hello script action as below and run it on all hello head nodes and worker nodes.</span></span> <span data-ttu-id="2c707-126">此指令碼動作將需要大約 20 分鐘，因為這些相依性也取決於其他封裝。</span><span class="sxs-lookup"><span data-stu-id="2c707-126">This script action will take about 20 minutes, as those dependencies also depend on other packages.</span></span> <span data-ttu-id="2c707-127">您應該將它放在某些位置，存取 tooyour HDInsight 叢集，例如 GitHub 位置或 hello 預設 BLOB 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="2c707-127">You should put it in some location that is accessible tooyour HDInsight cluster, such as a GitHub location or hello default BLOB storage account.</span></span>

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


<span data-ttu-id="2c707-128">上述的 hello 指令碼動作有兩個步驟。</span><span class="sxs-lookup"><span data-stu-id="2c707-128">There are two steps in hello script action above.</span></span> <span data-ttu-id="2c707-129">hello 第一個步驟是 tooinstall 所有 hello 必要程式庫。</span><span class="sxs-lookup"><span data-stu-id="2c707-129">hello first step is tooinstall all hello required libraries.</span></span> <span data-ttu-id="2c707-130">這些程式庫包含編譯 Caffe （例如 gflags glog) 和執行 （例如 numpy) Caffe hello 必要的程式庫。</span><span class="sxs-lookup"><span data-stu-id="2c707-130">Those libraries include hello necessary libraries for both compiling Caffe(such as gflags, glog) and running Caffe (such as numpy).</span></span> <span data-ttu-id="2c707-131">我們使用 libatlas CPU 最佳化，但您永遠可以依照 hello CaffeOnSpark wiki 需安裝其他最佳化程式庫，例如 MKL 或 CUDA （適用於 GPU)。</span><span class="sxs-lookup"><span data-stu-id="2c707-131">We are using libatlas for CPU optimization, but you can always follow hello CaffeOnSpark wiki on installing other optimization libraries, such as MKL or CUDA (for GPU).</span></span>

<span data-ttu-id="2c707-132">hello 第二步是 toodownload、 編譯和執行階段期間安裝 protobuf 2.5.0 Caffe 的。</span><span class="sxs-lookup"><span data-stu-id="2c707-132">hello second step is toodownload, compile, and install protobuf 2.5.0 for Caffe during runtime.</span></span> <span data-ttu-id="2c707-133">Protobuf 2.5.0[無須](https://github.com/yahoo/CaffeOnSpark/issues/87)，但是這個版本並非為 Ubuntu 16 上的封裝可使用，因此我們需要 toocompile 從 hello 原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="2c707-133">Protobuf 2.5.0 [is required](https://github.com/yahoo/CaffeOnSpark/issues/87), however this version is not available as a package on Ubuntu 16, so we need toocompile it from hello source code.</span></span> <span data-ttu-id="2c707-134">另外還有幾個資源上如何 hello 網際網路 toocompile，例如[這](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)</span><span class="sxs-lookup"><span data-stu-id="2c707-134">There are also a few resources on hello Internet on how toocompile it, such as [this](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)</span></span>

<span data-ttu-id="2c707-135">toosimply 開始，您可以只執行此指令碼動作對叢集 tooall hello 背景工作節點和前端節點 （適用於 HDInsight 3.5)。</span><span class="sxs-lookup"><span data-stu-id="2c707-135">toosimply get started, you can just run this script action against your cluster tooall hello worker nodes and head nodes (for HDInsight 3.5).</span></span> <span data-ttu-id="2c707-136">您可以執行 hello 指令碼動作執行的叢集，或者您也可以執行 hello 指令碼動作在 hello 叢集佈建時間。</span><span class="sxs-lookup"><span data-stu-id="2c707-136">You can either run hello script actions for a running cluster, or you can also run hello script actions during hello cluster provision time.</span></span> <span data-ttu-id="2c707-137">如需有關 hello 指令碼動作的詳細資訊，請參閱 hello 文件[這裡](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)</span><span class="sxs-lookup"><span data-stu-id="2c707-137">For more details on hello script actions, please see hello documentation [here](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)</span></span>

![指令碼動作 tooInstall 相依性](./media/hdinsight-deep-learning-caffe-spark/Script-Action-1.png)


## <a name="step-2-build-caffe-on-spark-for-hdinsight-on-hello-head-node"></a><span data-ttu-id="2c707-139">步驟 2： 根據 Caffe Spark HDInsight hello 前端節點上</span><span class="sxs-lookup"><span data-stu-id="2c707-139">Step 2: Build Caffe on Spark for HDInsight on hello head node</span></span>

<span data-ttu-id="2c707-140">hello 第二個步驟是 toobuild Caffe hello 叢集前端節點，在然後將發佈 hello 編譯的程式庫 tooall hello 背景工作節點。</span><span class="sxs-lookup"><span data-stu-id="2c707-140">hello second step is toobuild Caffe on hello headnode, and then distribute hello compiled libraries tooall hello worker nodes.</span></span> <span data-ttu-id="2c707-141">在此步驟中，您將需要太[ssh 到您的叢集前端節點](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix)，只要遵循 hello [CaffeOnSpark 建置程序](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn)下面是 hello 指令碼，您可以使用 toobuild CaffeOnSpark 搭配一些額外的步驟。</span><span class="sxs-lookup"><span data-stu-id="2c707-141">In this step, you will need too[ssh into your headnode](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), then simply follow hello [CaffeOnSpark build process](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), and below is hello script you can use toobuild CaffeOnSpark with a few additional steps.</span></span> 

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

<span data-ttu-id="2c707-142">您可能需要 toodo 超過 CaffeOnSpark 哪些 hello 文件，該處會指示。</span><span class="sxs-lookup"><span data-stu-id="2c707-142">You may need toodo more than what hello documentation of CaffeOnSpark says.</span></span> <span data-ttu-id="2c707-143">hello 變更如下：</span><span class="sxs-lookup"><span data-stu-id="2c707-143">hello changes are:</span></span>
- <span data-ttu-id="2c707-144">變更只 tooCPU 並針對此特定用途使用 libatlas。</span><span class="sxs-lookup"><span data-stu-id="2c707-144">Change tooCPU only and use libatlas for this particular purpose.</span></span>
- <span data-ttu-id="2c707-145">Put 的 hello 資料集 toohello BLOB 儲存體，這是可存取 tooall 背景工作節點，以供稍後使用的共用的位置。</span><span class="sxs-lookup"><span data-stu-id="2c707-145">Put hello datasets toohello BLOB storage, which is a shared location that is accessible tooall worker nodes for later use.</span></span>
- <span data-ttu-id="2c707-146">Put 的 hello 編譯 Caffe 文件庫 tooBLOB 儲存體，稍後您將會複製使用指令碼動作 tooavoid 其他的編譯時間這些程式庫 tooall hello 節點。</span><span class="sxs-lookup"><span data-stu-id="2c707-146">Put hello compiled Caffe libraries tooBLOB storage, and later you will copy those libraries tooall hello nodes using script actions tooavoid additional compilation time.</span></span>


### <a name="troubleshooting-an-ant-buildexception-has-occured-exec-returned-2"></a><span data-ttu-id="2c707-147">疑難排解︰發生 Ant BuildException︰exec 傳回︰2</span><span class="sxs-lookup"><span data-stu-id="2c707-147">Troubleshooting: An Ant BuildException has occured: exec returned: 2</span></span>

<span data-ttu-id="2c707-148">當第一次嘗試 toobuild CaffeOnSpark，有時它會顯示</span><span class="sxs-lookup"><span data-stu-id="2c707-148">When first trying toobuild CaffeOnSpark, sometimes it will say</span></span>

    failed tooexecute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2

<span data-ttu-id="2c707-149">由 「 請清除 「 只是全新的 hello 程式碼儲存機制，然後執行 「 請建置 「 即可解決此問題，只要您持有 hello 正確的依存性。</span><span class="sxs-lookup"><span data-stu-id="2c707-149">Simply clean hello code repository by "make clean" and then run "make build" will solve this issue, as long as you have hello correct dependencies.</span></span>

### <a name="troubleshooting-maven-repository-connection-time-out"></a><span data-ttu-id="2c707-150">疑難排解︰Maven 儲存機制連線逾時</span><span class="sxs-lookup"><span data-stu-id="2c707-150">Troubleshooting: Maven repository connection time out</span></span>

<span data-ttu-id="2c707-151">有時 maven 讓我 hello 連接逾時錯誤，類似 toobelow:</span><span class="sxs-lookup"><span data-stu-id="2c707-151">Sometimes maven gives me hello connection time out error, similar toobelow:</span></span>

    Retry:
    [INFO] Downloading: https://repo.maven.apache.org/maven2/com/twitter/chill_2.11/0.8.0/chill_2.11-0.8.0.jar
    Feb 01, 2017 5:14:49 AM org.apache.maven.wagon.providers.http.httpclient.impl.execchain.RetryExec execute
    INFO: I/O exception (java.net.SocketException) caught when processing request too{s}->https://repo.maven.apache.org:443: Connection timed out (Read failed)

<span data-ttu-id="2c707-152">它將會是 OK 之後等候幾分鐘的時間，並再試 toorebuild hello 程式碼，因此它可能 Maven 由於某種原因而限制 hello 從給定的 IP 位址的流量。</span><span class="sxs-lookup"><span data-stu-id="2c707-152">It will be OK after waiting for a few minutes and then just try toorebuild hello code, so it might be Maven somehow limits hello traffic from a given IP address.</span></span>


### <a name="troubleshooting-test-failure-for-caffe"></a><span data-ttu-id="2c707-153">疑難排解︰Caffe 測試失敗</span><span class="sxs-lookup"><span data-stu-id="2c707-153">Troubleshooting: Test failure for Caffe</span></span>

<span data-ttu-id="2c707-154">您可能會看到測試失敗時的 CaffeOnSpark，與下面類似的 hello 最終檢查。</span><span class="sxs-lookup"><span data-stu-id="2c707-154">You probably will see a test failure when doing hello final check for CaffeOnSpark, similar with below.</span></span> <span data-ttu-id="2c707-155">這是 prabably 相關以 utf-8 編碼方式，但應該不會影響 Caffe hello 使用量</span><span class="sxs-lookup"><span data-stu-id="2c707-155">This is prabably related with UTF-8 encoding, but should not impact hello usage of Caffe</span></span>

    Run completed in 32 seconds, 78 milliseconds.
    Total number of tests run: 7
    Suites: completed 5, aborted 0
    Tests: succeeded 6, failed 1, canceled 0, ignored 0, pending 0
    *** 1 TEST FAILED ***

## <a name="step-3-distribute-hello-required-libraries-tooall-hello-worker-nodes"></a><span data-ttu-id="2c707-156">步驟 3： 散佈 hello 所需的程式庫 tooall hello 背景工作節點</span><span class="sxs-lookup"><span data-stu-id="2c707-156">Step 3: Distribute hello required libraries tooall hello worker nodes</span></span>

<span data-ttu-id="2c707-157">hello 下一個步驟是 toodistribute hello 程式庫 (基本上 hello 文件庫中 CaffeOnSpark/caffe 公用/發佈/lib/和 CaffeOnSpark/caffe-distri/發佈/lib /) tooall hello 節點。</span><span class="sxs-lookup"><span data-stu-id="2c707-157">hello next step is toodistribute hello libraries (basically hello libraries in CaffeOnSpark/caffe-public/distribute/lib/ and CaffeOnSpark/caffe-distri/distribute/lib/) tooall hello nodes.</span></span> <span data-ttu-id="2c707-158">在步驟 2 中，將這些程式庫在 BLOB 儲存體，並在此步驟中，我們將使用指令碼動作 toocopy 它 tooall hello 前端節點和背景工作節點。</span><span class="sxs-lookup"><span data-stu-id="2c707-158">In Step 2, we put those libraries on BLOB storage, and in this step, we will use script actions toocopy it tooall hello head nodes and worker nodes.</span></span>

<span data-ttu-id="2c707-159">toodo 執行指令碼動作，如下所示，簡單 （您需要 toopoint toohello 正確的位置特定 tooyour 叢集）：</span><span class="sxs-lookup"><span data-stu-id="2c707-159">toodo this, simple run a script action as below (you need toopoint toohello right location specific tooyour cluster):</span></span>

    #!/bin/bash
    hadoop fs -get wasb:///CaffeOnSpark /home/changetoyourusername/

<span data-ttu-id="2c707-160">在步驟 2 中，我們將它放在 hello BLOB 儲存體，這是可存取 tooall hello 節點，因為在此步驟中我們只將它複製 tooall hello 節點。</span><span class="sxs-lookup"><span data-stu-id="2c707-160">Because in step 2, we put it on hello BLOB storage which is accessible tooall hello nodes, in this step we just simply copy it tooall hello nodes.</span></span>

## <a name="step-4-compose-a-caffe-model-and-run-it-distributely"></a><span data-ttu-id="2c707-161">步驟 4︰撰寫 Caffe 模型，並以分散方式執行它</span><span class="sxs-lookup"><span data-stu-id="2c707-161">Step 4: Compose a Caffe model and run it distributely</span></span>

<span data-ttu-id="2c707-162">執行上述步驟 hello 之後, Caffe hello 叢集前端節點上安裝完成後，我們很好的 toogo。</span><span class="sxs-lookup"><span data-stu-id="2c707-162">After running hello above steps, Caffe is alreay installed on hello headnode and we are good toogo.</span></span> <span data-ttu-id="2c707-163">hello 下一個步驟是 toowrite Caffe 模型。</span><span class="sxs-lookup"><span data-stu-id="2c707-163">hello next step is toowrite a Caffe model.</span></span> 

<span data-ttu-id="2c707-164">Caffe 正在使用"易懂 architecture"，在撰寫模型，您只需要 toodefine 組態檔，而不完全 （在大部分情況下） 撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="2c707-164">Caffe is using an "expressive architecture", where for composing a model, you just need toodefine a configuration file, and without coding at all (in most cases).</span></span> <span data-ttu-id="2c707-165">現在讓我們來看看那裡。</span><span class="sxs-lookup"><span data-stu-id="2c707-165">So let's take a look there.</span></span> 

<span data-ttu-id="2c707-166">hello 今天，我們將定型的模型是 MNIST 訓練範例模型。</span><span class="sxs-lookup"><span data-stu-id="2c707-166">hello model we will train today is a sample model for MNIST training.</span></span> <span data-ttu-id="2c707-167">手寫的數字的 hello MNIST 資料庫有個 60,000 範例中，定型集和測試集的 10,000 的範例。</span><span class="sxs-lookup"><span data-stu-id="2c707-167">hello MNIST database of handwritten digits has a training set of 60,000 examples, and a test set of 10,000 examples.</span></span> <span data-ttu-id="2c707-168">它是一組可從 NIST 提供之較大集的子集。</span><span class="sxs-lookup"><span data-stu-id="2c707-168">It is a subset of a larger set available from NIST.</span></span> <span data-ttu-id="2c707-169">hello 數字已大小正規化和固定大小的映像中置中。</span><span class="sxs-lookup"><span data-stu-id="2c707-169">hello digits have been size-normalized and centered in a fixed-size image.</span></span> <span data-ttu-id="2c707-170">CaffeOnSpark 有某些指令碼 toodownload hello 資料集，並將它轉換成 hello 正確的格式。</span><span class="sxs-lookup"><span data-stu-id="2c707-170">CaffeOnSpark has some scripts toodownload hello dataset and convert it into hello right format.</span></span>

<span data-ttu-id="2c707-171">CaffeOnSpark 針對 MNIST 訓練提供一些網路拓樸範例。</span><span class="sxs-lookup"><span data-stu-id="2c707-171">CaffeOnSpark provides some network topologies example for MNIST training.</span></span> <span data-ttu-id="2c707-172">它有 nice 設計的分割 hello 網路架構 （hello 網路中的 hello 拓撲） 和最佳化。</span><span class="sxs-lookup"><span data-stu-id="2c707-172">It has a nice design of splitting hello network architecture (hello topology of hello network) and optimization.</span></span> <span data-ttu-id="2c707-173">在此情況下，需要兩個檔案︰</span><span class="sxs-lookup"><span data-stu-id="2c707-173">In this case, There are two files required:</span></span> 

<span data-ttu-id="2c707-174">hello"規劃求解 」 檔案 （${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt） 用於愈加 hello 最佳化，並產生參數更新。</span><span class="sxs-lookup"><span data-stu-id="2c707-174">hello "Solver" file (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) is used for overseeing hello optimization and generating parameter updates.</span></span> <span data-ttu-id="2c707-175">比方說，它會定義是否 CPU 或 GPU 將用於，什麼是 hello 動量會多少反覆項目，等等。它也會定義哪些神經網路拓樸應該 hello （這是我們需要 hello 第二個檔案） 的程式使用。</span><span class="sxs-lookup"><span data-stu-id="2c707-175">For example, it defines whether CPU or GPU will be used, what's hello momentum, how many iterations will be, etc. It also defines which neuron network topology should hello program use (which is hello second file we need).</span></span> <span data-ttu-id="2c707-176">如需有關規劃求解的詳細資訊，請參閱太[Caffe 文件](http://caffe.berkeleyvision.org/tutorial/solver.html)。</span><span class="sxs-lookup"><span data-stu-id="2c707-176">For more information about Solver, please refer too[Caffe documentation](http://caffe.berkeleyvision.org/tutorial/solver.html).</span></span>

<span data-ttu-id="2c707-177">例如，因為我們使用 CPU，而不是 GPU，我們應該變更 hello 最後一行以：</span><span class="sxs-lookup"><span data-stu-id="2c707-177">For this example, since we are using CPU rather than GPU, we should change hello last line to:</span></span>

    # solver mode: CPU or GPU
    solver_mode: CPU

![Caffe 組態](./media/hdinsight-deep-learning-caffe-spark/Caffe-1.png)

<span data-ttu-id="2c707-179">您可以視需要變更其他行。</span><span class="sxs-lookup"><span data-stu-id="2c707-179">You can change other lines as needed.</span></span>

<span data-ttu-id="2c707-180">hello 第二個檔案 （${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt） 會定義如何 hello 神經網路看起來，hello 相關輸入和輸出檔。</span><span class="sxs-lookup"><span data-stu-id="2c707-180">hello second file (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) defines how hello neuron network looks like, and hello relevant input and output file.</span></span> <span data-ttu-id="2c707-181">我們也需要 tooupdate hello 檔案 tooreflect hello 定型資料的位置。</span><span class="sxs-lookup"><span data-stu-id="2c707-181">We also need tooupdate hello file tooreflect hello training data location.</span></span> <span data-ttu-id="2c707-182">變更下列的 lenet_memory_train_test.prototxt （您需要 toopoint toohello 正確的位置特定 tooyour 叢集） 中組件的 hello:</span><span class="sxs-lookup"><span data-stu-id="2c707-182">Change hello following part in lenet_memory_train_test.prototxt (you need toopoint toohello right location specific tooyour cluster):</span></span>

- <span data-ttu-id="2c707-183">也變更 hello"file:/Users/mridul/bigml/demodl/mnist_train_lmdb""wasb: / 專案/machine_learning/image_dataset/mnist_train_lmdb"</span><span class="sxs-lookup"><span data-stu-id="2c707-183">change hello "file:/Users/mridul/bigml/demodl/mnist_train_lmdb" too"wasb:///projects/machine_learning/image_dataset/mnist_train_lmdb"</span></span>
- <span data-ttu-id="2c707-184">變更 「 file:/Users/mridul/bigml/demodl/mnist_test_lmdb/ 」 太"wasb: / 專案/machine_learning/image_dataset/mnist_test_lmdb"</span><span class="sxs-lookup"><span data-stu-id="2c707-184">change "file:/Users/mridul/bigml/demodl/mnist_test_lmdb/" too"wasb:///projects/machine_learning/image_dataset/mnist_test_lmdb"</span></span>

![Caffe 組態](./media/hdinsight-deep-learning-caffe-spark/Caffe-2.png)

<span data-ttu-id="2c707-186">如需有關如何 toodefine hello 網路的詳細資訊，請檢查 hello [Caffe MNIST 資料集上的文件](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)</span><span class="sxs-lookup"><span data-stu-id="2c707-186">For more information on how toodefine hello network, please check hello [Caffe documentation on MNIST dataset](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)</span></span>

<span data-ttu-id="2c707-187">為了 hello 這篇部落格，我們只會使用這個簡單的 MNIST 範例。</span><span class="sxs-lookup"><span data-stu-id="2c707-187">For hello purpose of this blog, we just use this simple MNIST example.</span></span> <span data-ttu-id="2c707-188">您應該從 hello 前端節點執行下面的 hello 命令：</span><span class="sxs-lookup"><span data-stu-id="2c707-188">You should run hello command below from hello head node:</span></span>

    spark-submit --master yarn --deploy-mode cluster --num-executors 8 --files ${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt,${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt --conf spark.driver.extraLibraryPath="${LD_LIBRARY_PATH}" --conf spark.executorEnv.LD_LIBRARY_PATH="${LD_LIBRARY_PATH}" --class com.yahoo.ml.caffe.CaffeOnSpark ${CAFFE_ON_SPARK}/caffe-grid/target/caffe-grid-0.1-SNAPSHOT-jar-with-dependencies.jar -train -features accuracy,loss -label label -conf lenet_memory_solver.prototxt -devices 1 -connection ethernet -model wasb:///mnist.model -output wasb:///mnist_features_result

<span data-ttu-id="2c707-189">基本上它能將散發所需的 hello 檔案 （lenet_memory_solver.prototxt 和 lenet_memory_train_test.prototxt） tooeach YARN 容器，而且也設 hello 相關的每個 Spark 執行程式的驅動程式/tooLD_LIBRARY_PATH，hello 中定義的路徑前一個程式碼片段和點 toohello 位置具有 CaffeOnSpark 文件庫。</span><span class="sxs-lookup"><span data-stu-id="2c707-189">Basically it distributes hello required files (lenet_memory_solver.prototxt and lenet_memory_train_test.prototxt) tooeach YARN container, and also set hello relevant PATH of each Spark driver/executor tooLD_LIBRARY_PATH, which is defined in hello previous code snippet and points toohello location that has CaffeOnSpark libraries.</span></span> 

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="2c707-190">監視與疑難排解</span><span class="sxs-lookup"><span data-stu-id="2c707-190">Monitoring and troubleshooting</span></span>

<span data-ttu-id="2c707-191">因為我們使用 YARN 叢集模式，在此情況下 hello Spark 驅動程式將會排定的 tooan 任意容器 （和任意的背景工作節點） 只能中應該會出現類似 hello 主控台輸出：</span><span class="sxs-lookup"><span data-stu-id="2c707-191">Since we are using YARN cluster mode, in which case hello Spark driver will be scheduled tooan arbitrary container (and an arbitrary worker node) you should only see in hello console outputting something like:</span></span>

    17/02/01 23:22:16 INFO Client: Application report for application_1485916338528_0015 (state: RUNNING)

<span data-ttu-id="2c707-192">如果您想 tooknow 發生了什麼事，您通常需要 tooget hello Spark 驅動程式的記錄檔，其中有詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="2c707-192">If you want tooknow what happened, you usually need tooget hello Spark driver's log, which has more information.</span></span> <span data-ttu-id="2c707-193">在此情況下，您需要 toogo toohello YARN UI toofind hello 相關 YARN 記錄。</span><span class="sxs-lookup"><span data-stu-id="2c707-193">In this case, you need toogo toohello YARN UI toofind hello relevant YARN logs.</span></span> <span data-ttu-id="2c707-194">您可以取得此 url 的 YARN UI hello:</span><span class="sxs-lookup"><span data-stu-id="2c707-194">You can get hello YARN UI by this URL:</span></span> 

    https://yourclustername.azurehdinsight.net/yarnui
   
![YARN UI](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-1.png)

<span data-ttu-id="2c707-196">您可以看看此特定應用程式配置了多少資源。</span><span class="sxs-lookup"><span data-stu-id="2c707-196">You can take a look at how many resources are allocated for this particular application.</span></span> <span data-ttu-id="2c707-197">您可以按一下 hello 」 排程器 」 連結，然後您會看到這個應用程式中，有 9 執行的容器。</span><span class="sxs-lookup"><span data-stu-id="2c707-197">You can click hello "Scheduler" link, and then you will see that for this application, there are 9 containers running.</span></span> <span data-ttu-id="2c707-198">我們要求 YARN tooprovide 8 執行程式，而另一個容器是驅動程式處理序。</span><span class="sxs-lookup"><span data-stu-id="2c707-198">We ask YARN tooprovide 8 executors, and another container is for driver process.</span></span> 

![YARN 排程器](./media/hdinsight-deep-learning-caffe-spark/YARN-Scheduler.png)

<span data-ttu-id="2c707-200">如果發生失敗，您可能想 toocheck hello 驅動程式記錄檔或容器的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="2c707-200">You may want toocheck hello  driver logs or container logs if there are failures.</span></span> <span data-ttu-id="2c707-201">驅動程式記錄檔，您可以按一下 hello YARN UI 中的應用程式識別碼，然後按一下 hello 」 記錄檔 」 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2c707-201">For driver logs, you can click hello application ID in YARN UI, then click hello "Logs" button.</span></span> <span data-ttu-id="2c707-202">hello 驅動程式記錄檔會寫入至 stderr。</span><span class="sxs-lookup"><span data-stu-id="2c707-202">hello driver logs are written into stderr.</span></span>

![YARN UI 2](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-2.png)

<span data-ttu-id="2c707-204">例如，您會看到一些 hello 驅動程式記錄檔，從下方的 hello 錯誤指出配置太多的執行程式。</span><span class="sxs-lookup"><span data-stu-id="2c707-204">For example, you might see some of hello error below from hello driver logs, indicating you allocate too many executors.</span></span>

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

<span data-ttu-id="2c707-205">某些情況下，執行程式，而不是驅動程式中的 hello 問題可能會發生。</span><span class="sxs-lookup"><span data-stu-id="2c707-205">Sometimes, hello issue can happen in executors rather than drivers.</span></span> <span data-ttu-id="2c707-206">在此情況下，您需要 toocheck hello 容器的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="2c707-206">In this case, you need toocheck hello container logs.</span></span> <span data-ttu-id="2c707-207">您可以一律取得 hello 容器記錄檔，然後 hello 失敗的容器。</span><span class="sxs-lookup"><span data-stu-id="2c707-207">You can always get hello container logs, and then get hello failed container.</span></span> <span data-ttu-id="2c707-208">例如，您在執行 Caffe 時可能會遇到此失敗。</span><span class="sxs-lookup"><span data-stu-id="2c707-208">For example, you might meet this failure when running Caffe.</span></span>

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

<span data-ttu-id="2c707-209">在此情況下，您需要 tooget hello 失敗容器識別碼 （在上述案例 hello，它是 container_1485916338528_0008_05_000005）。</span><span class="sxs-lookup"><span data-stu-id="2c707-209">In this case, you need tooget hello failed container ID (in hello above case, it is container_1485916338528_0008_05_000005).</span></span> <span data-ttu-id="2c707-210">您需要 toorun</span><span class="sxs-lookup"><span data-stu-id="2c707-210">Then you need toorun</span></span> 

    yarn logs -containerId container_1485916338528_0008_03_000005

<span data-ttu-id="2c707-211">從 hello 叢集前端節點。</span><span class="sxs-lookup"><span data-stu-id="2c707-211">from hello headnode.</span></span> <span data-ttu-id="2c707-212">在檢查容器失敗之後，它是由使用 lenet_memory_solver.prototxt 中的 GPU 模式 (您應該改用 CPU 模式) 所引起。</span><span class="sxs-lookup"><span data-stu-id="2c707-212">After checking container failure, it is caused by using GPU mode (where you should use CPU mode instead) in lenet_memory_solver.prototxt.</span></span>

    17/02/01 07:10:48 INFO LMDB: Batch size:100
    WARNING: Logging before InitGoogleLogging() is written tooSTDERR
    F0201 07:10:48.309725 11624 common.cpp:79] Cannot use GPU in CPU-only Caffe: check mode.


## <a name="getting-results"></a><span data-ttu-id="2c707-213">取得結果</span><span class="sxs-lookup"><span data-stu-id="2c707-213">Getting results</span></span>

<span data-ttu-id="2c707-214">因為我們會配置 8 執行程式，而且 hello 網路拓撲很簡單，它應該只採用大約 30 分鐘 toorun hello 結果。</span><span class="sxs-lookup"><span data-stu-id="2c707-214">Since we are allocating 8 executors, and hello network topology is simple, it should only take around 30 minutes toorun hello result.</span></span> <span data-ttu-id="2c707-215">從 hello 命令列中，您可以看到我們放 hello 模型 toowasb:///mnist.model，並將名為 wasb hello 結果 tooa 資料夾: / / mnist_features_result。</span><span class="sxs-lookup"><span data-stu-id="2c707-215">From hello command line, you can see that we put hello model toowasb:///mnist.model, and put hello results tooa folder named wasb:///mnist_features_result.</span></span>

<span data-ttu-id="2c707-216">您可以透過執行取得 hello 結果</span><span class="sxs-lookup"><span data-stu-id="2c707-216">You can get hello results by running</span></span>

    hadoop fs -cat hdfs:///mnist_features_result/*

<span data-ttu-id="2c707-217">和 hello 結果如下所示：</span><span class="sxs-lookup"><span data-stu-id="2c707-217">and hello result looks like:</span></span>

    {"SampleID":"00009597","accuracy":[1.0],"loss":[0.028171852],"label":[2.0]}
    {"SampleID":"00009598","accuracy":[1.0],"loss":[0.028171852],"label":[6.0]}
    {"SampleID":"00009599","accuracy":[1.0],"loss":[0.028171852],"label":[1.0]}
    {"SampleID":"00009600","accuracy":[0.97],"loss":[0.0677709],"label":[5.0]}
    {"SampleID":"00009601","accuracy":[0.97],"loss":[0.0677709],"label":[0.0]}
    {"SampleID":"00009602","accuracy":[0.97],"loss":[0.0677709],"label":[1.0]}
    {"SampleID":"00009603","accuracy":[0.97],"loss":[0.0677709],"label":[2.0]}
    {"SampleID":"00009604","accuracy":[0.97],"loss":[0.0677709],"label":[3.0]}
    {"SampleID":"00009605","accuracy":[0.97],"loss":[0.0677709],"label":[4.0]}

<span data-ttu-id="2c707-218">hello SampleID 代表 hello 識別碼 hello MNIST 資料集中，且 hello 標籤 hello hello 模型的數字識別。</span><span class="sxs-lookup"><span data-stu-id="2c707-218">hello SampleID represents hello ID in hello MNIST dataset, and hello label is hello number that hello model identifies.</span></span>


## <a name="conclusion"></a><span data-ttu-id="2c707-219">結論</span><span class="sxs-lookup"><span data-stu-id="2c707-219">Conclusion</span></span>

<span data-ttu-id="2c707-220">這份文件，在您嘗試 tooinstall CaffeOnSpark 執行簡單的範例。</span><span class="sxs-lookup"><span data-stu-id="2c707-220">In this documentation, you have tried tooinstall CaffeOnSpark with running a simple example.</span></span> <span data-ttu-id="2c707-221">HDInsight 是完整受管理的雲端分散式的運算平台，而 hello 大型的資料集上執行機器學習和進階的分析工作負載的最佳位置和分散式深層的了解，您可以使用 Caffe HDInsight Spark tooperform 深入學習工作。</span><span class="sxs-lookup"><span data-stu-id="2c707-221">HDInsight is a full managed cloud distributed compute platform, and is hello best place for running machine learning and advanced analytics workloads on large data set, and for distributed deep learning, you can use Caffe on HDInsight Spark tooperform deep learning tasks.</span></span>


## <span data-ttu-id="2c707-222"><a name="seealso"></a>另請參閱</span><span class="sxs-lookup"><span data-stu-id="2c707-222"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="2c707-223">概觀：Azure HDInsight 上的 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="2c707-223">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="2c707-224">案例</span><span class="sxs-lookup"><span data-stu-id="2c707-224">Scenarios</span></span>
* [<span data-ttu-id="2c707-225">Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度</span><span class="sxs-lookup"><span data-stu-id="2c707-225">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="2c707-226">機器學習的 Spark： 使用 HDInsight toopredict 食物檢查結果中的 Spark</span><span class="sxs-lookup"><span data-stu-id="2c707-226">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

### <a name="manage-resources"></a><span data-ttu-id="2c707-227">管理資源</span><span class="sxs-lookup"><span data-stu-id="2c707-227">Manage resources</span></span>
* [<span data-ttu-id="2c707-228">管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="2c707-228">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

