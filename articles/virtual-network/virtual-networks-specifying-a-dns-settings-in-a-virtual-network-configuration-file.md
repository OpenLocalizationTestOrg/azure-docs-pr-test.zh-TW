---
title: "aaaSpecifying 虛擬網路組態檔中的 DNS 設定 |Microsoft 文件"
description: "如何使用虛擬網路組態的虛擬網路中的 toochange DNS 伺服器設定檔案中 hello 傳統部署模型"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a8905927-92ac-42b5-8c33-8e42c000692c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.openlocfilehash: d53a658773e1c930b5a28a701db0be9edd26565e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-dns-settings-in-a-virtual-network-configuration-file"></a><span data-ttu-id="6a26e-103">指定虛擬網路組態檔中的 DNS 設定</span><span class="sxs-lookup"><span data-stu-id="6a26e-103">Specifying DNS settings in a virtual network configuration file</span></span>
<span data-ttu-id="6a26e-104">網路組態檔有兩個項目，您可以使用 toospecify 網域名稱系統 (DNS) 設定： **DnsServers**和**DnsServerRef**。</span><span class="sxs-lookup"><span data-stu-id="6a26e-104">A network configuration file has two elements that you can use toospecify Domain Name System (DNS) settings: **DnsServers** and **DnsServerRef**.</span></span> <span data-ttu-id="6a26e-105">您可以藉由指定其 IP 位址新增的 DNS 伺服器清單，並參考名稱 toohello **DnsServers**項目。</span><span class="sxs-lookup"><span data-stu-id="6a26e-105">You can add a list of DNS servers by specifying their IP addresses and reference names toohello **DnsServers** element.</span></span> <span data-ttu-id="6a26e-106">然後您可以使用**DnsServerRef**元素 toospecify hello DnsServers 元素從哪一個 DNS 伺服器項目用於您的虛擬網路內的不同網站。</span><span class="sxs-lookup"><span data-stu-id="6a26e-106">You can then use a **DnsServerRef** element toospecify which DNS server entries from hello DnsServers element are used for different network sites within your virtual network.</span></span>

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="6a26e-107">本文涵蓋 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="6a26e-107">This article covers hello classic deployment model.</span></span>

<span data-ttu-id="6a26e-108">hello 網路組態檔可能包含下列項目 hello。</span><span class="sxs-lookup"><span data-stu-id="6a26e-108">hello network configuration file may contain hello following elements.</span></span> <span data-ttu-id="6a26e-109">每個項目的 hello 標題為連結的 tooa 頁面，提供其他有關 hello 元素值設定。</span><span class="sxs-lookup"><span data-stu-id="6a26e-109">hello title of each element is linked tooa page that provides additional information about hello element value settings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6a26e-110">如需如何 tooconfigure hello 網路組態檔的資訊，請參閱[設定虛擬網路使用網路組態檔](virtual-networks-using-network-configuration-file.md)。</span><span class="sxs-lookup"><span data-stu-id="6a26e-110">For information about how tooconfigure hello network configuration file, see [Configure a Virtual Network Using a Network Configuration File](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="6a26e-111">如需 hello 網路組態檔中所包含的每個項目的資訊，請參閱[Azure 虛擬網路組態結構描述](https://msdn.microsoft.com/library/azure/jj157100.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6a26e-111">For information about each element contained in hello network configuration file, see [Azure Virtual Network Configuration Schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
> 
> 

[<span data-ttu-id="6a26e-112">Dns 項目</span><span class="sxs-lookup"><span data-stu-id="6a26e-112">Dns Element</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

    <Dns>
      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>
    </Dns>

> [!WARNING]
> <span data-ttu-id="6a26e-113">hello**名稱**中 hello 屬性**DnsServer**項目只用來做為參考 hello **DnsServerRef**項目。</span><span class="sxs-lookup"><span data-stu-id="6a26e-113">hello **name** attribute in hello **DnsServer** element is used only as a reference for hello **DnsServerRef** element.</span></span> <span data-ttu-id="6a26e-114">它不代表 hello hello DNS 伺服器的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="6a26e-114">It does not represent hello host name for hello DNS server.</span></span> <span data-ttu-id="6a26e-115">每個**DnsServer**屬性值必須是唯一的 hello 整個 Microsoft Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6a26e-115">Each **DnsServer** attribute value must be unique across hello entire Microsoft Azure subscription</span></span>
> 
> 

[<span data-ttu-id="6a26e-116">Virtual Network Sites 項目</span><span class="sxs-lookup"><span data-stu-id="6a26e-116">Virtual Network Sites Element</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

    <DnsServersRef>
      <DnsServerRef name="ID1" />
      <DnsServerRef name="ID2" />
      <DnsServerRef name="ID3" />
    </DnsServersRef>

> [!NOTE]
> <span data-ttu-id="6a26e-117">在順序 toospecify hello Virtual Network Sites 項目這項設定，它必須先在 hello DNS 項目中定義。</span><span class="sxs-lookup"><span data-stu-id="6a26e-117">In order toospecify this setting for hello Virtual Network Sites element, it must be previously defined in hello DNS element.</span></span> <span data-ttu-id="6a26e-118">hello DnsServerRef*名稱*在 hello Virtual Network Sites 項目必須參考 tooa 名稱值 hello DNS 元素中指定的 DnsServer*名稱*。</span><span class="sxs-lookup"><span data-stu-id="6a26e-118">hello DnsServerRef *name* in hello Virtual Network Sites element must refer tooa name value specified in hello DNS element for DnsServer *name*.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="6a26e-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6a26e-119">Next steps</span></span>
* <span data-ttu-id="6a26e-120">了解 hello [Azure 虛擬網路組態結構描述](http://go.microsoft.com/fwlink/?LinkId=248093)。</span><span class="sxs-lookup"><span data-stu-id="6a26e-120">Understand hello [Azure Virtual Network Configuration Schema](http://go.microsoft.com/fwlink/?LinkId=248093).</span></span>
* <span data-ttu-id="6a26e-121">了解 hello [Azure 服務組態結構描述](https://msdn.microsoft.com/library/windowsazure/ee758710)。</span><span class="sxs-lookup"><span data-stu-id="6a26e-121">Understand hello [Azure Service Configuration Schema](https://msdn.microsoft.com/library/windowsazure/ee758710).</span></span>
* <span data-ttu-id="6a26e-122">[使用網路組態檔設定虛擬網路](virtual-networks-using-network-configuration-file.md)</span><span class="sxs-lookup"><span data-stu-id="6a26e-122">[Configure a virtual network using Network configuration files](virtual-networks-using-network-configuration-file.md).</span></span>

