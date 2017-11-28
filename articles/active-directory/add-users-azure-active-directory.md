---
title: "將使用者新增至 Azure Active Directory | Microsoft Docs"
description: "說明如何在 Azure Active Directory 中新增使用者。"
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
ms.openlocfilehash: 13a7d2d3b991206c45e66872b590bc27a224eead
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="quickstart-add-new-users-to-azure-active-directory"></a><span data-ttu-id="1c172-103">快速入門：將使用者新增至 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1c172-103">Quickstart: Add new users to Azure Active Directory</span></span>
<span data-ttu-id="1c172-104">本文說明如何在 Azure Active Directory (Azure AD) 中新增您組織中的使用者，您可以使用 Azure 入口網站一次新增一位，或藉由同步處理您內部部署 Windows Server AD 使用者帳戶資料來新增。</span><span class="sxs-lookup"><span data-stu-id="1c172-104">This article explains how to add new users in your organization in the Azure Active Directory (Azure AD) one at a time using the Azure portal or by synchronizing your on-premises Windows Server AD user account data.</span></span> 

## <a name="add-cloud-based-users"></a><span data-ttu-id="1c172-105">新增雲端式使用者</span><span class="sxs-lookup"><span data-stu-id="1c172-105">Add cloud-based users</span></span>
1. <span data-ttu-id="1c172-106">使用具備目錄全域管理員身分的帳戶來登入 [Azure Active Directory 管理中心](https://aad.portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="1c172-106">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="1c172-107">選取 [Azure Active Directory]**Azure Active Directory**，然後選取 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="1c172-107">Select **Azure Active Directory** and then **Users and groups**.</span></span>
3. <span data-ttu-id="1c172-108">在 [使用者和群組] 刀鋒視窗上，選取 [所有使用者]，然後選取 [新增使用者]。</span><span class="sxs-lookup"><span data-stu-id="1c172-108">On the **Users and groups** blade, select **All users**, and then select **New user**.</span></span>
   <span data-ttu-id="1c172-109">![選取 [新增] 命令](./media/add-users-azure-active-directory/add-user.png)</span><span class="sxs-lookup"><span data-stu-id="1c172-109">![Selecting the Add command](./media/add-users-azure-active-directory/add-user.png)</span></span>
4. <span data-ttu-id="1c172-110">輸入使用者的詳細資料，例如「名稱」和「使用者名稱」。</span><span class="sxs-lookup"><span data-stu-id="1c172-110">Enter details for the user, such as **Name** and **User name**.</span></span> <span data-ttu-id="1c172-111">使用者名稱的網域名稱部分必須是初始預設網域名稱 "[網域名稱].onmicrosoft.com"，或是已驗證的非同盟[自訂網域名稱](add-custom-domain.md)，例如"contoso.com"。</span><span class="sxs-lookup"><span data-stu-id="1c172-111">The domain name portion of the user name must either be the initial default domain name "[domain name].onmicrosoft.com" or a verified, non-federated [custom domain name](add-custom-domain.md) such as "contoso.com."</span></span>
5. <span data-ttu-id="1c172-112">複製或記下產生的使用者密碼，以便在此程序完成後，將它提供給使用者。</span><span class="sxs-lookup"><span data-stu-id="1c172-112">Copy or otherwise note the generated user password so that you can provide it to the user after this process is complete.</span></span>
6. <span data-ttu-id="1c172-113">(選擇性) 您可以開啟使用者的 [設定檔] 刀鋒視窗、[群組] 刀鋒視窗或 [目錄角色] 刀鋒視窗，然後在其中填入資訊。</span><span class="sxs-lookup"><span data-stu-id="1c172-113">Optionally, you can open and fill out the information in the **Profile** blade, the **Groups** blade, or the **Directory role** blade for the user.</span></span> <span data-ttu-id="1c172-114">如需有關使用者和系統管理員角色的詳細資訊，請參閱 [在 Azure AD 中指派系統管理員角色](active-directory-assign-admin-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="1c172-114">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="1c172-115">在 [使用者] 刀鋒視窗上，選取 [建立]。</span><span class="sxs-lookup"><span data-stu-id="1c172-115">On the **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="1c172-116">將產生的密碼安全地散發給新使用者，以便讓使用者可以登入。</span><span class="sxs-lookup"><span data-stu-id="1c172-116">Securely distribute the generated password to the new user so that the user can sign in.</span></span>

> [!TIP]
> <span data-ttu-id="1c172-117">您也可以同步處理內部部署 Windows Server AD 中的使用者帳戶資料。</span><span class="sxs-lookup"><span data-stu-id="1c172-117">You can also synchronize user account data from on-premises Windows Server AD.</span></span> <span data-ttu-id="1c172-118">Microsoft 的身分識別解決方案可跨越內部部署和雲端架構功能，建立單一使用者身分識別以用於所有資源的驗證和授權，不論位於何處。</span><span class="sxs-lookup"><span data-stu-id="1c172-118">Microsoft’s identity solutions span on-premises and cloud-based capabilities, creating a single user identity for authentication and authorization to all resources, regardless of location.</span></span> <span data-ttu-id="1c172-119">我們稱之為混合式身分識別。</span><span class="sxs-lookup"><span data-stu-id="1c172-119">We call this Hybrid Identity.</span></span> <span data-ttu-id="1c172-120">您可以針對混合式身分識別案例，使用 [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) 來整合您的內部部署目錄與 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="1c172-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) can be used to integrate your on-premises directories with Azure Active Directory for hybrid identity scenarios.</span></span> <span data-ttu-id="1c172-121">這可讓您為與 Azure AD 整合之 Office 365、Azure 和 SaaS 應用程式的使用者提供通用身分識別。</span><span class="sxs-lookup"><span data-stu-id="1c172-121">This allows you to provide a common identity for your users for Office 365, Azure, and SaaS applications integrated with Azure AD.</span></span> 

## <a name="delete-users-from-azure-ad"></a><span data-ttu-id="1c172-122">從 Azure AD 刪除使用者</span><span class="sxs-lookup"><span data-stu-id="1c172-122">Delete users from Azure AD</span></span>
1. <span data-ttu-id="1c172-123">使用具備目錄全域管理員身分的帳戶來登入 [Azure Active Directory 管理中心](https://aad.portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="1c172-123">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="1c172-124">選取 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="1c172-124">Select **Users and groups**.</span></span>
3. <span data-ttu-id="1c172-125">在 [使用者和群組] 刀鋒視窗上，從清單中選取要刪除的使用者。</span><span class="sxs-lookup"><span data-stu-id="1c172-125">On the **Users and groups** blade, select the user to delete from the list.</span></span> 
4. <span data-ttu-id="1c172-126">在所選使用者的刀鋒視窗上選取 [概觀]，然後在命令列中選取 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="1c172-126">On the blade for the selected user, select **Overview**, and then in the command bar, select **Delete**.</span></span>
   <span data-ttu-id="1c172-127">![選取 [新增] 命令](./media/add-users-azure-active-directory/delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="1c172-127">![Selecting the Add command](./media/add-users-azure-active-directory/delete-user.png)</span></span>


### <a name="learn-more"></a><span data-ttu-id="1c172-128">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="1c172-128">Learn more</span></span> 
* [<span data-ttu-id="1c172-129">新增外部使用者</span><span class="sxs-lookup"><span data-stu-id="1c172-129">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)

* [<span data-ttu-id="1c172-130">在 Azure AD 中將使用者指派給角色</span><span class="sxs-lookup"><span data-stu-id="1c172-130">Assign a user to a role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)

## <a name="next-steps"></a><span data-ttu-id="1c172-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1c172-131">Next steps</span></span>
<span data-ttu-id="1c172-132">在此快速入門中，您學到如何將使用者新增至 Azure AD Premium。</span><span class="sxs-lookup"><span data-stu-id="1c172-132">In this quickstart, you’ve learned how to add new users to Azure AD Premium.</span></span> 

<span data-ttu-id="1c172-133">您可以使用下列連結，從 Azure 入口網站在 Azure AD 中建立新的使用者。</span><span class="sxs-lookup"><span data-stu-id="1c172-133">You can use the following link to create a new user in Azure AD from the Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1c172-134">在 Azure AD 中新增使用者</span><span class="sxs-lookup"><span data-stu-id="1c172-134">Add users to Azure AD</span></span>](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 