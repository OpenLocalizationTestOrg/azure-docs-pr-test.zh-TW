---
title: "Azure Active Directory Domain Services：將 RHEL VM 加入受管理的網域 | Microsoft Docs"
description: "將 Red Hat Enterprise Linux 虛擬機器加入 Azure AD 網域服務"
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
ms.openlocfilehash: 69f1850bfed90392e9a4695e2443ffaa6bfc746d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-red-hat-enterprise-linux-7-virtual-machine-to-a-managed-domain"></a><span data-ttu-id="d1ae2-103">將 Red Hat Enterprise Linux 7 虛擬機器加入受管理的網域</span><span class="sxs-lookup"><span data-stu-id="d1ae2-103">Join a Red Hat Enterprise Linux 7 virtual machine to a managed domain</span></span>
<span data-ttu-id="d1ae2-104">本文說明如何將 Red Hat Enterprise Linux (RHEL) 7 虛擬機器加入 Azure AD 網域服務受管理網域。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-104">This article shows you how to join a Red Hat Enterprise Linux (RHEL) 7 virtual machine to an Azure AD Domain Services managed domain.</span></span>

## <a name="provision-a-red-hat-enterprise-linux-virtual-machine"></a><span data-ttu-id="d1ae2-105">佈建 Red Hat Enterprise Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="d1ae2-105">Provision a Red Hat Enterprise Linux virtual machine</span></span>
<span data-ttu-id="d1ae2-106">請執行下列步驟，以使用 Azure 入口網站佈建 RHEL 7 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-106">Perform the following steps to provision a RHEL 7 virtual machine using the Azure portal.</span></span>

1. <span data-ttu-id="d1ae2-107">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-107">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

    ![Azure 入口網站儀表板](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-dashboard.png)
2. <span data-ttu-id="d1ae2-109">按一下左邊窗格中的 [新增]，然後在搜尋列中輸入 **Red Hat**，如以下螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-109">Click **New** on the left pane and type **Red Hat** into the search bar as shown in the following screenshot.</span></span> <span data-ttu-id="d1ae2-110">搜尋結果中會出現 Red Hat Enterprise Linux 的項目。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-110">Entries for Red Hat Enterprise Linux appear in the search results.</span></span> <span data-ttu-id="d1ae2-111">按一下 [Red Hat Enterprise Linux 7.2]。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-111">Click **Red Hat Enterprise Linux 7.2**.</span></span>

    ![在結果中選取 RHEL](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-find-rhel-image.png)
3. <span data-ttu-id="d1ae2-113">[所有項目]  窗格中的搜尋結果應該會列出 Red Hat Enterprise Linux 7.2 映像。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-113">The search results in the **Everything** pane should list the Red Hat Enterprise Linux 7.2 image.</span></span> <span data-ttu-id="d1ae2-114">按一下 [Red Hat Enterprise Linux 7.2]  來檢視虛擬機器映像的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-114">Click **Red Hat Enterprise Linux 7.2** to view more information about the virtual machine image.</span></span>

    ![在結果中選取 RHEL](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-rhel-image.png)
4. <span data-ttu-id="d1ae2-116">在 [Red Hat Enterprise Linux 7.2]  窗格中，您應該會看到虛擬機器映像的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-116">In the **Red Hat Enterprise Linux 7.2** pane, you should see more information about the virtual machine image.</span></span> <span data-ttu-id="d1ae2-117">在 [選取部署模型] 下拉式清單中，選取 [傳統]。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-117">In the **Select a deployment model** dropdown, select **Classic**.</span></span> <span data-ttu-id="d1ae2-118">然後按一下 [建立]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-118">Then click the **Create** button.</span></span>

    ![檢視映像的詳細資料](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-clicked.png)
