---
title: "在 Azure 範本之間傳遞複雜的值 | Microsoft Docs"
description: "示範透過 Azure Resource Manager 範本與連結的範本，使用複雜物件共用狀態資料的建議做法。"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fd2f5e2d-d56d-4e01-a57d-34f3eaead4a9
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: tomfitz
ms.openlocfilehash: 23cc4321159a87b61c177b11381646af8bd9eb35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="share-state-to-and-from-azure-resource-manager-templates"></a><span data-ttu-id="83b64-103">在 Azure Resource Manager 範本中共用狀態以及從 Azure Resource Manager 範本共用狀態</span><span class="sxs-lookup"><span data-stu-id="83b64-103">Share state to and from Azure Resource Manager templates</span></span>
<span data-ttu-id="83b64-104">這個主題說明在範本中管理和共用狀態的最佳做法。</span><span class="sxs-lookup"><span data-stu-id="83b64-104">This topic shows best practices for managing and sharing state within templates.</span></span> <span data-ttu-id="83b64-105">本主題所顯示的參數與變數為您可以定義的物件類型範例，方便您用來組織部署需求。</span><span class="sxs-lookup"><span data-stu-id="83b64-105">The parameters and variables shown in this topic are examples of the type of objects you can define to conveniently organize your deployment requirements.</span></span> <span data-ttu-id="83b64-106">在這些範例中，您可以實作自己的物件與您環境適用的屬性值。</span><span class="sxs-lookup"><span data-stu-id="83b64-106">From these examples, you can implement your own objects with property values that make sense for your environment.</span></span>

