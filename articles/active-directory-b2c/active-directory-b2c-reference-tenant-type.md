---
title: "Azure Active Directory B2C：區域可用性和資料存留處 | Microsoft Docs"
description: "在 Azure Active Directory B2C 租用戶 hello 類型上的主題"
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
ms.openlocfilehash: d382921fe9d62183b6d52c47d62f952dabd116c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-region-availability--data-residency"></a><span data-ttu-id="5aa27-103">Azure Active Directory B2C：區域可用性和資料存留處</span><span class="sxs-lookup"><span data-stu-id="5aa27-103">Azure Active Directory B2C: Region availability & data residency</span></span>
<span data-ttu-id="5aa27-104">區域可用性和資料 residency 是兩個非常不同的概念會分別套用 tooAzure AD B2C 於 Azure hello 其餘部分。</span><span class="sxs-lookup"><span data-stu-id="5aa27-104">Region availability and data residency are two very different concepts that apply differently tooAzure AD B2C from hello rest of Azure.</span></span> <span data-ttu-id="5aa27-105">本文將說明這些兩個概念的 hello 差異，並比較它們應如何套用與 Azure AD B2C tooAzure。</span><span class="sxs-lookup"><span data-stu-id="5aa27-105">This article will explain hello differences between these two concepts and compare how they apply tooAzure versus Azure AD B2C.</span></span>

## <a name="summary"></a><span data-ttu-id="5aa27-106">摘要</span><span class="sxs-lookup"><span data-stu-id="5aa27-106">Summary</span></span>
<span data-ttu-id="5aa27-107">是 azure AD B2C**上市全球**以 hello 選項**在美國和歐洲的資料 residency**。</span><span class="sxs-lookup"><span data-stu-id="5aa27-107">Azure AD B2C is **generally available worldwide** with hello option for **data residency in United States or Europe**.</span></span>

## <a name="concepts"></a><span data-ttu-id="5aa27-108">概念</span><span class="sxs-lookup"><span data-stu-id="5aa27-108">Concepts</span></span>
* <span data-ttu-id="5aa27-109">**區域可用性**參考 toowhere 服務是可供使用。</span><span class="sxs-lookup"><span data-stu-id="5aa27-109">**Region availability** refers toowhere a service is available for use.</span></span>
* <span data-ttu-id="5aa27-110">**資料 residency**參考 toowhere 使用者資料會儲存。</span><span class="sxs-lookup"><span data-stu-id="5aa27-110">**Data residency** refers toowhere user data is stored.</span></span>

## <a name="region-availability"></a><span data-ttu-id="5aa27-111">區域可用性</span><span class="sxs-lookup"><span data-stu-id="5aa27-111">Region availability</span></span>
<span data-ttu-id="5aa27-112">Azure AD B2C 全球皆可使用透過 hello Azure 公用雲端。</span><span class="sxs-lookup"><span data-stu-id="5aa27-112">Azure AD B2C is available worldwide via hello Azure public cloud.</span></span> 

