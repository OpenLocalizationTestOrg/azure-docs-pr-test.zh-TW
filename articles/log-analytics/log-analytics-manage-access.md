---
title: "aaaManage Azure 記錄分析和 hello OMS 入口網站中的工作區 |Microsoft 文件"
description: "您可以管理使用者、 帳戶、 工作區，以及 Azure 帳戶上使用的各種系統管理工作的 Azure 記錄分析和 hello OMS 入口網站中的工作區。"
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: d0e5162d-584b-428c-8e8b-4dcaa746e783
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/06/2017
ms.author: magoedte
ms.openlocfilehash: 570e6c1f13ad28f120ecd65052d00c4ca986ac98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-workspaces"></a>管理工作區

toomanage 存取 tooLog 分析，您可以執行各種管理工作相關的 tooworkspaces。 本文章提供最佳作法建議和程序 toomanage 工作區。 工作區本質上是容器，包含帳戶資訊和 hello 帳戶的簡單組態資訊。 您或您組織的其他成員可能會使用多個工作區 toomanage 不同的資料集所收集從所有或部分 IT 基礎結構。

toocreate 工作區，您要：

1. 擁有 Azure 訂用帳戶。
2. 選擇工作區名稱。
3. 將 hello 工作區與您訂用帳戶產生關聯。
4. 選擇地理位置。

## <a name="determine-hello-number-of-workspaces-you-need"></a>判斷您需要工作區的 hello 的數目
工作區是一項 Azure 資源，其中資料收集、 彙總、 分析和呈現 hello Azure 入口網站中的容器。

您可以有多個工作區，每個 Azure 訂閱，您可以存取 toomore 比一個工作區。 可讓您 tooquery 及跨 hello 大部分讓資料相互關聯，因為它是不可能 tooquery 跨多個工作區的工作區的降至最低 hello 數目。 本章節描述當可能很有幫助 toocreate 多個工作區。

現今的工作區可提供︰

* 資料儲存體的地理位置
* 計費的細微度
* 資料隔離
* 設定範圍

根據上述特徵的 hello，您可能想 toocreate 多個工作區如果：

* 您是一家全球性公司，基於資料主權或合規性理由，您需要將資料儲存在特定區域。
* 您使用 Azure，而您想 tooavoid 傳出資料傳輸費用，讓工作區 hello 相同的區域，因為 hello 其所管理的 Azure 資源。
* 您想 tooallocate 費用 toodifferent 部門或根據其使用量的商務群組。 當您建立的每個部門或商務群組工作區時，Azure 帳單和使用量陳述式分別顯示每個工作區的 hello 費用。
* 您的受管理的服務提供者並為您管理每個客戶，與其他客戶的資料隔離需要 tookeep hello 記錄分析資料。
* 管理多個客戶，而且您想每個客戶 / 部門 / 商務群組 toosee 他們自己的資料，但不是 hello 資料供其他人。

當使用代理程式 toocollect 資料，您可以[設定每個代理程式 tooreport tooone 或多個工作區](log-analytics-windows-agents.md)。

如果您使用 System Center Operations Manager，每個 Operations Manager 管理群組只能連接一個工作區。 您可以在 Operations Manager 所管理的電腦上安裝 Microsoft Monitoring Agent hello 並且 hello 代理程式報告 tooboth Operations Manager 和不同的記錄分析工作區。

### <a name="workspace-information"></a>工作區資訊

您可以在 hello Azure 入口網站中您工作區的相關檢視詳細資料。 您也可以在 hello OMS 入口網站中檢視詳細資料。

#### <a name="view-workspace-information-in-hello-azure-portal"></a>Hello Azure 入口網站中檢視工作區資訊

