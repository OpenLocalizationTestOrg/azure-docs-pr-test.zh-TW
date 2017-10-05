---
title: "Azure Active Directory Domain Services：管理受管理網域上的群組原則 | Microsoft Docs"
description: "管理 Azure Active Directory Domain Services 受管理網域上的群組原則"
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
ms.openlocfilehash: 299e09ef1bb1b1db9d64447bf4537c7c3a3cfd5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="administer-group-policy-on-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="1421e-103">管理 Azure AD Domain Services 受管理網域上的群組原則</span><span class="sxs-lookup"><span data-stu-id="1421e-103">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="1421e-104">Azure Active Directory Domain Services 有「AADDC 使用者」和「AADDC 電腦」容器專用的內建群組原則物件 (GPO)。</span><span class="sxs-lookup"><span data-stu-id="1421e-104">Azure Active Directory Domain Services includes built-in Group Policy Objects (GPOs) for the 'AADDC Users' and 'AADDC Computers' containers.</span></span> <span data-ttu-id="1421e-105">您可以自訂這些內建 GPO，來設定受管理網域上的群組原則。</span><span class="sxs-lookup"><span data-stu-id="1421e-105">You can customize these built-in GPOs to configure Group Policy on the managed domain.</span></span> <span data-ttu-id="1421e-106">此外，「AAD DC 系統管理員」群組的成員可以在受管理網域內建立自己的自定組織單位 (OU)。</span><span class="sxs-lookup"><span data-stu-id="1421e-106">Additionally, members of the 'AAD DC Administrators' group can create their own custom OUs in the managed domain.</span></span> <span data-ttu-id="1421e-107">他們也可以建立自訂 GPO，並將它們連結至這些自訂的 OU。</span><span class="sxs-lookup"><span data-stu-id="1421e-107">They can also create custom GPOs and link them to these custom OUs.</span></span> <span data-ttu-id="1421e-108">屬於「AAD DC 系統管理員」群組的使用者會獲得受管理網域上的「群組原則」系統管理權限。</span><span class="sxs-lookup"><span data-stu-id="1421e-108">Users who belong to the 'AAD DC Administrators' group are granted Group Policy administration privileges on the managed domain.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1421e-109">開始之前</span><span class="sxs-lookup"><span data-stu-id="1421e-109">Before you begin</span></span>
<span data-ttu-id="1421e-110">若要執行本文中所列的工作，您需要︰</span><span class="sxs-lookup"><span data-stu-id="1421e-110">To perform the tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="1421e-111">有效的 **Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="1421e-111">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="1421e-112">**Azure AD 目錄** - 與內部部署目錄或僅限雲端的目錄同步處理。</span><span class="sxs-lookup"><span data-stu-id="1421e-112">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="1421e-113">**Azure AD 網域服務** 必須已針對 Azure AD 目錄啟用。</span><span class="sxs-lookup"><span data-stu-id="1421e-113">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span></span> <span data-ttu-id="1421e-114">如果還沒有啟用，請按照 [入門指南](active-directory-ds-getting-started.md)所述的所有工作來進行。</span><span class="sxs-lookup"><span data-stu-id="1421e-114">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="1421e-115">**已加入網域的虛擬機器** ，您可在其中管理 Azure AD 網域服務受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="1421e-115">A **domain-joined virtual machine** from which you administer the Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="1421e-116">如果您沒有這類虛擬機器，請依照名為[將 Windows 虛擬機器加入受管理的網域](active-directory-ds-admin-guide-join-windows-vm.md)一文所述的所有工作進行操作。</span><span class="sxs-lookup"><span data-stu-id="1421e-116">If you don't have such a virtual machine, follow all the tasks outlined in the article titled [Join a Windows virtual machine to a managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>
5. <span data-ttu-id="1421e-117">您需要目錄中**屬於「AAD DC 系統管理員」群組之使用者帳戶**的認證，才能管理受管理網域的群組原則。</span><span class="sxs-lookup"><span data-stu-id="1421e-117">You need the credentials of a **user account belonging to the 'AAD DC Administrators' group** in your directory, to administer Group Policy for your managed domain.</span></span>

<br>

