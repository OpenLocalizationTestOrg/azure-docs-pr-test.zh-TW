---
title: "在 Azure 入口網站中建立 Linux VM 的 FQDN | Microsoft Docs"
description: "了解如何在 Azure 入口網站中為基於 Resource Manager 的虛擬機器建立完整格式的網域名稱或 FQDN。"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2cd6c249-a737-4a0a-b5ba-e1c09e551b30
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 49bfec791fcca3feabc4eb280cefd7faada0ea31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-fully-qualified-domain-name-in-the-azure-portal-for-a-linux-vm"></a><span data-ttu-id="1e5ac-103">在 Azure 入口網站中建立 Linux VM 的完整網域名稱</span><span class="sxs-lookup"><span data-stu-id="1e5ac-103">Create a fully qualified domain name in the Azure portal for a Linux VM</span></span>

<span data-ttu-id="1e5ac-104">在 [Azure 入口網站](https://portal.azure.com) 中建立虛擬機器 (VM) 時，會自動建立虛擬機器的公用 IP 資源。</span><span class="sxs-lookup"><span data-stu-id="1e5ac-104">When you create a virtual machine (VM) in the [Azure portal](https://portal.azure.com), a public IP resource for the virtual machine is automatically created.</span></span> <span data-ttu-id="1e5ac-105">您可以使用此 IP 位址從遠端存取 VM。</span><span class="sxs-lookup"><span data-stu-id="1e5ac-105">You use this IP address to remotely access the VM.</span></span> <span data-ttu-id="1e5ac-106">雖然入口網站不會建立 [fully qualified domain name (完整網域名稱)](https://en.wikipedia.org/wiki/Fully_qualified_domain_name)(或稱 FQDN)，但是您可以在 VM 建立之後新增一個。</span><span class="sxs-lookup"><span data-stu-id="1e5ac-106">Although the portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, you can add one once the VM is created.</span></span> <span data-ttu-id="1e5ac-107">這篇文章示範建立 DNS 名稱或 FQDN 的步驟。</span><span class="sxs-lookup"><span data-stu-id="1e5ac-107">This article demonstrates the steps to create a DNS name or FQDN.</span></span>

## <a name="create-a-fqdn"></a><span data-ttu-id="1e5ac-108">建立 FQDN</span><span class="sxs-lookup"><span data-stu-id="1e5ac-108">Create a FQDN</span></span>
<span data-ttu-id="1e5ac-109">此文章假設您已經建立一個 VM。</span><span class="sxs-lookup"><span data-stu-id="1e5ac-109">This article assumes that you have already created a VM.</span></span> <span data-ttu-id="1e5ac-110">如果需要，您可以[在入口網站中建立一個 VM](quick-create-portal.md) 或[使用 Azure CLI](quick-create-cli.md) 來建立。</span><span class="sxs-lookup"><span data-stu-id="1e5ac-110">If needed, you can [create a VM in the portal](quick-create-portal.md) or [with the Azure CLI](quick-create-cli.md).</span></span> <span data-ttu-id="1e5ac-111">在您的 VM 已啟動並執行之後，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1e5ac-111">Follow these steps once your VM is up and running:</span></span>

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

<span data-ttu-id="1e5ac-112">您現在可以使用這個 DNS 名稱 (例如搭配 `ssh azureuser@mydns.westus.cloudapp.azure.com`) 從遠端連接到 VM。</span><span class="sxs-lookup"><span data-stu-id="1e5ac-112">You can now connect remotely to the VM using this DNS name such as with `ssh azureuser@mydns.westus.cloudapp.azure.com`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e5ac-113">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1e5ac-113">Next steps</span></span>
<span data-ttu-id="1e5ac-114">既然您的 VM 已經有公用 IP 和 DNS 名稱，您便可以部署通用應用程式架構或服務，例如 nginx、MongoDB、Docker 等等。</span><span class="sxs-lookup"><span data-stu-id="1e5ac-114">Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as nginx, MongoDB, Docker, etc.</span></span>

<span data-ttu-id="1e5ac-115">您也可以進一步閱讀[使用 Resource Manager](../../azure-resource-manager/resource-group-overview.md)，以取得建置 Azure 部署的相關秘訣。</span><span class="sxs-lookup"><span data-stu-id="1e5ac-115">You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.</span></span>
