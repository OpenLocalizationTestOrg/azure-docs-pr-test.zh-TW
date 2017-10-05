---
title: "命名 Azure Data Factory 實體的規則 |Microsoft Docs"
description: "描述 Data Factory 實體的命名規則。"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: bc5e801d-0b3b-48ec-9501-bb4146ea17f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: d447bbceb4ab344e011311eaf143b20f0a0400d3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-data-factory---naming-rules"></a><span data-ttu-id="20b52-103">Azure Data Factory - 命名規則</span><span class="sxs-lookup"><span data-stu-id="20b52-103">Azure Data Factory - naming rules</span></span>
<span data-ttu-id="20b52-104">下表提供 Data Factory 購件命名規則。</span><span class="sxs-lookup"><span data-stu-id="20b52-104">The following table provides naming rules for Data Factory artifacts.</span></span>

| <span data-ttu-id="20b52-105">名稱</span><span class="sxs-lookup"><span data-stu-id="20b52-105">Name</span></span> | <span data-ttu-id="20b52-106">名稱唯一性</span><span class="sxs-lookup"><span data-stu-id="20b52-106">Name Uniqueness</span></span> | <span data-ttu-id="20b52-107">驗證檢查</span><span class="sxs-lookup"><span data-stu-id="20b52-107">Validation Checks</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="20b52-108">Data Factory</span><span class="sxs-lookup"><span data-stu-id="20b52-108">Data Factory</span></span> |<span data-ttu-id="20b52-109">在 Microsoft Azure 中是唯一的。</span><span class="sxs-lookup"><span data-stu-id="20b52-109">Unique across Microsoft Azure.</span></span> <span data-ttu-id="20b52-110">名稱不區分大小寫，亦即 `MyDF` 和 `mydf` 會指相同的 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="20b52-110">Names are case-insensitive, that is, `MyDF` and `mydf` refer to the same data factory.</span></span> |<ul><li><span data-ttu-id="20b52-111">每個 Data Factory 只會繫結至一個 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="20b52-111">Each data factory is tied to exactly one Azure subscription.</span></span></li><li><span data-ttu-id="20b52-112">物件名稱必須以字母或數字開頭，並且只能包含字母、數字和虛線 (-) 字元。</span><span class="sxs-lookup"><span data-stu-id="20b52-112">Object names must start with a letter or a number, and can contain only letters, numbers, and the dash (-) character.</span></span></li><li><span data-ttu-id="20b52-113">每個虛線 (-) 字元的前面和後面必須緊接字母或數字。</span><span class="sxs-lookup"><span data-stu-id="20b52-113">Every dash (-) character must be immediately preceded and followed by a letter or a number.</span></span> <span data-ttu-id="20b52-114">容器名稱中不允許使用連續虛線。</span><span class="sxs-lookup"><span data-stu-id="20b52-114">Consecutive dashes are not permitted in container names.</span></span></li><li><span data-ttu-id="20b52-115">名稱長度可以介於 3-63 個字元。</span><span class="sxs-lookup"><span data-stu-id="20b52-115">Name can be 3-63 characters long.</span></span></li></ul> |
| <span data-ttu-id="20b52-116">連結的服務/資料表/管線</span><span class="sxs-lookup"><span data-stu-id="20b52-116">Linked Services/Tables/Pipelines</span></span> |<span data-ttu-id="20b52-117">在 Data Factory 中是唯一的。</span><span class="sxs-lookup"><span data-stu-id="20b52-117">Unique with in a data factory.</span></span> <span data-ttu-id="20b52-118">名稱不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="20b52-118">Names are case-insensitive.</span></span> |<ul><li><span data-ttu-id="20b52-119">資料表名稱的字元數目上限︰260。</span><span class="sxs-lookup"><span data-stu-id="20b52-119">Maximum number of characters in a table name: 260.</span></span></li><li><span data-ttu-id="20b52-120">物件名稱開頭必須為字母、數字或底線 (_)。</span><span class="sxs-lookup"><span data-stu-id="20b52-120">Object names must start with a letter, number, or an underscore (_).</span></span></li><li><span data-ttu-id="20b52-121">不允許使用下列字元：“.”、“+”、“?”、“/”、“<”、”>”、”*”、”%”、”&”、”:”、”\\”</span><span class="sxs-lookup"><span data-stu-id="20b52-121">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”, ”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |
| <span data-ttu-id="20b52-122">資源群組</span><span class="sxs-lookup"><span data-stu-id="20b52-122">Resource Group</span></span> |<span data-ttu-id="20b52-123">在 Microsoft Azure 中是唯一的。</span><span class="sxs-lookup"><span data-stu-id="20b52-123">Unique across Microsoft Azure.</span></span> <span data-ttu-id="20b52-124">名稱不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="20b52-124">Names are case-insensitive.</span></span> |<ul><li><span data-ttu-id="20b52-125">字元數目上限︰1000。</span><span class="sxs-lookup"><span data-stu-id="20b52-125">Maximum number of characters: 1000.</span></span></li><li><span data-ttu-id="20b52-126">名稱可包含字母、數字及下列字元：“-”、“_”、“,” 和 “.”。</span><span class="sxs-lookup"><span data-stu-id="20b52-126">Name can contain letters, digits, and the following characters: “-”, “_”, “,” and “.”</span></span></li></ul> |

