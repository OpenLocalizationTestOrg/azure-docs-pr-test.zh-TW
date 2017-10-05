---
title: "Azure Active Directory Domain Services：建立 Azure AD DC 系統管理員群組 | Microsoft Docs"
description: "使用 Azure 傳統入口網站啟用 Azure Active Directory Domain Services"
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
ms.date: 07/13/2017
ms.author: maheshu
ms.openlocfilehash: 5ed0125e05928cf0f6d9941e099b433ecb46e6e2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-classic-portal"></a><span data-ttu-id="d7095-103">使用 Azure 傳統入口網站啟用 Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="d7095-103">Enable Azure Active Directory Domain Services using the Azure classic portal</span></span>
<span data-ttu-id="d7095-104">本文將說明並逐步引導您進行所需的組態工作，以讓您啟用 Azure Active Directory (Azure AD) 租用戶的 Azure Active Directory Domain Services (Azure AD DS)。</span><span class="sxs-lookup"><span data-stu-id="d7095-104">This article describes and walks through the configuration tasks that are required for you to enable Azure Active Directory Domain Services (Azure AD DS) for your Azure Active Directory (Azure AD) tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="d7095-105">[**改為嘗試新的 (預覽) Azure 入口網站體驗**](active-directory-ds-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="d7095-105">[**Try the new (preview) Azure portal experience instead**](active-directory-ds-getting-started.md).</span></span> 
>

## <a name="task-1-create-the-azure-ad-dc-administrators-group"></a><span data-ttu-id="d7095-106">工作 1：建立 Azure AD DC 系統管理員群組</span><span class="sxs-lookup"><span data-stu-id="d7095-106">Task 1: create the Azure AD DC administrators group</span></span>
<span data-ttu-id="d7095-107">第一個工作是在您的 Azure AD 租用戶中建立系統管理群組。</span><span class="sxs-lookup"><span data-stu-id="d7095-107">The first task is to create an administrative group in your Azure AD tenant.</span></span> <span data-ttu-id="d7095-108">這個特殊的系統管理群組稱為 *AAD DC 系統管理員*。</span><span class="sxs-lookup"><span data-stu-id="d7095-108">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="d7095-109">此群組的成員會獲得電腦的系統管理權限，而這類電腦已加入受 Azure Active Directory Domain Services 管理的網域。</span><span class="sxs-lookup"><span data-stu-id="d7095-109">Members of this group are granted administrative permissions on machines that are domain-joined to the Azure Active Directory Domain Services-managed domain.</span></span> <span data-ttu-id="d7095-110">在加入網域的電腦上，這個群組會新增到系統管理員群組。</span><span class="sxs-lookup"><span data-stu-id="d7095-110">On domain-joined machines, this group is added to the administrators group.</span></span> <span data-ttu-id="d7095-111">此外，此群組的成員可以使用遠端桌面，從遠端連接到已加入網域的電腦。</span><span class="sxs-lookup"><span data-stu-id="d7095-111">Additionally, members of this group can use Remote Desktop to connect remotely to domain-joined machines.</span></span>  

> [!NOTE]
> <span data-ttu-id="d7095-112">您在使用 Azure Active Directory Domain Services 所建立的受管理網域內，沒有「網域系統管理員」或「企業系統管理員」權限。</span><span class="sxs-lookup"><span data-stu-id="d7095-112">You do not have Domain Administrator or Enterprise Administrator permissions on the managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="d7095-113">在受管理的網域上，服務會保留這些權限，並不會提供給租用戶中的使用者使用。</span><span class="sxs-lookup"><span data-stu-id="d7095-113">On managed domains, these permissions are reserved by the service and are not made available to users within the tenant.</span></span> <span data-ttu-id="d7095-114">不過，您可以使用在此組態工作中建立的特殊系統管理群組，執行某些特殊權限的作業。</span><span class="sxs-lookup"><span data-stu-id="d7095-114">However, you can use the special administrative group created in this configuration task to perform some privileged operations.</span></span> <span data-ttu-id="d7095-115">這些作業包括將電腦加入網域、隸屬於已加入網域之電腦上的管理群組，以及設定群組原則。</span><span class="sxs-lookup"><span data-stu-id="d7095-115">These operations include joining computers to the domain, belonging to the administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="d7095-116">在這個組態工作中，您會建立系統管理群組，並將目錄中的一或多位使用者加入該群組。</span><span class="sxs-lookup"><span data-stu-id="d7095-116">In this configuration task, you create the administrative group and add one or more users in your directory to the group.</span></span> <span data-ttu-id="d7095-117">若要為 Azure Active Directory Domain Services 建立系統管理群組，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d7095-117">To create the administrative group for Azure Active Directory Domain Services, do the following:</span></span>

1. <span data-ttu-id="d7095-118">前往 [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="d7095-118">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="d7095-119">在左窗格中選取 [Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d7095-119">In the left pane, select the **Active Directory** button.</span></span>
3. <span data-ttu-id="d7095-120">選取您要啟用 Azure Active Directory Domain Services 的 Azure AD 租用戶 (目錄)。</span><span class="sxs-lookup"><span data-stu-id="d7095-120">Select the Azure AD tenant (directory) for which you want to enable Azure Active Directory Domain Services.</span></span> <span data-ttu-id="d7095-121">您只能針對每個 Azure AD 目錄建立一個網域。</span><span class="sxs-lookup"><span data-stu-id="d7095-121">You can create only one domain for each Azure AD directory.</span></span>

    ![選取 Azure AD 目錄](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="d7095-123">在 [預覽目錄] 頁面上，按一下 [群組] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="d7095-123">On the **preview directory** page, click the **Groups** tab.</span></span>
5. <span data-ttu-id="d7095-124">若要將群組新增至 Azure AD 租用戶，請在視窗底部的工作窗格中，按一下 [新增群組]。</span><span class="sxs-lookup"><span data-stu-id="d7095-124">To add a group to your Azure AD tenant, on the task pane at the bottom of the window, click **Add Group**.</span></span>

    ![[新增群組] 按鈕](./media/active-directory-domain-services-getting-started/add-group-button.png)
6. <span data-ttu-id="d7095-126">在 [新增群組] 對話方塊中，建立名為 **AAD DC 系統管理員**的群組，然後將 [群組類型] 設定為 [安全性]。</span><span class="sxs-lookup"><span data-stu-id="d7095-126">In the **Add Group** dialog box, create a group named **AAD DC Administrators**, and then set **Group Type** to **Security**.</span></span>

   > [!WARNING]
   > <span data-ttu-id="d7095-127">若要在受 Azure Active Directory Domain Services 管理的網域內啟用存取，請以這個確切名稱建立群組。</span><span class="sxs-lookup"><span data-stu-id="d7095-127">To enable access within your Azure Active Directory Domain Services-managed domain, create a group with this exact name.</span></span>
   >
   >

    ![[新增群組] 對話方塊](./media/active-directory-domain-services-getting-started/create-admin-group.png)
7. <span data-ttu-id="d7095-129">在 [描述] 方塊中輸入描述，讓其他人了解此群組可授與 Azure Active Directory Domain Services 內的系統管理權限。</span><span class="sxs-lookup"><span data-stu-id="d7095-129">In the **Description** box, enter a description that enables others to understand that this group grants administrative permissions within Azure Active Directory Domain Services.</span></span>
8. <span data-ttu-id="d7095-130">建立該群組之後，按一下群組名稱以檢視其屬性。</span><span class="sxs-lookup"><span data-stu-id="d7095-130">After you've created the group, click the group name to view its properties.</span></span>
9. <span data-ttu-id="d7095-131">若要將使用者新增為此群組的成員，請按一下視窗底部的 [新增成員] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d7095-131">To add users as members of the group, at the bottom of the window, click the **Add Members** button.</span></span>

    ![新增群組成員按鈕](./media/active-directory-domain-services-getting-started/add-group-members-button.png)
10. <span data-ttu-id="d7095-133">在 [新增成員] 對話方塊中，選取應成為此群組成員的使用者，然後按一下右下角的核取記號圖示。</span><span class="sxs-lookup"><span data-stu-id="d7095-133">In the **Add members** dialog box, select the users who should be members of this group, and then click the checkmark icon at the lower right.</span></span>

    ![將使用者新增至系統管理員群組](./media/active-directory-domain-services-getting-started/add-group-members.png)


## <a name="next-step"></a><span data-ttu-id="d7095-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d7095-135">Next step</span></span>
[<span data-ttu-id="d7095-136">工作 2：建立或選取 Azure 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="d7095-136">Task 2: create or select an Azure virtual network</span></span>](active-directory-ds-getting-started-vnet.md)
