---
title: "Azure Active Directory Domain Services：開始使用 | Microsoft Docs"
description: "啟用 Azure Active Directory 網域服務使用 hello Azure 入口網站 （預覽）"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 8bde872a13bc9960d1e62c74017ff78a8953a0a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a><span data-ttu-id="2d562-103">啟用 Azure Active Directory 網域服務使用 hello Azure 入口網站 （預覽）</span><span class="sxs-lookup"><span data-stu-id="2d562-103">Enable Azure Active Directory Domain Services using hello Azure portal (Preview)</span></span>


## <a name="task-3-configure-administrative-group"></a><span data-ttu-id="2d562-104">工作 3：設定系統管理群組</span><span class="sxs-lookup"><span data-stu-id="2d562-104">Task 3: configure administrative group</span></span>
<span data-ttu-id="2d562-105">在這項設定工作中，您可以在 Azure AD 目錄中建立系統管理群組。</span><span class="sxs-lookup"><span data-stu-id="2d562-105">In this configuration task, you create an administrative group in your Azure AD directory.</span></span> <span data-ttu-id="2d562-106">這個特殊的系統管理群組稱為 *AAD DC 系統管理員*。</span><span class="sxs-lookup"><span data-stu-id="2d562-106">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="2d562-107">系統管理員權限的電腦已加入網域的 toohello 受管理的網域，會授與此群組的成員。</span><span class="sxs-lookup"><span data-stu-id="2d562-107">Members of this group are granted administrative permissions on machines that are domain-joined toohello managed domain.</span></span> <span data-ttu-id="2d562-108">已加入網域的電腦上，此群組會加入 toohello administrators 群組。</span><span class="sxs-lookup"><span data-stu-id="2d562-108">On domain-joined machines, this group is added toohello administrators group.</span></span> <span data-ttu-id="2d562-109">此外，此群組的成員可以使用遠端桌面 tooconnect 遠端 toodomain 加入機器。</span><span class="sxs-lookup"><span data-stu-id="2d562-109">Additionally, members of this group can use Remote Desktop tooconnect remotely toodomain-joined machines.</span></span>

> [!NOTE]
> <span data-ttu-id="2d562-110">您沒有 hello 您使用 Azure Active Directory 網域服務建立的受管理網域的網域系統管理員或企業系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="2d562-110">You do not have Domain Administrator or Enterprise Administrator permissions on hello managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="2d562-111">上受管理的網域，這些權限所保留的 hello 服務，並不會使用 toousers hello 租用戶中。</span><span class="sxs-lookup"><span data-stu-id="2d562-111">On managed domains, these permissions are reserved by hello service and are not made available toousers within hello tenant.</span></span> <span data-ttu-id="2d562-112">不過，您可以使用特殊 hello 建立系統管理群組中此組態工作 tooperform 某些特殊權限操作。</span><span class="sxs-lookup"><span data-stu-id="2d562-112">However, you can use hello special administrative group created in this configuration task tooperform some privileged operations.</span></span> <span data-ttu-id="2d562-113">這些作業包括加入電腦 toohello 網域屬於 toohello 管理群組已加入網域的機器上，設定群組原則。</span><span class="sxs-lookup"><span data-stu-id="2d562-113">These operations include joining computers toohello domain, belonging toohello administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="2d562-114">hello 精靈會自動建立 Azure AD 目錄中的 hello 系統管理群組。</span><span class="sxs-lookup"><span data-stu-id="2d562-114">hello wizard automatically creates hello administrative group in your Azure AD directory.</span></span> <span data-ttu-id="2d562-115">此群組名為「AAD DC 系統管理員」。</span><span class="sxs-lookup"><span data-stu-id="2d562-115">This group is called 'AAD DC Administrators'.</span></span> <span data-ttu-id="2d562-116">如果您有現有的群組具有此名稱在 Azure AD 目錄中，hello 精靈會選取此群組。</span><span class="sxs-lookup"><span data-stu-id="2d562-116">If you have an existing group with this name in your Azure AD directory, hello wizard selects this group.</span></span> <span data-ttu-id="2d562-117">您可以設定群組成員資格使用 hello **Administrator 群組**精靈頁面。</span><span class="sxs-lookup"><span data-stu-id="2d562-117">You can configure group membership using hello **Administrator group** wizard page.</span></span>

