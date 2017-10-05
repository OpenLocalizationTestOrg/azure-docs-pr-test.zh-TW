---
title: "使用 Azure Data Factory 從內部部署 SQL Server 將資料移至 SQL Azure | Microsoft Docs"
description: "請設定 ADF 管線來編寫兩個資料移轉活動，這兩個活動會每天在內部部署及雲端中的資料庫之間一同移動資料。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 36837c83-2015-48be-b850-c4346aa5ae8a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 39fe26d3388be8b558f05063a8965889c013a41e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-from-an-on-premises-sql-server-to-sql-azure-with-azure-data-factory"></a><span data-ttu-id="bdd4c-103">使用 Azure Data Factory 從內部部署 SQL Server 將資料移至 SQL Azure</span><span class="sxs-lookup"><span data-stu-id="bdd4c-103">Move data from an on-premises SQL server to SQL Azure with Azure Data Factory</span></span>
<span data-ttu-id="bdd4c-104">本主題說明如何使用 Azure Data Factory (ADF)，透過 Azure Blob 儲存體，將資料從內部部署的 SQL Server 資料庫移動至 SQL Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-104">This topic shows how to move data from an on-premises SQL Server Database to a SQL Azure Database via Azure Blob Storage using the Azure Data Factory (ADF).</span></span>

