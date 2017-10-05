---
title: "使用 Apache Kafka 搭配 Storm on HDInsight - Azure | Microsoft Docs"
description: "Apache Kafka 會隨著 Apache Storm on HDInsight 一起安裝。 了解如何使用 Storm 隨附的 KafkaBolt 和 KafkaSpout 元件來寫入 Kafka，然後從中讀取。 並且了解如何使用 Flux 架構來定義及提交 Storm 拓撲。"
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
ms.openlocfilehash: e8895ef3c11aea48513e4060a20f5f49b11fc961
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="use-apache-kafka-preview-with-storm-on-hdinsight"></a><span data-ttu-id="ae42e-105">使用 Apache Kafka (預覽) 搭配 Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="ae42e-105">Use Apache Kafka (preview) with Storm on HDInsight</span></span>

<span data-ttu-id="ae42e-106">了解如何使用 Apache Storm 讀取和寫入 Apache Kafka。</span><span class="sxs-lookup"><span data-stu-id="ae42e-106">Learn how to use Apache Storm to read from and write to Apache Kafka.</span></span> <span data-ttu-id="ae42e-107">本例也示範如何將資料從 Storm 拓撲儲存到 HDInsight 所使用的 HDFS 相容檔案系統。</span><span class="sxs-lookup"><span data-stu-id="ae42e-107">This example also demonstrates how to save data from a Storm topology to the HDFS-compatible file system used by HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="ae42e-108">本文件中的步驟建立 Azure 資源群組，其中包含 Storm on HDInsight 和 Kafka on HDInsight cluster 叢集。</span><span class="sxs-lookup"><span data-stu-id="ae42e-108">The steps in this document create an Azure resource group that contains both a Storm on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="ae42e-109">這兩個叢集都位於 Azure 虛擬網路中，可讓 Storm 叢集直接與 Kafka 叢集通訊。</span><span class="sxs-lookup"><span data-stu-id="ae42e-109">These clusters are both located within an Azure Virtual Network, which allows the Storm cluster to directly communicate with the Kafka cluster.</span></span>
> 
> <span data-ttu-id="ae42e-110">當您完成本文件中的步驟時，請記得刪除叢集，以避免產生過多的費用。</span><span class="sxs-lookup"><span data-stu-id="ae42e-110">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="ae42e-111">取得程式碼</span><span class="sxs-lookup"><span data-stu-id="ae42e-111">Get the code</span></span>

