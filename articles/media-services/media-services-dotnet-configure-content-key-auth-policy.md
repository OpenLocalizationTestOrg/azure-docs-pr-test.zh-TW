---
title: "使用媒體服務 .NET SDK 設定內容金鑰授權原則 | Microsoft Docs"
description: "了解如何使用媒體服務 .NET SDK 設定內容金鑰的授權原則。"
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 1a0aedda-5b87-4436-8193-09fc2f14310c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;mingfeiy
ms.openlocfilehash: 75dd9107dca215a0b31db3d44bada69210fe9ac6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a><span data-ttu-id="944fb-103">動態加密：設定內容金鑰授權原則</span><span class="sxs-lookup"><span data-stu-id="944fb-103">Dynamic encryption: configure content key authorization policy</span></span>
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a><span data-ttu-id="944fb-104">概觀</span><span class="sxs-lookup"><span data-stu-id="944fb-104">Overview</span></span>
<span data-ttu-id="944fb-105">Microsoft Azure 媒體服務可讓您傳遞受到進階加密標準 (AES) (使用 128 位元加密金鑰) 或 [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/)保護的 MPEG DASH、Smooth Streaming 和 HTTP Live Streaming (HLS) 串流。</span><span class="sxs-lookup"><span data-stu-id="944fb-105">Microsoft Azure Media Services enables you to deliver MPEG-DASH, Smooth Streaming, and HTTP-Live-Streaming (HLS) streams protected with Advanced Encryption Standard (AES) (using 128-bit encryption keys) or [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span></span> <span data-ttu-id="944fb-106">AMS 也可讓您傳遞使用 Widevine DRM 加密的 DASH 串流。</span><span class="sxs-lookup"><span data-stu-id="944fb-106">AMS also enables you to deliver DASH streams encrypted with Widevine DRM.</span></span> <span data-ttu-id="944fb-107">PlayReady 和 Widevine 是依照 Common Encryption (ISO/IEC 23001-7 CENC) 規格加密。</span><span class="sxs-lookup"><span data-stu-id="944fb-107">Both PlayReady and Widevine are encrypted per the Common Encryption (ISO/IEC 23001-7 CENC) specification.</span></span>

<span data-ttu-id="944fb-108">媒體服務也提供 **金鑰/授權傳遞服務** ，用戶端可以從該處取得 AES 金鑰或 PlayReady/Widevine 授權，以便播放加密的內容。</span><span class="sxs-lookup"><span data-stu-id="944fb-108">Media Services also provides a **Key/License Delivery Service** from which clients can obtain AES keys or PlayReady/Widevine licenses to play the encrypted content.</span></span>

<span data-ttu-id="944fb-109">如果您想要媒體服務加密資產，您需要建立加密金鑰 (**CommonEncryption** 或 **EnvelopeEncryption**) 與資產 (如[這裡](media-services-dotnet-create-contentkey.md)所述) 的，並且設定金鑰的授權原則 (如本文中所述)。</span><span class="sxs-lookup"><span data-stu-id="944fb-109">If you want for Media Services to encrypt an asset, you need to associate an encryption key (**CommonEncryption** or **EnvelopeEncryption**) with the asset (as described [here](media-services-dotnet-create-contentkey.md)) and also configure authorization policies for the key (as described in this article).</span></span>

<span data-ttu-id="944fb-110">播放程式要求串流時，媒體服務便會使用 AES 或 DRM 加密，使用指定的金鑰動態加密您的內容。</span><span class="sxs-lookup"><span data-stu-id="944fb-110">When a stream is requested by a player, Media Services uses the specified key to dynamically encrypt your content using AES or DRM encryption.</span></span> <span data-ttu-id="944fb-111">為了將串流解密，播放程式將從金鑰傳遞服務要求金鑰。</span><span class="sxs-lookup"><span data-stu-id="944fb-111">To decrypt the stream, the player will request the key from the key delivery service.</span></span> <span data-ttu-id="944fb-112">為了決定使用者是否有權取得金鑰，服務會評估為金鑰指定的授權原則。</span><span class="sxs-lookup"><span data-stu-id="944fb-112">To decide whether or not the user is authorized to get the key, the service evaluates the authorization policies that you specified for the key.</span></span>

<span data-ttu-id="944fb-113">媒體服務支援多種方式來驗證提出金鑰要求的使用者。</span><span class="sxs-lookup"><span data-stu-id="944fb-113">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="944fb-114">內容金鑰授權原則可能會有一個或多個授權限制：**open** 或 **token** 限制。</span><span class="sxs-lookup"><span data-stu-id="944fb-114">The content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span> <span data-ttu-id="944fb-115">權杖限制原則必須伴隨著安全權杖服務 (STS) 所發出的權杖。</span><span class="sxs-lookup"><span data-stu-id="944fb-115">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="944fb-116">媒體服務支援**簡單 Web 權杖** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) 格式和 **JSON Web 權杖** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) 格式的權杖。</span><span class="sxs-lookup"><span data-stu-id="944fb-116">Media Services supports tokens in the **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format and **JSON Web Token** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) format.</span></span>

