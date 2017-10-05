---
title: "Azure Active Directory 中的宣告對應 (公開預覽) | Microsoft Docs"
description: "此頁面說明 Azure Active Directory 宣告對應。"
services: active-directory
author: billmath
manager: femila
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: billmath
ms.openlocfilehash: 78dbbe085fca26ad529c6262ba852f3c06ace404
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="claims-mapping-in-azure-active-directory-public-preview"></a><span data-ttu-id="ff2f2-103">Azure Active Directory 中的宣告對應 (公開預覽)</span><span class="sxs-lookup"><span data-stu-id="ff2f2-103">Claims mapping in Azure Active Directory (public preview)</span></span>

>[!NOTE]
><span data-ttu-id="ff2f2-104">這項功能會取代目前透過入口網站提供的[宣告自訂](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-claims-customization)。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-104">This feature replaces and supersedes the [claims customization](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-claims-customization) offered through the portal today.</span></span> <span data-ttu-id="ff2f2-105">如果您在相同的應用程式中除了使用本文詳述的 Graph/PowerShell 方法外，還使用入口網站來自訂宣告，則針對該應用程式所核發的權杖將會忽略入口網站中的設定。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-105">If you customize claims using the portal in addition to the Graph/PowerShell method detailed in this document on the same application, tokens issued for that application will ignore the configuration in the portal.</span></span>
<span data-ttu-id="ff2f2-106">透過本文詳述的方法所進行的設定將不會反映在入口網站中。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-106">Configurations made through the methods detailed in this document will not be reflected in the portal.</span></span>

<span data-ttu-id="ff2f2-107">租用戶系統管理員會使用這項功能，以針對其租用戶的特定應用程式自訂權杖中所發出的宣告。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-107">This feature is used by tenant admins to customize the claims emitted in tokens for a specific application in their tenant.</span></span> <span data-ttu-id="ff2f2-108">您可以使用宣告對應原則來進行下列作業：</span><span class="sxs-lookup"><span data-stu-id="ff2f2-108">You can use claims mapping policies to:</span></span>

- <span data-ttu-id="ff2f2-109">選取要在權杖中包含哪些宣告。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-109">Select which claims are included in tokens.</span></span>
- <span data-ttu-id="ff2f2-110">建立尚未存在的宣告類型。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-110">Create claim types that do not already exist.</span></span>
- <span data-ttu-id="ff2f2-111">選擇或變更特定宣告中所發出的資料來源。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-111">Choose or change the source of data emitted in specific claims.</span></span>

>[!NOTE]
><span data-ttu-id="ff2f2-112">這項功能目前為公開預覽版。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-112">This capability currently is in public preview.</span></span> <span data-ttu-id="ff2f2-113">您應做好將任何變更還原或移除的準備。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-113">Be prepared to revert or remove any changes.</span></span> <span data-ttu-id="ff2f2-114">公用預覽版期間功能可用於任何 Azure Active Directory (Azure AD) 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-114">The feature is available in any Azure Active Directory (Azure AD) subscription during public preview.</span></span> <span data-ttu-id="ff2f2-115">不過，當功能正式推出時，功能的某些層面可能需要 Azure Active Directory Premium 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-115">However, when the feature becomes generally available, some aspects of the feature might require an Azure Active Directory premium subscription.</span></span>

## <a name="claims-mapping-policy-type"></a><span data-ttu-id="ff2f2-116">宣告對應原則類型</span><span class="sxs-lookup"><span data-stu-id="ff2f2-116">Claims mapping policy type</span></span>
<span data-ttu-id="ff2f2-117">在 Azure AD 中，**原則**物件代表個別應用程式或組織中的所有應用程式上強制執行的一組規則。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-117">In Azure AD, a **Policy** object represents a set of rules enforced on individual applications, or on all applications in an organization.</span></span> <span data-ttu-id="ff2f2-118">每個類型的原則都具有包含一組屬性的獨特結構，這些屬性會接著套用至它們已被指派的物件。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-118">Each type of policy has a unique structure, with a set of properties that are then applied to objects to which they are assigned.</span></span>

<span data-ttu-id="ff2f2-119">宣告對應原則是一種**原則**物件，會修改針對特定應用程式所核發之權杖所發出的宣告。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-119">A claims mapping policy is a type of **Policy** object that modifies the claims emitted in tokens issued for specific applications.</span></span>

## <a name="claim-sets"></a><span data-ttu-id="ff2f2-120">宣告集</span><span class="sxs-lookup"><span data-stu-id="ff2f2-120">Claim sets</span></span>
<span data-ttu-id="ff2f2-121">某些宣告集會定義其在權杖中的使用方式和時機。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-121">There are certain sets of claims that define how and when they are used in tokens.</span></span>

### <a name="core-claim-set"></a><span data-ttu-id="ff2f2-122">核心宣告集</span><span class="sxs-lookup"><span data-stu-id="ff2f2-122">Core claim set</span></span>
<span data-ttu-id="ff2f2-123">核心宣告集中的宣告會出現在每個權杖中，不論其原則為何。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-123">Claims in the core claim set are present in every token, regardless of policy.</span></span> <span data-ttu-id="ff2f2-124">系統會將這些宣告視為受限制宣告，您無法加以修改。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-124">These claims are also considered restricted, and cannot be modified.</span></span>

### <a name="basic-claim-set"></a><span data-ttu-id="ff2f2-125">基本宣告集</span><span class="sxs-lookup"><span data-stu-id="ff2f2-125">Basic claim set</span></span>
<span data-ttu-id="ff2f2-126">基本宣告集包含預設會針對權杖所發出的宣告 (除了核心宣告集以外)。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-126">The basic claim set includes the claims that are emitted by default for tokens (in addition to the core claim set).</span></span> <span data-ttu-id="ff2f2-127">使用宣告對應原則即可省略或修改這些宣告。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-127">These claims can be omitted or modified by using the claims mapping policies.</span></span>

### <a name="restricted-claim-set"></a><span data-ttu-id="ff2f2-128">受限制的宣告集</span><span class="sxs-lookup"><span data-stu-id="ff2f2-128">Restricted claim set</span></span>
<span data-ttu-id="ff2f2-129">無法使用原則來修改的受限制宣告。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-129">Restricted claims cannot be modified by using policy.</span></span> <span data-ttu-id="ff2f2-130">您無法變更資料來源，而且在產生這些宣告時不會套用任何轉換。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-130">The data source cannot be changed, and no transformation is applied when generating these claims.</span></span>

