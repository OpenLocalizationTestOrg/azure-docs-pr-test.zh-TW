---
title: "aaaNetwork 資源提供者概觀 |Microsoft 文件"
description: "深入了解 hello 新的網路資源提供者在 「 Azure 資源管理員"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 79bf09da-4809-45cb-8d21-705616ef24dc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 81b8f51fe8ee180d8f7885c6e04eb953904d7be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="network-resource-provider"></a><span data-ttu-id="91260-103">網路資源提供者</span><span class="sxs-lookup"><span data-stu-id="91260-103">Network Resource Provider</span></span>
<span data-ttu-id="91260-104">支柱需要在今天的商務成就，是 hello 能力 toobuild 和敏捷式軟體開發、 彈性、 安全和可重複的方式來管理大規模的網路應用程式。</span><span class="sxs-lookup"><span data-stu-id="91260-104">An underpinning need in today’s business success, is hello ability toobuild and manage large scale network aware applications in an agile, flexible, secure and repeatable way.</span></span> <span data-ttu-id="91260-105">Azure 資源管理員可讓您 toocreate 這類應用程式，當做單一集合的資源群組中的資源。</span><span class="sxs-lookup"><span data-stu-id="91260-105">Azure Resource Manager enables you toocreate such applications, as a single collection of resources in resource groups.</span></span> <span data-ttu-id="91260-106">管理這類資源時，是透過 Resource Manager 底下的各種資源提供者進行管理。</span><span class="sxs-lookup"><span data-stu-id="91260-106">Such resources are managed through various resource providers under Resource Manager.</span></span>

<span data-ttu-id="91260-107">Azure 資源管理員必須使用不同的資源提供者 tooprovide 存取 tooyour 資源。</span><span class="sxs-lookup"><span data-stu-id="91260-107">Azure Resource Manager relies on different resource providers tooprovide access tooyour resources.</span></span> <span data-ttu-id="91260-108">有三個主要的資源提供者：網路、儲存體和運算。</span><span class="sxs-lookup"><span data-stu-id="91260-108">There are three main resource providers: Network, Storage and Compute.</span></span> <span data-ttu-id="91260-109">本文將討論 hello 特性和 hello 網路的資源提供者的優點包括：</span><span class="sxs-lookup"><span data-stu-id="91260-109">This document discusses hello characteristics and benefits of hello Network Resource Provider, including:</span></span>

