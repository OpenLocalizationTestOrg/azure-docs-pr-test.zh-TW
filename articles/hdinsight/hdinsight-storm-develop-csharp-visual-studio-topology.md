---
title: "使用 Visual Studio 和 C#-Azure HDInsight aaaApache Storm 拓撲 |Microsoft 文件"
description: "深入了解如何在 C# toocreate Storm 拓撲。 Visual Studio 中建立簡單的單字計數拓撲使用 hello Hadoop tools for Visual Studio。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 380d804f-a8c5-4b20-9762-593ec4da5a0d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/02/2017
ms.author: larryfr
ms.openlocfilehash: b3fb01a4dda144fd7fb4141e624e31e667f93753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="develop-c-topologies-for-apache-storm-by-using-hello-data-lake-tools-for-visual-studio"></a>使用 hello Data Lake tools for Visual Studio 開發 Apache Storm 的 C# 拓撲

了解如何 toocreate 使用 hello Azure 資料湖 (Hadoop) 的 C# Storm 拓樸 tools for Visual Studio。 本文件逐步 hello Visual Studio 中建立 Storm 專案、 在本機測試和部署程序它 tooan Apache Storm Azure HDInsight 叢集上。

您也學到如何 toocreate 混合式拓撲中，使用 C# 和 Java 的元件。

> [!NOTE]
> 本文件中的 hello 步驟依賴 Windows 與 Visual Studio 開發環境，雖然 hello 已編譯的專案可以提交的 tooeither Linux 或 Windows 為基礎的 HDInsight 叢集。 只有在 2016 年 10 月 28 日之後所建立之以 Linux 為基礎的叢集可支援 SCP.NET 拓撲。

toouse C# 拓撲中使用以 Linux 為基礎的叢集，您必須更新 hello Microsoft.SCP.Net.SDK NuGet 封裝使用您的專案 tooversion 0.10.0.6 或更新版本。 hello hello 封裝版本也必須符合安裝在 HDInsight 上的 Storm hello 主要版本。

| HDInsight 版本 | Storm 版本 | SCP.NET 版本 | 預設 Mono 版本 |
|:-----------------:|:-------------:|:---------------:|:--------------------:|
| 3.3 |0.10.x |0.10.x.x</br>(僅限以 Windows 為基礎的 HDInsight) | NA |
| 3.4 | 0.10.0.x | 0.10.0.x | 3.2.8 |
| 3.5 | 1.0.2.x | 1.0.0.x | 4.2.1 |
| 3.6 | 1.1.0.x | 1.0.0.x | 4.2.8 |

> [!IMPORTANT]
> C# 拓撲以 Linux 為基礎的叢集上必須使用.NET 4.5，並使用單聲道 toorun hello HDInsight 叢集上。 查看 [Mono 相容性](http://www.mono-project.com/docs/about-mono/compatibility/) \(英文\) 以了解可能的不相容情形。

## <a name="install-visual-studio"></a>安裝 Visual Studio

您可以使用其中一種 hello 下列版本的 Visual Studio 開發 SCP.NET 與 C# 拓撲：

