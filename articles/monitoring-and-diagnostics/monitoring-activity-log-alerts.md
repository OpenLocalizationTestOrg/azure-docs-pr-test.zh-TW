---
title: "aaaCreate 活動記錄檔警示 |Microsoft 文件"
description: "可透過 SMS、 webhook，與電子郵件通知，hello 活動記錄檔中發生特定事件時。"
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
ms.date: 08/03/2017
ms.author: johnkem
ms.openlocfilehash: ba0716cc12a0b3a0024ee5562a025f3f153f8982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts"></a>建立活動記錄警示

## <a name="overview"></a>概觀
活動記錄檔的警示會啟動新的活動記錄事件發生時的警示符合 hello hello 警示中指定的條件。 它們是 Azure 資源，因此可以使用 Azure Resource Manager 範本來加以建立。 它們也可以建立、 更新，或在 hello Azure 入口網站中刪除。 本文介紹 hello 概念活動記錄檔的警示。 接著會說明如何 toouse hello Azure 入口網站的 tooset 向上活動記錄檔事件的警示。

通常您會建立活動記錄檔警示 tooreceive 通知時：

* 在您的 Azure 訂用帳戶、 通常已設定領域的 tooparticular 資源群組或資源的資源上發生特定變更。 例如，您可能想 toobe 刪除 myProductionResourceGroup 中任何虛擬機器時收到通知。 或者，您可能會想 toobe 如果任何新的角色指派給您的訂用帳戶中的 tooa 使用者收到通知。
* 隨即發生服務健康情況事件。 服務健全狀況事件包括事件和套用 tooresources 您訂用帳戶中的維護事件的通知。

在任一情況下，活動記錄檔警示監視僅適用於在 hello 訂用帳戶中的 hello 建立警示的事件。

您可以設定活動記錄檔警示 hello 活動記錄檔事件的 JSON 物件中任何最上層屬性為基礎。 不過，hello 入口網站會顯示 hello 最常用的選項：

