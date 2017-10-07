---
title: "aaaEDIFACT B2B 企業整合 Azure 邏輯應用程式訊息 |Microsoft 文件"
description: "利用 Azure Logic Apps 交換 EDI 格式的 EDIFACT 訊息以進行 B2B 企業整合"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 2257d2c8-1929-4390-b22c-f96ca8b291bc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/26/2016
ms.author: LADocs; jonfan
ms.openlocfilehash: 496fadcda58de2d36459202b839b0a63c9e5857c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="exchange-edifact-messages-for-enterprise-integration-with-logic-apps"></a>利用邏輯應用程式交換 EDIFACT 訊息以進行企業整合

您必須先建立 EDIFACT 合約並將該合約儲存在您的整合帳戶中，才可以交換 EDIFACT 訊息。 以下是如何 hello 步驟 toocreate EDIFACT 協議。

> [!NOTE]
> 此頁面涵蓋 Azure Logic Apps hello EDIFACT 功能。 如需詳細資訊，請參閱 [X12](logic-apps-enterprise-integration-x12.md)。

## <a name="before-you-start"></a>開始之前

以下是您所需要的 hello 項目：

* 已經定義並與 Azure 訂用帳戶相關聯的[整合帳戶](../logic-apps/logic-apps-enterprise-integration-accounts.md)  
* 至少已經在整合帳戶中定義兩個[夥伴](logic-apps-enterprise-integration-partners.md)

> [!NOTE]
> 當您會建立協議、 hello 內容，在您接收或傳送 hello 夥伴 tooand 必須符合 hello 合約型別 hello 訊息。

在您[建立整合帳戶](../logic-apps/logic-apps-enterprise-integration-accounts.md)並[新增夥伴](logic-apps-enterprise-integration-partners.md)之後，您可以依照下列步驟建立 EDIFACT 合約。

## <a name="create-an-edifact-agreement"></a>建立 EDIFACT 合約 

