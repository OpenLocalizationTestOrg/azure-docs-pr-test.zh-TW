---
title: "從 HTTP 來源移動資料 - Azure | Microsoft Docs"
description: "了解如何使用 Azure Data Factory 從內部部署或雲端 HTTP 來源移動資料。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 3cc1bd293868b0bb093f617ac12e16c26780fc89
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-an-http-source-using-azure-data-factory"></a><span data-ttu-id="054a8-103">使用 Azure Data Factory 來移動 HTTP 來源的資料</span><span class="sxs-lookup"><span data-stu-id="054a8-103">Move data from an HTTP source using Azure Data Factory</span></span>
<span data-ttu-id="054a8-104">本文概述如何使用 Azure Data Factory 中的複製活動，將內部部署/雲端 HTTP 端點中的資料移動到支援的接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="054a8-104">This article outlines how to use the Copy Activity in Azure Data Factory to move data from an on-premises/cloud HTTP endpoint to a supported sink data store.</span></span> <span data-ttu-id="054a8-105">本文是根據 [資料移動活動](data-factory-data-movement-activities.md)一文，該文呈現使用複製活動移動資料的一般概觀以及支援作為來源/接收的資料存放區清單。</span><span class="sxs-lookup"><span data-stu-id="054a8-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and the list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="054a8-106">Data factory 目前只支援把 HTTP 來源的資料移動到其他資料存放區，但不支援把其他資料存放區的資料移動到 HTTP 目的地。</span><span class="sxs-lookup"><span data-stu-id="054a8-106">Data factory currently supports only moving data from an HTTP source to other data stores, but not moving data from other data stores to an HTTP destination.</span></span>

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="054a8-107">支援的案例和驗證類型</span><span class="sxs-lookup"><span data-stu-id="054a8-107">Supported scenarios and authentication types</span></span>
<span data-ttu-id="054a8-108">您可以使用這個 HTTP 連接器，藉由使用 HTTP **GET**或 **POST** 方法，從**雲端和內部部署 HTTP/s 端點擷取資料**。</span><span class="sxs-lookup"><span data-stu-id="054a8-108">You can use this HTTP connector to retrieve data from **both cloud and on-premises HTTP/s endpoint** by using HTTP **GET** or **POST** method.</span></span> <span data-ttu-id="054a8-109">支援下列驗證類型︰**匿名****基本**、**摘要**、**Windows**和 **ClientCertificate**。</span><span class="sxs-lookup"><span data-stu-id="054a8-109">The following authentication types are supported: **Anonymous**, **Basic**, **Digest**, **Windows**, and **ClientCertificate**.</span></span> <span data-ttu-id="054a8-110">請注意，此連接器和 [Web 資料表連接器](data-factory-web-table-connector.md)的差異是︰後者是用來擷取 HTML 網頁上的資料表內容。</span><span class="sxs-lookup"><span data-stu-id="054a8-110">Note the difference between this connector and the [Web table connector](data-factory-web-table-connector.md) is: the latter is used to extract table content from web HTML page.</span></span>

