---
title: "在 AAD 中針對 Linux 建立工作或學校身分識別 | Microsoft Docs"
description: "了解如何在 Azure Active Directory 中建立用於 Linux 虛擬機器的工作或學校身分識別。"
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: b0f86d77-c669-4aa1-a095-c2aa4d9105fe
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/23/2016
ms.author: rasquill
ms.openlocfilehash: 4fdb72e3eec41d66f8561baf1755aa425ac278af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="creating-a-work-or-school-identity-in-azure-active-directory-to-use-with-linux-vms"></a><span data-ttu-id="8d72e-103">在 Azure Active Directory 中建立用於 Linux VM 的工作或學校身分識別</span><span class="sxs-lookup"><span data-stu-id="8d72e-103">Creating a Work or School identity in Azure Active Directory to use with Linux VMs</span></span>
<span data-ttu-id="8d72e-104">如果您已建立個人 Azure 帳戶，或有個人 MSDN 訂用帳戶並已建立 Azure 帳戶來運用 MSDN Azure 點數 -- 即表示您已使用「Microsoft 帳戶」  身分識別建立它。</span><span class="sxs-lookup"><span data-stu-id="8d72e-104">If you created a personal Azure account or have a personal MSDN subscription and created the Azure account to take advantage of the MSDN Azure credits -- you used a *Microsoft account* identity to create it.</span></span> <span data-ttu-id="8d72e-105">Azure 有許多很棒的功能 -- 例如 [資源群組範本](../../azure-resource-manager/resource-group-overview.md) -- 需要工作或學校帳戶 (由 Azure Active Directory 管理的身分識別) 才能運作。</span><span class="sxs-lookup"><span data-stu-id="8d72e-105">Many great features of Azure -- [resource group templates](../../azure-resource-manager/resource-group-overview.md) is one example -- require a work or school account (an identity managed by Azure Active Directory) to work.</span></span> <span data-ttu-id="8d72e-106">幸運的是，預設的 Azure Active Directory 網域會提供您個人的 Azure 帳戶，讓您可以用來建立新的工作或學校帳戶，以搭配需要這類帳戶使用的 Azure 功能，因此您可以遵循下列指示來建立新的工作或學校帳戶。</span><span class="sxs-lookup"><span data-stu-id="8d72e-106">You can follow the instructions below to create a new work or school account because fortunately, one of the best things about your personal Azure account is that it comes with a default Azure Active Directory domain that you can use to create a new work or school account that you can use with Azure features that require it.</span></span>

<span data-ttu-id="8d72e-107">不過，最近的變更讓您可以使用[這裡](../../xplat-cli-connect.md)所述的 `azure login` 互動式登入方法，以任何類型的 Azure 帳戶來管理您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8d72e-107">However, recent changes make it possible to manage your subscription with any type of Azure account using the `azure login` interactive login method described [here](../../xplat-cli-connect.md).</span></span> <span data-ttu-id="8d72e-108">您可以使用同樣的機制，或者可以遵循接下來的指示。</span><span class="sxs-lookup"><span data-stu-id="8d72e-108">You can either use that mechanism, or you can follow the instructions that follow.</span></span> <span data-ttu-id="8d72e-109">也可以 [在 Azure Active Directory 中建立用於 Windows VM 的工作或學校身分識別](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="8d72e-109">You can also [create a work or school identity in Azure Active Directory to use with Windows VMs](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

[!INCLUDE [virtual-machines-common-create-aad-work-id](../../../includes/virtual-machines-common-create-aad-work-id.md)]

