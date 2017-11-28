---
title: "在 Azure HDInsight Spark 上使用 Caffe 進行分散式深入學習 | Microsoft Docs"
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
ms.openlocfilehash: 14b7808c9534bce3049422d6bce1e8914b2c2fbc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-caffe-on-azure-hdinsight-spark-for-distributed-deep-learning"></a><span data-ttu-id="875f1-103">在 Azure HDInsight Spark 上使用 Caffe 進行分散式深入學習</span><span class="sxs-lookup"><span data-stu-id="875f1-103">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>


## <a name="introduction"></a><span data-ttu-id="875f1-104">簡介</span><span class="sxs-lookup"><span data-stu-id="875f1-104">Introduction</span></span>

<span data-ttu-id="875f1-105">深入學習的影響遍及醫療保健到傳輸到製造商等等。</span><span class="sxs-lookup"><span data-stu-id="875f1-105">Deep learning is impacting everything from healthcare to transportation to manufacturing, and more.</span></span> <span data-ttu-id="875f1-106">公司轉型為深度學習來解決艱難的問題，例如[影像分類](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/)[語音辨識](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html)、物件辨識和機器轉譯。</span><span class="sxs-lookup"><span data-stu-id="875f1-106">Companies are turning to deep learning to solve hard problems, like [image classification](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [speech recognition](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html), object recognition, and machine translation.</span></span> 

<span data-ttu-id="875f1-107">有[許多受歡迎的架構](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software)，包括 [Microsoft 認知工具組](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/)、[Tensorflow](https://www.tensorflow.org/)MXNet、Theano 等等。Caffe 是其中一個最著名的非符號 (必要) 類神經網路架構，並廣泛用在許多方面，包括電腦視覺。</span><span class="sxs-lookup"><span data-stu-id="875f1-107">There are [many popular frameworks](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), including [Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano, etc. Caffe is one of the most famous non-symbolic (imperative) neural network frameworks, and widely used in many areas including computer vision.</span></span> <span data-ttu-id="875f1-108">此外，[CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) 結合 Caffe 與 Apache Spark，在此情況下，深入學習可輕鬆地用於現有的 Hadoop 叢集結合 Spark ETL 管線，以減少系統複雜度和端對端學習的延遲。</span><span class="sxs-lookup"><span data-stu-id="875f1-108">Furthermore, [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) combines Caffe with Apache Spark, in which case deep learning can be easily used on an existing Hadoop cluster together with Spark ETL pipelines, reducing system complexity and latency for end-to-end learning.</span></span>

<span data-ttu-id="875f1-109">[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) 是唯一受完整管理的雲端 Hadoop 產品，為 Spark、Hive、MapReduce、HBase、Storm、Kafka 和 R 伺服器提供最佳化開放原始碼分析叢集，並提供 99.9% SLA 的支援。</span><span class="sxs-lookup"><span data-stu-id="875f1-109">[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) is the only fully-managed cloud Hadoop offering that provides optimized open source analytic clusters for Spark, Hive, MapReduce, HBase, Storm, Kafka, and R Server backed by a 99.9% SLA.</span></span> <span data-ttu-id="875f1-110">每個巨量資料技術及 ISV 應用程式都可輕鬆部署為受管理的叢集，以提供企業級安全性和監視功能。</span><span class="sxs-lookup"><span data-stu-id="875f1-110">Each of these big data technologies and ISV applications are easily deployable as managed clusters with enterprise-level security and monitoring.</span></span>

<span data-ttu-id="875f1-111">有些使用者會詢問有關如何在 HDInsight 上使用深入學習，也就是 Microsoft 的 PaaS Hadoop 產品。</span><span class="sxs-lookup"><span data-stu-id="875f1-111">Some users are asking us about how to use deep learning on HDInsight, which is Microsoft's PaaS Hadoop product.</span></span> <span data-ttu-id="875f1-112">我們在未來將會分享更多內容，但今天我們想要摘要列出有關如何使用 Caffe on HDInsight Spark 的技術部落格。</span><span class="sxs-lookup"><span data-stu-id="875f1-112">We will have more to share in the future, but today we want to summarize a technical blog on how to use Caffe on HDInsight Spark.</span></span>

<span data-ttu-id="875f1-113">如果您之前已安裝過 Caffe，您會發現安裝此架構有點困難。</span><span class="sxs-lookup"><span data-stu-id="875f1-113">If you have installed Caffe before, you will notice that installing this framework is a little bit challenging.</span></span> <span data-ttu-id="875f1-114">在此部落格中，我們會先說明如何針對 HDInsight 叢集安裝 [Caffe 在 Spark 上](https://github.com/yahoo/CaffeOnSpark)，然後使用內建 MNIST 示範來展示如何利用 CPU 上的 HDInsight Spark 來使用分散式深入學習。</span><span class="sxs-lookup"><span data-stu-id="875f1-114">In this blog, we will first illustrate how to install [Caffe on Spark](https://github.com/yahoo/CaffeOnSpark) for an HDInsight cluster, then use the built-in MNIST demo to demostrate how to use Distributed Deep Learning using HDInsight Spark on CPUs.</span></span>

<span data-ttu-id="875f1-115">要讓它在 HDInsight 上使用共有四個主要步驟。</span><span class="sxs-lookup"><span data-stu-id="875f1-115">There are four major steps to get it work on HDInsight.</span></span>

1. <span data-ttu-id="875f1-116">在所有節點上安裝必要的相依性</span><span class="sxs-lookup"><span data-stu-id="875f1-116">Install the required dependencies on all the nodes</span></span>
2. <span data-ttu-id="875f1-117">在前端節點上建置適用於 HDInsight 的 Spark Caffe</span><span class="sxs-lookup"><span data-stu-id="875f1-117">Build Caffe on Spark for HDInsight on the head node</span></span>
3. <span data-ttu-id="875f1-118">將所需的程式庫分散至所有背景工作角色節點</span><span class="sxs-lookup"><span data-stu-id="875f1-118">Distribute the required libraries to all the worker nodes</span></span>
4. <span data-ttu-id="875f1-119">撰寫 Caffe 模型，並以分散方式執行它</span><span class="sxs-lookup"><span data-stu-id="875f1-119">Compose a Caffe model and run it distributely</span></span>

<span data-ttu-id="875f1-120">由於 HDInsight 是 PaaS 的解決方案，它提供絕佳的平台功能 - 因此很容易就能執行某些工作。</span><span class="sxs-lookup"><span data-stu-id="875f1-120">Since HDInsight is a PaaS solution, it offers great platform features - so it is quite easy to perform some tasks.</span></span> <span data-ttu-id="875f1-121">我們在此部落格文章中經常使用的其中一個功能稱為[指令碼動作](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)，您可以用來執行 shell 命令以自訂叢集節點 (前端節點、背景工作角色節點或邊緣節點)。</span><span class="sxs-lookup"><span data-stu-id="875f1-121">One of the features that we heavily use in this blog post is called [Script Action](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), with which you can execute shell commands to customize cluster nodes (head node, worker node, or edge node).</span></span>

## <a name="step-1--install-the-required-dependencies-on-all-the-nodes"></a><span data-ttu-id="875f1-122">步驟 1︰在所有節點上安裝必要的相依性</span><span class="sxs-lookup"><span data-stu-id="875f1-122">Step 1:  Install the required dependencies on all the nodes</span></span>

<span data-ttu-id="875f1-123">若要開始，我們必須安裝我們需要的相依性。</span><span class="sxs-lookup"><span data-stu-id="875f1-123">To get started, we need to install the dependencies we need.</span></span> <span data-ttu-id="875f1-124">Caffe 網站和 [CaffeOnSpark 網站](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn)提供一些很有幫助的 wiki 可在 YARN 模式上安裝 Spark 的相依性 (這是 HDInsight Spark 的模式)，但我們必須多新增幾個 HDInsight 平台的相依性。</span><span class="sxs-lookup"><span data-stu-id="875f1-124">The Caffe site and [CaffeOnSpark site](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) offers some very useful wiki for installing the dependencies for Spark on YARN mode (which is the mode for HDInsight Spark), but we need to add a few more dependencies for HDInsight platform.</span></span> <span data-ttu-id="875f1-125">我們將使用如下所示的指令碼動作，並在所有的前端節點和背景工作角色節點上執行。</span><span class="sxs-lookup"><span data-stu-id="875f1-125">We will use the script action as below and run it on all the head nodes and worker nodes.</span></span> <span data-ttu-id="875f1-126">此指令碼動作將需要大約 20 分鐘，因為這些相依性也取決於其他封裝。</span><span class="sxs-lookup"><span data-stu-id="875f1-126">This script action will take about 20 minutes, as those dependencies also depend on other packages.</span></span> <span data-ttu-id="875f1-127">您應該將它放在 HDInsight 叢集可以存取的某個位置，例如 GitHub 位置或預設 BLOB 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="875f1-127">You should put it in some location that is accessible to your HDInsight cluster, such as a GitHub location or the default BLOB storage account.</span></span>

    #!/bin/bash
    #Please be aware that installing the below will add additional 20 mins to cluster creation because of the dependencies
    #installing all dependencies, including the ones mentioned in http://caffe.berkeleyvision.org/install_apt.html, as well a few packages that are not included in HDInsight, such as gflags, glog, lmdb, numpy
    #It seems numpy will only needed during compilation time, but for safety purpose we install them on all the nodes

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


<span data-ttu-id="875f1-128">上述指令碼動作中有兩個步驟。</span><span class="sxs-lookup"><span data-stu-id="875f1-128">There are two steps in the script action above.</span></span> <span data-ttu-id="875f1-129">第一個步驟是安裝所有必要的程式庫。</span><span class="sxs-lookup"><span data-stu-id="875f1-129">The first step is to install all the required libraries.</span></span> <span data-ttu-id="875f1-130">這些程式庫包含編譯 Caffe (例如 gflags、glog) 和執行 Caffe (例如 numpy) 的必要程式庫。</span><span class="sxs-lookup"><span data-stu-id="875f1-130">Those libraries include the necessary libraries for both compiling Caffe(such as gflags, glog) and running Caffe (such as numpy).</span></span> <span data-ttu-id="875f1-131">我們針對 CPU 最佳化使用 libatlas，但您一律可以依照 CaffeOnSpark wiki 安裝其他最佳化程式庫，例如 MKL 或 CUDA (適用於 GPU)。</span><span class="sxs-lookup"><span data-stu-id="875f1-131">We are using libatlas for CPU optimization, but you can always follow the CaffeOnSpark wiki on installing other optimization libraries, such as MKL or CUDA (for GPU).</span></span>

<span data-ttu-id="875f1-132">第二個步驟是在執行階段期間下載、編譯和安裝 Caffe 的 protobuf 2.5.0。</span><span class="sxs-lookup"><span data-stu-id="875f1-132">The second step is to download, compile, and install protobuf 2.5.0 for Caffe during runtime.</span></span> <span data-ttu-id="875f1-133">[需要](https://github.com/yahoo/CaffeOnSpark/issues/87) Protobuf 2.5.0，但這個版本不在 Ubuntu 16 以套件形式提供，因此我們需要從原始程式碼編譯它。</span><span class="sxs-lookup"><span data-stu-id="875f1-133">Protobuf 2.5.0 [is required](https://github.com/yahoo/CaffeOnSpark/issues/87), however this version is not available as a package on Ubuntu 16, so we need to compile it from the source code.</span></span> <span data-ttu-id="875f1-134">另外在網際網路上還有一些關於如何加以編譯的資源，例如[這個](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)</span><span class="sxs-lookup"><span data-stu-id="875f1-134">There are also a few resources on the Internet on how to compile it, such as [this](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)</span></span>

<span data-ttu-id="875f1-135">若是要簡易開始，您可以僅對叢集執行此指令碼動作至所有背景工作角色節點和前端節點 (適用於 HDInsight 3.5)。</span><span class="sxs-lookup"><span data-stu-id="875f1-135">To simply get started, you can just run this script action against your cluster to all the worker nodes and head nodes (for HDInsight 3.5).</span></span> <span data-ttu-id="875f1-136">您可以執行指令碼動作以執行叢集，或您也可以在叢集佈建階段期間執行指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="875f1-136">You can either run the script actions for a running cluster, or you can also run the script actions during the cluster provision time.</span></span> <span data-ttu-id="875f1-137">如需有關指令碼動作的詳細資訊，請參閱文件[這裡](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)</span><span class="sxs-lookup"><span data-stu-id="875f1-137">For more details on the script actions, please see the documentation [here](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)</span></span>

![安裝相依性的指令碼動作](./media/hdinsight-deep-learning-caffe-spark/Script-Action-1.png)


## <a name="step-2-build-caffe-on-spark-for-hdinsight-on-the-head-node"></a><span data-ttu-id="875f1-139">步驟 2︰在前端節點上建置適用於 HDInsight 的 Spark Caffe</span><span class="sxs-lookup"><span data-stu-id="875f1-139">Step 2: Build Caffe on Spark for HDInsight on the head node</span></span>

<span data-ttu-id="875f1-140">第二個步驟是在前端節點上建立 Caffe，然後將已編譯的程式庫傳送到所有背景工作角色節點。</span><span class="sxs-lookup"><span data-stu-id="875f1-140">The second step is to build Caffe on the headnode, and then distribute the compiled libraries to all the worker nodes.</span></span> <span data-ttu-id="875f1-141">在此步驟中，您將需要 [SSH 到您的前端節點](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix)，然後只需依照 [CaffeOnSpark 建置程序](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn)，下面是可用來以一些額外步驟建置 CaffeOnSpark 的指令碼。</span><span class="sxs-lookup"><span data-stu-id="875f1-141">In this step, you will need to [ssh into your headnode](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), then simply follow the [CaffeOnSpark build process](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), and below is the script you can use to build CaffeOnSpark with a few additional steps.</span></span> 

    #!/bin/bash
    git clone https://github.com/yahoo/CaffeOnSpark.git --recursive
    export CAFFE_ON_SPARK=$(pwd)/CaffeOnSpark

    pushd ${CAFFE_ON_SPARK}/caffe-public/
    cp Makefile.config.example Makefile.config
    echo "INCLUDE_DIRS += ${JAVA_HOME}/include" >> Makefile.config
    #Below configurations might need to be updated based on actual cases. For example, if you are using GPU, or using a different BLAS library, you may want to update those settings accordingly.
    echo "CPU_ONLY := 1" >> Makefile.config
    echo "BLAS := atlas" >> Makefile.config
    echo "INCLUDE_DIRS += /usr/include/hdf5/serial/" >> Makefile.config
    echo "LIBRARY_DIRS += /usr/lib/x86_64-linux-gnu/hdf5/serial/" >> Makefile.config
    popd

    #compile CaffeOnSpark
    pushd ${CAFFE_ON_SPARK}
    #always clean up the environment before building (especially when rebuiding), or there will be errors such as "failed to execute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2"
    make clean 
    #the build step usually takes 20~30 mins, since it has a lot maven dependencies
    make build 
    popd
    export LD_LIBRARY_PATH=${CAFFE_ON_SPARK}/caffe-public/distribute/lib:${CAFFE_ON_SPARK}/caffe-distri/distribute/lib

    hadoop fs -mkdir -p wasb:///projects/machine_learning/image_dataset

    ${CAFFE_ON_SPARK}/scripts/setup-mnist.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/mnist_*_lmdb wasb:///projects/machine_learning/image_dataset/

    ${CAFFE_ON_SPARK}/scripts/setup-cifar10.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/cifar10_*_lmdb wasb:///projects/machine_learning/image_dataset/

    #put the already compiled CaffeOnSpark libraries to wasb storage, then read back to each node using script actions. This is because CaffeOnSpark requires all the nodes have the libarries
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-public/distribute/lib/
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-distri/distribute/lib/* /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-public/distribute/lib/* /CaffeOnSpark/caffe-public/distribute/lib/

<span data-ttu-id="875f1-142">您可能需要執行 CaffeOnSpark 的文件顯示以外的作業。</span><span class="sxs-lookup"><span data-stu-id="875f1-142">You may need to do more than what the documentation of CaffeOnSpark says.</span></span> <span data-ttu-id="875f1-143">變更為：</span><span class="sxs-lookup"><span data-stu-id="875f1-143">The changes are:</span></span>
- <span data-ttu-id="875f1-144">只變更為 CPU 並使用 libatlas 於此特定目的。</span><span class="sxs-lookup"><span data-stu-id="875f1-144">Change to CPU only and use libatlas for this particular purpose.</span></span>
- <span data-ttu-id="875f1-145">將資料集放到 Blob 儲存體，也就是可以存取所有背景工作角色節點以供稍後使用的共用位置。</span><span class="sxs-lookup"><span data-stu-id="875f1-145">Put the datasets to the BLOB storage, which is a shared location that is accessible to all worker nodes for later use.</span></span>
- <span data-ttu-id="875f1-146">將已編譯的 Caffe 程式庫放至 Blob 儲存體，稍後您會將這些程式庫複製到使用指令碼動作以避免額外編譯時間的所有節點。</span><span class="sxs-lookup"><span data-stu-id="875f1-146">Put the compiled Caffe libraries to BLOB storage, and later you will copy those libraries to all the nodes using script actions to avoid additional compilation time.</span></span>


### <a name="troubleshooting-an-ant-buildexception-has-occured-exec-returned-2"></a><span data-ttu-id="875f1-147">疑難排解︰發生 Ant BuildException︰exec 傳回︰2</span><span class="sxs-lookup"><span data-stu-id="875f1-147">Troubleshooting: An Ant BuildException has occured: exec returned: 2</span></span>

<span data-ttu-id="875f1-148">當第一次嘗試建置 CaffeOnSpark 時，有時它會說</span><span class="sxs-lookup"><span data-stu-id="875f1-148">When first trying to build CaffeOnSpark, sometimes it will say</span></span>

    failed to execute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2

<span data-ttu-id="875f1-149">只要藉由 "make clean" 清除程式碼儲存機制，然後執行 "make build" 即可解決此問題，只要您有正確的相依性。</span><span class="sxs-lookup"><span data-stu-id="875f1-149">Simply clean the code repository by "make clean" and then run "make build" will solve this issue, as long as you have the correct dependencies.</span></span>

### <a name="troubleshooting-maven-repository-connection-time-out"></a><span data-ttu-id="875f1-150">疑難排解︰Maven 儲存機制連線逾時</span><span class="sxs-lookup"><span data-stu-id="875f1-150">Troubleshooting: Maven repository connection time out</span></span>

<span data-ttu-id="875f1-151">有時候 Maven 會顯示連線逾時錯誤，看起來如下︰</span><span class="sxs-lookup"><span data-stu-id="875f1-151">Sometimes maven gives me the connection time out error, similar to below:</span></span>

    Retry:
    [INFO] Downloading: https://repo.maven.apache.org/maven2/com/twitter/chill_2.11/0.8.0/chill_2.11-0.8.0.jar
    Feb 01, 2017 5:14:49 AM org.apache.maven.wagon.providers.http.httpclient.impl.execchain.RetryExec execute
    INFO: I/O exception (java.net.SocketException) caught when processing request to {s}->https://repo.maven.apache.org:443: Connection timed out (Read failed)

<span data-ttu-id="875f1-152">等候幾分鐘之後就會恢復，然後只需嘗試重建程式碼，因此，可能是 Maven 以某種方式限制來自指定 IP 位址的流量。</span><span class="sxs-lookup"><span data-stu-id="875f1-152">It will be OK after waiting for a few minutes and then just try to rebuild the code, so it might be Maven somehow limits the traffic from a given IP address.</span></span>


### <a name="troubleshooting-test-failure-for-caffe"></a><span data-ttu-id="875f1-153">疑難排解︰Caffe 測試失敗</span><span class="sxs-lookup"><span data-stu-id="875f1-153">Troubleshooting: Test failure for Caffe</span></span>

<span data-ttu-id="875f1-154">您可能會在進行 CaffeOnSpark 最終檢查時看到與下列類似的測試失敗。</span><span class="sxs-lookup"><span data-stu-id="875f1-154">You probably will see a test failure when doing the final check for CaffeOnSpark, similar with below.</span></span> <span data-ttu-id="875f1-155">這可能與 UTF-8 編碼方式相關，但應該不會影響 Caffe 的使用方式</span><span class="sxs-lookup"><span data-stu-id="875f1-155">This is prabably related with UTF-8 encoding, but should not impact the usage of Caffe</span></span>

    Run completed in 32 seconds, 78 milliseconds.
    Total number of tests run: 7
    Suites: completed 5, aborted 0
    Tests: succeeded 6, failed 1, canceled 0, ignored 0, pending 0
    *** 1 TEST FAILED ***

## <a name="step-3-distribute-the-required-libraries-to-all-the-worker-nodes"></a><span data-ttu-id="875f1-156">步驟 3︰將所需的程式庫分散至所有背景工作角色節點</span><span class="sxs-lookup"><span data-stu-id="875f1-156">Step 3: Distribute the required libraries to all the worker nodes</span></span>

<span data-ttu-id="875f1-157">下一步是將程式庫 (基本上為 CaffeOnSpark/caffe-public/distribute/lib/ 和 CaffeOnSpark/caffe-distri/distribute/lib/ 中的程式庫) 分散至所有節點。</span><span class="sxs-lookup"><span data-stu-id="875f1-157">The next step is to distribute the libraries (basically the libraries in CaffeOnSpark/caffe-public/distribute/lib/ and CaffeOnSpark/caffe-distri/distribute/lib/) to all the nodes.</span></span> <span data-ttu-id="875f1-158">在步驟 2 中，我們將這些程式庫放在 BLOB 儲存體，且在此步驟中，我們將使用指令碼動作，將它複製到所有的前端節點和背景工作角色節點。</span><span class="sxs-lookup"><span data-stu-id="875f1-158">In Step 2, we put those libraries on BLOB storage, and in this step, we will use script actions to copy it to all the head nodes and worker nodes.</span></span>

<span data-ttu-id="875f1-159">若要這樣做，只需執行如下所示的指令碼動作 (您需要指向您叢集特定的正確位置)︰</span><span class="sxs-lookup"><span data-stu-id="875f1-159">To do this, simple run a script action as below (you need to point to the right location specific to your cluster):</span></span>

    #!/bin/bash
    hadoop fs -get wasb:///CaffeOnSpark /home/changetoyourusername/

<span data-ttu-id="875f1-160">因為在步驟 2 中，我們將它放在可供所有節點存取的 BLOB 儲存體，在此步驟中我們只是將它複製到所有節點。</span><span class="sxs-lookup"><span data-stu-id="875f1-160">Because in step 2, we put it on the BLOB storage which is accessible to all the nodes, in this step we just simply copy it to all the nodes.</span></span>

## <a name="step-4-compose-a-caffe-model-and-run-it-distributely"></a><span data-ttu-id="875f1-161">步驟 4︰撰寫 Caffe 模型，並以分散方式執行它</span><span class="sxs-lookup"><span data-stu-id="875f1-161">Step 4: Compose a Caffe model and run it distributely</span></span>

<span data-ttu-id="875f1-162">在執行上述步驟之後，Caffe 便已安裝在前端節點上，而我們已經就緒。</span><span class="sxs-lookup"><span data-stu-id="875f1-162">After running the above steps, Caffe is alreay installed on the headnode and we are good to go.</span></span> <span data-ttu-id="875f1-163">下一個步驟是撰寫 Caffe 模型。</span><span class="sxs-lookup"><span data-stu-id="875f1-163">The next step is to write a Caffe model.</span></span> 

<span data-ttu-id="875f1-164">Caffe 是使用「快速架構」，其中針對撰寫模型，您只需要定義設定檔，而完全無需撰寫程式碼 (在大部分情況下)。</span><span class="sxs-lookup"><span data-stu-id="875f1-164">Caffe is using an "expressive architecture", where for composing a model, you just need to define a configuration file, and without coding at all (in most cases).</span></span> <span data-ttu-id="875f1-165">現在讓我們來看看那裡。</span><span class="sxs-lookup"><span data-stu-id="875f1-165">So let's take a look there.</span></span> 

<span data-ttu-id="875f1-166">現在我們要訓練的模型是 MNIST 訓練的範例模型。</span><span class="sxs-lookup"><span data-stu-id="875f1-166">The model we will train today is a sample model for MNIST training.</span></span> <span data-ttu-id="875f1-167">手寫數字的 MNIST 資料庫有 60,000 個範例的訓練集，以及 10,000 個範例的測試集。</span><span class="sxs-lookup"><span data-stu-id="875f1-167">The MNIST database of handwritten digits has a training set of 60,000 examples, and a test set of 10,000 examples.</span></span> <span data-ttu-id="875f1-168">它是一組可從 NIST 提供之較大集的子集。</span><span class="sxs-lookup"><span data-stu-id="875f1-168">It is a subset of a larger set available from NIST.</span></span> <span data-ttu-id="875f1-169">數字已大小正規化且在固定大小的影像置中。</span><span class="sxs-lookup"><span data-stu-id="875f1-169">The digits have been size-normalized and centered in a fixed-size image.</span></span> <span data-ttu-id="875f1-170">CaffeOnSpark 有一些指令碼可下載資料集，並將它轉換成正確的格式。</span><span class="sxs-lookup"><span data-stu-id="875f1-170">CaffeOnSpark has some scripts to download the dataset and convert it into the right format.</span></span>

<span data-ttu-id="875f1-171">CaffeOnSpark 針對 MNIST 訓練提供一些網路拓樸範例。</span><span class="sxs-lookup"><span data-stu-id="875f1-171">CaffeOnSpark provides some network topologies example for MNIST training.</span></span> <span data-ttu-id="875f1-172">它具有不錯的網路架構 (網路的拓撲) 分割設計和最佳化。</span><span class="sxs-lookup"><span data-stu-id="875f1-172">It has a nice design of splitting the network architecture (the topology of the network) and optimization.</span></span> <span data-ttu-id="875f1-173">在此情況下，需要兩個檔案︰</span><span class="sxs-lookup"><span data-stu-id="875f1-173">In this case, There are two files required:</span></span> 

<span data-ttu-id="875f1-174">"Solver" 檔案 (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) 用於監視最佳化並產生參數更新。</span><span class="sxs-lookup"><span data-stu-id="875f1-174">the "Solver" file (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) is used for overseeing the optimization and generating parameter updates.</span></span> <span data-ttu-id="875f1-175">例如，它會定義要使用 CPU 還是 GPU、趨勢為何，以及有多少反覆運算等等。它也會定義程式應該使用哪個神經網路拓撲 (也就是我們需要的第二個檔案)。</span><span class="sxs-lookup"><span data-stu-id="875f1-175">For example, it defines whether CPU or GPU will be used, what's the momentum, how many iterations will be, etc. It also defines which neuron network topology should the program use (which is the second file we need).</span></span> <span data-ttu-id="875f1-176">如需 Solver 的詳細資訊，請參閱 [Caffe 文件](http://caffe.berkeleyvision.org/tutorial/solver.html)。</span><span class="sxs-lookup"><span data-stu-id="875f1-176">For more information about Solver, please refer to [Caffe documentation](http://caffe.berkeleyvision.org/tutorial/solver.html).</span></span>

<span data-ttu-id="875f1-177">在此範例中，因為我們要使用 CPU 而不是 GPU，我們應該將最後一行變更為︰</span><span class="sxs-lookup"><span data-stu-id="875f1-177">For this example, since we are using CPU rather than GPU, we should change the last line to:</span></span>

    # solver mode: CPU or GPU
    solver_mode: CPU

![Caffe 組態](./media/hdinsight-deep-learning-caffe-spark/Caffe-1.png)

<span data-ttu-id="875f1-179">您可以視需要變更其他行。</span><span class="sxs-lookup"><span data-stu-id="875f1-179">You can change other lines as needed.</span></span>

<span data-ttu-id="875f1-180">第二個檔案 (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) 會定義神經網路看起來如何，以及相關的輸入和輸出檔。</span><span class="sxs-lookup"><span data-stu-id="875f1-180">The second file (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) defines how the neuron network looks like, and the relevant input and output file.</span></span> <span data-ttu-id="875f1-181">我們也需要更新檔案以反映訓練資料的位置。</span><span class="sxs-lookup"><span data-stu-id="875f1-181">We also need to update the file to reflect the training data location.</span></span> <span data-ttu-id="875f1-182">變更 lenet_memory_train_test.prototxt (您需要指向叢集特定的正確位置) 中的下列部分︰</span><span class="sxs-lookup"><span data-stu-id="875f1-182">Change the following part in lenet_memory_train_test.prototxt (you need to point to the right location specific to your cluster):</span></span>

- <span data-ttu-id="875f1-183">將 "file:/Users/mridul/bigml/demodl/mnist_train_lmdb" 變更為 "wasb:///projects/machine_learning/image_dataset/mnist_train_lmdb"</span><span class="sxs-lookup"><span data-stu-id="875f1-183">change the "file:/Users/mridul/bigml/demodl/mnist_train_lmdb" to "wasb:///projects/machine_learning/image_dataset/mnist_train_lmdb"</span></span>
- <span data-ttu-id="875f1-184">將 "file:/Users/mridul/bigml/demodl/mnist_test_lmdb/" 變更為 "wasb:///projects/machine_learning/image_dataset/mnist_test_lmdb"</span><span class="sxs-lookup"><span data-stu-id="875f1-184">change "file:/Users/mridul/bigml/demodl/mnist_test_lmdb/" to "wasb:///projects/machine_learning/image_dataset/mnist_test_lmdb"</span></span>

![Caffe 組態](./media/hdinsight-deep-learning-caffe-spark/Caffe-2.png)

<span data-ttu-id="875f1-186">如需有關如何定義網路的詳細資訊，請參閱 [MNIST 資料集上的 Caffe 文件](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)</span><span class="sxs-lookup"><span data-stu-id="875f1-186">For more information on how to define the network, please check the [Caffe documentation on MNIST dataset](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)</span></span>

<span data-ttu-id="875f1-187">針對此部落格的目的，只要使用這個簡單的 MNIST 範例。</span><span class="sxs-lookup"><span data-stu-id="875f1-187">For the purpose of this blog, we just use this simple MNIST example.</span></span> <span data-ttu-id="875f1-188">您應該從前端節點執行以下命令︰</span><span class="sxs-lookup"><span data-stu-id="875f1-188">You should run the command below from the head node:</span></span>

    spark-submit --master yarn --deploy-mode cluster --num-executors 8 --files ${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt,${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt --conf spark.driver.extraLibraryPath="${LD_LIBRARY_PATH}" --conf spark.executorEnv.LD_LIBRARY_PATH="${LD_LIBRARY_PATH}" --class com.yahoo.ml.caffe.CaffeOnSpark ${CAFFE_ON_SPARK}/caffe-grid/target/caffe-grid-0.1-SNAPSHOT-jar-with-dependencies.jar -train -features accuracy,loss -label label -conf lenet_memory_solver.prototxt -devices 1 -connection ethernet -model wasb:///mnist.model -output wasb:///mnist_features_result

<span data-ttu-id="875f1-189">基本上它會將所需檔案 (lenet_memory_solver.prototxt 和 lenet_memory_train_test.prototxt) 分散至每一個 YARN 容器，並也會將每個 Spark 驅動程式/執行程式的相對路徑設為 LD_LIBRARY_PATH，其定義於上述程式碼片段，並指向包含 CaffeOnSpark 程式庫的位置。</span><span class="sxs-lookup"><span data-stu-id="875f1-189">Basically it distributes the required files (lenet_memory_solver.prototxt and lenet_memory_train_test.prototxt) to each YARN container, and also set the relevant PATH of each Spark driver/executor to LD_LIBRARY_PATH, which is defined in the previous code snippet and points to the location that has CaffeOnSpark libraries.</span></span> 

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="875f1-190">監視與疑難排解</span><span class="sxs-lookup"><span data-stu-id="875f1-190">Monitoring and troubleshooting</span></span>

<span data-ttu-id="875f1-191">因為我們要使用 YARN 叢集模式，在此情況下，Spark 驅動程式會排定至任意容器 (和任意的背景工作角色節點)，在主控台輸出中應該只會看到如下︰</span><span class="sxs-lookup"><span data-stu-id="875f1-191">Since we are using YARN cluster mode, in which case the Spark driver will be scheduled to an arbitrary container (and an arbitrary worker node) you should only see in the console outputting something like:</span></span>

    17/02/01 23:22:16 INFO Client: Application report for application_1485916338528_0015 (state: RUNNING)

<span data-ttu-id="875f1-192">如果您想要知道發生了什麼事，通常需要取得 Spark 驅動程式的記錄檔，會有更多的資訊。</span><span class="sxs-lookup"><span data-stu-id="875f1-192">If you want to know what happened, you usually need to get the Spark driver's log, which has more information.</span></span> <span data-ttu-id="875f1-193">在此情況下，您需要前往 YARN UI 以尋找相關的 YARN 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="875f1-193">In this case, you need to go to the YARN UI to find the relevant YARN logs.</span></span> <span data-ttu-id="875f1-194">您可以藉由此 URL 取得 YARN UI：</span><span class="sxs-lookup"><span data-stu-id="875f1-194">You can get the YARN UI by this URL:</span></span> 

    https://yourclustername.azurehdinsight.net/yarnui
   
![YARN UI](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-1.png)

<span data-ttu-id="875f1-196">您可以看看此特定應用程式配置了多少資源。</span><span class="sxs-lookup"><span data-stu-id="875f1-196">You can take a look at how many resources are allocated for this particular application.</span></span> <span data-ttu-id="875f1-197">您可以按一下 [排程器] 連結，然後您會看到這個應用程式有 9 個執行中的容器。</span><span class="sxs-lookup"><span data-stu-id="875f1-197">You can click the "Scheduler" link, and then you will see that for this application, there are 9 containers running.</span></span> <span data-ttu-id="875f1-198">我們會要求 YARN 提供 8 個執行程式，以及另一個容器供驅動程式程序使用。</span><span class="sxs-lookup"><span data-stu-id="875f1-198">We ask YARN to provide 8 executors, and another container is for driver process.</span></span> 

![YARN 排程器](./media/hdinsight-deep-learning-caffe-spark/YARN-Scheduler.png)

<span data-ttu-id="875f1-200">如果發生失敗，您要檢查驅動程式記錄檔或容器記錄檔。</span><span class="sxs-lookup"><span data-stu-id="875f1-200">You may want to check the  driver logs or container logs if there are failures.</span></span> <span data-ttu-id="875f1-201">針對驅動程式記錄檔，您可以按一下 YARN UI 中的應用程式識別碼，然後按一下 [記錄] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="875f1-201">For driver logs, you can click the application ID in YARN UI, then click the "Logs" button.</span></span> <span data-ttu-id="875f1-202">驅動程式記錄檔會寫入 stderr。</span><span class="sxs-lookup"><span data-stu-id="875f1-202">The driver logs are written into stderr.</span></span>

![YARN UI 2](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-2.png)

<span data-ttu-id="875f1-204">例如，您可能會在下方看到一些來自驅動程式記錄檔的錯誤，表示配置太多的執行程式。</span><span class="sxs-lookup"><span data-stu-id="875f1-204">For example, you might see some of the error below from the driver logs, indicating you allocate too many executors.</span></span>

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

<span data-ttu-id="875f1-205">有時候，可能會在執行程式而不是驅動程式發生此問題。</span><span class="sxs-lookup"><span data-stu-id="875f1-205">Sometimes, the issue can happen in executors rather than drivers.</span></span> <span data-ttu-id="875f1-206">在此情況下，您需要檢查容器記錄檔。</span><span class="sxs-lookup"><span data-stu-id="875f1-206">In this case, you need to check the container logs.</span></span> <span data-ttu-id="875f1-207">您一律可以取得容器記錄檔，然後取得失敗的容器。</span><span class="sxs-lookup"><span data-stu-id="875f1-207">You can always get the container logs, and then get the failed container.</span></span> <span data-ttu-id="875f1-208">例如，您在執行 Caffe 時可能會遇到此失敗。</span><span class="sxs-lookup"><span data-stu-id="875f1-208">For example, you might meet this failure when running Caffe.</span></span>

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

<span data-ttu-id="875f1-209">在此情況下，您需要取得失敗的容器識別碼 (在上述案例中，它是 container_1485916338528_0008_05_000005)。</span><span class="sxs-lookup"><span data-stu-id="875f1-209">In this case, you need to get the failed container ID (in the above case, it is container_1485916338528_0008_05_000005).</span></span> <span data-ttu-id="875f1-210">然後您需要執行</span><span class="sxs-lookup"><span data-stu-id="875f1-210">Then you need to run</span></span> 

    yarn logs -containerId container_1485916338528_0008_03_000005

<span data-ttu-id="875f1-211">自前端節點。</span><span class="sxs-lookup"><span data-stu-id="875f1-211">from the headnode.</span></span> <span data-ttu-id="875f1-212">在檢查容器失敗之後，它是由使用 lenet_memory_solver.prototxt 中的 GPU 模式 (您應該改用 CPU 模式) 所引起。</span><span class="sxs-lookup"><span data-stu-id="875f1-212">After checking container failure, it is caused by using GPU mode (where you should use CPU mode instead) in lenet_memory_solver.prototxt.</span></span>

    17/02/01 07:10:48 INFO LMDB: Batch size:100
    WARNING: Logging before InitGoogleLogging() is written to STDERR
    F0201 07:10:48.309725 11624 common.cpp:79] Cannot use GPU in CPU-only Caffe: check mode.


## <a name="getting-results"></a><span data-ttu-id="875f1-213">取得結果</span><span class="sxs-lookup"><span data-stu-id="875f1-213">Getting results</span></span>

<span data-ttu-id="875f1-214">因為我們會配置 8 個執行程式，且網路拓撲很簡單，應該只需花費大約 30 分鐘的時間執行結果。</span><span class="sxs-lookup"><span data-stu-id="875f1-214">Since we are allocating 8 executors, and the network topology is simple, it should only take around 30 minutes to run the result.</span></span> <span data-ttu-id="875f1-215">從命令列中，您可以看到我們將此模型放到 wasb:///mnist.model，並將結果放到名為 wasb:///mnist_features_result 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="875f1-215">From the command line, you can see that we put the model to wasb:///mnist.model, and put the results to a folder named wasb:///mnist_features_result.</span></span>

<span data-ttu-id="875f1-216">您可以取得結果，方法為執行</span><span class="sxs-lookup"><span data-stu-id="875f1-216">You can get the results by running</span></span>

    hadoop fs -cat hdfs:///mnist_features_result/*

<span data-ttu-id="875f1-217">結果如下：</span><span class="sxs-lookup"><span data-stu-id="875f1-217">and the result looks like:</span></span>

    {"SampleID":"00009597","accuracy":[1.0],"loss":[0.028171852],"label":[2.0]}
    {"SampleID":"00009598","accuracy":[1.0],"loss":[0.028171852],"label":[6.0]}
    {"SampleID":"00009599","accuracy":[1.0],"loss":[0.028171852],"label":[1.0]}
    {"SampleID":"00009600","accuracy":[0.97],"loss":[0.0677709],"label":[5.0]}
    {"SampleID":"00009601","accuracy":[0.97],"loss":[0.0677709],"label":[0.0]}
    {"SampleID":"00009602","accuracy":[0.97],"loss":[0.0677709],"label":[1.0]}
    {"SampleID":"00009603","accuracy":[0.97],"loss":[0.0677709],"label":[2.0]}
    {"SampleID":"00009604","accuracy":[0.97],"loss":[0.0677709],"label":[3.0]}
    {"SampleID":"00009605","accuracy":[0.97],"loss":[0.0677709],"label":[4.0]}

<span data-ttu-id="875f1-218">SampleID 代表 MNIST 資料集的識別碼，且標籤是此模型識別的數字。</span><span class="sxs-lookup"><span data-stu-id="875f1-218">The SampleID represents the ID in the MNIST dataset, and the label is the number that the model identifies.</span></span>


## <a name="conclusion"></a><span data-ttu-id="875f1-219">結論</span><span class="sxs-lookup"><span data-stu-id="875f1-219">Conclusion</span></span>

<span data-ttu-id="875f1-220">在本文件中，您已嘗試執行簡單的範例來安裝 CaffeOnSpark。</span><span class="sxs-lookup"><span data-stu-id="875f1-220">In this documentation, you have tried to install CaffeOnSpark with running a simple example.</span></span> <span data-ttu-id="875f1-221">HDInsight 是完全受管理的雲端分散式計算平台，並且是在大型資料集上執行機器學習和進階分析工作負載的最佳位置，而針對分散式深入學習，您可以使用 Caffe on HDInsight Spark 來執行深入學習工作。</span><span class="sxs-lookup"><span data-stu-id="875f1-221">HDInsight is a full managed cloud distributed compute platform, and is the best place for running machine learning and advanced analytics workloads on large data set, and for distributed deep learning, you can use Caffe on HDInsight Spark to perform deep learning tasks.</span></span>


## <span data-ttu-id="875f1-222"><a name="seealso"></a>另請參閱</span><span class="sxs-lookup"><span data-stu-id="875f1-222"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="875f1-223">概觀：Azure HDInsight 上的 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="875f1-223">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="875f1-224">案例</span><span class="sxs-lookup"><span data-stu-id="875f1-224">Scenarios</span></span>
* [<span data-ttu-id="875f1-225">Spark 和機器學習：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度</span><span class="sxs-lookup"><span data-stu-id="875f1-225">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="875f1-226">Spark 和機器學習：使用 HDInsight 中的 Spark 來預測食物檢查結果</span><span class="sxs-lookup"><span data-stu-id="875f1-226">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

### <a name="manage-resources"></a><span data-ttu-id="875f1-227">管理資源</span><span class="sxs-lookup"><span data-stu-id="875f1-227">Manage resources</span></span>
* [<span data-ttu-id="875f1-228">在 Azure HDInsight 中管理 Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="875f1-228">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

