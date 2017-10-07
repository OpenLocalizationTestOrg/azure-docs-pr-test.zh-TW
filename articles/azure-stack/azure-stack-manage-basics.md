---
title: "aaaAzure 堆疊管理基本概念 |Microsoft 文件"
description: "了解您的需要 tooknow tooadminister Azure 堆疊。"
services: azure-stack
documentationcenter: 
author: twooley
manager: byronr
editor: 
ms.assetid: 856738a7-1510-442a-88a8-d316c67c757c
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: twooley
ms.openlocfilehash: cdf2818e9fc819b448508ca52bbdbec259890265
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stack-administration-basics"></a>Azure Stack 管理基本知識

有幾件事，您需要 tooknow，如果您是新 tooAzure 堆疊管理。 本指南概述您角色的雲端運算子，以及您為他們需要 tootell 您的使用者生產力 toobecome 快速。

## <a name="understand-development-kit-builds"></a>了解開發套件組建

檢閱 hello[什麼是 Azure 堆疊？](azure-stack-poc.md)文章 toomake 確定您了解 hello 目的 hello Azure 堆疊開發套件，以及其限制。 您應該為 「 沙箱 」 評估 Azure 堆疊和開發和測試您的應用程式在非生產環境中使用 hello 開發套件。 (如需部署資訊，請參閱 hello [Azure 堆疊開發套件部署](azure-stack-deploy-overview.md)快速入門。)

就像 Azure 一樣，我們迅速地進行創新。 我們會定期發行新組建。 當您想 toomove toohello 最新組建時，您必須[重新部署 Azure 堆疊](azure-stack-redeploy.md)。 此程序需要的時間，但 hello 好處是您可以試用 hello 最新的功能。 我們的網站上的 hello 文件會反映最新版本組建 hello。

## <a name="learn-about-available-services"></a>了解可用的服務

您將需要的哪些服務，您可以將可用的 tooyour 使用者感知。 Azure Stack 支援 Azure 服務的子集。 支援服務 hello 清單將會繼續 tooevolve。

**基礎服務**

根據預設，Azure 堆疊會包含下列 「 基本服務 」 的 hello 當您部署 Azure 堆疊：

- 計算
- 儲存體
- 網路
- 金鑰保存庫

利用這些基本服務，您可以提供基礎結構做為服務 (IaaS) tooyour 使用者，以最低組態。

**其他服務**

目前，我們支援下列其他平台做為服務 (PaaS) 服務的 hello:

- App Service
- Azure Functions
- SQL 和 MySQL 資料庫

這些服務需要其他設定，才能讓可用 tooyour 使用者。 如需詳細資訊，請參閱 hello 」 教學課程 」 和 hello 文件的 「 如何 tooguides\Offer 服務 」 各節。

**服務藍圖**