#### <a name="table-1-json-web-token-jwt-restricted-claim-set"></a><span data-ttu-id="ff2f2-131">表 1：JSON Web 權杖 (JWT) 的受限制宣告集</span><span class="sxs-lookup"><span data-stu-id="ff2f2-131">Table 1: JSON Web Token (JWT) restricted claim set</span></span>
|<span data-ttu-id="ff2f2-132">宣告類型 (名稱)</span><span class="sxs-lookup"><span data-stu-id="ff2f2-132">Claim type (name)</span></span>|
| ----- |
|<span data-ttu-id="ff2f2-133">_claim_names</span><span class="sxs-lookup"><span data-stu-id="ff2f2-133">_claim_names</span></span>|
|<span data-ttu-id="ff2f2-134">_claim_sources</span><span class="sxs-lookup"><span data-stu-id="ff2f2-134">_claim_sources</span></span>|
|<span data-ttu-id="ff2f2-135">access_token</span><span class="sxs-lookup"><span data-stu-id="ff2f2-135">access_token</span></span>|
|<span data-ttu-id="ff2f2-136">account_type</span><span class="sxs-lookup"><span data-stu-id="ff2f2-136">account_type</span></span>|
|<span data-ttu-id="ff2f2-137">acr</span><span class="sxs-lookup"><span data-stu-id="ff2f2-137">acr</span></span>|
|<span data-ttu-id="ff2f2-138">actor</span><span class="sxs-lookup"><span data-stu-id="ff2f2-138">actor</span></span>|
|<span data-ttu-id="ff2f2-139">actortoken</span><span class="sxs-lookup"><span data-stu-id="ff2f2-139">actortoken</span></span>|
|<span data-ttu-id="ff2f2-140">aio</span><span class="sxs-lookup"><span data-stu-id="ff2f2-140">aio</span></span>|
|<span data-ttu-id="ff2f2-141">altsecid</span><span class="sxs-lookup"><span data-stu-id="ff2f2-141">altsecid</span></span>|
|<span data-ttu-id="ff2f2-142">amr</span><span class="sxs-lookup"><span data-stu-id="ff2f2-142">amr</span></span>|
|<span data-ttu-id="ff2f2-143">app_chain</span><span class="sxs-lookup"><span data-stu-id="ff2f2-143">app_chain</span></span>|
|<span data-ttu-id="ff2f2-144">app_displayname</span><span class="sxs-lookup"><span data-stu-id="ff2f2-144">app_displayname</span></span>|
|<span data-ttu-id="ff2f2-145">app_res</span><span class="sxs-lookup"><span data-stu-id="ff2f2-145">app_res</span></span>|
|<span data-ttu-id="ff2f2-146">appctx</span><span class="sxs-lookup"><span data-stu-id="ff2f2-146">appctx</span></span>|
|<span data-ttu-id="ff2f2-147">appctxsender</span><span class="sxs-lookup"><span data-stu-id="ff2f2-147">appctxsender</span></span>|
|<span data-ttu-id="ff2f2-148">appid</span><span class="sxs-lookup"><span data-stu-id="ff2f2-148">appid</span></span>|
|<span data-ttu-id="ff2f2-149">appidacr</span><span class="sxs-lookup"><span data-stu-id="ff2f2-149">appidacr</span></span>|
|<span data-ttu-id="ff2f2-150">assertion</span><span class="sxs-lookup"><span data-stu-id="ff2f2-150">assertion</span></span>|
|<span data-ttu-id="ff2f2-151">at_hash</span><span class="sxs-lookup"><span data-stu-id="ff2f2-151">at_hash</span></span>|
|<span data-ttu-id="ff2f2-152">aud</span><span class="sxs-lookup"><span data-stu-id="ff2f2-152">aud</span></span>|
|<span data-ttu-id="ff2f2-153">auth_data</span><span class="sxs-lookup"><span data-stu-id="ff2f2-153">auth_data</span></span>|
|<span data-ttu-id="ff2f2-154">auth_time</span><span class="sxs-lookup"><span data-stu-id="ff2f2-154">auth_time</span></span>|
|<span data-ttu-id="ff2f2-155">authorization_code</span><span class="sxs-lookup"><span data-stu-id="ff2f2-155">authorization_code</span></span>|
|<span data-ttu-id="ff2f2-156">azp</span><span class="sxs-lookup"><span data-stu-id="ff2f2-156">azp</span></span>|
|<span data-ttu-id="ff2f2-157">azpacr</span><span class="sxs-lookup"><span data-stu-id="ff2f2-157">azpacr</span></span>|
|<span data-ttu-id="ff2f2-158">c_hash</span><span class="sxs-lookup"><span data-stu-id="ff2f2-158">c_hash</span></span>|
|<span data-ttu-id="ff2f2-159">ca_enf</span><span class="sxs-lookup"><span data-stu-id="ff2f2-159">ca_enf</span></span>|
|<span data-ttu-id="ff2f2-160">副本</span><span class="sxs-lookup"><span data-stu-id="ff2f2-160">cc</span></span>|
|<span data-ttu-id="ff2f2-161">cert_token_use</span><span class="sxs-lookup"><span data-stu-id="ff2f2-161">cert_token_use</span></span>|
|<span data-ttu-id="ff2f2-162">client_id</span><span class="sxs-lookup"><span data-stu-id="ff2f2-162">client_id</span></span>|
|<span data-ttu-id="ff2f2-163">cloud_graph_host_name</span><span class="sxs-lookup"><span data-stu-id="ff2f2-163">cloud_graph_host_name</span></span>|
|<span data-ttu-id="ff2f2-164">cloud_instance_name</span><span class="sxs-lookup"><span data-stu-id="ff2f2-164">cloud_instance_name</span></span>|
|<span data-ttu-id="ff2f2-165">cnf</span><span class="sxs-lookup"><span data-stu-id="ff2f2-165">cnf</span></span>|
|<span data-ttu-id="ff2f2-166">code</span><span class="sxs-lookup"><span data-stu-id="ff2f2-166">code</span></span>|
|<span data-ttu-id="ff2f2-167">controls</span><span class="sxs-lookup"><span data-stu-id="ff2f2-167">controls</span></span>|
|<span data-ttu-id="ff2f2-168">credential_keys</span><span class="sxs-lookup"><span data-stu-id="ff2f2-168">credential_keys</span></span>|
|<span data-ttu-id="ff2f2-169">csr</span><span class="sxs-lookup"><span data-stu-id="ff2f2-169">csr</span></span>|
|<span data-ttu-id="ff2f2-170">csr_type</span><span class="sxs-lookup"><span data-stu-id="ff2f2-170">csr_type</span></span>|
|<span data-ttu-id="ff2f2-171">deviceid</span><span class="sxs-lookup"><span data-stu-id="ff2f2-171">deviceid</span></span>|
|<span data-ttu-id="ff2f2-172">dns_names</span><span class="sxs-lookup"><span data-stu-id="ff2f2-172">dns_names</span></span>|
|<span data-ttu-id="ff2f2-173">domain_dns_name</span><span class="sxs-lookup"><span data-stu-id="ff2f2-173">domain_dns_name</span></span>|
|<span data-ttu-id="ff2f2-174">domain_netbios_name</span><span class="sxs-lookup"><span data-stu-id="ff2f2-174">domain_netbios_name</span></span>|
|<span data-ttu-id="ff2f2-175">e_exp</span><span class="sxs-lookup"><span data-stu-id="ff2f2-175">e_exp</span></span>|
|<span data-ttu-id="ff2f2-176">電子郵件</span><span class="sxs-lookup"><span data-stu-id="ff2f2-176">email</span></span>|
|<span data-ttu-id="ff2f2-177">endpoint</span><span class="sxs-lookup"><span data-stu-id="ff2f2-177">endpoint</span></span>|
|<span data-ttu-id="ff2f2-178">enfpolids</span><span class="sxs-lookup"><span data-stu-id="ff2f2-178">enfpolids</span></span>|
|<span data-ttu-id="ff2f2-179">exp</span><span class="sxs-lookup"><span data-stu-id="ff2f2-179">exp</span></span>|
|<span data-ttu-id="ff2f2-180">expires_on</span><span class="sxs-lookup"><span data-stu-id="ff2f2-180">expires_on</span></span>|
|<span data-ttu-id="ff2f2-181">grant_type</span><span class="sxs-lookup"><span data-stu-id="ff2f2-181">grant_type</span></span>|
|<span data-ttu-id="ff2f2-182">graph</span><span class="sxs-lookup"><span data-stu-id="ff2f2-182">graph</span></span>|
|<span data-ttu-id="ff2f2-183">group_sids</span><span class="sxs-lookup"><span data-stu-id="ff2f2-183">group_sids</span></span>|
|<span data-ttu-id="ff2f2-184">groups</span><span class="sxs-lookup"><span data-stu-id="ff2f2-184">groups</span></span>|
|<span data-ttu-id="ff2f2-185">hasgroups</span><span class="sxs-lookup"><span data-stu-id="ff2f2-185">hasgroups</span></span>|
|<span data-ttu-id="ff2f2-186">hash_alg</span><span class="sxs-lookup"><span data-stu-id="ff2f2-186">hash_alg</span></span>|
|<span data-ttu-id="ff2f2-187">home_oid</span><span class="sxs-lookup"><span data-stu-id="ff2f2-187">home_oid</span></span>|
|<span data-ttu-id="ff2f2-188">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant</span><span class="sxs-lookup"><span data-stu-id="ff2f2-188">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant</span></span>|
|<span data-ttu-id="ff2f2-189">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod</span><span class="sxs-lookup"><span data-stu-id="ff2f2-189">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod</span></span>|
|<span data-ttu-id="ff2f2-190">http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration</span><span class="sxs-lookup"><span data-stu-id="ff2f2-190">http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration</span></span>|
|<span data-ttu-id="ff2f2-191">http://schemas.microsoft.com/ws/2008/06/identity/claims/expired</span><span class="sxs-lookup"><span data-stu-id="ff2f2-191">http://schemas.microsoft.com/ws/2008/06/identity/claims/expired</span></span>|
|<span data-ttu-id="ff2f2-192">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span><span class="sxs-lookup"><span data-stu-id="ff2f2-192">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span></span>|
|<span data-ttu-id="ff2f2-193">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name</span><span class="sxs-lookup"><span data-stu-id="ff2f2-193">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name</span></span>|
|<span data-ttu-id="ff2f2-194">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier</span><span class="sxs-lookup"><span data-stu-id="ff2f2-194">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier</span></span>|
|<span data-ttu-id="ff2f2-195">iat</span><span class="sxs-lookup"><span data-stu-id="ff2f2-195">iat</span></span>|
|<span data-ttu-id="ff2f2-196">identityprovider</span><span class="sxs-lookup"><span data-stu-id="ff2f2-196">identityprovider</span></span>|
|<span data-ttu-id="ff2f2-197">idp</span><span class="sxs-lookup"><span data-stu-id="ff2f2-197">idp</span></span>|
|<span data-ttu-id="ff2f2-198">in_corp</span><span class="sxs-lookup"><span data-stu-id="ff2f2-198">in_corp</span></span>|
|<span data-ttu-id="ff2f2-199">instance</span><span class="sxs-lookup"><span data-stu-id="ff2f2-199">instance</span></span>|
|<span data-ttu-id="ff2f2-200">ipaddr</span><span class="sxs-lookup"><span data-stu-id="ff2f2-200">ipaddr</span></span>|
|<span data-ttu-id="ff2f2-201">isbrowserhostedapp</span><span class="sxs-lookup"><span data-stu-id="ff2f2-201">isbrowserhostedapp</span></span>|
|<span data-ttu-id="ff2f2-202">iss</span><span class="sxs-lookup"><span data-stu-id="ff2f2-202">iss</span></span>|
|<span data-ttu-id="ff2f2-203">jwk</span><span class="sxs-lookup"><span data-stu-id="ff2f2-203">jwk</span></span>|
|<span data-ttu-id="ff2f2-204">key_id</span><span class="sxs-lookup"><span data-stu-id="ff2f2-204">key_id</span></span>|
|<span data-ttu-id="ff2f2-205">key_type</span><span class="sxs-lookup"><span data-stu-id="ff2f2-205">key_type</span></span>|
|<span data-ttu-id="ff2f2-206">mam_compliance_url</span><span class="sxs-lookup"><span data-stu-id="ff2f2-206">mam_compliance_url</span></span>|
|<span data-ttu-id="ff2f2-207">mam_enrollment_url</span><span class="sxs-lookup"><span data-stu-id="ff2f2-207">mam_enrollment_url</span></span>|
|<span data-ttu-id="ff2f2-208">mam_terms_of_use_url</span><span class="sxs-lookup"><span data-stu-id="ff2f2-208">mam_terms_of_use_url</span></span>|
|<span data-ttu-id="ff2f2-209">mdm_compliance_url</span><span class="sxs-lookup"><span data-stu-id="ff2f2-209">mdm_compliance_url</span></span>|
|<span data-ttu-id="ff2f2-210">mdm_enrollment_url</span><span class="sxs-lookup"><span data-stu-id="ff2f2-210">mdm_enrollment_url</span></span>|
|<span data-ttu-id="ff2f2-211">mdm_terms_of_use_url</span><span class="sxs-lookup"><span data-stu-id="ff2f2-211">mdm_terms_of_use_url</span></span>|
|<span data-ttu-id="ff2f2-212">nameid</span><span class="sxs-lookup"><span data-stu-id="ff2f2-212">nameid</span></span>|
|<span data-ttu-id="ff2f2-213">nbf</span><span class="sxs-lookup"><span data-stu-id="ff2f2-213">nbf</span></span>|
|<span data-ttu-id="ff2f2-214">netbios_name</span><span class="sxs-lookup"><span data-stu-id="ff2f2-214">netbios_name</span></span>|
|<span data-ttu-id="ff2f2-215">nonce</span><span class="sxs-lookup"><span data-stu-id="ff2f2-215">nonce</span></span>|
|<span data-ttu-id="ff2f2-216">oid</span><span class="sxs-lookup"><span data-stu-id="ff2f2-216">oid</span></span>|
|<span data-ttu-id="ff2f2-217">on_prem_id</span><span class="sxs-lookup"><span data-stu-id="ff2f2-217">on_prem_id</span></span>|
|<span data-ttu-id="ff2f2-218">onprem_sam_account_name</span><span class="sxs-lookup"><span data-stu-id="ff2f2-218">onprem_sam_account_name</span></span>|
|<span data-ttu-id="ff2f2-219">onprem_sid</span><span class="sxs-lookup"><span data-stu-id="ff2f2-219">onprem_sid</span></span>|
|<span data-ttu-id="ff2f2-220">openid2_id</span><span class="sxs-lookup"><span data-stu-id="ff2f2-220">openid2_id</span></span>|
|<span data-ttu-id="ff2f2-221">password</span><span class="sxs-lookup"><span data-stu-id="ff2f2-221">password</span></span>|
|<span data-ttu-id="ff2f2-222">platf</span><span class="sxs-lookup"><span data-stu-id="ff2f2-222">platf</span></span>|
|<span data-ttu-id="ff2f2-223">polids</span><span class="sxs-lookup"><span data-stu-id="ff2f2-223">polids</span></span>|
|<span data-ttu-id="ff2f2-224">pop_jwk</span><span class="sxs-lookup"><span data-stu-id="ff2f2-224">pop_jwk</span></span>|
|<span data-ttu-id="ff2f2-225">preferred_username</span><span class="sxs-lookup"><span data-stu-id="ff2f2-225">preferred_username</span></span>|
|<span data-ttu-id="ff2f2-226">previous_refresh_token</span><span class="sxs-lookup"><span data-stu-id="ff2f2-226">previous_refresh_token</span></span>|
|<span data-ttu-id="ff2f2-227">primary_sid</span><span class="sxs-lookup"><span data-stu-id="ff2f2-227">primary_sid</span></span>|
|<span data-ttu-id="ff2f2-228">puid</span><span class="sxs-lookup"><span data-stu-id="ff2f2-228">puid</span></span>|
|<span data-ttu-id="ff2f2-229">pwd_exp</span><span class="sxs-lookup"><span data-stu-id="ff2f2-229">pwd_exp</span></span>|
|<span data-ttu-id="ff2f2-230">pwd_url</span><span class="sxs-lookup"><span data-stu-id="ff2f2-230">pwd_url</span></span>|
|<span data-ttu-id="ff2f2-231">redirect_uri</span><span class="sxs-lookup"><span data-stu-id="ff2f2-231">redirect_uri</span></span>|
|<span data-ttu-id="ff2f2-232">refresh_token</span><span class="sxs-lookup"><span data-stu-id="ff2f2-232">refresh_token</span></span>|
|<span data-ttu-id="ff2f2-233">refreshtoken</span><span class="sxs-lookup"><span data-stu-id="ff2f2-233">refreshtoken</span></span>|
|<span data-ttu-id="ff2f2-234">request_nonce</span><span class="sxs-lookup"><span data-stu-id="ff2f2-234">request_nonce</span></span>|
|<span data-ttu-id="ff2f2-235">資源</span><span class="sxs-lookup"><span data-stu-id="ff2f2-235">resource</span></span>|
|<span data-ttu-id="ff2f2-236">角色</span><span class="sxs-lookup"><span data-stu-id="ff2f2-236">role</span></span>|
|<span data-ttu-id="ff2f2-237">角色</span><span class="sxs-lookup"><span data-stu-id="ff2f2-237">roles</span></span>|
|<span data-ttu-id="ff2f2-238">scope</span><span class="sxs-lookup"><span data-stu-id="ff2f2-238">scope</span></span>|
|<span data-ttu-id="ff2f2-239">scp</span><span class="sxs-lookup"><span data-stu-id="ff2f2-239">scp</span></span>|
|<span data-ttu-id="ff2f2-240">sid</span><span class="sxs-lookup"><span data-stu-id="ff2f2-240">sid</span></span>|
|<span data-ttu-id="ff2f2-241">signature</span><span class="sxs-lookup"><span data-stu-id="ff2f2-241">signature</span></span>|
|<span data-ttu-id="ff2f2-242">signin_state</span><span class="sxs-lookup"><span data-stu-id="ff2f2-242">signin_state</span></span>|
|<span data-ttu-id="ff2f2-243">src1</span><span class="sxs-lookup"><span data-stu-id="ff2f2-243">src1</span></span>|
|<span data-ttu-id="ff2f2-244">src2</span><span class="sxs-lookup"><span data-stu-id="ff2f2-244">src2</span></span>|
|<span data-ttu-id="ff2f2-245">sub</span><span class="sxs-lookup"><span data-stu-id="ff2f2-245">sub</span></span>|
|<span data-ttu-id="ff2f2-246">tbid</span><span class="sxs-lookup"><span data-stu-id="ff2f2-246">tbid</span></span>|
|<span data-ttu-id="ff2f2-247">tenant_display_name</span><span class="sxs-lookup"><span data-stu-id="ff2f2-247">tenant_display_name</span></span>|
|<span data-ttu-id="ff2f2-248">tenant_region_scope</span><span class="sxs-lookup"><span data-stu-id="ff2f2-248">tenant_region_scope</span></span>|
|<span data-ttu-id="ff2f2-249">thumbnail_photo</span><span class="sxs-lookup"><span data-stu-id="ff2f2-249">thumbnail_photo</span></span>|
|<span data-ttu-id="ff2f2-250">tid</span><span class="sxs-lookup"><span data-stu-id="ff2f2-250">tid</span></span>|
|<span data-ttu-id="ff2f2-251">tokenAutologonEnabled</span><span class="sxs-lookup"><span data-stu-id="ff2f2-251">tokenAutologonEnabled</span></span>|
|<span data-ttu-id="ff2f2-252">trustedfordelegation</span><span class="sxs-lookup"><span data-stu-id="ff2f2-252">trustedfordelegation</span></span>|
|<span data-ttu-id="ff2f2-253">unique_name</span><span class="sxs-lookup"><span data-stu-id="ff2f2-253">unique_name</span></span>|
|<span data-ttu-id="ff2f2-254">upn</span><span class="sxs-lookup"><span data-stu-id="ff2f2-254">upn</span></span>|
|<span data-ttu-id="ff2f2-255">user_setting_sync_url</span><span class="sxs-lookup"><span data-stu-id="ff2f2-255">user_setting_sync_url</span></span>|
|<span data-ttu-id="ff2f2-256">username</span><span class="sxs-lookup"><span data-stu-id="ff2f2-256">username</span></span>|
|<span data-ttu-id="ff2f2-257">uti</span><span class="sxs-lookup"><span data-stu-id="ff2f2-257">uti</span></span>|
|<span data-ttu-id="ff2f2-258">ver</span><span class="sxs-lookup"><span data-stu-id="ff2f2-258">ver</span></span>|
|<span data-ttu-id="ff2f2-259">verified_primary_email</span><span class="sxs-lookup"><span data-stu-id="ff2f2-259">verified_primary_email</span></span>|
|<span data-ttu-id="ff2f2-260">verified_secondary_email</span><span class="sxs-lookup"><span data-stu-id="ff2f2-260">verified_secondary_email</span></span>|
|<span data-ttu-id="ff2f2-261">wids</span><span class="sxs-lookup"><span data-stu-id="ff2f2-261">wids</span></span>|
|<span data-ttu-id="ff2f2-262">win_ver</span><span class="sxs-lookup"><span data-stu-id="ff2f2-262">win_ver</span></span>|

