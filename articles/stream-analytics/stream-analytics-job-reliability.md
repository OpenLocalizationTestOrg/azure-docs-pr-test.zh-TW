---
title: "使用 Azure 串流分析工作來避免發生服務中斷 | Microsoft Docs"
description: "提供讓您的「串流分析」工作升級具有彈性的指引。"
services: stream-analytics
documentationCenter: 
authors: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 3ac65c93ecb47e93e963dd9869a7af70f73b19c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="guarantee-stream-analytics-job-reliability-during-service-updates"></a>在服務更新期間確保串流分析工作可靠性

在完全受管理的服務的部分是 hello 功能 toointroduce 新服務功能和增強功能的快速步調。 因此，「串流分析」可以每週 (或更頻繁地) 進行服務更新部署。 無論完成多少測試仍會有現有的執行作業可能會中斷到期 toohello 引入 bug 的風險。 對於這些風險執行重要的資料流處理工作的客戶需要 toobe 避免。 機制客戶可以使用 tooreduce 這個風險是 Azure 的**[配對的區域](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**模型。 

## <a name="how-do-azure-paired-regions-address-this-concern"></a>Azure 配對區域如何解決這個問題？

「串流分析」可確保以個別的批次更新在配對區域中的工作。 如此一來 hello 更新 tooidentify 潛在的重大 bug，以及修復它們之間沒有足夠的時間間隔。

_與 hello 例外狀況的印度中部_（其配對的區域、 印度南部及印度，並沒有資料流分析存在），分析就不會發生在 hello 更新 tooStream hello 部署相同的時間中的一組配對的區域。 在多個區域部署**hello 中相同的群組**可能會發生**hello 在同一時間**。

上的文件： hello **[可用性和配對的區域](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**具有區域會經過配對 hello 最新的資訊。

建議使用的 toodeploy 相同工作 tooboth 配對區域的客戶。 此外 tooStream Analytics 的內部監視功能，客戶也是建議 toomonitor hello 作業如同**兩者**實際執行的作業。 如果符號為識別的 toobe hello Stream Analytics 服務更新的結果，適當地擴大，並容錯移轉任何下游取用者 toohello 狀況良好的作業輸出。 擴大 toosupport 會防止受到 hello 新部署的 hello 配對的區域及維護 hello 完整性的 hello 配對作業。
