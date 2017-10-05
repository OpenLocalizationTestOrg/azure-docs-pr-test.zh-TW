---
title: "Azure 網路監看員中的安全性群組檢視簡介 | Microsoft Docs"
description: "本頁提供網路監看員安全性檢視功能的概觀"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: ad27ab85-9d84-4759-b2b9-e861ef8ea8d8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 2c581a2d152a6d3f16de8f249e27a426aa9f844f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-network-security-group-view-in-azure-network-watcher"></a><span data-ttu-id="adef5-103">Azure 網路監看員中的網路安全性群組檢視簡介</span><span class="sxs-lookup"><span data-stu-id="adef5-103">Introduction to network security group view in Azure Network Watcher</span></span>

<span data-ttu-id="adef5-104">網路安全性群組會在子網路層級或 NIC 層級產生關聯。</span><span class="sxs-lookup"><span data-stu-id="adef5-104">Network Security groups are associated at a subnet level or at a NIC level.</span></span> <span data-ttu-id="adef5-105">若在子網路層級產生關聯，它會套用至子網路中的所有 VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="adef5-105">When associated at a subnet level, it applies to all the VM instances in the subnet.</span></span> <span data-ttu-id="adef5-106">網路安全性群組檢視會針對虛擬機器傳回所有於 NIC 和子網路層級產生關聯的已設定 NSG 和規則，提供設定的深入解析。</span><span class="sxs-lookup"><span data-stu-id="adef5-106">Network Security Group view returns all the configured NSGs and rules that are associated at a NIC and subnet level for a virtual machine providing insight into the configuration.</span></span> <span data-ttu-id="adef5-107">此外，VM 中的每個 NIC 也會傳回有效的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="adef5-107">In addition, the effective security rules are returned for each of the NICs in a VM.</span></span> <span data-ttu-id="adef5-108">使用 [網路安全性群組] 檢視，您就可以評估 VM 的網路弱點，例如開啟的連接埠。</span><span class="sxs-lookup"><span data-stu-id="adef5-108">Using Network Security Group view, you can assess a VM for network vulnerabilities such as open ports.</span></span> <span data-ttu-id="adef5-109">您也可以根據[所設定的安全性規則和有效安全性規則之間的比較](network-watcher-nsg-auditing-powershell.md)，驗證網路安全性群組是否如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="adef5-109">You can also validate if your Network Security Group is working as expected based on a [comparison between the configured and the effective security rules](network-watcher-nsg-auditing-powershell.md).</span></span>

<span data-ttu-id="adef5-110">更大範圍的使用案例為安全性合規性與稽核。</span><span class="sxs-lookup"><span data-stu-id="adef5-110">A more extended use case is in security compliance and auditing.</span></span> <span data-ttu-id="adef5-111">您可以定義一組規定的安全性規則，以做為控管組織安全性的模型。</span><span class="sxs-lookup"><span data-stu-id="adef5-111">You can define a prescriptive set of security rules as a model for security governance in your organization.</span></span> <span data-ttu-id="adef5-112">藉由比較網路中每個 VM 的規定規則和有效規則，即可以程式設計方式實作定期合規性稽核。</span><span class="sxs-lookup"><span data-stu-id="adef5-112">A periodic compliance audit can be implemented in a programmatic way by comparing the prescriptive rules with the effective rules for each of the VMs in your network.</span></span>

<span data-ttu-id="adef5-113">在入口網站中，規則分為「有效」、「子網路」、「網路介面」和「預設」。</span><span class="sxs-lookup"><span data-stu-id="adef5-113">In the portal rules are divided by Effective, Subnet, Network Interface, and Default.</span></span> <span data-ttu-id="adef5-114">這可讓您簡潔地了解套用至虛擬機器的規則。</span><span class="sxs-lookup"><span data-stu-id="adef5-114">This provides a simple view into the rules applied to a virtual machine.</span></span> <span data-ttu-id="adef5-115">檢視畫面中提供了 [下載] 按鈕，以方便您輕鬆地下載所有安全性規則 (不論其標籤為何) 到 CSV 檔案中。</span><span class="sxs-lookup"><span data-stu-id="adef5-115">A download button is provided to easily download all the security rules no matter the tab into a CSV file.</span></span>

![安全性群組檢視][1]

<span data-ttu-id="adef5-117">您可以選取規則，隨即會開啟新的刀鋒視窗，顯示網路安全性群組和來源與目的地前置詞。</span><span class="sxs-lookup"><span data-stu-id="adef5-117">Rules can be selected and a new blade opens up to show the Network Security Group and source and destination prefixes.</span></span> <span data-ttu-id="adef5-118">從這個刀鋒視窗中，您可以直接瀏覽至網路安全性群組資源。</span><span class="sxs-lookup"><span data-stu-id="adef5-118">From this blade you can navigate directly to the Network Security Group resource.</span></span>

![向下鑽研][2]

### <a name="next-steps"></a><span data-ttu-id="adef5-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="adef5-120">Next steps</span></span>

<span data-ttu-id="adef5-121">瀏覽[使用 PowerShell 稽核網路安全性群組設定](network-watcher-nsg-auditing-powershell.md)，以了解如何稽核網路安全性群組設定</span><span class="sxs-lookup"><span data-stu-id="adef5-121">Learn how to audit your Network Security Group settings by visiting [Audit Network Security Group settings with PowerShell](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-security-group-view-overview/securitygroupview.png
[2]: ./media/network-watcher-security-group-view-overview/figure1.png









