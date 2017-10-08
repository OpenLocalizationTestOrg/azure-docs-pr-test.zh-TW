---
title: "aaaUnderstand azure 帳單 |Microsoft 文件"
description: "深入了解如何 tooread 並了解您的使用量和 Azure 訂用帳戶的帳單"
services: 
documentationcenter: 
author: tonguyen10
manager: tonguyen
editor: 
tags: billing
ms.assetid: 32eea268-161c-4b93-8774-bc435d78a8c9
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/14/2017
ms.author: tonguyen
ms.openlocfilehash: a3195eb129b1576e8cb665aa6f88a1a2647edd78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understand-your-bill-for-microsoft-azure"></a>了解 Microsoft Azure 帳單
toounderstand Azure 收費，比較您的發票 hello 詳細每日使用量檔案與 hello 成本 hello Azure 入口網站中的管理報表。

tooobtain PDF 的發票，以及您詳細每日使用量檔案 CSV 的下載，請參閱[取得您的 Azure 帳單寄送發票及每日使用量資料](billing-download-azure-invoice-daily-usage-date.md)。 

如需您發票的詳細字詞和描述，以及詳細的每日使用量檔案，請參閱[了解您 Microsoft Azure 發票上的字詞](billing-understand-your-invoice.md)和[了解您 Microsoft Azure 詳細使用量上的字詞](billing-understand-your-usage.md)。 

如需 hello 成本管理報表的詳細資訊，請參閱[Azure 入口網站中成本管理](https://docs.microsoft.com/en-us/azure/billing/billing-getting-started)。


## <a name="charges"></a>如何確定我的發票中的 hello 費用是否正確？
如果您需要發票費用的更多詳細資料，有幾個選項供您選擇。

### <a name="option-1-review-your-invoice-and-compare-hello-usage-and-costs-with-hello-detailed-usage-csv-file"></a>選項 1： 檢閱您的發票，並與 hello 使用量和成本比較詳細的 hello 與使用 CSV 檔案

hello 詳細使用狀況 CSV 檔案會顯示您的費用的計費週期內的每日使用量。 tooget 詳細使用狀況的 CSV 檔，請參閱[取得您的 Azure 帳單寄送發票及每日使用量資料](https://docs.microsoft.com/en-us/azure/billing/billing-download-azure-invoice-daily-usage-date)。

使用費用會顯示在 hello 計量表層級。 hello 下列詞彙表示 hello 相同的動作，在這兩個 hello 發票和 hello 詳細使用狀況的檔案。 比方說，hello 計費週期 hello 發票上的是相等 toohello 計費週期 hello 詳細使用狀況檔案所示。

 | 發票 (PDF) | 詳細使用量 (CSV)|
 | --- | --- |
|計費週期 | 計費期間 |
 |名稱 |計量類別 |
 |類型 |計量子類別 |
 |資源 |計量名稱 |
 |區域 |計量區域 |
 |已耗用 |已耗用的數量 |
 |已包括 |已包括的數量 |
 |可計費 |超額數量 |

hello**使用費**發票的區段具有每個計量器在計費期間所耗用的 hello 總計值。 例如，hello 下列螢幕擷取畫面顯示 hello Azure 排程器服務的使用費用。

![發票使用量費用](./media/billing-understand-your-bill/1.png)

hello**陳述式**> 一節的詳細使用狀況 CSV 顯示 hello 相同的費用。 這兩個 hello*已使用*量和*值*相符 hello 發票。

![CSV 使用量費用](./media/billing-understand-your-bill/2.png)

toosee 日，請移 toohello 這筆費用明細**每日使用量**hello CSV 的區段。 篩選 」 排程器 」 下*計量表類別*，您可以看到哪些天 hello 計量表已用和多少的使用狀況。 hello*資源*和*資源群組*也會列出資訊進行比較。 hello*已使用*值應該加總 toowhat 的 hello 發票上顯示。

![Hello CSV 中的每日使用量 > 一節](./media/billing-understand-your-bill/3.png)

每日，tooget hello 成本乘以 hello*已使用*量與 hello*速率*值從 hello**陳述式**> 一節。

深入了解 hello 發票 toolearn 看到[了解您的 Azure 發票](billing-understand-your-invoice.md)。

請參閱有關每個 hello CSV 中的 hello 行 toolearn[了解 Azure 的詳細的使用量](billing-understand-your-invoice.md)。

### <a name="option-2-review-your-invoice-and-compare-with-hello-usage-and-costs-in-hello-azure-portal"></a>選項 2： 檢閱您的發票，並以 hello 使用方式與 hello Azure 入口網站中的成本比較

hello Azure 入口網站也可協助您確認您的費用。 hello Azure 入口網站會將成本管理圖表提供您的使用量和 hello 費用，您的發票上的快速概觀。

toocontinue 與 hello 從上述範例，請瀏覽 hello[訂用帳戶頁面](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)，選取您的訂閱，然後選擇**成本分析**。 從該處，您可以指定 hello 時間範圍，並查看 hello Azure 排程器服務的使用量付費。

![Azure 入口網站中的成本分析檢視](./media/billing-understand-your-bill/4.png)

toosee hello 每日成本明細中的**成本記錄**，按一下 hello 資料列。

![Azure 入口網站中的成本記錄檢視](./media/billing-understand-your-bill/5.png)

詳細資訊，請參閱 toolearn[避免非預期的成本，以及 Azure 帳單和成本管理](billing-getting-started.md#costs)。

## <a name="external"></a>外部服務費用呢？
外部服務 (也稱為 Azure Marketplace 訂單) 是由獨立服務廠商提供，並會分開計費。 hello 費用不會顯示在您的 Azure 發票上。 詳細資訊，請參閱 toolearn[了解 Azure 外部的服務費用](billing-understand-your-azure-marketplace-charges.md)。

## <a name="payment"></a>我要如何進行付款？

如果您設定信用卡或扣款卡為您的付款方式，負責 hello 計費期間結束後的 10 天內自動 hello 付款。 您的信用卡帳單上 hello 明細項目會說出**MSFT Azure**。

如果您[付費的發票開立](billing-how-to-pay-by-invoice.md)，傳送付款 toohello 您的位置列出在您的發票的 hello 底部。 如需詳細說明，請[連絡客戶支援](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)。

## <a name="how-do-i-check-hello-status-of-a-payment-made-by-credit-card"></a>如何檢查所做的信用卡付款 hello 狀態？

[建立支援票證](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)tooask hello 狀態是否為您的付款。 

## <a name="tips-for-cost-management"></a>成本管理的秘訣
- 使用 hello 估計成本[定價計算機](https://azure.microsoft.com/pricing/calculator/)和[總成本的擁有權 [小算盤]](https://aka.ms/azure-tco-calculator)，並取得 hello[詳細定價資訊的每個服務](https://azure.microsoft.com/en-us/pricing/)。
- [設定帳務警示](billing-set-up-alerts.md)。
- [檢閱您的使用量和定期在 hello Azure 入口網站中的成本](billing-getting-started.md#costs)。

## <a name="need-help-contact-support"></a>需要協助嗎？ 請連絡支援人員。

如果您仍需要協助，[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)tooget 快速解決您的問題。
