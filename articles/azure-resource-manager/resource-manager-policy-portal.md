---
title: "資源原則的 aaaAzure 入口網站 |Microsoft 文件"
description: "描述如何 toouse Azure 入口網站 toocreate 和管理資源管理員原則。 原則可以套用在 hello 訂用帳戶或資源群組。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: tomfitz
ms.openlocfilehash: ce6413386317e532b63761a24458b85c996af4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-tooassign-and-manage-resource-policies"></a><span data-ttu-id="5a882-104">使用 Azure 入口網站 tooassign 和管理資源原則</span><span class="sxs-lookup"><span data-stu-id="5a882-104">Use Azure portal tooassign and manage resource policies</span></span>
<span data-ttu-id="5a882-105">hello Azure 入口網站可讓您 tooassign 資源原則 tooresource 群組和訂閱。</span><span class="sxs-lookup"><span data-stu-id="5a882-105">hello Azure portal enables you tooassign resource policies tooresource groups and subscriptions.</span></span> <span data-ttu-id="5a882-106">hello 使用者介面可讓您輕鬆 tooselect hello 原則 tooassign，並指定該原則 toocustomize hello 原則設定的參數值。</span><span class="sxs-lookup"><span data-stu-id="5a882-106">hello user interface makes it easy tooselect hello policy that you want tooassign, and specify parameter values for that policy toocustomize hello policy settings.</span></span> 

<span data-ttu-id="5a882-107">tooassign 透過 hello 入口網站的原則，hello 原則定義必須存在於訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5a882-107">tooassign a policy through hello portal, hello policy definition must already exist in your subscription.</span></span> <span data-ttu-id="5a882-108">您的訂用帳戶已準備好讓您 tooassign tooresource 群組或訂用帳戶的數個內建的原則定義。</span><span class="sxs-lookup"><span data-stu-id="5a882-108">Your subscription has several built-in policy definitions that are ready for you tooassign tooresource groups or subscriptions.</span></span> <span data-ttu-id="5a882-109">您會看到這些內建的原則和任何使用 hello 入口 tooassign 原則時，您已定義的自訂原則。</span><span class="sxs-lookup"><span data-stu-id="5a882-109">You see these built-in policies and any custom policies you have defined when using hello portal tooassign policies.</span></span> <span data-ttu-id="5a882-110">簡介 toopolicies 及 toodefine 自訂原則的方式，請參閱[資源原則概觀](resource-manager-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="5a882-110">For an introduction toopolicies and how toodefine customized policy, see [Resource policy overview](resource-manager-policy.md).</span></span>

<span data-ttu-id="5a882-111">原則會由所有子資源繼承。</span><span class="sxs-lookup"><span data-stu-id="5a882-111">Policies are inherited by all child resources.</span></span> <span data-ttu-id="5a882-112">因此，如果原則已套用的 tooa 資源群組，則該資源群組中的適用 tooall hello 資源。</span><span class="sxs-lookup"><span data-stu-id="5a882-112">So, if a policy is applied tooa resource group, it is applicable tooall hello resources in that resource group.</span></span> <span data-ttu-id="5a882-113">在本文中 hello 詞彙**範圍**參考 toohello 資源群組或指派 hello 原則的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5a882-113">In this article, hello term **scope** refers toohello resource group or subscription that is assigned hello policy.</span></span> 

<span data-ttu-id="5a882-114">建立和更新資源 (PUT 和 PATCH 作業) 時，會評估原則。</span><span class="sxs-lookup"><span data-stu-id="5a882-114">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

## <a name="assign-a-policy"></a><span data-ttu-id="5a882-115">指派原則</span><span class="sxs-lookup"><span data-stu-id="5a882-115">Assign a policy</span></span>

1. <span data-ttu-id="5a882-116">tooassign 原則 tooeither 資源群組或訂用帳戶，請選取該資源群組或訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5a882-116">tooassign a policy tooeither a resource group or subscription, select that resource group or subscription.</span></span> <span data-ttu-id="5a882-117">在 hello 設定選取**原則**。</span><span class="sxs-lookup"><span data-stu-id="5a882-117">In hello settings, select **Policies**.</span></span>

   ![選取原則](./media/resource-manager-policy-portal/select-policies.png)

2. <span data-ttu-id="5a882-119">toocreate 原則指派為此範圍中，選取**加入指派**。</span><span class="sxs-lookup"><span data-stu-id="5a882-119">toocreate a policy assignment for this scope, select **Add assignment**.</span></span>

   ![新增指派](./media/resource-manager-policy-portal/add-assignment.png)

3. <span data-ttu-id="5a882-121">選取您想要 tooassign hello 原則。</span><span class="sxs-lookup"><span data-stu-id="5a882-121">Select hello policy you want tooassign.</span></span> <span data-ttu-id="5a882-122">即使您尚未加入任何原則定義 tooyour 訂用帳戶，您會看到 hello 內建原則，可供指派。</span><span class="sxs-lookup"><span data-stu-id="5a882-122">Even if you have not added any policy definitions tooyour subscription, you see hello built-in policies that are available for assignment.</span></span> <span data-ttu-id="5a882-123">這些內建原則涵蓋許多常見的案例。</span><span class="sxs-lookup"><span data-stu-id="5a882-123">These built-in policies cover many common scenarios.</span></span>

   ![選取定義](./media/resource-manager-policy-portal/select-definition.png)