## <a name="task-1---provision-a-domain-joined-virtual-machine-to-remotely-administer-group-policy-for-the-managed-domain"></a><span data-ttu-id="1421e-118">工作 1 - 佈建已加入網域的虛擬機器以從遠端管理受管理網域的群組原則</span><span class="sxs-lookup"><span data-stu-id="1421e-118">Task 1 - Provision a domain-joined virtual machine to remotely administer Group Policy for the managed domain</span></span>
<span data-ttu-id="1421e-119">使用 Active Directory 管理中心 (ADAC) 或 AD PowerShell 等熟悉的 Active Directory 系統管理工具，可以從遠端管理 Azure AD 網域服務受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="1421e-119">Azure AD Domain Services managed domains can be managed remotely using familiar Active Directory administrative tools such as the Active Directory Administrative Center (ADAC) or AD PowerShell.</span></span> <span data-ttu-id="1421e-120">同樣地，使用群組原則伺服器系統管理工具，可以從遠端管理受管理網域的群組原則。</span><span class="sxs-lookup"><span data-stu-id="1421e-120">Similarly, Group Policy for the managed domain can be administered remotely using the Group Policy administration tools.</span></span>

<span data-ttu-id="1421e-121">Azure AD 目錄中的系統管理員沒有權限，不能透過遠端桌面連接受管理網域上的網域控制站。</span><span class="sxs-lookup"><span data-stu-id="1421e-121">Administrators in your Azure AD directory do not have privileges to connect to domain controllers on the managed domain via Remote Desktop.</span></span> <span data-ttu-id="1421e-122">「AAD DC 系統管理員」群組的成員可以遠端管理受管理網域的群組原則。</span><span class="sxs-lookup"><span data-stu-id="1421e-122">Members of the 'AAD DC Administrators' group can administer Group Policy for managed domains remotely.</span></span> <span data-ttu-id="1421e-123">他們可以使用已加入受管理網域的 Windows Server/用戶端電腦上的群組原則工具。</span><span class="sxs-lookup"><span data-stu-id="1421e-123">They can use Group Policy tools on a Windows Server/client computer joined to the managed domain.</span></span> <span data-ttu-id="1421e-124">可以將群組原則工具安裝為 Windows Server/用戶端電腦 (已加入受管理網域) 上群組原則管理選用功能的一部分。</span><span class="sxs-lookup"><span data-stu-id="1421e-124">Group Policy tools can be installed as part of the Group Policy Management optional feature on Windows Server and client machines joined to the managed domain.</span></span>

<span data-ttu-id="1421e-125">第一個工作是佈建已加入受管理網域的 Windows Server 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1421e-125">The first task is to provision a Windows Server virtual machine that is joined to the managed domain.</span></span> <span data-ttu-id="1421e-126">如需相關指示，請參閱標題為 [將 Windows Server 虛擬機器加入 Azure AD 網域服務受管理網域](active-directory-ds-admin-guide-join-windows-vm.md)的文章。</span><span class="sxs-lookup"><span data-stu-id="1421e-126">For instructions, refer to the article titled [join a Windows Server virtual machine to an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>

## <a name="task-2---install-group-policy-tools-on-the-virtual-machine"></a><span data-ttu-id="1421e-127">工作 2 - 在虛擬機器上安裝群組原則工具</span><span class="sxs-lookup"><span data-stu-id="1421e-127">Task 2 - Install Group Policy tools on the virtual machine</span></span>
<span data-ttu-id="1421e-128">執行下列步驟，在已加入網域的虛擬機器上安裝群組原則管理工具。</span><span class="sxs-lookup"><span data-stu-id="1421e-128">Perform the following steps to install the Group Policy Administration tools on the domain joined virtual machine.</span></span>

