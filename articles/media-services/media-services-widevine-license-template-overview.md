---
title: "aaaWidevine 授權範本概觀 |Microsoft 文件"
description: "本主題提供使用 tooconfigure Widevine 授權 Widevine 授權範本的概觀。"
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
ms.openlocfilehash: 67a6ae38cf3d3c21e1b7282aef15f79b21776414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="widevine-license-template-overview"></a><span data-ttu-id="1e1e9-103">Widevine 授權範本概觀</span><span class="sxs-lookup"><span data-stu-id="1e1e9-103">Widevine license template overview</span></span>
## <a name="overview"></a><span data-ttu-id="1e1e9-104">概觀</span><span class="sxs-lookup"><span data-stu-id="1e1e9-104">Overview</span></span>
<span data-ttu-id="1e1e9-105">Azure 媒體服務現在可讓您 tooconfigure 和要求 Widevine 授權。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-105">Azure Media Services now enables you tooconfigure and request Widevine licenses.</span></span> <span data-ttu-id="1e1e9-106">Hello 使用者播放程式會嘗試 tooplay Widevine 受保護的內容、 要求時傳送的 toohello 授權傳遞服務 tooobtain 授權。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-106">When hello end user player tries tooplay your Widevine protected content, a request is sent toohello license delivery service tooobtain a license.</span></span> <span data-ttu-id="1e1e9-107">如果 hello 授權服務核准 hello 要求，就會發出這是傳送的 toohello 用戶端 hello 授權，而且可以是使用的 toodecrypt 插 hello 指定的內容。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-107">If hello license service approves hello request, it issues hello license which is sent toohello client and can be used toodecrypt and play hello specified content.</span></span>

<span data-ttu-id="1e1e9-108">Widevine 授權要求會格式化為 JSON 訊息。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-108">Widevine license request is formatted as a JSON message.</span></span>  

>[!NOTE]
> <span data-ttu-id="1e1e9-109">您可以選擇 toocreate 空的訊息沒有值只是"{}"，而且會使用所有預設值建立授權範本。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-109">You can choose toocreate an empty message with no values just "{}" and a license template will be created with all defaults.</span></span> <span data-ttu-id="1e1e9-110">hello 預設適用於大部分情況。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-110">hello default works for most cases.</span></span> <span data-ttu-id="1e1e9-111">例如，一律必須使用預設值的 MS 型授權遞送案例。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-111">For example, for MS based license delivery scenarios that should always be default.</span></span> <span data-ttu-id="1e1e9-112">如果您需要 tooset hello 「 提供者 」 和 「 content_id"值，提供者必須符合 Google Widevine 認證。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-112">If you do need tooset hello "provider" and "content_id" values, a provider must match Google's Widevine credentials.</span></span>

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

