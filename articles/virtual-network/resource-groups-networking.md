---
title: "網路資源提供者概觀 | Microsoft Docs"
description: "深入了解 Azure 資源管理員中新的網路資源提供者"
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
ms.openlocfilehash: 2428c707ddeed281fddd1e57bc5574603f0b9b1c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="network-resource-provider"></a><span data-ttu-id="83494-103">網路資源提供者</span><span class="sxs-lookup"><span data-stu-id="83494-103">Network Resource Provider</span></span>
<span data-ttu-id="83494-104">現今企業成功的基礎是可以使用靈活、具彈性、安全且可重複的方式來建置和管理大規模網路感知應用程式。</span><span class="sxs-lookup"><span data-stu-id="83494-104">An underpinning need in today’s business success, is the ability to build and manage large scale network aware applications in an agile, flexible, secure and repeatable way.</span></span> <span data-ttu-id="83494-105">Azure Resource Manager 可讓您以資源群組中單一資源集合的形式，建立這類應用程式。</span><span class="sxs-lookup"><span data-stu-id="83494-105">Azure Resource Manager enables you to create such applications, as a single collection of resources in resource groups.</span></span> <span data-ttu-id="83494-106">管理這類資源時，是透過 Resource Manager 底下的各種資源提供者進行管理。</span><span class="sxs-lookup"><span data-stu-id="83494-106">Such resources are managed through various resource providers under Resource Manager.</span></span>

<span data-ttu-id="83494-107">Azure 資源管理員會仰賴不同的資源提供者來提供資源的存取權。</span><span class="sxs-lookup"><span data-stu-id="83494-107">Azure Resource Manager relies on different resource providers to provide access to your resources.</span></span> <span data-ttu-id="83494-108">有三個主要的資源提供者：網路、儲存體和運算。</span><span class="sxs-lookup"><span data-stu-id="83494-108">There are three main resource providers: Network, Storage and Compute.</span></span> <span data-ttu-id="83494-109">本文件討論網路資源提供者的特性和優點，包括：</span><span class="sxs-lookup"><span data-stu-id="83494-109">This document discusses the characteristics and benefits of the Network Resource Provider, including:</span></span>

