---
title: "aaaValidate XML-Azure 邏輯應用程式 |Microsoft 文件"
description: "Azure 邏輯應用程式和 B2B 案例的結構描述驗證 XML，利用 hello 企業版整合套件"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: d700588f-2d8a-4c92-93eb-e1e6e250e760
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 81f662d0ddf908657b54de8af0a75fff55782ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-for-enterprise-integration"></a>針對企業整合驗證 XML

通常在 B2B 實例中，必須先確定 hello 訊息交換所有效之後，才能開始資料處理 hello 夥伴協議中。 您可以利用 hello 企業版整合套件中的 hello 使用 hello XML 驗證連接器驗證針對預先定義的結構描述的文件。

## <a name="validate-a-document-with-hello-xml-validation-connector"></a>驗證文件以 hello XML 驗證連接器

1. 建立邏輯應用程式和[hello 應用程式 toohello 整合帳戶連結](../logic-apps/logic-apps-enterprise-integration-accounts.md "toolink 整合帳戶 tooa 邏輯應用程式了解")具有要用於驗證 XML 資料 toouse hello 結構描述。

2. 新增**要求-當 HTTP 要求**觸發程序 tooyour 邏輯應用程式。

    ![](./media/logic-apps-enterprise-integration-xml/xml-1.png)

3. tooadd hello **XML 驗證**動作中，選擇**將動作加入**。

4. 輸入所有 hello，其中一個動作 toohello toofilter *xml* hello [搜尋] 方塊中。 選擇 [XML 驗證]。

    ![](./media/logic-apps-enterprise-integration-xml/xml-2.png)

5. 選取您想要 toovalidate 的 XML 內容的 toospecify hello**內容**。

    ![](./media/logic-apps-enterprise-integration-xml/xml-1-5.png)

6. 選取要作為內容的 toovalidate hello hello body 標記。

    ![](./media/logic-apps-enterprise-integration-xml/xml-3.png)

7. toospecify hello 結構描述要用於驗證先前 hello toouse*內容*輸入中，選擇 **結構描述名稱**。

    ![](./media/logic-apps-enterprise-integration-xml/xml-4.png)

8. 儲存您的工作   

    ![](./media/logic-apps-enterprise-integration-xml/xml-5.png)

現在您已完成設定驗證連接器。 在真實世界應用程式中，您可能想 toostore hello 驗證資料中的特定業務 (LOB) 應用程式，例如 SalesForce。 toosend hello 驗證的輸出 tooSalesforce，加入的動作。

tootest 您驗證的動作，讓要求 toohello HTTP 端點。

## <a name="next-steps"></a>後續步驟
[深入了解 hello Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md "深入了解 Enterprise Integration Pack")   

