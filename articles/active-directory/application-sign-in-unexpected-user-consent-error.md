---
title: "aaa 未預期的錯誤時執行的應用程式同意 tooan |Microsoft 文件"
description: "討論在 hello 同意 tooan 應用程式和您可以執行這些程序期間可能發生的錯誤"
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
ms.openlocfilehash: dfee35f3a10e3cc4313109cedd972499452320f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-error-when-performing-consent-tooan-application"></a><span data-ttu-id="e7c24-103">執行同意 tooan 應用程式時發生非預期的錯誤</span><span class="sxs-lookup"><span data-stu-id="e7c24-103">Unexpected error when performing consent tooan application</span></span>

<span data-ttu-id="e7c24-104">這篇文章討論 hello 同意 tooan 應用程式的程序期間可能發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="e7c24-104">This article discusses errors that can occur during hello process of consenting tooan application.</span></span> <span data-ttu-id="e7c24-105">如果您正在疑難排解未包含任何錯誤訊息的非預期同意提示，請參閱 [Azure AD 的驗證案例](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)。</span><span class="sxs-lookup"><span data-stu-id="e7c24-105">If you are Troubleshoot unexpected consent prompts that do not contain any error messages, see [Authentication Scenarios for Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios).</span></span>

<span data-ttu-id="e7c24-106">許多與 Azure Active Directory 整合的應用程式需要的權限 tooaccess toofunction 順序中的其他資源。</span><span class="sxs-lookup"><span data-stu-id="e7c24-106">Many applications that integrate with Azure Active Directory require permissions tooaccess other resources in order toofunction.</span></span> <span data-ttu-id="e7c24-107">當這些資源也會與 Azure Active Directory 整合時，它們通常要求使用 hello 常見的權限 tooaccess 同意架構。</span><span class="sxs-lookup"><span data-stu-id="e7c24-107">When these resources are also integrated with Azure Active Directory, permissions tooaccess them is often requested using hello common consent framework.</span></span> 

<span data-ttu-id="e7c24-108">這會導致同意提示顯示，這通常就會發生 hello 第一次使用應用程式，但也會發生在 hello 應用程式的後續使用。</span><span class="sxs-lookup"><span data-stu-id="e7c24-108">This results in a consent prompt being displayed, which generally occurs hello first time an application is used but can also occur on a subsequent use of hello application.</span></span>

<span data-ttu-id="e7c24-109">某些條件必須為應用程式需要使用者 tooconsent toohello 權限，則為 true。</span><span class="sxs-lookup"><span data-stu-id="e7c24-109">Certain conditions must be true for a user tooconsent toohello permissions an application requires.</span></span> <span data-ttu-id="e7c24-110">如果不符合這些條件，便會發生各種錯誤。</span><span class="sxs-lookup"><span data-stu-id="e7c24-110">If these conditions are not met, various errors can occur.</span></span> <span data-ttu-id="e7c24-111">其中包含：</span><span class="sxs-lookup"><span data-stu-id="e7c24-111">These include:</span></span>

## <a name="requesting-not-authorized-permissions-error"></a><span data-ttu-id="e7c24-112">要求未經授權權限的錯誤</span><span class="sxs-lookup"><span data-stu-id="e7c24-112">Requesting not authorized permissions error</span></span>
* <span data-ttu-id="e7c24-113">**AADSTS90093:** &lt;clientAppDisplayName&gt;不是您的一個或多個權限授權 toogrant 要求。</span><span class="sxs-lookup"><span data-stu-id="e7c24-113">**AADSTS90093:** &lt;clientAppDisplayName&gt; is requesting one or more permissions that you are not authorized toogrant.</span></span> <span data-ttu-id="e7c24-114">請連絡的系統管理員可以同意 toothis 代表您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e7c24-114">Contact an administrator, who can consent toothis application on your behalf.</span></span>

<span data-ttu-id="e7c24-115">不是公司系統管理員的使用者嘗試 toouse 要求只有系統管理員可以授與的權限的應用程式時，就會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="e7c24-115">This error occurs when a user who is not a company administrator attempts toouse an application that is requesting permissions that only an administrator can grant.</span></span> <span data-ttu-id="e7c24-116">授與存取 toohello 應用程式，代表其組織的系統管理員，可以解決這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="e7c24-116">This error can be resolved by an administrator granting access toohello application on behalf of their organization.</span></span>

