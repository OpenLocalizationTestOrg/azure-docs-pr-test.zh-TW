---
title: "aaaAS2 B2B 企業整合 Azure 邏輯應用程式訊息 |Microsoft 文件"
description: "利用 Azure Logic Apps 交換適用於 B2B 企業整合的 AS2 訊息"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: c9b7e1a9-4791-474c-855f-988bd7bf4b7f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: LADocs; mandia
ms.openlocfilehash: 23f9d74dd0ad807e9cdaedb320d60496cfef9bc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="exchange-as2-messages-for-enterprise-integration-with-logic-apps"></a>利用邏輯應用程式交換適用於企業整合的 AS2 訊息

您必須先建立 AS2 合約並將該合約儲存在您的整合帳戶中，才可以交換 AS2 訊息。 以下是如何 hello 步驟 toocreate AS2 協議。

## <a name="before-you-start"></a>開始之前

以下是您所需要的 hello 項目：

* 已經定義並與 Azure 訂用帳戶相關聯的[整合帳戶](../logic-apps/logic-apps-enterprise-integration-accounts.md)
* 在至少兩個[夥伴](logic-apps-enterprise-integration-partners.md)，已經定義在整合帳戶並且使用 hello AS2 限定詞下設定**商務識別**

> [!NOTE]
> 當您建立協議時，hello 合約檔案中的 hello 內容必須符合 hello 合約類型。    

在您[建立整合帳戶](../logic-apps/logic-apps-enterprise-integration-accounts.md)並[新增夥伴](logic-apps-enterprise-integration-partners.md)之後，您可以依照下列步驟建立 AS2 合約。

## <a name="create-an-as2-agreement"></a>建立 AS2 合約

