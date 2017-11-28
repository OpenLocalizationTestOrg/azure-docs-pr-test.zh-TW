---
title: "Azure Active Directory 中預先整合應用程式的 hello SAML 權杖中發出的 aaaCustomizing 宣告 |Microsoft 文件"
description: "了解 toocustomize hello 發出宣告的方式在 hello Azure Active Directory 中預先整合應用程式的 SAML 權杖"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: f1daad62-ac8a-44cd-ac76-e97455e47803
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.custom: aaddev
ms.openlocfilehash: a376318929472403e799f02fdd3fbddc91d0a70c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-claims-issued-in-hello-saml-token-for-pre-integrated-apps-in-azure-active-directory"></a><span data-ttu-id="ecc8e-103">Azure Active Directory 中預先整合應用程式的 SAML 權杖在 hello 自訂宣告發出</span><span class="sxs-lookup"><span data-stu-id="ecc8e-103">Customizing claims issued in hello SAML token for pre-integrated apps in Azure Active Directory</span></span>
<span data-ttu-id="ecc8e-104">Azure Active Directory 現在支援數千種預先整合的應用程式中 hello Azure AD 應用程式庫，包括超過支援單一登入的 360 使用 hello SAML 2.0 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-104">Today Azure Active Directory supports thousands of pre-integrated applications in hello Azure AD Application Gallery, including over 360 that support single sign-on using hello SAML 2.0 protocol.</span></span> <span data-ttu-id="ecc8e-105">當使用者透過 Azure AD 使用 SAML tooan 應用程式，Azure AD 會傳送權杖 toohello 應用程式 （透過 HTTP POST)。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-105">When a user authenticates tooan application through Azure AD using SAML, Azure AD sends a token toohello application (via an HTTP POST).</span></span> <span data-ttu-id="ecc8e-106">與然後 hello 應用程式會驗證使用中的 hello 語彙基元 toolog hello 使用者而不是提示輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-106">And then, hello application validates and uses hello token toolog hello user in instead of prompting for a username and password.</span></span> <span data-ttu-id="ecc8e-107">這些 SAML 權杖包含 hello 使用者稱為 「 宣告 」 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-107">These SAML tokens contain pieces of information about hello user known as "claims".</span></span>

