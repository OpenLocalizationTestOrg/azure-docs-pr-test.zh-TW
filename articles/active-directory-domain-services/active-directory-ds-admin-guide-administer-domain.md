---
title: "Azure Active Directory Domain Services：管理受管理的網域 | Microsoft Docs"
description: "管理 Azure Active Directory 網域服務受管理網域"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4fdbc75-3e6b-4e20-8494-5dcc3bf2220a
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: a8292474b6b81172850c11f6cb5b04baf64aec77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="administer-an-azure-active-directory-domain-services-managed-domain"></a><span data-ttu-id="e0c22-103">管理 Azure Active Directory 網域服務受管理網域</span><span class="sxs-lookup"><span data-stu-id="e0c22-103">Administer an Azure Active Directory Domain Services managed domain</span></span>
<span data-ttu-id="e0c22-104">本文說明如何管理 Azure Active Directory (AD) 網域服務受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="e0c22-104">This article shows you how to administer an Azure Active Directory (AD) Domain Services managed domain.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e0c22-105">開始之前</span><span class="sxs-lookup"><span data-stu-id="e0c22-105">Before you begin</span></span>
<span data-ttu-id="e0c22-106">若要執行本文中所列的工作，您需要︰</span><span class="sxs-lookup"><span data-stu-id="e0c22-106">To perform the tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="e0c22-107">有效的 **Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="e0c22-107">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="e0c22-108">**Azure AD 目錄** - 與內部部署目錄或僅限雲端的目錄同步處理。</span><span class="sxs-lookup"><span data-stu-id="e0c22-108">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="e0c22-109">**Azure AD 網域服務** 必須已針對 Azure AD 目錄啟用。</span><span class="sxs-lookup"><span data-stu-id="e0c22-109">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span></span> <span data-ttu-id="e0c22-110">如果還沒有啟用，請按照 [入門指南](active-directory-ds-getting-started.md)所述的所有工作來進行。</span><span class="sxs-lookup"><span data-stu-id="e0c22-110">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="e0c22-111">**已加入網域的虛擬機器** ，您可在其中管理 Azure AD 網域服務受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="e0c22-111">A **domain-joined virtual machine** from which you administer the Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="e0c22-112">如果您沒有這類虛擬機器，請依照名為[將 Windows 虛擬機器加入受管理的網域](active-directory-ds-admin-guide-join-windows-vm.md)一文所述的所有工作進行操作。</span><span class="sxs-lookup"><span data-stu-id="e0c22-112">If you don't have such a virtual machine, follow all the tasks outlined in the article titled [Join a Windows virtual machine to a managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>
5. <span data-ttu-id="e0c22-113">您需要目錄中 **屬於「AAD DC 系統管理員」群組之使用者帳戶** 的認證，才能管理受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="e0c22-113">You need the credentials of a **user account belonging to the 'AAD DC Administrators' group** in your directory, to administer your managed domain.</span></span>

<br>

## <a name="administrative-tasks-you-can-perform-on-a-managed-domain"></a><span data-ttu-id="e0c22-114">可在受管理網域中執行的系統管理工作</span><span class="sxs-lookup"><span data-stu-id="e0c22-114">Administrative tasks you can perform on a managed domain</span></span>
<span data-ttu-id="e0c22-115">「AAD DC 系統管理員」群組的成員已獲授與受管理網域的權限，這些權限讓他們可以執行如下的工作︰</span><span class="sxs-lookup"><span data-stu-id="e0c22-115">Members of the 'AAD DC Administrators' group are granted privileges on the managed domain that enable them to perform tasks such as:</span></span>

* <span data-ttu-id="e0c22-116">將機器加入受管理網域。</span><span class="sxs-lookup"><span data-stu-id="e0c22-116">Join machines to the managed domain.</span></span>
* <span data-ttu-id="e0c22-117">為受管理網域中的「AADDC 電腦」和「AADDC 使用者」容器設定內建 GPO。</span><span class="sxs-lookup"><span data-stu-id="e0c22-117">Configure the built-in GPO for the 'AADDC Computers' and 'AADDC Users' containers in the managed domain.</span></span>
* <span data-ttu-id="e0c22-118">管理受管理網域上的 DNS。</span><span class="sxs-lookup"><span data-stu-id="e0c22-118">Administer DNS on the managed domain.</span></span>
* <span data-ttu-id="e0c22-119">建立及管理受管理網域上的自訂組織單位 (OU)。</span><span class="sxs-lookup"><span data-stu-id="e0c22-119">Create and administer custom Organizational Units (OUs) on the managed domain.</span></span>
* <span data-ttu-id="e0c22-120">取得已加入受管理網域之電腦的系統管理存取權。</span><span class="sxs-lookup"><span data-stu-id="e0c22-120">Gain administrative access to computers joined to the managed domain.</span></span>

