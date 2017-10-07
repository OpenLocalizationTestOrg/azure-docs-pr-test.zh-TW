---
title: "aaaPrevent 未預期的成本，管理帳單-Azure |Microsoft 文件"
description: "深入了解如何 tooavoid 未預期的費用，在 Azure 帳單上。 使用 Microsoft Azure 訂用帳戶的成本追蹤與管理功能。"
services: 
documentationcenter: 
author: tonguyen10
manager: tonguyen
editor: 
tags: billing
ms.assetid: 482191ac-147e-4eb6-9655-c40c13846672
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/10/2017
ms.author: tonguyen
ms.openlocfilehash: d380f27861531351ac8e570469c59a84b9ca99e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="prevent-unexpected-charges-with-azure-billing-and-cost-management"></a>使用 Azure 計費與成本管理避免非預期的費用

當您註冊 Azure 」 時，有幾件事，您可以 tooget 了解您的消費效能。 hello[定價計算機](https://azure.microsoft.com/pricing/calculator/)可以提供的成本估計值，才能建立 Azure 資源。 hello [Azure 入口網站](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)為您提供目前成本明細 hello 和趨勢預測您的訂用帳戶。 如果您想 toogroup，並了解不同的專案或小組的成本，查看[資源標記](../azure-resource-manager/resource-group-using-tags.md)。 如果您的組織有您喜歡 toouse 報告系統，請參閱 hello[計費 Api](billing-usage-rate-card-overview.md)。 

您也可以[下載過去的發票，並詳細說明使用檔](billing-download-azure-invoice-daily-usage-date.md)toomake 確定正確已向您收費。 如需比較每日使用量和發票的詳細資訊，請參閱[了解 Microsoft Azure 帳單](billing-understand-your-bill.md)。

如果您的訂閱是透過 Enterprise 合約 (EA)、 雲端方案提供者 (CSP) 或 Azure 發起者，這篇文章中的許多功能不適用 tooyou。 反之，我們有不同的工具組，可供您用於成本管理。 請參閱[適用於 EA、CSP 和贊助的其他資源](#other-offers)。

如果您的訂用帳戶是免費試用版、[Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)、Azure in Open (AIO) 或 BizSpark，當您用完所有的信用額度時，將會自動停用您的訂用帳戶。 深入了解[消費限制](#spending-limit)tooavoid 具有 unexpectantly 停用訂用帳戶。 

## <a name="get-estimated-costs-before-adding-azure-services"></a>在新增 Azure 服務之前取得估計的成本

### <a name="estimate-cost-online-using-hello-pricing-calculator"></a>估計成本線上使用 hello 定價計算機

簽出 hello[定價計算機](https://azure.microsoft.com/pricing/calculator/)tooget hello 服務您感興趣的估計每月成本。 您可以新增任何第一個合作對象 Azure 資源 tooget 估計成本。

![Hello 定價計算機功能表的螢幕擷取畫面](./media/billing-getting-started/pricing-calc.png)

例如，A1 Windows 虛擬機器 (VM) 會是估計的 toocost $66.96 美元/月中時數計算您讓它執行 hello 整個時間：

![顯示 A1 Windows VM 每個月的預估的 toocost $66.96 USD hello 定價計算機的螢幕擷取畫面](./media/billing-getting-started/pricing-calcVM.png)

如需價格的詳細資訊，請參閱此[常見問題集](https://azure.microsoft.com/pricing/faq/)。 或者，如果您想 tootalk tooan Azure 銷售人員，請連絡 1-800-867-1389。

### <a name="review-hello-estimated-cost-in-hello-azure-portal"></a>Hello Azure 入口網站中檢閱 hello 估計成本

通常當您新增服務 hello Azure 入口網站中，是檢視，顯示類似的估計的成本，每個月。 例如，當您選擇的 Windows VM 的 hello 大小，您看見 hello 預估每月成本 hello 運算時數：

![範例： A1 Windows VM 是每個月的預估的 toocost $66.96 美元](./media/billing-getting-started/vm-size-cost.PNG)

### <a name="set-up-billing-alerts"></a>設定帳務警示

設定計費警示 tooget 電子郵件時使用成本超過您指定的數量。 如果您有每月信用額度，請依照您設定指定金額時的額度設定警示。 如需詳細資訊，請參閱[為您的 Microsoft Azure 訂用帳戶設定帳單通知](billing-set-up-alerts.md)。

![帳務警示電子郵件的螢幕擷取畫面](./media/billing-getting-started/billing-alert.png)

> [!NOTE]
> 這項功能是仍處於預覽狀態，因此您應該定期檢查您的使用量。

您可以從 hello 定價計算機為您的第一個警示的指導方針 toouse hello 成本預估值。

### <a name="spending-limit"></a> 檢查您是否開啟消費限制

如果您有使用信用額度的訂閱，然後 hello 消費限制已為您預設。 如此一來，當您花光您的信用額度時，就不會針對您的信用卡收費。 請參閱 hello [Azure 優惠和 hello 可用性的消費限制的完整清單](https://azure.microsoft.com/support/legal/offer-details/)。

不過，如果您達到消費限制，就會停用您的服務。 這表示您的 VM 會被解除配置。 tooavoid 服務停機時間，您必須關閉 hello 消費限制。 任何超額部分都會用您在檔案上的信用卡收費。 

如果您已經有消費限制，toosee 移 toohello [hello 帳戶中心中檢視訂閱](https://account.windowsazure.com/Subscriptions)。 如果您的消費限制是開啟的，則會出現橫幅︰

![顯示有關消費限制上處於 hello 帳戶中心的警告的螢幕擷取畫面](./media/billing-getting-started/spending-limit-banner.PNG)

按一下 hello 橫幅，並遵循提示 tooremove hello 消費限制。 如果您註冊時，您未輸入信用卡資訊，您必須輸入 tooremove hello 消費限制。 如需詳細資訊，請參閱[Azure 消費限制 – 如何運作以及如何 tooenable 或將它移除](https://azure.microsoft.com/pricing/spending-limits/)。

## <a name="ways-toomonitor-your-costs-when-using-azure-services"></a>方式 toomonitor 您使用 Azure 服務時的成本

### <a name="tags"></a>新增標記 tooyour 資源 toogroup 帳單資料

支援服務，您可以使用標記 toogroup 計費資料。 例如，如果您執行數個 Vm 的不同小組，您可以使用標記 toocategorize 成本成本中心 (HR，行銷、 財務) 或環境 （生產環境中，進入生產階段前，測試）。 

![設定標記會顯示 hello 入口網站中的螢幕擷取畫面](./media/billing-getting-started/tags.PNG)

hello 標記會顯示在不同的報告檢視的成本。 例如，它們會立即顯示您的[成本分析檢視](#costs)，並在第一次計費期間之後，顯示[詳細使用量.csv](#invoice-and-usage)。

如需詳細資訊，請參閱[使用標記 tooorganize 您的 Azure 資源](../azure-resource-manager/resource-group-using-tags.md)。

### <a name="costs"></a>定期檢查的成本明細 hello 入口網站和完工速率

在您的服務開始執行之後，請定期檢查它們花了您多少錢。 您可以看到 hello 目前支出和完工速率 Azure 入口網站中。 

1. 請瀏覽 hello [Azure 入口網站中的訂用帳戶 刀鋒視窗](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)選取訂用帳戶。

2. 您應該看到 hello 成本分解和完工速率在 hello 快顯 刀鋒視窗。 它可能不支援您的優惠 （靠近 hello 頂端會顯示一則警告）。

    ![完工速率和分解 hello Azure 入口網站中的螢幕擷取畫面](./media/billing-getting-started/burn-rate.PNG)

3. 按一下**成本分析**hello 清單 toohello 左的 toosee hello 成本細目-依資源中。 等候 24 小時之後新增 hello 資料 toopopulate 的服務。

    ![在 Azure 入口網站中的 hello 成本分析檢視的螢幕擷取畫面](./media/billing-getting-started/cost-analysis.PNG)

4. 您可以依照不同屬性來篩選，例如[標記](#tags)資源群組和時間範圍。 按一下**套用**tooconfirm hello 篩選器和**下載**如果您想 tooexport hello 檢視 tooa 逗號分隔值 (.csv) 檔案。

5. 此外，您可以按一下資源 toosee 花歷程記錄和多少 hello 資源成本每一天。

    ![花在 Azure 入口網站中的歷程記錄檢視的 hello 螢幕擷取畫面](./media/billing-getting-started/costhistory.PNG)

我們建議您檢查 hello 您會看到您已看到，當您選取 hello 服務的 hello 預估的成本。 如果 hello 成本末來而多半極不同估計值，請再次檢查 hello 定價方案 (A1 vs A0 VM，例如) 您已選取為您的資源。 

### <a name="consider-enabling-cost-cutting-features-like-auto-shutdown-for-vms"></a>請考慮啟用成本削減功能，例如 VM 自動關機

根據您的案例中，您可以設定自動關機的 hello Azure 入口網站中的 Vm。 如需詳細資訊，請參閱[使用 Azure Resource Manager 的 VM 自動關機 (英文)](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/)。

![Hello 入口網站中的自動關閉選項的螢幕擷取畫面](./media/billing-getting-started/auto-shutdown.PNG)

自動關閉不 hello 與當您在關機時 hello VM 電源選項相同。 自動關閉會停止並取消配置 Vm toostop 額外的使用費用。 如需詳細資訊，請參閱 [Linux VM](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) 的定價常見問題，以及 [Windows VM](https://azure.microsoft.com/pricing/details/virtual-machines/windows/)有關 VM 的狀態。

如需更多針對開發和測試環境的成本削減功能，請參閱 [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab/)。

### <a name="turn-on-and-check-out-azure-advisor-recommendations"></a>開啟並查看 Azure 建議程式的建議

[Azure 建議程式](../advisor/advisor-overview.md)是一項預覽功能，可協助您藉由找出低使用率的資源，來降低成本。 在 hello Azure 入口網站中開啟：

![Azure 入口網站中 Azure 建議程式按鈕的螢幕擷取畫面](./media/billing-getting-started/advisor-button.PNG)

然後，您可以在 hello 取得可採取動作的建議**成本**hello Advisor 儀表板中的索引標籤：

![建議程式的成本建議範例的螢幕擷取畫面](./media/billing-getting-started/advisor-action.PNG)

如需詳細資訊，請參閱[建議程式成本建議](../advisor/advisor-cost-recommendations.md)。

### <a name="billing-api"></a>計費 API

使用我們計費 API tooprogrammatically get 使用量資料。 使用 hello RateCard API 和 hello 使用量 API 一起 tooget 您計費的使用量。 如需詳細資訊，請參閱[深入瞭解 Microsoft Azure 資源耗用量](billing-usage-rate-card-overview.md)。

## <a name="other-offers"></a> 其他資源和特殊案例

### <a name="ea-csp-and-sponsorship-customers"></a>EA、CSP 和贊助客戶
請連絡 tooyour 客戶經理或 Azure 合作夥伴 tooget 啟動。

| 提供項目 | 資源 |
|-------------------------------|-----------------------------------------------------------------------------------|
| Enterprise 合約 (EA) | [EA 入口網站](https://ea.azure.com/)、[協助文件](https://ea.azure.com/helpdocs)和 [Power BI 報告](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-enterprise/) |
| 雲端解決方案提供者 (CSP) | Talk tooyour 提供者 |
| Azure 贊助 | [贊助入口網站 (英文)](https://www.microsoftazuresponsorships.com/) |

如果您管理 IT 的大型組織，建議您閱讀[Azure 企業版 scaffold](../azure-resource-manager/resource-manager-subscription-governance.md)和 hello[企業 IT 技術白皮書](http://download.microsoft.com/download/F/F/F/FFF60E6C-DBA1-4214-BEFD-3130C340B138/Azure_Onboarding_Guide_for_IT_Organizations_EN_US.pdf)（.pdf 下載，僅限英文）。

### <a name="check-your-subscription-and-access"></a>檢查訂用帳戶和存取權

需要檢視成本[訂用帳戶層級存取 toobilling 資訊](billing-manage-access.md)，但是 hello 帳戶管理員可以存取 hello[帳戶中心](https://account.windowsazure.com/Home/Index)、 變更計費資訊，以及管理訂閱。 hello 帳戶管理員 hello 的人物是誰從頭到尾 hello 註冊程序。 如需詳細資訊，請參閱[hello 訂用帳戶或服務管理的新增或變更 Azure 系統管理員角色](billing-add-change-azure-subscription-administrator.md)。

toosee 如果您正在 hello 帳戶系統管理員，請移至 toohello [hello Azure 入口網站中的訂用帳戶 刀鋒視窗](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)並查看 hello 您具有存取權的訂用帳戶清單。 查看 [我的角色] 底下。 如果它顯示*帳戶管理員*，那麼您就是帳戶管理員。 如果它顯示諸如*擁有者*之類的其他角色，則表示您沒有完整權限。

![您的角色 hello hello Azure 入口網站中的訂閱檢視中的螢幕擷取畫面](./media/billing-getting-started/sub-blade-view.PNG)

如果您不是 hello 帳戶系統管理員，然後有人可能會讓您透過部分存取[Azure Active Directory 角色型存取控制](../active-directory/role-based-access-control-configure.md)(RBAC)。 toomanage 訂用帳戶和計費資訊，變更[尋找 hello 帳戶管理員](billing-subscription-transfer.md#whoisaa)並要求他們 tooperform hello 工作或[傳送嗨訂用帳戶 tooyou](billing-subscription-transfer.md)。

如果您的帳戶管理員已不再與您的組織，您需要 toomanage 計費[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)。 
## <a name="need-help-contact-support"></a>需要協助嗎？ 請連絡支援人員

如果您需要協助，[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)tooget 快速解決您的問題。
