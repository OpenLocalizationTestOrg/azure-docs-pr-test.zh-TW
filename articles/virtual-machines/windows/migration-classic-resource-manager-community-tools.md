---
title: "aaaCommunity 工具-移動傳統資源 tooAzure 資源管理員 |Microsoft 文件"
description: "這個 hello 社群 toohelp 所提供的文件類別目錄 hello 工具移轉 IaaS 資源從傳統 toohello Azure Resource Manager 部署模型。"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 228b697b-3950-49f5-84bb-283bb56621b1
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 67d5624a14d12a2d9eb46eb12aef461b706d4589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="community-tools-toomigrate-iaas-resources-from-classic-tooazure-resource-manager"></a>社群工具 toomigrate 傳統 tooAzure 資源管理員的 IaaS 資源
Hello 社群 tooassist 所提供的 IaaS 資源從傳統 toohello Azure Resource Manager 部署的模型移轉與此發行項目錄 hello 工具。

> [!NOTE]
> 這些工具尚未獲得 Microsoft 支援服務的官方支援。 因此他們開啟 GitHub 上的來源，我們很高興 tooaccept Pr 修正或其他案例。 tooreport 有問題，請使用的 hello GitHub 問題功能。
> 
> 使用這些工具移轉可能會造成傳統虛擬機器停機。 如果您想要尋求平台支援的移轉，請造訪 
> 
>   * [平台支援移轉的 IaaS 資源從傳統 tooAzure Resource Manager 堆疊](migration-classic-resource-manager-overview.md)
>   * [平台技術的深入剖析支援從傳統 tooAzure 資源管理員移轉](migration-classic-resource-manager-deep-dive.md)
>   * [從傳統 tooAzure 使用 Azure PowerShell 的資源管理員移轉 IaaS 資源](migration-classic-resource-manager-ps.md)
> 
> 

## <a name="asmmetadataparser"></a>AsmMetadataParser
這是從 Azure 服務管理 tooAzure 資源管理員的企業移轉過程中建立的協助程式工具的集合。 此工具可讓您 tooreplicate 您的基礎結構，到另一個訂用帳戶可用於測試移轉與您生產訂用帳戶上執行 hello 移轉之前鐵發生的問題。

[連結 toohello 工具文件](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset)

## <a name="migaz"></a>migAz
migAz 是一組完整的傳統的 IaaS 資源 tooAzure 資源管理員的 IaaS 資源的其他選項 toomigrate。 hello 移轉會發生在 hello 相同訂用帳戶之間或不同的訂用帳戶與訂用帳戶類型 (例如： CSP 訂用帳戶)。

[連結 toohello 工具文件](https://github.com/Azure/migAz)

## <a name="next-steps"></a>後續步驟

* [平台支援移轉的 IaaS 資源從傳統 tooAzure 資源管理員概觀](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [技術的深入剖析平台支援移轉從傳統 tooAzure 資源管理員](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [規劃移轉的 IaaS 資源從傳統 tooAzure 資源管理員](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [使用傳統 tooAzure 資源管理員的 PowerShell toomigrate IaaS 資源](migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [使用 CLI toomigrate IaaS 資源從傳統 tooAzure 資源管理員](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [檢閱最常見的移轉錯誤](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [檢閱 hello 最常見問題集從傳統 tooAzure 資源管理員移轉的 IaaS 資源](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

