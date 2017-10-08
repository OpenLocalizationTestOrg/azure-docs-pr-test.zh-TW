---
title: "aaaX12 B2B 企業整合 Azure 邏輯應用程式訊息 |Microsoft 文件"
description: "利用 Azure Logic Apps 交換 EDI 格式的 X12 訊息以進行 B2B 企業整合"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 7422d2d5-b1c7-4a11-8c9b-0d8cfa463164
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/31/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 20a077b299875a16ada66a500d5f1c8f9972d309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="exchange-x12-messages-for-enterprise-integration-with-logic-apps"></a>利用邏輯應用程式交換適用於企業整合的 X12 訊息

您必須先建立 X12 合約並將該合約儲存在您的整合帳戶中，才可以交換 X12 訊息。 以下是如何 hello 步驟 toocreate x12 協議。

> [!NOTE]
> 此頁面涵蓋 Azure Logic Apps hello X12 功能。 如需詳細資訊，請參閱 [EDIFACT](logic-apps-enterprise-integration-edifact.md)。

## <a name="before-you-start"></a>開始之前

以下是您所需要的 hello 項目：

* 已經定義並與 Azure 訂用帳戶相關聯的[整合帳戶](../logic-apps/logic-apps-enterprise-integration-accounts.md)
* 在至少兩個[夥伴](../logic-apps/logic-apps-enterprise-integration-partners.md)，定義在整合帳戶且設有 hello X12 識別碼下**商務識別**    
* 必要[結構描述](../logic-apps/logic-apps-enterprise-integration-schemas.md)上傳 tooyour[整合帳戶](../logic-apps/logic-apps-enterprise-integration-accounts.md)

之後您[建立整合帳戶](../logic-apps/logic-apps-enterprise-integration-accounts.md)，[加入夥伴](logic-apps-enterprise-integration-partners.md)，而且有[結構描述](../logic-apps/logic-apps-enterprise-integration-schemas.md)toouse，您可以建立 X12 協議，依照下列步驟。

## <a name="create-an-x12-agreement"></a>建立 X12 合約

