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
ms.openlocfilehash: ff07b9954d5c2ce71ab0ffd0db49fde15f323586
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="claims-mapping-in-azure-active-directory-public-preview"></a><span data-ttu-id="d5701-103">Azure Active Directory 中的宣告對應 (公開預覽)</span><span class="sxs-lookup"><span data-stu-id="d5701-103">Claims mapping in Azure Active Directory (public preview)</span></span>

>[!NOTE]
><span data-ttu-id="d5701-104">這項功能會取代並取代 hello[宣告自訂](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-claims-customization)目前提供透過 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="d5701-104">This feature replaces and supersedes hello [claims customization](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-claims-customization) offered through hello portal today.</span></span> <span data-ttu-id="d5701-105">如果您要自訂使用 hello 入口網站的宣告此外 toohello 圖形/PowerShell 方法本文中詳述 hello 上相同的應用程式、 針對該應用程式將會忽略 hello 入口網站中的 hello 組態所簽發的權杖。</span><span class="sxs-lookup"><span data-stu-id="d5701-105">If you customize claims using hello portal in addition toohello Graph/PowerShell method detailed in this document on hello same application, tokens issued for that application will ignore hello configuration in hello portal.</span></span>
<span data-ttu-id="d5701-106">透過這份文件中詳述的 hello 方法所做的組態將不會反映在 hello 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="d5701-106">Configurations made through hello methods detailed in this document will not be reflected in hello portal.</span></span>

<span data-ttu-id="d5701-107">這項功能會使用其租用戶中特定應用程式的權杖中發出的租用戶系統管理員 」 toocustomize hello 宣告。</span><span class="sxs-lookup"><span data-stu-id="d5701-107">This feature is used by tenant admins toocustomize hello claims emitted in tokens for a specific application in their tenant.</span></span> <span data-ttu-id="d5701-108">您可以使用宣告對應原則來進行下列作業：</span><span class="sxs-lookup"><span data-stu-id="d5701-108">You can use claims mapping policies to:</span></span>

- <span data-ttu-id="d5701-109">選取要在權杖中包含哪些宣告。</span><span class="sxs-lookup"><span data-stu-id="d5701-109">Select which claims are included in tokens.</span></span>
- <span data-ttu-id="d5701-110">建立尚未存在的宣告類型。</span><span class="sxs-lookup"><span data-stu-id="d5701-110">Create claim types that do not already exist.</span></span>
- <span data-ttu-id="d5701-111">選擇或變更 hello 發出特定的宣告中的資料來源。</span><span class="sxs-lookup"><span data-stu-id="d5701-111">Choose or change hello source of data emitted in specific claims.</span></span>

>[!NOTE]
><span data-ttu-id="d5701-112">這項功能目前為公開預覽版。</span><span class="sxs-lookup"><span data-stu-id="d5701-112">This capability currently is in public preview.</span></span> <span data-ttu-id="d5701-113">準備 toorevert 或移除任何變更。</span><span class="sxs-lookup"><span data-stu-id="d5701-113">Be prepared toorevert or remove any changes.</span></span> <span data-ttu-id="d5701-114">公開預覽期間的任何 Azure Active Directory (Azure AD) 訂用帳戶中使用 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="d5701-114">hello feature is available in any Azure Active Directory (Azure AD) subscription during public preview.</span></span> <span data-ttu-id="d5701-115">不過，hello 功能正式推出時，某些層面 hello 功能可能需要 Azure Active Directory premium 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d5701-115">However, when hello feature becomes generally available, some aspects of hello feature might require an Azure Active Directory premium subscription.</span></span>

## <a name="claims-mapping-policy-type"></a><span data-ttu-id="d5701-116">宣告對應原則類型</span><span class="sxs-lookup"><span data-stu-id="d5701-116">Claims mapping policy type</span></span>
<span data-ttu-id="d5701-117">在 Azure AD 中，**原則**物件代表個別應用程式或組織中的所有應用程式上強制執行的一組規則。</span><span class="sxs-lookup"><span data-stu-id="d5701-117">In Azure AD, a **Policy** object represents a set of rules enforced on individual applications, or on all applications in an organization.</span></span> <span data-ttu-id="d5701-118">每種原則有唯一的結構，以一組相關的屬性，然後套用 tooobjects toowhich 會指派給他們。</span><span class="sxs-lookup"><span data-stu-id="d5701-118">Each type of policy has a unique structure, with a set of properties that are then applied tooobjects toowhich they are assigned.</span></span>

<span data-ttu-id="d5701-119">宣告對應原則是一種**原則**修改 hello 的物件宣告在特定應用程式簽發的權杖中發出。</span><span class="sxs-lookup"><span data-stu-id="d5701-119">A claims mapping policy is a type of **Policy** object that modifies hello claims emitted in tokens issued for specific applications.</span></span>

## <a name="claim-sets"></a><span data-ttu-id="d5701-120">宣告集</span><span class="sxs-lookup"><span data-stu-id="d5701-120">Claim sets</span></span>
<span data-ttu-id="d5701-121">某些宣告集會定義其在權杖中的使用方式和時機。</span><span class="sxs-lookup"><span data-stu-id="d5701-121">There are certain sets of claims that define how and when they are used in tokens.</span></span>

### <a name="core-claim-set"></a><span data-ttu-id="d5701-122">核心宣告集</span><span class="sxs-lookup"><span data-stu-id="d5701-122">Core claim set</span></span>
<span data-ttu-id="d5701-123">所宣告的宣告 hello 核心組會在每個權杖，不論原則。</span><span class="sxs-lookup"><span data-stu-id="d5701-123">Claims in hello core claim set are present in every token, regardless of policy.</span></span> <span data-ttu-id="d5701-124">系統會將這些宣告視為受限制宣告，您無法加以修改。</span><span class="sxs-lookup"><span data-stu-id="d5701-124">These claims are also considered restricted, and cannot be modified.</span></span>

### <a name="basic-claim-set"></a><span data-ttu-id="d5701-125">基本宣告集</span><span class="sxs-lookup"><span data-stu-id="d5701-125">Basic claim set</span></span>
<span data-ttu-id="d5701-126">hello 基本的宣告集包含 hello 宣告，所發出的權杖 （在加法 toohello 核心宣告集） 的預設值。</span><span class="sxs-lookup"><span data-stu-id="d5701-126">hello basic claim set includes hello claims that are emitted by default for tokens (in addition toohello core claim set).</span></span> <span data-ttu-id="d5701-127">可省略這些宣告，或修改使用 hello 宣告對應原則。</span><span class="sxs-lookup"><span data-stu-id="d5701-127">These claims can be omitted or modified by using hello claims mapping policies.</span></span>

### <a name="restricted-claim-set"></a><span data-ttu-id="d5701-128">受限制的宣告集</span><span class="sxs-lookup"><span data-stu-id="d5701-128">Restricted claim set</span></span>
<span data-ttu-id="d5701-129">無法使用原則來修改的受限制宣告。</span><span class="sxs-lookup"><span data-stu-id="d5701-129">Restricted claims cannot be modified by using policy.</span></span> <span data-ttu-id="d5701-130">無法變更 hello 資料來源，並產生這些宣告時，會套用任何轉換。</span><span class="sxs-lookup"><span data-stu-id="d5701-130">hello data source cannot be changed, and no transformation is applied when generating these claims.</span></span>