1. 如果您尚未這樣做，請登入 toohello [Azure 入口網站](https://portal.azure.com)使用您的 Azure 訂用帳戶。
2. 在 hello**中樞**功能表上，按一下 [**更多服務**hello] 清單中的資源，在輸入**記錄分析**。 當您開始輸入 hello 清單會篩選根據您的輸入。 按一下 [Log Analytics]。  
    ![Azure 中樞](./media/log-analytics-manage-access/hub.png)  
3. 在 hello 記錄分析訂閱刀鋒視窗中，選取工作區。
4. hello 工作區 刀鋒視窗會顯示詳細 hello 工作區和其他資訊的連結。  
    ![工作區詳細資料](./media/log-analytics-manage-access/workspace-details.png)  


## <a name="manage-accounts-and-users"></a>管理帳戶和使用者
每個工作區可以有多個帳戶相關聯，而每個帳戶 （Microsoft 帳戶或組織帳戶） 可以存取 toomultiple 工作區。

依預設，hello Microsoft 帳戶或組織帳戶，會建立 hello 工作區成為 hello hello 工作區的系統管理員。

有兩個控制存取 tooa 記錄分析工作區的權限模型：

1. 舊版 Log Analytics 使用者角色
2. [Azure 角色型存取](../active-directory/role-based-access-control-configure.md)

hello 下表摘要說明您可以將使用每個權限模型的 hello 存取：

|                          | Log Analytics 入口網站 | Azure 入口網站 | API (包括 PowerShell) |
|--------------------------|----------------------|--------------|----------------------------|
| Log Analytics 使用者角色 | 是                  | 否           | 否                         |
| Azure 角色型存取  | 是                  | 是          | 是                        |

> [!NOTE]
> 記錄分析移動 toouse Azure 以角色為基礎的存取為 hello 權限模型取代 hello 記錄分析使用者角色。
>
>

hello 舊版記錄分析使用者角色只能控制存取 tooactivities 執行 hello[記錄分析入口網站](https://mms.microsoft.com)。

hello 下列活動，也需要 Azure 權限：

| 動作                                                          | 所需的 Azure 權限 | 注意事項 |
|-----------------------------------------------------------------|--------------------------|-------|
| 新增及移除管理解決方案                        | `Microsoft.Resources/deployments/*` <br> `Microsoft.OperationalInsights/*` <br> `Microsoft.OperationsManagement/*` <br> `Microsoft.Automation/*` <br> `Microsoft.Resources/deployments/*/write` | |
| 變更定價層的 hello                                       | `Microsoft.OperationalInsights/workspaces/*/write` | |
| 檢視資料中 hello*備份*和*Site Recovery*解決方案磚 | 系統管理員/共同管理員 | 使用 hello 傳統部署模型部署存取資源 |
| 在 hello Azure 入口網站中建立工作區                        | `Microsoft.Resources/deployments/*` <br> `Microsoft.OperationalInsights/workspaces/*` ||


### <a name="managing-access-toolog-analytics-using-azure-permissions"></a>管理存取 tooLog 分析使用 Azure 的權限
toogrant 存取 toohello 記錄分析工作區中使用 Azure 的權限，請依照下列中的 hello 步驟[使用角色指派 toomanage 存取 tooyour Azure 訂用帳戶資源](../active-directory/role-based-access-control-configure.md)。

Azure 有兩個適用於 Log Analytics 的內建使用者角色：
- Log Analytics 讀者
- Log Analytics 參與者

成員的 hello*記錄分析的讀取器*角色可以：
- 檢視及搜尋所有監視資料 
- 檢視監視的設定，包括所有 Azure 資源上檢視 hello Azure 診斷的組態。

| 類型    | 權限 | 說明 |
| ------- | ---------- | ----------- |
| 動作 | `*/read`   | 能力 tooview 所有的資源和資源組態。 包括檢視： <br> 虛擬機器擴充功能 <br> 在資源上設定 Azure 診斷 <br> 所有資源的所有屬性和設定 |
| 動作 | `Microsoft.OperationalInsights/workspaces/analytics/query/action` | 能力 tooperform v2 記錄搜尋查詢 |
| 動作 | `Microsoft.OperationalInsights/workspaces/search/action` | 能力 tooperform v1 記錄搜尋查詢 |
| 動作 | `Microsoft.Support/*` | 能力 tooopen 的支援案例 |
|不是動作 | `Microsoft.OperationalInsights/workspaces/sharedKeys/read` | 防止讀取的工作區金鑰需要的 toouse hello 資料收集應用程式開發介面和 tooinstall 代理程式 |


成員的 hello*記錄分析參與者*角色可以：
- 讀取所有監視資料 
- 建立和設定自動化帳戶
- 新增及移除管理解決方案
- 讀取儲存體帳戶金鑰 
- 設定 Azure 儲存體的記錄集合
- 編輯 Azure 資源的監視設定，包括
  - 加入 hello VM 延伸模組 tooVMs
  - 在所有 Azure 資源上設定 Azure 診斷

> [!NOTE] 
> 您可以使用 hello 能力 tooadd 虛擬機器擴充功能 tooa 虛擬機器 toogain 完整控制容錯移轉虛擬機器。

| 權限 | 說明 |
| ---------- | ----------- |
| `*/read`     | 能力 tooview 所有的資源和資源組態。 包括檢視： <br> 虛擬機器擴充功能 <br> 在資源上設定 Azure 診斷 <br> 所有資源的所有屬性和設定 |
| `Microsoft.Automation/automationAccounts/*` | 能力 toocreate 及設定 Azure 自動化帳戶，包括加入和編輯 runbook |
| `Microsoft.ClassicCompute/virtualMachines/extensions/*` <br> `Microsoft.Compute/virtualMachines/extensions/*` | 加入、 更新及移除虛擬機器擴充功能，包括 hello Microsoft Monitoring Agent 擴充功能和 hello OMS Agent for Linux 擴充功能 |
| `Microsoft.ClassicStorage/storageAccounts/listKeys/action` <br> `Microsoft.Storage/storageAccounts/listKeys/action` | 檢視 hello 儲存體帳戶金鑰。 需要從 Azure 儲存體帳戶的 tooconfigure 記錄分析 tooread 記錄檔 |
| `Microsoft.Insights/alertRules/*` | 新增、更新和移除警示規則 |
| `Microsoft.Insights/diagnosticSettings/*` | 在 Azure 資源上新增、更新和移除診斷設定 |
| `Microsoft.OperationalInsights/*` | 新增、更新和移除 Log Analytics 工作區的組態 |
| `Microsoft.OperationsManagement/*` | 新增及移除管理解決方案 |
| `Microsoft.Resources/deployments/*` | 建立及刪除部署。 需具備此權限，才能新增及移除解決方案、工作區和自動化帳戶 |
| `Microsoft.Resources/subscriptions/resourcegroups/deployments/*` | 建立及刪除部署。 需具備此權限，才能新增及移除解決方案、工作區和自動化帳戶 |

tooadd] 和 [移除使用者 tooa 」 使用者角色，則需要 toohave`Microsoft.Authorization/*/Delete`和`Microsoft.Authorization/*/Write`權限。

在不同範圍中使用這些角色 toogive 使用者存取權：
- 訂閱-hello 訂用帳戶中存取 tooall 工作區
- 資源群組-hello 資源群組中的存取 tooall 工作區
- 資源的存取 tooonly hello 指定工作區

使用[自訂角色](../active-directory/role-based-access-control-custom-roles.md)toocreate 角色 hello 所需的特定權限。

### <a name="azure-user-roles-and-log-analytics-portal-user-roles"></a>Azure 使用者角色和 Log Analytics 入口網站使用者角色
如果您有在最少的 Azure 的讀取權限 hello 記錄分析工作區，您可以開啟 hello 記錄分析入口網站，依序按一下 hello **OMS 入口網站**工作檢視 hello 記錄分析工作區時。

當開啟 hello 記錄分析入口網站，您可以切換 toousing hello 舊版記錄分析使用者角色。 如果您沒有在 hello 記錄分析入口網站中的角色指派，hello 服務[檢查 hello Azure 您擁有 hello 工作區的權限](https://docs.microsoft.com/rest/api/authorization/permissions#Permissions_ListForResource)。
您在 hello 記錄分析入口網站中的角色指派會決定使用，如下所示：

| 條件                                                   | 指派的 Log Analytics 使用者角色 | 注意事項 |
|--------------------------------------------------------------|----------------------------------|-------|
| 您的帳戶所屬 tooa 舊版記錄分析使用者角色     | hello 指定記錄分析使用者角色 | |
| 您的帳戶不屬於 tooa 舊版記錄分析使用者角色 <br> 完整的 Azure 權限 toohello 工作區 (`*`權限<sup>1</sup>) | 系統管理員 ||
| 您的帳戶不屬於 tooa 舊版記錄分析使用者角色 <br> 完整的 Azure 權限 toohello 工作區 (`*`權限<sup>1</sup>) <br> 非 `Microsoft.Authorization/*/Delete` 和 `Microsoft.Authorization/*/Write` 的動作 | 參與者 ||
| 您的帳戶不屬於 tooa 舊版記錄分析使用者角色 <br> Azure 讀取權限 | 唯讀 ||
| 您的帳戶不屬於 tooa 舊版記錄分析使用者角色 <br> 未經辨識的 Azure 權限 | 唯讀 ||
| 適用於雲端解決方案提供者 (CSP) 管理的訂用帳戶 <br> 您已登入與 hello 帳戶是在工作區中連結的 Azure Active Directory toohello hello | 系統管理員 | 通常 hello 的 CSP 的客戶 |
| 適用於雲端解決方案提供者 (CSP) 管理的訂用帳戶 <br> 您已登入與 hello 帳戶不在工作區中連結的 Azure Active Directory toohello hello | 參與者 | 通常 hello CSP |

<sup>1</sup>太參考[Azure 權限](../active-directory/role-based-access-control-custom-roles.md)如需有關角色定義。 評估動作的角色時`*`相當不太`Microsoft.OperationalInsights/workspaces/*`。

關於 hello Azure 入口網站中某些點 tookeep:

* 當您登入使用 http://mms.microsoft.com toohello OMS 入口網站時，您會看到 hello**選取工作區**清單。 此清單只包含您具有 Log Analytics 使用者角色的工作區。 toosee hello 工作區，您有存取 toowith Azure 訂用帳戶，您需要 toospecify 租用戶 hello URL 的一部分。 例如：`mms.microsoft.com/?tenant=contoso.com`。 hello 租用戶識別碼通常是使用 toosign 中的 hello 電子郵件地址的最後一部分。
* 如果您想 toonavigate 直接 tooa 入口網站，您有存取 toousing Azure 權限，則您需要 toospecify hello 資源 hello URL 的一部分。 它是可能 tooget 使用 PowerShell 此 URL。

  例如： `(Get-AzureRmOperationalInsightsWorkspace).PortalUrl`。

  hello URL 看起來像：`https://eus.mms.microsoft.com/?tenant=contoso.com&resource=%2fsubscriptions%2faaa5159e-dcf6-890a-a702-2d2fee51c102%2fresourcegroups%2fdb-resgroup%2fproviders%2fmicrosoft.operationalinsights%2fworkspaces%2fmydemo12`

### <a name="managing-users-in-hello-oms-portal"></a>管理 hello OMS 入口網站中的使用者
您可以管理使用者和群組的 hello**管理使用者** 索引標籤下 hello**帳戶**hello 設定 頁面中的索引標籤。   

![管理使用者](./media/log-analytics-manage-access/setup-workspace-manage-users.png)


#### <a name="add-a-user-tooan-existing-workspace"></a>加入使用者 tooan 現有工作區
使用下列步驟 tooadd 使用者或群組的 tooa 工作區的 hello。

1. 在 hello OMS 入口網站中，按一下 hello**設定**磚。
2. 按一下 hello**帳戶**索引標籤，然後按一下hello**管理使用者** 索引標籤。
3. 在 hello**管理使用者**區段中，選擇 hello 帳戶類型 tooadd:**組織帳戶**， **Microsoft 帳戶**， **Microsoft 支援服務**.

   * 如果您選擇的 Microsoft 帳戶，請輸入 hello 與 hello Microsoft 帳戶相關聯的 hello 使用者的電子郵件地址。
   * 如果您選擇 組織帳戶，輸入部分的 hello 使用者/群組的名稱或電子郵件別名，因此相符的使用者和群組的清單會出現在下拉式方塊。 選取使用者或群組。
   * 使用 Microsoft 支援工程師或其他 Microsoft 員工的暫時存取 tooyour 工作區 toohelp Microsoft 支援服務 toogive 進行疑難排解。

     > [!NOTE]
     > Hello 獲得最佳效能，限制 hello 與單一 OMS 帳戶 toothree 相關聯的 Active Directory 群組數目 — 系統管理員，一個參與者，和另一個用於唯讀使用者。 使用多個群組，可能會對記錄分析的 hello 效能的影響。
     >
     >
4. 選擇使用者或群組 tooadd hello 類型：**管理員**，**參與者**，或**ReadOnly 使用者**。  
5. 按一下 [新增] 。

   如果您要新增 Microsoft 帳戶，邀請 toojoin hello 工作區會傳送 toohello 您提供的電子郵件。 Hello 使用者依照 hello 邀請 toojoin OMS 中的 hello 指示後，hello 使用者可以存取 hello 工作區。
   如果您正在加入組織帳戶，hello 使用者就可以立即存取記錄分析。  

#### <a name="edit-an-existing-user-type"></a>編輯現有的使用者類型
您可以變更 hello 與您的 OMS 帳戶關聯的使用者帳戶角色。 您有下列角色選項的 hello:

* *管理員*：可以管理使用者、檢視和處理所有警示，以及新增和移除伺服器
* *參與者*：可以檢視和處理所有警示，以及新增和移除伺服器
* *唯讀使用者*︰標示為唯讀的使用者無法︰

  1. 新增/移除解決方案。 隱藏 hello 解決方案資源庫。
  2. 在 [我的儀表板] 上新增/修改/移除圖格。
  3. 檢視 hello**設定**頁面。 會隱藏 hello 頁面。
  4. 在 hello 搜尋檢視、 PowerBI 組態、 已儲存的搜尋和警示都會隱藏工作。

#### <a name="tooedit-an-account"></a>tooedit 帳戶
1. 在 hello OMS 入口網站中，按一下 hello**設定**磚。
2. 按一下 hello**帳戶**索引標籤，然後按一下hello**管理使用者** 索引標籤。
3. 選取您想 toochange hello 使用者 hello 角色。
4. 在 hello 確認對話方塊中，按一下 **是**。

### <a name="remove-a-user-from-a-workspace"></a>從工作區移除使用者
使用工作區中的下列步驟 tooremove 使用者 hello。 移除 hello 使用者不會關閉 hello 工作區。 相反地，它會移除該使用者和 hello 工作區中的 hello 關聯。 如果使用者是多個工作區相關聯，該使用者仍然可以登入 tooOMS，並查看其工作區。

1. 在 hello OMS 入口網站中，按一下 hello**設定**磚。
2. 按一下 hello**帳戶**索引標籤，然後按一下hello**管理使用者** 索引標籤。
3. 按一下**移除**想 tooremove 的下一個 toohello 使用者名稱。
4. 在 hello 確認對話方塊中，按一下 **是**。

### <a name="add-a-group-tooan-existing-workspace"></a>新增群組 tooan 現有工作區
1. 在前一節 「 tooadd 使用者 tooan 現有工作區"hello，請遵循步驟 1-4。
2. 在 [選擇使用者/群組] 下方，選取 [群組]。  
   ![新增群組 tooan 現有工作區](./media/log-analytics-manage-access/add-group.png)
3. 輸入顯示名稱或電子郵件地址的 hello hello 群組中，您想要 tooadd。
4. 在 hello 結果清單中選取 hello 群組，然後按一下**新增**。

## <a name="link-an-existing-workspace-tooan-azure-subscription"></a>連結現有的工作區 tooan Azure 訂用帳戶
2016 年 9 月 26 日之後建立的所有工作區必須是連結的 tooan 在建立時的 Azure 訂用帳戶。 此日期之前建立的工作區必須是連結的 tooa 工作區中，當您登入。 當您從 hello Azure 入口網站建立 hello 工作區或連結您的工作區 tooan Azure 訂用帳戶，您的 Azure Active Directory 會連結以組織帳戶。

### <a name="toolink-a-workspace-tooan-azure-subscription-in-hello-oms-portal"></a>toolink 工作區 tooan hello OMS 入口網站中的 Azure 訂用帳戶

- 當您登入 hello OMS 入口網站時，您將會提示的 tooselect Azure 訂用帳戶。 選取您想 toolink tooyour 工作區，然後按一下的 hello 訂用帳戶**連結**。  
    ![連結 Azure 訂用帳戶](./media/log-analytics-manage-access/required-link.png)

    > [!IMPORTANT]
    > toolink 工作區，您的 Azure 帳戶必須已經有您想要 toolink 存取 toohello 工作區。  換句話說，必須使用 tooaccess hello Azure 入口網站的 hello 帳戶**hello 相同**hello 使用 tooaccess hello 工作區的帳戶。 如果沒有，請參閱[加入使用者 tooan 現有工作區](#add-a-user-to-an-existing-workspace)。

### <a name="toolink-a-workspace-tooan-azure-subscription-in-hello-azure-portal"></a>toolink 工作區 tooan hello Azure 入口網站中的 Azure 訂用帳戶
1. 登入 hello [Azure 入口網站](http://portal.azure.com)。
2. 瀏覽 **Log Analytics**，然後加以選取。
3. 您會看到現有工作區清單。 按一下 [新增] 。  
   ![工作區清單](./media/log-analytics-manage-access/manage-access-link-azure01.png)
4. 在 [OMS 工作區] 下方，按一下 [或連結現有的]。  
   ![連結現有的](./media/log-analytics-manage-access/manage-access-link-azure02.png)
5. 按一下 [進行必要設定] 。  
   ![configure required settings](./media/log-analytics-manage-access/manage-access-link-azure03.png)
6. 您會看到工作區不 hello 清單尚未連結 tooyour Azure 帳戶。 選取工作區。  
   ![選取工作區](./media/log-analytics-manage-access/manage-access-link-azure04.png)
7. 如有需要您可以變更下列項目 hello 的值：
   * 訂用帳戶
   * 資源群組
   * 位置
   * 定價層   
     ![變更值](./media/log-analytics-manage-access/manage-access-link-azure05.png)
8. 按一下 [確定] 。 hello 工作區現在是連結的 tooyour Azure 帳戶。

> [!NOTE]
> 如果您沒有看到 hello 工作區中您想要 toolink，然後您 Azure 訂用帳戶沒有存取 toohello 工作區中，建立使用 hello OMS 入口網站。  toogrant 存取 toothis 帳戶 hello OMS 入口網站，請參閱[加入使用者 tooan 現有工作區](#add-a-user-to-an-existing-workspace)。
>
>

## <a name="upgrade-a-workspace-tooa-paid-plan"></a>升級工作區 tooa 付費計劃
OMS 有三種工作區方案類型：[免費]、[獨立] 和 [OMS]。  如果您在 hello*免費*計劃，每一天傳送 tooLog 分析資料的 500 MB 的限制。  如果超過此數量時，您需要 toochange 不會收集超過這個限制您工作區 tooa 付費計劃 tooavoid。 您隨時都可以變更方案類型。  如需 OMS 定價的詳細資訊，請參閱[價格詳細資料](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-pricing)。

### <a name="using-entitlements-from-an-oms-subscription"></a>使用 OMS 訂用帳戶的權利
來自 OMS E1、 OMS E2 OMS 或 System Center 的 OMS 附加元件購買的 toouse hello 權利選擇 hello *OMS* OMS 記錄分析的計劃。

當您購買 OMS 訂用帳戶時，hello 權利加入 tooyour Enterprise 合約。 這個合約會建立任何 Azure 訂用帳戶可以使用 hello 權利。 在這些訂用帳戶上的所有工作區使用 hello OMS 權利。

您需要工作區的使用方式是從 hello OMS 訂用帳戶套用的 tooyour 權利 tooensure:

1. 建立您的工作區中的 hello 包含 hello OMS 訂用帳戶的 Enterprise 合約一部分的 Azure 訂用帳戶
2. 選取 hello *OMS* hello 工作區的計劃

> [!NOTE]
> 如果在 2016 年 9 月 26 日之前已建立您的工作區，而且您定價計畫的記錄分析是*Premium*，則此工作區會使用適用於 System Center 的 hello OMS 附加元件權利。 您也可以使用權利變更 toohello *OMS*定價層。
>
>

hello Azure 或 OMS 入口網站中看不到 hello OMS 訂用帳戶的權利。 您可以看到權利和 hello 企業版入口網站中的使用方式。  

如果您需要 toochange hello 您的工作區連結到 Azure 訂用帳戶，您可以使用 Azure PowerShell hello [Move-azurermresource](https://msdn.microsoft.com/library/mt652516.aspx) cmdlet。

### <a name="using-azure-commitment-from-an-enterprise-agreement"></a>透過 Enterprise 合約使用 Azure 承諾
如果您沒有 OMS 訂用帳戶，分別為每個 OMS 的元件付費，hello 使用方式會出現在 Azure 帳單上。

如果您擁有 hello 企業版註冊 toowhich Azure 綁約連結您的 Azure 訂用帳戶，記錄分析的使用方式會自動借方針對 hello 剩餘貨幣認可。

如果您需要 toochange hello hello 工作區的 Azure 訂用帳戶連結到，您可以使用 Azure PowerShell hello [Move-azurermresource](https://msdn.microsoft.com/library/mt652516.aspx) cmdlet。  

### <a name="change-a-workspace-tooa-paid-pricing-tier-in-hello-azure-portal"></a>變更工作區 tooa 付費 hello Azure 入口網站中的定價層
1. 登入 hello [Azure 入口網站](http://portal.azure.com)。
2. 瀏覽 **Log Analytics**，然後加以選取。
3. 您會看到現有工作區清單。 選取工作區。  
4. 在 hello 工作區刀鋒視窗中，在**一般**，按一下 **定價層**。  
5. 在 定價層 之下，按一下 選取定價層，然後按一下選取。  
    ![選取方案](./media/log-analytics-manage-access/manage-access-change-plan03.png)
6. 當您重新整理檢視 hello Azure 入口網站中的時，您會看到**定價層**hello 層您選取的更新。  
    ![更新的方案](./media/log-analytics-manage-access/manage-access-change-plan04.png)

> [!NOTE]
> 如果您的工作區連結的 tooan 自動化帳戶，之前您可以選取 hello*獨立 (每個 GB)*定價層您必須先刪除任何**自動化和控制**解決方案並取消連結 hello 自動化帳戶。 在 [hello] 工作區刀鋒視窗中下,**一般**，按一下**解決方案**toosee 和刪除方案。 toounlink hello 自動化帳戶中，按一下 hello hello hello 的自動化帳戶名稱**定價層**刀鋒視窗。
>
>

### <a name="change-a-workspace-tooa-paid-pricing-tier-in-hello-oms-portal"></a>變更工作區 tooa 付費 hello OMS 入口網站中的定價層

toochange hello 使用 hello OMS 入口網站的定價層，您必須具有 Azure 訂用帳戶。

1. 在 hello OMS 入口網站中，按一下 hello**設定**磚。
2. 按一下 hello**帳戶**索引標籤，然後按一下hello **Azure 訂用帳戶和數據傳輸方案** 索引標籤。
3. 按一下 定價層想 toouse hello。
4. 按一下 [儲存] 。  
   ![訂用帳戶和行動數據方案](./media/log-analytics-manage-access/subscription-tab.png)

新的資料計劃會顯示在 hello OMS 入口網站功能區上方的網頁 hello。

![OMS 功能區](./media/log-analytics-manage-access/data-plan-changed.png)


## <a name="change-how-long-log-analytics-stores-data"></a>變更 Log Analytics 儲存資料的時間長度

在免費定價層的 hello，記錄分析會使可用 hello 最近七天的資料。
在標準定價層 hello，記錄分析會使可用 hello 過去 30 天的資料。
Hello Premium 定價層，記錄分析會使可用 hello 過去 365 天的資料。
Hello 獨立及定價層，根據預設，OMS 記錄分析會使可用 hello 過去的 31 天內的資料。

當您使用獨立 hello 和 OMS 定價層，您可以繼續 too2 年的資料 （730 天）。 儲存時間超過 hello 預設值為 31 天的資料產生的資料保留費用。 如需價格的詳細資訊，請參閱[超額費用](https://azure.microsoft.com/pricing/details/log-analytics/)。

toochange hello 長度的資料保留：

1. 登入 hello [Azure 入口網站](http://portal.azure.com)。
2. 瀏覽 **Log Analytics**，然後加以選取。
3. 您會看到現有工作區清單。 選取工作區。  
4. 在 hello 下的工作區] 刀鋒視窗**一般**，按一下 [**保留**。  
5. 使用 hello 滑桿 tooincrease 或減少 hello 的保留天數，然後按一下**儲存**。  
    ![變更保留](./media/log-analytics-manage-access/manage-access-change-retention01.png)

## <a name="change-an-azure-active-directory-organization-for-a-workspace"></a>變更工作區的 Azure Active Directory 組織

您可以變更工作區的 Azure Active Directory 組織。 變更 hello Azure Active Directory 組織可讓您 tooadd 使用者和群組從該目錄 toohello 工作區。

### <a name="toochange-hello-azure-active-directory-organization-for-a-workspace"></a>toochange hello Azure Active Directory 組織工作區

1. 在 hello hello OMS 入口網站中設定頁面上，按一下 [**帳戶**然後按一下hello**管理使用者**] 索引標籤。  
2. 檢閱有關組織帳戶，hello 資訊，然後按一下**變更組織**。  
    ![變更組織](./media/log-analytics-manage-access/manage-access-add-adorg01.png)
3. 輸入 hello 系統管理員 」 的 Azure Active Directory 網域中的 hello 身分識別的資訊。 接著，您會看到通知，指出您的工作區連結的 tooyour Azure Active Directory 網域。  
    ![連結的工作區通知](./media/log-analytics-manage-access/manage-access-add-adorg02.png)


## <a name="delete-a-log-analytics-workspace"></a>刪除 Log Analytics 工作區
當您刪除記錄分析工作區時，所有的資料相關 tooyour 工作區的 30 天內，會刪除從 hello OMS 服務。

如果您是系統管理員，而且有多個與 hello 區相關聯的使用者，這些使用者與 hello 區之間的 hello 關聯將會中斷。 如果 hello 使用者與其他工作區相關聯，則他們就可以繼續使用 OMS 的其他工作區。 不過，如果沒有其他工作區相關聯則他們需要 toocreate 工作區 toouse OMS。

### <a name="toodelete-a-workspace"></a>toodelete 工作區
1. 登入 hello [Azure 入口網站](http://portal.azure.com)。
2. 瀏覽 **Log Analytics**，然後加以選取。
3. 您會看到現有工作區清單。 選取您想 toodelete hello 工作區。
4. 在 hello 工作區刀鋒視窗中，按一下 **刪除**。  
    ![delete](./media/log-analytics-manage-access/delete-workspace01.png)
5. 在 hello 刪除工作區確認對話方塊中，按一下 **是**。

## <a name="next-steps"></a>後續步驟
* 請參閱[連接的 Windows 電腦 tooLog 分析](log-analytics-windows-agents.md)tooadd 代理程式並收集資料。
* [新增記錄分析解決方案從 hello 解決方案資源庫](log-analytics-add-solutions.md)tooadd 功能和收集資料。
* [在分析記錄檔中設定 proxy 和防火牆設定](log-analytics-proxy-firewall.md)如果您的組織使用 proxy 伺服器或防火牆，讓代理程式能夠以 hello 記錄分析服務通訊。