<span data-ttu-id="83b64-107">本主題是較大份白皮書的一部分。</span><span class="sxs-lookup"><span data-stu-id="83b64-107">This topic is part of a larger whitepaper.</span></span> <span data-ttu-id="83b64-108">若要閱讀完整的文件，請下載[世界級 Azure Resource Manager 範本注意事項和證明可行的作法](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf)。</span><span class="sxs-lookup"><span data-stu-id="83b64-108">To read the full paper, download [World Class Resource Manager Templates Considerations and Proven Practices](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span></span>

## <a name="provide-standard-configuration-settings"></a><span data-ttu-id="83b64-109">提供標準的組態設定</span><span class="sxs-lookup"><span data-stu-id="83b64-109">Provide standard configuration settings</span></span>
<span data-ttu-id="83b64-110">與其給予可提供總彈性和無數個變化的範本，其實常見的模式是提供可選取已知組態。</span><span class="sxs-lookup"><span data-stu-id="83b64-110">Rather than offer a template that provides total flexibility and countless variations, a common pattern is to provide a selection of known configurations.</span></span> <span data-ttu-id="83b64-111">實際上，使用者可選取沙箱、小型、中型和大型等標準 T 恤尺寸。</span><span class="sxs-lookup"><span data-stu-id="83b64-111">In effect, users can select standard t-shirt sizes such as sandbox, small, medium, and large.</span></span> <span data-ttu-id="83b64-112">T 恤尺寸的其他範例包括產品供應項目，例如社群版本或企業版本。</span><span class="sxs-lookup"><span data-stu-id="83b64-112">Other examples of t-shirt sizes are product offerings, such as community edition or enterprise edition.</span></span> <span data-ttu-id="83b64-113">在其他情況下，這可能是某種技術的工作負載特定組態，例如，對應減少或沒有 SQL。</span><span class="sxs-lookup"><span data-stu-id="83b64-113">In other cases, it may be workload-specific configurations of a technology – such as map reduce or no sql.</span></span>

<span data-ttu-id="83b64-114">有了複雜物件，您可以建立變數，其中包含有時也稱為「屬性包」的資料集合，並使用該資料在範本中驅動資源宣告。</span><span class="sxs-lookup"><span data-stu-id="83b64-114">With complex objects, you can create variables that contain collections of data, sometimes known as "property bags" and use that data to drive the resource declaration in your template.</span></span> <span data-ttu-id="83b64-115">這種方法可針對預先為客戶設定好的各種大小提供良好且已知的組態。</span><span class="sxs-lookup"><span data-stu-id="83b64-115">This approach provides good, known configurations of varying sizes that are preconfigured for customers.</span></span> <span data-ttu-id="83b64-116">如果沒有已知組態，範本的使用者就必須自行判斷叢集大小、納入平台資源限制，以及進行數學運算來識別儲存體帳戶所產生的資料分割和其他資源 (因叢集大小和資源限制而導致)。</span><span class="sxs-lookup"><span data-stu-id="83b64-116">Without known configurations, users of the template must determine cluster sizing on their own, factor in platform resource constraints, and do math to identify the resulting partitioning of storage accounts and other resources (due to cluster size and resource constraints).</span></span> <span data-ttu-id="83b64-117">除了為客戶提供更好的經驗，一些已知組態可讓您更輕鬆地提供支援，並協助您提供較高的密度等級。</span><span class="sxs-lookup"><span data-stu-id="83b64-117">In addition to making a better experience for the customer, a few known configurations are easier to support and can help you deliver a higher level of density.</span></span>

<span data-ttu-id="83b64-118">下列範例將顯示如何定義包含複雜物件以代表資料集合的變數。</span><span class="sxs-lookup"><span data-stu-id="83b64-118">The following example shows how to define variables that contain complex objects for representing collections of data.</span></span> <span data-ttu-id="83b64-119">此集合定義的值用於虛擬機器大小、網路設定、作業系統設定，以及可用性設定。</span><span class="sxs-lookup"><span data-stu-id="83b64-119">The collections define values that are used for virtual machine size, network settings, operating system settings and availability settings.</span></span>

    "variables": {
      "tshirtSize": "[variables(concat('tshirtSize', parameters('tshirtSize')))]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      },
      "tshirtSizeMedium": {
        "vmSize": "Standard_A3",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-8disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1],
          "jumpbox": 0
        }
      },
      "tshirtSizeLarge": {
        "vmSize": "Standard_A4",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-16disk-resources.json')]",
        "vmCount": 3,
        "slaveCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1,1],
          "jumpbox": 0
        }
      },
      "osSettings": {
        "scripts": [
          "[concat(variables('templateBaseUrl'), 'install_postgresql.sh')]",
          "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/shared_scripts/ubuntu/vm-disk-utils-0.1.sh"
        ],
        "imageReference": {
          "publisher": "Canonical",
          "offer": "UbuntuServer",
          "sku": "14.04.2-LTS",
          "version": "latest"
        }
      },
      "networkSettings": {
        "vnetName": "[parameters('virtualNetworkName')]",
        "addressPrefix": "10.0.0.0/16",
        "subnets": {
          "dmz": {
            "name": "dmz",
            "prefix": "10.0.0.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          },
          "data": {
            "name": "data",
            "prefix": "10.0.1.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          }
        }
      },
      "availabilitySetSettings": {
        "name": "pgsqlAvailabilitySet",
        "fdCount": 3,
        "udCount": 5
      }
    }

<span data-ttu-id="83b64-120">請注意，**tshirtSize** 變數會串連您透過參數 (**小**、**中**、**大**) 提供給文字 **tshirtSize** 的 T 恤大小。</span><span class="sxs-lookup"><span data-stu-id="83b64-120">Notice that the **tshirtSize** variable concatenates the t-shirt size you provided through a parameter (**Small**, **Medium**, **Large**) to the text **tshirtSize**.</span></span> <span data-ttu-id="83b64-121">您會使用這個變數來擷取該 T 恤大小的相關聯複雜物件變數。</span><span class="sxs-lookup"><span data-stu-id="83b64-121">You use this variable to retrieve the associated complex object variable for that t-shirt size.</span></span>

<span data-ttu-id="83b64-122">您稍後可以在範本中參考這些變數。</span><span class="sxs-lookup"><span data-stu-id="83b64-122">You can then reference these variables later in the template.</span></span> <span data-ttu-id="83b64-123">參考具名變數和其屬性的能力可簡化範本語法，而且可以讓您更容易了解內容。</span><span class="sxs-lookup"><span data-stu-id="83b64-123">The ability to reference named-variables and their properties simplifies the template syntax, and makes it easy to understand context.</span></span> <span data-ttu-id="83b64-124">下列範例使用如先前所示的物件來設定值，以定義要部署的資源。</span><span class="sxs-lookup"><span data-stu-id="83b64-124">The following example defines a resource to deploy by using the objects shown previously to set values.</span></span> <span data-ttu-id="83b64-125">例如，VM 大小是透過擷取 `variables('tshirtSize').vmSize` 的值來設定，而磁碟大小的值則是擷取自 `variables('tshirtSize').diskSize`。</span><span class="sxs-lookup"><span data-stu-id="83b64-125">For example, the VM size is set by retrieving the value for `variables('tshirtSize').vmSize` while the value for the disk size is retrieved from `variables('tshirtSize').diskSize`.</span></span> <span data-ttu-id="83b64-126">此外，連結之範本的 URI 是使用 `variables('tshirtSize').vmTemplate`的值來設定。</span><span class="sxs-lookup"><span data-stu-id="83b64-126">In addition, the URI for a linked template is set with the value for `variables('tshirtSize').vmTemplate`.</span></span>

    "name": "master-node",
    "type": "Microsoft.Resources/deployments",
    "apiVersion": "2015-01-01",
    "dependsOn": [
        "[concat('Microsoft.Resources/deployments/', 'shared')]"
    ],
    "properties": {
        "mode": "Incremental",
        "templateLink": {
          "uri": "[variables('tshirtSize').vmTemplate]",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "value": "[parameters('adminPassword')]"
          },
          "replicatorPassword": {
            "value": "[parameters('replicatorPassword')]"
          },
          "osSettings": {
            "value": "[variables('osSettings')]"
          },
          "subnet": {
            "value": "[variables('networkSettings').subnets.data]"
          },
          "commonSettings": {
            "value": {
              "region": "[parameters('region')]",
              "adminUsername": "[parameters('adminUsername')]",
              "namespace": "ms"
            }
          },
          "storageSettings": {
            "value":"[variables('tshirtSize').storage]"
          },
          "machineSettings": {
            "value": {
              "vmSize": "[variables('tshirtSize').vmSize]",
              "diskSize": "[variables('tshirtSize').diskSize]",
              "vmCount": 1,
              "availabilitySet": "[variables('availabilitySetSettings').name]"
            }
          },
          "masterIpAddress": {
            "value": "0"
          },
          "dbType": {
            "value": "MASTER"
          }
        }
      }
    }

