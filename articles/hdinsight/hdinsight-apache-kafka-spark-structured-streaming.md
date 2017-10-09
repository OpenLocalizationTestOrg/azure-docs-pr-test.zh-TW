---
title: "aaaApache Spark 結構化以資料流處理 Kafka-Azure HDInsight |Microsoft 文件"
description: "深入了解如何 toouse Apache Spark 資料流 (DStream) tooget 資料傳入或傳出 Apache Kafka。 在此範例中，您使用 Jupyter Notebook 從 HDInsight 上的 Spark 串流資料。"
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
ms.openlocfilehash: 0837e8fc5ea314e644daed029d596feeb2b02c68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-spark-structured-streaming-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="a4641-104">搭配 HDInsight 上的 Kafka (預覽) 使用 Spark 結構化串流</span><span class="sxs-lookup"><span data-stu-id="a4641-104">Use Spark Structured Streaming with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="a4641-105">深入了解如何 toouse Apache Kafka Azure HDInsight 上的 Spark 結構化資料流 tooread 資料。</span><span class="sxs-lookup"><span data-stu-id="a4641-105">Learn how toouse Spark Structured Streaming tooread data from Apache Kafka on Azure HDInsight.</span></span>

<span data-ttu-id="a4641-106">Spark 結構化串流是建置在 Spark SQL 上的串流處理引擎。</span><span class="sxs-lookup"><span data-stu-id="a4641-106">Spark structured streaming is a stream processing engine built on Spark SQL.</span></span> <span data-ttu-id="a4641-107">它允許您 tooexpress 資料流計算 hello 與批次計算相同的靜態資料。</span><span class="sxs-lookup"><span data-stu-id="a4641-107">It allows you tooexpress streaming computations hello same as batch computation on static data.</span></span> <span data-ttu-id="a4641-108">如需有關結構化資料流處理的詳細資訊，請參閱 hello[結構化資料流程式設計手冊 [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) Apache.org 在。</span><span class="sxs-lookup"><span data-stu-id="a4641-108">For more information on Structured Streaming, see hello [Structured Streaming Programming Guide [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) at Apache.org.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a4641-109">此範例使用 HDInsight 3.6 上的 Spark 2.1。</span><span class="sxs-lookup"><span data-stu-id="a4641-109">This example used Spark 2.1 on HDInsight 3.6.</span></span> <span data-ttu-id="a4641-110">結構化串流在 Spark 2.1 上會視為 __alpha__。</span><span class="sxs-lookup"><span data-stu-id="a4641-110">Structured Streaming is considered __alpha__ on Spark 2.1.</span></span>
>
> <span data-ttu-id="a4641-111">本文件中的 hello 步驟建立包含 HDInsight 上的 Spark 以及 Kafka HDInsight 叢集上的 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="a4641-111">hello steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="a4641-112">這些叢集會同時位於 Azure 虛擬網路，可讓 hello Spark 叢集 toodirectly 與 hello Kafka 叢集通訊。</span><span class="sxs-lookup"><span data-stu-id="a4641-112">These clusters are both located within an Azure Virtual Network, which allows hello Spark cluster toodirectly communicate with hello Kafka cluster.</span></span>
>
> <span data-ttu-id="a4641-113">當您完成這份文件中的 hello 步驟之後時，請記得 toodelete hello 叢集 tooavoid 過多費用。</span><span class="sxs-lookup"><span data-stu-id="a4641-113">When you are done with hello steps in this document, remember toodelete hello clusters tooavoid excess charges.</span></span>

## <a name="create-hello-clusters"></a><span data-ttu-id="a4641-114">建立 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="a4641-114">Create hello clusters</span></span>

<span data-ttu-id="a4641-115">Apache Kafka HDInsight 上不提供存取 toohello Kafka broker 透過 hello 公用網際網路。</span><span class="sxs-lookup"><span data-stu-id="a4641-115">Apache Kafka on HDInsight does not provide access toohello Kafka brokers over hello public internet.</span></span> <span data-ttu-id="a4641-116">討論 tooKafka 必須在 hello 與 hello 節點中的相同 Azure 虛擬網路的任何項目 hello Kafka 叢集。</span><span class="sxs-lookup"><span data-stu-id="a4641-116">Anything that talks tooKafka must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="a4641-117">例如，hello Kafka 與 Spark 叢集位於 Azure 的虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="a4641-117">For this example, both hello Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="a4641-118">hello 下圖顯示 hello 叢集之間通訊流動的方式：</span><span class="sxs-lookup"><span data-stu-id="a4641-118">hello following diagram shows how communication flows between hello clusters:</span></span>

![Azure 虛擬網路中的 Spark 和 Kafka 叢集圖表](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="a4641-120">hello Kafka 服務是有限的 toocommunication hello 虛擬網路內。</span><span class="sxs-lookup"><span data-stu-id="a4641-120">hello Kafka service is limited toocommunication within hello virtual network.</span></span> <span data-ttu-id="a4641-121">例如，可以透過存取 SSH 和 Ambari hello 網際網路，hello 叢集上的其他服務。</span><span class="sxs-lookup"><span data-stu-id="a4641-121">Other services on hello cluster, such as SSH and Ambari, can be accessed over hello internet.</span></span> <span data-ttu-id="a4641-122">Hello 公用連接埠適用於 HDInsight 上的詳細資訊，請參閱[連接埠和 Uri 使用 HDInsight](hdinsight-hadoop-port-settings-for-services.md)。</span><span class="sxs-lookup"><span data-stu-id="a4641-122">For more information on hello public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="a4641-123">雖然您可以建立 Azure 虛擬網路，Kafka 和 Spark 叢集以手動方式，很容易 toouse Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="a4641-123">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="a4641-124">使用 hello 下列步驟 toodeploy Azure 虛擬網路，Kafka，，和 Spark 叢集 tooyour Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a4641-124">Use hello following steps toodeploy an Azure virtual network, Kafka, and Spark clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="a4641-125">使用下列按鈕 toosign 中 tooAzure 和開啟 hello 範本 hello Azure 入口網站中的 hello。</span><span class="sxs-lookup"><span data-stu-id="a4641-125">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v4.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    <span data-ttu-id="a4641-126">hello Azure Resource Manager 範本位於**https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**。</span><span class="sxs-lookup"><span data-stu-id="a4641-126">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span></span>

    <span data-ttu-id="a4641-127">此範本會建立 hello 下列資源：</span><span class="sxs-lookup"><span data-stu-id="a4641-127">This template creates hello following resources:</span></span>

    * <span data-ttu-id="a4641-128">HDInsight 3.5 叢集上的 Kafka。</span><span class="sxs-lookup"><span data-stu-id="a4641-128">A Kafka on HDInsight 3.5 cluster.</span></span>
    * <span data-ttu-id="a4641-129">HDInsight 3.6 叢集上的 Spark。</span><span class="sxs-lookup"><span data-stu-id="a4641-129">A Spark on HDInsight 3.6 cluster.</span></span>
    * <span data-ttu-id="a4641-130">Azure 虛擬網路，其中包含 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="a4641-130">An Azure Virtual Network, which contains hello HDInsight clusters.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="a4641-131">hello 結構化的資料流筆記本用於這個範例需要 HDInsight 3.6 上的 Spark。</span><span class="sxs-lookup"><span data-stu-id="a4641-131">hello structured streaming notebook used in this example requires Spark on HDInsight 3.6.</span></span> <span data-ttu-id="a4641-132">如果您在 HDInsight 上使用較早版本的 Spark，使用 hello 筆記本時收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="a4641-132">If you use an earlier version of Spark on HDInsight, you receive errors when using hello notebook.</span></span>

2. <span data-ttu-id="a4641-133">使用下列資訊 toopopulate hello 項目上 hello 的 hello**自訂部署**刀鋒視窗中：</span><span class="sxs-lookup"><span data-stu-id="a4641-133">Use hello following information toopopulate hello entries on hello **Custom deployment** blade:</span></span>
   
    ![HDInsight 自訂部署](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="a4641-135">**資源群組**：建立群組或選取現有的群組。</span><span class="sxs-lookup"><span data-stu-id="a4641-135">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="a4641-136">此群組包含 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="a4641-136">This group contains hello HDInsight cluster.</span></span>

    * <span data-ttu-id="a4641-137">**位置**： 選取位置的地理位置關閉 tooyou。</span><span class="sxs-lookup"><span data-stu-id="a4641-137">**Location**: Select a location geographically close tooyou.</span></span>

    * <span data-ttu-id="a4641-138">**基底叢集名稱**: hello Spark 和 Kafka 叢集 hello 基底名稱為使用此值。</span><span class="sxs-lookup"><span data-stu-id="a4641-138">**Base Cluster Name**: This value is used as hello base name for hello Spark and Kafka clusters.</span></span> <span data-ttu-id="a4641-139">例如，輸入 **hdi** 可建立名為 spark-hdi__ 的 Spark 叢集以及名為 **kafka-hdi** 的 Kafka 叢集。</span><span class="sxs-lookup"><span data-stu-id="a4641-139">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="a4641-140">**叢集登入使用者名稱**: hello Spark 和 Kafka 叢集 hello 系統管理員使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="a4641-140">**Cluster Login User Name**: hello admin user name for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="a4641-141">**叢集登入密碼**: hello Spark 和 Kafka 叢集 hello 管理使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="a4641-141">**Cluster Login Password**: hello admin user password for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="a4641-142">**SSH 使用者名稱**: hello SSH 使用者 toocreate hello Spark 和 Kafka 叢集。</span><span class="sxs-lookup"><span data-stu-id="a4641-142">**SSH User Name**: hello SSH user toocreate for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="a4641-143">**SSH 密碼**: hello hello Spark 和 Kafka 叢集的 hello SSH 使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="a4641-143">**SSH Password**: hello password for hello SSH user for hello Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="a4641-144">讀取 hello**條款和條件**，然後選取**toohello 條款和條件前面所述，即表示我同意**。</span><span class="sxs-lookup"><span data-stu-id="a4641-144">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="a4641-145">最後，檢查**Pin toodashboard** ，然後選取 **購買**。</span><span class="sxs-lookup"><span data-stu-id="a4641-145">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="a4641-146">它會採用約 20 分鐘 toocreate hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="a4641-146">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="a4641-147">一旦已建立 hello 資源，您已重新導向的 toohello 資源群組 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a4641-147">Once hello resources have been created, you are redirected toohello resource group blade.</span></span>

![Hello vnet 與叢集資源群組 刀鋒視窗](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="a4641-149">請注意，hello hello HDInsight 叢集名稱**spark BASENAME**和**kafka BASENAME**，其中 BASENAME 是 hello 提供 toohello 範本的名稱。</span><span class="sxs-lookup"><span data-stu-id="a4641-149">Notice that hello names of hello HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="a4641-150">連接 toohello 叢集時，您可以使用在稍後步驟中的這些名稱。</span><span class="sxs-lookup"><span data-stu-id="a4641-150">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="get-hello-kafka-brokers"></a><span data-ttu-id="a4641-151">取得 hello Kafka 代理程式</span><span class="sxs-lookup"><span data-stu-id="a4641-151">Get hello Kafka brokers</span></span>

<span data-ttu-id="a4641-152">hello 在此範例中的程式碼會連接 toohello Kafka broker hello Kafka 叢集中的主機。</span><span class="sxs-lookup"><span data-stu-id="a4641-152">hello code in this example connects toohello Kafka broker hosts in hello Kafka cluster.</span></span> <span data-ttu-id="a4641-153">toofind hello Kafka broker 主機，請使用下列 PowerShell 或 Bash 範例 hello:</span><span class="sxs-lookup"><span data-stu-id="a4641-153">toofind hello Kafka broker hosts, use hello following PowerShell or Bash example:</span></span>

```powershell
$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
$clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
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
> <span data-ttu-id="a4641-154">這個範例預期`$PASSWORD`toocontain hello hello 叢集登入，密碼和`$CLUSTERNAME`toocontain hello hello Kafka 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="a4641-154">This example expects `$PASSWORD` toocontain hello password for hello cluster login, and `$CLUSTERNAME` toocontain hello name of hello Kafka cluster.</span></span>
>
> <span data-ttu-id="a4641-155">這個範例會使用 hello [jq](https://stedolan.github.io/jq/) hello JSON 文件中的公用程式 tooparse 資料。</span><span class="sxs-lookup"><span data-stu-id="a4641-155">This example uses hello [jq](https://stedolan.github.io/jq/) utility tooparse data out of hello JSON document.</span></span>

<span data-ttu-id="a4641-156">hello 輸出是類似 toohello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="a4641-156">hello output is similar toohello following text:</span></span>

`wn0-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn1-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn2-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn3-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092`

<span data-ttu-id="a4641-157">儲存這項資訊，，因為它正使用 hello 下列各節的這份文件中。</span><span class="sxs-lookup"><span data-stu-id="a4641-157">Save this information, as it is used in hello following sections of this document.</span></span>

## <a name="get-hello-notebooks"></a><span data-ttu-id="a4641-158">取得 hello 筆記本</span><span class="sxs-lookup"><span data-stu-id="a4641-158">Get hello notebooks</span></span>

<span data-ttu-id="a4641-159">這份文件中所述的 hello 範例的 hello 程式碼將會位於[https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming)。</span><span class="sxs-lookup"><span data-stu-id="a4641-159">hello code for hello example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span></span>

## <a name="upload-hello-notebooks"></a><span data-ttu-id="a4641-160">上傳 hello 筆記本</span><span class="sxs-lookup"><span data-stu-id="a4641-160">Upload hello notebooks</span></span>

<span data-ttu-id="a4641-161">Hello 專案 tooyour Spark 中的下列步驟 tooupload hello 筆記本，HDInsight 叢集上使用 hello:</span><span class="sxs-lookup"><span data-stu-id="a4641-161">Use hello following steps tooupload hello notebooks from hello project tooyour Spark on HDInsight cluster:</span></span>

1. <span data-ttu-id="a4641-162">在您的 web 瀏覽器連接 toohello Jupyter 筆記本，您的 Spark 叢集上。</span><span class="sxs-lookup"><span data-stu-id="a4641-162">In your web browser, connect toohello Jupyter notebook on your Spark cluster.</span></span> <span data-ttu-id="a4641-163">在 hello 下列 URL，取代`CLUSTERNAME`hello Kafka 叢集名稱：</span><span class="sxs-lookup"><span data-stu-id="a4641-163">In hello following URL, replace `CLUSTERNAME` with hello name of your Kafka cluster:</span></span>

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    <span data-ttu-id="a4641-164">出現提示時，輸入 hello 叢集登入 （管理員） 和建立 hello 叢集時所使用的密碼。</span><span class="sxs-lookup"><span data-stu-id="a4641-164">When prompted, enter hello cluster login (admin) and password used when you created hello cluster.</span></span>

2. <span data-ttu-id="a4641-165">Hello 上方右側的 hello 頁面上，從使用 hello__上傳__按鈕 tooupload hello__資料流推文 To_Kafka.ipynb__檔案 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="a4641-165">From hello upper right side of hello page, use hello __Upload__ button tooupload hello __Stream-Tweets-To_Kafka.ipynb__ file toohello cluster.</span></span> <span data-ttu-id="a4641-166">選取__開啟__toostart hello 上傳。</span><span class="sxs-lookup"><span data-stu-id="a4641-166">Select __Open__ toostart hello upload.</span></span>

    ![使用 hello 上傳按鈕 tooselect 並上傳筆記本](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-button.png)

    ![選取 hello KafkaStreaming.ipynb 檔案](./media/hdinsight-apache-kafka-spark-structured-streaming/select-notebook.png)

3. <span data-ttu-id="a4641-169">尋找 hello__資料流推文 To_Kafka.ipynb__ hello 筆記型電腦，然後選取清單中的項目__上傳__旁邊的按鈕。</span><span class="sxs-lookup"><span data-stu-id="a4641-169">Find hello __Stream-Tweets-To_Kafka.ipynb__ entry in hello list of notebooks, and select __Upload__ button beside it.</span></span>

    ![使用 hello 上傳按鈕 hello KafkaStreaming.ipynb 項目 tooupload 它 toohello 筆記本伺服器](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-notebook.png)

4. <span data-ttu-id="a4641-171">重複步驟 1-3 tooload hello __Spark-結構化的資料流-從-Kafka.ipynb__筆記型電腦。</span><span class="sxs-lookup"><span data-stu-id="a4641-171">Repeat steps 1-3 tooload hello __Spark-Structured-Streaming-From-Kafka.ipynb__ notebook.</span></span>

## <a name="load-tweets-into-kafka"></a><span data-ttu-id="a4641-172">將推文載入到 Kafka</span><span class="sxs-lookup"><span data-stu-id="a4641-172">Load tweets into Kafka</span></span>

<span data-ttu-id="a4641-173">Hello 檔案已上傳，一旦選取 hello__資料流推文 To_Kafka.ipynb__項目 tooopen hello 筆記型電腦。</span><span class="sxs-lookup"><span data-stu-id="a4641-173">Once hello files have been uploaded, select hello __Stream-Tweets-To_Kafka.ipynb__ entry tooopen hello notebook.</span></span> <span data-ttu-id="a4641-174">到 Kafka 遵循 hello 筆記本 tooload 推文中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="a4641-174">Follow hello steps in hello notebook tooload tweets into Kafka.</span></span>

## <a name="process-tweets-using-spark-structured-streaming"></a><span data-ttu-id="a4641-175">使用 Spark 結構化串流處理推文</span><span class="sxs-lookup"><span data-stu-id="a4641-175">Process tweets using Spark Structured Streaming</span></span>

<span data-ttu-id="a4641-176">從 hello Jupyter 筆記本首頁上，選取 hello __Spark-結構化的資料流-從-Kafka.ipynb__項目。</span><span class="sxs-lookup"><span data-stu-id="a4641-176">From hello Jupyter Notebook home page, select hello __Spark-Structured-Streaming-From-Kafka.ipynb__ entry.</span></span> <span data-ttu-id="a4641-177">從 Kafka 使用 Spark 結構化資料流處理，請遵循 hello 筆記本 tooload 推文中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="a4641-177">Follow hello steps in hello notebook tooload tweets from Kafka using Spark Structured Streaming.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4641-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a4641-178">Next steps</span></span>

<span data-ttu-id="a4641-179">既然您已經學會如何 toouse Spark 結構化資料流，請參閱下列文件 toolearn 深入了解使用 Spark 和 Kafka hello:</span><span class="sxs-lookup"><span data-stu-id="a4641-179">Now that you have learned how toouse Spark Structured Streaming, see hello following documents toolearn more about working with Spark and Kafka:</span></span>

* <span data-ttu-id="a4641-180">[如何 toouse 二手串流 (DStream) 與 Kafka](hdinsight-apache-spark-with-kafka.md)。</span><span class="sxs-lookup"><span data-stu-id="a4641-180">[How toouse Spark streaming (DStream) with Kafka](hdinsight-apache-spark-with-kafka.md).</span></span>
* [<span data-ttu-id="a4641-181">開始使用 Jupyter Notebook 與 HDInsight 上的 Spark</span><span class="sxs-lookup"><span data-stu-id="a4641-181">Start with Jupyter Notebook and Spark on HDInsight</span></span>](hdinsight-apache-spark-jupyter-spark-sql.md)