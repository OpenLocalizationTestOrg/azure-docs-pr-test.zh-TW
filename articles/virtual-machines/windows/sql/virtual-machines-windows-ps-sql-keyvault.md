---
title: "aaaIntegrate 金鑰保存庫在 Azure （資源管理員） 中的 Windows Vm 上的 SQL server |Microsoft 文件"
description: "了解如何 tooautomate hello 的 Azure 金鑰保存庫搭配使用的 SQL Server 加密組態。 本主題說明如何搭配 SQL Server 虛擬機器的 Azure 金鑰保存庫整合 toouse 建立與資源管理員。"
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: cd66dfb1-0e9b-4fb0-a471-9deaf4ab4ab8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/23/2017
ms.author: jroth
ms.openlocfilehash: 0d36d3d075d6538c18cd5ecb43c19a4b000a99e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-resource-manager"></a>在 Azure 虛擬機器上設定 SQL Server 的 Azure Key Vault 整合 (Resource Manager)
> [!div class="op_single_selector"]
> * [資源管理員](virtual-machines-windows-ps-sql-keyvault.md)
> * [傳統](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a>概觀
有多個 SQL Server 加密功能，例如[透明資料加密 (TDE)](https://msdn.microsoft.com/library/bb934049.aspx)、[資料行層級加密 (CLE)](https://msdn.microsoft.com/library/ms173744.aspx) 和[備份加密](https://msdn.microsoft.com/library/dn449489.aspx)。 這些形式的加密需要您 toomanage，而儲存 hello 用來加密的密碼編譯金鑰。 hello Azure 金鑰保存庫 (AKV) 服務是設計的 tooimprove hello 安全性和管理高可用性的位置中的這些索引鍵。 hello [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344)可讓 SQL Server toouse Azure 金鑰保存庫中的這些索引鍵。

如果您在內部部署與執行 SQL Server 的電腦上，那里會[步驟，您可以從內部部署 SQL Server 電腦遵循 tooaccess Azure 金鑰保存庫](https://msdn.microsoft.com/library/dn198405.aspx)。 在 Azure Vm 中的 SQL server，您可以使用 hello 來節省時間，但是*Azure 金鑰保存庫整合*功能。

啟用這項功能時，它會自動安裝 SQL Server Connector hello、 設定 hello EKM 提供者 tooaccess Azure 金鑰保存庫，並且建立 hello 認證 tooallow 您 tooaccess 您保存庫。 如果您在查看 hello 中的 hello 步驟先前所述內部文件，您可以看到這項功能會自動執行步驟 2 和 3。 您仍然必須 toodo 手動 hello 唯一的是 toocreate hello 金鑰保存庫和金鑰。 從該處，hello 整個安裝的 SQL VM 會自動執行。 此安裝程式完成後這項功能，您可以執行 T-SQL 陳述式 toobegin 加密您的資料庫或備份，像平常一樣。

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="enabling-and-configuring-akv-integration"></a>啟用及設定 AKV 整合
您可以在佈建期間啟用 AKV 整合，或針對現有的 VM 設定這項整合。

### <a name="new-vms"></a>新的 VM
如果您佈建新的 SQL Server 虛擬機器與資源管理員，hello Azure 入口網站會提供步驟 tooenable Azure 金鑰保存庫整合。 hello Azure 金鑰保存庫功能是僅供 hello Enterprise、 Developer 和 Evaluation 等版本的 SQL Server。

![SQL Azure 金鑰保存庫整合](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-arm-akv.png)

佈建的詳細逐步解說，請參閱[hello Azure 入口網站中的 SQL Server 虛擬機器佈建](virtual-machines-windows-portal-sql-server-provision.md)。

### <a name="existing-vms"></a>現有的 VM
如果是現有的 SQL Server 虛擬機器，請選取您的 SQL Server 虛擬機器。 然後選取 hello **SQL Server 組態**區段 hello**設定**刀鋒視窗。

![現有 VM 的 SQL AKV 整合](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-existing-vms.png)

在 hello **SQL Server 組態**刀鋒視窗中，按一下 hello**編輯**hello 自動化的金鑰保存庫整合 > 一節中的按鈕。

![設定現有 VM 的 SQL AKV 整合](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-configuration.png)

完成後，請按一下 hello **[確定]**上 hello hello 底部的按鈕**SQL Server 組態**刀鋒視窗 toosave 您的變更。

> [!NOTE]
> 您也可以使用範本來設定 AKV 整合。 如需詳細資訊，請參閱 [適用於 Azure 金鑰保存庫整合的 Azure 快速入門範本](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update)。
> 
> 

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

