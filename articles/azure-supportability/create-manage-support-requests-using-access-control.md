---
title: "aaaAzure 角色型存取控制 (RBAC) toocontrol 存取權限 toocreate 及管理支援要求 |Microsoft 文件"
description: "Azure 角色型存取控制 (RBAC) toocontrol 存取權限 toocreate 及管理支援要求"
author: ganganarayanan
ms.author: gangan
ms.date: 1/31/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: 58a0ca9d-86d2-469a-9714-3b8320c33cf5
ms.openlocfilehash: c68a699ac870fa6bf371deb8ed0424848f39acf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-role-based-access-control-rbac-toocontrol-access-rights-toocreate-and-manage-support-requests"></a><span data-ttu-id="2b34b-103">Azure 角色型存取控制 (RBAC) toocontrol 存取權限 toocreate 及管理支援要求</span><span class="sxs-lookup"><span data-stu-id="2b34b-103">Azure Role-Based Access Control (RBAC) toocontrol access rights toocreate and manage support requests</span></span>

<span data-ttu-id="2b34b-104">[角色型存取控制 (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) 提供適用於 Azure 的詳細存取權管理。</span><span class="sxs-lookup"><span data-stu-id="2b34b-104">[Role-Based Access Control (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) enables fine-grained access management for Azure.</span></span>
<span data-ttu-id="2b34b-105">支援 hello Azure 入口網站中的要求建立[portal.azure.com](https://portal.azure.com)，使用 Azure RBAC 模型 toodefine 可以建立和管理的支援要求。</span><span class="sxs-lookup"><span data-stu-id="2b34b-105">Support request creation in hello Azure portal, [portal.azure.com](https://portal.azure.com), uses Azure’s RBAC model toodefine who can create and manage support requests.</span></span>
<span data-ttu-id="2b34b-106">指派適當 RBAC 角色 toousers hello、 群組和應用程式在特定範圍，它可以是訂用帳戶、 資源群組或資源授與的存取。</span><span class="sxs-lookup"><span data-stu-id="2b34b-106">Access is granted by assigning hello appropriate RBAC role toousers, groups, and applications at a certain scope, which can be a subscription, resource group or a resource.</span></span>

<span data-ttu-id="2b34b-107">讓我們來看一個範例： 為具有 hello 訂用帳戶範圍的讀取權限的資源群組擁有者，您可以管理在 hello 資源群組下，例如網站、 虛擬機器，以及子網路的所有 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="2b34b-107">Let’s take an example: As a resource group owner with read permissions at hello subscription scope, you can manage all hello resources under hello resource group, like websites, virtual machines, and subnets.</span></span>
<span data-ttu-id="2b34b-108">不過，當您嘗試 toocreate 針對 hello 虛擬機器資源的支援要求時，您遇到下列錯誤 hello</span><span class="sxs-lookup"><span data-stu-id="2b34b-108">However, when you try toocreate a support request against hello virtual machine resource, you encounter hello following error</span></span>

![訂用帳戶錯誤](./media/create-manage-support-requests-using-access-control/subscription-error.png)

<span data-ttu-id="2b34b-110">在支援要求的管理，您需要寫入權限，或具有 hello 的角色，可支援在 hello 訂用帳戶範圍 toobe 無法 toocreate 動作 Microsoft.Support/* 及管理支援要求。</span><span class="sxs-lookup"><span data-stu-id="2b34b-110">In support request management, you need write permission or a role that has hello Support action Microsoft.Support/* at hello Subscription scope toobe able toocreate and manage support requests.</span></span>

<span data-ttu-id="2b34b-111">hello 下列文章說明如何使用 Azure 的自訂角色型存取控制 (RBAC) toocreate，及管理在 hello Azure 入口網站的支援要求。</span><span class="sxs-lookup"><span data-stu-id="2b34b-111">hello following article explains how you can use Azure’s custom Role-Based Access Control (RBAC) toocreate and manage support requests in hello Azure portal.</span></span>

## <a name="getting-started"></a><span data-ttu-id="2b34b-112">開始使用</span><span class="sxs-lookup"><span data-stu-id="2b34b-112">Getting Started</span></span>

<span data-ttu-id="2b34b-113">使用 hello 上述範例中，您將無法 toocreate 支援要求您為資源如果您已由 hello 訂用帳戶擁有者指派自訂 RBAC 角色 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2b34b-113">Using hello example above, you would be able toocreate a support request for your resource if you were assigned a custom RBAC role on hello subscription by hello subscription owner.</span></span>
<span data-ttu-id="2b34b-114">[自訂 RBAC 角色](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/)可以使用 Azure PowerShell、 Azure 命令列介面 (CLI) 和 hello REST API 來建立。</span><span class="sxs-lookup"><span data-stu-id="2b34b-114">[Custom RBAC roles](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) can be created using Azure PowerShell, Azure Command-Line Interface (CLI), and hello REST API.</span></span>

<span data-ttu-id="2b34b-115">hello 動作屬性的自訂安全性角色指定 hello Azure 操作 toowhich hello 角色會授與的存取。</span><span class="sxs-lookup"><span data-stu-id="2b34b-115">hello actions property of a custom role specifies hello Azure operations toowhich hello role grants access.</span></span>
<span data-ttu-id="2b34b-116">toocreate 支援要求管理自訂的角色，hello 角色必須擁有 hello 動作 Microsoft.Support/*</span><span class="sxs-lookup"><span data-stu-id="2b34b-116">toocreate a custom role for support request management, hello role must have hello action Microsoft.Support/*</span></span>

<span data-ttu-id="2b34b-117">以下是範例，您可以使用 toocreate 和管理自訂安全性角色的支援要求。</span><span class="sxs-lookup"><span data-stu-id="2b34b-117">Here’s an example of a custom role you can use toocreate and manage support requests.</span></span>
<span data-ttu-id="2b34b-118">我們已經名為 「 支援要求著作人 」 這個角色，且我們 toohello 本文章中的自訂角色的方式。</span><span class="sxs-lookup"><span data-stu-id="2b34b-118">We’ve named this role “Support Request Contributor” and that’s how we refer toohello custom role in this article.</span></span>

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

<span data-ttu-id="2b34b-119">中所述步驟 hello[這段影片](https://www.youtube.com/watch?v=-PaBaDmfwKI)toolearn 如何 toocreate 訂用帳戶自訂安全性角色。</span><span class="sxs-lookup"><span data-stu-id="2b34b-119">Follow hello steps outlined in [this video](https://www.youtube.com/watch?v=-PaBaDmfwKI) toolearn how toocreate a custom role for your subscription.</span></span>

## <a name="create-and-manage-support-requests-in-hello-azure-portal"></a><span data-ttu-id="2b34b-120">建立及管理在 hello Azure 入口網站的支援要求</span><span class="sxs-lookup"><span data-stu-id="2b34b-120">Create and manage support requests in hello Azure portal</span></span>

<span data-ttu-id="2b34b-121">讓我們來看一個範例-您是 hello 擁有者的訂用帳戶 「 Visual Studio MSDN 訂閱。 」</span><span class="sxs-lookup"><span data-stu-id="2b34b-121">Let’s take an example – you are hello owner of Subscription "Visual Studio MSDN Subscription."</span></span>
<span data-ttu-id="2b34b-122">Joe 是您對等的此訂用帳戶中的 hello 資源群組資源擁有者 toosome 並具有讀取權限 toohello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2b34b-122">Joe is your peer who is a resource owner toosome of hello resource groups in this subscription and has read permission toohello subscription.</span></span>
<span data-ttu-id="2b34b-123">您想 toogive 存取 tooyour 等 Joe，hello 能力 toocreate 和管理此訂用帳戶下的 hello 資源的支援票證。</span><span class="sxs-lookup"><span data-stu-id="2b34b-123">You wish toogive access tooyour peer, Joe, hello ability toocreate and manage support tickets for hello resources under this subscription.</span></span>

1. <span data-ttu-id="2b34b-124">hello 第一個步驟是 toogo toohello 訂用帳戶，並在 [設定] 下會看見使用者清單。</span><span class="sxs-lookup"><span data-stu-id="2b34b-124">hello first step is toogo toohello subscription and under "Settings" you see a list of users.</span></span> <span data-ttu-id="2b34b-125">按一下 hello 使用者 Joe 上 hello 訂用帳戶擁有讀取器存取權限，讓我們來指派新的自訂角色 toohim。</span><span class="sxs-lookup"><span data-stu-id="2b34b-125">Click hello user Joe who has reader access on hello Subscription and let’s assign a new custom role toohim.</span></span>

    ![新增角色](./media/create-manage-support-requests-using-access-control/add-role.png)

2. <span data-ttu-id="2b34b-127">按一下 [新增] 底下 hello 「 使用者 」 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2b34b-127">Click "Add" under hello "Users" blade.</span></span> <span data-ttu-id="2b34b-128">從 hello 角色清單中選取 hello 自訂角色 「 支援要求著作人 」</span><span class="sxs-lookup"><span data-stu-id="2b34b-128">Select hello custom role "Support Request Contributor" from hello list of roles</span></span>

    ![新增支援參與者角色](./media/create-manage-support-requests-using-access-control/add-support-contributor-role.png)

3. <span data-ttu-id="2b34b-130">選取之後 hello 角色名稱，請按一下 [加入使用者] 並輸入 hello Joe 的電子郵件憑證。</span><span class="sxs-lookup"><span data-stu-id="2b34b-130">After selecting hello role name, click "Add users" and enter hello Joe's email credentials.</span></span> <span data-ttu-id="2b34b-131">按一下 [選取]</span><span class="sxs-lookup"><span data-stu-id="2b34b-131">Click "Select"</span></span>

    ![新增使用者](./media/create-manage-support-requests-using-access-control/add-users.png)

4. <span data-ttu-id="2b34b-133">按一下 「 確定 」 tooproceed</span><span class="sxs-lookup"><span data-stu-id="2b34b-133">Click "Ok" tooproceed</span></span>

    ![新增存取](./media/create-manage-support-requests-using-access-control/add-access.png)

5. <span data-ttu-id="2b34b-135">現在您會看見 hello 與 hello 新增自訂角色 「 支援要求著作人 」 hello 的 hello 擁有者的訂用帳戶底下的使用者</span><span class="sxs-lookup"><span data-stu-id="2b34b-135">Now you see hello user with hello newly added custom role "Support Request Contributor" under hello Subscription for which you are hello owner</span></span>

    ![新增的使用者](./media/create-manage-support-requests-using-access-control/user-added.png)

    <span data-ttu-id="2b34b-137">Joe 登入時 hello 入口網站，他會看見 hello 訂用帳戶 toowhich 他已加入。</span><span class="sxs-lookup"><span data-stu-id="2b34b-137">When Joe logs in hello portal, he sees hello subscription toowhich he was added.</span></span>

7. <span data-ttu-id="2b34b-138">Joe 從 hello 「 說明及支援 」 刀鋒視窗中按一下 「 新的支援要求 」，而且可以建立支援要求的"Visual Studio Ultimate 與 MSDN"</span><span class="sxs-lookup"><span data-stu-id="2b34b-138">Joe clicks "New Support request" from hello "Help and Support" blade and can create support requests for "Visual Studio Ultimate with MSDN"</span></span>

    ![新增支援要求](./media/create-manage-support-requests-using-access-control/new-support-request.png)

8. <span data-ttu-id="2b34b-140">按一下 「 所有支援的要求 」 Joe 可以檢視針對此訂用帳戶建立支援要求 hello 清單![案例詳細資料檢視](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span><span class="sxs-lookup"><span data-stu-id="2b34b-140">Clicking "All support requests" Joe can see hello list of support requests created for this Subscription  ![Case details view](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span></span>

## <a name="remove-support-request-access-in-hello-azure-portal"></a><span data-ttu-id="2b34b-141">移除 hello Azure 入口網站支援要求的存取權</span><span class="sxs-lookup"><span data-stu-id="2b34b-141">Remove support request access in hello Azure portal</span></span>

<span data-ttu-id="2b34b-142">就如同它是可能 toogrant 存取 tooa 使用者 toocreate 及管理支援要求時，它會使用 hello 使用者也可能 tooremove 存取。</span><span class="sxs-lookup"><span data-stu-id="2b34b-142">Just as it is possible toogrant access tooa user toocreate and manage support requests, it's possible tooremove access for hello user as well.</span></span>
<span data-ttu-id="2b34b-143">tooremove hello 能力 toocreate 和管理的支援要求，請 toohello 訂用帳戶中，按一下 [設定]，按一下 hello 使用者 （在此情況下，是 Joe）。</span><span class="sxs-lookup"><span data-stu-id="2b34b-143">tooremove hello ability toocreate and manage support requests, go toohello Subscription, click "Settings" and click hello user (in this case, Joe).</span></span>
<span data-ttu-id="2b34b-144">以滑鼠右鍵按一下 「 支援要求著作人 」 hello 角色名稱，然後按一下 [移除]</span><span class="sxs-lookup"><span data-stu-id="2b34b-144">Right-click hello role name, "Support Request Contributor" and click "Remove"</span></span>

![移除支援要求存取權](./media/create-manage-support-requests-using-access-control/remove-support-request-access.png)

<span data-ttu-id="2b34b-146">當 Joe 登入 toohello 入口網站，並嘗試 toocreate 支援要求時，他會遇到下列錯誤 hello</span><span class="sxs-lookup"><span data-stu-id="2b34b-146">When Joe logs in toohello portal and tries toocreate a support request, he encounters hello following error</span></span>

![訂用帳戶錯誤-2](./media/create-manage-support-requests-using-access-control/subscription-error-2.png)

<span data-ttu-id="2b34b-148">當 Joe 按一下 [所有支援要求] 時，他不會看到任何支援要求</span><span class="sxs-lookup"><span data-stu-id="2b34b-148">Joe cannot see any support requests when he clicks "All support requests"</span></span>

![案例詳細資料檢視-2](./media/create-manage-support-requests-using-access-control/case-details-view-2.png)
