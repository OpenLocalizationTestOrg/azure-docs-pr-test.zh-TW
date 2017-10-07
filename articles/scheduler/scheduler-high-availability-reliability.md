---
title: "aaaScheduler 高可用性和可靠性"
description: "排程器高可用性和可靠性"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 5ec78e60-a9b9-405a-91a8-f010f3872d50
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/16/2016
ms.author: deli
ms.openlocfilehash: 5c9efb333eb42b393adc5deea657ca99206d425e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-high-availability-and-reliability"></a>排程器高可用性和可靠性
## <a name="azure-scheduler-high-availability"></a>Azure 排程器高可用性
做為 Azure 平台服務的核心，Azure 排程器高度可用，並以地理區域備援服務部署和地理區域複寫為其特色。

### <a name="geo-redundant-service-deployment"></a>地理區域備援服務部署
透過 hello 現在是在 Azure 中幾乎每個地理區域中的 UI 使用 azure 排程器。 hello Azure 排程器中可用的地區清單為[此處所列](https://azure.microsoft.com/regions/#services)。 如果裝載區域中的資料中心呈現無法使用，Azure 排程器的 hello 容錯移轉功能會是，從另一個資料中心 hello 服務可供使用。

### <a name="geo-regional-job-replication"></a>地理區域工作複寫
不只是 hello Azure 排程器前端可用於管理要求，但您自己的工作也是地理複寫。 當在一個區域發生中斷時，Azure 排程器容錯移轉，並確保該 hello 執行作業時從另一個資料中心 hello 配對地理區域。

比方說，如果您在美國中南部建立工作，Azure 排程器就會在中北部自動複寫該工作。 當美國中南部中失敗，則 Azure 排程器可確保從美國中北部執行 hello 工作。 

![][1]

如此一來，Azure 排程器可確保您的資料會保留在 hello 同一個發生在 Azure 發生錯誤時更廣泛的地理區域。 如此一來，您需要不重複的作業只 tooadd 的高可用性 – Azure 排程器會自動提供高可用性功能，為您的工作。

## <a name="azure-scheduler-reliability"></a>Azure 排程器可靠性
Azure 排程器會保證其本身的高可用性，並採用不同的方法 toouser 建立的工作。 例如，您的工作可能會叫用無法使用的 HTTP 端點。 Azure 排程器仍會嘗試 tooexecute 您的工作成功，但發生失敗的替代選項 toodeal，提供。 Azure 排程器會以兩種方式執行此項動作：

### <a name="configurable-retry-policy-via-retrypolicy"></a>可透過 "retryPolicy" 設定重試原則
Azure 排程器可讓您 tooconfigure 重試原則。 根據預設，如果工作失敗，排程器會嘗試 hello 作業試四次，30 秒的間隔。 您可以重新設定此重試原則 toobe 更積極 （例如，十倍，30 秒的間隔） 或更加鬆散 （例如，兩次，每日間隔。）

舉例來說，當這樣做有幫助時，您可能會建立一週執行一次，並叫用 HTTP 端點的工作。 如果 hello HTTP 端點已關閉的幾個小時執行您的工作時，您可能不想 toowait 一個更多週的 hello 作業 toorun 再次因為即使 hello 預設重試原則將會失敗。 在這種情況下，您可能會重新設定 hello 標準重試原則 tooretry 每隔三小時 （舉例來說） 而不是每隔 30 秒。

如何重試原則，tooconfigure 參照太 toolearn[retryPolicy](scheduler-concepts-terms.md#retrypolicy)。

### <a name="alternate-endpoint-configurability-via-erroraction"></a>可透過 "ErrorAction" 設定替代端點的功能
如果 Azure 排程器工作的 hello 目標端點仍然無法連線，Azure 排程器會回復 toohello 替代錯誤處理端點後其重試原則。 如果已設定替代錯誤處理端點，Azure 排程器會叫用它。 有了替代端點，您自己的工作可用高 hello 字體的失敗。

例如，在 hello 圖，Azure 排程器會依照其重試原則 toohit New York web 服務。 Hello 重試失敗之後，它會檢查是否有替代。 接著會繼續，並開始進行 toohello 替代 hello 與相同的要求重試原則。

![][2]

請注意，hello 相同的重試原則適用於 tooboth hello 原始動作和 hello 替代錯誤動作。 它也可能 toohave hello 替代錯誤動作的動作類型為 hello 主要動作的動作類型不同。 比方說，hello 主要動作可能會叫用 HTTP 端點，而 hello 錯誤動作而可能儲存體佇列、 服務匯流排佇列或進行錯誤記錄的服務匯流排主題動作。

如何 tooconfigure 替代端點，參照太 toolearn[errorAction](scheduler-concepts-terms.md#action-and-erroraction)。

## <a name="see-also"></a>另請參閱
 [排程器是什麼？](scheduler-intro.md)

 [Azure 排程器概念、術語及實體階層](scheduler-concepts-terms.md)

 [開始在 hello Azure 入口網站中使用排程器](scheduler-get-started-portal.md)

 [Azure 排程器的計劃和計費](scheduler-plans-billing.md)

 [排程 toobuild 複雜的方式與進階循環使用 Azure 排程器](scheduler-advanced-complexity.md)

 [Azure 排程器 REST API 參考](https://msdn.microsoft.com/library/mt629143)

 [Azure 排程器 PowerShell Cmdlet 參考](scheduler-powershell-reference.md)

 [Azure 排程器限制、預設值和錯誤碼](scheduler-limits-defaults-errors.md)

 [Azure 排程器輸出驗證](scheduler-outbound-authentication.md)

[1]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image1.png

[2]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image2.png