## <a name="pass-state-to-a-template"></a><span data-ttu-id="83b64-127">將狀態傳遞至範本</span><span class="sxs-lookup"><span data-stu-id="83b64-127">Pass state to a template</span></span>
<span data-ttu-id="83b64-128">您可以透過於部署期間直接提供的參數，在範本中共用狀態。</span><span class="sxs-lookup"><span data-stu-id="83b64-128">You share state into a template through parameters that you provide directly during deployment.</span></span>

<span data-ttu-id="83b64-129">下表列出在範本中的常用參數。</span><span class="sxs-lookup"><span data-stu-id="83b64-129">The following table lists commonly used parameters in templates.</span></span>

| <span data-ttu-id="83b64-130">名稱</span><span class="sxs-lookup"><span data-stu-id="83b64-130">Name</span></span> | <span data-ttu-id="83b64-131">值</span><span class="sxs-lookup"><span data-stu-id="83b64-131">Value</span></span> | <span data-ttu-id="83b64-132">說明</span><span class="sxs-lookup"><span data-stu-id="83b64-132">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="83b64-133">location</span><span class="sxs-lookup"><span data-stu-id="83b64-133">location</span></span> |<span data-ttu-id="83b64-134">來自 Azure 區域之條件約束清單的字串</span><span class="sxs-lookup"><span data-stu-id="83b64-134">String from a constrained list of Azure regions</span></span> |<span data-ttu-id="83b64-135">部署儲存資源的位置。</span><span class="sxs-lookup"><span data-stu-id="83b64-135">The location where the resources are deployed.</span></span> |
| <span data-ttu-id="83b64-136">storageAccountNamePrefix</span><span class="sxs-lookup"><span data-stu-id="83b64-136">storageAccountNamePrefix</span></span> |<span data-ttu-id="83b64-137">String</span><span class="sxs-lookup"><span data-stu-id="83b64-137">String</span></span> |<span data-ttu-id="83b64-138">放置 VM 磁碟之儲存體帳戶的唯一 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="83b64-138">Unique DNS name for the Storage Account where the VM's disks are placed</span></span> |
| <span data-ttu-id="83b64-139">domainName</span><span class="sxs-lookup"><span data-stu-id="83b64-139">domainName</span></span> |<span data-ttu-id="83b64-140">String</span><span class="sxs-lookup"><span data-stu-id="83b64-140">String</span></span> |<span data-ttu-id="83b64-141">可公開存取的 jumpbox VM 網域名稱格式為：**{domainName}.{location}.cloudapp.com** 例如：**mydomainname.westus.cloudapp.azure.com**</span><span class="sxs-lookup"><span data-stu-id="83b64-141">Domain name of the publicly accessible jumpbox VM in the format: **{domainName}.{location}.cloudapp.com** For example: **mydomainname.westus.cloudapp.azure.com**</span></span> |
| <span data-ttu-id="83b64-142">adminUsername</span><span class="sxs-lookup"><span data-stu-id="83b64-142">adminUsername</span></span> |<span data-ttu-id="83b64-143">String</span><span class="sxs-lookup"><span data-stu-id="83b64-143">String</span></span> |<span data-ttu-id="83b64-144">VM 的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="83b64-144">Username for the VMs</span></span> |
| <span data-ttu-id="83b64-145">adminPassword</span><span class="sxs-lookup"><span data-stu-id="83b64-145">adminPassword</span></span> |<span data-ttu-id="83b64-146">String</span><span class="sxs-lookup"><span data-stu-id="83b64-146">String</span></span> |<span data-ttu-id="83b64-147">VM 的密碼</span><span class="sxs-lookup"><span data-stu-id="83b64-147">Password for the VMs</span></span> |
| <span data-ttu-id="83b64-148">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="83b64-148">tshirtSize</span></span> |<span data-ttu-id="83b64-149">來自提供 T 恤大小之條件約束清單的字串</span><span class="sxs-lookup"><span data-stu-id="83b64-149">String from a constrained list of offered t-shirt sizes</span></span> |<span data-ttu-id="83b64-150">要佈建的具名縮放單位大小。</span><span class="sxs-lookup"><span data-stu-id="83b64-150">The named scale unit size to provision.</span></span> <span data-ttu-id="83b64-151">例如，"Small"、"Medium"、"Large"</span><span class="sxs-lookup"><span data-stu-id="83b64-151">For example, "Small", "Medium", "Large"</span></span> |
| <span data-ttu-id="83b64-152">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="83b64-152">virtualNetworkName</span></span> |<span data-ttu-id="83b64-153">String</span><span class="sxs-lookup"><span data-stu-id="83b64-153">String</span></span> |<span data-ttu-id="83b64-154">取用者想使用的虛擬網路名稱。</span><span class="sxs-lookup"><span data-stu-id="83b64-154">Name of the virtual network that the consumer wants to use.</span></span> |
| <span data-ttu-id="83b64-155">enableJumpbox</span><span class="sxs-lookup"><span data-stu-id="83b64-155">enableJumpbox</span></span> |<span data-ttu-id="83b64-156">來自條件約束清單的字串 (enabled/disabled)</span><span class="sxs-lookup"><span data-stu-id="83b64-156">String from a constrained list (enabled/disabled)</span></span> |<span data-ttu-id="83b64-157">識別是否要為環境啟用 JumpBox 的參數。</span><span class="sxs-lookup"><span data-stu-id="83b64-157">Parameter that identifies whether to enable a jumpbox for the environment.</span></span> <span data-ttu-id="83b64-158">值："enabled"、"disabled"</span><span class="sxs-lookup"><span data-stu-id="83b64-158">Values: "enabled", "disabled"</span></span> |