#### <a name="table-2-security-assertion-markup-language-saml-restricted-claim-set"></a><span data-ttu-id="ff2f2-263">表 2：安全性聲明標記語言 (SAML) 的受限制宣告集</span><span class="sxs-lookup"><span data-stu-id="ff2f2-263">Table 2: Security Assertion Markup Language (SAML) restricted claim set</span></span>
|<span data-ttu-id="ff2f2-264">宣告類型 (URI)</span><span class="sxs-lookup"><span data-stu-id="ff2f2-264">Claim type (URI)</span></span>|
| ----- |
|<span data-ttu-id="ff2f2-265">http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration</span><span class="sxs-lookup"><span data-stu-id="ff2f2-265">http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration</span></span>|
|<span data-ttu-id="ff2f2-266">http://schemas.microsoft.com/ws/2008/06/identity/claims/expired</span><span class="sxs-lookup"><span data-stu-id="ff2f2-266">http://schemas.microsoft.com/ws/2008/06/identity/claims/expired</span></span>|
|<span data-ttu-id="ff2f2-267">http://schemas.microsoft.com/identity/claims/accesstoken</span><span class="sxs-lookup"><span data-stu-id="ff2f2-267">http://schemas.microsoft.com/identity/claims/accesstoken</span></span>|
|<span data-ttu-id="ff2f2-268">http://schemas.microsoft.com/identity/claims/openid2_id</span><span class="sxs-lookup"><span data-stu-id="ff2f2-268">http://schemas.microsoft.com/identity/claims/openid2_id</span></span>|
|<span data-ttu-id="ff2f2-269">http://schemas.microsoft.com/identity/claims/identityprovider</span><span class="sxs-lookup"><span data-stu-id="ff2f2-269">http://schemas.microsoft.com/identity/claims/identityprovider</span></span>|
|<span data-ttu-id="ff2f2-270">http://schemas.microsoft.com/identity/claims/objectidentifier</span><span class="sxs-lookup"><span data-stu-id="ff2f2-270">http://schemas.microsoft.com/identity/claims/objectidentifier</span></span>|
|<span data-ttu-id="ff2f2-271">http://schemas.microsoft.com/identity/claims/puid</span><span class="sxs-lookup"><span data-stu-id="ff2f2-271">http://schemas.microsoft.com/identity/claims/puid</span></span>|
|<span data-ttu-id="ff2f2-272">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier[MR1]</span><span class="sxs-lookup"><span data-stu-id="ff2f2-272">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier[MR1]</span></span> |
|<span data-ttu-id="ff2f2-273">http://schemas.microsoft.com/identity/claims/tenantid</span><span class="sxs-lookup"><span data-stu-id="ff2f2-273">http://schemas.microsoft.com/identity/claims/tenantid</span></span>|
|<span data-ttu-id="ff2f2-274">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant</span><span class="sxs-lookup"><span data-stu-id="ff2f2-274">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant</span></span>|
|<span data-ttu-id="ff2f2-275">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod</span><span class="sxs-lookup"><span data-stu-id="ff2f2-275">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod</span></span>|
|<span data-ttu-id="ff2f2-276">http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider</span><span class="sxs-lookup"><span data-stu-id="ff2f2-276">http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider</span></span>|
|<span data-ttu-id="ff2f2-277">http://schemas.microsoft.com/ws/2008/06/identity/claims/groups</span><span class="sxs-lookup"><span data-stu-id="ff2f2-277">http://schemas.microsoft.com/ws/2008/06/identity/claims/groups</span></span>|
|<span data-ttu-id="ff2f2-278">http://schemas.microsoft.com/claims/groups.link</span><span class="sxs-lookup"><span data-stu-id="ff2f2-278">http://schemas.microsoft.com/claims/groups.link</span></span>|
|<span data-ttu-id="ff2f2-279">http://schemas.microsoft.com/ws/2008/06/identity/claims/role</span><span class="sxs-lookup"><span data-stu-id="ff2f2-279">http://schemas.microsoft.com/ws/2008/06/identity/claims/role</span></span>|
|<span data-ttu-id="ff2f2-280">http://schemas.microsoft.com/ws/2008/06/identity/claims/wids</span><span class="sxs-lookup"><span data-stu-id="ff2f2-280">http://schemas.microsoft.com/ws/2008/06/identity/claims/wids</span></span>|
|<span data-ttu-id="ff2f2-281">http://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant</span><span class="sxs-lookup"><span data-stu-id="ff2f2-281">http://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant</span></span>|
|<span data-ttu-id="ff2f2-282">http://schemas.microsoft.com/2014/02/devicecontext/claims/isknown</span><span class="sxs-lookup"><span data-stu-id="ff2f2-282">http://schemas.microsoft.com/2014/02/devicecontext/claims/isknown</span></span>|
|<span data-ttu-id="ff2f2-283">http://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged</span><span class="sxs-lookup"><span data-stu-id="ff2f2-283">http://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged</span></span>|
|<span data-ttu-id="ff2f2-284">http://schemas.microsoft.com/2014/03/psso</span><span class="sxs-lookup"><span data-stu-id="ff2f2-284">http://schemas.microsoft.com/2014/03/psso</span></span>|
|<span data-ttu-id="ff2f2-285">http://schemas.microsoft.com/claims/authnmethodsreferences</span><span class="sxs-lookup"><span data-stu-id="ff2f2-285">http://schemas.microsoft.com/claims/authnmethodsreferences</span></span>|
|<span data-ttu-id="ff2f2-286">http://schemas.xmlsoap.org/ws/2009/09/identity/claims/actor</span><span class="sxs-lookup"><span data-stu-id="ff2f2-286">http://schemas.xmlsoap.org/ws/2009/09/identity/claims/actor</span></span>|
|<span data-ttu-id="ff2f2-287">http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername</span><span class="sxs-lookup"><span data-stu-id="ff2f2-287">http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername</span></span>|
|<span data-ttu-id="ff2f2-288">http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey</span><span class="sxs-lookup"><span data-stu-id="ff2f2-288">http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey</span></span>|
|<span data-ttu-id="ff2f2-289">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname</span><span class="sxs-lookup"><span data-stu-id="ff2f2-289">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname</span></span>|
|<span data-ttu-id="ff2f2-290">http://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid</span><span class="sxs-lookup"><span data-stu-id="ff2f2-290">http://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid</span></span>|
|<span data-ttu-id="ff2f2-291">http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid</span><span class="sxs-lookup"><span data-stu-id="ff2f2-291">http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid</span></span>|
|<span data-ttu-id="ff2f2-292">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authorizationdecision</span><span class="sxs-lookup"><span data-stu-id="ff2f2-292">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authorizationdecision</span></span>|
|<span data-ttu-id="ff2f2-293">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authentication</span><span class="sxs-lookup"><span data-stu-id="ff2f2-293">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authentication</span></span>|
|<span data-ttu-id="ff2f2-294">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/sid</span><span class="sxs-lookup"><span data-stu-id="ff2f2-294">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/sid</span></span>|
|<span data-ttu-id="ff2f2-295">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarygroupsid</span><span class="sxs-lookup"><span data-stu-id="ff2f2-295">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarygroupsid</span></span>|
|<span data-ttu-id="ff2f2-296">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarysid</span><span class="sxs-lookup"><span data-stu-id="ff2f2-296">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarysid</span></span>|
|<span data-ttu-id="ff2f2-297">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid</span><span class="sxs-lookup"><span data-stu-id="ff2f2-297">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid</span></span>|
|<span data-ttu-id="ff2f2-298">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlywindowsdevicegroup</span><span class="sxs-lookup"><span data-stu-id="ff2f2-298">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlywindowsdevicegroup</span></span>|
|<span data-ttu-id="ff2f2-299">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdeviceclaim</span><span class="sxs-lookup"><span data-stu-id="ff2f2-299">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdeviceclaim</span></span>|
|<span data-ttu-id="ff2f2-300">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup</span><span class="sxs-lookup"><span data-stu-id="ff2f2-300">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup</span></span>|
|<span data-ttu-id="ff2f2-301">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsfqbnversion</span><span class="sxs-lookup"><span data-stu-id="ff2f2-301">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsfqbnversion</span></span>|
|<span data-ttu-id="ff2f2-302">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowssubauthority</span><span class="sxs-lookup"><span data-stu-id="ff2f2-302">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowssubauthority</span></span>|
|<span data-ttu-id="ff2f2-303">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsuserclaim</span><span class="sxs-lookup"><span data-stu-id="ff2f2-303">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsuserclaim</span></span>|
|<span data-ttu-id="ff2f2-304">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/x500distinguishedname</span><span class="sxs-lookup"><span data-stu-id="ff2f2-304">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/x500distinguishedname</span></span>|
|<span data-ttu-id="ff2f2-305">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn</span><span class="sxs-lookup"><span data-stu-id="ff2f2-305">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn</span></span>|
|<span data-ttu-id="ff2f2-306">http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid</span><span class="sxs-lookup"><span data-stu-id="ff2f2-306">http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid</span></span>|
|<span data-ttu-id="ff2f2-307">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn</span><span class="sxs-lookup"><span data-stu-id="ff2f2-307">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn</span></span>|
|<span data-ttu-id="ff2f2-308">http://schemas.microsoft.com/ws/2008/06/identity/claims/ispersistent</span><span class="sxs-lookup"><span data-stu-id="ff2f2-308">http://schemas.microsoft.com/ws/2008/06/identity/claims/ispersistent</span></span>|
|<span data-ttu-id="ff2f2-309">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier</span><span class="sxs-lookup"><span data-stu-id="ff2f2-309">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier</span></span>|
|<span data-ttu-id="ff2f2-310">http://schemas.microsoft.com/identity/claims/scope</span><span class="sxs-lookup"><span data-stu-id="ff2f2-310">http://schemas.microsoft.com/identity/claims/scope</span></span>|

