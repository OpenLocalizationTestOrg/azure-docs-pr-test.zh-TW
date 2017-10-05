---
title: "在 Linux 虛擬機器上使用 SAP | Microsoft Docs"
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
ms.openlocfilehash: 078865245989578d17b6eb0b59b379aa2056f31c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="using-sap-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="bfd17-103">在 Azure 中的 Linux 虛擬機器上使用 SAP</span><span class="sxs-lookup"><span data-stu-id="bfd17-103">Using SAP on Linux virtual machines in Azure</span></span>
<span data-ttu-id="bfd17-104">雲端運算這個廣泛使用的名詞已日益受到 IT 產業的重視，不論是小型公司、大型公司還是跨國企業都是如此。</span><span class="sxs-lookup"><span data-stu-id="bfd17-104">Cloud Computing is a widely used term which is gaining more and more importance within the IT industry, from small companies up to large and multinational corporations.</span></span> <span data-ttu-id="bfd17-105">Microsoft Azure 是 Microsoft 所推出的雲端服務平台，可提供各式各樣的新契機。</span><span class="sxs-lookup"><span data-stu-id="bfd17-105">Microsoft Azure is the Cloud Services Platform from Microsoft which offers a wide spectrum of new possibilities.</span></span> <span data-ttu-id="bfd17-106">客戶現在既能將應用程式快速佈建為雲端服務，也能快速取消佈建，因此不會再受到技術或預算所限制。</span><span class="sxs-lookup"><span data-stu-id="bfd17-106">Now customers are able to rapidly provision and de-provision applications as Cloud-Services, so they are not limited to technical or budgeting restrictions.</span></span> <span data-ttu-id="bfd17-107">與其在硬體基礎結構投入時間和預算，公司寧可專注於應用程式、商業流程及其帶給客戶和使用者的優點。</span><span class="sxs-lookup"><span data-stu-id="bfd17-107">Instead of investing time and budget into hardware infrastructure, companies can focus on the application, business processes and its benefits for customers and users.</span></span>

<span data-ttu-id="bfd17-108">Microsoft 透過 Microsoft Azure 虛擬機器，提供完整的基礎結構即服務 (IaaS) 平台。</span><span class="sxs-lookup"><span data-stu-id="bfd17-108">With Microsoft Azure virtual machines, Microsoft offers a comprehensive Infrastructure as a Service (IaaS) platform.</span></span> <span data-ttu-id="bfd17-109">Azure 虛擬機器 (IaaS) 支援以 SAP NetWeaver 為基礎的應用程式。</span><span class="sxs-lookup"><span data-stu-id="bfd17-109">SAP NetWeaver based applications are supported on Azure Virtual Machines (IaaS).</span></span> <span data-ttu-id="bfd17-110">下列白皮書說明如何在 Azure 中的 Windows 虛擬機器上，規劃及實作 SAP NetWeaver 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="bfd17-110">The whitepapers below describe how to plan and implement SAP NetWeaver based applications on Windows virtual machines in Azure.</span></span> <span data-ttu-id="bfd17-111">您也可以在 [Windows 虛擬機器](../../windows/classic/sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)上，實作 SAP NetWeaver 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bfd17-111">You can also implement SAP NetWeaver based applications on [Windows virtual machines](../../windows/classic/sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-sap-get-started](../../../../includes/virtual-machines-common-classic-sap-get-started.md)]

## <a name="sap-netweaver-on-azure-suse-linux-virtual-machines"></a><span data-ttu-id="bfd17-112">Azure SUSE Linux 虛擬機器上的 SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="bfd17-112">SAP NetWeaver on Azure SUSE Linux Virtual Machines</span></span>
<span data-ttu-id="bfd17-113">標題：在 Microsoft Azure SUSE Linux VM 上測試 SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="bfd17-113">Title: Testing SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span>

<span data-ttu-id="bfd17-114">摘要：目前 Azure Linux VM 上沒有執行 SAP NetWeaver 的正式 SAP 支援。</span><span class="sxs-lookup"><span data-stu-id="bfd17-114">Summary: There is no official SAP support for running SAP NetWeaver on Azure Linux VMs at this point in time.</span></span> <span data-ttu-id="bfd17-115">不過客戶可能想要執行一些測試，或可能考慮在 Azure Linux VM 上執行 SAP 示範或訓練系統，只要不需要連絡 SAP 支援。</span><span class="sxs-lookup"><span data-stu-id="bfd17-115">Nevertheless customers might want to do some testing or might consider to run SAP demo or training systems on Azure Linux VMs as long as there is no need for contacting SAP support.</span></span> <span data-ttu-id="bfd17-116">本文章應有助於設定執行 SAP 的 Azure SUSE Linux VM，並提供一些基本的提示，以避免常見的潛在問題。</span><span class="sxs-lookup"><span data-stu-id="bfd17-116">This article should help setting up Azure SUSE Linux VMs for running SAP and gives some basic hints in order to avoid common potential pitfalls.</span></span>

<span data-ttu-id="bfd17-117">更新日期：2015 年 12 月</span><span class="sxs-lookup"><span data-stu-id="bfd17-117">Updated: December 2015</span></span>

[<span data-ttu-id="bfd17-118">可在這裡找到這份文件</span><span class="sxs-lookup"><span data-stu-id="bfd17-118">This article can be found here</span></span>](../../virtual-machines-linux-sap-on-suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

