---
title: "在 Azure Active Directory 中為預先整合的應用程式自訂在 SAML 權杖中發出的宣告 | Microsoft Docs"
description: "了解如何在 Azure Active Directory 中為預先整合的應用程式自訂在 SAML 權杖中發出的宣告"
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
ms.openlocfilehash: 6d232759630fcc567788a8326b566b659f89d17a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="customizing-claims-issued-in-the-saml-token-for-pre-integrated-apps-in-azure-active-directory"></a><span data-ttu-id="b14f7-103">在 Azure Active Directory 中為預先整合的應用程式自訂在 SAML 權杖中發出的宣告</span><span class="sxs-lookup"><span data-stu-id="b14f7-103">Customizing claims issued in the SAML token for pre-integrated apps in Azure Active Directory</span></span>
<span data-ttu-id="b14f7-104">目前 Azure Active Directory 支援 Azure AD 應用程式庫中數千個預先整合的應用程式，有 360 個以上的應用程式支援使用 SAML 2.0 通訊協定的單一登入。</span><span class="sxs-lookup"><span data-stu-id="b14f7-104">Today Azure Active Directory supports thousands of pre-integrated applications in the Azure AD Application Gallery, including over 360 that support single sign-on using the SAML 2.0 protocol.</span></span> <span data-ttu-id="b14f7-105">當使用者使用 SAML 透過 Azure AD 驗證應用程式時，Azure AD 會將權杖傳送給應用程式 (透過 HTTP POST)。</span><span class="sxs-lookup"><span data-stu-id="b14f7-105">When a user authenticates to an application through Azure AD using SAML, Azure AD sends a token to the application (via an HTTP POST).</span></span> <span data-ttu-id="b14f7-106">然後，應用程式會驗證並使用權杖將使用者登入，而不會提示輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="b14f7-106">And then, the application validates and uses the token to log the user in instead of prompting for a username and password.</span></span> <span data-ttu-id="b14f7-107">這些 SAML 權杖包含關於使用者的資訊片段 (稱為「宣告」)。</span><span class="sxs-lookup"><span data-stu-id="b14f7-107">These SAML tokens contain pieces of information about the user known as "claims".</span></span>

