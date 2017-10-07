---
title: "aaaPoint 公司網際網路網域 tooa Traffic Manager 網域名稱 |Microsoft 文件"
description: "本文將協助您點將公司網域名稱 tooa Traffic Manager 網域名稱。"
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
ms.openlocfilehash: 84c428f60a1dc70452bf957d98a68c95e0b51715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="point-a-company-internet-domain-tooan-azure-traffic-manager-domain"></a><span data-ttu-id="49724-103">點將公司網際網路網域 tooan Azure Traffic Manager 網域</span><span class="sxs-lookup"><span data-stu-id="49724-103">Point a company Internet domain tooan Azure Traffic Manager domain</span></span>

<span data-ttu-id="49724-104">當您建立流量管理員設定檔時，Azure 會自動為該設定檔指派 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="49724-104">When you create a Traffic Manager profile, Azure automatically assigns a DNS name for that profile.</span></span> <span data-ttu-id="49724-105">toouse 從您的 DNS 區域的名稱建立的 CNAME DNS 記錄，將您的 Traffic Manager 設定檔的 toohello 網域名稱對應。</span><span class="sxs-lookup"><span data-stu-id="49724-105">toouse a name from your DNS zone, create a CNAME DNS record that maps toohello domain name of your Traffic Manager profile.</span></span> <span data-ttu-id="49724-106">您可以在 hello 找到 hello Traffic Manager 網域名稱**一般**hello 組態 頁面上的 hello Traffic Manager 設定檔 > 一節。</span><span class="sxs-lookup"><span data-stu-id="49724-106">You can find hello Traffic Manager domain name in hello **General** section on hello Configuration page of hello Traffic Manager profile.</span></span>

<span data-ttu-id="49724-107">比方說，toopoint 名稱 www.contoso.com toohello Traffic Manager DNS 名稱 contoso.trafficmanager.net，您會建立下列 DNS 資源記錄的 hello:</span><span class="sxs-lookup"><span data-stu-id="49724-107">For example, toopoint name www.contoso.com toohello Traffic Manager DNS name contoso.trafficmanager.net, you would create hello following DNS resource record:</span></span>

    www.contoso.com IN CNAME contoso.trafficmanager.net

<span data-ttu-id="49724-108">所有流量都要求太*www.contoso.com*太導向*contoso.trafficmanager.net*。</span><span class="sxs-lookup"><span data-stu-id="49724-108">All traffic requests too*www.contoso.com* get directed too*contoso.trafficmanager.net*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="49724-109">您無法指向第二層網域，例如*contoso.com*，toohello Traffic Manager 網域。</span><span class="sxs-lookup"><span data-stu-id="49724-109">You cannot point a second-level domain, such as *contoso.com*, toohello Traffic Manager domain.</span></span> <span data-ttu-id="49724-110">DNS 通訊協定標準不允許第二層網域名稱的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="49724-110">DNS protocol standards do not allow CNAME records for second-level domain names.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49724-111">後續步驟</span><span class="sxs-lookup"><span data-stu-id="49724-111">Next steps</span></span>

* [<span data-ttu-id="49724-112">流量管理員路由方法</span><span class="sxs-lookup"><span data-stu-id="49724-112">Traffic Manager routing methods</span></span>](traffic-manager-routing-methods.md)
* [<span data-ttu-id="49724-113">流量管理員 - 停用、啟用或刪除設定檔</span><span class="sxs-lookup"><span data-stu-id="49724-113">Traffic Manager - Disable, enable or delete a profile</span></span>](disable-enable-or-delete-a-profile.md)
* [<span data-ttu-id="49724-114">流量管理員 - 停用或啟用端點</span><span class="sxs-lookup"><span data-stu-id="49724-114">Traffic Manager - Disable or enable an endpoint</span></span>](disable-or-enable-an-endpoint.md)
