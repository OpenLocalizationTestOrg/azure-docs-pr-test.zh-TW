---
title: "Azure Active Directory Domain Services：開始使用 | Microsoft Docs"
description: "使用 Azure 入口網站 (預覽) 啟用 Azure Active Directory Domain Services"
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
ms.openlocfilehash: f87bcf33d3b1eb21c7d84814e4c4086f664e293d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal-preview"></a><span data-ttu-id="34d40-103">使用 Azure 入口網站 (預覽) 啟用 Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="34d40-103">Enable Azure Active Directory Domain Services using the Azure portal (Preview)</span></span>


## <a name="task-3-configure-administrative-group"></a><span data-ttu-id="34d40-104">工作 3：設定系統管理群組</span><span class="sxs-lookup"><span data-stu-id="34d40-104">Task 3: configure administrative group</span></span>
<span data-ttu-id="34d40-105">在這項設定工作中，您可以在 Azure AD 目錄中建立系統管理群組。</span><span class="sxs-lookup"><span data-stu-id="34d40-105">In this configuration task, you create an administrative group in your Azure AD directory.</span></span> <span data-ttu-id="34d40-106">這個特殊的系統管理群組稱為 *AAD DC 系統管理員*。</span><span class="sxs-lookup"><span data-stu-id="34d40-106">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="34d40-107">此群組的成員會獲得電腦的系統管理權限，而這類電腦已加入受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="34d40-107">Members of this group are granted administrative permissions on machines that are domain-joined to the managed domain.</span></span> <span data-ttu-id="34d40-108">在加入網域的電腦上，這個群組會新增到系統管理員群組。</span><span class="sxs-lookup"><span data-stu-id="34d40-108">On domain-joined machines, this group is added to the administrators group.</span></span> <span data-ttu-id="34d40-109">此外，此群組的成員可以使用遠端桌面，從遠端連接到已加入網域的電腦。</span><span class="sxs-lookup"><span data-stu-id="34d40-109">Additionally, members of this group can use Remote Desktop to connect remotely to domain-joined machines.</span></span>

> [!NOTE]
> <span data-ttu-id="34d40-110">您在使用 Azure Active Directory Domain Services 所建立的受管理網域內，沒有「網域系統管理員」或「企業系統管理員」權限。</span><span class="sxs-lookup"><span data-stu-id="34d40-110">You do not have Domain Administrator or Enterprise Administrator permissions on the managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="34d40-111">在受管理的網域上，服務會保留這些權限，並不會提供給租用戶中的使用者使用。</span><span class="sxs-lookup"><span data-stu-id="34d40-111">On managed domains, these permissions are reserved by the service and are not made available to users within the tenant.</span></span> <span data-ttu-id="34d40-112">不過，您可以使用在此組態工作中建立的特殊系統管理群組，執行某些特殊權限的作業。</span><span class="sxs-lookup"><span data-stu-id="34d40-112">However, you can use the special administrative group created in this configuration task to perform some privileged operations.</span></span> <span data-ttu-id="34d40-113">這些作業包括將電腦加入網域、隸屬於已加入網域之電腦上的管理群組，以及設定群組原則。</span><span class="sxs-lookup"><span data-stu-id="34d40-113">These operations include joining computers to the domain, belonging to the administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="34d40-114">精靈會在 Azure AD 目錄中自動建立系統管理群組。</span><span class="sxs-lookup"><span data-stu-id="34d40-114">The wizard automatically creates the administrative group in your Azure AD directory.</span></span> <span data-ttu-id="34d40-115">此群組名為「AAD DC 系統管理員」。</span><span class="sxs-lookup"><span data-stu-id="34d40-115">This group is called 'AAD DC Administrators'.</span></span> <span data-ttu-id="34d40-116">如果在 Azure AD 目錄中已有此名稱的現有群組存在，精靈會選取此群組。</span><span class="sxs-lookup"><span data-stu-id="34d40-116">If you have an existing group with this name in your Azure AD directory, the wizard selects this group.</span></span> <span data-ttu-id="34d40-117">您可以使用 [Administrator 群組] 精靈分頁設定群組成員資格。</span><span class="sxs-lookup"><span data-stu-id="34d40-117">You can configure group membership using the **Administrator group** wizard page.</span></span>

1. <span data-ttu-id="34d40-118">若要設定群組成員資格，請按一下 [AAD DC 系統管理員]。</span><span class="sxs-lookup"><span data-stu-id="34d40-118">To configure group membership, click **AAD DC Administrators**.</span></span>

    ![設定群組成員資格](./media/getting-started/domain-services-blade-admingroup.png)

2. <span data-ttu-id="34d40-120">按一下 [新增成員] 按鈕，將使用者從 Azure AD 目錄新增至系統管理員群組。</span><span class="sxs-lookup"><span data-stu-id="34d40-120">Click the **Add members** button to add users from your Azure AD directory to the administrator group.</span></span>

