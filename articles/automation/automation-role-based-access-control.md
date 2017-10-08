---
title: "在 Azure 自動化中的 aaaRole 型存取控制 |Microsoft 文件"
description: "角色型存取控制 (RBAC) 可以啟用對 Azure 資源的存取權管理。 本文說明如何在 Azure 自動化中的 RBAC 的向上 tooset。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
keywords: "自動化 rbac, 角色型存取控制, azure rbac"
ms.assetid: 04b5625e-0ee8-4b5b-85cd-7734c1b3d4a3
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/12/2016
ms.author: magoedte;sngun
ms.openlocfilehash: 051438e44d0c5c514d6dbaac5a312344ee311cdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-in-azure-automation"></a>Azure 自動化中的角色型存取控制
## <a name="role-based-access-control"></a>角色型存取控制
角色型存取控制 (RBAC) 可以啟用對 Azure 資源的存取權管理。 使用[RBAC](../active-directory/role-based-access-control-configure.md)、 您可以在您的小組隔離責任和授與僅 hello 存取 toousers、 群組和應用程式，它們必須 tooperform 他們的工作數量。 可以授與以角色為基礎的存取權 toousers 使用 hello Azure 入口網站、 Azure 命令列工具或 Azure 管理 Api。

## <a name="rbac-in-automation-accounts"></a>自動化帳戶中的 RBAC
在 Azure 自動化中，會授與存取指派適當 RBAC 角色 toousers hello、 群組和應用程式在 hello 自動化帳戶範圍。 下列是 hello 支援自動化帳戶的內建角色：  

| **角色** | **說明** |
|:--- |:--- |
| 擁有者 |hello 擁有者角色允許存取 tooall 資源，以及包括提供存取 tooother 使用者、 群組和應用程式 toomanage hello 自動化帳戶的自動化帳戶內的動作。 |
| 參與者 |hello 參與者角色可讓您 toomanage 以外修改其他使用者的所有內容存取權限 tooan 自動化帳戶。 |
| 讀取者 |hello 讀取者角色可讓您 tooview 自動化中的所有 hello 資源帳戶，但無法進行任何變更。 |
| 自動化運算子 |hello 自動化操作員角色可讓您 tooperform 操作工作例如啟動、 停止、 暫停、 繼續和排程作業。 這個角色是如果您想要 tooprotect 您的自動化帳戶資源，例如認證資產和 runbook 進行檢視或修改很有幫助，但是仍然允許這些 runbook 的組織 tooexecute 成員。 |
| 使用者存取系統管理員 |hello 使用者存取系統管理員角色，可讓您 toomanage 使用者存取 tooAzure 自動化帳戶。 |

> [!NOTE]
> 您無法授與存取權限 tooa 特定 runbook 或 runbook，只 toohello 資源，以及在 hello 自動化帳戶內的動作。  
> 
> 

本文章中我們將逐步引導您在 Azure 自動化中的 RBAC 的向上 tooset。 但首先，讓我們來看得更仔細查看 hello 個別權限授與 toohello 參與者，讀取器、 自動化運算子和使用者存取系統管理員，讓我們取得之前授與任何人都了解 rights toohello 自動化帳戶。  否則，可能會造成非預期或不想要的結果。     

## <a name="contributor-role-permissions"></a>參與者角色權限
hello 下表顯示 hello 自動化中的 hello 參與者角色可以執行的特定動作。

| **資源類型** | **讀取** | **寫入** | **刪除** | **其他動作** |
|:--- |:--- |:--- |:--- |:--- |
| Azure 自動化帳戶 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |
| 自動化憑證資產 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |
| 自動化連線資產 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |
| 自動化連線類型資產 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |
| 自動化認證資產 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |
| 自動化排程資產 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |
| 自動化變數資產 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |
| 自動化期望狀態組態 | | | |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |
| Hybrid Runbook Worker 類型 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |
| Azure 自動化作業 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |
| 自動化作業串流 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 自動化作業排程 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |
| 自動化模組 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |
| Azure 自動化 Runbook |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |
| 自動化 Runbook 草稿 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |
| 自動化 Runbook 草稿測試作業 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |
| 自動化 Webhook |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |

