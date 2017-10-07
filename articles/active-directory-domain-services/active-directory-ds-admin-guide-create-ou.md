---
title: "Azure Active Directory Domain Services：管理指南 | Microsoft Docs"
description: "在 Azure AD 網域服務受管理的網域上建立組織單位 (OU)"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 52602ad8-2b93-4082-8487-427bdcfa8126
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: ce7539e5d5c7c1bf9505ef229f2d31d84c00da05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-organizational-unit-ou-on-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="7a26c-103">在 Azure AD 網域服務的受管理網域上建立組織單位 (OU)</span><span class="sxs-lookup"><span data-stu-id="7a26c-103">Create an Organizational Unit (OU) on an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="7a26c-104">Azure AD 網域服務的受管理網域包含兩個內建的容器，分別稱為「AADDC 電腦」和「AADDC 使用者」。</span><span class="sxs-lookup"><span data-stu-id="7a26c-104">Azure AD Domain Services managed domains include two built-in containers called 'AADDC Computers' and 'AADDC Users' respectively.</span></span> <span data-ttu-id="7a26c-105">hello AADDC 電腦容器有電腦物件的所有電腦的加入 toohello 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="7a26c-105">hello 'AADDC Computers' container has computer objects for all computers that are joined toohello managed domain.</span></span> <span data-ttu-id="7a26c-106">hello ' AADDC 使用者 容器包含使用者和群組 hello Azure AD 租用戶中。</span><span class="sxs-lookup"><span data-stu-id="7a26c-106">hello 'AADDC Users' container includes users and groups in hello Azure AD tenant.</span></span> <span data-ttu-id="7a26c-107">有時候，您可能需要 toocreate hello 受管理網域 toodeploy 工作負載的服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="7a26c-107">Occasionally, it may be necessary toocreate service accounts on hello managed domain toodeploy workloads.</span></span> <span data-ttu-id="7a26c-108">基於此目的，您可以在 hello 受管理的網域上建立自訂組織單位 (OU)，並建立該 OU 中的服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="7a26c-108">For this purpose, you can create a custom Organizational Unit (OU) on hello managed domain and create service accounts within that OU.</span></span> <span data-ttu-id="7a26c-109">本文章將示範如何在受管理的網域 OU toocreate。</span><span class="sxs-lookup"><span data-stu-id="7a26c-109">This article shows you how toocreate an OU in your managed domain.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7a26c-110">開始之前</span><span class="sxs-lookup"><span data-stu-id="7a26c-110">Before you begin</span></span>
<span data-ttu-id="7a26c-111">本文所列 tooperform hello 工作，您必須：</span><span class="sxs-lookup"><span data-stu-id="7a26c-111">tooperform hello tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="7a26c-112">有效的 **Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="7a26c-112">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="7a26c-113">**Azure AD 目錄** - 與內部部署目錄或僅限雲端的目錄同步處理。</span><span class="sxs-lookup"><span data-stu-id="7a26c-113">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="7a26c-114">**Azure AD 網域服務**必須啟用 hello Azure AD 目錄。</span><span class="sxs-lookup"><span data-stu-id="7a26c-114">**Azure AD Domain Services** must be enabled for hello Azure AD directory.</span></span> <span data-ttu-id="7a26c-115">如果您尚未這樣做，請遵循 hello 中所述的所有 hello 工作[入門指南](active-directory-ds-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="7a26c-115">If you haven't done so, follow all hello tasks outlined in hello [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="7a26c-116">已加入網域的虛擬機器，您用來管理 hello Azure AD 網域服務受管理網域。</span><span class="sxs-lookup"><span data-stu-id="7a26c-116">A domain-joined virtual machine from which you administer hello Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="7a26c-117">如果您沒有這類虛擬機器，請遵循所有 hello 文章的標題中的 hello 工作[加入 Windows 虛擬機器 tooa 受管理的網域](active-directory-ds-admin-guide-join-windows-vm.md)。</span><span class="sxs-lookup"><span data-stu-id="7a26c-117">If you don't have such a virtual machine, follow all hello tasks outlined in hello article titled [Join a Windows virtual machine tooa managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>
5. <span data-ttu-id="7a26c-118">您需要 hello 認證**使用者帳戶隸屬 toohello ' AAD DC Administrators' 群組**目錄，toocreate 受管理的網域上的自訂 OU 中。</span><span class="sxs-lookup"><span data-stu-id="7a26c-118">You need hello credentials of a **user account belonging toohello 'AAD DC Administrators' group** in your directory, toocreate a custom OU on your managed domain.</span></span>

## <a name="install-ad-administration-tools-on-a-domain-joined-virtual-machine-for-remote-administration"></a><span data-ttu-id="7a26c-119">在已加入網域的虛擬機器上安裝 AD 系統管理工具進行遠端管理</span><span class="sxs-lookup"><span data-stu-id="7a26c-119">Install AD administration tools on a domain-joined virtual machine for remote administration</span></span>
<span data-ttu-id="7a26c-120">可以從遠端使用熟悉的 Active Directory 系統管理工具例如 hello Active Directory 管理中心 (ADAC) 或 AD PowerShell 管理 azure AD 網域服務受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="7a26c-120">Azure AD Domain Services managed domains can be managed remotely using familiar Active Directory administrative tools such as hello Active Directory Administrative Center (ADAC) or AD PowerShell.</span></span> <span data-ttu-id="7a26c-121">租用戶系統管理員沒有 hello 透過遠端桌面的受管理網域的權限 tooconnect toodomain 控制站。</span><span class="sxs-lookup"><span data-stu-id="7a26c-121">Tenant administrators do not have privileges tooconnect toodomain controllers on hello managed domain via Remote Desktop.</span></span> <span data-ttu-id="7a26c-122">tooadminister hello 受管理的網域，虛擬機器聯結的 toohello 受管理的網域上安裝 hello AD 系統管理工具功能。</span><span class="sxs-lookup"><span data-stu-id="7a26c-122">tooadminister hello managed domain, install hello AD administration tools feature on a virtual machine joined toohello managed domain.</span></span> <span data-ttu-id="7a26c-123">Toohello 文章的標題，請參閱[管理 Azure AD 網域服務受管理的網域](active-directory-ds-admin-guide-administer-domain.md)如需相關指示。</span><span class="sxs-lookup"><span data-stu-id="7a26c-123">Refer toohello article titled [administer an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-administer-domain.md) for instructions.</span></span>

## <a name="create-an-organizational-unit-on-hello-managed-domain"></a><span data-ttu-id="7a26c-124">在 hello 受管理的網域上建立組織單位</span><span class="sxs-lookup"><span data-stu-id="7a26c-124">Create an Organizational Unit on hello managed domain</span></span>
<span data-ttu-id="7a26c-125">既然 hello AD 系統管理工具安裝在 hello 已加入網域的虛擬機器，我們可以使用這些工具 toocreate 組織單位 hello 受管理網域上。</span><span class="sxs-lookup"><span data-stu-id="7a26c-125">Now that hello AD Administrative Tools are installed on hello domain joined virtual machine, we can use these tools toocreate an organization unit on hello managed domain.</span></span> <span data-ttu-id="7a26c-126">執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="7a26c-126">Perform hello following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="7a26c-127">只有 hello ' AAD DC Administrators' 群組的成員有自訂的 OU hello toocreate 必要權限。</span><span class="sxs-lookup"><span data-stu-id="7a26c-127">Only members of hello 'AAD DC Administrators' group have hello required privileges toocreate a custom OU.</span></span> <span data-ttu-id="7a26c-128">請確定您執行下列步驟以使用者所屬群組 toothis hello。</span><span class="sxs-lookup"><span data-stu-id="7a26c-128">Ensure that you perform hello following steps as a user who belongs toothis group.</span></span>
>
>

1. <span data-ttu-id="7a26c-129">從 hello 開始畫面上，按一下 **系統管理工具**。</span><span class="sxs-lookup"><span data-stu-id="7a26c-129">From hello Start screen, click **Administrative Tools**.</span></span> <span data-ttu-id="7a26c-130">您應該會看到 hello AD hello 虛擬機器上安裝的系統管理工具。</span><span class="sxs-lookup"><span data-stu-id="7a26c-130">You should see hello AD administrative tools installed on hello virtual machine.</span></span>

    ![安裝在伺服器上的系統管理工具](./media/active-directory-domain-services-admin-guide/install-rsat-admin-tools-installed.png)
2. <span data-ttu-id="7a26c-132">按一下 [Active Directory 管理中心] 。</span><span class="sxs-lookup"><span data-stu-id="7a26c-132">Click **Active Directory Administrative Center**.</span></span>

    ![Active Directory 管理中心](./media/active-directory-domain-services-admin-guide/adac-overview.png)
3. <span data-ttu-id="7a26c-134">tooview hello 網域中，按一下 hello hello 左窗格 (例如，' contoso100.com') 中的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="7a26c-134">tooview hello domain, click hello domain name in hello left pane (for example, 'contoso100.com').</span></span>

    ![ADAC - 檢視網域](./media/active-directory-domain-services-admin-guide/create-ou-adac-overview.png)
4. <span data-ttu-id="7a26c-136">Hello 右側**工作** 窗格中，按一下 **新增**hello 網域名稱 節點下。</span><span class="sxs-lookup"><span data-stu-id="7a26c-136">On hello right side **Tasks** pane, click **New** under hello domain name node.</span></span> <span data-ttu-id="7a26c-137">此範例中，按一下**新增**hello 右側 hello 'contoso100(local)' 節點下**工作**窗格。</span><span class="sxs-lookup"><span data-stu-id="7a26c-137">In this example, we click **New** under hello 'contoso100(local)' node on hello right side **Tasks** pane.</span></span>

    ![ADAC - 新的 OU](./media/active-directory-domain-services-admin-guide/create-ou-adac-new-ou.png)
5. <span data-ttu-id="7a26c-139">您應該會看到 hello 選項 toocreate 組織單位。</span><span class="sxs-lookup"><span data-stu-id="7a26c-139">You should see hello option toocreate an Organizational Unit.</span></span> <span data-ttu-id="7a26c-140">按一下**組織單位**toolaunch hello**建立組織單位**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="7a26c-140">Click **Organizational Unit** toolaunch hello **Create Organizational Unit** dialog.</span></span>
6. <span data-ttu-id="7a26c-141">在 [hello**建立組織單位**] 對話方塊中，指定**名稱**的 hello 新 OU。</span><span class="sxs-lookup"><span data-stu-id="7a26c-141">In hello **Create Organizational Unit** dialog, specify a **Name** for hello new OU.</span></span> <span data-ttu-id="7a26c-142">提供 hello OU 的簡短描述。</span><span class="sxs-lookup"><span data-stu-id="7a26c-142">Provide a short description for hello OU.</span></span> <span data-ttu-id="7a26c-143">您可能也會設定 hello**管理者**hello OU 的欄位。</span><span class="sxs-lookup"><span data-stu-id="7a26c-143">You may also set hello **Managed By** field for hello OU.</span></span> <span data-ttu-id="7a26c-144">toocreate hello 自訂 OU 中，按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="7a26c-144">toocreate hello custom OU, click **OK**.</span></span>

    ![ADAC - 建立 OU 對話方塊](./media/active-directory-domain-services-admin-guide/create-ou-dialog.png)
7. <span data-ttu-id="7a26c-146">新建立的 OU 的 hello 現在應該會出現在 hello AD 管理中心 (ADAC) 中。</span><span class="sxs-lookup"><span data-stu-id="7a26c-146">hello newly created OU should now appear in hello AD Administrative Center (ADAC).</span></span>

    ![ADAC - OU 已建立](./media/active-directory-domain-services-admin-guide/create-ou-done.png)

## <a name="permissionssecurity-for-newly-created-ous"></a><span data-ttu-id="7a26c-148">新建 OU 的權限/安全性</span><span class="sxs-lookup"><span data-stu-id="7a26c-148">Permissions/Security for newly created OUs</span></span>
<span data-ttu-id="7a26c-149">根據預設，hello （hello ' AAD DC Administrators' 群組的成員） 建立使用者自訂的 OU 會授與系統管理權限 （完全控制） 透過 hello hello OU。</span><span class="sxs-lookup"><span data-stu-id="7a26c-149">By default, hello user (member of hello 'AAD DC Administrators' group) who created hello custom OU is granted administrative privileges (full control) over hello OU.</span></span> <span data-ttu-id="7a26c-150">hello 使用者可以繼續進行，並授與權限 tooother 使用者或視需要的 toohello ' AAD DC Administrators' 群組。</span><span class="sxs-lookup"><span data-stu-id="7a26c-150">hello user can then go ahead and grant privileges tooother users or toohello 'AAD DC Administrators' group as desired.</span></span> <span data-ttu-id="7a26c-151">Hello 下列螢幕擷取畫面所示，hello 使用者 'bob@domainservicespreview.onmicrosoft.com' 建立的 hello 新 'MyCustomOU' 的組織單位是授與完整控制權。</span><span class="sxs-lookup"><span data-stu-id="7a26c-151">As seen in hello following screenshot, hello user 'bob@domainservicespreview.onmicrosoft.com' who created hello new 'MyCustomOU' organizational unit is granted full control over it.</span></span>

 ![ADAC - 新的 OU 安全性](./media/active-directory-domain-services-admin-guide/create-ou-permissions.png)

## <a name="notes-on-administering-custom-ous"></a><span data-ttu-id="7a26c-153">管理自訂 OU 的注意事項</span><span class="sxs-lookup"><span data-stu-id="7a26c-153">Notes on administering custom OUs</span></span>
<span data-ttu-id="7a26c-154">既然您已建立了自訂 OU，就可以繼續在這個 OU 中建立使用者、群組、電腦和服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="7a26c-154">Now that you have created a custom OU, you can go ahead and create users, groups, computers, and service accounts in this OU.</span></span> <span data-ttu-id="7a26c-155">您無法從 hello ' AADDC Users' OU toocustom Ou 移動使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="7a26c-155">You cannot move users or groups from hello 'AADDC Users' OU toocustom OUs.</span></span>

> [!WARNING]
> <span data-ttu-id="7a26c-156">您在自訂 OU 下建立的使用者帳戶、群組、服務帳戶和電腦物件無法在 Azure AD 租用戶中使用。</span><span class="sxs-lookup"><span data-stu-id="7a26c-156">User accounts, groups, service accounts, and computer objects that you create under custom OUs are not available in your Azure AD tenant.</span></span> <span data-ttu-id="7a26c-157">換句話說，這些物件不會使用 hello Azure AD Graph API 或 hello Azure AD UI 中顯示。</span><span class="sxs-lookup"><span data-stu-id="7a26c-157">In other words, these objects do not show up using hello Azure AD Graph API or in hello Azure AD UI.</span></span> <span data-ttu-id="7a26c-158">這些物件只可用於 Azure AD 網域服務受管理的網域中。</span><span class="sxs-lookup"><span data-stu-id="7a26c-158">These objects are only available in your Azure AD Domain Services managed domain.</span></span>
>
>

## <a name="related-content"></a><span data-ttu-id="7a26c-159">相關內容</span><span class="sxs-lookup"><span data-stu-id="7a26c-159">Related Content</span></span>
* [<span data-ttu-id="7a26c-160">Administer an Azure AD Domain Services managed domain (管理 Azure AD 網域服務受管理的網域)</span><span class="sxs-lookup"><span data-stu-id="7a26c-160">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="7a26c-161">設定受管理網域的群組原則</span><span class="sxs-lookup"><span data-stu-id="7a26c-161">Configure Group Policy on a managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="7a26c-162">Active Directory 管理中心：入門</span><span class="sxs-lookup"><span data-stu-id="7a26c-162">Active Directory Administrative Center: Getting Started</span></span>](https://technet.microsoft.com/library/dd560651.aspx)
* [<span data-ttu-id="7a26c-163">服務帳戶的逐步指南</span><span class="sxs-lookup"><span data-stu-id="7a26c-163">Service Accounts Step-by-Step Guide</span></span>](https://technet.microsoft.com/library/dd548356.aspx)
