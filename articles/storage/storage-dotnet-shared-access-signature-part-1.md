---
title: "aaaUsing 共用存取簽章 (SAS) 在 Azure 儲存體 |Microsoft 文件"
description: "了解 toouse 共用存取簽章 (SAS) toodelegate 存取 tooAzure 存放裝置資源，包括 blob、 佇列、 表格和檔案。"
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
ms.openlocfilehash: 53e06c78fbfdaa5fd209add719995ef2a6bc8f61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-shared-access-signatures-sas"></a><span data-ttu-id="c39cc-103">使用共用存取簽章 (SAS)</span><span class="sxs-lookup"><span data-stu-id="c39cc-103">Using shared access signatures (SAS)</span></span>

<span data-ttu-id="c39cc-104">共用的存取簽章 (SAS) 為您提供儲存體帳戶中的方式 toogrant 有限存取 tooobjects tooother 用戶端，而不會讓您的帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="c39cc-104">A shared access signature (SAS) provides you with a way toogrant limited access tooobjects in your storage account tooother clients, without exposing your account key.</span></span> <span data-ttu-id="c39cc-105">在本文中，我們提供 hello SAS 模型的概觀、 檢閱 SAS 最佳作法，以及查看一些範例。</span><span class="sxs-lookup"><span data-stu-id="c39cc-105">In this article, we provide an overview of hello SAS model, review SAS best practices, and look at some examples.</span></span>