* <span data-ttu-id="91260-110">**中繼資料**– 您可以新增資訊 tooresources 使用標記。</span><span class="sxs-lookup"><span data-stu-id="91260-110">**Metadata** – you can add information tooresources using tags.</span></span> <span data-ttu-id="91260-111">這些標記也有使用的 tootrack 資源使用量的資源群組和訂閱。</span><span class="sxs-lookup"><span data-stu-id="91260-111">These tags can be used tootrack resource utilization across resource groups and subscriptions.</span></span>
* <span data-ttu-id="91260-112">**更進一步控制網路** - 網路資源是進行鬆散偶合，而您可以更精密地控制它們。</span><span class="sxs-lookup"><span data-stu-id="91260-112">**Greater control of your network** - network resources are loosely coupled and you can control them in a more granular fashion.</span></span> <span data-ttu-id="91260-113">這表示您可以更靈活地管理 hello 網路資源。</span><span class="sxs-lookup"><span data-stu-id="91260-113">This means you have more flexibility in managing hello networking resources.</span></span>
* <span data-ttu-id="91260-114">**設定更快速** - 因為網路資源是進行鬆散偶合，所以您可以平行建立並協調網路資源。</span><span class="sxs-lookup"><span data-stu-id="91260-114">**Faster configuration** - because network resources are loosely coupled, you can create and orchestrate network resources in parallel.</span></span> <span data-ttu-id="91260-115">這已經大幅減少設定時間。</span><span class="sxs-lookup"><span data-stu-id="91260-115">This has drastically reduced configuration time.</span></span>
* <span data-ttu-id="91260-116">**Role Based Access Control** -RBAC 提供預設的角色，與特定安全性範圍，在加法 tooallowing hello 建立自訂的角色，安全管理。</span><span class="sxs-lookup"><span data-stu-id="91260-116">**Role Based Access Control** - RBAC provides default roles, with specific security scope, in addition tooallowing hello creation of custom roles for secure management.</span></span>
* <span data-ttu-id="91260-117">**更容易管理和部署**-它是更容易 toodeploy 和管理應用程式，因為您可以可以當做單一集合的資源群組中的資源建立整個應用程式堆疊。</span><span class="sxs-lookup"><span data-stu-id="91260-117">**Easier management and deployment** - it’s easier toodeploy and manage applications since you can can create an entire application stack as a single collection of resources in a resource group.</span></span> <span data-ttu-id="91260-118">和更快的 toodeploy，因為您可以部署只提供範本的 JSON 裝載。</span><span class="sxs-lookup"><span data-stu-id="91260-118">And faster toodeploy, since you can deploy by simply providing a template JSON payload.</span></span>
* <span data-ttu-id="91260-119">**快速自訂**-您可以使用宣告式樣式範本 tooenable 可重複且快速自訂部署。</span><span class="sxs-lookup"><span data-stu-id="91260-119">**Rapid customization** - you can use declarative-style templates tooenable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="91260-120">**可重複自訂**-您可以使用宣告式樣式範本 tooenable 可重複且快速自訂部署。</span><span class="sxs-lookup"><span data-stu-id="91260-120">**Repeatable customization** - you can use declarative-style templates tooenable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="91260-121">**管理介面**-您可以使用任何下列介面 toomanage hello 資源：</span><span class="sxs-lookup"><span data-stu-id="91260-121">**Management interfaces** - you can use any of hello following interfaces toomanage your resources:</span></span>
  * <span data-ttu-id="91260-122">REST 型 API</span><span class="sxs-lookup"><span data-stu-id="91260-122">REST based API</span></span>
  * <span data-ttu-id="91260-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="91260-123">PowerShell</span></span>
  * <span data-ttu-id="91260-124">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="91260-124">.NET SDK</span></span>
  * <span data-ttu-id="91260-125">Node.JS SDK</span><span class="sxs-lookup"><span data-stu-id="91260-125">Node.JS SDK</span></span>
  * <span data-ttu-id="91260-126">Java SDK</span><span class="sxs-lookup"><span data-stu-id="91260-126">Java SDK</span></span>
  * <span data-ttu-id="91260-127">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="91260-127">Azure CLI</span></span>
  * <span data-ttu-id="91260-128">預覽入口網站</span><span class="sxs-lookup"><span data-stu-id="91260-128">Preview Portal</span></span>
  * <span data-ttu-id="91260-129">Resource Manager 範本語言</span><span class="sxs-lookup"><span data-stu-id="91260-129">Resource Manager template language</span></span>

## <a name="network-resources"></a><span data-ttu-id="91260-130">網路資源</span><span class="sxs-lookup"><span data-stu-id="91260-130">Network resources</span></span>
<span data-ttu-id="91260-131">您現在可以獨立地管理網路資源，而不是透過單一計算資源 (虛擬機器) 進行管理。</span><span class="sxs-lookup"><span data-stu-id="91260-131">You can now manage network resources independently, instead of having them all managed through a single compute resource (a virtual machine).</span></span> <span data-ttu-id="91260-132">這確保具有較高程度的彈性和靈活性可在資源群組中撰寫複雜且大型的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="91260-132">This ensures a higher degree of flexibility and agility in composing a complex and large scale infrastructure in a resource group.</span></span>

<span data-ttu-id="91260-133">含有多介層應用程式之範例部署的概念檢視顯示如下。</span><span class="sxs-lookup"><span data-stu-id="91260-133">A conceptual view of a sample deployment involving a multi-tiered application is presented below.</span></span> <span data-ttu-id="91260-134">您看到的每項資源 (如 NIC、公用 IP 位址和 VM 等) 都可以分開管理。</span><span class="sxs-lookup"><span data-stu-id="91260-134">Each resource you see, such as NICs, public IP addresses, and VMs, can be managed independently.</span></span>