#### <a name="table-1-json-web-token-jwt-restricted-claim-set"></a><span data-ttu-id="d5701-131">表 1：JSON Web 權杖 (JWT) 的受限制宣告集</span><span class="sxs-lookup"><span data-stu-id="d5701-131">Table 1: JSON Web Token (JWT) restricted claim set</span></span>
|<span data-ttu-id="d5701-132">宣告類型 (名稱)</span><span class="sxs-lookup"><span data-stu-id="d5701-132">Claim type (name)</span></span>|
| ----- |
|<span data-ttu-id="d5701-133">_claim_names</span><span class="sxs-lookup"><span data-stu-id="d5701-133">_claim_names</span></span>|
|<span data-ttu-id="d5701-134">_claim_sources</span><span class="sxs-lookup"><span data-stu-id="d5701-134">_claim_sources</span></span>|
|<span data-ttu-id="d5701-135">access_token</span><span class="sxs-lookup"><span data-stu-id="d5701-135">access_token</span></span>|
|<span data-ttu-id="d5701-136">account_type</span><span class="sxs-lookup"><span data-stu-id="d5701-136">account_type</span></span>|
|<span data-ttu-id="d5701-137">acr</span><span class="sxs-lookup"><span data-stu-id="d5701-137">acr</span></span>|
|<span data-ttu-id="d5701-138">actor</span><span class="sxs-lookup"><span data-stu-id="d5701-138">actor</span></span>|
|<span data-ttu-id="d5701-139">actortoken</span><span class="sxs-lookup"><span data-stu-id="d5701-139">actortoken</span></span>|
|<span data-ttu-id="d5701-140">aio</span><span class="sxs-lookup"><span data-stu-id="d5701-140">aio</span></span>|
|<span data-ttu-id="d5701-141">altsecid</span><span class="sxs-lookup"><span data-stu-id="d5701-141">altsecid</span></span>|
|<span data-ttu-id="d5701-142">amr</span><span class="sxs-lookup"><span data-stu-id="d5701-142">amr</span></span>|
|<span data-ttu-id="d5701-143">app_chain</span><span class="sxs-lookup"><span data-stu-id="d5701-143">app_chain</span></span>|
|<span data-ttu-id="d5701-144">app_displayname</span><span class="sxs-lookup"><span data-stu-id="d5701-144">app_displayname</span></span>|
|<span data-ttu-id="d5701-145">app_res</span><span class="sxs-lookup"><span data-stu-id="d5701-145">app_res</span></span>|
|<span data-ttu-id="d5701-146">appctx</span><span class="sxs-lookup"><span data-stu-id="d5701-146">appctx</span></span>|
|<span data-ttu-id="d5701-147">appctxsender</span><span class="sxs-lookup"><span data-stu-id="d5701-147">appctxsender</span></span>|
|<span data-ttu-id="d5701-148">appid</span><span class="sxs-lookup"><span data-stu-id="d5701-148">appid</span></span>|
|<span data-ttu-id="d5701-149">appidacr</span><span class="sxs-lookup"><span data-stu-id="d5701-149">appidacr</span></span>|
|<span data-ttu-id="d5701-150">assertion</span><span class="sxs-lookup"><span data-stu-id="d5701-150">assertion</span></span>|
|<span data-ttu-id="d5701-151">at_hash</span><span class="sxs-lookup"><span data-stu-id="d5701-151">at_hash</span></span>|
|<span data-ttu-id="d5701-152">aud</span><span class="sxs-lookup"><span data-stu-id="d5701-152">aud</span></span>|
|<span data-ttu-id="d5701-153">auth_data</span><span class="sxs-lookup"><span data-stu-id="d5701-153">auth_data</span></span>|
|<span data-ttu-id="d5701-154">auth_time</span><span class="sxs-lookup"><span data-stu-id="d5701-154">auth_time</span></span>|
|<span data-ttu-id="d5701-155">authorization_code</span><span class="sxs-lookup"><span data-stu-id="d5701-155">authorization_code</span></span>|
|<span data-ttu-id="d5701-156">azp</span><span class="sxs-lookup"><span data-stu-id="d5701-156">azp</span></span>|
|<span data-ttu-id="d5701-157">azpacr</span><span class="sxs-lookup"><span data-stu-id="d5701-157">azpacr</span></span>|
|<span data-ttu-id="d5701-158">c_hash</span><span class="sxs-lookup"><span data-stu-id="d5701-158">c_hash</span></span>|
|<span data-ttu-id="d5701-159">ca_enf</span><span class="sxs-lookup"><span data-stu-id="d5701-159">ca_enf</span></span>|
|<span data-ttu-id="d5701-160">副本</span><span class="sxs-lookup"><span data-stu-id="d5701-160">cc</span></span>|
|<span data-ttu-id="d5701-161">cert_token_use</span><span class="sxs-lookup"><span data-stu-id="d5701-161">cert_token_use</span></span>|
|<span data-ttu-id="d5701-162">client_id</span><span class="sxs-lookup"><span data-stu-id="d5701-162">client_id</span></span>|
|<span data-ttu-id="d5701-163">cloud_graph_host_name</span><span class="sxs-lookup"><span data-stu-id="d5701-163">cloud_graph_host_name</span></span>|
|<span data-ttu-id="d5701-164">cloud_instance_name</span><span class="sxs-lookup"><span data-stu-id="d5701-164">cloud_instance_name</span></span>|
|<span data-ttu-id="d5701-165">cnf</span><span class="sxs-lookup"><span data-stu-id="d5701-165">cnf</span></span>|
|<span data-ttu-id="d5701-166">code</span><span class="sxs-lookup"><span data-stu-id="d5701-166">code</span></span>|
|<span data-ttu-id="d5701-167">controls</span><span class="sxs-lookup"><span data-stu-id="d5701-167">controls</span></span>|
|<span data-ttu-id="d5701-168">credential_keys</span><span class="sxs-lookup"><span data-stu-id="d5701-168">credential_keys</span></span>|
|<span data-ttu-id="d5701-169">csr</span><span class="sxs-lookup"><span data-stu-id="d5701-169">csr</span></span>|
|<span data-ttu-id="d5701-170">csr_type</span><span class="sxs-lookup"><span data-stu-id="d5701-170">csr_type</span></span>|
|<span data-ttu-id="d5701-171">deviceid</span><span class="sxs-lookup"><span data-stu-id="d5701-171">deviceid</span></span>|
|<span data-ttu-id="d5701-172">dns_names</span><span class="sxs-lookup"><span data-stu-id="d5701-172">dns_names</span></span>|
|<span data-ttu-id="d5701-173">domain_dns_name</span><span class="sxs-lookup"><span data-stu-id="d5701-173">domain_dns_name</span></span>|
|<span data-ttu-id="d5701-174">domain_netbios_name</span><span class="sxs-lookup"><span data-stu-id="d5701-174">domain_netbios_name</span></span>|
|<span data-ttu-id="d5701-175">e_exp</span><span class="sxs-lookup"><span data-stu-id="d5701-175">e_exp</span></span>|
|<span data-ttu-id="d5701-176">電子郵件</span><span class="sxs-lookup"><span data-stu-id="d5701-176">email</span></span>|
|<span data-ttu-id="d5701-177">endpoint</span><span class="sxs-lookup"><span data-stu-id="d5701-177">endpoint</span></span>|
|<span data-ttu-id="d5701-178">enfpolids</span><span class="sxs-lookup"><span data-stu-id="d5701-178">enfpolids</span></span>|
|<span data-ttu-id="d5701-179">exp</span><span class="sxs-lookup"><span data-stu-id="d5701-179">exp</span></span>|
|<span data-ttu-id="d5701-180">expires_on</span><span class="sxs-lookup"><span data-stu-id="d5701-180">expires_on</span></span>|
|<span data-ttu-id="d5701-181">grant_type</span><span class="sxs-lookup"><span data-stu-id="d5701-181">grant_type</span></span>|
|<span data-ttu-id="d5701-182">graph</span><span class="sxs-lookup"><span data-stu-id="d5701-182">graph</span></span>|
|<span data-ttu-id="d5701-183">group_sids</span><span class="sxs-lookup"><span data-stu-id="d5701-183">group_sids</span></span>|
|<span data-ttu-id="d5701-184">groups</span><span class="sxs-lookup"><span data-stu-id="d5701-184">groups</span></span>|
|<span data-ttu-id="d5701-185">hasgroups</span><span class="sxs-lookup"><span data-stu-id="d5701-185">hasgroups</span></span>|
|<span data-ttu-id="d5701-186">hash_alg</span><span class="sxs-lookup"><span data-stu-id="d5701-186">hash_alg</span></span>|
|<span data-ttu-id="d5701-187">home_oid</span><span class="sxs-lookup"><span data-stu-id="d5701-187">home_oid</span></span>|
|<span data-ttu-id="d5701-188">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant</span><span class="sxs-lookup"><span data-stu-id="d5701-188">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant</span></span>|
|<span data-ttu-id="d5701-189">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod</span><span class="sxs-lookup"><span data-stu-id="d5701-189">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod</span></span>|
|<span data-ttu-id="d5701-190">http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration</span><span class="sxs-lookup"><span data-stu-id="d5701-190">http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration</span></span>|
|<span data-ttu-id="d5701-191">http://schemas.microsoft.com/ws/2008/06/identity/claims/expired</span><span class="sxs-lookup"><span data-stu-id="d5701-191">http://schemas.microsoft.com/ws/2008/06/identity/claims/expired</span></span>|
|<span data-ttu-id="d5701-192">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span><span class="sxs-lookup"><span data-stu-id="d5701-192">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span></span>|
|<span data-ttu-id="d5701-193">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name</span><span class="sxs-lookup"><span data-stu-id="d5701-193">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name</span></span>|
|<span data-ttu-id="d5701-194">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier</span><span class="sxs-lookup"><span data-stu-id="d5701-194">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier</span></span>|
|<span data-ttu-id="d5701-195">iat</span><span class="sxs-lookup"><span data-stu-id="d5701-195">iat</span></span>|
|<span data-ttu-id="d5701-196">identityprovider</span><span class="sxs-lookup"><span data-stu-id="d5701-196">identityprovider</span></span>|
|<span data-ttu-id="d5701-197">idp</span><span class="sxs-lookup"><span data-stu-id="d5701-197">idp</span></span>|
|<span data-ttu-id="d5701-198">in_corp</span><span class="sxs-lookup"><span data-stu-id="d5701-198">in_corp</span></span>|
|<span data-ttu-id="d5701-199">instance</span><span class="sxs-lookup"><span data-stu-id="d5701-199">instance</span></span>|
|<span data-ttu-id="d5701-200">ipaddr</span><span class="sxs-lookup"><span data-stu-id="d5701-200">ipaddr</span></span>|
|<span data-ttu-id="d5701-201">isbrowserhostedapp</span><span class="sxs-lookup"><span data-stu-id="d5701-201">isbrowserhostedapp</span></span>|
|<span data-ttu-id="d5701-202">iss</span><span class="sxs-lookup"><span data-stu-id="d5701-202">iss</span></span>|
|<span data-ttu-id="d5701-203">jwk</span><span class="sxs-lookup"><span data-stu-id="d5701-203">jwk</span></span>|
|<span data-ttu-id="d5701-204">key_id</span><span class="sxs-lookup"><span data-stu-id="d5701-204">key_id</span></span>|
|<span data-ttu-id="d5701-205">key_type</span><span class="sxs-lookup"><span data-stu-id="d5701-205">key_type</span></span>|
|<span data-ttu-id="d5701-206">mam_compliance_url</span><span class="sxs-lookup"><span data-stu-id="d5701-206">mam_compliance_url</span></span>|
|<span data-ttu-id="d5701-207">mam_enrollment_url</span><span class="sxs-lookup"><span data-stu-id="d5701-207">mam_enrollment_url</span></span>|
|<span data-ttu-id="d5701-208">mam_terms_of_use_url</span><span class="sxs-lookup"><span data-stu-id="d5701-208">mam_terms_of_use_url</span></span>|
|<span data-ttu-id="d5701-209">mdm_compliance_url</span><span class="sxs-lookup"><span data-stu-id="d5701-209">mdm_compliance_url</span></span>|
|<span data-ttu-id="d5701-210">mdm_enrollment_url</span><span class="sxs-lookup"><span data-stu-id="d5701-210">mdm_enrollment_url</span></span>|
|<span data-ttu-id="d5701-211">mdm_terms_of_use_url</span><span class="sxs-lookup"><span data-stu-id="d5701-211">mdm_terms_of_use_url</span></span>|
|<span data-ttu-id="d5701-212">nameid</span><span class="sxs-lookup"><span data-stu-id="d5701-212">nameid</span></span>|
|<span data-ttu-id="d5701-213">nbf</span><span class="sxs-lookup"><span data-stu-id="d5701-213">nbf</span></span>|
|<span data-ttu-id="d5701-214">netbios_name</span><span class="sxs-lookup"><span data-stu-id="d5701-214">netbios_name</span></span>|
|<span data-ttu-id="d5701-215">nonce</span><span class="sxs-lookup"><span data-stu-id="d5701-215">nonce</span></span>|
|<span data-ttu-id="d5701-216">oid</span><span class="sxs-lookup"><span data-stu-id="d5701-216">oid</span></span>|
|<span data-ttu-id="d5701-217">on_prem_id</span><span class="sxs-lookup"><span data-stu-id="d5701-217">on_prem_id</span></span>|
|<span data-ttu-id="d5701-218">onprem_sam_account_name</span><span class="sxs-lookup"><span data-stu-id="d5701-218">onprem_sam_account_name</span></span>|
|<span data-ttu-id="d5701-219">onprem_sid</span><span class="sxs-lookup"><span data-stu-id="d5701-219">onprem_sid</span></span>|
|<span data-ttu-id="d5701-220">openid2_id</span><span class="sxs-lookup"><span data-stu-id="d5701-220">openid2_id</span></span>|
|<span data-ttu-id="d5701-221">password</span><span class="sxs-lookup"><span data-stu-id="d5701-221">password</span></span>|
|<span data-ttu-id="d5701-222">platf</span><span class="sxs-lookup"><span data-stu-id="d5701-222">platf</span></span>|
|<span data-ttu-id="d5701-223">polids</span><span class="sxs-lookup"><span data-stu-id="d5701-223">polids</span></span>|
|<span data-ttu-id="d5701-224">pop_jwk</span><span class="sxs-lookup"><span data-stu-id="d5701-224">pop_jwk</span></span>|
|<span data-ttu-id="d5701-225">preferred_username</span><span class="sxs-lookup"><span data-stu-id="d5701-225">preferred_username</span></span>|
|<span data-ttu-id="d5701-226">previous_refresh_token</span><span class="sxs-lookup"><span data-stu-id="d5701-226">previous_refresh_token</span></span>|
|<span data-ttu-id="d5701-227">primary_sid</span><span class="sxs-lookup"><span data-stu-id="d5701-227">primary_sid</span></span>|
|<span data-ttu-id="d5701-228">puid</span><span class="sxs-lookup"><span data-stu-id="d5701-228">puid</span></span>|
|<span data-ttu-id="d5701-229">pwd_exp</span><span class="sxs-lookup"><span data-stu-id="d5701-229">pwd_exp</span></span>|
|<span data-ttu-id="d5701-230">pwd_url</span><span class="sxs-lookup"><span data-stu-id="d5701-230">pwd_url</span></span>|
|<span data-ttu-id="d5701-231">redirect_uri</span><span class="sxs-lookup"><span data-stu-id="d5701-231">redirect_uri</span></span>|
|<span data-ttu-id="d5701-232">refresh_token</span><span class="sxs-lookup"><span data-stu-id="d5701-232">refresh_token</span></span>|
|<span data-ttu-id="d5701-233">refreshtoken</span><span class="sxs-lookup"><span data-stu-id="d5701-233">refreshtoken</span></span>|
|<span data-ttu-id="d5701-234">request_nonce</span><span class="sxs-lookup"><span data-stu-id="d5701-234">request_nonce</span></span>|
|<span data-ttu-id="d5701-235">資源</span><span class="sxs-lookup"><span data-stu-id="d5701-235">resource</span></span>|
|<span data-ttu-id="d5701-236">角色</span><span class="sxs-lookup"><span data-stu-id="d5701-236">role</span></span>|
|<span data-ttu-id="d5701-237">角色</span><span class="sxs-lookup"><span data-stu-id="d5701-237">roles</span></span>|
|<span data-ttu-id="d5701-238">scope</span><span class="sxs-lookup"><span data-stu-id="d5701-238">scope</span></span>|
|<span data-ttu-id="d5701-239">scp</span><span class="sxs-lookup"><span data-stu-id="d5701-239">scp</span></span>|
|<span data-ttu-id="d5701-240">sid</span><span class="sxs-lookup"><span data-stu-id="d5701-240">sid</span></span>|
|<span data-ttu-id="d5701-241">signature</span><span class="sxs-lookup"><span data-stu-id="d5701-241">signature</span></span>|
|<span data-ttu-id="d5701-242">signin_state</span><span class="sxs-lookup"><span data-stu-id="d5701-242">signin_state</span></span>|
|<span data-ttu-id="d5701-243">src1</span><span class="sxs-lookup"><span data-stu-id="d5701-243">src1</span></span>|
|<span data-ttu-id="d5701-244">src2</span><span class="sxs-lookup"><span data-stu-id="d5701-244">src2</span></span>|
|<span data-ttu-id="d5701-245">sub</span><span class="sxs-lookup"><span data-stu-id="d5701-245">sub</span></span>|
|<span data-ttu-id="d5701-246">tbid</span><span class="sxs-lookup"><span data-stu-id="d5701-246">tbid</span></span>|
|<span data-ttu-id="d5701-247">tenant_display_name</span><span class="sxs-lookup"><span data-stu-id="d5701-247">tenant_display_name</span></span>|
|<span data-ttu-id="d5701-248">tenant_region_scope</span><span class="sxs-lookup"><span data-stu-id="d5701-248">tenant_region_scope</span></span>|
|<span data-ttu-id="d5701-249">thumbnail_photo</span><span class="sxs-lookup"><span data-stu-id="d5701-249">thumbnail_photo</span></span>|
|<span data-ttu-id="d5701-250">tid</span><span class="sxs-lookup"><span data-stu-id="d5701-250">tid</span></span>|
|<span data-ttu-id="d5701-251">tokenAutologonEnabled</span><span class="sxs-lookup"><span data-stu-id="d5701-251">tokenAutologonEnabled</span></span>|
|<span data-ttu-id="d5701-252">trustedfordelegation</span><span class="sxs-lookup"><span data-stu-id="d5701-252">trustedfordelegation</span></span>|
|<span data-ttu-id="d5701-253">unique_name</span><span class="sxs-lookup"><span data-stu-id="d5701-253">unique_name</span></span>|
|<span data-ttu-id="d5701-254">upn</span><span class="sxs-lookup"><span data-stu-id="d5701-254">upn</span></span>|
|<span data-ttu-id="d5701-255">user_setting_sync_url</span><span class="sxs-lookup"><span data-stu-id="d5701-255">user_setting_sync_url</span></span>|
|<span data-ttu-id="d5701-256">username</span><span class="sxs-lookup"><span data-stu-id="d5701-256">username</span></span>|
|<span data-ttu-id="d5701-257">uti</span><span class="sxs-lookup"><span data-stu-id="d5701-257">uti</span></span>|
|<span data-ttu-id="d5701-258">ver</span><span class="sxs-lookup"><span data-stu-id="d5701-258">ver</span></span>|
|<span data-ttu-id="d5701-259">verified_primary_email</span><span class="sxs-lookup"><span data-stu-id="d5701-259">verified_primary_email</span></span>|
|<span data-ttu-id="d5701-260">verified_secondary_email</span><span class="sxs-lookup"><span data-stu-id="d5701-260">verified_secondary_email</span></span>|
|<span data-ttu-id="d5701-261">wids</span><span class="sxs-lookup"><span data-stu-id="d5701-261">wids</span></span>|
|<span data-ttu-id="d5701-262">win_ver</span><span class="sxs-lookup"><span data-stu-id="d5701-262">win_ver</span></span>|

