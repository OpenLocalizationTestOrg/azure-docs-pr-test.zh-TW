---
title: "Widevine 授權範本概觀 | Microsoft Docs"
description: "本主題提供了用來設定 Widevine 授權之 Widevine 授權範本的概觀。"
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0e6f1f05-7ed6-4ed6-82a0-0cc2182b075a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 667ff16dc7608dab2a5b8b1fd7df715da4620ca1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="widevine-license-template-overview"></a><span data-ttu-id="f78a2-103">Widevine 授權範本概觀</span><span class="sxs-lookup"><span data-stu-id="f78a2-103">Widevine license template overview</span></span>
## <a name="overview"></a><span data-ttu-id="f78a2-104">Overview</span><span class="sxs-lookup"><span data-stu-id="f78a2-104">Overview</span></span>
<span data-ttu-id="f78a2-105">Azure 媒體服務現在可讓您設定和要求 Widevine 授權。</span><span class="sxs-lookup"><span data-stu-id="f78a2-105">Azure Media Services now enables you to configure and request Widevine licenses.</span></span> <span data-ttu-id="f78a2-106">使用者播放程式嘗試播放 Widevine 保護內容時，會將要求傳送到授權傳遞服務來取得授權。</span><span class="sxs-lookup"><span data-stu-id="f78a2-106">When the end user player tries to play your Widevine protected content, a request is sent to the license delivery service to obtain a license.</span></span> <span data-ttu-id="f78a2-107">如果授權服務核准要求，就會發出傳送給用戶端並可用來解密和播放所指定內容的授權。</span><span class="sxs-lookup"><span data-stu-id="f78a2-107">If the license service approves the request, it issues the license which is sent to the client and can be used to decrypt and play the specified content.</span></span>

<span data-ttu-id="f78a2-108">Widevine 授權要求會格式化為 JSON 訊息。</span><span class="sxs-lookup"><span data-stu-id="f78a2-108">Widevine license request is formatted as a JSON message.</span></span>  

>[!NOTE]
> <span data-ttu-id="f78a2-109">您可以選擇建立不帶值而只有 "{}" 的空訊息，如此會建立具有所有預設值的授權範本。</span><span class="sxs-lookup"><span data-stu-id="f78a2-109">You can choose to create an empty message with no values just "{}" and a license template will be created with all defaults.</span></span> <span data-ttu-id="f78a2-110">大部分案例的預設工作。</span><span class="sxs-lookup"><span data-stu-id="f78a2-110">The default works for most cases.</span></span> <span data-ttu-id="f78a2-111">例如，一律必須使用預設值的 MS 型授權遞送案例。</span><span class="sxs-lookup"><span data-stu-id="f78a2-111">For example, for MS based license delivery scenarios that should always be default.</span></span> <span data-ttu-id="f78a2-112">若需要設定 "provider" 與 "content_id" 值，提供者必須符合 Google 的 Widevine 認證。</span><span class="sxs-lookup"><span data-stu-id="f78a2-112">If you do need to set the "provider" and "content_id" values, a provider must match Google's Widevine credentials.</span></span>

    {  
       “payload”:“<license challenge>”,
       “content_id”: “<content id>” 
       “provider”: ”<provider>”
       “allowed_track_types”:“<types>”,
       “content_key_specs”:[  
          {  
             “track_type”:“<track type 1>”
          },
          {  
             “track_type”:“<track type 2>”
          },
          …
       ],
       “policy_overrides”:{  
          “can_play”:<can play>,
          “can persist”:<can persist>,
          “can_renew”:<can renew>,
          “rental_duration_seconds”:<rental duration>,
          “playback_duration_seconds”:<playback duration>,
          “license_duration_seconds”:<license duration>,
          “renewal_recovery_duration_seconds”:<renewal recovery duration>,
          “renewal_server_url”:”<renewal server url>”,
          “renewal_delay_seconds”:<renewal delay>,
          “renewal_retry_interval_seconds”:<renewal retry interval>,
          “renew_with_usage”:<renew with usage>
       }
    }

