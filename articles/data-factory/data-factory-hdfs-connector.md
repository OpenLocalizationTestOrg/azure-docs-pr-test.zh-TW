---
title: "從內部部署 HDFS aaaMove 資料 |Microsoft 文件"
description: "深入了解如何 toomove 資料從內部部署 HDFS 使用 Azure Data Factory。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3215b82d-291a-46db-8478-eac1a3219614
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 96387e5dd089099fc2e983ab26d67c2044b973b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-on-premises-hdfs-using-azure-data-factory"></a><span data-ttu-id="ceceb-103">使用 Azure Data Factory 從內部部署的 HDFS 移動資料</span><span class="sxs-lookup"><span data-stu-id="ceceb-103">Move data from on-premises HDFS using Azure Data Factory</span></span>
<span data-ttu-id="ceceb-104">本文說明如何 toouse hello Azure Data Factory toomove 資料從內部部署 HDFS 中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="ceceb-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises HDFS.</span></span> <span data-ttu-id="ceceb-105">它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="ceceb-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="ceceb-106">您可以從 HDFS tooany 支援接收資料存放區複製資料。</span><span class="sxs-lookup"><span data-stu-id="ceceb-106">You can copy data from HDFS tooany supported sink data store.</span></span> <span data-ttu-id="ceceb-107">取得一份資料存放區支援接收由 hello 複製活動時，請參閱 hello[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)資料表。</span><span class="sxs-lookup"><span data-stu-id="ceceb-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="ceceb-108">資料處理站目前支援從內部部署 HDFS tooother 資料存放區，只有移動資料，但不適用於將資料從其他資料存放區 tooan 內部部署 HDFS。</span><span class="sxs-lookup"><span data-stu-id="ceceb-108">Data factory currently supports only moving data from an on-premises HDFS tooother data stores, but not for moving data from other data stores tooan on-premises HDFS.</span></span>

> [!NOTE]
> <span data-ttu-id="ceceb-109">複製活動不會刪除 hello 原始程式檔之後順利複製的 toohello 目的地。</span><span class="sxs-lookup"><span data-stu-id="ceceb-109">Copy Activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="ceceb-110">如果您需要 toodelete hello 原始程式檔複製成功之後，建立自訂活動 toodelete hello 檔案，並使用 hello 管線中的 hello 活動。</span><span class="sxs-lookup"><span data-stu-id="ceceb-110">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file and use hello activity in hello pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="ceceb-111">啟用連線</span><span class="sxs-lookup"><span data-stu-id="ceceb-111">Enabling connectivity</span></span>
<span data-ttu-id="ceceb-112">資料 Factory 服務支援使用 hello 資料管理閘道的連線 tooon 內部部署 HDFS。</span><span class="sxs-lookup"><span data-stu-id="ceceb-112">Data Factory service supports connecting tooon-premises HDFS using hello Data Management Gateway.</span></span> <span data-ttu-id="ceceb-113">請參閱[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)文章 toolearn 有關資料管理閘道器和 hello 閘道設定的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="ceceb-113">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span> <span data-ttu-id="ceceb-114">使用 hello 閘道 tooconnect tooHDFS，即使它裝載於 Azure IaaS VM。</span><span class="sxs-lookup"><span data-stu-id="ceceb-114">Use hello gateway tooconnect tooHDFS even if it is hosted in an Azure IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="ceceb-115">請確定 hello 資料管理閘道器可以存取太**所有**hello [節點名稱伺服器]: [name] 節點的連接埠] 和 [資料節點的伺服器]: [資料節點連接埠] hello Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="ceceb-115">Make sure hello Data Management Gateway can access too**ALL** hello [name node server]:[name node port] and [data node servers]:[data node port] of hello Hadoop cluster.</span></span> <span data-ttu-id="ceceb-116">預設 [名稱節點連接埠] 是 50070，而預設 [資料節點連接埠] 是 50075。</span><span class="sxs-lookup"><span data-stu-id="ceceb-116">Default [name node port] is 50070, and default [data node port] is 50075.</span></span>

<span data-ttu-id="ceceb-117">雖然您可以在 hello 上安裝閘道相同內部電腦或 hello Azure VM hello HDFS，我們建議您在個別機器/Azure IaaS VM 上安裝 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="ceceb-117">While you can install gateway on hello same on-premises machine or hello Azure VM as hello HDFS, we recommend that you install hello gateway on a separate machine/Azure IaaS VM.</span></span> <span data-ttu-id="ceceb-118">在個別機器上安裝閘道器可減少資源爭用並改善效能。</span><span class="sxs-lookup"><span data-stu-id="ceceb-118">Having gateway on a separate machine reduces resource contention and improves performance.</span></span> <span data-ttu-id="ceceb-119">當您在不同電腦上安裝 hello 閘道時，hello 部應該以 hello HDFS 無法 tooaccess hello 機器。</span><span class="sxs-lookup"><span data-stu-id="ceceb-119">When you install hello gateway on a separate machine, hello machine should be able tooaccess hello machine with hello HDFS.</span></span>

## <a name="getting-started"></a><span data-ttu-id="ceceb-120">開始使用</span><span class="sxs-lookup"><span data-stu-id="ceceb-120">Getting started</span></span>
<span data-ttu-id="ceceb-121">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從 HDFS 來源移動資料。</span><span class="sxs-lookup"><span data-stu-id="ceceb-121">You can create a pipeline with a copy activity that moves data from a HDFS source by using different tools/APIs.</span></span>

