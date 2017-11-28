---
title: "Azure Active Directory 網域服務： 加入 Windows Server VM tooa 受管理的網域 |Microsoft 文件"
description: "Windows Server 虛擬機器加入 tooAzure AD 網域服務"
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
ms.openlocfilehash: 1e85833b42bd51f3b3df067d6c5b69253459bec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-windows-server-virtual-machine-tooa-managed-domain"></a><span data-ttu-id="4331c-103">加入 Windows Server 虛擬機器 tooa 受管理的網域</span><span class="sxs-lookup"><span data-stu-id="4331c-103">Join a Windows Server virtual machine tooa managed domain</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4331c-104">Azure 傳統入口網站 - Windows</span><span class="sxs-lookup"><span data-stu-id="4331c-104">Azure classic portal - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
> * [<span data-ttu-id="4331c-105">PowerShell - Windows</span><span class="sxs-lookup"><span data-stu-id="4331c-105">PowerShell - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

<span data-ttu-id="4331c-106">本文章將示範如何 toojoin 虛擬機器執行 Windows Server 2012 R2 tooan Azure AD 網域服務會管理使用 hello Azure 傳統入口網站的網域。</span><span class="sxs-lookup"><span data-stu-id="4331c-106">This article shows you how toojoin a virtual machine running Windows Server 2012 R2 tooan Azure AD Domain Services managed domain, using hello Azure classic portal.</span></span>

## <a name="step-1-create-hello-windows-server-virtual-machine"></a><span data-ttu-id="4331c-107">步驟 1： 建立 hello Windows Server 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="4331c-107">Step 1: Create hello Windows Server virtual machine</span></span>
<span data-ttu-id="4331c-108">遵循 hello 中所述的 hello 指示[建立執行 Windows hello Azure 傳統入口網站中的虛擬機器](../virtual-machines/windows/classic/tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)教學課程。</span><span class="sxs-lookup"><span data-stu-id="4331c-108">Follow hello instructions outlined in hello [Create a virtual machine running Windows in hello Azure classic portal](../virtual-machines/windows/classic/tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) tutorial.</span></span> <span data-ttu-id="4331c-109">這個新建立的虛擬機器的 tooensure 聯結 toohello 務必相同虛擬網路，您已啟用 Azure AD 網域服務。</span><span class="sxs-lookup"><span data-stu-id="4331c-109">It is important tooensure that this newly created virtual machine is joined toohello same virtual network in which you enabled Azure AD Domain Services.</span></span> <span data-ttu-id="4331c-110">hello [快速建立] 選項不會讓您 toojoin hello 虛擬機器 tooa 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4331c-110">hello 'Quick Create' option does not enable you toojoin hello virtual machine tooa virtual network.</span></span> <span data-ttu-id="4331c-111">因此，您需要 toouse hello ' 位於 從組件庫 」 選項 toocreate hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4331c-111">Therefore, you need toouse hello 'From Gallery' option toocreate hello virtual machine.</span></span>

<span data-ttu-id="4331c-112">執行下列步驟 toocreate hello Windows 虛擬機器聯結的 toohello 虛擬網路已啟用 Azure AD 網域服務。</span><span class="sxs-lookup"><span data-stu-id="4331c-112">Perform hello following steps toocreate a Windows virtual machine joined toohello virtual network in which you've enabled Azure AD Domain Services.</span></span>

1. <span data-ttu-id="4331c-113">在 hello Azure 傳統入口網站，hello 在 hello hello 視窗底部的命令列上按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="4331c-113">In hello Azure classic portal, on hello command bar at hello bottom of hello window, click **New**.</span></span>
2. <span data-ttu-id="4331c-114">在 [計算] 底下，依序按一下 [虛擬機器] 和 [從資源庫]。</span><span class="sxs-lookup"><span data-stu-id="4331c-114">Under **Compute**, click **Virtual Machine**, then click **From Gallery**.</span></span>
3. <span data-ttu-id="4331c-115">hello 第一個畫面可讓您**選擇映像**您從虛擬機器的可用的映像的 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="4331c-115">hello first screen lets you **Choose an Image** for your virtual machine from hello list of available images.</span></span> <span data-ttu-id="4331c-116">挑選 hello 適當的映像。</span><span class="sxs-lookup"><span data-stu-id="4331c-116">Pick hello appropriate image.</span></span>

    ![選取映像](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-image.png)
4. <span data-ttu-id="4331c-118">hello 第二個畫面可讓您選取的電腦名稱、 大小，以及管理使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="4331c-118">hello second screen lets you pick a computer name, size, and administrative user name and password.</span></span> <span data-ttu-id="4331c-119">您的應用程式或工作負載，請使用 hello 層和所需大小 toorun。</span><span class="sxs-lookup"><span data-stu-id="4331c-119">Use hello tier and size required toorun your app or workload.</span></span> <span data-ttu-id="4331c-120">您在這裡所挑選的 hello 使用者名稱為 hello 機器的本機系統管理員使用者。</span><span class="sxs-lookup"><span data-stu-id="4331c-120">hello user name you pick here is a local administrator user on hello machine.</span></span> <span data-ttu-id="4331c-121">請勿在此輸入網域使用者帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="4331c-121">Do not enter a domain user account's credentials here.</span></span>

    ![設定虛擬機器](./media/active-directory-domain-services-admin-guide/create-windows-vm-config.png)
5. <span data-ttu-id="4331c-123">hello 第三個畫面可讓您設定網路功能、 儲存體和可用性的資源。</span><span class="sxs-lookup"><span data-stu-id="4331c-123">hello third screen lets you configure resources for networking, storage, and availability.</span></span> <span data-ttu-id="4331c-124">請選取您已啟用 Azure AD 網域服務，從 hello hello 虛擬網路**區域/同質群組/虛擬網路**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="4331c-124">Ensure you select hello virtual network in which you enabled Azure AD Domain Services from hello **Region/Affinity Group/Virtual Network** dropdown.</span></span> <span data-ttu-id="4331c-125">指定**雲端服務 DNS 名稱**為適合 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4331c-125">Specify a **Cloud Service DNS Name** as appropriate for hello virtual machine.</span></span>

    ![選取虛擬機器的虛擬網路](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-vnet.png)

   > [!WARNING]
   > <span data-ttu-id="4331c-127">請確定您加入 hello 虛擬機器 toohello 已啟用 Azure AD 網域服務的相同虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4331c-127">Ensure that you join hello virtual machine toohello same virtual network in which you've enabled Azure AD Domain Services.</span></span> <span data-ttu-id="4331c-128">如此一來，可以看到 hello 網域 hello 虛擬機器，並執行工作，例如將 hello 網域。</span><span class="sxs-lookup"><span data-stu-id="4331c-128">As a result, hello virtual machine can 'see' hello domain and perform tasks such as joining hello domain.</span></span> <span data-ttu-id="4331c-129">如果您選擇 toocreate hello 虛擬機器在不同的虛擬網路中，已啟用 Azure AD 網域服務的虛擬網路的 toohello 虛擬網路的連線。</span><span class="sxs-lookup"><span data-stu-id="4331c-129">If you choose toocreate hello virtual machine in a different virtual network, connect that virtual network toohello virtual network in which you've enabled Azure AD Domain Services.</span></span>
   >
   >
6. <span data-ttu-id="4331c-130">hello 第四個畫面可讓您安裝 hello VM 代理程式，並設定一些 hello 可用擴充功能。</span><span class="sxs-lookup"><span data-stu-id="4331c-130">hello fourth screen lets you install hello VM Agent and configure some of hello available extensions.</span></span>

    ![完成](./media/active-directory-domain-services-admin-guide/create-windows-vm-done.png)
7. <span data-ttu-id="4331c-132">Hello 傳統入口網站建立 hello 虛擬機器之後，會列出下 hello hello 新虛擬機器**虛擬機器**節點。</span><span class="sxs-lookup"><span data-stu-id="4331c-132">After hello virtual machine is created, hello classic portal lists hello new virtual machine under hello **Virtual Machines** node.</span></span> <span data-ttu-id="4331c-133">Hello 虛擬機器和雲端服務會自動啟動，而其狀態會列為**執行**。</span><span class="sxs-lookup"><span data-stu-id="4331c-133">Both hello virtual machine and cloud service are started automatically and their status is listed as **Running**.</span></span>

    ![虛擬機器已啟動並執行](./media/active-directory-domain-services-admin-guide/create-windows-vm-running.png)

## <a name="step-2-connect-toohello-windows-server-virtual-machine-using-hello-local-administrator-account"></a><span data-ttu-id="4331c-135">步驟 2： 連接 toohello 使用 hello 本機系統管理員帳戶的 Windows Server 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="4331c-135">Step 2: Connect toohello Windows Server virtual machine using hello local administrator account</span></span>
<span data-ttu-id="4331c-136">現在，我們連接 toohello 新建立的 Windows Server 虛擬機器，toojoin 它 toohello 網域。</span><span class="sxs-lookup"><span data-stu-id="4331c-136">Now, we connect toohello newly created Windows Server virtual machine, toojoin it toohello domain.</span></span> <span data-ttu-id="4331c-137">使用您指定當建立 hello 的虛擬機器，tooconnect tooit hello 本機系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="4331c-137">Use hello local administrator credentials you specified when creating hello virtual machine, tooconnect tooit.</span></span>

<span data-ttu-id="4331c-138">執行下列步驟 tooconnect toohello 虛擬機器的 hello。</span><span class="sxs-lookup"><span data-stu-id="4331c-138">Perform hello following steps tooconnect toohello virtual machine.</span></span>

1. <span data-ttu-id="4331c-139">瀏覽過**虛擬機器**hello 傳統入口網站中的節點。</span><span class="sxs-lookup"><span data-stu-id="4331c-139">Navigate too**Virtual Machines** node in hello classic portal.</span></span> <span data-ttu-id="4331c-140">選取您在步驟 1 中建立的 hello 虛擬機器，然後按一下**連接**hello 在 hello hello 視窗底部的命令列上。</span><span class="sxs-lookup"><span data-stu-id="4331c-140">Select hello virtual machine you created in Step 1 and click **Connect** on hello command bar at hello bottom of hello window.</span></span>

    ![TooWindows 虛擬機器連線](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. <span data-ttu-id="4331c-142">hello 傳統入口網站會提示您 tooopen 或儲存 '.rdp' 副檔名的檔案，這是使用的 tooconnect toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4331c-142">hello classic portal prompts you tooopen or save a file with a '.rdp' extension, which is used tooconnect toohello virtual machine.</span></span> <span data-ttu-id="4331c-143">下載完成時，請按一下 tooopen hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="4331c-143">Click tooopen hello file when it has finished downloading.</span></span>
3. <span data-ttu-id="4331c-144">Hello 登入提示字元之下，輸入您**本機系統管理員認證**，您建立 hello 虛擬機器時所指定。</span><span class="sxs-lookup"><span data-stu-id="4331c-144">At hello login prompt, enter your **local administrator credentials**, which you specified while creating hello virtual machine.</span></span> <span data-ttu-id="4331c-145">例如，我們在此範例中使用 'localhost\mahesh'。</span><span class="sxs-lookup"><span data-stu-id="4331c-145">For example, we've used 'localhost\mahesh' in this example.</span></span>

<span data-ttu-id="4331c-146">此時，您應該登入 toohello 新建立的 Windows 虛擬機器使用本機系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="4331c-146">At this point, you should be logged in toohello newly created Windows virtual machine using local Administrator credentials.</span></span> <span data-ttu-id="4331c-147">hello 下一個步驟是 toojoin hello 虛擬機器 toohello 網域。</span><span class="sxs-lookup"><span data-stu-id="4331c-147">hello next step is toojoin hello virtual machine toohello domain.</span></span>

## <a name="step-3-join-hello-windows-server-virtual-machine-toohello-aad-ds-managed-domain"></a><span data-ttu-id="4331c-148">步驟 3： 加入 hello Windows Server 虛擬機器 toohello AAD DS 受管理的網域</span><span class="sxs-lookup"><span data-stu-id="4331c-148">Step 3: Join hello Windows Server virtual machine toohello AAD-DS managed domain</span></span>
<span data-ttu-id="4331c-149">執行下列步驟 toojoin hello Windows Server 虛擬機器 toohello AAD DS 受管理的網域中的 hello。</span><span class="sxs-lookup"><span data-stu-id="4331c-149">Perform hello following steps toojoin hello Windows Server virtual machine toohello AAD-DS managed domain.</span></span>

1. <span data-ttu-id="4331c-150">連接 toohello Windows Server，步驟 2 中所示。</span><span class="sxs-lookup"><span data-stu-id="4331c-150">Connect toohello Windows Server as shown in Step 2.</span></span> <span data-ttu-id="4331c-151">從 hello 開始 畫面開啟**伺服器管理員**。</span><span class="sxs-lookup"><span data-stu-id="4331c-151">From hello Start screen, open **Server Manager**.</span></span>
2. <span data-ttu-id="4331c-152">按一下**本機伺服器**hello hello 伺服器管理員 視窗的左窗格中。</span><span class="sxs-lookup"><span data-stu-id="4331c-152">Click **Local Server** in hello left pane of hello Server Manager window.</span></span>

    ![啟動虛擬機器上的伺服器管理員](./media/active-directory-domain-services-admin-guide/join-domain-server-manager.png)
3. <span data-ttu-id="4331c-154">按一下**WORKGROUP**下 hello**屬性**> 一節。</span><span class="sxs-lookup"><span data-stu-id="4331c-154">Click **WORKGROUP** under hello **PROPERTIES** section.</span></span> <span data-ttu-id="4331c-155">在 hello**系統屬性**屬性頁上，按一下 **變更**toojoin hello 網域。</span><span class="sxs-lookup"><span data-stu-id="4331c-155">In hello **System Properties** property page, click **Change** toojoin hello domain.</span></span>

    ![[系統屬性] 頁面](./media/active-directory-domain-services-admin-guide/join-domain-system-properties.png)
4. <span data-ttu-id="4331c-157">指定 hello 網域名稱，您的 Azure AD 網域服務受管理網域中 hello**網域**文字方塊中，按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="4331c-157">Specify hello domain name of your Azure AD Domain Services managed domain in hello **Domain** textbox and click **OK**.</span></span>

    ![指定 hello 網域 toobe 聯結](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-domain.png)
5. <span data-ttu-id="4331c-159">您會提示的 tooenter 認證 toojoin hello 網域。</span><span class="sxs-lookup"><span data-stu-id="4331c-159">You are prompted tooenter your credentials toojoin hello domain.</span></span> <span data-ttu-id="4331c-160">請確定您**指定使用者隸屬 toohello AAD DC 系統管理員的 hello 認證**群組。</span><span class="sxs-lookup"><span data-stu-id="4331c-160">Ensure that you **specify hello credentials for a user belonging toohello AAD DC Administrators** group.</span></span> <span data-ttu-id="4331c-161">只有此群組的成員有權限 toojoin 機器 toohello 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="4331c-161">Only members of this group have privileges toojoin machines toohello managed domain.</span></span>

    ![指定用於加入網域的認證](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-credentials.png)
6. <span data-ttu-id="4331c-163">您可以使用其中一種 hello 下列方式來指定認證：</span><span class="sxs-lookup"><span data-stu-id="4331c-163">You can specify credentials in either of hello following ways:</span></span>

   * <span data-ttu-id="4331c-164">UPN 格式： 指定 hello hello 使用者帳戶的 UPN 尾碼，Azure AD 中的設定。</span><span class="sxs-lookup"><span data-stu-id="4331c-164">UPN format: Specify hello UPN suffix for hello user account, as configured in Azure AD.</span></span> <span data-ttu-id="4331c-165">在此範例中，hello 使用者 'bob' hello UPN 尾碼是 'bob@domainservicespreview.onmicrosoft.com'。</span><span class="sxs-lookup"><span data-stu-id="4331c-165">In this example, hello UPN suffix of hello user 'bob' is 'bob@domainservicespreview.onmicrosoft.com'.</span></span>
   * <span data-ttu-id="4331c-166">SAMAccountName 格式： 您可以在 hello SAMAccountName 格式指定 hello 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="4331c-166">SAMAccountName format: You can specify hello account name in hello SAMAccountName format.</span></span> <span data-ttu-id="4331c-167">在此範例中，hello 使用者 'bob' 需要 tooenter 'CONTOSO100\bob'。</span><span class="sxs-lookup"><span data-stu-id="4331c-167">In this example, hello user 'bob' would need tooenter 'CONTOSO100\bob'.</span></span>

     > [!NOTE]
     > <span data-ttu-id="4331c-168">**我們建議使用 hello UPN 格式 toospecify 認證。**</span><span class="sxs-lookup"><span data-stu-id="4331c-168">**We recommend using hello UPN format toospecify credentials.**</span></span> <span data-ttu-id="4331c-169">如果使用者的 UPN 前置詞太長 （例如，'joereallylongnameuser'） 自動產生可能 hello SAMAccountName。</span><span class="sxs-lookup"><span data-stu-id="4331c-169">hello SAMAccountName may be auto-generated if a user's UPN prefix is overly long (for example, 'joereallylongnameuser').</span></span> <span data-ttu-id="4331c-170">如果多個使用者擁有的 hello Azure AD 租用戶中，其 SAMAccountName 格式相同的 UPN 首碼 (例如，' bob') 可能會由自動產生 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="4331c-170">If multiple users have hello same UPN prefix (for example, 'bob') in your Azure AD tenant, their SAMAccountName format may be auto-generated by hello service.</span></span> <span data-ttu-id="4331c-171">在這些情況下，hello UPN 格式可以可靠地使用 toolog toohello 網域中的。</span><span class="sxs-lookup"><span data-stu-id="4331c-171">In these cases, hello UPN format can be used reliably toolog in toohello domain.</span></span>
     >
     >
7. <span data-ttu-id="4331c-172">順利加入網域後，您會看到下列訊息出現歡迎您 toohello 網域 hello。</span><span class="sxs-lookup"><span data-stu-id="4331c-172">After domain join is successful, you see hello following message welcoming you toohello domain.</span></span> <span data-ttu-id="4331c-173">重新啟動 hello 網域聯結作業 toocomplete hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4331c-173">Restart hello virtual machine for hello domain join operation toocomplete.</span></span>

    ![歡迎使用 toohello 網域](./media/active-directory-domain-services-admin-guide/join-domain-done.png)

## <a name="troubleshooting-domain-join"></a><span data-ttu-id="4331c-175">針對加入網域進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="4331c-175">Troubleshooting domain join</span></span>
### <a name="connectivity-issues"></a><span data-ttu-id="4331c-176">連線能力問題</span><span class="sxs-lookup"><span data-stu-id="4331c-176">Connectivity issues</span></span>
<span data-ttu-id="4331c-177">如果無法 toofind hello 網域 hello 虛擬機器，請參閱 toohello 下列疑難排解步驟：</span><span class="sxs-lookup"><span data-stu-id="4331c-177">If hello virtual machine is unable toofind hello domain, refer toohello following troubleshooting steps:</span></span>

* <span data-ttu-id="4331c-178">請確認 hello 虛擬機器連線的 toohello 相同虛擬網路，您已啟用網域服務中。</span><span class="sxs-lookup"><span data-stu-id="4331c-178">Ensure that hello virtual machine is connected toohello same virtual network as that you've enabled Domain Services in.</span></span> <span data-ttu-id="4331c-179">如果沒有，hello 虛擬機器無法 tooconnect toohello 網域網域，因此無法 toojoin hello 網域。</span><span class="sxs-lookup"><span data-stu-id="4331c-179">If not, hello virtual machine is unable tooconnect toohello domain and therefore is unable toojoin hello domain.</span></span>
* <span data-ttu-id="4331c-180">如果 hello 虛擬機器連線的 tooanother 虛擬網路，請確定此虛擬網路是連線的 toohello 虛擬網路已啟用網域服務。</span><span class="sxs-lookup"><span data-stu-id="4331c-180">If hello virtual machine is connected tooanother virtual network, ensure that this virtual network is connected toohello virtual network in which you've enabled Domain Services.</span></span>
* <span data-ttu-id="4331c-181">嘗試使用 tooping hello 網域使用 hello 的 hello 受管理的網域 (例如，' ping contoso100.com') 的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="4331c-181">Try tooping hello domain using hello domain name of hello managed domain (for example, 'ping contoso100.com').</span></span> <span data-ttu-id="4331c-182">如果您因此無法 toodo，再試一次 tooping hello IP 位址的 hello 網域 hello 頁面上顯示您已啟用 Azure AD 網域服務 (例如，' ping 10.0.0.4')。</span><span class="sxs-lookup"><span data-stu-id="4331c-182">If you're unable toodo so, try tooping hello IP addresses for hello domain displayed on hello page where you enabled Azure AD Domain Services (for example, 'ping 10.0.0.4').</span></span> <span data-ttu-id="4331c-183">如果您不能 tooping hello IP 位址，但未 hello 網域時，DNS 可能設定不正確。</span><span class="sxs-lookup"><span data-stu-id="4331c-183">If you're able tooping hello IP address but not hello domain, DNS may be incorrectly configured.</span></span> <span data-ttu-id="4331c-184">您可能不為 hello 虛擬網路的 DNS 伺服器設定 hello 網域 hello IP 的位址。</span><span class="sxs-lookup"><span data-stu-id="4331c-184">You may not have configured hello IP addresses of hello domain as DNS servers for hello virtual network.</span></span>
* <span data-ttu-id="4331c-185">嘗試排清 hello hello 虛擬機器 ('ipconfig /flushdns') 上的 DNS 解析程式快取。</span><span class="sxs-lookup"><span data-stu-id="4331c-185">Try flushing hello DNS resolver cache on hello virtual machine ('ipconfig /flushdns').</span></span>

<span data-ttu-id="4331c-186">如果您收到 toohello 對話方塊，詢問認證 toojoin hello 網域，表示您沒有連線問題。</span><span class="sxs-lookup"><span data-stu-id="4331c-186">If you get toohello dialog box that asks for credentials toojoin hello domain, you do not have connectivity issues.</span></span>

### <a name="credentials-related-issues"></a><span data-ttu-id="4331c-187">與認證相關的問題</span><span class="sxs-lookup"><span data-stu-id="4331c-187">Credentials-related issues</span></span>
<span data-ttu-id="4331c-188">請參閱下列步驟，如果您無法使用認證，而且無法 toojoin hello 網域 toohello。</span><span class="sxs-lookup"><span data-stu-id="4331c-188">Refer toohello following steps if you're having trouble with credentials and are unable toojoin hello domain.</span></span>

* <span data-ttu-id="4331c-189">請嘗試使用 hello UPN 格式 toospecify 認證。</span><span class="sxs-lookup"><span data-stu-id="4331c-189">Try using hello UPN format toospecify credentials.</span></span> <span data-ttu-id="4331c-190">hello SAMAccountName 為您的帳戶可能是自動產生如果有多個使用者以相同的 UPN 租用戶中的前置詞，或若您的 UPN 前置過度長的 hello。</span><span class="sxs-lookup"><span data-stu-id="4331c-190">hello SAMAccountName for your account may be auto-generated if there are multiple users with hello same UPN prefix in your tenant or if your UPN prefix is overly long.</span></span> <span data-ttu-id="4331c-191">因此，您可能會與所預期或使用您在內部部署網域中不同 hello SAMAccountName 格式，為您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="4331c-191">Therefore, hello SAMAccountName format for your account may be different from what you expect or use in your on-premises domain.</span></span>
* <span data-ttu-id="4331c-192">Toouse hello 所屬 toohello ' AAD DC Administrators' 群組 toojoin 機器 toohello 受管理的網域使用者帳戶的認證再試一次。</span><span class="sxs-lookup"><span data-stu-id="4331c-192">Try toouse hello credentials of a user account that belongs toohello 'AAD DC Administrators' group toojoin machines toohello managed domain.</span></span>
* <span data-ttu-id="4331c-193">請確定您有[啟用密碼同步處理](active-directory-ds-getting-started-password-sync.md)根據 hello hello 快速入門指南中所述的步驟。</span><span class="sxs-lookup"><span data-stu-id="4331c-193">Ensure that you have [enabled password synchronization](active-directory-ds-getting-started-password-sync.md) in accordance with hello steps outlined in hello Getting Started guide.</span></span>
* <span data-ttu-id="4331c-194">請務必使用 hello hello 使用者的 UPN，Azure AD 中的設定 (例如，'bob@domainservicespreview.onmicrosoft.com') 中的 toosign。</span><span class="sxs-lookup"><span data-stu-id="4331c-194">Ensure that you use hello UPN of hello user as configured in Azure AD (for example, 'bob@domainservicespreview.onmicrosoft.com') toosign in.</span></span>
* <span data-ttu-id="4331c-195">請確定您已經等候夠長的密碼同步處理 toocomplete hello 快速入門指南中所指定。</span><span class="sxs-lookup"><span data-stu-id="4331c-195">Ensure that you have waited long enough for password synchronization toocomplete as specified in hello Getting Started guide.</span></span>

## <a name="related-content"></a><span data-ttu-id="4331c-196">相關內容</span><span class="sxs-lookup"><span data-stu-id="4331c-196">Related Content</span></span>
* [<span data-ttu-id="4331c-197">Azure AD Domain Services - 入門指南</span><span class="sxs-lookup"><span data-stu-id="4331c-197">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="4331c-198">Administer an Azure AD Domain Services managed domain (管理 Azure AD 網域服務受管理的網域)</span><span class="sxs-lookup"><span data-stu-id="4331c-198">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
