---
title: "aaaCreate 連接 tooAzure 服務的函式 |Microsoft 文件"
description: "使用 Azure 函式 toocreate 連接 tooother Azure 的無伺服器應用程式服務。"
services: functions
documentationcenter: dev-center-name
author: yochay
manager: manager-alias
editor: 
tags: 
keywords: "azure functions, 函式, 事件處理, webhook, 動態計算, 無伺服器架構"
ms.assetid: ab86065d-6050-46c9-a336-1bfc1fa4b5a1
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 9d1f7d3b236f8d2c1a404c76aee410f6d458fb7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-functions-toocreate-a-function-that-connects-tooother-azure-services"></a>使用 Azure 函式 toocreate 函式連接 tooother Azure 服務

本主題說明如何 toocreate 會接聽在 Azure 儲存體佇列和複製 hello toomessages 的 Azure 功能中的函式訊息 toorows Azure 儲存體資料表中。 計時器觸發函式是使用的 tooload 到 hello 佇列的訊息。 第二個函式會從 hello 佇列讀取，並將訊息 toohello 資料表。 Hello 佇列和 hello 資料表建立您的 Azure hello 繫結定義為基礎的函式。 

更有趣的 toomake 項目，一個函式以 JavaScript 撰寫並 hello 其他以 C# 指令碼。 這可示範函式應用程式如何擁有使用不同語言的函式。 

您可以看到 [Channel 9 影片](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player)中示範的這個案例。

## <a name="create-a-function-that-writes-toohello-queue"></a>建立將寫入 toohello 佇列的函式