<span data-ttu-id="ceceb-122">最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="ceceb-122">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="ceceb-123">請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。</span><span class="sxs-lookup"><span data-stu-id="ceceb-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="ceceb-124">您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。</span><span class="sxs-lookup"><span data-stu-id="ceceb-124">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="ceceb-125">請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="ceceb-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="ceceb-126">無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:</span><span class="sxs-lookup"><span data-stu-id="ceceb-126">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="ceceb-127">建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="ceceb-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="ceceb-128">建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。</span><span class="sxs-lookup"><span data-stu-id="ceceb-128">Create **datasets** toorepresent input and output data for hello copy operation.</span></span>
3. <span data-ttu-id="ceceb-129">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="ceceb-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="ceceb-130">當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="ceceb-130">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="ceceb-131">當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="ceceb-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="ceceb-132">使用 Data Factory 實體的 HDFS 資料存放區中的使用的 toocopy 資料的 JSON 定義中的範例，請參閱[JSON 範例： 將資料從內部部署 HDFS tooAzure Blob 複製](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob)本文一節。</span><span class="sxs-lookup"><span data-stu-id="ceceb-132">For a sample with JSON definitions for Data Factory entities that are used toocopy data from a HDFS data store, see [JSON example: Copy data from on-premises HDFS tooAzure Blob](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) section of this article.</span></span>

<span data-ttu-id="ceceb-133">hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooHDFS 的 JSON 屬性的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="ceceb-133">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooHDFS:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="ceceb-134">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="ceceb-134">Linked service properties</span></span>
<span data-ttu-id="ceceb-135">連結的服務連結資料儲存區 tooa data factory。</span><span class="sxs-lookup"><span data-stu-id="ceceb-135">A linked service links a data store tooa data factory.</span></span> <span data-ttu-id="ceceb-136">您建立連結的服務型別的**Hdfs** toolink 在內部部署 HDFS tooyour 資料處理站。</span><span class="sxs-lookup"><span data-stu-id="ceceb-136">You create a linked service of type **Hdfs** toolink an on-premises HDFS tooyour data factory.</span></span> <span data-ttu-id="ceceb-137">下表中的 hello 提供 JSON 項目特定 tooHDFS 連結服務的描述。</span><span class="sxs-lookup"><span data-stu-id="ceceb-137">hello following table provides description for JSON elements specific tooHDFS linked service.</span></span>