## <a name="json-message"></a><span data-ttu-id="f78a2-113">JSON 訊息</span><span class="sxs-lookup"><span data-stu-id="f78a2-113">JSON message</span></span>
| <span data-ttu-id="f78a2-114">名稱</span><span class="sxs-lookup"><span data-stu-id="f78a2-114">Name</span></span> | <span data-ttu-id="f78a2-115">值</span><span class="sxs-lookup"><span data-stu-id="f78a2-115">Value</span></span> | <span data-ttu-id="f78a2-116">說明</span><span class="sxs-lookup"><span data-stu-id="f78a2-116">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f78a2-117">payload</span><span class="sxs-lookup"><span data-stu-id="f78a2-117">payload</span></span> |<span data-ttu-id="f78a2-118">Base64 編碼的字串</span><span class="sxs-lookup"><span data-stu-id="f78a2-118">Base64 encoded string</span></span> |<span data-ttu-id="f78a2-119">用戶端傳送的授權要求。</span><span class="sxs-lookup"><span data-stu-id="f78a2-119">The license request sent by a client.</span></span> |
| <span data-ttu-id="f78a2-120">content_id</span><span class="sxs-lookup"><span data-stu-id="f78a2-120">content_id</span></span> |<span data-ttu-id="f78a2-121">Base64 編碼的字串</span><span class="sxs-lookup"><span data-stu-id="f78a2-121">Base64 encoded string</span></span> |<span data-ttu-id="f78a2-122">用來針對每個 content_key_specs.track_type 衍生 KeyId(s) 與內容金鑰的識別碼。</span><span class="sxs-lookup"><span data-stu-id="f78a2-122">Identifier used to derive KeyId(s) and Content Key(s) for each content_key_specs.track_type.</span></span> |
| <span data-ttu-id="f78a2-123">provider</span><span class="sxs-lookup"><span data-stu-id="f78a2-123">provider</span></span> |<span data-ttu-id="f78a2-124">string</span><span class="sxs-lookup"><span data-stu-id="f78a2-124">string</span></span> |<span data-ttu-id="f78a2-125">用來查閱內容金鑰和原則。</span><span class="sxs-lookup"><span data-stu-id="f78a2-125">Used to look up content keys and policies.</span></span> <span data-ttu-id="f78a2-126">若將 MS 金鑰遞送用於 Widevine 授權遞送，系統會忽略此參數。</span><span class="sxs-lookup"><span data-stu-id="f78a2-126">If MS key delivery is used for Widevine license delivery, this parameter is ignored.</span></span> |
| <span data-ttu-id="f78a2-127">policy_name</span><span class="sxs-lookup"><span data-stu-id="f78a2-127">policy_name</span></span> |<span data-ttu-id="f78a2-128">string</span><span class="sxs-lookup"><span data-stu-id="f78a2-128">string</span></span> |<span data-ttu-id="f78a2-129">先前已登錄原則的名稱。</span><span class="sxs-lookup"><span data-stu-id="f78a2-129">Name of a previously registered policy.</span></span> <span data-ttu-id="f78a2-130">選用</span><span class="sxs-lookup"><span data-stu-id="f78a2-130">Optional</span></span> |
| <span data-ttu-id="f78a2-131">allowed_track_types</span><span class="sxs-lookup"><span data-stu-id="f78a2-131">allowed_track_types</span></span> |<span data-ttu-id="f78a2-132">列舉</span><span class="sxs-lookup"><span data-stu-id="f78a2-132">enum</span></span> |<span data-ttu-id="f78a2-133">SD_ONLY 或 SD_HD。</span><span class="sxs-lookup"><span data-stu-id="f78a2-133">SD_ONLY or SD_HD.</span></span> <span data-ttu-id="f78a2-134">控制授權中應該包含的內容金鑰</span><span class="sxs-lookup"><span data-stu-id="f78a2-134">Controls which content keys should be included in a license</span></span> |
| <span data-ttu-id="f78a2-135">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="f78a2-135">content_key_specs</span></span> |<span data-ttu-id="f78a2-136">JSON 結構的陣列，請參閱下方的 **內容金鑰規格**</span><span class="sxs-lookup"><span data-stu-id="f78a2-136">array of JSON structures, see **Content Key Specs** below</span></span> |<span data-ttu-id="f78a2-137">更細部控制要傳回的內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="f78a2-137">A finer grained control on what content keys to return.</span></span> <span data-ttu-id="f78a2-138">如需詳細資料，請參閱以下的內容金鑰規格。</span><span class="sxs-lookup"><span data-stu-id="f78a2-138">See Content Key Spec below for details.</span></span>  <span data-ttu-id="f78a2-139">只可以指定 allowed_track_types 和 content_key_specs 中的一個。</span><span class="sxs-lookup"><span data-stu-id="f78a2-139">Only one of allowed_track_types and content_key_specs can be specified.</span></span> |
| <span data-ttu-id="f78a2-140">use_policy_overrides_exclusively</span><span class="sxs-lookup"><span data-stu-id="f78a2-140">use_policy_overrides_exclusively</span></span> |<span data-ttu-id="f78a2-141">布林值。</span><span class="sxs-lookup"><span data-stu-id="f78a2-141">boolean.</span></span> <span data-ttu-id="f78a2-142">True 或 False</span><span class="sxs-lookup"><span data-stu-id="f78a2-142">true or false</span></span> |<span data-ttu-id="f78a2-143">使用 policy_overrides 所指定的原則屬性，並略過先前儲存的所有原則。</span><span class="sxs-lookup"><span data-stu-id="f78a2-143">Use policy attributes specified by policy_overrides and omit all previously stored policy.</span></span> |
| <span data-ttu-id="f78a2-144">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="f78a2-144">policy_overrides</span></span> |<span data-ttu-id="f78a2-145">JSON 結構，請參閱以下的 **原則覆寫**</span><span class="sxs-lookup"><span data-stu-id="f78a2-145">JSON structure, see **Policy Overrides** below</span></span> |<span data-ttu-id="f78a2-146">此授權的原則設定。</span><span class="sxs-lookup"><span data-stu-id="f78a2-146">Policy settings for this license.</span></span>  <span data-ttu-id="f78a2-147">如果此資產具有預先定義的原則，就會使用這些指定的值。</span><span class="sxs-lookup"><span data-stu-id="f78a2-147">In the event this asset has a pre-defined policy, these specified values will be used.</span></span> |
| <span data-ttu-id="f78a2-148">session_init</span><span class="sxs-lookup"><span data-stu-id="f78a2-148">session_init</span></span> |<span data-ttu-id="f78a2-149">JSON 結構，請參閱下方的 **工作階段初始化**</span><span class="sxs-lookup"><span data-stu-id="f78a2-149">JSON structure, see **Session Initialization** below</span></span> |<span data-ttu-id="f78a2-150">傳遞選擇性的資料給授權。</span><span class="sxs-lookup"><span data-stu-id="f78a2-150">Optional data passed to license.</span></span> |
| <span data-ttu-id="f78a2-151">parse_only</span><span class="sxs-lookup"><span data-stu-id="f78a2-151">parse_only</span></span> |<span data-ttu-id="f78a2-152">布林值。</span><span class="sxs-lookup"><span data-stu-id="f78a2-152">boolean.</span></span> <span data-ttu-id="f78a2-153">true 或 false</span><span class="sxs-lookup"><span data-stu-id="f78a2-153">true or false</span></span> |<span data-ttu-id="f78a2-154">剖析授權要求，但不會發出任何授權。</span><span class="sxs-lookup"><span data-stu-id="f78a2-154">The license request is parsed but no license is issued.</span></span> <span data-ttu-id="f78a2-155">不過，形成授權要求的值會在回應中傳回。</span><span class="sxs-lookup"><span data-stu-id="f78a2-155">However, values form the license request are returned in the response.</span></span> |

