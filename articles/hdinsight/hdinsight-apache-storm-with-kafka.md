---
title: "aaaUse Storm HDInsight 的 Azure 上使用 Apache Kafka |Microsoft 文件"
description: "Apache Kafka 會隨著 Apache Storm on HDInsight 一起安裝。 了解 toowrite tooKafka，並使用它，然後讀取 hello KafkaBolt 和 KafkaSpout Storm 所提供的元件。 也了解如何 toouse hello 變動 framework toodefine 和提交 Storm 拓撲。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e4941329-1580-4cd8-b82e-a2258802c1a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2017
ms.author: larryfr
ms.openlocfilehash: 95701f51dfdf6f1a859dcde96d7053df4f21701f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-kafka-preview-with-storm-on-hdinsight"></a><span data-ttu-id="a88ea-105">使用 Apache Kafka (預覽) 搭配 Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="a88ea-105">Use Apache Kafka (preview) with Storm on HDInsight</span></span>

<span data-ttu-id="a88ea-106">深入了解如何從 toouse Apache Storm tooread 和寫入 tooApache Kafka。</span><span class="sxs-lookup"><span data-stu-id="a88ea-106">Learn how toouse Apache Storm tooread from and write tooApache Kafka.</span></span> <span data-ttu-id="a88ea-107">此範例也示範如何從 HDFS 相容性 Storm 拓撲 toohello toosave 資料檔案使用 HDInsight 的系統。</span><span class="sxs-lookup"><span data-stu-id="a88ea-107">This example also demonstrates how toosave data from a Storm topology toohello HDFS-compatible file system used by HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="a88ea-108">本文件中的 hello 步驟建立包含在 HDInsight 上的 Storm 以及 Kafka HDInsight 叢集上的 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="a88ea-108">hello steps in this document create an Azure resource group that contains both a Storm on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="a88ea-109">這些叢集會同時位於 Azure 虛擬網路，可讓 hello Storm 叢集 toodirectly 與 hello Kafka 叢集通訊。</span><span class="sxs-lookup"><span data-stu-id="a88ea-109">These clusters are both located within an Azure Virtual Network, which allows hello Storm cluster toodirectly communicate with hello Kafka cluster.</span></span>
> 
> <span data-ttu-id="a88ea-110">當您完成這份文件中的 hello 步驟之後時，請記得 toodelete hello 叢集 tooavoid 過多費用。</span><span class="sxs-lookup"><span data-stu-id="a88ea-110">When you are done with hello steps in this document, remember toodelete hello clusters tooavoid excess charges.</span></span>

## <a name="get-hello-code"></a><span data-ttu-id="a88ea-111">取得 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="a88ea-111">Get hello code</span></span>

