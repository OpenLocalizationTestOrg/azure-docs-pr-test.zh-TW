---
title: "企業對企業 (B2B) 訊息-Azure 邏輯應用程式的 aaaCreate 夥伴 |Microsoft 文件"
description: "了解如何 tooadd 夥伴 tooyour 整合帳戶 hello 企業版整合套件與 Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: b179325c-a511-4c1b-9796-f7484b4f6873
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8dc70a8f441fcf228ed178029dcdbac940d794b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-update-partners-in-business-to-business-agreements-in-your-workflow"></a>新增或更新工作流程中企業對企業協議中的夥伴

合作夥伴是參與企業對企業 (B2B) 交易及在彼此之間交換訊息的實體。 在您可以建立這些交易中代表您與其他組織的合作夥伴之前，你們雙方必須先共用可識別及驗證彼此所傳送訊息的資訊。 在討論這些詳細資料，並已準備好 toostart 商務關係之後，您可以建立在您整合帳戶 toorepresent 夥伴雙方。

## <a name="what-roles-do-partners-have-in-your-integration-account"></a>合作夥伴在您的整合帳戶中扮演什麼角色？

有關夥伴之間交換的 hello 訊息 toodefine 詳細資料，您會建立這些夥伴之間的協議。 不過，您可以建立協議之前，您必須新增至少兩個夥伴 tooyour 整合帳戶。 您的組織必須為 hello hello 協議**主控合作夥伴**。 hello 另一個夥伴，或**來賓夥伴**代表 hello 與您的組織交換訊息的組織。 hello 來賓夥伴可以是另一家公司或甚至您組織中的部門。

在您新增這些合作夥伴之後，您可以建立合約。

接收和傳送設定會導向從 hello 觀點來看的 hello Hosted 夥伴。 例如，hello 接收協議中的設定判斷 hello 主控夥伴接收從來賓夥伴傳送訊息的方式。 同樣地，hello hello 協議上的傳送設定會指出 hello 主控夥伴傳送訊息 toohello 來賓夥伴的方式。

## <a name="how-toocreate-a-partner"></a>如何 toocreate 合作夥伴嗎？

1. 在 hello Azure 入口網站，選取 **瀏覽**。

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. 在 hello 篩選搜尋方塊中，輸入**整合**，然後選取**整合帳戶**hello 結果 清單中。

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. 選取您想 tooadd 合作夥伴之間的 hello 整合帳戶。

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. 選取 hello**夥伴**磚。

    ![](./media/logic-apps-enterprise-integration-partners/partner-1.png)

5. 在 hello 夥伴刀鋒視窗中，選擇 **新增**。

    ![](./media/logic-apps-enterprise-integration-partners/partner-2.png)

6. 輸入合作夥伴的名稱，然後選取 [辨識符號]。 最後，請輸入**值**toohelp 識別進入您的應用程式的文件。

    ![](./media/logic-apps-enterprise-integration-partners/partner-3.png)

7. 您的夥伴建立程序中，選取 hello toosee hello 進度*鈴鐺*通知圖示。

    ![](./media/logic-apps-enterprise-integration-partners/partner-4.png)

8. 加入新合作夥伴之間成功的 tooconfirm，選取 hello**夥伴**磚。

    ![](./media/logic-apps-enterprise-integration-partners/partner-5.png)

    選取 hello 夥伴磚之後，您也會看到新增的夥伴 hello 夥伴刀鋒視窗中。

    ![](./media/logic-apps-enterprise-integration-partners/partner-6.png)

## <a name="how-tooedit-existing-partners-in-your-integration-account"></a>如何 tooedit 現有整合帳戶中的合作夥伴

1. 選取 hello**夥伴**磚。
2. Hello 夥伴刀鋒視窗開啟後，請選取您想要 tooedit hello 夥伴。
3. 在 hello**更新夥伴**磚上，進行變更。
4. 瀏覽完畢之後，請選擇**儲存**，或您的變更，選取 toocancel**捨棄**。

    ![](./media/logic-apps-enterprise-integration-partners/edit-1.png)

## <a name="how-toodelete-a-partner"></a>如何 toodelete 合作夥伴

1. 選取 hello**夥伴**磚。
2. Hello 夥伴刀鋒視窗開啟後，請選取您想 toodelete hello 夥伴。
3. 選擇 [刪除]。

    ![](./media/logic-apps-enterprise-integration-partners/delete-1.png)

## <a name="next-steps"></a>後續步驟
* [深入了解合約](../logic-apps/logic-apps-enterprise-integration-agreements.md "了解企業整合合約")  