<span data-ttu-id="944fb-117">媒體服務不提供安全權杖服務。</span><span class="sxs-lookup"><span data-stu-id="944fb-117">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="944fb-118">您可以建立自訂 STS，或利用 Microsoft Azure ACS 來發行權杖。</span><span class="sxs-lookup"><span data-stu-id="944fb-118">You can create a custom STS or leverage Microsoft Azure ACS to issue tokens.</span></span> <span data-ttu-id="944fb-119">STS 必須設定為建立使用指定金鑰簽署的權杖，並發行在權杖限制組態中指定的宣告 (如本文中所述)。</span><span class="sxs-lookup"><span data-stu-id="944fb-119">The STS must be configured to create a token signed with the specified key and issue claims that you specified in the token restriction configuration (as described in this article).</span></span> <span data-ttu-id="944fb-120">如果權杖有效，且權杖中的宣告符合為內容金鑰設定的宣告，媒體服務金鑰傳遞服務會將加密金鑰傳回給用戶端。</span><span class="sxs-lookup"><span data-stu-id="944fb-120">The Media Services key delivery service will return the encryption key to the client if the token is valid and the claims in the token match those configured for the content key.</span></span>

<span data-ttu-id="944fb-121">如需詳細資訊，請參閱</span><span class="sxs-lookup"><span data-stu-id="944fb-121">For more information, see</span></span>

