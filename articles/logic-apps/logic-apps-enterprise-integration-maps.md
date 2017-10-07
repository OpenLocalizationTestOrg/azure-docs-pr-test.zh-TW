---
title: "使用 XSLT 對應-Azure Logic Apps aaaTransform XML |Microsoft 文件"
description: "加入 XSLT 對應 tootransform Azure 邏輯應用程式與 hello 企業版整合套件的 XML 資料"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 90f5cfc4-46b2-4ef7-8ac4-486bb0e3f289
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 720e6f988b8542136dfcc402c3c463fcfb2f23cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-maps-for-xml-data-transform"></a>針對 XML 資料轉換新增對應

企業整合會使用對應 tootransform 格式之間的 XML 資料。 對應是定義 hello 資料應該轉換成其他格式的文件中的 XML 文件。 

## <a name="why-use-maps"></a>為什麼要使用對應？

假設您定期 B2B 訂單或發票從接收的客戶使用 hello YYYMMDD 格式的日期。 不過，您的組織，在您儲存 hello MMDDYYY 格式的日期。 您也可以使用對應*轉換*hello MMDDYYY hello 訂單或發票詳細資料儲存在您的客戶活動資料庫之前 hello YYYMMDD 日期格式。

## <a name="how-do-i-create-a-map"></a>如何建立對應？

您可以建立 BizTalk 整合專案以 hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "深入了解 hello 企業版整合套件")for Visual Studio 2015。 接著，您可以建立整合對應檔案，以便以視覺方式對應兩個 XML 結構描述檔案中的項目。 建置此專案之後，您將擁有 XSLT 文件。

## <a name="how-do-i-add-a-map"></a>如何新增對應？

1. 在 hello Azure 入口網站，選取 **瀏覽**。

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. 在 hello 篩選搜尋方塊中，輸入**整合**，然後選取**整合帳戶**hello 結果清單中。

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. 選取您想要 tooadd hello 對應 hello 整合帳戶。

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. 選取 hello**對應**磚。

    ![](./media/logic-apps-enterprise-integration-maps/map-1.png)

5. Hello 對應刀鋒視窗開啟後，請選擇**新增**。

    ![](./media/logic-apps-enterprise-integration-maps/map-2.png)  

6. 在 [名稱] 中輸入對應的名稱。 tooupload hello 對應檔案中，選擇右側 hello hello hello 資料夾圖示**對應**文字方塊。 Hello 上傳程序完成之後，請選擇**確定**。

    ![](./media/logic-apps-enterprise-integration-maps/map-3.png)

7. Azure 會新增 hello 對應 tooyour 整合帳戶之後，您會取得對應檔是否已加入或不會顯示在螢幕上訊息。 您會收到此訊息之後，請選擇 hello**對應**磚，使您可以檢視 hello 新加入的對應。

    ![](./media/logic-apps-enterprise-integration-maps/map-4.png)

## <a name="how-do-i-edit-a-map"></a>如何編輯對應？

您必須上傳新的對應檔具有您想要的 hello 變更。 您可以先下載 hello 編輯對應。

tooupload 新的對應，以取代 hello 現有對應，請遵循下列步驟。

1. 選擇 hello**對應**磚。

2. Hello 對應刀鋒視窗開啟後，請選取您想 tooedit hello 對應。

3. 在 hello**對應**刀鋒視窗中，選擇**更新**。

    ![](./media/logic-apps-enterprise-integration-maps/edit-1.png)

4. 在 hello 檔案選擇器中，選取 hello 對應檔案，tooupload，然後選取**開啟**。

    ![](./media/logic-apps-enterprise-integration-maps/edit-2.png)

## <a name="how-toodelete-a-map"></a>如何 toodelete 對應嗎？

1. 選擇 hello**對應**磚。

2. Hello 對應刀鋒視窗開啟之後，選取您想要 toodelete hello 對應。

3. 選擇 [刪除]。

    ![](./media/logic-apps-enterprise-integration-maps/delete.png)

4. 確認您想 toodelete hello 對應。

    ![](./media/logic-apps-enterprise-integration-maps/delete-confirmation-1.png)

## <a name="next-steps"></a>後續步驟
* [深入了解 hello Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "深入了解 Enterprise Integration Pack")  
* [深入了解合約](../logic-apps/logic-apps-enterprise-integration-agreements.md "了解企業整合合約")  
* [深入了解轉換](logic-apps-enterprise-integration-transform.md "了解企業整合轉換")  

