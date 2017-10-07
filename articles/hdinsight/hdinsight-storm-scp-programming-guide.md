---
title: "aaaSCP.NET 程式設計指南 |Microsoft 文件"
description: "深入了解如何 toouse SCP.NET toocreate。以網路為基礎的 Storm 拓撲使用 HDInsight 上出現。"
services: hdinsight
documentationcenter: 
author: raviperi
manager: jhubbard
editor: cgronlun
ms.assetid: 34192ed0-b1d1-4cf7-a3d4-5466301cf307
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/16/2016
ms.author: raviperi
ms.openlocfilehash: a57f4217b07e0e82a3f36650308695fbb45d9128
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scp-programming-guide"></a>SCP 程式設計指南
SCP 是平台 toobuild 即時、 可靠、 一致和高效能資料處理應用程式。 它最上層的內建[Apache Storm](http://storm.incubator.apache.org/) -處理 hello OSS 社群所設計的系統資料流。 Storm 由 Nathan Marz 所設計，由 Twitter 公開原始碼。 它會運用[Apache 動物園管理員](http://zookeeper.apache.org/)，另一個 Apache 專案 tooenable 可靠的分散式的協調和狀態管理。 

Hello SCP 專案移植 Windows 上的出現不僅 hello 專案也加入擴充功能和自訂 hello Windows 生態系統。 hello 擴充功能包括.NET 開發人員體驗和程式庫、 hello 自訂包括 Windows 為基礎的部署。 

hello 擴充和自訂完成的方式，我們不需要 toofork hello OSS 專案，而且我們可能會利用衍生之上 Storm 的生態系統。

## <a name="processing-model"></a>處理模型
hello SCP 中的資料會模型化為連續資料流的 tuple。 通常 hello tuple 流入某些佇列第一次，然後挑選，以及裝載於 Storm 拓撲的商務邏輯所轉換，最後 hello 輸出無法使用管線傳送 tuple tooanother SCP 系統，或者是認可的 toostores 喜歡分散式的檔案系統或資料庫，例如 SQL Server。

![填入資料 tooprocessing，摘要的資料存放區的佇列的圖表](media/hdinsight-storm-scp-programming-guide/queue-feeding-data-to-processing-to-data-store.png)

在 Storm 中，應用程式拓撲定義一份運算圖。 拓撲中的每個節點包含處理邏輯，節點之間的連結代表資料流程。 hello 節點 tooinject 輸入的資料到 hello 拓撲稱為 Spouts，可以是使用的 toosequence hello 資料。 hello 輸入的資料可能位於檔案記錄檔、 交易式資料庫、 系統效能計數器等等。 使用這兩個輸入和輸出資料流的 hello 節點稱為攻擊，請勿 hello 實際資料的篩選和項目，並彙總。

SCP 支援竭盡所能、至少一次和剛好一次這三種資料處理方法。 在分散式串流處理應用程式中，資料處理期間可能發生各種錯誤，例如網路中斷、機器故障或使用者程式碼錯誤等。在-至少一次處理可以確保將會處理所有資料至少一次重新執行自動 hello 相同的資料時就會發生錯誤。 至少一次的處理方法簡單又可靠，在許多應用程式中都很適合。 不過，當 hello 應用程式需要精確的計算，例如，在-至少一次處理會不足因為 hello 相同的資料無法潛在播放 hello 應用程式拓撲中。 在此情況下，完全-hello 資料可能會重新執行，並多次處理時，即使之後處理的設計 toomake 確定 hello 結果是否正確。

SCP 運用 hello Java Virtual Machine (JVM) 出現在 hello 封面時，可讓.NET 開發人員 toodevelop 即時資料處理序應用程式。 hello.NET 和 JVM 透過 TCP 本機通訊端進行通訊。 基本上每個 Spout/閃電是以.Net/Java 處理序組 hello 使用者邏輯與外掛程式的.Net 處理序中執行的所在。

toobuild 資料，處理 SCP 之上的應用程式，需要數個步驟：

* 設計和實作 hello Spouts toopull 資料從佇列中。
* 設計和實作發射 tooprocess hello 輸入的資料，並儲存資料 tooexternal 存放區，例如資料庫。
* 設計 hello 拓樸，然後送出，再執行 hello 拓撲。 hello 拓撲定義端點和 hello 資料 hello 端點之間的流量。 SCP 會採取 hello 拓撲規格，並將它部署在 Storm 叢集上，每個頂點邏輯的其中一個節點執行的位置。 hello 容錯移轉和調整將會處理 hello Storm 工作排程器。

本文件將會使用一些簡單的範例 toowalk，如何透過 SCP toobuild 資料處理應用程式。

## <a name="scp-plugin-interface"></a>SCP 外掛程式介面
SCP 外掛程式 （或應用程式） 是獨立的 Exe，可以同時執行 Visual Studio 內 hello 開發階段，並在生產環境中部署之後插入 hello Storm 管線。 撰寫 hello SCP 外掛程式是只 hello 與撰寫任何其他標準 Windows 主控台應用程式相同。 SCP.NET 平台宣告 spout/閃電，某些介面和 hello 使用者外掛程式程式碼應該實作這些介面。 這項設計 hello 主要用途是該 hello 使用者可以專注於他們自己的商務 logics，並保留 SCP.NET 平台所處理其他事情 toobe。

hello 使用者外掛程式程式碼應該實作其中一個 hello 下列項目介面，取決於是否 hello 拓撲是交易式或非交易式和 hello 元件是否 spout 或閃電。

* ISCPSpout
* ISCPBolt
* ISCPTxSpout
* ISCPBatchBolt

### <a name="iscpplugin"></a>ISCPPlugin
ISCPPlugin 是 hello 所有種類外掛程式的通用介面。 目前為虛擬介面。

    public interface ISCPPlugin 
    {
    }

### <a name="iscpspout"></a>ISCPSpout
ISCPSpout 是非交易式 spout hello 介面。

     public interface ISCPSpout : ISCPPlugin                    
     {
         void NextTuple(Dictionary<string, Object> parms);         
         void Ack(long seqId, Dictionary<string, Object> parms);   
         void Fail(long seqId, Dictionary<string, Object> parms);  
     }

當`NextTuple()`會呼叫 hello C\#使用者程式碼可以發出一個或多個 tuple。 如果沒有任何 tooemit，此方法應傳回而不發出任何項目。 請注意，`NextTuple()`、`Ack()` 和 `Fail()` 都是在 C\# 程序的單一執行緒中放在密封迴圈內呼叫。 當不有任何 tuple tooemit 時，是禮貌 toohave NextTuple 睡眠的短的時間量 （例如 10 毫秒為單位），以不 toowaste 太多的 CPU。

只有當規格檔中啟用認可機制時，才會呼叫 `Ack()` 和 `Fail()`。 hello`seqId`是使用的 tooidentify hello tuple acked 或者失敗。 因此如果 ack 已啟用非交易式拓撲中，應使用下列發出函式的 hello Spout 中：

    public abstract void Emit(string streamId, List<object> values, long seqId); 

如果非交易式拓撲中不支援通知，hello`Ack()`和`Fail()`可以保留為空白的函式。

hello`parms`在這些函式的輸入的參數並非只是空的字典，這些是保留供未來使用。

### <a name="iscpbolt"></a>ISCPBolt
ISCPBolt 是非交易式閃電 hello 介面。

    public interface ISCPBolt : ISCPPlugin 
    {
    void Execute(SCPTuple tuple);           
    }

新的 tuple 可用時，hello`Execute()`函式呼叫 tooprocess 它。

### <a name="iscptxspout"></a>ISCPTxSpout
ISCPTxSpout 是交易式 spout hello 介面。

    public interface ISCPTxSpout : ISCPPlugin
    {
        void NextTx(out long seqId, Dictionary<string, Object> parms);  
        void Ack(long seqId, Dictionary<string, Object> parms);         
        void Fail(long seqId, Dictionary<string, Object> parms);        
    }

就像對應的非交易式節點一樣，`NextTx()`、`Ack()` 和 `Fail()` 也都是在 C\# 程序的單一執行緒中放在密封迴圈內呼叫。 沒有資料 tooemit 時，它是禮貌 toohave`NextTx`進入睡眠短的時間 （10 毫秒） 內，以不 toowaste 太多的 CPU。

`NextTx()`之所以是新的交易，toostart hello 參數`seqId`並使用的 tooidentify hello 交易，也會用於`Ack()`和`Fail()`。 在`NextTx()`，使用者可以發出資料 tooJava 側邊。 hello 資料會儲存在動物園管理員 toosupport 重新執行。 動物園管理員 hello 容量皆有限，因為使用者應該只會發出中繼資料，不在交易式 spout 大量資料。

Storm 會自動重播交易 (若失敗)，所以正常情況下應該不會呼叫 `Fail()` 。 但是如果 SCP 可以檢查交易式 spout 所發出的 hello 中繼資料，可以呼叫`Fail()`hello 的中繼資料無效。

hello`parms`在這些函式的輸入的參數並非只是空的字典，這些是保留供未來使用。

### <a name="iscpbatchbolt"></a>ISCPBatchBolt
ISCPBatchBolt 是交易式閃電 hello 介面。

    public interface ISCPBatchBolt : ISCPPlugin           
    {
        void Execute(SCPTuple tuple);
        void FinishBatch(Dictionary<string, Object> parms);  
    }

`Execute()`新的 tuple 抵達 hello 閃電時呼叫。 `FinishBatch()` 。 hello`parms`輸入的參數保留供未來使用。

在交易式拓撲中，有一個重要的概念 – `StormTxAttempt`。 它有 `TxId` 和 `AttemptId` 兩個欄位。 `TxId`並使用的 tooidentify 是特定的交易，並針對給定的交易，如果可能會有多個嘗試 hello 交易失敗，而是重新執行。 SCP.NET 新將不同 ISCPBatchBolt 物件 tooprocess 每個`StormTxAttempt`，就和 Java 端中的哪些 Storm 執行一樣。 hello 這種設計的目的是 toosupport 平行交易處理。 使用者應該記住它，如果完成交易嘗試，將會終結 hello 對應 ISCPBatchBolt 物件，記憶體回收。

## <a name="object-model"></a>物件模型
SCP.NET 與開發人員 tooprogram 也提供一組簡單的索引鍵物件。 包括 **Context**、**StateStore** 和 **SCPRuntime**。 在本節 hello 其餘部分中，將討論它們。

### <a name="context"></a>Context
內容會提供執行的環境 toohello 應用程式。 每個 ISCPPlugin 執行個體 (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) 都有一個對應的 Context 執行個體。 內容所提供的 hello 功能可分成兩個部分: （1) hello 靜態部分中可用 hello 整個 C\#處理時，只適用於 hello 特定內容執行個體 （2) hello 動態組件。

