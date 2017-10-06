---
title: "Azure Active Directory Domain Services：管理受管理網域上的 DNS | Microsoft Docs"
description: "管理 Azure Active Directory Domain Services 受管理網域上的 DNS"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: f2085283649eadd3c9e89f708b0eecf10b2d7d70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="administer-dns-on-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="e053f-103">管理 Azure AD 網域服務受管理網域上的 DNS</span><span class="sxs-lookup"><span data-stu-id="e053f-103">Administer DNS on an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="e053f-104">Azure Active Directory 網域服務包括提供 hello 受管理的網域的 DNS 解析的 DNS （網域名稱解析） 伺服器。</span><span class="sxs-lookup"><span data-stu-id="e053f-104">Azure Active Directory Domain Services includes a DNS (Domain Name Resolution) server that provides DNS resolution for hello managed domain.</span></span> <span data-ttu-id="e053f-105">有時候，您可能需要 tooconfigure hello 受管理網域上的 DNS。</span><span class="sxs-lookup"><span data-stu-id="e053f-105">Occasionally, you may need tooconfigure DNS on hello managed domain.</span></span> <span data-ttu-id="e053f-106">未聯結的 toohello 網域的機器設定負載平衡器虛擬 IP 位址，或設定外部 DNS 轉寄站，您可能需要 toocreate DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="e053f-106">You may need toocreate DNS records for machines that are not joined toohello domain, configure virtual IP addresses for load-balancers or setup external DNS forwarders.</span></span> <span data-ttu-id="e053f-107">基於這個理由，屬於 toohello ' AAD DC Administrators' 群組的使用者授與 hello 受管理的網域上的 DNS 管理權限。</span><span class="sxs-lookup"><span data-stu-id="e053f-107">For this reason, users who belong toohello 'AAD DC Administrators' group are granted DNS administration privileges on hello managed domain.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e053f-108">開始之前</span><span class="sxs-lookup"><span data-stu-id="e053f-108">Before you begin</span></span>
<span data-ttu-id="e053f-109">本文所列 tooperform hello 工作，您必須：</span><span class="sxs-lookup"><span data-stu-id="e053f-109">tooperform hello tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="e053f-110">有效的 **Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="e053f-110">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="e053f-111">**Azure AD 目錄** - 與內部部署目錄或僅限雲端的目錄同步處理。</span><span class="sxs-lookup"><span data-stu-id="e053f-111">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="e053f-112">**Azure AD 網域服務**必須啟用 hello Azure AD 目錄。</span><span class="sxs-lookup"><span data-stu-id="e053f-112">**Azure AD Domain Services** must be enabled for hello Azure AD directory.</span></span> <span data-ttu-id="e053f-113">如果您尚未這樣做，請遵循 hello 中所述的所有 hello 工作[入門指南](active-directory-ds-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="e053f-113">If you haven't done so, follow all hello tasks outlined in hello [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="e053f-114">A**已加入網域的虛擬機器**從您管理的 hello Azure AD 網域服務受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="e053f-114">A **domain-joined virtual machine** from which you administer hello Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="e053f-115">如果您沒有這類虛擬機器，請遵循所有 hello 文章的標題中的 hello 工作[加入 Windows 虛擬機器 tooa 受管理的網域](active-directory-ds-admin-guide-join-windows-vm.md)。</span><span class="sxs-lookup"><span data-stu-id="e053f-115">If you don't have such a virtual machine, follow all hello tasks outlined in hello article titled [Join a Windows virtual machine tooa managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>
5. <span data-ttu-id="e053f-116">您需要 hello 認證**使用者帳戶隸屬 toohello ' AAD DC Administrators' 群組**目錄，tooadminister DNS 的受管理的網域中。</span><span class="sxs-lookup"><span data-stu-id="e053f-116">You need hello credentials of a **user account belonging toohello 'AAD DC Administrators' group** in your directory, tooadminister DNS for your managed domain.</span></span>

<br>

## <a name="task-1---provision-a-domain-joined-virtual-machine-tooremotely-administer-dns-for-hello-managed-domain"></a><span data-ttu-id="e053f-117">工作 1-佈建已加入網域的虛擬機器 tooremotely 管理 DNS 的 hello 受管理的網域</span><span class="sxs-lookup"><span data-stu-id="e053f-117">Task 1 - Provision a domain-joined virtual machine tooremotely administer DNS for hello managed domain</span></span>
<span data-ttu-id="e053f-118">可以從遠端使用熟悉的 Active Directory 系統管理工具例如 hello Active Directory 管理中心 (ADAC) 或 AD PowerShell 管理 azure AD 網域服務受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="e053f-118">Azure AD Domain Services managed domains can be managed remotely using familiar Active Directory administrative tools such as hello Active Directory Administrative Center (ADAC) or AD PowerShell.</span></span> <span data-ttu-id="e053f-119">同樣地，可以使用 hello DNS 伺服器管理工具，從遠端管理 hello 受管理的網域的 DNS。</span><span class="sxs-lookup"><span data-stu-id="e053f-119">Similarly, DNS for hello managed domain can be administered remotely using hello DNS Server administration tools.</span></span>

<span data-ttu-id="e053f-120">Azure AD 目錄中的系統管理員沒有 hello 透過遠端桌面的受管理網域的權限 tooconnect toodomain 控制站。</span><span class="sxs-lookup"><span data-stu-id="e053f-120">Administrators in your Azure AD directory do not have privileges tooconnect toodomain controllers on hello managed domain via Remote Desktop.</span></span> <span data-ttu-id="e053f-121">Hello ' AAD DC Administrators' 群組的成員可以管理 DNS 的受管理的網域從遠端使用聯結的 toohello 受管理的網域的 Windows 伺服器/用戶端電腦的 DNS 伺服器工具。</span><span class="sxs-lookup"><span data-stu-id="e053f-121">Members of hello 'AAD DC Administrators' group can administer DNS for managed domains remotely using DNS Server tools from a Windows Server/client computer that is joined toohello managed domain.</span></span> <span data-ttu-id="e053f-122">DNS 伺服器工具可以安裝在 Windows Server 上 hello 遠端伺服器管理工具 (RSAT) 選擇性功能的一部分，而且用戶端電腦加入 toohello 受管理網域。</span><span class="sxs-lookup"><span data-stu-id="e053f-122">DNS Server tools can be installed as part of hello Remote Server Administration Tools (RSAT) optional feature on Windows Server and client machines joined toohello managed domain.</span></span>

<span data-ttu-id="e053f-123">hello 第一項工作是 tooprovision 是聯結的 toohello 受管理的網域 Windows Server 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e053f-123">hello first task is tooprovision a Windows Server virtual machine that is joined toohello managed domain.</span></span> <span data-ttu-id="e053f-124">如需指示，請參閱 toohello 文章 <<c0> [ 加入 Windows Server 虛擬機器 tooan Azure AD 網域服務受管理的網域](active-directory-ds-admin-guide-join-windows-vm.md)。</span><span class="sxs-lookup"><span data-stu-id="e053f-124">For instructions, refer toohello article titled [join a Windows Server virtual machine tooan Azure AD Domain Services managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>

## <a name="task-2---install-dns-server-tools-on-hello-virtual-machine"></a><span data-ttu-id="e053f-125">工作 2-hello 虛擬機器上安裝 DNS 伺服器工具</span><span class="sxs-lookup"><span data-stu-id="e053f-125">Task 2 - Install DNS Server tools on hello virtual machine</span></span>
<span data-ttu-id="e053f-126">執行下列步驟 tooinstall hello DNS 系統管理工具 hello 已加入網域的虛擬機器上的 hello。</span><span class="sxs-lookup"><span data-stu-id="e053f-126">Perform hello following steps tooinstall hello DNS Administration tools on hello domain joined virtual machine.</span></span> <span data-ttu-id="e053f-127">如需有關[安裝和使用遠端伺服器管理工具](https://technet.microsoft.com/library/hh831501.aspx)的詳細資訊，請參閱 TechNet。</span><span class="sxs-lookup"><span data-stu-id="e053f-127">For more information on [installing and using Remote Server Administration Tools](https://technet.microsoft.com/library/hh831501.aspx), see Technet.</span></span>

1. <span data-ttu-id="e053f-128">瀏覽過**虛擬機器**hello Azure 傳統入口網站中的節點。</span><span class="sxs-lookup"><span data-stu-id="e053f-128">Navigate too**Virtual Machines** node in hello Azure classic portal.</span></span> <span data-ttu-id="e053f-129">選取您在工作 1 中建立的 hello 虛擬機器，然後按一下**連接**hello 在 hello hello 視窗底部的命令列上。</span><span class="sxs-lookup"><span data-stu-id="e053f-129">Select hello virtual machine you created in Task 1 and click **Connect** on hello command bar at hello bottom of hello window.</span></span>

    ![TooWindows 虛擬機器連線](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. <span data-ttu-id="e053f-131">hello 傳統入口網站會提示您 tooopen 或儲存 '.rdp' 副檔名的檔案，這是使用的 tooconnect toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e053f-131">hello classic portal prompts you tooopen or save a file with a '.rdp' extension, which is used tooconnect toohello virtual machine.</span></span> <span data-ttu-id="e053f-132">下載完成時，請按一下 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="e053f-132">Click hello file when it has finished downloading.</span></span>
3. <span data-ttu-id="e053f-133">在 hello 登入提示字元中使用 hello 屬於 toohello ' AAD DC Administrators' 群組的使用者認證。</span><span class="sxs-lookup"><span data-stu-id="e053f-133">At hello login prompt, use hello credentials of a user belonging toohello 'AAD DC Administrators' group.</span></span> <span data-ttu-id="e053f-134">例如，使用 'bob@domainservicespreview.onmicrosoft.com' 在我們的案例。</span><span class="sxs-lookup"><span data-stu-id="e053f-134">For example, we use 'bob@domainservicespreview.onmicrosoft.com' in our case.</span></span>
4. <span data-ttu-id="e053f-135">從 hello 開始] 畫面開啟**伺服器管理員**。</span><span class="sxs-lookup"><span data-stu-id="e053f-135">From hello Start screen, open **Server Manager**.</span></span> <span data-ttu-id="e053f-136">按一下**新增角色及功能**hello hello 伺服器管理員] 視窗的中央窗格中。</span><span class="sxs-lookup"><span data-stu-id="e053f-136">Click **Add Roles and Features** in hello central pane of hello Server Manager window.</span></span>

    ![啟動虛擬機器上的伺服器管理員](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager.png)
5. <span data-ttu-id="e053f-138">在 hello**在您開始前**hello 頁面**新增角色及功能精靈**，按一下 [**下一步**。</span><span class="sxs-lookup"><span data-stu-id="e053f-138">On hello **Before You Begin** page of hello **Add Roles and Features Wizard**, click **Next**.</span></span>

    ![[開始之前] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-begin.png)
6. <span data-ttu-id="e053f-140">在 [hello**安裝類型**頁面上，保留 hello**角色型或功能型安裝**檢查的選項，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="e053f-140">On hello **Installation Type** page, leave hello **Role-based or feature-based installation** option checked and click **Next**.</span></span>

    ![[安裝類型] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-type.png)
7. <span data-ttu-id="e053f-142">在 [hello**伺服器選取項目**頁面上，選取 hello 目前虛擬機器從 hello 伺服器集區，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="e053f-142">On hello **Server Selection** page, select hello current virtual machine from hello server pool, and click **Next**.</span></span>

    ![[伺服器選擇] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-server.png)
8. <span data-ttu-id="e053f-144">在 [hello**伺服器角色**頁面上，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="e053f-144">On hello **Server Roles** page, click **Next**.</span></span> <span data-ttu-id="e053f-145">我們請略過此頁面，因為我們 hello 伺服器上未安裝任何角色。</span><span class="sxs-lookup"><span data-stu-id="e053f-145">We skip this page since we are not installing any roles on hello server.</span></span>
9. <span data-ttu-id="e053f-146">在 [hello**功能**頁面上，按一下 tooexpand hello**遠端伺服器管理工具**節點，然後按一下 [tooexpand hello**角色管理工具**節點。</span><span class="sxs-lookup"><span data-stu-id="e053f-146">On hello **Features** page, click tooexpand hello **Remote Server Administration Tools** node and then click tooexpand hello **Role Administration Tools** node.</span></span> <span data-ttu-id="e053f-147">選取**DNS 伺服器工具**hello 清單中的角色管理工具的功能。</span><span class="sxs-lookup"><span data-stu-id="e053f-147">Select **DNS Server Tools** feature from hello list of role administration tools.</span></span>

    ![[功能] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-dns-tools.png)
10. <span data-ttu-id="e053f-149">在 [hello**確認**頁面上，按一下**安裝**tooinstall hello DNS 伺服器工具功能 hello 虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="e053f-149">On hello **Confirmation** page, click **Install** tooinstall hello DNS Server tools feature on hello virtual machine.</span></span> <span data-ttu-id="e053f-150">功能安裝成功完成時，按一下**關閉**tooexit hello**新增角色及功能**精靈。</span><span class="sxs-lookup"><span data-stu-id="e053f-150">When feature installation completes successfully, click **Close** tooexit hello **Add Roles and Features** wizard.</span></span>

    ![確認電子郵件](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-dns-confirmation.png)

## <a name="task-3---launch-hello-dns-management-console-tooadminister-dns"></a><span data-ttu-id="e053f-152">工作 3-啟動 hello DNS 管理主控台 tooadminister DNS</span><span class="sxs-lookup"><span data-stu-id="e053f-152">Task 3 - Launch hello DNS management console tooadminister DNS</span></span>
<span data-ttu-id="e053f-153">既然 hello DNS 伺服器工具安裝功能 hello 已加入網域的虛擬機器，我們可以使用 hello DNS 工具 tooadminister DNS 受管理的 hello 網域上。</span><span class="sxs-lookup"><span data-stu-id="e053f-153">Now that hello DNS Server Tools feature is installed on hello domain joined virtual machine, we can use hello DNS tools tooadminister DNS on hello managed domain.</span></span>

> [!NOTE]
> <span data-ttu-id="e053f-154">您需要 toobe tooadminister hello 受管理的網域上的 DNS hello ' AAD DC Administrators' 群組的成員。</span><span class="sxs-lookup"><span data-stu-id="e053f-154">You need toobe a member of hello 'AAD DC Administrators' group, tooadminister DNS on hello managed domain.</span></span>
>
>

1. <span data-ttu-id="e053f-155">從 hello 開始畫面上，按一下 [**系統管理工具**。</span><span class="sxs-lookup"><span data-stu-id="e053f-155">From hello Start screen, click **Administrative Tools**.</span></span> <span data-ttu-id="e053f-156">您應該會看見 hello **DNS** hello 虛擬機器上安裝主控台。</span><span class="sxs-lookup"><span data-stu-id="e053f-156">You should see hello **DNS** console installed on hello virtual machine.</span></span>

    ![系統管理工具 - DNS 主控台](./media/active-directory-domain-services-admin-guide/install-rsat-dns-tools-installed.png)
2. <span data-ttu-id="e053f-158">按一下**DNS** toolaunch hello DNS 管理主控台。</span><span class="sxs-lookup"><span data-stu-id="e053f-158">Click **DNS** toolaunch hello DNS Management console.</span></span>
3. <span data-ttu-id="e053f-159">在 hello**連接 tooDNS 伺服器**] 對話方塊中，按一下標題為 hello 選項**hello 下列電腦**，然後輸入 hello DNS 網域名稱的 hello 受管理的網域 (例如，' contoso100.com')。</span><span class="sxs-lookup"><span data-stu-id="e053f-159">In hello **Connect tooDNS Server** dialog, click hello option titled **hello following computer**, and enter hello DNS domain name of hello managed domain (for example, 'contoso100.com').</span></span>

    ![DNS 主控台-連接 toodomain](./media/active-directory-domain-services-admin-guide/dns-console-connect-to-domain.png)
4. <span data-ttu-id="e053f-161">hello DNS 主控台連接 toohello 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="e053f-161">hello DNS Console connects toohello managed domain.</span></span>

    ![DNS 主控台 - 管理網域](./media/active-directory-domain-services-admin-guide/dns-console-managed-domain.png)
5. <span data-ttu-id="e053f-163">您現在可以使用 hello DNS 主控台 tooadd DNS 項目已啟用 AAD 網域服務的 hello 虛擬網路內的電腦。</span><span class="sxs-lookup"><span data-stu-id="e053f-163">You can now use hello DNS console tooadd DNS entries for computers within hello virtual network in which you've enabled AAD Domain Services.</span></span>

> [!WARNING]
> <span data-ttu-id="e053f-164">管理 DNS hello 受管理的網域使用 DNS 系統管理工具時，請格外小心。</span><span class="sxs-lookup"><span data-stu-id="e053f-164">Be careful when administering DNS for hello managed domain using DNS administration tools.</span></span> <span data-ttu-id="e053f-165">請確定您**請勿刪除或修改 hello 內建的 DNS 記錄所使用的 hello 網域中的網域服務**。</span><span class="sxs-lookup"><span data-stu-id="e053f-165">Ensure that you **do not delete or modify hello built-in DNS records that are used by Domain Services in hello domain**.</span></span> <span data-ttu-id="e053f-166">內建 DNS 記錄包括網域 DNS 記錄、名稱伺服器記錄和其他用於 DC 位置的記錄。</span><span class="sxs-lookup"><span data-stu-id="e053f-166">Built-in DNS records include domain DNS records, name server records, and other records used for DC location.</span></span> <span data-ttu-id="e053f-167">如果您修改這些記錄，網域服務也會受到干擾 hello 虛擬網路上。</span><span class="sxs-lookup"><span data-stu-id="e053f-167">If you modify these records, domain services are disrupted on hello virtual network.</span></span>
>
>

<span data-ttu-id="e053f-168">請參閱 hello [Technet 文章 DNS 工具](https://technet.microsoft.com/library/cc753579.aspx)如需管理 DNS 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="e053f-168">See hello [DNS tools article on Technet](https://technet.microsoft.com/library/cc753579.aspx) for more information about managing DNS.</span></span>

## <a name="related-content"></a><span data-ttu-id="e053f-169">相關內容</span><span class="sxs-lookup"><span data-stu-id="e053f-169">Related Content</span></span>
* [<span data-ttu-id="e053f-170">Azure AD Domain Services - 入門指南</span><span class="sxs-lookup"><span data-stu-id="e053f-170">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="e053f-171">加入 Windows Server 虛擬機器 tooan Azure AD 網域服務受管理的網域</span><span class="sxs-lookup"><span data-stu-id="e053f-171">Join a Windows Server virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="e053f-172">Administer an Azure AD Domain Services managed domain (管理 Azure AD 網域服務受管理的網域)</span><span class="sxs-lookup"><span data-stu-id="e053f-172">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="e053f-173">DNS 系統管理工具</span><span class="sxs-lookup"><span data-stu-id="e053f-173">DNS administration tools</span></span>](https://technet.microsoft.com/library/cc753579.aspx)
