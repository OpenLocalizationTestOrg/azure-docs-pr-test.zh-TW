---
title: "aaaCreate 及管理在 hello Azure 入口網站中的動作群組 |Microsoft 文件"
description: "深入了解如何 toocreate 及管理在 hello Azure 入口網站中的動作群組。"
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: ancav
ms.openlocfilehash: 97e0b22bea7787fff6856f895a7e6256c177efd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-action-groups-in-hello-azure-portal"></a>建立及管理在 hello Azure 入口網站中的動作群組
## <a name="overview"></a>概觀 ##
本文章將示範如何 toocreate 及管理在 hello Azure 入口網站中的動作群組。

您可以設定包含動作群組的動作清單。 接著，當您定義活動記錄警示時，可以使用這些群組。 這些群組則是每個活動記錄警示定義，請確保該 hello 會執行相同動作每次觸發 hello 活動記錄警示時重複使用。

動作群組可以有向上 too10 的每個動作類型。 每個動作所組成的 hello 下列屬性：

* **名稱**: hello 動作群組內的唯一識別碼。  
* **動作類型**：傳送 SMS、傳送電子郵件或呼叫 Webhook。  
* **詳細資料**: hello 相對應的電話號碼、 電子郵件地址或 webhook URI。

如需詳細資訊 toouse Azure Resource Manager 範本 tooconfigure 動作群組，請參閱[動作群組的資源管理員範本](monitoring-create-action-group-with-resource-manager-template.md)。

## <a name="create-an-action-group-by-using-hello-azure-portal"></a>使用 hello Azure 入口網站建立的動作群組 ##
1. 在 hello[入口網站](https://portal.azure.com)，選取**監視器**。 hello**監視器**刀鋒視窗中將合併所有將監視設定和資料在一個檢視中的。

    ![hello 「 監視 」 服務](./media/monitoring-action-groups/home-monitor.png)
2. 在 hello**活動記錄檔**區段中，選取**動作群組**。

    ![hello 「 動作群組 」 索引標籤](./media/monitoring-action-groups/action-groups-blade.png)
3. 選取**加入動作群組**，並填入 hello 欄位中。

    ![hello 「 新增動作群組 」 命令](./media/monitoring-action-groups/add-action-group.png)
4. 輸入的名稱在 hello**動作群組名稱**，然後輸入的名稱在 hello**簡短名稱**方塊。 hello 簡短名稱是在使用這個群組會傳送通知時，使用完整的動作群組名稱取代。

      ![hello 新增動作群組 對話方塊](./media/monitoring-action-groups/action-group-define.png)

5. hello**訂用帳戶**方塊 autofills 與您目前的訂用帳戶。 此訂用帳戶中儲存的 hello 動作群組是 hello 其中一個。

6. 選取 hello**資源群組**hello 動作在儲存群組。

7. 針對每個動作提供下列資訊，來定義動作的清單：

    a. **名稱**：輸入此動作的唯一識別碼。

    b. **動作類型**：選取 SMS、電子郵件或 Webhook。

    c. **詳細資料**： 根據 hello 動作類型，輸入電話號碼、 電子郵件地址或 webhook URI。

8. 選取**確定**toocreate hello 動作群組。

## <a name="manage-your-action-groups"></a>管理您的動作群組 ##
建立動作群組之後，會顯示在 hello**動作群組**區段 hello**監視器**刀鋒視窗。 選取您想要 toomanage hello 動作群組：

* 新增、編輯或移除動作。
* 刪除 hello 動作群組。

## <a name="next-steps"></a>後續步驟 ##
* 進一步了解 [SMS 警示行為](monitoring-sms-alert-behavior.md)。  
* 取得[hello 活動記錄警示 webhook 結構描述的了解](monitoring-activity-log-alerts-webhook.md)。  
* 深入了解警示的[速率限制](monitoring-alerts-rate-limiting.md)。 
* 取得[活動記錄檔警示概觀](monitoring-overview-alerts.md)，並了解如何 tooreceive 警示。  
* 了解如何太[設定警示，每當張貼服務健康情況通知](monitoring-activity-log-alerts-on-service-notifications.md)。
