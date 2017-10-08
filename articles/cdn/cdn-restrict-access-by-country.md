---
title: "依國家/地區的 Azure CDN 內容 aaaRestrict |Microsoft 文件"
description: "了解如何 toorestrict 存取 tooyour Azure CDN 內容使用 hello 地理篩選功能。"
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
ms.openlocfilehash: ffdd994612b6c9cfbf1a6e29d260709b4afa86e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-azure-cdn-content-by-country"></a><span data-ttu-id="089c1-103">依國家/地區限制 Azure CDN 內容</span><span class="sxs-lookup"><span data-stu-id="089c1-103">Restrict Azure CDN content by country</span></span>

## <a name="overview"></a><span data-ttu-id="089c1-104">概觀</span><span class="sxs-lookup"><span data-stu-id="089c1-104">Overview</span></span>
<span data-ttu-id="089c1-105">當使用者要求您的內容，根據預設時，會提供 hello 內容，不論 hello 使用者進行此要求的位置。</span><span class="sxs-lookup"><span data-stu-id="089c1-105">When a user requests your content, by default, hello content is served regardless of where hello user made this request from.</span></span> <span data-ttu-id="089c1-106">在某些情況下，您可以依國家/地區的 toorestrict 存取 tooyour 內容。</span><span class="sxs-lookup"><span data-stu-id="089c1-106">In some cases, you may want toorestrict access tooyour content by country.</span></span> <span data-ttu-id="089c1-107">本主題說明如何 toouse hello**地理篩選**順序 tooconfigure hello 服務 tooallow 或封鎖存取依國家/地區中的功能。</span><span class="sxs-lookup"><span data-stu-id="089c1-107">This topic explains how toouse hello **Geo-Filtering** feature in order tooconfigure hello service tooallow or block access by country.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="089c1-108">hello Verizon 和 Akamai 產品提供 hello 相同的地理篩選功能，但有 te 它們支援的國家/地區碼上有些許不同。</span><span class="sxs-lookup"><span data-stu-id="089c1-108">hello Verizon and Akamai products provide hello same geo-filtering functionality but have a small difference in te country codes they support.</span></span> <span data-ttu-id="089c1-109">針對連結 toohello 差異，請參閱步驟 3。</span><span class="sxs-lookup"><span data-stu-id="089c1-109">See Step 3 for a link toohello differences.</span></span>