您可以連接 tooa 儲存體佇列之前，您會需要 toocreate 載入 hello 訊息佇列的函式。 這個 JavaScript 函式會使用計時器觸發程序會寫入訊息 toohello 佇列每隔 10 秒。 如果您還沒有 Azure 帳戶，請參閱 hello[再試一次 Azure 函式](https://functions.azure.com/try)體驗，或[建立免費的 Azure 帳戶](https://azure.microsoft.com/free/)。

1. 請 toohello Azure 入口網站，並找出您的函式應用程式。

2. 按一下 [新增函式] > [TimerTrigger JavaScript]。 

3. 命名 hello 函式**FunctionsBindingsDemo1**，輸入 cron 運算式值為`0/10 * * * * *`如**排程**，然後按一下**建立**。
   
    ![新增計時器觸發函式](./media/functions-create-an-azure-connected-function/new-trigger-timer-function.png)

    您現在已建立會每隔 10 秒執行一次的計時器觸發函式。

5. 在 hello**開發**索引標籤上，按一下 **記錄檔**及檢視 hello 記錄檔中的 hello 活動。 您會看到每隔 10 秒寫入的記錄檔項目。
   
    ![檢視 hello 記錄 tooverify hello 函式運作方式](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-view-log.png)

## <a name="add-a-message-queue-output-binding"></a>新增訊息佇列輸出繫結

1. 在 hello**整合**索引標籤上，選擇**新輸出** > **Azure 佇列儲存體** > **選取**。

    ![新增觸發計時器函式](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab.png)

2. 輸入`myQueueItem`如**訊息參數名稱**和`functions-bindings`如**佇列名稱**，選取現有**儲存體帳戶連接**或按一下**新**toocreate 儲存體帳戶連接，然後按一下**儲存**。  

    ![建立 hello 輸出繫結 toohello 儲存體佇列](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab2.png)

1. 在 hello**開發**索引標籤上，新增下列程式碼 toohello 函式的 hello:
   
    ```javascript
   
    function myQueueItem() 
    {
        return {
            msg: "some message goes here",
            time: "time goes here"
        }
    }
   
    ```
2. 找出 hello*如果*陳述式的大約行 9 hello 函式，並插入 hello 下列程式碼會在該陳述式之後。
   
    ```javascript
   
    var toBeQed = myQueueItem();
    toBeQed.time = timeStamp;
    context.bindings.myQueueItem = toBeQed;
   
    ```  
   
    此程式碼建立**myQueueItem**並設定其**時間**屬性 toohello 目前時間戳記。 接著它會加入 hello 新佇列項目 toohello 內容的**myQueueItem**繫結。

3. 按一下 [儲存並執行]。

## <a name="view-storage-updates-by-using-storage-explorer"></a>使用儲存體總管來檢視儲存體更新
您可以確認您的函式正在檢視您所建立的 hello 佇列中的訊息。  您可以使用 Visual Studio 中的 Cloud Explorer 來連線 tooyour 儲存體佇列。 不過，hello 入口網站可讓您輕鬆 tooconnect tooyour 儲存體帳戶使用 Microsoft Azure 儲存體總管。

1. 在 hello**整合**索引標籤上，按一下您的佇列輸出繫結 >**文件**，然後取消隱藏 hello 連接字串儲存體帳戶，並複製 hello 值。 您使用此值 tooconnect tooyour 儲存體帳戶。

    ![下載 Azure 儲存體總管](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab3.png)


2. 如果您還沒有這麼做，請下載並安裝 [Microsoft Azure 儲存體總管](http://storageexplorer.com)。 
 
3. 按一下 [儲存體總管] 中的 hello 連接 tooAzure 儲存體圖示、 在 hello 欄位中，貼上 hello 連接字串並完成 hello 精靈。

    ![儲存體總管新增連接](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-storage-explorer.png)

4. 在下**本機和附加**，依序展開**儲存體帳戶**> 儲存體帳戶 >**佇列** > **函式繫結**並確認訊息會寫入 toohello 佇列。

    ![Hello 佇列中訊息的檢視](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer.png)

    如果 hello 佇列不存在，或為空白，則最有可能您函式繫結或程式碼發生問題。

## <a name="create-a-function-that-reads-from-hello-queue"></a>建立從 hello 佇列讀取的函式

既然您已加入 toohello 佇列的訊息時，您可以建立另一個函式會從 hello 佇列讀取和寫入 hello 訊息永久 tooan Azure 儲存體資料表。

1. 按一下 [新增函式] > [QueueTrigger-CSharp]。 
 
2. 命名 hello 函式`FunctionsBindingsDemo2`，輸入**函式繫結**在 hello**佇列名稱**欄位中，選取現有的儲存體帳戶或建立一個，，然後按一下**建立**.

    ![新增輸出佇列計時器函式](./media/functions-create-an-azure-connected-function/function-demo2-new-function.png) 

3. （選擇性）您可以確認 hello 新函式運作方式是在做為之前的存放裝置總管 中檢視 hello 新佇列。 您也可以使用 Visual Studio 中的雲端總管。  

4. （選擇性）重新整理 hello**函式繫結**排入佇列，並注意從 hello 佇列已經移除項目。 hello 移除會發生 hello 函式繫結的 toohello**函式繫結**輸入觸發程序和 hello 函式讀取 hello 佇列的佇列。 
 
## <a name="add-a-table-output-binding"></a>新增資料表輸出繫結

1. 在 FunctionsBindingsDemo2 中，按一下 [整合] > [新增輸出] > [Azure 資料表儲存體] > [選取]。

    ![新增繫結 tooan Azure 儲存體資料表](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab.png) 

2. 輸入 `functionbindings` 做為 資料表名稱 以及輸入 `myTable` 做為 資料表參數名稱，選擇 儲存體帳戶連線 或建立新的連線，然後按一下儲存。

    ![設定 hello 儲存體資料表繫結](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab2.png)
   
3. 在 hello**開發**索引標籤上，hello 現有函式程式碼取代 hello 下列：
   
    ```cs
    
    using System;
    
    public static void Run(QItem myQueueItem, ICollector<TableItem> myTable, TraceWriter log)
    {    
        TableItem myItem = new TableItem
        {
            PartitionKey = "key",
            RowKey = Guid.NewGuid().ToString(),
            Time = DateTime.Now.ToString("hh.mm.ss.ffffff"),
            Msg = myQueueItem.Msg,
            OriginalTime = myQueueItem.Time    
        };
        
        // Add hello item toohello table binding collection.
        myTable.Add(myItem);
    
        log.Verbose($"C# Queue trigger function processed: {myItem.RowKey} | {myItem.Msg} | {myItem.Time}");
    }
    
    public class TableItem
    {
        public string PartitionKey {get; set;}
        public string RowKey {get; set;}
        public string Time {get; set;}
        public string Msg {get; set;}
        public string OriginalTime {get; set;}
    }
    
    public class QItem
    {
        public string Msg { get; set;}
        public string Time { get; set;}
    }
    ```
    hello **TableItem**類別代表 hello 儲存體資料表中的資料列並加入 hello 項目 toohello`myTable`集合**TableItem**物件。 您必須設定 hello **PartitionKey**和**RowKey**屬性 toobe 無法 tooinsert hello 資料表。

4. 按一下 [儲存] 。  最後，您可以藉由檢視儲存體總管或 Visual Studio Cloud Explorer 中的 hello 資料表來確認 hello 函式可運作。

5. （選擇性）在儲存體帳戶在儲存體總管 中，依序展開**資料表** > **functionsbindings**並確認資料列會加入 toohello 資料表。 您可以在 Visual Studio 中的 Cloud Explorer 中 hello 相同。

    ![Hello 資料表中資料列的檢視](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer2.png)

    如果 hello 資料表不存在，或為空白，則最有可能您函式繫結或程式碼發生問題。 
 
[!INCLUDE [More binding information](../../includes/functions-bindings-next-steps.md)]

## <a name="next-steps"></a>後續步驟
如需 Azure 函式的詳細資訊，請參閱下列主題中的 hello:

* [Azure Functions 開發人員參考](functions-reference.md)  
  可供程式設計人員撰寫函數程式碼及定義觸發程序和繫結時參考。
* [測試 Azure Functions](functions-test-a-function.md)  
  說明可用於測試函式的各種工具和技巧。
* [如何 tooscale Azure 函式](functions-scale.md)  
  討論適用於 Azure 函式，包括 hello 耗用量主控方案，以及如何 toochoose hello 右計劃的服務方案。 

[!INCLUDE [Getting help note](../../includes/functions-get-help.md)]

