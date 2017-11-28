---
title: "在 Azure 儲存體中使用共用存取簽章 (SAS) | Microsoft Docs"
description: "學習如何使用共用存取簽章 (SAS) 委派存取至 Azure 儲存體資源，包括 Blob、佇列、資料表及檔案。"
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 46fd99d7-36b3-4283-81e3-f214b29f1152
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/18/2017
ms.author: marsma
ms.openlocfilehash: a753fd481c9f91d94b6a2bd3633142e2dddedaec
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="using-shared-access-signatures-sas"></a><span data-ttu-id="668bf-103">使用共用存取簽章 (SAS)</span><span class="sxs-lookup"><span data-stu-id="668bf-103">Using shared access signatures (SAS)</span></span>

<span data-ttu-id="668bf-104">若要在無須提供您帳戶金鑰的情況下，將儲存體帳戶中物件的限制存取授與其他用戶端，則可使用共用存取簽章 (SAS) 達成此目標。</span><span class="sxs-lookup"><span data-stu-id="668bf-104">A shared access signature (SAS) provides you with a way to grant limited access to objects in your storage account to other clients, without exposing your account key.</span></span> <span data-ttu-id="668bf-105">本文會提供有關 SAS 模型的概觀、檢閱最佳做法以及查看一些範例。</span><span class="sxs-lookup"><span data-stu-id="668bf-105">In this article, we provide an overview of the SAS model, review SAS best practices, and look at some examples.</span></span>

