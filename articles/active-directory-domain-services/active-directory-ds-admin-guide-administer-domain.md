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
ms.openlocfilehash: 11acc79e06163e3193b1aa981f2cd28af812789d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="administer-an-azure-active-directory-domain-services-managed-domain"></a><span data-ttu-id="da87a-103">管理 Azure Active Directory 網域服務受管理網域</span><span class="sxs-lookup"><span data-stu-id="da87a-103">Administer an Azure Active Directory Domain Services managed domain</span></span>
<span data-ttu-id="da87a-104">本文示範 tooadminister Azure Active Directory (AD) 網域服務網域的管理方式。</span><span class="sxs-lookup"><span data-stu-id="da87a-104">This article shows you how tooadminister an Azure Active Directory (AD) Domain Services managed domain.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="da87a-105">開始之前</span><span class="sxs-lookup"><span data-stu-id="da87a-105">Before you begin</span></span>
<span data-ttu-id="da87a-106">本文所列 tooperform hello 工作，您必須：</span><span class="sxs-lookup"><span data-stu-id="da87a-106">tooperform hello tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="da87a-107">有效的 **Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="da87a-107">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="da87a-108">**Azure AD 目錄** - 與內部部署目錄或僅限雲端的目錄同步處理。</span><span class="sxs-lookup"><span data-stu-id="da87a-108">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="da87a-109">**Azure AD 網域服務**必須啟用 hello Azure AD 目錄。</span><span class="sxs-lookup"><span data-stu-id="da87a-109">**Azure AD Domain Services** must be enabled for hello Azure AD directory.</span></span> <span data-ttu-id="da87a-110">如果您尚未這樣做，請遵循 hello 中所述的所有 hello 工作[入門指南](active-directory-ds-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="da87a-110">If you haven't done so, follow all hello tasks outlined in hello [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="da87a-111">A**已加入網域的虛擬機器**從您管理的 hello Azure AD 網域服務受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="da87a-111">A **domain-joined virtual machine** from which you administer hello Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="da87a-112">如果您沒有這類虛擬機器，請遵循所有 hello 文章的標題中的 hello 工作[加入 Windows 虛擬機器 tooa 受管理的網域](active-directory-ds-admin-guide-join-windows-vm.md)。</span><span class="sxs-lookup"><span data-stu-id="da87a-112">If you don't have such a virtual machine, follow all hello tasks outlined in hello article titled [Join a Windows virtual machine tooa managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>
5. <span data-ttu-id="da87a-113">您需要 hello 認證**使用者帳戶隸屬 toohello ' AAD DC Administrators' 群組**目錄，tooadminister 中受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="da87a-113">You need hello credentials of a **user account belonging toohello 'AAD DC Administrators' group** in your directory, tooadminister your managed domain.</span></span>

<br>

## <a name="administrative-tasks-you-can-perform-on-a-managed-domain"></a><span data-ttu-id="da87a-114">可在受管理網域中執行的系統管理工作</span><span class="sxs-lookup"><span data-stu-id="da87a-114">Administrative tasks you can perform on a managed domain</span></span>
<span data-ttu-id="da87a-115">Hello 受管理的網域，讓它們 tooperform 工作這類權限會授與 hello ' AAD DC Administrators' 群組的成員：</span><span class="sxs-lookup"><span data-stu-id="da87a-115">Members of hello 'AAD DC Administrators' group are granted privileges on hello managed domain that enable them tooperform tasks such as:</span></span>

* <span data-ttu-id="da87a-116">加入機器 toohello 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="da87a-116">Join machines toohello managed domain.</span></span>
* <span data-ttu-id="da87a-117">Hello 內建在設定 GPO 的 hello 'AADDC 電腦' 和 ' AADDC 使用者 容器 hello 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="da87a-117">Configure hello built-in GPO for hello 'AADDC Computers' and 'AADDC Users' containers in hello managed domain.</span></span>
* <span data-ttu-id="da87a-118">管理 hello 受管理的網域上的 DNS。</span><span class="sxs-lookup"><span data-stu-id="da87a-118">Administer DNS on hello managed domain.</span></span>
* <span data-ttu-id="da87a-119">建立及管理自訂組織單位 (Ou) 上 hello 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="da87a-119">Create and administer custom Organizational Units (OUs) on hello managed domain.</span></span>
* <span data-ttu-id="da87a-120">提升的系統管理存取 toocomputers 聯結 toohello 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="da87a-120">Gain administrative access toocomputers joined toohello managed domain.</span></span>

## <a name="administrative-privileges-you-do-not-have-on-a-managed-domain"></a><span data-ttu-id="da87a-121">未擁有的受管理網域系統管理權限</span><span class="sxs-lookup"><span data-stu-id="da87a-121">Administrative privileges you do not have on a managed domain</span></span>
<span data-ttu-id="da87a-122">hello 網域是由 Microsoft，包括活動，例如修補、 監視和備份管理。</span><span class="sxs-lookup"><span data-stu-id="da87a-122">hello domain is managed by Microsoft, including activities such as patching, monitoring and, performing backups.</span></span> <span data-ttu-id="da87a-123">因此，hello 網域已鎖定，而且您沒有權限 tooperform 特定系統管理工作 hello 網域上。</span><span class="sxs-lookup"><span data-stu-id="da87a-123">Therefore, hello domain is locked down and you do not have privileges tooperform certain administrative tasks on hello domain.</span></span> <span data-ttu-id="da87a-124">您無法執行之工作的部分範例如下。</span><span class="sxs-lookup"><span data-stu-id="da87a-124">Some examples of tasks you cannot perform are below.</span></span>

* <span data-ttu-id="da87a-125">您未獲授予 hello 受管理的網域的網域系統管理員或企業系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="da87a-125">You are not granted Domain Administrator or Enterprise Administrator privileges for hello managed domain.</span></span>
* <span data-ttu-id="da87a-126">您無法擴充 hello hello 受管理的網域結構描述。</span><span class="sxs-lookup"><span data-stu-id="da87a-126">You cannot extend hello schema of hello managed domain.</span></span>
* <span data-ttu-id="da87a-127">您無法連接 toodomain hello 使用遠端桌面受管理的網域控制站。</span><span class="sxs-lookup"><span data-stu-id="da87a-127">You cannot connect toodomain controllers for hello managed domain using Remote Desktop.</span></span>
* <span data-ttu-id="da87a-128">您無法加入網域控制站 toohello 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="da87a-128">You cannot add domain controllers toohello managed domain.</span></span>

## <a name="task-1---provision-a-domain-joined-windows-server-virtual-machine-tooremotely-administer-hello-managed-domain"></a><span data-ttu-id="da87a-129">工作 1-佈建已加入網域的 Windows Server 虛擬機器 tooremotely 管理 hello 受管理的網域</span><span class="sxs-lookup"><span data-stu-id="da87a-129">Task 1 - Provision a domain-joined Windows Server virtual machine tooremotely administer hello managed domain</span></span>
<span data-ttu-id="da87a-130">可以使用熟悉 Active Directory 系統管理工具，例如 hello Active Directory 管理中心 (ADAC) 或 AD PowerShell 管理 azure AD 網域服務受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="da87a-130">Azure AD Domain Services managed domains can be managed using familiar Active Directory administrative tools such as hello Active Directory Administrative Center (ADAC) or AD PowerShell.</span></span> <span data-ttu-id="da87a-131">租用戶系統管理員沒有 hello 透過遠端桌面的受管理網域的權限 tooconnect toodomain 控制站。</span><span class="sxs-lookup"><span data-stu-id="da87a-131">Tenant administrators do not have privileges tooconnect toodomain controllers on hello managed domain via Remote Desktop.</span></span> <span data-ttu-id="da87a-132">因此，hello ' AAD DC Administrators' 群組可以管理的成員管理的網域從遠端使用 AD 從聯結的 toohello 受管理的網域的 Windows 伺服器/用戶端電腦的系統管理工具。</span><span class="sxs-lookup"><span data-stu-id="da87a-132">Therefore, members of hello 'AAD DC Administrators' group can administer managed domains remotely using AD administrative tools from a Windows Server/client computer that is joined toohello managed domain.</span></span> <span data-ttu-id="da87a-133">可以安裝 AD 系統管理工具，因為 Windows Server 和用戶端電腦上 hello 遠端伺服器管理工具 (RSAT) 選擇性功能的一部分加入 toohello 受管理網域。</span><span class="sxs-lookup"><span data-stu-id="da87a-133">AD administrative tools can be installed as part of hello Remote Server Administration Tools (RSAT) optional feature on Windows Server and client machines joined toohello managed domain.</span></span>

<span data-ttu-id="da87a-134">hello 第一個步驟是 tooset 是聯結的 toohello 受管理網域的 Windows Server 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="da87a-134">hello first step is tooset up a Windows Server virtual machine that is joined toohello managed domain.</span></span> <span data-ttu-id="da87a-135">如需指示，請參閱 toohello 文章 <<c0> [ 加入 Windows Server 虛擬機器 tooan Azure AD 網域服務受管理的網域](active-directory-ds-admin-guide-join-windows-vm.md)。</span><span class="sxs-lookup"><span data-stu-id="da87a-135">For instructions, refer toohello article titled [join a Windows Server virtual machine tooan Azure AD Domain Services managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>

### <a name="remotely-administer-hello-managed-domain-from-a-client-computer-for-example-windows-10"></a><span data-ttu-id="da87a-136">從遠端管理 hello 受管理的網域從用戶端電腦 (例如，Windows 10)</span><span class="sxs-lookup"><span data-stu-id="da87a-136">Remotely administer hello managed domain from a client computer (for example, Windows 10)</span></span>
<span data-ttu-id="da87a-137">在此發行項使用 Windows Server 虛擬機器 tooadminister hello AAD DS hello 指示受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="da87a-137">hello instructions in this article use a Windows Server virtual machine tooadminister hello AAD-DS managed domain.</span></span> <span data-ttu-id="da87a-138">不過，您也可以選擇 toouse Windows 用戶端 (例如，Windows 10) 的虛擬機器 toodo 因此。</span><span class="sxs-lookup"><span data-stu-id="da87a-138">However, you can also choose toouse a Windows client (for example, Windows 10) virtual machine toodo so.</span></span>

<span data-ttu-id="da87a-139">您可以[安裝遠端伺服器管理工具 (RSAT)](http://social.technet.microsoft.com/wiki/contents/articles/2202.remote-server-administration-tools-rsat-for-windows-client-and-windows-server-dsforum2wiki.aspx)依照 hello 指示 TechNet 上的 Windows 用戶端虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="da87a-139">You can [install Remote Server Administration Tools (RSAT)](http://social.technet.microsoft.com/wiki/contents/articles/2202.remote-server-administration-tools-rsat-for-windows-client-and-windows-server-dsforum2wiki.aspx) on a Windows client virtual machine by following hello instructions on TechNet.</span></span>

## <a name="task-2---install-active-directory-administration-tools-on-hello-virtual-machine"></a><span data-ttu-id="da87a-140">工作 2-hello 虛擬機器上安裝 Active Directory 管理工具</span><span class="sxs-lookup"><span data-stu-id="da87a-140">Task 2 - Install Active Directory administration tools on hello virtual machine</span></span>
<span data-ttu-id="da87a-141">執行下列步驟 tooinstall hello 的 Active Directory 管理工具 hello 已加入網域的虛擬機器上的 hello。</span><span class="sxs-lookup"><span data-stu-id="da87a-141">Perform hello following steps tooinstall hello Active Directory Administration tools on hello domain joined virtual machine.</span></span> <span data-ttu-id="da87a-142">如需有關[安裝和使用遠端伺服器管理工具的詳細資訊](https://technet.microsoft.com/library/hh831501.aspx)，請參閱 TechNet。</span><span class="sxs-lookup"><span data-stu-id="da87a-142">See Technet for more [information on installing and using Remote Server Administration Tools](https://technet.microsoft.com/library/hh831501.aspx).</span></span>

1. <span data-ttu-id="da87a-143">瀏覽過**虛擬機器**hello Azure 傳統入口網站中的節點。</span><span class="sxs-lookup"><span data-stu-id="da87a-143">Navigate too**Virtual Machines** node in hello Azure classic portal.</span></span> <span data-ttu-id="da87a-144">選取您在工作 1 中建立的 hello 虛擬機器，然後按一下**連接**hello 在 hello hello 視窗底部的命令列上。</span><span class="sxs-lookup"><span data-stu-id="da87a-144">Select hello virtual machine you created in Task 1 and click **Connect** on hello command bar at hello bottom of hello window.</span></span>

    ![TooWindows 虛擬機器連線](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. <span data-ttu-id="da87a-146">hello 傳統入口網站會提示您 tooopen 或儲存 '.rdp' 副檔名的檔案，這是使用的 tooconnect toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="da87a-146">hello classic portal prompts you tooopen or save a file with a '.rdp' extension, which is used tooconnect toohello virtual machine.</span></span> <span data-ttu-id="da87a-147">下載完成時，請按一下 tooopen hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="da87a-147">Click tooopen hello file when it has finished downloading.</span></span>
3. <span data-ttu-id="da87a-148">在 hello 登入提示字元中使用 hello 屬於 toohello ' AAD DC Administrators' 群組的使用者認證。</span><span class="sxs-lookup"><span data-stu-id="da87a-148">At hello login prompt, use hello credentials of a user belonging toohello 'AAD DC Administrators' group.</span></span> <span data-ttu-id="da87a-149">例如，使用 'bob@domainservicespreview.onmicrosoft.com' 在我們的案例。</span><span class="sxs-lookup"><span data-stu-id="da87a-149">For example, we use 'bob@domainservicespreview.onmicrosoft.com' in our case.</span></span>
4. <span data-ttu-id="da87a-150">從 hello 開始 畫面開啟**伺服器管理員**。</span><span class="sxs-lookup"><span data-stu-id="da87a-150">From hello Start screen, open **Server Manager**.</span></span> <span data-ttu-id="da87a-151">按一下**新增角色及功能**hello hello 伺服器管理員 視窗的中央窗格中。</span><span class="sxs-lookup"><span data-stu-id="da87a-151">Click **Add Roles and Features** in hello central pane of hello Server Manager window.</span></span>

    ![啟動虛擬機器上的伺服器管理員](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager.png)
5. <span data-ttu-id="da87a-153">在 hello**在您開始前**hello 頁面**新增角色及功能精靈**，按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="da87a-153">On hello **Before You Begin** page of hello **Add Roles and Features Wizard**, click **Next**.</span></span>

    ![[開始之前] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-begin.png)
6. <span data-ttu-id="da87a-155">在 hello**安裝類型**頁面上，保留 hello**角色型或功能型安裝**檢查的選項，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="da87a-155">On hello **Installation Type** page, leave hello **Role-based or feature-based installation** option checked and click **Next**.</span></span>

    ![[安裝類型] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-type.png)
7. <span data-ttu-id="da87a-157">在 hello**伺服器選取項目**頁面上，選取 hello 目前虛擬機器從 hello 伺服器集區，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="da87a-157">On hello **Server Selection** page, select hello current virtual machine from hello server pool, and click **Next**.</span></span>

    ![[伺服器選擇] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-server.png)
8. <span data-ttu-id="da87a-159">在 hello**伺服器角色**頁面上，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="da87a-159">On hello **Server Roles** page, click **Next**.</span></span> <span data-ttu-id="da87a-160">我們請略過此頁面，因為我們 hello 伺服器上未安裝任何角色。</span><span class="sxs-lookup"><span data-stu-id="da87a-160">We skip this page since we are not installing any roles on hello server.</span></span>
9. <span data-ttu-id="da87a-161">在 hello**功能**頁面上，按一下 tooexpand hello**遠端伺服器管理工具**節點，然後按一下tooexpand hello**角色管理工具**節點。</span><span class="sxs-lookup"><span data-stu-id="da87a-161">On hello **Features** page, click tooexpand hello **Remote Server Administration Tools** node and then click tooexpand hello **Role Administration Tools** node.</span></span> <span data-ttu-id="da87a-162">選取**AD DS 與 AD LDS 工具**hello 清單中的角色管理工具的功能。</span><span class="sxs-lookup"><span data-stu-id="da87a-162">Select **AD DS and AD LDS Tools** feature from hello list of role administration tools.</span></span>

    ![[功能] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-ad-tools.png)
10. <span data-ttu-id="da87a-164">在 hello**確認**頁面上，按一下**安裝**tooinstall hello AD 與 AD LDS 工具功能 hello 虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="da87a-164">On hello **Confirmation** page, click **Install** tooinstall hello AD and AD LDS tools feature on hello virtual machine.</span></span> <span data-ttu-id="da87a-165">功能安裝成功完成時，按一下**關閉**tooexit hello**新增角色及功能**精靈。</span><span class="sxs-lookup"><span data-stu-id="da87a-165">When feature installation completes successfully, click **Close** tooexit hello **Add Roles and Features** wizard.</span></span>

    ![確認電子郵件](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-confirmation.png)

## <a name="task-3---connect-tooand-explore-hello-managed-domain"></a><span data-ttu-id="da87a-167">工作 3-連接 tooand 瀏覽 hello 受管理的網域</span><span class="sxs-lookup"><span data-stu-id="da87a-167">Task 3 - Connect tooand explore hello managed domain</span></span>
<span data-ttu-id="da87a-168">既然 hello AD 系統管理工具安裝在 hello 已加入網域的虛擬機器，我們可以使用這些工具 tooexplore 及管理 hello 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="da87a-168">Now that hello AD Administrative Tools are installed on hello domain joined virtual machine, we can use these tools tooexplore and administer hello managed domain.</span></span>

> [!NOTE]
> <span data-ttu-id="da87a-169">您需要 toobe 成員 hello ' AAD DC Administrators' 群組的 tooadminister hello 管理網域。</span><span class="sxs-lookup"><span data-stu-id="da87a-169">You need toobe a member of hello 'AAD DC Administrators' group, tooadminister hello managed domain.</span></span>
>
>

1. <span data-ttu-id="da87a-170">從 hello 開始畫面上，按一下 **系統管理工具**。</span><span class="sxs-lookup"><span data-stu-id="da87a-170">From hello Start screen, click **Administrative Tools**.</span></span> <span data-ttu-id="da87a-171">您應該會看到 hello AD hello 虛擬機器上安裝的系統管理工具。</span><span class="sxs-lookup"><span data-stu-id="da87a-171">You should see hello AD administrative tools installed on hello virtual machine.</span></span>

    ![安裝在伺服器上的系統管理工具](./media/active-directory-domain-services-admin-guide/install-rsat-admin-tools-installed.png)
2. <span data-ttu-id="da87a-173">按一下 [Active Directory 管理中心] 。</span><span class="sxs-lookup"><span data-stu-id="da87a-173">Click **Active Directory Administrative Center**.</span></span>

    ![Active Directory 管理中心](./media/active-directory-domain-services-admin-guide/adac-overview.png)
3. <span data-ttu-id="da87a-175">tooexplore hello 網域中，按一下 hello hello 左窗格 (例如，' contoso100.com') 中的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="da87a-175">tooexplore hello domain, click hello domain name in hello left pane (for example, 'contoso100.com').</span></span> <span data-ttu-id="da87a-176">請注意分別稱為「AADDC 電腦」和「AADDC 使用者」的兩個容器。</span><span class="sxs-lookup"><span data-stu-id="da87a-176">Notice two containers called 'AADDC Computers' and 'AADDC Users' respectively.</span></span>

    ![ADAC - 檢視網域](./media/active-directory-domain-services-admin-guide/adac-domain-view.png)
4. <span data-ttu-id="da87a-178">按一下稱為 hello 容器**AADDC 使用者**toosee 所有使用者和群組屬於 toohello 受都管理網域。</span><span class="sxs-lookup"><span data-stu-id="da87a-178">Click hello container called **AADDC Users** toosee all users and groups belonging toohello managed domain.</span></span> <span data-ttu-id="da87a-179">在此容器中，您應該會看到您的 Azure AD 租用戶中的使用者帳戶和群組顯示出來。</span><span class="sxs-lookup"><span data-stu-id="da87a-179">You should see user accounts and groups from your Azure AD tenant show up in this container.</span></span> <span data-ttu-id="da87a-180">請注意，在此範例中，呼叫 'bob' hello 使用者和呼叫 ' AAD DC Administrators' 群組的使用者帳戶是這個容器中。</span><span class="sxs-lookup"><span data-stu-id="da87a-180">Notice in this example, a user account for hello user called 'bob' and a group called 'AAD DC Administrators' are available in this container.</span></span>

    ![ADAC - 網域使用者](./media/active-directory-domain-services-admin-guide/adac-aaddc-users.png)
5. <span data-ttu-id="da87a-182">按一下稱為 hello 容器**AADDC 電腦**toosee hello 電腦加入 toothis 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="da87a-182">Click hello container called **AADDC Computers** toosee hello computers joined toothis managed domain.</span></span> <span data-ttu-id="da87a-183">您應該會看到 hello 目前虛擬機器，也就是聯結的 toohello 網域的項目。</span><span class="sxs-lookup"><span data-stu-id="da87a-183">You should see an entry for hello current virtual machine, which is joined toohello domain.</span></span> <span data-ttu-id="da87a-184">所有電腦的電腦帳戶加入 toohello 受管理的網域會儲存在此 「 AADDC 電腦 」 容器的 Azure AD 網域服務。</span><span class="sxs-lookup"><span data-stu-id="da87a-184">Computer accounts for all computers that are joined toohello Azure AD Domain Services managed domain are stored in this 'AADDC Computers' container.</span></span>

    ![ADAC - 已加入網域的電腦](./media/active-directory-domain-services-admin-guide/adac-aaddc-computers.png)

<br>

## <a name="related-content"></a><span data-ttu-id="da87a-186">相關內容</span><span class="sxs-lookup"><span data-stu-id="da87a-186">Related Content</span></span>
* [<span data-ttu-id="da87a-187">Azure AD Domain Services - 入門指南</span><span class="sxs-lookup"><span data-stu-id="da87a-187">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="da87a-188">加入 Windows Server 虛擬機器 tooan Azure AD 網域服務受管理的網域</span><span class="sxs-lookup"><span data-stu-id="da87a-188">Join a Windows Server virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="da87a-189">部署遠端伺服器管理工具</span><span class="sxs-lookup"><span data-stu-id="da87a-189">Deploy Remote Server Administration Tools</span></span>](https://technet.microsoft.com/library/hh831501.aspx)