<span data-ttu-id="bdd4c-105">針對將資料移至 Azure SQL Database 的各種選項，如需摘要說明的資料表，請參閱[將資料移至 Azure Machine Learning 的 Azure SQL Database](machine-learning-data-science-move-sql-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-105">For a table that summarizes various options for moving data to an Azure SQL Database, see [Move data to an Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

## <span data-ttu-id="bdd4c-106"><a name="intro"></a>簡介：什麼是 ADF ，以及其應該用來移轉資料的時機？</span><span class="sxs-lookup"><span data-stu-id="bdd4c-106"><a name="intro"></a>Introduction: What is ADF and when should it be used to migrate data?</span></span>
<span data-ttu-id="bdd4c-107">Azure Data Factory 是完全受管理的雲端架構資料整合服務，用來協調及自動化資料的移動和轉換。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-107">Azure Data Factory is a fully managed cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span></span> <span data-ttu-id="bdd4c-108">ADF 模型中的重要概念是管線。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-108">The key concept in the ADF model is pipeline.</span></span> <span data-ttu-id="bdd4c-109">管線是活動的邏輯群組，各個群組都會定義包含在資料集中的資料上要執行的動作。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-109">A pipeline is a logical grouping of Activities, each of which defines the actions to perform on the data contained in Datasets.</span></span> <span data-ttu-id="bdd4c-110">連結的服務是用來定義 Data Factory 所需的資訊，以便連接到資料資源。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-110">Linked services are used to define the information needed for Data Factory to connect to the data resources.</span></span>

<span data-ttu-id="bdd4c-111">使用 ADF，您可將現有的資料處理服務組合成具高可用性的資料管線，並在雲端中管理。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-111">With ADF, existing data processing services can be composed into data pipelines that are highly available and managed in the cloud.</span></span> <span data-ttu-id="bdd4c-112">這些資料管線可排程來內嵌、準備、轉換、分析和發佈資料，而 ADF 會管理並協調複雜的資料和處理中的相依項目。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-112">These data pipelines can be scheduled to ingest, prepare, transform, analyze, and publish data, and ADF manages and orchestrates the complex data and processing dependencies.</span></span> <span data-ttu-id="bdd4c-113">您可以快速地在雲端中建置和部署解決方案，藉此連接逐漸增加的內部部署和雲端資料來源。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-113">Solutions can be quickly built and deployed in the cloud, connecting a growing number of on-premises and cloud data sources.</span></span>

<span data-ttu-id="bdd4c-114">請考慮使用 ADF：</span><span class="sxs-lookup"><span data-stu-id="bdd4c-114">Consider using ADF:</span></span>

* <span data-ttu-id="bdd4c-115">若同時存取內部部署和雲端資源的混合式案例需要持續移轉資料</span><span class="sxs-lookup"><span data-stu-id="bdd4c-115">when data needs to be continually migrated in a hybrid scenario that accesses both on-premises and cloud resources</span></span>
* <span data-ttu-id="bdd4c-116">當資料進行交易、需要加以修改，或是在移轉期間新增了商務邏輯時。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-116">when the data is transacted or needs to be modified or have business logic added to it when being migrated.</span></span>

<span data-ttu-id="bdd4c-117">ADF 允許使用定期管理資料移動的簡易 JSON 指令碼，來進行排程和監視的工作。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-117">ADF allows for the scheduling and monitoring of jobs using simple JSON scripts that manage the movement of data on a periodic basis.</span></span> <span data-ttu-id="bdd4c-118">ADF 也有其他功能，例如支援複雜作業。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-118">ADF also has other capabilities such as support for complex operations.</span></span> <span data-ttu-id="bdd4c-119">如需 ADF 的詳細資訊，請參閱 [Azure Data Factory (ADF)](https://azure.microsoft.com/services/data-factory/)上的文件。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-119">For more information on ADF, see the documentation at [Azure Data Factory (ADF)](https://azure.microsoft.com/services/data-factory/).</span></span>

## <span data-ttu-id="bdd4c-120"><a name="scenario"></a>案例</span><span class="sxs-lookup"><span data-stu-id="bdd4c-120"><a name="scenario"></a>The Scenario</span></span>
<span data-ttu-id="bdd4c-121">我們設定了 ADF 管線來組成兩個資料移轉活動。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-121">We set up an ADF pipeline that composes two data migration activities.</span></span> <span data-ttu-id="bdd4c-122">它們每天都會一起在內部部署 SQL 資料庫和雲端 Azure SQL Database 之間移動資料。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-122">Together they move data on a daily basis between an on-premises SQL database and an Azure SQL Database in the cloud.</span></span> <span data-ttu-id="bdd4c-123">這兩個活動為：</span><span class="sxs-lookup"><span data-stu-id="bdd4c-123">The two activities are:</span></span>

* <span data-ttu-id="bdd4c-124">將資料從內部部署 SQL Server 資料庫複製到 Azure Blob 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="bdd4c-124">copy data from an on-premises SQL Server database to an Azure Blob Storage account</span></span>
* <span data-ttu-id="bdd4c-125">將資料從 Azure Blob 儲存體帳戶複製至 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="bdd4c-125">copy data from the Azure Blob Storage account to an Azure SQL Database.</span></span>

> [!NOTE]
> <span data-ttu-id="bdd4c-126">這裡顯示的步驟已根據 ADF 團隊所提供的更詳細教學課程進行改編：[利用資料管理閘道在內部部署來源和雲端之間移動資料](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)。該主題相關章節的參考資料也會在必要時提供。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-126">The steps shown here have been adapted from the more detailed tutorial provided by the ADF team: [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) References to the relevant sections of that topic are provided when appropriate.</span></span>
>
>

## <span data-ttu-id="bdd4c-127"><a name="prereqs"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="bdd4c-127"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="bdd4c-128">本教學課程假設您有：</span><span class="sxs-lookup"><span data-stu-id="bdd4c-128">This tutorial assumes you have:</span></span>

* <span data-ttu-id="bdd4c-129">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-129">An **Azure subscription**.</span></span> <span data-ttu-id="bdd4c-130">如果您沒有訂用帳戶，可以註冊 [免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-130">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="bdd4c-131">**Azure 儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-131">An **Azure storage account**.</span></span> <span data-ttu-id="bdd4c-132">在本教學課程中，您會使用 Azure 儲存體帳戶來儲存資料。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-132">You use an Azure storage account for storing the data in this tutorial.</span></span> <span data-ttu-id="bdd4c-133">如果您沒有 Azure 儲存體帳戶，請參閱 [建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account) 一文。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-133">If you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="bdd4c-134">建立儲存體帳戶之後，您必須取得用來存取儲存體的帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-134">After you have created the storage account, you need to obtain the account key used to access the storage.</span></span> <span data-ttu-id="bdd4c-135">請參閱[管理儲存體存取金鑰](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys)。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-135">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="bdd4c-136">存取 **Azure SQL Database**。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-136">Access to an **Azure SQL Database**.</span></span> <span data-ttu-id="bdd4c-137">如果您必須設定 Azure SQL Database， [開始使用 Microsoft Azure SQL Database ](../sql-database/sql-database-get-started.md) 主題會提供如何佈建 Azure SQL Database 之新執行個體的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-137">If you must set up an Azure SQL Database, the tpoic [Getting Started with Microsoft Azure SQL Database ](../sql-database/sql-database-get-started.md) provides information on how to provision a new instance of an Azure SQL Database.</span></span>
* <span data-ttu-id="bdd4c-138">已在本機上安裝和設定 **Azure PowerShell** 。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-138">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="bdd4c-139">如需指示，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-139">For instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!NOTE]
> <span data-ttu-id="bdd4c-140">此程序會使用 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-140">This procedure uses the [Azure portal](https://portal.azure.com/).</span></span>
>
>

## <span data-ttu-id="bdd4c-141"><a name="upload-data"></a> 將資料上傳至您的內部部署 SQL Server</span><span class="sxs-lookup"><span data-stu-id="bdd4c-141"><a name="upload-data"></a> Upload the data to your on-premises SQL Server</span></span>
<span data-ttu-id="bdd4c-142">我們會使用 [NYC 計程車資料集](http://chriswhong.com/open-data/foil_nyc_taxi/) 示範移轉程序。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-142">We use the [NYC Taxi dataset](http://chriswhong.com/open-data/foil_nyc_taxi/) to demonstrate the migration process.</span></span> <span data-ttu-id="bdd4c-143">NYC 計程車資料集可在 Azure Blob 儲存體 [NYC 計程車資料](http://www.andresmh.com/nyctaxitrips/)中取得 (如該文章所述)。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-143">The NYC Taxi dataset is available, as noted in that post, on Azure blob storage [NYC Taxi Data](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="bdd4c-144">該資料有兩個檔案：包含路線詳細資料的 trip_data.csv 檔案，以及包含每次車程支付車資之詳細資料的 trip_far.csv 檔案。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-144">The data has two files, the trip_data.csv file, which contains trip details, and the  trip_far.csv file, which contains details of the fare paid for each trip.</span></span> <span data-ttu-id="bdd4c-145">這些檔案的範例和說明都會在 [NYC 計程車車程資料集說明](machine-learning-data-science-process-sql-walkthrough.md#dataset)中提供。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-145">A sample and description of these files are provided in [NYC Taxi Trips Dataset Description](machine-learning-data-science-process-sql-walkthrough.md#dataset).</span></span>

<span data-ttu-id="bdd4c-146">您可以將這裡提供的程序調整為自己的資料集，或者遵循上述步驟使用 NYC 計程車資料集。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-146">You can either adapt the procedure provided here to a set of your own data or follow the steps as described by using the NYC Taxi dataset.</span></span> <span data-ttu-id="bdd4c-147">若要將 NYC 計程車資料集上傳至您的內部部署 SQL Server 資料庫，請遵循[大量匯入資料至 SQL Server 資料庫](machine-learning-data-science-process-sql-walkthrough.md#dbload)中概述的程序進行。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-147">To upload the NYC Taxi dataset into your on-premises SQL Server database, follow the procedure outlined in [Bulk Import Data into SQL Server Database](machine-learning-data-science-process-sql-walkthrough.md#dbload).</span></span> <span data-ttu-id="bdd4c-148">這些指示適用於 Azure 虛擬機器上的 SQL Server，但將資料上傳至內部部署 SQL Server 的程序是相同的。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-148">These instructions are for a SQL Server on an Azure Virtual Machine, but the procedure for uploading to the on-premises SQL Server is the same.</span></span>

## <span data-ttu-id="bdd4c-149"><a name="create-adf"></a> 建立 Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="bdd4c-149"><a name="create-adf"></a> Create an Azure Data Factory</span></span>
<span data-ttu-id="bdd4c-150">用於建立新 Azure Data Factory 的指示及 [Azure 入口網站](https://portal.azure.com/)中的資源群組，已在[建立 Azure Data Factory](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory) 提供。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-150">The instructions for creating a new Azure Data Factory and a resource group in the [Azure portal](https://portal.azure.com/) are provided [Create an Azure Data Factory](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory).</span></span> <span data-ttu-id="bdd4c-151">將新的 ADF 執行個體命名為 *adfdsp*，並將建立的資源群組命名為 *adfdsprg*。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-151">Name the new ADF instance *adfdsp* and name the resource group created *adfdsprg*.</span></span>

## <a name="install-and-configure-up-the-data-management-gateway"></a><span data-ttu-id="bdd4c-152">安裝和設定資料管理閘道</span><span class="sxs-lookup"><span data-stu-id="bdd4c-152">Install and configure up the Data Management Gateway</span></span>
<span data-ttu-id="bdd4c-153">若要在 Azure 資料處理站中啟用管線以使用內部部署的 SQL Server，您必須將其以連結服務形式新增至資料處理站。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-153">To enable your pipelines in an Azure data factory to work with an on-premises SQL Server, you need to add it as a Linked Service to the data factory.</span></span> <span data-ttu-id="bdd4c-154">若要建立內部部署 SQL Server 的連結服務，您必須︰</span><span class="sxs-lookup"><span data-stu-id="bdd4c-154">To create a Linked Service for an on-premises SQL Server, you must:</span></span>

* <span data-ttu-id="bdd4c-155">將 Microsoft 資料管理閘道下載並安裝到內部部署電腦。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-155">download and install Microsoft Data Management Gateway onto the on-premises computer.</span></span>
* <span data-ttu-id="bdd4c-156">設定內部部署資料來源的連結服務以使用閘道。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-156">configure the linked service for the on-premises data source to use the gateway.</span></span>

<span data-ttu-id="bdd4c-157">資料管理閘道器會序列化和還原序列化託管之電腦上的來源與接收資料。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-157">The Data Management Gateway serializes and deserializes the source and sink data on the computer where it is hosted.</span></span>

<span data-ttu-id="bdd4c-158">如需關於資料管理閘道的設定指示及詳細資料，請參閱 [利用資料管理閘道在內部部署來源和雲端之間移動資料](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span><span class="sxs-lookup"><span data-stu-id="bdd4c-158">For set-up instructions and details on Data Management Gateway, see [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span></span>

## <span data-ttu-id="bdd4c-159"><a name="adflinkedservices"></a>建立連結服務以連接至資料資源</span><span class="sxs-lookup"><span data-stu-id="bdd4c-159"><a name="adflinkedservices"></a>Create linked services to connect to the data resources</span></span>
<span data-ttu-id="bdd4c-160">連結服務定義會定義 Azure Data Factory 所需的資訊，以便連接到資料資源。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-160">A linked service defines the information needed for Azure Data Factory to connect to a data resource.</span></span> <span data-ttu-id="bdd4c-161">用於建立連結服務的逐步程序，已在[建立連結服務](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services)中提供。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-161">The step-by-step procedure for creating linked services is provided in [Create linked services](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).</span></span>

<span data-ttu-id="bdd4c-162">此案例中的三個資源都必須使用連結服務。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-162">We have three resources in this scenario for which linked services are needed.</span></span>

1. [<span data-ttu-id="bdd4c-163">內部部署 SQL Server 的連結服務</span><span class="sxs-lookup"><span data-stu-id="bdd4c-163">Linked service for on-premises SQL Server</span></span>](#adf-linked-service-onprem-sql)
2. [<span data-ttu-id="bdd4c-164">Azure Blob 儲存體的連結服務</span><span class="sxs-lookup"><span data-stu-id="bdd4c-164">Linked service for Azure Blob Storage</span></span>](#adf-linked-service-blob-store)
3. [<span data-ttu-id="bdd4c-165">Azure SQL Database 的連結服務</span><span class="sxs-lookup"><span data-stu-id="bdd4c-165">Linked service for Azure SQL database</span></span>](#adf-linked-service-azure-sql)

### <span data-ttu-id="bdd4c-166"><a name="adf-linked-service-onprem-sql"></a>內部部署 SQL Server 資料庫的連結服務</span><span class="sxs-lookup"><span data-stu-id="bdd4c-166"><a name="adf-linked-service-onprem-sql"></a>Linked service for on-premises SQL Server database</span></span>
<span data-ttu-id="bdd4c-167">若要建立內部部署 SQL Server 的連結服務：</span><span class="sxs-lookup"><span data-stu-id="bdd4c-167">To create the linked service for the on-premises SQL Server:</span></span>

* <span data-ttu-id="bdd4c-168">在 Azure 傳統入口網站的 ADF 登陸頁面按一下 [資料存放區] </span><span class="sxs-lookup"><span data-stu-id="bdd4c-168">click the **Data Store** in the ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="bdd4c-169">選取 [SQL]，然後輸入內部部署 SQL Server 的 [使用者名稱] 和 [密碼] 認證。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-169">select **SQL** and enter the *username* and *password* credentials for the on-premises SQL Server.</span></span> <span data-ttu-id="bdd4c-170">您必須以**完整伺服器名稱 + 反斜線 + 執行個體名稱 (伺服器名稱\執行個體名稱) 格式輸入伺服器名稱**。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-170">You need to enter the servername as a **fully qualified servername backslash instance name (servername\instancename)**.</span></span> <span data-ttu-id="bdd4c-171">將連結服務命名為 *adfonpremsql*。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-171">Name the linked service *adfonpremsql*.</span></span>

### <span data-ttu-id="bdd4c-172"><a name="adf-linked-service-blob-store"></a>Blob 的連結服務</span><span class="sxs-lookup"><span data-stu-id="bdd4c-172"><a name="adf-linked-service-blob-store"></a>Linked service for Blob</span></span>
<span data-ttu-id="bdd4c-173">若要建立 Azure Blob 儲存體帳戶的連結服務：</span><span class="sxs-lookup"><span data-stu-id="bdd4c-173">To create the linked service for the Azure Blob Storage account:</span></span>

* <span data-ttu-id="bdd4c-174">在 Azure 傳統入口網站的 ADF 登陸頁面按一下 [資料存放區] </span><span class="sxs-lookup"><span data-stu-id="bdd4c-174">click the **Data Store** in the ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="bdd4c-175">選取 [Azure 儲存體帳戶] </span><span class="sxs-lookup"><span data-stu-id="bdd4c-175">select **Azure Storage Account**</span></span>
* <span data-ttu-id="bdd4c-176">輸入 Azure Blob 儲存體帳戶金鑰和容器名稱。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-176">enter the Azure Blob Storage account key and container name.</span></span> <span data-ttu-id="bdd4c-177">將連結服務命名為「adfds」 。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-177">Name the Linked Service *adfds*.</span></span>

### <span data-ttu-id="bdd4c-178"><a name="adf-linked-service-azure-sql"></a>Azure SQL Database 的連結服務</span><span class="sxs-lookup"><span data-stu-id="bdd4c-178"><a name="adf-linked-service-azure-sql"></a>Linked service for Azure SQL database</span></span>
<span data-ttu-id="bdd4c-179">若要建立 Azure SQL Database 的連結服務：</span><span class="sxs-lookup"><span data-stu-id="bdd4c-179">To create the linked service for the Azure SQL Database:</span></span>

* <span data-ttu-id="bdd4c-180">在 Azure 傳統入口網站的 ADF 登陸頁面按一下 [資料存放區] </span><span class="sxs-lookup"><span data-stu-id="bdd4c-180">click the **Data Store** in the ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="bdd4c-181">選取 [Azure SQL]，然後輸入 Azure SQL Database 的 [使用者名稱] 和 [密碼] 認證。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-181">select **Azure SQL** and enter the *username* and *password* credentials for the Azure SQL Database.</span></span> <span data-ttu-id="bdd4c-182">*username* 必須指定為 *user@servername*。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-182">The *username* must be specified as *user@servername*.</span></span>   

## <span data-ttu-id="bdd4c-183"><a name="adf-tables"></a>定義和建立資料表以指定存取資料集的方式</span><span class="sxs-lookup"><span data-stu-id="bdd4c-183"><a name="adf-tables"></a>Define and create tables to specify how to access the datasets</span></span>
<span data-ttu-id="bdd4c-184">使用下列指令碼型程序，建立指定資料集結構、位置及可用性的資料表。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-184">Create tables that specify the structure, location, and availability of the datasets with the following script-based procedures.</span></span> <span data-ttu-id="bdd4c-185">JSON 檔案可用來定義資料表。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-185">JSON files are used to define the tables.</span></span> <span data-ttu-id="bdd4c-186">如需這些檔案結構的詳細資訊，請參閱 [資料集](../data-factory/data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-186">For more information on the structure of these files, see [Datasets](../data-factory/data-factory-create-datasets.md).</span></span>

> [!NOTE]
> <span data-ttu-id="bdd4c-187">您應該先執行 `Add-AzureAccount` Cmdlet，再執行 [New-AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) Cmdlet，以確認已選取正確的 Azure 訂用帳戶來執行命令。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-187">You should execute the `Add-AzureAccount` cmdlet before executing the [New-AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) cmdlet to confirm that the right Azure subscription is selected for the command execution.</span></span> <span data-ttu-id="bdd4c-188">如需此 Cmdlet 的文件，請參閱 [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0)。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-188">For documentation of this cmdlet, see [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).</span></span>
>
>

<span data-ttu-id="bdd4c-189">資料表中的 JSON 型定義使用下列名稱：</span><span class="sxs-lookup"><span data-stu-id="bdd4c-189">The JSON-based definitions in the tables use the following names:</span></span>

* <span data-ttu-id="bdd4c-190">內部部署 SQL Server 中的**資料表名稱**為 *nyctaxi_data*</span><span class="sxs-lookup"><span data-stu-id="bdd4c-190">the **table name** in the on-premises SQL server is *nyctaxi_data*</span></span>
* <span data-ttu-id="bdd4c-191">Azure Blob 儲存體帳戶中的「容器名稱」  為 *containername*</span><span class="sxs-lookup"><span data-stu-id="bdd4c-191">the **container name** in the Azure Blob Storage account is *containername*</span></span>  

<span data-ttu-id="bdd4c-192">此 ADF 管線所需的三個資料表定義為：</span><span class="sxs-lookup"><span data-stu-id="bdd4c-192">Three table definitions are needed for this ADF pipeline:</span></span>

1. [<span data-ttu-id="bdd4c-193">SQL 內部部署資料表</span><span class="sxs-lookup"><span data-stu-id="bdd4c-193">SQL on-premises Table</span></span>](#adf-table-onprem-sql)
2. [<span data-ttu-id="bdd4c-194">Blob 資料表 </span><span class="sxs-lookup"><span data-stu-id="bdd4c-194">Blob Table </span></span>](#adf-table-blob-store)
3. [<span data-ttu-id="bdd4c-195">SQL Azure 資料表</span><span class="sxs-lookup"><span data-stu-id="bdd4c-195">SQL Azure Table</span></span>](#adf-table-azure-sql)

> [!NOTE]
> <span data-ttu-id="bdd4c-196">這些程序使用 Azure PowerShell 來定義和建立 ADF 活動。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-196">These procedures use Azure PowerShell to define and create the ADF activities.</span></span> <span data-ttu-id="bdd4c-197">但是，這些工作也可以透過 Azure 入口網站來完成。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-197">But these tasks can also be accomplished using the Azure portal.</span></span> <span data-ttu-id="bdd4c-198">如需詳細資訊，請參閱[建立資料集](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets)。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-198">For details, see [Create datasets](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).</span></span>
>
>

### <span data-ttu-id="bdd4c-199"><a name="adf-table-onprem-sql"></a>SQL 內部部署資料表</span><span class="sxs-lookup"><span data-stu-id="bdd4c-199"><a name="adf-table-onprem-sql"></a>SQL on-premises Table</span></span>
<span data-ttu-id="bdd4c-200">內部部署 SQL Server 的資料表定義已在下列 JSON 檔案中指定：</span><span class="sxs-lookup"><span data-stu-id="bdd4c-200">The table definition for the on-premises SQL Server is specified in the following JSON file:</span></span>

        {
            "name": "OnPremSQLTable",
            "properties":
            {
                "location":
                {
                "type": "OnPremisesSqlServerTableLocation",
                "tableName": "nyctaxi_data",
                "linkedServiceName": "adfonpremsql"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1,   
                "waitOnExternal":
                {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
                }

                }
            }
        }

<span data-ttu-id="bdd4c-201">這裡未包含資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-201">The column names were not included here.</span></span> <span data-ttu-id="bdd4c-202">您可以子選取資料行名稱，方法是將其包含在此 (如需詳細資料，請參閱 [ADF 文件](../data-factory/data-factory-data-movement-activities.md) 主題)。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-202">You can sub-select on the column names by including them here (for details check the [ADF documentation](../data-factory/data-factory-data-movement-activities.md) topic.</span></span>

<span data-ttu-id="bdd4c-203">將資料表的 JSON 定義複製到名為 *onpremtabledef.json* 的檔案，並將其儲存至已知位置 (此處假設為 *C:\temp\onpremtabledef.json*)。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-203">Copy the JSON definition of the table into a file called *onpremtabledef.json* file and save it to a known location (here assumed to be *C:\temp\onpremtabledef.json*).</span></span> <span data-ttu-id="bdd4c-204">使用下列 Azure PowerShell Cmdlet，在 ADF 中建立資料表：</span><span class="sxs-lookup"><span data-stu-id="bdd4c-204">Create the table in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp –File C:\temp\onpremtabledef.json


### <span data-ttu-id="bdd4c-205"><a name="adf-table-blob-store"></a>Blob 資料表</span><span class="sxs-lookup"><span data-stu-id="bdd4c-205"><a name="adf-table-blob-store"></a>Blob Table</span></span>
<span data-ttu-id="bdd4c-206">輸出 Blob 位置的資料表定義如下 (此說明會將內嵌資料從內部部署對應至 Azure Blob)：</span><span class="sxs-lookup"><span data-stu-id="bdd4c-206">Definition for the table for the output blob location is in the following (this maps the ingested data from on-premises to Azure blob):</span></span>

        {
            "name": "OutputBlobTable",
            "properties":
            {
                "location":
                {
                "type": "AzureBlobLocation",
                "folderPath": "containername",
                "format":
                {
                "type": "TextFormat",
                "columnDelimiter": "\t"
                },
                "linkedServiceName": "adfds"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1
                }
            }
        }

<span data-ttu-id="bdd4c-207">將資料表的 JSON 定義複製到名為 *bloboutputtabledef.json* 的檔案，並將其儲存至已知位置 (此處假設為 *C:\temp\bloboutputtabledef.json*)。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-207">Copy the JSON definition of the table into a file called *bloboutputtabledef.json* file and save it to a known location (here assumed to be *C:\temp\bloboutputtabledef.json*).</span></span> <span data-ttu-id="bdd4c-208">使用下列 Azure PowerShell Cmdlet，在 ADF 中建立資料表：</span><span class="sxs-lookup"><span data-stu-id="bdd4c-208">Create the table in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\bloboutputtabledef.json  

### <span data-ttu-id="bdd4c-209"><a name="adf-table-azure-sq"></a>SQL Azure 資料表</span><span class="sxs-lookup"><span data-stu-id="bdd4c-209"><a name="adf-table-azure-sq"></a>SQL Azure Table</span></span>
<span data-ttu-id="bdd4c-210">SQL Azure 輸出的資料表定義如下 (此結構描述會對應來自 Blob 的資料)：</span><span class="sxs-lookup"><span data-stu-id="bdd4c-210">Definition for the table for the SQL Azure output is in the following (this schema maps the data coming from the blob):</span></span>

    {
        "name": "OutputSQLAzureTable",
        "properties":
        {
            "structure":
            [
                { "name": "column1", type": "String"},
                { "name": "column2", type": "String"}                
            ],
            "location":
            {
                "type": "AzureSqlTableLocation",
                "tableName": "your_db_name",
                "linkedServiceName": "adfdssqlazure_linked_servicename"
            },
            "availability":
            {
                "frequency": "Day",
                "interval": 1            
            }
        }
    }

<span data-ttu-id="bdd4c-211">將資料表的 JSON 定義複製到名為 *AzureSqlTable.json* 的檔案，並將其儲存至已知位置 (此處假設為 *C:\temp\AzureSqlTable.json*)。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-211">Copy the JSON definition of the table into a file called *AzureSqlTable.json* file and save it to a known location (here assumed to be *C:\temp\AzureSqlTable.json*).</span></span> <span data-ttu-id="bdd4c-212">使用下列 Azure PowerShell Cmdlet，在 ADF 中建立資料表：</span><span class="sxs-lookup"><span data-stu-id="bdd4c-212">Create the table in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\AzureSqlTable.json  


## <span data-ttu-id="bdd4c-213"><a name="adf-pipeline"></a>定義和建立管線</span><span class="sxs-lookup"><span data-stu-id="bdd4c-213"><a name="adf-pipeline"></a>Define and create the pipeline</span></span>
<span data-ttu-id="bdd4c-214">指定屬於管線的活動，並使用下列指令碼型程序建立管線。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-214">Specify the activities that belong to the pipeline and create the pipeline with the following script-based procedures.</span></span> <span data-ttu-id="bdd4c-215">JSON 檔案是用來定義管線屬性。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-215">A JSON file is used to define the pipeline properties.</span></span>

* <span data-ttu-id="bdd4c-216">指令碼假設 **管線名稱** 為 *AMLDSProcessPipeline*。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-216">The script assumes that the **pipeline name** is *AMLDSProcessPipeline*.</span></span>
* <span data-ttu-id="bdd4c-217">此外請注意，我們會設定管線週期以每日執行，並使用預設的作業執行時間 (12 am UTC)。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-217">Also note that we set the periodicity of the pipeline to be executed on daily basis and use the default execution time for the job (12 am UTC).</span></span>

> [!NOTE]
> <span data-ttu-id="bdd4c-218">下列程序會使用 Azure PowerShell 來定義和建立 ADF 管線。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-218">The following procedures use Azure PowerShell to define and create the ADF pipeline.</span></span> <span data-ttu-id="bdd4c-219">但是，此工作也可以透過 Azure 入口網站來完成。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-219">But this task can also be accomplished using the Azure portal.</span></span> <span data-ttu-id="bdd4c-220">如需詳細資訊，請參閱[建立管線](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline)。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-220">For details, see [Create pipeline](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).</span></span>
>
>

<span data-ttu-id="bdd4c-221">使用先前提供的資料表定義，將 ADF 的管線定義指定為：</span><span class="sxs-lookup"><span data-stu-id="bdd4c-221">Using the table definitions provided previously, the pipeline definition for the ADF is specified as follows:</span></span>

        {
            "name": "AMLDSProcessPipeline",
            "properties":
            {
                "description" : "This pipeline has one Copy activity that copies data from an on-premises SQL to Azure blob",
                 "activities":
                [
                    {
                        "name": "CopyFromSQLtoBlob",
                        "description": "Copy data from on-premises SQL server to blob",     
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OnPremSQLTable"} ],
                        "outputs": [ {"name": "OutputBlobTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "SqlSource",
                                "sqlReaderQuery": "select * from nyctaxi_data"
                            },
                            "sink":
                            {
                                "type": "BlobSink"
                            }   
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 0,
                            "timeout": "01:00:00"
                        }       

                     },

                    {
                        "name": "CopyFromBlobtoSQLAzure",
                        "description": "Push data to Sql Azure",        
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OutputBlobTable"} ],
                        "outputs": [ {"name": "OutputSQLAzureTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "BlobSource"
                            },
                            "sink":
                            {
                                "type": "SqlSink",
                                "WriteBatchTimeout": "00:5:00",                
                            }            
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 2,
                            "timeout": "02:00:00"
                        }
                     }
                ]
            }
        }

<span data-ttu-id="bdd4c-222">將該管線的 JSON 定義複製到名為 *pipelinedef.json* 的檔案，並將其儲存至已知位置 (此處假設為 *C:\temp\pipelinedef.json*)。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-222">Copy this JSON definition of the pipeline into a file called *pipelinedef.json* file and save it to a known location (here assumed to be *C:\temp\pipelinedef.json*).</span></span> <span data-ttu-id="bdd4c-223">使用下列 Azure PowerShell Cmdlet，在 ADF 中建立管線：</span><span class="sxs-lookup"><span data-stu-id="bdd4c-223">Create the pipeline in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryPipeline  -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\pipelinedef.json

<span data-ttu-id="bdd4c-224">確認您可以在 Azure 傳統入口網站的 ADF 上看見管線，如下所示 (當您按一下圖表時)</span><span class="sxs-lookup"><span data-stu-id="bdd4c-224">Confirm that you can see the pipeline on the ADF in the Azure Classic Portal show up as following (when you click the diagram)</span></span>

![ADF 管線](media/machine-learning-data-science-move-sql-azure-adf/DJP1kji.png)

## <span data-ttu-id="bdd4c-226"><a name="adf-pipeline-start"></a>啟動管線</span><span class="sxs-lookup"><span data-stu-id="bdd4c-226"><a name="adf-pipeline-start"></a>Start the Pipeline</span></span>
<span data-ttu-id="bdd4c-227">現在可使用下列命令來執行管線：</span><span class="sxs-lookup"><span data-stu-id="bdd4c-227">The pipeline can now be run using the following command:</span></span>

    Set-AzureDataFactoryPipelineActivePeriod -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp -StartDateTime startdateZ –EndDateTime enddateZ –Name AMLDSProcessPipeline

<span data-ttu-id="bdd4c-228">*startdate* 和 *enddate* 參數值必須替換為您想要執行管線的實際日期。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-228">The *startdate* and *enddate* parameter values need to be replaced with the actual dates between which you want the pipeline to run.</span></span>

<span data-ttu-id="bdd4c-229">當管線執行時，您應該可以看到資料在選取用於 Blob 的容器中顯示 (每天一個檔案)。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-229">Once the pipeline executes, you should be able to see the data show up in the container selected for the blob, one file per day.</span></span>

<span data-ttu-id="bdd4c-230">請注意，我們尚未運用 ADF 提供的功能，以遞增方式輸送資料。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-230">Note that we have not leveraged the functionality provided by ADF to pipe data incrementally.</span></span> <span data-ttu-id="bdd4c-231">如需如何執行此功能和 ADF 提供之其他功能的詳細資訊，請參閱 [ADF 文件](https://azure.microsoft.com/services/data-factory/)。</span><span class="sxs-lookup"><span data-stu-id="bdd4c-231">For more information on how to do this and other capabilities provided by ADF, see the [ADF documentation](https://azure.microsoft.com/services/data-factory/).</span></span>
