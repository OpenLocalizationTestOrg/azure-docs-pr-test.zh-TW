---
title: "aaaSpecifying 服務組態檔中的 DNS 設定 |Microsoft 文件"
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
ms.openlocfilehash: f192e33566dd8e669da04e6378a0c8e4b0b35ecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-dns-settings-in-a-service-configuration-file"></a><span data-ttu-id="a00dd-103">指定服務組態檔中的 DNS 設定</span><span class="sxs-lookup"><span data-stu-id="a00dd-103">Specifying DNS Settings in a Service Configuration File</span></span>
## <a name="dns-elements"></a><span data-ttu-id="a00dd-104">DNS 項目</span><span class="sxs-lookup"><span data-stu-id="a00dd-104">DNS elements</span></span>
<span data-ttu-id="a00dd-105">服務組態檔可能包含 DnsServers 元素與 hello hello 服務將使用的網域名稱系統 (DNS) 伺服器的 IPv4 位址的清單。</span><span class="sxs-lookup"><span data-stu-id="a00dd-105">A service configuration file may contain a DnsServers element with a list of IPv4 addresses for hello Domain Name System (DNS) servers that hello service will use.</span></span> <span data-ttu-id="a00dd-106">Hello 服務組態檔中的設定優先於 hello 網路組態檔中設定。</span><span class="sxs-lookup"><span data-stu-id="a00dd-106">Settings in hello service configuration file take precedence over settings in hello network configuration file.</span></span> <span data-ttu-id="a00dd-107">如需詳細資訊，請參閱 [Azure 服務組態結構描述 (.cscfg 檔)](https://msdn.microsoft.com/library/azure/ee758710.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a00dd-107">For more information, see [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx).</span></span>

<span data-ttu-id="a00dd-108">**NetworkConfiguration 項目**</span><span class="sxs-lookup"><span data-stu-id="a00dd-108">**NetworkConfiguration element**</span></span>

      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>

> [!WARNING]
> <span data-ttu-id="a00dd-109">hello**名稱**中 hello 屬性**DnsServer**項目作為參考名稱。</span><span class="sxs-lookup"><span data-stu-id="a00dd-109">hello **name** attribute in hello **DnsServer** element is used only as a reference name.</span></span> <span data-ttu-id="a00dd-110">它不代表 hello hello DNS 伺服器的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="a00dd-110">It does not represent hello host name for hello DNS server.</span></span> <span data-ttu-id="a00dd-111">每個**DnsServer**屬性值必須是唯一的 hello 整個 Microsoft Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a00dd-111">Each **DnsServer** attribute value must be unique across hello entire Microsoft Azure subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="a00dd-112">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a00dd-112">See Also</span></span>
[<span data-ttu-id="a00dd-113">Azure 服務組態結構描述 (.cscfg)</span><span class="sxs-lookup"><span data-stu-id="a00dd-113">Azure Service Configuration Schema (.cscfg)</span></span>](https://msdn.microsoft.com/library/windowsazure/ee758710)

[<span data-ttu-id="a00dd-114">Azure 虛擬網路組態結構描述</span><span class="sxs-lookup"><span data-stu-id="a00dd-114">Azure Virtual Network Configuration Schema</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

[<span data-ttu-id="a00dd-115">使用網路組態檔設定虛擬網路</span><span class="sxs-lookup"><span data-stu-id="a00dd-115">Configure a Virtual Network Using Network Configuration Files</span></span>](http://go.microsoft.com/fwlink/?LinkId=248094)

[<span data-ttu-id="a00dd-116">關於 hello 管理入口網站中的虛擬網路設定</span><span class="sxs-lookup"><span data-stu-id="a00dd-116">About Virtual Network settings in hello Management Portal</span></span>](http://go.microsoft.com/fwlink/?LinkId=248092)

