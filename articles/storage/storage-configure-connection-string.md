---
title: "aaaConfigure Azure 儲存體的連接字串 |Microsoft 文件"
description: "設定 Azure 儲存體帳戶的連接字串。 連接字串包含 hello 資訊所需 tooauthenticate 存取 tooa 儲存體帳戶從您的應用程式在執行階段。"
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: ecb0acb5-90a9-4eb2-93e6-e9860eda5e53
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: marsma
ms.openlocfilehash: 80c38a6f8f0d4f06b99e7c487647b984e01d1772
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-storage-connection-strings"></a><span data-ttu-id="14d68-104">設定 Azure 儲存體連接字串</span><span class="sxs-lookup"><span data-stu-id="14d68-104">Configure Azure Storage connection strings</span></span>

<span data-ttu-id="14d68-105">連接字串包含所需的應用程式 tooaccess 資料在執行階段的 Azure 儲存體帳戶中的 hello 驗證資訊。</span><span class="sxs-lookup"><span data-stu-id="14d68-105">A connection string includes hello authentication information required for your application tooaccess data in an Azure Storage account at runtime.</span></span> <span data-ttu-id="14d68-106">您可以設定連接字串，以進行下列動作：</span><span class="sxs-lookup"><span data-stu-id="14d68-106">You can configure connection strings to:</span></span>

* <span data-ttu-id="14d68-107">連接 toohello Azure 儲存體模擬器。</span><span class="sxs-lookup"><span data-stu-id="14d68-107">Connect toohello Azure storage emulator.</span></span>
* <span data-ttu-id="14d68-108">在 Azure 中存取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="14d68-108">Access a storage account in Azure.</span></span>
* <span data-ttu-id="14d68-109">透過共用存取簽章 (SAS) 存取 Azure 中的指定資源。</span><span class="sxs-lookup"><span data-stu-id="14d68-109">Access specified resources in Azure via a shared access signature (SAS).</span></span>

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

## <a name="storing-your-connection-string"></a><span data-ttu-id="14d68-110">儲存您的連接字串</span><span class="sxs-lookup"><span data-stu-id="14d68-110">Storing your connection string</span></span>
<span data-ttu-id="14d68-111">您的應用程式必須在執行階段 tooauthenticate 提出的要求 tooAzure 儲存體 tooaccess hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="14d68-111">Your application needs tooaccess hello connection string at runtime tooauthenticate requests made tooAzure Storage.</span></span> <span data-ttu-id="14d68-112">您有幾種選項可用來儲存連接字串：</span><span class="sxs-lookup"><span data-stu-id="14d68-112">You have several options for storing your connection string:</span></span>

