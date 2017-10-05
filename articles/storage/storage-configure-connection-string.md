---
title: "設定 Azure 儲存體的連接字串 | Microsoft Docs"
description: "設定 Azure 儲存體帳戶的連接字串。 連接字串包含在執行階段從應用程式驗證儲存體帳戶存取所需的資訊。"
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
ms.openlocfilehash: 01aa506e2b47fc29a70592e670a206a2b74248a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-azure-storage-connection-strings"></a><span data-ttu-id="8b615-104">設定 Azure 儲存體連接字串</span><span class="sxs-lookup"><span data-stu-id="8b615-104">Configure Azure Storage connection strings</span></span>

<span data-ttu-id="8b615-105">連接字串包含在執行階段應用程式存取 Azure 儲存體帳戶中資料所需的驗證資訊。</span><span class="sxs-lookup"><span data-stu-id="8b615-105">A connection string includes the authentication information required for your application to access data in an Azure Storage account at runtime.</span></span> <span data-ttu-id="8b615-106">您可以設定連接字串，以進行下列動作：</span><span class="sxs-lookup"><span data-stu-id="8b615-106">You can configure connection strings to:</span></span>

* <span data-ttu-id="8b615-107">連線至 Azure 儲存體模擬器</span><span class="sxs-lookup"><span data-stu-id="8b615-107">Connect to the Azure storage emulator.</span></span>
* <span data-ttu-id="8b615-108">在 Azure 中存取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8b615-108">Access a storage account in Azure.</span></span>
* <span data-ttu-id="8b615-109">透過共用存取簽章 (SAS) 存取 Azure 中的指定資源。</span><span class="sxs-lookup"><span data-stu-id="8b615-109">Access specified resources in Azure via a shared access signature (SAS).</span></span>

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

## <a name="storing-your-connection-string"></a><span data-ttu-id="8b615-110">儲存您的連接字串</span><span class="sxs-lookup"><span data-stu-id="8b615-110">Storing your connection string</span></span>
<span data-ttu-id="8b615-111">您的應用程式需要在執行階段存取連接字串，才能驗證對 Azure 儲存體進行的要求。</span><span class="sxs-lookup"><span data-stu-id="8b615-111">Your application needs to access the connection string at runtime to authenticate requests made to Azure Storage.</span></span> <span data-ttu-id="8b615-112">您有幾種選項可用來儲存連接字串：</span><span class="sxs-lookup"><span data-stu-id="8b615-112">You have several options for storing your connection string:</span></span>