* <span data-ttu-id="83494-110">**中繼資料** - 您可以使用標記新增資源的資訊。</span><span class="sxs-lookup"><span data-stu-id="83494-110">**Metadata** – you can add information to resources using tags.</span></span> <span data-ttu-id="83494-111">這些標記可以用來追蹤資源群組和訂用帳戶中的資源使用。</span><span class="sxs-lookup"><span data-stu-id="83494-111">These tags can be used to track resource utilization across resource groups and subscriptions.</span></span>
* <span data-ttu-id="83494-112">**更進一步控制網路** - 網路資源是進行鬆散偶合，而您可以更精密地控制它們。</span><span class="sxs-lookup"><span data-stu-id="83494-112">**Greater control of your network** - network resources are loosely coupled and you can control them in a more granular fashion.</span></span> <span data-ttu-id="83494-113">這表示可以更彈性地管理網路資源。</span><span class="sxs-lookup"><span data-stu-id="83494-113">This means you have more flexibility in managing the networking resources.</span></span>
* <span data-ttu-id="83494-114">**設定更快速** - 因為網路資源是進行鬆散偶合，所以您可以平行建立並協調網路資源。</span><span class="sxs-lookup"><span data-stu-id="83494-114">**Faster configuration** - because network resources are loosely coupled, you can create and orchestrate network resources in parallel.</span></span> <span data-ttu-id="83494-115">這已經大幅減少設定時間。</span><span class="sxs-lookup"><span data-stu-id="83494-115">This has drastically reduced configuration time.</span></span>
* <span data-ttu-id="83494-116">**角色型存取控制** - 除了允許建立自訂角色進行安全管理之外，RBAC 還提供具有特定安全性範圍的預設角色。</span><span class="sxs-lookup"><span data-stu-id="83494-116">**Role Based Access Control** - RBAC provides default roles, with specific security scope, in addition to allowing the creation of custom roles for secure management.</span></span>
* <span data-ttu-id="83494-117">**更易於管理和部署** - 更容易部署和管理應用程式，因為您可以建立整個應用程式堆疊做為資源群組中的單一資源集合。</span><span class="sxs-lookup"><span data-stu-id="83494-117">**Easier management and deployment** - it’s easier to deploy and manage applications since you can can create an entire application stack as a single collection of resources in a resource group.</span></span> <span data-ttu-id="83494-118">而且可以更快速地部署，因為只要提供範本 JSON 裝載即可進行部署。</span><span class="sxs-lookup"><span data-stu-id="83494-118">And faster to deploy, since you can deploy by simply providing a template JSON payload.</span></span>
* <span data-ttu-id="83494-119">**快速自訂** - 您可以使用宣告樣式範本進行可重複且快速自訂的部署。</span><span class="sxs-lookup"><span data-stu-id="83494-119">**Rapid customization** - you can use declarative-style templates to enable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="83494-120">**可重複自訂** - 您可以使用宣告樣式範本進行可重複且快速自訂的部署。</span><span class="sxs-lookup"><span data-stu-id="83494-120">**Repeatable customization** - you can use declarative-style templates to enable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="83494-121">**管理介面** - 您可以使用任何下列任一介面來管理您的資源：</span><span class="sxs-lookup"><span data-stu-id="83494-121">**Management interfaces** - you can use any of the following interfaces to manage your resources:</span></span>
  * <span data-ttu-id="83494-122">REST 型 API</span><span class="sxs-lookup"><span data-stu-id="83494-122">REST based API</span></span>
  * <span data-ttu-id="83494-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="83494-123">PowerShell</span></span>
  * <span data-ttu-id="83494-124">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="83494-124">.NET SDK</span></span>
  * <span data-ttu-id="83494-125">Node.JS SDK</span><span class="sxs-lookup"><span data-stu-id="83494-125">Node.JS SDK</span></span>
  * <span data-ttu-id="83494-126">Java SDK</span><span class="sxs-lookup"><span data-stu-id="83494-126">Java SDK</span></span>
  * <span data-ttu-id="83494-127">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="83494-127">Azure CLI</span></span>
  * <span data-ttu-id="83494-128">預覽入口網站</span><span class="sxs-lookup"><span data-stu-id="83494-128">Preview Portal</span></span>
  * <span data-ttu-id="83494-129">Resource Manager 範本語言</span><span class="sxs-lookup"><span data-stu-id="83494-129">Resource Manager template language</span></span>

## <a name="network-resources"></a><span data-ttu-id="83494-130">網路資源</span><span class="sxs-lookup"><span data-stu-id="83494-130">Network resources</span></span>
<span data-ttu-id="83494-131">您現在可以獨立地管理網路資源，而不是透過單一計算資源 (虛擬機器) 進行管理。</span><span class="sxs-lookup"><span data-stu-id="83494-131">You can now manage network resources independently, instead of having them all managed through a single compute resource (a virtual machine).</span></span> <span data-ttu-id="83494-132">這確保具有較高程度的彈性和靈活性可在資源群組中撰寫複雜且大型的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="83494-132">This ensures a higher degree of flexibility and agility in composing a complex and large scale infrastructure in a resource group.</span></span>

<span data-ttu-id="83494-133">含有多介層應用程式之範例部署的概念檢視顯示如下。</span><span class="sxs-lookup"><span data-stu-id="83494-133">A conceptual view of a sample deployment involving a multi-tiered application is presented below.</span></span> <span data-ttu-id="83494-134">您看到的每項資源 (如 NIC、公用 IP 位址和 VM 等) 都可以分開管理。</span><span class="sxs-lookup"><span data-stu-id="83494-134">Each resource you see, such as NICs, public IP addresses, and VMs, can be managed independently.</span></span>

