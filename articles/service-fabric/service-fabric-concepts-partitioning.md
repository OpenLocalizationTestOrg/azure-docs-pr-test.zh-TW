---
title: "aaaPartitioning Service Fabric 服務 |Microsoft 文件"
description: "描述如何 toopartition Service Fabric 可設定狀態服務。 資料分割可讓 hello 本機電腦上的資料存放區，因此可以一起調整資料和計算。"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 3b7248c8-ea92-4964-85e7-6f1291b5cc7b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: msfussell
ms.openlocfilehash: 6ead48716c08f4212535202ee69d169067d5c6d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="partition-service-fabric-reliable-services"></a>分割 Service Fabric 可靠服務
本文章提供簡介 toohello Azure Service Fabric 可靠的服務資料分割基本的概念。 hello hello 發行項中使用的原始碼也會提供在[GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions)。

## <a name="partitioning"></a>分割
資料分割不是唯一 tooService 網狀架構。 事實上，它是建置可調整服務的核心模式。 更廣泛的意義而言，我們可以將資料分割除以狀態 （資料） 的概念來計算成較小的可存取的單位 tooimprove 延展性和效能。 [資料分割][wikipartition]是一種知名的分割形式，也稱為分區化。

### <a name="partition-service-fabric-stateless-services"></a>分割 Service Fabric 無狀態服務
對於無狀態服務，您可以將資料分割視為邏輯單元，其中包含服務的一個或多個執行個體。 圖 1 顯示無狀態服務有 5 個執行個體分散到使用一個資料分割的叢集。

![無狀態服務](./media/service-fabric-concepts-partitioning/statelessinstances.png)

實際上有兩種無狀態服務解決方案。 hello 第一次是一項服務，例如將外部而言，其狀態保存在 Azure SQL database （例如網站儲存 hello 工作階段資訊和資料）。 hello 第二個是僅限計算服務 （例如計算機或影像縮圖） 不會管理任何持續性的狀態。

在任一情況下，分割無狀態服務是很少見的情況，通常是藉由新增更多執行個體來達成延展性和可用性。 hello 時，才想的 tooconsider 無狀態的服務執行個體的多個資料分割是當您需要 toomeet 特殊路由要求。

例如，試想有一個情況，其中識別碼在某個範圍內的使用者應只由特定的服務執行個體來服務。 當您可以分割為無狀態服務的另一個範例時，具有真正的分割區的後端 (例如分區化 SQL database)，而且您想的 toocontrol 哪個服務執行個體應該寫入 toohello 資料庫分區-，或執行其他準備工作hello 無狀態服務，會要求 hello 相同 hello 後端中使用時，分割區資訊。 這幾種情況也可以透過不同方式解決，不一定需要服務分割。

本逐步解說的 hello 其餘部分著重於可設定狀態的服務。

### <a name="partition-service-fabric-stateful-services"></a>分割 Service Fabric 具狀態服務
Service Fabric 就可以輕鬆 toodevelop 可延展的可設定狀態服務供應項目第一級方式 toopartition 狀態 （資料）。 在概念上，您可以將有關資料分割的可設定狀態服務視為延展單位，是透過可靠[複本](service-fabric-availability-services.md)，散發並 hello 叢集中的節點之間取得平衡。

Service Fabric 可設定狀態服務 hello 內容中的資料分割是指 toohello 程序可決定特定服務資料分割負責 hello hello 服務完成狀態的一部分。 (如前所述，資料分割是一組[複本](service-fabric-availability-services.md))。 Service Fabric 最棒的一點是它會 hello 資料分割放在不同節點上。 這可讓它們 toogrow tooa 節點的資源限制。 Hello 資料需要成長，成長的資料分割，以及 Service Fabric 節點之間會重新平衡資料分割。 這可確保 hello 繼續有效率地使用硬體資源。