![網路資源模型](./media/resource-groups-networking/Figure2.png)

<span data-ttu-id="91260-136">每項資源均包含一組通用屬性，以及其個別的屬性集。</span><span class="sxs-lookup"><span data-stu-id="91260-136">Every resource contains a common set of properties, and their individual property set.</span></span> <span data-ttu-id="91260-137">hello 的通用屬性包括：</span><span class="sxs-lookup"><span data-stu-id="91260-137">hello common properties are:</span></span>

| <span data-ttu-id="91260-138">屬性</span><span class="sxs-lookup"><span data-stu-id="91260-138">Property</span></span> | <span data-ttu-id="91260-139">說明</span><span class="sxs-lookup"><span data-stu-id="91260-139">Description</span></span> | <span data-ttu-id="91260-140">範例值</span><span class="sxs-lookup"><span data-stu-id="91260-140">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="91260-141">**name**</span><span class="sxs-lookup"><span data-stu-id="91260-141">**name**</span></span> |<span data-ttu-id="91260-142">唯一的資源名稱。</span><span class="sxs-lookup"><span data-stu-id="91260-142">Unique resource name.</span></span> <span data-ttu-id="91260-143">每個資源類型都有自己的命名限制。</span><span class="sxs-lookup"><span data-stu-id="91260-143">Each resource type has its own naming restrictions.</span></span> |<span data-ttu-id="91260-144">PIP01、VM01、NIC01</span><span class="sxs-lookup"><span data-stu-id="91260-144">PIP01, VM01, NIC01</span></span> |
| <span data-ttu-id="91260-145">**位置**</span><span class="sxs-lookup"><span data-stu-id="91260-145">**location**</span></span> |<span data-ttu-id="91260-146">Azure 中的 hello 資源所在的區域</span><span class="sxs-lookup"><span data-stu-id="91260-146">Azure region in which hello resource resides</span></span> |<span data-ttu-id="91260-147">westus、eastus</span><span class="sxs-lookup"><span data-stu-id="91260-147">westus, eastus</span></span> |
| <span data-ttu-id="91260-148">**id**</span><span class="sxs-lookup"><span data-stu-id="91260-148">**id**</span></span> |<span data-ttu-id="91260-149">唯一的 URI 型識別</span><span class="sxs-lookup"><span data-stu-id="91260-149">Unique URI based identification</span></span> |<span data-ttu-id="91260-150">/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span><span class="sxs-lookup"><span data-stu-id="91260-150">/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span></span> |

<span data-ttu-id="91260-151">您可以檢查 hello 個別 hello 的以下各節中的資源屬性。</span><span class="sxs-lookup"><span data-stu-id="91260-151">You can check hello individual properties of resources in hello sections below.</span></span>

[!INCLUDE [virtual-networks-nrp-pip-include](../../includes/virtual-networks-nrp-pip-include.md)]

[!INCLUDE [virtual-networks-nrp-nic-include](../../includes/virtual-networks-nrp-nic-include.md)]

[!INCLUDE [virtual-networks-nrp-nsg-include](../../includes/virtual-networks-nrp-nsg-include.md)]

[!INCLUDE [virtual-networks-nrp-udr-include](../../includes/virtual-networks-nrp-udr-include.md)]

[!INCLUDE [virtual-networks-nrp-vnet-include](../../includes/virtual-networks-nrp-vnet-include.md)]

[!INCLUDE [virtual-networks-nrp-dns-include](../../includes/virtual-networks-nrp-dns-include.md)]

[!INCLUDE [virtual-networks-nrp-lb-include](../../includes/virtual-networks-nrp-lb-include.md)]

[!INCLUDE [virtual-networks-nrp-appgw-include](../../includes/virtual-networks-nrp-appgw-include.md)]

[!INCLUDE [virtual-networks-nrp-vpn-include](../../includes/virtual-networks-nrp-vpn-include.md)]

