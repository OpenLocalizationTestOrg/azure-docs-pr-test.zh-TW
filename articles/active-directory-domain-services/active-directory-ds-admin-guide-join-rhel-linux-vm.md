---
title: "Azure Active Directory 網域服務： 加入 RHEL VM tooa 受管理的網域 |Microsoft 文件"
description: "將 Red Hat Enterprise Linux 虛擬機器加入 tooAzure AD 網域服務"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 87291c47-1280-43f8-8fb2-da1bd61a4942
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 41ca2aaf2eefbf9c403d2b834d61a1aa0943d950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-red-hat-enterprise-linux-7-virtual-machine-tooa-managed-domain"></a><span data-ttu-id="2068c-103">加入 Red Hat Enterprise Linux 7 虛擬機器 tooa 受管理的網域</span><span class="sxs-lookup"><span data-stu-id="2068c-103">Join a Red Hat Enterprise Linux 7 virtual machine tooa managed domain</span></span>
<span data-ttu-id="2068c-104">本文示範 toojoin Red Hat Enterprise Linux (RHEL) 7 虛擬機器 tooan Azure AD 網域服務網域的管理方式。</span><span class="sxs-lookup"><span data-stu-id="2068c-104">This article shows you how toojoin a Red Hat Enterprise Linux (RHEL) 7 virtual machine tooan Azure AD Domain Services managed domain.</span></span>

## <a name="provision-a-red-hat-enterprise-linux-virtual-machine"></a><span data-ttu-id="2068c-105">佈建 Red Hat Enterprise Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="2068c-105">Provision a Red Hat Enterprise Linux virtual machine</span></span>
<span data-ttu-id="2068c-106">執行下列步驟使用 hello Azure 入口網站的 tooprovision RHEL 7 虛擬機器的 hello。</span><span class="sxs-lookup"><span data-stu-id="2068c-106">Perform hello following steps tooprovision a RHEL 7 virtual machine using hello Azure portal.</span></span>

1. <span data-ttu-id="2068c-107">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="2068c-107">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

    ![Azure 入口網站儀表板](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-dashboard.png)
2. <span data-ttu-id="2068c-109">按一下**新增**在左窗格中，然後輸入 hello **Red Hat** hello 搜尋列中 hello 下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="2068c-109">Click **New** on hello left pane and type **Red Hat** into hello search bar as shown in hello following screenshot.</span></span> <span data-ttu-id="2068c-110">Red Hat Enterprise Linux 的項目會出現在 hello 搜尋結果。</span><span class="sxs-lookup"><span data-stu-id="2068c-110">Entries for Red Hat Enterprise Linux appear in hello search results.</span></span> <span data-ttu-id="2068c-111">按一下 [Red Hat Enterprise Linux 7.2]。</span><span class="sxs-lookup"><span data-stu-id="2068c-111">Click **Red Hat Enterprise Linux 7.2**.</span></span>

    ![在結果中選取 RHEL](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-find-rhel-image.png)
3. <span data-ttu-id="2068c-113">hello 搜尋結果中 hello**一切**窗格應該會列出 hello Red Hat Enterprise Linux 7.2 映像。</span><span class="sxs-lookup"><span data-stu-id="2068c-113">hello search results in hello **Everything** pane should list hello Red Hat Enterprise Linux 7.2 image.</span></span> <span data-ttu-id="2068c-114">按一下**Red Hat Enterprise Linux 7.2** tooview hello 虛擬機器映像的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="2068c-114">Click **Red Hat Enterprise Linux 7.2** tooview more information about hello virtual machine image.</span></span>

    ![在結果中選取 RHEL](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-rhel-image.png)