3. <span data-ttu-id="34d40-121">完成時，按一下 [確定] 以繼續前往精靈的 [摘要] 分頁。</span><span class="sxs-lookup"><span data-stu-id="34d40-121">When you are done, click **OK** to move on to the **Summary** page of the wizard.</span></span>

4. <span data-ttu-id="34d40-122">在精靈的 [摘要] 分頁中，檢閱受管理的網域的組態設定。</span><span class="sxs-lookup"><span data-stu-id="34d40-122">On the **Summary** page of the wizard, review the configuration settings for the managed domain.</span></span> <span data-ttu-id="34d40-123">您可以視需要返回精靈的任何步驟以進行變更。</span><span class="sxs-lookup"><span data-stu-id="34d40-123">You can go back to any step of the wizard to make changes, if necessary.</span></span> <span data-ttu-id="34d40-124">完成時，按一下 [確定] 來建立新的受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="34d40-124">When you are done, click **OK** to create the new managed domain.</span></span>

    ![摘要](./media/getting-started/domain-services-blade-summary.png)

5. <span data-ttu-id="34d40-126">您會看到通知，顯示 Azure AD Domain Services 部署的進度。</span><span class="sxs-lookup"><span data-stu-id="34d40-126">You see a notification that shows the progress of your Azure AD Domain Services deployment.</span></span> <span data-ttu-id="34d40-127">按一下通知以查看部署的詳細進度。</span><span class="sxs-lookup"><span data-stu-id="34d40-127">Click the notification to see detailed progress for the deployment.</span></span>

    ![通知 - 部署進行中](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a><span data-ttu-id="34d40-129">佈建受管理的網域</span><span class="sxs-lookup"><span data-stu-id="34d40-129">Provision your managed domain</span></span>
<span data-ttu-id="34d40-130">佈建受管理的網域的程序可能需要一小時的時間。</span><span class="sxs-lookup"><span data-stu-id="34d40-130">The process of provisioning your managed domain can take up to an hour.</span></span>

1. <span data-ttu-id="34d40-131">部署進行時，您可以在 [搜尋資源] 搜尋方塊中搜尋「網域服務」。</span><span class="sxs-lookup"><span data-stu-id="34d40-131">While your deployment is in progress, you can search for 'domain services' in the **Search resources** search box.</span></span> <span data-ttu-id="34d40-132">從搜尋結果選取 [Azure AD Domain Services]。</span><span class="sxs-lookup"><span data-stu-id="34d40-132">Select **Azure AD Domain Services** from the search result.</span></span> <span data-ttu-id="34d40-133">[Azure AD Domain Services] 刀鋒視窗會列出正在佈建的受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="34d40-133">The **Azure AD Domain Services** blade lists the managed domain that is being provisioned.</span></span>

    ![找出正在佈建的受管理的網域](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="34d40-135">按一下受管理的網域名稱 (例如，'contoso100.com')，以查看網域的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="34d40-135">Click the name of the managed domain (for example, 'contoso100.com') to see more details about the domain.</span></span>

    ![Domain Services - 佈建狀態](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="34d40-137">[概觀] 索引標籤會顯示目前佈建的網域。</span><span class="sxs-lookup"><span data-stu-id="34d40-137">The **Overview** tab shows that the domain is currently being provisioned.</span></span> <span data-ttu-id="34d40-138">完整佈建之前，您無法設定受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="34d40-138">You cannot configure the managed domain until it is fully provisioned.</span></span> <span data-ttu-id="34d40-139">完整佈建受管理的網域可能需要一小時的時間。</span><span class="sxs-lookup"><span data-stu-id="34d40-139">It may take up to an hour for your managed domain to be fully provisioned.</span></span>

    ![<span data-ttu-id="34d40-140">Domain Services - 佈建狀態期間的概觀索引標籤</span><span class="sxs-lookup"><span data-stu-id="34d40-140">Domain Services - Overview tab during the provisioning state</span></span> ](./media/getting-started/domain-services-provisioning-state-details.png)

4. <span data-ttu-id="34d40-141">當受管理的網域完整佈建時，[概觀] 索引標籤會將網域狀態顯示為 [執行中]。</span><span class="sxs-lookup"><span data-stu-id="34d40-141">When the managed domain is fully provisioned, the **Overview** tab shows the domain status as **Running**.</span></span>

    ![Domain Services - 完全佈建後的 [概觀] 索引標籤](./media/getting-started/domain-services-provisioned.png)

5. <span data-ttu-id="34d40-143">在 [屬性] 索引標籤上，您會看到網域控制站可供虛擬網路使用的兩個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="34d40-143">On the **Properties** tab, you see two IP addresses at which domain controllers are available for the virtual network.</span></span>

    ![Domain Services - 完整佈建後的屬性索引標籤](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a><span data-ttu-id="34d40-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="34d40-145">Next step</span></span>
[<span data-ttu-id="34d40-146">工作 4：更新 Azure 虛擬網路的 DNS 設定</span><span class="sxs-lookup"><span data-stu-id="34d40-146">Task 4: update the DNS settings for the Azure virtual network</span></span>](active-directory-ds-getting-started-dns.md)
