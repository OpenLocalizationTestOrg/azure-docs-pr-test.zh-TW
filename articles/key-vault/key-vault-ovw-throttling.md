---
ms.assetid: 
title: "金鑰保存庫節流指引 aaaAzure |Microsoft 文件"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 06/21/2017
ms.openlocfilehash: a75cf96bc6503e51f14378bee598bad57e85be82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-throttling-guidance"></a>Azure Key Vault 節流指導方針

節流是限制同時呼叫 toohello Azure 服務 tooprevent 的過度使用資源的 hello 數目的程序初始化。 Azure 金鑰保存庫 (AKV) 是設計的 toohandle 大量的要求。 如果產生大量的要求，就會發生，節流設定您的用戶端要求可協助維護最佳效能和可靠性的 hello AKV 服務。

節流限制會根據 hello 案例而有所不同。 例如，如果您正在執行大量的寫入，hello 節流可能性高於如果您只執行讀取。

## <a name="how-does-key-vault-handle-its-limits"></a>Key Vault 如何處理其限制？

金鑰保存庫中的服務限制有 tooprevent 不當使用的資源，並確定所有金鑰保存庫的用戶端的服務品質。 超過服務閾值時，Key Vault 可以限制一段時間內來自該用戶端的任何進一步要求。 發生這種情況，金鑰保存庫會傳回 HTTP 狀態碼 429 (太多要求)，和 hello 要求會失敗。 此外，無法傳回 429 計數朝向 hello 節流閥限制追蹤的金鑰保存庫的要求。 

如果您有需要更高節流限制的有效商務案例，請與我們連絡。


## <a name="how-toothrottle-your-app-in-response-tooservice-limits"></a>如何 toothrottle 回應 tooservice 中的應用程式限制

hello 如下**最佳做法**節流您的應用程式：
- Hello 的減少每個要求的作業。
- 減少 hello 頻率的要求。
- 避免立即重試。 
    - 所有要求都會讓您的使用量限制累加。

當您實作您的應用程式錯誤處理時，使用 hello HTTP 錯誤程式碼 429 toodetect hello 需要用戶端節流。 如果 hello 要求再次失敗，HTTP 429 錯誤代碼，您仍然遇到 Azure 服務的限制。 繼續 toouse hello 建議使用的用戶端節流方法，重試 hello 要求，直到成功為止。

### <a name="recommended-client-side-throttling-method"></a>建議使用的用戶端節流方法

針對 HTTP 錯誤碼 429，使用指數型輪詢方法開始為您的用戶端進行節流處理：

1. 等候 1 秒，重試要求
2. 如果等候 2 秒仍然進行節流處理，重試要求
3. 如果等候 4 秒仍然進行節流處理，重試要求
4. 如果等候 8 秒仍然進行節流處理，重試要求
5. 如果等候 16 秒仍然進行節流處理，重試要求

此時，您應該不會收到 HTTP 429 回應碼。

## <a name="see-also"></a>另請參閱

節流 hello Microsoft 雲端上的更深入方向，請參閱[節流模式](https://docs.microsoft.com/azure/architecture/patterns/throttling)。