<span data-ttu-id="089c1-110">如需適用於 tooconfiguring 考量這種類型的限制，請參閱 hello[考量](cdn-restrict-access-by-country.md#considerations)hello hello 主題結尾的區段。</span><span class="sxs-lookup"><span data-stu-id="089c1-110">For information about considerations that apply tooconfiguring this type of restriction, see hello [Considerations](cdn-restrict-access-by-country.md#considerations) section at hello end of hello topic.</span></span>  

![國家 (地區) 篩選](./media/cdn-filtering/cdn-country-filtering-akamai.png)

## <a name="step-1-define-hello-directory-path"></a><span data-ttu-id="089c1-112">步驟 1： 定義 hello 目錄路徑</span><span class="sxs-lookup"><span data-stu-id="089c1-112">Step 1: Define hello directory path</span></span>
<span data-ttu-id="089c1-113">選取您的端點內 hello 入口網站，並尋找 hello 地理篩選索引標籤上 hello 左側導覽 toofind 這項功能。</span><span class="sxs-lookup"><span data-stu-id="089c1-113">Select your endpoint within hello portal, and find hello Geo-Filtering tab on hello left-hand navigation toofind this feature.</span></span>

<span data-ttu-id="089c1-114">在設定的國家 （地區） 篩選器時，您必須指定將允許或拒絕存取 hello 相對路徑 toohello 位置 toowhich 的使用者。</span><span class="sxs-lookup"><span data-stu-id="089c1-114">When configuring a country filter, you must specify hello relative path toohello location toowhich users will be allowed or denied access.</span></span> <span data-ttu-id="089c1-115">您可以使用 "/"，或藉由指定目錄路徑 "/pictures/" 來選取資料夾，為所有檔案套用地區篩選。</span><span class="sxs-lookup"><span data-stu-id="089c1-115">You can apply geo-filtering for all your files with "/" or selected folders by specifying directory paths "/pictures/".</span></span> <span data-ttu-id="089c1-116">您也可以套用地理篩選 tooa 單一檔案 hello 檔案指定並留下任何 hello 結尾斜線"/ pictures/city.png"。</span><span class="sxs-lookup"><span data-stu-id="089c1-116">You can also apply geo-filtering tooa single file by specifying hello file, and leaving out hello trailing slash "/pictures/city.png".</span></span>

<span data-ttu-id="089c1-117">目錄路徑篩選器範例：</span><span class="sxs-lookup"><span data-stu-id="089c1-117">Example directory path filter:</span></span>

    /                                 
    /Photos/
    /Photos/Strasbourg/
      /Photos/Strasbourg/city.png

## <a name="step-2-define-hello-action-block-or-allow"></a><span data-ttu-id="089c1-118">步驟 2： 定義 hello 動作： 封鎖或允許</span><span class="sxs-lookup"><span data-stu-id="089c1-118">Step 2: Define hello action: block or allow</span></span>
<span data-ttu-id="089c1-119">**禁止：** hello 使用者指定的國家 （地區） 將會遭到拒絕存取 tooassets 要求從該遞迴路徑。</span><span class="sxs-lookup"><span data-stu-id="089c1-119">**Block:** Users from hello specified countries will be denied access tooassets requested from that recursive path.</span></span> <span data-ttu-id="089c1-120">若尚未設定該位置的其他國家 (地區) 篩選選項，則其他所有使用者都將允許存取。</span><span class="sxs-lookup"><span data-stu-id="089c1-120">If no other country filtering options have been configured for that location, then all other users will be allowed access.</span></span>

<span data-ttu-id="089c1-121">**允許：**只有 hello 的使用者指定的國家 （地區），都可以存取 tooassets 要求從該遞迴路徑。</span><span class="sxs-lookup"><span data-stu-id="089c1-121">**Allow:** Only users from hello specified countries will be allowed access tooassets requested from that recursive path.</span></span>

## <a name="step-3-define-hello-countries"></a><span data-ttu-id="089c1-122">步驟 3： 定義 hello 國家 （地區）</span><span class="sxs-lookup"><span data-stu-id="089c1-122">Step 3: Define hello countries</span></span>
<span data-ttu-id="089c1-123">選取您想 tooblock 或 hello 路徑允許的 hello 國家/地區。</span><span class="sxs-lookup"><span data-stu-id="089c1-123">Select hello countries that you want tooblock or allow for hello path.</span></span> 

<span data-ttu-id="089c1-124">例如，封鎖 /Photos/Strasbourg/hello 規則會篩選檔案包括：</span><span class="sxs-lookup"><span data-stu-id="089c1-124">For example, hello rule of blocking /Photos/Strasbourg/ will filter files including:</span></span>

    http://<endpoint>.azureedge.net/Photos/Strasbourg/1000.jpg
    http://<endpoint>.azureedge.net/Photos/Strasbourg/Cathedral/1000.jpg


### <a name="country-codes"></a><span data-ttu-id="089c1-125">國碼</span><span class="sxs-lookup"><span data-stu-id="089c1-125">Country codes</span></span>
<span data-ttu-id="089c1-126">hello**地理篩選**功能使用國家/地區代碼 toodefine hello 國家 （地區） 的要求將會允許或封鎖受保護的目錄。</span><span class="sxs-lookup"><span data-stu-id="089c1-126">hello **Geo-Filtering** feature uses country codes toodefine hello countries from which a request will be allowed or blocked for a secured directory.</span></span> <span data-ttu-id="089c1-127">您會發現 hello 中的國家/地區代碼[Azure CDN 國家/地區代碼](https://msdn.microsoft.com/library/mt761717.aspx)。</span><span class="sxs-lookup"><span data-stu-id="089c1-127">You will find hello country codes in [Azure CDN  Country Codes](https://msdn.microsoft.com/library/mt761717.aspx).</span></span> 

## <span data-ttu-id="089c1-128"><a id="considerations"></a>考量</span><span class="sxs-lookup"><span data-stu-id="089c1-128"><a id="considerations"></a>Considerations</span></span>
* <span data-ttu-id="089c1-129">它可能會佔用 too90 Verizon、 分鐘或幾分鐘 Akamai，以變更 tooyour 國家 （地區） 篩選組態 tootake 效果。</span><span class="sxs-lookup"><span data-stu-id="089c1-129">It may take up too90 minutes for Verizon, or a couple minutes with Akamai, for changes tooyour country filtering configuration tootake effect.</span></span>
* <span data-ttu-id="089c1-130">這項功能不支援萬用字元 (例如，‘*’)。</span><span class="sxs-lookup"><span data-stu-id="089c1-130">This feature does not support wildcard characters (for example, ‘*’).</span></span>
* <span data-ttu-id="089c1-131">hello 相對路徑相關聯的 hello 地理篩選組態將會遞迴地套用的 toothat 路徑。</span><span class="sxs-lookup"><span data-stu-id="089c1-131">hello geo-filtering configuration associated with hello relative path will be applied recursively toothat path.</span></span>
* <span data-ttu-id="089c1-132">只要一個規則可套用的 toohello 相同的相對路徑 (您無法建立多個國家 （地區） 篩選該點 toohello 相同的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="089c1-132">Only one rule can be applied toohello same relative path (you cannot create multiple country filters that point toohello same relative path.</span></span> <span data-ttu-id="089c1-133">不過，一個資料夾可有多個國家 (地區) 篩選。</span><span class="sxs-lookup"><span data-stu-id="089c1-133">However, a folder may have multiple country filters.</span></span> <span data-ttu-id="089c1-134">這是因為國家 （地區） 篩選器 toohello 遞迴性質。</span><span class="sxs-lookup"><span data-stu-id="089c1-134">This is due toohello recursive nature of country filters.</span></span> <span data-ttu-id="089c1-135">換句話說，可以將不同的國家 (地區) 篩選指派給先前設定之資料夾的子資料夾。</span><span class="sxs-lookup"><span data-stu-id="089c1-135">In other words, a subfolder of a previously configured folder can be assigned a different country filter.</span></span>