## <a name="policy-prevents-granting-permissions-error"></a><span data-ttu-id="e7c24-117">原則禁止授與權限錯誤</span><span class="sxs-lookup"><span data-stu-id="e7c24-117">Policy prevents granting permissions error</span></span>
* <span data-ttu-id="e7c24-118">**AADSTS90093:**的系統管理員&lt;tenantDisplayName&gt;已經設定原則，使您無法授與&lt;的應用程式名稱&gt;hello 對於要求的權限。</span><span class="sxs-lookup"><span data-stu-id="e7c24-118">**AADSTS90093:** An administrator of &lt;tenantDisplayName&gt; has set a policy that prevents you from granting &lt;name of app&gt; hello permissions it is requesting.</span></span> <span data-ttu-id="e7c24-119">請連絡系統管理員&lt;tenantDisplayName&gt;，使用者可以授與權限 toothis 應用程式代表您。</span><span class="sxs-lookup"><span data-stu-id="e7c24-119">Contact an administrator of &lt;tenantDisplayName&gt;, who can grant permissions toothis app on your behalf.</span></span>

<span data-ttu-id="e7c24-120">發生此錯誤時公司系統管理員會關閉使用者 tooconsent tooapplications，hello 能力則非系統管理員使用者嘗試 toouse 需要同意的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e7c24-120">This error occurs when a company administrator turns off hello ability for users tooconsent tooapplications, then a non-administrator user attempts toouse an application that requires consent.</span></span> <span data-ttu-id="e7c24-121">授與存取 toohello 應用程式，代表其組織的系統管理員，可以解決這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="e7c24-121">This error can be resolved by an administrator granting access toohello application on behalf of their organization.</span></span>

## <a name="intermittent-problem-error"></a><span data-ttu-id="e7c24-122">間歇性問題錯誤</span><span class="sxs-lookup"><span data-stu-id="e7c24-122">Intermittent problem error</span></span>
* <span data-ttu-id="e7c24-123">**AADSTS90090:**我們遇到錄製您太嘗試 toogrant hello 權限的間歇性問題似乎&lt;clientAppDisplayName&gt;。</span><span class="sxs-lookup"><span data-stu-id="e7c24-123">**AADSTS90090:** It looks like we encountered an intermittent problem recording hello permissions you attempted toogrant too&lt;clientAppDisplayName&gt;.</span></span> <span data-ttu-id="e7c24-124">請稍後再試一次。</span><span class="sxs-lookup"><span data-stu-id="e7c24-124">try again later.</span></span>

<span data-ttu-id="e7c24-125">此錯誤表示已發生間歇性服務端問題。</span><span class="sxs-lookup"><span data-stu-id="e7c24-125">This error indicates that an intermittent service side issue has occurred.</span></span> <span data-ttu-id="e7c24-126">它可以解決方法是嘗試再次 tooconsent toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e7c24-126">It can be resolved by attempting tooconsent toohello application again.</span></span>

## <a name="resource-not-available-error"></a><span data-ttu-id="e7c24-127">資源無法使用錯誤</span><span class="sxs-lookup"><span data-stu-id="e7c24-127">Resource not available error</span></span>
* <span data-ttu-id="e7c24-128">**AADSTS65005:** hello 應用程式&lt;clientAppDisplayName&gt;要求資源的權限 tooaccess &lt;resourceAppDisplayName&gt;未提供的。</span><span class="sxs-lookup"><span data-stu-id="e7c24-128">**AADSTS65005:** hello app &lt;clientAppDisplayName&gt; requested permissions tooaccess a resource &lt;resourceAppDisplayName&gt; that is not available.</span></span> 

<span data-ttu-id="e7c24-129">請連絡 hello 應用程式開發人員。</span><span class="sxs-lookup"><span data-stu-id="e7c24-129">Contact hello application developer.</span></span>

##  <a name="resource-not-available-in-tenant-error"></a><span data-ttu-id="e7c24-130">資源在租用戶無法使用錯誤</span><span class="sxs-lookup"><span data-stu-id="e7c24-130">Resource not available in tenant error</span></span>
* <span data-ttu-id="e7c24-131">**AADSTS65005:** &lt;clientAppDisplayName&gt;要求存取 tooa 資源&lt;resourceAppDisplayName&gt;未提供您組織中的&lt;tenantDisplayName&gt;。</span><span class="sxs-lookup"><span data-stu-id="e7c24-131">**AADSTS65005:** &lt;clientAppDisplayName&gt; is requesting access tooa resource &lt;resourceAppDisplayName&gt; that is not available in your organization &lt;tenantDisplayName&gt;.</span></span> 

<span data-ttu-id="e7c24-132">請確認此資源可以使用，或與 &lt;tenantDisplayName&gt; 的系統管理員連絡。</span><span class="sxs-lookup"><span data-stu-id="e7c24-132">Ensure that this resource is available or contact an administrator of &lt;tenantDisplayName&gt;.</span></span>

