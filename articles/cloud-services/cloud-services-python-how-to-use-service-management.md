---
title: "如何使用服務管理 API (Python) - 功能指南"
description: "了解如何透過程式設計從 Python 執行一般服務管理工作。"
services: cloud-services
documentationcenter: python
author: lmazuel
manager: wpickett
editor: 
ms.assetid: 61538ec0-1536-4a7e-ae89-95967fe35d73
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/30/2017
ms.author: lmazuel
ms.openlocfilehash: 13249ba9a4b317a3154776b411ce0bb1f316b3bb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-service-management-from-python"></a><span data-ttu-id="46f5c-103">如何從 Python 使用服務管理</span><span class="sxs-lookup"><span data-stu-id="46f5c-103">How to use Service Management from Python</span></span>
<span data-ttu-id="46f5c-104">本指南說明如何以程式設計方式，從 Python 執行一般服務管理工作。</span><span class="sxs-lookup"><span data-stu-id="46f5c-104">This guide shows you how to programmatically perform common service management tasks from Python.</span></span> <span data-ttu-id="46f5c-105">[Azure SDK for Python](https://github.com/Azure/azure-sdk-for-python) 中的 **ServiceManagementService** 類別支援以程式設計方式存取 [Azure 傳統入口網站][management-portal]所提供的大部分服務管理相關功能 (例如**建立、更新及刪除雲端服務、部署、資料管理服務和虛擬機器**)。</span><span class="sxs-lookup"><span data-stu-id="46f5c-105">The **ServiceManagementService** class in the [Azure SDK for Python](https://github.com/Azure/azure-sdk-for-python) supports programmatic access to much of the service management-related functionality that is available in the [Azure classic portal][management-portal] (such as **creating, updating, and deleting cloud services, deployments, data management services, and virtual machines**).</span></span> <span data-ttu-id="46f5c-106">建置需要透過程式設計方式存取服務管理的應用程式時，此功能十分實用。</span><span class="sxs-lookup"><span data-stu-id="46f5c-106">This functionality can be useful in building applications that need programmatic access to service management.</span></span>

## <span data-ttu-id="46f5c-107"><a name="WhatIs"> </a>什麼是服務管理？</span><span class="sxs-lookup"><span data-stu-id="46f5c-107"><a name="WhatIs"> </a>What is Service Management</span></span>
<span data-ttu-id="46f5c-108">服務管理 API 可讓使用者以程式設計方式存取 [Azure 傳統入口網站][management-portal]所提供的大部分服務管理功能。</span><span class="sxs-lookup"><span data-stu-id="46f5c-108">The Service Management API provides programmatic access to much of the service management functionality available through the [Azure classic portal][management-portal].</span></span> <span data-ttu-id="46f5c-109">Azure SDK for Python 可讓您管理雲端服務和儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="46f5c-109">The Azure SDK for Python allows you to manage your cloud services and storage accounts.</span></span>

<span data-ttu-id="46f5c-110">若要使用服務管理 API，您必須 [建立 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="46f5c-110">To use the Service Management API, you need to [create an Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <span data-ttu-id="46f5c-111"><a name="Concepts"> </a>概念</span><span class="sxs-lookup"><span data-stu-id="46f5c-111"><a name="Concepts"> </a>Concepts</span></span>
<span data-ttu-id="46f5c-112">Azure SDK for Python 含有 [Azure 服務管理 API][svc-mgmt-rest-api]，這是一種 REST API。</span><span class="sxs-lookup"><span data-stu-id="46f5c-112">The Azure SDK for Python wraps the [Azure Service Management API][svc-mgmt-rest-api], which is a REST API.</span></span> <span data-ttu-id="46f5c-113">所有 API 作業都會透過 SSL 而執行，並可使用 X.509 v3 憑證相互驗證。</span><span class="sxs-lookup"><span data-stu-id="46f5c-113">All API operations are performed over SSL and mutually authenticated using X.509 v3 certificates.</span></span> <span data-ttu-id="46f5c-114">管理服務可從執行於 Azure 的服務內存取，或直接透過網際網路，從任何可傳送 HTTPS 要求和接收 HTTPS 回應的應用程式存取。</span><span class="sxs-lookup"><span data-stu-id="46f5c-114">The management service may be accessed from within a service running in Azure, or directly over the Internet from any application that can send an HTTPS request and receive an HTTPS response.</span></span>

## <span data-ttu-id="46f5c-115"><a name="Installation"> </a>安裝</span><span class="sxs-lookup"><span data-stu-id="46f5c-115"><a name="Installation"> </a>Installation</span></span>
<span data-ttu-id="46f5c-116">本文中所述的所有功能都可在 `azure-servicemanagement-legacy` 封裝中找到，您可以使用 pip 來安裝此封裝。</span><span class="sxs-lookup"><span data-stu-id="46f5c-116">All the features described in this article are available in the `azure-servicemanagement-legacy` package, which you can install using pip.</span></span> <span data-ttu-id="46f5c-117">如需安裝 (例如，若您不熟悉 Python) 的詳細資訊，請參閱此文章︰[安裝 Python 和 Azure SDK](../python-how-to-install.md)</span><span class="sxs-lookup"><span data-stu-id="46f5c-117">For more information about installation (for example, if you are new to Python), see this article: [Installing Python and the Azure SDK](../python-how-to-install.md)</span></span>

## <span data-ttu-id="46f5c-118"><a name="Connect"> </a>作法：連線到服務管理</span><span class="sxs-lookup"><span data-stu-id="46f5c-118"><a name="Connect"> </a>How to: Connect to service management</span></span>
<span data-ttu-id="46f5c-119">若要連接到服務管理端點，您必須具備 Azure 訂用帳戶 ID 和有效的管理憑證。</span><span class="sxs-lookup"><span data-stu-id="46f5c-119">To connect to the Service Management endpoint, you need your Azure subscription ID and a valid management certificate.</span></span> <span data-ttu-id="46f5c-120">您可以透過 [Azure 傳統入口網站][management-portal]取得訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="46f5c-120">You can obtain your subscription ID through the [Azure classic portal][management-portal].</span></span>

> [!NOTE]
> <span data-ttu-id="46f5c-121">目前在 Windows 上執行時，可以使用以 OpenSSL 建立的憑證。</span><span class="sxs-lookup"><span data-stu-id="46f5c-121">It is now possible to use certificates created with OpenSSL when running on Windows.</span></span>  <span data-ttu-id="46f5c-122">這需要使用 Python 2.7.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="46f5c-122">It requires Python 2.7.4 or later.</span></span> <span data-ttu-id="46f5c-123">建議使用者使用 OpenSSL 而非 .pfx，因為未來可能會移除 .pfx 憑證的支援。</span><span class="sxs-lookup"><span data-stu-id="46f5c-123">We recommend users to use OpenSSL instead of .pfx, since support for .pfx certificates will likely be removed in the future.</span></span>
>
>

### <a name="management-certificates-on-windowsmaclinux-openssl"></a><span data-ttu-id="46f5c-124">Windows/Mac/Linux 上的管理憑證 (OpenSSL)</span><span class="sxs-lookup"><span data-stu-id="46f5c-124">Management certificates on Windows/Mac/Linux (OpenSSL)</span></span>
<span data-ttu-id="46f5c-125">您可以使用 [OpenSSL](http://www.openssl.org/) 建立管理憑證。</span><span class="sxs-lookup"><span data-stu-id="46f5c-125">You can use [OpenSSL](http://www.openssl.org/) to create your management certificate.</span></span>  <span data-ttu-id="46f5c-126">實際上您需要建立兩個憑證，一個用於伺服器 (`.cer` 檔案)，一個用於用戶端 (`.pem` 檔案)。</span><span class="sxs-lookup"><span data-stu-id="46f5c-126">You actually need to create two certificates, one for the server (a `.cer` file) and one for the client (a `.pem` file).</span></span> <span data-ttu-id="46f5c-127">若要建立 `.pem` 檔案，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="46f5c-127">To create the `.pem` file, execute:</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="46f5c-128">若要建立 `.cer` 憑證，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="46f5c-128">To create the `.cer` certificate, execute:</span></span>

    openssl x509 -inform pem -in mycert.pem -outform der -out mycert.cer

<span data-ttu-id="46f5c-129">如需有關 Azure 憑證的詳細資訊，請參閱 [Azure 雲端服務的憑證概觀](cloud-services-certs-create.md)。</span><span class="sxs-lookup"><span data-stu-id="46f5c-129">For more information about Azure certificates, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="46f5c-130">如需 OpenSSL 參數的完整說明，請參閱 [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html)上的文件。</span><span class="sxs-lookup"><span data-stu-id="46f5c-130">For a complete description of OpenSSL parameters, see the documentation at [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span></span>

<span data-ttu-id="46f5c-131">建立這些檔案之後，您必須透過 [Azure 傳統入口網站][management-portal]中 [設定] 索引標籤的 [上傳] 動作，將 `.cer` 檔案上傳至 Azure，且必須記下儲存 `.pem` 檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="46f5c-131">After you have created these files, you need to upload the `.cer` file to Azure via the "Upload" action of the "Settings" tab of the [Azure classic portal][management-portal], and you need to make note of where you saved the `.pem` file.</span></span>

<span data-ttu-id="46f5c-132">取得訂用帳戶識別碼、建立憑證，並將 `.cer` 檔案上傳至 Azure 之後，您可以將訂用帳戶識別碼和 `.pem` 檔案的路徑傳送至 **ServiceManagementService**，以連接到 Azure 管理端點：</span><span class="sxs-lookup"><span data-stu-id="46f5c-132">After you have obtained your subscription ID, created a certificate, and uploaded the `.cer` file to Azure, you can connect to the Azure management endpoint by passing the subscription id and the path to the `.pem` file to **ServiceManagementService**:</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = '<path_to_.pem_certificate>'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="46f5c-133">在上一個範例中， `sms` 是 **ServiceManagementService** 物件。</span><span class="sxs-lookup"><span data-stu-id="46f5c-133">In the preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="46f5c-134">**ServiceManagementService** 類別是用來管理 Azure 服務的主要類別。</span><span class="sxs-lookup"><span data-stu-id="46f5c-134">The **ServiceManagementService** class is the primary class used to manage Azure services.</span></span>

### <a name="management-certificates-on-windows-makecert"></a><span data-ttu-id="46f5c-135">Windows 上的管理憑證 (MakeCert)</span><span class="sxs-lookup"><span data-stu-id="46f5c-135">Management certificates on Windows (MakeCert)</span></span>
<span data-ttu-id="46f5c-136">您可以使用 `makecert.exe`，在您的機器上建立自我簽署管理憑證。</span><span class="sxs-lookup"><span data-stu-id="46f5c-136">You can create a self-signed management certificate on your machine using `makecert.exe`.</span></span>  <span data-ttu-id="46f5c-137">請以**系統管理員**的身分開啟 **Visual Studio 命令提示字元**，並使用下列命令 (將 AzureCertificate 取代為您要使用的憑證名稱)。</span><span class="sxs-lookup"><span data-stu-id="46f5c-137">Open a **Visual Studio command prompt** as an **administrator** and use the following command, replacing *AzureCertificate* with the certificate name you would like to use.</span></span>

    makecert -sky exchange -r -n "CN=AzureCertificate" -pe -a sha1 -len 2048 -ss My "AzureCertificate.cer"

<span data-ttu-id="46f5c-138">此命令會建立 `.cer` 檔案，並將其安裝在 [個人] 憑證存放區中。</span><span class="sxs-lookup"><span data-stu-id="46f5c-138">The command creates the `.cer` file, and installs it in the **Personal** certificate store.</span></span> <span data-ttu-id="46f5c-139">如需詳細資訊，請參閱 [Azure 雲端服務的憑證概觀](cloud-services-certs-create.md)。</span><span class="sxs-lookup"><span data-stu-id="46f5c-139">For more information, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span>

<span data-ttu-id="46f5c-140">建立憑證之後，您必須透過 [Azure 傳統入口網站][management-portal]中 [設定] 索引標籤的 [上傳] 動作，將 `.cer` 檔案上傳至 Azure。</span><span class="sxs-lookup"><span data-stu-id="46f5c-140">After you have created the certificate, you need to upload the `.cer` file to Azure via the "Upload" action of the "Settings" tab of the [Azure classic portal][management-portal].</span></span>

<span data-ttu-id="46f5c-141">取得訂用帳戶識別碼、建立憑證，並將 `.cer` 檔案上傳至 Azure 之後，您可以將訂用帳戶識別碼和 [個人] 憑證存放區中的憑證位置傳送至 **ServiceManagementService**，以連接到 Azure 管理端點 (同樣地，使用您的憑證名稱來取代 *AzureCertificate*)：</span><span class="sxs-lookup"><span data-stu-id="46f5c-141">After you have obtained your subscription ID, created a certificate, and uploaded the `.cer` file to Azure, you can connect to the Azure management endpoint by passing the subscription id and the location of the certificate in your **Personal** certificate store to **ServiceManagementService** (again, replace *AzureCertificate* with the name of your certificate):</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = 'CURRENT_USER\\my\\AzureCertificate'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="46f5c-142">在上一個範例中， `sms` 是 **ServiceManagementService** 物件。</span><span class="sxs-lookup"><span data-stu-id="46f5c-142">In the preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="46f5c-143">**ServiceManagementService** 類別是用來管理 Azure 服務的主要類別。</span><span class="sxs-lookup"><span data-stu-id="46f5c-143">The **ServiceManagementService** class is the primary class used to manage Azure services.</span></span>

## <span data-ttu-id="46f5c-144"><a name="ListAvailableLocations"> </a>作法：列出可用位置</span><span class="sxs-lookup"><span data-stu-id="46f5c-144"><a name="ListAvailableLocations"> </a>How to: List available locations</span></span>
<span data-ttu-id="46f5c-145">若要列出可用來託管服務的位置，請使用 **list\_locations** 方法：</span><span class="sxs-lookup"><span data-stu-id="46f5c-145">To list the locations that are available for hosting services, use the **list\_locations** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_locations()
    for location in result:
        print(location.name)

<span data-ttu-id="46f5c-146">在建立雲端服務或儲存體服務時，您必須提供有效的位置。</span><span class="sxs-lookup"><span data-stu-id="46f5c-146">When you create a cloud service or storage service you need to provide a valid location.</span></span> <span data-ttu-id="46f5c-147">**list\_locations** 方法一律會傳回目前可用位置的最新清單。</span><span class="sxs-lookup"><span data-stu-id="46f5c-147">The **list\_locations** method always returns an up-to-date list of the currently available locations.</span></span> <span data-ttu-id="46f5c-148">截至本文撰寫時間為止，可用位置如下：</span><span class="sxs-lookup"><span data-stu-id="46f5c-148">As of this writing, the available locations are:</span></span>

* <span data-ttu-id="46f5c-149">西歐</span><span class="sxs-lookup"><span data-stu-id="46f5c-149">West Europe</span></span>
* <span data-ttu-id="46f5c-150">北歐</span><span class="sxs-lookup"><span data-stu-id="46f5c-150">North Europe</span></span>
* <span data-ttu-id="46f5c-151">東南亞</span><span class="sxs-lookup"><span data-stu-id="46f5c-151">Southeast Asia</span></span>
* <span data-ttu-id="46f5c-152">東亞</span><span class="sxs-lookup"><span data-stu-id="46f5c-152">East Asia</span></span>
* <span data-ttu-id="46f5c-153">美國中部</span><span class="sxs-lookup"><span data-stu-id="46f5c-153">Central US</span></span>
* <span data-ttu-id="46f5c-154">美國中北部</span><span class="sxs-lookup"><span data-stu-id="46f5c-154">North Central US</span></span>
* <span data-ttu-id="46f5c-155">美國中南部</span><span class="sxs-lookup"><span data-stu-id="46f5c-155">South Central US</span></span>
* <span data-ttu-id="46f5c-156">美國西部</span><span class="sxs-lookup"><span data-stu-id="46f5c-156">West US</span></span>
* <span data-ttu-id="46f5c-157">美國東部</span><span class="sxs-lookup"><span data-stu-id="46f5c-157">East US</span></span>
* <span data-ttu-id="46f5c-158">日本東部</span><span class="sxs-lookup"><span data-stu-id="46f5c-158">Japan East</span></span>
* <span data-ttu-id="46f5c-159">日本西部</span><span class="sxs-lookup"><span data-stu-id="46f5c-159">Japan West</span></span>
* <span data-ttu-id="46f5c-160">巴西南部</span><span class="sxs-lookup"><span data-stu-id="46f5c-160">Brazil South</span></span>
* <span data-ttu-id="46f5c-161">澳洲東部</span><span class="sxs-lookup"><span data-stu-id="46f5c-161">Australia East</span></span>
* <span data-ttu-id="46f5c-162">澳大利亞東南部</span><span class="sxs-lookup"><span data-stu-id="46f5c-162">Australia Southeast</span></span>

## <span data-ttu-id="46f5c-163"><a name="CreateCloudService"> </a>作法：建立雲端服務</span><span class="sxs-lookup"><span data-stu-id="46f5c-163"><a name="CreateCloudService"> </a>How to: Create a cloud service</span></span>
<span data-ttu-id="46f5c-164">當您在 Azure 中建立應用程式並加以執行時，程式碼和組態會統稱為 Azure [雲端服務][cloud service] (在舊版的 Azure 中稱為*託管服務*)。</span><span class="sxs-lookup"><span data-stu-id="46f5c-164">When you create an application and run it in Azure, the code and configuration together are called an Azure [cloud service][cloud service] (known as a *hosted service* in earlier Azure releases).</span></span> <span data-ttu-id="46f5c-165">**create\_hosted\_service** 方法可讓您藉由提供託管服務名稱 (在 Azure 中必須是唯一的)、標籤 (自動編碼為 base64)、描述和位置，來建立新的託管服務。</span><span class="sxs-lookup"><span data-stu-id="46f5c-165">The **create\_hosted\_service** method allows you to create a new hosted service by providing a hosted service name (which must be unique in Azure), a label (automatically encoded to base64), a description, and a location.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myhostedservice'
    label = 'myhostedservice'
    desc = 'my hosted service'
    location = 'West US'

    sms.create_hosted_service(name, label, desc, location)

<span data-ttu-id="46f5c-166">您可以使用 **list\_hosted\_services** 方法，列出訂用帳戶的所有託管服務：</span><span class="sxs-lookup"><span data-stu-id="46f5c-166">You can list all the hosted services for your subscription with the **list\_hosted\_services** method:</span></span>

    result = sms.list_hosted_services()

    for hosted_service in result:
        print('Service name: ' + hosted_service.service_name)
        print('Management URL: ' + hosted_service.url)
        print('Location: ' + hosted_service.hosted_service_properties.location)
        print('')

<span data-ttu-id="46f5c-167">如果您想要取得特定託管服務的相關資訊，則可以將託管服務名稱傳遞給 **get\_hosted\_service\_properties** 方法：</span><span class="sxs-lookup"><span data-stu-id="46f5c-167">If you want to get information about a particular hosted service, you can do so by passing the hosted service name to the **get\_hosted\_service\_properties** method:</span></span>

    hosted_service = sms.get_hosted_service_properties('myhostedservice')

    print('Service name: ' + hosted_service.service_name)
    print('Management URL: ' + hosted_service.url)
    print('Location: ' + hosted_service.hosted_service_properties.location)

<span data-ttu-id="46f5c-168">在您建立雲端服務之後，就可以使用 **create\_deployment** 方法將程式碼部署至服務。</span><span class="sxs-lookup"><span data-stu-id="46f5c-168">After you have created a cloud service, you can deploy your code to the service with the **create\_deployment** method.</span></span>

## <span data-ttu-id="46f5c-169"><a name="DeleteCloudService"> </a>作法：刪除雲端服務</span><span class="sxs-lookup"><span data-stu-id="46f5c-169"><a name="DeleteCloudService"> </a>How to: Delete a cloud service</span></span>
<span data-ttu-id="46f5c-170">您可以將服務名稱傳遞給 **delete\_hosted\_service** 方法，以刪除雲端服務：</span><span class="sxs-lookup"><span data-stu-id="46f5c-170">You can delete a cloud service by passing the service name to the **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service('myhostedservice')

<span data-ttu-id="46f5c-171">您必須先刪除服務的所有部署，才能刪除該服務。</span><span class="sxs-lookup"><span data-stu-id="46f5c-171">Before you can delete a service, all deployments for the service must first be deleted.</span></span> <span data-ttu-id="46f5c-172">(請參閱 [作法：刪除部署](#DeleteDeployment) ，以取得詳細資料)。</span><span class="sxs-lookup"><span data-stu-id="46f5c-172">(See [How to: Delete a deployment](#DeleteDeployment) for details.)</span></span>

## <span data-ttu-id="46f5c-173"><a name="DeleteDeployment"> </a>作法：刪除部署</span><span class="sxs-lookup"><span data-stu-id="46f5c-173"><a name="DeleteDeployment"> </a>How to: Delete a deployment</span></span>
<span data-ttu-id="46f5c-174">若要刪除部署，請使用 **delete\_deployment** 方法。</span><span class="sxs-lookup"><span data-stu-id="46f5c-174">To delete a deployment, use the **delete\_deployment** method.</span></span> <span data-ttu-id="46f5c-175">下列範例示範如何刪除名為 `v1`的部署。</span><span class="sxs-lookup"><span data-stu-id="46f5c-175">The following example shows how to delete a deployment named `v1`.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment('myhostedservice', 'v1')

## <span data-ttu-id="46f5c-176"><a name="CreateStorageService"> </a>作法：建立儲存體服務</span><span class="sxs-lookup"><span data-stu-id="46f5c-176"><a name="CreateStorageService"> </a>How to: Create a storage service</span></span>
<span data-ttu-id="46f5c-177">[儲存體服務](../storage/common/storage-create-storage-account.md)可讓您存取 [Azure Blob](../storage/blobs/storage-python-how-to-use-blob-storage.md)、[資料表](../cosmos-db/table-storage-how-to-use-python.md)和[佇列](../storage/queues/storage-python-how-to-use-queue-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="46f5c-177">A [storage service](../storage/common/storage-create-storage-account.md) gives you access to Azure [Blobs](../storage/blobs/storage-python-how-to-use-blob-storage.md), [Tables](../cosmos-db/table-storage-how-to-use-python.md), and [Queues](../storage/queues/storage-python-how-to-use-queue-storage.md).</span></span> <span data-ttu-id="46f5c-178">若要建立儲存服務，您必須要有服務的名稱 (3 到 24 個小寫字元，且在 Azure 中是唯一的)、描述、標籤 (最多 100 個字元，會自動編碼為 base64)，以及位置。</span><span class="sxs-lookup"><span data-stu-id="46f5c-178">To create a storage service, you need a name for the service (between 3 and 24 lowercase characters and unique within Azure), a description, a label (up to 100 characters, automatically encoded to base64), and a location.</span></span> <span data-ttu-id="46f5c-179">下列範例說明如何藉由指定位置來建立儲存服務。</span><span class="sxs-lookup"><span data-stu-id="46f5c-179">The following example shows how to create a storage service by specifying a location.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mystorageaccount'
    label = 'mystorageaccount'
    location = 'West US'
    desc = 'My storage account description.'

    result = sms.create_storage_account(name, desc, label, location=location)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

<span data-ttu-id="46f5c-180">請注意，在上一個範例中，可將 **create\_storage\_account** 所傳回的結果傳至 **get\_operation\_status** 方法，以擷取 **create\_storage\_account** 作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="46f5c-180">Note in the preceding example that the status of the **create\_storage\_account** operation can be retrieved by passing the result returned by **create\_storage\_account** to the **get\_operation\_status** method.</span></span>  

<span data-ttu-id="46f5c-181">您可以使用 **list\_storage\_accounts** 方法列出您的儲存帳戶及其屬性：</span><span class="sxs-lookup"><span data-stu-id="46f5c-181">You can list your storage accounts and their properties with the **list\_storage\_accounts** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_storage_accounts()
    for account in result:
        print('Service name: ' + account.service_name)
        print('Location: ' + account.storage_service_properties.location)
        print('')

## <span data-ttu-id="46f5c-182"><a name="DeleteStorageService"> </a>作法：刪除儲存體服務</span><span class="sxs-lookup"><span data-stu-id="46f5c-182"><a name="DeleteStorageService"> </a>How to: Delete a storage service</span></span>
<span data-ttu-id="46f5c-183">您可以將儲存服務名稱傳至 **delete\_storage\_account** 方法，以刪除儲存服務。</span><span class="sxs-lookup"><span data-stu-id="46f5c-183">You can delete a storage service by passing the storage service name to the **delete\_storage\_account** method.</span></span> <span data-ttu-id="46f5c-184">如果刪除儲存體服務，則會刪除該服務中儲存的所有資料 (Blob、資料表和佇列)。</span><span class="sxs-lookup"><span data-stu-id="46f5c-184">Deleting a storage service deletes all data stored in the service (blobs, tables, and queues).</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_storage_account('mystorageaccount')

## <span data-ttu-id="46f5c-185"><a name="ListOperatingSystems"> </a>作法：列出可用作業系統</span><span class="sxs-lookup"><span data-stu-id="46f5c-185"><a name="ListOperatingSystems"> </a>How to: List available operating systems</span></span>
<span data-ttu-id="46f5c-186">若要列出可用來託管服務的作業系統，請使用 **list\_operating\_systems** 方法：</span><span class="sxs-lookup"><span data-stu-id="46f5c-186">To list the operating systems that are available for hosting services, use the **list\_operating\_systems** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_operating_systems()

    for os in result:
        print('OS: ' + os.label)
        print('Family: ' + os.family_label)
        print('Active: ' + str(os.is_active))

<span data-ttu-id="46f5c-187">或者，您可以使用 **list\_operating\_system\_families** 方法，以依系列將作業系統分組：</span><span class="sxs-lookup"><span data-stu-id="46f5c-187">Alternatively, you can use the **list\_operating\_system\_families** method, which groups the operating systems by family:</span></span>

    result = sms.list_operating_system_families()

    for family in result:
        print('Family: ' + family.label)
        for os in family.operating_systems:
            if os.is_active:
                print('OS: ' + os.label)
                print('Version: ' + os.version)
        print('')

## <span data-ttu-id="46f5c-188"><a name="CreateVMImage"> </a>作法：建立作業系統映像</span><span class="sxs-lookup"><span data-stu-id="46f5c-188"><a name="CreateVMImage"> </a>How to: Create an operating system image</span></span>
<span data-ttu-id="46f5c-189">若要將作業系統映像新增至映像儲存機制，請使用 **add\_os\_image** 方法：</span><span class="sxs-lookup"><span data-stu-id="46f5c-189">To add an operating system image to the image repository, use the **add\_os\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mycentos'
    label = 'mycentos'
    os = 'Linux' # Linux or Windows
    media_link = 'url_to_storage_blob_for_source_image_vhd'

    result = sms.add_os_image(label, media_link, name, os)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

<span data-ttu-id="46f5c-190">若要列出可用的作業系統映像，請使用 **list\_os\_images** 方法。</span><span class="sxs-lookup"><span data-stu-id="46f5c-190">To list the operating system images that are available, use the **list\_os\_images** method.</span></span> <span data-ttu-id="46f5c-191">其中包括所有的平台映像和使用者映像：</span><span class="sxs-lookup"><span data-stu-id="46f5c-191">It includes all platform images and user images:</span></span>

    result = sms.list_os_images()

    for image in result:
        print('Name: ' + image.name)
        print('Label: ' + image.label)
        print('OS: ' + image.os)
        print('Category: ' + image.category)
        print('Description: ' + image.description)
        print('Location: ' + image.location)
        print('Media link: ' + image.media_link)
        print('')

## <span data-ttu-id="46f5c-192"><a name="DeleteVMImage"> </a>作法：刪除作業系統映像</span><span class="sxs-lookup"><span data-stu-id="46f5c-192"><a name="DeleteVMImage"> </a>How to: Delete an operating system image</span></span>
<span data-ttu-id="46f5c-193">若要刪除使用者映像，請使用 **delete\_os\_image** 方法：</span><span class="sxs-lookup"><span data-stu-id="46f5c-193">To delete a user image, use the **delete\_os\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.delete_os_image('mycentos')

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

## <span data-ttu-id="46f5c-194"><a name="CreateVM"> </a>作法：建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="46f5c-194"><a name="CreateVM"> </a>How to: Create a virtual machine</span></span>
<span data-ttu-id="46f5c-195">若要建立虛擬機器，您必須先建立 [雲端服務](#CreateCloudService)。</span><span class="sxs-lookup"><span data-stu-id="46f5c-195">To create a virtual machine, you first need to create a [cloud service](#CreateCloudService).</span></span>  <span data-ttu-id="46f5c-196">接著，請使用 **create\_virtual\_machine\_deployment** 方法建立虛擬機器部署：</span><span class="sxs-lookup"><span data-stu-id="46f5c-196">Then create the virtual machine deployment using the **create\_virtual\_machine\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set the location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    # Name of an os image as returned by list_os_images
    image_name = 'OpenLogic__OpenLogic-CentOS-62-20120531-en-us-30GB.vhd'

    # Destination storage account container/blob where the VM disk
    # will be created
    media_link = 'url_to_target_storage_blob_for_vm_hd'

    # Linux VM configuration, you can use WindowsConfigurationSet
    # for a Windows VM instead
    linux_config = LinuxConfigurationSet('myhostname', 'myuser', 'mypassword', True)

    os_hd = OSVirtualHardDisk(image_name, media_link)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=os_hd,
        role_size='Small')

## <span data-ttu-id="46f5c-197"><a name="DeleteVM"> </a>作法：刪除虛擬機器</span><span class="sxs-lookup"><span data-stu-id="46f5c-197"><a name="DeleteVM"> </a>How to: Delete a virtual machine</span></span>
<span data-ttu-id="46f5c-198">若要刪除虛擬機器，您必須先使用 **delete\_deployment** 方法刪除部署：</span><span class="sxs-lookup"><span data-stu-id="46f5c-198">To delete a virtual machine, you first delete the deployment using the **delete\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment(service_name='myvm',
        deployment_name='myvm')

<span data-ttu-id="46f5c-199">接著可以使用 **delete\_hosted\_service** 方法刪除雲端服務：</span><span class="sxs-lookup"><span data-stu-id="46f5c-199">The cloud service can then be deleted using the **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service(service_name='myvm')

## <a name="how-to-create-a-virtual-machine-from-a-captured-virtual-machine-image"></a><span data-ttu-id="46f5c-200">作法：從擷取的虛擬機器映像建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="46f5c-200">How To: Create a Virtual Machine from a Captured Virtual Machine Image</span></span>
<span data-ttu-id="46f5c-201">若要擷取 VM 映像，請先呼叫 **capture\_vm\_image** 方法：</span><span class="sxs-lookup"><span data-stu-id="46f5c-201">To capture a VM image, you first call the **capture\_vm\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    # replace the below three parameters with actual values
    hosted_service_name = 'hs1'
    deployment_name = 'dep1'
    vm_name = 'vm1'

    image_name = vm_name + 'image'
    image = CaptureRoleAsVMImage    ('Specialized',
        image_name,
        image_name + 'label',
        image_name + 'description',
        'english',
        'mygroup')

    result = sms.capture_vm_image(
            hosted_service_name,
            deployment_name,
            vm_name,
            image
        )

<span data-ttu-id="46f5c-202">接著，若要確定您已成功擷取映像，請使用 **list\_vm\_images** api，並確定映像已顯示在結果中：</span><span class="sxs-lookup"><span data-stu-id="46f5c-202">Next, to make sure that you have successfully captured the image, use the **list\_vm\_images** api, and make sure your image is displayed in the results:</span></span>

    images = sms.list_vm_images()

<span data-ttu-id="46f5c-203">若最後要使用擷取的映像建立虛擬機器，請如同前面使用 **create\_virtual\_machine\_deployment** 方法，但這次改為傳入 vm_image_name</span><span class="sxs-lookup"><span data-stu-id="46f5c-203">To finally create the virtual machine using the captured image, use the **create\_virtual\_machine\_deployment** method as before, but this time pass in the vm_image_name instead</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set the location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=None,
        role_size='Small',
        vm_image_name = image_name)

<span data-ttu-id="46f5c-204">若要深入了解如何擷取 Linux 虛擬機器，請參閱[如何擷取 Linux 虛擬機器。](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="46f5c-204">To learn more about how to capture a Linux Virtual Machine, see [How to Capture a Linux Virtual Machine.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="46f5c-205">若要深入了解如何擷取 Windows 虛擬機器，請參閱[如何擷取 Windows 虛擬機器。](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="46f5c-205">To learn more about how to capture a Windows Virtual Machine, see [How to Capture a Windows Virtual Machine.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="46f5c-206"><a name="What's Next"> </a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="46f5c-206"><a name="What's Next"> </a>Next Steps</span></span>
<span data-ttu-id="46f5c-207">現在，您已了解服務管理的基本概念，您可以存取 [Azure Python SDK 的完整 API 參考文件](http://azure-sdk-for-python.readthedocs.org/) 並輕鬆執行複雜工作，以管理 Python 應用程式。</span><span class="sxs-lookup"><span data-stu-id="46f5c-207">Now that you've learned the basics of service management, you can access the [Complete API reference documentation for the Azure Python SDK](http://azure-sdk-for-python.readthedocs.org/) and perform complex tasks easily to manage your python application.</span></span>

<span data-ttu-id="46f5c-208">如需詳細資訊，請參閱 [Python 開發人員中心](/develop/python/)。</span><span class="sxs-lookup"><span data-stu-id="46f5c-208">For more information, see the [Python Developer Center](/develop/python/).</span></span>

[What is Service Management]: #WhatIs
[Concepts]: #Concepts
[How to: Connect to service management]: #Connect
[How to: List available locations]: #ListAvailableLocations
[How to: Create a cloud service]: #CreateCloudService
[How to: Delete a cloud service]: #DeleteCloudService
[How to: Create a deployment]: #CreateDeployment
[How to: Update a deployment]: #UpdateDeployment
[How to: Move deployments between staging and production]: #MoveDeployments
[How to: Delete a deployment]: #DeleteDeployment
[How to: Create a storage service]: #CreateStorageService
[How to: Delete a storage service]: #DeleteStorageService
[How to: List available operating systems]: #ListOperatingSystems
[How to: Create an operating system image]: #CreateVMImage
[How to: Delete an operating system image]: #DeleteVMImage
[How to: Create a virtual machine]: #CreateVM
[How to: Delete a virtual machine]: #DeleteVM
[Next Steps]: #NextSteps
[management-portal]: https://manage.windowsazure.com/
[svc-mgmt-rest-api]: http://msdn.microsoft.com/library/windowsazure/ee460799.aspx


[cloud service]:/services/cloud-services/
