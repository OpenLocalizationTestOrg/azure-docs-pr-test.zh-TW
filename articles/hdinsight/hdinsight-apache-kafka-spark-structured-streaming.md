---
title: "搭配 Kafka 進行 Apache Spark 結構化串流 - Azure HDInsight | Microsoft Docs"
description: "了解如何使用 Apache Spark 串流 (DStream) 將資料傳入或傳出 Apache Kafka。 在此範例中，您使用 Jupyter Notebook 從 HDInsight 上的 Spark 串流資料。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/09/2017
ms.author: larryfr
ms.openlocfilehash: 02b49e13e8f54c3d55310f4d2b21c7e09c91fe81
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-spark-structured-streaming-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="d1c20-104">搭配 HDInsight 上的 Kafka (預覽) 使用 Spark 結構化串流</span><span class="sxs-lookup"><span data-stu-id="d1c20-104">Use Spark Structured Streaming with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="d1c20-105">了解如何使用 Spark 結構化串流，從 Azure HDInsight 上的 Apache Kafka 讀取資料。</span><span class="sxs-lookup"><span data-stu-id="d1c20-105">Learn how to use Spark Structured Streaming to read data from Apache Kafka on Azure HDInsight.</span></span>

<span data-ttu-id="d1c20-106">Spark 結構化串流是建置在 Spark SQL 上的串流處理引擎。</span><span class="sxs-lookup"><span data-stu-id="d1c20-106">Spark structured streaming is a stream processing engine built on Spark SQL.</span></span> <span data-ttu-id="d1c20-107">它允許您進行與靜態資料批次計算相同的串流計算。</span><span class="sxs-lookup"><span data-stu-id="d1c20-107">It allows you to express streaming computations the same as batch computation on static data.</span></span> <span data-ttu-id="d1c20-108">如需有關結構化串流的詳細資訊，請參閱 Apache.org 的[結構化串流程式設計手冊 [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="d1c20-108">For more information on Structured Streaming, see the [Structured Streaming Programming Guide [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) at Apache.org.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d1c20-109">此範例使用 HDInsight 3.6 上的 Spark 2.1。</span><span class="sxs-lookup"><span data-stu-id="d1c20-109">This example used Spark 2.1 on HDInsight 3.6.</span></span> <span data-ttu-id="d1c20-110">結構化串流在 Spark 2.1 上會視為 __alpha__。</span><span class="sxs-lookup"><span data-stu-id="d1c20-110">Structured Streaming is considered __alpha__ on Spark 2.1.</span></span>
>
> <span data-ttu-id="d1c20-111">本文件中的步驟建立 Azure 資源群組，其中包含 HDInsight 上的 Spark 和 HDInsight 叢集上的 Kafka。</span><span class="sxs-lookup"><span data-stu-id="d1c20-111">The steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="d1c20-112">這兩個叢集都位於 Azure 虛擬網路中，可讓 Spark 叢集直接與 Kafka 叢集通訊。</span><span class="sxs-lookup"><span data-stu-id="d1c20-112">These clusters are both located within an Azure Virtual Network, which allows the Spark cluster to directly communicate with the Kafka cluster.</span></span>
>
> <span data-ttu-id="d1c20-113">當您完成本文件中的步驟時，請記得刪除叢集，以避免產生過多的費用。</span><span class="sxs-lookup"><span data-stu-id="d1c20-113">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span></span>

## <a name="create-the-clusters"></a><span data-ttu-id="d1c20-114">建立叢集</span><span class="sxs-lookup"><span data-stu-id="d1c20-114">Create the clusters</span></span>

<span data-ttu-id="d1c20-115">Apache Kafka on HDInsight 不提供透過公用網際網路存取 Kafka 訊息代理程式。</span><span class="sxs-lookup"><span data-stu-id="d1c20-115">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span></span> <span data-ttu-id="d1c20-116">任何 Kafka 相關項目必須位於與 Kafka 叢集中節點相同的 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d1c20-116">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="d1c20-117">例如，Kafka 和 Spark 叢集均位於 Azure 虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="d1c20-117">For this example, both the Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="d1c20-118">下圖顯示叢集之間的通訊流動方式︰</span><span class="sxs-lookup"><span data-stu-id="d1c20-118">The following diagram shows how communication flows between the clusters:</span></span>

![Azure 虛擬網路中的 Spark 和 Kafka 叢集圖表](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="d1c20-120">Kafka 服務僅限於虛擬網路內的通訊。</span><span class="sxs-lookup"><span data-stu-id="d1c20-120">The Kafka service is limited to communication within the virtual network.</span></span> <span data-ttu-id="d1c20-121">叢集上的其他服務 (例如 SSH 和 Ambari) 可以透過網際網路存取。</span><span class="sxs-lookup"><span data-stu-id="d1c20-121">Other services on the cluster, such as SSH and Ambari, can be accessed over the internet.</span></span> <span data-ttu-id="d1c20-122">如需有關適用於 HDInsight 的公用連接埠詳細資訊，請參閱 [HDInsight 所使用的連接埠和 URI](hdinsight-hadoop-port-settings-for-services.md)。</span><span class="sxs-lookup"><span data-stu-id="d1c20-122">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="d1c20-123">雖然您可以手動建立 Azure 虛擬網路、Kafka 和 Spark 叢集，但使用 Azure Resource Manager 範本更輕鬆。</span><span class="sxs-lookup"><span data-stu-id="d1c20-123">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="d1c20-124">使用下列步驟將 Azure 虛擬網路、Kafka 和 Spark 叢集部署到 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d1c20-124">Use the following steps to deploy an Azure virtual network, Kafka, and Spark clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="d1c20-125">使用以下按鈕，在 Azure 入口網站中登入 Azure 並開啟範本。</span><span class="sxs-lookup"><span data-stu-id="d1c20-125">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v4.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy to Azure"></a>
    
    <span data-ttu-id="d1c20-126">Azure Resource Manager 範本位於 **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**。</span><span class="sxs-lookup"><span data-stu-id="d1c20-126">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span></span>

    <span data-ttu-id="d1c20-127">此範本會建立下列資源：</span><span class="sxs-lookup"><span data-stu-id="d1c20-127">This template creates the following resources:</span></span>

    * <span data-ttu-id="d1c20-128">HDInsight 3.5 叢集上的 Kafka。</span><span class="sxs-lookup"><span data-stu-id="d1c20-128">A Kafka on HDInsight 3.5 cluster.</span></span>
    * <span data-ttu-id="d1c20-129">HDInsight 3.6 叢集上的 Spark。</span><span class="sxs-lookup"><span data-stu-id="d1c20-129">A Spark on HDInsight 3.6 cluster.</span></span>
    * <span data-ttu-id="d1c20-130">Azure 虛擬網路，其中包含 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="d1c20-130">An Azure Virtual Network, which contains the HDInsight clusters.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d1c20-131">此範例中使用的結構化串流 Notebook 需要 HDInsight 3.6 上的 Spark。</span><span class="sxs-lookup"><span data-stu-id="d1c20-131">The structured streaming notebook used in this example requires Spark on HDInsight 3.6.</span></span> <span data-ttu-id="d1c20-132">如果您在 HDInsight 上使用較早版本的 Spark，當使用 Notebook 時會收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="d1c20-132">If you use an earlier version of Spark on HDInsight, you receive errors when using the notebook.</span></span>

2. <span data-ttu-id="d1c20-133">使用下列資訊來填入 [自訂部署] 刀鋒視窗上的項目︰</span><span class="sxs-lookup"><span data-stu-id="d1c20-133">Use the following information to populate the entries on the **Custom deployment** blade:</span></span>
   
    ![HDInsight 自訂部署](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="d1c20-135">**資源群組**：建立群組或選取現有的群組。</span><span class="sxs-lookup"><span data-stu-id="d1c20-135">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="d1c20-136">此群組包含 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="d1c20-136">This group contains the HDInsight cluster.</span></span>

    * <span data-ttu-id="d1c20-137">**位置**：選取在地理上靠近您的位置。</span><span class="sxs-lookup"><span data-stu-id="d1c20-137">**Location**: Select a location geographically close to you.</span></span>

    * <span data-ttu-id="d1c20-138">**基底叢集名稱**︰此值會做為 Spark 和 Kafka 叢集的基底名稱。</span><span class="sxs-lookup"><span data-stu-id="d1c20-138">**Base Cluster Name**: This value is used as the base name for the Spark and Kafka clusters.</span></span> <span data-ttu-id="d1c20-139">例如，輸入 **hdi** 可建立名為 spark-hdi__ 的 Spark 叢集以及名為 **kafka-hdi** 的 Kafka 叢集。</span><span class="sxs-lookup"><span data-stu-id="d1c20-139">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="d1c20-140">**叢集登入使用者名稱**：Spark 和 Kafka 叢集的系統管理員使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="d1c20-140">**Cluster Login User Name**: The admin user name for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="d1c20-141">**叢集登入密碼**：Spark 和 Kafka 叢集的系統管理員使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="d1c20-141">**Cluster Login Password**: The admin user password for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="d1c20-142">**SSH 使用者名稱**︰建立 Spark 和 Kafka 叢集的 SSH 使用者。</span><span class="sxs-lookup"><span data-stu-id="d1c20-142">**SSH User Name**: The SSH user to create for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="d1c20-143">**SSH 密碼**：Spark 和 Kafka 叢集的 SSH 使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="d1c20-143">**SSH Password**: The password for the SSH user for the Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="d1c20-144">讀取**條款及條件**，然後選取 [我同意上方所述的條款及條件]。</span><span class="sxs-lookup"><span data-stu-id="d1c20-144">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="d1c20-145">最後，核取 [釘選到儀表板]，然後選取 [購買]。</span><span class="sxs-lookup"><span data-stu-id="d1c20-145">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="d1c20-146">大約需要 20 分鐘的時間來建立叢集。</span><span class="sxs-lookup"><span data-stu-id="d1c20-146">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="d1c20-147">一旦建立資源，您會被重新導向至 [資源群組] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d1c20-147">Once the resources have been created, you are redirected to the resource group blade.</span></span>

![Vnet 和叢集的資源群組刀鋒視窗](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="d1c20-149">請注意，HDInsight 叢集的名稱是 **spark-BASENAME** 和 **kafka-BASENAME**，其中 BASENAME 是您提供給範本的名稱。</span><span class="sxs-lookup"><span data-stu-id="d1c20-149">Notice that the names of the HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="d1c20-150">連線到叢集時，您會在稍後步驟中使用這些名稱。</span><span class="sxs-lookup"><span data-stu-id="d1c20-150">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="get-the-kafka-brokers"></a><span data-ttu-id="d1c20-151">取得 Kafka 代理程式</span><span class="sxs-lookup"><span data-stu-id="d1c20-151">Get the Kafka brokers</span></span>

<span data-ttu-id="d1c20-152">在此範例中的程式碼會連線到 Kafka 叢集中的 Kafka 代理程式主機。</span><span class="sxs-lookup"><span data-stu-id="d1c20-152">The code in this example connects to the Kafka broker hosts in the Kafka cluster.</span></span> <span data-ttu-id="d1c20-153">若要尋找 Kafka 代理程式主機，請使用下列 PowerShell 或 Bash 範例：</span><span class="sxs-lookup"><span data-stu-id="d1c20-153">To find the Kafka broker hosts, use the following PowerShell or Bash example:</span></span>

```powershell
$creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
$clusterName = Read-Host -Prompt "Enter the Kafka cluster name"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$brokerHosts = $respObj.host_components.HostRoles.host_name
($brokerHosts -join ":9092,") + ":9092"
```

```bash
curl -u admin:$PASSWORD -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")'
```

> [!NOTE]
> <span data-ttu-id="d1c20-154">這個範例預期 `$PASSWORD` 包含叢集登入的密碼，而 `$CLUSTERNAME` 包含 Kafka 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="d1c20-154">This example expects `$PASSWORD` to contain the password for the cluster login, and `$CLUSTERNAME` to contain the name of the Kafka cluster.</span></span>
>
> <span data-ttu-id="d1c20-155">這個範例會使用 [jq](https://stedolan.github.io/jq/) 公用程式來剖析 JSON 文件中的資料。</span><span class="sxs-lookup"><span data-stu-id="d1c20-155">This example uses the [jq](https://stedolan.github.io/jq/) utility to parse data out of the JSON document.</span></span>

<span data-ttu-id="d1c20-156">輸出大致如下：</span><span class="sxs-lookup"><span data-stu-id="d1c20-156">The output is similar to the following text:</span></span>

`wn0-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn1-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn2-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn3-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092`

<span data-ttu-id="d1c20-157">儲存此資訊，因為它會在此文件中的以下各節中使用。</span><span class="sxs-lookup"><span data-stu-id="d1c20-157">Save this information, as it is used in the following sections of this document.</span></span>

## <a name="get-the-notebooks"></a><span data-ttu-id="d1c20-158">取得 Notebook</span><span class="sxs-lookup"><span data-stu-id="d1c20-158">Get the notebooks</span></span>

<span data-ttu-id="d1c20-159">在 [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming) 可取得此文件所述範例的程式碼。</span><span class="sxs-lookup"><span data-stu-id="d1c20-159">The code for the example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span></span>

## <a name="upload-the-notebooks"></a><span data-ttu-id="d1c20-160">上傳 Notebook</span><span class="sxs-lookup"><span data-stu-id="d1c20-160">Upload the notebooks</span></span>

<span data-ttu-id="d1c20-161">使用下列步驟，將專案中的 Notebook 上傳到您 HDInsight 叢集上的 Spark：</span><span class="sxs-lookup"><span data-stu-id="d1c20-161">Use the following steps to upload the notebooks from the project to your Spark on HDInsight cluster:</span></span>

1. <span data-ttu-id="d1c20-162">在網頁瀏覽器中，連線到您 Spark 叢集上的 Jupyter Notebook。</span><span class="sxs-lookup"><span data-stu-id="d1c20-162">In your web browser, connect to the Jupyter notebook on your Spark cluster.</span></span> <span data-ttu-id="d1c20-163">在下列 URL 中，使用您的 Kafka 叢集名稱取代 `CLUSTERNAME`：</span><span class="sxs-lookup"><span data-stu-id="d1c20-163">In the following URL, replace `CLUSTERNAME` with the name of your Kafka cluster:</span></span>

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    <span data-ttu-id="d1c20-164">出現提示時，輸入您在建立叢集時所使用的叢集登入 (admin) 和密碼。</span><span class="sxs-lookup"><span data-stu-id="d1c20-164">When prompted, enter the cluster login (admin) and password used when you created the cluster.</span></span>

2. <span data-ttu-id="d1c20-165">從頁面右上角，使用 [上傳] 按鈕將 __Stream-Tweets-To_Kafka.ipynb__ 檔案上傳到叢集。</span><span class="sxs-lookup"><span data-stu-id="d1c20-165">From the upper right side of the page, use the __Upload__ button to upload the __Stream-Tweets-To_Kafka.ipynb__ file to the cluster.</span></span> <span data-ttu-id="d1c20-166">選取 [開啟] 以開始上傳。</span><span class="sxs-lookup"><span data-stu-id="d1c20-166">Select __Open__ to start the upload.</span></span>

    ![使用上傳按鈕來選取和上傳 Notebook](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-button.png)

    ![選取 KafkaStreaming.ipynb 檔案](./media/hdinsight-apache-kafka-spark-structured-streaming/select-notebook.png)

3. <span data-ttu-id="d1c20-169">在 Notebook 清單中尋找 __Stream-Tweets-To_Kafka.ipynb__ 項目，並選取項目旁邊的 [上傳] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d1c20-169">Find the __Stream-Tweets-To_Kafka.ipynb__ entry in the list of notebooks, and select __Upload__ button beside it.</span></span>

    ![使用 KafkaStreaming.ipynb 項目旁邊的 [上傳] 按鈕，將它上傳至 Notebook 伺服器](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-notebook.png)

4. <span data-ttu-id="d1c20-171">重複步驟 1-3 以上傳 __Spark-Structured-Streaming-From-Kafka.ipynb__ Notebook。</span><span class="sxs-lookup"><span data-stu-id="d1c20-171">Repeat steps 1-3 to load the __Spark-Structured-Streaming-From-Kafka.ipynb__ notebook.</span></span>

## <a name="load-tweets-into-kafka"></a><span data-ttu-id="d1c20-172">將推文載入到 Kafka</span><span class="sxs-lookup"><span data-stu-id="d1c20-172">Load tweets into Kafka</span></span>

<span data-ttu-id="d1c20-173">一旦上傳檔案，選取 __Stream-Tweets-To_Kafka.ipynb__ 項目以開啟 Notebook。</span><span class="sxs-lookup"><span data-stu-id="d1c20-173">Once the files have been uploaded, select the __Stream-Tweets-To_Kafka.ipynb__ entry to open the notebook.</span></span> <span data-ttu-id="d1c20-174">請依照 Notebook 中的步驟，將推文載入到 Kafka。</span><span class="sxs-lookup"><span data-stu-id="d1c20-174">Follow the steps in the notebook to load tweets into Kafka.</span></span>

## <a name="process-tweets-using-spark-structured-streaming"></a><span data-ttu-id="d1c20-175">使用 Spark 結構化串流處理推文</span><span class="sxs-lookup"><span data-stu-id="d1c20-175">Process tweets using Spark Structured Streaming</span></span>

<span data-ttu-id="d1c20-176">從 Jupyter Notebook 首頁，選取 __Spark-Structured-Streaming-From-Kafka.ipynb__ 項目。</span><span class="sxs-lookup"><span data-stu-id="d1c20-176">From the Jupyter Notebook home page, select the __Spark-Structured-Streaming-From-Kafka.ipynb__ entry.</span></span> <span data-ttu-id="d1c20-177">請依照 Notebook 中的步驟，使用 Spark 結構化串流從 Kafka 載入推文。</span><span class="sxs-lookup"><span data-stu-id="d1c20-177">Follow the steps in the notebook to load tweets from Kafka using Spark Structured Streaming.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1c20-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d1c20-178">Next steps</span></span>

<span data-ttu-id="d1c20-179">既然您已經學會如何使用 Spark 結構化串流，請參閱下列文件，以深入了解有關使用 Spark 與 Kafka 的方式：</span><span class="sxs-lookup"><span data-stu-id="d1c20-179">Now that you have learned how to use Spark Structured Streaming, see the following documents to learn more about working with Spark and Kafka:</span></span>

* <span data-ttu-id="d1c20-180">[如何搭配 Kafka 使用 Spark 串流 (DStream)](hdinsight-apache-spark-with-kafka.md)。</span><span class="sxs-lookup"><span data-stu-id="d1c20-180">[How to use Spark streaming (DStream) with Kafka](hdinsight-apache-spark-with-kafka.md).</span></span>
* [<span data-ttu-id="d1c20-181">開始使用 Jupyter Notebook 與 HDInsight 上的 Spark</span><span class="sxs-lookup"><span data-stu-id="d1c20-181">Start with Jupyter Notebook and Spark on HDInsight</span></span>](hdinsight-apache-spark-jupyter-spark-sql.md)