## <a name="reader-role-permissions"></a>讀取者角色權限
hello 下表顯示 hello 可以在自動化中的 hello 讀取器角色所執行的特定動作。

| **資源類型** | **讀取** | **寫入** | **刪除** | **其他動作** |
|:--- |:--- |:--- |:--- |:--- |
| 傳統訂用帳戶管理員 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 管理鎖定 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 權限 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 提供者作業 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 角色指派 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 角色定義 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |

## <a name="automation-operator-role-permissions"></a>自動化操作員角色權限
hello 下表顯示 hello 可執行的自動化中的 hello 自動化操作員角色的特定動作。

| **資源類型** | **讀取** | **寫入** | **刪除** | **其他動作** |
|:--- |:--- |:--- |:--- |:--- |
| Azure 自動化帳戶 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 自動化憑證資產 | | | | |
| 自動化連線資產 | | | | |
| 自動化連線類型資產 | | | | |
| 自動化認證資產 | | | | |
| 自動化排程資產 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | |
| 自動化變數資產 | | | | |
| 自動化期望狀態組態 | | | | |
| Hybrid Runbook Worker 類型 | | | | |
| Azure 自動化作業 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |
| 自動化作業串流 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 自動化作業排程 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | |
| 自動化模組 | | | | |
| Azure 自動化 Runbook |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 自動化 Runbook 草稿 | | | | |
| 自動化 Runbook 草稿測試作業 | | | | |
| 自動化 Webhook | | | | |

如需詳細資訊，hello[自動化運算子動作](../active-directory/role-based-access-built-in-roles.md#automation-operator)清單 hello hello 自動化帳戶和其資源的 hello 自動化操作員角色所支援的動作。

## <a name="user-access-administrator-role-permissions"></a>使用者存取系統管理員角色權限
hello 下表顯示 hello hello 自動化中的使用者存取系統管理員角色可以執行的特定動作。

| **資源類型** | **讀取** | **寫入** | **刪除** | **其他動作** |
|:--- |:--- |:--- |:--- |:--- |
| Azure 自動化帳戶 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 自動化憑證資產 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 自動化連線資產 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 自動化連線類型資產 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 自動化認證資產 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 自動化排程資產 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 自動化變數資產 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 自動化期望狀態組態 | | | | |
| Hybrid Runbook Worker 類型 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Azure 自動化作業 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 自動化作業串流 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 自動化作業排程 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 自動化模組 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Azure 自動化 Runbook |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 自動化 Runbook 草稿 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 自動化 Runbook 草稿測試作業 |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 自動化 Webhook |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |

## <a name="configure-rbac-for-your-automation-account-using-azure-portal"></a>使用 Azure 入口網站為您的自動化帳戶設定 RBAC
1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)從 hello 自動化帳戶 刀鋒視窗中開啟您的自動化帳戶。  
2. 按一下 hello**存取**頂端 hello 右下角的控制項。 這會開啟 hello**使用者**刀鋒視窗可以讓您加入新的使用者、 群組和應用程式 toomanage 自動化帳戶，然後檢視現有的角色，可設定為 hello 自動化帳戶。  
   
   ![[存取] 按鈕](media/automation-role-based-access-control/automation-01-access-button.png)  

> [!NOTE]
> **訂用帳戶系統管理員 」** hello 預設使用者為已經存在。 hello 訂用帳戶系統管理員 」 的 active directory 群組包含 hello 服務給系統管理員和 co-administrator(s) Azure 訂用帳戶。 hello 服務管理員是 hello 的擁有者 Azure 訂用帳戶以及它的資源，而且會有 hello 擁有者角色繼承 hello 自動化帳戶太。 這表示 hello 存取**繼承**如**服務系統管理員和共同管理員**的訂用帳戶和它的**指派**針對所有 hello 其他使用者。 按一下**訂閱管理員**tooview 更詳細說明有關其權限。  
> 
> 

### <a name="add-a-new-user-and-assign-a-role"></a>加入新使用者並指派角色
1. 從 hello 使用者 刀鋒視窗中，按一下 **新增**tooopen hello**新增存取 刀鋒視窗**您可以在其中新增使用者、 群組或應用程式，並指派角色 toothem。  
   
   ![新增使用者](media/automation-role-based-access-control/automation-02-add-user.png)  
