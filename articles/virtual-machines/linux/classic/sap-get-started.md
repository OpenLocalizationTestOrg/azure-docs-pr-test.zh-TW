---
title: "在 Linux 虛擬機器上的 SAP aaaUsing |Microsoft 文件"
description: "了解如何在 Microsoft Azure 中的 Linux 虛擬機器 (VM) 上使用 SAP"
services: virtual-machines-linux,virtual-network,storage
documentationcenter: saponazure
author: MSSedusch
manager: timlt
editor: 
tags: azure-service-management
keywords: 
ms.assetid: f9cd93dc-71ad-48a4-8778-4e48aec484a6
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: campaign-page
ms.tgt_pltfrm: vm-linux
ms.workload: na
ms.date: 10/04/2016
ms.author: sedusch
ms.openlocfilehash: a805cdecb515239057e185a92bf5c4d4e707f72f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-sap-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="382f4-103">在 Azure 中的 Linux 虛擬機器上使用 SAP</span><span class="sxs-lookup"><span data-stu-id="382f4-103">Using SAP on Linux virtual machines in Azure</span></span>
<span data-ttu-id="382f4-104">雲端運算廣泛使用的名詞日漸重要內 hello IT 產業、 從小型公司向上 toolarge 和一家跨國企業。</span><span class="sxs-lookup"><span data-stu-id="382f4-104">Cloud Computing is a widely used term which is gaining more and more importance within hello IT industry, from small companies up toolarge and multinational corporations.</span></span> <span data-ttu-id="382f4-105">Microsoft Azure 為 hello 它提供了各式各樣的新的可能性的 microsoft 雲端服務平台。</span><span class="sxs-lookup"><span data-stu-id="382f4-105">Microsoft Azure is hello Cloud Services Platform from Microsoft which offers a wide spectrum of new possibilities.</span></span> <span data-ttu-id="382f4-106">現在的客戶可以 toorapidly 佈建和取消佈建應用程式當成雲端服務，因此不會限制的 tootechnical 或預算限制。</span><span class="sxs-lookup"><span data-stu-id="382f4-106">Now customers are able toorapidly provision and de-provision applications as Cloud-Services, so they are not limited tootechnical or budgeting restrictions.</span></span> <span data-ttu-id="382f4-107">而不是投入時間和預算硬體基礎結構中，公司可以專注於 hello 應用程式、 商務程序和它的優點的客戶與使用者。</span><span class="sxs-lookup"><span data-stu-id="382f4-107">Instead of investing time and budget into hardware infrastructure, companies can focus on hello application, business processes and its benefits for customers and users.</span></span>

<span data-ttu-id="382f4-108">Microsoft 透過 Microsoft Azure 虛擬機器，提供完整的基礎結構即服務 (IaaS) 平台。</span><span class="sxs-lookup"><span data-stu-id="382f4-108">With Microsoft Azure virtual machines, Microsoft offers a comprehensive Infrastructure as a Service (IaaS) platform.</span></span> <span data-ttu-id="382f4-109">Azure 虛擬機器 (IaaS) 支援以 SAP NetWeaver 為基礎的應用程式。</span><span class="sxs-lookup"><span data-stu-id="382f4-109">SAP NetWeaver based applications are supported on Azure Virtual Machines (IaaS).</span></span> <span data-ttu-id="382f4-110">下面的 hello 白皮書說明如何 tooplan 和實作 SAP NetWeaver 架構的 Windows Azure 中的虛擬機器上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="382f4-110">hello whitepapers below describe how tooplan and implement SAP NetWeaver based applications on Windows virtual machines in Azure.</span></span> <span data-ttu-id="382f4-111">您也可以在 [Windows 虛擬機器](../../windows/classic/sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)上，實作 SAP NetWeaver 應用程式。</span><span class="sxs-lookup"><span data-stu-id="382f4-111">You can also implement SAP NetWeaver based applications on [Windows virtual machines](../../windows/classic/sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-sap-get-started](../../../../includes/virtual-machines-common-classic-sap-get-started.md)]

## <a name="sap-netweaver-on-azure-suse-linux-virtual-machines"></a><span data-ttu-id="382f4-112">Azure SUSE Linux 虛擬機器上的 SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="382f4-112">SAP NetWeaver on Azure SUSE Linux Virtual Machines</span></span>
<span data-ttu-id="382f4-113">標題： aaaTesting SAP NetWeaver on Microsoft Azure SUSE Linux Vm</span><span class="sxs-lookup"><span data-stu-id="382f4-113">title: aaaTesting SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span>

<span data-ttu-id="382f4-114">摘要：目前 Azure Linux VM 上沒有執行 SAP NetWeaver 的正式 SAP 支援。</span><span class="sxs-lookup"><span data-stu-id="382f4-114">Summary: There is no official SAP support for running SAP NetWeaver on Azure Linux VMs at this point in time.</span></span> <span data-ttu-id="382f4-115">不過客戶可能會想 toodo 某些測試，或可能會考慮 toorun Azure Linux Vm 上的 SAP 示範或訓練系統，只要不需要連絡 SAP 支援。</span><span class="sxs-lookup"><span data-stu-id="382f4-115">Nevertheless customers might want toodo some testing or might consider toorun SAP demo or training systems on Azure Linux VMs as long as there is no need for contacting SAP support.</span></span> <span data-ttu-id="382f4-116">這篇文章應該可以協助執行 SAP 的 Azure SUSE Linux Vm 的設定，並提供一些基本的提示順序 tooavoid 常見的潛在問題。</span><span class="sxs-lookup"><span data-stu-id="382f4-116">This article should help setting up Azure SUSE Linux VMs for running SAP and gives some basic hints in order tooavoid common potential pitfalls.</span></span>

<span data-ttu-id="382f4-117">更新日期：2015 年 12 月</span><span class="sxs-lookup"><span data-stu-id="382f4-117">Updated: December 2015</span></span>

[<span data-ttu-id="382f4-118">可在這裡找到這份文件</span><span class="sxs-lookup"><span data-stu-id="382f4-118">This article can be found here</span></span>](../../virtual-machines-linux-sap-on-suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