## <a name="claims-mapping-policy-properties"></a><span data-ttu-id="ff2f2-311">宣告對應原則屬性</span><span class="sxs-lookup"><span data-stu-id="ff2f2-311">Claims mapping policy properties</span></span>
<span data-ttu-id="ff2f2-312">使用宣告對應原則屬性，即可控制要發出哪些宣告，以及要從哪個來源取得資料。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-312">Use the properties of a claims mapping policy to control which claims are emitted, and where the data is sourced from.</span></span> <span data-ttu-id="ff2f2-313">如果未設定任何原則，系統所發出的權杖就會包含核心宣告集、基本宣告集，以及應用程式選擇要收到的任何選擇性宣告。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-313">If no policy is set, the system issues tokens containing the core claim set, the basic claim set, and any optional claims that the application has chosen to receive.</span></span>

### <a name="include-basic-claim-set"></a><span data-ttu-id="ff2f2-314">包含基本宣告集</span><span class="sxs-lookup"><span data-stu-id="ff2f2-314">Include basic claim set</span></span>

<span data-ttu-id="ff2f2-315">**字串：**IncludeBasicClaimSet</span><span class="sxs-lookup"><span data-stu-id="ff2f2-315">**String:** IncludeBasicClaimSet</span></span>

<span data-ttu-id="ff2f2-316">**資料類型：**布林值 (True 或 False)</span><span class="sxs-lookup"><span data-stu-id="ff2f2-316">**Data type:** Boolean (True or False)</span></span>

<span data-ttu-id="ff2f2-317">**摘要：**此屬性會決定是否在此原則所影響到的權杖中包含基本宣告集。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-317">**Summary:** This property determines whether the basic claim set is included in tokens affected by this policy.</span></span> 

- <span data-ttu-id="ff2f2-318">如果設為 True，此原則所影響到的權杖中就會發出基本宣告集。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-318">If set to True, all claims in the basic claim set are emitted in tokens affected by the policy.</span></span> 
- <span data-ttu-id="ff2f2-319">如果設為 False，權杖中將不會包含基本宣告集的宣告，除非相同原則的宣告結構描述屬性中個別新增了這些宣告。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-319">If set to False, claims in the basic claim set are not in the tokens, unless they are individually added in the claims schema property of the same policy.</span></span>

>[!NOTE] 
><span data-ttu-id="ff2f2-320">核心宣告集中的宣告會出現在每個權杖中，不論此屬性的設定為何。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-320">Claims in the core claim set are present in every token, regardless of what this property is set to.</span></span> 

### <a name="claims-schema"></a><span data-ttu-id="ff2f2-321">宣告結構描述</span><span class="sxs-lookup"><span data-stu-id="ff2f2-321">Claims schema</span></span>

<span data-ttu-id="ff2f2-322">**字串：**ClaimsSchema</span><span class="sxs-lookup"><span data-stu-id="ff2f2-322">**String:** ClaimsSchema</span></span>

<span data-ttu-id="ff2f2-323">**資料類型：**具有一或多個宣告結構描述項目的 JSON blob</span><span class="sxs-lookup"><span data-stu-id="ff2f2-323">**Data type:** JSON blob with one or more claim schema entries</span></span>

<span data-ttu-id="ff2f2-324">**摘要：**此屬性會定義除了基本宣告集和核心宣告集以外，原則所影響到的權杖中還會有哪些宣告。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-324">**Summary:** This property defines which claims are present in the tokens affected by the policy, in addition to the basic claim set and the core claim set.</span></span>
<span data-ttu-id="ff2f2-325">此屬性中所定義的每個宣告結構描述項目必須有某些資訊。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-325">For each claim schema entry defined in this property, certain information is required.</span></span> <span data-ttu-id="ff2f2-326">您必須指定資料來自何處 (**值**或**來源/識別碼組**)，以及資料是以哪種宣告形式來發出 (**宣告類型**)。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-326">You must specify where the data is coming from (**Value** or **Source/ID pair**), and which claim the data is emitted as (**Claim Type**).</span></span>

### <a name="claim-schema-entry-elements"></a><span data-ttu-id="ff2f2-327">宣告結構描述項目的元素</span><span class="sxs-lookup"><span data-stu-id="ff2f2-327">Claim schema entry elements</span></span>

<span data-ttu-id="ff2f2-328">**值：**值元素會定義靜態值來作為宣告中發出的資料。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-328">**Value:** The Value element defines a static value as the data to be emitted in the claim.</span></span>

<span data-ttu-id="ff2f2-329">**來源/識別碼組：**來源和識別碼元素會定義宣告中的資料來自何處。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-329">**Source/ID pair:** The Source and ID elements define where the data in the claim is sourced from.</span></span> 

<span data-ttu-id="ff2f2-330">來源元素必須設為下列其中一個值：</span><span class="sxs-lookup"><span data-stu-id="ff2f2-330">The Source element must be set to one of the following:</span></span> 


- <span data-ttu-id="ff2f2-331">「使用者」：宣告中的資料是使用者物件上的屬性。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-331">"user": The data in the claim is a property on the User object.</span></span> 
- <span data-ttu-id="ff2f2-332">「應用程式」：宣告中的資料是應用程式 (用戶端) 服務主體上的屬性。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-332">"application": The data in the claim is a property on the application (client) service principal.</span></span> 
- <span data-ttu-id="ff2f2-333">「資源」：宣告中的資料是資源服務主體上的屬性。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-333">"resource": The data in the claim is a property on the resource service principal.</span></span>
- <span data-ttu-id="ff2f2-334">「對象」：宣告中的資料是作為權杖對象之服務主體 (用戶端或資源服務主體) 上的屬性。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-334">"audience": The data in the claim is a property on the service principal that is the audience of the token (either the client or resource service principal).</span></span>
- <span data-ttu-id="ff2f2-335">「公司」：宣告中的資料是資源租用戶之公司物件上的屬性。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-335">“company”: The data in the claim is a property on the resource tenant’s Company object.</span></span>
- <span data-ttu-id="ff2f2-336">「轉換」：宣告中的資料來自宣告轉換 (請參閱本文稍後的＜宣告轉換＞一節)。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-336">"transformation": The data in the claim is from claims transformation (see the "Claims transformation" section later in this article).</span></span> 

<span data-ttu-id="ff2f2-337">如果來源是轉換，則 **TransformationID** 元素也必須包含在這個宣告定義中。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-337">If the source is transformation, the **TransformationID** element must be included in this claim definition as well.</span></span>

<span data-ttu-id="ff2f2-338">識別碼元素可識別宣告的值是由來源上的哪個屬性所提供。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-338">The ID element identifies which property on the source provides the value for the claim.</span></span> <span data-ttu-id="ff2f2-339">下表列出每個來源值的有效識別碼值。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-339">The following table lists the values of ID valid for each value of Source.</span></span>

