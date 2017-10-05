---
title: "適用於 PostgreSQL 的 Azure 資料庫中的限制 | Microsoft Docs"
description: "描述適用於 PostgreSQL 的 Azure 資料庫中的限制。"
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.topic: article
ms.date: 06/01/2017
ms.openlocfilehash: 38988fc5c0dc05331ea078534cd1a05e9eca2493
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="limitations-in-azure-database-for-postgresql"></a><span data-ttu-id="657c7-103">適用於 PostgreSQL 的 Azure 資料庫中的限制</span><span class="sxs-lookup"><span data-stu-id="657c7-103">Limitations in Azure Database for PostgreSQL</span></span>
<span data-ttu-id="657c7-104">適用於 PostgreSQL 的 Azure 資料庫服務目前為公開預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="657c7-104">The Azure Database for PostgreSQL service is in public preview.</span></span> <span data-ttu-id="657c7-105">下列各節說明資料庫服務中的容量和功能限制。</span><span class="sxs-lookup"><span data-stu-id="657c7-105">The following sections describe capacity and functional limits in the database service.</span></span>

## <a name="service-tier-maximums"></a><span data-ttu-id="657c7-106">服務層上限</span><span class="sxs-lookup"><span data-stu-id="657c7-106">Service Tier Maximums</span></span>
<span data-ttu-id="657c7-107">適用於 PostgreSQL 的 Azure 資料庫具有多個您在建立伺服器時可從中選擇的服務層。</span><span class="sxs-lookup"><span data-stu-id="657c7-107">Azure Database for PostgreSQL has multiple service tiers you can choose from when creating a server.</span></span> <span data-ttu-id="657c7-108">如需詳細資訊，請參閱[了解每個服務層中可用的項目](concepts-service-tiers.md)。</span><span class="sxs-lookup"><span data-stu-id="657c7-108">For more information, see [Understand what’s available in each service tier](concepts-service-tiers.md).</span></span>  

<span data-ttu-id="657c7-109">在服務預覽期間，每個服務層中具有連接、計算單位及儲存體的數目上限，如下：</span><span class="sxs-lookup"><span data-stu-id="657c7-109">There is a maximum number of connections, compute units, and storage in each service tier during the service preview, as follows:</span></span> 

|                            |                   |
| :------------------------- | :---------------- |
| <span data-ttu-id="657c7-110">**連接數目上限**</span><span class="sxs-lookup"><span data-stu-id="657c7-110">**Max connections**</span></span>        |                   |
| <span data-ttu-id="657c7-111">基本的 50 個計算單位</span><span class="sxs-lookup"><span data-stu-id="657c7-111">Basic 50 Compute Units</span></span>     | <span data-ttu-id="657c7-112">50 個連接</span><span class="sxs-lookup"><span data-stu-id="657c7-112">50 connections</span></span>    |
| <span data-ttu-id="657c7-113">基本的 100 個計算單位</span><span class="sxs-lookup"><span data-stu-id="657c7-113">Basic 100 Compute Units</span></span>    | <span data-ttu-id="657c7-114">100 個連接</span><span class="sxs-lookup"><span data-stu-id="657c7-114">100 connections</span></span>   |
| <span data-ttu-id="657c7-115">標準的 100 個計算單位</span><span class="sxs-lookup"><span data-stu-id="657c7-115">Standard 100 Compute Units</span></span> | <span data-ttu-id="657c7-116">200 個連接</span><span class="sxs-lookup"><span data-stu-id="657c7-116">200 connections</span></span>   |
| <span data-ttu-id="657c7-117">標準的 200 個計算單位</span><span class="sxs-lookup"><span data-stu-id="657c7-117">Standard 200 Compute Units</span></span> | <span data-ttu-id="657c7-118">300 個連接</span><span class="sxs-lookup"><span data-stu-id="657c7-118">300 connections</span></span>   |
| <span data-ttu-id="657c7-119">標準的 400 個計算單位</span><span class="sxs-lookup"><span data-stu-id="657c7-119">Standard 400 Compute Units</span></span> | <span data-ttu-id="657c7-120">400 個連接</span><span class="sxs-lookup"><span data-stu-id="657c7-120">400 connections</span></span>   |
| <span data-ttu-id="657c7-121">標準的 800 個計算單位</span><span class="sxs-lookup"><span data-stu-id="657c7-121">Standard 800 Compute Units</span></span> | <span data-ttu-id="657c7-122">500 個連接</span><span class="sxs-lookup"><span data-stu-id="657c7-122">500 connections</span></span>   |
| <span data-ttu-id="657c7-123">**計算單位數目上限**</span><span class="sxs-lookup"><span data-stu-id="657c7-123">**Max Compute Units**</span></span>      |                   |
| <span data-ttu-id="657c7-124">基本服務層</span><span class="sxs-lookup"><span data-stu-id="657c7-124">Basic service tier</span></span>         | <span data-ttu-id="657c7-125">100 個計算單位</span><span class="sxs-lookup"><span data-stu-id="657c7-125">100 Compute Units</span></span> |
| <span data-ttu-id="657c7-126">標準服務層</span><span class="sxs-lookup"><span data-stu-id="657c7-126">Standard service tier</span></span>      | <span data-ttu-id="657c7-127">800 個計算單位</span><span class="sxs-lookup"><span data-stu-id="657c7-127">800 Compute Units</span></span> |
| <span data-ttu-id="657c7-128">**儲存體上限**</span><span class="sxs-lookup"><span data-stu-id="657c7-128">**Max storage**</span></span>            |                   |
| <span data-ttu-id="657c7-129">基本服務層</span><span class="sxs-lookup"><span data-stu-id="657c7-129">Basic service tier</span></span>         | <span data-ttu-id="657c7-130">1 TB</span><span class="sxs-lookup"><span data-stu-id="657c7-130">1 TB</span></span>              |
| <span data-ttu-id="657c7-131">標準服務層</span><span class="sxs-lookup"><span data-stu-id="657c7-131">Standard service tier</span></span>      | <span data-ttu-id="657c7-132">1 TB</span><span class="sxs-lookup"><span data-stu-id="657c7-132">1 TB</span></span>              |

