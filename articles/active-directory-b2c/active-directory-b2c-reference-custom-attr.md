---
title: "Azure Active Directory B2C：自訂屬性 | Microsoft Docs"
description: "如何在 Azure Active Directory B2C 中使用自訂屬性收集取用者相關資訊"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 055ffb0a-197b-4716-8dad-1fd8a01e174f
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 356aaeff3a78fc7b682d621e8e0de9312582b2fe
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-use-custom-attributes-to-collect-information-about-your-consumers"></a><span data-ttu-id="fe2b2-103">Azure Active Directory B2C：使用自訂屬性收集您的取用者的相關資訊</span><span class="sxs-lookup"><span data-stu-id="fe2b2-103">Azure Active Directory B2C: Use custom attributes to collect information about your consumers</span></span>
<span data-ttu-id="fe2b2-104">您的 Azure Active Directory (Azure AD) B2C 目錄隨附一組內建資訊 (屬性)：名字、姓氏、城市、郵遞區號及其他屬性。</span><span class="sxs-lookup"><span data-stu-id="fe2b2-104">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of information (attributes): Given Name, Surname, City, Postal Code, and other attributes.</span></span> <span data-ttu-id="fe2b2-105">不過，每個取用者面向應用程式對於向取用者收集的屬性，皆有獨特需求。</span><span class="sxs-lookup"><span data-stu-id="fe2b2-105">However, every consumer-facing application has unique requirements on what attributes to gather from consumers.</span></span> <span data-ttu-id="fe2b2-106">Azure AD B2C 可讓您擴充目錄儲存在每個取用者帳戶上的屬性組合。</span><span class="sxs-lookup"><span data-stu-id="fe2b2-106">With Azure AD B2C, you can extend the set of attributes stored on each consumer account.</span></span> <span data-ttu-id="fe2b2-107">您可以在 [Azure 入口網站](https://portal.azure.com/) 上建立自訂屬性，然後如下方所示，將這些屬性用於您的註冊原則中。</span><span class="sxs-lookup"><span data-stu-id="fe2b2-107">You can create custom attributes on the [Azure portal](https://portal.azure.com/) and use it in your sign-up policies, as shown below.</span></span> <span data-ttu-id="fe2b2-108">您也可以使用 [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md)讀取和寫入這些屬性。</span><span class="sxs-lookup"><span data-stu-id="fe2b2-108">You can also read and write these attributes by using the [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="fe2b2-109">自訂屬性會使用 [Azure AD Graph API 目錄結構描述擴充](https://msdn.microsoft.com/library/azure/dn720459.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fe2b2-109">Custom attributes use [Azure AD Graph API Directory Schema Extensions](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span></span>
> 
> 

## <a name="create-a-custom-attribute"></a><span data-ttu-id="fe2b2-110">建立自訂屬性</span><span class="sxs-lookup"><span data-stu-id="fe2b2-110">Create a custom attribute</span></span>
1. <span data-ttu-id="fe2b2-111">遵循下列步驟以[瀏覽至 B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) (位於 Azure 入口網站上)。</span><span class="sxs-lookup"><span data-stu-id="fe2b2-111">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="fe2b2-112">按一下 [使用者屬性] 。</span><span class="sxs-lookup"><span data-stu-id="fe2b2-112">Click **User attributes**.</span></span>
3. <span data-ttu-id="fe2b2-113">按一下刀鋒視窗頂端的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="fe2b2-113">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="fe2b2-114">提供自訂屬性的**名稱** (例如 "ShoeSize") 和**說明** (選擇性)。</span><span class="sxs-lookup"><span data-stu-id="fe2b2-114">Provide a **Name** for the custom attribute (for example, "ShoeSize") and optionally, a **Description**.</span></span> <span data-ttu-id="fe2b2-115">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="fe2b2-115">Click **Create**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="fe2b2-116">目前僅提供「字串」 **資料類型** 。</span><span class="sxs-lookup"><span data-stu-id="fe2b2-116">Only the "String" **Data Type** is currently available.</span></span>
   > 
   > 

<span data-ttu-id="fe2b2-117">**使用者屬性**清單現已提供自訂屬性，您可用於註冊原則中。</span><span class="sxs-lookup"><span data-stu-id="fe2b2-117">The custom attribute is now available in the list of **User attributes**, and for use in your sign-up policies.</span></span>

## <a name="use-a-custom-attribute-in-your-sign-up-policy"></a><span data-ttu-id="fe2b2-118">在您的註冊原則中使用自訂屬性</span><span class="sxs-lookup"><span data-stu-id="fe2b2-118">Use a custom attribute in your sign-up policy</span></span>
1. <span data-ttu-id="fe2b2-119">遵循下列步驟以[瀏覽至 B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) (位於 Azure 入口網站上)。</span><span class="sxs-lookup"><span data-stu-id="fe2b2-119">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="fe2b2-120">按一下 [註冊原則] 。</span><span class="sxs-lookup"><span data-stu-id="fe2b2-120">Click **Sign-up policies**.</span></span>
3. <span data-ttu-id="fe2b2-121">按一下以開啟註冊原則 (例如 "B2C_1_SiUp")。</span><span class="sxs-lookup"><span data-stu-id="fe2b2-121">Click your sign-up policy (for example, "B2C_1_SiUp") to open it.</span></span> <span data-ttu-id="fe2b2-122">按一下刀鋒視窗頂端的 [編輯]  。</span><span class="sxs-lookup"><span data-stu-id="fe2b2-122">Click **Edit** at the top of the blade.</span></span>
4. <span data-ttu-id="fe2b2-123">按一下 [註冊屬性]  ，然後選取自訂屬性 (例如「ShoeSize」)。</span><span class="sxs-lookup"><span data-stu-id="fe2b2-123">Click **Sign-up attributes** and select the custom attribute (for example, "ShoeSize").</span></span> <span data-ttu-id="fe2b2-124">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="fe2b2-124">Click **OK**.</span></span>
5. <span data-ttu-id="fe2b2-125">按一下 [應用程式宣告]  ，然後選取自訂屬性。</span><span class="sxs-lookup"><span data-stu-id="fe2b2-125">Click **Application claims** and select the custom attribute.</span></span> <span data-ttu-id="fe2b2-126">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="fe2b2-126">Click **OK**.</span></span>
6. <span data-ttu-id="fe2b2-127">按一下刀鋒視窗頂端的 [儲存]  。</span><span class="sxs-lookup"><span data-stu-id="fe2b2-127">Click **Save** at the top of the blade.</span></span>

<span data-ttu-id="fe2b2-128">您可以使用原則上的「立即執行」功能來驗證取用者體驗。</span><span class="sxs-lookup"><span data-stu-id="fe2b2-128">You can use the "Run now" feature on the policy to verify the consumer experience.</span></span> <span data-ttu-id="fe2b2-129">現在您應會在於取用者註冊期間收集之屬性的清單中看到「ShoeSize」，其亦會在傳回至您應用程式的權杖中出現。</span><span class="sxs-lookup"><span data-stu-id="fe2b2-129">You should now see "ShoeSize" in the list of attributes collected during consumer sign-up, and see it in the token sent back to your application.</span></span>

## <a name="notes"></a><span data-ttu-id="fe2b2-130">注意事項</span><span class="sxs-lookup"><span data-stu-id="fe2b2-130">Notes</span></span>
* <span data-ttu-id="fe2b2-131">除了註冊原則，自訂屬性也可以使用於註冊或登入原則和設定檔編輯原則。</span><span class="sxs-lookup"><span data-stu-id="fe2b2-131">Along with sign-up policies, custom attributes can also be used in sign-up or sign-in policies and profile editing policies.</span></span>
* <span data-ttu-id="fe2b2-132">自訂屬性有已知的限制。</span><span class="sxs-lookup"><span data-stu-id="fe2b2-132">There is a known limitation of custom attributes.</span></span> <span data-ttu-id="fe2b2-133">只有在第一次用於任何原則時才會建立，而不是在您將它加入至 [使用者屬性] 清單時建立。</span><span class="sxs-lookup"><span data-stu-id="fe2b2-133">It is only created the first time it is used in any policy, and not when you add it to the list of **User attributes**.</span></span>

