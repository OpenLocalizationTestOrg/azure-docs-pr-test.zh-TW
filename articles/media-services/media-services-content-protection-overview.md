---
title: "使用 Azure 媒體服務保護您的內容 | Microsoft Docs"
description: "此文章簡介如何利用 Media Services 保護內容。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 81bc00e1-dcda-4d69-b9ab-8768b793422b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 64be4ea104bd11b8e191e2c8d4170a2de88acb47
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="protecting-content-overview"></a><span data-ttu-id="9e57b-103">保護內容概觀</span><span class="sxs-lookup"><span data-stu-id="9e57b-103">Protecting content overview</span></span>
<span data-ttu-id="9e57b-104">Microsoft Azure 媒體服務可讓您保護媒體從離開電腦到進行儲存、處理和傳遞時的安全。</span><span class="sxs-lookup"><span data-stu-id="9e57b-104">Microsoft Azure Media Services enables you to secure your media from the time it leaves your computer through storage, processing, and delivery.</span></span> <span data-ttu-id="9e57b-105">媒體服務可讓您傳遞利用進階加密標準 (AES) (使用 128 位元加密金鑰) 動態加密或任何主要 DRM：Microsoft PlayReady、Google Widevine 和 Apple FairPlay 的即時與隨選內容。</span><span class="sxs-lookup"><span data-stu-id="9e57b-105">Media Services allows you to deliver your live and on-demand content encrypted dynamically with Advanced Encryption Standard (AES) (using 128-bit encryption keys) or any of the major DRMs: Microsoft PlayReady, Google Widevine, and Apple FairPlay.</span></span> <span data-ttu-id="9e57b-106">媒體服務也提供服務，可傳遞 AES 金鑰和 DRM (PlayReady、Widevine 和 FairPlay) 授權給授權用戶端。</span><span class="sxs-lookup"><span data-stu-id="9e57b-106">Media Services also provides a service for delivering AES keys and DRM (PlayReady, Widevine, and FairPlay) licenses to authorized clients.</span></span> 

<span data-ttu-id="9e57b-107">下列映像示範 AMS 支援的內容保護工作流程。</span><span class="sxs-lookup"><span data-stu-id="9e57b-107">The following image demonstrates the content protection workflows that AMS supports.</span></span> 

![利用 PlayReady 保護](./media/media-services-content-protection-overview/media-services-content-protection-with-multi-drm.png)

>[!NOTE]
><span data-ttu-id="9e57b-109">建立 AMS 帳戶時，**預設**串流端點會新增至 [已停止] 狀態的帳戶。</span><span class="sxs-lookup"><span data-stu-id="9e57b-109">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="9e57b-110">若要開始串流內容並利用動態封裝和動態加密功能，您想要串流內容的串流端點必須處於 [執行中] 狀態。</span><span class="sxs-lookup"><span data-stu-id="9e57b-110">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 

