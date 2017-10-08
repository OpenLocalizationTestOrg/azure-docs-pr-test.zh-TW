---
title: "aaaDownload Azure 計費發票及每日使用量資料 |Microsoft 文件"
description: "描述如何 toodownload 或檢視您的 Azure 帳單寄送發票和每日使用量資料。"
keywords: "帳單發票,發票下載,azure 發票,azure 使用量"
services: 
documentationcenter: 
author: genlin
manager: tonguyen
editor: 
tags: billing
ms.assetid: 6d568d1d-3bd6-4348-97d0-1098b5fe0661
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: genli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2826df10f39914fcaeb9985271dadde550c68dfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="download-or-view-your-azure-billing-invoice-and-daily-usage-data"></a>下載或檢視您的 Azure 帳單發票和每日使用量資料
您可以從 hello 下載發票[Azure 入口網站](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)或讓它在電子郵件中傳送。 toodownload 您每日使用量、 移 toohello [Azure 帳戶中心](https://account.windowsazure.com)。 只有特定角色有權限 tooget 計費發票與使用量的資訊，例如 hello 帳戶系統管理員。 toolearn 進一步了解取得存取 toobilling 資訊，請參閱[計費使用角色的管理存取 tooAzure](billing-manage-access.md)。

## <a name="get-your-invoice-in-email-pdf"></a>透過電子郵件取得發票 (.pdf)
您可以參加，並設定您的 Azure 發票的其他收件者 tooreceive 以電子郵件。 這項功能可能無法用於支援優惠、Enterprise 合約或 Azure in Open 等特定訂用帳戶。

1. 選取您的訂閱 hello 從[訂用帳戶 刀鋒視窗](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)。 針對您擁有的每個訂用帳戶選擇加入。 依序按一下 [發票] 和 [以電子郵件寄送我的發票]。 

    ![顯示 hello 中，選擇流程的螢幕擷取畫面](./media/billing-download-azure-invoice-daily-usage-date/InvoicesDeepLink.PNG)
    
2. 按一下**參加**並接受 hello 條款。

    ![顯示 hello 中，選擇流程的螢幕擷取畫面](./media/billing-download-azure-invoice-daily-usage-date/InvoiceArticleStep2.PNG)
 
3. 一旦您已接受 hello 協議，您可以設定其他收件者。

    ![顯示 hello 中，選擇流程的螢幕擷取畫面](./media/billing-download-azure-invoice-daily-usage-date/InvoiceArticleStep3.PNG)
    
如果沒有得到一封電子郵件遵循 hello 步驟後，請確定您的電子郵件地址是正確的 hello[通訊喜好設定，在您的設定檔上](https://account.windowsazure.com/profile)。

## <a name="download-invoice-from-azure-portal-pdf"></a>從 Azure 入口網站下載發票 (.pdf)

1. 選取您的訂閱 hello 從[訂用帳戶 刀鋒視窗](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)做為 Azure 入口網站中[使用者具有存取 tooinvoices](billing-manage-access.md)。

2. 選取 [發票]。 

    ![顯示 hello 帳單及使用量選項的螢幕擷取畫面](./media/billing-download-azure-invoice-daily-usage-date/billingandusage.png) 

3. 按一下**下載發票**tooview PDF 發票的複本。 如果，該處會指示**無法使用**，請參閱[為什麼無法查看 hello 最後一個計費週期的發票？](#noinvoice)

    ![每一個計費週期的示範計費期，hello 下載選項，與總費用的螢幕擷取畫面](./media/billing-download-azure-invoice-daily-usage-date/billing4.png)

4. 您也可以按一下 hello 計費期間內，以檢視您每日使用量。 

如需發票的詳細資訊，請參閱[了解 Microsoft Azure 帳單](billing-understand-your-bill.md)。 如需管理成本上的協助，請參閱[使用 Azure 計費與成本管理避免非預期的成本](billing-getting-started.md)。

## <a name="download-usage-from-hello-account-center-csv"></a>下載從 hello 帳戶中心 (.csv) 的使用方式

1. 登入 hello [Azure 帳戶中心](https://account.windowsazure.com/subscriptions)為 hello 帳戶系統管理員。

2. 選取您想要的 hello 發票與使用量資訊的 hello 訂用帳戶。

3. 選取 [帳單記錄]。 

    ![顯示帳單記錄選項的螢幕擷取畫面](./media/billing-download-azure-invoice-daily-usage-date/Billinghisotry.png)

4. 您可以看到您的陳述式 hello 最後六次計費期和 hello 目前週期欠繳。 

    ![每一個計費週期的示範計費期、 選項 toodownload 發票及每日使用量以及總費用的螢幕擷取畫面](./media/billing-download-azure-invoice-daily-usage-date/billingSum.png)

5. 選取**檢視目前的陳述式**toosee 產生估計您在 hello hello 估計時間的費用。 此資訊每天只會更新一次，可能不會包含您的所有使用量。 您的每月發票可能會與這項估計有所不同。

    ![顯示 hello 檢視目前的陳述式選項的螢幕擷取畫面](./media/billing-download-azure-invoice-daily-usage-date/billingSum2.png)

    ![顯示目前的費用 hello 估計的螢幕擷取畫面](./media/billing-download-azure-invoice-daily-usage-date/billingSum3.png)

6. 選取**下載使用量**toodownload hello 每日使用量資料 CSV 檔案。 如果您看到兩個可用版本，請下載第 2 個版本。

    ![顯示 hello 下載使用方式選項的螢幕擷取畫面](./media/billing-download-azure-invoice-daily-usage-date/DLusage.png)

Hello 帳戶系統管理員可以存取 hello Azure 帳戶中心。 擁有者，例如其他計費系統管理員可以取得使用量資訊使用 hello[計費 Api](billing-usage-rate-card-overview.md)。

如需每日使用量的詳細資訊，請參閱[了解 Microsoft Azure 帳單](billing-understand-your-bill.md)。 如需管理成本上的協助，請參閱[使用 Azure 計費與成本管理避免非預期的成本](billing-getting-started.md)。

## <a name="noinvoice"></a>為什麼無法查看 hello 最後一個計費週期的發票？

您沒有看到發票的可能原因如下︰

- 您的訂用帳戶有尚未超過的每月信用額度，或您有免費試用版。 只有在您積欠費用時，才會產生發票。

- 它是從訂閱 tooAzure hello 天少於 30 天。

- 不產生 hello 發票。 等候直到在 hello hello 計費期間結束。

- 如果您不 hello 帳戶系統管理員，較舊的發票可能無法 avaialbe tooyou。

## <a name="need-help-contact-support"></a>需要協助嗎？ 請連絡支援人員。
如果您仍有進一步的問題，[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)tooget 快速解決您的問題。

