---
title: "對應用程式執行同意時發生非預期的錯誤 | Microsoft Docs"
description: "討論對應用程式執行同意的程序期間會發生的錯誤，以及可對錯誤採取的動作"
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
ms.openlocfilehash: fd500fdd4c8642bad96dcf71eebcf1fad461a35f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="unexpected-error-when-performing-consent-to-an-application"></a><span data-ttu-id="781ca-103">對應用程式執行同意時出現非預期的錯誤</span><span class="sxs-lookup"><span data-stu-id="781ca-103">Unexpected error when performing consent to an application</span></span>

<span data-ttu-id="781ca-104">這篇文章討論對應用程式進行同意的程序期間會發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="781ca-104">This article discusses errors that can occur during the process of consenting to an application.</span></span> <span data-ttu-id="781ca-105">如果您正在疑難排解未包含任何錯誤訊息的非預期同意提示，請參閱 [Azure AD 的驗證案例](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)。</span><span class="sxs-lookup"><span data-stu-id="781ca-105">If you are Troubleshoot unexpected consent prompts that do not contain any error messages, see [Authentication Scenarios for Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios).</span></span>

<span data-ttu-id="781ca-106">許多與 Azure Active Directory 整合的應用程式需要能存取其他資源的權限，才能夠運作。</span><span class="sxs-lookup"><span data-stu-id="781ca-106">Many applications that integrate with Azure Active Directory require permissions to access other resources in order to function.</span></span> <span data-ttu-id="781ca-107">當這些資源也與 Azure Active Directory 整合時，通常會使用一般的同意架構來要求存取這些資源的權限。</span><span class="sxs-lookup"><span data-stu-id="781ca-107">When these resources are also integrated with Azure Active Directory, permissions to access them is often requested using the common consent framework.</span></span> 

<span data-ttu-id="781ca-108">這會造成顯示同意提示，一般會發生在第一次使用應用程式時，但也會發生在後續使用應用程式時。</span><span class="sxs-lookup"><span data-stu-id="781ca-108">This results in a consent prompt being displayed, which generally occurs the first time an application is used but can also occur on a subsequent use of the application.</span></span>

<span data-ttu-id="781ca-109">某些條件必須成立，使用者才能同意應用程式所需的權限。</span><span class="sxs-lookup"><span data-stu-id="781ca-109">Certain conditions must be true for a user to consent to the permissions an application requires.</span></span> <span data-ttu-id="781ca-110">如果不符合這些條件，便會發生各種錯誤。</span><span class="sxs-lookup"><span data-stu-id="781ca-110">If these conditions are not met, various errors can occur.</span></span> <span data-ttu-id="781ca-111">其中包含：</span><span class="sxs-lookup"><span data-stu-id="781ca-111">These include:</span></span>

## <a name="requesting-not-authorized-permissions-error"></a><span data-ttu-id="781ca-112">要求未經授權權限的錯誤</span><span class="sxs-lookup"><span data-stu-id="781ca-112">Requesting not authorized permissions error</span></span>
* <span data-ttu-id="781ca-113">**AADSTS90093：** &lt;clientAppDisplayName&gt; 正在要求一或多個您未授權授與的權限。</span><span class="sxs-lookup"><span data-stu-id="781ca-113">**AADSTS90093:** &lt;clientAppDisplayName&gt; is requesting one or more permissions that you are not authorized to grant.</span></span> <span data-ttu-id="781ca-114">請連絡系統管理員，其可代表您同意此應用程式。</span><span class="sxs-lookup"><span data-stu-id="781ca-114">Contact an administrator, who can consent to this application on your behalf.</span></span>

<span data-ttu-id="781ca-115">當非公司系統管理員的使用者嘗試使用的應用程式正在要求只有系統管理員能夠授與的權限時，會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="781ca-115">This error occurs when a user who is not a company administrator attempts to use an application that is requesting permissions that only an administrator can grant.</span></span> <span data-ttu-id="781ca-116">可代表其組織授與應用程式存取權的系統管理員能夠解決此錯誤。</span><span class="sxs-lookup"><span data-stu-id="781ca-116">This error can be resolved by an administrator granting access to the application on behalf of their organization.</span></span>

