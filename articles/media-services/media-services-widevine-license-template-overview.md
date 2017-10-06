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
# <a name="widevine-license-template-overview"></a>Widevine 授權範本概觀
## <a name="overview"></a>概觀
Azure 媒體服務現在可讓您 tooconfigure 和要求 Widevine 授權。 Hello 使用者播放程式會嘗試 tooplay Widevine 受保護的內容、 要求時傳送的 toohello 授權傳遞服務 tooobtain 授權。 如果 hello 授權服務核准 hello 要求，就會發出這是傳送的 toohello 用戶端 hello 授權，而且可以是使用的 toodecrypt 插 hello 指定的內容。

Widevine 授權要求會格式化為 JSON 訊息。  

>[!NOTE]
> 您可以選擇 toocreate 空的訊息沒有值只是"{}"，而且會使用所有預設值建立授權範本。 hello 預設適用於大部分情況。 例如，一律必須使用預設值的 MS 型授權遞送案例。 如果您需要 tooset hello 「 提供者 」 和 「 content_id"值，提供者必須符合 Google Widevine 認證。

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

## <a name="json-message"></a>JSON 訊息
| 名稱 | 值 | 說明 |
| --- | --- | --- |
| payload |Base64 編碼的字串 |用戶端傳送嗨授權要求。 |
| content_id |Base64 編碼的字串 |識別項會用於每個 content_key_specs.track_type tooderive KeyId(s) 與內容的索引鍵。 |
| provider |字串 |使用內容金鑰和原則 toolook。 若將 MS 金鑰遞送用於 Widevine 授權遞送，系統會忽略此參數。 |
| policy_name |string |先前已登錄原則的名稱。 選用 |
| allowed_track_types |列舉 |SD_ONLY 或 SD_HD。 控制授權中應該包含的內容金鑰 |
| content_key_specs |JSON 結構的陣列，請參閱下方的 **內容金鑰規格** |精細地的控制內容金鑰 tooreturn 上。 如需詳細資料，請參閱以下的內容金鑰規格。  只可以指定 allowed_track_types 和 content_key_specs 中的一個。 |
| use_policy_overrides_exclusively |布林值。 True 或 False |使用 policy_overrides 所指定的原則屬性，並略過先前儲存的所有原則。 |
| policy_overrides |JSON 結構，請參閱以下的 **原則覆寫** |此授權的原則設定。  Hello 事件中這項資產有一個預先定義的原則，就會使用這些指定的值。 |
| session_init |JSON 結構，請參閱下方的 **工作階段初始化** |Toolicense 傳遞選擇性的資料。 |
| parse_only |布林值。 True 或 False |會剖析 hello 授權要求，但不發出任何授權。 不過，hello 回應會傳回值格式 hello 授權要求。 |

## <a name="content-key-specs"></a>內容金鑰規格
預先存在的原則存在，有任何 hello hello 內容金鑰規格中的值不需要 toospecify。 hello 預先存在此內容相關聯的原則會使用的 toodetermine hello 輸出保護 CGMS HDCP 等。  如果預先存在的原則未向 hello Widevine 授權伺服器，hello 內容提供者可以插入 hello 授權要求的 hello 值。   

每個 content_key_specs 必須指定所有曲目，不論 hello 選項 use_policy_overrides_exclusively。 

| 名稱 | 值 | 說明 |
| --- | --- | --- |
| content_key_specs track_type |字串 |追蹤類型名稱。 如果 content_key_specs hello 授權要求中指定，請確定所有追蹤的 toospecify 類型明確。 失敗 toodo 因此將會導致失敗 tooplayback 過去 10 秒。 |
| content_key_specs  <br/> security_level |uint32 |定義用戶端對於播放的穩健性需求。 <br/> 1 - 以軟體為基礎白箱加密是必要的。 <br/> 2 - 軟體加密和模糊化的解碼器是必要的。 <br/> 3-hello 金鑰材料和密碼編譯作業必須在硬體備份信任的執行的環境中執行。 <br/> 4-hello 密碼編譯和解碼的內容必須硬體備份信任的執行環境中執行。  <br/> 5-hello 密碼編譯、 解碼和 hello 媒體 （壓縮和未壓縮） 的所有處理都必須處理硬體備份信任的執行環境中。 |
| content_key_specs <br/> required_output_protection.hdc |字串 - 以下項目的其中一個：HDCP_NONE、HDCP_V1、HDCP_V2 |指出是否需要 HDCP |
| content_key_specs <br/>索引鍵 |Base64  <br/>編碼的字串 |此追蹤記錄的內容金鑰 toouse。如果指定，hello track_type 或 key_id 是必要項。  此選項可讓 hello 內容提供者而非讓 Widevine 授權伺服器查閱索引鍵或產生此音軌的 tooinject hello 內容金鑰。 |
| content_key_specs.key_id |Base64 編碼的二進位字串，16 位元組 |Hello 索引鍵的唯一識別碼。 |

