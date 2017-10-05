---
title: "如何為自訂開發的應用程式變更權杖存留期預設值 | Microsoft Docs"
description: "如何為針對 Azure AD 開發的應用程式更新權杖存留期原則"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: a28eacd820ed28a6470992ce86b060e886c00bcb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-change-the-token-lifetime-defaults-for-a-custom-developed-application"></a><span data-ttu-id="50a4e-103">如何為自訂開發的應用程式變更權杖存留期預設值</span><span class="sxs-lookup"><span data-stu-id="50a4e-103">How to change the token lifetime defaults for a custom-developed application</span></span>

<span data-ttu-id="50a4e-104">Azure AD Premium 可讓應用程式開發人員與租用戶系統管理員為針對非機密用戶端簽發的權杖設定存留期。</span><span class="sxs-lookup"><span data-stu-id="50a4e-104">Azure AD Premium allows app developers and tenant admins to configure the lifetime of tokens issued for non-confidential clients.</span></span> <span data-ttu-id="50a4e-105">權杖存留期原則是以整個租用戶為基礎所設定，或針對要存取的資源所設定。</span><span class="sxs-lookup"><span data-stu-id="50a4e-105">Token lifetime policies are set on a tenant-wide basis or the resources being accessed.</span></span>

 * <span data-ttu-id="50a4e-106">若要設定權杖存留期原則，您必須下載 [Azure AD PowerShell 模組 (英文)](https://www.powershellgallery.com/packages/AzureADPreview)。</span><span class="sxs-lookup"><span data-stu-id="50a4e-106">To set a token lifetime policy, you need to download the [Azure AD PowerShell Module](https://www.powershellgallery.com/packages/AzureADPreview).</span></span>

 * <span data-ttu-id="50a4e-107">執行 **Connect-AzureAD -Confirm** 命令。</span><span class="sxs-lookup"><span data-stu-id="50a4e-107">Run the **Connect-AzureAD -Confirm** command.</span></span>

 * <span data-ttu-id="50a4e-108">下列範例原則會設定單一要素重新整理權杖存留期上限。</span><span class="sxs-lookup"><span data-stu-id="50a4e-108">Here’s an example policy that sets the max age single factor refresh token.</span></span> <span data-ttu-id="50a4e-109">建立原則：```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span><span class="sxs-lookup"><span data-stu-id="50a4e-109">Create the policy: ```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span></span>

 * <span data-ttu-id="50a4e-110">請參閱[設定權杖存留期](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)一文，以了解如何建立其他自訂。</span><span class="sxs-lookup"><span data-stu-id="50a4e-110">Checkout the [Configuring token lifetime](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)   document to learn how to create other custom.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50a4e-111">後續步驟</span><span class="sxs-lookup"><span data-stu-id="50a4e-111">Next steps</span></span>
[<span data-ttu-id="50a4e-112">設定權杖存留期</span><span class="sxs-lookup"><span data-stu-id="50a4e-112">Configuring Token Lifetime</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)<br>

[<span data-ttu-id="50a4e-113">Azure AD 權杖參考</span><span class="sxs-lookup"><span data-stu-id="50a4e-113">Azure AD Token Reference</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-token-and-claims)