<span data-ttu-id="ecc8e-108">在識別說，「 宣告 」 內 hello 語彙基元所發出該使用者的使用者身分識別提供者指出資訊。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-108">In identity-speak, a “claim” is information that an identity provider states about a user inside hello token they issue for that user.</span></span> <span data-ttu-id="ecc8e-109">在[SAML 權杖](http://en.wikipedia.org/wiki/SAML_2.0)，此資料通常會包含在 hello SAML 屬性陳述式。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-109">In [SAML token](http://en.wikipedia.org/wiki/SAML_2.0), this data is typically contained in hello SAML Attribute Statement.</span></span> <span data-ttu-id="ecc8e-110">hello 使用者的唯一識別碼通常都會在 hello SAML 主體也稱為名稱識別項。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-110">hello user’s unique ID is typically represented in hello SAML Subject also called as Name Identifier.</span></span>

<span data-ttu-id="ecc8e-111">根據預設，Azure Active Directory 發出 SAML 權杖 tooyour 應用程式，其中包含 NameIdentifier 宣告，以在 Azure AD 中的 hello 使用者的使用者名稱 （也稱為使用者主體名稱） 的值。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-111">By default, Azure Active Directory issues a SAML token tooyour application that contains a NameIdentifier claim, with a value of hello user’s username (AKA user principal name) in Azure AD.</span></span> <span data-ttu-id="ecc8e-112">這個值可以唯一識別 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-112">this value can uniquely identify hello user.</span></span> <span data-ttu-id="ecc8e-113">hello SAML 語彙基元也會包含額外的宣告包含 hello 使用者的電子郵件地址、 名字和姓氏。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-113">hello SAML token also contains additional claims containing hello user’s email address, first name, and last name.</span></span>

<span data-ttu-id="ecc8e-114">tooview 或編輯 hello 宣告 hello 發出 SAML 權杖 toohello 應用程式，開啟 hello Azure 入口網站中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-114">tooview or edit hello claims issued in hello SAML token toohello application, open hello application in Azure portal.</span></span> <span data-ttu-id="ecc8e-115">然後選取 hello**檢視和編輯所有其他使用者屬性**核取方塊在 hello**使用者屬性**hello 應用程式 > 一節。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-115">Then select hello **View and edit all other user attributes** checkbox in hello **User Attributes** section of hello application.</span></span>

![使用者屬性區段][1]

<span data-ttu-id="ecc8e-117">有兩個可能的原因為何，您可能需要在 hello SAML 權杖中發出的 tooedit hello 宣告：</span><span class="sxs-lookup"><span data-stu-id="ecc8e-117">There are two possible reasons why you might need tooedit hello claims issued in hello SAML token:</span></span>
* <span data-ttu-id="ecc8e-118">hello 應用程式已寫入的 toorequire 用不同的宣告的 Uri 設定，或宣告值。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-118">hello application has been written toorequire a different set of claim URIs or claim values.</span></span>
* <span data-ttu-id="ecc8e-119">hello 應用程式已部署需要 hello NameIdentifier 宣告 toobe 以外的項目 hello 使用者名稱 （也稱為使用者主體名稱） 儲存在 Azure Active Directory 中的方式。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-119">hello application has been deployed in a way that requires hello NameIdentifier claim toobe something other than hello username (AKA user principal name) stored in Azure Active Directory.</span></span>

<span data-ttu-id="ecc8e-120">您可以編輯任何 hello 預設宣告值。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-120">You can edit any of hello default claim values.</span></span> <span data-ttu-id="ecc8e-121">選取 hello SAML token 屬性資料表中的 hello 宣告資料列。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-121">Select hello claim row in hello SAML token attributes table.</span></span> <span data-ttu-id="ecc8e-122">這會開啟 hello**編輯屬性**區段，然後您可以編輯宣告名稱、 值和命名空間與 hello 宣告相關聯。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-122">This opens hello **Edit Attribute** section and then you can edit claim name, value, and namespace associated with hello claim.</span></span>

![編輯使用者屬性][2]

<span data-ttu-id="ecc8e-124">您也可以移除使用 hello 操作功能表，按一下在 hello 所開啟的 （非 NameIdentifier) 宣告**...**圖示。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-124">You can also remove claims (other than NameIdentifier) using hello context menu, which opens by clicking on hello **...** icon.</span></span>  <span data-ttu-id="ecc8e-125">您也可以加入新的宣告，使用 hello**加入屬性** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-125">You can also add new claims using hello **Add attribute** button.</span></span>

![編輯使用者屬性][3]

## <a name="editing-hello-nameidentifier-claim"></a><span data-ttu-id="ecc8e-127">編輯 hello NameIdentifier 宣告</span><span class="sxs-lookup"><span data-stu-id="ecc8e-127">Editing hello NameIdentifier claim</span></span>
<span data-ttu-id="ecc8e-128">toosolve hello 問題已部署 hello 應用程式使用不同的使用者名稱，按一下 hello**使用者識別碼**下拉式清單中 hello**使用者屬性**> 一節。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-128">toosolve hello problem where hello application has been deployed using a different username, click on hello **User Identifier** drop down in hello **User Attributes** section.</span></span> <span data-ttu-id="ecc8e-129">這個動作會提供包含數個不同選項的對話方塊：</span><span class="sxs-lookup"><span data-stu-id="ecc8e-129">This action provides a dialog with several different options:</span></span>

![編輯使用者屬性][4]

<span data-ttu-id="ecc8e-131">在 hello 下拉式清單中，選取  **user.mail** tooset hello NameIdentifier 宣告 toobe hello 使用者的電子郵件地址 hello 目錄中。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-131">In hello drop-down, select **user.mail** tooset hello NameIdentifier claim toobe hello user’s email address in hello directory.</span></span> <span data-ttu-id="ecc8e-132">或者，選取**user.onpremisessamaccountname** tooset toohello 使用者 SAM 帳戶名稱，從同步處理內部部署 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-132">Or, select **user.onpremisessamaccountname** tooset toohello user’s SAM Account Name that has been synced from on-premises Azure AD.</span></span>