2. 從可用角色的 hello 清單中選取的角色。 我們將選擇 hello**讀取器**角色，但是您可以選擇任何 hello 可用的內建角色支援自動化帳戶或您已定義任何自訂角色。  
   
   ![選取角色](media/automation-role-based-access-control/automation-03-select-role.png)  
3. 按一下**將使用者新增**tooopen hello**將使用者新增**刀鋒視窗。 如果您新增任何使用者、 群組或應用程式 toomanage 列出您的訂用帳戶則這些使用者，並選取 tooadd 存取。 如果沒有列出任何使用者，或如果未列出您感興趣加入 hello 使用者再按一下**邀請**tooopen hello**邀請來賓**刀鋒視窗中，您可以在此邀請具有有效的 Microsoft 帳戶的使用者電子郵件地址，例如 Outlook.com、 OneDrive 或 Xbox Live Id。 一旦您已輸入 hello hello 使用者電子郵件地址，按一下 **選取**tooadd hello 使用者，然後按一下**確定**。 
   
   ![新增使用者](media/automation-role-based-access-control/automation-04-add-users.png)  
   
   現在您應該會看到新增的 hello 使用者 toohello**使用者**刀鋒視窗的 hello**讀取器**指派角色。  
   
   ![列出使用者](media/automation-role-based-access-control/automation-05-list-users.png)  
   
   您也可以指派角色 toohello 使用者從 hello**角色**刀鋒視窗。 
4. 按一下**角色**從 hello 使用者 刀鋒視窗 tooopen hello**角色 刀鋒視窗**。 您可以從這個刀鋒視窗中，檢視 hello hello 角色，hello 數目的使用者和群組指派 toothat 角色名稱。
   
    ![從 [使用者] 刀鋒視窗指派角色](media/automation-role-based-access-control/automation-06-assign-role-from-users-blade.png)  
   
   > [!NOTE]
   > 以角色為基礎的存取控制只可以在 hello 自動化帳戶層級設定，並不是在下列任何資源 hello 自動化帳戶。
   > 
   > 
   
    您可以指派多個角色 tooa 使用者、 群組或應用程式。 例如，如果我們加入 hello**自動化運算子**角色以及 hello**讀取者角色**toohello 使用者，然後他們可以檢視所有 hello 自動化資源，以及執行 hello runbook 工作。 您可以展開 hello 下拉式 tooview 的角色指派 toohello 使用者清單。  
   
    ![檢視多個角色](media/automation-role-based-access-control/automation-07-view-multiple-roles.png)  

### <a name="remove-a-user"></a>移除使用者
您可以移除 hello 人員不管理 hello 自動化帳戶或使用者不再適用於 hello 組織使用者的存取權限。 下列是 hello 步驟 tooremove 使用者： 

1. 從 hello**使用者**刀鋒視窗中，您想 tooremove 選取 hello 角色指派。
2. 按一下 hello**移除**hello 分派詳細資料 刀鋒視窗中的按鈕。
3. 按一下**是**tooconfirm 移除。 
   
   ![移除使用者](media/automation-role-based-access-control/automation-08-remove-users.png)  

## <a name="role-assigned-user"></a>角色指派的使用者
Tooa 角色指派的使用者登入時 tootheir 自動化帳戶，就可以看到 hello 清單中所列的擁有者 hello 帳戶**預設目錄**。 在自動化帳戶加入至訂單 tooview hello，它們必須切換 hello 預設目錄 toohello 擁有者的預設目錄。  

![預設目錄](media/automation-role-based-access-control/automation-09-default-directory-in-role-assigned-user.png)  

### <a name="user-experience-for-automation-operator-role"></a>自動化操作員角色的使用者經驗
當指派 toohello 自動化操作員角色檢視 hello 自動化帳戶指派給使用者，是時，他們可以只檢視 runbook 的 hello 清單時，runbook 作業和排程 hello 自動化帳戶中建立，但無法檢視其定義。 他們可以啟動、 停止、 暫停、 繼續或排程 hello runbook 工作。 hello 使用者不會有存取 tooother 自動化資源，例如混合式背景工作群組或 DSC 節點的組態。  