您需範例，您說 toogive 5 個節點叢集，而是已設定的 toohave 10 資料分割和三個複本的目標服務的啟動。 在此情況下，Service Fabric 會平衡 hello 複本分散 hello 叢集和您最後會出現兩個主要[複本](service-fabric-availability-services.md)每個節點。
如果您現在需要 tooscale hello 叢集 too10 節點時，Service Fabric 會重新平衡 hello 主要[複本](service-fabric-availability-services.md)10 的所有節點。 同樣地，如果您調整反向 too5 節點時，Service Fabric 會重新平衡所有 hello 複本 hello 5 節點之間。  

圖 2 顯示 hello 發佈的 10 個資料分割之前和之後調整 hello 叢集。

![具狀態服務](./media/service-fabric-concepts-partitioning/partitions.png)

如此一來，向外延展 hello 是因為來自用戶端要求會分散在電腦、 hello 應用程式的整體效能已獲得改善，而且會減少競爭資料的存取 toochunks 來達成。

## <a name="plan-for-partitioning"></a>規劃分割
之前實作的服務，您應該永遠考慮資料分割策略，是需要的 tooscale 出 hello。有不同的方式，但全部都著重於哪些 hello 應用程式需要 tooachieve。 Hello 這篇文章的內容，讓我們考慮某些 hello 更重要的層面。

一個好方法是 toothink hello 結構，需要進行資料分割，第一個步驟中 hello toobe hello 狀態的相關。

我們來看一個簡單的範例。 如果您 toobuild countywide 輪詢的服務，您可以建立 hello 郡中的每個城市的資料分割。 然後，您可以儲存的每個人的 hello 投票中對應 toothat 縣 （市） 的 hello 資料分割中的 hello 縣 （市）。 圖 3 說明一組的人員和 hello 所在的城市。

![簡單資料分割](./media/service-fabric-concepts-partitioning/cities.png)

因為 hello 母體擴展的城市變化很大，最後可能包含大量資料 （例如西雅圖） 的某些資料分割與極少的狀態 (例如 Kirkland) 與其他資料分割。 那麼 hello 影響的分割區不平均金額是狀態的什麼？

如果您認為 hello 範例需一次，可以輕鬆地查看保存 hello 投票數以供西雅圖的 hello 分割區會比其中一個 hello Kirkland 更多流量。 根據預設，Service Fabric 可確保沒有 hello 關於相同數目的每個節點上的主要和次要複本。 所以您最後可能是保存複本的一些節點處理有較多流量，而另外一些節點有較少流量。 您最好是想讓 tooavoid 熱，冷點以這種方式在叢集中。

在順序 tooavoid，您應該執行兩件事，從資料分割的觀點：

* 如此會平均分散到所有的資料分割，再試一次 toopartition hello 狀態。
* 報告負載從每個 hello 服務的 hello 複本。 (如需有關如何進行的資訊，請參閱[度量和負載](service-fabric-cluster-resource-manager-metrics.md)上的這篇文章)。 Service Fabric 提供服務，例如記憶體數量或記錄數目所耗用的 hello 功能 tooreport 負載。 根據報告的 hello 度量，Service Fabric 會偵測到某些資料分割正在提供更高的負載，比其他 hello 移動複本 toomore 適合節點，叢集會重新平衡，讓整體沒有節點多載。

有時候您不知道給定的資料分割中有多少資料。 一般建議是 toodo 這兩個-首先，採用資料分割策略，會將分散 hello 資料平均到 hello 資料分割和第二個，所報告的負載。  hello 第一種方法可避免述 hello 投票範例中，雖然 hello 第二個可協助存取或載入中暫存的差異變平滑經過一段時間的情況。

規劃磁碟分割的另一個層面是 toochoose hello 正確數目的資料分割 toobegin 與。
從 Service Fabric 的觀點來看，並不阻止您一開始就使用高於案例預期的資料分割數目。
事實上，假設 hello 資料分割數目上限是有效的方法。

在少數情況下，最後需要的磁碟分割可能比一開始選擇的數目更多。 當您無法變更 hello 資料分割計數 hello 事實之後，您將需要 tooapply 一些進階的資料分割方法，例如建立新的服務執行個體的 hello 相同服務類型。 您也需要的 tooimplement 路由傳送嗨某些用戶端邏輯要求 toohello 正確的服務執行個體，根據您的用戶端程式碼必須維護的用戶端知識。

