---
title: "從 HTTP 來源-Azure aaaMove 資料 |Microsoft 文件"
description: "深入了解如何從內部部署或雲端 HTTP toomove 資料來源使用 Azure Data Factory。"
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
ms.openlocfilehash: e39b9cbff870aef4be91938cacff39a2fd12d64a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-http-source-using-azure-data-factory"></a><span data-ttu-id="7902e-103">使用 Azure Data Factory 來移動 HTTP 來源的資料</span><span class="sxs-lookup"><span data-stu-id="7902e-103">Move data from an HTTP source using Azure Data Factory</span></span>
<span data-ttu-id="7902e-104">本文概述如何在 Azure Data Factory toomove 資料從雲端上的內部部署/HTTP 端點 tooa toouse hello 複製活動支援接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="7902e-104">This article outlines how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises/cloud HTTP endpoint tooa supported sink data store.</span></span> <span data-ttu-id="7902e-105">這篇文章是根據 hello[資料移動活動](data-factory-data-movement-activities.md)呈現資料移動的一般概觀，以及複製活動與 hello 清單做為來源/接收器所支援的資料存放區的發行項。</span><span class="sxs-lookup"><span data-stu-id="7902e-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and hello list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="7902e-106">資料處理站目前支援僅將資料從 HTTP 來源 tooother 資料存放區，但不是將資料從其他資料會儲存 tooan HTTP 目的地。</span><span class="sxs-lookup"><span data-stu-id="7902e-106">Data factory currently supports only moving data from an HTTP source tooother data stores, but not moving data from other data stores tooan HTTP destination.</span></span>

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="7902e-107">支援的案例和驗證類型</span><span class="sxs-lookup"><span data-stu-id="7902e-107">Supported scenarios and authentication types</span></span>
<span data-ttu-id="7902e-108">您可以使用此 HTTP 連接器 tooretrieve 資料從**雲端和內部部署的 HTTP/s 端點**使用 HTTP**取得**或**POST**方法。</span><span class="sxs-lookup"><span data-stu-id="7902e-108">You can use this HTTP connector tooretrieve data from **both cloud and on-premises HTTP/s endpoint** by using HTTP **GET** or **POST** method.</span></span> <span data-ttu-id="7902e-109">支援下列驗證類型的 hello:**匿名**，**基本**，**摘要**， **Windows**，和**ClientCertificate**。</span><span class="sxs-lookup"><span data-stu-id="7902e-109">hello following authentication types are supported: **Anonymous**, **Basic**, **Digest**, **Windows**, and **ClientCertificate**.</span></span> <span data-ttu-id="7902e-110">請注意這個連接器與 hello 的 hello 時差[Web 資料表連接器](data-factory-web-table-connector.md)是： hello 第二種是使用的 tooextract 資料表 HTML 網頁的內容。</span><span class="sxs-lookup"><span data-stu-id="7902e-110">Note hello difference between this connector and hello [Web table connector](data-factory-web-table-connector.md) is: hello latter is used tooextract table content from web HTML page.</span></span>

<span data-ttu-id="7902e-111">複製資料時從內部 HTTP 端點，您需要在 hello 在內部部署環境/Azure VM 中安裝資料管理閘道器。</span><span class="sxs-lookup"><span data-stu-id="7902e-111">When copying data from an on-premises HTTP endpoint, you need install a Data Management Gateway in hello on-premises environment/Azure VM.</span></span> <span data-ttu-id="7902e-112">請參閱[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)文章 toolearn 有關資料管理閘道器和 hello 閘道設定的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="7902e-112">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="7902e-113">開始使用</span><span class="sxs-lookup"><span data-stu-id="7902e-113">Getting started</span></span>
<span data-ttu-id="7902e-114">您可以建立內含複製活動的管線，使用不同的工具/API 將資料移出 HTTP 來源。</span><span class="sxs-lookup"><span data-stu-id="7902e-114">You can create a pipeline with a copy activity that moves data from an HTTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="7902e-115">最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="7902e-115">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="7902e-116">請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。</span><span class="sxs-lookup"><span data-stu-id="7902e-116">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