5. <span data-ttu-id="d1ae2-120">在「建立虛擬機器」精靈的 [基本] 頁面中，輸入新虛擬機器的 [主機名稱]。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-120">In the **Basics** page of the **Create virtual machine** wizard, enter the **Host Name** for the new virtual machine.</span></span> <span data-ttu-id="d1ae2-121">另外，請在 [使用者名稱] 欄位中指定本機系統管理員使用者名稱，以及指定 [密碼]。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-121">Also specify a local administrator user name in the **User name** field and a **Password**.</span></span> <span data-ttu-id="d1ae2-122">您也可以選擇使用 SSH 金鑰來驗證本機系統管理員使用者。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-122">You may also choose to use an SSH key to authenticate the local administrator user.</span></span> <span data-ttu-id="d1ae2-123">另外，請選取虛擬機器的 [定價層]  。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-123">Also select a **Pricing Tier** for the virtual machine.</span></span>

    ![建立 VM - 基本頁面](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-basic-details.png)
6. <span data-ttu-id="d1ae2-125">在「建立虛擬機器」精靈的 [大小] 頁面中，選取虛擬機器的大小。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-125">In the **Size** page of the **Create virtual machine** wizard, select the size for the virtual machine.</span></span>

    ![建立 VM - 選取大小](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-vm-size.png)

7. <span data-ttu-id="d1ae2-127">在「建立虛擬機器」精靈的 [設定] 頁面中，選取虛擬機器的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-127">In the **Settings** page of the **Create virtual machine** wizard, select the storage account for the virtual machine.</span></span> <span data-ttu-id="d1ae2-128">按一下 [虛擬網路] 以選取應作為 Linux VM 部署位置的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-128">Click **Virtual Network** to select the virtual network to which the Linux VM should be deployed.</span></span> <span data-ttu-id="d1ae2-129">在 [虛擬網路] 刀鋒視窗中，選取有提供 Azure AD Domain Services 的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-129">In the **Virtual Network** blade, select the virtual network in which Azure AD Domain Services is available.</span></span> <span data-ttu-id="d1ae2-130">在此範例中，我們挑選 'MyPreviewVNet' 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-130">In this example, we pick the 'MyPreviewVNet' virtual network.</span></span>

    ![建立 VM - 選取虛擬網路](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-select-vnet.png)
