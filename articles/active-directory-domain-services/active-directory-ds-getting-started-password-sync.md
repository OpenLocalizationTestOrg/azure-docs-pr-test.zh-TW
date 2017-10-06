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
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a><span data-ttu-id="8effb-103">啟用密碼同步處理 tooAzure Active Directory 網域服務</span><span class="sxs-lookup"><span data-stu-id="8effb-103">Enable password synchronization tooAzure Active Directory Domain Services</span></span>
<span data-ttu-id="8effb-104">在先前工作中，您已啟用 Azure Active Directory (Azure AD) 租用戶的 Azure Active Directory Domain Services。</span><span class="sxs-lookup"><span data-stu-id="8effb-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="8effb-105">hello 下一個工作是 tooenable 認證雜湊同步處理所需的 NT LAN Manager (NTLM) 和 Kerberos 驗證 tooAzure AD 網域服務。</span><span class="sxs-lookup"><span data-stu-id="8effb-105">hello next task is tooenable synchronization of credential hashes required for NT LAN Manager (NTLM) and Kerberos authentication tooAzure AD Domain Services.</span></span> <span data-ttu-id="8effb-106">您已設定認證同步處理之後，使用者可以登入 toohello 受管理的網域，利用其公司認證。</span><span class="sxs-lookup"><span data-stu-id="8effb-106">After you've set up credential synchronization, users can sign in toohello managed domain with their corporate credentials.</span></span>

<span data-ttu-id="8effb-107">所需的 hello 步驟截然不同的僅限雲端的使用者帳戶與使用者帳戶從您使用 Azure AD Connect 的內部部署目錄同步。</span><span class="sxs-lookup"><span data-stu-id="8effb-107">hello steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span>  <span data-ttu-id="8effb-108">必須有 Azure AD 租用戶的組合雲端唯一的使用者和使用者從您內部部署 AD 中，您需要 tooperform 這兩個步驟。</span><span class="sxs-lookup"><span data-stu-id="8effb-108">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need tooperform both steps.</span></span>

<br>

