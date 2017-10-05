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
ms.openlocfilehash: 017a8cabe81743af4c0cbb694098df799a904468
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-organizational-unit-ou-on-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="de70c-103">在 Azure AD 網域服務的受管理網域上建立組織單位 (OU)</span><span class="sxs-lookup"><span data-stu-id="de70c-103">Create an Organizational Unit (OU) on an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="de70c-104">Azure AD 網域服務的受管理網域包含兩個內建的容器，分別稱為「AADDC 電腦」和「AADDC 使用者」。</span><span class="sxs-lookup"><span data-stu-id="de70c-104">Azure AD Domain Services managed domains include two built-in containers called 'AADDC Computers' and 'AADDC Users' respectively.</span></span> <span data-ttu-id="de70c-105">「AADDC 電腦」容器有已加入受管理的網域中全部電腦的電腦物件。</span><span class="sxs-lookup"><span data-stu-id="de70c-105">The 'AADDC Computers' container has computer objects for all computers that are joined to the managed domain.</span></span> <span data-ttu-id="de70c-106">「AADDC 使用者」容器包含 Azure AD 租用戶中的使用者和群組。</span><span class="sxs-lookup"><span data-stu-id="de70c-106">The 'AADDC Users' container includes users and groups in the Azure AD tenant.</span></span> <span data-ttu-id="de70c-107">有時候，可能需要在受管理的網域上建立服務帳戶，才能部署工作負載。</span><span class="sxs-lookup"><span data-stu-id="de70c-107">Occasionally, it may be necessary to create service accounts on the managed domain to deploy workloads.</span></span> <span data-ttu-id="de70c-108">為此目的，您可以在受管理的網域上建立自訂的組織單位 (OU)，並在此 OU 內建立服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="de70c-108">For this purpose, you can create a custom Organizational Unit (OU) on the managed domain and create service accounts within that OU.</span></span> <span data-ttu-id="de70c-109">本文將示範如何在受管理的網域中建立 OU。</span><span class="sxs-lookup"><span data-stu-id="de70c-109">This article shows you how to create an OU in your managed domain.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="de70c-110">開始之前</span><span class="sxs-lookup"><span data-stu-id="de70c-110">Before you begin</span></span>
<span data-ttu-id="de70c-111">若要執行本文中所列的工作，您需要︰</span><span class="sxs-lookup"><span data-stu-id="de70c-111">To perform the tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="de70c-112">有效的 **Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="de70c-112">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="de70c-113">**Azure AD 目錄** - 與內部部署目錄或僅限雲端的目錄同步處理。</span><span class="sxs-lookup"><span data-stu-id="de70c-113">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="de70c-114">**Azure AD 網域服務** 必須已針對 Azure AD 目錄啟用。</span><span class="sxs-lookup"><span data-stu-id="de70c-114">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span></span> <span data-ttu-id="de70c-115">如果還沒有啟用，請按照 [入門指南](active-directory-ds-getting-started.md)所述的所有工作來進行。</span><span class="sxs-lookup"><span data-stu-id="de70c-115">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="de70c-116">已加入網域的虛擬機器，您可在其中管理 AD Domain Services 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="de70c-116">A domain-joined virtual machine from which you administer the Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="de70c-117">如果您沒有這類虛擬機器，請依照名為[將 Windows 虛擬機器加入受管理的網域](active-directory-ds-admin-guide-join-windows-vm.md)一文所述的所有工作進行操作。</span><span class="sxs-lookup"><span data-stu-id="de70c-117">If you don't have such a virtual machine, follow all the tasks outlined in the article titled [Join a Windows virtual machine to a managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>
5. <span data-ttu-id="de70c-118">您需要目錄中**屬於「AAD DC 系統管理員」群組之使用者帳戶**的認證，才能在受管理的網域上建立自訂 OU。</span><span class="sxs-lookup"><span data-stu-id="de70c-118">You need the credentials of a **user account belonging to the 'AAD DC Administrators' group** in your directory, to create a custom OU on your managed domain.</span></span>

