---
title: "適用於 Linux Vm 的金鑰保存庫註冊以 hello Azure CLI 1.0 的 aaaSet |Microsoft 文件"
description: "如何搭配使用 Azure 資源管理員虛擬機器使用金鑰保存庫註冊 tooset hello Azure CLI 1.0。"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: 275022e4e7e26d7363784c289dd7512047c07bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager-with-hello-azure-cli-10"></a>設定金鑰保存庫的虛擬機器的 Azure 資源管理員中設定以 hello Azure CLI 1.0
Hello Azure Resource Manager 堆疊中的密碼/憑證會模型化為 hello 的金鑰保存庫的資源提供者所提供的資源。 toolearn 進一步了解 Azure 金鑰保存庫，請參閱[何謂 Azure Key Vault？](../../key-vault/key-vault-whatis.md) 為了讓搭配 Azure 資源管理員虛擬機器使用的金鑰保存庫 toobe，hello *EnabledForDeployment* tootrue 必須設定金鑰保存庫上的屬性。 您可以在各種用戶端中執行這項操作。 本文章將示範如何使用與 Azure 虛擬機器設定金鑰保存庫 tooset。

## <a name="cli-versions-toocomplete-hello-task"></a>CLI 版本 toocomplete hello 工作
您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本

- [Azure CLI 1.0](#quick-commands) – 我們 CLI hello 傳統和資源管理部署模型 （此文件）
- [Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -hello 資源管理部署模型我們下一個層代 CLI

## <a name="use-cli-10-tooset-up-key-vault"></a>使用金鑰保存庫註冊的 CLI 1.0 tooset
toocreate 金鑰保存庫使用 hello 命令列介面 (CLI)，請參閱[管理金鑰保存庫使用 CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault)。

CLI 1.0 時，您必須 toocreate hello 金鑰保存庫後，再指派 hello 部署原則。 然後，您可以使用下列命令的 hello 指派 hello 原則：

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a>使用金鑰保存庫註冊的範本 tooset
當您使用範本時，您需要 tooset hello`enabledForDeployment`屬性太`true`hello 金鑰保存庫資源。

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