### <a name="static-part"></a>靜態部分
    public static ILogger Logger = null;
    public static SCPPluginType pluginType;                      
    public static Config Config { get; set; }                    
    public static TopologyContext TopologyContext { get; set; }  

`Logger` 做為記錄用途。

`pluginType`是用 hello C tooindicate hello 外掛程式類型\#程序。 如果 hello C\# （不含 Java) 的本機測試模式中執行程序，hello 外掛程式型別是`SCP_NET_LOCAL`。

    public enum SCPPluginType 
    {
        SCP_NET_LOCAL = 0,       
        SCP_NET_SPOUT = 1,       
        SCP_NET_BOLT = 2,        
        SCP_NET_TX_SPOUT = 3,   
        SCP_NET_BATCH_BOLT = 4  
    }

`Config`提供從 Java 端 tooget 組態參數。 從 Java 端 hello 參數傳遞時 C\#初始化外掛程式。 hello`Config`參數分為兩個部分：`stormConf`和`pluginConf`。

    public Dictionary<string, Object> stormConf { get; set; }  
    public Dictionary<string, Object> pluginConf { get; set; }  

`stormConf`Storm 所定義的參數和`pluginConf`hello SCP 所定義的參數。 例如：

    public class Constants
    {
        … …

        // constant string for pluginConf
        public static readonly String NONTRANSACTIONAL_ENABLE_ACK = "nontransactional.ack.enabled";  

        // constant string for stormConf
        public static readonly String STORM_ZOOKEEPER_SERVERS = "storm.zookeeper.servers";           
        public static readonly String STORM_ZOOKEEPER_PORT = "storm.zookeeper.port";                 
    }

