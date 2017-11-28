---
title: "Azure Active Directory 中的 aaaAttribute 為基礎的動態群組成員資格 |Microsoft 文件"
description: "如何 toocreate 進階包括支援的運算式規則運算子和參數的動態群組成員資格的規則。"
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
ms.openlocfilehash: 8cd06ed70433eff65401c67d7351d5dcc12a9dd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-attribute-based-rules-for-dynamic-group-membership-in-azure-active-directory"></a><span data-ttu-id="44eb3-103">在 Azure Active Directory 中針對動態群組成員資格建立以屬性為基礎的規則</span><span class="sxs-lookup"><span data-stu-id="44eb3-103">Create attribute-based rules for dynamic group membership in Azure Active Directory</span></span>
<span data-ttu-id="44eb3-104">在 Azure Active Directory (Azure AD) 中，您可以建立進階的規則 tooenable 複雜屬性為基礎群組動態成員資格。</span><span class="sxs-lookup"><span data-stu-id="44eb3-104">In Azure Active Directory (Azure AD), you can create advanced rules tooenable complex attribute-based dynamic memberships for groups.</span></span> <span data-ttu-id="44eb3-105">這篇文章說明 hello 屬性和語法 toocreate 動態成員資格規則的使用者或裝置。</span><span class="sxs-lookup"><span data-stu-id="44eb3-105">This article details hello attributes and syntax toocreate dynamic membership rules for users or devices.</span></span>

<span data-ttu-id="44eb3-106">當使用者或裝置的變更的任何屬性，hello 系統才會評估所有的動態群組規則在目錄 toosee hello 變更會觸發任何群組加入或移除。</span><span class="sxs-lookup"><span data-stu-id="44eb3-106">When any attributes of a user or device change, hello system evaluates all dynamic group rules in a directory toosee if hello change would trigger any group adds or removes.</span></span> <span data-ttu-id="44eb3-107">如果使用者或裝置滿足群組上的規則，就會將他們新增為該群組的成員。</span><span class="sxs-lookup"><span data-stu-id="44eb3-107">If a user or device satisfies a rule on a group, they are added as a member of that group.</span></span> <span data-ttu-id="44eb3-108">如果它們不會再滿足 hello 規則，則會將它移除。</span><span class="sxs-lookup"><span data-stu-id="44eb3-108">If they no longer satisfy hello rule, they are removed.</span></span>

> [!NOTE]
> - <span data-ttu-id="44eb3-109">您可以為安全性群組或 Office 365 群組的動態成員資格設定規則。</span><span class="sxs-lookup"><span data-stu-id="44eb3-109">You can set up a rule for dynamic membership on security groups or Office 365 groups.</span></span>
>
> - <span data-ttu-id="44eb3-110">此功能的每個使用者成員加入的 tooat 至少有一個動態群組需要有 Azure AD Premium P1 的授權。</span><span class="sxs-lookup"><span data-stu-id="44eb3-110">This feature requires an Azure AD Premium P1 license for each user member added tooat least one dynamic group.</span></span>
>
> - <span data-ttu-id="44eb3-111">您可以為裝置或使用者建立動態群組，但無法建立同時包含使用者和裝置物件的規則。</span><span class="sxs-lookup"><span data-stu-id="44eb3-111">You can create a dynamic group for devices or users, but you cannot create a rule that contains both user and device objects.</span></span>

> - <span data-ttu-id="44eb3-112">Hello 當時不可能 toocreate 裝置群組會根據擁有使用者的屬性。</span><span class="sxs-lookup"><span data-stu-id="44eb3-112">At hello moment it is not possible toocreate a device group based on owning user's attributes.</span></span> <span data-ttu-id="44eb3-113">裝置成員資格規則可以只參考立即屬性的裝置 hello 目錄中的物件。</span><span class="sxs-lookup"><span data-stu-id="44eb3-113">Device membership rules can only reference immediate attributes of device objects in hello directory.</span></span>

