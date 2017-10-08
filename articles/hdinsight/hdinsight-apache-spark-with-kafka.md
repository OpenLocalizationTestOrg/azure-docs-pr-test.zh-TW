---
title: "aaaApache Spark Kafka-Azure HDInsight 進行資料流處理 |Microsoft 文件"
description: "深入了解如何 toouse Spark Apache Spark toostream 資料傳入或傳出 Apache Kafka 使用 DStreams。 在此範例中，您使用 Jupyter Notebook 從 HDInsight 上的 Spark 串流資料。"
keywords: "kafka 範例,kafka zookeeper,spark 串流 kafka,spark 串流 kafka 範例"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: dd8f53c1-bdee-4921-b683-3be4c46c2039
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: f48b37aadafa4979cd27af68e8417db6acc8a0e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-dstream-example-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="cb500-105">在 HDInsight 上使用 Kafka 的 Apache Spark 串流 (DStream) 範例 (預覽)</span><span class="sxs-lookup"><span data-stu-id="cb500-105">Apache Spark streaming (DStream) example with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="cb500-106">深入了解如何 toouse 傳入或傳出 Apache Kafka 使用 DStreams HDInsight 上的 Spark Apache Spark toostream 資料。</span><span class="sxs-lookup"><span data-stu-id="cb500-106">Learn how toouse Spark Apache Spark toostream data into or out of Apache Kafka on HDInsight using DStreams.</span></span> <span data-ttu-id="cb500-107">這個範例會使用 Jupyter 筆記本 hello Spark 叢集上執行。</span><span class="sxs-lookup"><span data-stu-id="cb500-107">This example uses a Jupyter notebook that runs on hello Spark cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="cb500-108">本文件中的 hello 步驟建立包含 HDInsight 上的 Spark 以及 Kafka HDInsight 叢集上的 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="cb500-108">hello steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="cb500-109">這些叢集會同時位於 Azure 虛擬網路，可讓 hello Spark 叢集 toodirectly 與 hello Kafka 叢集通訊。</span><span class="sxs-lookup"><span data-stu-id="cb500-109">These clusters are both located within an Azure Virtual Network, which allows hello Spark cluster toodirectly communicate with hello Kafka cluster.</span></span>
>
> <span data-ttu-id="cb500-110">當您完成這份文件中的 hello 步驟之後時，請記得 toodelete hello 叢集 tooavoid 過多費用。</span><span class="sxs-lookup"><span data-stu-id="cb500-110">When you are done with hello steps in this document, remember toodelete hello clusters tooavoid excess charges.</span></span>

## <a name="create-hello-clusters"></a><span data-ttu-id="cb500-111">建立 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="cb500-111">Create hello clusters</span></span>

<span data-ttu-id="cb500-112">Apache Kafka HDInsight 上不提供存取 toohello Kafka broker 透過 hello 公用網際網路。</span><span class="sxs-lookup"><span data-stu-id="cb500-112">Apache Kafka on HDInsight does not provide access toohello Kafka brokers over hello public internet.</span></span> <span data-ttu-id="cb500-113">討論 tooKafka 必須在 hello 與 hello 節點中的相同 Azure 虛擬網路的任何項目 hello Kafka 叢集。</span><span class="sxs-lookup"><span data-stu-id="cb500-113">Anything that talks tooKafka must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="cb500-114">例如，hello Kafka 與 Spark 叢集位於 Azure 的虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="cb500-114">For this example, both hello Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="cb500-115">hello 下圖顯示 hello 叢集之間通訊流動的方式：</span><span class="sxs-lookup"><span data-stu-id="cb500-115">hello following diagram shows how communication flows between hello clusters:</span></span>

