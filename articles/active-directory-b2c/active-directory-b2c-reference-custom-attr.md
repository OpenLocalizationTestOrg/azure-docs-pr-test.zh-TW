---
title: "Azure Active Directory B2C：自訂屬性 | Microsoft Docs"
description: "在您取用者的 Azure Active Directory B2C toocollect 資訊 toouse 自訂屬性是如何"
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
ms.openlocfilehash: fb1bff77ad54c246c6d2f69f39c03eafb76fe6bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-use-custom-attributes-toocollect-information-about-your-consumers"></a><span data-ttu-id="31db4-103">Azure Active Directory B2C： 使用取用者的自訂屬性 toocollect 資訊</span><span class="sxs-lookup"><span data-stu-id="31db4-103">Azure Active Directory B2C: Use custom attributes toocollect information about your consumers</span></span>
<span data-ttu-id="31db4-104">您的 Azure Active Directory (Azure AD) B2C 目錄隨附一組內建資訊 (屬性)：名字、姓氏、城市、郵遞區號及其他屬性。</span><span class="sxs-lookup"><span data-stu-id="31db4-104">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of information (attributes): Given Name, Surname, City, Postal Code, and other attributes.</span></span> <span data-ttu-id="31db4-105">不過，每個消費者導向應用程式都有唯一需求與取用者的哪些屬性 toogather 上。</span><span class="sxs-lookup"><span data-stu-id="31db4-105">However, every consumer-facing application has unique requirements on what attributes toogather from consumers.</span></span> <span data-ttu-id="31db4-106">您可以使用 Azure AD B2C，擴充 hello 組儲存在每個取用者帳戶上的屬性。</span><span class="sxs-lookup"><span data-stu-id="31db4-106">With Azure AD B2C, you can extend hello set of attributes stored on each consumer account.</span></span> <span data-ttu-id="31db4-107">您可以建立自訂的屬性上 hello [Azure 入口網站](https://portal.azure.com/)並將它用於註冊的原則，如下所示。</span><span class="sxs-lookup"><span data-stu-id="31db4-107">You can create custom attributes on hello [Azure portal](https://portal.azure.com/) and use it in your sign-up policies, as shown below.</span></span> <span data-ttu-id="31db4-108">您也可以讀取和寫入這些屬性使用 hello [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="31db4-108">You can also read and write these attributes by using hello [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="31db4-109">自訂屬性會使用 [Azure AD Graph API 目錄結構描述擴充](https://msdn.microsoft.com/library/azure/dn720459.aspx)。</span><span class="sxs-lookup"><span data-stu-id="31db4-109">Custom attributes use [Azure AD Graph API Directory Schema Extensions](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span></span>
> 
> 

## <a name="create-a-custom-attribute"></a><span data-ttu-id="31db4-110">建立自訂屬性</span><span class="sxs-lookup"><span data-stu-id="31db4-110">Create a custom attribute</span></span>
1. <span data-ttu-id="31db4-111">[遵循這些步驟 toonavigate toohello B2C 功能刀鋒視窗上 hello Azure 入口網站](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)。</span><span class="sxs-lookup"><span data-stu-id="31db4-111">[Follow these steps toonavigate toohello B2C features blade on hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="31db4-112">按一下 [使用者屬性] 。</span><span class="sxs-lookup"><span data-stu-id="31db4-112">Click **User attributes**.</span></span>
3. <span data-ttu-id="31db4-113">按一下**+ 加**在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="31db4-113">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="31db4-114">提供**名稱**hello 自訂屬性 (例如，"ShoeSize")，並選擇性地**描述**。</span><span class="sxs-lookup"><span data-stu-id="31db4-114">Provide a **Name** for hello custom attribute (for example, "ShoeSize") and optionally, a **Description**.</span></span> <span data-ttu-id="31db4-115">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="31db4-115">Click **Create**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="31db4-116">只有 hello"String"**資料型別**目前可用。</span><span class="sxs-lookup"><span data-stu-id="31db4-116">Only hello "String" **Data Type** is currently available.</span></span>
   > 
   > 

<span data-ttu-id="31db4-117">hello 自訂屬性現已推出的 hello 清單**使用者屬性**，與在您註冊的原則中使用。</span><span class="sxs-lookup"><span data-stu-id="31db4-117">hello custom attribute is now available in hello list of **User attributes**, and for use in your sign-up policies.</span></span>

## <a name="use-a-custom-attribute-in-your-sign-up-policy"></a><span data-ttu-id="31db4-118">在您的註冊原則中使用自訂屬性</span><span class="sxs-lookup"><span data-stu-id="31db4-118">Use a custom attribute in your sign-up policy</span></span>
1. <span data-ttu-id="31db4-119">[遵循這些步驟 toonavigate toohello B2C 功能刀鋒視窗上 hello Azure 入口網站](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)。</span><span class="sxs-lookup"><span data-stu-id="31db4-119">[Follow these steps toonavigate toohello B2C features blade on hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="31db4-120">按一下 [註冊原則] 。</span><span class="sxs-lookup"><span data-stu-id="31db4-120">Click **Sign-up policies**.</span></span>
3. <span data-ttu-id="31db4-121">按一下 註冊原則 (例如，"B2C_1_SiUp 」) tooopen 它。</span><span class="sxs-lookup"><span data-stu-id="31db4-121">Click your sign-up policy (for example, "B2C_1_SiUp") tooopen it.</span></span> <span data-ttu-id="31db4-122">按一下**編輯**在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="31db4-122">Click **Edit** at hello top of hello blade.</span></span>
4. <span data-ttu-id="31db4-123">按一下**註冊屬性**和選取 hello 自訂屬性 (例如，"ShoeSize")。</span><span class="sxs-lookup"><span data-stu-id="31db4-123">Click **Sign-up attributes** and select hello custom attribute (for example, "ShoeSize").</span></span> <span data-ttu-id="31db4-124">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="31db4-124">Click **OK**.</span></span>
5. <span data-ttu-id="31db4-125">按一下**應用程式宣告**和選取 hello 自訂屬性。</span><span class="sxs-lookup"><span data-stu-id="31db4-125">Click **Application claims** and select hello custom attribute.</span></span> <span data-ttu-id="31db4-126">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="31db4-126">Click **OK**.</span></span>
6. <span data-ttu-id="31db4-127">按一下**儲存**在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="31db4-127">Click **Save** at hello top of hello blade.</span></span>

<span data-ttu-id="31db4-128">您可以使用 hello 「 立即執行 」 功能 hello 原則 tooverify hello 取用者經驗。</span><span class="sxs-lookup"><span data-stu-id="31db4-128">You can use hello "Run now" feature on hello policy tooverify hello consumer experience.</span></span> <span data-ttu-id="31db4-129">您現在應該看到 「 ShoeSize"hello 註冊時，取用者期間所收集的屬性清單中，並查看它的 hello 語彙基元傳送後 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="31db4-129">You should now see "ShoeSize" in hello list of attributes collected during consumer sign-up, and see it in hello token sent back tooyour application.</span></span>

## <a name="notes"></a><span data-ttu-id="31db4-130">注意事項</span><span class="sxs-lookup"><span data-stu-id="31db4-130">Notes</span></span>
* <span data-ttu-id="31db4-131">除了註冊原則，自訂屬性也可以使用於註冊或登入原則和設定檔編輯原則。</span><span class="sxs-lookup"><span data-stu-id="31db4-131">Along with sign-up policies, custom attributes can also be used in sign-up or sign-in policies and profile editing policies.</span></span>
* <span data-ttu-id="31db4-132">自訂屬性有已知的限制。</span><span class="sxs-lookup"><span data-stu-id="31db4-132">There is a known limitation of custom attributes.</span></span> <span data-ttu-id="31db4-133">當這個選項只有在任何原則中，使用它的第一次建立 hello 不加入 toohello 清單**使用者屬性**。</span><span class="sxs-lookup"><span data-stu-id="31db4-133">It is only created hello first time it is used in any policy, and not when you add it toohello list of **User attributes**.</span></span>