- <span data-ttu-id="7902e-117">您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。</span><span class="sxs-lookup"><span data-stu-id="7902e-117">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="7902e-118">請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="7902e-118">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> <span data-ttu-id="7902e-119">如 JSON 範例 toocopy HTTP 來源 tooAzure Blob 儲存體的資料，請參閱 < [JSON 範例](#json-examples)此文件的區段。</span><span class="sxs-lookup"><span data-stu-id="7902e-119">For JSON samples toocopy data from HTTP source tooAzure Blob Storage, see [JSON examples](#json-examples) section of this articles.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="7902e-120">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="7902e-120">Linked service properties</span></span>
<span data-ttu-id="7902e-121">下表中的 hello 提供 JSON 項目特定 tooHTTP 連結服務的描述。</span><span class="sxs-lookup"><span data-stu-id="7902e-121">hello following table provides description for JSON elements specific tooHTTP linked service.</span></span>

| <span data-ttu-id="7902e-122">屬性</span><span class="sxs-lookup"><span data-stu-id="7902e-122">Property</span></span> | <span data-ttu-id="7902e-123">說明</span><span class="sxs-lookup"><span data-stu-id="7902e-123">Description</span></span> | <span data-ttu-id="7902e-124">必要</span><span class="sxs-lookup"><span data-stu-id="7902e-124">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7902e-125">類型</span><span class="sxs-lookup"><span data-stu-id="7902e-125">type</span></span> | <span data-ttu-id="7902e-126">hello 類型屬性必須設定為： `Http`。</span><span class="sxs-lookup"><span data-stu-id="7902e-126">hello type property must be set to: `Http`.</span></span> | <span data-ttu-id="7902e-127">是</span><span class="sxs-lookup"><span data-stu-id="7902e-127">Yes</span></span> |
| <span data-ttu-id="7902e-128">url</span><span class="sxs-lookup"><span data-stu-id="7902e-128">url</span></span> | <span data-ttu-id="7902e-129">基底 URL toohello Web 伺服器</span><span class="sxs-lookup"><span data-stu-id="7902e-129">Base URL toohello Web Server</span></span> | <span data-ttu-id="7902e-130">是</span><span class="sxs-lookup"><span data-stu-id="7902e-130">Yes</span></span> |
| <span data-ttu-id="7902e-131">authenticationType</span><span class="sxs-lookup"><span data-stu-id="7902e-131">authenticationType</span></span> | <span data-ttu-id="7902e-132">指定 hello 驗證類型。</span><span class="sxs-lookup"><span data-stu-id="7902e-132">Specifies hello authentication type.</span></span> <span data-ttu-id="7902e-133">允許的值為︰**匿名**、**基本**、**摘要**、**Windows**、**ClientCertificate**。</span><span class="sxs-lookup"><span data-stu-id="7902e-133">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="7902e-134">請參閱 「 toosections 上多個屬性和 JSON 範例此表格下方的驗證類型分別。</span><span class="sxs-lookup"><span data-stu-id="7902e-134">Refer toosections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="7902e-135">是</span><span class="sxs-lookup"><span data-stu-id="7902e-135">Yes</span></span> |
| <span data-ttu-id="7902e-136">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="7902e-136">enableServerCertificateValidation</span></span> | <span data-ttu-id="7902e-137">指定是否 tooenable 伺服器 SSL 憑證驗證，是否來源是 HTTPS 的網頁伺服器</span><span class="sxs-lookup"><span data-stu-id="7902e-137">Specify whether tooenable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="7902e-138">否，預設值是 True</span><span class="sxs-lookup"><span data-stu-id="7902e-138">No, default is true</span></span> |
| <span data-ttu-id="7902e-139">gatewayName</span><span class="sxs-lookup"><span data-stu-id="7902e-139">gatewayName</span></span> | <span data-ttu-id="7902e-140">名稱的 hello 資料管理閘道器 tooconnect tooan 內部 HTTP 的來源。</span><span class="sxs-lookup"><span data-stu-id="7902e-140">Name of hello Data Management Gateway tooconnect tooan on-premises HTTP source.</span></span> | <span data-ttu-id="7902e-141">如果從內部部署 HTTP 來源複製資料，則為是。</span><span class="sxs-lookup"><span data-stu-id="7902e-141">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="7902e-142">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="7902e-142">encryptedCredential</span></span> | <span data-ttu-id="7902e-143">加密的認證 tooaccess hello HTTP 端點。</span><span class="sxs-lookup"><span data-stu-id="7902e-143">Encrypted credential tooaccess hello HTTP endpoint.</span></span> <span data-ttu-id="7902e-144">自動產生複製精靈] 或 [hello ClickOnce 快顯對話方塊以設定 hello 驗證資訊。</span><span class="sxs-lookup"><span data-stu-id="7902e-144">Auto-generated when you configure hello authentication information in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="7902e-145">否。</span><span class="sxs-lookup"><span data-stu-id="7902e-145">No.</span></span> <span data-ttu-id="7902e-146">僅當從內部部署 HTTP 伺服器複製資料時才套用。</span><span class="sxs-lookup"><span data-stu-id="7902e-146">Apply only when copying data from an on-premises HTTP server.</span></span> |

<span data-ttu-id="7902e-147">請參閱[在內部部署來源和資料管理閘道與 hello 雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)詳細資料設定為內部 HTTP 連接器資料來源的認證。</span><span class="sxs-lookup"><span data-stu-id="7902e-147">See [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for details about setting credentials for on-premises HTTP connector data source.</span></span>

### <a name="using-basic-digest-or-windows-authentication"></a><span data-ttu-id="7902e-148">使用基本、摘要或 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="7902e-148">Using Basic, Digest, or Windows authentication</span></span>

<span data-ttu-id="7902e-149">設定`authenticationType`為`Basic`， `Digest`，或`Windows`，並指定 hello 除了 hello HTTP 連接器泛型的上方導入了下列屬性：</span><span class="sxs-lookup"><span data-stu-id="7902e-149">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="7902e-150">屬性</span><span class="sxs-lookup"><span data-stu-id="7902e-150">Property</span></span> | <span data-ttu-id="7902e-151">說明</span><span class="sxs-lookup"><span data-stu-id="7902e-151">Description</span></span> | <span data-ttu-id="7902e-152">必要</span><span class="sxs-lookup"><span data-stu-id="7902e-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7902e-153">username</span><span class="sxs-lookup"><span data-stu-id="7902e-153">username</span></span> | <span data-ttu-id="7902e-154">使用者名稱 tooaccess hello HTTP 端點。</span><span class="sxs-lookup"><span data-stu-id="7902e-154">Username tooaccess hello HTTP endpoint.</span></span> | <span data-ttu-id="7902e-155">是</span><span class="sxs-lookup"><span data-stu-id="7902e-155">Yes</span></span> |
| <span data-ttu-id="7902e-156">password</span><span class="sxs-lookup"><span data-stu-id="7902e-156">password</span></span> | <span data-ttu-id="7902e-157">Hello 使用者 （使用者名稱） 的密碼。</span><span class="sxs-lookup"><span data-stu-id="7902e-157">Password for hello user (username).</span></span> | <span data-ttu-id="7902e-158">是</span><span class="sxs-lookup"><span data-stu-id="7902e-158">Yes</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="7902e-159">範例︰使用基本、摘要或 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="7902e-159">Example: using Basic, Digest, or Windows authentication</span></span>

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

### <a name="using-clientcertificate-authentication"></a><span data-ttu-id="7902e-160">使用 ClientCertificate 驗證</span><span class="sxs-lookup"><span data-stu-id="7902e-160">Using ClientCertificate authentication</span></span>

<span data-ttu-id="7902e-161">toouse 基本驗證時，設定`authenticationType`為`ClientCertificate`，並指定 hello 除了 hello HTTP 連接器泛型的上方導入了下列屬性：</span><span class="sxs-lookup"><span data-stu-id="7902e-161">toouse basic authentication, set `authenticationType` as `ClientCertificate`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="7902e-162">屬性</span><span class="sxs-lookup"><span data-stu-id="7902e-162">Property</span></span> | <span data-ttu-id="7902e-163">說明</span><span class="sxs-lookup"><span data-stu-id="7902e-163">Description</span></span> | <span data-ttu-id="7902e-164">必要</span><span class="sxs-lookup"><span data-stu-id="7902e-164">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7902e-165">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="7902e-165">embeddedCertData</span></span> | <span data-ttu-id="7902e-166">hello Base64 編碼內容的 hello 個人資訊交換 (PFX) 檔案的二進位資料。</span><span class="sxs-lookup"><span data-stu-id="7902e-166">hello Base64-encoded contents of binary data of hello Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="7902e-167">指定任一個 hello`embeddedCertData`或`certThumbprint`。</span><span class="sxs-lookup"><span data-stu-id="7902e-167">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="7902e-168">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="7902e-168">certThumbprint</span></span> | <span data-ttu-id="7902e-169">hello hello 憑證已安裝在閘道機器的憑證存放區上的憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="7902e-169">hello thumbprint of hello certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="7902e-170">僅當從內部部署 HTTP 來源複製資料時才套用。</span><span class="sxs-lookup"><span data-stu-id="7902e-170">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="7902e-171">指定任一個 hello`embeddedCertData`或`certThumbprint`。</span><span class="sxs-lookup"><span data-stu-id="7902e-171">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="7902e-172">password</span><span class="sxs-lookup"><span data-stu-id="7902e-172">password</span></span> | <span data-ttu-id="7902e-173">Hello 憑證相關聯的密碼。</span><span class="sxs-lookup"><span data-stu-id="7902e-173">Password associated with hello certificate.</span></span> | <span data-ttu-id="7902e-174">否</span><span class="sxs-lookup"><span data-stu-id="7902e-174">No</span></span> |

<span data-ttu-id="7902e-175">如果您使用`certThumbprint`安裝適用於驗證和 hello 憑證的 hello hello 本機電腦的個人存放區中，您需要 toogrant hello 的讀取權限 toohello 閘道服務：</span><span class="sxs-lookup"><span data-stu-id="7902e-175">If you use `certThumbprint` for authentication and hello certificate is installed in hello personal store of hello local computer, you need toogrant hello read permission toohello gateway service:</span></span>

1. <span data-ttu-id="7902e-176">啟動 Microsoft Management Console (MMC)。</span><span class="sxs-lookup"><span data-stu-id="7902e-176">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="7902e-177">新增 hello**憑證**嵌入式管理單元的目標 hello**本機電腦**。</span><span class="sxs-lookup"><span data-stu-id="7902e-177">Add hello **Certificates** snap-in that targets hello **Local Computer**.</span></span>
2. <span data-ttu-id="7902e-178">展開 [憑證]，[個人]，然後按一下 [憑證]。</span><span class="sxs-lookup"><span data-stu-id="7902e-178">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="7902e-179">Hello 個人存放區中的 hello 憑證上按一下滑鼠右鍵，然後選取**所有工作**->**管理私用金鑰...**</span><span class="sxs-lookup"><span data-stu-id="7902e-179">Right-click hello certificate from hello personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="7902e-180">在 [hello**安全性**索引標籤上，新增 hello 資料管理閘道主機服務執行使用 hello 讀取權限 toohello 憑證的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="7902e-180">On hello **Security** tab, add hello user account under which Data Management Gateway Host Service is running with hello read access toohello certificate.</span></span>  

#### <a name="example-using-client-certificate"></a><span data-ttu-id="7902e-181">範例︰使用用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="7902e-181">Example: using client certificate</span></span>
<span data-ttu-id="7902e-182">此連結服務連結資料 factory tooan 內部 HTTP web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="7902e-182">This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="7902e-183">它會使用與資料管理閘道器安裝 hello 機器已安裝的用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="7902e-183">It uses a client certificate that is installed on hello machine with Data Management Gateway installed.</span></span>

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

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="7902e-184">範例︰在檔案中使用用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="7902e-184">Example: using client certificate in a file</span></span>
<span data-ttu-id="7902e-185">此連結服務連結資料 factory tooan 內部 HTTP web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="7902e-185">This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="7902e-186">它會使用資料管理閘道器安裝 hello 機器上的用戶端憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="7902e-186">It uses a client certificate file on hello machine with Data Management Gateway installed.</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="7902e-187">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="7902e-187">Dataset properties</span></span>
<span data-ttu-id="7902e-188">區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="7902e-188">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="7902e-189">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="7902e-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="7902e-190">hello **typeProperties**區段是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置相關資訊。</span><span class="sxs-lookup"><span data-stu-id="7902e-190">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="7902e-191">hello typeProperties 區段類型的資料集**Http**具有下列屬性的 hello</span><span class="sxs-lookup"><span data-stu-id="7902e-191">hello typeProperties section for dataset of type **Http** has hello following properties</span></span>

| <span data-ttu-id="7902e-192">屬性</span><span class="sxs-lookup"><span data-stu-id="7902e-192">Property</span></span> | <span data-ttu-id="7902e-193">說明</span><span class="sxs-lookup"><span data-stu-id="7902e-193">Description</span></span> | <span data-ttu-id="7902e-194">必要</span><span class="sxs-lookup"><span data-stu-id="7902e-194">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="7902e-195">類型</span><span class="sxs-lookup"><span data-stu-id="7902e-195">type</span></span> | <span data-ttu-id="7902e-196">指定的 hello 資料集的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="7902e-196">Specified hello type of hello dataset.</span></span> <span data-ttu-id="7902e-197">必須設定得`Http`。</span><span class="sxs-lookup"><span data-stu-id="7902e-197">must be set too`Http`.</span></span> | <span data-ttu-id="7902e-198">是</span><span class="sxs-lookup"><span data-stu-id="7902e-198">Yes</span></span> |
| <span data-ttu-id="7902e-199">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="7902e-199">relativeUrl</span></span> | <span data-ttu-id="7902e-200">包含 hello 資料的相對 URL toohello 資源。</span><span class="sxs-lookup"><span data-stu-id="7902e-200">A relative URL toohello resource that contains hello data.</span></span> <span data-ttu-id="7902e-201">若未指定路徑，則會使用連結的 hello 服務定義中指定的唯一 hello URL。</span><span class="sxs-lookup"><span data-stu-id="7902e-201">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> <br><br> <span data-ttu-id="7902e-202">tooconstruct 動態 URL，您可以使用[Data Factory 函數和系統變數](data-factory-functions-variables.md)，例如"relativeUrl":"$$Text.Format ('/ my/報表？ 月 = {0:yyyy}-{0:MM} （& s) fmt = csv'，SliceStart) 」。</span><span class="sxs-lookup"><span data-stu-id="7902e-202">tooconstruct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), e.g. "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)".</span></span> | <span data-ttu-id="7902e-203">否</span><span class="sxs-lookup"><span data-stu-id="7902e-203">No</span></span> |
| <span data-ttu-id="7902e-204">requestMethod</span><span class="sxs-lookup"><span data-stu-id="7902e-204">requestMethod</span></span> | <span data-ttu-id="7902e-205">HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="7902e-205">Http method.</span></span> <span data-ttu-id="7902e-206">允許的值為 **GET** 或 **POST**。</span><span class="sxs-lookup"><span data-stu-id="7902e-206">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="7902e-207">否。</span><span class="sxs-lookup"><span data-stu-id="7902e-207">No.</span></span> <span data-ttu-id="7902e-208">預設值為 `GET`。</span><span class="sxs-lookup"><span data-stu-id="7902e-208">Default is `GET`.</span></span> |
| <span data-ttu-id="7902e-209">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="7902e-209">additionalHeaders</span></span> | <span data-ttu-id="7902e-210">其他 HTTP 要求標頭。</span><span class="sxs-lookup"><span data-stu-id="7902e-210">Additional HTTP request headers.</span></span> | <span data-ttu-id="7902e-211">否</span><span class="sxs-lookup"><span data-stu-id="7902e-211">No</span></span> |
| <span data-ttu-id="7902e-212">requestBody</span><span class="sxs-lookup"><span data-stu-id="7902e-212">requestBody</span></span> | <span data-ttu-id="7902e-213">HTTP 要求的內文。</span><span class="sxs-lookup"><span data-stu-id="7902e-213">Body for HTTP request.</span></span> | <span data-ttu-id="7902e-214">否</span><span class="sxs-lookup"><span data-stu-id="7902e-214">No</span></span> |
| <span data-ttu-id="7902e-215">format</span><span class="sxs-lookup"><span data-stu-id="7902e-215">format</span></span> | <span data-ttu-id="7902e-216">如果您想 toosimply **hello 資料擷取 HTTP 端點以-為**而不剖析它，請略過此格式設定。</span><span class="sxs-lookup"><span data-stu-id="7902e-216">If you want toosimply **retrieve hello data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="7902e-217">如果您希望 tooparse hello HTTP 回應內容進行複製時，支援下列格式類型的 hello: **TextFormat**， **JsonFormat**， **AvroFormat**， **OrcFormat**， **ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="7902e-217">If you want tooparse hello HTTP response content during copy, hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="7902e-218">如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。</span><span class="sxs-lookup"><span data-stu-id="7902e-218">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="7902e-219">否</span><span class="sxs-lookup"><span data-stu-id="7902e-219">No</span></span> |
| <span data-ttu-id="7902e-220">compression</span><span class="sxs-lookup"><span data-stu-id="7902e-220">compression</span></span> | <span data-ttu-id="7902e-221">指定 hello 類型和層級的 hello 資料壓縮。</span><span class="sxs-lookup"><span data-stu-id="7902e-221">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="7902e-222">支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。</span><span class="sxs-lookup"><span data-stu-id="7902e-222">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="7902e-223">支援的層級為：**Optimal** 和 **Fastest**。</span><span class="sxs-lookup"><span data-stu-id="7902e-223">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="7902e-224">如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。</span><span class="sxs-lookup"><span data-stu-id="7902e-224">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="7902e-225">否</span><span class="sxs-lookup"><span data-stu-id="7902e-225">No</span></span> |

### <a name="example-using-hello-get-default-method"></a><span data-ttu-id="7902e-226">範例： 使用 hello GET （預設值） 方法</span><span class="sxs-lookup"><span data-stu-id="7902e-226">Example: using hello GET (default) method</span></span>

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

### <a name="example-using-hello-post-method"></a><span data-ttu-id="7902e-227">範例： 使用 hello POST 方法</span><span class="sxs-lookup"><span data-stu-id="7902e-227">Example: using hello POST method</span></span>

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

## <a name="copy-activity-properties"></a><span data-ttu-id="7902e-228">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="7902e-228">Copy activity properties</span></span>
<span data-ttu-id="7902e-229">區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="7902e-229">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="7902e-230">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="7902e-230">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="7902e-231">屬性用於 hello **typeProperties** > 一節的 hello hello 活動另一方面會隨每個活動類型。</span><span class="sxs-lookup"><span data-stu-id="7902e-231">Properties available in hello **typeProperties** section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="7902e-232">複製活動它們而異的來源與接收的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="7902e-232">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="7902e-233">目前，當複製活動中的 hello 來源屬於型別**HttpSource**，支援下列屬性的 hello。</span><span class="sxs-lookup"><span data-stu-id="7902e-233">Currently, when hello source in copy activity is of type **HttpSource**, hello following properties are supported.</span></span>

| <span data-ttu-id="7902e-234">屬性</span><span class="sxs-lookup"><span data-stu-id="7902e-234">Property</span></span> | <span data-ttu-id="7902e-235">說明</span><span class="sxs-lookup"><span data-stu-id="7902e-235">Description</span></span> | <span data-ttu-id="7902e-236">必要</span><span class="sxs-lookup"><span data-stu-id="7902e-236">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="7902e-237">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="7902e-237">httpRequestTimeout</span></span> | <span data-ttu-id="7902e-238">hello 回應 hello HTTP 要求 tooget 的逾時 (TimeSpan)。</span><span class="sxs-lookup"><span data-stu-id="7902e-238">hello timeout (TimeSpan) for hello HTTP request tooget a response.</span></span> <span data-ttu-id="7902e-239">它是 hello 逾時 tooget 回應時，不 hello 逾時 tooread 回應資料。</span><span class="sxs-lookup"><span data-stu-id="7902e-239">It is hello timeout tooget a response, not hello timeout tooread response data.</span></span> | <span data-ttu-id="7902e-240">否。</span><span class="sxs-lookup"><span data-stu-id="7902e-240">No.</span></span> <span data-ttu-id="7902e-241">預設值：00:01:40</span><span class="sxs-lookup"><span data-stu-id="7902e-241">Default value: 00:01:40</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="7902e-242">支援的檔案和壓縮格式</span><span class="sxs-lookup"><span data-stu-id="7902e-242">Supported file and compression formats</span></span>
<span data-ttu-id="7902e-243">請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md)文章以了解詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7902e-243">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="7902e-244">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="7902e-244">JSON examples</span></span>
<span data-ttu-id="7902e-245">下列範例中的 hello 提供範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="7902e-245">hello following example provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="7902e-246">它們會顯示如何從 HTTP toocopy 資料來源 tooAzure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="7902e-246">They show how toocopy data from HTTP source tooAzure Blob Storage.</span></span> <span data-ttu-id="7902e-247">不過，資料可以複製**直接**從任何來源 tooany hello 接收所述的[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="7902e-247">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-http-source-tooazure-blob-storage"></a><span data-ttu-id="7902e-248">範例： 將資料複製 HTTP 來源 tooAzure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="7902e-248">Example: Copy data from HTTP source tooAzure Blob Storage</span></span>
<span data-ttu-id="7902e-249">hello Data Factory 方案，此範例包含下列 Data Factory 實體的 hello:</span><span class="sxs-lookup"><span data-stu-id="7902e-249">hello Data Factory solution for this sample contains hello following Data Factory entities:</span></span>

1. <span data-ttu-id="7902e-250">一個 [HTTP](#linked-service-properties) 類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="7902e-250">A linked service of type [HTTP](#linked-service-properties).</span></span>
2. <span data-ttu-id="7902e-251">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="7902e-251">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="7902e-252">[Http](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="7902e-252">An input [dataset](data-factory-create-datasets.md) of type [Http](#dataset-properties).</span></span>
4. <span data-ttu-id="7902e-253">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="7902e-253">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="7902e-254">具有使用 [HttpSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="7902e-254">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [HttpSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="7902e-255">hello 範例將資料從 Azure blob HTTP 來源 tooan 每小時。</span><span class="sxs-lookup"><span data-stu-id="7902e-255">hello sample copies data from an HTTP source tooan Azure blob every hour.</span></span> <span data-ttu-id="7902e-256">這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。</span><span class="sxs-lookup"><span data-stu-id="7902e-256">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

### <a name="http-linked-service"></a><span data-ttu-id="7902e-257">HTTP 連結服務</span><span class="sxs-lookup"><span data-stu-id="7902e-257">HTTP linked service</span></span>
<span data-ttu-id="7902e-258">這個範例會使用 hello HTTP 連結服務與匿名驗證。</span><span class="sxs-lookup"><span data-stu-id="7902e-258">This example uses hello HTTP linked service with anonymous authentication.</span></span> <span data-ttu-id="7902e-259">請參閱 [HTTP 連結服務](#linked-service-properties)一節，來了解您可以使用的不同驗證類型。</span><span class="sxs-lookup"><span data-stu-id="7902e-259">See [HTTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

### <a name="azure-storage-linked-service"></a><span data-ttu-id="7902e-260">Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="7902e-260">Azure Storage linked service</span></span>

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

### <a name="http-input-dataset"></a><span data-ttu-id="7902e-261">HTTP 輸入資料集</span><span class="sxs-lookup"><span data-stu-id="7902e-261">HTTP input dataset</span></span>
<span data-ttu-id="7902e-262">設定**外部**太**true**該 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時，會通知 hello Data Factory 服務。</span><span class="sxs-lookup"><span data-stu-id="7902e-262">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="7902e-263">Azure Blob 輸出資料集</span><span class="sxs-lookup"><span data-stu-id="7902e-263">Azure Blob output dataset</span></span>

<span data-ttu-id="7902e-264">資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。</span><span class="sxs-lookup"><span data-stu-id="7902e-264">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

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

### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="7902e-265">具有複製活動的管線</span><span class="sxs-lookup"><span data-stu-id="7902e-265">Pipeline with Copy activity</span></span>

<span data-ttu-id="7902e-266">hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。</span><span class="sxs-lookup"><span data-stu-id="7902e-266">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="7902e-267">在 hello 管線 JSON 定義中，hello**來源**類型設定得**HttpSource**和**接收**類型設定得**BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="7902e-267">In hello pipeline JSON definition, hello **source** type is set too**HttpSource** and **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="7902e-268">請參閱[HttpSource](#copy-activity-properties) hello hello HttpSource 支援之屬性的清單。</span><span class="sxs-lookup"><span data-stu-id="7902e-268">See [HttpSource](#copy-activity-properties) for hello list of properties supported by hello HttpSource.</span></span>

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
        "description": "Copy from an HTTP source tooan Azure blob",
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
> <span data-ttu-id="7902e-269">toomap 資料行從來源資料集 toocolumns 從接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="7902e-269">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="7902e-270">效能和微調</span><span class="sxs-lookup"><span data-stu-id="7902e-270">Performance and Tuning</span></span>
<span data-ttu-id="7902e-271">請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。</span><span class="sxs-lookup"><span data-stu-id="7902e-271">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