<span data-ttu-id="83b64-159">上節中所用的 **tshirtSize** 參數定義如下：</span><span class="sxs-lookup"><span data-stu-id="83b64-159">The **tshirtSize** parameter used in the previous section is defined as:</span></span>

    "parameters": {
      "tshirtSize": {
        "type": "string",
        "defaultValue": "Small",
        "allowedValues": [
          "Small",
          "Medium",
          "Large"
        ],
        "metadata": {
          "Description": "T-shirt size of the MongoDB deployment"
        }
      }
    }


## <a name="pass-state-to-linked-templates"></a><span data-ttu-id="83b64-160">將狀態傳遞至連結的範本</span><span class="sxs-lookup"><span data-stu-id="83b64-160">Pass state to linked templates</span></span>
<span data-ttu-id="83b64-161">當連線到連結的範本時，您經常混合使用靜態變數與產生的變數。</span><span class="sxs-lookup"><span data-stu-id="83b64-161">When connecting to linked templates, you often use a mix of static and generated variables.</span></span>

### <a name="static-variables"></a><span data-ttu-id="83b64-162">靜態變數</span><span class="sxs-lookup"><span data-stu-id="83b64-162">Static variables</span></span>
<span data-ttu-id="83b64-163">靜態變數通常用於提供基底值，例如在範本中全程使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="83b64-163">Static variables are often used to provide base values, such as URLs, that are used throughout a template.</span></span>