[!INCLUDE [virtual-networks-nrp-tm-include](../../includes/virtual-networks-nrp-tm-include.md)]

## <a name="management-interfaces"></a><span data-ttu-id="91260-152">管理介面</span><span class="sxs-lookup"><span data-stu-id="91260-152">Management interfaces</span></span>
<span data-ttu-id="91260-153">您可以使用不同的介面管理您的 Azure 網路資源。</span><span class="sxs-lookup"><span data-stu-id="91260-153">You can manage your Azure networking resources using different interfaces.</span></span> <span data-ttu-id="91260-154">在本文件中，我們將著重在指引這些介面：REST API 和範本。</span><span class="sxs-lookup"><span data-stu-id="91260-154">In this document we will focus on tow of those interfaces: REST API, and templates.</span></span>

### <a name="rest-api"></a><span data-ttu-id="91260-155">REST API</span><span class="sxs-lookup"><span data-stu-id="91260-155">REST API</span></span>
<span data-ttu-id="91260-156">如前所述，網路資源可以透過各種介面進行管理，包括 REST API、.NET SDK、Node.JS SDK、Java SDK、PowerShell、CLI、Azure 入口網站和範本。</span><span class="sxs-lookup"><span data-stu-id="91260-156">As mentioned earlier, network resources can be managed via a variety of interfaces, including REST API,.NET SDK, Node.JS SDK, Java SDK, PowerShell, CLI, Azure Portal and templates.</span></span>

<span data-ttu-id="91260-157">hello Rest API 的符合 toohello HTTP 1.1 通訊協定規格。</span><span class="sxs-lookup"><span data-stu-id="91260-157">hello Rest API’s conform toohello HTTP 1.1 protocol specification.</span></span> <span data-ttu-id="91260-158">下列顯示 hello 一般 URI 結構 hello API:</span><span class="sxs-lookup"><span data-stu-id="91260-158">hello general URI structure of hello API is presented below:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/providers/{resource-provider-namespace}/locations/{region-location}/register?api-version={api-version}

<span data-ttu-id="91260-159">和大括號中的 hello 參數代表 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="91260-159">And hello parameters in braces represent hello following elements:</span></span>

* <span data-ttu-id="91260-160">**subscription-id** - Azure 訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="91260-160">**subscription-id** - your Azure subscription id.</span></span>
* <span data-ttu-id="91260-161">**資源提供者命名空間**-hello 所使用的提供者的命名空間。</span><span class="sxs-lookup"><span data-stu-id="91260-161">**resource-provider-namespace** - namespace for hello provider being used.</span></span> <span data-ttu-id="91260-162">hello hello 網路資源提供者的值是*Microsoft.Network*。</span><span class="sxs-lookup"><span data-stu-id="91260-162">hello value for hello network resource provider is *Microsoft.Network*.</span></span>
* <span data-ttu-id="91260-163">**區域名稱**-hello Azure 區域名稱</span><span class="sxs-lookup"><span data-stu-id="91260-163">**region-name** - hello Azure region name</span></span>

<span data-ttu-id="91260-164">hello HTTP 支援下列方法進行呼叫 toohello REST API 時：</span><span class="sxs-lookup"><span data-stu-id="91260-164">hello following HTTP methods are supported when making calls toohello REST API:</span></span>

* <span data-ttu-id="91260-165">**PUT** -用 toocreate 指定類型的資源會修改資源屬性，或變更資源之間的關聯。</span><span class="sxs-lookup"><span data-stu-id="91260-165">**PUT** - used toocreate a resource of a given type, modify a resource property or change an association between resources.</span></span>
* <span data-ttu-id="91260-166">**取得**-tooretrieve 資訊用於佈建的資源。</span><span class="sxs-lookup"><span data-stu-id="91260-166">**GET** - used tooretrieve information for a provisioned resource.</span></span>
* <span data-ttu-id="91260-167">**刪除**-使用 toodelete 現有的資源。</span><span class="sxs-lookup"><span data-stu-id="91260-167">**DELETE** - used toodelete an existing resource.</span></span>

