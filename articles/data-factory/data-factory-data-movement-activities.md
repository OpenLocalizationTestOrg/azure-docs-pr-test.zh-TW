---
title: "使用複製活動 aaaMove 資料 |Microsoft 文件"
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
ms.openlocfilehash: 29b74154b9006795ead3b0ee9638a3dbf2c5d831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-by-using-copy-activity"></a><span data-ttu-id="ee895-105">使用複製活動來移動資料</span><span class="sxs-lookup"><span data-stu-id="ee895-105">Move data by using Copy Activity</span></span>
## <a name="overview"></a><span data-ttu-id="ee895-106">概觀</span><span class="sxs-lookup"><span data-stu-id="ee895-106">Overview</span></span>
<span data-ttu-id="ee895-107">在 Azure Data Factory，您可以使用複製活動 toocopy 資料在內部部署和雲端之間的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="ee895-107">In Azure Data Factory, you can use Copy Activity toocopy data between on-premises and cloud data stores.</span></span> <span data-ttu-id="ee895-108">複製 hello 資料之後，它可以進一步轉換及分析。</span><span class="sxs-lookup"><span data-stu-id="ee895-108">After hello data is copied, it can be further transformed and analyzed.</span></span> <span data-ttu-id="ee895-109">您也可以使用複製活動 toopublish 轉換和分析結果的商業智慧 (BI) 和應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="ee895-109">You can also use Copy Activity toopublish transformation and analysis results for business intelligence (BI) and application consumption.</span></span>

![複製活動的角色](media/data-factory-data-movement-activities/copy-activity.png)

