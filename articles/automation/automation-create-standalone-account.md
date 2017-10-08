---
title: "aaaCreate 獨立 Azure 自動化帳戶 |Microsoft 文件"
description: "教學課程，引導您完成 hello 建立、 測試和範例使用在 Azure 自動化中的安全性主體驗證。"
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 2f783441-15c7-4ea0-ba27-d7daa39b1dd3
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/18/2017
ms.author: magoedte
ms.openlocfilehash: 1500d25d9565d4082768933834303a17c5e84234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-standalone-azure-automation-account"></a>建立獨立的 Azure 自動化帳戶
本主題說明您如何 toocreate 自動化帳戶從 Azure 入口網站，如果您想 tooevaluate 並不包括 hello 額外的管理解決方案或與 OMS 記錄分析 tooprovide 整合了 Azure 自動化 hello 進階監視runbook 工作。  您可以新增這些管理解決方案，或整合 hello 未來在任何時間點的記錄分析。  以 hello 自動化帳戶，您就可以 tooauthenticate runbook 管理 Azure 資源管理員或 Azure 傳統部署中的資源。

當您在 hello Azure 入口網站中建立自動化帳戶時，它會自動建立：

* 執行身分帳戶，這在 Azure Active Directory，憑證時，會建立新的服務主體，並指派 hello 參與者角色型存取控制 (RBAC)，也就是使用 toomanage 資源管理員資源使用 runbook。   
* 上傳管理憑證，這是的傳統執行身分帳戶用於使用 runbook toomanage 傳統資源。  

這可讓您簡化 hello 程序可協助您快速開始建置和部署 runbook toosupport 自動化需求。  

## <a name="permissions-required-toocreate-automation-account"></a>所需的權限 toocreate 自動化帳戶
toocreate 或更新自動化帳戶，您必須遵循特定的權限的 hello 和必要的使用權限 toocomplete 本主題。   
 
* 在訂單 toocreate 自動化帳戶，您的 AD 使用者帳戶需要 toobe 加入的 tooa 角色與權限相等 toohello 擁有者角色 Microsoft.Automation 資源的發行項中所述[Azure 自動化中的角色型存取控制](automation-role-based-access-control.md).  
* 如果設定太 hello 應用程式登錄設定**是**，Azure AD 租用戶中的非系統管理使用者可以[註冊 AD 應用程式](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions)。  如果設定太 hello 應用程式登錄設定**否**，執行此動作的 hello 使用者必須是 Azure AD 中的全域管理員。 

如果您不是成員的 hello 訂用帳戶的 Active Directory 執行個體加入 toohello 全域系統管理員/共同管理員的角色 hello 訂用帳戶之前，您會做為來賓新增 tooActive 目錄。 在此情況下，您會收到 「 您沒有權限 toocreate...」 在 hello 警告**加入自動化帳戶**刀鋒視窗。 Toohello 全域系統管理員/共同管理員角色第一次可以從 hello 訂用帳戶的 Active Directory 執行個體中移除和 toomake 已加入的使用者其完整的使用者在 Active Directory 中。 tooverify，請在此情況下，從 hello **Azure Active Directory** hello Azure 入口網站，選取在窗格**使用者和群組**，選取**所有使用者**和選取 hello 之後特定使用者，則選取**設定檔**。 hello 值 hello**使用者類型**hello 使用者設定檔 下的屬性不可等於**客體**。

## <a name="create-a-new-automation-account-from-hello-azure-portal"></a>從 hello Azure 入口網站建立新的自動化帳戶
在本節中，執行下列步驟 toocreate hello Azure 入口網站中的 Azure 自動化帳戶的 hello。    

1. 登入 toohello hello 訂用帳戶系統管理員角色的成員且 hello 訂用帳戶的共同管理員帳戶的 Azure 入口網站。
2. 按一下 [新增] 。<br><br> ![在 Azure 入口網站中選取 [新增] 選項](media/automation-offering-get-started/automation-portal-martketplacestart.png)<br>  
3. 搜尋**自動化**，然後在 hello 搜尋結果選取**自動化和控制***。<br><br> ![在 Marketplace 中搜尋並選取自動化](media/automation-create-standalone-account/automation-marketplace-select-create-automationacct.png)<br> 
3. 在 hello 自動化帳戶刀鋒視窗中，按一下 **新增**。<br><br>![加入自動化帳戶](media/automation-create-standalone-account/automation-create-automationacct-properties.png)
   
   > [!NOTE]
   > 如果您看到下列警告 hello 中的 hello**加入自動化帳戶**刀鋒視窗中，這是因為您的帳戶不是 hello 訂用帳戶系統管理員角色的成員和 hello 訂用帳戶的共同管理員。<br><br>![加入自動化帳戶警告](media/automation-create-standalone-account/create-account-without-perms.png)
   > 
   > 
