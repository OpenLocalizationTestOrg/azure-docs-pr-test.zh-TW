---
title: "資源原則的 Azure 入口網站 | Microsoft Docs"
description: "描述如何使用 Azure 入口網站來建立和管理 Resource Manager 原則。 原則可以套用在訂用帳戶或資源群組。"
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
ms.openlocfilehash: 868b2cc1559053057d17b34c03e2e31347f399bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-portal-to-assign-and-manage-resource-policies"></a><span data-ttu-id="99db0-104">使用 Azure 入口網站來指派和管理資源原則</span><span class="sxs-lookup"><span data-stu-id="99db0-104">Use Azure portal to assign and manage resource policies</span></span>
<span data-ttu-id="99db0-105">Azure 入口網站可讓您將資源原則指派給資源群組和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="99db0-105">The Azure portal enables you to assign resource policies to resource groups and subscriptions.</span></span> <span data-ttu-id="99db0-106">使用者介面可讓您輕鬆地選取您想要指派的原則，並指定該原則的參數值來自訂原則設定。</span><span class="sxs-lookup"><span data-stu-id="99db0-106">The user interface makes it easy to select the policy that you want to assign, and specify parameter values for that policy to customize the policy settings.</span></span> 

<span data-ttu-id="99db0-107">若要透過入口網站指派原則，您的訂用帳戶必須已有原則定義。</span><span class="sxs-lookup"><span data-stu-id="99db0-107">To assign a policy through the portal, the policy definition must already exist in your subscription.</span></span> <span data-ttu-id="99db0-108">您的訂用帳戶有數個內建的原則定義，準備好讓您指派給資源群組或訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="99db0-108">Your subscription has several built-in policy definitions that are ready for you to assign to resource groups or subscriptions.</span></span> <span data-ttu-id="99db0-109">當您使用入口網站指派原則時，會看到這些內建的原則，以及您已定義的任何自訂原則。</span><span class="sxs-lookup"><span data-stu-id="99db0-109">You see these built-in policies and any custom policies you have defined when using the portal to assign policies.</span></span> <span data-ttu-id="99db0-110">如需原則簡介及定義自訂原則的方式，請參閱[資源原則概觀](resource-manager-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="99db0-110">For an introduction to policies and how to define customized policy, see [Resource policy overview](resource-manager-policy.md).</span></span>

<span data-ttu-id="99db0-111">原則會由所有子資源繼承。</span><span class="sxs-lookup"><span data-stu-id="99db0-111">Policies are inherited by all child resources.</span></span> <span data-ttu-id="99db0-112">所以，如果原則套用至資源群組，它會適用於該資源群組中的所有資源。</span><span class="sxs-lookup"><span data-stu-id="99db0-112">So, if a policy is applied to a resource group, it is applicable to all the resources in that resource group.</span></span> <span data-ttu-id="99db0-113">在本文中，**範圍**這個詞彙指的是已指派原則的資源群組或訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="99db0-113">In this article, the term **scope** refers to the resource group or subscription that is assigned the policy.</span></span> 

<span data-ttu-id="99db0-114">建立和更新資源 (PUT 和 PATCH 作業) 時，會評估原則。</span><span class="sxs-lookup"><span data-stu-id="99db0-114">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

## <a name="assign-a-policy"></a><span data-ttu-id="99db0-115">指派原則</span><span class="sxs-lookup"><span data-stu-id="99db0-115">Assign a policy</span></span>

1. <span data-ttu-id="99db0-116">若要將原則指派給資源群組或訂用帳戶，請選取該資源群組或訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="99db0-116">To assign a policy to either a resource group or subscription, select that resource group or subscription.</span></span> <span data-ttu-id="99db0-117">在設定中，選取 [原則]。</span><span class="sxs-lookup"><span data-stu-id="99db0-117">In the settings, select **Policies**.</span></span>

   ![選取原則](./media/resource-manager-policy-portal/select-policies.png)

2. <span data-ttu-id="99db0-119">若要建立此範圍的原則指派，請選取 [新增指派]。</span><span class="sxs-lookup"><span data-stu-id="99db0-119">To create a policy assignment for this scope, select **Add assignment**.</span></span>

   ![新增指派](./media/resource-manager-policy-portal/add-assignment.png)

3. <span data-ttu-id="99db0-121">選取您想要指派的原則。</span><span class="sxs-lookup"><span data-stu-id="99db0-121">Select the policy you want to assign.</span></span> <span data-ttu-id="99db0-122">即使您尚未將任何原則定義新增至您的訂用帳戶，仍會看到適用於指派的內建原則。</span><span class="sxs-lookup"><span data-stu-id="99db0-122">Even if you have not added any policy definitions to your subscription, you see the built-in policies that are available for assignment.</span></span> <span data-ttu-id="99db0-123">這些內建原則涵蓋許多常見的案例。</span><span class="sxs-lookup"><span data-stu-id="99db0-123">These built-in policies cover many common scenarios.</span></span>

   ![選取定義](./media/resource-manager-policy-portal/select-definition.png)

4. <span data-ttu-id="99db0-125">選取原則之後，您會看到原則的描述，以及該原則的所有參數。</span><span class="sxs-lookup"><span data-stu-id="99db0-125">After selecting a policy, you see a description of the policy, and any parameters for that policy.</span></span> <span data-ttu-id="99db0-126">例如，下圖顯示的 **Allowed locations** 參數是限制可用位置之原則的必要項目。</span><span class="sxs-lookup"><span data-stu-id="99db0-126">For example, the following image shows the **Allowed locations** parameter, which is required for the policy that restricts the available locations.</span></span>

   ![顯示參數](./media/resource-manager-policy-portal/show-parameters.png)

5. <span data-ttu-id="99db0-128">透過使用者介面，選取要針對原則參數指定的值 (例如可用於部署的位置)。</span><span class="sxs-lookup"><span data-stu-id="99db0-128">Through the user interface, select the values to specify for the policy parameters (such as the locations that can be used for deployment).</span></span>

   ![選取參數值](./media/resource-manager-policy-portal/select-parameters.png)

6. <span data-ttu-id="99db0-130">提供其他參數的值。</span><span class="sxs-lookup"><span data-stu-id="99db0-130">Provide values for the other parameters.</span></span> <span data-ttu-id="99db0-131">會根據您在啟動原則指派時選取的刀鋒視窗，自動將範圍進行指派。</span><span class="sxs-lookup"><span data-stu-id="99db0-131">The scope is automatically assigned based on the blade you selected when starting the policy assignment.</span></span> <span data-ttu-id="99db0-132">完成時選取 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="99db0-132">Select **OK** when done.</span></span>

   ![定義參數](./media/resource-manager-policy-portal/define-parameters.png)

  <span data-ttu-id="99db0-134">您已將原則指派至指定的範圍。</span><span class="sxs-lookup"><span data-stu-id="99db0-134">You have assigned the policy to the specified scope.</span></span>

## <a name="view-policy-assignments"></a><span data-ttu-id="99db0-135">檢視原則指派</span><span class="sxs-lookup"><span data-stu-id="99db0-135">View policy assignments</span></span>

<span data-ttu-id="99db0-136">將原則指派之後，您會在該範圍的原則清單中看見它。</span><span class="sxs-lookup"><span data-stu-id="99db0-136">After assigning a policy, you see it in the list of policies for that scope.</span></span> <span data-ttu-id="99db0-137">[詳細資料] 索引標籤會顯示原則指派的摘要。</span><span class="sxs-lookup"><span data-stu-id="99db0-137">The **Details** tab shows a summary of the policy assignment.</span></span>

![顯示詳細資料](./media/resource-manager-policy-portal/show-details.png)

<span data-ttu-id="99db0-139">[指派規則] 索引標籤會顯示原則定義的 JSON。</span><span class="sxs-lookup"><span data-stu-id="99db0-139">The **Assignment rule** tab shows the JSON for the policy definition.</span></span>

![顯示指派規則](./media/resource-manager-policy-portal/show-assignment-rule.png)

## <a name="change-an-existing-policy-assignment"></a><span data-ttu-id="99db0-141">變更現有的原則指派</span><span class="sxs-lookup"><span data-stu-id="99db0-141">Change an existing policy assignment</span></span>

<span data-ttu-id="99db0-142">若要變更原則，請選取 [編輯指派] 或 [刪除]</span><span class="sxs-lookup"><span data-stu-id="99db0-142">To change a policy, select **Edit assignment** or **Delete**</span></span>

![編輯或刪除指派](./media/resource-manager-policy-portal/edit-delete-policy.png)

## <a name="assign-custom-policies"></a><span data-ttu-id="99db0-144">指派自訂的原則</span><span class="sxs-lookup"><span data-stu-id="99db0-144">Assign custom policies</span></span>

<span data-ttu-id="99db0-145">如果您已在訂用帳戶中定義自訂原則，這些原則都可透過入口網站進行指派。</span><span class="sxs-lookup"><span data-stu-id="99db0-145">If you have defined custom policies in your subscription, those policies are available for assignment through the portal.</span></span> <span data-ttu-id="99db0-146">這些原則前面會加上 [自訂]</span><span class="sxs-lookup"><span data-stu-id="99db0-146">Those policies are prefaced with **[Custom]**</span></span>

![自訂原則](./media/resource-manager-policy-portal/show-custom-policy.png)

## <a name="next-steps"></a><span data-ttu-id="99db0-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="99db0-148">Next steps</span></span>
* <span data-ttu-id="99db0-149">若要深入了解定義原則的 JSON 語法，請參閱[資源原則概觀](resource-manager-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="99db0-149">To learn about the JSON syntax for defining policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="99db0-150">如需關於企業如何使用 Resource Manager 有效地管理訂閱的指引，請參閱 [Azure 企業 Scaffold - 規定的訂用帳戶治理](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="99db0-150">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="99db0-151">原則結構描述會發佈於 [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json)。</span><span class="sxs-lookup"><span data-stu-id="99db0-151">The policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

