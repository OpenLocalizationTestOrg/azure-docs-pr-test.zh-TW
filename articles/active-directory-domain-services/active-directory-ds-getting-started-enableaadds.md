---
title: "Azure Active Directory Domain Services︰啟用 Azure Active Directory Domain Services | Microsoft Docs"
description: "啟用 Azure Active Directory 網域服務使用 hello Azure 傳統入口網站"
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
ms.openlocfilehash: 6263eb1849808a7c85e572e1046bc9039362dd9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a><span data-ttu-id="ca023-103">啟用 Azure Active Directory 網域服務使用 hello Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="ca023-103">Enable Azure Active Directory Domain Services using hello Azure classic portal</span></span>

## <a name="task-3-enable-azure-active-directory-domain-services"></a><span data-ttu-id="ca023-104">工作 3︰啟用 Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="ca023-104">Task 3: enable Azure Active Directory Domain Services</span></span>
<span data-ttu-id="ca023-105">在這個工作中，以啟用 Azure Active Directory 網域服務 (Azure AD DS) 為您的目錄執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ca023-105">In this task, you enable Azure Active Directory Domain Services (Azure AD DS) for your directory by doing hello following steps:</span></span>

1. <span data-ttu-id="ca023-106">移 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="ca023-106">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="ca023-107">Hello 左窗格中，選取 [hello **Active Directory** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ca023-107">In hello left pane, select hello **Active Directory** button.</span></span>
3. <span data-ttu-id="ca023-108">選取您要為其 Azure AD DS tooenable hello Azure Active Directory (Azure AD) 租用 （目錄）。</span><span class="sxs-lookup"><span data-stu-id="ca023-108">Select hello Azure Active Directory (Azure AD) tenant (directory) for which you want tooenable Azure AD DS.</span></span>

    ![選取 Azure AD 目錄](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="ca023-110">在 [hello**預覽目錄**頁面上，按一下 hello**設定**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ca023-110">On hello **preview directory** page, click hello **Configure** tab.</span></span>

    ![設定目錄的索引標籤](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="ca023-112">在下**網域服務**，變更 hello**啟用這個目錄的網域服務**太選項**是**。</span><span class="sxs-lookup"><span data-stu-id="ca023-112">Under **domain services**, change hello **Enable domain services for this directory** option too**Yes**.</span></span>  
    <span data-ttu-id="ca023-113">在 hello 頁面上出現其他的 Azure Active Directory 網域服務組態選項。</span><span class="sxs-lookup"><span data-stu-id="ca023-113">Additional Azure Active Directory Domain Services configuration options appear on hello page.</span></span>

    ![啟用網域服務](./media/active-directory-domain-services-getting-started/enable-domain-services.png)

   > [!NOTE]
   > <span data-ttu-id="ca023-115">當您啟用 Azure Active Directory 網域服務租用戶時，Azure AD 會產生並儲存 hello Kerberos and NTLM 認證雜湊所需的驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="ca023-115">When you enable Azure Active Directory Domain Services for your tenant, Azure AD generates and stores hello Kerberos and NTLM credential hashes that are required for authenticating users.</span></span>
   >
   >
6. <span data-ttu-id="ca023-116">指定 hello**網域服務的 DNS 網域名稱**。</span><span class="sxs-lookup"><span data-stu-id="ca023-116">Specify hello **DNS domain name of domain services**.</span></span>

   * <span data-ttu-id="ca023-117">hello 目錄 hello 預設網域名稱 (與**。 onmicrosoft.com**尾碼) 預設會選取。</span><span class="sxs-lookup"><span data-stu-id="ca023-117">hello default domain name of hello directory (with a **.onmicrosoft.com** suffix) is selected by default.</span></span>

   * <span data-ttu-id="ca023-118">hello 清單包含所有已設定的 Azure AD 目錄的網域，包括驗證和未驗證網域上 hello 設定**網域** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ca023-118">hello list contains all domains that have been configured for your Azure AD directory, including both verified and unverified domains that you configure on hello **Domains** tab.</span></span>

   * <span data-ttu-id="ca023-119">您也可以輸入自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="ca023-119">You can also enter a custom domain name.</span></span> <span data-ttu-id="ca023-120">在此範例中，hello 自訂網域名稱是*contoso100.com*。</span><span class="sxs-lookup"><span data-stu-id="ca023-120">In this example, hello custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="ca023-121">hello 前置詞指定的網域名稱 (例如， *contoso100*在 hello *contoso100.com*網域名稱) 必須包含 15 個字元。</span><span class="sxs-lookup"><span data-stu-id="ca023-121">hello prefix of your specified domain name (for example, *contoso100* in hello *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="ca023-122">您無法使用包含超過 15 個字元的前置詞建立 Azure Active Directory Domain Services。</span><span class="sxs-lookup"><span data-stu-id="ca023-122">You cannot create an Azure Active Directory Domain Services domain with a prefix containing more than 15 characters.</span></span>
     >
     >
7. <span data-ttu-id="ca023-123">請確定您已選擇 hello 受管理的網域不存在 hello 虛擬網路中的 hello DNS 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="ca023-123">Ensure that hello DNS domain name you have chosen for hello managed domain does not already exist in hello virtual network.</span></span> <span data-ttu-id="ca023-124">具體來說，是否檢查 toosee:</span><span class="sxs-lookup"><span data-stu-id="ca023-124">Specifically, check toosee whether:</span></span>

   * <span data-ttu-id="ca023-125">您已經擁有網域以 hello 相同 hello 虛擬網路上的 DNS 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="ca023-125">You already have a domain with hello same DNS domain name on hello virtual network.</span></span>

   * <span data-ttu-id="ca023-126">hello 您選取的虛擬網路有 VPN 連線與內部部署網路，且您必須以 hello 網域相同的 DNS 網域名稱，在內部部署網路上。</span><span class="sxs-lookup"><span data-stu-id="ca023-126">hello virtual network you've selected has a VPN connection with your on-premises network, and you have a domain with hello same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="ca023-127">Hello 虛擬網路上有該名稱與現有的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="ca023-127">You have an existing cloud service with that name on hello virtual network.</span></span>
8. <span data-ttu-id="ca023-128">選取您想要使用的 Azure Active Directory 網域服務 toobe 的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="ca023-128">Select a virtual network on which you want Azure Active Directory Domain Services toobe available.</span></span> <span data-ttu-id="ca023-129">選取 hello 虛擬網路和專用子網路，您可以在 hello**連接網域服務 toothis 虛擬網路**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="ca023-129">Select hello virtual network and dedicated subnet you created in hello **Connect domain services toothis virtual network** drop-down list.</span></span> <span data-ttu-id="ca023-130">也請考慮下列 hello:</span><span class="sxs-lookup"><span data-stu-id="ca023-130">Also consider hello following:</span></span>

   * <span data-ttu-id="ca023-131">請確定您已指定該 hello 虛擬網路屬於 tooan 支援的 Azure Active Directory 網域服務的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="ca023-131">Ensure that hello virtual network that you have specified belongs tooan Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="ca023-132">tooascertain hello Azure Active Directory 網域服務可使用的 Azure 區域，請參閱[依地區的 Azure 服務](https://azure.microsoft.com/regions/#services/)。</span><span class="sxs-lookup"><span data-stu-id="ca023-132">tooascertain hello Azure regions where Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>

   * <span data-ttu-id="ca023-133">虛擬網路屬於 tooa 地區不支援 Azure Active Directory 網域服務，不要顯示 hello 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="ca023-133">Virtual networks that belong tooa region where Azure Active Directory Domain Services is not supported do not show up in hello drop-down list.</span></span>

   * <span data-ttu-id="ca023-134">用於 Azure Active Directory 網域服務中的 hello 虛擬網路內的專用子網路。</span><span class="sxs-lookup"><span data-stu-id="ca023-134">Use a dedicated subnet within hello virtual network for Azure Active Directory Domain Services.</span></span> <span data-ttu-id="ca023-135">請勿*不*選取 hello 閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="ca023-135">Do *not* select hello gateway subnet.</span></span> <span data-ttu-id="ca023-136">請參閱[網路考量](active-directory-ds-networking.md)。</span><span class="sxs-lookup"><span data-stu-id="ca023-136">See [networking considerations](active-directory-ds-networking.md).</span></span>

   * <span data-ttu-id="ca023-137">同樣地，使用 Azure 資源管理員所建立的虛擬網路並不會顯示 hello 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="ca023-137">Similarly, virtual networks that were created by using Azure Resource Manager do not appear in hello drop-down list.</span></span> <span data-ttu-id="ca023-138">Resource Manager 型虛擬網路目前不為 Azure Active Directory Domain Services 所支援。</span><span class="sxs-lookup"><span data-stu-id="ca023-138">Resource Manager-based virtual networks are not currently supported by Azure Active Directory Domain Services.</span></span>
9. <span data-ttu-id="ca023-139">tooenable Azure Active Directory 網域服務，在 hello hello 頁面底部的 hello 工作窗格中按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="ca023-139">tooenable Azure Active Directory Domain Services, in hello task pane at hello bottom of hello page, click **Save**.</span></span>
    * <span data-ttu-id="ca023-140">正在為您的目錄啟用 Azure Active Directory 網域服務，而 hello 頁面會顯示狀態*暫止*。</span><span class="sxs-lookup"><span data-stu-id="ca023-140">While Azure Active Directory Domain Services is being enabled for your directory, hello page displays a status of *Pending*.</span></span>

        ![啟用 [網域服務] 視窗](./media/active-directory-domain-services-getting-started/enable-domain-services-pendingstate.png)

        > [!NOTE]
        > <span data-ttu-id="ca023-142">Azure Active Directory Domain Services 可針對您的受管理網域提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="ca023-142">Azure Active Directory Domain Services provides high availability for your managed domain.</span></span> <span data-ttu-id="ca023-143">啟用 Azure Active Directory 網域服務後，hello hello 虛擬網路上可用服務都在其所在網域的 IP 位址會是一次顯示的一個。</span><span class="sxs-lookup"><span data-stu-id="ca023-143">After you enable Azure Active Directory Domain Services, hello IP addresses at which domain services are available on hello virtual network are displayed one at a time.</span></span> <span data-ttu-id="ca023-144">hello 第二個 IP 位址會顯示 hello 後不久前，很快就 hello 服務可讓您的網域的高可用性。</span><span class="sxs-lookup"><span data-stu-id="ca023-144">hello second IP address is displayed shortly after hello first, as soon hello service enables high availability for your domain.</span></span> <span data-ttu-id="ca023-145">當設定高可用性時，作用中的網域，您應該會看到兩個 IP 位址在 hello**網域服務**區段 hello**設定** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ca023-145">When high availability is configured and active for your domain, you should see two IP addresses in hello **domain services** section of hello **Configure** tab.</span></span>
        >
        >
    * <span data-ttu-id="ca023-146">在約 20 too30 分鐘 hello 在其所在網域服務是在 hello 虛擬網路中可用的第一個 IP 位址後**IP 位址**欄位 hello**設定**頁面。</span><span class="sxs-lookup"><span data-stu-id="ca023-146">After about 20 too30 minutes, hello first IP address at which domain services are available on your virtual network in hello **IP address** field on hello **Configure** page.</span></span>

        ![顯示第一次佈建 IP 的 [網域服務] 視窗](./media/active-directory-domain-services-getting-started/domain-services-enabled-firstdc-available.png)
    * <span data-ttu-id="ca023-148">當高可用性是您的網域內運作時，兩個 IP 位址會顯示在 [hello] 頁面上。</span><span class="sxs-lookup"><span data-stu-id="ca023-148">When high availability is operational for your domain, two IP addresses are displayed on hello page.</span></span> <span data-ttu-id="ca023-149">在所選虛擬網路上，從這兩個 IP 位址可使用您的受管理網域。</span><span class="sxs-lookup"><span data-stu-id="ca023-149">Your managed domain is available on your selected virtual network at these two IP addresses.</span></span>

10. <span data-ttu-id="ca023-150">請注意 hello 兩個 IP 位址，以便您可以更新 hello DNS 設定虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="ca023-150">Note hello two IP addresses so that you can update hello DNS settings for your virtual network.</span></span> <span data-ttu-id="ca023-151">如此可讓 hello 進行運算，例如網域加入虛擬網路 tooconnect toohello 網域上的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ca023-151">Doing so enables virtual machines on hello virtual network tooconnect toohello domain for operations such as domain join.</span></span>

    ![顯示兩個已佈建 IP 的 [網域服務] 視窗](./media/active-directory-domain-services-getting-started/domain-services-enabled-bothdcs-available.png)

> [!NOTE]
> <span data-ttu-id="ca023-153">根據您的 Azure AD 租用戶 （例如，hello 數字的使用者或群組） 的 hello 大小，同步處理 tooyour 受管理的網域會需要一些時間。</span><span class="sxs-lookup"><span data-stu-id="ca023-153">Depending on hello size of your Azure AD tenant (for example, hello number of users or groups), synchronization tooyour managed domain takes a while.</span></span> <span data-ttu-id="ca023-154">此同步處理程序會在 hello 背景。</span><span class="sxs-lookup"><span data-stu-id="ca023-154">This synchronization process happens in hello background.</span></span> <span data-ttu-id="ca023-155">針對大型的租用戶提供數以萬計的物件，可能需要一天，或兩個的所有使用者、 群組成員資格和認證 toobe 同步處理。</span><span class="sxs-lookup"><span data-stu-id="ca023-155">For large tenants with tens of thousands of objects, it might take a day or two for all users, group memberships, and credentials toobe synchronized.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="ca023-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ca023-156">Next step</span></span>
[<span data-ttu-id="ca023-157">工作 4： 更新 hello hello Azure 虛擬網路的 DNS 設定</span><span class="sxs-lookup"><span data-stu-id="ca023-157">Task 4: update hello DNS settings for hello Azure virtual network</span></span>](active-directory-ds-getting-started-update-dns.md)