`TopologyContext`會提供 tooget hello 拓撲內容，它是最有用之元件的多個平行處理原則。 下列是一個範例：

    //demo how tooget TopologyContext info
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)                      
    {
        Context.Logger.Info("TopologyContext info:");
        TopologyContext topologyContext = Context.TopologyContext;                    
        Context.Logger.Info("taskId: {0}", topologyContext.GetThisTaskId());          
        taskIndex = topologyContext.GetThisTaskIndex();
        Context.Logger.Info("taskIndex: {0}", taskIndex);
        string componentId = topologyContext.GetThisComponentId();                    
        Context.Logger.Info("componentId: {0}", componentId);
        List<int> componentTasks = topologyContext.GetComponentTasks(componentId);  
        Context.Logger.Info("taskNum: {0}", componentTasks.Count);                    
    }

### <a name="dynamic-part"></a>動態部分
下列介面 hello 是相關 tooa 特定內容執行個體。 hello 內容執行個體是 SCP.NET 平台所建立，並傳遞 toohello 使用者程式碼：

    // Declare hello Output and Input Stream Schemas

    public void DeclareComponentSchema(ComponentStreamSchema schema);   

    // Emit tuple toodefault stream.
    public abstract void Emit(List<object> values);                   

    // Emit tuple toohello specific stream.
    public abstract void Emit(string streamId, List<object> values);  

針對非交易式 spout 支援通知，會提供下列方法 hello:

    // for non-transactional Spout which supports ack
    public abstract void Emit(string streamId, List<object> values, long seqId);  

對於非交易式閃電支援通知，它應該明確`Ack()`或`Fail()`hello 它接收的 tuple。 且當發出新的 tuple，也必須指定 hello 新 tuple 的 hello 錨點。 提供下列方法 hello。

    public abstract void Emit(string streamId, IEnumerable<SCPTuple> anchors, List<object> values); 
    public abstract void Ack(SCPTuple tuple);
    public abstract void Fail(SCPTuple tuple);

### <a name="statestore"></a>StateStore
`StateStore` 提供元資料服務、單調數列產生和免等待協調。 高階分散式並行抽象可根據 `StateStore`來建置，包括分散式鎖定、分散式佇列、屏障和交易服務。

SCP 應用程式可能使用 hello`State`物件 toopersist 中動物園管理員，特別是針對交易式拓撲的特定資訊。 因此，如果交易式 spout 損毀，並重新啟動，它可以從動物園管理員擷取 hello 所需的資訊，然後重新啟動 hello 管線進行。

