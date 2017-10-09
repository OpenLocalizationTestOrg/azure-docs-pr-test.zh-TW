---
title: "適用於 Linux 的 AAD 中的工作或學校識別 aaaCreate |Microsoft 文件"
description: "深入了解如何 toocreate 中 Azure Active Directory toouse 與 Linux 虛擬機器的工作或學校身分識別。"
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
ms.openlocfilehash: 54c3d0b0e89fe1b2d6a9b58a46776fe446ed72b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-work-or-school-identity-in-azure-active-directory-toouse-with-linux-vms"></a><span data-ttu-id="0b511-103">在 Linux Vm 與 Azure Active Directory toouse 中建立的工作或學校的身分識別</span><span class="sxs-lookup"><span data-stu-id="0b511-103">Creating a Work or School identity in Azure Active Directory toouse with Linux VMs</span></span>
<span data-ttu-id="0b511-104">如果您建立個人的 Azure 帳戶或具有個人的 MSDN 訂用帳戶並建立 hello MSDN Azure 信用額度-hello Azure 帳戶 tootake 利用使用*Microsoft 帳戶*識別 toocreate 它。</span><span class="sxs-lookup"><span data-stu-id="0b511-104">If you created a personal Azure account or have a personal MSDN subscription and created hello Azure account tootake advantage of hello MSDN Azure credits -- you used a *Microsoft account* identity toocreate it.</span></span> <span data-ttu-id="0b511-105">許多很棒的功能的 Azure--[資源群組範本](../../azure-resource-manager/resource-group-overview.md)是其中一個範例-需要工作或學校帳戶 （Azure Active Directory 管理的身分識別） toowork。</span><span class="sxs-lookup"><span data-stu-id="0b511-105">Many great features of Azure -- [resource group templates](../../azure-resource-manager/resource-group-overview.md) is one example -- require a work or school account (an identity managed by Azure Active Directory) toowork.</span></span> <span data-ttu-id="0b511-106">您可以遵循 hello 指示 toocreate 下方的 hello 您個人的 Azure 帳戶相關的最佳事項之一是，它隨附預設 Azure Active Directory 網域，您可以使用 toocreate 新的工作或學校的幸運的是，新的工作或學校帳戶您可以使用 Azure 功能需要它的帳戶。</span><span class="sxs-lookup"><span data-stu-id="0b511-106">You can follow hello instructions below toocreate a new work or school account because fortunately, one of hello best things about your personal Azure account is that it comes with a default Azure Active Directory domain that you can use toocreate a new work or school account that you can use with Azure features that require it.</span></span>

<span data-ttu-id="0b511-107">然而，最近的變更可讓可能 toomanage 訂用帳戶使用 hello 的 Azure 帳戶的任何類型`azure login`所述的互動式登入方法[這裡](../../xplat-cli-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="0b511-107">However, recent changes make it possible toomanage your subscription with any type of Azure account using hello `azure login` interactive login method described [here](../../xplat-cli-connect.md).</span></span> <span data-ttu-id="0b511-108">您可以使用該機制，或您可以依照接下來的 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="0b511-108">You can either use that mechanism, or you can follow hello instructions that follow.</span></span> <span data-ttu-id="0b511-109">您也可以[建立工作或學校的身分識別中使用 Windows Vm 的 Azure Active Directory toouse](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="0b511-109">You can also [create a work or school identity in Azure Active Directory toouse with Windows VMs](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

[!INCLUDE [virtual-machines-common-create-aad-work-id](../../../includes/virtual-machines-common-create-aad-work-id.md)]

