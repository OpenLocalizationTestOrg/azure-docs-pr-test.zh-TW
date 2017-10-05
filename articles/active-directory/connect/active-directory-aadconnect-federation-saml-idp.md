---
title: "Azure AD Connect：使用 SAML 2.0 識別提供者來進行單一登入 | Microsoft Docs"
description: "本主題描述如何使用 SAML 2.0 相容 Idp 來進行單一登入。"
services: active-directory
author: billmath
manager: femila
ms.custom: it-pro
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 048697f87383662506fb851bb3ea510c2cddf043
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
#  <a name="use-a-saml-20-identity-provider-idp-for-single-sign-on"></a><span data-ttu-id="8a8a8-103">使用 SAML 2.0 識別提供者 (IdP) 來進行單一登入</span><span class="sxs-lookup"><span data-stu-id="8a8a8-103">Use a SAML 2.0 Identity Provider (IdP) for Single Sign On</span></span>

<span data-ttu-id="8a8a8-104">本主題所含的資訊是關於使用 SAML 2.0 相容 SP-Lite 設定檔型識別提供者來作為慣用的 Security Token Service (STS)/識別提供者。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-104">This topic contains information on using a SAML 2.0 compliant SP-Lite profile based Identity Provider as the preferred Security Token Service (STS) / identity provider.</span></span> <span data-ttu-id="8a8a8-105">在已有內部部署的使用者目錄和密碼存放區並可使用 SAML 2.0 來加以存取時，這種做法非常實用。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-105">This is useful where you already have a user directory and password store on-premises that can be accessed using SAML 2.0.</span></span> <span data-ttu-id="8a8a8-106">您可以使用這個現有的使用者目錄來登入 Office 365 和其他受到 Azure AD 保護的資源。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-106">This existing user directory can be used for sign-on to Office 365 and other Azure AD-secured resources.</span></span> <span data-ttu-id="8a8a8-107">SAML 2.0 SP-Lite 設定檔是以廣為使用的安全性聲明標記語言 (SAML) 同盟身分識別標準作為基礎，以提供登入和屬性交換架構。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-107">The SAML 2.0 SP-Lite profile is based on the widely used Security Assertion Markup Language (SAML) federated identity standard to provide a sign-on and attribute exchange framework.</span></span>

>[!NOTE]
><span data-ttu-id="8a8a8-108">如需已通過測試可與 Azure AD 搭配使用的第 3 方 Idp 清單，請參閱 [Azure AD 同盟相容性清單](active-directory-aadconnect-federation-compatibility.md)</span><span class="sxs-lookup"><span data-stu-id="8a8a8-108">For a list of 3rd party Idps that have been tested for use with Azure AD see the [Azure AD federation compatibility list](active-directory-aadconnect-federation-compatibility.md)</span></span>

<span data-ttu-id="8a8a8-109">Microsoft 藉由整合 Microsoft 雲端服務 (例如 Office 365) 和您已正確設定的 SAML 2.0 設定檔型 IdP，來支援此登入體驗。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-109">Microsoft supports this sign-on experience as the integration of a Microsoft cloud service, such as Office 365, with your properly configured SAML 2.0 profile based IdP.</span></span> <span data-ttu-id="8a8a8-110">SAML 2.0 識別提供者是第三方產品，因此 Microsoft 不支援與這些識別提供者有關的部署、設定和疑難排解最佳做法。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-110">SAML 2.0 identity providers are third-party products and therefore Microsoft does not provide support for the deployment, configuration, troubleshooting best practices regarding them.</span></span> <span data-ttu-id="8a8a8-111">與 SAML 2.0 識別提供者的整合在完成適當設定後，您可以使用 Microsoft 連線分析程式工具對整合結果進行測試，以了解所做的設定是否適當，詳情請見下面說明。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-111">Once properly configured, the integration with the SAML 2.0 identity provider can be tested for proper configuration by using the Microsoft Connectivity Analyzer Tool which is described in more detail below.</span></span> <span data-ttu-id="8a8a8-112">如需 SAML 2.0 SP-Lite 設定檔型識別提供者的詳細資訊，請向提供此識別提供者的組織詢問。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-112">For more information about your SAML 2.0 SP-Lite profile based identity provider, ask the organization that supplied it.</span></span>

>[!IMPORTANT]
><span data-ttu-id="8a8a8-113">在此登入案例中，只有一小部分的用戶端可與 SAML 2.0 識別提供者搭配使用，這些用戶端包括：</span><span class="sxs-lookup"><span data-stu-id="8a8a8-113">Only a limited set of clients are available in this sign-on scenario with SAML 2.0 identity providers, this includes:</span></span>

>- <span data-ttu-id="8a8a8-114">Web 型用戶端，例如 Outlook Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="8a8a8-114">Web-based clients such as Outlook Web Access and SharePoint Online</span></span>
- <span data-ttu-id="8a8a8-115">豐富型電子郵件用戶端，其使用基本驗證和受支援的 Exchange 存取方法 (例如 IMAP、POP、Active Sync、MAPI 等) (必須有增強型用戶端通訊協定端點才能部署)，這些用戶端包括：</span><span class="sxs-lookup"><span data-stu-id="8a8a8-115">Email-rich clients that use basic authentication and a supported Exchange access method such as IMAP, POP, Active Sync, MAPI, etc. (the Enhanced Client Protocol end point is required to be deployed), including:</span></span>
    - <span data-ttu-id="8a8a8-116">Microsoft Outlook 2010/Outlook 2013/Outlook 2016、Apple iPhone (各種 iOS 版本)</span><span class="sxs-lookup"><span data-stu-id="8a8a8-116">Microsoft Outlook 2010/Outlook 2013/Outlook 2016, Apple iPhone (various iOS versions)</span></span>
    - <span data-ttu-id="8a8a8-117">各種 Google Android 裝置</span><span class="sxs-lookup"><span data-stu-id="8a8a8-117">Various Google Android Devices</span></span>
    - <span data-ttu-id="8a8a8-118">Windows Phone 7、Windows Phone 7.8 及 Windows Phone 8.0</span><span class="sxs-lookup"><span data-stu-id="8a8a8-118">Windows Phone 7, Windows Phone 7.8, and Windows Phone 8.0</span></span>
    - <span data-ttu-id="8a8a8-119">Windows 8 郵件用戶端和 Windows 8.1 郵件用戶端</span><span class="sxs-lookup"><span data-stu-id="8a8a8-119">Windows 8 Mail Client and Windows 8.1 Mail Client</span></span>
    - <span data-ttu-id="8a8a8-120">Windows 10 郵件用戶端</span><span class="sxs-lookup"><span data-stu-id="8a8a8-120">Windows 10 Mail Client</span></span>

<span data-ttu-id="8a8a8-121">在此登入案例中，其他所有用戶端則無法與 SAML 2.0 識別提供者搭配使用。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-121">All other clients are not available in this sign-on scenario with your SAML 2.0 Identity Provider.</span></span> <span data-ttu-id="8a8a8-122">例如，若服務的設定是使用 SAML 2.0 識別提供者來進行單一登入，則 Lync 2010 桌面用戶端則無法登入該服務。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-122">For example, the Lync 2010 desktop client is not able to login into the service with your SAML 2.0 Identity Provider configured for single sign-on.</span></span>

