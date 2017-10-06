---
title: "建立虛擬機器映像的 hello Azure Marketplace aaaTechnical 必要條件 |Microsoft 文件"
description: "了解建立及部署虛擬機器映像 toohello Azure Marketplace 供其他人的 hello 需求 toopurchase。"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 63c16966-0304-4b17-a715-368a0a5ccb2c
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: fcae4d9e052581e3c1dfe7962e6d50ec31040419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="technical-prerequisites-for-creating-a-virtual-machine-image-for-hello-azure-marketplace"></a>技術建立虛擬機器映像的 hello Azure Marketplace 的必要條件
閱讀 hello 程序開始前，徹底，並了解為何，會執行每個步驟。 盡量，您應該準備您的公司資訊和其他資料，下載必要的工具和/或建立技術元件開始 hello 供應項目建立處理程序之前。 檢閱本文之後，您會更清楚這些項目。  

## <a name="download-needed-tools--applications"></a>下載需要的工具和應用程式
您應該有下列項目之後，再開始 hello 程序的 hello:

* 根據您的目標、 安裝 hello [Azure PowerShell cmdlet](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids)或[Linux 命令列介面工具](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409)從 hello [Azure 下載](https://azure.microsoft.com/downloads/)頁面。
* 從 CodePlex 安裝 Azure 儲存體總管。
* 下載並安裝適用於 Azure 認證 hello 憑證測試工具：
  * [http://go.microsoft.com/fwlink/?LinkID=526913](http://go.microsoft.com/fwlink/?LinkID=526913)。 您需要 Windows 型電腦 toorun hello 憑證 」 工具。 如果您沒有可用的 Windows 電腦，您可以執行使用 Windows 架構的 VM 在 Azure 中的 hello 工具。

## <a name="platforms-supported"></a>支援的平台
您可以在 Windows 或 Linux 上開發 Azure VM。 Hello 發行程序-例如建立 Azure 相容的虛擬硬碟 (VHD)-使用不同的工具和步驟的作業系統根據您使用的某些項目：  

* 如果您使用 Linux，請參閱"toohello 建立相容的 Azure VHD （以 Linux 為基礎） > 一節的 hello[虛擬機器映像發佈指南](marketplace-publishing-vm-image-creation.md)。
* 如果您使用 Windows 時，請參閱"toohello 建立相容的 Azure VHD （以 Windows 為基礎） > 一節的 hello[虛擬機器映像發佈指南](marketplace-publishing-vm-image-creation.md)。

> [!NOTE]
> 您需要存取 tooa Windows 為基礎的電腦：
> 
> * 執行 hello 憑證驗證工具。
> * 建立 hello VHD 憑證送出 hello VHD 共用存取簽章 URL。
> 
> 

## <a name="develop-your-vhd"></a>開發您的 VHD
您可以開發 Azure Vhd hello 雲端或內部部署中：

* 雲端開發表示所有開發步驟都會在 Azure 的 VHD 上遠端執行。
* 內部部署開發則需要使用內部部署基礎結構下載 VHD 和開發。 雖然可行，但我們不建議您這麼做。 請注意，開發 Windows 或 SQL 的內部部署需要您 toohave hello 相關的內部部署授權金鑰。 建立 VM 之後即無法加入或安裝 SQL Server。 您也必須提供根據已核准的 SQL 影像從 hello Azure 入口網站中。 如果您決定 toodevelop 內部，您必須不同於您在開發 hello 雲端中執行一些步驟。 您可以在 [建立內部部署 VM 映像](marketplace-publishing-vm-image-creation-on-premise.md)找到相關資訊。

[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
