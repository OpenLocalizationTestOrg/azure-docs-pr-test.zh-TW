---
title: "教學課程：使用 Azure BizTalk 服務處理 EDIFACT 發票 | Microsoft Docs"
description: "如何 toocreate 並設定 hello 方塊連接器或應用程式開發介面應用程式在 Azure App Service 中的邏輯應用程式中使用"
services: biztalk-services
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: 
ms.assetid: 7e0b93fa-3e2b-4a9c-89ef-abf1d3aa8fa9
ms.service: biztalk-services
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/31/2016
ms.author: deonhe
ms.openlocfilehash: 4ca021c9084b9b6540c93ef15fc3d44be0966970
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-process-edifact-invoices-using-azure-biztalk-services"></a>教學課程：使用 Azure BizTalk 服務處理 EDIFACT 發票

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

您可以使用 hello BizTalk 服務入口網站 tooconfigure 和部署 X12 和 EDIFACT 協議。 在本教學課程中，我們會探討如何 toocreate 交換的 EDIFACT 協議發票交易夥伴之間。 本教學課程描述端對端商務方案，內容涉及兩個交易夥伴，分別是 Northwind 和 Contoso，他們會交換 EDIFACT 訊息。  

## <a name="sample-based-on-this-tutorial"></a>根據本教學課程所建立的範例
此教學課程以範例，**傳送 EDIFACT Invoices Using BizTalk Services**，也就是從 hello 可用 toodownload [MSDN Code Gallery](http://go.microsoft.com/fwlink/?LinkId=401005)。 您無法使用 hello 範例，並瀏覽此教學課程 toounderstand hello 範例的建置方式。 或者，您可以使用這個教學課程 toocreate 從頭自己的解決方案。 本教學課程的目標傾向 hello 第二種方法，讓您了解這個方案的建置方式。 此外，盡可能，hello 教學課程與 hello 範例一致，而且使用 hello 相同的 hello 範例中的成品 （例如，結構描述、 轉換） 名稱。  

> [!NOTE]
> 此解決方案牽涉到從 EAI 橋接器 tooan EDI 橋接器傳送訊息，因為它會重複使用 hello [BizTalk Services 橋接器鏈結範例](http://code.msdn.microsoft.com/BizTalk-Bridge-chaining-2246b104)範例。  
> 
> 

## <a name="what-does-hello-solution-do"></a>Hello 解決方案有哪些功能？
在此方案中，Northwind 會從 Contoso 收到 EDIFACT 發票。 這些發票未採用標準 EDI 格式。 因此，在傳送之前 hello 發票 tooNorthwind，它必須是已轉換的 tooan EDIFACT 發票 （也稱為 INVOIC） 文件。 在收到時，Northwind 必須處理 hello EDIFACT 發票，並傳回控制訊息 （也稱為 CONTRL） tooContoso。

![][1]  

tooachieve 此商務案例中，Contoso 會使用提供的 Microsoft Azure BizTalk 服務的 hello 功能。

* Contoso 使用 EAI 橋接器 tootransform hello 原始發票 tooEDIFACT INVOIC。
* hello EAI 橋接器接著會傳送 hello 訊息 tooan EDI 傳送橋接器部署 hello BizTalk 服務入口網站中設定之協議的一部分。
* hello EDI 傳送橋接器會處理 hello EDIFACT INVOIC 並將其路由 tooNorthwind。
* 之後收到 hello 發票，Northwind 會傳回 CONTRL 訊息 toohello EDI 接收橋接器部署為 hello 協議的一部分。  

> [!NOTE]
> （選擇性） 此解決方案也會示範如何批次處理 toosend hello toouse 發票批次，而不是個別傳送每張發票。  
> 
> 

toocomplete hello 案例中，我們會使用服務匯流排佇列 toosend 發票從 Contoso tooNorthwind，或從 Northwind 接收通知。 您可以使用用戶端應用程式，其可供下載，並包含在可用的 hello 範例套件中建立這些佇列做為本教學課程的一部分。  

## <a name="prerequisites"></a>必要條件
* 您必須具有服務匯流排命名空間。 如需建立命名空間的指示，請參閱 [作法：建立或修改服務匯流排服務命名空間](https://msdn.microsoft.com/library/azure/hh674478.aspx)。 讓我們假設您已佈建服務匯流排命名空間，且其名稱為 **edifactbts**。
* 您必須擁有 BizTalk 服務訂用帳戶。 如需相關指示，請參閱 [使用 Azure 傳統入口網站建立 BizTalk 服務](http://go.microsoft.com/fwlink/?LinkID=302280)。 在本教學課程中，讓我們假設您擁有 BizTalk 服務訂用帳戶，且其名稱為 **contosowabs**。
* 註冊您的 BizTalk 服務訂閱 hello BizTalk 服務入口網站上。 如需指示，請參閱[註冊 hello BizTalk 服務入口網站上的 BizTalk 服務部署](https://msdn.microsoft.com/library/hh689837.aspx)
* 您必須安裝 Visual Studio。
* 您必須安裝 BizTalk 服務 SDK。 您可以下載 hello 從 SDK [http://go.microsoft.com/fwlink/?LinkId=235057](http://go.microsoft.com/fwlink/?LinkId=235057)  

## <a name="step-1-create-hello-service-bus-queues"></a>步驟 1： 建立 hello 服務匯流排佇列
此解決方案會使用交易夥伴之間的服務匯流排佇列 tooexchange 訊息。 Contoso 與 Northwind 從傳送訊息 toohello 佇列 hello EAI 和/或 EDI 橋接器位置使用它們。 在此方案中，您需要三個服務匯流排佇列：

* **northwindreceive** – Northwind hello 發票從 Contoso 接收透過此佇列。
* **contosoreceive** -Contoso 透過此佇列從 Northwind 接收 hello 通知。
* **暫止**-所有擱置的訊息會路由的 toothis 佇列。 如果訊息在處理期間失敗，則會加以擱置。

您可以使用 hello 範例封裝中包含的用戶端應用程式建立服務匯流排佇列。  

1. 從您下載 hello 範例的 hello 位置，開啟**教學課程傳送發票使用 BizTalk 服務 EDI Bridges.sln**。
2. 按**F5** toobuild 並開始 hello **Tutorial Client**應用程式。
3. 在 [hello] 畫面上，輸入 hello 服務匯流排 ACS 命名空間、 簽發者名稱和簽發者金鑰。
   
   ![][2]  
4. 隨即出現訊息方塊提示，指出將會在服務匯流排命名空間中建立三個佇列。 按一下 [確定] 。
5. 保持 hello 教學課程用戶端正在執行。 開啟 [hello]，按一下**Service Bus** > ***您的服務匯流排命名空間*** > **佇列**，並確認已建立 hello 三個佇列。  

## <a name="step-2-create-and-deploy-trading-partner-agreement"></a>步驟 2：建立和部署交易夥伴協議
建立 Contoso 與 Northwind 之間的交易夥伴協議。 交易夥伴協議定義 trade 合約的訊息結構描述 toouse，例如 hello 兩個商業夥伴之間的傳訊通訊協定 toouse 等等。交易夥伴協議包含兩個 EDI 橋接器、 一個 toosend 訊息 tootrading 夥伴 (稱為 hello **EDI 傳送橋接器**) 和一個 tooreceive 從交易夥伴的訊息 (稱為 hello **EDI 接收橋接器**).

Hello 在內容中此解決方案，hello EDI 傳送橋接器對應 toohello 傳送端的 hello 協議，並是使用的 toosend hello EDIFACT 發票從 Contoso tooNorthwind。 同樣地，hello EDI 接收橋接器對應 toohello 接收端的 hello 協議並是使用的 tooreceive Northwind 的確認。  

### <a name="create-hello-trading-partners"></a>建立交易夥伴的 hello
toostart，會建立交易夥伴 Contoso 和 Northwind。  

1. 在 hello BizTalk 服務入口網站，在 hello**夥伴**索引標籤上，按一下 **新增**。
2. 在 [hello 新增夥伴] 頁面，輸入**Contoso**作為夥伴名稱，然後按一下**儲存**。
3. 重複的 hello 步驟 toocreate hello 第二個夥伴， **Northwind**。  

### <a name="create-hello-agreement"></a>建立 hello 協議
交易夥伴的商務設定檔之間會建立交易夥伴協議。 這個解決方案使用 hello 預設夥伴設定檔，當我們建立 hello 夥伴會自動建立。  

1. 在 hello BizTalk 服務入口網站，按一下 **協議** > **新增**。
2. 在 hello 新協議的**一般設定**頁面上，指定在 hello 圖，顯示 hello 值，然後按一下**繼續**。
   
   ![][3]  
   
   按一下 [繼續] 之後，[接收設定] 和 [傳送設定] 這兩個索引標籤會變成可用狀態。
3. 建立 Contoso 與 Northwind 之間的 hello 傳送協議。 此協議控管 Contoso 如何傳送嗨 EDIFACT 發票 tooNorthwind。
   
   1. 按一下 [傳送設定] 。
   2. 保留 hello 預設值在 hello**輸入 URL**，**轉換**，和**批次處理**索引標籤。
   3. 在 [hello**通訊協定**] 索引標籤下 hello**結構描述**區段中上, 傳 hello **EFACT_D93A_INVOIC.xsd**結構描述。 此結構描述可與 hello 範例封裝。
      
      ![][4]  
   4. 在 hello**傳輸**索引標籤上，指定 hello hello 服務匯流排佇列的詳細資料。 Hello 傳送端協議中，我們使用 hello **northwindreceive**佇列 toosend hello EDIFACT 發票 tooNorthwind 並 hello**暫停**佇列 tooroute 時處理而失敗的任何訊息暫止。 建立這些佇列中的**步驟 1： 建立 Service Bus 佇列 hello** （在本主題中）。
      
      ![][5]  
      
      在下**傳輸設定 > 傳輸類型**和**訊息暫停設定 > 傳輸類型**，選取 Azure 服務匯流排，然後提供 hello 值 hello 影像所示。
4. 建立 hello 接收 Contoso 與 Northwind 之間的協議。 此協議控管 Contoso 如何從 Northwind 接收 hello 通知。
   
   1. 按一下 [接收設定] 。
   2. 保留 hello 預設值在 hello**傳輸**和**轉換**索引標籤。
   3. 在 [hello**通訊協定**] 索引標籤下 hello**結構描述**區段中上, 傳 hello **EFACT_4.1_CONTRL.xsd**結構描述。 此結構描述可與 hello 範例封裝。
   4. 在 hello**路由**索引標籤上，建立篩選器 tooensure，只有路由的 tooContoso Northwind 的確認。 在下**路由設定**，按一下 **新增**toocreate hello 路由篩選條件。
      
      ![][6]  
      
      1. 提供的值**規則名稱**，**路由規則**，和**路由目的地**hello 映像中所示。
      2. 按一下 [儲存] 。
   5. 在 hello**路由**再次索引標籤，指定已擱置的通知 （在處理期間失敗的通知） 傳送至其中。 設定 hello 傳輸類型 tooAzure 服務匯流排時，將路由目的地類型太**佇列**，驗證輸入太**共用存取簽章**(SAS)，提供 hello Service Bus hello SAS 連接字串命名空間，然後輸入 hello 佇列名稱**暫停**。
5. 最後，按一下 **部署**toodeploy hello 協議。 取得部署注意 hello 端點 hello 傳送和接收協議的位置。
   
   * 在 hello**傳送設定**索引標籤，下方**輸入 URL**，注意 hello 端點。 toosend EDI 傳送橋接器將訊息從 Contoso tooNorthwind 使用 hello，您必須傳送訊息 toothis 端點。
   * 在 hello**接收設定**索引標籤，下方**傳輸**，注意 hello 端點。 toosend 將訊息從 Northwind tooContoso 使用 hello EDI 接收橋接器，您必須傳送訊息 toothis 端點。  

## <a name="step-3-create-and-deploy-hello-biztalk-services-project"></a>步驟 3： 建立和部署 hello BizTalk 服務專案
在 hello 先前步驟中，您可以部署的 hello EDI 傳送和接收協議 tooprocess EDIFACT 發票和確認函。 這些合約可以只處理符合 toohello 標準 EDIFACT 訊息結構描述的訊息。 不過，每個針對此解決方案的 hello 案例，Contoso 傳送發票 tooNorthwind 內部專屬結構描述。 所以，EDI 傳送橋接器的 toohello 傳送 hello 訊息之前，它必須轉換從 hello 內部結構描述 toohello 標準 EDIFACT 發票結構描述。 hello BizTalk 服務 EAI 專案會這樣做。

hello BizTalk 服務專案， **InvoiceProcessingBridge**，轉換 hello 訊息也是您所下載的 hello 範例的一部分。 hello 專案包括下列成品的 hello:

* **INHOUSEINVOICE。XSD** – tooNorthwind 傳送嗨內部發票的結構描述。
* **EFACT_D93A_INVOIC。XSD** – hello 標準 EDIFACT 發票的結構描述。
* **EFACT_4.1_CONTRL。XSD** -Northwind 傳送 tooContoso hello EDIFACT 通知的結構描述。
* **INHOUSEINVOICE_to_D93AINVOIC。TRFM** – hello 對應 hello 內部發票結構描述 toohello 標準 EDIFACT 發票結構描述的轉換。  

### <a name="create-hello-biztalk-services-project"></a>建立 hello BizTalk 服務專案
1. Hello Visual Studio 方案，在展開 hello InvoiceProcessingBridge 專案，然後再開啟 hello **MessageFlowItinerary.bcs**檔案。
2. Hello 畫布上任何位置按一下，並設定 hello **BizTalk 服務 URL**在 hello 屬性方塊 toospecify 您 BizTalk 服務的訂用帳戶名稱。 例如： `https://contosowabs.biztalk.windows.net`。
   
   ![][7]  
3. 從 hello 工具箱，拖曳**Xml 單向橋接器**toohello 畫布。 設定 hello**實體名稱**和**相對位址**hello 的屬性太橋接器**ProcessInvoiceBridge**。 按兩下**ProcessInvoiceBridge** tooopen hello 橋接器組態介面。
4. Hello 內**訊息類型**方塊中，按一下加號 hello (**+**) 按鈕 toospecify hello 結構描述的 hello 內送訊息。 因為 hello EAI 橋接器的 hello 連入訊息一律是 hello 內部發票，設定此太**INHOUSEINVOICE**。
   
   ![][8]  
5. 按一下 hello **Xml 轉換**圖形，並在 hello 屬性方塊中的 hello**對應**屬性，按一下 hello 省略符號 (**...**) 按鈕。 在 hello**對應選取範圍**對話方塊中，選取 hello **INHOUSEINVOICE_to_D93AINVOIC**轉換檔案，然後按一下**確定**。
   
   ![][9]  
6. 返回太**MessageFlowItinerary.bcs**，並從 hello 工具箱，拖曳**雙向外部服務端點**方 hello toohello **ProcessInvoiceBridge**。 設定其**實體名稱**屬性太**EDIBridge**。
7. 在 hello 方案總管 中，展開 hello **MessageFlowItinerary.bcs**按兩下 hello **EDIBridge.config**檔案。 取代的 hello 的 hello 內容**EDIBridge.config** hello 下列。
   
   > [!NOTE]
   > 為什麼需要 tooedit hello.config 檔案？我們加入 toohello 橋接器設計工具畫布的 hello 外部服務端點會代表我們稍早部署的 hello EDI 橋接器。 EDI 橋接器是具有傳送和接收端的雙向橋接器。 不過，hello 我們加入 toohello 橋接器設計工具的 EAI 橋接器是單向橋接器。 因此，toohandle hello 不同訊息交換模式的 hello 這兩種橋接器，我們使用自訂橋接器行為其組態納入 hello.config 檔案中。 此外，hello 自訂行為也會處理 hello 驗證 toohello EDI 傳送橋接器端點。這個自訂行為可做為個別的範例： [BizTalk Services 橋接器鏈結範例-EAI tooEDI](http://code.msdn.microsoft.com/BizTalk-Bridge-chaining-2246b104)。 此解決方案會重複使用 hello 範例。  
   > 
   > 
   
   ```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
     <system.serviceModel>
       <extensions>
         <behaviorExtensions>
           <add name="BridgeAuthentication" 
                 type="Microsoft.BizTalk.Bridge.Behaviour.BridgeBehaviorElement, Microsoft.BizTalk.Bridge.Behaviour, Version=1.0.0.0, Culture=neutral, PublicKeyToken=ae58f69b69495c05" />
         </behaviorExtensions>
       </extensions>
       <behaviors>
         <endpointBehaviors>
           <behavior name="BridgeAuthenticationConfiguration">
             <!-- Enter hello ACS namespace, issuer name and issuer secret of hello BizTalk Services deployment -->
             <BridgeAuthentication acsnamespace="[YOUR ACS NAMESPACE]" 
                                   issuername="owner" 
                                   issuersecret="[YOUR ACS SECRET]" />
             <webHttp />
           </behavior>
         </endpointBehaviors>
       </behaviors>
       <bindings>
         <webHttpBinding>
           <binding name="BridgeBindingConfiguration">
             <security mode="Transport" />
           </binding>
         </webHttpBinding>
       </bindings>
       <client>
         <clear />
         <!--
           Go BizTalk Portal > Agreement > Send Settings > Inbound URL
           Copy hello Endpoint URL and paste it in hello below address field
         -->
         <endpoint name="TwoWayExternalServiceEndpointReference1" 
                   address="[YOUR EDI BRIDGE SEND URI]" 
                   behaviorConfiguration="BridgeAuthenticationConfiguration" 
                   binding="webHttpBinding" 
                   bindingConfiguration="BridgeBindingConfiguration" 
                   contract="System.ServiceModel.Routing.IRequestReplyRouter" />
       </client>
     </system.serviceModel>
   </configuration>
   
   ```
8. 更新 hello EDIBridge.config 檔案 tooinclude 組態詳細資料
   
   * 在下 *<behaviors>* 、 提供 hello ACS 命名空間和索引鍵相關聯 hello BizTalk 服務訂用帳戶。
   * 在下 *<client>* ，提供 hello hello EDI 傳送協議部署所在的端點。
   
   儲存變更並關閉 hello 設定檔。
9. 從 hello 工具箱中，按一下 hello**連接器**和聯結 hello **ProcessInvoiceBridge**和**EDIBridge**元件。 選取 hello 連接器，然後在 [屬性] 方塊中，設定**篩選條件**太**全部符合**。 這可確保由 hello EAI 橋接器處理的所有訊息都會路由都傳送 toohello EDI 橋接器。
   
   ![][10]  
10. 將變更儲存 toohello 方案。  

### <a name="deploy-hello-project"></a>部署 hello 專案
1. Hello 在電腦上建立 hello BizTalk 服務專案的位置，下載並安裝您的 BizTalk 服務訂閱 hello SSL 憑證。 從 BizTalk 服務 底下按一下 儀表板，然後按一下下載 SSL 憑證。 按兩下 hello 憑證，並遵循 hello 提示 toocomplete hello 安裝。 請確定您已安裝 hello 憑證**受信任的根憑證授權單位**憑證存放區。
2. 在 Visual Studio 方案總管 中，以滑鼠右鍵按一下 hello **InvoiceProcessingBridge**專案，然後再按一下**部署**。
3. 提供 hello 值 hello 影像所示，然後按**部署**。 您也可以按一下 BizTalk 服務取得 hello ACS 認證**連接資訊**從 hello BizTalk 服務儀表板。
   
   ![][11]  
   
   從 hello 輸出窗格中，複製 hello 端點 hello EAI 橋接器部署所在，比方說， `https://contosowabs.biztalk.windows.net/default/ProcessInvoiceBridge`。 您稍後將需要此端點 URL。  

## <a name="step-4-test-hello-solution"></a>步驟 4： 測試 hello 解決方案
在本主題中，我們查看 tootest 如何使用 hello hello 方案**Tutorial Client** hello 範例的一部分的應用程式。  

1. 在 Visual Studio 中，按下 F5 toostart hello **Tutorial Client**。
2. 囉 」 畫面必須 hello 值預先填入的 hello 步驟中，我們建立 hello 服務匯流排佇列。 按一下 [下一步] 。
3. 在 hello 下一步 視窗中，BizTalk 服務訂閱提供 ACS 認證和 hello 端點其中 EAI 和 EDI （接收） 橋接器部署。
   
   Hello 上一個步驟中，您必須複製 hello EAI 橋接器端點。 EDI 接收橋接器端點 hello BizTalk 服務入口網站中，移 toohello 協議 > 接收的設定 > 傳輸 > 端點。
   
   ![][12]  
4. 在 hello 下一步] 視窗中的 [Contoso 底下，按一下 [hello**傳送內部發票**] 按鈕。 在 hello 檔案開啟對話方塊，請開啟 hello INHOUSEINVOICE.txt 檔案。 檢查 hello hello 檔案內容，然後按一下**確定**toosend hello 發票。
   
   ![][13]  
5. 在幾秒 hello Northwind 就會收到發票。 按一下 hello**檢視訊息**Northwind 所收到的連結 toosee hello 發票。 請注意，contoso 傳送一個 hello 時的標準 EDIFACT 結構描述中的 hello Northwind 收到的發票的方式是在內部結構描述。
   
   ![][14]  
6. 選取 hello 發票，然後按一下**傳送認可**。 在快顯的 hello 對話方塊中，請注意該識別碼是在 hello 接收發票與 hello 認可傳送相同的 hello 交換。 按一下 確定 在 hello**傳送認可** 對話方塊。
   
   ![][15]  
7. 幾分鐘後，在 Contoso 成功收到 hello 確認。
   
   ![][16]  

## <a name="step-5-optional-send-edifact-invoice-in-batches"></a>步驟 5 (選用)：批次傳送 EDIFACT 發票
BizTalk 服務 EDI 橋接器也支援批次處理傳出訊息。 這項功能可用於接收夥伴想 tooreceive 一批訊息 （符合特定條件），而不是個別的訊息。

處理批次時，即 hello 最重要層面是 hello 實際釋放 hello 批次，也稱為 hello 釋放準則。 hello 釋放準則可以根據 hello 接收夥伴想 tooreceive 訊息的方式。 如果啟用批次處理時，EDI 橋接器 hello 就不會傳送 hello hello 符合釋放準則後，直到接收夥伴外寄訊息 toohello。 例如，依據訊息大小的批次準則只會在批次處理 'n' 則訊息時才分派批次。 批次準則也可以是依據時間，以便在每天固定時間傳送批次。 在此解決方案中，我們嘗試 hello 訊息大小基礎的準則。

1. 在 hello BizTalk 服務入口網站，按一下您稍早建立的 hello 協議。 按一下 [傳送設定] > [批次處理] > [新增批次]。
2. 對批次名稱輸入 **InvoiceBatch**、提供描述，然後按 [下一步]。
3. 指定定義必須批次處理哪些訊息的批次準則。 在此方案中，我們會批次處理所有訊息。 因此，選取 hello 使用進階定義 選項，並輸入**1 = 1**。 這個條件永遠會成立，因此會批次處理所有訊息。 按一下 [下一步] 。
   
   ![][17]  
4. 指定批次釋放準則。 從 hello 下拉式方塊，選取**MessageCountBased**，以及**計數**，指定**3**。 這表示 tooNorthwind 會傳送三個訊息的批次。 按一下 [下一步] 。
   
   ![][18]  
5. 檢閱 hello 摘要，然後按一下**儲存**。 按一下**部署**tooredeploy hello 協議。
6. 返回 toohello **Tutorial Client**，按一下 **傳送內部發票**，並遵循 hello 提示 toosend hello 發票。 您會注意到因為 hello 批次大小不符，就會在 Northwind 上收到任何發票。 重複此步驟兩次，所以您需要傳送 tooNorthwind 三則發票訊息。 這就符合 hello 3 則訊息的批次釋放準則，您現在應該會看到在 Northwind 上的發票。

<!--Image references-->
[1]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-1.PNG  
[2]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-2.PNG  
[3]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-3.PNG
[4]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-4.PNG  
[5]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-5.PNG  
[6]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-6.PNG  
[7]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-7.PNG  
[8]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-8.PNG
[9]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-9.PNG  
[10]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-10.PNG  
[11]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-11.PNG  
[12]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-12.PNG  
[13]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-13.PNG
[14]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-14.PNG  
[15]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-15.PNG  
[16]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-16.PNG  
[17]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-17.PNG  
[18]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-18.PNG