8. <span data-ttu-id="d1ae2-132">在「建立虛擬機器」精靈的 [摘要] 頁面上，檢閱後按一下 [確定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-132">On the **Summary** page of the **Create virtual machine** wizard, review and click the **OK** button.</span></span>

    ![建立 VM - 選取的虛擬網路](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-vnet-selected.png)
9. <span data-ttu-id="d1ae2-134">此時應該會開始根據 RHEL 7.2 映像部署新虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-134">Deployment of the new virtual machine based on the RHEL 7.2 image should start.</span></span>

    ![建立 VM - 部署開始](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployment-started.png)
10. <span data-ttu-id="d1ae2-136">幾分鐘後，虛擬機器應該會部署成功並可供使用。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-136">After a few minutes, the virtual machine should be deployed successfully and ready for use.</span></span>

    ![建立 VM - 已部署](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployed.png)

## <a name="connect-remotely-to-the-newly-provisioned-linux-virtual-machine"></a><span data-ttu-id="d1ae2-138">遠端連線到新佈建的 Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="d1ae2-138">Connect remotely to the newly provisioned Linux virtual machine</span></span>
<span data-ttu-id="d1ae2-139">RHEL 7.2 虛擬機器已佈建在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-139">The RHEL 7.2 virtual machine has been provisioned in Azure.</span></span> <span data-ttu-id="d1ae2-140">下一個工作是從遠端連線至虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-140">The next task is to connect remotely to the virtual machine.</span></span>

<span data-ttu-id="d1ae2-141">**連線到 RHEL 7.2 虛擬機器** 依照[如何登入執行 Linux 的虛擬機器](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)一文中的指示操作。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-141">**Connect to the RHEL 7.2 virtual machine** Follow the instructions in the article [How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="d1ae2-142">剩餘步驟是假設您使用 PuTTY SSH 用戶端來連線到 RHEL 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-142">The rest of the steps assume you use the PuTTY SSH client to connect to the RHEL virtual machine.</span></span> <span data-ttu-id="d1ae2-143">如需詳細資訊，請參閱 [PuTTY 下載頁面](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-143">For more information, see the [PuTTY Download page](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

1. <span data-ttu-id="d1ae2-144">開啟 PuTTY 程式。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-144">Open the PuTTY program.</span></span>
2. <span data-ttu-id="d1ae2-145">針對新建立的 RHEL 虛擬機器輸入 [主機名稱]  。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-145">Enter the **Host Name** for the newly created RHEL virtual machine.</span></span> <span data-ttu-id="d1ae2-146">在此範例中，我們的虛擬機器的主機名稱為 'contoso-rhel.cloudapp.net'。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-146">In this example, our virtual machine has the host name 'contoso-rhel.cloudapp.net'.</span></span> <span data-ttu-id="d1ae2-147">如果您不確定您的 VM 的主機名稱，請參閱 Azure 入口網站上的 VM 儀表板。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-147">If you are not sure of the host name of your VM, refer to the VM dashboard on the Azure portal.</span></span>

    ![PuTTY 連線](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-connect.png)
3. <span data-ttu-id="d1ae2-149">使用建立虛擬機器時指定的本機系統管理員認證來登入虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-149">Log on to the virtual machine using the local administrator credentials you specified when the virtual machine was created.</span></span> <span data-ttu-id="d1ae2-150">在此範例中，我們使用了本機系統管理員帳戶 "mahesh"。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-150">In this example, we used the local administrator account "mahesh".</span></span>

    ![PuTTY 登入](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-login.png)

## <a name="install-required-packages-on-the-linux-virtual-machine"></a><span data-ttu-id="d1ae2-152">在 Linux 虛擬機器上安裝必要封裝</span><span class="sxs-lookup"><span data-stu-id="d1ae2-152">Install required packages on the Linux virtual machine</span></span>
<span data-ttu-id="d1ae2-153">在連線到虛擬機器後，下一個工作是在虛擬機器上安裝要加入網域所需的封裝。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-153">After connecting to the virtual machine, the next task is to install packages required for domain join on the virtual machine.</span></span> <span data-ttu-id="d1ae2-154">執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d1ae2-154">Perform the following steps:</span></span>

1. <span data-ttu-id="d1ae2-155">**安裝 realmd：** realmd 封裝可用於加入網域。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-155">**Install realmd:** The realmd package is used for domain join.</span></span> <span data-ttu-id="d1ae2-156">在 PuTTY 終端機中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="d1ae2-156">In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="d1ae2-157">sudo yum install realmd</span><span class="sxs-lookup"><span data-stu-id="d1ae2-157">sudo yum install realmd</span></span>

    ![安裝 realmd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-realmd.png)

    <span data-ttu-id="d1ae2-159">幾分鐘之後，realmd 封裝應該就會安裝在虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-159">After a few minutes, the realmd package should get installed on the virtual machine.</span></span>

    ![realmd 已安裝](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-installed.png)
2. <span data-ttu-id="d1ae2-161">**安裝 sssd：** realmd 套件需倚賴 sssd 執行加入網域作業。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-161">**Install sssd:** The realmd package depends on sssd to perform domain join operations.</span></span> <span data-ttu-id="d1ae2-162">在 PuTTY 終端機中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="d1ae2-162">In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="d1ae2-163">sudo yum install sssd</span><span class="sxs-lookup"><span data-stu-id="d1ae2-163">sudo yum install sssd</span></span>

    ![安裝 sssd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-sssd.png)

    <span data-ttu-id="d1ae2-165">幾分鐘之後，sssd 封裝應該就會安裝在虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-165">After a few minutes, the sssd package should get installed on the virtual machine.</span></span>

    ![realmd 已安裝](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-sssd-installed.png)
3. <span data-ttu-id="d1ae2-167">**安裝 Kerberos：**在 PuTTY 終端機中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="d1ae2-167">**Install kerberos:** In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="d1ae2-168">sudo yum install krb5-workstation krb5-libs</span><span class="sxs-lookup"><span data-stu-id="d1ae2-168">sudo yum install krb5-workstation krb5-libs</span></span>

    ![安裝 kerberos](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-kerberos.png)

    <span data-ttu-id="d1ae2-170">幾分鐘之後，realmd 封裝應該就會安裝在虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-170">After a few minutes, the realmd package should get installed on the virtual machine.</span></span>

    ![Kerberos 已安裝](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kerberos-installed.png)

## <a name="join-the-linux-virtual-machine-to-the-managed-domain"></a><span data-ttu-id="d1ae2-172">將 Linux 虛擬機器加入受管理的網域</span><span class="sxs-lookup"><span data-stu-id="d1ae2-172">Join the Linux virtual machine to the managed domain</span></span>
<span data-ttu-id="d1ae2-173">既然 Linux 虛擬機器上已安裝必要的封裝，下一個工作是將虛擬機器加入受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-173">Now that the required packages are installed on the Linux virtual machine, the next task is to join the virtual machine to the managed domain.</span></span>

1. <span data-ttu-id="d1ae2-174">探索 AAD 網域服務受管理網域。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-174">Discover the AAD Domain Services managed domain.</span></span> <span data-ttu-id="d1ae2-175">在 PuTTY 終端機中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="d1ae2-175">In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="d1ae2-176">sudo realm discover CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="d1ae2-176">sudo realm discover CONTOSO100.COM</span></span>

    ![realm discover](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-discover.png)

    <span data-ttu-id="d1ae2-178">如果 **realm discover** 無法找到受管理的網域，請確定可從虛擬機器連線到網域 (請嘗試 ping)。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-178">If **realm discover** is unable to find your managed domain, ensure that the domain is reachable from the virtual machine (try ping).</span></span> <span data-ttu-id="d1ae2-179">也請確定虛擬機器已確實部署到有提供受管理網域的相同虛擬網路上。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-179">Also ensure that the virtual machine has indeed been deployed to the same virtual network in which the managed domain is available.</span></span>
2. <span data-ttu-id="d1ae2-180">初始化 kerberos。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-180">Initialize kerberos.</span></span> <span data-ttu-id="d1ae2-181">在 PuTTY 終端機中輸入下列命令。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-181">In your PuTTY terminal, type the following command.</span></span> <span data-ttu-id="d1ae2-182">請確定您是指定屬於 'AAD DC Administrators' 群組的使用者。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-182">Ensure that you specify a user who belongs to the 'AAD DC Administrators' group.</span></span> <span data-ttu-id="d1ae2-183">只有這些使用者可以將電腦加入受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-183">Only these users can join computers to the managed domain.</span></span>

    <span data-ttu-id="d1ae2-184">kinit bob@CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="d1ae2-184">kinit bob@CONTOSO100.COM</span></span>

    ![kinit ](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kinit.png)

    <span data-ttu-id="d1ae2-186">請確定您是以大寫字母指定網域名稱，否則 kinit 會失敗。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-186">Ensure that you specify the domain name in capital letters, else kinit fails.</span></span>
3. <span data-ttu-id="d1ae2-187">將電腦加入網域。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-187">Join the machine to the domain.</span></span> <span data-ttu-id="d1ae2-188">在 PuTTY 終端機中輸入下列命令。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-188">In your PuTTY terminal, type the following command.</span></span> <span data-ttu-id="d1ae2-189">指定您在前面步驟中指定的相同使用者 ('kinit')。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-189">Specify the same user you specified in the preceding step ('kinit').</span></span>

    <span data-ttu-id="d1ae2-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span><span class="sxs-lookup"><span data-stu-id="d1ae2-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span></span>

    ![加入領域](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-join.png)

<span data-ttu-id="d1ae2-192">當電腦成功加入受管理的網域時，您應該會收到訊息 (「已成功在領域中註冊電腦」)。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-192">You should get a message ("Successfully enrolled machine in realm") when the machine is successfully joined to the managed domain.</span></span>

## <a name="verify-domain-join"></a><span data-ttu-id="d1ae2-193">確認加入網域</span><span class="sxs-lookup"><span data-stu-id="d1ae2-193">Verify domain join</span></span>
<span data-ttu-id="d1ae2-194">您可以快速確認電腦是否已成功加入受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-194">You can quickly verify whether the machine has been successfully joined to the managed domain.</span></span> <span data-ttu-id="d1ae2-195">使用 SSH 和網域使用者帳戶連接到新加入網域的 RHEL VM，然後查看使用者帳戶是否解析正確。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-195">Connect to the newly domain joined RHEL VM using SSH and a domain user account and then check to see if the user account is resolved correctly.</span></span>

1. <span data-ttu-id="d1ae2-196">在 PuTTY 終端機中輸入下列命令，以使用 SSH 連線到新加入網域的 RHEL 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-196">In your PuTTY terminal, type the following command to connect to the newly domain joined RHEL virtual machine using SSH.</span></span> <span data-ttu-id="d1ae2-197">使用屬於受管理網域的網域帳戶 (例如，在此例中為 'bob@CONTOSO100.COM')。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-197">Use a domain account that belongs to the managed domain (for example, 'bob@CONTOSO100.COM' in this case.)</span></span>

    <span data-ttu-id="d1ae2-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="d1ae2-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span></span>
2. <span data-ttu-id="d1ae2-199">在 PuTTY 終端機中輸入下列命令，以查看是否已正確初始化主目錄。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-199">In your PuTTY terminal, type the following command to see if the home directory was initialized correctly.</span></span>

    <span data-ttu-id="d1ae2-200">pwd</span><span class="sxs-lookup"><span data-stu-id="d1ae2-200">pwd</span></span>
3. <span data-ttu-id="d1ae2-201">在 PuTTY 終端機中輸入下列命令，以查看是否會正確解析群組成員資格。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-201">In your PuTTY terminal, type the following command to see if the group memberships are being resolved correctly.</span></span>

    <span data-ttu-id="d1ae2-202">id</span><span class="sxs-lookup"><span data-stu-id="d1ae2-202">id</span></span>

<span data-ttu-id="d1ae2-203">這些命令的輸出範例如下：</span><span class="sxs-lookup"><span data-stu-id="d1ae2-203">A sample output of these commands follows:</span></span>

![確認加入網域](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-verify-domain-join.png)

## <a name="troubleshooting-domain-join"></a><span data-ttu-id="d1ae2-205">針對加入網域進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="d1ae2-205">Troubleshooting domain join</span></span>
<span data-ttu-id="d1ae2-206">請參閱 [針對加入網域進行疑難排解](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) 一文。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-206">Refer to the [Troubleshooting domain join](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) article.</span></span>

## <a name="related-content"></a><span data-ttu-id="d1ae2-207">相關內容</span><span class="sxs-lookup"><span data-stu-id="d1ae2-207">Related Content</span></span>
* [<span data-ttu-id="d1ae2-208">Azure AD Domain Services - 入門指南</span><span class="sxs-lookup"><span data-stu-id="d1ae2-208">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="d1ae2-209">將 Windows Server 虛擬機器加入 Azure AD 網域服務受管理的網域</span><span class="sxs-lookup"><span data-stu-id="d1ae2-209">Join a Windows Server virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* <span data-ttu-id="d1ae2-210">[如何登入執行 Linux 的虛擬機器](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="d1ae2-210">[How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* [<span data-ttu-id="d1ae2-211">安裝 Kerberos</span><span class="sxs-lookup"><span data-stu-id="d1ae2-211">Installing Kerberos</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [<span data-ttu-id="d1ae2-212">Red Hat Enterprise Linux 7 - Windows 整合指南</span><span class="sxs-lookup"><span data-stu-id="d1ae2-212">Red Hat Enterprise Linux 7 - Windows Integration Guide</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)
