---
title: "新使用者 tooAzure aaaAdd Active Directory |Microsoft 文件"
description: "說明如何在 Azure Active Directory tooadd 新使用者。"
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jeffgilb
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 6ca413c84a7a5238a30fd26fc751d687d827b24a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-new-users-tooazure-active-directory"></a><span data-ttu-id="a35bb-103">快速入門： 加入新使用者 tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a35bb-103">Quickstart: Add new users tooAzure Active Directory</span></span>
<span data-ttu-id="a35bb-104">本文說明 tooadd hello Azure Active Directory (Azure AD) 中您組織中的新使用者如何當其中一一次使用 hello Azure 入口網站或同步處理內部部署 Windows Server AD 使用者帳戶資料。</span><span class="sxs-lookup"><span data-stu-id="a35bb-104">This article explains how tooadd new users in your organization in hello Azure Active Directory (Azure AD) one at a time using hello Azure portal or by synchronizing your on-premises Windows Server AD user account data.</span></span> 

## <a name="add-cloud-based-users"></a><span data-ttu-id="a35bb-105">新增雲端式使用者</span><span class="sxs-lookup"><span data-stu-id="a35bb-105">Add cloud-based users</span></span>
1. <span data-ttu-id="a35bb-106">登入 toohello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com)hello 目錄的全域管理員的帳戶。</span><span class="sxs-lookup"><span data-stu-id="a35bb-106">Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="a35bb-107">選取 [Azure Active Directory]**Azure Active Directory**，然後選取 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="a35bb-107">Select **Azure Active Directory** and then **Users and groups**.</span></span>
3. <span data-ttu-id="a35bb-108">在 hello**使用者和群組**刀鋒視窗中，選取**所有使用者**，然後選取**新使用者**。</span><span class="sxs-lookup"><span data-stu-id="a35bb-108">On hello **Users and groups** blade, select **All users**, and then select **New user**.</span></span>
   <span data-ttu-id="a35bb-109">![選取 hello Add 命令](./media/add-users-azure-active-directory/add-user.png)</span><span class="sxs-lookup"><span data-stu-id="a35bb-109">![Selecting hello Add command](./media/add-users-azure-active-directory/add-user.png)</span></span>
4. <span data-ttu-id="a35bb-110">Hello 使用者輸入的詳細資訊，例如**名稱**和**使用者名**。</span><span class="sxs-lookup"><span data-stu-id="a35bb-110">Enter details for hello user, such as **Name** and **User name**.</span></span> <span data-ttu-id="a35bb-111">hello hello 使用者名稱的網域名稱部分必須 hello 初始預設網域名稱"[網域名稱].onmicrosoft.com 」 或已驗證非同盟[自訂網域名稱](add-custom-domain.md)例如"contoso.com"。</span><span class="sxs-lookup"><span data-stu-id="a35bb-111">hello domain name portion of hello user name must either be hello initial default domain name "[domain name].onmicrosoft.com" or a verified, non-federated [custom domain name](add-custom-domain.md) such as "contoso.com."</span></span>
5. <span data-ttu-id="a35bb-112">複製或其他方式的附註 hello，讓您能夠提供其 toohello 使用者完成此程序之後產生的使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="a35bb-112">Copy or otherwise note hello generated user password so that you can provide it toohello user after this process is complete.</span></span>
6. <span data-ttu-id="a35bb-113">（選擇性） 您可以開啟，並填寫 hello 資訊在 hello**設定檔**刀鋒視窗，hello**群組**刀鋒視窗中或使用 hello**目錄角色**hello 使用者 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a35bb-113">Optionally, you can open and fill out hello information in hello **Profile** blade, hello **Groups** blade, or hello **Directory role** blade for hello user.</span></span> <span data-ttu-id="a35bb-114">如需有關使用者和系統管理員角色的詳細資訊，請參閱 [在 Azure AD 中指派系統管理員角色](active-directory-assign-admin-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="a35bb-114">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="a35bb-115">在 hello**使用者**刀鋒視窗中，選取**建立**。</span><span class="sxs-lookup"><span data-stu-id="a35bb-115">On hello **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="a35bb-116">安全地散發 hello 產生密碼 toohello 新使用者，讓 hello 使用者可以登入。</span><span class="sxs-lookup"><span data-stu-id="a35bb-116">Securely distribute hello generated password toohello new user so that hello user can sign in.</span></span>

