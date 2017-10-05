---
title: "依國家/地區限制 Azure CDN 內容 | Microsoft Docs"
description: "了解如何使用地區篩選功能限制您的 Azure CDN 內容存取。"
services: cdn
documentationcenter: 
author: lichard
manager: akucer
editor: 
ms.assetid: 12c17cc5-28ee-4b0b-ba22-2266be2e786a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 30160088d9c770400f342e67527e1cf1cabc4f6b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="restrict-azure-cdn-content-by-country"></a><span data-ttu-id="2362a-103">依國家/地區限制 Azure CDN 內容</span><span class="sxs-lookup"><span data-stu-id="2362a-103">Restrict Azure CDN content by country</span></span>

## <a name="overview"></a><span data-ttu-id="2362a-104">概觀</span><span class="sxs-lookup"><span data-stu-id="2362a-104">Overview</span></span>
<span data-ttu-id="2362a-105">當使用者要求您的內容時，預設會提供內容，不論使用者從哪裡提出這項要求。</span><span class="sxs-lookup"><span data-stu-id="2362a-105">When a user requests your content, by default, the content is served regardless of where the user made this request from.</span></span> <span data-ttu-id="2362a-106">在某些情況下，您可能想要依國家 (地區) 限制存取您的內容。</span><span class="sxs-lookup"><span data-stu-id="2362a-106">In some cases, you may want to restrict access to your content by country.</span></span> <span data-ttu-id="2362a-107">本主題說明如何使用**地區篩選**功能設定服務，以依國家 (地區) 允許或封鎖存取。</span><span class="sxs-lookup"><span data-stu-id="2362a-107">This topic explains how to use the **Geo-Filtering** feature in order to configure the service to allow or block access by country.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2362a-108">Verizon 和 Akamai 產品提供相同地理篩選功能，不過兩者支援的國家 (地區) 代碼之間有些許差異。</span><span class="sxs-lookup"><span data-stu-id="2362a-108">The Verizon and Akamai products provide the same geo-filtering functionality but have a small difference in te country codes they support.</span></span> <span data-ttu-id="2362a-109">有關這些差異的連結，請參閱步驟 3。</span><span class="sxs-lookup"><span data-stu-id="2362a-109">See Step 3 for a link to the differences.</span></span>