#### <a name="table-2-security-assertion-markup-language-saml-restricted-claim-set"></a><span data-ttu-id="d5701-263">表 2：安全性聲明標記語言 (SAML) 的受限制宣告集</span><span class="sxs-lookup"><span data-stu-id="d5701-263">Table 2: Security Assertion Markup Language (SAML) restricted claim set</span></span>
|<span data-ttu-id="d5701-264">宣告類型 (URI)</span><span class="sxs-lookup"><span data-stu-id="d5701-264">Claim type (URI)</span></span>|
| ----- |
|<span data-ttu-id="d5701-265">http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration</span><span class="sxs-lookup"><span data-stu-id="d5701-265">http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration</span></span>|
|<span data-ttu-id="d5701-266">http://schemas.microsoft.com/ws/2008/06/identity/claims/expired</span><span class="sxs-lookup"><span data-stu-id="d5701-266">http://schemas.microsoft.com/ws/2008/06/identity/claims/expired</span></span>|
|<span data-ttu-id="d5701-267">http://schemas.microsoft.com/identity/claims/accesstoken</span><span class="sxs-lookup"><span data-stu-id="d5701-267">http://schemas.microsoft.com/identity/claims/accesstoken</span></span>|
|<span data-ttu-id="d5701-268">http://schemas.microsoft.com/identity/claims/openid2_id</span><span class="sxs-lookup"><span data-stu-id="d5701-268">http://schemas.microsoft.com/identity/claims/openid2_id</span></span>|
|<span data-ttu-id="d5701-269">http://schemas.microsoft.com/identity/claims/identityprovider</span><span class="sxs-lookup"><span data-stu-id="d5701-269">http://schemas.microsoft.com/identity/claims/identityprovider</span></span>|
|<span data-ttu-id="d5701-270">http://schemas.microsoft.com/identity/claims/objectidentifier</span><span class="sxs-lookup"><span data-stu-id="d5701-270">http://schemas.microsoft.com/identity/claims/objectidentifier</span></span>|
|<span data-ttu-id="d5701-271">http://schemas.microsoft.com/identity/claims/puid</span><span class="sxs-lookup"><span data-stu-id="d5701-271">http://schemas.microsoft.com/identity/claims/puid</span></span>|
|<span data-ttu-id="d5701-272">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier[MR1]</span><span class="sxs-lookup"><span data-stu-id="d5701-272">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier[MR1]</span></span> |
|<span data-ttu-id="d5701-273">http://schemas.microsoft.com/identity/claims/tenantid</span><span class="sxs-lookup"><span data-stu-id="d5701-273">http://schemas.microsoft.com/identity/claims/tenantid</span></span>|
|<span data-ttu-id="d5701-274">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant</span><span class="sxs-lookup"><span data-stu-id="d5701-274">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant</span></span>|
|<span data-ttu-id="d5701-275">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod</span><span class="sxs-lookup"><span data-stu-id="d5701-275">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod</span></span>|
|<span data-ttu-id="d5701-276">http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider</span><span class="sxs-lookup"><span data-stu-id="d5701-276">http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider</span></span>|
|<span data-ttu-id="d5701-277">http://schemas.microsoft.com/ws/2008/06/identity/claims/groups</span><span class="sxs-lookup"><span data-stu-id="d5701-277">http://schemas.microsoft.com/ws/2008/06/identity/claims/groups</span></span>|
|<span data-ttu-id="d5701-278">http://schemas.microsoft.com/claims/groups.link</span><span class="sxs-lookup"><span data-stu-id="d5701-278">http://schemas.microsoft.com/claims/groups.link</span></span>|
|<span data-ttu-id="d5701-279">http://schemas.microsoft.com/ws/2008/06/identity/claims/role</span><span class="sxs-lookup"><span data-stu-id="d5701-279">http://schemas.microsoft.com/ws/2008/06/identity/claims/role</span></span>|
|<span data-ttu-id="d5701-280">http://schemas.microsoft.com/ws/2008/06/identity/claims/wids</span><span class="sxs-lookup"><span data-stu-id="d5701-280">http://schemas.microsoft.com/ws/2008/06/identity/claims/wids</span></span>|
|<span data-ttu-id="d5701-281">http://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant</span><span class="sxs-lookup"><span data-stu-id="d5701-281">http://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant</span></span>|
|<span data-ttu-id="d5701-282">http://schemas.microsoft.com/2014/02/devicecontext/claims/isknown</span><span class="sxs-lookup"><span data-stu-id="d5701-282">http://schemas.microsoft.com/2014/02/devicecontext/claims/isknown</span></span>|
|<span data-ttu-id="d5701-283">http://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged</span><span class="sxs-lookup"><span data-stu-id="d5701-283">http://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged</span></span>|
|<span data-ttu-id="d5701-284">http://schemas.microsoft.com/2014/03/psso</span><span class="sxs-lookup"><span data-stu-id="d5701-284">http://schemas.microsoft.com/2014/03/psso</span></span>|
|<span data-ttu-id="d5701-285">http://schemas.microsoft.com/claims/authnmethodsreferences</span><span class="sxs-lookup"><span data-stu-id="d5701-285">http://schemas.microsoft.com/claims/authnmethodsreferences</span></span>|
|<span data-ttu-id="d5701-286">http://schemas.xmlsoap.org/ws/2009/09/identity/claims/actor</span><span class="sxs-lookup"><span data-stu-id="d5701-286">http://schemas.xmlsoap.org/ws/2009/09/identity/claims/actor</span></span>|
|<span data-ttu-id="d5701-287">http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername</span><span class="sxs-lookup"><span data-stu-id="d5701-287">http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername</span></span>|
|<span data-ttu-id="d5701-288">http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey</span><span class="sxs-lookup"><span data-stu-id="d5701-288">http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey</span></span>|
|<span data-ttu-id="d5701-289">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname</span><span class="sxs-lookup"><span data-stu-id="d5701-289">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname</span></span>|
|<span data-ttu-id="d5701-290">http://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid</span><span class="sxs-lookup"><span data-stu-id="d5701-290">http://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid</span></span>|
|<span data-ttu-id="d5701-291">http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid</span><span class="sxs-lookup"><span data-stu-id="d5701-291">http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid</span></span>|
|<span data-ttu-id="d5701-292">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authorizationdecision</span><span class="sxs-lookup"><span data-stu-id="d5701-292">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authorizationdecision</span></span>|
|<span data-ttu-id="d5701-293">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authentication</span><span class="sxs-lookup"><span data-stu-id="d5701-293">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authentication</span></span>|
|<span data-ttu-id="d5701-294">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/sid</span><span class="sxs-lookup"><span data-stu-id="d5701-294">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/sid</span></span>|
|<span data-ttu-id="d5701-295">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarygroupsid</span><span class="sxs-lookup"><span data-stu-id="d5701-295">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarygroupsid</span></span>|
|<span data-ttu-id="d5701-296">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarysid</span><span class="sxs-lookup"><span data-stu-id="d5701-296">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarysid</span></span>|
|<span data-ttu-id="d5701-297">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid</span><span class="sxs-lookup"><span data-stu-id="d5701-297">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid</span></span>|
|<span data-ttu-id="d5701-298">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlywindowsdevicegroup</span><span class="sxs-lookup"><span data-stu-id="d5701-298">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlywindowsdevicegroup</span></span>|
|<span data-ttu-id="d5701-299">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdeviceclaim</span><span class="sxs-lookup"><span data-stu-id="d5701-299">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdeviceclaim</span></span>|
|<span data-ttu-id="d5701-300">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup</span><span class="sxs-lookup"><span data-stu-id="d5701-300">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup</span></span>|
|<span data-ttu-id="d5701-301">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsfqbnversion</span><span class="sxs-lookup"><span data-stu-id="d5701-301">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsfqbnversion</span></span>|
|<span data-ttu-id="d5701-302">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowssubauthority</span><span class="sxs-lookup"><span data-stu-id="d5701-302">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowssubauthority</span></span>|
|<span data-ttu-id="d5701-303">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsuserclaim</span><span class="sxs-lookup"><span data-stu-id="d5701-303">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsuserclaim</span></span>|
|<span data-ttu-id="d5701-304">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/x500distinguishedname</span><span class="sxs-lookup"><span data-stu-id="d5701-304">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/x500distinguishedname</span></span>|
|<span data-ttu-id="d5701-305">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn</span><span class="sxs-lookup"><span data-stu-id="d5701-305">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn</span></span>|
|<span data-ttu-id="d5701-306">http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid</span><span class="sxs-lookup"><span data-stu-id="d5701-306">http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid</span></span>|
|<span data-ttu-id="d5701-307">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn</span><span class="sxs-lookup"><span data-stu-id="d5701-307">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn</span></span>|
|<span data-ttu-id="d5701-308">http://schemas.microsoft.com/ws/2008/06/identity/claims/ispersistent</span><span class="sxs-lookup"><span data-stu-id="d5701-308">http://schemas.microsoft.com/ws/2008/06/identity/claims/ispersistent</span></span>|
|<span data-ttu-id="d5701-309">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier</span><span class="sxs-lookup"><span data-stu-id="d5701-309">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier</span></span>|
|<span data-ttu-id="d5701-310">http://schemas.microsoft.com/identity/claims/scope</span><span class="sxs-lookup"><span data-stu-id="d5701-310">http://schemas.microsoft.com/identity/claims/scope</span></span>|

## <a name="claims-mapping-policy-properties"></a><span data-ttu-id="d5701-311">宣告對應原則屬性</span><span class="sxs-lookup"><span data-stu-id="d5701-311">Claims mapping policy properties</span></span>
<span data-ttu-id="d5701-312">使用對應的宣告會發出，因此 hello 資料來自何處，原則 toocontrol 宣告 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="d5701-312">Use hello properties of a claims mapping policy toocontrol which claims are emitted, and where hello data is sourced from.</span></span> <span data-ttu-id="d5701-313">如果沒有原則設定，hello 系統簽發權杖包含 hello 核心宣告集，hello 基本宣告集，並選擇 tooreceive hello 應用程式的任何選擇性宣告。</span><span class="sxs-lookup"><span data-stu-id="d5701-313">If no policy is set, hello system issues tokens containing hello core claim set, hello basic claim set, and any optional claims that hello application has chosen tooreceive.</span></span>

### <a name="include-basic-claim-set"></a><span data-ttu-id="d5701-314">包含基本宣告集</span><span class="sxs-lookup"><span data-stu-id="d5701-314">Include basic claim set</span></span>

<span data-ttu-id="d5701-315">**字串：**IncludeBasicClaimSet</span><span class="sxs-lookup"><span data-stu-id="d5701-315">**String:** IncludeBasicClaimSet</span></span>

<span data-ttu-id="d5701-316">**資料類型：**布林值 (True 或 False)</span><span class="sxs-lookup"><span data-stu-id="d5701-316">**Data type:** Boolean (True or False)</span></span>

<span data-ttu-id="d5701-317">**摘要：**此屬性決定 hello 基本的宣告集合是否包含在這個原則影響的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="d5701-317">**Summary:** This property determines whether hello basic claim set is included in tokens affected by this policy.</span></span> 

- <span data-ttu-id="d5701-318">如果組 tooTrue，hello 基本的宣告集中的所有宣告會發出權杖的 hello 原則影響。</span><span class="sxs-lookup"><span data-stu-id="d5701-318">If set tooTrue, all claims in hello basic claim set are emitted in tokens affected by hello policy.</span></span> 
- <span data-ttu-id="d5701-319">如果組 tooFalse，hello 基本的宣告集中的宣告不在 hello 語彙基元，除非它們個別加入 hello hello 宣告結構描述屬性中相同原則。</span><span class="sxs-lookup"><span data-stu-id="d5701-319">If set tooFalse, claims in hello basic claim set are not in hello tokens, unless they are individually added in hello claims schema property of hello same policy.</span></span>

>[!NOTE] 
><span data-ttu-id="d5701-320">設定會在每個權杖，不論這個屬性設定為宣告 hello 核心宣告。</span><span class="sxs-lookup"><span data-stu-id="d5701-320">Claims in hello core claim set are present in every token, regardless of what this property is set to.</span></span> 

### <a name="claims-schema"></a><span data-ttu-id="d5701-321">宣告結構描述</span><span class="sxs-lookup"><span data-stu-id="d5701-321">Claims schema</span></span>