<span data-ttu-id="83b64-164">在下面的範本摘要中，`templateBaseUrl` 會指定 GitHub 中範本的根位置。</span><span class="sxs-lookup"><span data-stu-id="83b64-164">In the following template excerpt, `templateBaseUrl` specifies the root location for the template in GitHub.</span></span> <span data-ttu-id="83b64-165">下一行會建置新的變數 `sharedTemplateUrl` ，它會將 基底 URL 與共用資源範本的已知名稱串連在一起。</span><span class="sxs-lookup"><span data-stu-id="83b64-165">The next line builds a new variable `sharedTemplateUrl` that concatenates the base URL with the known name of the shared resources template.</span></span> <span data-ttu-id="83b64-166">在該行下面，使用複雜物件變數儲存 T 恤尺寸，在此將基底 URL 和已知組態範本位置串連在一起，儲存在 `vmTemplate` 屬性中。</span><span class="sxs-lookup"><span data-stu-id="83b64-166">Below that line, a complex object variable is used to store a t-shirt size, where the base URL is concatenated to the known configuration template location and stored in the `vmTemplate` property.</span></span>

<span data-ttu-id="83b64-167">這個方法的優點是，如果範本位置變更，您只需要變更一個地方的靜態變數，就可以將它傳遞到所有連結的範本。</span><span class="sxs-lookup"><span data-stu-id="83b64-167">The benefit of this approach is that if the template location changes, you only need to change the static variable in one place, which passes it throughout the linked templates.</span></span>

    "variables": {
      "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
      "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "slaveCount": 1,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      }
    }

### <a name="generated-variables"></a><span data-ttu-id="83b64-168">產生的變數</span><span class="sxs-lookup"><span data-stu-id="83b64-168">Generated variables</span></span>
<span data-ttu-id="83b64-169">除了靜態變數，有數個變數是動態產生的。</span><span class="sxs-lookup"><span data-stu-id="83b64-169">In addition to static variables, several variables are generated dynamically.</span></span> <span data-ttu-id="83b64-170">本節將說明一些產生的變數的常見類型。</span><span class="sxs-lookup"><span data-stu-id="83b64-170">This section identifies some of the common types of generated variables.</span></span>

#### <a name="tshirtsize"></a><span data-ttu-id="83b64-171">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="83b64-171">tshirtSize</span></span>
<span data-ttu-id="83b64-172">您已熟悉這個從上述範例產生的變數。</span><span class="sxs-lookup"><span data-stu-id="83b64-172">You are familiar with this generated variable from the examples above.</span></span>

#### <a name="networksettings"></a><span data-ttu-id="83b64-173">networkSettings</span><span class="sxs-lookup"><span data-stu-id="83b64-173">networkSettings</span></span>
<span data-ttu-id="83b64-174">在容量、功能或端對端範圍的解決方案範本中，連結的範本通常會建立存在於網路上的資源。</span><span class="sxs-lookup"><span data-stu-id="83b64-174">In a capacity, capability, or end-to-end scoped solution template, the linked templates typically create resources that exist on a network.</span></span> <span data-ttu-id="83b64-175">一個直接的方法是使用複雜物件來儲存網路設定，並將其傳送到連結的範本。</span><span class="sxs-lookup"><span data-stu-id="83b64-175">One straightforward approach is to use a complex object to store network settings and pass them to linked templates.</span></span>