## <a name="json-message"></a><span data-ttu-id="1e1e9-113">JSON 訊息</span><span class="sxs-lookup"><span data-stu-id="1e1e9-113">JSON message</span></span>
| <span data-ttu-id="1e1e9-114">名稱</span><span class="sxs-lookup"><span data-stu-id="1e1e9-114">Name</span></span> | <span data-ttu-id="1e1e9-115">值</span><span class="sxs-lookup"><span data-stu-id="1e1e9-115">Value</span></span> | <span data-ttu-id="1e1e9-116">說明</span><span class="sxs-lookup"><span data-stu-id="1e1e9-116">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1e1e9-117">payload</span><span class="sxs-lookup"><span data-stu-id="1e1e9-117">payload</span></span> |<span data-ttu-id="1e1e9-118">Base64 編碼的字串</span><span class="sxs-lookup"><span data-stu-id="1e1e9-118">Base64 encoded string</span></span> |<span data-ttu-id="1e1e9-119">用戶端傳送嗨授權要求。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-119">hello license request sent by a client.</span></span> |
| <span data-ttu-id="1e1e9-120">content_id</span><span class="sxs-lookup"><span data-stu-id="1e1e9-120">content_id</span></span> |<span data-ttu-id="1e1e9-121">Base64 編碼的字串</span><span class="sxs-lookup"><span data-stu-id="1e1e9-121">Base64 encoded string</span></span> |<span data-ttu-id="1e1e9-122">識別項會用於每個 content_key_specs.track_type tooderive KeyId(s) 與內容的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-122">Identifier used tooderive KeyId(s) and Content Key(s) for each content_key_specs.track_type.</span></span> |
| <span data-ttu-id="1e1e9-123">provider</span><span class="sxs-lookup"><span data-stu-id="1e1e9-123">provider</span></span> |<span data-ttu-id="1e1e9-124">字串</span><span class="sxs-lookup"><span data-stu-id="1e1e9-124">string</span></span> |<span data-ttu-id="1e1e9-125">使用內容金鑰和原則 toolook。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-125">Used toolook up content keys and policies.</span></span> <span data-ttu-id="1e1e9-126">若將 MS 金鑰遞送用於 Widevine 授權遞送，系統會忽略此參數。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-126">If MS key delivery is used for Widevine license delivery, this parameter is ignored.</span></span> |
| <span data-ttu-id="1e1e9-127">policy_name</span><span class="sxs-lookup"><span data-stu-id="1e1e9-127">policy_name</span></span> |<span data-ttu-id="1e1e9-128">string</span><span class="sxs-lookup"><span data-stu-id="1e1e9-128">string</span></span> |<span data-ttu-id="1e1e9-129">先前已登錄原則的名稱。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-129">Name of a previously registered policy.</span></span> <span data-ttu-id="1e1e9-130">選用</span><span class="sxs-lookup"><span data-stu-id="1e1e9-130">Optional</span></span> |
| <span data-ttu-id="1e1e9-131">allowed_track_types</span><span class="sxs-lookup"><span data-stu-id="1e1e9-131">allowed_track_types</span></span> |<span data-ttu-id="1e1e9-132">列舉</span><span class="sxs-lookup"><span data-stu-id="1e1e9-132">enum</span></span> |<span data-ttu-id="1e1e9-133">SD_ONLY 或 SD_HD。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-133">SD_ONLY or SD_HD.</span></span> <span data-ttu-id="1e1e9-134">控制授權中應該包含的內容金鑰</span><span class="sxs-lookup"><span data-stu-id="1e1e9-134">Controls which content keys should be included in a license</span></span> |
| <span data-ttu-id="1e1e9-135">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="1e1e9-135">content_key_specs</span></span> |<span data-ttu-id="1e1e9-136">JSON 結構的陣列，請參閱下方的 **內容金鑰規格**</span><span class="sxs-lookup"><span data-stu-id="1e1e9-136">array of JSON structures, see **Content Key Specs** below</span></span> |<span data-ttu-id="1e1e9-137">精細地的控制內容金鑰 tooreturn 上。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-137">A finer grained control on what content keys tooreturn.</span></span> <span data-ttu-id="1e1e9-138">如需詳細資料，請參閱以下的內容金鑰規格。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-138">See Content Key Spec below for details.</span></span>  <span data-ttu-id="1e1e9-139">只可以指定 allowed_track_types 和 content_key_specs 中的一個。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-139">Only one of allowed_track_types and content_key_specs can be specified.</span></span> |
| <span data-ttu-id="1e1e9-140">use_policy_overrides_exclusively</span><span class="sxs-lookup"><span data-stu-id="1e1e9-140">use_policy_overrides_exclusively</span></span> |<span data-ttu-id="1e1e9-141">布林值。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-141">boolean.</span></span> <span data-ttu-id="1e1e9-142">True 或 False</span><span class="sxs-lookup"><span data-stu-id="1e1e9-142">true or false</span></span> |<span data-ttu-id="1e1e9-143">使用 policy_overrides 所指定的原則屬性，並略過先前儲存的所有原則。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-143">Use policy attributes specified by policy_overrides and omit all previously stored policy.</span></span> |
| <span data-ttu-id="1e1e9-144">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="1e1e9-144">policy_overrides</span></span> |<span data-ttu-id="1e1e9-145">JSON 結構，請參閱以下的 **原則覆寫**</span><span class="sxs-lookup"><span data-stu-id="1e1e9-145">JSON structure, see **Policy Overrides** below</span></span> |<span data-ttu-id="1e1e9-146">此授權的原則設定。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-146">Policy settings for this license.</span></span>  <span data-ttu-id="1e1e9-147">Hello 事件中這項資產有一個預先定義的原則，就會使用這些指定的值。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-147">In hello event this asset has a pre-defined policy, these specified values will be used.</span></span> |
| <span data-ttu-id="1e1e9-148">session_init</span><span class="sxs-lookup"><span data-stu-id="1e1e9-148">session_init</span></span> |<span data-ttu-id="1e1e9-149">JSON 結構，請參閱下方的 **工作階段初始化**</span><span class="sxs-lookup"><span data-stu-id="1e1e9-149">JSON structure, see **Session Initialization** below</span></span> |<span data-ttu-id="1e1e9-150">Toolicense 傳遞選擇性的資料。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-150">Optional data passed toolicense.</span></span> |
| <span data-ttu-id="1e1e9-151">parse_only</span><span class="sxs-lookup"><span data-stu-id="1e1e9-151">parse_only</span></span> |<span data-ttu-id="1e1e9-152">布林值。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-152">boolean.</span></span> <span data-ttu-id="1e1e9-153">True 或 False</span><span class="sxs-lookup"><span data-stu-id="1e1e9-153">true or false</span></span> |<span data-ttu-id="1e1e9-154">會剖析 hello 授權要求，但不發出任何授權。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-154">hello license request is parsed but no license is issued.</span></span> <span data-ttu-id="1e1e9-155">不過，hello 回應會傳回值格式 hello 授權要求。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-155">However, values form hello license request are returned in hello response.</span></span> |

