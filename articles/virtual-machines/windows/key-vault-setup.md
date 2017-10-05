---
title: "為 Azure Resource Manager 中的 Windows VM 設定 Key Vault | Microsoft Docs"
description: "如何設定要與 Azure Resource Manager 虛擬機器搭配使用的金鑰保存庫。"
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
ms.openlocfilehash: a5083a5216efbfd76fd912ec48c2f0ec3b30c4a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="192a7-103">為 Azure Resource Manager 中的虛擬機器設定金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="192a7-103">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="192a7-104">在 Azure Resource Manager 堆疊中，密碼/憑證會被塑造成「金鑰保存庫資源提供者」所提供的資源。</span><span class="sxs-lookup"><span data-stu-id="192a7-104">In Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by the resource provider of Key Vault.</span></span> <span data-ttu-id="192a7-105">若要深入了解「金鑰保存庫」，請參閱 [什麼是 Azure 金鑰保存庫？](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="192a7-105">To learn more about Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span>

> [!NOTE]
> 1. <span data-ttu-id="192a7-106">為了讓「金鑰保存庫」能與 Azure Resource Manager 虛擬機器搭配使用，必須將「金鑰保存庫」上的 **EnabledForDeployment** 屬性設定為 true。</span><span class="sxs-lookup"><span data-stu-id="192a7-106">In order for Key Vault to be used with Azure Resource Manager virtual machines, the **EnabledForDeployment** property on Key Vault must be set to true.</span></span> <span data-ttu-id="192a7-107">您可以在各種用戶端中執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="192a7-107">You can do this in various clients.</span></span>
> 2. <span data-ttu-id="192a7-108">「金鑰保存庫」必須建立在與「虛擬機器」相同的訂用帳戶和位置中。</span><span class="sxs-lookup"><span data-stu-id="192a7-108">The Key Vault needs to be created in the same subscription and location as the Virtual Machine.</span></span>
>
>

## <a name="use-powershell-to-set-up-key-vault"></a><span data-ttu-id="192a7-109">使用 PowerShell 來設定金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="192a7-109">Use PowerShell to set up Key Vault</span></span>
<span data-ttu-id="192a7-110">若要使用 PowerShell 來建立「金鑰保存庫」，請參閱 [開始使用 Azure 金鑰保存庫](../../key-vault/key-vault-get-started.md#vault)。</span><span class="sxs-lookup"><span data-stu-id="192a7-110">To create a key vault by using PowerShell, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md#vault).</span></span>

<span data-ttu-id="192a7-111">針對新的「金鑰保存庫」，您可以使用下列 PowerShell Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="192a7-111">For new key vaults, you can use this PowerShell cmdlet:</span></span>

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -EnabledForDeployment

<span data-ttu-id="192a7-112">針對現有的「金鑰保存庫」，您可以使用下列 PowerShell Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="192a7-112">For existing key vaults, you can use this PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

## <a name="us-cli-to-set-up-key-vault"></a><span data-ttu-id="192a7-113">使用 CLI 來設定金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="192a7-113">Us CLI to set up Key Vault</span></span>
<span data-ttu-id="192a7-114">若要使用命令列介面 (CLI) 來建立金鑰保存庫，請參閱 [使用 CLI 管理金鑰保存庫](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault)。</span><span class="sxs-lookup"><span data-stu-id="192a7-114">To create a key vault by using the command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="192a7-115">若使用 CLI，您必須在您指派部署原則之前建立金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="192a7-115">For CLI, you have to create the key vault before you assign the deployment policy.</span></span> <span data-ttu-id="192a7-116">您可以使用下列命令來達成目的：</span><span class="sxs-lookup"><span data-stu-id="192a7-116">You can do this by using the following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-to-set-up-key-vault"></a><span data-ttu-id="192a7-117">使用範本來設定金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="192a7-117">Use templates to set up Key Vault</span></span>
<span data-ttu-id="192a7-118">使用範本時，您需要將「金鑰保存庫」資源的 `enabledForDeployment` 屬性設定為 `true`。</span><span class="sxs-lookup"><span data-stu-id="192a7-118">While you use a template, you need to set the `enabledForDeployment` property to `true` for the Key Vault resource.</span></span>

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

<span data-ttu-id="192a7-119">如需使用範本來建立金鑰保存庫時可以設定的其他選項，請參閱 [Create a Key Vault (建立金鑰保存庫)](https://azure.microsoft.com/documentation/templates/101-key-vault-create/)。</span><span class="sxs-lookup"><span data-stu-id="192a7-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