規劃資料分割的另一個考量是 hello 可用的電腦資源。 為需要存取和儲存 toobe hello 狀態，您會繫結的 toofollow:

* 網路頻寬限制
* 系統記憶體限制
* 磁碟儲存體限制

因此怎樣若在執行中執行的叢集資源條件約束？hello 辦法就是，您可以直接向外延展 hello 叢集 tooaccommodate hello 新需求。

[hello 容量規劃指南](service-fabric-capacity-planning.md)提供的指導 toodetermine 您的叢集需要多少的節點。

## <a name="get-started-with-partitioning"></a>開始進行分割
本章節描述 tooget 中的資料分割您的服務的啟動方式。

Service Fabric 有三個資料分割配置可選擇：

* 範圍分割 (亦稱為 UniformInt64Partition)。
* 具名分割。 採用此模型的應用程式通常是在有界限集合內有可分割為值區的資料。 一些常見做為具名資料分割索引鍵的資料欄位範例包括區域、郵遞區號、客戶群組或其他商務界限。
* 單一分割。 單一資料分割通常用在 hello 服務不需要任何額外的路由。 例如，無狀態服務依預設使用此分割配置。

具名和單一分割配置是特殊形式的範圍資料分割。 根據預設，hello Visual Studio 範本，用於 Service Fabric 遠距資料分割，因為它是 hello 最常用與實用的一個。 hello 本文其餘部分著重於 hello 遠距的資料分割配置。

### <a name="ranged-partitioning-scheme"></a>範圍分割配置
這是使用的 toospecify 整數 （由低索引鍵，高索引鍵識別） 的範圍與資料分割 (n) 數目。 它會建立 n 個資料分割，分別負責非重疊子範圍的 hello 整體資料分割索引鍵範圍。 範例：具有低索引鍵 0、高索引鍵 99 及計數 4 的範圍分割配置，將會建立 4 個資料分割，如下所示。

![定界分割](./media/service-fabric-concepts-partitioning/range-partitioning.png)

常見的方法是 toocreate hello 資料集內的唯一索引鍵為基礎的雜湊。 索引鍵的某些常見範例可能是汽車識別號碼 (VIN)、員工識別碼或唯一字串。 藉由使用這個唯一索引鍵，您接著便會做為您的索引鍵產生雜湊程式碼、 模數 hello 索引鍵範圍、 toouse。 您可以指定 hello 上限和下限 hello 允許索引鍵範圍。

### <a name="select-a-hash-algorithm"></a>選取雜湊演算法
雜湊中的重要部分即為選取雜湊演算法。 考量是 hello 目標是否 toogroup （區域性機密雜湊）-彼此的附近的類似金鑰，或如果活動應該廣為散發的所有資料分割 （發佈雜湊），這是較常見。

hello 特性較佳分佈雜湊演算法是很容易 toocompute、 它有幾個衝突，和其平均發佈 hello 索引鍵。 有效率的雜湊演算法的理想範例為 hello [FNV 1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function)雜湊演算法。