1. <span data-ttu-id="1421e-129">在 Azure 傳統入口網站中瀏覽至 [虛擬機器]  節點。</span><span class="sxs-lookup"><span data-stu-id="1421e-129">Navigate to **Virtual Machines** node in the Azure classic portal.</span></span> <span data-ttu-id="1421e-130">選取您在工作 1 建立的虛擬機器，然後按一下視窗底部命令列上的 [連線]  。</span><span class="sxs-lookup"><span data-stu-id="1421e-130">Select the virtual machine you created in Task 1 and click **Connect** on the command bar at the bottom of the window.</span></span>

    ![連線至 Windows 虛擬機器](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. <span data-ttu-id="1421e-132">傳統入口網站會提示您開啟或儲存副檔名為 '.rdp' 的檔案，其可供用來連線到虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1421e-132">The classic portal prompts you to open or save a file with a '.rdp' extension, which is used to connect to the virtual machine.</span></span> <span data-ttu-id="1421e-133">在檔案下載完成時，按一下該檔案。</span><span class="sxs-lookup"><span data-stu-id="1421e-133">Click the file when it has finished downloading.</span></span>
3. <span data-ttu-id="1421e-134">在登入提示中，使用屬於「AAD DC 系統管理員」群組之使用者的認證。</span><span class="sxs-lookup"><span data-stu-id="1421e-134">At the login prompt, use the credentials of a user belonging to the 'AAD DC Administrators' group.</span></span> <span data-ttu-id="1421e-135">例如，使用 'bob@domainservicespreview.onmicrosoft.com' 在我們的案例。</span><span class="sxs-lookup"><span data-stu-id="1421e-135">For example, we use 'bob@domainservicespreview.onmicrosoft.com' in our case.</span></span>
4. <span data-ttu-id="1421e-136">在 [開始] 畫面中開啟 [伺服器管理員] 。</span><span class="sxs-lookup"><span data-stu-id="1421e-136">From the Start screen, open **Server Manager**.</span></span> <span data-ttu-id="1421e-137">按一下 [伺服器管理員] 視窗中央窗格內的 [新增角色及功能]  。</span><span class="sxs-lookup"><span data-stu-id="1421e-137">Click **Add Roles and Features** in the central pane of the Server Manager window.</span></span>

    ![啟動虛擬機器上的伺服器管理員](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager.png)
5. <span data-ttu-id="1421e-139">在 [新增角色及功能精靈] 的 [開始之前] 頁面上，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="1421e-139">On the **Before You Begin** page of the **Add Roles and Features Wizard**, click **Next**.</span></span>

    ![[開始之前] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-begin.png)
6. <span data-ttu-id="1421e-141">在 [安裝類型] 頁面上，保持勾選 [角色型或功能型安裝] 選項，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="1421e-141">On the **Installation Type** page, leave the **Role-based or feature-based installation** option checked and click **Next**.</span></span>

    ![[安裝類型] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-type.png)
7. <span data-ttu-id="1421e-143">在 [伺服器選擇] 頁面上，從伺服器集區中選取目前的虛擬機器，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="1421e-143">On the **Server Selection** page, select the current virtual machine from the server pool, and click **Next**.</span></span>

    ![[伺服器選擇] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-server.png)
8. <span data-ttu-id="1421e-145">在 [伺服器角色] 頁面上，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="1421e-145">On the **Server Roles** page, click **Next**.</span></span> <span data-ttu-id="1421e-146">我們會略過此頁面，因為我們沒有要在伺服器上安裝任何角色。</span><span class="sxs-lookup"><span data-stu-id="1421e-146">We skip this page since we are not installing any roles on the server.</span></span>
9. <span data-ttu-id="1421e-147">在 [功能] 頁面上，選取 [群組原則管理] 功能。</span><span class="sxs-lookup"><span data-stu-id="1421e-147">On the **Features** page, select the **Group Policy Management** feature.</span></span>

    ![[功能] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management.png)
10. <span data-ttu-id="1421e-149">在 [確認] 頁面上，按一下 [安裝] 在虛擬機器上安裝群組原則工具的功能。</span><span class="sxs-lookup"><span data-stu-id="1421e-149">On the **Confirmation** page, click **Install** to install the Group Policy Management feature on the virtual machine.</span></span> <span data-ttu-id="1421e-150">順利完成功能安裝時，按一下 [關閉] 以結束 [新增角色及功能] 精靈。</span><span class="sxs-lookup"><span data-stu-id="1421e-150">When feature installation completes successfully, click **Close** to exit the **Add Roles and Features** wizard.</span></span>

    ![確認電子郵件](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management-confirmation.png)

## <a name="task-3---launch-the-group-policy-management-console-to-administer-group-policy"></a><span data-ttu-id="1421e-152">工作 3 - 啟動群組原則管理主控台來管理群組原則</span><span class="sxs-lookup"><span data-stu-id="1421e-152">Task 3 - Launch the Group Policy management console to administer Group Policy</span></span>
<span data-ttu-id="1421e-153">您可以使用已加入網域的虛擬機器上的「群組原則」管理主控台來管理受管理網域上的群組原則。</span><span class="sxs-lookup"><span data-stu-id="1421e-153">You can use the Group Policy management console on the domain-joined virtual machine to administer Group Policy on the managed domain.</span></span>

> [!NOTE]
> <span data-ttu-id="1421e-154">您必須是「AAD DC 系統管理員」群組的成員，才能管理受管理網域的群組原則。</span><span class="sxs-lookup"><span data-stu-id="1421e-154">You need to be a member of the 'AAD DC Administrators' group, to administer Group Policy on the managed domain.</span></span>
>
>

1. <span data-ttu-id="1421e-155">從 [開始] 畫面中，按一下 [系統管理工具] 。</span><span class="sxs-lookup"><span data-stu-id="1421e-155">From the Start screen, click **Administrative Tools**.</span></span> <span data-ttu-id="1421e-156">您應該會看到安裝在虛擬機器上的 [群組原則管理] 主控台。</span><span class="sxs-lookup"><span data-stu-id="1421e-156">You should see the **Group Policy Management** console installed on the virtual machine.</span></span>

    ![啟動群組原則管理](./media/active-directory-domain-services-admin-guide/gp-management-installed.png)
2. <span data-ttu-id="1421e-158">按一下 [群組原則管理] 啟動群組原則管理主控台。</span><span class="sxs-lookup"><span data-stu-id="1421e-158">Click **Group Policy Management** to launch the Group Policy Management console.</span></span>

    ![群組原則主控台](./media/active-directory-domain-services-admin-guide/gp-management-console.png)

## <a name="task-4---customize-built-in-group-policy-objects"></a><span data-ttu-id="1421e-160">工作 4 - 自訂內建群組原則物件</span><span class="sxs-lookup"><span data-stu-id="1421e-160">Task 4 - Customize built-in Group Policy Objects</span></span>
<span data-ttu-id="1421e-161">有兩個內建群組原則物件 (GPO)，各自用於受管理網域中的「AADDC 電腦」和「AADDC 使用者」容器。</span><span class="sxs-lookup"><span data-stu-id="1421e-161">There are two built-in Group Policy Objects (GPOs) - one each for the 'AADDC Computers' and 'AADDC Users' containers in your managed domain.</span></span> <span data-ttu-id="1421e-162">您可以自訂這些 GPO，來設定受管理網域上的群組原則。</span><span class="sxs-lookup"><span data-stu-id="1421e-162">You can customize these GPOs to configure group policy on the managed domain.</span></span>

1. <span data-ttu-id="1421e-163">在 [群組原則管理] 主控台中，按一下 [Forest: contoso100.com] 和 [Domains] 節點加以展開，查看您的受管理網域的群組原則。</span><span class="sxs-lookup"><span data-stu-id="1421e-163">In the **Group Policy Management** console, click to expand the **Forest: contoso100.com** and **Domains** nodes to see the group policies for your managed domain.</span></span>

    ![內建 GPO](./media/active-directory-domain-services-admin-guide/builtin-gpos.png)
2. <span data-ttu-id="1421e-165">您可以自訂這些內建 GPO，來設定受管理網域上的群組原則。</span><span class="sxs-lookup"><span data-stu-id="1421e-165">You can customize these built-in GPOs to configure group policies on your managed domain.</span></span> <span data-ttu-id="1421e-166">以滑鼠右鍵按一下 GPO，然後按一下 [編輯...] 以自訂內建 GPO。</span><span class="sxs-lookup"><span data-stu-id="1421e-166">Right-click the GPO and click **Edit...** to customize the built-in GPO.</span></span> <span data-ttu-id="1421e-167">[群組原則設定編輯器] 工具可讓您自訂 GPO。</span><span class="sxs-lookup"><span data-stu-id="1421e-167">The Group Policy Configuration Editor tool enables you to customize the GPO.</span></span>

    ![編輯內建 GPO](./media/active-directory-domain-services-admin-guide/edit-builtin-gpo.png)
3. <span data-ttu-id="1421e-169">現在您可以使用 [群組原則管理編輯器] 主控台來編輯內建的 GPO。</span><span class="sxs-lookup"><span data-stu-id="1421e-169">You can now use the **Group Policy Management Editor** console to edit the built-in GPO.</span></span> <span data-ttu-id="1421e-170">例如，下列螢幕擷取畫面示範如何自訂內建「AADDC 電腦」的 GPO。</span><span class="sxs-lookup"><span data-stu-id="1421e-170">For instance, the following screenshot shows how to customize the built-in 'AADDC Computers' GPO.</span></span>

    ![自訂 GPO](./media/active-directory-domain-services-admin-guide/gp-editor.png)

## <a name="task-5---create-a-custom-group-policy-object-gpo"></a><span data-ttu-id="1421e-172">工作 5 - 建立自訂群組原則物件 (GPO)</span><span class="sxs-lookup"><span data-stu-id="1421e-172">Task 5 - Create a custom Group Policy Object (GPO)</span></span>
<span data-ttu-id="1421e-173">您可以建立或匯入自己的自訂群組原則物件。</span><span class="sxs-lookup"><span data-stu-id="1421e-173">You can create or import your own custom group policy objects.</span></span> <span data-ttu-id="1421e-174">您也可以將自訂 GPO 連結到您在受管理網域中建立的自訂 OU。</span><span class="sxs-lookup"><span data-stu-id="1421e-174">You can also link custom GPOs to a custom OU you have created in your managed domain.</span></span> <span data-ttu-id="1421e-175">如需建立自訂組織單位的詳細資訊，請參閱[在受管理網域上建立自訂 OU](active-directory-ds-admin-guide-create-ou.md)。</span><span class="sxs-lookup"><span data-stu-id="1421e-175">For more information on creating custom organizational units, see [create a custom OU on a managed domain](active-directory-ds-admin-guide-create-ou.md).</span></span>

> [!NOTE]
> <span data-ttu-id="1421e-176">您必須是「AAD DC 系統管理員」群組的成員，才能管理受管理網域的群組原則。</span><span class="sxs-lookup"><span data-stu-id="1421e-176">You need to be a member of the 'AAD DC Administrators' group, to administer Group Policy on the managed domain.</span></span>
>
>

1. <span data-ttu-id="1421e-177">在 [群組原則管理] 主控台中，按一下以選取您的自訂組織單位 (OU)。</span><span class="sxs-lookup"><span data-stu-id="1421e-177">In the **Group Policy Management** console, click to select your custom organizational unit (OU).</span></span> <span data-ttu-id="1421e-178">以滑鼠右鍵按一下 OU，然後按一下 [在這個網域中建立 GPO 並連結到...]。</span><span class="sxs-lookup"><span data-stu-id="1421e-178">Right-click the OU and click **Create a GPO in this domain, and Link it here...**.</span></span>

    ![建立自訂 GPO](./media/active-directory-domain-services-admin-guide/gp-create-gpo.png)
2. <span data-ttu-id="1421e-180">指定新 GPO 的名稱，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="1421e-180">Specify a name for the new GPO and click **OK**.</span></span>

    ![指定 GPO 的名稱](./media/active-directory-domain-services-admin-guide/gp-specify-gpo-name.png)
3. <span data-ttu-id="1421e-182">系統將會建立新的 GPO 並連結至您的自訂 OU。</span><span class="sxs-lookup"><span data-stu-id="1421e-182">A new GPO is created and linked to your custom OU.</span></span> <span data-ttu-id="1421e-183">以滑鼠右鍵按一下 GPO，然後按一下功能表上的 [編輯...]。</span><span class="sxs-lookup"><span data-stu-id="1421e-183">Right-click the GPO and click **Edit...** from the menu.</span></span>

    ![新建立的 GPO](./media/active-directory-domain-services-admin-guide/gp-gpo-created.png)
4. <span data-ttu-id="1421e-185">您可以使用 [群組原則管理編輯器] 自訂新建立的 GPO。</span><span class="sxs-lookup"><span data-stu-id="1421e-185">You can customize the newly created GPO using the **Group Policy Management Editor**.</span></span>

    ![自訂新 GPO](./media/active-directory-domain-services-admin-guide/gp-customize-gpo.png)


<span data-ttu-id="1421e-187">可在 Technet 上取得有關使用[群組原則管理主控台](https://technet.microsoft.com/library/cc753298.aspx)的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="1421e-187">More information about using [Group Policy Management Console](https://technet.microsoft.com/library/cc753298.aspx) is available on Technet.</span></span>

## <a name="related-content"></a><span data-ttu-id="1421e-188">相關內容</span><span class="sxs-lookup"><span data-stu-id="1421e-188">Related Content</span></span>
* [<span data-ttu-id="1421e-189">Azure AD Domain Services - 入門指南</span><span class="sxs-lookup"><span data-stu-id="1421e-189">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="1421e-190">將 Windows Server 虛擬機器加入 Azure AD 網域服務受管理的網域</span><span class="sxs-lookup"><span data-stu-id="1421e-190">Join a Windows Server virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="1421e-191">Administer an Azure AD Domain Services managed domain (管理 Azure AD 網域服務受管理的網域)</span><span class="sxs-lookup"><span data-stu-id="1421e-191">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="1421e-192">群組原則管理主控台</span><span class="sxs-lookup"><span data-stu-id="1421e-192">Group Policy Management Console</span></span>](https://technet.microsoft.com/library/cc753298.aspx)