## <a name="permissions-mismatch-error"></a><span data-ttu-id="e7c24-133">權限不符合錯誤</span><span class="sxs-lookup"><span data-stu-id="e7c24-133">Permissions mismatch error</span></span>
* <span data-ttu-id="e7c24-134">**AADSTS65005:** hello 應用程式要求的同意 tooaccess 資源&lt;resourceAppDisplayName&gt;。</span><span class="sxs-lookup"><span data-stu-id="e7c24-134">**AADSTS65005:** hello app requested consent tooaccess resource &lt;resourceAppDisplayName&gt;.</span></span> <span data-ttu-id="e7c24-135">此要求失敗，因為它不符合如何 hello 應用程式已預先設定的應用程式登錄期間。</span><span class="sxs-lookup"><span data-stu-id="e7c24-135">This request failed because it does not match how hello app was pre-configured during app registration.</span></span> <span data-ttu-id="e7c24-136">請連絡 hello 應用程式 vendor.* *</span><span class="sxs-lookup"><span data-stu-id="e7c24-136">Contact hello app vendor.**</span></span>

<span data-ttu-id="e7c24-137">Hello 應用程式的使用者嘗試 tooconsent toois 要求權限 tooaccess hello 組織的目錄 （租用戶） 中找不到資源應用程式時，就會發生所有這些錯誤。</span><span class="sxs-lookup"><span data-stu-id="e7c24-137">These errors all occur when hello application a user is trying tooconsent toois requesting permissions tooaccess a resource application that cannot be found in hello organization’s directory (tenant).</span></span> <span data-ttu-id="e7c24-138">發生的原因有數種：</span><span class="sxs-lookup"><span data-stu-id="e7c24-138">This can occur for several reasons:</span></span>

-   <span data-ttu-id="e7c24-139">hello 用戶端應用程式開發人員已將設定其應用程式不正確，造成它 toorequest 存取 tooan 無效的資源。</span><span class="sxs-lookup"><span data-stu-id="e7c24-139">hello client application developer has configured their application incorrectly, causing it toorequest access tooan invalid resource.</span></span> <span data-ttu-id="e7c24-140">在此情況下，hello 應用程式開發人員就必須更新 hello 組態的 hello 用戶端應用程式 tooresolve 此問題。</span><span class="sxs-lookup"><span data-stu-id="e7c24-140">In this case, hello application developer must update hello configuration of hello client application tooresolve this issue.</span></span>

-   <span data-ttu-id="e7c24-141">服務主體代表 hello 目標資源應用程式不存在於 hello 組織或存在於過去 hello 但已被移除。</span><span class="sxs-lookup"><span data-stu-id="e7c24-141">A Service Principal representing hello target resource application does not exist in hello organization, or existed in hello past but has been removed.</span></span> <span data-ttu-id="e7c24-142">這個問題，請將服務主體的 hello 資源應用程式中必須提供 hello 組織讓 hello 用戶端應用程式可以要求權限 tooit tooresolve。</span><span class="sxs-lookup"><span data-stu-id="e7c24-142">tooresolve this issue, a Service Principal for hello resource application must be provisioned in hello organization so hello client application can request permissions tooit.</span></span> <span data-ttu-id="e7c24-143">這可能會發生數種方式，取決於 hello 類型的應用程式，包括：</span><span class="sxs-lookup"><span data-stu-id="e7c24-143">This can happen in an number of ways, depending on hello type of application, including:</span></span>

    -   <span data-ttu-id="e7c24-144">取得訂用帳戶的 hello 資源應用程式 （Microsoft 所發行的應用程式）</span><span class="sxs-lookup"><span data-stu-id="e7c24-144">Acquiring a subscription for hello resource application (Microsoft published applications)</span></span>

    -   <span data-ttu-id="e7c24-145">同意 toohello 資源應用程式</span><span class="sxs-lookup"><span data-stu-id="e7c24-145">Consenting toohello resource application</span></span>

    -   <span data-ttu-id="e7c24-146">授與 hello 透過 hello Azure 入口網站的應用程式權限</span><span class="sxs-lookup"><span data-stu-id="e7c24-146">Granting hello application permissions via hello Azure Portal</span></span>

    -   <span data-ttu-id="e7c24-147">從 hello Azure AD 應用程式庫加入 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="e7c24-147">Adding hello application from hello Azure AD Application Gallery</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7c24-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e7c24-148">Next steps</span></span> 

[<span data-ttu-id="e7c24-149">Azure Active Directory 中的應用程式、權限及同意 (v1 端點)</span><span class="sxs-lookup"><span data-stu-id="e7c24-149">Apps, permissions, and consent in Azure Active Directory (v1 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)<br>

[<span data-ttu-id="e7c24-150">範圍、 權限，以及在 hello Azure Active Directory （v2.0 端點） 中同意</span><span class="sxs-lookup"><span data-stu-id="e7c24-150">Scopes, permissions, and consent in hello Azure Active Directory (v2.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


