---
title: "針對自訂開發的應用程式預設 aaaHow toochange hello 權杖存留期 |Microsoft 文件"
description: "如何在 Azure AD，您所開發的應用程式的 tooupdate 權杖存留期原則"
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
ms.openlocfilehash: 6e1aa1f2a7c33c1f55c5fb619c618ad43cd96273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochange-hello-token-lifetime-defaults-for-a-custom-developed-application"></a><span data-ttu-id="b72f1-103">Toochange hello 權杖存留期的自訂開發的應用程式的預設值</span><span class="sxs-lookup"><span data-stu-id="b72f1-103">How toochange hello token lifetime defaults for a custom-developed application</span></span>

<span data-ttu-id="b72f1-104">Azure AD Premium 可讓應用程式開發人員和租用戶系統管理員 」 tooconfigure hello 存留期的非機密用戶端簽發的權杖。</span><span class="sxs-lookup"><span data-stu-id="b72f1-104">Azure AD Premium allows app developers and tenant admins tooconfigure hello lifetime of tokens issued for non-confidential clients.</span></span> <span data-ttu-id="b72f1-105">權杖存留期原則會設定租用戶通用的原則或 hello 資源清單。</span><span class="sxs-lookup"><span data-stu-id="b72f1-105">Token lifetime policies are set on a tenant-wide basis or hello resources being accessed.</span></span>

 * <span data-ttu-id="b72f1-106">tooset 權杖存留期原則，您需要 toodownload hello [Azure AD PowerShell 模組](https://www.powershellgallery.com/packages/AzureADPreview)。</span><span class="sxs-lookup"><span data-stu-id="b72f1-106">tooset a token lifetime policy, you need toodownload hello [Azure AD PowerShell Module](https://www.powershellgallery.com/packages/AzureADPreview).</span></span>

 * <span data-ttu-id="b72f1-107">執行 hello**連接 azure Ad-確認**命令。</span><span class="sxs-lookup"><span data-stu-id="b72f1-107">Run hello **Connect-AzureAD -Confirm** command.</span></span>

 * <span data-ttu-id="b72f1-108">以下是範例原則，設定 hello 最大存留期的一項因素重新整理語彙基元。</span><span class="sxs-lookup"><span data-stu-id="b72f1-108">Here’s an example policy that sets hello max age single factor refresh token.</span></span> <span data-ttu-id="b72f1-109">建立 hello 原則：```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span><span class="sxs-lookup"><span data-stu-id="b72f1-109">Create hello policy: ```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span></span>

 * <span data-ttu-id="b72f1-110">簽出 hello[設定權杖存留期](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)如何文件 toolearn toocreate 其他自訂。</span><span class="sxs-lookup"><span data-stu-id="b72f1-110">Checkout hello [Configuring token lifetime](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)   document toolearn how toocreate other custom.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b72f1-111">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b72f1-111">Next steps</span></span>
[<span data-ttu-id="b72f1-112">設定權杖存留期</span><span class="sxs-lookup"><span data-stu-id="b72f1-112">Configuring Token Lifetime</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)<br>

[<span data-ttu-id="b72f1-113">Azure AD 權杖參考</span><span class="sxs-lookup"><span data-stu-id="b72f1-113">Azure AD Token Reference</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-token-and-claims)

