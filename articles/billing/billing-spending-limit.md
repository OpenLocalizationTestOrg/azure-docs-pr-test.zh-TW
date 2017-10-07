---
title: "aaaUnderstand Azure 消費限制 |Microsoft 文件"
description: "描述 Azure 消費限制的運作方式以及 tooremove 它"
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: genli
ms.openlocfilehash: ed01401a07c3d0e7edebe42fb1482b7b60b1df51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-spending-limit-and-how-tooremove-it"></a>了解 Azure 消費限制以及如何 tooremove 它

Azure 消費限制是對您 Azure 訂用帳戶消費額度的限制。 所有新的客戶註冊 hello 試用供應項目或包含多個月內的信用額度的優惠擁有 hello 消費限制預設為開啟。 hello 消費限制為 $0。 此限制無法變更。 hello 消費限制不適用於訂閱類型，例如隨用隨付訂用帳戶以及承諾計畫。 請參閱 hello [Azure 提供的消費限制的 hello hello 可用性的完整清單](https://azure.microsoft.com/support/legal/offer-details/)。

## <a name="what-happens-when-i-reach-hello-spending-limit"></a>當我達到消費限制的 hello 發生什麼事？

當您的使用方式導致耗盡 hello 每月量納入您的優惠的費用時，您部署的 hello 服務會停用該帳務月份 hello 其餘部分。 舉例來說，您部署的「雲端服務」會從生產環境中移除，而 Azure 虛擬機器則會停止並解除配置。 tooprevent 無法停用您的服務，您可以選擇 tooremove 消費限制。 您的服務停用時，您的儲存體帳戶和資料庫中的 hello 資料的使用。 系統管理員以唯讀方式 在 hello 開頭 hello 下一個計費月份，如果您的優惠包含透過數個月信用額度訂用帳戶將會重新啟用。 您可以重新部署您的雲端服務，並且具有完整存取 tooyour 儲存體帳戶和資料庫。

Hello 免費的試用訂用帳戶達到消費限制的 hello 之後，您可以重新啟用 hello 訂用帳戶，並讓它自動[升級 tooour 標準隨用隨付優惠](billing-upgrade-azure-subscription.md)後 90 天內。

當您遇到 hello 消費限制為您提供的服務時，您會收到通知。 登入 toohello [Azure 帳戶中心](https://account.windowsazure.com)，選取**帳戶**，然後選取**訂閱**。 您會看到有關訂用帳戶已達到消費限制的 hello 的通知。

## <a name="things-you-are-charged-for-even-if-you-have-a-spending-limit-enabled"></a>即使已啟用消費限制也需要付費的項目

某些 Azure 服務和[Marketplace 購買](https://azure.microsoft.com/marketplace/)可以產生 hello 付款方式 (CC) 下的費用，即使已設定的消費限制。 範例包括 Visual studio 授權、 Azure Active Directory premium、 支援計劃和大部分第三方品牌銷售透過 hello Marketplace 的服務。


## <a name="when-not-toouse-hello-spending-limit"></a>當不 toouse hello 消費限制

hello 消費限制，無法讓您無法部署或使用特定的服務商場和 Microsoft 服務。 以下是您應該在此移除消費限制，您的訂用帳戶的 hello hello 案例。

- 您計劃 toodeploy 前的合作對象影像像 Oracle 和 Visual Studio Team Services 等服務。 此案例會導致您 tooexceed 幾乎會立即您的消費限制，並會導致您的訂用帳戶 toobe 停用。

- 您有不可中斷的服務。

- 您有服務和資源的設定，例如虛擬 IP 位址，您不想 toolose。 當取消配置 hello 服務和資源，這些設定會遺失。


## <a name="remove-hello-spending-limit"></a>移除消費限制的 hello

您可以移除消費限制在任何時候，只要沒有有效的付款方式，與您訂用帳戶相關聯的 hello。 如有多個月內的信用額度的優惠，您也可以重新啟用 hello 消費限制，在您的下一個計費週期 hello 開頭。

tooremove 您的消費限制，請遵循下列步驟：

1. 登入 toohello [Azure 帳戶中心](https://account.windowsazure.com)。

2. 選取一個訂用帳戶。

3. 如果 hello 訂用帳戶已停用到期 toohello 正在達到消費限制，請按一下此通知: 「 訂用帳戶達到消費限制 hello 和已停用的 tooprevent 費用 」。 否則，請按一下**移除消費限制**在 hello**訂用帳戶狀態**區域。

4. 選取適合您的選項。

|選項|效果|
|-------|-----|
|無限期移除消費限制|移除 hello 時自動開啟在 hello hello 開始下一個計費週期沒有消費限制。|
|移除目前計費週期 hello 的消費限制|移除消費限制，使它傳回時自動開啟在 hello hello 開始下一個計費週期的 hello。|

## <a name="need-help-contact-support"></a>需要協助嗎？ 請連絡支援人員。
如果您仍需要協助，[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)tooget 快速解決您的問題。