## <a name="content-key-specs"></a><span data-ttu-id="1e1e9-156">內容金鑰規格</span><span class="sxs-lookup"><span data-stu-id="1e1e9-156">Content Key Specs</span></span>
<span data-ttu-id="1e1e9-157">預先存在的原則存在，有任何 hello hello 內容金鑰規格中的值不需要 toospecify。 hello 預先存在此內容相關聯的原則會使用的 toodetermine hello 輸出保護 CGMS HDCP 等。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-157">If a pre-existing policy exist, there is no need toospecify any of hello values in hello Content Key Spec.  hello pre-existing policy associated with this content will be used toodetermine hello output protection such as HDCP and CGMS.</span></span>  <span data-ttu-id="1e1e9-158">如果預先存在的原則未向 hello Widevine 授權伺服器，hello 內容提供者可以插入 hello 授權要求的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-158">If a pre-existing policy is not registered with hello Widevine License Server, hello content provider can inject hello values into hello license request.</span></span>   

<span data-ttu-id="1e1e9-159">每個 content_key_specs 必須指定所有曲目，不論 hello 選項 use_policy_overrides_exclusively。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-159">Each content_key_specs must be specified for all tracks, regardless of hello option use_policy_overrides_exclusively.</span></span> 

| <span data-ttu-id="1e1e9-160">名稱</span><span class="sxs-lookup"><span data-stu-id="1e1e9-160">Name</span></span> | <span data-ttu-id="1e1e9-161">值</span><span class="sxs-lookup"><span data-stu-id="1e1e9-161">Value</span></span> | <span data-ttu-id="1e1e9-162">說明</span><span class="sxs-lookup"><span data-stu-id="1e1e9-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1e1e9-163">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="1e1e9-163">content_key_specs.</span></span> <span data-ttu-id="1e1e9-164">track_type</span><span class="sxs-lookup"><span data-stu-id="1e1e9-164">track_type</span></span> |<span data-ttu-id="1e1e9-165">字串</span><span class="sxs-lookup"><span data-stu-id="1e1e9-165">string</span></span> |<span data-ttu-id="1e1e9-166">追蹤類型名稱。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-166">A track type name.</span></span> <span data-ttu-id="1e1e9-167">如果 content_key_specs hello 授權要求中指定，請確定所有追蹤的 toospecify 類型明確。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-167">If content_key_specs is specified in hello license request, make sure toospecify all track types explicitly.</span></span> <span data-ttu-id="1e1e9-168">失敗 toodo 因此將會導致失敗 tooplayback 過去 10 秒。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-168">Failure toodo so will result in failure tooplayback past 10 seconds.</span></span> |
| <span data-ttu-id="1e1e9-169">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="1e1e9-169">content_key_specs</span></span>  <br/> <span data-ttu-id="1e1e9-170">security_level</span><span class="sxs-lookup"><span data-stu-id="1e1e9-170">security_level</span></span> |<span data-ttu-id="1e1e9-171">uint32</span><span class="sxs-lookup"><span data-stu-id="1e1e9-171">uint32</span></span> |<span data-ttu-id="1e1e9-172">定義用戶端對於播放的穩健性需求。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-172">Defines client robustness requirements for playback.</span></span> <br/> <span data-ttu-id="1e1e9-173">1 - 以軟體為基礎白箱加密是必要的。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-173">1 - Software-based whitebox crypto is required.</span></span> <br/> <span data-ttu-id="1e1e9-174">2 - 軟體加密和模糊化的解碼器是必要的。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-174">2 - Software crypto and an obfuscated decoder is required.</span></span> <br/> <span data-ttu-id="1e1e9-175">3-hello 金鑰材料和密碼編譯作業必須在硬體備份信任的執行的環境中執行。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-175">3 - hello key material and crypto operations must be performed within a hardware backed trusted execution environment.</span></span> <br/> <span data-ttu-id="1e1e9-176">4-hello 密碼編譯和解碼的內容必須硬體備份信任的執行環境中執行。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-176">4 - hello crypto and decoding of content must be performed within a hardware backed trusted execution environment.</span></span>  <br/> <span data-ttu-id="1e1e9-177">5-hello 密碼編譯、 解碼和 hello 媒體 （壓縮和未壓縮） 的所有處理都必須處理硬體備份信任的執行環境中。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-177">5 - hello crypto, decoding and all handling of hello media (compressed and uncompressed) must be handled within a hardware backed trusted execution environment.</span></span> |
| <span data-ttu-id="1e1e9-178">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="1e1e9-178">content_key_specs</span></span> <br/> <span data-ttu-id="1e1e9-179">required_output_protection.hdc</span><span class="sxs-lookup"><span data-stu-id="1e1e9-179">required_output_protection.hdc</span></span> |<span data-ttu-id="1e1e9-180">字串 - 以下項目的其中一個：HDCP_NONE、HDCP_V1、HDCP_V2</span><span class="sxs-lookup"><span data-stu-id="1e1e9-180">string - one of: HDCP_NONE, HDCP_V1, HDCP_V2</span></span> |<span data-ttu-id="1e1e9-181">指出是否需要 HDCP</span><span class="sxs-lookup"><span data-stu-id="1e1e9-181">Indicates whether HDCP is require</span></span> |
| <span data-ttu-id="1e1e9-182">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="1e1e9-182">content_key_specs</span></span> <br/><span data-ttu-id="1e1e9-183">索引鍵</span><span class="sxs-lookup"><span data-stu-id="1e1e9-183">key</span></span> |<span data-ttu-id="1e1e9-184">Base64 </span><span class="sxs-lookup"><span data-stu-id="1e1e9-184">Base64</span></span> <br/><span data-ttu-id="1e1e9-185">編碼的字串</span><span class="sxs-lookup"><span data-stu-id="1e1e9-185">encoded string</span></span> |<span data-ttu-id="1e1e9-186">此追蹤記錄的內容金鑰 toouse。如果指定，hello track_type 或 key_id 是必要項。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-186">Content key toouse for this track. If specified, hello track_type or key_id is required.</span></span>  <span data-ttu-id="1e1e9-187">此選項可讓 hello 內容提供者而非讓 Widevine 授權伺服器查閱索引鍵或產生此音軌的 tooinject hello 內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-187">This option allows hello content provider tooinject hello content key for this track instead of letting Widevine license server generate or lookup a key.</span></span> |
| <span data-ttu-id="1e1e9-188">content_key_specs.key_id</span><span class="sxs-lookup"><span data-stu-id="1e1e9-188">content_key_specs.key_id</span></span> |<span data-ttu-id="1e1e9-189">Base64 編碼的二進位字串，16 位元組</span><span class="sxs-lookup"><span data-stu-id="1e1e9-189">Base64 encoded string  binary, 16 bytes</span></span> |<span data-ttu-id="1e1e9-190">Hello 索引鍵的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-190">Unique identifier for hello key.</span></span> |