* Visual Studio 2012 [(含 Update 4)](http://www.microsoft.com/download/details.aspx?id=39305)

* Visual Studio 2013 [(含 Update 4)](http://www.microsoft.com/download/details.aspx?id=44921) 或 [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)

* Visual Studio 2015 或 [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)

* Visual Studio 2017 (任何版本)

## <a name="install-data-lake-tools-for-visual-studio"></a>安裝 Data Lake Tools for Visual Studio

tooinstall Data Lake tools for Visual Studio，請依照下列中的 hello 步驟[開始使用 Data Lake tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)。

## <a name="install-java"></a>安裝 Java

當您提交從 Visual Studio 的 Storm 拓樸時，SCP.NET 會產生包含 hello 拓樸和相依性的 zip 檔案。 Java 是使用的 toocreate 這些 zip 檔案，因為它會使用與 Linux 型叢集更相容的格式。

1. 安裝 hello Java Developer Kit (JDK) 7 或更新版本在您的開發環境。 您可以取得 hello 從 Oracle JDK [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html)。 您也可以使用[其他 Java 發佈](http://openjdk.java.net/) \(英文\)。

2. hello`JAVA_HOME`包含 Java 的環境變數必須點 toohello 目錄。

3. hello`PATH`環境變數必須包含 hello`%JAVA_HOME%\bin`目錄。

您可以使用下列 C# 主控台應用程式 tooverify Java 和 hello JDK 已正確安裝 hello:

```csharp
using System;
using System.IO;
namespace ConsoleApplication2
{
   class Program
   {
       static void Main(string[] args)
       {
           string javaHome = Environment.GetEnvironmentVariable(“JAVA_HOME”);
           if (!string.IsNullOrEmpty(javaHome))
           {
               string jarExe = Path.Combine(javaHome + @”\bin”, “jar.exe”);
               if (File.Exists(jarExe))
               {
                   Console.WriteLine(“JAVA Is Installed properly”);
                    return;
               }
               else
               {
                   Console.WriteLine(“A valid JAVA JDK is not found. Looks like JRE is installed instead of JDK.”);
               }
           }
           else
           {
             Console.WriteLine(“A valid JAVA JDK is not found. JAVA_HOME environment variable is not set.”);
           }
       }  
   }
}
```

## <a name="storm-templates"></a>Storm 範本

hello Data Lake tools for Visual Studio 提供下列範本的 hello:

| 專案類型 | 示範 |
| --- | --- |
| Storm 應用程式 |空白 Storm 拓撲專案。 |
| Storm Azure SQL 寫入器範例 |如何 toowrite tooAzure SQL 資料庫。 |
| Storm Azure Cosmos DB 讀取器範例 |如何從 Azure Cosmos DB tooread。 |
| Storm Azure Cosmos DB 寫入器範例 |如何 toowrite tooAzure Cosmos DB。 |
| Storm EventHub 讀取器範例 |如何從 Azure 事件中樞 tooread。 |
| Storm EventHub 寫入器範例 |如何 toowrite tooAzure 事件中心。 |
| Storm HBase 讀取器範例 |如何 tooread 從上 HDInsight HBase 叢集。 |
| Storm HBase 寫入器範例 |Toowrite tooHBase HDInsight 上的叢集。 |
| Storm 混合式範例 |如何 toouse Java 元件。 |
| Storm 範例 |基本的字數統計拓撲。 |

> [!WARNING]
> 並非所有範本都能與 Linux 架構的 HDInsight 搭配運作。 可能不相容的 Mono hello 範本所使用的 Nuget 套件。 檢查 hello[單聲道的相容性](http://www.mono-project.com/docs/about-mono/compatibility/)文件，並使用 hello [.NET Portability Analyzer](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) tooidentify 潛在問題。

在本文件中的 hello 步驟，您可以使用 hello 基本 Storm 應用程式專案類型 toocreate 拓撲。

### <a name="hbase-templates-notes"></a>HBase 範本注意事項

hello HBase 讀取器和寫入器範本使用 hello HBase REST API，不 hello HBase Java 應用程式開發介面，toocommunicate HBase HDInsight 叢集上使用。

### <a name="eventhub-templates-notes"></a>EventHub 範本注意事項

> [!IMPORTANT]
> hello Java 為基礎的 EventHub spout 隨附的 hello EventHub 讀取器範本可能不適用於 HDInsight 版本 3.5 或更新版本上出現的元件。 此元件的更新版本可在 [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib) \(英文\) 取得。

如需使用此元件和搭配 Storm on HDInsight 3.5 使用的範例拓撲，請參閱 [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub) \(英文\)。

## <a name="create-a-c-topology"></a>建立 C# 拓撲

1. 開啟 Visual Studio，選取 [檔案] > [新增]，然後選取 [專案]。

2. 從 hello**新專案**視窗中，展開 **已安裝** > **範本**，然後選取**Azure 資料湖**。 從範本 hello 清單，選取**Storm 應用程式**。 在 hello 囉 」 畫面下方，輸入**WordCount**做 hello hello 應用程式名稱。

    ![[新增專案] 視窗的螢幕擷取畫面](./media/hdinsight-storm-develop-csharp-visual-studio-topology/new-project.png)

3. 建立 hello 專案之後，您應該有下列檔案的 hello:

   * **Program.cs**： 此檔案會定義您的專案的 hello 拓撲。 預設會建立含有一個 Spout 和一個 Bolt 的預設拓撲。

   * **Spout.cs**：發出亂數的範例 Spout。

   * **Bolt.cs**： 會保留 hello spout 所發出的數字計數範例閃電。

     當您建立 hello 專案時，NuGet 下載最新 hello [SCP.NET 封裝](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/)。

     [!INCLUDE [scp.net version important](../../includes/hdinsight-storm-scpdotnet-version.md)]

### <a name="implement-hello-spout"></a>實作 hello spout

1. 開啟 **Spout.cs**。 Spouts 是使用的 tooread 拓撲從外部來源中的資料。 hello spout 主要元件為：

   * **NextTuple**: hello spout 允許 tooemit 新 tuple 時，由 Storm 呼叫。

   * **Ack** （只有交易式拓撲）： 處理通知寄件者 hello spout tuple 的 hello 拓撲中的其他元件所起始。 認可 tuple，可讓 hello spout 知道它已順利處理的下游元件。

   * **失敗**（只有交易式拓撲）： 處理會失敗-處理 hello 拓撲中的其他元件的 tuple。 實作 Fail 方法可讓您 toore-發出 hello tuple，以便再次處理。

2. 取代 hello hello 內容**Spout** hello 文字之後使用的類別。 此 spout 隨機會發出到 hello 拓撲的句子。

    ```csharp
    private Context ctx;
    private Random r = new Random();
    string[] sentences = new string[] {
        "hello cow jumped over hello moon",
        "an apple a day keeps hello doctor away",
        "four score and seven years ago",
        "snow white and hello seven dwarfs",
        "i am at two with nature"
    };

    public Spout(Context ctx)
    {
        // Set hello instance context
        this.ctx = ctx;

        Context.Logger.Info("Generator constructor called");

        // Declare Output schema
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // hello schema for hello default output stream is
        // a tuple that contains a string field
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(null, outputSchema));
    }

    // Get an instance of hello spout
    public static Spout Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Spout(ctx);
    }

    public void NextTuple(Dictionary<string, Object> parms)
    {
        Context.Logger.Info("NextTuple enter");
        // hello sentence toobe emitted
        string sentence;

        // Get a random sentence
        sentence = sentences[r.Next(0, sentences.Length - 1)];
        Context.Logger.Info("Emit: {0}", sentence);
        // Emit it
        this.ctx.Emit(new Values(sentence));

        Context.Logger.Info("NextTuple exit");
    }

    public void Ack(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }
    ```

### <a name="implement-hello-bolts"></a>實作 hello 攻擊

1. 刪除現有的 hello **Bolt.cs** hello 專案檔案。

2. 在**方案總管 中**，hello 專案上按一下滑鼠右鍵，然後選取**新增** > **新項目**。 從 hello 清單中，選取 **出現閃電**，並輸入**Splitter.cs**做為 hello 名稱。 重複第二個閃電名為此程序 toocreate **Counter.cs**。

   * **Splitter.cs**：實作會將句子分成個別單字，並發出一串新文字的 Bolt。

   * **Counter.cs**： 實作閃電，計算每個字，並發出新的資料流字詞與每個單字的 hello 計數。

     > [!NOTE]
     > 這些攻擊讀取和寫入 toostreams，但您也可以使用閃電 toocommunicate 來源，例如資料庫或服務。

3. 開啟 **Splitter.cs**。 它預設只有一個方法：**Execute**。 hello 閃電收到 tuple，以進行處理時，會呼叫 hello Execute 方法。 此時，您可以讀取和處理內送 Tuple，以及發出輸出 Tuple。

4. 取代 hello hello 內容**分隔器**類別以下列程式碼的 hello:

    ```csharp
    private Context ctx;

    // Constructor
    public Splitter(Context ctx)
    {
        Context.Logger.Info("Splitter constructor called");
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // Input contains a tuple with a string field (hello sentence)
        inputSchema.Add("default", new List<Type>() { typeof(string) });
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // Outbound contains a tuple with a string field (hello word)
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance of hello bolt
    public static Splitter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Splitter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello sentence from hello tuple
        string sentence = tuple.GetString(0);
        // Split at space characters
        foreach (string word in sentence.Split(' '))
        {
            Context.Logger.Info("Emit: {0}", word);
            //Emit each word
            this.ctx.Emit(new Values(word));
        }

        Context.Logger.Info("Execute exit");
    }
    ```

5. 開啟**Counter.cs**，並取代 hello 下列中的 hello 類別內容：

    ```csharp
    private Context ctx;

    // Dictionary for holding words and counts
    private Dictionary<string, int> counts = new Dictionary<string, int>();

    // Constructor
    public Counter(Context ctx)
    {
        Context.Logger.Info("Counter constructor called");
        // Set instance context
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string field - hello word
        inputSchema.Add("default", new List<Type>() { typeof(string) });

        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string and integer field - hello word and hello word count
        outputSchema.Add("default", new List<Type>() { typeof(string), typeof(int) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance
    public static Counter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Counter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello word from hello tuple
        string word = tuple.GetString(0);
        // Do we already have an entry for hello word in hello dictionary?
        // If no, create one with a count of 0
        int count = counts.ContainsKey(word) ? counts[word] : 0;
        // Increment hello count
        count++;
        // Update hello count in hello dictionary
        counts[word] = count;

        Context.Logger.Info("Emit: {0}, count: {1}", word, count);
        // Emit hello word and count information
        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new List<SCPTuple> { tuple }, new Values(word, count));
        Context.Logger.Info("Execute exit");
    }
    ```

### <a name="define-hello-topology"></a>定義 hello 拓撲

在圖形中，它會定義元件之間流動 hello 資料的方式排列 spouts 和攻擊。 針對此拓撲，hello 圖形如下所示：

![元件排列方式的圖表](./media/hdinsight-storm-develop-csharp-visual-studio-topology/wordcount-topology.png)

句子從 hello spout 會發出，因此是分散式的 hello 分隔器閃電 tooinstances。 hello 分隔器閃電成文字，也就是分散式的 toohello 計數器閃電中斷 hello 句子。

字數統計會在本機保留 hello 計數器執行個體，因為我們想確定特定單字流程 toohello toomake 相同計數器閃電執行個體。 每個執行個體會保持追蹤特定文字。 Hello 分隔器閃電維護無狀態，因為它實際上並不重要 hello 分隔器的執行個體收到的句子。

開啟 **Program.cs**。 hello 重要的方法是**GetTopologyBuilder**，即是使用的 toodefine hello 拓樸提交 tooStorm。 取代 hello 內容**GetTopologyBuilder**以下列程式碼 tooimplement hello 拓樸先前所述的 hello:

```csharp
// Create a new topology named 'WordCount'
TopologyBuilder topologyBuilder = new TopologyBuilder("WordCount" + DateTime.Now.ToString("yyyyMMddHHmmss"));

// Add hello spout toohello topology.
// Name hello component 'sentences'
// Name hello field that is emitted as 'sentence'
topologyBuilder.SetSpout(
    "sentences",
    Spout.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"sentence"}}
    },
    1);
// Add hello splitter bolt toohello topology.
// Name hello component 'splitter'
// Name hello field that is emitted 'word'
// Use suffleGrouping toodistribute incoming tuples
//   from hello 'sentences' spout across instances
//   of hello splitter
topologyBuilder.SetBolt(
    "splitter",
    Splitter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word"}}
    },
    1).shuffleGrouping("sentences");

// Add hello counter bolt toohello topology.
// Name hello component 'counter'
// Name hello fields that are emitted 'word' and 'count'
// Use fieldsGrouping tooensure that tuples are routed
//   toocounter instances based on hello contents of field
//   position 0 (hello word). This could also have been
//   List<string>(){"word"}.
//   This ensures that hello word 'jumped', for example, will always
//   go toohello same instance
topologyBuilder.SetBolt(
    "counter",
    Counter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word", "count"}}
    },
    1).fieldsGrouping("splitter", new List<int>() { 0 });

// Add topology config
topologyBuilder.SetTopologyConfig(new Dictionary<string, string>()
{
    {"topology.kryo.register","[\"[B\"]"}
});

return topologyBuilder;
```

## <a name="submit-hello-topology"></a>送出 hello 拓樸

1. 在**方案總管 中**，hello 專案上按一下滑鼠右鍵，然後選取**提交 HDInsight 上的 tooStorm**。

   > [!NOTE]
   > 如果出現提示，請輸入您的 Azure 訂閱 hello 認證。 如果您有多個訂用帳戶，登入另一個則包含您在 HDInsight 叢集的 Storm toohello。

2. 選取您在 HDInsight 叢集的 Storm 從 hello **Storm 叢集**下拉式清單，然後選取**送出**。 如果使用 hello hello 提交成功，您可以監視**輸出**視窗。

3. 已成功送出 hello 拓樸，當 hello **Storm 拓撲**hello 叢集應該會出現。 選取 hello **WordCount**拓撲從 hello 列出 tooview hello 執行拓撲的相關資訊。

   > [!NOTE]
   > 您也可以從 [伺服器總管] 檢視 [Storm 拓撲]。 展開 [Azure] > [HDInsight]，以滑鼠右鍵按一下 Storm on HDInsight 叢集，然後選取 [檢視 Storm 拓撲]。

    tooview 資訊 hello 元件在 hello 拓撲中，按兩下 hello 圖中的 hello 元件。

4. 從 hello**拓撲摘要**檢視中，按一下**Kill** toostop hello 拓撲。

   > [!NOTE]
   > Storm 拓撲繼續 toorun 直到都已停用，或刪除 hello 叢集。

## <a name="transactional-topology"></a>交易式拓撲

hello 先前拓樸為非交易式。 hello 拓撲中的 hello 元件不會實作功能 tooreplaying 訊息。 如需交易式拓撲的範例，建立專案並選取**Storm 範例**hello 專案類型。

交易式拓撲實作 hello 遵循 toosupport 重新執行的資料：

* **中繼資料快取**: hello spout 必須儲存 hello 資料發出，以便可以擷取與發出一次，如果發生失敗的 hello 資料的中繼資料。 由於 hello 範例所發出的 hello 資料很小，每個 tuple 的 hello 未經處理資料都會儲存在重新執行的字典。

* **Ack**: hello 拓撲中的每個閃電可以呼叫`this.ctx.Ack(tuple)`tooacknowledge 已成功處理 tuple。 當所有發射 acked hello tuple，hello `Ack` hello spout 方法會叫用。 hello`Ack`方法可讓重新執行快取的 hello spout tooremove 資料。

* **失敗**： 可以在呼叫每個閃電`this.ctx.Fail(tuple)`tooindicate 該處理失敗的 tuple。 hello 失敗傳播 toohello`Fail`方法 hello spout，其中 hello tuple 可以重新執行所使用的快取中繼資料。

* **序列識別碼**：發出 Tuple 時，可以指定唯一的序列識別碼。 這個值識別 （「 通知 」 和 「 失敗 」） 重新執行處理的 hello tuple。 比方說，hello 在 hello spout **Storm 範例**發出資料時，專案會使用 hello 下列：

        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), lastSeqId);

    此程式碼會發出包含句子 toohello 預設資料流中包含的 hello 順序識別碼值與 tuple **lastSeqId**。 在此範例中，會遞增每個發出 Tuple 的 **lastSeqId**。

示 hello **Storm 範例**專案中，交易式元件是否可以在執行階段，根據組態設定。

## <a name="hybrid-topology-with-c-and-java"></a>採用 C# 和 Java 的混合式拓撲

您也可以使用 Data Lake 工具，如需 Visual Studio toocreate 混合拓撲，其中有些元件是 C#，而其他則 Java。

針對混合式拓撲範例，請建立專案，然後選取 [Storm 混合式範例]。 此範例類型示範 hello 下列概念：

* **Java Spout** 和 **C# Bolt**：定義於 **HybridTopology_javaSpout_csharpBolt**。

    * 交易式版本定義於 **HybridTopologyTx_javaSpout_csharpBolt**。

* **C# Spout** 和 **Java Bolt**：定義於 **HybridTopology_csharpSpout_javaBolt**。

    * 交易式版本定義於 **HybridTopologyTx_csharpSpout_javaBolt**。

  > [!NOTE]
  > 此版本也會示範 toouse Clojure 從文字檔案做為 Java 元件的程式碼。


tooswitch hello 拓撲時送出 hello 專案，只要移動 hello`[Active(true)]`想 toouse，送出 toohello 叢集之前的陳述式 toohello 拓撲。

> [!NOTE]
> 在 hello 這個專案的一部分提供所需的所有 hello Java 檔案**JavaDependency**資料夾。

當您建立並提交混合式拓撲，請考慮下列 hello:

* 您必須使用**JavaComponentConstructor** toocreate hello spout 或閃電的 Java 類別的執行個體。

* 您應該使用**microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** tooserialize 資料傳入或傳出 Java 元件從 Java 物件 tooJSON。

* 當送出 hello 拓撲 toohello 伺服器，您必須使用 hello**額外的組態**選項 toospecify hello **Java 檔案路徑**。 指定的 hello 路徑應該是包含 hello JAR 檔案，其中包含您的 Java 類別的 hello 目錄。

### <a name="azure-event-hubs"></a>Azure 事件中心

SCP.NET 版本 0.9.4.203 引入新類別，以及特別為 hello 事件中心 spout (從事件中心讀取 Java spout) 所使用的方法。 當您建立使用事件中心 spout 拓撲時，使用下列方法 hello:

* **EventHubSpoutConfig**類別： 建立物件，其中包含 hello hello spout 元件的設定。

* **TopologyBuilder.SetEventHubSpout**方法： 新增 hello 事件中心 spout 元件 toohello 拓撲。

> [!NOTE]
> 您仍然必須使用 hello **CustomizedInteropJSONSerializer** hello spout 所產生的 tooserialize 資料。

## <a id="configurationmanager"></a>使用 ConfigurationManager

請勿使用**ConfigurationManager** tooretrieve 組態中的值閃電和 spout 元件。 這麼做會導致 Null 指標例外狀況。 相反地，hello 專案組態傳入 hello Storm 拓樸為 hello 拓撲內容中的索引鍵和值組。 每個元件所使用的設定值必須擷取它們 hello 內容初始化期間。

hello 下列程式碼示範如何 tooretrieve 這些值：

```csharp
public class MyComponent : ISCPBolt
{
    // toohold configuration information loaded from context
    Configuration configuration;
    ...
    public MyComponent(Context ctx, Dictionary<string, Object> parms)
    {
        // Save a copy of hello context for this component instance
        this.ctx = ctx;
        // If it exists, load hello configuration for hello component
        if(parms.ContainsKey(Constants.USER_CONFIG))
        {
            this.configuration = parms[Constants.USER_CONFIG] as System.Configuration.Configuration;
        }
        // Retrieve hello value of "Foo" from configuration
        var foo = this.configuration.AppSettings.Settings["Foo"].Value;
    }
    ...
}
```

如果您使用`Get`方法 tooreturn 您元件的執行個體，您必須確定它會傳遞兩個 hello`Context`和`Dictionary<string, Object>`參數 toohello 建構函式。 hello 下列範例是基本`Get`正確傳遞這些值的方法：

```csharp
public static MyComponent Get(Context ctx, Dictionary<string, Object> parms)
{
    return new MyComponent(ctx, parms);
}
```

## <a name="how-tooupdate-scpnet"></a>如何 tooupdate SCP.NET

最新版 SCP.NET 支援透過 NuGet 進行封裝升級。 當新的更新可用時，您會收到升級通知。 toomanually 核取進行升級時，請遵循下列步驟：

1. 在**方案總管 中**，hello 專案上按一下滑鼠右鍵，然後選取**管理 NuGet 封裝**。

2. 從 hello 封裝管理員 中，選取**更新**。 如果有可用的更新，它會列出。 按一下**更新**的 hello 封裝 tooinstall 它。

> [!IMPORTANT]
> 如果您的專案建立的舊版 SCP.NET 未使用 NuGet，您必須執行下列步驟 tooupdate tooa 較新版本的 hello:
>
> 1. 在**方案總管 中**，hello 專案上按一下滑鼠右鍵，然後選取**管理 NuGet 封裝**。
> 2. 使用 hello**搜尋**欄位中搜尋，然後再新增， **Microsoft.SCP.Net.SDK** toohello 專案。

## <a name="troubleshoot-common-issues-with-topologies"></a>針對拓撲常見問題進行疑難排解

### <a name="null-pointer-exceptions"></a>Null 指標例外狀況

當您使用 C# 拓撲與 linux 的 HDInsight 叢集時，閃電和 spout 使用的元件**ConfigurationManager** tooread 組態設定，在執行階段可能會傳回 null 指標例外狀況。

hello 專案組態傳入 hello Storm 拓撲中，為 hello 拓撲內容中的索引鍵和值組。 它可以擷取從它們初始化時，傳遞 tooyour 元件 hello 字典物件。

如需詳細資訊，請參閱 hello [ConfigurationManager](#configurationmanager)本文件一節。

### <a name="systemtypeloadexception"></a>System.TypeLoadException

當您使用 C# 拓撲與 linux 的 HDInsight 叢集時，您可能會遇到下列錯誤 hello:

    System.TypeLoadException: Failure has occurred while loading a type.

當您使用與.NET 的 Mono 支援 hello 版本不相容的二進位檔時，就會發生此錯誤。

對於以 Linux 為基礎的 HDInsight 叢集，請確定專案使用針對 .NET 4.5 編譯的二進位檔。

### <a name="test-a-topology-locally"></a>在本機測試拓撲

雖然它是簡單 toodeploy 拓撲 tooa 叢集，在某些情況下，您可能需要 tootest 在本機的拓撲。 使用下列步驟 toorun hello 和測試 hello 範例拓撲在本教學課程，在本機開發環境中。

> [!WARNING]
> 本機測試只適用於僅限 C# 的基本拓撲。 您不得將本機測試使用於混合式拓撲或使用多個資料流的拓撲。

1. 在**方案總管 中**，hello 專案上按一下滑鼠右鍵，然後選取**屬性**。 在 hello 專案屬性中，變更 hello**輸出類型**太**主控台應用程式**。

    ![醒目提示 [輸出] 類型的專案屬性螢幕擷取畫面](./media/hdinsight-storm-develop-csharp-visual-studio-topology/outputtype.png)

   > [!NOTE]
   > 請記住 toochange hello**輸出類型**太回**類別庫**hello 拓撲 tooa 叢集部署之前。

2. 在**方案總管 中**，hello 專案上按一下滑鼠右鍵，然後選取**新增** > **新項目**。 選取**類別**，並輸入**LocalTest.cs**與 hello 類別名稱。 最後按一下 [新增]。

3. 開啟**LocalTest.cs**，並加入下列 hello**使用**hello 上方的陳述式：

    ```csharp
    using Microsoft.SCP;
    ```

4. 使用 hello 下列程式碼做為 hello 內容的 hello **LocalTest**類別：

    ```csharp
    // Drives hello topology components
    public void RunTestCase()
    {
        // An empty dictionary for use when creating components
        Dictionary<string, Object> emptyDictionary = new Dictionary<string, object>();

        #region Test hello spout
        {
            Console.WriteLine("Starting spout");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext spoutCtx = LocalContext.Get();
            // Get a new instance of hello spout, using hello local context
            Spout sentences = Spout.Get(spoutCtx, emptyDictionary);

            // Emit 10 tuples
            for (int i = 0; i < 10; i++)
            {
                sentences.NextTuple(emptyDictionary);
            }
            // Use LocalContext toopersist hello data stream toofile
            spoutCtx.WriteMsgQueueToFile("sentences.txt");
            Console.WriteLine("Spout finished");
        }
        #endregion

        #region Test hello splitter bolt
        {
            Console.WriteLine("Starting splitter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext splitterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Splitter splitter = Splitter.Get(splitterCtx, emptyDictionary);

            // Set hello data stream toohello data created by hello spout
            splitterCtx.ReadFromFileToMsgQueue("sentences.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = splitterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                splitter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            splitterCtx.WriteMsgQueueToFile("splitter.txt");
            Console.WriteLine("Splitter bolt finished");
        }
        #endregion

        #region Test hello counter bolt
        {
            Console.WriteLine("Starting counter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext counterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Counter counter = Counter.Get(counterCtx, emptyDictionary);

            // Set hello data stream toohello data created by splitter bolt
            counterCtx.ReadFromFileToMsgQueue("splitter.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = counterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                counter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            counterCtx.WriteMsgQueueToFile("counter.txt");
            Console.WriteLine("Counter bolt finished");
        }
        #endregion
    }
    ```

    需要一點時間 tooread 透過 hello 程式碼註解。 此程式碼使用**LocalContext** toorun hello 元件 hello 開發環境，並持續發生 hello hello 本機磁碟機上的元件 tootext 檔案之間的資料流。

1. 開啟**Program.cs**，並加入下列 toohello hello **Main**方法：

    ```csharp
    Console.WriteLine("Starting tests");
    System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "WordCount-LocalTest");
    // Initialize hello runtime
    SCPRuntime.Initialize();

    //If we are not running under hello local context, throw an error
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)
    {
        throw new Exception(string.Format("unexpected pluginType: {0}", Context.pluginType));
    }
    // Create test instance
    LocalTest tests = new LocalTest();
    // Run tests
    tests.RunTestCase();
    Console.WriteLine("Tests finished");
    Console.ReadKey();
    ```

2. 儲存 hello 變更，然後再按一下**F5**或選取**偵錯** > **開始偵錯**toostart hello 專案。 主控台視窗應該會出現，並身分 hello 測試進度的記錄狀態。 當**測試完成**隨即出現，請按任何鍵 tooclose hello 視窗。

3. 使用**Windows 檔案總管**toolocate hello 目錄，其中包含您的專案。 例如：**C:\Users\<your_user_name>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**。 在此目錄中，開啟 Bin，然後按一下偵錯。 您應該會看到 hello 測試執行時所產生的 hello 文字檔案： sentences.txt、 counter.txt 和 splitter.txt。 開啟每個文字檔案，並檢查 hello 資料。

   > [!NOTE]
   > 字串資料會在這些檔案中保存為十進位值的陣列。 例如， \[[97,103,111]] 在 hello **splitter.txt**檔案是 hello 字*和*。

> [!NOTE]
> 要確定 tooset hello**專案類型**太回**類別庫**之前部署 tooa Storm HDInsight 叢集上的。

### <a name="log-information"></a>記錄資訊

您可以使用 `Context.Logger`，輕鬆地記錄拓撲元件中的資訊。 例如，hello 下列範例會建立資訊的記錄項目：

```csharp
Context.Logger.Info("Component started");
```

可以檢視記錄的資訊從 hello **Hadoop 服務記錄檔**，找到**伺服器總管**。 展開您的 HDInsight 叢集的 Storm 的 hello 項目，然後展開**Hadoop 服務記錄檔**。 最後，選取 hello 記錄檔案 tooview。

> [!NOTE]
> hello 記錄檔會儲存在 hello Azure 儲存體帳戶，以供您的叢集。 tooview hello 記錄檔，Visual Studio 中的，您必須登入 toohello 擁有 hello 儲存體帳戶的 Azure 訂用帳戶。

### <a name="view-error-information"></a>檢視錯誤資訊

tooview 錯誤發生在執行的拓撲中，使用下列步驟的 hello:

1. 從**伺服器總管**，hello Storm HDInsight 叢集上的按一下滑鼠右鍵，然後選取**檢視 Storm 拓撲**。

2. Hello **Spout**和**釘**，hello**最後一個錯誤**資料行包含 hello 最後一個錯誤的資訊。

3. 選取 hello **Spout 識別碼**或**閃電識別碼**hello 元件列出發生錯誤。 Hello 是顯示的其他錯誤的詳細資料頁面上列出資訊在 hello**錯誤**在 hello hello 頁面底部的區段。

4. tooobtain 的詳細資訊，選取**連接埠**從 hello**執行程式**hello 頁面區段、 toosee hello Storm 背景工作記錄檔中的 hello 最後幾分鐘的時間。

### <a name="errors-submitting-topologies"></a>提交拓撲的錯誤

如果您遇到錯誤拓撲 tooHDInsight 送出時，您可以尋找記錄 hello 處理拓撲提交您的 HDInsight 叢集上的伺服器端元件。 tooretrieve 這些記錄檔時，下列命令，從命令列使用 hello:

    scp sshuser@clustername-ssh.azurehdinsight.net:/var/log/hdinsight-scpwebapi/hdinsight-scpwebapi.out .

取代__sshuser__以 hello hello 叢集的 SSH 使用者帳戶。 取代__clustername__ hello hello HDInsight 叢集名稱。 如需搭配 HDInsight 使用 `scp` 和 `ssh` 的詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

提交失敗有多種原因：

* JDK 未安裝或不在 hello 路徑。
* 必要的 Java 相依性不會包含在 hello 送出。
* 不相容的相依性。
* 重複的拓撲名稱。

如果 hello`hdinsight-scpwebapi.out`記錄檔包含`FileNotFoundException`，這可能會因下列條件的 hello:

* hello JDK 不上 hello 開發環境的 hello 路徑。 請確認該 hello hello 開發環境中，而且已安裝的 JDK `%JAVA_HOME%/bin` hello 路徑中。
* 遺漏 Java 相依性。 請確定您同時納入任何必要的 d 檔案做為 hello 送出的一部分。

## <a name="next-steps"></a>後續步驟

如需從事件中樞處理資料的範例，請參閱[利用 Storm on HDInsight 處理 Azure 事件中樞的事件](hdinsight-storm-develop-csharp-event-hub-topology.md)。

如需將資料流的資料分成多個資料流的 C# 拓撲範例，請參閱 [C# Storm 範例](https://github.com/Blackmist/csharp-storm-example)。

toodiscover 建立 C# 拓撲的相關詳細資訊，請參閱[GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md)。

與 HDInsight 的更多方式 toowork 及多個出現之 HDInsight 範例，請參閱下列文件的 hello:

**Microsoft SCP.NET**

* [SCP 程式設計指南](hdinsight-storm-scp-programming-guide.md)

**Apache Storm on HDInsight**

* [使用 Apache Storm on HDInsight 部署和監視拓撲](hdinsight-storm-deploy-monitor-topology.md)
* [Storm on HDInsight 的範例拓撲](hdinsight-storm-example-topology.md)

**Apache Hadoop on HDInsight**

* [搭配 HDInsight 上的 Hadoop 使用 Hive](hdinsight-use-hive.md)
* [搭配 HDInsight 上的 Hadoop 使用 Pig](hdinsight-use-pig.md)
* [搭配 HDInsight 上的 Hadoop 使用 MapReduce](hdinsight-use-mapreduce.md)

**Apache HBase on HDInsight**

* [開始使用 HBase on HDInsight](hdinsight-hbase-tutorial-get-started.md)