## <a name="administrative-privileges-you-do-not-have-on-a-managed-domain"></a><span data-ttu-id="e0c22-121">未擁有的受管理網域系統管理權限</span><span class="sxs-lookup"><span data-stu-id="e0c22-121">Administrative privileges you do not have on a managed domain</span></span>
<span data-ttu-id="e0c22-122">網域是由 Microsoft 負責管理，包括修補、監視及執行備份等活動。</span><span class="sxs-lookup"><span data-stu-id="e0c22-122">The domain is managed by Microsoft, including activities such as patching, monitoring and, performing backups.</span></span> <span data-ttu-id="e0c22-123">因此網域已遭鎖定，而且您不會擁有在網域上執行特定系統管理工作的權限。</span><span class="sxs-lookup"><span data-stu-id="e0c22-123">Therefore, the domain is locked down and you do not have privileges to perform certain administrative tasks on the domain.</span></span> <span data-ttu-id="e0c22-124">您無法執行之工作的部分範例如下。</span><span class="sxs-lookup"><span data-stu-id="e0c22-124">Some examples of tasks you cannot perform are below.</span></span>

* <span data-ttu-id="e0c22-125">你不會被授與受管理網域的「網域系統管理員」或「企業系統管理員」權限。</span><span class="sxs-lookup"><span data-stu-id="e0c22-125">You are not granted Domain Administrator or Enterprise Administrator privileges for the managed domain.</span></span>
* <span data-ttu-id="e0c22-126">您無法擴充受管理網域的結構描述。</span><span class="sxs-lookup"><span data-stu-id="e0c22-126">You cannot extend the schema of the managed domain.</span></span>
* <span data-ttu-id="e0c22-127">您無法使用遠端桌面連線到受管理網域的網域控制站。</span><span class="sxs-lookup"><span data-stu-id="e0c22-127">You cannot connect to domain controllers for the managed domain using Remote Desktop.</span></span>
* <span data-ttu-id="e0c22-128">您無法在受管理網域中新增網域控制站。</span><span class="sxs-lookup"><span data-stu-id="e0c22-128">You cannot add domain controllers to the managed domain.</span></span>

## <a name="task-1---provision-a-domain-joined-windows-server-virtual-machine-to-remotely-administer-the-managed-domain"></a><span data-ttu-id="e0c22-129">工作 1 - 佈建已加入網域的 Windows Server 虛擬機器以從遠端管理受管理的網域</span><span class="sxs-lookup"><span data-stu-id="e0c22-129">Task 1 - Provision a domain-joined Windows Server virtual machine to remotely administer the managed domain</span></span>
<span data-ttu-id="e0c22-130">您可以使用 Active Directory 管理中心 (ADAC) 或 AD PowerShell 等熟悉的 Active Directory 系統管理工具來管理 Azure AD 網域服務受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="e0c22-130">Azure AD Domain Services managed domains can be managed using familiar Active Directory administrative tools such as the Active Directory Administrative Center (ADAC) or AD PowerShell.</span></span> <span data-ttu-id="e0c22-131">租用戶系統管理員沒有權限，不能透過遠端桌面連接受管理網域上的網域控制站。</span><span class="sxs-lookup"><span data-stu-id="e0c22-131">Tenant administrators do not have privileges to connect to domain controllers on the managed domain via Remote Desktop.</span></span> <span data-ttu-id="e0c22-132">因此，「AAD DC 系統管理員」群組的成員可以使用 AD 系統管理工具，從已加入受管理網域的 Windows Server/用戶端電腦遠端管理受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="e0c22-132">Therefore, members of the 'AAD DC Administrators' group can administer managed domains remotely using AD administrative tools from a Windows Server/client computer that is joined to the managed domain.</span></span> <span data-ttu-id="e0c22-133">在已加入受管理網域的 Windows Server 和用戶端電腦上，可以將 AD 系統管理工具安裝做為遠端伺服器管理工具 (RSAT) 選擇性功能的一部分。</span><span class="sxs-lookup"><span data-stu-id="e0c22-133">AD administrative tools can be installed as part of the Remote Server Administration Tools (RSAT) optional feature on Windows Server and client machines joined to the managed domain.</span></span>

