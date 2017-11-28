---
title: "從 FTP 伺服器使用 Azure Data Factory aaaMove 資料 |Microsoft 文件"
description: "深入了解如何從 FTP 伺服器使用 Azure Data Factory toomove 資料。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: eea3bab0-a6e4-4045-ad44-9ce06229c718
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jingwang
ms.openlocfilehash: c707e29532b2a8a870603948cb6150ab857bd6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-ftp-server-by-using-azure-data-factory"></a><span data-ttu-id="d0c5a-103">使用 Azure Data Factory 從 FTP 伺服器移動資料</span><span class="sxs-lookup"><span data-stu-id="d0c5a-103">Move data from an FTP server by using Azure Data Factory</span></span>
<span data-ttu-id="d0c5a-104">本文說明如何 toouse hello 複製在 Azure Data Factory toomove 資料從 FTP 伺服器活動。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-104">This article explains how toouse hello copy activity in Azure Data Factory toomove data from an FTP server.</span></span> <span data-ttu-id="d0c5a-105">它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="d0c5a-106">您可以從 FTP 伺服器支援 tooany 接收資料存放區複製資料。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-106">You can copy data from an FTP server tooany supported sink data store.</span></span> <span data-ttu-id="d0c5a-107">取得一份資料存放區支援接收由 hello 複製活動時，請參閱 hello[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)資料表。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-107">For a list of data stores supported as sinks by hello copy activity, see hello [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="d0c5a-108">Data Factory 目前支援僅從 FTP 伺服器 tooother 資料移動的資料存放區，但不是將資料從其他資料會儲存 tooan FTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-108">Data Factory currently supports only moving data from an FTP server tooother data stores, but not moving data from other data stores tooan FTP server.</span></span> <span data-ttu-id="d0c5a-109">它支援內部部署和雲端 FTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-109">It supports both on-premises and cloud FTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="d0c5a-110">hello 複製活動不會刪除 hello 原始程式檔之後順利複製的 toohello 目的地。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-110">hello copy activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="d0c5a-111">如果您需要 toodelete hello 原始程式檔複製成功之後，建立自訂活動 toodelete hello 檔案，並使用 hello 活動 hello 管線中。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-111">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file, and use hello activity in hello pipeline.</span></span> 