Azure 堆疊將會繼續 tooadd 支援 Azure 服務。 預計的 hello 藍圖，請參閱 hello[混合式應用程式創新，使用 Azure 和 Azure 堆疊](https://go.microsoft.com/fwlink/?LinkId=842846&clcid=0x409)白皮書。 您也可以監視 hello [Azure 堆疊部落格文章](https://azure.microsoft.com/blog/tag/azure-stack-technical-preview)新宣告。

## <a name="what-tools-do-i-use-toomanage"></a>工具的作用為何使用 toomanage 嗎？
 
您可以使用 hello[管理員入口網站](azure-stack-manage-portals.md)或 PowerShell toomanage Azure 堆疊。 hello 最簡單方式 toolearn hello 基本概念都是透過 hello 入口網站。 如果您想 toouse PowerShell 時，有準備步驟。 您必須[安裝](azure-stack-powershell-install.md) PowerShell、[下載](azure-stack-powershell-download.md)其他模組，並[設定](azure-stack-powershell-configure-admin.md) PowerShell。

Azure Stack 使用 Azure Resource Manager 作為其基礎的部署、管理及組織機制。 如果您打算 toomanage Azure 堆疊和說明支援使用者，您應該了解有關資源管理員。 請參閱 hello[開始使用 Azure 資源管理員](http://download.microsoft.com/download/E/A/4/EA4017B5-F2ED-449A-897E-BD92E42479CE/Getting_Started_With_Azure_Resource_Manager_white_paper_EN_US.pdf)白皮書。

## <a name="your-typical-responsibilities"></a>您的一般責任

您的使用者想 toouse 服務。 從其觀點來看，您的主要角色是 toomake 這些服務可用 toothem。 您必須決定哪些服務 toooffer，並藉由建立提供這些服務[配額](azure-stack-setting-quotas.md)，[計劃](azure-stack-create-plan.md)，和[提供](azure-stack-create-offer.md)。 

您還需要 tooadd 項目 toohello marketplace，例如虛擬機器映像。 hello 最簡單方式是太[下載 marketplace 項目從 Azure tooAzure 堆疊](azure-stack-download-azure-marketplace-item.md)。

> [!NOTE]
> 如果您計劃、 提議和服務，您會想 tootest，您應該使用 hello[使用者入口網站](azure-stack-manage-portals.md); hello 管理員入口網站。

在加法 tooproviding services 中，您必須執行雲端運算子 tookeep Azure 堆疊的 hello 一般的責任啟動且正在執行。 這些責任 hello 如下：

- 新增使用者帳戶 (如 [Azure Active Directory](azure-stack-add-new-user-aad.md) 部署或 [Active Directory 同盟服務](azure-stack-add-users-adfs.md)部署)
- [指派角色型存取控制 (RBAC) 角色](azure-stack-manage-permissions.md)（這是不受限制的 tooadministrators。）
- [監視基礎結構健康情況](azure-stack-monitor-health.md)
- 管理[網路](azure-stack-viewing-public-ip-address-consumption.md)和[儲存體](azure-stack-manage-storage-accounts.md)資源
- 取代故障的硬體

## <a name="what-tootell-your-users"></a>哪些 tootell 您的使用者

您將需要您的使用者知道與 toowork services 如何在 Azure 堆疊 tooconnect toohello 開發套件的環境中，以及如何 toolet toosubscribe toooffers。

**了解 Azure 堆疊中 toowork 與服務的方式**

在使用服務和 Azure Stack 中的應用程式之前，有些資訊您的使用者必須先了解。 例如，有特定的 PowerShell 和 API 版本需求。 此外，還有 Azure 服務與 hello Azure 堆疊中的對等服務之間的某些功能差異。 請確定您的使用者，檢閱下列文章 hello:

- [關鍵考量：使用 Azure Stack 的服務或組建 Azure Stack 應用程式](azure-stack-considerations.md)
- [Azure Stack 中虛擬機器的考量](azure-stack-vm-considerations.md)
- [儲存體：差異和考量](azure-stack-acs-differences-tp2.md)

這些文章中的 hello 資訊摘要說明 hello Azure 中的服務與 Azure 堆疊之間的差異。 它會補充適用於 Azure 服務 hello 全域 Azure 文件中的 hello 資訊。 

**以使用者身分連接 tooAzure 堆疊**

在開發套件環境中，如果使用者沒有遠端桌面存取 toohello 開發套件主應用程式，它們必須設定虛擬私人網路 (VPN) 連線，才能存取 Azure 堆疊。 請參閱[連接 tooAzure 堆疊](azure-stack-connect-azure-stack.md)。 

您的使用者將如何太想 tooknow[存取 hello 使用者入口網站](azure-stack-manage-portals.md)或如何透過 PowerShell tooconnect。 如果使用 PowerShell，使用者可能必須 tooregister 資源提供者，才能使用服務。 (資源提供者負責管理服務。 例如，網路功能資源提供者的 hello 管理資源，例如虛擬網路、 網路介面和負載平衡器。)他們必須[安裝](azure-stack-powershell-install.md) PowerShell、[下載](azure-stack-powershell-download.md) 其他模組，並[設定](azure-stack-powershell-configure-user.md) PowerShell (其中包含資源提供者註冊)。

**訂閱 tooan 供應項目**

使用者可以存取服務之前，它們必須[訂閱 tooan 優惠](azure-stack-subscribe-plan-provision-vm.md)您已建立雲端操作員。

## <a name="where-tooget-support"></a>其中 tooget 支援

Hello Azure 堆疊開發套件，您可以要求支援相關的問題，在 hello [Microsoft 論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=azurestack)。 如果您按一下 hello 說明及支援圖示 （問號） 中的 hello 管理員入口網站，hello 右上角，然後按一下**新增支援要求**，這會直接開啟 hello 論壇網站。 我們會定期留意這些論壇。 Hello 開發套件是評估環境，因為沒有提供透過 Microsoft 客戶支援服務 (CSS) 提供官方支援。

## <a name="next-steps"></a>後續步驟

- [Azure Stack 中的區域管理](azure-stack-region-management.md)


