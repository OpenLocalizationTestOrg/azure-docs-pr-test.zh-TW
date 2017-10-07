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
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager-with-hello-azure-cli-10"></a><span data-ttu-id="16fb5-103">設定金鑰保存庫的虛擬機器的 Azure 資源管理員中設定以 hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="16fb5-103">Set up Key Vault for virtual machines in Azure Resource Manager with hello Azure CLI 1.0</span></span>
<span data-ttu-id="16fb5-104">Hello Azure Resource Manager 堆疊中的密碼/憑證會模型化為 hello 的金鑰保存庫的資源提供者所提供的資源。</span><span class="sxs-lookup"><span data-stu-id="16fb5-104">In hello Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by hello resource provider of Key Vault.</span></span> <span data-ttu-id="16fb5-105">toolearn 進一步了解 Azure 金鑰保存庫，請參閱[何謂 Azure Key Vault？](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="16fb5-105">toolearn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="16fb5-106">為了讓搭配 Azure 資源管理員虛擬機器使用的金鑰保存庫 toobe，hello *EnabledForDeployment* tootrue 必須設定金鑰保存庫上的屬性。</span><span class="sxs-lookup"><span data-stu-id="16fb5-106">In order for Key Vault toobe used with Azure Resource Manager virtual machines, hello *EnabledForDeployment* property on Key Vault must be set tootrue.</span></span> <span data-ttu-id="16fb5-107">您可以在各種用戶端中執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="16fb5-107">You can do this in various clients.</span></span> <span data-ttu-id="16fb5-108">本文章將示範如何使用與 Azure 虛擬機器設定金鑰保存庫 tooset。</span><span class="sxs-lookup"><span data-stu-id="16fb5-108">This article shows you how tooset up Key Vault for use with Azure Virtual Machines.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="16fb5-109">CLI 版本 toocomplete hello 工作</span><span class="sxs-lookup"><span data-stu-id="16fb5-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="16fb5-110">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本</span><span class="sxs-lookup"><span data-stu-id="16fb5-110">You can complete hello task using one of hello following CLI versions</span></span>

- <span data-ttu-id="16fb5-111">[Azure CLI 1.0](#quick-commands) – 我們 CLI hello 傳統和資源管理部署模型 （此文件）</span><span class="sxs-lookup"><span data-stu-id="16fb5-111">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="16fb5-112">[Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -hello 資源管理部署模型我們下一個層代 CLI</span><span class="sxs-lookup"><span data-stu-id="16fb5-112">[Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="use-cli-10-tooset-up-key-vault"></a><span data-ttu-id="16fb5-113">使用金鑰保存庫註冊的 CLI 1.0 tooset</span><span class="sxs-lookup"><span data-stu-id="16fb5-113">Use CLI 1.0 tooset up Key Vault</span></span>
<span data-ttu-id="16fb5-114">toocreate 金鑰保存庫使用 hello 命令列介面 (CLI)，請參閱[管理金鑰保存庫使用 CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault)。</span><span class="sxs-lookup"><span data-stu-id="16fb5-114">toocreate a key vault by using hello command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="16fb5-115">CLI 1.0 時，您必須 toocreate hello 金鑰保存庫後，再指派 hello 部署原則。</span><span class="sxs-lookup"><span data-stu-id="16fb5-115">For CLI 1.0, you have toocreate hello key vault before you assign hello deployment policy.</span></span> <span data-ttu-id="16fb5-116">然後，您可以使用下列命令的 hello 指派 hello 原則：</span><span class="sxs-lookup"><span data-stu-id="16fb5-116">You can then assign hello policy by using hello following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a><span data-ttu-id="16fb5-117">使用金鑰保存庫註冊的範本 tooset</span><span class="sxs-lookup"><span data-stu-id="16fb5-117">Use templates tooset up Key Vault</span></span>
<span data-ttu-id="16fb5-118">當您使用範本時，您需要 tooset hello`enabledForDeployment`屬性太`true`hello 金鑰保存庫資源。</span><span class="sxs-lookup"><span data-stu-id="16fb5-118">When you use a template, you need tooset hello `enabledForDeployment` property too`true` for hello Key Vault resource.</span></span>

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

<span data-ttu-id="16fb5-119">如需使用範本來建立金鑰保存庫時可以設定的其他選項，請參閱 [Create a Key Vault (建立金鑰保存庫)](https://azure.microsoft.com/documentation/templates/101-key-vault-create/)。</span><span class="sxs-lookup"><span data-stu-id="16fb5-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
