---
title: "aaaReport Azure 堆疊使用方式資料 tooAzure |Microsoft 文件"
description: "深入了解如何 tooset Azure 堆疊中的報告的使用量資料。"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun;AlfredoPizzirani
ms.openlocfilehash: deecd66d9022b2e0c274ff4e0276d3b2e3bcc99e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="report-azure-stack-usage-data-tooazure"></a>報告 Azure 堆疊使用方式資料 tooAzure 

使用量資料，也稱為如耗用量資料代表 hello 所使用的資源數量。 Azure 堆疊中使用量資料必須回報 tooAzure 計費用途。 Azure 堆疊雲端系統管理員應該設定其 Azure 堆疊執行個體 tooreport 使用量資料 tooAzure。

> [!NOTE]
> 使用量資料報告不需要 hello Azure 堆疊開發套件，而使用者不計費耗用的資源。 不過，Azure Stack 雲端系統管理員可以測試此功能並提供意見反應。 通常可以使用 Azure 堆疊多節點時，所有的 hello multi-node 環境必須報告使用量資料 tooAzure。

![計費流程](media/azure-stack-usage-reporting/billing-flow.png)

使用量資料是從 Azure 堆疊 tooAzure hello Azure 橋接器透過傳送。 在 Azure 中，hello 商務系統處理序 hello 使用量資料，並產生 hello 帳單。 Hello Azure 訂用帳戶擁有者 hello bill 產生之後，可以檢視，並從 hello 下載[Azure 帳戶中心](https://account.windowsazure.com/Subscriptions)。 關於如何授權 Azure 堆疊 toolearn 參考 toohello [Azure 堆疊封裝和定價文件](https://go.microsoft.com/fwlink/?LinkId=842847&clcid=0x409)。

## <a name="set-up-usage-data-reporting"></a>設定使用情況資料報告

tooset Azure 堆疊中的報告的使用量資料，您必須[註冊您的 Azure 堆疊執行個體，Azure](azure-stack-register.md)。 Hello 註冊程序的一部分，Azure 堆疊會以 hello Azure 橋接器，可連接 Azure 堆疊 tooAzure 並傳送嗨使用量資料設定。 從 Azure 堆疊 tooAzure 傳送 hello 下列使用量資料：

* **測量識別碼**– 所耗用的 hello 資源的唯一識別碼。
* **數量**：在特定時間範圍內發生的資源使用情況資料數量。
* **位置**– hello 目前 Azure 堆疊資源部署所在的位置。
* **資源 URI** – 完整的報告使用量 hello 資源的 URI。 
* **訂用帳戶 ID** – hello Azure 堆疊使用者訂用帳戶識別碼。
* **時間**– hello 使用量資料的開始和結束時間。 Hello Azure 堆疊中，以及報告的 toocommerce hello 使用量資料時，當使用這些資源的時間會有些延遲。 Azure 堆疊彙總每 24 小時的使用量資料，並報告使用量資料 toocommerce 管線，在 Azure 中的執行另一個幾個小時。 午夜之後一天的 Azure hello 中可能顯示的不久之前，就會發生，請使用方式。

## <a name="test-usage-data-reporting"></a>測試使用情況資料回報 

1. tootest 使用量資料報告，Azure 堆疊中建立幾個資源。 例如，您可以建立[儲存體帳戶](azure-stack-provision-storage-account.md)， [Windows Server VM](azure-stack-provision-vm.md)和 Linux VM 的基本和標準 Sku toosee 核心使用量報告的方式。 hello 不同類型的資源使用量資料會被報告不同的計量器。  

2. 讓您的資源執行幾小時。 系統大約每隔一小時會收集一次使用情況資訊。 在收集後，此傳輸的 tooAzure 及資料處理至 Azure 的商務系統 hello。 此程序可能佔用 tooa 幾個小時。  

3. 登入 toohello [Azure 帳戶中心](https://account.windowsazure.com/Subscriptions)為 hello Azure 帳戶系統管理員並選取 hello Azure 訂用帳戶，您會使用 tooregister hello Azure 堆疊。 您可以檢視 hello Azure 堆疊使用方式資料，請使用資源 hello 量支付每 hello hello 下列影像所示：  
   ![計費流程](media/azure-stack-usage-reporting/pricng-details.png)

Hello Azure 堆疊開發套件，以便顯示 hello 價格為 $0.00，不會向 Azure 堆疊資源。 通常可以使用 Azure 堆疊多節點時，您可以看到 hello 實際成本的每個資源。 

## <a name="which-azure-stack-instances-are-charged"></a>哪個 Azure Stack 執行個體被收費？
針對 Azure Stack 開發套件執行個體，資源的使用是免費的。 

公開上市，而 hello 開發套件環境仍可使用不花一毛錢向 Azure 堆疊多節點的系統。 針對多節點系統，工作負載 VM、儲存體服務與應用程式服務需收費。 

## <a name="are-users-charged-for-hello-infrastructure-vms"></a>使用者會針對 hello 基礎結構 Vm 的收費？
否，Azure 堆疊基礎結構在部署期間建立的 Vm 的 hello 使用量資料會報告的 tooAzure，但不有任何這些 Vm 的費用。 hello 基礎結構 Vm 包括 hello Vm 所建立的 hello Azure 堆疊部署指令碼，和 hello 例如執行 Microsoft 第一方資源提供者的運算、 儲存體、 SQL。

## <a name="what-azure-meters-are-used-when-reporting-usage-data"></a>回報使用情況資料時會使用哪些 Azure 計量？
hello 下面是用於使用量資料報告的計量器 hello 兩組：  

* **完整價格計量**：用於與使用者工作負載關聯的資源。  
* **系統管理計量**：用於基礎結構資源。 這些計量的價格為零。

## <a name="which-subscription-is-charged-for-hello-resources-consumed"></a>哪一個訂用帳戶則需支付所使用的 hello 資源？
hello 時提供的訂用帳戶[向 Azure 註冊 Azure 堆疊](azure-stack-register.md)會產生費用。

## <a name="what-types-of-subscriptions-are-supported-for-usage-data-reporting"></a>哪些類型的訂用帳戶支援使用情況資料回報？
Hello Azure 堆疊開發套件，Enterprise 合約 (EA)、 隨用隨付和 MSDN 訂用帳戶支援報告的使用量資料。 

## <a name="does-usage-data-reporting-work-in-sovereign-clouds"></a>使用情況資料回報在主權雲端中是否能運作？
在 hello Azure 堆疊開發套件，使用量資料報告需要 hello 全域 Azure 系統中建立的訂閱。 其中一個 hello 統領雲端 （hello Azure 政府、 Azure 德國和 Azure China 雲端） 中建立的訂閱無法向 Azure 中，因此它們不支援使用方式資料報表。 

## <a name="can-an-administrator-test-usage-data-reporting-before-ga"></a>在全面推出之前，系統管理員是否可以測試使用情況資料回報？
是，Azure 堆疊系統管理員可以測試 hello 使用量資料報告[註冊](azure-stack-register.md)hello 開發套件的執行個體與 Azure。 在註冊之後，使用量資料會開始從您的 Azure 堆疊執行個體 tooyour Azure 訂用帳戶。 

## <a name="how-can-users-identify-azure-stack-usage-data-in-hello-azure-billing-portal"></a>使用者如何識別 hello Azure 計費入口網站中的 Azure 堆疊使用方式資料？
使用者可以看到 hello 使用量詳細資料檔案中的 hello Azure 堆疊使用方式資料。 tooknow 關於如何 tooget hello 使用量詳細資料檔案，請參閱 toohello[從 hello Azure 帳戶中心下載使用量檔案](../billing/billing-download-azure-invoice-daily-usage-date.md#download-usage-from-the-account-center-csv)發行項。 hello 使用量詳細資料檔案包含識別堆疊 Azure 儲存體和 Vm 的 hello Azure 堆疊公尺。 使用 Azure 堆疊中的所有資源，會被都報告 hello 區域名為 「 Azure 堆疊 」。

## <a name="why-doesnt-hello-usage-reported-in-azure-stack-match-hello-report-generated-from-azure-account-center"></a>為什麼不 hello 在報告使用量 Azure 堆疊比對從 Azure 帳戶中心產生 hello 報表？
Hello 使用量資料產生與 Azure 堆疊中時提交的 tooAzure 商務時沒有延遲時間。 hello 延遲是從 Azure 堆疊 tooAzure 商務 hello 所需時間 tooupload 使用量資料。 Toothis 延遲，因為午夜不久之前所發生的使用方式可能會出現在 Azure 的 hello 遵循一天。 如果您使用 hello [Azure 堆疊使用量 Api](azure-stack-provider-resource-api.md)，並比較 hello 結果中的報告 toohello 使用量 hello Azure 計費入口網站，您可以看到差異。

## <a name="next-steps"></a>後續步驟

* [提供者使用量 API](azure-stack-provider-resource-api.md)  
* [租用戶使用量 API](azure-stack-tenant-resource-usage-api.md)
* [使用狀況常見問題集](azure-stack-usage-related-faq.md)