hello`StateStore`物件主要有這些方法：

    /// <summary>
    /// Static method tooretrieve a state store of hello given path and connStr 
    /// </summary>
    /// <param name="storePath">StateStore Path</param>
    /// <param name="connStr">StateStore Address</param>
    /// <returns>Instance of StateStore</returns>
    public static StateStore Get(string storePath, string connStr);

    /// <summary>
    /// Create a new state object in this state store instance
    /// </summary>
    /// <returns>State from StateStore</returns>
    public State Create();

    /// <summary>
    /// Retrieve all states that were previously uncommitted, excluding all aborted states 
    /// </summary>
    /// <returns>Uncommited States</returns>
    public IEnumerable<State> GetUnCommitted();

    /// <summary>
    /// Get all hello States in hello StateStore
    /// </summary>
    /// <returns>All hello States</returns>
    public IEnumerable<State> States();

    /// <summary>
    /// Get state or registry object
    /// </summary>
    /// <param name="info">Registry Name(Registry only)</param>
    /// <typeparam name="T">Type, Registry or State</typeparam>
    /// <returns>Return Registry or State</returns>
    public T Get<T>(string info = null);

    /// <summary>
    /// List all hello committed states
    /// </summary>
    /// <returns>Registries contain hello Committed State </returns> 
    public IEnumerable<Registry> Commited();

    /// <summary>
    /// List all hello Aborted State in hello StateStore
    /// </summary>
    /// <returns>Registries contain hello Aborted State</returns>
    public IEnumerable<Registry> Aborted();

    /// <summary>
    /// Retrieve an existing state object from this state store instance 
    /// </summary>
    /// <returns>State from StateStore</returns>
    /// <typeparam name="T">stateId, id of hello State</typeparam>
    public State GetState(long stateId)

hello`State`物件主要有這些方法：

    /// <summary>
    /// Set hello status of hello state object toocommit 
    /// </summary>
    public void Commit(bool simpleMode = true); 

    /// <summary>
    /// Set hello status of hello state object tooabort 
    /// </summary>
    public void Abort();

    /// <summary>
    /// Put an attribute value under hello give key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <param name="attribute">State Attribute</param> 
    public void PutAttribute<T>(string key, T attribute); 

    /// <summary>
    /// Get hello attribute value associated with hello given key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <returns>State Attribute</returns>               
    public T GetAttribute<T>(string key);                    

Hello`Commit()`方法，當 simpleMode tootrue 設定時，將只會刪除對應 ZNode 動物園管理員中的 hello。 否則，它會刪除 hello 目前 ZNode，並加入新的節點在 hello 已認可\_路徑。

### <a name="scpruntime"></a>SCPRuntime
SCPRuntime 提供下列兩種方法的 hello。

    public static void Initialize();

    public static void LaunchPlugin(newSCPPlugin createDelegate);  

`Initialize()`是使用的 tooinitialize hello SCP 執行階段環境。 在此方法中，hello C\# toohello Java 端，以及取得設定參數和拓撲內容，將連線程序。

`LaunchPlugin()`正在使用的 tookick 關閉 hello 訊息處理迴圈。 在此迴圈中，hello C\#外掛程式將會收到訊息格式 （包括 tuple 和控制訊號） 的 Java 端，，，然後處理 hello 訊息時，可能呼叫 hello 介面方法提供 hello 使用者程式碼。 hello 方法的輸入的參數`LaunchPlugin()`是一種委派可傳回實作 ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt 介面的物件。

    public delegate ISCPPlugin newSCPPlugin(Context ctx, Dictionary\<string, Object\> parms); 

如 ISCPBatchBolt，我們可以得到`StormTxAttempt`從`parms`，並用它 toojudge 是否在重新執行的嘗試。 這通常在 hello 認可閃電，並示範在 hello`HelloWorldTx`範例。

一般而言，hello SCP 增益集可以執行以下兩種模式：

1. 本機測試模式： 在此模式中，hello SCP 外掛程式 (hello C\#使用者程式碼) 在 Visual Studio 內執行 hello 開發階段。 `LocalContext`可在此模式，提供方法 tooserialize hello 發出 tuple toolocal 檔案，以及送回 toomemory 讀取。
   
        public interface ILocalContext
        {
            List\<SCPTuple\> RecvFromMsgQueue();
            void WriteMsgQueueToFile(string filepath, bool append = false);  
            void ReadFromFileToMsgQueue(string filepath);                    
        }
2. 一般模式： 在此模式中，hello SCP 外掛程式所啟動 storm java 處理序。
   
    以下是啟動 SCP 外掛程式的範例：
   
        namespace Scp.App.HelloWorld
        {
        public class Generator : ISCPSpout
        {
            … …
            public static Generator Get(Context ctx, Dictionary<string, Object> parms)
            {
            return new Generator(ctx);
            }
        }
   
        class HelloWorld
        {
            static void Main(string[] args)
            {
            /* Setting hello environment variable here can change hello log file name */
            System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "HelloWorld");
   
            SCPRuntime.Initialize();
            SCPRuntime.LaunchPlugin(new newSCPPlugin(Generator.Get));
            }
        }
        }

