---
title: "使用 Azure 服務匯流排 aaa.NET 多層式應用程式 |Microsoft 文件"
description: ".NET 教學課程，可協助您開發使用服務匯流排佇列 toocommunicate 各層之間的 Azure 中的多層式應用程式。"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1b8608ca-aa5a-4700-b400-54d65b02615c
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 04/11/2017
ms.author: sethm
ms.openlocfilehash: 485910ff1d3b8b0a709ee14ede32e57cf873829a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="net-multi-tier-application-using-azure-service-bus-queues"></a>使用 Azure 服務匯流排佇列的 .NET 多層應用程式
## <a name="introduction"></a>簡介
開發 Microsoft Azure 很容易使用 Visual Studio 和 hello 免費 Azure SDK for.NET。 本教學課程中引導您完成 hello 步驟 toocreate 使用多個在本機環境中執行的 Azure 資源的應用程式。

您將學習下列 hello:

* 如何 tooenable 進行 Azure 開發以單一電腦下載並安裝。
* 如何將 Visual Studio toodevelop toouse azure。
* 如何 toocreate 使用 web 和背景工作角色在 Azure 中的多層式應用程式。
* 如何使用服務匯流排佇列的 toocommunicate 之間層。

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

在本教學課程中，您會建置並執行 Azure 雲端服務中的 hello 多層式應用程式。 hello 前端是 ASP.NET MVC web 角色，且 hello 後端會使用服務匯流排佇列背景工作角色。 您可以建立 hello 相同多層式的應用程式與 hello 前端的 web 專案，部署的 tooan Azure 的網站，而不是雲端服務。 您也可以試用 hello [.NET 在內部部署/雲端的混合式應用程式](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md)教學課程。

hello 下列螢幕擷取畫面顯示 hello 完成應用程式。

![][0]

## <a name="scenario-overview-inter-role-communication"></a>案例概觀：內部角色通訊
toosubmit 處理 hello 前端 UI 元件，在 hello web 角色中，執行的順序必須與 hello 中間層邏輯 hello 背景工作角色執行互動。 這個範例會使用服務匯流排訊息 hello hello 各層之間的通訊。

使用服務匯流排傳訊 hello web 和中介層之間可分隔的兩個元件。 相較之下 toodirect 訊息 （也就是 TCP 或 HTTP） hello web 層未直接; 連接 toohello 中介層而是它推入工作單位，做為訊息，到 Service Bus 可靠地保留它們，直到準備好 tooconsume hello 中介層並進行處理。

服務匯流排提供兩個實體 toosupport 代理傳訊： 佇列和主題。 每個訊息佇列，傳送 toohello 佇列由單一接收者。 主題也支援每個發佈的訊息可提供 tooa 註冊 hello 主題的訂用帳戶中的 hello 發行/訂閱的模式。 每個訂閱在邏輯上會維護自己的訊息佇列。 訂閱也可以設定限制 hello 集到的訊息傳遞 hello 訂閱佇列 toothose 符合 hello 篩選條件的篩選規則。 hello 下列範例會使用服務匯流排佇列。

![][1]

此通訊機制具有數個超越直接傳訊的優點：

* **暫時分離。** 與 hello 非同步訊息模式中，產生者和消費者不需要在 hello 線上相同的時間。 服務匯流排可靠地儲存訊息，直到 hello 取用方準備要接收訊息。 這可讓 hello hello 分散式應用程式 toobe 中斷連接，可能是主動，例如，為了進行維護，或因為 tooa 元件損毀，而不會影響整體系統元件。 此外，hello 取用應用程式可能只需要線上 toocome hello 一天的特定時間。
* **負載調節。** 在許多應用程式，系統負載會隨著時間改變時所需的每個工作單位的 hello 處理時間通常不變。 調解訊息產生者和消費者與佇列表示取用應用程式 （hello 背景工作） 只需要 toobe 該 hello 佈建 tooaccommodate 平均負載，而非尖峰負載。 hello 深度 hello 佇列成長，且合約會隨著 hello 連入負載而改變。 這可直接節省金錢根據提供的基礎結構需要的 tooservice hello 應用程式負載 hello 數量。
* **負載平衡。** 隨著負載增加，多個背景工作處理序可以加入 tooread hello 佇列中。 只有其中一個 hello 背景工作處理序處理每個訊息。 此外，此提取為基礎的負載平衡可讓最有效地利用 hello 工作者機器即使背景工作電腦各有不同，根據處理能力，因為它們會在他們自己的最大速率提取訊息。 此模式通常稱為 hello*競爭取用者*模式。
  
  ![][2]