| <span data-ttu-id="ceceb-138">屬性</span><span class="sxs-lookup"><span data-stu-id="ceceb-138">Property</span></span> | <span data-ttu-id="ceceb-139">說明</span><span class="sxs-lookup"><span data-stu-id="ceceb-139">Description</span></span> | <span data-ttu-id="ceceb-140">必要</span><span class="sxs-lookup"><span data-stu-id="ceceb-140">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ceceb-141">類型</span><span class="sxs-lookup"><span data-stu-id="ceceb-141">type</span></span> |<span data-ttu-id="ceceb-142">hello 類型屬性必須設定為： **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="ceceb-142">hello type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="ceceb-143">是</span><span class="sxs-lookup"><span data-stu-id="ceceb-143">Yes</span></span> |
| <span data-ttu-id="ceceb-144">Url</span><span class="sxs-lookup"><span data-stu-id="ceceb-144">Url</span></span> |<span data-ttu-id="ceceb-145">URL toohello HDFS</span><span class="sxs-lookup"><span data-stu-id="ceceb-145">URL toohello HDFS</span></span> |<span data-ttu-id="ceceb-146">是</span><span class="sxs-lookup"><span data-stu-id="ceceb-146">Yes</span></span> |
| <span data-ttu-id="ceceb-147">authenticationType</span><span class="sxs-lookup"><span data-stu-id="ceceb-147">authenticationType</span></span> |<span data-ttu-id="ceceb-148">匿名或 Windows。</span><span class="sxs-lookup"><span data-stu-id="ceceb-148">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="ceceb-149">toouse **Kerberos 驗證**HDFS 連接器，請參閱太[本節](#use-kerberos-authentication-for-hdfs-connector)在內部部署環境 tooset 據此。</span><span class="sxs-lookup"><span data-stu-id="ceceb-149">toouse **Kerberos authentication** for HDFS connector, refer too[this section](#use-kerberos-authentication-for-hdfs-connector) tooset up your on-premises environment accordingly.</span></span> |<span data-ttu-id="ceceb-150">是</span><span class="sxs-lookup"><span data-stu-id="ceceb-150">Yes</span></span> |
| <span data-ttu-id="ceceb-151">userName</span><span class="sxs-lookup"><span data-stu-id="ceceb-151">userName</span></span> |<span data-ttu-id="ceceb-152">Windows 驗證的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="ceceb-152">Username for Windows authentication.</span></span> |<span data-ttu-id="ceceb-153">是 (適用於 Windows 驗證)</span><span class="sxs-lookup"><span data-stu-id="ceceb-153">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="ceceb-154">password</span><span class="sxs-lookup"><span data-stu-id="ceceb-154">password</span></span> |<span data-ttu-id="ceceb-155">Windows 驗證的密碼。</span><span class="sxs-lookup"><span data-stu-id="ceceb-155">Password for Windows authentication.</span></span> |<span data-ttu-id="ceceb-156">是 (適用於 Windows 驗證)</span><span class="sxs-lookup"><span data-stu-id="ceceb-156">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="ceceb-157">gatewayName</span><span class="sxs-lookup"><span data-stu-id="ceceb-157">gatewayName</span></span> |<span data-ttu-id="ceceb-158">Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello HDFS。</span><span class="sxs-lookup"><span data-stu-id="ceceb-158">Name of hello gateway that hello Data Factory service should use tooconnect toohello HDFS.</span></span> |<span data-ttu-id="ceceb-159">是</span><span class="sxs-lookup"><span data-stu-id="ceceb-159">Yes</span></span> |
| <span data-ttu-id="ceceb-160">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="ceceb-160">encryptedCredential</span></span> |<span data-ttu-id="ceceb-161">[新 AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) hello 存取認證的輸出。</span><span class="sxs-lookup"><span data-stu-id="ceceb-161">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of hello access credential.</span></span> |<span data-ttu-id="ceceb-162">否</span><span class="sxs-lookup"><span data-stu-id="ceceb-162">No</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="ceceb-163">使用匿名驗證</span><span class="sxs-lookup"><span data-stu-id="ceceb-163">Using Anonymous authentication</span></span>

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-windows-authentication"></a><span data-ttu-id="ceceb-164">使用 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="ceceb-164">Using Windows authentication</span></span>

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```
## <a name="dataset-properties"></a><span data-ttu-id="ceceb-165">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="ceceb-165">Dataset properties</span></span>
<span data-ttu-id="ceceb-166">區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="ceceb-166">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="ceceb-167">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="ceceb-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="ceceb-168">hello **typeProperties**區段是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ceceb-168">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="ceceb-169">hello typeProperties 區段類型的資料集**FileShare** （包括 HDFS 資料集） 具有下列屬性的 hello</span><span class="sxs-lookup"><span data-stu-id="ceceb-169">hello typeProperties section for dataset of type **FileShare** (which includes HDFS dataset) has hello following properties</span></span>

| <span data-ttu-id="ceceb-170">屬性</span><span class="sxs-lookup"><span data-stu-id="ceceb-170">Property</span></span> | <span data-ttu-id="ceceb-171">說明</span><span class="sxs-lookup"><span data-stu-id="ceceb-171">Description</span></span> | <span data-ttu-id="ceceb-172">必要</span><span class="sxs-lookup"><span data-stu-id="ceceb-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ceceb-173">folderPath</span><span class="sxs-lookup"><span data-stu-id="ceceb-173">folderPath</span></span> |<span data-ttu-id="ceceb-174">路徑 toohello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="ceceb-174">Path toohello folder.</span></span> <span data-ttu-id="ceceb-175">範例： `myfolder`</span><span class="sxs-lookup"><span data-stu-id="ceceb-175">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="ceceb-176">使用逸出字元 '\' hello 字串中的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="ceceb-176">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="ceceb-177">例如︰若為 folder\subfolder，請指定 folder\\\\subfolder；若為 d:\samplefolder，請指定 d:\\\\samplefolder。</span><span class="sxs-lookup"><span data-stu-id="ceceb-177">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="ceceb-178">您可以結合此屬性與**partitionBy** toohave 資料夾路徑根據配量開始/結束日期時間。</span><span class="sxs-lookup"><span data-stu-id="ceceb-178">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="ceceb-179">是</span><span class="sxs-lookup"><span data-stu-id="ceceb-179">Yes</span></span> |
| <span data-ttu-id="ceceb-180">fileName</span><span class="sxs-lookup"><span data-stu-id="ceceb-180">fileName</span></span> |<span data-ttu-id="ceceb-181">在 hello 指定 hello hello 檔案名稱**folderPath**如果您想 hello 資料表 toorefer tooa 特定檔案 hello 資料夾中的。</span><span class="sxs-lookup"><span data-stu-id="ceceb-181">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="ceceb-182">如果您未指定任何值，這個屬性，hello 資料表會指向 tooall hello 資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="ceceb-182">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="ceceb-183">檔案名稱未指定輸出資料集，hello hello 產生檔案名稱會在 hello 遵循此格式：</span><span class="sxs-lookup"><span data-stu-id="ceceb-183">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="ceceb-184">Data<Guid>.txt (例如：Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="ceceb-184">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="ceceb-185">否</span><span class="sxs-lookup"><span data-stu-id="ceceb-185">No</span></span> |
| <span data-ttu-id="ceceb-186">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="ceceb-186">partitionedBy</span></span> |<span data-ttu-id="ceceb-187">partitionedBy 可以是使用的 toospecify 動態 folderPath，時間序列資料的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="ceceb-187">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="ceceb-188">範例：folderPath 可針對每小時的資料進行參數化。</span><span class="sxs-lookup"><span data-stu-id="ceceb-188">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="ceceb-189">否</span><span class="sxs-lookup"><span data-stu-id="ceceb-189">No</span></span> |
| <span data-ttu-id="ceceb-190">format</span><span class="sxs-lookup"><span data-stu-id="ceceb-190">format</span></span> | <span data-ttu-id="ceceb-191">支援下列格式類型的 hello: **TextFormat**， **JsonFormat**， **AvroFormat**， **OrcFormat**， **ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="ceceb-191">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="ceceb-192">設定 hello**類型**下格式 tooone 這些值的屬性。</span><span class="sxs-lookup"><span data-stu-id="ceceb-192">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="ceceb-193">如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。</span><span class="sxs-lookup"><span data-stu-id="ceceb-193">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="ceceb-194">如果您想太**複製檔做為-是**之間以檔案為基礎存放區 （二進位複製），略過這兩個輸入和輸出資料集定義中的 hello 格式 > 一節。</span><span class="sxs-lookup"><span data-stu-id="ceceb-194">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="ceceb-195">否</span><span class="sxs-lookup"><span data-stu-id="ceceb-195">No</span></span> |
| <span data-ttu-id="ceceb-196">compression</span><span class="sxs-lookup"><span data-stu-id="ceceb-196">compression</span></span> | <span data-ttu-id="ceceb-197">指定 hello 類型和層級的 hello 資料壓縮。</span><span class="sxs-lookup"><span data-stu-id="ceceb-197">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="ceceb-198">支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。</span><span class="sxs-lookup"><span data-stu-id="ceceb-198">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="ceceb-199">支援的層級為：**Optimal** 和 **Fastest**。</span><span class="sxs-lookup"><span data-stu-id="ceceb-199">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="ceceb-200">如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。</span><span class="sxs-lookup"><span data-stu-id="ceceb-200">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="ceceb-201">否</span><span class="sxs-lookup"><span data-stu-id="ceceb-201">No</span></span> |

> [!NOTE]
> <span data-ttu-id="ceceb-202">無法同時使用檔名和 fileFilter。</span><span class="sxs-lookup"><span data-stu-id="ceceb-202">filename and fileFilter cannot be used simultaneously.</span></span>

### <a name="using-partionedby-property"></a><span data-ttu-id="ceceb-203">使用 partionedBy 屬性</span><span class="sxs-lookup"><span data-stu-id="ceceb-203">Using partionedBy property</span></span>
<span data-ttu-id="ceceb-204">當 hello 上一節中所述，您可指定動態 folderPath 和 filename 時間序列資料的 hello **partitionedBy**屬性， [Data Factory 函數與 hello 系統變數](data-factory-functions-variables.md)。</span><span class="sxs-lookup"><span data-stu-id="ceceb-204">As mentioned in hello previous section, you can specify a dynamic folderPath and filename for time series data with hello **partitionedBy** property, [Data Factory functions, and hello system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="ceceb-205">toolearn 深入了解時間序列資料集、 排程和配量，請參閱[建立資料集](data-factory-create-datasets.md)，[排程及執行](data-factory-scheduling-and-execution.md)，和[建立管線](data-factory-create-pipelines.md)文件。</span><span class="sxs-lookup"><span data-stu-id="ceceb-205">toolearn more about time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="ceceb-206">範例 1：</span><span class="sxs-lookup"><span data-stu-id="ceceb-206">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="ceceb-207">在此範例與 hello 指定 hello 格式 (YYYYMMDDHH) 中的 Data Factory 系統變數 SliceStart 的值取代 {Slice}。</span><span class="sxs-lookup"><span data-stu-id="ceceb-207">In this example {Slice} is replaced with hello value of Data Factory system variable SliceStart in hello format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="ceceb-208">hello SliceStart 是指 toostart hello 配量時間。</span><span class="sxs-lookup"><span data-stu-id="ceceb-208">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="ceceb-209">hello folderPath 是不同的每個配量。</span><span class="sxs-lookup"><span data-stu-id="ceceb-209">hello folderPath is different for each slice.</span></span> <span data-ttu-id="ceceb-210">例如：wikidatagateway/wikisampledataout/2014100103 或 wikidatagateway/wikisampledataout/2014100104。</span><span class="sxs-lookup"><span data-stu-id="ceceb-210">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="ceceb-211">範例 2：</span><span class="sxs-lookup"><span data-stu-id="ceceb-211">Sample 2:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
<span data-ttu-id="ceceb-212">在此範例中，SliceStart 的年、月、日和時間會擷取到 folderPath 和 fileName 屬性所使用的個別變數。</span><span class="sxs-lookup"><span data-stu-id="ceceb-212">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="ceceb-213">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="ceceb-213">Copy activity properties</span></span>
<span data-ttu-id="ceceb-214">區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="ceceb-214">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="ceceb-215">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="ceceb-215">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="ceceb-216">而 hello 活動 hello typeProperties 區段中可用的屬性會隨每個活動類型。</span><span class="sxs-lookup"><span data-stu-id="ceceb-216">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="ceceb-217">複製活動它們而異的來源與接收的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="ceceb-217">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="ceceb-218">複製活動時，來源是類型為**FileSystemSource** typeProperties 節中會使用下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="ceceb-218">For Copy Activity, when source is of type **FileSystemSource** hello following properties are available in typeProperties section:</span></span>

<span data-ttu-id="ceceb-219">**FileSystemSource**支援 hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="ceceb-219">**FileSystemSource** supports hello following properties:</span></span>

| <span data-ttu-id="ceceb-220">屬性</span><span class="sxs-lookup"><span data-stu-id="ceceb-220">Property</span></span> | <span data-ttu-id="ceceb-221">說明</span><span class="sxs-lookup"><span data-stu-id="ceceb-221">Description</span></span> | <span data-ttu-id="ceceb-222">允許的值</span><span class="sxs-lookup"><span data-stu-id="ceceb-222">Allowed values</span></span> | <span data-ttu-id="ceceb-223">必要</span><span class="sxs-lookup"><span data-stu-id="ceceb-223">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ceceb-224">遞迴</span><span class="sxs-lookup"><span data-stu-id="ceceb-224">recursive</span></span> |<span data-ttu-id="ceceb-225">指出是否 hello 讀取資料以遞迴方式從 hello 子資料夾，或只能從 hello 指定的資料夾。</span><span class="sxs-lookup"><span data-stu-id="ceceb-225">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="ceceb-226">True/False (預設值為 False)</span><span class="sxs-lookup"><span data-stu-id="ceceb-226">True, False (default)</span></span> |<span data-ttu-id="ceceb-227">否</span><span class="sxs-lookup"><span data-stu-id="ceceb-227">No</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="ceceb-228">支援的檔案和壓縮格式</span><span class="sxs-lookup"><span data-stu-id="ceceb-228">Supported file and compression formats</span></span>
<span data-ttu-id="ceceb-229">請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md)文章以了解詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="ceceb-229">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-example-copy-data-from-on-premises-hdfs-tooazure-blob"></a><span data-ttu-id="ceceb-230">JSON 範例： 將資料從內部部署 HDFS tooAzure Blob 複製</span><span class="sxs-lookup"><span data-stu-id="ceceb-230">JSON example: Copy data from on-premises HDFS tooAzure Blob</span></span>
<span data-ttu-id="ceceb-231">這個範例示範如何從 Blob 儲存體的內部部署 HDFS tooAzure toocopy 資料。</span><span class="sxs-lookup"><span data-stu-id="ceceb-231">This sample shows how toocopy data from an on-premises HDFS tooAzure Blob Storage.</span></span> <span data-ttu-id="ceceb-232">不過，資料可以複製**直接**hello 接收所述的 tooany[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="ceceb-232">However, data can be copied **directly** tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="ceceb-233">hello 範例提供下列 Data Factory 實體的 hello 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="ceceb-233">hello sample provides JSON definitions for hello following Data Factory entities.</span></span> <span data-ttu-id="ceceb-234">您可以使用這些定義 toocreate 管線 toocopy 資料從 HDFS tooAzure Blob 儲存體使用[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="ceceb-234">You can use these definitions toocreate a pipeline toocopy data from HDFS tooAzure Blob Storage by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

1. <span data-ttu-id="ceceb-235">[OnPremisesHdfs](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="ceceb-235">A linked service of type [OnPremisesHdfs](#linked-service-properties).</span></span>
2. <span data-ttu-id="ceceb-236">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="ceceb-236">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="ceceb-237">[FileShare](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="ceceb-237">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
4. <span data-ttu-id="ceceb-238">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="ceceb-238">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="ceceb-239">具有使用 [FileSystemSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="ceceb-239">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="ceceb-240">hello 範例將資料從內部部署 HDFS tooan Azure blob 的每個小時。</span><span class="sxs-lookup"><span data-stu-id="ceceb-240">hello sample copies data from an on-premises HDFS tooan Azure blob every hour.</span></span> <span data-ttu-id="ceceb-241">這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。</span><span class="sxs-lookup"><span data-stu-id="ceceb-241">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="ceceb-242">第一個步驟中，設定 hello 資料管理閘道器。</span><span class="sxs-lookup"><span data-stu-id="ceceb-242">As a first step, set up hello data management gateway.</span></span> <span data-ttu-id="ceceb-243">hello hello 中的指示[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="ceceb-243">hello instructions in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="ceceb-244">**HDFS 連結服務：**本例使用 hello Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="ceceb-244">**HDFS linked service:** This example uses hello Windows authentication.</span></span> <span data-ttu-id="ceceb-245">請參閱 [HDFS 連結服務](#linked-service-properties) 章節以了解您可以使用的各種不同類型的驗證。</span><span class="sxs-lookup"><span data-stu-id="ceceb-245">See [HDFS linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "HDFSLinkedService",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="ceceb-246">**Azure 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="ceceb-246">**Azure Storage linked service:**</span></span>

```JSON
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

<span data-ttu-id="ceceb-247">**HDFS 的輸入資料集：**此資料集是指 toohello HDFS 資料夾 DataTransfer/支援 UnitTest /。</span><span class="sxs-lookup"><span data-stu-id="ceceb-247">**HDFS input dataset:** This dataset refers toohello HDFS folder DataTransfer/UnitTest/.</span></span> <span data-ttu-id="ceceb-248">hello 管線會將所有的 hello 檔案複製此資料夾 toohello 目的地中。</span><span class="sxs-lookup"><span data-stu-id="ceceb-248">hello pipeline copies all hello files in this folder toohello destination.</span></span>

<span data-ttu-id="ceceb-249">設定"external":"true"會通知 hello Data Factory 服務的 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時。</span><span class="sxs-lookup"><span data-stu-id="ceceb-249">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

<span data-ttu-id="ceceb-250">**Azure Blob 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="ceceb-250">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="ceceb-251">資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。</span><span class="sxs-lookup"><span data-stu-id="ceceb-251">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="ceceb-252">hello blob 的 hello 資料夾路徑會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="ceceb-252">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="ceceb-253">hello 資料夾路徑會使用 hello 開始時間的年、 月、 日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="ceceb-253">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
    "name": "OutputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/hdfs/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
            "partitionedBy": [
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "MM"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "dd"
                    }
                },
                {
                    "name": "Hour",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "HH"
                    }
                }
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="ceceb-254">**具有檔案系統來源和 Blob 接收器的管線中複製活動：**</span><span class="sxs-lookup"><span data-stu-id="ceceb-254">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="ceceb-255">hello 管線包含複製活動的設定的 toouse 這些輸入和輸出資料集，而排程的 toorun 每小時。</span><span class="sxs-lookup"><span data-stu-id="ceceb-255">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="ceceb-256">在 hello 管線 JSON 定義中，hello**來源**類型設定得**FileSystemSource**和**接收**類型設定得**BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="ceceb-256">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="ceceb-257">指定 hello SQL 查詢**查詢**屬性選取 hello 資料在過去小時 toocopy hello。</span><span class="sxs-lookup"><span data-stu-id="ceceb-257">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```JSON
{
    "name": "pipeline",
    "properties":
    {
        "activities":
        [
            {
                "name": "HdfsToBlobCopy",
                "inputs": [ {"name": "InputDataset"} ],
                "outputs": [ {"name": "OutputDataset"} ],
                "type": "Copy",
                "typeProperties":
                {
                    "source":
                    {
                        "type": "FileSystemSource"
                    },
                    "sink":
                    {
                        "type": "BlobSink"
                    }
                },
                "policy":
                {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "00:05:00"
                }
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="use-kerberos-authentication-for-hdfs-connector"></a><span data-ttu-id="ceceb-258">對 HDFS 連接器使用 Kerberos 驗證</span><span class="sxs-lookup"><span data-stu-id="ceceb-258">Use Kerberos authentication for HDFS connector</span></span>
<span data-ttu-id="ceceb-259">以在 HDFS 連接器 toouse Kerberos 驗證有兩個選項 tooset hello 在內部部署環境。</span><span class="sxs-lookup"><span data-stu-id="ceceb-259">There are two options tooset up hello on-premises environment so as toouse Kerberos Authentication in HDFS connector.</span></span> <span data-ttu-id="ceceb-260">您可以選擇其中一個 hello 更適合您的案例。</span><span class="sxs-lookup"><span data-stu-id="ceceb-260">You can choose hello one better fits your case.</span></span>
* <span data-ttu-id="ceceb-261">選項 1：[將閘道電腦加入 Kerberos 領域](#kerberos-join-realm)</span><span class="sxs-lookup"><span data-stu-id="ceceb-261">Option 1: [Join gateway machine in Kerberos realm](#kerberos-join-realm)</span></span>
* <span data-ttu-id="ceceb-262">選項 2：[啟用 Windows 網域和 Kerberos 領域之間的相互信任](#kerberos-mutual-trust)</span><span class="sxs-lookup"><span data-stu-id="ceceb-262">Option 2: [Enable mutual trust between Windows domain and Kerberos realm](#kerberos-mutual-trust)</span></span>

### <span data-ttu-id="ceceb-263"><a name="kerberos-join-realm"></a>選項 1：將閘道電腦加入 Kerberos 領域</span><span class="sxs-lookup"><span data-stu-id="ceceb-263"><a name="kerberos-join-realm"></a>Option 1: Join gateway machine in Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="ceceb-264">需求：</span><span class="sxs-lookup"><span data-stu-id="ceceb-264">Requirement:</span></span>

* <span data-ttu-id="ceceb-265">hello 閘道電腦必須 toojoin hello Kerberos 領域，且無法再加入任何 Windows 網域。</span><span class="sxs-lookup"><span data-stu-id="ceceb-265">hello gateway machine needs toojoin hello Kerberos realm and can’t join any Windows domain.</span></span>

#### <a name="how-tooconfigure"></a><span data-ttu-id="ceceb-266">如何 tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="ceceb-266">How tooconfigure:</span></span>

<span data-ttu-id="ceceb-267">**在閘道電腦上︰**</span><span class="sxs-lookup"><span data-stu-id="ceceb-267">**On gateway machine:**</span></span>

1.  <span data-ttu-id="ceceb-268">執行 hello **Ksetup**公用程式 tooconfigure hello Kerberos KDC 伺服器和領域。</span><span class="sxs-lookup"><span data-stu-id="ceceb-268">Run hello **Ksetup** utility tooconfigure hello Kerberos KDC server and realm.</span></span>

    <span data-ttu-id="ceceb-269">hello 機器必須設定為工作群組的成員，因為 Kerberos 領域是從 Windows 網域不同。</span><span class="sxs-lookup"><span data-stu-id="ceceb-269">hello machine must be configured as a member of a workgroup since a Kerberos realm is different from a Windows domain.</span></span> <span data-ttu-id="ceceb-270">這可藉由設定 hello Kerberos 領域及新增 KDC 伺服器，如下所示。</span><span class="sxs-lookup"><span data-stu-id="ceceb-270">This can be achieved by setting hello Kerberos realm and adding a KDC server as follows.</span></span> <span data-ttu-id="ceceb-271">視需要以您自己的個別領域取代 *REALM.COM*。</span><span class="sxs-lookup"><span data-stu-id="ceceb-271">Replace *REALM.COM* with your own respective realm as needed.</span></span>

            C:> Ksetup /setdomain REALM.COM
            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>

    <span data-ttu-id="ceceb-272">**重新啟動**hello 機器後立即執行這些 2 命令。</span><span class="sxs-lookup"><span data-stu-id="ceceb-272">**Restart** hello machine after executing these 2 commands.</span></span>

2.  <span data-ttu-id="ceceb-273">確認 hello 組態**Ksetup**命令。</span><span class="sxs-lookup"><span data-stu-id="ceceb-273">Verify hello configuration with **Ksetup** command.</span></span> <span data-ttu-id="ceceb-274">hello 輸出應該類似：</span><span class="sxs-lookup"><span data-stu-id="ceceb-274">hello output should be like:</span></span>

            C:> Ksetup
            default realm = REALM.COM (external)
            REALM.com:
                kdc = <your_kdc_server_address>

<span data-ttu-id="ceceb-275">**在 Azure Data Factory 中：**</span><span class="sxs-lookup"><span data-stu-id="ceceb-275">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="ceceb-276">設定 hello HDFS 連接器使用**Windows 驗證**搭配 Kerberos 主體名稱和密碼 tooconnect toohello HDFS 資料來源。</span><span class="sxs-lookup"><span data-stu-id="ceceb-276">Configure hello HDFS connector using **Windows authentication** together with your Kerberos principal name and password tooconnect toohello HDFS data source.</span></span> <span data-ttu-id="ceceb-277">檢查組態詳細資料上的 [HDFS 連結服務屬性](#linked-service-properties)區段。</span><span class="sxs-lookup"><span data-stu-id="ceceb-277">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

### <span data-ttu-id="ceceb-278"><a name="kerberos-mutual-trust"></a>選項 2：啟用 Windows 網域和 Kerberos 領域之間的相互信任</span><span class="sxs-lookup"><span data-stu-id="ceceb-278"><a name="kerberos-mutual-trust"></a>Option 2: Enable mutual trust between Windows domain and Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="ceceb-279">需求：</span><span class="sxs-lookup"><span data-stu-id="ceceb-279">Requirement:</span></span>
*   <span data-ttu-id="ceceb-280">hello 閘道電腦必須加入 Windows 網域。</span><span class="sxs-lookup"><span data-stu-id="ceceb-280">hello gateway machine must join a Windows domain.</span></span>
*   <span data-ttu-id="ceceb-281">您需要的權限 tooupdate hello 網域控制站的設定。</span><span class="sxs-lookup"><span data-stu-id="ceceb-281">You need permission tooupdate hello domain controller's settings.</span></span>

#### <a name="how-tooconfigure"></a><span data-ttu-id="ceceb-282">如何 tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="ceceb-282">How tooconfigure:</span></span>

> [!NOTE]
> <span data-ttu-id="ceceb-283">取代 REALM.COM 和 AD.COM hello 視下列教學課程使用您自己的個別領域和網域控制站中。</span><span class="sxs-lookup"><span data-stu-id="ceceb-283">Replace REALM.COM and AD.COM in hello following tutorial with your own respective realm and domain controller as needed.</span></span>

<span data-ttu-id="ceceb-284">**在 KDC 伺服器上︰**</span><span class="sxs-lookup"><span data-stu-id="ceceb-284">**On KDC server:**</span></span>

1.  <span data-ttu-id="ceceb-285">編輯中的 hello KDC 組態**krb5.conf**檔案 toolet KDC 信任參考 toohello 遵循組態範本的 Windows 網域。</span><span class="sxs-lookup"><span data-stu-id="ceceb-285">Edit hello KDC configuration in **krb5.conf** file toolet KDC trust Windows Domain referring toohello following configuration template.</span></span> <span data-ttu-id="ceceb-286">根據預設，hello 組態是位於**/etc/krb5.conf**。</span><span class="sxs-lookup"><span data-stu-id="ceceb-286">By default, hello configuration is located at **/etc/krb5.conf**.</span></span>

            [logging]
             default = FILE:/var/log/krb5libs.log
             kdc = FILE:/var/log/krb5kdc.log
             admin_server = FILE:/var/log/kadmind.log

            [libdefaults]
             default_realm = REALM.COM
             dns_lookup_realm = false
             dns_lookup_kdc = false
             ticket_lifetime = 24h
             renew_lifetime = 7d
             forwardable = true

            [realms]
             REALM.COM = {
              kdc = node.REALM.COM
              admin_server = node.REALM.COM
             }
            AD.COM = {
             kdc = windc.ad.com
             admin_server = windc.ad.com
            }

            [domain_realm]
             .REALM.COM = REALM.COM
             REALM.COM = REALM.COM
             .ad.com = AD.COM
             ad.com = AD.COM

            [capaths]
             AD.COM = {
              REALM.COM = .
             }

  <span data-ttu-id="ceceb-287">**重新啟動**hello KDC 服務組態之後。</span><span class="sxs-lookup"><span data-stu-id="ceceb-287">**Restart** hello KDC service after configuration.</span></span>

2.  <span data-ttu-id="ceceb-288">準備名為主體 **krbtgt/REALM.COM@AD.COM**  KDC 伺服器以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="ceceb-288">Prepare a principal named **krbtgt/REALM.COM@AD.COM** in KDC server with hello following command:</span></span>

            Kadmin> addprinc krbtgt/REALM.COM@AD.COM

3.  <span data-ttu-id="ceceb-289">在 **hadoop.security.auth_to_local** HDFS 服務組態檔中，新增 `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`。</span><span class="sxs-lookup"><span data-stu-id="ceceb-289">In **hadoop.security.auth_to_local** HDFS service configuration file, add `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span></span>