## <a name="install-ad-administration-tools-on-a-domain-joined-virtual-machine-for-remote-administration"></a><span data-ttu-id="de70c-119">在已加入網域的虛擬機器上安裝 AD 系統管理工具進行遠端管理</span><span class="sxs-lookup"><span data-stu-id="de70c-119">Install AD administration tools on a domain-joined virtual machine for remote administration</span></span>
<span data-ttu-id="de70c-120">使用 Active Directory 管理中心 (ADAC) 或 AD PowerShell 等熟悉的 Active Directory 系統管理工具，可以從遠端管理 Azure AD 網域服務受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="de70c-120">Azure AD Domain Services managed domains can be managed remotely using familiar Active Directory administrative tools such as the Active Directory Administrative Center (ADAC) or AD PowerShell.</span></span> <span data-ttu-id="de70c-121">租用戶系統管理員沒有權限，不能透過遠端桌面連接受管理網域上的網域控制站。</span><span class="sxs-lookup"><span data-stu-id="de70c-121">Tenant administrators do not have privileges to connect to domain controllers on the managed domain via Remote Desktop.</span></span> <span data-ttu-id="de70c-122">若要管理受管理的網域，請在加入受管理網域的虛擬機器上安裝 AD 系統管理工具功能。</span><span class="sxs-lookup"><span data-stu-id="de70c-122">To administer the managed domain, install the AD administration tools feature on a virtual machine joined to the managed domain.</span></span> <span data-ttu-id="de70c-123">如需相關指示，請參閱 [dminister an Azure AD Domain Services managed domain (管理 Azure AD 網域服務受管理的網域)](active-directory-ds-admin-guide-administer-domain.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="de70c-123">Refer to the article titled [administer an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-administer-domain.md) for instructions.</span></span>

## <a name="create-an-organizational-unit-on-the-managed-domain"></a><span data-ttu-id="de70c-124">在受管理的網域上建立組織單位</span><span class="sxs-lookup"><span data-stu-id="de70c-124">Create an Organizational Unit on the managed domain</span></span>
<span data-ttu-id="de70c-125">既然加入網域的虛擬機器上已安裝了 AD 系統管理工具，我們就可以使用這些工具在受管理的網域上建立組織單位。</span><span class="sxs-lookup"><span data-stu-id="de70c-125">Now that the AD Administrative Tools are installed on the domain joined virtual machine, we can use these tools to create an organization unit on the managed domain.</span></span> <span data-ttu-id="de70c-126">執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="de70c-126">Perform the following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="de70c-127">只有「AAD DC 管理員」群組的成員具有建立自訂 OU 的必要權限。</span><span class="sxs-lookup"><span data-stu-id="de70c-127">Only members of the 'AAD DC Administrators' group have the required privileges to create a custom OU.</span></span> <span data-ttu-id="de70c-128">請確保以這個群組成員的使用者身分執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="de70c-128">Ensure that you perform the following steps as a user who belongs to this group.</span></span>
>
>

1. <span data-ttu-id="de70c-129">從 [開始] 畫面中，按一下 [系統管理工具] 。</span><span class="sxs-lookup"><span data-stu-id="de70c-129">From the Start screen, click **Administrative Tools**.</span></span> <span data-ttu-id="de70c-130">您應該會看到安裝在虛擬機器上的 AD 系統管理工具。</span><span class="sxs-lookup"><span data-stu-id="de70c-130">You should see the AD administrative tools installed on the virtual machine.</span></span>

    ![安裝在伺服器上的系統管理工具](./media/active-directory-domain-services-admin-guide/install-rsat-admin-tools-installed.png)
2. <span data-ttu-id="de70c-132">按一下 [Active Directory 管理中心] 。</span><span class="sxs-lookup"><span data-stu-id="de70c-132">Click **Active Directory Administrative Center**.</span></span>

    ![Active Directory 管理中心](./media/active-directory-domain-services-admin-guide/adac-overview.png)
3. <span data-ttu-id="de70c-134">若要檢視網域，請按一下左窗格中的網域名稱 (例如，'contoso100.com')。</span><span class="sxs-lookup"><span data-stu-id="de70c-134">To view the domain, click the domain name in the left pane (for example, 'contoso100.com').</span></span>

    ![ADAC - 檢視網域](./media/active-directory-domain-services-admin-guide/create-ou-adac-overview.png)
4. <span data-ttu-id="de70c-136">在右側的 [工作] 窗格中，按一下網域名稱節點下的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="de70c-136">On the right side **Tasks** pane, click **New** under the domain name node.</span></span> <span data-ttu-id="de70c-137">在此範例中，會在右側的 [工作] 窗格中，按一下 'contoso100(local)' 節點下的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="de70c-137">In this example, we click **New** under the 'contoso100(local)' node on the right side **Tasks** pane.</span></span>

    ![ADAC - 新的 OU](./media/active-directory-domain-services-admin-guide/create-ou-adac-new-ou.png)
5. <span data-ttu-id="de70c-139">您應該會看到建立組織單位的選項。</span><span class="sxs-lookup"><span data-stu-id="de70c-139">You should see the option to create an Organizational Unit.</span></span> <span data-ttu-id="de70c-140">按一下 [組織單位] 啟動 [建立組織單位] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="de70c-140">Click **Organizational Unit** to launch the **Create Organizational Unit** dialog.</span></span>
6. <span data-ttu-id="de70c-141">在 [建立組織單位] 對話方塊中，指定新 OU 的 [名稱]。</span><span class="sxs-lookup"><span data-stu-id="de70c-141">In the **Create Organizational Unit** dialog, specify a **Name** for the new OU.</span></span> <span data-ttu-id="de70c-142">提供 OU 的簡短描述。</span><span class="sxs-lookup"><span data-stu-id="de70c-142">Provide a short description for the OU.</span></span> <span data-ttu-id="de70c-143">您也可以設定 OU 的 [Managed By] \(管理者)  欄位。</span><span class="sxs-lookup"><span data-stu-id="de70c-143">You may also set the **Managed By** field for the OU.</span></span> <span data-ttu-id="de70c-144">若要建立自訂映像，請按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="de70c-144">To create the custom OU, click **OK**.</span></span>

    ![ADAC - 建立 OU 對話方塊](./media/active-directory-domain-services-admin-guide/create-ou-dialog.png)
7. <span data-ttu-id="de70c-146">新建立的 OU 現在應該會出現在 AD 管理中心 (ADAC) 中。</span><span class="sxs-lookup"><span data-stu-id="de70c-146">The newly created OU should now appear in the AD Administrative Center (ADAC).</span></span>

    ![ADAC - OU 已建立](./media/active-directory-domain-services-admin-guide/create-ou-done.png)

## <a name="permissionssecurity-for-newly-created-ous"></a><span data-ttu-id="de70c-148">新建 OU 的權限/安全性</span><span class="sxs-lookup"><span data-stu-id="de70c-148">Permissions/Security for newly created OUs</span></span>
<span data-ttu-id="de70c-149">建立自訂 OU 的使用者 (「AAD DC 系統管理員」群組的成員) 預設會被授與 OU 的系統管理權限 (完全控制)。</span><span class="sxs-lookup"><span data-stu-id="de70c-149">By default, the user (member of the 'AAD DC Administrators' group) who created the custom OU is granted administrative privileges (full control) over the OU.</span></span> <span data-ttu-id="de70c-150">這個使用者接著可以繼續將權限授與其他使用者，或視需要授與「AAD DC 系統管理員」群組。</span><span class="sxs-lookup"><span data-stu-id="de70c-150">The user can then go ahead and grant privileges to other users or to the 'AAD DC Administrators' group as desired.</span></span> <span data-ttu-id="de70c-151">下列螢幕擷取畫面，使用者所見 'bob@domainservicespreview.onmicrosoft.com' 新 'MyCustomOU' 組織單位的建立者授與完整控制權。</span><span class="sxs-lookup"><span data-stu-id="de70c-151">As seen in the following screenshot, the user 'bob@domainservicespreview.onmicrosoft.com' who created the new 'MyCustomOU' organizational unit is granted full control over it.</span></span>

 ![ADAC - 新的 OU 安全性](./media/active-directory-domain-services-admin-guide/create-ou-permissions.png)

## <a name="notes-on-administering-custom-ous"></a><span data-ttu-id="de70c-153">管理自訂 OU 的注意事項</span><span class="sxs-lookup"><span data-stu-id="de70c-153">Notes on administering custom OUs</span></span>
<span data-ttu-id="de70c-154">既然您已建立了自訂 OU，就可以繼續在這個 OU 中建立使用者、群組、電腦和服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="de70c-154">Now that you have created a custom OU, you can go ahead and create users, groups, computers, and service accounts in this OU.</span></span> <span data-ttu-id="de70c-155">您無法將使用者或群組從「AAD DC 使用者」OU 移至自訂 OU。</span><span class="sxs-lookup"><span data-stu-id="de70c-155">You cannot move users or groups from the 'AADDC Users' OU to custom OUs.</span></span>

> [!WARNING]
> <span data-ttu-id="de70c-156">您在自訂 OU 下建立的使用者帳戶、群組、服務帳戶和電腦物件無法在 Azure AD 租用戶中使用。</span><span class="sxs-lookup"><span data-stu-id="de70c-156">User accounts, groups, service accounts, and computer objects that you create under custom OUs are not available in your Azure AD tenant.</span></span> <span data-ttu-id="de70c-157">換句話說，使用 Azure AD Graph API 或 Azure AD UI 中都不會顯示這些物件。</span><span class="sxs-lookup"><span data-stu-id="de70c-157">In other words, these objects do not show up using the Azure AD Graph API or in the Azure AD UI.</span></span> <span data-ttu-id="de70c-158">這些物件只可用於 Azure AD 網域服務受管理的網域中。</span><span class="sxs-lookup"><span data-stu-id="de70c-158">These objects are only available in your Azure AD Domain Services managed domain.</span></span>
>
>

## <a name="related-content"></a><span data-ttu-id="de70c-159">相關內容</span><span class="sxs-lookup"><span data-stu-id="de70c-159">Related Content</span></span>
* [<span data-ttu-id="de70c-160">Administer an Azure AD Domain Services managed domain (管理 Azure AD 網域服務受管理的網域)</span><span class="sxs-lookup"><span data-stu-id="de70c-160">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="de70c-161">設定受管理網域的群組原則</span><span class="sxs-lookup"><span data-stu-id="de70c-161">Configure Group Policy on a managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="de70c-162">Active Directory 管理中心：入門</span><span class="sxs-lookup"><span data-stu-id="de70c-162">Active Directory Administrative Center: Getting Started</span></span>](https://technet.microsoft.com/library/dd560651.aspx)
* [<span data-ttu-id="de70c-163">服務帳戶的逐步指南</span><span class="sxs-lookup"><span data-stu-id="de70c-163">Service Accounts Step-by-Step Guide</span></span>](https://technet.microsoft.com/library/dd548356.aspx)