## <a name="toocreate-an-advanced-rule"></a><span data-ttu-id="44eb3-114">toocreate 進階規則</span><span class="sxs-lookup"><span data-stu-id="44eb3-114">toocreate an advanced rule</span></span>
1. <span data-ttu-id="44eb3-115">登入 toohello [Azure AD 系統管理中心](https://aad.portal.azure.com)是全域管理員或使用者帳戶系統管理員的帳戶。</span><span class="sxs-lookup"><span data-stu-id="44eb3-115">Sign in toohello [Azure AD admin center](https://aad.portal.azure.com) with an account that is a global administrator or a user account administrator.</span></span>
2. <span data-ttu-id="44eb3-116">選取 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="44eb3-116">Select **Users and groups**.</span></span>
3. <span data-ttu-id="44eb3-117">選取 [所有群組]。</span><span class="sxs-lookup"><span data-stu-id="44eb3-117">Select **All groups**.</span></span>

   ![開啟 hello 群組刀鋒視窗](./media/active-directory-groups-dynamic-membership-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="44eb3-119">在 [所有群組] 中，選取 [新增群組]。</span><span class="sxs-lookup"><span data-stu-id="44eb3-119">In **All groups**, select **New group**.</span></span>

   ![Add new group](./media/active-directory-groups-dynamic-membership-azure-portal/add-group-type.png)
5. <span data-ttu-id="44eb3-121">在 [hello**群組**刀鋒視窗中，輸入名稱和描述 hello 新群組。</span><span class="sxs-lookup"><span data-stu-id="44eb3-121">On hello **Group** blade, enter a name and description for hello new group.</span></span> <span data-ttu-id="44eb3-122">選取**成員資格類型**的其中一個**動態使用者**或**動態裝置**，根據您是否想 toocreate 規則的使用者或裝置，，，然後選取 [ **新增動態查詢**。</span><span class="sxs-lookup"><span data-stu-id="44eb3-122">Select a **Membership type** of either **Dynamic User** or **Dynamic Device**, depending on whether you want toocreate a rule for users or devices, and then select **Add dynamic query**.</span></span> <span data-ttu-id="44eb3-123">Hello 屬性用於裝置的規則，請參閱[裝置物件使用屬性 toocreate 規則](#using-attributes-to-create-rules-for-device-objects)。</span><span class="sxs-lookup"><span data-stu-id="44eb3-123">For hello attributes used for device rules, see [Using attributes toocreate rules for device objects](#using-attributes-to-create-rules-for-device-objects).</span></span>

   ![新增動態成員資格規則](./media/active-directory-groups-dynamic-membership-azure-portal/add-dynamic-group-rule.png)
6. <span data-ttu-id="44eb3-125">Hello 上**動態成員資格規則**刀鋒視窗中，輸入您的規則 hello**新增動態成員資格的進階規則**方塊中，按 Enter 鍵，並選取**建立**底部的 hellohello 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="44eb3-125">On hello **Dynamic membership rules** blade, enter your rule into hello **Add dynamic membership advanced rule** box, press Enter, and then select **Create** at hello bottom of hello blade.</span></span>
7. <span data-ttu-id="44eb3-126">選取**建立**上 hello**群組**刀鋒視窗 toocreate hello 群組。</span><span class="sxs-lookup"><span data-stu-id="44eb3-126">Select **Create** on hello **Group** blade toocreate hello group.</span></span>

## <a name="constructing-hello-body-of-an-advanced-rule"></a><span data-ttu-id="44eb3-127">建構進階規則的 hello 主體</span><span class="sxs-lookup"><span data-stu-id="44eb3-127">Constructing hello body of an advanced rule</span></span>
<span data-ttu-id="44eb3-128">您可以建立 hello 群組的動態成員資格的 hello 進階的規則基本上是二進位運算式包含三個部分，並產生 true 或 false 的結果。</span><span class="sxs-lookup"><span data-stu-id="44eb3-128">hello advanced rule that you can create for hello dynamic memberships for groups is essentially a binary expression that consists of three parts and results in a true or false outcome.</span></span> <span data-ttu-id="44eb3-129">hello 三個部分是：</span><span class="sxs-lookup"><span data-stu-id="44eb3-129">hello three parts are:</span></span>

* <span data-ttu-id="44eb3-130">左側的參數</span><span class="sxs-lookup"><span data-stu-id="44eb3-130">Left parameter</span></span>
* <span data-ttu-id="44eb3-131">二進位運算子</span><span class="sxs-lookup"><span data-stu-id="44eb3-131">Binary operator</span></span>
* <span data-ttu-id="44eb3-132">右側的常數</span><span class="sxs-lookup"><span data-stu-id="44eb3-132">Right constant</span></span>

<span data-ttu-id="44eb3-133">完整的進階的規則看起來類似 toothis: (leftParameter binaryOperator"RightConstant")，hello 左右括號是選擇性的 hello 整個二進位運算式，雙引號是選擇性的只需 hello 右當它是字串，而且 hello 左參數的 hello 語法 user.property 常數。</span><span class="sxs-lookup"><span data-stu-id="44eb3-133">A complete advanced rule looks similar toothis: (leftParameter binaryOperator "RightConstant"), where hello opening and closing parenthesis are optional for hello entire binary expression, double quotes are optional as well, only required for hello right constant when it is string, and hello syntax for hello left parameter is user.property.</span></span> <span data-ttu-id="44eb3-134">進階的規則可以包含一個以上的二進位運算式分隔 hello-和、-或，和-不是邏輯運算子。</span><span class="sxs-lookup"><span data-stu-id="44eb3-134">An advanced rule can consist of more than one binary expressions separated by hello -and, -or, and -not logical operators.</span></span>

<span data-ttu-id="44eb3-135">hello 以下是正確建構的進階規則的範例：</span><span class="sxs-lookup"><span data-stu-id="44eb3-135">hello following are examples of a properly constructed advanced rule:</span></span>
```
(user.department -eq "Sales") -or (user.department -eq "Marketing")
(user.department -eq "Sales") -and -not (user.jobTitle -contains "SDE")
```
<span data-ttu-id="44eb3-136">Hello 的支援的參數和運算式規則運算子的完整清單，請參閱下列各節。</span><span class="sxs-lookup"><span data-stu-id="44eb3-136">For hello complete list of supported parameters and expression rule operators, see sections below.</span></span> <span data-ttu-id="44eb3-137">Hello 屬性用於裝置的規則，請參閱[裝置物件使用屬性 toocreate 規則](#using-attributes-to-create-rules-for-device-objects)。</span><span class="sxs-lookup"><span data-stu-id="44eb3-137">For hello attributes used for device rules, see [Using attributes toocreate rules for device objects](#using-attributes-to-create-rules-for-device-objects).</span></span>

<span data-ttu-id="44eb3-138">hello hello 主體進階規則的總長度不能超過 2048年個字元。</span><span class="sxs-lookup"><span data-stu-id="44eb3-138">hello total length of hello body of your advanced rule cannot exceed 2048 characters.</span></span>

> [!NOTE]
> <span data-ttu-id="44eb3-139">字串和 regex 運算都不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="44eb3-139">String and regex operations are not case sensitive.</span></span> <span data-ttu-id="44eb3-140">您也可以使用 $null 做為常數，執行 Null 檢查，例如，user.department-eq $null。</span><span class="sxs-lookup"><span data-stu-id="44eb3-140">You can also perform Null checks, using $null as a constant, for example, user.department -eq $null.</span></span>
> <span data-ttu-id="44eb3-141">包含引號 " 的字串應該使用 ' 字元逸出，例如 user.department -eq \\`"Sales"。</span><span class="sxs-lookup"><span data-stu-id="44eb3-141">Strings containing quotes " should be escaped using 'character, for example, user.department -eq \\`"Sales".</span></span>

## <a name="supported-expression-rule-operators"></a><span data-ttu-id="44eb3-142">支援的運算式規則運算子</span><span class="sxs-lookup"><span data-stu-id="44eb3-142">Supported expression rule operators</span></span>
<span data-ttu-id="44eb3-143">hello 下表列出所有 hello 支援運算式規則運算子的進階規則的 hello hello 主體中使用其語法 toobe:</span><span class="sxs-lookup"><span data-stu-id="44eb3-143">hello following table lists all hello supported expression rule operators and their syntax toobe used in hello body of hello advanced rule:</span></span>

| <span data-ttu-id="44eb3-144"> 運算子</span><span class="sxs-lookup"><span data-stu-id="44eb3-144">Operator</span></span> | <span data-ttu-id="44eb3-145">語法</span><span class="sxs-lookup"><span data-stu-id="44eb3-145">Syntax</span></span> |
| --- | --- |
| <span data-ttu-id="44eb3-146">Not Equals</span><span class="sxs-lookup"><span data-stu-id="44eb3-146">Not Equals</span></span> |<span data-ttu-id="44eb3-147">-ne</span><span class="sxs-lookup"><span data-stu-id="44eb3-147">-ne</span></span> |
| <span data-ttu-id="44eb3-148">Equals</span><span class="sxs-lookup"><span data-stu-id="44eb3-148">Equals</span></span> |<span data-ttu-id="44eb3-149">-eq</span><span class="sxs-lookup"><span data-stu-id="44eb3-149">-eq</span></span> |
| <span data-ttu-id="44eb3-150">Not Starts With</span><span class="sxs-lookup"><span data-stu-id="44eb3-150">Not Starts With</span></span> |<span data-ttu-id="44eb3-151">-notStartsWith</span><span class="sxs-lookup"><span data-stu-id="44eb3-151">-notStartsWith</span></span> |
| <span data-ttu-id="44eb3-152">開頭為</span><span class="sxs-lookup"><span data-stu-id="44eb3-152">Starts With</span></span> |<span data-ttu-id="44eb3-153">-startsWith</span><span class="sxs-lookup"><span data-stu-id="44eb3-153">-startsWith</span></span> |
| <span data-ttu-id="44eb3-154">Not Contains</span><span class="sxs-lookup"><span data-stu-id="44eb3-154">Not Contains</span></span> |<span data-ttu-id="44eb3-155">-notContains</span><span class="sxs-lookup"><span data-stu-id="44eb3-155">-notContains</span></span> |
| <span data-ttu-id="44eb3-156">Contains</span><span class="sxs-lookup"><span data-stu-id="44eb3-156">Contains</span></span> |<span data-ttu-id="44eb3-157">-contains</span><span class="sxs-lookup"><span data-stu-id="44eb3-157">-contains</span></span> |
| <span data-ttu-id="44eb3-158">Not Match</span><span class="sxs-lookup"><span data-stu-id="44eb3-158">Not Match</span></span> |<span data-ttu-id="44eb3-159">-notMatch</span><span class="sxs-lookup"><span data-stu-id="44eb3-159">-notMatch</span></span> |
| <span data-ttu-id="44eb3-160">Match</span><span class="sxs-lookup"><span data-stu-id="44eb3-160">Match</span></span> |<span data-ttu-id="44eb3-161">-match</span><span class="sxs-lookup"><span data-stu-id="44eb3-161">-match</span></span> |
| <span data-ttu-id="44eb3-162">在</span><span class="sxs-lookup"><span data-stu-id="44eb3-162">In</span></span> | <span data-ttu-id="44eb3-163">-in</span><span class="sxs-lookup"><span data-stu-id="44eb3-163">-in</span></span> |
| <span data-ttu-id="44eb3-164">不在</span><span class="sxs-lookup"><span data-stu-id="44eb3-164">Not In</span></span> | <span data-ttu-id="44eb3-165">-notIn</span><span class="sxs-lookup"><span data-stu-id="44eb3-165">-notIn</span></span> |

## <a name="operator-precedence"></a><span data-ttu-id="44eb3-166">運算子優先順序</span><span class="sxs-lookup"><span data-stu-id="44eb3-166">Operator precedence</span></span>

<span data-ttu-id="44eb3-167">所有運算子如下所都列每個 toohigher 較低的優先順序。</span><span class="sxs-lookup"><span data-stu-id="44eb3-167">All Operators are listed below per precedence from lower toohigher.</span></span> <span data-ttu-id="44eb3-168">同一行上運算子的優先順序相等：</span><span class="sxs-lookup"><span data-stu-id="44eb3-168">Operators on same line are in equal precedence:</span></span>
````
-any -all
-or
-and
-not
-eq -ne -startsWith -notStartsWith -contains -notContains -match –notMatch -in -notIn
````
<span data-ttu-id="44eb3-169">可以用於所有的運算子，或不含 hello 連字號的前置詞。</span><span class="sxs-lookup"><span data-stu-id="44eb3-169">All operators can be used with or without hello hyphen prefix.</span></span> <span data-ttu-id="44eb3-170">優先順序不符合您的需求時，才需要括號。</span><span class="sxs-lookup"><span data-stu-id="44eb3-170">Parentheses are needed only when precedence does not meet your requirements.</span></span>
<span data-ttu-id="44eb3-171">例如：</span><span class="sxs-lookup"><span data-stu-id="44eb3-171">For example:</span></span>
```
   user.department –eq "Marketing" –and user.country –eq "US"
```
<span data-ttu-id="44eb3-172">相當於：</span><span class="sxs-lookup"><span data-stu-id="44eb3-172">is equivalent to:</span></span>
```
   (user.department –eq "Marketing") –and (user.country –eq "US")
```
## <a name="using-hello--in-and--notin-operators"></a><span data-ttu-id="44eb3-173">使用 hello-在和-notIn 運算子</span><span class="sxs-lookup"><span data-stu-id="44eb3-173">Using hello -In and -notIn operators</span></span>

<span data-ttu-id="44eb3-174">如果您想要針對不同的值數目的使用者屬性 toocompare hello 值可以使用 hello-中或-notIn 運算子。</span><span class="sxs-lookup"><span data-stu-id="44eb3-174">If you want toocompare hello value of a user attribute against a number of different values you can use hello -In or -notIn operators.</span></span> <span data-ttu-id="44eb3-175">以下是範例-運算子中使用 hello:</span><span class="sxs-lookup"><span data-stu-id="44eb3-175">Here is an example using hello -In operator:</span></span>
```
    user.department -In [ "50001", "50002", "50003", “50005”, “50006”, “50007”, “50008”, “50016”, “50020”, “50024”, “50038”, “50039”, “51100” ]
```
<span data-ttu-id="44eb3-176">請記下的 hello hello 使用"["和"]"hello 開頭和結尾 hello 值清單。</span><span class="sxs-lookup"><span data-stu-id="44eb3-176">Note hello use of hello "[" and "]" at hello beginning and end of hello list of values.</span></span> <span data-ttu-id="44eb3-177">這個條件評估 tooTrue 的 hello user.department 等於 hello 清單中的 hello 值的其中一個值。</span><span class="sxs-lookup"><span data-stu-id="44eb3-177">This condition evaluates tooTrue of hello value of user.department equals one of hello values in hello list.</span></span>


## <a name="query-error-remediation"></a><span data-ttu-id="44eb3-178">查詢錯誤補救</span><span class="sxs-lookup"><span data-stu-id="44eb3-178">Query error remediation</span></span>
<span data-ttu-id="44eb3-179">hello 下表列出可能出現的錯誤和如何 toocorrect 它們發生</span><span class="sxs-lookup"><span data-stu-id="44eb3-179">hello following table lists potential errors and how toocorrect them if they occur</span></span>

| <span data-ttu-id="44eb3-180">查詢剖析錯誤</span><span class="sxs-lookup"><span data-stu-id="44eb3-180">Query Parse Error</span></span> | <span data-ttu-id="44eb3-181">錯誤的使用方式</span><span class="sxs-lookup"><span data-stu-id="44eb3-181">Error Usage</span></span> | <span data-ttu-id="44eb3-182">更正的使用方式</span><span class="sxs-lookup"><span data-stu-id="44eb3-182">Corrected Usage</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44eb3-183">錯誤：不支援屬性。</span><span class="sxs-lookup"><span data-stu-id="44eb3-183">Error: Attribute not supported.</span></span> |<span data-ttu-id="44eb3-184">(user.invalidProperty -eq "Value")</span><span class="sxs-lookup"><span data-stu-id="44eb3-184">(user.invalidProperty -eq "Value")</span></span> |<span data-ttu-id="44eb3-185">(user.department -eq "value")</span><span class="sxs-lookup"><span data-stu-id="44eb3-185">(user.department -eq "value")</span></span><br/><span data-ttu-id="44eb3-186">屬性應符合一項來自 hello[支援屬性清單](#supported-properties)。</span><span class="sxs-lookup"><span data-stu-id="44eb3-186">Property should match one from hello [supported properties list](#supported-properties).</span></span> |
| <span data-ttu-id="44eb3-187">錯誤：屬性不支援運算子。</span><span class="sxs-lookup"><span data-stu-id="44eb3-187">Error: Operator is not supported on attribute.</span></span> |<span data-ttu-id="44eb3-188">(user.accountEnabled -contains true)</span><span class="sxs-lookup"><span data-stu-id="44eb3-188">(user.accountEnabled -contains true)</span></span> |<span data-ttu-id="44eb3-189">(user.accountEnabled -eq true)</span><span class="sxs-lookup"><span data-stu-id="44eb3-189">(user.accountEnabled -eq true)</span></span><br/><span data-ttu-id="44eb3-190"> 屬性屬於布林類型。</span><span class="sxs-lookup"><span data-stu-id="44eb3-190">Property is of type boolean.</span></span> <span data-ttu-id="44eb3-191">使用支援的 hello 運算子 (-eq 或-ne) 的布林型別，從清單上方的 hello。</span><span class="sxs-lookup"><span data-stu-id="44eb3-191">Use hello supported operators (-eq or -ne) on boolean type from hello above list.</span></span> |
| <span data-ttu-id="44eb3-192">錯誤：查詢編譯錯誤。</span><span class="sxs-lookup"><span data-stu-id="44eb3-192">Error: Query compilation error.</span></span> |<span data-ttu-id="44eb3-193">(user.department -eq "Sales") -and (user.department -eq "Marketing")(user.userPrincipalName -match "*@domain.ext")</span><span class="sxs-lookup"><span data-stu-id="44eb3-193">(user.department -eq "Sales") -and (user.department -eq "Marketing")(user.userPrincipalName -match "*@domain.ext")</span></span> |<span data-ttu-id="44eb3-194">(user.department -eq "Sales") -and (user.department -eq "Marketing")</span><span class="sxs-lookup"><span data-stu-id="44eb3-194">(user.department -eq "Sales") -and (user.department -eq "Marketing")</span></span><br/><span data-ttu-id="44eb3-195">邏輯運算子應該符合其中一個支援的 hello 上述的屬性清單。(user.userPrincipalName-比對 」。 *@domain.ext") 或 (user.userPrincipalName-比對"@domain.ext$") 在規則運算式中的錯誤。</span><span class="sxs-lookup"><span data-stu-id="44eb3-195">Logical operator should match one from hello supported properties list above.(user.userPrincipalName -match ".*@domain.ext")or(user.userPrincipalName -match "@domain.ext$")Error in regular expression.</span></span> |
| <span data-ttu-id="44eb3-196">錯誤：二進位運算式不是正確的格式。</span><span class="sxs-lookup"><span data-stu-id="44eb3-196">Error: Binary expression is not in right format.</span></span> |<span data-ttu-id="44eb3-197">(user.department –eq “Sales”) (user.department -eq "Sales")(user.department-eq"Sales")</span><span class="sxs-lookup"><span data-stu-id="44eb3-197">(user.department –eq “Sales”) (user.department -eq "Sales")(user.department-eq"Sales")</span></span> |<span data-ttu-id="44eb3-198">(user.accountEnabled -eq true) -and (user.userPrincipalName -contains "alias@domain")</span><span class="sxs-lookup"><span data-stu-id="44eb3-198">(user.accountEnabled -eq true) -and (user.userPrincipalName -contains "alias@domain")</span></span><br/><span data-ttu-id="44eb3-199">查詢有多個錯誤。</span><span class="sxs-lookup"><span data-stu-id="44eb3-199">Query has multiple errors.</span></span> <span data-ttu-id="44eb3-200">括號不在正確的位置。</span><span class="sxs-lookup"><span data-stu-id="44eb3-200">Parenthesis not in right place.</span></span> |
| <span data-ttu-id="44eb3-201">錯誤：設定動態成員資格時發生未知的錯誤。</span><span class="sxs-lookup"><span data-stu-id="44eb3-201">Error: Unknown error occurred during setting up dynamic memberships.</span></span> |<span data-ttu-id="44eb3-202">(user.accountEnabled -eq "True" AND user.userPrincipalName -contains "alias@domain")</span><span class="sxs-lookup"><span data-stu-id="44eb3-202">(user.accountEnabled -eq "True" AND user.userPrincipalName -contains "alias@domain")</span></span> |<span data-ttu-id="44eb3-203">(user.accountEnabled -eq true) -and (user.userPrincipalName -contains "alias@domain")</span><span class="sxs-lookup"><span data-stu-id="44eb3-203">(user.accountEnabled -eq true) -and (user.userPrincipalName -contains "alias@domain")</span></span><br/><span data-ttu-id="44eb3-204">查詢有多個錯誤。</span><span class="sxs-lookup"><span data-stu-id="44eb3-204">Query has multiple errors.</span></span> <span data-ttu-id="44eb3-205">括號不在正確的位置。</span><span class="sxs-lookup"><span data-stu-id="44eb3-205">Parenthesis not in right place.</span></span> |

## <a name="supported-properties"></a><span data-ttu-id="44eb3-206">支援的屬性</span><span class="sxs-lookup"><span data-stu-id="44eb3-206">Supported properties</span></span>
<span data-ttu-id="44eb3-207">hello 以下是您可以使用您的進階規則中的所有 hello 使用者內容：</span><span class="sxs-lookup"><span data-stu-id="44eb3-207">hello following are all hello user properties that you can use in your advanced rule:</span></span>

### <a name="properties-of-type-boolean"></a><span data-ttu-id="44eb3-208">布林型別的屬性</span><span class="sxs-lookup"><span data-stu-id="44eb3-208">Properties of type boolean</span></span>
<span data-ttu-id="44eb3-209">允許的運算子</span><span class="sxs-lookup"><span data-stu-id="44eb3-209">Allowed operators</span></span>

* <span data-ttu-id="44eb3-210">-eq</span><span class="sxs-lookup"><span data-stu-id="44eb3-210">-eq</span></span>
* <span data-ttu-id="44eb3-211">-ne</span><span class="sxs-lookup"><span data-stu-id="44eb3-211">-ne</span></span>

| <span data-ttu-id="44eb3-212">屬性</span><span class="sxs-lookup"><span data-stu-id="44eb3-212">Properties</span></span> | <span data-ttu-id="44eb3-213">允許的值</span><span class="sxs-lookup"><span data-stu-id="44eb3-213">Allowed values</span></span> | <span data-ttu-id="44eb3-214">使用量</span><span class="sxs-lookup"><span data-stu-id="44eb3-214">Usage</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44eb3-215">accountEnabled</span><span class="sxs-lookup"><span data-stu-id="44eb3-215">accountEnabled</span></span> |<span data-ttu-id="44eb3-216">true false</span><span class="sxs-lookup"><span data-stu-id="44eb3-216">true false</span></span> |<span data-ttu-id="44eb3-217">user.accountEnabled -eq true</span><span class="sxs-lookup"><span data-stu-id="44eb3-217">user.accountEnabled -eq true</span></span> |
| <span data-ttu-id="44eb3-218">dirSyncEnabled</span><span class="sxs-lookup"><span data-stu-id="44eb3-218">dirSyncEnabled</span></span> |<span data-ttu-id="44eb3-219">true false</span><span class="sxs-lookup"><span data-stu-id="44eb3-219">true false</span></span> |<span data-ttu-id="44eb3-220">user.dirSyncEnabled -eq true</span><span class="sxs-lookup"><span data-stu-id="44eb3-220">user.dirSyncEnabled -eq true</span></span> |

### <a name="properties-of-type-string"></a><span data-ttu-id="44eb3-221">字串類型的屬性</span><span class="sxs-lookup"><span data-stu-id="44eb3-221">Properties of type string</span></span>
<span data-ttu-id="44eb3-222">允許的運算子</span><span class="sxs-lookup"><span data-stu-id="44eb3-222">Allowed operators</span></span>

* <span data-ttu-id="44eb3-223">-eq</span><span class="sxs-lookup"><span data-stu-id="44eb3-223">-eq</span></span>
* <span data-ttu-id="44eb3-224">-ne</span><span class="sxs-lookup"><span data-stu-id="44eb3-224">-ne</span></span>
* <span data-ttu-id="44eb3-225">-notStartsWith</span><span class="sxs-lookup"><span data-stu-id="44eb3-225">-notStartsWith</span></span>
* <span data-ttu-id="44eb3-226">-startsWith</span><span class="sxs-lookup"><span data-stu-id="44eb3-226">-StartsWith</span></span>
* <span data-ttu-id="44eb3-227">-contains</span><span class="sxs-lookup"><span data-stu-id="44eb3-227">-contains</span></span>
* <span data-ttu-id="44eb3-228">-notContains</span><span class="sxs-lookup"><span data-stu-id="44eb3-228">-notContains</span></span>
* <span data-ttu-id="44eb3-229">-match</span><span class="sxs-lookup"><span data-stu-id="44eb3-229">-match</span></span>
* <span data-ttu-id="44eb3-230">-notMatch</span><span class="sxs-lookup"><span data-stu-id="44eb3-230">-notMatch</span></span>
* <span data-ttu-id="44eb3-231">-in</span><span class="sxs-lookup"><span data-stu-id="44eb3-231">-in</span></span>
* <span data-ttu-id="44eb3-232">-notIn</span><span class="sxs-lookup"><span data-stu-id="44eb3-232">-notIn</span></span>

| <span data-ttu-id="44eb3-233">屬性</span><span class="sxs-lookup"><span data-stu-id="44eb3-233">Properties</span></span> | <span data-ttu-id="44eb3-234">允許的值</span><span class="sxs-lookup"><span data-stu-id="44eb3-234">Allowed values</span></span> | <span data-ttu-id="44eb3-235">使用量</span><span class="sxs-lookup"><span data-stu-id="44eb3-235">Usage</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44eb3-236">city</span><span class="sxs-lookup"><span data-stu-id="44eb3-236">city</span></span> |<span data-ttu-id="44eb3-237">任何字串值或 $null</span><span class="sxs-lookup"><span data-stu-id="44eb3-237">Any string value or $null</span></span> |<span data-ttu-id="44eb3-238">(user.city -eq "value")</span><span class="sxs-lookup"><span data-stu-id="44eb3-238">(user.city -eq "value")</span></span> |
| <span data-ttu-id="44eb3-239">country</span><span class="sxs-lookup"><span data-stu-id="44eb3-239">country</span></span> |<span data-ttu-id="44eb3-240">任何字串值或 $null</span><span class="sxs-lookup"><span data-stu-id="44eb3-240">Any string value or $null</span></span> |<span data-ttu-id="44eb3-241">(user.country -eq "value")</span><span class="sxs-lookup"><span data-stu-id="44eb3-241">(user.country -eq "value")</span></span> |
| <span data-ttu-id="44eb3-242">companyName</span><span class="sxs-lookup"><span data-stu-id="44eb3-242">companyName</span></span> | <span data-ttu-id="44eb3-243">任何字串值或 $null</span><span class="sxs-lookup"><span data-stu-id="44eb3-243">Any string value or $null</span></span> | <span data-ttu-id="44eb3-244">(user.companyName -eq "value")</span><span class="sxs-lookup"><span data-stu-id="44eb3-244">(user.companyName -eq "value")</span></span> |
| <span data-ttu-id="44eb3-245">department</span><span class="sxs-lookup"><span data-stu-id="44eb3-245">department</span></span> |<span data-ttu-id="44eb3-246">任何字串值或 $null</span><span class="sxs-lookup"><span data-stu-id="44eb3-246">Any string value or $null</span></span> |<span data-ttu-id="44eb3-247">(user.department -eq "value")</span><span class="sxs-lookup"><span data-stu-id="44eb3-247">(user.department -eq "value")</span></span> |
| <span data-ttu-id="44eb3-248">displayName</span><span class="sxs-lookup"><span data-stu-id="44eb3-248">displayName</span></span> |<span data-ttu-id="44eb3-249">任何字串值</span><span class="sxs-lookup"><span data-stu-id="44eb3-249">Any string value</span></span> |<span data-ttu-id="44eb3-250">(user.displayName -eq "value")</span><span class="sxs-lookup"><span data-stu-id="44eb3-250">(user.displayName -eq "value")</span></span> |
| <span data-ttu-id="44eb3-251">facsimileTelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="44eb3-251">facsimileTelephoneNumber</span></span> |<span data-ttu-id="44eb3-252">任何字串值或 $null</span><span class="sxs-lookup"><span data-stu-id="44eb3-252">Any string value or $null</span></span> |<span data-ttu-id="44eb3-253">(user.facsimileTelephoneNumber -eq "value")</span><span class="sxs-lookup"><span data-stu-id="44eb3-253">(user.facsimileTelephoneNumber -eq "value")</span></span> |
| <span data-ttu-id="44eb3-254">givenName</span><span class="sxs-lookup"><span data-stu-id="44eb3-254">givenName</span></span> |<span data-ttu-id="44eb3-255">任何字串值或 $null</span><span class="sxs-lookup"><span data-stu-id="44eb3-255">Any string value or $null</span></span> |<span data-ttu-id="44eb3-256">(user.givenName -eq "value")</span><span class="sxs-lookup"><span data-stu-id="44eb3-256">(user.givenName -eq "value")</span></span> |
| <span data-ttu-id="44eb3-257">jobTitle</span><span class="sxs-lookup"><span data-stu-id="44eb3-257">jobTitle</span></span> |<span data-ttu-id="44eb3-258">任何字串值或 $null</span><span class="sxs-lookup"><span data-stu-id="44eb3-258">Any string value or $null</span></span> |<span data-ttu-id="44eb3-259">(user.jobTitle -eq "value")</span><span class="sxs-lookup"><span data-stu-id="44eb3-259">(user.jobTitle -eq "value")</span></span> |
| <span data-ttu-id="44eb3-260">mail</span><span class="sxs-lookup"><span data-stu-id="44eb3-260">mail</span></span> |<span data-ttu-id="44eb3-261">任何字串值或 $null （hello 使用者 SMTP 位址）</span><span class="sxs-lookup"><span data-stu-id="44eb3-261">Any string value or $null (SMTP address of hello user)</span></span> |<span data-ttu-id="44eb3-262">(user.mail -eq "value")</span><span class="sxs-lookup"><span data-stu-id="44eb3-262">(user.mail -eq "value")</span></span> |
| <span data-ttu-id="44eb3-263">mailNickName</span><span class="sxs-lookup"><span data-stu-id="44eb3-263">mailNickName</span></span> |<span data-ttu-id="44eb3-264">任何字串值 （hello 使用者的郵件別名）</span><span class="sxs-lookup"><span data-stu-id="44eb3-264">Any string value (mail alias of hello user)</span></span> |<span data-ttu-id="44eb3-265">(user.mailNickName -eq "value")</span><span class="sxs-lookup"><span data-stu-id="44eb3-265">(user.mailNickName -eq "value")</span></span> |
| <span data-ttu-id="44eb3-266">mobile</span><span class="sxs-lookup"><span data-stu-id="44eb3-266">mobile</span></span> |<span data-ttu-id="44eb3-267">任何字串值或 $null</span><span class="sxs-lookup"><span data-stu-id="44eb3-267">Any string value or $null</span></span> |<span data-ttu-id="44eb3-268">(user.mobile -eq "value")</span><span class="sxs-lookup"><span data-stu-id="44eb3-268">(user.mobile -eq "value")</span></span> |
| <span data-ttu-id="44eb3-269">objectId</span><span class="sxs-lookup"><span data-stu-id="44eb3-269">objectId</span></span> |<span data-ttu-id="44eb3-270">Hello 使用者物件的 GUID</span><span class="sxs-lookup"><span data-stu-id="44eb3-270">GUID of hello user object</span></span> |<span data-ttu-id="44eb3-271">(user.objectId -eq "1111111-1111-1111-1111-111111111111")</span><span class="sxs-lookup"><span data-stu-id="44eb3-271">(user.objectId -eq "1111111-1111-1111-1111-111111111111")</span></span> |
| <span data-ttu-id="44eb3-272">onPremisesSecurityIdentifier</span><span class="sxs-lookup"><span data-stu-id="44eb3-272">onPremisesSecurityIdentifier</span></span> | <span data-ttu-id="44eb3-273">已從同步處理的使用者，在內部部署安全性識別碼 (SID) 內部 toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="44eb3-273">On-premises security identifier (SID) for users who were synchronized from on-premises toohello cloud.</span></span> |<span data-ttu-id="44eb3-274">(user.onPremisesSecurityIdentifier -eq "S-1-1-11-1111111111-1111111111-1111111111-1111111")</span><span class="sxs-lookup"><span data-stu-id="44eb3-274">(user.onPremisesSecurityIdentifier -eq "S-1-1-11-1111111111-1111111111-1111111111-1111111")</span></span> |
| <span data-ttu-id="44eb3-275">passwordPolicies</span><span class="sxs-lookup"><span data-stu-id="44eb3-275">passwordPolicies</span></span> |<span data-ttu-id="44eb3-276">None DisableStrongPassword DisablePasswordExpiration DisablePasswordExpiration, DisableStrongPassword</span><span class="sxs-lookup"><span data-stu-id="44eb3-276">None DisableStrongPassword DisablePasswordExpiration DisablePasswordExpiration, DisableStrongPassword</span></span> |<span data-ttu-id="44eb3-277">(user.passwordPolicies -eq "DisableStrongPassword")</span><span class="sxs-lookup"><span data-stu-id="44eb3-277">(user.passwordPolicies -eq "DisableStrongPassword")</span></span> |
| <span data-ttu-id="44eb3-278">physicalDeliveryOfficeName</span><span class="sxs-lookup"><span data-stu-id="44eb3-278">physicalDeliveryOfficeName</span></span> |<span data-ttu-id="44eb3-279">任何字串值或 $null</span><span class="sxs-lookup"><span data-stu-id="44eb3-279">Any string value or $null</span></span> |<span data-ttu-id="44eb3-280">(user.physicalDeliveryOfficeName -eq "value")</span><span class="sxs-lookup"><span data-stu-id="44eb3-280">(user.physicalDeliveryOfficeName -eq "value")</span></span> |
| <span data-ttu-id="44eb3-281">postalCode</span><span class="sxs-lookup"><span data-stu-id="44eb3-281">postalCode</span></span> |<span data-ttu-id="44eb3-282">任何字串值或 $null</span><span class="sxs-lookup"><span data-stu-id="44eb3-282">Any string value or $null</span></span> |<span data-ttu-id="44eb3-283">(user.postalCode -eq "value")</span><span class="sxs-lookup"><span data-stu-id="44eb3-283">(user.postalCode -eq "value")</span></span> |
| <span data-ttu-id="44eb3-284">preferredLanguage</span><span class="sxs-lookup"><span data-stu-id="44eb3-284">preferredLanguage</span></span> |<span data-ttu-id="44eb3-285">ISO 639-1 code</span><span class="sxs-lookup"><span data-stu-id="44eb3-285">ISO 639-1 code</span></span> |<span data-ttu-id="44eb3-286">(user.preferredLanguage -eq "en-US")</span><span class="sxs-lookup"><span data-stu-id="44eb3-286">(user.preferredLanguage -eq "en-US")</span></span> |
| <span data-ttu-id="44eb3-287">sipProxyAddress</span><span class="sxs-lookup"><span data-stu-id="44eb3-287">sipProxyAddress</span></span> |<span data-ttu-id="44eb3-288">任何字串值或 $null</span><span class="sxs-lookup"><span data-stu-id="44eb3-288">Any string value or $null</span></span> |<span data-ttu-id="44eb3-289">(user.sipProxyAddress -eq "value")</span><span class="sxs-lookup"><span data-stu-id="44eb3-289">(user.sipProxyAddress -eq "value")</span></span> |
| <span data-ttu-id="44eb3-290">state</span><span class="sxs-lookup"><span data-stu-id="44eb3-290">state</span></span> |<span data-ttu-id="44eb3-291">任何字串值或 $null</span><span class="sxs-lookup"><span data-stu-id="44eb3-291">Any string value or $null</span></span> |<span data-ttu-id="44eb3-292">(user.state -eq "value")</span><span class="sxs-lookup"><span data-stu-id="44eb3-292">(user.state -eq "value")</span></span> |
| <span data-ttu-id="44eb3-293">streetAddress</span><span class="sxs-lookup"><span data-stu-id="44eb3-293">streetAddress</span></span> |<span data-ttu-id="44eb3-294">任何字串值或 $null</span><span class="sxs-lookup"><span data-stu-id="44eb3-294">Any string value or $null</span></span> |<span data-ttu-id="44eb3-295">(user.streetAddress -eq "value")</span><span class="sxs-lookup"><span data-stu-id="44eb3-295">(user.streetAddress -eq "value")</span></span> |
| <span data-ttu-id="44eb3-296">surname</span><span class="sxs-lookup"><span data-stu-id="44eb3-296">surname</span></span> |<span data-ttu-id="44eb3-297">任何字串值或 $null</span><span class="sxs-lookup"><span data-stu-id="44eb3-297">Any string value or $null</span></span> |<span data-ttu-id="44eb3-298">(user.surname -eq "value")</span><span class="sxs-lookup"><span data-stu-id="44eb3-298">(user.surname -eq "value")</span></span> |
| <span data-ttu-id="44eb3-299">telephoneNumber</span><span class="sxs-lookup"><span data-stu-id="44eb3-299">telephoneNumber</span></span> |<span data-ttu-id="44eb3-300">任何字串值或 $null</span><span class="sxs-lookup"><span data-stu-id="44eb3-300">Any string value or $null</span></span> |<span data-ttu-id="44eb3-301">(user.telephoneNumber -eq "value")</span><span class="sxs-lookup"><span data-stu-id="44eb3-301">(user.telephoneNumber -eq "value")</span></span> |
| <span data-ttu-id="44eb3-302">usageLocation</span><span class="sxs-lookup"><span data-stu-id="44eb3-302">usageLocation</span></span> |<span data-ttu-id="44eb3-303">兩個字母的國家 (地區) 代碼</span><span class="sxs-lookup"><span data-stu-id="44eb3-303">Two lettered country code</span></span> |<span data-ttu-id="44eb3-304">(user.usageLocation -eq "US")</span><span class="sxs-lookup"><span data-stu-id="44eb3-304">(user.usageLocation -eq "US")</span></span> |
| <span data-ttu-id="44eb3-305">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="44eb3-305">userPrincipalName</span></span> |<span data-ttu-id="44eb3-306">任何字串值</span><span class="sxs-lookup"><span data-stu-id="44eb3-306">Any string value</span></span> |<span data-ttu-id="44eb3-307">(user.userPrincipalName -eq "alias@domain")</span><span class="sxs-lookup"><span data-stu-id="44eb3-307">(user.userPrincipalName -eq "alias@domain")</span></span> |
| <span data-ttu-id="44eb3-308">userType</span><span class="sxs-lookup"><span data-stu-id="44eb3-308">userType</span></span> |<span data-ttu-id="44eb3-309">member guest $null</span><span class="sxs-lookup"><span data-stu-id="44eb3-309">member guest $null</span></span> |<span data-ttu-id="44eb3-310">(user.userType -eq "Member")</span><span class="sxs-lookup"><span data-stu-id="44eb3-310">(user.userType -eq "Member")</span></span> |

### <a name="properties-of-type-string-collection"></a><span data-ttu-id="44eb3-311">字串集合類型的屬性</span><span class="sxs-lookup"><span data-stu-id="44eb3-311">Properties of type string collection</span></span>
<span data-ttu-id="44eb3-312">允許的運算子</span><span class="sxs-lookup"><span data-stu-id="44eb3-312">Allowed operators</span></span>

* <span data-ttu-id="44eb3-313">-contains</span><span class="sxs-lookup"><span data-stu-id="44eb3-313">-contains</span></span>
* <span data-ttu-id="44eb3-314">-notContains</span><span class="sxs-lookup"><span data-stu-id="44eb3-314">-notContains</span></span>

| <span data-ttu-id="44eb3-315">屬性</span><span class="sxs-lookup"><span data-stu-id="44eb3-315">Properties</span></span> | <span data-ttu-id="44eb3-316">允許的值</span><span class="sxs-lookup"><span data-stu-id="44eb3-316">Allowed values</span></span> | <span data-ttu-id="44eb3-317">使用量</span><span class="sxs-lookup"><span data-stu-id="44eb3-317">Usage</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44eb3-318">otherMails</span><span class="sxs-lookup"><span data-stu-id="44eb3-318">otherMails</span></span> |<span data-ttu-id="44eb3-319">任何字串值</span><span class="sxs-lookup"><span data-stu-id="44eb3-319">Any string value</span></span> |<span data-ttu-id="44eb3-320">(user.otherMails -contains "alias@domain")</span><span class="sxs-lookup"><span data-stu-id="44eb3-320">(user.otherMails -contains "alias@domain")</span></span> |
| <span data-ttu-id="44eb3-321">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="44eb3-321">proxyAddresses</span></span> |<span data-ttu-id="44eb3-322">SMTP: alias@domain smtp: alias@domain</span><span class="sxs-lookup"><span data-stu-id="44eb3-322">SMTP: alias@domain smtp: alias@domain</span></span> |<span data-ttu-id="44eb3-323">(user.proxyAddresses -contains "SMTP: alias@domain")</span><span class="sxs-lookup"><span data-stu-id="44eb3-323">(user.proxyAddresses -contains "SMTP: alias@domain")</span></span> |

## <a name="multi-value-properties"></a><span data-ttu-id="44eb3-324">多重值屬性</span><span class="sxs-lookup"><span data-stu-id="44eb3-324">Multi-value properties</span></span>
<span data-ttu-id="44eb3-325">允許的運算子</span><span class="sxs-lookup"><span data-stu-id="44eb3-325">Allowed operators</span></span>

* <span data-ttu-id="44eb3-326">-任何 （滿足 hello 集合中的至少一個項目符合 hello 條件時）</span><span class="sxs-lookup"><span data-stu-id="44eb3-326">-any (satisfied when at least one item in hello collection matches hello condition)</span></span>
* <span data-ttu-id="44eb3-327">-（符合所有 hello 集合中的所有項目符合 hello 條件時）</span><span class="sxs-lookup"><span data-stu-id="44eb3-327">-all (satisfied when all items in hello collection match hello condition)</span></span>

| <span data-ttu-id="44eb3-328">屬性</span><span class="sxs-lookup"><span data-stu-id="44eb3-328">Properties</span></span> | <span data-ttu-id="44eb3-329">值</span><span class="sxs-lookup"><span data-stu-id="44eb3-329">Values</span></span> | <span data-ttu-id="44eb3-330">使用量</span><span class="sxs-lookup"><span data-stu-id="44eb3-330">Usage</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44eb3-331">assignedPlans</span><span class="sxs-lookup"><span data-stu-id="44eb3-331">assignedPlans</span></span> |<span data-ttu-id="44eb3-332">Hello 集合中的每個物件會公開下列字串屬性的 hello: capabilityStatus、 服務、 servicePlanId</span><span class="sxs-lookup"><span data-stu-id="44eb3-332">Each object in hello collection exposes hello following string properties: capabilityStatus, service, servicePlanId</span></span> |<span data-ttu-id="44eb3-333">user.assignedPlans -any (assignedPlan.servicePlanId -eq "efb87545-963c-4e0d-99df-69c6916d9eb0" -and assignedPlan.capabilityStatus -eq "Enabled")</span><span class="sxs-lookup"><span data-stu-id="44eb3-333">user.assignedPlans -any (assignedPlan.servicePlanId -eq "efb87545-963c-4e0d-99df-69c6916d9eb0" -and assignedPlan.capabilityStatus -eq "Enabled")</span></span> |

<span data-ttu-id="44eb3-334">多重值屬性是 hello 之物件的集合相同的型別。</span><span class="sxs-lookup"><span data-stu-id="44eb3-334">Multi-value properties are collections of objects of hello same type.</span></span> <span data-ttu-id="44eb3-335">您可以使用-任何和-所有運算子 tooapply 條件 tooone 或 hello 的所有集合中項目的 hello，分別。</span><span class="sxs-lookup"><span data-stu-id="44eb3-335">You can use -any and -all operators tooapply a condition tooone or all of hello items in hello collection, respectively.</span></span> <span data-ttu-id="44eb3-336">例如：</span><span class="sxs-lookup"><span data-stu-id="44eb3-336">For example:</span></span>

<span data-ttu-id="44eb3-337">assignedPlans 是多重值屬性，其中列出 toohello 使用者指派的所有服務方案。</span><span class="sxs-lookup"><span data-stu-id="44eb3-337">assignedPlans is a multi-value property that lists all service plans assigned toohello user.</span></span> <span data-ttu-id="44eb3-338">hello，下列運算式會選取擁有 hello Exchange Online (計劃 2) 服務計劃也處於啟用狀態的使用者：</span><span class="sxs-lookup"><span data-stu-id="44eb3-338">hello below expression will select users who have hello Exchange Online (Plan 2) service plan that is also in Enabled state:</span></span>

```
user.assignedPlans -any (assignedPlan.servicePlanId -eq "efb87545-963c-4e0d-99df-69c6916d9eb0" -and assignedPlan.capabilityStatus -eq "Enabled")
```

<span data-ttu-id="44eb3-339">（hello Guid 識別碼識別 hello Exchange Online (計劃 2) 的服務方案）。</span><span class="sxs-lookup"><span data-stu-id="44eb3-339">(hello Guid identifier identifies hello Exchange Online (Plan 2) service plan.)</span></span>

> [!NOTE]
> <span data-ttu-id="44eb3-340">這非常有用，如果您想要 tooidentify 所有使用者的 Office 365 （或其他 Microsoft 線上服務） 已啟用功能，如範例 tootarget 其與特定的一組原則。</span><span class="sxs-lookup"><span data-stu-id="44eb3-340">This is useful if you want tooidentify all users for whom an Office 365 (or other Microsoft Online Service) capability has been enabled, for example tootarget them with a certain set of policies.</span></span>

<span data-ttu-id="44eb3-341">hello 下列運算式會選取任何 hello （由服務名稱"SCO"識別） 的 Intune 服務相關聯的服務方案的所有使用者：</span><span class="sxs-lookup"><span data-stu-id="44eb3-341">hello following expression will select all users who have any service plan that is associated with hello Intune service (identified by service name "SCO"):</span></span>
```
user.assignedPlans -any (assignedPlan.service -eq "SCO" -and assignedPlan.capabilityStatus -eq "Enabled")
```

## <a name="use-of-null-values"></a><span data-ttu-id="44eb3-342">使用 Null 值</span><span class="sxs-lookup"><span data-stu-id="44eb3-342">Use of Null values</span></span>

<span data-ttu-id="44eb3-343">toospecify 規則中的 null 值時，您可以使用"null"或 $null。</span><span class="sxs-lookup"><span data-stu-id="44eb3-343">toospecify a null value in a rule, you can use "null" or $null.</span></span> <span data-ttu-id="44eb3-344">範例：</span><span class="sxs-lookup"><span data-stu-id="44eb3-344">Example:</span></span>
```
   user.mail –ne null
```
<span data-ttu-id="44eb3-345">相當於</span><span class="sxs-lookup"><span data-stu-id="44eb3-345">is equivalent to</span></span>
```
   user.mail –ne $null
   ```

## <a name="extension-attributes-and-custom-attributes"></a><span data-ttu-id="44eb3-346">擴充屬性和自訂屬性</span><span class="sxs-lookup"><span data-stu-id="44eb3-346">Extension attributes and custom attributes</span></span>
<span data-ttu-id="44eb3-347">動態成員資格規則支援擴充屬性和自訂屬性。</span><span class="sxs-lookup"><span data-stu-id="44eb3-347">Extension attributes and custom attributes are supported in dynamic membership rules.</span></span>

<span data-ttu-id="44eb3-348">擴充屬性從內部部署 Windows Server AD 同步處理，並採取 hello 格式的"ExtensionAttributeX"，其中 X 等於 1-15。</span><span class="sxs-lookup"><span data-stu-id="44eb3-348">Extension attributes are synced from on-premises Window Server AD and take hello format of "ExtensionAttributeX", where X equals 1 - 15.</span></span>
<span data-ttu-id="44eb3-349">以下是使用擴充屬性的規則範例：</span><span class="sxs-lookup"><span data-stu-id="44eb3-349">An example of a rule that uses an extension attribute would be</span></span>
```
(user.extensionAttribute15 -eq "Marketing")
```
<span data-ttu-id="44eb3-350">從內部部署 Windows Server AD 或連接 SaaS 應用程式與 hello hello 格式的同步處理自訂屬性"user.extension_[GUID]\__ [Attribute]"，其中 [GUID] 是 hello 唯一識別項在 AAD 中的 hello 應用程式，AAD 和 [屬性] 中的建立的 hello 屬性為其建立 hello hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="44eb3-350">Custom Attributes are synced from on-premises Windows Server AD or from a connected SaaS application and hello hello format of "user.extension_[GUID]\__[Attribute]", where [GUID] is hello unique identifier in AAD for hello application that created hello attribute in AAD and [Attribute] is hello name of hello attribute as it was created.</span></span>
<span data-ttu-id="44eb3-351">以下是使用自訂屬性的規則範例：</span><span class="sxs-lookup"><span data-stu-id="44eb3-351">An example of a rule that uses a custom attribute is</span></span>
```
user.extension_c272a57b722d4eb29bfe327874ae79cb__OfficeNumber  
```
<span data-ttu-id="44eb3-352">hello 自訂屬性名稱可以在 hello 目錄藉由查詢使用者的屬性使用圖表總管，並搜尋 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="44eb3-352">hello custom attribute name can be found in hello directory by querying a user's attribute using Graph Explorer and searching for hello attribute name.</span></span>

## <a name="direct-reports-rule"></a><span data-ttu-id="44eb3-353">「直屬員工」規則</span><span class="sxs-lookup"><span data-stu-id="44eb3-353">"Direct Reports" Rule</span></span>
<span data-ttu-id="44eb3-354">您可以建立一個群組，其中包含某位經理的所有直屬員工。</span><span class="sxs-lookup"><span data-stu-id="44eb3-354">You can create a group containing all direct reports of a manager.</span></span> <span data-ttu-id="44eb3-355">當 hello 經理的直屬員工在 hello 未來變更時，會自動調整 hello 群組的成員資格。</span><span class="sxs-lookup"><span data-stu-id="44eb3-355">When hello manager's direct reports change in hello future, hello group's membership will be adjusted automatically.</span></span>

> [!NOTE]
> 1. <span data-ttu-id="44eb3-356">Hello 規則 toowork，請確定 hello**經理識別碼**屬性已正確設定您的租用戶中的使用者。</span><span class="sxs-lookup"><span data-stu-id="44eb3-356">For hello rule toowork, make sure hello **Manager ID** property is set correctly on users in your tenant.</span></span> <span data-ttu-id="44eb3-357">您可以檢查 hello 目前值，使用者在其**設定檔索引標籤**。</span><span class="sxs-lookup"><span data-stu-id="44eb3-357">You can check hello current value for a user on their **Profile tab**.</span></span>
> 2. <span data-ttu-id="44eb3-358">此規則只支援**直屬**員工。</span><span class="sxs-lookup"><span data-stu-id="44eb3-358">This rule only supports **direct** reports.</span></span> <span data-ttu-id="44eb3-359">它是目前不可能 toocreate 的巢狀階層，例如包含直屬員工和其報告的群組的群組。</span><span class="sxs-lookup"><span data-stu-id="44eb3-359">It is currently not possible toocreate a group for a nested hierarchy, e.g. a group that includes direct reports and their reports.</span></span>

<span data-ttu-id="44eb3-360">**tooconfigure hello 群組**</span><span class="sxs-lookup"><span data-stu-id="44eb3-360">**tooconfigure hello group**</span></span>

1. <span data-ttu-id="44eb3-361">遵循的步驟 1-5 從區段[toocreate hello 進階規則](#to-create-the-advanced-rule)，然後選取**成員資格類型**的**動態使用者**。</span><span class="sxs-lookup"><span data-stu-id="44eb3-361">Follow steps 1-5 from section [toocreate hello advanced rule](#to-create-the-advanced-rule), and select a **Membership type** of **Dynamic User**.</span></span>
2. <span data-ttu-id="44eb3-362">在 [hello**動態成員資格規則**刀鋒視窗中，輸入 hello 規則以 hello，請使用下列語法：</span><span class="sxs-lookup"><span data-stu-id="44eb3-362">On hello **Dynamic membership rules** blade, enter hello rule with hello following syntax:</span></span>

    <span data-ttu-id="44eb3-363">*Direct Reports for "{obectID_of_manager}"*</span><span class="sxs-lookup"><span data-stu-id="44eb3-363">*Direct Reports for "{obectID_of_manager}"*</span></span>

    <span data-ttu-id="44eb3-364">有效規則的範例：</span><span class="sxs-lookup"><span data-stu-id="44eb3-364">An example of a valid rule:</span></span>
```
                    Direct Reports for "62e19b97-8b3d-4d4a-a106-4ce66896a863"
```
    where “62e19b97-8b3d-4d4a-a106-4ce66896a863” is hello objectID of hello manager. hello object ID can be found on manager's **Profile tab**.
3. <span data-ttu-id="44eb3-365">在儲存之後 hello 規則，以 hello 的所有使用者都指定 toohello 群組會加入經理識別碼值。</span><span class="sxs-lookup"><span data-stu-id="44eb3-365">After saving hello rule, all users with hello specified Manager ID value will be added toohello group.</span></span>

## <a name="using-attributes-toocreate-rules-for-device-objects"></a><span data-ttu-id="44eb3-366">將裝置物件使用屬性 toocreate 規則</span><span class="sxs-lookup"><span data-stu-id="44eb3-366">Using attributes toocreate rules for device objects</span></span>
<span data-ttu-id="44eb3-367">您也可以建立規則以在群組中選取成員資格的裝置物件。</span><span class="sxs-lookup"><span data-stu-id="44eb3-367">You can also create a rule that selects device objects for membership in a group.</span></span> <span data-ttu-id="44eb3-368">可以使用下列裝置屬性的 hello。</span><span class="sxs-lookup"><span data-stu-id="44eb3-368">hello following device attributes can be used.</span></span>

 <span data-ttu-id="44eb3-369">裝置屬性</span><span class="sxs-lookup"><span data-stu-id="44eb3-369">Device attribute</span></span>  | <span data-ttu-id="44eb3-370">值</span><span class="sxs-lookup"><span data-stu-id="44eb3-370">Values</span></span> | <span data-ttu-id="44eb3-371">範例</span><span class="sxs-lookup"><span data-stu-id="44eb3-371">Example</span></span>
 ----- | ----- | ----------------
 <span data-ttu-id="44eb3-372">accountEnabled</span><span class="sxs-lookup"><span data-stu-id="44eb3-372">accountEnabled</span></span> | <span data-ttu-id="44eb3-373">true false</span><span class="sxs-lookup"><span data-stu-id="44eb3-373">true false</span></span> | <span data-ttu-id="44eb3-374">(device.accountEnabled -eq true)</span><span class="sxs-lookup"><span data-stu-id="44eb3-374">(device.accountEnabled -eq true)</span></span>
 <span data-ttu-id="44eb3-375">displayName</span><span class="sxs-lookup"><span data-stu-id="44eb3-375">displayName</span></span> | <span data-ttu-id="44eb3-376">任何字串值</span><span class="sxs-lookup"><span data-stu-id="44eb3-376">any string value</span></span> |<span data-ttu-id="44eb3-377">(device.displayName -eq "Rob Iphone”)</span><span class="sxs-lookup"><span data-stu-id="44eb3-377">(device.displayName -eq "Rob Iphone”)</span></span>
 <span data-ttu-id="44eb3-378">deviceOSType</span><span class="sxs-lookup"><span data-stu-id="44eb3-378">deviceOSType</span></span> | <span data-ttu-id="44eb3-379">任何字串值</span><span class="sxs-lookup"><span data-stu-id="44eb3-379">any string value</span></span> | <span data-ttu-id="44eb3-380">(device.deviceOSType -eq "IOS")</span><span class="sxs-lookup"><span data-stu-id="44eb3-380">(device.deviceOSType -eq "IOS")</span></span>
 <span data-ttu-id="44eb3-381">deviceOSVersion</span><span class="sxs-lookup"><span data-stu-id="44eb3-381">deviceOSVersion</span></span> | <span data-ttu-id="44eb3-382">任何字串值</span><span class="sxs-lookup"><span data-stu-id="44eb3-382">any string value</span></span> | <span data-ttu-id="44eb3-383">(device.OSVersion -eq "9.1")</span><span class="sxs-lookup"><span data-stu-id="44eb3-383">(device.OSVersion -eq "9.1")</span></span>
 <span data-ttu-id="44eb3-384">deviceCategory</span><span class="sxs-lookup"><span data-stu-id="44eb3-384">deviceCategory</span></span> | <span data-ttu-id="44eb3-385">有效的裝置類別名稱</span><span class="sxs-lookup"><span data-stu-id="44eb3-385">a valid device category name</span></span> | <span data-ttu-id="44eb3-386">(device.deviceCategory -eq "BYOD")</span><span class="sxs-lookup"><span data-stu-id="44eb3-386">(device.deviceCategory -eq "BYOD")</span></span>
 <span data-ttu-id="44eb3-387">deviceManufacturer</span><span class="sxs-lookup"><span data-stu-id="44eb3-387">deviceManufacturer</span></span> | <span data-ttu-id="44eb3-388">任何字串值</span><span class="sxs-lookup"><span data-stu-id="44eb3-388">any string value</span></span> | <span data-ttu-id="44eb3-389">(device.deviceManufacturer -eq "Samsung")</span><span class="sxs-lookup"><span data-stu-id="44eb3-389">(device.deviceManufacturer -eq "Samsung")</span></span>
 <span data-ttu-id="44eb3-390">deviceModel</span><span class="sxs-lookup"><span data-stu-id="44eb3-390">deviceModel</span></span> | <span data-ttu-id="44eb3-391">任何字串值</span><span class="sxs-lookup"><span data-stu-id="44eb3-391">any string value</span></span> | <span data-ttu-id="44eb3-392">(device.deviceModel -eq "iPad Air")</span><span class="sxs-lookup"><span data-stu-id="44eb3-392">(device.deviceModel -eq "iPad Air")</span></span>
 <span data-ttu-id="44eb3-393">deviceOwnership</span><span class="sxs-lookup"><span data-stu-id="44eb3-393">deviceOwnership</span></span> | <span data-ttu-id="44eb3-394">個人、公司</span><span class="sxs-lookup"><span data-stu-id="44eb3-394">Personal, Company</span></span> | <span data-ttu-id="44eb3-395">(device.deviceOwnership -eq "Company")</span><span class="sxs-lookup"><span data-stu-id="44eb3-395">(device.deviceOwnership -eq "Company")</span></span>
 <span data-ttu-id="44eb3-396">domainName</span><span class="sxs-lookup"><span data-stu-id="44eb3-396">domainName</span></span> | <span data-ttu-id="44eb3-397">任何字串值</span><span class="sxs-lookup"><span data-stu-id="44eb3-397">any string value</span></span> | <span data-ttu-id="44eb3-398">(device.domainName -eq "contoso.com")</span><span class="sxs-lookup"><span data-stu-id="44eb3-398">(device.domainName -eq "contoso.com")</span></span>
 <span data-ttu-id="44eb3-399">enrollmentProfileName</span><span class="sxs-lookup"><span data-stu-id="44eb3-399">enrollmentProfileName</span></span> | <span data-ttu-id="44eb3-400">Apple 裝置註冊設定檔名稱</span><span class="sxs-lookup"><span data-stu-id="44eb3-400">Apple Device Enrollment Profile name</span></span> | <span data-ttu-id="44eb3-401">(device.enrollmentProfileName -eq "DEP iPhones")</span><span class="sxs-lookup"><span data-stu-id="44eb3-401">(device.enrollmentProfileName -eq "DEP iPhones")</span></span>
 <span data-ttu-id="44eb3-402">isRooted</span><span class="sxs-lookup"><span data-stu-id="44eb3-402">isRooted</span></span> | <span data-ttu-id="44eb3-403">true false</span><span class="sxs-lookup"><span data-stu-id="44eb3-403">true false</span></span> | <span data-ttu-id="44eb3-404">(device.isRooted -eq true)</span><span class="sxs-lookup"><span data-stu-id="44eb3-404">(device.isRooted -eq true)</span></span>
 <span data-ttu-id="44eb3-405">managementType</span><span class="sxs-lookup"><span data-stu-id="44eb3-405">managementType</span></span> | <span data-ttu-id="44eb3-406">MDM (適用於行動裝置)</span><span class="sxs-lookup"><span data-stu-id="44eb3-406">MDM (for mobile devices)</span></span><br><span data-ttu-id="44eb3-407">（針對 hello Intune 電腦代理程式所管理的電腦） 的電腦</span><span class="sxs-lookup"><span data-stu-id="44eb3-407">PC (for computers managed by hello Intune PC agent)</span></span> | <span data-ttu-id="44eb3-408">(device.managementType -eq "MDM")</span><span class="sxs-lookup"><span data-stu-id="44eb3-408">(device.managementType -eq "MDM")</span></span>
 <span data-ttu-id="44eb3-409">organizationalUnit</span><span class="sxs-lookup"><span data-stu-id="44eb3-409">organizationalUnit</span></span> | <span data-ttu-id="44eb3-410">hello hello 設定內部部署 Active Directory 的組織單位的名稱相符的任何字串值</span><span class="sxs-lookup"><span data-stu-id="44eb3-410">any string value matching hello name of hello organizational unit set by an on-premises Active Directory</span></span> | <span data-ttu-id="44eb3-411">(device.organizationalUnit -eq "US PCs")</span><span class="sxs-lookup"><span data-stu-id="44eb3-411">(device.organizationalUnit -eq "US PCs")</span></span>
 <span data-ttu-id="44eb3-412">deviceId</span><span class="sxs-lookup"><span data-stu-id="44eb3-412">deviceId</span></span> | <span data-ttu-id="44eb3-413">有效的 Azure AD 裝置識別碼</span><span class="sxs-lookup"><span data-stu-id="44eb3-413">a valid Azure AD device ID</span></span> | <span data-ttu-id="44eb3-414">(device.deviceId -eq "d4fe7726-5966-431c-b3b8-cddc8fdb717d")</span><span class="sxs-lookup"><span data-stu-id="44eb3-414">(device.deviceId -eq "d4fe7726-5966-431c-b3b8-cddc8fdb717d")</span></span>
 <span data-ttu-id="44eb3-415">objectId</span><span class="sxs-lookup"><span data-stu-id="44eb3-415">objectId</span></span> | <span data-ttu-id="44eb3-416">有效的 Azure AD 物件識別碼</span><span class="sxs-lookup"><span data-stu-id="44eb3-416">a valid Azure AD object ID</span></span> |  <span data-ttu-id="44eb3-417">(device.objectId -eq 76ad43c9-32c5-45e8-a272-7b58b58f596d")</span><span class="sxs-lookup"><span data-stu-id="44eb3-417">(device.objectId -eq 76ad43c9-32c5-45e8-a272-7b58b58f596d")</span></span>




## <a name="next-steps"></a><span data-ttu-id="44eb3-418">後續步驟</span><span class="sxs-lookup"><span data-stu-id="44eb3-418">Next steps</span></span>
<span data-ttu-id="44eb3-419">這些文章提供有關 Azure Active Directory 中群組的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="44eb3-419">These articles provide additional information on groups in Azure Active Directory.</span></span>

* [<span data-ttu-id="44eb3-420">查看現有的群組</span><span class="sxs-lookup"><span data-stu-id="44eb3-420">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="44eb3-421">建立新群組並新增成員</span><span class="sxs-lookup"><span data-stu-id="44eb3-421">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="44eb3-422">管理群組的設定</span><span class="sxs-lookup"><span data-stu-id="44eb3-422">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="44eb3-423">管理群組的成員資格</span><span class="sxs-lookup"><span data-stu-id="44eb3-423">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="44eb3-424">管理群組中使用者的動態規則</span><span class="sxs-lookup"><span data-stu-id="44eb3-424">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