<span data-ttu-id="ee895-111">「複製活動」是由安全、可靠、可調整且 [全域可用的服務](#global)提供技術支援。</span><span class="sxs-lookup"><span data-stu-id="ee895-111">Copy Activity is powered by a secure, reliable, scalable, and [globally available service](#global).</span></span> <span data-ttu-id="ee895-112">本文提供關於在 Data Factory 和複製活動中移動資料的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="ee895-112">This article provides details on data movement in Data Factory and Copy Activity.</span></span>

<span data-ttu-id="ee895-113">首先，讓我們看看在兩個雲端資料存放區之間，以及在內部部署資料存放區與雲端資料存放區之間，如何進行資料移轉。</span><span class="sxs-lookup"><span data-stu-id="ee895-113">First, let's see how data migration occurs between two cloud data stores, and between an on-premises data store and a cloud data store.</span></span>

> [!NOTE]
> <span data-ttu-id="ee895-114">一般情況下，請參閱有關活動 toolearn[了解管線和活動](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="ee895-114">toolearn about activities in general, see [Understanding pipelines and activities](data-factory-create-pipelines.md).</span></span>
>
>

### <a name="copy-data-between-two-cloud-data-stores"></a><span data-ttu-id="ee895-115">在兩個雲端資料存放區之間複製資料</span><span class="sxs-lookup"><span data-stu-id="ee895-115">Copy data between two cloud data stores</span></span>
<span data-ttu-id="ee895-116">Hello 雲端來源和接收的資料存放區時，複製活動會經歷下列階段 toocopy 資料從 hello 來源 toohello 接收 hello。</span><span class="sxs-lookup"><span data-stu-id="ee895-116">When both source and sink data stores are in hello cloud, Copy Activity goes through hello following stages toocopy data from hello source toohello sink.</span></span> <span data-ttu-id="ee895-117">hello 力量複製活動的服務：</span><span class="sxs-lookup"><span data-stu-id="ee895-117">hello service that powers Copy Activity:</span></span>

1. <span data-ttu-id="ee895-118">從 hello 來源資料存放區讀取資料。</span><span class="sxs-lookup"><span data-stu-id="ee895-118">Reads data from hello source data store.</span></span>
2. <span data-ttu-id="ee895-119">執行序列化/還原序列化、壓縮/解壓縮、資料行對應及類型轉換。</span><span class="sxs-lookup"><span data-stu-id="ee895-119">Performs serialization/deserialization, compression/decompression, column mapping, and type conversion.</span></span> <span data-ttu-id="ee895-120">它會根據 hello 輸入資料集、 輸出資料集，以及複製活動的 hello 設定這些作業。</span><span class="sxs-lookup"><span data-stu-id="ee895-120">It does these operations based on hello configurations of hello input dataset, output dataset, and Copy Activity.</span></span>
3. <span data-ttu-id="ee895-121">寫入資料 toohello 目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="ee895-121">Writes data toohello destination data store.</span></span>

<span data-ttu-id="ee895-122">hello 服務會自動選擇 hello 最佳區域 tooperform hello 資料移動。</span><span class="sxs-lookup"><span data-stu-id="ee895-122">hello service automatically chooses hello optimal region tooperform hello data movement.</span></span> <span data-ttu-id="ee895-123">此區域通常是 hello 一個最接近 toohello 接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="ee895-123">This region is usually hello one closest toohello sink data store.</span></span>

![從雲端複製到雲端](./media/data-factory-data-movement-activities/cloud-to-cloud.png)

### <a name="copy-data-between-an-on-premises-data-store-and-a-cloud-data-store"></a><span data-ttu-id="ee895-125">在內部部署資料存放區和雲端資料存放區之間複製資料</span><span class="sxs-lookup"><span data-stu-id="ee895-125">Copy data between an on-premises data store and a cloud data store</span></span>
<span data-ttu-id="ee895-126">toosecurely 移動資料的內部部署資料存放區之間的雲端資料存放區中，您在內部部署的電腦上安裝資料管理閘道器。</span><span class="sxs-lookup"><span data-stu-id="ee895-126">toosecurely move data between an on-premises data store and a cloud data store, install Data Management Gateway on your on-premises machine.</span></span> <span data-ttu-id="ee895-127">「資料管理閘道」是一個能夠啟用混合式資料移動及處理的代理程式。</span><span class="sxs-lookup"><span data-stu-id="ee895-127">Data Management Gateway is an agent that enables hybrid data movement and processing.</span></span> <span data-ttu-id="ee895-128">您可以安裝在相同機器 hello 資料存放區本身，因為 hello 或具有存取 toohello 資料儲存在不同電腦上。</span><span class="sxs-lookup"><span data-stu-id="ee895-128">You can install it on hello same machine as hello data store itself, or on a separate machine that has access toohello data store.</span></span>

<span data-ttu-id="ee895-129">在此案例中，資料管理閘道器會執行 hello 序列化/還原序列化、 壓縮/解壓縮、 資料行對應，及類型轉換。</span><span class="sxs-lookup"><span data-stu-id="ee895-129">In this scenario, Data Management Gateway performs hello serialization/deserialization, compression/decompression, column mapping, and type conversion.</span></span> <span data-ttu-id="ee895-130">資料不會流過 hello Azure Data Factory 服務透過。</span><span class="sxs-lookup"><span data-stu-id="ee895-130">Data does not flow through hello Azure Data Factory service.</span></span> <span data-ttu-id="ee895-131">相反地，資料管理閘道器會直接寫入 hello 資料 toohello 目的地存放區。</span><span class="sxs-lookup"><span data-stu-id="ee895-131">Instead, Data Management Gateway directly writes hello data toohello destination store.</span></span>

![從內部部署複製到雲端](./media/data-factory-data-movement-activities/onprem-to-cloud.png)

<span data-ttu-id="ee895-133">如需簡介和逐步解說，請參閱 [在內部部署和雲端資料存放區之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 。</span><span class="sxs-lookup"><span data-stu-id="ee895-133">See [Move data between on-premises and cloud data stores](data-factory-move-data-between-onprem-and-cloud.md) for an introduction and walkthrough.</span></span> <span data-ttu-id="ee895-134">如需有關此代理程式的詳細資訊，請參閱 [資料管理閘道](data-factory-data-management-gateway.md) 。</span><span class="sxs-lookup"><span data-stu-id="ee895-134">See [Data Management Gateway](data-factory-data-management-gateway.md) for detailed information about this agent.</span></span>

<span data-ttu-id="ee895-135">您也可以將資料從 / toosupported 資料存放區，使用資料管理閘道器裝載在 Azure IaaS 虛擬機器 (Vm) 上。</span><span class="sxs-lookup"><span data-stu-id="ee895-135">You can also move data from/toosupported data stores that are hosted on Azure IaaS virtual machines (VMs) by using Data Management Gateway.</span></span> <span data-ttu-id="ee895-136">在此情況下，您可以在安裝資料管理閘道器 hello hello 資料存放區本身，或具有存取 toohello 資料儲存在個別 VM 上的相同的 VM。</span><span class="sxs-lookup"><span data-stu-id="ee895-136">In this case, you can install Data Management Gateway on hello same VM as hello data store itself, or on a separate VM that has access toohello data store.</span></span>

## <a name="supported-data-stores-and-formats"></a><span data-ttu-id="ee895-137">支援的資料存放區和格式</span><span class="sxs-lookup"><span data-stu-id="ee895-137">Supported data stores and formats</span></span>
<span data-ttu-id="ee895-138">Data Factory 中的複製活動會將資料從來源資料存放區 tooa 接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="ee895-138">Copy Activity in Data Factory copies data from a source data store tooa sink data store.</span></span> <span data-ttu-id="ee895-139">Data Factory 支援下列資料存放區的 hello。</span><span class="sxs-lookup"><span data-stu-id="ee895-139">Data Factory supports hello following data stores.</span></span> <span data-ttu-id="ee895-140">從任何來源的資料可以寫入 tooany 接收。</span><span class="sxs-lookup"><span data-stu-id="ee895-140">Data from any source can be written tooany sink.</span></span> <span data-ttu-id="ee895-141">按一下 資料存放區 toolearn 如何 toocopy 資料 tooand 從該存放區。</span><span class="sxs-lookup"><span data-stu-id="ee895-141">Click a data store toolearn how toocopy data tooand from that store.</span></span>

> [!NOTE] 
> <span data-ttu-id="ee895-142">如果您需要 toomove 資料複製活動不支援的資料存放區中，使用**自訂活動**您自己的邏輯複製/移動資料的 Data Factory 中。</span><span class="sxs-lookup"><span data-stu-id="ee895-142">If you need toomove data to/from a data store that Copy Activity doesn't support, use a **custom activity** in Data Factory with your own logic for copying/moving data.</span></span> <span data-ttu-id="ee895-143">如需有關建立及使用自訂活動的詳細資料，請參閱 [在 Azure Data Factory 管線中使用自訂活動](data-factory-use-custom-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="ee895-143">For details on creating and using a custom activity, see [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md).</span></span>

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> <span data-ttu-id="ee895-144">資料存放區使用 * 可在內部部署或 Azure IaaS 上，因此需要您 tooinstall[資料管理閘道器](data-factory-data-management-gateway.md)在內部部署/Azure IaaS 電腦上。</span><span class="sxs-lookup"><span data-stu-id="ee895-144">Data stores with * can be on-premises or on Azure IaaS, and require you tooinstall [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises/Azure IaaS machine.</span></span>

### <a name="supported-file-formats"></a><span data-ttu-id="ee895-145">支援的檔案格式</span><span class="sxs-lookup"><span data-stu-id="ee895-145">Supported file formats</span></span>
<span data-ttu-id="ee895-146">您也可以使用複製活動**複製檔做為-是**之間以檔案為基礎的兩個資料存放區，您可以略過 hello[格式化區段](data-factory-create-datasets.md)在 hello 輸入和輸出資料集定義。</span><span class="sxs-lookup"><span data-stu-id="ee895-146">You can use Copy Activity too**copy files as-is** between two file-based data stores, you can skip hello [format section](data-factory-create-datasets.md) in both hello input and output dataset definitions.</span></span> <span data-ttu-id="ee895-147">hello 資料有效率地複製不含任何序列化/還原序列化。</span><span class="sxs-lookup"><span data-stu-id="ee895-147">hello data is copied efficiently without any serialization/deserialization.</span></span>

<span data-ttu-id="ee895-148">複製活動也會讀取和寫入 toofiles 中指定的格式： **Text、 JSON、 Avro、 ORC 及 Parquet**，並壓縮轉碼器**GZip、 Deflate、 BZip2 和 ZipDeflate**支援。</span><span class="sxs-lookup"><span data-stu-id="ee895-148">Copy Activity also reads from and writes toofiles in specified formats: **Text, JSON, Avro, ORC, and Parquet**, and compression codec **GZip, Deflate, BZip2, and ZipDeflate** are supported.</span></span> <span data-ttu-id="ee895-149">如需詳細資訊，請參閱[支援的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md)。</span><span class="sxs-lookup"><span data-stu-id="ee895-149">See [Supported file and compression formats](data-factory-supported-file-and-compression-formats.md) with details.</span></span>

<span data-ttu-id="ee895-150">例如，您可以執行 hello 下列複製的活動：</span><span class="sxs-lookup"><span data-stu-id="ee895-150">For example, you can do hello following copy activities:</span></span>

* <span data-ttu-id="ee895-151">複製資料在內部部署 SQL Server 中，將 ORC 格式寫入 tooAzure 資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="ee895-151">Copy data in on-premises SQL Server and write tooAzure Data Lake Store in ORC format.</span></span>
* <span data-ttu-id="ee895-152">將檔案從內部部署檔案系統複製文字 (CSV) 格式，並將 tooAzure Blob 寫入 Avro 格式。</span><span class="sxs-lookup"><span data-stu-id="ee895-152">Copy files in text (CSV) format from on-premises File System and write tooAzure Blob in Avro format.</span></span>
* <span data-ttu-id="ee895-153">從內部部署檔案系統複製 zip 的檔案解壓縮，然後登陸 tooAzure 資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="ee895-153">Copy zipped files from on-premises File System and decompress then land tooAzure Data Lake Store.</span></span>
* <span data-ttu-id="ee895-154">將資料從 Azure Blob 複製 GZip 壓縮的文字 (CSV) 格式，並將寫入 tooAzure SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="ee895-154">Copy data in GZip compressed text (CSV) format from Azure Blob and write tooAzure SQL Database.</span></span>

## <span data-ttu-id="ee895-155"><a name="global"></a>全域可用的資料移動</span><span class="sxs-lookup"><span data-stu-id="ee895-155"><a name="global"></a>Globally available data movement</span></span>
<span data-ttu-id="ee895-156">Azure Data Factory 提供了只 hello 美國西部、 美國東部、 和北歐區域。</span><span class="sxs-lookup"><span data-stu-id="ee895-156">Azure Data Factory is available only in hello West US, East US, and North Europe regions.</span></span> <span data-ttu-id="ee895-157">不過，可提供複製活動的 hello 服務位於全域 hello 下列區域和地理位置。</span><span class="sxs-lookup"><span data-stu-id="ee895-157">However, hello service that powers Copy Activity is available globally in hello following regions and geographies.</span></span> <span data-ttu-id="ee895-158">hello 全域可用的拓撲可確保通常可以避免跨地區躍點的高效率的資料移動。</span><span class="sxs-lookup"><span data-stu-id="ee895-158">hello globally available topology ensures efficient data movement that usually avoids cross-region hops.</span></span> <span data-ttu-id="ee895-159">如需了解某區域中是否有 Data Factory 和「資料移動」可供使用，請參閱 [依區域提供的服務](https://azure.microsoft.com/regions/#services) 。</span><span class="sxs-lookup"><span data-stu-id="ee895-159">See [Services by region](https://azure.microsoft.com/regions/#services) for availability of Data Factory and Data Movement in a region.</span></span>

### <a name="copy-data-between-cloud-data-stores"></a><span data-ttu-id="ee895-160">在雲端資料存放區之間複製資料</span><span class="sxs-lookup"><span data-stu-id="ee895-160">Copy data between cloud data stores</span></span>
<span data-ttu-id="ee895-161">Data Factory hello 雲端來源和接收的資料存放區時，會將服務部署使用 hello 中最接近的 toohello 接收 hello 區域中相同的地理位置 toomove hello 資料。</span><span class="sxs-lookup"><span data-stu-id="ee895-161">When both source and sink data stores are in hello cloud, Data Factory uses a service deployment in hello region that is closest toohello sink in hello same geography toomove hello data.</span></span> <span data-ttu-id="ee895-162">請參閱下表針對對應的 toohello:</span><span class="sxs-lookup"><span data-stu-id="ee895-162">Refer toohello following table for mapping:</span></span>

| <span data-ttu-id="ee895-163">地理位置的 hello 目的地資料存放區</span><span class="sxs-lookup"><span data-stu-id="ee895-163">Geography of hello destination data stores</span></span> | <span data-ttu-id="ee895-164">Hello 目的地資料存放區的區域</span><span class="sxs-lookup"><span data-stu-id="ee895-164">Region of hello destination data store</span></span> | <span data-ttu-id="ee895-165">用於資料移動的區域</span><span class="sxs-lookup"><span data-stu-id="ee895-165">Region used for data movement</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ee895-166">美國</span><span class="sxs-lookup"><span data-stu-id="ee895-166">United States</span></span> | <span data-ttu-id="ee895-167">美國東部</span><span class="sxs-lookup"><span data-stu-id="ee895-167">East US</span></span> | <span data-ttu-id="ee895-168">美國東部</span><span class="sxs-lookup"><span data-stu-id="ee895-168">East US</span></span> |
| &nbsp; | <span data-ttu-id="ee895-169">美國東部 2</span><span class="sxs-lookup"><span data-stu-id="ee895-169">East US 2</span></span> | <span data-ttu-id="ee895-170">美國東部 2</span><span class="sxs-lookup"><span data-stu-id="ee895-170">East US 2</span></span> |
| &nbsp; | <span data-ttu-id="ee895-171">美國中部</span><span class="sxs-lookup"><span data-stu-id="ee895-171">Central US</span></span> | <span data-ttu-id="ee895-172">美國中部</span><span class="sxs-lookup"><span data-stu-id="ee895-172">Central US</span></span> |
| &nbsp; | <span data-ttu-id="ee895-173">美國中北部</span><span class="sxs-lookup"><span data-stu-id="ee895-173">North Central US</span></span> | <span data-ttu-id="ee895-174">美國中北部</span><span class="sxs-lookup"><span data-stu-id="ee895-174">North Central US</span></span> |
| &nbsp; | <span data-ttu-id="ee895-175">美國中南部</span><span class="sxs-lookup"><span data-stu-id="ee895-175">South Central US</span></span> | <span data-ttu-id="ee895-176">美國中南部</span><span class="sxs-lookup"><span data-stu-id="ee895-176">South Central US</span></span> |
| &nbsp; | <span data-ttu-id="ee895-177">美國中西部</span><span class="sxs-lookup"><span data-stu-id="ee895-177">West Central US</span></span> | <span data-ttu-id="ee895-178">美國中西部</span><span class="sxs-lookup"><span data-stu-id="ee895-178">West Central US</span></span> |
| &nbsp; | <span data-ttu-id="ee895-179">美國西部</span><span class="sxs-lookup"><span data-stu-id="ee895-179">West US</span></span> | <span data-ttu-id="ee895-180">美國西部</span><span class="sxs-lookup"><span data-stu-id="ee895-180">West US</span></span> |
| &nbsp; | <span data-ttu-id="ee895-181">美國西部 2</span><span class="sxs-lookup"><span data-stu-id="ee895-181">West US 2</span></span> | <span data-ttu-id="ee895-182">美國西部</span><span class="sxs-lookup"><span data-stu-id="ee895-182">West US</span></span> |
| <span data-ttu-id="ee895-183">加拿大</span><span class="sxs-lookup"><span data-stu-id="ee895-183">Canada</span></span> | <span data-ttu-id="ee895-184">加拿大東部</span><span class="sxs-lookup"><span data-stu-id="ee895-184">Canada East</span></span> | <span data-ttu-id="ee895-185">加拿大中部</span><span class="sxs-lookup"><span data-stu-id="ee895-185">Canada Central</span></span> |
| &nbsp; | <span data-ttu-id="ee895-186">加拿大中部</span><span class="sxs-lookup"><span data-stu-id="ee895-186">Canada Central</span></span> | <span data-ttu-id="ee895-187">加拿大中部</span><span class="sxs-lookup"><span data-stu-id="ee895-187">Canada Central</span></span> |
| <span data-ttu-id="ee895-188">巴西</span><span class="sxs-lookup"><span data-stu-id="ee895-188">Brazil</span></span> | <span data-ttu-id="ee895-189">巴西南部</span><span class="sxs-lookup"><span data-stu-id="ee895-189">Brazil South</span></span> | <span data-ttu-id="ee895-190">巴西南部</span><span class="sxs-lookup"><span data-stu-id="ee895-190">Brazil South</span></span> |
| <span data-ttu-id="ee895-191">歐洲</span><span class="sxs-lookup"><span data-stu-id="ee895-191">Europe</span></span> | <span data-ttu-id="ee895-192">北歐</span><span class="sxs-lookup"><span data-stu-id="ee895-192">North Europe</span></span> | <span data-ttu-id="ee895-193">北歐</span><span class="sxs-lookup"><span data-stu-id="ee895-193">North Europe</span></span> |
| &nbsp; | <span data-ttu-id="ee895-194">西歐</span><span class="sxs-lookup"><span data-stu-id="ee895-194">West Europe</span></span> | <span data-ttu-id="ee895-195">西歐</span><span class="sxs-lookup"><span data-stu-id="ee895-195">West Europe</span></span> |
| <span data-ttu-id="ee895-196">英國</span><span class="sxs-lookup"><span data-stu-id="ee895-196">United Kingdom</span></span> | <span data-ttu-id="ee895-197">英國西部</span><span class="sxs-lookup"><span data-stu-id="ee895-197">UK West</span></span> | <span data-ttu-id="ee895-198">英國南部</span><span class="sxs-lookup"><span data-stu-id="ee895-198">UK South</span></span> |
| &nbsp; | <span data-ttu-id="ee895-199">英國南部</span><span class="sxs-lookup"><span data-stu-id="ee895-199">UK South</span></span> | <span data-ttu-id="ee895-200">英國南部</span><span class="sxs-lookup"><span data-stu-id="ee895-200">UK South</span></span> |
| <span data-ttu-id="ee895-201">亞太地區</span><span class="sxs-lookup"><span data-stu-id="ee895-201">Asia Pacific</span></span> | <span data-ttu-id="ee895-202">東南亞</span><span class="sxs-lookup"><span data-stu-id="ee895-202">Southeast Asia</span></span> | <span data-ttu-id="ee895-203">東南亞</span><span class="sxs-lookup"><span data-stu-id="ee895-203">Southeast Asia</span></span> |
| &nbsp; | <span data-ttu-id="ee895-204">東亞</span><span class="sxs-lookup"><span data-stu-id="ee895-204">East Asia</span></span> | <span data-ttu-id="ee895-205">東南亞</span><span class="sxs-lookup"><span data-stu-id="ee895-205">Southeast Asia</span></span> |
| <span data-ttu-id="ee895-206">澳大利亞</span><span class="sxs-lookup"><span data-stu-id="ee895-206">Australia</span></span> | <span data-ttu-id="ee895-207">澳洲東部</span><span class="sxs-lookup"><span data-stu-id="ee895-207">Australia East</span></span> | <span data-ttu-id="ee895-208">澳洲東部</span><span class="sxs-lookup"><span data-stu-id="ee895-208">Australia East</span></span> |
| &nbsp; | <span data-ttu-id="ee895-209">澳大利亞東南部</span><span class="sxs-lookup"><span data-stu-id="ee895-209">Australia Southeast</span></span> | <span data-ttu-id="ee895-210">澳大利亞東南部</span><span class="sxs-lookup"><span data-stu-id="ee895-210">Australia Southeast</span></span> |
| <span data-ttu-id="ee895-211">日本</span><span class="sxs-lookup"><span data-stu-id="ee895-211">Japan</span></span> | <span data-ttu-id="ee895-212">日本東部</span><span class="sxs-lookup"><span data-stu-id="ee895-212">Japan East</span></span> | <span data-ttu-id="ee895-213">日本東部</span><span class="sxs-lookup"><span data-stu-id="ee895-213">Japan East</span></span> |
| &nbsp; | <span data-ttu-id="ee895-214">日本西部</span><span class="sxs-lookup"><span data-stu-id="ee895-214">Japan West</span></span> | <span data-ttu-id="ee895-215">日本東部</span><span class="sxs-lookup"><span data-stu-id="ee895-215">Japan East</span></span> |
| <span data-ttu-id="ee895-216">印度</span><span class="sxs-lookup"><span data-stu-id="ee895-216">India</span></span> | <span data-ttu-id="ee895-217">印度中部</span><span class="sxs-lookup"><span data-stu-id="ee895-217">Central India</span></span> | <span data-ttu-id="ee895-218">印度中部</span><span class="sxs-lookup"><span data-stu-id="ee895-218">Central India</span></span> |
| &nbsp; | <span data-ttu-id="ee895-219">印度西部</span><span class="sxs-lookup"><span data-stu-id="ee895-219">West India</span></span> | <span data-ttu-id="ee895-220">印度中部</span><span class="sxs-lookup"><span data-stu-id="ee895-220">Central India</span></span> |
| &nbsp; | <span data-ttu-id="ee895-221">印度南部</span><span class="sxs-lookup"><span data-stu-id="ee895-221">South India</span></span> | <span data-ttu-id="ee895-222">印度中部</span><span class="sxs-lookup"><span data-stu-id="ee895-222">Central India</span></span> |

<span data-ttu-id="ee895-223">或者，您可以明確指出的 Data Factory 服務 toobe hello 區域中，藉由指定使用 tooperform hello 複製`executionLocation`下複製活動的屬性`typeProperties`。</span><span class="sxs-lookup"><span data-stu-id="ee895-223">Alternatively, you can explicitly indicate hello region of Data Factory service toobe used tooperform hello copy by specifying `executionLocation` property under Copy Activity `typeProperties`.</span></span> <span data-ttu-id="ee895-224">這個屬性支援的值詳列於上述**用於資料移動的區域**資料行。</span><span class="sxs-lookup"><span data-stu-id="ee895-224">Supported values for this property are listed in above **Region used for data movement** column.</span></span> <span data-ttu-id="ee895-225">請注意您的資料會通過該區域網路上 hello 傳輸進行複製時。</span><span class="sxs-lookup"><span data-stu-id="ee895-225">Note your data goes through that region over hello wire during copy.</span></span> <span data-ttu-id="ee895-226">例如 toocopy Azure 之間會儲存在韓國，您可以指定`"executionLocation": "Japan East"`tooroute 透過日本地區 (請參閱[範例 JSON](#by-using-json-scripts)做為參考)。</span><span class="sxs-lookup"><span data-stu-id="ee895-226">For example, toocopy between Azure stores in Korea, you can specify `"executionLocation": "Japan East"` tooroute through Japan region (see [sample JSON](#by-using-json-scripts) as reference).</span></span>

> [!NOTE]
> <span data-ttu-id="ee895-227">如果 hello 目的地資料存放區的 hello 區域不在上述清單中或無法偵測預設複製活動失敗而不是透過替代地區中，除非`executionLocation`指定。</span><span class="sxs-lookup"><span data-stu-id="ee895-227">If hello region of hello destination data store is not in preceding list or undetectable, by default Copy Activity fails instead of going through an alternative region, unless `executionLocation` is specified.</span></span> <span data-ttu-id="ee895-228">經過一段時間，將會展開 hello 支援區域清單。</span><span class="sxs-lookup"><span data-stu-id="ee895-228">hello supported region list will be expanded over time.</span></span>
>

### <a name="copy-data-between-an-on-premises-data-store-and-a-cloud-data-store"></a><span data-ttu-id="ee895-229">在內部部署資料存放區和雲端資料存放區之間複製資料</span><span class="sxs-lookup"><span data-stu-id="ee895-229">Copy data between an on-premises data store and a cloud data store</span></span>
<span data-ttu-id="ee895-230">在內部部署存放區 (或 Azure 虛擬機器/IaaS) 與雲端存放區之間複製資料時， [資料管理閘道](data-factory-data-management-gateway.md) 會在內部部署機器或虛擬機器上執行資料移動。</span><span class="sxs-lookup"><span data-stu-id="ee895-230">When data is being copied between on-premises (or Azure virtual machines/IaaS) and cloud stores, [Data Management Gateway](data-factory-data-management-gateway.md) performs data movement on an on-premises machine or virtual machine.</span></span> <span data-ttu-id="ee895-231">hello 資料不流經 hello 服務在 hello 雲端中，除非您使用 hello[分段複製](data-factory-copy-activity-performance.md#staged-copy)功能。</span><span class="sxs-lookup"><span data-stu-id="ee895-231">hello data does not flow through hello service in hello cloud, unless you use hello [staged copy](data-factory-copy-activity-performance.md#staged-copy) capability.</span></span> <span data-ttu-id="ee895-232">在此情況下，資料流經 hello 寫入 hello 接收資料存放區之前，請執行 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="ee895-232">In this case, data flows through hello staging Azure Blob storage before it is written into hello sink data store.</span></span>

## <a name="create-a-pipeline-with-copy-activity"></a><span data-ttu-id="ee895-233">建立具有複製活動的管線</span><span class="sxs-lookup"><span data-stu-id="ee895-233">Create a pipeline with Copy Activity</span></span>
<span data-ttu-id="ee895-234">您可以使用幾個方式來建立具有「複製活動」的管線︰</span><span class="sxs-lookup"><span data-stu-id="ee895-234">You can create a pipeline with Copy Activity in a couple of ways:</span></span>

### <a name="by-using-hello-copy-wizard"></a><span data-ttu-id="ee895-235">使用 hello 複製精靈</span><span class="sxs-lookup"><span data-stu-id="ee895-235">By using hello Copy Wizard</span></span>
<span data-ttu-id="ee895-236">hello 資料 Factory 複製精靈可協助您 toocreate 具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="ee895-236">hello Data Factory Copy Wizard helps you toocreate a pipeline with Copy Activity.</span></span> <span data-ttu-id="ee895-237">這個管線可讓您從支援的來源 toodestinations toocopy 資料*而不需要撰寫 JSON*定義連結的服務、 資料集和管線。</span><span class="sxs-lookup"><span data-stu-id="ee895-237">This pipeline allows you toocopy data from supported sources toodestinations *without writing JSON* definitions for linked services, datasets, and pipelines.</span></span> <span data-ttu-id="ee895-238">請參閱[資料 Factory 複製精靈](data-factory-copy-wizard.md)hello 精靈的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ee895-238">See [Data Factory Copy Wizard](data-factory-copy-wizard.md) for details about hello wizard.</span></span>  

### <a name="by-using-json-scripts"></a><span data-ttu-id="ee895-239">透過使用 JSON 指令碼</span><span class="sxs-lookup"><span data-stu-id="ee895-239">By using JSON scripts</span></span>
<span data-ttu-id="ee895-240">您可以使用 Data Factory 編輯器 hello Azure 入口網站、 Visual Studio 中或 Azure PowerShell toocreate JSON 定義中的管線 （透過使用複製活動）。</span><span class="sxs-lookup"><span data-stu-id="ee895-240">You can use Data Factory Editor in hello Azure portal, Visual Studio, or Azure PowerShell toocreate a JSON definition for a pipeline (by using Copy Activity).</span></span> <span data-ttu-id="ee895-241">然後，您可以部署 toocreate Data Factory 中的 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="ee895-241">Then, you can deploy it toocreate hello pipeline in Data Factory.</span></span> <span data-ttu-id="ee895-242">如需含有逐步指示的教學課程，請參閱 [教學課程：在 Azure Data Factory 管線中使用複製活動](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 。</span><span class="sxs-lookup"><span data-stu-id="ee895-242">See [Tutorial: Use Copy Activity in an Azure Data Factory pipeline](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for a tutorial with step-by-step instructions.</span></span>    

<span data-ttu-id="ee895-243">JSON 屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="ee895-243">JSON properties (such as name, description, input and output tables, and policies) are available for all types of activities.</span></span> <span data-ttu-id="ee895-244">屬性可用在 hello `typeProperties` hello 活動的區段會隨每個活動類型。</span><span class="sxs-lookup"><span data-stu-id="ee895-244">Properties that are available in hello `typeProperties` section of hello activity vary with each activity type.</span></span>

<span data-ttu-id="ee895-245">複製活動 hello`typeProperties`區段有所不同 hello 類型的來源和接收。</span><span class="sxs-lookup"><span data-stu-id="ee895-245">For Copy Activity, hello `typeProperties` section varies depending on hello types of sources and sinks.</span></span> <span data-ttu-id="ee895-246">按一下來源/接收器中 hello[支援來源與接收](#supported-data-stores-and-formats)區段 toolearn 有關針對該資料存放區的複製活動支援的型別屬性。</span><span class="sxs-lookup"><span data-stu-id="ee895-246">Click a source/sink in hello [Supported sources and sinks](#supported-data-stores-and-formats) section toolearn about type properties that Copy Activity supports for that data store.</span></span>

<span data-ttu-id="ee895-247">以下是範例 JSON 定義︰</span><span class="sxs-lookup"><span data-stu-id="ee895-247">Here's a sample JSON definition:</span></span>

```json
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from Azure blob tooAzure SQL table",
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
<span data-ttu-id="ee895-248">hello 排程 hello 中定義的輸出資料集可讓您判斷 hello 活動執行時 (例如：**每日**，頻率，做為**天**，以及做為間隔**1**)。</span><span class="sxs-lookup"><span data-stu-id="ee895-248">hello schedule that is defined in hello output dataset determines when hello activity runs (for example: **daily**, frequency as **day**, and interval as **1**).</span></span> <span data-ttu-id="ee895-249">hello 活動會將資料從輸入資料集 (**來源**) tooan 輸出資料集 (**接收**)。</span><span class="sxs-lookup"><span data-stu-id="ee895-249">hello activity copies data from an input dataset (**source**) tooan output dataset (**sink**).</span></span>

<span data-ttu-id="ee895-250">您可以指定多個輸入資料集 tooCopy 活動。</span><span class="sxs-lookup"><span data-stu-id="ee895-250">You can specify more than one input dataset tooCopy Activity.</span></span> <span data-ttu-id="ee895-251">Hello 活動開始執行前，它們是使用的 tooverify hello 相依性。</span><span class="sxs-lookup"><span data-stu-id="ee895-251">They are used tooverify hello dependencies before hello activity is run.</span></span> <span data-ttu-id="ee895-252">不過，只有 hello 從 hello 第一個資料集的資料是複製的 toohello 目的地資料集。</span><span class="sxs-lookup"><span data-stu-id="ee895-252">However, only hello data from hello first dataset is copied toohello destination dataset.</span></span> <span data-ttu-id="ee895-253">如需詳細資訊，請參閱 [排程和執行](data-factory-scheduling-and-execution.md)。</span><span class="sxs-lookup"><span data-stu-id="ee895-253">For more information, see [Scheduling and execution](data-factory-scheduling-and-execution.md).</span></span>  

## <a name="performance-and-tuning"></a><span data-ttu-id="ee895-254">效能和微調</span><span class="sxs-lookup"><span data-stu-id="ee895-254">Performance and tuning</span></span>
<span data-ttu-id="ee895-255">請參閱 hello[複製活動效能及微調指南](data-factory-copy-activity-performance.md)，其中描述 Azure Data Factory 中的資料移動 （複製活動） 的 hello 效能影響的關鍵因素。</span><span class="sxs-lookup"><span data-stu-id="ee895-255">See hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md), which describes key factors that affect hello performance of data movement (Copy Activity) in Azure Data Factory.</span></span> <span data-ttu-id="ee895-256">它也列出 hello 觀察到在內部測試期間的效能，並討論各種方式 toooptimize hello 複製活動的效能。</span><span class="sxs-lookup"><span data-stu-id="ee895-256">It also lists hello observed performance during internal testing and discusses various ways toooptimize hello performance of Copy Activity.</span></span>

## <a name="fault-tolerance"></a><span data-ttu-id="ee895-257">容錯</span><span class="sxs-lookup"><span data-stu-id="ee895-257">Fault tolerance</span></span>
<span data-ttu-id="ee895-258">根據預設，複製活動將會停止複製資料以及傳回失敗時遇到不相容的資料來源與接收器; 之間雖然您可以明確地設定 tooskip 和記錄檔 hello 不相容的資料列只複製這些相容的資料 toomake hello 複製成功。</span><span class="sxs-lookup"><span data-stu-id="ee895-258">By default, copy activity will stop copying data and return failure when encounter incompatible data between source and sink; while you can explicitly configure tooskip and log hello incompatible rows and only copy those compatible data toomake hello copy succeeded.</span></span> <span data-ttu-id="ee895-259">請參閱 hello[複製活動容錯](data-factory-copy-activity-fault-tolerance.md)上更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ee895-259">See hello [Copy Activity fault tolerance](data-factory-copy-activity-fault-tolerance.md) on more details.</span></span>

## <a name="security-considerations"></a><span data-ttu-id="ee895-260">安全性考量</span><span class="sxs-lookup"><span data-stu-id="ee895-260">Security considerations</span></span>
<span data-ttu-id="ee895-261">請參閱 hello[安全性考量](data-factory-data-movement-security-considerations.md)，其中描述 Azure Data Factory 中的資料移動服務使用 toosecure 您資料的安全性基礎結構。</span><span class="sxs-lookup"><span data-stu-id="ee895-261">See hello [Security considerations](data-factory-data-movement-security-considerations.md), which describes security infrastructure that data movement services in Azure Data Factory use toosecure your data.</span></span>

## <a name="scheduling-and-sequential-copy"></a><span data-ttu-id="ee895-262">排程和循序複製</span><span class="sxs-lookup"><span data-stu-id="ee895-262">Scheduling and sequential copy</span></span>
<span data-ttu-id="ee895-263">請參閱 [排程和執行](data-factory-scheduling-and-execution.md) ，以取得排程和執行在 Data Factory 中如何運作的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="ee895-263">See [Scheduling and execution](data-factory-scheduling-and-execution.md) for detailed information about how scheduling and execution works in Data Factory.</span></span> <span data-ttu-id="ee895-264">它是可能 toorun 多項複製作業逐一循序/排序的方式。</span><span class="sxs-lookup"><span data-stu-id="ee895-264">It is possible toorun multiple copy operations one after another in a sequential/ordered manner.</span></span> <span data-ttu-id="ee895-265">請參閱 hello[循序複製](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)> 一節。</span><span class="sxs-lookup"><span data-stu-id="ee895-265">See hello [Copy sequentially](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) section.</span></span>

## <a name="type-conversions"></a><span data-ttu-id="ee895-266">類型轉換</span><span class="sxs-lookup"><span data-stu-id="ee895-266">Type conversions</span></span>
<span data-ttu-id="ee895-267">不同的資料存放區有不同的原生類型系統。</span><span class="sxs-lookup"><span data-stu-id="ee895-267">Different data stores have different native type systems.</span></span> <span data-ttu-id="ee895-268">複製活動與 hello 下列兩種方法執行從來源類型 toosink 類型的自動類型轉換：</span><span class="sxs-lookup"><span data-stu-id="ee895-268">Copy Activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="ee895-269">從原生的來源類型 tooa.NET 型別轉換。</span><span class="sxs-lookup"><span data-stu-id="ee895-269">Convert from native source types tooa .NET type.</span></span>
2. <span data-ttu-id="ee895-270">從.NET 型別 tooa 原生接收類型轉換。</span><span class="sxs-lookup"><span data-stu-id="ee895-270">Convert from a .NET type tooa native sink type.</span></span>

<span data-ttu-id="ee895-271">從資料存放區的原生型別系統 tooa.NET 型別 hello 對應是 hello 各自的資料存放區文件中。</span><span class="sxs-lookup"><span data-stu-id="ee895-271">hello mapping from a native type system tooa .NET type for a data store is in hello respective data store article.</span></span> <span data-ttu-id="ee895-272">(按一下 hello 特定連結在 hello[支援資料存放區](#supported-data-stores)資料表)。</span><span class="sxs-lookup"><span data-stu-id="ee895-272">(Click hello specific link in hello [Supported data stores](#supported-data-stores) table).</span></span> <span data-ttu-id="ee895-273">以便複製活動會執行 hello 右邊轉換，您可以建立您的資料表時使用這些對應 toodetermine 適當類型。</span><span class="sxs-lookup"><span data-stu-id="ee895-273">You can use these mappings toodetermine appropriate types while creating your tables, so that Copy Activity performs hello right conversions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee895-274">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ee895-274">Next steps</span></span>
* <span data-ttu-id="ee895-275">toolearn 有關 hello 複製活動，請參閱[將資料從 Azure Blob 儲存體 tooAzure SQL Database 複製](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="ee895-275">toolearn about hello Copy Activity more, see [Copy data from Azure Blob storage tooAzure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
* <span data-ttu-id="ee895-276">toolearn 有關將資料從內部部署資料存放區 tooa 雲端資料儲存區，請參閱[將資料從內部部署 toocloud 資料存放區移](data-factory-move-data-between-onprem-and-cloud.md)。</span><span class="sxs-lookup"><span data-stu-id="ee895-276">toolearn about moving data from an on-premises data store tooa cloud data store, see [Move data from on-premises toocloud data stores](data-factory-move-data-between-onprem-and-cloud.md).</span></span>