- **類別**：系統管理、服務健康狀態、自動調整規模及建議。 如需詳細資訊，請參閱[hello Azure 活動記錄檔的概觀](./monitoring-overview-activity-logs.md#categories-in-the-activity-log)。 toolearn 進一步了解服務健全狀況事件，請參閱[接收服務通知上的活動記錄檔警示](./monitoring-activity-log-alerts-on-service-notifications.md)。
- **資源群組**
- **Resource**
- **資源類型**
- **作業名稱**: hello 資源管理員角色型存取控制作業名稱。
- **層級**: hello （詳細資訊、 資訊、 警告、 錯誤或重大） hello 事件嚴重性層級。
- **狀態**: hello 的 hello 事件，通常啟動、 失敗或成功的狀態。
- **由事件初始化**： 也稱為 hello 「 呼叫者。 」 hello 電子郵件地址或 Azure Active Directory 作業 hello hello 使用者識別碼。

>[!NOTE]
>您必須指定至少兩個準則中警示，具有一個在前面的 hello hello 類別。 您可能無法建立警示，每次 hello 活動記錄檔中建立事件時，就會啟動。
>
>

啟動 活動記錄警示時，它會使用動作群組 toogenerate 動作或通知。 動作群組是一組可重複使用的通知接收者，例如電子郵件地址、Webhook URL 或 SMS 電話號碼。 hello 接收者可以從多個警示 toocentralize 參考，並分組通知通道。 當您定義活動記錄警示時，會有兩個選項。 您可以：

* 在您的活動記錄警示中使用現有的動作群組。 
* 建立新的動作群組。 

toolearn 進一步了解動作群組，請參閱[建立及管理在 hello Azure 入口網站中的動作群組](monitoring-action-groups.md)。

toolearn 進一步了解服務健全狀況通知，請參閱[接收服務健全狀況通知上的活動記錄檔警示](monitoring-activity-log-alerts-on-service-notifications.md)。

## <a name="create-an-alert-on-an-activity-log-event-with-a-new-action-group-by-using-hello-azure-portal"></a>使用 hello Azure 入口網站建立與新的動作群組的活動記錄檔事件的警示
1. 在 hello[入口網站](https://portal.azure.com)，選取**監視器**。

    ![hello 「 監視 」 服務](./media/monitoring-activity-log-alerts/home-monitor.png)
2. 在 hello**活動記錄檔**區段中，選取**警示**。

    ![hello [警示] 索引標籤](./media/monitoring-activity-log-alerts/alerts-blades.png)
3. 選取**新增活動記錄檔警示**，並填入 hello 欄位中。

4. 輸入的名稱在 hello**活動記錄檔的警示名稱**方塊，然後選取**描述**。

    ![hello 「 新增活動記錄警示 」 命令](./media/monitoring-activity-log-alerts/add-activity-log-alert.png)

5. hello**訂用帳戶**方塊 autofills 與您目前的訂用帳戶。 此訂用帳戶中儲存的 hello 動作群組是 hello 其中一個。 hello 警示的資源是從它的已部署的 toothis 訂用帳戶和監視活動記錄事件。

    ![[新增活動記錄警示] 對話方塊中的 hello](./media/monitoring-activity-log-alerts/activity-log-alert-new-action-group.png)

6. 選取 hello**資源群組**哪些 hello 中建立警示的資源。 這不由 hello 警示所監視的 hello 資源群組。 相反地，它是 hello hello 警示資源所在的資源群組。

7. （選擇性） 選取**事件類別目錄**toomodify hello 所顯示的其他篩選。 對於系統管理事件，包括 hello 篩選**資源群組**，**資源**，**資源類型**，**作業名稱**， **層級**，**狀態**，和**由事件初始化**。 這些值會識別此警示應該監視的事件。

    >[!NOTE]
    >您必須指定至少一個在您的警示之前準則 hello。 您可能無法建立警示，每次 hello 活動記錄檔中建立事件時，就會啟動。
    >
    >

8. 輸入的名稱在 hello**動作群組名稱**，然後輸入的名稱在 hello**簡短名稱**方塊。 hello 簡短名稱是在使用這個群組會傳送通知時，使用完整的動作群組名稱取代。

9.  藉由提供 hello 動作定義動作的清單：

    a. **名稱**： 輸入 hello 動作名稱、 別名或識別項。

    b. **動作類型**：選取 SMS、電子郵件或 Webhook。

    c. **詳細資料**： 根據 hello 動作類型，輸入電話號碼、 電子郵件地址或 webhook URI。

10. 選取**確定**toocreate hello 警示。

hello 警示需要幾分鐘的時間 toofully 傳播，並再變成 作用中。 它時，會觸發新的事件符合 hello 警示的準則。

如需詳細資訊，請參閱[活動記錄檔警示中使用的了解 hello webhook 結構描述](monitoring-activity-log-alerts-webhook.md)。

>[!NOTE]
>這些步驟中所定義的 hello 動作群組是可重複使用與現有的動作群組的所有未來的警示定義。
>
>

## <a name="create-an-alert-on-an-activity-log-event-for-an-existing-action-group-by-using-hello-azure-portal"></a>建立使用 hello Azure 入口網站為現有的動作群組的活動記錄檔事件的警示
1. 請遵循步驟 1 到 7 中前一個區段 toocreate hello 活動記錄警示。

2. 在下**透過通知**，選取 hello**現有**動作群組 按鈕。 Hello 清單中選取現有的動作群組。

3. 選取**確定**toocreate hello 警示。

hello 警示需要幾分鐘的時間 toofully 傳播，並再變成 作用中。 它時，會觸發新的事件符合 hello 警示的準則。

## <a name="manage-your-alerts"></a>管理警示

建立警示之後，它會顯示在 hello hello 監視器] 刀鋒視窗的 [警示 > 一節。 選取您想要的 toomanage 的 hello 警示：

* 進行編輯。
* 進行刪除。
* 停用或啟用它，如果您想要 tootemporarily 停止或繼續收到 hello 警示的通知。

## <a name="next-steps"></a>後續步驟
- 取得[警示概觀](monitoring-overview-alerts.md)。
- 深入了解[通知速率限制](monitoring-alerts-rate-limiting.md)。
- 檢閱 hello[活動記錄警示 webhook 結構描述](monitoring-activity-log-alerts-webhook.md)。
- 深入了解[動作群組](monitoring-action-groups.md)。  
- 深入了解[服務健康狀態通知](monitoring-service-notifications.md)。
- 建立[活動記錄警示 toomonitor 所有訂用帳戶的自動調整引擎作業](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)。
- 建立[活動記錄警示 toomonitor 訂用帳戶的所有失敗的自動調整規模輸入/向外作業](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)。