![沒有存取 tooresourcres](media/automation-role-based-access-control/automation-10-no-access-to-resources.png)  

當 hello 使用者按一下 hello runbook 時，hello tooview hello 來源，或編輯 hello runbook 的命令不提供為 hello 自動化操作員角色不允許存取 toothem。  

![沒有存取 tooedit runbook](media/automation-role-based-access-control/automation-11-no-access-to-edit-runbook.png)  

hello 使用者會有存取 tooview 和 toocreate 排程，但不是會存取 tooany 其他資產類型。  

![沒有存取 tooassets](media/automation-role-based-access-control/automation-12-no-access-to-assets.png)  

此使用者也不具與 runbook 相關聯的存取 tooview hello webhook

![沒有存取 toowebhooks](media/automation-role-based-access-control/automation-13-no-access-to-webhooks.png)  

## <a name="configure-rbac-for-your-automation-account-using-azure-powershell"></a>使用 Azure PowerShell 為您的自動化帳戶設定 RBAC
以角色為基礎的存取也可以設定的 tooan 自動化帳戶使用 hello 下列[Azure PowerShell cmdlet](../active-directory/role-based-access-control-manage-access-powershell.md)。

• [Get-AzureRmRoleDefinition](https://msdn.microsoft.com/library/mt603792.aspx) 會列出 Azure Active Directory 中可用的所有 RBAC 角色。 您可以使用這個命令以及 hello**名稱**屬性 toolist 所有 hello 可由特定角色執行的動作。  
    **範例：**  
    ![取得角色定義](media/automation-role-based-access-control/automation-14-get-azurerm-role-definition.png)  

• [Get AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt619413.aspx)清單在 hello Azure AD RBAC 角色指派指定的範圍。 如果沒有任何參數，此命令會傳回 hello 訂用帳戶底下所做的所有 hello 角色指派。 使用 hello **ExpandPrincipalGroups**參數 toolist 存取指派 hello 可讓您指定使用者，以及 hello 群組 hello 使用者是的成員。  
    **範例：**使用 hello 下列命令 toolist，hello 的所有使用者和其自動化帳戶內的角色。

    Get-AzureRMRoleAssignment -scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>” 

![取得角色指派](media/automation-role-based-access-control/automation-15-get-azurerm-role-assignment.png)

•[新增 AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt603580.aspx) tooassign 存取 toousers、 群組和應用程式 tooa 特定範圍內。  
    **範例：**使用 hello 下列命令 tooassign hello"自動化操作員 」 角色 hello 自動化帳戶的範圍中的使用者。

    New-AzureRmRoleAssignment -SignInName <sign-in Id of a user you wish toogrant access> -RoleDefinitionName "Automation operator" -Scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>”  

![新角色指派](media/automation-role-based-access-control/automation-16-new-azurerm-role-assignment.png)

• 使用[移除 AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt603781.aspx) tooremove 存取指定的使用者、 群組或從特定範圍的應用程式。  
    **範例：**使用 hello 下列命令 tooremove hello 使用者從 hello 自動化帳戶的範圍中的 hello"自動化操作員 」 角色。

    Remove-AzureRmRoleAssignment -SignInName <sign-in Id of a user you wish tooremove> -RoleDefinitionName "Automation Operator" -Scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>”

在上述範例 hello，取代**登入識別碼**，**訂用帳戶 Id**，**資源群組名稱**和**自動化帳戶名稱**與您帳戶詳細資料。 選擇**是**時提示 tooconfirm 才能繼續 tooremove 使用者角色指派。   

## <a name="next-steps"></a>後續步驟
* 如需不同的方式 tooconfigure RBAC Azure 自動化的資訊，請參閱太[管理使用 Azure PowerShell RBAC](../active-directory/role-based-access-control-manage-access-powershell.md)。
* 如需不同的方式 toostart runbook 的詳細資訊，請參閱[啟動 runbook](automation-starting-a-runbook.md)
* 如需不同的 runbook 類型資訊，請參閱太[Azure 自動化 runbook 類型](automation-runbook-types.md)

