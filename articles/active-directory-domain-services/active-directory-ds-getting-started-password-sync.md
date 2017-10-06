---
title: "Azure Active Directory Domain Services︰啟用密碼同步處理 | Microsoft Docs"
description: "開始使用 Azure Active Directory 網域服務"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 5a32a0df-a3ca-4ebe-b980-91f58f8030fc
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 8e073df9de2996f5ad159dda746881c014ea3d66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a>啟用密碼同步處理 tooAzure Active Directory 網域服務
在先前工作中，您已啟用 Azure Active Directory (Azure AD) 租用戶的 Azure Active Directory Domain Services。 hello 下一個工作是 tooenable 認證雜湊同步處理所需的 NT LAN Manager (NTLM) 和 Kerberos 驗證 tooAzure AD 網域服務。 您已設定認證同步處理之後，使用者可以登入 toohello 受管理的網域，利用其公司認證。

所需的 hello 步驟截然不同的僅限雲端的使用者帳戶與使用者帳戶從您使用 Azure AD Connect 的內部部署目錄同步。  必須有 Azure AD 租用戶的組合雲端唯一的使用者和使用者從您內部部署 AD 中，您需要 tooperform 這兩個步驟。

<br>

> [!div class="op_single_selector"]
> * **僅限雲端的使用者帳戶**:[為僅限雲端的使用者帳戶 tooyour 受管理的網域，同步處理密碼](active-directory-ds-getting-started-password-sync.md)
> * **在內部部署使用者帳戶**:[從您在內部同步處理的使用者帳戶的密碼同步處理 AD tooyour 管理網域](active-directory-ds-getting-started-password-sync-synced-tenant.md)
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-cloud-only-user-accounts"></a>工作 5： 啟用僅限雲端的使用者帳戶的密碼同步處理 tooyour 受管理的網域
hello tooauthenticate 使用者管理網域，Azure Active Directory 網域服務需要認證雜湊適合 NTLM 和 Kerberos 驗證的格式。 Azure AD 不會產生，或在 hello 格式所需 NTLM 或 Kerberos 驗證，直到您啟用 Azure Active Directory 網域服務租用戶中儲存認證雜湊。 基於明顯的安全性考量，Azure AD 也不會儲存任何純文字形式的密碼認證。 因此，Azure AD 並沒有產生這些的 NTLM 或 Kerberos 認證雜湊會根據使用者的現有認證的方式 tooautomatically。

> [!NOTE]
> 如果您的組織有僅限雲端的使用者帳戶，需要 toouse Azure Active Directory 網域服務的使用者必須變更其密碼。 僅限雲端的使用者帳戶是使用 hello Azure 入口網站或 Azure AD PowerShell cmdlet 在 Azure AD 目錄中已建立的帳戶。 這類使用者帳戶不是從內部部署目錄進行同步。
>
>

此密碼變更程序會導致 hello 認證所需的 Azure Active Directory 網域服務的 Kerberos 和 NTLM 驗證 toobe 在 Azure AD 中產生的雜湊。 您可以是過期 hello 密碼 hello 中的所有使用者的租用戶需要 toouse Azure Active Directory 網域服務，或指示他們 toochange 他們的密碼。

### <a name="enable-ntlm-and-kerberos-credential-hash-generation-for-a-cloud-only-user-account"></a>針對僅限雲端使用者帳戶啟用 NTLM 和 Kerberos 認證雜湊產生功能
以下是您需要 tooprovide 使用者，讓他們可以變更其密碼的 hello 指示：

1. 移 toohello [Azure AD 存取面板](http://myapps.microsoft.com)頁面為您的組織。

    ![啟動 hello Azure AD 存取面板](./media/active-directory-domain-services-getting-started/access-panel.png)

2. 在 hello 頂端的右上角，按一下 [您的名稱，選取**設定檔**hello 功能表。

    ![選取設定檔](./media/active-directory-domain-services-getting-started/select-profile.png)

3. 在 [hello**設定檔**頁面上，按一下**變更密碼**。

    ![按一下 [變更密碼]](./media/active-directory-domain-services-getting-started/user-change-password.png)

   > [!NOTE]
   > 如果 hello**變更密碼**選項不會顯示 hello 存取面板] 視窗中，請確認您的組織具有設定[Azure AD 中的密碼管理](../active-directory/active-directory-passwords-getting-started.md)。
   >
   >
4. 在 [hello**變更密碼**頁面上，輸入您現有的 （舊） 密碼，輸入新密碼，並加以確認。

    ![建立適用於 Azure AD 網域服務的虛擬網路。](./media/active-directory-domain-services-getting-started/user-change-password2.png)

5. 按一下 [提交] 。

幾分鐘後變更您的密碼，hello 新的密碼已使用 Azure Active Directory 網域服務中。 在數分鐘後 （通常約 20 分鐘），您可以登入 toocomputers 所聯結的 toohello 受管理的網域使用 hello 新變更的密碼。

## <a name="related-content"></a>相關內容
* [如何 tooupdate 您自己的密碼](../active-directory/active-directory-passwords-update-your-own-password.md)
* [在 Azure AD 中開始使用密碼管理](../active-directory/active-directory-passwords-getting-started.md)
* [啟用密碼同步處理 tooAzure Active Directory 網域服務同步處理的 Azure ad 租用戶](active-directory-ds-getting-started-password-sync-synced-tenant.md)
* [受 Azure Active Directory Domain Services 管理的網域](active-directory-ds-admin-guide-administer-domain.md)
* [加入 Windows 虛擬機器 tooan Azure Active Directory 網域服務受管理網域](active-directory-ds-admin-guide-join-windows-vm.md)
* [加入 Red Hat Enterprise Linux 虛擬機器 tooan Azure Active Directory 網域服務受管理網域](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
