---
title: "aaaCreate 自訂角色型存取控制角色並指派 toointernal 和在 Azure 中的外部使用者 |Microsoft 文件"
description: "將針對內部和外部使用者使用 PowerShell 和 CLI 所建立的自訂 RBAC 角色進行指派"
services: active-directory
documentationcenter: 
author: andreicradu
manager: catadinu
editor: kgremban
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/10/2017
ms.author: a-crradu
ms.openlocfilehash: 26793a66d6ca2f771338eed87d10ce2b3b431841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="intro-on-role-based-access-control"></a>角色型存取控制簡介

以角色為基礎的存取控制是 Azure 入口網站只功能允許 hello 訂用帳戶的擁有者 tooassign 細微角色 tooother 使用者可以在其環境中管理特定資源。

RBAC 可讓大型組織及 Smb 的較佳的安全性管理的外部共同作業者、 廠商或 freelancers 需要存取您的環境，但不是一定 toohello 整個基礎結構或任何 toospecific 資源計費相關的範圍。 RBAC 允許 hello 彈性擁有一個 hello 系統管理員帳戶 （服務在訂用帳戶層級的系統管理員角色） 所管理的 Azure 訂閱並擁有多個受邀使用者 toowork 下的 hello 相同訂用帳戶但不含任何系統管理它的權限。 從管理和計費的觀點而言，hello RBAC 功能證明 toobe 在各種情況中使用 Azure 的階段和管理有效選項。

## <a name="prerequisites"></a>必要條件
使用 RBAC hello Azure 環境中需要：

