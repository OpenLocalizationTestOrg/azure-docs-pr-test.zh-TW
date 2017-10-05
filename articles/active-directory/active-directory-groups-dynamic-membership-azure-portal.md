---
title: "Azure Active Directory 中以屬性為基礎的動態群組成員資格 | Microsoft Docs"
description: "如何建立動態群組成員資格的進階規則，包括支援的運算式規則運算子和參數。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: fb434cc2-9a91-4ebf-9753-dd81e289787e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f4d9a08551d616ff98bc8734cbeec01d6e0d04ca
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-attribute-based-rules-for-dynamic-group-membership-in-azure-active-directory"></a><span data-ttu-id="5975f-103">在 Azure Active Directory 中針對動態群組成員資格建立以屬性為基礎的規則</span><span class="sxs-lookup"><span data-stu-id="5975f-103">Create attribute-based rules for dynamic group membership in Azure Active Directory</span></span>
<span data-ttu-id="5975f-104">在 Azure Active Directory (Azure AD) 中，您可以建立進階規則，以對群組啟用更複雜的屬性型動態成員資格。</span><span class="sxs-lookup"><span data-stu-id="5975f-104">In Azure Active Directory (Azure AD), you can create advanced rules to enable complex attribute-based dynamic memberships for groups.</span></span> <span data-ttu-id="5975f-105">本文將詳細說明用以建立適用於使用者或裝置之動態成員資格規則的屬性和語法。</span><span class="sxs-lookup"><span data-stu-id="5975f-105">This article details the attributes and syntax to create dynamic membership rules for users or devices.</span></span>

<span data-ttu-id="5975f-106">當使用者或裝置的任何屬性變更時，系統會評估目錄中的所有動態群組規則，以查看變更是否會觸發任何的群組新增或移除。</span><span class="sxs-lookup"><span data-stu-id="5975f-106">When any attributes of a user or device change, the system evaluates all dynamic group rules in a directory to see if the change would trigger any group adds or removes.</span></span> <span data-ttu-id="5975f-107">如果使用者或裝置滿足群組上的規則，就會將他們新增為該群組的成員。</span><span class="sxs-lookup"><span data-stu-id="5975f-107">If a user or device satisfies a rule on a group, they are added as a member of that group.</span></span> <span data-ttu-id="5975f-108">如果他們不再符合此規則，則會予以移除。</span><span class="sxs-lookup"><span data-stu-id="5975f-108">If they no longer satisfy the rule, they are removed.</span></span>

> [!NOTE]
> - <span data-ttu-id="5975f-109">您可以為安全性群組或 Office 365 群組的動態成員資格設定規則。</span><span class="sxs-lookup"><span data-stu-id="5975f-109">You can set up a rule for dynamic membership on security groups or Office 365 groups.</span></span>
>
> - <span data-ttu-id="5975f-110">此功能要求新增到至少一個動態群組的每個使用者成員都具有 Azure AD Premium P1 授權。</span><span class="sxs-lookup"><span data-stu-id="5975f-110">This feature requires an Azure AD Premium P1 license for each user member added to at least one dynamic group.</span></span>
>
> - <span data-ttu-id="5975f-111">您可以為裝置或使用者建立動態群組，但無法建立同時包含使用者和裝置物件的規則。</span><span class="sxs-lookup"><span data-stu-id="5975f-111">You can create a dynamic group for devices or users, but you cannot create a rule that contains both user and device objects.</span></span>

> - <span data-ttu-id="5975f-112">目前無法依據擁有使用者的屬性建立裝置群組。</span><span class="sxs-lookup"><span data-stu-id="5975f-112">At the moment it is not possible to create a device group based on owning user's attributes.</span></span> <span data-ttu-id="5975f-113">裝置成員資格規則只能參考目錄中裝置物件的直接屬性。</span><span class="sxs-lookup"><span data-stu-id="5975f-113">Device membership rules can only reference immediate attributes of device objects in the directory.</span></span>