## <a name="content-key-specs"></a><span data-ttu-id="f78a2-156">內容金鑰規格</span><span class="sxs-lookup"><span data-stu-id="f78a2-156">Content Key Specs</span></span>
<span data-ttu-id="f78a2-157">如果有預先存在的原則，則不需要在內容金鑰規格中指定任何值。與此內容相關聯且預先存在的原則將用來判斷輸出保護，例如 HDCP 和 CGMS。</span><span class="sxs-lookup"><span data-stu-id="f78a2-157">If a pre-existing policy exist, there is no need to specify any of the values in the Content Key Spec.  The pre-existing policy associated with this content will be used to determine the output protection such as HDCP and CGMS.</span></span>  <span data-ttu-id="f78a2-158">如果預先存在的原則未向 Widevine 授權伺服器登錄，內容提供者可以在授權要求中插入值。</span><span class="sxs-lookup"><span data-stu-id="f78a2-158">If a pre-existing policy is not registered with the Widevine License Server, the content provider can inject the values into the license request.</span></span>   

<span data-ttu-id="f78a2-159">必須對所有追蹤指定每個 content_key_specs，不論選項 use_policy_overrides_exclusively 為何。</span><span class="sxs-lookup"><span data-stu-id="f78a2-159">Each content_key_specs must be specified for all tracks, regardless of the option use_policy_overrides_exclusively.</span></span> 