<span data-ttu-id="83b64-176">通訊網路設定的範例如下所示。</span><span class="sxs-lookup"><span data-stu-id="83b64-176">An example of communicating network settings can be seen below.</span></span>

    "networkSettings": {
      "vnetName": "[parameters('virtualNetworkName')]",
      "addressPrefix": "10.0.0.0/16",
      "subnets": {
        "dmz": {
          "name": "dmz",
          "prefix": "10.0.0.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        },
        "data": {
          "name": "data",
          "prefix": "10.0.1.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        }
      }
    }

#### <a name="availabilitysettings"></a><span data-ttu-id="83b64-177">availabilitySettings</span><span class="sxs-lookup"><span data-stu-id="83b64-177">availabilitySettings</span></span>
<span data-ttu-id="83b64-178">連結的範本中所建立的資源通常會放置在可用性集合中。</span><span class="sxs-lookup"><span data-stu-id="83b64-178">Resources created in linked templates are often placed in an availability set.</span></span> <span data-ttu-id="83b64-179">在下列範例中，已指定可用性集合名稱，以及要使用的容錯網域和更新網域計數。</span><span class="sxs-lookup"><span data-stu-id="83b64-179">In the following example, the availability set name is specified and also the fault domain and update domain count to use.</span></span>

    "availabilitySetSettings": {
      "name": "pgsqlAvailabilitySet",
      "fdCount": 3,
      "udCount": 5
    }

<span data-ttu-id="83b64-180">如果您需要多個可用性集合 (例如，一個用於主要節點，其他用於資料節點)，您可以使用名稱做為前置詞，指定多個可用性集合，或依照稍早所示的模型建立特定 T 恤大小的變數。</span><span class="sxs-lookup"><span data-stu-id="83b64-180">If you need multiple availability sets (for example, one for master nodes and another for data nodes), you can use a name as a prefix, specify multiple availability sets, or follow the model shown earlier for creating a variable for a specific t-shirt size.</span></span>

#### <a name="storagesettings"></a><span data-ttu-id="83b64-181">storageSettings</span><span class="sxs-lookup"><span data-stu-id="83b64-181">storageSettings</span></span>
<span data-ttu-id="83b64-182">儲存體詳細資料通常會與連結的範本共用。</span><span class="sxs-lookup"><span data-stu-id="83b64-182">Storage details are often shared with linked templates.</span></span> <span data-ttu-id="83b64-183">在下面的範例中， *storageSettings* 物件會提供有關儲存體帳戶和容器名稱的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="83b64-183">In the example below, a *storageSettings* object provides details about the storage account and container names.</span></span>

    "storageSettings": {
        "vhdStorageAccountName": "[parameters('storageAccountName')]",
        "vhdContainerName": "[variables('vmStorageAccountContainerName')]",
        "destinationVhdsContainer": "[concat('https://', parameters('storageAccountName'), variables('vmStorageAccountDomain'), '/', variables('vmStorageAccountContainerName'), '/')]"
    }

#### <a name="ossettings"></a><span data-ttu-id="83b64-184">osSettings</span><span class="sxs-lookup"><span data-stu-id="83b64-184">osSettings</span></span>
<span data-ttu-id="83b64-185">利用連結的範本，您可能需要傳遞作業系統設定到各種節點類型，並橫跨不同的已知組態類型。</span><span class="sxs-lookup"><span data-stu-id="83b64-185">With linked templates, you may need to pass operating system settings to various nodes types across different known configuration types.</span></span> <span data-ttu-id="83b64-186">複雜物件是一種用來儲存及共用作業系統資訊的簡單方式，也讓支援多個作業系統部署的選擇變得更輕鬆。</span><span class="sxs-lookup"><span data-stu-id="83b64-186">A complex object is an easy way to store and share operating system information and also makes it easier to support multiple operating system choices for deployment.</span></span>

<span data-ttu-id="83b64-187">下列範例顯示 *osSettings*的物件：</span><span class="sxs-lookup"><span data-stu-id="83b64-187">The following example shows an object for *osSettings*:</span></span>

    "osSettings": {
      "imageReference": {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "14.04.2-LTS",
        "version": "latest"
      }
    }

#### <a name="machinesettings"></a><span data-ttu-id="83b64-188">machineSettings</span><span class="sxs-lookup"><span data-stu-id="83b64-188">machineSettings</span></span>
<span data-ttu-id="83b64-189">產生的變數 *machineSettings* 是複雜物件，包含用於建立 VM 的核心變數的混合。</span><span class="sxs-lookup"><span data-stu-id="83b64-189">A generated variable, *machineSettings* is a complex object containing a mix of core variables for creating a VM.</span></span> <span data-ttu-id="83b64-190">此變數包含系統管理員使用者名稱和密碼、VM 名稱的前置詞，以及作業系統映像參考。</span><span class="sxs-lookup"><span data-stu-id="83b64-190">The variables include administrator user name and password, a prefix for the VM names, and an operating system image reference.</span></span>

    "machineSettings": {
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "machineNamePrefix": "mongodb-",
        "osImageReference": {
            "publisher": "[variables('osFamilySpec').imagePublisher]",
            "offer": "[variables('osFamilySpec').imageOffer]",
            "sku": "[variables('osFamilySpec').imageSKU]",
            "version": "latest"
        }
    },

<span data-ttu-id="83b64-191">請注意，*osImageReference* 會擷取在主要範本中所定義之 *osSettings* 變數的值。</span><span class="sxs-lookup"><span data-stu-id="83b64-191">Note that *osImageReference* retrieves the values from the *osSettings* variable defined in the main template.</span></span> <span data-ttu-id="83b64-192">這表示您可以輕鬆地變更 VM 的作業系統—完全地或根據範本取用者的喜好設定。</span><span class="sxs-lookup"><span data-stu-id="83b64-192">That means you can easily change the operating system for a VM—entirely or based on the preference of a template consumer.</span></span>

#### <a name="vmscripts"></a><span data-ttu-id="83b64-193">vmScripts</span><span class="sxs-lookup"><span data-stu-id="83b64-193">vmScripts</span></span>
<span data-ttu-id="83b64-194">*vmScripts* 物件包含要在 VM 執行個體上下載及執行之指令碼的詳細資料，包括外部和內部參考。</span><span class="sxs-lookup"><span data-stu-id="83b64-194">The *vmScripts* object contains details about the scripts to download and execute on a VM instance, including outside and inside references.</span></span> <span data-ttu-id="83b64-195">外部參考包含基礎結構。</span><span class="sxs-lookup"><span data-stu-id="83b64-195">Outside references include the infrastructure.</span></span>
<span data-ttu-id="83b64-196">內部參考包含已安裝的軟體和組態。</span><span class="sxs-lookup"><span data-stu-id="83b64-196">Inside references include the installed software installed and configuration.</span></span>

<span data-ttu-id="83b64-197">您可以使用 *scriptsToDownload* 屬性列出要下載到 VM 的指令碼。</span><span class="sxs-lookup"><span data-stu-id="83b64-197">You use the *scriptsToDownload* property to list the scripts to download to the VM.</span></span> <span data-ttu-id="83b64-198">此物件也包含對不同動作類型之命令列引數的參考。</span><span class="sxs-lookup"><span data-stu-id="83b64-198">This object also contains references to command-line arguments for different types of actions.</span></span> <span data-ttu-id="83b64-199">這些動作包括為每個個別節點執行預設安裝、部署所有節點後所執行的安裝，以及可能為給定範本指定的任何其他指令碼。</span><span class="sxs-lookup"><span data-stu-id="83b64-199">These actions include executing the default installation for each individual node, an installation that runs after all nodes are deployed, and any additional scripts that may be specific to a given template.</span></span>

<span data-ttu-id="83b64-200">這個範例來自用於部署 MongoDB 的範本，需要有仲裁程式以提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="83b64-200">This example is from a template used to deploy MongoDB, which requires an arbiter to deliver high availability.</span></span> <span data-ttu-id="83b64-201">*arbiterNodeInstallCommand* 已新增到 *vmScripts* 中以安裝仲裁程式。</span><span class="sxs-lookup"><span data-stu-id="83b64-201">The *arbiterNodeInstallCommand* has been added to *vmScripts* to install the arbiter.</span></span>

<span data-ttu-id="83b64-202">您可以在變數區段中找到定義特定文字以搭配適當的值執行指令碼的變數。</span><span class="sxs-lookup"><span data-stu-id="83b64-202">The variables section is where you find the variables that define the specific text to execute the script with the proper values.</span></span>

    "vmScripts": {
        "scriptsToDownload": [
            "[concat(variables('scriptUrl'), 'mongodb-', variables('osFamilySpec').osName, '-install.sh')]",
            "[concat(variables('sharedScriptUrl'), 'vm-disk-utils-0.1.sh')]"
        ],
        "regularNodeInstallCommand": "[variables('installCommand')]",
        "lastNodeInstallCommand": "[concat(variables('installCommand'), ' -l')]",
        "arbiterNodeInstallCommand": "[concat(variables('installCommand'), ' -a')]"
    },


## <a name="return-state-from-a-template"></a><span data-ttu-id="83b64-203">從範本傳回狀態</span><span class="sxs-lookup"><span data-stu-id="83b64-203">Return state from a template</span></span>
<span data-ttu-id="83b64-204">您不只可以將資料傳遞到範本中，也可以與發出呼叫的範本共用資料。</span><span class="sxs-lookup"><span data-stu-id="83b64-204">Not only can you pass data into a template, you can also share data back to the calling template.</span></span> <span data-ttu-id="83b64-205">在已連結範本的 **outputs** 區段中，您可以提供可供來源範本使用的機碼/值組。</span><span class="sxs-lookup"><span data-stu-id="83b64-205">In the **outputs** section of a linked template, you can provide key/value pairs that can be consumed by the source template.</span></span>

<span data-ttu-id="83b64-206">下列範例顯示如何傳遞在連結的範本中產生的私人 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="83b64-206">The following example shows how to pass the private IP address generated in a linked template.</span></span>

    "outputs": {
        "masterip": {
            "value": "[reference(concat(variables('nicName'),0)).ipConfigurations[0].properties.privateIPAddress]",
            "type": "string"
         }
    }

<span data-ttu-id="83b64-207">在主要範本中，您可以透過下列語法使用該資料：</span><span class="sxs-lookup"><span data-stu-id="83b64-207">Within the main template, you can use that data with the following syntax:</span></span>

    "[reference('master-node').outputs.masterip.value]"

<span data-ttu-id="83b64-208">這個運算式可以用在主要範本的輸出區段或資源區段。</span><span class="sxs-lookup"><span data-stu-id="83b64-208">You can use this expression in either the outputs section or the resources section of the main template.</span></span> <span data-ttu-id="83b64-209">因為這個運算式依賴執行階段狀態，所以您無法在變數區段使用它。</span><span class="sxs-lookup"><span data-stu-id="83b64-209">You cannot use the expression in the variables section because it relies on the runtime state.</span></span> <span data-ttu-id="83b64-210">若要從主要範本傳回這個值，請使用︰</span><span class="sxs-lookup"><span data-stu-id="83b64-210">To return this value from the main template, use:</span></span>

    "outputs": {
      "masterIpAddress": {
        "value": "[reference('master-node').outputs.masterip.value]",
        "type": "string"
      }

<span data-ttu-id="83b64-211">如需使用已連結範本的輸出區段傳回虛擬機器之資料磁碟的範例，請參閱 [Creating multiple data disks for a Virtual Machine (為虛擬機器建立多個資料磁碟)](resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="83b64-211">For an example of using the outputs section of a linked template to return data disks for a virtual machine, see [Creating multiple data disks for a Virtual Machine](resource-group-create-multiple.md).</span></span>

## <a name="define-authentication-settings-for-virtual-machine"></a><span data-ttu-id="83b64-212">為虛擬機器定義驗證設定</span><span class="sxs-lookup"><span data-stu-id="83b64-212">Define authentication settings for virtual machine</span></span>
<span data-ttu-id="83b64-213">您可以使用與先前所示的相同組態設定模式，指定虛擬機器的驗證設定。</span><span class="sxs-lookup"><span data-stu-id="83b64-213">You can use the same pattern shown previously for configuration settings to specify the authentication settings for a virtual machine.</span></span> <span data-ttu-id="83b64-214">您要建立在驗證類型中傳遞的參數。</span><span class="sxs-lookup"><span data-stu-id="83b64-214">You create a parameter for passing in the type of authentication.</span></span>

    "parameters": {
      "authenticationType": {
        "allowedValues": [
          "password",
          "sshPublicKey"
        ],
        "defaultValue": "password",
        "metadata": {
          "description": "Authentication type"
        },
        "type": "string"
      }
    }

<span data-ttu-id="83b64-215">您要加入不同的驗證類型變數，有一個變數會根據參數值，儲存這個部署所用的類型。</span><span class="sxs-lookup"><span data-stu-id="83b64-215">You add variables for the different authentication types, and a variable to store which type is used for this deployment based on the value of the parameter.</span></span>

    "variables": {
      "osProfile": "[variables(concat('osProfile', parameters('authenticationType')))]",
      "osProfilepassword": {
        "adminPassword": "[parameters('adminPassword')]",
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]"
      },
      "osProfilesshPublicKey": {
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]",
        "linuxConfiguration": {
          "disablePasswordAuthentication": "true",
          "ssh": {
            "publicKeys": [
              {
                "keyData": "[parameters('sshPublicKey')]",
                "path": "/home/notused/.ssh/authorized_keys"
              }
            ]
          }
        }
      }
    }

<span data-ttu-id="83b64-216">定義虛擬機器時，您要將 **osProfile** 設成您建立的變數。</span><span class="sxs-lookup"><span data-stu-id="83b64-216">When defining the virtual machine, you set the **osProfile** to the variable you created.</span></span>

    {
      "type": "Microsoft.Compute/virtualMachines",
      ...
      "osProfile": "[variables('osProfile')]"
    }


## <a name="next-steps"></a><span data-ttu-id="83b64-217">後續步驟</span><span class="sxs-lookup"><span data-stu-id="83b64-217">Next steps</span></span>
* <span data-ttu-id="83b64-218">如要了解範本的各區段，請參閱 [編寫 Azure Resource Manager 範本](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="83b64-218">To learn about the sections of the template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="83b64-219">若要查看範本中可以使用的函數，請參閱 [Azure Resource Manager 範本函數](resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="83b64-219">To see the functions that are available within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md)</span></span>