[<span data-ttu-id="944fb-122">JWT 權杖驗證</span><span class="sxs-lookup"><span data-stu-id="944fb-122">JWT token authentication</span></span>](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

<span data-ttu-id="944fb-123">[整合 Azure 媒體服務 OWIN MVC 型應用程式與 Azure Active Directory 並根據 JWT 宣告限制內容金鑰傳遞](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/)。</span><span class="sxs-lookup"><span data-stu-id="944fb-123">[Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span></span>

<span data-ttu-id="944fb-124">[使用 Azure ACS 發行權杖](http://mingfeiy.com/acs-with-key-services)。</span><span class="sxs-lookup"><span data-stu-id="944fb-124">[Use Azure ACS to issue tokens](http://mingfeiy.com/acs-with-key-services).</span></span>

### <a name="some-considerations-apply"></a><span data-ttu-id="944fb-125">適用一些考量事項：</span><span class="sxs-lookup"><span data-stu-id="944fb-125">Some considerations apply:</span></span>
* <span data-ttu-id="944fb-126">當建立您的 AMS 帳戶時，系統會新增一個狀態為 [已停止] 的「預設」串流端點到您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="944fb-126">When your AMS account is created a **default** streaming endpoint is added  to your account in the **Stopped** state.</span></span> <span data-ttu-id="944fb-127">若要開始串流處理您的內容並利用動態封裝和動態加密功能，您的串流端點必須處於 [執行中] 狀態。</span><span class="sxs-lookup"><span data-stu-id="944fb-127">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, your streaming endpoint has to be in the **Running** state.</span></span> 
* <span data-ttu-id="944fb-128">您的資產必須包含一組調適性位元速率 MP4 或調適性位元速率 Smooth Streaming 檔案。</span><span class="sxs-lookup"><span data-stu-id="944fb-128">Your asset must contain a set of adaptive bitrate MP4s or  adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="944fb-129">如需詳細資訊，請參閱 [為資產編碼](media-services-encode-asset.md)。</span><span class="sxs-lookup"><span data-stu-id="944fb-129">For more information, see [Encode an asset](media-services-encode-asset.md).</span></span>
* <span data-ttu-id="944fb-130">使用 **AssetCreationOptions.StorageEncrypted** 選項，上傳資產並為其編碼。</span><span class="sxs-lookup"><span data-stu-id="944fb-130">Upload and encode your assets using **AssetCreationOptions.StorageEncrypted** option.</span></span>
* <span data-ttu-id="944fb-131">如果您計劃有多個內容金鑰需要相同的原則組態，強烈建議建立一個授權原則，並針對多個內容金鑰重複使用。</span><span class="sxs-lookup"><span data-stu-id="944fb-131">If you plan to have multiple content keys that require the same policy configuration, it is strongly recommended to create a single authorization policy and reuse it with multiple content keys.</span></span>
* <span data-ttu-id="944fb-132">金鑰傳遞服務會快取 ContentKeyAuthorizationPolicy 和其相關物件 (原則選項和限制) 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="944fb-132">The Key Delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.</span></span>  <span data-ttu-id="944fb-133">如果您建立 ContentKeyAuthorizationPolicy，並指定要使用 "Token" 的限制，那麼便測試它，然後將原則更新為"Open" 限制，將需要大約 15 分鐘，原則才會切換為 "Open" 版本的原則。</span><span class="sxs-lookup"><span data-stu-id="944fb-133">If you create a ContentKeyAuthorizationPolicy and specify to use a “Token” restriction, then test it, and then update the policy to “Open” restriction, it will take roughly 15 minutes before the policy switches to the “Open” version of the policy.</span></span>
* <span data-ttu-id="944fb-134">如果您加入或更新您的資產傳遞原則，您必須刪除現有的定位程式 (如果有的話)，並建立新的定位器。</span><span class="sxs-lookup"><span data-stu-id="944fb-134">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
* <span data-ttu-id="944fb-135">您目前無法加密漸進式下載。</span><span class="sxs-lookup"><span data-stu-id="944fb-135">Currently, you cannot encrypt progressive downloads.</span></span>

## <a name="aes-128-dynamic-encryption"></a><span data-ttu-id="944fb-136">AES-128 動態加密</span><span class="sxs-lookup"><span data-stu-id="944fb-136">AES-128 Dynamic Encryption</span></span>
### <a name="open-restriction"></a><span data-ttu-id="944fb-137">Open 限制</span><span class="sxs-lookup"><span data-stu-id="944fb-137">Open Restriction</span></span>
<span data-ttu-id="944fb-138">Open 限制表示系統將會傳送金鑰給提出金鑰要求的任何人。</span><span class="sxs-lookup"><span data-stu-id="944fb-138">Open restriction means the system will deliver the key to anyone who makes a key request.</span></span> <span data-ttu-id="944fb-139">這項限制可用於測試用途。</span><span class="sxs-lookup"><span data-stu-id="944fb-139">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="944fb-140">下列範例會建立 open 授權原則，並將它加入至內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="944fb-140">The following example creates an open authorization policy and adds it to the content key.</span></span>

    static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
    {
        // Create ContentKeyAuthorizationPolicy with Open restrictions
        // and create authorization policy
        IContentKeyAuthorizationPolicy policy = _context.
        ContentKeyAuthorizationPolicies.
        CreateAsync("Open Authorization Policy").Result;
        
        List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

        ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
                Name = "HLS Open Authorization Policy",
                KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                Requirements = null // no requirements needed for HLS
            };

        restrictions.Add(restriction);

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "policy", 
            ContentKeyDeliveryType.BaselineHttp, 
            restrictions, 
            "");

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy to ContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key to Asset: Key ID is " + updatedKey.Id);
    }


### <a name="token-restriction"></a><span data-ttu-id="944fb-141">Token 限制</span><span class="sxs-lookup"><span data-stu-id="944fb-141">Token Restriction</span></span>
<span data-ttu-id="944fb-142">本節描述如何建立內容金鑰授權原則，然後建立它與內容金鑰的關聯。</span><span class="sxs-lookup"><span data-stu-id="944fb-142">This section describes how to create a content key authorization policy and associate it with the content key.</span></span> <span data-ttu-id="944fb-143">授權原則描述必須符合哪些授權需求，以判斷使用者是否有權接收金鑰 (例如，「驗證金鑰」清單是否包含簽署權杖用的金鑰)。</span><span class="sxs-lookup"><span data-stu-id="944fb-143">The authorization policy describes what authorization requirements must be met to determine if the user is authorized to receive the key (for example, does the “verification key” list contain the key that the token was signed with).</span></span>

<span data-ttu-id="944fb-144">若要設定 token 限制選項，您需要使用 XML 來描述權杖的授權需求。</span><span class="sxs-lookup"><span data-stu-id="944fb-144">To configure the token restriction option, you need to use an XML to describe the token’s authorization requirements.</span></span> <span data-ttu-id="944fb-145">token 限制組態 XML 必須符合下列 XML 結構描述。</span><span class="sxs-lookup"><span data-stu-id="944fb-145">The token restriction configuration XML must conform to the following XML schema.</span></span>

#### <span data-ttu-id="944fb-146"><a id="schema"></a>Token 限制結構描述</span><span class="sxs-lookup"><span data-stu-id="944fb-146"><a id="schema"></a>Token restriction schema</span></span>
    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:tns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1" elementFormDefault="qualified" targetNamespace="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1" xmlns:xs="http://www.w3.org/2001/XMLSchema">
      <xs:complexType name="TokenClaim">
        <xs:sequence>
          <xs:element name="ClaimType" nillable="true" type="xs:string" />
          <xs:element minOccurs="0" name="ClaimValue" nillable="true" type="xs:string" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="TokenClaim" nillable="true" type="tns:TokenClaim" />
      <xs:complexType name="TokenRestrictionTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" name="AlternateVerificationKeys" nillable="true" type="tns:ArrayOfTokenVerificationKey" />
          <xs:element name="Audience" nillable="true" type="xs:anyURI" />
          <xs:element name="Issuer" nillable="true" type="xs:anyURI" />
          <xs:element name="PrimaryVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
          <xs:element minOccurs="0" name="RequiredClaims" nillable="true" type="tns:ArrayOfTokenClaim" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="TokenRestrictionTemplate" nillable="true" type="tns:TokenRestrictionTemplate" />
      <xs:complexType name="ArrayOfTokenVerificationKey">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="TokenVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfTokenVerificationKey" nillable="true" type="tns:ArrayOfTokenVerificationKey" />
      <xs:complexType name="TokenVerificationKey">
        <xs:sequence />
      </xs:complexType>
      <xs:element name="TokenVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
      <xs:complexType name="ArrayOfTokenClaim">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="TokenClaim" nillable="true" type="tns:TokenClaim" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfTokenClaim" nillable="true" type="tns:ArrayOfTokenClaim" />
      <xs:complexType name="SymmetricVerificationKey">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:TokenVerificationKey">
            <xs:sequence>
              <xs:element name="KeyValue" nillable="true" type="xs:base64Binary" />
            </xs:sequence>
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="SymmetricVerificationKey" nillable="true" type="tns:SymmetricVerificationKey" />
    </xs:schema>

<span data-ttu-id="944fb-147">設定 **token** 限制原則時，您必須指定主要**驗證金鑰**、**簽發者**和**對象**參數。</span><span class="sxs-lookup"><span data-stu-id="944fb-147">When configuring the **token** restricted policy, you must specify the primary** verification key**, **issuer** and **audience** parameters.</span></span> <span data-ttu-id="944fb-148">**主要驗證金鑰**包含簽署權杖使用的金鑰，**簽發者**是發行權杖的安全性權杖服務。</span><span class="sxs-lookup"><span data-stu-id="944fb-148">The **primary verification key **contains the key that the token was signed with, **issuer** is the secure token service that issues the token.</span></span> <span data-ttu-id="944fb-149">**對象** (有時稱為**範圍**) 描述權杖或權杖獲授權存取之資源的用途。</span><span class="sxs-lookup"><span data-stu-id="944fb-149">The **audience** (sometimes called **scope**) describes the intent of the token or the resource the token authorizes access to.</span></span> <span data-ttu-id="944fb-150">媒體服務金鑰傳遞服務會驗證權杖中的這些值符合在範本中的值。</span><span class="sxs-lookup"><span data-stu-id="944fb-150">The Media Services key delivery service validates that these values in the token match the values in the template.</span></span> 

<span data-ttu-id="944fb-151">使用 **Media Services SDK for .NET** 時，您可以使用 **TokenRestrictionTemplate** 類別來產生限制權杖。</span><span class="sxs-lookup"><span data-stu-id="944fb-151">When using **Media Services SDK for .NET**, you can use the **TokenRestrictionTemplate** class to generate the restriction token.</span></span>
<span data-ttu-id="944fb-152">下列範例會建立具有 token 限制的授權原則。</span><span class="sxs-lookup"><span data-stu-id="944fb-152">The following example creates an authorization policy with a token restriction.</span></span> <span data-ttu-id="944fb-153">在此範例中，用戶端必須提出權杖，權杖中包含簽署金鑰 (VerificationKey)、權杖簽發者和必要的宣告。</span><span class="sxs-lookup"><span data-stu-id="944fb-153">In this example, the client would have to present a token that contains: signing key (VerificationKey), a token issuer, and required claims.</span></span>

    public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
    {
        string tokenTemplateString = GenerateTokenRequirements();

        IContentKeyAuthorizationPolicy policy = _context.
                                ContentKeyAuthorizationPolicies.
                                CreateAsync("HLS token restricted authorization policy").Result;

        List<ContentKeyAuthorizationPolicyRestriction> restrictions =
                new List<ContentKeyAuthorizationPolicyRestriction>();

        ContentKeyAuthorizationPolicyRestriction restriction =
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Token Authorization Policy",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                    Requirements = tokenTemplateString
                };

        restrictions.Add(restriction);

        //You could have multiple options 
        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
                "Token option for HLS",
                ContentKeyDeliveryType.BaselineHttp,
                restrictions,
                null  // no key delivery data is needed for HLS
                );

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy to ContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key to Asset: Key ID is " + updatedKey.Id);

        return tokenTemplateString;
    }

    static private string GenerateTokenRequirements()
    {
        TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

        template.PrimaryVerificationKey = new SymmetricVerificationKey();
        template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();

        template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

        return TokenRestrictionTemplateSerializer.Serialize(template);
    }

