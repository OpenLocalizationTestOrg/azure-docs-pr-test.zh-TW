---
title: "透過 Kafka 串流的 Apache Spark - Azure HDInsight | Microsoft Docs"
description: "了解如何使用 DStreams 以 Spark Apache Spark 串流方式將資料送入或送出 Apache Kafka。 在此範例中，您使用 HDInsight 上之 Spark 的 Jupyter Notebook 來串流資料。"
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
ms.openlocfilehash: 81fa319f6fb94bdabacd8f68d14b9a1063a9749a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="apache-spark-streaming-dstream-example-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="6552e-105">在 HDInsight 上使用 Kafka 的 Apache Spark 串流 (DStream) 範例 (預覽)</span><span class="sxs-lookup"><span data-stu-id="6552e-105">Apache Spark streaming (DStream) example with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="6552e-106">了解如何在 HDInsight 上使用 DStreams，以 Spark Apache Spark 串流方式將資料送入或送出 Apache Kafka。</span><span class="sxs-lookup"><span data-stu-id="6552e-106">Learn how to use Spark Apache Spark to stream data into or out of Apache Kafka on HDInsight using DStreams.</span></span> <span data-ttu-id="6552e-107">這個範例會使用在 Spark 叢集上執行的 Jupyter Notebook。</span><span class="sxs-lookup"><span data-stu-id="6552e-107">This example uses a Jupyter notebook that runs on the Spark cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="6552e-108">本文件中的步驟建立 Azure 資源群組，其中包含 Spark on HDInsight 和 Kafka on HDInsight cluster 叢集。</span><span class="sxs-lookup"><span data-stu-id="6552e-108">The steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="6552e-109">這兩個叢集都位於 Azure 虛擬網路中，可讓 Spark 叢集直接與 Kafka 叢集通訊。</span><span class="sxs-lookup"><span data-stu-id="6552e-109">These clusters are both located within an Azure Virtual Network, which allows the Spark cluster to directly communicate with the Kafka cluster.</span></span>
>
> <span data-ttu-id="6552e-110">當您完成本文件中的步驟時，請記得刪除叢集，以避免產生過多的費用。</span><span class="sxs-lookup"><span data-stu-id="6552e-110">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span></span>

## <a name="create-the-clusters"></a><span data-ttu-id="6552e-111">建立叢集</span><span class="sxs-lookup"><span data-stu-id="6552e-111">Create the clusters</span></span>

<span data-ttu-id="6552e-112">Apache Kafka on HDInsight 不提供透過公用網際網路存取 Kafka 訊息代理程式。</span><span class="sxs-lookup"><span data-stu-id="6552e-112">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span></span> <span data-ttu-id="6552e-113">任何 Kafka 相關項目必須位於與 Kafka 叢集中節點相同的 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="6552e-113">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="6552e-114">例如，Kafka 和 Spark 叢集均位於 Azure 虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="6552e-114">For this example, both the Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="6552e-115">下圖顯示叢集之間的通訊流動方式︰</span><span class="sxs-lookup"><span data-stu-id="6552e-115">The following diagram shows how communication flows between the clusters:</span></span>