<span data-ttu-id="ceceb-290">**在網域控制站上：**</span><span class="sxs-lookup"><span data-stu-id="ceceb-290">**On domain controller:**</span></span>

1.  <span data-ttu-id="ceceb-291">執行下列 hello **Ksetup**命令 tooadd 領域項目：</span><span class="sxs-lookup"><span data-stu-id="ceceb-291">Run hello following **Ksetup** commands tooadd a realm entry:</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

2.  <span data-ttu-id="ceceb-292">建立從 Windows 網域 tooKerberos 領域的信任關係。</span><span class="sxs-lookup"><span data-stu-id="ceceb-292">Establish trust from Windows Domain tooKerberos Realm.</span></span> <span data-ttu-id="ceceb-293">[密碼] 是 hello 主體 hello 密碼 **krbtgt/REALM.COM@AD.COM** 。</span><span class="sxs-lookup"><span data-stu-id="ceceb-293">[password] is hello password for hello principal **krbtgt/REALM.COM@AD.COM**.</span></span>

            C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /passwordt:[password]

3.  <span data-ttu-id="ceceb-294">選取 Kerberos 所使用的加密演算法。</span><span class="sxs-lookup"><span data-stu-id="ceceb-294">Select encryption algorithm used in Kerberos.</span></span>

    1. <span data-ttu-id="ceceb-295">移 tooServer 管理員 > 群組原則管理 > 網域 > 群組原則物件 > 預設使用中的網域原則或編輯。</span><span class="sxs-lookup"><span data-stu-id="ceceb-295">Go tooServer Manager > Group Policy Management > Domain > Group Policy Objects > Default or Active Domain Policy, and Edit.</span></span>

    2. <span data-ttu-id="ceceb-296">在 hello**群組原則管理編輯器**快顯視窗中，移 tooComputer 組態 > 原則 > Windows 設定 > 安全性設定 > 本機原則 > 安全性選項和設定**網路安全性： 設定加密類型的 Kerberos 允許**。</span><span class="sxs-lookup"><span data-stu-id="ceceb-296">In hello **Group Policy Management Editor** popup window, go tooComputer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options, and configure **Network security: Configure Encryption types allowed for Kerberos**.</span></span>

    3. <span data-ttu-id="ceceb-297">您想要 toouse 選取 hello 加密演算法時連接 tooKDC。</span><span class="sxs-lookup"><span data-stu-id="ceceb-297">Select hello encryption algorithm you want toouse when connect tooKDC.</span></span> <span data-ttu-id="ceceb-298">通常，您只需選取所有 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="ceceb-298">Commonly, you can simply select all hello options.</span></span>

        ![設定 Kerberos 的加密類型](media/data-factory-hdfs-connector/config-encryption-types-for-kerberos.png)

    4. <span data-ttu-id="ceceb-300">使用**Ksetup**命令 toospecify hello 加密演算法 toobe hello 上使用特定的領域。</span><span class="sxs-lookup"><span data-stu-id="ceceb-300">Use **Ksetup** command toospecify hello encryption algorithm toobe used on hello specific REALM.</span></span>

                C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96