![網路資源模型](./media/resource-groups-networking/Figure2.png)

<span data-ttu-id="83494-136">每項資源均包含一組通用屬性，以及其個別的屬性集。</span><span class="sxs-lookup"><span data-stu-id="83494-136">Every resource contains a common set of properties, and their individual property set.</span></span> <span data-ttu-id="83494-137">通用屬性包括：</span><span class="sxs-lookup"><span data-stu-id="83494-137">The common properties are:</span></span>

| <span data-ttu-id="83494-138">屬性</span><span class="sxs-lookup"><span data-stu-id="83494-138">Property</span></span> | <span data-ttu-id="83494-139">說明</span><span class="sxs-lookup"><span data-stu-id="83494-139">Description</span></span> | <span data-ttu-id="83494-140">範例值</span><span class="sxs-lookup"><span data-stu-id="83494-140">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="83494-141">**name**</span><span class="sxs-lookup"><span data-stu-id="83494-141">**name**</span></span> |<span data-ttu-id="83494-142">唯一的資源名稱。</span><span class="sxs-lookup"><span data-stu-id="83494-142">Unique resource name.</span></span> <span data-ttu-id="83494-143">每個資源類型都有自己的命名限制。</span><span class="sxs-lookup"><span data-stu-id="83494-143">Each resource type has its own naming restrictions.</span></span> |<span data-ttu-id="83494-144">PIP01、VM01、NIC01</span><span class="sxs-lookup"><span data-stu-id="83494-144">PIP01, VM01, NIC01</span></span> |
| <span data-ttu-id="83494-145">**位置**</span><span class="sxs-lookup"><span data-stu-id="83494-145">**location**</span></span> |<span data-ttu-id="83494-146">資源所在的 Azure 區域</span><span class="sxs-lookup"><span data-stu-id="83494-146">Azure region in which the resource resides</span></span> |<span data-ttu-id="83494-147">westus、eastus</span><span class="sxs-lookup"><span data-stu-id="83494-147">westus, eastus</span></span> |
| <span data-ttu-id="83494-148">**id**</span><span class="sxs-lookup"><span data-stu-id="83494-148">**id**</span></span> |<span data-ttu-id="83494-149">唯一的 URI 型識別</span><span class="sxs-lookup"><span data-stu-id="83494-149">Unique URI based identification</span></span> |<span data-ttu-id="83494-150">/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span><span class="sxs-lookup"><span data-stu-id="83494-150">/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span></span> |

<span data-ttu-id="83494-151">您可以在下列各節中查看資源的個別屬性。</span><span class="sxs-lookup"><span data-stu-id="83494-151">You can check the individual properties of resources in the sections below.</span></span>

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

## <a name="management-interfaces"></a><span data-ttu-id="83494-152">管理介面</span><span class="sxs-lookup"><span data-stu-id="83494-152">Management interfaces</span></span>
<span data-ttu-id="83494-153">您可以使用不同的介面管理您的 Azure 網路資源。</span><span class="sxs-lookup"><span data-stu-id="83494-153">You can manage your Azure networking resources using different interfaces.</span></span> <span data-ttu-id="83494-154">在本文件中，我們將著重在指引這些介面：REST API 和範本。</span><span class="sxs-lookup"><span data-stu-id="83494-154">In this document we will focus on tow of those interfaces: REST API, and templates.</span></span>

### <a name="rest-api"></a><span data-ttu-id="83494-155">REST API</span><span class="sxs-lookup"><span data-stu-id="83494-155">REST API</span></span>
<span data-ttu-id="83494-156">如前所述，網路資源可以透過各種介面進行管理，包括 REST API、.NET SDK、Node.JS SDK、Java SDK、PowerShell、CLI、Azure 入口網站和範本。</span><span class="sxs-lookup"><span data-stu-id="83494-156">As mentioned earlier, network resources can be managed via a variety of interfaces, including REST API,.NET SDK, Node.JS SDK, Java SDK, PowerShell, CLI, Azure Portal and templates.</span></span>

