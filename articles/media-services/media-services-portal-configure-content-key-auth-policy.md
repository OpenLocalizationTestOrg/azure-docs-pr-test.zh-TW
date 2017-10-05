---
title: "使用 Azure 入口網站設定內容金鑰授權原則 | Microsoft Docs"
description: "了解如何設定內容金鑰的授權原則。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ee82a3fa-c34b-48f2-a108-8ba321f1691e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 5a35c7255a1c30a693862589c14f6a22a1900790
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="configure-content-key-authorization-policy"></a><span data-ttu-id="93017-103">設定內容金鑰授權原則</span><span class="sxs-lookup"><span data-stu-id="93017-103">Configure Content Key Authorization Policy</span></span>
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a><span data-ttu-id="93017-104">Overview</span><span class="sxs-lookup"><span data-stu-id="93017-104">Overview</span></span>
<span data-ttu-id="93017-105">Microsoft Azure 媒體服務可讓您傳遞受到進階加密標準 (AES) (使用 128 位元加密金鑰) 或 [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/)保護的 MPEG DASH、Smooth Streaming 和 HTTP Live Streaming (HLS) 串流。</span><span class="sxs-lookup"><span data-stu-id="93017-105">Microsoft Azure Media Services enables you to deliver MPEG-DASH, Smooth Streaming, and HTTP-Live-Streaming (HLS) streams protected with Advanced Encryption Standard (AES) (using 128-bit encryption keys) or [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span></span> <span data-ttu-id="93017-106">AMS 也可讓您傳遞使用 Widevine DRM 加密的 DASH 串流。</span><span class="sxs-lookup"><span data-stu-id="93017-106">AMS also enables you to deliver DASH streams encrypted with Widevine DRM.</span></span> <span data-ttu-id="93017-107">PlayReady 和 Widevine 是依照 Common Encryption (ISO/IEC 23001-7 CENC) 規格加密。</span><span class="sxs-lookup"><span data-stu-id="93017-107">Both PlayReady and Widevine are encrypted per the Common Encryption (ISO/IEC 23001-7 CENC) specification.</span></span>

<span data-ttu-id="93017-108">媒體服務也提供 **金鑰/授權傳遞服務** ，用戶端可以從該處取得 AES 金鑰或 PlayReady/Widevine 授權，以便播放加密的內容。</span><span class="sxs-lookup"><span data-stu-id="93017-108">Media Services also provides a **Key/License Delivery Service** from which clients can obtain AES keys or PlayReady/Widevine licenses to play the encrypted content.</span></span>

<span data-ttu-id="93017-109">本主題示範如何使用 Azure 入口網站設定內容金鑰授權原則。</span><span class="sxs-lookup"><span data-stu-id="93017-109">This topic shows how to use the Azure portal to configure the content key authorization policy.</span></span> <span data-ttu-id="93017-110">金鑰稍後可以用來動態加密您的內容。</span><span class="sxs-lookup"><span data-stu-id="93017-110">The key can later be used to dynamically encrypt your content.</span></span> <span data-ttu-id="93017-111">請注意，目前您可以加密下列串流格式：HLS、MPEG DASH 和 Smooth Streaming。</span><span class="sxs-lookup"><span data-stu-id="93017-111">Note that currently you can encrypt the following streaming formats: HLS, MPEG DASH, and Smooth Streaming.</span></span> <span data-ttu-id="93017-112">您無法加密漸進式下載。</span><span class="sxs-lookup"><span data-stu-id="93017-112">You cannot encrypt progressive downloads.</span></span>

<span data-ttu-id="93017-113">當播放程式要求設定為動態加密的串流時，媒體服務會使用設定的金鑰，以 AES 或 DRM 加密來動態加密您的內容。</span><span class="sxs-lookup"><span data-stu-id="93017-113">When a player requests a stream that is set to be dynamically encrypted, Media Services uses the configured key to dynamically encrypt your content using AES or DRM encryption.</span></span> <span data-ttu-id="93017-114">為了將串流解密，播放程式將從金鑰傳遞服務要求金鑰。</span><span class="sxs-lookup"><span data-stu-id="93017-114">To decrypt the stream, the player will request the key from the key delivery service.</span></span> <span data-ttu-id="93017-115">為了決定使用者是否有權取得金鑰，服務會評估為金鑰指定的授權原則。</span><span class="sxs-lookup"><span data-stu-id="93017-115">To decide whether or not the user is authorized to get the key, the service evaluates the authorization policies that you specified for the key.</span></span>

<span data-ttu-id="93017-116">如果您預計有多個內容金鑰，或想要指定 **金鑰/授權傳遞服務** URL，而非媒體服務金鑰傳遞服務，請使用媒體服務 .NET SDK 或 REST API。</span><span class="sxs-lookup"><span data-stu-id="93017-116">If you plan to have multiple content keys or want to specify a **Key/License Delivery Service** URL other than the Media Services key delivery service, use Media Services .NET SDK or REST APIs.</span></span>

[<span data-ttu-id="93017-117">使用媒體服務 .NET SDK 設定內容金鑰授權原則</span><span class="sxs-lookup"><span data-stu-id="93017-117">Configure Content Key Authorization Policy using Media Services .NET SDK</span></span>](media-services-dotnet-configure-content-key-auth-policy.md)

[<span data-ttu-id="93017-118">使用媒體服務 REST API 設定內容金鑰授權原則</span><span class="sxs-lookup"><span data-stu-id="93017-118">Configure Content Key Authorization Policy using Media Services REST API</span></span>](media-services-rest-configure-content-key-auth-policy.md)

### <a name="some-considerations-apply"></a><span data-ttu-id="93017-119">適用一些考量事項：</span><span class="sxs-lookup"><span data-stu-id="93017-119">Some considerations apply:</span></span>
* <span data-ttu-id="93017-120">當建立您的 AMS 帳戶時，系統會新增一個狀態為 [已停止] 的「預設」串流端點到您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="93017-120">When your AMS account is created a **default** streaming endpoint is added  to your account in the **Stopped** state.</span></span> <span data-ttu-id="93017-121">若要開始串流處理您的內容並利用動態封裝和動態加密功能，您的串流端點必須處於 [執行中] 狀態。</span><span class="sxs-lookup"><span data-stu-id="93017-121">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, your streaming endpoint has to be in the **Running** state.</span></span> 
* <span data-ttu-id="93017-122">您的資產必須包含一組調適性位元速率 MP4 或調適性位元速率 Smooth Streaming 檔案。</span><span class="sxs-lookup"><span data-stu-id="93017-122">Your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="93017-123">如需詳細資訊，請參閱 [為資產編碼](media-services-encode-asset.md)。</span><span class="sxs-lookup"><span data-stu-id="93017-123">For more information, see [Encode an asset](media-services-encode-asset.md).</span></span>
* <span data-ttu-id="93017-124">金鑰傳遞服務會快取 ContentKeyAuthorizationPolicy 和其相關物件 (原則選項和限制) 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="93017-124">The Key Delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.</span></span>  <span data-ttu-id="93017-125">如果您建立 ContentKeyAuthorizationPolicy，並指定要使用 "Token" 的限制，那麼便測試它，然後將原則更新為"Open" 限制，將需要大約 15 分鐘，原則才會切換為 "Open" 版本的原則。</span><span class="sxs-lookup"><span data-stu-id="93017-125">If you create a ContentKeyAuthorizationPolicy and specify to use a “Token” restriction, then test it, and then update the policy to “Open” restriction, it will take roughly 15 minutes before the policy switches to the “Open” version of the policy.</span></span>

## <a name="how-to-configure-the-key-authorization-policy"></a><span data-ttu-id="93017-126">作法：設定金鑰授權原則</span><span class="sxs-lookup"><span data-stu-id="93017-126">How to: configure the key authorization policy</span></span>
<span data-ttu-id="93017-127">若要設定金鑰授權原則，請選取 [ **內容保護** ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="93017-127">To configure the key authorization policy, select the **CONTENT PROTECTION** page.</span></span>

<span data-ttu-id="93017-128">媒體服務支援多種方式來驗證提出金鑰要求的使用者。</span><span class="sxs-lookup"><span data-stu-id="93017-128">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="93017-129">內容金鑰授權原則可以有 **open**、**token** 或 **IP** 授權限制 (**IP** 可以使用 REST 或 .NET SDK 設定)。</span><span class="sxs-lookup"><span data-stu-id="93017-129">The content key authorization policy can have **open**, **token**, or **IP** authorization restrictions (**IP** can be configured with REST or .NET SDK).</span></span>

### <a name="open-restriction"></a><span data-ttu-id="93017-130">Open 限制</span><span class="sxs-lookup"><span data-stu-id="93017-130">Open restriction</span></span>
<span data-ttu-id="93017-131">**open** 限制表示系統將會傳送金鑰給提出金鑰要求的任何人。</span><span class="sxs-lookup"><span data-stu-id="93017-131">The **open** restriction means the system will deliver the key to anyone who makes a key request.</span></span> <span data-ttu-id="93017-132">這項限制可用於測試用途。</span><span class="sxs-lookup"><span data-stu-id="93017-132">This restriction might be useful for testing purposes.</span></span>

![OpenPolicy][open_policy]

### <a name="token-restriction"></a><span data-ttu-id="93017-134">權杖限制</span><span class="sxs-lookup"><span data-stu-id="93017-134">Token restriction</span></span>
<span data-ttu-id="93017-135">若要選擇權杖限制原則，請按 [ **權杖** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="93017-135">To choose the token restricted policy, press the **TOKEN** button.</span></span>

<span data-ttu-id="93017-136">**權杖**限制原則必須伴隨著**安全權杖服務** (STS) 所發出的權杖。</span><span class="sxs-lookup"><span data-stu-id="93017-136">The **token** restricted policy must be accompanied by a token issued by a **Secure Token Service** (STS).</span></span> <span data-ttu-id="93017-137">媒體服務支援**簡單 Web 權杖** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) 格式和 **JSON Web 權杖** (JWT) 格式的權杖。</span><span class="sxs-lookup"><span data-stu-id="93017-137">Media Services supports tokens in the **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format and **JSON Web Token** (JWT) format.</span></span> <span data-ttu-id="93017-138">如需資訊，請參閱 [JWT 權杖驗證](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)。</span><span class="sxs-lookup"><span data-stu-id="93017-138">For information, see [JWT token authentication](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/).</span></span>

<span data-ttu-id="93017-139">媒體服務不提供 **安全權杖服務**。</span><span class="sxs-lookup"><span data-stu-id="93017-139">Media Services does not provide **Secure Token Services**.</span></span> <span data-ttu-id="93017-140">您可以建立自訂 STS，或利用 Microsoft Azure ACS 來發行權杖。</span><span class="sxs-lookup"><span data-stu-id="93017-140">You can create a custom STS or leverage Microsoft Azure ACS to issue tokens.</span></span> <span data-ttu-id="93017-141">STS 必須設定為建立使用指定的索引鍵和問題宣告您在權杖限制組態中指定簽署的權杖。</span><span class="sxs-lookup"><span data-stu-id="93017-141">The STS must be configured to create a token signed with the specified key and issue claims that you specified in the token restriction configuration.</span></span> <span data-ttu-id="93017-142">如果權杖有效，且權杖中的宣告符合為內容金鑰設定的宣告，媒體服務金鑰傳遞服務會將加密金鑰傳回給用戶端。</span><span class="sxs-lookup"><span data-stu-id="93017-142">The Media Services key delivery service will return the encryption key to the client if the token is valid and the claims in the token match those configured for the content key.</span></span> <span data-ttu-id="93017-143">如需詳細資訊，請參閱 [使用 Azure ACS 發行權杖](http://mingfeiy.com/acs-with-key-services)。</span><span class="sxs-lookup"><span data-stu-id="93017-143">For more information, see [Use Azure ACS to issue tokens](http://mingfeiy.com/acs-with-key-services).</span></span>

<span data-ttu-id="93017-144">設定 **TOKEN** 限制原則時，您必須設定**驗證金鑰**、**簽發者**和**對象**的值。</span><span class="sxs-lookup"><span data-stu-id="93017-144">When configuring the **TOKEN** restricted policy, you must set values for **verification key**, **issuer** and **audience**.</span></span> <span data-ttu-id="93017-145">主要驗證金鑰包含簽署權杖使用的金鑰，簽發者是發行權杖的安全權杖服務。</span><span class="sxs-lookup"><span data-stu-id="93017-145">The primary verification key contains the key that the token was signed with, issuer is the secure token service that issues the token.</span></span> <span data-ttu-id="93017-146">對象 (有時稱為範圍) 描述權杖或權杖獲授權存取之資源的用途。</span><span class="sxs-lookup"><span data-stu-id="93017-146">The audience (sometimes called scope) describes the intent of the token or the resource the token authorizes access to.</span></span> <span data-ttu-id="93017-147">媒體服務金鑰傳遞服務會驗證權杖中的這些值符合在範本中的值。</span><span class="sxs-lookup"><span data-stu-id="93017-147">The Media Services key delivery service validates that these values in the token match the values in the template.</span></span>

### <a name="playready"></a><span data-ttu-id="93017-148">PlayReady</span><span class="sxs-lookup"><span data-stu-id="93017-148">PlayReady</span></span>
<span data-ttu-id="93017-149">使用 **PlayReady**保護內容時，您需要在驗證原則中指定的其中一件事是定義 PlayReady 授權範本的 XML 字串。</span><span class="sxs-lookup"><span data-stu-id="93017-149">When protecting your content with **PlayReady**, one of the things you need to specify in your authorization policy is an XML string that defines the PlayReady license template.</span></span> <span data-ttu-id="93017-150">依預設，會設定下列原則：</span><span class="sxs-lookup"><span data-stu-id="93017-150">By default, the following policy is set:</span></span>

<span data-ttu-id="93017-151"><PlayReadyLicenseResponseTemplate xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1"> <LicenseTemplates> <PlayReadyLicenseTemplate><AllowTestDevices>true</AllowTestDevices> <ContentKey i:type="ContentEncryptionKeyFromHeader" /> <LicenseType>非持續性</LicenseType> <PlayRight> <AllowPassingVideoContentToUnknownOutput>允許</AllowPassingVideoContentToUnknownOutput> </PlayRight> </PlayReadyLicenseTemplate> </LicenseTemplates> </PlayReadyLicenseResponseTemplate></span><span class="sxs-lookup"><span data-stu-id="93017-151"><PlayReadyLicenseResponseTemplate xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1"> <LicenseTemplates> <PlayReadyLicenseTemplate><AllowTestDevices>true</AllowTestDevices> <ContentKey i:type="ContentEncryptionKeyFromHeader" /> <LicenseType>Nonpersistent</LicenseType> <PlayRight> <AllowPassingVideoContentToUnknownOutput>Allowed</AllowPassingVideoContentToUnknownOutput> </PlayRight> </PlayReadyLicenseTemplate> </LicenseTemplates> </PlayReadyLicenseResponseTemplate></span></span>

<span data-ttu-id="93017-152">您可以按一下 [匯入原則 xml] 按鈕，並提供符合[這裡](media-services-playready-license-template-overview.md)所定義之 XML 結構描述的不同 XML。</span><span class="sxs-lookup"><span data-stu-id="93017-152">You can click the **import policy xml** button and provide a different XML which conforms to the  XML Schema defined [here](media-services-playready-license-template-overview.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="93017-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="93017-153">Next step</span></span>
<span data-ttu-id="93017-154">檢閱媒體服務學習路徑。</span><span class="sxs-lookup"><span data-stu-id="93017-154">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="93017-155">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="93017-155">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[open_policy]: ./media/media-services-portal-configure-content-key-auth-policy/media-services-protect-content-with-open-restriction.png
[token_policy]: ./media/media-services-key-authorization-policy/media-services-protect-content-with-token-restriction.png

