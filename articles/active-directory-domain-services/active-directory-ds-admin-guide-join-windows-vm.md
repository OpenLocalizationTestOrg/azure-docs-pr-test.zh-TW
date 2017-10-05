---
title: "Azure Active Directory Domain Services：將 Windows Server VM 加入受管理的網域 | Microsoft Docs"
description: "將 Windows Server 虛擬機器加入 Azure AD 網域服務"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 74dbdb33-05db-4d47-badc-0d7bb6d0c8cb
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 9f8d21f6964d26a2e17e31d1f2947e7eb07c177d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-windows-server-virtual-machine-to-a-managed-domain"></a><span data-ttu-id="23fe8-103">將 Windows Server 虛擬機器加入受管理的網域</span><span class="sxs-lookup"><span data-stu-id="23fe8-103">Join a Windows Server virtual machine to a managed domain</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="23fe8-104">Azure 傳統入口網站 - Windows</span><span class="sxs-lookup"><span data-stu-id="23fe8-104">Azure classic portal - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
> * [<span data-ttu-id="23fe8-105">PowerShell - Windows</span><span class="sxs-lookup"><span data-stu-id="23fe8-105">PowerShell - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

<span data-ttu-id="23fe8-106">本文說明如何使用 Azure 傳統入口網站，將執行 Windows Server 2012 R2 的虛擬機器加入 Azure AD 網域服務受管理網域。</span><span class="sxs-lookup"><span data-stu-id="23fe8-106">This article shows you how to join a virtual machine running Windows Server 2012 R2 to an Azure AD Domain Services managed domain, using the Azure classic portal.</span></span>

## <a name="step-1-create-the-windows-server-virtual-machine"></a><span data-ttu-id="23fe8-107">步驟 1︰建立 Windows Server 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="23fe8-107">Step 1: Create the Windows Server virtual machine</span></span>
<span data-ttu-id="23fe8-108">請依照[在 Azure 傳統入口網站中建立執行 Windows 的虛擬機器](../virtual-machines/windows/classic/tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)教學課程中所述的指示操作。</span><span class="sxs-lookup"><span data-stu-id="23fe8-108">Follow the instructions outlined in the [Create a virtual machine running Windows in the Azure classic portal](../virtual-machines/windows/classic/tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) tutorial.</span></span> <span data-ttu-id="23fe8-109">務必要確實將此新建立的虛擬機器加入已在其中啟用 Azure AD 網域服務的相同虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="23fe8-109">It is important to ensure that this newly created virtual machine is joined to the same virtual network in which you enabled Azure AD Domain Services.</span></span> <span data-ttu-id="23fe8-110">[快速建立] 選項無法讓您將虛擬機器加入虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="23fe8-110">The 'Quick Create' option does not enable you to join the virtual machine to a virtual network.</span></span> <span data-ttu-id="23fe8-111">因此，您必須使用 [從資源庫] 選項來建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="23fe8-111">Therefore, you need to use the 'From Gallery' option to create the virtual machine.</span></span>

<span data-ttu-id="23fe8-112">執行下列步驟，以建立 Windows 虛擬機器，並將其加入已在其中啟用 Azure AD 網域服務的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="23fe8-112">Perform the following steps to create a Windows virtual machine joined to the virtual network in which you've enabled Azure AD Domain Services.</span></span>

1. <span data-ttu-id="23fe8-113">在 Azure 傳統入口網站中，按一下視窗底部命令列上的 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="23fe8-113">In the Azure classic portal, on the command bar at the bottom of the window, click **New**.</span></span>
2. <span data-ttu-id="23fe8-114">在 [計算] 底下，依序按一下 [虛擬機器] 和 [從資源庫]。</span><span class="sxs-lookup"><span data-stu-id="23fe8-114">Under **Compute**, click **Virtual Machine**, then click **From Gallery**.</span></span>
3. <span data-ttu-id="23fe8-115">第一個畫面可讓您從可用的映像清單中，為您的虛擬機器 [選擇映像]  。</span><span class="sxs-lookup"><span data-stu-id="23fe8-115">The first screen lets you **Choose an Image** for your virtual machine from the list of available images.</span></span> <span data-ttu-id="23fe8-116">請選擇適當的映像。</span><span class="sxs-lookup"><span data-stu-id="23fe8-116">Pick the appropriate image.</span></span>

    ![選取映像](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-image.png)
4. <span data-ttu-id="23fe8-118">第二個畫面可讓您挑選電腦名稱、大小，及系統管理使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="23fe8-118">The second screen lets you pick a computer name, size, and administrative user name and password.</span></span> <span data-ttu-id="23fe8-119">使用執行應用程式或工作負載所需的層次和大小。</span><span class="sxs-lookup"><span data-stu-id="23fe8-119">Use the tier and size required to run your app or workload.</span></span> <span data-ttu-id="23fe8-120">您在此挑選的使用者名稱會是機器上的本機系統管理員使用者。</span><span class="sxs-lookup"><span data-stu-id="23fe8-120">The user name you pick here is a local administrator user on the machine.</span></span> <span data-ttu-id="23fe8-121">請勿在此輸入網域使用者帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="23fe8-121">Do not enter a domain user account's credentials here.</span></span>

    ![設定虛擬機器](./media/active-directory-domain-services-admin-guide/create-windows-vm-config.png)
5. <span data-ttu-id="23fe8-123">第三個畫面可讓您設定網路、儲存體和可用性的資源。</span><span class="sxs-lookup"><span data-stu-id="23fe8-123">The third screen lets you configure resources for networking, storage, and availability.</span></span> <span data-ttu-id="23fe8-124">請在 [區域/同質群組/虛擬網路]  下拉式清單中確實選取已在其中啟用 Azure AD 網域服務的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="23fe8-124">Ensure you select the virtual network in which you enabled Azure AD Domain Services from the **Region/Affinity Group/Virtual Network** dropdown.</span></span> <span data-ttu-id="23fe8-125">為虛擬機器指定合適的 [雲端服務 DNS 名稱]  。</span><span class="sxs-lookup"><span data-stu-id="23fe8-125">Specify a **Cloud Service DNS Name** as appropriate for the virtual machine.</span></span>

    ![選取虛擬機器的虛擬網路](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-vnet.png)

   > [!WARNING]
   > <span data-ttu-id="23fe8-127">請確定將虛擬機器加入您已在其中啟用 Azure AD Domain Services 的相同虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="23fe8-127">Ensure that you join the virtual machine to the same virtual network in which you've enabled Azure AD Domain Services.</span></span> <span data-ttu-id="23fe8-128">因此，虛擬機器可以「看到」網域並執行加入網域之類的工作。</span><span class="sxs-lookup"><span data-stu-id="23fe8-128">As a result, the virtual machine can 'see' the domain and perform tasks such as joining the domain.</span></span> <span data-ttu-id="23fe8-129">如果您選擇在不同虛擬網路中建立虛擬機器，請將該虛擬網路連接到您已在其中啟用 Azure AD Domain Services 的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="23fe8-129">If you choose to create the virtual machine in a different virtual network, connect that virtual network to the virtual network in which you've enabled Azure AD Domain Services.</span></span>
   >
   >
6. <span data-ttu-id="23fe8-130">第四個畫面可讓您安裝 VM 代理程式及設定部分可用延伸模組。</span><span class="sxs-lookup"><span data-stu-id="23fe8-130">The fourth screen lets you install the VM Agent and configure some of the available extensions.</span></span>

    ![完成](./media/active-directory-domain-services-admin-guide/create-windows-vm-done.png)
7. <span data-ttu-id="23fe8-132">建立虛擬機器後，傳統入口網站會在 [虛擬機器]  節點底下列出新的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="23fe8-132">After the virtual machine is created, the classic portal lists the new virtual machine under the **Virtual Machines** node.</span></span> <span data-ttu-id="23fe8-133">虛擬機器和雲端服務都會自動啟動，而且它們的狀態會顯示為 [執行中] 。</span><span class="sxs-lookup"><span data-stu-id="23fe8-133">Both the virtual machine and cloud service are started automatically and their status is listed as **Running**.</span></span>

    ![虛擬機器已啟動並執行](./media/active-directory-domain-services-admin-guide/create-windows-vm-running.png)

## <a name="step-2-connect-to-the-windows-server-virtual-machine-using-the-local-administrator-account"></a><span data-ttu-id="23fe8-135">步驟 2︰使用本機系統管理員帳戶連線到 Windows Server 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="23fe8-135">Step 2: Connect to the Windows Server virtual machine using the local administrator account</span></span>
<span data-ttu-id="23fe8-136">現在，我們會連線到新建立的 Windows Server 虛擬機器，以便將其加入網域。</span><span class="sxs-lookup"><span data-stu-id="23fe8-136">Now, we connect to the newly created Windows Server virtual machine, to join it to the domain.</span></span> <span data-ttu-id="23fe8-137">使用建立虛擬機器時所指定的本機系統管理員認證，以便與其連線。</span><span class="sxs-lookup"><span data-stu-id="23fe8-137">Use the local administrator credentials you specified when creating the virtual machine, to connect to it.</span></span>

<span data-ttu-id="23fe8-138">執行下列步驟以連線到虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="23fe8-138">Perform the following steps to connect to the virtual machine.</span></span>

1. <span data-ttu-id="23fe8-139">在傳統入口網站中瀏覽至 [虛擬機器]  節點。</span><span class="sxs-lookup"><span data-stu-id="23fe8-139">Navigate to **Virtual Machines** node in the classic portal.</span></span> <span data-ttu-id="23fe8-140">選取您在步驟 1 建立的虛擬機器，然後按一下視窗底部命令列上的 [連線]  。</span><span class="sxs-lookup"><span data-stu-id="23fe8-140">Select the virtual machine you created in Step 1 and click **Connect** on the command bar at the bottom of the window.</span></span>

    ![連線至 Windows 虛擬機器](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. <span data-ttu-id="23fe8-142">傳統入口網站會提示您開啟或儲存副檔名為 '.rdp' 的檔案，其可供用來連線到虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="23fe8-142">The classic portal prompts you to open or save a file with a '.rdp' extension, which is used to connect to the virtual machine.</span></span> <span data-ttu-id="23fe8-143">在檔案下載完成時按一下加以開啟。</span><span class="sxs-lookup"><span data-stu-id="23fe8-143">Click to open the file when it has finished downloading.</span></span>
3. <span data-ttu-id="23fe8-144">在登入提示中，輸入您在建立虛擬機器時所指定的 [本機系統管理員認證] 。</span><span class="sxs-lookup"><span data-stu-id="23fe8-144">At the login prompt, enter your **local administrator credentials**, which you specified while creating the virtual machine.</span></span> <span data-ttu-id="23fe8-145">例如，我們在此範例中使用 'localhost\mahesh'。</span><span class="sxs-lookup"><span data-stu-id="23fe8-145">For example, we've used 'localhost\mahesh' in this example.</span></span>

<span data-ttu-id="23fe8-146">此時，您應該已使用本機系統管理員認證登入到新建立的 Windows 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="23fe8-146">At this point, you should be logged in to the newly created Windows virtual machine using local Administrator credentials.</span></span> <span data-ttu-id="23fe8-147">下一個步驟是將虛擬機器加入網域。</span><span class="sxs-lookup"><span data-stu-id="23fe8-147">The next step is to join the virtual machine to the domain.</span></span>

## <a name="step-3-join-the-windows-server-virtual-machine-to-the-aad-ds-managed-domain"></a><span data-ttu-id="23fe8-148">步驟 3︰將 Windows Server 虛擬機器加入 AAD-DS 受管理網域</span><span class="sxs-lookup"><span data-stu-id="23fe8-148">Step 3: Join the Windows Server virtual machine to the AAD-DS managed domain</span></span>
<span data-ttu-id="23fe8-149">請執行下列步驟，以將 Windows Server 虛擬機器加入 AAD-DS 受管理網域。</span><span class="sxs-lookup"><span data-stu-id="23fe8-149">Perform the following steps to join the Windows Server virtual machine to the AAD-DS managed domain.</span></span>

1. <span data-ttu-id="23fe8-150">如步驟 2 所示連線到 Windows Server。</span><span class="sxs-lookup"><span data-stu-id="23fe8-150">Connect to the Windows Server as shown in Step 2.</span></span> <span data-ttu-id="23fe8-151">在 [開始] 畫面中開啟 [伺服器管理員] 。</span><span class="sxs-lookup"><span data-stu-id="23fe8-151">From the Start screen, open **Server Manager**.</span></span>
2. <span data-ttu-id="23fe8-152">按一下 [伺服器管理員] 視窗之左窗格中的 [本機伺服器]  。</span><span class="sxs-lookup"><span data-stu-id="23fe8-152">Click **Local Server** in the left pane of the Server Manager window.</span></span>

    ![啟動虛擬機器上的伺服器管理員](./media/active-directory-domain-services-admin-guide/join-domain-server-manager.png)
3. <span data-ttu-id="23fe8-154">按一下 [屬性] 區段底下的 [工作群組]。</span><span class="sxs-lookup"><span data-stu-id="23fe8-154">Click **WORKGROUP** under the **PROPERTIES** section.</span></span> <span data-ttu-id="23fe8-155">在 [系統屬性] 屬性頁中，按一下 [變更] 來加入網域。</span><span class="sxs-lookup"><span data-stu-id="23fe8-155">In the **System Properties** property page, click **Change** to join the domain.</span></span>

    ![[系統屬性] 頁面](./media/active-directory-domain-services-admin-guide/join-domain-system-properties.png)
4. <span data-ttu-id="23fe8-157">在 [網域] 文字方塊中指定 Azure AD Domain Services 受管理網域的網域名稱，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="23fe8-157">Specify the domain name of your Azure AD Domain Services managed domain in the **Domain** textbox and click **OK**.</span></span>

    ![指定要加入的網域](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-domain.png)
5. <span data-ttu-id="23fe8-159">系統會提示您輸入認證以便加入網域。</span><span class="sxs-lookup"><span data-stu-id="23fe8-159">You are prompted to enter your credentials to join the domain.</span></span> <span data-ttu-id="23fe8-160">請確定您是 **指定屬於 AAD DC 系統管理員群組之使用者的認證** 。</span><span class="sxs-lookup"><span data-stu-id="23fe8-160">Ensure that you **specify the credentials for a user belonging to the AAD DC Administrators** group.</span></span> <span data-ttu-id="23fe8-161">只有此群組的成員才有權限可以將機器加入受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="23fe8-161">Only members of this group have privileges to join machines to the managed domain.</span></span>

    ![指定用於加入網域的認證](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-credentials.png)
6. <span data-ttu-id="23fe8-163">您可以透過下列任一方式指定認證︰</span><span class="sxs-lookup"><span data-stu-id="23fe8-163">You can specify credentials in either of the following ways:</span></span>

   * <span data-ttu-id="23fe8-164">UPN 格式︰指定 Azure AD 中所設定使用者帳戶的 UPN 尾碼。</span><span class="sxs-lookup"><span data-stu-id="23fe8-164">UPN format: Specify the UPN suffix for the user account, as configured in Azure AD.</span></span> <span data-ttu-id="23fe8-165">在此範例中，使用者 'bob' 的 UPN 尾碼是 'bob@domainservicespreview.onmicrosoft.com'。</span><span class="sxs-lookup"><span data-stu-id="23fe8-165">In this example, the UPN suffix of the user 'bob' is 'bob@domainservicespreview.onmicrosoft.com'.</span></span>
   * <span data-ttu-id="23fe8-166">SAMAccountName 格式︰您可以使用 SAMAccountName 格式指定帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="23fe8-166">SAMAccountName format: You can specify the account name in the SAMAccountName format.</span></span> <span data-ttu-id="23fe8-167">在此範例中，使用者 'bob' 必須輸入 'CONTOSO100\bob'。</span><span class="sxs-lookup"><span data-stu-id="23fe8-167">In this example, the user 'bob' would need to enter 'CONTOSO100\bob'.</span></span>

     > [!NOTE]
     > <span data-ttu-id="23fe8-168">**建議使用 UPN 格式來指定認證。**</span><span class="sxs-lookup"><span data-stu-id="23fe8-168">**We recommend using the UPN format to specify credentials.**</span></span> <span data-ttu-id="23fe8-169">如果使用者的 UPN 前置詞太長 (例如 'joereallylongnameuser')，就可能自動產生 SAMAccountName。</span><span class="sxs-lookup"><span data-stu-id="23fe8-169">The SAMAccountName may be auto-generated if a user's UPN prefix is overly long (for example, 'joereallylongnameuser').</span></span> <span data-ttu-id="23fe8-170">如果您的 Azure AD 租用戶中有多個使用者擁有相同的 UPN 前置詞 (例如 'bob')，則服務可能會自動產生它們的 SAMAccountName 格式。</span><span class="sxs-lookup"><span data-stu-id="23fe8-170">If multiple users have the same UPN prefix (for example, 'bob') in your Azure AD tenant, their SAMAccountName format may be auto-generated by the service.</span></span> <span data-ttu-id="23fe8-171">在這些情況下，您可以使用 UPN 格式可靠地登入網域。</span><span class="sxs-lookup"><span data-stu-id="23fe8-171">In these cases, the UPN format can be used reliably to log in to the domain.</span></span>
     >
     >
7. <span data-ttu-id="23fe8-172">順利加入網域後，您會看到下列訊息歡迎您加入網域。</span><span class="sxs-lookup"><span data-stu-id="23fe8-172">After domain join is successful, you see the following message welcoming you to the domain.</span></span> <span data-ttu-id="23fe8-173">重新啟動虛擬機器，以便完成加入網域作業。</span><span class="sxs-lookup"><span data-stu-id="23fe8-173">Restart the virtual machine for the domain join operation to complete.</span></span>

    ![歡迎加入網域](./media/active-directory-domain-services-admin-guide/join-domain-done.png)

## <a name="troubleshooting-domain-join"></a><span data-ttu-id="23fe8-175">針對加入網域進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="23fe8-175">Troubleshooting domain join</span></span>
### <a name="connectivity-issues"></a><span data-ttu-id="23fe8-176">連線能力問題</span><span class="sxs-lookup"><span data-stu-id="23fe8-176">Connectivity issues</span></span>
<span data-ttu-id="23fe8-177">如果虛擬機器找不到網域，請參閱下列疑難排解步驟︰</span><span class="sxs-lookup"><span data-stu-id="23fe8-177">If the virtual machine is unable to find the domain, refer to the following troubleshooting steps:</span></span>

* <span data-ttu-id="23fe8-178">確定虛擬機器已連線到您已在其中啟用網域服務的相同虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="23fe8-178">Ensure that the virtual machine is connected to the same virtual network as that you've enabled Domain Services in.</span></span> <span data-ttu-id="23fe8-179">若非如此，虛擬機器便無法連線到網域，因此無法加入網域。</span><span class="sxs-lookup"><span data-stu-id="23fe8-179">If not, the virtual machine is unable to connect to the domain and therefore is unable to join the domain.</span></span>
* <span data-ttu-id="23fe8-180">如果虛擬機器連線到其他虛擬網路，請確定此虛擬網路已連線到您已在其中啟用網域服務的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="23fe8-180">If the virtual machine is connected to another virtual network, ensure that this virtual network is connected to the virtual network in which you've enabled Domain Services.</span></span>
* <span data-ttu-id="23fe8-181">嘗試使用受管理網域的網域名稱來 ping 網域 (例如 'ping contoso100.com')。</span><span class="sxs-lookup"><span data-stu-id="23fe8-181">Try to ping the domain using the domain name of the managed domain (for example, 'ping contoso100.com').</span></span> <span data-ttu-id="23fe8-182">如果您無法這麼做，請嘗試 ping 頁面上所顯示、您已在其中啟用 Azure AD 網域服務之網域的 IP 位址 (例如 'ping 10.0.0.4')。</span><span class="sxs-lookup"><span data-stu-id="23fe8-182">If you're unable to do so, try to ping the IP addresses for the domain displayed on the page where you enabled Azure AD Domain Services (for example, 'ping 10.0.0.4').</span></span> <span data-ttu-id="23fe8-183">如果您能夠 ping 該 IP 位址，但無法 ping 網域，則表示 DNS 的設定可能不正確。</span><span class="sxs-lookup"><span data-stu-id="23fe8-183">If you're able to ping the IP address but not the domain, DNS may be incorrectly configured.</span></span> <span data-ttu-id="23fe8-184">您可能尚未將網域的 IP 位址設定為虛擬網路的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="23fe8-184">You may not have configured the IP addresses of the domain as DNS servers for the virtual network.</span></span>
* <span data-ttu-id="23fe8-185">請嘗試排清虛擬機器上的 DNS 解析程式快取 ('ipconfig /flushdns')。</span><span class="sxs-lookup"><span data-stu-id="23fe8-185">Try flushing the DNS resolver cache on the virtual machine ('ipconfig /flushdns').</span></span>

<span data-ttu-id="23fe8-186">如果您看到對話方塊要求您提供認證以加入網域，則表示您沒有連線問題。</span><span class="sxs-lookup"><span data-stu-id="23fe8-186">If you get to the dialog box that asks for credentials to join the domain, you do not have connectivity issues.</span></span>

### <a name="credentials-related-issues"></a><span data-ttu-id="23fe8-187">與認證相關的問題</span><span class="sxs-lookup"><span data-stu-id="23fe8-187">Credentials-related issues</span></span>
<span data-ttu-id="23fe8-188">如果您的認證有問題因而無法加入網域，請參閱下列步驟。</span><span class="sxs-lookup"><span data-stu-id="23fe8-188">Refer to the following steps if you're having trouble with credentials and are unable to join the domain.</span></span>

* <span data-ttu-id="23fe8-189">嘗試使用 UPN 格式來指定認證。</span><span class="sxs-lookup"><span data-stu-id="23fe8-189">Try using the UPN format to specify credentials.</span></span> <span data-ttu-id="23fe8-190">如果您的租用戶中有多個使用者具有相同的 UPN 前置詞，或您的 UPN 前置詞太長，可能就會自動為您的帳戶產生 SAMAccountName。</span><span class="sxs-lookup"><span data-stu-id="23fe8-190">The SAMAccountName for your account may be auto-generated if there are multiple users with the same UPN prefix in your tenant or if your UPN prefix is overly long.</span></span> <span data-ttu-id="23fe8-191">因此，您帳戶的 SAMAccountName 格式可能會與您在內部部署網域中預期或使用的格式不同。</span><span class="sxs-lookup"><span data-stu-id="23fe8-191">Therefore, the SAMAccountName format for your account may be different from what you expect or use in your on-premises domain.</span></span>
* <span data-ttu-id="23fe8-192">嘗試使用屬於「AAD DC 系統管理員」群組之使用者帳戶的認證，來將電腦加入受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="23fe8-192">Try to use the credentials of a user account that belongs to the 'AAD DC Administrators' group to join machines to the managed domain.</span></span>
* <span data-ttu-id="23fe8-193">確定您已根據《入門指南》中所述的步驟來 [啟用密碼同步處理](active-directory-ds-getting-started-password-sync.md) 。</span><span class="sxs-lookup"><span data-stu-id="23fe8-193">Ensure that you have [enabled password synchronization](active-directory-ds-getting-started-password-sync.md) in accordance with the steps outlined in the Getting Started guide.</span></span>
* <span data-ttu-id="23fe8-194">確定您使用 Azure AD 中所設定的使用者 UPN (例如 'bob@domainservicespreview.onmicrosoft.com') 來登入。</span><span class="sxs-lookup"><span data-stu-id="23fe8-194">Ensure that you use the UPN of the user as configured in Azure AD (for example, 'bob@domainservicespreview.onmicrosoft.com') to sign in.</span></span>
* <span data-ttu-id="23fe8-195">確定您已如《入門指南》中所指定的等候夠久的時間以讓密碼同步處理完成。</span><span class="sxs-lookup"><span data-stu-id="23fe8-195">Ensure that you have waited long enough for password synchronization to complete as specified in the Getting Started guide.</span></span>

## <a name="related-content"></a><span data-ttu-id="23fe8-196">相關內容</span><span class="sxs-lookup"><span data-stu-id="23fe8-196">Related Content</span></span>
* [<span data-ttu-id="23fe8-197">Azure AD Domain Services - 入門指南</span><span class="sxs-lookup"><span data-stu-id="23fe8-197">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="23fe8-198">Administer an Azure AD Domain Services managed domain (管理 Azure AD 網域服務受管理的網域)</span><span class="sxs-lookup"><span data-stu-id="23fe8-198">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