<span data-ttu-id="ecc8e-133">您也可以使用特殊的 hello **ExtractMailPrefix()**函式 tooremove hello 從 hello 電子郵件地址、 SAM 帳戶名稱或 hello 使用者主體名稱的網域尾碼。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-133">You can also use hello special **ExtractMailPrefix()** function tooremove hello domain suffix from either hello email address, SAM Account Name, or hello user principal name.</span></span> <span data-ttu-id="ecc8e-134">這會擷取僅 hello 第一部分 hello 使用者名稱傳遞出去 (例如，"joe_smith"而不是joe_smith@contoso.com)。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-134">This extracts only hello first part of hello user name being passed through (for example, "joe_smith" instead of joe_smith@contoso.com).</span></span>

![編輯使用者屬性][5]

<span data-ttu-id="ecc8e-136">我們現在還新增了 hello **join （)**函式 toojoin hello 驗證網域與 hello 使用者識別碼值。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-136">We have now also added hello **join()** function toojoin hello verified domain with hello user identifier value.</span></span> <span data-ttu-id="ecc8e-137">當您選取 hello join （） 函式在 hello**使用者識別碼**第一次選取類似電子郵件地址或使用者主體名稱為 hello 使用者識別碼，然後 hello 第二個下拉式清單中選取 已驗證的網域。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-137">when you select hello join() function in hello **User Identifier** First select hello user identifier as like email address or user principal name and then in hello second drop-down select your verified domain.</span></span> <span data-ttu-id="ecc8e-138">如果您選取 hello 電子郵件地址與 hello 已驗證網域，則 Azure AD 擷取從 hello 第一個值 joe_smith hello username joe_smith@contoso.com ，並將它附加與 contoso.onmicrosoft.com。請參閱下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="ecc8e-138">If you select hello email address with hello verified domain, then Azure AD extracts hello username from hello first value joe_smith from joe_smith@contoso.com and appends it with contoso.onmicrosoft.com. See hello following example:</span></span>

![編輯使用者屬性][6]

## <a name="adding-claims"></a><span data-ttu-id="ecc8e-140">新增宣告</span><span class="sxs-lookup"><span data-stu-id="ecc8e-140">Adding claims</span></span>
<span data-ttu-id="ecc8e-141">當新增宣告，您可以指定 hello 屬性名稱 （不嚴格需要 toofollow 根據 hello SAML 規格的 URI 模式）。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-141">When adding a claim, you can specify hello attribute name (which doesn’t strictly need toofollow a URI pattern as per hello SAML spec).</span></span> <span data-ttu-id="ecc8e-142">設定 hello 值 tooany 使用者屬性儲存在 hello 目錄中。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-142">Set hello value tooany user attribute that is stored in hello directory.</span></span>

![新增使用者屬性][7]

<span data-ttu-id="ecc8e-144">例如，您需要 toosend hello 使用者的 hello 部門所屬 tooin 組織 （例如，Sales) 宣告的形式。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-144">For example, you need toosend hello department that hello user belongs tooin their organization as a claim (such as, Sales).</span></span> <span data-ttu-id="ecc8e-145">如預期般 hello 應用程式中，輸入 hello 宣告名稱，然後選取**user.department** hello 值。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-145">Enter hello claim name as expected by hello application, and then select **user.department** as hello value.</span></span>

> [!NOTE]
> <span data-ttu-id="ecc8e-146">如果沒有針對選取的屬性儲存的值指定使用者，然後該宣告無法發行 hello 權杖中。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-146">If for a given user there is no value stored for a selected attribute, then that claim is not being issued in hello token.</span></span>