1.  登入 toohello [Azure 入口網站](http://portal.azure.com "Azure 入口網站")。 從 hello 左窗格中，選取**更多服務**。 

    > [!TIP]
    > 如果您沒有看到**更多服務**，您可能必須 tooexpand hello 功能表第一次。 在 hello hello 摺疊功能表頂端，選取**顯示功能表**。

    ![在左側功能表上選取 [更多服務]](./media/logic-apps-enterprise-integration-x12/account-1.png)

2.  在 hello 搜尋方塊中，輸入 「 整合 」 做為您的篩選器。 在 hello 結果清單中，選取 **整合帳戶**。  

    ![依據 [整合] 篩選，選取 [整合帳戶]](./media/logic-apps-enterprise-integration-x12/account-2.png)

3. 在 hello**整合帳戶**刀鋒視窗中開啟，您想要 tooadd hello 協議選取 hello 整合帳戶。
如果沒有看到任何整合帳戶，請[先建立一個](../logic-apps/logic-apps-enterprise-integration-accounts.md "關於整合帳戶的一切")。

    ![選取其中 toocreate hello 協議的整合帳戶](./media/logic-apps-enterprise-integration-x12/account-3.png)

4. 選取**概觀**，然後選取 hello**協議**磚。 如果您還沒有合約磚，請先新增 hello 磚。 

    ![選擇 [合約] 圖格](./media/logic-apps-enterprise-integration-agreements/agreement-1.png)

5. 在 hello 協議刀鋒視窗中開啟，選擇 **新增**。

    ![選擇 [新增]](./media/logic-apps-enterprise-integration-agreements/agreement-2.png)     

6. 在 [新增] 之下，輸入合約的 [名稱]。 Hello 合約類型 選取**X12**。 選取 hello**主控合作夥伴**，**主機識別**，**來賓夥伴**，和**客體身分識別**協議。 如需屬性的詳細資訊，請參閱在此步驟中的 hello 資料表。

    ![提供合約詳細資料](./media/logic-apps-enterprise-integration-x12/x12-1.png)  

    | 屬性 | 說明 |
    | --- | --- |
    | 名稱 |Hello 協議的名稱 |
    | 合約類型 | 應該是 X12 |
    | 主控夥伴 |合約需要主控夥伴和來賓夥伴。 hello 主控合作夥伴代表 hello 組織設定 hello 協議。 |
    | 主控身分識別 |Hello 主控合作夥伴的的識別項 |
    | 來賓夥伴 |合約需要主控夥伴和來賓夥伴。 hello 來賓夥伴代表正在進行 hello 主控合作夥伴與商務的 hello 組織。 |
    | 來賓身分識別 |Hello 來賓夥伴的的識別項 |
    | 接收設定 |這些屬性會套用 tooall 的協議所收到的訊息。 |
    | 傳送設定 |這些屬性會套用 tooall 的協議所傳送的訊息。 |  

  > [!NOTE]
  > X12 協議，取決於比對 hello 傳送者辨識符號和識別項和 hello 接收者辨識符號和識別碼 hello 夥伴和內送訊息中定義的解析。 如果這些值會變更您的合作夥伴，請太更新 hello 協議。

## <a name="configure-how-your-agreement-handles-received-messages"></a>設定合約處理所收到訊息的方式

既然您已經設定 hello 協議屬性，您可以設定如何識別本合約，以及處理從夥伴透過此協議接收內送訊息。

1.  在 [新增] 之下，選取 [接收設定]。
設定這些屬性，根據您的合約與 hello 夥伴與您交換訊息。 屬性描述，請參閱本節中的 hello 表格。

    [接收設定] 分成下列各區段：識別碼、通知、結構描述、信封、控制編號、驗證和內部設定。

2. 瀏覽完畢之後，請確定 toosave 您的設定選擇**確定**。

現在您的合約已準備好 toohandle 內送訊息符合 tooyour 選取的設定。

### <a name="identifiers"></a>識別項

![設定識別碼屬性](./media/logic-apps-enterprise-integration-x12/x12-2.png)  

| 屬性 | 說明 |
| --- | --- |
| ISA1 (授權辨識符號) |從 hello 下拉式清單中選取 hello 授權辨識符號值。 |
| ISA2 |選用。 輸入授權資訊值。 若為 ISA1 輸入的 hello 值不是 00，輸入最少一個英數字元和最多 10 個。 |
| ISA3 (安全性辨識符號) |從 hello 下拉式清單中選取 hello 安全性辨識符號值。 |
| ISA4 |選用。 輸入 hello 安全性資訊值。 若為 ISA3 輸入的 hello 值不是 00，輸入最少一個英數字元和最多 10 個。 |

### <a name="acknowledgment"></a>通知

![設定通知屬性](./media/logic-apps-enterprise-integration-x12/x12-3.png) 

| 屬性 | 說明 |
| --- | --- |
| 預期 TA1 |傳回技術通知 toohello 交換傳送者 |
| 預期 FA |傳回功能通知 toohello 交換傳送者。 然後選取您要讓 hello 997 或 999 通知根據 hello 結構描述版本 |
| 包含 AK2/IK2 迴圈 |在功能通知中針對已接受的交易集啟用 AK2 迴圈的產生 |

### <a name="schemas"></a>結構描述

選取每個交易類型 (ST1) 和傳送者應用程式 (GS2) 的結構描述。 hello 接收管線將拆解藉由符合針對 ST1 hello 值的 hello 內送訊息和 hello hello 傳入訊息中的 GS2 值的集合，並 hello hello 內送訊息的 hello 您在此處設定的結構描述。

![選取結構描述](./media/logic-apps-enterprise-integration-x12/x12-33.png) 

| 屬性 | 說明 |
| --- | --- |
| 版本 |選取 hello X12 版本 |
| 交易類型 (ST01) |選取 hello 交易類型 |
| 傳送者應用程式 (GS02) |選取 hello 寄件者應用程式 |
| 結構描述 |選取您想要 toouse hello 結構描述檔案。 結構描述會加入 tooyour 整合帳戶。 |

> [!NOTE]
> 設定所需的 hello[結構描述](../logic-apps/logic-apps-enterprise-integration-schemas.md)也就是上傳的 tooyour[整合帳戶](../logic-apps/logic-apps-enterprise-integration-accounts.md)。

### <a name="envelopes"></a>信封

![指定交易集中的 hello 分隔符號： 選擇 標準識別項 或 重複分隔符號](./media/logic-apps-enterprise-integration-x12/x12-34.png)

| 屬性 | 說明 |
| --- | --- |
| ISA11 使用方法 |指定交易集中的 hello 分隔符號 toouse: <p>選取**標準識別項**toouse 句號 （.） 的十進位表示法，而不是 hello 十進位表示法來 hello 內送文件以 hello EDI 接收管線。 <p>選取**重複分隔符號**toospecify hello 分隔符號為重複出現的簡易資料元素或重複的資料結構。 例如，通常 hello 克拉記號 (^) 是用來做 hello 重複分隔符號。 針對 HIPAA 結構描述，您可以只使用 hello 克拉記號。 |

### <a name="control-numbers"></a>控制編號

![選取 toohandle 如何控制號碼重複](./media/logic-apps-enterprise-integration-x12/x12-35.png) 

| 屬性 | 說明 |
| --- | --- |
| 不允許交換控制編號重複 |封鎖重複的交換。 檢查 hello 交換控制編號 (ISA13) 收到 hello 交換控制編號。 Hello 如果偵測到相符項目時，接收管線無法處理 hello 交換。 您可以指定 hello 的天數由值，以執行 hello 檢查*檢查每個 （天） 是否有重複的 ISA13*。 |
| 不允許群組控制編號重複 |封鎖有重複群組控制編號的交換。 |
| 不允許交易集控制編號重複 |封鎖有重複交易集控制編號的交換。 |

### <a name="validations"></a>驗證

![設定已接收訊息的驗證屬性](./media/logic-apps-enterprise-integration-x12/x12-36.png) 

當您完成每個驗證資料列時，將會自動新增另一個驗證資料列。 如果您未指定任何規則，驗證會使用 hello 「 預設 」 的資料列。

| 屬性 | 說明 |
| --- | --- |
| 訊息類型 |選取 hello EDI 訊息類型。 |
| EDI 驗證 |資料類型所定義的 hello 結構描述的 EDI 內容、 長度限制、 空白資料元素和尾端分隔符號執行 EDI 驗證。 |
| 擴充驗證 |如果 hello 資料型別不是 EDI，驗證在 hello 資料元素需求上，並允許重複、 列舉和資料元素長度驗證 （最小/最大）。 |
| 允許前置/尾端零 |保留任何額外的前置或尾端零及空格字元。 請勿移除這些字元。 |
| 修剪前置/尾端零 |移除前置或尾端零及空格字元。 |
| 尾端分隔符號原則 |產生尾端分隔符號。 <p>選取**不允許**tooprohibit 尾端分隔符號，並在 hello 分隔符號接收交換。 如果 hello 交換有尾端分隔符號與分隔字元，hello 交換宣告不正確。 <p>選取**選擇性**tooaccept 交換或不具有結尾分隔字元。 <p>選取**強制**hello 交換時必須有尾端分隔符號與分隔字元。 |

### <a name="internal-settings"></a>內部設定

![選取內部設定](./media/logic-apps-enterprise-integration-x12/x12-37.png) 

| 屬性 | 說明 |
| --- | --- |
| 將隱含的十進位格式"Nn 」 tooa 基底 10 數值轉換 |將轉換成基底 10 數值 hello 格式"Nn 」 指定的 EDI 數字 |
| 如果允許尾端分隔符號，則建立空的 XML 標籤 |選取此核取方塊 toohave hello 交換傳送者包含空白針對尾端分隔符號的 XML 標記。 |
| 將交換分割為交易集 - 發生錯誤時暫停交易集|每個交易集剖析成個別的 XML 文件的交換中藉由套用 hello 適當的信封 toohello 交易集。 暫停只有 hello 交易當 hello 驗證失敗。 |
| 將交換分割為交易集 - 發生錯誤時暫停交換|每個交易集剖析成個別的 XML 文件的交換中藉由套用 hello 適當的信封。 Hello 交換中的一個或多個交易集驗證失敗時，會暫停整個交換。 | 
| 保留交換 - 發生錯誤時暫停交易集 |會保留 hello 交換，然後建立 hello 整個批次交換的 XML 文件。 只會暫停 hello 交易集無法通過驗證，但仍繼續 tooprocess，所有其他交易集。 |
| 保留交換 - 發生錯誤時暫停交換 |會保留 hello 交換，然後建立 hello 整個批次交換的 XML 文件。 Hello 交換中的一個或多個交易集驗證失敗時，會暫停整個交換的 hello。 |

## <a name="configure-how-your-agreement-sends-messages"></a>設定合約傳送訊息的方式

您可以設定此協議如何識別及處理外寄傳送 tooyour 夥伴透過此合約的訊息。

1.  在 [新增] 之下，選取 [傳送設定]。
根據您與其交換訊息之夥伴所簽署的合約，設定這些屬性。 屬性描述，請參閱本節中的 hello 表格。

    [傳送設定] 分成下列各區段：識別碼、通知、結構描述、信封、字元集和分隔符號、控制編號以及驗證。

2. 瀏覽完畢之後，請確定 toosave 您的設定選擇**確定**。

現在您的合約是準備 toohandle 外寄訊息符合 tooyour 選取的設定。

### <a name="identifiers"></a>識別項

![設定識別碼屬性](./media/logic-apps-enterprise-integration-x12/x12-4.png)  

| 屬性 | 說明 |
| --- | --- |
| 授權辨識符號 (ISA1) |從 hello 下拉式清單中選取 hello 授權辨識符號值。 |
| ISA2 |輸入授權資訊值。 如果此值不是 00，則請最少輸入 1 個，最多 10 個英數字元。 |
| 安全性辨識符號 (ISA3) |從 hello 下拉式清單中選取 hello 安全性辨識符號值。 |
| ISA4 |輸入 hello 安全性資訊值。 如果此值不是 00，hello 值 (ISA4) 文字方塊中，然後輸入最少一個英數值，最多為 10。 |

### <a name="acknowledgment"></a>通知

![設定通知屬性](./media/logic-apps-enterprise-integration-x12/x12-5.png)  

| 屬性 | 說明 |
| --- | --- |
| 預期 TA1 |傳回技術通知 (TA1) toohello 交換傳送者。 此設定會指定該 hello 主控合作夥伴傳送 hello 訊息要求通知從 hello 協議中的 hello 來賓夥伴。 這些通知會預期收到 hello 主控合作夥伴根據 hello hello 協議的接收設定。 |
| 預期 FA |傳回功能通知 」 (FA) toohello 交換傳送者。 選取您要讓 hello 997 或 999 通知，根據您正在使用的 hello 結構描述版本。 這些通知會預期收到 hello 主控合作夥伴根據 hello hello 協議的接收設定。 |
| FA 版本 |選取 hello FA 版本 |

### <a name="schemas"></a>結構描述

![選取結構描述 toouse](./media/logic-apps-enterprise-integration-x12/x12-5.png)  

| 屬性 | 說明 |
| --- | --- |
| 版本 |選取 hello X12 版本 |
| 交易類型 (ST01) |選取 hello 交易類型 |
| 結構描述 |選取 hello 結構描述 toouse。 結構描述位於您的整合帳戶中。 若先選取結構描述，它會自動設定版本與交易類型  |

> [!NOTE]
> 設定所需的 hello[結構描述](../logic-apps/logic-apps-enterprise-integration-schemas.md)也就是上傳的 tooyour[整合帳戶](../logic-apps/logic-apps-enterprise-integration-accounts.md)。

### <a name="envelopes"></a>信封

![指定交易集中的 hello 分隔符號： 選擇 標準識別項 或 重複分隔符號](./media/logic-apps-enterprise-integration-x12/x12-6.png) 

| 屬性 | 說明 |
| --- | --- |
| ISA11 使用方法 |指定交易集中的 hello 分隔符號 toouse: <p>選取**標準識別項**toouse 句號 （.） 的十進位表示法，而不是 hello 十進位表示法來 hello 內送文件以 hello EDI 接收管線。 <p>選取**重複分隔符號**toospecify hello 分隔符號為重複出現的簡易資料元素或重複的資料結構。 例如，通常 hello 克拉記號 (^) 是用來做 hello 重複分隔符號。 針對 HIPAA 結構描述，您可以只使用 hello 克拉記號。 |

### <a name="control-numbers"></a>控制編號

![指定控制編號屬性](./media/logic-apps-enterprise-integration-x12/x12-8.png) 

| 屬性 | 說明 |
| --- | --- |
| 控制版本編號 (ISA12) |選取 hello hello X12 標準版本 |
| 使用狀況指示符號 (ISA15) |選取 hello 交換的內容。  hello 值的詳細資訊，實際執行資料或測試資料 |
| 結構描述 |Hello GS 和 ST 區段，它會傳送 toohello 傳送管線的 X12 編碼交換產生 |
| GS1 |選擇性，選取一個 hello 下拉式清單中的 hello 功能代碼的值 |
| GS2 |選擇性，應用程式寄件者 |
| GS3 |選擇性，應用程式接收者 |
| GS4 |選擇性，請選取 CCYYMMDD 或 YYMMDD |
| GS5 |選擇性，請選取 HHMM、HHMMSS 或 HHMMSSdd |
| GS7 |選擇性，選取一個 hello 下拉式清單中的 hello 負責單位的值 |
| GS8 |選擇性的 hello 文件版本 |
| 交換控制編號 (ISA13) |必要輸入 hello 交換控制編號值的範圍。 請輸入最小為 1，最大為 999999999 的數值 |
| 群組控制編號 (GS06) |需要，請輸入 hello 群組控制編號的數字範圍。 請輸入最小為 1，最大為 999999999 的數值 |
| 交易集控制編號 (ST02) |必要輸入 hello 交易集控制編號的數字範圍。 請輸入最小為 1，最大為 999999999 的數值範圍 |
| 前置詞 |選擇性，指定用於認可的交易集控制編號的 hello 範圍。 輸入數值 hello 中間兩個欄位和的英數字元值 （如有需要） hello 前置詞和尾碼欄位。 hello 的中間欄位是必要，而且包含 hello 最小值和 hello 控制編號的最大值 |
| 尾碼 |選擇性，指定通知中使用的交易集控制編號的 hello 範圍。 輸入 hello 中間兩個欄位的數值和的英數字元值 （如有需要） hello 前置詞和尾碼欄位。 hello 的中間欄位是必要，而且包含 hello 最小值和 hello 控制編號的最大值 |

### <a name="character-sets-and-separators"></a>字元集和分隔符號

除了 hello 字元集，您可以輸入不同的分隔符號集的每個訊息類型。 如果指定的訊息結構描述未指定字元集，則會使用預設字元集 hello。

![指定不同訊息類型的分隔符號](./media/logic-apps-enterprise-integration-x12/x12-9.png) 

| 屬性 | 說明 |
| --- | --- |
| 使用的字元組 toobe |toovalidate hello 屬性中，選取 hello X12 字元集。 hello 選項為 Basic、 擴充的 」 和 UTF8。 |
| 結構描述 |從 hello 下拉式清單中選取結構描述。 在您完成每個資料列時，便會自動新增一個資料列。 選取 hello 分隔符號 hello 選取的結構描述，設定您想 toouse，根據下列分隔符號描述 hello。 |
| 輸入類型 |從 hello 下拉式清單中選取的輸入的類型。 |
| 元件分隔符號 |tooseparate 複合資料元素，請輸入單一字元。 |
| 資料元素分隔符號 |tooseparate 複合資料元素內的簡單資料元素輸入單一字元。 |
| 取代字元 |輸入取代字元用於取代 hello 裝載資料中的所有分隔符號字元時產生輸出 X12 hello 訊息。 |
| 區段結束字元 |tooindicate hello EDI 區段結束，請輸入單一字元。 |
| 尾碼 |選取 hello 字元 hello 區段識別碼搭配使用。 如果您指定尾碼，則 hello 區段結束字元資料元素可以是空的。 如果 hello 區段結束字元留白，您必須指定尾碼。 |

> [!TIP]
> tooprovide 特殊字元的值，編輯 hello 協議為 JSON，並提供 hello ASCII 值 hello 特殊字元。

### <a name="validation"></a>驗證

![設定驗證屬性以便傳送訊息](./media/logic-apps-enterprise-integration-x12/x12-10.png) 

當您完成每個驗證資料列時，將會自動新增另一個驗證資料列。 如果您未指定任何規則，驗證會使用 hello 「 預設 」 的資料列。

| 屬性 | 說明 |
| --- | --- |
| 訊息類型 |選取 hello EDI 訊息類型。 |
| EDI 驗證 |資料類型所定義的 hello 結構描述的 EDI 內容、 長度限制、 空白資料元素和尾端分隔符號執行 EDI 驗證。 |
| 擴充驗證 |如果 hello 資料型別不是 EDI，驗證在 hello 資料元素需求上，並允許重複、 列舉和資料元素長度驗證 （最小/最大）。 |
| 允許前置/尾端零 |保留任何額外的前置或尾端零及空格字元。 請勿移除這些字元。 |
| 修剪前置/尾端零 |移除前置或尾端零字元。 |
| 尾端分隔符號原則 |產生尾端分隔符號。 <p>選取**不允許**tooprohibit 尾端分隔符號，並在 hello 分隔符號傳送交換。 如果 hello 交換有尾端分隔符號與分隔字元，hello 交換宣告不正確。 <p>選取**選擇性**toosend 交換或不具有結尾分隔字元。 <p>選取**強制**如果傳送嗨交換必須有尾端分隔符號與分隔字元。 |

## <a name="find-your-created-agreement"></a>尋找您建立的合約

1.  完成設定您協議屬性，在 hello 之後**新增**刀鋒視窗中，選擇**確定**toofinish 建立您的合約和傳回 tooyour 整合帳戶 刀鋒視窗。

    您新增的合約現在顯示於您的 [合約] 清單中。

2.  您也可以在整合帳戶概觀中檢視您的合約。 在您整合帳戶] 刀鋒視窗中，選擇 [**概觀**，然後選取 hello**協議**磚。

    ![選擇 「 合約 」 磚 tooview 所有協議](./media/logic-apps-enterprise-integration-x12/x12-1-5.png)   

## <a name="view-hello-swagger"></a>檢視 hello swagger
請參閱 hello [swagger 詳細資料](/connectors/x12/)。 

## <a name="learn-more"></a>詳細資訊
* [深入了解 hello Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md "深入了解 Enterprise Integration Pack")  

