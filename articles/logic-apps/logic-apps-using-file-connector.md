---
title: "aaaConnect tooon 內部檔案系統從 Azure 邏輯應用程式 |Microsoft 文件"
description: "邏輯應用程式工作流程透過 hello 在內部部署資料閘道和檔案系統連接器連接 tooon 內部部署檔案系統"
keywords: "檔案系統"
services: logic-apps
author: derek1ee
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/27/2017
ms.author: LADocs; deli
ms.openlocfilehash: beb5565293def4aba81f63f19e77d7498aac38c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-file-systems-from-logic-apps-with-hello-file-system-connector"></a>邏輯應用程式與 hello 檔案系統連接器連接 tooon 內部部署檔案系統

混合式雲端連線是中央 toologic 應用程式，因此 toomanage 資料和安全地存取內部資源，您的 logic apps 可以使用 hello 在內部部署資料閘道。 在本文中，我們會示範如何 tooconnect tooan 內部檔案系統與基本案例： 複製的檔案的上傳的 tooDropbox tooa 檔案共用，然後傳送電子郵件。

## <a name="prerequisites"></a>必要條件

- 安裝及最新設定 hello[在內部部署資料閘道](https://www.microsoft.com/download/details.aspx?id=53127)。
- 安裝 hello 最新的內部部署資料閘道，1.15.6150.1 版本或更新版本。 [Toohello 在內部部署資料閘道連接](http://aka.ms/logicapps-gateway)清單 hello 步驟。 hello 閘道必須安裝在內部部署電腦上，才能繼續與 hello 步驟 hello 其餘部分。

## <a name="add-trigger-and-actions-for-connecting-tooyour-file-system"></a>加入觸發程序和連接 tooyour 檔案系統的動作

1. 建立邏輯應用程式，並新增這個 Dropbox 觸發程序：**建立檔案時** 
2. 在 hello 觸發程序中，選擇**下一個步驟** > **將動作加入**。 
3. 在 [hello] 搜尋方塊中，輸入`file system`使您可以檢視 hello 檔案系統連接器的所有支援的動作。

   ![搜尋檔案連接器](media/logic-apps-using-file-connector/search-file-connector.png)

2. 選擇 hello**建立檔案**動作，並建立連接 tooyour 檔案系統。

   如果您沒有現有的連接，您必須提示的 toocreate 其中一個。

   1. 選擇 [透過內部部署資料閘道連線]。 隨即出現更多屬性。
   2. 選取檔案系統的根資料夾。
      
       > [!NOTE]
       > hello 根資料夾為 hello 主要父資料夾，用於所有檔案相關動作的相對路徑。 您可以指定本機資料夾 hello 機器 hello 在內部部署資料閘道已安裝，或 hello 資料夾可以是可以存取 hello 機器的網路共用位置上。

   3. 輸入 hello 閘道 hello 使用者名稱和密碼。
   4. 選取您先前安裝的 hello 閘道。

       ![設定連線](media/logic-apps-using-file-connector/create-file.png)

3. 提供所有 hello 詳細資料之後，請選擇**建立**。 

   邏輯應用程式設定，並測試您的連線，並確定 hello 連線正常運作。 
   如果 hello 連線已正確設定時，您會看到您先前選取的 hello 動作選項。 
   hello 檔案系統連接器現在可供使用。

4. 指定您要 toocopy Dropbox toohello 根資料夾中的檔案，您的內部檔案共用。

   ![建立檔案動作](media/logic-apps-using-file-connector/create-file-filled.png)

5. 邏輯應用程式複本 hello 檔案之後, 加入的 Outlook 動作傳送電子郵件，因此相關使用者了解 hello 新檔案。 輸入 hello 收件者、 標題和 hello 電子郵件的本文。 

   在 hello 動態的內容選取器，您可以選擇資料輸出 hello 檔案連接器好讓您可以加入更多詳細資料 toohello 電子郵件。

   ![傳送電子郵件動作](media/logic-apps-using-file-connector/send-email.png)

6. 儲存您的邏輯應用程式。 上傳檔案 tooDropbox 來測試您的應用程式。 hello 檔案應該會收到複製的 toohello 內部檔案共用，以及您應該會收到 hello 作業的相關電子郵件。

   > [!TIP] 
   > 了解如何太[監視您的 logic apps](../logic-apps/logic-apps-monitor-your-logic-apps.md)。

恭喜，您現在可以使用邏輯應用程式可以連接 tooyour 在內部部署檔案系統。 請嘗試瀏覽例如 hello 連接器提供其他功能：

- 建立檔案
- 列出資料夾中的檔案
- 附加檔案
- 刪除檔案
- 取得檔案內容
- 使用路徑來取得檔案內容
- 取得檔案中繼資料
- 使用路徑取得檔案中繼資料
- 列出根資料夾中的檔案
- 更新檔案

## <a name="view-hello-swagger"></a>檢視 hello swagger
請參閱 hello [swagger 詳細資料](/connectors/fileconnector/)。 

## <a name="get-help"></a>取得說明

tooask 問題回答的問題，以及了解哪些其他 Azure 邏輯應用程式使用者的行為，請瀏覽 hello [Azure 邏輯應用程式論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)。

toohelp 改善 Azure 邏輯應用程式和連接器、 票選或送出意見在 hello [Azure 邏輯應用程式使用者意見反應網站](http://aka.ms/logicapps-wish)。

## <a name="next-steps"></a>後續步驟

- [Tooon 內部部署資料連接](../logic-apps/logic-apps-gateway-connection.md)從邏輯應用程式
- 了解[企業整合](../logic-apps/logic-apps-enterprise-integration-overview.md)