| <span data-ttu-id="f78a2-160">名稱</span><span class="sxs-lookup"><span data-stu-id="f78a2-160">Name</span></span> | <span data-ttu-id="f78a2-161">值</span><span class="sxs-lookup"><span data-stu-id="f78a2-161">Value</span></span> | <span data-ttu-id="f78a2-162">說明</span><span class="sxs-lookup"><span data-stu-id="f78a2-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f78a2-163">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="f78a2-163">content_key_specs.</span></span> <span data-ttu-id="f78a2-164">track_type</span><span class="sxs-lookup"><span data-stu-id="f78a2-164">track_type</span></span> |<span data-ttu-id="f78a2-165">字串</span><span class="sxs-lookup"><span data-stu-id="f78a2-165">string</span></span> |<span data-ttu-id="f78a2-166">追蹤類型名稱。</span><span class="sxs-lookup"><span data-stu-id="f78a2-166">A track type name.</span></span> <span data-ttu-id="f78a2-167">如果授權要求中指定 content_key_specs，則請務必明確指定所有追蹤類型。</span><span class="sxs-lookup"><span data-stu-id="f78a2-167">If content_key_specs is specified in the license request, make sure to specify all track types explicitly.</span></span> <span data-ttu-id="f78a2-168">未這樣做會導致無法播放過去 10 秒。</span><span class="sxs-lookup"><span data-stu-id="f78a2-168">Failure to do so will result in failure to playback past 10 seconds.</span></span> |
| <span data-ttu-id="f78a2-169">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="f78a2-169">content_key_specs</span></span>  <br/> <span data-ttu-id="f78a2-170">security_level</span><span class="sxs-lookup"><span data-stu-id="f78a2-170">security_level</span></span> |<span data-ttu-id="f78a2-171">uint32</span><span class="sxs-lookup"><span data-stu-id="f78a2-171">uint32</span></span> |<span data-ttu-id="f78a2-172">定義用戶端對於播放的穩健性需求。</span><span class="sxs-lookup"><span data-stu-id="f78a2-172">Defines client robustness requirements for playback.</span></span> <br/> <span data-ttu-id="f78a2-173">1 - 以軟體為基礎白箱加密是必要的。</span><span class="sxs-lookup"><span data-stu-id="f78a2-173">1 - Software-based whitebox crypto is required.</span></span> <br/> <span data-ttu-id="f78a2-174">2 - 軟體加密和模糊化的解碼器是必要的。</span><span class="sxs-lookup"><span data-stu-id="f78a2-174">2 - Software crypto and an obfuscated decoder is required.</span></span> <br/> <span data-ttu-id="f78a2-175">3 - 金鑰資料和加密作業必須在支援硬體的受信任執行環境中執行。</span><span class="sxs-lookup"><span data-stu-id="f78a2-175">3 - The key material and crypto operations must be performed within a hardware backed trusted execution environment.</span></span> <br/> <span data-ttu-id="f78a2-176">4 - 內容的加密和解密必須在支援硬體的受信任執行環境中執行。</span><span class="sxs-lookup"><span data-stu-id="f78a2-176">4 - The crypto and decoding of content must be performed within a hardware backed trusted execution environment.</span></span>  <br/> <span data-ttu-id="f78a2-177">5 - 加密、解密和媒體 (壓縮和未壓縮) 的所有處理必須在支援硬體的受信任執行環境中處理。</span><span class="sxs-lookup"><span data-stu-id="f78a2-177">5 - The crypto, decoding and all handling of the media (compressed and uncompressed) must be handled within a hardware backed trusted execution environment.</span></span> |
| <span data-ttu-id="f78a2-178">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="f78a2-178">content_key_specs</span></span> <br/> <span data-ttu-id="f78a2-179">required_output_protection.hdc</span><span class="sxs-lookup"><span data-stu-id="f78a2-179">required_output_protection.hdc</span></span> |<span data-ttu-id="f78a2-180">字串 - 以下項目的其中一個：HDCP_NONE、HDCP_V1、HDCP_V2</span><span class="sxs-lookup"><span data-stu-id="f78a2-180">string - one of: HDCP_NONE, HDCP_V1, HDCP_V2</span></span> |<span data-ttu-id="f78a2-181">指出是否需要 HDCP</span><span class="sxs-lookup"><span data-stu-id="f78a2-181">Indicates whether HDCP is require</span></span> |
| <span data-ttu-id="f78a2-182">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="f78a2-182">content_key_specs</span></span> <br/><span data-ttu-id="f78a2-183">索引鍵</span><span class="sxs-lookup"><span data-stu-id="f78a2-183">key</span></span> |<span data-ttu-id="f78a2-184">Base64 </span><span class="sxs-lookup"><span data-stu-id="f78a2-184">Base64</span></span> <br/><span data-ttu-id="f78a2-185">編碼的字串</span><span class="sxs-lookup"><span data-stu-id="f78a2-185">encoded string</span></span> |<span data-ttu-id="f78a2-186">要用於此追蹤的內容金鑰。如果指定，則需要 track_type 或 key_id。</span><span class="sxs-lookup"><span data-stu-id="f78a2-186">Content key to use for this track. If specified, the track_type or key_id is required.</span></span>  <span data-ttu-id="f78a2-187">此選項可讓內容提供者插入此追蹤的內容金鑰，而不是讓 Widevine 授權伺服器產生或查閱金鑰。</span><span class="sxs-lookup"><span data-stu-id="f78a2-187">This option allows the content provider to inject the content key for this track instead of letting Widevine license server generate or lookup a key.</span></span> |
| <span data-ttu-id="f78a2-188">content_key_specs.key_id</span><span class="sxs-lookup"><span data-stu-id="f78a2-188">content_key_specs.key_id</span></span> |<span data-ttu-id="f78a2-189">Base64 編碼的二進位字串，16 位元組</span><span class="sxs-lookup"><span data-stu-id="f78a2-189">Base64 encoded string  binary, 16 bytes</span></span> |<span data-ttu-id="f78a2-190">金鑰的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="f78a2-190">Unique identifier for the key.</span></span> |