#### <span data-ttu-id="944fb-154"><a id="test"></a>測試權杖</span><span class="sxs-lookup"><span data-stu-id="944fb-154"><a id="test"></a>Test token</span></span>
<span data-ttu-id="944fb-155">若要取得根據用於金鑰授權原則之權杖限制的測試權杖，請執行下列動作。</span><span class="sxs-lookup"><span data-stu-id="944fb-155">To get a test token based on the token restriction that was used for the key authorization policy, do the following.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on the the data in the given TokenRestrictionTemplate.
    // Note, you need to pass the key id Guid because we specified 
    // TokenClaim.ContentKeyIdentifierClaim in during the creation of TokenRestrictionTemplate.
    Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

    //The GenerateTestToken method returns the token without the word “Bearer” in front
    //so you have to add it in front of the token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
    Console.WriteLine("The authorization token is:\nBearer {0}", testToken);
    Console.WriteLine();


## <a name="playready-dynamic-encryption"></a><span data-ttu-id="944fb-156">PlayReady 動態加密</span><span class="sxs-lookup"><span data-stu-id="944fb-156">PlayReady Dynamic Encryption</span></span>
<span data-ttu-id="944fb-157">媒體服務可讓您設定您要 PlayReady DRM 執行階段在使用者嘗試播放受保護內容時強制執行的權限和限制。</span><span class="sxs-lookup"><span data-stu-id="944fb-157">Media Services enables you to configure the rights and restrictions that you want for the PlayReady DRM runtime to enforce when a user is trying to play back protected content.</span></span> 

