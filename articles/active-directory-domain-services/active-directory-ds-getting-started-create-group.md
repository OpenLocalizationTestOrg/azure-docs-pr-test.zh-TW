---
title: "Azure Active Directory 網域服務： 建立 hello Azure AD DC administrators 群組 |Microsoft 文件"
description: "啟用 Azure Active Directory 網域服務使用 hello Azure 傳統入口網站"
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
ms.openlocfilehash: d629ab9632ef6a45b549630999ff9a122d60c040
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a><span data-ttu-id="0a750-103">啟用 Azure Active Directory 網域服務使用 hello Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="0a750-103">Enable Azure Active Directory Domain Services using hello Azure classic portal</span></span>
<span data-ttu-id="0a750-104">本文說明，並逐步引導您 tooenable Azure Active Directory 網域服務 (Azure AD DS) Azure Active Directory (Azure AD) 租用戶的 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="0a750-104">This article describes and walks through hello configuration tasks that are required for you tooenable Azure Active Directory Domain Services (Azure AD DS) for your Azure Active Directory (Azure AD) tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="0a750-105">[**請改嘗試 hello 新 Azure （預覽） 入口網站體驗**](active-directory-ds-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="0a750-105">[**Try hello new (preview) Azure portal experience instead**](active-directory-ds-getting-started.md).</span></span> 
>

## <a name="task-1-create-hello-azure-ad-dc-administrators-group"></a><span data-ttu-id="0a750-106">工作 1： 建立 hello Azure AD DC administrators 群組</span><span class="sxs-lookup"><span data-stu-id="0a750-106">Task 1: create hello Azure AD DC administrators group</span></span>
<span data-ttu-id="0a750-107">hello 第一項工作是 toocreate Azure AD 租用戶中的系統管理群組。</span><span class="sxs-lookup"><span data-stu-id="0a750-107">hello first task is toocreate an administrative group in your Azure AD tenant.</span></span> <span data-ttu-id="0a750-108">這個特殊的系統管理群組稱為 *AAD DC 系統管理員*。</span><span class="sxs-lookup"><span data-stu-id="0a750-108">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="0a750-109">系統管理員權限的電腦已加入網域的 toohello Azure Active Directory 網域服務管理的網域，會授與此群組的成員。</span><span class="sxs-lookup"><span data-stu-id="0a750-109">Members of this group are granted administrative permissions on machines that are domain-joined toohello Azure Active Directory Domain Services-managed domain.</span></span> <span data-ttu-id="0a750-110">已加入網域的電腦上，此群組會加入 toohello administrators 群組。</span><span class="sxs-lookup"><span data-stu-id="0a750-110">On domain-joined machines, this group is added toohello administrators group.</span></span> <span data-ttu-id="0a750-111">此外，此群組的成員可以使用遠端桌面 tooconnect 遠端 toodomain 加入機器。</span><span class="sxs-lookup"><span data-stu-id="0a750-111">Additionally, members of this group can use Remote Desktop tooconnect remotely toodomain-joined machines.</span></span>  

> [!NOTE]
> <span data-ttu-id="0a750-112">您沒有 hello 您使用 Azure Active Directory 網域服務建立的受管理網域的網域系統管理員或企業系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="0a750-112">You do not have Domain Administrator or Enterprise Administrator permissions on hello managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="0a750-113">上受管理的網域，這些權限所保留的 hello 服務，並不會使用 toousers hello 租用戶中。</span><span class="sxs-lookup"><span data-stu-id="0a750-113">On managed domains, these permissions are reserved by hello service and are not made available toousers within hello tenant.</span></span> <span data-ttu-id="0a750-114">不過，您可以使用特殊 hello 建立系統管理群組中此組態工作 tooperform 某些特殊權限操作。</span><span class="sxs-lookup"><span data-stu-id="0a750-114">However, you can use hello special administrative group created in this configuration task tooperform some privileged operations.</span></span> <span data-ttu-id="0a750-115">這些作業包括加入電腦 toohello 網域屬於 toohello 管理群組已加入網域的機器上，設定群組原則。</span><span class="sxs-lookup"><span data-stu-id="0a750-115">These operations include joining computers toohello domain, belonging toohello administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="0a750-116">在這項組態工作，您可以建立 hello 系統管理群組和目錄 toohello 群組中加入一個或多個使用者。</span><span class="sxs-lookup"><span data-stu-id="0a750-116">In this configuration task, you create hello administrative group and add one or more users in your directory toohello group.</span></span> <span data-ttu-id="0a750-117">Azure Active Directory 網域服務，toocreate hello 系統管理群組 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="0a750-117">toocreate hello administrative group for Azure Active Directory Domain Services, do hello following:</span></span>

1. <span data-ttu-id="0a750-118">移 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="0a750-118">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="0a750-119">Hello 左窗格中，選取 [hello **Active Directory** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0a750-119">In hello left pane, select hello **Active Directory** button.</span></span>
3. <span data-ttu-id="0a750-120">選取 hello Azure AD 租用戶 （目錄），您會想 tooenable Azure Active Directory 網域服務。</span><span class="sxs-lookup"><span data-stu-id="0a750-120">Select hello Azure AD tenant (directory) for which you want tooenable Azure Active Directory Domain Services.</span></span> <span data-ttu-id="0a750-121">您只能針對每個 Azure AD 目錄建立一個網域。</span><span class="sxs-lookup"><span data-stu-id="0a750-121">You can create only one domain for each Azure AD directory.</span></span>

    ![選取 Azure AD 目錄](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="0a750-123">在 [hello**預覽目錄**頁面上，按一下 hello**群組**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0a750-123">On hello **preview directory** page, click hello **Groups** tab.</span></span>
5. <span data-ttu-id="0a750-124">tooadd 群組 tooyour Azure AD 租用戶，在 hello hello 視窗底部的 hello 工作窗格上按一下**加入群組**。</span><span class="sxs-lookup"><span data-stu-id="0a750-124">tooadd a group tooyour Azure AD tenant, on hello task pane at hello bottom of hello window, click **Add Group**.</span></span>

    ![hello 加入群組 按鈕](./media/active-directory-domain-services-getting-started/add-group-button.png)
6. <span data-ttu-id="0a750-126">在 hello**加入群組**對話方塊方塊中，建立名為群組**AAD DC 管理員**，然後設定**群組類型**太**安全性**。</span><span class="sxs-lookup"><span data-stu-id="0a750-126">In hello **Add Group** dialog box, create a group named **AAD DC Administrators**, and then set **Group Type** too**Security**.</span></span>

   > [!WARNING]
   > <span data-ttu-id="0a750-127">tooenable 存取 Azure Active Directory 網域服務受管理網域內建立完全同名的群組。</span><span class="sxs-lookup"><span data-stu-id="0a750-127">tooenable access within your Azure Active Directory Domain Services-managed domain, create a group with this exact name.</span></span>
   >
   >

    ![hello 新增群組對話方塊](./media/active-directory-domain-services-getting-started/create-admin-group.png)
7. <span data-ttu-id="0a750-129">在 hello**描述**方塊中，輸入描述，可讓其他人 toounderstand 此群組授與 Azure Active Directory 網域服務的系統管理權限。</span><span class="sxs-lookup"><span data-stu-id="0a750-129">In hello **Description** box, enter a description that enables others toounderstand that this group grants administrative permissions within Azure Active Directory Domain Services.</span></span>
8. <span data-ttu-id="0a750-130">在您建立 hello 群組後，按一下 hello 群組名稱 tooview 其內容。</span><span class="sxs-lookup"><span data-stu-id="0a750-130">After you've created hello group, click hello group name tooview its properties.</span></span>
9. <span data-ttu-id="0a750-131">為在 hello hello 視窗底部的 hello 群組成員的 tooadd 使用者按一下 hello**新增成員** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0a750-131">tooadd users as members of hello group, at hello bottom of hello window, click hello **Add Members** button.</span></span>

    ![新增群組成員按鈕](./media/active-directory-domain-services-getting-started/add-group-members-button.png)
10. <span data-ttu-id="0a750-133">在 [hello**將成員加入**對話方塊中，選取 hello 使用者應該是此群組的成員，然後按一下hello] 核取記號圖示，hello 右下。</span><span class="sxs-lookup"><span data-stu-id="0a750-133">In hello **Add members** dialog box, select hello users who should be members of this group, and then click hello checkmark icon at hello lower right.</span></span>

    ![新增使用者 tooadministrators 群組](./media/active-directory-domain-services-getting-started/add-group-members.png)


## <a name="next-step"></a><span data-ttu-id="0a750-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0a750-135">Next step</span></span>
[<span data-ttu-id="0a750-136">工作 2：建立或選取 Azure 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="0a750-136">Task 2: create or select an Azure virtual network</span></span>](active-directory-ds-getting-started-vnet.md)
