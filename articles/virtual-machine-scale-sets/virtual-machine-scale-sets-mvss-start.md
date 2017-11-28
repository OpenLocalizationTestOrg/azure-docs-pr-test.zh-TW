---
title: "了解虛擬機器擴展集範本 | Microsoft Docs"
description: "了解如何為虛擬機器擴展集建立最基本的可行擴展集範本"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: negat
ms.openlocfilehash: 65f02c4675eb752dcc82e9a1d1c7f6c2c193fc32
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="learn-about-virtual-machine-scale-set-templates"></a><span data-ttu-id="06c0c-103">了解虛擬機器擴展集範本</span><span class="sxs-lookup"><span data-stu-id="06c0c-103">Learn about virtual machine scale set templates</span></span>
<span data-ttu-id="06c0c-104">[Azure Resource Manager 範本](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment)是部署相關資源群組的絕佳方式。</span><span class="sxs-lookup"><span data-stu-id="06c0c-104">[Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) are a great way to deploy groups of related resources.</span></span> <span data-ttu-id="06c0c-105">本教學課程系列說明如何建立最基本的可行擴展集範本，以及如何修改此範本來配合各種案例。</span><span class="sxs-lookup"><span data-stu-id="06c0c-105">This tutorial series shows how to create a minimum viable scale set template and how to modify this template to suit various scenarios.</span></span> <span data-ttu-id="06c0c-106">所有範例皆來自這個 [GitHub 存放庫](https://github.com/gatneil/mvss)。</span><span class="sxs-lookup"><span data-stu-id="06c0c-106">All examples come from this [GitHub repository](https://github.com/gatneil/mvss).</span></span> 

<span data-ttu-id="06c0c-107">此範本已刻意簡化。</span><span class="sxs-lookup"><span data-stu-id="06c0c-107">This template is intended to be simple.</span></span> <span data-ttu-id="06c0c-108">如需較完整的擴展集範本範例，請參閱 [Azure 快速入門範本 GitHub 存放庫](https://github.com/Azure/azure-quickstart-templates)，然後搜尋包含 `vmss` 字串的資料夾。</span><span class="sxs-lookup"><span data-stu-id="06c0c-108">For more complete examples of scale set templates, see the [Azure Quickstart Templates GitHub repository](https://github.com/Azure/azure-quickstart-templates) and search for folders that contain the string `vmss`.</span></span>

<span data-ttu-id="06c0c-109">如果您已經熟悉如何建立範本，您可以跳到「後續步驟」一節，以了解如何修改此範本。</span><span class="sxs-lookup"><span data-stu-id="06c0c-109">If you are already familiar with creating templates, you can skip to the "Next steps" section to see how to modify this template.</span></span>

## <a name="review-the-template"></a><span data-ttu-id="06c0c-110">檢閱範本</span><span class="sxs-lookup"><span data-stu-id="06c0c-110">Review the template</span></span>

<span data-ttu-id="06c0c-111">使用 GitHub 以檢閱最基本的可行擴展集範本，[azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json)。</span><span class="sxs-lookup"><span data-stu-id="06c0c-111">Use GitHub to review our minimum viable scale set template, [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).</span></span>

<span data-ttu-id="06c0c-112">在本教學課程中，我們將檢查差異 (`git diff master minimum-viable-scale-set`)，逐步建立最基本的可行擴展集範本。</span><span class="sxs-lookup"><span data-stu-id="06c0c-112">In this tutorial, we examine the diff (`git diff master minimum-viable-scale-set`) to create the minimum viable scale set template piece by piece.</span></span>

## <a name="define-schema-and-contentversion"></a><span data-ttu-id="06c0c-113">定義 $schema 和 contentVersion</span><span class="sxs-lookup"><span data-stu-id="06c0c-113">Define $schema and contentVersion</span></span>
<span data-ttu-id="06c0c-114">首先，我們會定義範本中的 `$schema` 和 `contentVersion`。</span><span class="sxs-lookup"><span data-stu-id="06c0c-114">First, we define `$schema` and `contentVersion` in the template.</span></span> <span data-ttu-id="06c0c-115">`$schema` 元素會定義範本語言的版本，並用於 Visual Studio 語法醒目提示及類似的驗證功能。</span><span class="sxs-lookup"><span data-stu-id="06c0c-115">The `$schema` element defines the version of the template language and is used for Visual Studio syntax highlighting and similar validation features.</span></span> <span data-ttu-id="06c0c-116">`contentVersion` 元素不是由 Azure 使用。</span><span class="sxs-lookup"><span data-stu-id="06c0c-116">The `contentVersion` element is not used by Azure.</span></span> <span data-ttu-id="06c0c-117">相反地，它可協助您追蹤範本版本。</span><span class="sxs-lookup"><span data-stu-id="06c0c-117">Instead, it helps you keep track of the template version.</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
  "contentVersion": "1.0.0.0",
```
## <a name="define-parameters"></a><span data-ttu-id="06c0c-118">定義參數</span><span class="sxs-lookup"><span data-stu-id="06c0c-118">Define parameters</span></span>
<span data-ttu-id="06c0c-119">接著，我們會定義兩個參數：`adminUsername` 和 `adminPassword`。</span><span class="sxs-lookup"><span data-stu-id="06c0c-119">Next, we define two parameters, `adminUsername` and `adminPassword`.</span></span> <span data-ttu-id="06c0c-120">參數是您在部署時指定的值。</span><span class="sxs-lookup"><span data-stu-id="06c0c-120">Parameters are values you specify at the time of deployment.</span></span> <span data-ttu-id="06c0c-121">`adminUsername` 參數就是一個 `string`，但是由於 `adminPassword` 是祕密，因此我們賦予它的類型是 `securestring`。</span><span class="sxs-lookup"><span data-stu-id="06c0c-121">The `adminUsername` parameter is simply a `string` type, but because `adminPassword` is a secret, we give it type `securestring`.</span></span> <span data-ttu-id="06c0c-122">稍後，這些參數會被傳送到擴展集組態。</span><span class="sxs-lookup"><span data-stu-id="06c0c-122">Later, these parameters are passed into the scale set configuration.</span></span>

```json
  "parameters": {
    "adminUsername": {
      "type": "string"
    },
    "adminPassword": {
      "type": "securestring"
    }
  },
```
## <a name="define-variables"></a><span data-ttu-id="06c0c-123">定義變數</span><span class="sxs-lookup"><span data-stu-id="06c0c-123">Define variables</span></span>
<span data-ttu-id="06c0c-124">Resource Manager 範本也可讓您定義以後要在範本中使用的變數。</span><span class="sxs-lookup"><span data-stu-id="06c0c-124">Resource Manager templates also let you define variables to be used later in the template.</span></span> <span data-ttu-id="06c0c-125">我們的範例不會使用任何變數，因此我們將 JSON 物件保留空白。</span><span class="sxs-lookup"><span data-stu-id="06c0c-125">Our example doesn't use any variables, so we've left the JSON object empty.</span></span>

```json
  "variables": {},
```

## <a name="define-resources"></a><span data-ttu-id="06c0c-126">定義資源</span><span class="sxs-lookup"><span data-stu-id="06c0c-126">Define resources</span></span>
<span data-ttu-id="06c0c-127">接下來是範本的資源區段。</span><span class="sxs-lookup"><span data-stu-id="06c0c-127">Next is the resources section of the template.</span></span> <span data-ttu-id="06c0c-128">在這裡，您會定義實際想要部署的項目。</span><span class="sxs-lookup"><span data-stu-id="06c0c-128">Here, you define what you actually want to deploy.</span></span> <span data-ttu-id="06c0c-129">與 `parameters` 和 `variables` (這些是 JSON 物件) 不同，`resources` 是一個 JSON 物件的 JSON 清單。</span><span class="sxs-lookup"><span data-stu-id="06c0c-129">Unlike `parameters` and `variables` (which are JSON objects), `resources` is a JSON list of JSON objects.</span></span>

```json
   "resources": [
```

<span data-ttu-id="06c0c-130">所有資源都必須要有 `type`、`name`、`apiVersion` 及 `location` 屬性。</span><span class="sxs-lookup"><span data-stu-id="06c0c-130">All resources require `type`, `name`, `apiVersion`, and `location` properties.</span></span> <span data-ttu-id="06c0c-131">這個範例的第一個資源具有類型 `Microsft.Network/virtualNetwork`、名稱`myVnet`，和 apiVersion `2016-03-30`。</span><span class="sxs-lookup"><span data-stu-id="06c0c-131">This example's first resource has type `Microsft.Network/virtualNetwork`, name `myVnet`, and apiVersion `2016-03-30`.</span></span> <span data-ttu-id="06c0c-132">(若要了解資源類型的最新 API 版本，請參閱 [Azure REST API 文件](https://docs.microsoft.com/rest/api/)。)</span><span class="sxs-lookup"><span data-stu-id="06c0c-132">(To find the latest API version for a resource type, see the [Azure REST API documentation](https://docs.microsoft.com/rest/api/).)</span></span>

```json
     {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "apiVersion": "2016-12-01",
```

## <a name="specify-location"></a><span data-ttu-id="06c0c-133">指定位置</span><span class="sxs-lookup"><span data-stu-id="06c0c-133">Specify location</span></span>
<span data-ttu-id="06c0c-134">為了指定虛擬網路的位置，我們使用 [Resource Manager 範本函式](../azure-resource-manager/resource-group-template-functions.md)。</span><span class="sxs-lookup"><span data-stu-id="06c0c-134">To specify the location for the virtual network, we use a [Resource Manager template function](../azure-resource-manager/resource-group-template-functions.md).</span></span> <span data-ttu-id="06c0c-135">此函式必須括在引號和方括號內，如下所示︰`"[<template-function>]"`。</span><span class="sxs-lookup"><span data-stu-id="06c0c-135">This function must be enclosed in quotes and square brackets like this: `"[<template-function>]"`.</span></span> <span data-ttu-id="06c0c-136">在此案例中，我們使用 `resourceGroup` 函式。</span><span class="sxs-lookup"><span data-stu-id="06c0c-136">In this case, we use the `resourceGroup` function.</span></span> <span data-ttu-id="06c0c-137">此函式不接受任何引數並且會傳回 JSON 物件，此物件含有這項部署之目的地資源群組的相關中繼資料。</span><span class="sxs-lookup"><span data-stu-id="06c0c-137">It takes in no arguments and returns a JSON object with metadata about the resource group this deployment is being deployed to.</span></span> <span data-ttu-id="06c0c-138">資源群組是由使用者在部署時所設定。</span><span class="sxs-lookup"><span data-stu-id="06c0c-138">The resource group is set by the user at the time of deployment.</span></span> <span data-ttu-id="06c0c-139">我們會接著使用 `.location` 來為此 JSON 物件編製索引，以從此 JSON 物件取得位置。</span><span class="sxs-lookup"><span data-stu-id="06c0c-139">We then index into this JSON object with `.location` to get the location from the JSON object.</span></span>

```json
       "location": "[resourceGroup().location]",
```

## <a name="specify-virtual-network-properties"></a><span data-ttu-id="06c0c-140">指定虛擬網路屬性</span><span class="sxs-lookup"><span data-stu-id="06c0c-140">Specify virtual network properties</span></span>
<span data-ttu-id="06c0c-141">每個 Resource Manager 資源都有自己的 `properties` 區段，用於該資源的特定組態。</span><span class="sxs-lookup"><span data-stu-id="06c0c-141">Each Resource Manager resource has its own `properties` section for configurations specific to the resource.</span></span> <span data-ttu-id="06c0c-142">在此案例中，我們要指定虛擬網路應該有一個使用私人 IP 位址範圍 `10.0.0.0/16` 的子網路。</span><span class="sxs-lookup"><span data-stu-id="06c0c-142">In this case, we specify that the virtual network should have one subnet using the private IP address range `10.0.0.0/16`.</span></span> <span data-ttu-id="06c0c-143">擴展集一律是包含在一個子網路內。</span><span class="sxs-lookup"><span data-stu-id="06c0c-143">A scale set is always contained within one subnet.</span></span> <span data-ttu-id="06c0c-144">它不能跨子網路。</span><span class="sxs-lookup"><span data-stu-id="06c0c-144">It cannot span subnets.</span></span>

```json
       "properties": {
         "addressSpace": {
           "addressPrefixes": [
             "10.0.0.0/16"
           ]
         },
         "subnets": [
           {
             "name": "mySubnet",
             "properties": {
               "addressPrefix": "10.0.0.0/16"
             }
           }
         ]
       }
     },
```

## <a name="add-dependson-list"></a><span data-ttu-id="06c0c-145">新增 dependsOn 清單</span><span class="sxs-lookup"><span data-stu-id="06c0c-145">Add dependsOn list</span></span>
<span data-ttu-id="06c0c-146">除了必要的 `type`、`name`、`apiVersion` 和 `location` 屬性，每個資源都能擁有選用的 `dependsOn` 字串清單。</span><span class="sxs-lookup"><span data-stu-id="06c0c-146">In addition to the required `type`, `name`, `apiVersion`, and `location` properties, each resource can have an optional `dependsOn` list of strings.</span></span> <span data-ttu-id="06c0c-147">這份清單會指定此部署中的哪些其他資源必須在部署此資源之前完成。</span><span class="sxs-lookup"><span data-stu-id="06c0c-147">This list specifies which other resources from this deployment must finish before deploying this resource.</span></span>

<span data-ttu-id="06c0c-148">在此案例中，這個清單中只有一個元素，即上述範例中的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="06c0c-148">In this case, there is only one element in the list, the virtual network from the previous example.</span></span> <span data-ttu-id="06c0c-149">之所以指定這項相依性，是因為擴展集必須先有網路存在，才能建立任何 VM。</span><span class="sxs-lookup"><span data-stu-id="06c0c-149">We specify this dependency because the scale set needs the network to exist before creating any VMs.</span></span> <span data-ttu-id="06c0c-150">如此一來，擴展集才能從先前在網路屬性中指定的 IP 位址範圍，為這些 VM 提供私人 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="06c0c-150">This way, the scale set can give these VMs private IP addresses from the IP address range previously specified in the network properties.</span></span> <span data-ttu-id="06c0c-151">dependsOn 清單中每個字串的格式是 `<type>/<name>`。</span><span class="sxs-lookup"><span data-stu-id="06c0c-151">The format of each string in the dependsOn list is `<type>/<name>`.</span></span> <span data-ttu-id="06c0c-152">使用與先前在虛擬網路資源定義中所使用的相同 `type` 和 `name`。</span><span class="sxs-lookup"><span data-stu-id="06c0c-152">Use the same `type` and `name` used previously in the virtual network resource definition.</span></span>

```json
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "apiVersion": "2016-04-30-preview",
       "location": "[resourceGroup().location]",
       "dependsOn": [
         "Microsoft.Network/virtualNetworks/myVnet"
       ],
```
## <a name="specify-scale-set-properties"></a><span data-ttu-id="06c0c-153">指定擴展集屬性</span><span class="sxs-lookup"><span data-stu-id="06c0c-153">Specify scale set properties</span></span>
<span data-ttu-id="06c0c-154">擴展集有許多屬性，可以在擴展集中自訂 VM。</span><span class="sxs-lookup"><span data-stu-id="06c0c-154">Scale sets have many properties for customizing the VMs in the scale set.</span></span> <span data-ttu-id="06c0c-155">如需這些屬性的完整清單，請參閱[擴展集 REST API 文件](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set)。</span><span class="sxs-lookup"><span data-stu-id="06c0c-155">For a full list of these properties, see the [scale set REST API documentation](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set).</span></span> <span data-ttu-id="06c0c-156">針對本教學課程，我們只會設定一些常用的屬性。</span><span class="sxs-lookup"><span data-stu-id="06c0c-156">For this tutorial, we will set only a few commonly used properties.</span></span>
### <a name="supply-vm-size-and-capacity"></a><span data-ttu-id="06c0c-157">提供 VM 大小和容量</span><span class="sxs-lookup"><span data-stu-id="06c0c-157">Supply VM size and capacity</span></span>
<span data-ttu-id="06c0c-158">擴展集需要知道要建立的 VM 大小 (即「SKU 名稱」)，以及要建立多少個這類 VM (即「SKU 容量」)。</span><span class="sxs-lookup"><span data-stu-id="06c0c-158">The scale set needs to know what size of VM to create ("sku name") and how many such VMs to create ("sku capacity").</span></span> <span data-ttu-id="06c0c-159">若要查看有哪些可用的 VM 大小，請參閱 [VM 大小文件](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes)。</span><span class="sxs-lookup"><span data-stu-id="06c0c-159">To see which VM sizes are available, see the [VM Sizes documentation](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).</span></span>

```json
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
       },
```

### <a name="choose-type-of-updates"></a><span data-ttu-id="06c0c-160">選擇更新類型</span><span class="sxs-lookup"><span data-stu-id="06c0c-160">Choose type of updates</span></span>
<span data-ttu-id="06c0c-161">擴展集也需要知道如何處理擴展集上的更新。</span><span class="sxs-lookup"><span data-stu-id="06c0c-161">The scale set also needs to know how to handle updates on the scale set.</span></span> <span data-ttu-id="06c0c-162">目前有兩個選項：`Manual` 和 `Automatic`。</span><span class="sxs-lookup"><span data-stu-id="06c0c-162">Currently, there are two options, `Manual` and `Automatic`.</span></span> <span data-ttu-id="06c0c-163">如需有關兩者之間差異的詳細資訊，請參閱有關[如何升級擴展集](./virtual-machine-scale-sets-upgrade-scale-set.md)的文件。</span><span class="sxs-lookup"><span data-stu-id="06c0c-163">For more information on the differences between the two, see the documentation on [how to upgrade a scale set](./virtual-machine-scale-sets-upgrade-scale-set.md).</span></span>

```json
       "properties": {
         "upgradePolicy": {
           "mode": "Manual"
         },
```

### <a name="choose-vm-operating-system"></a><span data-ttu-id="06c0c-164">選擇 VM 作業系統</span><span class="sxs-lookup"><span data-stu-id="06c0c-164">Choose VM operating system</span></span>
<span data-ttu-id="06c0c-165">擴展集需要知道要放置 VM 的作業系統。</span><span class="sxs-lookup"><span data-stu-id="06c0c-165">The scale set needs to know what operating system to put on the VMs.</span></span> <span data-ttu-id="06c0c-166">在這裡，我們會使用已完全修補的 Ubuntu 16.04-LTS 映像來建立 VM。</span><span class="sxs-lookup"><span data-stu-id="06c0c-166">Here, we create the VMs with a fully patched Ubuntu 16.04-LTS image.</span></span>

```json
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
               "publisher": "Canonical",
               "offer": "UbuntuServer",
               "sku": "16.04-LTS",
               "version": "latest"
             }
           },
```

### <a name="specify-computernameprefix"></a><span data-ttu-id="06c0c-167">指定 computerNamePrefix</span><span class="sxs-lookup"><span data-stu-id="06c0c-167">Specify computerNamePrefix</span></span>
<span data-ttu-id="06c0c-168">擴展集會部署多個 VM。</span><span class="sxs-lookup"><span data-stu-id="06c0c-168">The scale set deploys multiple VMs.</span></span> <span data-ttu-id="06c0c-169">我們會指定 `computerNamePrefix`，而不是指定每個 VM 名稱。</span><span class="sxs-lookup"><span data-stu-id="06c0c-169">Instead of specifying each VM name, we specify `computerNamePrefix`.</span></span> <span data-ttu-id="06c0c-170">擴展集會針對每個 VM 在此名稱前置詞附加索引，因此 VM 名稱的格式會是 `<computerNamePrefix>_<auto-generated-index>`。</span><span class="sxs-lookup"><span data-stu-id="06c0c-170">The scale set appends an index to the prefix for each VM, so VM names have the form `<computerNamePrefix>_<auto-generated-index>`.</span></span>

<span data-ttu-id="06c0c-171">在下列程式碼片段中，我們會使用先前的參數來設定擴展集內所有 VM 的系統管理員使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="06c0c-171">In the following snippet, we use the parameters from before to set the administrator username and password for all VMs in the scale set.</span></span> <span data-ttu-id="06c0c-172">我們使用 `parameters` 範本函式來執行這項作業。</span><span class="sxs-lookup"><span data-stu-id="06c0c-172">We do this with the `parameters` template function.</span></span> <span data-ttu-id="06c0c-173">此函式會接受字串，該字串指定要參考哪些參數，並且輸出該參數的值。</span><span class="sxs-lookup"><span data-stu-id="06c0c-173">This function takes in a string that specifies which parameter to refer to and outputs the value for that parameter.</span></span>

```json
           "osProfile": {
             "computerNamePrefix": "vm",
             "adminUsername": "[parameters('adminUsername')]",
             "adminPassword": "[parameters('adminPassword')]"
           },
```

### <a name="specify-vm-network-configuration"></a><span data-ttu-id="06c0c-174">指定 VM 網路組態</span><span class="sxs-lookup"><span data-stu-id="06c0c-174">Specify VM network configuration</span></span>
<span data-ttu-id="06c0c-175">最後，我們需要為擴展集內的 VM 指定網路組態。</span><span class="sxs-lookup"><span data-stu-id="06c0c-175">Finally, we need to specify the network configuration for the VMs in the scale set.</span></span> <span data-ttu-id="06c0c-176">在此案例中，我們只需要指定稍早建立之子網路的 ID。</span><span class="sxs-lookup"><span data-stu-id="06c0c-176">In this case, we only need to specify the ID of the subnet created earlier.</span></span> <span data-ttu-id="06c0c-177">這會告訴擴展集將網路介面放入這個子網路。</span><span class="sxs-lookup"><span data-stu-id="06c0c-177">This tells the scale set to put the network interfaces in this subnet.</span></span>

<span data-ttu-id="06c0c-178">您可以使用 `resourceId` 範本函式來取得包含該子網路的虛擬網路 ID。</span><span class="sxs-lookup"><span data-stu-id="06c0c-178">You can get the ID of the virtual network containing the subnet by using the `resourceId` template function.</span></span> <span data-ttu-id="06c0c-179">此函式會接受資源的類型和名稱，然後傳回該資源的完整識別碼。</span><span class="sxs-lookup"><span data-stu-id="06c0c-179">This function takes in the type and name of a resource and returns the fully qualified identifier of that resource.</span></span> <span data-ttu-id="06c0c-180">此 ID 的格式為：`/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`</span><span class="sxs-lookup"><span data-stu-id="06c0c-180">This ID has the form: `/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`</span></span>

<span data-ttu-id="06c0c-181">不過，只有虛擬網路的識別碼還不夠。</span><span class="sxs-lookup"><span data-stu-id="06c0c-181">However, the identifier of the virtual network is not enough.</span></span> <span data-ttu-id="06c0c-182">您必須指定擴展集 VM 所在的特定子網路。</span><span class="sxs-lookup"><span data-stu-id="06c0c-182">You must specify the specific subnet that the scale set VMs should be in.</span></span> <span data-ttu-id="06c0c-183">若要這樣做，請將 `/subnets/mySubnet` 串連至虛擬網路的 ID。</span><span class="sxs-lookup"><span data-stu-id="06c0c-183">To do this, concatenate `/subnets/mySubnet` to the ID of the virtual network.</span></span> <span data-ttu-id="06c0c-184">結果是會產生子網路的完整 ID。</span><span class="sxs-lookup"><span data-stu-id="06c0c-184">The result is the fully qualified ID of the subnet.</span></span> <span data-ttu-id="06c0c-185">使用 `concat` 函式來執行這項操作，此函式會接受一系列字串，然後傳回其串連結果。</span><span class="sxs-lookup"><span data-stu-id="06c0c-185">Do this concatenation with the `concat` function, which takes in a series of strings and returns their concatenation.</span></span>

```json
           "networkProfile": {
             "networkInterfaceConfigurations": [
               {
                 "name": "myNic",
                 "properties": {
                   "primary": "true",
                   "ipConfigurations": [
                     {
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
                           "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
                         }
                       }
                     }
                   ]
                 }
               }
             ]
           }
         }
       }
     }
   ]
}

```

## <a name="next-steps"></a><span data-ttu-id="06c0c-186">後續步驟</span><span class="sxs-lookup"><span data-stu-id="06c0c-186">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
