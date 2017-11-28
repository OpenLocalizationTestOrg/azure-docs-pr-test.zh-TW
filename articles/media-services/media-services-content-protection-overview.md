---
title: "aaaProtect 您的內容與 Azure Media Services |Microsoft 文件"
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
ms.openlocfilehash: abab7602d71d7357a692976420ca9a988c0d096f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-content-overview"></a><span data-ttu-id="22e86-103">保護內容概觀</span><span class="sxs-lookup"><span data-stu-id="22e86-103">Protecting content overview</span></span>
<span data-ttu-id="22e86-104">Microsoft Azure Media Services 可讓您 toosecure 離開您的電腦，透過儲存體、 處理和傳遞的 hello 時間從您的媒體。</span><span class="sxs-lookup"><span data-stu-id="22e86-104">Microsoft Azure Media Services enables you toosecure your media from hello time it leaves your computer through storage, processing, and delivery.</span></span> <span data-ttu-id="22e86-105">Media Services 可讓您使用動態加密您的實況和點播內容 toodeliver 進階加密標準 (AES) （使用 128 位元加密金鑰），或任何 hello 主要 DRMs: Microsoft PlayReady、 Google Widevine 和 Apple FairPlay。</span><span class="sxs-lookup"><span data-stu-id="22e86-105">Media Services allows you toodeliver your live and on-demand content encrypted dynamically with Advanced Encryption Standard (AES) (using 128-bit encryption keys) or any of hello major DRMs: Microsoft PlayReady, Google Widevine, and Apple FairPlay.</span></span> <span data-ttu-id="22e86-106">Media Services 也提供傳遞 AES 金鑰的服務並 DRM （PlayReady、 Widevine 和 FairPlay） 授權 tooauthorized 用戶端。</span><span class="sxs-lookup"><span data-stu-id="22e86-106">Media Services also provides a service for delivering AES keys and DRM (PlayReady, Widevine, and FairPlay) licenses tooauthorized clients.</span></span> 

<span data-ttu-id="22e86-107">下列映像的 hello 示範 hello AMS 支援的內容保護工作流程。</span><span class="sxs-lookup"><span data-stu-id="22e86-107">hello following image demonstrates hello content protection workflows that AMS supports.</span></span> 

![利用 PlayReady 保護](./media/media-services-content-protection-overview/media-services-content-protection-with-multi-drm.png)

>[!NOTE]
><span data-ttu-id="22e86-109">AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。</span><span class="sxs-lookup"><span data-stu-id="22e86-109">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="22e86-110">串流處理您的內容，並採取利用動態封裝和動態加密，toostart hello 串流端點，您想要從中 toostream 內容已經在 hello toobe**執行**狀態。</span><span class="sxs-lookup"><span data-stu-id="22e86-110">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

