---
title: "使用開放原始碼工具將 Azure 網路監看員 NSG 流量記錄視覺化 | Microsoft Docs"
description: "此頁面說明如何使用開放原始碼工具將 NSG 流量記錄視覺化。"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e9b2dcad-4da4-4d6b-aee2-6d0afade0cb8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 20f60ccd9108a7473705c2368f28d3152d0dd614
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-azure-network-watcher-nsg-flow-logs-using-open-source-tools"></a><span data-ttu-id="d0274-103">使用開放原始碼工具將 Azure 網路監看員 NSG 流量記錄視覺化</span><span class="sxs-lookup"><span data-stu-id="d0274-103">Visualize Azure Network Watcher NSG flow logs using open source tools</span></span>

<span data-ttu-id="d0274-104">網路安全性群組流量記錄提供的資訊可用於了解網路安全性群組上的輸入和輸出 IP 流量。</span><span class="sxs-lookup"><span data-stu-id="d0274-104">Network Security Group flow logs provide information that can be used understand ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="d0274-105">這些流量記錄顯示每一個規則的輸出和輸入流量、套用流量的 NIC、有關流量的 5 Tuple 資訊 (來源/目的地 IP、來源/目的地連接埠、通訊協定)，以及允許或拒絕流量。</span><span class="sxs-lookup"><span data-stu-id="d0274-105">These flow logs show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5 tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

<span data-ttu-id="d0274-106">這些流量記錄難以手動剖析和獲得見解。</span><span class="sxs-lookup"><span data-stu-id="d0274-106">These flow logs can be difficult to manually parse and gain insights from.</span></span> <span data-ttu-id="d0274-107">不過，有幾種開放原始碼工具可協助您將此資料視覺化。</span><span class="sxs-lookup"><span data-stu-id="d0274-107">However, there are several open source tools that can help visualize this data.</span></span> <span data-ttu-id="d0274-108">本文提供的解決方案使用「彈性堆疊」將這些記錄視覺化，該功能可讓您快速編製索引並以視覺化方式在 Kibana 儀表板上呈現流量記錄。</span><span class="sxs-lookup"><span data-stu-id="d0274-108">This article will provide a solution to visualize these logs using the Elastic Stack, which will allow you to quickly index and visualize your flow logs on a Kibana dashboard.</span></span>

## <a name="scenario"></a><span data-ttu-id="d0274-109">案例</span><span class="sxs-lookup"><span data-stu-id="d0274-109">Scenario</span></span>

<span data-ttu-id="d0274-110">在本文中，我們將設定一個解決方案，讓您使用「彈性堆疊」將網路安全性群組流量記錄視覺化。</span><span class="sxs-lookup"><span data-stu-id="d0274-110">In this article, we will set up a solution that will allow you to visualize Network Security Group flow logs using the Elastic Stack.</span></span>  <span data-ttu-id="d0274-111">Logstash 輸入外掛程式會直接從為了容納流量記錄而設定的儲存體 Blob 取得流量記錄。</span><span class="sxs-lookup"><span data-stu-id="d0274-111">A Logstash input plugin will obtain the flow logs directly from the storage blob configured for containing the flow logs.</span></span> <span data-ttu-id="d0274-112">然後，使用「彈性堆疊」，替流量記錄編製索引並用來建立 Kibana 儀表板，以將資訊視覺化。</span><span class="sxs-lookup"><span data-stu-id="d0274-112">Then, using the Elastic Stack, the flow logs will be indexed and used to create a Kibana dashboard to visualize the information.</span></span>

![案例][scenario]

## <a name="steps"></a><span data-ttu-id="d0274-114">步驟</span><span class="sxs-lookup"><span data-stu-id="d0274-114">Steps</span></span>