1.  登入 toohello [Azure 入口網站](http://portal.azure.com "Azure 入口網站")。  

2.  從 hello 左窗格中，選取**更多服務**。 在 [hello] 搜尋方塊中，輸入**整合**做為您的篩選條件。 在 hello 結果清單中，選取 **整合帳戶**。

    > [!TIP]
    > 如果您沒有看到**更多服務**，您可能必須 tooexpand hello 功能表第一次。 在 hello hello 摺疊功能表頂端，選取**顯示功能表**。

    ![更多服務，依據 [整合] 篩選，選取 [整合帳戶]](./media/logic-apps-enterprise-integration-agreements/overview-1.png)

3. 在 hello**整合帳戶**刀鋒視窗中開啟，您想要 toocreate hello 協議選取 hello 整合帳戶。
如果沒有看到任何整合帳戶，請[先建立一個](../logic-apps/logic-apps-enterprise-integration-accounts.md "關於整合帳戶的一切")。  

    ![選取其中 toocreate hello 協議的 hello 整合帳戶](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. 選擇 hello**協議**磚。 如果您還沒有合約磚，請先新增 hello 磚。

    ![選擇 [合約] 圖格](./media/logic-apps-enterprise-integration-agreements/agreement-1.png)

5. 在 hello 協議刀鋒視窗中開啟，選擇 **新增**。

    ![選擇 [新增]](./media/logic-apps-enterprise-integration-agreements/agreement-2.png)

6. 在 [新增] 之下，輸入合約的 [名稱]。 針對 [合約類型]，選取 **AS2**。 選取 hello**主控合作夥伴**，**主機識別**，**來賓夥伴**，和**客體身分識別**協議。

    ![提供合約詳細資料](./media/logic-apps-enterprise-integration-agreements/agreement-3.png)  

    | 屬性 | 說明 |
    | --- | --- |
    | 名稱 |Hello 協議的名稱 |
    | 合約類型 | 應該是 AS2 |
    | 主控夥伴 |合約需要主控夥伴和來賓夥伴。 hello 主控合作夥伴代表 hello 組織設定 hello 協議。 |
    | 主控身分識別 |Hello 主控合作夥伴的的識別項 |
    | 來賓夥伴 |合約需要主控夥伴和來賓夥伴。 hello 來賓夥伴代表正在進行 hello 主控合作夥伴與商務的 hello 組織。 |
    | 來賓身分識別 |Hello 來賓夥伴的的識別項 |
    | 接收設定 |這些屬性會套用 tooall 的協議所收到的訊息。 |
    | 傳送設定 |這些屬性會套用 tooall 的協議所傳送的訊息。 |

## <a name="configure-how-your-agreement-handles-received-messages"></a>設定合約處理所收到訊息的方式

既然您已經設定 hello 協議屬性，您可以設定如何識別本合約，以及處理從夥伴透過此協議接收內送訊息。

1.  在 [新增] 之下，選取 [接收設定]。
設定這些屬性，根據您的合約與 hello 夥伴與您交換訊息。 如屬性描述，請參閱本節中的 hello 資料表。

    ![設定 [接收設定]](./media/logic-apps-enterprise-integration-agreements/agreement-4.png)

2. （選擇性） 您可以覆寫內送訊息的 hello 屬性選取**覆寫訊息屬性**。

3. toorequire 所有內送訊息 toobe 簽署，請選取**訊息應該簽署**。 從 hello**憑證**清單中，選取現有[來賓夥伴公開憑證](../logic-apps/logic-apps-enterprise-integration-certificates.md)驗證 hello hello 訊息上的簽章。 或如果您沒有建立 hello 憑證。

4.  選取 toorequire 加密，所有內送訊息 toobe**訊息應該加密**。 從 hello**憑證**清單中，選取現有[主機夥伴私人憑證](../logic-apps/logic-apps-enterprise-integration-certificates.md)解密內送訊息。 或如果您沒有建立 hello 憑證。

5. toorequire 訊息 toobe 壓縮，選取**訊息應該壓縮**。

6. toosend 接收的訊息，同步訊息處理通知 (MDN) 選取**傳送 MDN**。

7. toosend 簽署 Mdn 的接收的訊息，選取**傳送簽署的 MDN**。

8. 非同步的 Mdn 接收之訊息，選取 toosend**傳送非同步 MDN**。

9. 瀏覽完畢之後，請確定 toosave 您的設定選擇**確定**。

現在您的合約已準備好 toohandle 內送訊息符合 tooyour 選取的設定。

| 屬性 | 說明 |
| --- | --- |
| 覆寫訊息屬性 |指出所接收訊息中可被覆寫的屬性。 |
| 訊息應該簽署 |需要訊息 toobe 數位簽章。 設定用於簽章驗證的 hello 來賓夥伴公開憑證。  |
| 訊息應該加密 |需要加密的訊息 toobe。 未加密的訊息會遭到拒絕。 設定用於解密 hello 訊息的 hello 主機夥伴私人憑證。  |
| 訊息應該壓縮 |需要訊息 toobe 壓縮。 未壓縮的訊息會遭到拒絕。 |
| MDN 文字 |hello 預設訊息處置通知 (MDN) toobe 傳送 toohello 訊息寄件者。 |
| 傳送 MDN |需要傳送 Mdn toobe。 |
| 傳送簽署的 MDN |需要已簽署的 Mdn toobe。 |
| MIC 演算法 |選取 hello 演算法 toouse 簽署訊息。 |
| 傳送非同步 MDN | 需要訊息 toobe 以非同步方式傳送。 |
| URL | 指定 hello toosend 其中 hello Mdn 的 URL。 |

## <a name="configure-how-your-agreement-sends-messages"></a>設定合約傳送訊息的方式

您可以設定此協議如何識別及處理外寄傳送 tooyour 夥伴透過此合約的訊息。

1.  在 [新增] 之下，選取 [傳送設定]。
設定這些屬性，根據您的合約與 hello 夥伴與您交換訊息。 如屬性描述，請參閱本節中的 hello 資料表。

    ![設定 hello [傳送設定] 屬性](./media/logic-apps-enterprise-integration-agreements/agreement-51.png)

2. toosend 簽章的訊息 tooyour 夥伴、 選取**啟用訊息簽署**。 用於簽章 hello 訊息，請在 hello **MIC 演算法**清單中，選取 hello*主機夥伴私人憑證 MIC 演算法*。 在 hello**憑證**清單中，選取現有[主機夥伴私人憑證](../logic-apps/logic-apps-enterprise-integration-certificates.md)。

3. toosend 加密的訊息 toohello 夥伴、 選取**啟用訊息加密**。 加密 hello 訊息，請在 hello**加密演算法**清單中，選取 hello*來賓夥伴公開憑證演算法*。
在 hello**憑證**清單中，選取現有[來賓夥伴公開憑證](../logic-apps/logic-apps-enterprise-integration-certificates.md)。

4. toocompress hello 訊息，選取**啟用訊息壓縮**。

5. 單一資料行，選取 toounfold hello HTTP content-type 標頭**展開 HTTP 標頭**。

6. tooreceive hello 同步 Mdn 傳送訊息，選取**要求 MDN**。

7. tooreceive 簽署 Mdn 之傳送 hello 訊息，選取**要求簽署的 MDN**。

8. tooreceive hello 非同步 Mdn 傳送訊息，選取**要求非同步 MDN**。 如果您選取此選項，輸入 hello URL toosend hello Mdn 的位置。

9. 選取 toorequire 不可否認性回條、**啟用 NRR**。  

10. 選取在 hello MIC toospecify 演算法格式 toouse 或登入 hello 傳出標頭的 hello AS2 訊息或 MDN， **SHA2 演算法格式**。  

11. 瀏覽完畢之後，請確定 toosave 您的設定選擇**確定**。

現在您的合約是準備 toohandle 外寄訊息符合 tooyour 選取的設定。

| 屬性 | 說明 |
| --- | --- |
| 啟用訊息簽署 |需要從帶正負號的 hello 協議 toobe 傳送的所有訊息。 |
| MIC 演算法 |hello 演算法 toouse 簽署訊息。 設定 hello 主機夥伴私人憑證 MIC 演算法來簽署 hello 訊息。 |
| 憑證 |選取 hello 憑證 toouse 簽署訊息。 設定 hello 主機夥伴私人憑證來簽署 hello 訊息。 |
| 啟用訊息加密 |要求傳送自此合約的所有訊息都必須經過加密。 設定 hello 來賓夥伴公開憑證演算法來加密 hello 訊息。 |
| 加密演算法 |hello 訊息加密的加密演算法 toouse。 設定加密 hello 訊息的 hello 來賓夥伴公開憑證。 |
| 憑證 |hello 憑證 toouse tooencrypt 訊息。 設定加密 hello 訊息的 hello 來賓夥伴私人憑證。 |
| 啟用訊息壓縮 |要求傳送自此合約的所有訊息都必須經過壓縮。 |
| 展開 HTTP 標頭 |會放置到單一行 hello HTTP content-type 標頭。 |
| 要求 MDN |針對傳送自此合約的所有訊息要求 MDN。 |
| 要求簽署的 MDN |需要所有傳送 toothis 協議 toobe 簽署的 Mdn。 |
| 要求非同步 MDN |要求非同步 Mdn 傳送 toobe toothis 協議。 |
| URL |指定 hello toosend 其中 hello Mdn 的 URL。 |
| 啟用 NRR |需要不可否認性回條 (NRR)，提供辨識項 hello 資料通訊屬性收到因為收件者。 |
| SHA2 演算法格式 |選取演算法格式 toouse hello MIC 或登入 hello 傳出 hello AS2 訊息或 MDN 的標頭中 |

## <a name="find-your-created-agreement"></a>尋找您建立的合約

1.  完成設定您協議屬性，在 hello 之後**新增**刀鋒視窗中，選擇**確定**toofinish 建立您的合約和傳回 tooyour 整合帳戶 刀鋒視窗。

    您新增的合約現在顯示於您的 [合約] 清單中。

2.  您也可以在整合帳戶概觀中檢視您的合約。 在您整合帳戶] 刀鋒視窗中，選擇 [**概觀**，然後選取 hello**協議**磚。 

    ![選擇 「 合約 」 磚 tooview 所有協議](./media/logic-apps-enterprise-integration-agreements/agreement-6.png)

## <a name="view-hello-swagger"></a>檢視 hello swagger
請參閱 hello [swagger 詳細資料](/connectors/as2/)。 

## <a name="next-steps"></a>後續步驟
* [深入了解 hello Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "深入了解 Enterprise Integration Pack")  