hello 下列各節討論 hello 實作程式碼，此架構。

## <a name="set-up-hello-development-environment"></a>設定 hello 開發環境
您可以開始開發 Azure 應用程式之前，取得 hello 工具，並設定您的開發環境。

1. 安裝 hello Azure SDK for.NET，從 hello SDK[下載頁面](https://azure.microsoft.com/downloads/)。
2. 在 hello **.NET**資料行中，按一下 hello 版本[Visual Studio](http://www.visualstudio.com)您使用。 hello 步驟在此教學課程使用 Visual Studio 2015，但也可使用 Visual Studio 2017。
3. 當系統提示 toorun 或儲存 hello 安裝程式時，按一下**執行**。
4. 在 hello **Web Platform Installer**，按一下 **安裝**並繼續進行 hello 安裝。
5. Hello 安裝完成之後，您將會擁有一切所需的 toostart toodevelop hello 應用程式。 hello SDK 包含工具，讓您輕鬆地開發 Visual Studio 中的 Azure 應用程式。

## <a name="create-a-namespace"></a>建立命名空間
hello 下一個步驟是 toocreate 服務命名空間，和取得共用存取簽章 (SAS) 金鑰。 命名空間會為每個透過服務匯流排公開的應用程式提供應用程式界限。 建立命名空間時，會產生 hello 系統 SAS 金鑰。 命名空間和 SAS 金鑰的 hello 組合提供服務匯流排 tooauthenticate 存取 tooan 應用程式的 hello 認證。

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-web-role"></a>建立 Web 角色
在本節中，建立 hello 前端應用程式。 首先，您會建立您的應用程式會顯示 hello 頁面。
在這之後，加入程式碼送出項目 tooa Service Bus 佇列，並顯示 hello 佇列的相關狀態資訊。

### <a name="create-hello-project"></a>建立 hello 專案
1. 使用系統管理員權限，請啟動 Visual Studio： 以滑鼠右鍵按一下 hello **Visual Studio**程式圖示，然後按一下**系統管理員身分執行**。 hello Azure 計算模擬器中，將在本文中，稍後討論需要 Visual Studio 會使用系統管理員權限來啟動。
   
   在 Visual Studio 中的 hello**檔案**功能表上，按一下 **新增**，然後按一下**專案**。
2. 從 已安裝的範本 的 Visual C# 下，按一下 雲端，然後按一下Azure 雲端服務。 名稱 hello 專案**MultiTierApp**。 然後按一下 [確定] 。
   
   ![][9]
3. 從 **.NET Framework 4.5** 角色中，按兩下 [ASP.NET Web 角色]。
   
   ![][10]
4. 將滑鼠停留在**WebRole1**下**Azure 雲端服務方案**、 按一下 hello 鉛筆圖示，和 hello web 角色重新命名過**FrontendWebRole**。 然後按一下 [確定] 。 (請確定您輸入 "Frontend"，其中 e 為小寫，而不是 "FrontEnd"。)
   
   ![][11]
5. 從 hello**新增 ASP.NET 專案**對話方塊中的，在 hello**選取範本**清單中，按一下**MVC**。
   
   ![][12]
6. 仍在 hello**新增 ASP.NET 專案**對話方塊方塊中，按一下 hello**變更驗證** 按鈕。 在 hello**變更驗證**對話方塊中，按一下**非驗證**，然後按一下**確定**。 在本教學課程中，您會部署不需要使用者登入的應用程式。
   
    ![][16]
7. 在 hello**新增 ASP.NET 專案**對話方塊中，按一下 **確定**toocreate hello 專案。
8. 在**方案總管] 中**，在 hello **FrontendWebRole**專案中，以滑鼠右鍵按一下**參考**，然後按一下 [**管理 NuGet 封裝**。
9. 按一下 hello**瀏覽**索引標籤，然後搜尋`Microsoft Azure Service Bus`。 選取 hello **WindowsAzure.ServiceBus**封裝中，按一下 **安裝**，並接受使用規定 hello。
   
   ![][13]
   
   請注意該 hello 需要用戶端組件現在會參考與已新增一些新的程式碼檔案。
10. 在 [方案總管] 中，於 [模型] 上按一下滑鼠右鍵、按一下 [新增]，再按一下 [類別]。 在 [hello**名稱**] 方塊中，輸入 hello 名稱**OnlineOrder.cs**。 然後按一下 [ **新增**]。

### <a name="write-hello-code-for-your-web-role"></a>撰寫您的 web 角色的 hello 程式碼
在本節中，您建立 hello 會顯示您的應用程式的各個頁面。

1. 在 Visual Studio 中的 hello OnlineOrder.cs 檔案，取代現有的命名空間定義以下列程式碼的 hello:
   
   ```csharp
   namespace FrontendWebRole.Models
   {
       public class OnlineOrder
       {
           public string Customer { get; set; }
           public string Product { get; set; }
       }
   }
   ```
2. 在 [方案總管] 中，按兩下 [Controllers\HomeController.cs]。 新增下列 hello**使用**在 hello hello 最上方的陳述式檔案適用於您剛剛建立，以及服務匯流排的模型 tooinclude hello 命名空間。
   
   ```csharp
   using FrontendWebRole.Models;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   ```
3. 也在 Visual Studio 中的 hello HomeController.cs 檔案，取代現有的命名空間定義 hello 下列程式碼。 這個程式碼包含的方法來處理 hello 送出的項目 toohello 佇列。
   
   ```csharp
   namespace FrontendWebRole.Controllers
   {
       public class HomeController : Controller
       {
           public ActionResult Index()
           {
               // Simply redirect tooSubmit, since Submit will serve as the
               // front page of this application.
               return RedirectToAction("Submit");
           }
   
           public ActionResult About()
           {
               return View();
           }
   
           // GET: /Home/Submit.
           // Controller method for a view you will create for hello submission
           // form.
           public ActionResult Submit()
           {
               // Will put code for displaying queue message count here.
   
               return View();
           }
   
           // POST: /Home/Submit.
           // Controller method for handling submissions from hello submission
           // form.
           [HttpPost]
           // Attribute toohelp prevent cross-site scripting attacks and
           // cross-site request forgery.  
           [ValidateAntiForgeryToken]
           public ActionResult Submit(OnlineOrder order)
           {
               if (ModelState.IsValid)
               {
                   // Will put code for submitting tooqueue here.
   
                   return RedirectToAction("Submit");
               }
               else
               {
                   return View(order);
               }
           }
       }
   }
   ```
4. 從 hello**建置**功能表上，按一下 **建置方案**tootest hello 精確度的工作為止。
5. 現在，建立 hello hello 檢視`Submit()`您稍早建立的方法。 Hello 內以滑鼠右鍵按一下`Submit()`方法 (hello 多載`Submit()`，不接受任何參數)，然後選擇 **加入檢視**。
   
   ![][14]
6. 建立 hello 檢視會出現的對話方塊。 在 hello**範本**清單中，選擇**建立**。 在 hello**模型類別**清單中，按一下 hello **OnlineOrder**類別。
   
   ![][15]
7. 按一下 [新增] 。
8. 現在，變更 hello 顯示應用程式的名稱。 在**方案總管 中**，連按兩下**_layout.cshtml\\_Layout.cshtml**檔案 tooopen hello Visual Studio 編輯器中。
9. 將所有出現的 **My ASP.NET Application** 取代為 **LITWARE'S Products**。
10. 移除 hello**首頁**，**有關**，和**連絡人**連結。 刪除 hello 反白顯示程式碼：
    
    ![][28]
11. 最後，修改 hello 送出頁面 tooinclude 某些 hello 佇列的相關資訊。 在**方案總管 中**，連按兩下**Views\Home\Submit.cshtml**檔案 tooopen hello Visual Studio 編輯器中。 新增下列一行之後 hello `<h2>Submit</h2>`。 現在，hello`ViewBag.MessageCount`是空的。 稍後您將在其中填入資料。
    
    ```html
    <p>Current number of orders in queue waiting toobe processed: @ViewBag.MessageCount</p>
    ```
12. 您現在已實作 UI。 您可以按**F5** toorun 您的應用程式，並確認它看起來正常。
    
    ![][17]

### <a name="write-hello-code-for-submitting-items-tooa-service-bus-queue"></a>撰寫 hello 送出項目 tooa 服務匯流排佇列的程式碼
現在，加入送出項目 tooa 佇列的程式碼。 首先，您會建立一個類別，並使其包含服務匯流排佇列連接資訊。 接著，從 Global.aspx.cs 初始化您的連線。 最後，更新您建立稍早在 HomeController.cs tooactually 送出項目 tooa 服務匯流排佇列中的 hello 提交程式碼。

1. 在**方案總管 中**，以滑鼠右鍵按一下**FrontendWebRole** （以滑鼠右鍵按一下 hello 專案，不 hello 角色）。 按一下 新增，然後按一下類別。
2. Hello 類別命名**QueueConnector.cs**。 按一下**新增**toocreate hello 類別。
3. 現在，加入程式碼，用以封裝 hello 連接資訊和初始化 hello 連線 tooa 服務匯流排佇列。 Hello，下列程式碼中，以取代 QueueConnector.cs hello 整個內容，並輸入值`your Service Bus namespace`（命名空間名稱） 和`yourKey`，也就是 hello**主索引鍵**您先前取得的 hello Azure入口網站。
   
   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Web;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   
   namespace FrontendWebRole
   {
       public static class QueueConnector
       {
           // Thread-safe. Recommended that you cache rather than recreating it
           // on every request.
           public static QueueClient OrdersQueueClient;
   
           // Obtain these values from hello portal.
           public const string Namespace = "your Service Bus namespace";
   
           // hello name of your queue.
           public const string QueueName = "OrdersQueue";
   
           public static NamespaceManager CreateNamespaceManager()
           {
               // Create hello namespace manager which gives you access to
               // management operations.
               var uri = ServiceBusEnvironment.CreateServiceUri(
                   "sb", Namespace, String.Empty);
               var tP = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                   "RootManageSharedAccessKey", "yourKey");
               return new NamespaceManager(uri, tP);
           }
   
           public static void Initialize()
           {
               // Using Http toobe friendly with outbound firewalls.
               ServiceBusEnvironment.SystemConnectivity.Mode =
                   ConnectivityMode.Http;
   
               // Create hello namespace manager which gives you access to
               // management operations.
               var namespaceManager = CreateNamespaceManager();
   
               // Create hello queue if it does not exist already.
               if (!namespaceManager.QueueExists(QueueName))
               {
                   namespaceManager.CreateQueue(QueueName);
               }
   
               // Get a client toohello queue.
               var messagingFactory = MessagingFactory.Create(
                   namespaceManager.Address,
                   namespaceManager.Settings.TokenProvider);
               OrdersQueueClient = messagingFactory.CreateQueueClient(
                   "OrdersQueue");
           }
       }
   }
   ```
4. 現在，請確定會呼叫您的 **Initialize** 方法。 在 [方案總管] 中，按兩下 [Global.asax\Global.asax.cs]。
5. 新增下列一行程式碼結尾 hello hello hello **Application_Start**方法。
   
   ```csharp
   FrontendWebRole.QueueConnector.Initialize();
   ```
6. 最後，更新 hello 送出項目 toohello 佇列稍早建立的 web 程式碼。 在 [方案總管] 中，按兩下 [Controllers\HomeController.cs]。
7. 更新 hello`Submit()`方法 （hello 多載會採用任何參數），如下所示 tooget hello 訊息計數 hello 佇列。
   
   ```csharp
   public ActionResult Submit()
   {
       // Get a NamespaceManager which allows you tooperform management and
       // diagnostic operations on your Service Bus queues.
       var namespaceManager = QueueConnector.CreateNamespaceManager();
   
       // Get hello queue, and obtain hello message count.
       var queue = namespaceManager.GetQueue(QueueConnector.QueueName);
       ViewBag.MessageCount = queue.MessageCount;
   
       return View();
   }
   ```
8. 更新 hello`Submit(OnlineOrder order)`方法 （hello 多載會接受一個參數），如下所示 toosubmit 排序資訊 toohello 佇列。
   
   ```csharp
   public ActionResult Submit(OnlineOrder order)
   {
       if (ModelState.IsValid)
       {
           // Create a message from hello order.
           var message = new BrokeredMessage(order);
   
           // Submit hello order.
           QueueConnector.OrdersQueueClient.Send(message);
           return RedirectToAction("Submit");
       }
       else
       {
           return View(order);
       }
   }
   ```
9. 您現在可以執行一次 hello 應用程式。 每次提交訂單時，會增加 hello 訊息計數。
   
   ![][18]

## <a name="create-hello-worker-role"></a>建立 hello 背景工作角色
您即將建立 hello 處理 hello 順序送出的背景工作角色。 這個範例會使用 hello**具有服務匯流排佇列背景工作角色**Visual Studio 專案範本。 您已向 hello 入口網站取得 hello 所需的認證。

1. 請確定您已經連接 Visual Studio tooyour Azure 帳戶。
2. 在 Visual Studio 中**方案總管 中**以滑鼠右鍵按一下**角色**下 hello 資料夾**MultiTierApp**專案。
3. 按一下 新增，然後按一下新的背景工作角色專案。 hello**加入新的角色專案** 對話方塊隨即出現。
   
   ![][26]
4. 在 hello**加入新的角色專案**對話方塊中，按一下 **具有服務匯流排佇列背景工作角色**。
   
   ![][23]
5. 在 hello**名稱**方塊中，名稱 hello 專案**OrderProcessingRole**。 然後按一下 [ **新增**]。
6. 您在步驟 9 的 hello 「 建立服務匯流排命名空間 」 一節 toohello 剪貼簿中取得複製 hello 連接字串。
7. 在**方案總管 中**，以滑鼠右鍵按一下 hello **OrderProcessingRole**您在步驟 5 中建立 (請確定您按一下滑鼠右鍵**OrderProcessingRole**下**角色**，和不 hello 類別)。 然後按一下 [屬性]。
8. 在 [hello**設定**hello] 索引標籤**屬性**對話方塊中，按一下 hello 的內部**值**方塊**microsoft.servicebus.connectionstring 所指定**，然後貼上您在步驟 6 中複製的 hello 端點值。
   
   ![][25]
9. 建立**OnlineOrder**類別 toorepresent hello 訂單，為您從 hello 佇列處理它們。 您可以重複使用已建立的類別。 在**方案總管 中**，以滑鼠右鍵按一下 hello **OrderProcessingRole**類別 （以滑鼠右鍵按一下 hello 類別圖示，不 hello 角色）。 按一下 [新增]，然後按一下 [現有項目]。
10. 瀏覽 toohello 子資料夾**FrontendWebRole\Models**，然後按兩下**OnlineOrder.cs** tooadd 它 toothis 專案。
11. 在**WorkerRole.cs**，變更 hello hello 值**QueueName**變數從`"ProcessingQueue"`太`"OrdersQueue"`hello 下列程式碼所示。
    
    ```csharp
    // hello name of your queue.
    const string QueueName = "OrdersQueue";
    ```
12. 新增 hello 下列 using 陳述式在 hello hello WorkerRole.cs 檔案最上方。
    
    ```csharp
    using FrontendWebRole.Models;
    ```
13. 在 hello`Run()`函式，在 hello`OnMessage()`呼叫，取代 hello hello 內容`try`以下列程式碼的 hello 子句。
    
    ```csharp
    Trace.WriteLine("Processing", receivedMessage.SequenceNumber.ToString());
    // View hello message as an OnlineOrder.
    OnlineOrder order = receivedMessage.GetBody<OnlineOrder>();
    Trace.WriteLine(order.Customer + ": " + order.Product, "ProcessingMessage");
    receivedMessage.Complete();
    ```
14. 您已完成 hello 應用程式。 您可以測試 hello 完整的應用程式，以滑鼠右鍵按一下方案總管 中的 hello MultiTierApp 專案選取**設定為啟始專案**，然後按 F5。 請注意，訊息計數不會遞增，因為 hello 背景工作角色處理 hello 佇列中的項目，並將其標示為完成。 您可以藉由檢視 hello Azure 計算模擬器 UI 中看到 hello 追蹤輸出的背景工作角色。 您可以在 hello 工作列的通知區域中的 hello 模擬器圖示上按一下滑鼠右鍵，然後選取**顯示計算模擬器 UI**。
    
    ![][19]
    
    ![][20]

## <a name="next-steps"></a>後續步驟
toolearn 有關 Service Bus 的詳細資訊，請參閱下列資源的 hello:  

* [Azure 服務匯流排文件][sbdocs]  
* [服務匯流排服務頁面][sbacom]  
* [如何 tooUse Service Bus 佇列][sbacomqhowto]  

toolearn 有關多層式案例的詳細資訊，請參閱：  

* [使用儲存體資料表、佇列與 Blob 的 .NET 多層式應用程式][mutitierstorage]  

[0]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[1]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-100.png
[2]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-101.png
[9]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-10.png
[10]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-11.png
[11]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-02.png
[12]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-12.png
[13]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-13.png
[14]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-33.png
[15]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-34.png
[16]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-14.png
[17]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[18]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app2.png

[19]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-38.png
[20]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-39.png
[23]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRole1.png
[25]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRoleProperties.png
[26]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBNewWorkerRole.png
[28]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-40.png

[sbdocs]: /azure/service-bus-messaging/  
[sbacom]: https://azure.microsoft.com/services/service-bus/  
[sbacomqhowto]: service-bus-dotnet-get-started-with-queues.md  
[mutitierstorage]: https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36