## <a name="policy-overrides"></a><span data-ttu-id="1e1e9-191">原則覆寫</span><span class="sxs-lookup"><span data-stu-id="1e1e9-191">Policy Overrides</span></span>
| <span data-ttu-id="1e1e9-192">名稱</span><span class="sxs-lookup"><span data-stu-id="1e1e9-192">Name</span></span> | <span data-ttu-id="1e1e9-193">值</span><span class="sxs-lookup"><span data-stu-id="1e1e9-193">Value</span></span> | <span data-ttu-id="1e1e9-194">說明</span><span class="sxs-lookup"><span data-stu-id="1e1e9-194">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1e1e9-195">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="1e1e9-195">policy_overrides.</span></span> <span data-ttu-id="1e1e9-196">can_play</span><span class="sxs-lookup"><span data-stu-id="1e1e9-196">can_play</span></span> |<span data-ttu-id="1e1e9-197">布林值。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-197">boolean.</span></span> <span data-ttu-id="1e1e9-198">True 或 False</span><span class="sxs-lookup"><span data-stu-id="1e1e9-198">true or false</span></span> |<span data-ttu-id="1e1e9-199">表示播放內容允許的 hello。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-199">Indicates that playback of hello content is allowed.</span></span> <span data-ttu-id="1e1e9-200">預設值為 false。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-200">Default is false.</span></span> |
| <span data-ttu-id="1e1e9-201">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="1e1e9-201">policy_overrides.</span></span> <span data-ttu-id="1e1e9-202">can_persist</span><span class="sxs-lookup"><span data-stu-id="1e1e9-202">can_persist</span></span> |<span data-ttu-id="1e1e9-203">布林值。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-203">boolean.</span></span> <span data-ttu-id="1e1e9-204">True 或 False</span><span class="sxs-lookup"><span data-stu-id="1e1e9-204">true or false</span></span> |<span data-ttu-id="1e1e9-205">表示該 hello 授權可能保存的 toonon 揮發性儲存體，供離線使用。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-205">Indicates that hello license may be persisted toonon-volatile storage for offline use.</span></span> <span data-ttu-id="1e1e9-206">預設值為 false。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-206">Default is false.</span></span> |
| <span data-ttu-id="1e1e9-207">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="1e1e9-207">policy_overrides.</span></span> <span data-ttu-id="1e1e9-208">can_renew</span><span class="sxs-lookup"><span data-stu-id="1e1e9-208">can_renew</span></span> |<span data-ttu-id="1e1e9-209">布林值 true 或 false</span><span class="sxs-lookup"><span data-stu-id="1e1e9-209">boolean true or false</span></span> |<span data-ttu-id="1e1e9-210">表示允許更新此授權。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-210">Indicates that renewal of this license is allowed.</span></span> <span data-ttu-id="1e1e9-211">如果為 true，hello hello 授權期間可以擴充的活動訊號。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-211">If true, hello duration of hello license can be extended by heartbeat.</span></span> <span data-ttu-id="1e1e9-212">預設值為 false。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-212">Default is false.</span></span> |
| <span data-ttu-id="1e1e9-213">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="1e1e9-213">policy_overrides.</span></span> <span data-ttu-id="1e1e9-214">license_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="1e1e9-214">license_duration_seconds</span></span> |<span data-ttu-id="1e1e9-215">int64</span><span class="sxs-lookup"><span data-stu-id="1e1e9-215">int64</span></span> |<span data-ttu-id="1e1e9-216">表示此特定授權的 hello 時間間隔。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-216">Indicates hello time window for this specific license.</span></span> <span data-ttu-id="1e1e9-217">值為 0 表示無限制 toohello 期間。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-217">A value of 0 indicates that there is no limit toohello duration.</span></span> <span data-ttu-id="1e1e9-218">預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-218">Default is 0.</span></span> |
| <span data-ttu-id="1e1e9-219">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="1e1e9-219">policy_overrides.</span></span> <span data-ttu-id="1e1e9-220">rental_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="1e1e9-220">rental_duration_seconds</span></span> |<span data-ttu-id="1e1e9-221">int64</span><span class="sxs-lookup"><span data-stu-id="1e1e9-221">int64</span></span> |<span data-ttu-id="1e1e9-222">指出允許播放時，hello 時間間隔。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-222">Indicates hello time window while playback is permitted.</span></span> <span data-ttu-id="1e1e9-223">值為 0 表示無限制 toohello 期間。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-223">A value of 0 indicates that there is no limit toohello duration.</span></span> <span data-ttu-id="1e1e9-224">預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-224">Default is 0.</span></span> |
| <span data-ttu-id="1e1e9-225">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="1e1e9-225">policy_overrides.</span></span> <span data-ttu-id="1e1e9-226">playback_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="1e1e9-226">playback_duration_seconds</span></span> |<span data-ttu-id="1e1e9-227">int64</span><span class="sxs-lookup"><span data-stu-id="1e1e9-227">int64</span></span> |<span data-ttu-id="1e1e9-228">hello 檢視視窗中的 hello 授權持續時間內啟動播放的時間。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-228">hello viewing window of time once playback starts within hello license duration.</span></span> <span data-ttu-id="1e1e9-229">值為 0 表示無限制 toohello 期間。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-229">A value of 0 indicates that there is no limit toohello duration.</span></span> <span data-ttu-id="1e1e9-230">預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-230">Default is 0.</span></span> |
| <span data-ttu-id="1e1e9-231">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="1e1e9-231">policy_overrides.</span></span> <span data-ttu-id="1e1e9-232">renewal_server_url</span><span class="sxs-lookup"><span data-stu-id="1e1e9-232">renewal_server_url</span></span> |<span data-ttu-id="1e1e9-233">字串</span><span class="sxs-lookup"><span data-stu-id="1e1e9-233">string</span></span> |<span data-ttu-id="1e1e9-234">Toohello 指定 URL 應該導向此授權的所有活動訊號 （更新） 要求。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-234">All heartbeat (renewal) requests for this license shall be directed toohello specified URL.</span></span> <span data-ttu-id="1e1e9-235">只有在 can_renew 為 true 時才會使用這個欄位。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-235">This field is only used if can_renew is true.</span></span> |
| <span data-ttu-id="1e1e9-236">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="1e1e9-236">policy_overrides.</span></span> <span data-ttu-id="1e1e9-237">renewal_delay_seconds</span><span class="sxs-lookup"><span data-stu-id="1e1e9-237">renewal_delay_seconds</span></span> |<span data-ttu-id="1e1e9-238">int64</span><span class="sxs-lookup"><span data-stu-id="1e1e9-238">int64</span></span> |<span data-ttu-id="1e1e9-239">license_start_time 之後經過幾秒才會第一次嘗試更新。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-239">How many seconds after license_start_time, before renewal is first attempted.</span></span> <span data-ttu-id="1e1e9-240">只有在 can_renew 為 true 時才會使用這個欄位。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-240">This field is only used if can_renew is true.</span></span> <span data-ttu-id="1e1e9-241">預設值為 0</span><span class="sxs-lookup"><span data-stu-id="1e1e9-241">Default is 0</span></span> |
| <span data-ttu-id="1e1e9-242">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="1e1e9-242">policy_overrides.</span></span> <span data-ttu-id="1e1e9-243">renewal_retry_interval_seconds</span><span class="sxs-lookup"><span data-stu-id="1e1e9-243">renewal_retry_interval_seconds</span></span> |<span data-ttu-id="1e1e9-244">int64</span><span class="sxs-lookup"><span data-stu-id="1e1e9-244">int64</span></span> |<span data-ttu-id="1e1e9-245">指定 hello 延遲後續授權更新要求失敗時之間的秒數。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-245">Specifies hello delay in seconds between subsequent license renewal requests, in case of failure.</span></span> <span data-ttu-id="1e1e9-246">只有在 can_renew 為 true 時才會使用這個欄位。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-246">This field is only used if can_renew is true.</span></span> |
| <span data-ttu-id="1e1e9-247">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="1e1e9-247">policy_overrides.</span></span> <span data-ttu-id="1e1e9-248">renewal_recovery_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="1e1e9-248">renewal_recovery_duration_seconds</span></span> |<span data-ttu-id="1e1e9-249">int64</span><span class="sxs-lookup"><span data-stu-id="1e1e9-249">int64</span></span> |<span data-ttu-id="1e1e9-250">允許，在其中播放時更新 toocontinue hello 視窗是時間的嘗試，因為 toobackend 問題 hello 授權伺服器尚未成功。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-250">hello window of time, in which playback is allowed toocontinue while renewal is attempted, yet unsuccessful due toobackend problems with hello license server.</span></span> <span data-ttu-id="1e1e9-251">值為 0 表示無限制 toohello 期間。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-251">A value of 0 indicates that there is no limit toohello duration.</span></span> <span data-ttu-id="1e1e9-252">只有在 can_renew 為 true 時才會使用這個欄位。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-252">This field is only used if can_renew is true.</span></span> |
| <span data-ttu-id="1e1e9-253">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="1e1e9-253">policy_overrides.</span></span> <span data-ttu-id="1e1e9-254">renew_with_usage</span><span class="sxs-lookup"><span data-stu-id="1e1e9-254">renew_with_usage</span></span> |<span data-ttu-id="1e1e9-255">布林值 true 或 false</span><span class="sxs-lookup"><span data-stu-id="1e1e9-255">boolean true or false</span></span> |<span data-ttu-id="1e1e9-256">表示啟動使用量時，應該更新傳送該 hello 授權。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-256">Indicates that hello license shall be sent for renewal when usage is started.</span></span> <span data-ttu-id="1e1e9-257">只有在 can_renew 為 true 時才會使用這個欄位。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-257">This field is only used if can_renew is true.</span></span> |