4. <span data-ttu-id="5a882-125">選取原則之後, 您會看到 hello 原則的描述，以及該原則的任何參數。</span><span class="sxs-lookup"><span data-stu-id="5a882-125">After selecting a policy, you see a description of hello policy, and any parameters for that policy.</span></span> <span data-ttu-id="5a882-126">例如，hello 下列影像顯示 hello**允許位置**限制 hello 可用位置的 hello 原則而言是必要的參數。</span><span class="sxs-lookup"><span data-stu-id="5a882-126">For example, hello following image shows hello **Allowed locations** parameter, which is required for hello policy that restricts hello available locations.</span></span>

   ![顯示參數](./media/resource-manager-policy-portal/show-parameters.png)

5. <span data-ttu-id="5a882-128">透過 hello 使用者介面中，選取 hello 值 toospecify hello 原則參數 （例如，用於部署的 hello 位置）。</span><span class="sxs-lookup"><span data-stu-id="5a882-128">Through hello user interface, select hello values toospecify for hello policy parameters (such as hello locations that can be used for deployment).</span></span>

   ![選取參數值](./media/resource-manager-policy-portal/select-parameters.png)

6. <span data-ttu-id="5a882-130">提供 hello 其他參數值。</span><span class="sxs-lookup"><span data-stu-id="5a882-130">Provide values for hello other parameters.</span></span> <span data-ttu-id="5a882-131">根據您選取 hello 原則指派要在啟動時的 hello 刀鋒視窗，自動指派 hello 範圍。</span><span class="sxs-lookup"><span data-stu-id="5a882-131">hello scope is automatically assigned based on hello blade you selected when starting hello policy assignment.</span></span> <span data-ttu-id="5a882-132">完成時選取 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="5a882-132">Select **OK** when done.</span></span>

   ![定義參數](./media/resource-manager-policy-portal/define-parameters.png)

  <span data-ttu-id="5a882-134">您已指派 hello 原則 toohello 指定範圍。</span><span class="sxs-lookup"><span data-stu-id="5a882-134">You have assigned hello policy toohello specified scope.</span></span>

## <a name="view-policy-assignments"></a><span data-ttu-id="5a882-135">檢視原則指派</span><span class="sxs-lookup"><span data-stu-id="5a882-135">View policy assignments</span></span>

<span data-ttu-id="5a882-136">在指派原則之後, 您看到它 hello 針對該領域的原則清單中。</span><span class="sxs-lookup"><span data-stu-id="5a882-136">After assigning a policy, you see it in hello list of policies for that scope.</span></span> <span data-ttu-id="5a882-137">hello**詳細資料**索引標籤會顯示 hello 原則指派的摘要。</span><span class="sxs-lookup"><span data-stu-id="5a882-137">hello **Details** tab shows a summary of hello policy assignment.</span></span>

![顯示詳細資料](./media/resource-manager-policy-portal/show-details.png)

<span data-ttu-id="5a882-139">hello**指派規則**索引標籤會顯示 hello JSON hello 原則定義。</span><span class="sxs-lookup"><span data-stu-id="5a882-139">hello **Assignment rule** tab shows hello JSON for hello policy definition.</span></span>

![顯示指派規則](./media/resource-manager-policy-portal/show-assignment-rule.png)

## <a name="change-an-existing-policy-assignment"></a><span data-ttu-id="5a882-141">變更現有的原則指派</span><span class="sxs-lookup"><span data-stu-id="5a882-141">Change an existing policy assignment</span></span>

<span data-ttu-id="5a882-142">toochange 原則，選取**編輯指派**或**刪除**</span><span class="sxs-lookup"><span data-stu-id="5a882-142">toochange a policy, select **Edit assignment** or **Delete**</span></span>

![編輯或刪除指派](./media/resource-manager-policy-portal/edit-delete-policy.png)

## <a name="assign-custom-policies"></a><span data-ttu-id="5a882-144">指派自訂的原則</span><span class="sxs-lookup"><span data-stu-id="5a882-144">Assign custom policies</span></span>

<span data-ttu-id="5a882-145">如果您已經在您的訂用帳戶中定義的自訂原則，這些原則是透過 hello 入口網站指派的可用。</span><span class="sxs-lookup"><span data-stu-id="5a882-145">If you have defined custom policies in your subscription, those policies are available for assignment through hello portal.</span></span> <span data-ttu-id="5a882-146">這些原則前面會加上 [自訂]</span><span class="sxs-lookup"><span data-stu-id="5a882-146">Those policies are prefaced with **[Custom]**</span></span>

![自訂原則](./media/resource-manager-policy-portal/show-custom-policy.png)

## <a name="next-steps"></a><span data-ttu-id="5a882-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5a882-148">Next steps</span></span>
* <span data-ttu-id="5a882-149">toolearn 有關 hello JSON 語法定義原則，請參閱[資源原則概觀](resource-manager-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="5a882-149">toolearn about hello JSON syntax for defining policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="5a882-150">如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="5a882-150">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="5a882-151">發行位置 hello 原則結構描述是在[http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json)。</span><span class="sxs-lookup"><span data-stu-id="5a882-151">hello policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