## <a name="enable-connectivity"></a><span data-ttu-id="d0c5a-112">啟用連線能力</span><span class="sxs-lookup"><span data-stu-id="d0c5a-112">Enable connectivity</span></span>
<span data-ttu-id="d0c5a-113">如果您要移動的資料**內部**FTP 伺服器 tooa 雲端資料儲存區 (例如，tooAzure Blob 儲存體)，安裝和使用資料管理閘道器。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-113">If you are moving data from an **on-premises** FTP server tooa cloud data store (for example, tooAzure Blob storage), install and use Data Management Gateway.</span></span> <span data-ttu-id="d0c5a-114">hello 資料管理閘道是安裝在您的內部部署電腦的用戶端代理程式，並可讓雲端服務 tooconnect tooan 在內部部署資源。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-114">hello Data Management Gateway is a client agent that is installed on your on-premises machine, and it allows cloud services tooconnect tooan on-premises resource.</span></span> <span data-ttu-id="d0c5a-115">如需詳細資訊，請參閱[資料管理閘道](data-factory-data-management-gateway.md)文章。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-115">For details, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="d0c5a-116">如需設定 hello 閘道和使用的逐步指示，請參閱[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-116">For step-by-step instructions on setting up hello gateway and using it, see [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="d0c5a-117">即使 hello 伺服器做為服務 (IaaS) 虛擬機器 (VM) 位於 Azure 的基礎結構，您可以使用 hello 閘道 tooconnect tooan FTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-117">You use hello gateway tooconnect tooan FTP server, even if hello server is on an Azure infrastructure as a service (IaaS) virtual machine (VM).</span></span>

<span data-ttu-id="d0c5a-118">它也是可能 tooinstall hello 閘道上 hello 相同內部電腦或 IaaS VM hello FTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-118">It is possible tooinstall hello gateway on hello same on-premises machine or IaaS VM as hello FTP server.</span></span> <span data-ttu-id="d0c5a-119">不過，我們建議您安裝 hello 閘道，在不同的電腦或 IaaS VM tooavoid 資源爭用，以及更佳的效能。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-119">However, we recommend that you install hello gateway on a separate machine or IaaS VM tooavoid resource contention, and for better performance.</span></span> <span data-ttu-id="d0c5a-120">當您在不同電腦上安裝 hello 閘道時，hello 部應該能夠 tooaccess hello FTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-120">When you install hello gateway on a separate machine, hello machine should be able tooaccess hello FTP server.</span></span>

## <a name="get-started"></a><span data-ttu-id="d0c5a-121">開始使用</span><span class="sxs-lookup"><span data-stu-id="d0c5a-121">Get started</span></span>
<span data-ttu-id="d0c5a-122">您可以藉由使用不同的工具 或 API，建立內含複製活動的管線，以便從 FTP 來源移動資料。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-122">You can create a pipeline with a copy activity that moves data from an FTP source by using different tools or APIs.</span></span>

<span data-ttu-id="d0c5a-123">最簡單方式 toocreate hello 管線為 toouse hello**資料 Factory 複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-123">hello easiest way toocreate a pipeline is toouse hello **Data Factory Copy Wizard**.</span></span> <span data-ttu-id="d0c5a-124">如需快速逐步解說，請參閱[教學課程︰使用複製精靈建立管線](data-factory-copy-data-wizard-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough.</span></span>

<span data-ttu-id="d0c5a-125">您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-125">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="d0c5a-126">請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="d0c5a-127">無論您是使用 hello 工具或 Api，執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:</span><span class="sxs-lookup"><span data-stu-id="d0c5a-127">Whether you use hello tools or APIs, perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="d0c5a-128">建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-128">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="d0c5a-129">建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-129">Create **datasets** toorepresent input and output data for hello copy operation.</span></span>
3. <span data-ttu-id="d0c5a-130">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="d0c5a-131">當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-131">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="d0c5a-132">當您使用工具或 Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-132">When you use tools or APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span> <span data-ttu-id="d0c5a-133">如需使用 FTP 資料存放區中的使用的 toocopy 資料的 Data Factory 實體的 JSON 定義的範例，請參閱 hello [JSON 範例： 將資料從 FTP 伺服器 tooAzure blob 複製](#json-example-copy-data-from-ftp-server-to-azure-blob)本文一節。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-133">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an FTP data store, see hello [JSON example: Copy data from FTP server tooAzure blob](#json-example-copy-data-from-ftp-server-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="d0c5a-134">如需支援的檔案和壓縮格式 toouse 的詳細資訊，請參閱[Azure Data Factory 中的檔案及壓縮格式](data-factory-supported-file-and-compression-formats.md)。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-134">For details about supported file and compression formats toouse, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="d0c5a-135">hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooFTP 的 JSON 屬性的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-135">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooFTP.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="d0c5a-136">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="d0c5a-136">Linked service properties</span></span>
<span data-ttu-id="d0c5a-137">hello 下表描述 JSON 項目特定 tooan FTP 連結服務。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-137">hello following table describes JSON elements specific tooan FTP linked service.</span></span>

| <span data-ttu-id="d0c5a-138">屬性</span><span class="sxs-lookup"><span data-stu-id="d0c5a-138">Property</span></span> | <span data-ttu-id="d0c5a-139">說明</span><span class="sxs-lookup"><span data-stu-id="d0c5a-139">Description</span></span> | <span data-ttu-id="d0c5a-140">必要</span><span class="sxs-lookup"><span data-stu-id="d0c5a-140">Required</span></span> | <span data-ttu-id="d0c5a-141">預設值</span><span class="sxs-lookup"><span data-stu-id="d0c5a-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d0c5a-142">類型</span><span class="sxs-lookup"><span data-stu-id="d0c5a-142">type</span></span> |<span data-ttu-id="d0c5a-143">設定此 tooFtpServer。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-143">Set this tooFtpServer.</span></span> |<span data-ttu-id="d0c5a-144">是</span><span class="sxs-lookup"><span data-stu-id="d0c5a-144">Yes</span></span> |&nbsp; |
| <span data-ttu-id="d0c5a-145">主機</span><span class="sxs-lookup"><span data-stu-id="d0c5a-145">host</span></span> |<span data-ttu-id="d0c5a-146">指定 hello 名稱或 IP 位址的 hello FTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-146">Specify hello name or IP address of hello FTP server.</span></span> |<span data-ttu-id="d0c5a-147">是</span><span class="sxs-lookup"><span data-stu-id="d0c5a-147">Yes</span></span> |&nbsp; |
| <span data-ttu-id="d0c5a-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="d0c5a-148">authenticationType</span></span> |<span data-ttu-id="d0c5a-149">指定 hello 的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-149">Specify hello authentication type.</span></span> |<span data-ttu-id="d0c5a-150">是</span><span class="sxs-lookup"><span data-stu-id="d0c5a-150">Yes</span></span> |<span data-ttu-id="d0c5a-151">基本或匿名</span><span class="sxs-lookup"><span data-stu-id="d0c5a-151">Basic, Anonymous</span></span> |
| <span data-ttu-id="d0c5a-152">username</span><span class="sxs-lookup"><span data-stu-id="d0c5a-152">username</span></span> |<span data-ttu-id="d0c5a-153">指定具有存取 toohello FTP 伺服器 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-153">Specify hello user who has access toohello FTP server.</span></span> |<span data-ttu-id="d0c5a-154">否</span><span class="sxs-lookup"><span data-stu-id="d0c5a-154">No</span></span> |&nbsp; |
| <span data-ttu-id="d0c5a-155">password</span><span class="sxs-lookup"><span data-stu-id="d0c5a-155">password</span></span> |<span data-ttu-id="d0c5a-156">指定 hello hello 使用者 （使用者名稱） 的密碼。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-156">Specify hello password for hello user (username).</span></span> |<span data-ttu-id="d0c5a-157">否</span><span class="sxs-lookup"><span data-stu-id="d0c5a-157">No</span></span> |&nbsp; |
| <span data-ttu-id="d0c5a-158">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="d0c5a-158">encryptedCredential</span></span> |<span data-ttu-id="d0c5a-159">指定加密的 hello 認證 tooaccess hello FTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-159">Specify hello encrypted credential tooaccess hello FTP server.</span></span> |<span data-ttu-id="d0c5a-160">否</span><span class="sxs-lookup"><span data-stu-id="d0c5a-160">No</span></span> |&nbsp; |
| <span data-ttu-id="d0c5a-161">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d0c5a-161">gatewayName</span></span> |<span data-ttu-id="d0c5a-162">指定資料管理閘道器 tooconnect tooan 內部 FTP 伺服器中的 hello hello 閘道名稱。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-162">Specify hello name of hello gateway in Data Management Gateway tooconnect tooan on-premises FTP server.</span></span> |<span data-ttu-id="d0c5a-163">否</span><span class="sxs-lookup"><span data-stu-id="d0c5a-163">No</span></span> |&nbsp; |
| <span data-ttu-id="d0c5a-164">連接埠</span><span class="sxs-lookup"><span data-stu-id="d0c5a-164">port</span></span> |<span data-ttu-id="d0c5a-165">指定 hello 的 hello FTP 伺服器正在接聽的通訊埠。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-165">Specify hello port on which hello FTP server is listening.</span></span> |<span data-ttu-id="d0c5a-166">否</span><span class="sxs-lookup"><span data-stu-id="d0c5a-166">No</span></span> |<span data-ttu-id="d0c5a-167">21</span><span class="sxs-lookup"><span data-stu-id="d0c5a-167">21</span></span> |
| <span data-ttu-id="d0c5a-168">enableSsl</span><span class="sxs-lookup"><span data-stu-id="d0c5a-168">enableSsl</span></span> |<span data-ttu-id="d0c5a-169">指定是否 toouse FTP over SSL/TLS 通道。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-169">Specify whether toouse FTP over an SSL/TLS channel.</span></span> |<span data-ttu-id="d0c5a-170">否</span><span class="sxs-lookup"><span data-stu-id="d0c5a-170">No</span></span> |<span data-ttu-id="d0c5a-171">true</span><span class="sxs-lookup"><span data-stu-id="d0c5a-171">true</span></span> |
| <span data-ttu-id="d0c5a-172">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="d0c5a-172">enableServerCertificateValidation</span></span> |<span data-ttu-id="d0c5a-173">指定是否 tooenable 伺服器 SSL 憑證驗證，當您使用 FTP over SSL/TLS 通道。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-173">Specify whether tooenable server SSL certificate validation when you are using FTP over SSL/TLS channel.</span></span> |<span data-ttu-id="d0c5a-174">否</span><span class="sxs-lookup"><span data-stu-id="d0c5a-174">No</span></span> |<span data-ttu-id="d0c5a-175">true</span><span class="sxs-lookup"><span data-stu-id="d0c5a-175">true</span></span> |

### <a name="use-anonymous-authentication"></a><span data-ttu-id="d0c5a-176">使用匿名驗證</span><span class="sxs-lookup"><span data-stu-id="d0c5a-176">Use Anonymous authentication</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {        
            "authenticationType": "Anonymous",
              "host": "myftpserver.com"
        }
    }
}
```

### <a name="use-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="d0c5a-177">使用純文字的使用者名稱和密碼進行基本驗證</span><span class="sxs-lookup"><span data-stu-id="d0c5a-177">Use username and password in plain text for basic authentication</span></span>

```JSON
{
    "name": "FTPLinkedService",
      "properties": {
    "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
      }
}
```

### <a name="use-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="d0c5a-178">使用連接埠、enableSsl、enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="d0c5a-178">Use port, enableSsl, enableServerCertificateValidation</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

### <a name="use-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="d0c5a-179">針對驗證和閘道器使用 encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="d0c5a-179">Use encryptedCredential for authentication and gateway</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "mygateway"
        }
      }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="d0c5a-180">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="d0c5a-180">Dataset properties</span></span>
<span data-ttu-id="d0c5a-181">如需定義資料集的區段和屬性完整清單，請參閱[建立資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-181">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="d0c5a-182">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-182">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="d0c5a-183">hello **typeProperties**區段是不同的資料集的每個型別。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-183">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="d0c5a-184">它提供特定 toohello 資料集類型的資訊。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-184">It provides information that is specific toohello dataset type.</span></span> <span data-ttu-id="d0c5a-185">hello **typeProperties**類型的資料集區段**FileShare**具有下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="d0c5a-185">hello **typeProperties** section for a dataset of type **FileShare** has hello following properties:</span></span>

| <span data-ttu-id="d0c5a-186">屬性</span><span class="sxs-lookup"><span data-stu-id="d0c5a-186">Property</span></span> | <span data-ttu-id="d0c5a-187">說明</span><span class="sxs-lookup"><span data-stu-id="d0c5a-187">Description</span></span> | <span data-ttu-id="d0c5a-188">必要</span><span class="sxs-lookup"><span data-stu-id="d0c5a-188">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d0c5a-189">folderPath</span><span class="sxs-lookup"><span data-stu-id="d0c5a-189">folderPath</span></span> |<span data-ttu-id="d0c5a-190">子路徑 toohello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-190">Subpath toohello folder.</span></span> <span data-ttu-id="d0c5a-191">使用逸出字元 '\' hello 字串中的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-191">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="d0c5a-192">如需範例，請參閱 [範例連結服務和資料集定義](#sample-linked-service-and-dataset-definitions) 。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-192">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="d0c5a-193">您可以結合此屬性與**partitionBy** toohave 資料夾路徑根據配量開始和結束日期時間。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-193">You can combine this property with **partitionBy** toohave folder paths based on slice start and end date-times.</span></span> |<span data-ttu-id="d0c5a-194">是</span><span class="sxs-lookup"><span data-stu-id="d0c5a-194">Yes</span></span> |
| <span data-ttu-id="d0c5a-195">fileName</span><span class="sxs-lookup"><span data-stu-id="d0c5a-195">fileName</span></span> |<span data-ttu-id="d0c5a-196">在 hello 指定 hello hello 檔案名稱**folderPath**如果您想 hello 資料表 toorefer tooa 特定檔案 hello 資料夾中的。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-196">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="d0c5a-197">如果您未指定任何值，這個屬性，hello 資料表會指向 tooall hello 資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-197">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="d0c5a-198">當**fileName**未指定輸出資料集 hello hello 產生檔案名稱是以下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="d0c5a-198">When **fileName** is not specified for an output dataset, hello name of hello generated file is in hello following format:</span></span> <br/><br/><span data-ttu-id="d0c5a-199">Data<Guid>.txt (範例：Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="d0c5a-199">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="d0c5a-200">否</span><span class="sxs-lookup"><span data-stu-id="d0c5a-200">No</span></span> |
| <span data-ttu-id="d0c5a-201">fileFilter</span><span class="sxs-lookup"><span data-stu-id="d0c5a-201">fileFilter</span></span> |<span data-ttu-id="d0c5a-202">在 hello 中指定的檔案子集篩選使用 toobe tooselect **folderPath**，而非所有檔案。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-202">Specify a filter toobe used tooselect a subset of files in hello **folderPath**, rather than all files.</span></span><br/><br/><span data-ttu-id="d0c5a-203">允許的值為︰`*` (多個字元) 和 `?` (單一字元)。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-203">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="d0c5a-204">範例 1：`"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="d0c5a-204">Example 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="d0c5a-205">範例 2：`"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="d0c5a-205">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="d0c5a-206">fileFilter 適用於輸入 FileShare 資料集。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-206">**fileFilter** is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="d0c5a-207">這個屬性不支援 Hadoop 分散式檔案系統 (HDFS)。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-207">This property is not supported with Hadoop Distributed File System (HDFS).</span></span> |<span data-ttu-id="d0c5a-208">否</span><span class="sxs-lookup"><span data-stu-id="d0c5a-208">No</span></span> |
| <span data-ttu-id="d0c5a-209">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="d0c5a-209">partitionedBy</span></span> |<span data-ttu-id="d0c5a-210">使用動態 toospecify **folderPath**和**fileName**時間序列資料的。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-210">Used toospecify a dynamic **folderPath** and **fileName** for time series data.</span></span> <span data-ttu-id="d0c5a-211">例如，您可以指定每小時資料參數化的 **folderPath**。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-211">For example, you can specify a **folderPath** that is parameterized for every hour of data.</span></span> |<span data-ttu-id="d0c5a-212">否</span><span class="sxs-lookup"><span data-stu-id="d0c5a-212">No</span></span> |
| <span data-ttu-id="d0c5a-213">format</span><span class="sxs-lookup"><span data-stu-id="d0c5a-213">format</span></span> | <span data-ttu-id="d0c5a-214">支援下列格式類型的 hello: **TextFormat**， **JsonFormat**， **AvroFormat**， **OrcFormat**， **ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-214">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="d0c5a-215">設定 hello**類型**下格式 tooone 這些值的屬性。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-215">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="d0c5a-216">如需詳細資訊，請參閱 hello[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)， [Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)， [Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)， [Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)，和[Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)區段。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-216">For more information, see hello [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="d0c5a-217">如果您想 toocopy 檔案，因為它們是以檔案為基礎的存放區 （二進位複製） 之間，略過這兩個輸入和輸出資料集定義中的 hello 格式 > 一節。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-217">If you want toocopy files as they are between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="d0c5a-218">否</span><span class="sxs-lookup"><span data-stu-id="d0c5a-218">No</span></span> |
| <span data-ttu-id="d0c5a-219">compression</span><span class="sxs-lookup"><span data-stu-id="d0c5a-219">compression</span></span> | <span data-ttu-id="d0c5a-220">指定 hello 類型和層級的 hello 資料壓縮。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-220">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="d0c5a-221">支援的類型為：GZip、Deflate、BZip2 和 ZipDeflate，而支援的層級為：最佳和最快。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-221">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**, and supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="d0c5a-222">如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-222">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="d0c5a-223">否</span><span class="sxs-lookup"><span data-stu-id="d0c5a-223">No</span></span> |
| <span data-ttu-id="d0c5a-224">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="d0c5a-224">useBinaryTransfer</span></span> |<span data-ttu-id="d0c5a-225">指定是否 toouse hello 二進位傳輸模式。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-225">Specify whether toouse hello binary transfer mode.</span></span> <span data-ttu-id="d0c5a-226">hello 值會針對二進位模式 （這是 hello 預設值），則為 true 和 false 的 ASCII。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-226">hello values are true for binary mode (this is hello default value), and false for ASCII.</span></span> <span data-ttu-id="d0c5a-227">這個屬性只可用時 hello 相關聯的連結的服務類型的型別： FtpServer。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-227">This property can only be used when hello associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="d0c5a-228">否</span><span class="sxs-lookup"><span data-stu-id="d0c5a-228">No</span></span> |

