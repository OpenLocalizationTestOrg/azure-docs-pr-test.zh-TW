---
title: "使用開放原始碼工具記錄檔的 Azure 網路監看員 NSG 流程 aaaVisualize |Microsoft 文件"
description: "此頁面描述 toouse 如何開啟來源工具 toovisualize NSG 流程記錄檔。"
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
ms.openlocfilehash: 47cb529d4a1e00e8c4c0fa6885cbf72aed3e74c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-azure-network-watcher-nsg-flow-logs-using-open-source-tools"></a><span data-ttu-id="43143-103">使用開放原始碼工具將 Azure 網路監看員 NSG 流量記錄視覺化</span><span class="sxs-lookup"><span data-stu-id="43143-103">Visualize Azure Network Watcher NSG flow logs using open source tools</span></span>

<span data-ttu-id="43143-104">網路安全性群組流量記錄提供的資訊可用於了解網路安全性群組上的輸入和輸出 IP 流量。</span><span class="sxs-lookup"><span data-stu-id="43143-104">Network Security Group flow logs provide information that can be used understand ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="43143-105">這些流程記錄檔會顯示輸出，以每個規則為基礎的輸入的流量，hello NIC hello 流程套，5 tuple 資訊 hello 流程 (來源/目的地 IP，來源/目的地連接埠通訊協定)，和如果允許或拒絕 hello 流量。</span><span class="sxs-lookup"><span data-stu-id="43143-105">These flow logs show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5 tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

<span data-ttu-id="43143-106">這些流程記錄檔可以是難以 toomanually 剖析，並從中獲得見解。</span><span class="sxs-lookup"><span data-stu-id="43143-106">These flow logs can be difficult toomanually parse and gain insights from.</span></span> <span data-ttu-id="43143-107">不過，有幾種開放原始碼工具可協助您將此資料視覺化。</span><span class="sxs-lookup"><span data-stu-id="43143-107">However, there are several open source tools that can help visualize this data.</span></span> <span data-ttu-id="43143-108">這篇文章會提供方案 toovisualize 使用 hello 彈性堆疊，以 tooquickly 索引可讓您，以視覺化方式檢視程式 Kibana 儀表板上的流量記錄這些記錄。</span><span class="sxs-lookup"><span data-stu-id="43143-108">This article will provide a solution toovisualize these logs using hello Elastic Stack, which will allow you tooquickly index and visualize your flow logs on a Kibana dashboard.</span></span>

## <a name="scenario"></a><span data-ttu-id="43143-109">案例</span><span class="sxs-lookup"><span data-stu-id="43143-109">Scenario</span></span>

<span data-ttu-id="43143-110">在本文中，我們將設定可讓您使用 hello 彈性堆疊 toovisualize 網路安全性小組流程記錄的解決方案。</span><span class="sxs-lookup"><span data-stu-id="43143-110">In this article, we will set up a solution that will allow you toovisualize Network Security Group flow logs using hello Elastic Stack.</span></span>  <span data-ttu-id="43143-111">Logstash 輸入的外掛程式會直接從 hello 設定為包含 hello 流程記錄檔的儲存體 blob 取得 hello 流程記錄檔。</span><span class="sxs-lookup"><span data-stu-id="43143-111">A Logstash input plugin will obtain hello flow logs directly from hello storage blob configured for containing hello flow logs.</span></span> <span data-ttu-id="43143-112">然後，使用 hello 彈性堆疊，hello 流程記錄檔會編製索引並使用 toocreate Kibana 儀表板 toovisualize hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="43143-112">Then, using hello Elastic Stack, hello flow logs will be indexed and used toocreate a Kibana dashboard toovisualize hello information.</span></span>

![案例][scenario]

## <a name="steps"></a><span data-ttu-id="43143-114">步驟</span><span class="sxs-lookup"><span data-stu-id="43143-114">Steps</span></span>