<span data-ttu-id="c39cc-106">使用 SAS 除了這裡所呈現的額外的程式碼範例，請參閱[開始使用.NET 的 Azure Blob 儲存體](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)hello 的其他範例和[Azure 程式碼範例](https://azure.microsoft.com/documentation/samples/?service=storage)程式庫。</span><span class="sxs-lookup"><span data-stu-id="c39cc-106">For additional code examples using SAS beyond those presented here, see [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/) and other samples available in hello [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?service=storage) library.</span></span> <span data-ttu-id="c39cc-107">您可以下載 hello 範例應用程式並加以執行，或瀏覽 hello GitHub 上的程式碼。</span><span class="sxs-lookup"><span data-stu-id="c39cc-107">You can download hello sample applications and run them, or browse hello code on GitHub.</span></span>

## <a name="what-is-a-shared-access-signature"></a><span data-ttu-id="c39cc-108">共用存取簽章為何？</span><span class="sxs-lookup"><span data-stu-id="c39cc-108">What is a shared access signature?</span></span>
<span data-ttu-id="c39cc-109">共用的存取簽章提供儲存體帳戶中的委派的存取 tooresources。</span><span class="sxs-lookup"><span data-stu-id="c39cc-109">A shared access signature provides delegated access tooresources in your storage account.</span></span> <span data-ttu-id="c39cc-110">透過 SAS，您可以授與用戶端存取 tooresources 在儲存體帳戶，而不需要共用您的帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="c39cc-110">With a SAS, you can grant clients access tooresources in your storage account, without sharing your account keys.</span></span> <span data-ttu-id="c39cc-111">這是在您的應用程式-SAS 中使用共用的存取簽章的 hello 重點是安全的方式 tooshare 您的儲存體資源，而不會危害您的帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="c39cc-111">This is hello key point of using shared access signatures in your applications--a SAS is a secure way tooshare your storage resources without compromising your account keys.</span></span>

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

<span data-ttu-id="c39cc-112">SAS 可讓您更精確地控制存取您授與擁有 hello SAS，其中包括 tooclients hello 類型：</span><span class="sxs-lookup"><span data-stu-id="c39cc-112">A SAS gives you granular control over hello type of access you grant tooclients who have hello SAS, including:</span></span>

* <span data-ttu-id="c39cc-113">hello 的 hello 透過 SAS 有效間隔，包括 hello 開始時間和 hello 到期時間。</span><span class="sxs-lookup"><span data-stu-id="c39cc-113">hello interval over which hello SAS is valid, including hello start time and hello expiry time.</span></span>
* <span data-ttu-id="c39cc-114">hello hello SAS 所授與權限。</span><span class="sxs-lookup"><span data-stu-id="c39cc-114">hello permissions granted by hello SAS.</span></span> <span data-ttu-id="c39cc-115">例如，blob 的 SAS 可能會授與讀取和寫入權限 toothat blob，但刪除權限。</span><span class="sxs-lookup"><span data-stu-id="c39cc-115">For example, a SAS for a blob might grant read and write permissions toothat blob, but not delete permissions.</span></span>
* <span data-ttu-id="c39cc-116">選擇性的 IP 位址或 IP 位址範圍從中接受 Azure 儲存體 hello SAS。</span><span class="sxs-lookup"><span data-stu-id="c39cc-116">An optional IP address or range of IP addresses from which Azure Storage will accept hello SAS.</span></span> <span data-ttu-id="c39cc-117">例如，您可以指定屬於 tooyour 組織某個範圍的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c39cc-117">For example, you might specify a range of IP addresses belonging tooyour organization.</span></span>
* <span data-ttu-id="c39cc-118">hello 通訊協定的 Azure 儲存體將會接受 hello SAS。</span><span class="sxs-lookup"><span data-stu-id="c39cc-118">hello protocol over which Azure Storage will accept hello SAS.</span></span> <span data-ttu-id="c39cc-119">您可以使用此使用 HTTPS 的選擇性參數 toorestrict 存取 tooclients。</span><span class="sxs-lookup"><span data-stu-id="c39cc-119">You can use this optional parameter toorestrict access tooclients using HTTPS.</span></span>

## <a name="when-should-you-use-a-shared-access-signature"></a><span data-ttu-id="c39cc-120">使用共用存取簽章的時機？</span><span class="sxs-lookup"><span data-stu-id="c39cc-120">When should you use a shared access signature?</span></span>
<span data-ttu-id="c39cc-121">當您想 tooprovide 存取 tooresources 中不具備儲存體帳戶的存取金鑰將儲存體帳戶 tooany 用戶端時，您可以使用 SAS。</span><span class="sxs-lookup"><span data-stu-id="c39cc-121">You can use a SAS when you want tooprovide access tooresources in your storage account tooany client not possessing your storage account's access keys.</span></span> <span data-ttu-id="c39cc-122">儲存體帳戶包含主要和次要存取金鑰，這兩種授與系統管理存取權 tooyour 帳戶和其中的所有資源都。</span><span class="sxs-lookup"><span data-stu-id="c39cc-122">Your storage account includes both a primary and secondary access key, both of which grant administrative access tooyour account, and all resources within it.</span></span> <span data-ttu-id="c39cc-123">這些金鑰的公開會開啟您帳戶 toohello 的可能性惡意或疏忽使用。</span><span class="sxs-lookup"><span data-stu-id="c39cc-123">Exposing either of these keys opens your account toohello possibility of malicious or negligent use.</span></span> <span data-ttu-id="c39cc-124">共用的存取簽章提供安全的替代方案，可讓用戶端 tooread、 寫入和刪除資料中根據 toohello 權限已明確授與您，儲存體帳戶，而不需要帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="c39cc-124">Shared access signatures provide a safe alternative that allows clients tooread, write, and delete data in your storage account according toohello permissions you've explicitly granted, and without need for an account key.</span></span>

<span data-ttu-id="c39cc-125">其中一個 SAS，是實用的常見案例是的服務使用者讀取和寫入其本身資料 tooyour 儲存體帳戶的位置。</span><span class="sxs-lookup"><span data-stu-id="c39cc-125">A common scenario where a SAS is useful is a service where users read and write their own data tooyour storage account.</span></span> <span data-ttu-id="c39cc-126">在儲存體帳戶儲存使用者資料的案例中，典型的設計模式有兩種：</span><span class="sxs-lookup"><span data-stu-id="c39cc-126">In a scenario where a storage account stores user data, there are two typical design patterns:</span></span>

1. <span data-ttu-id="c39cc-127">用戶端通過前端 Proxy 服務 (執行驗證) 來上傳與下載資料。</span><span class="sxs-lookup"><span data-stu-id="c39cc-127">Clients upload and download data via a front-end proxy service, which performs authentication.</span></span> <span data-ttu-id="c39cc-128">此前端 proxy 服務有 hello 好處是允許的商務規則驗證，但對於大量的資料或大量的交易中，建立可調整 toomatch 要求的服務可能是昂貴或困難。</span><span class="sxs-lookup"><span data-stu-id="c39cc-128">This front-end proxy service has hello advantage of allowing validation of business rules, but for large amounts of data or high-volume transactions, creating a service that can scale toomatch demand may be expensive or difficult.</span></span>

  ![案例圖表︰前端 Proxy 服務][sas-storage-fe-proxy-service]

1. <span data-ttu-id="c39cc-130">輕量型的服務驗證 hello 用戶端，視需要並接著會產生 SAS。</span><span class="sxs-lookup"><span data-stu-id="c39cc-130">A lightweight service authenticates hello client as needed and then generates a SAS.</span></span> <span data-ttu-id="c39cc-131">一旦 hello 用戶端收到 hello SAS，他們可以存取儲存體帳戶資源，直接與 hello 定義 hello SAS 而且 hello 間隔 hello SAS 所允許的權限。</span><span class="sxs-lookup"><span data-stu-id="c39cc-131">Once hello client receives hello SAS, they can access storage account resources directly with hello permissions defined by hello SAS and for hello interval allowed by hello SAS.</span></span> <span data-ttu-id="c39cc-132">hello SAS 可降低 hello 需要路由透過 hello 前端 proxy 服務的所有資料。</span><span class="sxs-lookup"><span data-stu-id="c39cc-132">hello SAS mitigates hello need for routing all data through hello front-end proxy service.</span></span>

  ![案例圖表︰SAS 提供者服務][sas-storage-provider-service]

<span data-ttu-id="c39cc-134">許多實際服務可能會混合運用這兩種方法。</span><span class="sxs-lookup"><span data-stu-id="c39cc-134">Many real-world services may use a hybrid of these two approaches.</span></span> <span data-ttu-id="c39cc-135">例如，某些資料可能會處理並驗證透過 hello 前端 proxy，而其他資料是儲存和/或直接使用 SAS 讀取。</span><span class="sxs-lookup"><span data-stu-id="c39cc-135">For example, some data might be processed and validated via hello front-end proxy, while other data is saved and/or read directly using SAS.</span></span>

<span data-ttu-id="c39cc-136">此外，您將需要 toouse SAS tooauthenticate hello 來源中的物件在某些情況下複製作業：</span><span class="sxs-lookup"><span data-stu-id="c39cc-136">Additionally, you will need toouse a SAS tooauthenticate hello source object in a copy operation in certain scenarios:</span></span>

* <span data-ttu-id="c39cc-137">當您複製 blob tooanother blob 存在於不同的儲存體帳戶中時，您必須使用 SAS tooauthenticate hello 來源 blob。</span><span class="sxs-lookup"><span data-stu-id="c39cc-137">When you copy a blob tooanother blob that resides in a different storage account, you must use a SAS tooauthenticate hello source blob.</span></span> <span data-ttu-id="c39cc-138">您可以選擇使用 SAS tooauthenticate hello 目的地 blob 以及。</span><span class="sxs-lookup"><span data-stu-id="c39cc-138">You can optionally use a SAS tooauthenticate hello destination blob as well.</span></span>
* <span data-ttu-id="c39cc-139">當您複製檔案 tooanother 檔案位於不同的儲存體帳戶中時，您必須使用 SAS tooauthenticate hello 原始程式檔。</span><span class="sxs-lookup"><span data-stu-id="c39cc-139">When you copy a file tooanother file that resides in a different storage account, you must use a SAS tooauthenticate hello source file.</span></span> <span data-ttu-id="c39cc-140">您可以選擇使用 SAS tooauthenticate hello 目的地檔案。</span><span class="sxs-lookup"><span data-stu-id="c39cc-140">You can optionally use a SAS tooauthenticate hello destination file as well.</span></span>
* <span data-ttu-id="c39cc-141">當您複製 blob tooa 檔案或檔案 tooa blob 時，您必須使用 SAS tooauthenticate hello 來源物件，即使 hello 來源和目的地的物件位於 hello 相同儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c39cc-141">When you copy a blob tooa file, or a file tooa blob, you must use a SAS tooauthenticate hello source object, even if hello source and destination objects reside within hello same storage account.</span></span>

## <a name="types-of-shared-access-signatures"></a><span data-ttu-id="c39cc-142">共用存取簽章的類型</span><span class="sxs-lookup"><span data-stu-id="c39cc-142">Types of shared access signatures</span></span>
<span data-ttu-id="c39cc-143">您可建立兩種類型的共用存取簽章：</span><span class="sxs-lookup"><span data-stu-id="c39cc-143">You can create two types of shared access signatures:</span></span>

* <span data-ttu-id="c39cc-144">**服務 SAS。**</span><span class="sxs-lookup"><span data-stu-id="c39cc-144">**Service SAS.**</span></span> <span data-ttu-id="c39cc-145">hello 服務 SAS 委派存取 tooa 資源中其中一個 hello 存放服務： hello Blob、 佇列、 資料表或檔案服務。</span><span class="sxs-lookup"><span data-stu-id="c39cc-145">hello service SAS delegates access tooa resource in just one of hello storage services: hello Blob, Queue, Table, or File service.</span></span> <span data-ttu-id="c39cc-146">請參閱[建構服務 SAS](https://msdn.microsoft.com/library/dn140255.aspx)和[Service SAS 範例](https://msdn.microsoft.com/library/dn140256.aspx)如需建構 hello 服務 SAS 權杖的深入資訊。</span><span class="sxs-lookup"><span data-stu-id="c39cc-146">See [Constructing a Service SAS](https://msdn.microsoft.com/library/dn140255.aspx) and [Service SAS Examples](https://msdn.microsoft.com/library/dn140256.aspx) for in-depth information about constructing hello service SAS token.</span></span>
* <span data-ttu-id="c39cc-147">**帳戶 SAS。**</span><span class="sxs-lookup"><span data-stu-id="c39cc-147">**Account SAS.**</span></span> <span data-ttu-id="c39cc-148">hello SAS 授權帳戶存取 tooresources 中一或多個 hello 儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="c39cc-148">hello account SAS delegates access tooresources in one or more of hello storage services.</span></span> <span data-ttu-id="c39cc-149">所有透過 SAS 服務可用的 hello 作業也會提供透過 SAS 的帳戶。</span><span class="sxs-lookup"><span data-stu-id="c39cc-149">All of hello operations available via a service SAS are also available via an account SAS.</span></span> <span data-ttu-id="c39cc-150">此外，與 hello 帳戶 SAS，您可以將委派存取 toooperations 適用於提供服務，例如 tooa **Get/Set 服務內容**和**取得 Service Stats**。您也可以委派存取 tooread、 寫入和刪除 blob 容器、 資料表、 佇列和服務的 SAS 不允許的檔案共用上的作業。</span><span class="sxs-lookup"><span data-stu-id="c39cc-150">Additionally, with hello account SAS, you can delegate access toooperations that apply tooa given service, such as **Get/Set Service Properties** and **Get Service Stats**. You can also delegate access tooread, write, and delete operations on blob containers, tables, queues, and file shares that are not permitted with a service SAS.</span></span> <span data-ttu-id="c39cc-151">請參閱[建構帳戶 SAS](https://msdn.microsoft.com/library/mt584140.aspx)如需建構 hello 帳戶 SAS 權杖的深入資訊。</span><span class="sxs-lookup"><span data-stu-id="c39cc-151">See [Constructing an Account SAS](https://msdn.microsoft.com/library/mt584140.aspx) for in-depth information about constructing hello account SAS token.</span></span>

## <a name="how-a-shared-access-signature-works"></a><span data-ttu-id="c39cc-152">共用存取簽章的運作方式</span><span class="sxs-lookup"><span data-stu-id="c39cc-152">How a shared access signature works</span></span>
<span data-ttu-id="c39cc-153">共用的存取簽章是帶正負號的 URI 指向 tooone 或更多的儲存體資源，並含有包含一組特殊的查詢參數的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="c39cc-153">A shared access signature is a signed URI that points tooone or more storage resources and includes a token that contains a special set of query parameters.</span></span> <span data-ttu-id="c39cc-154">hello 語彙基元指出 hello 用戶端如何存取 hello 的資源。</span><span class="sxs-lookup"><span data-stu-id="c39cc-154">hello token indicates how hello resources may be accessed by hello client.</span></span> <span data-ttu-id="c39cc-155">Hello 查詢參數，其中 hello 簽章、 是建構自 hello SAS 參數和使用 hello 帳戶金鑰進行簽署。</span><span class="sxs-lookup"><span data-stu-id="c39cc-155">One of hello query parameters, hello signature, is constructed from hello SAS parameters and signed with hello account key.</span></span> <span data-ttu-id="c39cc-156">Azure 儲存體 tooauthenticate hello SAS 會使用此簽章。</span><span class="sxs-lookup"><span data-stu-id="c39cc-156">This signature is used by Azure Storage tooauthenticate hello SAS.</span></span>

<span data-ttu-id="c39cc-157">SAS URI、 顯示 hello 資源 URI 和 hello SAS 權杖的範例如下：</span><span class="sxs-lookup"><span data-stu-id="c39cc-157">Here's an example of a SAS URI, showing hello resource URI and hello SAS token:</span></span>

![SAS URI 的元件][sas-storage-uri]

<span data-ttu-id="c39cc-159">hello SAS 權杖是一個字串 hello 產生*用戶端*端 (請參閱 hello [SAS 範例](#sas-examples)> 一節的程式碼範例)。</span><span class="sxs-lookup"><span data-stu-id="c39cc-159">hello SAS token is a string you generate on hello *client* side (see hello [SAS examples](#sas-examples) section for code examples).</span></span> <span data-ttu-id="c39cc-160">SAS 權杖產生 hello 儲存體用戶端程式庫，例如，不會追蹤 Azure 儲存體以任何方式。</span><span class="sxs-lookup"><span data-stu-id="c39cc-160">A SAS token you generate with hello storage client library, for example, is not tracked by Azure Storage in any way.</span></span> <span data-ttu-id="c39cc-161">您可以建立無限的數量的 SAS 權杖 hello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="c39cc-161">You can create an unlimited number of SAS tokens on hello client side.</span></span>

<span data-ttu-id="c39cc-162">當用戶端提供的 SAS URI tooAzure 儲存體做為要求的一部分時，hello 服務會檢查 hello SAS 參數和簽章 tooverify 是適用於驗證 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="c39cc-162">When a client provides a SAS URI tooAzure Storage as part of a request, hello service checks hello SAS parameters and signature tooverify that it is valid for authenticating hello request.</span></span> <span data-ttu-id="c39cc-163">如果 hello 服務會確認該 hello 簽章有效，會驗證 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="c39cc-163">If hello service verifies that hello signature is valid, then hello request is authenticated.</span></span> <span data-ttu-id="c39cc-164">否則，hello 要求被拒絕，錯誤碼 403 （禁止）。</span><span class="sxs-lookup"><span data-stu-id="c39cc-164">Otherwise, hello request is declined with error code 403 (Forbidden).</span></span>

## <a name="shared-access-signature-parameters"></a><span data-ttu-id="c39cc-165">共用存取簽章參數</span><span class="sxs-lookup"><span data-stu-id="c39cc-165">Shared access signature parameters</span></span>
<span data-ttu-id="c39cc-166">hello 帳戶 SAS 和服務的 SAS 權杖包含一些常見的參數，而也不使用一些參數的不同。</span><span class="sxs-lookup"><span data-stu-id="c39cc-166">hello account SAS and service SAS tokens include some common parameters, and also take a few parameters that that are different.</span></span>

### <a name="parameters-common-tooaccount-sas-and-service-sas-tokens"></a><span data-ttu-id="c39cc-167">一般 tooaccount SAS 參數和服務的 SAS 權杖</span><span class="sxs-lookup"><span data-stu-id="c39cc-167">Parameters common tooaccount SAS and service SAS tokens</span></span>
* <span data-ttu-id="c39cc-168">**Api 版本**指定 hello 儲存體服務版本 toouse tooexecute hello 要求的選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="c39cc-168">**Api version** An optional parameter that specifies hello storage service version toouse tooexecute hello request.</span></span>
* <span data-ttu-id="c39cc-169">**服務版本**指定 hello 儲存體服務版本 toouse tooauthenticate hello 要求的必要的參數。</span><span class="sxs-lookup"><span data-stu-id="c39cc-169">**Service version** A required parameter that specifies hello storage service version toouse tooauthenticate hello request.</span></span>
* <span data-ttu-id="c39cc-170">**開始時間。**</span><span class="sxs-lookup"><span data-stu-id="c39cc-170">**Start time.**</span></span> <span data-ttu-id="c39cc-171">這是 hello 的 hello SAS 生效的時間。</span><span class="sxs-lookup"><span data-stu-id="c39cc-171">This is hello time at which hello SAS becomes valid.</span></span> <span data-ttu-id="c39cc-172">hello 共用的存取簽章的開始時間是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="c39cc-172">hello start time for a shared access signature is optional.</span></span> <span data-ttu-id="c39cc-173">如果省略開始時間，hello SAS 就是立即生效。</span><span class="sxs-lookup"><span data-stu-id="c39cc-173">If a start time is omitted, hello SAS is effective immediately.</span></span> <span data-ttu-id="c39cc-174">hello 開始時間必須以 UTC （國際標準時間），具有特殊的 UTC 指示項 ("Z")，例如`1994-11-05T13:15:30Z`。</span><span class="sxs-lookup"><span data-stu-id="c39cc-174">hello start time must be expressed in UTC (Coordinated Universal Time), with a special UTC designator ("Z"), for example `1994-11-05T13:15:30Z`.</span></span>
* <span data-ttu-id="c39cc-175">**到期時間。**</span><span class="sxs-lookup"><span data-stu-id="c39cc-175">**Expiry time.**</span></span> <span data-ttu-id="c39cc-176">這是 hello 時間過後 hello SAS 已不再有效。</span><span class="sxs-lookup"><span data-stu-id="c39cc-176">This is hello time after which hello SAS is no longer valid.</span></span> <span data-ttu-id="c39cc-177">最佳做法建議您為 SAS 指定過期時間，或將它與預存存取原則建立關聯。</span><span class="sxs-lookup"><span data-stu-id="c39cc-177">Best practices recommend that you either specify an expiry time for a SAS, or associate it with a stored access policy.</span></span> <span data-ttu-id="c39cc-178">hello 到期時間必須以 UTC （國際標準時間），具有特殊的 UTC 指示項 ("Z")，例如`1994-11-05T13:15:30Z`（將詳細說明）。</span><span class="sxs-lookup"><span data-stu-id="c39cc-178">hello expiry time must be expressed in UTC (Coordinated Universal Time), with a special UTC designator ("Z"), for example `1994-11-05T13:15:30Z` (see more below).</span></span>
* <span data-ttu-id="c39cc-179">**權限。**</span><span class="sxs-lookup"><span data-stu-id="c39cc-179">**Permissions.**</span></span> <span data-ttu-id="c39cc-180">hello hello SAS 上指定的權限表示 hello 用戶端可以針對使用 hello SAS hello 儲存體資源執行哪些作業。</span><span class="sxs-lookup"><span data-stu-id="c39cc-180">hello permissions specified on hello SAS indicate what operations hello client can perform against hello storage resource using hello SAS.</span></span> <span data-ttu-id="c39cc-181">帳戶 SAS 和服務 SAS 的可用權限不同。</span><span class="sxs-lookup"><span data-stu-id="c39cc-181">Available permissions differ for an account SAS and a service SAS.</span></span>
* <span data-ttu-id="c39cc-182">**IP。**</span><span class="sxs-lookup"><span data-stu-id="c39cc-182">**IP.**</span></span> <span data-ttu-id="c39cc-183">指定的 IP 位址或 IP 位址範圍 Azure 外部的選擇性參數 (參閱 hello[路由工作階段設定狀態](../expressroute/expressroute-workflows.md#routing-session-configuration-state)的 Express Route) 從哪些 tooaccept 要求。</span><span class="sxs-lookup"><span data-stu-id="c39cc-183">An optional parameter that specifies an IP address or a range of IP addresses outside of Azure (see hello section [Routing session configuration state](../expressroute/expressroute-workflows.md#routing-session-configuration-state) for Express Route) from which tooaccept requests.</span></span>
* <span data-ttu-id="c39cc-184">**通訊協定。**</span><span class="sxs-lookup"><span data-stu-id="c39cc-184">**Protocol.**</span></span> <span data-ttu-id="c39cc-185">選擇性參數指定 hello 通訊協定，允許的要求。</span><span class="sxs-lookup"><span data-stu-id="c39cc-185">An optional parameter that specifies hello protocol permitted for a request.</span></span> <span data-ttu-id="c39cc-186">可能的值為 HTTPS 和 HTTP (`https,http`)，這只是 hello 預設值或 HTTPS (`https`)。</span><span class="sxs-lookup"><span data-stu-id="c39cc-186">Possible values are both HTTPS and HTTP (`https,http`), which is hello default value, or HTTPS only (`https`).</span></span> <span data-ttu-id="c39cc-187">請注意，僅 HTTP 是不允許的值。</span><span class="sxs-lookup"><span data-stu-id="c39cc-187">Note that HTTP only is not a permitted value.</span></span>
* <span data-ttu-id="c39cc-188">**簽章。**</span><span class="sxs-lookup"><span data-stu-id="c39cc-188">**Signature.**</span></span> <span data-ttu-id="c39cc-189">hello 簽章從 hello 建構其他參數指定做為部分權杖，然後再加密。</span><span class="sxs-lookup"><span data-stu-id="c39cc-189">hello signature is constructed from hello other parameters specified as part token and then encrypted.</span></span> <span data-ttu-id="c39cc-190">它已用 tooauthenticate hello SAS。</span><span class="sxs-lookup"><span data-stu-id="c39cc-190">It's used tooauthenticate hello SAS.</span></span>

### <a name="parameters-for-a-service-sas-token"></a><span data-ttu-id="c39cc-191">服務 SAS 權杖的參數</span><span class="sxs-lookup"><span data-stu-id="c39cc-191">Parameters for a service SAS token</span></span>
* <span data-ttu-id="c39cc-192">**儲存體資源。**</span><span class="sxs-lookup"><span data-stu-id="c39cc-192">**Storage resource.**</span></span> <span data-ttu-id="c39cc-193">可以委派對服務 SAS 存取的儲存體資源包括：</span><span class="sxs-lookup"><span data-stu-id="c39cc-193">Storage resources for which you can delegate access with a service SAS include:</span></span>
  * <span data-ttu-id="c39cc-194">容器和 Blob</span><span class="sxs-lookup"><span data-stu-id="c39cc-194">Containers and blobs</span></span>
  * <span data-ttu-id="c39cc-195">檔案共用及檔案</span><span class="sxs-lookup"><span data-stu-id="c39cc-195">File shares and files</span></span>
  * <span data-ttu-id="c39cc-196">佇列</span><span class="sxs-lookup"><span data-stu-id="c39cc-196">Queues</span></span>
  * <span data-ttu-id="c39cc-197">資料表和資料表實體範圍。</span><span class="sxs-lookup"><span data-stu-id="c39cc-197">Tables and ranges of table entities.</span></span>

### <a name="parameters-for-an-account-sas-token"></a><span data-ttu-id="c39cc-198">帳戶 SAS 權杖的參數</span><span class="sxs-lookup"><span data-stu-id="c39cc-198">Parameters for an account SAS token</span></span>
* <span data-ttu-id="c39cc-199">**一或多個服務。**</span><span class="sxs-lookup"><span data-stu-id="c39cc-199">**Service or services.**</span></span> <span data-ttu-id="c39cc-200">SA 帳戶可以委派存取 tooone 或多個 hello 儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="c39cc-200">An account SAS can delegate access tooone or more of hello storage services.</span></span> <span data-ttu-id="c39cc-201">例如，您可以建立委派存取 toohello Blob 和檔案服務的帳戶 SAS。</span><span class="sxs-lookup"><span data-stu-id="c39cc-201">For example, you can create an account SAS that delegates access toohello Blob and File service.</span></span> <span data-ttu-id="c39cc-202">或者，您可以建立一個 SAS，委派存取 tooall 四項服務 （Blob、 佇列、 表格和檔案）。</span><span class="sxs-lookup"><span data-stu-id="c39cc-202">Or you can create a SAS that delegates access tooall four services (Blob, Queue, Table, and File).</span></span>
* <span data-ttu-id="c39cc-203">**儲存體資源類型。**</span><span class="sxs-lookup"><span data-stu-id="c39cc-203">**Storage resource types.**</span></span> <span data-ttu-id="c39cc-204">Tooone 或存放裝置資源，而非特定資源的多個類別，適用於 SAS 的帳戶。</span><span class="sxs-lookup"><span data-stu-id="c39cc-204">An account SAS applies tooone or more classes of storage resources, rather than a specific resource.</span></span> <span data-ttu-id="c39cc-205">您可以建立帳戶 SAS toodelegate 存取：</span><span class="sxs-lookup"><span data-stu-id="c39cc-205">You can create an account SAS toodelegate access to:</span></span>
  * <span data-ttu-id="c39cc-206">服務層級 Api，稱為針對 hello 儲存體帳戶的資源。</span><span class="sxs-lookup"><span data-stu-id="c39cc-206">Service-level APIs, which are called against hello storage account resource.</span></span> <span data-ttu-id="c39cc-207">範例包括**取得/設定服務屬性**、**取得服務統計資料**和**列出容器/佇列/資料表/共用**。</span><span class="sxs-lookup"><span data-stu-id="c39cc-207">Examples include **Get/Set Service Properties**, **Get Service Stats**, and **List Containers/Queues/Tables/Shares**.</span></span>
  * <span data-ttu-id="c39cc-208">容器層級 Api，其會針對每個服務呼叫 hello 容器物件： blob 容器、 佇列、 資料表和檔案共用。</span><span class="sxs-lookup"><span data-stu-id="c39cc-208">Container-level APIs, which are called against hello container objects for each service: blob containers, queues, tables, and file shares.</span></span> <span data-ttu-id="c39cc-209">範例包括**建立/刪除容器**、**建立/刪除佇列**、**建立/刪除資料表**、**建立/刪除共用**和**列出 Blob/檔案和目錄**。</span><span class="sxs-lookup"><span data-stu-id="c39cc-209">Examples include **Create/Delete Container**, **Create/Delete Queue**, **Create/Delete Table**, **Create/Delete Share**, and **List Blobs/Files and Directories**.</span></span>
  * <span data-ttu-id="c39cc-210">物件層級 API，針對 Blob、佇列訊息、資料表實體和檔案呼叫。</span><span class="sxs-lookup"><span data-stu-id="c39cc-210">Object-level APIs, which are called against blobs, queue messages, table entities, and files.</span></span> <span data-ttu-id="c39cc-211">例如，**放置 Blob**、**查詢實體**、**取得訊息**和**建立檔案**。</span><span class="sxs-lookup"><span data-stu-id="c39cc-211">For example, **Put Blob**, **Query Entity**, **Get Messages**, and **Create File**.</span></span>

## <a name="examples-of-sas-uris"></a><span data-ttu-id="c39cc-212">SAS URI 的範例</span><span class="sxs-lookup"><span data-stu-id="c39cc-212">Examples of SAS URIs</span></span>

### <a name="service-sas-uri-example"></a><span data-ttu-id="c39cc-213">服務 SAS URI 範例</span><span class="sxs-lookup"><span data-stu-id="c39cc-213">Service SAS URI example</span></span>

<span data-ttu-id="c39cc-214">以下是提供的 SAS URI 讀取和寫入權限 tooa blob 服務的範例。</span><span class="sxs-lookup"><span data-stu-id="c39cc-214">Here is an example of a service SAS URI that provides read and write permissions tooa blob.</span></span> <span data-ttu-id="c39cc-215">hello 資料表細分 hello URI toounderstand 的每個部分看出何影響 toohello SA:</span><span class="sxs-lookup"><span data-stu-id="c39cc-215">hello table breaks down each part of hello URI toounderstand how it contributes toohello SAS:</span></span>

```
https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2015-04-05&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D
```

| <span data-ttu-id="c39cc-216">名稱</span><span class="sxs-lookup"><span data-stu-id="c39cc-216">Name</span></span> | <span data-ttu-id="c39cc-217">SAS 部分</span><span class="sxs-lookup"><span data-stu-id="c39cc-217">SAS portion</span></span> | <span data-ttu-id="c39cc-218">說明</span><span class="sxs-lookup"><span data-stu-id="c39cc-218">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c39cc-219">Blob URI</span><span class="sxs-lookup"><span data-stu-id="c39cc-219">Blob URI</span></span> |`https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt` |<span data-ttu-id="c39cc-220">hello hello blob 位址。</span><span class="sxs-lookup"><span data-stu-id="c39cc-220">hello address of hello blob.</span></span> <span data-ttu-id="c39cc-221">請注意，我們強烈建議您使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="c39cc-221">Note that using HTTPS is highly recommended.</span></span> |
| <span data-ttu-id="c39cc-222">儲存體服務版本</span><span class="sxs-lookup"><span data-stu-id="c39cc-222">Storage services version</span></span> |`sv=2015-04-05` |<span data-ttu-id="c39cc-223">儲存體服務 2012年-02-12 版和更新版本中，這個參數會指出 hello 版本 toouse。</span><span class="sxs-lookup"><span data-stu-id="c39cc-223">For storage services version 2012-02-12 and later, this parameter indicates hello version toouse.</span></span> |
| <span data-ttu-id="c39cc-224">開始時間</span><span class="sxs-lookup"><span data-stu-id="c39cc-224">Start time</span></span> |`st=2015-04-29T22%3A18%3A26Z` |<span data-ttu-id="c39cc-225">以 UTC 時間指定。</span><span class="sxs-lookup"><span data-stu-id="c39cc-225">Specified in UTC time.</span></span> <span data-ttu-id="c39cc-226">如果您想 hello SAS toobe 有效立即，省略 hello 開始時間。</span><span class="sxs-lookup"><span data-stu-id="c39cc-226">If you want hello SAS toobe valid immediately, omit hello start time.</span></span> |
| <span data-ttu-id="c39cc-227">過期時間</span><span class="sxs-lookup"><span data-stu-id="c39cc-227">Expiry time</span></span> |`se=2015-04-30T02%3A23%3A26Z` |<span data-ttu-id="c39cc-228">以 UTC 時間指定。</span><span class="sxs-lookup"><span data-stu-id="c39cc-228">Specified in UTC time.</span></span> |
| <span data-ttu-id="c39cc-229">資源</span><span class="sxs-lookup"><span data-stu-id="c39cc-229">Resource</span></span> |`sr=b` |<span data-ttu-id="c39cc-230">hello 資源是 blob。</span><span class="sxs-lookup"><span data-stu-id="c39cc-230">hello resource is a blob.</span></span> |
| <span data-ttu-id="c39cc-231">權限</span><span class="sxs-lookup"><span data-stu-id="c39cc-231">Permissions</span></span> |`sp=rw` |<span data-ttu-id="c39cc-232">hello hello SAS 授與的權限包括 Read (r)，和寫入 (w)。</span><span class="sxs-lookup"><span data-stu-id="c39cc-232">hello permissions granted by hello SAS include Read (r) and Write (w).</span></span> |
| <span data-ttu-id="c39cc-233">IP 範圍</span><span class="sxs-lookup"><span data-stu-id="c39cc-233">IP range</span></span> |`sip=168.1.5.60-168.1.5.70` |<span data-ttu-id="c39cc-234">hello 的 IP 位址範圍將會接受要求。</span><span class="sxs-lookup"><span data-stu-id="c39cc-234">hello range of IP addresses from which a request will be accepted.</span></span> |
| <span data-ttu-id="c39cc-235">通訊協定</span><span class="sxs-lookup"><span data-stu-id="c39cc-235">Protocol</span></span> |`spr=https` |<span data-ttu-id="c39cc-236">僅允許使用 HTTPS 的要求。</span><span class="sxs-lookup"><span data-stu-id="c39cc-236">Only requests using HTTPS are permitted.</span></span> |
| <span data-ttu-id="c39cc-237">簽章</span><span class="sxs-lookup"><span data-stu-id="c39cc-237">Signature</span></span> |`sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D` |<span data-ttu-id="c39cc-238">使用 tooauthenticate 存取 toohello blob。</span><span class="sxs-lookup"><span data-stu-id="c39cc-238">Used tooauthenticate access toohello blob.</span></span> <span data-ttu-id="c39cc-239">hello 簽章是計算字串簽章和金鑰使用 hello SHA256 演算法，並編碼使用 Base64 編碼的 HMAC。</span><span class="sxs-lookup"><span data-stu-id="c39cc-239">hello signature is an HMAC computed over a string-to-sign and key using hello SHA256 algorithm, and then encoded using Base64 encoding.</span></span> |

### <a name="account-sas-uri-example"></a><span data-ttu-id="c39cc-240">帳戶 SAS URI 範例</span><span class="sxs-lookup"><span data-stu-id="c39cc-240">Account SAS URI example</span></span>

<span data-ttu-id="c39cc-241">以下是範例 SA 帳戶的使用 hello hello 權杖相同的一般參數。</span><span class="sxs-lookup"><span data-stu-id="c39cc-241">Here is an example of an account SAS that uses hello same common parameters on hello token.</span></span> <span data-ttu-id="c39cc-242">由於上面說明了這些參數，在此處將不說明。</span><span class="sxs-lookup"><span data-stu-id="c39cc-242">Since these parameters are described above, they are not described here.</span></span> <span data-ttu-id="c39cc-243">只有 hello 參數，為特定 tooaccount SAS 詳述於下表 hello。</span><span class="sxs-lookup"><span data-stu-id="c39cc-243">Only hello parameters that are specific tooaccount SAS are described in hello table below.</span></span>

```
https://myaccount.blob.core.windows.net/?restype=service&comp=properties&sv=2015-04-05&ss=bf&srt=s&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=F%6GRVAZ5Cdj2Pw4tgU7IlSTkWgn7bUkkAg8P6HESXwmf%4B
```

| <span data-ttu-id="c39cc-244">名稱</span><span class="sxs-lookup"><span data-stu-id="c39cc-244">Name</span></span> | <span data-ttu-id="c39cc-245">SAS 部分</span><span class="sxs-lookup"><span data-stu-id="c39cc-245">SAS portion</span></span> | <span data-ttu-id="c39cc-246">說明</span><span class="sxs-lookup"><span data-stu-id="c39cc-246">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c39cc-247">資源 URI</span><span class="sxs-lookup"><span data-stu-id="c39cc-247">Resource URI</span></span> |`https://myaccount.blob.core.windows.net/?restype=service&comp=properties` |<span data-ttu-id="c39cc-248">hello Blob 服務端點，使用參數來取得服務屬性 （當使用 GET 呼叫），或設定服務屬性 （當呼叫組）。</span><span class="sxs-lookup"><span data-stu-id="c39cc-248">hello Blob service endpoint, with parameters for getting service properties (when called with GET) or setting service properties (when called with SET).</span></span> |
| <span data-ttu-id="c39cc-249">服務</span><span class="sxs-lookup"><span data-stu-id="c39cc-249">Services</span></span> |`ss=bf` |<span data-ttu-id="c39cc-250">hello SAS 套用 toohello Blob 和檔案服務</span><span class="sxs-lookup"><span data-stu-id="c39cc-250">hello SAS applies toohello Blob and File services</span></span> |
| <span data-ttu-id="c39cc-251">資源類型</span><span class="sxs-lookup"><span data-stu-id="c39cc-251">Resource types</span></span> |`srt=s` |<span data-ttu-id="c39cc-252">hello SAS 適用於 tooservice 層級的作業。</span><span class="sxs-lookup"><span data-stu-id="c39cc-252">hello SAS applies tooservice-level operations.</span></span> |
| <span data-ttu-id="c39cc-253">權限</span><span class="sxs-lookup"><span data-stu-id="c39cc-253">Permissions</span></span> |`sp=rw` |<span data-ttu-id="c39cc-254">hello 權限授與存取 tooread 和寫入作業。</span><span class="sxs-lookup"><span data-stu-id="c39cc-254">hello permissions grant access tooread and write operations.</span></span> |

<span data-ttu-id="c39cc-255">Toohello 服務層級，透過此 SAS 存取作業的權限受到限制是**取得 Blob 服務屬性**（讀取） 和**設定 Blob 服務屬性**（寫入）。</span><span class="sxs-lookup"><span data-stu-id="c39cc-255">Given that permissions are restricted toohello service level, accessible operations with this SAS are **Get Blob Service Properties** (read) and **Set Blob Service Properties** (write).</span></span> <span data-ttu-id="c39cc-256">不過，使用不同的資源 URI，hello 相同 SAS 權杖也可能是使用 toodelegate 存取太**取得 Blob 服務統計資料**（讀取）。</span><span class="sxs-lookup"><span data-stu-id="c39cc-256">However, with a different resource URI, hello same SAS token could also be used toodelegate access too**Get Blob Service Stats** (read).</span></span>

## <a name="controlling-a-sas-with-a-stored-access-policy"></a><span data-ttu-id="c39cc-257">使用預存存取原則控制 SAS</span><span class="sxs-lookup"><span data-stu-id="c39cc-257">Controlling a SAS with a stored access policy</span></span>
<span data-ttu-id="c39cc-258">共用存取簽章可以接受以下兩種格式其中之一：</span><span class="sxs-lookup"><span data-stu-id="c39cc-258">A shared access signature can take one of two forms:</span></span>

* <span data-ttu-id="c39cc-259">**臨機操作 SAS:**當您建立臨機操作 SAS、 hello 開始時間、 到期時間和 hello SAS 的權限會指定在 hello SAS URI （或默示擔保，則開始時間的 hello 案例中）。</span><span class="sxs-lookup"><span data-stu-id="c39cc-259">**Ad hoc SAS:** When you create an ad hoc SAS, hello start time, expiry time, and permissions for hello SAS are all specified in hello SAS URI (or implied, in hello case where start time is omitted).</span></span> <span data-ttu-id="c39cc-260">這種類型的 SAS 可能會建立為帳戶 SAS 或服務 SAS。</span><span class="sxs-lookup"><span data-stu-id="c39cc-260">This type of SAS can be created as an account SAS or a service SAS.</span></span>
* <span data-ttu-id="c39cc-261">**與預存的存取原則 SAS:**預存的存取原則定義資源的容器-blob 容器、 資料表、 佇列或檔案共用-和可以是一個或多個共用的存取簽章使用的 toomanage 條件約束。</span><span class="sxs-lookup"><span data-stu-id="c39cc-261">**SAS with stored access policy:** A stored access policy is defined on a resource container--a blob container, table, queue, or file share--and can be used toomanage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="c39cc-262">當您建立 SAS 關聯與預存的存取原則時，hello SAS 會繼承 hello 條件約束-hello 開始時間、 到期時間和權限-hello 預存存取原則的定義。</span><span class="sxs-lookup"><span data-stu-id="c39cc-262">When you associate a SAS with a stored access policy, hello SAS inherits hello constraints--hello start time, expiry time, and permissions--defined for hello stored access policy.</span></span>

> [!NOTE]
> <span data-ttu-id="c39cc-263">目前，帳戶 SAS 必須是臨機操作 SAS。</span><span class="sxs-lookup"><span data-stu-id="c39cc-263">Currently, an account SAS must be an ad hoc SAS.</span></span> <span data-ttu-id="c39cc-264">帳戶 SAS 尚不支援預存的存取原則。</span><span class="sxs-lookup"><span data-stu-id="c39cc-264">Stored access policies are not yet supported for account SAS.</span></span>

<span data-ttu-id="c39cc-265">hello hello 兩個形式之間的差異是很重要的一個重要的案例： 撤銷。</span><span class="sxs-lookup"><span data-stu-id="c39cc-265">hello difference between hello two forms is important for one key scenario: revocation.</span></span> <span data-ttu-id="c39cc-266">SAS URI 為 URL，因為任何人都可以取得 hello SAS，可以使用它無論原先建立者。</span><span class="sxs-lookup"><span data-stu-id="c39cc-266">Because a SAS URI is a URL, anyone that obtains hello SAS can use it, regardless of who originally created it.</span></span> <span data-ttu-id="c39cc-267">如果已公開發行 SAS，才能使用 hello 世界中的任何人。</span><span class="sxs-lookup"><span data-stu-id="c39cc-267">If a SAS is published publicly, it can be used by anyone in hello world.</span></span> <span data-ttu-id="c39cc-268">SAS 授與存取 tooresources tooanyone 擁有它，直到其中一四項發生：</span><span class="sxs-lookup"><span data-stu-id="c39cc-268">A SAS grants access tooresources tooanyone possessing it until one of four things happens:</span></span>

1. <span data-ttu-id="c39cc-269">hello 上 hello SAS 達到指定的到期時間。</span><span class="sxs-lookup"><span data-stu-id="c39cc-269">hello expiry time specified on hello SAS is reached.</span></span>
2. <span data-ttu-id="c39cc-270">hello hello SAS 為止 （參考的預存的存取原則時，而且如果它會指定到期時間） 所參考的 hello 預存存取原則中指定的到期時間。</span><span class="sxs-lookup"><span data-stu-id="c39cc-270">hello expiry time specified on hello stored access policy referenced by hello SAS is reached (if a stored access policy is referenced, and if it specifies an expiry time).</span></span> <span data-ttu-id="c39cc-271">這可能是因為 hello 間隔經過之後，或您修改了 hello 預存存取原則與到期時間在 hello 過去，這是其中一種方式 toorevoke hello SAS。</span><span class="sxs-lookup"><span data-stu-id="c39cc-271">This can occur either because hello interval elapses, or because you've modified hello stored access policy with an expiry time in hello past, which is one way toorevoke hello SAS.</span></span>
3. <span data-ttu-id="c39cc-272">hello 預存存取原則參考的 hello SAS 遭到刪除，也就是另一個方式 toorevoke hello SAS。</span><span class="sxs-lookup"><span data-stu-id="c39cc-272">hello stored access policy referenced by hello SAS is deleted, which is another way toorevoke hello SAS.</span></span> <span data-ttu-id="c39cc-273">請注意，如果您完全重新建立 hello 預存存取原則與 hello 相同的名稱，所有現有的 SAS 權杖會一次有效的相應 toohello 權限與原則相關聯該預存的存取 （假設的 hello SAS 未跳過該 hello 到期時間）。</span><span class="sxs-lookup"><span data-stu-id="c39cc-273">Note that if you recreate hello stored access policy with exactly hello same name, all existing SAS tokens will again be valid according toohello permissions associated with that stored access policy (assuming that hello expiry time on hello SAS has not passed).</span></span> <span data-ttu-id="c39cc-274">如果您打算 toorevoke hello SAS，是確定 toouse 不同名稱，如果您重新建立與到期時間在未來的 hello hello 存取原則。</span><span class="sxs-lookup"><span data-stu-id="c39cc-274">If you are intending toorevoke hello SAS, be sure toouse a different name if you recreate hello access policy with an expiry time in hello future.</span></span>
4. <span data-ttu-id="c39cc-275">重新產生已使用的 toocreate hello SAS 的 hello 帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="c39cc-275">hello account key that was used toocreate hello SAS is regenerated.</span></span> <span data-ttu-id="c39cc-276">重新產生帳戶金鑰會導致所有應用程式元件使用該金鑰 toofail tooauthenticate 其他有效的帳戶金鑰或 hello 新重新產生的帳戶金鑰在更新之前 toouse 或是 hello。</span><span class="sxs-lookup"><span data-stu-id="c39cc-276">Regenerating an account key will cause all application components using that key toofail tooauthenticate until they're updated toouse either hello other valid account key or hello newly regenerated account key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c39cc-277">共用的存取簽章 URI 都與 hello 帳戶金鑰的使用的 toocreate hello 簽章，與 hello 預存的存取原則 （如果有的話）。</span><span class="sxs-lookup"><span data-stu-id="c39cc-277">A shared access signature URI is associated with hello account key used toocreate hello signature, and hello associated stored access policy (if any).</span></span> <span data-ttu-id="c39cc-278">如果未不指定任何預存的存取原則，則 hello 只方式 toorevoke 共用的存取簽章是 toochange hello 帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="c39cc-278">If no stored access policy is specified, hello only way toorevoke a shared access signature is toochange hello account key.</span></span>

## <a name="authenticating-from-a-client-application-with-a-sas"></a><span data-ttu-id="c39cc-279">使用 SAS 從用戶端應用程式進行驗證</span><span class="sxs-lookup"><span data-stu-id="c39cc-279">Authenticating from a client application with a SAS</span></span>
<span data-ttu-id="c39cc-280">擁有 SAS 的用戶端可以使用 hello SAS tooauthenticate 對儲存體帳戶沒有 hello 帳戶金鑰的要求。</span><span class="sxs-lookup"><span data-stu-id="c39cc-280">A client who is in possession of a SAS can use hello SAS tooauthenticate a request against a storage account for which they do not possess hello account keys.</span></span> <span data-ttu-id="c39cc-281">SAS 可以包含在連接字串中，或直接從 hello 適當的建構函式或方法。</span><span class="sxs-lookup"><span data-stu-id="c39cc-281">A SAS can be included in a connection string, or used directly from hello appropriate constructor or method.</span></span>

### <a name="using-a-sas-in-a-connection-string"></a><span data-ttu-id="c39cc-282">在連接字串中使用 SAS</span><span class="sxs-lookup"><span data-stu-id="c39cc-282">Using a SAS in a connection string</span></span>
[!INCLUDE [storage-use-sas-in-connection-string-include](../../includes/storage-use-sas-in-connection-string-include.md)]

### <a name="using-a-sas-in-a-constructor-or-method"></a><span data-ttu-id="c39cc-283">在建構函式或方法中使用 SAS</span><span class="sxs-lookup"><span data-stu-id="c39cc-283">Using a SAS in a constructor or method</span></span>
<span data-ttu-id="c39cc-284">數個 Azure 儲存體用戶端程式庫建構函式和方法多載提供 SAS 參數，讓您可以驗證 SAS 要求 toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="c39cc-284">Several Azure Storage client library constructors and method overloads offer a SAS parameter, so that you can authenticate a request toohello service with a SAS.</span></span>

<span data-ttu-id="c39cc-285">例如，以下 SAS URI 是使用的 toocreate 參考 tooa 區塊 blob。</span><span class="sxs-lookup"><span data-stu-id="c39cc-285">For example, here a SAS URI is used toocreate a reference tooa block blob.</span></span> <span data-ttu-id="c39cc-286">hello SAS 提供 hello 只有 hello 要求所需的認證。</span><span class="sxs-lookup"><span data-stu-id="c39cc-286">hello SAS provides hello only credentials needed for hello request.</span></span> <span data-ttu-id="c39cc-287">hello 區塊 blob 參考然後用於寫入作業：</span><span class="sxs-lookup"><span data-stu-id="c39cc-287">hello block blob reference is then used for a write operation:</span></span>

```csharp
string sasUri = "https://storagesample.blob.core.windows.net/sample-container/" +
    "sampleBlob.txt?sv=2015-07-08&sr=b&sig=39Up9JzHkxhUIhFEjEH9594DJxe7w6cIRCg0V6lCGSo%3D" +
    "&se=2016-10-18T21%3A51%3A37Z&sp=rcw";

CloudBlockBlob blob = new CloudBlockBlob(new Uri(sasUri));

// Create operation: Upload a blob with hello specified name toohello container.
// If hello blob does not exist, it will be created. If it does exist, it will be overwritten.
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

## <a name="best-practices-when-using-sas"></a><span data-ttu-id="c39cc-288">使用 SAS 時的最佳做法</span><span class="sxs-lookup"><span data-stu-id="c39cc-288">Best practices when using SAS</span></span>
<span data-ttu-id="c39cc-289">當您在應用程式中使用共用的存取簽章時，您需要 toobe 注意兩個潛在的風險：</span><span class="sxs-lookup"><span data-stu-id="c39cc-289">When you use shared access signatures in your applications, you need toobe aware of two potential risks:</span></span>

* <span data-ttu-id="c39cc-290">如果 SAS 洩漏出去，則取得該 SAS 的任何人都可以使用它，這有可能會洩露您的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c39cc-290">If a SAS is leaked, it can be used by anyone who obtains it, which can potentially compromise your storage account.</span></span>
* <span data-ttu-id="c39cc-291">如果 SAS 提供 tooa 用戶端應用程式到期且 hello 應用程式無法 tooretrieve 新 SAS 從您的服務，可能會減慢 hello 應用程式的功能。</span><span class="sxs-lookup"><span data-stu-id="c39cc-291">If a SAS provided tooa client application expires and hello application is unable tooretrieve a new SAS from your service, then hello application's functionality may be hindered.</span></span>

<span data-ttu-id="c39cc-292">hello 使用共用的存取簽章的下列建議可協助降低這些風險：</span><span class="sxs-lookup"><span data-stu-id="c39cc-292">hello following recommendations for using shared access signatures can help mitigate these risks:</span></span>

1. <span data-ttu-id="c39cc-293">**一律使用 HTTPS** toocreate 或散發 SAS。</span><span class="sxs-lookup"><span data-stu-id="c39cc-293">**Always use HTTPS** toocreate or distribute a SAS.</span></span> <span data-ttu-id="c39cc-294">如果 SAS 是透過 HTTP 傳入，而且攔截，執行攔截密碼破解攻擊的攻擊者為可以 tooread hello SAS，，然後使用它，就如同 hello 適合使用者可以擁有，可能洩漏機密資料，或允許的資料損毀 hello惡意的使用者。</span><span class="sxs-lookup"><span data-stu-id="c39cc-294">If a SAS is passed over HTTP and intercepted, an attacker performing a man-in-the-middle attack is able tooread hello SAS and then use it just as hello intended user could have, potentially compromising sensitive data or allowing for data corruption by hello malicious user.</span></span>
2. <span data-ttu-id="c39cc-295">**可能的話，參考預存存取原則。**</span><span class="sxs-lookup"><span data-stu-id="c39cc-295">**Reference stored access policies where possible.**</span></span> <span data-ttu-id="c39cc-296">預存存取原則讓您無須 tooregenerate hello 儲存體帳戶金鑰 hello 選項 toorevoke 權限。</span><span class="sxs-lookup"><span data-stu-id="c39cc-296">Stored access policies give you hello option toorevoke permissions without having tooregenerate hello storage account keys.</span></span> <span data-ttu-id="c39cc-297">這些最在 hello 設定 hello 逾期，未來的 （或無限的），並確定它有定期更新 toomove 遠到未來的 hello。</span><span class="sxs-lookup"><span data-stu-id="c39cc-297">Set hello expiration on these very far in hello future (or infinite) and make sure it's regularly updated toomove it farther into hello future.</span></span>
3. <span data-ttu-id="c39cc-298">**在臨機操作 SAS 上使用短期的到期時間。**</span><span class="sxs-lookup"><span data-stu-id="c39cc-298">**Use near-term expiration times on an ad hoc SAS.**</span></span> <span data-ttu-id="c39cc-299">如此一來，即使 SAS 遭到入侵，亦僅會造成短期影響。</span><span class="sxs-lookup"><span data-stu-id="c39cc-299">In this way, even if a SAS is compromised, it's valid only for a short time.</span></span> <span data-ttu-id="c39cc-300">如果您無法參考預存存取原則，此做法格外重要。</span><span class="sxs-lookup"><span data-stu-id="c39cc-300">This practice is especially important if you cannot reference a stored access policy.</span></span> <span data-ttu-id="c39cc-301">Star 逾期時間也會限制 hello 可以藉由限制 hello 時間可用 tooupload tooit 寫入 tooa blob 的資料量。</span><span class="sxs-lookup"><span data-stu-id="c39cc-301">Near-term expiration times also limit hello amount of data that can be written tooa blob by limiting hello time available tooupload tooit.</span></span>
4. <span data-ttu-id="c39cc-302">**有 hello SAS 必要時，自動更新用戶端。**</span><span class="sxs-lookup"><span data-stu-id="c39cc-302">**Have clients automatically renew hello SAS if necessary.**</span></span> <span data-ttu-id="c39cc-303">用戶端應該更新 hello SAS hello 到期日重試提供 hello SAS hello 服務無法使用時的順序 tooallow 時間之前。</span><span class="sxs-lookup"><span data-stu-id="c39cc-303">Clients should renew hello SAS well before hello expiration, in order tooallow time for retries if hello service providing hello SAS is unavailable.</span></span> <span data-ttu-id="c39cc-304">如果您的 SAS 適用於少量立即 toobe，存留較短的作業都必須是 toobe 期間內完成 hello 到期，則這可能是不必要更新 toobe hello SAS 不正常。</span><span class="sxs-lookup"><span data-stu-id="c39cc-304">If your SAS is meant toobe used for a small number of immediate, short-lived operations that are expected toobe completed within hello expiration period, then this may be unnecessary as hello SAS is not expected toobe renewed.</span></span> <span data-ttu-id="c39cc-305">不過，如果您有定期正在透過 SAS 要求的用戶端，然後到期 hello 可能性派上用場。</span><span class="sxs-lookup"><span data-stu-id="c39cc-305">However, if you have client that is routinely making requests via SAS, then hello possibility of expiration comes into play.</span></span> <span data-ttu-id="c39cc-306">hello 重要考量是 toobalance hello 需要 hello SAS toobe 存留較短 （如先前所述） 與 hello 用戶端的 hello 需要 tooensure 早期要求更新足夠 （tooavoid 中斷到期 toohello SAS 到期之前 toosuccessful 更新）。</span><span class="sxs-lookup"><span data-stu-id="c39cc-306">hello key consideration is toobalance hello need for hello SAS toobe short-lived (as previously stated) with hello need tooensure that hello client is requesting renewal early enough (tooavoid disruption due toohello SAS expiring prior toosuccessful renewal).</span></span>
5. <span data-ttu-id="c39cc-307">**請小心使用 SAS 開始時間。**</span><span class="sxs-lookup"><span data-stu-id="c39cc-307">**Be careful with SAS start time.**</span></span> <span data-ttu-id="c39cc-308">如果您設定 hello 開始時間的 SAS 太**現在**，然後 tooclock 誤差 （根據 toodifferent 機器的目前時間的差異），因為失敗可能會觀察到間歇性 hello 第一個幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="c39cc-308">If you set hello start time for a SAS too**now**, then due tooclock skew (differences in current time according toodifferent machines), failures may be observed intermittently for hello first few minutes.</span></span> <span data-ttu-id="c39cc-309">一般情況下，設定 hello 開始時間 toobe 至少 15 分鐘過去 hello。</span><span class="sxs-lookup"><span data-stu-id="c39cc-309">In general, set hello start time toobe at least 15 minutes in hello past.</span></span> <span data-ttu-id="c39cc-310">或是不進行任何設定，這會針對所有案例立即生效。</span><span class="sxs-lookup"><span data-stu-id="c39cc-310">Or, don't set it at all, which will make it valid immediately in all cases.</span></span> <span data-ttu-id="c39cc-311">hello 相同通常適用於 tooexpiry 時間以及-請記住，您可能會注意到向上 too15 分鐘的時鐘誤差任一方向上的任何要求。</span><span class="sxs-lookup"><span data-stu-id="c39cc-311">hello same generally applies tooexpiry time as well--remember that you may observe up too15 minutes of clock skew in either direction on any request.</span></span> <span data-ttu-id="c39cc-312">用戶端使用 REST 版本先前 too2012-02-12，hello SAS 未參考的預存的存取原則的最大持續期間是 1 小時，並指定較長的詞彙，比，將會失敗的任何原則。</span><span class="sxs-lookup"><span data-stu-id="c39cc-312">For clients using a REST version prior too2012-02-12, hello maximum duration for a SAS that does not reference a stored access policy is 1 hour, and any policies specifying longer term than that will fail.</span></span>
6. <span data-ttu-id="c39cc-313">**是特定的 hello 資源 toobe 存取。**</span><span class="sxs-lookup"><span data-stu-id="c39cc-313">**Be specific with hello resource toobe accessed.**</span></span> <span data-ttu-id="c39cc-314">安全性最佳作法是 tooprovide hello 最低必要權限的使用者。</span><span class="sxs-lookup"><span data-stu-id="c39cc-314">A security best practice is tooprovide a user with hello minimum required privileges.</span></span> <span data-ttu-id="c39cc-315">如果使用者只需要讀取權限 tooa 單一實體，然後授與他們 toothat 單一實體讀取權限和不讀取/寫入/刪除存取 tooall 實體。</span><span class="sxs-lookup"><span data-stu-id="c39cc-315">If a user only needs read access tooa single entity, then grant them read access toothat single entity, and not read/write/delete access tooall entities.</span></span> <span data-ttu-id="c39cc-316">這也有助於降低 hello 損毀，如果 SAS 遭到入侵，因為 hello SAS hello 指針，攻擊者中的電力較少。</span><span class="sxs-lookup"><span data-stu-id="c39cc-316">This also helps lessen hello damage if a SAS is compromised because hello SAS has less power in hello hands of an attacker.</span></span>
7. <span data-ttu-id="c39cc-317">**了解您帳戶的任何方式將會被收取費用，包括以 SAS 方式完成的部分。**</span><span class="sxs-lookup"><span data-stu-id="c39cc-317">**Understand that your account will be billed for any usage, including that done with SAS.**</span></span> <span data-ttu-id="c39cc-318">如果您提供寫入存取 tooa blob 時，使用者可能選擇 tooupload 200 GB 的 blob。</span><span class="sxs-lookup"><span data-stu-id="c39cc-318">If you provide write access tooa blob, a user may choose tooupload a 200GB blob.</span></span> <span data-ttu-id="c39cc-319">如果您已獲得它們讀取權限，可能會選擇 toodownload 10 次，在輸出中產生 2 TB 成本為您。</span><span class="sxs-lookup"><span data-stu-id="c39cc-319">If you've given them read access as well, they may choose toodownload it 10 times, incurring 2 TB in egress costs for you.</span></span> <span data-ttu-id="c39cc-320">同樣地，提供有限的權限 toohelp 減輕惡意使用者的 hello 潛在動作。</span><span class="sxs-lookup"><span data-stu-id="c39cc-320">Again, provide limited permissions toohelp mitigate hello potential actions of malicious users.</span></span> <span data-ttu-id="c39cc-321">使用這項威脅存留較短的 SAS tooreduce （但留意時鐘誤差 hello 結束時間）。</span><span class="sxs-lookup"><span data-stu-id="c39cc-321">Use short-lived SAS tooreduce this threat (but be mindful of clock skew on hello end time).</span></span>
8. <span data-ttu-id="c39cc-322">**使用 SAS 驗證寫入資料。**</span><span class="sxs-lookup"><span data-stu-id="c39cc-322">**Validate data written using SAS.**</span></span> <span data-ttu-id="c39cc-323">當用戶端應用程式寫入資料 tooyour 儲存體帳戶時，請注意，可能會有該資料的問題。</span><span class="sxs-lookup"><span data-stu-id="c39cc-323">When a client application writes data tooyour storage account, keep in mind that there can be problems with that data.</span></span> <span data-ttu-id="c39cc-324">如果您的應用程式需要的驗證或授權之前準備好 toouse 資料，您應該在 hello 資料寫入之後，它由您的應用程式之前執行這項驗證。</span><span class="sxs-lookup"><span data-stu-id="c39cc-324">If your application requires that that data be validated or authorized before it is ready toouse, you should perform this validation after hello data is written and before it is used by your application.</span></span> <span data-ttu-id="c39cc-325">這種做法也可防止損毀或惡意的資料寫入 tooyour 帳戶的使用者，正確地取得 hello SAS，或是利用遺漏的 SAS 的使用者。</span><span class="sxs-lookup"><span data-stu-id="c39cc-325">This practice also protects against corrupt or malicious data being written tooyour account, either by a user who properly acquired hello SAS, or by a user exploiting a leaked SAS.</span></span>
9. <span data-ttu-id="c39cc-326">**請勿一直使用 SAS。**</span><span class="sxs-lookup"><span data-stu-id="c39cc-326">**Don't always use SAS.**</span></span> <span data-ttu-id="c39cc-327">有時 hello 與針對儲存體帳戶的特定作業相關聯的風險，勝過 hello 優點的 SAS。</span><span class="sxs-lookup"><span data-stu-id="c39cc-327">Sometimes hello risks associated with a particular operation against your storage account outweigh hello benefits of SAS.</span></span> <span data-ttu-id="c39cc-328">這類作業，建立中介層服務寫入 tooyour 儲存體帳戶之後執行商務規則驗證、 驗證和稽核。</span><span class="sxs-lookup"><span data-stu-id="c39cc-328">For such operations, create a middle-tier service that writes tooyour storage account after performing business rule validation, authentication, and auditing.</span></span> <span data-ttu-id="c39cc-329">此外，有時也是以其他方式較簡單的 toomanage 存取。</span><span class="sxs-lookup"><span data-stu-id="c39cc-329">Also, sometimes it's simpler toomanage access in other ways.</span></span> <span data-ttu-id="c39cc-330">比方說，如果您想 toomake 容器中的所有 blob 公開可讀取，您可以進行 hello 容器為公用，而不是 SAS tooevery 用戶端提供存取。</span><span class="sxs-lookup"><span data-stu-id="c39cc-330">For example, if you want toomake all blobs in a container publically readable, you can make hello container Public, rather than providing a SAS tooevery client for access.</span></span>
10. <span data-ttu-id="c39cc-331">**使用儲存體分析 toomonitor 您的應用程式。**</span><span class="sxs-lookup"><span data-stu-id="c39cc-331">**Use Storage Analytics toomonitor your application.**</span></span> <span data-ttu-id="c39cc-332">您可以使用記錄和度量 tooobserve 任何特殊驗證失敗，因為 tooan 中斷您 SAS 提供者服務或 toohello 不小心移除預存的存取原則。</span><span class="sxs-lookup"><span data-stu-id="c39cc-332">You can use logging and metrics tooobserve any spike in authentication failures due tooan outage in your SAS provider service or toohello inadvertent removal of a stored access policy.</span></span> <span data-ttu-id="c39cc-333">請參閱 hello [Azure 儲存體團隊部落格](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="c39cc-333">See hello [Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx) for additional information.</span></span>

## <a name="sas-examples"></a><span data-ttu-id="c39cc-334">SAS 範例</span><span class="sxs-lookup"><span data-stu-id="c39cc-334">SAS examples</span></span>
<span data-ttu-id="c39cc-335">下面是兩種類型共用存取簽章 (帳戶 SAS 和服務 SAS) 的一些範例。</span><span class="sxs-lookup"><span data-stu-id="c39cc-335">Below are some examples of both types of shared access signatures, account SAS and service SAS.</span></span>

<span data-ttu-id="c39cc-336">toorun 這些 C# 範例中，您需要下列專案中的 NuGet 套件 tooreference hello:</span><span class="sxs-lookup"><span data-stu-id="c39cc-336">toorun these C# examples, you need tooreference hello following NuGet packages in your project:</span></span>

* <span data-ttu-id="c39cc-337">[適用於.NET 的 azure 儲存體用戶端程式庫](http://www.nuget.org/packages/WindowsAzure.Storage)，版本 6.x 或更新版本 （toouse 帳戶 SAS）。</span><span class="sxs-lookup"><span data-stu-id="c39cc-337">[Azure Storage Client Library for .NET](http://www.nuget.org/packages/WindowsAzure.Storage), version 6.x or later (toouse account SAS).</span></span>
* [<span data-ttu-id="c39cc-338">Azure 資源管理員</span><span class="sxs-lookup"><span data-stu-id="c39cc-338">Azure Configuration Manager</span></span>](http://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager)

<span data-ttu-id="c39cc-339">如需其他範例，示範如何 toocreate 和測試 SAS，請參閱[儲存體的 Azure 程式碼範例](https://azure.microsoft.com/documentation/samples/?service=storage)。</span><span class="sxs-lookup"><span data-stu-id="c39cc-339">For additional examples that show how toocreate and test a SAS, see [Azure Code Samples for Storage](https://azure.microsoft.com/documentation/samples/?service=storage).</span></span>

### <a name="example-create-and-use-an-account-sas"></a><span data-ttu-id="c39cc-340">範例︰建立和使用帳戶 SAS</span><span class="sxs-lookup"><span data-stu-id="c39cc-340">Example: Create and use an account SAS</span></span>
<span data-ttu-id="c39cc-341">hello 下列程式碼範例會建立僅適用於 hello Blob 及檔案服務的 SAS 的帳戶，並提供 hello 用戶端權限讀取、 寫入和列出權限 tooaccess 服務層級應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="c39cc-341">hello following code example creates an account SAS that is valid for hello Blob and File services, and gives hello client permissions read, write, and list permissions tooaccess service-level APIs.</span></span> <span data-ttu-id="c39cc-342">hello 帳戶 SAS 會限制 hello 通訊協定 tooHTTPS，因此 hello 要求必須設定成使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="c39cc-342">hello account SAS restricts hello protocol tooHTTPS, so hello request must be made with HTTPS.</span></span>

```csharp
static string GetAccountSASToken()
{
    // toocreate hello account SAS, you need toouse your shared key credentials. Modify for your account.
    const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

    // Create a new access policy for hello account.
    SharedAccessAccountPolicy policy = new SharedAccessAccountPolicy()
        {
            Permissions = SharedAccessAccountPermissions.Read | SharedAccessAccountPermissions.Write | SharedAccessAccountPermissions.List,
            Services = SharedAccessAccountServices.Blob | SharedAccessAccountServices.File,
            ResourceTypes = SharedAccessAccountResourceTypes.Service,
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Protocols = SharedAccessProtocol.HttpsOnly
        };

    // Return hello SAS token.
    return storageAccount.GetSharedAccessSignature(policy);
}
```

<span data-ttu-id="c39cc-343">toouse hello 帳戶 SAS tooaccess 服務層級 Api hello Blob 服務、 建構使用 hello SAS Blob 用戶端物件和 hello 儲存體帳戶的 Blob 儲存體端點。</span><span class="sxs-lookup"><span data-stu-id="c39cc-343">toouse hello account SAS tooaccess service-level APIs for hello Blob service, construct a Blob client object using hello SAS and hello Blob storage endpoint for your storage account.</span></span>

```csharp
static void UseAccountSAS(string sasToken)
{
    // Create new storage credentials using hello SAS token.
    StorageCredentials accountSAS = new StorageCredentials(sasToken);
    // Use these credentials and hello account name toocreate a Blob service client.
    CloudStorageAccount accountWithSAS = new CloudStorageAccount(accountSAS, "account-name", endpointSuffix: null, useHttps: true);
    CloudBlobClient blobClientWithSAS = accountWithSAS.CreateCloudBlobClient();

    // Now set hello service properties for hello Blob client created with hello SAS.
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

    // hello permissions granted by hello account SAS also permit you tooretrieve service properties.
    ServiceProperties serviceProperties = blobClientWithSAS.GetServiceProperties();
    Console.WriteLine(serviceProperties.HourMetrics.MetricsLevel);
    Console.WriteLine(serviceProperties.HourMetrics.RetentionDays);
    Console.WriteLine(serviceProperties.HourMetrics.Version);
}
```

### <a name="example-create-a-stored-access-policy"></a><span data-ttu-id="c39cc-344">範例：建立預存的存取原則</span><span class="sxs-lookup"><span data-stu-id="c39cc-344">Example: Create a stored access policy</span></span>
<span data-ttu-id="c39cc-345">hello 下列程式碼會建立預存的存取原則在容器上。</span><span class="sxs-lookup"><span data-stu-id="c39cc-345">hello following code creates a stored access policy on a container.</span></span> <span data-ttu-id="c39cc-346">您可以使用 hello 存取原則 toospecify 條件約束服務 hello 容器上的 SAS 或其 blob。</span><span class="sxs-lookup"><span data-stu-id="c39cc-346">You can use hello access policy toospecify constraints for a service SAS on hello container or its blobs.</span></span>

```csharp
private static async Task CreateSharedAccessPolicyAsync(CloudBlobContainer container, string policyName)
{
    // Create a new shared access policy and define its constraints.
    // hello access policy provides create, write, read, list, and delete permissions.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
        // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
        SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.List |
            SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create | SharedAccessBlobPermissions.Delete
    };

    // Get hello container's existing permissions.
    BlobContainerPermissions permissions = await container.GetPermissionsAsync();

    // Add hello new policy toohello container's permissions, and set hello container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    await container.SetPermissionsAsync(permissions);
}
```

### <a name="example-create-a-service-sas-on-a-container"></a><span data-ttu-id="c39cc-347">範例︰在容器上建立服務 SAS</span><span class="sxs-lookup"><span data-stu-id="c39cc-347">Example: Create a service SAS on a container</span></span>
<span data-ttu-id="c39cc-348">下列程式碼的 hello 容器上建立 SAS。</span><span class="sxs-lookup"><span data-stu-id="c39cc-348">hello following code creates a SAS on a container.</span></span> <span data-ttu-id="c39cc-349">提供現有的預存的存取原則的 hello 名稱，該原則與 hello SAS 相關聯。</span><span class="sxs-lookup"><span data-stu-id="c39cc-349">If hello name of an existing stored access policy is provided, that policy is associated with hello SAS.</span></span> <span data-ttu-id="c39cc-350">如果未不提供任何預存的存取原則，則 hello 程式碼會建立臨機操作 SAS hello 容器上。</span><span class="sxs-lookup"><span data-stu-id="c39cc-350">If no stored access policy is provided, then hello code creates an ad-hoc SAS on hello container.</span></span>

```csharp
private static string GetContainerSasUri(CloudBlobContainer container, string storedPolicyName = null)
{
    string sasContainerToken;

    // If no stored policy is specified, create a new access policy and define its constraints.
    if (storedPolicyName == null)
    {
        // Note that hello SharedAccessBlobPolicy class is used both toodefine hello parameters of an ad-hoc SAS, and
        // tooconstruct a shared access policy that is saved toohello container's shared access policies.
        SharedAccessBlobPolicy adHocPolicy = new SharedAccessBlobPolicy()
        {
            // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
            // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List
        };

        // Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
        sasContainerToken = container.GetSharedAccessSignature(adHocPolicy, null);

        Console.WriteLine("SAS for blob container (ad hoc): {0}", sasContainerToken);
        Console.WriteLine();
    }
    else
    {
        // Generate hello shared access signature on hello container. In this case, all of hello constraints for the
        // shared access signature are specified on hello stored access policy, which is provided by name.
        // It is also possible toospecify some constraints on an ad-hoc SAS and others on hello stored access policy.
        sasContainerToken = container.GetSharedAccessSignature(null, storedPolicyName);

        Console.WriteLine("SAS for blob container (stored access policy): {0}", sasContainerToken);
        Console.WriteLine();
    }

    // Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

### <a name="example-create-a-service-sas-on-a-blob"></a><span data-ttu-id="c39cc-351">範例︰在 Blob 上建立服務 SAS</span><span class="sxs-lookup"><span data-stu-id="c39cc-351">Example: Create a service SAS on a blob</span></span>
<span data-ttu-id="c39cc-352">下列程式碼的 hello 的 blob 上建立 SAS。</span><span class="sxs-lookup"><span data-stu-id="c39cc-352">hello following code creates a SAS on a blob.</span></span> <span data-ttu-id="c39cc-353">提供現有的預存的存取原則的 hello 名稱，該原則與 hello SAS 相關聯。</span><span class="sxs-lookup"><span data-stu-id="c39cc-353">If hello name of an existing stored access policy is provided, that policy is associated with hello SAS.</span></span> <span data-ttu-id="c39cc-354">如果未不提供任何預存的存取原則，則 hello 程式碼會建立臨機操作 SAS hello blob 上。</span><span class="sxs-lookup"><span data-stu-id="c39cc-354">If no stored access policy is provided, then hello code creates an ad-hoc SAS on hello blob.</span></span>

```csharp
private static string GetBlobSasUri(CloudBlobContainer container, string blobName, string policyName = null)
{
    string sasBlobToken;

    // Get a reference tooa blob within hello container.
    // Note that hello blob may not exist yet, but a SAS can still be created for it.
    CloudBlockBlob blob = container.GetBlockBlobReference(blobName);

    if (policyName == null)
    {
        // Create a new access policy and define its constraints.
        // Note that hello SharedAccessBlobPolicy class is used both toodefine hello parameters of an ad-hoc SAS, and
        // tooconstruct a shared access policy that is saved toohello container's shared access policies.
        SharedAccessBlobPolicy adHocSAS = new SharedAccessBlobPolicy()
        {
            // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
            // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create
        };

        // Generate hello shared access signature on hello blob, setting hello constraints directly on hello signature.
        sasBlobToken = blob.GetSharedAccessSignature(adHocSAS);

        Console.WriteLine("SAS for blob (ad hoc): {0}", sasBlobToken);
        Console.WriteLine();
    }
    else
    {
        // Generate hello shared access signature on hello blob. In this case, all of hello constraints for the
        // shared access signature are specified on hello container's stored access policy.
        sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

        Console.WriteLine("SAS for blob (stored access policy): {0}", sasBlobToken);
        Console.WriteLine();
    }

    // Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

## <a name="conclusion"></a><span data-ttu-id="c39cc-355">結論</span><span class="sxs-lookup"><span data-stu-id="c39cc-355">Conclusion</span></span>
<span data-ttu-id="c39cc-356">共用的存取簽章可用於不應有 hello 帳戶金鑰的 tooyour 儲存體帳戶 tooclients 提供有限的權限。</span><span class="sxs-lookup"><span data-stu-id="c39cc-356">Shared access signatures are useful for providing limited permissions tooyour storage account tooclients that should not have hello account key.</span></span> <span data-ttu-id="c39cc-357">因此，它們是 hello 安全性模型，使用 Azure 儲存體的任何應用程式不可或缺的一部分。</span><span class="sxs-lookup"><span data-stu-id="c39cc-357">As such, they are a vital part of hello security model for any application using Azure Storage.</span></span> <span data-ttu-id="c39cc-358">如果您遵循此處所列的 hello 最佳作法，您可以使用儲存體帳戶中的 SAS tooprovide 更大的彈性存取 tooresources 不會危及應用程式的 hello 安全性。</span><span class="sxs-lookup"><span data-stu-id="c39cc-358">If you follow hello best practices listed here, you can use SAS tooprovide greater flexibility of access tooresources in your storage account, without compromising hello security of your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c39cc-359">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c39cc-359">Next Steps</span></span>
* [<span data-ttu-id="c39cc-360">管理匿名讀取權限 toocontainers 和 blob</span><span class="sxs-lookup"><span data-stu-id="c39cc-360">Manage anonymous read access toocontainers and blobs</span></span>](storage-manage-access-to-resources.md)
* [<span data-ttu-id="c39cc-361">使用共用存取簽章來委派存取權</span><span class="sxs-lookup"><span data-stu-id="c39cc-361">Delegating Access with a Shared Access Signature</span></span>](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [<span data-ttu-id="c39cc-362">資料表與佇列 SAS 簡介</span><span class="sxs-lookup"><span data-stu-id="c39cc-362">Introducing Table and Queue SAS</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)

[sas-storage-fe-proxy-service]: ./media/storage-dotnet-shared-access-signature-part-1/sas-storage-fe-proxy-service.png
[sas-storage-provider-service]: ./media/storage-dotnet-shared-access-signature-part-1/sas-storage-provider-service.png
[sas-storage-uri]: ./media/storage-dotnet-shared-access-signature-part-1/sas-storage-uri.png
