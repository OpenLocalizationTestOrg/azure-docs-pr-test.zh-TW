---
title: "aaaAdd 擁有者和使用者在 Azure DevTest Labs |Microsoft 文件"
description: "在 Azure DevTest Labs 使用 hello Azure 入口網站或 PowerShell 加入擁有者和使用者"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 4f51d9a5-2702-45f0-a2d5-a3635b58c416
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 2a98f5fe1efbd7c23e0d97f58f47c37462aed3b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a>在 Azure DevTest Labs 中新增擁有者和使用者
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

Azure DevTest Labs 的存取權是由 [Azure 角色型存取控制 (RBAC)](../active-directory/role-based-access-control-what-is.md)所控制。 使用 RBAC 時，您可以分隔責任至您小組內*角色*您授與只能存取必要 toousers tooperform hello 量他們的工作。 這些 RBAC 角色的其中三個分別是*擁有者*、*DevTest Labs 使用者*和*參與者*。 在本文中，您學會中每個 hello 三個主要 RBAC 角色可以執行的動作。 您了解從該處，同時透過 hello tooadd 使用者 tooa 實驗室-如何入口網站與透過 PowerShell 指令碼，和如何 tooadd 使用者在 hello 訂用帳戶層級。

## <a name="actions-that-can-be-performed-in-each-role"></a>可在每個角色執行的動作
您可以對使用者指派三個主要角色︰

* 擁有者
* DevTest Labs 使用者
* 參與者

hello 下表說明每個角色中的使用者可以執行的 hello 動作：

| **此角色中的使用者可以執行的動作** | **DevTest Labs 使用者** | **擁有者** | **參與者** |
| --- | --- | --- | --- |
| **實驗室工作** | | | |
| 加入使用者 tooa 實驗室 |否 |是 |否 |
| 更新成本設定 |否 |是 |是 |
| **VM 的基本工作** | | | |
| 新增和移除自訂映像 |否 |是 |是 |
| 新增、更新和刪除公式 |是 |是 |是 |
| 將 Azure Marketplace 映像加入白名單 |否 |是 |是 |
| **VM 工作** | | | |
| 建立 VM |是 |是 |是 |
| 啟動、停止和刪除 VM |Hello 使用者所建立的 Vm |是 |是 |
| 更新 VM 原則 |否 |是 |是 |
| 在 VM 中新增/移除資料磁碟 |Hello 使用者所建立的 Vm |是 |是 |
| **構件工作** | | | |
| 新增和移除構件儲存機制 |否 |是 |是 |
| 套用構件 |是 |是 |是 |

> [!NOTE]
> 當使用者建立的 VM 時，該使用者會自動指派 toohello**擁有者**hello 建立 VM 角色。
> 
> 