## <a name="policy-overrides"></a><span data-ttu-id="f78a2-191">原則覆寫</span><span class="sxs-lookup"><span data-stu-id="f78a2-191">Policy Overrides</span></span>
| <span data-ttu-id="f78a2-192">名稱</span><span class="sxs-lookup"><span data-stu-id="f78a2-192">Name</span></span> | <span data-ttu-id="f78a2-193">值</span><span class="sxs-lookup"><span data-stu-id="f78a2-193">Value</span></span> | <span data-ttu-id="f78a2-194">說明</span><span class="sxs-lookup"><span data-stu-id="f78a2-194">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f78a2-195">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="f78a2-195">policy_overrides.</span></span> <span data-ttu-id="f78a2-196">can_play</span><span class="sxs-lookup"><span data-stu-id="f78a2-196">can_play</span></span> |<span data-ttu-id="f78a2-197">布林值。</span><span class="sxs-lookup"><span data-stu-id="f78a2-197">boolean.</span></span> <span data-ttu-id="f78a2-198">true 或 false</span><span class="sxs-lookup"><span data-stu-id="f78a2-198">true or false</span></span> |<span data-ttu-id="f78a2-199">表示允許播放內容。</span><span class="sxs-lookup"><span data-stu-id="f78a2-199">Indicates that playback of the content is allowed.</span></span> <span data-ttu-id="f78a2-200">預設值為 false。</span><span class="sxs-lookup"><span data-stu-id="f78a2-200">Default is false.</span></span> |
| <span data-ttu-id="f78a2-201">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="f78a2-201">policy_overrides.</span></span> <span data-ttu-id="f78a2-202">can_persist</span><span class="sxs-lookup"><span data-stu-id="f78a2-202">can_persist</span></span> |<span data-ttu-id="f78a2-203">布林值。</span><span class="sxs-lookup"><span data-stu-id="f78a2-203">boolean.</span></span> <span data-ttu-id="f78a2-204">true 或 false</span><span class="sxs-lookup"><span data-stu-id="f78a2-204">true or false</span></span> |<span data-ttu-id="f78a2-205">表示可以將授權保存到非揮發性儲存體，供離線使用。</span><span class="sxs-lookup"><span data-stu-id="f78a2-205">Indicates that the license may be persisted to non-volatile storage for offline use.</span></span> <span data-ttu-id="f78a2-206">預設值為 false。</span><span class="sxs-lookup"><span data-stu-id="f78a2-206">Default is false.</span></span> |
| <span data-ttu-id="f78a2-207">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="f78a2-207">policy_overrides.</span></span> <span data-ttu-id="f78a2-208">can_renew</span><span class="sxs-lookup"><span data-stu-id="f78a2-208">can_renew</span></span> |<span data-ttu-id="f78a2-209">布林值 true 或 false</span><span class="sxs-lookup"><span data-stu-id="f78a2-209">boolean true or false</span></span> |<span data-ttu-id="f78a2-210">表示允許更新此授權。</span><span class="sxs-lookup"><span data-stu-id="f78a2-210">Indicates that renewal of this license is allowed.</span></span> <span data-ttu-id="f78a2-211">如果為 true，則在授權期間可以透過活動訊號延長。</span><span class="sxs-lookup"><span data-stu-id="f78a2-211">If true, the duration of the license can be extended by heartbeat.</span></span> <span data-ttu-id="f78a2-212">預設值為 false。</span><span class="sxs-lookup"><span data-stu-id="f78a2-212">Default is false.</span></span> |
| <span data-ttu-id="f78a2-213">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="f78a2-213">policy_overrides.</span></span> <span data-ttu-id="f78a2-214">license_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="f78a2-214">license_duration_seconds</span></span> |<span data-ttu-id="f78a2-215">int64</span><span class="sxs-lookup"><span data-stu-id="f78a2-215">int64</span></span> |<span data-ttu-id="f78a2-216">指出此特定授權的期間。</span><span class="sxs-lookup"><span data-stu-id="f78a2-216">Indicates the time window for this specific license.</span></span> <span data-ttu-id="f78a2-217">值為 0 表示期間沒有限制。</span><span class="sxs-lookup"><span data-stu-id="f78a2-217">A value of 0 indicates that there is no limit to the duration.</span></span> <span data-ttu-id="f78a2-218">預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="f78a2-218">Default is 0.</span></span> |
| <span data-ttu-id="f78a2-219">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="f78a2-219">policy_overrides.</span></span> <span data-ttu-id="f78a2-220">rental_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="f78a2-220">rental_duration_seconds</span></span> |<span data-ttu-id="f78a2-221">int64</span><span class="sxs-lookup"><span data-stu-id="f78a2-221">int64</span></span> |<span data-ttu-id="f78a2-222">指出允許播放的期間。</span><span class="sxs-lookup"><span data-stu-id="f78a2-222">Indicates the time window while playback is permitted.</span></span> <span data-ttu-id="f78a2-223">值為 0 表示期間沒有限制。</span><span class="sxs-lookup"><span data-stu-id="f78a2-223">A value of 0 indicates that there is no limit to the duration.</span></span> <span data-ttu-id="f78a2-224">預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="f78a2-224">Default is 0.</span></span> |
| <span data-ttu-id="f78a2-225">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="f78a2-225">policy_overrides.</span></span> <span data-ttu-id="f78a2-226">playback_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="f78a2-226">playback_duration_seconds</span></span> |<span data-ttu-id="f78a2-227">int64</span><span class="sxs-lookup"><span data-stu-id="f78a2-227">int64</span></span> |<span data-ttu-id="f78a2-228">一旦在授權期間內開始播放的檢視時段。</span><span class="sxs-lookup"><span data-stu-id="f78a2-228">The viewing window of time once playback starts within the license duration.</span></span> <span data-ttu-id="f78a2-229">值為 0 表示期間沒有限制。</span><span class="sxs-lookup"><span data-stu-id="f78a2-229">A value of 0 indicates that there is no limit to the duration.</span></span> <span data-ttu-id="f78a2-230">預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="f78a2-230">Default is 0.</span></span> |
| <span data-ttu-id="f78a2-231">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="f78a2-231">policy_overrides.</span></span> <span data-ttu-id="f78a2-232">renewal_server_url</span><span class="sxs-lookup"><span data-stu-id="f78a2-232">renewal_server_url</span></span> |<span data-ttu-id="f78a2-233">字串</span><span class="sxs-lookup"><span data-stu-id="f78a2-233">string</span></span> |<span data-ttu-id="f78a2-234">應該將此授權的所有活動訊號 (更新) 要求導向到指定 URL。</span><span class="sxs-lookup"><span data-stu-id="f78a2-234">All heartbeat (renewal) requests for this license shall be directed to the specified URL.</span></span> <span data-ttu-id="f78a2-235">只有在 can_renew 為 true 時才會使用這個欄位。</span><span class="sxs-lookup"><span data-stu-id="f78a2-235">This field is only used if can_renew is true.</span></span> |
| <span data-ttu-id="f78a2-236">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="f78a2-236">policy_overrides.</span></span> <span data-ttu-id="f78a2-237">renewal_delay_seconds</span><span class="sxs-lookup"><span data-stu-id="f78a2-237">renewal_delay_seconds</span></span> |<span data-ttu-id="f78a2-238">int64</span><span class="sxs-lookup"><span data-stu-id="f78a2-238">int64</span></span> |<span data-ttu-id="f78a2-239">license_start_time 之後經過幾秒才會第一次嘗試更新。</span><span class="sxs-lookup"><span data-stu-id="f78a2-239">How many seconds after license_start_time, before renewal is first attempted.</span></span> <span data-ttu-id="f78a2-240">只有在 can_renew 為 true 時才會使用這個欄位。</span><span class="sxs-lookup"><span data-stu-id="f78a2-240">This field is only used if can_renew is true.</span></span> <span data-ttu-id="f78a2-241">預設值為 0</span><span class="sxs-lookup"><span data-stu-id="f78a2-241">Default is 0</span></span> |
| <span data-ttu-id="f78a2-242">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="f78a2-242">policy_overrides.</span></span> <span data-ttu-id="f78a2-243">renewal_retry_interval_seconds</span><span class="sxs-lookup"><span data-stu-id="f78a2-243">renewal_retry_interval_seconds</span></span> |<span data-ttu-id="f78a2-244">int64</span><span class="sxs-lookup"><span data-stu-id="f78a2-244">int64</span></span> |<span data-ttu-id="f78a2-245">指定若發生失敗，後續授權更新要求之間的延遲秒數。</span><span class="sxs-lookup"><span data-stu-id="f78a2-245">Specifies the delay in seconds between subsequent license renewal requests, in case of failure.</span></span> <span data-ttu-id="f78a2-246">只有在 can_renew 為 true 時才會使用這個欄位。</span><span class="sxs-lookup"><span data-stu-id="f78a2-246">This field is only used if can_renew is true.</span></span> |
| <span data-ttu-id="f78a2-247">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="f78a2-247">policy_overrides.</span></span> <span data-ttu-id="f78a2-248">renewal_recovery_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="f78a2-248">renewal_recovery_duration_seconds</span></span> |<span data-ttu-id="f78a2-249">int64</span><span class="sxs-lookup"><span data-stu-id="f78a2-249">int64</span></span> |<span data-ttu-id="f78a2-250">時段，在此時段當嘗試進行更新時允許繼續播放，不過因為授權伺服器發生後端問題而未成功。</span><span class="sxs-lookup"><span data-stu-id="f78a2-250">The window of time, in which playback is allowed to continue while renewal is attempted, yet unsuccessful due to backend problems with the license server.</span></span> <span data-ttu-id="f78a2-251">值為 0 表示期間沒有限制。</span><span class="sxs-lookup"><span data-stu-id="f78a2-251">A value of 0 indicates that there is no limit to the duration.</span></span> <span data-ttu-id="f78a2-252">只有在 can_renew 為 true 時才會使用這個欄位。</span><span class="sxs-lookup"><span data-stu-id="f78a2-252">This field is only used if can_renew is true.</span></span> |
| <span data-ttu-id="f78a2-253">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="f78a2-253">policy_overrides.</span></span> <span data-ttu-id="f78a2-254">renew_with_usage</span><span class="sxs-lookup"><span data-stu-id="f78a2-254">renew_with_usage</span></span> |<span data-ttu-id="f78a2-255">布林值 true 或 false</span><span class="sxs-lookup"><span data-stu-id="f78a2-255">boolean true or false</span></span> |<span data-ttu-id="f78a2-256">表示開始使用時應該傳送授權以進行更新。</span><span class="sxs-lookup"><span data-stu-id="f78a2-256">Indicates that the license shall be sent for renewal when usage is started.</span></span> <span data-ttu-id="f78a2-257">只有在 can_renew 為 true 時才會使用這個欄位。</span><span class="sxs-lookup"><span data-stu-id="f78a2-257">This field is only used if can_renew is true.</span></span> |