## <a name="session-initialization"></a><span data-ttu-id="1e1e9-258">工作階段初始化</span><span class="sxs-lookup"><span data-stu-id="1e1e9-258">Session Initialization</span></span>
| <span data-ttu-id="1e1e9-259">名稱</span><span class="sxs-lookup"><span data-stu-id="1e1e9-259">Name</span></span> | <span data-ttu-id="1e1e9-260">值</span><span class="sxs-lookup"><span data-stu-id="1e1e9-260">Value</span></span> | <span data-ttu-id="1e1e9-261">說明</span><span class="sxs-lookup"><span data-stu-id="1e1e9-261">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1e1e9-262">provider_session_token</span><span class="sxs-lookup"><span data-stu-id="1e1e9-262">provider_session_token</span></span> |<span data-ttu-id="1e1e9-263">Base64 編碼的字串</span><span class="sxs-lookup"><span data-stu-id="1e1e9-263">Base64 encoded string</span></span> |<span data-ttu-id="1e1e9-264">此工作階段權杖在 hello 授權中傳回，而且會存在於後續的更新作業。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-264">This session token is passed back in hello license and will exist in subsequent renewals.</span></span>  <span data-ttu-id="1e1e9-265">超過工作階段將不會保存 hello 工作階段權杖。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-265">hello session token will not persist beyond sessions.</span></span> |
| <span data-ttu-id="1e1e9-266">provider_client_token</span><span class="sxs-lookup"><span data-stu-id="1e1e9-266">provider_client_token</span></span> |<span data-ttu-id="1e1e9-267">Base64 編碼的字串</span><span class="sxs-lookup"><span data-stu-id="1e1e9-267">Base64 encoded string</span></span> |<span data-ttu-id="1e1e9-268">用戶端權杖 toosend hello 授權回應中。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-268">Client token toosend back in hello license response.</span></span>  <span data-ttu-id="1e1e9-269">如果 hello 授權要求包含用戶端權杖，則會忽略此值。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-269">If hello license request contains a client token, this value is ignored.</span></span> <span data-ttu-id="1e1e9-270">hello 用戶端權杖會授權工作階段之外保存。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-270">hello client token will persist beyond license sessions.</span></span> |
| <span data-ttu-id="1e1e9-271">override_provider_client_token</span><span class="sxs-lookup"><span data-stu-id="1e1e9-271">override_provider_client_token</span></span> |<span data-ttu-id="1e1e9-272">布林值。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-272">boolean.</span></span> <span data-ttu-id="1e1e9-273">True 或 False</span><span class="sxs-lookup"><span data-stu-id="1e1e9-273">true or false</span></span> |<span data-ttu-id="1e1e9-274">如果為 false，hello 授權要求包含用戶端權杖時，使用 hello 要求中的 hello 語彙基元，即使此結構中指定用戶端權杖。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-274">If false and hello license request contains a client token, use hello token from hello request even if a client token was specified in this structure.</span></span>  <span data-ttu-id="1e1e9-275">如果為 true，一律使用這個結構中指定的 hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-275">If true, always use hello token specified in this structure.</span></span> |