<span data-ttu-id="83494-157">Rest API 符合 HTTP 1.1 通訊協定規格。</span><span class="sxs-lookup"><span data-stu-id="83494-157">The Rest API’s conform to the HTTP 1.1 protocol specification.</span></span> <span data-ttu-id="83494-158">API 的一般 URI 結構顯示如下：</span><span class="sxs-lookup"><span data-stu-id="83494-158">The general URI structure of the API is presented below:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/providers/{resource-provider-namespace}/locations/{region-location}/register?api-version={api-version}

<span data-ttu-id="83494-159">而以大括弧括住的參數代表下列元素：</span><span class="sxs-lookup"><span data-stu-id="83494-159">And the parameters in braces represent the following elements:</span></span>

* <span data-ttu-id="83494-160">**subscription-id** - Azure 訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="83494-160">**subscription-id** - your Azure subscription id.</span></span>
* <span data-ttu-id="83494-161">**resource-provider-namespace** - 正在使用之提供者的命名空間。</span><span class="sxs-lookup"><span data-stu-id="83494-161">**resource-provider-namespace** - namespace for the provider being used.</span></span> <span data-ttu-id="83494-162">網路資源提供者的值是 *Microsoft.Network*。</span><span class="sxs-lookup"><span data-stu-id="83494-162">THe value for the network resource provider is *Microsoft.Network*.</span></span>
* <span data-ttu-id="83494-163">**region-name** - Azure 區域名稱</span><span class="sxs-lookup"><span data-stu-id="83494-163">**region-name** - the Azure region name</span></span>

<span data-ttu-id="83494-164">呼叫 REST API 時，支援下列 HTTP 方法：</span><span class="sxs-lookup"><span data-stu-id="83494-164">The following HTTP methods are supported when making calls to the REST API:</span></span>

* <span data-ttu-id="83494-165">**PUT** - 用來建立所指定類型的資源、修改資源屬性，或變更資源之間的關聯。</span><span class="sxs-lookup"><span data-stu-id="83494-165">**PUT** - used to create a resource of a given type, modify a resource property or change an association between resources.</span></span>
* <span data-ttu-id="83494-166">**GET** - 用來擷取已佈建資源的資訊。</span><span class="sxs-lookup"><span data-stu-id="83494-166">**GET** - used to retrieve information for a provisioned resource.</span></span>
* <span data-ttu-id="83494-167">**DELETE** - 用來刪除現有資源。</span><span class="sxs-lookup"><span data-stu-id="83494-167">**DELETE** - used to delete an existing resource.</span></span>

<span data-ttu-id="83494-168">要求和回應都符合 JSON 裝載格式。</span><span class="sxs-lookup"><span data-stu-id="83494-168">Both the request and response conform to a JSON payload format.</span></span> <span data-ttu-id="83494-169">如需詳細資料，請參閱 [Azure 資源管理 API](https://msdn.microsoft.com/library/azure/dn948464.aspx)。</span><span class="sxs-lookup"><span data-stu-id="83494-169">For more details, see [Azure Resource Management APIs](https://msdn.microsoft.com/library/azure/dn948464.aspx).</span></span>

### <a name="resource-manager-template-language"></a><span data-ttu-id="83494-170">Resource Manager 範本語言</span><span class="sxs-lookup"><span data-stu-id="83494-170">Resource Manager template language</span></span>
<span data-ttu-id="83494-171">除了以命令方式 (透過 API 或 SDK) 管理資源之外，藉由使用「Resource Manager 範本語言」，您還可以使用宣告式程式設計樣式來建置和管理網路資源。</span><span class="sxs-lookup"><span data-stu-id="83494-171">In addition to managing resources imperatively (via APIs or SDK), you can also use a declarative programming style to build and manage network resources by using the Resource Manager Template Language.</span></span>

<span data-ttu-id="83494-172">範本的範例表示法提供如下 –</span><span class="sxs-lookup"><span data-stu-id="83494-172">A sample representation of a template is provided below –</span></span>

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "<version-number-of-template>",
      "parameters": { <parameter-definitions-of-template> },
      "variables": { <variable-definitions-of-template> },
      "resources": [ { <definition-of-resource-to-deploy> } ],
      "outputs": { <output-of-template> }    
    }