* 具有獨立的 Azure 訂用帳戶指派 toohello 使用者作為擁有者 （訂用帳戶的角色）
* 擁有 hello 的 hello Azure 訂用帳戶的擁有者角色
* 具有存取 toohello [Azure 入口網站](https://portal.azure.com)
* 請確定下列資源提供者的 toohave hello 註冊 hello 使用者訂用帳戶： **apiversion**。 如需有關如何 tooregister hello 資源提供者的詳細資訊，請參閱[資源管理員提供者、 區域、 應用程式開發介面版本和結構描述](/azure-resource-manager/resource-manager-supported-services.md)。

> [!NOTE]
> Office 365 訂閱或 Azure Active Directory 的授權 (例如： 存取 tooAzure Active Directory) hello O365 入口網站不品質使用 RBAC 佈建。

## <a name="how-can-rbac-be-used"></a>如何使用 RBAC
RBAC 在 Azure 中可套用於三個不同範圍。 從 hello 最高範圍 toohello 最低的其中一個，這些屬性，如下所示：

* 訂用帳戶 (最高)
* 資源群組
* 資源範圍 （hello 最低存取層級提供目標的權限 tooan 個別 Azure 資源的範圍）

## <a name="assign-rbac-roles-at-hello-subscription-scope"></a>將在 hello 訂用帳戶範圍 RBAC 角色指派
使用 RBAC 時，有兩個常見的範例 (但是不限於)︰

* 讓外部使用者從 hello 組織 （非 hello 系統管理使用者的 Azure Active Directory 租用戶的一部分），受邀 toomanage 特定資源或 hello 整個訂用帳戶
* Hello 組織 （它們是 hello 使用者的 Azure Active Directory 租用戶的一部分），但屬於不同的小組或需要細微的存取權限的群組內部使用者使用任一 toohello 整個訂用帳戶或 toocertain 資源群組或資源的範圍限制在 hello環境

## <a name="grant-access-at-a-subscription-level-for-a-user-outside-of-azure-active-directory"></a>為 Azure Active Directory 外部的使用者授與訂用帳戶等級的存取權
RBAC 角色可授與只由**擁有者**hello 訂用帳戶的因此 hello 系統管理使用者必須使用登已預先指派此角色，或建立 hello Azure 訂用帳戶的使用者名稱。

從 hello Azure 入口網站之後您, 登入為系統管理員，選取 「 訂閱 」 並選擇 hello 所需的其中一個。
![在 Azure 入口網站中的訂用帳戶] 刀鋒視窗](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png)根據預設，如果 hello [系統管理使用者已購買 hello Azure 訂用帳戶，hello 使用者會顯示為**帳戶管理員**，這個正在 hello 訂用帳戶角色。 如需有關 hello Azure 訂用帳戶的角色的詳細資訊，請參閱[hello 訂用帳戶或服務管理的新增或變更 Azure 系統管理員角色](/billing/billing-add-change-azure-subscription-administrator.md)。

在此範例中，hello 使用者 」alflanigan@outlook.com」 為 hello**擁有者**hello 「 免費試用版 」 的訂用帳戶中 hello AAD 租用戶 「 預設的 Azure 租用戶 」。 因為此使用者是 hello Azure 訂用帳戶以 hello hello 建立者的初始 Outlook 」 的 Microsoft 帳戶 (Microsoft 帳戶 = Outlook，Live 等) hello 預設加入此租用戶中的所有其他使用者的網域名稱將會**"@alflaniganuoutlook.onmicrosoft.com"**. 根據設計，hello 語法 hello 新網域的構成方式放在一起 hello 使用者名稱和網域名稱建立 hello 租用戶和新增 hello 延伸模組的 hello 使用者**"。 onmicrosoft.com"**。
此外，使用者可以登入與 hello 租用戶中的自訂網域名稱新增並驗證 hello 新租用戶後。 如需有關如何 tooverify 自訂網域名稱中的 Azure Active Directory 租用戶，請參閱[新增自訂網域名稱 tooyour 目錄](/active-directory/active-directory-add-domain)。

在此範例中，hello"預設租用戶 Azure"目錄包含只有具備 hello 網域名稱的使用者 」@alflanigan.onmicrosoft.com"。

Hello 系統管理使用者必須按一下 選取 hello 訂用帳戶之後,**存取控制 (IAM)**然後**加入新的角色**。





![Azure 入口網站中的存取控制 IAM 功能](./media/role-based-access-control-create-custom-roles-for-internal-external-users/1.png)





![在 Azure 入口網站的存取控制 IAM 功能中新增使用者](./media/role-based-access-control-create-custom-roles-for-internal-external-users/2.png)

hello 下一個步驟是 tooselect hello 角色 toobe 指派和 hello hello RBAC 角色會指派給使用者。 在 hello**角色**下拉式功能表 hello 系統管理使用者會看到只有 hello 內建 RBAC 角色在 Azure 中可用的。 如需每個角色及其可指派範圍的詳細說明，請參閱 [Azure 角色型存取控制的內建角色](/active-directory/role-based-access-built-in-roles.md)。

hello 系統管理使用者就必須 hello 外部使用者 tooadd hello 電子郵件地址。 hello 預期行為是讓 hello 外部使用者 toonot 都會顯示在現有的租用戶的 hello。 已邀請 hello 外部使用者之後，他會顯示在**訂用帳戶 > 存取控制 (IAM)**與 hello 目前所有的使用者目前指派的 RBAC 角色在 hello 訂用帳戶範圍。





![新增權限 toonew RBAC 角色](./media/role-based-access-control-create-custom-roles-for-internal-external-users/3.png)





![訂用帳戶等級的 RBAC 角色清單](./media/role-based-access-control-create-custom-roles-for-internal-external-users/4.png)

hello 使用者 」chessercarlton@gmail.com」 已受邀的 toobe**擁有者**hello 「 免費試用版 」 訂用帳戶。 在傳送嗨邀請之後, hello 外部使用者會收到電子郵件確認以啟用連結。
![RBAC 角色的電子郵件邀請](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)

由於外部 toohello 組織，hello 新使用者並沒有任何現有的屬性 hello"預設租用戶 Azure 」 的目錄中。 它們將在建立之後 hello 外部使用者已授與同意 toobe 記錄與他已被指派至角色 hello 訂用帳戶相關聯的 hello 目錄中。





![RBAC 角色的電子郵件邀請訊息](./media/role-based-access-control-create-custom-roles-for-internal-external-users/6.png)

顯示 hello 中當做外部使用者從現在起的 Azure Active Directory 租用戶的 hello 外部使用者，這可以在 hello Azure 入口網站和 hello 傳統入口網站中檢視。





![使用者刀鋒視窗 Azure Active Directory Azure 入口網站](./media/role-based-access-control-create-custom-roles-for-internal-external-users/7.png)





![使用者刀鋒視窗 Azure Active Directory Azure 傳統入口網站](./media/role-based-access-control-create-custom-roles-for-internal-external-users/8.png)

在 hello**使用者**可以辨識這兩個入口網站的 hello 外部使用者的檢視：

* hello Azure 入口網站中的 hello 不同的圖示類型
* hello 不同來源 hello 傳統入口網站中的點

不過，授與**擁有者**或**參與者**存取 tooan 外部使用者在 hello**訂用帳戶**範圍，不允許 hello 存取 toohello 系統管理使用者的目錄除非 hello**全域管理員**允許它。 Hello 使用者內容，在 hello**使用者類型**具有兩個一般參數，**成員**和**客體**可以識別。 成員是來賓時從外部來源的受邀使用者 toohello 目錄 hello 目錄中註冊的使用者。 如需詳細資訊，請參閱 [Azure Active Directory 系統管理員如何新增 B2B 共同作業使用者](/active-directory/active-directory-b2b-admin-add-users)。

> [!NOTE]
> 請確定輸入 hello 入口網站中的 hello 認證之後, hello 外部使用者選取 hello toosign 入正確的目錄。 hello 相同的使用者可以有存取 toomultiple 目錄和可以選取其中任一種按一下 hello 右上角中 hello Azure 入口網站中的 hello 使用者名稱，然後選擇 hello 適當目錄 hello 下拉式清單中。

同時會 hello 目錄中的客體，hello 外部使用者可以管理 hello Azure 的訂用帳戶的所有資源，但無法存取 hello 目錄。





![存取限制的 tooazure active directory 的 Azure 入口網站](./media/role-based-access-control-create-custom-roles-for-internal-external-users/9.png)

Azure Active Directory 和 Azure 訂用帳戶沒有父子式關聯性，如同其他 Azure 資源 (例如︰虛擬機器、虛擬網路、Web Apps、儲存體等) 與 Azure 訂用帳戶。 所有 hello 後者是建立、 管理和 Azure 訂用帳戶時使用的 toomanage hello 存取 tooan Azure 目錄，在 Azure 訂用帳戶計費。 如需詳細資訊，請參閱[如何為 Azure 訂用帳戶已相關的 tooAzure AD](/active-directory/active-directory-how-subscriptions-associated-directory)。

從所有的 hello 內建 RBAC 角色，**擁有者**和**參與者**tooall hello 環境、 差異為，參與者無法建立 hello 及 delete 中新的資源提供完整的管理存取RBAC 角色。 hello 其他內建角色，例如**虛擬機器參與者**提供完整的管理存取僅由 hello 名稱，不論 hello toohello 資源**資源群組**正在建立到。

指派 hello 內建 RBAC 的角色**虛擬機器參與者**在訂用帳戶層級中，表示該 hello 指派的使用者 hello 角色：

* 可以檢視所有虛擬機器不論其部署日期和 hello 資源群組的一部分
* Hello 訂用帳戶中有完整的管理存取 toohello 虛擬機器
* 無法檢視 hello 訂用帳戶中的任何其他資源類型
* 無法從計費觀點來操作任何變更

> [!NOTE]
> RBAC 正在 Azure 入口網站的唯一功能，它不會授與存取 toohello 傳統入口網站。

## <a name="assign-a-built-in-rbac-role-tooan-external-user"></a>指派給內建 RBAC 角色 tooan 外部使用者
在這項測試不同的狀況，如 hello 外部使用者 」alflanigan@gmail.com"會成為**虛擬機器參與者**。




![虛擬機器參與者內建角色](./media/role-based-access-control-create-custom-roles-for-internal-external-users/11.png)

hello 正常的行為，這個外部的使用者與此內建的角色是 toosee，以及管理只有虛擬機器和其相鄰資源管理員唯一所需資源部署時。 根據設計，這些限制的角色提供存取 hello Azure 入口網站中建立的唯一 tootheir 對應資源，無論某些仍然可以部署以及 hello 傳統的入口網站中 (例如： 虛擬機器)。





![Azure 入口網站中的虛擬機器參與者角色概觀](./media/role-based-access-control-create-custom-roles-for-internal-external-users/12.png)

## <a name="grant-access-at-a-subscription-level-for-a-user-in-hello-same-directory"></a>授與存取訂用帳戶層級中 hello 使用者相同的目錄
hello 程序並不相同 tooadding 外部使用者，同時從 hello 系統管理員觀點來看，授與 hello RBAC 角色，以及被授與存取 toohello 角色 hello 使用者。 此處 hello 差異是因為 hello 訂用帳戶內的所有 hello 資源範圍後，都即可使用 hello 儀表板中登入，該 hello 受邀使用者不會收到任何電子郵件邀請。

## <a name="assign-rbac-roles-at-hello-resource-group-scope"></a>將在 hello 資源群組範圍的 RBAC 角色指派
指派在 RBAC 角色**資源群組**範圍已指派 hello 角色在 hello 訂用帳戶層級，這兩種類型的使用者-外部或內部的相同程序 (hello 屬於相同的目錄)。 hello hello RBAC 角色所指派的使用者僅在其環境中的 toosee hello 資源群組已指派給這些存取從 hello**資源群組**hello Azure 入口網站中的圖示。

## <a name="assign-rbac-roles-at-hello-resource-scope"></a>將在 hello 資源範圍 RBAC 角色指派
指定於 Azure 中的資源範圍 RBAC 角色指派 hello 角色在 hello 訂用帳戶層級或 hello 資源群組層級的相同程序，下列 hello 相同這兩種案例的工作流程。 同樣地，hello hello RBAC 角色所指派之使用者可以看到只有 hello，它們有已指派給項目存取，可能是在 hello**所有資源** 索引標籤或直接在儀表板中。

RBAC 同時在資源群組範圍或資源範圍的一個重要環節是 hello 使用者 toomake 確定 toosign 單元 toohello 正確目錄。





![Azure 入口網站中的目錄登入](./media/role-based-access-control-create-custom-roles-for-internal-external-users/13.png)

## <a name="assign-rbac-roles-for-an-azure-active-directory-group"></a>為 Azure Active Directory 群組指派 RBAC 角色
所有在 hello 三個不同的範圍中的管理、 部署和管理各種資源與指派的使用者沒有 hello Azure 優惠 hello 權限使用 RBAC 的 hello 案例需要的管理個人的訂用帳戶。 不論 hello RBAC 角色指派給訂用帳戶、 資源群組或資源範圍，所有的 hello 資源上的其他使用者所建立的 hello 分派計費 hello 一個 Azure 訂用帳戶 hello 使用者有權存取的位置。 如此一來，hello 擁有計費的整個 Azure 訂用帳戶的系統管理員權限的使用者具有完整 hello 耗用量，不論概觀 hello 資源管理者。

對於較大的組織而言，您可以套用 RBAC 角色在 hello 考慮 hello 觀點來看該 hello 系統管理使用者的 Azure Active Directory 群組相同的方式想 toogrant hello 細微的存取權的小組或整個部門，不會個別針對每個使用者，因此考慮為極階段和管理有效選項。 tooillustrate 此範例中，hello**參與者**角色已加入 tooone 的 hello 群組中的 hello hello 訂用帳戶層級的租用戶。





![新增 AAD 群組的 RBAC 角色](./media/role-based-access-control-create-custom-roles-for-internal-external-users/14.png)

這些群組都是安全性群組，只在 Azure Active Directory 內進行佈建和管理。

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-powershell"></a>建立自訂的 RBAC 角色 tooopen 支援要求使用 PowerShell
hello 內建 RBAC 角色在 Azure 中可確保特定根據 hello hello 環境中的可用資源的權限層級。 不過，如果這些角色都不符合 hello 系統管理使用者的需求，是藉由建立自訂的 RBAC 角色更多的 hello 選項 toolimit 存取。

建立自訂的 RBAC 角色需要 tootake 一個內建角色並加以編輯，然後再將其匯回 hello 環境中。 使用 PowerShell 或 CLI 為管理 hello 下載和上傳的 hello 角色。

重要 toounderstand hello 必要條件建立自訂安全性角色可授與 hello 訂用帳戶層級更細微的存取並開啟支援要求的 hello 受邀使用者 hello 彈性也可讓它。

此範例中的 hello 內建角色**讀取器**可讓使用者存取 tooview 所有 hello 資源範圍但不是 tooedit 它們，或建立新的已自訂開啟支援要求的 tooallow hello 使用者 hello 選項。

hello 匯出 hello 的第一個動作**讀取器**角色需求 toobe 在 PowerShell 中完成系統管理員身分執行提高權限。

```
Login-AzureRMAccount

Get-AzureRMRoleDefinition -Name "Reader"

Get-AzureRMRoleDefinition -Name "Reader" | ConvertTo-Json | Out-File C:\rbacrole2.json

```





![讀取器 RBAC 角色的 PowerShell 螢幕擷取畫面](./media/role-based-access-control-create-custom-roles-for-internal-external-users/15.png)

然後，您需要 hello 角色 tooextract hello JSON 的範本。





![自訂讀取器 RBAC 角色的 JSON 範本](./media/role-based-access-control-create-custom-roles-for-internal-external-users/16.png)

典型的 RBAC 角色是由三個主要區段所組成︰**Actions**、**NotActions** 和 **AssignableScopes**。

在 hello**動作**區段會列出所有 hello 此角色允許的操作。 從資源提供者指派給每個動作的重要 toounderstand 它。 在此情況下，用於建立支援票證 hello **Microsoft.Support**必須列出資源提供者。

toobe 無法 toosee 所有 hello 可用和已註冊您的訂用帳戶中的資源提供者，您可以使用 PowerShell。
```
Get-AzureRMResourceProvider

```
此外，您可以檢查 hello 所有 hello 使用 PowerShell cmdlet toomanage hello 資源提供者。
    ![資源提供者管理的 PowerShell 螢幕擷取畫面](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)

所有 hello 特定 RBAC 角色，資源提供者會 hello 區段底下所列的動作 toorestrict **NotActions**。
最後，是強制性該 hello RBAC 角色包含 hello 明確訂用帳戶 Id 使用的位置。 hello 訂用帳戶 Id 列在 hello **AssignableScopes**，否則您不能 tooimport hello 角色在您的訂用帳戶。

之後建立和自訂 hello RBAC 角色時，它需要 toobe 匯入後的 hello 環境。

```
New-AzureRMRoleDefinition -InputFile "C:\rbacrole2.json"

```

在此範例中，hello 自訂此 RBAC 角色名稱會是 「 讀取器支援票證的存取層級 」 hello 訂用帳戶以及 tooopen 支援要求中的所有項目允許 hello 使用者 tooview。

> [!NOTE]
> hello 只有兩個內建 RBAC 角色允許的開啟支援要求的 hello 動作是**擁有者**和**參與者**。 對於使用者 toobe tooopen 無法支援要求，他必須為指派 RBAC 角色只在 hello 訂用帳戶範圍，因為根據 Azure 訂用帳戶建立支援的所有要求。

這個新的自訂角色指派給 hello tooan 使用者相同的目錄。





![匯入 hello Azure 入口網站中的自訂 RBAC 角色的螢幕擷取畫面](./media/role-based-access-control-create-custom-roles-for-internal-external-users/18.png)





![螢幕擷取畫面的指派中 hello 自訂匯入的 RBAC 角色 toouser 相同的目錄](./media/role-based-access-control-create-custom-roles-for-internal-external-users/19.png)





![自訂匯入的 RBAC 角色之權限的螢幕擷取畫面](./media/role-based-access-control-create-custom-roles-for-internal-external-users/20.png)

hello 範例已進一步詳細的 tooemphasize hello 限制這個自訂的 RBAC 角色，如下所示：
* 可以建立新的支援要求
* 無法建立新的資源範圍 (例如︰虛擬機器)
* 無法建立新的資源群組





![建立支援要求之自訂 RBAC 角色的螢幕擷取畫面](./media/role-based-access-control-create-custom-roles-for-internal-external-users/21.png)





![螢幕擷取畫面的自訂 RBAC 角色無法 toocreate Vm](./media/role-based-access-control-create-custom-roles-for-internal-external-users/22.png)





![螢幕擷取畫面的自訂 RBAC 角色無法 toocreate 新 RGs](./media/role-based-access-control-create-custom-roles-for-internal-external-users/23.png)

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-azure-cli"></a>建立自訂的 RBAC 角色 tooopen 支援使用 Azure CLI 要求
執行在 Mac 上，而不需要存取 tooPowerShell，Azure CLI 是 hello 方式 toogo。

hello 步驟 toocreate 自訂安全性角色都是相同的與 hello 唯一例外狀況，使用 CLI hello 角色無法在下載 JSON 範本，但它可以在檢視 hello CLI hello。

此範例中，我已選擇 hello 的內建角色**備份讀取器**。

```

azure role show "backup reader" --json

```





![備份讀取器角色顯示的 CLI 螢幕擷取畫面](./media/role-based-access-control-create-custom-roles-for-internal-external-users/24.png)

編輯 Visual Studio 中的 hello 角色 JSON 範本中複製 hello 內容之後，hello **Microsoft.Support**資源提供者已新增在 hello**動作**區段，讓這位使用者可以開啟但仍繼續 toobe hello 備份保存庫的讀取器的支援要求。 一次是必要 tooadd hello 訂用帳戶 ID，此角色將會使用 hello **AssignableScopes** > 一節。

```

azure role create --inputfile <path>

```





![匯入自訂 RBAC 角色的 CLI 螢幕擷取畫面](./media/role-based-access-control-create-custom-roles-for-internal-external-users/25.png)

hello 新角色現已推出 hello Azure 入口網站和 hello assignation 程序是 hello 相同如 hello 先前範例所示。





![使用 CLI 1.0 所建立之自訂 RBAC 角色的 Azure 入口網站螢幕擷取畫面](./media/role-based-access-control-create-custom-roles-for-internal-external-users/26.png)

最新組建 2017，hello Azure 雲端殼層 hello 為上市。 Azure 雲端殼層是補數 tooIDE 和 hello Azure 入口網站。 您可以利用此服務，取得經過驗證且裝載於 Azure 內以瀏覽器為基礎的殼層，您可以使用它而不使用安裝在您電腦上的 CLI。





![Azure Cloud Shell](./media/role-based-access-control-create-custom-roles-for-internal-external-users/27.png)