如需一般的雜湊程式碼演算法的選擇是絕佳的資源為 hello[雜湊函式上的維基百科頁面](http://en.wikipedia.org/wiki/Hash_function)。

## <a name="build-a-stateful-service-with-multiple-partitions"></a>建置具有多個資料分割的具狀態服務
讓我們使用多個資料分割建立第一個可靠的具狀態服務。 在此範例中，您將建立非常簡單的應用程式，您想要 toostore 所有開頭之姓氏以字母 hello 中的相同的 hello 相同的資料分割。

撰寫任何程式碼之前，您會需要 toothink 需 hello 資料分割和資料分割索引鍵。 您需要什麼但 26 （一個 hello 字母中的每個字母），資料分割相關 hello 低和高索引鍵嗎？
字面意義，我們想要 toohave 字母每一個資料分割，我們可以使用 0 作為 hello 低索引鍵和 25 hello 高索引鍵，因為每個字母是它自己的金鑰。

> [!NOTE]
> 這是一個簡化的實例，因為事實上 hello 散發會以不平均。 最後一個名稱開頭為"S"或"M"會比 hello 的開頭為"X"更為常見 hello 字母或"Y"。
> 
> 

1. 開啟 [Visual Studio] > [檔案] > [新增] > [專案]。
2. 在 hello**新專案**對話方塊方塊中，選擇 hello Service Fabric 應用程式。
3. 呼叫 hello 專案 」 AlphabetPartitions"。
4. 在 hello**建立服務**對話方塊方塊中，選擇**可設定狀態**服務並呼叫 「 Alphabet.Processing"hello 圖所示。
       ![Visual Studio 中的新增服務對話方塊][1]

  <!--  ![Stateful service screenshot](./media/service-fabric-concepts-partitioning/createstateful.png)-->

5. 設定資料分割的 hello 數目。 開啟 hello Applicationmanifest.xml 檔案位於 hello ApplicationPackageRoot 資料夾 hello AlphabetPartitions 專案和更新 hello 參數 Processing_PartitionCount too26 如下所示。
   
    ```xml
    <Parameter Name="Processing_PartitionCount" DefaultValue="26" />
    ```
   
    您也需要 tooupdate hello LowKey 與 HighKey 項目的屬性 hello StatefulService 在 hello ApplicationManifest.xml 如下所示。
   
    ```xml
    <Service Name="Processing">
      <StatefulService ServiceTypeName="ProcessingType" TargetReplicaSetSize="[Processing_TargetReplicaSetSize]" MinReplicaSetSize="[Processing_MinReplicaSetSize]">
        <UniformInt64Partition PartitionCount="[Processing_PartitionCount]" LowKey="0" HighKey="25" />
      </StatefulService>
    </Service>
    ```
6. Hello 服務 toobe 存取，如開啟連接埠端點加入 hello 端點項目 （位於 hello 目錄資料夾） 的 ServiceManifest.xml 的 hello Alphabet.Processing 服務，如下所示：
   
    ```xml
    <Endpoint Name="ProcessingServiceEndpoint" Port="8089" Protocol="http" Type="Internal" />
    ```
   
    現在 hello 服務是設定的 toolisten tooan 內部端點具有 26 資料分割。
7. 接下來，您必須 toooverride hello `CreateServiceReplicaListeners()` hello 處理類別的方法。
   
   > [!NOTE]
   > 在這個範例中，我們假設您使用簡單的 HttpCommunicationListener。 如需可靠的服務通訊的詳細資訊，請參閱[hello 可靠的服務通訊模型](service-fabric-reliable-services-communication.md)。
   > 
   > 
8. 複本在上接聽的 hello url 建議的模式為下列格式的 hello: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`。
    因此您需要 tooconfigure 您通訊接聽程式 toolisten 在 hello 正確端點，並使用此模式。
   
    此服務的多個複本可能會裝載於 hello 同一部電腦，因此此位址必須 toobe 唯一 toohello 複本。 這是為什麼分割區識別碼 + 複本識別碼是 hello URL 中。 HttpListener 可以接聽相同通訊埠，只要 hello URL 前置詞是唯一的 hello 的多個地址。
   
    hello 進階案例，其中的次要複本也接聽的唯讀要求有額外的 GUID。 Hello 案例時，您會想 toomake 確定當轉換從主要 toosecondary tooforce 用戶端 toore 解析 hello 位址時，會使用新的唯一位址。 '+' hello 地址，以便 hello 複本在上接聽所有 IP、 FQDM、 localhost （等） 可用的主機 hello 下列程式碼範例示範當做。
   
    ```CSharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
         return new[] { new ServiceReplicaListener(context => this.CreateInternalListener(context))};
    }
    private ICommunicationListener CreateInternalListener(ServiceContext context)
    {
   
         EndpointResourceDescription internalEndpoint = context.CodePackageActivationContext.GetEndpoint("ProcessingServiceEndpoint");
         string uriPrefix = String.Format(
                "{0}://+:{1}/{2}/{3}-{4}/",
                internalEndpoint.Protocol,
                internalEndpoint.Port,
                context.PartitionId,
                context.ReplicaOrInstanceId,
                Guid.NewGuid());
   
         string nodeIP = FabricRuntime.GetNodeContext().IPAddressOrFQDN;
   
         string uriPublished = uriPrefix.Replace("+", nodeIP);
         return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInternalRequest);
    }
    ```
   
    另外值得注意的是該 hello 發行 URL 會稍有不同 hello 接聽的 URL 首碼。
    hello 接聽的 URL 會指定 tooHttpListener。 已發行的 URL 是 hello URL 是已發行的 toohello Service Fabric 命名服務，可用於服務探索，hello。 用戶端會透過該探索服務來要求這個位址。 用戶端取得需求 toohave hello 實際 IP 或 FQDN hello 節點的順序 tooconnect hello 位址。 因此您需要 tooreplace '+' 與 hello 節點的 IP 或 FQDN，示上述。
9. hello 最後一個步驟是 tooadd hello 處理邏輯 toohello 服務，如下所示。
   
    ```CSharp
    private async Task ProcessInternalRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        string output = null;
        string user = context.Request.QueryString["lastname"].ToString();
   
        try
        {
            output = await this.AddUserAsync(user);
        }
        catch (Exception ex)
        {
            output = ex.Message;
        }
   
        using (HttpListenerResponse response = context.Response)
        {
            if (output != null)
            {
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    private async Task<string> AddUserAsync(string user)
    {
        IReliableDictionary<String, String> dictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<String, String>>("dictionary");
   
        using (ITransaction tx = this.StateManager.CreateTransaction())
        {
            bool addResult = await dictionary.TryAddAsync(tx, user.ToUpperInvariant(), user);
   
            await tx.CommitAsync();
   
            return String.Format(
                "User {0} {1}",
                user,
                addResult ? "sucessfully added" : "already exists");
        }
    }
    ```
   
    `ProcessInternalRequest`讀取 hello hello 查詢字串參數使用 toocall hello 磁碟分割和呼叫值`AddUserAsync`tooadd hello lastname toohello 可靠字典`dictionary`。
10. 讓我們加入無狀態服務 toohello 專案 toosee 呼叫特定資料分割的方式。
    
    此服務可做為簡單的 web 介面，可接受 hello lastname 做為查詢字串參數，決定 hello 資料分割索引鍵，並將它傳送 toohello Alphabet.Processing 服務進行處理。
11. 在 hello**建立服務**對話方塊方塊中，選擇  **Stateless**服務並呼叫 「 Alphabet.Web"如下所示。
    
    ![無狀態服務螢幕擷取畫面](./media/service-fabric-concepts-partitioning/createnewstateless.png).
12. 更新 hello ServiceManifest.xml 中的 hello Alphabet.WebApi 服務 tooopen 埠，如下所示的 hello 端點資訊。
    
    ```xml
    <Endpoint Name="WebApiServiceEndpoint" Protocol="http" Port="8081"/>
    ```
13. 您需要 tooreturn hello 類別 Web 中 ServiceInstanceListeners 的集合。 同樣地，您可以選擇 tooimplement 簡單 HttpCommunicationListener。
    
    ```CSharp
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] {new ServiceInstanceListener(context => this.CreateInputListener(context))};
    }
    private ICommunicationListener CreateInputListener(ServiceContext context)
    {
        // Service instance's URL is hello node's IP & desired port
        EndpointResourceDescription inputEndpoint = context.CodePackageActivationContext.GetEndpoint("WebApiServiceEndpoint")
        string uriPrefix = String.Format("{0}://+:{1}/alphabetpartitions/", inputEndpoint.Protocol, inputEndpoint.Port);
        var uriPublished = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
        return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInputRequest);
    }
    ```
14. 現在您需要 tooimplement hello 處理邏輯。 hello HttpCommunicationListener 呼叫`ProcessInputRequest`當要求進入。 因此讓我們繼續並加入下列程式碼 hello。
    
    ```CSharp
    private async Task ProcessInputRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        String output = null;
        try
        {
            string lastname = context.Request.QueryString["lastname"];
            char firstLetterOfLastName = lastname.First();
            ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    
            ResolvedServicePartition partition = await this.servicePartitionResolver.ResolveAsync(alphabetServiceUri, partitionKey, cancelRequest);
            ResolvedServiceEndpoint ep = partition.GetEndpoint();
    
            JObject addresses = JObject.Parse(ep.Address);
            string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
            UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
            primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
            string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    
            output = String.Format(
                    "Result: {0}. <p>Partition key: '{1}' generated from hello first letter '{2}' of input value '{3}'. <br>Processing service partition ID: {4}. <br>Processing service replica address: {5}",
                    result,
                    partitionKey,
                    firstLetterOfLastName,
                    lastname,
                    partition.Info.Id,
                    primaryReplicaAddress);
        }
        catch (Exception ex) { output = ex.Message; }
    
        using (var response = context.Response)
        {
            if (output != null)
            {
                output = output + "added tooPartition: " + primaryReplicaAddress;
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    ```
    
    讓我們帶您逐步了解。 hello 程式碼會讀取 hello hello 查詢字串參數的第一個字母`lastname`成 char。 然後，它會判斷此代號 hello 資料分割索引鍵中減去 hello 十六進位值`A`hello 十六進位值中的 hello 姓氏的第一個字母。
    
    ```CSharp
    string lastname = context.Request.QueryString["lastname"];
    char firstLetterOfLastName = lastname.First();
    ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    ```
    
    請記得，在此範例中，我們使用 26 個資料分割，每個資料分割有一個資料分割索引鍵。
    接下來，我們會取得 hello 服務資料分割`partition`此索引鍵使用 hello`ResolveAsync`方法上 hello`servicePartitionResolver`物件。 `servicePartitionResolver` 定義為
    
    ```CSharp
    private readonly ServicePartitionResolver servicePartitionResolver = ServicePartitionResolver.GetDefault();
    ```
    
    hello`ResolveAsync`方法會採用 hello 服務 URI、 hello 資料分割索引鍵，以及取消語彙基元做為參數。 為處理服務的 hello hello 服務 URI `fabric:/AlphabetPartitions/Processing`。 接下來，我們取得 hello 資料分割的 hello 端點。
    
    ```CSharp
    ResolvedServiceEndpoint ep = partition.GetEndpoint()
    ```
    
    最後，我們會建置 hello 端點 URL 加上 hello querystring，並呼叫 hello 處理服務。
    
    ```CSharp
    JObject addresses = JObject.Parse(ep.Address);
    string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
    UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
    primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
    string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    ```
    
    一旦 hello 處理完成時，我們 hello 輸出回寫。
15. hello 最後一個步驟是 tootest hello 服務。 Visual Studio 會在本機和雲端部署中使用應用程式參數。 tootest hello 26 本機分割區的服務，您需要 tooupdate hello `Local.xml` hello ApplicationParameters hello AlphabetPartitions 專案資料夾中檔案，如下所示：
    
    ```xml
    <Parameters>
      <Parameter Name="Processing_PartitionCount" Value="26" />
      <Parameter Name="WebApi_InstanceCount" Value="1" />
    </Parameters>
    ```
16. 完成部署之後，您可以檢查 hello 服務和所有其 hello Service Fabric 總管中的資料分割。
    
    ![Service Fabric 總管螢幕擷取畫面](./media/service-fabric-concepts-partitioning/sfxpartitions.png)
17. 在瀏覽器中，您可以測試邏輯分割輸入 hello `http://localhost:8081/?lastname=somename`。 您會看到，各個姓氏開頭的 hello 相同的字母儲存在 hello 相同的資料分割。
    
    ![瀏覽器螢幕擷取畫面](./media/service-fabric-concepts-partitioning/samplerunning.png)

hello 範例 hello 整個原始程式碼位於[GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions)。

## <a name="next-steps"></a>後續步驟
如需 Service Fabric 概念資訊，請參閱 hello 下列：

* [Service Fabric 服務的可用性](service-fabric-availability-services.md)
* [Service Fabric 服務的延展性](service-fabric-concepts-scalability.md)
* [Service Fabric 應用程式的容量規劃](service-fabric-capacity-planning.md)

[wikipartition]: https://en.wikipedia.org/wiki/Partition_(database)

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png