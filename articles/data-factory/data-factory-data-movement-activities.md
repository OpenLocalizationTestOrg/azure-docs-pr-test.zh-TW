---
title: "使用複製活動來移動資料 | Microsoft Docs"
description: "了解 Data Factory 管線中的資料移動︰雲端存放區之間和內部部署與雲端之間的資料移轉。 使用「複製活動」。"
keywords: "複製資料, 資料移動, 資料移轉, 傳輸資料"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 67543a20-b7d5-4d19-8b5e-af4c1fd7bc75
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 0cefbe1303de1cfa46cc4b771c0cd3aa7819597c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-by-using-copy-activity"></a><span data-ttu-id="7ad4d-105">使用複製活動來移動資料</span><span class="sxs-lookup"><span data-stu-id="7ad4d-105">Move data by using Copy Activity</span></span>
## <a name="overview"></a><span data-ttu-id="7ad4d-106">概觀</span><span class="sxs-lookup"><span data-stu-id="7ad4d-106">Overview</span></span>
<span data-ttu-id="7ad4d-107">在 Azure Data Factory 中，您可以使用「複製活動」在內部部署與雲端資料存放區之間複製資料。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-107">In Azure Data Factory, you can use Copy Activity to copy data between on-premises and cloud data stores.</span></span> <span data-ttu-id="7ad4d-108">複製資料之後，可以將它進一步轉換及進行分析。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-108">After the data is copied, it can be further transformed and analyzed.</span></span> <span data-ttu-id="7ad4d-109">您也可以使用「複製活動」來發佈商業智慧 (BI) 及應用程式使用情況的轉換和分析結果。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-109">You can also use Copy Activity to publish transformation and analysis results for business intelligence (BI) and application consumption.</span></span>

![複製活動的角色](media/data-factory-data-movement-activities/copy-activity.png)

