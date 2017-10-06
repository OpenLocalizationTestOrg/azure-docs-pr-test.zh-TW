---
title: "在 Azure 網路監看員 aaaIntroduction toosecurity 群組檢視 |Microsoft 文件"
description: "此頁面提供 hello 網路監看員安全性檢視功能的概觀"
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
ms.openlocfilehash: c2f6dbbffd0aedbb9db4b69d1758f2e66dd7abb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonetwork-security-group-view-in-azure-network-watcher"></a><span data-ttu-id="ef755-103">簡介 toonetwork 安全性在 Azure 網路監看員的群組檢視</span><span class="sxs-lookup"><span data-stu-id="ef755-103">Introduction toonetwork security group view in Azure Network Watcher</span></span>

<span data-ttu-id="ef755-104">網路安全性群組會在子網路層級或 NIC 層級產生關聯。</span><span class="sxs-lookup"><span data-stu-id="ef755-104">Network Security groups are associated at a subnet level or at a NIC level.</span></span> <span data-ttu-id="ef755-105">當關聯的子網路層級，它會套用 hello 子網路中的 tooall hello VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="ef755-105">When associated at a subnet level, it applies tooall hello VM instances in hello subnet.</span></span> <span data-ttu-id="ef755-106">網路安全性群組檢視會傳回所有設定的 hello Nsg 在 NIC 和子網路的層級，提供深入了解 hello 組態的虛擬機器關聯的規則。</span><span class="sxs-lookup"><span data-stu-id="ef755-106">Network Security Group view returns all hello configured NSGs and rules that are associated at a NIC and subnet level for a virtual machine providing insight into hello configuration.</span></span> <span data-ttu-id="ef755-107">此外，hello 有效的安全性規則會傳回每個 VM 中的 hello Nic。</span><span class="sxs-lookup"><span data-stu-id="ef755-107">In addition, hello effective security rules are returned for each of hello NICs in a VM.</span></span> <span data-ttu-id="ef755-108">使用 [網路安全性群組] 檢視，您就可以評估 VM 的網路弱點，例如開啟的連接埠。</span><span class="sxs-lookup"><span data-stu-id="ef755-108">Using Network Security Group view, you can assess a VM for network vulnerabilities such as open ports.</span></span> <span data-ttu-id="ef755-109">您也可以驗證您的網路安全性群組是否正常運作根據如果[hello 之間的比較設定和 hello 有效的安全性規則](network-watcher-nsg-auditing-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="ef755-109">You can also validate if your Network Security Group is working as expected based on a [comparison between hello configured and hello effective security rules](network-watcher-nsg-auditing-powershell.md).</span></span>

<span data-ttu-id="ef755-110">更大範圍的使用案例為安全性合規性與稽核。</span><span class="sxs-lookup"><span data-stu-id="ef755-110">A more extended use case is in security compliance and auditing.</span></span> <span data-ttu-id="ef755-111">您可以定義一組規定的安全性規則，以做為控管組織安全性的模型。</span><span class="sxs-lookup"><span data-stu-id="ef755-111">You can define a prescriptive set of security rules as a model for security governance in your organization.</span></span> <span data-ttu-id="ef755-112">定期的相容性稽核可實作於程式設計的方式，藉由比較 hello 精準規則 hello 有效規則 hello Vm 網路中的每個。</span><span class="sxs-lookup"><span data-stu-id="ef755-112">A periodic compliance audit can be implemented in a programmatic way by comparing hello prescriptive rules with hello effective rules for each of hello VMs in your network.</span></span>

<span data-ttu-id="ef755-113">Hello 入口網站的規則會除以有效、 子網路、 網路介面和預設值。</span><span class="sxs-lookup"><span data-stu-id="ef755-113">In hello portal rules are divided by Effective, Subnet, Network Interface, and Default.</span></span> <span data-ttu-id="ef755-114">這可讓您簡單檢視 hello 套用規則 tooa 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ef755-114">This provides a simple view into hello rules applied tooa virtual machine.</span></span> <span data-ttu-id="ef755-115">下載 按鈕會提供 tooeasily 下載到 CSV 檔案中所有的 hello 安全性規則，不論 hello 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ef755-115">A download button is provided tooeasily download all hello security rules no matter hello tab into a CSV file.</span></span>

![安全性群組檢視][1]

<span data-ttu-id="ef755-117">選取規則和 tooshow hello 網路安全性群組以及來源和目的地首碼的新刀鋒視窗會開啟。</span><span class="sxs-lookup"><span data-stu-id="ef755-117">Rules can be selected and a new blade opens up tooshow hello Network Security Group and source and destination prefixes.</span></span> <span data-ttu-id="ef755-118">從這個刀鋒視窗中您可以瀏覽直接 toohello 網路安全性群組資源。</span><span class="sxs-lookup"><span data-stu-id="ef755-118">From this blade you can navigate directly toohello Network Security Group resource.</span></span>

![向下鑽研][2]

### <a name="next-steps"></a><span data-ttu-id="ef755-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ef755-120">Next steps</span></span>

<span data-ttu-id="ef755-121">了解如何 tooaudit 您的網路安全性群組設定造訪[稽核網路安全性群組設定使用 PowerShell](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="ef755-121">Learn how tooaudit your Network Security Group settings by visiting [Audit Network Security Group settings with PowerShell](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-security-group-view-overview/securitygroupview.png
[2]: ./media/network-watcher-security-group-view-overview/figure1.png









