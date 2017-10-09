---
title: "aaaMicrosoft Azure 多重要素驗證的使用者狀態"
description: "了解 Azure MFA 中的使用者狀態"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 0b9fde23-2d36-45b3-950d-f88624a68fbd
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: cf5b977b09d09330b7b3bc668abd79e602d62015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorequire-two-step-verification-for-a-user-or-group"></a>如何 toorequire 雙步驟驗證的使用者或群組

可供您要求使用雙步驟驗證的方法有兩種。 hello 第一個選項是 tooenable 每個個別使用者的 Azure Multi-factor Authentication (MFA)。 當使用者分別啟用時，它們一定會執行 （有一些例外，像是登入來自受信任的 IP 位址時，或記住 hello 開啟裝置的功能） 的雙步驟驗證。 hello 第二個選項是 tooset 建立需要兩步驟驗證，在某些情況下的條件式存取原則。

>[!TIP] 
>選擇其中一個這些方法 toorequire 雙步驟驗證，不可同時為兩者。 為使用者啟用 Azure MFA 的效力會凌駕任何條件式存取原則。

## <a name="which-option-is-right-for-you"></a>您合適的選項

**藉由變更使用者狀態啟用 Azure MFA**是 hello 要求雙步驟驗證的傳統方式。 它適用於這兩個 hello 雲端中的 Azure MFA 和 Azure MFA Server。 您所啟用的所有 hello 使用者都擁有 hello 相同的體驗，每次登入時會 tooperform 雙步驟驗證。 啟用使用者的效力會凌駕任何可能影響該使用者的條件式存取原則。 

**使用條件式存取原則來啟用 Azure MFA** 是用來要求使用雙步驟驗證的更彈性方法。 它只是，適用於 hello 雲端中的 Azure MFA 和條件式存取是[付費功能的 Azure Active Directory](https://www.microsoft.com/cloud-platform/azure-active-directory-features)。 您可以建立適用於 toogroups 與個別使用者的條件式存取原則。 您可以對高風險群組施加比低風險群組更多的限制，或者，也可以只針對高風險雲端應用程式要求雙步驟驗證，至於低風險的雲端應用程式則略過雙步驟驗證。 

這兩個選項會提示使用者 tooregister Azure Multi-factor Authentication hello 之後 hello 需求開啟登入的第一次。 這兩個選項也會使用可設定的 hello [Azure Multi-factor Authentication 設定](multi-factor-authentication-whats-next.md)

## <a name="enable-azure-mfa-by-changing-user-status"></a>藉由變更使用者狀態來啟用 Azure MFA

Azure Multi-factor Authentication Server 中的使用者帳戶具有下列三種不同狀態的 hello:

| 狀態 | 說明 | 受影響的非瀏覽器應用程式 |
|:---:|:---:|:---:|
| 已停用 |hello 預設狀態之新使用者未註冊 Azure Multi-factor Authentication (MFA)。 |否 |
| 已啟用 |hello 使用者已註冊 Azure MFA，但尚未註冊。 會將其下一次登入時提示的 tooregister hello。 |否。  Hello 註冊程序完成之前，他們可以繼續 toowork。 |
| 已強制 |hello 使用者已註冊且已完成 Azure MFA hello 註冊程序。 |是。  應用程式需要應用程式密碼。 |

使用者的狀態會反映是否為系統管理員具有它們在註冊 Azure MFA，以及他們是否完成 hello 註冊程序。

所有使用者一開始都是「已停用」狀態。 當您在 Azure MFA 中註冊使用者時，他們的狀態會變更為「已啟用」。 啟用的使用者登入並完成 hello 註冊程序，其狀態會變更太*強制執行*。  

### <a name="view-hello-status-for-a-user"></a>檢視使用者的 hello 狀態

使用下列步驟 tooaccess hello 頁面供您檢視及管理使用者狀態的 hello:

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)身為系統管理員。
2. 跳過**Azure Active Directory** > **使用者和群組** > **所有使用者**。
3. 選取 [多重要素驗證]。
   ![選取 Multi-Factor Authentication](./media/multi-factor-authentication-get-started-user-states/selectmfa.png)
