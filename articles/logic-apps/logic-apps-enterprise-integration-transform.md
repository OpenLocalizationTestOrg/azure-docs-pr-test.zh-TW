---
title: "aaaConvert XML 資料轉換為 Azure 邏輯應用程式與 |Microsoft 文件"
description: "建立轉換或 mapps tooconvert 在邏輯應用程式中使用 hello 企業整合 SDK 的格式之間的 XML 資料"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: add01429-21bc-4bab-8b23-bc76ba7d0bde
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: b56ec1072c5058d3aefc7f88ac9b2748ebe56456
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-integration-with-xml-transforms"></a>具備 XML 轉換的企業整合
## <a name="overview"></a>概觀
hello 企業整合轉換連接器將資料轉換從一種格式 tooanother 格式。 比方說，您可能包含目前的日期，格式為 hello YearMonthDay hello 內送訊息。 您可以使用轉換 tooreformat hello 日期 toobe hello MonthDayYear 格式。

## <a name="what-does-a-transform-do"></a>轉換的作用為何？
轉換就是所謂的對應，是由來源 XML 結構描述 (輸入 hello) 和目標的 XML 結構描述 （hello 輸出） 所組成。 您可以使用不同的內建函數 toohelp 操作，或控制 hello 資料，包括字串操作、 條件式指派、 算術運算式、 日期時間格式子，即使迴圈建構。

## <a name="how-toocreate-a-transform"></a>如何 toocreate 轉換嗎？
您可以使用 hello Visual Studio，以建立轉換/對應[企業整合 SDK](https://aka.ms/vsmapsandschemas)。 當您完成建立和測試 hello 轉換，您上傳到整合帳戶 hello 轉換。 

## <a name="how-toouse-a-transform"></a>如何 toouse 轉換
您將 hello 轉換/對應上傳到整合帳戶之後，您可以使用它 toocreate 邏輯應用程式。 hello 邏輯應用程式會執行轉換時，就會觸發 hello 邏輯應用程式 （和需要 toobe 轉換的輸入內容）。

**以下是轉換 hello 步驟 toouse**:

### <a name="prerequisites"></a>必要條件

* 建立整合帳戶並新增地圖 tooit  

既然您已經處理的 hello 必要元件，它是時間 toocreate 邏輯應用程式：  

1. 建立邏輯應用程式和[tooyour 整合帳戶連結到](../logic-apps/logic-apps-enterprise-integration-accounts.md "toolink 整合帳戶 tooa 邏輯應用程式了解")包含 hello 對應。
2. 新增**要求**觸發程序 tooyour 邏輯應用程式  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-1.png)    
3. 新增 hello**轉換 XML**第一個選取的動作**加入的動作**   
   ![](./media/logic-apps-enterprise-integration-transforms/transform-2.png)   
4. 輸入 hello 字*轉換*hello 搜尋方塊 toofilter 中所有 hello 動作 toohello 其中一個要 toouse  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-3.png)  
5. 選取 hello**轉換 XML**動作   
6. 新增 hello XML**內容**您轉換。 您可以使用任何您收到 hello 與 hello HTTP 要求中的 XML 資料**內容**。 在此範例中，選取 hello hello 觸發 hello 邏輯應用程式的 HTTP 要求主體。
7. 選取 hello 名稱 hello**對應**想要 toouse tooperform hello 轉換。 hello 對應必須已經是整合帳戶中。 在先前步驟中，您已經為您的邏輯應用程式存取 tooyour 整合帳戶包含您的對應。      
   ![](./media/logic-apps-enterprise-integration-transforms/transform-4.png) 
8. 儲存您的工作   
    ![](./media/logic-apps-enterprise-integration-transforms/transform-5.png) 

此時，您已完成設定對應。 在真實世界應用程式中，您可能想 toostore hello 轉換資料，例如 SalesForce 的 LOB 應用程式中。 您可以輕鬆地為動作 toosend hello 輸出的 hello 轉換 tooSalesforce。 

您現在可以藉由要求 toohello HTTP 端點測試轉換。  

## <a name="features-and-use-cases"></a>功能和使用案例
* 建立在對應中的 hello 轉換可以很簡單，例如從一個文件 tooanother 複製名稱和地址。 或者，您可以建立更複雜的轉換使用 hello 的方塊外對應作業。  
* 目前有多個對應作業或函數可供使用，包括字串、日期時間函數等等。  
* 您可以 hello 結構描述之間的直接資料複本。 在對應工具包含在 hello SDK 中的 hello，這很簡單，只繪製一條線連接 hello hello 來源結構描述中的項目與其 hello 目的結構描述中的對應項目。  
* 在建立對應時，您會檢視 hello 地圖，顯示所有 hello 關聯性和您所建立的連結的圖形表示法。
* 使用 hello 測試對應功能 tooadd 範例 XML 訊息。 簡單按一下滑鼠，您可以測試 hello 對應您建立，並查看 hello 產生輸出。  
* 上傳現有的對應  
* 包含 hello XML 格式的支援。

## <a name="learn-more"></a>詳細資訊
* [深入了解 hello Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md "深入了解 Enterprise Integration Pack")  
* [深入了解對應](../logic-apps/logic-apps-enterprise-integration-maps.md "了解企業整合對應")  