<span data-ttu-id="ae42e-112">在 [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka) 可取得本文件所使用的範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="ae42e-112">The code for the example used in this document is available at [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span></span>

<span data-ttu-id="ae42e-113">若要編譯此專案，您需要開發環境的下列設定：</span><span class="sxs-lookup"><span data-stu-id="ae42e-113">To compile this project, you need the following configuration for your development environment:</span></span>

* <span data-ttu-id="ae42e-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="ae42e-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="ae42e-115">HDInsight 3.5 或更新版本需要 Java 8。</span><span class="sxs-lookup"><span data-stu-id="ae42e-115">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="ae42e-116">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="ae42e-116">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

* <span data-ttu-id="ae42e-117">SSH 用戶端 (您需要 `ssh` 和 `scp` 命令) - 如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="ae42e-117">An SSH client (you need the `ssh` and `scp` commands) - For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="ae42e-118">文字編輯器或整合式開發環境 (IDE)。</span><span class="sxs-lookup"><span data-stu-id="ae42e-118">A text editor or IDE.</span></span>

<span data-ttu-id="ae42e-119">當您在開發工作站上安裝 Java 和 JDK 時可能會設定下列環境變數。</span><span class="sxs-lookup"><span data-stu-id="ae42e-119">The following environment variables may be set when you install Java and the JDK on your development workstation.</span></span> <span data-ttu-id="ae42e-120">不過，您應該檢查它們是否存在，以及它們是否包含您系統的正確值。</span><span class="sxs-lookup"><span data-stu-id="ae42e-120">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="ae42e-121">`JAVA_HOME` - 應指向已安裝 JDK 的目錄。</span><span class="sxs-lookup"><span data-stu-id="ae42e-121">`JAVA_HOME` - should point to the directory where the JDK is installed.</span></span>
* <span data-ttu-id="ae42e-122">`PATH` - 應該包含下列路徑：</span><span class="sxs-lookup"><span data-stu-id="ae42e-122">`PATH` - should contain the following paths:</span></span>
  
    * <span data-ttu-id="ae42e-123">`JAVA_HOME` (或對等的路徑)。</span><span class="sxs-lookup"><span data-stu-id="ae42e-123">`JAVA_HOME` (or the equivalent path).</span></span>
    * <span data-ttu-id="ae42e-124">`JAVA_HOME\bin` (或對等的路徑)。</span><span class="sxs-lookup"><span data-stu-id="ae42e-124">`JAVA_HOME\bin` (or the equivalent path).</span></span>
    * <span data-ttu-id="ae42e-125">已安裝 Maven 的目錄。</span><span class="sxs-lookup"><span data-stu-id="ae42e-125">The directory where Maven is installed.</span></span>

## <a name="create-the-clusters"></a><span data-ttu-id="ae42e-126">建立叢集</span><span class="sxs-lookup"><span data-stu-id="ae42e-126">Create the clusters</span></span>

<span data-ttu-id="ae42e-127">Apache Kafka on HDInsight 不提供透過公用網際網路存取 Kafka 訊息代理程式。</span><span class="sxs-lookup"><span data-stu-id="ae42e-127">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span></span> <span data-ttu-id="ae42e-128">任何 Kafka 相關項目必須位於與 Kafka 叢集中節點相同的 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="ae42e-128">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="ae42e-129">例如，Kafka 和 Storm 叢集均位於 Azure 虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="ae42e-129">For this example, both the Kafka and Storm clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="ae42e-130">下圖顯示叢集之間的通訊流動方式︰</span><span class="sxs-lookup"><span data-stu-id="ae42e-130">The following diagram shows how communication flows between the clusters:</span></span>

![Azure 虛擬網路中的 Storm 和 Kafka 叢集圖表](./media/hdinsight-apache-storm-with-kafka/storm-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="ae42e-132">叢集上的其他服務 (例如 SSH 和 Ambari) 可以透過網際網路存取。</span><span class="sxs-lookup"><span data-stu-id="ae42e-132">Other services on the cluster such as SSH and Ambari can be accessed over the internet.</span></span> <span data-ttu-id="ae42e-133">如需有關適用於 HDInsight 的公用連接埠詳細資訊，請參閱 [HDInsight 所使用的連接埠和 URI](hdinsight-hadoop-port-settings-for-services.md)。</span><span class="sxs-lookup"><span data-stu-id="ae42e-133">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="ae42e-134">雖然您可以手動建立 Azure 虛擬網路、Kafka 和 Storm 叢集，但使用 Azure Resource Manager 範本更輕鬆。</span><span class="sxs-lookup"><span data-stu-id="ae42e-134">While you can create an Azure virtual network, Kafka, and Storm clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="ae42e-135">使用下列步驟將 Azure 虛擬網路、Kafka 和 Storm 叢集部署到 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ae42e-135">Use the following steps to deploy an Azure virtual network, Kafka, and Storm clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="ae42e-136">使用以下按鈕，在 Azure 入口網站中登入 Azure 並開啟範本。</span><span class="sxs-lookup"><span data-stu-id="ae42e-136">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-storm-cluster-in-vnet-v2.json" target="_blank"><img src="./media/hdinsight-apache-storm-with-kafka/deploy-to-azure.png" alt="Deploy to Azure"></a>
   
    <span data-ttu-id="ae42e-137">Azure Resource Manager 範本位於 **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**。</span><span class="sxs-lookup"><span data-stu-id="ae42e-137">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**.</span></span> <span data-ttu-id="ae42e-138">它會建立下列資源︰</span><span class="sxs-lookup"><span data-stu-id="ae42e-138">It creates the following resources:</span></span>
    
    * <span data-ttu-id="ae42e-139">Azure 資源群組</span><span class="sxs-lookup"><span data-stu-id="ae42e-139">Azure resource group</span></span>
    * <span data-ttu-id="ae42e-140">Azure 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="ae42e-140">Azure Virtual Network</span></span>
    * <span data-ttu-id="ae42e-141">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="ae42e-141">Azure Storage account</span></span>
    * <span data-ttu-id="ae42e-142">HDInsight 版本 3.6 上的 Kafka (三個背景工作角色節點)</span><span class="sxs-lookup"><span data-stu-id="ae42e-142">Kafka on HDInsight version 3.6 (three worker nodes)</span></span>
    * <span data-ttu-id="ae42e-143">HDInsight 版本 3.6 上的 Storm (三個背景工作角色節點)</span><span class="sxs-lookup"><span data-stu-id="ae42e-143">Storm on HDInsight version 3.6 (three worker nodes)</span></span>

  > [!WARNING]
  > <span data-ttu-id="ae42e-144">若要保證 Kafka 在 HDInsight 上的可用性，您的叢集必須包含至少三個背景工作角色節點。</span><span class="sxs-lookup"><span data-stu-id="ae42e-144">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="ae42e-145">此範本會建立包含三個背景工作角色節點的 Kafka 叢集。</span><span class="sxs-lookup"><span data-stu-id="ae42e-145">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="ae42e-146">使用下列指引來填入 [自訂部署] 刀鋒視窗上的項目︰</span><span class="sxs-lookup"><span data-stu-id="ae42e-146">Use the following guidance to populate the entries on the **Custom deployment** blade:</span></span>
   
    ![HDInsight 自訂部署](./media/hdinsight-apache-storm-with-kafka/parameters.png)

    * <span data-ttu-id="ae42e-148">**資源群組**：建立群組或選取現有的群組。</span><span class="sxs-lookup"><span data-stu-id="ae42e-148">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="ae42e-149">此群組包含 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="ae42e-149">This group contains the HDInsight cluster.</span></span>
   
    * <span data-ttu-id="ae42e-150">**位置**：選取在地理上靠近您的位置。</span><span class="sxs-lookup"><span data-stu-id="ae42e-150">**Location**: Select a location geographically close to you.</span></span>

    * <span data-ttu-id="ae42e-151">**基底叢集名稱**︰此值會做為 Storm 和 Kafka 叢集的基底名稱。</span><span class="sxs-lookup"><span data-stu-id="ae42e-151">**Base Cluster Name**: This value is used as the base name for the Storm and Kafka clusters.</span></span> <span data-ttu-id="ae42e-152">例如，輸入 **hdi** 可建立名為 **storm-hdi** 的 Storm 叢集以及名為 **kafka-hdi** 的 Kafka 叢集。</span><span class="sxs-lookup"><span data-stu-id="ae42e-152">For example, entering **hdi** creates a Storm cluster named **storm-hdi** and a Kafka cluster named **kafka-hdi**.</span></span>
   
    * <span data-ttu-id="ae42e-153">**叢集登入使用者名稱**：Storm 和 Kafka 叢集的系統管理員使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="ae42e-153">**Cluster Login User Name**: The admin user name for the Storm and Kafka clusters.</span></span>
   
    * <span data-ttu-id="ae42e-154">**叢集登入密碼**：Storm 和 Kafka 叢集的系統管理員使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="ae42e-154">**Cluster Login Password**: The admin user password for the Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="ae42e-155">**SSH 使用者名稱**︰建立 Storm 和 Kafka 叢集的 SSH 使用者。</span><span class="sxs-lookup"><span data-stu-id="ae42e-155">**SSH User Name**: The SSH user to create for the Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="ae42e-156">**SSH 密碼**：Storm 和 Kafka 叢集的 SSH 使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="ae42e-156">**SSH Password**: The password for the SSH user for the Storm and Kafka clusters.</span></span>

3. <span data-ttu-id="ae42e-157">讀取**條款及條件**，然後選取 [我同意上方所述的條款及條件]。</span><span class="sxs-lookup"><span data-stu-id="ae42e-157">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="ae42e-158">最後，核取 [釘選到儀表板]，然後選取 [購買]。</span><span class="sxs-lookup"><span data-stu-id="ae42e-158">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="ae42e-159">大約需要 20 分鐘的時間來建立叢集。</span><span class="sxs-lookup"><span data-stu-id="ae42e-159">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="ae42e-160">一旦建立資源，即會顯示 [資源群組] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ae42e-160">Once the resources have been created, the blade for the resource group is displayed.</span></span>

![Vnet 和叢集的資源群組刀鋒視窗](./media/hdinsight-apache-storm-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="ae42e-162">請注意，HDInsight 叢集的名稱是 **storm-BASENAME** 和 **kafka-BASENAME**，其中 BASENAME 是您提供給範本的名稱。</span><span class="sxs-lookup"><span data-stu-id="ae42e-162">Notice that the names of the HDInsight clusters are **storm-BASENAME** and **kafka-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="ae42e-163">連接到叢集時，您會在稍後步驟中使用這些名稱。</span><span class="sxs-lookup"><span data-stu-id="ae42e-163">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="understanding-the-code"></a><span data-ttu-id="ae42e-164">了解程式碼</span><span class="sxs-lookup"><span data-stu-id="ae42e-164">Understanding the code</span></span>

<span data-ttu-id="ae42e-165">此專案包含兩種拓撲︰</span><span class="sxs-lookup"><span data-stu-id="ae42e-165">This project contains two topologies:</span></span>

* <span data-ttu-id="ae42e-166">**KafkaWriter**︰由 **writer.yaml** 檔案定義，此拓撲會使用 Apache Storm 隨附的 KafkaBolt 將隨機句子寫入 Kafka。</span><span class="sxs-lookup"><span data-stu-id="ae42e-166">**KafkaWriter**: Defined by the **writer.yaml** file, this topology writes random sentences to Kafka using the KafkaBolt provided with Apache Storm.</span></span>

    <span data-ttu-id="ae42e-167">此拓撲使用自訂 **SentenceSpout** 元件來產生隨機句子。</span><span class="sxs-lookup"><span data-stu-id="ae42e-167">This topology uses a custom **SentenceSpout** component to generate random sentences.</span></span>

* <span data-ttu-id="ae42e-168">**KafkaReader**︰由 **reader.yaml** 檔案定義，此拓撲會使用 Apache Storm 隨附的 KafkaSpout 來讀取 Kafka 中的資料，然後將資料記錄至 stdout。</span><span class="sxs-lookup"><span data-stu-id="ae42e-168">**KafkaReader**: Defined by the **reader.yaml** file, this topology reads data from Kafka using the KafkaSpout provided with Apache Storm, then logs the data to stdout.</span></span>

    <span data-ttu-id="ae42e-169">此拓撲使用 Storm HdfsBolt 將資料寫入 Storm 叢集的預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="ae42e-169">This topology uses the Storm HdfsBolt to write data to default storage for the Storm cluster.</span></span>
### <a name="flux"></a><span data-ttu-id="ae42e-170">Flux</span><span class="sxs-lookup"><span data-stu-id="ae42e-170">Flux</span></span>

<span data-ttu-id="ae42e-171">拓撲是使用 [Flux](https://storm.apache.org/releases/1.1.0/flux.html) 來定義的。</span><span class="sxs-lookup"><span data-stu-id="ae42e-171">The topologies are defined using [Flux](https://storm.apache.org/releases/1.1.0/flux.html).</span></span> <span data-ttu-id="ae42e-172">Storm 0.10.x 引進了 Flux，可讓您區隔拓撲組態與程式碼。</span><span class="sxs-lookup"><span data-stu-id="ae42e-172">Flux was introduced in Storm 0.10.x and allows you to separate the topology configuration from the code.</span></span> <span data-ttu-id="ae42e-173">若為使用 Flux 架構的拓撲，拓撲定義於 YAML 檔案中。</span><span class="sxs-lookup"><span data-stu-id="ae42e-173">For Topologies that use the Flux framework, the topology is defined in a YAML file.</span></span> <span data-ttu-id="ae42e-174">YAML 檔案可以納入為拓撲的一部分。</span><span class="sxs-lookup"><span data-stu-id="ae42e-174">The YAML file can be included as part of the topology.</span></span> <span data-ttu-id="ae42e-175">它也可以是您提交拓撲時使用的獨立檔案。</span><span class="sxs-lookup"><span data-stu-id="ae42e-175">It can also be a standalone file used when you submit the topology.</span></span> <span data-ttu-id="ae42e-176">Flux 也支援執行階段的變數替代 (在此範例中使用)。</span><span class="sxs-lookup"><span data-stu-id="ae42e-176">Flux also supports variable substitution at run-time, which is used in this example.</span></span>

<span data-ttu-id="ae42e-177">在執行階段會針對這些拓撲設定下列參數：</span><span class="sxs-lookup"><span data-stu-id="ae42e-177">The following parameters are set at run time for these topologies:</span></span>

* <span data-ttu-id="ae42e-178">`${kafka.topic}`：拓樸讀取/寫入的 Kafka 主題名稱。</span><span class="sxs-lookup"><span data-stu-id="ae42e-178">`${kafka.topic}`: The name of the Kafka topic that the topologies read/write to.</span></span>

* <span data-ttu-id="ae42e-179">`${kafka.broker.hosts}`：Kafka 訊息代理程式執行所在的主機。</span><span class="sxs-lookup"><span data-stu-id="ae42e-179">`${kafka.broker.hosts}`: The hosts that the Kafka brokers run on.</span></span> <span data-ttu-id="ae42e-180">KafkaBolt 在寫入 Kafka 時會使用訊息代理程式資訊。</span><span class="sxs-lookup"><span data-stu-id="ae42e-180">The broker information is used by the KafkaBolt when writing to Kafka.</span></span>

* <span data-ttu-id="ae42e-181">`${kafka.zookeeper.hosts}`：Kafka 叢集中 Zookeeper 執行所在的主機。</span><span class="sxs-lookup"><span data-stu-id="ae42e-181">`${kafka.zookeeper.hosts}`: The hosts that Zookeeper runs on in the Kafka cluster.</span></span>

<span data-ttu-id="ae42e-182">如需 Flux 拓撲的詳細資訊，請參閱 [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html)。</span><span class="sxs-lookup"><span data-stu-id="ae42e-182">For more information on Flux topologies, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="download-and-compile-the-project"></a><span data-ttu-id="ae42e-183">下載並編譯專案</span><span class="sxs-lookup"><span data-stu-id="ae42e-183">Download and compile the project</span></span>

1. <span data-ttu-id="ae42e-184">在開發環境中，從 [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka) 下載專案，開啟命令列，並將目錄變更為您下載專案的位置。</span><span class="sxs-lookup"><span data-stu-id="ae42e-184">On your development environment, download the project from [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), open a command-line, and change directories to the location that you downloaded the project.</span></span>

2. <span data-ttu-id="ae42e-185">從 **hdinsight-storm-java-kafka** 目錄，使用下列命令來編譯專案並建立部署套件︰</span><span class="sxs-lookup"><span data-stu-id="ae42e-185">From the **hdinsight-storm-java-kafka** directory, use the following command to compile the project and create a package for deployment:</span></span>

  ```bash
  mvn clean package
  ```

    <span data-ttu-id="ae42e-186">封裝程序會在 `target` 目錄中建立名為 `KafkaTopology-1.0-SNAPSHOT.jar` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="ae42e-186">The package process creates a file named `KafkaTopology-1.0-SNAPSHOT.jar` in the `target` directory.</span></span>

3. <span data-ttu-id="ae42e-187">使用下列命令將套件複製到 Storm on HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="ae42e-187">Use the following commands to copy the package to your Storm on HDInsight cluster.</span></span> <span data-ttu-id="ae42e-188">將 **USERNAME** 替換為叢集的 SSH 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="ae42e-188">Replace **USERNAME** with the SSH user name for the cluster.</span></span> <span data-ttu-id="ae42e-189">將 **BASENAME** 替換為您在建立叢集時使用的基底名稱。</span><span class="sxs-lookup"><span data-stu-id="ae42e-189">Replace **BASENAME** with the base name you used when creating the cluster.</span></span>

  ```bash
  scp ./target/KafkaTopology-1.0-SNAPSHOT.jar USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
  ```

    <span data-ttu-id="ae42e-190">出現提示時，請輸入您在建立叢集時所使用的密碼。</span><span class="sxs-lookup"><span data-stu-id="ae42e-190">When prompted, enter the password you used when creating the clusters.</span></span>

## <a name="configure-the-topology"></a><span data-ttu-id="ae42e-191">設定拓撲</span><span class="sxs-lookup"><span data-stu-id="ae42e-191">Configure the topology</span></span>

1. <span data-ttu-id="ae42e-192">請使用下列方法之一探索 Kafka 訊息代理程式主機：</span><span class="sxs-lookup"><span data-stu-id="ae42e-192">Use one of the following methods to discover the Kafka broker hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
    $clusterName = Read-Host -Prompt "Enter the Kafka cluster name"
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
    > <span data-ttu-id="ae42e-193">Bash 範例假設 `$CLUSTERNAME` 包含 HDInsight 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="ae42e-193">The Bash example assumes that `$CLUSTERNAME` contains the name of the HDInsight cluster.</span></span> <span data-ttu-id="ae42e-194">它也假設已安裝 [jq](https://stedolan.github.io/jq/)。</span><span class="sxs-lookup"><span data-stu-id="ae42e-194">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="ae42e-195">出現提示時，輸入叢集登入帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="ae42e-195">When prompted, enter the password for the cluster login account.</span></span>

    <span data-ttu-id="ae42e-196">傳回的值類似下列文字︰</span><span class="sxs-lookup"><span data-stu-id="ae42e-196">The value returned is similar to the following text:</span></span>

        wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092

    > [!IMPORTANT]
    > <span data-ttu-id="ae42e-197">雖然叢集可能有兩個以上的訊息代理程式主機，您並不需要提供客戶端完整的主機名單。</span><span class="sxs-lookup"><span data-stu-id="ae42e-197">While there may be more than two broker hosts for your cluster, you do not need to provide a full list of all hosts to clients.</span></span> <span data-ttu-id="ae42e-198">列出一兩個主機便已足夠。</span><span class="sxs-lookup"><span data-stu-id="ae42e-198">One or two is enough.</span></span>

2. <span data-ttu-id="ae42e-199">請使用下列方法之一探索 Kafka Zookeeper 主機：</span><span class="sxs-lookup"><span data-stu-id="ae42e-199">Use one of the following methods to discover the Kafka Zookeeper hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
    $clusterName = Read-Host -Prompt "Enter the Kafka cluster name"
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
    > <span data-ttu-id="ae42e-200">Bash 範例假設 `$CLUSTERNAME` 包含 HDInsight 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="ae42e-200">The Bash example assumes that `$CLUSTERNAME` contains the name of the HDInsight cluster.</span></span> <span data-ttu-id="ae42e-201">它也假設已安裝 [jq](https://stedolan.github.io/jq/)。</span><span class="sxs-lookup"><span data-stu-id="ae42e-201">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="ae42e-202">出現提示時，輸入叢集登入帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="ae42e-202">When prompted, enter the password for the cluster login account.</span></span>

    <span data-ttu-id="ae42e-203">傳回的值類似下列文字︰</span><span class="sxs-lookup"><span data-stu-id="ae42e-203">The value returned is similar to the following text:</span></span>

        zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181

    > [!IMPORTANT]
    > <span data-ttu-id="ae42e-204">雖然可能有兩個以上的 Zookeeper 節點，您並不需要提供客戶端完整的主機名單。</span><span class="sxs-lookup"><span data-stu-id="ae42e-204">While there are more than two Zookeeper nodes, you do not need to provide a full list of all hosts to clients.</span></span> <span data-ttu-id="ae42e-205">列出一兩個主機便已足夠。</span><span class="sxs-lookup"><span data-stu-id="ae42e-205">One or two is enough.</span></span>

    <span data-ttu-id="ae42e-206">儲存這個值以便稍後使用。</span><span class="sxs-lookup"><span data-stu-id="ae42e-206">Save this value, as it is used later.</span></span>

3. <span data-ttu-id="ae42e-207">編輯專案根目錄中的 `dev.properties` 檔案。</span><span class="sxs-lookup"><span data-stu-id="ae42e-207">Edit the `dev.properties` file in the root of the project.</span></span> <span data-ttu-id="ae42e-208">將訊息代理程式和 Zookeeper 主機資訊新增至本檔案相符的行。</span><span class="sxs-lookup"><span data-stu-id="ae42e-208">Add the Broker and Zookeeper hosts information to the matching lines in this file.</span></span> <span data-ttu-id="ae42e-209">下例是使用先前步驟中的範例值所設定：</span><span class="sxs-lookup"><span data-stu-id="ae42e-209">The following example is configured using the sample values from the previous steps:</span></span>

        kafka.zookeeper.hosts: zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181
        kafka.broker.hosts: wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092
        kafka.topic: stormtopic

4. <span data-ttu-id="ae42e-210">儲存 `dev.properties` 檔案，然後使用下列命令將它上傳至 Storm 叢集：</span><span class="sxs-lookup"><span data-stu-id="ae42e-210">Save the `dev.properties` file and then use the following command to upload it to the Storm cluster:</span></span>

     ```bash
    scp dev.properties USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
    ```

    <span data-ttu-id="ae42e-211">將 **USERNAME** 替換為叢集的 SSH 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="ae42e-211">Replace **USERNAME** with the SSH user name for the cluster.</span></span> <span data-ttu-id="ae42e-212">將 **BASENAME** 替換為您在建立叢集時使用的基底名稱。</span><span class="sxs-lookup"><span data-stu-id="ae42e-212">Replace **BASENAME** with the base name you used when creating the cluster.</span></span>

## <a name="start-the-writer"></a><span data-ttu-id="ae42e-213">開始寫入器</span><span class="sxs-lookup"><span data-stu-id="ae42e-213">Start the writer</span></span>

1. <span data-ttu-id="ae42e-214">使用下列命令來透過 SSH 連接到 Storm 叢集。</span><span class="sxs-lookup"><span data-stu-id="ae42e-214">Use the following to connect to the Storm cluster using SSH.</span></span> <span data-ttu-id="ae42e-215">將 **USERNAME** 替換為建立叢集時所使用的 SSH 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="ae42e-215">Replace **USERNAME** with the SSH user name used when creating the cluster.</span></span> <span data-ttu-id="ae42e-216">將 **BASENAME** 替換為建立叢集時使用的基底名稱。</span><span class="sxs-lookup"><span data-stu-id="ae42e-216">Replace **BASENAME** with the base name used when creating the cluster.</span></span>

  ```bash
  ssh USERNAME@storm-BASENAME-ssh.azurehdinsight.net
  ```

    <span data-ttu-id="ae42e-217">出現提示時，請輸入您在建立叢集時所使用的密碼。</span><span class="sxs-lookup"><span data-stu-id="ae42e-217">When prompted, enter the password you used when creating the clusters.</span></span>
   
    <span data-ttu-id="ae42e-218">如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="ae42e-218">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="ae42e-219">從 SSH 連線，使用下列命令來建立拓撲使用的 Kafka 主題：</span><span class="sxs-lookup"><span data-stu-id="ae42e-219">From the SSH connection, use the following command to create the Kafka topic used by the topology:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic stormtopic --zookeeper $KAFKAZKHOSTS
    ```

    <span data-ttu-id="ae42e-220">以您在上一節擷取的 Zookeeper 主機資訊取代 `$KAFKAZKHOSTS`。</span><span class="sxs-lookup"><span data-stu-id="ae42e-220">Replace `$KAFKAZKHOSTS` with the Zookeeper host information you retrieved in the previous section.</span></span>

2. <span data-ttu-id="ae42e-221">在連往 Storm 叢集的 SSH 連線中，使用下列命令來啟動寫入器拓撲：</span><span class="sxs-lookup"><span data-stu-id="ae42e-221">From the SSH connection to the Storm cluster, use the following command to start the writer topology:</span></span>

    ```bash
    storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
    ```

    <span data-ttu-id="ae42e-222">此命令使用的參數如下：</span><span class="sxs-lookup"><span data-stu-id="ae42e-222">The parameters used with this command are:</span></span>

    * <span data-ttu-id="ae42e-223">`org.apache.storm.flux.Flux`︰使用 Flux 來設定及執行此拓撲。</span><span class="sxs-lookup"><span data-stu-id="ae42e-223">`org.apache.storm.flux.Flux`: Use Flux to configure and run this topology.</span></span>

    * <span data-ttu-id="ae42e-224">`--remote`：將拓撲提交至 Nimbus。</span><span class="sxs-lookup"><span data-stu-id="ae42e-224">`--remote`: Submit the topology to Nimbus.</span></span> <span data-ttu-id="ae42e-225">拓撲會分散於叢集中的背景工作節點。</span><span class="sxs-lookup"><span data-stu-id="ae42e-225">The topology is distributed across the worker nodes in the cluster.</span></span>

    * <span data-ttu-id="ae42e-226">`-R /writer.yaml`︰使用 `writer.yaml` 檔案來設定拓撲。</span><span class="sxs-lookup"><span data-stu-id="ae42e-226">`-R /writer.yaml`: Use the `writer.yaml` file to configure the topology.</span></span> <span data-ttu-id="ae42e-227">`-R` 表示此資源包含在 jar 檔案中。</span><span class="sxs-lookup"><span data-stu-id="ae42e-227">`-R` indicates that this resource is included in the jar file.</span></span> <span data-ttu-id="ae42e-228">剛檔案位於 jar 的根目錄中，所以 `/writer.yaml` 是它的路徑。</span><span class="sxs-lookup"><span data-stu-id="ae42e-228">It's in the root of the jar, so `/writer.yaml` is the path to it.</span></span>

    * <span data-ttu-id="ae42e-229">`--filter`：使用 `dev.properties` 檔案的值填入 `writer.yaml` 拓撲的項目。</span><span class="sxs-lookup"><span data-stu-id="ae42e-229">`--filter`: Populate entries in the `writer.yaml` topology using values in the `dev.properties` file.</span></span> <span data-ttu-id="ae42e-230">例如，使用檔案的 `kafka.topic` 項目值取代拓撲定義的 `${kafka.topic}` 項目。</span><span class="sxs-lookup"><span data-stu-id="ae42e-230">For example, the value of the `kafka.topic` entry in the file is used to replace the `${kafka.topic}` entry in the topology definition.</span></span>

5. <span data-ttu-id="ae42e-231">一旦啟動拓撲，請使用下列命令確認它將資料寫入 Kafka 主題：</span><span class="sxs-lookup"><span data-stu-id="ae42e-231">Once the topology has started, use the following command to verify that it is writing data to the Kafka topic:</span></span>

  ```bash
  /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $KAFKAZKHOSTS --from-beginning --topic stormtopic
  ```

    <span data-ttu-id="ae42e-232">以您在上一節擷取的 Zookeeper 主機資訊取代 `$KAFKAZKHOSTS`。</span><span class="sxs-lookup"><span data-stu-id="ae42e-232">Replace `$KAFKAZKHOSTS` with the Zookeeper host information you retrieved in the previous section.</span></span>

    <span data-ttu-id="ae42e-233">此命令會使用 Kafka 隨附的指令碼來監視主題。</span><span class="sxs-lookup"><span data-stu-id="ae42e-233">This command uses a script shipped with Kafka to monitor the topic.</span></span> <span data-ttu-id="ae42e-234">稍後，它應該會開始傳回已寫入主題的隨機句子。</span><span class="sxs-lookup"><span data-stu-id="ae42e-234">After a moment, it should start returning random sentences that have been written to the topic.</span></span> <span data-ttu-id="ae42e-235">輸出類似於下列範例：</span><span class="sxs-lookup"><span data-stu-id="ae42e-235">The output is similar to the following example:</span></span>

        i am at two with nature             
        an apple a day keeps the doctor away
        snow white and the seven dwarfs     
        the cow jumped over the moon        
        an apple a day keeps the doctor away
        an apple a day keeps the doctor away
        the cow jumped over the moon        
        an apple a day keeps the doctor away
        an apple a day keeps the doctor away
        four score and seven years ago      
        snow white and the seven dwarfs     
        snow white and the seven dwarfs     
        i am at two with nature             
        an apple a day keeps the doctor away

    <span data-ttu-id="ae42e-236">使用 Ctrl + c 來停止指令碼。</span><span class="sxs-lookup"><span data-stu-id="ae42e-236">Use Ctrl+c to stop the script.</span></span>

## <a name="start-the-reader"></a><span data-ttu-id="ae42e-237">開始讀取器</span><span class="sxs-lookup"><span data-stu-id="ae42e-237">Start the reader</span></span>

1. <span data-ttu-id="ae42e-238">在 Storm 叢集的 SSH 工作階段中，使用下列命令來啟動讀取器拓撲：</span><span class="sxs-lookup"><span data-stu-id="ae42e-238">From the SSH session to the Storm cluster, use the following command to start the reader topology:</span></span>

  ```bash
  storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties
  ```

2. <span data-ttu-id="ae42e-239">拓撲啟動後，請開啟 Storm UI。</span><span class="sxs-lookup"><span data-stu-id="ae42e-239">Once the topology starts, open the Storm UI.</span></span> <span data-ttu-id="ae42e-240">此 Web UI 位於 https://storm-BASENAME.azurehdinsight.net/stormui。</span><span class="sxs-lookup"><span data-stu-id="ae42e-240">This web UI is located at https://storm-BASENAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="ae42e-241">將 __BASENAME__ 替換為建立叢集時使用的基底名稱。</span><span class="sxs-lookup"><span data-stu-id="ae42e-241">Replace __BASENAME__ with the base name used when the cluster was created.</span></span> 

    <span data-ttu-id="ae42e-242">出現提示時，使用建立叢集時所用的系統管理員登入名稱 (預設為 `admin`) 和密碼。</span><span class="sxs-lookup"><span data-stu-id="ae42e-242">When prompted, use the admin login name (default, `admin`) and password used when the cluster was created.</span></span> <span data-ttu-id="ae42e-243">您會看到類似下圖的網頁︰</span><span class="sxs-lookup"><span data-stu-id="ae42e-243">You see a web page similar to the following image:</span></span>

    ![Storm UI](./media/hdinsight-apache-storm-with-kafka/stormui.png)

3. <span data-ttu-id="ae42e-245">從 Storm UI 選取 [拓樸摘要] 區段中的 __kafka-reader__ 連結，以顯示 __kafka-reader__ 拓樸相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ae42e-245">From the Storm UI, select the __kafka-reader__ link in the __Topology Summary__ section to display information about the __kafka-reader__ topology.</span></span>

    ![Storm Web UI 的拓撲摘要區段](./media/hdinsight-apache-storm-with-kafka/topology-summary.png)

4. <span data-ttu-id="ae42e-247">選取 [Bolt (所有時間)] 區段中的 __logger-bolt__ 連結，以顯示 logger-bolt 元件的執行個體相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ae42e-247">To display information about the instances of the logger-bolt component, select the __logger-bolt__ link in the __Bolts (All time)__ section.</span></span>

    ![Bolt 區段中的 Logger-bolt 連結](./media/hdinsight-apache-storm-with-kafka/bolts.png)

5. <span data-ttu-id="ae42e-249">在 [執行程式] 區段中，選取 [連接埠] 欄中的連結，以顯示此元件執行個體的記錄資訊。</span><span class="sxs-lookup"><span data-stu-id="ae42e-249">In the __Executors__ section, select a link in the __Port__ column to display logging information about this instance of the component.</span></span>

    ![執行程式連結](./media/hdinsight-apache-storm-with-kafka/executors.png)

    <span data-ttu-id="ae42e-251">記錄檔包含從 Kafka 主題讀取的資料記錄檔。</span><span class="sxs-lookup"><span data-stu-id="ae42e-251">The log contains a log of the data read from the Kafka topic.</span></span> <span data-ttu-id="ae42e-252">記錄檔中的資訊類似下列文字︰</span><span class="sxs-lookup"><span data-stu-id="ae42e-252">The information in the log is similar to the following text:</span></span>

        2016-11-04 17:47:14.907 c.m.e.LoggerBolt [INFO] Received data: four score and seven years ago
        2016-11-04 17:47:14.907 STDIO [INFO] the cow jumped over the moon
        2016-11-04 17:47:14.908 c.m.e.LoggerBolt [INFO] Received data: the cow jumped over the moon
        2016-11-04 17:47:14.911 STDIO [INFO] snow white and the seven dwarfs
        2016-11-04 17:47:14.911 c.m.e.LoggerBolt [INFO] Received data: snow white and the seven dwarfs
        2016-11-04 17:47:14.932 STDIO [INFO] snow white and the seven dwarfs
        2016-11-04 17:47:14.932 c.m.e.LoggerBolt [INFO] Received data: snow white and the seven dwarfs
        2016-11-04 17:47:14.969 STDIO [INFO] an apple a day keeps the doctor away
        2016-11-04 17:47:14.970 c.m.e.LoggerBolt [INFO] Received data: an apple a day keeps the doctor away

## <a name="stop-the-topologies"></a><span data-ttu-id="ae42e-253">停止拓撲</span><span class="sxs-lookup"><span data-stu-id="ae42e-253">Stop the topologies</span></span>

<span data-ttu-id="ae42e-254">在連往 Storm 叢集的 SSH 工作階段中，使用下列命令來停止 Storm 拓撲：</span><span class="sxs-lookup"><span data-stu-id="ae42e-254">From an SSH session to the Storm cluster, use the following commands to stop the Storm topologies:</span></span>

  ```bash
  storm kill kafka-writer
  storm kill kafka-reader
  ```

## <a name="delete-the-cluster"></a><span data-ttu-id="ae42e-255">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="ae42e-255">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="ae42e-256">因為本文件中的步驟會在相同的 Azure 資源群組中建立兩個叢集，您可以在 Azure 入口網站中刪除資源群組。</span><span class="sxs-lookup"><span data-stu-id="ae42e-256">Since the steps in this document create both clusters in the same Azure resource group, you can delete the resource group in the Azure portal.</span></span> <span data-ttu-id="ae42e-257">刪除資源群組，會移除依照本文指示建立的所有資源。</span><span class="sxs-lookup"><span data-stu-id="ae42e-257">Deleting the resource group removes all resources created by following this document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae42e-258">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ae42e-258">Next steps</span></span>

<span data-ttu-id="ae42e-259">如需更多可搭配 Storm on HDInsight 使用的拓撲範例，請參閱 [Storm 拓撲和元件範例](hdinsight-storm-example-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="ae42e-259">For more example topologies that can be used with Storm on HDInsight, see [Example Storm topologies and components](hdinsight-storm-example-topology.md).</span></span>

<span data-ttu-id="ae42e-260">如需部署和監視以 Linux 為基礎的 HDInsight 上的拓撲相關資訊，請參閱[部署和管理以 Linux 為基礎的 HDInsight 上的 Apache Storm 拓撲](hdinsight-storm-deploy-monitor-topology-linux.md)</span><span class="sxs-lookup"><span data-stu-id="ae42e-260">For information on deploying and monitoring topologies on Linux-based HDInsight, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>