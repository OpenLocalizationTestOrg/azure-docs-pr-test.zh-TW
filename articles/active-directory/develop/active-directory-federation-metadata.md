---
title: "aaaAzure AD 同盟中繼資料 |Microsoft 文件"
description: "本文說明 hello 同盟中繼資料文件的 Azure Active Directory 發行之服務的接受 Azure Active Directory 發出的權杖。"
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
ms.openlocfilehash: 23535bcd5eeb3e9b2e17d89a9b0420fc98bd3895
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="federation-metadata"></a><span data-ttu-id="a7cd0-103">同盟中繼資料</span><span class="sxs-lookup"><span data-stu-id="a7cd0-103">Federation metadata</span></span>
<span data-ttu-id="a7cd0-104">Azure Active Directory (Azure AD) 服務所設定的 Azure AD 會發出 tooaccept hello 安全性權杖，發行同盟中繼資料文件。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-104">Azure Active Directory (Azure AD) publishes a federation metadata document for services that is configured tooaccept hello security tokens that Azure AD issues.</span></span> <span data-ttu-id="a7cd0-105">hello 同盟中繼資料文件格式述 hello [Web 服務同盟語言 (Ws-federation) 1.2 版](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html)，來擴充[hello OASIS 安全性聲明標記語言 (SAML) 的中繼資料v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf)。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-105">hello federation metadata document format is described in hello [Web Services Federation Language (WS-Federation) Version 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), which extends [Metadata for hello OASIS Security Assertion Markup Language (SAML) v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span></span>

## <a name="tenant-specific-and-tenant-independent-metadata-endpoints"></a><span data-ttu-id="a7cd0-106">租用戶專屬與租用戶獨立中繼資料端點</span><span class="sxs-lookup"><span data-stu-id="a7cd0-106">Tenant-specific and Tenant-independent metadata endpoints</span></span>
<span data-ttu-id="a7cd0-107">Azure AD 會發佈租用戶專屬與租用戶獨立端點。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-107">Azure AD publishes tenant-specific and tenant-independent endpoints.</span></span>

<span data-ttu-id="a7cd0-108">租用戶專屬端點是專為特定租用戶所設計的。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-108">Tenant-specific endpoints are designed for a particular tenant.</span></span> <span data-ttu-id="a7cd0-109">hello 租用戶專屬同盟中繼資料包含 hello 租用戶，包括租用戶專屬簽發者和端點資訊的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-109">hello tenant-specific federation metadata includes information about hello tenant, including tenant-specific issuer and endpoint information.</span></span> <span data-ttu-id="a7cd0-110">限制存取 tooa 單一租用戶的應用程式使用租用戶專用端點。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-110">Applications that restrict access tooa single tenant use tenant-specific endpoints.</span></span>

<span data-ttu-id="a7cd0-111">租用戶獨立端點提供常見 tooall Azure AD 租用戶的資訊。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-111">Tenant-independent endpoints provide information that is common tooall Azure AD tenants.</span></span> <span data-ttu-id="a7cd0-112">此資訊適用於裝載在 tootenants *login.microsoftonline.com*並在租用戶之間共用。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-112">This information applies tootenants hosted at *login.microsoftonline.com* and is shared across tenants.</span></span> <span data-ttu-id="a7cd0-113">建議多租用戶應用程式使用租用戶獨立端點，因為它們並不與任何特定租用戶相關聯。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-113">Tenant-independent endpoints are recommended for multi-tenant applications, since they are not associated with any particular tenant.</span></span>

## <a name="federation-metadata-endpoints"></a><span data-ttu-id="a7cd0-114">同盟中繼資料端點</span><span class="sxs-lookup"><span data-stu-id="a7cd0-114">Federation metadata endpoints</span></span>
<span data-ttu-id="a7cd0-115">Azure AD 會在 `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`發佈同盟中繼資料。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-115">Azure AD publishes federation metadata at `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span>

<span data-ttu-id="a7cd0-116">如**租用戶專用端點**，hello`TenantDomainName`可以是下列類型的 hello:</span><span class="sxs-lookup"><span data-stu-id="a7cd0-116">For **tenant-specific endpoints**, hello `TenantDomainName` can be one of hello following types:</span></span>

* <span data-ttu-id="a7cd0-117">Azure AD 租用戶已註冊的網域名稱，例如： `contoso.onmicrosoft.com`。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-117">A registered domain name of an Azure AD tenant, such as: `contoso.onmicrosoft.com`.</span></span>
* <span data-ttu-id="a7cd0-118">不可變的 hello 租用識別碼 hello 網域，例如`72f988bf-86f1-41af-91ab-2d7cd011db45`。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-118">hello immutable tenant ID of hello domain, such as `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span></span>

<span data-ttu-id="a7cd0-119">如**租用戶獨立端點**，hello`TenantDomainName`是`common`。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-119">For **tenant-independent endpoints**, hello `TenantDomainName` is `common`.</span></span> <span data-ttu-id="a7cd0-120">本文件列出只 hello 同盟中繼資料的項目通用 tooall Azure AD 租用戶都會裝載在 login.microsoftonline.com。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-120">This document lists only hello Federation Metadata elements that are common tooall Azure AD tenants that are hosted at login.microsoftonline.com.</span></span>

<span data-ttu-id="a7cd0-121">例如，租用戶專屬端點可能是 `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-121">For example, a tenant-specific endpoint might be `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span> <span data-ttu-id="a7cd0-122">hello 租用戶獨立端點[https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml)。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-122">hello tenant-independent endpoint is [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span></span> <span data-ttu-id="a7cd0-123">您可以輸入此 URL 在瀏覽器中檢視 hello 同盟中繼資料文件。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-123">You can view hello federation metadata document by typing this URL in a browser.</span></span>

## <a name="contents-of-federation-metadata"></a><span data-ttu-id="a7cd0-124">同盟中繼資料內容</span><span class="sxs-lookup"><span data-stu-id="a7cd0-124">Contents of federation Metadata</span></span>
<span data-ttu-id="a7cd0-125">hello 下節提供將 Azure AD 所簽發的 hello 權杖的服務所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-125">hello following section provides information needed by services that consume hello tokens issued by Azure AD.</span></span>

### <a name="entity-id"></a><span data-ttu-id="a7cd0-126">實體識別碼</span><span class="sxs-lookup"><span data-stu-id="a7cd0-126">Entity ID</span></span>
<span data-ttu-id="a7cd0-127">hello`EntityDescriptor`元素包含`EntityID`屬性。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-127">hello `EntityDescriptor` element contains an `EntityID` attribute.</span></span> <span data-ttu-id="a7cd0-128">hello 值 hello`EntityID`屬性代表 hello 簽發者，也就是 hello 安全性語彙基元服務 (STS) 發行的 hello 權杖。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-128">hello value of hello `EntityID` attribute represents hello issuer, that is, hello security token service (STS) that issued hello token.</span></span> <span data-ttu-id="a7cd0-129">當您收到權杖時，很重要的 toovalidate hello 簽發者。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-129">It is important toovalidate hello issuer when you receive a token.</span></span>

<span data-ttu-id="a7cd0-130">hello 下列中繼資料顯示範例租用戶專屬`EntityDescriptor`具有項目`EntityID`項目。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-130">hello following metadata shows a sample tenant-specific `EntityDescriptor` element with an `EntityID` element.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="_b827a749-cfcb-46b3-ab8b-9f6d14a1294b"
entityID="https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db45/">
```
<span data-ttu-id="a7cd0-131">您可以取代 hello 租用戶獨立端點中的 hello 租用戶識別碼與您的租用戶識別碼 toocreate 租用戶專屬`EntityID`值。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-131">You can replace hello tenant ID in hello tenant-independent endpoint with your tenant ID toocreate a tenant-specific `EntityID` value.</span></span> <span data-ttu-id="a7cd0-132">hello 產生的值將 hello 與 hello 權杖簽發者相同。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-132">hello resulting value will be hello same as hello token issuer.</span></span> <span data-ttu-id="a7cd0-133">hello 策略允許特定租用戶的多租用戶應用程式 toovalidate hello 簽發者。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-133">hello strategy allows a multi-tenant application toovalidate hello issuer for a given tenant.</span></span>

<span data-ttu-id="a7cd0-134">hello 下列中繼資料顯示範例租用戶獨立`EntityID`項目。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-134">hello following metadata shows a sample tenant-independent `EntityID` element.</span></span> <span data-ttu-id="a7cd0-135">請注意，該 hello`{tenant}`為常值，而不是預留位置。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-135">Please note, that hello `{tenant}` is a literal, not a placeholder.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="="_0e5bd9d0-49ef-4258-bc15-21ce143b61bd"
entityID="https://sts.windows.net/{tenant}/">
```

### <a name="token-signing-certificates"></a><span data-ttu-id="a7cd0-136">權杖簽署憑證</span><span class="sxs-lookup"><span data-stu-id="a7cd0-136">Token signing certificates</span></span>
<span data-ttu-id="a7cd0-137">當服務收到 Azure AD 租用戶所發出的權杖時，hello hello token 的簽章必須以驗證 hello 同盟中繼資料文件中已發行的簽署金鑰。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-137">When a service receives a token that is issued by a Azure AD tenant, hello signature of hello token must be validated with a signing key that is published in hello federation metadata document.</span></span> <span data-ttu-id="a7cd0-138">hello 同盟中繼資料包含 hello 的 hello hello 租用戶用於權杖簽署的憑證的公開部分。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-138">hello federation metadata includes hello public portion of hello certificates that hello tenants use for token signing.</span></span> <span data-ttu-id="a7cd0-139">hello 憑證未經處理位元組會出現在 hello`KeyDescriptor`項目。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-139">hello certificate raw bytes appear in hello `KeyDescriptor` element.</span></span> <span data-ttu-id="a7cd0-140">hello 權杖簽署憑證是有效的簽章只當 hello 值 hello`use`屬性是`signing`。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-140">hello token signing certificate is valid for signing only when hello value of hello `use` attribute is `signing`.</span></span>

<span data-ttu-id="a7cd0-141">Azure AD 所發行的同盟中繼資料文件可以有多個簽署金鑰的詳細資訊，例如 Azure AD 準備 tooupdate hello 簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-141">A federation metadata document published by Azure AD can have multiple signing keys, such as when Azure AD is preparing tooupdate hello signing certificate.</span></span> <span data-ttu-id="a7cd0-142">當同盟中繼資料文件包含一個以上的憑證時，驗證 hello 權杖的服務應 hello 文件中支援的所有憑證。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-142">When a federation metadata document includes more than one certificate, a service that is validating hello tokens should support all certificates in hello document.</span></span>

<span data-ttu-id="a7cd0-143">hello 下列中繼資料顯示範例`KeyDescriptor`具有簽署金鑰的項目。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-143">hello following metadata shows a sample `KeyDescriptor` element with a signing key.</span></span>

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

<span data-ttu-id="a7cd0-144">hello`KeyDescriptor`元素會出現在兩個地方 hello 同盟中繼資料文件; hello WS-同盟專用區段和 hello SAML 專用區段中。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-144">hello `KeyDescriptor` element appears in two places in hello federation metadata document; in hello WS-Federation-specific section and hello SAML-specific section.</span></span> <span data-ttu-id="a7cd0-145">在這兩個區段中發行的 hello 憑證將 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-145">hello certificates published in both sections will be hello same.</span></span>

<span data-ttu-id="a7cd0-146">在 hello WS-同盟專用區段中，WS-同盟中繼資料讀取器會讀取來自 hello 憑證`RoleDescriptor`元素與 hello`SecurityTokenServiceType`型別。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-146">In hello WS-Federation-specific section, a WS-Federation metadata reader would read hello certificates from a `RoleDescriptor` element with hello `SecurityTokenServiceType` type.</span></span>

<span data-ttu-id="a7cd0-147">hello 下列中繼資料顯示範例`RoleDescriptor`項目。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-147">hello following metadata shows a sample `RoleDescriptor` element.</span></span>

```
<RoleDescriptor xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:fed="http://docs.oasis-open.org/wsfed/federation/200706" xsi:type="fed:SecurityTokenServiceType"protocolSupportEnumeration="http://docs.oasis-open.org/wsfed/federation/200706">
```

<span data-ttu-id="a7cd0-148">在 hello SAML 專用區段中，WS-同盟中繼資料讀取器會讀取來自 hello 憑證`IDPSSODescriptor`項目。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-148">In hello SAML-specific section, a WS-Federation metadata reader would read hello certificates from a `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="a7cd0-149">hello 下列中繼資料顯示範例`IDPSSODescriptor`項目。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-149">hello following metadata shows a sample `IDPSSODescriptor` element.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
```
<span data-ttu-id="a7cd0-150">有一些 hello 租用戶專用和租用戶獨立憑證的格式沒有差異。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-150">There are no differences in hello format of tenant-specific and tenant-independent certificates.</span></span>

### <a name="ws-federation-endpoint-url"></a><span data-ttu-id="a7cd0-151">WS 同盟端點 URL</span><span class="sxs-lookup"><span data-stu-id="a7cd0-151">WS-Federation endpoint URL</span></span>
<span data-ttu-id="a7cd0-152">hello 同盟中繼資料包含 URL 是 Azure AD 用於單一登入和單一登出 WS-同盟通訊協定中的 hello。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-152">hello federation metadata includes hello URL that is Azure AD uses for single sign-in and single sign-out in WS-Federation protocol.</span></span> <span data-ttu-id="a7cd0-153">此端點會出現在 hello`PassiveRequestorEndpoint`項目。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-153">This endpoint appears in hello `PassiveRequestorEndpoint` element.</span></span>

<span data-ttu-id="a7cd0-154">hello 下列中繼資料顯示範例`PassiveRequestorEndpoint`租用戶專用端點項目。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-154">hello following metadata shows a sample `PassiveRequestorEndpoint` element for a tenant-specific endpoint.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/72f988bf-86f1-41af-91ab-2d7cd011db45/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```
<span data-ttu-id="a7cd0-155">Hello 租用戶獨立端點，hello WS-同盟 URL 會出現在 hello WS-同盟端點 hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-155">For hello tenant-independent endpoint, hello WS-Federation URL appears in hello WS-Federation endpoint, as shown in hello following sample.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/common/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```

### <a name="saml-protocol-endpoint-url"></a><span data-ttu-id="a7cd0-156">SAML 通訊協定端點 URL</span><span class="sxs-lookup"><span data-stu-id="a7cd0-156">SAML protocol endpoint URL</span></span>
<span data-ttu-id="a7cd0-157">hello 同盟中繼資料包含 Azure AD 用於單一登入和單一登出 SAML 2.0 通訊協定中的 hello URL。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-157">hello federation metadata includes hello URL that Azure AD uses for single sign-in and single sign-out in SAML 2.0 protocol.</span></span> <span data-ttu-id="a7cd0-158">這些端點會出現在 hello`IDPSSODescriptor`項目。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-158">These endpoints appear in hello `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="a7cd0-159">hello 登入和登出 Url 會出現在 hello`SingleSignOnService`和`SingleLogoutService`項目。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-159">hello sign-in and sign-out URLs appear in hello `SingleSignOnService` and `SingleLogoutService` elements.</span></span>

<span data-ttu-id="a7cd0-160">hello 下列中繼資料顯示範例`PassiveResistorEndpoint`租用戶專用端點。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-160">hello following metadata shows a sample `PassiveResistorEndpoint` for a tenant-specific endpoint.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com /saml2" />
  </IDPSSODescriptor>
```

<span data-ttu-id="a7cd0-161">同樣地 hello hello 通用 SAML 2.0 通訊協定端點的端點會發佈在 hello 租用戶獨立同盟中繼資料，hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="a7cd0-161">Similarly hello endpoints for hello common SAML 2.0 protocol endpoints are published in hello tenant-independent federation metadata, as shown in hello following sample.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
  </IDPSSODescriptor>
```
