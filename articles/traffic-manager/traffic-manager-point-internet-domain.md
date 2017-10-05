---
title: "將公司網際網路網域指向流量管理員網域名稱 | Microsoft Docs"
description: "本文將協助您將公司網域名稱指向流量管理員網域名稱。"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 29822946-2d45-4434-ba47-fc180a445cc3
ms.service: traffic-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: kumud
ms.openlocfilehash: 0322b3510cfd4f94031d8c1db8f1cc032b997fa8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="point-a-company-internet-domain-to-an-azure-traffic-manager-domain"></a><span data-ttu-id="ab4c8-103">將公司網際網路網域指向 Azure 流量管理員網域</span><span class="sxs-lookup"><span data-stu-id="ab4c8-103">Point a company Internet domain to an Azure Traffic Manager domain</span></span>

<span data-ttu-id="ab4c8-104">當您建立流量管理員設定檔時，Azure 會自動為該設定檔指派 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="ab4c8-104">When you create a Traffic Manager profile, Azure automatically assigns a DNS name for that profile.</span></span> <span data-ttu-id="ab4c8-105">若要使用來自 DNS 區域的名稱，建立對應至流量管理員設定檔網域名稱的 CNAME DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="ab4c8-105">To use a name from your DNS zone, create a CNAME DNS record that maps to the domain name of your Traffic Manager profile.</span></span> <span data-ttu-id="ab4c8-106">您可以在流量管理員設定檔的 [組態] 頁面上的 [一般]  區段找到流量管理員網域名稱。</span><span class="sxs-lookup"><span data-stu-id="ab4c8-106">You can find the Traffic Manager domain name in the **General** section on the Configuration page of the Traffic Manager profile.</span></span>

<span data-ttu-id="ab4c8-107">例如，若要將名稱 www.contoso.com 指向流量管理員 DNS 名稱 contoso.trafficmanager.net，您會建立下列 DNS 資源記錄：</span><span class="sxs-lookup"><span data-stu-id="ab4c8-107">For example, to point name www.contoso.com to the Traffic Manager DNS name contoso.trafficmanager.net, you would create the following DNS resource record:</span></span>

    www.contoso.com IN CNAME contoso.trafficmanager.net

<span data-ttu-id="ab4c8-108">進入 www.contoso.com 的所有流量要求會被導向至 contoso.trafficmanager.net。</span><span class="sxs-lookup"><span data-stu-id="ab4c8-108">All traffic requests to *www.contoso.com* get directed to *contoso.trafficmanager.net*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ab4c8-109">您無法將第二層網域 (例如 *contoso.com*) 指向流量管理員網域。</span><span class="sxs-lookup"><span data-stu-id="ab4c8-109">You cannot point a second-level domain, such as *contoso.com*, to the Traffic Manager domain.</span></span> <span data-ttu-id="ab4c8-110">DNS 通訊協定標準不允許第二層網域名稱的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="ab4c8-110">DNS protocol standards do not allow CNAME records for second-level domain names.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab4c8-111">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ab4c8-111">Next steps</span></span>

* [<span data-ttu-id="ab4c8-112">流量管理員路由方法</span><span class="sxs-lookup"><span data-stu-id="ab4c8-112">Traffic Manager routing methods</span></span>](traffic-manager-routing-methods.md)
* [<span data-ttu-id="ab4c8-113">流量管理員 - 停用、啟用或刪除設定檔</span><span class="sxs-lookup"><span data-stu-id="ab4c8-113">Traffic Manager - Disable, enable or delete a profile</span></span>](disable-enable-or-delete-a-profile.md)
* [<span data-ttu-id="ab4c8-114">流量管理員 - 停用或啟用端點</span><span class="sxs-lookup"><span data-stu-id="ab4c8-114">Traffic Manager - Disable or enable an endpoint</span></span>](disable-or-enable-an-endpoint.md)