> [!div class="op_single_selector"]
> * <span data-ttu-id="8effb-109">**僅限雲端的使用者帳戶**:[為僅限雲端的使用者帳戶 tooyour 受管理的網域，同步處理密碼](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="8effb-109">**Cloud-only user accounts**: [Synchronize passwords for cloud-only user accounts tooyour managed domain](active-directory-ds-getting-started-password-sync.md)</span></span>
> * <span data-ttu-id="8effb-110">**在內部部署使用者帳戶**:[從您在內部同步處理的使用者帳戶的密碼同步處理 AD tooyour 管理網域](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="8effb-110">**On-premises user accounts**: [Synchronize passwords for user accounts synced from your on-premises AD tooyour managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span>
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-cloud-only-user-accounts"></a><span data-ttu-id="8effb-111">工作 5： 啟用僅限雲端的使用者帳戶的密碼同步處理 tooyour 受管理的網域</span><span class="sxs-lookup"><span data-stu-id="8effb-111">Task 5: enable password synchronization tooyour managed domain for cloud-only user accounts</span></span>
<span data-ttu-id="8effb-112">hello tooauthenticate 使用者管理網域，Azure Active Directory 網域服務需要認證雜湊適合 NTLM 和 Kerberos 驗證的格式。</span><span class="sxs-lookup"><span data-stu-id="8effb-112">tooauthenticate users on hello managed domain, Azure Active Directory Domain Services needs credential hashes in a format that's suitable for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="8effb-113">Azure AD 不會產生，或在 hello 格式所需 NTLM 或 Kerberos 驗證，直到您啟用 Azure Active Directory 網域服務租用戶中儲存認證雜湊。</span><span class="sxs-lookup"><span data-stu-id="8effb-113">Azure AD does not generate or store credential hashes in hello format that's required for NTLM or Kerberos authentication, until you enable Azure Active Directory Domain Services for your tenant.</span></span> <span data-ttu-id="8effb-114">基於明顯的安全性考量，Azure AD 也不會儲存任何純文字形式的密碼認證。</span><span class="sxs-lookup"><span data-stu-id="8effb-114">For obvious security reasons, Azure AD also does not store any password credentials in clear-text form.</span></span> <span data-ttu-id="8effb-115">因此，Azure AD 並沒有產生這些的 NTLM 或 Kerberos 認證雜湊會根據使用者的現有認證的方式 tooautomatically。</span><span class="sxs-lookup"><span data-stu-id="8effb-115">Therefore, Azure AD does not have a way tooautomatically generate these NTLM or Kerberos credential hashes based on users' existing credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="8effb-116">如果您的組織有僅限雲端的使用者帳戶，需要 toouse Azure Active Directory 網域服務的使用者必須變更其密碼。</span><span class="sxs-lookup"><span data-stu-id="8effb-116">If your organization has cloud-only user accounts, users who need toouse Azure Active Directory Domain Services must change their passwords.</span></span> <span data-ttu-id="8effb-117">僅限雲端的使用者帳戶是使用 hello Azure 入口網站或 Azure AD PowerShell cmdlet 在 Azure AD 目錄中已建立的帳戶。</span><span class="sxs-lookup"><span data-stu-id="8effb-117">A cloud-only user account is an account that was created in your Azure AD directory using either hello Azure portal or Azure AD PowerShell cmdlets.</span></span> <span data-ttu-id="8effb-118">這類使用者帳戶不是從內部部署目錄進行同步。</span><span class="sxs-lookup"><span data-stu-id="8effb-118">Such user accounts aren't synchronized from an on-premises directory.</span></span>
>
>

<span data-ttu-id="8effb-119">此密碼變更程序會導致 hello 認證所需的 Azure Active Directory 網域服務的 Kerberos 和 NTLM 驗證 toobe 在 Azure AD 中產生的雜湊。</span><span class="sxs-lookup"><span data-stu-id="8effb-119">This password change process causes hello credential hashes that are required by Azure Active Directory Domain Services for Kerberos and NTLM authentication toobe generated in Azure AD.</span></span> <span data-ttu-id="8effb-120">您可以是過期 hello 密碼 hello 中的所有使用者的租用戶需要 toouse Azure Active Directory 網域服務，或指示他們 toochange 他們的密碼。</span><span class="sxs-lookup"><span data-stu-id="8effb-120">You can either expire hello passwords for all users in hello tenant who need toouse Azure Active Directory Domain Services or instruct them toochange their passwords.</span></span>

### <a name="enable-ntlm-and-kerberos-credential-hash-generation-for-a-cloud-only-user-account"></a><span data-ttu-id="8effb-121">針對僅限雲端使用者帳戶啟用 NTLM 和 Kerberos 認證雜湊產生功能</span><span class="sxs-lookup"><span data-stu-id="8effb-121">Enable NTLM and Kerberos credential hash generation for a cloud-only user account</span></span>
<span data-ttu-id="8effb-122">以下是您需要 tooprovide 使用者，讓他們可以變更其密碼的 hello 指示：</span><span class="sxs-lookup"><span data-stu-id="8effb-122">Here are hello instructions you need tooprovide users, so they can change their passwords:</span></span>

1. <span data-ttu-id="8effb-123">移 toohello [Azure AD 存取面板](http://myapps.microsoft.com)頁面為您的組織。</span><span class="sxs-lookup"><span data-stu-id="8effb-123">Go toohello [Azure AD Access Panel](http://myapps.microsoft.com) page for your organization.</span></span>

    ![啟動 hello Azure AD 存取面板](./media/active-directory-domain-services-getting-started/access-panel.png)

2. <span data-ttu-id="8effb-125">在 hello 頂端的右上角，按一下 [您的名稱，選取**設定檔**hello 功能表。</span><span class="sxs-lookup"><span data-stu-id="8effb-125">In hello top right corner, click on your name and select **Profile** from hello menu.</span></span>

    ![選取設定檔](./media/active-directory-domain-services-getting-started/select-profile.png)

3. <span data-ttu-id="8effb-127">在 [hello**設定檔**頁面上，按一下**變更密碼**。</span><span class="sxs-lookup"><span data-stu-id="8effb-127">On hello **Profile** page, click on **Change password**.</span></span>

    ![按一下 [變更密碼]](./media/active-directory-domain-services-getting-started/user-change-password.png)

   > [!NOTE]
   > <span data-ttu-id="8effb-129">如果 hello**變更密碼**選項不會顯示 hello 存取面板] 視窗中，請確認您的組織具有設定[Azure AD 中的密碼管理](../active-directory/active-directory-passwords-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="8effb-129">If hello **Change password** option is not displayed in hello Access Panel window, ensure that your organization has configured [password management in Azure AD](../active-directory/active-directory-passwords-getting-started.md).</span></span>
   >
   >
4. <span data-ttu-id="8effb-130">在 [hello**變更密碼**頁面上，輸入您現有的 （舊） 密碼，輸入新密碼，並加以確認。</span><span class="sxs-lookup"><span data-stu-id="8effb-130">On hello **change password** page, type your existing (old) password, type a new password, and then confirm it.</span></span>

    ![建立適用於 Azure AD 網域服務的虛擬網路。](./media/active-directory-domain-services-getting-started/user-change-password2.png)

5. <span data-ttu-id="8effb-132">按一下 [提交] 。</span><span class="sxs-lookup"><span data-stu-id="8effb-132">Click **submit**.</span></span>

<span data-ttu-id="8effb-133">幾分鐘後變更您的密碼，hello 新的密碼已使用 Azure Active Directory 網域服務中。</span><span class="sxs-lookup"><span data-stu-id="8effb-133">A few minutes after you have changed your password, hello new password is usable in Azure Active Directory Domain Services.</span></span> <span data-ttu-id="8effb-134">在數分鐘後 （通常約 20 分鐘），您可以登入 toocomputers 所聯結的 toohello 受管理的網域使用 hello 新變更的密碼。</span><span class="sxs-lookup"><span data-stu-id="8effb-134">After a few more minutes (typically, about 20 minutes), you can sign in toocomputers that are joined toohello managed domain by using hello newly changed password.</span></span>

## <a name="related-content"></a><span data-ttu-id="8effb-135">相關內容</span><span class="sxs-lookup"><span data-stu-id="8effb-135">Related Content</span></span>
* [<span data-ttu-id="8effb-136">如何 tooupdate 您自己的密碼</span><span class="sxs-lookup"><span data-stu-id="8effb-136">How tooupdate your own password</span></span>](../active-directory/active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="8effb-137">在 Azure AD 中開始使用密碼管理</span><span class="sxs-lookup"><span data-stu-id="8effb-137">Getting started with Password Management in Azure AD</span></span>](../active-directory/active-directory-passwords-getting-started.md)
* [<span data-ttu-id="8effb-138">啟用密碼同步處理 tooAzure Active Directory 網域服務同步處理的 Azure ad 租用戶</span><span class="sxs-lookup"><span data-stu-id="8effb-138">Enable password synchronization tooAzure Active Directory Domain Services for a synced Azure AD tenant</span></span>](active-directory-ds-getting-started-password-sync-synced-tenant.md)
* [<span data-ttu-id="8effb-139">受 Azure Active Directory Domain Services 管理的網域</span><span class="sxs-lookup"><span data-stu-id="8effb-139">Administer an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="8effb-140">加入 Windows 虛擬機器 tooan Azure Active Directory 網域服務受管理網域</span><span class="sxs-lookup"><span data-stu-id="8effb-140">Join a Windows virtual machine tooan Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="8effb-141">加入 Red Hat Enterprise Linux 虛擬機器 tooan Azure Active Directory 網域服務受管理網域</span><span class="sxs-lookup"><span data-stu-id="8effb-141">Join a Red Hat Enterprise Linux virtual machine tooan Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