<span data-ttu-id="7ad4d-111">「複製活動」是由安全、可靠、可調整且 [全域可用的服務](#global)提供技術支援。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-111">Copy Activity is powered by a secure, reliable, scalable, and [globally available service](#global).</span></span> <span data-ttu-id="7ad4d-112">本文提供關於在 Data Factory 和複製活動中移動資料的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-112">This article provides details on data movement in Data Factory and Copy Activity.</span></span>

<span data-ttu-id="7ad4d-113">首先，讓我們看看在兩個雲端資料存放區之間，以及在內部部署資料存放區與雲端資料存放區之間，如何進行資料移轉。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-113">First, let's see how data migration occurs between two cloud data stores, and between an on-premises data store and a cloud data store.</span></span>

> [!NOTE]
> <span data-ttu-id="7ad4d-114">若要了解活動的大致情況，請參閱 [了解管線和活動](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-114">To learn about activities in general, see [Understanding pipelines and activities](data-factory-create-pipelines.md).</span></span>
>
>

### <a name="copy-data-between-two-cloud-data-stores"></a><span data-ttu-id="7ad4d-115">在兩個雲端資料存放區之間複製資料</span><span class="sxs-lookup"><span data-stu-id="7ad4d-115">Copy data between two cloud data stores</span></span>
<span data-ttu-id="7ad4d-116">當來源和接收資料存放區都在雲端時，「複製活動」就會經歷下列階段，將資料從來源複製到接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-116">When both source and sink data stores are in the cloud, Copy Activity goes through the following stages to copy data from the source to the sink.</span></span> <span data-ttu-id="7ad4d-117">為「複製活動」提供技術支援的雲端服務會：</span><span class="sxs-lookup"><span data-stu-id="7ad4d-117">The service that powers Copy Activity:</span></span>

1. <span data-ttu-id="7ad4d-118">從來源資料存放區讀取資料。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-118">Reads data from the source data store.</span></span>
2. <span data-ttu-id="7ad4d-119">執行序列化/還原序列化、壓縮/解壓縮、資料行對應及類型轉換。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-119">Performs serialization/deserialization, compression/decompression, column mapping, and type conversion.</span></span> <span data-ttu-id="7ad4d-120">它會根據輸入資料集、輸出資料集及「複製活動」的組態執行這些作業。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-120">It does these operations based on the configurations of the input dataset, output dataset, and Copy Activity.</span></span>
3. <span data-ttu-id="7ad4d-121">將資料寫入目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-121">Writes data to the destination data store.</span></span>

<span data-ttu-id="7ad4d-122">此服務會自動選擇最佳區域來執行資料移動。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-122">The service automatically chooses the optimal region to perform the data movement.</span></span> <span data-ttu-id="7ad4d-123">此區域通常是最靠近接收資料存放區的區域。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-123">This region is usually the one closest to the sink data store.</span></span>

![從雲端複製到雲端](./media/data-factory-data-movement-activities/cloud-to-cloud.png)

### <a name="copy-data-between-an-on-premises-data-store-and-a-cloud-data-store"></a><span data-ttu-id="7ad4d-125">在內部部署資料存放區和雲端資料存放區之間複製資料</span><span class="sxs-lookup"><span data-stu-id="7ad4d-125">Copy data between an on-premises data store and a cloud data store</span></span>
<span data-ttu-id="7ad4d-126">若要安全地在內部部署資料存放區與雲端資料存放區之間移動資料，請在內部部署機器上安裝「資料管理閘道」。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-126">To securely move data between an on-premises data store and a cloud data store, install Data Management Gateway on your on-premises machine.</span></span> <span data-ttu-id="7ad4d-127">「資料管理閘道」是一個能夠啟用混合式資料移動及處理的代理程式。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-127">Data Management Gateway is an agent that enables hybrid data movement and processing.</span></span> <span data-ttu-id="7ad4d-128">您可以將它安裝在與資料存放區本身相同的機器上，或是安裝在可存取該資料存放區的另一部機器上。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-128">You can install it on the same machine as the data store itself, or on a separate machine that has access to the data store.</span></span>

<span data-ttu-id="7ad4d-129">在此案例中，「資料管理閘道」會執行序列化/還原序列化、壓縮/解壓縮、資料行對應及類型轉換。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-129">In this scenario, Data Management Gateway performs the serialization/deserialization, compression/decompression, column mapping, and type conversion.</span></span> <span data-ttu-id="7ad4d-130">資料不會流經 Azure Data Factory 服務。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-130">Data does not flow through the Azure Data Factory service.</span></span> <span data-ttu-id="7ad4d-131">取而代之的是，「資料管理閘道」會直接將資料寫入到目的地存放區。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-131">Instead, Data Management Gateway directly writes the data to the destination store.</span></span>

![從內部部署複製到雲端](./media/data-factory-data-movement-activities/onprem-to-cloud.png)

<span data-ttu-id="7ad4d-133">如需簡介和逐步解說，請參閱 [在內部部署和雲端資料存放區之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-133">See [Move data between on-premises and cloud data stores](data-factory-move-data-between-onprem-and-cloud.md) for an introduction and walkthrough.</span></span> <span data-ttu-id="7ad4d-134">如需有關此代理程式的詳細資訊，請參閱 [資料管理閘道](data-factory-data-management-gateway.md) 。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-134">See [Data Management Gateway](data-factory-data-management-gateway.md) for detailed information about this agent.</span></span>

<span data-ttu-id="7ad4d-135">您也可以使用「資料管理閘道」，將資料移出/移入 Azure IaaS 虛擬機器 (VM) 上所裝載的支援資料存放區。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-135">You can also move data from/to supported data stores that are hosted on Azure IaaS virtual machines (VMs) by using Data Management Gateway.</span></span> <span data-ttu-id="7ad4d-136">在此情況下，您可以將「資料管理閘道」安裝在與資料存放區本身相同的 VM 上，或是安裝在可存取該資料存放區的另一部 VM 上。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-136">In this case, you can install Data Management Gateway on the same VM as the data store itself, or on a separate VM that has access to the data store.</span></span>

## <a name="supported-data-stores-and-formats"></a><span data-ttu-id="7ad4d-137">支援的資料存放區和格式</span><span class="sxs-lookup"><span data-stu-id="7ad4d-137">Supported data stores and formats</span></span>
<span data-ttu-id="7ad4d-138">Data Factory 中的複製活動會將資料從來源資料存放區複製到接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-138">Copy Activity in Data Factory copies data from a source data store to a sink data store.</span></span> <span data-ttu-id="7ad4d-139">Data Factory 支援下列資料存放區。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-139">Data Factory supports the following data stores.</span></span> <span data-ttu-id="7ad4d-140">可將來自任何來源的資料寫入任何接收器。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-140">Data from any source can be written to any sink.</span></span> <span data-ttu-id="7ad4d-141">按一下資料存放區，即可了解如何將資料複製到該存放區，以及從該存放區複製資料。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-141">Click a data store to learn how to copy data to and from that store.</span></span>

> [!NOTE] 
> <span data-ttu-id="7ad4d-142">如果您需要將資料移入/移出「複製活動」不支援的資料存放區，請在 Data Factory 中使用 **自訂活動** 搭配您自己的邏輯來複製/移動資料。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-142">If you need to move data to/from a data store that Copy Activity doesn't support, use a **custom activity** in Data Factory with your own logic for copying/moving data.</span></span> <span data-ttu-id="7ad4d-143">如需有關建立及使用自訂活動的詳細資料，請參閱 [在 Azure Data Factory 管線中使用自訂活動](data-factory-use-custom-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-143">For details on creating and using a custom activity, see [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md).</span></span>

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> <span data-ttu-id="7ad4d-144">具有 * 的資料存放區可以在內部部署環境或 Azure IaaS 上，並且需要您在內部部署/Azure IaaS 機器上安裝 [資料管理閘道](data-factory-data-management-gateway.md) 。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-144">Data stores with * can be on-premises or on Azure IaaS, and require you to install [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises/Azure IaaS machine.</span></span>

### <a name="supported-file-formats"></a><span data-ttu-id="7ad4d-145">支援的檔案格式</span><span class="sxs-lookup"><span data-stu-id="7ad4d-145">Supported file formats</span></span>
<span data-ttu-id="7ad4d-146">您可以使用「複製活動」在兩個以檔案為基礎的資料存放區之間**依原樣複製檔案**，您可以在輸入和輸出資料集定義中略過[格式區段](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-146">You can use Copy Activity to **copy files as-is** between two file-based data stores, you can skip the [format section](data-factory-create-datasets.md) in both the input and output dataset definitions.</span></span> <span data-ttu-id="7ad4d-147">系統會有效率地複製資料，而不會進行任何序列化/還原序列化。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-147">The data is copied efficiently without any serialization/deserialization.</span></span>

<span data-ttu-id="7ad4d-148">「複製活動」也會以指定的格式讀取和寫入檔案：**文字、JSON、Avro、ORC 和 Parquet**，並支援 **GZip、Deflate、BZip2 和 ZipDeflate** 壓縮轉碼器。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-148">Copy Activity also reads from and writes to files in specified formats: **Text, JSON, Avro, ORC, and Parquet**, and compression codec **GZip, Deflate, BZip2, and ZipDeflate** are supported.</span></span> <span data-ttu-id="7ad4d-149">如需詳細資訊，請參閱[支援的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md)。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-149">See [Supported file and compression formats](data-factory-supported-file-and-compression-formats.md) with details.</span></span>

<span data-ttu-id="7ad4d-150">例如，您可以執行下列複製活動：</span><span class="sxs-lookup"><span data-stu-id="7ad4d-150">For example, you can do the following copy activities:</span></span>

* <span data-ttu-id="7ad4d-151">複製內部部署 SQL Server 中的資料，然後以 ORC 格式寫入 Azure Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-151">Copy data in on-premises SQL Server and write to Azure Data Lake Store in ORC format.</span></span>
* <span data-ttu-id="7ad4d-152">從內部部署檔案系統複製文字 (CSV) 格式的檔案，然後以 Avro 格式寫入 Azure Blob 中。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-152">Copy files in text (CSV) format from on-premises File System and write to Azure Blob in Avro format.</span></span>
* <span data-ttu-id="7ad4d-153">從內部部署檔案系統複製壓縮檔，然後解壓縮到 Azure Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-153">Copy zipped files from on-premises File System and decompress then land to Azure Data Lake Store.</span></span>
* <span data-ttu-id="7ad4d-154">從 Azure Blob 複製 GZip 壓縮文字 (CSV) 格式的資料，然後寫入 Azure SQL Database 中。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-154">Copy data in GZip compressed text (CSV) format from Azure Blob and write to Azure SQL Database.</span></span>

## <span data-ttu-id="7ad4d-155"><a name="global"></a>全域可用的資料移動</span><span class="sxs-lookup"><span data-stu-id="7ad4d-155"><a name="global"></a>Globally available data movement</span></span>
<span data-ttu-id="7ad4d-156">Azure Data Factory 只在美國西部、美國東部和北歐區域提供使用。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-156">Azure Data Factory is available only in the West US, East US, and North Europe regions.</span></span> <span data-ttu-id="7ad4d-157">不過，支援複製活動的服務可在下列區域和地理位置全域提供使用。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-157">However, the service that powers Copy Activity is available globally in the following regions and geographies.</span></span> <span data-ttu-id="7ad4d-158">全域可用的拓撲可確保進行有效率的資料移動，通常可避免發生跨區域躍點的情況。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-158">The globally available topology ensures efficient data movement that usually avoids cross-region hops.</span></span> <span data-ttu-id="7ad4d-159">如需了解某區域中是否有 Data Factory 和「資料移動」可供使用，請參閱 [依區域提供的服務](https://azure.microsoft.com/regions/#services) 。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-159">See [Services by region](https://azure.microsoft.com/regions/#services) for availability of Data Factory and Data Movement in a region.</span></span>

### <a name="copy-data-between-cloud-data-stores"></a><span data-ttu-id="7ad4d-160">在雲端資料存放區之間複製資料</span><span class="sxs-lookup"><span data-stu-id="7ad4d-160">Copy data between cloud data stores</span></span>
<span data-ttu-id="7ad4d-161">當來源和接收資料存放區都位於雲端時，Data Factory 會使用區域中最接近相同地理位置之接收的服務部署來移動資料。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-161">When both source and sink data stores are in the cloud, Data Factory uses a service deployment in the region that is closest to the sink in the same geography to move the data.</span></span> <span data-ttu-id="7ad4d-162">如需對應資訊，請參閱下表︰</span><span class="sxs-lookup"><span data-stu-id="7ad4d-162">Refer to the following table for mapping:</span></span>

| <span data-ttu-id="7ad4d-163">目的地資料存放區的地理位置</span><span class="sxs-lookup"><span data-stu-id="7ad4d-163">Geography of the destination data stores</span></span> | <span data-ttu-id="7ad4d-164">目的地資料存放區的區域</span><span class="sxs-lookup"><span data-stu-id="7ad4d-164">Region of the destination data store</span></span> | <span data-ttu-id="7ad4d-165">用於資料移動的區域</span><span class="sxs-lookup"><span data-stu-id="7ad4d-165">Region used for data movement</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="7ad4d-166">美國</span><span class="sxs-lookup"><span data-stu-id="7ad4d-166">United States</span></span> | <span data-ttu-id="7ad4d-167">美國東部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-167">East US</span></span> | <span data-ttu-id="7ad4d-168">美國東部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-168">East US</span></span> |
| &nbsp; | <span data-ttu-id="7ad4d-169">美國東部 2</span><span class="sxs-lookup"><span data-stu-id="7ad4d-169">East US 2</span></span> | <span data-ttu-id="7ad4d-170">美國東部 2</span><span class="sxs-lookup"><span data-stu-id="7ad4d-170">East US 2</span></span> |
| &nbsp; | <span data-ttu-id="7ad4d-171">美國中部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-171">Central US</span></span> | <span data-ttu-id="7ad4d-172">美國中部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-172">Central US</span></span> |
| &nbsp; | <span data-ttu-id="7ad4d-173">美國中北部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-173">North Central US</span></span> | <span data-ttu-id="7ad4d-174">美國中北部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-174">North Central US</span></span> |
| &nbsp; | <span data-ttu-id="7ad4d-175">美國中南部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-175">South Central US</span></span> | <span data-ttu-id="7ad4d-176">美國中南部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-176">South Central US</span></span> |
| &nbsp; | <span data-ttu-id="7ad4d-177">美國中西部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-177">West Central US</span></span> | <span data-ttu-id="7ad4d-178">美國中西部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-178">West Central US</span></span> |
| &nbsp; | <span data-ttu-id="7ad4d-179">美國西部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-179">West US</span></span> | <span data-ttu-id="7ad4d-180">美國西部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-180">West US</span></span> |
| &nbsp; | <span data-ttu-id="7ad4d-181">美國西部 2</span><span class="sxs-lookup"><span data-stu-id="7ad4d-181">West US 2</span></span> | <span data-ttu-id="7ad4d-182">美國西部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-182">West US</span></span> |
| <span data-ttu-id="7ad4d-183">加拿大</span><span class="sxs-lookup"><span data-stu-id="7ad4d-183">Canada</span></span> | <span data-ttu-id="7ad4d-184">加拿大東部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-184">Canada East</span></span> | <span data-ttu-id="7ad4d-185">加拿大中部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-185">Canada Central</span></span> |
| &nbsp; | <span data-ttu-id="7ad4d-186">加拿大中部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-186">Canada Central</span></span> | <span data-ttu-id="7ad4d-187">加拿大中部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-187">Canada Central</span></span> |
| <span data-ttu-id="7ad4d-188">巴西</span><span class="sxs-lookup"><span data-stu-id="7ad4d-188">Brazil</span></span> | <span data-ttu-id="7ad4d-189">巴西南部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-189">Brazil South</span></span> | <span data-ttu-id="7ad4d-190">巴西南部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-190">Brazil South</span></span> |
| <span data-ttu-id="7ad4d-191">歐洲</span><span class="sxs-lookup"><span data-stu-id="7ad4d-191">Europe</span></span> | <span data-ttu-id="7ad4d-192">北歐</span><span class="sxs-lookup"><span data-stu-id="7ad4d-192">North Europe</span></span> | <span data-ttu-id="7ad4d-193">北歐</span><span class="sxs-lookup"><span data-stu-id="7ad4d-193">North Europe</span></span> |
| &nbsp; | <span data-ttu-id="7ad4d-194">西歐</span><span class="sxs-lookup"><span data-stu-id="7ad4d-194">West Europe</span></span> | <span data-ttu-id="7ad4d-195">西歐</span><span class="sxs-lookup"><span data-stu-id="7ad4d-195">West Europe</span></span> |
| <span data-ttu-id="7ad4d-196">英國</span><span class="sxs-lookup"><span data-stu-id="7ad4d-196">United Kingdom</span></span> | <span data-ttu-id="7ad4d-197">英國西部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-197">UK West</span></span> | <span data-ttu-id="7ad4d-198">英國南部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-198">UK South</span></span> |
| &nbsp; | <span data-ttu-id="7ad4d-199">英國南部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-199">UK South</span></span> | <span data-ttu-id="7ad4d-200">英國南部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-200">UK South</span></span> |
| <span data-ttu-id="7ad4d-201">亞太地區</span><span class="sxs-lookup"><span data-stu-id="7ad4d-201">Asia Pacific</span></span> | <span data-ttu-id="7ad4d-202">東南亞</span><span class="sxs-lookup"><span data-stu-id="7ad4d-202">Southeast Asia</span></span> | <span data-ttu-id="7ad4d-203">東南亞</span><span class="sxs-lookup"><span data-stu-id="7ad4d-203">Southeast Asia</span></span> |
| &nbsp; | <span data-ttu-id="7ad4d-204">東亞</span><span class="sxs-lookup"><span data-stu-id="7ad4d-204">East Asia</span></span> | <span data-ttu-id="7ad4d-205">東南亞</span><span class="sxs-lookup"><span data-stu-id="7ad4d-205">Southeast Asia</span></span> |
| <span data-ttu-id="7ad4d-206">澳大利亞</span><span class="sxs-lookup"><span data-stu-id="7ad4d-206">Australia</span></span> | <span data-ttu-id="7ad4d-207">澳洲東部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-207">Australia East</span></span> | <span data-ttu-id="7ad4d-208">澳洲東部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-208">Australia East</span></span> |
| &nbsp; | <span data-ttu-id="7ad4d-209">澳大利亞東南部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-209">Australia Southeast</span></span> | <span data-ttu-id="7ad4d-210">澳大利亞東南部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-210">Australia Southeast</span></span> |
| <span data-ttu-id="7ad4d-211">日本</span><span class="sxs-lookup"><span data-stu-id="7ad4d-211">Japan</span></span> | <span data-ttu-id="7ad4d-212">日本東部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-212">Japan East</span></span> | <span data-ttu-id="7ad4d-213">日本東部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-213">Japan East</span></span> |
| &nbsp; | <span data-ttu-id="7ad4d-214">日本西部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-214">Japan West</span></span> | <span data-ttu-id="7ad4d-215">日本東部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-215">Japan East</span></span> |
| <span data-ttu-id="7ad4d-216">印度</span><span class="sxs-lookup"><span data-stu-id="7ad4d-216">India</span></span> | <span data-ttu-id="7ad4d-217">印度中部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-217">Central India</span></span> | <span data-ttu-id="7ad4d-218">印度中部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-218">Central India</span></span> |
| &nbsp; | <span data-ttu-id="7ad4d-219">印度西部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-219">West India</span></span> | <span data-ttu-id="7ad4d-220">印度中部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-220">Central India</span></span> |
| &nbsp; | <span data-ttu-id="7ad4d-221">印度南部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-221">South India</span></span> | <span data-ttu-id="7ad4d-222">印度中部</span><span class="sxs-lookup"><span data-stu-id="7ad4d-222">Central India</span></span> |

<span data-ttu-id="7ad4d-223">或者，您可以明確指出要用來執行複製的 Data Factory 服務區域，方法是指定複製活動 `typeProperties` 底下的 `executionLocation`屬性。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-223">Alternatively, you can explicitly indicate the region of Data Factory service to be used to perform the copy by specifying `executionLocation` property under Copy Activity `typeProperties`.</span></span> <span data-ttu-id="7ad4d-224">這個屬性支援的值詳列於上述**用於資料移動的區域**資料行。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-224">Supported values for this property are listed in above **Region used for data movement** column.</span></span> <span data-ttu-id="7ad4d-225">請注意，您的資料在複製期間會透過網路通過該區域。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-225">Note your data goes through that region over the wire during copy.</span></span> <span data-ttu-id="7ad4d-226">例如，若要在韓國的 Azure 存放區之間複製，您可以將 `"executionLocation": "Japan East"` 指定為經過日本區域 (請參考[範例 JSON](#by-using-json-scripts))。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-226">For example, to copy between Azure stores in Korea, you can specify `"executionLocation": "Japan East"` to route through Japan region (see [sample JSON](#by-using-json-scripts) as reference).</span></span>

> [!NOTE]
> <span data-ttu-id="7ad4d-227">如果目的地資料存放區的區域不在上述清單中，除非指定 `executionLocation`，否則「複製活動」預設將會失敗而不會搜查替代區域。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-227">If the region of the destination data store is not in preceding list or undetectable, by default Copy Activity fails instead of going through an alternative region, unless `executionLocation` is specified.</span></span> <span data-ttu-id="7ad4d-228">支援的區域清單將會隨著時間擴展。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-228">The supported region list will be expanded over time.</span></span>
>

### <a name="copy-data-between-an-on-premises-data-store-and-a-cloud-data-store"></a><span data-ttu-id="7ad4d-229">在內部部署資料存放區和雲端資料存放區之間複製資料</span><span class="sxs-lookup"><span data-stu-id="7ad4d-229">Copy data between an on-premises data store and a cloud data store</span></span>
<span data-ttu-id="7ad4d-230">在內部部署存放區 (或 Azure 虛擬機器/IaaS) 與雲端存放區之間複製資料時， [資料管理閘道](data-factory-data-management-gateway.md) 會在內部部署機器或虛擬機器上執行資料移動。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-230">When data is being copied between on-premises (or Azure virtual machines/IaaS) and cloud stores, [Data Management Gateway](data-factory-data-management-gateway.md) performs data movement on an on-premises machine or virtual machine.</span></span> <span data-ttu-id="7ad4d-231">除非您使用 [分段複製](data-factory-copy-activity-performance.md#staged-copy) 功能，否則資料不會流經雲端服務。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-231">The data does not flow through the service in the cloud, unless you use the [staged copy](data-factory-copy-activity-performance.md#staged-copy) capability.</span></span> <span data-ttu-id="7ad4d-232">在此情況下，資料會先流經預備環境 Azure Blob 儲存體，然後才寫入接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-232">In this case, data flows through the staging Azure Blob storage before it is written into the sink data store.</span></span>

## <a name="create-a-pipeline-with-copy-activity"></a><span data-ttu-id="7ad4d-233">建立具有複製活動的管線</span><span class="sxs-lookup"><span data-stu-id="7ad4d-233">Create a pipeline with Copy Activity</span></span>
<span data-ttu-id="7ad4d-234">您可以使用幾個方式來建立具有「複製活動」的管線︰</span><span class="sxs-lookup"><span data-stu-id="7ad4d-234">You can create a pipeline with Copy Activity in a couple of ways:</span></span>

### <a name="by-using-the-copy-wizard"></a><span data-ttu-id="7ad4d-235">透過使用複製精靈</span><span class="sxs-lookup"><span data-stu-id="7ad4d-235">By using the Copy Wizard</span></span>
<span data-ttu-id="7ad4d-236">「Data Factory 複製精靈」可協助您建立具有「複製活動」的管線。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-236">The Data Factory Copy Wizard helps you to create a pipeline with Copy Activity.</span></span> <span data-ttu-id="7ad4d-237">此管線可讓您在「不需要」為連結服務、資料集及管線「撰寫 JSON」  定義的情況下，將資料從支援的來源複製到目的地。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-237">This pipeline allows you to copy data from supported sources to destinations *without writing JSON* definitions for linked services, datasets, and pipelines.</span></span> <span data-ttu-id="7ad4d-238">如需有關此精靈的詳細資料，請參閱 [Data Factory 複製精靈](data-factory-copy-wizard.md) 。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-238">See [Data Factory Copy Wizard](data-factory-copy-wizard.md) for details about the wizard.</span></span>  

### <a name="by-using-json-scripts"></a><span data-ttu-id="7ad4d-239">透過使用 JSON 指令碼</span><span class="sxs-lookup"><span data-stu-id="7ad4d-239">By using JSON scripts</span></span>
<span data-ttu-id="7ad4d-240">您可以使用 Azure 入口網站中的「Data Factory 編輯器」、Visual Studio 或 Azure PowerShell 來建立管線的 JSON 定義 (透過使用「複製活動」)。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-240">You can use Data Factory Editor in the Azure portal, Visual Studio, or Azure PowerShell to create a JSON definition for a pipeline (by using Copy Activity).</span></span> <span data-ttu-id="7ad4d-241">然後，您可以部署它以在 Data Factory 中建立管線。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-241">Then, you can deploy it to create the pipeline in Data Factory.</span></span> <span data-ttu-id="7ad4d-242">如需含有逐步指示的教學課程，請參閱 [教學課程：在 Azure Data Factory 管線中使用複製活動](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-242">See [Tutorial: Use Copy Activity in an Azure Data Factory pipeline](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for a tutorial with step-by-step instructions.</span></span>    

<span data-ttu-id="7ad4d-243">JSON 屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-243">JSON properties (such as name, description, input and output tables, and policies) are available for all types of activities.</span></span> <span data-ttu-id="7ad4d-244">活動的 `typeProperties` 區段中可用的屬性會因每個活動類型的不同而有所不同。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-244">Properties that are available in the `typeProperties` section of the activity vary with each activity type.</span></span>

<span data-ttu-id="7ad4d-245">在複製活動中， `typeProperties` 區段會根據來源和接收器的類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-245">For Copy Activity, the `typeProperties` section varies depending on the types of sources and sinks.</span></span> <span data-ttu-id="7ad4d-246">按一下 [支援來源和接收器](#supported-data-stores-and-formats) 一節中的來源/接收器，即可了解「複製活動」針對該資料存放區所支援的類型屬性。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-246">Click a source/sink in the [Supported sources and sinks](#supported-data-stores-and-formats) section to learn about type properties that Copy Activity supports for that data store.</span></span>

<span data-ttu-id="7ad4d-247">以下是範例 JSON 定義︰</span><span class="sxs-lookup"><span data-stu-id="7ad4d-247">Here's a sample JSON definition:</span></span>

```json
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from Azure blob to Azure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputBlobTable"
          }
        ],
        "outputs": [
          {
            "name": "OutputSQLTable"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink"
          },
          "executionLocation": "Japan East"          
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2016-07-12T00:00:00Z",
    "end": "2016-07-13T00:00:00Z"
  }
}
```
<span data-ttu-id="7ad4d-248">輸出資料集中定義的排程會決定活動的執行時間 (例如「每日」，即頻率為「日」，間隔為 **1**)。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-248">The schedule that is defined in the output dataset determines when the activity runs (for example: **daily**, frequency as **day**, and interval as **1**).</span></span> <span data-ttu-id="7ad4d-249">活動會將資料從輸入資料集 (**source**) 複製到輸出資料集 (**sink**)。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-249">The activity copies data from an input dataset (**source**) to an output dataset (**sink**).</span></span>

<span data-ttu-id="7ad4d-250">您可以為「複製活動」指定多個輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-250">You can specify more than one input dataset to Copy Activity.</span></span> <span data-ttu-id="7ad4d-251">系統會先使用它們來確認相依性，然後才執行活動。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-251">They are used to verify the dependencies before the activity is run.</span></span> <span data-ttu-id="7ad4d-252">不過，只有來自第一個資料集的資料會被複製到目的地資料集。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-252">However, only the data from the first dataset is copied to the destination dataset.</span></span> <span data-ttu-id="7ad4d-253">如需詳細資訊，請參閱 [排程和執行](data-factory-scheduling-and-execution.md)。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-253">For more information, see [Scheduling and execution](data-factory-scheduling-and-execution.md).</span></span>  

## <a name="performance-and-tuning"></a><span data-ttu-id="7ad4d-254">效能和微調</span><span class="sxs-lookup"><span data-stu-id="7ad4d-254">Performance and tuning</span></span>
<span data-ttu-id="7ad4d-255">請參閱 [複製活動的效能及微調指南](data-factory-copy-activity-performance.md)，其中說明在 Azure Data Factory 中會影響資料移動 (複製活動) 效能的重要因素。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-255">See the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md), which describes key factors that affect the performance of data movement (Copy Activity) in Azure Data Factory.</span></span> <span data-ttu-id="7ad4d-256">它也列出在內部測試期間所觀察到的效能，並討論各種可將「複製活動」效能最佳化的方式。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-256">It also lists the observed performance during internal testing and discusses various ways to optimize the performance of Copy Activity.</span></span>

## <a name="fault-tolerance"></a><span data-ttu-id="7ad4d-257">容錯</span><span class="sxs-lookup"><span data-stu-id="7ad4d-257">Fault tolerance</span></span>
<span data-ttu-id="7ad4d-258">根據預設，來源與接收之間出現不相容的資料時，複製活動會停止複製資料並傳回失敗；而您可以明確設定略過並記錄不相容的資料列，只複製那些相容的資料，使複製成功。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-258">By default, copy activity will stop copying data and return failure when encounter incompatible data between source and sink; while you can explicitly configure to skip and log the incompatible rows and only copy those compatible data to make the copy succeeded.</span></span> <span data-ttu-id="7ad4d-259">如需詳細資訊，請參閱[複製活動容錯](data-factory-copy-activity-fault-tolerance.md)。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-259">See the [Copy Activity fault tolerance](data-factory-copy-activity-fault-tolerance.md) on more details.</span></span>

## <a name="security-considerations"></a><span data-ttu-id="7ad4d-260">安全性考量</span><span class="sxs-lookup"><span data-stu-id="7ad4d-260">Security considerations</span></span>
<span data-ttu-id="7ad4d-261">請參閱[安全性考量](data-factory-data-movement-security-considerations.md)，說明 Azure Data Factory 中資料移動服務用來保護您資料的安全性基礎結構。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-261">See the [Security considerations](data-factory-data-movement-security-considerations.md), which describes security infrastructure that data movement services in Azure Data Factory use to secure your data.</span></span>

## <a name="scheduling-and-sequential-copy"></a><span data-ttu-id="7ad4d-262">排程和循序複製</span><span class="sxs-lookup"><span data-stu-id="7ad4d-262">Scheduling and sequential copy</span></span>
<span data-ttu-id="7ad4d-263">請參閱 [排程和執行](data-factory-scheduling-and-execution.md) ，以取得排程和執行在 Data Factory 中如何運作的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-263">See [Scheduling and execution](data-factory-scheduling-and-execution.md) for detailed information about how scheduling and execution works in Data Factory.</span></span> <span data-ttu-id="7ad4d-264">您可以利用循序/排序的方式，逐一執行多個複製作業。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-264">It is possible to run multiple copy operations one after another in a sequential/ordered manner.</span></span> <span data-ttu-id="7ad4d-265">請參閱[循序複製](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)一節。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-265">See the [Copy sequentially](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) section.</span></span>

## <a name="type-conversions"></a><span data-ttu-id="7ad4d-266">類型轉換</span><span class="sxs-lookup"><span data-stu-id="7ad4d-266">Type conversions</span></span>
<span data-ttu-id="7ad4d-267">不同的資料存放區有不同的原生類型系統。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-267">Different data stores have different native type systems.</span></span> <span data-ttu-id="7ad4d-268">「複製活動」會藉由下列含有兩個步驟的方法，執行從來源類型轉換成接收類型的自動類型轉換：</span><span class="sxs-lookup"><span data-stu-id="7ad4d-268">Copy Activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="7ad4d-269">從原生來源類型轉換成 .NET 類型。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-269">Convert from native source types to a .NET type.</span></span>
2. <span data-ttu-id="7ad4d-270">從 .NET 類型轉換成原生接收類型。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-270">Convert from a .NET type to a native sink type.</span></span>

<span data-ttu-id="7ad4d-271">資料存放區從原生類型系統到 .NET 類型的對應，位於個別的資料存放區文章中。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-271">The mapping from a native type system to a .NET type for a data store is in the respective data store article.</span></span> <span data-ttu-id="7ad4d-272">(按一下 [支援的資料存放區](#supported-data-stores) 表格中的特定連結)。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-272">(Click the specific link in the [Supported data stores](#supported-data-stores) table).</span></span> <span data-ttu-id="7ad4d-273">您可以在建立資料表時，使用這些對應來判斷適當的類型，以便讓「複製活動」能夠執行正確的轉換。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-273">You can use these mappings to determine appropriate types while creating your tables, so that Copy Activity performs the right conversions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ad4d-274">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7ad4d-274">Next steps</span></span>
* <span data-ttu-id="7ad4d-275">若要深入了解複製活動，請參閱 [將資料從 Azure Blob 儲存體複製到 Azure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-275">To learn about the Copy Activity more, see [Copy data from Azure Blob storage to Azure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
* <span data-ttu-id="7ad4d-276">若要了解如何將資料從內部部署資料存放區移到雲端資料存放區，請參閱 [將資料從內部部署資料存放區移到雲端資料存放區](data-factory-move-data-between-onprem-and-cloud.md)。</span><span class="sxs-lookup"><span data-stu-id="7ad4d-276">To learn about moving data from an on-premises data store to a cloud data store, see [Move data from on-premises to cloud data stores](data-factory-move-data-between-onprem-and-cloud.md).</span></span>
