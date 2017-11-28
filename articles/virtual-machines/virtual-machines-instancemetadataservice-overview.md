---
title: "aaaAzure 執行個體中繼資料服務的概觀 |Microsoft 文件"
description: "RESTful 介面 tooget VM 的計算、 網路與即將進行維護事件相關的資訊。"
services: virtual-machines-windows, virtual-machines-linux,virtual-machines-scale-sets, cloud-services
documentationcenter: virtual-machines
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 03/27/2017
ms.author: harijay
ms.openlocfilehash: e87cdf28f80b9ef8cc566b637549c48846862f0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-instance-metadata-service"></a><span data-ttu-id="c9b6a-103">Azure 執行個體中繼資料服務</span><span class="sxs-lookup"><span data-stu-id="c9b6a-103">Azure Instance Metadata Service</span></span> 


<span data-ttu-id="c9b6a-104">hello Azure 執行個體中繼資料服務提供執行可使用的 toomanage 和設定虛擬機器的虛擬機器執行個體的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-104">hello Azure Instance Metadata Service provides information about running virtual machine instances that can be used toomanage and configure your virtual machines.</span></span>
<span data-ttu-id="c9b6a-105">這包括 SKU、網路組態及近期維護事件等資訊。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-105">This includes information such as SKU, network configuration, and upcoming maintenance events.</span></span> <span data-ttu-id="c9b6a-106">如需可用資訊類型的詳細資訊，請參閱[中繼資料類別](#instance-metadata-data-categories)。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-106">For more information on what type of information is available, see [metadata categories](#instance-metadata-data-categories).</span></span>

<span data-ttu-id="c9b6a-107">Azure 的執行個體中繼資料服務是可存取 tooall IaaS Vm 建立 hello 透過 REST 端點[Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/)。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-107">Azure's Instance Metadata Service is a REST Endpoint accessible tooall IaaS VMs created via hello [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="c9b6a-108">hello 端點位於已知的路由的內部 IP 位址 (`169.254.169.254`) 以存取只能從 hello VM 內。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-108">hello endpoint is available at a well-known non-routable IP address (`169.254.169.254`) that can be accessed only from within hello VM.</span></span>

### <a name="important-information"></a><span data-ttu-id="c9b6a-109">重要資訊</span><span class="sxs-lookup"><span data-stu-id="c9b6a-109">Important information</span></span>

<span data-ttu-id="c9b6a-110">這項服務已在全域 Azure 區域中**正式推出**。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-110">This service is  **generally available** in Global Azure Regions.</span></span> <span data-ttu-id="c9b6a-111">目前有 Government、China 和 German Azure Cloud 的公開預覽版。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-111">It is in Public preview for Government, China, and German Azure Cloud.</span></span> <span data-ttu-id="c9b6a-112">定期收到更新 tooexpose 新虛擬機器執行個體相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-112">It regularly receives updates tooexpose new information about virtual machine instances.</span></span> <span data-ttu-id="c9b6a-113">此頁面會反映最新的 hello[資料分類](#instance-metadata-data-categories)可用。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-113">This page reflects hello up-to-date [data categories](#instance-metadata-data-categories) available.</span></span>

## <a name="service-availability"></a><span data-ttu-id="c9b6a-114">服務可用性</span><span class="sxs-lookup"><span data-stu-id="c9b6a-114">Service Availability</span></span>
<span data-ttu-id="c9b6a-115">hello 服務處於可用正式推出的所有全域 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-115">hello service is available in all generally available Global Azure regions.</span></span> <span data-ttu-id="c9b6a-116">hello 服務為 hello 政府、 China 或德國區域中的公用預覽。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-116">hello service is in public preview  in hello Government, China, or Germany regions.</span></span>

<span data-ttu-id="c9b6a-117">區域</span><span class="sxs-lookup"><span data-stu-id="c9b6a-117">Regions</span></span>                                        | <span data-ttu-id="c9b6a-118">可用性？</span><span class="sxs-lookup"><span data-stu-id="c9b6a-118">Availability?</span></span>
-----------------------------------------------|-----------------------------------------------
[<span data-ttu-id="c9b6a-119">所有正式推出的全域 Azure 區域</span><span class="sxs-lookup"><span data-stu-id="c9b6a-119">All Generally Available Global Azure Regions</span></span>](https://azure.microsoft.com/en-us/regions/)     | <span data-ttu-id="c9b6a-120">正式推出</span><span class="sxs-lookup"><span data-stu-id="c9b6a-120">Generally Available</span></span> 
[<span data-ttu-id="c9b6a-121">Azure Government</span><span class="sxs-lookup"><span data-stu-id="c9b6a-121">Azure Government</span></span>](https://azure.microsoft.com/en-us/overview/clouds/government/)              | <span data-ttu-id="c9b6a-122">預覽狀態</span><span class="sxs-lookup"><span data-stu-id="c9b6a-122">In Preview</span></span> 
[<span data-ttu-id="c9b6a-123">Azure China</span><span class="sxs-lookup"><span data-stu-id="c9b6a-123">Azure China</span></span>](https://www.azure.cn/)                                                           | <span data-ttu-id="c9b6a-124">預覽狀態</span><span class="sxs-lookup"><span data-stu-id="c9b6a-124">In Preview</span></span>
[<span data-ttu-id="c9b6a-125">Azure Germany</span><span class="sxs-lookup"><span data-stu-id="c9b6a-125">Azure Germany</span></span>](https://azure.microsoft.com/en-us/overview/clouds/germany/)                    | <span data-ttu-id="c9b6a-126">預覽狀態</span><span class="sxs-lookup"><span data-stu-id="c9b6a-126">In Preview</span></span>

<span data-ttu-id="c9b6a-127">Hello 服務變為可以使用其他的 Azure 雲端中時，會更新這個資料表。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-127">This table is updated when hello service becomes available in other Azure clouds.</span></span>

<span data-ttu-id="c9b6a-128">tootry 出 hello 執行個體中繼資料服務，建立從 VM [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/)或 hello [Azure 入口網站](http://portal.azure.com)hello 上方區域和後續 hello 以下的範例中。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-128">tootry out hello Instance Metadata Service, create a VM from [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) or hello [Azure portal](http://portal.azure.com) in hello above regions and follow hello examples below.</span></span>

## <a name="usage"></a><span data-ttu-id="c9b6a-129">使用量</span><span class="sxs-lookup"><span data-stu-id="c9b6a-129">Usage</span></span>

### <a name="versioning"></a><span data-ttu-id="c9b6a-130">版本控制</span><span class="sxs-lookup"><span data-stu-id="c9b6a-130">Versioning</span></span>
<span data-ttu-id="c9b6a-131">hello 執行個體中繼資料服務已進行版本設定。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-131">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="c9b6a-132">版本都是必要項，而 hello 目前版本為`2017-04-02`。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-132">Versions are mandatory and hello current version is `2017-04-02`.</span></span>

> [!NOTE] 
> <span data-ttu-id="c9b6a-133">預覽舊版的排程為 hello 的 api 版本 {最新} 支援的事件。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-133">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="c9b6a-134">不再支援這種格式，而且將在未來的 hello 中被取代。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-134">This format is no longer supported and will be deprecated in hello future.</span></span>

<span data-ttu-id="c9b6a-135">當我們新增較新版本時，如果您的指令碼對於特定資料格式有相依性，則因為相容性，仍然可以存取較舊版本。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-135">As we add newer versions, older versions can still be accessed for compatibility if your scripts have dependencies on specific data formats.</span></span> <span data-ttu-id="c9b6a-136">不過請注意該 hello 目前預覽 version(2017-03-01) 通常可使用 hello 服務後，可能無法使用。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-136">However, note that hello current preview version(2017-03-01) may not be available once hello service is generally available.</span></span>

### <a name="using-headers"></a><span data-ttu-id="c9b6a-137">使用標頭</span><span class="sxs-lookup"><span data-stu-id="c9b6a-137">Using Headers</span></span>
<span data-ttu-id="c9b6a-138">當您查詢 hello 執行個體中繼資料服務時，您必須提供 hello 標頭`Metadata: true`tooensure hello 要求不小心重新導向。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-138">When you query hello Instance Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="retrieving-metadata"></a><span data-ttu-id="c9b6a-139">擷取中繼資料</span><span class="sxs-lookup"><span data-stu-id="c9b6a-139">Retrieving metadata</span></span>

<span data-ttu-id="c9b6a-140">執行個體中繼資料適用於使用 [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) 建立/管理的執行中 VM。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-140">Instance metadata is available for running VMs created/managed using [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="c9b6a-141">存取使用 hello 下列要求的虛擬機器執行個體的所有資料分類：</span><span class="sxs-lookup"><span data-stu-id="c9b6a-141">Access all data categories for a virtual machine instance using hello following request:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> <span data-ttu-id="c9b6a-142">所有執行個體中繼資料查詢都會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-142">All instance metadata queries are case-sensitive.</span></span>

### <a name="data-output"></a><span data-ttu-id="c9b6a-143">資料輸出</span><span class="sxs-lookup"><span data-stu-id="c9b6a-143">Data output</span></span>
<span data-ttu-id="c9b6a-144">根據預設，hello 執行個體中繼資料服務會傳回資料以 JSON 格式 (`Content-Type: application/json`)。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-144">By default, hello Instance Metadata Service returns data in JSON format (`Content-Type: application/json`).</span></span> <span data-ttu-id="c9b6a-145">不過，不同的 API 可以依照要求傳回不同格式的資料。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-145">However, different APIs can return data in different formats if requested.</span></span>
<span data-ttu-id="c9b6a-146">hello 表是應用程式開發介面可能支援其他資料格式的參考。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-146">hello following table is a reference of other data formats APIs may support.</span></span>

<span data-ttu-id="c9b6a-147">API</span><span class="sxs-lookup"><span data-stu-id="c9b6a-147">API</span></span> | <span data-ttu-id="c9b6a-148">預設資料格式</span><span class="sxs-lookup"><span data-stu-id="c9b6a-148">Default Data Format</span></span> | <span data-ttu-id="c9b6a-149">其他格式</span><span class="sxs-lookup"><span data-stu-id="c9b6a-149">Other Formats</span></span>
--------|---------------------|--------------
<span data-ttu-id="c9b6a-150">/instance</span><span class="sxs-lookup"><span data-stu-id="c9b6a-150">/instance</span></span> | <span data-ttu-id="c9b6a-151">json</span><span class="sxs-lookup"><span data-stu-id="c9b6a-151">json</span></span> | <span data-ttu-id="c9b6a-152">文字</span><span class="sxs-lookup"><span data-stu-id="c9b6a-152">text</span></span>
<span data-ttu-id="c9b6a-153">/scheduledevents</span><span class="sxs-lookup"><span data-stu-id="c9b6a-153">/scheduledevents</span></span> | <span data-ttu-id="c9b6a-154">json</span><span class="sxs-lookup"><span data-stu-id="c9b6a-154">json</span></span> | <span data-ttu-id="c9b6a-155">無</span><span class="sxs-lookup"><span data-stu-id="c9b6a-155">none</span></span>

<span data-ttu-id="c9b6a-156">tooaccess 為非預設回應格式，指定 hello 要求的格式為 hello 要求查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-156">tooaccess a non-default response format, specify hello requested format as a querystring parameter in hello request.</span></span> <span data-ttu-id="c9b6a-157">例如：</span><span class="sxs-lookup"><span data-stu-id="c9b6a-157">For example:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a><span data-ttu-id="c9b6a-158">安全性</span><span class="sxs-lookup"><span data-stu-id="c9b6a-158">Security</span></span>
<span data-ttu-id="c9b6a-159">hello 非路由的 IP 位址上執行虛擬機器執行個體只能從存取 hello 執行個體中繼資料服務端點。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-159">hello Instance Metadata Service endpoint is accessible only from within hello running virtual machine instance on a non-routable IP address.</span></span> <span data-ttu-id="c9b6a-160">此外，任何要求與`X-Forwarded-For`hello 服務已拒絕郵件標頭。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-160">In addition, any request with a `X-Forwarded-For` header is rejected by hello service.</span></span>
<span data-ttu-id="c9b6a-161">我們也需要要求 toocontain `Metadata: true` hello 實際要求的標頭 tooensure 直接的方式，而且不屬於預期的重新導向。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-161">We also require requests toocontain a `Metadata: true` header tooensure that hello actual request was directly intended and not a part of unintentional redirection.</span></span> 

### <a name="error"></a><span data-ttu-id="c9b6a-162">錯誤</span><span class="sxs-lookup"><span data-stu-id="c9b6a-162">Error</span></span>
<span data-ttu-id="c9b6a-163">如果找不到的資料元素或格式不正確的要求，hello 執行個體中繼資料服務會傳回標準 HTTP 錯誤。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-163">If there is a data element not found or a malformed request, hello Instance Metadata Service returns standard HTTP errors.</span></span> <span data-ttu-id="c9b6a-164">例如：</span><span class="sxs-lookup"><span data-stu-id="c9b6a-164">For example:</span></span>

<span data-ttu-id="c9b6a-165">HTTP 狀態碼</span><span class="sxs-lookup"><span data-stu-id="c9b6a-165">HTTP Status Code</span></span> | <span data-ttu-id="c9b6a-166">原因</span><span class="sxs-lookup"><span data-stu-id="c9b6a-166">Reason</span></span>
----------------|-------
<span data-ttu-id="c9b6a-167">200 確定</span><span class="sxs-lookup"><span data-stu-id="c9b6a-167">200 OK</span></span> |
<span data-ttu-id="c9b6a-168">400 不正確的要求</span><span class="sxs-lookup"><span data-stu-id="c9b6a-168">400 Bad Request</span></span> | <span data-ttu-id="c9b6a-169">遺漏 `Metadata: true` 標頭</span><span class="sxs-lookup"><span data-stu-id="c9b6a-169">Missing `Metadata: true` header</span></span>
<span data-ttu-id="c9b6a-170">404 找不到</span><span class="sxs-lookup"><span data-stu-id="c9b6a-170">404 Not Found</span></span> | <span data-ttu-id="c9b6a-171">hello 要求的項目不存在</span><span class="sxs-lookup"><span data-stu-id="c9b6a-171">hello requested element does't exist</span></span> 
<span data-ttu-id="c9b6a-172">405 不允許的方法</span><span class="sxs-lookup"><span data-stu-id="c9b6a-172">405 Method Not Allowed</span></span> | <span data-ttu-id="c9b6a-173">僅支援 `GET` 和 `POST` 要求</span><span class="sxs-lookup"><span data-stu-id="c9b6a-173">Only `GET` and `POST` requests are supported</span></span>
<span data-ttu-id="c9b6a-174">429 要求太多</span><span class="sxs-lookup"><span data-stu-id="c9b6a-174">429 Too Many Requests</span></span> | <span data-ttu-id="c9b6a-175">hello API 目前最多支援 5 每秒查詢數</span><span class="sxs-lookup"><span data-stu-id="c9b6a-175">hello API currently supports a maximum of 5 queries per second</span></span>
<span data-ttu-id="c9b6a-176">500 服務錯誤</span><span class="sxs-lookup"><span data-stu-id="c9b6a-176">500 Service Error</span></span>     | <span data-ttu-id="c9b6a-177">稍後重試</span><span class="sxs-lookup"><span data-stu-id="c9b6a-177">Retry after some time</span></span>

### <a name="examples"></a><span data-ttu-id="c9b6a-178">範例</span><span class="sxs-lookup"><span data-stu-id="c9b6a-178">Examples</span></span>

> [!NOTE] 
> <span data-ttu-id="c9b6a-179">所有 API 回應都是 JSON 字串。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-179">All API responses are JSON strings.</span></span> <span data-ttu-id="c9b6a-180">下列所有範例回應均列印清晰，很容易閱讀。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-180">All following example responses  are pretty-printed for readability.</span></span>

#### <a name="retrieving-network-information"></a><span data-ttu-id="c9b6a-181">擷取網路資訊</span><span class="sxs-lookup"><span data-stu-id="c9b6a-181">Retrieving network information</span></span>

<span data-ttu-id="c9b6a-182">**要求**</span><span class="sxs-lookup"><span data-stu-id="c9b6a-182">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

<span data-ttu-id="c9b6a-183">**回應**</span><span class="sxs-lookup"><span data-stu-id="c9b6a-183">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="c9b6a-184">hello 回應是 JSON 字串。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-184">hello response is a JSON string.</span></span> <span data-ttu-id="c9b6a-185">下列範例回應 hello 是美觀列印來提高可讀性。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-185">hello following example response is pretty-printed for readability.</span></span>

```
{
  "interface": [
    {
      "ipv4": {
        "ipAddress": [
          {
            "privateIpAddress": "10.1.0.4",
            "publicIpAddress": "X.X.X.X"
          }
        ],
        "subnet": [
          {
            "address": "10.1.0.0",
            "prefix": "24"
          }
        ]
      },
      "ipv6": {
        "ipAddress": []
      },
      "macAddress": "000D3AF806EC"
    }
  ]
}

```

#### <a name="retrieving-public-ip-address"></a><span data-ttu-id="c9b6a-186">擷取公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="c9b6a-186">Retrieving public IP address</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a><span data-ttu-id="c9b6a-187">擷取執行個體的所有中繼資料</span><span class="sxs-lookup"><span data-stu-id="c9b6a-187">Retrieving all metadata for an instance</span></span>

<span data-ttu-id="c9b6a-188">**要求**</span><span class="sxs-lookup"><span data-stu-id="c9b6a-188">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

<span data-ttu-id="c9b6a-189">**回應**</span><span class="sxs-lookup"><span data-stu-id="c9b6a-189">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="c9b6a-190">hello 回應是 JSON 字串。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-190">hello response is a JSON string.</span></span> <span data-ttu-id="c9b6a-191">下列範例回應 hello 是美觀列印來提高可讀性。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-191">hello following example response is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "westcentralus",
    "name": "IMDSSample",
    "offer": "UbuntuServer",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "Canonical",
    "sku": "16.04.0-LTS",
    "version": "16.04.201610200",
    "vmId": "5d33a910-a7a0-4443-9f01-6a807801b29b",
    "vmSize": "Standard_A1"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.1.0.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.1.0.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": []
        },
        "macAddress": "000D3AF806EC"
      }
    ]
  }
}
```

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a><span data-ttu-id="c9b6a-192">擷取 Windows 虛擬機器中的中繼資料</span><span class="sxs-lookup"><span data-stu-id="c9b6a-192">Retrieving metadata in Windows Virtual Machine</span></span>

<span data-ttu-id="c9b6a-193">**要求**</span><span class="sxs-lookup"><span data-stu-id="c9b6a-193">**Request**</span></span>

<span data-ttu-id="c9b6a-194">可以透過 hello PowerShell 公用程式在 Windows 中擷取執行個體中繼資料`curl`:</span><span class="sxs-lookup"><span data-stu-id="c9b6a-194">Instance metadata can be retrieved in Windows via hello PowerShell utility `curl`:</span></span> 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

<span data-ttu-id="c9b6a-195">或透過 hello `Invoke-RestMethod` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c9b6a-195">Or through hello `Invoke-RestMethod` cmdlet:</span></span>
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

<span data-ttu-id="c9b6a-196">**回應**</span><span class="sxs-lookup"><span data-stu-id="c9b6a-196">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="c9b6a-197">hello 回應是 JSON 字串。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-197">hello response is a JSON string.</span></span> <span data-ttu-id="c9b6a-198">下列範例回應 hello 是美觀列印來提高可讀性。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-198">hello following example response  is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "westus",
    "name": "SQLTest",
    "offer": "SQL2016SP1-WS2016",
    "osType": "Windows",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "MicrosoftSQLServer",
    "sku": "Enterprise",
    "version": "13.0.400110",
    "vmId": "453945c8-3923-4366-b2d3-ea4c80e9b70e",
    "vmSize": "Standard_DS2"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.0.1.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.0.1.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": [
            
          ]
        },
        "macAddress": "002248020E1E"
      }
    ]
  }
}
```

## <a name="instance-metadata-data-categories"></a><span data-ttu-id="c9b6a-199">執行個體中繼資料資料類別</span><span class="sxs-lookup"><span data-stu-id="c9b6a-199">Instance metadata data categories</span></span>
<span data-ttu-id="c9b6a-200">下列資料類別目錄的 hello 都是透過 hello 執行個體中繼資料服務：</span><span class="sxs-lookup"><span data-stu-id="c9b6a-200">hello following data categories are available through hello Instance Metadata Service:</span></span>

<span data-ttu-id="c9b6a-201">資料</span><span class="sxs-lookup"><span data-stu-id="c9b6a-201">Data</span></span> | <span data-ttu-id="c9b6a-202">說明</span><span class="sxs-lookup"><span data-stu-id="c9b6a-202">Description</span></span>
-----|------------
<span data-ttu-id="c9b6a-203">location</span><span class="sxs-lookup"><span data-stu-id="c9b6a-203">location</span></span> | <span data-ttu-id="c9b6a-204">Azure 區域 hello VM 正在執行</span><span class="sxs-lookup"><span data-stu-id="c9b6a-204">Azure Region hello VM is running in</span></span>
<span data-ttu-id="c9b6a-205">名稱</span><span class="sxs-lookup"><span data-stu-id="c9b6a-205">name</span></span> | <span data-ttu-id="c9b6a-206">Hello VM 的名稱</span><span class="sxs-lookup"><span data-stu-id="c9b6a-206">Name of hello VM</span></span> 
<span data-ttu-id="c9b6a-207">提供項目</span><span class="sxs-lookup"><span data-stu-id="c9b6a-207">offer</span></span> | <span data-ttu-id="c9b6a-208">提供 hello VM 映像的資訊。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-208">Offer information for hello VM image.</span></span> <span data-ttu-id="c9b6a-209">此值只會針對從 Azure 映像庫部署的映像呈現。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-209">This value is only present for images deployed from Azure image gallery.</span></span>
<span data-ttu-id="c9b6a-210">publisher</span><span class="sxs-lookup"><span data-stu-id="c9b6a-210">publisher</span></span> | <span data-ttu-id="c9b6a-211">Hello VM 映像的發行者</span><span class="sxs-lookup"><span data-stu-id="c9b6a-211">Publisher of hello VM image</span></span>
<span data-ttu-id="c9b6a-212">sku</span><span class="sxs-lookup"><span data-stu-id="c9b6a-212">sku</span></span> | <span data-ttu-id="c9b6a-213">特定 hello VM 映像的 SKU</span><span class="sxs-lookup"><span data-stu-id="c9b6a-213">Specific SKU for hello VM image</span></span>  
<span data-ttu-id="c9b6a-214">版本</span><span class="sxs-lookup"><span data-stu-id="c9b6a-214">version</span></span> | <span data-ttu-id="c9b6a-215">Hello VM 映像的版本</span><span class="sxs-lookup"><span data-stu-id="c9b6a-215">Version of hello VM image</span></span> 
<span data-ttu-id="c9b6a-216">osType</span><span class="sxs-lookup"><span data-stu-id="c9b6a-216">osType</span></span> | <span data-ttu-id="c9b6a-217">Linux 或 Windows</span><span class="sxs-lookup"><span data-stu-id="c9b6a-217">Linux or Windows</span></span> 
<span data-ttu-id="c9b6a-218">platformUpdateDomain</span><span class="sxs-lookup"><span data-stu-id="c9b6a-218">platformUpdateDomain</span></span> |  <span data-ttu-id="c9b6a-219">[更新網域](virtual-machines-windows-manage-availability.md)VM 正在執行中的 hello</span><span class="sxs-lookup"><span data-stu-id="c9b6a-219">[Update domain](virtual-machines-windows-manage-availability.md) hello VM is running in</span></span>
<span data-ttu-id="c9b6a-220">platformFaultDomain</span><span class="sxs-lookup"><span data-stu-id="c9b6a-220">platformFaultDomain</span></span> | <span data-ttu-id="c9b6a-221">[容錯網域](virtual-machines-windows-manage-availability.md)VM 正在執行中的 hello</span><span class="sxs-lookup"><span data-stu-id="c9b6a-221">[Fault domain](virtual-machines-windows-manage-availability.md) hello VM is running in</span></span>
<span data-ttu-id="c9b6a-222">vmId</span><span class="sxs-lookup"><span data-stu-id="c9b6a-222">vmId</span></span> | <span data-ttu-id="c9b6a-223">[唯一識別項](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/)hello VM</span><span class="sxs-lookup"><span data-stu-id="c9b6a-223">[Unique identifier](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) for hello VM</span></span>
<span data-ttu-id="c9b6a-224">vmSize</span><span class="sxs-lookup"><span data-stu-id="c9b6a-224">vmSize</span></span> | [<span data-ttu-id="c9b6a-225">VM 大小</span><span class="sxs-lookup"><span data-stu-id="c9b6a-225">VM size</span></span>](virtual-machines-windows-sizes.md)
<span data-ttu-id="c9b6a-226">ipv4/privateIpAddress</span><span class="sxs-lookup"><span data-stu-id="c9b6a-226">ipv4/privateIpAddress</span></span> | <span data-ttu-id="c9b6a-227">Hello VM 本機 IPv4 位址</span><span class="sxs-lookup"><span data-stu-id="c9b6a-227">Local IPv4 address of hello VM</span></span> 
<span data-ttu-id="c9b6a-228">ipv4/publicIpAddress</span><span class="sxs-lookup"><span data-stu-id="c9b6a-228">ipv4/publicIpAddress</span></span> | <span data-ttu-id="c9b6a-229">Hello VM 的公用 IPv4 位址</span><span class="sxs-lookup"><span data-stu-id="c9b6a-229">Public IPv4 address of hello VM</span></span>
<span data-ttu-id="c9b6a-230">subnet/address</span><span class="sxs-lookup"><span data-stu-id="c9b6a-230">subnet/address</span></span> | <span data-ttu-id="c9b6a-231">Hello VM 子網路位址</span><span class="sxs-lookup"><span data-stu-id="c9b6a-231">Subnet address of hello VM</span></span>
<span data-ttu-id="c9b6a-232">subnet/prefix</span><span class="sxs-lookup"><span data-stu-id="c9b6a-232">subnet/prefix</span></span> | <span data-ttu-id="c9b6a-233">子網路首碼，範例 24</span><span class="sxs-lookup"><span data-stu-id="c9b6a-233">Subnet prefix, example 24</span></span>
<span data-ttu-id="c9b6a-234">ipv6/ipAddress</span><span class="sxs-lookup"><span data-stu-id="c9b6a-234">ipv6/ipAddress</span></span> | <span data-ttu-id="c9b6a-235">Hello VM 本機 IPv6 位址</span><span class="sxs-lookup"><span data-stu-id="c9b6a-235">Local IPv6 address of hello VM</span></span>
<span data-ttu-id="c9b6a-236">macAddress</span><span class="sxs-lookup"><span data-stu-id="c9b6a-236">macAddress</span></span> | <span data-ttu-id="c9b6a-237">VM mac 位址</span><span class="sxs-lookup"><span data-stu-id="c9b6a-237">VM mac address</span></span> 
<span data-ttu-id="c9b6a-238">scheduledevents</span><span class="sxs-lookup"><span data-stu-id="c9b6a-238">scheduledevents</span></span> | <span data-ttu-id="c9b6a-239">目前為公開預覽版，請參閱 [scheduledevents](virtual-machines-scheduled-events.md)</span><span class="sxs-lookup"><span data-stu-id="c9b6a-239">Currently in Public Preview See [scheduledevents](virtual-machines-scheduled-events.md)</span></span>

## <a name="example-scenarios-for-usage"></a><span data-ttu-id="c9b6a-240">使用方式的範例案例</span><span class="sxs-lookup"><span data-stu-id="c9b6a-240">Example Scenarios for usage</span></span>  

### <a name="tracking-vm-running-on-azure"></a><span data-ttu-id="c9b6a-241">追蹤在 Azure 上執行的 VM</span><span class="sxs-lookup"><span data-stu-id="c9b6a-241">Tracking VM running on Azure</span></span>

<span data-ttu-id="c9b6a-242">做為服務提供者，您可能需要執行您的軟體的 Vm tootrack hello 數目或有需要唯一性 tootrack hello VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-242">As a service provider, you may require tootrack hello number of VMs running your software or have agents that need tootrack uniqueness of hello VM.</span></span> <span data-ttu-id="c9b6a-243">toobe 無法 tooget 的唯一識別碼，讓 VM 時，使用 hello`vmId`欄位從 執行個體中繼資料服務。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-243">toobe able tooget a unique ID for a VM, use hello `vmId` field from Instance Metadata Service.</span></span>

<span data-ttu-id="c9b6a-244">**要求**</span><span class="sxs-lookup"><span data-stu-id="c9b6a-244">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

<span data-ttu-id="c9b6a-245">**回應**</span><span class="sxs-lookup"><span data-stu-id="c9b6a-245">**Response**</span></span>

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a><span data-ttu-id="c9b6a-246">容器的位置，資料分割基礎容錯/更新網域</span><span class="sxs-lookup"><span data-stu-id="c9b6a-246">Placement of containers, data-partitions based Fault/Update domain</span></span> 

<span data-ttu-id="c9b6a-247">對於特定案例，不同資料複本的放置相當重要。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-247">For certain scenarios, placement of different data replicas is of prime importance.</span></span> <span data-ttu-id="c9b6a-248">例如， [HDFS 複本放置](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps)或透過容器位置[orchestrator](https://kubernetes.io/docs/user-guide/node-selection/)可能需要 tooknow hello`platformFaultDomain`和`platformUpdateDomain`hello VM 執行。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-248">For example, [HDFS replica placement](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) or container placement via an [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) may you require tooknow hello `platformFaultDomain` and `platformUpdateDomain` hello VM is running on.</span></span>
<span data-ttu-id="c9b6a-249">您可以查詢此資料直接透過 hello 執行個體中繼資料服務。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-249">You can query this data directly via hello Instance Metadata Service.</span></span>

<span data-ttu-id="c9b6a-250">**要求**</span><span class="sxs-lookup"><span data-stu-id="c9b6a-250">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

<span data-ttu-id="c9b6a-251">**回應**</span><span class="sxs-lookup"><span data-stu-id="c9b6a-251">**Response**</span></span>

```
0
```

### <a name="getting-more-information-about-hello-vm-during-support-case"></a><span data-ttu-id="c9b6a-252">取得支援案例期間 hello VM 之詳細資訊</span><span class="sxs-lookup"><span data-stu-id="c9b6a-252">Getting more information about hello VM during support case</span></span> 

<span data-ttu-id="c9b6a-253">做為服務提供者，您可能會收到支援呼叫您要放置 tooknow hello VM 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-253">As a service provider, you may get a support call where you would like tooknow more information about hello VM.</span></span> <span data-ttu-id="c9b6a-254">詢問 hello 客戶 tooshare hello 計算中繼資料可提供基本資訊的 hello 支援專業人員 tooknow hello 種 VM 在 Azure 上。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-254">Asking hello customer tooshare hello compute metadata can provide basic information for hello support professional tooknow about hello kind of VM on Azure.</span></span> 

<span data-ttu-id="c9b6a-255">**要求**</span><span class="sxs-lookup"><span data-stu-id="c9b6a-255">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

<span data-ttu-id="c9b6a-256">**回應**</span><span class="sxs-lookup"><span data-stu-id="c9b6a-256">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="c9b6a-257">hello 回應是 JSON 字串。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-257">hello response is a JSON string.</span></span> <span data-ttu-id="c9b6a-258">下列範例回應 hello 是美觀列印來提高可讀性。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-258">hello following example response is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "CentralUS",
    "name": "IMDSCanary",
    "offer": "RHEL",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "RedHat",
    "sku": "7.2",
    "version": "7.2.20161026",
    "vmId": "5c08b38e-4d57-4c23-ac45-aca61037f084",
    "vmSize": "Standard_DS2"
  }
}
```

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-hello-vm"></a><span data-ttu-id="c9b6a-259">呼叫使用 hello VM 內的不同語言的中繼資料服務的範例</span><span class="sxs-lookup"><span data-stu-id="c9b6a-259">Examples of calling metadata service using different languages inside hello VM</span></span> 

<span data-ttu-id="c9b6a-260">語言</span><span class="sxs-lookup"><span data-stu-id="c9b6a-260">Language</span></span> | <span data-ttu-id="c9b6a-261">範例</span><span class="sxs-lookup"><span data-stu-id="c9b6a-261">Example</span></span> 
---------|----------------
<span data-ttu-id="c9b6a-262">Ruby</span><span class="sxs-lookup"><span data-stu-id="c9b6a-262">Ruby</span></span>     | <span data-ttu-id="c9b6a-263">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span><span class="sxs-lookup"><span data-stu-id="c9b6a-263">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span></span>
<span data-ttu-id="c9b6a-264">Go Lan</span><span class="sxs-lookup"><span data-stu-id="c9b6a-264">Go Lan</span></span>   | <span data-ttu-id="c9b6a-265">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span><span class="sxs-lookup"><span data-stu-id="c9b6a-265">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span></span>            
<span data-ttu-id="c9b6a-266">Python</span><span class="sxs-lookup"><span data-stu-id="c9b6a-266">python</span></span>   | <span data-ttu-id="c9b6a-267">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span><span class="sxs-lookup"><span data-stu-id="c9b6a-267">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span></span>
<span data-ttu-id="c9b6a-268">C++</span><span class="sxs-lookup"><span data-stu-id="c9b6a-268">C++</span></span>      | <span data-ttu-id="c9b6a-269">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span><span class="sxs-lookup"><span data-stu-id="c9b6a-269">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span></span>
<span data-ttu-id="c9b6a-270">C#</span><span class="sxs-lookup"><span data-stu-id="c9b6a-270">C#</span></span>       | <span data-ttu-id="c9b6a-271">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span><span class="sxs-lookup"><span data-stu-id="c9b6a-271">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span></span>
<span data-ttu-id="c9b6a-272">Javascript</span><span class="sxs-lookup"><span data-stu-id="c9b6a-272">Javascript</span></span> | <span data-ttu-id="c9b6a-273">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span><span class="sxs-lookup"><span data-stu-id="c9b6a-273">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span></span>
<span data-ttu-id="c9b6a-274">Powershell</span><span class="sxs-lookup"><span data-stu-id="c9b6a-274">Powershell</span></span> | <span data-ttu-id="c9b6a-275">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span><span class="sxs-lookup"><span data-stu-id="c9b6a-275">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span></span>
<span data-ttu-id="c9b6a-276">Bash</span><span class="sxs-lookup"><span data-stu-id="c9b6a-276">Bash</span></span>       | <span data-ttu-id="c9b6a-277">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span><span class="sxs-lookup"><span data-stu-id="c9b6a-277">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span></span>
    

## <a name="faq"></a><span data-ttu-id="c9b6a-278">常見問題集</span><span class="sxs-lookup"><span data-stu-id="c9b6a-278">FAQ</span></span>
1. <span data-ttu-id="c9b6a-279">我收到 hello 錯誤`400 Bad Request, Required metadata header not specified`。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-279">I am getting hello error `400 Bad Request, Required metadata header not specified`.</span></span> <span data-ttu-id="c9b6a-280">這代表什麼？</span><span class="sxs-lookup"><span data-stu-id="c9b6a-280">What does this mean?</span></span>
   * <span data-ttu-id="c9b6a-281">hello 執行個體中繼資料服務需要 hello 標頭`Metadata: true`toobe 傳入 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-281">hello Instance Metadata Service requires hello header `Metadata: true` toobe passed in hello request.</span></span> <span data-ttu-id="c9b6a-282">在 hello REST 呼叫中傳遞此標頭可讓存取 toohello 執行個體中繼資料服務。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-282">Passing this header in hello REST call allows access toohello Instance Metadata Service.</span></span> 
2. <span data-ttu-id="c9b6a-283">為什麼我沒有收到我的 VM 計算資訊？</span><span class="sxs-lookup"><span data-stu-id="c9b6a-283">Why am I not getting compute information for my VM?</span></span>
   * <span data-ttu-id="c9b6a-284">目前執行個體中繼資料服務的 hello 僅支援使用 Azure Resource Manager 建立的執行個體。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-284">Currently hello Instance Metadata Service only supports instances created with Azure Resource Manager.</span></span> <span data-ttu-id="c9b6a-285">在 hello 未來，我們可能會加入雲端服務 Vm 的支援。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-285">In hello future, we may add support for Cloud Service VMs.</span></span>
3. <span data-ttu-id="c9b6a-286">我在一陣子之後回過頭來透過 Azure Resource Manager 建立我的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-286">I created my Virtual Machine through Azure Resource Manager a while back.</span></span> <span data-ttu-id="c9b6a-287">為什麼我看不到計算中繼資料資訊？</span><span class="sxs-lookup"><span data-stu-id="c9b6a-287">Why am I not see compute metadata information?</span></span>
   * <span data-ttu-id="c9b6a-288">對於任何 2016 年 9 月之後建立的 Vm，新增[標記](../azure-resource-manager/resource-group-using-tags.md)toostart 文件都看到計算中繼資料。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-288">For any VMs created after Sep 2016, add a [Tag](../azure-resource-manager/resource-group-using-tags.md) toostart seeing compute metadata.</span></span> <span data-ttu-id="c9b6a-289">對於較舊的 Vm （2016 年 9 月之前建立），新增/移除延伸模組或資料磁碟 toohello VM toorefresh 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-289">For older VMs (created before Sep 2016), add/remove extensions or data disks toohello VM toorefresh metadata.</span></span>
4. <span data-ttu-id="c9b6a-290">為什麼我會收到 hello 錯誤`500 Internal Server Error`？</span><span class="sxs-lookup"><span data-stu-id="c9b6a-290">Why am I getting hello error `500 Internal Server Error`?</span></span>
   * <span data-ttu-id="c9b6a-291">請根據指數型輪詢系統重試您的要求。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-291">Please retry your request based on exponential back off system.</span></span> <span data-ttu-id="c9b6a-292">如果 hello 問題持續發生，請連絡 Azure 支援。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-292">If hello issue persists contact  Azure support.</span></span>
5. <span data-ttu-id="c9b6a-293">我要在哪裡共用其他問題/註解？</span><span class="sxs-lookup"><span data-stu-id="c9b6a-293">Where do I share additional questions/comments?</span></span>
   * <span data-ttu-id="c9b6a-294">請在 http://feedback.azure.com 上傳送您的註解。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-294">Send your comments on http://feedback.azure.com.</span></span>
7. <span data-ttu-id="c9b6a-295">這是否適用於虛擬機器擴展集執行個體？</span><span class="sxs-lookup"><span data-stu-id="c9b6a-295">Would this work for Virtual Machine Scale Set Instance?</span></span>
   * <span data-ttu-id="c9b6a-296">是，中繼資料服務適用於擴展集執行個體。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-296">Yes Metadata service is available for Scale Set Instances.</span></span> 
6. <span data-ttu-id="c9b6a-297">如何在 hello 服務取得支援？</span><span class="sxs-lookup"><span data-stu-id="c9b6a-297">How do I get support for hello service?</span></span>
   * <span data-ttu-id="c9b6a-298">hello 服務 tooget 支援 hello VM，您不能 tooget 中繼資料回應長時間重試後的 Azure 入口網站中建立的支援問題</span><span class="sxs-lookup"><span data-stu-id="c9b6a-298">tooget support for hello service, create a support issue in Azure portal for hello VM where you are not able tooget metadata response after long retries</span></span> 

   ![執行個體中繼資料支援](./media/virtual-machines-instancemetadataservice-overview/InstanceMetadata-support.png)
    
## <a name="next-steps"></a><span data-ttu-id="c9b6a-300">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c9b6a-300">Next Steps</span></span>

- <span data-ttu-id="c9b6a-301">深入了解 hello [scheduledevents](virtual-machines-scheduled-events.md) API**在公開預覽**hello 執行個體中繼資料服務所提供。</span><span class="sxs-lookup"><span data-stu-id="c9b6a-301">Learn more about hello [scheduledevents](virtual-machines-scheduled-events.md) API **In Public Preview** provided by hello Instance Metadata Service.</span></span>