<span data-ttu-id="b14f7-108">在身分識別交談中，「宣告」是身分識別提供者在為使用者發出的權杖中關於使用者說明的資訊。</span><span class="sxs-lookup"><span data-stu-id="b14f7-108">In identity-speak, a “claim” is information that an identity provider states about a user inside the token they issue for that user.</span></span> <span data-ttu-id="b14f7-109">在 [SAML 權杖](http://en.wikipedia.org/wiki/SAML_2.0)中，此資料通常包含在 SAML 屬性陳述式中。</span><span class="sxs-lookup"><span data-stu-id="b14f7-109">In [SAML token](http://en.wikipedia.org/wiki/SAML_2.0), this data is typically contained in the SAML Attribute Statement.</span></span> <span data-ttu-id="b14f7-110">使用者的唯一識別碼通常在 SAML Subject 中表示，也稱為「名稱識別碼」。</span><span class="sxs-lookup"><span data-stu-id="b14f7-110">The user’s unique ID is typically represented in the SAML Subject also called as Name Identifier.</span></span>

<span data-ttu-id="b14f7-111">根據預設，Azure Active Directory 會發出 SAML 權杖給您的應用程式，其包含一個 NameIdentifier 宣告，具有使用者在 Azure AD 中的使用者名稱 (也稱為使用者主體名稱) 的值。</span><span class="sxs-lookup"><span data-stu-id="b14f7-111">By default, Azure Active Directory issues a SAML token to your application that contains a NameIdentifier claim, with a value of the user’s username (AKA user principal name) in Azure AD.</span></span> <span data-ttu-id="b14f7-112">此值可唯一識別使用者。</span><span class="sxs-lookup"><span data-stu-id="b14f7-112">this value can uniquely identify the user.</span></span> <span data-ttu-id="b14f7-113">SAML 權杖也包含額外的宣告，其包含使用者的電子郵件地址、名字和姓氏。</span><span class="sxs-lookup"><span data-stu-id="b14f7-113">The SAML token also contains additional claims containing the user’s email address, first name, and last name.</span></span>

<span data-ttu-id="b14f7-114">若要檢視或編輯在 SAML 權杖中對應用程式發出的宣告，請在 Azure 入口網站中開啟應用程式。</span><span class="sxs-lookup"><span data-stu-id="b14f7-114">To view or edit the claims issued in the SAML token to the application, open the application in Azure portal.</span></span> <span data-ttu-id="b14f7-115">然後在應用程式的 [使用者屬性] 區段中，選取 [檢視和編輯所有其他使用者屬性] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="b14f7-115">Then select the **View and edit all other user attributes** checkbox in the **User Attributes** section of the application.</span></span>

![使用者屬性區段][1]

<span data-ttu-id="b14f7-117">編輯在 SAML 權杖中簽發的宣告有兩個可能原因：</span><span class="sxs-lookup"><span data-stu-id="b14f7-117">There are two possible reasons why you might need to edit the claims issued in the SAML token:</span></span>
* <span data-ttu-id="b14f7-118">應用程式是設計為要求不同的宣告 URI 組或宣告值。</span><span class="sxs-lookup"><span data-stu-id="b14f7-118">The application has been written to require a different set of claim URIs or claim values.</span></span>
* <span data-ttu-id="b14f7-119">應用程式已部署為要求 NameIdentifier 宣告必須是 Azure Active Directory 中儲存之 username (也稱為使用者主體名稱) 以外的項目。</span><span class="sxs-lookup"><span data-stu-id="b14f7-119">The application has been deployed in a way that requires the NameIdentifier claim to be something other than the username (AKA user principal name) stored in Azure Active Directory.</span></span>

<span data-ttu-id="b14f7-120">您可以編輯任何預設的宣告值。</span><span class="sxs-lookup"><span data-stu-id="b14f7-120">You can edit any of the default claim values.</span></span> <span data-ttu-id="b14f7-121">選取 SAML 權杖屬性資料表中的宣告資料列。</span><span class="sxs-lookup"><span data-stu-id="b14f7-121">Select the claim row in the SAML token attributes table.</span></span> <span data-ttu-id="b14f7-122">這會開啟 [編輯屬性] 區段，然後您可以編輯宣告名稱、值，以及與宣告相關聯的命名空間。</span><span class="sxs-lookup"><span data-stu-id="b14f7-122">This opens the **Edit Attribute** section and then you can edit claim name, value, and namespace associated with the claim.</span></span>

![編輯使用者屬性][2]

<span data-ttu-id="b14f7-124">您也可以使用快顯功能表來移除宣告 (除了 NameIdentifier 以外)，按一下 [...] 圖示即可開啟該功能表。</span><span class="sxs-lookup"><span data-stu-id="b14f7-124">You can also remove claims (other than NameIdentifier) using the context menu, which opens by clicking on the **...** icon.</span></span>  <span data-ttu-id="b14f7-125">使用 [新增屬性] 按鈕，也可以新增宣告。</span><span class="sxs-lookup"><span data-stu-id="b14f7-125">You can also add new claims using the **Add attribute** button.</span></span>

![編輯使用者屬性][3]

## <a name="editing-the-nameidentifier-claim"></a><span data-ttu-id="b14f7-127">編輯 NameIdentifier 宣告</span><span class="sxs-lookup"><span data-stu-id="b14f7-127">Editing the NameIdentifier claim</span></span>
<span data-ttu-id="b14f7-128">若要解決使用不同的使用者名稱部署應用程式的問題，請按一下 [使用者屬性] 區段中的 [使用者識別碼] 下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="b14f7-128">To solve the problem where the application has been deployed using a different username, click on the **User Identifier** drop down in the **User Attributes** section.</span></span> <span data-ttu-id="b14f7-129">這個動作會提供包含數個不同選項的對話方塊：</span><span class="sxs-lookup"><span data-stu-id="b14f7-129">This action provides a dialog with several different options:</span></span>

![編輯使用者屬性][4]

<span data-ttu-id="b14f7-131">在下拉式清單中，選取 [user.mail]，將 NameIdentifier 宣告設定為使用者在目錄中的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="b14f7-131">In the drop-down, select **user.mail** to set the NameIdentifier claim to be the user’s email address in the directory.</span></span> <span data-ttu-id="b14f7-132">或者，選取 **user.onpremisessamaccountname** 設定為從內部部署 Azure AD 同步處理的使用者 SAM 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="b14f7-132">Or, select **user.onpremisessamaccountname** to set to the user’s SAM Account Name that has been synced from on-premises Azure AD.</span></span>

<span data-ttu-id="b14f7-133">您也可以使用特殊的 **ExtractMailPrefix()** 函式，從電子郵件地址、SAM 帳戶名稱或使用者主體名稱中將網域尾碼移除。</span><span class="sxs-lookup"><span data-stu-id="b14f7-133">You can also use the special **ExtractMailPrefix()** function to remove the domain suffix from either the email address, SAM Account Name, or the user principal name.</span></span> <span data-ttu-id="b14f7-134">這只會擷取使用者名稱的第一個部分 (例如，"joe_smith" 而不是 joe_smith@contoso.com)。</span><span class="sxs-lookup"><span data-stu-id="b14f7-134">This extracts only the first part of the user name being passed through (for example, "joe_smith" instead of joe_smith@contoso.com).</span></span>

![編輯使用者屬性][5]

<span data-ttu-id="b14f7-136">我們現在還新增了 **join()** 函式，以聯結已驗證的網域與使用者識別碼值。</span><span class="sxs-lookup"><span data-stu-id="b14f7-136">We have now also added the **join()** function to join the verified domain with the user identifier value.</span></span> <span data-ttu-id="b14f7-137">當您選取 [使用者識別碼] 中的 join() 函式時，先選取像是電子郵件地址或使用者主體名稱的使用者識別碼，然後在第二個下拉式清單中選取已驗證的網域。</span><span class="sxs-lookup"><span data-stu-id="b14f7-137">when you select the join() function in the **User Identifier** First select the user identifier as like email address or user principal name and then in the second drop-down select your verified domain.</span></span> <span data-ttu-id="b14f7-138">如果您選取包含已驗證網域的電子郵件地址，則 Azure AD 會從 joe_smith@contoso.com 的第一個值 joe_smith 中擷取使用者名稱，並將它與 contoso.onmicrosoft.com 附加。</span><span class="sxs-lookup"><span data-stu-id="b14f7-138">If you select the email address with the verified domain, then Azure AD extracts the username from the first value joe_smith from joe_smith@contoso.com and appends it with contoso.onmicrosoft.com.</span></span> <span data-ttu-id="b14f7-139">請參閱下列範例：</span><span class="sxs-lookup"><span data-stu-id="b14f7-139">See the following example:</span></span>

![編輯使用者屬性][6]

## <a name="adding-claims"></a><span data-ttu-id="b14f7-141">新增宣告</span><span class="sxs-lookup"><span data-stu-id="b14f7-141">Adding claims</span></span>
<span data-ttu-id="b14f7-142">新增宣告時，您可以指定屬性名稱 (不必根據 SAML 規格嚴格遵循 URI 模式)。</span><span class="sxs-lookup"><span data-stu-id="b14f7-142">When adding a claim, you can specify the attribute name (which doesn’t strictly need to follow a URI pattern as per the SAML spec).</span></span> <span data-ttu-id="b14f7-143">將值設定為儲存在目錄中的任何使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="b14f7-143">Set the value to any user attribute that is stored in the directory.</span></span>

![新增使用者屬性][7]

<span data-ttu-id="b14f7-145">例如，您必須傳送使用者在其組織內所屬的部門作為宣告 (例如，銷售)。</span><span class="sxs-lookup"><span data-stu-id="b14f7-145">For example, you need to send the department that the user belongs to in their organization as a claim (such as, Sales).</span></span> <span data-ttu-id="b14f7-146">輸入應用程式預期的宣告名稱，然後選取 **user.department** 作為值。</span><span class="sxs-lookup"><span data-stu-id="b14f7-146">Enter the claim name as expected by the application, and then select **user.department** as the value.</span></span>

> [!NOTE]
> <span data-ttu-id="b14f7-147">如果指定的使用者沒有針對選取的屬性儲存的值，則權杖中不會發出該宣告。</span><span class="sxs-lookup"><span data-stu-id="b14f7-147">If for a given user there is no value stored for a selected attribute, then that claim is not being issued in the token.</span></span>

> [!TIP]
> <span data-ttu-id="b14f7-148">只有在使用 [Azure AD Connect 工具](../active-directory-aadconnect.md)從內部部署的 Active Directory 同步處理使用者資料時，才支援 **user.onpremisesecurityidentifier** 和 **user.onpremisesamaccountname**。</span><span class="sxs-lookup"><span data-stu-id="b14f7-148">The **user.onpremisesecurityidentifier** and **user.onpremisesamaccountname** are only supported when synchronizing user data from on-premises Active Directory using the [Azure AD Connect tool](../active-directory-aadconnect.md).</span></span>

## <a name="restricted-claims"></a><span data-ttu-id="b14f7-149">受限制的宣告</span><span class="sxs-lookup"><span data-stu-id="b14f7-149">Restricted claims</span></span>

<span data-ttu-id="b14f7-150">SAML 有一些受限制的宣告。</span><span class="sxs-lookup"><span data-stu-id="b14f7-150">There are some restricted claims in SAML.</span></span> <span data-ttu-id="b14f7-151">如果您新增這些宣告，則 Azure AD 不會傳送這些宣告。</span><span class="sxs-lookup"><span data-stu-id="b14f7-151">If you add these claims, then Azure AD will not send these claims.</span></span> <span data-ttu-id="b14f7-152">以下是受限制的 SAML 宣告集：</span><span class="sxs-lookup"><span data-stu-id="b14f7-152">Following are the SAML restricted claim set:</span></span>

    | <span data-ttu-id="b14f7-153">宣告類型 (URI)</span><span class="sxs-lookup"><span data-stu-id="b14f7-153">Claim type (URI)</span></span> |
    | ------------------- |
    | <span data-ttu-id="b14f7-154">http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration</span><span class="sxs-lookup"><span data-stu-id="b14f7-154">http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration</span></span> |
    | <span data-ttu-id="b14f7-155">http://schemas.microsoft.com/ws/2008/06/identity/claims/expired</span><span class="sxs-lookup"><span data-stu-id="b14f7-155">http://schemas.microsoft.com/ws/2008/06/identity/claims/expired</span></span> |
    | <span data-ttu-id="b14f7-156">http://schemas.microsoft.com/identity/claims/accesstoken</span><span class="sxs-lookup"><span data-stu-id="b14f7-156">http://schemas.microsoft.com/identity/claims/accesstoken</span></span> |
    | <span data-ttu-id="b14f7-157">http://schemas.microsoft.com/identity/claims/openid2_id</span><span class="sxs-lookup"><span data-stu-id="b14f7-157">http://schemas.microsoft.com/identity/claims/openid2_id</span></span> |
    | <span data-ttu-id="b14f7-158">http://schemas.microsoft.com/identity/claims/identityprovider</span><span class="sxs-lookup"><span data-stu-id="b14f7-158">http://schemas.microsoft.com/identity/claims/identityprovider</span></span> |
    | <span data-ttu-id="b14f7-159">http://schemas.microsoft.com/identity/claims/objectidentifier</span><span class="sxs-lookup"><span data-stu-id="b14f7-159">http://schemas.microsoft.com/identity/claims/objectidentifier</span></span> |
    | <span data-ttu-id="b14f7-160">http://schemas.microsoft.com/identity/claims/puid</span><span class="sxs-lookup"><span data-stu-id="b14f7-160">http://schemas.microsoft.com/identity/claims/puid</span></span> |
    | <span data-ttu-id="b14f7-161">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier[MR1]</span><span class="sxs-lookup"><span data-stu-id="b14f7-161">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier[MR1]</span></span> |
    | <span data-ttu-id="b14f7-162">http://schemas.microsoft.com/identity/claims/tenantid</span><span class="sxs-lookup"><span data-stu-id="b14f7-162">http://schemas.microsoft.com/identity/claims/tenantid</span></span> |
    | <span data-ttu-id="b14f7-163">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant</span><span class="sxs-lookup"><span data-stu-id="b14f7-163">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant</span></span> |
    | <span data-ttu-id="b14f7-164">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod</span><span class="sxs-lookup"><span data-stu-id="b14f7-164">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod</span></span> |
    | <span data-ttu-id="b14f7-165">http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider</span><span class="sxs-lookup"><span data-stu-id="b14f7-165">http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider</span></span> |
    | <span data-ttu-id="b14f7-166">http://schemas.microsoft.com/ws/2008/06/identity/claims/groups</span><span class="sxs-lookup"><span data-stu-id="b14f7-166">http://schemas.microsoft.com/ws/2008/06/identity/claims/groups</span></span> |
    | <span data-ttu-id="b14f7-167">http://schemas.microsoft.com/claims/groups.link</span><span class="sxs-lookup"><span data-stu-id="b14f7-167">http://schemas.microsoft.com/claims/groups.link</span></span> |
    | <span data-ttu-id="b14f7-168">http://schemas.microsoft.com/ws/2008/06/identity/claims/role</span><span class="sxs-lookup"><span data-stu-id="b14f7-168">http://schemas.microsoft.com/ws/2008/06/identity/claims/role</span></span> |
    | <span data-ttu-id="b14f7-169">http://schemas.microsoft.com/ws/2008/06/identity/claims/wids</span><span class="sxs-lookup"><span data-stu-id="b14f7-169">http://schemas.microsoft.com/ws/2008/06/identity/claims/wids</span></span> |
    | <span data-ttu-id="b14f7-170">http://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant</span><span class="sxs-lookup"><span data-stu-id="b14f7-170">http://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant</span></span> |
    | <span data-ttu-id="b14f7-171">http://schemas.microsoft.com/2014/02/devicecontext/claims/isknown</span><span class="sxs-lookup"><span data-stu-id="b14f7-171">http://schemas.microsoft.com/2014/02/devicecontext/claims/isknown</span></span> |
    | <span data-ttu-id="b14f7-172">http://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged</span><span class="sxs-lookup"><span data-stu-id="b14f7-172">http://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged</span></span> |
    | <span data-ttu-id="b14f7-173">http://schemas.microsoft.com/2014/03/psso</span><span class="sxs-lookup"><span data-stu-id="b14f7-173">http://schemas.microsoft.com/2014/03/psso</span></span> |
    | <span data-ttu-id="b14f7-174">http://schemas.microsoft.com/claims/authnmethodsreferences</span><span class="sxs-lookup"><span data-stu-id="b14f7-174">http://schemas.microsoft.com/claims/authnmethodsreferences</span></span> |
    | <span data-ttu-id="b14f7-175">http://schemas.xmlsoap.org/ws/2009/09/identity/claims/actor</span><span class="sxs-lookup"><span data-stu-id="b14f7-175">http://schemas.xmlsoap.org/ws/2009/09/identity/claims/actor</span></span> |
    | <span data-ttu-id="b14f7-176">http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername</span><span class="sxs-lookup"><span data-stu-id="b14f7-176">http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername</span></span> |
    | <span data-ttu-id="b14f7-177">http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey</span><span class="sxs-lookup"><span data-stu-id="b14f7-177">http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey</span></span> |
    | <span data-ttu-id="b14f7-178">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname</span><span class="sxs-lookup"><span data-stu-id="b14f7-178">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname</span></span> |
    | <span data-ttu-id="b14f7-179">http://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid</span><span class="sxs-lookup"><span data-stu-id="b14f7-179">http://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid</span></span> |
    | <span data-ttu-id="b14f7-180">http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid</span><span class="sxs-lookup"><span data-stu-id="b14f7-180">http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid</span></span> |
    | <span data-ttu-id="b14f7-181">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authorizationdecision</span><span class="sxs-lookup"><span data-stu-id="b14f7-181">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authorizationdecision</span></span> |
    | <span data-ttu-id="b14f7-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authentication</span><span class="sxs-lookup"><span data-stu-id="b14f7-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authentication</span></span> |
    | <span data-ttu-id="b14f7-183">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/sid</span><span class="sxs-lookup"><span data-stu-id="b14f7-183">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/sid</span></span> |
    | <span data-ttu-id="b14f7-184">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarygroupsid</span><span class="sxs-lookup"><span data-stu-id="b14f7-184">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarygroupsid</span></span> |
    | <span data-ttu-id="b14f7-185">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarysid</span><span class="sxs-lookup"><span data-stu-id="b14f7-185">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarysid</span></span> |
    | <span data-ttu-id="b14f7-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid</span><span class="sxs-lookup"><span data-stu-id="b14f7-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid</span></span> |
    | <span data-ttu-id="b14f7-187">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlywindowsdevicegroup</span><span class="sxs-lookup"><span data-stu-id="b14f7-187">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlywindowsdevicegroup</span></span> |
    | <span data-ttu-id="b14f7-188">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdeviceclaim</span><span class="sxs-lookup"><span data-stu-id="b14f7-188">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdeviceclaim</span></span> |
    | <span data-ttu-id="b14f7-189">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup</span><span class="sxs-lookup"><span data-stu-id="b14f7-189">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup</span></span> |
    | <span data-ttu-id="b14f7-190">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsfqbnversion</span><span class="sxs-lookup"><span data-stu-id="b14f7-190">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsfqbnversion</span></span> |
    | <span data-ttu-id="b14f7-191">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowssubauthority</span><span class="sxs-lookup"><span data-stu-id="b14f7-191">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowssubauthority</span></span> |
    | <span data-ttu-id="b14f7-192">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsuserclaim</span><span class="sxs-lookup"><span data-stu-id="b14f7-192">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsuserclaim</span></span> |
    | <span data-ttu-id="b14f7-193">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/x500distinguishedname</span><span class="sxs-lookup"><span data-stu-id="b14f7-193">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/x500distinguishedname</span></span> |
    | <span data-ttu-id="b14f7-194">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn</span><span class="sxs-lookup"><span data-stu-id="b14f7-194">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn</span></span> |
    | <span data-ttu-id="b14f7-195">http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid</span><span class="sxs-lookup"><span data-stu-id="b14f7-195">http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid</span></span> |
    | <span data-ttu-id="b14f7-196">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn</span><span class="sxs-lookup"><span data-stu-id="b14f7-196">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn</span></span> |
    | <span data-ttu-id="b14f7-197">http://schemas.microsoft.com/ws/2008/06/identity/claims/ispersistent</span><span class="sxs-lookup"><span data-stu-id="b14f7-197">http://schemas.microsoft.com/ws/2008/06/identity/claims/ispersistent</span></span> |
    | <span data-ttu-id="b14f7-198">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier</span><span class="sxs-lookup"><span data-stu-id="b14f7-198">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier</span></span> |
    | <span data-ttu-id="b14f7-199">http://schemas.microsoft.com/identity/claims/scope</span><span class="sxs-lookup"><span data-stu-id="b14f7-199">http://schemas.microsoft.com/identity/claims/scope</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b14f7-200">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b14f7-200">Next steps</span></span>
* [<span data-ttu-id="b14f7-201">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="b14f7-201">Article Index for Application Management in Azure Active Directory</span></span>](../active-directory-apps-index.md)
* [<span data-ttu-id="b14f7-202">設定對不在 Azure Active Directory 應用程式庫中的應用程式的單一登入</span><span class="sxs-lookup"><span data-stu-id="b14f7-202">Configuring single sign-on to applications that are not in the Azure Active Directory application gallery</span></span>](../active-directory-saas-custom-apps.md)
* [<span data-ttu-id="b14f7-203">SAML 型單一登入疑難排解</span><span class="sxs-lookup"><span data-stu-id="b14f7-203">Troubleshooting SAML-Based Single Sign-On</span></span>](active-directory-saml-debugging.md)

<!--Image references-->
[1]: ./media/active-directory-saml-claims-customization/user-attribute-section.png
[2]: ./media/active-directory-saml-claims-customization/edit-claim-name-value.png
[3]: ./media/active-directory-saml-claims-customization/delete-claim.png
[4]: ./media/active-directory-saml-claims-customization/user-identifier.png
[5]: ./media/active-directory-saml-claims-customization/extractemailprefix-function.png
[6]: ./media/active-directory-saml-claims-customization/join-function.png
[7]: ./media/active-directory-saml-claims-customization/add-attribute.png