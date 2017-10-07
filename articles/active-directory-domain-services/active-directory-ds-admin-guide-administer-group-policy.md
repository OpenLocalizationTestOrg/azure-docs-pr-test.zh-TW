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
ms.openlocfilehash: d56ebf27e3015a7f3385ac5a4ddd77ea2c88387f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="administer-group-policy-on-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="092ea-103">管理 Azure AD Domain Services 受管理網域上的群組原則</span><span class="sxs-lookup"><span data-stu-id="092ea-103">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="092ea-104">Azure Active Directory 網域服務的 hello ' AADDC 使用者 」 和 「 AADDC 電腦 」 容器包含內建群組原則物件 (Gpo)。</span><span class="sxs-lookup"><span data-stu-id="092ea-104">Azure Active Directory Domain Services includes built-in Group Policy Objects (GPOs) for hello 'AADDC Users' and 'AADDC Computers' containers.</span></span> <span data-ttu-id="092ea-105">您可以自訂這些內建的 Gpo tooconfigure hello 受管理的網域上的群組原則。</span><span class="sxs-lookup"><span data-stu-id="092ea-105">You can customize these built-in GPOs tooconfigure Group Policy on hello managed domain.</span></span> <span data-ttu-id="092ea-106">此外，hello ' AAD DC Administrators' 群組的成員可以建立自己的自訂 Ou hello 受管理的網域中。</span><span class="sxs-lookup"><span data-stu-id="092ea-106">Additionally, members of hello 'AAD DC Administrators' group can create their own custom OUs in hello managed domain.</span></span> <span data-ttu-id="092ea-107">它們也可以建立自訂的 Gpo，並將其連結 toothese 自訂 Ou。</span><span class="sxs-lookup"><span data-stu-id="092ea-107">They can also create custom GPOs and link them toothese custom OUs.</span></span> <span data-ttu-id="092ea-108">Hello 受管理的網域上的群組原則系統管理特殊權限會授與使用者隸屬 toohello ' AAD DC Administrators' 群組。</span><span class="sxs-lookup"><span data-stu-id="092ea-108">Users who belong toohello 'AAD DC Administrators' group are granted Group Policy administration privileges on hello managed domain.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="092ea-109">開始之前</span><span class="sxs-lookup"><span data-stu-id="092ea-109">Before you begin</span></span>
<span data-ttu-id="092ea-110">本文所列 tooperform hello 工作，您必須：</span><span class="sxs-lookup"><span data-stu-id="092ea-110">tooperform hello tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="092ea-111">有效的 **Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="092ea-111">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="092ea-112">**Azure AD 目錄** - 與內部部署目錄或僅限雲端的目錄同步處理。</span><span class="sxs-lookup"><span data-stu-id="092ea-112">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="092ea-113">**Azure AD 網域服務**必須啟用 hello Azure AD 目錄。</span><span class="sxs-lookup"><span data-stu-id="092ea-113">**Azure AD Domain Services** must be enabled for hello Azure AD directory.</span></span> <span data-ttu-id="092ea-114">如果您尚未這樣做，請遵循 hello 中所述的所有 hello 工作[入門指南](active-directory-ds-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="092ea-114">If you haven't done so, follow all hello tasks outlined in hello [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="092ea-115">A**已加入網域的虛擬機器**從您管理的 hello Azure AD 網域服務受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="092ea-115">A **domain-joined virtual machine** from which you administer hello Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="092ea-116">如果您沒有這類虛擬機器，請遵循所有 hello 文章的標題中的 hello 工作[加入 Windows 虛擬機器 tooa 受管理的網域](active-directory-ds-admin-guide-join-windows-vm.md)。</span><span class="sxs-lookup"><span data-stu-id="092ea-116">If you don't have such a virtual machine, follow all hello tasks outlined in hello article titled [Join a Windows virtual machine tooa managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>
5. <span data-ttu-id="092ea-117">您需要 hello 認證**使用者帳戶隸屬 toohello ' AAD DC Administrators' 群組**目錄，tooadminister 群組原則的受管理的網域中。</span><span class="sxs-lookup"><span data-stu-id="092ea-117">You need hello credentials of a **user account belonging toohello 'AAD DC Administrators' group** in your directory, tooadminister Group Policy for your managed domain.</span></span>

<br>

## <a name="task-1---provision-a-domain-joined-virtual-machine-tooremotely-administer-group-policy-for-hello-managed-domain"></a><span data-ttu-id="092ea-118">工作 1-佈建已加入網域的虛擬機器 tooremotely hello 受管理的網域的管理群組原則</span><span class="sxs-lookup"><span data-stu-id="092ea-118">Task 1 - Provision a domain-joined virtual machine tooremotely administer Group Policy for hello managed domain</span></span>
<span data-ttu-id="092ea-119">可以從遠端使用熟悉的 Active Directory 系統管理工具例如 hello Active Directory 管理中心 (ADAC) 或 AD PowerShell 管理 azure AD 網域服務受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="092ea-119">Azure AD Domain Services managed domains can be managed remotely using familiar Active Directory administrative tools such as hello Active Directory Administrative Center (ADAC) or AD PowerShell.</span></span> <span data-ttu-id="092ea-120">同樣地，可以使用 hello 群組原則系統管理工具，從遠端管理的 hello 受管理的網域群組原則。</span><span class="sxs-lookup"><span data-stu-id="092ea-120">Similarly, Group Policy for hello managed domain can be administered remotely using hello Group Policy administration tools.</span></span>

<span data-ttu-id="092ea-121">Azure AD 目錄中的系統管理員沒有 hello 透過遠端桌面的受管理網域的權限 tooconnect toodomain 控制站。</span><span class="sxs-lookup"><span data-stu-id="092ea-121">Administrators in your Azure AD directory do not have privileges tooconnect toodomain controllers on hello managed domain via Remote Desktop.</span></span> <span data-ttu-id="092ea-122">Hello ' AAD DC Administrators' 群組的成員可以管理群組原則的受管理的網域從遠端。</span><span class="sxs-lookup"><span data-stu-id="092ea-122">Members of hello 'AAD DC Administrators' group can administer Group Policy for managed domains remotely.</span></span> <span data-ttu-id="092ea-123">他們可以在 Windows 伺服器/用戶端電腦已加入的 toohello 受管理的網域上使用群組原則工具。</span><span class="sxs-lookup"><span data-stu-id="092ea-123">They can use Group Policy tools on a Windows Server/client computer joined toohello managed domain.</span></span> <span data-ttu-id="092ea-124">可以安裝 Windows Server 和用戶端電腦上 hello 群組原則管理選擇性功能的一部分加入 toohello 受管理的網域群組原則工具。</span><span class="sxs-lookup"><span data-stu-id="092ea-124">Group Policy tools can be installed as part of hello Group Policy Management optional feature on Windows Server and client machines joined toohello managed domain.</span></span>

<span data-ttu-id="092ea-125">hello 第一項工作是 tooprovision 是聯結的 toohello 受管理的網域 Windows Server 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="092ea-125">hello first task is tooprovision a Windows Server virtual machine that is joined toohello managed domain.</span></span> <span data-ttu-id="092ea-126">如需指示，請參閱 toohello 文章 <<c0> [ 加入 Windows Server 虛擬機器 tooan Azure AD 網域服務受管理的網域](active-directory-ds-admin-guide-join-windows-vm.md)。</span><span class="sxs-lookup"><span data-stu-id="092ea-126">For instructions, refer toohello article titled [join a Windows Server virtual machine tooan Azure AD Domain Services managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>

## <a name="task-2---install-group-policy-tools-on-hello-virtual-machine"></a><span data-ttu-id="092ea-127">工作 2-hello 虛擬機器上安裝群組原則工具</span><span class="sxs-lookup"><span data-stu-id="092ea-127">Task 2 - Install Group Policy tools on hello virtual machine</span></span>
<span data-ttu-id="092ea-128">執行下列步驟 tooinstall hello 群組原則系統管理工具 hello 已加入網域的虛擬機器上的 hello。</span><span class="sxs-lookup"><span data-stu-id="092ea-128">Perform hello following steps tooinstall hello Group Policy Administration tools on hello domain joined virtual machine.</span></span>

1. <span data-ttu-id="092ea-129">瀏覽過**虛擬機器**hello Azure 傳統入口網站中的節點。</span><span class="sxs-lookup"><span data-stu-id="092ea-129">Navigate too**Virtual Machines** node in hello Azure classic portal.</span></span> <span data-ttu-id="092ea-130">選取您在工作 1 中建立的 hello 虛擬機器，然後按一下**連接**hello 在 hello hello 視窗底部的命令列上。</span><span class="sxs-lookup"><span data-stu-id="092ea-130">Select hello virtual machine you created in Task 1 and click **Connect** on hello command bar at hello bottom of hello window.</span></span>

    ![TooWindows 虛擬機器連線](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. <span data-ttu-id="092ea-132">hello 傳統入口網站會提示您 tooopen 或儲存 '.rdp' 副檔名的檔案，這是使用的 tooconnect toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="092ea-132">hello classic portal prompts you tooopen or save a file with a '.rdp' extension, which is used tooconnect toohello virtual machine.</span></span> <span data-ttu-id="092ea-133">下載完成時，請按一下 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="092ea-133">Click hello file when it has finished downloading.</span></span>
3. <span data-ttu-id="092ea-134">在 hello 登入提示字元中使用 hello 屬於 toohello ' AAD DC Administrators' 群組的使用者認證。</span><span class="sxs-lookup"><span data-stu-id="092ea-134">At hello login prompt, use hello credentials of a user belonging toohello 'AAD DC Administrators' group.</span></span> <span data-ttu-id="092ea-135">例如，使用 'bob@domainservicespreview.onmicrosoft.com' 在我們的案例。</span><span class="sxs-lookup"><span data-stu-id="092ea-135">For example, we use 'bob@domainservicespreview.onmicrosoft.com' in our case.</span></span>
4. <span data-ttu-id="092ea-136">從 hello 開始 畫面開啟**伺服器管理員**。</span><span class="sxs-lookup"><span data-stu-id="092ea-136">From hello Start screen, open **Server Manager**.</span></span> <span data-ttu-id="092ea-137">按一下**新增角色及功能**hello hello 伺服器管理員 視窗的中央窗格中。</span><span class="sxs-lookup"><span data-stu-id="092ea-137">Click **Add Roles and Features** in hello central pane of hello Server Manager window.</span></span>

    ![啟動虛擬機器上的伺服器管理員](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager.png)
5. <span data-ttu-id="092ea-139">在 hello**在您開始前**hello 頁面**新增角色及功能精靈**，按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="092ea-139">On hello **Before You Begin** page of hello **Add Roles and Features Wizard**, click **Next**.</span></span>

    ![[開始之前] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-begin.png)
6. <span data-ttu-id="092ea-141">在 hello**安裝類型**頁面上，保留 hello**角色型或功能型安裝**檢查的選項，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="092ea-141">On hello **Installation Type** page, leave hello **Role-based or feature-based installation** option checked and click **Next**.</span></span>

    ![[安裝類型] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-type.png)
7. <span data-ttu-id="092ea-143">在 hello**伺服器選取項目**頁面上，選取 hello 目前虛擬機器從 hello 伺服器集區，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="092ea-143">On hello **Server Selection** page, select hello current virtual machine from hello server pool, and click **Next**.</span></span>

    ![[伺服器選擇] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-server.png)
8. <span data-ttu-id="092ea-145">在 hello**伺服器角色**頁面上，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="092ea-145">On hello **Server Roles** page, click **Next**.</span></span> <span data-ttu-id="092ea-146">我們請略過此頁面，因為我們 hello 伺服器上未安裝任何角色。</span><span class="sxs-lookup"><span data-stu-id="092ea-146">We skip this page since we are not installing any roles on hello server.</span></span>
9. <span data-ttu-id="092ea-147">在 hello**功能**頁面上，選取 hello**群組原則管理**功能。</span><span class="sxs-lookup"><span data-stu-id="092ea-147">On hello **Features** page, select hello **Group Policy Management** feature.</span></span>

    ![[功能] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management.png)
10. <span data-ttu-id="092ea-149">在 hello**確認**頁面上，按一下**安裝**hello 虛擬機器上的 tooinstall hello 群組原則管理功能。</span><span class="sxs-lookup"><span data-stu-id="092ea-149">On hello **Confirmation** page, click **Install** tooinstall hello Group Policy Management feature on hello virtual machine.</span></span> <span data-ttu-id="092ea-150">功能安裝成功完成時，按一下**關閉**tooexit hello**新增角色及功能**精靈。</span><span class="sxs-lookup"><span data-stu-id="092ea-150">When feature installation completes successfully, click **Close** tooexit hello **Add Roles and Features** wizard.</span></span>

    ![確認電子郵件](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management-confirmation.png)

## <a name="task-3---launch-hello-group-policy-management-console-tooadminister-group-policy"></a><span data-ttu-id="092ea-152">工作 3-啟動 hello 群組原則管理主控台 tooadminister 群組原則</span><span class="sxs-lookup"><span data-stu-id="092ea-152">Task 3 - Launch hello Group Policy management console tooadminister Group Policy</span></span>
<span data-ttu-id="092ea-153">您可以使用 hello 群組原則管理主控台上 hello 已加入網域的虛擬機器 tooadminister hello 受管理的網域上的群組原則。</span><span class="sxs-lookup"><span data-stu-id="092ea-153">You can use hello Group Policy management console on hello domain-joined virtual machine tooadminister Group Policy on hello managed domain.</span></span>

> [!NOTE]
> <span data-ttu-id="092ea-154">您需要 toobe tooadminister hello 受管理的網域上的群組原則 hello ' AAD DC Administrators' 群組的成員。</span><span class="sxs-lookup"><span data-stu-id="092ea-154">You need toobe a member of hello 'AAD DC Administrators' group, tooadminister Group Policy on hello managed domain.</span></span>
>
>

1. <span data-ttu-id="092ea-155">從 hello 開始畫面上，按一下 **系統管理工具**。</span><span class="sxs-lookup"><span data-stu-id="092ea-155">From hello Start screen, click **Administrative Tools**.</span></span> <span data-ttu-id="092ea-156">您應該會看見 hello**群組原則管理**hello 虛擬機器上安裝主控台。</span><span class="sxs-lookup"><span data-stu-id="092ea-156">You should see hello **Group Policy Management** console installed on hello virtual machine.</span></span>

    ![啟動群組原則管理](./media/active-directory-domain-services-admin-guide/gp-management-installed.png)
2. <span data-ttu-id="092ea-158">按一下**群組原則管理**toolaunch hello 群組原則管理主控台。</span><span class="sxs-lookup"><span data-stu-id="092ea-158">Click **Group Policy Management** toolaunch hello Group Policy Management console.</span></span>

    ![群組原則主控台](./media/active-directory-domain-services-admin-guide/gp-management-console.png)

## <a name="task-4---customize-built-in-group-policy-objects"></a><span data-ttu-id="092ea-160">工作 4 - 自訂內建群組原則物件</span><span class="sxs-lookup"><span data-stu-id="092ea-160">Task 4 - Customize built-in Group Policy Objects</span></span>
<span data-ttu-id="092ea-161">有兩個內建群組原則物件 (Gpo) 的每個受管理的網域中的 hello 'AADDC 電腦' 和 ' AADDC 使用者 容器。</span><span class="sxs-lookup"><span data-stu-id="092ea-161">There are two built-in Group Policy Objects (GPOs) - one each for hello 'AADDC Computers' and 'AADDC Users' containers in your managed domain.</span></span> <span data-ttu-id="092ea-162">您可以自訂這些 Gpo tooconfigure 上的群組原則 hello 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="092ea-162">You can customize these GPOs tooconfigure group policy on hello managed domain.</span></span>

1. <span data-ttu-id="092ea-163">在 hello**群組原則管理**主控台中，按一下 tooexpand hello**樹系： contoso100.com**和**網域**節點 toosee hello 群組原則的受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="092ea-163">In hello **Group Policy Management** console, click tooexpand hello **Forest: contoso100.com** and **Domains** nodes toosee hello group policies for your managed domain.</span></span>

    ![內建 GPO](./media/active-directory-domain-services-admin-guide/builtin-gpos.png)
2. <span data-ttu-id="092ea-165">您可以自訂這些內建的 Gpo tooconfigure 群組原則在受管理的網域上。</span><span class="sxs-lookup"><span data-stu-id="092ea-165">You can customize these built-in GPOs tooconfigure group policies on your managed domain.</span></span> <span data-ttu-id="092ea-166">Hello GPO 上按一下滑鼠右鍵，然後按一下**編輯...** toocustomize hello 內建 GPO。</span><span class="sxs-lookup"><span data-stu-id="092ea-166">Right-click hello GPO and click **Edit...** toocustomize hello built-in GPO.</span></span> <span data-ttu-id="092ea-167">hello 群組原則組態編輯器工具可讓您 toocustomize hello GPO。</span><span class="sxs-lookup"><span data-stu-id="092ea-167">hello Group Policy Configuration Editor tool enables you toocustomize hello GPO.</span></span>

    ![編輯內建 GPO](./media/active-directory-domain-services-admin-guide/edit-builtin-gpo.png)
3. <span data-ttu-id="092ea-169">您現在可以使用 hello**群組原則管理編輯器**主控台 tooedit hello 內建 GPO。</span><span class="sxs-lookup"><span data-stu-id="092ea-169">You can now use hello **Group Policy Management Editor** console tooedit hello built-in GPO.</span></span> <span data-ttu-id="092ea-170">比方說，下列螢幕擷取畫面的 hello 顯示 toocustomize hello 內建的 「 AADDC 電腦 」 GPO 的方式。</span><span class="sxs-lookup"><span data-stu-id="092ea-170">For instance, hello following screenshot shows how toocustomize hello built-in 'AADDC Computers' GPO.</span></span>

    ![自訂 GPO](./media/active-directory-domain-services-admin-guide/gp-editor.png)

## <a name="task-5---create-a-custom-group-policy-object-gpo"></a><span data-ttu-id="092ea-172">工作 5 - 建立自訂群組原則物件 (GPO)</span><span class="sxs-lookup"><span data-stu-id="092ea-172">Task 5 - Create a custom Group Policy Object (GPO)</span></span>
<span data-ttu-id="092ea-173">您可以建立或匯入自己的自訂群組原則物件。</span><span class="sxs-lookup"><span data-stu-id="092ea-173">You can create or import your own custom group policy objects.</span></span> <span data-ttu-id="092ea-174">您也可以將連結自訂 Gpo tooa 自訂您受管理的網域中建立的 OU。</span><span class="sxs-lookup"><span data-stu-id="092ea-174">You can also link custom GPOs tooa custom OU you have created in your managed domain.</span></span> <span data-ttu-id="092ea-175">如需建立自訂組織單位的詳細資訊，請參閱[在受管理網域上建立自訂 OU](active-directory-ds-admin-guide-create-ou.md)。</span><span class="sxs-lookup"><span data-stu-id="092ea-175">For more information on creating custom organizational units, see [create a custom OU on a managed domain](active-directory-ds-admin-guide-create-ou.md).</span></span>

> [!NOTE]
> <span data-ttu-id="092ea-176">您需要 toobe tooadminister hello 受管理的網域上的群組原則 hello ' AAD DC Administrators' 群組的成員。</span><span class="sxs-lookup"><span data-stu-id="092ea-176">You need toobe a member of hello 'AAD DC Administrators' group, tooadminister Group Policy on hello managed domain.</span></span>
>
>

1. <span data-ttu-id="092ea-177">在 hello**群組原則管理**主控台中，按一下 tooselect 自訂組織單位 (OU)。</span><span class="sxs-lookup"><span data-stu-id="092ea-177">In hello **Group Policy Management** console, click tooselect your custom organizational unit (OU).</span></span> <span data-ttu-id="092ea-178">Hello OU 上按一下滑鼠右鍵，然後按一下**在這個網域中建立 GPO 並連結到...**.</span><span class="sxs-lookup"><span data-stu-id="092ea-178">Right-click hello OU and click **Create a GPO in this domain, and Link it here...**.</span></span>

    ![建立自訂 GPO](./media/active-directory-domain-services-admin-guide/gp-create-gpo.png)
2. <span data-ttu-id="092ea-180">指定 hello 新 GPO 的名稱，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="092ea-180">Specify a name for hello new GPO and click **OK**.</span></span>

    ![指定 GPO 的名稱](./media/active-directory-domain-services-admin-guide/gp-specify-gpo-name.png)
3. <span data-ttu-id="092ea-182">建立新的 GPO，並連結 tooyour 自訂 OU。</span><span class="sxs-lookup"><span data-stu-id="092ea-182">A new GPO is created and linked tooyour custom OU.</span></span> <span data-ttu-id="092ea-183">Hello GPO 上按一下滑鼠右鍵，然後按一下**編輯...** hello 功能表。</span><span class="sxs-lookup"><span data-stu-id="092ea-183">Right-click hello GPO and click **Edit...** from hello menu.</span></span>

    ![新建立的 GPO](./media/active-directory-domain-services-admin-guide/gp-gpo-created.png)
4. <span data-ttu-id="092ea-185">您可以自訂 hello 新建立的 GPO，使用 hello**群組原則管理編輯器**。</span><span class="sxs-lookup"><span data-stu-id="092ea-185">You can customize hello newly created GPO using hello **Group Policy Management Editor**.</span></span>

    ![自訂新 GPO](./media/active-directory-domain-services-admin-guide/gp-customize-gpo.png)


<span data-ttu-id="092ea-187">可在 Technet 上取得有關使用[群組原則管理主控台](https://technet.microsoft.com/library/cc753298.aspx)的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="092ea-187">More information about using [Group Policy Management Console](https://technet.microsoft.com/library/cc753298.aspx) is available on Technet.</span></span>

## <a name="related-content"></a><span data-ttu-id="092ea-188">相關內容</span><span class="sxs-lookup"><span data-stu-id="092ea-188">Related Content</span></span>
* [<span data-ttu-id="092ea-189">Azure AD Domain Services - 入門指南</span><span class="sxs-lookup"><span data-stu-id="092ea-189">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="092ea-190">加入 Windows Server 虛擬機器 tooan Azure AD 網域服務受管理的網域</span><span class="sxs-lookup"><span data-stu-id="092ea-190">Join a Windows Server virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="092ea-191">Administer an Azure AD Domain Services managed domain (管理 Azure AD 網域服務受管理的網域)</span><span class="sxs-lookup"><span data-stu-id="092ea-191">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="092ea-192">群組原則管理主控台</span><span class="sxs-lookup"><span data-stu-id="092ea-192">Group Policy Management Console</span></span>](https://technet.microsoft.com/library/cc753298.aspx)