<span data-ttu-id="22e86-111">本主題說明[概念與術語](media-services-content-protection-overview.md)相關 toounderstanding AMS 與內容的保護。</span><span class="sxs-lookup"><span data-stu-id="22e86-111">This topic explains [concepts and terminology](media-services-content-protection-overview.md) relevant toounderstanding content protection with AMS.</span></span> <span data-ttu-id="22e86-112">hello 主題也包含[連結](media-services-content-protection-overview.md#common-scenarios)tootopics 顯示 tooachieve 內容保護工作的方式。</span><span class="sxs-lookup"><span data-stu-id="22e86-112">hello topic also contains [links](media-services-content-protection-overview.md#common-scenarios) tootopics that show how tooachieve content protection tasks.</span></span> 

## <a name="dynamic-encryption"></a><span data-ttu-id="22e86-113">動態加密</span><span class="sxs-lookup"><span data-stu-id="22e86-113">Dynamic encryption</span></span>
<span data-ttu-id="22e86-114">Microsoft Azure Media Services 可讓您的內容動態加密使用 AES 清除金鑰或 DRM 加密 toodeliver: Microsoft PlayReady、 Google Widevine 和 Apple FairPlay。</span><span class="sxs-lookup"><span data-stu-id="22e86-114">Microsoft Azure Media Services enables you toodeliver your content encrypted  dynamically with AES clear key or DRM encryption: Microsoft PlayReady, Google Widevine, and Apple FairPlay.</span></span>

<span data-ttu-id="22e86-115">目前，您可以加密 hello 下列資料流的格式： HLS、 MPEG DASH 和 Smooth Streaming。</span><span class="sxs-lookup"><span data-stu-id="22e86-115">Currently, you can encrypt hello following streaming formats: HLS, MPEG DASH, and Smooth Streaming.</span></span> <span data-ttu-id="22e86-116">您無法加密漸進式下載。</span><span class="sxs-lookup"><span data-stu-id="22e86-116">You cannot encrypt progressive downloads.</span></span>

<span data-ttu-id="22e86-117">如果想要讓 Media Services tooencrypt 資產，您需要與您的 asset tooassociate 加密金鑰 （「 CommonEncryption 」 或 「 EnvelopeEncryption 」），並也可以設定 hello 金鑰授權原則。</span><span class="sxs-lookup"><span data-stu-id="22e86-117">If you want for Media Services tooencrypt an asset, you need tooassociate an encryption key (CommonEncryption or EnvelopeEncryption) with your asset and also configure authorization policies for hello key.</span></span>

<span data-ttu-id="22e86-118">您也需要 tooconfigure hello 資產的傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="22e86-118">You also need tooconfigure hello asset's delivery policy.</span></span> <span data-ttu-id="22e86-119">如果您想 toostream 儲存體加密資產，請確定您想要的 toospecify toodeliver 它藉由設定資產遞送原則。</span><span class="sxs-lookup"><span data-stu-id="22e86-119">If you want toostream a storage encrypted asset, make sure toospecify how you want toodeliver it by configuring asset delivery policy.</span></span>

<span data-ttu-id="22e86-120">Media Services 時，播放程式要求串流時，使用指定的 hello 金鑰 toodynamically 加密您的內容使用 AES 清除金鑰或 DRM 加密。</span><span class="sxs-lookup"><span data-stu-id="22e86-120">When a stream is requested by a player, Media Services uses hello specified key toodynamically encrypt your content using AES clear key or DRM encryption.</span></span> <span data-ttu-id="22e86-121">toodecrypt hello 資料流，hello 播放程式會要求 hello 金鑰從 hello 金鑰傳遞服務。</span><span class="sxs-lookup"><span data-stu-id="22e86-121">toodecrypt hello stream, hello player will request hello key from hello key delivery service.</span></span> <span data-ttu-id="22e86-122">toodecide hello 使用者獲授權 tooget hello 索引鍵，hello 服務會評估您指定 hello 索引鍵的 hello 授權原則。</span><span class="sxs-lookup"><span data-stu-id="22e86-122">toodecide whether or not hello user is authorized tooget hello key, hello service evaluates hello authorization policies that you specified for hello key.</span></span>


## <a name="storage-encryption"></a><span data-ttu-id="22e86-123">儲存體加密</span><span class="sxs-lookup"><span data-stu-id="22e86-123">Storage encryption</span></span>
<span data-ttu-id="22e86-124">使用儲存體加密 tooencrypt 您清除的內容，在本機使用 AES 256 位元加密，然後將它上傳 tooAzure 儲存體的方式予以儲存加密在靜止。</span><span class="sxs-lookup"><span data-stu-id="22e86-124">Use storage encryption tooencrypt your clear content locally using AES 256 bit encryption and then upload it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="22e86-125">使用儲存體加密保護的資產會自動加密，並在 「 加密的檔案系統先前 tooencoding，及選擇性地重新加密的先前 toouploading 回為新輸出資產。</span><span class="sxs-lookup"><span data-stu-id="22e86-125">Assets protected with storage encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="22e86-126">儲存體加密的 hello 主要使用案例是當您想的 toosecure 強式加密您高品質的輸入的媒體檔案放在磁碟。</span><span class="sxs-lookup"><span data-stu-id="22e86-126">hello primary use case for storage encryption is when you want toosecure your high quality input media files with strong encryption at rest on disk.</span></span>

<span data-ttu-id="22e86-127">在順序 toodeliver 儲存體加密資產，您必須設定 hello 資產的傳遞原則，讓媒體服務知道要如何 toodeliver 您的內容。</span><span class="sxs-lookup"><span data-stu-id="22e86-127">In order toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy so Media Services knows how you want toodeliver your content.</span></span> <span data-ttu-id="22e86-128">在您的資產進行串流處理之前，請使用 hello 將內容串流伺服器移除 hello 儲存體加密和資料流的 hello 指定傳遞原則 （例如 AES、 一般加密或不加密）。</span><span class="sxs-lookup"><span data-stu-id="22e86-128">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy (for example, AES, common encryption, or no encryption).</span></span>

## <a name="common-encryption-cenc"></a><span data-ttu-id="22e86-129">一般加密 (CENC)</span><span class="sxs-lookup"><span data-stu-id="22e86-129">Common encryption (CENC)</span></span>
<span data-ttu-id="22e86-130">當使用 PlayReady 或/及 Widewine 加密您的內容時會使用一般加密。</span><span class="sxs-lookup"><span data-stu-id="22e86-130">Common encryption is used when encrypting your content with PlayReady or/and Widewine.</span></span>

## <a name="using-cbcs-aapl-encryption"></a><span data-ttu-id="22e86-131">使用 cbcs-aapl 加密</span><span class="sxs-lookup"><span data-stu-id="22e86-131">Using cbcs-aapl encryption</span></span>
<span data-ttu-id="22e86-132">使用 FairPlay 加密您的內容時會使用 Cbcs-aapl。</span><span class="sxs-lookup"><span data-stu-id="22e86-132">Cbcs-aapl is used when encrypting your content with FairPlay.</span></span>

## <a name="envelope-encryption"></a><span data-ttu-id="22e86-133">信封加密</span><span class="sxs-lookup"><span data-stu-id="22e86-133">Envelope encryption</span></span>
<span data-ttu-id="22e86-134">如果您想要 tooprotect 您的內容與 AES 128 清除金鑰，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="22e86-134">Use this option if you want tooprotect your content with AES-128 clear key.</span></span> <span data-ttu-id="22e86-135">若要更安全的選項，請選擇其中一個 hello DRMs 本主題中列出。</span><span class="sxs-lookup"><span data-stu-id="22e86-135">If you want a more secure option, choose one of hello DRMs listed in this topic.</span></span> 

## <a name="licenses-and-keys-delivery-service"></a><span data-ttu-id="22e86-136">授權和金鑰傳遞服務</span><span class="sxs-lookup"><span data-stu-id="22e86-136">Licenses and keys delivery service</span></span>
<span data-ttu-id="22e86-137">Media Services 提供傳遞 PlayReady、 Widevine (FairPlay） DRM 授權的服務和 AES 清除金鑰 tooauthorized 用戶端。</span><span class="sxs-lookup"><span data-stu-id="22e86-137">Media Services provides a service for delivering DRM (PlayReady, Widevine, FairPlay) licenses and AES clear keys tooauthorized clients.</span></span> <span data-ttu-id="22e86-138">您可以使用[hello Azure 入口網站](media-services-portal-protect-content.md)，REST API 或 Media Services SDK for.NET tooconfigure 授權和驗證原則的授權和金鑰。</span><span class="sxs-lookup"><span data-stu-id="22e86-138">You can use [hello Azure portal](media-services-portal-protect-content.md), REST API, or Media Services SDK for .NET tooconfigure authorization and authentication policies for your licenses and keys.</span></span>

## <a name="token-restriction"></a><span data-ttu-id="22e86-139">權杖限制</span><span class="sxs-lookup"><span data-stu-id="22e86-139">Token restriction</span></span>
<span data-ttu-id="22e86-140">hello 內容金鑰授權原則可能會有一或多個授權限制： 開啟或語彙基元限制。</span><span class="sxs-lookup"><span data-stu-id="22e86-140">hello content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span> <span data-ttu-id="22e86-141">hello 權杖限制的原則必須隨附由安全權杖服務 (STS) 發行的權杖。</span><span class="sxs-lookup"><span data-stu-id="22e86-141">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="22e86-142">Media Services 支援 hello 簡易 Web 權杖 (SWT) 格式和 JSON Web Token (JWT) 格式的權杖。</span><span class="sxs-lookup"><span data-stu-id="22e86-142">Media Services supports tokens in hello Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span></span> <span data-ttu-id="22e86-143">媒體服務不提供安全權杖服務。</span><span class="sxs-lookup"><span data-stu-id="22e86-143">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="22e86-144">您可以建立自訂的 STS，或利用 Microsoft Azure ACS tooissue 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="22e86-144">You can create a custom STS or leverage Microsoft Azure ACS tooissue tokens.</span></span> <span data-ttu-id="22e86-145">hello STS 必須設定以指定的 hello 簽署權杖的 toocreate hello 權杖限制組態中指定的索引鍵和問題的宣告。</span><span class="sxs-lookup"><span data-stu-id="22e86-145">hello STS must be configured toocreate a token signed with hello specified key and issue claims that you specified in hello token restriction configuration.</span></span> <span data-ttu-id="22e86-146">hello Media Services 金鑰傳遞服務會傳回 hello 要求金鑰 （或授權） toohello 用戶端 hello 語彙基元是否有效並 hello 宣告 hello 語彙基元在比對中所設定的 hello 金鑰 （或授權）。</span><span class="sxs-lookup"><span data-stu-id="22e86-146">hello Media Services key delivery service will return hello requested key (or license) toohello client if hello token is valid and hello claims in hello token match those configured for hello key (or license).</span></span>

<span data-ttu-id="22e86-147">在設定 hello 權杖限制的原則時，您必須指定 hello 主要驗證金鑰、 簽發者和對象的參數。</span><span class="sxs-lookup"><span data-stu-id="22e86-147">When configuring hello token restricted policy, you must specify hello primary verification key, issuer and audience parameters.</span></span> <span data-ttu-id="22e86-148">hello 主要驗證金鑰包含 hello 確認 hello 權杖簽署，而且發行者是 hello 安全權杖服務發行 hello 權杖的金鑰。</span><span class="sxs-lookup"><span data-stu-id="22e86-148">hello primary verification key contains hello key that hello token was signed with, issuer is hello secure token service that issues hello token.</span></span> <span data-ttu-id="22e86-149">hello 對象 （有時稱為 「 範圍 」） 說明的 hello 語彙基元的 hello 意圖或 hello 資源 hello 權杖授與存取權。</span><span class="sxs-lookup"><span data-stu-id="22e86-149">hello audience (sometimes called scope) describes hello intent of hello token or hello resource hello token authorizes access to.</span></span> <span data-ttu-id="22e86-150">hello Media Services 金鑰傳遞服務會驗證這些 hello 權杖中的值符合 hello 範本中的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="22e86-150">hello Media Services key delivery service validates that these values in hello token match hello values in hello template.</span></span>

## <a name="streaming-urls"></a><span data-ttu-id="22e86-151">串流 URL</span><span class="sxs-lookup"><span data-stu-id="22e86-151">Streaming URLs</span></span>
<span data-ttu-id="22e86-152">如果您的資產使用一個以上的 DRM 加密，您應該使用的加密標記 hello 串流 URL: (格式 ='m3u8-aapl' 加密 = 'xxx')。</span><span class="sxs-lookup"><span data-stu-id="22e86-152">If your asset was encrypted with more than one DRM, you should use an encryption tag in hello streaming URL: (format='m3u8-aapl', encryption='xxx').</span></span>

<span data-ttu-id="22e86-153">hello 下列考量適用於：</span><span class="sxs-lookup"><span data-stu-id="22e86-153">hello following considerations apply:</span></span>

* <span data-ttu-id="22e86-154">僅可指定零個或一個加密類型。</span><span class="sxs-lookup"><span data-stu-id="22e86-154">Only zero or one encryption type can be specified.</span></span>
* <span data-ttu-id="22e86-155">加密類型沒有 toobe hello url 中指定，如果只有一個加密已套用的 toohello 資產。</span><span class="sxs-lookup"><span data-stu-id="22e86-155">Encryption type doesn't have toobe specified in hello url if only one encryption was applied toohello asset.</span></span>
* <span data-ttu-id="22e86-156">加密類型不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="22e86-156">Encryption type is case insensitive.</span></span>
* <span data-ttu-id="22e86-157">您可以指定下列加密類型的 hello:</span><span class="sxs-lookup"><span data-stu-id="22e86-157">hello following encryption types can be specified:</span></span>  
  * <span data-ttu-id="22e86-158">**cenc**︰一般加密 (Playready 或 Widevine)</span><span class="sxs-lookup"><span data-stu-id="22e86-158">**cenc**:  Common encryption (Playready or Widevine)</span></span>
  * <span data-ttu-id="22e86-159">**cbcs-aapl**：Fairplay</span><span class="sxs-lookup"><span data-stu-id="22e86-159">**cbcs-aapl**: Fairplay</span></span>
  * <span data-ttu-id="22e86-160">**cbc**：AES 信封加密。</span><span class="sxs-lookup"><span data-stu-id="22e86-160">**cbc**: AES envelope encryption.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="22e86-161">常見案例</span><span class="sxs-lookup"><span data-stu-id="22e86-161">Common scenarios</span></span>
<span data-ttu-id="22e86-162">hello 下列主題示範如何在儲存體，tooprotect 內容傳遞動態加密進行媒體串流處理，使用 AMS 金鑰/授權傳遞服務</span><span class="sxs-lookup"><span data-stu-id="22e86-162">hello following topics demonstrate how tooprotect content in storage, deliver dynamically encrypted streaming media, use AMS key/license delivery service</span></span>

* [<span data-ttu-id="22e86-163">以 AES 保護</span><span class="sxs-lookup"><span data-stu-id="22e86-163">Protect with AES</span></span>](media-services-protect-with-aes128.md) 
* [<span data-ttu-id="22e86-164">以 PlayReady 及/或 Widevine 保護 </span><span class="sxs-lookup"><span data-stu-id="22e86-164">Protect with PlayReady and/or Widevine </span></span>](media-services-protect-with-drm.md)
* [<span data-ttu-id="22e86-165">串流以 Apple FairPlay 及/或 PlayReady 保護的 HLS 內容</span><span class="sxs-lookup"><span data-stu-id="22e86-165">Stream your HLS content Protected with Apple FairPlay and/or PlayReady</span></span>](media-services-protect-hls-with-fairplay.md)

### <a name="additional-scenarios"></a><span data-ttu-id="22e86-166">其他案例</span><span class="sxs-lookup"><span data-stu-id="22e86-166">Additional scenarios</span></span>
* <span data-ttu-id="22e86-167">[如何 toointegrate Azure PlayReady 授權服務與您自己的加密程式/串流伺服器](http://mingfeiy.com/integrate-azure-playready-license-service-encryptorstreaming-server)。</span><span class="sxs-lookup"><span data-stu-id="22e86-167">[How toointegrate Azure PlayReady License service with your own encryptor/streaming server](http://mingfeiy.com/integrate-azure-playready-license-service-encryptorstreaming-server).</span></span>
* [<span data-ttu-id="22e86-168">使用 castLabs toodeliver DRM 授權 tooAzure 媒體服務</span><span class="sxs-lookup"><span data-stu-id="22e86-168">Using castLabs toodeliver DRM licenses tooAzure Media Services</span></span>](media-services-castlabs-integration.md)

>[!NOTE]
><span data-ttu-id="22e86-169">目前不支援使用外部 DRM 伺服器 (技術) 並從 AMS 進行串流處理的案例。</span><span class="sxs-lookup"><span data-stu-id="22e86-169">A scenario in which you use an external DRM server(technology) and stream from AMS is currently not supported.</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="22e86-170">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="22e86-170">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="22e86-171">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="22e86-171">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="22e86-172">相關連結</span><span class="sxs-lookup"><span data-stu-id="22e86-172">Related Links</span></span>
[<span data-ttu-id="22e86-173">利用 Azure 媒體服務宣告 PlayReady 是一個服務和 AES 動態加密</span><span class="sxs-lookup"><span data-stu-id="22e86-173">Announcing PlayReady as a service and AES dynamic encryption with Azure Media Services</span></span>](http://mingfeiy.com/playready)

[<span data-ttu-id="22e86-174">Azure 媒體服務 PlayReady 授權傳遞定價說明</span><span class="sxs-lookup"><span data-stu-id="22e86-174">Azure Media Services PlayReady license delivery pricing explained</span></span>](http://mingfeiy.com/playready-pricing-explained-in-azure-media-services)

[<span data-ttu-id="22e86-175">Toodebug aes 加密 Azure 媒體服務中的資料流的方式</span><span class="sxs-lookup"><span data-stu-id="22e86-175">How toodebug for AES encrypted stream in Azure Media Services</span></span>](http://mingfeiy.com/debug-aes-encrypted-stream-azure-media-services)

[<span data-ttu-id="22e86-176">JWT 權杖驗證</span><span class="sxs-lookup"><span data-stu-id="22e86-176">JWT token authenitcation</span></span>](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

<span data-ttu-id="22e86-177">[整合 Azure 媒體服務 OWIN MVC 型應用程式與 Azure Active Directory 並根據 JWT 宣告限制內容金鑰傳遞](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/)。</span><span class="sxs-lookup"><span data-stu-id="22e86-177">[Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span></span>

<span data-ttu-id="22e86-178">[使用 Azure ACS tooissue 語彙基元](http://mingfeiy.com/acs-with-key-services)。</span><span class="sxs-lookup"><span data-stu-id="22e86-178">[Use Azure ACS tooissue tokens](http://mingfeiy.com/acs-with-key-services).</span></span>

[content-protection]: ./media/media-services-content-protection-overview/media-services-content-protection.png