## <a name="policy-prevents-granting-permissions-error"></a><span data-ttu-id="781ca-117">原則禁止授與權限錯誤</span><span class="sxs-lookup"><span data-stu-id="781ca-117">Policy prevents granting permissions error</span></span>
* <span data-ttu-id="781ca-118">**AADSTS90093：**&lt;tenantDisplayName&gt; 的系統管理員設定了原則，讓您無法將 &lt;應用程式名稱&gt; 正在要求的權限授與該應用程式。</span><span class="sxs-lookup"><span data-stu-id="781ca-118">**AADSTS90093:** An administrator of &lt;tenantDisplayName&gt; has set a policy that prevents you from granting &lt;name of app&gt; the permissions it is requesting.</span></span> <span data-ttu-id="781ca-119">請連絡 &lt;tenantDisplayName&gt; 的系統管理員，其可代表您將權限授與此應用程式。</span><span class="sxs-lookup"><span data-stu-id="781ca-119">Contact an administrator of &lt;tenantDisplayName&gt;, who can grant permissions to this app on your behalf.</span></span>

<span data-ttu-id="781ca-120">當公司系統管理員關閉使用者同意應用程式的功能，接著非系統管理員使用者嘗試使用需要同意的應用程式時，會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="781ca-120">This error occurs when a company administrator turns off the ability for users to consent to applications, then a non-administrator user attempts to use an application that requires consent.</span></span> <span data-ttu-id="781ca-121">可代表其組織授與應用程式存取權的系統管理員能夠解決此錯誤。</span><span class="sxs-lookup"><span data-stu-id="781ca-121">This error can be resolved by an administrator granting access to the application on behalf of their organization.</span></span>

## <a name="intermittent-problem-error"></a><span data-ttu-id="781ca-122">間歇性問題錯誤</span><span class="sxs-lookup"><span data-stu-id="781ca-122">Intermittent problem error</span></span>
* <span data-ttu-id="781ca-123">**AADSTS90090：**要記錄您嘗試授與 &lt;clientAppDisplayName&gt; 的權限時似乎發生問題，此問題間歇性發生。</span><span class="sxs-lookup"><span data-stu-id="781ca-123">**AADSTS90090:** It looks like we encountered an intermittent problem recording the permissions you attempted to grant to &lt;clientAppDisplayName&gt;.</span></span> <span data-ttu-id="781ca-124">請稍後再試一次。</span><span class="sxs-lookup"><span data-stu-id="781ca-124">try again later.</span></span>

<span data-ttu-id="781ca-125">此錯誤表示已發生間歇性服務端問題。</span><span class="sxs-lookup"><span data-stu-id="781ca-125">This error indicates that an intermittent service side issue has occurred.</span></span> <span data-ttu-id="781ca-126">再次嘗試同意應用程式，可解決此問題。</span><span class="sxs-lookup"><span data-stu-id="781ca-126">It can be resolved by attempting to consent to the application again.</span></span>

## <a name="resource-not-available-error"></a><span data-ttu-id="781ca-127">資源無法使用錯誤</span><span class="sxs-lookup"><span data-stu-id="781ca-127">Resource not available error</span></span>
* <span data-ttu-id="781ca-128">**AADSTS65005：**應用程式 &lt;clientAppDisplayName&gt; 要求可存取資源 &lt;resourceAppDisplayName&gt; 的權限，但該資源無法使用。</span><span class="sxs-lookup"><span data-stu-id="781ca-128">**AADSTS65005:** The app &lt;clientAppDisplayName&gt; requested permissions to access a resource &lt;resourceAppDisplayName&gt; that is not available.</span></span> 

<span data-ttu-id="781ca-129">請連絡應用程式開發人員。</span><span class="sxs-lookup"><span data-stu-id="781ca-129">Contact the application developer.</span></span>

##  <a name="resource-not-available-in-tenant-error"></a><span data-ttu-id="781ca-130">資源在租用戶無法使用錯誤</span><span class="sxs-lookup"><span data-stu-id="781ca-130">Resource not available in tenant error</span></span>
* <span data-ttu-id="781ca-131">**AADSTS65005：** &lt;clientAppDisplayName&gt; 正在要求存取資源 &lt;resourceAppDisplayName&gt;，但此資源在您的 &lt;tenantDisplayName&gt; 組織中無法使用。</span><span class="sxs-lookup"><span data-stu-id="781ca-131">**AADSTS65005:** &lt;clientAppDisplayName&gt; is requesting access to a resource &lt;resourceAppDisplayName&gt; that is not available in your organization &lt;tenantDisplayName&gt;.</span></span> 

<span data-ttu-id="781ca-132">請確認此資源可以使用，或與 &lt;tenantDisplayName&gt; 的系統管理員連絡。</span><span class="sxs-lookup"><span data-stu-id="781ca-132">Ensure that this resource is available or contact an administrator of &lt;tenantDisplayName&gt;.</span></span>