1.  登入 toohello [Azure 入口網站](http://portal.azure.com "Azure 入口網站")。 從 hello 左窗格中，選取**更多服務**。

    > [!TIP]
    > 如果您沒有看到**更多服務**，您可能必須 tooexpand hello 功能表第一次。 在 hello hello 摺疊功能表頂端，選取**顯示功能表**。

    ![在左側功能表上選取 [更多服務]](./media/logic-apps-enterprise-integration-edifact/edifact-0.png)

2. 在 hello 搜尋方塊中，輸入 「 整合 」 篩選條件。 在 hello 結果清單中，選取 **整合帳戶**。

    ![依據 [整合] 篩選，選取 [整合帳戶]](./media/logic-apps-enterprise-integration-edifact/edifact-1-3.png)

3. 在 hello**整合帳戶**刀鋒視窗中開啟，您想要 toocreate hello 協議選取 hello 整合帳戶。
如果沒有看到任何整合帳戶，請[先建立一個](../logic-apps/logic-apps-enterprise-integration-accounts.md "關於整合帳戶的一切")。  

    ![選取其中 toocreate hello 協議的整合帳戶](./media/logic-apps-enterprise-integration-edifact/edifact-1-4.png)

4. 選擇 hello**協議**磚。 如果您還沒有合約磚，請先新增 hello 磚。   

    ![選擇 [合約] 圖格](./media/logic-apps-enterprise-integration-edifact/edifact-1-5.png)

5. 在 hello 協議刀鋒視窗中開啟，選擇 **新增**。

    ![選擇 [新增]](./media/logic-apps-enterprise-integration-edifact/edifact-agreement-2.png)

6. 在 [新增] 之下，輸入合約的 [名稱]。 針對 [合約類型]，選取 **EDIFACT**。 選取 hello**主控合作夥伴**，**主機識別**，**來賓夥伴**，和**客體身分識別**協議。

    ![提供合約詳細資料](./media/logic-apps-enterprise-integration-edifact/edifact-1.png)

    | 屬性 | 說明 |
    | --- | --- |
    | 名稱 |Hello 協議的名稱 |
    | 合約類型 | 應該是 EDIFACT |
    | 主控夥伴 |合約需要主控夥伴和來賓夥伴。 hello 主控合作夥伴代表 hello 組織設定 hello 協議。 |
    | 主控身分識別 |Hello 主控合作夥伴的的識別項 |
    | 來賓夥伴 |合約需要主控夥伴和來賓夥伴。 hello 來賓夥伴代表正在進行 hello 主控合作夥伴與商務的 hello 組織。 |
    | 來賓身分識別 |Hello 來賓夥伴的的識別項 |
    | 接收設定 |這些屬性會套用 tooall 的協議所收到的訊息。 |
    | 傳送設定 |這些屬性會套用 tooall 的協議所傳送的訊息。 |

## <a name="configure-how-your-agreement-handles-received-messages"></a>設定合約處理所收到訊息的方式

既然您已經設定 hello 協議屬性，您可以設定如何識別本合約，以及處理從夥伴透過此協議接收內送訊息。

1.  在 [新增] 之下，選取 [接收設定]。
設定這些屬性，根據您的合約與 hello 夥伴與您交換訊息。 屬性描述，請參閱本節中的 hello 表格。

    [接收設定] 分成下列各區段：識別碼、通知、結構描述、控制編號、驗證和內部設定。

    ![設定 [接收設定]](./media/logic-apps-enterprise-integration-edifact/edifact-2.png)  

2. 瀏覽完畢之後，請確定 toosave 您的設定選擇**確定**。

現在您的合約已準備好 toohandle 內送訊息符合 tooyour 選取的設定。

### <a name="identifiers"></a>識別項

| 屬性 | 說明 |
| --- | --- |
| UNB6.1 (接收者參考密碼) |輸入範圍 1 到 14 個字元的英數字元值。 |
| UNB6.2 (接收者參考辨識符號) |輸入最少 1 個字元，最多 2 個字元的英數字元值。 |

### <a name="acknowledgments"></a>通知

| 屬性 | 說明 |
| --- | --- |
| 訊息回條 (CONTRL) |選取此核取方塊 tooreturn 技術 (CONTRL) 通知 toohello 交換傳送者。 hello 通知會傳送 hello 協議的 hello 傳送設定為基礎的 toohello 交換傳送者。 |
| 通知 (CONTRL) |選取此核取方塊 tooreturn，將功能 (CONTRL) 通知 toohello 交換傳送者 hello 通知會傳送 hello 協議的 hello 傳送設定為基礎的 toohello 交換傳送者。 |

### <a name="schemas"></a>結構描述

| 屬性 | 說明 |
| --- | --- |
| UNH2.1 (TYPE) |選取交易集類型。 |
| UNH2.2 (VERSION) |輸入 hello 訊息版本號碼。 (最少 1 個字元；最多 3 個字元)。 |
| UNH2.3 (RELEASE) |輸入 hello 訊息版次號碼。 (最少 1 個字元；最多 3 個字元)。 |
| UNH2.5 (ASSOCIATED ASSIGNED CODE) |輸入 hello 分派程式碼。 (最少 6 個字元。 必須是英數字元)。 |
| UNG2.1 (APP SENDER ID) |輸入最少 1 個字元，最多 35 個字元的英數字元值。 |
| UNG2.2 (APP SENDER CODE QUALIFIER) |輸入最多 4 個字元的英數字元值。 |
| 結構描述 |選取 hello 先前上傳您想從您的帳戶相關聯的整合的 toouse 結構描述。 |

### <a name="control-numbers"></a>控制編號
| 屬性 | 說明 |
| --- | --- |
| 不允許交換控制編號重複 |tooblock 重複的交換，選取此屬性。 如果選取，系統會檢查 hello EDIFACT 解碼動作 hello 的交換控制編號 (UNB5) 收到 hello 交換不符合先前處理的交換控制編號。 如果偵測到相符項目，所以不予處理 hello 交換。 |
| 每隔下列天數檢查是否有重複的 UNB5 |如果您選擇 toodisallow 重複的交換控制編號，您可以指定當 tooperform hello 核取此設定中，提供 hello 適當值的 hello 天數。 |
| 不允許群組控制編號重複 |tooblock 交換具有重複群組控制號碼 (UNG5) 中，選取此屬性。 |
| 不允許交易集控制編號重複 |tooblock 交換具有重複交易集控制編號 (UNH1)，選取這個屬性。 |
| EDIFACT 通知控制編號 |toodesignate hello 交易集參考編號，用於在通知中，輸入 hello 前置詞、 參考編號範圍和後置字元的值。 |

### <a name="validations"></a>驗證

當您完成每個驗證資料列時，將會自動新增另一個驗證資料列。 如果您未指定任何規則，驗證會使用 hello 「 預設 」 的資料列。

| 屬性 | 說明 |
| --- | --- |
| 訊息類型 |選取 hello EDI 訊息類型。 |
| EDI 驗證 |資料類型所定義的 hello 結構描述的 EDI 內容、 長度限制、 空白資料元素和尾端分隔符號執行 EDI 驗證。 |
| 擴充驗證 |如果 hello 資料型別不是 EDI，驗證在 hello 資料元素需求上，並允許重複、 列舉和資料元素長度驗證 （最小/最大）。 |
| 允許前置/尾端零 |保留任何額外的前置或尾端零及空格字元。 請勿移除這些字元。 |
| 修剪前置/尾端零 |移除前置或尾端零及空格字元。 |
| 尾端分隔符號原則 |產生尾端分隔符號。 <p>選取**不允許**tooprohibit 尾端分隔符號，並在 hello 分隔符號接收交換。 如果 hello 交換有尾端分隔符號與分隔字元，hello 交換宣告不正確。 <p>選取**選擇性**tooaccept 交換或不具有結尾分隔字元。 <p>選取**強制**hello 接收交換時必須有尾端分隔符號與分隔字元。 |

### <a name="internal-settings"></a>內部設定

| 屬性 | 說明 |
| --- | --- |
| 如果允許尾端分隔符號，則建立空的 XML 標籤 |選取此核取方塊 toohave hello 交換傳送者包含空白針對尾端分隔符號的 XML 標記。 |
| 將交換分割為交易集 - 發生錯誤時暫停交易集|每個交易集剖析成個別的 XML 文件的交換中藉由套用 hello 適當的信封 toohello 交易集。 只會暫停 hello 交易集驗證失敗。 |
| 將交換分割為交易集 - 發生錯誤時暫停交換|每個交易集剖析成個別的 XML 文件的交換中藉由套用 hello 適當的信封。 Hello 交換中的一個或多個交易集驗證失敗時擱置 hello 整個交換。 | 
| 保留交換 - 發生錯誤時暫停交易集 |會保留 hello 交換，然後建立 hello 整個批次交換的 XML 文件。 只會暫停 hello 交易集驗證失敗，但仍繼續 tooprocess 所有其他交易集。 |
| 保留交換 - 發生錯誤時暫停交換 |會保留 hello 交換，然後建立 hello 整個批次交換的 XML 文件。 Hello 交換中的一個或多個交易集驗證失敗時擱置 hello 整個交換。 |

## <a name="configure-how-your-agreement-sends-messages"></a>設定合約傳送訊息的方式

您可以設定此協議如何識別及處理外寄傳送 tooyour 夥伴透過此合約的訊息。

1.  在 [新增] 之下，選取 [傳送設定]。
根據您與其交換訊息之夥伴所簽署的合約，設定這些屬性。 屬性描述，請參閱本節中的 hello 表格。

    [傳送設定] 分成下列各區段：識別碼、通知、結構描述、信封、字元集和分隔符號、控制編號以及驗證。

    ![設定 [傳送設定]](./media/logic-apps-enterprise-integration-edifact/edifact-3.png)    

2. 瀏覽完畢之後，請確定 toosave 您的設定選擇**確定**。

現在您的合約是準備 toohandle 外寄訊息符合 tooyour 選取的設定。

### <a name="identifiers"></a>識別項

| 屬性 | 說明 |
| --- | --- |
| UNB1.2 (語法版本) |選取介於 **1** 到 **4** 之間的值。 |
| UNB2.3 (傳送者反向路由位址) |輸入最少 1 個字元，最多 14 個字元的英數字元值。 |
| UNB3.3 (接收者反向路由位址) |輸入最少 1 個字元，最多 14 個字元的英數字元值。 |
| UNB6.1 (接收者參考密碼) |輸入最少 1 個字元，最多 14 個字元的英數字元值。 |
| UNB6.2 (接收者參考辨識符號) |輸入最少 1 個字元，最多 2 個字元的英數字元值。 |
| UNB7 (應用程式參考識別碼) |輸入最少 1 個字元，最多 14 個字元的英數字元值。 |

### <a name="acknowledgment"></a>通知
| 屬性 | 說明 |
| --- | --- |
| 訊息回條 (CONTRL) |如果 hello 主控合作夥伴預期 tooreceive 技術 (CONTRL) 通知，請選取此核取方塊。 此設定指定傳送 hello 訊息，該 hello 主控合作夥伴要求 hello 來賓夥伴傳送通知。 |
| 通知 (CONTRL) |如果 hello 主控合作夥伴預期 tooreceive 功能 (CONTRL) 通知，請選取此核取方塊。 此設定指定傳送 hello 訊息，該 hello 主控合作夥伴要求 hello 來賓夥伴傳送通知。 |
| 針對接受的交易集產生 SG1/SG4 迴圈 |如果您選擇 toorequest 功能通知，請接受的交易集功能 CONTRL 通知中選取此核取方塊 tooforce 產生 SG1/SG4 迴圈。 |

### <a name="schemas"></a>結構描述
| 屬性 | 說明 |
| --- | --- |
| UNH2.1 (TYPE) |選取交易集類型。 |
| UNH2.2 (VERSION) |輸入 hello 訊息版本號碼。 |
| UNH2.3 (RELEASE) |輸入 hello 訊息版次號碼。 |
| 結構描述 |選取 hello 結構描述 toouse。 結構描述位於您的整合帳戶中。 tooaccess 您的結構描述第一次連結整合帳戶 tooyour 邏輯應用程式。 |

### <a name="envelopes"></a>信封
| 屬性 | 說明 |
| --- | --- |
| UNB8 (處理優先順序代碼) |輸入不超過 1 個字元的字母值。 |
| UNB10 (通訊協議) |輸入最少 1 個字元，最多 40 個字元的英數字元值。 |
| UNB11 (測試指示器) |選取此核取方塊 tooindicate hello 產生交換的是測試資料 |
| 套用 UNA 區段 (字串服務建議) |選取此核取方塊 toogenerate 傳送嗨交換 toobe 的 UNA 區段。 |
| 套用 UNG 區段 (功能群組標頭) |選取此核取方塊 toocreate，群組 hello 訊息傳送 toohello 來賓夥伴中的 hello 功能群組標頭區段。 hello 下列是使用的 toocreate hello UNG 區段： <p>對於 **UNG1**，輸入最少 1 個字元，最多 6 個字元的英數字元值。 <p>對於 **UNG2.1**，輸入最少 1 個字元，最多 35 個字元的英數字元值。 <p>對於 **UNG2.2**，輸入最多 4 個字元的英數字元值。 <p>對於 **UNG3.1**，輸入最少 1 個字元，最多 35 個字元的英數字元值。 <p>對於 **UNG3.2**，輸入最多 4 個字元的英數字元值。 <p>對於 **UNG6**，輸入最少 1 個字元，最多 3 個字元的英數字元值。 <p>對於 **UNG7.1**，輸入最少 1 個字元，最多 3 個字元的英數字元值。 <p>對於 **UNG7.2**，輸入最少 1 個字元，最多 3 個字元的英數字元值。 <p>對於 **UNG7.3**，輸入最少 1 個字元，最多 6 個字元的英數字元值。 <p>對於 **UNG8**，輸入最少 1 個字元，最多 14 個字元的英數字元值。 |

### <a name="character-sets-and-separators"></a>字元集和分隔符號

除了 hello 字元集，您可以輸入一組不同的分隔符號 toobe 用於每個訊息類型。 如果未針對指定的訊息結構描述指定字元集，則會使用預設字元集 hello。

| 屬性 | 說明 |
| --- | --- |
| UNB1.1 (系統識別碼) |選取 hello EDIFACT 字元集設定 toobe hello 外寄交換套用。 |
| 結構描述 |從 hello 下拉式清單中選取結構描述。 在您完成每個資料列時，便會自動新增一個資料列。 選取 hello 分隔符號 hello 選取的結構描述，設定您想 toouse，根據下列分隔符號描述 hello。 |
| 輸入類型 |從 hello 下拉式清單中選取的輸入的類型。 |
| 元件分隔符號 |tooseparate 複合資料元素，請輸入單一字元。 |
| 資料元素分隔符號 |tooseparate 複合資料元素內的簡單資料元素輸入單一字元。 |
| 區段結束字元 |tooindicate hello EDI 區段結束，請輸入單一字元。 |
| 尾碼 |選取 hello 字元 hello 區段識別碼搭配使用。 如果您指定尾碼，則 hello 區段結束字元資料元素可以是空的。 如果 hello 區段結束字元留白，您必須指定尾碼。 |

### <a name="control-numbers"></a>控制編號
| 屬性 | 說明 |
| --- | --- |
| UNB5 (交換控制編號) |輸入前置詞、 hello 交換控制編號，值的範圍和後置字元。 這些值是使用的 toogenerate 外寄交換。 hello 首碼和尾碼是選擇性的而需要 hello 控制編號。 hello 控制號碼會遞增每一個新的訊息。hello 首碼和尾碼維持 hello 相同。 |
| UNG5 (群組控制編號) |輸入前置詞、 hello 交換控制編號，值的範圍和後置字元。 這些值會用 toogenerate hello 群組控制編號。 hello 首碼和尾碼是選擇性的而需要 hello 控制編號。 hello 控制號碼會遞增每一個新訊息，直到達到 hello 最大值。hello 首碼和尾碼維持 hello 相同。 |
| UNH1 (訊息標頭參考編號) |輸入前置詞、 hello 交換控制編號，值的範圍和後置字元。 這些值會用 toogenerate hello 訊息標頭參照號碼。 hello 首碼和尾碼是選擇性的而需要 hello 參考編號。 hello 參照號碼會遞增每一個新的訊息。hello 首碼和尾碼維持 hello 相同。 |

### <a name="validations"></a>驗證

當您完成每個驗證資料列時，將會自動新增另一個驗證資料列。 如果您未指定任何規則，驗證會使用 hello 「 預設 」 的資料列。

| 屬性 | 說明 |
| --- | --- |
| 訊息類型 |選取 hello EDI 訊息類型。 |
| EDI 驗證 |Hello hello 結構描述、 長度限制、 空白資料元素和尾端分隔符號的 EDI 屬性所定義的資料類型上執行 EDI 驗證。 |
| 擴充驗證 |如果 hello 資料型別不是 EDI，驗證在 hello 資料元素需求上，並允許重複、 列舉和資料元素長度驗證 （最小/最大）。 |
| 允許前置/尾端零 |保留任何額外的前置或尾端零及空格字元。 請勿移除這些字元。 |
| 修剪前置/尾端零 |移除前置或尾端零字元。 |
| 尾端分隔符號原則 |產生尾端分隔符號。 <p>選取**不允許**tooprohibit 尾端分隔符號，並在 hello 分隔符號傳送交換。 如果 hello 交換有尾端分隔符號與分隔字元，hello 交換宣告不正確。 <p>選取**選擇性**toosend 交換或不具有結尾分隔字元。 <p>選取**強制**如果傳送嗨交換必須有尾端分隔符號與分隔字元。 |

## <a name="find-your-created-agreement"></a>尋找您建立的合約

1.  完成設定您協議屬性，在 hello 之後**新增**刀鋒視窗中，選擇**確定**toofinish 建立您的合約和傳回 tooyour 整合帳戶 刀鋒視窗。

    您新增的合約現在顯示於您的 [合約] 清單中。

2.  您也可以在整合帳戶概觀中檢視您的合約。 在您整合帳戶] 刀鋒視窗中，選擇 [**概觀**，然後選取 hello**協議**磚。 

    ![選擇 「 合約 」 磚 tooview 所有協議](./media/logic-apps-enterprise-integration-edifact/edifact-4.png)   

## <a name="view-swagger-file"></a>檢視 Swagger 檔案
tooview hello Swagger 詳細資料，hello EDIFACT 連接器，請參閱[EDIFACT](/connectors/edifact/)。

## <a name="learn-more"></a>詳細資訊
* [深入了解 hello Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "深入了解 Enterprise Integration Pack")  

