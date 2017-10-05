---
title: "Azure Active Directory B2C：區域可用性和資料存留處 | Microsoft Docs"
description: "有關 Azure Active Directory B2C 租用戶類型的主題"
services: active-directory-b2c
documentationcenter: 
author: gsacavdm
manager: krassk
editor: bryanla
ms.assetid: 8a0644da-b825-4edc-8ce9-541c3c976afb
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: gsacavdm
ms.openlocfilehash: facd66f0324e382ea7609a035de8129ba433846f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-region-availability--data-residency"></a><span data-ttu-id="8cc5f-103">Azure Active Directory B2C：區域可用性和資料存留處</span><span class="sxs-lookup"><span data-stu-id="8cc5f-103">Azure Active Directory B2C: Region availability & data residency</span></span>
<span data-ttu-id="8cc5f-104">區域可用性和資料存留處是兩個非常不同的概念，這些概念套用到 Azure AD B2C 的方式與套用到其餘 Azure 的方式不同。</span><span class="sxs-lookup"><span data-stu-id="8cc5f-104">Region availability and data residency are two very different concepts that apply differently to Azure AD B2C from the rest of Azure.</span></span> <span data-ttu-id="8cc5f-105">本文將說明這兩個概念之間的差異，並比較它們如何套用在 Azure 與 Azure AD B2C。</span><span class="sxs-lookup"><span data-stu-id="8cc5f-105">This article will explain the differences between these two concepts and compare how they apply to Azure versus Azure AD B2C.</span></span>

## <a name="summary"></a><span data-ttu-id="8cc5f-106">摘要</span><span class="sxs-lookup"><span data-stu-id="8cc5f-106">Summary</span></span>
<span data-ttu-id="8cc5f-107">Azure AD B2C 是**在全球正式運作**，具有**資料存留處在美國或歐洲**的選項。</span><span class="sxs-lookup"><span data-stu-id="8cc5f-107">Azure AD B2C is **generally available worldwide** with the option for **data residency in United States or Europe**.</span></span>

## <a name="concepts"></a><span data-ttu-id="8cc5f-108">概念</span><span class="sxs-lookup"><span data-stu-id="8cc5f-108">Concepts</span></span>
* <span data-ttu-id="8cc5f-109">「區域可用性」係指一項服務是否可供使用。</span><span class="sxs-lookup"><span data-stu-id="8cc5f-109">**Region availability** refers to where a service is available for use.</span></span>
* <span data-ttu-id="8cc5f-110">「資料存留處」係指使用者資料的儲存位置。</span><span class="sxs-lookup"><span data-stu-id="8cc5f-110">**Data residency** refers to where user data is stored.</span></span>

## <a name="region-availability"></a><span data-ttu-id="8cc5f-111">區域可用性</span><span class="sxs-lookup"><span data-stu-id="8cc5f-111">Region availability</span></span>
<span data-ttu-id="8cc5f-112">Azure AD B2C 是透過 Azure 公用雲端在全球提供使用。</span><span class="sxs-lookup"><span data-stu-id="8cc5f-112">Azure AD B2C is available worldwide via the Azure public cloud.</span></span> 

