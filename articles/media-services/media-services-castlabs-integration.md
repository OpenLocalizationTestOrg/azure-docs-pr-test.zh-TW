---
title: "aaaUsing castLabs toodeliver Widevine 授權 tooAzure Media Services |Microsoft 文件"
description: "本文說明如何使用 Azure 媒體服務 (AMS) toodeliver 以 PlayReady 和 Widevine DRMs AMS 動態加密的資料流。 hello PlayReady 授權來自 Media Services PlayReady 授權伺服器，並 Widevine 授權傳遞 castLabs 授權伺服器。"
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 2a9a408a-a995-49e1-8d8f-ac5b51e17d40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: Mingfeiy;willzhan;Juliako
ms.openlocfilehash: 80d2778fb283a96361e7e511990a36c2f551a310
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-castlabs-toodeliver-widevine-licenses-tooazure-media-services"></a><span data-ttu-id="92897-104">使用 castLabs toodeliver Widevine 授權 tooAzure 媒體服務</span><span class="sxs-lookup"><span data-stu-id="92897-104">Using castLabs toodeliver Widevine licenses tooAzure Media Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="92897-105">Axinom</span><span class="sxs-lookup"><span data-stu-id="92897-105">Axinom</span></span>](media-services-axinom-integration.md)
> * [<span data-ttu-id="92897-106">castLabs</span><span class="sxs-lookup"><span data-stu-id="92897-106">castLabs</span></span>](media-services-castlabs-integration.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="92897-107">概觀</span><span class="sxs-lookup"><span data-stu-id="92897-107">Overview</span></span>
<span data-ttu-id="92897-108">本文說明如何使用 Azure 媒體服務 (AMS) toodeliver 以 PlayReady 和 Widevine DRMs AMS 動態加密的資料流。</span><span class="sxs-lookup"><span data-stu-id="92897-108">This article describes how you can use Azure Media Services (AMS) toodeliver a stream that is dynamically encrypted by AMS with both PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="92897-109">hello PlayReady 授權來自 Media Services PlayReady 授權伺服器，且傳遞 Widevine 授權**castLabs**授權伺服器。</span><span class="sxs-lookup"><span data-stu-id="92897-109">hello PlayReady license comes from Media Services PlayReady license server and Widevine license is delivered by **castLabs** license server.</span></span>

<span data-ttu-id="92897-110">tooplayback 串流處理受保護的內容由 CENC （PlayReady 和/或 Widevine），您可以使用[Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html)。</span><span class="sxs-lookup"><span data-stu-id="92897-110">tooplayback streaming content protected by CENC (PlayReady and/or Widevine), you can use  [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="92897-111">如需詳細資訊，請參閱 [AMP 文件](http://amp.azure.net/libs/amp/latest/docs/) 。</span><span class="sxs-lookup"><span data-stu-id="92897-111">See [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details.</span></span>

<span data-ttu-id="92897-112">下列圖表中的 hello 示範高層級的 Azure 媒體服務和 castLabs 整合架構。</span><span class="sxs-lookup"><span data-stu-id="92897-112">hello following diagram demonstrates a high-level Azure Media Services and castLabs integration architecture.</span></span>

![整合](./media/media-services-castlabs-integration/media-services-castlabs-integration.png)

## <a name="typical-system-set-up"></a><span data-ttu-id="92897-114">一般系統設定</span><span class="sxs-lookup"><span data-stu-id="92897-114">Typical system set up</span></span>
* <span data-ttu-id="92897-115">媒體內容儲存在 AMS 中。</span><span class="sxs-lookup"><span data-stu-id="92897-115">Media content is stored in AMS.</span></span>
* <span data-ttu-id="92897-116">內容金鑰的金鑰識別碼儲存在 castLabs 與 AMS 中。</span><span class="sxs-lookup"><span data-stu-id="92897-116">Key IDs of content keys are stored in both castLabs and AMS.</span></span>
* <span data-ttu-id="92897-117">castLabs 與 AMS 皆有內建權杖驗證。</span><span class="sxs-lookup"><span data-stu-id="92897-117">castLabs and AMS both have token authentication built in.</span></span> <span data-ttu-id="92897-118">hello 下列各節討論驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="92897-118">hello following sections discuss authentication tokens.</span></span> 
* <span data-ttu-id="92897-119">當用戶端要求 toostream hello 視訊時，hello 內容動態加密**一般加密**(CENC) 和動態 AMS tooSmooth 來封裝資料流和虛線。</span><span class="sxs-lookup"><span data-stu-id="92897-119">When a client requests toostream hello video, hello content is dynamically encrypted with **Common Encryption** (CENC) and dynamically packaged by AMS tooSmooth Streaming and DASH.</span></span> <span data-ttu-id="92897-120">我們也會針對 HLS 串流通訊協定傳遞 PlayReady M2TS 基礎資料流加密。</span><span class="sxs-lookup"><span data-stu-id="92897-120">We also deliver PlayReady M2TS elementary stream encryption for HLS streaming protocol.</span></span>
* <span data-ttu-id="92897-121">PlayReady 授權擷取自 AMS 授權伺服器，Widevine 授權擷取自 castLabs 授權伺服器。</span><span class="sxs-lookup"><span data-stu-id="92897-121">PlayReady license is retrieved from AMS license server and Widevine license is retrieved from castLabs license server.</span></span> 
* <span data-ttu-id="92897-122">Media Player 會自動決定哪些授權 toofetch，根據 hello 用戶端的平台功能。</span><span class="sxs-lookup"><span data-stu-id="92897-122">Media Player automatically decides which license toofetch based on hello client platform capability.</span></span> 

## <a name="authentication-token-generation-for-getting-a-license"></a><span data-ttu-id="92897-123">產生驗證權杖以取得授權</span><span class="sxs-lookup"><span data-stu-id="92897-123">Authentication token generation for getting a license</span></span>
<span data-ttu-id="92897-124">CastLabs 和 AMS 支援 JWT （JSON Web 權杖） 使用的權杖格式 tooauthorize 授權。</span><span class="sxs-lookup"><span data-stu-id="92897-124">Both castLabs and AMS support JWT (JSON Web Token) token format used tooauthorize a license.</span></span> 

### <a name="jwt-token-in-ams"></a><span data-ttu-id="92897-125">AMS 中的 JWT 權杖</span><span class="sxs-lookup"><span data-stu-id="92897-125">JWT token in AMS</span></span>
<span data-ttu-id="92897-126">hello 下表描述 AMS 中的 JWT 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="92897-126">hello following table describes JWT token in AMS.</span></span> 

| <span data-ttu-id="92897-127">簽發者</span><span class="sxs-lookup"><span data-stu-id="92897-127">Issuer</span></span> | <span data-ttu-id="92897-128">簽發者字串 hello 選擇安全權杖服務 (STS)</span><span class="sxs-lookup"><span data-stu-id="92897-128">Issuer string from hello chosen Secure Token Service (STS)</span></span> |
| --- | --- |
| <span data-ttu-id="92897-129">對象</span><span class="sxs-lookup"><span data-stu-id="92897-129">Audience</span></span> |<span data-ttu-id="92897-130">使用 STS 從 hello 的對象字串。</span><span class="sxs-lookup"><span data-stu-id="92897-130">Audience string from hello used STS</span></span> |
| <span data-ttu-id="92897-131">Claims</span><span class="sxs-lookup"><span data-stu-id="92897-131">Claims</span></span> |<span data-ttu-id="92897-132">一組宣告</span><span class="sxs-lookup"><span data-stu-id="92897-132">A set of claims</span></span> |
| <span data-ttu-id="92897-133">NotBefore</span><span class="sxs-lookup"><span data-stu-id="92897-133">NotBefore</span></span> |<span data-ttu-id="92897-134">啟動 hello 語彙基元的有效性</span><span class="sxs-lookup"><span data-stu-id="92897-134">Start validity of hello token</span></span> |
| <span data-ttu-id="92897-135">Expires</span><span class="sxs-lookup"><span data-stu-id="92897-135">Expires</span></span> |<span data-ttu-id="92897-136">Hello 語彙基元的結束有效性</span><span class="sxs-lookup"><span data-stu-id="92897-136">End validity of hello token</span></span> |
| <span data-ttu-id="92897-137">SigningCredentials</span><span class="sxs-lookup"><span data-stu-id="92897-137">SigningCredentials</span></span> |<span data-ttu-id="92897-138">PlayReady 授權伺服器，授權伺服器與 STS，castLabs 之間共用的 hello 索引鍵可能是對稱或非對稱金鑰。</span><span class="sxs-lookup"><span data-stu-id="92897-138">hello key that is shared among PlayReady License Server, castLabs License Server and STS, it could be either symmetric or asymmetric key.</span></span> |

### <a name="jwt-token-in-castlabs"></a><span data-ttu-id="92897-139">castLabs 中的 JWT 權杖</span><span class="sxs-lookup"><span data-stu-id="92897-139">JWT token in castLabs</span></span>
<span data-ttu-id="92897-140">hello 下表描述 castLabs 中的 JWT 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="92897-140">hello following table describes JWT token in castLabs.</span></span> 

| <span data-ttu-id="92897-141">名稱</span><span class="sxs-lookup"><span data-stu-id="92897-141">Name</span></span> | <span data-ttu-id="92897-142">說明</span><span class="sxs-lookup"><span data-stu-id="92897-142">Description</span></span> |
| --- | --- |
| <span data-ttu-id="92897-143">optData</span><span class="sxs-lookup"><span data-stu-id="92897-143">optData</span></span> |<span data-ttu-id="92897-144">JSON 字串，其中包含您的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="92897-144">A JSON string containing information about you.</span></span> |
| <span data-ttu-id="92897-145">crt</span><span class="sxs-lookup"><span data-stu-id="92897-145">crt</span></span> |<span data-ttu-id="92897-146">含有 hello 資產的相關資訊的 JSON 字串，它的授權資訊與播放權限。</span><span class="sxs-lookup"><span data-stu-id="92897-146">A JSON string containing information about hello asset, its license info and playback rights.</span></span> |
| <span data-ttu-id="92897-147">iat</span><span class="sxs-lookup"><span data-stu-id="92897-147">iat</span></span> |<span data-ttu-id="92897-148">epoch hello 目前日期時間。</span><span class="sxs-lookup"><span data-stu-id="92897-148">hello current datetime in epoch.</span></span> |
| <span data-ttu-id="92897-149">jti</span><span class="sxs-lookup"><span data-stu-id="92897-149">jti</span></span> |<span data-ttu-id="92897-150">有關這個語彙基元 （每個權杖可以只用一次在 hello castLabs 系統） 的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="92897-150">A unique identifier about this token (every token can only be used once in hello castLabs system).</span></span> |

## <a name="sample-solution-set-up"></a><span data-ttu-id="92897-151">範例解決方案設定</span><span class="sxs-lookup"><span data-stu-id="92897-151">Sample solution set up</span></span>
<span data-ttu-id="92897-152">hello[範例方案](https://github.com/AzureMediaServicesSamples/CastlabsIntegration)包含兩個專案：</span><span class="sxs-lookup"><span data-stu-id="92897-152">hello [sample solution](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) consists of two projects:</span></span>

* <span data-ttu-id="92897-153">可以是使用的 tooset DRM 的限制已經內嵌的資產，PlayReady 和 Widevine 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="92897-153">A console app that can be used tooset DRM restrictions on an already ingested asset, for both PlayReady and Widevine.</span></span>
* <span data-ttu-id="92897-154">Web 應用程式，用於遞出權杖，可視為「非常簡易」的 STS 版本。</span><span class="sxs-lookup"><span data-stu-id="92897-154">A Web Application that hands out tokens, which could be seen as a VERY SIMPLIFIED version of an STS.</span></span>

<span data-ttu-id="92897-155">toouse hello 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="92897-155">toouse hello console application:</span></span>

1. <span data-ttu-id="92897-156">變更 hello app.config toosetup AMS 認證、 castLabs 認證、 STS 組態和共用的金鑰。</span><span class="sxs-lookup"><span data-stu-id="92897-156">Change hello app.config toosetup AMS credentials, castLabs credentials, STS configuration and shared key.</span></span>
2. <span data-ttu-id="92897-157">將資產上傳到 AMS。</span><span class="sxs-lookup"><span data-stu-id="92897-157">Upload an Asset into AMS.</span></span>
3. <span data-ttu-id="92897-158">從 hello get hello UUID 上傳資產，並變更 hello Program.cs 檔案中的行 32:</span><span class="sxs-lookup"><span data-stu-id="92897-158">Get hello UUID from hello uploaded Asset, and change Line 32 in hello Program.cs file:</span></span>
   
      <span data-ttu-id="92897-159">var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();</span><span class="sxs-lookup"><span data-stu-id="92897-159">var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();</span></span>
4. <span data-ttu-id="92897-160">使用命名 hello castLabs 系統 (hello Program.cs 檔案中的行 44) 中的 hello 資產的 AssetId。</span><span class="sxs-lookup"><span data-stu-id="92897-160">Use an AssetId for naming hello asset in hello castLabs system (Line 44 in hello Program.cs file).</span></span>
   
   <span data-ttu-id="92897-161">您必須設定為 AssetId **castLabs**; 它必須 toobe 唯一英數字串。</span><span class="sxs-lookup"><span data-stu-id="92897-161">You must set AssetId for **castLabs**; it needs toobe a unique alphanumeric string.</span></span>
5. <span data-ttu-id="92897-162">執行 hello 程式。</span><span class="sxs-lookup"><span data-stu-id="92897-162">Run hello program.</span></span>

<span data-ttu-id="92897-163">toouse hello Web 應用程式 (STS):</span><span class="sxs-lookup"><span data-stu-id="92897-163">toouse hello Web Application (STS):</span></span>

1. <span data-ttu-id="92897-164">變更 hello web.config toosetup castlabs 商店識別碼、 hello STS 組態和 hello 共用的金鑰。</span><span class="sxs-lookup"><span data-stu-id="92897-164">Change hello web.config toosetup castlabs merchant ID, hello STS configuration and hello shared key.</span></span>
2. <span data-ttu-id="92897-165">部署 tooAzure 網站。</span><span class="sxs-lookup"><span data-stu-id="92897-165">Deploy tooAzure Websites.</span></span>
3. <span data-ttu-id="92897-166">瀏覽 toohello 網站。</span><span class="sxs-lookup"><span data-stu-id="92897-166">Navigate toohello website.</span></span>

## <a name="playing-back-a-video"></a><span data-ttu-id="92897-167">播放視訊</span><span class="sxs-lookup"><span data-stu-id="92897-167">Playing back a video</span></span>
<span data-ttu-id="92897-168">使用一般加密 （PlayReady 和/或 Widevine） 的 tooplayback 視訊加密，您可以使用 hello [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html)。</span><span class="sxs-lookup"><span data-stu-id="92897-168">tooplayback a video encrypted with common encryption (PlayReady and/or Widevine), you can use hello [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="92897-169">當執行 hello 主控台應用程式時，會回應 hello 內容金鑰識別碼和 hello 資訊清單的 URL。</span><span class="sxs-lookup"><span data-stu-id="92897-169">When running hello console app, hello Content Key ID and hello Manifest URL are echoed.</span></span>

1. <span data-ttu-id="92897-170">開啟新索引標籤，並啟動 STS：http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid]。</span><span class="sxs-lookup"><span data-stu-id="92897-170">Open a new tab and launch your STS: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].</span></span>
2. <span data-ttu-id="92897-171">跳過[Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html)。</span><span class="sxs-lookup"><span data-stu-id="92897-171">Go too[Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
3. <span data-ttu-id="92897-172">在 hello 串流 URL 中貼上。</span><span class="sxs-lookup"><span data-stu-id="92897-172">Paste in hello streaming URL.</span></span>
4. <span data-ttu-id="92897-173">按一下 hello**進階選項**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="92897-173">Click hello **Advanced Options** checkbox.</span></span>
5. <span data-ttu-id="92897-174">在 hello**保護**下拉式清單中，選取 PlayReady 和/或 Widevine。</span><span class="sxs-lookup"><span data-stu-id="92897-174">In hello **Protection** dropdown, select PlayReady and/or Widevine.</span></span>
6. <span data-ttu-id="92897-175">貼上您向您的 STS hello 語彙基元文字方塊中的 hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="92897-175">Paste hello token that you got from your STS in hello Token textbox.</span></span> 
   
   <span data-ttu-id="92897-176">hello castLab 授權伺服器不需要 hello"Bearer ="hello 權杖前面的前置詞。</span><span class="sxs-lookup"><span data-stu-id="92897-176">hello castLab license server does not need hello “Bearer=” prefix in front of hello token.</span></span> <span data-ttu-id="92897-177">因此請先移除，再送出 hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="92897-177">So please remove that before submitting hello token.</span></span>
7. <span data-ttu-id="92897-178">更新 hello 播放程式。</span><span class="sxs-lookup"><span data-stu-id="92897-178">Update hello player.</span></span>
8. <span data-ttu-id="92897-179">應該播放視訊的 hello。</span><span class="sxs-lookup"><span data-stu-id="92897-179">hello video should be playing.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="92897-180">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="92897-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="92897-181">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="92897-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

