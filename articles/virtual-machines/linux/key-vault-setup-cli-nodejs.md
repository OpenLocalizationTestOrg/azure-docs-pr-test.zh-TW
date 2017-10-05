---
title: "使用 Azure CLI 1.0 設定 Linux VM 的 Key Vault | Microsoft Docs"
description: "如何使用 Azure CLI 1.0 設定要與 Azure Resource Manager 虛擬機器搭配使用的 Key Vault。"
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
ms.openlocfilehash: fed612a354d45f34619f2a66bd40d78740c43ac7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager-with-the-azure-cli-10"></a><span data-ttu-id="7ad4b-103">使用 Azure CLI 1.0 為 Azure Resource Manager 中的虛擬機器設定 Key Vault</span><span class="sxs-lookup"><span data-stu-id="7ad4b-103">Set up Key Vault for virtual machines in Azure Resource Manager with the Azure CLI 1.0</span></span>
<span data-ttu-id="7ad4b-104">在 Azure Resource Manager 堆疊中，密碼/憑證會被塑造成「Key Vault 資源提供者」所提供的資源。</span><span class="sxs-lookup"><span data-stu-id="7ad4b-104">In the Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by the resource provider of Key Vault.</span></span> <span data-ttu-id="7ad4b-105">若要深入了解「Azure 金鑰保存庫」，請參閱 [什麼是 Azure 金鑰保存庫？](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="7ad4b-105">To learn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="7ad4b-106">為了讓「金鑰保存庫」能與 Azure Resource Manager 虛擬機器搭配使用，必須將「金鑰保存庫」上的 *EnabledForDeployment* 屬性設定為 true。</span><span class="sxs-lookup"><span data-stu-id="7ad4b-106">In order for Key Vault to be used with Azure Resource Manager virtual machines, the *EnabledForDeployment* property on Key Vault must be set to true.</span></span> <span data-ttu-id="7ad4b-107">您可以在各種用戶端中執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="7ad4b-107">You can do this in various clients.</span></span> <span data-ttu-id="7ad4b-108">本文說明如何設定要與 Azure 虛擬機器搭配使用的 Key Vault。</span><span class="sxs-lookup"><span data-stu-id="7ad4b-108">This article shows you how to set up Key Vault for use with Azure Virtual Machines.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="7ad4b-109">用以完成工作的 CLI 版本</span><span class="sxs-lookup"><span data-stu-id="7ad4b-109">CLI versions to complete the task</span></span>
<span data-ttu-id="7ad4b-110">您可以使用下列其中一個 CLI 版本來完成工作</span><span class="sxs-lookup"><span data-stu-id="7ad4b-110">You can complete the task using one of the following CLI versions</span></span>

- <span data-ttu-id="7ad4b-111">[Azure CLI 1.0](#quick-commands) – 適用於傳統和資源管理部署模型的 CLI (本文章)</span><span class="sxs-lookup"><span data-stu-id="7ad4b-111">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="7ad4b-112">[Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - 適用於資源管理部署模型的新一代 CLI</span><span class="sxs-lookup"><span data-stu-id="7ad4b-112">[Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="use-cli-10-to-set-up-key-vault"></a><span data-ttu-id="7ad4b-113">使用 CLI 1.0 來設定 Key Vault</span><span class="sxs-lookup"><span data-stu-id="7ad4b-113">Use CLI 1.0 to set up Key Vault</span></span>
<span data-ttu-id="7ad4b-114">若要使用命令列介面 (CLI) 建立金鑰保存庫，請參閱 [使用 CLI 管理金鑰保存庫](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault)。</span><span class="sxs-lookup"><span data-stu-id="7ad4b-114">To create a key vault by using the command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="7ad4b-115">若使用 CLI 1.0，您必須在您指派部署原則之前建立金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="7ad4b-115">For CLI 1.0, you have to create the key vault before you assign the deployment policy.</span></span> <span data-ttu-id="7ad4b-116">然後，您可以使用下列命令來指派原則︰</span><span class="sxs-lookup"><span data-stu-id="7ad4b-116">You can then assign the policy by using the following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-to-set-up-key-vault"></a><span data-ttu-id="7ad4b-117">使用範本來設定金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="7ad4b-117">Use templates to set up Key Vault</span></span>
<span data-ttu-id="7ad4b-118">當您使用範本時，您需要針對金鑰保存庫資源將 `enabledForDeployment` 屬性設定為 `true`。</span><span class="sxs-lookup"><span data-stu-id="7ad4b-118">When you use a template, you need to set the `enabledForDeployment` property to `true` for the Key Vault resource.</span></span>

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

<span data-ttu-id="7ad4b-119">如需使用範本來建立金鑰保存庫時可以設定的其他選項，請參閱 [Create a Key Vault (建立金鑰保存庫)](https://azure.microsoft.com/documentation/templates/101-key-vault-create/)。</span><span class="sxs-lookup"><span data-stu-id="7ad4b-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
