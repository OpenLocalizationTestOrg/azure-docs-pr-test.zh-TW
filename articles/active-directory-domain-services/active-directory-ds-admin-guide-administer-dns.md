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
ms.openlocfilehash: 812641a3e4d5bf496d81b036d326595c5722b7fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="administer-dns-on-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="b9b9c-103">管理 Azure AD 網域服務受管理網域上的 DNS</span><span class="sxs-lookup"><span data-stu-id="b9b9c-103">Administer DNS on an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="b9b9c-104">Azure Active Directory 網域服務包括可為受管理網域提供 DNS 解析的 DNS (網域名稱解析) 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-104">Azure Active Directory Domain Services includes a DNS (Domain Name Resolution) server that provides DNS resolution for the managed domain.</span></span> <span data-ttu-id="b9b9c-105">有時候，您可能需要在受管理網域上設定 DNS。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-105">Occasionally, you may need to configure DNS on the managed domain.</span></span> <span data-ttu-id="b9b9c-106">您可能需要為未新增網域的機器建立 DNS 記錄、設定負載平衡器的虛擬 IP 位址，或設定外部 DNS 轉寄站。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-106">You may need to create DNS records for machines that are not joined to the domain, configure virtual IP addresses for load-balancers or setup external DNS forwarders.</span></span> <span data-ttu-id="b9b9c-107">基於這個理由，屬於「AAD DC 系統管理員」群組的使用者會獲授與受管理網域上的 DNS 系統管理權限。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-107">For this reason, users who belong to the 'AAD DC Administrators' group are granted DNS administration privileges on the managed domain.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b9b9c-108">開始之前</span><span class="sxs-lookup"><span data-stu-id="b9b9c-108">Before you begin</span></span>
<span data-ttu-id="b9b9c-109">若要執行本文中所列的工作，您需要︰</span><span class="sxs-lookup"><span data-stu-id="b9b9c-109">To perform the tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="b9b9c-110">有效的 **Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-110">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="b9b9c-111">**Azure AD 目錄** - 與內部部署目錄或僅限雲端的目錄同步處理。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-111">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="b9b9c-112">**Azure AD 網域服務** 必須已針對 Azure AD 目錄啟用。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-112">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span></span> <span data-ttu-id="b9b9c-113">如果還沒有啟用，請按照 [入門指南](active-directory-ds-getting-started.md)所述的所有工作來進行。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-113">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="b9b9c-114">**已加入網域的虛擬機器** ，您可在其中管理 Azure AD 網域服務受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-114">A **domain-joined virtual machine** from which you administer the Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="b9b9c-115">如果您沒有這類虛擬機器，請依照名為[將 Windows 虛擬機器加入受管理的網域](active-directory-ds-admin-guide-join-windows-vm.md)一文所述的所有工作進行操作。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-115">If you don't have such a virtual machine, follow all the tasks outlined in the article titled [Join a Windows virtual machine to a managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>
5. <span data-ttu-id="b9b9c-116">您需要目錄中 **屬於「AAD DC 系統管理員」群組之使用者帳戶** 的認證，才能管理受管理網域的 DNS。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-116">You need the credentials of a **user account belonging to the 'AAD DC Administrators' group** in your directory, to administer DNS for your managed domain.</span></span>

<br>

## <a name="task-1---provision-a-domain-joined-virtual-machine-to-remotely-administer-dns-for-the-managed-domain"></a><span data-ttu-id="b9b9c-117">工作 1 - 佈建已加入網域的虛擬機器以從遠端管理受管理網域的 DNS</span><span class="sxs-lookup"><span data-stu-id="b9b9c-117">Task 1 - Provision a domain-joined virtual machine to remotely administer DNS for the managed domain</span></span>
<span data-ttu-id="b9b9c-118">使用 Active Directory 管理中心 (ADAC) 或 AD PowerShell 等熟悉的 Active Directory 系統管理工具，可以從遠端管理 Azure AD 網域服務受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-118">Azure AD Domain Services managed domains can be managed remotely using familiar Active Directory administrative tools such as the Active Directory Administrative Center (ADAC) or AD PowerShell.</span></span> <span data-ttu-id="b9b9c-119">同樣地，使用 DNS 伺服器系統管理工具，可以從遠端管理受管理網域的 DNS。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-119">Similarly, DNS for the managed domain can be administered remotely using the DNS Server administration tools.</span></span>

