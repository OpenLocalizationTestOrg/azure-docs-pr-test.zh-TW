---
title: "啟動金鑰保存庫的 Windows Vm 在 Azure 資源管理員 aaaSet |Microsoft 文件"
description: "如何搭配 Azure 資源管理員虛擬機器使用金鑰保存庫註冊 tooset。"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 33a483e2-cfbc-4c62-a588-5d9fd52491e2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: kasing
ms.openlocfilehash: 53bbe90708202ecfdcf754822d04bf2469631f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager"></a>為 Azure Resource Manager 中的虛擬機器設定金鑰保存庫

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

Azure Resource Manager 堆疊中的密碼/憑證會模型化為 hello 的金鑰保存庫的資源提供者所提供的資源。 toolearn 進一步了解金鑰保存庫，請參閱[何謂 Azure Key Vault？](../../key-vault/key-vault-whatis.md)

> [!NOTE]
> 1. 為了讓搭配 Azure 資源管理員虛擬機器使用的金鑰保存庫 toobe，hello **EnabledForDeployment** tootrue 必須設定金鑰保存庫上的屬性。 您可以在各種用戶端中執行這項操作。
> 2. hello toobe 中建立的金鑰保存庫需求 hello 相同訂用帳戶和位置，如 hello 虛擬機器。
>
>

## <a name="use-powershell-tooset-up-key-vault"></a>使用 PowerShell tooset 金鑰保存庫註冊
toocreate 金鑰保存庫使用 PowerShell，請參閱[開始使用 Azure 金鑰保存庫](../../key-vault/key-vault-get-started.md#vault)。

針對新的「金鑰保存庫」，您可以使用下列 PowerShell Cmdlet：

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -EnabledForDeployment

針對現有的「金鑰保存庫」，您可以使用下列 PowerShell Cmdlet：

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

## <a name="us-cli-tooset-up-key-vault"></a>我們 CLI tooset 金鑰保存庫註冊
toocreate 金鑰保存庫使用 hello 命令列介面 (CLI)，請參閱[管理金鑰保存庫使用 CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault)。

CLI 中，您必須 toocreate hello 金鑰保存庫後，再指派 hello 部署原則。 您可以使用下列命令的 hello:

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a>使用金鑰保存庫註冊的範本 tooset
雖然您使用範本，您需要 tooset hello`enabledForDeployment`屬性太`true`hello 金鑰保存庫資源。

    {
      "type": "Microsoft.KeyVault/vaults",
      "name": "ContosoKeyVault",
      "apiVersion": "2015-06-01",
      "location": "<location-of-key-vault>",
      "properties": {
        "enabledForDeployment": "true",
        ....
        ....
      }
    }

如需使用範本來建立金鑰保存庫時可以設定的其他選項，請參閱 [Create a Key Vault (建立金鑰保存庫)](https://azure.microsoft.com/documentation/templates/101-key-vault-create/)。
