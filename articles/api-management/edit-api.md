---
title: "透過 Azure 入口網站編輯 API | Microsoft Docs"
description: "本教學課程會示範如何使用 API 管理 (APIM) 來編輯 API。"
services: api-management
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 11/08/2017
ms.author: apimpm
ms.openlocfilehash: 362c36181da706e3fe0a27cc5ab262271c2a1e57
ms.sourcegitcommit: b854df4fc66c73ba1dd141740a2b348de3e1e028
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/04/2017
---
# <a name="edit-an-api"></a>編輯 API

本教學課程中的步驟會示範如何使用 API 管理 (APIM) 來編輯 API。 

+ 您可以透過新增、刪除或重新命名 APIM 執行個體中的作業來執行此動作。 
+ 您可以編輯您 API 的 Swagger。

## <a name="prerequisites"></a>必要條件

+ [建立 Azure API 管理執行個體](get-started-create-service-instance.md)
+ [匯入和發佈您的第一個 API](import-and-publish.md)

[!INCLUDE [api-management-navigate-to-instance.md](../../includes/api-management-navigate-to-instance.md)]

## <a name="edit-an-api-in-apim"></a>在 APIM 中編輯 API

![編輯 API](./media/edit-api/edit-api001.png)

1. 按一下 [API] 索引標籤。
2. 選取其中一個您先前匯入的 API。
3. 選取 [設計] 索引標籤。
4. 選取您想要編輯的作業。
5. 若要重新命名作業，請選取 [前端]視窗中的**鉛筆**。

## <a name="update-the-swagger"></a>更新 Swagger

若要從 Azure 入口網站更新您的後端 API，您可以遵循下列步驟：

1. 選取 [所有作業]
2. 按一下 [前端] 視窗中的鉛筆。

    ![編輯 API](./media/edit-api/edit-api002.png)

    您 API 的 Swagger 會隨即出現。

    ![編輯 API](./media/edit-api/edit-api003.png)

3. 更新 Swagger。
4. 按下 [儲存] 。

[!INCLUDE [api-management-define-api-topics.md](../../includes/api-management-define-api-topics.md)]

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [APIM 原則範例](policy-samples.md)
> [轉換及保護已發佈的 API](transform-api.md)