![Azure 虛擬網路中的 Spark 和 Kafka 叢集圖表](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="cb500-117">雖然 Kafka 本身是有限的 toocommunication hello 虛擬網路內，hello 叢集上的其他服務例如可以透過存取 SSH 和 Ambari hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="cb500-117">Though Kafka itself is limited toocommunication within hello virtual network, other services on hello cluster such as SSH and Ambari can be accessed over hello internet.</span></span> <span data-ttu-id="cb500-118">Hello 公用連接埠適用於 HDInsight 上的詳細資訊，請參閱[連接埠和 Uri 使用 HDInsight](hdinsight-hadoop-port-settings-for-services.md)。</span><span class="sxs-lookup"><span data-stu-id="cb500-118">For more information on hello public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="cb500-119">雖然您可以建立 Azure 虛擬網路，Kafka 和 Spark 叢集以手動方式，很容易 toouse Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="cb500-119">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="cb500-120">使用 hello 下列步驟 toodeploy Azure 虛擬網路，Kafka，，和 Spark 叢集 tooyour Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="cb500-120">Use hello following steps toodeploy an Azure virtual network, Kafka, and Spark clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="cb500-121">使用下列按鈕 toosign 中 tooAzure 和開啟 hello 範本 hello Azure 入口網站中的 hello。</span><span class="sxs-lookup"><span data-stu-id="cb500-121">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    <span data-ttu-id="cb500-122">hello Azure Resource Manager 範本位於**https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**。</span><span class="sxs-lookup"><span data-stu-id="cb500-122">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="cb500-123">HDInsight 上 Kafka tooguarantee 可用性，您的叢集必須包含至少三個背景工作節點。</span><span class="sxs-lookup"><span data-stu-id="cb500-123">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="cb500-124">此範本會建立包含三個背景工作角色節點的 Kafka 叢集。</span><span class="sxs-lookup"><span data-stu-id="cb500-124">This template creates a Kafka cluster that contains three worker nodes.</span></span>

    <span data-ttu-id="cb500-125">此範本會為 Kafka 和 Spark 建立 HDInsight 3.6 叢集。</span><span class="sxs-lookup"><span data-stu-id="cb500-125">This template creates an HDInsight 3.6 cluster for both Kafka and Spark.</span></span>

2. <span data-ttu-id="cb500-126">使用下列資訊 toopopulate hello 項目上 hello 的 hello**自訂部署**刀鋒視窗中：</span><span class="sxs-lookup"><span data-stu-id="cb500-126">Use hello following information toopopulate hello entries on hello **Custom deployment** blade:</span></span>
   
    ![HDInsight 自訂部署](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="cb500-128">**資源群組**：建立群組或選取現有的群組。</span><span class="sxs-lookup"><span data-stu-id="cb500-128">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="cb500-129">此群組包含 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="cb500-129">This group contains hello HDInsight cluster.</span></span>

    * <span data-ttu-id="cb500-130">**位置**： 選取位置的地理位置關閉 tooyou。</span><span class="sxs-lookup"><span data-stu-id="cb500-130">**Location**: Select a location geographically close tooyou.</span></span>

    * <span data-ttu-id="cb500-131">**基底叢集名稱**: hello Spark 和 Kafka 叢集 hello 基底名稱為使用此值。</span><span class="sxs-lookup"><span data-stu-id="cb500-131">**Base Cluster Name**: This value is used as hello base name for hello Spark and Kafka clusters.</span></span> <span data-ttu-id="cb500-132">例如，輸入 **hdi** 可建立名為 spark-hdi__ 的 Spark 叢集以及名為 **kafka-hdi** 的 Kafka 叢集。</span><span class="sxs-lookup"><span data-stu-id="cb500-132">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="cb500-133">**叢集登入使用者名稱**: hello Spark 和 Kafka 叢集 hello 系統管理員使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="cb500-133">**Cluster Login User Name**: hello admin user name for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="cb500-134">**叢集登入密碼**: hello Spark 和 Kafka 叢集 hello 管理使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="cb500-134">**Cluster Login Password**: hello admin user password for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="cb500-135">**SSH 使用者名稱**: hello SSH 使用者 toocreate hello Spark 和 Kafka 叢集。</span><span class="sxs-lookup"><span data-stu-id="cb500-135">**SSH User Name**: hello SSH user toocreate for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="cb500-136">**SSH 密碼**: hello hello Spark 和 Kafka 叢集的 hello SSH 使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="cb500-136">**SSH Password**: hello password for hello SSH user for hello Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="cb500-137">讀取 hello**條款和條件**，然後選取**toohello 條款和條件前面所述，即表示我同意**。</span><span class="sxs-lookup"><span data-stu-id="cb500-137">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="cb500-138">最後，檢查**Pin toodashboard** ，然後選取 **購買**。</span><span class="sxs-lookup"><span data-stu-id="cb500-138">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="cb500-139">它會採用約 20 分鐘 toocreate hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="cb500-139">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="cb500-140">一旦已建立 hello 資源，您已重新導向的 tooa 刀鋒視窗中的 hello 資源群組含有 hello 叢集和 web 儀表板。</span><span class="sxs-lookup"><span data-stu-id="cb500-140">Once hello resources have been created, you are redirected tooa blade for hello resource group that contains hello clusters and web dashboard.</span></span>

![Hello vnet 與叢集資源群組 刀鋒視窗](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="cb500-142">請注意，hello hello HDInsight 叢集名稱**spark BASENAME**和**kafka BASENAME**，其中 BASENAME 是 hello 提供 toohello 範本的名稱。</span><span class="sxs-lookup"><span data-stu-id="cb500-142">Notice that hello names of hello HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="cb500-143">連接 toohello 叢集時，您可以使用在稍後步驟中的這些名稱。</span><span class="sxs-lookup"><span data-stu-id="cb500-143">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="use-hello-notebooks"></a><span data-ttu-id="cb500-144">使用 hello 筆記本</span><span class="sxs-lookup"><span data-stu-id="cb500-144">Use hello notebooks</span></span>

<span data-ttu-id="cb500-145">這份文件中所述的 hello 範例的 hello 程式碼將會位於[https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka)。</span><span class="sxs-lookup"><span data-stu-id="cb500-145">hello code for hello example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span></span>

<span data-ttu-id="cb500-146">Hello 中的 hello 步驟`README.md`檔案 toocomplete 這個範例。</span><span class="sxs-lookup"><span data-stu-id="cb500-146">Follow hello steps in hello `README.md` file toocomplete this example.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="cb500-147">刪除 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="cb500-147">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="cb500-148">因為這份文件中的 hello 步驟建立這兩者中的叢集 hello 相同的 Azure 資源群組，您可以刪除 hello hello Azure 入口網站中的資源群組。</span><span class="sxs-lookup"><span data-stu-id="cb500-148">Since hello steps in this document create both clusters in hello same Azure resource group, you can delete hello resource group in hello Azure portal.</span></span> <span data-ttu-id="cb500-149">正在刪除 hello 群組移除依照此文件、 hello Azure 虛擬網路和 hello 叢集所使用的儲存體帳戶建立的所有資源。</span><span class="sxs-lookup"><span data-stu-id="cb500-149">Deleting hello group removes all resources created by following this document, hello Azure Virtual Network, and storage account used by hello clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb500-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cb500-150">Next steps</span></span>

<span data-ttu-id="cb500-151">在此範例中，您將學會如何 toouse 二手 tooread 和撰寫 tooKafka。</span><span class="sxs-lookup"><span data-stu-id="cb500-151">In this example, you learned how toouse Spark tooread and write tooKafka.</span></span> <span data-ttu-id="cb500-152">使用下列連結 toodiscover hello 其他方式 toowork 與 Kafka:</span><span class="sxs-lookup"><span data-stu-id="cb500-152">Use hello following links toodiscover other ways toowork with Kafka:</span></span>

* [<span data-ttu-id="cb500-153">開始使用 Apache Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb500-153">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="cb500-154">在 HDInsight 上使用 MirrorMaker toocreate Kafka 的複本</span><span class="sxs-lookup"><span data-stu-id="cb500-154">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="cb500-155">使用 Apache Storm 搭配 HDInsight 上的 Kafka</span><span class="sxs-lookup"><span data-stu-id="cb500-155">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

