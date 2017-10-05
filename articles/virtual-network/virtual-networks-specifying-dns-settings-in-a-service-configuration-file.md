---
title: "指定服務組態檔中的 DNS 設定 | Microsoft Docs"
description: "使用虛擬網路的服務組態檔指定自訂的 DNS 設定"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 467a4b99-8691-40b3-b640-e25e49675c71
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/24/2016
ms.author: jdial
ms.openlocfilehash: 0fba2ea06827aff29a7a092933edb8120d668b29
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="specifying-dns-settings-in-a-service-configuration-file"></a><span data-ttu-id="c9c4b-103">指定服務組態檔中的 DNS 設定</span><span class="sxs-lookup"><span data-stu-id="c9c4b-103">Specifying DNS Settings in a Service Configuration File</span></span>
## <a name="dns-elements"></a><span data-ttu-id="c9c4b-104">DNS 項目</span><span class="sxs-lookup"><span data-stu-id="c9c4b-104">DNS elements</span></span>
<span data-ttu-id="c9c4b-105">服務組態檔可能包含 DnsServers 項目，以及服務會使用的網域名稱系統 (DNS) 伺服器的 IPv4 位址清單。</span><span class="sxs-lookup"><span data-stu-id="c9c4b-105">A service configuration file may contain a DnsServers element with a list of IPv4 addresses for the Domain Name System (DNS) servers that the service will use.</span></span> <span data-ttu-id="c9c4b-106">服務組態檔中的設定優先於網路組態檔中的設定。</span><span class="sxs-lookup"><span data-stu-id="c9c4b-106">Settings in the service configuration file take precedence over settings in the network configuration file.</span></span> <span data-ttu-id="c9c4b-107">如需詳細資訊，請參閱 [Azure 服務組態結構描述 (.cscfg 檔)](https://msdn.microsoft.com/library/azure/ee758710.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c9c4b-107">For more information, see [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx).</span></span>

<span data-ttu-id="c9c4b-108">**NetworkConfiguration 項目**</span><span class="sxs-lookup"><span data-stu-id="c9c4b-108">**NetworkConfiguration element**</span></span>

      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>

> [!WARNING]
> <span data-ttu-id="c9c4b-109">**DnsServer** 項目中的 **name** 屬性只做為參考名稱。</span><span class="sxs-lookup"><span data-stu-id="c9c4b-109">The **name** attribute in the **DnsServer** element is used only as a reference name.</span></span> <span data-ttu-id="c9c4b-110">它不代表 DNS 伺服器的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="c9c4b-110">It does not represent the host name for the DNS server.</span></span> <span data-ttu-id="c9c4b-111">每個 **DnsServer** 屬性值在整個 Microsoft Azure 訂用帳戶中必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="c9c4b-111">Each **DnsServer** attribute value must be unique across the entire Microsoft Azure subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="c9c4b-112">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c9c4b-112">See Also</span></span>
[<span data-ttu-id="c9c4b-113">Azure 服務組態結構描述 (.cscfg)</span><span class="sxs-lookup"><span data-stu-id="c9c4b-113">Azure Service Configuration Schema (.cscfg)</span></span>](https://msdn.microsoft.com/library/windowsazure/ee758710)

[<span data-ttu-id="c9c4b-114">Azure 虛擬網路組態結構描述</span><span class="sxs-lookup"><span data-stu-id="c9c4b-114">Azure Virtual Network Configuration Schema</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

[<span data-ttu-id="c9c4b-115">使用網路組態檔設定虛擬網路</span><span class="sxs-lookup"><span data-stu-id="c9c4b-115">Configure a Virtual Network Using Network Configuration Files</span></span>](http://go.microsoft.com/fwlink/?LinkId=248094)

[<span data-ttu-id="c9c4b-116">關於管理入口網站中的虛擬網路設定</span><span class="sxs-lookup"><span data-stu-id="c9c4b-116">About Virtual Network settings in the Management Portal</span></span>](http://go.microsoft.com/fwlink/?LinkId=248092)

