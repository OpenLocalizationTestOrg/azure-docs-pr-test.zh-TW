---
title: "aaaCreate、 連結、 刪除或移動 Azure 邏輯應用程式中整合帳戶 |Microsoft 文件"
description: "如何整合 toocreate 帳戶，並將其連結 tooyour 邏輯應用程式"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: d3ad9e99-a9ee-477b-81bf-0881e11e632f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: LADocs; mandia
ms.openlocfilehash: fda6c91723b3e3624ee176df112ba8b6c9800273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-an-integration-account"></a>什麼是整合帳戶？

整合帳戶可讓企業整合應用程式 toomanage 成品，包括結構描述、 對應、 憑證、 夥伴和協議。 您所建立的任何整合應用程式使用整合帳戶 tooaccess 這些結構描述、 對應、 憑證等等。

## <a name="create-an-integration-account"></a>建立整合帳戶

1.  登入 toohello [Azure 入口網站](http://portal.azure.com "Azure 入口網站")。 從 hello 左窗格中，選取**更多服務**。

    ![選取 [更多服務]。](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. 在 hello 搜尋方塊中，輸入 「 整合 」 篩選條件。 在 hello 結果清單中，選取 **整合帳戶**。

    ![依據 [整合] 篩選，選取 [整合帳戶]](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. 在 hello hello 頁面頂端，選擇**新增**。

    ![選擇 [新增]](./media/logic-apps-enterprise-integration-accounts/account-3.png)

4. 命名您的整合帳戶和選取 hello 想 toouse 的 Azure 訂用帳戶。 您可以建立新的 [資源群組]，或選取現有的資源群組。 然後選取 [位置] 以便裝載整合帳戶和 [定價層]。 

    準備就緒時，請選擇 [建立]。

    ![提供整合帳戶的詳細資料](./media/logic-apps-enterprise-integration-accounts/account-4.png)

    Azure 會佈建您的整合帳戶在選取的 hello 的位置，應該在 1 分鐘內完成。

5. 重新整理 hello 頁面。 您會看到已列出新的整合帳戶。

    ![您的新整合帳戶隨即出現](./media/logic-apps-enterprise-integration-accounts/account-5.png) 

接下來，hello 整合帳戶，您建立的 tooyour 邏輯應用程式連結。 

## <a name="link-an-integration-account-tooa-logic-app"></a>連結整合帳戶 tooa 邏輯應用程式

toogive toomaps、 結構描述、 合約和其他成品，整合帳戶，連結 hello 整合帳戶 tooyour 邏輯應用程式中的，存取您的 logic apps。

### <a name="prerequisites"></a>必要條件

* 整合帳戶
* 邏輯應用程式

> [!NOTE] 
> 請確定應用程式整合帳戶和邏輯位於 hello*相同的 Azure 位置*開始之前。


1. 在 hello Azure 入口網站，選取應用程式邏輯，並檢查邏輯應用程式的位置。

    ![選取邏輯應用程式，檢查位置](./media/logic-apps-enterprise-integration-accounts/linkaccount-1.png)

2. 在 [設定] 之下，選取 [整合帳戶]。

    ![選取 [整合帳戶]](./media/logic-apps-enterprise-integration-accounts/linkaccount-2.png)

3. 從 hello**選取整合帳戶**清單，選取 hello 整合帳戶想 toolink tooyour 邏輯應用程式。 toofinish 連結中，選擇**儲存**。

    ![選取您的整合帳戶](./media/logic-apps-enterprise-integration-accounts/linkaccount-3.png)

    您會得到通知帳戶是連結的 tooyour 邏輯應用程式，且整合帳戶中的所有成品都都可以立即可用 tooyour 邏輯應用程式顯示您的整合。

    ![邏輯應用程式連結 tooyour 整合帳戶](./media/logic-apps-enterprise-integration-accounts/linkaccount-5.png)

現在已整合帳戶連結的 tooyour 邏輯應用程式，您可以使用邏輯應用程式中的 hello B2B 連接器。 部分常見的 B2B 連接器包括 XML 驗證和一般檔案編碼/解碼。  

## <a name="delete-your-integration-account"></a>刪除您的整合帳戶

1. 選取 [更多服務]。

    ![選取 [更多服務]。](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. 在 hello 搜尋方塊中，輸入 「 整合 」 篩選條件。 在 hello 結果清單中，選取 **整合帳戶**。

    ![依據 [整合] 篩選，選取 [整合帳戶]](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. 選取您想 toodelete hello 整合帳戶。

    ![選取整合帳戶 toodelete](./media/logic-apps-enterprise-integration-accounts/account-5.png)

4. 在 hello 功能表上選擇 **刪除**。

    ![選擇 [刪除]](./media/logic-apps-enterprise-integration-accounts/delete.png)

5. 確認您的選擇 toodelete hello 整合帳戶。

## <a name="move-your-integration-account"></a>移動您的整合帳戶

toomove 整合帳戶 tooanother Azure 的訂用帳戶或資源群組，請遵循下列步驟。

> [!IMPORTANT]
> 在您移動整合帳戶之後，您必須更新所有指令碼 toouse hello 新的資源 Id。

1. 選取 [更多服務]。

    ![選取 [更多服務]。](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. 在 hello 搜尋方塊中，輸入 「 整合 」 篩選條件。 在 hello 結果清單中，選取 **整合帳戶**。

    ![依據 [整合] 篩選，選取 [整合帳戶]](./media/logic-apps-enterprise-integration-accounts/account-2.png)

3. 選取您想 toomove hello 整合帳戶。 在 [設定] 之下選擇 [屬性]。

    ![選取整合帳戶 toomove。 在 [設定] 之下選擇 [屬性]](./media/logic-apps-enterprise-integration-accounts/move.png)

5. 變更 hello 資源群組或與整合帳戶相關聯的 Azure 訂用帳戶。

    ![選擇 [變更資源群組] 或 [變更訂用帳戶]](./media/logic-apps-enterprise-integration-accounts/move-2.png)

## <a name="next-steps"></a>後續步驟
* [深入了解合約](../logic-apps/logic-apps-enterprise-integration-agreements.md "了解企業整合合約")  

