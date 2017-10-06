---
title: "aaaScheduler 限制及預設值"
description: "排程器限制及預設值"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 88f4a3e9-6dbd-4943-8543-f0649d423061
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 6fe0600d3ce3249d5aab1b877369b175316b5437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-limits-and-defaults"></a>排程器限制及預設值
## <a name="scheduler-quotas-limits-defaults-and-throttles"></a>排程器配額、限制、預設值和節流
[!INCLUDE [scheduler-limits-table](../../includes/scheduler-limits-table.md)]

## <a name="hello-x-ms-request-id-header"></a>hello x ms-要求識別碼標頭
每個對 hello 排程器服務所提出的要求會傳回回應標頭**x ms-要求識別碼**。此標頭包含唯一識別 hello 要求的不透明值。

如果要求不一致的方式失敗，且您有會確認 hello 要求為正確的組成之後，您可以使用此值 tooreport hello 錯誤 tooMicrosoft。 在報表中，加入 x ms-要求識別碼，hello 的大約時間 hello 值該 hello 製作要求之 hello hello 訂用帳戶、 工作集合和/或作業的識別碼和 hello hello 要求嘗試的作業類型。

## <a name="see-also"></a>另請參閱
 [排程器是什麼？](scheduler-intro.md)

 [Azure 排程器概念、術語及實體階層](scheduler-concepts-terms.md)

 [開始在 hello Azure 入口網站中使用排程器](scheduler-get-started-portal.md)

 [Azure 排程器的計劃和計費](scheduler-plans-billing.md)

 [Azure 排程器 REST API 參考](https://msdn.microsoft.com/library/mt629143)

 [Azure 排程器 PowerShell Cmdlet 參考](scheduler-powershell-reference.md)

 [Azure 排程器高可用性和可靠性](scheduler-high-availability-reliability.md)

 [Azure 排程器輸出驗證](scheduler-outbound-authentication.md)