<span data-ttu-id="b9b9c-120">Azure AD 目錄中的系統管理員沒有權限，不能透過遠端桌面連接受管理網域上的網域控制站。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-120">Administrators in your Azure AD directory do not have privileges to connect to domain controllers on the managed domain via Remote Desktop.</span></span> <span data-ttu-id="b9b9c-121">「AAD DC 系統管理員」群組的成員可以使用 DNS 伺服器工具，從已加入受管理網域的 Windows Server/用戶端電腦遠端管理受管理網域的 DNS。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-121">Members of the 'AAD DC Administrators' group can administer DNS for managed domains remotely using DNS Server tools from a Windows Server/client computer that is joined to the managed domain.</span></span> <span data-ttu-id="b9b9c-122">在已加入受管理網域的 Windows Server 和用戶端電腦上，可以將 DNS 伺服器工具安裝做為遠端伺服器管理工具 (RSAT) 選擇性功能的一部分。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-122">DNS Server tools can be installed as part of the Remote Server Administration Tools (RSAT) optional feature on Windows Server and client machines joined to the managed domain.</span></span>

<span data-ttu-id="b9b9c-123">第一個工作是佈建已加入受管理網域的 Windows Server 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-123">The first task is to provision a Windows Server virtual machine that is joined to the managed domain.</span></span> <span data-ttu-id="b9b9c-124">如需相關指示，請參閱標題為 [將 Windows Server 虛擬機器加入 Azure AD 網域服務受管理網域](active-directory-ds-admin-guide-join-windows-vm.md)的文章。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-124">For instructions, refer to the article titled [join a Windows Server virtual machine to an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>

## <a name="task-2---install-dns-server-tools-on-the-virtual-machine"></a><span data-ttu-id="b9b9c-125">工作 2 - 在虛擬機器上安裝 DNS 伺服器工具</span><span class="sxs-lookup"><span data-stu-id="b9b9c-125">Task 2 - Install DNS Server tools on the virtual machine</span></span>
<span data-ttu-id="b9b9c-126">請執行下列步驟，以在已加入網域的虛擬機器上安裝 DNS 系統管理工具。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-126">Perform the following steps to install the DNS Administration tools on the domain joined virtual machine.</span></span> <span data-ttu-id="b9b9c-127">如需有關[安裝和使用遠端伺服器管理工具](https://technet.microsoft.com/library/hh831501.aspx)的詳細資訊，請參閱 TechNet。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-127">For more information on [installing and using Remote Server Administration Tools](https://technet.microsoft.com/library/hh831501.aspx), see Technet.</span></span>

1. <span data-ttu-id="b9b9c-128">在 Azure 傳統入口網站中瀏覽至 [虛擬機器]  節點。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-128">Navigate to **Virtual Machines** node in the Azure classic portal.</span></span> <span data-ttu-id="b9b9c-129">選取您在工作 1 建立的虛擬機器，然後按一下視窗底部命令列上的 [連線]  。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-129">Select the virtual machine you created in Task 1 and click **Connect** on the command bar at the bottom of the window.</span></span>

    ![連線至 Windows 虛擬機器](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. <span data-ttu-id="b9b9c-131">傳統入口網站會提示您開啟或儲存副檔名為 '.rdp' 的檔案，其可供用來連線到虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-131">The classic portal prompts you to open or save a file with a '.rdp' extension, which is used to connect to the virtual machine.</span></span> <span data-ttu-id="b9b9c-132">在檔案下載完成時，按一下該檔案。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-132">Click the file when it has finished downloading.</span></span>
3. <span data-ttu-id="b9b9c-133">在登入提示中，使用屬於「AAD DC 系統管理員」群組之使用者的認證。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-133">At the login prompt, use the credentials of a user belonging to the 'AAD DC Administrators' group.</span></span> <span data-ttu-id="b9b9c-134">例如，使用 'bob@domainservicespreview.onmicrosoft.com' 在我們的案例。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-134">For example, we use 'bob@domainservicespreview.onmicrosoft.com' in our case.</span></span>
4. <span data-ttu-id="b9b9c-135">在 [開始] 畫面中開啟 [伺服器管理員] 。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-135">From the Start screen, open **Server Manager**.</span></span> <span data-ttu-id="b9b9c-136">按一下 [伺服器管理員] 視窗中央窗格內的 [新增角色及功能]  。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-136">Click **Add Roles and Features** in the central pane of the Server Manager window.</span></span>

    ![啟動虛擬機器上的伺服器管理員](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager.png)
5. <span data-ttu-id="b9b9c-138">在 [新增角色及功能精靈] 的 [開始之前] 頁面上，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-138">On the **Before You Begin** page of the **Add Roles and Features Wizard**, click **Next**.</span></span>

    ![[開始之前] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-begin.png)
6. <span data-ttu-id="b9b9c-140">在 [安裝類型] 頁面上，保持勾選 [角色型或功能型安裝] 選項，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-140">On the **Installation Type** page, leave the **Role-based or feature-based installation** option checked and click **Next**.</span></span>

    ![[安裝類型] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-type.png)
7. <span data-ttu-id="b9b9c-142">在 [伺服器選擇] 頁面上，從伺服器集區中選取目前的虛擬機器，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-142">On the **Server Selection** page, select the current virtual machine from the server pool, and click **Next**.</span></span>

    ![[伺服器選擇] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-server.png)
8. <span data-ttu-id="b9b9c-144">在 [伺服器角色] 頁面上，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-144">On the **Server Roles** page, click **Next**.</span></span> <span data-ttu-id="b9b9c-145">我們會略過此頁面，因為我們沒有要在伺服器上安裝任何角色。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-145">We skip this page since we are not installing any roles on the server.</span></span>
9. <span data-ttu-id="b9b9c-146">在 [功能] 頁面上，按一下以展開 [遠端伺服器管理工具] 節點，然後按一下以展開 [角色管理工具] 節點。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-146">On the **Features** page, click to expand the **Remote Server Administration Tools** node and then click to expand the **Role Administration Tools** node.</span></span> <span data-ttu-id="b9b9c-147">從角色管理工具清單中，選取 [DNS 伺服器工具] 功能。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-147">Select **DNS Server Tools** feature from the list of role administration tools.</span></span>

    ![[功能] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-dns-tools.png)
10. <span data-ttu-id="b9b9c-149">在 [確認] 頁面上，按一下 [安裝] 以在虛擬機器上安裝 DNS 伺服器工具功能。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-149">On the **Confirmation** page, click **Install** to install the DNS Server tools feature on the virtual machine.</span></span> <span data-ttu-id="b9b9c-150">順利完成功能安裝時，按一下 [關閉] 以結束 [新增角色及功能] 精靈。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-150">When feature installation completes successfully, click **Close** to exit the **Add Roles and Features** wizard.</span></span>

    ![確認電子郵件](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-dns-confirmation.png)

## <a name="task-3---launch-the-dns-management-console-to-administer-dns"></a><span data-ttu-id="b9b9c-152">工作 3 - 啟動 DNS 管理主控台來管理 DNS</span><span class="sxs-lookup"><span data-stu-id="b9b9c-152">Task 3 - Launch the DNS management console to administer DNS</span></span>
<span data-ttu-id="b9b9c-153">既然加入網域的虛擬機器上已安裝了 [DNS 伺服器工具] 功能，我們就可以使用 DNS 工具來管理受管理網域上的 DNS。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-153">Now that the DNS Server Tools feature is installed on the domain joined virtual machine, we can use the DNS tools to administer DNS on the managed domain.</span></span>

> [!NOTE]
> <span data-ttu-id="b9b9c-154">您必須是「AAD DC 系統管理員」群組的成員，才能在受管理的網域上管理 DNS。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-154">You need to be a member of the 'AAD DC Administrators' group, to administer DNS on the managed domain.</span></span>
>
>

1. <span data-ttu-id="b9b9c-155">從 [開始] 畫面中，按一下 [系統管理工具] 。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-155">From the Start screen, click **Administrative Tools**.</span></span> <span data-ttu-id="b9b9c-156">您應該會看到安裝在虛擬機器上的 [DNS]  主控台。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-156">You should see the **DNS** console installed on the virtual machine.</span></span>

    ![系統管理工具 - DNS 主控台](./media/active-directory-domain-services-admin-guide/install-rsat-dns-tools-installed.png)
2. <span data-ttu-id="b9b9c-158">按一下 [DNS]  以啟動 DNS 管理主控台。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-158">Click **DNS** to launch the DNS Management console.</span></span>
3. <span data-ttu-id="b9b9c-159">在 [連線到 DNS 伺服器] 對話方塊中，按一下標題為 [下列電腦] 的選項，然後輸入受管理網域的 DNS 網域名稱 (例如 'contoso100.com')。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-159">In the **Connect to DNS Server** dialog, click the option titled **The following computer**, and enter the DNS domain name of the managed domain (for example, 'contoso100.com').</span></span>

    ![DNS 主控台 - 連線到網域](./media/active-directory-domain-services-admin-guide/dns-console-connect-to-domain.png)
4. <span data-ttu-id="b9b9c-161">DNS 主控台連線到受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-161">The DNS Console connects to the managed domain.</span></span>

    ![DNS 主控台 - 管理網域](./media/active-directory-domain-services-admin-guide/dns-console-managed-domain.png)
5. <span data-ttu-id="b9b9c-163">您現在可以使用 DNS 主控台來為已在其中啟用 AAD 網域服務之虛擬網路內的電腦新增 DNS 項目。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-163">You can now use the DNS console to add DNS entries for computers within the virtual network in which you've enabled AAD Domain Services.</span></span>

> [!WARNING]
> <span data-ttu-id="b9b9c-164">使用 DNS 管理工具來管理受管理網域的 DNS 時，請務必小心。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-164">Be careful when administering DNS for the managed domain using DNS administration tools.</span></span> <span data-ttu-id="b9b9c-165">務必要確定您 **並未刪除或修改網域中的網域服務所使用的內建 DNS 記錄**。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-165">Ensure that you **do not delete or modify the built-in DNS records that are used by Domain Services in the domain**.</span></span> <span data-ttu-id="b9b9c-166">內建 DNS 記錄包括網域 DNS 記錄、名稱伺服器記錄和其他用於 DC 位置的記錄。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-166">Built-in DNS records include domain DNS records, name server records, and other records used for DC location.</span></span> <span data-ttu-id="b9b9c-167">如果您修改這些記錄，虛擬網路上的網域服務會中斷。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-167">If you modify these records, domain services are disrupted on the virtual network.</span></span>
>
>

<span data-ttu-id="b9b9c-168">如需有關管理 DNS 的詳細資訊，請參閱 [Technet 上的 DNS 工具文章](https://technet.microsoft.com/library/cc753579.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b9b9c-168">See the [DNS tools article on Technet](https://technet.microsoft.com/library/cc753579.aspx) for more information about managing DNS.</span></span>

## <a name="related-content"></a><span data-ttu-id="b9b9c-169">相關內容</span><span class="sxs-lookup"><span data-stu-id="b9b9c-169">Related Content</span></span>
* [<span data-ttu-id="b9b9c-170">Azure AD Domain Services - 入門指南</span><span class="sxs-lookup"><span data-stu-id="b9b9c-170">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="b9b9c-171">將 Windows Server 虛擬機器加入 Azure AD 網域服務受管理的網域</span><span class="sxs-lookup"><span data-stu-id="b9b9c-171">Join a Windows Server virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="b9b9c-172">Administer an Azure AD Domain Services managed domain (管理 Azure AD 網域服務受管理的網域)</span><span class="sxs-lookup"><span data-stu-id="b9b9c-172">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="b9b9c-173">DNS 系統管理工具</span><span class="sxs-lookup"><span data-stu-id="b9b9c-173">DNS administration tools</span></span>](https://technet.microsoft.com/library/cc753579.aspx)