> [!TIP]
> <span data-ttu-id="ecc8e-147">hello **user.onpremisesecurityidentifier**和**user.onpremisesamaccountname**時同步處理使用者資料，從內部部署 Active Directory 使用 hello，才支援[AzureAD Connect 工具](../active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-147">hello **user.onpremisesecurityidentifier** and **user.onpremisesamaccountname** are only supported when synchronizing user data from on-premises Active Directory using hello [Azure AD Connect tool](../active-directory-aadconnect.md).</span></span>

## <a name="restricted-claims"></a><span data-ttu-id="ecc8e-148">受限制的宣告</span><span class="sxs-lookup"><span data-stu-id="ecc8e-148">Restricted claims</span></span>

<span data-ttu-id="ecc8e-149">SAML 有一些受限制的宣告。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-149">There are some restricted claims in SAML.</span></span> <span data-ttu-id="ecc8e-150">如果您新增這些宣告，則 Azure AD 不會傳送這些宣告。</span><span class="sxs-lookup"><span data-stu-id="ecc8e-150">If you add these claims, then Azure AD will not send these claims.</span></span> <span data-ttu-id="ecc8e-151">以下是 hello SAML 限制宣告集：</span><span class="sxs-lookup"><span data-stu-id="ecc8e-151">Following are hello SAML restricted claim set:</span></span>

    | <span data-ttu-id="ecc8e-152">宣告類型 (URI)</span><span class="sxs-lookup"><span data-stu-id="ecc8e-152">Claim type (URI)</span></span> |
    | ------------------- |
    | <span data-ttu-id="ecc8e-153">http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration</span><span class="sxs-lookup"><span data-stu-id="ecc8e-153">http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration</span></span> |
    | <span data-ttu-id="ecc8e-154">http://schemas.microsoft.com/ws/2008/06/identity/claims/expired</span><span class="sxs-lookup"><span data-stu-id="ecc8e-154">http://schemas.microsoft.com/ws/2008/06/identity/claims/expired</span></span> |
    | <span data-ttu-id="ecc8e-155">http://schemas.microsoft.com/identity/claims/accesstoken</span><span class="sxs-lookup"><span data-stu-id="ecc8e-155">http://schemas.microsoft.com/identity/claims/accesstoken</span></span> |
    | <span data-ttu-id="ecc8e-156">http://schemas.microsoft.com/identity/claims/openid2_id</span><span class="sxs-lookup"><span data-stu-id="ecc8e-156">http://schemas.microsoft.com/identity/claims/openid2_id</span></span> |
    | <span data-ttu-id="ecc8e-157">http://schemas.microsoft.com/identity/claims/identityprovider</span><span class="sxs-lookup"><span data-stu-id="ecc8e-157">http://schemas.microsoft.com/identity/claims/identityprovider</span></span> |
    | <span data-ttu-id="ecc8e-158">http://schemas.microsoft.com/identity/claims/objectidentifier</span><span class="sxs-lookup"><span data-stu-id="ecc8e-158">http://schemas.microsoft.com/identity/claims/objectidentifier</span></span> |
    | <span data-ttu-id="ecc8e-159">http://schemas.microsoft.com/identity/claims/puid</span><span class="sxs-lookup"><span data-stu-id="ecc8e-159">http://schemas.microsoft.com/identity/claims/puid</span></span> |
    | <span data-ttu-id="ecc8e-160">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier[MR1]</span><span class="sxs-lookup"><span data-stu-id="ecc8e-160">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier[MR1]</span></span> |
    | <span data-ttu-id="ecc8e-161">http://schemas.microsoft.com/identity/claims/tenantid</span><span class="sxs-lookup"><span data-stu-id="ecc8e-161">http://schemas.microsoft.com/identity/claims/tenantid</span></span> |
    | <span data-ttu-id="ecc8e-162">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant</span><span class="sxs-lookup"><span data-stu-id="ecc8e-162">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant</span></span> |
    | <span data-ttu-id="ecc8e-163">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod</span><span class="sxs-lookup"><span data-stu-id="ecc8e-163">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod</span></span> |
    | <span data-ttu-id="ecc8e-164">http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider</span><span class="sxs-lookup"><span data-stu-id="ecc8e-164">http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider</span></span> |
    | <span data-ttu-id="ecc8e-165">http://schemas.microsoft.com/ws/2008/06/identity/claims/groups</span><span class="sxs-lookup"><span data-stu-id="ecc8e-165">http://schemas.microsoft.com/ws/2008/06/identity/claims/groups</span></span> |
    | <span data-ttu-id="ecc8e-166">http://schemas.microsoft.com/claims/groups.link</span><span class="sxs-lookup"><span data-stu-id="ecc8e-166">http://schemas.microsoft.com/claims/groups.link</span></span> |
    | <span data-ttu-id="ecc8e-167">http://schemas.microsoft.com/ws/2008/06/identity/claims/role</span><span class="sxs-lookup"><span data-stu-id="ecc8e-167">http://schemas.microsoft.com/ws/2008/06/identity/claims/role</span></span> |
    | <span data-ttu-id="ecc8e-168">http://schemas.microsoft.com/ws/2008/06/identity/claims/wids</span><span class="sxs-lookup"><span data-stu-id="ecc8e-168">http://schemas.microsoft.com/ws/2008/06/identity/claims/wids</span></span> |
    | <span data-ttu-id="ecc8e-169">http://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant</span><span class="sxs-lookup"><span data-stu-id="ecc8e-169">http://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant</span></span> |
    | <span data-ttu-id="ecc8e-170">http://schemas.microsoft.com/2014/02/devicecontext/claims/isknown</span><span class="sxs-lookup"><span data-stu-id="ecc8e-170">http://schemas.microsoft.com/2014/02/devicecontext/claims/isknown</span></span> |
    | <span data-ttu-id="ecc8e-171">http://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged</span><span class="sxs-lookup"><span data-stu-id="ecc8e-171">http://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged</span></span> |
    | <span data-ttu-id="ecc8e-172">http://schemas.microsoft.com/2014/03/psso</span><span class="sxs-lookup"><span data-stu-id="ecc8e-172">http://schemas.microsoft.com/2014/03/psso</span></span> |
    | <span data-ttu-id="ecc8e-173">http://schemas.microsoft.com/claims/authnmethodsreferences</span><span class="sxs-lookup"><span data-stu-id="ecc8e-173">http://schemas.microsoft.com/claims/authnmethodsreferences</span></span> |
    | <span data-ttu-id="ecc8e-174">http://schemas.xmlsoap.org/ws/2009/09/identity/claims/actor</span><span class="sxs-lookup"><span data-stu-id="ecc8e-174">http://schemas.xmlsoap.org/ws/2009/09/identity/claims/actor</span></span> |
    | <span data-ttu-id="ecc8e-175">http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername</span><span class="sxs-lookup"><span data-stu-id="ecc8e-175">http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername</span></span> |
    | <span data-ttu-id="ecc8e-176">http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey</span><span class="sxs-lookup"><span data-stu-id="ecc8e-176">http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey</span></span> |
    | <span data-ttu-id="ecc8e-177">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname</span><span class="sxs-lookup"><span data-stu-id="ecc8e-177">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname</span></span> |
    | <span data-ttu-id="ecc8e-178">http://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid</span><span class="sxs-lookup"><span data-stu-id="ecc8e-178">http://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid</span></span> |
    | <span data-ttu-id="ecc8e-179">http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid</span><span class="sxs-lookup"><span data-stu-id="ecc8e-179">http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid</span></span> |
    | <span data-ttu-id="ecc8e-180">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authorizationdecision</span><span class="sxs-lookup"><span data-stu-id="ecc8e-180">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authorizationdecision</span></span> |
    | <span data-ttu-id="ecc8e-181">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authentication</span><span class="sxs-lookup"><span data-stu-id="ecc8e-181">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authentication</span></span> |
    | <span data-ttu-id="ecc8e-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/sid</span><span class="sxs-lookup"><span data-stu-id="ecc8e-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/sid</span></span> |
    | <span data-ttu-id="ecc8e-183">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarygroupsid</span><span class="sxs-lookup"><span data-stu-id="ecc8e-183">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarygroupsid</span></span> |
    | <span data-ttu-id="ecc8e-184">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarysid</span><span class="sxs-lookup"><span data-stu-id="ecc8e-184">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarysid</span></span> |
    | <span data-ttu-id="ecc8e-185">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid</span><span class="sxs-lookup"><span data-stu-id="ecc8e-185">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid</span></span> |
    | <span data-ttu-id="ecc8e-186">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlywindowsdevicegroup</span><span class="sxs-lookup"><span data-stu-id="ecc8e-186">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlywindowsdevicegroup</span></span> |
    | <span data-ttu-id="ecc8e-187">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdeviceclaim</span><span class="sxs-lookup"><span data-stu-id="ecc8e-187">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdeviceclaim</span></span> |
    | <span data-ttu-id="ecc8e-188">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup</span><span class="sxs-lookup"><span data-stu-id="ecc8e-188">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup</span></span> |
    | <span data-ttu-id="ecc8e-189">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsfqbnversion</span><span class="sxs-lookup"><span data-stu-id="ecc8e-189">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsfqbnversion</span></span> |
    | <span data-ttu-id="ecc8e-190">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowssubauthority</span><span class="sxs-lookup"><span data-stu-id="ecc8e-190">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowssubauthority</span></span> |
    | <span data-ttu-id="ecc8e-191">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsuserclaim</span><span class="sxs-lookup"><span data-stu-id="ecc8e-191">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsuserclaim</span></span> |
    | <span data-ttu-id="ecc8e-192">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/x500distinguishedname</span><span class="sxs-lookup"><span data-stu-id="ecc8e-192">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/x500distinguishedname</span></span> |
    | <span data-ttu-id="ecc8e-193">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn</span><span class="sxs-lookup"><span data-stu-id="ecc8e-193">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn</span></span> |
    | <span data-ttu-id="ecc8e-194">http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid</span><span class="sxs-lookup"><span data-stu-id="ecc8e-194">http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid</span></span> |
    | <span data-ttu-id="ecc8e-195">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn</span><span class="sxs-lookup"><span data-stu-id="ecc8e-195">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn</span></span> |
    | <span data-ttu-id="ecc8e-196">http://schemas.microsoft.com/ws/2008/06/identity/claims/ispersistent</span><span class="sxs-lookup"><span data-stu-id="ecc8e-196">http://schemas.microsoft.com/ws/2008/06/identity/claims/ispersistent</span></span> |
    | <span data-ttu-id="ecc8e-197">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier</span><span class="sxs-lookup"><span data-stu-id="ecc8e-197">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier</span></span> |
    | <span data-ttu-id="ecc8e-198">http://schemas.microsoft.com/identity/claims/scope</span><span class="sxs-lookup"><span data-stu-id="ecc8e-198">http://schemas.microsoft.com/identity/claims/scope</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ecc8e-199">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ecc8e-199">Next steps</span></span>
* [<span data-ttu-id="ecc8e-200">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="ecc8e-200">Article Index for Application Management in Azure Active Directory</span></span>](../active-directory-apps-index.md)
* [<span data-ttu-id="ecc8e-201">設定單一登入 tooapplications 不在 hello Azure Active Directory 應用程式庫</span><span class="sxs-lookup"><span data-stu-id="ecc8e-201">Configuring single sign-on tooapplications that are not in hello Azure Active Directory application gallery</span></span>](../active-directory-saas-custom-apps.md)
* [<span data-ttu-id="ecc8e-202">SAML 型單一登入疑難排解</span><span class="sxs-lookup"><span data-stu-id="ecc8e-202">Troubleshooting SAML-Based Single Sign-On</span></span>](active-directory-saml-debugging.md)

<!--Image references-->
[1]: ./media/active-directory-saml-claims-customization/user-attribute-section.png
[2]: ./media/active-directory-saml-claims-customization/edit-claim-name-value.png
[3]: ./media/active-directory-saml-claims-customization/delete-claim.png
[4]: ./media/active-directory-saml-claims-customization/user-identifier.png
[5]: ./media/active-directory-saml-claims-customization/extractemailprefix-function.png
[6]: ./media/active-directory-saml-claims-customization/join-function.png
[7]: ./media/active-directory-saml-claims-customization/add-attribute.png