---
title: "使用 Azure Data Factory 從 FTP 伺服器移動資料 | Microsoft Docs"
description: "了解如何使用 Azure Data Factory 從 FTP 伺服器移動資料。"
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
ms.openlocfilehash: f8f31f3a2ee02c964737dd32145499f3dcfd0624
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-an-ftp-server-by-using-azure-data-factory"></a><span data-ttu-id="9e7d8-103">使用 Azure Data Factory 從 FTP 伺服器移動資料</span><span class="sxs-lookup"><span data-stu-id="9e7d8-103">Move data from an FTP server by using Azure Data Factory</span></span>
<span data-ttu-id="9e7d8-104">本文說明如何使用 Azure Data Factory 中的「複製活動」，從 FTP 伺服器移動資料。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-104">This article explains how to use the copy activity in Azure Data Factory to move data from an FTP server.</span></span> <span data-ttu-id="9e7d8-105">本文是根據[資料移動活動](data-factory-data-movement-activities.md)一文，該文提供使用複製活動來移動資料的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-105">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="9e7d8-106">您可以將資料從 FTP 伺服器複製到任何支援的接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-106">You can copy data from an FTP server to any supported sink data store.</span></span> <span data-ttu-id="9e7d8-107">如需複製活動所支援作為接收器的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)資料表。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-107">For a list of data stores supported as sinks by the copy activity, see the [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="9e7d8-108">資料處理站目前只支援將資料從 FTP 伺服器移到其他資料存放區，而不支援將資料從其他資料存放區移到 FTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-108">Data Factory currently supports only moving data from an FTP server to other data stores, but not moving data from other data stores to an FTP server.</span></span> <span data-ttu-id="9e7d8-109">它支援內部部署和雲端 FTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-109">It supports both on-premises and cloud FTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="9e7d8-110">來源檔案成功複製至目的地後，「複製活動」不會將它刪除。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-110">The copy activity does not delete the source file after it is successfully copied to the destination.</span></span> <span data-ttu-id="9e7d8-111">如果您需要在成功複製後刪除來源檔案，請建立自訂活動來刪除檔案，並在管道中使用該活動。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-111">If you need to delete the source file after a successful copy, create a custom activity to delete the file, and use the activity in the pipeline.</span></span> 

## <a name="enable-connectivity"></a><span data-ttu-id="9e7d8-112">啟用連線能力</span><span class="sxs-lookup"><span data-stu-id="9e7d8-112">Enable connectivity</span></span>
<span data-ttu-id="9e7d8-113">如果您要將資料從內部部署 FTP 伺服器移到雲端資料存放區 (例如：移到 Azure Blob 儲存體)，請安裝並使用資料管理閘道。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-113">If you are moving data from an **on-premises** FTP server to a cloud data store (for example, to Azure Blob storage), install and use Data Management Gateway.</span></span> <span data-ttu-id="9e7d8-114">資料管理閘道是安裝在內部部署電腦上的用戶端代理程式，允許雲端服務連接至內部部署資源。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-114">The Data Management Gateway is a client agent that is installed on your on-premises machine, and it allows cloud services to connect to an on-premises resource.</span></span> <span data-ttu-id="9e7d8-115">如需詳細資訊，請參閱[資料管理閘道](data-factory-data-management-gateway.md)文章。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-115">For details, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="9e7d8-116">請參閱[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)一文來了解設定和使用閘道器的逐步說明。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-116">For step-by-step instructions on setting up the gateway and using it, see [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="9e7d8-117">即使伺服器位於 Azure 架構即服務 (IaaS) 虛擬機器 (VM) 上，您還是可以使用閘道器連接至 FTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-117">You use the gateway to connect to an FTP server, even if the server is on an Azure infrastructure as a service (IaaS) virtual machine (VM).</span></span>

<span data-ttu-id="9e7d8-118">您可以將閘道器安裝在與 FTP 伺服器相同的內部部署電腦或 IaaS VM 上。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-118">It is possible to install the gateway on the same on-premises machine or IaaS VM as the FTP server.</span></span> <span data-ttu-id="9e7d8-119">不過，建議您將閘道器安裝在個別的機器 或 IaaS VM 上，除了可避免發生資源爭用的情況之外，也可獲得較佳的效能。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-119">However, we recommend that you install the gateway on a separate machine or IaaS VM to avoid resource contention, and for better performance.</span></span> <span data-ttu-id="9e7d8-120">當您在不同電腦上安裝閘道時，電腦應該能夠存取 FTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-120">When you install the gateway on a separate machine, the machine should be able to access the FTP server.</span></span>

## <a name="get-started"></a><span data-ttu-id="9e7d8-121">開始使用</span><span class="sxs-lookup"><span data-stu-id="9e7d8-121">Get started</span></span>
<span data-ttu-id="9e7d8-122">您可以藉由使用不同的工具 或 API，建立內含複製活動的管線，以便從 FTP 來源移動資料。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-122">You can create a pipeline with a copy activity that moves data from an FTP source by using different tools or APIs.</span></span>

<span data-ttu-id="9e7d8-123">建立管線的最簡單方式就是使用「資料處理站複製精靈」。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-123">The easiest way to create a pipeline is to use the **Data Factory Copy Wizard**.</span></span> <span data-ttu-id="9e7d8-124">如需快速逐步解說，請參閱[教學課程︰使用複製精靈建立管線](data-factory-copy-data-wizard-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough.</span></span>

<span data-ttu-id="9e7d8-125">您也可以使用下列工具來建立管線︰Azure 入口網站、Visual Studio、PowerShell、Azure Resource Manager 範本、.NET API 及 REST API。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-125">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="9e7d8-126">如需建立內含複製活動之管線的逐步指示，請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="9e7d8-127">不論您是使用工具還是 API，都需執行下列步驟來建立將資料從來源資料存放區移到接收資料存放區的管線：</span><span class="sxs-lookup"><span data-stu-id="9e7d8-127">Whether you use the tools or APIs, perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="9e7d8-128">建立**連結服務**，將輸入和輸出資料存放區連結到資料處理站。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-128">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="9e7d8-129">建立**資料集**，代表複製作業的輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-129">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="9e7d8-130">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="9e7d8-131">使用精靈時，精靈會自動為您建立這些 Data Factory 實體 (已連結的服務、資料集及管線) 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-131">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="9e7d8-132">使用工具或 API (.NET API 除外) 時，您需使用 JSON 格式來定義這些資料處理站實體。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-132">When you use tools or APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span> <span data-ttu-id="9e7d8-133">如需相關範例，其中含有用來從 FTP 資料存放區複製資料的資料處理站實體的 JSON 定義，請參閱本文的 [JSON 範例：將資料從 FTP 伺服器複製到 Azure Blob](#json-example-copy-data-from-ftp-server-to-azure-blob) 一節。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-133">For a sample with JSON definitions for Data Factory entities that are used to copy data from an FTP data store, see the [JSON example: Copy data from FTP server to Azure blob](#json-example-copy-data-from-ftp-server-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="9e7d8-134">如需可用的支援檔案和壓縮格式的詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md)。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-134">For details about supported file and compression formats to use, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="9e7d8-135">下列各節提供 JSON 屬性的相關詳細資料，這些屬性是用來定義 FTP 特定的資料處理站實體：</span><span class="sxs-lookup"><span data-stu-id="9e7d8-135">The following sections provide details about JSON properties that are used to define Data Factory entities specific to FTP.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="9e7d8-136">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="9e7d8-136">Linked service properties</span></span>
<span data-ttu-id="9e7d8-137">下表提供 FTP 連結服務專屬的 JSON 元素說明。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-137">The following table describes JSON elements specific to an FTP linked service.</span></span>

| <span data-ttu-id="9e7d8-138">屬性</span><span class="sxs-lookup"><span data-stu-id="9e7d8-138">Property</span></span> | <span data-ttu-id="9e7d8-139">說明</span><span class="sxs-lookup"><span data-stu-id="9e7d8-139">Description</span></span> | <span data-ttu-id="9e7d8-140">必要</span><span class="sxs-lookup"><span data-stu-id="9e7d8-140">Required</span></span> | <span data-ttu-id="9e7d8-141">預設值</span><span class="sxs-lookup"><span data-stu-id="9e7d8-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9e7d8-142">類型</span><span class="sxs-lookup"><span data-stu-id="9e7d8-142">type</span></span> |<span data-ttu-id="9e7d8-143">設定為 FtpServer。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-143">Set this to FtpServer.</span></span> |<span data-ttu-id="9e7d8-144">是</span><span class="sxs-lookup"><span data-stu-id="9e7d8-144">Yes</span></span> |&nbsp; |
| <span data-ttu-id="9e7d8-145">主機</span><span class="sxs-lookup"><span data-stu-id="9e7d8-145">host</span></span> |<span data-ttu-id="9e7d8-146">指定 FTP 伺服器的名稱或 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-146">Specify the name or IP address of the FTP server.</span></span> |<span data-ttu-id="9e7d8-147">是</span><span class="sxs-lookup"><span data-stu-id="9e7d8-147">Yes</span></span> |&nbsp; |
| <span data-ttu-id="9e7d8-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="9e7d8-148">authenticationType</span></span> |<span data-ttu-id="9e7d8-149">指定驗證類型。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-149">Specify the authentication type.</span></span> |<span data-ttu-id="9e7d8-150">是</span><span class="sxs-lookup"><span data-stu-id="9e7d8-150">Yes</span></span> |<span data-ttu-id="9e7d8-151">基本或匿名</span><span class="sxs-lookup"><span data-stu-id="9e7d8-151">Basic, Anonymous</span></span> |
| <span data-ttu-id="9e7d8-152">username</span><span class="sxs-lookup"><span data-stu-id="9e7d8-152">username</span></span> |<span data-ttu-id="9e7d8-153">指定擁有 FTP 伺服器存取權限的使用者。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-153">Specify the user who has access to the FTP server.</span></span> |<span data-ttu-id="9e7d8-154">否</span><span class="sxs-lookup"><span data-stu-id="9e7d8-154">No</span></span> |&nbsp; |
| <span data-ttu-id="9e7d8-155">password</span><span class="sxs-lookup"><span data-stu-id="9e7d8-155">password</span></span> |<span data-ttu-id="9e7d8-156">指定使用者 (使用者名稱) 的密碼。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-156">Specify the password for the user (username).</span></span> |<span data-ttu-id="9e7d8-157">否</span><span class="sxs-lookup"><span data-stu-id="9e7d8-157">No</span></span> |&nbsp; |
| <span data-ttu-id="9e7d8-158">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="9e7d8-158">encryptedCredential</span></span> |<span data-ttu-id="9e7d8-159">指定用來存取 FTP 伺服器的加密認證。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-159">Specify the encrypted credential to access the FTP server.</span></span> |<span data-ttu-id="9e7d8-160">否</span><span class="sxs-lookup"><span data-stu-id="9e7d8-160">No</span></span> |&nbsp; |
| <span data-ttu-id="9e7d8-161">gatewayName</span><span class="sxs-lookup"><span data-stu-id="9e7d8-161">gatewayName</span></span> |<span data-ttu-id="9e7d8-162">指定資料管理閘道中連結至內部部署 FTP 伺服器的閘道器名稱。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-162">Specify the name of the gateway in Data Management Gateway to connect to an on-premises FTP server.</span></span> |<span data-ttu-id="9e7d8-163">否</span><span class="sxs-lookup"><span data-stu-id="9e7d8-163">No</span></span> |&nbsp; |
| <span data-ttu-id="9e7d8-164">連接埠</span><span class="sxs-lookup"><span data-stu-id="9e7d8-164">port</span></span> |<span data-ttu-id="9e7d8-165">指定 FTP 伺服器所接聽的連接埠</span><span class="sxs-lookup"><span data-stu-id="9e7d8-165">Specify the port on which the FTP server is listening.</span></span> |<span data-ttu-id="9e7d8-166">否</span><span class="sxs-lookup"><span data-stu-id="9e7d8-166">No</span></span> |<span data-ttu-id="9e7d8-167">21</span><span class="sxs-lookup"><span data-stu-id="9e7d8-167">21</span></span> |
| <span data-ttu-id="9e7d8-168">enableSsl</span><span class="sxs-lookup"><span data-stu-id="9e7d8-168">enableSsl</span></span> |<span data-ttu-id="9e7d8-169">指定是否使用透過 SSL/TLS 的 FTP 通道。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-169">Specify whether to use FTP over an SSL/TLS channel.</span></span> |<span data-ttu-id="9e7d8-170">否</span><span class="sxs-lookup"><span data-stu-id="9e7d8-170">No</span></span> |<span data-ttu-id="9e7d8-171">true</span><span class="sxs-lookup"><span data-stu-id="9e7d8-171">true</span></span> |
| <span data-ttu-id="9e7d8-172">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="9e7d8-172">enableServerCertificateValidation</span></span> |<span data-ttu-id="9e7d8-173">指定是否在使用透過 SSL/TLS 的 FTP 通道時啟用伺服器 SSL 憑證驗證。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-173">Specify whether to enable server SSL certificate validation when you are using FTP over SSL/TLS channel.</span></span> |<span data-ttu-id="9e7d8-174">否</span><span class="sxs-lookup"><span data-stu-id="9e7d8-174">No</span></span> |<span data-ttu-id="9e7d8-175">true</span><span class="sxs-lookup"><span data-stu-id="9e7d8-175">true</span></span> |

### <a name="use-anonymous-authentication"></a><span data-ttu-id="9e7d8-176">使用匿名驗證</span><span class="sxs-lookup"><span data-stu-id="9e7d8-176">Use Anonymous authentication</span></span>

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

### <a name="use-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="9e7d8-177">使用純文字的使用者名稱和密碼進行基本驗證</span><span class="sxs-lookup"><span data-stu-id="9e7d8-177">Use username and password in plain text for basic authentication</span></span>

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

### <a name="use-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="9e7d8-178">使用連接埠、enableSsl、enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="9e7d8-178">Use port, enableSsl, enableServerCertificateValidation</span></span>

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

### <a name="use-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="9e7d8-179">針對驗證和閘道器使用 encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="9e7d8-179">Use encryptedCredential for authentication and gateway</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="9e7d8-180">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="9e7d8-180">Dataset properties</span></span>
<span data-ttu-id="9e7d8-181">如需定義資料集的區段和屬性完整清單，請參閱[建立資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-181">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="9e7d8-182">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-182">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="9e7d8-183">不同類型資料集的 **typeProperties** 區段不同。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-183">The **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="9e7d8-184">它提供資料集類型的特定資訊。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-184">It provides information that is specific to the dataset type.</span></span> <span data-ttu-id="9e7d8-185">FileShare 類型資料集的 typeProperties 區段有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="9e7d8-185">The **typeProperties** section for a dataset of type **FileShare** has the following properties:</span></span>

| <span data-ttu-id="9e7d8-186">屬性</span><span class="sxs-lookup"><span data-stu-id="9e7d8-186">Property</span></span> | <span data-ttu-id="9e7d8-187">說明</span><span class="sxs-lookup"><span data-stu-id="9e7d8-187">Description</span></span> | <span data-ttu-id="9e7d8-188">必要</span><span class="sxs-lookup"><span data-stu-id="9e7d8-188">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9e7d8-189">folderPath</span><span class="sxs-lookup"><span data-stu-id="9e7d8-189">folderPath</span></span> |<span data-ttu-id="9e7d8-190">資料夾的子路徑。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-190">Subpath to the folder.</span></span> <span data-ttu-id="9e7d8-191">使用逸出字元 ‘ \ ’ 當做字串中的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-191">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="9e7d8-192">如需範例，請參閱 [範例連結服務和資料集定義](#sample-linked-service-and-dataset-definitions) 。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-192">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="9e7d8-193">您可以結合此屬性與 partitionBy ，讓資料夾路徑以配量開始和結束日期時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-193">You can combine this property with **partitionBy** to have folder paths based on slice start and end date-times.</span></span> |<span data-ttu-id="9e7d8-194">是</span><span class="sxs-lookup"><span data-stu-id="9e7d8-194">Yes</span></span> |
| <span data-ttu-id="9e7d8-195">fileName</span><span class="sxs-lookup"><span data-stu-id="9e7d8-195">fileName</span></span> |<span data-ttu-id="9e7d8-196">如果您想要資料表參考資料夾中的特定檔案，請指定 **folderPath** 中的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-196">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="9e7d8-197">如果沒有為此屬性指定任何值，資料表會指向資料夾中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-197">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="9e7d8-198">若未指定輸出資料集的 fileName，所產生檔案的名稱是下列格式︰</span><span class="sxs-lookup"><span data-stu-id="9e7d8-198">When **fileName** is not specified for an output dataset, the name of the generated file is in the following format:</span></span> <br/><br/><span data-ttu-id="9e7d8-199">Data<Guid>.txt (範例：Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="9e7d8-199">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="9e7d8-200">否</span><span class="sxs-lookup"><span data-stu-id="9e7d8-200">No</span></span> |
| <span data-ttu-id="9e7d8-201">fileFilter</span><span class="sxs-lookup"><span data-stu-id="9e7d8-201">fileFilter</span></span> |<span data-ttu-id="9e7d8-202">指定要用來在 folderPath (而不是所有檔案) 中選取檔案子集的篩選器。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-202">Specify a filter to be used to select a subset of files in the **folderPath**, rather than all files.</span></span><br/><br/><span data-ttu-id="9e7d8-203">允許的值為︰`*` (多個字元) 和 `?` (單一字元)。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-203">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="9e7d8-204">範例 1：`"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="9e7d8-204">Example 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="9e7d8-205">範例 2：`"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="9e7d8-205">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="9e7d8-206">fileFilter 適用於輸入 FileShare 資料集。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-206">**fileFilter** is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="9e7d8-207">這個屬性不支援 Hadoop 分散式檔案系統 (HDFS)。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-207">This property is not supported with Hadoop Distributed File System (HDFS).</span></span> |<span data-ttu-id="9e7d8-208">否</span><span class="sxs-lookup"><span data-stu-id="9e7d8-208">No</span></span> |
| <span data-ttu-id="9e7d8-209">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="9e7d8-209">partitionedBy</span></span> |<span data-ttu-id="9e7d8-210">用來指定時間序列資料的動態 folderPath 和 filename。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-210">Used to specify a dynamic **folderPath** and **fileName** for time series data.</span></span> <span data-ttu-id="9e7d8-211">例如，您可以指定每小時資料參數化的 **folderPath**。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-211">For example, you can specify a **folderPath** that is parameterized for every hour of data.</span></span> |<span data-ttu-id="9e7d8-212">否</span><span class="sxs-lookup"><span data-stu-id="9e7d8-212">No</span></span> |
| <span data-ttu-id="9e7d8-213">format</span><span class="sxs-lookup"><span data-stu-id="9e7d8-213">format</span></span> | <span data-ttu-id="9e7d8-214">支援下列格式類型：**TextFormat**、**JsonFormat**、**AvroFormat**、**OrcFormat**、**ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-214">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="9e7d8-215">將格式下的 **type** 屬性設定為這些值其中之一。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-215">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="9e7d8-216">如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-216">For more information, see the [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="9e7d8-217">如果您想要在以檔案為基礎的存放區之間依原樣複製檔案 (二進位複本)，請在輸入和輸出資料集定義中略過格式區段。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-217">If you want to copy files as they are between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="9e7d8-218">否</span><span class="sxs-lookup"><span data-stu-id="9e7d8-218">No</span></span> |
| <span data-ttu-id="9e7d8-219">compression</span><span class="sxs-lookup"><span data-stu-id="9e7d8-219">compression</span></span> | <span data-ttu-id="9e7d8-220">指定此資料的壓縮類型和層級。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-220">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="9e7d8-221">支援的類型為：GZip、Deflate、BZip2 和 ZipDeflate，而支援的層級為：最佳和最快。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-221">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**, and supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="9e7d8-222">如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-222">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="9e7d8-223">否</span><span class="sxs-lookup"><span data-stu-id="9e7d8-223">No</span></span> |
| <span data-ttu-id="9e7d8-224">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="9e7d8-224">useBinaryTransfer</span></span> |<span data-ttu-id="9e7d8-225">指定是否使用二進位傳輸模式。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-225">Specify whether to use the binary transfer mode.</span></span> <span data-ttu-id="9e7d8-226">值對二進位模式為真 (為預設值)，對 ASCII 為則為假。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-226">The values are true for binary mode (this is the default value), and false for ASCII.</span></span> <span data-ttu-id="9e7d8-227">只有在相關聯的連結服務類型的類型為 FtpServer 時，才可以使用這個屬性。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-227">This property can only be used when the associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="9e7d8-228">否</span><span class="sxs-lookup"><span data-stu-id="9e7d8-228">No</span></span> |

> [!NOTE]
> <span data-ttu-id="9e7d8-229">無法同時使用 fileName 和 fileFilter。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-229">**fileName** and **fileFilter** cannot be used simultaneously.</span></span>

### <a name="use-the-partionedby-property"></a><span data-ttu-id="9e7d8-230">使用 partionedBy 屬性</span><span class="sxs-lookup"><span data-stu-id="9e7d8-230">Use the partionedBy property</span></span>
<span data-ttu-id="9e7d8-231">如上一節所述，您可以利用 partitionedBy 屬性指定時間序列資料的動態 folderPath 和 fileName。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-231">As mentioned in the previous section, you can specify a dynamic **folderPath** and **fileName** for time series data with the **partitionedBy** property.</span></span>

<span data-ttu-id="9e7d8-232">若要了解時間序列資料集、排程和配量，請參閱[建立資料集](data-factory-create-datasets.md)、[排程和執行](data-factory-scheduling-and-execution.md)以及[建立管線](data-factory-create-pipelines.md)等文章。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-232">To learn about time series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="9e7d8-233">範例 1</span><span class="sxs-lookup"><span data-stu-id="9e7d8-233">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="9e7d8-234">在此範例中，{Slice} 會取代成資料處理站系統變數 SliceStart 的值 (使用指定的格式 (YYYYMMDDHH))。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-234">In this example, {Slice} is replaced with the value of Data Factory system variable SliceStart, in the format specified (YYYYMMDDHH).</span></span> <span data-ttu-id="9e7d8-235">SliceStart 是指配量的開始時間。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-235">The SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="9e7d8-236">每個配量的資料夾路徑都不同。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-236">The folder path is different for each slice.</span></span> <span data-ttu-id="9e7d8-237">(例如：wikidatagateway/wikisampledataout/2014100103 或 wikidatagateway/wikisampledataout/2014100104。)</span><span class="sxs-lookup"><span data-stu-id="9e7d8-237">(For example, wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.)</span></span>

#### <a name="sample-2"></a><span data-ttu-id="9e7d8-238">範例 2</span><span class="sxs-lookup"><span data-stu-id="9e7d8-238">Sample 2</span></span>

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
<span data-ttu-id="9e7d8-239">在此範例中，SliceStart 的年、月、日和時間會擷取到 folderPath 和 fileName 屬性所使用的個別變數。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-239">In this example, the year, month, day, and time of SliceStart are extracted into separate variables that are used by the **folderPath** and **fileName** properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="9e7d8-240">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="9e7d8-240">Copy activity properties</span></span>
<span data-ttu-id="9e7d8-241">如需可用來定義活動的區段和屬性完整清單，請參閱[建立管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-241">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="9e7d8-242">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-242">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="9e7d8-243">另一方面，活動的 typeProperties 區段中可用的屬性會隨著每個活動類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-243">Properties available in the **typeProperties** section of the activity, on the other hand, vary with each activity type.</span></span> <span data-ttu-id="9e7d8-244">就複製活動而言，類型屬性會根據來源和接收的類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-244">For the copy activity, the type properties vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="9e7d8-245">在複製活動中，如果來源的類型為 FileSystemSource，則 typeProperties 區段會有下列可用屬性：</span><span class="sxs-lookup"><span data-stu-id="9e7d8-245">In copy activity, when the source is of type **FileSystemSource**, the following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="9e7d8-246">屬性</span><span class="sxs-lookup"><span data-stu-id="9e7d8-246">Property</span></span> | <span data-ttu-id="9e7d8-247">說明</span><span class="sxs-lookup"><span data-stu-id="9e7d8-247">Description</span></span> | <span data-ttu-id="9e7d8-248">允許的值</span><span class="sxs-lookup"><span data-stu-id="9e7d8-248">Allowed values</span></span> | <span data-ttu-id="9e7d8-249">必要</span><span class="sxs-lookup"><span data-stu-id="9e7d8-249">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9e7d8-250">遞迴</span><span class="sxs-lookup"><span data-stu-id="9e7d8-250">recursive</span></span> |<span data-ttu-id="9e7d8-251">指出是否從子資料夾、或只有從指定的資料夾，以遞迴方式讀取資料。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-251">Indicates whether the data is read recursively from the subfolders, or only from the specified folder.</span></span> |<span data-ttu-id="9e7d8-252">True/False (預設值為 False)</span><span class="sxs-lookup"><span data-stu-id="9e7d8-252">True, False (default)</span></span> |<span data-ttu-id="9e7d8-253">否</span><span class="sxs-lookup"><span data-stu-id="9e7d8-253">No</span></span> |

## <a name="json-example-copy-data-from-ftp-server-to-azure-blob"></a><span data-ttu-id="9e7d8-254">JSON 範例：將資料從 FTP 伺服器複製到 Azure Blob</span><span class="sxs-lookup"><span data-stu-id="9e7d8-254">JSON example: Copy data from FTP server to Azure Blob</span></span>
<span data-ttu-id="9e7d8-255">此範例示範如何將資料從 FTP 伺服器複製至 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-255">This sample shows how to copy data from an FTP server to Azure Blob storage.</span></span> <span data-ttu-id="9e7d8-256">不過，您可以使用資料處理站中的複製活動，把資料直接複製到 [支援的資料存放區及格式](data-factory-data-movement-activities.md#supported-data-stores-and-formats)一文中所述的任何接收器。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-256">However, data can be copied directly to any of the sinks stated in the [supported data stores and formats](data-factory-data-movement-activities.md#supported-data-stores-and-formats), by using the copy activity in Data Factory.</span></span>  

<span data-ttu-id="9e7d8-257">以下範例提供可用來使用 [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)、[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 或 [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md) 建立管線的範例 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-257">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span></span>

* <span data-ttu-id="9e7d8-258">[FtpServer](#linked-service-properties) 類型的連結服務</span><span class="sxs-lookup"><span data-stu-id="9e7d8-258">A linked service of type [FtpServer](#linked-service-properties)</span></span>
* <span data-ttu-id="9e7d8-259">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務</span><span class="sxs-lookup"><span data-stu-id="9e7d8-259">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="9e7d8-260">[FileShare](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="9e7d8-260">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties)</span></span>
* <span data-ttu-id="9e7d8-261">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="9e7d8-261">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="9e7d8-262">具有使用 [FileSystemSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)</span><span class="sxs-lookup"><span data-stu-id="9e7d8-262">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="9e7d8-263">範例會每隔一小時就把 FTP 伺服器的資料複製到 Azure Blob。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-263">The sample copies data from an FTP server to an Azure blob every hour.</span></span> <span data-ttu-id="9e7d8-264">範例後面的各節會說明這些範例中使用的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-264">The JSON properties used in these samples are described in sections following the samples.</span></span>

### <a name="ftp-linked-service"></a><span data-ttu-id="9e7d8-265">FTP 連結服務</span><span class="sxs-lookup"><span data-stu-id="9e7d8-265">FTP linked service</span></span>

<span data-ttu-id="9e7d8-266">此範例運用純文字使用者名稱和密碼來使用基本驗證。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-266">This example uses basic authentication, with the user name and password in plain text.</span></span> <span data-ttu-id="9e7d8-267">您也可以使用下列其中一種方式：</span><span class="sxs-lookup"><span data-stu-id="9e7d8-267">You can also use one of the following ways:</span></span>

* <span data-ttu-id="9e7d8-268">匿名驗證</span><span class="sxs-lookup"><span data-stu-id="9e7d8-268">Anonymous authentication</span></span>
* <span data-ttu-id="9e7d8-269">基本驗證與加密認證</span><span class="sxs-lookup"><span data-stu-id="9e7d8-269">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="9e7d8-270">透過 SSL/TLS 的 FTP (FTPS)</span><span class="sxs-lookup"><span data-stu-id="9e7d8-270">FTP over SSL/TLS (FTPS)</span></span>

<span data-ttu-id="9e7d8-271">請參閱 [FTP 連結服務](#linked-service-properties)一節，來了解您可以使用的不同驗證類型。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-271">See the [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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
### <a name="azure-storage-linked-service"></a><span data-ttu-id="9e7d8-272">Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="9e7d8-272">Azure Storage linked service</span></span>

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
### <a name="ftp-input-dataset"></a><span data-ttu-id="9e7d8-273">FTP 輸入資料集</span><span class="sxs-lookup"><span data-stu-id="9e7d8-273">FTP input dataset</span></span>

<span data-ttu-id="9e7d8-274">此資料及係指 FTP 資料夾 `mysharedfolder` 和 `test.csv` 檔案。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-274">This dataset refers to the FTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="9e7d8-275">管線會將檔案複製至目的地。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-275">The pipeline copies the file to the destination.</span></span>

<span data-ttu-id="9e7d8-276">設定 external 為 true 會通知資料處理站服務：這是資料處理站外部的資料集而且不是由資料處理站中的活動所產生。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-276">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory, and is not produced by an activity in the data factory.</span></span>

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

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="9e7d8-277">Azure Blob 輸出資料集</span><span class="sxs-lookup"><span data-stu-id="9e7d8-277">Azure Blob output dataset</span></span>

<span data-ttu-id="9e7d8-278">資料會每小時寫入至新的 Blob (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-278">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="9e7d8-279">根據正在處理之配量的開始時間，以動態方式評估 blob 的資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-279">The folder path for the blob is dynamically evaluated, based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="9e7d8-280">資料夾路徑會使用開始時間的年、月、日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-280">The folder path uses the year, month, day, and hours parts of the start time.</span></span>

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


### <a name="a-copy-activity-in-a-pipeline-with-file-system-source-and-blob-sink"></a><span data-ttu-id="9e7d8-281">具有檔案系統來源和 blob 接收器的管線中複製活動</span><span class="sxs-lookup"><span data-stu-id="9e7d8-281">A copy activity in a pipeline with file system source and blob sink</span></span>

<span data-ttu-id="9e7d8-282">此管線包含複製活動，該活動已設定為使用輸入和輸出資料集並排定為每小時執行。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-282">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="9e7d8-283">在管線 JSON 定義中，source 類型設為 FileSystemSource，而 sink 類型設為 BlobSink。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-283">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and the **sink** type is set to **BlobSink**.</span></span>

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
> <span data-ttu-id="9e7d8-284">若要將來源資料集中的資料行對應至接收資料集中的資料行，請參閱[在 Azure Data Factory 中對應資料集資料行](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-284">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e7d8-285">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9e7d8-285">Next steps</span></span>
<span data-ttu-id="9e7d8-286">請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="9e7d8-286">See the following articles:</span></span>

* <span data-ttu-id="9e7d8-287">若要了解影響 Data Factory 中資料移動 (複製活動) 效能的關鍵因素，以及各種最佳化的方法，請參閱[複製活動的效能及微調指南](data-factory-copy-activity-performance.md)。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-287">To learn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways to optimize it, see the [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="9e7d8-288">如需使用複製活動來建立管線的逐步指示，請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="9e7d8-288">For step-by-step instructions for creating a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
