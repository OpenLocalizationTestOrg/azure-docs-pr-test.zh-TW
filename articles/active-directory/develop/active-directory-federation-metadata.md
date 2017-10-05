---
title: "Azure AD 同盟中繼資料 | Microsoft Docs"
description: "本文說明 Azure Active Directory 針對接受 Azure Active Directory 權杖之服務所發佈的同盟中繼資料文件。"
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: c2d5f80b-aa74-452c-955b-d8eb3ed62652
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ecafb02a6ac13d1c3cd1fe77ef710cd8525e32b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="federation-metadata"></a><span data-ttu-id="954b1-103">同盟中繼資料</span><span class="sxs-lookup"><span data-stu-id="954b1-103">Federation metadata</span></span>
<span data-ttu-id="954b1-104">Azure Active Directory (Azure AD) 會針對服務發佈同盟中繼資料文件，而該服務已設定為接受由 Azure AD 簽發的安全性權杖。</span><span class="sxs-lookup"><span data-stu-id="954b1-104">Azure Active Directory (Azure AD) publishes a federation metadata document for services that is configured to accept the security tokens that Azure AD issues.</span></span> <span data-ttu-id="954b1-105">[Web 服務同盟語言 (WS-Federation) 1.2 版](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) (該說明為[適用於 OASIS 安全性聲明標記語言 (SAML) 的中繼資料 2.0 版 的延伸資訊](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf)) 中說明了同盟中繼資料文件格式。</span><span class="sxs-lookup"><span data-stu-id="954b1-105">The federation metadata document format is described in the [Web Services Federation Language (WS-Federation) Version 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), which extends [Metadata for the OASIS Security Assertion Markup Language (SAML) v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span></span>

## <a name="tenant-specific-and-tenant-independent-metadata-endpoints"></a><span data-ttu-id="954b1-106">租用戶專屬與租用戶獨立中繼資料端點</span><span class="sxs-lookup"><span data-stu-id="954b1-106">Tenant-specific and Tenant-independent metadata endpoints</span></span>
<span data-ttu-id="954b1-107">Azure AD 會發佈租用戶專屬與租用戶獨立端點。</span><span class="sxs-lookup"><span data-stu-id="954b1-107">Azure AD publishes tenant-specific and tenant-independent endpoints.</span></span>

<span data-ttu-id="954b1-108">租用戶專屬端點是專為特定租用戶所設計的。</span><span class="sxs-lookup"><span data-stu-id="954b1-108">Tenant-specific endpoints are designed for a particular tenant.</span></span> <span data-ttu-id="954b1-109">租用戶專屬同盟中繼資料包含租用戶相關資訊，其中包括租用戶專屬簽發者和端點資訊。</span><span class="sxs-lookup"><span data-stu-id="954b1-109">The tenant-specific federation metadata includes information about the tenant, including tenant-specific issuer and endpoint information.</span></span> <span data-ttu-id="954b1-110">限制存取單一租用戶的應用程式會使用租用戶專屬端點。</span><span class="sxs-lookup"><span data-stu-id="954b1-110">Applications that restrict access to a single tenant use tenant-specific endpoints.</span></span>

<span data-ttu-id="954b1-111">租用戶獨立端點會提供通用資訊給所有 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="954b1-111">Tenant-independent endpoints provide information that is common to all Azure AD tenants.</span></span> <span data-ttu-id="954b1-112">本資訊適用裝載於 login.microsoftonline.com  的租用戶，並由所有租用戶共用。</span><span class="sxs-lookup"><span data-stu-id="954b1-112">This information applies to tenants hosted at *login.microsoftonline.com* and is shared across tenants.</span></span> <span data-ttu-id="954b1-113">建議多租用戶應用程式使用租用戶獨立端點，因為它們並不與任何特定租用戶相關聯。</span><span class="sxs-lookup"><span data-stu-id="954b1-113">Tenant-independent endpoints are recommended for multi-tenant applications, since they are not associated with any particular tenant.</span></span>

## <a name="federation-metadata-endpoints"></a><span data-ttu-id="954b1-114">同盟中繼資料端點</span><span class="sxs-lookup"><span data-stu-id="954b1-114">Federation metadata endpoints</span></span>
<span data-ttu-id="954b1-115">Azure AD 會在 `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`發佈同盟中繼資料。</span><span class="sxs-lookup"><span data-stu-id="954b1-115">Azure AD publishes federation metadata at `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span>

<span data-ttu-id="954b1-116">若為**租用戶專屬端點**，`TenantDomainName` 可以是下列其中一種類型：</span><span class="sxs-lookup"><span data-stu-id="954b1-116">For **tenant-specific endpoints**, the `TenantDomainName` can be one of the following types:</span></span>

* <span data-ttu-id="954b1-117">Azure AD 租用戶已註冊的網域名稱，例如： `contoso.onmicrosoft.com`。</span><span class="sxs-lookup"><span data-stu-id="954b1-117">A registered domain name of an Azure AD tenant, such as: `contoso.onmicrosoft.com`.</span></span>
* <span data-ttu-id="954b1-118">網域的不可變租用戶識別碼，例如 `72f988bf-86f1-41af-91ab-2d7cd011db45`。</span><span class="sxs-lookup"><span data-stu-id="954b1-118">The immutable tenant ID of the domain, such as `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span></span>

<span data-ttu-id="954b1-119">若為**租用戶獨立端點**，`TenantDomainName` 是 `common`。</span><span class="sxs-lookup"><span data-stu-id="954b1-119">For **tenant-independent endpoints**, the `TenantDomainName` is `common`.</span></span> <span data-ttu-id="954b1-120">本文件只列出通用於所有 Azure AD 租用戶 (裝載於 login.microsoftonline.com) 的同盟中繼資料項目。</span><span class="sxs-lookup"><span data-stu-id="954b1-120">This document lists only the Federation Metadata elements that are common to all Azure AD tenants that are hosted at login.microsoftonline.com.</span></span>

<span data-ttu-id="954b1-121">例如，租用戶專屬端點可能是 `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`。</span><span class="sxs-lookup"><span data-stu-id="954b1-121">For example, a tenant-specific endpoint might be `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span> <span data-ttu-id="954b1-122">租用戶獨立端點是 [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml)。</span><span class="sxs-lookup"><span data-stu-id="954b1-122">The tenant-independent endpoint is [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span></span> <span data-ttu-id="954b1-123">您可以在瀏覽器中輸入此 URL 以檢視同盟中繼資料文件。</span><span class="sxs-lookup"><span data-stu-id="954b1-123">You can view the federation metadata document by typing this URL in a browser.</span></span>

## <a name="contents-of-federation-metadata"></a><span data-ttu-id="954b1-124">同盟中繼資料內容</span><span class="sxs-lookup"><span data-stu-id="954b1-124">Contents of federation Metadata</span></span>
<span data-ttu-id="954b1-125">以下小節提供使用 Azure AD 所簽發之權杖的服務所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="954b1-125">The following section provides information needed by services that consume the tokens issued by Azure AD.</span></span>

### <a name="entity-id"></a><span data-ttu-id="954b1-126">實體識別碼</span><span class="sxs-lookup"><span data-stu-id="954b1-126">Entity ID</span></span>
<span data-ttu-id="954b1-127">`EntityDescriptor` 項目包含 `EntityID` 屬性。</span><span class="sxs-lookup"><span data-stu-id="954b1-127">The `EntityDescriptor` element contains an `EntityID` attribute.</span></span> <span data-ttu-id="954b1-128">`EntityID` 屬性的值代表簽發者 (也就是簽發權杖的 Security Token Service (STS))。</span><span class="sxs-lookup"><span data-stu-id="954b1-128">The value of the `EntityID` attribute represents the issuer, that is, the security token service (STS) that issued the token.</span></span> <span data-ttu-id="954b1-129">請務必在收到權杖時驗證簽發者。</span><span class="sxs-lookup"><span data-stu-id="954b1-129">It is important to validate the issuer when you receive a token.</span></span>

<span data-ttu-id="954b1-130">下列中繼資料說明了含有 `EntityID` 項目的範例租用戶專屬 `EntityDescriptor` 項目。</span><span class="sxs-lookup"><span data-stu-id="954b1-130">The following metadata shows a sample tenant-specific `EntityDescriptor` element with an `EntityID` element.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="_b827a749-cfcb-46b3-ab8b-9f6d14a1294b"
entityID="https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db45/">
```
<span data-ttu-id="954b1-131">您可以使用租用戶識別碼來取代租用戶獨立端點中的租用戶識別碼，以建立租用戶特定的 `EntityID` 值。</span><span class="sxs-lookup"><span data-stu-id="954b1-131">You can replace the tenant ID in the tenant-independent endpoint with your tenant ID to create a tenant-specific `EntityID` value.</span></span> <span data-ttu-id="954b1-132">產生的值會與權杖簽發者相同。</span><span class="sxs-lookup"><span data-stu-id="954b1-132">The resulting value will be the same as the token issuer.</span></span> <span data-ttu-id="954b1-133">這項策略可讓多租用戶應用程式驗證指定租用戶的簽發者。</span><span class="sxs-lookup"><span data-stu-id="954b1-133">The strategy allows a multi-tenant application to validate the issuer for a given tenant.</span></span>

<span data-ttu-id="954b1-134">下列中繼資料說明了範例租用戶獨立 `EntityID` 項目。</span><span class="sxs-lookup"><span data-stu-id="954b1-134">The following metadata shows a sample tenant-independent `EntityID` element.</span></span> <span data-ttu-id="954b1-135">請注意， `{tenant}` 是常值，而不是預留位置。</span><span class="sxs-lookup"><span data-stu-id="954b1-135">Please note, that the `{tenant}` is a literal, not a placeholder.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="="_0e5bd9d0-49ef-4258-bc15-21ce143b61bd"
entityID="https://sts.windows.net/{tenant}/">
```

### <a name="token-signing-certificates"></a><span data-ttu-id="954b1-136">權杖簽署憑證</span><span class="sxs-lookup"><span data-stu-id="954b1-136">Token signing certificates</span></span>
<span data-ttu-id="954b1-137">當服務接收由 Azure AD 租用戶簽發的權杖時，權杖的簽章必須使用同盟中繼資料文件中發佈的簽署金鑰驗證。</span><span class="sxs-lookup"><span data-stu-id="954b1-137">When a service receives a token that is issued by a Azure AD tenant, the signature of the token must be validated with a signing key that is published in the federation metadata document.</span></span> <span data-ttu-id="954b1-138">同盟中繼資料包含租用戶用於權杖簽署之憑證的公開部分。</span><span class="sxs-lookup"><span data-stu-id="954b1-138">The federation metadata includes the public portion of the certificates that the tenants use for token signing.</span></span> <span data-ttu-id="954b1-139">憑證原始位元組會出現在 `KeyDescriptor` 項目中。</span><span class="sxs-lookup"><span data-stu-id="954b1-139">The certificate raw bytes appear in the `KeyDescriptor` element.</span></span> <span data-ttu-id="954b1-140">當 `use` 屬性值為 `signing` 時，權杖簽署憑證僅能適用於簽署。</span><span class="sxs-lookup"><span data-stu-id="954b1-140">The token signing certificate is valid for signing only when the value of the `use` attribute is `signing`.</span></span>

<span data-ttu-id="954b1-141">Azure AD 所發佈之同盟中繼資料文件可以有多組簽署金鑰 (例如，Azure AD 準備更新簽署憑證時)。</span><span class="sxs-lookup"><span data-stu-id="954b1-141">A federation metadata document published by Azure AD can have multiple signing keys, such as when Azure AD is preparing to update the signing certificate.</span></span> <span data-ttu-id="954b1-142">當同盟中繼資料文件包含多個憑證時，正在驗證權杖的服務應會支援該文件中的所有憑證。</span><span class="sxs-lookup"><span data-stu-id="954b1-142">When a federation metadata document includes more than one certificate, a service that is validating the tokens should support all certificates in the document.</span></span>

<span data-ttu-id="954b1-143">下列中繼資料說明了具有簽署金鑰的範例 `KeyDescriptor` 項目。</span><span class="sxs-lookup"><span data-stu-id="954b1-143">The following metadata shows a sample `KeyDescriptor` element with a signing key.</span></span>

```
<KeyDescriptor use="signing">
<KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
<X509Data>
<X509Certificate>
MIIDPjCCAiqgAwIBAgIQVWmXY/+9RqFA/OG9kFulHDAJBgUrDgMCHQUAMC0xKzApBgNVBAMTImFjY291bnRzLmFjY2Vzc2NvbnRyb2wud2luZG93cy5uZXQwHhcNMTIwNjA3MDcwMDAwWhcNMTQwNjA3MDcwMDAwWjAtMSswKQYDVQQDEyJhY2NvdW50cy5hY2Nlc3Njb250cm9sLndpbmRvd3MubmV0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEArCz8Sn3GGXmikH2MdTeGY1D711EORX/lVXpr+ecGgqfUWF8MPB07XkYuJ54DAuYT318+2XrzMjOtqkT94VkXmxv6dFGhG8YZ8vNMPd4tdj9c0lpvWQdqXtL1TlFRpD/P6UMEigfN0c9oWDg9U7Ilymgei0UXtf1gtcQbc5sSQU0S4vr9YJp2gLFIGK11Iqg4XSGdcI0QWLLkkC6cBukhVnd6BCYbLjTYy3fNs4DzNdemJlxGl8sLexFytBF6YApvSdus3nFXaMCtBGx16HzkK9ne3lobAwL2o79bP4imEGqg+ibvyNmbrwFGnQrBc1jTF9LyQX9q+louxVfHs6ZiVwIDAQABo2IwYDBeBgNVHQEEVzBVgBCxDDsLd8xkfOLKm4Q/SzjtoS8wLTErMCkGA1UEAxMiYWNjb3VudHMuYWNjZXNzY29udHJvbC53aW5kb3dzLm5ldIIQVWmXY/+9RqFA/OG9kFulHDAJBgUrDgMCHQUAA4IBAQAkJtxxm/ErgySlNk69+1odTMP8Oy6L0H17z7XGG3w4TqvTUSWaxD4hSFJ0e7mHLQLQD7oV/erACXwSZn2pMoZ89MBDjOMQA+e6QzGB7jmSzPTNmQgMLA8fWCfqPrz6zgH+1F1gNp8hJY57kfeVPBiyjuBmlTEBsBlzolY9dd/55qqfQk6cgSeCbHCy/RU/iep0+UsRMlSgPNNmqhj5gmN2AFVCN96zF694LwuPae5CeR2ZcVknexOWHYjFM0MgUSw0ubnGl0h9AJgGyhvNGcjQqu9vd1xkupFgaN+f7P3p3EVN5csBg5H94jEcQZT7EKeTiZ6bTrpDAnrr8tDCy8ng
</X509Certificate>
</X509Data>
</KeyInfo>
</KeyDescriptor>
  ```

<span data-ttu-id="954b1-144">`KeyDescriptor` 項目會出現在同盟中繼資料文件中的兩個位置：WS 同盟專屬區段和 SAML 專屬區段。</span><span class="sxs-lookup"><span data-stu-id="954b1-144">The `KeyDescriptor` element appears in two places in the federation metadata document; in the WS-Federation-specific section and the SAML-specific section.</span></span> <span data-ttu-id="954b1-145">發佈在這兩個區段的憑證將會是相同的。</span><span class="sxs-lookup"><span data-stu-id="954b1-145">The certificates published in both sections will be the same.</span></span>

<span data-ttu-id="954b1-146">在 WS 同盟專屬區段中，WS 同盟中繼資料讀取器會從 `RoleDescriptor` 項目中讀取類型為 `SecurityTokenServiceType` 的憑證。</span><span class="sxs-lookup"><span data-stu-id="954b1-146">In the WS-Federation-specific section, a WS-Federation metadata reader would read the certificates from a `RoleDescriptor` element with the `SecurityTokenServiceType` type.</span></span>

<span data-ttu-id="954b1-147">下列中繼資料說明範例 `RoleDescriptor` 項目。</span><span class="sxs-lookup"><span data-stu-id="954b1-147">The following metadata shows a sample `RoleDescriptor` element.</span></span>

```
<RoleDescriptor xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:fed="http://docs.oasis-open.org/wsfed/federation/200706" xsi:type="fed:SecurityTokenServiceType"protocolSupportEnumeration="http://docs.oasis-open.org/wsfed/federation/200706">
```

<span data-ttu-id="954b1-148">在 SAML 專屬區段中，WS 同盟中繼資料讀取器會讀取來自 `IDPSSODescriptor` 項目的憑證。</span><span class="sxs-lookup"><span data-stu-id="954b1-148">In the SAML-specific section, a WS-Federation metadata reader would read the certificates from a `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="954b1-149">下列中繼資料說明範例 `IDPSSODescriptor` 項目。</span><span class="sxs-lookup"><span data-stu-id="954b1-149">The following metadata shows a sample `IDPSSODescriptor` element.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
```
<span data-ttu-id="954b1-150">租用戶專屬與租用戶獨立憑證格式並沒有差異。</span><span class="sxs-lookup"><span data-stu-id="954b1-150">There are no differences in the format of tenant-specific and tenant-independent certificates.</span></span>

### <a name="ws-federation-endpoint-url"></a><span data-ttu-id="954b1-151">WS 同盟端點 URL</span><span class="sxs-lookup"><span data-stu-id="954b1-151">WS-Federation endpoint URL</span></span>
<span data-ttu-id="954b1-152">同盟中繼資料包含 Azure AD 用於 WS-同盟通訊協定中之單一登入和單一登出的 URL。</span><span class="sxs-lookup"><span data-stu-id="954b1-152">The federation metadata includes the URL that is Azure AD uses for single sign-in and single sign-out in WS-Federation protocol.</span></span> <span data-ttu-id="954b1-153">此端點會出現在 `PassiveRequestorEndpoint` 項目中。</span><span class="sxs-lookup"><span data-stu-id="954b1-153">This endpoint appears in the `PassiveRequestorEndpoint` element.</span></span>

<span data-ttu-id="954b1-154">下列中繼資料說明了租用戶專屬端點的範例 `PassiveRequestorEndpoint` 項目。</span><span class="sxs-lookup"><span data-stu-id="954b1-154">The following metadata shows a sample `PassiveRequestorEndpoint` element for a tenant-specific endpoint.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/72f988bf-86f1-41af-91ab-2d7cd011db45/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```
<span data-ttu-id="954b1-155">若為租用戶獨立端點，WS 同盟 URL 會出現在 WS 同盟端點中，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="954b1-155">For the tenant-independent endpoint, the WS-Federation URL appears in the WS-Federation endpoint, as shown in the following sample.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/common/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```

### <a name="saml-protocol-endpoint-url"></a><span data-ttu-id="954b1-156">SAML 通訊協定端點 URL</span><span class="sxs-lookup"><span data-stu-id="954b1-156">SAML protocol endpoint URL</span></span>
<span data-ttu-id="954b1-157">同盟中繼資料包含 Azure AD 用於 SAML 2.0 通訊協定中之單一登入和單一登出的 URL。</span><span class="sxs-lookup"><span data-stu-id="954b1-157">The federation metadata includes the URL that Azure AD uses for single sign-in and single sign-out in SAML 2.0 protocol.</span></span> <span data-ttu-id="954b1-158">這些端點會出現在 `IDPSSODescriptor` 項目中。</span><span class="sxs-lookup"><span data-stu-id="954b1-158">These endpoints appear in the `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="954b1-159">登入和登出 URL 會出現在 `SingleSignOnService` 和 `SingleLogoutService` 項目中。</span><span class="sxs-lookup"><span data-stu-id="954b1-159">The sign-in and sign-out URLs appear in the `SingleSignOnService` and `SingleLogoutService` elements.</span></span>

<span data-ttu-id="954b1-160">下列中繼資料說明了租用戶專屬端點的範例 `PassiveResistorEndpoint` 。</span><span class="sxs-lookup"><span data-stu-id="954b1-160">The following metadata shows a sample `PassiveResistorEndpoint` for a tenant-specific endpoint.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com /saml2" />
  </IDPSSODescriptor>
```

<span data-ttu-id="954b1-161">同樣地，適用於一般 SAML 2.0 通訊協定端點的端點也會發佈在租用戶獨立同盟中繼資料中，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="954b1-161">Similarly the endpoints for the common SAML 2.0 protocol endpoints are published in the tenant-independent federation metadata, as shown in the following sample.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
  </IDPSSODescriptor>
```
