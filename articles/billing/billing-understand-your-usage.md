---
title: "aaaUnderstand Azure 的詳細使用量 |Microsoft 文件"
description: "深入了解如何 tooread 並了解您 Azure 訂用帳戶的詳細使用量 CSV hello 區段"
services: 
documentationcenter: 
author: tonguyen10
manager: tonguyen
editor: 
tags: billing
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: tonguyen
ms.openlocfilehash: c9284bf94bfa9f36cdd5d39e653a35def7c1aa34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understand-terms-on-your-microsoft-azure-detailed-usage-charges"></a>了解您 Microsoft Azure 詳細使用量費用的相關字詞 
hello 費用的 CSV 檔案包含每日的詳細使用狀況和 hello 目前計費週期的計量器層級的使用費用。 

tooget 您詳細的使用方式的檔案，請參閱[如何 tooget 您 Azure 帳單寄送發票及每日使用量資料](billing-download-azure-invoice-daily-usage-date.md)。
此檔案以逗號分隔值 (.csv) 檔案格式提供，您可以使用試算表應用程式開啟這個檔案。 如果您看到兩個可用版本，請下載第 2 個版本。 這是 hello 最新的檔案格式。

使用費用是總 hello**每月**訂用帳戶的費用。 使用量費用不會將任何信用額度或折扣列入考慮。

## <a name="detailed-terms-and-descriptions-of-your-detailed-usage-file"></a>詳細使用量檔案的詳細字詞和描述
hello 下列章節說明顯示在第 2 版的 hello 詳細使用狀況檔案中的 hello 重要詞彙。

### <a name="statement"></a>陳述式
hello hello 上方區段詳細使用 CSV 檔案顯示 hello 服務期間 hello 月計費期間使用。 hello 下表列出 hello 條款和本節中所顯示的描述。

| 詞彙 | 說明 |
| --- | --- |
|計費期間 |當使用 hello 公尺 hello 計費期間 |
|計量類別 |識別 hello 最上層服務如 hello 使用量 |
|計量子類別 |定義 Azure 服務，可能會影響 hello 速率 hello 類型 |
|計量名稱 |識別所耗用的 hello 計量表的測量單位，hello |
|計量區域 |識別 hello 資料中心位置為基礎的價格特定服務的 hello 資料中心位置 |
|SKU |識別每個 Azure 計量表 hello 唯一系統識別碼 |
|單位 |識別 hello hello 服務負責中的單位。 例如，GB、小時、10,000 秒。 |
|已耗用的數量 |hello 計量表 hello 計費週期期間所使用的 hello 數量 |
|已包括的數量 |hello 數量，就會包含在目前的計費週期中的 hello 計量的 |
|超額數量 |顯示 hello 差異 hello 耗用的數量和之間 hello 包含數量。 我們會針對此數量向您收費。 沒有包含數量與隨用隨付優惠與 hello 優惠，這個總數是 hello 相同 hello 耗用的數量。 |
|承諾用量期間 |顯示您與 6 或 12 個月的優惠相關聯的承諾金額會減去的 hello 計量表費用。 計量費用得依時間順序減去。 |
|貨幣 |您目前的計費週期中使用的 hello 貨幣 |
|超額部分 |顯示超過您的承諾金額與 6 或 12 個月的優惠相關聯的 hello 計量表費用 |
|承諾用量費率 |顯示與 6 或 12 個月的優惠相關聯的 hello 總承諾金額為基礎的 hello 承諾速率 |
|費率 |hello 速率收費每計費單位 |
|值 |顯示 hello 結果相乘 hello 逐 hello 速率超額部分 Quantity 資料行。 如果耗用的數量不超過的 hello hello 包含數量，此資料行中就不需付費。 |

### <a name="daily-usage"></a>每日使用量

hello hello CSV 檔案的每日使用量 > 一節顯示會影響 hello 帳單費率的使用方式詳細資料。 hello 下表列出 hello 條款和本節中所顯示的描述。

| 詞彙 | 說明 |
| --- | --- |
|使用日期 |hello 日期在何時使用 hello 計量表 |
|計量類別 |識別 hello 最上層的服務，其屬於這種使用方式 |
|計量識別碼 |hello 計費用 tooprice 計費的使用量計量表識別項 |
|計量子類別 |定義 hello Azure 服務類型，它可能會影響 hello 速率 |
|計量名稱 |識別所耗用的 hello 計量表的測量單位，hello |
|計量區域 |識別 hello 資料中心位置為基礎的價格特定服務的 hello 資料中心位置 |
|單位 |識別 hello 單位中的 hello 計量表會產生費用。 例如，GB、小時、10,000 秒。 |
|已耗用的數量 |已使用針對該日的 hello 計量表的 hello 數量 |
|資源位置 |識別 hello hello 計量器執行所在的資料中心 |
|已耗用的服務 |hello 您所使用的 Azure 平台服務 |
|資源群組 |hello 資源群組中的 hello 已部署的計量器正在執行中。 <br/><br/>如需詳細資訊，請參閱 [Azure Resource Manager 概觀](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)。 |
|執行個體識別碼 | hello 識別碼 hello 計量表。 <br/><br/> hello 識別項包含 hello 建立時指定的 hello 計量表的名稱。 Hello 資源的任何一個 hello 名稱或 hello 完整資源 id。 如需詳細資訊，請參閱 [Azure Resource Manager API](https://docs.microsoft.com/rest/api/resources/resources)。 |
|標記 | 您指派 toohello 計量表的標記。 使用標記 toogroup 帳單記錄。<br/><br/>例如，您可以使用標記 toodistribute 成本的 hello 部門使用 hello 計量表。 支援發出的標記的服務是虛擬機器、 儲存和使用 hello 佈建的網路服務[Azure 資源管理員 API](https://docs.microsoft.com/rest/api/resources/resources)。 如需詳細資訊，請參閱[使用標記組織您的 Azure 資源](http://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/)。 |
|其他資訊 |服務專屬的中繼資料。 例如，虛擬機器的影像類型。 |
|服務資訊 1 |hello 服務所屬 tooon 訂用帳戶的 hello 專案名稱 |
|服務資訊 2 |舊版欄位，可擷取選擇性的服務特定中繼資料 |

## <a name="how-do-i-make-sure-that-hello-charges-in-my-detailed-usage-file-are-correct"></a>如何確定我的詳細使用狀況檔案中的 hello 費用是否正確？
如果您需要詳細使用量檔案費用的更多詳細資料，請參閱[了解您的 Microsoft Azure 帳單。](./billing-understand-your-bill.md)

## <a name="external"></a>外部服務費用呢？
外部服務 (也稱為 Marketplace 訂單) 是由獨立服務廠商提供，並會分開計費。 hello 費用不會顯示 hello Azure 發票上。 詳細資訊，請參閱 toolearn[了解 Azure 外部的服務費用](billing-understand-your-azure-marketplace-charges.md)。

## <a name="need-help-contact-support"></a>需要協助嗎？ 請連絡支援人員。
如果仍需要協助，請[連絡支援人員](https://portal.azure.com/?)以快速解決您的問題。