## <a name="azure-ad-saml-20-protocol-requirements"></a><span data-ttu-id="8a8a8-123">Azure AD SAML 2.0 通訊協定需求</span><span class="sxs-lookup"><span data-stu-id="8a8a8-123">Azure AD SAML 2.0 protocol requirements</span></span>
<span data-ttu-id="8a8a8-124">本主題會詳述為了與 Azure AD 同盟以便能夠登入一或多個 Microsoft 雲端服務 (例如 Office 365)，您的 SAML 2.0 識別提供者所必須實作之通訊協定和訊息格式的需求。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-124">This topic contains detailed requirements on the protocol and message formatting that your SAML 2.0 identity provider must implement to federate with Azure AD to enable sign-on to one or more Microsoft cloud services (such as Office 365).</span></span> <span data-ttu-id="8a8a8-125">此案例所使用之 Microsoft 雲端服務的 SAML 2.0 信賴憑證者 (SP-STS) 是 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-125">The SAML 2.0 relying party (SP-STS) for a Microsoft cloud service used in this scenario is Azure AD.</span></span>

<span data-ttu-id="8a8a8-126">建議您務必要讓 SAML 2.0 識別提供者的輸出訊息盡可能地與所提供的追蹤範例類似。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-126">It is recommended that you ensure your SAML 2.0 identity provider output messages be as similar to the provided sample traces as possible.</span></span> <span data-ttu-id="8a8a8-127">此外，如有可能，也請使用來自所提供之 Azure AD 中繼資料的特定屬性值。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-127">Also, use specific attribute values from the supplied Azure AD metadata where possible.</span></span> <span data-ttu-id="8a8a8-128">在對輸出訊息感到滿意後，您可以使用 Microsoft 連線分析程式來進行測試，方法如下所述。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-128">Once you are happy with your output messages, you can test with the Microsoft Connectivity Analyzer as described below.</span></span>

