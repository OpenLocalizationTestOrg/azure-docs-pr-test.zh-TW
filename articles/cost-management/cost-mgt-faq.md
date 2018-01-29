---
title: "Azure 成本管理的常見問題集 | Microsoft Docs"
description: "提供一些關於 Azure 成本管理常見問題的解答。"
services: cost-management
keywords: 
author: bandersmsft
ms.author: banders
ms.date: 12/14/2017
ms.topic: article
ms.service: cost-management
manager: carmonm
ms.custom: 
ms.openlocfilehash: f62e5a224c2fb33714a80bc47b98238208b787e5
ms.sourcegitcommit: 357afe80eae48e14dffdd51224c863c898303449
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/15/2017
---
# <a name="frequently-asked-questions-for-azure-cost-management"></a>Azure 成本管理的常見問題集

本文說明 Azure 成本管理 (也稱為 Cloudyn) 的一些常見問題。 如果您有關於「成本管理」的問題，可以在 [Cloudyn 的 Azure 成本管理常見問題集](https://social.msdn.microsoft.com/Forums/en-US/231bf072-2c71-4121-8339-ac9d868137b9/faqs-for-azure-cost-management-by-cloudyn?forum=Cloudyn) \(英文\) 詢問。

## <a name="how-can-i-resolve-common-indirect-enterprise-setup-problems"></a>如何解決常見的間接企業設定問題？

當您第一次使用 Cloudyn 入口網站時，如果您是 Enterprise 合約或雲端解決方案提供者 (CSP) 使用者，您可能會看到下列訊息：

- 在「設定 Azure 成本管理」精靈中顯示「指定的 API 金鑰不是最上層的註冊金鑰」。
- 在 Enterprise 合約入口網站中顯示「直接註冊 – 否」。
- 在 Cloudyn 入口網站中顯示：「找不到過去 30 天的使用方式資料。 請連絡您的散發者以確定您的 Azure 帳戶已啟用標記」。

前面的訊息指出您透過轉銷商或雲端解決方案提供者購買了 Azure Enterprise 合約。 您的轉銷商或雲端解決方案提供者必須為您的 Azure 帳戶啟用「標記」，您才能在 Cloudyn 中檢視資料。

以下是修正問題的方法：

1. 您的轉銷商必須為您的帳戶啟用「標記」。 如需指示，請參閱[間接客戶上線指南](https://ea.azure.com/api/v3Help/v2IndirectCustomerOnboardingGuide)。

2. 您要產生用於 Cloudyn 的 Azure Enterprise 合約金鑰。 如需指示，請參閱[新增您的 Azure EA](https://support.cloudyn.com/hc/en-us/articles/210429585-Adding-Your-AZURE-EA) 或[如何尋找您的 EA 註冊識別碼和 API 金鑰](https://youtu.be/u_phLs_udig)。

只有 Azure 服務系統管理員可以啟用「成本管理」。 共同管理員的權限不足。

在您可以產生 Azure Enterprise 合約 API 金鑰以設定 Cloudyn 之前，您必須啟用 Azure 帳單 API，方法是遵循下列文章中的指示：

- [適用於企業客戶的報告 API 概觀](../billing/billing-enterprise-api.md)
- **啟用對 API 的資料存取**下的 [Microsoft Azure 企業版入口網站報告 API](https://ea.azure.com/helpdocs/reportingAPI)


您可能也需要提供部門管理員、帳戶擁有者，以及企業管理員等權限，才能使用帳單 API「檢視費用」。

## <a name="why-dont-i-see-optimizer-recommendations"></a>為什麼無法查看最佳化工具建議？

建議的資訊只適用於所啟動的帳戶。 將不會看到任何建議資訊**最佳化工具**報告的帳戶類別*未*，包括：

- 最佳化管理員
- 調整大小最佳化
- 無效率

您無法檢視最佳化工具建議的任何資料，最有可能，您會有未的帳戶。 若要啟用帳戶，您需要向您的 Azure 認證。

若要啟用帳戶：

1.  在 Cloudyn 入口網站中，按一下右上角的 [設定] 並選取 [雲端帳戶]。
2.  在 Microsoft Azure 帳戶 索引標籤中，尋找具有帳戶**未**訂用帳戶。
3.  帳戶未右邊，按一下 **編輯**相似的鉛筆的符號。
4.  自動偵測您的租用戶識別碼和速率識別碼。 按 [下一步] 。
5.  您要重新導向至 Azure 入口網站。 登入入口網站，並授權以存取您的 Azure 資料 Cloudyn 收集器。
6.  接下來，您要重新導向至 [Cloudyn 帳戶管理] 頁面，而且您的訂用帳戶更新**active**帳戶狀態。 它會顯示一個綠色核取記號。
7.  如果您沒有看到綠色勾號符號的一個或多個訂用帳戶，這表示您沒有建立訂用帳戶的讀取器應用程式 (CloudynCollector) 的權限。 具有較高的權限，訂用帳戶的使用者需要重複步驟 3 和 4。  

完成上述步驟之後，您可以檢視最佳化工具建議一到兩天內。 不過，可能需要最多五天之前完全最佳化資料可供使用。


## <a name="how-do-i-enable-suspended-or-locked-out-users"></a>如何讓暫時停權或被鎖住的使用者恢復使用？

如果您收到要求允許使用者存取權的警示，則需要啟用使用者帳戶。

啟用使用者帳戶：

1. 使用您用來設定 Cloudyn 的 Azure 系統管理使用者帳戶，登入 Cloudyn。 或者，使用已被授與系統管理員存取權的使用者帳戶登入。

2. 選取右上角的齒輪符號，選取 [使用者管理]。

3. 尋找使用者，選取鉛筆符號，然後編輯使用者。

4. 在 [User status] \(使用者狀態\) 下，將狀態從 [Suspended] \(已暫時停權\) 變更為 [Active] \(作用中\)。

Cloudyn 使用者帳戶使用單一登入從 Azure 連線。 如果使用者輸入錯誤的密碼，可能會被鎖住而無法進入 Cloudyn，但可能還是可以存取 Azure。

如果您在 Cloudyn 中變更了電子郵件地址而與在 Azure 中的預設地址不同，您的帳戶會被鎖住。可能會顯示：「狀態 initiallySuspended」。 如果您的使用者帳戶被鎖住，請連絡其他系統管理員重設您的帳戶。

我們建議您至少建立兩個 Cloudyn 系統管理員帳戶，以免其中一個帳戶被鎖住。

如果您無法登入 Cloudyn 入口網站，請確定您使用正確的 Azure 成本管理 URL 登入 Cloudyn。 使用[https://azure.cloudyn.com](https://ms.portal.azure.com/#blade/Microsoft_Azure_CostManagement/CloudynMainBlade)。

請避免使用 Cloudyn 直接 URL https://app.cloudyn.com。

## <a name="how-do-i-activate-unactivated-accounts-with-azure-credentials"></a>如何使用 Azure 認證啟用尚未啟用的帳戶？

一旦 Cloudyn 探索到您的 Azure 帳戶，與成本相關的報表就會立即提供成本資料。 不過，要讓 Cloudyn 提供使用方式和效能資料，您還必須為帳戶註冊您的 Azure 認證。 如需指示，請參閱[新增 Azure Resource Manager](https://support.cloudyn.com/hc/en-us/articles/212784085-Adding-Azure-Resource-Manager)。

若要為帳戶新增 Azure 認證，請在 Cloudyn 入口網站中，選取帳戶名稱 (不是訂用帳戶) 右邊的編輯符號。

在您的 Azure 認證新增到 Cloudyn 之前，帳戶都會顯示為 _un-activated_ \(未啟用\)。

## <a name="how-do-i-add-multiple-accounts-and-entities-to-an-existing-subscription"></a>如何將多個帳戶和實體新增至現有的訂用帳戶？

其他實體可用來將其他的 Enterprise 合約新增到 Cloudyn 訂用帳戶。 下列連結說明如何新增其他實體：

- [新增實體](https://support.cloudyn.com/hc/en-us/articles/212016145-Adding-an-Entity) \(英文\) 文章
- [使用成本實體定義您的階層](https://support.cloudyn.com/hc/en-us/articles/115005142529-Video-Defining-your-hierarchy-with-Cost-Entities) \(英文\) 影片

如果是雲端解決方案提供者：

若要將其他雲端解決方案提供者帳戶新增至實體，當您建立新的實體時，請選取 [MSP Access] \(MSP 存取\)  而不是 [Enterprise]。 如果您的帳戶註冊為 Enterprise 合約，而且您想要新增雲端解決方案提供者認證，Cloudyn 支援人員可能需要修改您的帳戶設定。 如果您是付費的 Azure 訂閱者，可以在 Azure 入口網站中建立新的支援要求。 選取 [說明 + 支援]，然後選取 [新增支援要求]。

## <a name="currency-symbols-in-cloudyn-reports"></a>Cloudyn 報表中的貨幣符號

您可能會有多個使用不同貨幣的 Azure 帳戶。 不過，在 Cloudyn 成本報表中，每個報表不會顯示一個以上的貨幣類型。

如果您有使用不同貨幣的多個訂用帳戶，父實體和其子實體貨幣會以 **$** 符號顯示。 建議的最佳作法是避免在相同的實體階層中使用不同的貨幣。 換句話說，在實體結構中組織的所有訂用帳戶都應該使用相同的貨幣。

Cloudyn 會自動偵測您的 Enterprise 合約訂用帳戶貨幣，並在報表中正確顯示。  不過，Cloudyn 僅會針對 CSP 和 Web-direct Azure 帳戶顯示 **$** 符號。

## <a name="what-are-cloudyn-data-refresh-timelines"></a>什麼是 Cloudyn 資料重新整理時間軸？

Cloudyn 有下列資料重新整理時間軸：

- **初始**：設定之後，可能需要 24 小時的時間，才能在 Cloudyn 中檢視成本資料。 Cloudyn 也可能需要 10 天的時間，才能收集足夠的資料以顯示調整大小的建議。
- **每日**：從每個月 10 日到月底，Cloudyn 會在隔天大約 UTC+3 之後顯示前一天的資料。
- **每月**：從每個月 1 日到 10 日，Cloudyn 只會顯示到上個月底的資料。

當前一天有完整資料時，Cloudyn 就會處理前一天的資料。 在 Cloudyn 中，通常在每天大約 UTC+3 時可以獲得前一天的資料。 某些資料 (例如標記) 則可能需要額外的 24 小時處理。

每個月月初無法收集當月的資料。 在這段期間，服務提供者要完成上個月的帳單。 上個月的資料會在每個月開始後的 5 到 10 天出現在 Cloudyn 中。 在這段期間，您可能只會看到上個月的分攤成本。 您可能不會看到每日帳單或使用方式資料。 有資料可用時，Cloudyn 就會追溯處理。 處理後，每個月的 5 日到 10 日會顯示所有每個月的資料。

如果從 Azure 傳送資料到 Cloudyn 時發生延遲，資料仍會記錄在 Azure 中。 連線恢復時，資料就會傳送至 Cloudyn。

## <a name="how-can-a-direct-csp-configure-cloudyn-access-for-indirect-csp-customers-or-partners"></a>直接雲端解決方案提供者如何設定間接雲端解決方案提供者客戶或合作夥伴的 Cloudyn 存取？

如需指示，請參閱[設定 Cloudyn 中的間接 CSP 存取](quick-register-csp.md#configure-indirect-csp-access-in-cloudyn)。

## <a name="what-causes-the-optimizer-menu-item-to-appear"></a>造成最佳化工具功能表項目出現的原因為何？

在您新增 Azure Resource Manager 存取，且系統已收集資料之後，您應該會看見 [最佳化工具] 選項。 若要啟動 Azure Resource Manager 存取，請參閱[如何使用 Azure 認證啟用尚未啟用的帳戶？](#how-do-i-activate-unactivated-accounts-with-azure-credentials)

## <a name="is-cost-managementcloudyn-agent-based"></a>是否會使用成本管理/Cloudyn 代理程式？

編號 不會使用代理程式。 VM 的 Azure 虛擬機器計量資料，是從 Microsoft Insights API 收集而來。 如果您想要收集來自 Azure VM 的計量資料，便必須啟用它們的診斷設定。

## <a name="do-cloudyn-reports-show-more-than-one-ad-tenant-per-report"></a>每份 Cloudyn 報告是否能顯示超過一個 AD 租用戶的資料？

可以。 您可以針對您所擁有的每個 AD 租用戶[建立相對應的雲端帳戶實體](tutorial-user-access.md#create-entities)。 如此一來，您便可以檢視所有的 Azure AD 租用戶資料，以及其他雲端平台提供者 (包括 Amazon Web Services 和 Google Cloud Platform)。