4. 新的頁面上，顯示 hello 使用者狀態時，隨即開啟。
   ![Multi-Factor Authentication 使用者狀態 - 螢幕擷取畫面](./media/multi-factor-authentication-get-started-user-states/userstate1.png)

### <a name="change-hello-status-for-a-user"></a>變更使用者的 hello 狀態

1. 使用上述步驟 tooget toohello multi-factor authentication 使用者頁面的 hello。
2. 您為 Azure MFA 想 tooenable 尋找 hello 使用者。 您可能需要 toochange hello hello 頂端的檢視。 
   ![尋找使用者 - 螢幕擷取畫面](./media/multi-factor-authentication-get-started-cloud/enable1.png)
3. 請檢查 hello 方塊下一步 tootheir 名稱。
4. 在 hello 右下快速步驟，選擇**啟用**或**停用**。
   ![啟用所選的使用者 - 螢幕擷取畫面](./media/multi-factor-authentication-get-started-cloud/user1.png)

   >[!TIP]
   >*啟用*使用者自動切換太*強制執行*當他們註冊為 Azure MFA。 您不應手動變更 hello 使用者狀態 tooenforced。 

5. 確認您的選擇會開啟 hello 快顯視窗中。 

當您啟用使用者之後，應透過電子郵件通知他們。 告訴他們，則會要求他們 tooregister hello 登入時的下一次。 此外，如果您的組織使用不支援新式驗證的非瀏覽器應用程式，其需要 toocreate 應用程式密碼。 您也可以包含連結 tooour [Azure MFA 使用者指南](./end-user/multi-factor-authentication-end-user.md)toohelp 它們開始。

### <a name="use-powershell"></a>使用 PowerShell
toochange hello 使用者狀態的狀態使用[Azure AD PowerShell](/powershell/azure/overview)，變更`$st.State`。 有三個可能的狀態︰

* 已啟用
* 已強制
* 已停用  

不會移到使用者直接 toohello*強制*狀態。 非瀏覽器型應用程式將會停止運作，因為 hello 使用者未通過 MFA 註冊並取得[應用程式密碼](multi-factor-authentication-whats-next.md#app-passwords)。 

使用 PowerShell 是一個不錯的選項，當您需要讓使用者 toobulk。 建立會在使用者清單中循環移動並啟用這些使用者的 PowerShell 指令碼：

        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName bsimon@contoso.com -StrongAuthenticationRequirements $sta

下列是一個範例：

    $users = "bsimon@contoso.com","jsmith@contoso.com","ljacobson@contoso.com"
    foreach ($user in $users)
    {
        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName $user -StrongAuthenticationRequirements $sta
    }

## <a name="enable-azure-mfa-with-a-conditional-access-policy"></a>使用條件式存取原則來啟用 Azure MFA

條件式存取是 Azure Active Directory 的付費功能，其具有許多可能的設定選項。 這些步驟逐步其中一種方式 toocreate 原則。 如需詳細資訊，請參閱 [Azure Active Directory 中的條件式存取](../active-directory/active-directory-conditional-access-azure-portal.md)。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)身為系統管理員。
2. 跳過**Azure Active Directory** > **條件式存取**。
3. 選取 [新增原則]。
4. 在 [指派] 底下選取 [使用者和群組]。 使用 hello **Include**和**排除**toospecify hello 原則將管理哪些使用者和群組的索引標籤。
5. 在 [指派] 底下選取 [雲端應用程式]。 選擇 tooinclude**所有雲端應用程式**。
6. 在 [存取控制] 底下選取 [授與]。 選擇 [需要多重要素驗證]。
7. 開啟**啟用原則**太**上**，然後選取 **儲存**。

hello hello 條件式存取原則中的其他選項可讓您 toospecify 應該是必要的雙步驟驗證的確切時間。 例如，您可以進行原則，指出： 當約聘人員嘗試 tooaccess 我們採購的應用程式從未加入網域的裝置上不受信任網路時，需要兩步驟驗證。 

## <a name="next-steps"></a>後續步驟

- 取得秘訣 hello[條件式存取的最佳做法](../active-directory/active-directory-conditional-access-best-practices.md)

- 管理[您的使用者和其裝置](multi-factor-authentication-manage-users-and-devices.md)的 Multi-Factor Authentication 設定