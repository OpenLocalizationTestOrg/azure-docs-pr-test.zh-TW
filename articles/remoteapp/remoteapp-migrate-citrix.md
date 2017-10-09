---
title: "從 Azure RemoteApp tooCitrix XenApp Essentials aaaMigrate |Microsoft 文件"
description: "如何從 Azure RemoteApp tooCitrix XenApp Essentials toomigrate"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 695a8165-3454-4855-8e21-f2eb2c61201b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: aa3ce28bc5a86d5b1dd3408196d51935395f55c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-azure-remoteapp-toocitrix-xenapp-essentials"></a>從 Azure RemoteApp tooCitrix XenApp Essentials 移轉

您使用 Azure RemoteApp，而且您想要 toomigrate tooCitrix XenApp Essentials，有幾個必要條件 tookeep 記住。 首先，請閱讀 Citrix 的 [Citrix XenApp Essentials 技術部署逐步指南](https://docs.citrix.com/content/dam/docs/en-us/citrix-cloud/downloads/xenapp-essentials-deployment-guide.pdf) \(英文\)，以及其[線上技術文件庫](http://docs.citrix.com/en-us/citrix-cloud/xenapp-and-xendesktop-service/xenapp-essentials.html) \(英文\)。 

## <a name="prerequisite-steps-for-migration"></a>移轉先決條件步驟

1. 建立新的虛擬網路，或決定您要在 Azure Resource Manager 的哪個 Azure 虛擬網路中部署 Citrix XenApp Essentials。 Azure RemoteApp 使用 hello Azure 傳統入口網站。Citrix XenApp Essentials 僅支援 Azure 資源管理員。  
2. 請確定您選取該 hello 虛擬網路，具有網路存取 tooyour 網域控制站，因為 Citrix 只支援混合式部署。 如果您使用的 Azure RemoteApp 雲端部署，請確定您的虛擬網路的網路存取 tooan Active Directory 網域控制站。 您也可以使用 Azure Active Directory Domain Services (Azure AD DS)。 
3. 請確認該 DNS 已正確設定 hello 虛擬網路，以便加入該網域是您第一次嘗試成功的 hello。 您可以在您選取，hello 虛擬網路中建立虛擬機器 (VM)，並執行手動網域聯結 tooverify 該 hello DNS 和網域聯結如預期般運作。 這可確保您已成功 hello 部署 Citrix XenApp Essentials 的第一次。 
4. 如有需要，請在搭配 Azure RemoteApp 使用的 Azure 傳統入口網站虛擬網路，和您的 Azure Resource Manager 虛擬網路之間，建立虛擬網路對等互連。 此對等互連的程序的運作 hello 兩個網路位於 hello 相同區域。 如果沒有的話，使用站對站 VPN tooconnect hello 虛擬網路的網路功能。 
5. 如有需要讀取[如何 toomigrate 資料傳入活動和從 Azure RemoteApp](remoteapp-migrate.md)。 
6. 更新您現有 Azure RemoteApp 映像 tooinclude hello Citrix VDA 元件 （如需指示，請參閱 hello Citrix 文件）。 
7. 移 toohello Azure Marketplace 並開始 Citrix XenApp Essentials 部署。

## <a name="other-considerations"></a>其他考量

請注意下列其他考量，當您移轉的 hello:
- Citrix XenApp Essentials 僅支援混合式部署。 換句話說，它會需要網路存取 tooa 網域控制站中順序 tooperform 網域加入。 如果您使用的 Azure RemoteApp 雲端部署，請使用 Azure AD DS，或請確認您的虛擬網路已加入網域的存取 tooActive 目錄。 
- 如何 toomove 使用者資料 tooCitrix XenApp Essentials 的伺服器，請參閱的 toolearn[如何 toomigrate 資料傳入活動和從 Azure RemoteApp](remoteapp-migrate.md)。 
- Citrix XenApp Essentials 僅支援 Active Directory 帳戶。 它並不支援 Microsoft 帳戶 (例如 outlook.com、msn.com 或 hotmail.com)。 

## <a name="citrix-xenapp-essentials-billing"></a>Citrix XenApp Essentials 計費

如需定價的完整詳細資訊，請參閱 hello[常見問題集](https://www.citrix.com/global-partners/microsoft/resources/xenapp-essentials-faq.html#tab-30699)和[Citrix 概觀文章](https://www.citrix.com/global-partners/microsoft/remote-app.html)。 有三個計費元件 tooCitrix XenApp Essentials:

- hello Citrix 服務費用，也就是每位使用者每月 $12。 像所有 Azure Marketplace 購買項目，這是與您 Azure 訂用帳戶相關聯的計費的 toohello 付款方法。 如果您是 Enterprise 合約 (EA) 客戶，則無法使用 Azure 貨幣點數。 
- 遠端資料服務 (RDS) 用戶端存取授權 (CAL)。 目前，您可以為 $6.25 購買 hello 已包裝的遠端存取費用以 hello Citrix XenApp Essentials 付款。 如果您是 EA 客戶，您可以使用 Azure 的貨幣信用額度 toopay 這個。 如果您想 toouse 您現有的 RDS Cal 時，請與我們連絡[ arainfo@microsoft.com ](mailto:arainfo@microsoft.com)，因此我們可以套用這個 tooyour 帳單。 
- Azure 計算和儲存體。 這是 hello Azure 儲存體成本和計算耗用量的 hello Vm 使用。 在選取 VM 大小及使用者密度時，請注意價格。 如果您是 EA 客戶，您可以使用 Azure 的貨幣信用額度 toopay 這個。

如果仍有問題，您可以：
- 請透過下列電子郵件地址連絡我們：[arainfo@microsoft.com](mailto:arainfo@microsoft.com)。
- [連絡 Azure 支援](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)。 啟動[開啟 Azure 支援案例](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)toohelp 必要條件與步驟 1 到 5。 步驟 6-7，請連絡開啟支援票證 hello Citrix 管理入口網站中的 Citrix。 
