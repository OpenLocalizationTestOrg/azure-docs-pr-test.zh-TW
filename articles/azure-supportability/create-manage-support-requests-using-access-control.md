---
title: "使用 Azure 角色型存取控制 (RBAC) 控制建立及管理支援要求的存取權 | Microsoft Docs"
description: "使用 Azure 角色型存取控制 (RBAC) 控制建立及管理支援要求的存取權"
author: ganganarayanan
ms.author: gangan
ms.date: 1/31/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: 58a0ca9d-86d2-469a-9714-3b8320c33cf5
ms.openlocfilehash: 20ebd324cbf379980b43d255d468673de2b6d950
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-role-based-access-control-rbac-to-control-access-rights-to-create-and-manage-support-requests"></a><span data-ttu-id="73d4c-103">使用 Azure 角色型存取控制 (RBAC) 控制建立及管理支援要求的存取權</span><span class="sxs-lookup"><span data-stu-id="73d4c-103">Azure Role-Based Access Control (RBAC) to control access rights to create and manage support requests</span></span>

<span data-ttu-id="73d4c-104">[角色型存取控制 (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) 提供適用於 Azure 的詳細存取權管理。</span><span class="sxs-lookup"><span data-stu-id="73d4c-104">[Role-Based Access Control (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) enables fine-grained access management for Azure.</span></span>
<span data-ttu-id="73d4c-105">Azure 入口網站 ([portal.azure.com](https://portal.azure.com)) 中建立支援要求的功能是使用 Azure 的 RBAC 模型來定義可以建立及管理支援要求的人員。</span><span class="sxs-lookup"><span data-stu-id="73d4c-105">Support request creation in the Azure portal, [portal.azure.com](https://portal.azure.com), uses Azure’s RBAC model to define who can create and manage support requests.</span></span>
<span data-ttu-id="73d4c-106">在訂用帳戶、資源群組和應用程式等特定範圍，將適當的 RBAC 角色指派給使用者、群組和應用程式，即可授與存取權。</span><span class="sxs-lookup"><span data-stu-id="73d4c-106">Access is granted by assigning the appropriate RBAC role to users, groups, and applications at a certain scope, which can be a subscription, resource group or a resource.</span></span>

<span data-ttu-id="73d4c-107">我們來看一個範例：您是資源群組擁有者，且擁有訂用帳戶範圍讀取權限，您可以管理資源群組中的所有資源，如網站、虛擬機器，以及子網路。</span><span class="sxs-lookup"><span data-stu-id="73d4c-107">Let’s take an example: As a resource group owner with read permissions at the subscription scope, you can manage all the resources under the resource group, like websites, virtual machines, and subnets.</span></span>
<span data-ttu-id="73d4c-108">不過，當您嘗試建立虛擬機器資源的支援要求時，會遇到錯誤如下</span><span class="sxs-lookup"><span data-stu-id="73d4c-108">However, when you try to create a support request against the virtual machine resource, you encounter the following error</span></span>

![訂用帳戶錯誤](./media/create-manage-support-requests-using-access-control/subscription-error.png)

<span data-ttu-id="73d4c-110">在支援要求管理中，您需要有寫入權限，或是在訂用帳戶範圍有 Microsoft.Support/* 支援動作的角色，才能建立及管理支援要求。</span><span class="sxs-lookup"><span data-stu-id="73d4c-110">In support request management, you need write permission or a role that has the Support action Microsoft.Support/* at the Subscription scope to be able to create and manage support requests.</span></span>

<span data-ttu-id="73d4c-111">以下文章說明您可以如何使用 Azure 的自訂角色型存取控制 (RBAC)，在 Azure 入口網站中建立及管理支援要求。</span><span class="sxs-lookup"><span data-stu-id="73d4c-111">The following article explains how you can use Azure’s custom Role-Based Access Control (RBAC) to create and manage support requests in the Azure portal.</span></span>

## <a name="getting-started"></a><span data-ttu-id="73d4c-112">開始使用</span><span class="sxs-lookup"><span data-stu-id="73d4c-112">Getting Started</span></span>

<span data-ttu-id="73d4c-113">如果訂用帳戶擁有者指派您訂用帳戶的自訂 RBAC 角色，您就能使用上述的範例為資源建立支援要求。</span><span class="sxs-lookup"><span data-stu-id="73d4c-113">Using the example above, you would be able to create a support request for your resource if you were assigned a custom RBAC role on the subscription by the subscription owner.</span></span>
<span data-ttu-id="73d4c-114">使用 Azure PowerShell、Azure 命令列介面 (CLI) 和 REST API，可以建立[自訂 RBAC 角色](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/)。</span><span class="sxs-lookup"><span data-stu-id="73d4c-114">[Custom RBAC roles](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) can be created using Azure PowerShell, Azure Command-Line Interface (CLI), and the REST API.</span></span>

<span data-ttu-id="73d4c-115">自訂角色的動作屬性會指定角色授與存取權的 Azure 作業。</span><span class="sxs-lookup"><span data-stu-id="73d4c-115">The actions property of a custom role specifies the Azure operations to which the role grants access.</span></span>
<span data-ttu-id="73d4c-116">若要建立支援要求管理的自訂角色，該角色必須有 Microsoft.Support/* 動作。</span><span class="sxs-lookup"><span data-stu-id="73d4c-116">To create a custom role for support request management, the role must have the action Microsoft.Support/*</span></span>

<span data-ttu-id="73d4c-117">以下是自訂角色的範例，它可以建立及管理支援要求。</span><span class="sxs-lookup"><span data-stu-id="73d4c-117">Here’s an example of a custom role you can use to create and manage support requests.</span></span>
<span data-ttu-id="73d4c-118">我們將此角色命名為 "Support Request Contributor" (支援要求參與者)，在本文中這個名稱指的就是自訂角色。</span><span class="sxs-lookup"><span data-stu-id="73d4c-118">We’ve named this role “Support Request Contributor” and that’s how we refer to the custom role in this article.</span></span>

``` Json
{
    "Name":  "Support Request Contributor",
    "Id":  "1f2aad59-39b0-41da-b052-2fb070bd7942",
    "IsCustom":  true,
    "Description":  "Lets you create and manage support tickets.",
    "Actions":  [
                    "Microsoft.Support/*"
                ],
    "NotActions":  [
                   ],
    "AssignableScopes":  [
                             "/"
                         ]
}
```

<span data-ttu-id="73d4c-119">遵循[影片](https://www.youtube.com/watch?v=-PaBaDmfwKI)中的步驟以了解如何為您的訂用帳戶建立自訂角色。</span><span class="sxs-lookup"><span data-stu-id="73d4c-119">Follow the steps outlined in [this video](https://www.youtube.com/watch?v=-PaBaDmfwKI) to learn how to create a custom role for your subscription.</span></span>

## <a name="create-and-manage-support-requests-in-the-azure-portal"></a><span data-ttu-id="73d4c-120">在 Azure 入口網站中建立及管理彈性工作</span><span class="sxs-lookup"><span data-stu-id="73d4c-120">Create and manage support requests in the Azure portal</span></span>

<span data-ttu-id="73d4c-121">我們來看一個範例：您是 "Visual Studio MSDN Subscription" 訂用帳戶的擁有者。</span><span class="sxs-lookup"><span data-stu-id="73d4c-121">Let’s take an example – you are the owner of Subscription "Visual Studio MSDN Subscription."</span></span>
<span data-ttu-id="73d4c-122">Joe 是此訂用帳戶內某資源群組的擁有者，和你是對等關係，並且擁有訂用帳戶的讀取權限。</span><span class="sxs-lookup"><span data-stu-id="73d4c-122">Joe is your peer who is a resource owner to some of the resource groups in this subscription and has read permission to the subscription.</span></span>
<span data-ttu-id="73d4c-123">您希望提供 Joe 存取權，讓他能建立及管理此訂用帳戶的支援票證。</span><span class="sxs-lookup"><span data-stu-id="73d4c-123">You wish to give access to your peer, Joe, the ability to create and manage support tickets for the resources under this subscription.</span></span>

1. <span data-ttu-id="73d4c-124">首先移置訂用帳戶，您會在 [設定] 下看到使用者清單。</span><span class="sxs-lookup"><span data-stu-id="73d4c-124">The first step is to go to the subscription and under "Settings" you see a list of users.</span></span> <span data-ttu-id="73d4c-125">按一下使用者 Joe (他有訂用帳戶的讀取者權限)，然後指派自訂角色給他。</span><span class="sxs-lookup"><span data-stu-id="73d4c-125">Click the user Joe who has reader access on the Subscription and let’s assign a new custom role to him.</span></span>

    ![新增角色](./media/create-manage-support-requests-using-access-control/add-role.png)

2. <span data-ttu-id="73d4c-127">按一下 [使用者] 刀鋒視窗中的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="73d4c-127">Click "Add" under the "Users" blade.</span></span> <span data-ttu-id="73d4c-128">選取角色清單中的自訂角色 "Support Request Contributor"</span><span class="sxs-lookup"><span data-stu-id="73d4c-128">Select the custom role "Support Request Contributor" from the list of roles</span></span>

    ![新增支援參與者角色](./media/create-manage-support-requests-using-access-control/add-support-contributor-role.png)

3. <span data-ttu-id="73d4c-130">選取角色名稱之後，按一下 [新增使用者] 並輸入 Joe 的電子郵件認證。</span><span class="sxs-lookup"><span data-stu-id="73d4c-130">After selecting the role name, click "Add users" and enter the Joe's email credentials.</span></span> <span data-ttu-id="73d4c-131">按一下 [選取]</span><span class="sxs-lookup"><span data-stu-id="73d4c-131">Click "Select"</span></span>

    ![新增使用者](./media/create-manage-support-requests-using-access-control/add-users.png)

4. <span data-ttu-id="73d4c-133">按一下 [確定] 以繼續進行</span><span class="sxs-lookup"><span data-stu-id="73d4c-133">Click "Ok" to proceed</span></span>

    ![新增存取](./media/create-manage-support-requests-using-access-control/add-access.png)

5. <span data-ttu-id="73d4c-135">現在，剛才新增自訂角色 "Support Request Contributor" 的使用者會顯示在您擁有的訂用帳戶下</span><span class="sxs-lookup"><span data-stu-id="73d4c-135">Now you see the user with the newly added custom role "Support Request Contributor" under the Subscription for which you are the owner</span></span>

    ![新增的使用者](./media/create-manage-support-requests-using-access-control/user-added.png)

    <span data-ttu-id="73d4c-137">當 Joe 登入入口網站時，他會看到已新增的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="73d4c-137">When Joe logs in the portal, he sees the subscription to which he was added.</span></span>

7. <span data-ttu-id="73d4c-138">Joe 只要按一下 [說明及支援] 刀鋒視窗中的 [新增支援要求]，就能建立「Visual Studio Ultimate 含 MSDN」的支援要求</span><span class="sxs-lookup"><span data-stu-id="73d4c-138">Joe clicks "New Support request" from the "Help and Support" blade and can create support requests for "Visual Studio Ultimate with MSDN"</span></span>

    ![新增支援要求](./media/create-manage-support-requests-using-access-control/new-support-request.png)

8. <span data-ttu-id="73d4c-140">按一下 「 所有支援的要求 」 Joe 可以檢視針對此訂用帳戶建立支援要求清單![案例詳細資料檢視](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span><span class="sxs-lookup"><span data-stu-id="73d4c-140">Clicking "All support requests" Joe can see the list of support requests created for this Subscription  ![Case details view](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span></span>

## <a name="remove-support-request-access-in-the-azure-portal"></a><span data-ttu-id="73d4c-141">在 Azure 入口網站中移除支援要求存取權</span><span class="sxs-lookup"><span data-stu-id="73d4c-141">Remove support request access in the Azure portal</span></span>

<span data-ttu-id="73d4c-142">如同可以授與使用者建立及管理支援要求的存取權，您也可以移除使用者的存取權。</span><span class="sxs-lookup"><span data-stu-id="73d4c-142">Just as it is possible to grant access to a user to create and manage support requests, it's possible to remove access for the user as well.</span></span>
<span data-ttu-id="73d4c-143">若要移除建立及管理支援要求的能力，請移至該訂用帳戶，按一下 [設定] 然後按一下使用者 (此範例中為 Joe)。</span><span class="sxs-lookup"><span data-stu-id="73d4c-143">To remove the ability to create and manage support requests, go to the Subscription, click "Settings" and click the user (in this case, Joe).</span></span>
<span data-ttu-id="73d4c-144">按一下角色名稱 [Support Request Contributor]，再按一下 [移除]</span><span class="sxs-lookup"><span data-stu-id="73d4c-144">Right-click the role name, "Support Request Contributor" and click "Remove"</span></span>

![移除支援要求存取權](./media/create-manage-support-requests-using-access-control/remove-support-request-access.png)

<span data-ttu-id="73d4c-146">當 Joe 登入入口網站並嘗試建立支援要求時，他會遇到錯誤如下</span><span class="sxs-lookup"><span data-stu-id="73d4c-146">When Joe logs in to the portal and tries to create a support request, he encounters the following error</span></span>

![訂用帳戶錯誤-2](./media/create-manage-support-requests-using-access-control/subscription-error-2.png)

<span data-ttu-id="73d4c-148">當 Joe 按一下 [所有支援要求] 時，他不會看到任何支援要求</span><span class="sxs-lookup"><span data-stu-id="73d4c-148">Joe cannot see any support requests when he clicks "All support requests"</span></span>

![案例詳細資料檢視-2](./media/create-manage-support-requests-using-access-control/case-details-view-2.png)
