---
title: "aaaEncode 或解碼 Azure 邏輯應用程式中的一般檔案 |Microsoft 文件"
description: "如何 toouse hello 檔案檔案編碼器或解碼器在邏輯應用程式中的 hello 企業版整合套件"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 82152dab-c7ad-43df-b721-596559703be8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; mandia
ms.openlocfilehash: 2c295586625fd84366ec7cbafdcebf0489ba234d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-enterprise-integration-with-flat-files"></a>企業與一般檔案整合概觀

然後再傳送 tooa 協力廠商企業對企業 (B2B) 案例中的，您可能想 tooencode XML 內容。 在邏輯應用程式中，您可以使用這編碼連接器 toodo hello 一般檔案。 hello 您所建立的邏輯應用程式可以取得其 XML 內容從各種來源，包括從 HTTP 要求的觸發程序、 從另一個應用程式，或甚至是從一個 hello 許多[連接器](../connectors/apis-list.md)。 如需邏輯應用程式的詳細資訊，請參閱 hello[邏輯應用程式文件](logic-apps-what-are-logic-apps.md "深入了解 Logic apps")。  

## <a name="create-hello-flat-file-encoding-connector"></a>建立 hello 一般檔案編碼連接器
請遵循這些步驟 tooadd 編碼連接器 tooyour 邏輯應用程式的一般檔案。

1. 建立邏輯應用程式和[tooyour 整合帳戶連結到](logic-apps-enterprise-integration-accounts.md "toolink 整合帳戶 tooa 邏輯應用程式了解")。 此帳戶包含您將使用 tooencode hello XML 資料的 hello 結構描述。  
2. 新增**要求-當 HTTP 要求**觸發程序 tooyour 邏輯應用程式。  
   ![觸發程序 tooselect 的螢幕擷取畫面](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)    
3. 加入 hello 一般檔案編碼動作，如下所示：
   
    a. 選取 hello**加上**符號。
   
    b. 選取 hello**將動作加入**（會顯示您選取加號 hello 之後） 的連結。
   
    c. 在 [hello] 搜尋方塊中，輸入*一般*toofilter 所有 hello 動作 toohello 其中一個要 toouse。
   
    d. 選取 hello**一般檔案編碼方式**hello 清單中的選項。   
   ![一般檔案編碼選項的螢幕擷取畫面](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)   
4. 在 hello**一般檔案編碼方式**對話方塊中，選取 hello**內容**文字方塊。  
   ![內容文字方塊的螢幕擷取畫面](media/logic-apps-enterprise-integration-flatfile/flatfile-3.png)  
5. 選取要作為內容的 tooencode hello hello body 標記。 hello body 標記將會填入 hello 內容 欄位。     
   ![內文標記的螢幕擷取畫面](media/logic-apps-enterprise-integration-flatfile/flatfile-4.png)  
6. 選取 hello**結構描述名稱**清單方塊中，，然後選擇您想要 toouse tooencode hello hello 結構描述輸入內容。    
   ![結構描述名稱清單方塊的螢幕擷取畫面](media/logic-apps-enterprise-integration-flatfile/flatfile-5.png)  
7. 儲存您的工作。   
   ![儲存圖示的螢幕擷取畫面](media/logic-apps-enterprise-integration-flatfile/flatfile-6.png)  

此時，您已完成設定一般檔案編碼連接器。 在真實世界應用程式中，您可能想在特定業務應用程式，例如 Salesforce toostore hello 編碼資料。 或者，您可以傳送該交易夥伴的編碼的資料 tooa。 您可以輕鬆加入動作 toosend hello 的 hello 輸出編碼方式使用任何一個 hello 的動作 tooSalesforce 或 tooyour 交易夥伴，提供其他連接器。

您現在可以測試您的連接器的要求 toohello HTTP 結束點，包括 hello hello 要求主體中的 hello XML 內容。  

## <a name="create-hello-flat-file-decoding-connector"></a>建立 hello 解碼連接器的一般檔案

> [!NOTE]
> toocomplete 這些步驟，您需要的 toohave 結構描述檔案已上傳到您整合帳戶。

1. 新增**要求-當 HTTP 要求**觸發程序 tooyour 邏輯應用程式。  
   ![觸發程序 tooselect 的螢幕擷取畫面](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)    
2. 加入 hello 一般檔案解碼動作，如下所示：
   
    a. 選取 hello**加上**符號。
   
    b. 選取 hello**將動作加入**（會顯示您選取加號 hello 之後） 的連結。
   
    c. 在 [hello] 搜尋方塊中，輸入*一般*toofilter 所有 hello 動作 toohello 其中一個要 toouse。
   
    d. 選取 hello**一般檔案解碼**hello 清單中的選項。   
   ![一般檔案解碼選項的螢幕擷取畫面](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)   
3. 選取 hello**內容**控制項。 這會產生從先前的步驟，可作為 hello 內容 toodecode hello 內容的清單。 請注意該 hello*主體*hello 從傳入的 HTTP 要求是做為 hello 內容 toodecode 可用 toobe。 您也可以直接在 hello 輸入 hello 內容 toodecode**內容**控制項。     
4. 選取 hello*主體*標記。 請注意 hello body 標記已在 hello**內容**控制項。
5. 選取 hello hello 想 toouse toodecode hello 內容的結構描述名稱。 hello 下列螢幕擷取畫面顯示*OrderFile* hello 選取的結構描述名稱。 這個結構描述名稱已上傳到 hello 整合帳戶之前。
   
   ![一般檔案解碼對話方塊的螢幕擷取畫面](media/logic-apps-enterprise-integration-flatfile/flatfile-decode-1.png)    
6. 儲存您的工作。  
   ![儲存圖示的螢幕擷取畫面](media/logic-apps-enterprise-integration-flatfile/flatfile-6.png)    

此時，您已完成設定一般檔案解碼連接器。 在真實世界應用程式中，您可能想在特定業務應用程式，例如 Salesforce toostore hello 已解碼的資料。 您可以輕鬆加入動作 toosend hello 輸出的解碼動作 tooSalesforce hello。

您現在可以藉由要求 toohello HTTP 端點來測試您的連接器，且想 hello XML 內容包括 toodecode hello hello 要求主體中。  

## <a name="next-steps"></a>後續步驟
* [深入了解 hello Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "深入了解 Enterprise Integration Pack")。  