* <span data-ttu-id="8b615-113">在桌面上或裝置上執行的應用程式可將連接字串儲存在 **app.config** 或 **web.config** 檔案。</span><span class="sxs-lookup"><span data-stu-id="8b615-113">An application running on the desktop or on a device can store the connection string in an **app.config** or **web.config** file.</span></span> <span data-ttu-id="8b615-114">將連接字串新增至這些檔案中的 **AppSettings** 區段。</span><span class="sxs-lookup"><span data-stu-id="8b615-114">Add the connection string to the **AppSettings** section in these files.</span></span>
* <span data-ttu-id="8b615-115">在 Azure 雲端服務中執行的應用程式可將連接字串儲存在 [Azure 服務組態結構描述 (.cscfg) 檔](https://msdn.microsoft.com/library/ee758710.aspx)中。</span><span class="sxs-lookup"><span data-stu-id="8b615-115">An application running in an Azure cloud service can store the connection string in the [Azure service configuration schema (.cscfg) file](https://msdn.microsoft.com/library/ee758710.aspx).</span></span> <span data-ttu-id="8b615-116">將此連接字串加入服務組態檔的 [ConfigurationSettings]  區段。</span><span class="sxs-lookup"><span data-stu-id="8b615-116">Add the connection string to the **ConfigurationSettings** section of the service configuration file.</span></span>
* <span data-ttu-id="8b615-117">您可以直接在您的程式碼中使用連接字串。</span><span class="sxs-lookup"><span data-stu-id="8b615-117">You can use your connection string directly in your code.</span></span> <span data-ttu-id="8b615-118">不過，在大部分情況下，建議您在組態檔中儲存連接字串。</span><span class="sxs-lookup"><span data-stu-id="8b615-118">However, we recommend that you store your connection string in a configuration file in most scenarios.</span></span>

<span data-ttu-id="8b615-119">在組態檔內儲存連接字串，可讓您更容易更新連接字串，藉此在儲存體模擬器和雲端中的 Azure 儲存體帳戶之間切換。</span><span class="sxs-lookup"><span data-stu-id="8b615-119">Storing your connection string in a configuration file makes it easy to update the connection string to switch between the storage emulator and an Azure storage account in the cloud.</span></span> <span data-ttu-id="8b615-120">您只需要編輯連接字串以指向您的目標環境。</span><span class="sxs-lookup"><span data-stu-id="8b615-120">You only need to edit the connection string to point to your target environment.</span></span>

<span data-ttu-id="8b615-121">您可以使用 [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)，在執行階段存取連接字串，而不論應用程式執行所在的地方為何。</span><span class="sxs-lookup"><span data-stu-id="8b615-121">You can use the [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) to access your connection string at runtime regardless of where your application is running.</span></span>

## <a name="create-a-connection-string-for-the-storage-emulator"></a><span data-ttu-id="8b615-122">建立儲存體模擬器的連接字串</span><span class="sxs-lookup"><span data-stu-id="8b615-122">Create a connection string for the storage emulator</span></span>
[!INCLUDE [storage-emulator-connection-string-include](../../includes/storage-emulator-connection-string-include.md)]

<span data-ttu-id="8b615-123">如需儲存體模擬器的詳細資訊，請參閱 [使用 Azure 儲存體模擬器進行開發和測試](storage-use-emulator.md) 。</span><span class="sxs-lookup"><span data-stu-id="8b615-123">For more information about the storage emulator, see [Use the Azure storage emulator for development and testing](storage-use-emulator.md).</span></span>

## <a name="create-a-connection-string-for-an-azure-storage-account"></a><span data-ttu-id="8b615-124">建立 Azure 儲存體帳戶的連接字串</span><span class="sxs-lookup"><span data-stu-id="8b615-124">Create a connection string for an Azure storage account</span></span>
<span data-ttu-id="8b615-125">若要建立 Azure 儲存體帳戶的連接字串，請使用以下格式。</span><span class="sxs-lookup"><span data-stu-id="8b615-125">To create a connection string for your Azure storage account, use the following format.</span></span> <span data-ttu-id="8b615-126">指出您是否要透過 HTTPS (建議選項) 或 HTTP 連線至儲存體帳戶、使用您的儲存體帳戶名稱來取代 `myAccountName`，以及使用您的帳戶存取金鑰來取代 `myAccountKey`：</span><span class="sxs-lookup"><span data-stu-id="8b615-126">Indicate whether you want to connect to the storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with the name of your storage account, and replace `myAccountKey` with your account access key:</span></span>

`DefaultEndpointsProtocol=[http|https];AccountName=myAccountName;AccountKey=myAccountKey`

<span data-ttu-id="8b615-127">例如，您的連接字串看起來可能如下所示︰</span><span class="sxs-lookup"><span data-stu-id="8b615-127">For example, your connection string might look similar to:</span></span>

`DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=<account-key>`

<span data-ttu-id="8b615-128">雖然 Azure 儲存體可同時支援連接字串中的 HTTP 和 HTTPS，但*強烈建議您使用 HTTPS*。</span><span class="sxs-lookup"><span data-stu-id="8b615-128">Although Azure Storage supports both HTTP and HTTPS in a connection string, *HTTPS is highly recommended*.</span></span>

> [!TIP]
> <span data-ttu-id="8b615-129">您可以在 [Azure 入口網站](https://portal.azure.com)中找到儲存體帳戶的連接字串。</span><span class="sxs-lookup"><span data-stu-id="8b615-129">You can find your storage account's connection strings in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="8b615-130">若要查看這主要和次要存取金鑰的連接字串，請在儲存體帳戶的功能表刀鋒視窗中，瀏覽至 [設定] > [存取金鑰]。</span><span class="sxs-lookup"><span data-stu-id="8b615-130">Navigate to **SETTINGS** > **Access keys** in your storage account's menu blade to see connection strings for both primary and secondary access keys.</span></span>
>

## <a name="create-a-connection-string-using-a-shared-access-signature"></a><span data-ttu-id="8b615-131">使用共用存取簽章建立連接字串</span><span class="sxs-lookup"><span data-stu-id="8b615-131">Create a connection string using a shared access signature</span></span>
[!INCLUDE [storage-use-sas-in-connection-string-include](../../includes/storage-use-sas-in-connection-string-include.md)]

## <a name="create-a-connection-string-for-an-explicit-storage-endpoint"></a><span data-ttu-id="8b615-132">建立明確儲存體端點的連接字串</span><span class="sxs-lookup"><span data-stu-id="8b615-132">Create a connection string for an explicit storage endpoint</span></span>
<span data-ttu-id="8b615-133">您可以在連接字串中指定明確的服務端點，而不使用預設端點。</span><span class="sxs-lookup"><span data-stu-id="8b615-133">You can specify explicit service endpoints in your connection string instead of using the default endpoints.</span></span> <span data-ttu-id="8b615-134">若要建立指定明確端點的連接字串，請使用下列格式來指定每個服務的完整服務端點，包括通訊協定規格 (HTTPS (建議選項) 或 HTTP)：</span><span class="sxs-lookup"><span data-stu-id="8b615-134">To create a connection string that specifies an explicit endpoint, specify the complete service endpoint for each service, including the protocol specification (HTTPS (recommended) or HTTP), in the following format:</span></span>

```
DefaultEndpointsProtocol=[http|https];
BlobEndpoint=myBlobEndpoint;
FileEndpoint=myFileEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
AccountName=myAccountName;
AccountKey=myAccountKey
```

<span data-ttu-id="8b615-135">您可能想要指定明確端點的一個案例為是否您已將 Blob 儲存體端點對應至[自訂網域](storage-custom-domain-name.md)。</span><span class="sxs-lookup"><span data-stu-id="8b615-135">One scenario where you might wish to specify an explicit endpoint is when you've mapped your Blob storage endpoint to a [custom domain](storage-custom-domain-name.md).</span></span> <span data-ttu-id="8b615-136">在此情況下，您可以在連接字串中指定 Blob 儲存體的自訂端點。</span><span class="sxs-lookup"><span data-stu-id="8b615-136">In that case, you can specify your custom endpoint for Blob storage in your connection string.</span></span> <span data-ttu-id="8b615-137">您可以選擇性地指派其他服務的預設端點 (如果應用程式有使用這些服務) 。</span><span class="sxs-lookup"><span data-stu-id="8b615-137">You can optionally specify the default endpoints for the other services if your application uses them.</span></span>

<span data-ttu-id="8b615-138">以下是針對 Blob 服務指定明確端點的連接字串範例︰</span><span class="sxs-lookup"><span data-stu-id="8b615-138">Here is an example of a connection string that specifies an explicit endpoint for the Blob service:</span></span>

```
# Blob endpoint only
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
AccountName=storagesample;
AccountKey=<account-key>
```

<span data-ttu-id="8b615-139">此範例會指定所有服務的明確端點，包括 Blob 服務的自訂網域︰</span><span class="sxs-lookup"><span data-stu-id="8b615-139">This example specifies explicit endpoints for all services, including a custom domain for the Blob service:</span></span>

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

<span data-ttu-id="8b615-140">連接字串中的端點值可用來建構連線至儲存體服務的要求 URI，並要求任何傳回到您程式碼的 URI 形式。</span><span class="sxs-lookup"><span data-stu-id="8b615-140">The endpoint values in a connection string are used to construct the request URIs to the storage services, and dictate the form of any URIs that are returned to your code.</span></span>

<span data-ttu-id="8b615-141">如果你已將儲存體端點對應至自訂網域，且從連接字串中省略該端點，則無法使用該連接字串，從程式碼中存取該服務中的資料。</span><span class="sxs-lookup"><span data-stu-id="8b615-141">If you've mapped a storage endpoint to a custom domain and omit that endpoint from a connection string, then you will not be able to use that connection string to access data in that service from your code.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b615-142">連接字串中的服務端點值必須是格式正確的 URI，包括 `https://`(建議) 或 `http://`。</span><span class="sxs-lookup"><span data-stu-id="8b615-142">Service endpoint values in your connection strings must be well-formed URIs, including `https://` (recommended) or `http://`.</span></span> <span data-ttu-id="8b615-143">因為 Azure 儲存體還不支援自訂網域的 HTTPS，您必須針對任何指向自訂網域的端點 URI，指定 `http://`。</span><span class="sxs-lookup"><span data-stu-id="8b615-143">Because Azure Storage does not yet support HTTPS for custom domains, you *must* specify `http://` for any endpoint URI that points to a custom domain.</span></span>
>

### <a name="create-a-connection-string-with-an-endpoint-suffix"></a><span data-ttu-id="8b615-144">建立包含端點尾碼的連接字串</span><span class="sxs-lookup"><span data-stu-id="8b615-144">Create a connection string with an endpoint suffix</span></span>
<span data-ttu-id="8b615-145">若要建立區域或包含不同端點尾碼的執行個體 (例如 Azure China 或 Azure Government) 中儲存體服務的連接字串，請使用下列連接字串格式。</span><span class="sxs-lookup"><span data-stu-id="8b615-145">To create a connection string for a storage service in regions or instances with different endpoint suffixes, such as for Azure China or Azure Government, use the following connection string format.</span></span> <span data-ttu-id="8b615-146">指出您是否要透過 HTTPS (建議) 或 HTTP 連線至儲存體帳戶、使用您的儲存體帳戶名稱來取代 `myAccountName`、使用您的帳戶存取金鑰來取代 `myAccountKey`，以及使用 URI 尾碼來取代 `mySuffix`：</span><span class="sxs-lookup"><span data-stu-id="8b615-146">Indicate whether you want to connect to the storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with the name of your storage account, replace `myAccountKey` with your account access key, and replace `mySuffix` with the URI suffix:</span></span>

```
DefaultEndpointsProtocol=[http|https];
AccountName=myAccountName;
AccountKey=myAccountKey;
EndpointSuffix=mySuffix;
```

<span data-ttu-id="8b615-147">以下是 Azure China 中儲存體服務的連接字串範例：</span><span class="sxs-lookup"><span data-stu-id="8b615-147">Here's an example connection string for storage services in Azure China:</span></span>

```
DefaultEndpointsProtocol=https;
AccountName=storagesample;
AccountKey=<account-key>;
EndpointSuffix=core.chinacloudapi.cn;
```

## <a name="parsing-a-connection-string"></a><span data-ttu-id="8b615-148">剖析連接字串</span><span class="sxs-lookup"><span data-stu-id="8b615-148">Parsing a connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="next-steps"></a><span data-ttu-id="8b615-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8b615-149">Next steps</span></span>
* [<span data-ttu-id="8b615-150">使用 Azure 儲存體模擬器進行開發和測試</span><span class="sxs-lookup"><span data-stu-id="8b615-150">Use the Azure storage emulator for development and testing</span></span>](storage-use-emulator.md)
* [<span data-ttu-id="8b615-151">Azure 儲存體總管</span><span class="sxs-lookup"><span data-stu-id="8b615-151">Azure Storage explorers</span></span>](storage-explorers.md)
* [<span data-ttu-id="8b615-152">使用共用存取簽章 (SAS)</span><span class="sxs-lookup"><span data-stu-id="8b615-152">Using Shared Access Signatures (SAS)</span></span>](storage-dotnet-shared-access-signature-part-1.md)