<span data-ttu-id="8a8a8-129">您可以從此 URL 下載 Azure AD 中繼資料：[https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml](http://https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml)。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-129">The Azure AD metadata can be downloaded from this URL: [https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml](http://https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml).</span></span>
<span data-ttu-id="8a8a8-130">若您是使用中國專屬 Office 365 執行個體的中國客戶，則請使用下列同盟端點：[https://nexus.partner.microsoftonline-p.cn/federationmetadata/saml20/federationmetadata.xml](https://nexus.partner.microsoftonline-p.cn/federationmetadata/saml20/federationmetadata.xml)。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-130">For customers in China using the China-specific instance of Office 365, the following federation endpoint should be used: [https://nexus.partner.microsoftonline-p.cn/federationmetadata/saml20/federationmetadata.xml](https://nexus.partner.microsoftonline-p.cn/federationmetadata/saml20/federationmetadata.xml).</span></span>

## <a name="saml-protocol-requirements"></a><span data-ttu-id="8a8a8-131">SAML 通訊協定需求</span><span class="sxs-lookup"><span data-stu-id="8a8a8-131">SAML protocol requirements</span></span>
<span data-ttu-id="8a8a8-132">本節詳述如何將要求和回應訊息成對放在一起，以協助您正確地設定訊息格式。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-132">This section details how the request and response message pairs are put together in order to help you to format your messages correctly.</span></span>

<span data-ttu-id="8a8a8-133">您可以對 Azure AD 進行設定，讓 Azure AD 與使用 SAML 2.0 SP Lite 設定檔 (具有如下所示的某些特定需求) 的識別提供者搭配運作。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-133">Azure AD can be configured to work with identity providers that use the SAML 2.0 SP Lite profile with some specific requirements as listed below.</span></span> <span data-ttu-id="8a8a8-134">透過使用 SAML 要求和回應訊息範例以及自動和手動的測試，您就可以實現與 Azure AD 的互通性。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-134">Using the sample SAML request and response messages along with automated and manual testing, you can work to achieve interoperability with Azure AD.</span></span>

## <a name="signature-block-requirements"></a><span data-ttu-id="8a8a8-135">簽章區塊需求</span><span class="sxs-lookup"><span data-stu-id="8a8a8-135">Signature block requirements</span></span>
<span data-ttu-id="8a8a8-136">在 SAML 回應訊息內，簽章節點含有訊息本身的數位簽章相關資訊。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-136">Within the SAML Response message the Signature node contains information about the digital signature for the message itself.</span></span> <span data-ttu-id="8a8a8-137">簽章區塊具有下列需求︰</span><span class="sxs-lookup"><span data-stu-id="8a8a8-137">The signature block has the following requirements:</span></span>

1. <span data-ttu-id="8a8a8-138">判斷提示節點本身必須經過簽署</span><span class="sxs-lookup"><span data-stu-id="8a8a8-138">The assertion node itself must be signed</span></span>
2.  <span data-ttu-id="8a8a8-139">必須使用 RSA-sha1 演算法來作為 DigestMethod。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-139">The RSA-sha1 algorithm must be used as the DigestMethod.</span></span> <span data-ttu-id="8a8a8-140">不接受其他數位簽章演算法。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-140">Other digital signature algorithms are not accepted.</span></span>
   `<ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1"/>`
3.  <span data-ttu-id="8a8a8-141">您也可以簽署 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-141">You may also sign the XML document.</span></span> 
4.  <span data-ttu-id="8a8a8-142">Transform Algorithm 必須符合下列範例中的值：`<ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"/>
       <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>`</span><span class="sxs-lookup"><span data-stu-id="8a8a8-142">The Transform Algorithm must match the values in the following sample:    `<ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"/>
       <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>`</span></span>
9.  <span data-ttu-id="8a8a8-143">SignatureMethod Algorithm 必須符合下列範例：`<ds:SignatureMethod Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1"/>`</span><span class="sxs-lookup"><span data-stu-id="8a8a8-143">The SignatureMethod Algorithm must match the following sample:   `<ds:SignatureMethod Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1"/>`</span></span>

## <a name="supported-bindings"></a><span data-ttu-id="8a8a8-144">支援的繫結</span><span class="sxs-lookup"><span data-stu-id="8a8a8-144">Supported bindings</span></span>
<span data-ttu-id="8a8a8-145">繫結就是所需的傳輸相關通訊參數。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-145">Bindings are the transport related communications parameters that are required.</span></span> <span data-ttu-id="8a8a8-146">下列需求適用於繫結</span><span class="sxs-lookup"><span data-stu-id="8a8a8-146">The following requirements apply to the bindings</span></span>

1. <span data-ttu-id="8a8a8-147">HTTPS 是必要的傳輸。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-147">HTTPS is the required transport.</span></span>
2.  <span data-ttu-id="8a8a8-148">在登入期間，Azure AD 需要 HTTP POST 以便提交權杖</span><span class="sxs-lookup"><span data-stu-id="8a8a8-148">Azure AD will require HTTP POST for token submission during logon</span></span>
3.  <span data-ttu-id="8a8a8-149">Azure AD 會對識別提供者的驗證要求使用 HTTP POST，並對識別提供者的登出訊息使用 REDIRECT。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-149">Azure AD will use HTTP POST for the authentication request to the identity provider and REDIRECT for the Logoff message to the identity provider.</span></span>

## <a name="required-attributes"></a><span data-ttu-id="8a8a8-150">必要的屬性</span><span class="sxs-lookup"><span data-stu-id="8a8a8-150">Required attributes</span></span>
<span data-ttu-id="8a8a8-151">下表顯示 SAML 2.0 訊息中特定屬性的需求。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-151">This table shows requirements for specific attributes in the SAML 2.0 message.</span></span>
 
|<span data-ttu-id="8a8a8-152">屬性</span><span class="sxs-lookup"><span data-stu-id="8a8a8-152">Attribute</span></span>|<span data-ttu-id="8a8a8-153">說明</span><span class="sxs-lookup"><span data-stu-id="8a8a8-153">Description</span></span>|
| ----- | ----- |
|<span data-ttu-id="8a8a8-154">NameID</span><span class="sxs-lookup"><span data-stu-id="8a8a8-154">NameID</span></span>|<span data-ttu-id="8a8a8-155">這個判斷提示的值必須與 Azure AD 使用者的 ImmutableID 相同。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-155">The value of this assertion must be the same as the Azure AD user’s ImmutableID.</span></span> <span data-ttu-id="8a8a8-156">此值最多可以有 64 個英數字元。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-156">It can be up to 64 alpha numeric characters.</span></span> <span data-ttu-id="8a8a8-157">若為非 HTML 安全字元就必須編碼，例如，"+" 字元將會顯示為 ".2B"。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-157">Any non HTML safe characters must be encoded, for example a “+” character is shown as “.2B”.</span></span>|
|<span data-ttu-id="8a8a8-158">IDPEmail</span><span class="sxs-lookup"><span data-stu-id="8a8a8-158">IDPEmail</span></span>|<span data-ttu-id="8a8a8-159">在 SAML 回應中，使用者主體名稱 (UPN) 會列示為名稱是 IDPEmail 的項目。這是使用者在 Azure AD/Office 365 中的 UserPrincipalName (UPN)。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-159">The User Principal Name (UPN) is listed in the SAML response as an element with the name IDPEmail This is the user’s UserPrincipalName (UPN) in Azure AD/Office 365.</span></span> <span data-ttu-id="8a8a8-160">此 UPN 會使用電子郵件地址格式。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-160">The UPN is in email address format.</span></span> <span data-ttu-id="8a8a8-161">Windows Office 365 (Azure Active Directory) 中的 UPN 值。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-161">UPN value in Windows Office 365 (Azure Active Directory).</span></span>|
|<span data-ttu-id="8a8a8-162">簽發者</span><span class="sxs-lookup"><span data-stu-id="8a8a8-162">Issuer</span></span>|<span data-ttu-id="8a8a8-163">需要有此屬性來作為識別提供者的 URI。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-163">This is required to be a URI of the identity provider.</span></span> <span data-ttu-id="8a8a8-164">請勿重複使用訊息範例中的 Issuer 屬性。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-164">You should not reuse the Issuer from the sample messages.</span></span> <span data-ttu-id="8a8a8-165">如果您的 Azure AD 租用戶有多個頂層網域，Issuer 必須符合針對每個網域所設定的指定 URI 設定。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-165">If you have multiple top-level domains in your Azure AD tenants the Issuer must match the specified URI setting configured per domain.</span></span>|

>[!IMPORTANT]
><span data-ttu-id="8a8a8-166">針對 SAML 2.0，Azure AD 目前支援下列 NameID 格式的 URI：urn:oasis:names:tc:SAML:2.0:nameid-format:persistent。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-166">Azure AD currently supports the following NameID Format URI for SAML 2.0:urn:oasis:names:tc:SAML:2.0:nameid-format:persistent.</span></span>

## <a name="sample-saml-request-and-response-messages"></a><span data-ttu-id="8a8a8-167">SAML 要求和回應訊息範例</span><span class="sxs-lookup"><span data-stu-id="8a8a8-167">Sample SAML request and response messages</span></span>
<span data-ttu-id="8a8a8-168">下面顯示了一對用來交換登入訊息的要求和回應訊息。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-168">A request and response message pair is shown for the sign-on message exchange.</span></span>
<span data-ttu-id="8a8a8-169">這個要求訊息範例會從 Azure AD 傳送到 SAML 2.0 識別提供者範例。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-169">This is a sample request message that is sent from Azure AD to a sample SAML 2.0 identity provider.</span></span> <span data-ttu-id="8a8a8-170">SAML 2.0 識別提供者範例是設定為使用 SAML-P 通訊協定的 Active Directory 同盟服務 (AD FS)。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-170">The sample SAML 2.0 identity provider is Active Directory Federation Services (AD FS) configured to use SAML-P protocol.</span></span> <span data-ttu-id="8a8a8-171">此範例也已經對其他 SAML 2.0 識別提供者完成互通性測試。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-171">Interoperability testing has also been completed with other SAML 2.0 identity providers.</span></span>

    `<samlp:AuthnRequest xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" ID="_7171b0b2-19f2-4ba2-8f94-24b5e56b7f1e" IssueInstant="2014-01-30T16:18:35Z" Version="2.0" AssertionConsumerServiceIndex="0" >
    <saml:Issuer>urn:federation:MicrosoftOnline</saml:Issuer>
    <samlp:NameIDPolicy Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"/>
    </samlp:AuthnRequest>`

<span data-ttu-id="8a8a8-172">這個回應訊息範例會從 SAML 2.0 相容識別提供者範例傳送到 Azure AD/Office 365。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-172">This is a sample response message that is sent from the sample SAML 2.0 compliant identity provider to Azure AD / Office 365.</span></span>

    `<samlp:Response ID="_592c022f-e85e-4d23-b55b-9141c95cd2a5" Version="2.0" IssueInstant="2014-01-31T15:36:31.357Z" Destination="https://login.microsoftonline.com/login.srf" Consent="urn:oasis:names:tc:SAML:2.0:consent:unspecified" InResponseTo="_049917a6-1183-42fd-a190-1d2cbaf9b144" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">http://WS2012R2-0.contoso.com/adfs/services/trust</Issuer>
    <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
    </samlp:Status>
    <Assertion ID="_7e3c1bcd-f180-4f78-83e1-7680920793aa" IssueInstant="2014-01-31T15:36:31.279Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">
    <Issuer>http://WS2012R2-0.contoso.com/adfs/services/trust</Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      <ds:SignedInfo>
        <ds:CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
        <ds:SignatureMethod Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1" />
        <ds:Reference URI="#_7e3c1bcd-f180-4f78-83e1-7680920793aa">
          <ds:Transforms>
            <ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature" />
            <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
          </ds:Transforms>
          <ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
          <ds:DigestValue>CBn/5YqbheaJP425c0pHva9PhNY=</ds:DigestValue>
        </ds:Reference>
      </ds:SignedInfo>
      <ds:SignatureValue>TciWMyHW2ZODrh/2xrvp5ggmcHBFEd9vrp6DYXp+hZWJzmXMmzwmwS8KNRJKy8H7XqBsdELA1Msqi8I3TmWdnoIRfM/ZAyUppo8suMu6Zw+boE32hoQRnX9EWN/f0vH6zA/YKTzrjca6JQ8gAV1ErwvRWDpyMcwdYCiWALv9ScbkAcebOE1s1JctZ5RBXggdZWrYi72X+I4i6WgyZcIGai/rZ4v2otoWAEHS0y1yh1qT7NDPpl/McDaTGkNU6C+8VfjD78DrUXEcAfKvPgKlKrOMZnD1lCGsViimGY+LSuIdY45MLmyaa5UT4KWph6dA==</ds:SignatureValue>
      <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
        <ds:X509Data>
          <ds:X509Certificate>MIIC7jCCAdagAwIBAgIQRrjsbFPaXIlOG3GTv50fkjANBgkqhkiG9w0BAQsFADAzMTEwLwYDVQQDEyhBREZTIFNpZ25pbmcgLSBXUzIwMTJSMi0wLnN3aW5mb3JtZXIuY29tMB4XDTE0MDEyMDE1MTY0MFoXDTE1MDEyMDE1MTY0MFowMzExMC8GA1UEAxMoQURGUyBTaWduaW5nIC0gV1MyMDEyUjItMC5zd2luZm9ybWVyLmNvbTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAKe+rLVmXy1QwCwZwqgbbp1/+3ZWxd9T/jV0hpLIIWr+LCOHqq8n8beJvlivgLmDJo8f+EITnAxWcsJUvVai/35AhHCUq9tc9sqMp5PWtabAEMb2AU72/QlX/72D2/NbGQq1BWYbqUpgpCZ2nSgvlWDHlCiUo//UGsvfox01kjTFlmqQInsJVfRxF5AcCAwEAATANBgkqhkiG9w0BAQsFAAOCAQEAi8c6C4zaTEc7aQiUgvnGQgCbMZbhUXXLGRpjvFLKaQzkwa9eq7WLJibcSNyGXBa/SfT5wJgsm3TPKgSehGAOTirhcqHheZyvBObAScY7GOT+u9pVYp6raFrc7ez3c+CGHeV/tNvy1hJNs12FYH4X+ZCNFIT9tprieR25NCdi5SWUbPZL0tVzJsHc1y92b2M2FxqRDohxQgJvyJOpcg2mSBzZZIkvDg7gfPSUXHVS1MQs0RHSbwq/XdQocUUhl9/e/YWCbNNxlM84BxFsBUok1dH/gzBySx+Fc8zYi7cOq9yaBT3RLT6cGmFGVYZJW4FyhPZOCLVNsLlnPQcX3dDg9A==</ds:X509Certificate>
        </ds:X509Data>
      </KeyInfo>
    </ds:Signature>
    <Subject>
      <NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent">ABCDEG1234567890</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="_049917a6-1183-42fd-a190-1d2cbaf9b144" NotOnOrAfter="2014-01-31T15:41:31.357Z" Recipient="https://login.microsoftonline.com/login.srf" />
      </SubjectConfirmation>
    </Subject>
    <Conditions NotBefore="2014-01-31T15:36:31.263Z" NotOnOrAfter="2014-01-31T16:36:31.263Z">
      <AudienceRestriction>
        <Audience>urn:federation:MicrosoftOnline</Audience>
      </AudienceRestriction>
    </Conditions>
    <AttributeStatement>
      <Attribute Name="IDPEmail">
        <AttributeValue>administrator@contoso.com</AttributeValue>
      </Attribute>
    </AttributeStatement>
    <AuthnStatement AuthnInstant="2014-01-31T15:36:30.200Z" SessionIndex="_7e3c1bcd-f180-4f78-83e1-7680920793aa">
      <AuthnContext>
        <AuthnContextClassRef>urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport</AuthnContextClassRef>
      </AuthnContext>
    </AuthnStatement>
    </Assertion>
    </samlp:Response>`

## <a name="configure-your-saml-20-compliant-identity-provider"></a><span data-ttu-id="8a8a8-173">設定 SAML 2.0 相容識別提供者</span><span class="sxs-lookup"><span data-stu-id="8a8a8-173">Configure your SAML 2.0 compliant identity provider</span></span>
<span data-ttu-id="8a8a8-174">本主題含有相關指導方針，可指出該如何設定 SAML 2.0 識別提供者，讓它與 Azure AD 建立同盟關係，以便能夠使用 SAML 2.0 通訊協定，以單一登入的方式存取一或多個 Microsoft 雲端服務 (例如 Office 365)。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-174">This topic contains guidelines on how to configure your SAML 2.0 identity provider to federate with Azure AD to enable single sign-on access to one or more Microsoft cloud services (such as Office 365) using the SAML 2.0 protocol.</span></span> <span data-ttu-id="8a8a8-175">此案例所使用之 Microsoft 雲端服務的 SAML 2.0 信賴憑證者是 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-175">The SAML 2.0 relying party for a Microsoft cloud service used in this scenario is Azure AD.</span></span>

## <a name="add-azure-ad-metadata"></a><span data-ttu-id="8a8a8-176">新增 Azure AD 中繼資料</span><span class="sxs-lookup"><span data-stu-id="8a8a8-176">Add Azure AD metadata</span></span>
<span data-ttu-id="8a8a8-177">您的 SAML 2.0 識別提供者需要遵守 Azure AD 信賴憑證者的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-177">Your SAML 2.0 identity provider needs to adhere to information about the Azure AD relying party.</span></span> <span data-ttu-id="8a8a8-178">Azure AD 會在 https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml 發佈中繼資料。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-178">Azure AD publishes metadata at https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml.</span></span>

<span data-ttu-id="8a8a8-179">當您在設定 SAML 2.0 識別提供者時，建議您一律匯入最新的 Azure AD 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-179">It is recommended that you always import the latest Azure AD metadata when configuring your SAML 2.0 identity provider.</span></span> <span data-ttu-id="8a8a8-180">請注意，Azure AD 不會從識別提供者讀取中繼資料。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-180">Note that Azure AD does not read metadata from the identity provider.</span></span>

## <a name="add-azure-ad-as-a-relying-party"></a><span data-ttu-id="8a8a8-181">將 Azure AD 新增為信賴憑證者</span><span class="sxs-lookup"><span data-stu-id="8a8a8-181">Add Azure AD as a relying party</span></span>
<span data-ttu-id="8a8a8-182">您必須讓 SAML 2.0 識別提供者能夠與 Azure AD 通訊。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-182">You have to enable communication between your SAML 2.0 identity provider and Azure AD.</span></span> <span data-ttu-id="8a8a8-183">這項設定會根據您使用的特定識別提供者而有所不同，因此請參閱其相關文件。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-183">This configuration will be dependent on your specific identity provider and you should refer to documentation for it.</span></span> <span data-ttu-id="8a8a8-184">一般來說，您會將信賴憑證者識別碼設定為和來自 Azure AD 中繼資料的 entityID 相同。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-184">You would typically set the relying party ID to the same as the entityID from the Azure AD metadata.</span></span>

>[!NOTE]
><span data-ttu-id="8a8a8-185">請確認 SAML 2.0 識別提供者伺服器上的時鐘已和正確的時間來源同步。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-185">Verify the clock on your SAML 2.0 identity provider server is synchronized to an accurate time source.</span></span> <span data-ttu-id="8a8a8-186">時鐘時間不正確將可能導致同盟登入失敗。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-186">An inaccurate clock time can cause federated logins to fail.</span></span>

## <a name="install-windows-powershell-for-sign-on-with-saml-20-identity-provider"></a><span data-ttu-id="8a8a8-187">安裝 Windows PowerShell 以使用 SAML 2.0 識別提供者來進行登入</span><span class="sxs-lookup"><span data-stu-id="8a8a8-187">Install Windows PowerShell for sign-on with SAML 2.0 identity provider</span></span>
<span data-ttu-id="8a8a8-188">在設定了 SAML 2.0 識別提供者以便用於 Azure AD 登入之後，下一步是下載並安裝適用於 Windows PowerShell 的 Azure Active Directory 模組。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-188">After you have configured your SAML 2.0 identity provider for use with Azure AD sign-on, the next step is to download and install the Azure Active Directory Module for Windows PowerShell.</span></span> <span data-ttu-id="8a8a8-189">安裝完成後，您將會使用這些 Cmdlet 來將 Azure AD 網域設定為同盟網域。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-189">Once installed, you will use these cmdlets to configure your Azure AD domains as federated domains.</span></span>

<span data-ttu-id="8a8a8-190">適用於 Windows PowerShell 的 Azure Active Directory 模組可供下載以便管理組織在 Azure AD 中的資料。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-190">The Azure Active Directory Module for Windows PowerShell is a download for managing your organizations data in Azure AD.</span></span> <span data-ttu-id="8a8a8-191">此模組會在 Windows PowerShell 中安裝一組 Cmdlet；您必須執行這些 Cmdlet 來設定 Azure AD 的單一登入存取權，進而設定您所訂閱之所有雲端服務的單一登入存取權。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-191">This module installs a set of cmdlets to Windows PowerShell; you run those cmdlets to set up single sign-on access to Azure AD and in turn to all of the cloud services you are subscribed to.</span></span> <span data-ttu-id="8a8a8-192">如需有關如何下載及安裝 Cmdlet 的指示，請參閱 [http://technet.microsoft.com/library/jj151815.aspx](http://technet.microsoft.com/library/jj151815.aspx)</span><span class="sxs-lookup"><span data-stu-id="8a8a8-192">For instructions about how to download and install the cmdlets, see [http://technet.microsoft.com/library/jj151815.aspx](http://technet.microsoft.com/library/jj151815.aspx)</span></span>

## <a name="set-up-a-trust-between-your-saml-identity-provider-and-azure-ad"></a><span data-ttu-id="8a8a8-193">設定 SAML 識別提供者與 Azure AD 的信任關係</span><span class="sxs-lookup"><span data-stu-id="8a8a8-193">Set up a trust between your SAML identity provider and Azure AD</span></span>
<span data-ttu-id="8a8a8-194">在 Azure AD 網域中設定同盟之前，您必須先設定自訂網域。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-194">Before configuring federation on an Azure AD domain, it must have a custom domain configured.</span></span> <span data-ttu-id="8a8a8-195">您無法為 Microsoft 所提供的預設網域建立同盟關係。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-195">You cannot federate the default domain that is provided by Microsoft.</span></span> <span data-ttu-id="8a8a8-196">Microsoft 的預設網域會以 "onmicrosoft.com" 結尾。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-196">The default domain from Microsoft ends with “onmicrosoft.com”.</span></span>
<span data-ttu-id="8a8a8-197">您將會在 Windows PowerShell 命令列介面中執行一系列的 Cmdlet，以新增或轉換用於進行單一登入的網域。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-197">You will run a series of cmdlets in the Windows PowerShell command-line interface to add or convert domains for single sign-on.</span></span>

<span data-ttu-id="8a8a8-198">每個您想要使用 SAML 2.0 識別提供者來建立同盟的 Azure Active Directory 網域，都必須新增為單一登入網域，或從標準網域轉換為單一登入網域。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-198">Each Azure Active Directory domain that you want to federate using your SAML 2.0 identity provider must either be added as a single sign-on domain or converted to be a single sign-on domain from a standard domain.</span></span> <span data-ttu-id="8a8a8-199">新增或轉換網域會設定 SAML 2.0 識別提供者和 Azure AD 之間的信任關係。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-199">Adding or converting a domain sets up a trust between your SAML 2.0 identity provider and Azure AD.</span></span>

<span data-ttu-id="8a8a8-200">下列程序可逐步引導您將現有的標準網域轉換為使用 SAML 2.0 SP-Lite 的同盟網域。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-200">The following procedure walks you through converting an existing standard domain to a federated domain using SAML 2.0 SP-Lite.</span></span> <span data-ttu-id="8a8a8-201">請注意，在您執行此步驟之後，您的網域可能會發生中斷從而影響使用者，時間可能長達 2 小時。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-201">Note that your domain may experience an outage that impacts users up to 2 hours after you take this step.</span></span>

## <a name="configuring-a-domain-in-your-azure-ad-directory-for-federation"></a><span data-ttu-id="8a8a8-202">在 Azure AD 目錄中設定用於同盟的網域</span><span class="sxs-lookup"><span data-stu-id="8a8a8-202">Configuring a domain in your Azure AD Directory for federation</span></span>


1. <span data-ttu-id="8a8a8-203">以租用戶管理員的身分連線到您的 Azure AD 目錄：Connect-MsolService。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-203">Connect to your Azure AD Directory as a tenant administrator: Connect-MsolService .</span></span>
2.  <span data-ttu-id="8a8a8-204">設定要用來搭配使用同盟功能和 SAML 2.0 的 Office 365 網域：`$dom = "contoso.com" $BrandName - "Sample SAML 2.0 IDP" $LogOnUrl = "https://WS2012R2-0.contoso.com/passiveLogon" $LogOffUrl = "https://WS2012R2-0.contoso.com/passiveLogOff" $ecpUrl = "https://WS2012R2-0.contoso.com/PAOS" $MyURI = "urn:uri:MySamlp2IDP" $MySigningCert = @" MIIC7jCCAdagAwIBAgIQRrjsbFPaXIlOG3GTv50fkjANBgkqhkiG9w0BAQsFADAzMTEwLwYDVQQDEyh BREZTIFNpZ25pbmcgLSBXUzIwMTJSMi0wLnN3aW5mb3JtZXIuY29tMB4XDTE0MDEyMDE1MTY0MFoXDT E1MDEyMDE1MTY0MFowMzExMC8GA1UEAxMoQURGUyBTaWduaW5nIC0gV1MyMDEyUjItMC5zd2luZm9yb WVyLmNvbTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAKe+rLVmXy1QwCwZwqgbbp1/kupQ VcjKuKLitVDbssFyqbDTjP7WRjlVMWAHBI3kgNT7oE362Gf2WMJFf1b0HcrsgLin7daRXpq4Qi6OA57 sW1YFMj3sqyuTP0eZV3S4+ZbDVob6amsZIdIwxaLP9Zfywg2bLsGnVldB0+XKedZwDbCLCVg+3ZWxd9 T/jV0hpLIIWr+LCOHqq8n8beJvlivgLmDJo8f+EITnAxWcsJUvVai/35AhHCUq9tc9sqMp5PWtabAEM b2AU72/QlX/72D2/NbGQq1BWYbqUpgpCZ2nSgvlWDHlCiUo//UGsvfox01kjTFlmqQInsJVfRxF5AcC AwEAATANBgkqhkiG9w0BAQsFAAOCAQEAi8c6C4zaTEc7aQiUgvnGQgCbMZbhUXXLGRpjvFLKaQzkwa9 eq7WLJibcSNyGXBa/SfT5wJgsm3TPKgSehGAOTirhcqHheZyvBObAScY7GOT+u9pVYp6raFrc7ez3c+ CGHeV/tNvy1hJNs12FYH4X+ZCNFIT9tprieR25NCdi5SWUbPZL0tVzJsHc1y92b2M2FxqRDohxQgJvy JOpcg2mSBzZZIkvDg7gfPSUXHVS1MQs0RHSbwq/XdQocUUhl9/e/YWCbNNxlM84BxFsBUok1dH/gzBy Sx+Fc8zYi7cOq9yaBT3RLT6cGmFGVYZJW4FyhPZOCLVNsLlnPQcX3dDg9A==" "@ $uri = "http://WS2012R2-0.contoso.com/adfs/services/trust" $Protocol = "SAMLP" Set-MsolDomainAuthentication -DomainName $dom -FederationBrandName $dom -Authentication Federated -PassiveLogOnUri $MyURI -ActiveLogOnUri $ecpUrl -SigningCertificate $MySigningCert -IssuerUri $uri -LogOffUri $url -PreferredAuthenticationProtocol $Protocol`</span><span class="sxs-lookup"><span data-stu-id="8a8a8-204">Configure your desired Office 365 domain to use federation with SAML 2.0: `$dom = "contoso.com" $BrandName - "Sample SAML 2.0 IDP" $LogOnUrl = "https://WS2012R2-0.contoso.com/passiveLogon" $LogOffUrl = "https://WS2012R2-0.contoso.com/passiveLogOff" $ecpUrl = "https://WS2012R2-0.contoso.com/PAOS" $MyURI = "urn:uri:MySamlp2IDP" $MySigningCert = @" MIIC7jCCAdagAwIBAgIQRrjsbFPaXIlOG3GTv50fkjANBgkqhkiG9w0BAQsFADAzMTEwLwYDVQQDEyh BREZTIFNpZ25pbmcgLSBXUzIwMTJSMi0wLnN3aW5mb3JtZXIuY29tMB4XDTE0MDEyMDE1MTY0MFoXDT E1MDEyMDE1MTY0MFowMzExMC8GA1UEAxMoQURGUyBTaWduaW5nIC0gV1MyMDEyUjItMC5zd2luZm9yb WVyLmNvbTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAKe+rLVmXy1QwCwZwqgbbp1/kupQ VcjKuKLitVDbssFyqbDTjP7WRjlVMWAHBI3kgNT7oE362Gf2WMJFf1b0HcrsgLin7daRXpq4Qi6OA57 sW1YFMj3sqyuTP0eZV3S4+ZbDVob6amsZIdIwxaLP9Zfywg2bLsGnVldB0+XKedZwDbCLCVg+3ZWxd9 T/jV0hpLIIWr+LCOHqq8n8beJvlivgLmDJo8f+EITnAxWcsJUvVai/35AhHCUq9tc9sqMp5PWtabAEM b2AU72/QlX/72D2/NbGQq1BWYbqUpgpCZ2nSgvlWDHlCiUo//UGsvfox01kjTFlmqQInsJVfRxF5AcC AwEAATANBgkqhkiG9w0BAQsFAAOCAQEAi8c6C4zaTEc7aQiUgvnGQgCbMZbhUXXLGRpjvFLKaQzkwa9 eq7WLJibcSNyGXBa/SfT5wJgsm3TPKgSehGAOTirhcqHheZyvBObAScY7GOT+u9pVYp6raFrc7ez3c+ CGHeV/tNvy1hJNs12FYH4X+ZCNFIT9tprieR25NCdi5SWUbPZL0tVzJsHc1y92b2M2FxqRDohxQgJvy JOpcg2mSBzZZIkvDg7gfPSUXHVS1MQs0RHSbwq/XdQocUUhl9/e/YWCbNNxlM84BxFsBUok1dH/gzBy Sx+Fc8zYi7cOq9yaBT3RLT6cGmFGVYZJW4FyhPZOCLVNsLlnPQcX3dDg9A==" "@ $uri = "http://WS2012R2-0.contoso.com/adfs/services/trust" $Protocol = "SAMLP" Set-MsolDomainAuthentication -DomainName $dom -FederationBrandName $dom -Authentication Federated -PassiveLogOnUri $MyURI -ActiveLogOnUri $ecpUrl -SigningCertificate $MySigningCert -IssuerUri $uri -LogOffUri $url -PreferredAuthenticationProtocol $Protocol`</span></span> 

3.  <span data-ttu-id="8a8a8-205">您可以從 IDP 中繼資料檔案取得簽署憑證的 base64 編碼字串。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-205">You can obtain the signing certificate base64 encoded string from your IDP metadata file.</span></span> <span data-ttu-id="8a8a8-206">我們提供了此位置的範例，但此範例可能會隨您的實作方式而略有不同。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-206">An example of this location has been provided but may differ slightly based on your implementation.</span></span>

    `<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol"> <KeyDescriptor use="signing"> <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#"> <X509Data> <X509Certificate>MIIC5jCCAc6gAwIBAgIQLnaxUPzay6ZJsC8HVv/QfTANBgkqhkiG9w0BAQsFADAvMS0wKwYDVQQDEyRBREZTIFNpZ25pbmcgLSBmcy50ZWNobGFiY2VudHJhbC5vcmcwHhcNMTMxMTA0MTgxMzMyWhcNMTQxMTA0MTgxMzMyWjAvMS0wKwYDVQQDEyRBREZTIFNpZ25pbmcgLSBmcy50ZWNobGFiY2VudHJhbC5vcmcwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCwMdVLTr5YTSRp+ccbSpuuFeXMfABD9mVCi2wtkRwC30TIyPdORz642MkurdxdPCWjwgJ0HW6TvXwcO9afH3OC5V//wEGDoNcI8PV4enCzTYFe/h//w51uqyv48Fbb3lEXs+aVl8155OAj2sO9IX64OJWKey82GQWK3g7LfhWWpp17j5bKpSd9DBH5pvrV+Q1ESU3mx71TEOvikHGCZYitEPywNeVMLRKrevdWI3FAhFjcCSO6nWDiMqCqiTDYOURXIcHVYTSof1YotkJ4tG6mP5Kpjzd4VQvnR7Pjb47nhIYG6iZ3mR1F85Ns9+hBWukQWNN2hcD/uGdPXhpdMVpBAgMBAAEwDQYJKoZIhvcNAQELBQADggEBAK7h7jF7wPzhZ1dPl4e+XMAr8I7TNbhgEU3+oxKyW/IioQbvZVw1mYVCbGq9Rsw4KE06eSMybqHln3w5EeBbLS0MEkApqHY+p68iRpguqa+W7UHKXXQVgPMCpqxMFKonX6VlSQOR64FgpBme2uG+LJ8reTgypEKspQIN0WvtPWmiq4zAwBp08hAacgv868c0MM4WbOYU0rzMIR6Q+ceGVRImlCwZ5b7XKp4mJZ9hlaRjeuyVrDuzBkzROSurX1OXoci08yJvhbtiBJLf3uPOJHrhjKRwIt2TnzS9ElgFZlJiDIA26Athe73n43CT0af2IG6yC7e6sK4L3NEXJrwwUZk=</X509Certificate> </X509Data> </KeyInfo> </KeyDescriptor>` 

<span data-ttu-id="8a8a8-207">如需「Set-msoldomainauthentication」的詳細資訊，請參閱：[http://technet.microsoft.com/library/dn194112.aspx](http://technet.microsoft.com/library/dn194112.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-207">For more information about “Set-MsolDomainAuthentication”, see: [http://technet.microsoft.com/library/dn194112.aspx](http://technet.microsoft.com/library/dn194112.aspx).</span></span>

>[!NOTE]
><span data-ttu-id="8a8a8-208">只有在已經為識別提供者設定了 ECP 擴充功能時，才必須執行使用「$ecpUrl = "https://WS2012R2-0.contoso.com/PAOS"」。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-208">You must run use “$ecpUrl = “https://WS2012R2-0.contoso.com/PAOS“” only if you set up an ECP extension for your identity provider.</span></span> <span data-ttu-id="8a8a8-209">Exchange Online 用戶端 (Outlook Web App (OWA) 除外) 仰賴以 POST 為基礎的作用中端點。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-209">Exchange Online clients, excluding Outlook Web Application (OWA), rely on a POST based active end point.</span></span> <span data-ttu-id="8a8a8-210">如果您的 SAML 2.0 STS 所實作的作用中端點，類似於 Shibboleth 以 ECP 實作的作用中端點，則這些豐富型用戶端可能可以和 Exchange Online 服務互動。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-210">If your SAML 2.0 STS implements an active end point similar to Shibboleth’s ECP implementation of an active end point it may be possible for these rich clients to interact with the Exchange Online service.</span></span>

<span data-ttu-id="8a8a8-211">設定好同盟之後，您可以切換回「非同盟」(或「受管理」) 模式，不過，系統最多需要兩個小時才能完成這項變更，而且您必須對每位使用者指派新的隨機密碼以便用於雲端式登入。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-211">Once federation has been configured you can switch back to “non-federated” (or “managed”), however this change takes up to two hours to complete and it requires assigning new random passwords for cloud based sign-in to each user.</span></span> <span data-ttu-id="8a8a8-212">在某些情況下，您可能需要切換回「受管理」模式，以將設定中的錯誤重設。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-212">Switching back to “managed” may be required in some scenarios to reset an error in your settings.</span></span> <span data-ttu-id="8a8a8-213">如需網域轉換的詳細資訊，請參閱：[http://msdn.microsoft.com/library/windowsazure/dn194122.aspx](http://msdn.microsoft.com/library/windowsazure/dn194122.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-213">For more information on Domain conversion see: [http://msdn.microsoft.com/library/windowsazure/dn194122.aspx](http://msdn.microsoft.com/library/windowsazure/dn194122.aspx).</span></span>

## <a name="provision-user-principals-to-azure-ad--office-365"></a><span data-ttu-id="8a8a8-214">將使用者主體佈建到 Azure AD/Office 365</span><span class="sxs-lookup"><span data-stu-id="8a8a8-214">Provision user principals to Azure AD / Office 365</span></span>
<span data-ttu-id="8a8a8-215">您必須先以使用者主體 (對應到 SAML 2.0 宣告中的判斷提示) 佈建 Azure AD，然後才能向 Office 365 驗證您的使用者。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-215">Before you can authenticate your users to Office 365 you must provision Azure AD with user principals that correspond to the assertion in the SAML 2.0 claim.</span></span> <span data-ttu-id="8a8a8-216">如果 Azure AD 事先不知道這些使用者主體，您就無法使用這些主體來進行同盟登入。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-216">If these user principals are not known to Azure AD in advance then they cannot be used for federated sign-in.</span></span> <span data-ttu-id="8a8a8-217">Azure AD Connect 或 Windows PowerShell 均可用來佈建使用者主體。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-217">Either Azure AD Connect or Windows PowerShell can be used to provision user principals.</span></span>

<span data-ttu-id="8a8a8-218">您可以使用 Azure AD Connect 將主體從內部部署 Active Directory 佈建到您在 Azure AD 目錄中的網域。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-218">Azure AD Connect can be used to provision principals to your domains in your Azure AD Directory from the on-premises Active Directory.</span></span> <span data-ttu-id="8a8a8-219">如需詳細資訊，請參閱[整合您的內部部署目錄與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-219">For more detailed information, see [Integrate your on-premises directories with Azure Active Directory](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="8a8a8-220">您也可以使用 Windows PowerShell 來自動將新的使用者新增至 Azure AD，並從內部部署目錄同步處理變更。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-220">Windows PowerShell can also be used to automate adding new users to Azure AD and to synchronize changes from the on-premises directory.</span></span> <span data-ttu-id="8a8a8-221">若要使用 Windows PowerShell Cmdlet，您必須下載 [Azure Active Directory 模組](https://docs.microsoft.com/powershell/azure/install-adv2?view=azureadps-2.0)。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-221">To use the Windows PowerShell cmdlets you must download the [Azure Active Directory Modules](https://docs.microsoft.com/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

<span data-ttu-id="8a8a8-222">此程序示範如何將單一使用者新增至 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-222">This procedure shows how to add a single user to Azure AD.</span></span>


1. <span data-ttu-id="8a8a8-223">以租用戶管理員的身分連線到您的 Azure AD 目錄：Connect-MsolService。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-223">Connect to your Azure AD Directory as a tenant administrator: Connect-MsolService.</span></span>
2.  <span data-ttu-id="8a8a8-224">建立新的使用者主體：` New-MsolUser
        -UserPrincipalName elwoodf1@contoso.com
        -ImmutableId ABCDEFG1234567890
        -DisplayName "Elwood Folk"
        -FirstName Elwood 
        -LastName Folk 
        -AlternateEmailAddresses "Elwood.Folk@contoso.com" 
        -LicenseAssignment "samlp2test:ENTERPRISEPACK" 
        -UsageLocation "US" `</span><span class="sxs-lookup"><span data-stu-id="8a8a8-224">Create a new user principal: ` New-MsolUser
        -UserPrincipalName elwoodf1@contoso.com
    -ImmutableId ABCDEFG1234567890
    -DisplayName "Elwood Folk"
    -FirstName Elwood 
    -LastName Folk 
    -AlternateEmailAddresses "Elwood.Folk@contoso.com" 
    -LicenseAssignment "samlp2test:ENTERPRISEPACK" 
    -UsageLocation "US" `</span></span> 

<span data-ttu-id="8a8a8-225">如需「New-MsolUser」的詳細資訊，請參閱 [http://technet.microsoft.com/library/dn194096.aspx](http://technet.microsoft.com/library/dn194096.aspx)</span><span class="sxs-lookup"><span data-stu-id="8a8a8-225">For more information about “New-MsolUser” check out, [http://technet.microsoft.com/library/dn194096.aspx](http://technet.microsoft.com/library/dn194096.aspx)</span></span>

>[!NOTE]
><span data-ttu-id="8a8a8-226">「UserPrinciplName」值必須符合您會為 SAML 2.0 宣告中的「IDPEmail」傳送的值，而「ImmutableID」值則必須符合「NameID」判斷提示中所傳送的值。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-226">The “UserPrinciplName” value must match the value that you will send for “IDPEmail” in your SAML 2.0 claim and the “ImmutableID” value must match the value sent in your “NameID” assertion.</span></span>

## <a name="verify-single-sign-on-with-your-saml-20-idp"></a><span data-ttu-id="8a8a8-227">使用 SAML 2.0 IDP 驗證單一登入</span><span class="sxs-lookup"><span data-stu-id="8a8a8-227">Verify single sign-on with your SAML 2.0 IDP</span></span>
<span data-ttu-id="8a8a8-228">若您是系統管理員，請在驗證和管理單一登入 (也稱為身分識別同盟) 之前，先檢閱相關資訊並執行下列文章中的步驟，以設定使用 SAML 2.0 SP-Lite 型識別提供者來進行的單一登入：</span><span class="sxs-lookup"><span data-stu-id="8a8a8-228">As the administrator, before you verify and manage single sign-on (also called identity federation), review the information and perform the steps in the following articles to set up single sign-on with your SAML 2.0 SP-Lite based identity provider:</span></span>


1.  <span data-ttu-id="8a8a8-229">您已檢閱 Azure AD SAML 2.0 通訊協定需求</span><span class="sxs-lookup"><span data-stu-id="8a8a8-229">You have reviewed the Azure AD SAML 2.0 Protocol Requirements</span></span>
2.  <span data-ttu-id="8a8a8-230">您已設定 SAML 2.0 識別提供者</span><span class="sxs-lookup"><span data-stu-id="8a8a8-230">You have configured your SAML 2.0 identity provider</span></span>
3.  <span data-ttu-id="8a8a8-231">安裝 Windows PowerShell 以使用 SAML 2.0 識別提供者來進行單一登入</span><span class="sxs-lookup"><span data-stu-id="8a8a8-231">Install Windows PowerShell for single sign-on with SAML 2.0 identity provider</span></span>
4.  <span data-ttu-id="8a8a8-232">設定 SAML 2.0 識別提供者與 Azure AD 的信任關係</span><span class="sxs-lookup"><span data-stu-id="8a8a8-232">Set up a trust between SAML 2.0 identity provider and Azure AD</span></span>
5.  <span data-ttu-id="8a8a8-233">透過 Windows PowerShell 或 Azure AD Connect 將已知的測試使用者主體佈建到 Azure Active Directory (Office 365)。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-233">Provisioned a known test user principal to Azure Active Directory (Office 365) either through Windows PowerShell or Azure AD Connect.</span></span>
6.  <span data-ttu-id="8a8a8-234">使用 [Azure AD Connect](active-directory-aadconnect.md) 來設定目錄同步作業。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-234">Configure directory synchronization using [Azure AD Connect](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="8a8a8-235">在設定了使用 SAML 2.0 SP-Lite 型識別提供者來進行的單一登入後，您應該確認它是否能正常運作。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-235">After setting up single sign-on with your SAML 2.0 SP-Lite based identity Provider, you should verify that it is working correctly.</span></span>

>[!NOTE]
><span data-ttu-id="8a8a8-236">如果您轉換網域而非新增網域，系統最多可能需要 24 小時才能設定好單一登入。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-236">If you converted a domain, rather than adding one, it may take up to 24 hours to set up single sign-on.</span></span>
<span data-ttu-id="8a8a8-237">在驗證單一登入之前，請先完成 Active Directory 同步作業的設定、對目錄進行同步處理，並啟用已同步處理的使用者。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-237">Before you verify single sign-on, you should finish setting up Active Directory synchronization, synchronize your directories, and activate your synced users.</span></span>

### <a name="use-the-tool-to-verify-that-single-sign-on-has-been-set-up-correctly"></a><span data-ttu-id="8a8a8-238">使用工具來驗證系統是否已正確設定單一登入</span><span class="sxs-lookup"><span data-stu-id="8a8a8-238">Use the tool to verify that single sign-on has been set up correctly</span></span>
<span data-ttu-id="8a8a8-239">若要驗證系統是否已正確設定單一登入，您可以執行下列程序來確認您能夠使用公司認證來登入雲端服務。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-239">To verify that single sign-on has been set up correctly, you can perform the following procedure to confirm that you are able to sign in to the cloud service with your corporate credentials.</span></span>

<span data-ttu-id="8a8a8-240">Microsoft 已提供一項工具供您用來測試 SAML 2.0 型識別提供者。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-240">Microsoft has provided a tool that you can use to test your SAML 2.0 based identity provider.</span></span> <span data-ttu-id="8a8a8-241">在執行這項測試工具之前，您必須已將 Azure AD 租用戶設定為與您的識別提供者建立同盟。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-241">Before running the test tool you must have configured an Azure AD tenant to federate with your identity provider.</span></span>

>[!NOTE]
><span data-ttu-id="8a8a8-242">連線分析程式需要使用 Internet Explorer 10 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-242">The Connectivity Analyzer requires Internet Explorer 10 or later.</span></span>



1. <span data-ttu-id="8a8a8-243">請從 [https://testconnectivity.microsoft.com/?tabid=Client](https://testconnectivity.microsoft.com/?tabid=Client) 下載連線分析程式。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-243">Download the Connectivity Analyzer from, [https://testconnectivity.microsoft.com/?tabid=Client](https://testconnectivity.microsoft.com/?tabid=Client).</span></span>
2.  <span data-ttu-id="8a8a8-244">按一下 [立即安裝] 以開始下載及安裝此工具。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-244">Click Install Now to begin downloading and installing the tool.</span></span>
3.  <span data-ttu-id="8a8a8-245">選取 [我無法設定與 Office 365、Azure 或其他使用 Azure Active Directory 之服務的同盟]。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-245">Select “I can’t set up federation with Office 365, Azure, or other services that use Azure Active Directory”.</span></span>
4.  <span data-ttu-id="8a8a8-246">工具開始下載並執行後，您會看到 [連線診斷] 視窗。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-246">Once the tool is downloaded and running, you will see the Connectivity Diagnostics window.</span></span> <span data-ttu-id="8a8a8-247">此工具會逐步引導您完成同盟連線的測試。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-247">The tool will step you through testing your federation connection.</span></span>
5.  <span data-ttu-id="8a8a8-248">連線分析程式會開啟您的 SAML 2.0 IDP 以供您登入，請輸入您要測試之使用者主體的認證：![SAML](media/active-directory-aadconnect-federation-saml-idp/saml1.png)</span><span class="sxs-lookup"><span data-stu-id="8a8a8-248">The Connectivity Analyzer will open your SAML 2.0 IDP for you to logon, enter the credentials for the user principal you are testing: ![SAML](media/active-directory-aadconnect-federation-saml-idp/saml1.png)</span></span>
6.  <span data-ttu-id="8a8a8-249">請在 [同盟測試登入] 視窗中，輸入所設定來與 SAML 2.0 識別提供者同盟之 Azure AD 租用戶的帳戶名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-249">At the Federation test sign-in window you should enter an account name and password for the Azure AD tenant that is configured to be federated with your SAML 2.0 identity provider.</span></span> <span data-ttu-id="8a8a8-250">此工具會嘗試使用這些認證來進行登入，而系統則會在輸出中提供登入嘗試期間所執行之測試的詳細結果。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-250">The tool will attempt to sign-in using those credentials and detailed results of tests performed during the sign-in attempt will be provided as output.</span></span>
<span data-ttu-id="8a8a8-251">![SAML](media/active-directory-aadconnect-federation-saml-idp/saml2.png)</span><span class="sxs-lookup"><span data-stu-id="8a8a8-251">![SAML](media/active-directory-aadconnect-federation-saml-idp/saml2.png)</span></span>
7. <span data-ttu-id="8a8a8-252">此視窗顯示失敗的測試結果。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-252">This window shows a failed result of testing.</span></span> <span data-ttu-id="8a8a8-253">按一下 [檢閱詳細結果] 將會顯示所執行之每項測試結果的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-253">Clicking on Review detailed results will show information about the results for each test that was performed.</span></span> <span data-ttu-id="8a8a8-254">您也可以將結果儲存至磁碟中以便共用。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-254">You can also save the results to disk in order to share them.</span></span>
 
>[!NOTE]
><span data-ttu-id="8a8a8-255">連線分析程式也會使用 WS* 型通訊協定和 ECP/PAOS 通訊協定來測試作用中的同盟。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-255">The Connectivity analyzer also tests Active Federation using the WS*-based and ECP/PAOS protocols.</span></span> <span data-ttu-id="8a8a8-256">如果您沒有使用這些通訊協定，則可以忽略下列錯誤：使用識別提供者的作用中同盟端點來測試作用中登入流程。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-256">If you are not using these you can disregard the following error: Testing the Active sign-in flow using your identity provider’s Active federation endpoint.</span></span>

### <a name="manually-verify-that-single-sign-on-has-been-set-up-correctly"></a><span data-ttu-id="8a8a8-257">手動驗證系統是否已正確設定單一登入</span><span class="sxs-lookup"><span data-stu-id="8a8a8-257">Manually verify that single sign-on has been set up correctly</span></span>
<span data-ttu-id="8a8a8-258">手動驗證提供了額外的步驟供您執行，以確保您的 SAML 2.0 識別提供者在許多情況下皆可正常運作。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-258">Manual verification provides additional steps that you can take to ensure that your SAML 2.0 identity Provider is working properly in many scenarios.</span></span>
<span data-ttu-id="8a8a8-259">若要驗證系統是否已正確設定單一登入，請完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8a8a8-259">To verify that single sign-on has been set up correctly, complete the following steps:</span></span>


1. <span data-ttu-id="8a8a8-260">在已加入網域的電腦上，使用和您用於公司認證相同的登入名稱來登入雲端服務。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-260">On a domain-joined computer, sign in to your cloud service using the same logon name that you use for your corporate credentials.</span></span>
2.  <span data-ttu-id="8a8a8-261">在密碼方塊內按一下。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-261">Click inside the password box.</span></span> <span data-ttu-id="8a8a8-262">如果您已設定單一登入，密碼方塊將呈陰影狀，而且您會看到下列訊息：「您現在必須在 <your company> 登入。」</span><span class="sxs-lookup"><span data-stu-id="8a8a8-262">If single sign-on is set up, the password box will be shaded, and you will see the following message: “You are now required to sign in at <your company>.”</span></span>
3.  <span data-ttu-id="8a8a8-263">在 <your company> 連結按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-263">Click the Sign in at <your company> link.</span></span> <span data-ttu-id="8a8a8-264">如果您能夠登入，則表示您已設定好單一登入。</span><span class="sxs-lookup"><span data-stu-id="8a8a8-264">If you are able to sign in, then single sign-on has been set up.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a8a8-265">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8a8a8-265">Next Steps</span></span>


- [<span data-ttu-id="8a8a8-266">使用 Azure AD Connect 管理和自訂 Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="8a8a8-266">Active Directory Federation Services management and customization with Azure AD Connect</span></span>](active-directory-aadconnect-federation-management.md)
- [<span data-ttu-id="8a8a8-267">Azure AD 同盟相容性清單</span><span class="sxs-lookup"><span data-stu-id="8a8a8-267">Azure AD federation compatibility list</span></span>](active-directory-aadconnect-federation-compatibility.md)
- [<span data-ttu-id="8a8a8-268">Azure AD Connect 自訂安裝</span><span class="sxs-lookup"><span data-stu-id="8a8a8-268">Azure AD Connect Custom Installation</span></span>](active-directory-aadconnect-get-started-custom.md)