#### <a name="table-3-valid-id-values-per-source"></a><span data-ttu-id="ff2f2-340">表 3：每個來源的有效識別碼值</span><span class="sxs-lookup"><span data-stu-id="ff2f2-340">Table 3: Valid ID values per source</span></span>
|<span data-ttu-id="ff2f2-341">來源</span><span class="sxs-lookup"><span data-stu-id="ff2f2-341">Source</span></span>|<span data-ttu-id="ff2f2-342">ID</span><span class="sxs-lookup"><span data-stu-id="ff2f2-342">ID</span></span>|<span data-ttu-id="ff2f2-343">說明</span><span class="sxs-lookup"><span data-stu-id="ff2f2-343">Description</span></span>|
|-----|-----|-----|
|<span data-ttu-id="ff2f2-344">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-344">User</span></span>|<span data-ttu-id="ff2f2-345">surname</span><span class="sxs-lookup"><span data-stu-id="ff2f2-345">surname</span></span>|<span data-ttu-id="ff2f2-346">姓氏</span><span class="sxs-lookup"><span data-stu-id="ff2f2-346">Family Name</span></span>|
|<span data-ttu-id="ff2f2-347">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-347">User</span></span>|<span data-ttu-id="ff2f2-348">givenname</span><span class="sxs-lookup"><span data-stu-id="ff2f2-348">givenname</span></span>|<span data-ttu-id="ff2f2-349">名字</span><span class="sxs-lookup"><span data-stu-id="ff2f2-349">Given Name</span></span>|
|<span data-ttu-id="ff2f2-350">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-350">User</span></span>|<span data-ttu-id="ff2f2-351">displayname</span><span class="sxs-lookup"><span data-stu-id="ff2f2-351">displayname</span></span>|<span data-ttu-id="ff2f2-352">顯示名稱</span><span class="sxs-lookup"><span data-stu-id="ff2f2-352">Display Name</span></span>|
|<span data-ttu-id="ff2f2-353">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-353">User</span></span>|<span data-ttu-id="ff2f2-354">objectid</span><span class="sxs-lookup"><span data-stu-id="ff2f2-354">objectid</span></span>|<span data-ttu-id="ff2f2-355">ObjectID</span><span class="sxs-lookup"><span data-stu-id="ff2f2-355">ObjectID</span></span>|
|<span data-ttu-id="ff2f2-356">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-356">User</span></span>|<span data-ttu-id="ff2f2-357">mail</span><span class="sxs-lookup"><span data-stu-id="ff2f2-357">mail</span></span>|<span data-ttu-id="ff2f2-358">電子郵件地址</span><span class="sxs-lookup"><span data-stu-id="ff2f2-358">Email Address</span></span>|
|<span data-ttu-id="ff2f2-359">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-359">User</span></span>|<span data-ttu-id="ff2f2-360">userprincipalname</span><span class="sxs-lookup"><span data-stu-id="ff2f2-360">userprincipalname</span></span>|<span data-ttu-id="ff2f2-361">使用者主體名稱</span><span class="sxs-lookup"><span data-stu-id="ff2f2-361">User Principal Name</span></span>|
|<span data-ttu-id="ff2f2-362">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-362">User</span></span>|<span data-ttu-id="ff2f2-363">department</span><span class="sxs-lookup"><span data-stu-id="ff2f2-363">department</span></span>|<span data-ttu-id="ff2f2-364">department</span><span class="sxs-lookup"><span data-stu-id="ff2f2-364">Department</span></span>|
|<span data-ttu-id="ff2f2-365">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-365">User</span></span>|<span data-ttu-id="ff2f2-366">onpremisessamaccountname</span><span class="sxs-lookup"><span data-stu-id="ff2f2-366">onpremisessamaccountname</span></span>|<span data-ttu-id="ff2f2-367">內部部署的 Sam 帳戶名稱</span><span class="sxs-lookup"><span data-stu-id="ff2f2-367">On Premises Sam Account Name</span></span>|
|<span data-ttu-id="ff2f2-368">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-368">User</span></span>|<span data-ttu-id="ff2f2-369">netbiosname</span><span class="sxs-lookup"><span data-stu-id="ff2f2-369">netbiosname</span></span>|<span data-ttu-id="ff2f2-370">NetBios 名稱</span><span class="sxs-lookup"><span data-stu-id="ff2f2-370">NetBios Name</span></span>|
|<span data-ttu-id="ff2f2-371">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-371">User</span></span>|<span data-ttu-id="ff2f2-372">dnsdomainname</span><span class="sxs-lookup"><span data-stu-id="ff2f2-372">dnsdomainname</span></span>|<span data-ttu-id="ff2f2-373">Dns 網域名稱</span><span class="sxs-lookup"><span data-stu-id="ff2f2-373">Dns Domain Name</span></span>|
|<span data-ttu-id="ff2f2-374">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-374">User</span></span>|<span data-ttu-id="ff2f2-375">onpremisesecurityidentifier</span><span class="sxs-lookup"><span data-stu-id="ff2f2-375">onpremisesecurityidentifier</span></span>|<span data-ttu-id="ff2f2-376">內部部署的安全性識別碼</span><span class="sxs-lookup"><span data-stu-id="ff2f2-376">on-premises Security Identifier</span></span>|
|<span data-ttu-id="ff2f2-377">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-377">User</span></span>|<span data-ttu-id="ff2f2-378">companyname</span><span class="sxs-lookup"><span data-stu-id="ff2f2-378">companyname</span></span>|<span data-ttu-id="ff2f2-379">組織名稱</span><span class="sxs-lookup"><span data-stu-id="ff2f2-379">Organization Name</span></span>|
|<span data-ttu-id="ff2f2-380">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-380">User</span></span>|<span data-ttu-id="ff2f2-381">streetaddress</span><span class="sxs-lookup"><span data-stu-id="ff2f2-381">streetaddress</span></span>|<span data-ttu-id="ff2f2-382">街道地址</span><span class="sxs-lookup"><span data-stu-id="ff2f2-382">Street Address</span></span>|
|<span data-ttu-id="ff2f2-383">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-383">User</span></span>|<span data-ttu-id="ff2f2-384">postalcode</span><span class="sxs-lookup"><span data-stu-id="ff2f2-384">postalcode</span></span>|<span data-ttu-id="ff2f2-385">郵遞區號</span><span class="sxs-lookup"><span data-stu-id="ff2f2-385">Postal Code</span></span>|
|<span data-ttu-id="ff2f2-386">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-386">User</span></span>|<span data-ttu-id="ff2f2-387">preferredlanguange</span><span class="sxs-lookup"><span data-stu-id="ff2f2-387">preferredlanguange</span></span>|<span data-ttu-id="ff2f2-388">慣用語言</span><span class="sxs-lookup"><span data-stu-id="ff2f2-388">Preferred Language</span></span>|
|<span data-ttu-id="ff2f2-389">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-389">User</span></span>|<span data-ttu-id="ff2f2-390">onpremisesuserprincipalname</span><span class="sxs-lookup"><span data-stu-id="ff2f2-390">onpremisesuserprincipalname</span></span>|<span data-ttu-id="ff2f2-391">內部部署的 UPN</span><span class="sxs-lookup"><span data-stu-id="ff2f2-391">on-premises UPN</span></span>|
|<span data-ttu-id="ff2f2-392">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-392">User</span></span>|<span data-ttu-id="ff2f2-393">mailNickname</span><span class="sxs-lookup"><span data-stu-id="ff2f2-393">mailnickname</span></span>|<span data-ttu-id="ff2f2-394">郵件暱稱</span><span class="sxs-lookup"><span data-stu-id="ff2f2-394">Mail Nickname</span></span>|
|<span data-ttu-id="ff2f2-395">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-395">User</span></span>|<span data-ttu-id="ff2f2-396">extensionattribute1</span><span class="sxs-lookup"><span data-stu-id="ff2f2-396">extensionattribute1</span></span>|<span data-ttu-id="ff2f2-397">擴充屬性 1</span><span class="sxs-lookup"><span data-stu-id="ff2f2-397">Extension Attribute 1</span></span>|
|<span data-ttu-id="ff2f2-398">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-398">User</span></span>|<span data-ttu-id="ff2f2-399">extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="ff2f2-399">extensionattribute2</span></span>|<span data-ttu-id="ff2f2-400">擴充屬性 2</span><span class="sxs-lookup"><span data-stu-id="ff2f2-400">Extension Attribute 2</span></span>|
|<span data-ttu-id="ff2f2-401">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-401">User</span></span>|<span data-ttu-id="ff2f2-402">extensionattribute3</span><span class="sxs-lookup"><span data-stu-id="ff2f2-402">extensionattribute3</span></span>|<span data-ttu-id="ff2f2-403">擴充屬性 3</span><span class="sxs-lookup"><span data-stu-id="ff2f2-403">Extension Attribute 3</span></span>|
|<span data-ttu-id="ff2f2-404">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-404">User</span></span>|<span data-ttu-id="ff2f2-405">extensionattribute4</span><span class="sxs-lookup"><span data-stu-id="ff2f2-405">extensionattribute4</span></span>|<span data-ttu-id="ff2f2-406">擴充屬性 4</span><span class="sxs-lookup"><span data-stu-id="ff2f2-406">Extension Attribute 4</span></span>|
|<span data-ttu-id="ff2f2-407">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-407">User</span></span>|<span data-ttu-id="ff2f2-408">extensionattribute5</span><span class="sxs-lookup"><span data-stu-id="ff2f2-408">extensionattribute5</span></span>|<span data-ttu-id="ff2f2-409">擴充屬性 5</span><span class="sxs-lookup"><span data-stu-id="ff2f2-409">Extension Attribute 5</span></span>|
|<span data-ttu-id="ff2f2-410">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-410">User</span></span>|<span data-ttu-id="ff2f2-411">extensionattribute6</span><span class="sxs-lookup"><span data-stu-id="ff2f2-411">extensionattribute6</span></span>|<span data-ttu-id="ff2f2-412">擴充屬性 6</span><span class="sxs-lookup"><span data-stu-id="ff2f2-412">Extension Attribute 6</span></span>|
|<span data-ttu-id="ff2f2-413">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-413">User</span></span>|<span data-ttu-id="ff2f2-414">extensionattribute7</span><span class="sxs-lookup"><span data-stu-id="ff2f2-414">extensionattribute7</span></span>|<span data-ttu-id="ff2f2-415">擴充屬性 7</span><span class="sxs-lookup"><span data-stu-id="ff2f2-415">Extension Attribute 7</span></span>|
|<span data-ttu-id="ff2f2-416">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-416">User</span></span>|<span data-ttu-id="ff2f2-417">extensionattribute8</span><span class="sxs-lookup"><span data-stu-id="ff2f2-417">extensionattribute8</span></span>|<span data-ttu-id="ff2f2-418">擴充屬性 8</span><span class="sxs-lookup"><span data-stu-id="ff2f2-418">Extension Attribute 8</span></span>|
|<span data-ttu-id="ff2f2-419">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-419">User</span></span>|<span data-ttu-id="ff2f2-420">extensionattribute9</span><span class="sxs-lookup"><span data-stu-id="ff2f2-420">extensionattribute9</span></span>|<span data-ttu-id="ff2f2-421">擴充屬性 9</span><span class="sxs-lookup"><span data-stu-id="ff2f2-421">Extension Attribute 9</span></span>|
|<span data-ttu-id="ff2f2-422">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-422">User</span></span>|<span data-ttu-id="ff2f2-423">extensionattribute10</span><span class="sxs-lookup"><span data-stu-id="ff2f2-423">extensionattribute10</span></span>|<span data-ttu-id="ff2f2-424">擴充屬性 10</span><span class="sxs-lookup"><span data-stu-id="ff2f2-424">Extension Attribute 10</span></span>|
|<span data-ttu-id="ff2f2-425">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-425">User</span></span>|<span data-ttu-id="ff2f2-426">extensionattribute11</span><span class="sxs-lookup"><span data-stu-id="ff2f2-426">extensionattribute11</span></span>|<span data-ttu-id="ff2f2-427">擴充屬性 11</span><span class="sxs-lookup"><span data-stu-id="ff2f2-427">Extension Attribute 11</span></span>|
|<span data-ttu-id="ff2f2-428">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-428">User</span></span>|<span data-ttu-id="ff2f2-429">extensionattribute12</span><span class="sxs-lookup"><span data-stu-id="ff2f2-429">extensionattribute12</span></span>|<span data-ttu-id="ff2f2-430">擴充屬性 12</span><span class="sxs-lookup"><span data-stu-id="ff2f2-430">Extension Attribute 12</span></span>|
|<span data-ttu-id="ff2f2-431">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-431">User</span></span>|<span data-ttu-id="ff2f2-432">extensionattribute13</span><span class="sxs-lookup"><span data-stu-id="ff2f2-432">extensionattribute13</span></span>|<span data-ttu-id="ff2f2-433">擴充屬性 13</span><span class="sxs-lookup"><span data-stu-id="ff2f2-433">Extension Attribute 13</span></span>|
|<span data-ttu-id="ff2f2-434">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-434">User</span></span>|<span data-ttu-id="ff2f2-435">extensionattribute14</span><span class="sxs-lookup"><span data-stu-id="ff2f2-435">extensionattribute14</span></span>|<span data-ttu-id="ff2f2-436">擴充屬性 14</span><span class="sxs-lookup"><span data-stu-id="ff2f2-436">Extension Attribute 14</span></span>|
|<span data-ttu-id="ff2f2-437">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-437">User</span></span>|<span data-ttu-id="ff2f2-438">extensionattribute15</span><span class="sxs-lookup"><span data-stu-id="ff2f2-438">extensionattribute15</span></span>|<span data-ttu-id="ff2f2-439">擴充屬性 15</span><span class="sxs-lookup"><span data-stu-id="ff2f2-439">Extension Attribute 15</span></span>|
|<span data-ttu-id="ff2f2-440">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-440">User</span></span>|<span data-ttu-id="ff2f2-441">othermail</span><span class="sxs-lookup"><span data-stu-id="ff2f2-441">othermail</span></span>|<span data-ttu-id="ff2f2-442">其他郵件</span><span class="sxs-lookup"><span data-stu-id="ff2f2-442">Other Mail</span></span>|
|<span data-ttu-id="ff2f2-443">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-443">User</span></span>|<span data-ttu-id="ff2f2-444">country</span><span class="sxs-lookup"><span data-stu-id="ff2f2-444">country</span></span>|<span data-ttu-id="ff2f2-445">國家 (地區)</span><span class="sxs-lookup"><span data-stu-id="ff2f2-445">Country</span></span>|
|<span data-ttu-id="ff2f2-446">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-446">User</span></span>|<span data-ttu-id="ff2f2-447">city</span><span class="sxs-lookup"><span data-stu-id="ff2f2-447">city</span></span>|<span data-ttu-id="ff2f2-448">City</span><span class="sxs-lookup"><span data-stu-id="ff2f2-448">City</span></span>|
|<span data-ttu-id="ff2f2-449">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-449">User</span></span>|<span data-ttu-id="ff2f2-450">state</span><span class="sxs-lookup"><span data-stu-id="ff2f2-450">state</span></span>|<span data-ttu-id="ff2f2-451">State</span><span class="sxs-lookup"><span data-stu-id="ff2f2-451">State</span></span>|
|<span data-ttu-id="ff2f2-452">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-452">User</span></span>|<span data-ttu-id="ff2f2-453">jobtitle</span><span class="sxs-lookup"><span data-stu-id="ff2f2-453">jobtitle</span></span>|<span data-ttu-id="ff2f2-454">職稱</span><span class="sxs-lookup"><span data-stu-id="ff2f2-454">Job Title</span></span>|
|<span data-ttu-id="ff2f2-455">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-455">User</span></span>|<span data-ttu-id="ff2f2-456">employeeid</span><span class="sxs-lookup"><span data-stu-id="ff2f2-456">employeeid</span></span>|<span data-ttu-id="ff2f2-457">員工識別碼</span><span class="sxs-lookup"><span data-stu-id="ff2f2-457">Employee ID</span></span>|
|<span data-ttu-id="ff2f2-458">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-458">User</span></span>|<span data-ttu-id="ff2f2-459">facsimiletelephonenumber</span><span class="sxs-lookup"><span data-stu-id="ff2f2-459">facsimiletelephonenumber</span></span>|<span data-ttu-id="ff2f2-460">傳真電話號碼</span><span class="sxs-lookup"><span data-stu-id="ff2f2-460">Facsimile Telephone Number</span></span>|
|<span data-ttu-id="ff2f2-461">application, resource, audience</span><span class="sxs-lookup"><span data-stu-id="ff2f2-461">application, resource, audience</span></span>|<span data-ttu-id="ff2f2-462">displayname</span><span class="sxs-lookup"><span data-stu-id="ff2f2-462">displayname</span></span>|<span data-ttu-id="ff2f2-463">顯示名稱</span><span class="sxs-lookup"><span data-stu-id="ff2f2-463">Display Name</span></span>|
|<span data-ttu-id="ff2f2-464">application, resource, audience</span><span class="sxs-lookup"><span data-stu-id="ff2f2-464">application, resource, audience</span></span>|<span data-ttu-id="ff2f2-465">objected</span><span class="sxs-lookup"><span data-stu-id="ff2f2-465">objected</span></span>|<span data-ttu-id="ff2f2-466">ObjectID</span><span class="sxs-lookup"><span data-stu-id="ff2f2-466">ObjectID</span></span>|
|<span data-ttu-id="ff2f2-467">application, resource, audience</span><span class="sxs-lookup"><span data-stu-id="ff2f2-467">application, resource, audience</span></span>|<span data-ttu-id="ff2f2-468">tags</span><span class="sxs-lookup"><span data-stu-id="ff2f2-468">tags</span></span>|<span data-ttu-id="ff2f2-469">服務主體標籤</span><span class="sxs-lookup"><span data-stu-id="ff2f2-469">Service Principal Tag</span></span>|
|<span data-ttu-id="ff2f2-470">公司</span><span class="sxs-lookup"><span data-stu-id="ff2f2-470">Company</span></span>|<span data-ttu-id="ff2f2-471">tenantcountry</span><span class="sxs-lookup"><span data-stu-id="ff2f2-471">tenantcountry</span></span>|<span data-ttu-id="ff2f2-472">租用戶的國家/地區</span><span class="sxs-lookup"><span data-stu-id="ff2f2-472">Tenant’s country</span></span>|