4.  <span data-ttu-id="ceceb-301">Hello 之間建立對應 hello 網域帳戶和 Kerberos 主體順序 toouse Kerberos 主體中的 Windows 網域中。</span><span class="sxs-lookup"><span data-stu-id="ceceb-301">Create hello mapping between hello domain account and Kerberos principal, in order toouse Kerberos principal in Windows Domain.</span></span>

    1. <span data-ttu-id="ceceb-302">啟動 hello 系統管理工具 > **Active Directory 使用者和電腦**。</span><span class="sxs-lookup"><span data-stu-id="ceceb-302">Start hello Administrative tools > **Active Directory Users and Computers**.</span></span>

    2. <span data-ttu-id="ceceb-303">按一下 [檢視] > [進階功能] 來設定進階功能。</span><span class="sxs-lookup"><span data-stu-id="ceceb-303">Configure advanced features by clicking **View** > **Advanced Features**.</span></span>

    3. <span data-ttu-id="ceceb-304">找出您想 toocreate 對應，以滑鼠右鍵按一下 tooview hello 帳戶 toowhich**名稱對應**> 按一下**Kerberos 名稱** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ceceb-304">Locate hello account toowhich you want toocreate mappings, and right-click tooview **Name Mappings** > click **Kerberos Names** tab.</span></span>

    4. <span data-ttu-id="ceceb-305">將主體加入從 hello 領域。</span><span class="sxs-lookup"><span data-stu-id="ceceb-305">Add a principal from hello realm.</span></span>

        ![對應安全性身分識別](media/data-factory-hdfs-connector/map-security-identity.png)