<span data-ttu-id="9e57b-111">本主題說明關於了解以 AMS 內容保護的 [概念與術語](media-services-content-protection-overview.md) 。</span><span class="sxs-lookup"><span data-stu-id="9e57b-111">This topic explains [concepts and terminology](media-services-content-protection-overview.md) relevant to understanding content protection with AMS.</span></span> <span data-ttu-id="9e57b-112">主題也包含說明如何達成內容保護工作的主題 [連結](media-services-content-protection-overview.md#common-scenarios) 。</span><span class="sxs-lookup"><span data-stu-id="9e57b-112">The topic also contains [links](media-services-content-protection-overview.md#common-scenarios) to topics that show how to achieve content protection tasks.</span></span> 

## <a name="dynamic-encryption"></a><span data-ttu-id="9e57b-113">動態加密</span><span class="sxs-lookup"><span data-stu-id="9e57b-113">Dynamic encryption</span></span>
<span data-ttu-id="9e57b-114">Microsoft Azure 媒體服務可讓您傳遞使用 AES 清除金鑰或 DRM 加密：Microsoft PlayReady、Google Widevine 和 Apple FairPlay 所動態加密的內容。</span><span class="sxs-lookup"><span data-stu-id="9e57b-114">Microsoft Azure Media Services enables you to deliver your content encrypted  dynamically with AES clear key or DRM encryption: Microsoft PlayReady, Google Widevine, and Apple FairPlay.</span></span>

<span data-ttu-id="9e57b-115">目前，您可以加密下列串流格式：HLS、MPEG DASH 和 Smooth Streaming。</span><span class="sxs-lookup"><span data-stu-id="9e57b-115">Currently, you can encrypt the following streaming formats: HLS, MPEG DASH, and Smooth Streaming.</span></span> <span data-ttu-id="9e57b-116">您無法加密漸進式下載。</span><span class="sxs-lookup"><span data-stu-id="9e57b-116">You cannot encrypt progressive downloads.</span></span>

<span data-ttu-id="9e57b-117">如果您想要媒體服務加密資產，則需要建立加密金鑰 (CommonEncryption 或 EnvelopeEncryption) 與資產的關聯，同時設定金鑰的授權原則。</span><span class="sxs-lookup"><span data-stu-id="9e57b-117">If you want for Media Services to encrypt an asset, you need to associate an encryption key (CommonEncryption or EnvelopeEncryption) with your asset and also configure authorization policies for the key.</span></span>

<span data-ttu-id="9e57b-118">您也需要設定資產的傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="9e57b-118">You also need to configure the asset's delivery policy.</span></span> <span data-ttu-id="9e57b-119">如果您想要串流處理儲存體加密的資產，請一定要透過設定資產傳遞原則來指定資產傳遞方式。</span><span class="sxs-lookup"><span data-stu-id="9e57b-119">If you want to stream a storage encrypted asset, make sure to specify how you want to deliver it by configuring asset delivery policy.</span></span>

<span data-ttu-id="9e57b-120">播放程式要求串流時，媒體服務便會使用 AES 清除金鑰或 DRM 加密，使用指定的金鑰動態加密您的內容。</span><span class="sxs-lookup"><span data-stu-id="9e57b-120">When a stream is requested by a player, Media Services uses the specified key to dynamically encrypt your content using AES clear key or DRM encryption.</span></span> <span data-ttu-id="9e57b-121">為了將串流解密，播放程式將從金鑰傳遞服務要求金鑰。</span><span class="sxs-lookup"><span data-stu-id="9e57b-121">To decrypt the stream, the player will request the key from the key delivery service.</span></span> <span data-ttu-id="9e57b-122">為了決定使用者是否有權取得金鑰，服務會評估為金鑰指定的授權原則。</span><span class="sxs-lookup"><span data-stu-id="9e57b-122">To decide whether or not the user is authorized to get the key, the service evaluates the authorization policies that you specified for the key.</span></span>


## <a name="storage-encryption"></a><span data-ttu-id="9e57b-123">儲存體加密</span><span class="sxs-lookup"><span data-stu-id="9e57b-123">Storage encryption</span></span>
<span data-ttu-id="9e57b-124">使用儲存體加密，使用 AES-256 位元加密對您的純文字內容進行本機加密，然後將其上傳到已靜止加密儲存的 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="9e57b-124">Use storage encryption to encrypt your clear content locally using AES 256 bit encryption and then upload it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="9e57b-125">使用儲存體加密保護的資產會在編碼之前自動解除加密並放在加密的檔案系統中，並且選擇性地在上傳為新的輸出資產之前重新加密。</span><span class="sxs-lookup"><span data-stu-id="9e57b-125">Assets protected with storage encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="9e57b-126">儲存體加密的主要使用案例是當您想要使用強式加密保護靜止在磁碟上的高品質輸入媒體檔案時。</span><span class="sxs-lookup"><span data-stu-id="9e57b-126">The primary use case for storage encryption is when you want to secure your high quality input media files with strong encryption at rest on disk.</span></span>

<span data-ttu-id="9e57b-127">若要傳遞儲存體加密資產，您必須設定資產的傳遞原則，讓媒體服務知道您的內容傳遞方式。</span><span class="sxs-lookup"><span data-stu-id="9e57b-127">In order to deliver a storage encrypted asset, you must configure the asset’s delivery policy so Media Services knows how you want to deliver your content.</span></span> <span data-ttu-id="9e57b-128">串流處理資產之前，串流伺服器會移除儲存體加密，並使用指定的傳遞原則來串流處理您的內容 (例如，AES、一般加密或不加密)。</span><span class="sxs-lookup"><span data-stu-id="9e57b-128">Before your asset can be streamed, the streaming server removes the storage encryption and streams your content using the specified delivery policy (for example, AES, common encryption, or no encryption).</span></span>

## <a name="common-encryption-cenc"></a><span data-ttu-id="9e57b-129">一般加密 (CENC)</span><span class="sxs-lookup"><span data-stu-id="9e57b-129">Common encryption (CENC)</span></span>
<span data-ttu-id="9e57b-130">當使用 PlayReady 或/及 Widewine 加密您的內容時會使用一般加密。</span><span class="sxs-lookup"><span data-stu-id="9e57b-130">Common encryption is used when encrypting your content with PlayReady or/and Widewine.</span></span>

## <a name="using-cbcs-aapl-encryption"></a><span data-ttu-id="9e57b-131">使用 cbcs-aapl 加密</span><span class="sxs-lookup"><span data-stu-id="9e57b-131">Using cbcs-aapl encryption</span></span>
<span data-ttu-id="9e57b-132">使用 FairPlay 加密您的內容時會使用 Cbcs-aapl。</span><span class="sxs-lookup"><span data-stu-id="9e57b-132">Cbcs-aapl is used when encrypting your content with FairPlay.</span></span>

## <a name="envelope-encryption"></a><span data-ttu-id="9e57b-133">信封加密</span><span class="sxs-lookup"><span data-stu-id="9e57b-133">Envelope encryption</span></span>
<span data-ttu-id="9e57b-134">如果您想要使用 AES-128 清除金鑰來保護您的內容，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="9e57b-134">Use this option if you want to protect your content with AES-128 clear key.</span></span> <span data-ttu-id="9e57b-135">如果需要更安全的選項，請選擇本主題中所列的其中一個 DRM。</span><span class="sxs-lookup"><span data-stu-id="9e57b-135">If you want a more secure option, choose one of the DRMs listed in this topic.</span></span> 

## <a name="licenses-and-keys-delivery-service"></a><span data-ttu-id="9e57b-136">授權和金鑰傳遞服務</span><span class="sxs-lookup"><span data-stu-id="9e57b-136">Licenses and keys delivery service</span></span>
<span data-ttu-id="9e57b-137">媒體服務提供一種服務，可將 DRM (PlayReady、Widevine 與 FairPlay) 授權和 AES 清除金鑰傳遞給授權用戶端。</span><span class="sxs-lookup"><span data-stu-id="9e57b-137">Media Services provides a service for delivering DRM (PlayReady, Widevine, FairPlay) licenses and AES clear keys to authorized clients.</span></span> <span data-ttu-id="9e57b-138">若要設定您授權和金鑰的授權和驗證原則，才能使用 [Azure 入口網站](media-services-portal-protect-content.md)、REST API 或 Media Services SDK for .NET。</span><span class="sxs-lookup"><span data-stu-id="9e57b-138">You can use [the Azure portal](media-services-portal-protect-content.md), REST API, or Media Services SDK for .NET to configure authorization and authentication policies for your licenses and keys.</span></span>

## <a name="token-restriction"></a><span data-ttu-id="9e57b-139">權杖限制</span><span class="sxs-lookup"><span data-stu-id="9e57b-139">Token restriction</span></span>
<span data-ttu-id="9e57b-140">內容金鑰授權原則可能會有一個或多個授權限制：open 或 token 限制。</span><span class="sxs-lookup"><span data-stu-id="9e57b-140">The content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span> <span data-ttu-id="9e57b-141">權杖限制原則必須伴隨著安全權杖服務 (STS) 所發出的權杖。</span><span class="sxs-lookup"><span data-stu-id="9e57b-141">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="9e57b-142">媒體服務支援簡單 Web 權杖 (SWT) 格式和 JSON Web 權杖 (JWT) 格式的權杖。</span><span class="sxs-lookup"><span data-stu-id="9e57b-142">Media Services supports tokens in the Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span></span> <span data-ttu-id="9e57b-143">媒體服務不提供安全權杖服務。</span><span class="sxs-lookup"><span data-stu-id="9e57b-143">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="9e57b-144">您可以建立自訂 STS，或利用 Microsoft Azure ACS 來發行權杖。</span><span class="sxs-lookup"><span data-stu-id="9e57b-144">You can create a custom STS or leverage Microsoft Azure ACS to issue tokens.</span></span> <span data-ttu-id="9e57b-145">STS 必須設定為建立使用指定的索引鍵和問題宣告您在權杖限制組態中指定簽署的權杖。</span><span class="sxs-lookup"><span data-stu-id="9e57b-145">The STS must be configured to create a token signed with the specified key and issue claims that you specified in the token restriction configuration.</span></span> <span data-ttu-id="9e57b-146">如果權杖有效，且權杖中的宣告符合針對金鑰 (或授權) 所設定的宣告，媒體服務金鑰傳遞服務會將所要求的金鑰 (或授權) 傳回給用戶端。</span><span class="sxs-lookup"><span data-stu-id="9e57b-146">The Media Services key delivery service will return the requested key (or license) to the client if the token is valid and the claims in the token match those configured for the key (or license).</span></span>

<span data-ttu-id="9e57b-147">設定 token 限制原則時，您必須指定主要驗證金鑰、簽發者和對象參數。</span><span class="sxs-lookup"><span data-stu-id="9e57b-147">When configuring the token restricted policy, you must specify the primary verification key, issuer and audience parameters.</span></span> <span data-ttu-id="9e57b-148">主要驗證金鑰包含簽署權杖使用的金鑰，簽發者是發行權杖的安全權杖服務。</span><span class="sxs-lookup"><span data-stu-id="9e57b-148">The primary verification key contains the key that the token was signed with, issuer is the secure token service that issues the token.</span></span> <span data-ttu-id="9e57b-149">對象 (有時稱為範圍) 描述權杖或權杖獲授權存取之資源的用途。</span><span class="sxs-lookup"><span data-stu-id="9e57b-149">The audience (sometimes called scope) describes the intent of the token or the resource the token authorizes access to.</span></span> <span data-ttu-id="9e57b-150">媒體服務金鑰傳遞服務會驗證權杖中的這些值符合在範本中的值。</span><span class="sxs-lookup"><span data-stu-id="9e57b-150">The Media Services key delivery service validates that these values in the token match the values in the template.</span></span>

## <a name="streaming-urls"></a><span data-ttu-id="9e57b-151">串流 URL</span><span class="sxs-lookup"><span data-stu-id="9e57b-151">Streaming URLs</span></span>
<span data-ttu-id="9e57b-152">如果使用一個以上 DRM 來加密您的資產，您應該使用串流 URL 中的加密標籤：(format='m3u8-aapl', encryption='xxx')。</span><span class="sxs-lookup"><span data-stu-id="9e57b-152">If your asset was encrypted with more than one DRM, you should use an encryption tag in the streaming URL: (format='m3u8-aapl', encryption='xxx').</span></span>

<span data-ttu-id="9e57b-153">您必須考量下列事項：</span><span class="sxs-lookup"><span data-stu-id="9e57b-153">The following considerations apply:</span></span>

* <span data-ttu-id="9e57b-154">僅可指定零個或一個加密類型。</span><span class="sxs-lookup"><span data-stu-id="9e57b-154">Only zero or one encryption type can be specified.</span></span>
* <span data-ttu-id="9e57b-155">如果只有一個加密套用到資產，則無須在 URL 中指定加密類型。</span><span class="sxs-lookup"><span data-stu-id="9e57b-155">Encryption type doesn't have to be specified in the url if only one encryption was applied to the asset.</span></span>
* <span data-ttu-id="9e57b-156">加密類型不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="9e57b-156">Encryption type is case insensitive.</span></span>
* <span data-ttu-id="9e57b-157">可以指定下列加密類型︰</span><span class="sxs-lookup"><span data-stu-id="9e57b-157">The following encryption types can be specified:</span></span>  
  * <span data-ttu-id="9e57b-158">**cenc**︰一般加密 (Playready 或 Widevine)</span><span class="sxs-lookup"><span data-stu-id="9e57b-158">**cenc**:  Common encryption (Playready or Widevine)</span></span>
  * <span data-ttu-id="9e57b-159">**cbcs-aapl**：Fairplay</span><span class="sxs-lookup"><span data-stu-id="9e57b-159">**cbcs-aapl**: Fairplay</span></span>
  * <span data-ttu-id="9e57b-160">**cbc**：AES 信封加密。</span><span class="sxs-lookup"><span data-stu-id="9e57b-160">**cbc**: AES envelope encryption.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="9e57b-161">常見案例</span><span class="sxs-lookup"><span data-stu-id="9e57b-161">Common scenarios</span></span>
<span data-ttu-id="9e57b-162">下列主題說明如何保護儲存體中的內容、提供動態加密串流處理媒體、使用 AMS 金鑰/授權傳遞服務</span><span class="sxs-lookup"><span data-stu-id="9e57b-162">The following topics demonstrate how to protect content in storage, deliver dynamically encrypted streaming media, use AMS key/license delivery service</span></span>

* [<span data-ttu-id="9e57b-163">以 AES 保護</span><span class="sxs-lookup"><span data-stu-id="9e57b-163">Protect with AES</span></span>](media-services-protect-with-aes128.md) 
* [<span data-ttu-id="9e57b-164">以 PlayReady 及/或 Widevine 保護 </span><span class="sxs-lookup"><span data-stu-id="9e57b-164">Protect with PlayReady and/or Widevine </span></span>](media-services-protect-with-drm.md)
* [<span data-ttu-id="9e57b-165">串流以 Apple FairPlay 及/或 PlayReady 保護的 HLS 內容</span><span class="sxs-lookup"><span data-stu-id="9e57b-165">Stream your HLS content Protected with Apple FairPlay and/or PlayReady</span></span>](media-services-protect-hls-with-fairplay.md)

### <a name="additional-scenarios"></a><span data-ttu-id="9e57b-166">其他案例</span><span class="sxs-lookup"><span data-stu-id="9e57b-166">Additional scenarios</span></span>
* <span data-ttu-id="9e57b-167">[如何整合 Azure PlayReady 授權服務與您自己的加密程式/串流伺服器](http://mingfeiy.com/integrate-azure-playready-license-service-encryptorstreaming-server)。</span><span class="sxs-lookup"><span data-stu-id="9e57b-167">[How to integrate Azure PlayReady License service with your own encryptor/streaming server](http://mingfeiy.com/integrate-azure-playready-license-service-encryptorstreaming-server).</span></span>
* [<span data-ttu-id="9e57b-168">使用 castLabs 將 DRM 授權傳遞到 Azure 媒體服務</span><span class="sxs-lookup"><span data-stu-id="9e57b-168">Using castLabs to deliver DRM licenses to Azure Media Services</span></span>](media-services-castlabs-integration.md)

>[!NOTE]
><span data-ttu-id="9e57b-169">目前不支援使用外部 DRM 伺服器 (技術) 並從 AMS 進行串流處理的案例。</span><span class="sxs-lookup"><span data-stu-id="9e57b-169">A scenario in which you use an external DRM server(technology) and stream from AMS is currently not supported.</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="9e57b-170">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="9e57b-170">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9e57b-171">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="9e57b-171">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="9e57b-172">相關連結</span><span class="sxs-lookup"><span data-stu-id="9e57b-172">Related Links</span></span>
[<span data-ttu-id="9e57b-173">利用 Azure 媒體服務宣告 PlayReady 是一個服務和 AES 動態加密</span><span class="sxs-lookup"><span data-stu-id="9e57b-173">Announcing PlayReady as a service and AES dynamic encryption with Azure Media Services</span></span>](http://mingfeiy.com/playready)

[<span data-ttu-id="9e57b-174">Azure 媒體服務 PlayReady 授權傳遞定價說明</span><span class="sxs-lookup"><span data-stu-id="9e57b-174">Azure Media Services PlayReady license delivery pricing explained</span></span>](http://mingfeiy.com/playready-pricing-explained-in-azure-media-services)

[<span data-ttu-id="9e57b-175">如何偵錯 Azure 媒體服務的 AES 加密串流</span><span class="sxs-lookup"><span data-stu-id="9e57b-175">How to debug for AES encrypted stream in Azure Media Services</span></span>](http://mingfeiy.com/debug-aes-encrypted-stream-azure-media-services)

[<span data-ttu-id="9e57b-176">JWT 權杖驗證</span><span class="sxs-lookup"><span data-stu-id="9e57b-176">JWT token authenitcation</span></span>](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

<span data-ttu-id="9e57b-177">[整合 Azure 媒體服務 OWIN MVC 型應用程式與 Azure Active Directory 並根據 JWT 宣告限制內容金鑰傳遞](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/)。</span><span class="sxs-lookup"><span data-stu-id="9e57b-177">[Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span></span>

<span data-ttu-id="9e57b-178">[使用 Azure ACS 發行權杖](http://mingfeiy.com/acs-with-key-services)。</span><span class="sxs-lookup"><span data-stu-id="9e57b-178">[Use Azure ACS to issue tokens](http://mingfeiy.com/acs-with-key-services).</span></span>

[content-protection]: ./media/media-services-content-protection-overview/media-services-content-protection.png