## <a name="topology-specification-language"></a>拓撲規格語言
SCP 拓撲規格是特定領域的語言，用來描述和設定 SCP 拓撲。 它以 Storm 的 Clojure DSL 為基礎 (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>)，而由 SCP 擴充。

直接透過 hello toostorm 叢集來執行，就可以提出拓撲規格***runspec***命令。

SCP.NET 已新增下列函式 toodefine hello 交易式拓撲：

| **新函數** | **參數** | **說明** |
| --- | --- | --- |
| **tx-topolopy** |topology-name<br />spout-map<br />bolt-map |定義具有 hello 拓撲名稱的交易式拓撲&nbsp;spouts 定義地圖與 hello 發射定義地圖 |
| **scp-tx-spout** |exec-name<br />args<br />fields |定義交易式 spout。 它會執行與 hello 應用程式***exec 名稱***使用***args***。<br /><br />hello***欄位***是 spout 的 hello 輸出欄位 |
| **scp-tx-batch-bolt** |exec-name<br />args<br />fields |定義交易式批次 Bolt。 它會執行與 hello 應用程式***exec 名稱***使用***引數。***<br /><br />hello 欄位是針對閃電 hello 輸出欄位。 |
| **scp-tx-commit-bolt** |exec-name<br />args<br />fields |定義交易式認可者 Bolt。 它會執行與 hello 應用程式***exec 名稱***使用***args***。<br /><br />hello***欄位***是閃電的 hello 輸出欄位 |
| **nontx-topolopy** |topology-name<br />spout-map<br />bolt-map |定義非交易式拓撲 hello 拓撲，以名稱&nbsp;spouts 定義地圖與 hello 發射定義地圖 |
| **scp-spout** |exec-name<br />args<br />fields<br />參數 |定義非交易式 spout。 它會執行與 hello 應用程式***exec 名稱***使用***args***。<br /><br />hello***欄位***是 spout 的 hello 輸出欄位<br /><br />hello***參數***是選擇性的它使用 toospecify 某些參數，例如"nontransactional.ack.enabled"。 |
| **scp-bolt** |exec-name<br />args<br />fields<br />參數 |定義非交易式 Bolt。 它會執行與 hello 應用程式***exec 名稱***使用***args***。<br /><br />hello***欄位***是閃電的 hello 輸出欄位<br /><br />hello***參數***是選擇性的它使用 toospecify 某些參數，例如"nontransactional.ack.enabled"。 |

SCP.NET 定義下列關鍵字：

| **關鍵字** | **說明** |
| --- | --- |
| **:name** |定義 hello 拓撲名稱 |
| **:topology** |定義 hello 拓撲使用上述函式的 hello 和中的建置。 |
| **:p** |定義每個 spout 或閃電 hello 平行處理原則提示。 |
| **:config** |定義設定參數，或更新 hello 現有的 |
| **:schema** |定義 hello 結構描述的資料流。 |

還有常用參數：

| **參數** | **說明** |
| --- | --- |
| **"plugin.name"** |hello C# 外掛程式 exe 檔案名稱 |
| **"plugin.args"** |外掛程式引數 |
| **"output.schema"** |輸出結構描述 |
| **"nontransactional.ack.enabled"** |非交易式拓撲是否啟用認可 |

hello runspec 命令將會部署與 hello 位元，hello 使用量就像是：

    .\bin\runSpec.cmd
    usage: runSpec [spec-file target-dir [resource-dir] [-cp classpath]]
    ex: runSpec examples\HelloWorld\HelloWorld.spec specs examples\HelloWorld\Target

hello***資源-dir***參數是選擇性的您需要 toospecify 時想 tooplug C\# hello 應用程式、 hello 相依性和組態，則將會包含應用程式，而此目錄。

hello ***classpath***也是選擇性參數。 如果 hello 規格檔案包含 Java Spout 或閃電，則使用的 toospecify hello Java classpath。

## <a name="miscellaneous-features"></a>其他功能
### <a name="input-and-output-schema-declaration"></a>輸入和輸出結構描述宣告
hello 使用者可發出 C 中的 tuple\#處理、 hello 平台需要 tooserialize hello tuple 成 byte []、 傳輸 tooJava 端，以及 Storm 會傳輸此 tuple toohello 的目標。 同時在下游元件 hello C\#程序將會接收 tuple 從 java 端，並將它轉換 toohello 原始型別平台，所有這些作業會隱藏 hello 平台。

toosupport hello 序列化和還原序列化，使用者程式碼需要 hello 輸入和輸出的 toodeclare hello 結構描述。