<span data-ttu-id="ceceb-307">**在閘道電腦上︰**</span><span class="sxs-lookup"><span data-stu-id="ceceb-307">**On gateway machine:**</span></span>

* <span data-ttu-id="ceceb-308">執行下列 hello **Ksetup**命令 tooadd 領域項目。</span><span class="sxs-lookup"><span data-stu-id="ceceb-308">Run hello following **Ksetup** commands tooadd a realm entry.</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

<span data-ttu-id="ceceb-309">**在 Azure Data Factory 中：**</span><span class="sxs-lookup"><span data-stu-id="ceceb-309">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="ceceb-310">設定 hello HDFS 連接器使用**Windows 驗證**連同您的網域帳戶或 Kerberos 主體 tooconnect toohello HDFS 資料來源。</span><span class="sxs-lookup"><span data-stu-id="ceceb-310">Configure hello HDFS connector using **Windows authentication** together with either your Domain Account or Kerberos Principal tooconnect toohello HDFS data source.</span></span> <span data-ttu-id="ceceb-311">檢查組態詳細資料上的 [HDFS 連結服務屬性](#linked-service-properties)區段。</span><span class="sxs-lookup"><span data-stu-id="ceceb-311">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

> [!NOTE]
> <span data-ttu-id="ceceb-312">toomap 資料行從來源資料集 toocolumns 從接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="ceceb-312">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="performance-and-tuning"></a><span data-ttu-id="ceceb-313">效能和微調</span><span class="sxs-lookup"><span data-stu-id="ceceb-313">Performance and Tuning</span></span>
<span data-ttu-id="ceceb-314">請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。</span><span class="sxs-lookup"><span data-stu-id="ceceb-314">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