<span data-ttu-id="e0c22-134">第一個步驟是設定已加入受管理網域的 Windows Server 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e0c22-134">The first step is to set up a Windows Server virtual machine that is joined to the managed domain.</span></span> <span data-ttu-id="e0c22-135">如需相關指示，請參閱標題為 [將 Windows Server 虛擬機器加入 Azure AD 網域服務受管理網域](active-directory-ds-admin-guide-join-windows-vm.md)的文章。</span><span class="sxs-lookup"><span data-stu-id="e0c22-135">For instructions, refer to the article titled [join a Windows Server virtual machine to an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>

### <a name="remotely-administer-the-managed-domain-from-a-client-computer-for-example-windows-10"></a><span data-ttu-id="e0c22-136">從用戶端電腦 (例如 Windows 10) 遠端管理受管理的網域</span><span class="sxs-lookup"><span data-stu-id="e0c22-136">Remotely administer the managed domain from a client computer (for example, Windows 10)</span></span>
<span data-ttu-id="e0c22-137">本文中的指示使用 Windows Server 虛擬機器來管理 AAD-DS 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="e0c22-137">The instructions in this article use a Windows Server virtual machine to administer the AAD-DS managed domain.</span></span> <span data-ttu-id="e0c22-138">不過，您也可以選擇使用 Windows 用戶端 (例如 Windows 10) 虛擬機器來執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="e0c22-138">However, you can also choose to use a Windows client (for example, Windows 10) virtual machine to do so.</span></span>