<span data-ttu-id="ff2f2-473">**TransformationID：**只有在來源元素設定為「轉換」時，才必須提供 TransformationID 元素。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-473">**TransformationID:** The TransformationID element must be provided only if the Source element is set to “transformation”.</span></span>

- <span data-ttu-id="ff2f2-474">此元素必須符合 **ClaimsTransformation** 屬性 (會定義如何產生此宣告的資料) 中轉換項目的識別碼元素。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-474">This element must match the ID element of the transformation entry in the **ClaimsTransformation** property that defines how the data for this claim is generated.</span></span>

<span data-ttu-id="ff2f2-475">**宣告類型：****JwtClaimType** 和 **SamlClaimType** 元素會定義此宣告結構描述項目是參考哪個宣告。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-475">**Claim Type:** The **JwtClaimType** and **SamlClaimType** elements define which claim this claim schema entry refers to.</span></span>

- <span data-ttu-id="ff2f2-476">JwtClaimType 必須包含要在 JWT 中發出的宣告名稱。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-476">The JwtClaimType must contain the name of the claim to be emitted in JWTs.</span></span>
- <span data-ttu-id="ff2f2-477">SamlClaimType 必須包含要在 SAML 權杖中發出的宣告 URI。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-477">The SamlClaimType must contain the URI of the claim to be emitted in SAML tokens.</span></span>

>[!NOTE]
><span data-ttu-id="ff2f2-478">受限制宣告集裡面所含宣告的名稱和 URI 不能用於宣告類型元素。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-478">Names and URIs of claims in the restricted claim set cannot be used for the claim type elements.</span></span> <span data-ttu-id="ff2f2-479">如需詳細資訊，請參閱本文稍後的＜例外狀況和限制＞一節。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-479">For more information, see the "Exceptions and restrictions" section later in this article.</span></span>

### <a name="claims-transformation"></a><span data-ttu-id="ff2f2-480">宣告轉換</span><span class="sxs-lookup"><span data-stu-id="ff2f2-480">Claims transformation</span></span>

<span data-ttu-id="ff2f2-481">**字串：**ClaimsTransformation</span><span class="sxs-lookup"><span data-stu-id="ff2f2-481">**String:** ClaimsTransformation</span></span>

<span data-ttu-id="ff2f2-482">**資料類型：**具有一或多個轉換項目的 JSON blob</span><span class="sxs-lookup"><span data-stu-id="ff2f2-482">**Data type:** JSON blob, with one or more transformation entries</span></span> 

<span data-ttu-id="ff2f2-483">**摘要：**使用此屬性可對來源資料套用常見的轉換，以便為宣告結構描述中指定的宣告產生輸出資料。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-483">**Summary:** Use this property to apply common transformations to source data, to generate the output data for claims specified in the Claims Schema.</span></span>

<span data-ttu-id="ff2f2-484">**識別碼：**使用識別碼元素可在 TransformationID 宣告結構描述項目中參考此轉換項目。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-484">**ID:** Use the ID element to reference this transformation entry in the TransformationID Claims Schema entry.</span></span> <span data-ttu-id="ff2f2-485">對於這項原則內的每個轉換項目，此值都必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-485">This value must be unique for each transformation entry within this policy.</span></span>

<span data-ttu-id="ff2f2-486">**TransformationMethod：**TransformationMethod 元素可識別該執行哪個作業才能為宣告產生資料。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-486">**TransformationMethod:** The TransformationMethod element identifies which operation is performed to generate the data for the claim.</span></span>

<span data-ttu-id="ff2f2-487">根據您所選擇的方法，系統預期會有一組輸入和輸出。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-487">Based on the method chosen, a set of inputs and outputs is expected.</span></span> <span data-ttu-id="ff2f2-488">您可以使用 **InputClaims**、**InputParameters** 和 **OutputClaims** 元素來定義這些輸入和輸出。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-488">These are defined by using the **InputClaims**, **InputParameters** and **OutputClaims** elements.</span></span>

#### <a name="table-4-transformation-methods-and-expected-inputs-and-outputs"></a><span data-ttu-id="ff2f2-489">表 4：轉換方法和預期的輸入和輸出</span><span class="sxs-lookup"><span data-stu-id="ff2f2-489">Table 4: Transformation methods and expected inputs and outputs</span></span>
|<span data-ttu-id="ff2f2-490">TransformationMethod</span><span class="sxs-lookup"><span data-stu-id="ff2f2-490">TransformationMethod</span></span>|<span data-ttu-id="ff2f2-491">預期的輸入</span><span class="sxs-lookup"><span data-stu-id="ff2f2-491">Expected input</span></span>|<span data-ttu-id="ff2f2-492">預期的輸出</span><span class="sxs-lookup"><span data-stu-id="ff2f2-492">Expected output</span></span>|<span data-ttu-id="ff2f2-493">說明</span><span class="sxs-lookup"><span data-stu-id="ff2f2-493">Description</span></span>|
|-----|-----|-----|-----|
|<span data-ttu-id="ff2f2-494">Join</span><span class="sxs-lookup"><span data-stu-id="ff2f2-494">Join</span></span>|<span data-ttu-id="ff2f2-495">string1、string2、分隔符號</span><span class="sxs-lookup"><span data-stu-id="ff2f2-495">string1, string2, separator</span></span>|<span data-ttu-id="ff2f2-496">outputClaim</span><span class="sxs-lookup"><span data-stu-id="ff2f2-496">outputClaim</span></span>|<span data-ttu-id="ff2f2-497">可在輸入字串之間使用分隔符號來聯結這些字串。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-497">Joins input strings by using a separator in between.</span></span> <span data-ttu-id="ff2f2-498">例如：string1:"foo@bar.com" , string2:"sandbox" , separator:"." 會導致 outputClaim:"foo@bar.com.sandbox"</span><span class="sxs-lookup"><span data-stu-id="ff2f2-498">For example: string1:"foo@bar.com" , string2:"sandbox" , separator:"." results in outputClaim:"foo@bar.com.sandbox"</span></span>|
|<span data-ttu-id="ff2f2-499">ExtractMailPrefix</span><span class="sxs-lookup"><span data-stu-id="ff2f2-499">ExtractMailPrefix</span></span>|<span data-ttu-id="ff2f2-500">mail</span><span class="sxs-lookup"><span data-stu-id="ff2f2-500">mail</span></span>|<span data-ttu-id="ff2f2-501">outputClaim</span><span class="sxs-lookup"><span data-stu-id="ff2f2-501">outputClaim</span></span>|<span data-ttu-id="ff2f2-502">擷取電子郵件地址的本機部分。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-502">Extracts the local part of an email address.</span></span> <span data-ttu-id="ff2f2-503">例如：mail:"foo@bar.com" 會導致 outputClaim:"foo"。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-503">For example: mail:"foo@bar.com" results in outputClaim:"foo".</span></span> <span data-ttu-id="ff2f2-504">如果沒有 @ 符號，則原始輸入字串會以現狀傳回。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-504">If no @ sign is present, then the orignal input string is returned as is.</span></span>|

<span data-ttu-id="ff2f2-505">**InputClaims：**使用 InputClaims 元素可從宣告結構描述項目將資料傳遞至轉換。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-505">**InputClaims:** Use an InputClaims element to pass the data from a claim schema entry to a transformation.</span></span> <span data-ttu-id="ff2f2-506">它有兩個屬性：**ClaimTypeReferenceId** 和 **TransformationClaimType**。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-506">It has two attributes: **ClaimTypeReferenceId** and **TransformationClaimType**.</span></span>

- <span data-ttu-id="ff2f2-507">**ClaimTypeReferenceId** 會與宣告結構描述項目的識別碼元素聯結以尋找適當的輸入宣告。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-507">**ClaimTypeReferenceId** is joined with ID element of the claim schema entry to find the appropriate input claim.</span></span> 
- <span data-ttu-id="ff2f2-508">**TransformationClaimType** 則可用來為此輸入指定唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-508">**TransformationClaimType** is used to give a unique name to this input.</span></span> <span data-ttu-id="ff2f2-509">此名稱必須符合轉換方法的其中一個預期輸入。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-509">This name must match one of the expected inputs for the transformation method.</span></span>

<span data-ttu-id="ff2f2-510">**InputParameters：**使用 InputParameters 元素可對轉換傳遞常數值。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-510">**InputParameters:** Use an InputParameters element to pass a constant value to a transformation.</span></span> <span data-ttu-id="ff2f2-511">它有兩個屬性：**值**和**識別碼**。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-511">It has two attributes: **Value** and **ID**.</span></span>

- <span data-ttu-id="ff2f2-512">**值**是要傳遞的實際常數值。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-512">**Value** is the actual constant value to be passed.</span></span>
- <span data-ttu-id="ff2f2-513">**識別碼**則可用來為此輸入指定唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-513">**ID** is used to give a unique name to this input.</span></span> <span data-ttu-id="ff2f2-514">此名稱必須符合轉換方法的其中一個預期輸入。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-514">This name must match one of the expected inputs for the transformation method.</span></span>

<span data-ttu-id="ff2f2-515">**OutputClaims：**使用 OutputClaims 元素可保留轉換所產生的資料，並將資料繫結到宣告結構描述項目。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-515">**OutputClaims:** Use an OutputClaims element to hold the data generated by a transformation, and tie it to a claim schema entry.</span></span> <span data-ttu-id="ff2f2-516">它有兩個屬性：**ClaimTypeReferenceId** 和 **TransformationClaimType**。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-516">It has two attributes: **ClaimTypeReferenceId** and **TransformationClaimType**.</span></span>

- <span data-ttu-id="ff2f2-517">**ClaimTypeReferenceId** 會與宣告結構描述項目的識別碼聯結以尋找適當的輸出宣告。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-517">**ClaimTypeReferenceId** is joined with the ID of the claim schema entry to find the appropriate output claim.</span></span>
- <span data-ttu-id="ff2f2-518">**TransformationClaimType** 則可用來為此輸出指定唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-518">**TransformationClaimType** is used to give a unique name to this output.</span></span> <span data-ttu-id="ff2f2-519">此名稱必須符合轉換方法的其中一個預期輸出。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-519">This name must match one of the expected outputs for the transformation method.</span></span>

### <a name="exceptions-and-restrictions"></a><span data-ttu-id="ff2f2-520">例外狀況和限制</span><span class="sxs-lookup"><span data-stu-id="ff2f2-520">Exceptions and restrictions</span></span>

<span data-ttu-id="ff2f2-521">**SAML NameID 和 UPN：**您用來取得 NameID 和 UPN 值的來源屬性以及所允許的宣告轉換會受到限制。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-521">**SAML NameID and UPN:** The attributes from which you source the NameID and UPN values, and the claims transformations that are permitted, are limited.</span></span>

