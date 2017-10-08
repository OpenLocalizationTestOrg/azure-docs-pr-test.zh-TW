---
title: "XML 驗證-Azure 邏輯應用程式的 aaaSchemas |Microsoft 文件"
description: "使用適用於 Azure Logic Apps 與企業整合套件的結構描述來驗證 XML 文件"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 56c5846c-5d8c-4ad4-9652-60b07aa8fc3b
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 87cf92741e10ff7cccd260f27442909e34928903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-with-schemas-for-azure-logic-apps-and-hello-enterprise-integration-pack"></a>使用結構描述驗證 XML，為 Azure 邏輯應用程式與 hello 企業版整合套件

結構描述確認收到 hello XML 文件都有效，而且有 hello 預期的資料中預先定義的格式。 結構描述也可用來驗證在 B2B 案例中交換的訊息。

## <a name="add-a-schema"></a>新增結構描述

1. 在 hello Azure 入口網站，選取 **更多服務**。

    ![Azure 入口網站，[更多服務]](media/logic-apps-enterprise-integration-schemas/overview-11.png)

2. 在 hello 篩選搜尋方塊中，輸入**整合**，然後選取**整合帳戶**hello 結果清單中。

    ![篩選搜尋方塊](media/logic-apps-enterprise-integration-schemas/overview-21.png)

3. 選取 hello**整合帳戶**想 tooadd hello 結構描述。

    ![整合帳戶清單](media/logic-apps-enterprise-integration-schemas/overview-31.png)

4. 選擇 hello**結構描述**磚。

    ![範例整合帳戶 "Schemas"](media/logic-apps-enterprise-integration-schemas/schema-11.png)

### <a name="add-a-schema-file-smaller-than-2-mb"></a>新增小於 2 MB 的結構描述檔案

1. 在 hello**結構描述**刀鋒視窗中開啟 （從 hello 先前步驟)，選擇**新增**。

    ![[結構描述] 刀鋒視窗，[新增]](media/logic-apps-enterprise-integration-schemas/schema-21.png)

2. 輸入結構描述名稱。 Hello 結構描述檔案上傳選取 hello 資料夾圖示的 下一步 toohello**結構描述**方塊。 Hello 上傳程序完成之後，請選取**確定**。

    ![[新增結構描述] 的螢幕擷取畫面，反白顯示了 [小型檔案]](media/logic-apps-enterprise-integration-schemas/schema-31.png)

### <a name="add-a-schema-file-larger-than-2-mb-up-too8-mb-maximum"></a>加入結構描述檔案超過 2 MB （向上 too8 MB 最大值）

這些步驟會有所不同 hello blob 容器的存取層級：**公用**或**沒有匿名存取**。

**toodetermine 此存取層級**

1.  開啟 [Azure 儲存體總管]。 

2.  在下**Blob 容器**，選取您想要的 hello blob 容器。 

3.  選取 [安全性]、[存取層級]。

如果 hello blob 安全性存取層級為**公用**，請遵循下列步驟。

![Azure 儲存體總管，已反白選取 [Blob 容器]、[安全性] 與 [公開]](media/logic-apps-enterprise-integration-schemas/blob-public.png)

1. 上傳 hello 結構描述 tooyour 儲存體帳戶，並複製 hello URI。

    ![儲存體帳戶，已反白顯示 URI](media/logic-apps-enterprise-integration-schemas/schema-blob.png)

2. 在**新增結構描述**，選取**大型檔案**，並提供在 hello hello URI**內容 URI**文字方塊。

    ![[結構描述]，已反白顯示 [新增] 按鈕和 [大型檔案]](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

如果 hello blob 安全性存取層級為**沒有匿名存取**，請遵循下列步驟。

![Azure 儲存體總管，已反白顯示 [Blob 容器]、[安全性] 和 [無匿名存取]](media/logic-apps-enterprise-integration-schemas/blob-1.png)

1. 上傳 hello 結構描述 tooyour 儲存體帳戶。

    ![儲存體帳戶](media/logic-apps-enterprise-integration-schemas/blob-3.png)

2. 產生 hello 結構描述的共用的存取簽章。

    ![儲存體帳戶，已反白顯示 [共用存取簽章] 索引標籤](media/logic-apps-enterprise-integration-schemas/blob-2.png)

3. 在**新增結構描述**，選取**大型檔案**，並提供在 hello hello 共用的存取簽章 URI**內容 URI**文字方塊。

    ![[結構描述]，已反白顯示 [新增] 按鈕和 [大型檔案]](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

4. 在 hello**結構描述**刀鋒視窗中的整合帳戶，您新增的結構描述應該會出現。

    ![您的 「 結構描述 」 和 hello 反白顯示的新結構描述的整合帳戶](media/logic-apps-enterprise-integration-schemas/schema-41.png)

## <a name="edit-schemas"></a>編輯結構描述

1. 選擇 hello**結構描述**磚。

2. 之後 hello**結構描述**刀鋒視窗隨即開啟，您想 tooedit 選取 hello 結構描述。

3. 在 hello**結構描述**刀鋒視窗中，選擇**編輯**。

    ![[結構描述] 刀鋒視窗](media/logic-apps-enterprise-integration-schemas/edit-12.png)

4. 您想 tooedit，然後選取 選取 hello 結構描述檔案**開啟**。

    ![開啟結構描述檔案 tooedit](media/logic-apps-enterprise-integration-schemas/edit-31.png)

已成功上傳 azure 便會顯示訊息的 hello 結構描述。

## <a name="delete-schemas"></a>刪除結構描述

1. 選擇 hello**結構描述**磚。

2. 之後 hello**結構描述**刀鋒視窗隨即開啟，您想要 toodelete 選取 hello 結構描述。

3. 在 hello**結構描述**刀鋒視窗中，選擇**刪除**。

    ![[結構描述] 刀鋒視窗](media/logic-apps-enterprise-integration-schemas/delete-12.png)

4. 您想 toodelete hello tooconfirm 選取的結構描述中，選擇 **是**。

    ![[刪除結構描述] 確認訊息](media/logic-apps-enterprise-integration-schemas/delete-21.png)

    在 hello**結構描述**刀鋒視窗中，重新整理 hello 結構描述清單中，不再包含您所刪除的 hello 結構描述。

    ![您的整合帳戶，已反白顯示 [結構描述]](media/logic-apps-enterprise-integration-schemas/delete-31.png)

## <a name="next-steps"></a>後續步驟
* [深入了解 hello Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "深入了解 hello 企業版整合套件")。  

