---
title: "在 Azure 入口網站 hello aaaRole 型存取控制 |Microsoft 文件"
description: "快速入門中存取管理 hello Azure 入口網站中的 角色型存取控制。 使用角色指派 tooassign 權限 tooyour 資源。"
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 8078f366-a2c4-4fbb-a44b-fc39fd89df81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: b87e00089b0fc93fb212b318330a6f22bfbf59e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-access-tooyour-azure-subscription-resources"></a>使用角色型存取控制 toomanage 存取 tooyour Azure 訂用帳戶資源
> [!div class="op_single_selector"]
> * [使用者或群組管理存取](role-based-access-control-manage-assignments.md)
> * [資源管理存取](role-based-access-control-configure.md)

Azure 角色型存取控制 (RBAC) 可以對 Azure 進行更細緻的存取權管理。 使用 RBAC 時，您可以授與只 hello 少量的存取權，使用者需要 tooperform 他們的工作。 這篇文章可協助您立即執行 RBAC 與 hello Azure 入口網站中。 如果您需要有關 RBAC 如何協助您管理存取權的詳細資訊，請參閱 [什麼是角色型存取控制](role-based-access-control-what-is.md)。

在每個訂用帳戶，您可以授與向上 too2000 角色指派。 

## <a name="view-access"></a>檢視存取權
您可以查看誰存取 tooa 資源、 資源群組或從其主要刀鋒視窗的訂用帳戶中 hello [Azure 入口網站](https://portal.azure.com)。 例如，我們想要擁有我們的資源群組的存取 tooone toosee:

1. 選取**資源群組**hello hello 左側的導覽列中。  
    ![資源群組 - 圖示](./media/role-based-access-control-configure/resourcegroups_icon.png)
2. 選取 hello hello hello 資源群組名稱**資源群組**刀鋒視窗。
3. 選取**存取控制 (IAM)** hello 左側功能表中。  
4. hello 存取控制刀鋒視窗會列出所有使用者、 群組和已被授與存取 toohello 資源群組的應用程式。  
   
    ![使用者刀鋒視窗 - 繼承的存取權和指派的存取權螢幕擷取畫面](./media/role-based-access-control-configure/view-access.png)

請注意，某些角色的範圍太**此資源**有些則是**繼承**從另一個範圍內。 存取指派特別 toohello 資源群組，或繼承自指派 toohello 父訂用帳戶。

> [!NOTE]
> Hello 新 RBAC 模型中，以傳統訂用帳戶系統管理員和共同管理員會視為 hello 訂用帳戶的擁有者。

## <a name="add-access"></a>新增存取權
您授與從 hello 資源、 資源群組或訂用帳戶 hello hello 角色指派範圍內。

1. 選取**新增**hello 存取控制 刀鋒視窗。  
2. 您想從 hello tooassign 選取 hello 角色**選取角色**刀鋒視窗。
3. 選取您想 toogrant 存取您目錄中的 hello 使用者、 群組或應用程式。 您可以搜尋顯示名稱、 電子郵件地址與物件識別碼 hello 目錄。  
   
    ![新增使用者刀鋒視窗 - 搜尋螢幕擷取畫面](./media/role-based-access-control-configure/grant-access2.png)
4. 選取**確定**toocreate hello 分派。 hello**加入使用者**快顯視窗會追蹤 hello 進度。  
    ![新增使用者進度列 - 螢幕擷取畫面](./media/role-based-access-control-configure/addinguser_popup.png)

已成功加入之後的角色指派，它會出現在 hello**使用者**刀鋒視窗。

## <a name="remove-access"></a>移除存取權
1. 將游標停留 hello 分派的 tooremove hello 名稱。 核取方塊會顯示下一個 toohello 名稱。
2. 使用 hello 核取方塊 tooselect 一或多個角色指派。
2. 選取 [移除]。  
3. 選取**是**tooconfirm hello 移除。

無法移除已繼承的指派。 如果您需要 tooremove 繼承的指派，您會需要的 toodo 在 hello hello 角色指派建立所在的範圍。 在 [hello**範圍**資料行中下, 一步] 太**繼承**會帶您 toohello 資源已在指派給這個角色的連結。 請列於該處 toohello 資源移 tooremove hello 角色指派。

![使用者刀鋒視窗 - 繼承的存取存停用 [移除] 按鈕螢幕擷取畫面](./media/role-based-access-control-configure/remove-access2.png)

## <a name="other-tools-toomanage-access"></a>其他工具 toomanage 存取
您可以將角色指派和使用 Azure rbac 進行命令，在 hello Azure 入口網站以外的工具管理存取權。  遵循 hello 連結 toolearn 更多關於 hello 必要條件，並開始使用 hello Azure rbac 進行命令。

* [Azure PowerShell](role-based-access-control-manage-access-powershell.md)
* [Azure 命令列介面](role-based-access-control-manage-access-azure-cli.md)
* [REST API](role-based-access-control-manage-access-rest.md)

## <a name="next-steps"></a>後續步驟
* [建立存取權變更歷程記錄報告](role-based-access-control-access-change-history-report.md)
* 請參閱 hello [RBAC 內建的角色](role-based-access-built-in-roles.md)
* 定義您自己的 [Azure RBAC 中的自訂角色](role-based-access-control-custom-roles.md)