<span data-ttu-id="657c7-133">到達太多連接時，您可能會收到下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="657c7-133">When too many connections are reached, you may receive the following error:</span></span>
> <span data-ttu-id="657c7-134">嚴重錯誤︰很抱歉，已經有太多用戶端</span><span class="sxs-lookup"><span data-stu-id="657c7-134">FATAL:  sorry, too many clients already</span></span>

## <a name="preview-functional-limitations"></a><span data-ttu-id="657c7-135">預覽功能限制</span><span class="sxs-lookup"><span data-stu-id="657c7-135">Preview functional limitations</span></span>
### <a name="scale-operations"></a><span data-ttu-id="657c7-136">調整作業</span><span class="sxs-lookup"><span data-stu-id="657c7-136">Scale operations</span></span>
1.  <span data-ttu-id="657c7-137">目前不支援跨服務層動態調整伺服器。</span><span class="sxs-lookup"><span data-stu-id="657c7-137">Dynamic scaling of servers across service tiers is currently not supported.</span></span> <span data-ttu-id="657c7-138">也就是在基本和標準服務層之間切換。</span><span class="sxs-lookup"><span data-stu-id="657c7-138">That is, switching between Basic and Standard service tiers.</span></span>
2.  <span data-ttu-id="657c7-139">目前不支援依需求在預先建立的伺服器上動態增加儲存體。</span><span class="sxs-lookup"><span data-stu-id="657c7-139">Dynamic on-demand increase of storage on pre-created server is currently not supported.</span></span>
3.  <span data-ttu-id="657c7-140">不支援減少伺服器儲存體大小。</span><span class="sxs-lookup"><span data-stu-id="657c7-140">Decreasing server storage size is not supported.</span></span>

### <a name="server-version-upgrades"></a><span data-ttu-id="657c7-141">伺服器版本升級</span><span class="sxs-lookup"><span data-stu-id="657c7-141">Server version upgrades</span></span>
- <span data-ttu-id="657c7-142">目前不支援在主要資料庫引擎版本之間進行自動轉換。</span><span class="sxs-lookup"><span data-stu-id="657c7-142">Automated migration between major database engine versions is currently not supported.</span></span>

### <a name="subscription-management"></a><span data-ttu-id="657c7-143">訂用帳戶管理</span><span class="sxs-lookup"><span data-stu-id="657c7-143">Subscription management</span></span>
- <span data-ttu-id="657c7-144">目前不支援跨訂用帳戶和資源群組動態移動預先建立的伺服器。</span><span class="sxs-lookup"><span data-stu-id="657c7-144">Dynamically moving pre-created servers across subscription and resource group is currently not supported.</span></span>

### <a name="point-in-time-restore"></a><span data-ttu-id="657c7-145">還原時間點</span><span class="sxs-lookup"><span data-stu-id="657c7-145">Point-in-time-restore</span></span>
1.  <span data-ttu-id="657c7-146">不允許還原到不同服務層和/或計算單位與儲存體大小。</span><span class="sxs-lookup"><span data-stu-id="657c7-146">Restoring to different service tier and/or Compute Units and Storage size is not allowed.</span></span>
2.  <span data-ttu-id="657c7-147">不支援還原已卸除的伺服器。</span><span class="sxs-lookup"><span data-stu-id="657c7-147">Restoring a dropped server is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="657c7-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="657c7-148">Next steps</span></span>
- <span data-ttu-id="657c7-149">了解[每個定價層層中可用的項目](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="657c7-149">Understand [What’s available in each pricing tier](concepts-service-tiers.md)</span></span>
- <span data-ttu-id="657c7-150">了解[支援的 PostgreSQL 資料庫版本](concepts-supported-versions.md)</span><span class="sxs-lookup"><span data-stu-id="657c7-150">Understand [Supported PostgreSQL Database Versions](concepts-supported-versions.md)</span></span>
- <span data-ttu-id="657c7-151">檢閱[如何使用 Azure 入口網站，在適用於 PostgreSQL 的 Azure 資料庫中備份和還原伺服器](howto-restore-server-portal.md)</span><span class="sxs-lookup"><span data-stu-id="657c7-151">Review [How To Back up and Restore a server in Azure Database for PostgreSQL using the Azure portal](howto-restore-server-portal.md)</span></span>