## <a name="policy-overrides"></a>原則覆寫
| 名稱 | 值 | 說明 |
| --- | --- | --- |
| policy_overrides can_play |布林值。 True 或 False |表示播放內容允許的 hello。 預設值為 false。 |
| policy_overrides can_persist |布林值。 True 或 False |表示該 hello 授權可能保存的 toonon 揮發性儲存體，供離線使用。 預設值為 false。 |
| policy_overrides can_renew |布林值 true 或 false |表示允許更新此授權。 如果為 true，hello hello 授權期間可以擴充的活動訊號。 預設值為 false。 |
| policy_overrides license_duration_seconds |int64 |表示此特定授權的 hello 時間間隔。 值為 0 表示無限制 toohello 期間。 預設值為 0。 |
| policy_overrides rental_duration_seconds |int64 |指出允許播放時，hello 時間間隔。 值為 0 表示無限制 toohello 期間。 預設值為 0。 |
| policy_overrides playback_duration_seconds |int64 |hello 檢視視窗中的 hello 授權持續時間內啟動播放的時間。 值為 0 表示無限制 toohello 期間。 預設值為 0。 |
| policy_overrides renewal_server_url |字串 |Toohello 指定 URL 應該導向此授權的所有活動訊號 （更新） 要求。 只有在 can_renew 為 true 時才會使用這個欄位。 |
| policy_overrides renewal_delay_seconds |int64 |license_start_time 之後經過幾秒才會第一次嘗試更新。 只有在 can_renew 為 true 時才會使用這個欄位。 預設值為 0 |
| policy_overrides renewal_retry_interval_seconds |int64 |指定 hello 延遲後續授權更新要求失敗時之間的秒數。 只有在 can_renew 為 true 時才會使用這個欄位。 |
| policy_overrides renewal_recovery_duration_seconds |int64 |允許，在其中播放時更新 toocontinue hello 視窗是時間的嘗試，因為 toobackend 問題 hello 授權伺服器尚未成功。 值為 0 表示無限制 toohello 期間。 只有在 can_renew 為 true 時才會使用這個欄位。 |
| policy_overrides renew_with_usage |布林值 true 或 false |表示啟動使用量時，應該更新傳送該 hello 授權。 只有在 can_renew 為 true 時才會使用這個欄位。 |

## <a name="session-initialization"></a>工作階段初始化
| 名稱 | 值 | 說明 |
| --- | --- | --- |
| provider_session_token |Base64 編碼的字串 |此工作階段權杖在 hello 授權中傳回，而且會存在於後續的更新作業。  超過工作階段將不會保存 hello 工作階段權杖。 |
| provider_client_token |Base64 編碼的字串 |用戶端權杖 toosend hello 授權回應中。  如果 hello 授權要求包含用戶端權杖，則會忽略此值。 hello 用戶端權杖會授權工作階段之外保存。 |
| override_provider_client_token |布林值。 True 或 False |如果為 false，hello 授權要求包含用戶端權杖時，使用 hello 要求中的 hello 語彙基元，即使此結構中指定用戶端權杖。  如果為 true，一律使用這個結構中指定的 hello 語彙基元。 |

## <a name="configure-your-widevine-licenses-using-net-types"></a>使用 .NET 型別設定您的 Widevine 授權
媒體服務提供可讓您設定 Widevine 授權的 .NET API。 

### <a name="classes-as-defined-in-hello-media-services-net-sdk"></a>Hello Media Services.NET SDK 中所定義的類別
hello 下面是這些類型的 hello 定義。

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

### <a name="example"></a>範例
下列範例會示範如何 hello toouse.NET Api tooconfigure 簡單 Widevine 授權。

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


## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>另請參閱
[使用 PlayReady 和/或 Widevine 動態 Common Encryption](media-services-protect-with-drm.md)