<span data-ttu-id="83494-173">範本主要是透過參數所插入之資源和執行個體值的 JSON 描述。</span><span class="sxs-lookup"><span data-stu-id="83494-173">The template is primarily a JSON description of the resources and the instance values injected via parameters.</span></span> <span data-ttu-id="83494-174">下列範例可以用來建立具有 2 個子網路的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="83494-174">The example below can be used to create a virtual network with 2 subnets.</span></span>

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

<span data-ttu-id="83494-175">您可以選擇在使用範本時手動提供參數值，也可以使用參數檔案。</span><span class="sxs-lookup"><span data-stu-id="83494-175">You have the option of providing the parameter values manually when using a template, or you can use a parameter file.</span></span> <span data-ttu-id="83494-176">下列範例顯示一組可能的參數值以與上述範本搭配使用：</span><span class="sxs-lookup"><span data-stu-id="83494-176">The example below shows a possible set of parameter values to be used with the template above:</span></span>

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


<span data-ttu-id="83494-177">使用範本的主要優點如下：</span><span class="sxs-lookup"><span data-stu-id="83494-177">The main advantages of using templates are:</span></span>

* <span data-ttu-id="83494-178">您可以透過宣告樣式在資源群組中建置複雜的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="83494-178">You can build a complex infrastructure in a resource group in a declarative style.</span></span> <span data-ttu-id="83494-179">建立資源 (包括相依性管理) 時的協調是由 Resource Manager 負責。</span><span class="sxs-lookup"><span data-stu-id="83494-179">The orchestration of creating the resources, including dependency management, is handled by Resource Manager.</span></span>
* <span data-ttu-id="83494-180">只要變更參數，即可透過可重複的方式在各種區域和某個區域內建立基礎結構。</span><span class="sxs-lookup"><span data-stu-id="83494-180">The infrastructure can be created in a repeatable way across various regions and within a region by simply changing parameters.</span></span>
* <span data-ttu-id="83494-181">宣告樣式可讓建置範本以及推出基礎結構的前置時間變短。</span><span class="sxs-lookup"><span data-stu-id="83494-181">The declarative style leads to shorter lead time in building the templates and rolling out the infrastructure.</span></span>