hello 輸入/輸出資料流之結構描述是定義為字典，hello 金鑰為 hello StreamId hello 值為 hello hello 資料行類型。 hello 元件可以有多個宣告的資料流。

    public class ComponentStreamSchema
    {
        public Dictionary<string, List<Type>> InputStreamSchema { get; set; }
        public Dictionary<string, List<Type>> OutputStreamSchema { get; set; }
        public ComponentStreamSchema(Dictionary<string, List<Type>> input, Dictionary<string, List<Type>> output)
        {
            InputStreamSchema = input;
            OutputStreamSchema = output;
        }
    }


在內容物件有的 hello 加入下列 API:

    public void DeclareComponentSchema(ComponentStreamSchema schema)

使用者程式碼必須確定發出 hello tuple 遵守 hello，該資料流所定義的結構描述或 hello 系統將會擲回執行階段例外狀況。

### <a name="multi-stream-support"></a>多重串流支援
SCP 支援使用者程式碼 tooemit，或是接收來自多個不同的資料流 hello 在相同的時間。 hello 支援反映 hello 內容物件中 hello 發出方法會接受選擇性的資料流識別碼參數。

已加入 hello SCP.NET 內容物件中的兩個方法。 它們是使用的 tooemit Tuple 或 Tuple toospecify StreamId。 hello StreamId 是字串，而且它需要 toobe 一致，在這兩個 C\#和 hello 拓撲定義規格。

        /* Emit tuple toohello specific stream. */
        public abstract void Emit(string streamId, List<object> values);

        /* for non-transactional Spout only */
        public abstract void Emit(string streamId, List<object> values, long seqId);

hello 發出 tooa 不存在的資料流將導致執行階段例外狀況。

### <a name="fields-grouping"></a>欄位分組
內建欄位群組在 Strom 運作不正確 SCP.NET 中的 hello。 Hello Java Proxy 側邊，在所有 hello 欄位資料型別都是實際 byte []，並分組 hello 欄位使用 hello 位元組 [] 物件的雜湊程式碼 tooperform hello 群組。 hello 位元組 [] 物件的雜湊程式碼是此物件在記憶體中的 hello 位址。 因此 hello 群組會是錯誤的兩個位元組 [] 的物件相同的內容，但不是 hello 相同的位址，該共用 hello。

SCP.NET 加入自訂的群組的方法，它會使用 hello hello 位元組 [] toodo hello 群組內容。 在**規格**檔案，就像是 hello 語法：

    (bolt-spec
        {
            "spout_test" (scp-field-group :non-tx [0,1])
        }
        …
    )


在這裡，

1. “scp-field-group” 表示「SCP 實作的自訂欄位分組」。
2. “:tx” 或 “:non-tx” 表示是否為交易式拓撲。 由於 hello 的起始索引與非 tx 拓撲不同 tx 中，我們需要這項資訊。
3. [0,1] 表示欄位 Id 的雜湊集，從 0 開始。

### <a name="hybrid-topology"></a>混合式拓撲
原生 Storm 以 Java 撰寫的 hello。 和 SCP.Net 已經增強，它 tooenable 我們自訂 toowrite C\#程式碼 toohandle 其商務邏輯。 但我們也支援混合式拓撲，不僅包含 C\# spout/bolt，也包含 Java Spout/Bolt。

### <a name="specify-java-spoutbolt-in-spec-file"></a>在規格檔中指定 Java Spout/Bolt
在規格的檔案中，「 scp spout"和"scp 閃電 」 也可以使用的 toospecify Java Spouts 和攻擊，範例如下：

    (spout-spec 
      (microsoft.scp.example.HybridTopology.Generator.)           
      :p 1)

這裡`microsoft.scp.example.HybridTopology.Generator`hello hello Java Spout 類別名稱。

### <a name="specify-java-classpath-in-runspec-command"></a>在 runSpec 命令中指定 Java 類別路徑
如果您想包含 Java Spouts 或發射 toosubmit 拓撲時，您需要使用 Java Spouts toofirst 編譯 hello 或攻擊，並取得 hello Jar 檔案。 接著，您應該指定 hello java classpath 提交拓撲時，包含 hello Jar 檔案。 下列是一個範例：

    bin\runSpec.cmd examples\HybridTopology\HybridTopology.spec specs examples\HybridTopology\net\Target -cp examples\HybridTopology\java\target\*

這裡**範例\\HybridTopology\\java\\目標\\** hello 資料夾包含 hello Java Spout/閃電 Jar 檔案。

### <a name="serialization-and-deserialization-between-java-and-c"></a>Java 與 C\ 之間的序列化和還原序列化
我們的 SCP 元件包含 Java 和 C\# 端。 順序 toointeract 與原生 Java Spouts/攻擊，序列化/還原序列化必須執行時，在 Java 側邊與 C 之間\#端 hello 下列圖表所示。

![java 元件傳送 tooSCP 元件傳送 tooJava 元件的圖表](media/hdinsight-storm-scp-programming-guide/java-compent-sending-to-scp-component-sending-to-java-component.png)