<span data-ttu-id="d5701-322">**字串：**ClaimsSchema</span><span class="sxs-lookup"><span data-stu-id="d5701-322">**String:** ClaimsSchema</span></span>

<span data-ttu-id="d5701-323">**資料類型：**具有一或多個宣告結構描述項目的 JSON blob</span><span class="sxs-lookup"><span data-stu-id="d5701-323">**Data type:** JSON blob with one or more claim schema entries</span></span>

<span data-ttu-id="d5701-324">**摘要：**此屬性會定義哪些宣告會出現在 hello 原則影響的 hello 語彙基元，此外 toohello 基本宣告集和 hello 核心宣告集。</span><span class="sxs-lookup"><span data-stu-id="d5701-324">**Summary:** This property defines which claims are present in hello tokens affected by hello policy, in addition toohello basic claim set and hello core claim set.</span></span>
<span data-ttu-id="d5701-325">此屬性中所定義的每個宣告結構描述項目必須有某些資訊。</span><span class="sxs-lookup"><span data-stu-id="d5701-325">For each claim schema entry defined in this property, certain information is required.</span></span> <span data-ttu-id="d5701-326">您必須指定 hello 資料來自何處 (**值**或**來源/識別碼組**)，以及哪個宣告 hello 資料就會發出為 (**宣告的型別**)。</span><span class="sxs-lookup"><span data-stu-id="d5701-326">You must specify where hello data is coming from (**Value** or **Source/ID pair**), and which claim hello data is emitted as (**Claim Type**).</span></span>

### <a name="claim-schema-entry-elements"></a><span data-ttu-id="d5701-327">宣告結構描述項目的元素</span><span class="sxs-lookup"><span data-stu-id="d5701-327">Claim schema entry elements</span></span>

<span data-ttu-id="d5701-328">**值：** hello 值項目定義為靜態值為 hello 資料 toobe hello 宣告中所發出。</span><span class="sxs-lookup"><span data-stu-id="d5701-328">**Value:** hello Value element defines a static value as hello data toobe emitted in hello claim.</span></span>

<span data-ttu-id="d5701-329">**來源/識別碼組：** hello 來源和項目指定 ID 定義 hello 宣告中的 hello 資料來自何處。</span><span class="sxs-lookup"><span data-stu-id="d5701-329">**Source/ID pair:** hello Source and ID elements define where hello data in hello claim is sourced from.</span></span> 

<span data-ttu-id="d5701-330">hello 來源項目必須設定 tooone hello 以下的：</span><span class="sxs-lookup"><span data-stu-id="d5701-330">hello Source element must be set tooone of hello following:</span></span> 


- <span data-ttu-id="d5701-331">「 使用者 」: hello hello 資料宣告是 hello 使用者物件上的屬性。</span><span class="sxs-lookup"><span data-stu-id="d5701-331">"user": hello data in hello claim is a property on hello User object.</span></span> 
- <span data-ttu-id="d5701-332">「 應用程式 」: hello hello 資料宣告是 hello 應用程式 （用戶端） 的服務主體上的屬性。</span><span class="sxs-lookup"><span data-stu-id="d5701-332">"application": hello data in hello claim is a property on hello application (client) service principal.</span></span> 
- <span data-ttu-id="d5701-333">「 資源 」: hello hello 資料宣告是 hello 資源服務主體上的屬性。</span><span class="sxs-lookup"><span data-stu-id="d5701-333">"resource": hello data in hello claim is a property on hello resource service principal.</span></span>
- <span data-ttu-id="d5701-334">"audience": hello hello 宣告中的資料是 hello 是 hello 對象的 hello 語彙基元 （任一 hello 用戶端或資源服務主體） 的服務主體上的屬性。</span><span class="sxs-lookup"><span data-stu-id="d5701-334">"audience": hello data in hello claim is a property on hello service principal that is hello audience of hello token (either hello client or resource service principal).</span></span>
- <span data-ttu-id="d5701-335">「 公司 」: hello hello 資料宣告是 hello 資源租用戶的公司物件上的屬性。</span><span class="sxs-lookup"><span data-stu-id="d5701-335">“company”: hello data in hello claim is a property on hello resource tenant’s Company object.</span></span>
- <span data-ttu-id="d5701-336">「 轉換 」: hello hello 資料宣告從宣告轉換 （請參閱本文稍後的 hello"宣告轉換 」 一節）。</span><span class="sxs-lookup"><span data-stu-id="d5701-336">"transformation": hello data in hello claim is from claims transformation (see hello "Claims transformation" section later in this article).</span></span> 

<span data-ttu-id="d5701-337">如果 hello 來源是轉換，hello **TransformationID**元素必須包含在這個宣告定義。</span><span class="sxs-lookup"><span data-stu-id="d5701-337">If hello source is transformation, hello **TransformationID** element must be included in this claim definition as well.</span></span>

<span data-ttu-id="d5701-338">hello ID 項目識別哪個 hello 來源上的屬性提供 hello 宣告 hello 值。</span><span class="sxs-lookup"><span data-stu-id="d5701-338">hello ID element identifies which property on hello source provides hello value for hello claim.</span></span> <span data-ttu-id="d5701-339">hello 下表列出每個值的來源有效的識別碼 hello 的值。</span><span class="sxs-lookup"><span data-stu-id="d5701-339">hello following table lists hello values of ID valid for each value of Source.</span></span>