### <a name="enable-network-security-group-flow-logging"></a><span data-ttu-id="d0274-115">啟用網路安全性群組流量記錄</span><span class="sxs-lookup"><span data-stu-id="d0274-115">Enable Network Security Group flow logging</span></span>
<span data-ttu-id="d0274-116">在此案例中，您必須在您的帳戶中至少一個網路安全性群組上啟用「網路安全性群組流量記錄」。</span><span class="sxs-lookup"><span data-stu-id="d0274-116">For this scenario, you must have Network Security Group Flow Logging enabled on at least one Network Security Group in your account.</span></span> <span data-ttu-id="d0274-117">如需有關啟用網路安全性流量記錄的指示，請參閱下列文章︰[網路安全性群組的流量記錄簡介](network-watcher-nsg-flow-logging-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d0274-117">For instructions on enabling Network Security Flow Logs, refer to the following article [Introduction to flow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>


### <a name="set-up-the-elastic-stack"></a><span data-ttu-id="d0274-118">設定彈性堆疊</span><span class="sxs-lookup"><span data-stu-id="d0274-118">Set up the Elastic Stack</span></span>
<span data-ttu-id="d0274-119">藉由連線 NSG 流量記錄與彈性堆疊，我們可以建立 Kibana 儀表板，以便從記錄搜尋、繪圖、分析和洞察。</span><span class="sxs-lookup"><span data-stu-id="d0274-119">By connecting NSG flow logs with the Elastic Stack, we can create a Kibana dashboard what allows us to search, graph, analyze, and derive insights from our logs.</span></span>

#### <a name="install-elasticsearch"></a><span data-ttu-id="d0274-120">安裝 Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="d0274-120">Install Elasticsearch</span></span>

1. <span data-ttu-id="d0274-121">5.0 版和更新版本的彈性堆疊需要 Java 8。</span><span class="sxs-lookup"><span data-stu-id="d0274-121">The Elastic Stack from version 5.0 and above requires Java 8.</span></span> <span data-ttu-id="d0274-122">執行命令 `java -version` 來檢查您的版本。</span><span class="sxs-lookup"><span data-stu-id="d0274-122">Run the command `java -version` to check your version.</span></span> <span data-ttu-id="d0274-123">如果您沒有安裝 Java，請參閱 [Oracle 網站](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)上的文件</span><span class="sxs-lookup"><span data-stu-id="d0274-123">If you do not have java install, refer to documentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span></span>
1. <span data-ttu-id="d0274-124">針對您的系統下載正確的二進位套件︰</span><span class="sxs-lookup"><span data-stu-id="d0274-124">Download the correct binary package for your system:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    <span data-ttu-id="d0274-125">可在 [Elasticsearch 安裝](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)找到其他安裝方法</span><span class="sxs-lookup"><span data-stu-id="d0274-125">Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span></span>

1. <span data-ttu-id="d0274-126">使用下列命令確認 Elasticsearch 正在執行︰</span><span class="sxs-lookup"><span data-stu-id="d0274-126">Verify that Elasticsearch is running with the command:</span></span>

    ```
    curl http://127.0.0.1:9200
    ```

    <span data-ttu-id="d0274-127">您應該會看到如下所示的回應：</span><span class="sxs-lookup"><span data-stu-id="d0274-127">You should see a response similar to this:</span></span>

    ```
    {
    "name" : "Angela Del Toro",
    "cluster_name" : "elasticsearch",
    "version" : {
        "number" : "5.2.0",
        "build_hash" : "8ff36d139e16f8720f2947ef62c8167a888992fe",
        "build_timestamp" : "2016-01-27T13:32:39Z",
        "build_snapshot" : false,
        "lucene_version" : "6.1.0"
    },
    "tagline" : "You Know, for Search"
    }
    ```

<span data-ttu-id="d0274-128">如需安裝彈性搜尋的進一步指示，請參閱[安裝](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)頁面</span><span class="sxs-lookup"><span data-stu-id="d0274-128">For further instructions on installing Elastic search, refer to the page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span></span>

### <a name="install-logstash"></a><span data-ttu-id="d0274-129">安裝 Logstash</span><span class="sxs-lookup"><span data-stu-id="d0274-129">Install Logstash</span></span>

1. <span data-ttu-id="d0274-130">若要安裝 Logstash，請執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="d0274-130">To install Logstash run the following commands:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. <span data-ttu-id="d0274-131">接下來，我們必須設定 Logstash 以存取並剖析流量記錄。</span><span class="sxs-lookup"><span data-stu-id="d0274-131">Next we need to configure Logstash to access and parse the flow logs.</span></span> <span data-ttu-id="d0274-132">建立 logstash.conf 檔案，使用︰</span><span class="sxs-lookup"><span data-stu-id="d0274-132">Create a logstash.conf file using:</span></span>

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. <span data-ttu-id="d0274-133">將下列內容新增至檔案：</span><span class="sxs-lookup"><span data-stu-id="d0274-133">Add the following content to the file:</span></span>

  ```
    input {
      azureblob
        {
            storage_account_name => "mystorageaccount"
            storage_access_key => "storageaccesskey"
            container => "nsgflowlogContainerName"
            codec => "json"
        }
      }

      filter {
        split { field => "[records]" }
        split { field => "[records][properties][flows]"}
        split { field => "[records][properties][flows][flows]"}
        split { field => "[records][properties][flows][flows][flowTuples]"}

     mutate{
      split => { "[records][resourceId]" => "/"}
      add_field => {"Subscription" => "%{[records][resourceId][2]}"
                    "ResourceGroup" => "%{[records][resourceId][4]}"
                    "NetworkSecurityGroup" => "%{[records][resourceId][8]}"}
      convert => {"Subscription" => "string"}
      convert => {"ResourceGroup" => "string"}
      convert => {"NetworkSecurityGroup" => "string"}
      split => { "[records][properties][flows][flows][flowTuples]" => ","}
      add_field => {
                  "unixtimestamp" => "%{[records][properties][flows][flows][flowTuples][0]}"
                  "srcIp" => "%{[records][properties][flows][flows][flowTuples][1]}"
                  "destIp" => "%{[records][properties][flows][flows][flowTuples][2]}"
                  "srcPort" => "%{[records][properties][flows][flows][flowTuples][3]}"
                  "destPort" => "%{[records][properties][flows][flows][flowTuples][4]}"
                  "protocol" => "%{[records][properties][flows][flows][flowTuples][5]}"
                  "trafficflow" => "%{[records][properties][flows][flows][flowTuples][6]}"
                  "traffic" => "%{[records][properties][flows][flows][flowTuples][7]}"
                   }
      convert => {"unixtimestamp" => "integer"}
      convert => {"srcPort" => "integer"}
      convert => {"destPort" => "integer"}        
     }

     date{
       match => ["unixtimestamp" , "UNIX"]
     }
    }

    output {
      stdout { codec => rubydebug }
      elasticsearch {
        hosts => "localhost"
        index => "nsg-flow-logs"
      }
    }  

  ```

<span data-ttu-id="d0274-134">如需安裝 Logstash 的進一步指示，請參閱[正式文件](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span><span class="sxs-lookup"><span data-stu-id="d0274-134">For further instructions on installing Logstash, refer to the [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span></span>

### <a name="install-the-logstash-input-plugin-for-azure-blob-storage"></a><span data-ttu-id="d0274-135">安裝 Azure blob 儲存體的 Logstash 輸入外掛程式</span><span class="sxs-lookup"><span data-stu-id="d0274-135">Install the Logstash input plugin for Azure blob storage</span></span>

<span data-ttu-id="d0274-136">此 Logstash 外掛程式可讓您直接從流量記錄的指定儲存體帳戶存取它們。</span><span class="sxs-lookup"><span data-stu-id="d0274-136">This Logstash plugin will allow you to directly access the flow logs from their designated storage account.</span></span> <span data-ttu-id="d0274-137">若要安裝此外掛程式，請從預設的 Logstash 安裝目錄 (在此案例中為 /usr/share/logstash/bin) 執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="d0274-137">To install this plugin, from the default Logstash installation directory (in this case /usr/share/logstash/bin) run the command:</span></span>

```
logstash-plugin install logstash-input-azureblob
```

<span data-ttu-id="d0274-138">若要啟動 Logstash，請執行命令︰</span><span class="sxs-lookup"><span data-stu-id="d0274-138">To start Logstash run the command:</span></span>

```
sudo /etc/init.d/logstash start
```

<span data-ttu-id="d0274-139">如需此外掛程式的詳細資訊，請參閱[這裡 (英文)](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob) 的文件</span><span class="sxs-lookup"><span data-stu-id="d0274-139">For more information about this plugin, refer to documentation [here](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)</span></span>

### <a name="install-kibana"></a><span data-ttu-id="d0274-140">安裝 Kibana</span><span class="sxs-lookup"><span data-stu-id="d0274-140">Install Kibana</span></span>

1. <span data-ttu-id="d0274-141">執行下列命令以安裝 Kibana：</span><span class="sxs-lookup"><span data-stu-id="d0274-141">Run the following commands to install Kibana:</span></span>

  ```
  curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
  tar xzvf kibana-5.2.0-linux-x86_64.tar.gz
  ```

1. <span data-ttu-id="d0274-142">若要執行 Kibana，請使用這些命令︰</span><span class="sxs-lookup"><span data-stu-id="d0274-142">To run Kibana use the commands:</span></span>

  ```
  cd kibana-5.2.0-linux-x86_64/
  ./bin/kibana
  ```

1. <span data-ttu-id="d0274-143">若要檢視 Kibana Web 介面，請瀏覽至`http://localhost:5601`</span><span class="sxs-lookup"><span data-stu-id="d0274-143">To view your Kibana web interface, navigate to `http://localhost:5601`</span></span>
1. <span data-ttu-id="d0274-144">在此案例中，用於流量記錄的索引模式為 "nsg-flow-logs"。</span><span class="sxs-lookup"><span data-stu-id="d0274-144">For this scenario, the index pattern used for the flow logs is "nsg-flow-logs".</span></span> <span data-ttu-id="d0274-145">您可以變更 logstash.conf 檔案的 [輸出] 區段中的索引模式。</span><span class="sxs-lookup"><span data-stu-id="d0274-145">You may change the index pattern in the "output" section of your logstash.conf file.</span></span>

1. <span data-ttu-id="d0274-146">如果您想要從遠端檢視 Kibana 儀表板，建立輸入 NSG 規則以允許存取**連接埠 5601**。</span><span class="sxs-lookup"><span data-stu-id="d0274-146">If you want to view the Kibana dashboard remotely, create an inbound NSG rule allowing access to **port 5601**.</span></span>

### <a name="create-a-kibana-dashboard"></a><span data-ttu-id="d0274-147">建立 Kibana 儀表板</span><span class="sxs-lookup"><span data-stu-id="d0274-147">Create a Kibana dashboard</span></span>

<span data-ttu-id="d0274-148">在本文中，我們提供了範例儀表板，讓您檢視警示中的趨勢和詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d0274-148">For this article, we have provided a sample dashboard for you to view trends and details in your alerts.</span></span>

![圖 1][1]

1. <span data-ttu-id="d0274-150">下載儀表板檔案 ([這裡](https://aka.ms/networkwatchernsgflowlogdashboard))、視覺效果檔案 ([這裡](https://aka.ms/networkwatchernsgflowlogvisualizations))，以及儲存的搜尋檔案 ([這裡](https://aka.ms/networkwatchernsgflowlogsearch))。</span><span class="sxs-lookup"><span data-stu-id="d0274-150">Download the dashboard file [here](https://aka.ms/networkwatchernsgflowlogdashboard), the visualization file [here](https://aka.ms/networkwatchernsgflowlogvisualizations), and the saved search file [here](https://aka.ms/networkwatchernsgflowlogsearch).</span></span>

1. <span data-ttu-id="d0274-151">在 Kibana 的 [管理] 索引標籤下，瀏覽至 [儲存的物件] 並匯入這三個檔案。</span><span class="sxs-lookup"><span data-stu-id="d0274-151">Under the **Management** tab of Kibana, navigate to **Saved Objects** and import all three files.</span></span> <span data-ttu-id="d0274-152">然後您可以從 [儀表板] 索引標籤開啟並載入範例儀表板。</span><span class="sxs-lookup"><span data-stu-id="d0274-152">Then from the **Dashboard** tab you can open and load the sample dashboard.</span></span>

<span data-ttu-id="d0274-153">您也可以針對自己感興趣的計量，量身製作自己的視覺效果和儀表板。</span><span class="sxs-lookup"><span data-stu-id="d0274-153">You can also create your own visualizations and dashboards tailored towards metrics of your own interest.</span></span> <span data-ttu-id="d0274-154">從 Kibana 的[正式文件](https://www.elastic.co/guide/en/kibana/current/visualize.html)深入了解如何建立 Kibana 視覺效果。</span><span class="sxs-lookup"><span data-stu-id="d0274-154">Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span></span>

### <a name="visualize-nsg-flow-logs"></a><span data-ttu-id="d0274-155">將 NSG 流量記錄視覺化</span><span class="sxs-lookup"><span data-stu-id="d0274-155">Visualize NSG flow logs</span></span>

<span data-ttu-id="d0274-156">範例儀表板會提供流量記錄的數個視覺效果︰</span><span class="sxs-lookup"><span data-stu-id="d0274-156">The sample dashboard provides several visualizations of the flow logs:</span></span>

1. <span data-ttu-id="d0274-157">一段時間各決策/方向的流量 - 顯示一段期間內流量數目的時間序列圖。</span><span class="sxs-lookup"><span data-stu-id="d0274-157">Flows by Decision/Direction Over Time - time series graphs showing the number of flows over the time period.</span></span> <span data-ttu-id="d0274-158">您可以編輯這些視覺效果的時間單位和範圍。</span><span class="sxs-lookup"><span data-stu-id="d0274-158">You can edit the unit of time and span of both these visualizations.</span></span> <span data-ttu-id="d0274-159">「各決策的流量」顯示允許或拒絕所做決策的比例，而「各方向的流量」則顯示輸入和輸出流量的比例。</span><span class="sxs-lookup"><span data-stu-id="d0274-159">Flows by Decision shows the proportion of allow or deny decisions made, while Flows by Direction shows the proportion of inbound and outbound traffic.</span></span> <span data-ttu-id="d0274-160">使用這些視覺效果，您可以檢查一段時間的流量趨勢，並尋找任何突增狀況或不尋常的模式。</span><span class="sxs-lookup"><span data-stu-id="d0274-160">With these visuals you can examine traffic trends over time and look for any spikes or unusual patterns.</span></span>

  ![圖 2][2]

1. <span data-ttu-id="d0274-162">各目的地/來源連接埠的流量 – 圓形圖，可顯示個別連接埠的流量分解。</span><span class="sxs-lookup"><span data-stu-id="d0274-162">Flows by Destination/Source Port – pie charts showing the breakdown of flows to their respective ports.</span></span> <span data-ttu-id="d0274-163">在此檢視中，您可以查看最常使用的連接埠。</span><span class="sxs-lookup"><span data-stu-id="d0274-163">With this view you can see your most commonly used ports.</span></span> <span data-ttu-id="d0274-164">如果您按一下圓形圖內的特定連接埠，則儀表板的其餘部分會進一步篩選至該連接埠的流量。</span><span class="sxs-lookup"><span data-stu-id="d0274-164">If you click on a specific port within the pie chart, the rest of the dashboard will filter down to flows of that port.</span></span>

  ![圖 3][3]

1. <span data-ttu-id="d0274-166">流量數目和最早記錄時間 – 顯示已記錄流量數目和最舊記錄擷取日期之計量。</span><span class="sxs-lookup"><span data-stu-id="d0274-166">Number of Flows and Earliest Log Time – metrics showing you the number of flows recorded and the date of the earliest log captured.</span></span>

  ![圖 4][4]

1. <span data-ttu-id="d0274-168">各 NSG 和規則的流量 – 長條圖，可顯示每個 NSG 內的流量分布，以及每個 NSG 內的規則。</span><span class="sxs-lookup"><span data-stu-id="d0274-168">Flows by NSG and Rule – a bar graph showing you the distribution of flows within each NSG, as well as the distribution of rules within each NSG.</span></span> <span data-ttu-id="d0274-169">您可以在這裡查看哪些 NSG 和規則產生最多流量。</span><span class="sxs-lookup"><span data-stu-id="d0274-169">From here you can see which NSG and rules generated the most traffic.</span></span>

  ![圖 5][5]

1. <span data-ttu-id="d0274-171">前 10 個來源/目的地 IP – 長條圖，可顯示前 10 個來源和目的地 IP。</span><span class="sxs-lookup"><span data-stu-id="d0274-171">Top 10 Source/Destination IPs – bar charts showing the top 10 source and destination IPs.</span></span> <span data-ttu-id="d0274-172">您可以調整這些圖表以顯示更多或更少的 IP 排名。</span><span class="sxs-lookup"><span data-stu-id="d0274-172">You can adjust these charts to show more or less top IPs.</span></span> <span data-ttu-id="d0274-173">您可以在這裡查看最常出現的 IP，以及針對每個 IP 進行的流量決策 (允許或拒絕)。</span><span class="sxs-lookup"><span data-stu-id="d0274-173">From here you can see the most commonly occurring IPs as well as the traffic decision (allow or deny) being made towards each IP.</span></span>

  ![圖 6][6]

1. <span data-ttu-id="d0274-175">流量 Tuple – 下表顯示每個流量 Tuple 內含的資訊，以及其對應的 NGS 和規則。</span><span class="sxs-lookup"><span data-stu-id="d0274-175">Flow Tuples – this table shows you the information contained within each flow tuple, as well as its corresponding NGS and rule.</span></span>

  ![圖 7][7]

<span data-ttu-id="d0274-177">使用儀表板頂端的查詢列，您可以根據任何流量參數 (例如訂用帳戶識別碼、資源群組、規則或任何其他感興趣的變數)，進一步篩選儀表板。</span><span class="sxs-lookup"><span data-stu-id="d0274-177">Using the query bar at the top of the dashboard, you can filter down the dashboard based on any parameter of the flows, such as subscription ID, resource groups, rule, or any other variable of interest.</span></span> <span data-ttu-id="d0274-178">如需 Kibana 查詢與篩選器的詳細資訊，請參閱[正式文件](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)</span><span class="sxs-lookup"><span data-stu-id="d0274-178">For more about Kibana's queries and filters, refer to the [official documentation](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)</span></span>

## <a name="conclusion"></a><span data-ttu-id="d0274-179">結論</span><span class="sxs-lookup"><span data-stu-id="d0274-179">Conclusion</span></span>

<span data-ttu-id="d0274-180">結合網路安全性群組流量記錄與彈性堆疊，我們提供功能強大且可自訂的方式來將網路流量視覺化。</span><span class="sxs-lookup"><span data-stu-id="d0274-180">By combining the Network Security Group flow logs with the Elastic Stack, we have come up with powerful and customizable way to visualize our network traffic.</span></span> <span data-ttu-id="d0274-181">這些儀表板可讓您快速取得和分享您的網路流量深入解析，以及進一步篩選和調查任何潛在的異常狀況。</span><span class="sxs-lookup"><span data-stu-id="d0274-181">These dashboards allow you to quickly gain and share insights about your network traffic, as well as filter down and investigate on any potential anomalies.</span></span> <span data-ttu-id="d0274-182">您可以使用 Kibana 量身製作這些儀表板並建立特定視覺效果，以符合任何安全性、稽核和合規性需求。</span><span class="sxs-lookup"><span data-stu-id="d0274-182">Using Kibana, you can tailor these dashboards and create specific visualizations to meet any security, audit, and compliance needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0274-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d0274-183">Next steps</span></span>

<span data-ttu-id="d0274-184">若要了解如何利用 Power BI 將 NSG 流量記錄視覺化，請瀏覽[利用 Power BI 將 NSG 流量記錄視覺](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="d0274-184">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


<!--Image references-->

[scenario]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/scenario.png
[1]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure7.png