4. 在 hello**加入自動化帳戶**刀鋒視窗中的，在 hello**名稱**方塊中，輸入新的自動化帳戶的名稱。
5. 如果您有多個訂用帳戶，指定一個 hello 新的帳戶之新的或現有**資源群組**和 Azure 資料中心**位置**。
6. 確認 hello 值**是**選取 hello**建立 Azure 執行身分帳戶**選項，然後按一下 hello**建立** 按鈕。  
   
   > [!NOTE]
   > 如果您選擇 toonot hello 執行身分帳戶選取 hello 選項建立**否**，您會看到一則警告訊息中 hello**加入自動化帳戶**刀鋒視窗。  Hello Azure 入口網站中建立 hello 帳戶時，它沒有對應的驗證識別身分，在您的傳統或資源管理員的訂用帳戶目錄服務，因此，沒有存取 tooresources 您訂用帳戶中。  如此可防止任何從正在 tooauthenticate 可以參考此帳戶的 runbook，並執行這些部署模型中對資源的工作。
   > 
   > ![加入自動化帳戶警告](media/automation-create-standalone-account/create-account-decline-create-runas-msg.png)<br>
   > 未建立 hello 服務主體時，將未指派 hello 參與者角色。
   > 

7. 而 Azure 會建立 hello 自動化帳戶，您可以追蹤在 hello 進度**通知**hello 功能表。

### <a name="resources-included"></a>包含的資源
已成功建立 hello 自動化帳戶時，會自動為您建立數個資源。  hello 下表摘要說明 hello 執行身分帳戶的資源。<br>

| 資源 | 說明 |
| --- | --- |
| AzureAutomationTutorial Runbook |範例圖形化 runbook，示範如何使用 tooauthenticate hello 執行身分帳戶，並取得 hello 資源管理員的所有資源。 |
| AzureAutomationTutorialScript Runbook |此範例 PowerShell runbook 會示範如何使用 tooauthenticate hello 執行身分帳戶，並取得 hello 資源管理員的所有資源。 |
| AzureRunAsCertificate |憑證資產會自動建立自動化帳戶建立期間，或使用現有帳戶 hello 以下的 PowerShell 指令碼。  它可讓您使用 Azure tooauthenticate，讓您可以從 runbook 來管理 Azure 資源管理員資源。  此憑證有一年的有效期。 |
| AzureRunAsConnection |連線資產會自動建立自動化帳戶建立期間，或使用現有帳戶的 hello 以下的 PowerShell 指令碼。 |

hello 下表摘要說明 hello 傳統執行身分帳戶的資源。<br>

| 資源 | 說明 |
| --- | --- |
| AzureClassicAutomationTutorial Runbook |範例圖形化 runbook，以便使用 hello 傳統的執行身分帳戶 （憑證） 的訂用帳戶中取得所有 hello 傳統 Vm，然後輸出 hello VM 名稱和狀態。 |
| AzureClassicAutomationTutorial 指令碼 Runbook |此範例 PowerShell runbook，其使用 hello 傳統的執行身分帳戶 （憑證） 的訂用帳戶中取得所有 hello 傳統 Vm，然後輸出 hello VM 名稱和狀態。 |
| AzureClassicRunAsCertificate |憑證資產會自動建立也就是搭配 Azure 使用 tooauthenticate，因此，您可以從 runbook 來管理 Azure 傳統資源。  此憑證有一年的有效期。 |
| AzureClassicRunAsConnection |也就是自動建立的連線資產搭配 Azure 使用 tooauthenticate，因此，您可以從 runbook 來管理 Azure 傳統資源。 |


## <a name="next-steps"></a>後續步驟
* toolearn 詳細資料圖形化撰寫，請參閱[Azure 自動化中的圖形化撰寫](automation-graphical-authoring-intro.md)。
* 請參閱 < 開始使用 PowerShell runbook tooget[我的第一個 PowerShell runbook](automation-first-runbook-textual-powershell.md)。
* tooget 開始使用 PowerShell 工作流程 runbook，請參閱[我的第一個 PowerShell 工作流程 runbook](automation-first-runbook-textual.md)。
