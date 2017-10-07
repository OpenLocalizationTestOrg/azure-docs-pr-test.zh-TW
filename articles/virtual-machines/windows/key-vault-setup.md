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
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="c80eb-103">為 Azure Resource Manager 中的虛擬機器設定金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="c80eb-103">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="c80eb-104">Azure Resource Manager 堆疊中的密碼/憑證會模型化為 hello 的金鑰保存庫的資源提供者所提供的資源。</span><span class="sxs-lookup"><span data-stu-id="c80eb-104">In Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by hello resource provider of Key Vault.</span></span> <span data-ttu-id="c80eb-105">toolearn 進一步了解金鑰保存庫，請參閱[何謂 Azure Key Vault？](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="c80eb-105">toolearn more about Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span>

> [!NOTE]
> 1. <span data-ttu-id="c80eb-106">為了讓搭配 Azure 資源管理員虛擬機器使用的金鑰保存庫 toobe，hello **EnabledForDeployment** tootrue 必須設定金鑰保存庫上的屬性。</span><span class="sxs-lookup"><span data-stu-id="c80eb-106">In order for Key Vault toobe used with Azure Resource Manager virtual machines, hello **EnabledForDeployment** property on Key Vault must be set tootrue.</span></span> <span data-ttu-id="c80eb-107">您可以在各種用戶端中執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="c80eb-107">You can do this in various clients.</span></span>
> 2. <span data-ttu-id="c80eb-108">hello toobe 中建立的金鑰保存庫需求 hello 相同訂用帳戶和位置，如 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="c80eb-108">hello Key Vault needs toobe created in hello same subscription and location as hello Virtual Machine.</span></span>
>
>

## <a name="use-powershell-tooset-up-key-vault"></a><span data-ttu-id="c80eb-109">使用 PowerShell tooset 金鑰保存庫註冊</span><span class="sxs-lookup"><span data-stu-id="c80eb-109">Use PowerShell tooset up Key Vault</span></span>
<span data-ttu-id="c80eb-110">toocreate 金鑰保存庫使用 PowerShell，請參閱[開始使用 Azure 金鑰保存庫](../../key-vault/key-vault-get-started.md#vault)。</span><span class="sxs-lookup"><span data-stu-id="c80eb-110">toocreate a key vault by using PowerShell, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md#vault).</span></span>

<span data-ttu-id="c80eb-111">針對新的「金鑰保存庫」，您可以使用下列 PowerShell Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="c80eb-111">For new key vaults, you can use this PowerShell cmdlet:</span></span>

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -EnabledForDeployment

<span data-ttu-id="c80eb-112">針對現有的「金鑰保存庫」，您可以使用下列 PowerShell Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="c80eb-112">For existing key vaults, you can use this PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

## <a name="us-cli-tooset-up-key-vault"></a><span data-ttu-id="c80eb-113">我們 CLI tooset 金鑰保存庫註冊</span><span class="sxs-lookup"><span data-stu-id="c80eb-113">Us CLI tooset up Key Vault</span></span>
<span data-ttu-id="c80eb-114">toocreate 金鑰保存庫使用 hello 命令列介面 (CLI)，請參閱[管理金鑰保存庫使用 CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault)。</span><span class="sxs-lookup"><span data-stu-id="c80eb-114">toocreate a key vault by using hello command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="c80eb-115">CLI 中，您必須 toocreate hello 金鑰保存庫後，再指派 hello 部署原則。</span><span class="sxs-lookup"><span data-stu-id="c80eb-115">For CLI, you have toocreate hello key vault before you assign hello deployment policy.</span></span> <span data-ttu-id="c80eb-116">您可以使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="c80eb-116">You can do this by using hello following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a><span data-ttu-id="c80eb-117">使用金鑰保存庫註冊的範本 tooset</span><span class="sxs-lookup"><span data-stu-id="c80eb-117">Use templates tooset up Key Vault</span></span>
<span data-ttu-id="c80eb-118">雖然您使用範本，您需要 tooset hello`enabledForDeployment`屬性太`true`hello 金鑰保存庫資源。</span><span class="sxs-lookup"><span data-stu-id="c80eb-118">While you use a template, you need tooset hello `enabledForDeployment` property too`true` for hello Key Vault resource.</span></span>

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

<span data-ttu-id="c80eb-119">如需使用範本來建立金鑰保存庫時可以設定的其他選項，請參閱 [Create a Key Vault (建立金鑰保存庫)](https://azure.microsoft.com/documentation/templates/101-key-vault-create/)。</span><span class="sxs-lookup"><span data-stu-id="c80eb-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