## <a name="add-an-owner-or-user-at-hello-lab-level"></a>在 hello 實驗室層級加入擁有者或使用者
擁有者和使用者可以加入層級 hello 實驗室透過 hello Azure 入口網站。 這包括擁有有效 [Microsoft 帳戶 (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account)的外部使用者。
hello 步驟會引導您加入的擁有者或使用者 tooa 實驗室中 Azure DevTest Labs hello 程序：

1. 登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。
2. 選取**更多服務**，然後選取**DevTest Labs**從 hello 清單。
3. 從 hello 清單的實驗室中，選取 hello 所需的實驗室。
4. 在 hello 實驗室刀鋒視窗中，選取 **組態**。 
5. 在 hello**組態**刀鋒視窗中，選取**使用者**。
6. 在 hello**使用者**刀鋒視窗中，選取**+ 加**。
   
    ![新增使用者](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
7. 在 hello**選取角色**刀鋒視窗中，選取 hello 所需的角色。 hello 區段[可在每個角色執行的動作](#actions-that-can-be-performed-in-each-role)清單 hello hello 擁有者、 DevTest 使用者和參與者角色中的可執行各種動作。
8. 在 hello**將使用者新增**刀鋒視窗中，輸入 hello 電子郵件地址或您想要在您指定的 hello 角色 tooadd hello 使用者名稱。 如果找不到 hello 使用者，錯誤訊息，說明 hello 問題。 如果找到 hello 使用者，則會列出該使用者，並選取。 
9. 選取 [選取] 。
10. 選取**確定**tooclose hello**新增存取**刀鋒視窗。
11. 當您傳回 toohello**使用者**刀鋒視窗中，已新增 hello 使用者。  

## <a name="add-an-external-user-tooa-lab-using-powershell"></a>新增外部使用者 tooa 實驗室使用 PowerShell
此外 tooadding hello Azure 入口網站中的使用者，您可以新增要使用 PowerShell 指令碼的外部使用者 tooyour 實驗室。 在 hello 遵循範例中，只需修改 hello 參數值在 hello**值 toochange**註解。
您可以擷取 hello `subscriptionId`， `labResourceGroup`，和`labName`hello Azure 入口網站中的 hello 實驗室刀鋒視窗中的值。

> [!NOTE]
> hello 範例指令碼會假設該 hello 指定的使用者都已經加入成為客體 toohello Active Directory，和如果不是 hello 案例將會失敗。 tooadd 使用者不在 hello Active Directory tooa 實驗室中，使用 hello Azure 入口網站 tooassign hello 使用者 tooa 角色 hello 區段中所示[hello 實驗室層級加入擁有者或使用者](#add-an-owner-or-user-at-the-lab-level)。   
> 
> 

    # Add an external user in DevTest Labs user role tooa lab
    # Ensure that guest users can be added toohello Azure Active directory:
    # https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values toochange
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Login-AzureRmAccount

    # Select hello Azure subscription that contains hello lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve hello user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create hello role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-hello-subscription-level"></a>在 hello 訂用帳戶層級加入擁有者或使用者
在 Azure 中的父範圍 toochild 範圍從傳播 azure 權限。 因此，包含實驗室之 Azure 訂用帳戶的擁有者會自動成為這些實驗室的擁有者。 他們也擁有 hello Vm 和 hello 實驗室的使用者和 hello Azure DevTest Labs 服務所建立的其他資源。 

您可以加入其他擁有者 tooa 實驗室透過 hello 實驗室刀鋒視窗中 hello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。 不過，hello 加入擁有者的系統管理範圍是較窄比 hello 訂用帳戶擁有者的範圍。 例如，hello 加入擁有者不需要完整存取 toosome 的 hello 資源建立 hello 訂用帳戶中的 hello DevTest Labs 服務。 

tooadd 擁有者 tooan Azure 訂用帳戶，請遵循下列步驟：

1. 登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。
2. 選取**更服務**，然後選取**訂閱**從 hello 清單。
3. 選取所需的 hello 訂用帳戶。
4. 選取 [存取]  圖示。 
   
    ![存取使用者](./media/devtest-lab-add-devtest-user/access-users.png)
5. 在 hello**使用者**刀鋒視窗中，選取**新增**。
   
    ![新增使用者](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. 在 hello**選取角色**刀鋒視窗中，選取**擁有者**。
7. 在 hello**將使用者新增**刀鋒視窗中，輸入 hello 電子郵件地址或名稱要的 hello 使用者作為擁有者 tooadd。 如果找不到 hello 使用者，您會取得錯誤訊息，說明 hello 問題。 如果找到 hello 使用者，該使用者列在 hello**使用者**文字方塊。
8. 選取 hello 所在的使用者名稱。
9. 選取 [選取] 。
10. 選取**確定**tooclose hello**新增存取**刀鋒視窗。
11. 當您傳回 toohello**使用者**刀鋒視窗中，已新增 hello 使用者作為擁有者。 此使用者現在是任何實驗室建立這個訂用帳戶，底下的擁有者，並因此可能無法 tooperform 擁有者工作。 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