#### <a name="table-3-valid-id-values-per-source"></a><span data-ttu-id="d5701-340">表 3：每個來源的有效識別碼值</span><span class="sxs-lookup"><span data-stu-id="d5701-340">Table 3: Valid ID values per source</span></span>
|<span data-ttu-id="d5701-341">來源</span><span class="sxs-lookup"><span data-stu-id="d5701-341">Source</span></span>|<span data-ttu-id="d5701-342">ID</span><span class="sxs-lookup"><span data-stu-id="d5701-342">ID</span></span>|<span data-ttu-id="d5701-343">說明</span><span class="sxs-lookup"><span data-stu-id="d5701-343">Description</span></span>|
|-----|-----|-----|
|<span data-ttu-id="d5701-344">User</span><span class="sxs-lookup"><span data-stu-id="d5701-344">User</span></span>|<span data-ttu-id="d5701-345">surname</span><span class="sxs-lookup"><span data-stu-id="d5701-345">surname</span></span>|<span data-ttu-id="d5701-346">姓氏</span><span class="sxs-lookup"><span data-stu-id="d5701-346">Family Name</span></span>|
|<span data-ttu-id="d5701-347">User</span><span class="sxs-lookup"><span data-stu-id="d5701-347">User</span></span>|<span data-ttu-id="d5701-348">givenname</span><span class="sxs-lookup"><span data-stu-id="d5701-348">givenname</span></span>|<span data-ttu-id="d5701-349">名字</span><span class="sxs-lookup"><span data-stu-id="d5701-349">Given Name</span></span>|
|<span data-ttu-id="d5701-350">User</span><span class="sxs-lookup"><span data-stu-id="d5701-350">User</span></span>|<span data-ttu-id="d5701-351">displayname</span><span class="sxs-lookup"><span data-stu-id="d5701-351">displayname</span></span>|<span data-ttu-id="d5701-352">顯示名稱</span><span class="sxs-lookup"><span data-stu-id="d5701-352">Display Name</span></span>|
|<span data-ttu-id="d5701-353">User</span><span class="sxs-lookup"><span data-stu-id="d5701-353">User</span></span>|<span data-ttu-id="d5701-354">objectid</span><span class="sxs-lookup"><span data-stu-id="d5701-354">objectid</span></span>|<span data-ttu-id="d5701-355">ObjectID</span><span class="sxs-lookup"><span data-stu-id="d5701-355">ObjectID</span></span>|
|<span data-ttu-id="d5701-356">User</span><span class="sxs-lookup"><span data-stu-id="d5701-356">User</span></span>|<span data-ttu-id="d5701-357">mail</span><span class="sxs-lookup"><span data-stu-id="d5701-357">mail</span></span>|<span data-ttu-id="d5701-358">電子郵件地址</span><span class="sxs-lookup"><span data-stu-id="d5701-358">Email Address</span></span>|
|<span data-ttu-id="d5701-359">User</span><span class="sxs-lookup"><span data-stu-id="d5701-359">User</span></span>|<span data-ttu-id="d5701-360">userprincipalname</span><span class="sxs-lookup"><span data-stu-id="d5701-360">userprincipalname</span></span>|<span data-ttu-id="d5701-361">使用者主體名稱</span><span class="sxs-lookup"><span data-stu-id="d5701-361">User Principal Name</span></span>|
|<span data-ttu-id="d5701-362">User</span><span class="sxs-lookup"><span data-stu-id="d5701-362">User</span></span>|<span data-ttu-id="d5701-363">department</span><span class="sxs-lookup"><span data-stu-id="d5701-363">department</span></span>|<span data-ttu-id="d5701-364">department</span><span class="sxs-lookup"><span data-stu-id="d5701-364">Department</span></span>|
|<span data-ttu-id="d5701-365">User</span><span class="sxs-lookup"><span data-stu-id="d5701-365">User</span></span>|<span data-ttu-id="d5701-366">onpremisessamaccountname</span><span class="sxs-lookup"><span data-stu-id="d5701-366">onpremisessamaccountname</span></span>|<span data-ttu-id="d5701-367">內部部署的 Sam 帳戶名稱</span><span class="sxs-lookup"><span data-stu-id="d5701-367">On Premises Sam Account Name</span></span>|
|<span data-ttu-id="d5701-368">User</span><span class="sxs-lookup"><span data-stu-id="d5701-368">User</span></span>|<span data-ttu-id="d5701-369">netbiosname</span><span class="sxs-lookup"><span data-stu-id="d5701-369">netbiosname</span></span>|<span data-ttu-id="d5701-370">NetBios 名稱</span><span class="sxs-lookup"><span data-stu-id="d5701-370">NetBios Name</span></span>|
|<span data-ttu-id="d5701-371">User</span><span class="sxs-lookup"><span data-stu-id="d5701-371">User</span></span>|<span data-ttu-id="d5701-372">dnsdomainname</span><span class="sxs-lookup"><span data-stu-id="d5701-372">dnsdomainname</span></span>|<span data-ttu-id="d5701-373">Dns 網域名稱</span><span class="sxs-lookup"><span data-stu-id="d5701-373">Dns Domain Name</span></span>|
|<span data-ttu-id="d5701-374">User</span><span class="sxs-lookup"><span data-stu-id="d5701-374">User</span></span>|<span data-ttu-id="d5701-375">onpremisesecurityidentifier</span><span class="sxs-lookup"><span data-stu-id="d5701-375">onpremisesecurityidentifier</span></span>|<span data-ttu-id="d5701-376">內部部署的安全性識別碼</span><span class="sxs-lookup"><span data-stu-id="d5701-376">on-premises Security Identifier</span></span>|
|<span data-ttu-id="d5701-377">User</span><span class="sxs-lookup"><span data-stu-id="d5701-377">User</span></span>|<span data-ttu-id="d5701-378">companyname</span><span class="sxs-lookup"><span data-stu-id="d5701-378">companyname</span></span>|<span data-ttu-id="d5701-379">組織名稱</span><span class="sxs-lookup"><span data-stu-id="d5701-379">Organization Name</span></span>|
|<span data-ttu-id="d5701-380">User</span><span class="sxs-lookup"><span data-stu-id="d5701-380">User</span></span>|<span data-ttu-id="d5701-381">streetaddress</span><span class="sxs-lookup"><span data-stu-id="d5701-381">streetaddress</span></span>|<span data-ttu-id="d5701-382">街道地址</span><span class="sxs-lookup"><span data-stu-id="d5701-382">Street Address</span></span>|
|<span data-ttu-id="d5701-383">User</span><span class="sxs-lookup"><span data-stu-id="d5701-383">User</span></span>|<span data-ttu-id="d5701-384">postalcode</span><span class="sxs-lookup"><span data-stu-id="d5701-384">postalcode</span></span>|<span data-ttu-id="d5701-385">郵遞區號</span><span class="sxs-lookup"><span data-stu-id="d5701-385">Postal Code</span></span>|
|<span data-ttu-id="d5701-386">User</span><span class="sxs-lookup"><span data-stu-id="d5701-386">User</span></span>|<span data-ttu-id="d5701-387">preferredlanguange</span><span class="sxs-lookup"><span data-stu-id="d5701-387">preferredlanguange</span></span>|<span data-ttu-id="d5701-388">慣用語言</span><span class="sxs-lookup"><span data-stu-id="d5701-388">Preferred Language</span></span>|
|<span data-ttu-id="d5701-389">User</span><span class="sxs-lookup"><span data-stu-id="d5701-389">User</span></span>|<span data-ttu-id="d5701-390">onpremisesuserprincipalname</span><span class="sxs-lookup"><span data-stu-id="d5701-390">onpremisesuserprincipalname</span></span>|<span data-ttu-id="d5701-391">內部部署的 UPN</span><span class="sxs-lookup"><span data-stu-id="d5701-391">on-premises UPN</span></span>|
|<span data-ttu-id="d5701-392">User</span><span class="sxs-lookup"><span data-stu-id="d5701-392">User</span></span>|<span data-ttu-id="d5701-393">mailNickname</span><span class="sxs-lookup"><span data-stu-id="d5701-393">mailnickname</span></span>|<span data-ttu-id="d5701-394">郵件暱稱</span><span class="sxs-lookup"><span data-stu-id="d5701-394">Mail Nickname</span></span>|
|<span data-ttu-id="d5701-395">User</span><span class="sxs-lookup"><span data-stu-id="d5701-395">User</span></span>|<span data-ttu-id="d5701-396">extensionattribute1</span><span class="sxs-lookup"><span data-stu-id="d5701-396">extensionattribute1</span></span>|<span data-ttu-id="d5701-397">擴充屬性 1</span><span class="sxs-lookup"><span data-stu-id="d5701-397">Extension Attribute 1</span></span>|
|<span data-ttu-id="d5701-398">User</span><span class="sxs-lookup"><span data-stu-id="d5701-398">User</span></span>|<span data-ttu-id="d5701-399">extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="d5701-399">extensionattribute2</span></span>|<span data-ttu-id="d5701-400">擴充屬性 2</span><span class="sxs-lookup"><span data-stu-id="d5701-400">Extension Attribute 2</span></span>|
|<span data-ttu-id="d5701-401">User</span><span class="sxs-lookup"><span data-stu-id="d5701-401">User</span></span>|<span data-ttu-id="d5701-402">extensionattribute3</span><span class="sxs-lookup"><span data-stu-id="d5701-402">extensionattribute3</span></span>|<span data-ttu-id="d5701-403">擴充屬性 3</span><span class="sxs-lookup"><span data-stu-id="d5701-403">Extension Attribute 3</span></span>|
|<span data-ttu-id="d5701-404">User</span><span class="sxs-lookup"><span data-stu-id="d5701-404">User</span></span>|<span data-ttu-id="d5701-405">extensionattribute4</span><span class="sxs-lookup"><span data-stu-id="d5701-405">extensionattribute4</span></span>|<span data-ttu-id="d5701-406">擴充屬性 4</span><span class="sxs-lookup"><span data-stu-id="d5701-406">Extension Attribute 4</span></span>|
|<span data-ttu-id="d5701-407">User</span><span class="sxs-lookup"><span data-stu-id="d5701-407">User</span></span>|<span data-ttu-id="d5701-408">extensionattribute5</span><span class="sxs-lookup"><span data-stu-id="d5701-408">extensionattribute5</span></span>|<span data-ttu-id="d5701-409">擴充屬性 5</span><span class="sxs-lookup"><span data-stu-id="d5701-409">Extension Attribute 5</span></span>|
|<span data-ttu-id="d5701-410">User</span><span class="sxs-lookup"><span data-stu-id="d5701-410">User</span></span>|<span data-ttu-id="d5701-411">extensionattribute6</span><span class="sxs-lookup"><span data-stu-id="d5701-411">extensionattribute6</span></span>|<span data-ttu-id="d5701-412">擴充屬性 6</span><span class="sxs-lookup"><span data-stu-id="d5701-412">Extension Attribute 6</span></span>|
|<span data-ttu-id="d5701-413">User</span><span class="sxs-lookup"><span data-stu-id="d5701-413">User</span></span>|<span data-ttu-id="d5701-414">extensionattribute7</span><span class="sxs-lookup"><span data-stu-id="d5701-414">extensionattribute7</span></span>|<span data-ttu-id="d5701-415">擴充屬性 7</span><span class="sxs-lookup"><span data-stu-id="d5701-415">Extension Attribute 7</span></span>|
|<span data-ttu-id="d5701-416">User</span><span class="sxs-lookup"><span data-stu-id="d5701-416">User</span></span>|<span data-ttu-id="d5701-417">extensionattribute8</span><span class="sxs-lookup"><span data-stu-id="d5701-417">extensionattribute8</span></span>|<span data-ttu-id="d5701-418">擴充屬性 8</span><span class="sxs-lookup"><span data-stu-id="d5701-418">Extension Attribute 8</span></span>|
|<span data-ttu-id="d5701-419">User</span><span class="sxs-lookup"><span data-stu-id="d5701-419">User</span></span>|<span data-ttu-id="d5701-420">extensionattribute9</span><span class="sxs-lookup"><span data-stu-id="d5701-420">extensionattribute9</span></span>|<span data-ttu-id="d5701-421">擴充屬性 9</span><span class="sxs-lookup"><span data-stu-id="d5701-421">Extension Attribute 9</span></span>|
|<span data-ttu-id="d5701-422">User</span><span class="sxs-lookup"><span data-stu-id="d5701-422">User</span></span>|<span data-ttu-id="d5701-423">extensionattribute10</span><span class="sxs-lookup"><span data-stu-id="d5701-423">extensionattribute10</span></span>|<span data-ttu-id="d5701-424">擴充屬性 10</span><span class="sxs-lookup"><span data-stu-id="d5701-424">Extension Attribute 10</span></span>|
|<span data-ttu-id="d5701-425">User</span><span class="sxs-lookup"><span data-stu-id="d5701-425">User</span></span>|<span data-ttu-id="d5701-426">extensionattribute11</span><span class="sxs-lookup"><span data-stu-id="d5701-426">extensionattribute11</span></span>|<span data-ttu-id="d5701-427">擴充屬性 11</span><span class="sxs-lookup"><span data-stu-id="d5701-427">Extension Attribute 11</span></span>|
|<span data-ttu-id="d5701-428">User</span><span class="sxs-lookup"><span data-stu-id="d5701-428">User</span></span>|<span data-ttu-id="d5701-429">extensionattribute12</span><span class="sxs-lookup"><span data-stu-id="d5701-429">extensionattribute12</span></span>|<span data-ttu-id="d5701-430">擴充屬性 12</span><span class="sxs-lookup"><span data-stu-id="d5701-430">Extension Attribute 12</span></span>|
|<span data-ttu-id="d5701-431">User</span><span class="sxs-lookup"><span data-stu-id="d5701-431">User</span></span>|<span data-ttu-id="d5701-432">extensionattribute13</span><span class="sxs-lookup"><span data-stu-id="d5701-432">extensionattribute13</span></span>|<span data-ttu-id="d5701-433">擴充屬性 13</span><span class="sxs-lookup"><span data-stu-id="d5701-433">Extension Attribute 13</span></span>|
|<span data-ttu-id="d5701-434">User</span><span class="sxs-lookup"><span data-stu-id="d5701-434">User</span></span>|<span data-ttu-id="d5701-435">extensionattribute14</span><span class="sxs-lookup"><span data-stu-id="d5701-435">extensionattribute14</span></span>|<span data-ttu-id="d5701-436">擴充屬性 14</span><span class="sxs-lookup"><span data-stu-id="d5701-436">Extension Attribute 14</span></span>|
|<span data-ttu-id="d5701-437">User</span><span class="sxs-lookup"><span data-stu-id="d5701-437">User</span></span>|<span data-ttu-id="d5701-438">extensionattribute15</span><span class="sxs-lookup"><span data-stu-id="d5701-438">extensionattribute15</span></span>|<span data-ttu-id="d5701-439">擴充屬性 15</span><span class="sxs-lookup"><span data-stu-id="d5701-439">Extension Attribute 15</span></span>|
|<span data-ttu-id="d5701-440">User</span><span class="sxs-lookup"><span data-stu-id="d5701-440">User</span></span>|<span data-ttu-id="d5701-441">othermail</span><span class="sxs-lookup"><span data-stu-id="d5701-441">othermail</span></span>|<span data-ttu-id="d5701-442">其他郵件</span><span class="sxs-lookup"><span data-stu-id="d5701-442">Other Mail</span></span>|
|<span data-ttu-id="d5701-443">User</span><span class="sxs-lookup"><span data-stu-id="d5701-443">User</span></span>|<span data-ttu-id="d5701-444">country</span><span class="sxs-lookup"><span data-stu-id="d5701-444">country</span></span>|<span data-ttu-id="d5701-445">國家 (地區)</span><span class="sxs-lookup"><span data-stu-id="d5701-445">Country</span></span>|
|<span data-ttu-id="d5701-446">User</span><span class="sxs-lookup"><span data-stu-id="d5701-446">User</span></span>|<span data-ttu-id="d5701-447">city</span><span class="sxs-lookup"><span data-stu-id="d5701-447">city</span></span>|<span data-ttu-id="d5701-448">City</span><span class="sxs-lookup"><span data-stu-id="d5701-448">City</span></span>|
|<span data-ttu-id="d5701-449">User</span><span class="sxs-lookup"><span data-stu-id="d5701-449">User</span></span>|<span data-ttu-id="d5701-450">state</span><span class="sxs-lookup"><span data-stu-id="d5701-450">state</span></span>|<span data-ttu-id="d5701-451">State</span><span class="sxs-lookup"><span data-stu-id="d5701-451">State</span></span>|
|<span data-ttu-id="d5701-452">User</span><span class="sxs-lookup"><span data-stu-id="d5701-452">User</span></span>|<span data-ttu-id="d5701-453">jobtitle</span><span class="sxs-lookup"><span data-stu-id="d5701-453">jobtitle</span></span>|<span data-ttu-id="d5701-454">職稱</span><span class="sxs-lookup"><span data-stu-id="d5701-454">Job Title</span></span>|
|<span data-ttu-id="d5701-455">User</span><span class="sxs-lookup"><span data-stu-id="d5701-455">User</span></span>|<span data-ttu-id="d5701-456">employeeid</span><span class="sxs-lookup"><span data-stu-id="d5701-456">employeeid</span></span>|<span data-ttu-id="d5701-457">員工識別碼</span><span class="sxs-lookup"><span data-stu-id="d5701-457">Employee ID</span></span>|
|<span data-ttu-id="d5701-458">User</span><span class="sxs-lookup"><span data-stu-id="d5701-458">User</span></span>|<span data-ttu-id="d5701-459">facsimiletelephonenumber</span><span class="sxs-lookup"><span data-stu-id="d5701-459">facsimiletelephonenumber</span></span>|<span data-ttu-id="d5701-460">傳真電話號碼</span><span class="sxs-lookup"><span data-stu-id="d5701-460">Facsimile Telephone Number</span></span>|
|<span data-ttu-id="d5701-461">application, resource, audience</span><span class="sxs-lookup"><span data-stu-id="d5701-461">application, resource, audience</span></span>|<span data-ttu-id="d5701-462">displayname</span><span class="sxs-lookup"><span data-stu-id="d5701-462">displayname</span></span>|<span data-ttu-id="d5701-463">顯示名稱</span><span class="sxs-lookup"><span data-stu-id="d5701-463">Display Name</span></span>|
|<span data-ttu-id="d5701-464">application, resource, audience</span><span class="sxs-lookup"><span data-stu-id="d5701-464">application, resource, audience</span></span>|<span data-ttu-id="d5701-465">objected</span><span class="sxs-lookup"><span data-stu-id="d5701-465">objected</span></span>|<span data-ttu-id="d5701-466">ObjectID</span><span class="sxs-lookup"><span data-stu-id="d5701-466">ObjectID</span></span>|
|<span data-ttu-id="d5701-467">application, resource, audience</span><span class="sxs-lookup"><span data-stu-id="d5701-467">application, resource, audience</span></span>|<span data-ttu-id="d5701-468">tags</span><span class="sxs-lookup"><span data-stu-id="d5701-468">tags</span></span>|<span data-ttu-id="d5701-469">服務主體標籤</span><span class="sxs-lookup"><span data-stu-id="d5701-469">Service Principal Tag</span></span>|
|<span data-ttu-id="d5701-470">公司</span><span class="sxs-lookup"><span data-stu-id="d5701-470">Company</span></span>|<span data-ttu-id="d5701-471">tenantcountry</span><span class="sxs-lookup"><span data-stu-id="d5701-471">tenantcountry</span></span>|<span data-ttu-id="d5701-472">租用戶的國家/地區</span><span class="sxs-lookup"><span data-stu-id="d5701-472">Tenant’s country</span></span>|

<span data-ttu-id="d5701-473">**TransformationID:** hello TransformationID 元素必須提供來源項目時，才 hello 設定得 「 轉換 」。</span><span class="sxs-lookup"><span data-stu-id="d5701-473">**TransformationID:** hello TransformationID element must be provided only if hello Source element is set too“transformation”.</span></span>

- <span data-ttu-id="d5701-474">此項目必須符合在 hello hello 轉換項目的 hello ID 元素**ClaimsTransformation**屬性，定義如何產生此宣告的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="d5701-474">This element must match hello ID element of hello transformation entry in hello **ClaimsTransformation** property that defines how hello data for this claim is generated.</span></span>

<span data-ttu-id="d5701-475">**宣告類型：** hello **JwtClaimType**和**SamlClaimType**元素會定義哪個宣告此宣告的結構描述項目參考。</span><span class="sxs-lookup"><span data-stu-id="d5701-475">**Claim Type:** hello **JwtClaimType** and **SamlClaimType** elements define which claim this claim schema entry refers to.</span></span>

- <span data-ttu-id="d5701-476">hello JwtClaimType 必須包含發出的 Jwt hello 宣告 toobe hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="d5701-476">hello JwtClaimType must contain hello name of hello claim toobe emitted in JWTs.</span></span>
- <span data-ttu-id="d5701-477">hello SamlClaimType 必須包含 URI 的 hello 宣告 toobe SAML 權杖中發出的 hello。</span><span class="sxs-lookup"><span data-stu-id="d5701-477">hello SamlClaimType must contain hello URI of hello claim toobe emitted in SAML tokens.</span></span>