#### <a name="table-5-attributes-allowed-as-a-data-source-for-saml-nameid"></a><span data-ttu-id="ff2f2-522">表 5：允許作為 SAML NameID 資料來源的屬性</span><span class="sxs-lookup"><span data-stu-id="ff2f2-522">Table 5: Attributes allowed as a data source for SAML NameID</span></span>
|<span data-ttu-id="ff2f2-523">來源</span><span class="sxs-lookup"><span data-stu-id="ff2f2-523">Source</span></span>|<span data-ttu-id="ff2f2-524">ID</span><span class="sxs-lookup"><span data-stu-id="ff2f2-524">ID</span></span>|<span data-ttu-id="ff2f2-525">說明</span><span class="sxs-lookup"><span data-stu-id="ff2f2-525">Description</span></span>|
|-----|-----|-----|
|<span data-ttu-id="ff2f2-526">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-526">User</span></span>|<span data-ttu-id="ff2f2-527">mail</span><span class="sxs-lookup"><span data-stu-id="ff2f2-527">mail</span></span>|<span data-ttu-id="ff2f2-528">電子郵件地址</span><span class="sxs-lookup"><span data-stu-id="ff2f2-528">Email Address</span></span>|
|<span data-ttu-id="ff2f2-529">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-529">User</span></span>|<span data-ttu-id="ff2f2-530">userprincipalname</span><span class="sxs-lookup"><span data-stu-id="ff2f2-530">userprincipalname</span></span>|<span data-ttu-id="ff2f2-531">使用者主體名稱</span><span class="sxs-lookup"><span data-stu-id="ff2f2-531">User Principal Name</span></span>|
|<span data-ttu-id="ff2f2-532">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-532">User</span></span>|<span data-ttu-id="ff2f2-533">onpremisessamaccountname</span><span class="sxs-lookup"><span data-stu-id="ff2f2-533">onpremisessamaccountname</span></span>|<span data-ttu-id="ff2f2-534">內部部署的 Sam 帳戶名稱</span><span class="sxs-lookup"><span data-stu-id="ff2f2-534">On Premises Sam Account Name</span></span>|
|<span data-ttu-id="ff2f2-535">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-535">User</span></span>|<span data-ttu-id="ff2f2-536">employeeid</span><span class="sxs-lookup"><span data-stu-id="ff2f2-536">employeeid</span></span>|<span data-ttu-id="ff2f2-537">員工識別碼</span><span class="sxs-lookup"><span data-stu-id="ff2f2-537">Employee ID</span></span>|
|<span data-ttu-id="ff2f2-538">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-538">User</span></span>|<span data-ttu-id="ff2f2-539">extensionattribute1</span><span class="sxs-lookup"><span data-stu-id="ff2f2-539">extensionattribute1</span></span>|<span data-ttu-id="ff2f2-540">擴充屬性 1</span><span class="sxs-lookup"><span data-stu-id="ff2f2-540">Extension Attribute 1</span></span>|
|<span data-ttu-id="ff2f2-541">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-541">User</span></span>|<span data-ttu-id="ff2f2-542">extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="ff2f2-542">extensionattribute2</span></span>|<span data-ttu-id="ff2f2-543">擴充屬性 2</span><span class="sxs-lookup"><span data-stu-id="ff2f2-543">Extension Attribute 2</span></span>|
|<span data-ttu-id="ff2f2-544">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-544">User</span></span>|<span data-ttu-id="ff2f2-545">extensionattribute3</span><span class="sxs-lookup"><span data-stu-id="ff2f2-545">extensionattribute3</span></span>|<span data-ttu-id="ff2f2-546">擴充屬性 3</span><span class="sxs-lookup"><span data-stu-id="ff2f2-546">Extension Attribute 3</span></span>|
|<span data-ttu-id="ff2f2-547">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-547">User</span></span>|<span data-ttu-id="ff2f2-548">extensionattribute4</span><span class="sxs-lookup"><span data-stu-id="ff2f2-548">extensionattribute4</span></span>|<span data-ttu-id="ff2f2-549">擴充屬性 4</span><span class="sxs-lookup"><span data-stu-id="ff2f2-549">Extension Attribute 4</span></span>|
|<span data-ttu-id="ff2f2-550">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-550">User</span></span>|<span data-ttu-id="ff2f2-551">extensionattribute5</span><span class="sxs-lookup"><span data-stu-id="ff2f2-551">extensionattribute5</span></span>|<span data-ttu-id="ff2f2-552">擴充屬性 5</span><span class="sxs-lookup"><span data-stu-id="ff2f2-552">Extension Attribute 5</span></span>|
|<span data-ttu-id="ff2f2-553">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-553">User</span></span>|<span data-ttu-id="ff2f2-554">extensionattribute6</span><span class="sxs-lookup"><span data-stu-id="ff2f2-554">extensionattribute6</span></span>|<span data-ttu-id="ff2f2-555">擴充屬性 6</span><span class="sxs-lookup"><span data-stu-id="ff2f2-555">Extension Attribute 6</span></span>|
|<span data-ttu-id="ff2f2-556">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-556">User</span></span>|<span data-ttu-id="ff2f2-557">extensionattribute7</span><span class="sxs-lookup"><span data-stu-id="ff2f2-557">extensionattribute7</span></span>|<span data-ttu-id="ff2f2-558">擴充屬性 7</span><span class="sxs-lookup"><span data-stu-id="ff2f2-558">Extension Attribute 7</span></span>|
|<span data-ttu-id="ff2f2-559">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-559">User</span></span>|<span data-ttu-id="ff2f2-560">extensionattribute8</span><span class="sxs-lookup"><span data-stu-id="ff2f2-560">extensionattribute8</span></span>|<span data-ttu-id="ff2f2-561">擴充屬性 8</span><span class="sxs-lookup"><span data-stu-id="ff2f2-561">Extension Attribute 8</span></span>|
|<span data-ttu-id="ff2f2-562">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-562">User</span></span>|<span data-ttu-id="ff2f2-563">extensionattribute9</span><span class="sxs-lookup"><span data-stu-id="ff2f2-563">extensionattribute9</span></span>|<span data-ttu-id="ff2f2-564">擴充屬性 9</span><span class="sxs-lookup"><span data-stu-id="ff2f2-564">Extension Attribute 9</span></span>|
|<span data-ttu-id="ff2f2-565">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-565">User</span></span>|<span data-ttu-id="ff2f2-566">extensionattribute10</span><span class="sxs-lookup"><span data-stu-id="ff2f2-566">extensionattribute10</span></span>|<span data-ttu-id="ff2f2-567">擴充屬性 10</span><span class="sxs-lookup"><span data-stu-id="ff2f2-567">Extension Attribute 10</span></span>|
|<span data-ttu-id="ff2f2-568">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-568">User</span></span>|<span data-ttu-id="ff2f2-569">extensionattribute11</span><span class="sxs-lookup"><span data-stu-id="ff2f2-569">extensionattribute11</span></span>|<span data-ttu-id="ff2f2-570">擴充屬性 11</span><span class="sxs-lookup"><span data-stu-id="ff2f2-570">Extension Attribute 11</span></span>|
|<span data-ttu-id="ff2f2-571">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-571">User</span></span>|<span data-ttu-id="ff2f2-572">extensionattribute12</span><span class="sxs-lookup"><span data-stu-id="ff2f2-572">extensionattribute12</span></span>|<span data-ttu-id="ff2f2-573">擴充屬性 12</span><span class="sxs-lookup"><span data-stu-id="ff2f2-573">Extension Attribute 12</span></span>|
|<span data-ttu-id="ff2f2-574">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-574">User</span></span>|<span data-ttu-id="ff2f2-575">extensionattribute13</span><span class="sxs-lookup"><span data-stu-id="ff2f2-575">extensionattribute13</span></span>|<span data-ttu-id="ff2f2-576">擴充屬性 13</span><span class="sxs-lookup"><span data-stu-id="ff2f2-576">Extension Attribute 13</span></span>|
|<span data-ttu-id="ff2f2-577">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-577">User</span></span>|<span data-ttu-id="ff2f2-578">extensionattribute14</span><span class="sxs-lookup"><span data-stu-id="ff2f2-578">extensionattribute14</span></span>|<span data-ttu-id="ff2f2-579">擴充屬性 14</span><span class="sxs-lookup"><span data-stu-id="ff2f2-579">Extension Attribute 14</span></span>|
|<span data-ttu-id="ff2f2-580">User</span><span class="sxs-lookup"><span data-stu-id="ff2f2-580">User</span></span>|<span data-ttu-id="ff2f2-581">extensionattribute15</span><span class="sxs-lookup"><span data-stu-id="ff2f2-581">extensionattribute15</span></span>|<span data-ttu-id="ff2f2-582">擴充屬性 15</span><span class="sxs-lookup"><span data-stu-id="ff2f2-582">Extension Attribute 15</span></span>|

#### <a name="table-6-transformation-methods-allowed-for-saml-nameid"></a><span data-ttu-id="ff2f2-583">表 6：允許 SAML NameID 使用的轉換方法</span><span class="sxs-lookup"><span data-stu-id="ff2f2-583">Table 6: Transformation methods allowed for SAML NameID</span></span>
|<span data-ttu-id="ff2f2-584">TransformationMethod</span><span class="sxs-lookup"><span data-stu-id="ff2f2-584">TransformationMethod</span></span>|<span data-ttu-id="ff2f2-585">限制</span><span class="sxs-lookup"><span data-stu-id="ff2f2-585">Restrictions</span></span>|
| ----- | ----- |
|<span data-ttu-id="ff2f2-586">ExtractMailPrefix</span><span class="sxs-lookup"><span data-stu-id="ff2f2-586">ExtractMailPrefix</span></span>|<span data-ttu-id="ff2f2-587">None</span><span class="sxs-lookup"><span data-stu-id="ff2f2-587">None</span></span>|
|<span data-ttu-id="ff2f2-588">Join</span><span class="sxs-lookup"><span data-stu-id="ff2f2-588">Join</span></span>|<span data-ttu-id="ff2f2-589">所聯結的尾碼必須是資源租用戶的已驗證網域。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-589">The suffix being joined must be a verified domain of the resource tenant.</span></span>|

### <a name="custom-signing-key"></a><span data-ttu-id="ff2f2-590">自訂簽署金鑰</span><span class="sxs-lookup"><span data-stu-id="ff2f2-590">Custom signing key</span></span>
<span data-ttu-id="ff2f2-591">您必須對服務主體物件指派自訂簽署金鑰，宣告對應原則才會生效。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-591">A custom signing key must be assigned to the service principal object for a claims mapping policy to take effect.</span></span> <span data-ttu-id="ff2f2-592">所有已核發並受到該原則影響的權杖皆會使用此金鑰來簽署。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-592">All tokens issued that have been impacted by the policy are signed with this key.</span></span> <span data-ttu-id="ff2f2-593">您必須將應用程式設定為接受使用此金鑰所簽署的權杖。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-593">Applications must be configured to accept tokens signed with this key.</span></span> <span data-ttu-id="ff2f2-594">這可確保系統確認宣告對應原則的建立者已修改權杖。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-594">This ensures acknowledgment that tokens have been modified by the creator of the claims mapping policy.</span></span> <span data-ttu-id="ff2f2-595">這項確認可防止應用程式使用惡意執行者所建立的宣告對應原則。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-595">This protects applications from claims mapping policies created by malicious actors.</span></span>

### <a name="cross-tenant-scenarios"></a><span data-ttu-id="ff2f2-596">跨租用戶案例</span><span class="sxs-lookup"><span data-stu-id="ff2f2-596">Cross-tenant scenarios</span></span>
<span data-ttu-id="ff2f2-597">宣告對應原則不適用於來賓使用者。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-597">Claims mapping policies do not apply to guest users.</span></span> <span data-ttu-id="ff2f2-598">如果有來賓使用者嘗試使用指派給應用程式服務主體的宣告對應原則來存取應用程式，系統就會核發預設權杖 (原則沒有任何效果)。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-598">If a guest user attempts to access an application with a claims mapping policy assigned to its service principal, the default token is issued (the policy has no effect).</span></span>

## <a name="claims-mapping-policy-assignment"></a><span data-ttu-id="ff2f2-599">宣告對應原則指派</span><span class="sxs-lookup"><span data-stu-id="ff2f2-599">Claims mapping policy assignment</span></span>
<span data-ttu-id="ff2f2-600">宣告對應原則只能指派給服務主體物件。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-600">Claims mapping policies can only be assigned to service principal objects.</span></span>

### <a name="example-claims-mapping-policies"></a><span data-ttu-id="ff2f2-601">宣告對應原則範例</span><span class="sxs-lookup"><span data-stu-id="ff2f2-601">Example claims mapping policies</span></span>

