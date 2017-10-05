---
title: "登入應用程式時看到非預期的同意提示 | Microsoft Docs"
description: "如何疑難排解使用者會看到已與 Azure AD 整合的應用程式顯示您未預期的同意提示"
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
ms.openlocfilehash: e5b823e1251a7221f73efe6838d439f827f9665d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="unexpected-consent-prompt-when-signing-in-to-an-application"></a><span data-ttu-id="34ff6-103">登入應用程式時看到非預期的同意提示</span><span class="sxs-lookup"><span data-stu-id="34ff6-103">Unexpected consent prompt when signing in to an application</span></span>

<span data-ttu-id="34ff6-104">許多與 Azure Active Directory 整合的應用程式需要各種資源的權限，才能執行。</span><span class="sxs-lookup"><span data-stu-id="34ff6-104">Many applications that integrate with Azure Active Directory require permissions to various resources in order to run.</span></span> <span data-ttu-id="34ff6-105">當這些資源也與 Azure Active Directory 整合時，會使用 Azure AD 同意架構來要求存取這些資源的權限。</span><span class="sxs-lookup"><span data-stu-id="34ff6-105">When these resources are also integrated with Azure Active Directory, permissions to access them is requested using the Azure AD consent framework.</span></span> 

<span data-ttu-id="34ff6-106">這會導致當第一次使用應用程式會一直顯示同意提示，但這通常只應顯示一次。</span><span class="sxs-lookup"><span data-stu-id="34ff6-106">This results in a consent prompt being shown the first time an application is used, which is often a one-time operation.</span></span> 

## <a name="scenarios-in-which-users-see-consent-prompts"></a><span data-ttu-id="34ff6-107">使用者會看到同意提示的案例</span><span class="sxs-lookup"><span data-stu-id="34ff6-107">Scenarios in which users see consent prompts</span></span>

<span data-ttu-id="34ff6-108">還有其他提示預期會在各種案例中發生：</span><span class="sxs-lookup"><span data-stu-id="34ff6-108">Additional prompts can be expected in various scenarios:</span></span>

* <span data-ttu-id="34ff6-109">應用程式需要的權限集已變更。</span><span class="sxs-lookup"><span data-stu-id="34ff6-109">The set of permissions required by the application have changed.</span></span>

* <span data-ttu-id="34ff6-110">原本同意應用程式的使用者不是系統管理員，且現在有不同的使用者 (非系統管理員) 正首次使用應用程式。</span><span class="sxs-lookup"><span data-stu-id="34ff6-110">The user who originally consented to the application was not an administrator, and now a different (non-admin) User is using the application for the first time.</span></span>

* <span data-ttu-id="34ff6-111">原本同意應用程式的使用者為系統管理員，但他們未代表整個組織同意。</span><span class="sxs-lookup"><span data-stu-id="34ff6-111">The user who originally consented to the application was an administrator, but they did not consent on-behalf of the entire organization.</span></span>

* <span data-ttu-id="34ff6-112">在初步獲得同意後，應用程式正在使用 [增量和動態同意](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent)要求其他權限。</span><span class="sxs-lookup"><span data-stu-id="34ff6-112">The application is using [incremental and dynamic consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) to request additional permissions after consent was initially granted.</span></span> <span data-ttu-id="34ff6-113">這通常用於當應用程式的選擇性功能額外需要基礎功能所需權限以外的權限時。</span><span class="sxs-lookup"><span data-stu-id="34ff6-113">This is often used when optional features of an application additional require permissions beyond those required for baseline functionality.</span></span>

* <span data-ttu-id="34ff6-114">在初步獲得同意後，同意遭到撤銷。</span><span class="sxs-lookup"><span data-stu-id="34ff6-114">Consent was revoked after being granted initially.</span></span>

* <span data-ttu-id="34ff6-115">開發人員已設定應用程式在每次使用時都需要同意提示 (注意：這不是最佳做法)。</span><span class="sxs-lookup"><span data-stu-id="34ff6-115">The developer has configured the application to require a consent prompt every time it is used (note: this is not best practice).</span></span>

## <a name="next-steps"></a><span data-ttu-id="34ff6-116">後續步驟</span><span class="sxs-lookup"><span data-stu-id="34ff6-116">Next steps</span></span>

-   [<span data-ttu-id="34ff6-117">Azure Active Directory 中的應用程式、權限及同意 (v1.0 端點)</span><span class="sxs-lookup"><span data-stu-id="34ff6-117">Apps, permissions, and consent in Azure Active Directory (v1.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)

-   [<span data-ttu-id="34ff6-118">Azure Active Directory v2.0 端點中的範圍、權限及同意</span><span class="sxs-lookup"><span data-stu-id="34ff6-118">Scopes, permissions, and consent in the Azure Active Directory (v2.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


