---
title: "新使用者 tooAzure aaaAdd Active Directory |Microsoft 文件"
description: "說明如何 tooadd 新使用者或變更 Azure Active Directory 中的使用者資訊。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 0a90c3c5-4e0e-43bd-a606-6ee00f163038
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: curtand;jeffsta
ms.reviewer: jeffsta
ms.openlocfilehash: c4a156ea31b81202bb0d0ac224afbfc3f1785532
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-new-users-tooazure-active-directory"></a><span data-ttu-id="b76ce-103">加入新使用者 tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b76ce-103">Add new users tooAzure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b76ce-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b76ce-104">Azure portal</span></span>](active-directory-users-create-azure-portal.md)
> * [<span data-ttu-id="b76ce-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="b76ce-105">Azure classic portal</span></span>](active-directory-create-users.md)
>
>

<span data-ttu-id="b76ce-106">本文說明如何在組織中的 tooadd 新使用者 hello Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="b76ce-106">This article explains how tooadd new users in your organization in hello Azure Active Directory (Azure AD).</span></span> 

1. <span data-ttu-id="b76ce-107">登入 toohello [Azure 入口網站](https://portal.azure.com)hello 目錄的全域管理員的帳戶。</span><span class="sxs-lookup"><span data-stu-id="b76ce-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="b76ce-108">選取**更多服務**，輸入**使用者和群組**在 hello 文字方塊中，然後選取  **Enter**。</span><span class="sxs-lookup"><span data-stu-id="b76ce-108">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![開啟使用者和群組](./media/active-directory-users-create-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="b76ce-110">在 hello**使用者和群組**刀鋒視窗中，選取**所有使用者**，然後選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="b76ce-110">On hello **Users and groups** blade, select **All users**, and then select **Add**.</span></span>

   ![選取 hello Add 命令](./media/active-directory-users-create-azure-portal/create-users-add-command.png)
4. <span data-ttu-id="b76ce-112">Hello 使用者輸入的詳細資訊，例如**名稱**和**使用者名**。</span><span class="sxs-lookup"><span data-stu-id="b76ce-112">Enter details for hello user, such as **Name** and **User name**.</span></span> <span data-ttu-id="b76ce-113">hello 網域名稱部分 hello 使用者名稱必須是 hello 初始預設網域名稱 」 foo.onmicrosoft.com 「 網域名稱或已驗證、 非同盟的網域名稱，例如"contoso.com"。</span><span class="sxs-lookup"><span data-stu-id="b76ce-113">hello domain name portion of hello user name must either be hello initial default domain name "foo.onmicrosoft.com" domain name, or a verified, non-federated domain name such as "contoso.com."</span></span>
5. <span data-ttu-id="b76ce-114">複製或其他方式的附註 hello，讓您能夠提供其 toohello 使用者完成此程序之後產生的使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="b76ce-114">Copy or otherwise note hello generated user password so that you can provide it toohello user after this process is complete.</span></span>
6. <span data-ttu-id="b76ce-115">（選擇性） 您可以開啟，並填寫 hello 資訊在 hello**設定檔**刀鋒視窗，hello**群組**刀鋒視窗中或使用 hello**目錄角色**hello 使用者 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b76ce-115">Optionally, you can open and fill out hello information in hello **Profile** blade, hello **Groups** blade, or hello **Directory role** blade for hello user.</span></span> <span data-ttu-id="b76ce-116">如需有關使用者和系統管理員角色的詳細資訊，請參閱 [在 Azure AD 中指派系統管理員角色](active-directory-assign-admin-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="b76ce-116">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="b76ce-117">在 hello**使用者**刀鋒視窗中，選取**建立**。</span><span class="sxs-lookup"><span data-stu-id="b76ce-117">On hello **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="b76ce-118">安全地散發 hello 產生密碼 toohello 新使用者，讓 hello 使用者可以登入。</span><span class="sxs-lookup"><span data-stu-id="b76ce-118">Securely distribute hello generated password toohello new user so that hello user can sign in.</span></span>

### <a name="next-steps"></a><span data-ttu-id="b76ce-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b76ce-119">Next steps</span></span>
* [<span data-ttu-id="b76ce-120">新增外部使用者</span><span class="sxs-lookup"><span data-stu-id="b76ce-120">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)
* [<span data-ttu-id="b76ce-121">重設使用者密碼在 hello 新版 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b76ce-121">Reset a user's password in hello new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="b76ce-122">變更使用者的工作資訊</span><span class="sxs-lookup"><span data-stu-id="b76ce-122">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="b76ce-123">管理使用者設定檔</span><span class="sxs-lookup"><span data-stu-id="b76ce-123">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="b76ce-124">在 Azure AD 中刪除使用者</span><span class="sxs-lookup"><span data-stu-id="b76ce-124">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
* [<span data-ttu-id="b76ce-125">在您的 Azure AD 中指派使用者 tooa 角色</span><span class="sxs-lookup"><span data-stu-id="b76ce-125">Assign a user tooa role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)