>[!NOTE]
><span data-ttu-id="d5701-478">名稱與 Uri 中 hello 的宣告受限制的宣告集不能用於為 hello 宣告型別項目。</span><span class="sxs-lookup"><span data-stu-id="d5701-478">Names and URIs of claims in hello restricted claim set cannot be used for hello claim type elements.</span></span> <span data-ttu-id="d5701-479">如需詳細資訊，請參閱本文稍後 hello < 例外狀況和限制 > 一節。</span><span class="sxs-lookup"><span data-stu-id="d5701-479">For more information, see hello "Exceptions and restrictions" section later in this article.</span></span>

### <a name="claims-transformation"></a><span data-ttu-id="d5701-480">宣告轉換</span><span class="sxs-lookup"><span data-stu-id="d5701-480">Claims transformation</span></span>

<span data-ttu-id="d5701-481">**字串：**ClaimsTransformation</span><span class="sxs-lookup"><span data-stu-id="d5701-481">**String:** ClaimsTransformation</span></span>

<span data-ttu-id="d5701-482">**資料類型：**具有一或多個轉換項目的 JSON blob</span><span class="sxs-lookup"><span data-stu-id="d5701-482">**Data type:** JSON blob, with one or more transformation entries</span></span> 

<span data-ttu-id="d5701-483">**摘要：**使用這個屬性 tooapply 一般轉換 toosource 資料、 toogenerate hello 輸出資料的宣告中指定 hello 宣告結構描述。</span><span class="sxs-lookup"><span data-stu-id="d5701-483">**Summary:** Use this property tooapply common transformations toosource data, toogenerate hello output data for claims specified in hello Claims Schema.</span></span>

<span data-ttu-id="d5701-484">**ID:**使用 hello ID 項目 tooreference 此轉換中的項目 hello TransformationID 宣告結構描述項目。</span><span class="sxs-lookup"><span data-stu-id="d5701-484">**ID:** Use hello ID element tooreference this transformation entry in hello TransformationID Claims Schema entry.</span></span> <span data-ttu-id="d5701-485">對於這項原則內的每個轉換項目，此值都必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="d5701-485">This value must be unique for each transformation entry within this policy.</span></span>

<span data-ttu-id="d5701-486">**TransformationMethod:** hello TransformationMethod 元素會識別哪一個作業已執行的 toogenerate hello hello 宣告的資料。</span><span class="sxs-lookup"><span data-stu-id="d5701-486">**TransformationMethod:** hello TransformationMethod element identifies which operation is performed toogenerate hello data for hello claim.</span></span>

<span data-ttu-id="d5701-487">根據選擇的 hello 方法，必須輸入和輸出的一組。</span><span class="sxs-lookup"><span data-stu-id="d5701-487">Based on hello method chosen, a set of inputs and outputs is expected.</span></span> <span data-ttu-id="d5701-488">這些定義使用 hello **InputClaims**，**這**和**OutputClaims**項目。</span><span class="sxs-lookup"><span data-stu-id="d5701-488">These are defined by using hello **InputClaims**, **InputParameters** and **OutputClaims** elements.</span></span>

#### <a name="table-4-transformation-methods-and-expected-inputs-and-outputs"></a><span data-ttu-id="d5701-489">表 4：轉換方法和預期的輸入和輸出</span><span class="sxs-lookup"><span data-stu-id="d5701-489">Table 4: Transformation methods and expected inputs and outputs</span></span>
|<span data-ttu-id="d5701-490">TransformationMethod</span><span class="sxs-lookup"><span data-stu-id="d5701-490">TransformationMethod</span></span>|<span data-ttu-id="d5701-491">預期的輸入</span><span class="sxs-lookup"><span data-stu-id="d5701-491">Expected input</span></span>|<span data-ttu-id="d5701-492">預期的輸出</span><span class="sxs-lookup"><span data-stu-id="d5701-492">Expected output</span></span>|<span data-ttu-id="d5701-493">說明</span><span class="sxs-lookup"><span data-stu-id="d5701-493">Description</span></span>|
|-----|-----|-----|-----|
|<span data-ttu-id="d5701-494">Join</span><span class="sxs-lookup"><span data-stu-id="d5701-494">Join</span></span>|<span data-ttu-id="d5701-495">string1、string2、分隔符號</span><span class="sxs-lookup"><span data-stu-id="d5701-495">string1, string2, separator</span></span>|<span data-ttu-id="d5701-496">outputClaim</span><span class="sxs-lookup"><span data-stu-id="d5701-496">outputClaim</span></span>|<span data-ttu-id="d5701-497">可在輸入字串之間使用分隔符號來聯結這些字串。</span><span class="sxs-lookup"><span data-stu-id="d5701-497">Joins input strings by using a separator in between.</span></span> <span data-ttu-id="d5701-498">例如：string1:"foo@bar.com" , string2:"sandbox" , separator:"." 會導致 outputClaim:"foo@bar.com.sandbox"</span><span class="sxs-lookup"><span data-stu-id="d5701-498">For example: string1:"foo@bar.com" , string2:"sandbox" , separator:"." results in outputClaim:"foo@bar.com.sandbox"</span></span>|
|<span data-ttu-id="d5701-499">ExtractMailPrefix</span><span class="sxs-lookup"><span data-stu-id="d5701-499">ExtractMailPrefix</span></span>|<span data-ttu-id="d5701-500">mail</span><span class="sxs-lookup"><span data-stu-id="d5701-500">mail</span></span>|<span data-ttu-id="d5701-501">outputClaim</span><span class="sxs-lookup"><span data-stu-id="d5701-501">outputClaim</span></span>|<span data-ttu-id="d5701-502">擷取 hello 的電子郵件地址的本機部份。</span><span class="sxs-lookup"><span data-stu-id="d5701-502">Extracts hello local part of an email address.</span></span> <span data-ttu-id="d5701-503">例如：mail:"foo@bar.com" 會導致 outputClaim:"foo"。</span><span class="sxs-lookup"><span data-stu-id="d5701-503">For example: mail:"foo@bar.com" results in outputClaim:"foo".</span></span> <span data-ttu-id="d5701-504">如果不是 @ 符號是存在，則現狀傳回 hello 原始輸入的字串。</span><span class="sxs-lookup"><span data-stu-id="d5701-504">If no @ sign is present, then hello orignal input string is returned as is.</span></span>|

<span data-ttu-id="d5701-505">**InputClaims:**使用宣告架構項目 tooa 轉換 InputClaims 元素 toopass hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="d5701-505">**InputClaims:** Use an InputClaims element toopass hello data from a claim schema entry tooa transformation.</span></span> <span data-ttu-id="d5701-506">它有兩個屬性：**ClaimTypeReferenceId** 和 **TransformationClaimType**。</span><span class="sxs-lookup"><span data-stu-id="d5701-506">It has two attributes: **ClaimTypeReferenceId** and **TransformationClaimType**.</span></span>

- <span data-ttu-id="d5701-507">**ClaimTypeReferenceId**聯結與 hello 宣告結構描述項目 toofind hello 適當輸入宣告的 ID 項目。</span><span class="sxs-lookup"><span data-stu-id="d5701-507">**ClaimTypeReferenceId** is joined with ID element of hello claim schema entry toofind hello appropriate input claim.</span></span> 
- <span data-ttu-id="d5701-508">**TransformationClaimType**是使用的 toogive 唯一名稱 toothis 輸入。</span><span class="sxs-lookup"><span data-stu-id="d5701-508">**TransformationClaimType** is used toogive a unique name toothis input.</span></span> <span data-ttu-id="d5701-509">此名稱必須符合預期的 hello 輸入 hello 轉換方法的其中一種。</span><span class="sxs-lookup"><span data-stu-id="d5701-509">This name must match one of hello expected inputs for hello transformation method.</span></span>

<span data-ttu-id="d5701-510">**在這：**使用這項目 toopass 常數值 tooa 轉換。</span><span class="sxs-lookup"><span data-stu-id="d5701-510">**InputParameters:** Use an InputParameters element toopass a constant value tooa transformation.</span></span> <span data-ttu-id="d5701-511">它有兩個屬性：**值**和**識別碼**。</span><span class="sxs-lookup"><span data-stu-id="d5701-511">It has two attributes: **Value** and **ID**.</span></span>

- <span data-ttu-id="d5701-512">**值**hello 實際的常數值 toobe 傳遞。</span><span class="sxs-lookup"><span data-stu-id="d5701-512">**Value** is hello actual constant value toobe passed.</span></span>
- <span data-ttu-id="d5701-513">**識別碼**是使用的 toogive 唯一名稱 toothis 輸入。</span><span class="sxs-lookup"><span data-stu-id="d5701-513">**ID** is used toogive a unique name toothis input.</span></span> <span data-ttu-id="d5701-514">此名稱必須符合預期的 hello 輸入 hello 轉換方法的其中一種。</span><span class="sxs-lookup"><span data-stu-id="d5701-514">This name must match one of hello expected inputs for hello transformation method.</span></span>

<span data-ttu-id="d5701-515">**OutputClaims:**使用產生的轉換，OutputClaims 元素 toohold hello 資料，並將它連接 tooa 宣告結構描述項目。</span><span class="sxs-lookup"><span data-stu-id="d5701-515">**OutputClaims:** Use an OutputClaims element toohold hello data generated by a transformation, and tie it tooa claim schema entry.</span></span> <span data-ttu-id="d5701-516">它有兩個屬性：**ClaimTypeReferenceId** 和 **TransformationClaimType**。</span><span class="sxs-lookup"><span data-stu-id="d5701-516">It has two attributes: **ClaimTypeReferenceId** and **TransformationClaimType**.</span></span>

- <span data-ttu-id="d5701-517">**ClaimTypeReferenceId**與 hello 識別碼 hello 宣告結構描述項目 toofind hello 適當的輸出宣告的聯結。</span><span class="sxs-lookup"><span data-stu-id="d5701-517">**ClaimTypeReferenceId** is joined with hello ID of hello claim schema entry toofind hello appropriate output claim.</span></span>
- <span data-ttu-id="d5701-518">**TransformationClaimType**是使用的 toogive 的唯一名稱 toothis 輸出。</span><span class="sxs-lookup"><span data-stu-id="d5701-518">**TransformationClaimType** is used toogive a unique name toothis output.</span></span> <span data-ttu-id="d5701-519">這個名稱必須符合預期的 hello 輸出 hello 轉換方法的其中一個。</span><span class="sxs-lookup"><span data-stu-id="d5701-519">This name must match one of hello expected outputs for hello transformation method.</span></span>

### <a name="exceptions-and-restrictions"></a><span data-ttu-id="d5701-520">例外狀況和限制</span><span class="sxs-lookup"><span data-stu-id="d5701-520">Exceptions and restrictions</span></span>

<span data-ttu-id="d5701-521">**SAML NameID 和 UPN:** hello 屬性來源 hello NameID 和 UPN 值與 hello 宣告的允許，轉換會受到限制。</span><span class="sxs-lookup"><span data-stu-id="d5701-521">**SAML NameID and UPN:** hello attributes from which you source hello NameID and UPN values, and hello claims transformations that are permitted, are limited.</span></span>

