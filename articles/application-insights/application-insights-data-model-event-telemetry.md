---
title: "aaaAzure Insights 遙測資料模型的應用程式-事件遙測 |Microsoft 文件"
description: "事件遙測的 Application Insights 資料模型"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: cd7dc3c5f4f3df22b7a52ee79fcad566a27a9f4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="event-telemetry-application-insights-data-model"></a>事件遙測：Application Insights 資料模型

您可以建立事件遙測項目 (在[Application Insights](app-insights-overview.md)) toorepresent 應用程式中發生的事件。 通常它是與使用者互動的事件，例如按一下按鈕或簽出訂單。 它也可以是初始化或組態更新等應用程式生命週期事件。 

語意上來說，事件可能會或可能不是相互關聯的 toorequests。 不過，如果使用得當，事件遙測比要求或追蹤更重要。 代表企業遙測事件，而且應該主旨 tooseparate，較不主動[取樣](app-insights-api-filtering-sampling.md)。

## <a name="name"></a>名稱

事件名稱。 tooallow 適當的群組和實用的度量，限制您的應用程式，使其產生少量個別的事件名稱。 例如，針對每個產生的事件執行個體，不要使用不同的名稱。

最大長度︰512 個字元

## <a name="custom-properties"></a>自訂屬性

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>自訂度量

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a>後續步驟

- 如需 Application Insights 類型和資料模型，請參閱[資料模型](application-insights-data-model.md)。
- [撰寫自訂事件遙測](app-insights-api-custom-events-metrics.md#trackevent)
- 查看 Application Insights 支援的[平台](app-insights-platforms.md)。