<span data-ttu-id="ff2f2-602">在 Azure AD 中，當您可以為特定的服務主體自訂權杖中所發出的宣告時，許多案例便可能實現。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-602">In Azure AD, many scenarios are possible when you can customize claims emitted in tokens for specific service principals.</span></span> <span data-ttu-id="ff2f2-603">在本節中，我們將逐步解說一些常見案例，以協助您掌握如何使用宣告對應原則類型。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-603">In this section, we walk through a few common scenarios that can help you grasp how to use the claims mapping policy type.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="ff2f2-604">必要條件</span><span class="sxs-lookup"><span data-stu-id="ff2f2-604">Prerequisites</span></span>
<span data-ttu-id="ff2f2-605">在下列範例中，您會為服務主體建立、更新、連結和刪除原則。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-605">In the following examples, you create, update, link, and delete policies for service principals.</span></span> <span data-ttu-id="ff2f2-606">如果您是 Azure AD 的新手，我們建議您先深入了解如何取得 Azure AD 租用戶，然後再利用這些範例繼續進行。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-606">If you are new to Azure AD, we recommend that you learn about how to get an Azure AD tenant before you proceed with these examples.</span></span> 

<span data-ttu-id="ff2f2-607">若要開始使用，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ff2f2-607">To get started, do the following steps:</span></span>


1. <span data-ttu-id="ff2f2-608">下載最新的 [Azure AD PowerShell 模組公開預覽版本](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.127)。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-608">Download the latest [Azure AD PowerShell Module public preview release](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.127).</span></span>
2.  <span data-ttu-id="ff2f2-609">執行 Connect 命令以登入您的 Azure AD 管理帳戶。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-609">Run the Connect command to sign in to your Azure AD admin account.</span></span> <span data-ttu-id="ff2f2-610">您每次啟動新的工作階段時執行此命令。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-610">Run this command each time you start a new session.</span></span>
    
     ``` powershell
    Connect-AzureAD -Confirm
    
    ```
3.  <span data-ttu-id="ff2f2-611">若要查看在組織中建立的所有原則，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-611">To see all policies that have been created in your organization, run the following command.</span></span> <span data-ttu-id="ff2f2-612">建議您在進行完下列案例中的大部分作業之後執行此命令，以確認原則是否如預期般地建立。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-612">We recommend that you run this command after most operations in the following scenarios, to check that your policies are being created as expected.</span></span>
   
    ``` powershell
        Get-AzureADPolicy
    
    ```
#### <a name="example-create-and-assign-a-policy-to-omit-the-basic-claims-from-tokens-issued-to-a-service-principal"></a><span data-ttu-id="ff2f2-613">範例：建立並指派原則，以在核發給服務主體的權杖中省略基本宣告。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-613">Example: Create and assign a policy to omit the basic claims from tokens issued to a service principal.</span></span>
<span data-ttu-id="ff2f2-614">在此範例中，您將會建立原則，以從核發給連結之服務主體的權杖中移除基本宣告集。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-614">In this example, you create a policy that removes the basic claim set from tokens issued to linked service principals.</span></span>


1. <span data-ttu-id="ff2f2-615">建立宣告對應原則。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-615">Create a claims mapping policy.</span></span> <span data-ttu-id="ff2f2-616">這個連結至特定服務主體的原則會從權杖中移除基本宣告。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-616">This policy, linked to specific service principals, removes the basic claim set from tokens.</span></span>
    1. <span data-ttu-id="ff2f2-617">若要建立原則，請執行此命令：</span><span class="sxs-lookup"><span data-stu-id="ff2f2-617">To create the policy, run this command:</span></span> 
    
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"false"}}') -DisplayName "OmitBasicClaims” -Type "ClaimsMappingPolicy"
    ```
    2. <span data-ttu-id="ff2f2-618">若要查看您的新原則並取得原則的 ObjectId，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="ff2f2-618">To see your new policy, and to get the policy ObjectId, run the following command:</span></span>
    
     ``` powershell
    Get-AzureADPolicy
    ```
2.  <span data-ttu-id="ff2f2-619">將原則指派給服務主體。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-619">Assign the policy to your service principal.</span></span> <span data-ttu-id="ff2f2-620">您也需要取得服務主體的 ObjectId。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-620">You also need to get the ObjectId of your service principal.</span></span> 
    1.  <span data-ttu-id="ff2f2-621">若要查看您組織的所有服務主體，您可以查詢 Microsoft Graph。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-621">To see all your organization's service principals, you can query Microsoft Graph.</span></span> <span data-ttu-id="ff2f2-622">或者，在 Azure AD Graph 總管，登入您的 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-622">Or, in Azure AD Graph Explorer, sign in to your Azure AD account.</span></span>
    2.  <span data-ttu-id="ff2f2-623">當您有服務主體的 ObjectId 時，執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="ff2f2-623">When you have the ObjectId of your service principal, run the following command:</span></span>  
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of the ServicePrincipal> -RefObjectId <ObjectId of the Policy>
    ```
#### <a name="example-create-and-assign-a-policy-to-include-the-employeeid-and-tenantcountry-as-claims-in-tokens-issued-to-a-service-principal"></a><span data-ttu-id="ff2f2-624">範例：建立並指派原則，以在核發給服務主體的權杖中納入 EmployeeID 和 TenantCountry 來作為宣告。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-624">Example: Create and assign a policy to include the EmployeeID and TenantCountry as claims in tokens issued to a service principal.</span></span>
<span data-ttu-id="ff2f2-625">在此範例中，您將會建立原則，以在核發給連結之服務主體的權杖中新增 EmployeeID 和 TenantCountry。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-625">In this example, you create a policy that adds the EmployeeID and TenantCountry to tokens issued to linked service principals.</span></span> <span data-ttu-id="ff2f2-626">在 SAML 權杖和 JWT 中，系統會以名稱宣告類型來發出 EmployeeID。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-626">The EmployeeID is emitted as the name claim type in both SAML tokens and JWTs.</span></span> <span data-ttu-id="ff2f2-627">在 SAML 權杖和 JWT 中，系統會以國家/地區宣告類型來發出 TenantCountry。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-627">The TenantCountry is emitted as the country claim type in both SAML tokens and JWTs.</span></span> <span data-ttu-id="ff2f2-628">在此範例中，我們會繼續在權杖中納入基本宣告集。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-628">In this example, we continue to include the basic claims set in the tokens.</span></span>

1. <span data-ttu-id="ff2f2-629">建立宣告對應原則。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-629">Create a claims mapping policy.</span></span> <span data-ttu-id="ff2f2-630">這個連結至特定服務主體的原則會在權杖中新增 EmployeeID 和 TenantCountry 宣告。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-630">This policy, linked to specific service principals, adds the EmployeeID and TenantCountry claims to tokens.</span></span>
    1. <span data-ttu-id="ff2f2-631">若要建立原則，請執行此命令：</span><span class="sxs-lookup"><span data-stu-id="ff2f2-631">To create the policy, run this command:</span></span>  
     
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema": [{"Source":"user","ID":"employeeid","SamlClaimType":"http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name","JwtClaimType":"name"},{"Source":"company","ID":" tenantcountry ","SamlClaimType":" http://schemas.xmlsoap.org/ws/2005/05/identity/claims/country ","JwtClaimType":"country"}]}}') -DisplayName "ExtraClaimsExample” -Type "ClaimsMappingPolicy"
    ```
    
    2. <span data-ttu-id="ff2f2-632">若要查看您的新原則並取得原則的 ObjectId，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="ff2f2-632">To see your new policy, and to get the policy ObjectId, run the following command:</span></span>
     
     ``` powershell  
    Get-AzureADPolicy
    ```
2.  <span data-ttu-id="ff2f2-633">將原則指派給服務主體。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-633">Assign the policy to your service principal.</span></span> <span data-ttu-id="ff2f2-634">您也需要取得服務主體的 ObjectId。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-634">You also need to get the ObjectId of your service principal.</span></span> 
    1.  <span data-ttu-id="ff2f2-635">若要查看您組織的所有服務主體，您可以查詢 Microsoft Graph。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-635">To see all your organization's service principals, you can query Microsoft Graph.</span></span> <span data-ttu-id="ff2f2-636">或者，在 Azure AD Graph 總管，登入您的 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-636">Or, in Azure AD Graph Explorer, sign in to your Azure AD account.</span></span>
    2.  <span data-ttu-id="ff2f2-637">當您有服務主體的 ObjectId 時，執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="ff2f2-637">When you have the ObjectId of your service principal, run the following command:</span></span>  
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of the ServicePrincipal> -RefObjectId <ObjectId of the Policy>
    ```
#### <a name="example-create-and-assign-a-policy-that-uses-a-claims-transformation-in-tokens-issued-to-a-service-principal"></a><span data-ttu-id="ff2f2-638">範例：建立並指派原則，以在核發給服務主體的權杖中使用宣告轉換。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-638">Example: Create and assign a policy that uses a claims transformation in tokens issued to a service principal.</span></span>
<span data-ttu-id="ff2f2-639">在此範例中，您將會建立原則，以對核發給連結之服務主體的 JWT 發出自訂宣告「JoinedData」。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-639">In this example, you create a policy that emits a custom claim “JoinedData” to JWTs issued to linked service principals.</span></span> <span data-ttu-id="ff2f2-640">這個宣告會包含藉由聯結資料 (儲存於使用者物件上的 extensionattribute1 屬性中) 與「.sandbox」所建立的值。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-640">This claim contains a value created by joining the data stored in the extensionattribute1 attribute on the user object with “.sandbox”.</span></span> <span data-ttu-id="ff2f2-641">在此範例中，我們會在權杖中排除基本宣告集。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-641">In this example, we exclude the basic claims set in the tokens.</span></span>


1. <span data-ttu-id="ff2f2-642">建立宣告對應原則。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-642">Create a claims mapping policy.</span></span> <span data-ttu-id="ff2f2-643">這個連結至特定服務主體的原則會在權杖中新增 EmployeeID 和 TenantCountry 宣告。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-643">This policy, linked to specific service principals, adds the EmployeeID and TenantCountry claims to tokens.</span></span>
    1. <span data-ttu-id="ff2f2-644">若要建立原則，請執行此命令：</span><span class="sxs-lookup"><span data-stu-id="ff2f2-644">To create the policy, run this command:</span></span> 
     
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema":[{"Source":"user","ID":"extensionattribute1"},{"Source":"transformation","ID":"DataJoin","TransformationId":"JoinTheData","JwtClaimType":"JoinedData"}],"ClaimsTransformation":[{"ID":"JoinTheData","TransformationMethod":"Join","InputClaims":[{"ClaimTypeReferenceId":"extensionattribute1","TransformationClaimType":"string1"}], "InputParameters": [{"Id":"string2","Value":"sandbox"},{"Id":"separator","Value":"."}],"OutputClaims":[{"ClaimTypeReferenceId":"DataJoin","TransformationClaimType":"outputClaim"}]}]}}') -DisplayName "TransformClaimsExample” -Type "ClaimsMappingPolicy"
    ```
    
    2. <span data-ttu-id="ff2f2-645">若要查看您的新原則並取得原則的 ObjectId，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="ff2f2-645">To see your new policy, and to get the policy ObjectId, run the following command:</span></span> 
     
     ``` powershell
    Get-AzureADPolicy
    ```
2.  <span data-ttu-id="ff2f2-646">將原則指派給服務主體。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-646">Assign the policy to your service principal.</span></span> <span data-ttu-id="ff2f2-647">您也需要取得服務主體的 ObjectId。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-647">You also need to get the ObjectId of your service principal.</span></span> 
    1.  <span data-ttu-id="ff2f2-648">若要查看您組織的所有服務主體，您可以查詢 Microsoft Graph。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-648">To see all your organization's service principals, you can query Microsoft Graph.</span></span> <span data-ttu-id="ff2f2-649">或者，在 Azure AD Graph 總管，登入您的 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ff2f2-649">Or, in Azure AD Graph Explorer, sign in to your Azure AD account.</span></span>
    2.  <span data-ttu-id="ff2f2-650">當您有服務主體的 ObjectId 時，執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="ff2f2-650">When you have the ObjectId of your service principal, run the following command:</span></span> 
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of the ServicePrincipal> -RefObjectId <ObjectId of the Policy>
    ```