4. <span data-ttu-id="2068c-116">在 [hello **Red Hat Enterprise Linux 7.2** ] 窗格中，您應該會看到 hello 虛擬機器映像的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="2068c-116">In hello **Red Hat Enterprise Linux 7.2** pane, you should see more information about hello virtual machine image.</span></span> <span data-ttu-id="2068c-117">在 [hello**選取部署模型**下拉式清單中，選取**傳統**。</span><span class="sxs-lookup"><span data-stu-id="2068c-117">In hello **Select a deployment model** dropdown, select **Classic**.</span></span> <span data-ttu-id="2068c-118">然後按一下 [hello**建立**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2068c-118">Then click hello **Create** button.</span></span>

    ![檢視映像的詳細資料](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-clicked.png)
5. <span data-ttu-id="2068c-120">在 [hello**基本概念**hello 頁面**建立虛擬機器**精靈] 中，輸入 hello**主機名稱**hello 新虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2068c-120">In hello **Basics** page of hello **Create virtual machine** wizard, enter hello **Host Name** for hello new virtual machine.</span></span> <span data-ttu-id="2068c-121">也指定本機系統管理員使用者名稱中 hello**使用者名**欄位和**密碼**。</span><span class="sxs-lookup"><span data-stu-id="2068c-121">Also specify a local administrator user name in hello **User name** field and a **Password**.</span></span> <span data-ttu-id="2068c-122">您也可以選擇 toouse SSH 金鑰 tooauthenticate hello 本機系統管理員使用者。</span><span class="sxs-lookup"><span data-stu-id="2068c-122">You may also choose toouse an SSH key tooauthenticate hello local administrator user.</span></span> <span data-ttu-id="2068c-123">也選取**定價層**hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2068c-123">Also select a **Pricing Tier** for hello virtual machine.</span></span>

    ![建立 VM - 基本頁面](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-basic-details.png)
6. <span data-ttu-id="2068c-125">在 [hello**大小**頁面 hello**建立虛擬機器**hello 虛擬機器精靈、 選取 hello 大小。</span><span class="sxs-lookup"><span data-stu-id="2068c-125">In hello **Size** page of hello **Create virtual machine** wizard, select hello size for hello virtual machine.</span></span>

    ![建立 VM - 選取大小](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-vm-size.png)

7. <span data-ttu-id="2068c-127">在 [hello**設定**頁面 hello**建立虛擬機器**精靈、 選取 hello hello 虛擬機器的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="2068c-127">In hello **Settings** page of hello **Create virtual machine** wizard, select hello storage account for hello virtual machine.</span></span> <span data-ttu-id="2068c-128">按一下**虛擬網路**tooselect hello 虛擬網路 toowhich hello Linux VM，必須先部署。</span><span class="sxs-lookup"><span data-stu-id="2068c-128">Click **Virtual Network** tooselect hello virtual network toowhich hello Linux VM should be deployed.</span></span> <span data-ttu-id="2068c-129">在 [hello**虛擬網路**刀鋒視窗中，選取 hello Azure AD 網域服務可用的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="2068c-129">In hello **Virtual Network** blade, select hello virtual network in which Azure AD Domain Services is available.</span></span> <span data-ttu-id="2068c-130">在此範例中，我們挑選 hello 'MyPreviewVNet' 的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="2068c-130">In this example, we pick hello 'MyPreviewVNet' virtual network.</span></span>

    ![建立 VM - 選取虛擬網路](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-select-vnet.png)
8. <span data-ttu-id="2068c-132">Hello 上**摘要**hello 頁面**建立虛擬機器**精靈、 檢閱，並按一下 hello**確定**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2068c-132">On hello **Summary** page of hello **Create virtual machine** wizard, review and click hello **OK** button.</span></span>

    ![建立 VM - 選取的虛擬網路](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-vnet-selected.png)
9. <span data-ttu-id="2068c-134">部署的 hello 新的虛擬機器根據 hello RHEL 7.2 映像應該會開始。</span><span class="sxs-lookup"><span data-stu-id="2068c-134">Deployment of hello new virtual machine based on hello RHEL 7.2 image should start.</span></span>

    ![建立 VM - 部署開始](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployment-started.png)
10. <span data-ttu-id="2068c-136">請稍候幾分鐘 hello 虛擬機器必須部署成功且可供使用。</span><span class="sxs-lookup"><span data-stu-id="2068c-136">After a few minutes, hello virtual machine should be deployed successfully and ready for use.</span></span>

    ![建立 VM - 已部署](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployed.png)

## <a name="connect-remotely-toohello-newly-provisioned-linux-virtual-machine"></a><span data-ttu-id="2068c-138">從遠端連線 toohello 新提供的 Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="2068c-138">Connect remotely toohello newly provisioned Linux virtual machine</span></span>
<span data-ttu-id="2068c-139">hello RHEL 7.2 虛擬機器已在 Azure 中佈建。</span><span class="sxs-lookup"><span data-stu-id="2068c-139">hello RHEL 7.2 virtual machine has been provisioned in Azure.</span></span> <span data-ttu-id="2068c-140">hello 下一個工作是 tooconnect 遠端 toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2068c-140">hello next task is tooconnect remotely toohello virtual machine.</span></span>

<span data-ttu-id="2068c-141">**Toohello RHEL 7.2 虛擬機器連線**遵循 hello 文章中的 hello 指示[如何 tooa 執行 Linux 的虛擬機器上的 toolog](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="2068c-141">**Connect toohello RHEL 7.2 virtual machine** Follow hello instructions in hello article [How toolog on tooa virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="2068c-142">hello 其餘 hello 步驟假設您使用 hello PuTTY SSH 用戶端 tooconnect toohello RHEL 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2068c-142">hello rest of hello steps assume you use hello PuTTY SSH client tooconnect toohello RHEL virtual machine.</span></span> <span data-ttu-id="2068c-143">如需詳細資訊，請參閱 hello [PuTTY 下載頁面](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)。</span><span class="sxs-lookup"><span data-stu-id="2068c-143">For more information, see hello [PuTTY Download page](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

1. <span data-ttu-id="2068c-144">開啟 hello PuTTY 程式。</span><span class="sxs-lookup"><span data-stu-id="2068c-144">Open hello PuTTY program.</span></span>
2. <span data-ttu-id="2068c-145">輸入 hello**主機名稱**hello 新建 RHEL 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2068c-145">Enter hello **Host Name** for hello newly created RHEL virtual machine.</span></span> <span data-ttu-id="2068c-146">在此範例中，我們的虛擬機器會具有 hello 主機名稱 'contoso rhel.cloudapp.net'。</span><span class="sxs-lookup"><span data-stu-id="2068c-146">In this example, our virtual machine has hello host name 'contoso-rhel.cloudapp.net'.</span></span> <span data-ttu-id="2068c-147">如果您不確定您的 VM hello 主機名稱，請參閱 toohello hello Azure 入口網站上的 VM 儀表板。</span><span class="sxs-lookup"><span data-stu-id="2068c-147">If you are not sure of hello host name of your VM, refer toohello VM dashboard on hello Azure portal.</span></span>

    ![PuTTY 連線](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-connect.png)
3. <span data-ttu-id="2068c-149">登入 toohello 使用 hello hello 虛擬機器建立時，您所指定的本機系統管理員認證的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2068c-149">Log on toohello virtual machine using hello local administrator credentials you specified when hello virtual machine was created.</span></span> <span data-ttu-id="2068c-150">在此範例中，我們會使用 hello 本機系統管理員帳戶 」 mahesh"。</span><span class="sxs-lookup"><span data-stu-id="2068c-150">In this example, we used hello local administrator account "mahesh".</span></span>

    ![PuTTY 登入](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-login.png)

## <a name="install-required-packages-on-hello-linux-virtual-machine"></a><span data-ttu-id="2068c-152">Hello Linux 虛擬機器上安裝必要的封裝</span><span class="sxs-lookup"><span data-stu-id="2068c-152">Install required packages on hello Linux virtual machine</span></span>
<span data-ttu-id="2068c-153">連接 toohello 虛擬機器之後, hello 下一個工作是 tooinstall 封裝所需的 hello 虛擬機器上的網域加入。</span><span class="sxs-lookup"><span data-stu-id="2068c-153">After connecting toohello virtual machine, hello next task is tooinstall packages required for domain join on hello virtual machine.</span></span> <span data-ttu-id="2068c-154">執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="2068c-154">Perform hello following steps:</span></span>

1. <span data-ttu-id="2068c-155">**安裝 realmd:** hello realmd 封裝用於加入網域。</span><span class="sxs-lookup"><span data-stu-id="2068c-155">**Install realmd:** hello realmd package is used for domain join.</span></span> <span data-ttu-id="2068c-156">在您 PuTTY 終端機中，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="2068c-156">In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="2068c-157">sudo yum install realmd</span><span class="sxs-lookup"><span data-stu-id="2068c-157">sudo yum install realmd</span></span>

    ![安裝 realmd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-realmd.png)

    <span data-ttu-id="2068c-159">在幾分鐘後應該取得安裝 hello realmd 套件 hello 虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="2068c-159">After a few minutes, hello realmd package should get installed on hello virtual machine.</span></span>

    ![realmd 已安裝](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-installed.png)
2. <span data-ttu-id="2068c-161">**安裝 sssd:** hello realmd 套件相依於 sssd tooperform 網域加入作業。</span><span class="sxs-lookup"><span data-stu-id="2068c-161">**Install sssd:** hello realmd package depends on sssd tooperform domain join operations.</span></span> <span data-ttu-id="2068c-162">在您 PuTTY 終端機中，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="2068c-162">In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="2068c-163">sudo yum install sssd</span><span class="sxs-lookup"><span data-stu-id="2068c-163">sudo yum install sssd</span></span>

    ![安裝 sssd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-sssd.png)

    <span data-ttu-id="2068c-165">在幾分鐘後應該取得安裝 hello sssd 套件 hello 虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="2068c-165">After a few minutes, hello sssd package should get installed on hello virtual machine.</span></span>

    ![realmd 已安裝](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-sssd-installed.png)
3. <span data-ttu-id="2068c-167">**安裝 kerberos:**您 PuTTY 的終端機中輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="2068c-167">**Install kerberos:** In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="2068c-168">sudo yum install krb5-workstation krb5-libs</span><span class="sxs-lookup"><span data-stu-id="2068c-168">sudo yum install krb5-workstation krb5-libs</span></span>

    ![安裝 kerberos](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-kerberos.png)

    <span data-ttu-id="2068c-170">在幾分鐘後應該取得安裝 hello realmd 套件 hello 虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="2068c-170">After a few minutes, hello realmd package should get installed on hello virtual machine.</span></span>

    ![Kerberos 已安裝](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kerberos-installed.png)

## <a name="join-hello-linux-virtual-machine-toohello-managed-domain"></a><span data-ttu-id="2068c-172">加入 hello Linux 虛擬機器 toohello 受管理的網域</span><span class="sxs-lookup"><span data-stu-id="2068c-172">Join hello Linux virtual machine toohello managed domain</span></span>
<span data-ttu-id="2068c-173">現在，hello Linux 虛擬機器上安裝所需的 hello 封裝，hello 下一項工作就會是 toojoin hello 虛擬機器 toohello 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="2068c-173">Now that hello required packages are installed on hello Linux virtual machine, hello next task is toojoin hello virtual machine toohello managed domain.</span></span>

1. <span data-ttu-id="2068c-174">探索 hello AAD 網域服務受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="2068c-174">Discover hello AAD Domain Services managed domain.</span></span> <span data-ttu-id="2068c-175">在您 PuTTY 終端機中，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="2068c-175">In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="2068c-176">sudo realm discover CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="2068c-176">sudo realm discover CONTOSO100.COM</span></span>

    ![realm discover](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-discover.png)

    <span data-ttu-id="2068c-178">如果**領域探索**是無法 toofind 您受管理的網域，請確定該 hello 網域可連線從 hello 虛擬機器 (請嘗試 ping)。</span><span class="sxs-lookup"><span data-stu-id="2068c-178">If **realm discover** is unable toofind your managed domain, ensure that hello domain is reachable from hello virtual machine (try ping).</span></span> <span data-ttu-id="2068c-179">此外也請確認該 hello 虛擬機器已確實已部署的 toohello 在哪一個 hello 受管理的網域都位於相同虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="2068c-179">Also ensure that hello virtual machine has indeed been deployed toohello same virtual network in which hello managed domain is available.</span></span>
2. <span data-ttu-id="2068c-180">初始化 kerberos。</span><span class="sxs-lookup"><span data-stu-id="2068c-180">Initialize kerberos.</span></span> <span data-ttu-id="2068c-181">在您 PuTTY 終端機中，輸入下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="2068c-181">In your PuTTY terminal, type hello following command.</span></span> <span data-ttu-id="2068c-182">請確認您指定隸屬 toohello ' AAD DC Administrators' 群組的使用者身分。</span><span class="sxs-lookup"><span data-stu-id="2068c-182">Ensure that you specify a user who belongs toohello 'AAD DC Administrators' group.</span></span> <span data-ttu-id="2068c-183">只有這些使用者可以加入電腦 toohello 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="2068c-183">Only these users can join computers toohello managed domain.</span></span>

    <span data-ttu-id="2068c-184">kinit bob@CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="2068c-184">kinit bob@CONTOSO100.COM</span></span>

    ![kinit ](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kinit.png)

    <span data-ttu-id="2068c-186">請確定您指定 hello 網域名稱以大寫的字母，且其他 kinit 失敗。</span><span class="sxs-lookup"><span data-stu-id="2068c-186">Ensure that you specify hello domain name in capital letters, else kinit fails.</span></span>
3. <span data-ttu-id="2068c-187">加入 hello 機器 toohello 網域。</span><span class="sxs-lookup"><span data-stu-id="2068c-187">Join hello machine toohello domain.</span></span> <span data-ttu-id="2068c-188">在您 PuTTY 終端機中，輸入下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="2068c-188">In your PuTTY terminal, type hello following command.</span></span> <span data-ttu-id="2068c-189">指定 hello hello 前面步驟 ('kinit') 中所指定的同一個使用者。</span><span class="sxs-lookup"><span data-stu-id="2068c-189">Specify hello same user you specified in hello preceding step ('kinit').</span></span>

    <span data-ttu-id="2068c-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span><span class="sxs-lookup"><span data-stu-id="2068c-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span></span>

    ![加入領域](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-join.png)

<span data-ttu-id="2068c-192">您應該會收到訊息 （「 已順利註冊機器領域中 」） hello 機器時已成功的 toohello 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="2068c-192">You should get a message ("Successfully enrolled machine in realm") when hello machine is successfully joined toohello managed domain.</span></span>

## <a name="verify-domain-join"></a><span data-ttu-id="2068c-193">確認加入網域</span><span class="sxs-lookup"><span data-stu-id="2068c-193">Verify domain join</span></span>
<span data-ttu-id="2068c-194">您可以快速驗證 hello 機器是否已成功加入的 toohello 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="2068c-194">You can quickly verify whether hello machine has been successfully joined toohello managed domain.</span></span> <span data-ttu-id="2068c-195">連接 toohello 加入 RHEL VM 是否已正確地解決 hello 使用者帳戶使用 SSH 和網域使用者帳戶，然後核取 toosee 新網域。</span><span class="sxs-lookup"><span data-stu-id="2068c-195">Connect toohello newly domain joined RHEL VM using SSH and a domain user account and then check toosee if hello user account is resolved correctly.</span></span>

1. <span data-ttu-id="2068c-196">在您 PuTTY 終端機，下列命令 tooconnect toohello 新類型 hello 中使用 SSH RHEL 虛擬機器加入網域。</span><span class="sxs-lookup"><span data-stu-id="2068c-196">In your PuTTY terminal, type hello following command tooconnect toohello newly domain joined RHEL virtual machine using SSH.</span></span> <span data-ttu-id="2068c-197">使用網域帳戶所屬 toohello 受管理的網域 (例如，'bob@CONTOSO100.COM' 在此情況下。)</span><span class="sxs-lookup"><span data-stu-id="2068c-197">Use a domain account that belongs toohello managed domain (for example, 'bob@CONTOSO100.COM' in this case.)</span></span>

    <span data-ttu-id="2068c-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="2068c-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span></span>
2. <span data-ttu-id="2068c-199">您 PuTTY 的終端機中輸入下列命令 toosee，如果已正確初始化 hello 主目錄的 hello。</span><span class="sxs-lookup"><span data-stu-id="2068c-199">In your PuTTY terminal, type hello following command toosee if hello home directory was initialized correctly.</span></span>

    <span data-ttu-id="2068c-200">pwd</span><span class="sxs-lookup"><span data-stu-id="2068c-200">pwd</span></span>
3. <span data-ttu-id="2068c-201">您 PuTTY 的終端機中輸入下列命令 toosee，如果正在正確解析 hello 群組成員資格的 hello。</span><span class="sxs-lookup"><span data-stu-id="2068c-201">In your PuTTY terminal, type hello following command toosee if hello group memberships are being resolved correctly.</span></span>

    <span data-ttu-id="2068c-202">id</span><span class="sxs-lookup"><span data-stu-id="2068c-202">id</span></span>

<span data-ttu-id="2068c-203">這些命令的輸出範例如下：</span><span class="sxs-lookup"><span data-stu-id="2068c-203">A sample output of these commands follows:</span></span>

![確認加入網域](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-verify-domain-join.png)

## <a name="troubleshooting-domain-join"></a><span data-ttu-id="2068c-205">針對加入網域進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="2068c-205">Troubleshooting domain join</span></span>
<span data-ttu-id="2068c-206">請參閱 toohello[疑難排解網域加入](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join)發行項。</span><span class="sxs-lookup"><span data-stu-id="2068c-206">Refer toohello [Troubleshooting domain join](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) article.</span></span>

## <a name="related-content"></a><span data-ttu-id="2068c-207">相關內容</span><span class="sxs-lookup"><span data-stu-id="2068c-207">Related Content</span></span>
* [<span data-ttu-id="2068c-208">Azure AD Domain Services - 入門指南</span><span class="sxs-lookup"><span data-stu-id="2068c-208">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="2068c-209">加入 Windows Server 虛擬機器 tooan Azure AD 網域服務受管理的網域</span><span class="sxs-lookup"><span data-stu-id="2068c-209">Join a Windows Server virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* <span data-ttu-id="2068c-210">[如何 tooa 執行 Linux 的虛擬機器上的 toolog](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="2068c-210">[How toolog on tooa virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* [<span data-ttu-id="2068c-211">安裝 Kerberos</span><span class="sxs-lookup"><span data-stu-id="2068c-211">Installing Kerberos</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [<span data-ttu-id="2068c-212">Red Hat Enterprise Linux 7 - Windows 整合指南</span><span class="sxs-lookup"><span data-stu-id="2068c-212">Red Hat Enterprise Linux 7 - Windows Integration Guide</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)