![Azure 虛擬網路中的 Spark 和 Kafka 叢集圖表](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="6552e-117">Kafka 本身受限於虛擬網路內的通訊，但叢集上的 SSH 和 Ambari 等其他服務可以透過網際網路存取。</span><span class="sxs-lookup"><span data-stu-id="6552e-117">Though Kafka itself is limited to communication within the virtual network, other services on the cluster such as SSH and Ambari can be accessed over the internet.</span></span> <span data-ttu-id="6552e-118">如需有關適用於 HDInsight 的公用連接埠詳細資訊，請參閱 [HDInsight 所使用的連接埠和 URI](hdinsight-hadoop-port-settings-for-services.md)。</span><span class="sxs-lookup"><span data-stu-id="6552e-118">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="6552e-119">雖然您可以手動建立 Azure 虛擬網路、Kafka 和 Spark 叢集，但使用 Azure Resource Manager 範本更輕鬆。</span><span class="sxs-lookup"><span data-stu-id="6552e-119">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="6552e-120">使用下列步驟將 Azure 虛擬網路、Kafka 和 Spark 叢集部署到 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6552e-120">Use the following steps to deploy an Azure virtual network, Kafka, and Spark clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="6552e-121">使用以下按鈕，在 Azure 入口網站中登入 Azure 並開啟範本。</span><span class="sxs-lookup"><span data-stu-id="6552e-121">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy to Azure"></a>
    
    <span data-ttu-id="6552e-122">Azure Resource Manager 範本位於 **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**。</span><span class="sxs-lookup"><span data-stu-id="6552e-122">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="6552e-123">若要保證 Kafka 在 HDInsight 上的可用性，您的叢集必須包含至少三個背景工作角色節點。</span><span class="sxs-lookup"><span data-stu-id="6552e-123">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="6552e-124">此範本會建立包含三個背景工作角色節點的 Kafka 叢集。</span><span class="sxs-lookup"><span data-stu-id="6552e-124">This template creates a Kafka cluster that contains three worker nodes.</span></span>

    <span data-ttu-id="6552e-125">此範本會為 Kafka 和 Spark 建立 HDInsight 3.6 叢集。</span><span class="sxs-lookup"><span data-stu-id="6552e-125">This template creates an HDInsight 3.6 cluster for both Kafka and Spark.</span></span>

2. <span data-ttu-id="6552e-126">使用下列資訊來填入 [自訂部署] 刀鋒視窗上的項目︰</span><span class="sxs-lookup"><span data-stu-id="6552e-126">Use the following information to populate the entries on the **Custom deployment** blade:</span></span>
   
    ![HDInsight 自訂部署](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="6552e-128">**資源群組**：建立群組或選取現有的群組。</span><span class="sxs-lookup"><span data-stu-id="6552e-128">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="6552e-129">此群組包含 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="6552e-129">This group contains the HDInsight cluster.</span></span>

    * <span data-ttu-id="6552e-130">**位置**：選取在地理上靠近您的位置。</span><span class="sxs-lookup"><span data-stu-id="6552e-130">**Location**: Select a location geographically close to you.</span></span>

    * <span data-ttu-id="6552e-131">**基底叢集名稱**︰此值會做為 Spark 和 Kafka 叢集的基底名稱。</span><span class="sxs-lookup"><span data-stu-id="6552e-131">**Base Cluster Name**: This value is used as the base name for the Spark and Kafka clusters.</span></span> <span data-ttu-id="6552e-132">例如，輸入 **hdi** 可建立名為 spark-hdi__ 的 Spark 叢集以及名為 **kafka-hdi** 的 Kafka 叢集。</span><span class="sxs-lookup"><span data-stu-id="6552e-132">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="6552e-133">**叢集登入使用者名稱**：Spark 和 Kafka 叢集的系統管理員使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="6552e-133">**Cluster Login User Name**: The admin user name for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="6552e-134">**叢集登入密碼**：Spark 和 Kafka 叢集的系統管理員使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="6552e-134">**Cluster Login Password**: The admin user password for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="6552e-135">**SSH 使用者名稱**︰建立 Spark 和 Kafka 叢集的 SSH 使用者。</span><span class="sxs-lookup"><span data-stu-id="6552e-135">**SSH User Name**: The SSH user to create for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="6552e-136">**SSH 密碼**：Spark 和 Kafka 叢集的 SSH 使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="6552e-136">**SSH Password**: The password for the SSH user for the Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="6552e-137">讀取**條款及條件**，然後選取 [我同意上方所述的條款及條件]。</span><span class="sxs-lookup"><span data-stu-id="6552e-137">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="6552e-138">最後，核取 [釘選到儀表板]，然後選取 [購買]。</span><span class="sxs-lookup"><span data-stu-id="6552e-138">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="6552e-139">大約需要 20 分鐘的時間來建立叢集。</span><span class="sxs-lookup"><span data-stu-id="6552e-139">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="6552e-140">建立資源後，您會重新導向至資源群組的刀鋒視窗，其中內含叢集和 Web 儀表板。</span><span class="sxs-lookup"><span data-stu-id="6552e-140">Once the resources have been created, you are redirected to a blade for the resource group that contains the clusters and web dashboard.</span></span>

![Vnet 和叢集的資源群組刀鋒視窗](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="6552e-142">請注意，HDInsight 叢集的名稱是 **spark-BASENAME** 和 **kafka-BASENAME**，其中 BASENAME 是您提供給範本的名稱。</span><span class="sxs-lookup"><span data-stu-id="6552e-142">Notice that the names of the HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="6552e-143">連接到叢集時，您會在稍後步驟中使用這些名稱。</span><span class="sxs-lookup"><span data-stu-id="6552e-143">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="use-the-notebooks"></a><span data-ttu-id="6552e-144">使用 Notebook</span><span class="sxs-lookup"><span data-stu-id="6552e-144">Use the notebooks</span></span>

<span data-ttu-id="6552e-145">在 [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka) 可取得本文件所述範例的程式碼。</span><span class="sxs-lookup"><span data-stu-id="6552e-145">The code for the example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span></span>

<span data-ttu-id="6552e-146">請依照 `README.md` 檔案中的步驟以完成此範例。</span><span class="sxs-lookup"><span data-stu-id="6552e-146">Follow the steps in the `README.md` file to complete this example.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="6552e-147">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="6552e-147">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="6552e-148">因為本文件中的步驟會在相同的 Azure 資源群組中建立兩個叢集，您可以在 Azure 入口網站中刪除資源群組。</span><span class="sxs-lookup"><span data-stu-id="6552e-148">Since the steps in this document create both clusters in the same Azure resource group, you can delete the resource group in the Azure portal.</span></span> <span data-ttu-id="6552e-149">刪除群組，即可移除依循本文件建立的所有資源、Azure 虛擬網路，以及叢集所使用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6552e-149">Deleting the group removes all resources created by following this document, the Azure Virtual Network, and storage account used by the clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6552e-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6552e-150">Next steps</span></span>

<span data-ttu-id="6552e-151">在此範例中，您已了解如何使用 Spark 來讀取和寫入至 Kafka。</span><span class="sxs-lookup"><span data-stu-id="6552e-151">In this example, you learned how to use Spark to read and write to Kafka.</span></span> <span data-ttu-id="6552e-152">使用下列連結來探索使用 Kafka 的其他方式︰</span><span class="sxs-lookup"><span data-stu-id="6552e-152">Use the following links to discover other ways to work with Kafka:</span></span>

* [<span data-ttu-id="6552e-153">開始使用 Apache Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="6552e-153">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="6552e-154">使用 MirrorMaker 建立 Apache Kafka on HDInsight 複本</span><span class="sxs-lookup"><span data-stu-id="6552e-154">Use MirrorMaker to create a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="6552e-155">使用 Apache Storm 搭配 Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="6552e-155">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