> [!TIP]
> <span data-ttu-id="a35bb-117">您也可以同步處理內部部署 Windows Server AD 中的使用者帳戶資料。</span><span class="sxs-lookup"><span data-stu-id="a35bb-117">You can also synchronize user account data from on-premises Windows Server AD.</span></span> <span data-ttu-id="a35bb-118">Microsoft 的身分識別解決方案跨越內部部署和雲端架構的功能，建立單一使用者識別進行驗證和授權 tooall 資源，不論位置為何。</span><span class="sxs-lookup"><span data-stu-id="a35bb-118">Microsoft’s identity solutions span on-premises and cloud-based capabilities, creating a single user identity for authentication and authorization tooall resources, regardless of location.</span></span> <span data-ttu-id="a35bb-119">我們稱之為混合式身分識別。</span><span class="sxs-lookup"><span data-stu-id="a35bb-119">We call this Hybrid Identity.</span></span> <span data-ttu-id="a35bb-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)可以是您的內部部署目錄與 Azure Active Directory 混合式身分識別案例使用的 toointegrate。</span><span class="sxs-lookup"><span data-stu-id="a35bb-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) can be used toointegrate your on-premises directories with Azure Active Directory for hybrid identity scenarios.</span></span> <span data-ttu-id="a35bb-121">這可讓您 tooprovide 通用識別身分為您的 Office 365、 Azure 和 SaaS 應用程式的使用者與 Azure AD 整合。</span><span class="sxs-lookup"><span data-stu-id="a35bb-121">This allows you tooprovide a common identity for your users for Office 365, Azure, and SaaS applications integrated with Azure AD.</span></span> 

## <a name="delete-users-from-azure-ad"></a><span data-ttu-id="a35bb-122">從 Azure AD 刪除使用者</span><span class="sxs-lookup"><span data-stu-id="a35bb-122">Delete users from Azure AD</span></span>
1. <span data-ttu-id="a35bb-123">登入 toohello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com)hello 目錄的全域管理員的帳戶。</span><span class="sxs-lookup"><span data-stu-id="a35bb-123">Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="a35bb-124">選取 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="a35bb-124">Select **Users and groups**.</span></span>
3. <span data-ttu-id="a35bb-125">在 hello**使用者和群組**刀鋒視窗中，選取 hello 使用者 toodelete 從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="a35bb-125">On hello **Users and groups** blade, select hello user toodelete from hello list.</span></span> 
4. <span data-ttu-id="a35bb-126">在 hello 選使用者的 hello 刀鋒視窗，選取 **概觀**，然後 hello 命令列中，選取**刪除**。</span><span class="sxs-lookup"><span data-stu-id="a35bb-126">On hello blade for hello selected user, select **Overview**, and then in hello command bar, select **Delete**.</span></span>
   <span data-ttu-id="a35bb-127">![選取 hello Add 命令](./media/add-users-azure-active-directory/delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="a35bb-127">![Selecting hello Add command](./media/add-users-azure-active-directory/delete-user.png)</span></span>


### <a name="learn-more"></a><span data-ttu-id="a35bb-128">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="a35bb-128">Learn more</span></span> 
* [<span data-ttu-id="a35bb-129">新增外部使用者</span><span class="sxs-lookup"><span data-stu-id="a35bb-129">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)

* [<span data-ttu-id="a35bb-130">在您的 Azure AD 中指派使用者 tooa 角色</span><span class="sxs-lookup"><span data-stu-id="a35bb-130">Assign a user tooa role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)

## <a name="next-steps"></a><span data-ttu-id="a35bb-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a35bb-131">Next steps</span></span>
<span data-ttu-id="a35bb-132">本快速入門中，您學到如何新增使用者 tooAzure tooadd AD Premium。</span><span class="sxs-lookup"><span data-stu-id="a35bb-132">In this quickstart, you’ve learned how tooadd new users tooAzure AD Premium.</span></span> 

<span data-ttu-id="a35bb-133">您可以使用 hello hello Azure 入口網站中的下列 Azure AD 中的連結 toocreate 新的使用者。</span><span class="sxs-lookup"><span data-stu-id="a35bb-133">You can use hello following link toocreate a new user in Azure AD from hello Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a35bb-134">新增使用者 tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="a35bb-134">Add users tooAzure AD</span></span>](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 
