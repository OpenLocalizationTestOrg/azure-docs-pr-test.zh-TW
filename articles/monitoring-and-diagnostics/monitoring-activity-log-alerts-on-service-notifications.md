---
title: "在服務通知 aaaReceive 活動記錄檔警示 |Microsoft 文件"
description: "在 Azure 服務發生時透過 SMS、電子郵件或 Webhook 獲得通知。"
author: johnkemnetz
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
ms.date: 03/31/2017
ms.author: johnkem
ms.openlocfilehash: dd35e8f39d2a522efdae4dfed20779c992c1dd27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts-on-service-notifications"></a>建立服務通知的活動記錄警示
## <a name="overview"></a>概觀
本文將說明您的服務健全狀況通知 tooset 活動記錄警示 hello Azure 入口網站的使用方式。  

您可以收到通知時，Azure 都會傳送服務健全狀況通知 tooyour Azure 訂用帳戶。 您可以設定為基礎的 hello 警示：

- hello 類別的服務健全狀況通知 （事件、 維護、 資訊等等）。
- 受影響的 hello 服務。
- 受影響的 hello 到區域。
- hello hello 通知 （使用中和已解決的比較） 狀態。
- hello 層級的 hello 通知 （資訊、 警告、 錯誤）。

您也可以設定 hello 警示應收件者：

- 選取現有的動作群組。
- 建立新動作群組 (可用於未來的警示)。

toolearn 進一步了解動作群組，請參閱[建立及管理群組動作](monitoring-action-groups.md)。

如需如何 tooconfigure 服務健全狀況通知警示使用的 Azure Resource Manager 範本資訊，請參閱[資源管理員範本](monitoring-create-activity-log-alerts-with-resource-manager-template.md)。

## <a name="create-an-alert-on-a-service-health-notification-for-a-new-action-group-by-using-hello-azure-portal"></a>使用 hello Azure 入口網站建立新的動作群組的服務健全狀況通知警示
1. 在 hello[入口網站](https://portal.azure.com)，選取**監視器**。

    ![hello 「 監視 」 服務](./media/monitoring-activity-log-alerts-on-service-notifications/home-monitor.png)

2. 在 hello**活動記錄檔**區段中，選取**警示**。

    ![hello [警示] 索引標籤](./media/monitoring-activity-log-alerts-on-service-notifications/alerts-blades.png)

3. 選取**新增活動記錄檔警示**，並填入 hello 欄位中。

    ![hello 「 新增活動記錄警示 」 命令](./media/monitoring-activity-log-alerts-on-service-notifications/add-activity-log-alert.png)

4. 輸入的名稱在 hello**活動記錄檔的警示名稱**方塊，並提供**描述**。

    ![[新增活動記錄警示] 對話方塊中的 hello](./media/monitoring-activity-log-alerts-on-service-notifications/activity-log-alert-service-notification-new-action-group.png)

5. hello**訂用帳戶**方塊 autofills 與您目前的訂用帳戶。 此訂用帳戶是使用的 toosave hello 活動記錄警示。 hello 警示的資源是為它的 hello 活動記錄檔中的已部署的 toothis 訂用帳戶和監視事件。

6. 選取 hello**資源群組**哪些 hello 中建立警示的資源。 這不由 hello 警示所監視的 hello 資源群組。 相反地，它是 hello hello 警示資源所在的資源群組。

7. 在 hello**事件類別目錄**方塊中，選取**服務健全狀況**。 （選擇性） 選取 hello**服務**，**區域**，**類型**，**狀態**，和**層級**的服務您想 tooreceive 健康情況通知。

8. 在下**透過警示**，選取 hello**新增**動作群組 按鈕。 輸入的名稱在 hello**動作群組名稱**，然後輸入的名稱在 hello**簡短名稱**方塊。 hello 簡短名稱參考時都會引發這個警示所傳送嗨通知中。

9. 藉由提供 hello 接收器中定義接收者的清單：

    a. **名稱**： 輸入 hello 接收器的名稱、 別名或識別項。

    b. **動作類型**：選取 SMS、電子郵件或 Webhook。

    c. **詳細資料**： 根據選擇的 hello 動作類型，輸入電話號碼、 電子郵件地址或 webhook URI。

10. 選取**確定**toocreate hello 警示。

在幾分鐘的時間內 hello 警示為作用中，並且開始 tootrigger 根據您在建立期間指定的 hello 條件。

如需活動記錄檔警示 hello webhook 結構描述資訊，請參閱[Webhook Azure 活動記錄警示](monitoring-activity-log-alerts-webhook.md)。

>[!NOTE]
>這些步驟中所定義的 hello 動作群組是可重複使用與現有的動作群組的所有未來的警示定義。
>
>

## <a name="create-an-alert-on-a-service-health-notification-for-an-existing-action-group-by-using-hello-azure-portal"></a>建立現有的動作群組的服務健全狀況通知警示使用 hello Azure 入口網站

1. 請遵循步驟 1 到 7 中前一個區段 toocreate hello 您服務的健全狀況通知。 

2. 在下**透過警示**，選取 hello**現有**動作群組 按鈕。 選取 hello 適當的動作群組。

3. 選取**確定**toocreate hello 警示。

在幾分鐘的時間內 hello 警示為作用中，並且開始 tootrigger 根據您在建立期間指定的 hello 條件。

## <a name="manage-your-alerts"></a>管理警示

建立警示之後，會顯示在 hello**警示**區段 hello**監視器**刀鋒視窗。 選取您想要的 toomanage 的 hello 警示：

* 進行編輯。
* 進行刪除。
* 停用或啟用它，如果您想要 tootemporarily 停止或繼續收到 hello 警示的通知。

## <a name="next-steps"></a>後續步驟
- 深入了解[服務健康狀態通知](monitoring-service-notifications.md)。
- 深入了解[通知速率限制](monitoring-alerts-rate-limiting.md)。
- 檢閱 hello[活動記錄警示 webhook 結構描述](monitoring-activity-log-alerts-webhook.md)。
- 取得[活動記錄檔警示概觀](monitoring-overview-alerts.md)，並了解如何 tooreceive 警示。 
- 深入了解[動作群組](monitoring-action-groups.md)。