<span data-ttu-id="83494-182">如需範例範本，請參閱 [Azure 快速入門範本](https://github.com/Azure/azure-quickstart-templates)。</span><span class="sxs-lookup"><span data-stu-id="83494-182">For sample templates, see [Azure quickstart templates](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="83494-183">如需有關「Resource Manager 範本語言」的詳細資訊，請參閱 [Azure Resource Manager 範本語言](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="83494-183">For more information on the Resource Manager Template Language, see [Azure Resource Manager Template Language](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="83494-184">上述範例範本使用虛擬網路和子網路資源。</span><span class="sxs-lookup"><span data-stu-id="83494-184">The sample template above uses the virtual network and subnet resources.</span></span> <span data-ttu-id="83494-185">下列是其他您可以使用的網路資源：</span><span class="sxs-lookup"><span data-stu-id="83494-185">There are other network resources you can use as listed below:</span></span>

### <a name="using-a-template"></a><span data-ttu-id="83494-186">使用範本</span><span class="sxs-lookup"><span data-stu-id="83494-186">Using a template</span></span>
<span data-ttu-id="83494-187">您可以使用 PowerShell 或 AzureCLI 從範本部署服務到 Azure，或執行按一下動作來從 GitHub 部署。</span><span class="sxs-lookup"><span data-stu-id="83494-187">You can deploy services to Azure from a template by using PowerShell, AzureCLI, or by performing a click to deploy from GitHub.</span></span> <span data-ttu-id="83494-188">若要在 GitHub 中從範本部署服務，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="83494-188">To deploy services from a template in GitHub, execute the following steps:</span></span>

1. <span data-ttu-id="83494-189">從 GitHub 開啟 template3 檔案。</span><span class="sxs-lookup"><span data-stu-id="83494-189">Open the template3 file from GitHub.</span></span> <span data-ttu-id="83494-190">在此範例中，請開啟 [具有兩個子網路的虛擬網路](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network)。</span><span class="sxs-lookup"><span data-stu-id="83494-190">As an example, open [Virtual network with two subnets](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).</span></span>
2. <span data-ttu-id="83494-191">按一下 [部署至 Azure] ，然後使用您的認證登入 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="83494-191">Click on **Deploy to Azure**, and then sign in on to the Azure portal with your credentials.</span></span>
3. <span data-ttu-id="83494-192">驗證範本，然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="83494-192">Verify the template, and then click **Save**.</span></span>
4. <span data-ttu-id="83494-193">按一下 [編輯參數] 並選取位置 (例如*美國西部 (West US)* 做為 vnet 和子網路。</span><span class="sxs-lookup"><span data-stu-id="83494-193">Click **Edit parameters** and select a location, such as *West US*, for the vnet and subnets.</span></span>
5. <span data-ttu-id="83494-194">如有必要，請變更 [ADDRESSPREFIX] 和 [SUBNETPREFIX] 參數，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="83494-194">If necessary, change the **ADDRESSPREFIX** and **SUBNETPREFIX** parameters, and then click **OK**.</span></span>
6. <span data-ttu-id="83494-195">按一下 [選取資源群組]  ，然後按一下您想要對其新增 vnet 和子網路的資源群組。</span><span class="sxs-lookup"><span data-stu-id="83494-195">Click **Select a resource group** and then click on the resource group you want to add the vnet and subnets to.</span></span> <span data-ttu-id="83494-196">或者，您可以按一下 [或建立新的] 來建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="83494-196">Alternatively, you can create a new resource group by clicking **Or create new**.</span></span>
7. <span data-ttu-id="83494-197">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="83494-197">Click **Create**.</span></span> <span data-ttu-id="83494-198">請注意顯示 [佈建範本部署] 的磚。</span><span class="sxs-lookup"><span data-stu-id="83494-198">Notice the tile displaying **Provisioning Template deployment**.</span></span> <span data-ttu-id="83494-199">完成部署之後，您將會看到類似下面所示的畫面。</span><span class="sxs-lookup"><span data-stu-id="83494-199">Once the deployment is done, you will see a screen similar to one below.</span></span>

![範例範本部署](./media/resource-groups-networking/Figure6.png)

## <a name="next-steps"></a><span data-ttu-id="83494-201">後續步驟</span><span class="sxs-lookup"><span data-stu-id="83494-201">Next steps</span></span>
[<span data-ttu-id="83494-202">Azure 資源管理員範本語言</span><span class="sxs-lookup"><span data-stu-id="83494-202">Azure Resource Manager Template Language</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[<span data-ttu-id="83494-203">Azure 網路 - 常用範本</span><span class="sxs-lookup"><span data-stu-id="83494-203">Azure Networking – commonly used templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

[<span data-ttu-id="83494-204">Azure Resource Manager 與傳統部署</span><span class="sxs-lookup"><span data-stu-id="83494-204">Azure Resource Manager vs. classic deployment</span></span>](../azure-resource-manager/resource-manager-deployment-model.md)

[<span data-ttu-id="83494-205">Azure Resource Manager 概觀</span><span class="sxs-lookup"><span data-stu-id="83494-205">Azure Resource Manager Overview</span></span>](../azure-resource-manager/resource-group-overview.md)