<span data-ttu-id="944fb-158">使用 PlayReady 保護內容時，您需要在驗證原則中指定的其中一件事是定義 [PlayReady 授權範本](media-services-playready-license-template-overview.md)的 XML 字串。</span><span class="sxs-lookup"><span data-stu-id="944fb-158">When protecting your content with PlayReady, one of the things you need to specify in your authorization policy is an XML string that defines the [PlayReady license template](media-services-playready-license-template-overview.md).</span></span> <span data-ttu-id="944fb-159">在 Media Services SDK for .NET 中，**PlayReadyLicenseResponseTemplate** 和 **PlayReadyLicenseTemplate** 類別將協助您定義 PlayReady 授權範本。</span><span class="sxs-lookup"><span data-stu-id="944fb-159">In Media Services SDK for .NET, the **PlayReadyLicenseResponseTemplate** and **PlayReadyLicenseTemplate** classes will help you define the PlayReady License Template.</span></span>

<span data-ttu-id="944fb-160">[本主題](media-services-protect-with-drm.md)示範如何使用 **PlayReady** 和 **Widevine** 加密內容。</span><span class="sxs-lookup"><span data-stu-id="944fb-160">[This topic](media-services-protect-with-drm.md) shows how to encrypt your content with **PlayReady** and **Widevine**.</span></span>

