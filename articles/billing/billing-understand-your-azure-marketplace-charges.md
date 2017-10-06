---
title: "aaaUnderstand Azure 外部的服務費用 |Microsoft 文件"
description: "了解 Azure 中外部服務 (先前稱為 Marketplace) 費用的計費方式。"
services: 
documentationcenter: 
author: adpick
manager: tonguyen
editor: 
tags: billing
ms.assetid: 5e0e2a3c-d111-4054-8508-0c111c1b749b
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: adpick
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1d2cb28319e2ab4eff753177220993cbf94c96ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understand-your-azure-billing-for-external-service-charges"></a>了解外部服務費用的 Azure 計費方式
呼叫 Azure Marketplace toobe 使用外部的服務。 一般而言，它們是由第三方發佈且適用於 Azure，但已完全整合於 Azure 內的服務。 例如，ClearDB 和 SendGrid 是可在 Azure 中購買的外部服務，然而它們並非由 Microsoft 所發行。

當您佈建新的外部服務或資源時，系統會顯示警告︰

![Marketplace 購買警告](./media/billing-understand-your-azure-marketplace-charges/marketplace-warning.PNG)

> [!NOTE]
> 外部服務乃是由 Microsoft 之外的公司所發佈，不過 Microsoft 產品有時候也會分類為外部服務。
> 
> 

## <a name="how-external-services-are-billed"></a>如何對外部服務計費
- 外部服務會分開計費。 系統會將這類服務視為 Azure 訂用帳戶內的個別訂單。 您購買 hello 服務時，會設定為每個服務的 hello 計費週期。 不是 toobe hello hello 您購買它所在的訂用帳戶的計費期的問題感到困惑。 您還會收到獨立的帳單，而信用卡收費也會分開進行。
- 每項外部服務都有各自的計費模式。 有些服務採用隨用隨付的方式計費，有些則使用按月付款模式。 您需要使用信用卡來支付 Azure 外部服務的費用，不能以發票付款的方式來購買。
- 外部服務不適用於每個月的免費信用額度。 如果您使用 Azure 訂用帳戶包含[免費信用額度](https://azure.microsoft.com/pricing/spending-limits/)，它們不能套用的 tooexternal 服務帳單。 使用信用卡 toopurchase 外部服務。


## <a name="view-external-service-spending-and-history-in-hello-azure-portal"></a>檢視外部服務消費和 hello Azure 入口網站中的歷程記錄
您可以檢視一份 hello 外部服務的每個訂用帳戶內 hello [Azure 入口網站](https://portal.azure.com/): 

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)hello 帳戶系統管理員身分。
2. 在 hello 中樞功能表中，選取 **訂閱**。
   
    ![Hello 中樞功能表中選取訂用帳戶](./media/billing-understand-your-azure-marketplace-charges/sub-button.png) 
3. 在 hello**訂閱**刀鋒視窗中，選取 hello 訂閱您想 tooview，，然後選取**外部服務**。
   
    ![在 [hello 帳單] 刀鋒視窗中選取訂用帳戶](./media/billing-understand-your-azure-marketplace-charges/select-sub-external-services.png)
4. 您應該會看到每個外部服務訂單、 hello 發行者名稱、 您購買的服務層、 hello 資源和 hello 目前的訂單狀態為您提供名稱。 toosee 過去的帳單，選取 外部服務。
   
    ![選取外部服務](./media/billing-understand-your-azure-marketplace-charges/external-service-blade2.png)
5. 從這裡，您可以檢視過去的包括 hello 稅分解的帳單金額。
   
    ![檢視外部服務帳單記錄](./media/billing-understand-your-azure-marketplace-charges/billing-overview-blade.png)

## <a name="view-external-service-spending-for-enterprise-agreement-ea-customers"></a>檢視 Enterprise 合約 (EA) 客戶的外部服務消費
EA 客戶可以查看消費外部服務，並下載 hello EA 入口網站中的報表。 請參閱[Azure Marketplace 中的 EA 客戶](https://ea.azure.com/helpdocs/azureMarketplace)tooget 啟動。

## <a name="manage-payment-methods-for-external-service-orders"></a>管理外部服務訂單的付款方法
更新付款方式的外部服務訂單從 hello[帳戶中心](https://account.windowsazure.com/)。

> [!NOTE]
> 如果您購買訂用帳戶使用的公司或學校帳戶，[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)toomake 變更 tooyour 付款方法。
> 
> 

1. 登入 toohello[帳戶中心](https://account.windowsazure.com/)和[瀏覽 toohello **marketplace**  索引標籤](https://account.windowsazure.com/Store)
   
    ![Hello 帳戶中心] 中選取 [marketplace](./media/billing-understand-your-azure-marketplace-charges/select-marketplace.png)
2. 選取您想要 toomanage hello 外部服務
   
    ![選取您想要 toomanage hello 外部服務](./media/billing-understand-your-azure-marketplace-charges/select-ext-service.png)
3. 按一下**變更付款方式**右邊 hello hello 頁面。 此連結會帶您 tooa 不同入口 toomanage 付款方法。
   
    ![訂單摘要](./media/billing-understand-your-azure-marketplace-charges/change-payment.PNG)
4. 按一下**編輯資訊**並遵循指示 tooupdate 付款資訊。
   
    ![選取編輯資訊](./media/billing-understand-your-azure-marketplace-charges/edit-info.png)

## <a name="cancel-an-external-service-order"></a>取消外部服務訂單
如果您想 toocancel 外部服務順序，刪除在 hello hello 資源[Azure 入口網站](https://portal.azure.com)。

![刪除資源](./media/billing-understand-your-azure-marketplace-charges/deleteMarketplaceOrder.PNG)

## <a name="need-help-contact-support"></a>需要協助嗎？ 請連絡支援人員。
如果您仍有問題，[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)tooget 快速解決您的問題。