<span data-ttu-id="054a8-111">從內部部署 HTTP 端點複製資料時，您需要在內部部署環境/Azure VM 中安裝資料管理閘道。</span><span class="sxs-lookup"><span data-stu-id="054a8-111">When copying data from an on-premises HTTP endpoint, you need install a Data Management Gateway in the on-premises environment/Azure VM.</span></span> <span data-ttu-id="054a8-112">請參閱 [在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文來了解資料管理閘道和設定閘道的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="054a8-112">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="054a8-113">開始使用</span><span class="sxs-lookup"><span data-stu-id="054a8-113">Getting started</span></span>
<span data-ttu-id="054a8-114">您可以建立內含複製活動的管線，使用不同的工具/API 將資料移出 HTTP 來源。</span><span class="sxs-lookup"><span data-stu-id="054a8-114">You can create a pipeline with a copy activity that moves data from an HTTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="054a8-115">若要建立管線，最簡單的方式就是使用**複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="054a8-115">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="054a8-116">如需使用複製資料精靈建立管線的快速逐步解說，請參閱 [教學課程︰使用複製精靈建立管線](data-factory-copy-data-wizard-tutorial.md) 。</span><span class="sxs-lookup"><span data-stu-id="054a8-116">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

- <span data-ttu-id="054a8-117">您也可以使用下列工具來建立管線︰**Azure 入口網站**、**Visual Studio**、**Azure PowerShell**、**Azure Resource Manager 範本**、**.NET API** 及 **REST API**。</span><span class="sxs-lookup"><span data-stu-id="054a8-117">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="054a8-118">如需建立內含複製活動之管線的逐步指示，請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="054a8-118">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> <span data-ttu-id="054a8-119">若要將資料從 HTTP 來源複製到 Azure Blob 儲存體的 JSON 範例，請參閱本文的 [JSON 範例](#json-examples)一節。</span><span class="sxs-lookup"><span data-stu-id="054a8-119">For JSON samples to copy data from HTTP source to Azure Blob Storage, see [JSON examples](#json-examples) section of this articles.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="054a8-120">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="054a8-120">Linked service properties</span></span>
<span data-ttu-id="054a8-121">下表提供 HTTP 連結服務專屬 JSON 元素的說明。</span><span class="sxs-lookup"><span data-stu-id="054a8-121">The following table provides description for JSON elements specific to HTTP linked service.</span></span>

| <span data-ttu-id="054a8-122">屬性</span><span class="sxs-lookup"><span data-stu-id="054a8-122">Property</span></span> | <span data-ttu-id="054a8-123">說明</span><span class="sxs-lookup"><span data-stu-id="054a8-123">Description</span></span> | <span data-ttu-id="054a8-124">必要</span><span class="sxs-lookup"><span data-stu-id="054a8-124">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="054a8-125">類型</span><span class="sxs-lookup"><span data-stu-id="054a8-125">type</span></span> | <span data-ttu-id="054a8-126">類型屬性必須設為：`Http`。</span><span class="sxs-lookup"><span data-stu-id="054a8-126">The type property must be set to: `Http`.</span></span> | <span data-ttu-id="054a8-127">是</span><span class="sxs-lookup"><span data-stu-id="054a8-127">Yes</span></span> |
| <span data-ttu-id="054a8-128">url</span><span class="sxs-lookup"><span data-stu-id="054a8-128">url</span></span> | <span data-ttu-id="054a8-129">Web 伺服器的基本 URL</span><span class="sxs-lookup"><span data-stu-id="054a8-129">Base URL to the Web Server</span></span> | <span data-ttu-id="054a8-130">是</span><span class="sxs-lookup"><span data-stu-id="054a8-130">Yes</span></span> |
| <span data-ttu-id="054a8-131">authenticationType</span><span class="sxs-lookup"><span data-stu-id="054a8-131">authenticationType</span></span> | <span data-ttu-id="054a8-132">指定驗證類型。</span><span class="sxs-lookup"><span data-stu-id="054a8-132">Specifies the authentication type.</span></span> <span data-ttu-id="054a8-133">允許的值為︰**匿名**、**基本**、**摘要**、**Windows**、**ClientCertificate**。</span><span class="sxs-lookup"><span data-stu-id="054a8-133">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="054a8-134">請分別參閱此關於更多屬性的下列資料表各節以及這些驗證類型的 JSON 範例。</span><span class="sxs-lookup"><span data-stu-id="054a8-134">Refer to sections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="054a8-135">是</span><span class="sxs-lookup"><span data-stu-id="054a8-135">Yes</span></span> |
| <span data-ttu-id="054a8-136">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="054a8-136">enableServerCertificateValidation</span></span> | <span data-ttu-id="054a8-137">如果來源是 HTTPS Web 伺服器，指定是否啟用伺服器 SSL 憑證驗證</span><span class="sxs-lookup"><span data-stu-id="054a8-137">Specify whether to enable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="054a8-138">否，預設值是 True</span><span class="sxs-lookup"><span data-stu-id="054a8-138">No, default is true</span></span> |
| <span data-ttu-id="054a8-139">gatewayName</span><span class="sxs-lookup"><span data-stu-id="054a8-139">gatewayName</span></span> | <span data-ttu-id="054a8-140">連接至內部部署 HTTP 來源的「資料管理閘道」閘道。</span><span class="sxs-lookup"><span data-stu-id="054a8-140">Name of the Data Management Gateway to connect to an on-premises HTTP source.</span></span> | <span data-ttu-id="054a8-141">如果從內部部署 HTTP 來源複製資料，則為是。</span><span class="sxs-lookup"><span data-stu-id="054a8-141">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="054a8-142">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="054a8-142">encryptedCredential</span></span> | <span data-ttu-id="054a8-143">用來存取 HTTP 端點的加密認證。</span><span class="sxs-lookup"><span data-stu-id="054a8-143">Encrypted credential to access the HTTP endpoint.</span></span> <span data-ttu-id="054a8-144">當您在複製精靈或 ClickOnce 快顯對話方塊中設定驗證資訊時會自動產生。</span><span class="sxs-lookup"><span data-stu-id="054a8-144">Auto-generated when you configure the authentication information in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="054a8-145">否。</span><span class="sxs-lookup"><span data-stu-id="054a8-145">No.</span></span> <span data-ttu-id="054a8-146">僅當從內部部署 HTTP 伺服器複製資料時才套用。</span><span class="sxs-lookup"><span data-stu-id="054a8-146">Apply only when copying data from an on-premises HTTP server.</span></span> |

<span data-ttu-id="054a8-147">如需設定內部部署 HTTP 連接器資料來源認證的詳細資訊，請參閱[利用資料管理閘道在內部部署來源和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)。</span><span class="sxs-lookup"><span data-stu-id="054a8-147">See [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for details about setting credentials for on-premises HTTP connector data source.</span></span>

### <a name="using-basic-digest-or-windows-authentication"></a><span data-ttu-id="054a8-148">使用基本、摘要或 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="054a8-148">Using Basic, Digest, or Windows authentication</span></span>

<span data-ttu-id="054a8-149">將 `authenticationType` 設定為 `Basic`、`Digest`或 `Windows`，並指定除了上面介紹的 HTTP 連接器泛用的下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="054a8-149">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="054a8-150">屬性</span><span class="sxs-lookup"><span data-stu-id="054a8-150">Property</span></span> | <span data-ttu-id="054a8-151">說明</span><span class="sxs-lookup"><span data-stu-id="054a8-151">Description</span></span> | <span data-ttu-id="054a8-152">必要</span><span class="sxs-lookup"><span data-stu-id="054a8-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="054a8-153">username</span><span class="sxs-lookup"><span data-stu-id="054a8-153">username</span></span> | <span data-ttu-id="054a8-154">存取 HTTP 端點的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="054a8-154">Username to access the HTTP endpoint.</span></span> | <span data-ttu-id="054a8-155">是</span><span class="sxs-lookup"><span data-stu-id="054a8-155">Yes</span></span> |
| <span data-ttu-id="054a8-156">password</span><span class="sxs-lookup"><span data-stu-id="054a8-156">password</span></span> | <span data-ttu-id="054a8-157">使用者 (使用者名稱) 的密碼。</span><span class="sxs-lookup"><span data-stu-id="054a8-157">Password for the user (username).</span></span> | <span data-ttu-id="054a8-158">是</span><span class="sxs-lookup"><span data-stu-id="054a8-158">Yes</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="054a8-159">範例︰使用基本、摘要或 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="054a8-159">Example: using Basic, Digest, or Windows authentication</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "basic",
            "url" : "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

### <a name="using-clientcertificate-authentication"></a><span data-ttu-id="054a8-160">使用 ClientCertificate 驗證</span><span class="sxs-lookup"><span data-stu-id="054a8-160">Using ClientCertificate authentication</span></span>

<span data-ttu-id="054a8-161">若要使用基本驗證，將 `authenticationType` 設定為 `ClientCertificate`，並指定除了上面介紹的 HTTP 連接器泛用的下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="054a8-161">To use basic authentication, set `authenticationType` as `ClientCertificate`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="054a8-162">屬性</span><span class="sxs-lookup"><span data-stu-id="054a8-162">Property</span></span> | <span data-ttu-id="054a8-163">說明</span><span class="sxs-lookup"><span data-stu-id="054a8-163">Description</span></span> | <span data-ttu-id="054a8-164">必要</span><span class="sxs-lookup"><span data-stu-id="054a8-164">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="054a8-165">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="054a8-165">embeddedCertData</span></span> | <span data-ttu-id="054a8-166">Base 64 編碼的個人資訊交換 (PFX) 檔案之二進位資料內容。</span><span class="sxs-lookup"><span data-stu-id="054a8-166">The Base64-encoded contents of binary data of the Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="054a8-167">指定 `embeddedCertData` 或 `certThumbprint`。</span><span class="sxs-lookup"><span data-stu-id="054a8-167">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="054a8-168">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="054a8-168">certThumbprint</span></span> | <span data-ttu-id="054a8-169">憑證指紋已安裝在您閘道器電腦的憑證存放區上。</span><span class="sxs-lookup"><span data-stu-id="054a8-169">The thumbprint of the certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="054a8-170">僅當從內部部署 HTTP 來源複製資料時才套用。</span><span class="sxs-lookup"><span data-stu-id="054a8-170">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="054a8-171">指定 `embeddedCertData` 或 `certThumbprint`。</span><span class="sxs-lookup"><span data-stu-id="054a8-171">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="054a8-172">password</span><span class="sxs-lookup"><span data-stu-id="054a8-172">password</span></span> | <span data-ttu-id="054a8-173">與憑證相關聯的密碼。</span><span class="sxs-lookup"><span data-stu-id="054a8-173">Password associated with the certificate.</span></span> | <span data-ttu-id="054a8-174">否</span><span class="sxs-lookup"><span data-stu-id="054a8-174">No</span></span> |

<span data-ttu-id="054a8-175">如果您使用 `certThumbprint` 進行驗證且憑證已安裝在本機電腦的個人存放區中，您必須授與讀取權限給閘道器服務︰</span><span class="sxs-lookup"><span data-stu-id="054a8-175">If you use `certThumbprint` for authentication and the certificate is installed in the personal store of the local computer, you need to grant the read permission to the gateway service:</span></span>

1. <span data-ttu-id="054a8-176">啟動 Microsoft Management Console (MMC)。</span><span class="sxs-lookup"><span data-stu-id="054a8-176">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="054a8-177">新增目標為 [本機電腦] 的 [憑證] 嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="054a8-177">Add the **Certificates** snap-in that targets the **Local Computer**.</span></span>
2. <span data-ttu-id="054a8-178">展開 [憑證]，[個人]，然後按一下 [憑證]。</span><span class="sxs-lookup"><span data-stu-id="054a8-178">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="054a8-179">以滑鼠右鍵按一下個人存放區中的 [憑證]，然後選取 [所有工作]->[管理私用金鑰...]</span><span class="sxs-lookup"><span data-stu-id="054a8-179">Right-click the certificate from the personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="054a8-180">在 [安全性] 索引標籤上，新增資料管理閘道主機服務使用憑證讀取存取執行所在的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="054a8-180">On the **Security** tab, add the user account under which Data Management Gateway Host Service is running with the read access to the certificate.</span></span>  

#### <a name="example-using-client-certificate"></a><span data-ttu-id="054a8-181">範例︰使用用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="054a8-181">Example: using client certificate</span></span>
<span data-ttu-id="054a8-182">此連結服務會將您的資料處理站與內部部署 HTTP web 伺服器連結。</span><span class="sxs-lookup"><span data-stu-id="054a8-182">This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="054a8-183">它會使用已安裝資料管理閘道的電腦上所安裝的用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="054a8-183">It uses a client certificate that is installed on the machine with Data Management Gateway installed.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"

        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="054a8-184">範例︰在檔案中使用用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="054a8-184">Example: using client certificate in a file</span></span>
<span data-ttu-id="054a8-185">此連結服務會將您的資料處理站與內部部署 HTTP web 伺服器連結。</span><span class="sxs-lookup"><span data-stu-id="054a8-185">This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="054a8-186">它會使用已安裝資料管理閘道的電腦上的用戶端憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="054a8-186">It uses a client certificate file on the machine with Data Management Gateway installed.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="054a8-187">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="054a8-187">Dataset properties</span></span>
<span data-ttu-id="054a8-188">如需定義資料集的區段和屬性完整清單，請參閱[建立資料集](data-factory-create-datasets.md)一文。</span><span class="sxs-lookup"><span data-stu-id="054a8-188">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="054a8-189">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="054a8-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="054a8-190">每個資料集類型的 **typeProperties** 區段都不同，可提供資料存放區中的資料位置資訊。</span><span class="sxs-lookup"><span data-stu-id="054a8-190">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="054a8-191">**Http** 類型資料集的 typeProperties 區段具有下列屬性</span><span class="sxs-lookup"><span data-stu-id="054a8-191">The typeProperties section for dataset of type **Http** has the following properties</span></span>

| <span data-ttu-id="054a8-192">屬性</span><span class="sxs-lookup"><span data-stu-id="054a8-192">Property</span></span> | <span data-ttu-id="054a8-193">說明</span><span class="sxs-lookup"><span data-stu-id="054a8-193">Description</span></span> | <span data-ttu-id="054a8-194">必要</span><span class="sxs-lookup"><span data-stu-id="054a8-194">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="054a8-195">類型</span><span class="sxs-lookup"><span data-stu-id="054a8-195">type</span></span> | <span data-ttu-id="054a8-196">指定資料集的類型。</span><span class="sxs-lookup"><span data-stu-id="054a8-196">Specified the type of the dataset.</span></span> <span data-ttu-id="054a8-197">必須設為 `Http`。</span><span class="sxs-lookup"><span data-stu-id="054a8-197">must be set to `Http`.</span></span> | <span data-ttu-id="054a8-198">是</span><span class="sxs-lookup"><span data-stu-id="054a8-198">Yes</span></span> |
| <span data-ttu-id="054a8-199">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="054a8-199">relativeUrl</span></span> | <span data-ttu-id="054a8-200">包含資料之資源的相對 URL。</span><span class="sxs-lookup"><span data-stu-id="054a8-200">A relative URL to the resource that contains the data.</span></span> <span data-ttu-id="054a8-201">當路徑未指定時，則只會使用在連結服務定義中指定的 URL。</span><span class="sxs-lookup"><span data-stu-id="054a8-201">When path is not specified, only the URL specified in the linked service definition is used.</span></span> <br><br> <span data-ttu-id="054a8-202">若要建構動態 URL，您可以使用[Data Factory 函式與系統變數](data-factory-functions-variables.md)，例如 "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"。</span><span class="sxs-lookup"><span data-stu-id="054a8-202">To construct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), e.g. "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)".</span></span> | <span data-ttu-id="054a8-203">否</span><span class="sxs-lookup"><span data-stu-id="054a8-203">No</span></span> |
| <span data-ttu-id="054a8-204">requestMethod</span><span class="sxs-lookup"><span data-stu-id="054a8-204">requestMethod</span></span> | <span data-ttu-id="054a8-205">HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="054a8-205">Http method.</span></span> <span data-ttu-id="054a8-206">允許的值為 **GET** 或 **POST**。</span><span class="sxs-lookup"><span data-stu-id="054a8-206">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="054a8-207">否。</span><span class="sxs-lookup"><span data-stu-id="054a8-207">No.</span></span> <span data-ttu-id="054a8-208">預設值為 `GET`。</span><span class="sxs-lookup"><span data-stu-id="054a8-208">Default is `GET`.</span></span> |
| <span data-ttu-id="054a8-209">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="054a8-209">additionalHeaders</span></span> | <span data-ttu-id="054a8-210">其他 HTTP 要求標頭。</span><span class="sxs-lookup"><span data-stu-id="054a8-210">Additional HTTP request headers.</span></span> | <span data-ttu-id="054a8-211">否</span><span class="sxs-lookup"><span data-stu-id="054a8-211">No</span></span> |
| <span data-ttu-id="054a8-212">requestBody</span><span class="sxs-lookup"><span data-stu-id="054a8-212">requestBody</span></span> | <span data-ttu-id="054a8-213">HTTP 要求的內文。</span><span class="sxs-lookup"><span data-stu-id="054a8-213">Body for HTTP request.</span></span> | <span data-ttu-id="054a8-214">否</span><span class="sxs-lookup"><span data-stu-id="054a8-214">No</span></span> |
| <span data-ttu-id="054a8-215">format</span><span class="sxs-lookup"><span data-stu-id="054a8-215">format</span></span> | <span data-ttu-id="054a8-216">如果您只想要**從 HTTP 端點依現狀擷取資料**而不剖析它，請略過此格式設定。</span><span class="sxs-lookup"><span data-stu-id="054a8-216">If you want to simply **retrieve the data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="054a8-217">如果您想要在複製期間剖析 HTTP 回應內容，支援下列格式類型：**TextFormat**、**JsonFormat**、**AvroFormat**、**OrcFormat**、**ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="054a8-217">If you want to parse the HTTP response content during copy, the following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="054a8-218">如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。</span><span class="sxs-lookup"><span data-stu-id="054a8-218">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="054a8-219">否</span><span class="sxs-lookup"><span data-stu-id="054a8-219">No</span></span> |
| <span data-ttu-id="054a8-220">compression</span><span class="sxs-lookup"><span data-stu-id="054a8-220">compression</span></span> | <span data-ttu-id="054a8-221">指定此資料的壓縮類型和層級。</span><span class="sxs-lookup"><span data-stu-id="054a8-221">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="054a8-222">支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。</span><span class="sxs-lookup"><span data-stu-id="054a8-222">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="054a8-223">支援的層級為：**Optimal** 和 **Fastest**。</span><span class="sxs-lookup"><span data-stu-id="054a8-223">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="054a8-224">如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。</span><span class="sxs-lookup"><span data-stu-id="054a8-224">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="054a8-225">否</span><span class="sxs-lookup"><span data-stu-id="054a8-225">No</span></span> |

### <a name="example-using-the-get-default-method"></a><span data-ttu-id="054a8-226">範例︰使用 GET (預設值) 方法</span><span class="sxs-lookup"><span data-stu-id="054a8-226">Example: using the GET (default) method</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

### <a name="example-using-the-post-method"></a><span data-ttu-id="054a8-227">範例︰使用 POST 方法</span><span class="sxs-lookup"><span data-stu-id="054a8-227">Example: using the POST method</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
           "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="054a8-228">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="054a8-228">Copy activity properties</span></span>
<span data-ttu-id="054a8-229">如需定義活動的區段和屬性完整清單，請參閱[建立管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="054a8-229">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="054a8-230">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="054a8-230">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="054a8-231">另一方面，活動的 **typeProperties** 區段中可用的屬性會隨著每個活動類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="054a8-231">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="054a8-232">就「複製活動」而言，這些屬性會根據來源和接收器的類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="054a8-232">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="054a8-233">目前，當複製活動中的來源類型為 **HttpSource** 時，支援下列屬性。</span><span class="sxs-lookup"><span data-stu-id="054a8-233">Currently, when the source in copy activity is of type **HttpSource**, the following properties are supported.</span></span>

| <span data-ttu-id="054a8-234">屬性</span><span class="sxs-lookup"><span data-stu-id="054a8-234">Property</span></span> | <span data-ttu-id="054a8-235">說明</span><span class="sxs-lookup"><span data-stu-id="054a8-235">Description</span></span> | <span data-ttu-id="054a8-236">必要</span><span class="sxs-lookup"><span data-stu-id="054a8-236">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="054a8-237">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="054a8-237">httpRequestTimeout</span></span> | <span data-ttu-id="054a8-238">HTTP 的逾時 (TimeSpan) 要求取得回應。</span><span class="sxs-lookup"><span data-stu-id="054a8-238">The timeout (TimeSpan) for the HTTP request to get a response.</span></span> <span data-ttu-id="054a8-239">逾時會取得回應，而非逾時讀取回應資料。</span><span class="sxs-lookup"><span data-stu-id="054a8-239">It is the timeout to get a response, not the timeout to read response data.</span></span> | <span data-ttu-id="054a8-240">否。</span><span class="sxs-lookup"><span data-stu-id="054a8-240">No.</span></span> <span data-ttu-id="054a8-241">預設值：00:01:40</span><span class="sxs-lookup"><span data-stu-id="054a8-241">Default value: 00:01:40</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="054a8-242">支援的檔案和壓縮格式</span><span class="sxs-lookup"><span data-stu-id="054a8-242">Supported file and compression formats</span></span>
<span data-ttu-id="054a8-243">請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md)文章以了解詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="054a8-243">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="054a8-244">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="054a8-244">JSON examples</span></span>
<span data-ttu-id="054a8-245">下列範例提供您使用 [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)、[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 或 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md) 來建立管線時，可使用的範例 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="054a8-245">The following example provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="054a8-246">這些範例示範如何將資料從 HTTP 來源複製到 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="054a8-246">They show how to copy data from HTTP source to Azure Blob Storage.</span></span> <span data-ttu-id="054a8-247">不過，您可以在 Azure Data Factory 中使用複製活動，從任何來源 **直接** 將資料複製到 [這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 所說的任何接收器。</span><span class="sxs-lookup"><span data-stu-id="054a8-247">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-http-source-to-azure-blob-storage"></a><span data-ttu-id="054a8-248">範例：將資料從 HTTP 來源複製到 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="054a8-248">Example: Copy data from HTTP source to Azure Blob Storage</span></span>
<span data-ttu-id="054a8-249">此範例的 Data Factory 方案包含下列資料處理站實體︰</span><span class="sxs-lookup"><span data-stu-id="054a8-249">The Data Factory solution for this sample contains the following Data Factory entities:</span></span>

1. <span data-ttu-id="054a8-250">一個 [HTTP](#linked-service-properties) 類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="054a8-250">A linked service of type [HTTP](#linked-service-properties).</span></span>
2. <span data-ttu-id="054a8-251">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="054a8-251">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="054a8-252">[Http](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="054a8-252">An input [dataset](data-factory-create-datasets.md) of type [Http](#dataset-properties).</span></span>
4. <span data-ttu-id="054a8-253">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="054a8-253">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="054a8-254">具有使用 [HttpSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="054a8-254">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [HttpSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="054a8-255">範例會每隔一小時就把 HTTP 來源的資料複製到 Azure Blob。</span><span class="sxs-lookup"><span data-stu-id="054a8-255">The sample copies data from an HTTP source to an Azure blob every hour.</span></span> <span data-ttu-id="054a8-256">範例後面的各節會說明這些範例中使用的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="054a8-256">The JSON properties used in these samples are described in sections following the samples.</span></span>

### <a name="http-linked-service"></a><span data-ttu-id="054a8-257">HTTP 連結服務</span><span class="sxs-lookup"><span data-stu-id="054a8-257">HTTP linked service</span></span>
<span data-ttu-id="054a8-258">此範例會使用匿名驗證來使用 HTTP 連結服務。</span><span class="sxs-lookup"><span data-stu-id="054a8-258">This example uses the HTTP linked service with anonymous authentication.</span></span> <span data-ttu-id="054a8-259">請參閱 [HTTP 連結服務](#linked-service-properties)一節，來了解您可以使用的不同驗證類型。</span><span class="sxs-lookup"><span data-stu-id="054a8-259">See [HTTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="054a8-260">Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="054a8-260">Azure Storage linked service</span></span>

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

### <a name="http-input-dataset"></a><span data-ttu-id="054a8-261">HTTP 輸入資料集</span><span class="sxs-lookup"><span data-stu-id="054a8-261">HTTP input dataset</span></span>
<span data-ttu-id="054a8-262">將 **external** 設定為 **true** 會通知 Data Factory 服務：這是 Data Factory 外部的資料集而且不是由 Data Factory 中的活動所產生。</span><span class="sxs-lookup"><span data-stu-id="054a8-262">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}

```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="054a8-263">Azure Blob 輸出資料集</span><span class="sxs-lookup"><span data-stu-id="054a8-263">Azure Blob output dataset</span></span>

<span data-ttu-id="054a8-264">資料會每小時寫入至新的 Blob (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="054a8-264">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="054a8-265">具有複製活動的管線</span><span class="sxs-lookup"><span data-stu-id="054a8-265">Pipeline with Copy activity</span></span>

<span data-ttu-id="054a8-266">此管線包含複製活動，該活動已設定為使用輸入和輸出資料集並排定為每小時執行。</span><span class="sxs-lookup"><span data-stu-id="054a8-266">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="054a8-267">在管線 JSON 定義中，**source** 類型設為 **HttpSource**，而 **sink** 類型設為 **BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="054a8-267">In the pipeline JSON definition, the **source** type is set to **HttpSource** and **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="054a8-268">請參閱 [HttpSource](#copy-activity-properties) 以取得 HttpSource 支援的屬性清單。</span><span class="sxs-lookup"><span data-stu-id="054a8-268">See [HttpSource](#copy-activity-properties) for the list of properties supported by the HttpSource.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "HttpSourceToAzureBlob",
        "description": "Copy from an HTTP source to an Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "HttpSourceDataInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "HttpSource"
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
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```

> [!NOTE]
> <span data-ttu-id="054a8-269">若要將來源資料集中的資料行對應至接收資料集中的資料行，請參閱[在 Azure Data Factory 中對應資料集資料行](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="054a8-269">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="054a8-270">效能和微調</span><span class="sxs-lookup"><span data-stu-id="054a8-270">Performance and Tuning</span></span>
<span data-ttu-id="054a8-271">請參閱[複製活動的效能及微調指南](data-factory-copy-activity-performance.md)一文，以了解在 Azure Data Factory 中會影響資料移動 (複製活動) 效能的重要因素，以及各種最佳化的方法。</span><span class="sxs-lookup"><span data-stu-id="054a8-271">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
