---
title: "aaaIntegrate 金鑰保存庫在 Azure （傳統） 中的 Windows Vm 上的 SQL server |Microsoft 文件"
description: "了解如何 tooautomate hello 的 Azure 金鑰保存庫搭配使用的 SQL Server 加密組態。 本主題說明如何使用 SQL Server 虛擬機器的 Azure 金鑰保存庫整合 toouse 建立 hello 傳統部署模型中。"
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: ab8d41a7-1971-4032-ab71-eb435c455dc1
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 02/17/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 54664875b76dac7271d5a9f00b3f41fdc9c08491
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-classic"></a>在 Azure 虛擬機器上設定 SQL Server 的 Azure Key Vault 整合 (傳統)
> [!div class="op_single_selector"]
> * [資源管理員](../sql/virtual-machines-windows-ps-sql-keyvault.md)
> * [傳統](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a>概觀
有多個 SQL Server 加密功能，例如[透明資料加密 (TDE)](https://msdn.microsoft.com/library/bb934049.aspx)、[資料行層級加密 (CLE)](https://msdn.microsoft.com/library/ms173744.aspx) 和[備份加密](https://msdn.microsoft.com/library/dn449489.aspx)。 這些形式的加密需要您 toomanage，而儲存 hello 用來加密的密碼編譯金鑰。 hello Azure 金鑰保存庫 (AKV) 服務是設計的 tooimprove hello 安全性和管理高可用性的位置中的這些索引鍵。 hello [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344)可讓 SQL Server toouse Azure 金鑰保存庫中的這些索引鍵。

> [!IMPORTANT] 
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。

如果您沒有執行 SQL Server 在內部部署機器，有[步驟，您可以從內部部署 SQL Server 電腦遵循 tooaccess Azure 金鑰保存庫](https://msdn.microsoft.com/library/dn198405.aspx)。 在 Azure Vm 中的 SQL server，您可以使用 hello 來節省時間，但是*Azure 金鑰保存庫整合*功能。 少數的 Azure PowerShell cmdlet tooenable 這項功能，您可以使用自動化 hello 組態所需的 SQL VM tooaccess 金鑰保存庫。

啟用這項功能時，它會自動安裝 SQL Server Connector hello、 設定 hello EKM 提供者 tooaccess Azure 金鑰保存庫，並且建立 hello 認證 tooallow 您 tooaccess 您保存庫。 如果您在查看 hello 中的 hello 步驟先前所述內部文件，您可以看到這項功能會自動執行步驟 2 和 3。 您仍然必須 toodo 手動 hello 唯一的是 toocreate hello 金鑰保存庫和金鑰。 從該處，hello 整個安裝的 SQL VM 會自動執行。 此安裝程式完成後這項功能，您可以執行 T-SQL 陳述式 toobegin 加密您的資料庫或備份，像平常一樣。

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="configure-akv-integration"></a>設定 AKV 整合
使用 PowerShell tooconfigure Azure 金鑰保存庫整合。 hello 下列各節提供所需的 hello 參數的概觀，然後的範例 PowerShell 指令碼。

### <a name="install-hello-sql-server-iaas-extension"></a>安裝 SQL Server IaaS 延伸模組 hello
首先，[安裝 SQL Server IaaS 延伸模組 hello](../classic/sql-server-agent-extension.md)。

### <a name="understand-hello-input-parameters"></a>了解 hello 輸入的參數
hello 下列資料表列出 hello 參數需要 toorun hello PowerShell 指令碼 hello 下一節。

| 參數 | 說明 | 範例 |
| --- | --- | --- |
| **$akvURL** |**hello 金鑰保存庫 URL** |"https://contosokeyvault.vault.azure.net/" |
| **$spName** |**服務主體名稱** |"fde2b411-33d5-4e11-af04eb07b669ccf2" |
| **$spSecret** |**服務主體密碼** |"9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM=" |
| **$credName** |**認證名稱**: AKV 整合建立 SQL Server，讓 hello VM toohave 存取 toohello 金鑰保存庫中的認證。 選擇此認證的名稱。 |"mycred1" |
| **$vmName** |**虛擬機器名稱**: hello 先前建立的 SQL VM 名稱。 |"myvmname" |
| **$serviceName** |**服務名稱**: hello 與 hello SQL VM 相關聯的雲端服務名稱。 |"mycloudservicename" |

### <a name="enable-akv-integration-with-powershell"></a>使用 PowerShell 啟用 AKV 整合
hello**新增 AzureVMSqlServerKeyVaultCredentialConfig** cmdlet 會建立 hello Azure 金鑰保存庫整合功能的組態物件。 hello**組 AzureVMSqlServerExtension**設定這項整合以 hello **KeyVaultCredentialSettings**參數。 hello 下列步驟顯示如何 toouse 這些命令。

1. 在 Azure PowerShell 中，先設定 hello 輸入的參數的特定值 hello 本主題的前幾節中所述。 下列指令碼的 hello 是範例。
   
        $akvURL = "https://contosokeyvault.vault.azure.net/"
        $spName = "fde2b411-33d5-4e11-af04eb07b669ccf2"
        $spSecret = "9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM="
        $credName = "mycred1"
        $vmName = "myvmname"
        $serviceName = "mycloudservicename"
2. 然後使用 hello 以下 tooconfigure 編寫指令碼，並啟用 AKV 整合。
   
        $secureakv =  $spSecret | ConvertTo-SecureString -AsPlainText -Force
        $akvs = New-AzureVMSqlServerKeyVaultCredentialConfig -Enable -CredentialName $credname -AzureKeyVaultUrl $akvURL -ServicePrincipalName $spName -ServicePrincipalSecret $secureakv
        Get-AzureVM -ServiceName $serviceName -Name $vmName | Set-AzureVMSqlServerExtension -KeyVaultCredentialSettings $akvs | Update-AzureVM

hello SQL IaaS 代理程式延伸模組將會更新這個新的設定 hello SQL VM。

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

