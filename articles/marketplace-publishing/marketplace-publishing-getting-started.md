---
title: "如何的 aaaOverview toocreate 及部署方案 toohello Marketplace |Microsoft 文件"
description: "了解 hello 步驟需要的 toobecome 核准的 Microsoft 開發人員，建立及部署虛擬機器映像、 範本、 資料服務或在 hello Azure Marketplace 中的開發人員服務"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 5343bd26-c6e4-4589-85b7-4a2c00bba8ab
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/05/2017
ms.author: hascipio
ms.openlocfilehash: ac5480b98b8b1021a595db951ed9c974f74415dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publish-and-manage-an-offer-in-hello-azure-marketplace"></a>發佈和管理在 hello Azure Marketplace 提供項目
這篇文章會提供 toohelp 開發人員建立、 部署和管理他們 hello Azure Marketplace 中列出的其他 Azure 客戶和合作夥伴 toopurchase 和使用的解決方案。

## <a name="marketplace-publishing"></a>Marketplace 發佈
為 Azure 的 「 發行者 」，您可以發佈和銷售您的創新方案或服務 tooother 開發人員，Isv 和 IT 專業人員在 hello Marketplace。 透過 hello Marketplace，您可以連線到客戶希望 tooquickly 開發雲端應用程式與行動方案。 如果您的方案的目標商務使用者，您可能想 tooconsider hello [AppSource](http://appsource.microsoft.com) marketplace。


## <a name="supported-types-of-solutions"></a>支援的解決方案類型
因為 「 發行者 」 是 toodefine 貴公司提供哪些類型的方案，您會想 toodo hello 第一件事。 hello Marketplace 支援下列類型的優惠的 hello:

|解決方案類型|虛擬機器|解決方案範本|
|---|---|---|
|**定義**|預先配置的映像，包含完整安裝的作業系統以及一或多個應用程式。 虛擬機器映像提供 hello 資訊必要 toocreate，並部署 hello Azure 虛擬機器服務中的虛擬機器。|可參考一或多個獨特 Azure 服務 (包含由其他賣家發佈的服務) 的資料結構。 Azure 的訂閱者可以使用它 toodeploy 以單一、 協調的方式中一或多個供應項目。|
|**範例**|身為 Azure 發行者，您已建立並驗證帶有創新資料庫服務的 VM。 其他 Azure 訂戶想 tooprocure，並將此 VM 部署至雲端服務環境。|為 Azure 的 「 發行者 」，您已配套一的組服務從整個 Azure，可讓您快速 toodeploy 與負載平衡、 增強式的安全性、 高可用性的雲端服務。 其他 Azure 訂戶可以獲得符合其目標的 hello 解決方案範本，以節省時間。 在沒有 toomanually 找出、 採購、 部署和設定 hello 相同或類似的 Azure 服務。|

> [!NOTE]
> 某些步驟之間會共用 hello 不同類型解決方案，因此有些則解決方案的相異 toohello 個別的型別。 本文章提供簡短的概觀的 hello 步驟需 toocomplete 的任何類型的解決方案。

## <a name="publish-a-solution"></a>發佈解決方案
![提名、註冊、發佈](media/marketplace-publishing-getting-started/img01.png)

### <a name="nominate-your-solution-for-pre-approval"></a>提名您的解決方案以供預先核准
虛擬機器 toopublish[方案](https://createopportunity.azurewebsites.net)toohello Marketplace，完成 Microsoft Azure 認證的 hello**方案提名表單**。

>[!NOTE]
> 如果您正在使用協力廠商客戶經理或 DX 夥伴管理員，要求他們 toonominate hello Azure 認證計劃您的方案。 您也可以移 toohello [Microsoft Azure 認證](http://createopportunity.azurewebsites.net)網頁和填寫 hello 應用程式表單。 輸入 hello 夥伴客戶經理或 DX 夥伴管理員的電子郵件中 hello **Microsoft 發起人連絡人**方塊。

如果符合在 hello hello 適用性準則[Azure Marketplace 參與原則](http://go.microsoft.com/fwlink/?LinkID=526833)和您的應用程式獲得核准後，我們開始使用您 tooonboard 您方案 toohello Marketplace。

### <a name="register-your-account-as-a-microsoft-seller"></a>將您的帳戶註冊為 Microsoft 賣方
將您的 Microsoft 帳戶註冊為 [Microsoft 開發人員帳戶](marketplace-publishing-accounts-creation-registration.md)。

### <a name="publish-your-solution"></a>發佈您的解決方案
toopublish 方案 toohello 服務商場，請遵循下列步驟：
1. 符合 hello 非技術性的需求。

    a. 滿足 hello[非技術性的必要條件](marketplace-publishing-pre-requisites.md)。

    b. 滿足 hello [VM 技術必要條件](marketplace-publishing-vm-image-creation-prerequisites.md)。

    c. 滿足 hello[方案範本技術必要條件](marketplace-publishing-solution-template-creation-prerequisites.md)。

2. 建立您的供應項目。

    a. 建立[虛擬機器](marketplace-publishing-vm-image-creation.md)供應項目。

    b.這是另一個 C# 主控台應用程式。 建立[解決方案範本](marketplace-publishing-solution-template-creation.md)供應項目。

3. 建立您的供應項目[行銷內容](marketplace-publishing-push-to-staging.md)。

4. 在預備環境中測試您的供應項目。

    a. 在[預備環境](marketplace-publishing-vm-image-test-in-staging.md)中測試您的 VM 供應項目。

    b.這是另一個 C# 主控台應用程式。 在[預備環境](marketplace-publishing-solution-template-test-in-staging.md)中測試您的解決方案範本供應項目。

5. 部署您的優惠 toohello [Marketplace](marketplace-publishing-push-to-production.md)。


### <a name="create-and-manage-a-virtual-machine-image"></a>建立和管理虛擬機器映像
使用這些資源來建立和管理 VM 映像︰
* 建立[內部部署](marketplace-publishing-vm-image-creation-on-premise.md) VM 映像。
* 建立虛擬機器執行[hello Azure 入口網站中的 Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
* 建立虛擬機器執行[hello Azure 入口網站中的 Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
* 針對 [VHD 建立](marketplace-publishing-vm-image-creation-troubleshooting.md)常見問題進行疑難排解。

## <a name="manage-your-solution"></a>管理您的解決方案
管理您的解決方案，協助從 hello 下列資源：
* [虛擬機器的讀取 hello 後製指南提供](marketplace-publishing-vm-image-post-publishing.md)
* [更新優惠或 SKU 的 hello 非技術性的詳細資料](marketplace-publishing-vm-image-post-publishing.md#update-the-nontechnical-details-of-an-offer-or-a-sku)
* [更新優惠或 SKU 的 hello 技術的詳細資料](marketplace-publishing-vm-image-post-publishing.md#update-the-technical-details-of-a-sku)
* [在已列出的供應項目下新增 SKU](marketplace-publishing-vm-image-post-publishing.md#add-a-new-sku-under-a-listed-offer)
* [變更所列的 SKU hello 資料磁碟計數](marketplace-publishing-vm-image-post-publishing.md#change-the-data-disk-count-for-a-listed-sku)
* [列出的優惠刪除 hello Marketplace](marketplace-publishing-vm-image-post-publishing.md)
* [從 hello Marketplace 刪除列出的 SKU](marketplace-publishing-vm-image-post-publishing.md#delete-a-listed-sku-from-the-marketplace)
* [從 hello Marketplace 刪除 hello 目前版本列出的 SKU](marketplace-publishing-vm-image-post-publishing.md#delete-the-current-version-of-a-listed-sku-from-the-marketplace)
* [還原 hello 列出價格 tooproduction 值](marketplace-publishing-vm-image-post-publishing.md#revert-the-listing-price-to-production-values)
* [還原 hello 計費模型 tooproduction 值](marketplace-publishing-vm-image-post-publishing.md#revert-the-billing-model-to-production-values)
* [還原列出的 SKU toohello 生產環境值 hello 可見性設定](marketplace-publishing-vm-image-post-publishing.md#revert-the-visibility-setting-of-a-listed-sku-to-the-production-value)
* [變更雲端解決方案提供者轉售商獎勵](marketplace-publishing-csp-incentive.md)
* [了解付款報告](marketplace-publishing-report-payout.md)
* [以發佈者身分取得支援](marketplace-publishing-get-publisher-support.md)

## <a name="additional-resources"></a>其他資源
[設定 Azure PowerShell](marketplace-publishing-powershell-setup.md)