## <a name="session-initialization"></a><span data-ttu-id="f78a2-258">工作階段初始化</span><span class="sxs-lookup"><span data-stu-id="f78a2-258">Session Initialization</span></span>
| <span data-ttu-id="f78a2-259">名稱</span><span class="sxs-lookup"><span data-stu-id="f78a2-259">Name</span></span> | <span data-ttu-id="f78a2-260">值</span><span class="sxs-lookup"><span data-stu-id="f78a2-260">Value</span></span> | <span data-ttu-id="f78a2-261">說明</span><span class="sxs-lookup"><span data-stu-id="f78a2-261">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f78a2-262">provider_session_token</span><span class="sxs-lookup"><span data-stu-id="f78a2-262">provider_session_token</span></span> |<span data-ttu-id="f78a2-263">Base64 編碼的字串</span><span class="sxs-lookup"><span data-stu-id="f78a2-263">Base64 encoded string</span></span> |<span data-ttu-id="f78a2-264">此工作階段權杖會傳回到授權，並且會在後續的更新作業中存在。</span><span class="sxs-lookup"><span data-stu-id="f78a2-264">This session token is passed back in the license and will exist in subsequent renewals.</span></span>  <span data-ttu-id="f78a2-265">工作階段權杖不會在工作階段之外保存。</span><span class="sxs-lookup"><span data-stu-id="f78a2-265">The session token will not persist beyond sessions.</span></span> |
| <span data-ttu-id="f78a2-266">provider_client_token</span><span class="sxs-lookup"><span data-stu-id="f78a2-266">provider_client_token</span></span> |<span data-ttu-id="f78a2-267">Base64 編碼的字串</span><span class="sxs-lookup"><span data-stu-id="f78a2-267">Base64 encoded string</span></span> |<span data-ttu-id="f78a2-268">要在授權回應中傳回的用戶端權杖。</span><span class="sxs-lookup"><span data-stu-id="f78a2-268">Client token to send back in the license response.</span></span>  <span data-ttu-id="f78a2-269">如果授權要求包含用戶端權杖，則會忽略此值。</span><span class="sxs-lookup"><span data-stu-id="f78a2-269">If the license request contains a client token, this value is ignored.</span></span> <span data-ttu-id="f78a2-270">用戶端權杖會在授權工作階段之外保存。</span><span class="sxs-lookup"><span data-stu-id="f78a2-270">The client token will persist beyond license sessions.</span></span> |
| <span data-ttu-id="f78a2-271">override_provider_client_token</span><span class="sxs-lookup"><span data-stu-id="f78a2-271">override_provider_client_token</span></span> |<span data-ttu-id="f78a2-272">布林值。</span><span class="sxs-lookup"><span data-stu-id="f78a2-272">boolean.</span></span> <span data-ttu-id="f78a2-273">true 或 false</span><span class="sxs-lookup"><span data-stu-id="f78a2-273">true or false</span></span> |<span data-ttu-id="f78a2-274">如果為 false 並且授權要求包含用戶端權杖，請使用來自要求的權杖，即使此結構中已指定用戶端權杖亦然。</span><span class="sxs-lookup"><span data-stu-id="f78a2-274">If false and the license request contains a client token, use the token from the request even if a client token was specified in this structure.</span></span>  <span data-ttu-id="f78a2-275">如果為 true，則一律使用這個結構中指定的權杖。</span><span class="sxs-lookup"><span data-stu-id="f78a2-275">If true, always use the token specified in this structure.</span></span> |