> [!NOTE]
> <span data-ttu-id="d0c5a-229">無法同時使用 fileName 和 fileFilter。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-229">**fileName** and **fileFilter** cannot be used simultaneously.</span></span>

### <a name="use-hello-partionedby-property"></a><span data-ttu-id="d0c5a-230">使用 hello partionedBy 屬性</span><span class="sxs-lookup"><span data-stu-id="d0c5a-230">Use hello partionedBy property</span></span>
<span data-ttu-id="d0c5a-231">如 hello 前一節中所述，您可以指定動態**folderPath**和**fileName**以 hello 時間序列資料的**partitionedBy**屬性。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-231">As mentioned in hello previous section, you can specify a dynamic **folderPath** and **fileName** for time series data with hello **partitionedBy** property.</span></span>

<span data-ttu-id="d0c5a-232">toolearn 有關時間序列資料集、 排程和配量，請參閱[建立資料集](data-factory-create-datasets.md)，[排程與執行](data-factory-scheduling-and-execution.md)，和[建立管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-232">toolearn about time series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="d0c5a-233">範例 1</span><span class="sxs-lookup"><span data-stu-id="d0c5a-233">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="d0c5a-234">在此範例中，Data Factory 系統變數 SliceStart hello 值取代 {Slice} 是，在 hello 格式指定 (YYYYMMDDHH)。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-234">In this example, {Slice} is replaced with hello value of Data Factory system variable SliceStart, in hello format specified (YYYYMMDDHH).</span></span> <span data-ttu-id="d0c5a-235">hello SliceStart 是指 toostart hello 配量時間。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-235">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="d0c5a-236">hello 資料夾路徑是不同的每個配量。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-236">hello folder path is different for each slice.</span></span> <span data-ttu-id="d0c5a-237">(例如：wikidatagateway/wikisampledataout/2014100103 或 wikidatagateway/wikisampledataout/2014100104。)</span><span class="sxs-lookup"><span data-stu-id="d0c5a-237">(For example, wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.)</span></span>

#### <a name="sample-2"></a><span data-ttu-id="d0c5a-238">範例 2</span><span class="sxs-lookup"><span data-stu-id="d0c5a-238">Sample 2</span></span>

```json
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
<span data-ttu-id="d0c5a-239">在此範例中，hello 年、 月、 日和時間的 SliceStart 會擷取至不同的變數所使用的 hello **folderPath**和**fileName**屬性。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-239">In this example, hello year, month, day, and time of SliceStart are extracted into separate variables that are used by hello **folderPath** and **fileName** properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="d0c5a-240">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="d0c5a-240">Copy activity properties</span></span>
<span data-ttu-id="d0c5a-241">如需可用來定義活動的區段和屬性完整清單，請參閱[建立管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-241">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="d0c5a-242">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-242">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="d0c5a-243">屬性用於 hello **typeProperties**區段 hello hello 上的活動，換句話說，每個活動類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-243">Properties available in hello **typeProperties** section of hello activity, on hello other hand, vary with each activity type.</span></span> <span data-ttu-id="d0c5a-244">Hello 複製活動，根據 hello 類型的來源與接收 hello 類型屬性而有所不同。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-244">For hello copy activity, hello type properties vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="d0c5a-245">複製活動中，當 hello 來源的類型為**FileSystemSource**，hello 下列屬性可用於**typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="d0c5a-245">In copy activity, when hello source is of type **FileSystemSource**, hello following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="d0c5a-246">屬性</span><span class="sxs-lookup"><span data-stu-id="d0c5a-246">Property</span></span> | <span data-ttu-id="d0c5a-247">說明</span><span class="sxs-lookup"><span data-stu-id="d0c5a-247">Description</span></span> | <span data-ttu-id="d0c5a-248">允許的值</span><span class="sxs-lookup"><span data-stu-id="d0c5a-248">Allowed values</span></span> | <span data-ttu-id="d0c5a-249">必要</span><span class="sxs-lookup"><span data-stu-id="d0c5a-249">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d0c5a-250">遞迴</span><span class="sxs-lookup"><span data-stu-id="d0c5a-250">recursive</span></span> |<span data-ttu-id="d0c5a-251">指出是否 hello 讀取資料以遞迴方式從 hello 子資料夾，或只 hello 指定的資料夾。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-251">Indicates whether hello data is read recursively from hello subfolders, or only from hello specified folder.</span></span> |<span data-ttu-id="d0c5a-252">True/False (預設值為 False)</span><span class="sxs-lookup"><span data-stu-id="d0c5a-252">True, False (default)</span></span> |<span data-ttu-id="d0c5a-253">否</span><span class="sxs-lookup"><span data-stu-id="d0c5a-253">No</span></span> |

## <a name="json-example-copy-data-from-ftp-server-tooazure-blob"></a><span data-ttu-id="d0c5a-254">JSON 範例： 從 FTP 伺服器 tooAzure Blob 複製資料</span><span class="sxs-lookup"><span data-stu-id="d0c5a-254">JSON example: Copy data from FTP server tooAzure Blob</span></span>
<span data-ttu-id="d0c5a-255">這個範例示範如何從 FTP 伺服器 tooAzure Blob 儲存體 toocopy 資料。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-255">This sample shows how toocopy data from an FTP server tooAzure Blob storage.</span></span> <span data-ttu-id="d0c5a-256">不過，資料可以複製直接的 hello tooany 接收器中所述的 hello[支援資料存放區和格式](data-factory-data-movement-activities.md#supported-data-stores-and-formats)，使用 Data Factory 中的 hello 複製活動。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-256">However, data can be copied directly tooany of hello sinks stated in hello [supported data stores and formats](data-factory-data-movement-activities.md#supported-data-stores-and-formats), by using hello copy activity in Data Factory.</span></span>  

<span data-ttu-id="d0c5a-257">hello 下列範例會提供範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)， [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)，或[PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="d0c5a-257">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span></span>

* <span data-ttu-id="d0c5a-258">[FtpServer](#linked-service-properties) 類型的連結服務</span><span class="sxs-lookup"><span data-stu-id="d0c5a-258">A linked service of type [FtpServer](#linked-service-properties)</span></span>
* <span data-ttu-id="d0c5a-259">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務</span><span class="sxs-lookup"><span data-stu-id="d0c5a-259">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="d0c5a-260">[FileShare](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="d0c5a-260">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties)</span></span>
* <span data-ttu-id="d0c5a-261">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="d0c5a-261">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="d0c5a-262">具有使用 [FileSystemSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)</span><span class="sxs-lookup"><span data-stu-id="d0c5a-262">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="d0c5a-263">hello 範例將資料從 FTP 伺服器 tooan Azure blob 的每個小時。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-263">hello sample copies data from an FTP server tooan Azure blob every hour.</span></span> <span data-ttu-id="d0c5a-264">這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-264">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

### <a name="ftp-linked-service"></a><span data-ttu-id="d0c5a-265">FTP 連結服務</span><span class="sxs-lookup"><span data-stu-id="d0c5a-265">FTP linked service</span></span>

<span data-ttu-id="d0c5a-266">這個範例會使用基本驗證，以 hello 使用者名稱和密碼以純文字。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-266">This example uses basic authentication, with hello user name and password in plain text.</span></span> <span data-ttu-id="d0c5a-267">您也可以使用下列方式 hello:</span><span class="sxs-lookup"><span data-stu-id="d0c5a-267">You can also use one of hello following ways:</span></span>

* <span data-ttu-id="d0c5a-268">匿名驗證</span><span class="sxs-lookup"><span data-stu-id="d0c5a-268">Anonymous authentication</span></span>
* <span data-ttu-id="d0c5a-269">基本驗證與加密認證</span><span class="sxs-lookup"><span data-stu-id="d0c5a-269">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="d0c5a-270">透過 SSL/TLS 的 FTP (FTPS)</span><span class="sxs-lookup"><span data-stu-id="d0c5a-270">FTP over SSL/TLS (FTPS)</span></span>

<span data-ttu-id="d0c5a-271">請參閱 hello [FTP 連結服務](#linked-service-properties)不同類型的驗證，您可以使用的區段。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-271">See hello [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
    "type": "FtpServer",
    "typeProperties": {
        "host": "myftpserver.com",           
        "authenticationType": "Basic",
        "username": "Admin",
        "password": "123456"
    }
  }
}
```
### <a name="azure-storage-linked-service"></a><span data-ttu-id="d0c5a-272">Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="d0c5a-272">Azure Storage linked service</span></span>

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
### <a name="ftp-input-dataset"></a><span data-ttu-id="d0c5a-273">FTP 輸入資料集</span><span class="sxs-lookup"><span data-stu-id="d0c5a-273">FTP input dataset</span></span>

<span data-ttu-id="d0c5a-274">此資料集是指 toohello FTP 資料夾`mysharedfolder`和檔案`test.csv`。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-274">This dataset refers toohello FTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="d0c5a-275">hello 管線複製 hello 檔案 toohello 目的地。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-275">hello pipeline copies hello file toohello destination.</span></span>

<span data-ttu-id="d0c5a-276">設定**外部**太**true**該 hello 資料集是外部 toohello 資料處理站，並不產生 hello data factory 中的活動時，會通知 hello Data Factory 服務。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-276">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory, and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "FTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "FTPLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv",
      "useBinaryTransfer": true
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="d0c5a-277">Azure Blob 輸出資料集</span><span class="sxs-lookup"><span data-stu-id="d0c5a-277">Azure Blob output dataset</span></span>

<span data-ttu-id="d0c5a-278">資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-278">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="d0c5a-279">hello blob 的 hello 資料夾路徑會動態評估，依據 hello 正在處理的 hello 配量的開始時間。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-279">hello folder path for hello blob is dynamically evaluated, based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="d0c5a-280">hello 資料夾路徑會使用 hello 的 hello 開始時間的年、 月、 日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-280">hello folder path uses hello year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/ftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="a-copy-activity-in-a-pipeline-with-file-system-source-and-blob-sink"></a><span data-ttu-id="d0c5a-281">具有檔案系統來源和 blob 接收器的管線中複製活動</span><span class="sxs-lookup"><span data-stu-id="d0c5a-281">A copy activity in a pipeline with file system source and blob sink</span></span>

<span data-ttu-id="d0c5a-282">hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-282">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="d0c5a-283">在 hello 管線 JSON 定義中，hello**來源**類型設定得**FileSystemSource**，和 hello**接收**類型設定得**BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-283">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and hello **sink** type is set too**BlobSink**.</span></span>

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00Z",
        "end": "2016-08-24T19:00:00Z"
    }
}
```
> [!NOTE]
> <span data-ttu-id="d0c5a-284">toomap 資料行從來源資料集 toocolumns 從接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-284">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0c5a-285">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d0c5a-285">Next steps</span></span>
<span data-ttu-id="d0c5a-286">請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="d0c5a-286">See hello following articles:</span></span>

* <span data-ttu-id="d0c5a-287">關於金鑰 toolearn 因素影響效能的 Data Factory 中的資料移動 （複製活動） 和各種方式 toooptimize 的請參閱 hello[複製活動效能及微調指南](data-factory-copy-activity-performance.md)。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-287">toolearn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways toooptimize it, see hello [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="d0c5a-288">複製活動與建立管線的逐步指示，請參閱 hello[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="d0c5a-288">For step-by-step instructions for creating a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