<span data-ttu-id="5aa27-113">這不同於 hello 模型大部分其他 Azure 服務後續的結合資料 residency 與可用性。</span><span class="sxs-lookup"><span data-stu-id="5aa27-113">This differs from hello model most other Azure services follow which couple availability with data residency.</span></span> <span data-ttu-id="5aa27-114">您可以看到這兩個 Azure 中的範例[產品可用的地區](https://azure.microsoft.com/regions/services/)頁面和 hello [Active Directory B2C 定價計算機](https://azure.microsoft.com/pricing/details/active-directory-b2c/)。</span><span class="sxs-lookup"><span data-stu-id="5aa27-114">You can see examples of this in both Azure's [Products Available By Region](https://azure.microsoft.com/regions/services/) page and hello [Active Directory B2C pricing calculator](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span></span>

## <a name="data-residency"></a><span data-ttu-id="5aa27-115">資料存留處</span><span class="sxs-lookup"><span data-stu-id="5aa27-115">Data residency</span></span>
<span data-ttu-id="5aa27-116">Azure AD B2C 會將使用者資料儲存在美國或歐洲。</span><span class="sxs-lookup"><span data-stu-id="5aa27-116">Azure AD B2C stores user data in either United States or Europe.</span></span>

<span data-ttu-id="5aa27-117">資料存留處是根據[建立 Azure AD B2C 租用戶](active-directory-b2c-get-started.md)時所選取的國家/地區來決定。</span><span class="sxs-lookup"><span data-stu-id="5aa27-117">Data residency is determined based on which country/region is selected when [creating an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

![預覽租用戶的螢幕擷取畫面](./media/active-directory-b2c-reference-tenant-type/data-residency-b2c-tenant.png)

<span data-ttu-id="5aa27-119">資料所在 hello 美國境內取得下列國家/地區的 hello:</span><span class="sxs-lookup"><span data-stu-id="5aa27-119">Data resides in hello United States for hello following countries/regions:</span></span>

> <span data-ttu-id="5aa27-120">美國、加拿大、哥斯大黎加、多明尼加共和國、薩爾瓦多、瓜地馬拉、墨西哥、巴拿馬、波多黎各和千里達及托巴哥</span><span class="sxs-lookup"><span data-stu-id="5aa27-120">United States, Canada, Costa Rica, Dominican Republic, El Salvador, Guatemala, Mexico, Panama, Puerto Rico and Trinidad & Tobago</span></span>

<span data-ttu-id="5aa27-121">資料會遵循國家/地區的 hello 位於歐洲：</span><span class="sxs-lookup"><span data-stu-id="5aa27-121">Data resides in Europe for hello following countries/regions:</span></span>

> <span data-ttu-id="5aa27-122">阿爾及利亞、奧地利、亞塞拜然、巴林、白俄羅斯、比利時、保加利亞、克羅埃西亞、賽普勒斯、捷克共和國、丹麥、埃及、愛沙尼亞、芬蘭、法國、德國、希臘、匈牙利、冰島、愛爾蘭、以色列、義大利、約旦、哈薩克、肯亞、科威特、拉脫維亞、黎巴嫩、列支敦斯登、立陶宛、盧森堡、馬其頓 (FYRO)、馬爾他、蒙特內哥羅、摩洛哥、荷蘭、奈及利亞、挪威、阿曼、巴基斯坦、波蘭、葡萄牙、卡達、羅馬尼亞、俄羅斯、沙烏地阿拉伯、塞爾維亞、斯洛伐克、斯洛維尼亞、南非、西班牙、瑞典、瑞士、突尼西亞、土耳其、烏克蘭、阿拉伯聯合大公國和英國。</span><span class="sxs-lookup"><span data-stu-id="5aa27-122">Algeria, Austria, Azerbaijan, Bahrain, Belarus, Belgium, Bulgaria, Croatia, Cyprus, Czech Republic, Denmark, Egypt, Estonia, Finland, France, Germany, Greece, Hungary, Iceland, Ireland, Israel, Italy, Jordan, Kazakhstan, Kenya, Kuwait, Lativa, Lebanon, Liechtenstein, Lituania, Luxembourg, Macedonia FYRO, Malta, Montenegro, Morocco, Netherlands, Nigeria, Norway, Oman, Pakistan, Poland, Portugal, Qatar, Romania, Russia, Saudi Arabia, Serbia, Slovakia, Slovenia, South Africa, Spain, Sweden, Switzerland, Tunisia, Turkey, Ukraine, United Arab Emirates and United Kingdom.</span></span>

<span data-ttu-id="5aa27-123">hello 剩餘國家 （地區） 是 hello 處理序正在加入 toohello 清單中。</span><span class="sxs-lookup"><span data-stu-id="5aa27-123">hello remaining countries/regions are in hello process of being added toohello list.</span></span>  <span data-ttu-id="5aa27-124">現在，您仍然可以使用 Azure AD B2C 所挑選的 hello 國家/地區上述任何。</span><span class="sxs-lookup"><span data-stu-id="5aa27-124">For now, you can still use Azure AD B2C by picking any of hello countries/regions above.</span></span>

> <span data-ttu-id="5aa27-125">阿富汗、阿根廷、澳洲、巴西、智利、哥倫比亞、厄瓜多、香港特別行政區、印度、印尼、伊拉克、日本、韓國、馬來西亞、紐西蘭、巴拉圭、祕魯、菲律賓、新加坡、斯里蘭卡、台灣、泰國、烏拉圭和委內瑞拉。</span><span class="sxs-lookup"><span data-stu-id="5aa27-125">Afghanistan, Argentina, Australia, Brazil, Chile, Colombia, Ecuador, Hong Kong SAR, India, Indonesia, Iraq, Japan, Korea, Malaysia, New Zealand, Paraguay, Peru, Philippines, Singapore, Sri Lanka, Taiwan, Thailand, Uruguay and Venezuela.</span></span>

## <a name="preview-tenant"></a><span data-ttu-id="5aa27-126">預覽租用戶</span><span class="sxs-lookup"><span data-stu-id="5aa27-126">Preview tenant</span></span>
<span data-ttu-id="5aa27-127">如果您已在 Azure AD B2C 的預覽期間建立 B2C 租用戶，您的 [租用戶類型] 可能會顯示為 [預覽租用戶]。</span><span class="sxs-lookup"><span data-stu-id="5aa27-127">If you had created a B2C tenant during Azure AD B2C's preview period, it is likely that your **Tenant type** says **Preview tenant**.</span></span> <span data-ttu-id="5aa27-128">如果這是 hello 情況下，您必須使用您的租用戶，僅適用於開發和測試用途，不能用於實際執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="5aa27-128">If this is hello case, you MUST use your tenant only for development and testing purposes, and NOT for production apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5aa27-129">沒有從預覽 B2C 租用戶 tooa 生產調整 B2C 租用戶移轉路徑。</span><span class="sxs-lookup"><span data-stu-id="5aa27-129">There is no migration path from a preview B2C tenant tooa production-scale B2C tenant.</span></span> <span data-ttu-id="5aa27-130">請注意，那里已知問題時刪除預覽 B2C 租用戶和重新建立生產調整 B2C 租用戶與 hello 相同的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="5aa27-130">Note that there are known issues when you delete a preview B2C tenant and re-create a production-scale B2C tenant with hello same domain name.</span></span> <span data-ttu-id="5aa27-131">您有 toocreate 生產調整 B2C 租用戶和不同的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="5aa27-131">You have toocreate a production-scale B2C tenant with a different domain name.</span></span>


![預覽租用戶的螢幕擷取畫面](./media/active-directory-b2c-reference-tenant-type/preview-b2c-tenant.png)