#### <a name="table-5-attributes-allowed-as-a-data-source-for-saml-nameid"></a><span data-ttu-id="d5701-522">表 5：允許作為 SAML NameID 資料來源的屬性</span><span class="sxs-lookup"><span data-stu-id="d5701-522">Table 5: Attributes allowed as a data source for SAML NameID</span></span>
|<span data-ttu-id="d5701-523">來源</span><span class="sxs-lookup"><span data-stu-id="d5701-523">Source</span></span>|<span data-ttu-id="d5701-524">ID</span><span class="sxs-lookup"><span data-stu-id="d5701-524">ID</span></span>|<span data-ttu-id="d5701-525">說明</span><span class="sxs-lookup"><span data-stu-id="d5701-525">Description</span></span>|
|-----|-----|-----|
|<span data-ttu-id="d5701-526">User</span><span class="sxs-lookup"><span data-stu-id="d5701-526">User</span></span>|<span data-ttu-id="d5701-527">mail</span><span class="sxs-lookup"><span data-stu-id="d5701-527">mail</span></span>|<span data-ttu-id="d5701-528">電子郵件地址</span><span class="sxs-lookup"><span data-stu-id="d5701-528">Email Address</span></span>|
|<span data-ttu-id="d5701-529">User</span><span class="sxs-lookup"><span data-stu-id="d5701-529">User</span></span>|<span data-ttu-id="d5701-530">userprincipalname</span><span class="sxs-lookup"><span data-stu-id="d5701-530">userprincipalname</span></span>|<span data-ttu-id="d5701-531">使用者主體名稱</span><span class="sxs-lookup"><span data-stu-id="d5701-531">User Principal Name</span></span>|
|<span data-ttu-id="d5701-532">User</span><span class="sxs-lookup"><span data-stu-id="d5701-532">User</span></span>|<span data-ttu-id="d5701-533">onpremisessamaccountname</span><span class="sxs-lookup"><span data-stu-id="d5701-533">onpremisessamaccountname</span></span>|<span data-ttu-id="d5701-534">內部部署的 Sam 帳戶名稱</span><span class="sxs-lookup"><span data-stu-id="d5701-534">On Premises Sam Account Name</span></span>|
|<span data-ttu-id="d5701-535">User</span><span class="sxs-lookup"><span data-stu-id="d5701-535">User</span></span>|<span data-ttu-id="d5701-536">employeeid</span><span class="sxs-lookup"><span data-stu-id="d5701-536">employeeid</span></span>|<span data-ttu-id="d5701-537">員工識別碼</span><span class="sxs-lookup"><span data-stu-id="d5701-537">Employee ID</span></span>|
|<span data-ttu-id="d5701-538">User</span><span class="sxs-lookup"><span data-stu-id="d5701-538">User</span></span>|<span data-ttu-id="d5701-539">extensionattribute1</span><span class="sxs-lookup"><span data-stu-id="d5701-539">extensionattribute1</span></span>|<span data-ttu-id="d5701-540">擴充屬性 1</span><span class="sxs-lookup"><span data-stu-id="d5701-540">Extension Attribute 1</span></span>|
|<span data-ttu-id="d5701-541">User</span><span class="sxs-lookup"><span data-stu-id="d5701-541">User</span></span>|<span data-ttu-id="d5701-542">extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="d5701-542">extensionattribute2</span></span>|<span data-ttu-id="d5701-543">擴充屬性 2</span><span class="sxs-lookup"><span data-stu-id="d5701-543">Extension Attribute 2</span></span>|
|<span data-ttu-id="d5701-544">User</span><span class="sxs-lookup"><span data-stu-id="d5701-544">User</span></span>|<span data-ttu-id="d5701-545">extensionattribute3</span><span class="sxs-lookup"><span data-stu-id="d5701-545">extensionattribute3</span></span>|<span data-ttu-id="d5701-546">擴充屬性 3</span><span class="sxs-lookup"><span data-stu-id="d5701-546">Extension Attribute 3</span></span>|
|<span data-ttu-id="d5701-547">User</span><span class="sxs-lookup"><span data-stu-id="d5701-547">User</span></span>|<span data-ttu-id="d5701-548">extensionattribute4</span><span class="sxs-lookup"><span data-stu-id="d5701-548">extensionattribute4</span></span>|<span data-ttu-id="d5701-549">擴充屬性 4</span><span class="sxs-lookup"><span data-stu-id="d5701-549">Extension Attribute 4</span></span>|
|<span data-ttu-id="d5701-550">User</span><span class="sxs-lookup"><span data-stu-id="d5701-550">User</span></span>|<span data-ttu-id="d5701-551">extensionattribute5</span><span class="sxs-lookup"><span data-stu-id="d5701-551">extensionattribute5</span></span>|<span data-ttu-id="d5701-552">擴充屬性 5</span><span class="sxs-lookup"><span data-stu-id="d5701-552">Extension Attribute 5</span></span>|
|<span data-ttu-id="d5701-553">User</span><span class="sxs-lookup"><span data-stu-id="d5701-553">User</span></span>|<span data-ttu-id="d5701-554">extensionattribute6</span><span class="sxs-lookup"><span data-stu-id="d5701-554">extensionattribute6</span></span>|<span data-ttu-id="d5701-555">擴充屬性 6</span><span class="sxs-lookup"><span data-stu-id="d5701-555">Extension Attribute 6</span></span>|
|<span data-ttu-id="d5701-556">User</span><span class="sxs-lookup"><span data-stu-id="d5701-556">User</span></span>|<span data-ttu-id="d5701-557">extensionattribute7</span><span class="sxs-lookup"><span data-stu-id="d5701-557">extensionattribute7</span></span>|<span data-ttu-id="d5701-558">擴充屬性 7</span><span class="sxs-lookup"><span data-stu-id="d5701-558">Extension Attribute 7</span></span>|
|<span data-ttu-id="d5701-559">User</span><span class="sxs-lookup"><span data-stu-id="d5701-559">User</span></span>|<span data-ttu-id="d5701-560">extensionattribute8</span><span class="sxs-lookup"><span data-stu-id="d5701-560">extensionattribute8</span></span>|<span data-ttu-id="d5701-561">擴充屬性 8</span><span class="sxs-lookup"><span data-stu-id="d5701-561">Extension Attribute 8</span></span>|
|<span data-ttu-id="d5701-562">User</span><span class="sxs-lookup"><span data-stu-id="d5701-562">User</span></span>|<span data-ttu-id="d5701-563">extensionattribute9</span><span class="sxs-lookup"><span data-stu-id="d5701-563">extensionattribute9</span></span>|<span data-ttu-id="d5701-564">擴充屬性 9</span><span class="sxs-lookup"><span data-stu-id="d5701-564">Extension Attribute 9</span></span>|
|<span data-ttu-id="d5701-565">User</span><span class="sxs-lookup"><span data-stu-id="d5701-565">User</span></span>|<span data-ttu-id="d5701-566">extensionattribute10</span><span class="sxs-lookup"><span data-stu-id="d5701-566">extensionattribute10</span></span>|<span data-ttu-id="d5701-567">擴充屬性 10</span><span class="sxs-lookup"><span data-stu-id="d5701-567">Extension Attribute 10</span></span>|
|<span data-ttu-id="d5701-568">User</span><span class="sxs-lookup"><span data-stu-id="d5701-568">User</span></span>|<span data-ttu-id="d5701-569">extensionattribute11</span><span class="sxs-lookup"><span data-stu-id="d5701-569">extensionattribute11</span></span>|<span data-ttu-id="d5701-570">擴充屬性 11</span><span class="sxs-lookup"><span data-stu-id="d5701-570">Extension Attribute 11</span></span>|
|<span data-ttu-id="d5701-571">User</span><span class="sxs-lookup"><span data-stu-id="d5701-571">User</span></span>|<span data-ttu-id="d5701-572">extensionattribute12</span><span class="sxs-lookup"><span data-stu-id="d5701-572">extensionattribute12</span></span>|<span data-ttu-id="d5701-573">擴充屬性 12</span><span class="sxs-lookup"><span data-stu-id="d5701-573">Extension Attribute 12</span></span>|
|<span data-ttu-id="d5701-574">User</span><span class="sxs-lookup"><span data-stu-id="d5701-574">User</span></span>|<span data-ttu-id="d5701-575">extensionattribute13</span><span class="sxs-lookup"><span data-stu-id="d5701-575">extensionattribute13</span></span>|<span data-ttu-id="d5701-576">擴充屬性 13</span><span class="sxs-lookup"><span data-stu-id="d5701-576">Extension Attribute 13</span></span>|
|<span data-ttu-id="d5701-577">User</span><span class="sxs-lookup"><span data-stu-id="d5701-577">User</span></span>|<span data-ttu-id="d5701-578">extensionattribute14</span><span class="sxs-lookup"><span data-stu-id="d5701-578">extensionattribute14</span></span>|<span data-ttu-id="d5701-579">擴充屬性 14</span><span class="sxs-lookup"><span data-stu-id="d5701-579">Extension Attribute 14</span></span>|
|<span data-ttu-id="d5701-580">User</span><span class="sxs-lookup"><span data-stu-id="d5701-580">User</span></span>|<span data-ttu-id="d5701-581">extensionattribute15</span><span class="sxs-lookup"><span data-stu-id="d5701-581">extensionattribute15</span></span>|<span data-ttu-id="d5701-582">擴充屬性 15</span><span class="sxs-lookup"><span data-stu-id="d5701-582">Extension Attribute 15</span></span>|

#### <a name="table-6-transformation-methods-allowed-for-saml-nameid"></a><span data-ttu-id="d5701-583">表 6：允許 SAML NameID 使用的轉換方法</span><span class="sxs-lookup"><span data-stu-id="d5701-583">Table 6: Transformation methods allowed for SAML NameID</span></span>
|<span data-ttu-id="d5701-584">TransformationMethod</span><span class="sxs-lookup"><span data-stu-id="d5701-584">TransformationMethod</span></span>|<span data-ttu-id="d5701-585">限制</span><span class="sxs-lookup"><span data-stu-id="d5701-585">Restrictions</span></span>|
| ----- | ----- |
|<span data-ttu-id="d5701-586">ExtractMailPrefix</span><span class="sxs-lookup"><span data-stu-id="d5701-586">ExtractMailPrefix</span></span>|<span data-ttu-id="d5701-587">None</span><span class="sxs-lookup"><span data-stu-id="d5701-587">None</span></span>|
|<span data-ttu-id="d5701-588">Join</span><span class="sxs-lookup"><span data-stu-id="d5701-588">Join</span></span>|<span data-ttu-id="d5701-589">要聯結的 hello 尾碼必須 hello 資源的租用戶的已驗證的網域。</span><span class="sxs-lookup"><span data-stu-id="d5701-589">hello suffix being joined must be a verified domain of hello resource tenant.</span></span>|

### <a name="custom-signing-key"></a><span data-ttu-id="d5701-590">自訂簽署金鑰</span><span class="sxs-lookup"><span data-stu-id="d5701-590">Custom signing key</span></span>
<span data-ttu-id="d5701-591">宣告對應原則 tootake 效果 toohello 服務主體物件必須指派自訂的簽署金鑰。</span><span class="sxs-lookup"><span data-stu-id="d5701-591">A custom signing key must be assigned toohello service principal object for a claims mapping policy tootake effect.</span></span> <span data-ttu-id="d5701-592">所有簽發的權杖，受到 hello 原則會使用此金鑰簽署。</span><span class="sxs-lookup"><span data-stu-id="d5701-592">All tokens issued that have been impacted by hello policy are signed with this key.</span></span> <span data-ttu-id="d5701-593">應用程式必須使用此金鑰進行簽署的設定的 tooaccept 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="d5701-593">Applications must be configured tooaccept tokens signed with this key.</span></span> <span data-ttu-id="d5701-594">這可確保通知的語彙基元已被修改的 hello hello 建立者的宣告對應的原則。</span><span class="sxs-lookup"><span data-stu-id="d5701-594">This ensures acknowledgment that tokens have been modified by hello creator of hello claims mapping policy.</span></span> <span data-ttu-id="d5701-595">這項確認可防止應用程式使用惡意執行者所建立的宣告對應原則。</span><span class="sxs-lookup"><span data-stu-id="d5701-595">This protects applications from claims mapping policies created by malicious actors.</span></span>

### <a name="cross-tenant-scenarios"></a><span data-ttu-id="d5701-596">跨租用戶案例</span><span class="sxs-lookup"><span data-stu-id="d5701-596">Cross-tenant scenarios</span></span>
<span data-ttu-id="d5701-597">宣告對應原則不會套用 tooguest 使用者。</span><span class="sxs-lookup"><span data-stu-id="d5701-597">Claims mapping policies do not apply tooguest users.</span></span> <span data-ttu-id="d5701-598">如果有 guest 使用者嘗試 tooaccess 應用程式與宣告對應原則指派 tooits 服務主體時，發出 hello 預設的語彙基元 （hello 原則沒有任何影響）。</span><span class="sxs-lookup"><span data-stu-id="d5701-598">If a guest user attempts tooaccess an application with a claims mapping policy assigned tooits service principal, hello default token is issued (hello policy has no effect).</span></span>

## <a name="claims-mapping-policy-assignment"></a><span data-ttu-id="d5701-599">宣告對應原則指派</span><span class="sxs-lookup"><span data-stu-id="d5701-599">Claims mapping policy assignment</span></span>
<span data-ttu-id="d5701-600">宣告對應原則只能指派 tooservice principal 物件。</span><span class="sxs-lookup"><span data-stu-id="d5701-600">Claims mapping policies can only be assigned tooservice principal objects.</span></span>

### <a name="example-claims-mapping-policies"></a><span data-ttu-id="d5701-601">宣告對應原則範例</span><span class="sxs-lookup"><span data-stu-id="d5701-601">Example claims mapping policies</span></span>

<span data-ttu-id="d5701-602">在 Azure AD 中，當您可以為特定的服務主體自訂權杖中所發出的宣告時，許多案例便可能實現。</span><span class="sxs-lookup"><span data-stu-id="d5701-602">In Azure AD, many scenarios are possible when you can customize claims emitted in tokens for specific service principals.</span></span> <span data-ttu-id="d5701-603">在本節中，我們逐步解說，可協助您掌握 toouse hello 如何宣告對應原則類型可為一些常見案例。</span><span class="sxs-lookup"><span data-stu-id="d5701-603">In this section, we walk through a few common scenarios that can help you grasp how toouse hello claims mapping policy type.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="d5701-604">必要條件</span><span class="sxs-lookup"><span data-stu-id="d5701-604">Prerequisites</span></span>
<span data-ttu-id="d5701-605">Hello 遵循範例，在您建立、 更新連結，並刪除服務主體原則。</span><span class="sxs-lookup"><span data-stu-id="d5701-605">In hello following examples, you create, update, link, and delete policies for service principals.</span></span> <span data-ttu-id="d5701-606">如果您是新 tooAzure AD，我們建議您了解 tooget 的 Azure AD 租用戶才能繼續進行這些範例。</span><span class="sxs-lookup"><span data-stu-id="d5701-606">If you are new tooAzure AD, we recommend that you learn about how tooget an Azure AD tenant before you proceed with these examples.</span></span> 

<span data-ttu-id="d5701-607">tooget 啟動，請勿 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d5701-607">tooget started, do hello following steps:</span></span>