## <a name="to-create-an-advanced-rule"></a><span data-ttu-id="5975f-114">建立進階規則</span><span class="sxs-lookup"><span data-stu-id="5975f-114">To create an advanced rule</span></span>
1. <span data-ttu-id="5975f-115">使用具備全域管理員或使用者帳戶管理員身分的帳戶來登入 [Azure AD 系統管理中心](https://aad.portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="5975f-115">Sign in to the [Azure AD admin center](https://aad.portal.azure.com) with an account that is a global administrator or a user account administrator.</span></span>
2. <span data-ttu-id="5975f-116">選取 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="5975f-116">Select **Users and groups**.</span></span>
3. <span data-ttu-id="5975f-117">選取 [所有群組]。</span><span class="sxs-lookup"><span data-stu-id="5975f-117">Select **All groups**.</span></span>

   ![開啟群組刀鋒視窗](./media/active-directory-groups-dynamic-membership-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="5975f-119">在 [所有群組] 中，選取 [新增群組]。</span><span class="sxs-lookup"><span data-stu-id="5975f-119">In **All groups**, select **New group**.</span></span>

   ![Add new group](./media/active-directory-groups-dynamic-membership-azure-portal/add-group-type.png)
5. <span data-ttu-id="5975f-121">在 [群組]  刀鋒視窗上，輸入新群組的名稱和描述。</span><span class="sxs-lookup"><span data-stu-id="5975f-121">On the **Group** blade, enter a name and description for the new group.</span></span> <span data-ttu-id="5975f-122">依據您是要為使用者還是裝置建立規則，在 [成員資格類型] 選取 [動態使用者] 或 [動態裝置]，然後選取 [新增動態查詢]。</span><span class="sxs-lookup"><span data-stu-id="5975f-122">Select a **Membership type** of either **Dynamic User** or **Dynamic Device**, depending on whether you want to create a rule for users or devices, and then select **Add dynamic query**.</span></span> <span data-ttu-id="5975f-123">如需了解有哪些用於裝置規則的屬性，請參閱 [使用屬性來建立裝置物件的規則](#using-attributes-to-create-rules-for-device-objects)。</span><span class="sxs-lookup"><span data-stu-id="5975f-123">For the attributes used for device rules, see [Using attributes to create rules for device objects](#using-attributes-to-create-rules-for-device-objects).</span></span>

   ![新增動態成員資格規則](./media/active-directory-groups-dynamic-membership-azure-portal/add-dynamic-group-rule.png)
6. <span data-ttu-id="5975f-125">在 [動態成員資格規則] 刀鋒視窗上，於 [新增動態成員資格進階規則] 方塊中輸入您的規則、按 Enter，然後選取刀鋒視窗底部的 [建立]。</span><span class="sxs-lookup"><span data-stu-id="5975f-125">On the **Dynamic membership rules** blade, enter your rule into the **Add dynamic membership advanced rule** box, press Enter, and then select **Create** at the bottom of the blade.</span></span>
7. <span data-ttu-id="5975f-126">選取 [更多服務]  on the  來建立群組。</span><span class="sxs-lookup"><span data-stu-id="5975f-126">Select **Create** on the **Group** blade to create the group.</span></span>

## <a name="constructing-the-body-of-an-advanced-rule"></a><span data-ttu-id="5975f-127">建構進階規則的主體</span><span class="sxs-lookup"><span data-stu-id="5975f-127">Constructing the body of an advanced rule</span></span>
<span data-ttu-id="5975f-128">您可以為群組的動態成員資格建立的進階規則基本上是一個二進位運算式，其中包含三個部分，且會產生 true 或 false 的結果。</span><span class="sxs-lookup"><span data-stu-id="5975f-128">The advanced rule that you can create for the dynamic memberships for groups is essentially a binary expression that consists of three parts and results in a true or false outcome.</span></span> <span data-ttu-id="5975f-129">這三個部分包括：</span><span class="sxs-lookup"><span data-stu-id="5975f-129">The three parts are:</span></span>

* <span data-ttu-id="5975f-130">左側的參數</span><span class="sxs-lookup"><span data-stu-id="5975f-130">Left parameter</span></span>
* <span data-ttu-id="5975f-131">二進位運算子</span><span class="sxs-lookup"><span data-stu-id="5975f-131">Binary operator</span></span>
* <span data-ttu-id="5975f-132">右側的常數</span><span class="sxs-lookup"><span data-stu-id="5975f-132">Right constant</span></span>

<span data-ttu-id="5975f-133">完整的進階規則外觀如下：(leftParameter binaryOperator "RightConstant")，其中可選擇性地使用左右括號來括住整個二進位運算式，也可以選擇性地使用雙引號、只有在其為字串時需要括住右側常數，且左側參數的語法是 user.property。</span><span class="sxs-lookup"><span data-stu-id="5975f-133">A complete advanced rule looks similar to this: (leftParameter binaryOperator "RightConstant"), where the opening and closing parenthesis are optional for the entire binary expression, double quotes are optional as well, only required for the right constant when it is string, and the syntax for the left parameter is user.property.</span></span> <span data-ttu-id="5975f-134">進階規則可以包含多個二進位運算式，並以 -and、 -or 和 -not 邏輯運算子分隔。</span><span class="sxs-lookup"><span data-stu-id="5975f-134">An advanced rule can consist of more than one binary expressions separated by the -and, -or, and -not logical operators.</span></span>

<span data-ttu-id="5975f-135">以下是正確建構的進階規則的範例：</span><span class="sxs-lookup"><span data-stu-id="5975f-135">The following are examples of a properly constructed advanced rule:</span></span>
```
(user.department -eq "Sales") -or (user.department -eq "Marketing")
(user.department -eq "Sales") -and -not (user.jobTitle -contains "SDE")
```
<span data-ttu-id="5975f-136">如需支援的參數和運算式規則運算子的完整清單，請參閱下列各節。</span><span class="sxs-lookup"><span data-stu-id="5975f-136">For the complete list of supported parameters and expression rule operators, see sections below.</span></span> <span data-ttu-id="5975f-137">如需了解有哪些用於裝置規則的屬性，請參閱 [使用屬性來建立裝置物件的規則](#using-attributes-to-create-rules-for-device-objects)。</span><span class="sxs-lookup"><span data-stu-id="5975f-137">For the attributes used for device rules, see [Using attributes to create rules for device objects](#using-attributes-to-create-rules-for-device-objects).</span></span>

<span data-ttu-id="5975f-138">進階規則主體的總長度不得超過 2048 個字元。</span><span class="sxs-lookup"><span data-stu-id="5975f-138">The total length of the body of your advanced rule cannot exceed 2048 characters.</span></span>

> [!NOTE]
> <span data-ttu-id="5975f-139">字串和 regex 運算都不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="5975f-139">String and regex operations are not case sensitive.</span></span> <span data-ttu-id="5975f-140">您也可以使用 $null 做為常數，執行 Null 檢查，例如，user.department-eq $null。</span><span class="sxs-lookup"><span data-stu-id="5975f-140">You can also perform Null checks, using $null as a constant, for example, user.department -eq $null.</span></span>
> <span data-ttu-id="5975f-141">包含引號 " 的字串應該使用 ' 字元逸出，例如 user.department -eq \\`"Sales"。</span><span class="sxs-lookup"><span data-stu-id="5975f-141">Strings containing quotes " should be escaped using 'character, for example, user.department -eq \\`"Sales".</span></span>

## <a name="supported-expression-rule-operators"></a><span data-ttu-id="5975f-142">支援的運算式規則運算子</span><span class="sxs-lookup"><span data-stu-id="5975f-142">Supported expression rule operators</span></span>
<span data-ttu-id="5975f-143">下表列出所有支援的運算式規則運算子及其用於進階規則主體中的語法：</span><span class="sxs-lookup"><span data-stu-id="5975f-143">The following table lists all the supported expression rule operators and their syntax to be used in the body of the advanced rule:</span></span>

| <span data-ttu-id="5975f-144">運算子</span><span class="sxs-lookup"><span data-stu-id="5975f-144">Operator</span></span> | <span data-ttu-id="5975f-145">語法</span><span class="sxs-lookup"><span data-stu-id="5975f-145">Syntax</span></span> |
| --- | --- |
| <span data-ttu-id="5975f-146">Not Equals</span><span class="sxs-lookup"><span data-stu-id="5975f-146">Not Equals</span></span> |<span data-ttu-id="5975f-147">-ne</span><span class="sxs-lookup"><span data-stu-id="5975f-147">-ne</span></span> |
| <span data-ttu-id="5975f-148">Equals</span><span class="sxs-lookup"><span data-stu-id="5975f-148">Equals</span></span> |<span data-ttu-id="5975f-149">-eq</span><span class="sxs-lookup"><span data-stu-id="5975f-149">-eq</span></span> |
| <span data-ttu-id="5975f-150">Not Starts With</span><span class="sxs-lookup"><span data-stu-id="5975f-150">Not Starts With</span></span> |<span data-ttu-id="5975f-151">-notStartsWith</span><span class="sxs-lookup"><span data-stu-id="5975f-151">-notStartsWith</span></span> |
| <span data-ttu-id="5975f-152">開頭為</span><span class="sxs-lookup"><span data-stu-id="5975f-152">Starts With</span></span> |<span data-ttu-id="5975f-153">-startsWith</span><span class="sxs-lookup"><span data-stu-id="5975f-153">-startsWith</span></span> |
| <span data-ttu-id="5975f-154">Not Contains</span><span class="sxs-lookup"><span data-stu-id="5975f-154">Not Contains</span></span> |<span data-ttu-id="5975f-155">-notContains</span><span class="sxs-lookup"><span data-stu-id="5975f-155">-notContains</span></span> |
| <span data-ttu-id="5975f-156">Contains</span><span class="sxs-lookup"><span data-stu-id="5975f-156">Contains</span></span> |<span data-ttu-id="5975f-157">-contains</span><span class="sxs-lookup"><span data-stu-id="5975f-157">-contains</span></span> |
| <span data-ttu-id="5975f-158">Not Match</span><span class="sxs-lookup"><span data-stu-id="5975f-158">Not Match</span></span> |<span data-ttu-id="5975f-159">-notMatch</span><span class="sxs-lookup"><span data-stu-id="5975f-159">-notMatch</span></span> |
| <span data-ttu-id="5975f-160">Match</span><span class="sxs-lookup"><span data-stu-id="5975f-160">Match</span></span> |<span data-ttu-id="5975f-161">-match</span><span class="sxs-lookup"><span data-stu-id="5975f-161">-match</span></span> |
| <span data-ttu-id="5975f-162">在</span><span class="sxs-lookup"><span data-stu-id="5975f-162">In</span></span> | <span data-ttu-id="5975f-163">-in</span><span class="sxs-lookup"><span data-stu-id="5975f-163">-in</span></span> |
| <span data-ttu-id="5975f-164">不在</span><span class="sxs-lookup"><span data-stu-id="5975f-164">Not In</span></span> | <span data-ttu-id="5975f-165">-notIn</span><span class="sxs-lookup"><span data-stu-id="5975f-165">-notIn</span></span> |

## <a name="operator-precedence"></a><span data-ttu-id="5975f-166">運算子優先順序</span><span class="sxs-lookup"><span data-stu-id="5975f-166">Operator precedence</span></span>

<span data-ttu-id="5975f-167">所有運算子都會列在下面 (由高至低排定優先順序)。</span><span class="sxs-lookup"><span data-stu-id="5975f-167">All Operators are listed below per precedence from lower to higher.</span></span> <span data-ttu-id="5975f-168">同一行上運算子的優先順序相等：</span><span class="sxs-lookup"><span data-stu-id="5975f-168">Operators on same line are in equal precedence:</span></span>
````
-any -all
-or
-and
-not
-eq -ne -startsWith -notStartsWith -contains -notContains -match –notMatch -in -notIn
````
<span data-ttu-id="5975f-169">不管有沒有連字號前置詞，均可使用所有運算子。</span><span class="sxs-lookup"><span data-stu-id="5975f-169">All operators can be used with or without the hyphen prefix.</span></span> <span data-ttu-id="5975f-170">優先順序不符合您的需求時，才需要括號。</span><span class="sxs-lookup"><span data-stu-id="5975f-170">Parentheses are needed only when precedence does not meet your requirements.</span></span>
<span data-ttu-id="5975f-171">例如：</span><span class="sxs-lookup"><span data-stu-id="5975f-171">For example:</span></span>
```
   user.department –eq "Marketing" –and user.country –eq "US"
```
<span data-ttu-id="5975f-172">相當於：</span><span class="sxs-lookup"><span data-stu-id="5975f-172">is equivalent to:</span></span>
```
   (user.department –eq "Marketing") –and (user.country –eq "US")
```
## <a name="using-the--in-and--notin-operators"></a><span data-ttu-id="5975f-173">使用 -In 和 -notIn 運算子</span><span class="sxs-lookup"><span data-stu-id="5975f-173">Using the -In and -notIn operators</span></span>

<span data-ttu-id="5975f-174">如果您想要針對許多不同的值比較使用者屬性的值，您可以使用 -In 或 -notIn 運算子。</span><span class="sxs-lookup"><span data-stu-id="5975f-174">If you want to compare the value of a user attribute against a number of different values you can use the -In or -notIn operators.</span></span> <span data-ttu-id="5975f-175">使用 -In 運算子的範例如下︰</span><span class="sxs-lookup"><span data-stu-id="5975f-175">Here is an example using the -In operator:</span></span>
```
    user.department -In [ "50001", "50002", "50003", “50005”, “50006”, “50007”, “50008”, “50016”, “50020”, “50024”, “50038”, “50039”, “51100” ]
```
<span data-ttu-id="5975f-176">請注意值清單的開頭和結尾有使用 "[" 和 "]"。</span><span class="sxs-lookup"><span data-stu-id="5975f-176">Note the use of the "[" and "]" at the beginning and end of the list of values.</span></span> <span data-ttu-id="5975f-177">當 user.department 的值等於清單中的其中一個值時，這個條件會評估為 True。</span><span class="sxs-lookup"><span data-stu-id="5975f-177">This condition evaluates to True of the value of user.department equals one of the values in the list.</span></span>


## <a name="query-error-remediation"></a><span data-ttu-id="5975f-178">查詢錯誤補救</span><span class="sxs-lookup"><span data-stu-id="5975f-178">Query error remediation</span></span>
<span data-ttu-id="5975f-179">下表列出可能的錯誤以及其更正方式</span><span class="sxs-lookup"><span data-stu-id="5975f-179">The following table lists potential errors and how to correct them if they occur</span></span>

| <span data-ttu-id="5975f-180">查詢剖析錯誤</span><span class="sxs-lookup"><span data-stu-id="5975f-180">Query Parse Error</span></span> | <span data-ttu-id="5975f-181">錯誤的使用方式</span><span class="sxs-lookup"><span data-stu-id="5975f-181">Error Usage</span></span> | <span data-ttu-id="5975f-182">更正的使用方式</span><span class="sxs-lookup"><span data-stu-id="5975f-182">Corrected Usage</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5975f-183">錯誤：不支援屬性。</span><span class="sxs-lookup"><span data-stu-id="5975f-183">Error: Attribute not supported.</span></span> |<span data-ttu-id="5975f-184">(user.invalidProperty -eq "Value")</span><span class="sxs-lookup"><span data-stu-id="5975f-184">(user.invalidProperty -eq "Value")</span></span> |<span data-ttu-id="5975f-185">(user.department -eq "value")</span><span class="sxs-lookup"><span data-stu-id="5975f-185">(user.department -eq "value")</span></span><br/><span data-ttu-id="5975f-186">屬性應該符合 [支援的屬性清單](#supported-properties)。</span><span class="sxs-lookup"><span data-stu-id="5975f-186">Property should match one from the [supported properties list](#supported-properties).</span></span> |
| <span data-ttu-id="5975f-187">錯誤：屬性不支援運算子。</span><span class="sxs-lookup"><span data-stu-id="5975f-187">Error: Operator is not supported on attribute.</span></span> |<span data-ttu-id="5975f-188">(user.accountEnabled -contains true)</span><span class="sxs-lookup"><span data-stu-id="5975f-188">(user.accountEnabled -contains true)</span></span> |<span data-ttu-id="5975f-189">(user.accountEnabled -eq true)</span><span class="sxs-lookup"><span data-stu-id="5975f-189">(user.accountEnabled -eq true)</span></span><br/><span data-ttu-id="5975f-190">屬性屬於布林類型。</span><span class="sxs-lookup"><span data-stu-id="5975f-190">Property is of type boolean.</span></span> <span data-ttu-id="5975f-191">使用上述清單中的布林型別支援的運算子 (-eq 或-ne)。</span><span class="sxs-lookup"><span data-stu-id="5975f-191">Use the supported operators (-eq or -ne) on boolean type from the above list.</span></span> |
| <span data-ttu-id="5975f-192">錯誤：查詢編譯錯誤。</span><span class="sxs-lookup"><span data-stu-id="5975f-192">Error: Query compilation error.</span></span> |<span data-ttu-id="5975f-193">(user.department -eq "Sales") -and (user.department -eq "Marketing")(user.userPrincipalName -match "*@domain.ext")</span><span class="sxs-lookup"><span data-stu-id="5975f-193">(user.department -eq "Sales") -and (user.department -eq "Marketing")(user.userPrincipalName -match "*@domain.ext")</span></span> |<span data-ttu-id="5975f-194">(user.department -eq "Sales") -and (user.department -eq "Marketing")</span><span class="sxs-lookup"><span data-stu-id="5975f-194">(user.department -eq "Sales") -and (user.department -eq "Marketing")</span></span><br/><span data-ttu-id="5975f-195">邏輯運算子應該符合上述支援的屬性清單中的一個屬性。(user.userPrincipalName -match ".*@domain.ext") 或 (user.userPrincipalName -match "@domain.ext$") 規則運算式發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="5975f-195">Logical operator should match one from the supported properties list above.(user.userPrincipalName -match ".*@domain.ext")or(user.userPrincipalName -match "@domain.ext$")Error in regular expression.</span></span> |
| <span data-ttu-id="5975f-196">錯誤：二進位運算式不是正確的格式。</span><span class="sxs-lookup"><span data-stu-id="5975f-196">Error: Binary expression is not in right format.</span></span> |<span data-ttu-id="5975f-197">(user.department –eq “Sales”) (user.department -eq "Sales")(user.department-eq"Sales")</span><span class="sxs-lookup"><span data-stu-id="5975f-197">(user.department –eq “Sales”) (user.department -eq "Sales")(user.department-eq"Sales")</span></span> |<span data-ttu-id="5975f-198">(user.accountEnabled -eq true) -and (user.userPrincipalName -contains "alias@domain")</span><span class="sxs-lookup"><span data-stu-id="5975f-198">(user.accountEnabled -eq true) -and (user.userPrincipalName -contains "alias@domain")</span></span><br/><span data-ttu-id="5975f-199">查詢有多個錯誤。</span><span class="sxs-lookup"><span data-stu-id="5975f-199">Query has multiple errors.</span></span> <span data-ttu-id="5975f-200">括號不在正確的位置。</span><span class="sxs-lookup"><span data-stu-id="5975f-200">Parenthesis not in right place.</span></span> |
| <span data-ttu-id="5975f-201">錯誤：設定動態成員資格時發生未知的錯誤。</span><span class="sxs-lookup"><span data-stu-id="5975f-201">Error: Unknown error occurred during setting up dynamic memberships.</span></span> |<span data-ttu-id="5975f-202">(user.accountEnabled -eq "True" AND user.userPrincipalName -contains "alias@domain")</span><span class="sxs-lookup"><span data-stu-id="5975f-202">(user.accountEnabled -eq "True" AND user.userPrincipalName -contains "alias@domain")</span></span> |<span data-ttu-id="5975f-203">(user.accountEnabled -eq true) -and (user.userPrincipalName -contains "alias@domain")</span><span class="sxs-lookup"><span data-stu-id="5975f-203">(user.accountEnabled -eq true) -and (user.userPrincipalName -contains "alias@domain")</span></span><br/><span data-ttu-id="5975f-204">查詢有多個錯誤。</span><span class="sxs-lookup"><span data-stu-id="5975f-204">Query has multiple errors.</span></span> <span data-ttu-id="5975f-205">括號不在正確的位置。</span><span class="sxs-lookup"><span data-stu-id="5975f-205">Parenthesis not in right place.</span></span> |

## <a name="supported-properties"></a><span data-ttu-id="5975f-206">支援的屬性</span><span class="sxs-lookup"><span data-stu-id="5975f-206">Supported properties</span></span>
<span data-ttu-id="5975f-207">以下是您可以在進階規則中使用的所有使用者屬性：</span><span class="sxs-lookup"><span data-stu-id="5975f-207">The following are all the user properties that you can use in your advanced rule:</span></span>

### <a name="properties-of-type-boolean"></a><span data-ttu-id="5975f-208">布林型別的屬性</span><span class="sxs-lookup"><span data-stu-id="5975f-208">Properties of type boolean</span></span>
<span data-ttu-id="5975f-209">允許的運算子</span><span class="sxs-lookup"><span data-stu-id="5975f-209">Allowed operators</span></span>

* <span data-ttu-id="5975f-210">-eq</span><span class="sxs-lookup"><span data-stu-id="5975f-210">-eq</span></span>
* <span data-ttu-id="5975f-211">-ne</span><span class="sxs-lookup"><span data-stu-id="5975f-211">-ne</span></span>

| <span data-ttu-id="5975f-212">屬性</span><span class="sxs-lookup"><span data-stu-id="5975f-212">Properties</span></span> | <span data-ttu-id="5975f-213">允許的值</span><span class="sxs-lookup"><span data-stu-id="5975f-213">Allowed values</span></span> | <span data-ttu-id="5975f-214">使用量</span><span class="sxs-lookup"><span data-stu-id="5975f-214">Usage</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5975f-215">accountEnabled</span><span class="sxs-lookup"><span data-stu-id="5975f-215">accountEnabled</span></span> |<span data-ttu-id="5975f-216">true false</span><span class="sxs-lookup"><span data-stu-id="5975f-216">true false</span></span> |<span data-ttu-id="5975f-217">user.accountEnabled -eq true</span><span class="sxs-lookup"><span data-stu-id="5975f-217">user.accountEnabled -eq true</span></span> |
| <span data-ttu-id="5975f-218">dirSyncEnabled</span><span class="sxs-lookup"><span data-stu-id="5975f-218">dirSyncEnabled</span></span> |<span data-ttu-id="5975f-219">true false</span><span class="sxs-lookup"><span data-stu-id="5975f-219">true false</span></span> |<span data-ttu-id="5975f-220">user.dirSyncEnabled -eq true</span><span class="sxs-lookup"><span data-stu-id="5975f-220">user.dirSyncEnabled -eq true</span></span> |

### <a name="properties-of-type-string"></a><span data-ttu-id="5975f-221">字串類型的屬性</span><span class="sxs-lookup"><span data-stu-id="5975f-221">Properties of type string</span></span>
<span data-ttu-id="5975f-222">允許的運算子</span><span class="sxs-lookup"><span data-stu-id="5975f-222">Allowed operators</span></span>

* <span data-ttu-id="5975f-223">-eq</span><span class="sxs-lookup"><span data-stu-id="5975f-223">-eq</span></span>
* <span data-ttu-id="5975f-224">-ne</span><span class="sxs-lookup"><span data-stu-id="5975f-224">-ne</span></span>
* <span data-ttu-id="5975f-225">-notStartsWith</span><span class="sxs-lookup"><span data-stu-id="5975f-225">-notStartsWith</span></span>
* <span data-ttu-id="5975f-226">-startsWith</span><span class="sxs-lookup"><span data-stu-id="5975f-226">-StartsWith</span></span>
* <span data-ttu-id="5975f-227">-contains</span><span class="sxs-lookup"><span data-stu-id="5975f-227">-contains</span></span>
* <span data-ttu-id="5975f-228">-notContains</span><span class="sxs-lookup"><span data-stu-id="5975f-228">-notContains</span></span>
* <span data-ttu-id="5975f-229">-match</span><span class="sxs-lookup"><span data-stu-id="5975f-229">-match</span></span>
* <span data-ttu-id="5975f-230">-notMatch</span><span class="sxs-lookup"><span data-stu-id="5975f-230">-notMatch</span></span>
* <span data-ttu-id="5975f-231">-in</span><span class="sxs-lookup"><span data-stu-id="5975f-231">-in</span></span>
* <span data-ttu-id="5975f-232">-notIn</span><span class="sxs-lookup"><span data-stu-id="5975f-232">-notIn</span></span>

| <span data-ttu-id="5975f-233">屬性</span><span class="sxs-lookup"><span data-stu-id="5975f-233">Properties</span></span> | <span data-ttu-id="5975f-234">允許的值</span><span class="sxs-lookup"><span data-stu-id="5975f-234">Allowed values</span></span> | <span data-ttu-id="5975f-235">使用量</span><span class="sxs-lookup"><span data-stu-id="5975f-235">Usage</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5975f-236">city</span><span class="sxs-lookup"><span data-stu-id="5975f-236">city</span></span> |<span data-ttu-id="5975f-237">任何字串值或 $null</span><span class="sxs-lookup"><span data-stu-id="5975f-237">Any string value or $null</span></span> |<span data-ttu-id="5975f-238">(user.city -eq "value")</span><span class="sxs-lookup"><span data-stu-id="5975f-238">(user.city -eq "value")</span></span> |
| <span data-ttu-id="5975f-239">country</span><span class="sxs-lookup"><span data-stu-id="5975f-239">country</span></span> |<span data-ttu-id="5975f-240">任何字串值或 $null</span><span class="sxs-lookup"><span data-stu-id="5975f-240">Any string value or $null</span></span> |<span data-ttu-id="5975f-241">(user.country -eq "value")</span><span class="sxs-lookup"><span data-stu-id="5975f-241">(user.country -eq "value")</span></span> |
| <span data-ttu-id="5975f-242">companyName</span><span class="sxs-lookup"><span data-stu-id="5975f-242">companyName</span></span> | <span data-ttu-id="5975f-243">任何字串值或 $null</span><span class="sxs-lookup"><span data-stu-id="5975f-243">Any string value or $null</span></span> | <span data-ttu-id="5975f-244">(user.companyName -eq "value")</span><span class="sxs-lookup"><span data-stu-id="5975f-244">(user.companyName -eq "value")</span></span> |
| <span data-ttu-id="5975f-245">department</span><span class="sxs-lookup"><span data-stu-id="5975f-245">department</span></span> |<span data-ttu-id="5975f-246">任何字串值或 $null</span><span class="sxs-lookup"><span data-stu-id="5975f-246">Any string value or $null</span></span> |<span data-ttu-id="5975f-247">(user.department -eq "value")</span><span class="sxs-lookup"><span data-stu-id="5975f-247">(user.department -eq "value")</span></span> |
| <span data-ttu-id="5975f-248">displayName</span><span class="sxs-lookup"><span data-stu-id="5975f-248">displayName</span></span> |<span data-ttu-id="5975f-249">任何字串值</span><span class="sxs-lookup"><span data-stu-id="5975f-249">Any string value</span></span> |<span data-ttu-id="5975f-250">(user.displayName -eq "value")</span><span class="sxs-lookup"><span data-stu-id="5975f-250">(user.displayName -eq "value")</span></span> |
| <span data-ttu-id="5975f-251">facsimileTelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="5975f-251">facsimileTelephoneNumber</span></span> |<span data-ttu-id="5975f-252">任何字串值或 $null</span><span class="sxs-lookup"><span data-stu-id="5975f-252">Any string value or $null</span></span> |<span data-ttu-id="5975f-253">(user.facsimileTelephoneNumber -eq "value")</span><span class="sxs-lookup"><span data-stu-id="5975f-253">(user.facsimileTelephoneNumber -eq "value")</span></span> |
| <span data-ttu-id="5975f-254">givenName</span><span class="sxs-lookup"><span data-stu-id="5975f-254">givenName</span></span> |<span data-ttu-id="5975f-255">任何字串值或 $null</span><span class="sxs-lookup"><span data-stu-id="5975f-255">Any string value or $null</span></span> |<span data-ttu-id="5975f-256">(user.givenName -eq "value")</span><span class="sxs-lookup"><span data-stu-id="5975f-256">(user.givenName -eq "value")</span></span> |
| <span data-ttu-id="5975f-257">jobTitle</span><span class="sxs-lookup"><span data-stu-id="5975f-257">jobTitle</span></span> |<span data-ttu-id="5975f-258">任何字串值或 $null</span><span class="sxs-lookup"><span data-stu-id="5975f-258">Any string value or $null</span></span> |<span data-ttu-id="5975f-259">(user.jobTitle -eq "value")</span><span class="sxs-lookup"><span data-stu-id="5975f-259">(user.jobTitle -eq "value")</span></span> |
| <span data-ttu-id="5975f-260">mail</span><span class="sxs-lookup"><span data-stu-id="5975f-260">mail</span></span> |<span data-ttu-id="5975f-261">任何字串值或 $null (使用者的 SMTP 位址)</span><span class="sxs-lookup"><span data-stu-id="5975f-261">Any string value or $null (SMTP address of the user)</span></span> |<span data-ttu-id="5975f-262">(user.mail -eq "value")</span><span class="sxs-lookup"><span data-stu-id="5975f-262">(user.mail -eq "value")</span></span> |
| <span data-ttu-id="5975f-263">mailNickName</span><span class="sxs-lookup"><span data-stu-id="5975f-263">mailNickName</span></span> |<span data-ttu-id="5975f-264">任何字串值 (使用者的郵件別名)</span><span class="sxs-lookup"><span data-stu-id="5975f-264">Any string value (mail alias of the user)</span></span> |<span data-ttu-id="5975f-265">(user.mailNickName -eq "value")</span><span class="sxs-lookup"><span data-stu-id="5975f-265">(user.mailNickName -eq "value")</span></span> |
| <span data-ttu-id="5975f-266">mobile</span><span class="sxs-lookup"><span data-stu-id="5975f-266">mobile</span></span> |<span data-ttu-id="5975f-267">任何字串值或 $null</span><span class="sxs-lookup"><span data-stu-id="5975f-267">Any string value or $null</span></span> |<span data-ttu-id="5975f-268">(user.mobile -eq "value")</span><span class="sxs-lookup"><span data-stu-id="5975f-268">(user.mobile -eq "value")</span></span> |
| <span data-ttu-id="5975f-269">objectId</span><span class="sxs-lookup"><span data-stu-id="5975f-269">objectId</span></span> |<span data-ttu-id="5975f-270">使用者物件的 GUID</span><span class="sxs-lookup"><span data-stu-id="5975f-270">GUID of the user object</span></span> |<span data-ttu-id="5975f-271">(user.objectId -eq "1111111-1111-1111-1111-111111111111")</span><span class="sxs-lookup"><span data-stu-id="5975f-271">(user.objectId -eq "1111111-1111-1111-1111-111111111111")</span></span> |
| <span data-ttu-id="5975f-272">onPremisesSecurityIdentifier</span><span class="sxs-lookup"><span data-stu-id="5975f-272">onPremisesSecurityIdentifier</span></span> | <span data-ttu-id="5975f-273">已從內部部署環境同步至雲端之使用者的內部部署安全性識別碼 (SID)。</span><span class="sxs-lookup"><span data-stu-id="5975f-273">On-premises security identifier (SID) for users who were synchronized from on-premises to the cloud.</span></span> |<span data-ttu-id="5975f-274">(user.onPremisesSecurityIdentifier -eq "S-1-1-11-1111111111-1111111111-1111111111-1111111")</span><span class="sxs-lookup"><span data-stu-id="5975f-274">(user.onPremisesSecurityIdentifier -eq "S-1-1-11-1111111111-1111111111-1111111111-1111111")</span></span> |
| <span data-ttu-id="5975f-275">passwordPolicies</span><span class="sxs-lookup"><span data-stu-id="5975f-275">passwordPolicies</span></span> |<span data-ttu-id="5975f-276">None DisableStrongPassword DisablePasswordExpiration DisablePasswordExpiration, DisableStrongPassword</span><span class="sxs-lookup"><span data-stu-id="5975f-276">None DisableStrongPassword DisablePasswordExpiration DisablePasswordExpiration, DisableStrongPassword</span></span> |<span data-ttu-id="5975f-277">(user.passwordPolicies -eq "DisableStrongPassword")</span><span class="sxs-lookup"><span data-stu-id="5975f-277">(user.passwordPolicies -eq "DisableStrongPassword")</span></span> |
| <span data-ttu-id="5975f-278">physicalDeliveryOfficeName</span><span class="sxs-lookup"><span data-stu-id="5975f-278">physicalDeliveryOfficeName</span></span> |<span data-ttu-id="5975f-279">任何字串值或 $null</span><span class="sxs-lookup"><span data-stu-id="5975f-279">Any string value or $null</span></span> |<span data-ttu-id="5975f-280">(user.physicalDeliveryOfficeName -eq "value")</span><span class="sxs-lookup"><span data-stu-id="5975f-280">(user.physicalDeliveryOfficeName -eq "value")</span></span> |
| <span data-ttu-id="5975f-281">postalCode</span><span class="sxs-lookup"><span data-stu-id="5975f-281">postalCode</span></span> |<span data-ttu-id="5975f-282">任何字串值或 $null</span><span class="sxs-lookup"><span data-stu-id="5975f-282">Any string value or $null</span></span> |<span data-ttu-id="5975f-283">(user.postalCode -eq "value")</span><span class="sxs-lookup"><span data-stu-id="5975f-283">(user.postalCode -eq "value")</span></span> |
| <span data-ttu-id="5975f-284">preferredLanguage</span><span class="sxs-lookup"><span data-stu-id="5975f-284">preferredLanguage</span></span> |<span data-ttu-id="5975f-285">ISO 639-1 code</span><span class="sxs-lookup"><span data-stu-id="5975f-285">ISO 639-1 code</span></span> |<span data-ttu-id="5975f-286">(user.preferredLanguage -eq "en-US")</span><span class="sxs-lookup"><span data-stu-id="5975f-286">(user.preferredLanguage -eq "en-US")</span></span> |
| <span data-ttu-id="5975f-287">sipProxyAddress</span><span class="sxs-lookup"><span data-stu-id="5975f-287">sipProxyAddress</span></span> |<span data-ttu-id="5975f-288">任何字串值或 $null</span><span class="sxs-lookup"><span data-stu-id="5975f-288">Any string value or $null</span></span> |<span data-ttu-id="5975f-289">(user.sipProxyAddress -eq "value")</span><span class="sxs-lookup"><span data-stu-id="5975f-289">(user.sipProxyAddress -eq "value")</span></span> |
| <span data-ttu-id="5975f-290">state</span><span class="sxs-lookup"><span data-stu-id="5975f-290">state</span></span> |<span data-ttu-id="5975f-291">任何字串值或 $null</span><span class="sxs-lookup"><span data-stu-id="5975f-291">Any string value or $null</span></span> |<span data-ttu-id="5975f-292">(user.state -eq "value")</span><span class="sxs-lookup"><span data-stu-id="5975f-292">(user.state -eq "value")</span></span> |
| <span data-ttu-id="5975f-293">streetAddress</span><span class="sxs-lookup"><span data-stu-id="5975f-293">streetAddress</span></span> |<span data-ttu-id="5975f-294">任何字串值或 $null</span><span class="sxs-lookup"><span data-stu-id="5975f-294">Any string value or $null</span></span> |<span data-ttu-id="5975f-295">(user.streetAddress -eq "value")</span><span class="sxs-lookup"><span data-stu-id="5975f-295">(user.streetAddress -eq "value")</span></span> |
| <span data-ttu-id="5975f-296">surname</span><span class="sxs-lookup"><span data-stu-id="5975f-296">surname</span></span> |<span data-ttu-id="5975f-297">任何字串值或 $null</span><span class="sxs-lookup"><span data-stu-id="5975f-297">Any string value or $null</span></span> |<span data-ttu-id="5975f-298">(user.surname -eq "value")</span><span class="sxs-lookup"><span data-stu-id="5975f-298">(user.surname -eq "value")</span></span> |
| <span data-ttu-id="5975f-299">telephoneNumber</span><span class="sxs-lookup"><span data-stu-id="5975f-299">telephoneNumber</span></span> |<span data-ttu-id="5975f-300">任何字串值或 $null</span><span class="sxs-lookup"><span data-stu-id="5975f-300">Any string value or $null</span></span> |<span data-ttu-id="5975f-301">(user.telephoneNumber -eq "value")</span><span class="sxs-lookup"><span data-stu-id="5975f-301">(user.telephoneNumber -eq "value")</span></span> |
| <span data-ttu-id="5975f-302">usageLocation</span><span class="sxs-lookup"><span data-stu-id="5975f-302">usageLocation</span></span> |<span data-ttu-id="5975f-303">兩個字母的國家 (地區) 代碼</span><span class="sxs-lookup"><span data-stu-id="5975f-303">Two lettered country code</span></span> |<span data-ttu-id="5975f-304">(user.usageLocation -eq "US")</span><span class="sxs-lookup"><span data-stu-id="5975f-304">(user.usageLocation -eq "US")</span></span> |
| <span data-ttu-id="5975f-305">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="5975f-305">userPrincipalName</span></span> |<span data-ttu-id="5975f-306">任何字串值</span><span class="sxs-lookup"><span data-stu-id="5975f-306">Any string value</span></span> |<span data-ttu-id="5975f-307">(user.userPrincipalName -eq "alias@domain")</span><span class="sxs-lookup"><span data-stu-id="5975f-307">(user.userPrincipalName -eq "alias@domain")</span></span> |
| <span data-ttu-id="5975f-308">userType</span><span class="sxs-lookup"><span data-stu-id="5975f-308">userType</span></span> |<span data-ttu-id="5975f-309">member guest $null</span><span class="sxs-lookup"><span data-stu-id="5975f-309">member guest $null</span></span> |<span data-ttu-id="5975f-310">(user.userType -eq "Member")</span><span class="sxs-lookup"><span data-stu-id="5975f-310">(user.userType -eq "Member")</span></span> |

### <a name="properties-of-type-string-collection"></a><span data-ttu-id="5975f-311">字串集合類型的屬性</span><span class="sxs-lookup"><span data-stu-id="5975f-311">Properties of type string collection</span></span>
<span data-ttu-id="5975f-312">允許的運算子</span><span class="sxs-lookup"><span data-stu-id="5975f-312">Allowed operators</span></span>

* <span data-ttu-id="5975f-313">-contains</span><span class="sxs-lookup"><span data-stu-id="5975f-313">-contains</span></span>
* <span data-ttu-id="5975f-314">-notContains</span><span class="sxs-lookup"><span data-stu-id="5975f-314">-notContains</span></span>

| <span data-ttu-id="5975f-315">屬性</span><span class="sxs-lookup"><span data-stu-id="5975f-315">Properties</span></span> | <span data-ttu-id="5975f-316">允許的值</span><span class="sxs-lookup"><span data-stu-id="5975f-316">Allowed values</span></span> | <span data-ttu-id="5975f-317">使用量</span><span class="sxs-lookup"><span data-stu-id="5975f-317">Usage</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5975f-318">otherMails</span><span class="sxs-lookup"><span data-stu-id="5975f-318">otherMails</span></span> |<span data-ttu-id="5975f-319">任何字串值</span><span class="sxs-lookup"><span data-stu-id="5975f-319">Any string value</span></span> |<span data-ttu-id="5975f-320">(user.otherMails -contains "alias@domain")</span><span class="sxs-lookup"><span data-stu-id="5975f-320">(user.otherMails -contains "alias@domain")</span></span> |
| <span data-ttu-id="5975f-321">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="5975f-321">proxyAddresses</span></span> |<span data-ttu-id="5975f-322">SMTP: alias@domain smtp: alias@domain</span><span class="sxs-lookup"><span data-stu-id="5975f-322">SMTP: alias@domain smtp: alias@domain</span></span> |<span data-ttu-id="5975f-323">(user.proxyAddresses -contains "SMTP: alias@domain")</span><span class="sxs-lookup"><span data-stu-id="5975f-323">(user.proxyAddresses -contains "SMTP: alias@domain")</span></span> |

## <a name="multi-value-properties"></a><span data-ttu-id="5975f-324">多重值屬性</span><span class="sxs-lookup"><span data-stu-id="5975f-324">Multi-value properties</span></span>
<span data-ttu-id="5975f-325">允許的運算子</span><span class="sxs-lookup"><span data-stu-id="5975f-325">Allowed operators</span></span>

* <span data-ttu-id="5975f-326">-any (集合中至少有一個項目符合條件時滿足)</span><span class="sxs-lookup"><span data-stu-id="5975f-326">-any (satisfied when at least one item in the collection matches the condition)</span></span>
* <span data-ttu-id="5975f-327">-all (集合中的所有項目符合條件時滿足)</span><span class="sxs-lookup"><span data-stu-id="5975f-327">-all (satisfied when all items in the collection match the condition)</span></span>

| <span data-ttu-id="5975f-328">屬性</span><span class="sxs-lookup"><span data-stu-id="5975f-328">Properties</span></span> | <span data-ttu-id="5975f-329">值</span><span class="sxs-lookup"><span data-stu-id="5975f-329">Values</span></span> | <span data-ttu-id="5975f-330">使用量</span><span class="sxs-lookup"><span data-stu-id="5975f-330">Usage</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5975f-331">assignedPlans</span><span class="sxs-lookup"><span data-stu-id="5975f-331">assignedPlans</span></span> |<span data-ttu-id="5975f-332">集合中的每個物件都會公開下列字串屬性：capabilityStatus、service、servicePlanId</span><span class="sxs-lookup"><span data-stu-id="5975f-332">Each object in the collection exposes the following string properties: capabilityStatus, service, servicePlanId</span></span> |<span data-ttu-id="5975f-333">user.assignedPlans -any (assignedPlan.servicePlanId -eq "efb87545-963c-4e0d-99df-69c6916d9eb0" -and assignedPlan.capabilityStatus -eq "Enabled")</span><span class="sxs-lookup"><span data-stu-id="5975f-333">user.assignedPlans -any (assignedPlan.servicePlanId -eq "efb87545-963c-4e0d-99df-69c6916d9eb0" -and assignedPlan.capabilityStatus -eq "Enabled")</span></span> |

<span data-ttu-id="5975f-334">多重值屬性是相同類型之物件的集合。</span><span class="sxs-lookup"><span data-stu-id="5975f-334">Multi-value properties are collections of objects of the same type.</span></span> <span data-ttu-id="5975f-335">您可以使用 -any 和 -all 運算子，分別將條件套用至集合中的一個或所有項目。</span><span class="sxs-lookup"><span data-stu-id="5975f-335">You can use -any and -all operators to apply a condition to one or all of the items in the collection, respectively.</span></span> <span data-ttu-id="5975f-336">例如：</span><span class="sxs-lookup"><span data-stu-id="5975f-336">For example:</span></span>

<span data-ttu-id="5975f-337">assignedPlans 是多重值屬性，可列出所有指派給使用者的服務方案。</span><span class="sxs-lookup"><span data-stu-id="5975f-337">assignedPlans is a multi-value property that lists all service plans assigned to the user.</span></span> <span data-ttu-id="5975f-338">下列運算式將會選取擁有 Exchange Online (方案 2) 服務方案 (也處於 [已啟用] 狀態) 的使用者：</span><span class="sxs-lookup"><span data-stu-id="5975f-338">The below expression will select users who have the Exchange Online (Plan 2) service plan that is also in Enabled state:</span></span>

```
user.assignedPlans -any (assignedPlan.servicePlanId -eq "efb87545-963c-4e0d-99df-69c6916d9eb0" -and assignedPlan.capabilityStatus -eq "Enabled")
```

<span data-ttu-id="5975f-339">(GUID 識別碼可識別 Exchange Online (方案 2) 服務方案。)</span><span class="sxs-lookup"><span data-stu-id="5975f-339">(The Guid identifier identifies the Exchange Online (Plan 2) service plan.)</span></span>

> [!NOTE]
> <span data-ttu-id="5975f-340">如果您想要識別已啟用 Office 365 (或其他 Microsoft Online 服務) 功能的所有使用者，例如以一組特定原則鎖定他們，此屬性非常有用。</span><span class="sxs-lookup"><span data-stu-id="5975f-340">This is useful if you want to identify all users for whom an Office 365 (or other Microsoft Online Service) capability has been enabled, for example to target them with a certain set of policies.</span></span>

<span data-ttu-id="5975f-341">下列運算式將會選取有任何服務方案與 Intune 服務 (透過服務名稱 "SCO" 來識別) 相關聯的所有使用者：</span><span class="sxs-lookup"><span data-stu-id="5975f-341">The following expression will select all users who have any service plan that is associated with the Intune service (identified by service name "SCO"):</span></span>
```
user.assignedPlans -any (assignedPlan.service -eq "SCO" -and assignedPlan.capabilityStatus -eq "Enabled")
```

## <a name="use-of-null-values"></a><span data-ttu-id="5975f-342">使用 Null 值</span><span class="sxs-lookup"><span data-stu-id="5975f-342">Use of Null values</span></span>

<span data-ttu-id="5975f-343">若要在規則中指定 null 值，您可以使用 "null" 或 $null。</span><span class="sxs-lookup"><span data-stu-id="5975f-343">To specify a null value in a rule, you can use "null" or $null.</span></span> <span data-ttu-id="5975f-344">範例：</span><span class="sxs-lookup"><span data-stu-id="5975f-344">Example:</span></span>
```
   user.mail –ne null
```
<span data-ttu-id="5975f-345">相當於</span><span class="sxs-lookup"><span data-stu-id="5975f-345">is equivalent to</span></span>
```
   user.mail –ne $null
   ```

## <a name="extension-attributes-and-custom-attributes"></a><span data-ttu-id="5975f-346">擴充屬性和自訂屬性</span><span class="sxs-lookup"><span data-stu-id="5975f-346">Extension attributes and custom attributes</span></span>
<span data-ttu-id="5975f-347">動態成員資格規則支援擴充屬性和自訂屬性。</span><span class="sxs-lookup"><span data-stu-id="5975f-347">Extension attributes and custom attributes are supported in dynamic membership rules.</span></span>

<span data-ttu-id="5975f-348">擴充屬性會從內部部署 Windows Server AD 進行同步處理，並採用 "ExtensionAttributeX" 格式，其中 X 等於 1-15。</span><span class="sxs-lookup"><span data-stu-id="5975f-348">Extension attributes are synced from on-premises Window Server AD and take the format of "ExtensionAttributeX", where X equals 1 - 15.</span></span>
<span data-ttu-id="5975f-349">以下是使用擴充屬性的規則範例：</span><span class="sxs-lookup"><span data-stu-id="5975f-349">An example of a rule that uses an extension attribute would be</span></span>
```
(user.extensionAttribute15 -eq "Marketing")
```
<span data-ttu-id="5975f-350">自訂屬性會從內部部署 Windows Server AD 或從連線的 SaaS 應用程式進行同步處理，並採用 "user.extension[GUID]\__[Attribute]" 格式，其中 [GUID] 是 AAD 中的唯一識別碼 (適用於在 AAD 中建立屬性的應用程式)，而 [Attribute] 是其建立的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="5975f-350">Custom Attributes are synced from on-premises Windows Server AD or from a connected SaaS application and the the format of "user.extension_[GUID]\__[Attribute]", where [GUID] is the unique identifier in AAD for the application that created the attribute in AAD and [Attribute] is the name of the attribute as it was created.</span></span>
<span data-ttu-id="5975f-351">以下是使用自訂屬性的規則範例：</span><span class="sxs-lookup"><span data-stu-id="5975f-351">An example of a rule that uses a custom attribute is</span></span>
```
user.extension_c272a57b722d4eb29bfe327874ae79cb__OfficeNumber  
```
<span data-ttu-id="5975f-352">使用 [Graph 總管] 查詢使用者的屬性並搜尋屬性名稱，即可在目錄中找到自訂屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="5975f-352">The custom attribute name can be found in the directory by querying a user's attribute using Graph Explorer and searching for the attribute name.</span></span>

## <a name="direct-reports-rule"></a><span data-ttu-id="5975f-353">「直屬員工」規則</span><span class="sxs-lookup"><span data-stu-id="5975f-353">"Direct Reports" Rule</span></span>
<span data-ttu-id="5975f-354">您可以建立一個群組，其中包含某位經理的所有直屬員工。</span><span class="sxs-lookup"><span data-stu-id="5975f-354">You can create a group containing all direct reports of a manager.</span></span> <span data-ttu-id="5975f-355">當經理的直屬員工在未來變更時，系統將會自動調整群組的成員資格。</span><span class="sxs-lookup"><span data-stu-id="5975f-355">When the manager's direct reports change in the future, the group's membership will be adjusted automatically.</span></span>

> [!NOTE]
> 1. <span data-ttu-id="5975f-356">若要讓規則得以運作，請確定已對您租用戶中的使用者正確設定 [經理識別碼] 屬性。</span><span class="sxs-lookup"><span data-stu-id="5975f-356">For the rule to work, make sure the **Manager ID** property is set correctly on users in your tenant.</span></span> <span data-ttu-id="5975f-357">您可以在其 **[設定檔] 索引標籤**上檢查使用者的目前值。</span><span class="sxs-lookup"><span data-stu-id="5975f-357">You can check the current value for a user on their **Profile tab**.</span></span>
> 2. <span data-ttu-id="5975f-358">此規則只支援**直屬**員工。</span><span class="sxs-lookup"><span data-stu-id="5975f-358">This rule only supports **direct** reports.</span></span> <span data-ttu-id="5975f-359">目前無法建立巢狀階層的群組，例如包含直屬員工及其員工的群組。</span><span class="sxs-lookup"><span data-stu-id="5975f-359">It is currently not possible to create a group for a nested hierarchy, e.g. a group that includes direct reports and their reports.</span></span>

<span data-ttu-id="5975f-360">**設定群組**</span><span class="sxs-lookup"><span data-stu-id="5975f-360">**To configure the group**</span></span>

1. <span data-ttu-id="5975f-361">依照[建立進階規則](#to-create-the-advanced-rule)一節中的步驟 1-5 操作，然後在 [成員資格類型] 中選取 [動態使用者]。</span><span class="sxs-lookup"><span data-stu-id="5975f-361">Follow steps 1-5 from section [To create the advanced rule](#to-create-the-advanced-rule), and select a **Membership type** of **Dynamic User**.</span></span>
2. <span data-ttu-id="5975f-362">在 [動態成員資格規則]  刀鋒視窗上，使用下列語法來輸入規則：</span><span class="sxs-lookup"><span data-stu-id="5975f-362">On the **Dynamic membership rules** blade, enter the rule with the following syntax:</span></span>

    <span data-ttu-id="5975f-363">*Direct Reports for "{obectID_of_manager}"*</span><span class="sxs-lookup"><span data-stu-id="5975f-363">*Direct Reports for "{obectID_of_manager}"*</span></span>

    <span data-ttu-id="5975f-364">有效規則的範例：</span><span class="sxs-lookup"><span data-stu-id="5975f-364">An example of a valid rule:</span></span>
```
                    Direct Reports for "62e19b97-8b3d-4d4a-a106-4ce66896a863"
```
    where “62e19b97-8b3d-4d4a-a106-4ce66896a863” is the objectID of the manager. The object ID can be found on manager's **Profile tab**.
3. <span data-ttu-id="5975f-365">儲存規則之後，即會將具有指定經理識別碼值的所有使用者新增至群組。</span><span class="sxs-lookup"><span data-stu-id="5975f-365">After saving the rule, all users with the specified Manager ID value will be added to the group.</span></span>

## <a name="using-attributes-to-create-rules-for-device-objects"></a><span data-ttu-id="5975f-366">使用屬性來建立裝置物件的規則</span><span class="sxs-lookup"><span data-stu-id="5975f-366">Using attributes to create rules for device objects</span></span>
<span data-ttu-id="5975f-367">您也可以建立規則以在群組中選取成員資格的裝置物件。</span><span class="sxs-lookup"><span data-stu-id="5975f-367">You can also create a rule that selects device objects for membership in a group.</span></span> <span data-ttu-id="5975f-368">可以使用下列裝置屬性。</span><span class="sxs-lookup"><span data-stu-id="5975f-368">The following device attributes can be used.</span></span>

 <span data-ttu-id="5975f-369">裝置屬性</span><span class="sxs-lookup"><span data-stu-id="5975f-369">Device attribute</span></span>  | <span data-ttu-id="5975f-370">值</span><span class="sxs-lookup"><span data-stu-id="5975f-370">Values</span></span> | <span data-ttu-id="5975f-371">範例</span><span class="sxs-lookup"><span data-stu-id="5975f-371">Example</span></span>
 ----- | ----- | ----------------
 <span data-ttu-id="5975f-372">accountEnabled</span><span class="sxs-lookup"><span data-stu-id="5975f-372">accountEnabled</span></span> | <span data-ttu-id="5975f-373">true false</span><span class="sxs-lookup"><span data-stu-id="5975f-373">true false</span></span> | <span data-ttu-id="5975f-374">(device.accountEnabled -eq true)</span><span class="sxs-lookup"><span data-stu-id="5975f-374">(device.accountEnabled -eq true)</span></span>
 <span data-ttu-id="5975f-375">displayName</span><span class="sxs-lookup"><span data-stu-id="5975f-375">displayName</span></span> | <span data-ttu-id="5975f-376">任何字串值</span><span class="sxs-lookup"><span data-stu-id="5975f-376">any string value</span></span> |<span data-ttu-id="5975f-377">(device.displayName -eq "Rob Iphone”)</span><span class="sxs-lookup"><span data-stu-id="5975f-377">(device.displayName -eq "Rob Iphone”)</span></span>
 <span data-ttu-id="5975f-378">deviceOSType</span><span class="sxs-lookup"><span data-stu-id="5975f-378">deviceOSType</span></span> | <span data-ttu-id="5975f-379">任何字串值</span><span class="sxs-lookup"><span data-stu-id="5975f-379">any string value</span></span> | <span data-ttu-id="5975f-380">(device.deviceOSType -eq "IOS")</span><span class="sxs-lookup"><span data-stu-id="5975f-380">(device.deviceOSType -eq "IOS")</span></span>
 <span data-ttu-id="5975f-381">deviceOSVersion</span><span class="sxs-lookup"><span data-stu-id="5975f-381">deviceOSVersion</span></span> | <span data-ttu-id="5975f-382">任何字串值</span><span class="sxs-lookup"><span data-stu-id="5975f-382">any string value</span></span> | <span data-ttu-id="5975f-383">(device.OSVersion -eq "9.1")</span><span class="sxs-lookup"><span data-stu-id="5975f-383">(device.OSVersion -eq "9.1")</span></span>
 <span data-ttu-id="5975f-384">deviceCategory</span><span class="sxs-lookup"><span data-stu-id="5975f-384">deviceCategory</span></span> | <span data-ttu-id="5975f-385">有效的裝置類別名稱</span><span class="sxs-lookup"><span data-stu-id="5975f-385">a valid device category name</span></span> | <span data-ttu-id="5975f-386">(device.deviceCategory -eq "BYOD")</span><span class="sxs-lookup"><span data-stu-id="5975f-386">(device.deviceCategory -eq "BYOD")</span></span>
 <span data-ttu-id="5975f-387">deviceManufacturer</span><span class="sxs-lookup"><span data-stu-id="5975f-387">deviceManufacturer</span></span> | <span data-ttu-id="5975f-388">任何字串值</span><span class="sxs-lookup"><span data-stu-id="5975f-388">any string value</span></span> | <span data-ttu-id="5975f-389">(device.deviceManufacturer -eq "Samsung")</span><span class="sxs-lookup"><span data-stu-id="5975f-389">(device.deviceManufacturer -eq "Samsung")</span></span>
 <span data-ttu-id="5975f-390">deviceModel</span><span class="sxs-lookup"><span data-stu-id="5975f-390">deviceModel</span></span> | <span data-ttu-id="5975f-391">任何字串值</span><span class="sxs-lookup"><span data-stu-id="5975f-391">any string value</span></span> | <span data-ttu-id="5975f-392">(device.deviceModel -eq "iPad Air")</span><span class="sxs-lookup"><span data-stu-id="5975f-392">(device.deviceModel -eq "iPad Air")</span></span>
 <span data-ttu-id="5975f-393">deviceOwnership</span><span class="sxs-lookup"><span data-stu-id="5975f-393">deviceOwnership</span></span> | <span data-ttu-id="5975f-394">個人、公司</span><span class="sxs-lookup"><span data-stu-id="5975f-394">Personal, Company</span></span> | <span data-ttu-id="5975f-395">(device.deviceOwnership -eq "Company")</span><span class="sxs-lookup"><span data-stu-id="5975f-395">(device.deviceOwnership -eq "Company")</span></span>
 <span data-ttu-id="5975f-396">domainName</span><span class="sxs-lookup"><span data-stu-id="5975f-396">domainName</span></span> | <span data-ttu-id="5975f-397">任何字串值</span><span class="sxs-lookup"><span data-stu-id="5975f-397">any string value</span></span> | <span data-ttu-id="5975f-398">(device.domainName -eq "contoso.com")</span><span class="sxs-lookup"><span data-stu-id="5975f-398">(device.domainName -eq "contoso.com")</span></span>
 <span data-ttu-id="5975f-399">enrollmentProfileName</span><span class="sxs-lookup"><span data-stu-id="5975f-399">enrollmentProfileName</span></span> | <span data-ttu-id="5975f-400">Apple 裝置註冊設定檔名稱</span><span class="sxs-lookup"><span data-stu-id="5975f-400">Apple Device Enrollment Profile name</span></span> | <span data-ttu-id="5975f-401">(device.enrollmentProfileName -eq "DEP iPhones")</span><span class="sxs-lookup"><span data-stu-id="5975f-401">(device.enrollmentProfileName -eq "DEP iPhones")</span></span>
 <span data-ttu-id="5975f-402">isRooted</span><span class="sxs-lookup"><span data-stu-id="5975f-402">isRooted</span></span> | <span data-ttu-id="5975f-403">true false</span><span class="sxs-lookup"><span data-stu-id="5975f-403">true false</span></span> | <span data-ttu-id="5975f-404">(device.isRooted -eq true)</span><span class="sxs-lookup"><span data-stu-id="5975f-404">(device.isRooted -eq true)</span></span>
 <span data-ttu-id="5975f-405">managementType</span><span class="sxs-lookup"><span data-stu-id="5975f-405">managementType</span></span> | <span data-ttu-id="5975f-406">MDM (適用於行動裝置)</span><span class="sxs-lookup"><span data-stu-id="5975f-406">MDM (for mobile devices)</span></span><br><span data-ttu-id="5975f-407">PC (適用於 Intune PC 代理程式管理的電腦)</span><span class="sxs-lookup"><span data-stu-id="5975f-407">PC (for computers managed by the Intune PC agent)</span></span> | <span data-ttu-id="5975f-408">(device.managementType -eq "MDM")</span><span class="sxs-lookup"><span data-stu-id="5975f-408">(device.managementType -eq "MDM")</span></span>
 <span data-ttu-id="5975f-409">organizationalUnit</span><span class="sxs-lookup"><span data-stu-id="5975f-409">organizationalUnit</span></span> | <span data-ttu-id="5975f-410">符合內部部署 Active Directory 所設定的組織單位名稱的任何字串值</span><span class="sxs-lookup"><span data-stu-id="5975f-410">any string value matching the name of the organizational unit set by an on-premises Active Directory</span></span> | <span data-ttu-id="5975f-411">(device.organizationalUnit -eq "US PCs")</span><span class="sxs-lookup"><span data-stu-id="5975f-411">(device.organizationalUnit -eq "US PCs")</span></span>
 <span data-ttu-id="5975f-412">deviceId</span><span class="sxs-lookup"><span data-stu-id="5975f-412">deviceId</span></span> | <span data-ttu-id="5975f-413">有效的 Azure AD 裝置識別碼</span><span class="sxs-lookup"><span data-stu-id="5975f-413">a valid Azure AD device ID</span></span> | <span data-ttu-id="5975f-414">(device.deviceId -eq "d4fe7726-5966-431c-b3b8-cddc8fdb717d")</span><span class="sxs-lookup"><span data-stu-id="5975f-414">(device.deviceId -eq "d4fe7726-5966-431c-b3b8-cddc8fdb717d")</span></span>
 <span data-ttu-id="5975f-415">objectId</span><span class="sxs-lookup"><span data-stu-id="5975f-415">objectId</span></span> | <span data-ttu-id="5975f-416">有效的 Azure AD 物件識別碼</span><span class="sxs-lookup"><span data-stu-id="5975f-416">a valid Azure AD object ID</span></span> |  <span data-ttu-id="5975f-417">(device.objectId -eq 76ad43c9-32c5-45e8-a272-7b58b58f596d")</span><span class="sxs-lookup"><span data-stu-id="5975f-417">(device.objectId -eq 76ad43c9-32c5-45e8-a272-7b58b58f596d")</span></span>




## <a name="next-steps"></a><span data-ttu-id="5975f-418">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5975f-418">Next steps</span></span>
<span data-ttu-id="5975f-419">這些文章提供有關 Azure Active Directory 中群組的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="5975f-419">These articles provide additional information on groups in Azure Active Directory.</span></span>

* [<span data-ttu-id="5975f-420">查看現有的群組</span><span class="sxs-lookup"><span data-stu-id="5975f-420">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="5975f-421">建立新群組並新增成員</span><span class="sxs-lookup"><span data-stu-id="5975f-421">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="5975f-422">管理群組的設定</span><span class="sxs-lookup"><span data-stu-id="5975f-422">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="5975f-423">管理群組的成員資格</span><span class="sxs-lookup"><span data-stu-id="5975f-423">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="5975f-424">管理群組中使用者的動態規則</span><span class="sxs-lookup"><span data-stu-id="5975f-424">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