<span data-ttu-id="a88ea-112">使用這份文件中的 hello 範例的 hello 程式碼將會位於[https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka)。</span><span class="sxs-lookup"><span data-stu-id="a88ea-112">hello code for hello example used in this document is available at [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span></span>

<span data-ttu-id="a88ea-113">toocompile 此專案中，您需要下列組態的開發環境的 hello:</span><span class="sxs-lookup"><span data-stu-id="a88ea-113">toocompile this project, you need hello following configuration for your development environment:</span></span>

* <span data-ttu-id="a88ea-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="a88ea-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="a88ea-115">HDInsight 3.5 或更新版本需要 Java 8。</span><span class="sxs-lookup"><span data-stu-id="a88ea-115">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="a88ea-116">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="a88ea-116">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

* <span data-ttu-id="a88ea-117">將 SSH 用戶端 (您需要 hello`ssh`和`scp`命令)-如需資訊，請參閱[搭配使用 SSH 和 HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="a88ea-117">An SSH client (you need hello `ssh` and `scp` commands) - For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="a88ea-118">文字編輯器或整合式開發環境 (IDE)。</span><span class="sxs-lookup"><span data-stu-id="a88ea-118">A text editor or IDE.</span></span>

<span data-ttu-id="a88ea-119">hello 下列環境變數設定當您在開發工作站上安裝 Java 和 hello JDK。</span><span class="sxs-lookup"><span data-stu-id="a88ea-119">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="a88ea-120">不過，您應該檢查其存在且包含您系統的 hello 正確值。</span><span class="sxs-lookup"><span data-stu-id="a88ea-120">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="a88ea-121">`JAVA_HOME`-應該指向 toohello hello JDK 安裝的目錄。</span><span class="sxs-lookup"><span data-stu-id="a88ea-121">`JAVA_HOME` - should point toohello directory where hello JDK is installed.</span></span>
* <span data-ttu-id="a88ea-122">`PATH`-應包含下列路徑的 hello:</span><span class="sxs-lookup"><span data-stu-id="a88ea-122">`PATH` - should contain hello following paths:</span></span>
  
    * <span data-ttu-id="a88ea-123">`JAVA_HOME`（或 hello 等路徑）。</span><span class="sxs-lookup"><span data-stu-id="a88ea-123">`JAVA_HOME` (or hello equivalent path).</span></span>
    * <span data-ttu-id="a88ea-124">`JAVA_HOME\bin`（或 hello 等路徑）。</span><span class="sxs-lookup"><span data-stu-id="a88ea-124">`JAVA_HOME\bin` (or hello equivalent path).</span></span>
    * <span data-ttu-id="a88ea-125">hello Maven 安裝所在的目錄。</span><span class="sxs-lookup"><span data-stu-id="a88ea-125">hello directory where Maven is installed.</span></span>

## <a name="create-hello-clusters"></a><span data-ttu-id="a88ea-126">建立 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="a88ea-126">Create hello clusters</span></span>

<span data-ttu-id="a88ea-127">Apache Kafka HDInsight 上不提供存取 toohello Kafka broker 透過 hello 公用網際網路。</span><span class="sxs-lookup"><span data-stu-id="a88ea-127">Apache Kafka on HDInsight does not provide access toohello Kafka brokers over hello public internet.</span></span> <span data-ttu-id="a88ea-128">討論 tooKafka 必須在 hello 與 hello 節點中的相同 Azure 虛擬網路的任何項目 hello Kafka 叢集。</span><span class="sxs-lookup"><span data-stu-id="a88ea-128">Anything that talks tooKafka must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="a88ea-129">例如，hello Kafka 與 Storm 叢集位於 Azure 的虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="a88ea-129">For this example, both hello Kafka and Storm clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="a88ea-130">hello 下圖顯示 hello 叢集之間通訊流動的方式：</span><span class="sxs-lookup"><span data-stu-id="a88ea-130">hello following diagram shows how communication flows between hello clusters:</span></span>

![Azure 虛擬網路中的 Storm 和 Kafka 叢集圖表](./media/hdinsight-apache-storm-with-kafka/storm-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="a88ea-132">例如，可以透過存取 SSH 和 Ambari hello 網際網路，hello 叢集上的其他服務。</span><span class="sxs-lookup"><span data-stu-id="a88ea-132">Other services on hello cluster such as SSH and Ambari can be accessed over hello internet.</span></span> <span data-ttu-id="a88ea-133">Hello 公用連接埠適用於 HDInsight 上的詳細資訊，請參閱[連接埠和 Uri 使用 HDInsight](hdinsight-hadoop-port-settings-for-services.md)。</span><span class="sxs-lookup"><span data-stu-id="a88ea-133">For more information on hello public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="a88ea-134">雖然您可以建立 Azure 虛擬網路，Kafka，和 Storm 叢集以手動方式，很容易 toouse Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="a88ea-134">While you can create an Azure virtual network, Kafka, and Storm clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="a88ea-135">使用 hello 下列步驟 toodeploy Azure 虛擬網路，Kafka，，和 Storm 叢集 tooyour Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a88ea-135">Use hello following steps toodeploy an Azure virtual network, Kafka, and Storm clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="a88ea-136">使用下列按鈕 toosign 中 tooAzure 和開啟 hello 範本 hello Azure 入口網站中的 hello。</span><span class="sxs-lookup"><span data-stu-id="a88ea-136">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-storm-cluster-in-vnet-v2.json" target="_blank"><img src="./media/hdinsight-apache-storm-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    <span data-ttu-id="a88ea-137">hello Azure Resource Manager 範本位於**https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**。</span><span class="sxs-lookup"><span data-stu-id="a88ea-137">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**.</span></span> <span data-ttu-id="a88ea-138">它會建立 hello 下列資源：</span><span class="sxs-lookup"><span data-stu-id="a88ea-138">It creates hello following resources:</span></span>
    
    * <span data-ttu-id="a88ea-139">Azure 資源群組</span><span class="sxs-lookup"><span data-stu-id="a88ea-139">Azure resource group</span></span>
    * <span data-ttu-id="a88ea-140">Azure 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="a88ea-140">Azure Virtual Network</span></span>
    * <span data-ttu-id="a88ea-141">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="a88ea-141">Azure Storage account</span></span>
    * <span data-ttu-id="a88ea-142">HDInsight 版本 3.6 上的 Kafka (三個背景工作角色節點)</span><span class="sxs-lookup"><span data-stu-id="a88ea-142">Kafka on HDInsight version 3.6 (three worker nodes)</span></span>
    * <span data-ttu-id="a88ea-143">HDInsight 版本 3.6 上的 Storm (三個背景工作角色節點)</span><span class="sxs-lookup"><span data-stu-id="a88ea-143">Storm on HDInsight version 3.6 (three worker nodes)</span></span>

  > [!WARNING]
  > <span data-ttu-id="a88ea-144">HDInsight 上 Kafka tooguarantee 可用性，您的叢集必須包含至少三個背景工作節點。</span><span class="sxs-lookup"><span data-stu-id="a88ea-144">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="a88ea-145">此範本會建立包含三個背景工作角色節點的 Kafka 叢集。</span><span class="sxs-lookup"><span data-stu-id="a88ea-145">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="a88ea-146">使用下列指引 toopopulate hello 項目上 hello 的 hello**自訂部署**刀鋒視窗中：</span><span class="sxs-lookup"><span data-stu-id="a88ea-146">Use hello following guidance toopopulate hello entries on hello **Custom deployment** blade:</span></span>
   
    ![HDInsight 自訂部署](./media/hdinsight-apache-storm-with-kafka/parameters.png)

    * <span data-ttu-id="a88ea-148">**資源群組**：建立群組或選取現有的群組。</span><span class="sxs-lookup"><span data-stu-id="a88ea-148">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="a88ea-149">此群組包含 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="a88ea-149">This group contains hello HDInsight cluster.</span></span>
   
    * <span data-ttu-id="a88ea-150">**位置**： 選取位置的地理位置關閉 tooyou。</span><span class="sxs-lookup"><span data-stu-id="a88ea-150">**Location**: Select a location geographically close tooyou.</span></span>

    * <span data-ttu-id="a88ea-151">**基底叢集名稱**: hello Storm 和 Kafka 叢集 hello 基底名稱為使用此值。</span><span class="sxs-lookup"><span data-stu-id="a88ea-151">**Base Cluster Name**: This value is used as hello base name for hello Storm and Kafka clusters.</span></span> <span data-ttu-id="a88ea-152">例如，輸入 **hdi** 可建立名為 **storm-hdi** 的 Storm 叢集以及名為 **kafka-hdi** 的 Kafka 叢集。</span><span class="sxs-lookup"><span data-stu-id="a88ea-152">For example, entering **hdi** creates a Storm cluster named **storm-hdi** and a Kafka cluster named **kafka-hdi**.</span></span>
   
    * <span data-ttu-id="a88ea-153">**叢集登入使用者名稱**: hello Storm 和 Kafka 叢集 hello 系統管理員使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="a88ea-153">**Cluster Login User Name**: hello admin user name for hello Storm and Kafka clusters.</span></span>
   
    * <span data-ttu-id="a88ea-154">**叢集登入密碼**: hello Storm 和 Kafka 叢集 hello 管理使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="a88ea-154">**Cluster Login Password**: hello admin user password for hello Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="a88ea-155">**SSH 使用者名稱**: hello SSH 使用者 toocreate hello Storm 和 Kafka 叢集。</span><span class="sxs-lookup"><span data-stu-id="a88ea-155">**SSH User Name**: hello SSH user toocreate for hello Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="a88ea-156">**SSH 密碼**: hello hello Storm 和 Kafka 叢集的 hello SSH 使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="a88ea-156">**SSH Password**: hello password for hello SSH user for hello Storm and Kafka clusters.</span></span>

3. <span data-ttu-id="a88ea-157">讀取 hello**條款和條件**，然後選取**toohello 條款和條件前面所述，即表示我同意**。</span><span class="sxs-lookup"><span data-stu-id="a88ea-157">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="a88ea-158">最後，檢查**Pin toodashboard** ，然後選取 **購買**。</span><span class="sxs-lookup"><span data-stu-id="a88ea-158">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="a88ea-159">它會採用約 20 分鐘 toocreate hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="a88ea-159">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="a88ea-160">一旦已建立 hello 資源，會顯示 hello 資源群組的 hello 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a88ea-160">Once hello resources have been created, hello blade for hello resource group is displayed.</span></span>

![Hello vnet 與叢集資源群組 刀鋒視窗](./media/hdinsight-apache-storm-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="a88ea-162">請注意，hello hello HDInsight 叢集名稱**storm BASENAME**和**kafka BASENAME**，其中 BASENAME 是 hello 提供 toohello 範本的名稱。</span><span class="sxs-lookup"><span data-stu-id="a88ea-162">Notice that hello names of hello HDInsight clusters are **storm-BASENAME** and **kafka-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="a88ea-163">連接 toohello 叢集時，您可以使用在稍後步驟中的這些名稱。</span><span class="sxs-lookup"><span data-stu-id="a88ea-163">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="understanding-hello-code"></a><span data-ttu-id="a88ea-164">了解 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="a88ea-164">Understanding hello code</span></span>

<span data-ttu-id="a88ea-165">此專案包含兩種拓撲︰</span><span class="sxs-lookup"><span data-stu-id="a88ea-165">This project contains two topologies:</span></span>

* <span data-ttu-id="a88ea-166">**KafkaWriter**: hello 所定義**writer.yaml**檔案，此拓撲寫入使用 hello KafkaBolt 隨附 Apache Storm 的隨機句子 tooKafka。</span><span class="sxs-lookup"><span data-stu-id="a88ea-166">**KafkaWriter**: Defined by hello **writer.yaml** file, this topology writes random sentences tooKafka using hello KafkaBolt provided with Apache Storm.</span></span>

    <span data-ttu-id="a88ea-167">此拓撲會使用自訂**SentenceSpout**元件 toogenerate 隨機句子。</span><span class="sxs-lookup"><span data-stu-id="a88ea-167">This topology uses a custom **SentenceSpout** component toogenerate random sentences.</span></span>

* <span data-ttu-id="a88ea-168">**KafkaReader**: hello 所定義**reader.yaml**檔案，此拓撲，讀取 Kafka 使用 hello KafkaSpout 隨附 Apache Storm 則記錄檔 hello 資料 toostdout。</span><span class="sxs-lookup"><span data-stu-id="a88ea-168">**KafkaReader**: Defined by hello **reader.yaml** file, this topology reads data from Kafka using hello KafkaSpout provided with Apache Storm, then logs hello data toostdout.</span></span>

    <span data-ttu-id="a88ea-169">此拓撲會使用 hello Storm HdfsBolt toowrite 資料 toodefault 儲存 hello Storm 叢集。</span><span class="sxs-lookup"><span data-stu-id="a88ea-169">This topology uses hello Storm HdfsBolt toowrite data toodefault storage for hello Storm cluster.</span></span>
### <a name="flux"></a><span data-ttu-id="a88ea-170">Flux</span><span class="sxs-lookup"><span data-stu-id="a88ea-170">Flux</span></span>

<span data-ttu-id="a88ea-171">使用定義 hello 拓撲[變動](https://storm.apache.org/releases/1.1.0/flux.html)。</span><span class="sxs-lookup"><span data-stu-id="a88ea-171">hello topologies are defined using [Flux](https://storm.apache.org/releases/1.1.0/flux.html).</span></span> <span data-ttu-id="a88ea-172">中導入變動 Storm 0.10.x，並讓您從 hello 碼 tooseparate hello 拓撲組態。</span><span class="sxs-lookup"><span data-stu-id="a88ea-172">Flux was introduced in Storm 0.10.x and allows you tooseparate hello topology configuration from hello code.</span></span> <span data-ttu-id="a88ea-173">如需使用 hello 變動架構的拓撲，hello 拓撲 YAML 檔案中定義。</span><span class="sxs-lookup"><span data-stu-id="a88ea-173">For Topologies that use hello Flux framework, hello topology is defined in a YAML file.</span></span> <span data-ttu-id="a88ea-174">hello YAML 檔案可以是 hello 拓撲的一部分。</span><span class="sxs-lookup"><span data-stu-id="a88ea-174">hello YAML file can be included as part of hello topology.</span></span> <span data-ttu-id="a88ea-175">它也可以使用當您送出 hello 拓撲的獨立檔案。</span><span class="sxs-lookup"><span data-stu-id="a88ea-175">It can also be a standalone file used when you submit hello topology.</span></span> <span data-ttu-id="a88ea-176">Flux 也支援執行階段的變數替代 (在此範例中使用)。</span><span class="sxs-lookup"><span data-stu-id="a88ea-176">Flux also supports variable substitution at run-time, which is used in this example.</span></span>

<span data-ttu-id="a88ea-177">hello 設定下列參數是在執行階段針對這些拓撲：</span><span class="sxs-lookup"><span data-stu-id="a88ea-177">hello following parameters are set at run time for these topologies:</span></span>

* <span data-ttu-id="a88ea-178">`${kafka.topic}`: hello hello Kafka 主題 hello 拓撲讀名稱。</span><span class="sxs-lookup"><span data-stu-id="a88ea-178">`${kafka.topic}`: hello name of hello Kafka topic that hello topologies read/write to.</span></span>

* <span data-ttu-id="a88ea-179">`${kafka.broker.hosts}`: hello 裝載該 hello Kafka 居間處理上執行。</span><span class="sxs-lookup"><span data-stu-id="a88ea-179">`${kafka.broker.hosts}`: hello hosts that hello Kafka brokers run on.</span></span> <span data-ttu-id="a88ea-180">hello KafkaBolt 撰寫 tooKafka 時，會使用 hello broker 資訊。</span><span class="sxs-lookup"><span data-stu-id="a88ea-180">hello broker information is used by hello KafkaBolt when writing tooKafka.</span></span>

* <span data-ttu-id="a88ea-181">`${kafka.zookeeper.hosts}`： 動物園管理員在執行中的 hello 主機 hello Kafka 叢集。</span><span class="sxs-lookup"><span data-stu-id="a88ea-181">`${kafka.zookeeper.hosts}`: hello hosts that Zookeeper runs on in hello Kafka cluster.</span></span>

<span data-ttu-id="a88ea-182">如需 Flux 拓撲的詳細資訊，請參閱 [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html)。</span><span class="sxs-lookup"><span data-stu-id="a88ea-182">For more information on Flux topologies, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="download-and-compile-hello-project"></a><span data-ttu-id="a88ea-183">下載並編譯 hello 專案</span><span class="sxs-lookup"><span data-stu-id="a88ea-183">Download and compile hello project</span></span>

1. <span data-ttu-id="a88ea-184">在開發環境中，下載 hello 專案從[https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka)，開啟 命令列，並變更您已經下載 hello 專案目錄 toohello 位置。</span><span class="sxs-lookup"><span data-stu-id="a88ea-184">On your development environment, download hello project from [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), open a command-line, and change directories toohello location that you downloaded hello project.</span></span>

2. <span data-ttu-id="a88ea-185">從 hello **hdinsight storm-java kafka**目錄下，使用 hello 下列命令 toocompile hello 專案，並建立部署的套件：</span><span class="sxs-lookup"><span data-stu-id="a88ea-185">From hello **hdinsight-storm-java-kafka** directory, use hello following command toocompile hello project and create a package for deployment:</span></span>

  ```bash
  mvn clean package
  ```

    <span data-ttu-id="a88ea-186">hello 封裝程序會建立名為`KafkaTopology-1.0-SNAPSHOT.jar`在 hello`target`目錄。</span><span class="sxs-lookup"><span data-stu-id="a88ea-186">hello package process creates a file named `KafkaTopology-1.0-SNAPSHOT.jar` in hello `target` directory.</span></span>

3. <span data-ttu-id="a88ea-187">使用下列命令 toocopy hello 封裝 tooyour Storm HDInsight 叢集上的 hello。</span><span class="sxs-lookup"><span data-stu-id="a88ea-187">Use hello following commands toocopy hello package tooyour Storm on HDInsight cluster.</span></span> <span data-ttu-id="a88ea-188">取代**USERNAME** hello 叢集 hello SSH 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="a88ea-188">Replace **USERNAME** with hello SSH user name for hello cluster.</span></span> <span data-ttu-id="a88ea-189">取代**BASENAME** hello 基底名稱與您在建立時使用 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="a88ea-189">Replace **BASENAME** with hello base name you used when creating hello cluster.</span></span>

  ```bash
  scp ./target/KafkaTopology-1.0-SNAPSHOT.jar USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
  ```

    <span data-ttu-id="a88ea-190">出現提示時，輸入 hello 建立 hello 叢集時所使用的密碼。</span><span class="sxs-lookup"><span data-stu-id="a88ea-190">When prompted, enter hello password you used when creating hello clusters.</span></span>

## <a name="configure-hello-topology"></a><span data-ttu-id="a88ea-191">設定 hello 拓撲</span><span class="sxs-lookup"><span data-stu-id="a88ea-191">Configure hello topology</span></span>

1. <span data-ttu-id="a88ea-192">使用其中一種下列方法 toodiscover hello hello Kafka broker 主機：</span><span class="sxs-lookup"><span data-stu-id="a88ea-192">Use one of hello following methods toodiscover hello Kafka broker hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $brokerHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($brokerHosts -join ":9092,") + ":9092"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="a88ea-193">hello Bash 範例假設`$CLUSTERNAME`包含 hello hello HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="a88ea-193">hello Bash example assumes that `$CLUSTERNAME` contains hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="a88ea-194">它也假設已安裝 [jq](https://stedolan.github.io/jq/)。</span><span class="sxs-lookup"><span data-stu-id="a88ea-194">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="a88ea-195">出現提示時，輸入 hello 密碼 hello 叢集登入帳戶。</span><span class="sxs-lookup"><span data-stu-id="a88ea-195">When prompted, enter hello password for hello cluster login account.</span></span>

    <span data-ttu-id="a88ea-196">傳回的 hello 值是類似 toohello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="a88ea-196">hello value returned is similar toohello following text:</span></span>

        wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092

    > [!IMPORTANT]
    > <span data-ttu-id="a88ea-197">雖然可能會有兩個以上的 broker 主機叢集，您不需要 tooprovide 所有主機 tooclients 的完整清單。</span><span class="sxs-lookup"><span data-stu-id="a88ea-197">While there may be more than two broker hosts for your cluster, you do not need tooprovide a full list of all hosts tooclients.</span></span> <span data-ttu-id="a88ea-198">列出一兩個主機便已足夠。</span><span class="sxs-lookup"><span data-stu-id="a88ea-198">One or two is enough.</span></span>

2. <span data-ttu-id="a88ea-199">使用下列方法 toodiscover hello Kafka 動物園管理員主機 hello 的其中一個：</span><span class="sxs-lookup"><span data-stu-id="a88ea-199">Use one of hello following methods toodiscover hello Kafka Zookeeper hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $zookeeperHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($zookeeperHosts -join ":2181,") + ":2181"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="a88ea-200">hello Bash 範例假設`$CLUSTERNAME`包含 hello hello HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="a88ea-200">hello Bash example assumes that `$CLUSTERNAME` contains hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="a88ea-201">它也假設已安裝 [jq](https://stedolan.github.io/jq/)。</span><span class="sxs-lookup"><span data-stu-id="a88ea-201">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="a88ea-202">出現提示時，輸入 hello 密碼 hello 叢集登入帳戶。</span><span class="sxs-lookup"><span data-stu-id="a88ea-202">When prompted, enter hello password for hello cluster login account.</span></span>

    <span data-ttu-id="a88ea-203">傳回的 hello 值是類似 toohello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="a88ea-203">hello value returned is similar toohello following text:</span></span>

        zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181

    > [!IMPORTANT]
    > <span data-ttu-id="a88ea-204">兩個以上的動物園管理員節點時，您不需要 tooprovide 所有主機 tooclients 的完整清單。</span><span class="sxs-lookup"><span data-stu-id="a88ea-204">While there are more than two Zookeeper nodes, you do not need tooprovide a full list of all hosts tooclients.</span></span> <span data-ttu-id="a88ea-205">列出一兩個主機便已足夠。</span><span class="sxs-lookup"><span data-stu-id="a88ea-205">One or two is enough.</span></span>

    <span data-ttu-id="a88ea-206">儲存這個值以便稍後使用。</span><span class="sxs-lookup"><span data-stu-id="a88ea-206">Save this value, as it is used later.</span></span>

3. <span data-ttu-id="a88ea-207">編輯 hello `dev.properties` hello hello 專案根目錄中的檔案。</span><span class="sxs-lookup"><span data-stu-id="a88ea-207">Edit hello `dev.properties` file in hello root of hello project.</span></span> <span data-ttu-id="a88ea-208">此檔案中加入 hello Broker 和動物園管理員主機資訊 toohello 相符的行。</span><span class="sxs-lookup"><span data-stu-id="a88ea-208">Add hello Broker and Zookeeper hosts information toohello matching lines in this file.</span></span> <span data-ttu-id="a88ea-209">hello 下列範例會使用設定 hello 先前步驟中的 hello 範例值：</span><span class="sxs-lookup"><span data-stu-id="a88ea-209">hello following example is configured using hello sample values from hello previous steps:</span></span>

        kafka.zookeeper.hosts: zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181
        kafka.broker.hosts: wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092
        kafka.topic: stormtopic

4. <span data-ttu-id="a88ea-210">儲存 hello`dev.properties`檔案，然後使用 hello 下列命令 tooupload 它 toohello Storm 叢集：</span><span class="sxs-lookup"><span data-stu-id="a88ea-210">Save hello `dev.properties` file and then use hello following command tooupload it toohello Storm cluster:</span></span>

     ```bash
    scp dev.properties USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
    ```

    <span data-ttu-id="a88ea-211">取代**USERNAME** hello 叢集 hello SSH 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="a88ea-211">Replace **USERNAME** with hello SSH user name for hello cluster.</span></span> <span data-ttu-id="a88ea-212">取代**BASENAME** hello 基底名稱與您在建立時使用 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="a88ea-212">Replace **BASENAME** with hello base name you used when creating hello cluster.</span></span>

## <a name="start-hello-writer"></a><span data-ttu-id="a88ea-213">啟動 hello 寫入器</span><span class="sxs-lookup"><span data-stu-id="a88ea-213">Start hello writer</span></span>

1. <span data-ttu-id="a88ea-214">使用 hello 遵循使用 SSH tooconnect toohello Storm 叢集。</span><span class="sxs-lookup"><span data-stu-id="a88ea-214">Use hello following tooconnect toohello Storm cluster using SSH.</span></span> <span data-ttu-id="a88ea-215">取代**USERNAME** hello 建立 hello 叢集時所使用的 SSH 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="a88ea-215">Replace **USERNAME** with hello SSH user name used when creating hello cluster.</span></span> <span data-ttu-id="a88ea-216">取代**BASENAME** hello 建立 hello 叢集時所使用的基底名稱。</span><span class="sxs-lookup"><span data-stu-id="a88ea-216">Replace **BASENAME** with hello base name used when creating hello cluster.</span></span>

  ```bash
  ssh USERNAME@storm-BASENAME-ssh.azurehdinsight.net
  ```

    <span data-ttu-id="a88ea-217">出現提示時，輸入 hello 建立 hello 叢集時所使用的密碼。</span><span class="sxs-lookup"><span data-stu-id="a88ea-217">When prompted, enter hello password you used when creating hello clusters.</span></span>
   
    <span data-ttu-id="a88ea-218">如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="a88ea-218">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="a88ea-219">從 hello SSH 連線，使用下列命令 toocreate hello Kafka 主題 hello 拓撲所使用的 hello:</span><span class="sxs-lookup"><span data-stu-id="a88ea-219">From hello SSH connection, use hello following command toocreate hello Kafka topic used by hello topology:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic stormtopic --zookeeper $KAFKAZKHOSTS
    ```

    <span data-ttu-id="a88ea-220">取代`$KAFKAZKHOSTS`hello 動物園管理員與裝載您擷取 hello 前一節中的資訊。</span><span class="sxs-lookup"><span data-stu-id="a88ea-220">Replace `$KAFKAZKHOSTS` with hello Zookeeper host information you retrieved in hello previous section.</span></span>

2. <span data-ttu-id="a88ea-221">從 hello SSH 連線 toohello Storm 叢集，使用下列命令 toostart hello 寫入器拓撲 hello:</span><span class="sxs-lookup"><span data-stu-id="a88ea-221">From hello SSH connection toohello Storm cluster, use hello following command toostart hello writer topology:</span></span>

    ```bash
    storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
    ```

    <span data-ttu-id="a88ea-222">此命令搭配使用的 hello 參數如下：</span><span class="sxs-lookup"><span data-stu-id="a88ea-222">hello parameters used with this command are:</span></span>

    * <span data-ttu-id="a88ea-223">`org.apache.storm.flux.Flux`： 使用變動 tooconfigure，並執行此拓撲。</span><span class="sxs-lookup"><span data-stu-id="a88ea-223">`org.apache.storm.flux.Flux`: Use Flux tooconfigure and run this topology.</span></span>

    * <span data-ttu-id="a88ea-224">`--remote`： 送出 hello 拓撲 tooNimbus。</span><span class="sxs-lookup"><span data-stu-id="a88ea-224">`--remote`: Submit hello topology tooNimbus.</span></span> <span data-ttu-id="a88ea-225">hello 拓撲會分佈在 hello hello 叢集中的背景工作節點。</span><span class="sxs-lookup"><span data-stu-id="a88ea-225">hello topology is distributed across hello worker nodes in hello cluster.</span></span>

    * <span data-ttu-id="a88ea-226">`-R /writer.yaml`： 使用 hello`writer.yaml`檔案 tooconfigure hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="a88ea-226">`-R /writer.yaml`: Use hello `writer.yaml` file tooconfigure hello topology.</span></span> <span data-ttu-id="a88ea-227">`-R`表示此資源包含在 hello jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="a88ea-227">`-R` indicates that this resource is included in hello jar file.</span></span> <span data-ttu-id="a88ea-228">它是在 hello jar hello 根目錄中因此`/writer.yaml`是 hello 路徑 tooit。</span><span class="sxs-lookup"><span data-stu-id="a88ea-228">It's in hello root of hello jar, so `/writer.yaml` is hello path tooit.</span></span>

    * <span data-ttu-id="a88ea-229">`--filter`: Hello 中的項目填入`writer.yaml`使用 hello 中值的拓樸`dev.properties`檔案。</span><span class="sxs-lookup"><span data-stu-id="a88ea-229">`--filter`: Populate entries in hello `writer.yaml` topology using values in hello `dev.properties` file.</span></span> <span data-ttu-id="a88ea-230">例如，hello hello 值`kafka.topic`hello 檔案中的項目是使用的 tooreplace hello `${kafka.topic}` hello 拓撲定義項目。</span><span class="sxs-lookup"><span data-stu-id="a88ea-230">For example, hello value of hello `kafka.topic` entry in hello file is used tooreplace hello `${kafka.topic}` entry in hello topology definition.</span></span>

5. <span data-ttu-id="a88ea-231">Hello 拓撲啟動之後，使用下列命令 tooverify 其正寫入資料 toohello Kafka 主題 hello:</span><span class="sxs-lookup"><span data-stu-id="a88ea-231">Once hello topology has started, use hello following command tooverify that it is writing data toohello Kafka topic:</span></span>

  ```bash
  /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $KAFKAZKHOSTS --from-beginning --topic stormtopic
  ```

    <span data-ttu-id="a88ea-232">取代`$KAFKAZKHOSTS`hello 動物園管理員與裝載您擷取 hello 前一節中的資訊。</span><span class="sxs-lookup"><span data-stu-id="a88ea-232">Replace `$KAFKAZKHOSTS` with hello Zookeeper host information you retrieved in hello previous section.</span></span>

    <span data-ttu-id="a88ea-233">此命令會使用隨附於 Kafka toomonitor hello 主題的指令碼。</span><span class="sxs-lookup"><span data-stu-id="a88ea-233">This command uses a script shipped with Kafka toomonitor hello topic.</span></span> <span data-ttu-id="a88ea-234">隨後，它應該開始傳回隨機句子已寫入 toohello 主題。</span><span class="sxs-lookup"><span data-stu-id="a88ea-234">After a moment, it should start returning random sentences that have been written toohello topic.</span></span> <span data-ttu-id="a88ea-235">hello 輸出是 toohello 類似下列範例程式碼：</span><span class="sxs-lookup"><span data-stu-id="a88ea-235">hello output is similar toohello following example:</span></span>

        i am at two with nature             
        an apple a day keeps hello doctor away
        snow white and hello seven dwarfs     
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        four score and seven years ago      
        snow white and hello seven dwarfs     
        snow white and hello seven dwarfs     
        i am at two with nature             
        an apple a day keeps hello doctor away

    <span data-ttu-id="a88ea-236">使用 Ctrl + c toostop hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="a88ea-236">Use Ctrl+c toostop hello script.</span></span>

## <a name="start-hello-reader"></a><span data-ttu-id="a88ea-237">啟動 hello 讀取器</span><span class="sxs-lookup"><span data-stu-id="a88ea-237">Start hello reader</span></span>

1. <span data-ttu-id="a88ea-238">從 hello SSH 工作階段 toohello Storm 叢集，使用下列命令 toostart hello 讀取器拓撲 hello:</span><span class="sxs-lookup"><span data-stu-id="a88ea-238">From hello SSH session toohello Storm cluster, use hello following command toostart hello reader topology:</span></span>

  ```bash
  storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties
  ```

2. <span data-ttu-id="a88ea-239">一旦 hello 拓樸開始，開啟 hello Storm UI。</span><span class="sxs-lookup"><span data-stu-id="a88ea-239">Once hello topology starts, open hello Storm UI.</span></span> <span data-ttu-id="a88ea-240">此 Web UI 位於 https://storm-BASENAME.azurehdinsight.net/stormui。</span><span class="sxs-lookup"><span data-stu-id="a88ea-240">This web UI is located at https://storm-BASENAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="a88ea-241">取代__BASENAME__ hello hello 叢集建立時使用的基底名稱。</span><span class="sxs-lookup"><span data-stu-id="a88ea-241">Replace __BASENAME__ with hello base name used when hello cluster was created.</span></span> 

    <span data-ttu-id="a88ea-242">出現提示時，使用 hello 管理員登入名稱 (預設值， `admin`) 和 hello 叢集建立時使用的密碼。</span><span class="sxs-lookup"><span data-stu-id="a88ea-242">When prompted, use hello admin login name (default, `admin`) and password used when hello cluster was created.</span></span> <span data-ttu-id="a88ea-243">您會看到下列映像網頁類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="a88ea-243">You see a web page similar toohello following image:</span></span>

    ![Storm UI](./media/hdinsight-apache-storm-with-kafka/stormui.png)

3. <span data-ttu-id="a88ea-245">從 hello Storm UI 中，選取 hello __kafka 讀取器__hello 中的連結__拓撲摘要__區段 toodisplay 資訊 hello __kafka 讀取器__拓撲。</span><span class="sxs-lookup"><span data-stu-id="a88ea-245">From hello Storm UI, select hello __kafka-reader__ link in hello __Topology Summary__ section toodisplay information about hello __kafka-reader__ topology.</span></span>

    ![拓樸 hello Storm web UI 的 [摘要] 區段](./media/hdinsight-apache-storm-with-kafka/topology-summary.png)

4. <span data-ttu-id="a88ea-247">toodisplay 資訊 hello 元件的執行個體 hello 記錄器閃電，選取 hello__記錄器閃電__hello 中的連結__攻擊 （所有時間）__ > 一節。</span><span class="sxs-lookup"><span data-stu-id="a88ea-247">toodisplay information about hello instances of hello logger-bolt component, select hello __logger-bolt__ link in hello __Bolts (All time)__ section.</span></span>

    ![Hello 發射區段中的記錄器閃電連結](./media/hdinsight-apache-storm-with-kafka/bolts.png)

5. <span data-ttu-id="a88ea-249">在 hello__執行程式__區段中，選取 hello 中的連結__連接埠__hello 元件的這個執行個體的資料行 toodisplay 記錄資訊。</span><span class="sxs-lookup"><span data-stu-id="a88ea-249">In hello __Executors__ section, select a link in hello __Port__ column toodisplay logging information about this instance of hello component.</span></span>

    ![執行程式連結](./media/hdinsight-apache-storm-with-kafka/executors.png)

    <span data-ttu-id="a88ea-251">hello 記錄檔會包含讀取自 hello Kafka 主題的 hello 資料的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="a88ea-251">hello log contains a log of hello data read from hello Kafka topic.</span></span> <span data-ttu-id="a88ea-252">hello 記錄檔中的 hello 資訊是類似 toohello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="a88ea-252">hello information in hello log is similar toohello following text:</span></span>

        2016-11-04 17:47:14.907 c.m.e.LoggerBolt [INFO] Received data: four score and seven years ago
        2016-11-04 17:47:14.907 STDIO [INFO] hello cow jumped over hello moon
        2016-11-04 17:47:14.908 c.m.e.LoggerBolt [INFO] Received data: hello cow jumped over hello moon
        2016-11-04 17:47:14.911 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.911 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.969 STDIO [INFO] an apple a day keeps hello doctor away
        2016-11-04 17:47:14.970 c.m.e.LoggerBolt [INFO] Received data: an apple a day keeps hello doctor away

## <a name="stop-hello-topologies"></a><span data-ttu-id="a88ea-253">停止 hello 拓撲</span><span class="sxs-lookup"><span data-stu-id="a88ea-253">Stop hello topologies</span></span>

<span data-ttu-id="a88ea-254">從 SSH 工作階段 toohello Storm 叢集中，使用下列命令 toostop hello Storm 拓撲 hello:</span><span class="sxs-lookup"><span data-stu-id="a88ea-254">From an SSH session toohello Storm cluster, use hello following commands toostop hello Storm topologies:</span></span>

  ```bash
  storm kill kafka-writer
  storm kill kafka-reader
  ```

## <a name="delete-hello-cluster"></a><span data-ttu-id="a88ea-255">刪除 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="a88ea-255">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="a88ea-256">因為這份文件中的 hello 步驟建立這兩者中的叢集 hello 相同的 Azure 資源群組，您可以刪除 hello hello Azure 入口網站中的資源群組。</span><span class="sxs-lookup"><span data-stu-id="a88ea-256">Since hello steps in this document create both clusters in hello same Azure resource group, you can delete hello resource group in hello Azure portal.</span></span> <span data-ttu-id="a88ea-257">正在刪除 hello 資源群組中移除遵循本文件所建立的所有資源。</span><span class="sxs-lookup"><span data-stu-id="a88ea-257">Deleting hello resource group removes all resources created by following this document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a88ea-258">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a88ea-258">Next steps</span></span>

<span data-ttu-id="a88ea-259">如需更多可搭配 Storm on HDInsight 使用的拓撲範例，請參閱 [Storm 拓撲和元件範例](hdinsight-storm-example-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="a88ea-259">For more example topologies that can be used with Storm on HDInsight, see [Example Storm topologies and components](hdinsight-storm-example-topology.md).</span></span>

<span data-ttu-id="a88ea-260">如需部署和監視以 Linux 為基礎的 HDInsight 上的拓撲相關資訊，請參閱[部署和管理以 Linux 為基礎的 HDInsight 上的 Apache Storm 拓撲](hdinsight-storm-deploy-monitor-topology-linux.md)</span><span class="sxs-lookup"><span data-stu-id="a88ea-260">For information on deploying and monitoring topologies on Linux-based HDInsight, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>