### <a name="enable-network-security-group-flow-logging"></a><span data-ttu-id="43143-115">啟用網路安全性群組流量記錄</span><span class="sxs-lookup"><span data-stu-id="43143-115">Enable Network Security Group flow logging</span></span>
<span data-ttu-id="43143-116">在此案例中，您必須在您的帳戶中至少一個網路安全性群組上啟用「網路安全性群組流量記錄」。</span><span class="sxs-lookup"><span data-stu-id="43143-116">For this scenario, you must have Network Security Group Flow Logging enabled on at least one Network Security Group in your account.</span></span> <span data-ttu-id="43143-117">如需有關啟用網路安全性流程記錄檔的指示，請參閱下列文章 toohello[網路安全性群組的簡介 tooflow 記錄](network-watcher-nsg-flow-logging-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="43143-117">For instructions on enabling Network Security Flow Logs, refer toohello following article [Introduction tooflow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>


### <a name="set-up-hello-elastic-stack"></a><span data-ttu-id="43143-118">設定彈性堆疊 hello</span><span class="sxs-lookup"><span data-stu-id="43143-118">Set up hello Elastic Stack</span></span>
<span data-ttu-id="43143-119">藉由連接 NSG hello 彈性堆疊的記錄檔，我們可以建立 Kibana 儀表板，讓我們 toosearch、 圖形、 分析和洞察從我們的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="43143-119">By connecting NSG flow logs with hello Elastic Stack, we can create a Kibana dashboard what allows us toosearch, graph, analyze, and derive insights from our logs.</span></span>

#### <a name="install-elasticsearch"></a><span data-ttu-id="43143-120">安裝 Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="43143-120">Install Elasticsearch</span></span>

1. <span data-ttu-id="43143-121">hello 彈性堆疊從 5.0 版和更新版本需要 Java 8。</span><span class="sxs-lookup"><span data-stu-id="43143-121">hello Elastic Stack from version 5.0 and above requires Java 8.</span></span> <span data-ttu-id="43143-122">執行 hello 命令`java -version`toocheck 您的版本。</span><span class="sxs-lookup"><span data-stu-id="43143-122">Run hello command `java -version` toocheck your version.</span></span> <span data-ttu-id="43143-123">如果您沒有安裝，請參閱 toodocumentation java [Oracle 的網站](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span><span class="sxs-lookup"><span data-stu-id="43143-123">If you do not have java install, refer toodocumentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span></span>
1. <span data-ttu-id="43143-124">下載 hello 二進位的正確封裝您的系統：</span><span class="sxs-lookup"><span data-stu-id="43143-124">Download hello correct binary package for your system:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    <span data-ttu-id="43143-125">可在 [Elasticsearch 安裝](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)找到其他安裝方法</span><span class="sxs-lookup"><span data-stu-id="43143-125">Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span></span>

1. <span data-ttu-id="43143-126">請確認 Elasticsearch 正以 hello 命令：</span><span class="sxs-lookup"><span data-stu-id="43143-126">Verify that Elasticsearch is running with hello command:</span></span>

    ```
    curl http://127.0.0.1:9200
    ```

    <span data-ttu-id="43143-127">您應該會看到回應類似 toothis:</span><span class="sxs-lookup"><span data-stu-id="43143-127">You should see a response similar toothis:</span></span>

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

<span data-ttu-id="43143-128">如需有關安裝彈性的搜尋的進一步指示，請參閱 toohello 頁面[安裝](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span><span class="sxs-lookup"><span data-stu-id="43143-128">For further instructions on installing Elastic search, refer toohello page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span></span>

### <a name="install-logstash"></a><span data-ttu-id="43143-129">安裝 Logstash</span><span class="sxs-lookup"><span data-stu-id="43143-129">Install Logstash</span></span>

1. <span data-ttu-id="43143-130">tooinstall Logstash 執行 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="43143-130">tooinstall Logstash run hello following commands:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. <span data-ttu-id="43143-131">接著，我們需要 tooconfigure Logstash tooaccess 及剖析 hello 流程記錄。</span><span class="sxs-lookup"><span data-stu-id="43143-131">Next we need tooconfigure Logstash tooaccess and parse hello flow logs.</span></span> <span data-ttu-id="43143-132">建立 logstash.conf 檔案，使用︰</span><span class="sxs-lookup"><span data-stu-id="43143-132">Create a logstash.conf file using:</span></span>

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. <span data-ttu-id="43143-133">加入下列內容 toohello 檔 hello:</span><span class="sxs-lookup"><span data-stu-id="43143-133">Add hello following content toohello file:</span></span>

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

<span data-ttu-id="43143-134">如需安裝 Logstash 的進一步指示，請參閱 toohello[官方文件集](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span><span class="sxs-lookup"><span data-stu-id="43143-134">For further instructions on installing Logstash, refer toohello [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span></span>

### <a name="install-hello-logstash-input-plugin-for-azure-blob-storage"></a><span data-ttu-id="43143-135">安裝 Azure blob 儲存體的 hello Logstash 輸入的外掛程式</span><span class="sxs-lookup"><span data-stu-id="43143-135">Install hello Logstash input plugin for Azure blob storage</span></span>

<span data-ttu-id="43143-136">此 Logstash 外掛程式可讓您 toodirectly 存取 hello 流程記錄檔從其指定的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="43143-136">This Logstash plugin will allow you toodirectly access hello flow logs from their designated storage account.</span></span> <span data-ttu-id="43143-137">tooinstall 此外掛程式中，從 hello 預設 Logstash （在此案例的 /usr/share/logstash/bin) 的安裝目錄執行 hello 命令：</span><span class="sxs-lookup"><span data-stu-id="43143-137">tooinstall this plugin, from hello default Logstash installation directory (in this case /usr/share/logstash/bin) run hello command:</span></span>

```
logstash-plugin install logstash-input-azureblob
```

<span data-ttu-id="43143-138">toostart Logstash 執行 hello 命令：</span><span class="sxs-lookup"><span data-stu-id="43143-138">toostart Logstash run hello command:</span></span>

```
sudo /etc/init.d/logstash start
```

<span data-ttu-id="43143-139">如需有關此外掛程式的詳細資訊，請參閱 toodocumentation[這裡](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)</span><span class="sxs-lookup"><span data-stu-id="43143-139">For more information about this plugin, refer toodocumentation [here](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)</span></span>

### <a name="install-kibana"></a><span data-ttu-id="43143-140">安裝 Kibana</span><span class="sxs-lookup"><span data-stu-id="43143-140">Install Kibana</span></span>

1. <span data-ttu-id="43143-141">執行下列命令 tooinstall Kibana hello:</span><span class="sxs-lookup"><span data-stu-id="43143-141">Run hello following commands tooinstall Kibana:</span></span>

  ```
  curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
  tar xzvf kibana-5.2.0-linux-x86_64.tar.gz
  ```

1. <span data-ttu-id="43143-142">toorun Kibana 使用 hello 命令：</span><span class="sxs-lookup"><span data-stu-id="43143-142">toorun Kibana use hello commands:</span></span>

  ```
  cd kibana-5.2.0-linux-x86_64/
  ./bin/kibana
  ```

1. <span data-ttu-id="43143-143">tooview Kibana web 介面，請瀏覽過`http://localhost:5601`</span><span class="sxs-lookup"><span data-stu-id="43143-143">tooview your Kibana web interface, navigate too`http://localhost:5601`</span></span>
1. <span data-ttu-id="43143-144">此案例中，用於 hello 流程記錄檔的 hello 索引模式是 「 nsg 流程-記錄檔 」。</span><span class="sxs-lookup"><span data-stu-id="43143-144">For this scenario, hello index pattern used for hello flow logs is "nsg-flow-logs".</span></span> <span data-ttu-id="43143-145">您可以變更 logstash.conf 檔案 hello 「 輸出 」 一節中的 hello 索引模式。</span><span class="sxs-lookup"><span data-stu-id="43143-145">You may change hello index pattern in hello "output" section of your logstash.conf file.</span></span>

1. <span data-ttu-id="43143-146">如果要從遠端 tooview hello Kibana 儀表板，請建立輸入的 NSG 規則允許存取太**連接埠 5601**。</span><span class="sxs-lookup"><span data-stu-id="43143-146">If you want tooview hello Kibana dashboard remotely, create an inbound NSG rule allowing access too**port 5601**.</span></span>

### <a name="create-a-kibana-dashboard"></a><span data-ttu-id="43143-147">建立 Kibana 儀表板</span><span class="sxs-lookup"><span data-stu-id="43143-147">Create a Kibana dashboard</span></span>

<span data-ttu-id="43143-148">如本文中，我們已提供為您 tooview 趨勢的範例儀表板和中的警示詳細資料。</span><span class="sxs-lookup"><span data-stu-id="43143-148">For this article, we have provided a sample dashboard for you tooview trends and details in your alerts.</span></span>

![圖 1][1]

1. <span data-ttu-id="43143-150">下載 hello 儀表板檔案[這裡](https://aka.ms/networkwatchernsgflowlogdashboard)，hello 視覺效果檔案[這裡](https://aka.ms/networkwatchernsgflowlogvisualizations)，和儲存的 hello 搜尋檔案[這裡](https://aka.ms/networkwatchernsgflowlogsearch)。</span><span class="sxs-lookup"><span data-stu-id="43143-150">Download hello dashboard file [here](https://aka.ms/networkwatchernsgflowlogdashboard), hello visualization file [here](https://aka.ms/networkwatchernsgflowlogvisualizations), and hello saved search file [here](https://aka.ms/networkwatchernsgflowlogsearch).</span></span>

1. <span data-ttu-id="43143-151">在 hello**管理** 索引標籤的 Kibana，瀏覽過**儲存物件**並匯入所有的三個檔案。</span><span class="sxs-lookup"><span data-stu-id="43143-151">Under hello **Management** tab of Kibana, navigate too**Saved Objects** and import all three files.</span></span> <span data-ttu-id="43143-152">然後從 hello**儀表板** 索引標籤，您可以開啟和負載 hello 範例儀表板。</span><span class="sxs-lookup"><span data-stu-id="43143-152">Then from hello **Dashboard** tab you can open and load hello sample dashboard.</span></span>

<span data-ttu-id="43143-153">您也可以針對自己感興趣的計量，量身製作自己的視覺效果和儀表板。</span><span class="sxs-lookup"><span data-stu-id="43143-153">You can also create your own visualizations and dashboards tailored towards metrics of your own interest.</span></span> <span data-ttu-id="43143-154">從 Kibana 的[正式文件](https://www.elastic.co/guide/en/kibana/current/visualize.html)深入了解如何建立 Kibana 視覺效果。</span><span class="sxs-lookup"><span data-stu-id="43143-154">Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span></span>

### <a name="visualize-nsg-flow-logs"></a><span data-ttu-id="43143-155">將 NSG 流量記錄視覺化</span><span class="sxs-lookup"><span data-stu-id="43143-155">Visualize NSG flow logs</span></span>

<span data-ttu-id="43143-156">hello 範例儀表板會提供數個視覺效果的 hello 流程記錄檔：</span><span class="sxs-lookup"><span data-stu-id="43143-156">hello sample dashboard provides several visualizations of hello flow logs:</span></span>

1. <span data-ttu-id="43143-157">流程決策/方向一段時間的時間序列圖形顯示 hello 時間週期的 hello 流程數目。</span><span class="sxs-lookup"><span data-stu-id="43143-157">Flows by Decision/Direction Over Time - time series graphs showing hello number of flows over hello time period.</span></span> <span data-ttu-id="43143-158">您可以編輯 hello 時間單位，而且這些視覺效果的範圍。</span><span class="sxs-lookup"><span data-stu-id="43143-158">You can edit hello unit of time and span of both these visualizations.</span></span> <span data-ttu-id="43143-159">流程決策顯示 hello 比例的允許或拒絕流量的輸入和輸出流量的方向顯示 hello 比例時所做的決定。</span><span class="sxs-lookup"><span data-stu-id="43143-159">Flows by Decision shows hello proportion of allow or deny decisions made, while Flows by Direction shows hello proportion of inbound and outbound traffic.</span></span> <span data-ttu-id="43143-160">使用這些視覺效果，您可以檢查一段時間的流量趨勢，並尋找任何突增狀況或不尋常的模式。</span><span class="sxs-lookup"><span data-stu-id="43143-160">With these visuals you can examine traffic trends over time and look for any spikes or unusual patterns.</span></span>

  ![圖 2][2]

1. <span data-ttu-id="43143-162">流程由目的地/來源的連接埠-圓形圖顯示 hello 分解的流量 tootheir 個別連接埠。</span><span class="sxs-lookup"><span data-stu-id="43143-162">Flows by Destination/Source Port – pie charts showing hello breakdown of flows tootheir respective ports.</span></span> <span data-ttu-id="43143-163">在此檢視中，您可以查看最常使用的連接埠。</span><span class="sxs-lookup"><span data-stu-id="43143-163">With this view you can see your most commonly used ports.</span></span> <span data-ttu-id="43143-164">如果您按一下 hello 圓形圖內的特定連接埠上，hello 儀表板的 hello rest 會篩選 tooflows 連接埠的清單。</span><span class="sxs-lookup"><span data-stu-id="43143-164">If you click on a specific port within hello pie chart, hello rest of hello dashboard will filter down tooflows of that port.</span></span>

  ![圖 3][3]

1. <span data-ttu-id="43143-166">流程和最早記錄時間 – 顯示您的流量 hello 數目記錄和 hello 最早的記錄檔的 hello 日期擷取度量的數目。</span><span class="sxs-lookup"><span data-stu-id="43143-166">Number of Flows and Earliest Log Time – metrics showing you hello number of flows recorded and hello date of hello earliest log captured.</span></span>

  ![圖 4][4]

1. <span data-ttu-id="43143-168">NSG 的規則-橫條圖，顯示您的流程中每個 NSG，hello 發佈，以及 hello 發佈中每個 NSG 規則的流量。</span><span class="sxs-lookup"><span data-stu-id="43143-168">Flows by NSG and Rule – a bar graph showing you hello distribution of flows within each NSG, as well as hello distribution of rules within each NSG.</span></span> <span data-ttu-id="43143-169">從這裡您可以看到哪些 NSG 及規則產生 hello 大部分的流量。</span><span class="sxs-lookup"><span data-stu-id="43143-169">From here you can see which NSG and rules generated hello most traffic.</span></span>

  ![圖 5][5]

1. <span data-ttu-id="43143-171">前 10 個來源/目的地 Ip – 顯示 hello 前 10 個來源和目的地 Ip 的橫條圖。</span><span class="sxs-lookup"><span data-stu-id="43143-171">Top 10 Source/Destination IPs – bar charts showing hello top 10 source and destination IPs.</span></span> <span data-ttu-id="43143-172">您可以調整這些圖表 tooshow 增加或減少最上層的 Ip。</span><span class="sxs-lookup"><span data-stu-id="43143-172">You can adjust these charts tooshow more or less top IPs.</span></span> <span data-ttu-id="43143-173">從這裡您可以查看最常進行 Ip hello 以及 hello 流量決策 （允許或拒絕） 進行向每個 IP。</span><span class="sxs-lookup"><span data-stu-id="43143-173">From here you can see hello most commonly occurring IPs as well as hello traffic decision (allow or deny) being made towards each IP.</span></span>

  ![圖 6][6]

1. <span data-ttu-id="43143-175">下表顯示您流程 Tuple – hello 中的每個流程 tuple，以及對應 NGS 和規則所包含的資訊。</span><span class="sxs-lookup"><span data-stu-id="43143-175">Flow Tuples – this table shows you hello information contained within each flow tuple, as well as its corresponding NGS and rule.</span></span>

  ![圖 7][7]

<span data-ttu-id="43143-177">使用 hello 查詢列在 hello hello 儀表板的頂端，您可以篩選向下 hello hello 的流量，例如訂用帳戶 ID、 資源群組、 規則或感興趣的任何其他變數的任何參數為基礎的儀表板。</span><span class="sxs-lookup"><span data-stu-id="43143-177">Using hello query bar at hello top of hello dashboard, you can filter down hello dashboard based on any parameter of hello flows, such as subscription ID, resource groups, rule, or any other variable of interest.</span></span> <span data-ttu-id="43143-178">如需詳細資訊 Kibana 的查詢和篩選，請參閱 toohello[官方文件集](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)</span><span class="sxs-lookup"><span data-stu-id="43143-178">For more about Kibana's queries and filters, refer toohello [official documentation](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)</span></span>

## <a name="conclusion"></a><span data-ttu-id="43143-179">結論</span><span class="sxs-lookup"><span data-stu-id="43143-179">Conclusion</span></span>

<span data-ttu-id="43143-180">藉由結合 hello 網路安全性小組流程記錄檔以 hello 彈性堆疊，我們已隨附於強大、 可自訂的方式 toovisualize 我們網路流量。</span><span class="sxs-lookup"><span data-stu-id="43143-180">By combining hello Network Security Group flow logs with hello Elastic Stack, we have come up with powerful and customizable way toovisualize our network traffic.</span></span> <span data-ttu-id="43143-181">這些儀表板 tooquickly 改善可讓您共用深入了解您的網路流量，以及篩選向下以及調查任何潛在的異常狀況。</span><span class="sxs-lookup"><span data-stu-id="43143-181">These dashboards allow you tooquickly gain and share insights about your network traffic, as well as filter down and investigate on any potential anomalies.</span></span> <span data-ttu-id="43143-182">使用 Kibana，您可以修改這些儀表板，並建立特定視覺效果 toomeet 任何安全性、 稽核及相容性的需求。</span><span class="sxs-lookup"><span data-stu-id="43143-182">Using Kibana, you can tailor these dashboards and create specific visualizations toomeet any security, audit, and compliance needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43143-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="43143-183">Next steps</span></span>

<span data-ttu-id="43143-184">了解 toovisualize NSG 流程記錄的方式有了 Power BI 瀏覽[視覺化 NSG 流動 Power BI 的記錄檔](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="43143-184">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


<!--Image references-->

[scenario]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/scenario.png
[1]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure7.png
