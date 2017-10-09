---
title: "ClearDB MySql 資料庫，使用 Azure App Service 的 aaaFAQ |Microsoft 文件"
description: "回答有關使用 Azure App Service 中使用 ClearDB MySQL 資料庫的 toocommon 問題。"
documentationcenter: php
services: 
author: sunbuild
manager: yochayk
editor: 
tags: mysql
ms.assetid: c2ed5e78-6d7d-4d0c-b7ee-a52ae41ceab8
ms.service: multiple
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/27/2016
ms.author: sumuth
ms.openlocfilehash: 3d9c9daca2b845ede8d3a1fdadefa7e668d62dee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="faq-for-cleardb-mysql-databases-with-azure-app-service"></a>ClearDB MySQL 資料庫搭配 Azure App Service 的常見問題集
此常見問題集可回答為 Azure Web Apps 使用及購買 ClearDB MySQL 資料庫的常見問題。

## <a name="what-options-do-i-have-for-mysql-on-azure"></a>在 Azure 上的 MySQL 有哪些選項？
您有幾種選項：

* [ClearDB Shared MySQL 資料庫](/marketplace/partners/cleardb/databases/)
* [ClearDB MySQL Premium 叢集](/marketplace/partners/cleardb-clusters/cluster/)
* [Azure VM 上執行的 MySQL 叢集](https://github.com/azure/azure-quickstart-templates/tree/master/mysql-replication)
* [Azure VM 上執行的 MySQL 單一執行個體](virtual-machines/windows/classic/mysql-2008r2.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

ClearDB MySQL 代管服務並會為您管理 hello MySQL 基礎結構。 當您執行您自己的 MySQL 叢集或資料庫在 Azure 虛擬機器上時，您會擁有 tooset hello MySQL server，並且讓它保持修補檔案更新。

## <a name="do-i-need-a-credit-card-for-hello-web-app--mysql-template-in-hello-azure-marketplace"></a>是否需要使用信用卡 hello Web 應用程式 + hello Azure Marketplace 中的 MySQL 範本？
這取決於您使用的訂閱 hello 類型。 以下是一些常用的訂用帳戶類型：

* [預付型](/offers/ms-azr-0003p/)：需要信用卡，購買付費的 MySQL 資料庫時，將向您的信用卡收費。
* [免費試用](https://azure.microsoft.com/pricing/free-trial/)：包括可用於 Microsoft Azure 服務的信用額度，但不允許購買第三方資源。 訂用帳戶啟用 toopurchase 第三方服務或付費的 MySQL 資料庫，您需要 toouse 信用卡。 針對 Web Apps，您可以建立免費的 ClearDB MySQL 資料庫。
* [MSDN 訂用帳戶](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/)和**MSDN 開發測試付**： 類似 tooFree 試用、 MSDN 訂用帳戶會要求您 toohave 信用卡 toopurchase 付費從 ClearDB MySQL 解決方案。
* [Enterprise 合約 (EA)](https://azure.microsoft.com/pricing/enterprise-agreement/)：我們會每季以單一彙總的發票就 EA 向 EA 客戶的所有 Azure Marketplace (第三方) 購買項目收費。 您需要付費以外的任何 marketplace 購買 hello 綁約。 請注意，此時，Azure 市集無法使用 toocustomers 亞塞拜然、 克羅埃西亞、 挪威和波多黎各中註冊。 
* [DreamSpark](https://www.dreamspark.com/Product/Product.aspx?productid=99)：您只能為 Web Apps 建立免費的 ClearDB 資料庫。 可用的 ClearDB MySQL 資料庫，您可以建立的 hello 數目沒有限制。 請注意，免費的資料庫並未 toobe 用於生產環境 web 應用程式，因為這項服務僅供試用版。

## <a name="why-was-i-charged-350-for-a-web-app--mysql-from-hello-azure-marketplace"></a>為什麼扣款 $3.50 Web 應用程式 + MySQL 從 hello Azure Marketplace？
hello 預設資料庫選項坦，也就是 $3.50。 我們不要顯示 hello 成本資料庫建立期間，您可能不小心購買您不想要的資料庫。 我們正在嘗試 toofind 方式 tooimprove hello 經驗，但是在那之前您必須檢查所有您選取的定價層 web 應用程式和資料庫後，再按一下**建立**和啟動 hello 部署的 hello 資源。

## <a name="i-am-running-mysql-on-my-own-azure-virtual-machine-can-i-connect-my-azure-web-app-toomy-database"></a>我在自己的 Azure 虛擬機器上執行 MySQL。 可以連線我 Azure web 應用程式的 toomy 資料庫嗎？
是。 您可以連接您的 web 應用程式 tooyour 資料庫，只要您的 Azure VM 已授與遠端存取 tooyour web 應用程式。 如需詳細資訊，請參閱 [在虛擬機器上安裝 MySQL](virtual-machines/windows/classic/mysql-2008r2.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。

## <a name="in-which-countries-are-cleardb-premium-mysql-clusters-supported"></a>支援 ClearDB Premium MySQL 叢集的國家 (地區)有哪些？
[ClearDB Premium MySQL 叢集](/marketplace/partners/cleardb-clusters/cluster/)hello 例外狀況的印度、 澳洲、 巴西南部和中國全球所有 Azure 地區中可用。

## <a name="can-i-create-a-new-cluster-prior-toocreating-a-database-with-cleardb-premium-cluster-solution"></a>建立新的叢集之前 toocreating 資料庫的 ClearDB premium 叢集解決方案？
否，不支援建立空白的 ClearDB 叢集。 hello Azure 入口網站可讓您 toocreate 資料庫可能會建立新的叢集在 hello 叢集中相同的時間。

## <a name="will-i-be-warned-if-i-try-toodelete-a-cleardb-mysql-database-that-is-in-use-by-one-of-my-applications"></a>將我會收到警告如果我嘗試 toodelete ClearDB MySQL 資料庫使用中的 我的應用程式嗎？
否，如果您刪除應用程式所相依的 Marketplace 購買項目，Azure 將不會警告您。

## <a name="which-regions-can-i-create-cleardb-databases-in"></a>可以在哪些區域中建立 ClearDB 資料庫？
Azure Marketplace 目前無法使用 toocustomers 亞塞拜然、 克羅埃西亞、 挪威或波多黎各中註冊。 這些區域中無法使用 ClearDB。

## <a name="what-pricing-tier-should-i-choose-for-a-production-web-app-and-database"></a>針對生產 Web 應用程式和資料庫，應該選擇哪個定價層？
對 Web Apps 使用「基本」或更高的定價層。 針對 ClearDB，我們建議 Saturn 或 Jupiter 計劃。 檢閱 hello 功能和限制每個定價層的兩個[Web 應用程式](https://azure.microsoft.com/pricing/details/app-service/)和[ClearDB MySQL 資料庫](/marketplace/partners/cleardb/databases/)toochoose hello 符合您需求的其中一個。

## <a name="how-do-i-upgrade-my-cleardb-database-from-one-plan-tooanother"></a>如何升級我的 ClearDB 資料庫從一個計劃 tooanother 中？
在 hello [Azure 入口網站](https://portal.azure.com)，您就能相應 ClearDB 共用主控資料庫。 請閱讀本[文章](https://blogs.msdn.microsoft.com/appserviceteam/2016/10/06/upgrade-your-cleardb-mysql-database-in-azure-portal/)toolearn 更多。 我們目前不支援升級 ClearDB Premium hello Azure 入口網站中的叢集。

## <a name="i-cant-see-my-cleardb-database-in-azure-portal"></a>我在 Azure 入口網站中看不到我的 ClearDB 資料庫？
如果我們建立使用 Azure 資源管理員的 ClearDB 資料庫或[新版 Azure 入口網站](https://portal.azure.com)，將不會顯示在 hello[舊的 Azure 入口網站](https://manage.windowsazure.com)。 toowork-解決這個問題是 toolink 您的資料庫手動 toohello web 應用程式。 同樣地如果 hello 中建立的 ClearDB 資料庫[舊的入口網站](https://manage.windowsazure.com)您不會是能 toosee hello 中的資料庫[新版 Azure 入口網站](https://portal.azure.com)。 沒有任何解決 hello 後面的案例。

## <a name="who-do-i-contact-for-support-when-my-database-is-down"></a>我的資料庫關閉時應向誰連絡尋求支援？
如有任何資料庫相關的問題，請連絡 [ClearDB 支援](https://www.cleardb.com/developers/help/support) 。 準備 tooprovide 其與您的 Azure 訂用帳戶資訊。

## <a name="can-i-create-additional-users-for-my-cleardb-mysql-database-cluster-solution"></a>我可以為自己的 ClearDB MySQL 資料庫叢集解決方案建立其他的使用者嗎？
不行。 您無法建立其他的使用者，但可以在自己的 ClearDB 資料庫叢集上建立其他的資料庫。  

## <a name="can-basicpro-series-databases-be-upgraded-in-place-similar-tooplanetary-plans-today-on-cleardb-portal"></a>Basic/Pro 系列資料庫會升級的就地類似 tooPlanetary 計劃今天 ClearDB 入口網站？
是，可以就地升級基本系列資料庫 (基本 60 到基本 500)。 可以就地升級專業系列 (專業 125 到專業 1000)，但專業 60 除外。 我們目前不支援升級專業 60 資料庫。 

## <a name="when-i-migrate-my-resources-from-one-subscription-tooanother-does-my-cleardb-mysql-database-get-migrated-as-well"></a>當我從一個訂用帳戶 tooanother 移轉我的資源時，並 ClearDB MySQL 資料庫移轉以及嗎？
當跨訂用帳戶執行資源移轉時，適用某些 [限制](app-service-web/app-service-move-resources.md) 。 ClearDB MySQL 資料庫是第三方服務，因此在 Azure 訂用帳戶移轉期間是不會移轉的。 如果您不會管理 hello 移轉您的 MySQL 資料庫先前 toomigrating Azure 資源，您可以停用資料庫的 ClearDB MySQL。 請先手動移轉資料庫，然後再為您的 Web 應用程式執行 Azure 訂用帳戶移轉作業。 

## <a name="i-hit-hello-spending-limit-on-my-subscription-i-removed-hello-limit-and-my-app-service-is-online-however-hello-database-is-not-accessible-how-do-i-re-enable-hello-cleardb-database"></a>我已達到 hello 我的訂用帳戶消費限制。 我移除 hello 限制和我的應用程式服務已上線，但不能存取 hello 資料庫。 如何重新啟用 hello 的 ClearDB 資料庫？
請連絡[ClearDB 支援](https://www.cleardb.com/developers/help/support)toore 啟用 hello 資料庫。 提供您的 Azure 訂用帳戶資訊和資料庫名稱。

## <a name="can-i-transfer-a-cleardb-database-from-a-credit-card-subscription-tooan-ea-subscription"></a>可以從信用卡訂用帳戶 tooan EA 訂用帳戶轉移的 ClearDB 資料庫嗎？
現有的 ClearDB 資料庫使用與 hello 現有的訂閱相關聯的 hello 信用卡。 toouse tooa 新資料的資料庫需要 toomigrate EA 訂用帳戶：

* 使用您的 EA 訂用帳戶購買新 ClearDB 資料庫。
* 移轉資料 tooyour 新資料庫。
* 更新應用程式 toouse hello 新資料庫。
* 刪除舊的 ClearDB 資料庫。

當您使用 MySQL (ClearDB) 建立新的 web 應用程式，或建立 MySQL database (ClearDB) 時，您所選擇的 hello 訂用帳戶會決定您將支付 hello 服務。 EA 訂用帳戶，我們不會封鎖 hello 協力廠商服務，例如 ClearDB hello Azure 入口網站中的 hello 的採購。 將每季並以後付方式向 EA 訂用帳戶就財務承諾以外收費。 hello EA 客戶要有 tooset 付款方式例如信用卡 toopay 任何第三方 marketplace 服務的設定。

## <a name="where-can-i-see-hello-charges-for-cleardb-resources-in-an-ea-subscription"></a>哪裡可以看到 ClearDB 資源 EA 訂用帳戶中的 hello 費用？
對於直接 EA 客戶，Azure Marketplace 費用會顯示 hello 企業版入口網站。 請注意，所有 Marketplace 購買項目和使用均會每季並以後付方式就財務承諾以外收費。 EA 客戶有 toopay 直接 toohello 協力廠商服務提供者，而且可以執行因此藉由啟用付款方式，例如其 EA 的信用卡帳戶。

間接 EA 客戶可以找到其 Azure Marketplace 訂用帳戶上 hello**管理訂用帳戶**隱藏 hello 企業版入口網站，但定價頁面。 客戶應該連絡其 LSP 以了解相關的 Marketplace 費用資訊。

您的 EA Azure 註冊系統管理員可以管理協力廠商服務的存取 tooAzure Marketplace。 它們可以停用或重新啟用從 hello 企業版入口網站中的 hello 帳戶區段下的 hello 管理帳戶和訂用帳戶存放區中存取 too3rd 廠商購買。

## <a name="who-do-i-contact-for-questions-about-my-bill-for-cleardb-services-in-my-ea-subscription"></a>若對我的 EA 訂用帳戶中 ClearDB 服務的帳單有問題，應該連絡誰？
請連絡[企業客戶支援](http://aka.ms/AzureEntSupport)方面 toobilling EA 註冊下使用。 hello EA 入口網站支援小組將會回答您的問題，或協助解決您的問題。

## <a name="more-information"></a>詳細資訊
[Azure Marketplace 常見問題集](/marketplace/faq/)