<span data-ttu-id="2362a-110">如需適用於設定此類限制之考量的資訊，請參閱本主題結尾的 [考量](cdn-restrict-access-by-country.md#considerations) 一節。</span><span class="sxs-lookup"><span data-stu-id="2362a-110">For information about considerations that apply to configuring this type of restriction, see the [Considerations](cdn-restrict-access-by-country.md#considerations) section at the end of the topic.</span></span>  

![國家 (地區) 篩選](./media/cdn-filtering/cdn-country-filtering-akamai.png)

## <a name="step-1-define-the-directory-path"></a><span data-ttu-id="2362a-112">步驟 1：定義目錄路徑</span><span class="sxs-lookup"><span data-stu-id="2362a-112">Step 1: Define the directory path</span></span>
<span data-ttu-id="2362a-113">選取您在入口網站內的端點，然後尋找左邊導覽上的 [地區篩選] 索引標籤，以找到這項功能。</span><span class="sxs-lookup"><span data-stu-id="2362a-113">Select your endpoint within the portal, and find the Geo-Filtering tab on the left-hand navigation to find this feature.</span></span>

<span data-ttu-id="2362a-114">在設定國家 (地區) 篩選器時，您必須指定要允許或拒絕使用者存取之位置的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="2362a-114">When configuring a country filter, you must specify the relative path to the location to which users will be allowed or denied access.</span></span> <span data-ttu-id="2362a-115">您可以使用 "/"，或藉由指定目錄路徑 "/pictures/" 來選取資料夾，為所有檔案套用地區篩選。</span><span class="sxs-lookup"><span data-stu-id="2362a-115">You can apply geo-filtering for all your files with "/" or selected folders by specifying directory paths "/pictures/".</span></span> <span data-ttu-id="2362a-116">您也可以將地區篩選套用至單一檔案，方法是指定檔案，並保留結尾斜線 "/pictures/city.png"。</span><span class="sxs-lookup"><span data-stu-id="2362a-116">You can also apply geo-filtering to a single file by specifying the file, and leaving out the trailing slash "/pictures/city.png".</span></span>

<span data-ttu-id="2362a-117">目錄路徑篩選器範例：</span><span class="sxs-lookup"><span data-stu-id="2362a-117">Example directory path filter:</span></span>

    /                                 
    /Photos/
    /Photos/Strasbourg/
      /Photos/Strasbourg/city.png

## <a name="step-2-define-the-action-block-or-allow"></a><span data-ttu-id="2362a-118">步驟 2：定義動作：封鎖或允許</span><span class="sxs-lookup"><span data-stu-id="2362a-118">Step 2: Define the action: block or allow</span></span>
<span data-ttu-id="2362a-119">**封鎖：** 將拒絕來自指定國家 (地區) 的使用者，存取從該遞迴路徑要求的資產。</span><span class="sxs-lookup"><span data-stu-id="2362a-119">**Block:** Users from the specified countries will be denied access to assets requested from that recursive path.</span></span> <span data-ttu-id="2362a-120">若尚未設定該位置的其他國家 (地區) 篩選選項，則其他所有使用者都將允許存取。</span><span class="sxs-lookup"><span data-stu-id="2362a-120">If no other country filtering options have been configured for that location, then all other users will be allowed access.</span></span>

<span data-ttu-id="2362a-121">**允許：** 只允許來自指定國家 (地區) 的使用者存取從該遞迴路徑要求的資產。</span><span class="sxs-lookup"><span data-stu-id="2362a-121">**Allow:** Only users from the specified countries will be allowed access to assets requested from that recursive path.</span></span>

## <a name="step-3-define-the-countries"></a><span data-ttu-id="2362a-122">步驟 3：定義國家 (地區)</span><span class="sxs-lookup"><span data-stu-id="2362a-122">Step 3: Define the countries</span></span>
<span data-ttu-id="2362a-123">選取您想要封鎖或允許路徑的國家 (地區)。</span><span class="sxs-lookup"><span data-stu-id="2362a-123">Select the countries that you want to block or allow for the path.</span></span> 

<span data-ttu-id="2362a-124">例如，封鎖 /Photos/Strasbourg/ 的規則會篩選檔案，包括：</span><span class="sxs-lookup"><span data-stu-id="2362a-124">For example, the rule of blocking /Photos/Strasbourg/ will filter files including:</span></span>

    http://<endpoint>.azureedge.net/Photos/Strasbourg/1000.jpg
    http://<endpoint>.azureedge.net/Photos/Strasbourg/Cathedral/1000.jpg


### <a name="country-codes"></a><span data-ttu-id="2362a-125">國碼</span><span class="sxs-lookup"><span data-stu-id="2362a-125">Country codes</span></span>
<span data-ttu-id="2362a-126">**地區篩選**功能可使用國碼 (地區碼) 來定義國家 (地區)，以允許或封鎖該國家 (地區) 對受保護目錄的要求。</span><span class="sxs-lookup"><span data-stu-id="2362a-126">The **Geo-Filtering** feature uses country codes to define the countries from which a request will be allowed or blocked for a secured directory.</span></span> <span data-ttu-id="2362a-127">您可以在 [Azure CDN 國家 (地區) 代碼 (英文)](https://msdn.microsoft.com/library/mt761717.aspx) 找到國家 (地區) 代碼。</span><span class="sxs-lookup"><span data-stu-id="2362a-127">You will find the country codes in [Azure CDN  Country Codes](https://msdn.microsoft.com/library/mt761717.aspx).</span></span> 

## <span data-ttu-id="2362a-128"><a id="considerations"></a>考量</span><span class="sxs-lookup"><span data-stu-id="2362a-128"><a id="considerations"></a>Considerations</span></span>
* <span data-ttu-id="2362a-129">您對國家 (地區) 篩選組態的變更，Verizon 需要 90 分鐘，Akamai 需要數分鐘，才會生效。</span><span class="sxs-lookup"><span data-stu-id="2362a-129">It may take up to 90 minutes for Verizon, or a couple minutes with Akamai, for changes to your country filtering configuration to take effect.</span></span>
* <span data-ttu-id="2362a-130">這項功能不支援萬用字元 (例如，‘*’)。</span><span class="sxs-lookup"><span data-stu-id="2362a-130">This feature does not support wildcard characters (for example, ‘*’).</span></span>
* <span data-ttu-id="2362a-131">會將相對路徑相關聯的地區篩選組態，遞迴地套用到該路徑。</span><span class="sxs-lookup"><span data-stu-id="2362a-131">The geo-filtering configuration associated with the relative path will be applied recursively to that path.</span></span>
* <span data-ttu-id="2362a-132">只有一個規則可套用至相同的相對路徑，您無法建立指向相同之相對路徑的多個國家 (地區) 篩選。</span><span class="sxs-lookup"><span data-stu-id="2362a-132">Only one rule can be applied to the same relative path (you cannot create multiple country filters that point to the same relative path.</span></span> <span data-ttu-id="2362a-133">不過，一個資料夾可有多個國家 (地區) 篩選。</span><span class="sxs-lookup"><span data-stu-id="2362a-133">However, a folder may have multiple country filters.</span></span> <span data-ttu-id="2362a-134">這是因為國家 (地區) 篩選的遞迴本質。</span><span class="sxs-lookup"><span data-stu-id="2362a-134">This is due to the recursive nature of country filters.</span></span> <span data-ttu-id="2362a-135">換句話說，可以將不同的國家 (地區) 篩選指派給先前設定之資料夾的子資料夾。</span><span class="sxs-lookup"><span data-stu-id="2362a-135">In other words, a subfolder of a previously configured folder can be assigned a different country filter.</span></span>