## <a name="configure-your-widevine-licenses-using-net-types"></a><span data-ttu-id="1e1e9-276">使用 .NET 型別設定您的 Widevine 授權</span><span class="sxs-lookup"><span data-stu-id="1e1e9-276">Configure your Widevine licenses using .NET types</span></span>
<span data-ttu-id="1e1e9-277">媒體服務提供可讓您設定 Widevine 授權的 .NET API。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-277">Media Services provides .NET APIs that let you configure your Widevine licenses.</span></span> 

### <a name="classes-as-defined-in-hello-media-services-net-sdk"></a><span data-ttu-id="1e1e9-278">Hello Media Services.NET SDK 中所定義的類別</span><span class="sxs-lookup"><span data-stu-id="1e1e9-278">Classes as defined in hello Media Services .NET SDK</span></span>
<span data-ttu-id="1e1e9-279">hello 下面是這些類型的 hello 定義。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-279">hello following are hello definitions of these types.</span></span>

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

### <a name="example"></a><span data-ttu-id="1e1e9-280">範例</span><span class="sxs-lookup"><span data-stu-id="1e1e9-280">Example</span></span>
<span data-ttu-id="1e1e9-281">下列範例會示範如何 hello toouse.NET Api tooconfigure 簡單 Widevine 授權。</span><span class="sxs-lookup"><span data-stu-id="1e1e9-281">hello following example shows how toouse .NET APIs tooconfigure  a simple Widevine license.</span></span>

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


## <a name="media-services-learning-paths"></a><span data-ttu-id="1e1e9-282">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="1e1e9-282">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1e1e9-283">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="1e1e9-283">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="1e1e9-284">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1e1e9-284">See also</span></span>
[<span data-ttu-id="1e1e9-285">使用 PlayReady 和/或 Widevine 動態 Common Encryption</span><span class="sxs-lookup"><span data-stu-id="1e1e9-285">Using PlayReady and/or Widevine Dynamic Common Encryption</span></span>](media-services-protect-with-drm.md)