<span data-ttu-id="e0c22-139">您可以按照 TechNet 上的指示，在 Windows 用戶端虛擬機器上 [安裝遠端伺服器管理工具 (RSAT)](http://social.technet.microsoft.com/wiki/contents/articles/2202.remote-server-administration-tools-rsat-for-windows-client-and-windows-server-dsforum2wiki.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="e0c22-139">You can [install Remote Server Administration Tools (RSAT)](http://social.technet.microsoft.com/wiki/contents/articles/2202.remote-server-administration-tools-rsat-for-windows-client-and-windows-server-dsforum2wiki.aspx) on a Windows client virtual machine by following the instructions on TechNet.</span></span>

## <a name="task-2---install-active-directory-administration-tools-on-the-virtual-machine"></a><span data-ttu-id="e0c22-140">工作 2 - 在虛擬機器上安裝 Active Directory 系統管理工具</span><span class="sxs-lookup"><span data-stu-id="e0c22-140">Task 2 - Install Active Directory administration tools on the virtual machine</span></span>
<span data-ttu-id="e0c22-141">請執行下列步驟，以在已加入網域的虛擬機器上安裝 Active Directory 系統管理工具。</span><span class="sxs-lookup"><span data-stu-id="e0c22-141">Perform the following steps to install the Active Directory Administration tools on the domain joined virtual machine.</span></span> <span data-ttu-id="e0c22-142">如需有關[安裝和使用遠端伺服器管理工具的詳細資訊](https://technet.microsoft.com/library/hh831501.aspx)，請參閱 TechNet。</span><span class="sxs-lookup"><span data-stu-id="e0c22-142">See Technet for more [information on installing and using Remote Server Administration Tools](https://technet.microsoft.com/library/hh831501.aspx).</span></span>

1. <span data-ttu-id="e0c22-143">在 Azure 傳統入口網站中瀏覽至 [虛擬機器]  節點。</span><span class="sxs-lookup"><span data-stu-id="e0c22-143">Navigate to **Virtual Machines** node in the Azure classic portal.</span></span> <span data-ttu-id="e0c22-144">選取您在工作 1 建立的虛擬機器，然後按一下視窗底部命令列上的 [連線]  。</span><span class="sxs-lookup"><span data-stu-id="e0c22-144">Select the virtual machine you created in Task 1 and click **Connect** on the command bar at the bottom of the window.</span></span>

    ![連線至 Windows 虛擬機器](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. <span data-ttu-id="e0c22-146">傳統入口網站會提示您開啟或儲存副檔名為 '.rdp' 的檔案，其可供用來連線到虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e0c22-146">The classic portal prompts you to open or save a file with a '.rdp' extension, which is used to connect to the virtual machine.</span></span> <span data-ttu-id="e0c22-147">在檔案下載完成時按一下加以開啟。</span><span class="sxs-lookup"><span data-stu-id="e0c22-147">Click to open the file when it has finished downloading.</span></span>
3. <span data-ttu-id="e0c22-148">在登入提示中，使用屬於「AAD DC 系統管理員」群組之使用者的認證。</span><span class="sxs-lookup"><span data-stu-id="e0c22-148">At the login prompt, use the credentials of a user belonging to the 'AAD DC Administrators' group.</span></span> <span data-ttu-id="e0c22-149">例如，使用 'bob@domainservicespreview.onmicrosoft.com' 在我們的案例。</span><span class="sxs-lookup"><span data-stu-id="e0c22-149">For example, we use 'bob@domainservicespreview.onmicrosoft.com' in our case.</span></span>
4. <span data-ttu-id="e0c22-150">在 [開始] 畫面中開啟 [伺服器管理員] 。</span><span class="sxs-lookup"><span data-stu-id="e0c22-150">From the Start screen, open **Server Manager**.</span></span> <span data-ttu-id="e0c22-151">按一下 [伺服器管理員] 視窗中央窗格內的 [新增角色及功能]  。</span><span class="sxs-lookup"><span data-stu-id="e0c22-151">Click **Add Roles and Features** in the central pane of the Server Manager window.</span></span>

    ![啟動虛擬機器上的伺服器管理員](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager.png)
5. <span data-ttu-id="e0c22-153">在 [新增角色及功能精靈] 的 [開始之前] 頁面上，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="e0c22-153">On the **Before You Begin** page of the **Add Roles and Features Wizard**, click **Next**.</span></span>

    ![[開始之前] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-begin.png)
6. <span data-ttu-id="e0c22-155">在 [安裝類型] 頁面上，保持勾選 [角色型或功能型安裝] 選項，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="e0c22-155">On the **Installation Type** page, leave the **Role-based or feature-based installation** option checked and click **Next**.</span></span>

    ![[安裝類型] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-type.png)
7. <span data-ttu-id="e0c22-157">在 [伺服器選擇] 頁面上，從伺服器集區中選取目前的虛擬機器，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="e0c22-157">On the **Server Selection** page, select the current virtual machine from the server pool, and click **Next**.</span></span>

    ![[伺服器選擇] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-server.png)
8. <span data-ttu-id="e0c22-159">在 [伺服器角色] 頁面上，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="e0c22-159">On the **Server Roles** page, click **Next**.</span></span> <span data-ttu-id="e0c22-160">我們會略過此頁面，因為我們沒有要在伺服器上安裝任何角色。</span><span class="sxs-lookup"><span data-stu-id="e0c22-160">We skip this page since we are not installing any roles on the server.</span></span>
9. <span data-ttu-id="e0c22-161">在 [功能] 頁面上，按一下以展開 [遠端伺服器管理工具] 節點，然後按一下以展開 [角色管理工具] 節點。</span><span class="sxs-lookup"><span data-stu-id="e0c22-161">On the **Features** page, click to expand the **Remote Server Administration Tools** node and then click to expand the **Role Administration Tools** node.</span></span> <span data-ttu-id="e0c22-162">從角色管理工具的清單中選取 [AD DS 及 AD LDS 工具]  功能。</span><span class="sxs-lookup"><span data-stu-id="e0c22-162">Select **AD DS and AD LDS Tools** feature from the list of role administration tools.</span></span>

    ![[功能] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-ad-tools.png)
10. <span data-ttu-id="e0c22-164">在 [確認] 頁面上，按一下 [安裝] 以在虛擬機器上安裝 AD 與 AD LDS 工具功能。</span><span class="sxs-lookup"><span data-stu-id="e0c22-164">On the **Confirmation** page, click **Install** to install the AD and AD LDS tools feature on the virtual machine.</span></span> <span data-ttu-id="e0c22-165">順利完成功能安裝時，按一下 [關閉] 以結束 [新增角色及功能] 精靈。</span><span class="sxs-lookup"><span data-stu-id="e0c22-165">When feature installation completes successfully, click **Close** to exit the **Add Roles and Features** wizard.</span></span>

    ![確認電子郵件](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-confirmation.png)

## <a name="task-3---connect-to-and-explore-the-managed-domain"></a><span data-ttu-id="e0c22-167">工作 3 - 連線到受管理網域並進行瀏覽</span><span class="sxs-lookup"><span data-stu-id="e0c22-167">Task 3 - Connect to and explore the managed domain</span></span>
<span data-ttu-id="e0c22-168">既然加入網域的虛擬機器上已安裝了 AD 系統管理工具，我們就可以使用這些工具來探索和管理受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="e0c22-168">Now that the AD Administrative Tools are installed on the domain joined virtual machine, we can use these tools to explore and administer the managed domain.</span></span>

> [!NOTE]
> <span data-ttu-id="e0c22-169">您必須是「AAD DC 系統管理員」群組的成員，才能管理受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="e0c22-169">You need to be a member of the 'AAD DC Administrators' group, to administer the managed domain.</span></span>
>
>

1. <span data-ttu-id="e0c22-170">從 [開始] 畫面中，按一下 [系統管理工具] 。</span><span class="sxs-lookup"><span data-stu-id="e0c22-170">From the Start screen, click **Administrative Tools**.</span></span> <span data-ttu-id="e0c22-171">您應該會看到安裝在虛擬機器上的 AD 系統管理工具。</span><span class="sxs-lookup"><span data-stu-id="e0c22-171">You should see the AD administrative tools installed on the virtual machine.</span></span>

    ![安裝在伺服器上的系統管理工具](./media/active-directory-domain-services-admin-guide/install-rsat-admin-tools-installed.png)
2. <span data-ttu-id="e0c22-173">按一下 [Active Directory 管理中心] 。</span><span class="sxs-lookup"><span data-stu-id="e0c22-173">Click **Active Directory Administrative Center**.</span></span>

    ![Active Directory 管理中心](./media/active-directory-domain-services-admin-guide/adac-overview.png)
3. <span data-ttu-id="e0c22-175">若要探索網域，請按一下左窗格中的網域名稱 (例如，'contoso100.com')。</span><span class="sxs-lookup"><span data-stu-id="e0c22-175">To explore the domain, click the domain name in the left pane (for example, 'contoso100.com').</span></span> <span data-ttu-id="e0c22-176">請注意分別稱為「AADDC 電腦」和「AADDC 使用者」的兩個容器。</span><span class="sxs-lookup"><span data-stu-id="e0c22-176">Notice two containers called 'AADDC Computers' and 'AADDC Users' respectively.</span></span>

    ![ADAC - 檢視網域](./media/active-directory-domain-services-admin-guide/adac-domain-view.png)
4. <span data-ttu-id="e0c22-178">在稱為 [AADDC 使用者]  的容器上按一下，以查看所有屬於受管理網域的使用者和群組。</span><span class="sxs-lookup"><span data-stu-id="e0c22-178">Click the container called **AADDC Users** to see all users and groups belonging to the managed domain.</span></span> <span data-ttu-id="e0c22-179">在此容器中，您應該會看到您的 Azure AD 租用戶中的使用者帳戶和群組顯示出來。</span><span class="sxs-lookup"><span data-stu-id="e0c22-179">You should see user accounts and groups from your Azure AD tenant show up in this container.</span></span> <span data-ttu-id="e0c22-180">在這個範例中，請注意此容器中有 'bob' 使用者的使用者帳戶和稱為「AAD DC 系統管理員」的群組。</span><span class="sxs-lookup"><span data-stu-id="e0c22-180">Notice in this example, a user account for the user called 'bob' and a group called 'AAD DC Administrators' are available in this container.</span></span>

    ![ADAC - 網域使用者](./media/active-directory-domain-services-admin-guide/adac-aaddc-users.png)
5. <span data-ttu-id="e0c22-182">在稱為 [AADDC 電腦]  的容器上按一下，以查看已新增此受管理網域的電腦。</span><span class="sxs-lookup"><span data-stu-id="e0c22-182">Click the container called **AADDC Computers** to see the computers joined to this managed domain.</span></span> <span data-ttu-id="e0c22-183">您應該會看到已加入網域之目前虛擬機器的項目。</span><span class="sxs-lookup"><span data-stu-id="e0c22-183">You should see an entry for the current virtual machine, which is joined to the domain.</span></span> <span data-ttu-id="e0c22-184">已新增 Azure AD 網域服務受管理網域之所有電腦的電腦帳戶會儲存在此「AADDC 電腦」容器中。</span><span class="sxs-lookup"><span data-stu-id="e0c22-184">Computer accounts for all computers that are joined to the Azure AD Domain Services managed domain are stored in this 'AADDC Computers' container.</span></span>

    ![ADAC - 已加入網域的電腦](./media/active-directory-domain-services-admin-guide/adac-aaddc-computers.png)

<br>

## <a name="related-content"></a><span data-ttu-id="e0c22-186">相關內容</span><span class="sxs-lookup"><span data-stu-id="e0c22-186">Related Content</span></span>
* [<span data-ttu-id="e0c22-187">Azure AD Domain Services - 入門指南</span><span class="sxs-lookup"><span data-stu-id="e0c22-187">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="e0c22-188">將 Windows Server 虛擬機器加入 Azure AD 網域服務受管理的網域</span><span class="sxs-lookup"><span data-stu-id="e0c22-188">Join a Windows Server virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="e0c22-189">部署遠端伺服器管理工具</span><span class="sxs-lookup"><span data-stu-id="e0c22-189">Deploy Remote Server Administration Tools</span></span>](https://technet.microsoft.com/library/hh831501.aspx)