1. **Java 端序列化和 C\# 端還原序列化**
   
   首次，我們提供 Java 端序列化和 C\# 端還原序列化的預設實作。 Java 端中的 hello 序列化方法可加以指定規格的檔案中：
   
       (scp-bolt
           {
               "plugin.name" "HybridTopology.exe"
               "plugin.args" ["displayer"]
               "output.schema" {}
               "customized.java.serializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer"]
           })
   
   還原序列化方法，在 C 中的 hello\#端應該指定在 C 中\#使用者程式碼：
   
       Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
       inputSchema.Add("default", new List<Type>() { typeof(Person) });
       this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, null));
       this.ctx.DeclareCustomizedDeserializer(new CustomizedInteropJSONDeserializer());            
   
   這個預設實作應該處理大部分的情況下，如果 hello 資料類型不是太複雜。 某些情況下，可能是因為 hello 使用者資料型別是過於複雜、 或 hello 效能在我們的預設實作不符合 hello 使用者的需求，使用者可以外掛程式自己的實作。
   
   hello 序列化介面端定義為在 java 中：
   
       public interface ICustomizedInteropJavaSerializer {
           public void prepare(String[] args);
           public List<ByteBuffer> serialize(List<Object> objectList);
       }
   
   hello 還原序列化介面，在 C 中\#端定義為：
   
   公用介面 ICustomizedInteropCSharpDeserializer
   
       public interface ICustomizedInteropCSharpDeserializer
       {
           List<Object> Deserialize(List<byte[]> dataList, List<Type> targetTypes);
       }
2. **C\# 端序列化和 Java 端還原序列化**
   
   hello C 中的序列化方法\#端應該指定在 C 中\#使用者程式碼：
   
       this.ctx.DeclareCustomizedSerializer(new CustomizedInteropJSONSerializer()); 
   
   hello Java 端中的還原序列化方法應指定規格的檔案中：
   
     (scp-spout
   
       {
         "plugin.name" "HybridTopology.exe"
         "plugin.args" ["generator"]
         "output.schema" {"default" ["person"]}
         "customized.java.deserializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" "microsoft.scp.example.HybridTopology.Person"]
       })
   
   這裡"microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer"hello 還原序列化程式，名稱，而 「 microsoft.scp.example.HybridTopology.Person"hello 目標類別 hello 資料還原序列化。
   
   使用者也可以外掛其自己實作的 C\# 序列化程式和 Java Deserializer。 這是 C hello 介面\#序列化程式：
   
       public interface ICustomizedInteropCSharpSerializer
       {
           List<byte[]> Serialize(List<object> dataList);
       }
   
   這是 Java 還原序列化程式的 hello 介面：
   
       public interface ICustomizedInteropJavaDeserializer {
           public void prepare(String[] targetClassNames);
           public List<Object> Deserialize(List<ByteBuffer> dataList);
       }

## <a name="scp-host-mode"></a>SCP 主機模式
在此模式中，使用者可以編譯它們代碼 tooDLL，，並使用 SCPHost.exe SCP toosubmit 拓撲所提供。 hello 規格檔案看起來像這樣：

    (scp-spout
      {
        "plugin.name" "SCPHost.exe"
        "plugin.args" ["HelloWorld.dll" "Scp.App.HelloWorld.Generator" "Get"]
        "output.schema" {"default" ["sentence"]}
      })

其中，`plugin.name` 指定為 SCP SDK 所提供的 `SCPHost.exe`。 SCPHost.exe 只接受三個參數：

1. hello 第一次是 hello DLL 名稱，亦即`"HelloWorld.dll"`在此範例中。
2. hello 第二個是 hello 類別名稱，亦即`"Scp.App.HelloWorld.Generator"`在此範例中。
3. hello 第三個是 hello 的公用靜態方法，它可以是叫用的 tooget ISCPPlugin 的執行個體的名稱。

在主機模式中，使用者程式碼會編譯成 DLL，供 SCP 平台叫用。 因此 SCP 平台可以得到 hello 整個處理邏輯的完整控制權。 因此，建議客戶 SCP 主機模式 toosubmit 拓撲因為它可以簡化 hello 開發經驗，以及較新版本的更多的彈性和更好的回溯相容性帶我們。

## <a name="scp-programming-examples"></a>SCP 程式設計範例
### <a name="helloworld"></a>HelloWorld
**HelloWorld**是非常簡單的範例 tooshow SCP.Net 的功用。 它使用非交易拓撲，具有一個名為 **generator** 的 spout，以及名為 **splitter** 和 **counter** 的兩個 bolt。 hello spout**產生器**將隨機產生某些句子，並發出這些句子太**分隔器**。 hello 閃電**分隔器**會分割 hello 句子 toowords 和發出這些字太**計數器**閃電。 hello 閃電"counter"會使用每個字組的字典 toorecord hello 發生次數。