<span data-ttu-id="668bf-106">除了本文所提供的範例外，如果您還需要其他使用 SAS 的程式碼範例，請參閱[在 .NET 中開始使用 Azure Blob 儲存體](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)和 [Azure 程式碼範例](https://azure.microsoft.com/documentation/samples/?service=storage)程式庫提供的其他範例。</span><span class="sxs-lookup"><span data-stu-id="668bf-106">For additional code examples using SAS beyond those presented here, see [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/) and other samples available in the [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?service=storage) library.</span></span> <span data-ttu-id="668bf-107">您可以下載範例應用程式並加以執行，或瀏覽 GitHub 上的程式碼。</span><span class="sxs-lookup"><span data-stu-id="668bf-107">You can download the sample applications and run them, or browse the code on GitHub.</span></span>

## <a name="what-is-a-shared-access-signature"></a><span data-ttu-id="668bf-108">共用存取簽章為何？</span><span class="sxs-lookup"><span data-stu-id="668bf-108">What is a shared access signature?</span></span>
<span data-ttu-id="668bf-109">共用存取簽章可提供您儲存體帳戶中資源的委派存取。</span><span class="sxs-lookup"><span data-stu-id="668bf-109">A shared access signature provides delegated access to resources in your storage account.</span></span> <span data-ttu-id="668bf-110">透過 SAS，您可以對用戶端授與儲存體帳戶中資源的存取權，而不必共用帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="668bf-110">With a SAS, you can grant clients access to resources in your storage account, without sharing your account keys.</span></span> <span data-ttu-id="668bf-111">這是在您應用程式中使用共用存取簽章的重點 - SAS 是共用儲存體資源的安全方式，而不會危害您的帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="668bf-111">This is the key point of using shared access signatures in your applications--a SAS is a secure way to share your storage resources without compromising your account keys.</span></span>

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

<span data-ttu-id="668bf-112">SAS 可讓您更細微地控制要對擁有 SAS 的用戶端授與何種類型的存取權，包括︰</span><span class="sxs-lookup"><span data-stu-id="668bf-112">A SAS gives you granular control over the type of access you grant to clients who have the SAS, including:</span></span>

* <span data-ttu-id="668bf-113">SAS 的有效期間，包括開始時間和到期時間。</span><span class="sxs-lookup"><span data-stu-id="668bf-113">The interval over which the SAS is valid, including the start time and the expiry time.</span></span>
* <span data-ttu-id="668bf-114">SAS 所授與的權限。</span><span class="sxs-lookup"><span data-stu-id="668bf-114">The permissions granted by the SAS.</span></span> <span data-ttu-id="668bf-115">例如，Blob 的 SAS 可能會授與該 Blob 的讀取和寫入權限，但不授與刪除權限。</span><span class="sxs-lookup"><span data-stu-id="668bf-115">For example, a SAS for a blob might grant read and write permissions to that blob, but not delete permissions.</span></span>
* <span data-ttu-id="668bf-116">Azure 儲存體接受的 SAS 所來自的選擇性 IP 位址或 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="668bf-116">An optional IP address or range of IP addresses from which Azure Storage will accept the SAS.</span></span> <span data-ttu-id="668bf-117">例如，您可以指定屬於組織的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="668bf-117">For example, you might specify a range of IP addresses belonging to your organization.</span></span>
* <span data-ttu-id="668bf-118">Azure 儲存體接受的 SAS 所透過的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="668bf-118">The protocol over which Azure Storage will accept the SAS.</span></span> <span data-ttu-id="668bf-119">您可以使用這個選擇性參數來限制使用 HTTPS 之用戶端的存取權。</span><span class="sxs-lookup"><span data-stu-id="668bf-119">You can use this optional parameter to restrict access to clients using HTTPS.</span></span>

## <a name="when-should-you-use-a-shared-access-signature"></a><span data-ttu-id="668bf-120">使用共用存取簽章的時機？</span><span class="sxs-lookup"><span data-stu-id="668bf-120">When should you use a shared access signature?</span></span>
<span data-ttu-id="668bf-121">當您想要將儲存體帳戶中的資源存取權提供給未具有您儲存體帳戶存取金鑰的用戶端時，即可使用 SAS。</span><span class="sxs-lookup"><span data-stu-id="668bf-121">You can use a SAS when you want to provide access to resources in your storage account to any client not possessing your storage account's access keys.</span></span> <span data-ttu-id="668bf-122">您的儲存體帳戶包含主要與次要存取金鑰，兩者皆可授與帳戶及帳戶內所有資源的系統管理存取權。</span><span class="sxs-lookup"><span data-stu-id="668bf-122">Your storage account includes both a primary and secondary access key, both of which grant administrative access to your account, and all resources within it.</span></span> <span data-ttu-id="668bf-123">提供以上任一金鑰，皆有可能讓您的帳戶遭到惡意或粗心使用。</span><span class="sxs-lookup"><span data-stu-id="668bf-123">Exposing either of these keys opens your account to the possibility of malicious or negligent use.</span></span> <span data-ttu-id="668bf-124">共用存取簽章提供了安全的替代方式，無需帳戶金鑰便可讓用戶端根據獲明確授與的權限，來讀取、寫入及刪除您儲存體帳戶中的資料。</span><span class="sxs-lookup"><span data-stu-id="668bf-124">Shared access signatures provide a safe alternative that allows clients to read, write, and delete data in your storage account according to the permissions you've explicitly granted, and without need for an account key.</span></span>

<span data-ttu-id="668bf-125">證明 SAS 非常有用的一個常見案例，就是使用者在您的儲存體帳戶中讀取和寫入自己的資料。</span><span class="sxs-lookup"><span data-stu-id="668bf-125">A common scenario where a SAS is useful is a service where users read and write their own data to your storage account.</span></span> <span data-ttu-id="668bf-126">在儲存體帳戶儲存使用者資料的案例中，典型的設計模式有兩種：</span><span class="sxs-lookup"><span data-stu-id="668bf-126">In a scenario where a storage account stores user data, there are two typical design patterns:</span></span>

1. <span data-ttu-id="668bf-127">用戶端通過前端 Proxy 服務 (執行驗證) 來上傳與下載資料。</span><span class="sxs-lookup"><span data-stu-id="668bf-127">Clients upload and download data via a front-end proxy service, which performs authentication.</span></span> <span data-ttu-id="668bf-128">此前端 Proxy 服務有個好處，那就是允許商務規則的驗證，但在大量資料或大量交易的情況下，建立可調整以符合需求的服務可能十分昂貴或困難。</span><span class="sxs-lookup"><span data-stu-id="668bf-128">This front-end proxy service has the advantage of allowing validation of business rules, but for large amounts of data or high-volume transactions, creating a service that can scale to match demand may be expensive or difficult.</span></span>

  ![案例圖表︰前端 Proxy 服務](./media/storage-dotnet-shared-access-signature-part-1/sas-storage-fe-proxy-service.png)   

1. <span data-ttu-id="668bf-130">輕量型服務可視需要驗證用戶端，然後產生 SAS。</span><span class="sxs-lookup"><span data-stu-id="668bf-130">A lightweight service authenticates the client as needed and then generates a SAS.</span></span> <span data-ttu-id="668bf-131">在用戶端收到 SAS 之後，他們可以使用 SAS 所定義的權限，並在 SAS 允許的間隔內直接存取儲存體帳戶資源。</span><span class="sxs-lookup"><span data-stu-id="668bf-131">Once the client receives the SAS, they can access storage account resources directly with the permissions defined by the SAS and for the interval allowed by the SAS.</span></span> <span data-ttu-id="668bf-132">SAS 可減輕透過前端 Proxy 服務路由所有資料的需求。</span><span class="sxs-lookup"><span data-stu-id="668bf-132">The SAS mitigates the need for routing all data through the front-end proxy service.</span></span>

  ![案例圖表︰SAS 提供者服務](./media/storage-dotnet-shared-access-signature-part-1/sas-storage-provider-service.png)   

<span data-ttu-id="668bf-134">許多實際服務可能會混合運用這兩種方法。</span><span class="sxs-lookup"><span data-stu-id="668bf-134">Many real-world services may use a hybrid of these two approaches.</span></span> <span data-ttu-id="668bf-135">例如，某些資料可能會透過前端 Proxy 處理和驗證，其他資料則會直接使用 SAS 來儲存和/或讀取。</span><span class="sxs-lookup"><span data-stu-id="668bf-135">For example, some data might be processed and validated via the front-end proxy, while other data is saved and/or read directly using SAS.</span></span>

<span data-ttu-id="668bf-136">此外，在某些情況下，您必須使用 SAS 來驗證複製作業中的來源物件：</span><span class="sxs-lookup"><span data-stu-id="668bf-136">Additionally, you will need to use a SAS to authenticate the source object in a copy operation in certain scenarios:</span></span>

* <span data-ttu-id="668bf-137">當您將 Blob 複製到另一個位於不同的儲存體帳戶的 Blob 時，您必須使用 SAS 來驗證來源 Blob。</span><span class="sxs-lookup"><span data-stu-id="668bf-137">When you copy a blob to another blob that resides in a different storage account, you must use a SAS to authenticate the source blob.</span></span> <span data-ttu-id="668bf-138">您亦可選擇使用 SAS 來驗證目的地 Blob。</span><span class="sxs-lookup"><span data-stu-id="668bf-138">You can optionally use a SAS to authenticate the destination blob as well.</span></span>
* <span data-ttu-id="668bf-139">當您將檔案複製到另一個位於不同儲存體帳戶的檔案時，您必須使用 SAS 來驗證來源檔案。</span><span class="sxs-lookup"><span data-stu-id="668bf-139">When you copy a file to another file that resides in a different storage account, you must use a SAS to authenticate the source file.</span></span> <span data-ttu-id="668bf-140">您亦可選擇使用 SAS 來驗證目的地檔案。</span><span class="sxs-lookup"><span data-stu-id="668bf-140">You can optionally use a SAS to authenticate the destination file as well.</span></span>
* <span data-ttu-id="668bf-141">當您將 Blob 複製到檔案，或將檔案複製到 Blob 時，您必須使用 SAS 來驗證來源物件，即使來源和目的地位於相同的儲存體帳戶內也一樣。</span><span class="sxs-lookup"><span data-stu-id="668bf-141">When you copy a blob to a file, or a file to a blob, you must use a SAS to authenticate the source object, even if the source and destination objects reside within the same storage account.</span></span>

## <a name="types-of-shared-access-signatures"></a><span data-ttu-id="668bf-142">共用存取簽章的類型</span><span class="sxs-lookup"><span data-stu-id="668bf-142">Types of shared access signatures</span></span>
<span data-ttu-id="668bf-143">您可建立兩種類型的共用存取簽章：</span><span class="sxs-lookup"><span data-stu-id="668bf-143">You can create two types of shared access signatures:</span></span>

* <span data-ttu-id="668bf-144">**服務 SAS。**</span><span class="sxs-lookup"><span data-stu-id="668bf-144">**Service SAS.**</span></span> <span data-ttu-id="668bf-145">服務 SAS 只會將存取權限委派給一種儲存體服務資源：Blob、佇列、資料表或檔案服務。</span><span class="sxs-lookup"><span data-stu-id="668bf-145">The service SAS delegates access to a resource in just one of the storage services: the Blob, Queue, Table, or File service.</span></span> <span data-ttu-id="668bf-146">如需有關建構服務 SAS 權杖的深入資訊，請參閱[建構服務 SAS](https://msdn.microsoft.com/library/dn140255.aspx) 和[服務 SAS 範例](https://msdn.microsoft.com/library/dn140256.aspx)。</span><span class="sxs-lookup"><span data-stu-id="668bf-146">See [Constructing a Service SAS](https://msdn.microsoft.com/library/dn140255.aspx) and [Service SAS Examples](https://msdn.microsoft.com/library/dn140256.aspx) for in-depth information about constructing the service SAS token.</span></span>
* <span data-ttu-id="668bf-147">**帳戶 SAS。**</span><span class="sxs-lookup"><span data-stu-id="668bf-147">**Account SAS.**</span></span> <span data-ttu-id="668bf-148">帳戶 SAS 則將存取權限委派給一或多個儲存體服務的資源。</span><span class="sxs-lookup"><span data-stu-id="668bf-148">The account SAS delegates access to resources in one or more of the storage services.</span></span> <span data-ttu-id="668bf-149">可透過服務 SAS 取得的所有作業也可透過帳戶 SAS 取得。</span><span class="sxs-lookup"><span data-stu-id="668bf-149">All of the operations available via a service SAS are also available via an account SAS.</span></span> <span data-ttu-id="668bf-150">此外，利用帳戶 SAS，您可以委派適用指定的服務作業 (例如：**取得/設定服務屬性**和**取得服務統計資料**) 的存取。您也可以將 Blob 容器、資料表、佇列和檔案共用的讀取、寫入和刪除作業的存取權限，委派給本無權限的服務 SAS。</span><span class="sxs-lookup"><span data-stu-id="668bf-150">Additionally, with the account SAS, you can delegate access to operations that apply to a given service, such as **Get/Set Service Properties** and **Get Service Stats**. You can also delegate access to read, write, and delete operations on blob containers, tables, queues, and file shares that are not permitted with a service SAS.</span></span> <span data-ttu-id="668bf-151">如需有關建構帳戶 SAS 權杖的深入資訊，請參閱[建構帳戶 SAS](https://msdn.microsoft.com/library/mt584140.aspx)。</span><span class="sxs-lookup"><span data-stu-id="668bf-151">See [Constructing an Account SAS](https://msdn.microsoft.com/library/mt584140.aspx) for in-depth information about constructing the account SAS token.</span></span>

## <a name="how-a-shared-access-signature-works"></a><span data-ttu-id="668bf-152">共用存取簽章的運作方式</span><span class="sxs-lookup"><span data-stu-id="668bf-152">How a shared access signature works</span></span>
<span data-ttu-id="668bf-153">共用存取簽章是指向一或多個儲存體資源，並包括含有一組特殊的查詢參數權杖的已簽署 URI。</span><span class="sxs-lookup"><span data-stu-id="668bf-153">A shared access signature is a signed URI that points to one or more storage resources and includes a token that contains a special set of query parameters.</span></span> <span data-ttu-id="668bf-154">權杖指出用戶端可以如何存取資源。</span><span class="sxs-lookup"><span data-stu-id="668bf-154">The token indicates how the resources may be accessed by the client.</span></span> <span data-ttu-id="668bf-155">簽章是查詢參數的其中一個，根據 SAS 參數所建構並使用帳戶金鑰進行簽署。</span><span class="sxs-lookup"><span data-stu-id="668bf-155">One of the query parameters, the signature, is constructed from the SAS parameters and signed with the account key.</span></span> <span data-ttu-id="668bf-156">Azure 儲存體會使用此簽章來驗證 SAS。</span><span class="sxs-lookup"><span data-stu-id="668bf-156">This signature is used by Azure Storage to authenticate the SAS.</span></span>

<span data-ttu-id="668bf-157">以下是 SAS URI 範例，其顯示資源 URI 和 SAS 權杖︰</span><span class="sxs-lookup"><span data-stu-id="668bf-157">Here's an example of a SAS URI, showing the resource URI and the SAS token:</span></span>

![SAS URI 的元件](./media/storage-dotnet-shared-access-signature-part-1/sas-storage-uri.png)   

<span data-ttu-id="668bf-159">SAS 權杖是*用戶端*所產生的字串 (如需程式碼範例，請參閱〈[SAS 範例](#sas-examples)〉一節)。</span><span class="sxs-lookup"><span data-stu-id="668bf-159">The SAS token is a string you generate on the *client* side (see the [SAS examples](#sas-examples) section for code examples).</span></span> <span data-ttu-id="668bf-160">譬如 Azure 儲存體不會以任何方式，追蹤您透過儲存體用戶端程式庫所產生的 SAS 權杖。</span><span class="sxs-lookup"><span data-stu-id="668bf-160">A SAS token you generate with the storage client library, for example, is not tracked by Azure Storage in any way.</span></span> <span data-ttu-id="668bf-161">您可以在用戶端建立不限數量的 SAS 權杖。</span><span class="sxs-lookup"><span data-stu-id="668bf-161">You can create an unlimited number of SAS tokens on the client side.</span></span>

<span data-ttu-id="668bf-162">當用戶端在要求中提供 SAS URI 給 Azure 儲存體時，服務會檢查 SAS 參數和簽章，以確認它是有效的，可用於驗證要求。</span><span class="sxs-lookup"><span data-stu-id="668bf-162">When a client provides a SAS URI to Azure Storage as part of a request, the service checks the SAS parameters and signature to verify that it is valid for authenticating the request.</span></span> <span data-ttu-id="668bf-163">如果服務確認簽章有效，則要求會通過驗證。</span><span class="sxs-lookup"><span data-stu-id="668bf-163">If the service verifies that the signature is valid, then the request is authenticated.</span></span> <span data-ttu-id="668bf-164">否則要求會遭到拒絕，並產生錯誤碼 403 (禁止)。</span><span class="sxs-lookup"><span data-stu-id="668bf-164">Otherwise, the request is declined with error code 403 (Forbidden).</span></span>

## <a name="shared-access-signature-parameters"></a><span data-ttu-id="668bf-165">共用存取簽章參數</span><span class="sxs-lookup"><span data-stu-id="668bf-165">Shared access signature parameters</span></span>
<span data-ttu-id="668bf-166">帳戶 SAS 和服務 SAS 權杖包含一些常見的參數，並且採取幾個不同參數。</span><span class="sxs-lookup"><span data-stu-id="668bf-166">The account SAS and service SAS tokens include some common parameters, and also take a few parameters that that are different.</span></span>

### <a name="parameters-common-to-account-sas-and-service-sas-tokens"></a><span data-ttu-id="668bf-167">帳戶 SAS 和服務 SAS 權杖的通用參數</span><span class="sxs-lookup"><span data-stu-id="668bf-167">Parameters common to account SAS and service SAS tokens</span></span>
* <span data-ttu-id="668bf-168">**API 版本** 選擇性參數，指定要用來執行要求的儲存體服務版本。</span><span class="sxs-lookup"><span data-stu-id="668bf-168">**Api version** An optional parameter that specifies the storage service version to use to execute the request.</span></span>
* <span data-ttu-id="668bf-169">**服務版本** 必要參數，指定要用於驗證要求的儲存體服務版本。</span><span class="sxs-lookup"><span data-stu-id="668bf-169">**Service version** A required parameter that specifies the storage service version to use to authenticate the request.</span></span>
* <span data-ttu-id="668bf-170">**開始時間。**</span><span class="sxs-lookup"><span data-stu-id="668bf-170">**Start time.**</span></span> <span data-ttu-id="668bf-171">這是指 SAS 生效的時間。</span><span class="sxs-lookup"><span data-stu-id="668bf-171">This is the time at which the SAS becomes valid.</span></span> <span data-ttu-id="668bf-172">共用存取簽章的開始時間為選擇性。</span><span class="sxs-lookup"><span data-stu-id="668bf-172">The start time for a shared access signature is optional.</span></span> <span data-ttu-id="668bf-173">若省略開始時間，SAS 便會立即生效。</span><span class="sxs-lookup"><span data-stu-id="668bf-173">If a start time is omitted, the SAS is effective immediately.</span></span> <span data-ttu-id="668bf-174">開始時間必須以 UTC (國際標準時間) 表示，並包含特殊的 UTC 指示項 ("Z")，例如 `1994-11-05T13:15:30Z`。</span><span class="sxs-lookup"><span data-stu-id="668bf-174">The start time must be expressed in UTC (Coordinated Universal Time), with a special UTC designator ("Z"), for example `1994-11-05T13:15:30Z`.</span></span>
* <span data-ttu-id="668bf-175">**到期時間。**</span><span class="sxs-lookup"><span data-stu-id="668bf-175">**Expiry time.**</span></span> <span data-ttu-id="668bf-176">這是指 SAS 何時失效的時間。</span><span class="sxs-lookup"><span data-stu-id="668bf-176">This is the time after which the SAS is no longer valid.</span></span> <span data-ttu-id="668bf-177">最佳做法建議您為 SAS 指定過期時間，或將它與預存存取原則建立關聯。</span><span class="sxs-lookup"><span data-stu-id="668bf-177">Best practices recommend that you either specify an expiry time for a SAS, or associate it with a stored access policy.</span></span> <span data-ttu-id="668bf-178">過期時間必須以 UTC (國際標準時間) 表示，並包含特殊的 UTC 指示項 ("Z")，例如 `1994-11-05T13:15:30Z` (參閱以下的更多資訊)。</span><span class="sxs-lookup"><span data-stu-id="668bf-178">The expiry time must be expressed in UTC (Coordinated Universal Time), with a special UTC designator ("Z"), for example `1994-11-05T13:15:30Z` (see more below).</span></span>
* <span data-ttu-id="668bf-179">**權限。**</span><span class="sxs-lookup"><span data-stu-id="668bf-179">**Permissions.**</span></span> <span data-ttu-id="668bf-180">在 SAS 上指定的權限表示用戶端可以使用 SAS 來對儲存體資源執行哪些作業。</span><span class="sxs-lookup"><span data-stu-id="668bf-180">The permissions specified on the SAS indicate what operations the client can perform against the storage resource using the SAS.</span></span> <span data-ttu-id="668bf-181">帳戶 SAS 和服務 SAS 的可用權限不同。</span><span class="sxs-lookup"><span data-stu-id="668bf-181">Available permissions differ for an account SAS and a service SAS.</span></span>
* <span data-ttu-id="668bf-182">**IP。**</span><span class="sxs-lookup"><span data-stu-id="668bf-182">**IP.**</span></span> <span data-ttu-id="668bf-183">選用參數，可指定要從中接受要求且位於 Azure 外部的 IP 位址或 IP 位址範圍 (請參閱適用於 Express Route 的 [路由工作階段組態狀態](../../expressroute/expressroute-workflows.md#routing-session-configuration-state) 一節)。</span><span class="sxs-lookup"><span data-stu-id="668bf-183">An optional parameter that specifies an IP address or a range of IP addresses outside of Azure (see the section [Routing session configuration state](../../expressroute/expressroute-workflows.md#routing-session-configuration-state) for Express Route) from which to accept requests.</span></span>
* <span data-ttu-id="668bf-184">**通訊協定。**</span><span class="sxs-lookup"><span data-stu-id="668bf-184">**Protocol.**</span></span> <span data-ttu-id="668bf-185">選擇性參數，指定對要求允許的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="668bf-185">An optional parameter that specifies the protocol permitted for a request.</span></span> <span data-ttu-id="668bf-186">可能的值為 HTTPS 和 HTTP (`https,http`)，其為預設值或僅限 HTTPS (`https`)。</span><span class="sxs-lookup"><span data-stu-id="668bf-186">Possible values are both HTTPS and HTTP (`https,http`), which is the default value, or HTTPS only (`https`).</span></span> <span data-ttu-id="668bf-187">請注意，僅 HTTP 是不允許的值。</span><span class="sxs-lookup"><span data-stu-id="668bf-187">Note that HTTP only is not a permitted value.</span></span>
* <span data-ttu-id="668bf-188">**簽章。**</span><span class="sxs-lookup"><span data-stu-id="668bf-188">**Signature.**</span></span> <span data-ttu-id="668bf-189">簽章是從其他參數建構，指定為權杖的一部分，然後加密。</span><span class="sxs-lookup"><span data-stu-id="668bf-189">The signature is constructed from the other parameters specified as part token and then encrypted.</span></span> <span data-ttu-id="668bf-190">它是用來驗證 SAS。</span><span class="sxs-lookup"><span data-stu-id="668bf-190">It's used to authenticate the SAS.</span></span>

### <a name="parameters-for-a-service-sas-token"></a><span data-ttu-id="668bf-191">服務 SAS 權杖的參數</span><span class="sxs-lookup"><span data-stu-id="668bf-191">Parameters for a service SAS token</span></span>
* <span data-ttu-id="668bf-192">**儲存體資源。**</span><span class="sxs-lookup"><span data-stu-id="668bf-192">**Storage resource.**</span></span> <span data-ttu-id="668bf-193">可以委派對服務 SAS 存取的儲存體資源包括：</span><span class="sxs-lookup"><span data-stu-id="668bf-193">Storage resources for which you can delegate access with a service SAS include:</span></span>
  * <span data-ttu-id="668bf-194">容器和 Blob</span><span class="sxs-lookup"><span data-stu-id="668bf-194">Containers and blobs</span></span>
  * <span data-ttu-id="668bf-195">檔案共用及檔案</span><span class="sxs-lookup"><span data-stu-id="668bf-195">File shares and files</span></span>
  * <span data-ttu-id="668bf-196">佇列</span><span class="sxs-lookup"><span data-stu-id="668bf-196">Queues</span></span>
  * <span data-ttu-id="668bf-197">資料表和資料表實體範圍。</span><span class="sxs-lookup"><span data-stu-id="668bf-197">Tables and ranges of table entities.</span></span>

### <a name="parameters-for-an-account-sas-token"></a><span data-ttu-id="668bf-198">帳戶 SAS 權杖的參數</span><span class="sxs-lookup"><span data-stu-id="668bf-198">Parameters for an account SAS token</span></span>
* <span data-ttu-id="668bf-199">**一或多個服務。**</span><span class="sxs-lookup"><span data-stu-id="668bf-199">**Service or services.**</span></span> <span data-ttu-id="668bf-200">帳戶 SAS 可以委派存取給一或多個儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="668bf-200">An account SAS can delegate access to one or more of the storage services.</span></span> <span data-ttu-id="668bf-201">例如，您可以建立委派存取 Blob 和檔案服務的帳戶 SAS。</span><span class="sxs-lookup"><span data-stu-id="668bf-201">For example, you can create an account SAS that delegates access to the Blob and File service.</span></span> <span data-ttu-id="668bf-202">或者您可以建立委派存取給全部四個服務 (Blob、佇列、表格和檔案) 的 SAS。</span><span class="sxs-lookup"><span data-stu-id="668bf-202">Or you can create a SAS that delegates access to all four services (Blob, Queue, Table, and File).</span></span>
* <span data-ttu-id="668bf-203">**儲存體資源類型。**</span><span class="sxs-lookup"><span data-stu-id="668bf-203">**Storage resource types.**</span></span> <span data-ttu-id="668bf-204">帳戶 SAS 適用於一或多個類別的儲存體資源，而不是特定資源。</span><span class="sxs-lookup"><span data-stu-id="668bf-204">An account SAS applies to one or more classes of storage resources, rather than a specific resource.</span></span> <span data-ttu-id="668bf-205">您可以建立帳戶 SAS 來委派存取給：</span><span class="sxs-lookup"><span data-stu-id="668bf-205">You can create an account SAS to delegate access to:</span></span>
  * <span data-ttu-id="668bf-206">對儲存體帳戶資源呼叫的服務層級 API。</span><span class="sxs-lookup"><span data-stu-id="668bf-206">Service-level APIs, which are called against the storage account resource.</span></span> <span data-ttu-id="668bf-207">範例包括**取得/設定服務屬性**、**取得服務統計資料**和**列出容器/佇列/資料表/共用**。</span><span class="sxs-lookup"><span data-stu-id="668bf-207">Examples include **Get/Set Service Properties**, **Get Service Stats**, and **List Containers/Queues/Tables/Shares**.</span></span>
  * <span data-ttu-id="668bf-208">容器層級 API，會針對每個服務的容器物件呼叫：Blob 容器、佇列、資料表和檔案共用。</span><span class="sxs-lookup"><span data-stu-id="668bf-208">Container-level APIs, which are called against the container objects for each service: blob containers, queues, tables, and file shares.</span></span> <span data-ttu-id="668bf-209">範例包括**建立/刪除容器**、**建立/刪除佇列**、**建立/刪除資料表**、**建立/刪除共用**和**列出 Blob/檔案和目錄**。</span><span class="sxs-lookup"><span data-stu-id="668bf-209">Examples include **Create/Delete Container**, **Create/Delete Queue**, **Create/Delete Table**, **Create/Delete Share**, and **List Blobs/Files and Directories**.</span></span>
  * <span data-ttu-id="668bf-210">物件層級 API，針對 Blob、佇列訊息、資料表實體和檔案呼叫。</span><span class="sxs-lookup"><span data-stu-id="668bf-210">Object-level APIs, which are called against blobs, queue messages, table entities, and files.</span></span> <span data-ttu-id="668bf-211">例如，**放置 Blob**、**查詢實體**、**取得訊息**和**建立檔案**。</span><span class="sxs-lookup"><span data-stu-id="668bf-211">For example, **Put Blob**, **Query Entity**, **Get Messages**, and **Create File**.</span></span>

## <a name="examples-of-sas-uris"></a><span data-ttu-id="668bf-212">SAS URI 的範例</span><span class="sxs-lookup"><span data-stu-id="668bf-212">Examples of SAS URIs</span></span>

### <a name="service-sas-uri-example"></a><span data-ttu-id="668bf-213">服務 SAS URI 範例</span><span class="sxs-lookup"><span data-stu-id="668bf-213">Service SAS URI example</span></span>

<span data-ttu-id="668bf-214">以下是提供讀取和寫入 Blob 權限的服務 SAS URI 範例。</span><span class="sxs-lookup"><span data-stu-id="668bf-214">Here is an example of a service SAS URI that provides read and write permissions to a blob.</span></span> <span data-ttu-id="668bf-215">此資料表會細分 URI 的每一部分，以了解它會如何影響 SAS：</span><span class="sxs-lookup"><span data-stu-id="668bf-215">The table breaks down each part of the URI to understand how it contributes to the SAS:</span></span>

```
https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2015-04-05&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D
```

| <span data-ttu-id="668bf-216">名稱</span><span class="sxs-lookup"><span data-stu-id="668bf-216">Name</span></span> | <span data-ttu-id="668bf-217">SAS 部分</span><span class="sxs-lookup"><span data-stu-id="668bf-217">SAS portion</span></span> | <span data-ttu-id="668bf-218">說明</span><span class="sxs-lookup"><span data-stu-id="668bf-218">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="668bf-219">Blob URI</span><span class="sxs-lookup"><span data-stu-id="668bf-219">Blob URI</span></span> |`https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt` |<span data-ttu-id="668bf-220">Blob 的位址。</span><span class="sxs-lookup"><span data-stu-id="668bf-220">The address of the blob.</span></span> <span data-ttu-id="668bf-221">請注意，我們強烈建議您使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="668bf-221">Note that using HTTPS is highly recommended.</span></span> |
| <span data-ttu-id="668bf-222">儲存體服務版本</span><span class="sxs-lookup"><span data-stu-id="668bf-222">Storage services version</span></span> |`sv=2015-04-05` |<span data-ttu-id="668bf-223">若是儲存體服務版本 2012-02-12 和更新版本，此參數表示要使用的版本。</span><span class="sxs-lookup"><span data-stu-id="668bf-223">For storage services version 2012-02-12 and later, this parameter indicates the version to use.</span></span> |
| <span data-ttu-id="668bf-224">開始時間</span><span class="sxs-lookup"><span data-stu-id="668bf-224">Start time</span></span> |`st=2015-04-29T22%3A18%3A26Z` |<span data-ttu-id="668bf-225">以 UTC 時間指定。</span><span class="sxs-lookup"><span data-stu-id="668bf-225">Specified in UTC time.</span></span> <span data-ttu-id="668bf-226">如果您想要 SAS 立即生效，請略過開始時間。</span><span class="sxs-lookup"><span data-stu-id="668bf-226">If you want the SAS to be valid immediately, omit the start time.</span></span> |
| <span data-ttu-id="668bf-227">過期時間</span><span class="sxs-lookup"><span data-stu-id="668bf-227">Expiry time</span></span> |`se=2015-04-30T02%3A23%3A26Z` |<span data-ttu-id="668bf-228">以 UTC 時間指定。</span><span class="sxs-lookup"><span data-stu-id="668bf-228">Specified in UTC time.</span></span> |
| <span data-ttu-id="668bf-229">資源</span><span class="sxs-lookup"><span data-stu-id="668bf-229">Resource</span></span> |`sr=b` |<span data-ttu-id="668bf-230">此資源是 Blob。</span><span class="sxs-lookup"><span data-stu-id="668bf-230">The resource is a blob.</span></span> |
| <span data-ttu-id="668bf-231">權限</span><span class="sxs-lookup"><span data-stu-id="668bf-231">Permissions</span></span> |`sp=rw` |<span data-ttu-id="668bf-232">SAS 所授與的權限包括讀取 (r) 和寫入 (w)。</span><span class="sxs-lookup"><span data-stu-id="668bf-232">The permissions granted by the SAS include Read (r) and Write (w).</span></span> |
| <span data-ttu-id="668bf-233">IP 範圍</span><span class="sxs-lookup"><span data-stu-id="668bf-233">IP range</span></span> |`sip=168.1.5.60-168.1.5.70` |<span data-ttu-id="668bf-234">將從中接受要求的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="668bf-234">The range of IP addresses from which a request will be accepted.</span></span> |
| <span data-ttu-id="668bf-235">通訊協定</span><span class="sxs-lookup"><span data-stu-id="668bf-235">Protocol</span></span> |`spr=https` |<span data-ttu-id="668bf-236">僅允許使用 HTTPS 的要求。</span><span class="sxs-lookup"><span data-stu-id="668bf-236">Only requests using HTTPS are permitted.</span></span> |
| <span data-ttu-id="668bf-237">簽章</span><span class="sxs-lookup"><span data-stu-id="668bf-237">Signature</span></span> |`sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D` |<span data-ttu-id="668bf-238">用來驗證對 Blob 的存取權。</span><span class="sxs-lookup"><span data-stu-id="668bf-238">Used to authenticate access to the blob.</span></span> <span data-ttu-id="668bf-239">此簽章是 HMAC 根據要簽署字串和金鑰，使用 SHA256 演算法進行計算，然後使用 Base64 方式進行編碼而來的。</span><span class="sxs-lookup"><span data-stu-id="668bf-239">The signature is an HMAC computed over a string-to-sign and key using the SHA256 algorithm, and then encoded using Base64 encoding.</span></span> |

### <a name="account-sas-uri-example"></a><span data-ttu-id="668bf-240">帳戶 SAS URI 範例</span><span class="sxs-lookup"><span data-stu-id="668bf-240">Account SAS URI example</span></span>

<span data-ttu-id="668bf-241">以下是對權杖使用相同通用參數的帳戶 SAS 範例。</span><span class="sxs-lookup"><span data-stu-id="668bf-241">Here is an example of an account SAS that uses the same common parameters on the token.</span></span> <span data-ttu-id="668bf-242">由於上面說明了這些參數，在此處將不說明。</span><span class="sxs-lookup"><span data-stu-id="668bf-242">Since these parameters are described above, they are not described here.</span></span> <span data-ttu-id="668bf-243">下表只會說明帳戶 SAS 的特定參數。</span><span class="sxs-lookup"><span data-stu-id="668bf-243">Only the parameters that are specific to account SAS are described in the table below.</span></span>

```
https://myaccount.blob.core.windows.net/?restype=service&comp=properties&sv=2015-04-05&ss=bf&srt=s&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=F%6GRVAZ5Cdj2Pw4tgU7IlSTkWgn7bUkkAg8P6HESXwmf%4B
```

| <span data-ttu-id="668bf-244">名稱</span><span class="sxs-lookup"><span data-stu-id="668bf-244">Name</span></span> | <span data-ttu-id="668bf-245">SAS 部分</span><span class="sxs-lookup"><span data-stu-id="668bf-245">SAS portion</span></span> | <span data-ttu-id="668bf-246">說明</span><span class="sxs-lookup"><span data-stu-id="668bf-246">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="668bf-247">資源 URI</span><span class="sxs-lookup"><span data-stu-id="668bf-247">Resource URI</span></span> |`https://myaccount.blob.core.windows.net/?restype=service&comp=properties` |<span data-ttu-id="668bf-248">Blob 服務端點，具有用來取得服務屬性 (使用 GET 呼叫時) 或設定服務屬性 (使用 SET 呼叫時) 的參數。</span><span class="sxs-lookup"><span data-stu-id="668bf-248">The Blob service endpoint, with parameters for getting service properties (when called with GET) or setting service properties (when called with SET).</span></span> |
| <span data-ttu-id="668bf-249">服務</span><span class="sxs-lookup"><span data-stu-id="668bf-249">Services</span></span> |`ss=bf` |<span data-ttu-id="668bf-250">SAS 適用於 Blob 和檔案服務</span><span class="sxs-lookup"><span data-stu-id="668bf-250">The SAS applies to the Blob and File services</span></span> |
| <span data-ttu-id="668bf-251">資源類型</span><span class="sxs-lookup"><span data-stu-id="668bf-251">Resource types</span></span> |`srt=s` |<span data-ttu-id="668bf-252">SAS 適用於服務層級的作業。</span><span class="sxs-lookup"><span data-stu-id="668bf-252">The SAS applies to service-level operations.</span></span> |
| <span data-ttu-id="668bf-253">權限</span><span class="sxs-lookup"><span data-stu-id="668bf-253">Permissions</span></span> |`sp=rw` |<span data-ttu-id="668bf-254">此權限可授與讀取和寫入作業的存取權。</span><span class="sxs-lookup"><span data-stu-id="668bf-254">The permissions grant access to read and write operations.</span></span> |

<span data-ttu-id="668bf-255">假設權限僅限於服務層級，此 SAS 可存取的作業是**取得 Blob 服務屬性** (讀取) 和**設定 Blob 服務屬性** (寫入)。</span><span class="sxs-lookup"><span data-stu-id="668bf-255">Given that permissions are restricted to the service level, accessible operations with this SAS are **Get Blob Service Properties** (read) and **Set Blob Service Properties** (write).</span></span> <span data-ttu-id="668bf-256">不過，利用不同的資源 URI，相同的 SAS 權杖也可以用來委派存取給 **取得 Blob 服務統計資料** (讀取)。</span><span class="sxs-lookup"><span data-stu-id="668bf-256">However, with a different resource URI, the same SAS token could also be used to delegate access to **Get Blob Service Stats** (read).</span></span>

## <a name="controlling-a-sas-with-a-stored-access-policy"></a><span data-ttu-id="668bf-257">使用預存存取原則控制 SAS</span><span class="sxs-lookup"><span data-stu-id="668bf-257">Controlling a SAS with a stored access policy</span></span>
<span data-ttu-id="668bf-258">共用存取簽章可以接受以下兩種格式其中之一：</span><span class="sxs-lookup"><span data-stu-id="668bf-258">A shared access signature can take one of two forms:</span></span>

* <span data-ttu-id="668bf-259">**臨機操作 SAS：** 建立臨機操作 SAS 時，SAS 的開始時間、過期時間和權限都會在 SAS URI 上進行指定 (或暗示，在此情況下則會略過開始時間)。</span><span class="sxs-lookup"><span data-stu-id="668bf-259">**Ad hoc SAS:** When you create an ad hoc SAS, the start time, expiry time, and permissions for the SAS are all specified in the SAS URI (or implied, in the case where start time is omitted).</span></span> <span data-ttu-id="668bf-260">這種類型的 SAS 可能會建立為帳戶 SAS 或服務 SAS。</span><span class="sxs-lookup"><span data-stu-id="668bf-260">This type of SAS can be created as an account SAS or a service SAS.</span></span>
* <span data-ttu-id="668bf-261">**具有預存存取原則的 SAS：** 預存存取原則會在資源容器 (Blob 容器、資料表、佇列或檔案共用) 中定義，且可用來管理一或多個共用存取簽章的限制。</span><span class="sxs-lookup"><span data-stu-id="668bf-261">**SAS with stored access policy:** A stored access policy is defined on a resource container--a blob container, table, queue, or file share--and can be used to manage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="668bf-262">當您將 SAS 與預存存取原則建立關聯時，SAS 會繼承為該預存存取原則所定義的限制 (開始時間、過期時間和權限)。</span><span class="sxs-lookup"><span data-stu-id="668bf-262">When you associate a SAS with a stored access policy, the SAS inherits the constraints--the start time, expiry time, and permissions--defined for the stored access policy.</span></span>

> [!NOTE]
> <span data-ttu-id="668bf-263">目前，帳戶 SAS 必須是臨機操作 SAS。</span><span class="sxs-lookup"><span data-stu-id="668bf-263">Currently, an account SAS must be an ad hoc SAS.</span></span> <span data-ttu-id="668bf-264">帳戶 SAS 尚不支援預存的存取原則。</span><span class="sxs-lookup"><span data-stu-id="668bf-264">Stored access policies are not yet supported for account SAS.</span></span>

<span data-ttu-id="668bf-265">這兩種格式間的差異對於以下這一個重要案例而言相當重要：撤銷。</span><span class="sxs-lookup"><span data-stu-id="668bf-265">The difference between the two forms is important for one key scenario: revocation.</span></span> <span data-ttu-id="668bf-266">SAS URI 為 URL，因此無論其原始建立者為何，任何人只要取得 SAS 即可自由使用。</span><span class="sxs-lookup"><span data-stu-id="668bf-266">Because a SAS URI is a URL, anyone that obtains the SAS can use it, regardless of who originally created it.</span></span> <span data-ttu-id="668bf-267">如果是公開發佈 SAS，則全世界的人都可以使用此 SAS。</span><span class="sxs-lookup"><span data-stu-id="668bf-267">If a SAS is published publicly, it can be used by anyone in the world.</span></span> <span data-ttu-id="668bf-268">除非發生下述四種情況之一，否則 SAS 會將資源存取權授與具有 SAS 的任何人：</span><span class="sxs-lookup"><span data-stu-id="668bf-268">A SAS grants access to resources to anyone possessing it until one of four things happens:</span></span>

1. <span data-ttu-id="668bf-269">已到達 SAS 上指定的過期時間。</span><span class="sxs-lookup"><span data-stu-id="668bf-269">The expiry time specified on the SAS is reached.</span></span>
2. <span data-ttu-id="668bf-270">已到達在 SAS 所參考之預存存取原則上所指定的過期時間 (如果參考的是預存存取原則，而且如果此預存存取原則指定了過期時間)。</span><span class="sxs-lookup"><span data-stu-id="668bf-270">The expiry time specified on the stored access policy referenced by the SAS is reached (if a stored access policy is referenced, and if it specifies an expiry time).</span></span> <span data-ttu-id="668bf-271">發生此情況的原因，有可能是因為已超過指定的間隔時間，或是因為您已修改預存存取原則，將過期時間設定為過去的日期，這是撤銷 SAS 的一種方法。</span><span class="sxs-lookup"><span data-stu-id="668bf-271">This can occur either because the interval elapses, or because you've modified the stored access policy with an expiry time in the past, which is one way to revoke the SAS.</span></span>
3. <span data-ttu-id="668bf-272">已刪除 SAS 所參考之預存存取原則，這是撤銷 SAS 的另外一種方法。</span><span class="sxs-lookup"><span data-stu-id="668bf-272">The stored access policy referenced by the SAS is deleted, which is another way to revoke the SAS.</span></span> <span data-ttu-id="668bf-273">請注意，如果您使用完全相同的名稱來重新建立預存存取原則，則現有的所有 SAS 權杖會根據與該預存存取原則有關的權限再次有效 (假設 SAS 上的過期時間尚未過去)。</span><span class="sxs-lookup"><span data-stu-id="668bf-273">Note that if you recreate the stored access policy with exactly the same name, all existing SAS tokens will again be valid according to the permissions associated with that stored access policy (assuming that the expiry time on the SAS has not passed).</span></span> <span data-ttu-id="668bf-274">如果您打算撤銷 SAS，且如果您要使用未來的過期時間來重新建立存取原則，則務必使用不同的名稱。</span><span class="sxs-lookup"><span data-stu-id="668bf-274">If you are intending to revoke the SAS, be sure to use a different name if you recreate the access policy with an expiry time in the future.</span></span>
4. <span data-ttu-id="668bf-275">系統會重新產生用來建立 SAS 的帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="668bf-275">The account key that was used to create the SAS is regenerated.</span></span> <span data-ttu-id="668bf-276">重新產生帳戶金鑰將會導致所有使用該金鑰的應用程式元件無法進行驗證，直到他們已更新為使用其他有效帳戶金鑰或重新產生帳戶金鑰為止。</span><span class="sxs-lookup"><span data-stu-id="668bf-276">Regenerating an account key will cause all application components using that key to fail to authenticate until they're updated to use either the other valid account key or the newly regenerated account key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="668bf-277">共用存取簽章 URI 會與用來建立簽章的帳戶金鑰，以及相關聯的預存的存取原則 (如果有的話) 產生關聯。</span><span class="sxs-lookup"><span data-stu-id="668bf-277">A shared access signature URI is associated with the account key used to create the signature, and the associated stored access policy (if any).</span></span> <span data-ttu-id="668bf-278">如果未指定任何預存的存取原則，則撤銷共用存取簽章的唯一方式是變更帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="668bf-278">If no stored access policy is specified, the only way to revoke a shared access signature is to change the account key.</span></span>

## <a name="authenticating-from-a-client-application-with-a-sas"></a><span data-ttu-id="668bf-279">使用 SAS 從用戶端應用程式進行驗證</span><span class="sxs-lookup"><span data-stu-id="668bf-279">Authenticating from a client application with a SAS</span></span>
<span data-ttu-id="668bf-280">擁有 SAS 的用戶端，可以使用 SAS 來對他們未擁有帳戶金鑰的儲存體帳戶驗證要求。</span><span class="sxs-lookup"><span data-stu-id="668bf-280">A client who is in possession of a SAS can use the SAS to authenticate a request against a storage account for which they do not possess the account keys.</span></span> <span data-ttu-id="668bf-281">SAS 可以包含在連接字串，或直接從適當的建構函式或方法來使用。</span><span class="sxs-lookup"><span data-stu-id="668bf-281">A SAS can be included in a connection string, or used directly from the appropriate constructor or method.</span></span>

### <a name="using-a-sas-in-a-connection-string"></a><span data-ttu-id="668bf-282">在連接字串中使用 SAS</span><span class="sxs-lookup"><span data-stu-id="668bf-282">Using a SAS in a connection string</span></span>
[!INCLUDE [storage-use-sas-in-connection-string-include](../../../includes/storage-use-sas-in-connection-string-include.md)]

### <a name="using-a-sas-in-a-constructor-or-method"></a><span data-ttu-id="668bf-283">在建構函式或方法中使用 SAS</span><span class="sxs-lookup"><span data-stu-id="668bf-283">Using a SAS in a constructor or method</span></span>
<span data-ttu-id="668bf-284">數個 Azure 儲存體用戶端程式庫的建構函式和方法多載會提供 SAS 參數，以便您使用 SAS 來驗證對服務的要求。</span><span class="sxs-lookup"><span data-stu-id="668bf-284">Several Azure Storage client library constructors and method overloads offer a SAS parameter, so that you can authenticate a request to the service with a SAS.</span></span>

<span data-ttu-id="668bf-285">例如，這裡便使用 SAS URI 來建立區塊 Blob 的參考。</span><span class="sxs-lookup"><span data-stu-id="668bf-285">For example, here a SAS URI is used to create a reference to a block blob.</span></span> <span data-ttu-id="668bf-286">SAS 提供要求所需的唯一認證。</span><span class="sxs-lookup"><span data-stu-id="668bf-286">The SAS provides the only credentials needed for the request.</span></span> <span data-ttu-id="668bf-287">區塊 Blob 參考接著會用來進行寫入作業︰</span><span class="sxs-lookup"><span data-stu-id="668bf-287">The block blob reference is then used for a write operation:</span></span>

```csharp
string sasUri = "https://storagesample.blob.core.windows.net/sample-container/" +
    "sampleBlob.txt?sv=2015-07-08&sr=b&sig=39Up9JzHkxhUIhFEjEH9594DJxe7w6cIRCg0V6lCGSo%3D" +
    "&se=2016-10-18T21%3A51%3A37Z&sp=rcw";

CloudBlockBlob blob = new CloudBlockBlob(new Uri(sasUri));

// Create operation: Upload a blob with the specified name to the container.
// If the blob does not exist, it will be created. If it does exist, it will be overwritten.
try
{
    MemoryStream msWrite = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    msWrite.Position = 0;
    using (msWrite)
    {
        await blob.UploadFromStreamAsync(msWrite);
    }

    Console.WriteLine("Create operation succeeded for SAS {0}", sasUri);
    Console.WriteLine();
}
catch (StorageException e)
{
    if (e.RequestInformation.HttpStatusCode == 403)
    {
        Console.WriteLine("Create operation failed for SAS {0}", sasUri);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
    else
    {
        Console.WriteLine(e.Message);
        Console.ReadLine();
        throw;
    }
}

```

## <a name="best-practices-when-using-sas"></a><span data-ttu-id="668bf-288">使用 SAS 時的最佳做法</span><span class="sxs-lookup"><span data-stu-id="668bf-288">Best practices when using SAS</span></span>
<span data-ttu-id="668bf-289">當您在應用程式中使用共用存取簽章時，您必須留意兩個潛在風險：</span><span class="sxs-lookup"><span data-stu-id="668bf-289">When you use shared access signatures in your applications, you need to be aware of two potential risks:</span></span>

* <span data-ttu-id="668bf-290">如果 SAS 洩漏出去，則取得該 SAS 的任何人都可以使用它，這有可能會洩露您的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="668bf-290">If a SAS is leaked, it can be used by anyone who obtains it, which can potentially compromise your storage account.</span></span>
* <span data-ttu-id="668bf-291">如果提供給用戶端應用程式的 SAS 已過期，且此應用程式無法從您的服務擷取新的 SAS，那麼該應用程式的功能可能會受到影響。</span><span class="sxs-lookup"><span data-stu-id="668bf-291">If a SAS provided to a client application expires and the application is unable to retrieve a new SAS from your service, then the application's functionality may be hindered.</span></span>

<span data-ttu-id="668bf-292">下列關於使用共用存取簽章的建議，將可協助您平衡這些風險：</span><span class="sxs-lookup"><span data-stu-id="668bf-292">The following recommendations for using shared access signatures can help mitigate these risks:</span></span>

1. <span data-ttu-id="668bf-293">**永遠使用 HTTPS** 來建立或散佈 SAS。</span><span class="sxs-lookup"><span data-stu-id="668bf-293">**Always use HTTPS** to create or distribute a SAS.</span></span> <span data-ttu-id="668bf-294">若透過 HTTP 來傳遞 SAS 並遭到攔截，執行攔截式攻擊的攻擊者即可讀取並使用 SAS (就如同預期使用者執行般)，這有可能會洩露敏感資料或允許惡意使用者損毀資料。</span><span class="sxs-lookup"><span data-stu-id="668bf-294">If a SAS is passed over HTTP and intercepted, an attacker performing a man-in-the-middle attack is able to read the SAS and then use it just as the intended user could have, potentially compromising sensitive data or allowing for data corruption by the malicious user.</span></span>
2. <span data-ttu-id="668bf-295">**可能的話，參考預存存取原則。**</span><span class="sxs-lookup"><span data-stu-id="668bf-295">**Reference stored access policies where possible.**</span></span> <span data-ttu-id="668bf-296">預存存取原則提供了撤銷權限且無需重新產生儲存體帳戶金鑰的選項。</span><span class="sxs-lookup"><span data-stu-id="668bf-296">Stored access policies give you the option to revoke permissions without having to regenerate the storage account keys.</span></span> <span data-ttu-id="668bf-297">將到期日設在未來 (或無限) 的日期，並確定定期更新到期日以將到期日再往未來的日期移動。</span><span class="sxs-lookup"><span data-stu-id="668bf-297">Set the expiration on these very far in the future (or infinite) and make sure it's regularly updated to move it farther into the future.</span></span>
3. <span data-ttu-id="668bf-298">**在臨機操作 SAS 上使用短期的到期時間。**</span><span class="sxs-lookup"><span data-stu-id="668bf-298">**Use near-term expiration times on an ad hoc SAS.**</span></span> <span data-ttu-id="668bf-299">如此一來，即使 SAS 遭到入侵，亦僅會造成短期影響。</span><span class="sxs-lookup"><span data-stu-id="668bf-299">In this way, even if a SAS is compromised, it's valid only for a short time.</span></span> <span data-ttu-id="668bf-300">如果您無法參考預存存取原則，此做法格外重要。</span><span class="sxs-lookup"><span data-stu-id="668bf-300">This practice is especially important if you cannot reference a stored access policy.</span></span> <span data-ttu-id="668bf-301">短期到期時間亦可協助限制可寫入 Blob 的資料量，方法是限制可對其上傳的可用時間。</span><span class="sxs-lookup"><span data-stu-id="668bf-301">Near-term expiration times also limit the amount of data that can be written to a blob by limiting the time available to upload to it.</span></span>
4. <span data-ttu-id="668bf-302">**讓用戶端視需要自動更新 SAS。**</span><span class="sxs-lookup"><span data-stu-id="668bf-302">**Have clients automatically renew the SAS if necessary.**</span></span> <span data-ttu-id="668bf-303">用戶端應在到期日之前就更新 SAS，以便如果提供 SAS 的服務無法使用的話，還有時間可以進行重試。</span><span class="sxs-lookup"><span data-stu-id="668bf-303">Clients should renew the SAS well before the expiration, in order to allow time for retries if the service providing the SAS is unavailable.</span></span> <span data-ttu-id="668bf-304">如果您打算將 SAS 用於少量的即時短期操作 (預計可在到期期限內完成的操作)，則此建議可能沒有必要，因為沒有更新 SAS 的打算。</span><span class="sxs-lookup"><span data-stu-id="668bf-304">If your SAS is meant to be used for a small number of immediate, short-lived operations that are expected to be completed within the expiration period, then this may be unnecessary as the SAS is not expected to be renewed.</span></span> <span data-ttu-id="668bf-305">不過，如果您有定期透過 SAS 做出要求的用戶端，則到期的可能性便有可能發生。</span><span class="sxs-lookup"><span data-stu-id="668bf-305">However, if you have client that is routinely making requests via SAS, then the possibility of expiration comes into play.</span></span> <span data-ttu-id="668bf-306">主要考量是要平衡下列兩個需求：短期的 SAS (如先前所述)，與確保用戶端提早要求更新以避免成功更新之前因 SAS 過期而中斷。</span><span class="sxs-lookup"><span data-stu-id="668bf-306">The key consideration is to balance the need for the SAS to be short-lived (as previously stated) with the need to ensure that the client is requesting renewal early enough (to avoid disruption due to the SAS expiring prior to successful renewal).</span></span>
5. <span data-ttu-id="668bf-307">**請小心使用 SAS 開始時間。**</span><span class="sxs-lookup"><span data-stu-id="668bf-307">**Be careful with SAS start time.**</span></span> <span data-ttu-id="668bf-308">如果您將 SAS 的開始時間設為 [現在]，則由於時鐘誤差 (根據不同機器會有不同的目前時間)，前幾分鐘可能偶爾會被視為失敗。</span><span class="sxs-lookup"><span data-stu-id="668bf-308">If you set the start time for a SAS to **now**, then due to clock skew (differences in current time according to different machines), failures may be observed intermittently for the first few minutes.</span></span> <span data-ttu-id="668bf-309">一般而言，請將開始時間設為至少 15 分鐘之前的時間。</span><span class="sxs-lookup"><span data-stu-id="668bf-309">In general, set the start time to be at least 15 minutes in the past.</span></span> <span data-ttu-id="668bf-310">或是不進行任何設定，這會針對所有案例立即生效。</span><span class="sxs-lookup"><span data-stu-id="668bf-310">Or, don't set it at all, which will make it valid immediately in all cases.</span></span> <span data-ttu-id="668bf-311">同樣的道理通常亦適用於過期時間，請記住，您可針對任何要求保留前後多達 15 分鐘的時鐘誤差。</span><span class="sxs-lookup"><span data-stu-id="668bf-311">The same generally applies to expiry time as well--remember that you may observe up to 15 minutes of clock skew in either direction on any request.</span></span> <span data-ttu-id="668bf-312">若是用戶端使用 2012-02-12 之前的 REST 版本，則不參考預存存取原則之 SAS 的最大持續期限是 1 個小時，且任何指定比 1 個小時還要長的原則都會失敗。</span><span class="sxs-lookup"><span data-stu-id="668bf-312">For clients using a REST version prior to 2012-02-12, the maximum duration for a SAS that does not reference a stored access policy is 1 hour, and any policies specifying longer term than that will fail.</span></span>
6. <span data-ttu-id="668bf-313">**請具體指出要存取的資源。**</span><span class="sxs-lookup"><span data-stu-id="668bf-313">**Be specific with the resource to be accessed.**</span></span> <span data-ttu-id="668bf-314">安全性最佳做法是提供使用者最低需求權限。</span><span class="sxs-lookup"><span data-stu-id="668bf-314">A security best practice is to provide a user with the minimum required privileges.</span></span> <span data-ttu-id="668bf-315">如果使用者只需要單一實體的讀取存取權，則授與他們該單一實體的讀取存取權，而非授與他們所有實體的讀取/寫入/刪除存取權。</span><span class="sxs-lookup"><span data-stu-id="668bf-315">If a user only needs read access to a single entity, then grant them read access to that single entity, and not read/write/delete access to all entities.</span></span> <span data-ttu-id="668bf-316">這有助於減輕洩露 SAS 遭受的損害，因為當 SAS 落入攻擊者手中時，即無法發揮固有功能。</span><span class="sxs-lookup"><span data-stu-id="668bf-316">This also helps lessen the damage if a SAS is compromised because the SAS has less power in the hands of an attacker.</span></span>
7. <span data-ttu-id="668bf-317">**了解您帳戶的任何方式將會被收取費用，包括以 SAS 方式完成的部分。**</span><span class="sxs-lookup"><span data-stu-id="668bf-317">**Understand that your account will be billed for any usage, including that done with SAS.**</span></span> <span data-ttu-id="668bf-318">如果您提供 Blob 的寫入存取權，則使用者可能會選擇上傳 200GB 的 Blob。</span><span class="sxs-lookup"><span data-stu-id="668bf-318">If you provide write access to a blob, a user may choose to upload a 200GB blob.</span></span> <span data-ttu-id="668bf-319">若您也同時提供使用者讀取存取權，則他們可能會選擇下載 10 次，而您便會產生 2TB 的出口成本。</span><span class="sxs-lookup"><span data-stu-id="668bf-319">If you've given them read access as well, they may choose to download it 10 times, incurring 2 TB in egress costs for you.</span></span> <span data-ttu-id="668bf-320">再次強調，提供有限的權限有助於減少惡意使用者採取的潛在動作。</span><span class="sxs-lookup"><span data-stu-id="668bf-320">Again, provide limited permissions to help mitigate the potential actions of malicious users.</span></span> <span data-ttu-id="668bf-321">使用短期 SAS 以降低此威脅 (但請注意結束時間的時鐘誤差)。</span><span class="sxs-lookup"><span data-stu-id="668bf-321">Use short-lived SAS to reduce this threat (but be mindful of clock skew on the end time).</span></span>
8. <span data-ttu-id="668bf-322">**使用 SAS 驗證寫入資料。**</span><span class="sxs-lookup"><span data-stu-id="668bf-322">**Validate data written using SAS.**</span></span> <span data-ttu-id="668bf-323">當用戶端應用程式將資料寫入您的儲存體帳戶時，請留意該資料可能會造成問題。</span><span class="sxs-lookup"><span data-stu-id="668bf-323">When a client application writes data to your storage account, keep in mind that there can be problems with that data.</span></span> <span data-ttu-id="668bf-324">如果您的應用程式要求在開始使用資料之前先驗證或授權資料，則您應在寫入資料之後但應用程式尚未開始使用資料之前執行此驗證。</span><span class="sxs-lookup"><span data-stu-id="668bf-324">If your application requires that that data be validated or authorized before it is ready to use, you should perform this validation after the data is written and before it is used by your application.</span></span> <span data-ttu-id="668bf-325">此做法也可防止正確取得 SAS 的使用者或是利用洩漏 SAS 的使用者，損毀資料或將惡意資料寫入您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="668bf-325">This practice also protects against corrupt or malicious data being written to your account, either by a user who properly acquired the SAS, or by a user exploiting a leaked SAS.</span></span>
9. <span data-ttu-id="668bf-326">**請勿一直使用 SAS。**</span><span class="sxs-lookup"><span data-stu-id="668bf-326">**Don't always use SAS.**</span></span> <span data-ttu-id="668bf-327">有時候，在儲存體帳戶中執行特定作業的相關風險可能大過 SAS 的好處。</span><span class="sxs-lookup"><span data-stu-id="668bf-327">Sometimes the risks associated with a particular operation against your storage account outweigh the benefits of SAS.</span></span> <span data-ttu-id="668bf-328">針對此類作業，請建立一個中介層服務，在執行商務規則驗證、驗證及稽核之後才寫入您的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="668bf-328">For such operations, create a middle-tier service that writes to your storage account after performing business rule validation, authentication, and auditing.</span></span> <span data-ttu-id="668bf-329">另外，有時候以其他方式管理存取權可能比較簡單。</span><span class="sxs-lookup"><span data-stu-id="668bf-329">Also, sometimes it's simpler to manage access in other ways.</span></span> <span data-ttu-id="668bf-330">例如，如果您要讓容器中的所有 Blob 都可公開讀取，則您可以將此容器設定為 [公用]，而不是將 SAS 提供給每個用戶端進行存取。</span><span class="sxs-lookup"><span data-stu-id="668bf-330">For example, if you want to make all blobs in a container publically readable, you can make the container Public, rather than providing a SAS to every client for access.</span></span>
10. <span data-ttu-id="668bf-331">**使用儲存體分析來監視您的應用程式。**</span><span class="sxs-lookup"><span data-stu-id="668bf-331">**Use Storage Analytics to monitor your application.**</span></span> <span data-ttu-id="668bf-332">您可以使用記錄和度量來觀察由於 SAS 提供者服務中斷或不小心移除預存存取原則，而造成的任何驗證失敗急劇增加。</span><span class="sxs-lookup"><span data-stu-id="668bf-332">You can use logging and metrics to observe any spike in authentication failures due to an outage in your SAS provider service or to the inadvertent removal of a stored access policy.</span></span> <span data-ttu-id="668bf-333">如需額外資訊，請參閱 [Azure 儲存體團隊部落格](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx) (英文)。</span><span class="sxs-lookup"><span data-stu-id="668bf-333">See the [Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx) for additional information.</span></span>

## <a name="sas-examples"></a><span data-ttu-id="668bf-334">SAS 範例</span><span class="sxs-lookup"><span data-stu-id="668bf-334">SAS examples</span></span>
<span data-ttu-id="668bf-335">下面是兩種類型共用存取簽章 (帳戶 SAS 和服務 SAS) 的一些範例。</span><span class="sxs-lookup"><span data-stu-id="668bf-335">Below are some examples of both types of shared access signatures, account SAS and service SAS.</span></span>

<span data-ttu-id="668bf-336">若要執行這些 C# 範例，您必須參考專案中的下列 NuGet 封裝︰</span><span class="sxs-lookup"><span data-stu-id="668bf-336">To run these C# examples, you need to reference the following NuGet packages in your project:</span></span>

* <span data-ttu-id="668bf-337">[Azure Storage Client Library for .NET](http://www.nuget.org/packages/WindowsAzure.Storage)，版本 6.x 或更高版本 (以使用 帳戶 SAS)。</span><span class="sxs-lookup"><span data-stu-id="668bf-337">[Azure Storage Client Library for .NET](http://www.nuget.org/packages/WindowsAzure.Storage), version 6.x or later (to use account SAS).</span></span>
* [<span data-ttu-id="668bf-338">Azure 資源管理員</span><span class="sxs-lookup"><span data-stu-id="668bf-338">Azure Configuration Manager</span></span>](http://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager)

<span data-ttu-id="668bf-339">如需其他範例，示範如何建立及測試 SAS，請參閱 [Azure 儲存體的程式碼範例](https://azure.microsoft.com/documentation/samples/?service=storage)。</span><span class="sxs-lookup"><span data-stu-id="668bf-339">For additional examples that show how to create and test a SAS, see [Azure Code Samples for Storage](https://azure.microsoft.com/documentation/samples/?service=storage).</span></span>

### <a name="example-create-and-use-an-account-sas"></a><span data-ttu-id="668bf-340">範例︰建立和使用帳戶 SAS</span><span class="sxs-lookup"><span data-stu-id="668bf-340">Example: Create and use an account SAS</span></span>
<span data-ttu-id="668bf-341">下列程式碼範例會建立適用於 Blob 和檔案服務的帳戶 SAS，並提供用戶端權限讀取、寫入和列出權限來存取服務層級 API。</span><span class="sxs-lookup"><span data-stu-id="668bf-341">The following code example creates an account SAS that is valid for the Blob and File services, and gives the client permissions read, write, and list permissions to access service-level APIs.</span></span> <span data-ttu-id="668bf-342">帳戶 SAS 會將通訊協定限制為 HTTPS，因此必須使用 HTTPS 提出要求。</span><span class="sxs-lookup"><span data-stu-id="668bf-342">The account SAS restricts the protocol to HTTPS, so the request must be made with HTTPS.</span></span>

```csharp
static string GetAccountSASToken()
{
    // To create the account SAS, you need to use your shared key credentials. Modify for your account.
    const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

    // Create a new access policy for the account.
    SharedAccessAccountPolicy policy = new SharedAccessAccountPolicy()
        {
            Permissions = SharedAccessAccountPermissions.Read | SharedAccessAccountPermissions.Write | SharedAccessAccountPermissions.List,
            Services = SharedAccessAccountServices.Blob | SharedAccessAccountServices.File,
            ResourceTypes = SharedAccessAccountResourceTypes.Service,
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Protocols = SharedAccessProtocol.HttpsOnly
        };

    // Return the SAS token.
    return storageAccount.GetSharedAccessSignature(policy);
}
```

<span data-ttu-id="668bf-343">若要使用 帳戶 SAS 來存取 Blob 服務的服務層級 API，請使用 SAS 及儲存體帳戶的 Blob 儲存體端點來建構 Blob 用戶端物件。</span><span class="sxs-lookup"><span data-stu-id="668bf-343">To use the account SAS to access service-level APIs for the Blob service, construct a Blob client object using the SAS and the Blob storage endpoint for your storage account.</span></span>

```csharp
static void UseAccountSAS(string sasToken)
{
    // Create new storage credentials using the SAS token.
    StorageCredentials accountSAS = new StorageCredentials(sasToken);
    // Use these credentials and the account name to create a Blob service client.
    CloudStorageAccount accountWithSAS = new CloudStorageAccount(accountSAS, "account-name", endpointSuffix: null, useHttps: true);
    CloudBlobClient blobClientWithSAS = accountWithSAS.CreateCloudBlobClient();

    // Now set the service properties for the Blob client created with the SAS.
    blobClientWithSAS.SetServiceProperties(new ServiceProperties()
    {
        HourMetrics = new MetricsProperties()
        {
            MetricsLevel = MetricsLevel.ServiceAndApi,
            RetentionDays = 7,
            Version = "1.0"
        },
        MinuteMetrics = new MetricsProperties()
        {
            MetricsLevel = MetricsLevel.ServiceAndApi,
            RetentionDays = 7,
            Version = "1.0"
        },
        Logging = new LoggingProperties()
        {
            LoggingOperations = LoggingOperations.All,
            RetentionDays = 14,
            Version = "1.0"
        }
    });

    // The permissions granted by the account SAS also permit you to retrieve service properties.
    ServiceProperties serviceProperties = blobClientWithSAS.GetServiceProperties();
    Console.WriteLine(serviceProperties.HourMetrics.MetricsLevel);
    Console.WriteLine(serviceProperties.HourMetrics.RetentionDays);
    Console.WriteLine(serviceProperties.HourMetrics.Version);
}
```

### <a name="example-create-a-stored-access-policy"></a><span data-ttu-id="668bf-344">範例：建立預存的存取原則</span><span class="sxs-lookup"><span data-stu-id="668bf-344">Example: Create a stored access policy</span></span>
<span data-ttu-id="668bf-345">下列程式碼會在容器上建立預存的存取原則。</span><span class="sxs-lookup"><span data-stu-id="668bf-345">The following code creates a stored access policy on a container.</span></span> <span data-ttu-id="668bf-346">您可以使用存取原則，對於容器上的服務 SAS 或其 Blob 指定條件約束。</span><span class="sxs-lookup"><span data-stu-id="668bf-346">You can use the access policy to specify constraints for a service SAS on the container or its blobs.</span></span>

```csharp
private static async Task CreateSharedAccessPolicyAsync(CloudBlobContainer container, string policyName)
{
    // Create a new shared access policy and define its constraints.
    // The access policy provides create, write, read, list, and delete permissions.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        // When the start time for the SAS is omitted, the start time is assumed to be the time when the storage service receives the request.
        // Omitting the start time for a SAS that is effective immediately helps to avoid clock skew.
        SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.List |
            SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create | SharedAccessBlobPermissions.Delete
    };

    // Get the container's existing permissions.
    BlobContainerPermissions permissions = await container.GetPermissionsAsync();

    // Add the new policy to the container's permissions, and set the container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    await container.SetPermissionsAsync(permissions);
}
```

### <a name="example-create-a-service-sas-on-a-container"></a><span data-ttu-id="668bf-347">範例︰在容器上建立服務 SAS</span><span class="sxs-lookup"><span data-stu-id="668bf-347">Example: Create a service SAS on a container</span></span>
<span data-ttu-id="668bf-348">下列程式碼會在容器上建立 SAS。</span><span class="sxs-lookup"><span data-stu-id="668bf-348">The following code creates a SAS on a container.</span></span> <span data-ttu-id="668bf-349">如果提供現有預存存取原則的名稱，該原則將與 SAS 相關聯。</span><span class="sxs-lookup"><span data-stu-id="668bf-349">If the name of an existing stored access policy is provided, that policy is associated with the SAS.</span></span> <span data-ttu-id="668bf-350">如果未提供任何預存存取原則，則程式碼會在容器上建立臨機操作 SAS。</span><span class="sxs-lookup"><span data-stu-id="668bf-350">If no stored access policy is provided, then the code creates an ad-hoc SAS on the container.</span></span>

```csharp
private static string GetContainerSasUri(CloudBlobContainer container, string storedPolicyName = null)
{
    string sasContainerToken;

    // If no stored policy is specified, create a new access policy and define its constraints.
    if (storedPolicyName == null)
    {
        // Note that the SharedAccessBlobPolicy class is used both to define the parameters of an ad-hoc SAS, and
        // to construct a shared access policy that is saved to the container's shared access policies.
        SharedAccessBlobPolicy adHocPolicy = new SharedAccessBlobPolicy()
        {
            // When the start time for the SAS is omitted, the start time is assumed to be the time when the storage service receives the request.
            // Omitting the start time for a SAS that is effective immediately helps to avoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List
        };

        // Generate the shared access signature on the container, setting the constraints directly on the signature.
        sasContainerToken = container.GetSharedAccessSignature(adHocPolicy, null);

        Console.WriteLine("SAS for blob container (ad hoc): {0}", sasContainerToken);
        Console.WriteLine();
    }
    else
    {
        // Generate the shared access signature on the container. In this case, all of the constraints for the
        // shared access signature are specified on the stored access policy, which is provided by name.
        // It is also possible to specify some constraints on an ad-hoc SAS and others on the stored access policy.
        sasContainerToken = container.GetSharedAccessSignature(null, storedPolicyName);

        Console.WriteLine("SAS for blob container (stored access policy): {0}", sasContainerToken);
        Console.WriteLine();
    }

    // Return the URI string for the container, including the SAS token.
    return container.Uri + sasContainerToken;
}
```

### <a name="example-create-a-service-sas-on-a-blob"></a><span data-ttu-id="668bf-351">範例︰在 Blob 上建立服務 SAS</span><span class="sxs-lookup"><span data-stu-id="668bf-351">Example: Create a service SAS on a blob</span></span>
<span data-ttu-id="668bf-352">下列程式碼會在 Blob 上建立 SAS。</span><span class="sxs-lookup"><span data-stu-id="668bf-352">The following code creates a SAS on a blob.</span></span> <span data-ttu-id="668bf-353">如果提供現有預存存取原則的名稱，該原則將與 SAS 相關聯。</span><span class="sxs-lookup"><span data-stu-id="668bf-353">If the name of an existing stored access policy is provided, that policy is associated with the SAS.</span></span> <span data-ttu-id="668bf-354">如果未提供任何預存存取原則，則程式碼會在 Blob 上建立臨機操作 SAS。</span><span class="sxs-lookup"><span data-stu-id="668bf-354">If no stored access policy is provided, then the code creates an ad-hoc SAS on the blob.</span></span>

```csharp
private static string GetBlobSasUri(CloudBlobContainer container, string blobName, string policyName = null)
{
    string sasBlobToken;

    // Get a reference to a blob within the container.
    // Note that the blob may not exist yet, but a SAS can still be created for it.
    CloudBlockBlob blob = container.GetBlockBlobReference(blobName);

    if (policyName == null)
    {
        // Create a new access policy and define its constraints.
        // Note that the SharedAccessBlobPolicy class is used both to define the parameters of an ad-hoc SAS, and
        // to construct a shared access policy that is saved to the container's shared access policies.
        SharedAccessBlobPolicy adHocSAS = new SharedAccessBlobPolicy()
        {
            // When the start time for the SAS is omitted, the start time is assumed to be the time when the storage service receives the request.
            // Omitting the start time for a SAS that is effective immediately helps to avoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create
        };

        // Generate the shared access signature on the blob, setting the constraints directly on the signature.
        sasBlobToken = blob.GetSharedAccessSignature(adHocSAS);

        Console.WriteLine("SAS for blob (ad hoc): {0}", sasBlobToken);
        Console.WriteLine();
    }
    else
    {
        // Generate the shared access signature on the blob. In this case, all of the constraints for the
        // shared access signature are specified on the container's stored access policy.
        sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

        Console.WriteLine("SAS for blob (stored access policy): {0}", sasBlobToken);
        Console.WriteLine();
    }

    // Return the URI string for the container, including the SAS token.
    return blob.Uri + sasBlobToken;
}
```

## <a name="conclusion"></a><span data-ttu-id="668bf-355">結論</span><span class="sxs-lookup"><span data-stu-id="668bf-355">Conclusion</span></span>
<span data-ttu-id="668bf-356">若要提供您儲存體帳戶的有限權限給沒有帳戶金鑰的用戶端，則共用存取簽章是非常有用的方式。</span><span class="sxs-lookup"><span data-stu-id="668bf-356">Shared access signatures are useful for providing limited permissions to your storage account to clients that should not have the account key.</span></span> <span data-ttu-id="668bf-357">因此，對於任何使用 Azure 儲存體的應用程式而言，共用存取簽章是安全性模型不可或缺的一部分。</span><span class="sxs-lookup"><span data-stu-id="668bf-357">As such, they are a vital part of the security model for any application using Azure Storage.</span></span> <span data-ttu-id="668bf-358">如果您依照此處所列的最佳做法進行，則您可以使用 SAS 來提供更大的彈性以存取儲存體帳戶中的資源，且不會影響應用程式的安全性。</span><span class="sxs-lookup"><span data-stu-id="668bf-358">If you follow the best practices listed here, you can use SAS to provide greater flexibility of access to resources in your storage account, without compromising the security of your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="668bf-359">後續步驟</span><span class="sxs-lookup"><span data-stu-id="668bf-359">Next Steps</span></span>
* [<span data-ttu-id="668bf-360">管理對容器與 Blob 的匿名讀取權限。</span><span class="sxs-lookup"><span data-stu-id="668bf-360">Manage anonymous read access to containers and blobs</span></span>](../blobs/storage-manage-access-to-resources.md)
* [<span data-ttu-id="668bf-361">使用共用存取簽章來委派存取權</span><span class="sxs-lookup"><span data-stu-id="668bf-361">Delegating Access with a Shared Access Signature</span></span>](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [<span data-ttu-id="668bf-362">資料表與佇列 SAS 簡介</span><span class="sxs-lookup"><span data-stu-id="668bf-362">Introducing Table and Queue SAS</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
