---
title: "Azure 訂用帳戶的帳單或參與名單警示 aaaSet |Microsoft 文件"
description: "描述如何設定您的 Azure 帳單上的警示，以避免計費出現意外的狀況。"
keywords: "信用額度警示, 計費警示"
services: 
documentationcenter: 
author: vikdesai
manager: tonguyen
editor: 
tags: billing
ms.assetid: 9b7b3eeb-cd9d-4690-86a3-51b1e2a8974f
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: vikdesai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 711b9c72c59874792b0e229cdc5ec0fa517c24c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-billing-or-credit-alerts-for-your-microsoft-azure-subscriptions"></a>為您的 Microsoft Azure 訂用帳戶設定計費或信用額度警示
如果您是 Azure 訂用帳戶的 hello 帳戶管理員，您可以使用 hello Azure 計費警示服務 toocreate 自訂計費警示可協助您監視及管理您的 Azure 帳戶計費的活動。

這項服務處於預覽狀態，因此您需要 tooenable 它 hello 預覽功能 頁面中第一次。

## <a name="set-hello-alert-threshold-and-email-recipients"></a>設定 hello 警示閾值與電子郵件收件者
1. 請瀏覽[hello 預覽功能 頁面](https://account.windowsazure.com/PreviewFeatures)並啟用**計費警示服務**。

1. 在收到 hello hello 計費服務已開啟的電子郵件確認訂用帳戶之後，請瀏覽[hello 的訂閱 頁面](https://account.windowsazure.com/Subscriptions)hello 帳戶入口網站中。 按一下您想 toomonitor，然後再按一下 hello 訂閱**警示**。

    ![Hello 訂閱檢視的 Azure 帳戶中心的螢幕擷取畫面，反白顯示的警示][Image1]

2. 接下來，按一下**新增警示**toocreate 第一個。 您可以設定每個訂閱，有不同的閾值的五個計費警示總數和 tootwo 有關警示的電子郵件收件者。

    ![Hello 警示檢視，您可以在其中加入警示的螢幕擷取畫面][Image2]

3. 當您新增警示時，您會為它唯一的名稱、 選擇消費閾值，並選擇 hello 傳送警示的電子郵件地址。 設定時 hello 臨界值，則您可以任選**計費總計**或**貨幣信貸**從 hello**警示**清單。 計費總計，訂閱消費超出 hello 臨界值時，就會傳送一個警示。 貨幣信貸，貨幣信貸低於 hello 限制時，就會傳送一個警示。 貨幣信貸常 tooFree 試用版，Visual Studio 訂用帳戶。

    ![Hello [新增警示] 檢視中，您可以在其中設定收件者的螢幕擷取畫面][Image3]

Azure 支援任何電子郵件地址，但不會確認 hello 電子郵件地址可正常運作，因此請仔細檢查有沒有錯字。

## <a name="check-on-your-alerts"></a>檢查您的通知
您設定的警示之後，hello 帳戶中心會列出它們，並顯示有多少比較您可以設定。 每個警示，您會看到 hello 日期和時間送出，不論是計費總計 或 貨幣信貸，警示您設定的 hello 限制。 hello 日期和時間格式是 24 小時國際標準時間 (UTC)，並且 hello 日期 dd-mm yyyy 的格式。 Hello 加上簽章的 hello 清單 tooedit 中的警示，或按一下 hello 垃圾筒 toodelete 它。

## <a name="billing-alerts-for-enterprise-agreement-ea-customers"></a>Enterprise 合約 (EA) 客戶適用的計費警示
透過設定消費配額，EA 客戶可以取得註冊底下每個部門的警示。 請參閱[部門消費配額](https://ea.azure.com/helpdocs/departmentSpendingQuotas)hello EA 入口 tooget 啟動中。

## <a name="learn-more-about-azure-cost-management"></a>深入了解 Azure 成本管理
- 請使用 hello 預估成本[定價計算機](https://azure.microsoft.com/pricing/calculator/)，[總成本的擁有權 [小算盤]](https://aka.ms/azure-tco-calculator)，而且當您加入服務。
- [定期在 Azure 入口網站檢閱您的使用量和成本](billing-getting-started.md#costs)。
- 開啟 [Azure Advisor 成本建議](../advisor/advisor-cost-recommendations.md)。

詳細資訊，請參閱 toolearn [Azure 成本管理指南](billing-getting-started.md)。

[Image1]: ./media/azure-billing-set-up-alerts/billingalert1.png 
[Image2]: ./media/azure-billing-set-up-alerts/billingalert2.png
[Image3]: ./media/azure-billing-set-up-alerts/billingalerts3.png 