### <a name="open-restriction"></a><span data-ttu-id="944fb-161">Open 限制</span><span class="sxs-lookup"><span data-stu-id="944fb-161">Open Restriction</span></span>
<span data-ttu-id="944fb-162">Open 限制表示系統將會傳送金鑰給提出金鑰要求的任何人。</span><span class="sxs-lookup"><span data-stu-id="944fb-162">Open restriction means the system will deliver the key to anyone who makes a key request.</span></span> <span data-ttu-id="944fb-163">這項限制可用於測試用途。</span><span class="sxs-lookup"><span data-stu-id="944fb-163">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="944fb-164">下列範例會建立 open 授權原則，並將它加入至內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="944fb-164">The following example creates an open authorization policy and adds it to the content key.</span></span>

    static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
    {

        // Create ContentKeyAuthorizationPolicy with Open restrictions 
        // and create authorization policy          

        List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
        {
            new ContentKeyAuthorizationPolicyRestriction 
            { 
                Name = "Open", 
                KeyRestrictionType = (int)ContentKeyRestrictionType.Open, 
                Requirements = null
            }
        };

        // Configure PlayReady license template.
        string newLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.PlayReadyLicense,
                    restrictions, newLicenseTemplate);

        IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                    ContentKeyAuthorizationPolicies.
                    CreateAsync("Deliver Common Content Key with no restrictions").
                    Result;


        contentKeyAuthorizationPolicy.Options.Add(policyOption);

        // Associate the content key authorization policy with the content key.
        contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
        contentKey = contentKey.UpdateAsync().Result;
    }

