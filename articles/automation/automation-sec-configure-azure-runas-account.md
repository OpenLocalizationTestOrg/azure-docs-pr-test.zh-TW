---
title: "aaaConfigure Azure 執行身分帳戶 |Microsoft 文件"
description: "本教學課程會引導您 hello 建立、 測試和範例使用在 Azure 自動化中的安全性主體驗證。"
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
keywords: "服務主體名稱, setspn, azure 驗證"
ms.assetid: 2f783441-15c7-4ea0-ba27-d7daa39b1dd3
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/06/2017
ms.author: magoedte
ROBOTS: NOINDEX
redirect_url: /azure/automation/
redirect_document_id: True
ms.openlocfilehash: 06675d2f6b9d8e7260ffaead4f2b2f61c2b98d13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-an-azure-run-as-account"></a>使用 Azure 執行身分帳戶驗證 Runbook
本文章將示範如何 tooconfigure Azure 自動化帳戶 hello Azure 入口網站中。 toodo 因此，您可以使用 hello 執行身分帳戶功能 tooauthenticate runbook 管理在 Azure 資源管理員] 或 [Azure 服務管理的資源。

當您在 hello Azure 入口網站中建立自動化帳戶時，您會自動建立兩個帳戶：

* 執行身分帳戶。 此帳戶會在 Azure Active Directory (Azure AD) 中建立服務主體，並建立一個憑證。 它也會指派 hello 參與者角色型存取控制 (RBAC)，可使用 runbook 來管理資源管理員資源。
* 傳統執行身分帳戶。 此帳戶上傳管理憑證，也就是使用服務管理 toomanage 或傳統資源使用 runbook。

必須建立您的自動化帳戶的您，並可協助您快速開始建置及部署 runbook toosupport 簡化 hello 程序自動化。

使用執行身分和傳統執行身分帳戶，您可以︰

* 當資源管理員或服務管理資源管理 hello Azure 入口網站中的 runbook 從 Azure 提供標準化的方式 tooauthenticate。
* 自動化 hello 使用通用的 runbook，您可以設定 Azure 的警示。

> [!NOTE]
> hello [Azure 警示的整合功能](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)與自動化全域 runbook 需要使用已設定執行身分帳戶與傳統執行身分帳戶的自動化帳戶。 您可以選取自動化帳戶已有定義執行身分和傳統執行身分帳戶，或您可以選擇 toocreate 新的自動化帳戶。
>  

本文示範 toocreate 自動化帳戶從 hello Azure 入口網站如何使用 Azure PowerShell 更新自動化帳戶、 管理 hello 帳戶設定，以及驗證您的 runbook。

您開始建立自動化帳戶之前，它會是個不錯的主意 toounderstand，並考慮下列 hello:

* 建立自動化帳戶，不會影響您可能已經在傳統的 hello 或資源管理員部署模型中建立的自動化帳戶。
* hello 程序只適用於您在 hello Azure 入口網站中建立的自動化帳戶。 嘗試 toocreate hello Azure 傳統入口網站的帳戶不會複寫 hello 執行身分帳戶設定。
* 如果您已經有 runbook 與資產 （例如排程或變數） 中發生 toomanage 傳統資源，而且您想 runbook tooauthenticate 與 hello 新傳統執行身分帳戶，執行 hello 下列任一動作：

  * toocreate 傳統執行身分帳戶，請遵循 hello < 管理您的執行身分帳戶 > 一節中的 hello 指示。 
  * tooupdate hello 「 使用 PowerShell 來更新您的自動化帳戶 」 一節中的現有帳戶，使用 hello PowerShell 指令碼。
* tooauthenticate 使用 hello 新執行身分帳戶和傳統執行與自動化帳戶，需要您現有的 runbook 與 hello hello > 一節中提供的範例程式碼的 toomodify[驗證程式碼範例](#authentication-code-examples)。

    >[!NOTE]
    >hello 執行身分帳戶是針對使用 hello 憑證為基礎的服務主體的資源管理員資源進行驗證。 hello 傳統執行身分帳戶是對服務管理資源的管理憑證進行驗證。

## <a name="create-an-automation-account-from-hello-azure-portal"></a>從 hello Azure 入口網站中建立自動化帳戶
在本節中，您可以建立 Azure 自動化帳戶從 hello 接著會建立執行身分帳戶和傳統執行身分帳戶的 Azure 入口網站。

>[!NOTE]
>toocreate 自動化帳戶，您必須是 hello 服務系統管理員角色的成員或 hello 訂用帳戶會授與存取 toohello 訂用帳戶的共同管理員。 您也必須新增為使用者 toothat 訂用帳戶的預設 Active Directory 執行個體。 hello 帳戶不需要 toobe 的特殊權限的角色指派。
>
>如果您不是成員的 hello 訂用帳戶的 Active Directory 執行個體加入 toohello hello 訂用帳戶的共同管理員角色之前，您將會做為來賓新增 tooActive 目錄。 在此例中，您會收到 「 您沒有權限 toocreate...」 在 hello 警告**加入自動化帳戶**刀鋒視窗。
>
>Toohello 共同系統管理員角色首先會從 hello 訂用帳戶的 Active Directory 執行個體，並重新加入 toomake 加入的使用者其完整的使用者在 Active Directory 中。 tooverify 這種情況的 hello **Azure Active Directory** hello 選取 Azure 入口網站中的窗格**使用者和群組**、 選取**所有使用者**後，您選取hello 特定使用者，選取**設定檔**。 hello 值 hello**使用者類型**hello 使用者設定檔 下的屬性不可等於**客體**。
>

1. 登入 toohello hello 訂用帳戶系統管理員角色的成員且 hello 訂用帳戶的共同管理員帳戶的 Azure 入口網站。

2. 選取 [自動化帳戶] 。

3. 在 hello**自動化帳戶**刀鋒視窗中，按一下 **新增**。
hello**加入自動化帳戶**刀鋒視窗隨即開啟。

 ![hello [加入自動化帳戶] 刀鋒視窗](media/automation-sec-configure-azure-runas-account/create-automation-account-properties-b.png)

   > [!NOTE]
   > 如果您的帳戶不是 hello 訂用帳戶系統管理員角色的成員和 hello 訂用帳戶的共同管理員，hello 上會顯示下列警告 hello**加入自動化帳戶**刀鋒視窗中：
   >
   >![加入自動化帳戶警告](media/automation-sec-configure-azure-runas-account/create-account-without-perms.png)
   >
   >

4. 在 hello**加入自動化帳戶**刀鋒視窗中的，在 hello**名稱**方塊中，輸入新的自動化帳戶的名稱。

5. 如果您有多個訂用帳戶時，請勿 hello 遵循：

    a. 在下**訂用帳戶**，指定一個 hello 新帳戶。

    b. 在 [資源群組] 底下，按一下 [建立新的] 或 [使用現有的]。

    c. 在 [位置] 底下，指定 Azure 資料中心。

6. 在 建立 Azure 執行身分帳戶 底下選取 是，然後按一下建立。

   > [!NOTE]
   > 如果您選擇不 toocreate hello 執行身分帳戶選取**否**，會顯示警告訊息 hello**加入自動化帳戶**刀鋒視窗。 雖然 hello 帳戶建立 hello Azure 入口網站中，它並沒有對應的驗證識別身分，在您的傳統或資源管理員的訂用帳戶目錄服務中。 因此，hello 帳戶已無存取 tooresources 您訂用帳戶中。 此情況會導致參考此帳戶的任何 Runbook 無法進行驗證，也無法對這些部署模型中的資源執行工作。
   >
   > ![Hello [加入自動化帳戶] 刀鋒視窗上的警告訊息](media/automation-sec-configure-azure-runas-account/create-account-decline-create-runas-msg.png)
   >
   > 此外，因為不建立 hello 服務主體、 hello 參與者角色未指派。
   >

7. 而 Azure 會建立 hello 自動化帳戶，您可以追蹤在 hello 進度**通知**hello 功能表。

### <a name="resources"></a>資源
已成功建立 hello 自動化帳戶時，會自動為您建立數個資源。 下列兩個資料表的 hello 摘要 hello 資源：

#### <a name="run-as-account-resources"></a>執行身分帳戶資源

| 資源 | 說明 |
| --- | --- |
| AzureAutomationTutorial Runbook | 範例圖形化 runbook，示範如何使用 tooauthenticate hello 執行身分帳戶，並取得 hello 資源管理員的所有資源。 |
| AzureAutomationTutorialScript Runbook | 此範例 PowerShell runbook 會示範如何使用 tooauthenticate hello 執行身分帳戶，並取得 hello 資源管理員的所有資源。 |
| AzureRunAsCertificate | hello 憑證資產會自動建立，當您建立自動化帳戶，或使用現有的帳戶的 PowerShell 指令碼後面的 hello。 hello 憑證可讓您使用 Azure tooauthenticate，讓您可以從 runbook 來管理 Azure 資源管理員資源。 hello 憑證都有一年的使用期限。 |
| AzureRunAsConnection | hello 連線資產會自動建立，當您建立自動化帳戶，或使用現有帳戶的 hello PowerShell 指令碼。 |

#### <a name="classic-run-as-account-resources"></a>傳統執行身分帳戶資源

| 資源 | 說明 |
| --- | --- |
| AzureClassicAutomationTutorial Runbook | 取得所有訂用帳戶中的 hello 傳統部署模型，使用 hello 傳統執行身分帳戶 （憑證），來建立和再將 hello VM 名稱和狀態 hello Vm 範例圖形化 runbook。 |
| AzureClassicAutomationTutorial 指令碼 Runbook | 取得所有的範例 PowerShell runbook hello 傳統訂用帳戶中的 Vm 使用 hello 傳統執行身分帳戶 （憑證），並寫入然後 hello VM 名稱和狀態。 |
| AzureClassicRunAsCertificate | 您搭配 Azure 使用 tooauthenticate，使您可以管理 Azure 傳統資源從 runbook 自動建立 hello 憑證資產。 hello 憑證都有一年的使用期限。 |
| AzureClassicRunAsConnection | 您搭配 Azure 使用 tooauthenticate，以便您可以從 runbook 來管理 Azure 傳統資源 hello 自動建立的連線資產。 |

## <a name="verify-run-as-authentication"></a>確認執行身分驗證
執行使用 hello 新執行身分帳戶可以成功進行驗證的小型測試 tooconfirm。

1. 在 hello Azure 入口網站，開啟您稍早建立的 hello 自動化帳戶。

2. 按一下 hello **Runbook**磚 tooopen hello runbook 的清單。

3. 選取 hello **AzureAutomationTutorialScript** runbook，然後按一下**啟動**toostart hello runbook。 發生下列事件的 hello:
 * A [runbook 工作](automation-runbook-execution.md)建立時，hello**作業**刀鋒視窗會顯示，而 hello 工作狀態會顯示在 hello**工作摘要**磚。
 * hello 作業狀態的開頭為**排入佇列**，表示它正在等待在 hello 雲端 toobecome 可用的 runbook worker。
 * hello 狀態會變成**起始**當背景工作宣告 hello 作業。
 * hello 狀態會變成**執行**hello runbook 開始執行時。
 * Hello runbook 工作完成時執行，您應該會看到狀態為**已完成**。

       ![Security Principal Runbook Test](media/automation-sec-configure-azure-runas-account/job-summary-automationtutorialscript.png)
4. toosee hello hello runbook 的詳細的結果，請按一下 hello**輸出**磚。  
hello**輸出**刀鋒視窗會顯示，其中該 hello runbook 順利通過驗證，並傳回一份 hello 資源群組中所提供的所有資源。

5. 關閉 hello**輸出**刀鋒視窗 tooreturn toohello**工作摘要**刀鋒視窗。

6. 關閉 hello**工作摘要**刀鋒視窗，然後 hello 對應**AzureAutomationTutorialScript** runbook 刀鋒視窗。

## <a name="verify-classic-run-as-authentication"></a>確認傳統執行身分驗證
執行類似的小型測試 tooconfirm 使用 hello 新傳統執行身分帳戶可以成功進行驗證。

1. 在 hello Azure 入口網站，開啟您稍早建立的 hello 自動化帳戶。

2. 按一下 hello **Runbook**磚 tooopen hello runbook 的清單。

3. 選取 hello **AzureClassicAutomationTutorialScript** runbook，然後按一下**啟動**太啟動 hello runbook。 發生下列事件的 hello:

 * A [runbook 工作](automation-runbook-execution.md)建立時，hello**作業**刀鋒視窗會顯示，而 hello 工作狀態會顯示在 hello**工作摘要**磚。
 * hello 作業狀態的開頭為**排入佇列**，表示它正在等待在 hello 雲端 toobecome 可用的 runbook worker。
 * hello 狀態會變成**起始**當背景工作宣告 hello 作業。
 * hello 狀態會變成**執行**hello runbook 開始執行時。
 * Hello runbook 工作完成時執行，您應該會看到狀態為**已完成**。

    ![安全性主體 Runbook 測試](media/automation-sec-configure-azure-runas-account/job-summary-automationclassictutorialscript.png)<br>
4. toosee hello hello runbook 的詳細的結果，請按一下 hello**輸出**磚。  
hello**輸出**刀鋒視窗會顯示，其中該 hello runbook 成功通過驗證，並傳回的清單中的所有傳統 Vm hello 訂用帳戶中。

5. 關閉 hello**輸出**刀鋒視窗 tooreturn toohello**工作摘要**刀鋒視窗。

6. 關閉 hello**工作摘要**刀鋒視窗，然後 hello 對應**AzureAutomationTutorialScript** runbook 刀鋒視窗。

## <a name="managing-your-run-as-account"></a>管理執行身分帳戶
在某個時間點您的自動化帳戶到期前，您將需要 toorenew hello 憑證。 如果您認為該 hello 執行身分帳戶已遭洩漏，您可以刪除並重新建立它。 本章節將討論如何 tooperform 這些作業。

### <a name="self-signed-certificate-renewal"></a>自我簽署憑證更新
hello hello 執行身分帳戶建立的自我簽署的憑證到期從建立 hello 日期起一年。 您可以在該憑證到期前隨時更新憑證。 當您更新它時，hello 目前有效的憑證會保留的 tooensure 任何 runbook 的執行中或正在執行，會進入佇列，並可向 hello 執行身分帳戶，不會產生負面影響。 hello 憑證到期日前就持續有效。

> [!NOTE]
> 如果您已設定您自動化執行身分帳戶 toouse 您企業憑證授權單位所核發的憑證，且您使用此選項，將會自我簽署憑證所取代 hello 企業憑證。

toorenew hello 憑證，請勿遵循 hello:

1. 在 hello Azure 入口網站，開啟 hello 自動化帳戶。

2. 在 hello**自動化帳戶**刀鋒視窗中的，在 hello**帳戶屬性**窗格下**帳戶設定**，選取**執行身分帳戶**。

    ![自動化帳戶的屬性窗格](media/automation-sec-configure-azure-runas-account/automation-account-properties-pane.png)
3. 在 hello**執行身分帳戶**屬性刀鋒視窗中，選取任一 hello 執行身分帳戶或 hello 傳統執行身分帳戶，您想要 toorenew hello 憑證。

4. 在 hello**屬性**hello 刀鋒視窗中選取帳戶，請按一下**更新憑證**。

    ![更新執行身分帳戶的憑證](media/automation-sec-configure-azure-runas-account/automation-account-renew-runas-certificate.png)

5. 當更新 hello 憑證後時，您可以追蹤下的 hello 進度**通知**hello 功能表。

### <a name="delete-a-run-as-or-classic-run-as-account"></a>刪除執行身分或傳統執行身分帳戶
本章節描述如何 toodelete 並重新建立執行身分或傳統執行身分帳戶。 當您執行此動作時，會保留 hello 自動化帳戶。 刪除執行身分或傳統執行身分帳戶後，您可以在 hello Azure 入口網站中重新建立它。

1. 在 hello Azure 入口網站，開啟 hello 自動化帳戶。

2. 在 [hello**自動化帳戶**刀鋒視窗中的，hello 帳戶屬性] 窗格中，選取**執行身分帳戶**。

3. 在 hello**執行身分帳戶**想 toodelete 屬性刀鋒視窗中，選取任一 hello 執行身分帳戶 」 或 「 傳統執行身分帳戶。 然後，在 hello**屬性**hello 刀鋒視窗中選取帳戶，請按一下**刪除**。

 ![刪除執行身分帳戶](media/automation-sec-configure-azure-runas-account/automation-account-delete-runas.png)

4. 正在刪除 hello 帳戶，而您可以追蹤下的 hello 進度**通知**hello 功能表。

5. Hello 帳戶已被刪除後，您可以重新建立它在 hello**執行身分帳戶**屬性刀鋒視窗中的選取 hello 建立選項**Azure 執行身分帳戶**。

 ![重新建立 hello 自動化執行身分帳戶](media/automation-sec-configure-azure-runas-account/automation-account-create-runas.png)

### <a name="misconfiguration"></a>設定錯誤
某些組態項目所需的 hello 執行身分或傳統執行身分帳戶 toofunction 正確可能已刪除或在初始安裝期間，建立方式不正確。 hello 項目包括：

* 憑證資產
* 連線資產
* 已從 hello 參與者角色移除執行身分帳戶
* Azure AD 中的服務主體或應用程式

在上述的 hello 和設定錯誤的其他執行個體，hello 自動化帳戶會偵測 hello 變更，並顯示狀態為*完整*上 hello**執行身分帳戶**hello 的屬性刀鋒視窗帳戶。

![不完整的執行身分帳戶設定狀態](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config.png)

當您選取執行身分帳戶 hello 時，hello 帳戶**屬性** 窗格會顯示下列錯誤訊息的 hello:

![不完整的執行身分設定警告訊息](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config-msg.png).

您可以快速解決這些執行身分帳戶的問題，藉由刪除並重新建立 hello 帳戶。

## <a name="update-your-automation-account-by-using-powershell"></a>使用 PowerShell 更新自動化帳戶
如果您可以使用指定 PowerShell tooupdate 您現有的自動化帳戶：

* 建立自動化帳戶，但拒絕 toocreate hello 執行身分帳戶。
* 您已經使用自動化帳戶 toomanage 資源管理員資源，並想 runbook 驗證 tooupdate hello tooinclude hello 執行身分帳戶。
* 您已經使用自動化帳戶 toomanage 傳統資源，而且您想 tooupdate 它 toouse hello 傳統執行身分帳戶，而不要建立新的帳戶和移轉您的 runbook 與資產 tooit。   
* 您想要 toocreate 執行身分和傳統執行身分帳戶使用企業憑證授權單位 (CA) 所核發的憑證。

hello 指令碼有 hello 下列必要條件：

* hello 指令碼可以與 2.01 和更新版本的 Azure 資源管理員模組只能在 Windows 10 和 Windows Server 2016 上執行。 不支援在舊版 Windows 上執行。
* Azure PowerShell 1.0 和更新版本。 如需 hello PowerShell 1.0 版的資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。
* 自動化帳戶被稱為 hello hello 值*– AutomationAccountName*和*-ApplicationDisplayName* hello 下列 PowerShell 指令碼中的參數。

tooget hello 值*SubscriptionID*， *ResourceGroup*，和*AutomationAccountName*、 哪些是 hello 指令碼的必要的參數、 執行 hello 遵循：
1. 在 hello Azure 入口網站中選取您的自動化帳戶上 hello**自動化帳戶**刀鋒視窗中，然後再選取**所有設定**。 
2. 在 hello**所有設定**刀鋒視窗底下**帳戶設定**，選取**屬性**。 
3. 請注意在 hello hello 值**屬性**刀鋒視窗。

![hello 自動化帳戶 [屬性] 刀鋒視窗](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

### <a name="create-a-run-as-account-powershell-script"></a>建立執行身分帳戶 PowerShell 指令碼
這個 PowerShell 指令碼包含支援的設定 hello:

* 使用自我簽署憑證建立執行身分帳戶。
* 使用自我簽署憑證建立執行身分帳戶和傳統執行身分帳戶。
* 使用企業憑證建立執行身分帳戶和傳統執行身分帳戶。
* 建立執行身分帳戶和傳統執行身分帳戶 hello Azure 政府雲端中使用自我簽署的憑證。

視您選取的 hello 組態選項，hello 指令碼會建立 hello 下列項目。

**若為執行身分帳戶︰**

* 建立 Azure AD 應用程式 toobe 匯出以自我簽署的任一個 hello 或企業憑證的公開金鑰，在 Azure AD 中建立 hello 應用程式的服務主體帳戶，並指派 hello hello 帳戶在您目前的參與者角色訂用帳戶。 您可以變更此設定 tooOwner 或任何其他角色。 如需詳細資訊，請參閱 [Azure 自動化中的角色型存取控制](automation-role-based-access-control.md)。
* 建立名為自動化憑證資產*AzureRunAsCertificate* hello 中指定的自動化帳戶。 hello 憑證資產會保存 hello 憑證私密金鑰，可由 hello Azure AD 應用程式。
* 建立名為自動化連線資產*AzureRunAsConnection* hello 中指定的自動化帳戶。 hello 連線資產會保存 hello applicationId、 tenantId、 subscriptionId、 和憑證指紋。

**若為傳統執行身分帳戶：**

* 建立名為自動化憑證資產*AzureClassicRunAsCertificate* hello 中指定的自動化帳戶。 hello 憑證資產會保存 hello 憑證私密金鑰由 hello 管理憑證。
* 建立名為自動化連線資產*AzureClassicRunAsConnection* hello 中指定的自動化帳戶。 hello 連線資產包含 hello 訂用帳戶名稱、 訂用帳戶 Id，與憑證資產名稱。

>[!NOTE]
> 如果您選取其中一個選項，建立傳統執行身分帳戶，hello 指令碼執行之後上, 傳 hello 公用憑證 （.cer 檔案名稱副檔名） toohello 管理的存放區 hello 訂用帳戶的 hello 自動化帳戶中建立。
> 

tooexecute hello 指令碼和 hello 憑證上傳，請勿遵循 hello:

1. 儲存您的電腦上下列指令碼的 hello。 在此範例中，以儲存 hello filename*新增 RunAsAccount.ps1*。

        #Requires -RunAsAdministrator
         Param (
        [Parameter(Mandatory=$true)]
        [String] $ResourceGroup,

        [Parameter(Mandatory=$true)]
        [String] $AutomationAccountName,

        [Parameter(Mandatory=$true)]
        [String] $ApplicationDisplayName,

        [Parameter(Mandatory=$true)]
        [String] $SubscriptionId,

        [Parameter(Mandatory=$true)]
        [Boolean] $CreateClassicRunAsAccount,

        [Parameter(Mandatory=$true)]
        [String] $SelfSignedCertPlainPassword,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$EnvironmentName="AzureCloud",

        [Parameter(Mandatory=$false)]
        [int] $SelfSignedCertNoOfMonthsUntilExpired = 12
        )

        function CreateSelfSignedCertificate([string] $keyVaultName, [string] $certificateName, [string] $selfSignedCertPlainPassword,
                                      [string] $certPath, [string] $certPathCer, [string] $selfSignedCertNoOfMonthsUntilExpired ) {
        $Cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation cert:\LocalMachine\My `
           -KeyExportPolicy Exportable -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
           -NotAfter (Get-Date).AddMonths($selfSignedCertNoOfMonthsUntilExpired)

        $CertPassword = ConvertTo-SecureString $selfSignedCertPlainPassword -AsPlainText -Force
        Export-PfxCertificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPath -Password $CertPassword -Force | Write-Verbose
        Export-Certificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPathCer -Type CERT | Write-Verbose
        }

        function CreateServicePrincipal([System.Security.Cryptography.X509Certificates.X509Certificate2] $PfxCert, [string] $applicationDisplayName) {  
        $CurrentDate = Get-Date
        $keyValue = [System.Convert]::ToBase64String($PfxCert.GetRawCertData())
        $KeyId = (New-Guid).Guid

        $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
        $KeyCredential.StartDate = $CurrentDate
        $KeyCredential.EndDate= [DateTime]$PfxCert.GetExpirationDateString()
        $KeyCredential.EndDate = $KeyCredential.EndDate.AddDays(-1)
        $KeyCredential.KeyId = $KeyId
        $KeyCredential.CertValue  = $keyValue

        # Use key credentials and create an Azure AD application
        $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $KeyId) -KeyCredentials $KeyCredential
        $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId
        $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

        # Sleep here for a few seconds tooallow hello service principal application toobecome active (ordinarily takes a few seconds)
        Sleep -s 15
        $NewRole = New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
        $Retries = 0;
        While ($NewRole -eq $null -and $Retries -le 6)
        {
           Sleep -s 10
           New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
           $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
           $Retries++;
        }
           return $Application.ApplicationId.ToString();
        }

        function CreateAutomationCertificateAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $certifcateAssetName,[string] $certPath, [string] $certPlainPassword, [Boolean] $Exportable) {
        $CertPassword = ConvertTo-SecureString $certPlainPassword -AsPlainText -Force   
        Remove-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $certifcateAssetName -ErrorAction SilentlyContinue
        New-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Path $certPath -Name $certifcateAssetName -Password $CertPassword -Exportable:$Exportable  | write-verbose
        }

        function CreateAutomationConnectionAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $connectionAssetName, [string] $connectionTypeName, [System.Collections.Hashtable] $connectionFieldValues ) {
        Remove-AzureRmAutomationConnection -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -Force -ErrorAction SilentlyContinue
        New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -ConnectionTypeName $connectionTypeName -ConnectionFieldValues $connectionFieldValues
        }

        Import-Module AzureRM.Profile
        Import-Module AzureRM.Resources

        $AzureRMProfileVersion= (Get-Module AzureRM.Profile).Version
        if (!(($AzureRMProfileVersion.Major -ge 2 -and $AzureRMProfileVersion.Minor -ge 1) -or ($AzureRMProfileVersion.Major -gt 2)))
        {
           Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
           return
        }

        Login-AzureRmAccount -EnvironmentName $EnvironmentName
        $Subscription = Select-AzureRmSubscription -SubscriptionId $SubscriptionId

        # Create a Run As account by using a service principal
        $CertifcateAssetName = "AzureRunAsCertificate"
        $ConnectionAssetName = "AzureRunAsConnection"
        $ConnectionTypeName = "AzureServicePrincipal"

        if ($EnterpriseCertPathForRunAsAccount -and $EnterpriseCertPlainPasswordForRunAsAccount) {
        $PfxCertPathForRunAsAccount = $EnterpriseCertPathForRunAsAccount
        $PfxCertPlainPasswordForRunAsAccount = $EnterpriseCertPlainPasswordForRunAsAccount
        } else {
          $CertificateName = $AutomationAccountName+$CertifcateAssetName
          $PfxCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".pfx")
          $PfxCertPlainPasswordForRunAsAccount = $SelfSignedCertPlainPassword
          $CerCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".cer")
          CreateSelfSignedCertificate $KeyVaultName $CertificateName $PfxCertPlainPasswordForRunAsAccount $PfxCertPathForRunAsAccount $CerCertPathForRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create a service principal
        $PfxCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($PfxCertPathForRunAsAccount, $PfxCertPlainPasswordForRunAsAccount)
        $ApplicationId=CreateServicePrincipal $PfxCert $ApplicationDisplayName

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate hello ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
            # Create a Run As account by using a service principal
            $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
            $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
            $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
            $UploadMessage = "Please upload hello .cer format of #CERT# toohello Management store by following hello steps below." + [Environment]::NewLine +
                    "Log in toohello Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                    "Then click Upload and upload hello .cer format of #CERT#"

             if ($EnterpriseCertPathForClassicRunAsAccount -and $EnterpriseCertPlainPasswordForClassicRunAsAccount ) {
             $PfxCertPathForClassicRunAsAccount = $EnterpriseCertPathForClassicRunAsAccount
             $PfxCertPlainPasswordForClassicRunAsAccount = $EnterpriseCertPlainPasswordForClassicRunAsAccount
             $UploadMessage = $UploadMessage.Replace("#CERT#", $PfxCertPathForClassicRunAsAccount)
        } else {
             $ClassicRunAsAccountCertificateName = $AutomationAccountName+$ClassicRunAsAccountCertifcateAssetName
             $PfxCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".pfx")
             $PfxCertPlainPasswordForClassicRunAsAccount = $SelfSignedCertPlainPassword
             $CerCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".cer")
             $UploadMessage = $UploadMessage.Replace("#CERT#", $CerCertPathForClassicRunAsAccount)
             CreateSelfSignedCertificate $KeyVaultName $ClassicRunAsAccountCertificateName $PfxCertPlainPasswordForClassicRunAsAccount $PfxCertPathForClassicRunAsAccount $CerCertPathForClassicRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate hello ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. 在電腦上按一下 [啟動]，然後以提高的使用者權限啟動 **Windows PowerShell**。

3. 從 hello 提高 PowerShell 命令列殼層移 toohello 資料夾包含您在步驟 1 中建立的 hello 指令碼。

4. 您需要的 hello 組態使用 hello 參數值執行 hello 指令碼。

    **使用自我簽署憑證建立執行身分帳戶**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    **使用自我簽署憑證建立執行身分帳戶和傳統執行身分帳戶**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    **使用企業憑證建立執行身分帳戶和傳統執行身分帳戶**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    **使用自我簽署的憑證 hello Azure 政府雲端中建立執行身分帳戶和傳統執行身分帳戶**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > Hello 指令碼執行之後，您將會提示的 tooauthenticate 與 Azure。 使用屬於 hello 訂用帳戶系統管理員角色的成員和 hello 訂用帳戶的共同管理員帳戶登入。
    >
    >

Hello 指令碼順利執行之後，請注意 hello 下列：
* 如果您使用自我簽署的公開憑證 （.cer 檔案） 建立傳統執行身分帳戶，hello 指令碼建立，並將它 hello 使用者設定檔在電腦上儲存 toohello 暫存檔案資料夾*%USERPROFILE%\AppData\Local\Temp*，使用 tooexecute hello PowerShell 工作階段。
* 如果您使用企業公開憑證 (.cer 檔案) 建立了傳統執行身分帳戶，請使用此憑證。 請依照指示 hello[上傳 Azure 傳統入口網站管理 API 憑證 toohello](../azure-api-management-certs.md)，並驗證服務管理資源的 hello 認證組態使用 hello[範例程式碼服務管理資源 tooauthenticate](#sample-code-to-authenticate-with-service-management-resources)。 
* 如果您未*不*建立傳統執行身分帳戶、 向資源管理員資源及驗證 hello 認證組態使用 hello[範例程式碼來驗證服務管理資源](#sample-code-to-authenticate-with-resource-manager-resources)。

## <a name="sample-code-tooauthenticate-with-resource-manager-resources"></a>使用資源管理員資源的範例程式碼 tooauthenticate
您可以使用更新的 hello 下列範例程式碼取自 hello *AzureAutomationTutorialScript*範例 runbook、 tooauthenticate 透過 hello 執行身分帳戶 toomanage 資源管理員資源與您的 runbook。

    $connectionName = "AzureRunAsConnection"
    $SubId = Get-AutomationVariable -Name 'SubscriptionId'
    try
    {
       # Get hello connection "AzureRunAsConnection "
       $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

       "Signing in tooAzure..."
       Add-AzureRmAccount `
         -ServicePrincipal `
         -TenantId $servicePrincipalConnection.TenantId `
         -ApplicationId $servicePrincipalConnection.ApplicationId `
         -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
       "Setting context tooa specific subscription"     
       Set-AzureRmContext -SubscriptionId $SubId              
    }
    catch {
        if (!$servicePrincipalConnection)
        {
           $ErrorMessage = "Connection $connectionName not found."
           throw $ErrorMessage
         } else{
            Write-Error -Message $_.Exception
            throw $_.Exception
         }
    }

您 tooeasily 處理多個訂用帳戶之間的 toohelp，hello 指令碼包含兩個額外的程式碼行支援參考在訂用帳戶的內容。 名為變數資產*SubscriptionId*包含 hello hello 訂用帳戶識別碼。 之後 hello `Add-AzureRmAccount` cmdlet 陳述式，hello [ `Set-AzureRmContext` ](/powershell/module/azurerm.profile/set-azurermcontext)指令程式會與 hello 參數集陳述*-SubscriptionId*。 如果太泛型 hello 變數名稱，您可以修改它 tooinclude 前置詞，或使用另一個命名慣例 toomake 它更容易 tooidentify。 或者，您可以使用 hello 參數集*-訂用帳戶名稱*而不是*-SubscriptionId*與對應的變數資產。

hello 您用來驗證 hello runbook 中的 cmdlet `Add-AzureRmAccount`，使用 hello *ServicePrincipalCertificate*參數集。 它會使用 hello 服務主體認證，hello 使用者認證來驗證。

## <a name="sample-code-tooauthenticate-with-service-management-resources"></a>範例程式碼 tooauthenticate 與服務管理資源
您可以使用下列更新的範例程式碼，取自 hello hello *AzureClassicAutomationTutorialScript*範例 runbook，使用傳統執行身分帳戶 toomanage，傳統資源與 hello tooauthenticate 您runbook。

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID

## <a name="next-steps"></a>後續步驟
* [Azure AD 中的應用程式和服務主體物件](../active-directory/active-directory-application-objects.md)
* [Azure 自動化中的角色型存取控制](automation-role-based-access-control.md)
* [Azure 雲端服務的憑證概觀](../cloud-services/cloud-services-certs-create.md)
