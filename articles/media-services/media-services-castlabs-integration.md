---
title: "使用 castLabs 將 Widevine 授權傳遞到 Azure 媒體服務 | Microsoft Docs"
description: "本文說明如何使用 Azure 媒體服務 (AMS) 來傳遞 AMS 使用 PlayReady 與 Widevine DRM 動態加密的資料流。 PlayReady 授權來自媒體服務 PlayReady 授權伺服器，Widevine 授權由 castLabs 授權伺服器傳遞。"
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
ms.openlocfilehash: 5b69e804809f834e81221fb2787a997a52dbe286
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="using-castlabs-to-deliver-widevine-licenses-to-azure-media-services"></a><span data-ttu-id="bad03-104">使用 castLabs 將 Widevine 授權傳遞到 Azure 媒體服務</span><span class="sxs-lookup"><span data-stu-id="bad03-104">Using castLabs to deliver Widevine licenses to Azure Media Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bad03-105">Axinom</span><span class="sxs-lookup"><span data-stu-id="bad03-105">Axinom</span></span>](media-services-axinom-integration.md)
> * [<span data-ttu-id="bad03-106">castLabs</span><span class="sxs-lookup"><span data-stu-id="bad03-106">castLabs</span></span>](media-services-castlabs-integration.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="bad03-107">Overview</span><span class="sxs-lookup"><span data-stu-id="bad03-107">Overview</span></span>
<span data-ttu-id="bad03-108">本文說明如何使用 Azure 媒體服務 (AMS) 來傳遞 AMS 使用 PlayReady 與 Widevine DRM 動態加密的資料流。</span><span class="sxs-lookup"><span data-stu-id="bad03-108">This article describes how you can use Azure Media Services (AMS) to deliver a stream that is dynamically encrypted by AMS with both PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="bad03-109">PlayReady 授權來自媒體服務 PlayReady 授權伺服器，Widevine 授權則來自 **castLabs** 授權伺服器。</span><span class="sxs-lookup"><span data-stu-id="bad03-109">The PlayReady license comes from Media Services PlayReady license server and Widevine license is delivered by **castLabs** license server.</span></span>

<span data-ttu-id="bad03-110">若要播放受 CENC (PlayReady 和/或 Widevine) 保護的串流內容，您可以使用 [Azure 媒體播放器](http://amsplayer.azurewebsites.net/azuremediaplayer.html) 。</span><span class="sxs-lookup"><span data-stu-id="bad03-110">To playback streaming content protected by CENC (PlayReady and/or Widevine), you can use  [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="bad03-111">如需詳細資訊，請參閱 [AMP 文件](http://amp.azure.net/libs/amp/latest/docs/) 。</span><span class="sxs-lookup"><span data-stu-id="bad03-111">See [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details.</span></span>

<span data-ttu-id="bad03-112">以下為 Azure 媒體服務與 castLabs 整合架構概況圖。</span><span class="sxs-lookup"><span data-stu-id="bad03-112">The following diagram demonstrates a high-level Azure Media Services and castLabs integration architecture.</span></span>

![整合](./media/media-services-castlabs-integration/media-services-castlabs-integration.png)

## <a name="typical-system-set-up"></a><span data-ttu-id="bad03-114">一般系統設定</span><span class="sxs-lookup"><span data-stu-id="bad03-114">Typical system set up</span></span>
* <span data-ttu-id="bad03-115">媒體內容儲存在 AMS 中。</span><span class="sxs-lookup"><span data-stu-id="bad03-115">Media content is stored in AMS.</span></span>
* <span data-ttu-id="bad03-116">內容金鑰的金鑰識別碼儲存在 castLabs 與 AMS 中。</span><span class="sxs-lookup"><span data-stu-id="bad03-116">Key IDs of content keys are stored in both castLabs and AMS.</span></span>
* <span data-ttu-id="bad03-117">castLabs 與 AMS 皆有內建權杖驗證。</span><span class="sxs-lookup"><span data-stu-id="bad03-117">castLabs and AMS both have token authentication built in.</span></span> <span data-ttu-id="bad03-118">以下幾節將會討論驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="bad03-118">The following sections discuss authentication tokens.</span></span> 
* <span data-ttu-id="bad03-119">用戶端要求串流視訊時，AMS 會使用 **一般加密** (CENC) 動態加密內容，並動態封裝到 Smooth Streaming 與 DASH。</span><span class="sxs-lookup"><span data-stu-id="bad03-119">When a client requests to stream the video, the content is dynamically encrypted with **Common Encryption** (CENC) and dynamically packaged by AMS to Smooth Streaming and DASH.</span></span> <span data-ttu-id="bad03-120">我們也會針對 HLS 串流通訊協定傳遞 PlayReady M2TS 基礎資料流加密。</span><span class="sxs-lookup"><span data-stu-id="bad03-120">We also deliver PlayReady M2TS elementary stream encryption for HLS streaming protocol.</span></span>
* <span data-ttu-id="bad03-121">PlayReady 授權擷取自 AMS 授權伺服器，Widevine 授權擷取自 castLabs 授權伺服器。</span><span class="sxs-lookup"><span data-stu-id="bad03-121">PlayReady license is retrieved from AMS license server and Widevine license is retrieved from castLabs license server.</span></span> 
* <span data-ttu-id="bad03-122">媒體播放器會根據平台功能自動決定提取哪些授權。</span><span class="sxs-lookup"><span data-stu-id="bad03-122">Media Player automatically decides which license to fetch based on the client platform capability.</span></span> 

## <a name="authentication-token-generation-for-getting-a-license"></a><span data-ttu-id="bad03-123">產生驗證權杖以取得授權</span><span class="sxs-lookup"><span data-stu-id="bad03-123">Authentication token generation for getting a license</span></span>
<span data-ttu-id="bad03-124">castLabs 與 AMS 皆支援使用 JWT (JSON Web Token) 權杖格式進行授權。</span><span class="sxs-lookup"><span data-stu-id="bad03-124">Both castLabs and AMS support JWT (JSON Web Token) token format used to authorize a license.</span></span> 

### <a name="jwt-token-in-ams"></a><span data-ttu-id="bad03-125">AMS 中的 JWT 權杖</span><span class="sxs-lookup"><span data-stu-id="bad03-125">JWT token in AMS</span></span>
<span data-ttu-id="bad03-126">下表說明 AMS 中的 JWT 權杖。</span><span class="sxs-lookup"><span data-stu-id="bad03-126">The following table describes JWT token in AMS.</span></span> 

| <span data-ttu-id="bad03-127">簽發者</span><span class="sxs-lookup"><span data-stu-id="bad03-127">Issuer</span></span> | <span data-ttu-id="bad03-128">所選安全權杖服務 (STS) 中的簽發者字串</span><span class="sxs-lookup"><span data-stu-id="bad03-128">Issuer string from the chosen Secure Token Service (STS)</span></span> |
| --- | --- |
| <span data-ttu-id="bad03-129">Audience</span><span class="sxs-lookup"><span data-stu-id="bad03-129">Audience</span></span> |<span data-ttu-id="bad03-130">所使用 STS 中的對象字串</span><span class="sxs-lookup"><span data-stu-id="bad03-130">Audience string from the used STS</span></span> |
| <span data-ttu-id="bad03-131">Claims</span><span class="sxs-lookup"><span data-stu-id="bad03-131">Claims</span></span> |<span data-ttu-id="bad03-132">一組宣告</span><span class="sxs-lookup"><span data-stu-id="bad03-132">A set of claims</span></span> |
| <span data-ttu-id="bad03-133">NotBefore</span><span class="sxs-lookup"><span data-stu-id="bad03-133">NotBefore</span></span> |<span data-ttu-id="bad03-134">權杖的生效日期</span><span class="sxs-lookup"><span data-stu-id="bad03-134">Start validity of the token</span></span> |
| <span data-ttu-id="bad03-135">Expires</span><span class="sxs-lookup"><span data-stu-id="bad03-135">Expires</span></span> |<span data-ttu-id="bad03-136">權杖的有效期限</span><span class="sxs-lookup"><span data-stu-id="bad03-136">End validity of the token</span></span> |
| <span data-ttu-id="bad03-137">SigningCredentials</span><span class="sxs-lookup"><span data-stu-id="bad03-137">SigningCredentials</span></span> |<span data-ttu-id="bad03-138">PlayReady 授權伺服器、castLabs 授權伺服器與 STS 之間共用的金鑰，可以是對稱或非對稱金鑰。</span><span class="sxs-lookup"><span data-stu-id="bad03-138">The key that is shared among PlayReady License Server, castLabs License Server and STS, it could be either symmetric or asymmetric key.</span></span> |

### <a name="jwt-token-in-castlabs"></a><span data-ttu-id="bad03-139">castLabs 中的 JWT 權杖</span><span class="sxs-lookup"><span data-stu-id="bad03-139">JWT token in castLabs</span></span>
<span data-ttu-id="bad03-140">下表說明 castLabs 中的 JWT 權杖。</span><span class="sxs-lookup"><span data-stu-id="bad03-140">The following table describes JWT token in castLabs.</span></span> 

| <span data-ttu-id="bad03-141">名稱</span><span class="sxs-lookup"><span data-stu-id="bad03-141">Name</span></span> | <span data-ttu-id="bad03-142">說明</span><span class="sxs-lookup"><span data-stu-id="bad03-142">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bad03-143">optData</span><span class="sxs-lookup"><span data-stu-id="bad03-143">optData</span></span> |<span data-ttu-id="bad03-144">JSON 字串，其中包含您的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="bad03-144">A JSON string containing information about you.</span></span> |
| <span data-ttu-id="bad03-145">crt</span><span class="sxs-lookup"><span data-stu-id="bad03-145">crt</span></span> |<span data-ttu-id="bad03-146">JSON 字串，其中包含資產、其授權資訊與播放權限的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="bad03-146">A JSON string containing information about the asset, its license info and playback rights.</span></span> |
| <span data-ttu-id="bad03-147">iat</span><span class="sxs-lookup"><span data-stu-id="bad03-147">iat</span></span> |<span data-ttu-id="bad03-148">Epoch 中目前的日期時間。</span><span class="sxs-lookup"><span data-stu-id="bad03-148">The current datetime in epoch.</span></span> |
| <span data-ttu-id="bad03-149">jti</span><span class="sxs-lookup"><span data-stu-id="bad03-149">jti</span></span> |<span data-ttu-id="bad03-150">權杖的唯一識別碼 (每個權杖在 castLabs 系統中只使用一次)。</span><span class="sxs-lookup"><span data-stu-id="bad03-150">A unique identifier about this token (every token can only be used once in the castLabs system).</span></span> |

## <a name="sample-solution-set-up"></a><span data-ttu-id="bad03-151">範例解決方案設定</span><span class="sxs-lookup"><span data-stu-id="bad03-151">Sample solution set up</span></span>
<span data-ttu-id="bad03-152">[範例解決方案](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) 包含兩個專案：</span><span class="sxs-lookup"><span data-stu-id="bad03-152">The [sample solution](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) consists of two projects:</span></span>

* <span data-ttu-id="bad03-153">主控台應用程式，用於為 PlayReady 與 Widevine 在已內嵌的資產上設定 DRM 限制。</span><span class="sxs-lookup"><span data-stu-id="bad03-153">A console app that can be used to set DRM restrictions on an already ingested asset, for both PlayReady and Widevine.</span></span>
* <span data-ttu-id="bad03-154">Web 應用程式，用於遞出權杖，可視為「非常簡易」的 STS 版本。</span><span class="sxs-lookup"><span data-stu-id="bad03-154">A Web Application that hands out tokens, which could be seen as a VERY SIMPLIFIED version of an STS.</span></span>

<span data-ttu-id="bad03-155">若要使用主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="bad03-155">To use the console application:</span></span>

1. <span data-ttu-id="bad03-156">變更 app.config 以設定 AMS 認證、castLabs 認證、STS 組態及共用的金鑰。</span><span class="sxs-lookup"><span data-stu-id="bad03-156">Change the app.config to setup AMS credentials, castLabs credentials, STS configuration and shared key.</span></span>
2. <span data-ttu-id="bad03-157">將資產上傳到 AMS。</span><span class="sxs-lookup"><span data-stu-id="bad03-157">Upload an Asset into AMS.</span></span>
3. <span data-ttu-id="bad03-158">從已上傳的資產中取得 UUID，然後變更 Program.cs 檔中的行 32：</span><span class="sxs-lookup"><span data-stu-id="bad03-158">Get the UUID from the uploaded Asset, and change Line 32 in the Program.cs file:</span></span>
   
      <span data-ttu-id="bad03-159">var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();</span><span class="sxs-lookup"><span data-stu-id="bad03-159">var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();</span></span>
4. <span data-ttu-id="bad03-160">使用 AssetId 命名 castLabs 系統中的資產 (Program.cs 檔中的行 44)。</span><span class="sxs-lookup"><span data-stu-id="bad03-160">Use an AssetId for naming the asset in the castLabs system (Line 44 in the Program.cs file).</span></span>
   
   <span data-ttu-id="bad03-161">您必須設定 **castLabs**的 AssetId；必須是唯一的英數字元字串。</span><span class="sxs-lookup"><span data-stu-id="bad03-161">You must set AssetId for **castLabs**; it needs to be a unique alphanumeric string.</span></span>
5. <span data-ttu-id="bad03-162">執行程式。</span><span class="sxs-lookup"><span data-stu-id="bad03-162">Run the program.</span></span>

<span data-ttu-id="bad03-163">若要使用 Web 應用程式 (STS)：</span><span class="sxs-lookup"><span data-stu-id="bad03-163">To use the Web Application (STS):</span></span>

1. <span data-ttu-id="bad03-164">變更 web.config 以設定 castlabs 商店識別碼、STS 組態和共用的金鑰。</span><span class="sxs-lookup"><span data-stu-id="bad03-164">Change the web.config to setup castlabs merchant ID, the STS configuration and the shared key.</span></span>
2. <span data-ttu-id="bad03-165">部署到 Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="bad03-165">Deploy to Azure Websites.</span></span>
3. <span data-ttu-id="bad03-166">瀏覽至該網站。</span><span class="sxs-lookup"><span data-stu-id="bad03-166">Navigate to the website.</span></span>

## <a name="playing-back-a-video"></a><span data-ttu-id="bad03-167">播放視訊</span><span class="sxs-lookup"><span data-stu-id="bad03-167">Playing back a video</span></span>
<span data-ttu-id="bad03-168">若要播放使用一般加密 (PlayReady 和/或 Widevine) 技術加密的視訊，您可以使用 [Azure 媒體播放器](http://amsplayer.azurewebsites.net/azuremediaplayer.html)。</span><span class="sxs-lookup"><span data-stu-id="bad03-168">To playback a video encrypted with common encryption (PlayReady and/or Widevine), you can use the [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="bad03-169">執行主控台應用程式時，會回應內容金鑰識別碼和資訊清單 URL。</span><span class="sxs-lookup"><span data-stu-id="bad03-169">When running the console app, the Content Key ID and the Manifest URL are echoed.</span></span>

1. <span data-ttu-id="bad03-170">開啟新索引標籤，並啟動 STS：http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid]。</span><span class="sxs-lookup"><span data-stu-id="bad03-170">Open a new tab and launch your STS: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].</span></span>
2. <span data-ttu-id="bad03-171">移至 [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html)。</span><span class="sxs-lookup"><span data-stu-id="bad03-171">Go to [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
3. <span data-ttu-id="bad03-172">貼上資料流 URL。</span><span class="sxs-lookup"><span data-stu-id="bad03-172">Paste in the streaming URL.</span></span>
4. <span data-ttu-id="bad03-173">按一下 [ **進階選項** ] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="bad03-173">Click the **Advanced Options** checkbox.</span></span>
5. <span data-ttu-id="bad03-174">在 [保護]  下拉式清單中選取 PlayReady 和/或 Widevine。</span><span class="sxs-lookup"><span data-stu-id="bad03-174">In the **Protection** dropdown, select PlayReady and/or Widevine.</span></span>
6. <span data-ttu-id="bad03-175">在 [權杖] 文字方塊中貼上您從 STS 取得的權杖。</span><span class="sxs-lookup"><span data-stu-id="bad03-175">Paste the token that you got from your STS in the Token textbox.</span></span> 
   
   <span data-ttu-id="bad03-176">castLab 授權伺服器不需要權杖前有 “Bearer=” 前置詞。</span><span class="sxs-lookup"><span data-stu-id="bad03-176">The castLab license server does not need the “Bearer=” prefix in front of the token.</span></span> <span data-ttu-id="bad03-177">因此請先移除該前置詞，再提交權杖。</span><span class="sxs-lookup"><span data-stu-id="bad03-177">So please remove that before submitting the token.</span></span>
7. <span data-ttu-id="bad03-178">更新播放程式。</span><span class="sxs-lookup"><span data-stu-id="bad03-178">Update the player.</span></span>
8. <span data-ttu-id="bad03-179">視訊應隨即播放。</span><span class="sxs-lookup"><span data-stu-id="bad03-179">The video should be playing.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="bad03-180">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="bad03-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="bad03-181">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="bad03-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