<span data-ttu-id="8cc5f-113">這與大多數其他 Azure 服務所依循的模型不同，該模型是將可用性與資料存留處結合。</span><span class="sxs-lookup"><span data-stu-id="8cc5f-113">This differs from the model most other Azure services follow which couple availability with data residency.</span></span> <span data-ttu-id="8cc5f-114">您可以在 Azure 的[依區域提供的產品](https://azure.microsoft.com/regions/services/)頁面和 [Azure Active Directory B2C 定價計算機](https://azure.microsoft.com/pricing/details/active-directory-b2c/)中看到這個的相關範例。</span><span class="sxs-lookup"><span data-stu-id="8cc5f-114">You can see examples of this in both Azure's [Products Available By Region](https://azure.microsoft.com/regions/services/) page and the [Active Directory B2C pricing calculator](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span></span>

## <a name="data-residency"></a><span data-ttu-id="8cc5f-115">資料存留處</span><span class="sxs-lookup"><span data-stu-id="8cc5f-115">Data residency</span></span>
<span data-ttu-id="8cc5f-116">Azure AD B2C 會將使用者資料儲存在美國或歐洲。</span><span class="sxs-lookup"><span data-stu-id="8cc5f-116">Azure AD B2C stores user data in either United States or Europe.</span></span>

<span data-ttu-id="8cc5f-117">資料存留處是根據[建立 Azure AD B2C 租用戶](active-directory-b2c-get-started.md)時所選取的國家/地區來決定。</span><span class="sxs-lookup"><span data-stu-id="8cc5f-117">Data residency is determined based on which country/region is selected when [creating an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

![預覽租用戶的螢幕擷取畫面](./media/active-directory-b2c-reference-tenant-type/data-residency-b2c-tenant.png)

<span data-ttu-id="8cc5f-119">針對下列國家/地區，資料會位於美國：</span><span class="sxs-lookup"><span data-stu-id="8cc5f-119">Data resides in the United States for the following countries/regions:</span></span>

> <span data-ttu-id="8cc5f-120">美國、加拿大、哥斯大黎加、多明尼加共和國、薩爾瓦多、瓜地馬拉、墨西哥、巴拿馬、波多黎各和千里達及托巴哥</span><span class="sxs-lookup"><span data-stu-id="8cc5f-120">United States, Canada, Costa Rica, Dominican Republic, El Salvador, Guatemala, Mexico, Panama, Puerto Rico and Trinidad & Tobago</span></span>

<span data-ttu-id="8cc5f-121">針對下列國家/地區，資料會位於歐洲：</span><span class="sxs-lookup"><span data-stu-id="8cc5f-121">Data resides in Europe for the following countries/regions:</span></span>

> <span data-ttu-id="8cc5f-122">阿爾及利亞、奧地利、亞塞拜然、巴林、白俄羅斯、比利時、保加利亞、克羅埃西亞、賽普勒斯、捷克共和國、丹麥、埃及、愛沙尼亞、芬蘭、法國、德國、希臘、匈牙利、冰島、愛爾蘭、以色列、義大利、約旦、哈薩克、肯亞、科威特、拉脫維亞、黎巴嫩、列支敦斯登、立陶宛、盧森堡、馬其頓 (FYRO)、馬爾他、蒙特內哥羅、摩洛哥、荷蘭、奈及利亞、挪威、阿曼、巴基斯坦、波蘭、葡萄牙、卡達、羅馬尼亞、俄羅斯、沙烏地阿拉伯、塞爾維亞、斯洛伐克、斯洛維尼亞、南非、西班牙、瑞典、瑞士、突尼西亞、土耳其、烏克蘭、阿拉伯聯合大公國和英國。</span><span class="sxs-lookup"><span data-stu-id="8cc5f-122">Algeria, Austria, Azerbaijan, Bahrain, Belarus, Belgium, Bulgaria, Croatia, Cyprus, Czech Republic, Denmark, Egypt, Estonia, Finland, France, Germany, Greece, Hungary, Iceland, Ireland, Israel, Italy, Jordan, Kazakhstan, Kenya, Kuwait, Lativa, Lebanon, Liechtenstein, Lituania, Luxembourg, Macedonia FYRO, Malta, Montenegro, Morocco, Netherlands, Nigeria, Norway, Oman, Pakistan, Poland, Portugal, Qatar, Romania, Russia, Saudi Arabia, Serbia, Slovakia, Slovenia, South Africa, Spain, Sweden, Switzerland, Tunisia, Turkey, Ukraine, United Arab Emirates and United Kingdom.</span></span>

<span data-ttu-id="8cc5f-123">其餘國家/地區正在新增到清單。</span><span class="sxs-lookup"><span data-stu-id="8cc5f-123">The remaining countries/regions are in the process of being added to the list.</span></span>  <span data-ttu-id="8cc5f-124">目前，您仍可透過挑選上述任何國家/地區來使用 Azure AD B2C。</span><span class="sxs-lookup"><span data-stu-id="8cc5f-124">For now, you can still use Azure AD B2C by picking any of the countries/regions above.</span></span>

> <span data-ttu-id="8cc5f-125">阿富汗、阿根廷、澳洲、巴西、智利、哥倫比亞、厄瓜多、香港特別行政區、印度、印尼、伊拉克、日本、韓國、馬來西亞、紐西蘭、巴拉圭、祕魯、菲律賓、新加坡、斯里蘭卡、台灣、泰國、烏拉圭和委內瑞拉。</span><span class="sxs-lookup"><span data-stu-id="8cc5f-125">Afghanistan, Argentina, Australia, Brazil, Chile, Colombia, Ecuador, Hong Kong SAR, India, Indonesia, Iraq, Japan, Korea, Malaysia, New Zealand, Paraguay, Peru, Philippines, Singapore, Sri Lanka, Taiwan, Thailand, Uruguay and Venezuela.</span></span>

## <a name="preview-tenant"></a><span data-ttu-id="8cc5f-126">預覽租用戶</span><span class="sxs-lookup"><span data-stu-id="8cc5f-126">Preview tenant</span></span>
<span data-ttu-id="8cc5f-127">如果您已在 Azure AD B2C 的預覽期間建立 B2C 租用戶，您的 [租用戶類型] 可能會顯示為 [預覽租用戶]。</span><span class="sxs-lookup"><span data-stu-id="8cc5f-127">If you had created a B2C tenant during Azure AD B2C's preview period, it is likely that your **Tenant type** says **Preview tenant**.</span></span> <span data-ttu-id="8cc5f-128">如果情況如此，您只能將租用戶用於開發和測試用途，而不能用於生產應用程式。</span><span class="sxs-lookup"><span data-stu-id="8cc5f-128">If this is the case, you MUST use your tenant only for development and testing purposes, and NOT for production apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8cc5f-129">預覽 B2C 租用戶沒有任何途徑可以移轉到生產級別 B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="8cc5f-129">There is no migration path from a preview B2C tenant to a production-scale B2C tenant.</span></span> <span data-ttu-id="8cc5f-130">請注意，當您刪除預覽 B2C 租用戶並使用相同的網域名稱重建生產級別 B2C 租用戶時，會發生已知的問題。</span><span class="sxs-lookup"><span data-stu-id="8cc5f-130">Note that there are known issues when you delete a preview B2C tenant and re-create a production-scale B2C tenant with the same domain name.</span></span> <span data-ttu-id="8cc5f-131">您必須使用不同的網域名稱建立生產級別 B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="8cc5f-131">You have to create a production-scale B2C tenant with a different domain name.</span></span>


![預覽租用戶的螢幕擷取畫面](./media/active-directory-b2c-reference-tenant-type/preview-b2c-tenant.png)