1. <span data-ttu-id="2d562-118">tooconfigure 群組成員資格，按一下 [ **AAD DC 管理員**。</span><span class="sxs-lookup"><span data-stu-id="2d562-118">tooconfigure group membership, click **AAD DC Administrators**.</span></span>

    ![設定群組成員資格](./media/getting-started/domain-services-blade-admingroup.png)

2. <span data-ttu-id="2d562-120">按一下 hello**將成員加入**按鈕 tooadd 使用者從 Azure AD 目錄 toohello 系統管理員群組。</span><span class="sxs-lookup"><span data-stu-id="2d562-120">Click hello **Add members** button tooadd users from your Azure AD directory toohello administrator group.</span></span>

3. <span data-ttu-id="2d562-121">當您完成之後時，按一下 [**確定**上 toohello toomove**摘要**hello 精靈頁面。</span><span class="sxs-lookup"><span data-stu-id="2d562-121">When you are done, click **OK** toomove on toohello **Summary** page of hello wizard.</span></span>

4. <span data-ttu-id="2d562-122">在 [hello**摘要**精靈頁面的 hello] 檢閱 hello 組態設定 hello 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="2d562-122">On hello **Summary** page of hello wizard, review hello configuration settings for hello managed domain.</span></span> <span data-ttu-id="2d562-123">您可以移回 tooany 步驟的 hello 精靈 toomake 變更，如有必要。</span><span class="sxs-lookup"><span data-stu-id="2d562-123">You can go back tooany step of hello wizard toomake changes, if necessary.</span></span> <span data-ttu-id="2d562-124">當您完成之後時，按一下 [**確定**toocreate hello 新增受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="2d562-124">When you are done, click **OK** toocreate hello new managed domain.</span></span>

    ![摘要](./media/getting-started/domain-services-blade-summary.png)

5. <span data-ttu-id="2d562-126">您會看到顯示 Azure AD 網域服務部署的 hello 進度通知。</span><span class="sxs-lookup"><span data-stu-id="2d562-126">You see a notification that shows hello progress of your Azure AD Domain Services deployment.</span></span> <span data-ttu-id="2d562-127">按一下 hello 通知 toosee 詳細 hello 部署的進度。</span><span class="sxs-lookup"><span data-stu-id="2d562-127">Click hello notification toosee detailed progress for hello deployment.</span></span>

    ![通知 - 部署進行中](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a><span data-ttu-id="2d562-129">佈建受管理的網域</span><span class="sxs-lookup"><span data-stu-id="2d562-129">Provision your managed domain</span></span>
<span data-ttu-id="2d562-130">佈建受管理的網域 hello 程序可能佔用 tooan 小時。</span><span class="sxs-lookup"><span data-stu-id="2d562-130">hello process of provisioning your managed domain can take up tooan hour.</span></span>

1. <span data-ttu-id="2d562-131">在進行部署時，您可以搜尋 ' 網域中的服務' hello**搜尋資源**搜尋] 方塊。</span><span class="sxs-lookup"><span data-stu-id="2d562-131">While your deployment is in progress, you can search for 'domain services' in hello **Search resources** search box.</span></span> <span data-ttu-id="2d562-132">選取**Azure AD 網域服務**從 hello 搜尋結果。</span><span class="sxs-lookup"><span data-stu-id="2d562-132">Select **Azure AD Domain Services** from hello search result.</span></span> <span data-ttu-id="2d562-133">hello **Azure AD 網域服務**刀鋒視窗會列出 hello 正在佈建的受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="2d562-133">hello **Azure AD Domain Services** blade lists hello managed domain that is being provisioned.</span></span>

    ![找出正在佈建的受管理的網域](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="2d562-135">按一下 hello 受管理網域 (例如，' contoso100.com') toosee hello 名稱 hello 定義域有關的更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2d562-135">Click hello name of hello managed domain (for example, 'contoso100.com') toosee more details about hello domain.</span></span>

    ![Domain Services - 佈建狀態](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="2d562-137">hello**概觀**索引標籤會顯示目前正在佈建該 hello 網域。</span><span class="sxs-lookup"><span data-stu-id="2d562-137">hello **Overview** tab shows that hello domain is currently being provisioned.</span></span> <span data-ttu-id="2d562-138">完整佈建之前，您無法設定 hello 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="2d562-138">You cannot configure hello managed domain until it is fully provisioned.</span></span> <span data-ttu-id="2d562-139">就會在完全佈建您受管理的網域 toobe tooan 小時。</span><span class="sxs-lookup"><span data-stu-id="2d562-139">It may take up tooan hour for your managed domain toobe fully provisioned.</span></span>

    ![<span data-ttu-id="2d562-140">網域服務的 hello 佈建狀態在 [概觀] 索引標籤</span><span class="sxs-lookup"><span data-stu-id="2d562-140">Domain Services - Overview tab during hello provisioning state</span></span> ](./media/getting-started/domain-services-provisioning-state-details.png)

4. <span data-ttu-id="2d562-141">Hello 受管理的網域完整佈建，hello**概觀**索引標籤會顯示 hello 網域狀態為**執行**。</span><span class="sxs-lookup"><span data-stu-id="2d562-141">When hello managed domain is fully provisioned, hello **Overview** tab shows hello domain status as **Running**.</span></span>

    ![Domain Services - 完全佈建後的 [概觀] 索引標籤](./media/getting-started/domain-services-provisioned.png)

5. <span data-ttu-id="2d562-143">在 [hello**屬性**索引標籤上，您會看到兩個在哪個網域控制站可供 hello 虛擬網路的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2d562-143">On hello **Properties** tab, you see two IP addresses at which domain controllers are available for hello virtual network.</span></span>

    ![Domain Services - 完整佈建後的屬性索引標籤](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a><span data-ttu-id="2d562-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2d562-145">Next step</span></span>
[<span data-ttu-id="2d562-146">工作 4： 更新 hello hello Azure 虛擬網路的 DNS 設定</span><span class="sxs-lookup"><span data-stu-id="2d562-146">Task 4: update hello DNS settings for hello Azure virtual network</span></span>](active-directory-ds-getting-started-dns.md)