## <a name="permissions-mismatch-error"></a><span data-ttu-id="781ca-133">權限不符合錯誤</span><span class="sxs-lookup"><span data-stu-id="781ca-133">Permissions mismatch error</span></span>
* <span data-ttu-id="781ca-134">**AADSTS65005：**應用程式要求同意存取 &lt;resourceAppDisplayName&gt; 資源。</span><span class="sxs-lookup"><span data-stu-id="781ca-134">**AADSTS65005:** The app requested consent to access resource &lt;resourceAppDisplayName&gt;.</span></span> <span data-ttu-id="781ca-135">此要求失敗，因為它不符合在應用程式註冊期間預先設定應用程式的方式。</span><span class="sxs-lookup"><span data-stu-id="781ca-135">This request failed because it does not match how the app was pre-configured during app registration.</span></span> <span data-ttu-id="781ca-136">請連絡應用程式廠商。**</span><span class="sxs-lookup"><span data-stu-id="781ca-136">Contact the app vendor.**</span></span>

<span data-ttu-id="781ca-137">當使用者嘗試同意的應用程式正在要求存取某個資源應用程式的權限，但在組織的目錄 (租用戶) 中找不到該應用程式時，這些錯誤全部發生。</span><span class="sxs-lookup"><span data-stu-id="781ca-137">These errors all occur when the application a user is trying to consent to is requesting permissions to access a resource application that cannot be found in the organization’s directory (tenant).</span></span> <span data-ttu-id="781ca-138">發生的原因有數種：</span><span class="sxs-lookup"><span data-stu-id="781ca-138">This can occur for several reasons:</span></span>

-   <span data-ttu-id="781ca-139">用戶端應用程式開發人員將其應用程式設定錯誤，導致應用程式要求存取無效的資源。</span><span class="sxs-lookup"><span data-stu-id="781ca-139">The client application developer has configured their application incorrectly, causing it to request access to an invalid resource.</span></span> <span data-ttu-id="781ca-140">在此狀況下，應用程式開發人員必須更新用戶端應用程式的組態，以解決此問題。</span><span class="sxs-lookup"><span data-stu-id="781ca-140">In this case, the application developer must update the configuration of the client application to resolve this issue.</span></span>

-   <span data-ttu-id="781ca-141">代表目標資源應用程式的服務主體不存在於組織中，或是過去曾存在，但現已遭移除。</span><span class="sxs-lookup"><span data-stu-id="781ca-141">A Service Principal representing the target resource application does not exist in the organization, or existed in the past but has been removed.</span></span> <span data-ttu-id="781ca-142">若要解決此問題，在組織中必須佈建資源應用程式的服務主體，讓用戶端應用程式可以向主體要求權限。</span><span class="sxs-lookup"><span data-stu-id="781ca-142">To resolve this issue, a Service Principal for the resource application must be provisioned in the organization so the client application can request permissions to it.</span></span> <span data-ttu-id="781ca-143">發生這種狀況的方式有數種，視應用程式類型而定，包括︰</span><span class="sxs-lookup"><span data-stu-id="781ca-143">This can happen in an number of ways, depending on the type of application, including:</span></span>

    -   <span data-ttu-id="781ca-144">取得資源應用程式 (Microsoft 發佈的應用程式) 的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="781ca-144">Acquiring a subscription for the resource application (Microsoft published applications)</span></span>

    -   <span data-ttu-id="781ca-145">同意資源應用程式</span><span class="sxs-lookup"><span data-stu-id="781ca-145">Consenting to the resource application</span></span>

    -   <span data-ttu-id="781ca-146">透過 Azure Portal 授與應用程式權限</span><span class="sxs-lookup"><span data-stu-id="781ca-146">Granting the application permissions via the Azure Portal</span></span>

    -   <span data-ttu-id="781ca-147">從 Azure AD 應用程式資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="781ca-147">Adding the application from the Azure AD Application Gallery</span></span>

## <a name="next-steps"></a><span data-ttu-id="781ca-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="781ca-148">Next steps</span></span> 

[<span data-ttu-id="781ca-149">Azure Active Directory 中的應用程式、權限及同意 (v1 端點)</span><span class="sxs-lookup"><span data-stu-id="781ca-149">Apps, permissions, and consent in Azure Active Directory (v1 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)<br>

[<span data-ttu-id="781ca-150">Azure Active Directory v2.0 端點中的範圍、權限及同意</span><span class="sxs-lookup"><span data-stu-id="781ca-150">Scopes, permissions, and consent in the Azure Active Directory (v2.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


