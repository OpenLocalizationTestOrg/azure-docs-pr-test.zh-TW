---
title: "Azure Active Directory Domain Services︰啟用 Azure Active Directory Domain Services | Microsoft Docs"
description: "使用 Azure 傳統入口網站啟用 Azure Active Directory Domain Services"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c659da59-f4b5-4edd-b702-1727a8ccb36f
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: ed72325ca9db99405c6173eb882a92f80cd77f47
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-classic-portal"></a><span data-ttu-id="77cdd-103">使用 Azure 傳統入口網站啟用 Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="77cdd-103">Enable Azure Active Directory Domain Services using the Azure classic portal</span></span>

## <a name="task-3-enable-azure-active-directory-domain-services"></a><span data-ttu-id="77cdd-104">工作 3︰啟用 Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="77cdd-104">Task 3: enable Azure Active Directory Domain Services</span></span>
<span data-ttu-id="77cdd-105">在此工作中，您執行下列步驟來啟用您目錄的 Azure Active Directory Domain Services (Azure AD DS)︰</span><span class="sxs-lookup"><span data-stu-id="77cdd-105">In this task, you enable Azure Active Directory Domain Services (Azure AD DS) for your directory by doing the following steps:</span></span>

1. <span data-ttu-id="77cdd-106">前往 [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="77cdd-106">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="77cdd-107">在左窗格中選取 [Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="77cdd-107">In the left pane, select the **Active Directory** button.</span></span>
3. <span data-ttu-id="77cdd-108">選取您要啟用 Azure AD DS 的 Azure Active Directory (Azure AD) 租用戶 (目錄)。</span><span class="sxs-lookup"><span data-stu-id="77cdd-108">Select the Azure Active Directory (Azure AD) tenant (directory) for which you want to enable Azure AD DS.</span></span>

    ![選取 Azure AD 目錄](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="77cdd-110">在 [預覽目錄] 頁面上，按一下 [設定] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="77cdd-110">On the **preview directory** page, click the **Configure** tab.</span></span>

    ![設定目錄的索引標籤](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="77cdd-112">在 [網域服務] 下，將 [啟用此目錄的網域服務] 選項變更為 [是]。</span><span class="sxs-lookup"><span data-stu-id="77cdd-112">Under **domain services**, change the **Enable domain services for this directory** option to **Yes**.</span></span>  
    <span data-ttu-id="77cdd-113">其他的 Azure Active Directory Domain Services 組態選項會出現在頁面上。</span><span class="sxs-lookup"><span data-stu-id="77cdd-113">Additional Azure Active Directory Domain Services configuration options appear on the page.</span></span>

    ![啟用網域服務](./media/active-directory-domain-services-getting-started/enable-domain-services.png)

   > [!NOTE]
   > <span data-ttu-id="77cdd-115">當您針對租用戶啟用 Azure Active Directory Domain Services 時，Azure AD 會產生並儲存驗證使用者所需的 Kerberos 和 NTLM 認證雜湊。</span><span class="sxs-lookup"><span data-stu-id="77cdd-115">When you enable Azure Active Directory Domain Services for your tenant, Azure AD generates and stores the Kerberos and NTLM credential hashes that are required for authenticating users.</span></span>
   >
   >
6. <span data-ttu-id="77cdd-116">指定 **網域服務的 DNS 網域名稱**。</span><span class="sxs-lookup"><span data-stu-id="77cdd-116">Specify the **DNS domain name of domain services**.</span></span>

   * <span data-ttu-id="77cdd-117">根據預設，將會選取目錄的預設網域名稱 (具有 **.onmicrosoft.com** 尾碼)。</span><span class="sxs-lookup"><span data-stu-id="77cdd-117">The default domain name of the directory (with a **.onmicrosoft.com** suffix) is selected by default.</span></span>

   * <span data-ttu-id="77cdd-118">清單包含所有已針對 Azure AD 目錄設定的網域，包括您在 [網域] 索引標籤中設定的已驗證以及未驗證的網域。</span><span class="sxs-lookup"><span data-stu-id="77cdd-118">The list contains all domains that have been configured for your Azure AD directory, including both verified and unverified domains that you configure on the **Domains** tab.</span></span>

   * <span data-ttu-id="77cdd-119">您也可以輸入自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="77cdd-119">You can also enter a custom domain name.</span></span> <span data-ttu-id="77cdd-120">在此範例中，自訂網域名稱是 contoso100.com。</span><span class="sxs-lookup"><span data-stu-id="77cdd-120">In this example, the custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="77cdd-121">指定網域名稱的前置詞 (例如，contoso100.com 網域名稱中的 contoso100) 必須包含 15 個以內的字元。</span><span class="sxs-lookup"><span data-stu-id="77cdd-121">The prefix of your specified domain name (for example, *contoso100* in the *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="77cdd-122">您無法使用包含超過 15 個字元的前置詞建立 Azure Active Directory Domain Services。</span><span class="sxs-lookup"><span data-stu-id="77cdd-122">You cannot create an Azure Active Directory Domain Services domain with a prefix containing more than 15 characters.</span></span>
     >
     >
7. <span data-ttu-id="77cdd-123">確定虛擬網路中還沒有您為受管理網域選擇的 DNS 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="77cdd-123">Ensure that the DNS domain name you have chosen for the managed domain does not already exist in the virtual network.</span></span> <span data-ttu-id="77cdd-124">具體來說，檢查是否︰</span><span class="sxs-lookup"><span data-stu-id="77cdd-124">Specifically, check to see whether:</span></span>

   * <span data-ttu-id="77cdd-125">您在虛擬網路上已有包含相同 DNS 網域名稱的網域。</span><span class="sxs-lookup"><span data-stu-id="77cdd-125">You already have a domain with the same DNS domain name on the virtual network.</span></span>

   * <span data-ttu-id="77cdd-126">您選取的虛擬網路已透過 VPN 連線到內部部署網路，而您在內部部署網路上有 DNS 網域名稱相同的網域。</span><span class="sxs-lookup"><span data-stu-id="77cdd-126">The virtual network you've selected has a VPN connection with your on-premises network, and you have a domain with the same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="77cdd-127">您在虛擬網路上已有具有該名稱的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="77cdd-127">You have an existing cloud service with that name on the virtual network.</span></span>
8. <span data-ttu-id="77cdd-128">選取您想要 Azure Active Directory Domain Services 可用的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="77cdd-128">Select a virtual network on which you want Azure Active Directory Domain Services to be available.</span></span> <span data-ttu-id="77cdd-129">在 [將網域服務連線至此虛擬網路] 下拉式清單中，選取您建立的虛擬網路和專用子網路。</span><span class="sxs-lookup"><span data-stu-id="77cdd-129">Select the virtual network and dedicated subnet you created in the **Connect domain services to this virtual network** drop-down list.</span></span> <span data-ttu-id="77cdd-130">並請考慮下列項目：</span><span class="sxs-lookup"><span data-stu-id="77cdd-130">Also consider the following:</span></span>

   * <span data-ttu-id="77cdd-131">請確定您指定的虛擬網路屬於 Azure Active Directory Domain Services 所支援的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="77cdd-131">Ensure that the virtual network that you have specified belongs to an Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="77cdd-132">如需可使用 Azure Active Directory Domain Services 的 Azure 區域清單，請參閱[依區域提供的 Azure 服務](https://azure.microsoft.com/regions/#services/)頁面。</span><span class="sxs-lookup"><span data-stu-id="77cdd-132">To ascertain the Azure regions where Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>

   * <span data-ttu-id="77cdd-133">屬於不支援 Azure Active Directory Domain Services 區域的虛擬網路，不會出現在下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="77cdd-133">Virtual networks that belong to a region where Azure Active Directory Domain Services is not supported do not show up in the drop-down list.</span></span>

   * <span data-ttu-id="77cdd-134">在虛擬網路內使用適用於 Azure Active Directory Domain Services 的專用子網路。</span><span class="sxs-lookup"><span data-stu-id="77cdd-134">Use a dedicated subnet within the virtual network for Azure Active Directory Domain Services.</span></span> <span data-ttu-id="77cdd-135">請勿選取閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="77cdd-135">Do *not* select the gateway subnet.</span></span> <span data-ttu-id="77cdd-136">請參閱[網路考量](active-directory-ds-networking.md)。</span><span class="sxs-lookup"><span data-stu-id="77cdd-136">See [networking considerations](active-directory-ds-networking.md).</span></span>

   * <span data-ttu-id="77cdd-137">同樣地，使用 Azure Resource Manager 建立的虛擬網路也不會出現在下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="77cdd-137">Similarly, virtual networks that were created by using Azure Resource Manager do not appear in the drop-down list.</span></span> <span data-ttu-id="77cdd-138">Resource Manager 型虛擬網路目前不為 Azure Active Directory Domain Services 所支援。</span><span class="sxs-lookup"><span data-stu-id="77cdd-138">Resource Manager-based virtual networks are not currently supported by Azure Active Directory Domain Services.</span></span>
9. <span data-ttu-id="77cdd-139">若要啟用 Azure Active Directory Domain Services，請按一下頁面底部工作窗格中的 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="77cdd-139">To enable Azure Active Directory Domain Services, in the task pane at the bottom of the page, click **Save**.</span></span>
    * <span data-ttu-id="77cdd-140">在為您的目錄啟用 Azure Active Directory Domain Services 時，頁面會顯示 [暫止] 狀態。</span><span class="sxs-lookup"><span data-stu-id="77cdd-140">While Azure Active Directory Domain Services is being enabled for your directory, the page displays a status of *Pending*.</span></span>

        ![啟用 [網域服務] 視窗](./media/active-directory-domain-services-getting-started/enable-domain-services-pendingstate.png)

        > [!NOTE]
        > <span data-ttu-id="77cdd-142">Azure Active Directory Domain Services 可針對您的受管理網域提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="77cdd-142">Azure Active Directory Domain Services provides high availability for your managed domain.</span></span> <span data-ttu-id="77cdd-143">啟用 Azure Active Directory Domain Services 後，可在虛擬網路上使用網域服務的 IP 位址會逐一顯示。</span><span class="sxs-lookup"><span data-stu-id="77cdd-143">After you enable Azure Active Directory Domain Services, the IP addresses at which domain services are available on the virtual network are displayed one at a time.</span></span> <span data-ttu-id="77cdd-144">一旦服務針對您的網域啟用高可用性之後，第二個 IP 位址便會立即顯示在第一個之後。</span><span class="sxs-lookup"><span data-stu-id="77cdd-144">The second IP address is displayed shortly after the first, as soon the service enables high availability for your domain.</span></span> <span data-ttu-id="77cdd-145">在針對您的網域設定高可用性並使它成為作用中狀態時，您應該會在 [設定] 索引標籤的 [網域服務] 區段中看到兩個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="77cdd-145">When high availability is configured and active for your domain, you should see two IP addresses in the **domain services** section of the **Configure** tab.</span></span>
        >
        >
    * <span data-ttu-id="77cdd-146">大約 20 至 30 分鐘後，會在 [設定] 頁面的 [IP 位址] 欄位中看見可在您虛擬網路上使用「網域服務」的第一個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="77cdd-146">After about 20 to 30 minutes, the first IP address at which domain services are available on your virtual network in the **IP address** field on the **Configure** page.</span></span>

        ![顯示第一次佈建 IP 的 [網域服務] 視窗](./media/active-directory-domain-services-getting-started/domain-services-enabled-firstdc-available.png)
    * <span data-ttu-id="77cdd-148">若您的網域可支援高可用性，則會在頁面上顯示兩個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="77cdd-148">When high availability is operational for your domain, two IP addresses are displayed on the page.</span></span> <span data-ttu-id="77cdd-149">在所選虛擬網路上，從這兩個 IP 位址可使用您的受管理網域。</span><span class="sxs-lookup"><span data-stu-id="77cdd-149">Your managed domain is available on your selected virtual network at these two IP addresses.</span></span>

10. <span data-ttu-id="77cdd-150">記下這兩個 IP 位址，以更新您虛擬網路的 DNS 設定。</span><span class="sxs-lookup"><span data-stu-id="77cdd-150">Note the two IP addresses so that you can update the DNS settings for your virtual network.</span></span> <span data-ttu-id="77cdd-151">如此會讓虛擬網路上的虛擬機器連線到網域，以進行像是加入網域等作業。</span><span class="sxs-lookup"><span data-stu-id="77cdd-151">Doing so enables virtual machines on the virtual network to connect to the domain for operations such as domain join.</span></span>

    ![顯示兩個已佈建 IP 的 [網域服務] 視窗](./media/active-directory-domain-services-getting-started/domain-services-enabled-bothdcs-available.png)

> [!NOTE]
> <span data-ttu-id="77cdd-153">視 Azure AD 租用戶大小而定 (例如，使用者或群組等的數目)，同步處理至您的受管理網域需要一些時間。</span><span class="sxs-lookup"><span data-stu-id="77cdd-153">Depending on the size of your Azure AD tenant (for example, the number of users or groups), synchronization to your managed domain takes a while.</span></span> <span data-ttu-id="77cdd-154">這個同步處理程序會在背景執行。</span><span class="sxs-lookup"><span data-stu-id="77cdd-154">This synchronization process happens in the background.</span></span> <span data-ttu-id="77cdd-155">對於具有成千上萬個物件的大型租用戶，則可能需要一到兩天的時間，所有使用者、群組成員資格和認證才會完成同步處理。</span><span class="sxs-lookup"><span data-stu-id="77cdd-155">For large tenants with tens of thousands of objects, it might take a day or two for all users, group memberships, and credentials to be synchronized.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="77cdd-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="77cdd-156">Next step</span></span>
[<span data-ttu-id="77cdd-157">工作 4：更新 Azure 虛擬網路的 DNS 設定</span><span class="sxs-lookup"><span data-stu-id="77cdd-157">Task 4: update the DNS settings for the Azure virtual network</span></span>](active-directory-ds-getting-started-update-dns.md)