### <a name="token-restriction"></a><span data-ttu-id="944fb-165">Token 限制</span><span class="sxs-lookup"><span data-stu-id="944fb-165">Token Restriction</span></span>
<span data-ttu-id="944fb-166">若要設定 token 限制選項，您需要使用 XML 來描述權杖的授權需求。</span><span class="sxs-lookup"><span data-stu-id="944fb-166">To configure the token restriction option, you need to use an XML to describe the token’s authorization requirements.</span></span> <span data-ttu-id="944fb-167">Token 限制組態 XML 必須符合 [此](#schema) 節。</span><span class="sxs-lookup"><span data-stu-id="944fb-167">The token restriction configuration XML must conform to the XML schema shown in [this](#schema) section.</span></span>

    public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
    {
        string tokenTemplateString = GenerateTokenRequirements();

        IContentKeyAuthorizationPolicy policy = _context.
                                ContentKeyAuthorizationPolicies.
                                CreateAsync("HLS token restricted authorization policy").Result;

        List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
        {
            new ContentKeyAuthorizationPolicyRestriction 
            { 
                Name = "Token Authorization Policy", 
                KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                Requirements = tokenTemplateString, 
            }
        };

        // Configure PlayReady license template.
        string newLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.PlayReadyLicense,
                    restrictions, newLicenseTemplate);

        IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                    ContentKeyAuthorizationPolicies.
                    CreateAsync("Deliver Common Content Key with no restrictions").
                    Result;

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy to ContentKey
        contentKeyAuthorizationPolicy.Options.Add(policyOption);

        // Associate the content key authorization policy with the content key
        contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
        contentKey = contentKey.UpdateAsync().Result;

        return tokenTemplateString;
    }

    static private string GenerateTokenRequirements()
    {

        TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

        template.PrimaryVerificationKey = new SymmetricVerificationKey();
        template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();


        template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

        return TokenRestrictionTemplateSerializer.Serialize(template);
    } 

    static private string ConfigurePlayReadyLicenseTemplate()
    {
        // The following code configures PlayReady License Template using .NET classes
        // and returns the XML string.

        //The PlayReadyLicenseResponseTemplate class represents the template for the response sent back to the end user. 
        //It contains a field for a custom data string between the license server and the application 
        //(may be useful for custom app logic) as well as a list of one or more license templates.
        PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();

        // The PlayReadyLicenseTemplate class represents a license template for creating PlayReady licenses
        // to be returned to the end users. 
        //It contains the data on the content key in the license and any rights or restrictions to be 
        //enforced by the PlayReady DRM runtime when using the content key.
        PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();
        //Configure whether the license is persistent (saved in persistent storage on the client) 
        //or non-persistent (only held in memory while the player is using the license).  
        licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

        // AllowTestDevices controls whether test devices can use the license or not.  
        // If true, the MinimumSecurityLevel property of the license
        // is set to 150.  If false (the default), the MinimumSecurityLevel property of the license is set to 2000.
        licenseTemplate.AllowTestDevices = true;


        // You can also configure the Play Right in the PlayReady license by using the PlayReadyPlayRight class. 
        // It grants the user the ability to playback the content subject to the zero or more restrictions 
        // configured in the license and on the PlayRight itself (for playback specific policy). 
        // Much of the policy on the PlayRight has to do with output restrictions 
        // which control the types of outputs that the content can be played over and 
        // any restrictions that must be put in place when using a given output.
        // For example, if the DigitalVideoOnlyContentRestriction is enabled, 
        //then the DRM runtime will only allow the video to be displayed over digital outputs 
        //(analog video outputs won’t be allowed to pass the content).

        //IMPORTANT: These types of restrictions can be very powerful but can also affect the consumer experience. 
        // If the output protections are configured too restrictive, 
        // the content might be unplayable on some clients. For more information, see the PlayReady Compliance Rules document.

        // For example:
        //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

        responseTemplate.LicenseTemplates.Add(licenseTemplate);

        return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
    }


<span data-ttu-id="944fb-168">若要取得根據用於金鑰授權原則之權杖限制的測試權杖，請參閱 [此](#test) 節。</span><span class="sxs-lookup"><span data-stu-id="944fb-168">To get a test token based on the token restriction that was used for the key authorization policy see [this](#test) section.</span></span> 

## <span data-ttu-id="944fb-169"><a id="types"></a>定義 ContentKeyAuthorizationPolicy 時使用的類型</span><span class="sxs-lookup"><span data-stu-id="944fb-169"><a id="types"></a>Types used when defining ContentKeyAuthorizationPolicy</span></span>
### <span data-ttu-id="944fb-170"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span><span class="sxs-lookup"><span data-stu-id="944fb-170"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span></span>
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <span data-ttu-id="944fb-171"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="944fb-171"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>
    public enum ContentKeyDeliveryType
    {
      None = 0,
      PlayReadyLicense = 1,
      BaselineHttp = 2,
      Widevine = 3
    }

### <span data-ttu-id="944fb-172"><a id="TokenType"></a>TokenType</span><span class="sxs-lookup"><span data-stu-id="944fb-172"><a id="TokenType"></a>TokenType</span></span>
    public enum TokenType
    {
        Undefined = 0,
        SWT = 1,
        JWT = 2,
    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="944fb-173">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="944fb-173">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="944fb-174">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="944fb-174">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="944fb-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="944fb-175">Next step</span></span>
<span data-ttu-id="944fb-176">現在，您已設定內容金鑰授權原則，請移至 [如何設定資產傳遞原則](media-services-dotnet-configure-asset-delivery-policy.md) 主題。</span><span class="sxs-lookup"><span data-stu-id="944fb-176">Now that you have configured content key's authorization policy, go to the [How to configure asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md) topic.</span></span>