<span data-ttu-id="91260-168">Hello 要求和回應符合 tooa JSON 裝載格式。</span><span class="sxs-lookup"><span data-stu-id="91260-168">Both hello request and response conform tooa JSON payload format.</span></span> <span data-ttu-id="91260-169">如需詳細資料，請參閱 [Azure 資源管理 API](https://msdn.microsoft.com/library/azure/dn948464.aspx)。</span><span class="sxs-lookup"><span data-stu-id="91260-169">For more details, see [Azure Resource Management APIs](https://msdn.microsoft.com/library/azure/dn948464.aspx).</span></span>

### <a name="resource-manager-template-language"></a><span data-ttu-id="91260-170">Resource Manager 範本語言</span><span class="sxs-lookup"><span data-stu-id="91260-170">Resource Manager template language</span></span>
<span data-ttu-id="91260-171">在加法 toomanaging 資源以命令方式 （透過應用程式開發介面或 SDK） 中，您也可以使用宣告式程式設計樣式 toobuild 和管理網路資源使用資源管理員範本語言 hello。</span><span class="sxs-lookup"><span data-stu-id="91260-171">In addition toomanaging resources imperatively (via APIs or SDK), you can also use a declarative programming style toobuild and manage network resources by using hello Resource Manager Template Language.</span></span>

<span data-ttu-id="91260-172">範本的範例表示法提供如下 –</span><span class="sxs-lookup"><span data-stu-id="91260-172">A sample representation of a template is provided below –</span></span>

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "<version-number-of-template>",
      "parameters": { <parameter-definitions-of-template> },
      "variables": { <variable-definitions-of-template> },
      "resources": [ { <definition-of-resource-to-deploy> } ],
      "outputs": { <output-of-template> }    
    }

<span data-ttu-id="91260-173">hello 範本是主要的 JSON 描述 hello 資源和透過參數插入 hello 執行個體的值。</span><span class="sxs-lookup"><span data-stu-id="91260-173">hello template is primarily a JSON description of hello resources and hello instance values injected via parameters.</span></span> <span data-ttu-id="91260-174">下列的 hello 範例可以使用的 toocreate 具有 2 的子網路的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="91260-174">hello example below can be used toocreate a virtual network with 2 subnets.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/VNET.json",
        "contentVersion": "1.0.0.0",
        "parameters" : {
          "location": {
            "type": "String",
            "allowedValues": ["East US", "West US", "West Europe", "East Asia", "South East Asia"],
            "metadata" : {
              "Description" : "Deployment location"
            }
          },
          "virtualNetworkName":{
            "type" : "string",
            "defaultValue":"myVNET",
            "metadata" : {
              "Description" : "VNET name"
            }
          },
          "addressPrefix":{
            "type" : "string",
            "defaultValue" : "10.0.0.0/16",
            "metadata" : {
              "Description" : "Address prefix"
            }

          },
          "subnet1Name": {
            "type" : "string",
            "defaultValue" : "Subnet-1",
            "metadata" : {
              "Description" : "Subnet 1 Name"
            }
          },
          "subnet2Name": {
            "type" : "string",
            "defaultValue" : "Subnet-2",
            "metadata" : {
              "Description" : "Subnet 2 name"
            }
          },
          "subnet1Prefix" : {
            "type" : "string",
            "defaultValue" : "10.0.0.0/24",
            "metadata" : {
              "Description" : "Subnet 1 Prefix"
            }
          },
          "subnet2Prefix" : {
            "type" : "string",
            "defaultValue" : "10.0.1.0/24",
            "metadata" : {
              "Description" : "Subnet 2 Prefix"
            }
          }
        },
        "resources": [
        {
          "apiVersion": "2015-05-01-preview",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "[parameters('virtualNetworkName')]",
          "location": "[parameters('location')]",
          "properties": {
            "addressSpace": {
              "addressPrefixes": [
                "[parameters('addressPrefix')]"
              ]
            },
            "subnets": [
              {
                "name": "[parameters('subnet1Name')]",
                "properties" : {
                  "addressPrefix": "[parameters('subnet1Prefix')]"
                }
              },
              {
                "name": "[parameters('subnet2Name')]",
                "properties" : {
                  "addressPrefix": "[parameters('subnet2Prefix')]"
                }
              }
            ]
          }
        }
        ]
    }