1. <span data-ttu-id="d5701-608">下載最新的 hello [Azure AD PowerShell 模組公開預覽版本](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.127)。</span><span class="sxs-lookup"><span data-stu-id="d5701-608">Download hello latest [Azure AD PowerShell Module public preview release](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.127).</span></span>
2.  <span data-ttu-id="d5701-609">執行 hello 連接命令 toosign tooyour Azure AD 系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="d5701-609">Run hello Connect command toosign in tooyour Azure AD admin account.</span></span> <span data-ttu-id="d5701-610">您每次啟動新的工作階段時執行此命令。</span><span class="sxs-lookup"><span data-stu-id="d5701-610">Run this command each time you start a new session.</span></span>
    
     ``` powershell
    Connect-AzureAD -Confirm
    
    ```
3.  <span data-ttu-id="d5701-611">toosee 命令已建立您的組織，執行下列的 hello 中的所有原則。</span><span class="sxs-lookup"><span data-stu-id="d5701-611">toosee all policies that have been created in your organization, run hello following command.</span></span> <span data-ttu-id="d5701-612">我們建議您執行此命令，在 hello 的大部分作業後，下列案例中，預期 toocheck 作為正在建立您的原則。</span><span class="sxs-lookup"><span data-stu-id="d5701-612">We recommend that you run this command after most operations in hello following scenarios, toocheck that your policies are being created as expected.</span></span>
   
    ``` powershell
        Get-AzureADPolicy
    
    ```
#### <a name="example-create-and-assign-a-policy-tooomit-hello-basic-claims-from-tokens-issued-tooa-service-principal"></a><span data-ttu-id="d5701-613">範例： 建立及指派原則 tooomit hello 基本的宣告簽發的權杖 tooa 服務主體。</span><span class="sxs-lookup"><span data-stu-id="d5701-613">Example: Create and assign a policy tooomit hello basic claims from tokens issued tooa service principal.</span></span>
<span data-ttu-id="d5701-614">在此範例中，您建立的原則移除發行的權杖 toolinked hello 基本的宣告集，服務主體。</span><span class="sxs-lookup"><span data-stu-id="d5701-614">In this example, you create a policy that removes hello basic claim set from tokens issued toolinked service principals.</span></span>


1. <span data-ttu-id="d5701-615">建立宣告對應原則。</span><span class="sxs-lookup"><span data-stu-id="d5701-615">Create a claims mapping policy.</span></span> <span data-ttu-id="d5701-616">此原則，連結的 toospecific 服務主體，會移除語彙基元中的 hello 基本的宣告集。</span><span class="sxs-lookup"><span data-stu-id="d5701-616">This policy, linked toospecific service principals, removes hello basic claim set from tokens.</span></span>
    1. <span data-ttu-id="d5701-617">toocreate hello 原則，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="d5701-617">toocreate hello policy, run this command:</span></span> 
    
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"false"}}') -DisplayName "OmitBasicClaims” -Type "ClaimsMappingPolicy"
    ```
    2. <span data-ttu-id="d5701-618">toosee 您新的原則和 tooget hello 原則 ObjectId，執行 hello，下列命令：</span><span class="sxs-lookup"><span data-stu-id="d5701-618">toosee your new policy, and tooget hello policy ObjectId, run hello following command:</span></span>
    
     ``` powershell
    Get-AzureADPolicy
    ```
2.  <span data-ttu-id="d5701-619">指派 hello 原則 tooyour 服務主體。</span><span class="sxs-lookup"><span data-stu-id="d5701-619">Assign hello policy tooyour service principal.</span></span> <span data-ttu-id="d5701-620">您也需要 tooget hello 您的服務主體的 ObjectId。</span><span class="sxs-lookup"><span data-stu-id="d5701-620">You also need tooget hello ObjectId of your service principal.</span></span> 
    1.  <span data-ttu-id="d5701-621">toosee 貴組織的所有服務主體中，您可以查詢 Graph。</span><span class="sxs-lookup"><span data-stu-id="d5701-621">toosee all your organization's service principals, you can query Microsoft Graph.</span></span> <span data-ttu-id="d5701-622">或者，在 Azure AD Graph 總管 中，登入 tooyour Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d5701-622">Or, in Azure AD Graph Explorer, sign in tooyour Azure AD account.</span></span>
    2.  <span data-ttu-id="d5701-623">當您擁有 hello ObjectId 的下列命令您服務主體時，執行 hello:</span><span class="sxs-lookup"><span data-stu-id="d5701-623">When you have hello ObjectId of your service principal, run hello following command:</span></span>  
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
#### <a name="example-create-and-assign-a-policy-tooinclude-hello-employeeid-and-tenantcountry-as-claims-in-tokens-issued-tooa-service-principal"></a><span data-ttu-id="d5701-624">範例： 建立及指派原則 tooinclude hello EmployeeID 和 TenantCountry 權杖中的宣告發出 tooa 服務主體。</span><span class="sxs-lookup"><span data-stu-id="d5701-624">Example: Create and assign a policy tooinclude hello EmployeeID and TenantCountry as claims in tokens issued tooa service principal.</span></span>
<span data-ttu-id="d5701-625">在此範例中，您建立原則，將 hello EmployeeID 和 TenantCountry tootokens 發出 toolinked 服務主體。</span><span class="sxs-lookup"><span data-stu-id="d5701-625">In this example, you create a policy that adds hello EmployeeID and TenantCountry tootokens issued toolinked service principals.</span></span> <span data-ttu-id="d5701-626">為 SAML 權杖和 Jwt 中的 hello 名稱宣告類型，就會發出 hello EmployeeID。</span><span class="sxs-lookup"><span data-stu-id="d5701-626">hello EmployeeID is emitted as hello name claim type in both SAML tokens and JWTs.</span></span> <span data-ttu-id="d5701-627">以宣告方式 hello 國家 （地區） 在 SAML 權杖和 Jwt 的型別，就會發出 hello TenantCountry。</span><span class="sxs-lookup"><span data-stu-id="d5701-627">hello TenantCountry is emitted as hello country claim type in both SAML tokens and JWTs.</span></span> <span data-ttu-id="d5701-628">在此範例中，我們將繼續 tooinclude hello 基本宣告 hello 語彙基元中設定。</span><span class="sxs-lookup"><span data-stu-id="d5701-628">In this example, we continue tooinclude hello basic claims set in hello tokens.</span></span>

1. <span data-ttu-id="d5701-629">建立宣告對應原則。</span><span class="sxs-lookup"><span data-stu-id="d5701-629">Create a claims mapping policy.</span></span> <span data-ttu-id="d5701-630">此原則，連結的 toospecific 服務主體加入 hello EmployeeID 和 TenantCountry 宣告 tootokens。</span><span class="sxs-lookup"><span data-stu-id="d5701-630">This policy, linked toospecific service principals, adds hello EmployeeID and TenantCountry claims tootokens.</span></span>
    1. <span data-ttu-id="d5701-631">toocreate hello 原則，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="d5701-631">toocreate hello policy, run this command:</span></span>  
     
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema": [{"Source":"user","ID":"employeeid","SamlClaimType":"http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name","JwtClaimType":"name"},{"Source":"company","ID":" tenantcountry ","SamlClaimType":" http://schemas.xmlsoap.org/ws/2005/05/identity/claims/country ","JwtClaimType":"country"}]}}') -DisplayName "ExtraClaimsExample” -Type "ClaimsMappingPolicy"
    ```
    
    2. <span data-ttu-id="d5701-632">toosee 您新的原則和 tooget hello 原則 ObjectId，執行 hello，下列命令：</span><span class="sxs-lookup"><span data-stu-id="d5701-632">toosee your new policy, and tooget hello policy ObjectId, run hello following command:</span></span>
     
     ``` powershell  
    Get-AzureADPolicy
    ```
2.  <span data-ttu-id="d5701-633">指派 hello 原則 tooyour 服務主體。</span><span class="sxs-lookup"><span data-stu-id="d5701-633">Assign hello policy tooyour service principal.</span></span> <span data-ttu-id="d5701-634">您也需要 tooget hello 您的服務主體的 ObjectId。</span><span class="sxs-lookup"><span data-stu-id="d5701-634">You also need tooget hello ObjectId of your service principal.</span></span> 
    1.  <span data-ttu-id="d5701-635">toosee 貴組織的所有服務主體中，您可以查詢 Graph。</span><span class="sxs-lookup"><span data-stu-id="d5701-635">toosee all your organization's service principals, you can query Microsoft Graph.</span></span> <span data-ttu-id="d5701-636">或者，在 Azure AD Graph 總管 中，登入 tooyour Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d5701-636">Or, in Azure AD Graph Explorer, sign in tooyour Azure AD account.</span></span>
    2.  <span data-ttu-id="d5701-637">當您擁有 hello ObjectId 的下列命令您服務主體時，執行 hello:</span><span class="sxs-lookup"><span data-stu-id="d5701-637">When you have hello ObjectId of your service principal, run hello following command:</span></span>  
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
#### <a name="example-create-and-assign-a-policy-that-uses-a-claims-transformation-in-tokens-issued-tooa-service-principal"></a><span data-ttu-id="d5701-638">範例： 建立及發行的權杖 tooa 服務主體中使用宣告轉換原則指派。</span><span class="sxs-lookup"><span data-stu-id="d5701-638">Example: Create and assign a policy that uses a claims transformation in tokens issued tooa service principal.</span></span>
<span data-ttu-id="d5701-639">在此範例中，您建立原則，它會發出 tooJWTs 發出 toolinked 服務主體的自訂宣告"JoinedData"。</span><span class="sxs-lookup"><span data-stu-id="d5701-639">In this example, you create a policy that emits a custom claim “JoinedData” tooJWTs issued toolinked service principals.</span></span> <span data-ttu-id="d5701-640">這個宣告包含聯結 hello 資料儲存在 「.sandbox"hello 使用者物件上的 hello extensionattribute1 屬性中建立的值。</span><span class="sxs-lookup"><span data-stu-id="d5701-640">This claim contains a value created by joining hello data stored in hello extensionattribute1 attribute on hello user object with “.sandbox”.</span></span> <span data-ttu-id="d5701-641">在此範例中，我們會排除 hello 基本 hello 語彙基元中設定的宣告。</span><span class="sxs-lookup"><span data-stu-id="d5701-641">In this example, we exclude hello basic claims set in hello tokens.</span></span>


1. <span data-ttu-id="d5701-642">建立宣告對應原則。</span><span class="sxs-lookup"><span data-stu-id="d5701-642">Create a claims mapping policy.</span></span> <span data-ttu-id="d5701-643">此原則，連結的 toospecific 服務主體加入 hello EmployeeID 和 TenantCountry 宣告 tootokens。</span><span class="sxs-lookup"><span data-stu-id="d5701-643">This policy, linked toospecific service principals, adds hello EmployeeID and TenantCountry claims tootokens.</span></span>
    1. <span data-ttu-id="d5701-644">toocreate hello 原則，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="d5701-644">toocreate hello policy, run this command:</span></span> 
     
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema":[{"Source":"user","ID":"extensionattribute1"},{"Source":"transformation","ID":"DataJoin","TransformationId":"JoinTheData","JwtClaimType":"JoinedData"}],"ClaimsTransformation":[{"ID":"JoinTheData","TransformationMethod":"Join","InputClaims":[{"ClaimTypeReferenceId":"extensionattribute1","TransformationClaimType":"string1"}], "InputParameters": [{"Id":"string2","Value":"sandbox"},{"Id":"separator","Value":"."}],"OutputClaims":[{"ClaimTypeReferenceId":"DataJoin","TransformationClaimType":"outputClaim"}]}]}}') -DisplayName "TransformClaimsExample” -Type "ClaimsMappingPolicy"
    ```
    
    2. <span data-ttu-id="d5701-645">toosee 您新的原則和 tooget hello 原則 ObjectId，執行 hello，下列命令：</span><span class="sxs-lookup"><span data-stu-id="d5701-645">toosee your new policy, and tooget hello policy ObjectId, run hello following command:</span></span> 
     
     ``` powershell
    Get-AzureADPolicy
    ```
2.  <span data-ttu-id="d5701-646">指派 hello 原則 tooyour 服務主體。</span><span class="sxs-lookup"><span data-stu-id="d5701-646">Assign hello policy tooyour service principal.</span></span> <span data-ttu-id="d5701-647">您也需要 tooget hello 您的服務主體的 ObjectId。</span><span class="sxs-lookup"><span data-stu-id="d5701-647">You also need tooget hello ObjectId of your service principal.</span></span> 
    1.  <span data-ttu-id="d5701-648">toosee 貴組織的所有服務主體中，您可以查詢 Graph。</span><span class="sxs-lookup"><span data-stu-id="d5701-648">toosee all your organization's service principals, you can query Microsoft Graph.</span></span> <span data-ttu-id="d5701-649">或者，在 Azure AD Graph 總管 中，登入 tooyour Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d5701-649">Or, in Azure AD Graph Explorer, sign in tooyour Azure AD account.</span></span>
    2.  <span data-ttu-id="d5701-650">當您擁有 hello ObjectId 的下列命令您服務主體時，執行 hello:</span><span class="sxs-lookup"><span data-stu-id="d5701-650">When you have hello ObjectId of your service principal, run hello following command:</span></span> 
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