此範例有兩個規格檔：**HelloWorld.spec** 和 **HelloWorld\_EnableAck.spec**。 在 hello C\#程式碼，它可以找出是否藉由取得 hello pluginConf Java 來自啟用通知。

    /* demo how tooget pluginConf info */
    if (Context.Config.pluginConf.ContainsKey(Constants.NONTRANSACTIONAL_ENABLE_ACK))
    {
        enableAck = (bool)(Context.Config.pluginConf[Constants.NONTRANSACTIONAL_ENABLE_ACK]);
    }
    Context.Logger.Info("enableAck: {0}", enableAck);

Hello spout 中啟用通知時，字典有尚未 acked 使用的 toocache hello tuple。 如果呼叫 Fail()，hello 失敗的 tuple 重新執行：

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        Context.Logger.Info("Fail, seqId: {0}", seqId);
        if (cachedTuples.ContainsKey(seqId))
        {
            /* get hello cached tuple */
            string sentence = cachedTuples[seqId];

            /* replay hello failed tuple */
            Context.Logger.Info("Re-Emit: {0}, seqId: {1}", sentence, seqId);
            this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), seqId);
        }
        else
        {
            Context.Logger.Warn("Fail(), can't find cached tuple for seqId {0}!", seqId);
        }
    }

### <a name="helloworldtx"></a>HelloWorldTx
hello **HelloWorldTx**範例將示範如何 tooimplement 交易式拓撲。 它有一個名為 **generator** 的 spout，一個名為 **partial-count** 的批次 bolt，以及一個名為 **count-sum** 的認可 bolt。 另外還有三個預先建立的 txt 檔案︰**DataSource0.txt**、**DataSource1.txt**、**DataSource2.txt**。

在每個交易中，hello spout**產生器**會隨機選擇兩個檔案從 hello 預先建立的三個檔案，並發出 hello 兩個檔案名稱 toohello**部分計數**閃電。 hello 閃電**部分計數**會先收到 hello tuple，然後開啟 hello 檔案和計數 hello 數字從取得 hello 檔案名稱，這個檔案中，以及最後發出 hello 文字數字 toohello**計數總和**閃電。 hello**計數總和**閃電將摘要說明 hello 總計數。

tooachieve**正好一次**語意、 hello 認可閃電**計數總和**需要 toojudge 是否在重新執行的交易。 在此範例中，它有一個靜態成員變數：

    public static long lastCommittedTxId = -1; 

建立 ISCPBatchBolt 執行個體時，它會取得 hello`txAttempt`從輸入參數：

    public static CountSum Get(Context ctx, Dictionary<string, Object> parms)
    {
        /* for transactional topology, we can get txAttempt from hello input parms */
        if (parms.ContainsKey(Constants.STORM_TX_ATTEMPT))
        {
            StormTxAttempt txAttempt = (StormTxAttempt)parms[Constants.STORM_TX_ATTEMPT];
            return new CountSum(ctx, txAttempt);
        }
        else
        {
            throw new Exception("null txAttempt");
        }
    }

當`FinishBatch()`呼叫時，hello`lastCommittedTxId`如果它不是重新執行的交易將會更新。

    public void FinishBatch(Dictionary<string, Object> parms)
    {
        /* judge whether it is a replayed transaction? */
        bool replay = (this.txAttempt.TxId <= lastCommittedTxId);

        if (!replay)
        {
            /* If it is not replayed, update hello toalCount and lastCommittedTxId vaule */
            totalCount = totalCount + this.count;
            lastCommittedTxId = this.txAttempt.TxId;
        }
        … …
    }


### <a name="hybridtopology"></a>HybridTopology
此拓撲包含 Java Spout 和 C\# Bolt。 它會使用 hello 預設序列化和還原序列化實作 SCP 平台所提供。 請 ref hello **HybridTopology.spec**中**範例\\HybridTopology** hello 規格檔案的詳細資訊，資料夾和**SubmitTopology.bat**的方式toospecify Java classpath。

### <a name="scphostdemo"></a>SCPHostDemo
在本質上這個範例是 hello 與 HelloWorld 相同。 hello 只差別 hello 使用者程式碼會編譯為 DLL，並使用 SCPHost.exe 送出 hello 拓撲。 如需詳細說明，請 ref hello > 一節 「 SCP 主機模式 」。

## <a name="next-steps"></a>後續步驟
建立使用 SCP 的 Storm 拓撲的範例，請參閱 hello 下列：

* [使用 Visual Studio 開發 Apache Storm on HDInsight 的 C# 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [利用 Storm on HDInsight 處理 Azure 事件中心的事件](hdinsight-storm-develop-csharp-event-hub-topology.md)
* [在 C# Storm 拓樸中建立多個資料流](hdinsight-storm-twitter-trending.md)
* [使用 Storm 拓撲從 Power Bi toovisualize 資料](hdinsight-storm-power-bi-topology.md)
* [使用 Storm on HDInsight 處理事件中心的車輛感應器資料](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/IotExample)
* [擷取、 轉換及載入 (ETL) 從 Azure 事件中心 tooHBase](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample)
* [在 HDInsight 上使用 Storm 和 HBase 讓事件相互關聯](hdinsight-storm-correlation-topology.md)