<span data-ttu-id="91260-175">您擁有 hello 選項時使用範本，以手動方式提供 hello 參數值，或者您可以使用參數檔案。</span><span class="sxs-lookup"><span data-stu-id="91260-175">You have hello option of providing hello parameter values manually when using a template, or you can use a parameter file.</span></span> <span data-ttu-id="91260-176">hello 下面範例會顯示一組可能的參數值 toobe 上述 hello 範本搭配使用：</span><span class="sxs-lookup"><span data-stu-id="91260-176">hello example below shows a possible set of parameter values toobe used with hello template above:</span></span>

    {
      "location": {
          "value": "East US"
      },
      "virtualNetworkName": {
          "value": "VNET1"
      },
      "subnet1Name": {
          "value": "Subnet1"
      },
      "subnet2Name": {
          "value": "Subnet2"
      },
      "addressPrefix": {
          "value": "192.168.0.0/16"
      },
      "subnet1Prefix": {
          "value": "192.168.1.0/24"
      },
      "subnet2Prefix": {
          "value": "192.168.2.0/24"
      }
    }


<span data-ttu-id="91260-177">hello 的使用範本的主要優點包括：</span><span class="sxs-lookup"><span data-stu-id="91260-177">hello main advantages of using templates are:</span></span>

* <span data-ttu-id="91260-178">您可以透過宣告樣式在資源群組中建置複雜的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="91260-178">You can build a complex infrastructure in a resource group in a declarative style.</span></span> <span data-ttu-id="91260-179">hello 建立 hello 資源，包括相依性管理的協調流程會處理由資源管理員。</span><span class="sxs-lookup"><span data-stu-id="91260-179">hello orchestration of creating hello resources, including dependency management, is handled by Resource Manager.</span></span>
* <span data-ttu-id="91260-180">hello 基礎結構可以建立可重複的方式在各個區域和區域內只要變更參數。</span><span class="sxs-lookup"><span data-stu-id="91260-180">hello infrastructure can be created in a repeatable way across various regions and within a region by simply changing parameters.</span></span>
* <span data-ttu-id="91260-181">hello 宣告式方法會導致 tooshorter 前置重疊時間建置 hello 範本與推出 hello 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="91260-181">hello declarative style leads tooshorter lead time in building hello templates and rolling out hello infrastructure.</span></span>