## <a name="configure-your-widevine-licenses-using-net-types"></a><span data-ttu-id="f78a2-276">使用 .NET 型別設定您的 Widevine 授權</span><span class="sxs-lookup"><span data-stu-id="f78a2-276">Configure your Widevine licenses using .NET types</span></span>
<span data-ttu-id="f78a2-277">媒體服務提供可讓您設定 Widevine 授權的 .NET API。</span><span class="sxs-lookup"><span data-stu-id="f78a2-277">Media Services provides .NET APIs that let you configure your Widevine licenses.</span></span> 

### <a name="classes-as-defined-in-the-media-services-net-sdk"></a><span data-ttu-id="f78a2-278">媒體服務 .NET SDK 中所定義的類別</span><span class="sxs-lookup"><span data-stu-id="f78a2-278">Classes as defined in the Media Services .NET SDK</span></span>
<span data-ttu-id="f78a2-279">以下是這些類型的定義。</span><span class="sxs-lookup"><span data-stu-id="f78a2-279">The following are the definitions of these types.</span></span>

    public class WidevineMessage
    {
        public WidevineMessage();

        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public AllowedTrackTypes? allowed_track_types { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public ContentKeySpecs[] content_key_specs { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public object policy_overrides { get; set; }
    }

    [JsonConverter(typeof(StringEnumConverter))]
    public enum AllowedTrackTypes
    {
        SD_ONLY = 0,
        SD_HD = 1
    }
    public class ContentKeySpecs
    {
        public ContentKeySpecs();

        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public string key_id { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public RequiredOutputProtection required_output_protection { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public int? security_level { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public string track_type { get; set; }
    }

    public class RequiredOutputProtection
    {
        public RequiredOutputProtection();

        public Hdcp hdcp { get; set; }
    }

    [JsonConverter(typeof(StringEnumConverter))]
    public enum Hdcp
    {
        HDCP_NONE = 0,
        HDCP_V1 = 1,
        HDCP_V2 = 2
    }

### <a name="example"></a><span data-ttu-id="f78a2-280">範例</span><span class="sxs-lookup"><span data-stu-id="f78a2-280">Example</span></span>
<span data-ttu-id="f78a2-281">下列範例示範如何使用 .NET API 來設定簡單的 Widevine 授權。</span><span class="sxs-lookup"><span data-stu-id="f78a2-281">The following example shows how to use .NET APIs to configure  a simple Widevine license.</span></span>

    private static string ConfigureWidevineLicenseTemplate()
    {
        var template = new WidevineMessage
        {
            allowed_track_types = AllowedTrackTypes.SD_HD,
            content_key_specs = new[]
            {
                new ContentKeySpecs
                {
                    required_output_protection = new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
                    security_level = 1,
                    track_type = "SD"
                }
            },
            policy_overrides = new
            {
                can_play = true,
                can_persist = true,
                can_renew = false
            }
        };

        string configuration = JsonConvert.SerializeObject(template);
        return configuration;
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="f78a2-282">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="f78a2-282">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f78a2-283">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="f78a2-283">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="f78a2-284">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f78a2-284">See also</span></span>
[<span data-ttu-id="f78a2-285">使用 PlayReady 和/或 Widevine 動態 Common Encryption</span><span class="sxs-lookup"><span data-stu-id="f78a2-285">Using PlayReady and/or Widevine Dynamic Common Encryption</span></span>](media-services-protect-with-drm.md)