* <span data-ttu-id="14d68-113">應用程式正在執行 hello 桌面或裝置上可以儲存中的 hello 連接字串**app.config**或**web.config**檔案。</span><span class="sxs-lookup"><span data-stu-id="14d68-113">An application running on hello desktop or on a device can store hello connection string in an **app.config** or **web.config** file.</span></span> <span data-ttu-id="14d68-114">新增 hello 連接字串 toohello **AppSettings**這些檔案中的區段。</span><span class="sxs-lookup"><span data-stu-id="14d68-114">Add hello connection string toohello **AppSettings** section in these files.</span></span>
* <span data-ttu-id="14d68-115">在 Azure 雲端服務中執行的應用程式可以將 hello 連接字串儲存在 hello [Azure 服務組態結構描述 (.cscfg) 檔](https://msdn.microsoft.com/library/ee758710.aspx)。</span><span class="sxs-lookup"><span data-stu-id="14d68-115">An application running in an Azure cloud service can store hello connection string in hello [Azure service configuration schema (.cscfg) file](https://msdn.microsoft.com/library/ee758710.aspx).</span></span> <span data-ttu-id="14d68-116">新增 hello 連接字串 toohello **ConfigurationSettings** hello 服務組態檔區段。</span><span class="sxs-lookup"><span data-stu-id="14d68-116">Add hello connection string toohello **ConfigurationSettings** section of hello service configuration file.</span></span>
* <span data-ttu-id="14d68-117">您可以直接在您的程式碼中使用連接字串。</span><span class="sxs-lookup"><span data-stu-id="14d68-117">You can use your connection string directly in your code.</span></span> <span data-ttu-id="14d68-118">不過，在大部分情況下，建議您在組態檔中儲存連接字串。</span><span class="sxs-lookup"><span data-stu-id="14d68-118">However, we recommend that you store your connection string in a configuration file in most scenarios.</span></span>

<span data-ttu-id="14d68-119">儲存您的連接字串組態檔中，可以輕鬆 tooupdate hello 連接字串 tooswitch hello 儲存體模擬器與 Azure 儲存體帳戶之間 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="14d68-119">Storing your connection string in a configuration file makes it easy tooupdate hello connection string tooswitch between hello storage emulator and an Azure storage account in hello cloud.</span></span> <span data-ttu-id="14d68-120">您只需要 tooedit hello 連接字串 toopoint tooyour 目標環境。</span><span class="sxs-lookup"><span data-stu-id="14d68-120">You only need tooedit hello connection string toopoint tooyour target environment.</span></span>

<span data-ttu-id="14d68-121">您可以使用 hello [Microsoft Azure 組態管理員](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)tooaccess 在執行階段，不論您的應用程式執行所在的連接字串。</span><span class="sxs-lookup"><span data-stu-id="14d68-121">You can use hello [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) tooaccess your connection string at runtime regardless of where your application is running.</span></span>

## <a name="create-a-connection-string-for-hello-storage-emulator"></a><span data-ttu-id="14d68-122">建立 hello 儲存體模擬器的連接字串</span><span class="sxs-lookup"><span data-stu-id="14d68-122">Create a connection string for hello storage emulator</span></span>
[!INCLUDE [storage-emulator-connection-string-include](../../includes/storage-emulator-connection-string-include.md)]

<span data-ttu-id="14d68-123">如需 hello 儲存體模擬器的詳細資訊，請參閱[使用 hello Azure 儲存體模擬器進行開發和測試](storage-use-emulator.md)。</span><span class="sxs-lookup"><span data-stu-id="14d68-123">For more information about hello storage emulator, see [Use hello Azure storage emulator for development and testing](storage-use-emulator.md).</span></span>

## <a name="create-a-connection-string-for-an-azure-storage-account"></a><span data-ttu-id="14d68-124">建立 Azure 儲存體帳戶的連接字串</span><span class="sxs-lookup"><span data-stu-id="14d68-124">Create a connection string for an Azure storage account</span></span>
<span data-ttu-id="14d68-125">toocreate Azure 儲存體帳戶的連接字串，使用 hello 下列格式。</span><span class="sxs-lookup"><span data-stu-id="14d68-125">toocreate a connection string for your Azure storage account, use hello following format.</span></span> <span data-ttu-id="14d68-126">表示是否要 tooconnect toohello 儲存體帳戶，透過 HTTPS （建議選項） 或 HTTP，而取代`myAccountName`同名的儲存體帳戶，並取代 hello`myAccountKey`與您的帳戶存取金鑰：</span><span class="sxs-lookup"><span data-stu-id="14d68-126">Indicate whether you want tooconnect toohello storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with hello name of your storage account, and replace `myAccountKey` with your account access key:</span></span>

`DefaultEndpointsProtocol=[http|https];AccountName=myAccountName;AccountKey=myAccountKey`

<span data-ttu-id="14d68-127">例如，您的連接字串看起來可能如下所示︰</span><span class="sxs-lookup"><span data-stu-id="14d68-127">For example, your connection string might look similar to:</span></span>

`DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=<account-key>`

<span data-ttu-id="14d68-128">雖然 Azure 儲存體可同時支援連接字串中的 HTTP 和 HTTPS，但*強烈建議您使用 HTTPS*。</span><span class="sxs-lookup"><span data-stu-id="14d68-128">Although Azure Storage supports both HTTP and HTTPS in a connection string, *HTTPS is highly recommended*.</span></span>

> [!TIP]
> <span data-ttu-id="14d68-129">您可以找到您的儲存體帳戶連接字串 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="14d68-129">You can find your storage account's connection strings in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="14d68-130">瀏覽過**設定** > **存取金鑰**儲存體帳戶的功能表刀鋒視窗 toosee 連接字串中這兩個主要和次要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="14d68-130">Navigate too**SETTINGS** > **Access keys** in your storage account's menu blade toosee connection strings for both primary and secondary access keys.</span></span>
>

## <a name="create-a-connection-string-using-a-shared-access-signature"></a><span data-ttu-id="14d68-131">使用共用存取簽章建立連接字串</span><span class="sxs-lookup"><span data-stu-id="14d68-131">Create a connection string using a shared access signature</span></span>
[!INCLUDE [storage-use-sas-in-connection-string-include](../../includes/storage-use-sas-in-connection-string-include.md)]

## <a name="create-a-connection-string-for-an-explicit-storage-endpoint"></a><span data-ttu-id="14d68-132">建立明確儲存體端點的連接字串</span><span class="sxs-lookup"><span data-stu-id="14d68-132">Create a connection string for an explicit storage endpoint</span></span>
<span data-ttu-id="14d68-133">您可以在連接字串，而不是使用 hello 預設端點中指定明確的服務端點。</span><span class="sxs-lookup"><span data-stu-id="14d68-133">You can specify explicit service endpoints in your connection string instead of using hello default endpoints.</span></span> <span data-ttu-id="14d68-134">toocreate 連接字串，指定了明確的端點，指定下列格式的 hello hello 完整服務端點的每個服務，包括 hello 通訊協定規格 （HTTPS （建議選項） 或 HTTP）：</span><span class="sxs-lookup"><span data-stu-id="14d68-134">toocreate a connection string that specifies an explicit endpoint, specify hello complete service endpoint for each service, including hello protocol specification (HTTPS (recommended) or HTTP), in hello following format:</span></span>

```
DefaultEndpointsProtocol=[http|https];
BlobEndpoint=myBlobEndpoint;
FileEndpoint=myFileEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
AccountName=myAccountName;
AccountKey=myAccountKey
```

<span data-ttu-id="14d68-135">您可能希望 toospecify 了明確的端點的其中一個案例是當您已對應您的 Blob 儲存體端點 tooa[自訂網域](storage-custom-domain-name.md)。</span><span class="sxs-lookup"><span data-stu-id="14d68-135">One scenario where you might wish toospecify an explicit endpoint is when you've mapped your Blob storage endpoint tooa [custom domain](storage-custom-domain-name.md).</span></span> <span data-ttu-id="14d68-136">在此情況下，您可以在連接字串中指定 Blob 儲存體的自訂端點。</span><span class="sxs-lookup"><span data-stu-id="14d68-136">In that case, you can specify your custom endpoint for Blob storage in your connection string.</span></span> <span data-ttu-id="14d68-137">您可以選擇性地指定 hello hello 預設端點的其他服務如果應用程式使用它們。</span><span class="sxs-lookup"><span data-stu-id="14d68-137">You can optionally specify hello default endpoints for hello other services if your application uses them.</span></span>

<span data-ttu-id="14d68-138">指定明確 hello Blob 服務端點的連接字串範例如下：</span><span class="sxs-lookup"><span data-stu-id="14d68-138">Here is an example of a connection string that specifies an explicit endpoint for hello Blob service:</span></span>

```
# Blob endpoint only
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
AccountName=storagesample;
AccountKey=<account-key>
```

<span data-ttu-id="14d68-139">這個範例會指定明確端點的所有服務，包括 hello Blob 服務的自訂網域：</span><span class="sxs-lookup"><span data-stu-id="14d68-139">This example specifies explicit endpoints for all services, including a custom domain for hello Blob service:</span></span>

```
# All service endpoints
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
FileEndpoint=https://myaccount.file.core.windows.net;
QueueEndpoint=https://myaccount.queue.core.windows.net;
TableEndpoint=https://myaccount.table.core.windows.net;
AccountName=storagesample;
AccountKey=<account-key>
```

<span data-ttu-id="14d68-140">連接字串中的 hello 端點值是使用的 tooconstruct hello 要求 Uri toohello 儲存體服務，並指示 hello 形式傳回 tooyour 程式碼的任何 Uri。</span><span class="sxs-lookup"><span data-stu-id="14d68-140">hello endpoint values in a connection string are used tooconstruct hello request URIs toohello storage services, and dictate hello form of any URIs that are returned tooyour code.</span></span>

<span data-ttu-id="14d68-141">如果您已對應儲存體端點 tooa 自訂網域，並省略從連接字串，該端點，然後就可以 toouse 該連接字串 tooaccess 該服務，從您的程式碼中的資料。</span><span class="sxs-lookup"><span data-stu-id="14d68-141">If you've mapped a storage endpoint tooa custom domain and omit that endpoint from a connection string, then you will not be able toouse that connection string tooaccess data in that service from your code.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="14d68-142">連接字串中的服務端點值必須是格式正確的 URI，包括 `https://`(建議) 或 `http://`。</span><span class="sxs-lookup"><span data-stu-id="14d68-142">Service endpoint values in your connection strings must be well-formed URIs, including `https://` (recommended) or `http://`.</span></span> <span data-ttu-id="14d68-143">因為 Azure 儲存體還不支援 HTTPS 的自訂網域，但您*必須*指定`http://`為任何端點 URI 指向 tooa 自訂網域。</span><span class="sxs-lookup"><span data-stu-id="14d68-143">Because Azure Storage does not yet support HTTPS for custom domains, you *must* specify `http://` for any endpoint URI that points tooa custom domain.</span></span>
>

### <a name="create-a-connection-string-with-an-endpoint-suffix"></a><span data-ttu-id="14d68-144">建立包含端點尾碼的連接字串</span><span class="sxs-lookup"><span data-stu-id="14d68-144">Create a connection string with an endpoint suffix</span></span>
<span data-ttu-id="14d68-145">toocreate 連接字串儲存體服務中的區域或不同的端點尾碼，具有執行個體這類中國 Azure 或 Azure 政府，使用下列連接字串格式的 hello。</span><span class="sxs-lookup"><span data-stu-id="14d68-145">toocreate a connection string for a storage service in regions or instances with different endpoint suffixes, such as for Azure China or Azure Government, use hello following connection string format.</span></span> <span data-ttu-id="14d68-146">表示是否要 tooconnect toohello 儲存體帳戶，透過 HTTPS （建議選項） 或 HTTP，而取代`myAccountName`hello 您的儲存體帳戶名稱，以取代`myAccountKey`與您的帳戶存取金鑰，取代`mySuffix`以 hello URI後置詞：</span><span class="sxs-lookup"><span data-stu-id="14d68-146">Indicate whether you want tooconnect toohello storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with hello name of your storage account, replace `myAccountKey` with your account access key, and replace `mySuffix` with hello URI suffix:</span></span>

```
DefaultEndpointsProtocol=[http|https];
AccountName=myAccountName;
AccountKey=myAccountKey;
EndpointSuffix=mySuffix;
```

<span data-ttu-id="14d68-147">以下是 Azure China 中儲存體服務的連接字串範例：</span><span class="sxs-lookup"><span data-stu-id="14d68-147">Here's an example connection string for storage services in Azure China:</span></span>

```
DefaultEndpointsProtocol=https;
AccountName=storagesample;
AccountKey=<account-key>;
EndpointSuffix=core.chinacloudapi.cn;
```

## <a name="parsing-a-connection-string"></a><span data-ttu-id="14d68-148">剖析連接字串</span><span class="sxs-lookup"><span data-stu-id="14d68-148">Parsing a connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="next-steps"></a><span data-ttu-id="14d68-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="14d68-149">Next steps</span></span>
* [<span data-ttu-id="14d68-150">使用 hello Azure 儲存體模擬器進行開發和測試</span><span class="sxs-lookup"><span data-stu-id="14d68-150">Use hello Azure storage emulator for development and testing</span></span>](storage-use-emulator.md)
* [<span data-ttu-id="14d68-151">Azure 儲存體總管</span><span class="sxs-lookup"><span data-stu-id="14d68-151">Azure Storage explorers</span></span>](storage-explorers.md)
* [<span data-ttu-id="14d68-152">使用共用存取簽章 (SAS)</span><span class="sxs-lookup"><span data-stu-id="14d68-152">Using Shared Access Signatures (SAS)</span></span>](storage-dotnet-shared-access-signature-part-1.md)