<span data-ttu-id="91260-182">如需範例範本，請參閱 [Azure 快速入門範本](https://github.com/Azure/azure-quickstart-templates)。</span><span class="sxs-lookup"><span data-stu-id="91260-182">For sample templates, see [Azure quickstart templates](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="91260-183">如需有關 hello 資源管理員範本語言的詳細資訊，請參閱[Azure 資源管理員範本語言](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="91260-183">For more information on hello Resource Manager Template Language, see [Azure Resource Manager Template Language](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="91260-184">hello 虛擬網路和子網路資源，則會使用上述的 hello 範例範本。</span><span class="sxs-lookup"><span data-stu-id="91260-184">hello sample template above uses hello virtual network and subnet resources.</span></span> <span data-ttu-id="91260-185">下列是其他您可以使用的網路資源：</span><span class="sxs-lookup"><span data-stu-id="91260-185">There are other network resources you can use as listed below:</span></span>

### <a name="using-a-template"></a><span data-ttu-id="91260-186">使用範本</span><span class="sxs-lookup"><span data-stu-id="91260-186">Using a template</span></span>
<span data-ttu-id="91260-187">使用 PowerShell、 AzureCLI，或按一下 toodeploy 執行從 GitHub，您可以部署服務 tooAzure 從範本。</span><span class="sxs-lookup"><span data-stu-id="91260-187">You can deploy services tooAzure from a template by using PowerShell, AzureCLI, or by performing a click toodeploy from GitHub.</span></span> <span data-ttu-id="91260-188">toodeploy 服務範本，以在 GitHub 中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="91260-188">toodeploy services from a template in GitHub, execute hello following steps:</span></span>

1. <span data-ttu-id="91260-189">從 GitHub 開啟 hello template3 檔案。</span><span class="sxs-lookup"><span data-stu-id="91260-189">Open hello template3 file from GitHub.</span></span> <span data-ttu-id="91260-190">在此範例中，請開啟 [具有兩個子網路的虛擬網路](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network)。</span><span class="sxs-lookup"><span data-stu-id="91260-190">As an example, open [Virtual network with two subnets](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).</span></span>
2. <span data-ttu-id="91260-191">按一下**部署 tooAzure**，然後登入 toohello 在 Azure 入口網站使用您的認證。</span><span class="sxs-lookup"><span data-stu-id="91260-191">Click on **Deploy tooAzure**, and then sign in on toohello Azure portal with your credentials.</span></span>
3. <span data-ttu-id="91260-192">確認 hello 範本，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="91260-192">Verify hello template, and then click **Save**.</span></span>
4. <span data-ttu-id="91260-193">按一下**編輯參數**選取一個位置，例如*美國西部*、 hello vnet 和子網路。</span><span class="sxs-lookup"><span data-stu-id="91260-193">Click **Edit parameters** and select a location, such as *West US*, for hello vnet and subnets.</span></span>
5. <span data-ttu-id="91260-194">如有必要，變更 hello **ADDRESSPREFIX**和**SUBNETPREFIX**參數，然後再按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="91260-194">If necessary, change hello **ADDRESSPREFIX** and **SUBNETPREFIX** parameters, and then click **OK**.</span></span>
6. <span data-ttu-id="91260-195">按一下**選取資源群組**，然後按一下您想 tooadd hello vnet 和子網路與 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="91260-195">Click **Select a resource group** and then click on hello resource group you want tooadd hello vnet and subnets to.</span></span> <span data-ttu-id="91260-196">或者，您可以按一下 [或建立新的] 來建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="91260-196">Alternatively, you can create a new resource group by clicking **Or create new**.</span></span>
7. <span data-ttu-id="91260-197">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="91260-197">Click **Create**.</span></span> <span data-ttu-id="91260-198">請注意 hello 磚顯示**佈建的範本部署**。</span><span class="sxs-lookup"><span data-stu-id="91260-198">Notice hello tile displaying **Provisioning Template deployment**.</span></span> <span data-ttu-id="91260-199">一旦 hello 部署完成，您會看到以下畫面類似 tooone。</span><span class="sxs-lookup"><span data-stu-id="91260-199">Once hello deployment is done, you will see a screen similar tooone below.</span></span>

![範例範本部署](./media/resource-groups-networking/Figure6.png)

## <a name="next-steps"></a><span data-ttu-id="91260-201">後續步驟</span><span class="sxs-lookup"><span data-stu-id="91260-201">Next steps</span></span>
[<span data-ttu-id="91260-202">Azure 資源管理員範本語言</span><span class="sxs-lookup"><span data-stu-id="91260-202">Azure Resource Manager Template Language</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[<span data-ttu-id="91260-203">Azure 網路 - 常用範本</span><span class="sxs-lookup"><span data-stu-id="91260-203">Azure Networking – commonly used templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

[<span data-ttu-id="91260-204">Azure Resource Manager 與傳統部署</span><span class="sxs-lookup"><span data-stu-id="91260-204">Azure Resource Manager vs. classic deployment</span></span>](../azure-resource-manager/resource-manager-deployment-model.md)

[<span data-ttu-id="91260-205">Azure Resource Manager 概觀</span><span class="sxs-lookup"><span data-stu-id="91260-205">Azure Resource Manager Overview</span></span>](../azure-resource-manager/resource-group-overview.md)

